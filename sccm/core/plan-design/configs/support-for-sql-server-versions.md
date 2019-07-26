---
title: Versões do SQL Server com suporte
titleSuffix: Configuration Manager
description: Obtenha os requisitos de configuração e versão do SQL Server para hospedar um banco de dados de site do Configuration Manager.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 710f9939b157c27d9eff6007d7f91cdef15889fe
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68339372"
---
# <a name="supported-sql-server-versions-for-configuration-manager"></a>Versões do SQL Server compatíveis com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Cada site do System Center Configuration Manager exige uma configuração e versão do SQL Server com suporte para hospedar o banco de dados do site.  



##  <a name="bkmk_Instances"></a> Instâncias e locais do SQL Server  
 
### <a name="central-administration-site-and-primary-sites"></a>Site de administração central e sites primários  
O banco de dados do site deve usar uma instalação completa do SQL Server.  

O SQL Server pode estar localizado:  

- No computador do servidor do site.  
- Em um computador remoto do servidor do site.  

Há suporte para as seguintes instâncias:  

- A instância padrão ou nomeada do SQL Server.  
- Configurações com várias instâncias.  
- Um cluster do SQL Server. Consulte [Usar um cluster do SQL Server para o banco de dados do site do System Center Configuration Manager](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database).
- Um grupo de disponibilidade AlwaysOn do SQL Server. Para obter mais informações, confira [SQL Server AlwaysOn para um banco de dados do site altamente disponível](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).


### <a name="secondary-sites"></a>Sites secundários  
O banco de dados do site pode usar a instância padrão de uma instalação completa do SQL Server ou SQL Server Express.  

O SQL Server deve estar localizado no computador do servidor do site.  


### <a name="limitations-to-support"></a>Limitações ao suporte   
As configurações a seguir não são compatíveis:
- Um cluster do SQL Server em uma configuração de cluster de NLB (Balanceamento de Carga de Rede)
- Um cluster do SQL Server em um CSV (Volume Compartilhado Clusterizado)
- Tecnologia de espelhamento de banco de dados do SQL Server e replicação ponto a ponto

Há suporte para a replicação transacional do SQL Server apenas para replicar objetos para os pontos de gerenciamento que são configurados para usar [réplicas de banco de dados](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).  



##  <a name="bkmk_SQLVersions"></a> Versões compatíveis do Microsoft SQL Server  
Em uma hierarquia com vários sites, diferentes sites podem usar diferentes versões do SQL Server para hospedar o banco de dados do site. Desde que os itens a seguir sejam verdadeiros:
- O Configuration Manager dá suporte à versão do SQL Server que você usa.
- As versões do SQL Server que você usa ainda têm suporte da Microsoft.
- O SQL Server oferece suporte à replicação entre as duas versões do SQL Server. Por exemplo, o SQL Server não oferece suporte à replicação entre o SQL Server 2008 R2 e o SQL Server 2016. Para saber mais, consulte [Recursos preteridos na replicação do SQL Server](https://docs.microsoft.com/sql/relational-databases/replication/deprecated-features-in-sql-server-replication).



A menos que especificado o contrário, as versões do SQL Server a seguir são compatíveis com todas as versões ativas do Configuration Manager. Se for adicionado suporte para uma nova versão ou service pack do SQL Server, a versão do Configuration Manager que adiciona esse suporte é observada. Da mesma forma, se o suporte for preterido, procure os detalhes sobre as versões afetadas do Configuration Manager.   

O suporte para um service pack específico do SQL Server inclui atualizações cumulativas, a menos que elas dividam a compatibilidade com versões anteriores com a versão base do service pack. Quando nenhuma versão de service pack estiver indicada, o suporte se destinará a essa versão do SQL Server sem service pack. No futuro, se um service pack for liberado para uma versão do SQL Server, uma instrução de suporte separada é declarada antes que essa nova versão de service pack tenha suporte.


> [!IMPORTANT]  
> Ao usar o SQL Server Standard para o banco de dados no site de administração central, você limita o número total de clientes para o qual a hierarquia pode dar suporte. Consulte [Números de tamanho e escala](/sccm/core/plan-design/configs/size-and-scale-numbers).

### <a name="sql-server-2017-standard-enterprise"></a>SQL Server 2017: Standard, Enterprise  
Use esta versão do SQL Server, com, no mínimo, a [atualização cumulativa versão 2](https://support.microsoft.com/help/4052574), a partir do [Configuration Manager versão 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710) para os seguintes sites: 

- Um site de administração central  
- Um site primário  
- Um site secundário  
  <!--SMS.498506-->

### <a name="sql-server-2016-sp2-standard-enterprise"></a>SQL Server 2016 SP2: Standard, Enterprise  
<!--514985-->
Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

- Um site de administração central  
- Um site primário  
- Um site secundário  

### <a name="sql-server-2016-sp1-standard-enterprise"></a>SQL Server 2016 SP1: Standard, Enterprise  
Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

- Um site de administração central  
- Um site primário  
- Um site secundário  

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016: Standard, Enterprise  
Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

- Um site de administração central  
- Um site primário  
- Um site secundário  

### <a name="sql-server-2014-sp3-standard-enterprise"></a>SQL Server 2014 SP3: Standard, Enterprise  
Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

- Um site de administração central  
- Um site primário  
- Um site secundário

### <a name="sql-server-2014-sp2-standard-enterprise"></a>SQL Server 2014 SP2: Standard, Enterprise  
Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

- Um site de administração central  
- Um site primário  
- Um site secundário

### <a name="sql-server-2014-sp1-standard-enterprise"></a>SQL Server 2014 SP1: Standard, Enterprise  
 Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

- Um site de administração central  
- Um site primário  
- Um site secundário

### <a name="sql-server-2012-sp4-standard-enterprise"></a>SQL Server 2012 SP4: Standard, Enterprise  
 Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

- Um site de administração central  
- Um site primário  
- Um site secundário  

### <a name="sql-server-2012-sp3-standard-enterprise"></a>SQL Server 2012 SP3: Standard, Enterprise  
 Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

- Um site de administração central  
- Um site primário  
- Um site secundário  

### <a name="sql-server-2008-r2-sp3-standard-enterprise-datacenter"></a>SQL Server 2008 R2 SP3: Standard, Enterprise, Datacenter     
Esta versão do SQL Server não é compatível. Para saber mais, confira [Suporte preterido para versões do SQL Server como um banco de dados do site](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#sql-server).  

### <a name="sql-server-2017-express"></a>SQL Server 2017 Express   
Use esta versão do SQL Server, com, no mínimo, a [atualização cumulativa versão 2](https://support.microsoft.com/help/4052574), a partir do [Configuration Manager versão 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710) para os seguintes sites:
- Um site secundário
<!--SMS.498506-->

### <a name="sql-server-2016-express-sp2"></a>SQL Server 2016 Express SP2  
Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:
- Um site secundário

### <a name="sql-server-2016-express-sp1"></a>SQL Server 2016 Express SP1  
Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:
- Um site secundário

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express
Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:
- Um site secundário

### <a name="sql-server-2014-express-sp3"></a>SQL Server 2014 Express SP3   
Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

- Um site secundário  

### <a name="sql-server-2014-express-sp2"></a>SQL Server 2014 Express SP2   
Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

- Um site secundário  

### <a name="sql-server-2014-express-sp1"></a>SQL Server 2014 Express SP1   
 Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

- Um site secundário  

### <a name="sql-server-2012-express-sp3"></a>SQL Server 2012 Express SP3  
Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

- Um site secundário  



##  <a name="bkmk_SQLConfig"></a> Configurações necessárias para o SQL Server  
Os itens a seguir são necessários para todas as instalações do SQL Server usadas para um banco de dados do site (incluindo o SQL Server Express). Quando o Configuration Manager instala o SQL Server Express como parte de uma instalação de site secundário, essas configurações são criadas automaticamente para você.  

### <a name="sql-server-architecture-version"></a>Versão da arquitetura do SQL Server  
O Configuration Manager requer uma versão de 64 bits do SQL Server para hospedar o banco de dados do site.  

### <a name="database-collation"></a>Ordenação de banco de dados  
Em cada site, a instância do SQL Server usada para o site e o banco de dados do site devem usar a seguinte ordenação: **SQL_Latin1_General_CP1_CI_AS**.  

O Configuration Manager dá suporte a duas exceções a esta ordenação para atender aos padrões definidos no GB18030 para uso na China. Para saber mais, confira [Suporte internacional](/sccm/core/plan-design/hierarchy/international-support).  

### <a name="database-compatibility-level"></a>Nível de compatibilidade do banco de dados   
O Configuration Manager requer que o nível de compatibilidade do banco de dados do site não seja menor do que a versão mais antiga com suporte do SQL Server para sua versão do Configuration Manager. Por exemplo, a começar da versão 1702, você precisará ter um [nível de compatibilidade do banco de dados](https://docs.microsoft.com/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database) maior ou igual a 110. <!-- SMS.506266--> 

### <a name="sql-server-features"></a>Recursos do SQL Server  
Somente o recurso **Serviços de Mecanismo de Banco de Dados** é necessário para cada servidor do site.  

A replicação de banco de dados do Configuration Manager não exige o recurso **replicação do SQL Server**. No entanto, essa configuração do SQL Server é necessária ao usar [réplicas de banco de dados para pontos de gerenciamento](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).  

### <a name="windows-authentication"></a>Autenticação do Windows  
O Configuration Manager exige que a **Autenticação do Windows** valide as conexões com o banco de dados.  

### <a name="sql-server-instance"></a>Instância do SQL Server  
Use uma instância dedicada do SQL Server para cada site. A instância pode ser uma **instância nomeada** ou a **instância padrão**.  

### <a name="sql-server-memory"></a>Memória do SQL Server  
Reserve memória para o SQL Server usando o SQL Server Management Studio e definindo a configuração **Memória mínima do servidor** em **Opções de Memória do Servidor**. Para saber mais sobre como definir esta configuração, consulte [Opções de configuração do servidor de memória do SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options).  

- **Para um servidor de banco de dados instalado no mesmo computador do que o servidor do site**: Limite a memória do SQL Server a 50-80% da memória de sistema endereçável disponível.  

- **Para um servidor de banco de dados dedicado (remoto do servidor do site)** : Limite a memória do SQL Server a 80-90% da memória de sistema endereçável disponível.  

- **Para a reserva de memória para o pool de buffers de cada instância do SQL Server em uso**:  

  - Para um site de administração central: Defina um mínimo de 8 gigabytes (GB).  
  - Para um site primário: Defina um mínimo de 8 gigabytes (GB).  
  - Para um site secundário: Defina um mínimo de 4 gigabytes (GB).  

### <a name="sql-nested-triggers"></a>Gatilhos aninhados de SQL  
Os gatilhos aninhados de SQL devem estar habilitados. Para saber mais, confira [Definir a opção de configuração do servidor de gatilhos aninhados](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option) 

### <a name="sql-server-clr-integration"></a>Integração de CLR do SQL Server  
O banco de dados do site exige que o CLR (common language runtime) do SQL Server seja habilitado. Essa opção é habilitada automaticamente ao instalar o Configuration Manager. Para saber mais sobre o CLR, confira [Introdução à integração do SQL Server CLR](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).  

### <a name="sql-server-service-broker-ssb"></a>SQL SSB (Server Service Broker)
O SQL Server Service Broker é necessário tanto para replicação entre sites quanto para um único site primário. 

##  <a name="bkmk_optional"></a> Configurações opcionais para o SQL Server  
As configurações a seguir são opcionais para cada banco de dados que usa uma instalação completa do SQL Server.  

### <a name="sql-server-service"></a>Serviço SQL Server  
Você pode configurar o serviço do SQL Server para execução usando:  

- Uma conta de *usuário de domínio com direitos limitados*:  

  - Essa configuração é uma prática recomendada e pode exigir o registro manual do SPN (nome da entidade de serviço) da conta.  

- A conta **sistema local** do computador que executa o SQL Server:  

  - Use a conta do sistema local para simplificar o processo de configuração.  
  - Ao usar a conta do sistema local, o Configuration Manager registra automaticamente o SPN para o serviço SQL Server.  
  - Usar a conta do sistema local para o serviço SQL Server não é uma prática recomendada do SQL Server.  

Quando o computador que executa o SQL Server não usa a conta do sistema local para executar o serviço SQL Server, configure o SPN da conta que executa o serviço SQL Server no Active Directory Domain Services. (Quando a conta do sistema for usada, o SPN será registrado automaticamente para você.)

Para saber mais sobre SPNs de banco de dados do site, confira [Gerenciar o SPN do servidor de banco de dados do site](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_SPN).  

Para saber mais sobre como alterar a conta usada pelo serviço SQL Server, confira [Serviços SCM: alterar a conta de inicialização do serviço](https://docs.microsoft.com/sql/database-engine/configure-windows/scm-services-change-the-service-startup-account).  

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services  
O SQL Server Reporting Services é necessário para a instalação de um ponto do Reporting Services que permite a execução de relatórios.  

> [!IMPORTANT]  
> Após a atualização do SQL Server de uma versão anterior, poderá surgir o seguinte erro:  *O Construtor de Relatórios não existe*.  
> Para resolver esse erro, é necessário reinstalar a função do sistema de sites do ponto do Reporting Services.  

### <a name="sql-server-ports"></a>Portas do SQL Server  
Para a comunicação com o mecanismo de banco de dados do SQL Server e para a replicação entre sites, é possível usar as configurações de porta padrão do SQL Server ou especificar portas personalizadas:  

- A **comunicação entre sites** usa o SQL Server Service Broker, que usa a porta TCP 4022 por padrão.  
- A **comunicação intrassite** entre o mecanismo de banco de dados do SQL Server e as várias funções do sistema de sites do Configuration Manager usa a porta TCP 1433 por padrão. As seguintes funções do sistema de site se comunicam diretamente com o banco de dados do SQL Server:  

  - Ponto de gerenciamento  
  - Computador do Provedor de SMS  
  - Ponto do Reporting Services  
  - Servidor do site  

Quando um computador que executa o SQL Server hospeda um banco de dados de mais de um site, cada banco de dados deve usar uma instância separada do SQL Server. Além disso, cada instância deve ser configurada para usar um conjunto exclusivo de portas.  

> [!WARNING]  
> O Configuration Manager não dá suporte a portas dinâmicas. Como as instâncias nomeadas do SQL Server por padrão usam as portas dinâmicas para fazer conexões com o mecanismo de banco de dados, ao usar uma instância nomeada, configure manualmente a porta estática que deseja usar para a comunicação entre sites.  

Se você tiver um firewall habilitado no computador com o SQL Server, verifique se ele está configurado para permitir as portas usadas por sua implantação e todos os locais de rede entre os computadores que se comunicam com o SQL Server.  

Para ver um exemplo sobre como configurar o SQL Server para usar uma porta específica, confira [Configurar um servidor para escutar em uma porta TCP específica](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  



## <a name="upgrade-options-for-sql-server"></a>Opções de atualização para o SQL Server

Se você precisa atualizar sua versão do SQL Server, recomendamos os seguintes métodos, do mais fácil para o mais complexo:  

- [Atualização do SQL Server no local](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#to-upgrade-sql-server-on-the-site-database-server) (recomendado)  

- Instale uma nova versão do SQL Server em um novo computador e, em seguida, [use a opção de mover o banco de dados](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_dbconfig) da instalação do Configuration Manager para apontar o servidor do site para o novo SQL Server  

- Use [backup e recuperação](/sccm/protect/understand/backup-and-recovery). Há suporte para o uso de backup e recuperação para um cenário de upgrade do SQL. Você pode ignorar o requisito de controle de versão do SQL ao revisar as [Considerações antes de recuperar um site](/sccm/protect/understand/recover-sites#considerations-before-recovering-a-site). 
