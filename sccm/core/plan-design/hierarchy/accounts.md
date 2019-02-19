---
title: Contas usadas
titleSuffix: Configuration Manager
description: Identifique e gerencie grupos e contas do Windows no Configuration Manager.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f0c9ad4831d0450b7a30de4117a65005164d5080
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122382"
---
# <a name="accounts-used-in-configuration-manager"></a>Contas usadas no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as seguintes informações para identificar os grupos e as contas do Windows usados no Configuration Manager, como são usados e quais são os requisitos.  

- [Grupos do Windows que o Configuration Manager cria e usa](#bkmk_groups)  
    - [ConfigMgr_CollectedFilesAccess](#configmgrcollectedfilesaccess)  
    - [ConfigMgr_DViewAccess](#configmgrdviewaccess)  
    - [Usuários de Controle Remoto do ConfigMgr](#configmgr-remote-control-users)  
    - [Administradores de SMS](#sms-admins)  
    - [SMS_SiteSystemToSiteServerConnection_MP_&lt;sitecode\>](#bkmk_remotemp)  
    - [SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;sitecode\>](#bkmk_remoteprov)  
    - [SMS_SiteSystemToSiteServerConnection_Stat_&lt;sitecode\>](#bkmk_remotestat)  
    - [SMS_SiteToSiteConnection_&lt;sitecode\>](#bkmk_filerepl)  

- [Contas que o Configuration Manager usa](#bkmk_accounts)
    - [Conta de descoberta de grupo do Active Directory](#active-directory-group-discovery-account)  
    - [Conta de descoberta de sistemas do Active Directory](#active-directory-system-discovery-account)  
    - [Conta de descoberta de usuário do Active Directory](#active-directory-user-discovery-account)  
    - [Conta da floresta do Active Directory](#active-directory-forest-account)  
    - [Conta do ponto de registro de certificado](#certificate-registration-point-account)  
    - [Conta de captura da imagem do sistema operacional](#capture-os-image-account)  
    - [Conta de instalação do cliente por push](#client-push-installation-account)  
    - [Conta de conexão do ponto de registro](#enrollment-point-connection-account)  
    - [Conta de conexão do Exchange Server](#exchange-server-connection-account)  
    - [Conta de conexão do ponto de gerenciamento](#management-point-connection-account)  
    - [Conta de conexão multicast](#multicast-connection-account)  
    - [Conta de acesso de rede](#network-access-account)  
    - [Conta de acesso ao Pacote](#package-access-account)  
    - [Conta do ponto do Reporting Services](#reporting-services-point-account)  
    - [Contas do visualizador permitidas em ferramentas remotas](#remote-tools-permitted-viewer-accounts)  
    - [Conta de instalação do site](#site-installation-account)
    - [Conta de instalação do sistema de sites](#site-system-installation-account)  
    - [Conta do servidor proxy do sistema de sites](#site-system-proxy-server-account)  
    - [Conta de conexão do servidor SMTP](#smtp-server-connection-account)  
    - [Conta da conexão do ponto de atualização do software](#software-update-point-connection-account)  
    - [Conta do site de origem](#source-site-account)  
    - [Conta do banco de dados do site de origem](#source-site-database-account)  
    - [Conta de ingresso no domínio de sequência de tarefas](#task-sequence-domain-join-account)  
    - [Conta de conexão de pasta de rede da sequência de tarefas](#task-sequence-network-folder-connection-account)  
    - [Execução da sequência de tarefas como conta](#task-sequence-run-as-account)  



## <a name="bkmk_groups"></a> Grupos do Windows que o Configuration Manager cria e usa  

 O Configuration Manager cria automaticamente e, em muitos casos, mantém automaticamente os seguintes grupos do Windows:  

> [!NOTE]  
>  Quando o Configuration Manager cria um grupo em um computador que é membro do domínio, trata-se de um grupo de segurança local. Se o computador for um controlador de domínio, o grupo será um grupo de domínio local. Esse tipo de grupo é compartilhado entre todos os controladores de domínio no domínio.  


### <a name="configmgrcollectedfilesaccess"></a>ConfigMgr_CollectedFilesAccess  

O Configuration Manager usa esse grupo para conceder acesso para exibir arquivos coletados pelo inventário de software.  

Para obter mais informações, consulte [Introdução ao inventário de software](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).

#### <a name="type-and-location"></a>Tipo e local
Esse é um grupo de segurança local criado no servidor do site primário.

Quando um site é desinstalado, esse grupo não é removido automaticamente. Exclua-o manualmente depois de desinstalar um site.

#### <a name="membership"></a>Associação
O Configuration Manager gerencia automaticamente a associação ao grupo. A associação inclui usuários administrativos que recebem a permissão **Exibir Arquivos Coletados** para o objeto protegível **Coleção** de uma função de segurança atribuída.

#### <a name="permissions"></a>Permissões
Por padrão, este grupo tem a permissão **Ler** para a seguinte pasta no servidor do site: `C:\Program Files\Microsoft Configuration Manager\sinv.box\FileCol`  


### <a name="configmgrdviewaccess"></a>ConfigMgr_DViewAccess  

 Esse grupo é um grupo de segurança local criado no servidor de banco de dados do site ou no servidor de réplica de banco de dados pelo Configuration Manager para um site primário filho. O site o cria quando você usa exibições distribuídas para a replicação de banco de dados entre sites em uma hierarquia. Ele contém o servidor do site e as contas de computador do SQL Server do site de administração central.

 Para obter mais informações, confira [Transferências de dados entre sites](/sccm/core/servers/manage/data-transfers-between-sites).


### <a name="configmgr-remote-control-users"></a>Usuários de Controle Remoto do ConfigMgr  

 As ferramentas remotas do Configuration Manager usam esse grupo para armazenar as contas e os grupos configurados na lista de **Visualizadores Permitidos**. O site atribui essa lista a cada cliente.  

Para obter mais informações, confira [Introdução ao controle remoto](/sccm/core/clients/manage/remote-control/introduction-to-remote-control).

#### <a name="type-and-location"></a>Tipo e local
Esse é um grupo de segurança local criado no cliente do Configuration Manager quando o cliente recebe uma política que habilita as ferramentas remotas.

Depois de desabilitar as ferramentas remotas para um cliente, esse grupo não é removido automaticamente. Exclua-o manualmente depois de desabilitar as ferramentas remotas.

#### <a name="membership"></a>Associação
Por padrão, não existem membros nesse grupo. Ao adicionar usuários à lista **Visualizadores Permitidos**, eles são adicionados automaticamente a esse grupo.

Use a lista **Visualizadores Permitidos** para gerenciar a associação desse grupo em vez de adicionar usuários ou grupos diretamente a esse grupo.

Além de ser visualizador permitido, um usuário administrativo deve ter a permissão **Controle Remoto** para o objeto **Coleção**. Atribua essa permissão usando a função de segurança **Operador de Ferramentas Remotas**.  

#### <a name="permissions"></a>Permissões
Por padrão, esse grupo não tem permissões para nenhum local no computador. Ele é usado apenas para armazenar a lista de **Visualizadores Permitidos**.  


### <a name="sms-admins"></a>Administradores de SMS  

 O Configuration Manager usa esse grupo para permitir acesso ao Provedor de SMS por meio do WMI. O acesso ao Provedor de SMS é necessário para exibir e alterar objetos no console do Configuration Manager.  

> [!NOTE]  
>  A configuração da administração baseada em funções de um usuário administrativo determina quais objetos eles podem exibir e gerenciar quando usam o console do Configuration Manager.  

Para obter mais informações, veja [Planejar para o provedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).

#### <a name="type-and-location"></a>Tipo e local
Esse é um grupo de segurança local criado em cada computador que possui um Provedor de SMS. 

Quando um site é desinstalado, esse grupo não é removido automaticamente. Exclua-o manualmente depois de desinstalar um site.

#### <a name="membership"></a>Associação
O Configuration Manager gerencia automaticamente a associação ao grupo. Por padrão, cada usuário administrativo em uma hierarquia e a conta de computador do servidor do site são membros do grupo **Administradores de SMS** em cada computador do Provedor de SMS de um site.

#### <a name="permissions"></a>Permissões
Você pode exibir os direitos e permissões para o grupo de administradores de SMS no snap-in do MMC de **Controle WMI**. Por padrão, esse grupo recebe **Habilitar Conta** e **Habilitação Remota** no namespace do WMI `Root\SMS`. Os Usuários Autenticados têm as permissões **Execute Methods**, **Provider Write**e **Enable Account**.

Quando você usa um console do Configuration Manager remoto, configure as permissões DCOM de **Ativação Remota** no computador servidor do site e no provedor de SMS. Conceda esses direitos ao grupo de **Administradores de SMS**. Essa ação simplifica a administração, em vez de conceder esses direitos diretamente a usuários ou grupos. Para obter mais informações, confira [Configurar permissões DCOM para consoles remotos do Configuration Manager](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ConfigDCOMforRemoteConsole). 


### <a name="bkmk_remotemp"></a> SMS_SiteSystemToSiteServerConnection_MP_&lt;sitecode\>  
 
Ponto de gerenciamento remotos com relação ao servidor do site usam esse grupo para conexão com o banco de dados do site. Esse grupo fornece a um ponto de gerenciamento acesso a pastas da caixa de entrada no servidor do site e ao banco de dados do site.  

#### <a name="type-and-location"></a>Tipo e local
Esse é um grupo de segurança local criado em cada computador que possui um Provedor de SMS.

Quando um site é desinstalado, esse grupo não é removido automaticamente. Exclua-o manualmente depois de desinstalar um site.

#### <a name="membership"></a>Associação
O Configuration Manager gerencia automaticamente a associação ao grupo. Por padrão, a associação inclui as contas de computadores remotos que têm um ponto de gerenciamento para o site.

#### <a name="permissions"></a>Permissões
Por padrão, esse grupo tem permissão para **Ler**, **Ler e executar** e **Listar conteúdo da pasta** para a seguinte pasta no servidor do site: `C:\Program Files\Microsoft Configuration Manager\inboxes`. Esse grupo tem a permissão adicional **Write** para subpastas abaixo da pasta **inboxes**, nas quais o ponto de gerenciamento grava dados do cliente.


### <a name="bkmk_remoteprov"></a> SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;sitecode\>  
 
Computadores do provedor de SMS remotos usam esse grupo para conectarem-se ao servidor do site.  

#### <a name="type-and-location"></a>Tipo e local
Esse é um grupo de segurança local criado no servidor do site.

Quando um site é desinstalado, esse grupo não é removido automaticamente. Exclua-o manualmente depois de desinstalar um site.

#### <a name="membership"></a>Associação
O Configuration Manager gerencia automaticamente a associação ao grupo. Por padrão, a associação inclui a conta de computador ou uma conta de usuário de domínio. Ele usa essa conta para se conectar ao servidor do site de cada Provedor de SMS remoto.

#### <a name="permissions"></a>Permissões
Por padrão, esse grupo tem permissão para **Ler**, **Ler e executar** e **Listar conteúdo da pasta** para a seguinte pasta no servidor do site: `C:\Program Files\Microsoft Configuration Manager\inboxes`. Esse grupo tem as permissões adicionais de **Gravar** e **Modificar** subpastas abaixo das caixas de entrada. O Provedor de SMS requer acesso a essas pastas.

Esse grupo também tem permissão de **Ler** para as subpastas no servidor do site abaixo `C:\Program Files\Microsoft Configuration Manager\OSD\Bin`. 

Também tem as seguintes permissões para as subpastas abaixo `C:\Program Files\Microsoft Configuration Manager\OSD\boot`:
- **Ler**  
- **Ler e executar**  
- **Listar conteúdo de pastas**  
- **Gravar**  
- **Modificar**   


### <a name="bkmk_remotestat"></a> SMS_SiteSystemToSiteServerConnection_Stat_&lt;sitecode\>  

O componente de gerenciador de expedição de arquivo no sistema de site remoto do Configuration Manager usa este grupo para se conectar ao servidor do site.  

#### <a name="type-and-location"></a>Tipo e local
Esse é um grupo de segurança local criado no servidor do site.

Quando um site é desinstalado, esse grupo não é removido automaticamente. Exclua-o manualmente depois de desinstalar um site.

#### <a name="membership"></a>Associação
O Configuration Manager gerencia automaticamente a associação ao grupo. Por padrão, a associação inclui a conta de computador ou a conta de usuário de domínio. Ele usa essa conta para se conectar ao servidor do site de cada sistema de site remoto que executa o gerenciador de expedição de arquivo.

#### <a name="permissions"></a>Permissões
Por padrão, esse grupo tem permissão para **Ler**, **Ler e executar** e **Listar conteúdo da pasta** para a seguinte pasta e subpastas no servidor do site: `C:\Program Files\Microsoft Configuration Manager\inboxes`. 

Esse grupo tem as permissões adicionais para **Gravar** e **Modificar** a seguinte pasta no servidor do site: `C:\Program Files\Microsoft Configuration Manager\inboxes\statmgr.box`.


### <a name="bkmk_filerepl"></a> SMS_SiteToSiteConnection_&lt;sitecode\>  
 O Configuration Manager usa esse grupo para permitir a replicação baseada em arquivos entre sites em uma hierarquia. Para cada site remoto que transfere arquivos diretamente para esse site, esse grupo tem contas configuradas como uma **Conta de Replicação de Arquivo**.  

#### <a name="type-and-location"></a>Tipo e local
Esse é um grupo de segurança local criado no servidor do site.

#### <a name="membership"></a>Associação
Quando você instala um novo site como filho de outro site, o Configuration Manager adiciona automaticamente a conta de computador do novo servidor do site a este grupo no servidor do site pai. O Configuration Manager também adiciona a conta do computador do site pai ao grupo no novo servidor do site. Se outra conta for especificada para transferências baseadas em arquivo, adicione essa conta a esse grupo no servidor do site de destino.

Quando um site é desinstalado, esse grupo não é removido automaticamente. Exclua-o manualmente depois de desinstalar um site.

#### <a name="permissions"></a>Permissões
Por padrão, esse grupo tem **Controle total** para a seguinte pasta: `C:\Program Files\Microsoft Configuration Manager\inboxes\despoolr.box\receive`.



## <a name="bkmk_accounts"></a> Contas que o Configuration Manager usa  

 É possível configurar as seguintes contas para o Configuration Manager.  


### <a name="active-directory-group-discovery-account"></a>Conta de descoberta de grupo do Active Directory  

 O site usa a **Conta de descoberta de grupo do Active Directory** para descobrir os seguintes objetos de localizações no Active Directory Domain Services que você especificar:
- Grupos de segurança locais, globais e universais
- A associação dentro desses grupos
- A associação dentro de grupos de distribuição
   - Os grupos de distribuição não são descobertos como recursos de grupo

  Essa conta pode ser uma conta de computador do servidor do site que executa a descoberta, ou uma conta de usuário do Windows. Ela precisa ter permissão de acesso de **Leitura** nas localizações do Active Directory especificadas para descoberta.  

  Para obter mais informações, confira [Descoberta de grupo do Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutGroup).


### <a name="active-directory-system-discovery-account"></a>Conta de descoberta de sistemas do Active Directory  

 O site usa a **Conta de descoberta do sistema do Active Directory** para descobrir computadores das localizações no Active Directory Domain Services que você especificar.  

 Essa conta pode ser uma conta de computador do servidor do site que executa a descoberta, ou uma conta de usuário do Windows. Ela precisa ter permissão de acesso de **Leitura** nas localizações do Active Directory especificadas para descoberta.  

 Para saber mais, confira [Descoberta de sistema do Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutSystem).


### <a name="active-directory-user-discovery-account"></a>Conta de descoberta de usuário do Active Directory  
 
 O site usa a **Conta de descoberta de usuário do Active Directory** para descobrir contas de usuário das localizações no Active Directory Domain Services que você especificar.  

 Essa conta pode ser uma conta de computador do servidor do site que executa a descoberta, ou uma conta de usuário do Windows. Ela precisa ter permissão de acesso de **Leitura** nas localizações do Active Directory especificadas para descoberta.  

 Para obter mais informações, confira [Descoberta de usuário do Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser). 


### <a name="active-directory-forest-account"></a>Conta da floresta do Active Directory  

 O site usa a **Conta de Floresta do Active Directory** para descobrir a infraestrutura de rede em florestas do Active Directory. Os sites de administração central e sites primários também o usam para publicar dados do site no Active Directory Domain Services para uma floresta.  

 > [!NOTE]  
 >  Sites secundários usam sempre a conta de computador do servidor do site secundário para publicar no Active Directory.  

 Para descobrir e publicar em florestas não confiáveis, a conta da floresta do Active Directory deve ser uma conta global. Se você não usar a conta de computador do servidor do site, selecione somente uma conta global.  

 Essa conta deve ter a permissão **Ler** em cada floresta do Active Directory de onde você deseja descobrir a infraestrutura de rede.  

 Essa conta deve ter a permissão **Controle Total** no contêiner **Gerenciamento do Sistema** e todos os seus objetos filho em cada floresta do Active Directory em que você deseja publicar dados do site. Para obter mais informações, consulte [Preparar o Active Directory para publicação de sites](/sccm/core/plan-design/network/extend-the-active-directory-schema).  

 Para obter mais informações, confira [Sobre a descoberta de floresta do Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutForest).


### <a name="certificate-registration-point-account"></a>Conta do ponto de registro de certificado  

 O ponto de registro do certificado usa a **Conta do ponto de registro de certificado** para conectar-se ao banco de dados do Configuration Manager. Ele usa sua conta de computador por padrão, mas você pode configurar uma conta de usuário em vez disso. Quando o ponto de registro de certificado estiver em um domínio não confiável do servidor do site, você deve especificar uma conta de usuário. Essa conta requer acesso somente de **Leitura** ao banco de dados do site, pois operações de gravação são administradas pelo sistema de mensagem de estado.  

 Para obter mais informações, consulte [Introdução aos perfis de certificado](/sccm/protect/deploy-use/introduction-to-certificate-profiles).


### <a name="capture-os-image-account"></a>Conta de captura da imagem do sistema operacional  

 Quando você captura uma imagem do sistema operacional, o Configuration Manager usa a **Conta de captura de imagem do sistema operacional** para acessar a pasta na qual você armazena as imagens capturadas. Se você adicionar a etapa **Capturar imagem do sistema operacional** a uma sequência de tarefas, essa conta será necessária.  

 A conta deve ter permissões de **Leitura** e **Gravação** no compartilhamento de rede em que você armazena a imagem capturada.  

 Se você alterar a senha para a conta no Windows, atualize a sequência de tarefas com a nova senha. O cliente do Configuration Manager recebe a nova senha quando baixa a política do cliente.  

 Se você precisar usar essa conta, crie uma conta de usuário de domínio. Conceda a ela permissões mínimas para acessar os recursos de rede necessários e use-a para todas as sequências de tarefas de captura.  

 > [!IMPORTANT]  
 >  Não atribua permissões de entrada interativa a essa conta.  
 >   
 >  Não use a conta de acesso à rede para essa conta.  

 Para obter mais informações, confira [Criar uma sequência de tarefas para capturar um sistema operacional](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system).


### <a name="client-push-installation-account"></a>Conta de instalação do cliente por push  

 Quando você implanta clientes usando o método de instalação do cliente por push, o site usa a **Conta de instalação do cliente por push** para a conexão a computadores e a instalação do software cliente do Configuration Manager. Se você não especificar essa conta, o servidor do site tentará usar sua conta de computador.  

 Essa conta deve ser um membro do grupo **Administradores** local nos computadores cliente de destino. Essa conta não exige direitos de **Administrador de Domínio**.  

 Você pode especificar mais de uma conta de instalação do cliente por push. O Configuration Manager tentará cada uma sucessivamente até obter êxito.  

> [!TIP]  
>  Se você tem um ambiente grande do Active Directory e precisa alterar essa conta, use o seguinte processo para coordenar mais eficazmente essa atualização de conta: 
> 1. Crie uma nova conta com um nome diferente   
> 2. Adicione a nova conta à lista de contas de instalação do cliente por push do Configuration Manager  
> 3. Dê tempo suficiente para o Active Directory Domain Services replicar a nova conta  
> 4. Em seguida, remova a conta antiga do Configuration Manager e do Active Directory Domain Services  

> [!IMPORTANT]  
>  Não conceda a essa conta o direito de entrar localmente.  

 Para saber mais, confira [Instalação no cliente por push](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation).


### <a name="enrollment-point-connection-account"></a>Conta de conexão do ponto de registro  

 O ponto de registro usa a **Conta de conexão do ponto de registro** para conectar-se ao banco de dados do Configuration Manager. Ele usa sua conta de computador por padrão, mas você pode configurar uma conta de usuário em vez disso. Quando o ponto de registro estiver em um domínio não confiável do servidor do site, especifique uma conta de usuário. Essa conta requer acesso de **Leitura** e **Gravação** ao banco de dados do site.  

 Para obter mais informações, confira [Instalar funções do sistema de site para o MDM local](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm).


### <a name="exchange-server-connection-account"></a>Conta de conexão do Exchange Server  

 O servidor do site usa a **Conta de conexão do Exchange Server** para se conectar ao Exchange Server especificado. Ele usa essa conexão para localizar e gerenciar dispositivos móveis que se conectam ao Exchange Server. Essa conta requer cmdlets do Exchange PowerShell que fornecem as permissões necessárias para o computador do Exchange Server. Para obter mais informações sobre os cmdlets, confira [Gerenciar dispositivos móveis com o Configuration Manager e o Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  


### <a name="management-point-connection-account"></a>Conta de conexão do ponto de gerenciamento  

 O ponto de gerenciamento usa a **Conta de conexão do ponto de gerenciamento** para conectar-se ao banco de dados do Configuration Manager. Ele usa essa conexão para enviar e recuperar informações para os clientes. O ponto de gerenciamento usa sua conta de computador por padrão, mas você pode configurar uma conta de usuário em vez disso. Quando o ponto de gerenciamento estiver em um domínio não confiável do servidor do site, especifique uma conta de usuário.  

 Crie a conta com direitos limitados, a conta local no computador que executa o Microsoft SQL Server.  

> [!IMPORTANT]  
>  Não conceda direitos de entrada interativa a essa conta.  


### <a name="multicast-connection-account"></a>Conta de conexão multicast  

 Os pontos de distribuição habilitados para multicast usam a **Conta de conexão multicast** para ler as informações do banco de dados do site. O servidor usa sua conta de computador por padrão, mas você pode configurar uma conta de usuário em vez disso. Quando o banco de dados do site estiver em uma floresta não confiável, especifique uma conta de usuário. Por exemplo, se o data center tiver uma rede de perímetro em uma floresta diferente do servidor e do banco de dados do site, use essa conta para ler as informações multicast do banco de dados do site.  

 Se você precisar dessa conta, crie-a com direitos limitados, a conta local no computador que executa o Microsoft SQL Server.  

> [!IMPORTANT]  
>  Não conceda direitos de entrada interativa a essa conta.  

 Para mais informações, consulte [Usar o multicast para implantar o Windows pela rede](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network).


### <a name="network-access-account"></a>Conta de acesso à rede  

 Os computadores cliente usam a **conta de acesso à rede** quando não podem usar a conta do computador local para acessar conteúdo em pontos de distribuição. Isso se aplica principalmente a clientes do grupo de trabalho e computadores de domínios não confiáveis. Essa conta também é usada durante a implantação do sistema operacional, quando o computador que está instalando o sistema operacional ainda não tem uma conta de computador no domínio.  

> [!Important]  
>  A conta de acesso à rede nunca é usada com contexto de segurança para executar programas, instalar atualizações de software nem executar sequências de tarefas. Ela é usada somente para acessar recursos na rede.  

 Primeiro, um cliente do Configuration Manager tenta usar sua conta de computador para baixar o conteúdo. Se ele falhar, ele tentará automaticamente a conta de acesso à rede.  

 Da versão 1806 em diante, um grupo de trabalho ou um cliente ingressado no Azure AD pode acessar com segurança conteúdo dos pontos de distribuição sem precisar de uma conta de acesso à rede. Esse comportamento inclui cenários de implantação de sistema operacional com uma sequência de tarefas em execução no Centro de Software, PXE ou mídia de inicialização. Para obter mais informações, confira [HTTP aprimorado](/sccm/core/plan-design/hierarchy/enhanced-http).<!--1358228,1358278-->

 > [!Note]  
 > Se você habilitar **HTTP aprimorado** para não exigir a conta de acesso à rede, o ponto de distribuição precisará estar executando o Windows Server 2008 R2 SP1 ou posterior. <!--SCCMDocs-pr issue #2696-->
>  
> Atualize os clientes pelo menos para a versão 1806 antes de habilitar essa funcionalidade. Se você permitir apenas conexões **HTTP aprimoradas**, os clientes mais antigos não poderão se autenticar usando esse método, portanto, não será possível baixar o pacote de atualização de cliente de um ponto de distribuição. <!--vso2841213-->   

#### <a name="permissions"></a>Permissões

 Conceda a essa conta as permissões mínimas adequadas sobre o conteúdo que o cliente necessita para acessar o software. A conta deve ter o direito de **Acesso a este computador pela rede** no ponto de distribuição. Você pode configurar até 10 contas de acesso à rede por site.  

 Crie a conta em qualquer domínio que forneça o acesso necessário aos recursos. A conta de acesso à rede deve incluir sempre um nome de domínio. Não há suporte para segurança de passagem para essa conta. Se houver pontos de distribuição em vários domínios, crie a conta em um domínio confiável.  

> [!TIP]  
> Para evitar bloqueios de conta, não altere a senha em uma conta de acesso à rede existente. Em vez disso, crie uma nova conta e configure-a no Configuration Manager. Quando tiver passado tempo suficiente para que todos os clientes recebam os detalhes da nova conta, remova a conta antiga das pastas de rede compartilhadas e exclua-a.  

> [!IMPORTANT]  
>  Não conceda direitos de entrada interativa a essa conta.  
>   
>  Não conceda a essa conta o direito de ingressar computadores ao domínio. Se tiver de adicionar computadores ao domínio durante uma sequência de tarefas, use a [Conta de ingresso no domínio da sequência de tarefas](#task-sequence-domain-join-account).  

#### <a name="configure-the-network-access-account"></a>Configurar a conta de acesso à rede  

1.  No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**. Em seguida, selecione o site.  

2.  No grupo **Configurações** da faixa de opções, selecione **Configurar Componentes do Site** e escolha **Distribuição de Software**.  

3.  Clique na guia **Conta de acesso à rede**. Configure uma ou mais contas e clique em **OK**.  


### <a name="package-access-account"></a>Conta de acesso ao pacote  

 Uma **Conta de acesso ao pacote** permite configurar permissões NTFS para especificar usuários e grupos de usuários que podem acessar um conteúdo de pacote nos pontos de distribuição. Por padrão, o Configuration Manager concede acesso somente às contas de acesso genérico **Usuário** e **Administrador**. Você pode controlar o acesso a computadores cliente usando contas ou grupos do Windows adicionais. Os dispositivos móveis sempre recuperam o conteúdo do pacote anonimamente e, portanto, não usam uma conta de acesso a pacote.  

 Por padrão, quando o Configuration Manager copia os arquivos de conteúdo para um ponto de distribuição, ele concede acesso de **Leitura** ao grupo local **Usuários** e **Controle Total** ao grupo local **Administradores**. As permissões reais necessárias dependem do pacote. Se houver clientes em grupos de trabalho ou em florestas não confiáveis, os clientes usarão a conta de acesso à rede para acessar o conteúdo do pacote. Verifique se a conta de acesso à rede tem permissões para o pacote usando as contas de acesso ao pacote definidas.  

 Use contas em um domínio que possa acessar os pontos de distribuição. Se você criar ou modificar a conta depois de criar o pacote, deverá redistribuir o pacote. Atualizar o pacote não altera as permissões de NTFS no pacote.  

 Não é necessário adicionar a conta de acesso à rede como uma conta de acesso a pacote, pois a associação do grupo **Usuários** a adiciona automaticamente. Restringir a conta de acesso a pacote somente à conta de acesso à rede não impede que clientes acessem o pacote.  

#### <a name="manage-package-access-accounts"></a>Gerenciar contas de acesso a pacote  

1.  No console do Configuration Manager, escolha **Biblioteca de Software**.  

2.  No workspace **Biblioteca de software**, determine o tipo de conteúdo para o qual você deseja gerenciar as contas de acesso e siga as etapas fornecidas:  

    -   **Aplicativo**: expanda **Gerenciamento de Aplicativos**, escolha **Aplicativos** e selecione o aplicativo para o qual você quer gerenciar as contas de acesso.  

    -   **Pacote**: expanda **Gerenciamento de aplicativos**, clique em **Pacotes** e selecione o pacote para o qual você quer gerenciar as contas de acesso.  

    -   **Pacote de implantação de atualização de software**: expanda **Atualizações do Software**, clique em **Pacotes de Implantação** e selecione os pacotes de implantação para os quais você quer gerenciar as contas de acesso.  

    -   **Pacote de drivers**: expanda **Sistemas operacionais**, clique em **Pacotes de drivers** e selecione o pacote de drivers para o qual você quer gerenciar as contas de acesso.  

    -   **Imagem do sistema operacional**: expanda **Sistemas Operacionais**, escolha **Imagens do Sistema Operacional** e selecione as imagens do sistema operacional para as quais você quer gerenciar as contas de acesso.  

    -   **Pacote de atualização do sistema operacional**: expanda **Sistemas Operacionais**, escolha **Pacotes de atualização do sistema operacional** e, em seguida, selecione o pacote de atualização do sistema operacional para os quais você deseja gerenciar as contas de acesso.  

    -   **Imagem de inicialização**: expanda **Sistemas operacionais**, clique em **Imagens de inicialização** e selecione a imagem de inicialização para a qual você quer gerenciar as contas de acesso.  

3.  Clique com o botão direito no objeto selecionado e clique em **Gerenciar Contas de Acesso**.  

4.  Na caixa de diálogo **Adicionar Conta** , especifique o tipo de conta que receberá permissão de acesso ao conteúdo e os direitos de acesso associados à conta.  

    > [!NOTE]  
    >  Quando você adiciona um nome de usuário para a conta e o Configuration Manager encontra uma conta de usuário local e uma conta de usuário de domínio com esse nome, o Configuration Manager estabelece direitos de acesso para a conta de usuário de domínio.  


### <a name="reporting-services-point-account"></a>Conta do ponto do Reporting Services  
 
 O SQL Server Reporting Services usa a **Conta do ponto do Reporting Services** para recuperar os dados para relatórios do Configuration Manager do banco de dados do site. A conta e senha de usuário do Windows especificadas serão criptografadas e armazenadas no banco de dados do SQL Server Reporting Services.  

 > [!NOTE]  
 > A conta que você especifica deve ter permissões de **Logon local** no computador que hospeda o banco de dados do SQL Reporting Services.

 Para mais informações, confira [Introdução a relatórios](/sccm/core/servers/manage/introduction-to-reporting).


### <a name="remote-tools-permitted-viewer-accounts"></a>Contas do visualizador permitidas em ferramentas remotas  

 As contas que você especificar como **Visualizadores permitidos** para controle remoto representam uma lista de usuários que podem usar a funcionalidade de ferramentas remotas em clientes.  

Para obter mais informações, confira [Introdução ao controle remoto](/sccm/core/clients/manage/remote-control/introduction-to-remote-control).


### <a name="site-installation-account"></a>Conta de instalação do site
<!--SCCMDocs issue #572--> Use uma conta de usuário de domínio para entrar servidor em que você executa a instalação do Configuration Manager e instala um novo site.

Essa conta exige os seguintes direitos:  

- **Administrador** nos seguintes servidores:
    - Servidor do site  
    - Cada servidor que hospeda o banco de dados do site  
    - Cada instância do Provedor de SMS para o site  

- **Sysadmin** na instância do SQL Server que hospeda o banco de dados do site  

A configuração do Configuration Manager adiciona automaticamente essa conta ao grupo [Administradores de SMS](#sms-admins).

Após a instalação, essa conta é o único usuário com direitos para o console do Configuration Manager. Se você precisar remover essa conta, primeiro adicione seus direitos a outro usuário.

Ao expandir um site autônomo para incluir um site de administração central, essa conta requer os direitos baseados em função de **Administrador Completo** ou **Administrador de Infraestrutura** no site primário autônomo.


### <a name="site-system-installation-account"></a>Conta de instalação do sistema de sites  

 O servidor do site usa a **Conta de instalação de sistema de sites** para instalar, reinstalar, desinstalar e configurar sistemas de sites. Se você configurar o sistema de sites para exigir que o servidor do site inicie conexões a esse sistema, o Configuration Manager também usará essa conta para efetuar pull de dados do sistema de sites após a instalação do sistema de sites e quaisquer funções. Cada sistema de sites pode ter uma conta de instalação diferente, mas você pode configurar a conta de apenas uma instalação para gerenciar todas as funções de sistema de sites.  

 Essa conta requer permissões administrativas locais nos sistemas de sites de destino. Além disso, essa conta deve ter **Acesso a este computador pela rede** na política de segurança nos sistemas de sites de destino.  

 > [!TIP]  
 >  Se você tiver muitos controladores de domínio e essas contas forem usadas em vários domínios, antes de configurar o sistema de sites, verifique se o Active Directory replicou essas contas.  
 >   
 >  Quando você especifica uma conta local em cada sistema de sites a ser gerenciado, essa configuração é mais segura do que usar contas de domínio. Ela limita o dano que os invasores poderão causar se a conta for comprometida. No entanto, as contas de domínio são mais fáceis de gerenciar. Considere as compensações entre segurança e administração eficaz.  


### <a name="site-system-proxy-server-account"></a>Conta do servidor proxy do sistema de sites
<!--SCCMDocs issue #648--> As seguintes funções do sistema de sites usam a **Conta de servidor proxy do sistema de sites** para acessar a Internet por meio de um servidor proxy ou firewall que requer o acesso autenticado:

- Ponto de sincronização do Asset Intelligence
- Conector do Exchange Server
- Ponto de Conexão de Serviço
- Ponto de atualização de software

> [!IMPORTANT]  
>  Especifique uma conta que tenha menos permissões possíveis para o firewall ou servidor proxy necessário.  

 Para obter mais informações, confira [Suporte ao servidor proxy](/sccm/core/plan-design/network/proxy-server-support).


### <a name="smtp-server-connection-account"></a>Conta de conexão do servidor SMTP  

 O servidor do site usa a **Conta de conexão do servidor SMTP** para enviar alertas por email quando o servidor SMTP requer acesso autenticado.  

> [!IMPORTANT]  
>  Especifique uma conta que tenha o mínimo possível de permissões para enviar emails.  

 Para obter mais informações, veja [Usar alertas e o sistema de status](/sccm/core/servers/manage/use-alerts-and-the-status-system).


### <a name="software-update-point-connection-account"></a>Conta da conexão do ponto de atualização do software  

 O servidor do site usa a **Conta de conexão do ponto de atualização de software** para os dois serviços de atualização de software a seguir:  

-   O WSUS (Windows Server Update Services), que define configurações como definições de produto, classificações e configurações upstream.  

-   Gerenciador de Sincronização do WSUS, que requer a sincronização para um servidor do WSUS upstream ou o Microsoft Update.  

A [conta de instalação do sistema de sites](#site-system-installation-account) pode instalar componentes para atualizações de software, mas não pode executar funções específicas de atualização de software no ponto de atualização de software. Se não for possível usar a conta do computador do servidor do site para essa funcionalidade, porque o ponto de atualização de software está em uma floresta não confiável, você precisará especificar essa conta além da conta de instalação do sistema de sites.  

Essa conta deve ser um administrador local no computador em que você instala o WSUS. Também deve fazer parte do grupo local de **Administradores do WSUS**.  

Para obter mais informações, confira [Planejar atualizações de software](/sccm/sum/plan-design/plan-for-software-updates).


### <a name="source-site-account"></a>Conta do site de origem  

 O processo de migração usa a **Conta do site de origem** para acessar o Provedor de SMS do site de origem. Essa conta requer permissão de **Ler** para os objetos do site no site de origem para reunir dados para tarefas de migração.  

 Se você tiver pontos de distribuição do Configuration Manager 2007 ou sites secundários com pontos de distribuição colocalizados, ao atualizá-los para os pontos de distribuição do Configuration Manager (branch atual), essa conta também deverá ter permissões de **Excluir** para a classe **Site**. Essa permissão é para remover com êxito o ponto de distribuição do site do Configuration Manager 2007 durante a atualização.  

> [!NOTE]  
>  A conta de site de origem e a [conta de banco de dados do site de origem](#source-site-database-account) são identificadas como **Gerenciador de Migração** no nó **Contas** do workspace **Administração** no console do Configuration Manager.  

 Para saber mais, confira [Migrar dados entre hierarquias](https://docs.microsoft.com/en-us/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="source-site-database-account"></a>Conta do banco de dados do site de origem  

 O processo de migração usa a **Conta do banco de dados do site de origem** para acessar o banco de dados do SQL Server do site de origem. Para reunir dados do banco de dados do SQL Server do site de origem, a conta de banco de dados do site de origem deve ter permissões de **Ler** e **Executar** para o banco de dados do SQL Server do site de origem.  

 Se você usar a conta de computador do Configuration Manager (branch atual), verifique se todos os itens a seguir são verdadeiros para essa conta:  
   
 - Ela é um membro do grupo de segurança **Usuários COM Distribuídos** no mesmo domínio que o site do Configuration Manager 2007  
 - Ela é um membro do grupo de segurança **Administradores de SMS**  
 - Ela tem permissão de **Ler** para todos os objetos do Configuration Manager 2007  

> [!NOTE]  
>  A conta de site de origem e a [conta de banco de dados do site de origem](#source-site-database-account) são identificadas como **Gerenciador de Migração** no nó **Contas** do workspace **Administração** no console do Configuration Manager.  

 Para saber mais, confira [Migrar dados entre hierarquias](https://docs.microsoft.com/en-us/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="task-sequence-domain-join-account"></a>Conta de ingresso no domínio de sequência de tarefas 

 A Instalação do Windows usa a **Conta de ingresso no domínio de sequência de tarefas** para ingressar um computador com uma imagem criada recentemente em um domínio. Essa conta é exibida pela etapa de sequência de tarefas do [Grupo de Trabalho ou Domínio de Ingresso](/sccm/osd/understand/task-sequence-steps#BKMK_JoinDomainorWorkgroup) com a opção **Ingressar em domínio**. Essa conta também pode ser configurada com a etapa [Aplicar configurações de rede](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyNetworkSettings), mas isso não é necessário.  

 Essa conta requer o direito de **Ingresso no Domínio** no domínio de destino.  

> [!TIP]  
>  Crie uma conta de usuário de domínio com as permissões mínimas para ingressar no domínio e use-a para todas as sequências de tarefas.  

> [!IMPORTANT]  
>  Não atribua permissões de entrada interativa a essa conta.  
>   
>  Não use a conta de acesso à rede para essa conta.  


### <a name="task-sequence-network-folder-connection-account"></a>Conta de conexão de pasta de rede da sequência de tarefas  

 O mecanismo de sequência de tarefas usa a **Conta de conexão da pasta de rede de sequência de tarefas** para conectar-se a uma pasta compartilhada na rede. Essa conta é necessária para a etapa da sequência de tarefas de [Conectar-se à Pasta de Rede](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder).  

 Essa conta requer permissões para acessar a pasta compartilhada especificada. Deve ser uma conta de usuário de domínio.  

> [!TIP]  
>  Crie uma conta de usuário de domínio com permissões mínimas para acessar os recursos de rede necessários e usá-los em todas as sequências de tarefas.  

> [!IMPORTANT]  
>  Não atribua permissões de entrada interativa a essa conta.  
>   
>  Não use a conta de acesso à rede para essa conta.  


### <a name="task-sequence-run-as-account"></a>Execução da sequência de tarefas como conta  

 O mecanismo de sequência de tarefas usa **Execução da sequência de tarefas como conta** para executar linhas de comando com credenciais diferentes da conta do Sistema Local. Essa conta é exigida pela etapa de sequência de tarefas [Executar Linha de Comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) com a opção **Executar esta etapa como a seguinte conta**.  

 Configure a conta para ter as permissões mínimas necessárias para executar a linha de comando especificada na sequência de tarefas. A conta requer direitos de entrada interativa. Isso geralmente requer a capacidade de instalar software e acessar recursos de rede.  

> [!IMPORTANT]  
>  Não use a conta de acesso à rede para essa conta.  
>   
>  Nunca faça da conta um administrador de domínio.  
>   
>  Nunca configure perfis móveis para esta conta. Quando a sequência de tarefas é executada, ela baixa o perfil móvel da conta. Isso deixa o perfil vulnerável ao acesso no computador local.  
>   
>  Limite o escopo da conta. Por exemplo, crie outra sequência de tarefas executada como contas para cada sequência de tarefas. Então, se uma conta for comprometida, somente os computadores cliente aos quais a conta tem acesso serão comprometidos.  
>   
>  Se a linha de comando exigir acesso administrativo no computador, considere a criação de uma conta do administrador local exclusivamente para essa conta em todos os computadores que executam a sequência de tarefas. Exclua a conta depois que você não precisar mais dela.  

