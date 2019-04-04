---
title: Cluster do SQL Server
titleSuffix: Configuration Manager
description: Usar um cluster do SQL Server para hospedar o banco de dados do site do Configuration Manager
ms.date: 03/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d07005c63f0d69d57d24eac163b67c34529658cf
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58477544"
---
# <a name="use-a-sql-server-cluster-for-the-site-database"></a>Usar um cluster do SQL Server para hospedar o banco de dados do site

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode usar um cluster de failover do SQL Server para hospedar o banco de dados do site do Configuration Manager. Um cluster oferece suporte para failover e aumenta a confiabilidade do banco de dados do site. No entanto, ele não fornece processamento adicional nem benefícios de balanceamento de carga. Além disso, um cluster de Failover do SQL Server usa o armazenamento compartilhado e introduz um ponto único de falha. Pode ocorrer degradação no desempenho, uma vez que o servidor do site deve localizar o nó ativo do cluster do SQL Server, antes de se conectar ao banco de dados do site.  

> [!IMPORTANT]  
> A configuração bem-sucedida dos clusters do SQL Server se baseia na documentação e nos procedimentos fornecidos na biblioteca de documentação do SQL Server.  


Antes de instalar o Configuration Manager, prepare o cluster do SQL Server para dar suporte a ele. Para saber mais, confira [Preparar uma instância clusterizada do SQL Server](#bkmk_prepare).

Durante a instalação do Configuration Manager, o gravador Serviço de Cópias de Sombra de Volume do Windows será instalado em cada nó do computador físico do cluster do Microsoft Windows Server. Este serviço tem suporte para a tarefa de manutenção **Servidor do Site de Backup**.  

Depois de instalar o site, o Configuration Manager verifica se há alterações para o nó de cluster a cada hora. O Configuration Manager gerencia automaticamente as alterações encontradas que afetam as instalações de componentes. Por exemplo, um failover de nó ou a adição de um novo nó ao cluster do SQL Server.  



## <a name="supported-options"></a>Opções com suporte

As opções a seguir têm suporte para clusters de failover do SQL Server usados como o banco de dados do site:

- Um cluster de instância única  

- Configurações com várias instâncias  

- Vários nós ativos  

- Uma instância nomeada ou uma padrão  



## <a name="prerequisites"></a>Pré-requisitos

Lembre-se dos seguintes pré-requisitos:  

- O banco de dados do site deve ser remoto do servidor do site. O cluster não pode incluir o servidor do sistema de sites.  

    > [!Note]  
    > Da versão 1810 em diante, o processo de instalação do Configuration Manager não bloqueia mais a instalação da função de servidor de site em um computador com a função do Windows para clustering de failover. Anteriormente, não era possível colocar o banco de dados do site no servidor do site. Com esta alteração, é possível criar um site altamente disponível com menos servidores usando o cluster do SQL e um servidor do site no modo passivo. Para obter mais informações, confira [Opções de alta disponibilidade](/sccm/core/servers/deploy/configure/high-availability-options). <!--3607761, fka 1359132-->  

- Adicione a conta do computador do servidor do site ao grupo **Administradores** local de cada servidor no cluster.  

- Para fornecer suporte a autenticação Kerberos, habilite o protocolo de comunicação de rede **TCP/IP** para a conexão de rede de cada nó de cluster do SQL Server. O protocolo **Pipes Nomeados** não é necessário, mas ele pode ser usado para solucionar problemas de autenticação Kerberos. As definições de protocolo de rede são configuradas no **SQL Server Configuration Manager** em **Configuração de Rede do SQL Server**.  

- Se você usa uma PKI (infraestrutura de chave pública), confira [Requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements). Há requisitos específicos de certificado para o uso de um cluster do SQL Server, no banco de dados do site.  



## <a name="limitations"></a>Limitações

Considere as seguintes limitações:  


### <a name="installation-and-configuration"></a>Instalação e configuração

- Sites secundários não podem usar um cluster do SQL Server.  

- A opção de especificar locais de arquivo não padrão para o banco de dados do site não está disponível ao especificar um cluster do SQL Server.  


### <a name="sms-provider"></a>Provedor de SMS

Não é possível instalar uma instância do Provedor de SMS em um cluster do SQL Server. Além disso, ele não tem suporte em computadores executados como um nó clusterizado do SQL Server.  


### <a name="data-replication-options"></a>Opções de replicação de dados

Se você usa **Exibições Distribuídas**, então não é possível usar um cluster do SQL Server para hospedar o banco de dados do site.  


### <a name="backup-and-recovery"></a>Backup e descoberta

O Configuration Manager não é compatível com o backup do DPM (Data Protection Manager) para um cluster do SQL Server que usa uma instância nomeada. Ele é compatível com backup de DPM em um cluster do SQL Server que use a instância padrão do SQL Server.  



## <a name="bkmk_prepare"></a> Preparar uma instância clusterizada do SQL Server  

Aqui estão as principais tarefas para preparar o banco de dados do site:

- Crie o cluster virtual do SQL Server para hospedar o banco de dados do site em um ambiente de cluster existente do Windows Server. Para ver as etapas específicas de instalação e configuração de um cluster do SQL Server, consulte a documentação específica referente à sua versão do SQL Server. Para saber mais, confira [Criar um novo cluster de failover do SQL Server](https://docs.microsoft.com/sql/sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup?view=sql-server-2017).  

- Em cada computador no cluster do SQL Server, coloque um arquivo na pasta raiz de cada unidade em que você não deseja que o Configuration Manager instale componentes do site. Atribua um nome ao arquivo `NO_SMS_ON_DRIVE.SMS`. Por padrão, o Configuration Manager instala alguns componentes em cada nó físico para dar suporte a operações como backup.  

- Adicione a conta do computador do servidor do site ao grupo **Administradores** local de cada computador do nó do cluster do Windows Server.  

- Na instância virtual do SQL Server, atribua a função **sysadmin** do SQL Server à conta de usuário que executa a instalação do Configuration Manager.  


### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>Para instalar um novo site usando um SQL Server clusterizado  

Para instalar um site que usa um banco de dados do site em cluster, execute a instalação do Configuration Manager seguindo o processo normal para instalar um site com a seguinte alteração:  

- Na página **Informações do Banco de Dados** , especifique o nome da instância do cluster virtual do SQL Server que hospedará o banco de dados do site. A instância virtual substitui o nome do computador que executa o SQL Server.  

    > [!IMPORTANT]  
    > Não digite o nome do Windows Server virtual criado pelo cluster do Windows Server, quando digitar o nome da instância do cluster virtual do SQL Server. Se você usar o nome do Windows Server virtual, o banco de dados do site será instalado no disco rígido local do nó de cluster do Windows Server ativo. Isso impedirá um failover bem-sucedido se esse nó falhar.  
