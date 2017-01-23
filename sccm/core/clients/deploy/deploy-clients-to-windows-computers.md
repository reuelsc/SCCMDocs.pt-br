---
title: Implantar clientes Windows | Microsoft Docs
description: Saiba como implantar clientes em computadores Windows no System Center Configuration Manager.
ms.custom: na
ms.date: 12/27/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
caps.latest.revision: 13
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 9555a16d97224a1cf49a426ab225468b07403f60
ms.openlocfilehash: 0e5e624fdfc2b5ee5b497d1063bd4e2d15df578b


---
# <a name="how-to-deploy-clients-to-windows-computers-in-system-center-configuration-manager"></a>Como implantar clientes em computadores Windows no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de instalar os clientes do Configuration Manager, verifique se todos os [pré-requisitos](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) estão em vigor e se você concluiu todas as configurações de implantação necessárias.   

##  <a name="a-namebkmkclientpusha-how-to-install-clients-with-client-push"></a><a name="BKMK_ClientPush"></a> Como instalar clientes com push de cliente  

Você pode configurar a instalação do cliente por push para um site, e a instalação será executada automaticamente nos computadores descobertos nos limites configurados do site quando esses limites forem configurados como um grupo de limites. Ou, você pode iniciar uma instalação do cliente por push executando o Assistente de Instalação do Cliente por Push para uma coleção ou um recurso específico em uma coleção.  

Você também pode usar o Assistente de Instalação do Cliente por Push para instalar o cliente do Configuration Manager para resultados de [consulta](../../../core/servers/manage/queries-technical-reference.md). Para que a instalação tenha êxito, um dos itens retornados pela consulta deve ser o atributo **ResourceID** da classe de atributos **Recurso do Sistema**.   

Se o servidor do site não puder entrar em contato com o computador cliente nem iniciar o processo de instalação, ele repetirá automaticamente a tentativa de instalação a cada hora por até 7 dias.  

Para ajudar a acompanhar o processo de instalação do cliente, instale um ponto de status de fallback antes de instalar os clientes. Quando um ponto de status de fallback é instalado, ele é atribuído automaticamente a clientes quando eles são instalados pelo método de instalação do cliente por push. Exiba os relatórios de atribuição e de implantação do cliente para acompanhar o andamento da instalação do cliente. 

Os arquivos de log do cliente fornecem informações mais detalhadas para solução de problemas e não requerem um ponto de status de fallback. Por exemplo, o arquivo CCM.log no servidor do site registra quaisquer problemas que o servidor do site tenha para se conectar ao computador, e o arquivo CCMSetup.log no cliente registra o processo de instalação.  

> [!IMPORTANT]  
>  Para que o push de cliente tenha êxito, verifique se todos os pré-requisitos estão em vigor. Eles estão listados na seção "Dependências do método de instalação" em [Pré-requisitos para a implantação de clientes em computadores com Windows no System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md).  

### <a name="to-configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Para configurar o site para usar automaticamente o push do cliente para computadores descobertos

1.  No console do Configuration Manager, escolha **Administração** > **Configuração de Site** > **Sites**.  

3.  Selecione o site para o qual deseja configurar a instalação automática do cliente por push em todo o site.  

4.  Na guia **Início**, no grupo **Configurações**, escolha **Configurações de Instalação de Cliente** > **Instalação do Cliente por Push**.  

5.  Na guia **Geral** da caixa de diálogo **Propriedades da Instalação do Cliente por Push**, selecione **Habilitar a instalação automática do cliente por push em todo o site**. Selecione os tipos de sistema para os quais o Configuration Manager deve enviar por push o software cliente.  

6.  Selecione se deseja instalar o cliente em controladores de domínio.  

7.  Na guia **Contas**, especifique uma ou mais contas para que o Configuration Manager use ao se conectar ao computador para instalar o software cliente. Clique no ícone **Criar**, insira o **Nome de usuário** e a **Senha** (com menos de 38 caracteres), confirme a senha e, em seguida, clique em **OK**. Você deve especificar pelo menos uma conta de instalação por push do cliente, que deve ter direitos de administrador local em cada computador no qual você deseja instalar o cliente. Se você não especificar uma conta de instalação do cliente por push, o Configuration Manager tentará usar a conta de computador do sistema de sites, o que causará uma falha do push do cliente entre domínios.  

    
    > [!NOTE]  
    >  Se você pretende usar o método de instalação do cliente por push de um site secundário, a conta deve ser especificada no site secundário que inicia o push do cliente.  
    >   
    >  Para obter mais informações sobre a conta de instalação do cliente por push, consulte o procedimento a seguir, "Para usar o Assistente de Instalação do Cliente por Push".  

8.  Completar a guia **Propriedades da Instalação**.

     As [propriedades da instalação do cliente](../../../core/clients/deploy/about-client-installation-properties.md) especificadas nesta guia serão publicadas no Active Directory Domain Services se o esquema for estendido para o Configuration Manager e lido pelas instalações do cliente nas quais o CCMSetup é executado sem propriedades de instalação.  

    > [!NOTE]  
    >  Se você habilitar a instalação do cliente por push em um site secundário, verifique se a propriedade SMSSITECODE está definida como o nome do site do Configuration Manager de seu site primário pai. Se o esquema do Active Directory estiver estendido para o Configuration Manager, você também poderá definir como AUTO para localizar automaticamente a atribuição do site correto.  

### <a name="to-use-the-client-push-installation-wizard"></a>Para usar o Assistente de Instalação do Cliente por Push

1.  No console do Configuration Manager, escolha **Administração** >  **Configuração de Site** > **Sites**.  

3.  Selecione o site para o qual deseja configurar a instalação automática do cliente por push em todo o site.  

4.  Na guia **Início** > grupo **Configurações**, escolha **Configurações de Instalação de Cliente** > **Instalação do Cliente por Push**.  

5.  Completar a guia **Propriedades da Instalação**.  

     As [propriedades da instalação do cliente](../../../core/clients/deploy/about-client-installation-properties.md) especificadas nesta guia serão publicadas no Active Directory Domain Services se o esquema for estendido para o Configuration Manager e lido pelas instalações do cliente nas quais o CCMSetup é executado sem propriedades de instalação.  

6.  No console do Configuration Manager, escolha **Ativos e Conformidade**.  

7.  No espaço de trabalho **Ativos e Conformidade** , selecione um ou mais computadores ou uma coleção de computadores.  

8.  Na guia **Início** , escolha um dos seguintes:  

    -   Se desejar instalar o cliente em um único computador ou em vários computadores, no grupo **Dispositivo**, escolha **Instalar Cliente**.  

    -   Se desejar instalar o cliente em uma coleção de computadores, no grupo **Coleção**, escolha **Instalar Cliente**.  

9. Na página **Antes de Começar** do **Assistente de Instalação do Cliente**, examine as informações e, em seguida, escolha **Avançar**.  

10. Completar a página **Opções de instalação**.  

11. Revise as configurações de instalação e feche o assistente.  

> [!NOTE]  
>  Você pode usar o assistente para instalar clientes mesmo se o site não está configurado para push do cliente.  

##  <a name="a-namebkmkclientsupa-how-to-install-clients-with-software-update-based-installation"></a><a name="BKMK_ClientSUP"></a> Como instalar clientes com a instalação baseada em atualização de software  
 A instalação do cliente baseada em atualização de software publica o cliente em um ponto de atualização de software como uma atualização de software. Use esse método para uma primeira instalação ou uma atualização.  

 Se um computador tiver o cliente instalado, o Configuration Manager fornecerá o cliente com a política de cliente, que inclui o nome do servidor do ponto de atualização de software e a porta da qual obter atualizações de software.   

> [!IMPORTANT]  
>  Para usar a instalação baseada em atualização de software, você deve usar o mesmo servidor WSUS (Windows Server Update Services) para instalação do cliente e atualizações de software. Esse servidor deve ser o ponto de atualização de software ativo em um site primário. Para mais informações, confira [Install a software update point](../../../sum/get-started/install-a-software-update-point.md) (Instalar um ponto de atualização de software).  

Se um computador não tiver o cliente do Configuration Manager instalado, você deverá configurar e atribuir um GPO (Objeto de Política de Grupo) no Active Directory Domain Services para especificar o nome do servidor do ponto de atualização de software.  

Você não pode adicionar propriedades de linha de comando a uma instalação do cliente baseada em atualização de software. Se você tiver o esquema do Active Directory estendido para o Configuration Manager, os computadores cliente consultarão automaticamente o Active Directory Domain Services quanto a propriedades de instalação quando forem instaladas.  

Se você não tiver o esquema do Active Directory estendido, poderá usar a política de grupos para provisionar as configurações de instalação do cliente em computadores no site. Essas configurações são aplicadas automaticamente nas instalações do cliente baseadas em atualização de software. Para obter mais informações, consulte [Como provisionar propriedades de instalação de cliente (política de grupo e instalação de cliente com base na atualização do software)](#BKMK_Provision) e [Como atribuir clientes a um site no System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

Use os procedimentos a seguir para configurar computadores sem um cliente do Configuration Manager para usarem o ponto de atualização de software para instalação do cliente e atualizações de software e para publicar o software cliente no ponto de atualização de software.  

> [!NOTE]  
>  Se os computadores estiverem em um estado de reinicialização pendente após uma instalação anterior do software, uma instalação de cliente de atualização com base em software pode causar a reinicialização do computador.  

### <a name="configure-a-group-policy-object-in-active-directory-domain-services-to-specify-the-software-update-point-for-client-installation-and-software-updates"></a>Configure um Objeto de Política de Grupo no Active Directory Domain Services para especificar o ponto de atualização de software para instalação do cliente e atualizações de software:  

1.  Use o Console de Gerenciamento de Política de Grupo para abrir um Objeto de Política de Grupo novo ou existente.  

2.  No console, expanda **Configuração do Computador**, expanda **Modelos Administrativos**, expanda **Componentes do Windows** e escolha **Windows Update**.  

3.  Abra as propriedades da configuração **Especificar o local do serviço do Microsoft Update na intranet** e escolha **Habilitado**.  

4.  Na caixa **Configurar o serviço de atualização da intranet para detectar atualizações**, especifique o nome e a porta do servidor do ponto de atualização de software:  

    -   Se o sistema de sites do Configuration Manager estiver configurado para usar um FQDN (nome de domínio totalmente qualificado), use o formato FQDN.  

    -   Se o sistema de sites do Configuration Manager não está configurado para usar um FQDN, use um formato de nome curto.  

    > [!NOTE]  
    >  Para determinar o número da porta, consulte [Como determinar as configurações de porta usadas pelo WSUS no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

     Exemplo: **http://server1.contoso.com:8530**  

5.  Na caixa **Configurar o servidor de estatísticas da intranet**, especifique o nome do servidor de estatísticas da intranet. Ele não precisa ser o mesmo que o servidor do ponto de atualização de software e o formato não precisa corresponder se ele for o mesmo servidor.  

6.  Atribua o Objeto de Política de Grupo aos computadores nos quais você deseja instalar o cliente e receber atualizações de software.  

### <a name="to-publish-the-configuration-manager-client-to-the-software-update-point"></a>Para publicar o cliente do Configuration Manager no ponto de atualização de software  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração do Site** > **Sites**.  

3.  Selecione o site para o qual deseja configurar a instalação do cliente baseada em atualização de software.  

4.  Na guia **Início**, no grupo **Configurações**, escolha **Configurações de Instalação de Cliente** e, em seguida, escolha **Instalação do Cliente com Base na Atualização de Software**.  

5.  Selecione **Habilitar instalação do cliente baseada na atualização de software**.  

6.  Se o software cliente no servidor do site do Configuration Manager for uma versão mais recente do que a que está no ponto de atualização de software, a caixa de diálogo **Versão Mais Recente do Pacote do Cliente Detectada** será aberta. Clique em **Sim** para publicar a versão mais recente.  

    > [!NOTE]  
    >  Se o software cliente não foi publicado anteriormente no ponto de atualização de software, essa caixa estará em branco.  

A atualização de software para o cliente do Configuration Manager não é atualizada automaticamente quando existe uma nova versão. Se você atualizar o site, o que inclui uma nova versão do cliente, deverá repetir este procedimento e clicar em **Sim** para ir para a etapa 6.  

##  <a name="a-namebkmkclientgpa-how-to-install-clients-with-group-policy"></a><a name="BKMK_ClientGP"></a> Como instalar clientes com política de grupo  
 Você pode usar a Política de Grupo no Active Directory Domain Services para publicar ou atribuir o cliente do Configuration Manager para instalação em computadores na empresa. O cliente será instalado quando o computador for iniciado. Quando você usa a Política de Grupo, o cliente é exibido no Painel de Controle **Adicionar ou Remover Programas** para que o usuário o instale.  

 Use o pacote do Windows Installer (CCMSetup.msi) para instalações baseadas na Política de Grupo. Esse arquivo é encontrado na pasta **&lt;diretório de instalação do ConfigMgr\>\bin\i386** no servidor do site do Configuration Manager. Você não pode adicionar propriedades a esse arquivo para modificar o comportamento de instalação.  

> [!IMPORTANT]  
>  Você deve ter permissões de administrador para acessar os arquivos de instalação do cliente.  

-   Se o esquema do Active Directory estiver estendido para o Configuration Manager e **Publicar este site no Active Directory Domain Services** estiver selecionado na guia **Avançado** da caixa de diálogo **Propriedades do Site**, os computadores cliente pesquisarão automaticamente as propriedades de instalação do Active Directory Domain Services. Para obter mais informações sobre as propriedades de instalação publicadas, consulte [Sobre as propriedades de instalação de cliente publicadas nos Serviços de Domínio do Active Directory no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

-   Se o esquema do Active Directory não foi estendido, você poderá usar o procedimento neste tópico para armazenar as propriedades de instalação no Registro de computadores: [Como provisionar propriedades de instalação de cliente (Política de Grupo e Instalação de cliente com base na atualização do software)](#BKMK_Provision). Essas propriedades de instalação serão usadas quando o cliente for instalado.  

Para obter informações sobre como usar a Política de Grupo nos Serviços de Domínio Active Directory para instalar o software, consulte a documentação do Windows Server.  

##  <a name="a-namebkmkmanuala-how-to-install-clients-manually"></a><a name="BKMK_Manual"></a> Como instalar clientes manualmente  
 Você pode instalar manualmente o software cliente em computadores na sua empresa usando o programa CCMSetup.exe. Esse programa e seus arquivos de suporte podem ser encontrados na pasta **Cliente** da pasta de instalação do Configuration Manager no servidor do site e nos pontos de gerenciamento no seu site. Esta pasta é compartilhada na rede como  

 \\\\*&lt;Nome do servidor do site\>*\SMS_*&lt;Código do site\>*\Client\  

 em que *&lt;Nome do servidor do site\>* é o nome de um dos servidores que hospeda um ponto de gerenciamento e *&lt;Código do site\>* é o código do site primário ao qual o cliente pertencerá.  Para executar CCMSetup.exe da linha de comando no cliente, é preciso mapear uma unidade de rede para esse local e executar o comando.  

> [!IMPORTANT]  
>  Você deve ter permissões de administrador para acessar os arquivos de instalação do cliente.  

 O CCMSetup.exe copia todos os pré-requisitos necessários para o computador cliente e chama o pacote do Windows Installer (Client.msi) para instalar o cliente. Não é possível executar o Client.msi diretamente.  

 Você pode especificar propriedades da linha de comando para o CCMSetup.exe e o Client.msi para modificar o comportamento da instalação do cliente. Verifique se você especificou as propriedades de CCMSetup (as propriedades que começam com **/**) antes de especificar as propriedades de Client.msi. Por exemplo:  

```  
CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01  
```  
e o cliente é instalado usando as seguintes propriedades:  

|Propriedade|Descrição|  
|--------------|-----------------|  
|**/mp:SMSMP01**|Esta propriedade de CCMSetup especifica o ponto de gerenciamento SMSMP01 para baixar os arquivos de instalação necessários do cliente.|  
|**/logon**|Esta propriedade de CCMSetup especifica que a instalação deverá parar se um cliente do Configuration Manager for encontrado no computador.|  
|**SMSSITECODE=AUTO**|Esta propriedade de Client.msi especifica que o cliente tenta localizar o código do site do Configuration Manager a ser usado, por exemplo, usando o Active Directory Domain Services.|  
|**FSP=SMSFP01**|Esta propriedade de Client.msi especifica que o ponto de status de fallback chamado SMSFP01 será usado para receber mensagens de estado enviadas do computador cliente.|  

 Para ver detalhes sobre todas as propriedades de CCMSetup.exe, consulte [Sobre as propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md)  

### <a name="examples"></a>Exemplos
 Estes exemplos são para clientes do Active Directory na intranet e usam os seguintes valores para representar aspectos diferentes do site:  

 **MPSERVER** = servidor que hospeda o ponto de gerenciamento   
**FSPSERVER** = servidor que hospeda o ponto de status de fallback  
**ABC** = código do site  
**contoso.com** = nome de domínio  

 Todos os servidores do sistema de sites são configurados com um FQDN de intranet e o site é publicado na floresta do Active Directory do cliente.  

 No computador cliente, faça logon como um administrador local, mapeie uma unidade (z:) para \\\MPSERVER\SMS_ABC\Client, mude o prompt de comando para a unidade z e, em seguida, execute um dos comandos a seguir.  

 **Exemplo 1:**  

```  
CCMSetup.exe  
```  
Este exemplo instala o cliente sem propriedades adicionais para que ele seja configurado automaticamente com as propriedades de instalação do cliente publicadas no Active Directory Domain Services. Por exemplo, o cliente é configurado automaticamente para o código do site (exige que o local de rede do cliente seja incluído em um grupo de limites configurado para atribuição do cliente), ponto de gerenciamento, o ponto de status de fallback e se o cliente deve se comunicar usando somente HTTPS. Para obter mais informações sobre as propriedades de instalação do cliente que podem ser configuradas automaticamente para clientes do Active Directory, consulte [Sobre as propriedades de instalação de cliente publicadas nos Serviços de Domínio do Active Directory no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

 **Exemplo 2:**  

```  
CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com  
```  
Este exemplo substitui a configuração automática que o Active Directory Domain Services pode fornecer e não exige que o local de rede do cliente esteja incluído em um grupo de limites configurado para atribuição do cliente. Em vez disso, a instalação especifica o site, um ponto de gerenciamento da intranet e um ponto de gerenciamento baseado na Internet, um ponto de status de fallback que aceita conexões da Internet e usa um certificado PKI do cliente (se disponível) com o período de validade mais longo.  

##  <a name="a-namebkmkclientlogonscripta-how-to-install-clients-with-logon-scripts"></a><a name="BKMK_ClientLogonScript"></a> Como instalar clientes com scripts de logon  
 O Configuration Manager dá suporte a scripts de logon para instalar o software cliente do Configuration Manager. Você pode usar o arquivo de programa **CCMSetup.exe** em um script de logon para disparar a instalação do cliente.  

 A instalação de script de logon usa os mesmos métodos da instalação manual do cliente. Você pode especificar a propriedade de instalação **/logon** para CCMSsetup.exe, que evita que o cliente seja instalado se alguma versão do cliente já existir no computador. Isso impede que a reinstalação do cliente ocorra toda vez que o script de logon é executado.  

 Se não for especificada nenhuma fonte de instalação que esteja usando a propriedade **/Source** e nenhum ponto de gerenciamento do qual obter a instalação for especificado usando a propriedade **/MP**, CCMSetup.exe poderá localizar o ponto de gerenciamento pesquisando os Serviços de Domínio do Active Directory se o esquema tiver sido estendido para o Configuration Manager e o site estiver publicado no Active Directory Domain Services. Como alternativa, o cliente pode usar DNS ou WINS para localizar um ponto de gerenciamento.  

##  <a name="a-namebkmkclientappa-how-to-install-clients-with-a-package-and-program"></a><a name="BKMK_ClientApp"></a> Como instalar clientes com um pacote e programa  
 Você pode usar o Configuration Manager para criar e implantar um pacote e um programa que atualiza o software cliente para computadores selecionados na hierarquia. Um arquivo de definição de pacote que preenche as propriedades do pacote com valores geralmente usados é fornecido com o Configuration Manager. Você pode personalizar o comportamento da instalação do cliente especificando propriedades de linha de comando adicionais.  

> [!NOTE]  
>  Não é possível atualizar clientes do Configuration Manager 2007 usando esse método. Em vez disso, use a atualização automática de cliente, que cria e implanta automaticamente um pacote com a versão mais recente do cliente. Para obter mais informações, consulte [Atualizar clientes no System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md).  
>   
>  Para obter mais informações sobre como migrar de versões mais antigas do Configuration Manager, confira [Planning a client migration strategy in System Center Configuration Manager](../../../core/migration/planning-a-client-migration-strategy.md) (Planejando uma estratégia de migração de cliente no System Center Configuration Manager).  

 
###<a name="to-create-a-package-and-program-for-the-client-software"></a>Para criar um pacote e um programa para o software do cliente  

Use o procedimento a seguir para criar um pacote e um programa do Configuration Manager que você possa implantar nos computadores cliente do Configuration Manager para atualizar o software cliente.  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Pacotes**.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Pacote com base na Definição**.  

4.  Na página **Definição do Pacote** do assistente, selecione **Microsoft** na lista suspensa **Editor** e selecione **Atualização de Cliente do Configuration Manager** na lista **Definição do pacote**.  

5.  Na página **Arquivos de Origem**, selecione **Sempre obter arquivos da pasta de origem**.  

6.  Na página **Pasta de Origem**, selecione **Caminho de rede (nome UNC)** e insira o caminho de rede para o computador e a pasta que contém os arquivos de instalação do cliente.  

    > [!NOTE]  
    >  O computador no qual a implantação do Configuration Manager é executada deve ter acesso à pasta de rede que você especificar, caso contrário, a instalação falhará.  

    Se desejar alterar alguma das propriedades de instalação do cliente, você poderá modificar os parâmetros de linha de comando CCMSetup.exe na guia **Geral** da caixa de diálogo do programa **Propriedades de atualização silenciosa de agente do Configuration Manager** . As propriedades de instalação padrão são **/noservice SMSSITECODE=AUTO**.  

9. Distribua o pacote para todos os pontos de distribuição em que você deseja hospedar o pacote de atualização do cliente. Em seguida, você pode implantar o pacote nas coleções de computador que contêm clientes que você deseja atualizar.  

## <a name="how-to-install-clients-to-intune-mdm-managed-windows-devices"></a>Como instalar clientes em dispositivos do Windows gerenciados por MDM

Você pode implantar os arquivos de instalação do cliente em computadores que são registrados com o Microsoft Intune. 

Para garantir que o dispositivo permaneça em um estado gerenciado depois da instalação do software cliente, o dispositivo deverá estar na rede corporativa e dentro de um limite de site do Configuration Manager. 

> [!NOTE]
> Depois que o software cliente for instalado, o dispositivo terá o registro no Intune cancelado.

### <a name="to-install-clients-with-intune"></a>Para instalar clientes com o Intune:

1. No Intune, [crie um aplicativo](/intune/deploy-use/add-apps-for-mobile-devices-in-microsoft-intune) que contém o arquivo de instalação de cliente do Configuration Manager **ccmsetup.msi**.

2. No Intune Software Publisher, use os seguintes parâmetros de linha de comando:

  **CCMSETUPCMD="/MP:&lt;FQDN do ponto de gerenciamento> SMSMP=&lt;FQDN do ponto de gerenciamento> SMSSITECODE=&lt;Código do site> DNSSUFFIX=&lt;Sufixo DNS do ponto de gerenciamento>"**

3. [Implante o aplicativo](/intune/deploy-use/deploy-apps-in-microsoft-intune) nos computadores Windows registrados.

##  <a name="a-namebkmkclientimagea-how-to-install-clients-with-a-computer-image"></a><a name="BKMK_ClientImage"></a> Como instalar clientes com uma imagem do computador  
É possível pré-instalar o software cliente do Configuration Manager em um computador de imagem mestra que será usado para criar uma imagem de outros computadores.   

### <a name="to-prepare-the-client-computer-for-imaging"></a>Para preparar o computador cliente para geração de imagens  

1.  Instale manualmente o software cliente do Configuration Manager no computador com a imagem mestra. Para obter mais informações, consulte [Como instalar manualmente os clientes do Configuration Manager](#BKMK_Manual).  

    > [!IMPORTANT]  
    >  Não especifique um código do site do Configuration Manager para o cliente nas propriedades da linha de comando CCMSetup.exe.  

2.  No prompt de comando, digite **net stop ccmexec** para garantir que o serviço **Host de Agente do SMS** (Ccmexec.exe) não esteja sendo executado no computador com a imagem mestra.  

3.  Remova todos os certificados armazenados no armazenamento de computador local no computador com a imagem mestra.  Por exemplo, se você usar certificados PKI (infraestrutura de chave pública), deverá remover os certificados na loja **Pessoal** para **Computador** e **Usuário** antes de criar a imagem no computador.

4.  Se os clientes forem instalados em uma hierarquia do Configuration Manager diferente em vez do computador com a imagem mestra, remova a chave de raiz confiável do computador com a imagem mestra.  
    > [!NOTE]  
    >  Se os clientes não conseguirem consultar os Serviços de Domínio do Active Directory para localizar um ponto de gerenciamento, eles usarão a chave de raiz confiável para determinar pontos de gerenciamento confiáveis. Se todos os clientes com imagens forem implantados na mesma hierarquia co computador mestre, deixe a chave de raiz confiável no lugar. Se os clientes forem implantados em hierarquia diferentes, remova a chave de raiz confiável e, como prática recomendada, provisione esses clientes com a nova chave de raiz confiável. Para obter mais informações, consulte  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK). 

5.  Use o software de geração de imagens para capturar a imagem do computador mestre.  

6.  Implante a imagem nos computadores de destino.  

##  <a name="a-namebkmkclientworkgroupa-how-to-install-clients-on-workgroup-computers"></a><a name="BKMK_ClientWorkgroup"></a> Como instalar clientes em computadores do grupo de trabalho  
 O Configuration Manager dá suporte à instalação do cliente para computadores do grupos de trabalho. Instale o cliente em computadores do grupo de trabalho usando o método especificado em [Como instalar manualmente os clientes do Configuration Manager](#BKMK_Manual).  

 Pré-requisitos:  

-   O cliente deve ser instalado manualmente em cada computador do grupo de trabalho. Durante a instalação, o usuário conectado deve ter direitos de administrador local.  

-   Para acessar recursos no domínio de servidor do site do Configuration Manager, a conta de acesso à rede deve ser configurada para o site. Especifique essa conta como uma propriedade do componente de distribuição de software. Para obter mais informações, consulte [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

 Limitações:  

-   Os clientes do grupo de trabalho não podem localizar pontos de gerenciamento dos Serviços de Domínio do Active Directory. Em vez disso, devem usar DNS, WINS ou outro ponto de gerenciamento.  

-   Não há suporte para roaming global, pois os clientes não podem consultar os Serviços de Domínio do Active Directory para obter informações do site.  

-   Os métodos de descoberta do Active Directory não podem descobrir computadores do grupos de trabalho.  

-   Não é possível implantar o software para os usuários de computadores do grupo de trabalho.  

-   Você não pode usar o método de instalação do cliente por push para instalar o cliente em computadores do grupo de trabalho.  

-   Clientes do grupo de trabalho não podem usar o Kerberos para autenticação e podem exigir aprovação manual.  

-   Um cliente de grupo de trabalho não pode ser configurado como um ponto de distribuição. O Configuration Manager exige que os computadores do ponto de distribuição sejam membros de um domínio.  

### <a name="to-install-the-client-on-workgroup-computers"></a>Para instalar o cliente em computadores do grupo de trabalho  

Verifique os pré-requisitos e, em seguida, siga as instruções na seção [Como instalar manualmente os clientes do Configuration Manager](#BKMK_Manual).  

   Este exemplo instala o cliente para gerenciamento de clientes de intranet e especifica o código do site e o sufixo DNS para localizar um ponto de gerenciamento: `**CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com**`  

     

   Este exemplo requer que o cliente esteja em um local de rede configurado em um grupo de limite para que a atribuição automática do site tenha êxito. O comando inclui um ponto de status de fallback no servidor FSPSERVER, para ajudar a controlar a implantação do cliente e identificar quaisquer problemas de comunicação do cliente: `**CCMSetup.exe FSP=fspserver.constoso.com**`  

      

##  <a name="a-namebkmkclientinterneta-how-to-install-clients-for-internet-based-client-management"></a><a name="BKMK_ClientInternet"></a> Como instalar clientes para o gerenciamento de clientes baseados na Internet  
 Quando o site do Configuration Manager dá suporte ao gerenciamento de clientes baseado na Internet para clientes que às vezes estão na intranet e às vezes estão na Internet, você tem duas opções ao instalar clientes na intranet:  

-   Você pode incluir a propriedade de Client.msi de CCMHOSTNAME=*&lt;FQDN da Internet do ponto de gerenciamento baseado na Internet\>* ao instalar o cliente, por exemplo, usando a instalação manual ou por push do cliente. Ao usar esse método, você também deve atribuir diretamente o cliente ao site e não pode usar a atribuição automática do site. A seção [Como instalar manualmente os clientes do Configuration Manager](#BKMK_Manual) neste tópico fornece um exemplo desse método de configuração.  

-   Você pode instalar o cliente para gerenciamento de clientes de intranet e atribuir ao cliente um ponto de gerenciamento de clientes baseados na Internet usando as propriedades do cliente do Configuration Manager no Painel de Controle ou usando um script. Ao usar esse método, você pode usar a atribuição automática de clientes. Para obter mais informações, consulte a seção [Como configurar clientes para gerenciamento de clientes baseados na Internet após a instalação do cliente](#BKMK_ConfigureIBCM_MP) neste tópico.  

 Se tiver de instalar clientes que estão na Internet porque são clientes apenas da Internet ou porque você deve instalá-los antes de eles voltarem à intranet, escolha um dos seguintes métodos com suporte:  

-   Forneça um mecanismo para que esses clientes se conectem temporariamente à intranet com uma VPN (rede virtual privada) e instale-os usando algum método adequado de instalação do cliente.  

-   Use um método de instalação independente do Configuration Manager, como empacotamento dos arquivos de origem de instalação do cliente na mídia removível que você pode enviar para que os usuários instalem com as instruções. Os arquivos de origem de instalação do cliente estão localizados na pasta *&lt;InstallationPath\>*\Client no servidor do site do Configuration Manager e nos pontos de gerenciamento. Inclua na mídia um script para copiar manualmente na pasta do cliente e dessa pasta, instale o cliente usando o CCMSetup.exe e todas as propriedades da linha de comando CCMSetup apropriada.  

> [!NOTE]  
>  O Configuration Manager não dá suporte para a instalação um cliente diretamente do ponto de gerenciamento baseado na Internet ou do ponto de atualização do software baseado na Internet.  

 Como os clientes gerenciados pela Internet precisam se comunicar com sistemas do site baseado na Internet, verifique se esses clientes também têm certificados PKI instalados antes de você instalá-los. Você deve instalar esses certificados independentemente do Configuration Manager. Para obter mais informações sobre os requisitos de certificado, consulte [Requisitos de certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

### <a name="to-install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Para instalar clientes na Internet especificando propriedades da linha de comando CCMSetup  

1.  Siga as instruções na seção [Como instalar manualmente os clientes do Configuration Manager](#BKMK_Manual) e sempre inclua o seguinte:  

    -   Propriedade de linha de comando do CCMSetup **/source:***&lt;caminho local para a pasta copiada Cliente\>*  

    -   Propriedade da linha de comando CCMSetup **/UsePKICert**  

    -   Propriedade Client.msi **CCMHOSTNAME=***&lt;FQDN do ponto de gerenciamento baseado na Internet\>*  

    -   Propriedade Client.msi **SMSSIGNCERT=***&lt;caminho local para o certificado de assinatura do servidor do site exportado\>*  

    -   Propriedade Client.msi **SMSSITECODE=***&lt;código do site de ponto de gerenciamento baseado na Internet\>*  

    > [!NOTE]  
    >  Se o site tiver mais de um ponto de gerenciamento baseado na Internet, não importa qual ponto de gerenciamento baseado na Internet você especifica para a propriedade CCMHOSTNAME. Quando um cliente do Configuration Manager se conecta ao ponto de gerenciamento baseado na Internet especificado, o ponto de gerenciamento envia ao cliente uma lista de pontos de gerenciamento disponíveis baseados na Internet no site e o cliente seleciona aleatoriamente um da lista.  

2.  Se você não quiser que o cliente verifique a CRL (lista de revogação de certificados), especifique a propriedade da linha de comando CCMSetup **/NoCRLCheck**.  

3.  Se estiver usando um ponto de status de fallback baseado na Internet, especifique a propriedade Client.msi **FSP=***&lt;FQDN da Internet do ponto de status de fallback baseado na Internet\>*.  

4.  Se estiver instalando o cliente para o gerenciamento de clientes apenas da Internet, especifique a propriedade Client.msi **CCMALWAYSINF=1**.  

5.  Verifique se você precisa especificar propriedades adicionais da linha de comando CCMSetup. Por exemplo, talvez você precise especificar um critério de seleção de certificados se o cliente tiver mais de um certificado PKI válido. Para obter uma lista das propriedades disponíveis, consulte [Sobre as propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

   Exemplo: `**CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1**`  

   Este exemplo instala os arquivos de origem do cliente de uma pasta na unidade D com configurações para usar um certificado PKI do cliente e selecionar o certificado com o período de validade mais longo para gerenciamento de clientes apenas da Internet, atribui o cliente para usar o ponto de gerenciamento baseado na Internet chamado SERVER1 e o ponto de status de fallback no domínio contoso.com, e atribui o cliente ao site ABC.  

###  <a name="a-namebkmkconfigureibcmmpato-configure-clients-for-internet-based-client-management-after-client-installation"></a><a name="BKMK_ConfigureIBCM_MP"></a>Para configurar clientes para o gerenciamento de clientes baseados na Internet após a instalação do cliente  
 Para atribuir o ponto de gerenciamento baseado na Internet após a instalação do cliente, use um dos procedimentos a seguir. O primeiro requer configuração manual e é apropriado para poucos clientes. O segundo é mais apropriado para a configuração de muitos clientes.  

#### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation-by-assigning-the-internet-based-management-point-in-configuration-manager-properties"></a>Para configurar clientes para gerenciamento de clientes baseado na Internet após a instalação do cliente atribuindo o ponto de gerenciamento baseado na Internet nas Propriedades do Configuration Manager  

1.  Navegue até **Configuration Manager** no Painel de Controle do computador cliente e clique duas vezes para abrir suas propriedades.  

2.  Na guia **Internet** , insira o nome do domínio totalmente qualificado do ponto de gerenciamento baseado na Internet na caixa de texto FQDN de Internet.  

    > [!NOTE]  
    >  A guia **Internet** só ficará disponível se o cliente tiver um certificado PKI do cliente.  

3.  Insira as configurações do servidor proxy se o cliente for acessar a Internet usando um servidor proxy.  

#### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Para configurar clientes para gerenciamento de clientes baseados na Internet após a instalação do cliente usando um script  

1.  Abra um editor de texto, como o Bloco de Notas.  

2.  Copie e insira o seguinte no arquivo. Substituir *mp.contoso.com* pelo FQDN de Internet do seu ponto de gerenciamento baseado na Internet.  

    ```  
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the Internet-Based Management Point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

    > [!NOTE]  
    >  Se precisar excluir um ponto de gerenciamento baseado na Internet especifico para que o cliente não seja configurado para usar um ponto de gerenciamento baseado na Internet, remova o valor dentro das aspas para que essa linha se torne **newInternetBasedManagementPointFQDN = ""**.  

4.  Salve o arquivo com uma extensão .vbs.  

5.  Use cscript para executar o script em computadores cliente, usando um dos seguintes métodos:  

    -   Implante o arquivo nos clientes existentes do Configuration Manager usando um pacote e um programa.  

    -   Execute o arquivo localmente em clientes existentes do Configuration Manager clicando duas vezes no arquivo de script do Windows Explorer.  

 Talvez você precise reiniciar o cliente para que as alterações entrem em vigor.  

##  <a name="a-namebkmkprovisiona-how-to-provision-client-installation-properties-group-policy-and-software-update-based-client-installation"></a><a name="BKMK_Provision"></a> Como provisionar propriedades de instalação de cliente (política de grupo e instalação do cliente baseada em atualização de software)  
 Você pode usar a Política de Grupo do Windows para provisionar computadores com as propriedades de instalação de cliente do Configuration Manager. Essas propriedades estão armazenadas no Registro do computador e são lidas quando o software cliente é instalado. Esse procedimento normalmente não é necessário, mas poderá ser necessário para alguns cenários de instalação de cliente, como:  

-   Você está usando as configurações da política de grupo ou métodos de instalação do cliente baseados na atualização do software e não estendeu o esquema do Active Directory para o Configuration Manager.  

-   Você deseja substituir as propriedades de instalação do cliente em computadores específicos.  

> [!NOTE]  
>  Se alguma das propriedade de instalação for fornecida na linha de comando CCMSetup.exe, as propriedades de instalação provisionadas em computadores não serão usadas.  

 Um modelo administrativo da política de grupo chamado ConfigMgrInstallation.adm é fornecido na mídia de instalação do Configuration Manager, que pode ser usado para provisionar computadores cliente com propriedades da instalação.   

### <a name="to-configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Para configurar e atribuir propriedades de instalação do cliente usando um objeto da política de grupo  

1.  Importar o modelo administrativo ConfigMgrInstallation.adm em um Objeto de Política de Grupo novo ou existente, usando um editor como Editor de Objeto de Política de Grupo do Windows. O arquivo pode ser localizado na pasta **TOOLS\ConfigMgrADMTemplates** na mídia de instalação do Configuration Manager.  

2.  Abra as propriedades da configuração importada **Definir configurações de implantação de cliente**.  

3.  Escolha **Habilitado**.  

4.  Na caixa **CCMSetup** , digite as propriedades de linha de comando CCMSetup necessárias. Para obter uma lista das propriedades de linha de comando de CCMSetup e exemplos de seu uso, consulte [Sobre as propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

5.  Atribuir o Objeto de Política de Grupo a computadores que você deseja provisionar com as propriedades de instalação do cliente do Configuration Manager.  

 Para obter informações sobre a Política de Grupo do Windows, consulte a documentação do Windows Server.  

### <a name="see-also"></a>Consulte também
[Métodos de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md)


<!--HONumber=Dec16_HO5-->


