---
title: Configurar grupos de disponibilidade | Microsoft Docs
description: Configurar e gerenciar grupos de disponibilidade AlwaysOn do SQL Server com o SCCM.
ms.custom: na
ms.date: 5/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dc221ddf547c43ab1f25ff83c3c9bb603297ece6
ms.openlocfilehash: 138834b6cc64332202256961ad1d2f5ab6d176db
ms.contentlocale: pt-br
ms.lasthandoff: 06/01/2017


---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>Configurar grupos de disponibilidade AlwaysOn do SQL Server para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as informações neste tópico para configurar e gerenciar os grupos de disponibilidade que você usa com o Configuration Manager.

Antes de começar:  
-   Conheça as informações em [Preparar para usar grupos de disponibilidade AlwaysOn do SQL Server com o Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).
-   Familiarize-se com a documentação do SQL Server que abrange o uso dos grupos de disponibilidade e os procedimentos relacionados que são necessários para concluir os cenários a seguir.

> [!TIP]  
>  Os links deste tópico para o SQL Server estão no conteúdo para o SQL Server 2016. Se você não usar essa versão do SQL Server, veja a documentação para a versão que você usa.

## <a name="create-and-configure-an-availability-group"></a>Criar e configurar um grupo de disponibilidade
Use o procedimento a seguir para criar um grupo de disponibilidade e, em seguida, mova uma cópia do banco de dados do site para esse grupo de disponibilidade.

Para concluir este procedimento, a conta usada deverá ser:
-   Um membro do grupo **Administradores Locais** em cada computador que estará no grupo de disponibilidade.
-   Um **sysadmin** em cada instância do SQL Server que hospedará o banco de dados do site.

### <a name="to-create-and-configure-an-availability-group-for-configuration-manager"></a>Para criar e configurar um grupo de disponibilidade para o Configuration Manager  
1.    Use o seguinte comando para parar o site do Configuration Manager: **Preinst.exe /stopsite**. Para saber mais sobre como usar o Preinst.exe, confira [Ferramenta de manutenção de hierarquia](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

2.    Altere o modelo de backup do banco de dados do site de **SIMPLES** para **COMPLETO**.
Confira [Exibir ou alterar o modelo de recuperação de um banco de dados](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) na documentação do SQL Server. (Grupos de disponibilidade são compatíveis apenas com COMPLETO.)

3.    Use o SQL Server para criar um backup completo do seu banco de dados do site e, em seguida, siga um destes procedimentos, dependendo se o servidor que hospeda seu banco de dados do site será um membro de réplica do novo grupo de disponibilidade ou não:
    -   **Será membro de seu grupo de disponibilidade:**  
        Se você usar esse servidor como o membro de réplica primária inicial do grupo de disponibilidade, não precisará restaurar uma cópia do banco de dados do site para este ou outro servidor no grupo. O banco de dados já estará em vigor na réplica primária e o SQL Server replicará o banco de dados para as réplicas secundárias durante uma etapa posterior.  

      -    **Não será um membro do grupo de disponibilidade:**   
    Você deve restaurar uma cópia do banco de dados do site para o servidor que hospedará a réplica primária do grupo.

    Para obter informações sobre como concluir essa etapa, confira [Criar um backup completo de banco de dados](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) e [Restaurar um backup de banco de dados usando SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)na documentação do SQL Server.

4.    No servidor que hospedará a réplica primária inicial do grupo, use o [Assistente para Novo Grupo de Disponibilidade](/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio) para criar o grupo de disponibilidade. No assistente:
      -    Na página **Selecionar Banco de Dados**, escolha o banco de dados para o site do Configuration Manager.  

      -    Na página **Especificar Réplicas** , configure:
          -    **Réplicas**: especifique os servidores que hospedarão réplicas secundárias.

          -    **Ouvinte**: especifique o **Nome DNS do Ouvinte** como um nome DNS completo, como **&lt;Listener_Server>.fabrikam.com**. Ele é usado quando você configura o Configuration Manager para usar o banco de dados do site no grupo de disponibilidade.

      -    Na página **Selecionar Sincronização de Dados Inicial** , escolha **Completa**. Depois que o assistente cria o grupo de disponibilidade, o assistente fará backup do log de transações e do banco de dados primário, além de restaurá-los em cada servidor que hospeda uma réplica secundária. (Se você não usar essa etapa, será preciso restaurar uma cópia do banco de dados do site em cada servidor que hospeda uma réplica secundária e unir manualmente esse banco de dados ao grupo.)   

5.    Verifique a configuração em cada réplica:   
  1.    Verifique se a conta de computador do servidor do site é um membro do grupo **Administradores Locais** em cada computador que seja um membro do grupo de disponibilidade.  

  2.  Execute o [script de verificação](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites) dos pré-requisitos para confirmar se o banco de dados do site em cada réplica está configurado corretamente.

  3.    Se for necessário definir as configurações em réplicas secundárias, você deverá realizar o failover manualmente da réplica primária para a réplica secundária antes de continuar porque você só pode configurar o banco de dados de uma réplica primária. Para saber mais, veja [Executar um failover manual planejado de um grupo de disponibilidade](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) na documentação do SQL Server.

6.    Depois que todas as réplicas atenderem aos requisitos, o grupo de disponibilidade estará pronto para ser usado com o Configuration Manager.

## <a name="configure-a-site-to-use-the-database-in-the-availability-group"></a>Configurar um site para usar o banco de dados do site no grupo de disponibilidade
Depois que você [criar e configurar o grupo de disponibilidade](#create-and-configure-an-availability-group), use a manutenção de site do Configuration Manager para configurar o site para usar o banco de dados que é hospedado pelo grupo de disponibilidade.

Não há suporte para instalar um novo site com o seu banco de dados em um grupo de disponibilidade. Por exemplo, se você usar a mídia de 1702 de linha de base, deverá instalar o site usando uma única instância do SQL Server. Depois de instalar o site, você poderá mover o banco de dados do site para o grupo de disponibilidade.

Para concluir este procedimento, a conta usada para executar a instalação do Configuration Manager deverá ser:
-   Um membro do grupo **Administradores Locais** em cada computador que seja um membro do grupo de disponibilidade.
-   Um **sysadmin** em cada instância do SQL Server que hospeda o banco de dados do site.

> [!IMPORTANT]
> Quando você usa o Microsoft Intune com o Configuration Manager em uma configuração híbrida, a movimentação do banco de dados do site para ou de um grupo de disponibilidade aciona uma ressincronização dos dados com a nuvem. Isso não pode ser evitado.

### <a name="to-configure-a-site-to-use-the-availability-group"></a>Para configurar um site para usar o grupo de disponibilidade
1.    Execute a **Instalação do Configuration Manager** na **&lt;*pasta de instalação do site do Configuration Manager*>\BIN\X64\setup.exe**.

2.    Na página **Introdução** , selecione **Realizar a manutenção do site ou redefinir este site**e clique em **Próximo**.

3.    Escolha a opção **Modificar configuração do SQL Server** e clique em **Avançar**.

4.    Reconfigure o seguinte para o banco de dados do site:
    -   **Nome do SQL Server:** insira o nome virtual do **ouvinte** do grupo de disponibilidade configurado ao criar o grupo de disponibilidade. O nome virtual deve ser um nome DNS completo, como **&lt;*servidorDoPontoDeExtremidade*>.fabrikam.com**.  

    -   **Instância:** esse valor deve estar em branco para especificação da instância padrão do *ouvinte* do grupo de disponibilidade. Se o banco de dados do site atual estiver instalado em uma instância nomeada, esta será listada e deverá ser apagada.

    -   **Banco de Dados:** deixe o nome como ele aparece. Esse é o nome do banco de dados do site atual.

5.    Depois de fornecer as informações do novo local do banco de dados, conclua a Instalação com o processo e as configurações normais.



## <a name="add-and-remove-replica-members"></a>Adicionar e remover membros de réplica  
Quando o banco de dados do site está hospedado em um grupo de disponibilidade, use os procedimentos a seguir para adicionar ou remover membros de réplica. O Configuration Manager dá suporte a um único primário e até dois nós secundários.

Para concluir os seguintes procedimentos, a conta usada deverá ser:
-   Um membro do grupo **Administradores Locais** em cada computador que seja um membro do grupo de disponibilidade.
-   Um **sysadmin** em cada SQL Server que hospeda ou hospedará o banco de dados do site.


### <a name="to-add-a-new-replica-member"></a>Para adicionar um novo membro de réplica
1.    Adicione o novo servidor como uma réplica secundária ao grupo de disponibilidade. Confira [Adicionar uma réplica secundária a um grupo de disponibilidade (SQL Server)](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server)na biblioteca de documentação do SQL Server.

2.    Pare o site do Configuration Manager executando **Preinst.exe /stopsite**. Veja [Ferramenta de manutenção de hierarquia](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

3.    Use o SQL Server para criar um backup do banco de dados do site da réplica primária e, em seguida, restaure esse backup no novo servidor de réplica secundária. Confira [Criar um backup completo de banco de dados](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) e [Restaurar um backup de banco de dados usando SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)na documentação do SQL Server.

4.    Configure cada réplica secundária. Execute as seguintes ações em cada réplica secundária no grupo de disponibilidade:

    1.    Verifique se a conta de computador do servidor do site é um membro do grupo **Administradores Locais** em cada computador que seja um membro do grupo de disponibilidade.

    2.    Execute o [script de verificação](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites) dos pré-requisitos para confirmar se o banco de dados do site em cada réplica está configurado corretamente.

    3.    Se for necessário configurar a nova réplica, faça o failover manual da réplica primária para a nova réplica secundária e, em seguida, verifique as configurações necessárias. Confira [Executar um failover manual planejado de um grupo de disponibilidade](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) na documentação do SQL Server.

5.    Reinicie o site iniciando os serviços Gerenciador de Componentes de Site (**sitecomp**) e **SMS_Executive** .

### <a name="to-remove-a-replica-member"></a>Para remover um membro de réplica
Para este procedimento, use as informações em [Remover uma réplica secundária de um grupo de disponibilidade](/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server) na documentação do SQL Server.

## <a name="stop-using-an-availability-group"></a>Parar de usar um grupo de disponibilidade
Use o procedimento a seguir quando você não quiser mais hospedar o banco de dados do site em um grupo de disponibilidade. Isso envolve a mudança do banco de dados do site novamente para uma única instância do SQL Server.

Para concluir este procedimento, a conta usada deverá ser:
-   Um membro do grupo **Administradores Locais** em cada computador que seja um membro do grupo de disponibilidade
-   Um **sysadmin** em cada instância do SQL Server que hospeda o banco de dados do site.

> [!IMPORTANT]  
> Quando você usa o Microsoft Intune com o Configuration Manager em uma configuração híbrida, a movimentação do banco de dados do site para ou de um grupo de disponibilidade aciona uma ressincronização dos dados com a nuvem. Isso não pode ser evitado.

### <a name="to-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a>Para mover o banco de dados do site de um grupo de disponibilidade de volta para um SQL Server de única instância
1.    Pare o site do Configuration Manager usando o seguinte comando: **Preinst.exe /stopsite**. Para saber mais, veja [Ferramenta de manutenção de hierarquia](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

2.    Use o SQL Server para criar um backup completo do seu banco de dados do site da réplica primária. Para obter informações sobre como concluir essa etapa, confira [Criar um backup completo de banco de dados](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) na documentação do SQL Server.

3.    Se o servidor que é a réplica primária para o grupo de disponibilidade for hospedar a instância única do banco de dados do site, você poderá ignorar essa etapa:  

    -   Use o SQL Server para restaurar o backup do banco de dados do site no servidor que hospedará o banco de dados do site. Confira [Restaurar um backup de banco de dados usando SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms) na documentação do SQL Server.   <br />  <br />

4.    No servidor que hospedará o banco de dados do site (a réplica primária ou o servidor onde você restaurou o banco de dados do site), altere o modelo de backup para o banco de dados do site de **COMPLETO** para **SIMPLES**. Confira [Exibir ou alterar o modelo de recuperação de um banco de dados](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) na documentação do SQL Server.  

5.    Execute a **Instalação do Configuration Manager** na **&lt;*pasta de instalação do site do Configuration Manager>*\BIN\X64\setup.exe**.

6.    Na página **Introdução** , selecione **Realizar a manutenção do site ou redefinir este site**e clique em **Próximo**.  

7.    Escolha a opção **Modificar configuração do SQL Server** e clique em **Avançar**.  

8.    Reconfigure o seguinte para o banco de dados do site:
    -   **Nome do SQL Server:** insira o nome do servidor que agora hospeda o banco de dados do site.

    -   **Instância:** especifique a instância nomeada que hospeda o banco de dados do site ou deixe em branco se o banco de dados estiver na instância padrão.

    -   **Banco de Dados:** deixe o nome como ele aparece. Esse é o nome do banco de dados do site atual.    

9.    Depois de fornecer as informações do novo local do banco de dados, conclua a Instalação com o processo e as configurações normais. Quando a Instalação é concluída, o site reinicia e começa a usar o novo local do banco de dados.    

10.    Para limpar os servidores que eram membros do grupo de disponibilidade, siga as orientações em [Remover um grupo de disponibilidade](/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server) na documentação do SQL Server.

