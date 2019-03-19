---
title: Tutorial&#58; Habilitar o cogerenciamento para novos dispositivos Windows 10 baseados na Internet
titleSuffix: Configuration Manager
description: Configure o cogerenciamento de dispositivos Windows 10 para o Configuration Manager e o Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/08/2019
ms.topic: tutorial
ms.prod: configuration-manager
ms.service: ''
ms.technology: ''
ms.assetid: ''
ms.openlocfilehash: 61400d382a539efa495af99795e32fc1f2a517ab
ms.sourcegitcommit: af8693048e6706ffda72572374f56e0bc7dfce2c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/11/2019
ms.locfileid: "57737347"
---
# <a name="tutorial-enable-co-management-for-new-internet-based-devices"></a>Tutorial: Habilitar o cogerenciamento para novos dispositivos baseados na Internet
Com o cogerenciamento, você pode manter seus processos bem estabelecidos para usar o Configuration Manager para gerenciar PCs na sua organização. Ao mesmo tempo, você está investindo na nuvem com o uso do Intune para provisionamento moderno e segurança. 

Neste tutorial, você configura o cogerenciamento de dispositivos Windows 10 em um ambiente com o Azure AD (Active Directory) e um AD local, mas que não têm um [Azure AD (Active Directory) híbrido](https://docs.microsoft.com/azure/active-directory/devices/overview#hybrid-azure-ad-joined-devices). O ambiente do Configuration Manager inclui um único site primário com todas as funções do sistema de sites localizadas no mesmo servidor, o servidor do site. Este tutorial começa com a premissa de que seus dispositivos Windows 10 já estão inscritos no Intune. 

Se você tiver um Azure Active Directory híbrido que una o AD local ao Azure AD, é recomendável seguir nosso tutorial complementar, [Habilitar o cogerenciamento para clientes do Configuration Manager](/sccm/comanage/tutorial-co-manage-clients). 
 
Use este tutorial quando:  
- Você tiver dispositivos Windows 10 para introduzir no cogerenciamento. Esses dispositivos podem ter sido provisionados por meio do Windows Autopilot ou diretamente do OEM do seu hardware. 
- Você tiver dispositivos Windows 10 na Internet que atualmente gerencia com o Intune, aos quais deseja adicionar o cliente do Configuration Manager.


**Neste tutorial, você vai:**  
> [!div class="checklist"]  
> * Examinar os pré-requisitos para o Azure e seu ambiente local
> * Solicitar um certificado SSL público para o CMG (gateway de gerenciamento de nuvem)
> * Habilitar serviços do Azure no Configuration Manager
> * Implantar e configurar um gateway de gerenciamento de nuvem  
> * Configurar o ponto de gerenciamento e os clientes para usar o CMG
> * Habilitar o cogerenciamento no Configuration Manager
> * Configurar o Intune para instalar o cliente do Configuration Manager
> * Atribuir uma licença para serviços de nuvem



## <a name="prerequisites"></a>Pré-requisitos  

### <a name="azure-services-and-environment"></a>Ambiente e serviços do Azure
- Assinatura do Azure ([avaliação gratuita](https://azure.microsoft.com/free)) 
- Azure Active Directory Premium 
- Assinatura do Microsoft Intune 
  > [!TIP]  
  > Uma Assinatura EMS (Enterprise Mobility and Security) inclui o Azure Active Directory Premium e o Microsoft Intune. Assinatura EMS ([avaliação gratuita](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

- Os usuários devem [receber licenças](tutorial-co-manage-clients.md#assign-intune-licenses-to-users) para o *Intune* e o *Azure Active Directory Premium*
- O Intune é configurado para [inscrição automática de dispositivos](tutorial-co-manage-clients.md#configure-auto-enrollment-of-devices-to-intune)  


### <a name="on-premises-infrastructure"></a>Infraestrutura local
- Branch atual do System Center Configuration Manager, versão 1810 ou posterior.  
  
  A versão 1810 introduz o [HTTP Avançado](/sccm/core/plan-design/hierarchy/enhanced-http), que é usado neste tutorial para evitar requisitos de PKI mais complexos. Usando o HTTP Avançado, o site primário que você usa para gerenciar clientes deve ser configurado para usar certificados gerados pelo Configuration Manager para sistemas de sites HTTP.  
   
  A versão 1810 também introduz uma linha de comando mais simples para a instalação baseada na Internet do cliente do Configuration Manager.

- A [Autoridade de MDM](https://docs.microsoft.com/sccm/mdm/deploy-use/change-mdm-authority) deve ser definida para o Intune  

### <a name="external-certificates"></a>Certificados externos:
- Certificado de autenticação de servidor do CMG. Esse certificado é um certificado SSL de um provedor de certificados público e globalmente confiável. Por exemplo, DigiCert, Thawte ou VeriSign, entre outros. Você vai exportar esse certificado como um arquivo .PFX com Chave Privada.  

- Mais adiante neste tutorial, fornecemos instruções sobre como configurar a solicitação para esse certificado.

### <a name="permissions"></a>Permissões
Ao longo deste tutorial, use as seguintes permissões para concluir tarefas:
- Uma conta que seja um *administrador global* no Azure  
- Uma conta que seja um *administrador de domínio* na sua infraestrutura local  
- Uma conta que seja um *administrador completo* para *todos* os escopos no Configuration Manager   


## <a name="request-a-public-certificate-for-the-cloud-management-gateway"></a>Solicitar um certificado público para o gateway de gerenciamento de nuvem
Quando os dispositivos estão na Internet, o cogerenciamento exige o CMG (gateway de gerenciamento de nuvem) do Configuration Manager. O CMG permite que os dispositivos Windows 10 baseados na Internet se comuniquem com a sua implantação local do Configuration Manager. Para estabelecer uma relação de confiança entre os dispositivos e o ambiente do Configuration Manager, o CMG requer um certificado SSL.

Este tutorial usa um certificado público chamado **certificado de autenticação de servidor do CMG** que deriva autoridade de um provedor de certificados globalmente confiáveis. Embora seja possível configurar o cogerenciamento usando os certificados que derivam autoridade da sua autoridade de certificação local da Microsoft, o uso de certificados autoassinados está além do escopo deste tutorial.

O **certificado de autenticação de servidor do CMG** é usado para criptografar o tráfego de comunicações entre o cliente do Configuration Manager e o CMG. O certificado é rastreado para uma Raiz Confiável para verificar a identidade do servidor para o cliente. O certificado público inclui uma Raiz Confiável na qual os clientes do Windows já confiam.

Sobre esse certificado: 

- Você identifica um nome exclusivo para o serviço CMG no Azure e, em seguida, especifica esse nome na solicitação de certificado.  
- Você gera a solicitação de certificado em um servidor específico e, em seguida, envia a solicitação para um provedor de certificados públicos para receber o certificado SSL necessário.  
- Você importa para o sistema que gerou a solicitação o certificado que recebe de volta do provedor. Você usa o mesmo computador para exportar o certificado para uso quando, posteriormente, implanta o CMG no Azure.  
- Quando o CMG é instalado, ele cria um serviço CMG no Azure usando o nome especificado no certificado.  

### <a name="identify-a-unique-name-for-your-cloud-management-gateway-in-azure"></a>Identificar um nome exclusivo para o gateway de gerenciamento de nuvem no Azure
Ao solicitar o certificado de autenticação de servidor do CMG, você especifica o que deve ser um nome exclusivo para identificar o *Serviço de nuvem (clássico)* no Azure. Por padrão, a nuvem pública do Azure usa *cloudapp.net* e o CMG é hospedado no domínio cloudapp.net como *\<SeuNomeDNSExclusivo>.cloudapp.net*.  

> [!TIP]  
> Neste tutorial, o **certificado de autenticação de servidor do CMG** usa um FQDN que termina em *contoso.com*.  Depois que criarmos o CMG, vamos configurar um registro de nome canônico (CNAME) no DNS público da nossa organização. Esse registro cria um alias para o CMG que é mapeado para o nome que usamos no certificado público.  

Antes de solicitar o certificado púbico, confirme se o nome que deseja usar está disponível no Azure. Você não cria o serviço diretamente no Azure. Em vez disso, o nome que é especificado no certificado público que você solicita é usado pelo Configuration Manager para criar o serviço de nuvem quando você instala o CMG.  

1. Entre no [portal do Microsoft Azure](https://portal.azure.com/).  

2. Selecione **Criar um recurso**, escolha a categoria **Computação** e, em seguida, selecione **Serviço de Nuvem**. A folha Serviço de nuvem (clássico) é aberta.

3. Para **Nome DNS**, especifique o nome do prefixo para o serviço de nuvem que você usará. Esse prefixo deve ser o mesmo ao que será usado posteriormente quando você solicitar um certificado público para o certificado de autenticação de servidor do CMG. Usamos *MyCSG*, que cria o namespace *MyCSG.cloudapp.net*. A interface confirma se o nome está disponível ou se já está sendo usado por outro serviço.  
 Depois de confirmar se o nome que deseja usar está disponível, você está pronto para enviar a CSR (Solicitação de Assinatura de Certificado).

### <a name="request-the-certificate"></a>Solicitar o certificado
Use as informações a seguir para enviar uma solicitação de assinatura de certificado para o seu CMG a um provedor de certificados públicos. Altere os valores a seguir para que sejam relevantes ao seu ambiente.  

- *MyCMG* para identificar o nome do serviço do gateway de gerenciamento de nuvem
- *Contoso* como o nome da empresa
- *Contoso.com* como o domínio público

É recomendável usar o seu servidor do site primário para gerar a CSR (solicitação de assinatura de certificado). Ao receber o certificado, você deverá inscrevê-lo no mesmo servidor que gerou a CSR, do contrário, não será possível exportar a chave privada dos certificados, o que é obrigatório.  

Solicite um tipo de provedor de chave de versão 2 ao gerar uma CSR. Somente os certificados de versão 2 são permitidos.  

> [!TIP]  
> Quando implantarmos o CMG, também instalaremos um CDP (ponto de distribuição na nuvem) ao mesmo tempo. Por padrão, quando você implanta um CMG, a opção **Permitir que CMG funcione como um ponto de distribuição na nuvem e ofereça conteúdo de armazenamento do Azure** é selecionada. A colocalização do CDP no servidor com o CMG elimina a necessidade de certificados e configurações diferentes para dar suporte ao CDP. Mesmo que o CDP não precise usar o cogerenciamento, ele é útil na maioria dos ambientes.  
>
> Se for usar pontos adicionais de distribuição na nuvem para cogerenciamento, será preciso solicitar certificados separados para cada servidor a mais. Para solicitar um certificado público para o CDP, use os mesmos detalhes usados para a CSR do gateway de gerenciamento de nuvem. Você só precisa alterar o nome comum para que ele seja exclusivo para cada CDP.  

**Detalhes para a CSR do gateway de gerenciamento de nuvem**
- **Nome comum**: ClousServiceNameCMG.YourCompanyPubilcDomainName.com  
Exemplo: MyCSG.contoso.com  
- **Nome Alternativo da Entidade**: igual ao CN (Nome Comum)  
- **Organização**:  o nome da sua organização  
- **Departamento**: de acordo com a sua organização  
- **Cidade**: de acordo com a sua organização  
- **Estado**: de acordo com a sua organização  
- **País**: de acordo com a sua organização  
- **Tamanho da chave: 2048**  
- **Provider: Microsoft RSA SChannel Cryptographic Provider**  

### <a name="import-the-certificate"></a>Importar o certificado
Depois de receber o certificado público, importe-o para o repositório de certificados local do computador que criou a CSR. Em seguida, exporte o certificado como um arquivo .PFX para que seja possível usá-lo para o CMG no Azure.  

Os provedores de certificados públicos geralmente fornecem instruções para importação do certificado. O processo para importar o certificado deve ser parecido com estas orientações:  

1. No computador em que o certificado deve ser importado, localize o arquivo .pfx do certificado.  

2. Clique com botão direito do mouse no arquivo e selecione **Instalar PFX**  

3. Quando o Assistente para Importação de Certificados for iniciado, selecione **Avançar**.  

4. Na página **Arquivo a Ser Importado**, selecione **Avançar**. 

5. Na página **Senha**, insira a senha para a chave privada na caixa Senha e selecione **Avançar**.  
  
   Selecione a opção para tornar a chave exportável.

6. Na página **Repositório de Certificados**, escolha **Selecionar automaticamente o repositório de certificados conforme o tipo de certificado** e selecione **Avançar**.  

7.  Selecione **Concluir**.

### <a name="export-the-certificate"></a>Exportar o certificado
Exporte o *certificado de autenticação de servidor do CMG* do seu servidor. Exportar novamente o certificado o torna utilizável para o gateway de gerenciamento de nuvem no Azure.  

1. No servidor em que você importou o certificado SSL público, execute **certlm.msc** para abrir o console do Gerenciador de Certificados.  

2. No console do Gerenciador de Certificados, selecione **Pessoal > Certificados**. Em seguida, clique com o botão direito do mouse no *certificado de autenticação de servidor do CMG* que você inscreveu no procedimento anterior e selecione **Todas as Tarefas > Exportar**.  

3. No Assistente para Exportação de Certificados, selecione **Avançar**, selecione **Sim, exportar a chave privada** e clique em **Avançar**.  

4. Na página Formato do Arquivo de Exportação, selecione **Troca de Informações Pessoais – PKCS nº 12 (.PFX)**, selecione **Avançar** e forneça uma senha. Para o nome do arquivo, especifique um nome como **C:\ConfigMgrCloudMGServer**. Você vai fazer referência a esse arquivo quando criar o CMG no Azure.  

5. Selecione **Avançar** e confirme as seguintes configurações antes de selecionar **Concluir** para completar a exportação:  

   - Exportar Chaves = Sim  
   - Incluir todos os certificados no caminho da certificação = Sim  
   - Formato do arquivo = Troca de Informações Pessoais (*.pfx)  

6. Depois de concluir a exportação, localize o arquivo .pfx e coloque uma cópia dele em **C:\Certs** no servidor do site primário do Configuration Manager que vai gerenciar os clientes baseados na Internet. Certs é uma pasta temporária que deve ser usada para transferir certificados entre servidores. Você acessa o arquivo de certificado do servidor do site primário quando implanta o gateway de gerenciamento de nuvem no Azure.  

Depois de copiar o certificado para o servidor do site primário, você pode excluir o Certificado do repositório de Certificados Pessoais do servidor membro. 


## <a name="enable-azure-cloud-services-in-configuration-manager"></a>Habilitar serviços de nuvem do Azure no Configuration Manager
Para configurar os serviços do Azure de dentro do console do Configuration Manager, use o assistente para Configurar Serviços do Azure e crie dois aplicativos do Azure Active Directory.  

- **Aplicativo de servidor**: um *aplicativo Web* no Azure Active Directory  
- **Aplicativo de cliente**: um aplicativo *Cliente Nativo* no Azure Active Directory  

Execute o procedimento a seguir no servidor do site primário.  

1. No servidor do site primário, abra o console do Configuration Manager e vá para **Administração > Serviços de Nuvem > Serviços do Azure** e selecione **Configurar Serviços do Azure**.  

   Na página Configurar Serviços do Azure, especifique um nome amigável para o serviço de gerenciamento de nuvem que você está configurando. Por exemplo: *Meu serviço de gerenciamento de nuvem*   

   Em seguida, selecione **Gerenciamento de Nuvem** e **Avançar**.  
   
   > [!TIP]  
   > Confira mais informações sobre as configurações feitas no assistente em [Iniciar o assistente para Serviços do Azure](https://docs.microsoft.com/sccm/core/servers/deploy/configure/Azure-services-wizard#start-the-azure-services-wizard)


2. Na página **Propriedades do Aplicativo**, em **Aplicativo Web**, selecione **Procurar** para abrir a caixa de diálogo **Aplicativo de Servidor** e selecione **Criar**. Configure os seguintes campos:

   - **Nome do aplicativo**: especifique um nome amigável para o aplicativo, como *aplicativo web de Gerenciamento de Nuvem*.  

   - **URL da home page**: esse valor não é usado pelo Configuration Manager, mas é exigido pelo Azure Active Directory. Por padrão, esse valor é https://ConfigMgrService.  
   
   - **URI da ID do aplicativo**: esse valor precisa ser exclusivo no locatário do Azure AD. Ele está localizado no token de acesso usado pelo cliente do Configuration Manager para solicitar o acesso ao serviço. Por padrão, esse valor é https://ConfigMgrService.  

   Em seguida, selecione **Conectar** e especifique uma conta de Administrador Global do Azure. Essas credenciais não são salvas pelo Configuration Manager. Essa persona não exige permissões no Configuration Manager e não precisa ser a mesma conta que executa o Assistente para Serviços do Azure. 

   Depois que você entrar, os resultados são exibidos. Selecione **OK** para fechar a caixa de diálogo Criar Aplicativo de Servidor e retornar à página Propriedades do Aplicativo. 

3. Para **aplicativo Cliente Nativo**, selecione **Procurar** para abrir a caixa de diálogo **Aplicativo cliente**. 

4. Selecione **Criar** para abrir a caixa de diálogo **Criar Aplicativo Cliente** e, em seguida, configure os seguintes campos:  

   - **Nome do aplicativo**: especifique um nome amigável para o aplicativo, como *aplicativo cliente nativo de Gerenciamento de Nuvem*.
   
   - **URL de resposta**: esse valor não é usado pelo Configuration Manager, mas é exigido pelo Azure AD. Por padrão, esse valor é https://ConfigMgrClient.
   Em seguida, selecione **Conectar** e especifique uma conta de Administrador Global do Azure. Como o aplicativo Web, essas credenciais não serão salvas e não exigem permissões no Configuration Manager.
   
   Depois que você entrar, os resultados são exibidos. Selecione **OK** para fechar a caixa de diálogo Criar Aplicativo Cliente e retornar à página Propriedades do Aplicativo. Selecione **Avançar** para continuar.

5. Na página **Definir Configurações de Descoberta**, marque a caixa **Habilitar a Descoberta de Usuários do Azure Active Directory**, selecione **Avançar** e conclua a configuração das caixas de diálogo Descoberta para o seu ambiente.  

6. Continue pelas páginas Resumo, Progresso e Conclusão e feche o assistente.  

   Os Serviços do Azure para a Descoberta de usuários do Azure Active Directory agora estão habilitados no Configuration Manager.  Deixe o console aberto por enquanto.  

7. Abra um navegador e entre no [portal do Azure](https://portal.azure.com/).  

8. Selecione **Todos os serviços > Azure Active Directory > Registros de aplicativo**e, em seguida:

   1. Selecione o aplicativo Web que você criou. 

   2. Vá para **Configurações > Permissões necessárias**, selecione **Conceder permissões** e selecione **Sim**.  

   3. Selecione o aplicativo Cliente Nativo que você criou. 

   4. Vá para **Configurações > Permissões necessárias**, selecione **Conceder permissões** e selecione **Sim**.  

9. No console do Configuration Manager, vá para **Administração > Visão Geral > Serviços de Nuvem > Serviços do Azure** e selecione o seu Serviço do Azure. Em seguida, clique com o botão direito do mouse em **Descoberta de Usuários do Azure Active Directory** e selecione **Executar Descoberta Completa Agora**. Selecione **Sim** para confirmar a ação.  

10. No servidor do site primário, abra **SMS_AZUREAD_DISCOVERY_AGENT.log** do Configuration Manager e procure a seguinte entrada para confirmar se essa descoberta está funcionando:  *UDX publicado com êxito para usuários do Azure Active Directory*  

    Por padrão, o arquivo de log está em *%Program_Files%\Microsoft Configuration Manager\Logs*.  


## <a name="create-the-cloud-services-in-azure"></a>Criar os serviços de nuvem no Azure
**Nesta seção do tutorial, você vai**:
- Criar o serviço de nuvem do CMG  
- Criar registros CNAME de DNS para ambos os serviços  

### <a name="create-the-cmg"></a>Criar o CMG
Use este procedimento para instalar um gateway de gerenciamento de nuvem como um serviço no Azure. O CMG é instalado no site de camada superior da hierarquia. Neste tutorial, continuamos usando o site primário em que os certificados foram inscritos e exportados.

1. No servidor do site primário, abra o console do Configuration Manager e vá para **Administração > Visão Geral > Serviços de Nuvem > Gateway de Gerenciamento de Nuvem** e selecione **Criar Gateway de Gerenciamento de Nuvem**.  

2. Na página **Geral**:  

   1. Selecione o seu ambiente de nuvem para **ambiente do Azure**. Este tutorial usa **AzurePublicCloud**.  
   
   2. Selecione **Implantação do Azure Resource Manager**.  
  
   3. **Entre** na sua assinatura do Azure. O Configuration Manager preenche informações adicionais com base nas informações configuradas quando você habilitou os serviços de nuvem do Azure para o Configuration Manager.  

   Selecione **Avançar** para continuar.  

3. Na página **Configurações**, procure e selecione o arquivo chamado **ConfigMgrCloudMGServer.pfx**, que é o arquivo que você exportou após a importação do certificado de autenticação de servidor do CMG. Depois que você especifica a senha, o **Nome do serviço** e o **Nome da implantação** são preenchidos automaticamente, com base nos detalhes do arquivo de certificado .pfx. 

4. Defina a sua **Região**.

5. Para **Grupo de Recursos**, use um grupo de recursos existente ou crie um grupo com um nome amigável que não use espaços, como **CofigMgrCloudServices**. Se você optar por criar um grupo, o grupo será adicionado como um grupo de recursos no Azure.  

6. A menos que você esteja pronto para configurar em grande escala, use um (1) para o número de **Instâncias de VM**. O número de instâncias de VM permite que um único Serviço de nuvem CMG (Gateway de Gerenciamento de Nuvem) expanda para dar suporte a mais conexões de cliente. Posteriormente, você pode usar o console do Configuration Manager para retornar e editar o número de instâncias de VM que usa.  

7. Habilite a caixa de seleção para **Verificar Revogação de Certificado de Cliente**. 

8. Habilite a caixa de seleção para **Permitir que CMG funcione como um ponto de distribuição na nuvem e ofereça conteúdo de armazenamento do Azure** se desejar implantar um ponto de distribuição na nuvem com o CMG.

9. Selecione **Avançar** para continuar.

10. Examine os valores na página **Alerta** e selecione **Avançar**.

11. Examine a página **Resumo** e clique em **Avançar** para criar o Serviço de Nuvem do gateway de gerenciamento de nuvem. Selecione **Fechar** para concluir o assistente.  

12. No nó Gateway de Gerenciamento de Nuvem do console do Configuration Manager, agora você pode ver o novo serviço.  

### <a name="create-dns-cname-records"></a>Criar registros CNAME de DNS

Ao criar uma entrada DNS para o CMG, você habilita os dispositivos Windows 10 dentro e fora da sua rede corporativa para usar resolução de nomes para encontrar o serviço de nuvem do CMG no Azure.

Nosso exemplo de registro CNAME usa os seguintes detalhes:  

- O nome da empresa é **Contoso** com um namespace DNS público de ***Contoso.com***.  

- O nome do serviço CMG é **MyCMG**, que se torna ***MyCMG.CloudApp.Net*** no Azure.  

Exemplo de registro CNAME: *MyCMG.contoso.com => My.cloudapp.net*

## <a name="configure-the-management-point-and-clients-to-use-the-cmg"></a>Configurar o ponto de gerenciamento e os clientes para usar o CMG
Defina configurações que permitam que os clientes e pontos de gerenciamento local usem o gateway de gerenciamento de nuvem. 

Como usamos o HTTP Avançado para comunicações do cliente, não há necessidade de usar um ponto de gerenciamento HTTPS.  

### <a name="create-the-cmg-connection-point"></a>Criar o ponto de conexão do CMG
Configure o site para dar suporte ao HTTP Avançado.  

1. No console do Configuration Manager, acesse **Administração > Visão Geral > Configuração do Site > Sites** e abra as propriedades do site primário.  

2. Na guia **Comunicação do Computador Cliente**, selecione a opção *HTTPS ou HTTP* para **Use os certificados gerados pelo Configuration Manager para sistemas de sites HTTP** e selecione **OK** para salvar a configuração. 

3. Agora vá para **Administração > Visão Geral > Configuração do Site > Servidores e Funções do Sistema de Sites** e selecione o servidor com um ponto de gerenciamento em que você deseja instalar o ponto de conexão do gateway de gerenciamento de nuvem.  

4. Selecione **Adicionar Funções do Sistema de Sites** e **Avançar**> **Avançar**.  

5. Selecione o **Ponto de conexão do gateway de gerenciamento de nuvem** e, em seguida, selecione **Avançar** para continuar.  

6. Revise as seleções padrão na página **Ponto de conexão do gateway de gerenciamento de nuvem** e verifique se o CMG correto está selecionado. Em caso de vários gateways de gerenciamento de nuvem, você pode usar a lista suspensa para especificar um CMG diferente. Você também pode alterar o CMG em uso, após a instalação. Selecione **Avançar** para continuar.

7. Selecione **Avançar** para iniciar a instalação e exiba os resultados na página Conclusão.  Selecione **Fechar** para concluir a instalação do ponto de conexão. 

8. Agora vá para **Administração > Visão Geral > Configuração do Site > Servidores e Funções do Sistema de Sites** e abra as **Propriedades** para o ponto de gerenciamento em que você instalou o ponto de conexão. Na guia **Geral**, marque a caixa para **Permitir tráfego do gateway de gerenciamento de nuvem do Configuration Manager** e selecione **OK** para salvar a configuração. 
   > [!TIP]  
   > Embora não seja necessário habilitar o cogerenciamento, é recomendável fazer essa mesma edição para qualquer ponto de atualização de software. 

### <a name="configure-client-settings-to-direct-clients-to-use-the-cmg"></a>Definir configurações do cliente para orientar os clientes a usar o CMG
Use as Configurações do Cliente de modo a definir os clientes do Configuration Manager para se comunicarem com o CMG.  

1. Abra o **console do Configuration Manager > Administração > Visão Geral > Configurações do Cliente** e edite as **Configurações do Cliente Padrão**.  

2. Selecione **Serviços de Nuvem**.

3. Na página **Configurações Padrão**, defina as seguintes configurações para = **Sim**  

   - **Registrar automaticamente novos dispositivos ingressados em domínio do Windows 10 com o Azure Active Directory**  

   - **Habilitar clientes a usarem um gateway de gerenciamento de nuvem** 

   - **Permitir acesso ao ponto de distribuição na nuvem** 

4. Na página **Política do Cliente**, defina **Habilitar solicitações da política de usuário de clientes da Internet** = **Sim** 

1. Selecione **OK** para salvar esta configuração. 



## <a name="enable-co-management-in-configuration-manager"></a>Habilitar o cogerenciamento no Configuration Manager
Com as configurações do Azure, as funções do sistema de sites e as configurações do cliente em vigor, você pode configurar o Configuration Manager para habilitar o cogerenciamento. No entanto, você ainda precisará fazer algumas configurações no Intune depois de habilitar o cogerenciamento antes da conclusão deste tutorial. Uma dessas tarefas é configurar o Intune para implantar o cliente do Configuration Manager. Essa tarefa fica mais fácil com o salvamento da linha de comando para a implantação do cliente, que está disponível no Assistente para Configuração de Cogerenciamento. Por essa razão habilitamos o cogerenciamento agora, antes de concluirmos a configuração do Intune. 

> [!TIP]  
>  Na etapa seis do procedimento a seguir, você atribuirá uma coleção como uma *Grupo piloto* para o cogerenciamento. Esse é um grupo que contém um número pequeno de clientes para testar as suas configurações de cogerenciamento. É recomendável criar uma coleção adequada antes de iniciar o procedimento. Em seguida, você pode selecionar essa coleção sem sair do procedimento para isso.  
 
1. No console do Configuration Manager, acesse **Administração** > **Visão Geral** > **Serviços de Nuvem** > **Cogerenciamento**.

2. Na guia Início, no grupo Gerenciar, selecione **Configurar cogerenciamento** para abrir o Assistente para Configuração de Cogerenciamento.

3. Na página *Assinatura*, selecione **Conectar**, entre no seu locatário do Intune e selecione **Avançar**.

4. Na página *Habilitação*, na lista suspensa *Registro automático no Intune*, selecione uma das seguintes opções:  

   - **Piloto**  - *(recomendado)* membros da coleção que você especifica são automaticamente inscritos no Intune e podem ser cogerenciados. Especifique a coleção piloto na página *Preparo* desse assistente. Essa opção permite testar o cogerenciamento em um subconjunto de clientes. Em seguida, você pode distribuir o cogerenciamento para clientes adicionais usando uma abordagem em fases.  

   - **Todos**: o cogerenciamento é habilitado para todos os clientes.  

   Antes de passar para a próxima página do assistente, selecione **Copiar** e salve a linha de comando CCMSetup que é fornecida. Você usará a linha de comando posteriormente quando configurar o Intune para implantar o cliente do Configuration Manager. Se você não salvar essa linha de comando agora, será possível revisar a configuração do cogerenciamento a qualquer momento para obter essa linha de comando. 

5. Na página *Cargas de Trabalho*, é possível alternar cargas de trabalho no **Configuration Manager** para uma das seguintes e, quando estiver pronto para continuar, selecionar **Avançar**.  
   
   - **Piloto Intune**: alterna uma carga de trabalho apenas para os dispositivos no grupo Piloto. Você atribuirá uma coleção como o grupo Piloto na próxima página do assistente.  
   
   - **Intune**: alterna a carga de trabalho associada para todos os dispositivos Windows 10 cogerenciados.  

   Não é necessário alternar quaisquer cargas de trabalho no momento em que você habilita o cogerenciamento. É possível revisitar essa configuração no console do Configuration Manager posteriormente, depois que o cogerenciamento é configurado.  

   Antes de alternar uma carga de trabalho, certifique-se de que a carga de trabalho correspondente no Intune esteja configurada e implantada. Fazer isso mantém as cargas de trabalho gerenciadas.  

6. Na página *Preparo*, especifique uma coleção a ser usada para a **Coleção Piloto** e clique em **Avançar**. A coleção que você especifica é usada como parte da distribuição em fases do cogerenciamento. Você pode alterar as coleções no grupo piloto a qualquer momento por meio das propriedades de cogerenciamento.  

7. Na página *Resumo*, selecione **Avançar** e, em seguida, **Fechar** para concluir o Assistente.  

## <a name="use-intune-to-deploy-the-configuration-manager-client"></a>Usar o Intune para implantar o cliente do Configuration Manager
Você pode usar o Intune para instalar o cliente do Configuration Manager em dispositivos Windows 10 que atualmente são gerenciados apenas com o Intune.  

Assim, quando um dispositivo Windows 10 anteriormente não gerenciado se inscrever no Intune, ele instalará automaticamente o cliente do Configuration Manager.

### <a name="create-an-intune-app-to-install-the-configuration-manager-client"></a>Criar um aplicativo Intune para instalar o cliente do Configuration Manager

1. No servidor do site primário, entre no [portal do Azure](https://portal.azure.com/) e vá para **Intune > Aplicativos cliente > Aplicativos > Adicionar**.

2. Para **Tipo de aplicativo**: selecione **Aplicativo de linha de negócios**.

3. Selecione **Arquivo do pacote do aplicativo** e navegue até o local do arquivo do Configuration Manager **ccmsetup.msi** e selecione **Abrir > OK**.
Por exemplo, *C:\Arquivos de Programas\Microsoft Configuration Manager\bin\i386\ccmsetup.msi*   

4. Selecione **Informações do Aplicativo** e especifique os seguintes detalhes:
   - **Descrição**: Cliente do Gerenciador de Configurações  

   - **Publicador**: Microsoft  

   - **Argumentos de linha de comando**:  *\<Especifique a linha de comando **CCMSETUPCMD**. Você pode usar a linha de comando que salvou na página* Habilitação *do Assistente para Configuração do Cogerenciamento. Essa linha de comando inclui os nomes do seu serviço de nuvem e os valores adicionais que permitem que os dispositivos instalem o software cliente do Configuration Manager.>*  

     A estrutura da linha de comando deve ser semelhante a este exemplo usando apenas os parâmetros CCMSETUPCMD e SMSSiteCode:  
 
         CCMSETUPCMD="CCMHOSTNAME=<ServiceName.CLOUDAPP.NET/CCM_Proxy_MutualAuth/<GUID>" SMSSiteCode="<YourSiteCode>"  

     > [!TIP]  
     > Se a linha de comando não estiver disponível, você poderá exibir as propriedades de *CoMgmtSettingsProd* no console do Configuration Manager para obter uma cópia da linha de comando.    

5. Selecione **OK > Adicionar**.  O aplicativo é criado e se torna disponível no console do Intune. Depois que o aplicativo estiver disponível, use a seção a seguir para configurar o Intune para atribuí-lo aos dispositivos Windows 10.

### <a name="assign-the-intune-app-to-install-the-configuration-manager-client"></a>Atribuir o aplicativo Intune para instalar o cliente do Configuration Manager
O procedimento a seguir implanta o aplicativo para instalar o cliente do Configuration Manager criado no procedimento anterior. 

1. Entre no [portal do Azure](https://portal.azure.com/).  Selecione **Todos os serviços > Intune > Aplicativos cliente > Aplicativos** e selecione **Inicialização da Configuração do Cliente ConfigMgr**, o aplicativo criado para implantar o cliente do Configuration Manager.  

2. Selecione **Atribuições > Adicionar grupo**.  Defina **Tipo de atribuição** como **Obrigatório** e use **Grupos Incluídos** e **Grupos Excluídos** para definir os grupos do Azure AD (Active Directory) que têm usuários e dispositivos que você deseja que participem do cogerenciamento.  

3. Selecione **OK** e **salve** a configuração.
Agora o aplicativo é obrigatório para usuários e dispositivos aos quais você o atribuiu. Depois que o aplicativo instala o cliente do Configuration Manager em um dispositivo, ele é gerenciado pelo cogerenciamento.

## <a name="assign-intune-licenses-to-users"></a>Atribuir licenças do Intune aos usuários   
Uma ação frequentemente negligenciada, porém, crítica, é atribuir uma licença do Intune a cada usuário que usa um dispositivo cogerenciado.  

Para atribuir licenças a grupos de usuários, use o Azure Active Directory.  

1. Entre no [portal do Azure](https://portal.azure.com/) com uma conta de Administrador. Para gerenciar licenças, a conta deve ter uma função Administrador global ou administrador da conta do usuário.  

2. Selecione **Todos os serviços** no painel de navegação esquerdo e selecione **Azure Active Directory**.  

3. No painel **Azure Active Directory**, selecione **Licenças** para abrir um painel no qual é possível ver e gerenciar todos os produtos licenciáveis no locatário.  
 
4. Em **Todos os produtos**, selecione a sua opção de produto que inclui a licença do Intune e selecione **Atribuir** na parte superior do painel.  

   Por exemplo, você pode selecionar **Enterprise Mobility + Security E5**, se é como você obtém o Intune.  

5. No painel **Atribuir licença**, clique em **Usuários e grupos** para abrir o painel **Usuários e grupos**. Selecione os grupos e usuários individuais a quem deseja atribuir uma licença.  Em seguida, clique em **Selecionar** na parte inferior do painel para confirmar a seleção.  

6. No painel **Atribuir licença**, clique em **Opções de atribuição** para exibir todos os planos de serviço incluídos no produto selecionado anteriormente. Se você tiver selecionado um único produto, como o Intune, somente esse produto será mostrado.  
   - Defina **Microsoft Intune** como **Ativado**.  
   - Atribua a cada usuário uma licença para o **Azure Active Directory Premium**.  

   Quando as licenças aplicáveis forem atribuídas, selecione **OK**.  

7. Para concluir a atribuição, no painel **Atribuir licença**, clique em **Atribuir** na parte inferior do painel.  

8. Uma notificação é exibida no canto superior direito que mostra o status e o resultado do processo. Se a atribuição ao grupo não puder ser concluída (por exemplo, devido a licenças preexistentes no grupo), clique na notificação para ver os detalhes da falha. 


## <a name="summary"></a>Resumo 
Depois de concluir as etapas de configuração deste tutorial, incluindo a última ação para garantir que as licenças sejam atribuídas, os seus dispositivos poderão ser cogerenciados com êxito. 

## <a name="next-steps"></a>Próximas etapas
- Verificar o status de dispositivos cogerenciados com o [painel de cogerenciamento](https://docs.microsoft.com/sccm/core/clients/manage/co-management-dashboard)
- Usar o [Windows Autopilot]() para provisionar novos dispositivos
- Usar o [acesso condicional](https://docs.microsoft.com/sccm/comanage/quickstart-conditional-access) e regras de conformidade do Intune para gerenciar o acesso do usuário aos recursos corporativos
