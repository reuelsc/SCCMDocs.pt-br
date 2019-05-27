---
title: Recuperação de site
titleSuffix: Configuration Manager
description: Aprenda a recuperar seus sites no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8506996f7b769003c937de69a9c7f659341c4294
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65501023"
---
#  <a name="recover-a-configuration-manager-site"></a>Recuperar um site do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Execute uma recuperação de site do Configuration Manager depois que um site falhar ou ocorrer perda de dados no banco de dados do site. Reparação e nova sincronização de dados são as tarefas principais de uma recuperação de site para evitar a interrupção das operações.

As seções neste tópico podem ajudá-lo a recuperar um site do Configuration Manager. Para criar um backup, veja [Backup para o Configuration Manager](/sccm/core/servers/manage/backup-and-recovery).



## <a name="considerations-before-recovering-a-site"></a>Considerações antes de recuperar um site

> [!Important]  
> Essas informações aplicam-se somente a cenários de recuperação de site. Quando você estiver atualizando sua infraestrutura local e não estiver recuperando ativamente um site com falha, examine as informações nos artigos a seguir:
> - [Atualizar infraestrutura local](/sccm/core/servers/manage/upgrade-on-premises-infrastructure)
> - [Modificar sua infra-estrutura](/sccm/core/servers/manage/modify-your-infrastructure)


#### <a name="use-the-same-version-and-edition-of-sql-server"></a>Use a mesma versão e edição do SQL Server   
Por exemplo, não há suporte para restaurar um banco de dados do SQL Server 2014 para SQL Server 2016. Da mesma forma, não há suporte para restaurar de um banco de dados de site do SQL Server 2016 da edição Standard para a edição Enterprise.
- O SQL Server não pode ser definido como **modo de usuário único**.
- Verifique se os arquivos MDF e LDF são válidos. Quando você recupera um site, não há verificação do estado dos arquivos.  

#### <a name="sql-server-always-on-availability-groups"></a>Grupos de disponibilidade Always On do SQL Server   
Se você usar grupos de disponibilidade Always On do SQL Server para hospedar o banco de dados do site, modifique seus planos de recuperação conforme descrito em [Preparar-se para usar o Always On do SQL Server](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-recovery).

#### <a name="database-replicas"></a>Réplicas de banco de dados  
Depois de restaurar um banco de dados do site que você configurou para réplicas de banco de dados, reconfigure cada réplica. Antes de usar as réplicas de banco de dados, recrie publicações e assinaturas.



## <a name="determine-your-recovery-options"></a>Determinar as opções de recuperação

Há duas áreas principais a considerar para a recuperação de site do servidor do site primário e do site de administração central do Configuration Manager: o **servidor do site** e o **banco de dados do site**.
As seções a seguir podem ajudá-lo a selecionar as melhores opções para seu cenário de recuperação.

> [!NOTE]   
> Quando a instalação do Configuration Manager detecta um site existente no servidor, é possível iniciar uma recuperação de site, mas as opções de recuperação para o servidor do site são limitadas. Por exemplo, se você executar a instalação em um servidor de site existente, quando escolher a recuperação poderá recuperar o servidor de banco de dados do site, mas a opção de recuperação do servidor do site estará desativada.


### <a name="site-server-recovery-options"></a>Opções de recuperação do servidor do site

Inicie a instalação do Configuration Manager de uma cópia da pasta **CD.Latest** criada fora da pasta de instalação do Configuration Manager.  

-   Se você executar a instalação do menu **Iniciar** no servidor do site, a opção **Recuperar um site** não estará disponível.  

-   Se você tiver instalado todas as atualizações de dentro do console do Configuration Manager antes de fazer o backup, não poderá reinstalar o site usando a instalação dos seguintes locais: 
    - Mídia de instalação
    - O caminho de instalação do Configuration Manager 

Em seguida, selecione a opção **Recuperar um site**. Você tem as seguintes opções de recuperação para o servidor do site que falhou:  

#### <a name="recover-the-site-server-using-an-existing-backup"></a>Recuperar o servidor do site usando um backup existente
Use essa opção quando você tiver um backup do Configuration Manager do servidor do site anterior à falha do site. O site cria esse backup como parte da tarefa de manutenção **Servidor do Site de Backup**. O site é reinstalado e as definições do site são configuradas com base no site do backup.  

#### <a name="reinstall-the-site-server"></a>Reinstalar o servidor do site
Use essa opção quando não houver backup do servidor do site. O servidor do site é reinstalado e você deve especificar as configurações do site como faria durante uma instalação inicial.  

-   Você deve usar o mesmo código do site e nome do banco de dados do site que você usou quando o site com falha foi instalado inicialmente.  

-   Você pode reinstalar o site em um novo computador que execute uma nova versão do sistema operacional.  

-   O servidor deve usar o mesmo nome do host e FQDN (nome de domínio totalmente qualificado) que o servidor do site original.   


### <a name="site-database-recovery-options"></a>Opções de recuperação do banco de dados do site

Quando você executa a instalação do Configuration Manager, tem as seguintes opções de recuperação para o banco de dados do site:  

#### <a name="recover-the-site-database-using-a-backup-set"></a>Recuperar o banco de dados do site usando um conjunto de backup
Use essa opção quando você tiver um backup do Configuration Manager do banco de dados do site de antes da falha do banco de dados. O site cria esse backup como parte da tarefa de manutenção **Servidor do Site de Backup**. Em uma hierarquia, quando você restaurar um site primário, o processo de recuperação recuperará do site de administração central todas as alterações feitas no banco de dados do site após o último backup. Ao restaurar o site de administração central, o processo de recuperação recupera essas alterações de um site primário de referência. Ao recuperar o banco de dados do site para um site primário autônomo, você perde as alterações do site após o último backup.  

Ao recuperar o banco de dados do site para um site em uma hierarquia, o comportamento de recuperação é diferente para um site de administração central e um site primário. O comportamento também é diferente quando o último backup está dentro ou fora do período de retenção do controle de alterações do SQL Server. Para obter mais informações, veja a seção [Cenários de recuperação de banco de dados do site](#site-database-recovery-scenarios) neste artigo.  

> [!NOTE]   
> Se você selecionar restaurar o banco de dados do site usando um conjunto de backup, mas o banco de dados do site já existir, a recuperação falhará.   

#### <a name="create-a-new-database-for-this-site"></a>Criar um novo banco de dados para este site
Use essa opção quando não houver backup do banco de dados do site. Em uma hierarquia, o processo de recuperação cria um novo banco de dados do site. Ao restaurar um site primário filho, ele recupera os dados por meio da replicação do site de administração central. Ao restaurar o site de administração central, ele replica os dados de um site primário de referência. Essa opção não está disponível quando você está recuperando um site primário autônomo ou um site de administração central que não tem sites primários.  

#### <a name="use-a-site-database-that-has-been-manually-recovered"></a>Use um banco de dados do site recuperado manualmente
Use essa opção quando você já tiver recuperado o banco de dados do site do Configuration Manager, mas precisar concluir o processo de recuperação.  

- O Configuration Manager pode recuperar o banco de dados do site de qualquer um dos seguintes processos:  

  - A tarefa de manutenção de backup do Configuration Manager  
  - Um backup de banco de dados do site usando o DPM (Data Protection Manager)  
  - Outro processo de backup   

    Depois de restaurar o banco de dados do site usando um método fora do Configuration Manager, execute a Instalação e selecione essa opção para concluir a recuperação do banco de dados do site.  

    > [!NOTE]   
    > Quando o DPM for usado para fazer backup do banco de dados do site, use os procedimentos do DPM para restaurar o banco de dados do site para um local especificado antes de continuar o processo de restauração no Configuration Manager. Para obter mais informações sobre o DPM, veja a biblioteca de documentação do [Data Protection Manager](https://docs.microsoft.com/system-center/dpm).    

- Em uma hierarquia, quando você recuperar um banco de dados do site primário, o processo de recuperação recuperará do site de administração central todas as alterações feitas no banco de dados do site após o último backup. Ao restaurar o site de administração central, o processo de recuperação recupera essas alterações de um site primário de referência. Ao recuperar o banco de dados do site para um site primário autônomo, você perde as alterações do site após o último backup.   

#### <a name="skip-database-recovery"></a>Ignorar a recuperação do banco de dados
Use essa opção quando não ocorrer perda de dados no servidor de banco de dados do site do Configuration Manager. Essa opção é válida somente quando o banco de dados do site está em um computador diferente do servidor do site que você está recuperando.  


### <a name="sql-server-change-tracking-retention-period"></a>Período de retenção do controle de alterações do SQL Server

O Configuration Manager habilita o controle de alterações para o banco de dados do site no SQL Server. O controle de alterações permite que o Configuration Manager consulte informações sobre as alterações feitas às tabelas do banco de dados após período anterior. O período de retenção especifica por quanto tempo as informações do controle de alterações são mantidas. Por padrão, o banco de dados do site é configurado para ter um período de retenção de cinco dias. Ao recuperar um banco de dados do site, o processo de recuperação procede de maneira diferente quando o backup está dentro ou está fora do período de retenção. Por exemplo, se o SQL Server falhar e seu último backup for de sete dias, ele estará fora do período de retenção.

Para obter mais informações sobre elementos internos de controle de alterações do SQL Server, confira a seguinte postagem no blog da equipe do SQL Server: [Change Tracking Cleanup – part 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1/) (Limpeza de Controle de Alterações – parte 1) e [Change Tracking Cleanup – part 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2) (Limpeza de Controle de Alterações – parte 2).


### <a name="reinitialization-of-site-or-global-data"></a>Reinicialização de site ou dados globais

O processo para reinicializar o site ou dados globais substitui dados existentes no banco de dados do site por dados de outro banco de dados do site. Por exemplo, quando o site ABC reinicializa os dados do site XYZ, ocorrem as seguintes etapas:
- Os dados são copiados do site XYZ para o site ABC.
- Os dados existentes do site XYZ são removidos do banco de dados do site ABC.
- Os dados copiados do site XYZ são inseridos no banco de dados do site ABC.

#### <a name="example-scenario-1-the-primary-site-reinitializes-the-global-data-from-the-central-administration-site"></a>Cenário de exemplo 1: o site primário reinicializa os dados globais do site de administração central  
O processo de recuperação remove os dados globais existentes do site primário no banco de dados do site primário e substitui os dados pelos dados globais copiados do site de administração central.

#### <a name="example-scenario-2-the-central-administration-site-reinitializes-the-site-data-from-a-primary-site"></a>Cenário de exemplo 2: O site de administração central reinicializa os dados do site de um site primário 
O processo de recuperação remove os dados existentes do site primário do banco de dados do site de administração central. Ele substitui os dados pelos dados copiados do site primário. Os dados do site de outros sites primários não são afetados.


### <a name="site-database-recovery-scenarios"></a>Cenários de recuperação de banco de dados do site

Depois que um banco de dados do site é restaurado de um backup, o Configuration Manager tenta restaurar as alterações no site e nos dados globais após o último backup do banco de dados. Configuration Manager inicia as ações a seguir depois que um banco de dados do site é restaurado do backup:  

#### <a name="recovered-site-is-a-central-administration-site"></a>O site recuperado é um site administração central
- Backup de banco de dados dentro do período de retenção do controle de alterações  

     - **Dados globais**: as alterações nos dados globais após o backup são replicadas de todos os sites primários.  

     - **Dados do site**: as alterações nos dados do site após o backup são replicadas de todos os sites primários.  

- Backup de banco de dados mais antigo que o período de retenção do controle de alterações  

     - **Dados globais**: o site de administração central reinicializa os dados globais do site primário de referência, quando especificados. Em seguida, todos os outros sites primários reinicializam os dados globais do site de administração central. Se você não especificar um site de referência, todos os sites primários reinicializarão os dados globais do site de administração central. Esses dados são o que você restaurou do backup.  

     - **Dados do site**: o site de administração central reinicializa os dados do site por meio de cada site primário.  

#### <a name="recovered-site-is-a-primary-site"></a>O site recuperado é um site primário
- Backup de banco de dados dentro do período de retenção do controle de alterações  

     - **Dados globais**: as alterações dos dados globais após o backup são replicadas no site de administração central.  

     - **Dados do site**: o site de administração central reinicializa os dados do site por meio do site primário. As alterações após o backup são perdidas. Os clientes regeneram a maioria dos dados quando enviam informações para o site primário.  

- Backup de banco de dados mais antigo que o período de retenção do controle de alterações  
     - **Dados globais**: o site primário reinicializa os dados globais do site de administração central.  

     - **Dados do site**: o site de administração central reinicializa os dados do site por meio do site primário. As alterações após o backup são perdidas. Os clientes regeneram a maioria dos dados quando enviam informações para o site primário.  



## <a name="site-recovery-procedures"></a>Procedimentos de recuperação do site

Use um dos procedimentos a seguir para ajudá-lo a recuperar o servidor do site e o banco de dados do site:


### <a name="start-a-site-recovery-in-the-setup-wizard"></a>Iniciar uma recuperação do site no assistente de instalação

1.  Copie a [pasta CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder) para um local fora da pasta de instalação do Configuration Manager. Por meio da cópia da pasta CD.Latest, execute o assistente de instalação do Configuration Manager.  

2.  Na página **Guia de Introdução** , selecione **Recuperar um site**e clique em **Avançar**.  

3.  Conclua o assistente usando as opções apropriadas para a recuperação de site.  

     - Durante a recuperação, a instalação identifica a porta do SQL SSB (Server Service Broker) usada pelo SQL Server. Não altere essa configuração de porta durante a recuperação, ou a replicação de dados não funcionará corretamente após o término da recuperação.  

     - Você pode especificar o caminho novo ou o original para usar na instalação do Configuration Manager no assistente de instalação.  


### <a name="start-an-unattended-site-recovery"></a>Iniciar uma recuperação autônoma do site

1. Prepare o script de instalação autônoma para as opções necessárias para a recuperação de site. Para obter mais informações, confira [Recuperação de site autônoma](/sccm/core/servers/manage/unattended-recovery).  

2. Execute a instalação do Configuration Manager usando a opção de linha de comando `/script`. Por exemplo, você cria um arquivo de inicialização da instalação **ConfigMgrUnattend.ini**. Você salva-o no diretório `C:\Temp` do computador no qual está executando a instalação. Use o seguinte comando:  

    `setup.exe /script C:\temp\ConfigMgrUnattend.ini`  


> [!NOTE]   
>  Depois de recuperar um site de administração central, a replicação de alguns dados de sites filho pode não ser estabelecida. Esses dados podem incluir inventário de hardware, inventário de software e mensagens de status.
>
>  Se isso ocorrer, reinicialize **ConfigMgrDRSSiteQueue** para a replicação de banco de dados. Use o **SQL Server Manager** para executar a seguinte consulta no banco de dados do site para o site de administração central:
>
> ``` SQL
> IF EXISTS (SELECT * FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)  
>  
> ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON
> ```



## <a name="post-recovery-tasks"></a>Tarefas de pós-recuperação

Depois da recuperação do site, há várias tarefas pós-recuperação a considerar antes da conclusão da recuperação de site. Use as seções a seguir para ajudá-lo a concluir o processo de recuperação de site.


### <a name="reenter-user-account-passwords"></a>Reinsira as senhas de conta de usuário

Após uma recuperação de servidor do site, digite novamente as senhas para todas as contas de usuário no site. Essas senhas são redefinidas durante a recuperação de site. As contas são listadas na página **Concluído** do assistente de instalação depois que a recuperação de site está concluída. A lista também é salva em `C:\ConfigMgrPostRecoveryActions.html` no servidor do site recuperado.

#### <a name="reenter-user-account-passwords-after-site-recovery"></a>Reinsira as senhas de conta de usuário após a recuperação de site
1. Abra o console do Configuration Manager e conecte-se ao site recuperado.  

2. No workspace **Administração**, expanda **Segurança** e clique em **Contas**.  

3. Para cada conta, execute as seguintes etapas para reinserir a senha:  

     1. Selecione a conta na lista identificada após a recuperação de site.  

     2. Na faixa de opções, clique em **Propriedades**.  

     3. Na guia **Geral**, clique em **Definir** e digite novamente a senha da conta.  

     4. Clique em **Verificar**, selecione a fonte de dados apropriada para a conta de usuário selecionada e, em seguida, clique em **Testar conexão**. Esta etapa testa se a conta de usuário pode se conectar à fonte de dados e verifica as credenciais.  

     5. Clique em **OK** para salvar as alterações de senha e, em seguida, clique em **OK** para fechar a página de propriedades de conta.  


### <a name="reenter-sideloading-keys"></a>Reinsira as chaves de sideload

Após uma recuperação de servidor do site, reinsira as chaves de sideload do Windows especificadas para o site. Essas chaves são redefinidas durante a recuperação de site. Ao reinserir as chaves de sideload, o site redefine a contagem na coluna **Ativações usadas** para as chaves de sideload do Windows. 

Por exemplo, antes da falha do site, a contagem de **Total de ativações** aparecia como **100**. O número de chaves que os dispositivos usara, ou as **Ativações usadas**, é de **90**. Depois da recuperação de site, a coluna **Total de ativações** ainda exibe **100**, mas a coluna **Ativações usadas** exibe incorretamente **0**. Depois de 10 novos dispositivos usarem uma chave de sideload, não haverá mais chaves de sideload e o 11º dispositivo falhará em aplicar uma chave de sideload.


### <a name="recreate-the-microsoft-intune-subscription"></a>Recriar a Assinatura do Microsoft Intune

Se você recuperar um servidor do site do Configuration Manager depois que de refazer a imagem do servidor do site, a assinatura do Microsoft Intune não será restaurada. Reconecte sua assinatura depois de recuperar o site. Não crie uma nova solicitação APN. Em vez disso, carregue o arquivo PEM atual válido. Use o mesmo arquivo que você carregou na última vez que configurou ou renovou o gerenciamento de iOS. Para obter mais informações, consulte [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription).


### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Configurar o SSL para funções do sistema de site que usam IIS

Ao recuperar sistemas de sistema de sites que executam o IIS configurados para HTTPS, reconfigure o IIS para usar o certificado do servidor Web.


### <a name="reinstall-hotfixes"></a>Reinstalar hotfixes 

Feita a recuperação de site, você deverá reinstalar os hotfixes que foram aplicados ao servidor do site. Depois da recuperação de site, exiba a lista de hotfixes instalados anteriormente na página **Concluído** do assistente de instalação. Essa lista também é salva em `C:\ConfigMgrPostRecoveryActions.html` no servidor do site recuperado.


### <a name="recover-custom-reports"></a>Recuperar relatórios personalizados 

Alguns clientes criam relatórios personalizados no SQL Server Reporting Services. Quando esse componente falha, recupere os relatórios de um backup do servidor de relatório. Para obter mais informações sobre como restaurar relatórios personalizados no Reporting Services, veja [Operações de backup e restauração do Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).


### <a name="recover-content-files"></a>Recuperar arquivos de conteúdo

O banco de dados do site rastreia o local em que o servidor do site armazena os arquivos de conteúdo. Não é feito backup nem restauração dos arquivos de conteúdo em si como parte do processo de backup e recuperação. Para recuperar completamente os arquivos de conteúdo, restaure a biblioteca de conteúdo e os arquivos de origem do pacote no local de origem. Há vários métodos para recuperar os arquivos de conteúdo. O método mais fácil é restaurar os arquivos de um backup de sistema de arquivos do servidor do site.

Se você não tiver um backup do sistema de arquivos para os arquivos de origem do pacote, copie-o ou baixe-o manualmente. Esse processo é semelhante a quando você criou o pacote originalmente. Execute a seguinte consulta no SQL Server para encontrar o local de origem do pacote de todos os pacotes e aplicativos: `SELECT * FROM v_Package`. Identifique o site de origem do pacote observando os três primeiros caracteres da ID do pacote. Por exemplo, se a ID do pacote for CEN00001, o código do site de origem será CEN. Ao restaurar os arquivos de origem do pacote, eles devem ser restaurados no mesmo local em que estavam antes da falha.

Se você não tiver o backup do sistema de arquivos que inclui a biblioteca de conteúdo, terá as seguintes opções de restauração:  

- **Importar um arquivo de conteúdo pré-teste**: em uma hierarquia do Configuration Manager, você pode criar um arquivo de conteúdo pré-teste com todos os pacotes e aplicativos de outra localização. Em seguida, importe o arquivo de conteúdo pré-teste para recuperar a biblioteca de conteúdo no servidor do site.  

- **Atualizar conteúdo**: o Configuration Manager copia o conteúdo da origem do pacote para a biblioteca de conteúdo. Para essa ação ser concluída com sucesso, os arquivos de origem do pacote devem estar disponíveis no local de origem. Execute essa ação em cada pacote e aplicativo.


### <a name="recover-custom-software-updates"></a>Recuperar atualizações de software personalizadas

Quando você tiver incluído arquivos de banco de dados do System Center Updates Publisher em seu plano de backup, poderá recuperar os bancos de dados se houver falha do computador do Updates Publisher. Para obter mais informações sobre o Updates Publisher, veja [System Center Updates Publisher](/sccm/sum/tools/updates-publisher).

#### <a name="restore-the-updates-publisher-database"></a>Restaurar o banco de dados do Updates Publisher
1. Reinstale o Updates Publisher no computador recuperado.  

2. Copie o arquivo de banco de dados **Scupdb.sdf** de seu destino de backup para `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` no computador que executa o Updates Publisher.  

3. Quando mais de um usuário executa o Updates Publisher no computador, copie cada arquivo de banco de dados para o local apropriado do perfil do usuário.  


### <a name="user-state-migration-data"></a>Dados de migração de estado do usuário

Como parte das propriedades de ponto de migração de estado, você deve especificar as pastas que armazenam dados de estado do usuário. Depois de recuperar um ponto de migração de estado, restaure manualmente os dados de estado do usuário no servidor. Restaure-os para as mesmas pastas que armazenavam os dados antes da falha.


### <a name="regenerate-the-certificates-for-distribution-points"></a>Gerar novamente os certificados para pontos de distribuição

Depois de restaurar um site, o **distmgr.log** pode listar a seguinte entrada para um ou mais pontos de distribuição: `Failed to decrypt cert PFX data`. Essa entrada indica que os dados do certificado do ponto de distribuição não podem ser descriptografados pelo site. Para resolver esse problema, você deve gerar ou importar novamente o certificado para os pontos de distribuição afetados. Use o cmdlet [Set-CMDistributionPoint](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmdistributionpoint) do PowerShell.


### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Atualizar certificados usados para pontos de distribuição baseados em nuvem

O Configuration Manager exige um certificado de gerenciamento do Azure para o servidor do site se comunicar com pontos de distribuição baseados em nuvem. Após a recuperação de site, atualize os certificados para os pontos de distribuição baseados em nuvem.



## <a name="recover-a-secondary-site"></a>Recuperar um site secundário

O Configuration Manager não é compatível com backup do banco de dados em um site secundário, mas é compatível com a recuperação reinstalando o site secundário. A recuperação de sites secundários é necessária quando um site secundário do Configuration Manager falha.


### <a name="requirements"></a>requisitos

- O servidor deve atender a todos os pré-requisitos do site secundário e ter os direitos de segurança apropriados configurados.  

- Use o mesmo caminho de instalação usado para o site que falhou.  

- Use um servidor com a mesma configuração do servidor que falhou. Essa configuração inclui seu FQDN (nome de domínio totalmente qualificado).  

- O servidor deve ter a mesma configuração do SQL Server que o site que falhou.  

     - Durante uma recuperação de site secundário, o Configuration Manager não instalará o SQL Server Express se ele já não estiver instalado no computador.  

     - Você deve usar a mesma versão do SQL Server e a mesma instância do SQL Server usadas para o banco de dados do site secundário antes da falha.  


### <a name="procedure"></a>Procedimento

Use a ação **Recuperar Site Secundário** do nó **Sites** no console do Configuration Manager. Ao contrário de outros tipos de sites, a recuperação de um site secundário não usa um arquivo de backup. Esse processo reinstalará os arquivos do site secundário no servidor que falhou. Depois que o site é reinstalado, os dados do site secundário são reinicializados usando o site primário pai.

Durante o processo de recuperação, o Configuration Manager verifica se a biblioteca de conteúdo existe no servidor do site secundário. Ele também verifica se o conteúdo apropriado está disponível. O site secundário usa a biblioteca de conteúdo existente, caso ela inclua o conteúdo apropriado. Caso contrário, para recuperar a biblioteca de conteúdo de um site secundário, redistribua ou pré-configure o conteúdo para o servidor.

Quando você tem um ponto de distribuição que não está no servidor do site secundário, não é necessário reinstalar o ponto de distribuição durante recuperações do site secundário. Após a recuperação de site secundário, o site sincroniza-se automaticamente com o ponto de distribuição.

Você pode verificar o status da recuperação de sites secundários usando a ação **Mostrar Status da Instalação** do nó **Sites** no console do Configuration Manager.
