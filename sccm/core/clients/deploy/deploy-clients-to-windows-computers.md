---
title: Implantar clientes no Windows
titleSuffix: Configuration Manager
description: Saiba como implantar o cliente do Configuration Manager em computadores Windows.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5efca393afe2fc6441d074f987549228e7d0418f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342368"
---
# <a name="how-to-deploy-clients-to-windows-computers-in-system-center-configuration-manager"></a>Como implantar clientes em computadores Windows no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de instalar os clientes do Configuration Manager, verifique se todos os [pré-requisitos](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) estão em vigor e se você concluiu todas as configurações de implantação necessárias.   



##  <a name="BKMK_ClientPush"></a> Como instalar clientes com push de cliente  

Configure a instalação do cliente por push para um site. A instalação do cliente é executada automaticamente nos computadores descobertos nos limites configurados do site quando esses limites são configurados como um grupo de limites. Ou, você pode iniciar uma instalação do cliente por push executando o Assistente de Instalação do Cliente por Push para uma coleção ou um recurso específico em uma coleção.  

Você também pode usar o Assistente de Instalação do Cliente por Push para instalar o cliente do Configuration Manager para resultados de [consulta](../../../core/servers/manage/queries-technical-reference.md). Para que a instalação tenha êxito, um dos itens retornados pela consulta deve ser o atributo **ResourceID** da classe de atributos **Recurso do Sistema**.   

Se o servidor do site não puder acessar o computador cliente nem iniciar o processo de instalação, ele repetirá automaticamente a instalação a cada hora. O servidor continua tentando novamente por até sete dias.  

Para ajudar a acompanhar o processo de instalação do cliente, instale um ponto de status de fallback antes de instalar os clientes. Quando um ponto de status de fallback é instalado, ele é atribuído automaticamente aos clientes quando eles são instalados pelo método de instalação do cliente por push. Para acompanhar o andamento da instalação do cliente, exiba os relatórios de atribuição e de implantação do cliente. 

Os arquivos de log do cliente fornecem informações mais detalhadas para solução de problemas. Os arquivos de log não exigem um ponto de status de fallback. Por exemplo, o arquivo **CCM.log** no servidor do site registra os problemas por meio do servidor do site durante a conexão com o computador. O arquivo **CCMSetup.log** no cliente registra o processo de instalação.  

> [!IMPORTANT]  
>  Para que o push de cliente tenha êxito, verifique se todos os pré-requisitos estão em vigor. Para obter mais informações, consulte [Dependências do método de instalação](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#installation-method-dependencies).  

### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Configurar o site para usar automaticamente o push do cliente para os computadores descobertos

1.  No console do Configuration Manager, escolha **Administração** > **Configuração de Site** > **Sites**.  

3.  Selecione o site para o qual deseja configurar a instalação automática do cliente por push em todo o site.  

4.  Na guia **Início**, no grupo **Configurações**, escolha **Configurações de Instalação de Cliente** > **Instalação do Cliente por Push**.  

5.  Na guia **Geral** da caixa de diálogo **Propriedades da Instalação do Cliente por Push**, selecione **Habilitar a instalação automática do cliente por push em todo o site**. Selecione os tipos de sistema para os quais o Configuration Manager deve enviar por push o software cliente.  

6.  Selecione se deseja instalar o cliente em controladores de domínio.  

7.  Na guia **Contas**, especifique uma ou mais contas para que o Configuration Manager use ao se conectar ao computador de destino. Clique no ícone **Criar**, insira o **Nome de usuário** e a **Senha** (com menos de 38 caracteres), confirme a senha e, em seguida, clique em **OK**. Especifique, pelo menos, uma conta de instalação do cliente por push. Essa conta deve ter direitos de Administrador local no computador de destino para instalar o cliente. Se você não especificar uma conta de instalação do cliente por push, o Configuration Manager tentará usar a conta de computador do sistema de sites. O push do cliente entre domínios falha ao usar a conta de computador do sistema de sites.  
    > [!NOTE]  
    >  Para usar o push do cliente em um site secundário, especifique a conta no site secundário que inicia o push do cliente.  
    >   
    >  Para obter mais informações sobre a conta de instalação do cliente por push, consulte o procedimento a seguir, [Usar o Assistente de Instalação do Cliente por Push](#use-the-client-push-installation-wizard).  

8.  Completar a guia **Propriedades da Instalação**.

     Se o esquema for estendido para o Configuration Manager, o site publicará no Active Directory Domain Services as [propriedades de instalação de Cliente](../../../core/clients/deploy/about-client-installation-properties.md) especificadas nesta guia. Essas configurações são lidas pelas instalações de cliente nas quais o CCMSetup é executado sem propriedades de instalação.  

    > [!NOTE]  
    >  Se você habilitar a instalação do cliente por push em um site secundário, verifique se a propriedade **SMSSITECODE** está definida com o nome do site do Configuration Manager de seu site primário pai. Se o esquema do Active Directory for estendido para o Configuration Manager, você também poderá definir essa propriedade como AUTO para encontrar automaticamente a atribuição de site correta.  

### <a name="use-the-client-push-installation-wizard"></a>Usar o Assistente de Instalação do Cliente por Push

1.  No console do Configuration Manager, escolha **Administração** >  **Configuração de Site** > **Sites**.  

3.  Selecione o site para o qual deseja configurar a instalação automática do cliente por push em todo o site.  

4.  Na guia **Início** > grupo **Configurações**, escolha **Configurações de Instalação de Cliente** > **Instalação do Cliente por Push**.  

5.  Completar a guia **Propriedades da Instalação**.  

     Se o esquema for estendido para o Configuration Manager, o site publicará no Active Directory Domain Services as [propriedades de instalação de Cliente](../../../core/clients/deploy/about-client-installation-properties.md) especificadas nesta guia. Essas configurações são lidas pelas instalações de cliente nas quais o CCMSetup é executado sem propriedades de instalação.   

6.  No console do Configuration Manager, escolha **Ativos e Conformidade**.  

7.  No espaço de trabalho **Ativos e Conformidade** , selecione um ou mais computadores ou uma coleção de computadores.  

8.  Na guia **Página Inicial**, escolha uma das seguintes opções:  

    -   Se desejar instalar o cliente em um único computador ou em vários computadores, no grupo **Dispositivo**, escolha **Instalar Cliente**.  

    -   Se desejar instalar o cliente em uma coleção de computadores, no grupo **Coleção**, escolha **Instalar Cliente**.  

9. Na página **Antes de Começar** do **Assistente de Instalação do Cliente**, examine as informações e, em seguida, escolha **Avançar**.  

10. Completar a página **Opções de instalação**.  

11. Revise as configurações de instalação e feche o assistente.  

> [!NOTE]  
>  Use o assistente para instalar clientes, mesmo se o site não estiver configurado para o push do cliente.  



##  <a name="BKMK_ClientSUP"></a> Como instalar clientes com a instalação baseada em atualização de software  
 A instalação do cliente baseada em atualização de software publica o cliente em um ponto de atualização de software como uma atualização de software. Use esse método para uma primeira instalação ou uma atualização.  

 Se um computador tiver o cliente do Configuration Manager instalado, ele receberá a política do cliente do site. Essa política inclui o nome do servidor de ponto de atualização de software e a porta da qual obter atualizações de software.   

> [!IMPORTANT]  
>  Para usar a instalação baseada em atualização de software, você deve usar o mesmo servidor WSUS (Windows Server Update Services) para instalação do cliente e atualizações de software. Esse servidor deve ser o ponto de atualização de software ativo em um site primário. Para mais informações, confira [Install a software update point](../../../sum/get-started/install-a-software-update-point.md) (Instalar um ponto de atualização de software).  

Se um computador não tiver o cliente do Configuration Manager instalado, configure e atribua um objeto de política de grupo no Active Directory Domain Services para especificar o nome do servidor do ponto de atualização de software.  

Não é possível adicionar propriedades de linha de comando a uma instalação do cliente baseada em atualização de software. Se você estender o esquema do Active Directory para o Configuration Manager, os computadores cliente consultarão automaticamente o Active Directory Domain Services para obter as propriedades de instalação quando elas forem instaladas.  

Se você não estender o esquema do Active Directory, use a política de grupo para provisionar as configurações de instalação do cliente em computadores no site. Essas configurações são aplicadas automaticamente nas instalações do cliente baseadas em atualização de software. Para obter mais informações, consulte [Como provisionar as propriedades de instalação do cliente (política de grupo e instalação do cliente baseada em atualização de software)](#BKMK_Provision) e [Como atribuir clientes a um site](../../../core/clients/deploy/assign-clients-to-a-site.md).  

Use os procedimentos a seguir para configurar computadores sem um cliente do Configuration Manager para usarem o ponto de atualização de software para instalação do cliente e atualizações de software e para publicar o software cliente no ponto de atualização de software.  

> [!NOTE]  
>  Se os computadores estiverem em um estado de reinicialização pendente após uma instalação anterior do software, uma instalação de cliente de atualização com base em software pode causar a reinicialização do computador.  

### <a name="configure-a-group-policy-object-in-active-directory-domain-services-to-specify-the-software-update-point-for-client-installation-and-software-updates"></a>Configure um objeto de política de grupo no Active Directory Domain Services para especificar o ponto de atualização de software para a instalação do cliente e as atualizações de software:  

1.  Use o Console de Gerenciamento de Política de Grupo para abrir um objeto de política de grupo novo ou existente.  

2.  No console, expanda **Configuração do Computador**, expanda **Modelos Administrativos**, expanda **Componentes do Windows** e escolha **Windows Update**.  

3.  Abra as propriedades da configuração **Especificar o local do serviço do Microsoft Update na intranet** e escolha **Habilitado**.  

4.  Na caixa **Configurar o serviço de atualização da intranet para detectar atualizações**, especifique o nome e a porta do servidor do ponto de atualização de software:  

    -   Se o sistema de sites do Configuration Manager estiver configurado para usar um FQDN (nome de domínio totalmente qualificado), use o formato FQDN.  

    -   Se o sistema de sites do Configuration Manager não estiver configurado para usar um FQDN, use um formato de nome curto.  

    > [!NOTE]  
    >  Para determinar o número da porta, consulte [Como determinar as configurações de porta usadas pelo WSUS](../../../sum/plan-design/plan-for-software-updates.md).  

     Exemplo: **http://server1.contoso.com:8530**  

5.  Na caixa **Configurar o servidor de estatísticas da intranet**, especifique o nome do servidor de estatísticas da intranet. Ele não precisa ser o mesmo do servidor de ponto de atualização de software. Se ele for o mesmo servidor, o formato não precisará ter uma correspondência.  

6.  Atribua o objeto de política de grupo aos computadores nos quais deseja instalar o cliente e receber atualizações de software.  

### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>Publicar o cliente do Configuration Manager no ponto de atualização de software  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração do Site** > **Sites**.  

3.  Selecione o site para o qual deseja configurar a instalação do cliente baseada em atualização de software.  

4.  Na guia **Início**, no grupo **Configurações**, escolha **Configurações de Instalação de Cliente** e, em seguida, escolha **Instalação do Cliente com Base na Atualização de Software**.  

5.  Selecione **Habilitar instalação do cliente baseada na atualização de software**.  

6.  Se o software cliente no servidor do site do Configuration Manager tiver uma versão mais recente do que a versão localizada no ponto de atualização de software, a caixa de diálogo **Versão Mais Recente do Pacote do Cliente Detectada** será aberta. Clique em **Sim** para publicar a versão mais recente.  

    > [!NOTE]  
    >  Se o software cliente não foi publicado anteriormente no ponto de atualização de software, essa caixa é exibida em branco.  

A atualização de software para o cliente do Configuration Manager não é atualizada automaticamente quando há uma nova versão. Se você atualizar o site, o que inclui uma nova versão do cliente, repita esse procedimento e clique em **Sim** para ir para a etapa 6.  



##  <a name="BKMK_ClientGP"></a> Como instalar clientes com política de grupo  
 Use a política de grupo no Active Directory Domain Services para publicar ou atribuir o cliente do Configuration Manager para instalação nos computadores da empresa. O cliente é instalado quando o computador é iniciado. Quando você usa a política de grupo, o cliente é exibido no Painel de Controle **Adicionar ou Remover Programas** para que o usuário o instale.  

 Use o pacote do Windows Installer (CCMSetup.msi) para instalações baseadas na política de grupo. Esse arquivo é encontrado na pasta **&lt;diretório de instalação do ConfigMgr\>\bin\i386** no servidor do site do Configuration Manager. Não é possível adicionar propriedades a esse arquivo para modificar o comportamento da instalação.  

> [!IMPORTANT]  
>  Você deve ter permissões de administrador para acessar os arquivos de instalação do cliente.  

-   Se o esquema do Active Directory estiver estendido para o Configuration Manager e **Publicar este site no Active Directory Domain Services** estiver selecionado na guia **Avançado** da caixa de diálogo **Propriedades do Site**, os computadores cliente pesquisarão automaticamente as propriedades de instalação do Active Directory Domain Services. Para obter mais informações sobre as propriedades de instalação publicadas, consulte [Sobre as propriedades de instalação do cliente publicadas no Active Directory Domain Services](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

-   Se o esquema do Active Directory não foi estendido, use o procedimento descrito neste tópico para armazenar as propriedades de instalação no Registro de computadores: [Como provisionar as propriedades de instalação do cliente (política de grupo e instalação do cliente baseada em atualização de software)](#BKMK_Provision). Essas propriedades de instalação são usadas quando o cliente é instalado.  

Para obter informações sobre como usar a política de grupo no Active Directory Domain Services para instalar um software, consulte a documentação do Windows Server.  



##  <a name="BKMK_Manual"></a> Como instalar clientes manualmente  
 Você pode instalar manualmente o software cliente em computadores na sua empresa usando o programa CCMSetup.exe. Esse programa e seus arquivos de suporte podem ser encontrados na pasta **Cliente** da pasta de instalação do Configuration Manager no servidor do site e nos pontos de gerenciamento no seu site. Esta pasta é compartilhada na rede como  

 \\\\*&lt;Nome do servidor do site\>* \SMS_*&lt;Código do site\>* \Client\  

 em que *&lt;Nome do Servidor do Site\>* é o nome de um dos servidores que hospeda um ponto de gerenciamento e *&lt;Código do Site\>* é o código do site primário ao qual o cliente é atribuído. Para executar CCMSetup.exe da linha de comando no cliente, é preciso mapear uma unidade de rede para esse local e executar o comando.  

> [!IMPORTANT]  
>  Você deve ter permissões de administrador para acessar os arquivos de instalação do cliente.  

 O CCMSetup.exe copia todos os pré-requisitos necessários para o computador cliente e chama o pacote do Windows Installer (Client.msi) para instalar o cliente. Não é possível executar o Client.msi diretamente.  

 Você pode especificar propriedades da linha de comando para o CCMSetup.exe e o Client.msi para modificar o comportamento da instalação do cliente. Verifique se você especificou as propriedades de CCMSetup (as propriedades que começam com **/**) antes de especificar as propriedades de Client.msi. Por exemplo:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`    

e o cliente é instalado usando as seguintes propriedades:  

|Propriedade|Descrição|  
|--------------|-----------------|  
|**/mp:SMSMP01**|Esta propriedade de CCMSetup especifica o ponto de gerenciamento SMSMP01 para baixar os arquivos de instalação necessários do cliente.|  
|**/logon**|Esta propriedade de CCMSetup especifica que a instalação deverá parar se um cliente do Configuration Manager for encontrado no computador.|  
|**SMSSITECODE=AUTO**|Esta propriedade de Client.msi especifica que o cliente tenta localizar o código do site do Configuration Manager a ser usado, por exemplo, usando o Active Directory Domain Services.|  
|**FSP=SMSFP01**|Essa propriedade de Client.msi especifica que o ponto de status de fallback chamado SMSFP01 é usado para receber mensagens de estado enviadas do computador cliente.|  

 Para obter detalhes sobre todas as propriedades de CCMSetup.exe, consulte [Sobre as propriedades de instalação do cliente](../../../core/clients/deploy/about-client-installation-properties.md)  

> [!Tip]  
> Para que o procedimento instale o cliente do Configuration Manager em um dispositivo Windows 10 moderno usando a identidade do Azure AD, consulte [Instalar e atribuir os clientes do Windows 10 do Configuration Manager usando o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Esse procedimento destina-se a clientes na intranet ou na Internet.  


### <a name="examples"></a>Exemplos
 Esses exemplos destinam-se a clientes do Active Directory na intranet. Eles usam os seguintes valores para representar diferentes aspectos do site:  

 **MPSERVER** = servidor que hospeda o ponto de gerenciamento   
**FSPSERVER** = servidor que hospeda o ponto de status de fallback  
**ABC** = código do site  
**contoso.com** = nome de domínio  

 Todos os servidores do sistema de sites são configurados com um FQDN de intranet. O site é publicado na floresta do Active Directory do cliente.  

 No computador cliente, faça logon como administrador local, mapeie uma unidade (z:) para \\\MPSERVER\SMS_ABC\Client, alterne o prompt de comando para a unidade z e, em seguida, execute um dos seguintes comandos:  

 **Exemplo 1:**  

`CCMSetup.exe`  

Este exemplo instala o cliente sem propriedades adicionais. O cliente é configurado automaticamente com as propriedades de instalação do cliente publicadas no Active Directory Domain Services. Ele é definido automaticamente com as seguintes configurações: 
- Código do site. Essa configuração exige que um local de rede do cliente seja incluído em um grupo de limites configurado para atribuição do cliente. 
- Ponto de gerenciamento
- Ponto de status de fallback
- Comunicar-se usando somente HTTPS  
  
Para obter mais informações, consulte [Sobre as propriedades de instalação do cliente publicadas no Active Directory Domain Services](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

 **Exemplo 2:**  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
Esse exemplo substitui a configuração automática fornecida pelo Active Directory Domain Services. Ele não exige que o local de rede do cliente seja incluído em um grupo de limites configurado para atribuição do cliente. Em vez disso, a instalação especifica as seguintes configurações:
- Código do site
- Ponto de gerenciamento da intranet 
- Ponto de gerenciamento baseado na Internet
- Ponto de status de fallback que aceita conexões da Internet
- Usar um certificado PKI (se disponível) do cliente que tem o período de validade mais longo  



##  <a name="BKMK_ClientLogonScript"></a> Como instalar clientes com scripts de logon  
 O Configuration Manager dá suporte a scripts de logon para instalar o software cliente do Configuration Manager. Você pode usar o arquivo de programa **CCMSetup.exe** em um script de logon para disparar a instalação do cliente.  

 A instalação de script de logon usa os mesmos métodos da instalação manual do cliente. Especifique a propriedade de instalação **/logon** para CCMSsetup.exe. Se uma versão do cliente já existir no computador, essa propriedade impedirá que o cliente seja instalado. Esse comportamento impede que a reinstalação do cliente ocorra sempre que o script de logon é executado.  

 Se nenhuma fonte de instalação for especificada pela propriedade **/Source** e nenhum ponto de gerenciamento do qual obter a instalação for especificado pela propriedade **/MP**, CCMSetup.exe localizará o ponto de gerenciamento pesquisando o Active Directory Domain Services. Esse comportamento ocorrerá apenas se o esquema for estendido para o Configuration Manager e o site for publicado no Active Directory Domain Services. Como alternativa, o cliente pode usar DNS ou WINS para localizar um ponto de gerenciamento.  



##  <a name="BKMK_ClientApp"></a> Como instalar clientes com um pacote e programa  
 Você pode usar o Configuration Manager para criar e implantar um pacote e um programa que atualiza o software cliente para computadores selecionados na hierarquia. Um arquivo de definição de pacote que preenche as propriedades do pacote com valores geralmente usados é fornecido com o Configuration Manager. Personalize o comportamento da instalação do cliente especificando propriedades de linha de comando adicionais.  

> [!NOTE]  
>  Não é possível atualizar clientes do Configuration Manager 2007 usando esse método. Em vez disso, use a atualização automática de cliente, que cria e implanta automaticamente um pacote com a versão mais recente do cliente. Para obter mais informações, consulte [Atualizar clientes](../../../core/clients/manage/upgrade/upgrade-clients.md).  
>   
>  Para obter mais informações sobre como migrar de versões mais antigas do cliente do Configuration Manager, consulte [Planejando uma estratégia de migração do cliente](../../../core/migration/planning-a-client-migration-strategy.md).  

 
### <a name="create-a-package-and-program-for-the-client-software"></a>Criar um pacote e um programa para o software cliente  

Use o procedimento a seguir para criar um pacote e um programa do Configuration Manager que você possa implantar nos computadores cliente do Configuration Manager para atualizar o software cliente.  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Pacotes**.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Pacote com base na Definição**.  

4.  Na página **Definição do Pacote** do assistente, selecione **Microsoft** na lista suspensa **Editor** e selecione **Atualização de Cliente do Configuration Manager** na lista **Definição do pacote**.  

5.  Na página **Arquivos de Origem**, selecione **Sempre obter arquivos da pasta de origem**.  

6.  Na página **Pasta de Origem**, selecione **Caminho de rede (Nome UNC)**. Em seguida, insira o caminho de rede para o computador e a pasta que contém os arquivos de instalação do cliente.  

    > [!NOTE]  
    >  O computador no qual a implantação do Configuration Manager é executada deverá ter acesso à pasta de rede especificada; caso contrário, a instalação falhará.  

    Para alterar uma das propriedades de instalação do cliente, modifique os parâmetros de linha de comando do CCMSetup.exe na guia **Geral** da caixa de diálogo do programa **Propriedades de atualização silenciosa de agente do Configuration Manager**. As propriedades de instalação padrão são **/noservice SMSSITECODE=AUTO**.  

9. Distribua o pacote para todos os pontos de distribuição em que você deseja hospedar o pacote de atualização do cliente. Em seguida, você pode implantar o pacote nas coleções de computador que contêm clientes que você deseja atualizar.  



## <a name="bkmk_mdm"></a>Como instalar clientes em dispositivos Windows gerenciados pelo Intune MDM

Você pode implantar os arquivos de instalação do cliente em computadores que são registrados com o Microsoft Intune. 

Esse procedimento destina-se a um cliente tradicional conectado à intranet. Ele usa métodos tradicionais de autenticação de cliente. Para garantir que o dispositivo permaneça em um estado gerenciado após a instalação do software cliente, o dispositivo deve estar na intranet e dentro de um limite do site do Configuration Manager.  

Para que o procedimento instale o cliente do Configuration Manager em um dispositivo Windows 10 moderno usando a identidade do Azure AD, consulte [Instalar e atribuir os clientes do Windows 10 do Configuration Manager usando o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

> [!NOTE]
> Depois que o software cliente é instalado, o registro do dispositivo no Intune é cancelado.
> 
> A partir da versão 1710, os clientes não cancelam o registro do Intune. Eles podem ter o cliente do Configuration Manager e o registro de MDM ao mesmo tempo. Para obter mais informações, consulte [Cogerenciamento](/sccm/core/clients/manage/co-management-overview).

###  <a name="install-clients-with-intune"></a>Para instalar clientes com o Intune:

1. No Intune, [crie um aplicativo](/intune/deploy-use/add-apps-for-mobile-devices-in-microsoft-intune) que contém o arquivo de instalação de cliente do Configuration Manager **ccmsetup.msi**. Esse arquivo é encontrado na pasta **&lt;diretório de instalação do ConfigMgr\>\bin\i386** no servidor do site do Configuration Manager.

2. No Intune Software Publisher, insira os parâmetros de linha de comando. Por exemplo, use a seguinte linha de comando com um cliente tradicional na intranet:

  `CCMSETUPCMD="/MP:&lt;FQDN of management point> SMSMP=&lt;FQDN of management point> SMSSITECODE=&lt;Your site code> DNSSUFFIX=&lt;DNS Suffix of management point>"`  

   > [!Note]  
   > Para obter uma linha de comando de exemplo a ser usada com um cliente moderno do Windows 10 usando a autenticação do Azure AD, consulte [Preparar dispositivos Windows 10 para o cogerenciamento](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client).

3. [Implante o aplicativo](/intune/deploy-use/deploy-apps-in-microsoft-intune) nos computadores Windows registrados.



##  <a name="BKMK_ClientImage"></a> Como instalar clientes com uma imagem do computador  
Pré-instale o software cliente do Configuration Manager em um computador de referência utilizado para criar uma imagem do sistema operacional.   

> [!Important]
> Ao usar a sequência de tarefas do Configuration Manager para implantar a imagem do sistema operacional, a etapa [Preparar Cliente do ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) da sequência de tarefas remove completamente o cliente do Configuration Manager. 

### <a name="prepare-the-client-computer-for-imaging"></a>Preparar o computador cliente para a geração de imagens  

1.  Instale manualmente o software cliente do Configuration Manager no computador de referência. Para obter mais informações, consulte [Como instalar manualmente os clientes do Configuration Manager](#BKMK_Manual).  

    > [!IMPORTANT]  
    >  Não especifique um código do site do Configuration Manager para o cliente nas propriedades de linha de comando do CCMSetup.exe.  

2.  Em um prompt de comando, digite `net stop ccmexec` para garantir que o serviço **Host de Agente do SMS** (Ccmexec.exe) não esteja sendo executado no computador de referência.
3.  Exclua o arquivo **SMSCFG.INI** da pasta **Windows** no computador de referência.  
3.  Remova os certificados armazenados no repositório de computador local no computador de referência. Por exemplo, se você usar certificados PKI (infraestrutura de chave pública), deverá remover os certificados na loja **Pessoal** para **Computador** e **Usuário** antes de criar a imagem no computador.

4.  Se os clientes forem instalados em uma hierarquia do Configuration Manager diferente do computador de referência, remova a chave de raiz confiável do computador de referência.  
    > [!NOTE]  
    >  Se os clientes não conseguirem consultar os Serviços de Domínio do Active Directory para localizar um ponto de gerenciamento, eles usarão a chave de raiz confiável para determinar pontos de gerenciamento confiáveis. Se todos os clientes com imagens forem implantados na mesma hierarquia do computador mestre, deixe a chave de raiz confiável no lugar. Se os clientes forem implantados em hierarquia diferentes, remova a chave de raiz confiável. Provisione também esses clientes com a nova chave de raiz confiável. Para obter mais informações, consulte [Planejando a chave de raiz confiável](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK). 

5.  Use o software de geração de imagens para capturar a imagem do computador mestre.  

6.  Implante a imagem nos computadores de destino.  



##  <a name="BKMK_ClientWorkgroup"></a> Como instalar clientes em computadores do grupo de trabalho  
 O Configuration Manager dá suporte à instalação do cliente para computadores do grupos de trabalho. Instale o cliente em computadores do grupo de trabalho usando o método especificado em [Como instalar manualmente os clientes do Configuration Manager](#BKMK_Manual).  

 Pré-requisitos:  

-   O cliente deve ser instalado manualmente em cada computador do grupo de trabalho. Durante a instalação, o usuário conectado deve ter direitos de administrador local.  

-   Para acessar recursos no domínio de servidor do site do Configuration Manager, a conta de acesso à rede deve ser configurada para o site. Especifique essa conta como uma propriedade do componente de distribuição de software. Para obter mais informações, consulte [Componentes do site para o System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

 Limitações:  

-   Os clientes do grupo de trabalho não podem localizar pontos de gerenciamento dos Serviços de Domínio do Active Directory. Em vez disso, devem usar DNS, WINS ou outro ponto de gerenciamento.  

-   Não há suporte para roaming global, pois os clientes não podem consultar os Serviços de Domínio do Active Directory para obter informações do site.  

-   Os métodos de descoberta do Active Directory não podem descobrir computadores do grupos de trabalho.  

-   Não é possível implantar o software para os usuários de computadores do grupo de trabalho.  

-   Você não pode usar o método de instalação do cliente por push para instalar o cliente em computadores do grupo de trabalho.  

-   Clientes do grupo de trabalho não podem usar o Kerberos para autenticação e podem exigir aprovação manual.  

-   Um cliente de grupo de trabalho não pode ser configurado como um ponto de distribuição. O Configuration Manager exige que os computadores do ponto de distribuição sejam membros de um domínio.  

### <a name="install-the-client-on-workgroup-computers"></a>Instalar o cliente em computadores do grupo de trabalho  

Verifique os pré-requisitos e, em seguida, siga as instruções da seção [Como instalar manualmente os clientes do Configuration Manager](#BKMK_Manual).  

   Este exemplo instala o cliente para gerenciamento de clientes de intranet e especifica o código do site e o sufixo DNS para localizar um ponto de gerenciamento. `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

     

   Esse exemplo exige que o cliente esteja em um local de rede configurado em um grupo de limites. Esse requisito existe para que a atribuição automática de site seja bem-sucedida. O comando inclui um ponto de status de fallback no servidor FSPSERVER. Essa propriedade ajuda a acompanhar a implantação do cliente e identificar os problemas de comunicação do cliente. 
   `CCMSetup.exe FSP=fspserver.constoso.com`  

      

##  <a name="BKMK_ClientInternet"></a> Como instalar clientes para o gerenciamento de clientes baseado na Internet  
 
> [!Note]
> Esta seção não se aplica a clientes que usam um [gateway de gerenciamento de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway). Para instalar clientes baseados na Internet usando um gateway de gerenciamento de nuvem, consulte [Instalar e atribuir clientes do Windows 10 do Configuration Manager usando o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

Quando o site do Configuration Manager dá suporte ao [gerenciamento de clientes baseado na Internet](/sccm/core/clients/manage/plan-internet-based-client-management) para clientes que, às vezes, estão na intranet e, outras, na Internet, você tem duas opções ao instalar clientes na intranet:  

-   Inclua a propriedade CCMHOSTNAME=*&lt;FQDN da Internet do ponto de gerenciamento baseado na Internet\>* de Client.msi ao instalar o cliente, por exemplo, usando a instalação manual ou do cliente por push. Ao usar esse método, você também deve atribuir diretamente o cliente ao site e não pode usar a atribuição automática do site. A seção [Como instalar manualmente os clientes do Configuration Manager](#BKMK_Manual) neste tópico fornece um exemplo desse método de configuração.  

-   Instale o cliente para o gerenciamento de clientes na intranet e, em seguida, atribua um ponto de gerenciamento de clientes baseado na Internet ao cliente. Altere o ponto de gerenciamento usando as propriedades do cliente do Configuration Manager no Painel de Controle ou usando um script. Ao usar esse método, você pode usar a atribuição automática de clientes. Para obter mais informações, consulte a seção [Como configurar clientes para o gerenciamento de clientes baseado na Internet após a instalação do cliente](#BKMK_ConfigureIBCM_MP) neste tópico.  

 Se precisar instalar clientes que estão na Internet, escolha um dos seguintes métodos compatíveis:  

-   Forneça um mecanismo para que esses clientes se conectem temporariamente à intranet com uma VPN. Em seguida, instale o cliente usando um método de instalação do cliente apropriado.  

-   Use um método de instalação que não depende do Configuration Manager. Por exemplo, empacote os arquivos de origem de instalação do cliente em uma mídia removível que você pode enviar para os usuários, para instalação com instruções. Os arquivos de origem de instalação do cliente estão localizados na pasta *&lt;InstallationPath\>* \Client no servidor do site do Configuration Manager e nos pontos de gerenciamento. Inclua na mídia um script para copiar manualmente na pasta do cliente e dessa pasta, instale o cliente usando o CCMSetup.exe e todas as propriedades da linha de comando CCMSetup apropriada.  

> [!NOTE]  
>  O Configuration Manager não dá suporte à instalação de um cliente diretamente do ponto de gerenciamento baseado na Internet ou do ponto de atualização de software baseado na Internet.  

 Os clientes gerenciados pela Internet devem se comunicar com sistemas de sites baseados na Internet. Garanta que esses clientes também têm certificados PKI (infraestrutura de chave pública) antes de instalar o cliente. Instale esses certificados independentemente do Configuration Manager. Para obter mais informações sobre os requisitos de certificado, consulte [Requisitos do certificado PKI](../../../core/plan-design/network/pki-certificate-requirements.md).  

### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Instalar clientes na Internet especificando as propriedades de linha de comando do CCMSetup  

1.  Siga as instruções da seção [Como instalar manualmente os clientes do Configuration Manager](#BKMK_Manual) e sempre inclua o seguinte:  

    -   Propriedade de linha de comando do CCMSetup **/source:***&lt;caminho local para a pasta Client copiada\>*  

    -   Propriedade da linha de comando CCMSetup **/UsePKICert**  

    -   Propriedade **CCMHOSTNAME=***&lt;FQDN do ponto de gerenciamento baseado na Internet\>* de Client.msi  

    -   Propriedade **SMSSIGNCERT=***&lt;caminho local para o certificado de autenticação do servidor do site exportado\>* de Client.msi  

    -   Propriedade **SMSSITECODE=***&lt;código do site do ponto de gerenciamento baseado na Internet\>* de Client.msi  

    > [!NOTE]  
    >  Se o site tiver mais de um ponto de gerenciamento baseado na Internet, qualquer ponto de gerenciamento baseado na Internet poderá especificado para a propriedade CCMHOSTNAME. Quando um cliente do Configuration Manager se conecta ao ponto de gerenciamento baseado na Internet, o ponto de gerenciamento envia ao cliente uma lista de pontos de gerenciamento baseados na Internet disponíveis no site. O cliente seleciona um ponto aleatoriamente na lista.  

2.  Se você não quiser que o cliente verifique a CRL (lista de revogação de certificados), especifique a propriedade da linha de comando CCMSetup **/NoCRLCheck**.  

3.  Se estiver usando um ponto de status de fallback baseado na Internet, especifique a propriedade **FSP=***&lt;FQDN da Internet do ponto de status de fallback baseado na Internet\>* de Client.msi.  

4.  Se estiver instalando o cliente para o gerenciamento de clientes apenas na Internet, especifique a propriedade **CCMALWAYSINF=1** de Client.msi.  

5.  Verifique se você precisa especificar propriedades adicionais da linha de comando CCMSetup. Por exemplo, talvez você precise especificar um critério de seleção de certificados se o cliente tiver mais de um certificado PKI válido. Para obter uma lista de propriedades disponíveis, consulte [Sobre as propriedades de instalação do cliente](../../../core/clients/deploy/about-client-installation-properties.md).  

   Exemplo:  
   `CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`    

   Este exemplo instala o cliente com os seguintes comportamentos:
   - Usar arquivos de origem de uma pasta na unidade D
   - Usar um certificado PKI do cliente 
   - Selecionar o certificado com o período de validade mais longo 
   - Gerenciamento de clientes apenas na Internet
   - Atribuir o cliente a usar o ponto de gerenciamento baseado na Internet chamado SERVER1
   - Atribuir o ponto de status de fallback baseado na Internet no domínio contoso.com
   - Atribuir o cliente ao site ABC  

###  <a name="BKMK_ConfigureIBCM_MP"></a>Para configurar clientes para o gerenciamento de clientes baseado na Internet após a instalação do cliente  
 Para atribuir o ponto de gerenciamento baseado na Internet após a instalação do cliente, use um destes procedimentos. O primeiro requer configuração manual e é apropriado para poucos clientes. O segundo é mais apropriado para a configuração de muitos clientes.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-assigning-the-internet-based-management-point-in-configuration-manager-properties"></a>Configurar clientes para o gerenciamento de clientes baseado na Internet após a instalação do cliente atribuindo o ponto de gerenciamento baseado na Internet nas propriedades do Configuration Manager  

1.  Navegue até **Configuration Manager** no Painel de Controle do computador cliente e clique duas vezes para abrir suas propriedades.  

2.  Na guia **Internet**, insira o nome de domínio totalmente qualificado do ponto de gerenciamento baseado na Internet na caixa de texto FQDN de Internet.  

    > [!NOTE]  
    >  A guia **Internet** só ficará disponível se o cliente tiver um certificado PKI do cliente.  

3.  Se o cliente acessar a Internet usando um servidor proxy, insira as configurações do servidor proxy.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Configurar clientes para o gerenciamento de clientes baseado na Internet após a instalação do cliente usando um script  

1.  Abra um editor de texto, como o Bloco de Notas.  

2.  Copie e insira a amostra de VBScript a seguir no arquivo. Substitua *mp.contoso.com* pelo FQDN de Internet do ponto de gerenciamento baseado na Internet.  

    ```  
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the internet-based management point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

    > [!NOTE]  
    >  Caso precise excluir um ponto de gerenciamento baseado na Internet especificado, para que o cliente não seja configurado para usar um ponto de gerenciamento baseado na Internet, remova o valor dentro das aspas para que essa linha se torne `newInternetBasedManagementPointFQDN = ""`  

4.  Salve o arquivo com uma extensão .vbs.  

5.  Use cscript.exe para executar o script nos computadores cliente, usando um dos seguintes métodos:  

    -   Implante o arquivo nos clientes existentes do Configuration Manager usando um pacote e um programa.  

    -   Execute o arquivo localmente em clientes existentes do Configuration Manager clicando duas vezes no arquivo de script do Windows Explorer.  

 Talvez você precise reiniciar o cliente para que as alterações entrem em vigor.  



##  <a name="BKMK_Provision"></a> Como provisionar propriedades de instalação de cliente (política de grupo e instalação do cliente baseada em atualização de software)  
 Use a política de grupo do Windows para provisionar computadores com as propriedades de instalação do cliente do Configuration Manager. Essas propriedades estão armazenadas no Registro do computador e são lidas quando o software cliente é instalado. Esse procedimento normalmente não é necessário, mas pode ser necessário para alguns cenários de instalação do cliente, como:  

-   Você está usando as configurações de política de grupo ou métodos de instalação do cliente baseados em atualização de software. Você não estendeu o esquema do Active Directory para o Configuration Manager.  

-   Você deseja substituir as propriedades de instalação do cliente em computadores específicos.  

> [!NOTE]  
>  Se uma das propriedades de instalação for fornecida na linha de comando do CCMSetup.exe, as propriedades de instalação provisionadas nos computadores não serão usadas.  

 Um modelo administrativo de política de grupo chamado ConfigMgrInstallation.adm é fornecido na mídia de instalação do Configuration Manager. Esse modelo pode ser usado para provisionar computadores cliente com propriedades de instalação.   

### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Configurar e atribuir as propriedades de instalação do cliente usando um Objeto de política de grupo  

1.  Importe o modelo administrativo ConfigMgrInstallation.adm para um objeto de política de grupo novo ou existente, usando um editor como o Editor de Objeto de Política de Grupo do Windows. O arquivo pode ser localizado na pasta **TOOLS\ConfigMgrADMTemplates** na mídia de instalação do Configuration Manager.  

2.  Abra as propriedades da configuração importada **Definir configurações de implantação de cliente**.  

3.  Escolha **Habilitado**.  

4.  Na caixa **CCMSetup** , digite as propriedades de linha de comando CCMSetup necessárias. Para obter uma lista das propriedades de linha de comando do CCMSetup e exemplos de uso, consulte [Sobre as propriedades de instalação do cliente](../../../core/clients/deploy/about-client-installation-properties.md).  

5.  Atribua o objeto de política de grupo aos computadores que deseja provisionar com as propriedades de instalação do cliente do Configuration Manager.  

Para obter informações sobre a política de grupo do Windows, consulte a documentação do Windows Server.  



## <a name="next-steps"></a>Próximas etapas
Para obter mais ajuda para instalação do cliente do Configuration Manager, consulte [Métodos de instalação do cliente](../../../core/clients/deploy/plan/client-installation-methods.md).