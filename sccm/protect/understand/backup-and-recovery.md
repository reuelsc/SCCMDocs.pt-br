---
title: Sites de backup
titleSuffix: Configuration Manager
description: Saiba como fazer o backup seus sites antes de falha ou perda de dados no System Center Configuration Manager.
ms.custom: na
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
caps.latest.revision: "22"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 7dae5ada647146713b884b09d0eda1c7ec6531ef
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="back-up-a-configuration-manager-site"></a>Fazer backup de um site do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Prepare abordagens de backup e recuperação para evitar perda de dados. Para sites do Configuration Manager uma abordagem de backup e recuperação pode ajudá-lo a recuperar sites e hierarquias mais rapidamente e com o mínimo de perda de dados.  

As seções neste tópico podem ajudá-lo a fazer backup de seus sites. Para recuperar um site, veja [Recuperação para o Configuration Manager](/sccm/protect/understand/recover-sites).  

## <a name="considerations-before-creating-a-backup"></a>Considerações antes de criar um backup  
-   **Se você usar um grupo de disponibilidade do AlwaysOn do SQL Server para hospedar o banco de dados do site:** modifique seu backup e os planos de recuperação conforme descrito em [Preparar para usar o AlwaysOn do SQL Server](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-backup).

-   O Configuration Manager pode recuperar o banco de dados do site por meio da tarefa de manutenção de backup do Configuration Manager ou de um backup do banco de dados do site criado com outro processo.   

    Por exemplo, é possível restaurar o banco de dados do site por um backup criado como parte de um plano de manutenção do Microsoft SQL Server. Você também pode usar um backup que é criado usando o Data Protection Manager para fazer backup de seu banco de dados do site (DPM).

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>Usando o Data Protection Manager para fazer backup do banco de dados do site
Você pode usar o System Center 2012 Data Protection Manager (DPM) para fazer backup do banco de dados do site.

É necessário criar um novo grupo de proteção no DPM para o computador do banco de dados do site. Na página **Selecionar Membros do Grupo** do Assistente para Criar Novo Grupo de Proteção, selecione o serviço SMS Writer na lista de fontes de dados e selecione o banco de dados do site como membro apropriado. Para obter mais informações sobre como usar o DPM para fazer backup do banco de dados do site, consulte a [Biblioteca de Documentação do Data Protection Manager](http://go.microsoft.com/fwlink/?LinkId=272772) no TechNet.  

> [!IMPORTANT]  
>  O Configuration Manager não dá suporte ao backup do DPM para um cluster do SQL Server que usa uma instância nomeada, mas dá suporte ao backup do DPM em um cluster do SQL Server que usa a instância padrão do SQL Server.  

 Depois de restaurar o banco de dados do site, siga as etapas da Instalação para recuperar o site. Selecione a opção de recuperação **Usar um banco de dados do site recuperado manualmente** para usar o banco de dados do site recuperado com o uso do Data Protection Manager.  

## <a name="backup-maintenance-task"></a>Tarefa de manutenção de backup
É possível automatizar o backup de sites do Configuration Manager agendando a tarefa de manutenção Servidor do Site de Backup predefinida. Essa tarefa:

-   É executada conforme um agendamento
-   Faz backup do banco de dados do site
-   Faz backup de chaves específicas do Registro
-   Faz backup de arquivos e pastas específicas
-   Faz backup da [pasta CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder)   

Planeje executar a tarefa padrão de backup do site, no mínimo, a cada 5 dias. Isso ocorre porque o Configuration Manager usa um *Período de retenção do controle de alterações do SQL Server* de 5 dias.  (Veja [Período de retenção do controle de alterações do SQL Server](/sccm/protect/understand/recover-sites#bkmk_SQLretention) no tópico Recuperar sites).

Para simplificar o processo de backup, é possível criar o arquivo **AfterBackup.bat** para executar ações pós-backup automaticamente depois de executar a tarefa de manutenção de backup com êxito. O arquivo AfterBackup.bat é normalmente é usado para arquivar o instantâneo de backup em um local seguro. Também é possível usar o arquivo AfterBackup.bat para copiar arquivos para a pasta de backup e iniciar outras tarefas de backup complementares.  

É possível fazer backup de um site de administração central e de um site primário, mas não há suporte de backup para sites secundários ou servidores de sistema de site.

Quando o serviço de backup do Configuration Manager é executado, ele segue as instruções definidas no arquivo de controle de backup (**&lt;PastaDeInstalaçãoDoConfigMgr\>\Inboxes\Smsbkup.box\Smsbkup.ctl**). É possível modificar o arquivo de controle de backup para alterar o comportamento do serviço de backup.  

As informações de status de backup do site são gravadas no arquivo **Smsbkup.log** . O arquivo é criado na pasta de destino especificada nas propriedades da tarefa de manutenção Servidor do Site de Backup.  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>Para habilitar a tarefa de manutenção de backup do site  

1.  No console do Configuration Manager, abra **Administração** > **Configuração do Site** > **Sites**.  

2.  Selecione o site no qual deseja habilitar a tarefa de manutenção de backup do site.  

3.  Na guia **Início**, no grupo **Configurações**, escolha **Tarefas de Manutenção do Site**.  

4.  Escolha **Servidor do Site de Backup**  >  **Editar**.  

5.  Escolha **Habilitar esta tarefa** > **Definir Caminhos** para especificar o destino do backup. Você tem as seguintes opções:  

    > [!IMPORTANT]  
    >  Para ajudar a evitar a violação dos arquivos de backup, armazene os arquivos em um local seguro. O caminho de backup mais seguro é uma unidade local, para que possibilite definir permissões do sistema de arquivos NTFS na pasta. O Configuration Manager não criptografa os dados de backup armazenados no caminho do backup.  

    -   **Unidade local no servidor do site para dados e banco de dados do site**: especifica que os arquivos de backup do site e do banco de dados do site são armazenados no caminho especificado na unidade de disco local do servidor do site. É necessário criar a pasta local para poder executar a tarefa de backup. A conta Sistema Local no servidor do site deve ter permissões de **Gravação** no sistema de arquivos NTFS para a pasta local do backup do servidor do site. A conta Sistema Local no computador que está executando o SQL Server deve ter permissões de **Gravação** NTFS para a pasta do backup do banco de dados do site.  

    -   **Caminho de rede (nome UNC) para dados e banco de dados do site**: especifica que os arquivos de backup do site e do banco de dados do site são armazenados no caminho UNC especificado. É necessário criar o compartilhamento para poder executar a tarefa de backup. A conta de computador do servidor do site e a conta de computador do SQL Server, se o SQL Server estiver instalado em outro computador, devem ter permissões de **Gravação** NTFS e compartilhar permissões para a pasta de rede compartilhada.  

    -   **Unidades locais no servidor do site e no SQL Server**: especifica que os arquivos de backup do site são armazenados no caminho especificado na unidade local do servidor do site e que os arquivos de backup do banco de dados do site são armazenados no caminho especificado na unidade local do servidor de banco de dados do site. É necessário criar as pastas locais para poder executar a tarefa de backup. A conta de computador do servidor do site deve ter permissões de **Gravação** NTFS para a pasta criada no servidor do site. A conta de computador do SQL Server deve ter permissões de **Gravação** NTFS para a pasta criada no servidor de banco de dados do site. Essa opção está disponível somente quando o banco de dados do site não está instalado no servidor do site.  

    > [!NOTE]  
    >   A opção de navegar até o destino do backup está disponível somente quando o caminho UNC do destino do backup é especificado.

    > O nome da pasta ou do compartilhamento usado como destino do backup não oferece suporte ao uso de caracteres Unicode.  

6.  Configure um agendamento para a tarefa de backup do site. Como prática recomendada, considere agendar a execução do backup para fora do horário de trabalho ativo. Se houver uma hierarquia, considere agendar a execução para no mínimo duas vezes por semana para garantir a máximo retenção de dados em caso de falha do site.  

    Ao executar o console do Configuration Manager no mesmo servidor do site em que o backup está sendo configurado, a tarefa de manutenção Servidor do Site de Backup usa a hora local para o agendamento. Quando o console do Configuration Manager é executado em um computador remoto do site que está sendo configurado para backup, a tarefa de manutenção Servidor do Site de Backup usa o horário UTC para o agendamento.  

7.  Escolha se um alerta deve ser criado caso a tarefa de backup do site falhe, clique em **OK** e em **OK** novamente. Quando selecionado, o Configuration Manager cria um alerta crítico para a falha do backup, que pode ser visto no nó **Alertas** do espaço de trabalho **Monitoramento**.  

 Em seguida, verifique se a tarefa de manutenção Servidor do Site de Backup está em execução para garantir que os backups estão sendo criadas.  

#### <a name="to-verify-that-the-backup-site-server-maintenance-task-is-running"></a>Para verificar se a tarefa de manutenção Servidor do Site de Backup está em execução  
Verifique se a tarefa de manutenção Site de Backup está em execução conferindo o seguinte:  

-   Confira o carimbo de data/hora dos arquivos na pasta de destino do backup que a tarefa criou. Verifique se o carimbo de data/hora foi atualizado com uma hora que coincida com a hora em que a tarefa foi agendada para ser executada pela última vez.  

-   No nó **Status do Componente** do espaço de trabalho **Monitoramento** , confira as mensagens de status de SMS_SITE_BACKUP. Quando o backup do site for concluído com êxito, você verá a mensagem ID 5035, que indica que o backup do site foi concluído sem erros.  

-   Quando a tarefa de manutenção Servidor do Site de Backup estiver configurada para criar um alerta em caso de falha do backup, é possível verificar as falhas de backup no nó **Alertas** do espaço de trabalho **Monitoramento** .  

-   Em &lt;*PastaDeInstalaçãoDoConfigMgr*>\Logs, verifique se há avisos e erros em Smsbkup.log. Quando o backup do site for concluído com êxito, você verá `Backup completed` com um carimbo de data e hora e a ID de mensagem `STATMSG: ID=5035`.  

    > [!TIP]  
    >  Quando a tarefa de manutenção de backup falha, é possível reiniciá-la interrompendo e reiniciando o serviço SMS_SITE_BACKUP.  

## <a name="archive-the-backup-snapshot"></a>Arquivar o instantâneo de backup  
A primeira vez que a tarefa de manutenção Servidor do Site de Backup é executada, um instantâneo de backup é criado, e você pode usá-lo para recuperar o servidor do site em caso de falha. Quando a tarefa de backup é executada novamente durante ciclos subsequentes, é criado um novo instantâneo de backup que substitui o instantâneo anterior. Consequentemente, o site fica com apenas um instantâneo de backup e não há como recuperar um instantâneo de backup anterior.  

Como prática recomendada, mantenha diversos arquivos de instantâneo de backup, pelos seguintes motivos:  

-   É comum que a mídia de backup falhe, seja extraviada ou contenha apenas um backup parcial. Recuperar um site primário autônomo com falha de um backup mais antigo é melhor do que recuperar sem qualquer backup. Para um servidor de site em uma hierarquia, o backup deve estar no período de retenção do controle de alterações do SQL Server, ou o backup não será necessário.  

-   Uma corrupção no site pode não ser detectada durante vários ciclos de backup. Pode ser necessário usar um instantâneo de backup anterior à corrupção do site. Isso se aplica a um site primário autônomo e a sites em uma hierarquia em que o backup está no período de retenção do controle de alterações do SQL Server.  

-   O site poderá não ter nenhum instantâneo de backup, se, por exemplo, a tarefa de manutenção de servidor do site de backup falhar. Como a tarefa de backup remove o instantâneo de backup anterior antes de começar a fazer o backup dos dados atuais, não haverá um instantâneo de backup válido.  

## <a name="using-the-afterbackupbat-file"></a>Usando o arquivo AfterBackup.bat  
Após o backup bem-sucedido do site, a tarefa do Servidor do Site de Backup tentará executar automaticamente um arquivo chamado AfterBackup.bat. Você deve criar manualmente o arquivo AfterBackup.bat em &lt;*PastaDeInstalaçãoDoConfigMgr*>\Inboxes\Smsbkup. Se existir um arquivo AfterBackup.bat e ele estiver armazenado na pasta correta, ele será executado automaticamente depois que a tarefa de backup for concluída.

O arquivo AfterBackup.bat permite arquivar o instantâneo de backup no final de cada operação de backup, e executa automaticamente outras tarefas pós-backup que não fazem parte da tarefa de manutenção do servidor do site de backup. O arquivo AfterBackup.bat integra o arquivo e as operações de backup, garantindo assim que cada novo instantâneo de backup seja arquivado.

Quando o arquivo AfterBackup.bat não está presente, a tarefa de backup a ignora sem efeito sobre a operação de backup. Para verificar se a tarefa de backup do site executou com sucesso o arquivo AfterBackup.bat, consulte o nó **Status do Componente** no espaço de trabalho **Monitoramento** e verifique as mensagens de status de SMS_SITE_BACKUP. Quando a tarefa inicia com êxito o arquivo de comando AfterBackup.bat, você vê uma mensagem ID 5040.  

> [!TIP]  
>  Para criar o arquivo AfterBackup.bat para arquivar os arquivos de backup do servidor do site, você deve usar uma ferramenta de comando de cópia, como o [Robocopy](http://go.microsoft.com/fwlink/p/?LinkId=228408), no arquivo em lotes. Por exemplo, você pode criar o arquivo AfterBackup.bat, e na primeira linha, adicionar algo semelhante a: `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

 Embora o uso pretendido do AfterBackup.bat seja arquivar instantâneos de backup, você pode criar um arquivo AfterBackup.bat para executar tarefas adicionais ao final de cada operação de backup.  

##  <a name="supplemental-backup-tasks"></a>Tarefas de backup complementares  
A tarefa de manutenção do servidor do site de backup fornece um instantâneo de backup para os arquivos do servidor do site e banco de dados do site, mas há outros itens sem backup que você deve considerar ao criar a estratégia de backup. Use as seções a seguir para ajudá-lo a concluir sua estratégia de backup do Configuration Manager.  

### <a name="back-up-custom-reporting-services-reports"></a>Fazer backup de relatórios personalizados do Reporting Services  
Quando você modifica ou cria relatórios personalizados do Reporting Services, criar backup para os arquivos de banco de dados do servidor é uma parte importante de sua estratégia de backup. O backup do servidor de relatórios deve incluir backup dos arquivos de origem para relatórios e modelos, chaves de criptografia, montagens ou extensões personalizadas, arquivos de configuração personalizados, visualizações do SQL Server usadas em relatórios personalizados, procedimentos de armazenamento personalizados, e assim por diante.  

> [!IMPORTANT]  
>  Quando o Configuration Manager é atualizado para uma versão mais recente, os relatórios predefinidos podem ser substituídos por novos relatórios. Se modificar um relatório predefinido, faça backup do relatório e restaure-o no Reporting Services.  

 Para obter mais informações sobre como fazer backup de relatórios personalizados no Reporting Services, veja [Operações de backup e restauração para uma instalação do Reporting Services](https://technet.microsoft.com/library/ms155814\(v=sql.120\).aspx) nos Manuais Online do SQL Server 2014.  

### <a name="back-up-content-files"></a>Fazer backup de arquivos de conteúdo  
A biblioteca de conteúdo no Configuration Manager é o local que armazena todos os arquivos de conteúdo para atualizações de software, aplicativos, implantação de sistema operacional e assim por diante. A biblioteca de conteúdo está localizada no servidor do site e em cada ponto de distribuição. A tarefa de manutenção do servidor do site de backup não inclui um backup para a biblioteca de conteúdo ou para os diretórios de origem do pacote. Quando um servidor do site falha, as informações sobre os arquivos da biblioteca de conteúdo são restauradas no banco de dados do site, mas você deve restaurar a biblioteca de conteúdo e os diretórios de origem do pacote no servidor do site.  

-   **Biblioteca de conteúdo**: a biblioteca de conteúdo deve ser restaurada antes de redistribuir o conteúdo nos pontos de distribuição. Quando você começa a redistribuição do conteúdo, o Configuration Manager copia os arquivos da biblioteca de conteúdo no servidor do site para os pontos de distribuição. A biblioteca de conteúdo do servidor do site está na pasta SCCMContentLib, que normalmente fica localizada na unidade com mais espaço livre em disco quando o site foi instalado.  

-   **Arquivos de origem do pacote**: os arquivos de origem do pacote devem ser restaurados antes de atualizar o conteúdo nos pontos de distribuição. Quando você inicia uma atualização de conteúdo, o Configuration Manager copia arquivos novos ou modificados da origem do pacote na biblioteca de conteúdo, que por sua vez, copia os arquivos nos pontos de distribuição associados. É possível executar a seguinte consulta no SQL Server para encontrar o local de origem do pacote de todos os pacotes e aplicativos: `SELECT * FROM v_Package`. É possível identificar o site de origem do pacote observando os três primeiros caracteres da ID do pacote. Por exemplo, se a ID do pacote for CEN00001, o código do site de origem será CEN. Ao restaurar os arquivos de origem do pacote, eles devem ser restaurados no mesmo local em que estavam antes da falha.  

 Certifique-se de incluir a biblioteca de conteúdo e os diretórios de origem do pacote em seu backup de sistema de arquivos para o servidor do site.  

### <a name="back-up-custom-software-updates"></a>Fazer backup de atualizações de software personalizadas  
 O System Center Updates Publisher 2011 é uma ferramenta autônoma que permite que você publique atualizações de software personalizadas no WSUS (Windows Server Update Services), sincronize-as com o Configuration Manager, avalie a conformidade das atualizações de software e implante-as nos clientes. O Updates Publisher usa um banco de dados local para seu repositório de atualização de software. Quando você usa o Updates Publisher para gerenciar atualizações de software personalizadas, determine se você deverá incluir o banco de dados do Updates Publisher em seu plano de backup. Para obter mais informações sobre o Updates Publisher, consulte [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) na biblioteca do System Center TechCenter.  

 Use o procedimento a seguir para fazer backup do banco de dados do Updates Publisher.  

#### <a name="to-back-up-the-updates-publisher-2011-database"></a>Para fazer o backup do banco de dados do Updates Publisher 2011  

1.  No computador que executa o Updates Publisher, navegue até o arquivo de banco de dados do Updates Publisher (Scupdb.sdf) em %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\\. Há um arquivo de banco de dados diferente para cada usuário que executa o Updates Publisher.  

2.  Copie o arquivo do banco de dados no destino de backup. Por exemplo, se o seu destino de backup for E:\ConfigMgr_Backup, você poderá copiar o arquivo de banco de dados do Updates Publisher para E:\ConfigMgr_Backup\SCUP2011.  

    > [!TIP]  
    >  Quando há mais de um arquivo de banco de dados em um computador, considere armazenar o arquivo em uma subpasta que indique o perfil do usuário associado ao arquivo de banco de dados. Por exemplo, pode haver um arquivo de banco de dados em E:\ConfigMgr_Backup\SCUP2011\User1 e outro em E:\ConfigMgr_Backup\SCUP2011\User2.  

## <a name="user-state-migration-data"></a>Dados de migração de estado do usuário  
Você pode usar as sequências da tarefas do Configuration Manager para capturar e restaurar dados de estado do usuário em cenários de implantação de sistema operacional no qual você deseja manter o estado do usuário do sistema operacional atual. As pastas que armazenam os dados do estado do usuário são listadas nas propriedades do ponto de migração de estado. Esses dados de migração de estado do usuário não ganham backup como parte da tarefa de manutenção de backup do servidor do site. Como parte do plano de backup, você deve fazer backup manualmente das pastas especificadas para armazenar os dados de migração do estado do usuário.   

### <a name="to-determine-the-folders-used-to-store-user-state-migration-data"></a>Para determinar as pastas usadas para armazenar dados de migração de estado do usuário  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração**, expanda **Configuração de Site** e escolha **Funções de Servidores e Sistema de Site**.  

3.  Selecione o sistema de sites que hospeda a função de migração de estado e escolha **Ponto de migração de estado** em **Funções do Sistema de Sites**.  


4.  Na guia **Função do Site** , no grupo **Propriedades** , clique em **Propriedades**.  
5.  As pastas que armazenam os dados de migração de estado do usuário estão listadas na seção **Detalhes da Pasta** na guia **Geral** .  



## <a name="about-the-sms-writer-service"></a>Sobre o serviço SMS Writer  
O SMS Writer é um serviço que interage com o VSS (Serviço de Cópias de Sombra de Volume) durante o processo de backup. O serviço SMS Writer deve estar em execução para o backup do site do Configuration Manager para ser concluído com êxito.  

### <a name="purpose"></a>Finalidade  
O SMS Writer registra-se no serviço VSS e se associa às suas interfaces e eventos. Quando o VSS transmite eventos ou envia notificações específicas para o SMS Writer, o SMS Writer responde à notificação e executa a ação apropriada. O SMS Writer lê o arquivo de controle de backup (smsbkup.ctl), localizado em &lt;*Caminho de Instalação do ConfigMgr*>\inboxes\smsbkup.box, e determina os arquivos e os dados que devem ser armazenados em backup. O SMS Writer cria metadados, que consistem em vários componentes, com base nessas informações e em dados específicos da chave e das subchaves de registro de SMS. O serviço envia os metadados ao VSS quando solicitado. Em seguida, o VSS envia os metadados ao aplicativo solicitante, o Gerenciador de Backup do Configuration Manager. O Gerenciador de Backup seleciona os dados que passam por backup e envia esses dados ao SMS Writer via VSS. O SMS Writer executa as etapas apropriadas para se preparar para o backup. Quando o VSS está pronto para capturar o instantâneo, ele envia um evento, o SMS Writer interrompe todos os serviços do Configuration Manager e assegura que as atividades do Configuration Manager sejam congeladas enquanto o instantâneo é criado. Depois que o instantâneo é concluído, o SMS Writer reinicia os serviços e as atividades.  

O serviço SMS Writer é instalado automaticamente. Ele deve estar em execução quando o aplicativo VSS solicitar um backup ou uma restauração.  

### <a name="writer-id"></a>ID do gravador  
A ID do gravador do SMS Writer é: 03ba67dd-dc6d-4729-a038-251f7018463b.  

### <a name="permissions"></a>Permissões  
O serviço SMS Writer deve ser executado pela conta Sistema Local.  

### <a name="volume-shadow-copy-service"></a>Serviço de Cópias de Sombra de Volume  
O VSS é um conjunto de APIs COM que implementa uma estrutura para permitir a execução de backups de volume enquanto os aplicativos de um sistema continuam a ser gravados nos volumes. O VSS fornece uma interface consistente que permite a coordenação entre os aplicativos do usuário que atualizam dados em disco (o serviço SMS Writer) e aqueles que fazem backup dos aplicativos (o serviço Gerenciador de Backup). Para saber mais, veja o tópico [Serviço de Cópias de Sombra de Volume](http://go.microsoft.com/fwlink/p/?LinkId=241968) no Windows Server TechCenter.  

## <a name="next-steps"></a>Próximas etapas
Depois de criar um backup, pratique a [recuperação de site](/sccm/protect/understand/recover-sites) com esse backup. Isso pode ajudá-lo a se familiarizar com o processo de recuperação antes de precisar confiar nele e pode ajudar a confirmar que o backup foi bem-sucedido para a finalidade pretendida.  
