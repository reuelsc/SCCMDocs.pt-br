---
title: AlwaysOn do SQL Server
titleSuffix: Configuration Manager
description: Planeje usar um grupo de disponibilidade AlwaysOn do SQL Server com SCCM.
ms.custom: na
ms.date: 12/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
caps.latest.revision: "16"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 7efd0c76a0723a98661b0861eb16298eee524f35
ms.sourcegitcommit: f1535281b2c3fecff773b722c3f7590bf6ba10a0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/03/2018
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Preparar para usar os grupos de disponibilidade AlwaysOn do SQL Server com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Prepare o System Center Configuration Manager para usar grupos de disponibilidade AlwaysOn do SQL Server como uma solução de alta disponibilidade e recuperação de desastre para o banco de dados do site.  
O Configuration Manager dá suporte ao uso de grupos de disponibilidade:
-     No site de administração central e em sites primários.
-     No local ou no Microsoft Azure.

Ao usar os grupos de disponibilidade no Microsoft Azure, você pode aumentar ainda mais a disponibilidade do seu banco de dados do site usando os *Conjuntos de Disponibilidade do Azure*. Para obter mais informações sobre os Conjuntos de Disponibilidade do Azure, consulte [Gerenciar a disponibilidade de máquinas virtuais](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).

>  [!Important]   
>  Antes de continuar, conheça a configuração do SQL Server e os grupos de disponibilidade do SQL Server. As informações a seguir fazem referência à biblioteca de documentação e aos procedimentos do SQL Server.

## <a name="supported-scenarios"></a>Cenários com suporte
Veja a seguir os cenários com suporte para usar grupos de disponibilidade com o Configuration Manager. Os detalhes e os procedimentos para cada um podem ser encontrados em [Configurar grupos de disponibilidade para o Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag).


-      [Criar um grupo de disponibilidade para uso com o Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag#create-and-configure-an-availability-group).
-     [Configurar um site para usar um grupo de disponibilidade](/sccm/core/servers/deploy/configure/configure-aoag#configure-a-site-to-use-the-database-in-the-availability-group).
-     [Adicionar ou remover membros de réplica síncrona de um grupo de disponibilidade que hospeda um banco de dados do site](/sccm/core/servers/deploy/configure/configure-aoag#add-and-remove-synchronous-replica-members).
-     [Configurar réplicas de confirmação assíncrona](/sccm/core/servers/deploy/configure/configure-aoag#configure-an-asynchronous-commit-repilca) (exige o Configuration Manager versão 1706 ou posterior.)
-     [Recuperar um site de uma réplica de confirmação assíncrona](/sccm/core/servers/deploy/configure/configure-aoag#use-the-asynchronous-replica-to-recover-your-site) (exige o Configuration Manager versão 1706 ou posterior.)
-     [Mova o banco de dados para fora do site de um grupo de disponibilidade para uma instância padrão ou nomeada de um SQL Server autônomo](/sccm/core/servers/deploy/configure/configure-aoag#stop-using-an-availability-group).


## <a name="prerequisites"></a>Pré-requisitos
Os seguintes requisitos aplicam-se a todos os cenários. Se os pré-requisitos adicionais se aplicarem a um cenário específico, eles serão detalhados com esse cenário.   

### <a name="configuration-manager-accounts-and-permissions"></a>Contas e permissões do Configuration Manager
**Servidor do site para acesso de membro de réplica:**   
A conta de computador do servidor do site deve ser um membro do grupo **Administradores Locais** em cada computador que seja um membro do grupo de disponibilidade.

### <a name="sql-server"></a>SQL Server
**Versão:**  
Cada réplica no grupo de disponibilidade deve executar uma versão do SQL Server compatível com a sua versão do Configuration Manager. Quando há suporte no SQL Server, nós diferentes de um grupo de disponibilidade poderão executar versões diferentes do SQL Server.

**Edição:**  
É necessário usar uma edição *Enterprise* do SQL Server.

**Conta**  
Cada instância do SQL Server pode ser executada sob uma conta de usuário de domínio (**conta de serviço**) ou uma conta fora do domínio. Cada réplica em um grupo pode ter uma configuração diferente. De acordo com as [práticas recomendadas do SQL Server](/sql/sql-server/install/security-considerations-for-a-sql-server-installation#before-installing-includessnoversionincludesssnoversion-mdmd), use uma conta com as menores permissões possíveis.

-   Para configurar contas de serviço e permissões para o SQL Server 2016, veja [Configurar contas de serviço e permissões do Windows](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions) no MSDN.
-   Para usar uma conta fora do domínio, você deverá usar certificados. Para saber mais, confira [Usar certificados para um ponto de extremidade de espelhamento de banco de dados (Transact-SQL)](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).


Para saber mais, veja [Criar um ponto de extremidade de espelhamento de banco de dados para grupos de disponibilidade AlwaysOn](/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).

### <a name="availability-group-configurations"></a>Configurações de grupo de disponibilidade
**Membros de réplica:**  
-   O grupo de disponibilidade deve ter uma réplica primária.
-   Antes da versão 1706, você podia ter até duas réplicas secundárias síncronas.
-   A partir da versão 1706, você pode usar o mesmo número e tipo de réplicas em um grupo de disponibilidade como compatível com a versão do SQL Server que você usa.

-   A partir da versão 1706, você pode usar a réplica de confirmação assíncrona para recuperar sua réplica síncrona. Confira [Opções de recuperação do banco de dados do site]( /sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) no tópico Backup e recuperação para obter informações sobre como fazer isso.
    > [!CAUTION]  
    > O Configuration Manager não dá suporte a [failover](https://go.microsoft.com/fwlink/?linkid=626885) para uso da réplica de confirmação assíncrona como o banco de dados do site.
Como o Configuration Manager não valida o estado da réplica de confirmação assíncrona para confirmar que é atual, e [por design essa réplica pode estar fora de sincronia]( https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes), o uso de uma réplica de confirmação assíncrona como o banco de dados do site pode colocar em risco a integridade do site e dos dados.

Cada membro de réplica deve:
-   Usar a **instância padrão**  
    *A partir da versão 1702, você pode usar uma* ***instância nomeada***.

-     Ter **Conexões na Função Primária** definida como **Sim**
-     Ter **Secundária Legível** definida como **Sim**  
-     Ser definida para **Failover Manual**      

    >  [!TIP]
    >  O Configuration Manager dá suporte ao uso de réplicas síncronas do grupo de disponibilidade quando definidas para **Failover Automático**. No entanto, o **Failover Manual** deve ser definido quando:
    >  -  Você executar a instalação para especificar o uso do banco de dados do site no grupo de disponibilidade.
    >  -  Quando você instala qualquer atualização para o Configuration Manager (não apenas as atualizações que se aplicam ao banco de dados do site).  

**Local do membro de réplica:**  
Todas as réplicas em um grupo de disponibilidade devem ser hospedadas no local ou hospedadas no Microsoft Azure. Não há suporte para um grupo que inclui um membro local e um membro no Azure.     

Quando você configurar um grupo de disponibilidade no Azure e o grupo estiver atrás de um balanceador de carga interno ou externo, a seguir estarão as portas padrão que você deverá abrir para habilitar o acesso de Instalação para cada réplica:   

-     Mapeador de pontos de extremidade RCP - **TCP 135**   
-     Protocolo SMB – **TCP 445**  
    *Você pode remover essa porta após a movimentação do banco de dados ser concluída. A partir da versão 1702, essa porta não é mais necessária.*
-     SQL Server Service Broker - **TCP 4022**
-     SQL sobre TCP – **TCP 1433**   

Após a Instalação ser concluída, as seguintes portas deverão permanecer acessíveis:
-     SQL Server Service Broker - **TCP 4022**
-     SQL sobre TCP – **TCP 1433**

A partir da versão 1702, você pode usar portas personalizadas para essas configurações. As mesmas portas devem ser usadas pelo ponto de extremidade e em todas as réplicas no grupo de disponibilidade.


**Ouvinte:**   
O grupo de disponibilidade deve ter pelo menos um **ouvinte do grupo de disponibilidade**. O nome virtual desse ouvinte é usado quando você configura o Configuration Manager para usar o banco de dados do site no grupo de disponibilidade. Embora um grupo de disponibilidade possa conter vários ouvintes, o Configuration Manager pode usar apenas um. Confira [Criar ou configurar um ouvinte do grupo de disponibilidade (SQL Server)](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server) para obter mais informações.

**Caminhos de arquivo:**   
Quando você executa a Instalação do Configuration Manager para configurar um site para usar o banco de dados em um grupo de disponibilidade, cada servidor de réplica secundária deve ter um caminho de arquivo de SQL Server idêntico ao caminho do arquivo para os arquivos de banco de dados do site conforme encontrados na réplica primária atual.
-   Se não existir um caminho idêntico, a Instalação não adicionará a instância para o grupo de disponibilidade como o novo local do banco de dados do site.
-   Além disso, a conta de serviço local do SQL Server deve ter permissão de **Controle Total** para essa pasta.

Os servidores de réplica secundária exigem esse caminho de arquivo apenas enquanto você estiver usando a Instalação para especificar a instância do banco de dados no grupo de disponibilidade. Depois que a Instalação concluir a configuração do banco de dados do site no grupo de disponibilidade, você poderá excluir o caminho não utilizado dos servidores de réplica secundária.

Por exemplo, considere o seguinte cenário:
-   Você cria um grupo de disponibilidade que usa três SQL Servers.

-   Seu servidor de réplica primária é uma nova instalação do SQL Server 2014. Por padrão, os arquivos .MDF e .LDF do banco de dados são armazenados em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA.

-   Ambos os servidores de réplica secundária foram atualizados para o SQL Server 2014 de versões anteriores e mantêm o caminho de arquivo original para armazenar arquivos de banco de dados: C:\Arquivos de Programas\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA.

-   Antes de tentar mover o banco de dados do site para esse grupo de disponibilidade, em cada servidor de réplica secundária você deve criar o seguinte caminho de arquivo, mesmo que as réplicas secundárias não vão usar esse local de arquivo: C:\Arquivos de Programas\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA (esta é uma duplicata do caminho que está em uso na réplica primária).

-   Depois, conceda à conta de serviço do SQL Server em cada réplica secundária acesso de controle total para o local do arquivo criado recentemente no servidor.

-   Agora, você pode executar com êxito a Instalação do Configuration Manager para configurar o site a usar o banco de dados no grupo de disponibilidade.

**Configurar o banco de dados em uma nova réplica:**   
 O banco de dados de cada réplica deve ser definido com o seguinte:
-   **Integração CLR** deve estar *habilitada*
-     **Tamanho máximo de repl de texto** deve ser *2147483647*
-     O proprietário do banco de dados deve ser a *Conta SA*
-     **TRUSTWORTY** deve ser **ON**
-     **Service Broker** deve estar *habilitado*

Você pode fazer essas configurações em apenas uma réplica primária. Para configurar uma réplica secundária, você deverá primeiro fazer failover do primário para o secundário para transformar o secundário em nova réplica primária.   

Use a documentação do SQL Server, quando necessário, para ajudá-lo a definir as configurações. Por exemplo, veja [TRUSTWORTHY](/sql/relational-databases/security/trustworthy-database-property) ou [Integração CLR](/sql/relational-databases/clr-integration/clr-integration-enabling) na documentação do SQL Server.

### <a name="verification-script"></a>Script de verificação
Você pode executar o script a seguir para verificar as configurações de banco de dados para réplicas primárias e secundárias. Antes de corrigir um problema em uma réplica secundária, você deverá alterar essa réplica secundária para ser a réplica primária.

    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targetting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targetted database is ' + @dbname + N'.'

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

## <a name="limitations-and-known-issues"></a>Limitações e problemas conhecidos
As seguintes limitações aplicam-se a todos os cenários.   

**Opções e configurações do SQL Server que não têm suporte:**
- **Grupos de disponibilidade básicos**  
  A partir do SQL Server 2016 Standard, os [grupos de disponibilidade básicos](https://msdn.microsoft.com/library/mt614935.aspx) não dão suporte ao acesso de leitura de réplicas secundárias, um requisito para uso com o Configuration Manager.
- **Instância de cluster de failover**  
  As [instâncias de cluster de failover](/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server) não têm suporte para uma réplica usada com o Configuration Manager.

- **MultiSubnetFailover**    
    Não há suporte para usar um grupo de disponibilidade em uma configuração de várias sub-redes ou com a cadeia de conexão de palavra-chave [MutliSubnetFailover](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover).



**Servidores SQL que hospedam os grupos de disponibilidade adicional:**   
Antes da versão 1610 do Configuration Manager, quando um grupo de disponibilidade em um SQL Server hospedar um ou mais grupos de disponibilidade além do grupo que você usar para o Configuration Manager, cada réplica em cada um dos grupos de disponibilidade adicionais deverá ter as seguintes configurações definidas no momento em que você executar a instalação do Configuration Manager Setup ou instalar uma atualização para o Configuration Manager:
-   **Failover Manual**
-   **permitir qualquer conexão somente leitura**

**Uso de bancos de dados sem suporte:**
-   **O Configuration Manager dá suporte apenas ao banco de dados do site em um grupo de disponibilidade:** não há suporte para o seguinte:
    -   Banco de dados de relatórios
    -   Banco de dados do WSUS
-   **Banco de dados preexistente:** não é possível usar o novo banco de dados criado na réplica. Em vez disso, você deve restaurar uma cópia de um banco de dados existente do Configuration Manager para a réplica primária ao configurar um grupo de disponibilidade.

**Erros de instalação em ConfigMgrSetup.log:**  
Quando você executa a instalação para mover um banco de dados do site para um grupo de disponibilidade, a instalação tenta processar as funções de banco de dados nas réplicas secundárias do grupo de disponibilidade e os logs de erros, como o seguinte:
-   ERRO: Erro do SQL Server: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Falha ao atualizar o banco de dados "CM_AAA" porque ele é somente leitura. Instalação do Configuration Manager 1/21/2016 4:54:59 PM 7344 (0x1CB0)  

Esses erros podem ser ignorados.

## <a name="changes-for-site-backup"></a>Alterações para o backup do site
**Faça backup dos arquivos de banco de dados:**  
Quando um banco de dados do site é executado em um grupo de disponibilidade, você deve executar a tarefa de manutenção interna do servidor **Site de Backup** para fazer backup de configurações e arquivos comuns do Configuration Manager. No entanto, não use os arquivos .MDF ou .LDF criados por esse backup. Em vez disso, faça backups diretos desses arquivos de banco de dados usando o SQL Server.

**Log de transações:**  
O modelo de recuperação do banco de dados do site deve ser definido como **Completo** (um requisito para usar em um grupo de disponibilidade). Com essa configuração, planeje monitorar e manter o tamanho do log de transações de banco de dados de site. No modelo de recuperação completo, as transações não são protegidas até que um backup completo do banco de dados ou o log de transações seja feito. Confira [Fazer backup e restaurar bancos de dados do SQL Server](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases) na documentação do SQL Server para obter mais informações.

## <a name="changes-for-site-recovery"></a>Alterações para a recuperação de site
Você poderá usar a opção de recuperação de site **Ignorar recuperação de banco de dados (Use esta opção se o banco de dados do site não tiver sido afetado)** se pelo menos um nó do grupo de disponibilidade permanecer funcional.

 Antes de você recuperar o site quando todos os nós de um grupo de disponibilidade tiverem sido perdidos, será preciso recriar o grupo de disponibilidade. O Configuration Manager não pode recriar nem restaurar o nó de disponibilidade. Depois que o grupo for recriado e um backup for restaurado e reconfigurado, você poderá usar a opção de recuperação de site **Ignorar recuperação de banco de dados (Use esta opção se o banco de dados do site não tiver sido afetado)**.

Para obter mais informações, consulte [Backup e recuperação para o System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

## <a name="changes-for-reporting"></a>Alterações para relatórios
**Instale o ponto do Reporting Services:**  
O ponto do Reporting Services não oferece suporte a usar o nome virtual do ouvinte do grupo de disponibilidade ou hospedar o banco de dados de serviços de relatórios em um grupo de disponibilidade AlwaysOn do SQL Server:
-   Por padrão, a instalação do ponto do Reporting Services define o **Nome do servidor de banco de dados de site** como o nome virtual que está especificado como o ouvinte. Altere isso para especificar um nome do computador e a instância de uma réplica no grupo de disponibilidade.
-   Para descarregar a carga de relatórios e aumentar a disponibilidade quando um nó de réplica estiver offline, instale pontos adicionais do Reporting Services em cada nó de réplica e configure cada ponto a ponto do Reporting Services para seu próprio nome de computador.

Quando você instala um ponto do Reporting Services em cada réplica do grupo de disponibilidade, os relatórios sempre podem se conectar a um servidor ativo do ponto de relatório.

**Alterne o ponto do Reporting Services usado pelo console:**  
Para executar relatórios, no console, acesse **Monitoramento** > **Visão Geral** > **Reporting** > **Relatórios** e, em seguida, escolha **Opções de Relatório**. Na caixa de diálogo Opções de Relatório, selecione o ponto do Reporting Services desejado.

## <a name="next-steps"></a>Próximas etapas
Depois de entender os pré-requisitos, as limitações e as alterações para tarefas comuns que são necessárias quando você usa grupos de disponibilidade, veja [Configurar grupos de disponibilidade para o Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag), para saber os procedimentos para instalar e configurar seu site para usar grupos de disponibilidade.
