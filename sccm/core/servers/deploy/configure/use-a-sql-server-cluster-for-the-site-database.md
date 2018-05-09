---
title: Cluster do SQL Server
titleSuffix: Configuration Manager
description: Use as configurações do cluster do SQL Server para hospedar o banco de dados do site do System Center Configuration Manager. Inclui informações sobre opções com suporte.
ms.date: 2/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dfd791dead376f22014156829bec1fa2fb75ab51
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="use-a-sql-server-cluster-for-the-system-center-configuration-manager-site-database"></a>Use um cluster do SQL Server para o banco de dados do site do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


 Você pode usar o cluster do SQL Server para hospedar o banco de dados do site do System Center Configuration Manager. O banco de dados do site é a única função de sistema de sites com suporte em um cluster de servidores.  

> [!IMPORTANT]  
>  A configuração bem-sucedida dos clusters do SQL Server se baseia na documentação e nos procedimentos fornecidos na biblioteca de documentação do SQL Server.  

 Um cluster pode dar suporte a failover e melhorar a confiabilidade do banco de dados do site. No entanto, isso não fornece processamento adicional ou benefícios de balanceamento de carga. Na verdade, pode ocorrer degradação no desempenho, uma vez que o servidor do site deve localizar o nó ativo do cluster do SQL Server antes de se conectar ao banco de dados do site.  

 Antes de instalar o Configuration Manager, você deve preparar o cluster do SQL Server para dar suporte a ele. (Consulte os pré-requisitos nesta seção.)  

 Durante a instalação do Configuration Manager, o gravador Serviço de Cópias de Sombra de Volume do Windows será instalado em cada nó do computador físico do cluster do Microsoft Windows Server. Isso dá suporte à tarefa de manutenção **Servidor do Site de Backup**.  

 Depois de instalar o site, o Configuration Manager verifica se há alterações para o nó de cluster a cada hora. O Configuration Manager gerencia automaticamente as alterações que afetam as instalações de componentes do Configuration Manager (como um failover de nó ou a adição de um novo nó ao cluster do SQL Server).  

## <a name="supported-options-for-using-a-sql-server-failover-cluster"></a>Opções com suporte para uso de um cluster de failover do SQL Server

As opções a seguir têm suporte para clusters de failover do SQL Server usados como o banco de dados do site:

-   Um cluster de instância única  

-   Configuração com várias instâncias  

-   Vários nós ativos  

-   Uma instância nomeada ou uma padrão  

Lembre-se dos seguintes pré-requisitos:  

-   O banco de dados do site deve ser remoto do servidor do site. (O cluster não pode incluir o servidor do sistema de sites.)  

-   É preciso adicionar a conta do computador do servidor do site ao grupo Administradores Locais de cada servidor no cluster.  

-   Para dar suporte a autenticação Kerberos, o protocolo de comunicação de rede **TCP/IP** deve ser habilitado para conexão de rede de cada nó de cluster do SQL Server. **Pipes nomeados** não são necessários, mas podem ser usados para solucionar problemas de autenticação Kerberos. As definições de protocolo de rede são configuradas no **SQL Server Configuration Manager** em **Configuração de Rede do SQL Server**.  

-   Se você usar uma PKI, consulte os Requisitos de certificado PKI para o Configuration Manager para ver os requisitos específicos de certificado ao usar um cluster do SQL Server para o banco de dados do site.  

Considere as seguintes limitações:  

-   **Instalação e configuração:**  

    -   Sites secundários não podem usar um cluster do SQL Server.  

    -   A opção de especificar locais de arquivo não padrão para o banco de dados do site não está disponível ao especificar um cluster do SQL Server.  

-   **Provedor de SMS:**  

    -   Não há suporte para a instalação de uma instância do Provedor de SMS em um cluster do SQL Server ou em um computador que seja executado como um nó clusterizado do SQL Server.  

-   **Opções de replicação de dados:**  

    -   Se você usar **Exibições Distribuídas**, não poderá usar um cluster do SQL Server para hospedar o banco de dados do site.  

-   **Backup e recuperação:**  

    -   O Configuration Manager não dá suporte ao backup do DPM (Data Protection Manager) para um cluster do SQL Server que usa uma instância nomeada. No entanto, ele dá suporte a backup do DPM em um cluster do SQL Server que usa a instância padrão do SQL Server.  

## <a name="prepare-a-clustered-sql-server-instance-for-the-site-database"></a>Preparar uma instância clusterizada do SQL Server para o banco de dados do site  

Aqui estão as principais tarefas executadas para preparar o banco de dados do site:

-   Crie o cluster virtual do SQL Server para hospedar o banco de dados do site em um ambiente de cluster existente do Windows Server. Para ver as etapas específicas de instalação e configuração de um cluster do SQL Server, consulte a documentação específica referente à sua versão do SQL Server. Por exemplo, se você estiver usando o SQL Server 2008 R2, consulte [Installing a SQL Server 2008 R2 Failover Cluster (Instalando um cluster de failover do SQL Server 2008 R2)](http://go.microsoft.com/fwlink/p/?LinkId=240231).  

-   Em cada computador do cluster do SQL Server, você pode colocar um arquivo na pasta raiz de cada unidade na qual você não deseja que o Configuration Manager instale componentes do site. O arquivo deve ser nomeado **NO_SMS_ON_DRIVE.SMS**. Por padrão, o Configuration Manager instala alguns componentes em cada nó físico para dar suporte a operações como backup.  

-   Adicione a conta do computador do servidor de site ao grupo **Administradores Locais** de cada computador do nó do cluster do Windows Server.  

-   Na instância virtual do SQL Server, atribua a função **sysadmin** do SQL Server à conta de usuário que executará a instalação do Configuration Manager.  

### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>Para instalar um novo site usando um SQL Server clusterizado  
 Para instalar um site que usa um banco de dados do site em cluster, execute a instalação do Configuration Manager seguindo o processo normal para instalar um site com a seguinte alteração:  

-   Na página **Informações do Banco de Dados** , especifique o nome da instância do cluster virtual do SQL Server que hospedará o banco de dados do site. A instância virtual substitui o nome do computador que executa o SQL Server.  

    > [!IMPORTANT]  
    >  Ao digitar o nome da instância do cluster virtual do SQL Server, não digite o nome do Windows Server virtual criado pelo cluster do Windows Server. Se você usar o nome do Windows Server virtual, o banco de dados do site será instalado no disco rígido local do nó de cluster do Windows Server ativo. Isso impedirá um failover bem-sucedido se esse nó falhar.  
