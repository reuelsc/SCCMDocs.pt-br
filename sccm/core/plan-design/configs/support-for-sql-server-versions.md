---
title: Suporte para SQL Server | System Center Configuration Manager
description: "Obtenha os requisitos de configuração e versão do SQL Server para hospedar um banco de dados de site do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
caps.latest.revision: 21
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b17720021f797d404a89933939427696dfafd7dc


---
# <a name="support-for-sql-server-versions-for-system-center-configuration-manager"></a>Suporte para versões do SQL Server para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Cada site do System Center Configuration Manager exige uma configuração e versão do SQL Server com suporte para hospedar o banco de dados do site.  

##  <a name="a-namebkmkinstancesa-sql-server-instances-and-locations"></a><a name="bkmk_Instances"></a> Instâncias e locais do SQL Server  
 **Site de administração central e sites primários:**  

O banco de dados do site deve usar uma instalação completa do SQL Server.  

 O local do SQL Server pode estar em:  

-   o computador do servidor do site  
-   Um computador remoto do servidor do site  

Há suporte para as seguintes instâncias:  

-   Instância padrão ou nomeada do SQL Server  
-   Configurações com várias instâncias  
-   Cluster do SQL Server – Consulte [Usar um cluster do SQL Server para hospedar o banco de dados do site](../../../core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md)
-   Grupo de disponibilidade AlwaysOn do SQL Server - esta opção exige o Configuration Manager versão 1602 ou posterior. Para obter detalhes, confira [SQL Server AlwaysOn for a highly available site database for System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) (AlwaysOn do SQL Server para um banco de dados de site altamente disponível para o System Center Configuration Manager)  

> [!NOTE]  
>  Não há suporte para o cluster do SQL Server em uma configuração de cluster NLB (Balanceamento de Carga de Rede). Além disso, não há suporte para a tecnologia de espelhamento de banco de dados do SQL Server e para a replicação ponto a ponto. Há suporte para a replicação transacional padrão do SQL Server apenas para replicar objetos para os pontos de gerenciamento que são configurados para usar [réplicas de banco de dados](https://technet.microsoft.com/library/mt608546.aspx).  


 **Sites secundários:**  

 O banco de dados do site pode usar a instância padrão de uma instalação completa do SQL Server ou SQL Server Express  

 O local do SQL Server deve ser no computador do servidor do site  

##  <a name="a-namebkmksqlversionsa-supported-versions-of-sql-server"></a><a name="bkmk_SQLVersions"></a> Versões do Microsoft SQL Server com suporte  
 Em uma hierarquia com vários sites, diferentes sites podem usar diferentes versões do SQL Server para hospedar o banco de dados do site, desde que a versão do SQL Server usadas tenha suporte do Configuration Manager.  

 As versões do SQL Server a seguir têm suporte com o System Center Configuration Manager versão 1511 e posterior.  

> [!IMPORTANT]  
>  Usar o SQL Server Standard para o banco de dados no site de administração central limita o número total de clientes para o qual a hierarquia pode dar suporte. Consulte [Números de tamanho e escala](../../../core/plan-design/configs/size-and-scale-numbers.md).

### <a name="sql-server-2016---standard-enterprise"></a>SQL Server 2016 – Standard, Enterprise  

Com suporte para uso na versão 1606.   
Você pode usar essa versão do SQL Server sem uma versão de atualização cumulativa mínima para o seguinte:  

-   Site de administração central  
-   Site primário  
-   Site secundário  


### <a name="sql-server-2014-sp2---standard-enterprise"></a>SQL Server 2014 SP2 – Standard, Enterprise  

Com suporte na versão 1511 e posterior.  
Você pode usar essa versão do SQL Server sem uma versão de atualização cumulativa mínima para o seguinte:  

-   Site de administração central  
-   Site primário  
-   Site secundário  



### <a name="sql-server-2014-sp1---standard-enterprise"></a>SQL Server 2014 SP1 – Standard, Enterprise  

Com suporte na versão 1511 e posterior.  
 Você pode usar essa versão do SQL Server sem uma versão de atualização cumulativa mínima para o seguinte:  

-   Site de administração central  
-   Site primário  
-   Site secundário  


### <a name="sql-server-2012-sp3---standard-enterprise"></a>SQL Server 2012 SP3 – Standard, Enterprise  

Com suporte na versão 1511 e posterior.  
 Você pode usar essa versão do SQL Server sem uma versão de atualização cumulativa mínima para o seguinte:  

-   Site de administração central  
-   Site primário  
-   Site secundário  


### <a name="sql-server-2012-sp2---standard-enterprise"></a>SQL Server 2012 SP2 – Standard, Enterprise  

Com suporte na versão 1511 e posterior.  
 Você pode usar essa versão do SQL Server sem uma versão de atualização cumulativa mínima para o seguinte:  

-   Site de administração central  
-   Site primário  
-   Site secundário  


### <a name="sql-server-2008-r2-sp3---standard-enterprise-datacenter"></a>SQL Server 2008 R2 SP3 – Standard, Enterprise, Datacenter  

Com suporte na versão 1511 e posterior.    
Você pode usar essa versão do SQL Server sem uma versão de atualização cumulativa mínima para o seguinte:  

-   Site de administração central  
-   Site primário  
-   Site secundário  

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express
Com suporte para uso na versão 1606.  
Você pode usar essa versão do SQL Server sem uma versão de atualização cumulativa mínima para o seguinte:
-   Site secundário

### <a name="sql-server-2014-express-sp2"></a>SQL Server 2014 Express SP2  
Com suporte para uso na versão 1511 e posterior.  
Você pode usar essa versão do SQL Server sem uma versão de atualização cumulativa mínima para o seguinte:  

-   Site secundário  


### <a name="sql-server-2014-express-sp1"></a>SQL Server 2014 Express SP1  
 Com suporte para uso na versão 1511 e posterior.   
 Você pode usar essa versão do SQL Server sem uma versão de atualização cumulativa mínima para o seguinte:  

-   Site secundário  

### <a name="sql-server-2012-express-sp3"></a>SQL Server 2012 Express SP3  
Com suporte para uso na versão 1511 e posterior.   
Você pode usar essa versão do SQL Server sem uma versão de atualização cumulativa mínima para o seguinte:  

-   Site secundário  

### <a name="sql-server-2012-express-sp2"></a>SQL Server 2012 Express SP2  
 Com suporte para uso na versão 1511 e posterior.  
 Você pode usar essa versão do SQL Server sem uma versão de atualização cumulativa mínima para o seguinte:  

-   Site secundário  

##  <a name="a-namebkmksqlconfiga-required-configurations-for-sql-server"></a><a name="bkmk_SQLConfig"></a> Configurações obrigatórias para o SQL Server  
 Os itens a seguir são necessários para todas as instalações do SQL Server usadas para um banco de dados de site, (incluindo o SQL Server Express). Quando o Configuration Manager instala o SQL Server Express como parte da instalação do site secundário, essas configurações são feitas automaticamente para você.  

 **Versão da arquitetura do SQL Server:**  
 O Configuration Manager requer uma versão de 64 bits do SQL Server para hospedar o banco de dados do site.  

 **Agrupamento de banco de dados:**  
 Em cada site, a instância do SQL Server que é usada para o site e o banco de dados do site devem usar o seguinte agrupamento: **SQL_Latin1_General_CP1_CI_AS**.  

 O Configuration Manager dá suporte a duas exceções a este agrupamento para atender aos padrões definidos no GB18030 para uso na China. para obter mais informações, consulte, [Suporte internacional no System Center Configuration Manager](../../../core/plan-design/hierarchy/international-support.md).  

 **Recursos do SQL Server:**  
 Somente o recurso **Serviços de Mecanismo de Banco de Dados** é necessário para cada servidor do site.  

 A replicação de banco de dados do Configuration Manager não exige o recurso de **replicação do SQL Server**. No entanto, essa configuração do SQL Server será necessária se você for usar [Réplicas de banco de dados para pontos de gerenciamento para o System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Autenticação do Windows:**  
 O Configuration Manager exige que a **Autenticação do Windows** valide as conexões com o banco de dados.  

 **Instância do SQL Server:**  
 Você deve usar uma instância dedicada do SQL Server para cada site. Isso pode ser uma **instância nomeada** ou uma **instância padrão**.  

 **Memória do SQL Server:**  
 Reserve a memória para o SQL Server usando o SQL Server Management Studio e definindo a configuração de **Memória mínima do servidor** em **Opções de Memória do Servidor**. Para obter mais informações sobre como definir uma quantidade fixa de memória, veja [Como: definir uma quantidade fixa de memória (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759).  

-   **Servidor de banco de dados instalado no mesmo computador que o servidor do site:** - limite a memória do SQL Server para 50% a 80% da memória do sistema endereçável disponível.  

-   **Servidor de banco de dados localizado (remoto do servidor do site):** – limite a memória do SQL Server a 80% a 90% da memória de sistema endereçável disponível.  

-   **Reserva de memória para o pool de buffers de cada instância do SQL Server em uso:**  

    -   Site de administração central: mínimo de 8 gigabytes (GB)  
    -   Site primário: mínimo de 8 gigabytes (GB)  
    -   Site secundário: mínimo de 4 gigabytes (GB)  

 **Gatilhos aninhados de SQL:**  

 A opção[Gatilhos aninhados de SQL](http://go.microsoft.com/fwlink/?LinkId=528802) deve estar habilitada.  

 **Integração de CLR do SQL Server**  

  O banco de dados do site exige que o CLR (common language runtime) do SQL Server seja habilitado. Isso é habilitado automaticamente quando o Configuration Manager é instalado. Para saber mais sobre o CLR, confira [Introdução à integração do SQL Server CLR](https://msdn.microsoft.com/library/ms254498\(v=vs.110\).aspx)  

##  <a name="a-namebkmkoptionala-optional-configurations-for-sql-server"></a><a name="bkmk_optional"></a> Configurações opcionais para o SQL Server  
 As configurações a seguir são opcionais para cada banco de dados que usa uma instalação completa do SQL Server.  

 **Serviço SQL Server:**  
 Você pode configurar o serviço do SQL Server para execução usando:  

-   Conta do**usuário de domínio local** :  

    -   Essa é uma prática recomendada e pode exigir que você registre manualmente o SPN (nome da entidade de serviço) para a conta.  

-   Conta do**sistema local** do computador que executa o SQL Server:  

    -   Use a conta do sistema local para simplificar o processo de configuração.  
    -   Ao usar a conta do sistema local, o Configuration Manager registra automaticamente o SPN para o serviço SQL Server.  
    -   Lembre-se de que usar a conta do sistema local para o serviço SQL Server não é uma melhor prática do SQL Server.  

Quando o SQL Server não usar a conta de sistema local do computador para executar serviços do SQL Server, você deve configurar o SPN (nome da entidade de serviço) da conta que executa os serviços SQL Server nos Serviços de Domínio do Active Directory. (Quando a conta do sistema for usada, o SPN será registrado automaticamente para você.)

Para obter informações sobre SPNs para o banco de dados do site, consulte  [Manage the SPN for the site database server](../../../core/servers/manage/modify-your-infrastructure.md#bkmk_SPN) no tópico [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md) .  

Para obter informações sobre como alterar a conta usada pelo Serviço do SQL, veja [Como: alterar a conta de inicialização do serviço do SQL Server (SQL Server Configuration Manager)](http://go.microsoft.com/fwlink/p/?LinkId=237661).  

**SQL Server Reporting Services:**  
Necessário para instalar um ponto do Reporting Services que permita executar relatórios.  

**Portas do SQL Server:**  
Para a comunicação com o mecanismo de banco de dados do SQL Server e para a replicação entre sites, é possível usar as configurações de porta padrão do SQL Server ou especificar portas personalizadas:  

-   A**comunicação entre sites** usa o SQL Server Service Broker que, por padrão, usa a porta TCP 4022.  
-   A **comunicação entre sites** entre o mecanismo de banco de dados do SQL Server e várias funções do sistema de sites do Configuration Manager usa a porta TCP 1433 por padrão. As seguintes funções do sistema de site se comunicam diretamente com o banco de dados do SQL Server:  

    -   Ponto de gerenciamento  
    -   Computador do Provedor de SMS  
    -   Ponto do Reporting Services  
    -   Servidor do site  

Quando um SQL Server hospeda um bancos de dados de mais de um site, cada banco de dados deve usar uma instância separada do SQL Server, e cada instância deve ser configurada para usar um conjunto de portas exclusivo.  

> [!WARNING]  
>  O Configuration Manager não dá suporte a portas dinâmicas. Como as instâncias nomeadas do SQL Server por padrão usam as portas dinâmicas para fazer conexões com o mecanismo de banco de dados, ao usar uma instância nomeada, configure manualmente a porta estática que deseja usar para a comunicação entre sites.  

Se você tiver um firewall habilitado no computador com o SQL Server, verifique se ele está configurado para permitir as portas usadas por sua implantação e em todos os locais na rede entre os computadores que se comunicam com o SQL Server.  

Para obter um exemplo de como configurar o SQL Server para usar uma porta específica, veja [Como: configurar um servidor para escutar em uma porta TCP específica (SQL Server Configuration Manager)](http://go.microsoft.com/fwlink/p/?LinkID=226349) na biblioteca do TechNet do SQL Server.  



<!--HONumber=Nov16_HO1-->


