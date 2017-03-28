---
title: "Backup e recuperação | Microsoft Docs"
description: Saiba como fazer o backup e recuperar seus sites em caso de falha ou perda de dados no System Center Configuration Manager.
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
caps.latest.revision: 22
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1b9e49da1a5bbfca93fe683b82d2c0056a22cc1f
ms.openlocfilehash: 67441d0c19114f628e8b4308f58165ba67c738df
ms.lasthandoff: 03/21/2017

---

# <a name="backup-and-recovery"></a>Backup e descoberta

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Prepare abordagens de backup e recuperação para evitar perda de dados. Para sites do Configuration Manager uma abordagem de backup e recuperação pode ajudar a recuperar sites e hierarquias mais rapidamente e com o mínimo de perda de dados. As seções neste tópico podem ajudá-lo a fazer o backup de seus sites e recuperar um site em caso de falha ou perda de dados.  



- [Fazer backup de um site do Configuration Manager](#BKMK_SiteBackup)   

  - [Tarefa de manutenção de backup](#BKMK_BackupMaintenanceTask)   

  - [Usando o Data Protection Manager para fazer backup do banco de dados do site](#BKMK_DPMBackup)   

  -  [Arquivando o instantâneo de backup](#BKMK_ArchivingBackupSnapshot)   

  -  [Usando o arquivo AfterBackup.bat](#BKMK_UsingAfterBackup)   

  -  [Tarefas de backup complementares](#BKMK_SupplementalBackup)   

-  [Recuperar um site do Configuration Manager](#BKMK_RecoverSite)   

  -   [Determinar as opções de recuperação](#BKMK_DetermineRecoveryOptions)   

         -   [Opções de recuperação do servidor do site](#BKMK_SiteServerRecoveryOptions)   

         -   [Opções de recuperação do banco de dados do site](#BKMK_SiteDatabaseRecoveryOption)   

         -   [Período de retenção do controle de alterações do SQL Server](#bkmk_SQLretention)   

         -   [Processo para reinicializar o site ou dados globais](#bkmk_reinit)   

         -   [Cenários de recuperação de banco de dados do site](#BKMK_SiteDBRecoveryScenarios)  

  -   [Chaves de arquivo de script de recuperação autônoma do site](#BKMK_UnattendedSiteRecoveryKeys)  

  -   [Tarefas de pós-recuperação](#BKMK_PostRecovery)  

  -   [Recuperar um site secundário](#BKMK_RecoverSecondarySite)  

-   [Serviço SMS Writer](#BKMK_SMSWriterService)  

> [!NOTE]  
>  Se você usa um grupo de disponibilidade AlwaysOn do SQL Server para hospedar o banco de dados do site, modifique seus planos de backup e recuperação conforme descrito na seção [Alterações de backup e recuperação quando você usa um grupo de disponibilidade AlwaysOn do SQL Server](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#bkmk_BnR) do tópico [AlwaysOn do SQL Server para um banco de dados do site altamente disponível do System Center Configuration Manager](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

##  <a name="BKMK_SiteBackup"></a> Fazer backup de um site do Configuration Manager  
 O Configuration Manager tem uma tarefa de manutenção de backup que:  

-   É executada conforme um agendamento  

-   Faz backup do banco de dados do site  

-   Faz backup de chaves específicas do Registro  

-   Faz backup de arquivos e pastas específicas  

-   Faz backup da pasta **CD.Latest**  (Consulte [A pasta CD.Latest do System Center Configuration Manager](../../core/servers/manage/the-cd.latest-folder.md))  

 Planeje executar a tarefa padrão de backup do site, no mínimo, a cada 5 dias. Isso ocorre porque o Configuration Manager usa um [Período de retenção do controle de alterações do SQL Server](#bkmk_SQLretention) de 5 dias.  

 Para simplificar o processo de backup, é possível criar o arquivo **AfterBackup.bat** para executar ações pós-backup automaticamente depois de executar a tarefa de manutenção de backup com êxito. O arquivo AfterBackup.bat é normalmente é usado para arquivar o instantâneo de backup em um local seguro. Também é possível usar o arquivo AfterBackup.bat para copiar arquivos para a pasta de backup e iniciar outras tarefas de backup complementares.

Use as seções a seguir para ajudá-lo a criar sua estratégia de backup do Configuration Manager.  

> [!NOTE]  
>  O Configuration Manager pode recuperar o banco de dados do site por meio da tarefa de manutenção de backup do Configuration Manager ou de um backup do banco de dados do site criado com outro processo. Por exemplo, é possível restaurar o banco de dados do site por um backup criado como parte de um plano de manutenção do Microsoft SQL Server. Você pode restaurar o banco de dados do site por meio de um backup criado usando o System Center 2012 DPM (Data Protection Manager). Para obter mais informações, consulte [Usando o Data Protection Manager para fazer backup do banco de dados do site](#BKMK_DPMBackup).  

###  <a name="BKMK_BackupMaintenanceTask"></a> Tarefa de manutenção de backup  
 É possível automatizar o backup de sites do Configuration Manager agendando a tarefa de manutenção Servidor do Site de Backup predefinida. É possível fazer backup de um site de administração central e de um site primário, mas não há suporte de backup para sites secundários ou servidores de sistema de site. Quando o serviço de backup do Configuration Manager é executado, ele segue as instruções definidas no arquivo de controle de backup (**&lt;PastaDeInstalaçãoDoConfigMgr\>\Inboxes\Smsbkup.box\Smsbkup.ctl**). É possível modificar o arquivo de controle de backup para alterar o comportamento do serviço de backup. As informações de status de backup do site são gravadas no arquivo **Smsbkup.log** . O arquivo é criado na pasta de destino especificada nas propriedades da tarefa de manutenção Servidor do Site de Backup.  


##### <a name="to-enable-the-site-backup-maintenance-task"></a>Para habilitar a tarefa de manutenção de backup do site  

1.  No console do Configuration Manager, abra **Administração** > **Configuração do Site**  

     \> **Sites**.  

2.  Selecione o site no qual deseja habilitar a tarefa de manutenção de backup do site.  

3.  Na guia **Início**, no grupo **Configurações**, escolha **Tarefas de Manutenção do Site**.  

4.  Escolha **Servidor do Site de Backup**  >  **Editar**.  

5.  Escolha **Habilitar esta tarefa** > **Definir Caminhos** para especificar o destino do backup. Você tem as seguintes opções:  

    > [!IMPORTANT]  
    >  Para ajudar a evitar a violação dos arquivos de backup, armazene os arquivos em um local seguro. O caminho de backup mais seguro é uma unidade local, para que possibilite definir permissões do sistema de arquivos NTFS na pasta. O Configuration Manager não criptografa os dados de backup armazenados no caminho do backup.  

    -   **Unidade local no servidor do site para dados e banco de dados do site**: especifica que os arquivos de backup do site e do banco de dados do site são armazenados no caminho especificado na unidade de disco local do servidor do site. É necessário criar a pasta local para poder executar a tarefa de backup.   A conta Sistema Local no servidor do site deve ter permissões de **Gravação** no sistema de arquivos NTFS para a pasta local do backup do servidor do site. A conta Sistema Local no computador que está executando o SQL Server deve ter permissões de **Gravação** NTFS para a pasta do backup do banco de dados do site.  

    -   **Caminho de rede (nome UNC) para dados e banco de dados do site**: especifica que os arquivos de backup do site e do banco de dados do site são armazenados no caminho UNC especificado. Você deve criar o compartilhamento antes de executar a tarefa de backup. A conta de computador do servidor do site e a conta de computador do SQL Server, se o SQL Server estiver instalado em outro computador, deverão ter permissões de **Gravação** NTFS e compartilhar permissões para a pasta de rede compartilhada.  

    -   **Unidades locais no servidor do site e no SQL Server**: especifica que os arquivos de backup do site são armazenados no caminho especificado na unidade local do servidor do site e que os arquivos de backup do banco de dados do site são armazenados no caminho especificado na unidade local do servidor de banco de dados do site. É necessário criar as pastas locais para poder executar a tarefa de backup. A conta de computador do servidor do site deve ter permissões de **Gravação** NTFS para a pasta criada no servidor do site. A conta de computador do SQL Server deve ter permissões de **Gravação** NTFS para a pasta criada no servidor de banco de dados do site. Essa opção está disponível somente quando o banco de dados do site não está instalado no servidor do site.  

    > [!NOTE]  
    >    - A opção de navegar até o destino do backup está disponível somente quando o caminho UNC do destino do backup é especificado.

    > - O nome da pasta ou do compartilhamento usado como destino do backup não oferece suporte ao uso de caracteres Unicode.  


6.  Configure um agendamento para a tarefa de backup do site. Como prática recomendada, considere agendar a execução do backup para fora do horário de trabalho ativo. Se houver uma hierarquia, considere agendar a execução para no mínimo duas vezes por semana para garantir a máximo retenção de dados em caso de falha do site.  

    Ao executar o console do Configuration Manager no mesmo servidor do site em que o backup está sendo configurado, a tarefa de manutenção Servidor do Site de Backup usa a hora local para o agendamento. Quando o console do Configuration Manager é executado em um computador remoto do site que está sendo configurado para backup, a tarefa de manutenção Servidor do Site de Backup usa o horário UTC para o agendamento.  

7.  Escolha se um alerta deve ser criado caso a tarefa de backup do site falhe, clique em **OK** e em **OK** novamente. Quando selecionado, o Configuration Manager cria um alerta crítico para a falha do backup, que pode ser visto no nó **Alertas** do espaço de trabalho **Monitoramento**.  

 Em seguida, verifique se a tarefa de manutenção Servidor do Site de Backup está em execução para garantir que os backups estão sendo criadas.  

##### <a name="to-verify-that-the-backup-site-server-maintenance-task-is-running"></a>Para verificar se a tarefa de manutenção Servidor do Site de Backup está em execução  

-   Verifique se a tarefa de manutenção Site de Backup está em execução conferindo o seguinte:  

    -   Confira o carimbo de data/hora dos arquivos na pasta de destino do backup que a tarefa criou. Verifique se o carimbo de data/hora foi atualizado com uma hora que coincida com a hora em que a tarefa foi agendada para ser executada pela última vez.  

    -   No nó **Status do Componente** do espaço de trabalho **Monitoramento** , confira as mensagens de status de SMS_SITE_BACKUP. Quando o backup do site for concluído com êxito, você verá a mensagem ID 5035, que indica que o backup do site foi concluído sem erros.  

    -   Quando a tarefa de manutenção Servidor do Site de Backup estiver configurada para criar um alerta em caso de falha do backup, é possível verificar as falhas de backup no nó **Alertas** do espaço de trabalho **Monitoramento** .  

    -   Em &lt;*PastaDeInstalaçãoDoConfigMgr*>\Logs, verifique se há avisos e erros em Smsbkup.log. Quando o backup do site for concluído com êxito, você verá `Backup completed` com um carimbo de data e hora e a ID de mensagem `STATMSG: ID=5035`.  

    > [!TIP]  
    >  Quando a tarefa de manutenção de backup falha, é possível reiniciá-la interrompendo e reiniciando o serviço SMS_SITE_BACKUP.  

###  <a name="BKMK_DPMBackup"></a> Usando o Data Protection Manager para fazer backup do banco de dados do site  
 Você pode usar o System Center 2012 Data Protection Manager (DPM) para fazer backup do banco de dados do site. É necessário criar um novo grupo de proteção no DPM para o computador do banco de dados do site. Na página **Selecionar Membros do Grupo** do Assistente para Criar Novo Grupo de Proteção, selecione o serviço SMS Writer na lista de fontes de dados e selecione o banco de dados do site como membro apropriado. Para obter mais informações sobre como usar o DPM para fazer backup do banco de dados do site, consulte a [Biblioteca de Documentação do Data Protection Manager](http://go.microsoft.com/fwlink/?LinkId=272772) no TechNet.  

> [!IMPORTANT]  
>  O Configuration Manager não dá suporte ao backup do DPM para um cluster do SQL Server que usa uma instância nomeada, mas dá suporte ao backup do DPM em um cluster do SQL Server que usa a instância padrão do SQL Server.  

 Depois de restaurar o banco de dados do site, siga as etapas da Instalação para recuperar o site. Selecione a opção de recuperação **Usar um banco de dados do site recuperado manualmente** para usar o banco de dados do site recuperado com o uso do Data Protection Manager.  

###  <a name="BKMK_ArchivingBackupSnapshot"></a> Arquivando o instantâneo de backup  
 A primeira vez que a tarefa de manutenção Servidor do Site de Backup é executada, um instantâneo de backup é criado, e você pode usá-lo para recuperar o servidor do site em caso de falha. Quando a tarefa de backup é executada novamente durante ciclos subsequentes, é criado um novo instantâneo de backup que substitui o instantâneo anterior. Consequentemente, o site fica com apenas um instantâneo de backup e não há como recuperar um instantâneo de backup anterior.  

 Como prática recomendada, mantenha diversos arquivos de instantâneo de backup, pelos seguintes motivos:  

-   É comum que a mídia de backup falhe, seja extraviada ou contenha apenas um backup parcial. Recuperar um site primário autônomo com falha de um backup mais antigo é melhor do que recuperar sem qualquer backup. Para um servidor de site em uma hierarquia, o backup deve estar no período de retenção do controle de alterações do SQL Server, ou o backup não será necessário.  

-   Uma corrupção no site pode não ser detectada durante vários ciclos de backup. Pode ser necessário usar um instantâneo de backup anterior à corrupção do site. Isso se aplica a um site primário autônomo e a sites em uma hierarquia em que o backup está no período de retenção do controle de alterações do SQL Server.  

-   O site poderá não ter nenhum instantâneo de backup, se, por exemplo, a tarefa de manutenção de servidor do site de backup falhar. Como a tarefa de backup remove o instantâneo de backup anterior antes de começar a fazer o backup dos dados atuais, não haverá um instantâneo de backup válido.  

###  <a name="BKMK_UsingAfterBackup"></a> Usando o arquivo AfterBackup.bat  
 Após o backup bem-sucedido do site, a tarefa do Servidor do Site de Backup tentará executar automaticamente um arquivo chamado AfterBackup.bat. Você deve criar manualmente o arquivo AfterBackup.bat em &lt;*PastaDeInstalaçãoDoConfigMgr*>\Inboxes\Smsbkup. Se existir um arquivo AfterBackup.bat e ele estiver armazenado na pasta correta, ele será executado automaticamente depois que a tarefa de backup for concluída. O arquivo AfterBackup.bat permite arquivar o instantâneo de backup no final de cada operação de backup, e executa automaticamente outras tarefas pós-backup que não fazem parte da tarefa de manutenção do servidor do site de backup. O arquivo AfterBackup.bat integra o arquivo e as operações de backup, garantindo assim que cada novo instantâneo de backup seja arquivado. Quando o arquivo AfterBackup.bat não está presente, a tarefa de backup a ignora sem efeito sobre a operação de backup. Para verificar se a tarefa de backup do site executou com sucesso o arquivo AfterBackup.bat, consulte o nó **Status do Componente** no espaço de trabalho **Monitoramento** e verifique as mensagens de status de SMS_SITE_BACKUP. Quando a tarefa inicia com êxito o arquivo de comando AfterBackup.bat, você vê uma mensagem ID 5040.  

> [!TIP]  
>  Para criar o arquivo AfterBackup.bat para arquivar os arquivos de backup do servidor do site, você deve usar uma ferramenta de comando de cópia, como o Robocopy, no arquivo em lotes. Por exemplo, você pode criar o arquivo AfterBackup.bat, e na primeira linha, adicionar algo semelhante a: `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`. Para obter mais informações sobre o Robocopy, veja a página da Web de referência de linha de comando [Robocopy](http://go.microsoft.com/fwlink/p/?LinkId=228408) .  

 Embora o uso pretendido do AfterBackup.bat seja arquivar instantâneos de backup, você pode criar um arquivo AfterBackup.bat para executar tarefas adicionais ao final de cada operação de backup.  

###  <a name="BKMK_SupplementalBackup"></a> Tarefas de backup complementares  
 A tarefa de manutenção do servidor do site de backup fornece um instantâneo de backup para os arquivos do servidor do site e banco de dados do site, mas há outros itens sem backup que você deve considerar ao criar a estratégia de backup. Use as seções a seguir para ajudá-lo a concluir sua estratégia de backup do Configuration Manager.  

#### <a name="back-up-custom-reporting-services-reports"></a>Fazer backup de relatórios personalizados do Reporting Services  
 Quando você modifica ou cria relatórios personalizados do Reporting Services, criar backup para os arquivos de banco de dados do servidor é uma parte importante de sua estratégia de backup. O backup do servidor de relatórios deve incluir backup dos arquivos de origem para relatórios e modelos, chaves de criptografia, montagens ou extensões personalizadas, arquivos de configuração personalizados, visualizações do SQL Server usadas em relatórios personalizados, procedimentos de armazenamento personalizados, e assim por diante.  

> [!IMPORTANT]  
>  Quando o Configuration Manager é atualizado para uma versão mais recente, os relatórios predefinidos podem ser substituídos por novos relatórios. Se modificar um relatório predefinido, faça backup do relatório e restaure-o no Reporting Services.  

 Para obter mais informações sobre como fazer backup de relatórios personalizados no Reporting Services, veja [Operações de backup e restauração para uma instalação do Reporting Services](https://technet.microsoft.com/library/ms155814\(v=sql.120\).aspx) nos Manuais Online do SQL Server 2014.  

#### <a name="backup-content-files"></a>Fazer backup de arquivos de conteúdo  
 A biblioteca de conteúdo no Configuration Manager é o local que armazena todos os arquivos de conteúdo para atualizações de software, aplicativos, implantação de sistema operacional e assim por diante. A biblioteca de conteúdo está localizada no servidor do site e em cada ponto de distribuição. A tarefa de manutenção do servidor do site de backup não inclui um backup para a biblioteca de conteúdo ou para os diretórios de origem do pacote. Quando um servidor do site falha, as informações sobre os arquivos da biblioteca de conteúdo são restauradas no banco de dados do site, mas você deve restaurar a biblioteca de conteúdo e os diretórios de origem do pacote no servidor do site.  

-   **Biblioteca de conteúdo**: a biblioteca de conteúdo deve ser restaurada antes de redistribuir o conteúdo nos pontos de distribuição. Quando você começa a redistribuição do conteúdo, o Configuration Manager copia os arquivos da biblioteca de conteúdo no servidor do site para os pontos de distribuição. A biblioteca de conteúdo do servidor do site está na pasta SCCMContentLib, que normalmente fica localizada na unidade com mais espaço livre em disco quando o site foi instalado.  

-   **Arquivos de origem do pacote**: os arquivos de origem do pacote devem ser restaurados antes de atualizar o conteúdo nos pontos de distribuição. Quando você inicia uma atualização de conteúdo, o Configuration Manager copia arquivos novos ou modificados da origem do pacote na biblioteca de conteúdo, que por sua vez, copia os arquivos nos pontos de distribuição associados. É possível executar a seguinte consulta no SQL Server para encontrar o local de origem do pacote de todos os pacotes e aplicativos: `SELECT * FROM v_Package`. É possível identificar o site de origem do pacote observando os três primeiros caracteres da ID do pacote. Por exemplo, se a ID do pacote for CEN00001, o código do site de origem será CEN. Ao restaurar os arquivos de origem do pacote, eles devem ser restaurados no mesmo local em que estavam antes da falha.  

 Certifique-se de incluir a biblioteca de conteúdo e os diretórios de origem do pacote em seu backup de sistema de arquivos para o servidor do site.  

#### <a name="back-up-custom-software-updates"></a>Fazer backup de atualizações de software personalizadas  
 O System Center Updates Publisher 2011 é uma ferramenta autônoma que permite que você publique atualizações de software personalizadas no WSUS (Windows Server Update Services), sincronize-as com o Configuration Manager, avalie a conformidade das atualizações de software e implante-as nos clientes. O Updates Publisher usa um banco de dados local para seu repositório de atualização de software. Quando você usa o Updates Publisher para gerenciar atualizações de software personalizadas, determine se será necessário incluir o banco de dados do Updates Publisher em seu plano de backup. Para obter mais informações sobre o Updates Publisher, consulte [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) na biblioteca do System Center TechCenter.  

 Use o procedimento a seguir para fazer backup do banco de dados do Updates Publisher.  

###### <a name="to-back-up-the-updates-publisher-2011-database"></a>Para fazer o backup do banco de dados do Updates Publisher 2011  

1.  No computador que executa o Updates Publisher, navegue até o arquivo de banco de dados do Updates Publisher (Scupdb.sdf) em %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\\. Há um arquivo de banco de dados diferente para cada usuário que executa o Updates Publisher.  

2.  Copie o arquivo do banco de dados no destino de backup. Por exemplo, se o seu destino de backup for E:\ConfigMgr_Backup, você poderá copiar o arquivo de banco de dados do Updates Publisher para E:\ConfigMgr_Backup\SCUP2011.  

    > [!TIP]  
    >  Quando há mais de um arquivo de banco de dados em um computador, considere armazenar o arquivo em uma subpasta que indique o perfil do usuário associado ao arquivo de banco de dados. Por exemplo, pode haver um arquivo de banco de dados em E:\ConfigMgr_Backup\SCUP2011\User1 e outro em E:\ConfigMgr_Backup\SCUP2011\User2.  

### <a name="user-state-migration-data"></a>Dados de migração de estado do usuário  
 Você pode usar as sequências da tarefas do Configuration Manager para capturar e restaurar dados de estado do usuário em cenários de implantação do sistema operacional no qual você deseja manter o estado do usuário do sistema operacional atual. As pastas que armazenam os dados do estado do usuário são listadas nas propriedades do ponto de migração de estado. Esses dados de migração de estado do usuário não ganham backup como parte da tarefa de manutenção de backup do servidor do site. Como parte do plano de backup, você deve fazer backup manualmente das pastas especificadas para armazenar os dados de migração do estado do usuário.   

#### <a name="to-determine-the-folders-used-to-store-user-state-migration-data"></a>Para determinar as pastas usadas para armazenar dados de migração de estado do usuário  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração**, expanda **Configuração de Site** e escolha **Funções de Servidores e Sistema de Site**.  

3.  Selecione o sistema de sites que hospeda a função de migração de estado e escolha **Ponto de migração de estado** em **Funções do Sistema de Sites**.  


4.  Na guia **Função do Site** , no grupo **Propriedades** , clique em **Propriedades**.  
5.  As pastas que armazenam os dados de migração de estado do usuário estão listadas na seção **Detalhes da Pasta** na guia **Geral** .  

## <a name="recover-a-configuration-manager-site"></a>Recuperar um site do Configuration Manager
 Uma recuperação de site do Configuration Manager é necessária sempre que um site do Configuration Manager falha ou ocorre perda de dados no banco de dados do site. Reparação e nova sincronização de dados são as tarefas principais de uma recuperação de site para evitar a interrupção das operações.  

> [!IMPORTANT]  
>  Ao recuperar o banco de dados para um site:  

>  -   É necessário usar a mesma versão e edição do SQL Server. Por exemplo, não há suporte para restaurar um banco de dados executado no SQL Server 2012 para o SQL Server 2014. Da mesma forma, não há suporte para restaurar um banco de dados do site executado em uma Standard Edition do SQL Server 2014 para uma Enterprise Edition do SQL Server 2014.  
> -   O SQL Server não deve ser definido como **modo de usuário único**.  
> -   Certifique-se de que os arquivos .MDF e .LDF são válidos. Ao recuperar um site, não há verificação para o estado dos arquivos que estão sendo restaurados.  


 A recuperação de site é iniciada pela execução do Assistente de Instalação do Configuration Manager por meio da pasta CD.Latest.  Você também pode configurar o script de instalação autônoma e usar a opção **/script** de comando da Instalação para executar a instalação dessa mesma pasta CD.Latest. Suas opções de recuperação variam dependendo se você tiver um backup de banco de dados do site do Configuration Manager. Para obter mais informações, consulte [A pasta CD.Latest do System Center Configuration Manager](../../core/servers/manage/the-cd.latest-folder.md).  

> [!IMPORTANT]  
>  Se você executar a instalação do Configuration Manager por meio do menu **Iniciar** no servidor do site, a opção **Recuperar um site** não estará disponível.  

>  Se você tiver instalado atualizações de dentro do console do Configuration Manager antes de fazer o backup, não poderá reinstalar com êxito o site usando a instalação por meio da mídia de instalação ou o caminho de instalação do Configuration Manager.  

> [!NOTE]  
>  Após restaurar o banco de dados do site que estava configurado para as réplicas de banco de dados, reconfigure cada réplica para poder usá-las, recriando as publicações e assinaturas.  

###  <a name="BKMK_DetermineRecoveryOptions"></a> Determinar as opções de recuperação  
 Há duas áreas principais que você deve considerar para a recuperação do servidor do site primário e site de administração central do Configuration Manager, o servidor do site e o banco de dados do site. Use as seguintes seções para ajudar a determinar as opções que você deve escolher para o seu cenário de recuperação.  

> [!NOTE]  

####  <a name="BKMK_SiteServerRecoveryOptions"></a> Opções de recuperação do servidor do site  
 Você deve iniciar a Instalação de uma cópia da pasta CD.Latest criada fora da pasta de instalação do Configuration Manager. Em seguida, selecione a opção **Recuperar um site** . Quando você executa a instalação, tem as seguintes opções de recuperação para o servidor do site que falhou:  

-   **Recover the site server using an existing backup (Recuperar o servidor do site usando um backup existente)**: use essa opção quando houver um backup do servidor do site do Configuration Manager criado no servidor do site, como parte da tarefa de manutenção **Servidor do Site de Backup** anterior à falha. O site é reinstalado e as definições configuradas, com base no site de backup.  

-   **Reinstalar o servidor do site**: use essa opção quando não houver backup do servidor do site. O servidor do site é reinstalado e você deve especificar as configurações do site, assim como faria durante uma instalação inicial. Você deve usar o mesmo código e nome de banco de dados do site que usou quando o site com falha foi instalado pela primeira vez para recuperação.  

> [!NOTE]  
>  Quando a instalação detecta um site do Configuration Manager existente no servidor, é possível iniciar uma recuperação de site, mas as opções de recuperação do servidor do site são limitadas. Por exemplo, se você executar a instalação em um servidor de site existente, quando escolher a recuperação poderá recuperar o servidor de banco de dados do site, mas a opção de recuperação do servidor do site estará desativada.  

####  <a name="BKMK_SiteDatabaseRecoveryOption"></a> Opções de recuperação do banco de dados do site  
 Quando você executa a instalação, tem as seguintes opções de recuperação para o banco de dados do site:  

-   **Recover the site database using a backup set (Recuperar o banco de dados do site usando um conjunto de backup)**: use essa opção quando você tiver um backup do banco de dados do site do Configuration Manager criado como parte da tarefa de manutenção do **Servidor do Site de Backup** anterior à falha do banco de dados do site. Quando há uma hierarquia, as alterações feitas no banco de dados do site após o último backup do banco de dados do site são recuperadas do site de administração central para um site primário, ou de um site primário de referência para um site de administração central. Ao recuperar o banco de dados do site para um site primário autônomo, as alterações do site após o último backup são perdidas.  

     Ao recuperar o banco de dados do site para um site em uma hierarquia, o comportamento de recuperação é diferente para sites de administração central e sites primários, e quando o último backup está dentro ou fora do período de retenção de controle de alterações do SQL Server. Para obter mais informações, consulte a seção [Cenários de recuperação de banco de dados do site](#BKMK_SiteDBRecoveryScenarios) neste tópico.  

    > [!NOTE]  
    >  A recuperação falha ao selecionar a opção para restaurar o banco de dados do site usando um conjunto de backup, mas o banco de dados do site já existe.  

-   **Create a new database for this site (Criar um novo banco de dados para este site)**: use essa opção quando não houver backup do banco de dados do site do Configuration Manager. Quando há uma hierarquia, o novo banco de dados do site é criado e os dados são recuperados usando dados replicados do site de administração central para um site primário, ou de um site primário de referência para um site de administração central. Essa opção não está disponível quando se recupera um local primário autônomo ou um site de administração central que não tem sites primários.  

-   **Usar um banco de dados do site recuperado manualmente**: use essa opção quando você já tiver recuperado o banco de dados do site do Configuration Manager, mas precisar concluir o processo de recuperação. O Configuration Manager pode recuperar o banco de dados do site por meio da tarefa de manutenção de backup do Configuration Manager ou de um backup do banco de dados do site realizado usando o DPM ou outro processo. Depois de restaurar o banco de dados do site usando um método fora do Configuration Manager, é necessário executar a Instalação e selecionar essa opção para concluir a recuperação do banco de dados do site. Quando há uma hierarquia, as alterações feitas no banco de dados do site após o último backup do banco de dados do site são recuperadas do site de administração central para um site primário, ou de um site primário de referência para um site de administração central. Ao recuperar o banco de dados do site para um site primário autônomo, as alterações do site após o último backup são perdidas.  

    > [!NOTE]  
    >  Quando o DPM for usado para fazer backup do banco de dados do site, use os procedimentos do DPM para restaurar o banco de dados do site para um local especificado antes de continuar o processo de restauração no Configuration Manager. Para obter mais informações sobre o DPM, consulte a [Biblioteca de Documentação do Data Protection Manager](http://go.microsoft.com/fwlink/?LinkId=272772) no TechNet.  

-   **Ignorar recuperação do banco de dados**: use essa opção quando não ocorrer perda de dados no servidor de banco de dados do site do Configuration Manager. Essa opção é válida somente quando o banco de dados do site está em um computador diferente do servidor do site que está sendo recuperado.  

####  <a name="bkmk_SQLretention"></a> Período de retenção do controle de alterações do SQL Server  
 O controle de alterações é habilitado para o banco de dados do site no SQL Server. O controle de alterações permite que o Configuration Manager consulte informações sobre as alterações feitas nas tabelas do banco de dados após determinado período anterior. O período de retenção especifica por quanto tempo as informações do controle de alterações são mantidas. Por padrão, o banco de dados do site é configurado para ter um período de retenção de 5 dias. Ao recuperar um banco de dados do site, o processo de recuperação procede de maneira diferente quando o backup está dentro ou está fora do período de retenção. Por exemplo, se o servidor de banco de dados do site falhar e o último backup tiver 7 dias, ele estará fora do período de retenção.

 Para obter mais informações sobre elementos internos de controle de alterações do SQL Server, consulte os seguintes blogs da equipe do SQL Server: [Limpeza do Controle de Alterações – parte 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1) e [Limpeza do Controle de Alterações – parte 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2).



####  <a name="bkmk_reinit"></a> Processo para reinicializar o site ou dados globais  
 O processo para reinicializar o site ou dados globais substitui dados existentes no banco de dados do site por dados de outro banco de dados do site. Por exemplo, quando o site ABC reinicializa os dados do site XYZ, ocorrem as seguintes etapas:  

-   Os dados são copiados do site XYZ para o site ABC.  

-   Os dados existentes do site XYZ são removidos do banco de dados do site ABC.  

-   Os dados copiados do site XYZ são inseridos no banco de dados do site ABC.  

##### <a name="example-scenario-1"></a>Cenário de exemplo 1  
 **O site primário reinicializa os dados globais do site de administração central**: o processo de recuperação remove os dados globais existentes do site primário no banco de dados do site primário e substitui os dados pelos dados globais copiados do site de administração central.  

##### <a name="example-scenario-2"></a>Cenário de exemplo 2  
 **O site de administração central reinicializa os dados do site de um site primário**: o processo de recuperação remove os dados existentes desse site primário no banco de dados do site de administração central e substitui os dados pelos dados copiados do site primário. Os dados do site de outros sites primários não são afetados.  

####  <a name="BKMK_SiteDBRecoveryScenarios"></a> Cenários de recuperação de banco de dados do site  
 Depois que um banco de dados do site é restaurado de um backup, o Configuration Manager tenta restaurar as alterações no site e nos dados globais após o último backup do banco de dados. Veja a seguir uma descrição das ações iniciadas pelo Configuration Manager depois que um banco de dados do site é restaurado do backup.  

 **Site recuperado é um site administração central:**  

-   **Backup de banco de dados dentro do período de retenção do controle de alterações**  

    -   **Dados globais:** as alterações nos dados globais após o backup são replicadas de todos os sites primários.  

    -   **Dados do site:** as alterações nos dados do site após o backup são replicadas de todos os sites primários.  

-   **Backup de banco de dados mais antigo que o período de retenção do controle de alterações**  

    -   **Dados globais:** o site de administração central reinicializará os dados globais do site primário de referência, se for especificado. Em seguida, todos os outros sites primários reinicializam os dados globais do site de administração central. Se nenhum site de referência for especificado, todos os sites primários reinicializarão os dados globais do site de administração central (os dados que foram restaurados do backup).  

    -   **Dados do site:** o site de administração central reinicializa os dados do site por meio de cada site primário.  

 **O site recuperado é um site primário:**  

-   **Backup de banco de dados dentro do período de retenção do controle de alterações**  

    -   **Dados globais:** as alterações dos dados globais após o backup são replicadas no site de administração central.  

    -   **Dados do site:** o site de administração central reinicializa os dados do site por meio do site primário. As alterações ocorridas pós o backup são perdidas, mas a maioria dos dados é gerada novamente pelos clientes que enviam as informações ao site primário.  

-   **Backup de banco de dados mais antigo que o período de retenção do controle de alterações**  

    -   **Dados globais:** o site primário reinicializa os dados globais do site de administração central.  

    -   **Dados do site:** o site de administração central reinicializa os dados do site por meio do site primário. As alterações ocorridas pós o backup são perdidas, mas a maioria dos dados é gerada novamente pelos clientes que enviam as informações ao site primário.  

### <a name="site-recovery-procedures"></a>Procedimentos de recuperação do site  
 Use um dos procedimentos a seguir como auxílio para recuperar o servidor do site e o banco de dados do site.  

##### <a name="to-start-a-site-recovery-in-the-setup-wizard"></a>Para iniciar uma recuperação do site no Assistente de Instalação  

1.  Copie a pasta CD.Latest para um local fora da pasta de Instalação do Configuration Manager. (Consulte [A pasta CD.Latest do System Center Configuration Manager](../../core/servers/manage/the-cd.latest-folder.md))  

     Por meio da cópia da pasta CD.Latest, execute o Assistente de instalação do Configuration Manager.  

2.  Na página **Guia de Introdução** , selecione **Recuperar um site**e clique em **Avançar**.  

3.  Conclua o assistente usando as opções apropriadas para a recuperação do site.  

    > [!IMPORTANT]  
    >  Durante a recuperação, a Instalação identifica a porta do SQL Server Service Broker (SSB) usada pelo SQL Server. Não altere essa configuração de porta durante a recuperação; caso contrário, a replicação de dados não funcionará corretamente após o término da recuperação.  

    > [!NOTE]  
    >  Você pode especificar o caminho novo ou o original para usar na instalação do Configuration Manager no Assistente de Instalação.  

##### <a name="to-start-an-unattended-site-recovery"></a>Para iniciar uma recuperação autônoma do site  

1.  Prepare o script de instalação autônoma para as opções necessárias para a recuperação do site.  

2.  Execute a Instalação do Configuration Manager usando a opção **/script** do comando. Por exemplo, se você nomeasse seu arquivo de inicialização de instalação como ConfigMgrUnattend.ini e o salvasse no diretório C:\Temp do computador no qual a instalação está em execução, o comando seria o seguinte: **Setup /script C:\temp\ConfigMgrUnattend.ini**.  

> [!NOTE]  
>  Depois de recuperar um site de administração central, a replicação de alguns dados de sites filho pode não ser estabelecida. Isso pode incluir inventário de hardware, inventário de software e mensagens de status.  
>   
>  Se isso ocorrer, será necessário reinicializar o **ConfigMgrDRSSiteQueue** para a replicação de banco de dados.  Para fazer isso, use o **SQL Server Manager** para executar a seguinte consulta no banco de dados do site do Configuration Manager no site de administração central:  
>   
>  **IF EXISTS (SELECT \* FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)**  
>   
>  **ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON**  

###  <a name="BKMK_UnattendedSiteRecoveryKeys"></a> Chaves de arquivo de script de recuperação autônoma do site  
 Para executar uma recuperação autônoma de um site de administração central ou de um site primário do Configuration Manager, é possível criar um script de instalação autônoma e usar a Instalação com a opção de comando /script. O script fornece o mesmo tipo de informação que o Assistente de Instalação solicita, porém não há configurações padrão. Todos os valores devem ser especificados para as chaves de instalação que se aplicam ao tipo de recuperação usado.  

 Você pode executar a Instalação autônoma do Configuration Manager usando um arquivo de inicialização com a opção de linha de comando de instalação /script. A instalação autônoma tem suporte para a recuperação de site de administração central e de site primário do Configuration Manager. Para usar a opção de linha de comando de instalação /script, é necessário criar um arquivo de inicialização e especificar o nome do arquivo de inicialização após a opção de linha de comando de instalação /script. O nome do arquivo não é importante, contanto que tenha a extensão de nome de arquivo .ini. Para fazer referência ao arquivo de inicialização de instalação na linha de comando, é necessário fornecer o caminho completo do arquivo. Por exemplo, se o arquivo de inicialização de instalação for nomeado como setup.ini e armazenado na pasta C:\setup, sua linha de comando será:  

 **setup /script c:\setup\setup.ini**.  

> [!IMPORTANT]  
>  É necessário ter direitos de administrador para executar a Instalação. Ao executar a Instalação com o script autônomo, inicie o prompt de comando em um contexto de administrador usando **Executar como administrador**.  

 O script contém nomes de seção, nomes de chave e valores. Os nomes de chave da seção requeridos variam de acordo com o tipo de recuperação do script. A ordem das chaves dentro das seções, bem como a ordem das seções dentro do arquivo, não é importante. As chaves não diferenciam maiúsculas de minúsculas. Ao fornecer valores para chaves, o nome da chave deve ser seguido por um de sinal de igualdade (=) e o valor da chave.  

 Use as seções a seguir como auxílio para criar seu script para a recuperação autônoma do site. As tabelas listam as chaves de script de instalação disponíveis, seus valores correspondentes, se são necessárias, em que tipo de instalação são usadas e uma descrição breve da chave.  

#### <a name="recover-a-central-administration-site-unattended"></a>Recuperar um site de administração central de forma autônoma  
 Use as informações a seguir para configurar um arquivo de script de Instalação autônoma para recuperação em um site de administração central.  

 **Identificação**  

-   **Nome da chave:** Action  

    -   **Obrigatória:** Sim  

    -   **Valores:** RecoverCCAR  

    -   **Detalhes:** recupera um site de administração central  

**RecoveryOptions**  

-   **Nome da chave:** ServerRecoveryOptions  

    -   **Obrigatória:** Sim  

    -   **Valores:** 1, 2 ou 4  

         1 = Servidor do site de recuperação e SQL Server.  

         2 = Recuperar apenas o servidor do site.  

         4 = Recuperar apenas o SQL Server.  

    -   **Detalhes:** especifica se a Instalação recuperará o servidor do site, o SQL Server ou ambos. As chaves associadas são necessárias quando o seguinte valor é definido para a configuração de ServerRecoveryOptions:  

        -   **Valor = 1** Você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.  

             A chave **BackupLocation** é necessária quando o valor **10** é configurado para a chave **DatabaseRecoveryOptions** , que restaura o banco de dados do site por meio do backup.  

        -   **Valor = 2** Você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.  

        -   **Valor = 4** A chave **BackupLocation** é necessária quando o valor **10** é configurado para a chave **DatabaseRecoveryOptions** , que restaura o banco de dados do site por meio do backup.  

-   **Nome da chave:** DatabaseRecoveryOptions  

    -   **Obrigatória:** Talvez  

    -   **Valores:** 10, 20, 40, 80  

         10 = Restaurar, por meio do backup, o banco de dados do site.  

         20 = Usar um banco de dados do site recuperado manualmente usando outro método.  

         40 = Criar um novo banco de dados para o site. Use essa opção quando não houver backup do banco de dados do site disponível. Os dados globais e do site são recuperados por meio da replicação de outros sites.  

         80 = Ignorar recuperação do banco de dados.  

    -   **Detalhes:** especifica como a Instalação recuperará o banco de dados do site no SQL Server. Essa chave é necessária quando a configuração **ServerRecoveryOptions** tem o valor **1** ou **4**.  

-   **Nome da chave:** ReferenceSite  

    -   **Obrigatória:** Talvez  

    -   **Valores:** &lt;FQDNDoSiteDeReferência\>  

    -   **Detalhes:** especificará o site primário de referência que o site de administração central usa para recuperar dados globais se o backup do banco de dados for mais antigo que o período de retenção do controle de alterações ou quando o site for recuperado sem backup.  

         Quando um site de referência não é especificado e o backup é mais antigo que o período de retenção do controle de alterações, todos os sites primários são reinicializados com os dados restaurados por meio do site de administração central.  

         Quando o site de referência não é especificado e o backup está dentro do período de retenção do controle de alterações, somente as alterações ocorridas desde o backup são replicadas dos sites primários. Quando houver alterações conflitantes de sites primários diferentes, o site de administração central usará a primeira alteração que receber.  

         Essa chave é necessária quando a configuração **DatabaseRecoveryOptions** tem o valor **40**.  

-   **Nome da chave:** SiteServerBackupLocation  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;CaminhoParaConjuntoDeBackupDoServidorDeSite\>  

    -   **Detalhes:** especifica o caminho para o conjunto de backups do servidor de site. Essa chave é opcional quando a configuração **ServerRecoveryOptions** tem o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.  

-   **Nome da chave:** BackupLocation  

    -   **Obrigatória:** Talvez  

    -   **Valores:** &lt;CaminhoParaConjuntoDeBackupDoBancoDeDadosDoSite\>  

    -   **Detalhes:** especifica o caminho para o conjunto de backup do banco de dados do site. A chave **BackupLocation** é necessária quando o valor **1** ou **4** é configurado para a chave **ServerRecoveryOptions** , e o valor **10** é configurado para a chave **DatabaseRecoveryOptions** .  

**Opções**  

-   **Nome da chave:** ProductID  

    -   **Obrigatória:** Sim  

    -   **Valores:**  

         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  

         Avaliação  

    -   **Detalhes:** a chave do produto (Product Key) de instalação do Configuration Manager, incluindo os traços. Inserir **Eval** pode instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** SiteCode  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;Código do site\>  

    -   **Detalhes:** três caracteres alfanuméricos que identificam exclusivamente o site na hierarquia. É necessário especificar o código do site que foi usado pelo site antes da falha.  

-   **Nome da chave:** SiteName  

    -   **Obrigatória:** Sim  

    -   **Valores:** SiteName  

    -   **Detalhes:** descrição desse site.  

-   **Nome da chave:** SMSInstallDir  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*ConfigMgrInstallationPath*>  

    -   **Detalhes:** especifica a pasta de instalação dos arquivos de programa do Configuration Manager.  

        > [!NOTE]  
        >  Você pode especificar o caminho novo ou o original para usar na instalação do Configuration Manager.  

-   **Nome da chave:** SDKServer  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*FQDN do Provedor de SMS*>  

    -   **Detalhes:** especifica o FQDN para o servidor que hospedará o Provedor de SMS. Você deve especificar o servidor que hospedou o Provedor de SMS antes da falha.  

         Você pode configurar outros Provedores de SMS para o site após a instalação inicial.  

-   **Nome da chave:** PrerequisiteComp  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = baixar  

         1 = já baixado  

    -   **Detalhes:** especifica se os arquivos de pré-requisito da Instalação já foram baixados. Por exemplo, se você usar o valor 0, a Instalação baixará os arquivos.  

-   **Nome da chave:** PrerequisitePath  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Detalhes:** especifica o caminho para os arquivos de pré-requisito da Instalação. Dependendo do valor do **PrerequisiteComp** , a Instalação usará esse caminho para armazenar arquivos baixados ou para localizar arquivos baixados anteriormente.  

-   **Nome da chave:** AdminConsole  

    -   **Obrigatória:** Talvez  

    -   **Valores:** 0 ou 1  

         0 = não instalar  

         1 = instalar  

    -   **Detalhes:** especifica se deseja instalar o console do Configuration Manager. Essa chave é necessária quando a configuração de **ServerRecoveryOptions** tem o valor **4**.  

-   **Nome da chave:** JoinCEIP  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = não ingressar  

         1 = ingressar  

    -   **Detalhes:** especifica se deve ingressar no Programa de Aperfeiçoamento da Experiência do Usuário.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Obrigatória:** Sim  

    -   **Valores:** *&lt;NomeDoServidorSQL\>*  

    -   **Detalhes:** o nome do servidor ou o nome da instância clusterizada executando o SQL Server que hospedará o banco de dados do site. Você deverá especificar o mesmo servidor que hospedou o banco de dados do site antes da falha.  

-   **Nome da chave:** DatabaseName  

    -   **Obrigatória:** Sim  

    -   **Valores:**  

         *&lt;NomeDoBancoDeDadosDoSite\>*  

         ou  

         *&lt;NomeDaInstância\>*\\*&lt;NomeDoBancoDeDadosDoSite\>*  

    -   **Detalhes:** especifica o nome do banco de dados do SQL Server a ser criado ou usado para instalar o banco de dados do site de administração central. Você deverá especificar o mesmo nome do banco de dados usado antes da falha.  

        > [!IMPORTANT]  
        >  Você deverá especificar o nome da instância e o nome do banco de dados do site se você não usar a instância padrão.  

-   **Nome da chave:** SQLSSBPort  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*SSBPortNumber*>  

    -   **Detalhes:** especifica a porta do SQL Server Service Broker (SSB) usada pelo SQL Server. Normalmente, o SSB está configurado para usar a porta TCP 4022, mas há suporte para outras portas. Você deve especificar a mesma porta do SSB que foi usada antes da falha.  

#### <a name="recover-a-primary-site-unattended"></a>Recuperar um site primário autônomo  
 Use as informações a seguir para configurar um arquivo de script de Instalação autônoma para recuperação em um site de administração central.  

 **Identificação**  

-   **Nome da chave:** Action  

    -   **Obrigatória:** Sim  

    -   **Valores:** RecoverPrimarySite  

    -   **Detalhes:** recupera um site primário  

**RecoveryOptions**  

-   **Nome da chave:** ServerRecoveryOptions  

    -   **Obrigatória:** Sim  

    -   **Valores:** 1, 2 ou 4  

         1 = Servidor do site de recuperação e SQL Server.  

         2 = Recuperar apenas o servidor do site.  

         4 = Recuperar apenas o SQL Server.  

    -   **Detalhes:** especifica se a Instalação recuperará o servidor do site, o SQL Server ou ambos. As chaves associadas são necessárias quando o seguinte valor é definido para a configuração de ServerRecoveryOptions:  

        -   **Valor = 1** Você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.  

             A chave **BackupLocation** é necessária quando o valor **10** é configurado para a chave **DatabaseRecoveryOptions** , que restaura o banco de dados do site por meio do backup.  

        -   **Valor = 2** Você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.  

        -   **Valor = 4** A chave **BackupLocation** é necessária quando o valor **10** é configurado para a chave **DatabaseRecoveryOptions** , que restaura o banco de dados do site por meio do backup.  

-   **Nome da chave:** DatabaseRecoveryOptions  

    -   **Obrigatória:** Talvez  

    -   **Valores:** 10, 20, 40, 80  

         10 = Restaurar, por meio do backup, o banco de dados do site.  

         20 = Usar um banco de dados do site recuperado manualmente usando outro método.  

         40 = Criar um novo banco de dados para o site. Use essa opção quando não houver backup do banco de dados do site disponível. Os dados globais e do site são recuperados por meio da replicação de outros sites.  

         80 = Ignorar recuperação do banco de dados.  

    -   **Detalhes:** especifica como a Instalação recuperará o banco de dados do site no SQL Server. Essa chave é necessária quando a configuração **ServerRecoveryOptions** tem o valor **1** ou **4**.  

-   **Nome da chave:** SiteServerBackupLocation  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;CaminhoParaConjuntoDeBackupDoServidorDeSite\>  

    -   **Detalhes:** especifica o caminho para o conjunto de backups do servidor de site. Essa chave é opcional quando a configuração **ServerRecoveryOptions** tem o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.  

-   **Nome da chave:** BackupLocation  

    -   **Obrigatória:** Talvez  

    -   **Valores:** &lt;CaminhoParaConjuntoDeBackupDoBancoDeDadosDoSite\>  

    -   **Detalhes:** especifica o caminho para o conjunto de backup do banco de dados do site. A chave **BackupLocation** é necessária quando o valor **1** ou **4** é configurado para a chave **ServerRecoveryOptions** , e o valor **10** é configurado para a chave **DatabaseRecoveryOptions** .  

**Opções**  

-   **Nome da chave:** ProductID  

    -   **Obrigatória:** Sim  

    -   **Valores:**  

         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  

         Avaliação  

    -   **Detalhes:** a chave do produto (Product Key) de instalação do Configuration Manager, incluindo os traços. Inserir **Eval** pode instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** SiteCode  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;Código do site\>  

    -   **Detalhes:** três caracteres alfanuméricos que identificam exclusivamente o site na hierarquia. É necessário especificar o código do site que foi usado pelo site antes da falha.  

-   **Nome da chave:** SiteName  

    -   **Obrigatória:** Sim  

    -   **Valores:** SiteName  

    -   **Detalhes:** descrição desse site.  

-   **Nome da chave:** SMSInstallDir  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*ConfigMgrInstallationPath*>  

    -   **Detalhes:** especifica a pasta de instalação dos arquivos de programa do Configuration Manager.  

        > [!NOTE]  
        >  Você pode especificar o caminho novo ou o original para usar na instalação do Configuration Manager.  

-   **Nome da chave:** SDKServer  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*FQDN do Provedor de SMS*>  

    -   **Detalhes:** especifica o FQDN para o servidor que hospedará o Provedor de SMS. Você deve especificar o servidor que hospedou o Provedor de SMS antes da falha.  

         Você pode configurar outros Provedores de SMS para o site após a instalação inicial.  

-   **Nome da chave:** PrerequisiteComp  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = baixar  

         1 = já baixado  

    -   **Detalhes:** especifica se os arquivos de pré-requisito da Instalação já foram baixados. Por exemplo, se você usar o valor 0, a Instalação baixará os arquivos.  

-   **Nome da chave:** PrerequisitePath  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Detalhes:** especifica o caminho para os arquivos de pré-requisito da Instalação. Dependendo do valor do **PrerequisiteComp** , a Instalação usará esse caminho para armazenar arquivos baixados ou para localizar arquivos baixados anteriormente.  

-   **Nome da chave:** AdminConsole  

    -   **Obrigatória:** Talvez  

    -   **Valores:** 0 ou 1  

         0 = não instalar  

         1 = instalar  

    -   **Detalhes:** especifica se deseja instalar o console do Configuration Manager. Essa chave é necessária quando a configuração de **ServerRecoveryOptions** tem o valor **4**.  

-   **Nome da chave:** JoinCEIP  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = não ingressar  

         1 = ingressar  

    -   **Detalhes:** especifica se deve ingressar no Programa de Aperfeiçoamento da Experiência do Usuário.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Obrigatória:** Sim  

    -   **Valores:** *&lt;NomeDoServidorSQL\>*  

    -   **Detalhes:** o nome do servidor ou o nome da instância clusterizada executando o SQL Server que hospedará o banco de dados do site. Você deverá especificar o mesmo servidor que hospedou o banco de dados do site antes da falha.  

-   **Nome da chave:** DatabaseName  

    -   **Obrigatória:** Sim  

    -   **Valores:**  

         *&lt;NomeDoBancoDeDadosDoSite\>*  

         ou  

         *&lt;NomeDaInstância\>*\\*&lt;NomeDoBancoDeDadosDoSite\>*  

    -   **Detalhes:** especifica o nome do banco de dados do SQL Server a ser criado ou usado para instalar o banco de dados do site de administração central. Você deverá especificar o mesmo nome do banco de dados usado antes da falha.  

        > [!IMPORTANT]  
        >  Você deverá especificar o nome da instância e o nome do banco de dados do site se você não usar a instância padrão.  

-   **Nome da chave:** SQLSSBPort  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*SSBPortNumber*>  

    -   **Detalhes:** especifica a porta do SQL Server Service Broker (SSB) usada pelo SQL Server. Normalmente, o SSB está configurado para usar a porta TCP 4022, mas há suporte para outras portas. Você deve especificar a mesma porta do SSB que foi usada antes da falha.  

**ExpansionOption de hierarquia**  

-   **Nome da chave:** CCARSiteServer  

    -   **Obrigatória:** Talvez  

    -   **Valores:** &lt;*SiteCodeForCentralAdministrationSite*>  

    -   **Detalhes:** especifica o site de administração central ao qual o site primário será anexado quando ingressar na hierarquia do Configuration Manager. Essa configuração é necessária se o site primário foi anexado ao site de administração central antes da falha. É necessário especificar o código do site usado para o site de administração central antes da falha.  

-   **Nome da chave:** CASRetryInterval  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*Interval*>  

    -   **Detalhes:** especifica o intervalo de repetição (em minutos) para tentar uma conexão ao site de administração central depois de a conexão falhar. Por exemplo, se a conexão com o site de administração central falhar, o site primário aguardará o número de minutos especificado para CASRetryInterval e tentará novamente se conectar.  

-   **Nome da chave:** WaitForCASTimeout  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*Timeout*>  

    -   **Detalhes:** especifica o valor máximo do tempo limite (em minutos) para o site primário se conectar ao site de administração central. Por exemplo, se o site primário falhar ao conectar-se ao site de administração central, o site primário tentará novamente a conexão ao site de administração central baseado no CASRetryInterval até chegar ao período do WaitForCASTimeout. Você pode especificar um valor de 0 a 100.  

###  <a name="BKMK_PostRecovery"></a> Tarefas de pós-recuperação  
 Feita a recuperação de seu site, há várias tarefas de pós-recuperação a considerar antes da conclusão da recuperação do site. Use as seções a seguir para ajudá-lo a concluir o processo de recuperação do site.  

#### <a name="re-enter-user-account-passwords"></a>Digite novamente as senhas de conta de usuário  
 Recuperado o servidor do site, as senhas das contas de usuário especificadas para o site devem ser digitadas novamente porque elas são redefinidas durante a recuperação de site. As contas são listadas na página **Concluído** no Assistente de Instalação após a recuperação do site estiver concluída e salva em C:\ConfigMgrPostRecoveryActions.html no servidor do site recuperado.  

###### <a name="to-re-enter-user-account-passwords-after-site-recovery"></a>Para digitar novamente as senhas de conta de usuário após a recuperação de site  

1.  Abra o console do Configuration Manager e conecte-se ao site recuperado.  

2.  No console do Configuration Manager, clique em **Administração**.  

3.  No espaço de trabalho **Administração** , expanda **Segurança**e clique em **Contas**.  

4.  Para cada conta em que você tenha que digitar novamente a senha, faça o seguinte:  

    1.  Selecione a conta da lista de contas que foram identificadas após a recuperação do site. Você pode encontrar essa lista no C:\ConfigMgrPostRecoveryActions.html no servidor do site recuperado.  

    2.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades** para abrir as propriedades da conta.  

    3.  Na guia **Geral** , clique em **Definir**e digite novamente as senhas da conta.  

    4.  Clique em **Verificar**, selecione a fonte de dados apropriada para a conta de usuário selecionada e clique em **Testar conexão** para verificar se a conta de usuário pode conectar-se à fonte de dados.  

    5.  Clique em **OK** para salvar as alterações de senha e clique em **OK**.  

#### <a name="re-enter-sideloading-keys"></a>Digite novamente as chaves de sideload  
 Recuperado o servidor do site, é necessário digitar novamente as chaves de sideload do Windows especificadas para o site porque elas são redefinidas durante a recuperação do site. Ao digitar novamente as chaves de sideload, a contagem na coluna **Ativações usadas** para as chaves de sideload do Windows é redefinida no console do Configuration Manager. Por exemplo, digamos que antes da falha do site a contagem de **Total de ativações** estava definida como **100** e de **Ativações usadas** como **90** para o número de chaves usadas pelos dispositivos. Recuperado o site, a coluna **Total de ativações** continua a exibir **100**, mas a coluna **Ativações usadas** exibe incorretamente **0**. No entanto, quando 10 novos dispositivos usarem uma chave de sideload, não haverá mais chaves de sideload disponíveis e o dispositivo seguinte irá falhar ao usar uma chave de sideload.  

#### <a name="recreate-the-microsoft-intune-subscription"></a>Recriar a Assinatura do Microsoft Intune  
 Se você recuperar um servidor do site do Configuration Manager depois que o computador do servidor do site for restaurado ao estado anterior, a assinatura do Microsoft Intune não será restaurada. É necessário reconectar a assinatura depois de recuperar o site.  Não crie uma nova solicitação de APN. Em vez disso, carregue o arquivo .pem atual válido carregado na última vez em que o gerenciamento do iOS foi configurado ou renovado. Para obter mais informações, consulte [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription).  

#### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Configurar o SSL para funções do sistema de site que usam IIS  
 Ao recuperar sistemas de site que executam o IIS e que foram configurados para HTTPS antes da falha, você precisa reconfigurar o IIS para usar o certificado do servidor Web.  

#### <a name="reinstall-hotfixes-in-the-recovered-site-server"></a>Reinstalar os hotfixes no servidor do Site recuperado  
 Feita a recuperação de site, você deverá reinstalar os hotfixes que foram aplicados ao servidor do site. Os hotfixes instalados anteriormente são listados na página **Concluído** no Assistente de Instalação após a recuperação de site e salvos em C: **\ConfigMgrPostRecoveryActions.html** no servidor do site recuperado.  

#### <a name="recover-custom-reports-on-the-computer-running-reporting-services"></a>Recuperar relatórios personalizados no computador que está executando o Reporting Services  
 Quando você cria relatórios do Reporting Services personalizados e o Reporting Services falha, você pode recuperar os relatórios feito o backup do servidor de relatório. Para obter mais informações sobre como restaurar relatórios personalizados no Reporting Services, consulte [Operações de backup e restauração para a Instalação do Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=228724) nos Manuais Online do SQL Server 2008.  

#### <a name="recover-content-files"></a>Recuperar arquivos de conteúdo  
 O banco de dados do site contém informações sobre onde os arquivos de conteúdo são armazenados no servidor do site, mas os arquivos de conteúdo não passam por backup ou restauração como parte do processo de backup ou recuperação. Para recuperar completamente os arquivos de conteúdo, você deve restaurar a biblioteca de conteúdo e os arquivos de origem do pacote no local original. Há vários métodos de recuperar seus arquivos de conteúdo, mas o mais fácil é restaurá-los por meio do backup do sistema de arquivo do servidor do site.  

 Se você não tem o backup do sistema de arquivo para os arquivos de origem do pacote, você deve copiar ou baixá-los manualmente da mesma forma quando o pacote foi criado pela primeira vez. É possível executar a seguinte consulta no SQL Server para encontrar o local de origem do pacote de todos os pacotes e aplicativos: `SELECT * FROM v_Package`. É possível identificar o site de origem do pacote observando os três primeiros caracteres da ID do pacote. Por exemplo, se a ID do pacote for CEN00001, o código do site de origem será CEN. Ao restaurar os arquivos de origem do pacote, eles devem ser restaurados no mesmo local em que estavam antes da falha.  

 Se você não tem o backup do sistema de arquivo que contém a biblioteca de conteúdo, você possui as seguintes opções de restauração:  

-   **Import a prestaged content file (Importar um arquivo de conteúdo pré-teste)**: quando você tem uma hierarquia do Configuration Manager, você pode criar um arquivo de conteúdo pré-teste com todos os pacotes e aplicativos de outro local e importar o arquivo de conteúdo pré-teste para recuperar a biblioteca de conteúdo no servidor do site.  

-   **Atualizar conteúdo**: ao iniciar a ação de atualizar o conteúdo para um tipo de implantação de um pacote ou aplicativo, o conteúdo é copiado da origem do pacote para a biblioteca de conteúdo. Os arquivos de origem do pacote devem estar disponíveis no local original para essa ação ser concluída com êxito. Você deve executar essa ação em cada pacote e aplicativo.  

#### <a name="recover-custom-software-updates-on-the-computer-running-updates-publisher"></a>Recuperar atualizações de software personalizadas no computador que executa o Updates Publisher  
 Quando você tem arquivos do banco de dados do Update Publisher incluídos em seu plano de backup, você pode recuperar os bancos de dados em caso de falha no computador em que o Update Publisher é executado. Para obter mais informações sobre o Updates Publisher, consulte [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) na biblioteca do System Center TechCenter.  

 Use o procedimento a seguir para restaurar o banco de dados do Updates Publisher.  

###### <a name="to-restore-the-updates-publisher-2011-database"></a>Para restaurar o banco de dados do Updates Publisher 2011  

1.  Reinstale o Updates Publisher no computador recuperado.  

2.  Copie o arquivo de banco de dados (Scupdb.sdf) de seu destino de backup para %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\ no computador que executa o Updates Publisher.  

3.  Quando mais de um usuário executa o Updates Publisher no computador, você deve copiar cada arquivo de banco de dados para o local apropriado do perfil do usuário.  

#### <a name="user-state-migration-data"></a>Dados de migração de estado do usuário  
 Como parte das propriedades do sistema de site do ponto de migração de estado, você especifica as pastas que armazenam os dados de migração de estado do usuário. Depois de recuperar um servidor com uma pasta que armazena dados de migração de estado do usuário, você deve restaurar manualmente os dados de migração de estado do usuário no servidor para as mesmas pastas que armazenaram os dados antes da falha.  

#### <a name="regenerate-the-certificates-for-distribution-points"></a>Gerar novamente os certificados para pontos de distribuição  
 Depois de restaurar um site, o distmgr.log pode conter a seguinte entrada para um ou mais pontos de distribuição: **Falha ao descriptografar dados PFX do certificado**. Essa entrada indica que os dados do certificado do ponto de distribuição não podem ser descriptografados pelo site. Para resolver isso, você deve gerar novamente ou importar novamente o certificado para os pontos de distribuição afetados. Isso pode ser feito usando o cmdlet [Set-CMDistributionPoint](https://technet.microsoft.com/library/jj821872\(v=sc.20\).aspx) do PowerShell.  

#### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Atualizar certificados usados para pontos de distribuição baseados em nuvem  
 O Configuration Manager requer um certificado de gerenciamento que ele utiliza para comunicação do servidor do site com o ponto de distribuição baseado em nuvem. Após recuperações de site, você deve atualizar os certificados para os pontos de distribuição baseados em nuvem.  

####  <a name="BKMK_RecoverSecondarySite"></a> Recuperar um site secundário  
 O Configuration Manager não dá suporte ao backup do banco de dados em um site secundário, mas dá suporte à recuperação reinstalando o site secundário. A recuperação de sites secundários é necessária quando um site secundário do Configuration Manager falha. Você pode recuperar sites secundários usando a ação **Recuperar Site Secundário** do nó **Sites** no console do Configuration Manager. Diferentemente da recuperação de um site de administração central ou site primário, a recuperação de sites secundários não usa um arquivo de backup, e em vez disso reinstala os arquivos do site secundário no computador do site secundário com falha. Em seguida, os dados do site secundário são reinicializados com os dados do site pai primário. Durante o processo de recuperação, o Configuration Manager verifica se há uma biblioteca de conteúdo no computador do site secundário e se o conteúdo apropriado está disponível. O site secundário usará a biblioteca de conteúdo existente, se ela contiver o conteúdo apropriado. Caso contrário, para recuperar a biblioteca de conteúdo de um site secundário recuperado, será necessário redistribuir ou pré-configurar o conteúdo para o site recuperado. Quando você possui um ponto de distribuição que não está no site secundário, não é necessário reinstalar o ponto de distribuição durante recuperações do site secundário. Após a recuperação de site secundário, o site sincroniza-se automaticamente com o ponto de distribuição.  

 Você pode verificar o status da recuperação de sites secundários usando a ação **Mostrar Status da Instalação** do nó **Sites** no console do Configuration Manager.  

> [!IMPORTANT]  
>  Você deve usar um computador com a mesma configuração que o computador que falhou, como seu FQDN, para recuperar com êxito o site secundário. O computador também deve atender a todos os pré-requisitos do site secundário e ter os direitos de segurança apropriados configurados. Além disso, use o mesmo caminho de instalação usado para o site que falhou.  

> [!IMPORTANT]  
>  Durante a recuperação de sites secundários, o Configuration Manager não instalará o SQL Server Express se ele não estiver instalado no computador. Portanto, para poder recuperar um site secundário, você deve instalar manualmente o SQL Server Express ou o SQL Server. Você deve usar a mesma versão do SQL Server e a mesma instância do SQL Server usadas para o banco de dados do site secundário antes da falha.  

##  <a name="BKMK_SMSWriterService"></a> Serviço SMS Writer  
 O SMS Writer é um serviço que interage com o VSS (Serviço de Cópias de Sombra de Volume) durante o processo de backup. O serviço SMS Writer deve estar em execução para o backup do site do Configuration Manager para ser concluído com êxito.  

### <a name="purpose"></a>Finalidade  
 O SMS Writer registra-se no serviço VSS e se associa às suas interfaces e eventos. Quando o VSS transmite eventos ou envia notificações específicas para o SMS Writer, o SMS Writer responde à notificação e executa a ação apropriada. O SMS Writer lê o arquivo de controle de backup (smsbkup.ctl), localizado em &lt;*Caminho de Instalação do ConfigMgr*>\inboxes\smsbkup.box, e determina os arquivos e os dados que devem ser armazenados em backup. O SMS Writer cria metadados, que consistem em vários componentes, com base nessas informações e em dados específicos da chave e das subchaves de registro de SMS. O serviço envia os metadados ao VSS quando solicitado. Em seguida, o VSS envia os metadados ao aplicativo solicitante, o Gerenciador de Backup do Configuration Manager. O Gerenciador de Backup seleciona os dados que passam por backup e envia esses dados ao SMS Writer via VSS. O SMS Writer executa as etapas apropriadas para se preparar para o backup. Quando o VSS está pronto para capturar o instantâneo, ele envia um evento, o SMS Writer interrompe todos os serviços do Configuration Manager e assegura que as atividades do Configuration Manager sejam congeladas enquanto o instantâneo é criado. Depois que o instantâneo é concluído, o SMS Writer reinicia os serviços e as atividades.  

 O serviço SMS Writer é instalado automaticamente. Ele deve estar em execução quando o aplicativo VSS solicitar um backup ou uma restauração.  

### <a name="writer-id"></a>ID do gravador  
 A ID do gravador do SMS Writer é: 03ba67dd-dc6d-4729-a038-251f7018463b.  

### <a name="permissions"></a>Permissões  
 O serviço SMS Writer deve ser executado pela conta Sistema Local.  

### <a name="volume-shadow-copy-service"></a>Serviço de Cópias de Sombra de Volume  
 O VSS é um conjunto de APIs COM que implementa uma estrutura para permitir a execução de backups de volume enquanto os aplicativos de um sistema continuam a ser gravados nos volumes. O VSS fornece uma interface consistente que permite a coordenação entre os aplicativos do usuário que atualizam dados em disco (o serviço SMS Writer) e aqueles que fazem backup dos aplicativos (o serviço Gerenciador de Backup). Para obter mais informações sobre o VSS, consulte o tópico [Serviço de Cópias de Sombra de Volume](http://go.microsoft.com/fwlink/p/?LinkId=241968) no Windows Server TechCenter.  

