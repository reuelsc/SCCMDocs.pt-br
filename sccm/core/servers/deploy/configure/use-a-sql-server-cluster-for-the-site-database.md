---
title: Cluster do SQL Server | Microsoft Docs
description: "Use as configurações do cluster do SQL Server para hospedar o banco de dados do site do System Center Configuration Manager. Inclui informações sobre opções com suporte."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
caps.latest.revision: 10
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: e5a001ee018e240396498d134c5e75e325eae275


---
# <a name="use-a-sql-server-cluster-for-the-system-center-configuration-manager-site-database"></a>Use um cluster do SQL Server para o banco de dados do site do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


 Você pode usar o cluster do SQL Server para hospedar o banco de dados do site do System Center Configuration Manager. O banco de dados do site é a única função de sistema de sites com suporte em um cluster de servidores.  

> [!NOTE]  
>  Uma configuração bem-sucedida e clusters do SQL Server requerem que você esteja familiarizado com a configuração de clusters do SQL Server e se baseie em documentação e nos procedimentos fornecidos na biblioteca de documentação do SQL Server.  

 O uso de um cluster pode dar suporte a failover e melhorar a confiabilidade do banco de dados do site. No entanto, o uso de um banco de dados do site em cluster não fornece processamento adicional ou benefícios de balanceamento de carga. Na verdade, pode ocorrer degradação no desempenho, uma vez que o servidor do site deve localizar o nó ativo do cluster do SQL Server antes de se conectar ao banco de dados do site.  

 Antes de instalar o Configuration Manager, você deve preparar o cluster do SQL Server para dar suporte a ele. (Consulte os pré-requisitos nesta seção.)  

 Durante a Instalação do Configuration Manager, o gravador VSS (Serviço de Cópias de Sombra do Volume) será instalado em cada nó do computador físico do cluster do Microsoft Windows Server para dar suporte à tarefa de manutenção **Servidor do Site de Backup**.  

 Após a instalação do site, o Configuration Manager verifica alterações ao nó de cluster a cada hora e gerencia automaticamente as alterações que afetam as instalações de componentes do Configuration Manager (como um failover de nó ou a adição de um novo nó ao cluster do SQL Server).  

## <a name="supported-options-for-using-a-sql-server-failover-cluster"></a>Opções com suporte para uso de um cluster de failover do SQL Server

-   Cluster de instância única  

-   Configuração com várias instâncias  

-   Vários nós ativos  

-   Há suporte para instâncias nomeadas e padrão  

**Pré-requisitos:**  

-   O banco de dados do site deve ser remoto do servidor do site. (O cluster não pode incluir o servidor do sistema de sites.)  

-   É preciso adicionar a conta do computador do servidor do site ao grupo Administradores Locais de cada servidor no cluster.  

-   Para dar suporte a autenticação Kerberos, o protocolo de comunicação de rede **TCP/IP** deve ser habilitado para conexão de rede de cada nó de cluster do SQL Server. **Pipes nomeados** não são necessários, mas podem ser usados para solucionar problemas de autenticação Kerberos. As definições de protocolo de rede são configuradas no **SQL Server Configuration Manager** em **Configuração de Rede do SQL Server**.  

-   Se você usar uma PKI, consulte os &lt;Requisitos de certificado PKI para o Configuration Manager> para ver os requisitos específicos de certificado ao usar um cluster do SQL Server para o banco de dados do site.  

**Limitações a serem consideradas:**  

-   **Instalação e configuração:**  

    -   Sites secundários não podem usar um cluster do SQL Server.  

    -   A opção de especificar locais de arquivo não padrão para o banco de dados do site não está disponível ao especificar um cluster do SQL Server.  

-   **Provedor de SMS:**  

    -   Não há suporte para a instalação de uma instância do Provedor de SMS em um cluster do SQL Server ou em um computador que seja executado como um nó clusterizado do SQL Server.  

-   **Opções de replicação de dados:**  

    -   Se você usar **Exibições Distribuídas**, não poderá usar um Cluster do SQL Server para hospedar o banco de dados do site.  

-   **Backup e recuperação:**  

    -   O Configuration Manager não dá suporte ao backup do DPM para um cluster do SQL Server que usa uma instância nomeada, mas dá suporte ao backup do DPM em um cluster do SQL Server que usa a instância padrão do SQL Server.  

## <a name="to-prepare-a-clustered-sql-server-instance-for-the-site-database"></a>Para preparar uma instância clusterizada do SQL Server para o banco de dados do site  

-   Crie o cluster virtual do SQL Server para hospedar o banco de dados do site em um ambiente de cluster existente do Windows Server. Para ver as etapas específicas de instalação e configuração de um cluster do SQL Server, consulte a documentação específica referente à sua versão do SQL Server. Por exemplo, se você estiver usando o SQL Server 2008 R2, consulte  [Installing a SQL Server 2008 R2 Failover Cluster (Instalando um cluster de failover do SQL Server 2008 R2)](http://go.microsoft.com/fwlink/p/?LinkId=240231). Se você estiver usando o SQL Server 2014, consulte [Instalação do cluster de failover do SQL Server](https://technet.microsoft.com/library/hh231721\(v=sql.120\).aspx).  

-   Em cada computador do cluster do SQL Server, você pode colocar um arquivo com o nome **NO_SMS_ON_DRIVE.SMS** na pasta raiz de cada unidade na qual você não deseja que o Configuration Manager instale componentes do site. Por padrão, o Configuration Manager instala alguns componentes em cada nó físico para dar suporte a operações como backup.  

-   Adicione a conta do computador do servidor de site ao grupo **Administradores Locais** de cada computador do nó do cluster do Windows Server.  

-   Na instância virtual do SQL Server, atribua a função **sysadmin** do SQL Server à conta de usuário que executará a instalação do Configuration Manager.  

### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>Para instalar um novo site usando um SQL Server clusterizado  
 Para instalar um site que usa um banco de dados do site em cluster, execute a instalação do Configuration Manager seguindo o processo normal para instalar um site com a seguinte alteração:  

-   Na página **Informações do Banco de Dados** , especifique o nome da instância do cluster virtual do SQL Server que hospedará o banco de dados do site.  A instância virtual substitui o nome do computador que executa o SQL Server.  

    > [!IMPORTANT]  
    >  Ao digitar o nome da instância do cluster virtual do SQL Server, não digite o nome do Windows Server virtual criado pelo cluster do Windows Server. Se você usar o nome do Windows Server virtual, o banco de dados do site será instalado no disco rígido local do nó de cluster do Windows Server ativo. Isso impedirá um failover bem-sucedido se esse nó falhar.  



<!--HONumber=Dec16_HO3-->


