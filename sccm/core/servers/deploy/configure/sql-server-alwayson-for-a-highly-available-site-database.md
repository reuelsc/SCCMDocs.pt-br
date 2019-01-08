---
title: AlwaysOn do SQL Server
titleSuffix: Configuration Manager
description: Planejamento de uso de um Grupo de Disponibilidade AlwaysOn do SQL Server com o Gerenciador de Configurações
ms.date: 08/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2d6dc236381606b72dcb3603e269161dcdd5d6b9
ms.sourcegitcommit: f2a1fa59fb3870a6bebca61daf15c0c157e9fdd6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54030998"
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Preparar para usar os grupos de disponibilidade AlwaysOn do SQL Server com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use este artigo na preparação do Gerenciador de Configurações para uso dos Grupos de Disponibilidade Always On do SQL Server. Este recurso fornece uma solução de alta disponibilidade e recuperação de desastre para o banco de dados do site.  

O Configuration Manager dá suporte ao uso de grupos de disponibilidade:
- No site de administração central e em sites primários.
- No local ou no Microsoft Azure.

Ao usar os grupos de disponibilidade no Microsoft Azure, você pode aumentar ainda mais a disponibilidade do seu banco de dados do site usando os *Conjuntos de Disponibilidade do Azure*. Para obter mais informações sobre os Conjuntos de Disponibilidade do Azure, consulte [Gerenciar a disponibilidade de máquinas virtuais](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).

> [!Important]
>  Antes de continuar, conheça a configuração do SQL Server e os grupos de disponibilidade do SQL Server. As informações a seguir fazem referência à biblioteca de documentação e aos procedimentos do SQL Server.



## <a name="supported-scenarios"></a>Cenários com suporte

Os cenários seguintes são compatíveis com o uso de grupos de disponibilidade com o Gerenciador de Configurações. Para saber mais e procedimentos para cada cenário em [Configurar Grupos de Disponibilidade para o Gerenciador de Configurações](/sccm/core/servers/deploy/configure/configure-aoag).

- [Criar um grupo de disponibilidade para uso com o Gerenciador de Configurações](/sccm/core/servers/deploy/configure/configure-aoag#create-and-configure-an-availability-group)  
- [Configurar um site para usar um grupo de disponibilidade](/sccm/core/servers/deploy/configure/configure-aoag#configure-a-site-to-use-the-database-in-the-availability-group)  
- [Adicionar ou remover membros de réplica síncrona de um grupo de disponibilidade que hospeda um banco de dados do site](/sccm/core/servers/deploy/configure/configure-aoag#add-and-remove-synchronous-replica-members)  
- [Configurar réplicas de confirmação assíncronas](/sccm/core/servers/deploy/configure/configure-aoag#configure-an-asynchronous-commit-repilca)  
- [Recuperar um site de uma réplica de confirmação assíncrona](/sccm/core/servers/deploy/configure/configure-aoag#use-the-asynchronous-replica-to-recover-your-site)  
- [Mover um banco de dados do site para fora de um grupo de disponibilidade para uma instância padrão ou nomeada de um SQL Server autônomo](/sccm/core/servers/deploy/configure/configure-aoag#stop-using-an-availability-group)  



## <a name="prerequisites"></a>Pré-requisitos

Os seguintes requisitos aplicam-se a todos os cenários. Se pré-requisitos adicionais se aplicarem a um cenário específico, eles serão detalhados com esse cenário.   

### <a name="configuration-manager-accounts-and-permissions"></a>Contas e permissões do Configuration Manager

#### <a name="site-server-to-replica-member-access"></a>Servidor do site para acesso de membro de réplica   
A conta de computador do servidor do site deve ser membro do grupo **Administradores Locais** em cada computador que for membro do grupo de disponibilidade.


### <a name="sql-server"></a>SQL Server

#### <a name="version"></a>Version  
Cada réplica no grupo de disponibilidade deve executar uma versão do SQL Server compatível com sua versão do Gerenciador de Configurações. Quando há suporte no SQL Server, nós diferentes de um grupo de disponibilidade poderão executar versões diferentes do SQL Server. Para saber mais, veja [Versões do SQL Server compatíveis com o Gerenciador de Configurações](/sccm/core/plan-design/configs/support-for-sql-server-versions) <!--SCCMDocs issue 656-->

#### <a name="edition"></a>Edição  
Use uma edição *Enterprise* do SQL Server.

#### <a name="account"></a>Conta  
Cada instância do SQL Server pode ser executada sob uma conta de usuário de domínio (**conta de serviço**) ou uma conta fora do domínio. Cada réplica em um grupo pode ter uma configuração diferente. 

- Use uma conta com o mínimo possível de permissões. Para saber mais, veja [Considerações de segurança para uma instalação do SQL Server](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation).  

- Para saber mais sobre como configurar contas de serviço e permissões para o SQL Server em [Configurar contas de serviço e permissões do Windows](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions).  

- Para usar uma conta fora do domínio, você deverá usar certificados. Para saber mais, veja [Usar certificados para um ponto de extremidade de espelhamento de banco de dados (Transact-SQL)](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).  

- Para saber mais, veja [Criar um ponto de extremidade de espelhamento de banco de dados para grupos de disponibilidade AlwaysOn](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).  


### <a name="availability-group-configurations"></a>Configurações de grupo de disponibilidade

#### <a name="replica-members"></a>Membros de réplica  
- O grupo de disponibilidade deve ter uma réplica primária.  

- Use a mesma quantidade e tipo de réplicas em um grupo de disponibilidade compatível com a sua versão do SQL Server.

- Você pode usar a réplica de confirmação assíncrona para recuperar sua réplica síncrona. Para saber mais, veja [Opções de recuperação do banco de dados do site](/sccm/core/servers/manage/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption).  

    > [!Warning]  
    > O Gerenciador de Configurações não é compatível com *failover* para uso da réplica de confirmação assíncrona como banco de dados do site. Para saber mais, veja [Failover e modos de failover (Grupos de Disponibilidade AlwaysOn)](https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups?view=sql-server-2014).  

O Gerenciador de Configurações não valida o estado da réplica de confirmação assíncrona para confirmar se é atual. O uso de uma réplica de confirmação assíncrona como banco de dados do site pode por em risco a integridade do seu site e dos dados. Por design, essa réplica pode não estar sincronizada. Para saber mais, veja [Visão geral dos Grupos de Disponibilidade AlwaysOn do SQL Server](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server).

Cada membro de réplica deve ter a seguinte configuração:

- Usar a *instância padrão* ou uma *instância nomeada*  

- A configuração **Conexões na Função Primária** é **Permitir todas as conexões**  

- A configuração **Secundária Legível** deve ser **Sim**  

- Habilitada para **Failover Manual**     

  > [!TIP]
  >  O Configuration Manager dá suporte ao uso de réplicas síncronas do grupo de disponibilidade quando definidas para **Failover Automático**. Defina o **Failover Manual** ao:
  >  -  Executar a Instalação do Gerenciador de Configurações para especificar o uso do banco de dados do site no grupo de disponibilidade.  
  >  -  Instalar qualquer atualização no Gerenciador de Configurações. (Não apenas as atualizações que se aplicam ao banco de dados do site).  

#### <a name="replica-member-location"></a>Local do membro de réplica
Hospede todas as réplicas em um grupo de disponibilidade local ou hospede todos no Microsoft Azure. Não há compatibilidade para um grupo que inclua um membro local e um membro no Azure.     

A Instalação do Gerenciador de Configurações precisa se conectar a cada réplica. Quando você configurar um grupo de disponibilidade no Azure e o grupo estiver atrás de um balanceador de carga interno ou externo, abra as portas padrão a seguir:   

- Mapeador de pontos de extremidade RPC: **TCP 135**   

- SQL Server Service Broker: **TCP 4022**  

- SQL por TCP: **TCP 1433**   


Após a conclusão da Instalação, as portas a seguir devem permanecer abertas para o Gerenciador de Configurações:  

- SQL Server Service Broker: **TCP 4022**  

- SQL por TCP: **TCP 1433**  

Você pode usar portas personalizadas para essas configurações. Use as mesmas portas personalizadas pelo ponto de extremidade e em todas as réplicas no grupo de disponibilidade.


#### <a name="listener"></a>Ouvinte   
O grupo de disponibilidade deve ter pelo menos um *ouvinte do grupo de disponibilidade*. O nome virtual desse ouvinte é usado durante a instalação do Gerenciador de Configurações para uso do banco de dados do site no grupo de disponibilidade. Embora um grupo de disponibilidade possa conter vários ouvintes, o Configuration Manager pode usar apenas um. Para saber mais, veja [Criar ou configurar um ouvinte do Grupo de Disponibilidade do SQL Server](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server).

#### <a name="file-paths"></a>Caminhos de arquivo   
Quando você executa a Instalação do Gerenciador de Configurações para configurar um site para usar o banco de dados em um grupo de disponibilidade, cada servidor de réplica secundária deve ter um caminho de arquivo de SQL Server idêntico ao caminho do arquivo para os arquivos de banco de dados do site na réplica primária atual. Se não existir um caminho idêntico, a instalação não adicionará a instância para o grupo de disponibilidade como novo local do banco de dados do site.  

A conta de serviço local do SQL Server deve ter permissão de **Controle Total** para essa pasta.

Os servidores de réplica secundária exigem esse caminho de arquivo apenas enquanto você estiver usando a Instalação do Gerenciador de Configurações para especificar a instância do banco de dados no grupo de disponibilidade. Depois de concluída a configuração do banco de dados do site no grupo de disponibilidade, você poderá excluir o caminho não usado dos servidores de réplica secundária.

Por exemplo, considere o seguinte cenário:

- Você cria um grupo de disponibilidade que usa três SQL Servers.  

- Seu servidor de réplica primária é uma nova instalação do SQL Server 2014. Por padrão, ele armazena os arquivos de banco de dados .MDF e .LDF em `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`.  

- Você atualizou seus dois servidores de réplica secundária para o SQL Server 2014 de versões anteriores. Com a atualização, esses servidores mantêm o caminho do arquivo original para armazenar arquivos de banco de dados: `C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA`.  

- Antes de mover o banco de dados do site para esse grupo de disponibilidade, crie o seguinte caminho de arquivo em cada servidor de réplica secundária: `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`. Esse caminho é uma duplicata do caminho em uso na réplica primária, mesmo que as réplicas secundárias não usem o local deste arquivo.  

- Depois, conceda à conta de serviço do SQL Server em cada réplica secundária acesso de controle total para o local do arquivo criado recentemente no servidor.  

- Agora, você pode executar com êxito a Instalação do Configuration Manager para configurar o site a usar o banco de dados no grupo de disponibilidade.  

#### <a name="configure-the-database-on-a-new-replica"></a>Configurar o banco de dados em uma nova réplica   
 Configure o banco de dados de cada réplica com as seguintes configurações:  

- Habilite a **Integração CLR**. Para saber mais, veja [Integração CLR](https://docs.microsoft.com/sql/relational-databases/clr-integration/clr-integration-enabling).  

- Defina o **Tamanho máximo de repl de texto** como `2147483647`  

- Defina o proprietário do banco de dados como *Conta SA*  

- **ATIVE** a configuração do **TRUSTWORTY**. Para saber mais, veja [propriedade do banco de dados TRUSTWORTHY](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property).   

- Habilite o **Service Broker**  

Faça essas configurações apenas em uma réplica primária. Para configurar uma réplica secundária, primeiro faça failover do primário para o secundário. Essa ação faz da secundária a nova réplica primária.   


### <a name="verification-script"></a>Script de verificação

Execute o script de SQL a seguir para verificar as configurações de banco de dados para réplicas primárias e secundárias. Antes de corrigir um problema em uma réplica secundária, altere essa réplica secundária para ser a réplica primária.

```SQL
    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targetting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targeted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:
```



## <a name="limitations-and-known-issues"></a>Limitações e problemas conhecidos

As seguintes limitações aplicam-se a todos os cenários.   

#### <a name="unsupported-sql-server-options-and-configurations"></a>Configurações e opções não compatíveis do SQL Server

- **Grupos de disponibilidade básicos**: Introduzidos com a edição Standard do SQL Server 2016, os grupos de disponibilidade básicos não dão suporte ao acesso de leitura a réplicas secundárias. A configuração exige esse acesso. Para saber mais, veja [Grupos de disponibilidade básicos de SQL Server](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups?view=sql-server-2017).  

- **Instância de cluster de failover**: As instâncias de cluster de failover não dão suporte a uma réplica usada com o Configuration Manager. Para saber mais, veja [Instâncias de cluster de failover AlwaysOn do SQL Server](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server).  

- **MultiSubnetFailover**: O uso de um grupo de disponibilidade não é compatível com o Configuration Manager em uma configuração de várias sub-redes. Também não é possível usar a cadeia de conexão da palavra-chave do [MutliSubnetFailover](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover).  

#### <a name="sql-servers-that-host-additional-availability-groups"></a>Servidores SQL que hospedam grupos de disponibilidade adicionais
<!--SCCMDocs issue 649--> Quando o SQL Server hospeda um ou mais grupos de disponibilidade além do grupo que você usa para o Gerenciador de Configurações, ele precisa de configurações específicas no momento em que você executar a instalação do Gerenciador de Configurações. Essas configurações também são necessárias para instalar uma atualização no Gerenciador de Configurações. Cada réplica em cada grupo de disponibilidade deve ter as seguintes configurações:

- Failover Manual  
- Permitir qualquer conexão somente leitura  

#### <a name="unsupported-database-use"></a>Uso de banco de dados sem suporte

- **O Configuration Manager dá suporte apenas ao banco de dados do site em um grupo de disponibilidade:** Os seguintes bancos de dados não tem suporte do Configuration Manager em um grupo de disponibilidade Always On do SQL Server:  
    - Banco de dados de relatórios  
    - Banco de dados do WSUS  

- **Banco de dados preexistente:** Não é possível usar o novo banco de dados criado na réplica. Restaure uma cópia de um banco de dados existente do Gerenciador de Configurações para a réplica primária ao configurar um grupo de disponibilidade.  

#### <a name="setup-errors-in-configmgrsetuplog"></a>Erros de instalação em ConfigMgrSetup.log  
Ao executar a Instalação do Gerenciador de Configurações para mover um banco de dados do site para um grupo de disponibilidade, ela tenta processar as funções de banco de dados nas réplicas secundárias do grupo de disponibilidade. O arquivo **ConfigMgrSetup.log** apresenta o seguinte erro:  

`ERROR: SQL Server error: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Failed to update database "CM_AAA" because the database is read-only. Configuration Manager Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)`  

Esses erros podem ser ignorados.

#### <a name="site-expansion"></a>Expansão do site
<!--SCCMDocs issue 568--> Se você configurar o banco de dados do site para que um site primário autônomo use o SQL AlwaysOn, você não poderá expandir o site para incluir um site de administração central. Se você tentar esse processo, não dará certo. Para expandir o site, remova temporariamente o banco de dados do site primário do grupo de disponibilidade.



## <a name="changes-for-site-backup"></a>Alterações para o backup do site

### <a name="backup-database-files"></a>Fazer backup dos arquivos de banco de dados
  
Quando um banco de dados do site usar um grupo de disponibilidade, execute a tarefa de manutenção interna do **servidor do Site de Backup** para fazer backup de configurações e arquivos comuns do Gerenciador de Configurações. Não use os arquivos .MDF ou .LDF criados por esse backup. Em vez disso, faça backups diretos desses arquivos de banco de dados usando o SQL Server.


### <a name="transaction-log"></a>Log de transações  

Defina o modelo de recuperação do banco de dados de site como **Completo**. Essa configuração é um requisito para o uso do Gerenciador de Configurações em um grupo de disponibilidade. Planeje monitorar e manter o tamanho do log de transações de banco de dados do site. No modelo de recuperação completo, as transações só são protegidas após ser feito um backup completo do banco de dados ou do log de transações. Para saber mais, veja [Fazer backup e restaurar bancos de dados do SQL Server](https://docs.microsoft.com/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases).



## <a name="changes-for-site-recovery"></a>Alterações para a recuperação de site

Se pelo menos um nó do grupo de disponibilidade permanecer funcional, use a opção de recuperação de site para **Ignorar a recuperação de banco de dados (Use esta opção se o banco de dados do site não tiver sido afetado)**.

Quando todos os nós de um grupo de disponibilidade tiverem sido perdidos, será preciso recriar o grupo de disponibilidade antes de recuperar o site. O Gerenciador de Configurações não pode recriar nem restaurar o nó de disponibilidade. Recrie o grupo, restaure o backup e reconfigure o SQL. Em seguida, use a opção de recuperação de site para **Ignorar a recuperação do banco de dados (use esta opção se o banco de dados do site não tiver sido afetado)**.

Para obter mais informações, veja [Backup e recuperação](/sccm/core/servers/manage/backup-and-recovery).



## <a name="changes-for-reporting"></a>Alterações para relatórios

### <a name="install-the-reporting-service-point"></a>Instalar o ponto do Reporting Services

O ponto do Reporting Services não é compatível com o uso do nome virtual do ouvinte do grupo de disponibilidade. Ele também não é compatível com a hospedagem do próprio banco de dados em um Grupo de Disponibilidade Always On do SQL Server.  

- Por padrão, a instalação do ponto do Reporting Services define o **Nome do servidor de banco de dados do site** como o nome virtual especificado como ouvinte. Altere essa configuração para especificar um nome do computador e a instância de uma réplica no grupo de disponibilidade.  

- Para descarregar relatórios e aumentar a disponibilidade quando um nó de réplica estiver offline, considere a instalação de pontos adicionais do Reporting Services em cada nó de réplica. Em seguida, configure cada ponto do Reporting Services para usar o próprio nome do computador. Quando você instala um ponto do Reporting Services em cada réplica do grupo de disponibilidade, os relatórios sempre podem se conectar a um servidor ativo do ponto de relatório.  


### <a name="switch-the-reporting-services-point-used-by-the-console"></a>Alternar o ponto do Reporting Services usado pelo console

1. No console do Configuration Manager, acesse o workspace **Monitoramento**.  

2. Expanda **Reporting** e selecione **Relatórios**.  

3. Clique em **Opções de Relatório**.  

4. Na caixa de diálogo Opções de Relatório, selecione o ponto do Reporting Services desejado.  



## <a name="next-steps"></a>Próximas etapas

Este artigo descreveu os pré-requisitos, as limitações e as alterações em tarefas comuns que o Gerenciador de Configurações exige ao usar grupos de disponibilidade. Consulte os procedimentos de instalação e configuração do site para uso dos grupos de disponibilidade em [Configurar grupos de disponibilidade](/sccm/core/servers/deploy/configure/configure-aoag).
