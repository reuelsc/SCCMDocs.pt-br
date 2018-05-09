---
title: Contas usadas
titleSuffix: Configuraton Manager
description: Identifique e gerencie grupos e contas do Windows no System Center Configuration Manager.
ms.date: 2/9/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b2ca81115207db66a39d2aeb5e07740ae259d54c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="accounts-used-in-system-center-configuration-manager"></a>Contas usadas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as seguintes informações para identificar os grupos e as contas do Windows usados no System Center Configuration Manager, como são usados e quais são os requisitos.  

## <a name="windows-groups-that-configuration-manager-creates-and-uses"></a>Grupos do Windows que o Configuration Manager cria e usa  
 O Configuration Manager cria automaticamente e, em muitos casos, mantém automaticamente os seguintes grupos do Windows:  

> [!NOTE]  
>  Quando o Configuration Manager cria um grupo em um computador que é membro do domínio, trata-se de um grupo de segurança local. Quando o computador é um controlador de domínio, trata-se de um grupo de domínio local compartilhado entre todos os controladores de domínio no domínio.  


### <a name="configmgrcollectedfilesaccess"></a>ConfigMgr_CollectedFilesAccess  
O Configuration Manager usa esse grupo para conceder acesso para exibir arquivos coletados pelo inventário de software.  

A tabela a seguir lista os detalhes adicionais desse grupo:  

|Detalhes|Mais informações|  
|------------|----------------------|  
|Tipo e local|Esse é um grupo de segurança local criado no servidor do site primário.<br /><br /> Quando um site é desinstalado, esse grupo não é removido automaticamente. Ele deve ser excluído manualmente.|  
|Associação|O Configuration Manager gerencia automaticamente a associação ao grupo. A associação inclui usuários administrativos que recebem a permissão **Exibir Arquivos Coletados** para o objeto protegível **Coleção** de uma função de segurança atribuída.|  
|Permissões|Por padrão, este grupo tem a permissão **Read** para a seguinte pasta no servidor do site: **%path%\Microsoft Configuration Manager\sinv.box\FileCol**.|  

### <a name="configmgrdviewaccess"></a>ConfigMgr_DViewAccess  
 Esse grupo é um grupo de segurança local criado no servidor de banco de dados do site ou no servidor de réplica de banco de dados pelo Configuration Manager. Ele não está sendo usado, mas está reservado para uso futuro.  

### <a name="configmgr-remote-control-users"></a>Usuários de Controle Remoto do ConfigMgr  
 As ferramentas remotas do Configuration Manager usam esse grupo para armazenar as contas e os grupos configurados na lista de Visualizadores Permitidos, atribuídos a cada cliente.  

 A tabela a seguir lista os detalhes adicionais desse grupo:  

|Detalhes|Mais informações|  
|------------|----------------------|  
|Tipo e local|Esse é um grupo de segurança local criado no cliente do Configuration Manager quando o cliente recebe uma política que habilita as ferramentas remotas.<br /><br /> Depois de desabilitar as ferramentas remotas para um cliente, esse grupo não é removido automaticamente. Ele deve ser excluído manualmente de cada computador cliente.|  
|Associação|Por padrão, não existem membros nesse grupo. Ao adicionar usuários à lista Visualizadores Permitidos, eles são adicionados automaticamente a esse grupo.<br /><br /> Você pode usar a lista Visualizadores Permitidos para gerenciar a associação desse grupo em vez de adicionar usuários ou grupos diretamente a ele.<br /><br /> Além de ser visualizador permitido, um usuário administrativo deve ter a permissão **Controle Remoto** para o objeto **Coleção**. É possível atribuir essa permissão usando a função de segurança Operador de Ferramentas Remoto.|  
|Permissões|Por padrão, esse grupo não tem permissões para qualquer local no computador. Ele é usado apenas para armazenar a lista de Visualizadores Permitidos.|  

### <a name="sms-admins"></a>Administradores de SMS  
 O Configuration Manager usa esse grupo para conceder acesso ao Provedor de SMS por meio do WMI (Windows Management Instrumentation). O acesso ao Provedor de SMS é necessário para exibir e alterar objetos no console do Configuration Manager.  

> [!NOTE]  
>  A configuração da administração baseada em funções de um usuário administrativo determina quais objetos eles podem exibir e gerenciar quando usam o console do Configuration Manager.  

 A tabela a seguir lista os detalhes adicionais desse grupo:  

|Detalhes|Mais informações|  
|------------|----------------------|  
|Tipo e local|Esse é um grupo de segurança local criado em cada computador que possui um Provedor de SMS.<br /><br /> Quando um site é desinstalado, esse grupo não é removido automaticamente. Ele deve ser excluído manualmente.|  
|Associação|O Configuration Manager gerencia automaticamente a associação ao grupo. Por padrão, cada usuário administrativo em uma hierarquia e a conta de computador do servidor do site são membros do grupo Administradores de SMS em cada computador do Provedor de SMS de um site.|  
|Permissões|Os direitos e as permissões de administradores de SMS são definidos no snap-in do MMC do Controle WMI. Por padrão, o grupo de Administradores de SMS recebe **Enable Account** e **Remote Enable** sobre o namespace Raiz\SMS. Os Usuários Autenticados têm as permissões **Execute Methods**, **Provider Write**e **Enable Account**.<br /><br /> Os usuários administrativos que usarão um console remoto do Configuration Manager também precisam de permissões DCOM para Ativação Remota no computador do servidor do site e no computador do Provedor de SMS. É uma prática recomendada conceder esses direitos a Administradores de SMS para simplificar a administração em vez de conceder esses direitos diretamente a usuários ou grupos. Para obter mais informações, consulte a seção [Configurar permissões DCOM para consoles remotos do Configuration Manager](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole) no artigo [Modificar sua infraestrutura do System Center Configuration Manager](../../../core/servers/manage/modify-your-infrastructure.md).|  

### <a name="smssitesystemtositeserverconnectionmpltsitecode"></a>SMS_SiteSystemToSiteServerConnection_MP_&lt;sitecode\>  
 Os pontos de gerenciamento do Configuration Manager que são remotos com relação ao servidor do site usam esse grupo para conexão com o banco de dados do site. Esse grupo fornece a um ponto de gerenciamento acesso a pastas da caixa de entrada no servidor do site e ao banco de dados do site.  

 A tabela a seguir lista os detalhes adicionais desse grupo:  

|Detalhes|Mais informações|  
|------------|----------------------|  
|Tipo e local|Esse é um grupo de segurança local criado em cada computador que possui um Provedor de SMS.<br /><br /> Quando um site é desinstalado, esse grupo não é removido automaticamente. Ele deve ser excluído manualmente.|  
|Associação|O Configuration Manager gerencia automaticamente a associação ao grupo. Por padrão, a associação inclui as contas de computadores remotos que têm um ponto de gerenciamento para o site.|  
|Permissões|Por padrão, esse grupo tem as permissões **Ler**, **Ler e executar** e **Listar conteúdo da pasta** para a pasta **%path%\Microsoft Configuration Manager\inboxes** no servidor do site. Esse grupo tem a permissão adicional **Write** para subpastas abaixo da pasta **inboxes** nas quais o ponto de gerenciamento grava dados do cliente.|  

### <a name="smssitesystemtositeserverconnectionsmsprovltsitecode"></a>SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;sitecode\>  
 Os computadores do Provedor de SMS do Configuration Manager que são remotos com relação ao servidor do site usam esse grupo para conexão com o servidor do site.  

 A tabela a seguir lista os detalhes adicionais desse grupo:  

|Detalhes|Mais informações|  
|------------|----------------------|  
|Tipo e local|Esse é um grupo de segurança local criado no servidor do site.<br /><br /> Quando um site é desinstalado, esse grupo não é removido automaticamente. Ele deve ser excluído manualmente.|  
|Associação|O Configuration Manager gerencia automaticamente a associação ao grupo. Por padrão, a associação inclui a conta de computador ou a conta de usuário do domínio que é usada para conexão ao servidor do site por meio de cada computador remoto que tem um Provedor de SMS instalado para o site.|  
|Permissões|Por padrão, esse grupo tem as permissões **Ler**, **Ler e executar** e **Listar conteúdo da pasta** para a pasta **%path%\Microsoft Configuration Manager\inboxes** no servidor do site. Esse grupo tem a permissão adicional **Gravação** ou as permissões de **Gravação** e **Modificação** para subpastas abaixo da pasta **inboxes** às quais o Provedor de SMS precisa de acesso.<br /><br /> Esse grupo também tem as permissões **Ler**, **Ler e executar**, **Listar conteúdo da pasta**, **Gravar** e **Modificar** para as pastas abaixo de **%path%\Microsoft Configuration Manager\OSD\boot** e a permissão **Ler** para as pastas abaixo de **%path%\Microsoft Configuration Manager\OSD\Bin** no servidor do site.|  

### <a name="smssitesystemtositeserverconnectionstatltsitecode"></a>SMS_SiteSystemToSiteServerConnection_Stat_&lt;sitecode\>  
 O Gerenciador de Expedição de Arquivo nos computadores do sistema de site remoto do Configuration Manager usa este grupo para se conectar ao servidor do site.  

 A tabela a seguir lista os detalhes adicionais desse grupo:  

|Detalhes|Mais informações|  
|------------|----------------------|  
|Tipo e local|Esse é um grupo de segurança local criado no servidor do site.<br /><br /> Quando um site é desinstalado, esse grupo não é removido automaticamente. Ele deve ser excluído manualmente.|  
|Associação|O Configuration Manager gerencia automaticamente a associação ao grupo. Por padrão, a associação inclui a conta de computador ou a conta de usuário do domínio usada para conexão ao servidor do site por meio de cada computador do sistema de site remoto que executa o Gerenciador de Expedição de Arquivos.|  
|Permissões|Por padrão, esse grupo tem as permissões **Ler**, **Ler e executar** e **Listar conteúdo da pasta** para a pasta **%path%\Microsoft Configuration Manager\inboxes** e subpastas abaixo desse local no servidor do site. Esse grupo tem as permissões adicionais **Gravar** e **Modificar** para a pasta **%path%\Microsoft Configuration Manager\inboxes\statmgr.box** no servidor do site.|  

### <a name="smssitetositeconnectionltsitecode"></a>SMS_SiteToSiteConnection_&lt;sitecode\>  
 O Configuration Manager usa esse grupo para permitir a replicação baseada em arquivos entre sites em uma hierarquia. Para cada site remoto que transfere arquivos diretamente para esse site, esse grupo tem contas configuradas como uma **Conta de Replicação de Arquivo**.  

 A tabela a seguir lista os detalhes adicionais desse grupo:  

|Detalhes|Mais informações|  
|------------|----------------------|  
|Tipo e local|Esse é um grupo de segurança local criado no servidor do site.|  
|Associação|Quando você instala um novo site como filho de outro site, o Configuration Manager adiciona automaticamente a conta de computador do novo site ao grupo no servidor do site pai. O Configuration Manager também adiciona a conta do computador do site pai ao grupo no novo servidor do site. Se outra conta for especificada para transferências baseadas em arquivo, adicione essa conta a esse grupo no servidor do site de destino.<br /><br /> Quando um site é desinstalado, esse grupo não é removido automaticamente. Ele deve ser excluído manualmente.|  
|Permissões|Por padrão, esse grupo tem **controle total** na pasta **%path%\Microsoft Configuration Manager\inboxes\despoolr.box\receive** .|  

## <a name="accounts-that-configuration-manager-uses"></a>Contas que o Configuration Manager usa  
 É possível configurar as seguintes contas para o Configuration Manager.  

### <a name="active-directory-group-discovery-account"></a>Conta de Descoberta de Grupos do Active Directory  
 A **Conta de Descoberta de Grupos do Active Directory** é usada para descobrir grupos de segurança locais, globais e universais, a associação nesses grupos e a associação em grupos de distribuição dos locais especificados no Active Directory Domain Services. Grupos de distribuição não são descobertos como recursos de grupo.  

 Essa conta pode ser uma conta de computador do servidor do site que executa a descoberta, ou uma conta de usuário do Windows. Deve ter permissão de acesso **Ler** nos locais do Active Directory especificados para descoberta.  

### <a name="active-directory-system-discovery-account"></a>Conta de Descoberta de Sistemas do Active Directory  
 A **Conta de Descoberta de Sistemas do Active Directory** é usada para descobrir computadores nos locais especificados em Serviços de Domínio Active Directory.  

 Essa conta pode ser uma conta de computador do servidor do site que executa a descoberta, ou uma conta de usuário do Windows. Deve ter permissão de acesso **Ler** nos locais do Active Directory especificados para descoberta.  

### <a name="active-directory-user-discovery-account"></a>Conta de Descoberta de Usuários do Active Directory  
 A **Conta de Descoberta de Usuários do Active Directory** é usada para descobrir contas de usuário nos locais especificados em Serviços de Domínio Active Directory.  

 Essa conta pode ser uma conta de computador do servidor do site que executa a descoberta, ou uma conta de usuário do Windows. Deve ter permissão de acesso **Ler** nos locais do Active Directory especificados para descoberta.  

### <a name="active-directory-forest-account"></a>Conta da Floresta do Active Directory  
 A **Conta de Floresta do Active Directory** é usada para descobrir a infraestrutura de rede em florestas do Active Directory. Os sites de administração central e sites primários também o usam para publicar dados do site no Active Directory Domain Services para uma floresta.  

> [!NOTE]  
>  Sites secundários usam sempre a conta de computador do servidor do site secundário para publicar no Active Directory.  

> [!NOTE]  
>  A Conta da Floresta do Active Directory deve ser uma conta global para descobrir e publicar em florestas não confiáveis. Se você não usar a conta de computador do servidor do site, será possível selecionar somente uma conta global.  

 Essa conta deve ter a permissão **Ler** em cada floresta do Active Directory de onde você deseja descobrir a infraestrutura de rede.  

 Essa conta deve ter a permissão **Controle Total** no contêiner Gerenciamento do Sistema e todos os seus objetos filho em cada floresta do Active Directory onde você deseja publicar dados do site.  

### <a name="asset-intelligence-synchronization-point-proxy-server-account"></a>Conta do Servidor Proxy do Ponto de Sincronização do Asset Intelligence  
 O ponto de sincronização do Asset Intelligence usa a **Conta do Servidor Proxy do Ponto de Sincronização do Asset Intelligence** para acessar a Internet através de um servidor proxy ou de firewall que exige acesso autenticado.  

> [!IMPORTANT]  
>  Especifique uma conta que tenha menos permissões possíveis para o firewall ou servidor proxy necessário.  

### <a name="certificate-registration-point-account"></a>Conta do ponto de registro de certificado  
 A **Conta do Ponto de Registro de Certificado** conecta o ponto de registro do certificado ao banco de dados do Configuration Manager. A conta de computador do servidor de ponto de registro de certificado é usada por padrão, porém, você pode em vez disso configurar uma conta de usuário. Você deve especificar uma conta de usuário sempre que o ponto de registro de certificado estiver em um domínio não confiável do servidor do site. Essa conta requer acesso somente de **Leitura** ao banco de dados do site, pois operações de gravação são administradas pelo sistema de mensagem de estado.  

### <a name="capture-operating-system-image-account"></a>Capturar Conta de Imagem do Sistema Operacional  
 O Configuration Manager usa a **Conta Capturar Imagem do Sistema Operacional** para acessar a pasta na qual as imagens capturadas são armazenadas quando você implanta sistemas operacionais. Essa conta será necessária se você adicionar a etapa **Capturar Imagem do Sistema Operacional** a uma sequência de tarefas.  

 A conta deve ter permissões de **Leitura** e **Gravação** no compartilhamento de rede onde a imagem capturada é armazenada.  

 Se a senha da conta for alterada no Windows, você deverá atualizar a sequência das tarefas com a nova senha. O cliente do Configuration Manager recebe a nova senha quando baixa a política do cliente.  

 Se você usar essa conta, poderá criar uma conta de usuário de domínio com permissões mínimas para acessar os recursos de rede necessários e usá-los em todas as contas de sequência de tarefas.  

> [!IMPORTANT]  
>  Não atribua permissões de logon interativo a essa conta.  
>   
>  Não use a Conta de Acesso à Rede para essa conta.  

### <a name="client-push-installation-account"></a>Conta de Instalação do Cliente por Push  
 A **Conta de Instalação do Cliente por Push** será usada para conexão com os computadores e instalação do software cliente do Configuration Manager se você implantar clientes usando instalação do cliente por push. Se essa conta não for especificada, a conta do servidor do site será usada para tentar instalar o software do cliente.  

 Essa conta deve ser membro do grupo local de **Administradores** nos computadores em que o software cliente do Configuration Manager será instalado. Essa conta não exige direitos de **Administrador de Domínio**.  

 Você pode especificar uma ou mais Contas de Instalação do Cliente por Push, as quais o Configuration Manager tentará sucessivamente até obter êxito.  

> [!TIP]  
>  Para coordenar mais eficazmente as atualizações de conta em grandes implantações do Active Directory, crie uma nova conta com um nome diferente e adicione a nova conta à lista de Contas de Instalação do Cliente por Push no Configuration Manager. Permita tempo suficiente para que o Active Directory Domain Services replique a nova conta, e depois remova a conta antiga do Configuration Manager e do Active Directory Domain Services.  

> [!IMPORTANT]  
>  Não conceda a essa conta o direito de fazer logon localmente.  

### <a name="enrollment-point-connection-account"></a>Conta de Conexão do Ponto de Registro  
 A **Conta de Conexão do Ponto de Registro** conecta o ponto de registro ao banco de dados do Configuration Manager. A conta de computador do ponto de registro é usada por padrão, mas você pode configurar uma conta de usuário, em vez disso. Você deve especificar uma conta de usuário sempre que o ponto de registro estiver em um domínio não confiável do servidor do site. Essa conta requer acesso de **Leitura** e **Gravação** ao banco de dados do site.  

### <a name="exchange-server-connection-account"></a>Conta de Conexão do Exchange Server  
 A **Conta de Conexão do Exchange Server** conecta o servidor do site ao computador do Exchange Server especificado para encontrar e gerenciar dispositivos móveis que se conectam ao Exchange Server. Essa conta requer cmdlets do Exchange PowerShell que fornecem as permissões necessárias para o computador do Exchange Server. Para obter mais informações sobre os cmdlets, veja [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="exchange-server-connector-proxy-server-account"></a>Conta de Servidor Proxy do Conector do Exchange Server  
 O conector do Exchange Server usa a **Conta de Servidor Proxy do Conector do Exchange Server** para acessar a Internet através de um servidor proxy ou de firewall que requer acesso autenticado.  

> [!IMPORTANT]  
>  Especifique uma conta que tenha menos permissões possíveis para o firewall ou servidor proxy necessário.  

### <a name="management-point-connection-account"></a>Conta de conexão do ponto de gerenciamento  
 A **Conta de Conexão do Ponto de Gerenciamento** é usada para conectar o ponto de gerenciamento ao banco de dados do site do Configuration Manager para que ele possa enviar e recuperar informações para os clientes. A conta de computador do ponto de gerenciamento é usada por padrão, mas você pode configurar uma conta de usuário, em vez disso. Você deve especificar uma conta de usuário sempre que o ponto de gerenciamento estiver em um domínio não confiável do servidor do site.  

 Crie a conta com direitos limitados, a conta local no computador que executa o Microsoft SQL Server.  

> [!IMPORTANT]  
>  Não conceda direitos de logon interativo a essa conta.  

### <a name="multicast-connection-account"></a>Conta de Conexão Multicast  
 Os pontos de distribuição configurados para multicast usam a **Conta de Conexão Multicast** para ler as informações do banco de dados do site. Por padrão, a conta do computador do ponto de distribuição é usada, mas você pode configurar uma conta de usuário, em vez disso. Você deve especificar uma conta de usuário sempre que o banco de dados do site estiver em uma floresta não confiável. Por exemplo, se o seu centro de dados tiver uma rede de perímetro em uma floresta diferente do servidor e do banco de dados do site, você poderá usar essa conta para ler as informações multicast do banco de dados do site.  

 Se você criar essa conta, crie-a com direitos limitados, a conta local no computador que executa o Microsoft SQL Server.  

> [!IMPORTANT]  
>  Não conceda direitos de logon interativo a essa conta.  

### <a name="network-access-account"></a>Conta de Acesso à Rede  
 Os computadores cliente usam a **Conta de Acesso à Rede** quando não podem usar a conta do computador local para acessar conteúdo em pontos de distribuição. Por exemplo, isso se aplica a clientes do grupo de trabalho e computadores de domínios não confiáveis. Essa conta também pode ser usada durante a implantação do sistema operacional quando o computador que está instalando o sistema operacional ainda não tem uma conta de computador no domínio.  

> [!NOTE]  
>  A Conta de Acesso à Rede nunca é usada com contexto de segurança para executar programas, instalar atualizações de software nem executar sequências de tarefas. Ela é usada somente para acessar recursos na rede.  

 Conceda a essa conta as permissões mínimas adequadas sobre o conteúdo que o cliente necessita para acessar o software. A conta deve ter o direito de **Acesso a este computador pela rede** no ponto de distribuição ou em outro servidor que contém o conteúdo do pacote. Você pode configurar até 10 contas de acesso de rede por site.  

> [!WARNING]  
>  Quando Configuration Manager tenta usar a conta computername$ para baixar conteúdo e falha, ele tenta automaticamente a Conta de Acesso à Rede novamente, mesmo que já tenha tentado e falhado.  

 Crie a conta em qualquer domínio que forneça o acesso necessário aos recursos. A conta de acesso à rede deve incluir sempre um nome de domínio. Não há suporte para segurança de passagem para essa conta. Se houver pontos de distribuição em vários domínios, crie a conta em um domínio confiável.  

> [!TIP]  
>  Para evitar bloqueios de conta, não altere a senha em uma conta de acesso à rede existente. Em vez disso, crie uma nova conta e configure-a no Configuration Manager. Quando tiver passado tempo suficiente para que todos os clientes recebam os detalhes da nova conta, remova a conta antiga das pastas de rede compartilhadas e exclua-a.  

> [!IMPORTANT]  
>  Não conceda direitos de logon interativo a essa conta.
>   
>  Não conceda a essa conta o direito de ingressar computadores ao domínio. Se tiver de adicionar computadores ao domínio durante uma sequência de tarefas, use a Conta de Adição de Domínio do Editor de Sequência de Tarefas.  

### <a name="package-access-account"></a>Conta de Acesso ao Pacote  
 Uma **Conta de Acesso ao Pacote** permite configurar permissões NTFS para especificar usuários e grupos de usuários que podem acessar uma pasta de pacote nos pontos de distribuição. Por padrão, o Configuration Manager concede acesso somente a contas de **Usuários** e **Administradores** genéricas. Você pode controlar o acesso a computadores cliente usando contas ou grupos do Windows adicionais. Os dispositivos móveis sempre recuperam o conteúdo do pacote anonimamente e, portanto, não usam as Contas de Acesso ao Pacote.  

 Por padrão, quando o Configuration Manager cria o compartilhamento de pacotes em um ponto de distribuição, ele concede acesso de **Leitura** ao grupo local de **Usuários** e **Controle Total** ao grupo local de **Administradores**. As permissões reais necessárias dependerão do pacote. Se houver clientes em grupos de trabalho ou em florestas não confiáveis, os clientes usarão a Conta de Acesso à Rede para acessar o conteúdo do pacote. Verifique se a Conta de Acesso à Rede tem permissões para o pacote usando as Contas de Acesso ao Pacote definidas.  

 Use contas em um domínio que possa acessar os pontos de distribuição. Se você criar ou alterar a conta após a criação do pacote, deverá redistribuir o pacote. A atualização do pacote não altera as permissões de NTFS no pacote.  

 Não é necessário adicionar a Conta de Acesso à Rede como uma Conta de Acesso de Pacote, pois a associação do grupo Usuários a adiciona automaticamente. Restringir a Conta de Acesso de Pacote somente à Conta de Acesso à Rede não impede que clientes acessem o pacote.  

### <a name="reporting-services-point-account"></a>Conta do ponto do Reporting Services  
 O SQL Server Reporting Services usa a **Conta do Ponto do Reporting Services** para recuperar os dados para relatórios do Configuration Manager do banco de dados do site. A conta e senha de usuário do Windows especificadas serão criptografadas e armazenadas no banco de dados do SQL Server Reporting Services.  
>[!NOTE]
>A conta que você especifica deve ter permissões de Logon Local no computador que hospeda o banco de dados do Reporting Services.

### <a name="remote-tools-permitted-viewer-accounts"></a>Contas do visualizador permitidas em ferramentas remotas  
 As contas que você especificar como **Visualizadores permitidos** para controle remoto representam uma lista de usuários que podem usar a funcionalidade de ferramentas remotas em clientes.  

### <a name="site-system-installation-account"></a>Conta de instalação do sistema de site  
 O servidor do site usa a **Conta de Instalação de Sistema de Site** para instalar, reinstalar, desinstalar e configurar sistemas de site. Se você configurar o sistema de sites para exigir que o servidor do site inicie conexões a esse sistema, o Configuration Manager também usará essa conta para efetuar pull de dados do computador do sistema do sites, após esta e outras funções do sistema do sites forem instaladas. Cada sistema de site pode ter uma Conta de Instalação de Sistema de Site diferente, mas é possível configurar somente uma para gerenciar todas as funções nesse sistema de site.  

 Essa conta requer permissões administrativas locais nos sistemas dos sites que forem instalados e configurados por administradores. Além disso, essa conta precisa ter **Acesso a este computador pela rede** na política de segurança nos sistemas dos sites que forem instalados e configurados por administradores.  

> [!TIP]  
>  Se você tiver muitos controladores de domínio e estas contas forem usadas em vários domínios, verifique se as contas foram replicadas antes de configurar o sistema de sites.  
>   
>  Quando você especifica uma conta local em cada sistema de site a ser gerenciado, esta configuração é mais segura do que se usar contas de domínio, porque ela limita os danos de invasores podem fazer se a conta for comprometida. No entanto, as contas de domínio são mais fáceis de gerenciar. Considere as compensações entre segurança e administração eficaz.  

### <a name="smtp-server-connection-account"></a>Conta de conexão do servidor SMTP  
 O servidor do site usa a **Conta de Conexão do Servidor SMTP** para enviar alertas de email quando o servidor SMTP requer acesso autenticado.  

> [!IMPORTANT]  
>  Especifique uma conta que tenha o mínimo possível de permissões para enviar emails.  

### <a name="software-update-point-connection-account"></a>Conta da conexão do ponto de atualização do software  
 O servidor do site usa a **Conta de Conexão do Ponto de Atualização de Software** para os dois serviços de atualizações de software a seguir:  

-   O Configuration Manager do WSUS, que define configurações como de upstream, classificações e definições de produto.  

-   Gerenciador de Sincronização do WSUS, que requer a sincronização para um servidor do WSUS upstream ou o Microsoft Update.  

A Conta de Instalação de Sistema de Site pode instalar componentes para atualizações de software, mas não pode executar funções específicas de atualizações de software no ponto de atualização de software. Se não é possível utilizar a conta do computador do servidor do site para essa funcionalidade, porque o ponto de atualização de software está em uma floresta não confiável, você deve especificar essa conta além da Conta de Instalação de Sistema de Site.  

Essa conta deve ser de um administrador local no computador onde o WSUS está instalado. Ele também deve fazer parte do grupo local de Administradores do WSUS.  

### <a name="software-update-point-proxy-server-account"></a>Conta do servidor proxy do ponto de atualização do software  
 O ponto de atualização de software usa a **Conta do Servidor Proxy do Ponto de Atualização de Software** para acessar a Internet através de um servidor proxy ou de firewall que requer acesso autenticado.  

> [!IMPORTANT]  
>  Especifique uma conta que tenha menos permissões possíveis para o firewall ou servidor proxy necessário.  

### <a name="source-site-account"></a>Conta do site de origem  
 O processo de migração usa a **Conta do Site de Origem** para acessar o Provedor de SMS do site de origem. Essa conta requer permissão de **Ler** para os objetos do site no site de origem para reunir dados para tarefas de migração.  

 Se você atualizar pontos de distribuição ou sites secundários do Configuration Manager 2007 que têm pontos de distribuição colocalizados para pontos de distribuição do System Center Configuration Manager, essa conta também deverá ter permissões de **Excluir** para a classe do **Site** para remover com êxito o ponto de distribuição do site do Configuration Manager 2007 durante a atualização.  

> [!NOTE]  
>  A Conta de Site de Origem e a Conta de Banco de Dados do Site de Origem são identificadas como **Gerenciador de Migração** no nó **Contas** do espaço de trabalho **Administração** no console do Configuration Manager.  

### <a name="source-site-database-account"></a>Conta do banco de dados do site de origem  
 O processo de migração usa a **Conta do Banco de Dados do Site de Origem** para acessar o banco de dados do SQL Server do site de origem. Para reunir dados do banco de dados do SQL Server do site de origem, a Conta de Banco de Dados do Site de origem deve ter permissões de **Ler** e **Executar** para o banco de dados do SQL Server do site de origem.  

> [!NOTE]  
>  Se você usar a conta do computador do System Center Configuration Manager, verifique se as condições a seguir são verdadeiras para essa conta:  
>   
> -   É um membro do grupo de segurança **Distributed COM – Usuários** no domínio no qual o site do Configuration Manager 2007 reside.  
> -   Ele é um membro do grupo de segurança **Administradores de SMS** .  
> -   Ele tem a permissão de **Leitura** para todos os objetos do Configuration Manager 2007.  

> [!NOTE]  
>  A Conta de Site de Origem e a Conta de Banco de Dados do Site de Origem são identificadas como **Gerenciador de Migração** no nó **Contas** do espaço de trabalho **Administração** no console do Configuration Manager.  

### <a name="task-sequence-editor-domain-joining-account"></a>Conta de junção de domínio de editor de sequência de tarefas  
 A **Conta de Junção de Domínio de Editor de Sequência de Tarefas** é usada em uma sequência de tarefas para ingressar um novo computador de imagem em um domínio. Essa conta é necessária se você adicionar a etapa **Ingressar no Domínio ou Grupo de Trabalho** a uma sequência de tarefas e selecionar **Ingressar em um domínio**. Essa conta também pode ser configurada se você adicionar a etapa **Aplicar Configurações de Rede** a uma sequência de tarefas, mas isso não é necessário.  

 Essa conta requer o direito de **Ingresso no Domínio** no domínio em que o computador está ingressando.  

> [!TIP]  
>  Se você precisar dessa conta para suas sequências de tarefas, poderá criar uma conta de usuário de domínio com permissões mínimas para acessar os recursos de rede necessários e usá-los em todas as contas da sequência de tarefas.  

> [!IMPORTANT]  
>  Não atribua permissões de logon interativo a essa conta.  
>   
>  Não use a Conta de Acesso à Rede para essa conta.  

### <a name="task-sequence-editor-network-folder-connection-account"></a>Conta de conexão de pasta de rede do editor de sequência de tarefas  
 Uma sequência de tarefas usa a **Conta de Conexão de Pasta de Rede do Editor de Sequência de Tarefas** para conectar-se a uma pasta compartilhada na rede. Essa conta é necessária se você adicionar a etapa **Conectar à Pasta de Rede** a uma sequência de tarefas.  

 Essa conta requer permissões para acessar a pasta compartilhada especificada. Ela também deve ser uma conta de domínio.  

> [!TIP]  
>  Se você precisar dessa conta para suas sequências de tarefas, poderá criar uma conta de usuário de domínio com permissões mínimas para acessar os recursos de rede necessários e usá-los em todas as contas da sequência de tarefas.  

> [!IMPORTANT]  
>  Não atribua permissões de logon interativo a essa conta.  
>   
>  Não use a Conta de Acesso à Rede para essa conta.  

### <a name="task-sequence-run-as-account"></a>Conta Executar como sequência de tarefas  
 A **Conta Executar como Sequência de Tarefa** é usada para executar linhas de comando em sequências de tarefas e usar credenciais diferentes da conta do sistema local. Essa conta é necessária se você adicionar a etapa **Executar Linha de Comando** a uma sequência de tarefas, mas não desejar que ela execute com permissões da conta do Sistema Local no computador gerenciado.  

 Configure a conta para ter as permissões mínimas necessárias para executar a linha de comando especificada na sequência de tarefas. A conta requer direitos de entrada interativos e geralmente requer a capacidade de instalar software e acessar recursos da rede.  

> [!IMPORTANT]  
>  Não use a Conta de Acesso à Rede para essa conta.  
>   
>  Nunca faça da conta um administrador de domínio.  
>   
>  Nunca configure perfis móveis para esta conta. Quando a sequência de tarefas é executada, ela baixa o perfil móvel da conta. Isso deixa o perfil vulnerável ao acesso no computador local.  
>   
>  Limite o escopo da conta. Por exemplo, crie Contas Executar como Sequência de Tarefas diferente para cada sequência de tarefas; desse modo, se uma conta for comprometida, somente os computadores cliente aos quais a conta tem acesso ficarão comprometidos.  
>   
>  Se a linha de comando exige acesso administrativo no computador, considere a criação de uma conta do administrador local exclusivamente para a conta Executar como de Sequência de Tarefas em todos os computadores que executam a sequência de tarefas. Exclua a conta assim que ela não for mais necessária.  
