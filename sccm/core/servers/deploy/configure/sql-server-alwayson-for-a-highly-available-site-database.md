---
title: SQL Server AlwaysOn | Microsoft Docs
ms.custom: na
ms.date: 1/4/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
caps.latest.revision: 16
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: aaaab003ddd22f18160d4be63cfeab3a7e7f6b03
ms.lasthandoff: 03/27/2017


---
# <a name="sql-server-alwayson-for-a-highly-available-site-database-for-system-center-configuration-manager"></a>AlwaysOn do SQL Server para um banco de dados do site altamente disponível do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


 Começando na versão 1602 do System Center Configuration Manager, você pode usar [Grupos de Disponibilidade AlwaysOn](https://msdn.microsoft.com/library/hh510230\(v=sql.120\).aspx) do SQL Server para hospedar o banco de dados do site em sites primários e o site de administração central como uma solução de alta disponibilidade e de recuperação de desastres. O grupo de disponibilidade pode ser hospedado no local ou no Microsoft Azure.  

 Ao usar o Microsoft Azure para hospedar o grupo de disponibilidade, você pode aumentar ainda mais a disponibilidade do seu banco de dados do site usando os Grupos de Disponibilidade AlwaysOn do SQL Server com Conjuntos de Disponibilidade do Azure. Para obter mais informações sobre os Conjuntos de Disponibilidade do Azure, consulte [Gerenciar a disponibilidade de máquinas virtuais](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).  

 O Configuration Manager dá suporte à hospedagem de banco de dados do site em um Grupo de Disponibilidade do SQL que está por trás de um Balanceador de Carga Interno ou Externo. Além de configurar as exceções de firewall em cada réplica, você precisará adicionar regras de balanceamento de carga para as seguintes portas:
  - SQL sobre TCP: TCP 1433
  - SQL Server Service Broker: TCP 4022
  - Protocolo SMB: TCP 445
  - Mapeador de ponto de extremidade RPC: TCP 135


Veja a seguir cenários que têm suporte para os grupos de disponibilidade:  

-   Você pode mover o banco de dados do site para a instância padrão de um grupo de disponibilidade  

-   Você pode adicionar ou remover membros de réplica de um grupo de disponibilidade que hospeda um banco de dados do site  

-   Você pode mover o banco de dados do site de um grupo de disponibilidade para uma instância padrão ou nomeada de um SQL Server autônomo  

> [!Important]  
> Quando você usa o Microsoft Intune com o Configuration Manager em uma configuração híbrida, a movimentação do banco de dados do site para ou de um grupo de disponibilidade aciona uma ressincronização dos dados com a nuvem. Isso não pode ser evitado. 



> [!NOTE]  
>  A configuração bem-sucedida e o uso de grupos de disponibilidade exigem que você esteja familiarizado com a configuração do SQL Server e de grupos de disponibilidade do SQL Server. Os procedimentos do System Center Configuration Manager neste tópico se baseiam na documentação e nos procedimentos adicionais encontrados na biblioteca de documentação do SQL Server.  

 **Problemas conhecidos ao usar grupos de disponibilidade do AlwaysOn com o Configuration Manager:**  

-   **Todos os servidores de réplica exigem um caminho de arquivo idêntico no momento em que você define o Configuration Manager para usar o grupo de disponibilidade:**  

    -   Quando você executa a Instalação do Configuration Manager para redirecionar o site para usar o banco de dados em um grupo de disponibilidade, cada servidor de réplica secundária no grupo deve ter um caminho de arquivo idêntico ao caminho do arquivo usado para hospedar os arquivos de banco de dados do site na réplica primária atual. Se não existir um caminho idêntico nas réplicas secundárias, a Instalação não adicionará a instância dos grupos de disponibilidade como o novo local do banco de dados do site.  

         Além disso, em cada servidor de réplica secundária, a conta de serviço local do SQL Server deve ter permissão de **Controle Total** para essa pasta.  

         Os servidores de réplica secundária exigem esse caminho de arquivo apenas enquanto você estiver usando a Instalação para especificar a instância do banco de dados no grupo de disponibilidade.  Depois que a Instalação concluir a alteração para usar o banco de dados do site no grupo de disponibilidade, você poderá excluir o caminho não utilizado dos servidores de réplica secundária.  

         Por exemplo, considere o seguinte cenário:  

        -   Você cria um grupo de disponibilidade que usa três SQL Servers  

        -   Seu servidor de réplica primária é uma nova instalação do SQL Server 2014.  Por padrão, os arquivos .MDF e .LDF do banco de dados são armazenados em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA  

        -   Ambos os servidores de réplica secundária foram atualizados para o SQL Server 2014 de versões anteriores e mantêm o caminho de arquivo original para armazenar arquivos de banco de dados: C:\Arquivos de Programas\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA  

        -   Antes de tentar mover o banco de dados do site para esse grupo de disponibilidade, em cada servidor de réplica secundária você deve criar o seguinte caminho de arquivo, mesmo que as réplicas secundárias não vão usar esse local de arquivo: C:\Arquivos de Programas\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA (esta é uma duplicata do caminho que está em uso na réplica primária)  

        -   Depois, conceda à conta de serviço do SQL Server em cada réplica secundária acesso de controle total para o local do arquivo criado recentemente no servidor  

        -   Agora, você pode executar com êxito a Instalação do Configuration Manager para instruir o site a usar o banco de dados no grupo de disponibilidade  

-   **Quando a Instalação é executada para instruir o banco de dados do site a usar o grupo de disponibilidade, erros semelhantes ao seguinte podem ser registrados em ConfigMgrSetup.log:**  

    -   ERRO: Erro do SQL Server: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Falha ao atualizar o banco de dados "CM_AAA" porque ele é somente leitura.   Instalação do Configuration Manager 1/21/2016 4:54:59 PM  7344 (0x1CB0)  

     Esses erros são registrados quando a Instalação tenta processar funções de banco de dados em réplicas secundárias do grupo de disponibilidade. Esses erros podem ser ignorados com segurança.
- **Servidores SQL que hospedam os grupos de disponibilidade adicional:**

  Antes de instalar a versão 1610, quando você usa um grupo de disponibilidade e, em seguida, executa a instalação do Configuration Manager ou instala uma atualização para o Configuration Manager, cada réplica em cada grupo de disponibilidade adicional no SQL Server que hospeda o grupo de disponibilidade do Configuration Manager deve ter as seguintes configurações:
    - **Failover Manual**
    - **permitir qualquer conexão somente leitura**


##  <a name="bkmk_BnR"></a> Alterações de backup e recuperação quando você usa um grupo de disponibilidade AlwaysOn do SQL Server  
 **Backup:**  

 Quando um banco de dados do site é executado em um grupo de disponibilidade, você deve continuar executando a tarefa de manutenção interna do servidor **Site de Backup** para fazer backup de configurações e arquivos comuns do Configuration Manager, mas planeje não usar os arquivos .MDF ou .LDF criados por esse backup. Em vez disso, planeje fazer backups diretos do banco de dados do site usando o SQL Server.  

 Além disso, como o modelo de recuperação do banco de dados é definido como completo, você deve planejar monitorar e manter o tamanho do log de transações do banco de dados do site.  No modelo de recuperação completo, as transações não são protegidas até que um backup completo do banco de dados ou o log de transações seja feito. Um modelo de recuperação completo é um requisito para usar o banco de dados do site em um grupo de disponibilidade e é definido quando você configura o grupo para uso com o Configuration Manager. Para obter mais informações sobre backup e restauração do SQL Server, confira [Fazer backup e restaurar bancos de dados do SQL Server](https://msdn.microsoft.com/library/ms187048\(v=sql.120\).aspx) na documentação do SQL Server.  

 **Recuperação:**  

 Durante uma recuperação de site, desde que um nó do grupo de disponibilidade permaneça funcionando, você poderá usar a opção de recuperação de site **Ignorar recuperação de banco de dados (Use esta opção se o banco de dados do site não tiver sido afetado)**.  

 No entanto, se todos os nós de um grupo de disponibilidade tiverem sido perdidos, antes de recuperar o site, será preciso recriar o grupo de disponibilidade (o System Center Configuration Manager não pode recriar nem restaurar o nó de disponibilidade).  Depois que o grupo tiver sido recriado com um backup restaurado e reconfigurado, você poderá usar a opção de recuperação de site **Ignorar recuperação de banco de dados (Use esta opção se o banco de dados do site não tiver sido afetado)**.  

 Para obter mais informações sobre backup e recuperação, consulte [Backup e recuperação para o System Center Configuration Manager](../../../../protect/understand/backup-and-recovery.md).  

##  <a name="bkmk_create"></a> Configurar um grupo de disponibilidade para uso com o Configuration Manager  
 Antes de iniciar o procedimento a seguir, familiarize-se com os procedimentos do SQL Server necessários para concluir essa configuração e com os seguintes detalhes que se aplicam aos grupos de disponibilidade que você configura para uso com o Configuration Manager.  

 **Requisitos para os grupos de disponibilidade AlwaysOn que você usa com o System Center Configuration Manager:**  

-  *Versão*: cada nó (ou réplica) no grupo de disponibilidade deve executar uma versão do SQL Server com suporte no System Center Configuration Manager. Se houver suporte no SQL Server, nós diferentes do grupo de disponibilidade poderão executar versões diferentes do SQL Server.   

- *Edição*: é necessário usar uma Enterprise Edition do SQL Server.  O SQL Server 2016 Standard Edition introduz grupos de disponibilidade Básicos, que não têm suporte no Configuration Manager.


-   O grupo de disponibilidade deve ter uma réplica primária e pode ter até duas réplicas secundárias síncronas.  

-  Depois de adicionar um banco de dados a um grupo de disponibilidade, você deve fazer o failover da réplica primária para uma secundária (fazendo dela a nova réplica primária) e, em seguida, configurar o banco de dados com o seguinte:
    - Enable Trustworthy: igual a True
    - Enable the Service Broker: igual a True
    - Set the dbowner: igual a SA

    Você pode executar o script a seguir para definir essas configurações, em que cm_ABC é o nome do seu banco de dados do site:  

    >     Mestre USE  
    >     ALTER DATABASE cm_ABC SET NEW_BROKER   
    >     ALTER DATABASE cm_ABC SET ENABLE_BROKER  
    >     ALTER DATABASE cm_ABC SET TRUSTWORTHY ON;  
    >     USE cm_ABC  
    >     EXEC sp_changedbowner 'sa'  
    >     Exec sp_configure 'max text repl size (B)', reconfigurar 2147483647



-   O grupo de disponibilidade deve ter pelo menos um **ouvinte do grupo de disponibilidade**.  O nome virtual desse ouvinte é usado quando você configura o Configuration Manager para usar o banco de dados do site no grupo de disponibilidade. Embora um grupo de disponibilidade possa conter vários ouvintes, o Configuration Manager pode usar apenas um  

-   Cada réplica primária e secundária deve:  
    - Ser definida para **permitir qualquer conexão somente leitura**
    - Usar a **instância padrão**
    - Ser definida para **Failover Manual**  

        > [!TIP]  
        >  O System Center Configuration Manager dá suporte ao uso de réplicas do grupo de disponibilidade quando definidas para Failover Automático. No entanto, o Failover Manual deve ser definido quando você executa a Instalação para especificar o uso do banco de dados do site no grupo de disponibilidade e no momento em que você instala todas as atualizações no Configuration Manager (não apenas as atualizações que se aplicam ao banco de dados do site).  

  **Limitações para grupos de disponibilidade**
   - Não há suporte para grupos de disponibilidade Básicos (introduzidos com o SQL Server 2016 Standard Edition). Isso ocorre porque os grupos de disponibilidade básicos não dão suporte ao acesso de leitura de réplicas secundárias, um requisito para uso com o Configuration Manager. Para obter mais informações, consulte [Grupos de disponibilidade básicos (Grupos de Disponibilidade AlwaysOn)](https://msdn.microsoft.com/en-us/library/mt614935.aspx).

   - Há suporte para grupos de disponibilidade apenas no banco de dados do site e não no banco de dados de atualização de software nem no banco de dados de relatório.   
   - Quando usa um grupo de disponibilidade, você deve configurar manualmente o ponto de relatório para usar a réplica primária atual, e não o ouvinte do grupo de disponibilidade. Se a réplica primária fizer o failover para outra réplica, você precisará reconfigurar o ponto de relatório para usar a nova réplica primária.  
   - Antes de instalar atualizações, como a versão 1606, certifique-se de que o grupo de disponibilidade esteja definido para failover manual. Após a atualização do site, você pode restaurar o failover para que ele seja automático.



 **Permissões necessárias para configurar e usar grupos de disponibilidade:**  

-   A conta de computador do servidor do site deve ser um membro do grupo **Administradores Locais** em cada computador que seja um membro do grupo de disponibilidade.  

#### <a name="to-configure-an-availability-group-to-host-a-site-database"></a>Para configurar um grupo de disponibilidade para hospedar um banco de dados do site  

1.  Use o seguinte comando para parar o site do Configuration Manager:  
     **Preinst.exe /stopsite**  

     Para obter mais informações sobre o uso de Preinst.exe, consulte [Ferramenta de Manutenção de Hierarquia (Preinst.exe) para o System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

2.  Altere o modelo de backup do banco de dados do site de **SIMPLES** para **COMPLETO**.  

     Confira [Exibir ou alterar o modelo de recuperação de um banco de dados](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx) na documentação do SQL Server. (Grupos de disponibilidade são compatíveis apenas com COMPLETO.)  

3.  No servidor que hospedará a réplica primária do grupo, use o **Assistente para Novo Grupo de Disponibilidade** para criar o grupo de disponibilidade. No assistente:  

    -   Na página **Selecionar Banco de Dados**, escolha o banco de dados para o site do Configuration Manager  

    -   Na página **Especificar Réplicas** , configure:  

        -   **Réplicas**: especifique os servidores que hospedarão réplicas secundárias  

        -   **Ouvinte**: especifique o **Nome DNS do Ouvinte** como um nome DNS completo, como **&lt;Listener_Server >.fabrikam.com**. Ele é usado quando você configura o Configuration Manager para usar o banco de dados do site no grupo de disponibilidade.

    -   Na página **Selecionar Sincronização de Dados Inicial** , escolha **Completa**. Depois que o assistente cria o grupo de disponibilidade, o assistente fará backup do log de transações e do banco de dados primário, além de restaurá-los em cada servidor que hospeda uma réplica secundária. Se você não usar essa etapa, será preciso restaurar uma cópia do banco de dados do site em cada servidor que hospeda uma réplica secundária e unir manualmente esse banco de dados ao grupo.  

    Para mais informações, confira [Usar a caixa de diálogo Assistente de Grupo de Disponibilidade](https://msdn.microsoft.com/library/hh403415\(v=sql.120\).aspx) na documentação do SQL Server.  

4.  Depois que o grupo de disponibilidade for configurado, configure o banco de dados do site na réplica primária com a propriedade **TRUSTWORTHY** e **habilite a integração CLR**. Para obter informações sobre como configurá-los, confira [Propriedade de banco de dados TRUSTWORTHY](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx) e  [Habilitando integração CLR](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx) na documentação do SQL Server.  

5.  Execute as seguintes ações para configurar cada réplica secundária no grupo de disponibilidade:  

    1.  Faça failover manualmente da réplica primária atual em uma réplica secundária. Confira [Executar um failover manual planejado de um grupo de disponibilidade](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) na documentação do SQL Server.  

    2.  Configure o banco de dados na nova réplica primária com a propriedade **TRUSTWORTHY** e **habilite a integração CLR**.  

6.  Depois que todas as réplicas forem promovidas para réplicas primárias e os bancos de dados configurados, o grupo de disponibilidade estará pronto para ser usado com o Configuration Manager.  





##  <a name="bkmk_direct"></a> Mover um banco de dados do site para um grupo de disponibilidade  
 Você pode mover um banco de dados de um site instalado anteriormente para um grupo de disponibilidade. Primeiro, você deve criar o grupo de disponibilidade e, depois, configurar o banco de dados para operação no grupo de disponibilidade.  

 Para concluir esse procedimento, a conta de usuário que executa a Instalação do Configuration Manager deve ser um membro do grupo **Administradores Locais** em cada computador que é um membro do grupo de disponibilidade.  

#### <a name="to-move-a-site-database-to-an-availability-group"></a>Para mover um banco de dados do site para um grupo de disponibilidade  

1.  Execute a **Instalação do Configuration Manager** na **&lt;pasta de instalação do site do Configuration Manager\>\BIN\X64\setup.exe**.  

2.  Na página **Introdução** , selecione **Realizar a manutenção do site ou redefinir este site**e clique em **Próximo**.  

3.  Escolha a opção **Modificar configuração do SQL Server** e clique em **Avançar**.  

4.  Reconfigure o seguinte para o banco de dados do site:  

    -   **Nome do SQL Server:** insira o nome virtual do ouvinte do grupo de disponibilidade configurado ao criar o grupo de disponibilidade. O nome virtual deve ser um nome DNS completo, como **&lt;Servidor do ponto de extremidade\>.fabrikam.com**  

    -   **Instância:** esse valor deve estar em branco para especificar a instância padrão do ouvinte do grupo de disponibilidade.  Se o banco de dados do site atual estiver instalado em uma instância nomeada, esta será listada e deverá ser apagada  

    -   **Banco de Dados:** deixe o nome como ele aparece. Esse é o nome do banco de dados do site atual.  

5.  Depois de fornecer as informações do novo local do banco de dados, conclua a Instalação com o processo e as configurações normais.  

##  <a name="bkmk_change"></a> Adicionar ou remover membros de um grupo de disponibilidade ativo  
 Depois que o Configuration Manager estiver usando um banco de dados do site hospedado em um grupo de disponibilidade, você poderá remover um membro de réplica ou incluir um membro de réplica adicional (não exceda um nó primário e dois nós secundários).  

#### <a name="to-add-a-new-replica-member"></a>Para adicionar um novo membro de réplica  

1.  Adicione o novo servidor como uma réplica secundária ao grupo de disponibilidade. Confira  [Adicionar uma réplica secundária a um grupo de disponibilidade (SQL Server)](https://msdn.microsoft.com/library/hh213247\(v=sql.120\).aspx)na biblioteca de documentação do SQL Server.  

2.  Pare o site do Configuration Manager executando **Preinst.exe /stopsite** Consulte [Ferramenta de Manutenção de Hierarquia (Preinst.exe) para o System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

3.  Configure cada réplica secundária. Execute as seguintes ações em cada réplica secundária no grupo de disponibilidade:  

    1.  Faça failover manualmente da réplica primária na nova réplica secundária. Confira [Executar um failover manual planejado de um grupo de disponibilidade](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) na documentação do SQL Server.  

    2.  Configure o banco de dados no novo servidor para ser Confiável e habilite a integração CLR. Confira [Propriedade de banco de dados TRUSTWORTHY](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx) e  [Habilitando integração CLR](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx)na documentação do SQL Server.  

4.  Reinicie o site iniciando os serviços Gerenciador de Componentes de Site (**sitecomp**) e **SMS_Executive** .  

#### <a name="to-remove-a-replica-member-from-the-availability-group"></a>Para remover um membro de réplica do grupo de disponibilidade  

-   Use as informações em [Remover uma réplica secundária de um grupo de disponibilidade](https://msdn.microsoft.com/library/hh213149\(v=sql.120\).aspx) na documentação do SQL Server.  

##  <a name="bkmk_remove"></a> Mover o banco de dados do site de um grupo de disponibilidade de volta para um SQL Server de única instância  
 Use o procedimento a seguir quando você não quiser mais hospedar o banco de dados do site em um grupo de disponibilidade.  

#### <a name="to-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a>Para mover o banco de dados do site de um grupo de disponibilidade de volta para um SQL Server de única instância  

1.  Pare o site do Configuration Manager usando o seguinte comando:  
     **Preinst.exe /stopsite**.  Para obter mais informações, consulte [Ferramenta de Manutenção de Hierarquia (Preinst.exe) para o System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

2.  Use o SQL Server para criar um backup completo do seu banco de dados do site da réplica primária. Para obter informações sobre como concluir essa etapa, confira [Criar um backup completo de banco de dados](https://msdn.microsoft.com/library/ms187510\(v=sql.120\).aspx) na documentação do SQL Server.  

3.  Se o servidor que hospeda a réplica primária para o grupo de disponibilidade agora for hospedar a instância única do banco de dados do site, você poderá ignorar essa etapa:  

    -   Use o SQL Server para restaurar o backup do banco de dados do site no servidor que hospedará o banco de dados do site.  Confira [Restaurar um backup de banco de dados (SQL Server Management Studio)](https://msdn.microsoft.com/library/ms177429\(v=sql.120\).aspx) na documentação do SQL Server.  

4.  No banco de dados do site restaurado, altere o modelo de backup do banco de dados do site de **COMPLETO** para **SIMPLES**.  Confira [Exibir ou alterar o modelo de recuperação de um banco de dados](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx) na documentação do SQL Server.  

5.  Execute a **Instalação do Configuration Manager** na **&lt;pasta de instalação do site do Configuration Manager\>\BIN\X64\setup.exe**.  

6.  Na página **Introdução** , selecione **Realizar a manutenção do site ou redefinir este site**e clique em **Próximo**.  

7.  Escolha a opção **Modificar configuração do SQL Server** e clique em **Avançar**.  

8.  Reconfigure o seguinte para o banco de dados do site:  

    -   **Nome do SQL Server:** insira o nome do servidor que agora hospeda o banco de dados do site.  

    -   **Instância:** especifique a instância nomeada que hospeda o banco de dados do site ou deixe em branco se o banco de dados estiver na instância padrão.  

    -   **Banco de Dados:** deixe o nome como ele aparece. Esse é o nome do banco de dados do site atual.  

9. Depois de fornecer as informações do novo local do banco de dados, conclua a Instalação com o processo e as configurações normais. Quando a Instalação é concluída, o site reinicia e começa a usar o novo local do banco de dados.  

10. Para limpar os servidores que eram membros do grupo de disponibilidade, siga as orientações em [Remover um grupo de disponibilidade](https://msdn.microsoft.com/library/ff878113\(v=sql.120\).aspx) na documentação do SQL Server.

