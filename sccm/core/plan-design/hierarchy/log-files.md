---
title: Arquivos de log | System Center Configuration Manager
description: Use os arquivos de log para solucionar problemas em uma hierarquia do System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1ff371e-b0ad-4048-aeda-02a9ff08889e
caps.latest.revision: 9
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: cb27f2f2a6e0b0e3d6fca2d616d8ab806b74f9df


---
# <a name="log-files-in-system-center-configuration-manager"></a>Arquivos de log no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

No System Center Configuration Manager, os componentes do cliente e do servidor do site registram informações de processos em arquivos de log individuais. Por padrão, o registro em log de componentes do cliente e do servidor fica habilitado no Configuration Manager. As informações nesses arquivos de log podem ajudá-lo a solucionar problemas que podem ocorrer em sua hierarquia do Configuration Manager.  

 As seções a seguir fornecem detalhes sobre os diferentes arquivos de log. Use essas informações para exibir e monitorar os logs do cliente e do servidor do Configuration Manager para obter detalhes de operação e identificar informações de erro que podem ajudá-lo a solucionar problemas.  

-   [Sobre os arquivos de log do Configuration Manager](#BKMK_AboutLogs)  

    -   [Configurar opções de log usando o Configuration Manager Service Manager](#BKMK_LogOptions)  

    -   [Localizando logs do Configuration Manager](#BKMK_LogLocation)  

-   [Logs do cliente do Configuration Manager](#BKMK_ClientLogs)  

    -   [Operações do cliente](#BKMK_ClientOpLogs)  

    -   [Arquivos de log de instalação do cliente](#BKMK_ClientInstallLog)  

    -   [Cliente para Linux e UNIX](#BKMK_LogFilesforLnU)  

    -   [Cliente para computadores Mac](#BKMK_LogfilesforMac)  

-   [Arquivos de log do servidor de sites do Configuration Manager](#BKMK_ServerLogs)  

    -   [Logs do servidor do site e do servidor do sistema de sites](#BKMK_SiteSiteServerLog)  

    -   [Arquivos de log de instalação do servidor do site](#BKMK_SiteInstallLog)  

    -   [Arquivos de log do ponto de status de fallback](#BKMK_FSPLog)  

    -   [Arquivos de log do ponto de gerenciamento](#BKMK_MPLog)  

    -   [Arquivos de log do ponto de atualização de software](#BKMK_SUPLog)  

-   [Arquivos de log da funcionalidade do Configuration Manager](#BKMK_FunctionLogs)  

    -   [Gerenciamento de aplicativo](#BKMK_AppManageLog)  

    -   [Asset Intelligence](#BKMK_AILog)  

    -   [Backup e recuperação](#BKMK_BnRLog)  

    -   [Notificação de cliente](#BKMK_BGB)  

    -   [Registro de certificado](#BKMK_CertificateEnrollment)  

    -   [Configurações de conformidade e acesso a recursos da empresa](#BKMK_CompSettingsLog)  

    -   [Console do Configuration Manager](#BKMK_ConsoleLog)  

    -   [Gerenciamento de conteúdo](#BKMK_ContentLog)  

    -   [Descoberta](#BKMK_DiscoveryLog)  

    -   [Endpoint Protection](#BKMK_EPLog)  

    -   [Extensões](#BKMK_Extensions)  

    -   [Inventário](#BKMK_InventoryLog)  

    -   [Medição](#BKMK_MeteringLog)  

    -   [Migração](#BKMK_MigrationLog)  

    -   [Dispositivos móveis](#BKMK_MDMLog)  

    -   [Implantação do sistema operacional](#BKMK_OSDLog)  

    -   [Gerenciamento de energia](#BKMK_PowerMgmtLog)  

    -   [Controle remoto](#BKMK_RCLog)  

    -   [Relatórios](#BKMK_ReportLog)  

    -   [Administração baseada em funções](#BKMK_RBALog)  

    -   [Ponto de conexão de serviço](#BKMK_WITLog)  

    -   [Atualizações de software](#BKMK_SU_NAPLog)  

    -   [Wake On LAN](#BKMK_WOLLog)  

    -   [Windows Update Agent](#BKMK_WULog)  

    -   [Servidor do WSUS](#BKMK_WSUSLog)  

##  <a name="a-namebkmkaboutlogsa-about-configuration-manager-log-files"></a><a name="BKMK_AboutLogs"></a> Sobre arquivos de log do Configuration Manager  
 Por padrão, a maioria dos processos do Configuration Manager grava informações operacionais em um arquivo de log dedicado ao processo em questão. Estes arquivos de log são identificados pelo **.LOG** ou pela extensão do **.LO_** . O Configuration Manager grava no arquivo .LOG até que o log atinja seu tamanho máximo. Quando o log está cheio, o arquivo .LOG é copiado em um arquivo com o mesmo nome mas com extensão .LO_ e o processo ou componente continua a gravar no arquivo .LOG. Quando o arquivo .LOG atinge novamente seu tamanho máximo, o arquivo .LO_ é substituído e o processo se repete. Alguns componentes criam um histórico de arquivos de log acrescentando uma data ou o carimbo de data/hora ao nome do arquivo ou mantendo a extensão .LOG. Uma exceção ao tamanho máximo e uso do arquivo **.LO_** é o cliente para Linux e UNIX. Para obter informações sobre como o cliente do Linux e UNIX usa arquivos de log, consulte Gerenciar arquivos de log do cliente para Linux e UNIX na seção [Cliente para Linux e UNIX](#BKMK_LogFilesforLnU) neste tópico.  

 Para ver os logs, use a ferramenta de visualizador de log do Configuration Manager, CMTrace, localizada na pasta **\SMSSETUP\TOOLS** da mídia de origem do Configuration Manager. A ferramenta CMTrace é também adicionada a todas as imagens de inicialização acrescentadas à **Biblioteca de Software**.  

###  <a name="a-namebkmklogoptionsa-configure-logging-options-by-using-the-configuration-manager-service-manager"></a><a name="BKMK_LogOptions"></a> Configurar opções de log usando o Configuration Manager Service Manager  
 O Configuration Manager dá suporte a opções que permitem que você altere o local em que os arquivos de log são armazenados, bem como o tamanho do arquivo de log.  

 Use o procedimento a seguir para usar o **Configuration Manager Service Manager** para modificar o tamanho dos arquivos de log, o nome e o local do arquivo de log e forçar os vários componentes a gravar em um único arquivo de log.  

##### <a name="to-modify-logging-for-a-component"></a>Para modificar o log para um componente:  

1.  No console do Configuration Manager, clique em **Monitoramento**, clique em **Status do Sistema** e, depois, em **Status do Site** ou **Status do Componente**.  

2.  Na guia **Início** , no grupo **Componente** , clique em **Iniciar** e selecione **Configuration Manager Service Manager**.  

3.  Quando o Configuration Manager Service Manager abrir, conecte-se ao site que deseja gerenciar.  

     Se você não vir o site que deseja gerenciar, clique em **Site**, clique em **Conectar**e insira o nome do servidor do site para o site correto.  

4.  Expanda o site e navegue até **Componentes** ou **Servidores**, dependendo de onde estejam localizados os componentes que você quer gerenciar.  

5.  No painel direito, selecione um ou mais componentes.  

6.  No menu **Componente** , clique em **Log**.  

7.  Na caixa de diálogo **Log de Componentes do Configuration Manager** , conclua as opções de configuração disponíveis de sua seleção.  

8.  Clique em **OK** para salvar a configuração.  

###  <a name="a-namebkmkloglocationa-locating-configuration-manager-logs"></a><a name="BKMK_LogLocation"></a> Localizando logs do Configuration Manager  
 Por padrão, os arquivos de log do Configuration Manager são armazenados em uma variedade de locais que dependem do processo que cria o arquivo de log e da configuração de seus sistemas de sites. Como o local do log em um determinado computador pode variar, use a pesquisa para localizar os arquivos de log relevantes nos computadores do Configuration Manager para ajudá-lo a solucionar problemas de um cenário específico.  

##  <a name="a-namebkmkclientlogsa-configuration-manager-client-logs"></a><a name="BKMK_ClientLogs"></a> Logs do cliente do Configuration Manager  
 As seções a seguir listam os arquivos de log relacionados a operações e instalação do cliente.  

###  <a name="a-namebkmkclientoplogsa-client-operations"></a><a name="BKMK_ClientOpLogs"></a> Operações do cliente  
 A tabela a seguir lista os arquivos de log encontrados no cliente do Configuration Manager.  

|Nome do log|Descrição|  
|--------------|-----------------|  
|CAS.log|Serviço de acesso de conteúdo. Mantém o cache do pacote local no cliente.|  
|Ccm32BitLauncher.log|Ações de registros para iniciar aplicativos no cliente marcado como "executar como 32 bits".|  
|CcmEval.log|Registra as atividades de avaliação de status do cliente do Configuration Manager e detalhes dos componentes que são exigidos pelo cliente do Configuration Manager.|  
|CcmEvalTask.log|Registra as atividades de avaliação de status do cliente do Configuration Manager que são iniciadas pela tarefa de avaliação agendada.|  
|CcmExec.log|Registra as atividades do cliente e o serviço de Host de Agente do SMS. Esse arquivo de log também inclui informações sobre como habilitar e desabilitar o proxy de ativação.|  
|CcmMessaging.log|Registra as atividades relacionadas a comunicações entre o cliente e os pontos de gerenciamento.|  
|CCMNotificationAgent.log|Registra as atividades relacionadas a operações de notificação do cliente.|  
|Ccmperf.log|Registra as atividades relacionadas à manutenção e captura de dados referentes aos contadores de desempenho de cliente.|  
|CcmRestart.log|Registra a atividade de reinicialização de serviço do cliente.|  
|CCMSDKProvider.log|Registra as atividades para as interfaces SDK do cliente.|  
|CertificateMaintenance.log|Mantém os certificados para os Serviços de Domínio Active Directory e pontos de gerenciamento.|  
|CIDownloader.log|Registra os detalhes sobre downloads de definição do item de configuração.|  
|CITaskMgr.log|Registra as tarefas que são iniciadas para cada aplicativo e tipo de implantação, como o download de conteúdo ou ações de instalação e desinstalação.|  
|ClientAuth.log|Registra a atividade de autenticação e assinatura para o cliente.|  
|ClientIDManagerStartup.log|Cria e mantém o GUID do cliente e identifica as tarefas executadas durante a atribuição e o registro do cliente.|  
|ClientLocation.log|Registra as tarefas que estão relacionadas à atribuição de site do cliente.|  
|CMHttpsReadiness.log|Registra os resultados da execução da Ferramenta de avaliação de prontidão do HTTPS do Configuration Manager. Essa ferramenta verifica se os computadores têm o certificado de autenticação de cliente PKI que pode ser usado para o Configuration Manager.|  
|CmRcService.log|Registra as informações para o serviço de controle remoto.|  
|ContentTransferManager.log|Agenda o BITS (Serviço de transferência inteligente de plano de fundo) ou protocolo SMB para baixar ou acessar pacotes.|  
|DataTransferService.log|Registra todas as comunicações de BITS para acesso a política ou pacote.|  
|EndpointProtectionAgent|Registra as informações sobre a instalação do cliente do Endpoint Protection e o aplicativo de política de antimalware para esse cliente.|  
|execmgr.log|Registra os detalhes sobre pacotes e sequências de tarefas que são executados no cliente.|  
|ExpressionSolver.log|Registra os detalhes sobre os métodos de detecção aprimorados que são usados quando o log detalhado ou de depuração está habilitado.|  
|ExternalEventAgent.log|Registra o histórico de detecção de malware do Endpoint Protection e eventos relacionados ao status do cliente.|  
|FileBITS.log|Registra todas as tarefas de acesso de pacote do SMB.|  
|FileSystemFile.log|Registra a atividade do provedor de WMI (Instrumentação de Gerenciamento do Windows) para o inventário de software e a coleção de arquivos.|  
|FSPStateMessage.log|Registra a atividade de mensagens de estado que são enviadas para o ponto de status de fallback pelo cliente.|  
|InternetProxy.log|Registra a atividade de configuração e uso de proxy de rede para o cliente.|  
|InventoryAgent.log|Registra as atividades de inventário de hardware e de software e as ações de descoberta de pulsação no cliente.|  
|LocationCache.log|Registra a atividade de uso e manutenção do cache de localização para o cliente.|  
|LocationServices.log|Registra a atividade do cliente para localizar os pontos de gerenciamento, pontos de atualização de software e pontos de distribuição.|  
|MaintenanceCoordinator.log|Registra a atividade de tarefa de manutenção geral do cliente.|  
|Mifprovider.log|Registra a atividade do provedor de WMI para arquivos .MIF.|  
|mtrmgr.log|Monitora todos os processos de medição de software.|  
|PolicyAgent.log|Registra as solicitações de políticas feitas usando o serviço de transferência de dados.|  
|PolicyAgentProvider.log|Registra as alterações na política.|  
|PolicyEvaluator.log|Registra os detalhes sobre a avaliação de políticas em computadores cliente, incluindo as políticas de atualizações de software.|  
|PolicyPlatformClient.log|Registra o processo de correção e conformidade para todos os provedores localizados no **%Program Files%\Microsoft Policy Platform**, exceto o provedor de arquivo.|  
|PolicySdk.log|Registra as atividades para as interfaces SDK do sistema da política.|  
|Pwrmgmt.log|Registra as informações sobre como habilitar ou desabilitar e definir as configurações do cliente de proxy de ativação.|  
|PwrProvider.log|Registra as atividades do provedor de gerenciamento de energia (PWRInvProvider) hospedado no serviço WMI (Instrumentação de Gerenciamento do Windows). Em todas as versões com suporte do Windows, o provedor enumera as configurações atuais nos computadores durante o inventário de hardware e aplica as configurações do plano de energia.|  
|SCClient_&lt;domínio\>@&lt;nome de usuário\>_1.log|Registra a atividade no Centro de Software para o usuário especificado no computador cliente.|  
|SCClient_&lt;domínio\>@&lt;nome de usuário\>_2.log|Registra a atividade de histórico no Centro de Software para o usuário especificado no computador cliente.|  
|Scheduler.log|Registra as atividades de tarefas agendadas para todas as operações do cliente.|  
|SCNotify_&lt;domínio\>@&lt;nome de usuário\>_1.log|Registra a atividade para notificar os usuários sobre o software para o usuário especificado.|  
|SCNotify_&lt;domínio\>@&lt;nome de usuário\>_1-&lt;date_time>.log|Registra as informações de histórico para notificar os usuários sobre o software para o usuário especificado.|  
|setuppolicyevaluator.log|Registra a configuração e a criação da política de inventário na WMI.|  
|SleepAgent_&lt;domínio\>@&lt;@SYSTEM_0.log|Principal arquivo de log do proxy de ativação.|  
|smscliui.log|Registra o uso do cliente do Configuration Manager no Painel de Controle.|  
|SrcUpdateMgr.log|Registra a atividade dos aplicativos Windows Installer instalados que são atualizados com os locais de origem do ponto de distribuição atual.|  
|StatusAgent.log|Registra as mensagens de status que são criadas pelos componentes do cliente.|  
|SWMTRReportGen.log|Gera um relatório de dados de uso que é coletado pelo agente de medição. Esses dados são registrados em log no Mtrmgr.log.|  
|UserAffinity.log|Registra os detalhes sobre a afinidade de dispositivo de usuário.|  
|VirtualApp.log|Registra as informações específicas para a avaliação dos tipos de implantação do App-V.|  
|Wedmtrace.log|Registra as operações relacionadas a filtros de gravação nos clientes do Windows Embedded.|  
|wakeprxy-install.log|Registra as informações de instalação quando os clientes recebem a opção de configuração do cliente para habilitar o proxy de ativação.|  
|wakeprxy-uninstall.log|Registra as informações sobre a desinstalação do proxy de ativação quando os clientes recebem a opção de configuração do cliente para desabilitar o proxy de ativação, se o proxy de ativação foi habilitado anteriormente.|  

###  <a name="a-namebkmkclientinstallloga-client-installation-log-files"></a><a name="BKMK_ClientInstallLog"></a> Arquivos de log de instalação do cliente  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas à instalação do cliente do Configuration Manager.  

|Nome do log|Descrição|  
|--------------|-----------------|  
|ccmsetup.log|Registra as tarefas da **ccmsetup** para instalação, atualização e remoção do cliente. Pode ser usado para solucionar problemas de instalação do cliente.|  
|ccmsetup-ccmeval.log|Registra as tarefas da **ccmsetup** de status e correção do cliente.|  
|CcmRepair.log|Registra as atividades de reparo do agente do cliente.|  
|client.msi.log|Registra as tarefas de instalação executadas pelo client.msi. Pode ser usado para solucionar problemas de instalação ou remoção do cliente.|  

###  <a name="a-namebkmklogfilesforlnua-client-for-linux-and-unix"></a><a name="BKMK_LogFilesforLnU"></a> Cliente para Linux e UNIX  
 O cliente do Configuration Manager para Linux e UNIX registra as informações nos seguintes arquivos de log.  

> [!TIP]  
>  Começando com o cliente para Linux e UNIX por meio da atualização cumulativa 1, você pode usar o CMTrace para exibir arquivos de log do cliente para Linux e UNIX.  

> [!NOTE]  
>  Quando você usar a versão inicial do cliente para Linux e UNIX e fizer referência à documentação nesta seção, substitua as seguintes referências para cada arquivo ou processo:  
>   
>  -   Substitua **omiserver.bin** por **nwserver.bin**  
> -   Substitua **omi** por **nanowbem**  

|Nome do log|Detalhes|  
|--------------|-------------|  
|scxcm.log|Esse é o arquivo de log do serviço principal do cliente do Configuration Manager para Linux e UNIX (ccmexec.bin). Esse arquivo de log contém informações sobre a instalação e as operações em andamento do ccmexec.bin.<br /><br /> Por padrão, este arquivo de log é criado no seguinte local: **/var/opt/microsoft/scxcm.log**<br /><br /> Para alterar o local do arquivo de log, edite **/opt/microsoft/configmgr/etc/scxcm.conf** e altere o campo **CAMINHO** . Não é necessário reiniciar o computador cliente ou serviço de cliente para que a alteração entre em vigor.<br /><br /> Você pode definir o nível de log para uma das quatro diferentes configurações:|  
|scxcmprovider.log|Esse é o arquivo de log do serviço CIM do cliente do Configuration Manager para Linux e UNIX (omiserver.bin). Esse arquivo de log contém informações sobre as operações em andamento do nwserver.bin.<br /><br /> Por padrão, este log é criado no seguinte local: **/var/opt/microsoft/configmgr/scxcmprovider.log**<br /><br /> Para alterar o local do arquivo de log, edite **/opt/microsoft/omi/etc/scxcmprovider.conf** e altere o campo **CAMINHO** . Não é necessário reiniciar o computador cliente ou serviço de cliente para que a alteração entre em vigor.<br /><br /> Você pode definir o nível de log para uma das três diferentes configurações:|  

 **Os dois arquivos de log dão suporte a vários níveis de registro em log:**  

-   **scxcm.log** - Para alterar o nível de log, edite **/opt/microsoft/configmgr/etc/scxcm.conf** e altere cada instância da marca **MODULE** em cada nível de log desejado:  

    -   ERRO: indica problemas que exigem atenção.  

    -   AVISO: indica possíveis problemas de operações do cliente.  

    -   INFORMAÇÕES: log mais detalhado que indica o status de vários eventos no cliente.  

    -   RASTREAMENTO: log detalhado que normalmente é usado para diagnosticar problemas.  

-   **scxcmprovider.log** - Para alterar o nível de log, edite **/opt/microsoft/omi/etc/scxcmprovider.conf** e altere cada instância da marca **MÓDULO** em cada nível de log desejado:  

    -   ERRO: indica problemas que exigem atenção.  

    -   AVISO: indica possíveis problemas de operações do cliente.  

    -   INFORMAÇÕES: log mais detalhado que indica o status de vários eventos no cliente.  

Em condições normais de operação, o nível de log de ERRO deve ser usado. O nível de ERRO de log cria o menor arquivo de log. À medida que o nível de log vai aumentando de ERRO para AVISO para INFO para RASTREAMENTO, cada etapa resulta em um arquivo de log maior, pois mais dados são gravados no arquivo de log.  

####  <a name="a-namebkmkmanagelinuxlogsa-manage-log-files-for-the-client-for-linux-and-unix-client"></a><a name="BKMK_ManageLinuxLogs"></a> Gerenciar arquivos de log do cliente para o cliente do Linux e UNIX  
O cliente para Linux e UNIX não limita o tamanho máximo dos arquivos de log do cliente nem copia automaticamente o conteúdo de seus arquivos **.LOG** para outro arquivo, como um arquivo **.LO_** . Se você deseja controlar o tamanho máximo dos arquivos de log, implemente um processo para gerenciar os arquivos de log independente do cliente do Configuration Manager para Linux e UNIX.  

Por exemplo, você pode usar o comando do Linux e UNIX **logrotate** para gerenciar o tamanho e a rotação dos arquivos de log de clientes. O cliente do Configuration Manager para Linux e UNIX fornece uma interface que habilita a **logrotate** a avisar o cliente quando a rotação do log estiver concluída, permitindo que o cliente retome o registro no arquivo de log.  

Para obter informações sobre o **logrotate**, consulte a documentação para as distribuições do Linux e UNIX que você usa.  

###  <a name="a-namebkmklogfilesformaca-client-for-mac-computers"></a><a name="BKMK_LogfilesforMac"></a> Cliente para computadores Mac  
O cliente do Configuration Manager para computadores Mac registra informações nos seguintes arquivos de log.  

|Nome do log|Detalhes|  
|--------------|-------------|  
|CCMClient-*&lt;data_hora>*.log|Registra atividades que estão relacionadas a operações do cliente Mac, que incluem gerenciamento de aplicativos, inventário e log de erros.<br /><br /> Esse arquivo de log está localizado na pasta **/Library/Application Support/Microsoft/CCM/Logs** no computador Mac.|  
|CCMAgent-*&lt;data_hora>*.log|Registra informações que estão relacionadas a operações do cliente, que incluem operações de logon e logoff do usuário e atividade do computador Mac.<br /><br /> Esse arquivo de log está localizado na pasta **~/Library/Logs** no computador Mac.|  
|CCMNotifications-*&lt;data_hora>*.log|Registra atividades relacionadas a notificações do Configuration Manager exibidas no computador Mac.<br /><br /> Esse arquivo de log está localizado na pasta **~/Library/Logs** no computador Mac.|  
|CCMPrefPane-*&lt;data_hora>*.log|Registra atividades relacionadas à caixa de diálogo de preferências do Configuration Manager no computador Mac, que inclui logs de erros e status geral.<br /><br /> Esse arquivo de log está localizado na pasta **~/Library/Logs** no computador Mac.|  

 Adicionalmente, o arquivo de log SMS_DM.log no servidor do sistema de site registra a comunicação entre computadores Mac e ponto de gerenciamento habilitado para dispositivos móveis e computadores Mac.  

##  <a name="a-namebkmkserverlogsa-configuration-manager-site-server-log-files"></a><a name="BKMK_ServerLogs"></a> Arquivos de log do servidor do site do Configuration Manager  
 As seções a seguir listam arquivos de log localizados no servidor do site ou relacionados às funções específicas do sistema de site.  

###  <a name="a-namebkmksitesiteserverloga-site-server-and-site-system-server-logs"></a><a name="BKMK_SiteSiteServerLog"></a> Logs do servidor do site e do servidor do sistema de sites  
 A tabela a seguir lista os arquivos de log localizados no servidor de sites e nos servidores do sistema de sites do Configuration Manager.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|adctrl.log|Registra atividade de processamento do registro.|Servidor do site|  
|ADForestDisc.log|Registra ações de descoberta de florestas do Active Directory.|Servidor do site|  
|ADService.log|Registra criação de conta e detalhes do grupo de segurança no Active Directory.|Servidor do site|  
|adsgdis.log|Registra ações de descoberta de grupos do Active Directory.|Servidor do site|  
|adsysdis.log|Registra ações de descoberta de sistemas do Active Directory.|Servidor do site|  
|adusrdis.log|Registra ações de descoberta de usuário do Active Directory.|Servidor do site|  
|ccm.log|Registra atividades de instalação push de cliente.|Servidor do site|  
|CertMgr.log|Registra as atividades de certificado para comunicações intra-sites.|Servidor do sistema de site|  
|chmgr.log|Registra atividades do Gerenciador de Integridade do Cliente.|Servidor do site|  
|Cidm.log|Registra alterações nas configurações de cliente pelo CIDM (Gerenciador de dados de instalação do cliente).|Servidor do site|  
|colleval.log|Registra detalhes sobre quando as coleções são criadas, alteradas e excluídas pelo Collection Evaluator.|Servidor do site|  
|compmon.log|Registra o status dos threads do componente monitorados para o servidor do site.|Servidor do sistema de site|  
|compsumm.log|Registra tarefas do Component Status Summarizer.|Servidor do site|  
|ComRegSetup.log|Registra a instalação inicial dos resultados do registro COM para um servidor de site.|Servidor do sistema de site|  
|dataldr.log|Registra informações sobre o processamento de arquivos MIF e o inventário de hardware no banco de dados do Configuration Manager.|Servidor do site|  
|ddm.log|Registra as atividades do gerenciador de dados de descoberta.|Servidor do site|  
|despool.log|Registra transferências de comunicação site a site de entrada.|Servidor do site|  
|distmgr.log|Registra os detalhes sobre a criação de pacote, compactação, a replicação delta e atualizações de informações.|Servidor do site|  
|EPCtrlMgr.log|Registra informações sobre a sincronização de informações de ameaça de malware do servidor da função de sistema de sites do Endpoint Protection no banco de dados do Configuration Manager.|Servidor do site|  
|EPMgr.log|Registra o status da função do sistema de site Endpoint Protection.|Servidor do sistema de site|  
|EPSetup.log|Fornece informações sobre a instalação da função do sistema de site do Endpoint Protection.|Servidor do sistema de site|  
|EnrollSrv.log|Registra atividades do processo do serviço de registro.|Servidor do sistema de site|  
|EnrollWeb.log|Registra atividades do processo de site da Web de registro.|Servidor do sistema de site|  
|fspmgr.log|Registra atividades da função de sistema de site do ponto de status de fallback.|Servidor do sistema de site|  
|hman.log|Registra informações sobre as alterações de configuração do site e a publicação de informações do site nos Serviços de Domínio Active Directory.|Servidor do site|  
|Inboxast.log|Registra os arquivos movidos do ponto de gerenciamento para a pasta de CAIXAS DE ENTRADA correspondente no servidor do site.|Servidor do site|  
|inboxmgr.log|Registra atividades de transferência de arquivo entre as pastas de caixa de entrada.|Servidor do site|  
|inboxmon.log|Registra o processamento de arquivos de caixa de entrada e atualizações do contador de desempenho.|Servidor do site|  
|invproc.log|Registra o encaminhamento de arquivos MIF de um site secundário para seu site pai.|Servidor do site|  
|migmctrl.log|Informações de registros de ações de migração que envolvem trabalhos de migração, pontos de distribuição compartilhados e atualizações de ponto de distribuição.|O site de nível superior na hierarquia do Configuration Manager e cada site primário filho<br /><br /> Em uma hierarquia de vários sites primários, use o arquivo de log criado no site de administração central.|  
|mpcontrol.log|Grava o registro do ponto de gerenciamento com WINS. Registra a disponibilidade do ponto de gerenciamento a cada 10 minutos.|Servidor do sistema de site|  
|mpfdm.log|Registra as ações do componente do ponto de gerenciamento que movem arquivos de cliente para pasta de CAIXAS DE ENTRADA no servidor do site.|Servidor do sistema de site|  
|mpMSI.log|Registra detalhes sobre a instalação do ponto de gerenciamento.|Servidor do site|  
|MPSetup.log|Registra o processo de wrapper de instalação do ponto de gerenciamento.|Servidor do site|  
|netdisc.log|Registra ações de descoberta de rede.|Servidor do site|  
|ntsvrdis.log|Registra a atividade de descoberta dos servidores do sistema de site.|Servidor do site|  
|Objreplmgr|Registra o processamento de notificações de alteração de objeto para replicação.|Servidor do site|  
|offermgr.log|Registra atualizações de anúncio.|Servidor do site|  
|offersum.log|Registra o resumo de mensagens de status da implantação.|Servidor do site|  
|OfflineServicingMgr.log|Registra as atividades de aplicação de atualizações para arquivos de imagem de sistema operacional.|Servidor do site|  
|outboxmon.log|Registra o processamento de arquivos de caixa de saída e atualizações de contador de desempenho.|Servidor do site|  
|PerfSetup.log|Registra os resultados da instalação de contadores de desempenho.|Servidor do sistema de site|  
|PkgXferMgr.log|Registra as ações do componente SMS Executive que é responsável por enviar conteúdo de um site primário para um ponto de distribuição remoto.|Servidor do site|  
|policypv.log|Registra atualizações para as políticas do cliente para refletir as alterações nas configurações do cliente ou implantações.|Servidor do site primário|  
|rcmctrl.log|Registra as atividades de replicação de banco de dados entre sites na hierarquia.|Servidor do site|  
|replmgr.log|Registra a replicação de arquivos entre os componentes de servidor do site e o componente Agendador.|Servidor do site|  
|ResourceExplorer.log|Registra erros, avisos e informações sobre como executar o Gerenciador de Recursos.|O computador que executa o console do Configuration Manager|  
|ruleengine.log|Registra detalhes sobre regras de implantação automática para identificação, download de conteúdo, grupo de atualização de software e criação de implantação.|Servidor do site|  
|schedule.log|Registra detalhes sobre a replicação de arquivos e trabalho de site a site.|Servidor do site|  
|sender.log|Registra os arquivos que são transferidos por replicação baseada em arquivos entre sites.|Servidor do site|  
|sinvproc.log|Registra informações sobre o processamento de dados de inventário de software para o banco de dados do site.|Servidor do site|  
|sitecomp.log|Registra detalhes sobre a manutenção dos componentes do site instalados em todos os servidores do sistema de site no site.|Servidor do site|  
|sitectrl.log|Registra as alterações de configuração de site feitas para objetos de controle de site no banco de dados.|Servidor do site|  
|sitestat.log|Registra disponibilidade e espaço em disco monitorando o processo de todos os sistemas de site.|Servidor do site|  
|SmsAdminUI.log|Registra atividades do console do Configuration Manager.|O computador que executa o console do Configuration Manager|  
|SMSAWEBSVCSetup.log|Registra as atividades de instalação do serviço da Web de catálogo do aplicativo.|Servidor do sistema de site|  
|smsbkup.log|Registra a saída do processo de backup do site.|Servidor do site|  
|smsdbmon.log|Registra as alterações de banco de dados.|Servidor do site|  
|SMSENROLLSRVSetup.log|Registra as atividades de instalação do Serviço Web de Registro.|Servidor do sistema de site|  
|SMSENROLLWEBSetup.log|Registra as atividades de instalação do Site da Web de Registro.|Servidor do sistema de site|  
|smsexec.log|Registra o processamento de todos os threads de componente de servidor do site.|Servidor de site ou servidor de sistema de site|  
|SMSFSPSetup.log|Registra as mensagens geradas pela instalação de um ponto de status de fallback.|Servidor do sistema de site|  
|SMSPORTALWEBSetup.log|Registra as atividades de instalação do site da Web do catálogo de aplicativos.|Servidor do sistema de site|  
|SMSProv.log|Registra o acesso do provedor WMI ao banco de dados do site.|Computador com o Provedor de SMS|  
|srsrpMSI.log|Registra resultados detalhados do processo de instalação de ponto de relatório por meio da saída do MSI.|Servidor do sistema de site|  
|srsrpsetup.log|Resultados de registros do processo de instalação do ponto de relatório.|Servidor do sistema de site|  
|statesys.log|Registra o processamento de mensagens de estado do sistema.|Servidor do site|  
|statmgr.log|Registra a gravação de todas as mensagens de status para o banco de dados.|Servidor do site|  
|swmproc.log|Registra o processamento de arquivos e configurações de medição.|Servidor do site|  

###  <a name="a-namebkmksiteinstallloga-site-server-installation-log-files"></a><a name="BKMK_SiteInstallLog"></a> Arquivos de log de instalação do servidor do site  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas à instalação do site.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|Registra avaliação de componente de pré-requisitos e atividades de instalação.|Servidor do site|  
|ConfigMgrSetup.log|Registra saída detalhada do programa de instalação do servidor do site.|Servidor do site|  
|ConfigMgrSetupWizard.log|Registra as informações relacionadas à atividade no assistente de instalação.|Servidor do site|  
|SMS_BOOTSTRAP.log|Registra informações sobre o andamento do início do processo de instalação do site secundário. Detalhes do processo de instalação atual estão contidos em ConfigMgrSetup.log.|Servidor do site|  
|smstsvc.log|Registra as informações sobre a instalação, o uso e a remoção de um serviço do Windows que é usado para testar conectividade da rede e permissões entre servidores, usando a conta de computador do servidor que inicia a conexão.|Servidor de site e sistemas de site|  

###  <a name="a-namebkmkfsploga-fallback-status-point-logs-files"></a><a name="BKMK_FSPLog"></a> Arquivos de log do ponto de status de fallback  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas ao ponto de status de fallback.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|FspIsapi|Registra detalhes sobre comunicações com o ponto de status de fallback de clientes herdados de dispositivos móveis e computadores cliente.|Servidor do sistema de site|  
|fspMSI.log|Registra as mensagens geradas pela instalação de um ponto de status de fallback.|Servidor do sistema de site|  
|fspmgr.log|Registra atividades da função de sistema de site do ponto de status de fallback.|Servidor do sistema de site|  

###  <a name="a-namebkmkmploga-management-point-logs-files"></a><a name="BKMK_MPLog"></a> Arquivos de log do ponto de gerenciamento  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas ao ponto de gerenciamento.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|Registra atividade de mensagens de cliente no ponto de extremidade.|Servidor do sistema de site|  
|MP_CliReg.log|Registra a atividade de registro de cliente processada pelo ponto de gerenciamento.|Servidor do sistema de site|  
|MP_Ddr.log|Registra a conversão de registros XML.ddr de clientes e os copia para o servidor do site.|Servidor do sistema de site|  
|MP_Framework.log|Registra atividades do ponto de gerenciamento principal e componentes de estrutura do cliente.|Servidor do sistema de site|  
|MP_GetAuth.log|Registra a atividade de autorização do cliente.|Servidor do sistema de site|  
|MP_GetPolicy.log|Registra atividade de solicitação da política de computadores cliente.|Servidor do sistema de site|  
|MP_Hinv.log|Registra detalhes sobre a conversão de registros de inventário de hardware XML de clientes e a cópia desses arquivos para o servidor do site.|Servidor do sistema de site|  
|MP_Location.log|Registra solicitação de local e atividade de resposta dos clientes.|Servidor do sistema de site|  
|MP_OOBMgr.log|Registra as atividades do ponto de gerenciamento relacionadas ao recebimento de OTP de um cliente.|Servidor do sistema de site|  
|MP_Policy.log|Comunicação da política de registros.|Servidor do sistema de site|  
|MP_Relay.log|Registra a transferência de arquivos que são coletados do cliente.|Servidor do sistema de site|  
|MP_Retry.log|Registra os processos de repetição de inventário de hardware.|Servidor do sistema de site|  
|MP_Sinv.log|Registra detalhes sobre a conversão de registros de inventário de software XML de clientes e a cópia desses arquivos para o servidor do site.|Servidor do sistema de site|  
|MP_SinvCollFile.log|Registra detalhes sobre a coleção de arquivos.|Servidor do sistema de site|  
|MP_Status.log|Registra os detalhes sobre a conversão de arquivos de mensagens de status XML.svf de clientes e a cópia desses arquivos para o servidor do site.|Servidor do sistema de site|  
|mpcontrol.log|Grava o registro do ponto de gerenciamento com WINS. Registra a disponibilidade do ponto de gerenciamento a cada 10 minutos.|Servidor do site|  
|mpfdm.log|Registra as ações do componente do ponto de gerenciamento que movem arquivos de cliente para pasta de CAIXAS DE ENTRADA no servidor do site.|Servidor do sistema de site|  
|mpMSI.log|Registra detalhes sobre a instalação do ponto de gerenciamento.|Servidor do site|  
|MPSetup.log|Registra o processo de wrapper de instalação do ponto de gerenciamento.|Servidor do site|  

###  <a name="a-namebkmksuploga-software-update-point-log-files"></a><a name="BKMK_SUPLog"></a> Arquivos de log do ponto de atualização de software  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas ao ponto de atualização de software.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|Registra detalhes sobre a replicação de arquivos de notificação de atualizações de software de um site pai para sites filho.|Servidor do site|  
|PatchDownloader.log|Registra detalhes sobre o processo de baixar atualizações de software da fonte de atualizações para o destino de download no servidor de site.|O computador que hospeda o console do Configuration Manager no qual os downloads são iniciados|  
|ruleengine.log|Registra detalhes sobre regras de implantação automática para identificação, download de conteúdo, grupo de atualização de software e criação de implantação.|Servidor do site|  
|SUPSetup.log|Registra os detalhes sobre a instalação do ponto de atualização de software. Quando a instalação do ponto de atualização de software é concluída, **Installation was successful** é gravado nesse arquivo de log.|Servidor do sistema de site|  
|WCM.log|Registra os detalhes sobre a configuração do ponto de atualização de software e conexões ao servidor do Windows Server Update Services (WSUS) para categorias de atualização assinadas, classificações e idiomas.|Servidor do site que se conecta ao servidor do Windows Server Update Services (WSUS)|  
|WSUSCtrl.log|Registra os detalhes sobre a configuração, a conectividade de banco de dados e a integridade do servidor do WSUS para o site.|Servidor do sistema de site|  
|wsyncmgr.log|Registra detalhes sobre o processo de sincronização de atualizações de software.|Servidor do sistema de site|  
|WUSSyncXML.log|Registra os detalhes sobre a ferramenta de inventário para o processo de sincronização do Microsoft Updates.|O computador cliente configurado como o host de sincronização para a ferramenta de inventário para o Microsoft Updates.|  

##  <a name="a-namebkmkfunctionlogsa-log-files-for-configuration-manager-functionality"></a><a name="BKMK_FunctionLogs"></a> Arquivos de log da funcionalidade do Configuration Manager  
 As seções a seguir listam os arquivos de log relacionados às diferentes funções no Configuration Manager.  

###  <a name="a-namebkmkappmanageloga-application-management"></a><a name="BKMK_AppManageLog"></a> Gerenciamento de aplicativo  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas ao gerenciamento de aplicativos.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|AppIntentEval.log|Registra os detalhes sobre o estado atual e pretendido dos aplicativos, sua aplicabilidade, se os requisitos foram atendidos, tipos de implantação e dependências.|Cliente|  
|AppDiscovery.log|Registra os detalhes sobre a descoberta ou detecção de aplicativos em computadores cliente.|Cliente|  
|AppEnforce.log|Registra os detalhes sobre as ações de imposição (instalar e desinstalar) realizadas para aplicativos no cliente.|Cliente|  
|awebsctl.log|Registra as atividades de monitoramento da função do sistema de site do ponto de serviços Web do catálogo de aplicativos.|Servidor do sistema de site|  
|awebsvcMSI.log|Registra informações de instalação detalhadas da função do sistema de site do ponto de serviços Web do catálogo de aplicativos.|Servidor do sistema de site|  
|CCMSDKProvider.log|Registra as atividades do SDK do gerenciamento de aplicativos.|Cliente|  
|colleval.log|Registra detalhes sobre quando as coleções são criadas, alteradas e excluídas pelo Collection Evaluator.|Servidor do sistema de site|  
|ConfigMgrSoftwareCatalog.log|Registra a atividade do catálogo de aplicativos, inclusive o uso de Silverlight.|Cliente|  
|portlctl.log|Registra as atividades de monitoramento da função do sistema de site do ponto de sites da Web do catálogo de aplicativos.|Servidor do sistema de site|  
|portlwebMSI.log|Registra a atividade da instalação MSI para a função de sites da Web do catálogo de aplicativos.|Servidor do sistema de site|  
|PrestageContent.log|Registra detalhes sobre o uso da ferramenta ExtractContent.exe em um ponto de distribuição em pré-teste remoto. Essa ferramenta extrai o conteúdo exportado para um arquivo.|Servidor do sistema de site|  
|ServicePortalWebService.log|Registra as atividades dos serviços Web do catálogo de aplicativos.|Servidor do sistema de site|  
|ServicePortalWebSite.log|Registra as atividades dos sites da Web do catálogo de aplicativos.|Servidor do sistema de site|  
|SMSdpmon.log|Registra detalhes sobre a tarefa agendada de monitoramento da integridade do ponto de distribuição, que é configurada em um ponto de distribuição.|Servidor do site|  
|SoftwareCatalogUpdateEndpoint.log|Registra as atividades de gerenciamento de URL para o catálogo de aplicativos mostrado no Centro de Software.|Cliente|  
|SoftwareCenterSystemTasks.log|Registra as atividades de validação de componente de pré-requisito do Centro de Software.|Cliente|  

 A tabela a seguir lista os arquivos de log que contêm informações relacionadas à implantação de pacotes e programas.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|colleval.log|Registra detalhes sobre quando as coleções são criadas, alteradas e excluídas pelo Collection Evaluator.|Servidor do site|  
|execmgr.log|Registra os detalhes sobre pacotes e sequências de tarefas que são executados.|Cliente|  

###  <a name="a-namebkmkailoga-asset-intelligence"></a><a name="BKMK_AILog"></a> Asset Intelligence  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas ao Asset Intelligence.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|Registra as atividades das ações de inventário do Asset Intelligence.|Cliente|  
|aikbmgr.log|Registra os detalhes sobre o processamento de arquivos XML por meio da caixa de entrada para a atualização do catálogo do Asset Intelligence.|Servidor do site|  
|AIUpdateSvc.log|Registra a interação entre o ponto de sincronização do Asset Intelligence e o SCO (System Center Online), o serviço da Web online.|Servidor do sistema de site|  
|AIUSMSI.log|Registra os detalhes sobre a instalação da função de sistema de site do ponto de sincronização do Asset Intelligence.|Servidor do sistema de site|  
|AIUSSetup.log|Registra os detalhes sobre a instalação da função de sistema de site do ponto de sincronização do Asset Intelligence.|Servidor do sistema de site|  
|ManagedProvider.log|Registra os detalhes sobre a descoberta de software com uma marca de identificação do software associado. Também registra as atividades relacionadas ao inventário de hardware.|Servidor do sistema de site|  
|MVLSImport.log|Registra os detalhes sobre o processamento de arquivos de licenciamento importados.|Servidor do sistema de site|  

###  <a name="a-namebkmkbnrloga-backup-and-recovery"></a><a name="BKMK_BnRLog"></a> Backup e recuperação  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas às ações de backup e recuperação, inclusive redefinições de site e alterações no Provedor de SMS.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|Registra informações sobre tarefas de configuração e recuperação quando o Configuration Manager recupera um site por meio de backup.|Servidor do site|  
|smsbkup.log|Registra os detalhes sobre a atividade de backup do site.|Servidor do site|  
|smssqlbkup.log|Registra a saída do processo de backup do banco de dados do site quando o SQL Server é instalado em um servidor diferente do servidor do site.|Servidor de banco de dados do site|  
|Smswriter.log|Registra informações sobre o estado do gravador VSS do Configuration Manager usado pelo processo de backup.|Servidor do site|  

###  <a name="a-namebkmkcertificateenrollmenta-certificate-enrollment"></a><a name="BKMK_CertificateEnrollment"></a> Registro de certificado  
 A tabela a seguir lista os arquivos de log do Configuration Manager que contêm informações relacionadas ao registro de certificado, que usa o ponto de registro de certificado e o Módulo de Política do Configuration Manager no servidor que executa o Serviço de Registro de Dispositivo de Rede.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|Crp.log|Registra as atividades de registro.|Ponto de registro de certificado|  
|Crpctrl.log|Registra a integridade operacional do ponto de registro de certificado.|Ponto de registro de certificado|  
|Crpsetup.log|Registra detalhes sobre a instalação e a configuração do ponto de registro de certificado.|Ponto de registro de certificado|  
|Crpmsi.log|Registra detalhes sobre a instalação e a configuração do ponto de registro de certificado.|Ponto de registro de certificado|  
|NDESPlugin.log|Registra as atividades de registro de certificado e verificação de desafio.|Módulo de Política do Configuration Manager e o Serviço de Registro de Dispositivo de Rede|  

 Além dos arquivos de log do Configuration Manager, examine os logs dos aplicativos do Windows no Visualizador de Eventos no servidor que executa o Serviço de Registro de Dispositivo de Rede e no servidor que hospeda o ponto de registro de certificado. Por exemplo, procure por mensagens da origem **NetworkDeviceEnrollmentService** . Você também pode usar os seguintes arquivos de log:  

-   Arquivos de log do IIS para o Serviço de Registro de Dispositivo de Rede: **&lt;path\>\inetpub\logs\LogFiles\W3SVC1**  

-   Arquivos de log do IIS para o ponto de registro de certificado: **&lt;path\>\inetpub\logs\LogFiles\W3SVC1**  

-   Arquivo de log da Política de Registro de Dispositivo de Rede: **mscep.log**  

    > [!NOTE]  
    >  Este arquivo está localizado na pasta do perfil da conta de Serviço de Registro de Dispositivo de Rede, por exemplo, C:\Users\SCEPSvc. Para obter mais informações sobre como habilitar registro para o Serviço de Registro de Dispositivo de Rede, consulte a seção [Habilitar Registro](http://go.microsoft.com/fwlink/?LinkId=320576) no NDES (Serviço de Registro de Dispositivo de Rede) no artigo AD CS (Serviços de Certificados do Active Directory) no wiki da TechNet.  

###  <a name="a-namebkmkbgba-client-notification"></a><a name="BKMK_BGB"></a> Notificação de cliente  
 A tabela a seguir lista os arquivos de log que contêm as informações relacionadas à notificação de cliente.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|bgbmgr.log|Registra os detalhes sobre as atividades do servidor de site relacionando as tarefas de notificação do cliente e processando os arquivos online e de status da tarefa.|Servidor do site|  
|BGBServer.log|Registra as atividades do servidor de notificação como comunicações do cliente para o servidor e envio de tarefas aos clientes. Também registra informações sobre a geração de arquivos de status de tarefa e online a serem enviados para o servidor do site.|Ponto de gerenciamento|  
|BgbSetup.log|Registra as atividades do processo do invólucro de instalação do servidor de notificação durante a instalação e a desinstalação.|Ponto de gerenciamento|  
|bgbisapiMSI.log|Registra os detalhes sobre a instalação e a desinstalação do servidor de notificação.|Ponto de gerenciamento|  
|BgbHttpProxy.log|Registra as atividades do proxy HTTP de notificação enquanto ele retransmite as mensagens de clientes usando HTTP do servidor de notificação e para ele.|Cliente|  
|CCMNotificationAgent.log|Registra as atividades do agente de notificação, como a comunicação de cliente para servidor, e informações sobre tarefas recebidas e despachadas para outros agentes cliente.|Cliente|  

###  <a name="a-namebkmkcompsettingsloga-compliance-settings-and-company-resource-access"></a><a name="BKMK_CompSettingsLog"></a> Configurações de conformidade e acesso a recursos da empresa  
 A tabela a seguir lista os arquivos de log que contêm as informações relacionadas a configurações de conformidade e acesso ao recurso da empresa.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|Registra os detalhes sobre o processo de correção e conformidade para configurações de conformidade, atualizações de software e gerenciamento de aplicativos.|Cliente|  
|CITaskManager.log|Registra as informações sobre o agendamento de tarefas do item de configuração.|Cliente|  
|DCMAgent.log|Registra as informações de alto nível sobre avaliação, relatórios conflitantes e correção de itens e aplicativos de configuração.|Cliente|  
|DCMReporting.log|Registra as informações sobre os relatórios dos resultados da plataforma de política em mensagens de estado para itens de configuração.|Cliente|  
|DcmWmiProvider.log|Registra as informações sobre a leitura de synclets de item de configuração por meio da Instrumentação de Gerenciamento do Windows (WMI).|Cliente|  

###  <a name="a-namebkmkconsoleloga-configuration-manager-console"></a><a name="BKMK_ConsoleLog"></a> Console do Configuration Manager  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas ao console do Configuration Manager.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|Registra a instalação do console do Configuration Manager.|Computador que executa o console do Configuration Manager|  
|SmsAdminUI.log|Registra informações sobre a operação do console do Configuration Manager.|Computador que executa o console do Configuration Manager|  
|SMSProv.log|Registra as atividades executadas pelo Provedor de SMS. As atividades do console do Configuration Manager usam o Provedor de SMS.|Servidor de site ou servidor de sistema de site|  

###  <a name="a-namebkmkcontentloga-content-management"></a><a name="BKMK_ContentLog"></a> Gerenciamento de conteúdo  
 A tabela a seguir lista os arquivos de log que contêm as informações relacionadas ao gerenciamento de conteúdo.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|CloudDP-&lt;guid\>.log|Registra detalhes de uma distribuição específica baseada em nuvem, incluindo informações sobre armazenamento e acesso a conteúdo.|Servidor do sistema de site|  
|CloudMgr.log|Registra detalhes sobre o provisionamento de conteúdo, coletando estatísticas de armazenamento e largura de banda, além de ações iniciadas pelo administrador para interromper ou iniciar o serviço de nuvem que executa um ponto de distribuição baseado em nuvem.|Servidor do sistema de site|  
|DataTransferService.log|Registra todas as comunicações de BITS para acesso a política ou pacote. Esse log também é usado para gerenciamento de conteúdo por pontos de distribuição de recepção.|Um computador configurado como um ponto de distribuição de recepção|  
|PullDP.log|Registra os detalhes sobre o conteúdo que o ponto de distribuição de recepção transfere dos pontos de distribuição de origem.|Um computador configurado como um ponto de distribuição de recepção|  
|PrestageContent.log|Registra detalhes sobre o uso da ferramenta ExtractContent.exe em um ponto de distribuição em pré-teste remoto. Essa ferramenta extrai o conteúdo exportado para um arquivo.|Função do sistema de site|  
|SMSdpmon.log|Registra detalhes sobre a tarefa agendada de monitoramento de integridade do ponto de distribuição, que está configurada em um ponto de distribuição.|Função do sistema de site|  
|smsdpprov.log|Registra os detalhes sobre a extração de arquivos compactados recebidos de um site primário. Esse log é gerado pelo provedor WMI do ponto de distribuição remoto.|Um computador de ponto de distribuição que não está colocalizado com o servidor do site.|  

###  <a name="a-namebkmkdiscoveryloga-discovery"></a><a name="BKMK_DiscoveryLog"></a> Descoberta  
A tabela a seguir lista os arquivos de log que contêm informações relacionadas à Descoberta.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|Registra as ações da Descoberta de Grupos de Segurança do Active Directory.|Servidor do site|  
|adsysdis.log|Registra ações de descoberta de sistemas do Active Directory.|Servidor do site|  
|adusrdis.log|Registra ações de descoberta de usuário do Active Directory.|Servidor do site|  
|ADForestDisc.log|Registra ações de descoberta de florestas do Active Directory.|Servidor do site|  
|ddm.log|Registra as atividades do gerenciador de dados de descoberta.|Servidor do site|  
|InventoryAgent.log|Registra as atividades de inventário de hardware e de software e as ações de descoberta de pulsação no cliente.|Cliente|  
|netdisc.log|Registra ações de descoberta de rede.|Servidor do site|  

###  <a name="a-namebkmkeploga-endpoint-protection"></a><a name="BKMK_EPLog"></a> Endpoint Protection  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas ao Endpoint Protection.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|Registra os detalhes sobre a instalação do cliente do Endpoint Protection e do aplicativo da política de antimalware para esse cliente.|Cliente|  
|EPCtrlMgr.log|Registra detalhes sobre a sincronização de informações de ameaça de malware do servidor de função do Endpoint Protection no banco de dados do Configuration Manager.|Servidor do sistema de site|  
|EPMgr.log|Monitora o status da função do sistema de site do Endpoint Protection.|Servidor do sistema de site|  
|EPSetup.log|Fornece informações sobre a instalação da função do sistema de site do Endpoint Protection.|Servidor do sistema de site|  

###  <a name="a-namebkmkextensionsa-extensions"></a><a name="BKMK_Extensions"></a> Extensões  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas às Extensões.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|Registra informações sobre o download das extensões da Microsoft e a instalação e desinstalação de todas as extensões.|O computador que executa o console do Configuration Manager|  
|FeatureExtensionInstaller.log|Registra informações sobre a instalação e a remoção das extensões individuais quando elas são habilitadas ou desabilitadas no console do Configuration Manager.|O computador que executa o console do Configuration Manager|  
|SmsAdminUI.log|Registra atividades do console do Configuration Manager.|O computador que executa o console do Configuration Manager|  

###  <a name="a-namebkmkinventoryloga-inventory"></a><a name="BKMK_InventoryLog"></a> Inventário  
 A tabela a seguir lista os arquivos de log que contêm as informações relacionadas ao processamento de dados de inventário.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|dataldr.log|Registra informações sobre o processamento de arquivos MIF e o inventário de hardware no banco de dados do Configuration Manager.|Servidor do site|  
|invproc.log|Registra o encaminhamento de arquivos MIF de um site secundário para seu site pai.|Servidor do site secundário|  
|sinvproc.log|Registra informações sobre o processamento de dados de inventário de software para o banco de dados do site.|Servidor do site|  

###  <a name="a-namebkmkmeteringloga-metering"></a><a name="BKMK_MeteringLog"></a> Medição  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas à medição.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Monitora todos os processos de medição de software.|Servidor do site|  

###  <a name="a-namebkmkmigrationloga-migration"></a><a name="BKMK_MigrationLog"></a> Migração  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas à migração.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|migmctrl.log|Registra as informações sobre as ações de migração que envolvem trabalhos de migração, pontos de distribuição compartilhados e atualizações do ponto de distribuição.|O site de nível superior na hierarquia do Configuration Manager e cada site primário filho<br /><br /> Em uma hierarquia de vários sites primários, use o arquivo de log criado no site de administração central.|  

###  <a name="a-namebkmkmdmloga-mobile-devices"></a><a name="BKMK_MDMLog"></a> Dispositivos móveis  
 As seções a seguir listam os arquivos de log que contêm informações relacionadas ao gerenciamento de dispositivos móveis.  

####  <a name="a-namebkmkenrollmentloga-enrollment"></a><a name="BKMK_EnrollmentLog"></a> Registro  
 A tabela a seguir lista os logs que contêm informações relacionadas ao registro do dispositivo móvel.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|DMPRP.log|Registra a comunicação entre os pontos de gerenciamento habilitados para dispositivos móveis e os pontos de extremidade do ponto de gerenciamento.|Servidor do sistema de site|  
|dmpmsi.log|Registra os dados do Windows Installer para a configuração de um ponto de gerenciamento habilitado para dispositivos móveis.|Servidor do sistema de site|  
|DMPSetup.log|Registra a configuração do ponto de gerenciamento quando ele está habilitado para dispositivos móveis.|Servidor do sistema de site|  
|enrollsrvMSI.log|Registra os dados do Windows Installer para a configuração de um ponto de registro.|Servidor do sistema de site|  
|enrollmentweb.log|Registra a comunicação entre os dispositivos móveis e o ponto proxy do registro.|Servidor do sistema de site|  
|enrollwebMSI.log|Registra os dados do Windows Installer para a configuração de um ponto proxy do registro.|Servidor do sistema de site|  
|enrollmentservice.log|Registra a comunicação entre um ponto proxy do registro e um ponto de registro.|Servidor do sistema de site|  
|SMS_DM.log|Registra a comunicação entre os dispositivos móveis, os computadores Mac e o ponto de gerenciamento habilitado para dispositivos móveis e computadores Mac.|Servidor do sistema de site|  

####  <a name="a-namebkmkexchsrvloga-exchange-server-connector"></a><a name="BKMK_ExchSrvLog"></a> Conector do Exchange Server  
 A tabela a seguir lista os logs que contêm informações relacionadas ao conector do Exchange Server.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|easdisc.log|Registra as atividades e o status do conector do Exchange Server.|Servidor do site|  

####  <a name="a-namebkmkmdlegloga-mobile-device-legacy"></a><a name="BKMK_MDLegLog"></a> Herdado de dispositivo móvel  
 A tabela a seguir lista os logs que contêm informações relacionadas ao cliente herdado de dispositivos móveis.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|DmCertEnroll.log|Registra detalhes sobre os dados de registro de certificado em clientes herdados de dispositivos móveis.|Cliente|  
|DMCertResp.htm|Registra a resposta HTML do servidor de certificado quando o programa registrador de cliente herdado de dispositivo móvel solicita um certificado PKI.|Cliente|  
|DmClientHealth.log|Registra os GUIDs de todos os clientes herdados de dispositivo móvel que se comunicam com o ponto de gerenciamento habilitado para dispositivos móveis.|Servidor do sistema de site|  
|DmClientRegistration.log|Registra as solicitações e respostas de registro de e para clientes herdados de dispositivo móvel.|Servidor do sistema de site|  
|DmClientSetup.log|Registra os dados da configuração de cliente para clientes herdados de dispositivo móvel.|Cliente|  
|DmClientXfer.log|Registra os dados de transferência do cliente para clientes herdados de dispositivo móvel e para implantações do ActiveSync.|Cliente|  
|DmCommonInstaller.log|Registra a instalação do arquivo de transferência de cliente para a configuração de arquivos de transferência de cliente herdado de dispositivo móvel.|Cliente|  
|DmInstaller.log|Registra se o DMInstaller chama corretamente o DmClientSetup, e se o DmClientSetup sai com êxito ou falha em clientes herdados de dispositivo móvel.|Cliente|  
|DmpDatastore.log|Registra todas as conexões de banco de dados do site e consultas feitas pelo ponto de gerenciamento habilitado para dispositivos móveis.|Servidor do sistema de site|  
|DmpDiscovery.log|Registra todos os dados da descoberta dos clientes herdados de dispositivo móvel no ponto de gerenciamento habilitado para dispositivos móveis.|Servidor do sistema de site|  
|DmpHardware.log|Registra os dados de inventário de hardware dos clientes herdados de dispositivo móvel no ponto de gerenciamento habilitado para dispositivos móveis.|Servidor do sistema de site|  
|DmpIsapi.log|Registra a comunicação do cliente herdado de dispositivo móvel com um ponto de gerenciamento habilitado para dispositivos móveis.|Servidor do sistema de site|  
|dmpmsi.log|Registra os dados do Windows Installer para a configuração de um ponto de gerenciamento habilitado para dispositivos móveis.|Servidor do sistema de site|  
|DMPSetup.log|Registra a configuração do ponto de gerenciamento quando ele está habilitado para dispositivos móveis.|Servidor do sistema de site|  
|DmpSoftware.log|Registra os dados de distribuição de software dos clientes herdados de dispositivo móvel no ponto de gerenciamento habilitado para dispositivos móveis.|Servidor do sistema de site|  
|DmpStatus.log|Registra os dados das mensagens de status dos clientes de dispositivo móvel no ponto de gerenciamento habilitado para dispositivos móveis.|Servidor do sistema de site|  
|DmSvc.log|Registra a comunicação de cliente dos clientes herdados de dispositivo móvel com um ponto de gerenciamento habilitado para dispositivos móveis.|Cliente|  
|FspIsapi.log|Registra detalhes sobre comunicações com o ponto de status de fallback de clientes herdados de dispositivos móveis e computadores cliente.|Servidor do sistema de site|  

###  <a name="a-namebkmkosdloga-operating-system-deployment"></a><a name="BKMK_OSDLog"></a> Implantação de sistema operacional  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas à implantação de sistema operacional.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|CAS.log|Registra detalhes quando os pontos de distribuição são encontrados para o conteúdo referenciado.|Cliente|  
|ccmsetup.log|Registra as tarefas da **ccmsetup** para instalação, atualização e remoção do cliente. Pode ser usado para solucionar problemas de instalação do cliente.|Cliente|  
|CreateTSMedia.log|Registra detalhes para a criação de mídia de sequência de tarefas.|O computador que executa o console do Configuration Manager|  
|DeployToVhd.log|Registra detalhes sobre o processo de criação e modificação do VHD|O computador que executa o console do Configuration Manager|  
|Dism.log|Registra as ações de instalação de driver ou as ações de aplicação de atualização para a instalação offline.|Servidor do sistema de site|  
|distmgr.log|Registra detalhes sobre a configuração de habilitação de um ponto de distribuição para PXE.|Servidor do sistema de site|  
|DriverCatalog.log|Registra os detalhes sobre drivers de dispositivo importados para o catálogo de drivers.|Servidor do sistema de site|  
|mcsisapi.log|Registra as informações de transferência de pacote de multicast e respostas de solicitação de cliente.|Servidor do sistema de site|  
|mcsexec.log|Registra as ações de verificação de integridade, namespace, criação de sessão e verificação de certificado.|Servidor do sistema de site|  
|mcsmgr.log|Registra as alterações na configuração, no modo de segurança e na disponibilidade.|Servidor do sistema de site|  
|mcsprv.log|Registra a interação do provedor de multicast com os Serviços de Implantação do Windows (WDS).|Servidor do sistema de site|  
|MCSSetup.log|Registra os detalhes sobre a instalação da função de servidor multicast.|Servidor do sistema de site|  
|MCSMSI.log|Registra os detalhes sobre a instalação da função de servidor multicast.|Servidor do sistema de site|  
|Mcsperf.log|Registra os detalhes sobre as atualizações do contador de desempenho multicast.|Servidor do sistema de site|  
|MP_ClientIDManager.log|Registra as respostas do ponto de gerenciamento para as sequências de tarefas de solicitações de ID do cliente, iniciadas por meio do PXE ou da mídia de inicialização.|Servidor do sistema de site|  
|MP_DriverManager.log|Registra as respostas do ponto de gerenciamento às solicitações de ação da sequência de tarefas do driver de aplicação automática.|Servidor do sistema de site|  
|OfflineServicingMgr.log|Registra os detalhes de agendamentos de instalação offline e ações de aplicação de atualização em arquivos .wim do sistema operacional.|Servidor do sistema de site|  
|Setupact.log|Registra os detalhes sobre os logs do Windows Sysprep e de instalação.|Cliente|  
|Setupapi.log|Registra os detalhes sobre os logs do Windows Sysprep e de instalação.|Cliente|  
|Setuperr.log|Registra os detalhes sobre os logs do Windows Sysprep e de instalação.|Cliente|  
|smpisapi.log|Registra os detalhes sobre as ações de captura e restauração do estado do cliente, e informações de limite.|Cliente|  
|Smpmgr.log|Registra os detalhes sobre os resultados de verificações de integridade do ponto de migração de estado e de alterações de configuração.|Servidor do sistema de site|  
|smpmsi.log|Registra os detalhes de instalação e configuração do ponto de migração de estado.|Servidor do sistema de site|  
|smpperf.log|Registra as atualizações do contador de desempenho do ponto de migração de estado.|Servidor do sistema de site|  
|smspxe.log|Registra os detalhes das respostas a clientes que o PXE inicializa e detalhes da expansão de imagens e arquivos de inicialização.|Servidor do sistema de site|  
|smssmpsetup.log|Registra os detalhes de instalação e configuração do ponto de migração de estado.|Servidor do sistema de site|  
|Smsts.log|Registra as atividades de sequência de tarefas.|Cliente|  
|TSAgent.log|Registra o resultado das dependências da sequência de tarefas antes de iniciar uma sequência de tarefas.|Cliente|  
|TaskSequenceProvider.log|Registra os detalhes das sequências de tarefas quando elas são importadas, exportadas ou editadas.|Servidor do sistema de site|  
|loadstate.log|Registra os detalhes da USMT (Ferramenta de Migração de Perfil do Usuário) e da restauração dos dados de estado do usuário.|Cliente|  
|scanstate.log|Registra os detalhes da USMT (Ferramenta de Migração de Perfil do Usuário) e captura dos dados de estado do usuário.|Cliente|  

###  <a name="a-namebkmkpowermgmtloga-power-management"></a><a name="BKMK_PowerMgmtLog"></a> Gerenciamento de energia  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas ao gerenciamento de energia.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|Pwrmgmt.log|Registra os detalhes sobre as atividades de gerenciamento de energia no computador cliente, inclusive o monitoramento e a imposição de configurações pelo agente cliente de gerenciamento de energia.|Cliente|  

###  <a name="a-namebkmkrcloga-remote-control"></a><a name="BKMK_RCLog"></a> Controle remoto  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas ao controle remoto.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|Registra os detalhes sobre a atividade do visualizador de controle remoto.|Localizado na pasta *%temp%* no computador que executa o visualizador de controle remoto.|  

###  <a name="a-namebkmkreportloga-reporting"></a><a name="BKMK_ReportLog"></a> Relatórios  
 A tabela a seguir lista os arquivos de log do Configuration Manager que contêm informações relacionadas a relatórios.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|srsrp.log|Registra as informações sobre a atividade e o status do ponto do Reporting Services.|Servidor do sistema de site|  
|srsrpMSI.log|Registra os resultados detalhados do processo de instalação de ponto do Reporting Services por meio da saída do MSI.|Servidor do sistema de site|  
|srsrpsetup.log|Registra os resultados do processo de instalação do ponto do Reporting Services.|Servidor do sistema de site|  

###  <a name="a-namebkmkrbaloga-role-based-administration"></a><a name="BKMK_RBALog"></a> Administração baseada em funções  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas ao gerenciamento da administração baseada em funções.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|hman.log|Registra as informações sobre as alterações de configuração do site e a publicação de informações do site nos Serviços de Domínio Active Directory.|Servidor do site|  
|SMSProv.log|Registra o acesso do provedor WMI ao banco de dados do site.|Computador com o Provedor de SMS|  

###  <a name="a-namebkmkwitloga-service-connection-point"></a><a name="BKMK_WITLog"></a> Ponto de conexão de serviço  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas ao ponto de conexão de serviço.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|Registra informações de certificado e conta proxy.|Servidor do site|  
|colleval.log|Registra detalhes sobre quando as coleções são criadas, alteradas e excluídas pelo Collection Evaluator.|Site primário e site de administração central|  
|Cloudusersync.log|Registra habilitação de licença para usuários.|Computador com o ponto de conexão de serviço|  
|dataldr.log|Registra informações sobre o processamento de arquivos MIF.|Servidor do site|  
|ddm.log|Registra as atividades do gerenciador de dados de descoberta.|Servidor do site|  
|distmgr.log|Registra detalhes sobre solicitações de distribuição de conteúdo.|Servidor do site de nível superior|  
|Dmpdownloader.log|Registra detalhes sobre downloads do Microsoft Intune.|Computador com o ponto de conexão de serviço|  
|Dmpuploader.log|Registra detalhes para carregar alterações de banco de dados para o Microsoft Intune.|Computador com o ponto de conexão de serviço|  
|hman.log|Registra informações sobre o encaminhamento de mensagens.|Servidor do site|  
|objreplmgr.log|Registra o processamento de política e atribuição.|Servidor do site primário|  
|policypv.log|Registra a geração de políticas de todas as políticas.|Servidor do site|  
|outgoingcontentmanager.log|Registra conteúdo carregado para o Microsoft Intune.|Computador com o ponto de conexão de serviço|  
|sitecomp.log|Registra detalhes da instalação do ponto de conexão de serviço.|Servidor do site|  
|SmsAdminUI.log|Registra atividades do console do Configuration Manager.|Computador que executa o console do Configuration Manager|  
|SMSProv.log|Registra as atividades executadas pelo Provedor de SMS. As atividades do console do Configuration Manager usam o Provedor de SMS.|Computador com o Provedor de SMS|  
|SrvBoot.log|Registra detalhes sobre o serviço de instalação do ponto de conexão de serviço.|Computador com o ponto de conexão de serviço|  
|statesys.log|Registra o processamento de mensagens de gerenciamento de dispositivo móvel.|Site primário e site de administração central|  

###  <a name="a-namebkmksunaploga-software-updates"></a><a name="BKMK_SU_NAPLog"></a> Atualizações de software  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas a atualizações de software.  Além disso, alguns detalhes permanecem relacionados à Proteção de Acesso à Rede, um recurso que não está mais disponível com o System Center Configuration Manager.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|ccmcca.log|Registra detalhes sobre o processamento da avaliação de conformidade baseada no processamento da política de NAP do Configuration Manager, e contém o processamento de correção para cada atualização de software necessária à conformidade.|Cliente|  
|Ccmperf.log|Registra as atividades relacionadas à manutenção e captura de dados referentes aos contadores de desempenho de cliente.|Cliente|  
|PatchDownloader.log|Registra detalhes sobre o processo de baixar atualizações de software da fonte de atualizações para o destino de download no servidor de site.|O computador que hospeda o console do Configuration Manager no qual os downloads são iniciados|  
|PolicyEvaluator.log|Registra os detalhes sobre a avaliação de políticas em computadores cliente, incluindo as políticas de atualizações de software.|Cliente|  
|RebootCoordinator.log|Registra os detalhes sobre a coordenação da reinicialização do sistema em computadores cliente após as instalações de atualização de software.|Cliente|  
|ScanAgent.log|Registra os detalhes sobre as solicitações de verificação de atualizações de software, a localização do WSUS e ações relacionadas.|Cliente|  
|SdmAgent.log|Registra os detalhes sobre o controle de correção e conformidade. No entanto, o arquivo de log das atualizações de software, o Updateshandler.log, fornece mais informações sobre a instalação das atualizações de software necessárias à conformidade.<br /><br /> Esse arquivo de log é compartilhado com configurações de conformidade.|Cliente|  
|ServiceWindowManager.log|Registra os detalhes sobre a avaliação de janelas de manutenção.|Cliente|  
|smssha.log|O arquivo de log principal do cliente de Proteção de Acesso à Rede do Configuration Manager, que contém informações de declaração de integridade mescladas dos dois componentes do Configuration Manager: LS (serviços de localização) e o CCA (agente de conformidade de configuração). Esse arquivo de log também contém informações sobre as interações entre o agente de integridade do sistema do Configuration Manager e o agente NAP do sistema operacional, e também entre o agente de integridade do sistema do Configuration Manager e o agente de conformidade de configuração e os serviços de localização. Ele fornece informações sobre se o agente NAP foi inicializado com êxito e sobre os dados e a segurança da declaração de integridade.|Cliente|  
|Smsshv.log|Esse é o arquivo de log principal para o ponto do validador da integridade do sistema e registra as operações básicas do serviço do validador da integridade do sistema, como o progresso da inicialização.|Servidor do sistema de site|  
|Smsshvadcacheclient.log|Registra detalhes sobre a recuperação das referências do estado de integridade do Configuration Manager do Active Directory Domain Services.|Servidor do sistema de site|  
|SmsSHVCacheStore.log|Registra os detalhes sobre o repositório em cache usado para manter as referências do estado de integridade NAP do Configuration Manager, recuperadas por meio do Active Directory Domain Services, como a leitura do repositório e a limpeza das entradas do arquivo de repositório em cache local. O armazenamento em cache não é configurável.|Servidor do sistema de site|  
|smsSHVQuarValidator.log|Registra as informações da declaração de integridade do cliente e de operações de processamento. Para obter informações completas, altere a chave do Registro **LogLevel** de 1 para 0 no seguinte local: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMSSHV\Logging\\@GLOBAL**|Servidor do sistema de site|  
|smsshvregistrysettings.log|Registra qualquer alteração dinâmica na configuração do componente do validador da integridade do sistema enquanto o serviço estiver sendo executado.|Servidor do sistema de site|  
|SMSSHVSetup.log|Registra o êxito ou a falha (com a causa da falha) da instalação do ponto do validador da integridade do sistema.|Servidor do sistema de site|  
|SmsWusHandler.log|Registra os detalhes sobre o processo de digitalização para a ferramenta de inventário do Microsoft Updates.|Cliente|  
|StateMessage.log|Registra os detalhes sobre as mensagens de estado de atualizações de software criadas e enviadas ao ponto de gerenciamento.|Cliente|  
|SUPSetup.log|Registra os detalhes sobre a instalação do ponto de atualização de software. Quando a instalação do ponto de atualização de software é concluída, **Installation was successful** é gravado nesse arquivo de log.|Servidor do sistema de site|  
|UpdatesDeployment.log|Registra os detalhes sobre as implantações no cliente, incluindo a ativação, a avaliação e a imposição da atualização de software. O registro extenso mostra informações adicionais sobre a interação com a interface de usuário cliente.|Cliente|  
|UpdatesHandler.log|Registra os detalhes sobre a verificação de conformidade da atualização de software e sobre o download e a instalação de atualizações de software no cliente.|Cliente|  
|UpdatesStore.log|Registra os detalhes sobre o status de conformidade para as atualizações de software avaliadas durante o ciclo de verificação de conformidade.|Cliente|  
|WCM.log|Registra detalhes sobre configurações do ponto de atualização de software e conexões ao servidor do WSUS (Windows Server Update Services) para categorias de atualização assinadas, classificações e idiomas.|Servidor do site|  
|WSUSCtrl.log|Registra os detalhes sobre a configuração, a conectividade de banco de dados e a integridade do servidor do WSUS para o site.|Servidor do sistema de site|  
|wsyncmgr.log|Registra detalhes sobre o processo de sincronização de atualizações de software.|Servidor do site|  
|WUAHandler.log|Registra detalhes sobre o Windows Update Agent no cliente quando ele procura por atualizações de software.|Cliente|  

###  <a name="a-namebkmkwolloga-wake-on-lan"></a><a name="BKMK_WOLLog"></a> Wake On LAN  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas ao uso de Wake on LAN.  

> [!NOTE]  
>  Quando você suplementa o Wake On LAN usando proxy de ativação, essa atividade será registrada no cliente. Por exemplo, consulte CcmExec.log e SleepAgent_&lt;domínio\>@SYSTEM_0.log na seção [Operações de Cliente](#BKMK_ClientOpLogs) neste tópico.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|Registra detalhes sobre a quais clientes precisam ser enviados pacotes de ativação, o número de pacotes de ativação enviados e o número de pacotes de ativação repetidos.|Servidor do site|  
|wolmgr.log|Registra detalhes sobre os procedimentos de ativação, como quando as implantações de ativação são configuradas para Wake On LAN.|Servidor do site|  

###  <a name="a-namebkmkwuloga-windows-update-agent"></a><a name="BKMK_WULog"></a> Windows Update Agent  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas ao Windows Update Agent.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|Registra detalhes sobre quando o Windows Update Agent se conecta ao servidor do WSUS e recupera as atualizações de software para avaliação de conformidade, se houver atualizações para os componentes do agente.|Cliente|  

###  <a name="a-namebkmkwsusloga-wsus-server"></a><a name="BKMK_WSUSLog"></a> Servidor do WSUS  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas ao servidor do WSUS.  

|Nome do log|Descrição|Computador com o arquivo de log|  
|--------------|-----------------|----------------------------|  
|Change.log|Registra detalhes sobre as informações de banco de dados do servidor do WSUS alteradas.|Servidor do WSUS|  
|SoftwareDistribution.log|Registra detalhes sobre as atualizações de software sincronizadas da origem de atualização configurada para o banco de dados do servidor do WSUS.|Servidor do WSUS|  



<!--HONumber=Nov16_HO1-->


