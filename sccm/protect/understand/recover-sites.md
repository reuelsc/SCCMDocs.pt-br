---
title: "Recuperação de site"
titleSuffix: Configuration Manager
description: Aprenda a recuperar seus sites no System Center Configuration Manager.
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 497860c9b5698271d7ca6e4683e99350100f596f
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
#  <a name="recover-a-configuration-manager-site"></a>Recuperar um site do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Execute uma recuperação de site do Configuration Manager depois que um site do Configuration Manager falhar ou ocorrer perda de dados no banco de dados do site. Reparação e nova sincronização de dados são as tarefas principais de uma recuperação de site para evitar a interrupção das operações.

As seções neste tópico podem ajudá-lo a recuperar um site do Configuration Manager. Para criar um backup, veja [Backup para o Configuration Manager](/sccm/protect/understand/backup-and-recovery).

## <a name="considerations-before-recovering-a-site"></a>Considerações antes de recuperar um site
> [!Important]  
> Essas informações aplicam-se somente a cenários de recuperação de site.  Quando você estiver atualizando sua infraestrutura local e não estiver recuperando ativamente um site com falha, examine as informações nos tópicos a seguir:
> - [Atualizar infraestrutura local](/sccm/core/servers/manage/upgrade-on-premises-infrastructure)
> - [Modificar sua infra-estrutura](/sccm/core/servers/manage/modify-your-infrastructure)


**Você deve usar a mesma versão e edição do SQL Server:** por exemplo, não há suporte à restauração de um banco de dados que era executado no SQL Server 2014 no SQL Server 2016. Da mesma forma, não há suporte para restaurar um banco de dados do site executado em uma Standard Edition do SQL Server 2016 para uma Enterprise Edition do SQL Server 2016.
-   O SQL Server não deve ser definido como **modo de usuário único**.
-   Certifique-se de que os arquivos .MDF e .LDF são válidos. Ao recuperar um site, não há verificação para o estado dos arquivos que estão sendo restaurados.

**Se você usar um grupo de disponibilidade do AlwaysOn do SQL Server para hospedar o banco de dados do site:** modifique seus planos de recuperação conforme descrito em [Preparar para usar o AlwaysOn do SQL Server](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-recovery).

**Quando você usa réplicas de banco de dados:** após restaurar o banco de dados do site que estava configurado para as réplicas de banco de dados, reconfigure cada réplica para poder usá-las, recriando as publicações e assinaturas.

## <a name="determine-your-recovery-options"></a>Determinar as opções de recuperação
Há duas áreas principais para considerar para a recuperação do servidor do site primário e site de administração central do Configuration Manager, o **servidor do site** e o **banco de dados do site**.
As seções a seguir podem ajudá-lo a selecionar as melhores opções para seu cenário de recuperação.

> [!NOTE]   
> Quando a instalação detecta um site do Configuration Manager existente no servidor, é possível iniciar uma recuperação de site, mas as opções de recuperação do servidor do site são limitadas. Por exemplo, se você executar a instalação em um servidor de site existente, quando escolher a recuperação poderá recuperar o servidor de banco de dados do site, mas a opção de recuperação do servidor do site estará desativada.

### <a name="site-server-recovery-options"></a>Opções de recuperação do servidor do site
Inicie a Instalação de uma cópia da pasta **CD.Latest** criada fora da pasta de instalação do Configuration Manager.
-   Se você executar a instalação do Configuration Manager por meio do menu **Iniciar** no servidor do site, a opção **Recuperar um site** não estará disponível.
-   Se você instalou atualizações de dentro do console do Configuration Manager antes de ter feito o backup, não poderá reinstalar com êxito o site usando a instalação por meio da mídia de instalação ou o caminho de instalação do Configuration Manager.

Em seguida, selecione a opção **Recuperar um site**. Você tem as seguintes opções de recuperação para o servidor do site que falhou:

-   **Recuperar o servidor do site usando um backup existente**: use essa opção quando houver um backup do servidor do site do Configuration Manager criado no servidor do site, como parte da tarefa de manutenção **Servidor do Site de Backup** anterior à falha. O site é reinstalado e as definições configuradas, com base no site de backup.
-   **Reinstalar o servidor do site**: use essa opção quando não houver backup do servidor do site. O servidor do site é reinstalado e você deve especificar as configurações do site, assim como faria durante uma instalação inicial.
  -   Você deve usar o mesmo código e nome de banco de dados do site que usou quando o site com falha foi instalado pela primeira vez.
  -   Você pode reinstalar o site em um novo computador que executa um novo sistema operacional.
  -   O computador deve usar o mesmo nome de domínio totalmente qualificado do servidor do site original.   

### <a name="site-database-recovery-options"></a>Opções de recuperação do banco de dados do site
Quando você executa a instalação, tem as seguintes opções de recuperação para o banco de dados do site:
-   **Recuperar o banco de dados do site usando um conjunto de backup**: use essa opção quando você tiver um backup do banco de dados do site do Configuration Manager criado como parte da tarefa de manutenção do **Servidor do Site de Backup** anterior à falha do banco de dados do site. Quando há uma hierarquia, as alterações feitas no banco de dados do site após o último backup do banco de dados do site são recuperadas do site de administração central para um site primário, ou de um site primário de referência para um site de administração central. Ao recuperar o banco de dados do site para um site primário autônomo, as alterações do site após o último backup são perdidas.

   Ao recuperar o banco de dados do site para um site em uma hierarquia, o comportamento de recuperação é diferente para sites de administração central e sites primários, e quando o último backup está dentro ou fora do período de retenção de controle de alterações do SQL Server. Para obter mais informações, consulte a seção [Cenários de recuperação de banco de dados do site](##site-database-recovery-scenarios) neste tópico.
  > [!NOTE]   
  > A recuperação falha ao selecionar a opção para restaurar o banco de dados do site usando um conjunto de backup, mas o banco de dados do site já existe.  

-   **Criar um novo banco de dados para este site**: use essa opção quando não houver backup do banco de dados do site do Configuration Manager. Quando há uma hierarquia, o novo banco de dados do site é criado e os dados são recuperados usando dados replicados do site de administração central para um site primário, ou de um site primário de referência para um site de administração central. Essa opção não está disponível quando se recupera um local primário autônomo ou um site de administração central que não tem sites primários.

-   **Usar um banco de dados do site recuperado manualmente**: use essa opção quando você já tiver recuperado o banco de dados do site do Configuration Manager, mas precisar concluir o processo de recuperação.
    -   O Configuration Manager pode recuperar o banco de dados do site por meio da tarefa de manutenção de backup do Configuration Manager ou de um backup do banco de dados do site realizado usando o DPM ou outro processo. Depois de restaurar o banco de dados do site usando um método fora do Configuration Manager, é necessário executar a Instalação e selecionar essa opção para concluir a recuperação do banco de dados do site.

    > [!NOTE]   
    > Quando o DPM for usado para fazer backup do banco de dados do site, use os procedimentos do DPM para restaurar o banco de dados do site para um local especificado antes de continuar o processo de restauração no Configuration Manager. Para obter mais informações sobre o DPM, consulte a [Biblioteca de Documentação do Data Protection Manager]() no TechNet.    

    -   Quando há uma hierarquia, as alterações feitas no banco de dados do site após o último backup do banco de dados do site são recuperadas do site de administração central para um site primário, ou de um site primário de referência para um site de administração central. Ao recuperar o banco de dados do site para um site primário autônomo, as alterações do site após o último backup são perdidas.     


-   **Ignorar recuperação do banco de dados**: use essa opção quando não ocorrer perda de dados no servidor de banco de dados do site do Configuration Manager. Essa opção é válida somente quando o banco de dados do site está em um computador diferente do servidor do site que está sendo recuperado.

### <a name="sql-server-change-tracking-retention-period"></a>Período de retenção do controle de alterações do SQL Server
O controle de alterações é habilitado para o banco de dados do site no SQL Server. O controle de alterações permite que o Configuration Manager consulte informações sobre as alterações feitas nas tabelas do banco de dados após determinado período anterior. O período de retenção especifica por quanto tempo as informações do controle de alterações são mantidas. Por padrão, o banco de dados do site é configurado para ter um período de retenção de 5 dias. Ao recuperar um banco de dados do site, o processo de recuperação procede de maneira diferente quando o backup está dentro ou está fora do período de retenção. Por exemplo, se o servidor de banco de dados do site falhar e o último backup tiver 7 dias, ele estará fora do período de retenção.

Para obter mais informações sobre elementos internos de controle de alterações do SQL Server, consulte os seguintes blogs da equipe do SQL Server: [Limpeza do Controle de Alterações – parte 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1/) e [Limpeza do Controle de Alterações – parte 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2).

### <a name="reinitialization-of-site-or-global-data"></a>Reinicialização de site ou dados globais
O processo para reinicializar o site ou dados globais substitui dados existentes no banco de dados do site por dados de outro banco de dados do site. Por exemplo, quando o site ABC reinicializa os dados do site XYZ, ocorrem as seguintes etapas:
-   Os dados são copiados do site XYZ para o site ABC.
-   Os dados existentes do site XYZ são removidos do banco de dados do site ABC.
-   Os dados copiados do site XYZ são inseridos no banco de dados do site ABC.

#### <a name="example-scenario-1"></a>Cenário de exemplo 1
**O site primário reinicializa os dados globais do site de administração central**: o processo de recuperação remove os dados globais existentes do site primário no banco de dados do site primário e substitui os dados pelos dados globais copiados do site de administração central.

#### <a name="example-scenario-2"></a>Cenário de exemplo 2
**O site de administração central reinicializa os dados do site de um site primário**: o processo de recuperação remove os dados existentes desse site primário no banco de dados do site de administração central e substitui os dados pelos dados copiados do site primário. Os dados do site de outros sites primários não são afetados.

### <a name="site-database-recovery-scenarios"></a>Cenários de recuperação de banco de dados do site
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

## <a name="site-recovery-procedures"></a>Procedimentos de recuperação do site
Use um dos procedimentos a seguir como auxílio para recuperar o servidor do site e o banco de dados do site.

### <a name="to-start-a-site-recovery-in-the-setup-wizard"></a>Para iniciar uma recuperação do site no Assistente de Instalação
1.  Copie a [pasta CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder) para um local fora da pasta de Instalação do Configuration Manager.
Por meio da cópia da pasta CD.Latest, execute o Assistente de instalação do Configuration Manager.

2.  Na página **Guia de Introdução** , selecione **Recuperar um site**e clique em **Avançar**.

3.  Conclua o assistente usando as opções apropriadas para a recuperação de site.

  -   Durante a recuperação, a Instalação identifica a porta do SQL Server Service Broker (SSB) usada pelo SQL Server. Não altere essa configuração de porta durante a recuperação; caso contrário, a replicação de dados não funcionará corretamente após o término da recuperação.

  -   Você pode especificar o caminho novo ou o original para usar na instalação do Configuration Manager no Assistente de Instalação.

### <a name="to-start-an-unattended-site-recovery"></a>Para iniciar uma recuperação autônoma do site
  1.    Prepare o script de instalação autônoma para as opções necessárias para a recuperação de site.  Veja [Chaves de arquivo de script de recuperação autônoma do site](/sccm/protect/understand/unattended-site-recovery-script-file-keys).

  2.    Execute a Instalação do Configuration Manager usando a opção **/script** do comando. Por exemplo, se você nomeasse seu arquivo de inicialização de instalação como ConfigMgrUnattend.ini e o salvasse no diretório C:\Temp do computador no qual a instalação está em execução, o comando seria o seguinte: **Setup /script C:\temp\ConfigMgrUnattend.ini**.

  > [!NOTE]   
  >  Depois de recuperar um site de administração central, a replicação de alguns dados de sites filho pode não ser estabelecida. Isso pode incluir inventário de hardware, inventário de software e mensagens de status.
  >
  >  Se isso ocorrer, será necessário reinicializar o **ConfigMgrDRSSiteQueue** para a replicação de banco de dados.  Para fazer isso, use o **SQL Server Manager** para executar a seguinte consulta no banco de dados do site do Configuration Manager no site de administração central:
  >
  >  **IF EXISTS (SELECT \* FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)**
  >
  >  **ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON**


## <a name="post-recovery-tasks"></a>Tarefas de pós-recuperação
Feita a recuperação de seu site, há várias tarefas de pós-recuperação a considerar antes da conclusão da recuperação de site. Use as seções a seguir para ajudá-lo a concluir o processo de recuperação de site.

### <a name="re-enter-user-account-passwords"></a>Digite novamente as senhas de conta de usuário
Recuperado o servidor do site, as senhas das contas de usuário especificadas para o site devem ser digitadas novamente porque elas são redefinidas durante a recuperação de site. As contas são listadas na página **Concluído** no Assistente de Instalação após a recuperação de site estiver concluída e salva em C:\ConfigMgrPostRecoveryActions.html no servidor do site recuperado.

#### <a name="to-re-enter-user-account-passwords-after-site-recovery"></a>Para digitar novamente as senhas de conta de usuário após a recuperação de site

1.  Abra o console do Configuration Manager e conecte-se ao site recuperado.

2.  No console do Configuration Manager, clique em **Administração**.

3.  No espaço de trabalho **Administração** , expanda **Segurança**e clique em **Contas**.

4.  Para cada conta em que você digitar novamente a senha, faça o seguinte:

    1.  Selecione a conta da lista de contas que foram identificadas após a recuperação de site. Você pode encontrar essa lista no C:\ConfigMgrPostRecoveryActions.html no servidor do site recuperado.

    2.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades** para abrir as propriedades da conta.

    3.  Na guia **Geral** , clique em **Definir**e digite novamente as senhas da conta.

    4.  Clique em **Verificar**, selecione a fonte de dados apropriada para a conta de usuário selecionada e clique em **Testar conexão** para verificar se a conta de usuário pode conectar-se à fonte de dados.

    5.  Clique em **OK** para salvar as alterações de senha e clique em **OK**.

### <a name="re-enter-sideloading-keys"></a>Digite novamente as chaves de sideload
Recuperado o servidor do site, é necessário digitar novamente as chaves de sideload do Windows especificadas para o site porque elas são redefinidas durante a recuperação de site. Ao digitar novamente as chaves de sideload, a contagem na coluna **Ativações usadas** para as chaves de sideload do Windows é redefinida no console do Configuration Manager. Por exemplo, digamos que antes da falha do site a contagem de **Total de ativações** estava definida como **100** e de **Ativações usadas** como **90** para o número de chaves usadas pelos dispositivos. Recuperado o site, a coluna **Total de ativações** continua a exibir **100**, mas a coluna **Ativações usadas** exibe incorretamente **0**. No entanto, quando 10 novos dispositivos usarem uma chave de sideload, não haverá mais chaves de sideload disponíveis e o dispositivo seguinte irá falhar ao usar uma chave de sideload.

### <a name="recreate-the-microsoft-intune-subscription"></a>Recriar a Assinatura do Microsoft Intune
 Se você recuperar um servidor do site do Configuration Manager depois que o computador do servidor do site for restaurado ao estado anterior, a assinatura do Microsoft Intune não será restaurada. É necessário reconectar a assinatura depois de recuperar o site.  Não crie uma nova solicitação de APN. Em vez disso, carregue o arquivo .pem atual válido carregado na última vez em que o gerenciamento do iOS foi configurado ou renovado. Para obter mais informações, consulte [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription).

### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Configurar o SSL para funções do sistema de site que usam IIS
Ao recuperar sistemas de site que executam o IIS e que foram configurados para HTTPS antes da falha, você precisa reconfigurar o IIS para usar o certificado do servidor Web.

### <a name="reinstall-hotfixes-in-the-recovered-site-server"></a>Reinstalar os hotfixes no servidor do Site recuperado
Feita a recuperação de site, você deverá reinstalar os hotfixes que foram aplicados ao servidor do site. Exibir a lista de hotfixes instalados anteriormente na página **Concluído** do Assistente de Instalação após a recuperação de site. Essa lista também é salva em **C:\ConfigMgrPostRecoveryActions.html** no servidor do site recuperado.

### <a name="recover-custom-reports-on-the-computer-running-reporting-services"></a>Recuperar relatórios personalizados no computador que está executando o Reporting Services
Quando você cria relatórios do Reporting Services personalizados e o Reporting Services falha, você pode recuperar os relatórios feito o backup do servidor de relatório. Para obter mais informações sobre como restaurar relatórios personalizados no Reporting Services, consulte [Operações de backup e restauração para a Instalação do Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=228724) nos Manuais Online do SQL Server 2008.

### <a name="recover-content-files"></a>Recuperar arquivos de conteúdo
 O banco de dados do site contém informações sobre onde os arquivos de conteúdo são armazenados no servidor do site, mas os arquivos de conteúdo não passam por backup ou restauração como parte do processo de backup ou recuperação. Para recuperar completamente os arquivos de conteúdo, você deve restaurar a biblioteca de conteúdo e os arquivos de origem do pacote no local original. Há vários métodos de recuperar seus arquivos de conteúdo, mas o mais fácil é restaurá-los por meio do backup do sistema de arquivos do servidor do site.

 Se você não tem o backup do sistema de arquivos para os arquivos de origem do pacote, você deve copiar ou baixá-los manualmente da mesma forma quando o pacote foi criado pela primeira vez. É possível executar a seguinte consulta no SQL Server para encontrar o local de origem do pacote de todos os pacotes e aplicativos: `SELECT * FROM v_Package`. É possível identificar o site de origem do pacote observando os três primeiros caracteres da ID do pacote. Por exemplo, se a ID do pacote for CEN00001, o código do site de origem será CEN. Ao restaurar os arquivos de origem do pacote, eles devem ser restaurados no mesmo local em que estavam antes da falha.

 Se você não tem o backup do sistema de arquivos que contém a biblioteca de conteúdo, você possui as seguintes opções de restauração:

-   **Import a prestaged content file (Importar um arquivo de conteúdo pré-teste)**: quando você tem uma hierarquia do Configuration Manager, você pode criar um arquivo de conteúdo pré-teste com todos os pacotes e aplicativos de outro local e importar o arquivo de conteúdo pré-teste para recuperar a biblioteca de conteúdo no servidor do site.

-   **Atualizar conteúdo**: ao iniciar a ação de atualizar o conteúdo para um tipo de implantação de um pacote ou aplicativo, o conteúdo é copiado da origem do pacote para a biblioteca de conteúdo. Os arquivos de origem do pacote devem estar disponíveis no local original para essa ação ser concluída com êxito. Você deve executar essa ação em cada pacote e aplicativo.

### <a name="recover-custom-software-updates-on-the-computer-running-updates-publisher"></a>Recuperar atualizações de software personalizadas no computador que executa o Updates Publisher
Quando você tem arquivos do banco de dados do Update Publisher incluídos em seu plano de backup, você pode recuperar os bancos de dados em caso de falha no computador em que o Update Publisher é executado. Para obter mais informações sobre o Updates Publisher, consulte [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) na biblioteca do System Center TechCenter.

Use o procedimento a seguir para restaurar o banco de dados do Updates Publisher.

#### <a name="to-restore-the-updates-publisher-2011-database"></a>Para restaurar o banco de dados do Updates Publisher 2011
1.  Reinstale o Updates Publisher no computador recuperado.

2.  Copie o arquivo de banco de dados (Scupdb.sdf) de seu destino de backup para %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\ no computador que executa o Updates Publisher.

3.  Quando mais de um usuário executa o Updates Publisher no computador, você deve copiar cada arquivo de banco de dados para o local apropriado do perfil do usuário.

### <a name="user-state-migration-data"></a>Dados de migração de estado do usuário
Como parte das propriedades do sistema de site do ponto de migração de estado, você especifica as pastas que armazenam os dados de migração de estado do usuário. Depois de recuperar um servidor com uma pasta que armazena dados de migração de estado do usuário, você deve restaurar manualmente os dados de migração de estado do usuário no servidor para as mesmas pastas que armazenaram os dados antes da falha.

### <a name="regenerate-the-certificates-for-distribution-points"></a>Gerar novamente os certificados para pontos de distribuição
Depois de restaurar um site, o distmgr.log pode conter a seguinte entrada para um ou mais pontos de distribuição: **Falha ao descriptografar dados PFX do certificado**. Essa entrada indica que os dados do certificado do ponto de distribuição não podem ser descriptografados pelo site. Para resolver isso, você deve gerar novamente ou importar novamente o certificado para os pontos de distribuição afetados. Isso pode ser feito usando o cmdlet [Set-CMDistributionPoint](https://technet.microsoft.com/library/jj821872\(v=sc.20\).aspx) do PowerShell.

### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Atualizar certificados usados para pontos de distribuição baseados em nuvem
 O Configuration Manager requer um certificado de gerenciamento que ele utiliza para comunicação do servidor do site com o ponto de distribuição baseado em nuvem. Após recuperações de site, você deve atualizar os certificados para os pontos de distribuição baseados em nuvem.

## <a name="recover-a-secondary-site"></a>Recuperar um site secundário
 O Configuration Manager não dá suporte ao backup do banco de dados em um site secundário, mas dá suporte à recuperação reinstalando o site secundário. A recuperação de sites secundários é necessária quando um site secundário do Configuration Manager falha.

### <a name="requirements-for-reinstalling-a-secondary-site"></a>Requisitos para a reinstalação de um site secundário
-   O computador deve atender a todos os pré-requisitos do site secundário e ter os direitos de segurança apropriados configurados.
-   Você deve usar o mesmo caminho de instalação usado para o site que falhou.
-   Você deve usar um computador com a mesma configuração que o computador que falhou, como seu FQDN, para recuperar com êxito o site secundário.
-   O computador deve ter a mesma configuração do SQL Server que o site com falha.
  -   Durante a recuperação de sites secundários, o Configuration Manager não instalará o SQL Server Express se ele já não estiver instalado no computador.
  -   Você deve usar a mesma versão do SQL Server e a mesma instância do SQL Server usadas para o banco de dados do site secundário antes da falha.

### <a name="to-recover-a-secondary-site"></a>Para recuperar um site secundário:
Para recuperar sites secundários, use a ação **Recuperar Site Secundário** do nó **Sites** no console do Configuration Manager. Diferentemente da recuperação de um site de administração central ou site primário, a recuperação de sites secundários não usa um arquivo de backup, e em vez disso reinstala os arquivos do site secundário no computador do site secundário com falha. Depois que o site reinstalar, os dados do site secundário são reinicializados com os dados do site pai primário.

Durante o processo de recuperação, o Configuration Manager verifica se há uma biblioteca de conteúdo no computador do site secundário e se o conteúdo apropriado está disponível. O site secundário usará a biblioteca de conteúdo existente, se ela contiver o conteúdo apropriado. Caso contrário, para recuperar a biblioteca de conteúdo de um site secundário recuperado, será necessário redistribuir ou pré-configurar o conteúdo para o site recuperado.

Quando você possui um ponto de distribuição que não está no site secundário, não é necessário reinstalar o ponto de distribuição durante recuperações do site secundário. Após a recuperação de site secundário, o site sincroniza-se automaticamente com o ponto de distribuição.

Você pode verificar o status da recuperação de sites secundários usando a ação **Mostrar Status da Instalação** do nó **Sites** no console do Configuration Manager.
