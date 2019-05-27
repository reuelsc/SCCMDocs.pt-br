---
title: Sites de backup
titleSuffix: Configuration Manager
description: Saiba como fazer o backup de seus sites antes do evento de falha ou perda de dados no Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: aff3393dca29d558c62c0a508b8cbf6c98f9fbfa
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65501231"
---
# <a name="back-up-a-configuration-manager-site"></a>Fazer backup de um site do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Prepare abordagens de backup e recuperação para evitar perda de dados. Para sites do Configuration Manager uma abordagem de backup e recuperação pode ajudá-lo a recuperar sites e hierarquias mais rapidamente e com o mínimo de perda de dados.  

As seções neste artigo podem ajudá-lo a fazer backup de seus sites. Para recuperar um site, veja [Recuperação para o Configuration Manager](/sccm/core/servers/manage/recover-sites).  



## <a name="considerations-before-creating-a-backup"></a>Considerações antes de criar um backup  

-   Se você usa um grupo de disponibilidade Always On do SQL Server para hospedar o banco de dados do site: modifique seus planos de backup e recuperação conforme descrito em [Preparar para usar o SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-backup).  

-   O Configuration Manager pode recuperar o banco de dados do site da tarefa de backup do Configuration Manager. Ele também pode usar um backup do banco de dados do site que você cria com outro processo.   

     Por exemplo, é possível restaurar o banco de dados do site de um backup criado como parte de um plano de manutenção do Microsoft SQL Server. Você também pode usar um backup criado usando o Data Protection Manager para fazer backup de seu banco de dados do site.  

-   Da versão 1806 em diante, instale um servidor de site adicional no modo *passivo*. O servidor do site no modo passivo é usado além do servidor do site existente no modo *ativo*. Um servidor do site no modo passivo está disponível para uso imediato quando for necessário. Para obter mais informações, confira [Alta disponibilidade do servidor do Site](/sccm/core/servers/deploy/configure/site-server-high-availability). Embora essa função não elimine a necessidade de planejar e executar operações de backup e recuperação, ela reduz consideravelmente o esforço para recuperar um site quando necessário.  
  

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>Usando o Data Protection Manager para fazer backup do banco de dados do site
Você pode usar o System Center DPM (Data Protection Manager) para fazer backup do banco de dados do site do Configuration Manager.

Crie um novo grupo de proteção no DPM para o computador do banco de dados do site. Na página **Selecionar Membros do Grupo** do Assistente para Criar Novo Grupo de Proteção, selecione o serviço SMS Writer na lista de fontes de dados. Em seguida, selecione o banco de dados do site como um membro apropriado. Para obter mais informações sobre o uso do DPM, veja a biblioteca de documentação do [Data Protection Manager](https://docs.microsoft.com/system-center/dpm).  

> [!IMPORTANT]  
>  O Configuration Manager não é compatível com backup do DPM para um cluster do SQL Server que use uma instância nomeada. Ele é compatível com backup de DPM em um cluster do SQL Server que use a instância padrão do SQL Server.  

Depois de restaurar o banco de dados do site, siga as etapas na instalação para recuperar o site. Para usar o banco de dados do site do qual você fez backup com o Data Protection Manager, selecione a opção de recuperação para **Usar um banco de dados de site recuperado manualmente**.  



## <a name="backup-maintenance-task"></a>Tarefa de manutenção de backup
É possível automatizar o backup de sites do Configuration Manager agendando a tarefa de manutenção Servidor do Site de Backup predefinida. Essa tarefa tem os seguintes recursos:

-   É executada conforme um agendamento
-   Faz backup do banco de dados do site
-   Faz backup de chaves específicas do Registro
-   Faz backup de arquivos e pastas específicas
-   Faz backup da [pasta CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder)   

Planeje executar a tarefa padrão de backup do site pelo menos a cada cinco dias. Esse agendamento ocorre porque o Configuration Manager usa um *Período de retenção do controle de alterações do SQL Server* de cinco dias. Para obter mais informações, veja [Período de retenção do controle de alterações do SQL Server](/sccm/protect/understand/recover-sites#bkmk_SQLretention).

Para simplificar o processo de backup, crie um arquivo **AfterBackup.bat**. Esse script executa automaticamente ações pós-backup depois que a tarefa de backup é concluída com êxito. Use o arquivo AfterBackup.bat para arquivar o instantâneo de backup em um local seguro. Também é possível usar o arquivo AfterBackup.bat para copiar arquivos para a pasta de backup ou iniciar outras tarefas de backup.  

Você pode fazer backup de um site de administração central e de um site primário. Sites secundários ou servidores do sistema de sites não têm tarefas de backup.

Quando o serviço de backup do Configuration Manager é executado, ele segue as instruções definidas no arquivo de controle de backup: `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box\Smsbkup.ctl`. É possível modificar o arquivo de controle de backup para alterar o comportamento do serviço de backup.  
> [!NOTE]
> As modificações de **Smsbkup.ctl** serão aplicadas após a reinicialização do serviço SMS_SITE_VSS_WRITER no servidor do site ser executada.

As informações de status de backup do site são gravadas no arquivo **Smsbkup.log** . O arquivo é criado na pasta de destino especificada nas propriedades da tarefa de manutenção do Servidor do Site de Backup.  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>Para habilitar a tarefa de manutenção de backup do site  
1.  No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**.  

2.  Selecione o site no qual deseja habilitar a tarefa de manutenção de backup do site.  

3.  Clique em **Tarefas de Manutenção do Site** na faixa de opções.  

4.  Selecione a tarefa **Servidor do Site de Backup** e, em seguida, clique em **Editar**.  

5.  Selecione a opção para **Habilitar esta tarefa**. Clique em **Definir Caminhos** para especificar o destino do backup. Você tem as seguintes opções:  

    > [!IMPORTANT]  
    >  Para ajudar a evitar a violação dos arquivos de backup, armazene os arquivos em um local seguro. O caminho de backup mais seguro é para uma unidade local que possibilite definir permissões do arquivo NTFS na pasta. O Configuration Manager não criptografa os dados de backup armazenados no caminho do backup.  

    -   **Unidade local no servidor do site para dados e banco de dados do site**: especifica que a tarefa armazene os arquivos de backup do site e do banco de dados do site no caminho especificado na unidade de disco local do servidor do site. Crie a pasta local antes das execuções de tarefa de backup. A conta do Sistema Local no servidor do site deve ter permissões de arquivo NTFS de **Gravação** para a pasta local do backup do servidor do site. A conta Sistema Local no computador que está executando o SQL Server deve ter permissões de **Gravação** do NTFS para a pasta do backup do banco de dados do site.  

    -   **Caminho de rede (nome UNC) para dados e banco de dados do site**: especifica que a tarefa armazene os arquivos de backup para o site e o banco de dados do site no caminho de rede especificado. Crie o compartilhamento antes da execução da tarefa de backup. A conta de computador do servidor do site deve ter permissões de compartilhamento e NTFS de **Gravação** para a pasta de rede compartilhada. Se o SQL Server estiver instalado em outro computador, a conta de computador do SQL Server deverá ter as mesmas permissões.  

    -   **Unidades locais no servidor do site e SQL Server**: especifica que a tarefa armazene os arquivos de backup para o site no caminho especificado na unidade local do servidor do site. A tarefa armazena os arquivos de backup do banco de dados do site no caminho especificado na unidade local do servidor de banco de dados do site. Crie as pastas locais antes da execução da tarefa de backup. A conta de computador do servidor do site deve ter permissões de **Gravação** NTFS para a pasta criada no servidor do site. A conta de computador do SQL Server deve ter permissões de **Gravação** NTFS para a pasta criada no servidor de banco de dados do site. Essa opção está disponível somente quando o banco de dados do site não está instalado no servidor do site.  

    > [!NOTE]  
    >   A opção de navegar até o destino do backup está disponível somente quando você especifica o caminho de rede do destino do backup.  
    >  
    > O nome da pasta ou do compartilhamento usado como destino do backup não é compatível com o uso de caracteres Unicode.  

6.  Configure um agendamento para a tarefa de backup do site. Considere um agendamento de backup que esteja fora do horário comercial ativo. Se você tiver uma hierarquia, considere um agendamento que seja executado pelo menos duas vezes por semana. Se o site falhar, esse agendamento garantirá a máxima retenção de dados.  

    Ao executar o console do Configuration Manager no mesmo servidor do site que você está configurando para backup, a tarefa de backup usará o horário local para o agendamento. Quando você executa o console do Configuration Manager de outro computador, a tarefa de backup usa o UTC (Tempo Universal Coordenado) para o agendamento.  

7.  Escolha se deseja criar um alerta se a tarefa de backup do site falhar. Quando selecionada, o Configuration Manager cria um alerta crítico para a falha do backup. Você pode examinar esses alertas no nó **Alertas** no workspace **Monitoramento**.  

#### <a name="verify-that-the-backup-site-server-maintenance-task-is-running"></a>Verificar se a tarefa de manutenção Servidor do Site de Backup está em execução  

-   Confira o carimbo de data/hora dos arquivos na pasta de destino do backup que a tarefa criou. Verifique se que o carimbo de data/hora é atualizado para a última hora em que a tarefa foi agendada para ser executada.  

-   Vá para o nó **Status do Componente** do workspace **Monitoramento**. Examine as mensagens de status **SMS_SITE_BACKUP**. Quando o backup do site for concluído com êxito, você verá a ID da mensagem **5035**. Essa mensagem indica que o backup do site foi concluído sem erros.  

-   Quando você configura a tarefa de backup para criar um alerta quando ela falhar, examine os alertas de falha de backup no nó **Alertas** do workspace **Monitoramento**.  

-   Abra o Windows Explorer no servidor do site e navegue até `<ConfigMgrInstallationFolder>\Logs`. Examine **Smsbkup.log** para verificar se há avisos e erros. Quando o backup do site for concluído com êxito, o log mostrará `Backup completed` com a ID de mensagem `STATMSG: ID=5035`.  

    > [!TIP]  
    >  Quando a tarefa de manutenção de backup falha, reinicie-a parando e reiniciando o serviço Windows **SMS_SITE_BACKUP**.  



## <a name="archive-the-backup-snapshot"></a>Arquivar o instantâneo de backup  
A tarefa de backup cria um instantâneo de backup na primeira vez em que é executada. Você poderá usar esse instantâneo para recuperar o servidor do site se ele falhar. Quando a tarefa de backup é executada novamente no agendamento, ela cria um novo instantâneo de backup que substitui o anterior. Assim, o site tem apenas um instantâneo de backup e não há como recuperar um instantâneo de backup anterior.  

Mantenha vários arquivos do instantâneo de backup pelos seguintes motivos:  

-   É comum que a mídia de backup falhe, seja extraviada ou contenha apenas um backup parcial. Recuperar um site primário autônomo com falha de um backup mais antigo é melhor do que recuperar sem qualquer backup. Para um servidor de site em uma hierarquia, o backup deve estar no período de retenção do controle de alterações do SQL Server, ou o backup não será necessário.  

-   Uma corrupção no site pode não ser detectada durante vários ciclos de backup. Pode ser necessário usar um instantâneo de backup anterior à corrupção do site. Esse motivo se aplica a um site primário autônomo e a sites em uma hierarquia em que o backup está no período de retenção do controle de alterações do SQL Server.  

-   O site não pode ter nenhum instantâneo de backup. Por exemplo, se a tarefa de manutenção do Servidor do Site de Backup falhar. Como a tarefa de backup remove o instantâneo de backup anterior antes de ele começar a fazer o backup dos dados atuais, não haverá um instantâneo de backup válido.  



## <a name="using-the-afterbackupbat-file"></a>Usando o arquivo AfterBackup.bat  
Após o backup bem-sucedido do site, a tarefa de backup tenta automaticamente executar um script chamado **AfterBackup.bat**. Crie manualmente o arquivo AfterBackup.bat no servidor do site em `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box`. Se existir um arquivo AfterBackup.bat na pasta correta, ele será executado automaticamente depois que a tarefa de backup for concluída.

O arquivo AfterBackup.bat permite arquivar o instantâneo de backup ao final de cada operação de backup. Ele pode realizar automaticamente outras tarefas pós-backup que não fazem parte da tarefa de manutenção do Servidor do Site de Backup. O arquivo AfterBackup.bat integra o arquivo e as operações de backup, garantindo assim que cada novo instantâneo de backup seja arquivado.

Se o arquivo AfterBackup.bat não estiver presente, a tarefa de backup o ignorará sem afetar a operação de backup. Para verificar se a tarefa de backup executou com sucesso esse script, veja o nó **Status do Componente** no workspace **Monitoramento** e examine as mensagens de status de **SMS_SITE_BACKUP**. Quando a tarefa iniciar com êxito após o arquivo de comando AfterBackup.bat, você verá a ID da mensagem **5040**.  

> [!TIP]  
>  Para arquivar os arquivos de backup do servidor do site com AfterBackup.bat, você deve usar uma ferramenta de comando de cópia no arquivo de lote. Uma dessas ferramentas é [Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy) no Windows Server. Por exemplo, crie o arquivo AfterBackup.bat com o seguinte comando: `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

Embora o uso pretendido do AfterBackup.bat seja arquivar instantâneos de backup, você pode criar um arquivo AfterBackup.bat para executar tarefas adicionais ao final de cada operação de backup.  



##  <a name="supplemental-backup-tasks"></a>Tarefas de backup complementares  
A tarefa de manutenção do Servidor do Site de Backup fornece um instantâneo de backup para os arquivos de servidor do site e banco de dados do site. Há outros itens sem backup que você deve considerar ao criar sua estratégia de backup. Use estas seções para ajudá-lo a concluir sua estratégia de backup do Configuration Manager.  

### <a name="back-up-custom-reports"></a>Fazer backup de relatórios personalizados   
Se você modificar relatórios personalizados predefinidos ou criados no SQL Server Reporting Services, crie um backup para os arquivos do banco de dados do servidor de relatório. O backup do servidor de relatório deve incluir os seguintes componentes:
- Os arquivos de origem para relatórios e modelos
- Chaves de criptografia
- Assemblies ou extensões personalizadas
- Arquivos de configuração
- Exibições personalizadas do SQL Server usadas em relatórios personalizados
- Procedimentos armazenados personalizados  

> [!IMPORTANT]  
>  Quando o Configuration Manager é atualizado para uma versão mais recente, os relatórios predefinidos podem ser substituídos por novos relatórios. Se você modificar um relatório predefinido, faça backup do relatório e restaure-o no Reporting Services.  

Para obter mais informações sobre como restaurar relatórios personalizados no Reporting Services, veja [Operações de backup e restauração para o Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).  

### <a name="back-up-content-files"></a>Fazer backup de arquivos de conteúdo  
A biblioteca de conteúdo no Configuration Manager é o local em que todos os arquivos de conteúdo são armazenados para todas as implantações de software. A biblioteca de conteúdo está localizada no servidor do site e em cada ponto de distribuição. A tarefa de manutenção do Servidor do Site de Backup não faz backup da biblioteca de conteúdo nem de arquivos de origem do pacote. Quando um servidor do site falha, as informações sobre a biblioteca de conteúdo são restauradas no banco de dados do site, mas você deve restaurar a biblioteca de conteúdo e os arquivos de origem do pacote.  

-   A biblioteca de conteúdo deve ser restaurada antes de redistribuir o conteúdo nos pontos de distribuição. Quando você começa a redistribuição do conteúdo, o Configuration Manager copia os arquivos da biblioteca de conteúdo no servidor do site para os pontos de distribuição. Para obter mais informações, confira [A biblioteca de conteúdo](/sccm/core/plan-design/hierarchy/the-content-library).  

-   Os arquivos de origem do pacote devem ser restaurados antes de atualizar o conteúdo nos pontos de distribuição. Quando você começa uma atualização de conteúdo, o Configuration Manager copia arquivos novos ou modificados da origem do pacote para a biblioteca de conteúdo. Em seguida, ele copia os arquivos para pontos de distribuição associados. Execute a seguinte consulta do SQL Server no banco de dados do site para encontrar o local de origem do pacote para todos os pacotes e aplicativos: `SELECT * FROM v_Package`. É possível identificar o site de origem do pacote observando os três primeiros caracteres da ID do pacote. Por exemplo, se a ID do pacote for CEN00001, o código do site de origem será CEN. Ao restaurar os arquivos de origem do pacote, eles devem ser restaurados no mesmo local em que estavam antes da falha.  

Inclua a biblioteca de conteúdo e os arquivos de origem do pacote em seu backup de sistema de arquivos para o servidor do site.  

### <a name="back-up-custom-software-updates"></a>Fazer backup de atualizações de software personalizadas  
O System Center Updates Publisher é uma ferramenta autônoma que permite que você gerencie atualizações de software personalizadas. O Updates Publisher usa um banco de dados local para seu repositório de atualização de software. Quando você usa o Updates Publisher para gerenciar atualizações de software personalizadas, determine se você deverá incluir o banco de dados do Updates Publisher em seu plano de backup. Para obter mais informações, confira [System Center Updates Publisher](/sccm/sum/tools/updates-publisher).  

Use o procedimento a seguir para fazer backup do banco de dados do Updates Publisher.  

#### <a name="back-up-the-updates-publisher-database"></a>Fazer backup do banco de dados do Updates Publisher  

1.  No computador que executa o Updates Publisher, navegue até o arquivo de banco de dados do Updates Publisher **Scupdb.sdf** em `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\`. Há um arquivo de banco de dados diferente para cada usuário que executa o Updates Publisher.  

2.  Copie o arquivo do banco de dados no destino de backup. Por exemplo, se o seu destino de backup for `E:\ConfigMgr_Backup`, você poderá copiar o arquivo de banco de dados do Updates Publisher para `E:\ConfigMgr_Backup\SCUP`.  

    > [!TIP]  
    >  Quando há mais de um arquivo de banco de dados em um computador, considere armazenar o arquivo em uma subpasta que indique o perfil do usuário associado ao arquivo de banco de dados. Por exemplo, você poderia ter um arquivo de banco de dados `E:\ConfigMgr_Backup\SCUP\User1` e outro arquivo de banco de dados no `E:\ConfigMgr_Backup\SCUP\User2`.  



## <a name="user-state-migration-data"></a>Dados de migração de estado do usuário  
Você pode usar sequências de tarefas do Configuration Manager para capturar e restaurar os dados de estado do usuário em cenários de implantação do sistema operacional. As propriedades do ponto de migração de estado listam as pastas que armazenam os dados de estado do usuário. Não é feito o backup desses dados como parte da tarefa de manutenção de Backup do Servidor do Site. Como parte do plano de backup, você deve fazer backup manualmente das pastas especificadas para armazenar os dados de migração do estado do usuário.   

### <a name="determine-the-folders-used-to-store-user-state-migration-data"></a>Determinar as pastas usadas para armazenar dados de migração de estado do usuário  

1.  No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Funções do Sistema de Sites e Servidores**.  

2.  Selecione o sistema de sites que hospeda a função de migração de estado. Em seguida, selecione **Ponto de migração de estado** no painel **Funções do Sistema de Sites**.  

3.  Na faixa de opções, clique em **Propriedades**.  

4.  As pastas que armazenam os dados de migração de estado do usuário estão listadas na seção **Detalhes da Pasta** na guia **Geral** .  



## <a name="about-the-sms-writer-service"></a>Sobre o serviço SMS Writer  
O SMS Writer é um serviço que interage com o VSS (Serviço de Cópias de Sombra de Volume) do Windows durante o processo de backup. O serviço SMS Writer deve estar em execução para o backup do site do Configuration Manager ser concluído com êxito.  

### <a name="process"></a>Processar  
1. O SMS Writer registra-se no serviço VSS e se associa às suas interfaces e eventos. 
2. Quando o VSS transmite eventos ou envia notificações específicas para o SMS Writer, o SMS Writer responde à notificação e executa a ação apropriada. 
3. O SMS Writer lê o arquivo de controle de backup **smsbkup.ctl** localizado em `<ConfigMgrInstallationPath>\inboxes\smsbkup.box` e determina os arquivos e os dados para backup. 
4. O SMS Writer cria metadados, que consiste em vários componentes, incluindo dados específicos da chave do Registro do SMS e subchaves. 
    a. Ele envia os metadados ao VSS quando solicitado. 
    b. O VSS então envia os metadados ao aplicativo solicitante, o Gerenciador de Backup do Configuration Manager. 
5. O Gerenciador de Backup seleciona os dados que passam por backup e os envia ao SMS Writer via VSS. 
6. O SMS Writer executa as etapas apropriadas para se preparar para o backup. 
7. Posteriormente, quando o VSS está pronto para capturar o instantâneo: a. Ele envia um evento b. O SMS Writer interrompe todos os serviços do Configuration Manager c. Isso garante que as atividades do Configuration Manager sejam congeladas enquanto o instantâneo é criado. 
8. Depois que o instantâneo é concluído, o SMS Writer reinicia os serviços e as atividades.

O serviço SMS Writer é instalado automaticamente. Ele deve estar em execução quando o aplicativo VSS solicitar um backup ou uma restauração.  

### <a name="writer-id"></a>ID do gravador  
A ID do gravador do SMS Writer é **03ba67dd-dc6d-4729-a038-251f7018463b**.  

### <a name="permissions"></a>Permissões  
O serviço SMS Writer deve ser executado pela conta Sistema Local.  

### <a name="volume-shadow-copy-service"></a>Serviço de Cópias de Sombra de Volume  
O VSS é um conjunto de APIs COM que implementa uma estrutura para permitir a execução de backups de volume enquanto os aplicativos de um sistema continuam a ser gravados nos volumes. O VSS fornece uma interface consistente que permite a coordenação entre os aplicativos do usuário que atualizam dados em disco (o serviço SMS Writer) e aqueles que fazem backup dos aplicativos (o serviço Gerenciador de Backup). Para obter mais informações, veja [Serviço de Cópias de Sombra de Volume](https://go.microsoft.com/fwlink/p/?LinkId=241968).  



## <a name="next-steps"></a>Próximas etapas
Depois de criar um backup, pratique a [recuperação de site](/sccm/protect/understand/recover-sites) com esse backup. Essa prática pode ajudar você a se familiarizar com o processo de recuperação antes de precisar usá-lo. Também pode ajudar a confirmar que o backup foi bem-sucedido para a finalidade pretendida.  
