---
title: "Versões do SQL Server com suporte"
titleSuffix: Configuration Manager
description: "Obtenha os requisitos de configuração e versão do SQL Server para hospedar um banco de dados de site do System Center Configuration Manager."
ms.custom: na
ms.date: 02/14/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5c17efa3498907fcc57d366965bec3b4198890bb
ms.sourcegitcommit: 37e990d191028160486dbca286d2ea945bd5c8c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="supported-sql-server-versions-for-system-center-configuration-manager"></a>Versões do SQL Server com suporte no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Cada site do System Center Configuration Manager exige uma configuração e versão do SQL Server com suporte para hospedar o banco de dados do site.  

##  <a name="bkmk_Instances"></a> Instâncias e locais do SQL Server  
 **Site de administração central e sites primários**  
 O banco de dados do site deve usar uma instalação completa do SQL Server.  

 O SQL Server pode estar localizado:  

-   No computador do servidor do site.  
-   Em um computador remoto do servidor do site.  

Há suporte para as seguintes instâncias:  

-   A instância padrão ou nomeada do SQL Server.  
-   Configurações com várias instâncias.  
-   Um cluster do SQL Server. Consulte [Usar um cluster do SQL Server para o banco de dados do site do System Center Configuration Manager](../../../core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).
-   Um grupo de disponibilidade AlwaysOn do SQL Server. Essa opção exige o Configuration Manager versão 1602 ou posterior. Para obter detalhes, consulte [AlwaysOn do SQL Server para um banco de dados do site altamente disponível do System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).


 **Sites secundários**  
 O banco de dados do site pode usar a instância padrão de uma instalação completa do SQL Server ou SQL Server Express.  

 O SQL Server deve estar localizado no computador do servidor do site.  

 **Limitações ao suporte**   
 As configurações a seguir não têm suporte:
 -   Um cluster do SQL Server em uma configuração de cluster de NLB (Balanceamento de Carga de Rede)
 -   Um cluster do SQL Server em um CSV (Volume Compartilhado Clusterizado)
 -   Tecnologia de espelhamento de banco de dados do SQL Server e replicação ponto a ponto

Há suporte para a replicação transacional do SQL Server apenas para replicar objetos para os pontos de gerenciamento que são configurados para usar [réplicas de banco de dados](https://technet.microsoft.com/library/mt608546.aspx).  

##  <a name="bkmk_SQLVersions"></a> Versões compatíveis do Microsoft SQL Server  
 Em uma hierarquia com vários sites, diferentes sites podem usar diferentes versões do SQL Server para hospedar o banco de dados do site. Desde que os itens a seguir sejam verdadeiros:
 -  O Configuration Manager dá suporte à versão do SQL Server que você usa.
 -  As versões do SQL Server que você usa ainda têm suporte da Microsoft.
 -  O SQL Server oferece suporte à replicação entre as duas versões do SQL Server.  Por exemplo, o [SQL Server não oferece suporte à replicação entre o SQL Server 2008 R2 e o SQL Server 2016](https://docs.microsoft.com/sql/relational-databases/replication/deprecated-features-in-sql-server-replication).



 A mesmo que especificado o contrário, as versões do SQL Server a seguir têm suporte com todas as versões ativas do no System Center Configuration Manager. Se for adicionado suporte para uma nova versão ou service pack do SQL Server, a versão do Configuration Manager que adiciona esse suporte é observada. Da mesma forma, se o suporte for preterido, procure os detalhes sobre as versões afetadas do Configuration Manager.   

O suporte para um service pack específico do SQL Server inclui atualizações cumulativas, a menos que elas dividam a compatibilidade com versões anteriores com a versão base do service pack. Quando nenhuma versão de service pack estiver indicada, o suporte se destinará a essa versão do SQL Server sem service pack. No futuro, se um service pack for liberado para uma versão do SQL Server, uma instrução de suporte separada é declarada antes que essa nova versão de service pack tenha suporte.


> [!IMPORTANT]  
>  Ao usar o SQL Server Standard para o banco de dados no site de administração central, você limita o número total de clientes para o qual a hierarquia pode dar suporte. Consulte [Números de tamanho e escala](../../../core/plan-design/configs/size-and-scale-numbers.md).

### <a name="sql-server-2017-standard-enterprise"></a>SQL Server 2017: Standard, Enterprise  
Use esta versão do SQL Server, com, no mínimo, a [atualização cumulativa versão 2](https://support.microsoft.com/help/4052574), a partir do [Configuration Manager versão 1710](https://docs.microsoft.com/en-us/sccm/core/plan-design/changes/whats-new-in-version-1710) para os seguintes sites: 

-   Um site de administração central  
-   Um site primário  
-   Um site secundário  
<!--SMS.498506-->

### <a name="sql-server-2016-sp1-standard-enterprise"></a>SQL Server 2016 SP1: Standard, Enterprise  
Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site de administração central  
-   Um site primário  
-   Um site secundário  

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016: Standard, Enterprise  
Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site de administração central  
-   Um site primário  
-   Um site secundário  


### <a name="sql-server-2014-sp2-standard-enterprise"></a>SQL Server 2014 SP2: Standard, Enterprise  
Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site de administração central  
-   Um site primário  
-   Um site secundário

### <a name="sql-server-2014-sp1-standard-enterprise"></a>SQL Server 2014 SP1: Standard, Enterprise  
 Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site de administração central  
-   Um site primário  
-   Um site secundário

### <a name="sql-server-2012-sp4-standard-enterprise"></a>SQL Server 2012 SP4: Standard, Enterprise  
 Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site de administração central  
-   Um site primário  
-   Um site secundário  

### <a name="sql-server-2012-sp3-standard-enterprise"></a>SQL Server 2012 SP3: Standard, Enterprise  
 Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site de administração central  
-   Um site primário  
-   Um site secundário  

<!-- Support for this service pack version has been dropped by Microsoft    
### SQL Server 2012 SP2: Standard, Enterprise   
 You can use this version of SQL Server with no minimum cumulative update version for the following sites:  

-   A central administration site  
-   A primary site  
-   A secondary site  
-->

### <a name="sql-server-2008-r2-sp3-standard-enterprise-datacenter"></a>SQL Server 2008 R2 SP3: Standard, Enterprise, Datacenter     
  Não há suporte para esta versão do SQL Server [a partir da versão 1702.](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-support-for-sql-server-versions-as-a-site-database)  
 Esta versão do SQL Server permanece com suporte quando você usa uma versão do Configuration Manager antes da 1702.

Quando houver suporte pela versão do Configuration Manager, você poderá usar esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site de administração central  
-   Um site primário
-   Um site secundário

### <a name="sql-server-2017-express"></a>SQL Server 2017 Express   
Use esta versão do SQL Server, com, no mínimo, a [atualização cumulativa versão 2](https://support.microsoft.com/help/4052574), a partir do [Configuration Manager versão 1710](https://docs.microsoft.com/en-us/sccm/core/plan-design/changes/whats-new-in-version-1710) para os seguintes sites:
-   Um site secundário
<!--SMS.498506-->

### <a name="sql-server-2016-express-sp1"></a>SQL Server 2016 Express SP1  
Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:
-   Um site secundário

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express
Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:
-   Um site secundário


### <a name="sql-server-2014-express-sp2"></a>SQL Server 2014 Express SP2   
Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site secundário  


### <a name="sql-server-2014-express-sp1"></a>SQL Server 2014 Express SP1   
 Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site secundário  

### <a name="sql-server-2012-express-sp3"></a>SQL Server 2012 Express SP3  
Use esta versão do SQL Server sem uma versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site secundário  

<!-- Support for this service pack version has been dropped by Microsoft   
### SQL Server 2012 Express SP2   
 You can use this version of SQL Server with no minimum cumulative update version for the following sites:  

-   A secondary site  
-->


##  <a name="bkmk_SQLConfig"></a> Configurações necessárias para o SQL Server  
 Os itens a seguir são necessários para todas as instalações do SQL Server usadas para um banco de dados do site (incluindo o SQL Server Express). Quando o Configuration Manager instala o SQL Server Express como parte de uma instalação de site secundário, essas configurações são criadas automaticamente para você.  

 **Versão da arquitetura do SQL Server**  
 O Configuration Manager requer uma versão de 64 bits do SQL Server para hospedar o banco de dados do site.  

 **Agrupamento de banco de dados**  
 Em cada site, a instância do SQL Server que é usada para o site e o banco de dados do site devem usar o seguinte agrupamento: **SQL_Latin1_General_CP1_CI_AS**.  

 O Configuration Manager dá suporte a duas exceções a este agrupamento para atender aos padrões definidos no GB18030 para uso na China. para obter mais informações, consulte, [Suporte internacional no System Center Configuration Manager](../../../core/plan-design/hierarchy/international-support.md).  

 **Nível de compatibilidade do banco de dados** </br>
 O Configuration Manager requer que o nível de compatibilidade do banco de dados do site não seja menor do que a versão mais antiga com suporte do SQL Server para sua versão do Configuration Manager. Por exemplo, a começar da versão 1702, você precisará ter um [nível de compatibilidade do banco de dados](https://docs.microsoft.com/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database) maior ou igual a 110. <!-- SMS.506266--> 

 **Recursos do SQL Server**  
 Somente o recurso **Serviços de Mecanismo de Banco de Dados** é necessário para cada servidor do site.  

 A replicação de banco de dados do Configuration Manager não exige o recurso **replicação do SQL Server**. No entanto, essa configuração do SQL Server será necessária quando você usar [réplicas de banco de dados para pontos de gerenciamento do System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Autenticação do Windows**  
 O Configuration Manager exige que a **Autenticação do Windows** valide as conexões com o banco de dados.  

 **Instância do SQL Server**  
 Você deve usar uma instância dedicada do SQL Server para cada site. A instância pode ser uma **instância nomeada** ou a **instância padrão**.  

 **Memória do SQL Server**  
 Reserve memória para o SQL Server usando o SQL Server Management Studio e definindo a configuração **Memória mínima do servidor** em **Opções de Memória do Servidor**. Para saber mais sobre como configurar isso,confira [Como: definir uma quantidade fixa de memória usando (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759).  

-   **Para um servidor de banco de dados instalado no mesmo computador que o servidor do site** Limite a memória do SQL Server a 50% a 80% da memória do sistema endereçável disponível.  

-   **Para um servidor de banco de dados dedicado (remoto desde o servidor do site)** Limite a memória do SQL Server a 80% a 90% da memória do sistema endereçável disponível.  

-   **Para a reserva de memória para o pool de buffers de cada instância do SQL Server em uso:**  

    -   Para um site de administração central: defina um mínimo de 8 GB (gigabytes).  
    -   Para um site primário: defina um mínimo de 8 GB (gigabytes).  
    -   Para um site secundário: defina um mínimo de 4 GB (gigabytes).  

**Gatilhos aninhados de SQL**  
 A opção[Gatilhos aninhados de SQL](http://go.microsoft.com/fwlink/?LinkId=528802) deve estar habilitada.  

 **Integração de CLR do SQL Server**  
  O banco de dados do site exige que o CLR (common language runtime) do SQL Server seja habilitado. Isso é habilitado automaticamente quando o Configuration Manager é instalado. Para saber mais sobre o CLR, confira [Introdução à integração do SQL Server CLR](https://msdn.microsoft.com/library/ms254498\(v=vs.110\).aspx).  

##  <a name="bkmk_optional"></a> Configurações opcionais para o SQL Server  
 As configurações a seguir são opcionais para cada banco de dados que usa uma instalação completa do SQL Server.  

 **Serviço SQL Server**  
 Você pode configurar o serviço do SQL Server para execução usando:  

-   Uma conta de *usuário de domínio com direitos limitados*:  

    -   Essa é uma prática recomendada e pode exigir o registro manual do SPN (nome da entidade de serviço) da conta.  

-   A conta **sistema local** do computador que executa o SQL Server:  

    -   Use a conta do sistema local para simplificar o processo de configuração.  
    -   Ao usar a conta do sistema local, o Configuration Manager registra automaticamente o SPN para o serviço SQL Server.  
    -   Lembre-se de que usar a conta do sistema local para o serviço SQL Server não é uma melhor prática do SQL Server.  

Quando o computador que executa o SQL Server não usa a conta sistema local para executar o serviço SQL Server, é necessário configurar o SPN da conta que executa o serviço SQL Server no Active Directory Domain Services. (Quando a conta do sistema for usada, o SPN será registrado automaticamente para você.)

Para obter informações sobre SPNs para o banco de dados do site, consulte [Gerenciar o SPN para o servidor de banco de dados do site](../../../core/servers/manage/modify-your-infrastructure.md#bkmk_SPN) no artigo [Modificar a infraestrutura do System Center Configuration Manager](../../../core/servers/manage/modify-your-infrastructure.md).  

Para obter informações sobre como alterar a conta usada pelo serviço SQL Server, consulte [Como alterar a conta de inicialização do serviço do SQL Server (SQL Server Configuration Manager)](http://go.microsoft.com/fwlink/p/?LinkId=237661).  

**SQL Server Reporting Services**  
O SQL Server Reporting Services é necessário para a instalação de um ponto do Reporting Services que permite a execução de relatórios.  

> [!IMPORTANT]  
> Após a atualização do SQL Server de uma versão anterior, você poderá ver o seguinte erro: *Construtor de Relatórios não existe*.    
> Para resolver esse erro, é necessário reinstalar a função do sistema de sites do ponto do Reporting Services.

**Portas do SQL Server**  
Para a comunicação com o mecanismo de banco de dados do SQL Server e para a replicação entre sites, é possível usar as configurações de porta padrão do SQL Server ou especificar portas personalizadas:  

-   A **comunicação entre sites** usa o SQL Server Service Broker, que usa a porta TCP 4022 por padrão.  
-   A **comunicação intrassite** entre o mecanismo de banco de dados do SQL Server e as várias funções do sistema de sites do Configuration Manager usa a porta TCP 1433 por padrão. As seguintes funções do sistema de site se comunicam diretamente com o banco de dados do SQL Server:  

    -   Ponto de gerenciamento  
    -   Computador do Provedor de SMS  
    -   Ponto do Reporting Services  
    -   Servidor do site  

Quando um computador que executa o SQL Server hospeda um banco de dados de mais de um site, cada banco de dados deve usar uma instância separada do SQL Server. Além disso, cada instância deve ser configurada para usar um conjunto exclusivo de portas.  

> [!WARNING]  
>  O Configuration Manager não dá suporte a portas dinâmicas. Como as instâncias nomeadas do SQL Server por padrão usam as portas dinâmicas para fazer conexões com o mecanismo de banco de dados, ao usar uma instância nomeada, configure manualmente a porta estática que deseja usar para a comunicação entre sites.  

Se você tiver um firewall habilitado no computador com o SQL Server, verifique se ele está configurado para permitir as portas usadas por sua implantação e em todos os locais na rede entre os computadores que se comunicam com o SQL Server.  

Para obter um exemplo de como configurar o SQL Server para usar uma porta específica, veja [Como: configurar um servidor para escutar em uma porta TCP específica (SQL Server Configuration Manager)](http://go.microsoft.com/fwlink/p/?LinkID=226349) na biblioteca do TechNet do SQL Server.  

## <a name="upgrade-options-for-sql-server"></a>Opções de atualização para o SQL Server
Se você precisa atualizar sua versão do SQL Server, recomendamos os seguintes métodos, do mais fácil para o mais complexo.
1. [Atualização do SQL Server no local](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recomendado).
2. Instale uma nova versão do SQL Server em um novo computador e, em seguida, [use a opção de mover o banco de dados](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) da instalação do Configuration Manager para apontar o servidor do site para o novo SQL Server.
3. Use [backup e recuperação](/sccm/protect/understand/backup-and-recovery). Há suporte para o uso de backup e recuperação para um cenário de upgrade do SQL. Você pode ignorar o requisito de controle de versão do SQL ao revisar as [Considerações antes de recuperar um site](/sccm/protect/understand/recover-sites.md#considerations-before-recovering-a-site). 
