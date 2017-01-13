---
title: "Operações de migração | Microsoft Docs"
description: Criar e executar trabalhos para migrar dados e clientes para o System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c28e3492-851a-40fc-ba13-67ebc2d8b41a
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5e3d3f4194b06442e34c10988a20fe9ca40ac5d7
ms.openlocfilehash: 3b5fc05542125454e224df73344cb29cb5f502ef


---
# <a name="operations-for-migrating-to-system-center-configuration-manager"></a>Operações de migração para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para migração no System Center Configuration Manager, após configurar com êxito a coleta de dados do site de origem em uma hierarquia de origem com suporte, você pode iniciar a migração de dados e clientes. Use as informações nas seções a seguir para criar e executar trabalhos de migração para migras dados e clientes e depois concluir o processo de migração.  

-   [Criar e editar trabalhos de migração](#Create_Edit_migration_Jobs)  

-   [Executar trabalhos de migração](#Run_Migration_Jobs)  

-   [Atualizar ou reatribuir um ponto de distribuição compartilhado](#BKMK_ProcUpgrdSS)  

-   [Monitorar a atividade de migração no espaço de trabalho Migração](#Monitor_MIgration)  

-   [Migrar clientes](#BKMK_MigrateClients)  

-   [Concluir migração](#Complete_Migration)  

##  <a name="a-namecreateeditmigrationjobsa-create-and-edit-migration-jobs"></a><a name="Create_Edit_migration_Jobs"></a> Criar e editar trabalhos de migração  
 Use os procedimentos a seguir para criar trabalhos de migração de dados, editar a lista de exclusões de trabalhos de migração baseados em coleção, configurar pontos de distribuição compartilhados e editar agendamentos de trabalhos de migração.  

> [!NOTE]  
>  O procedimento a seguir usado para criar um trabalho de migração que migra por coleções aplica-se somente às hierarquias de origem que executam uma versão com suporte do Configuration Manager 2007. O tipo de trabalho de migração baseado em coleção não está disponível quando você migra de uma hierarquia de origem do System Center 2012 Configuration Manager ou do System Center Configuration Manager.  

#### <a name="to-create-a-migration-job-to-migrate-by-collections"></a>Para criar um trabalho de migração para migrar por coleções  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Migração**e clique em **Trabalhos de Migração**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Trabalho de Migração**.  

4.  Na página **Geral** do Assistente para Criar Trabalho de Migração configure o seguinte e clique em **OK**:  

    -   Especifique um nome para o trabalho de migração.  

    -   Na lista suspensa **Tipo de Trabalho** , selecione **Migração da coleção**.  

5.  Na página **Selecionar Coleções** , configure o seguinte e clique em **Próximo**:  

    -   Selecione as coleções que você deseja migrar.  

    -   Se deseja migrar somente as coleções e não os objetos associados a elas, desmarque a opção **Migrar objetos associados às coleções especificadas** . Ao desmarcar essa opção, nenhum objeto associado será migrado nesse trabalho e você poderá pular as etapas 6 e 7.  

6.  Na página **Selecionar Objetos** , desmarque os tipos de objeto ou objetos disponíveis específicos que você não deseja migrar. Por padrão, todos os tipos de objeto associado e objetos disponíveis são selecionados. Clique em **Avançar**.  

7.  Na página **Propriedade de Conteúdo** , atribua a propriedade de conteúdo de cada site de origem listado a um site na hierarquia de destino e clique em **Próximo**.  

8.  Na página **Escopo de Segurança** , selecione um ou mais escopos de segurança de administração baseada em funções para atribuir aos objetos a serem migrados nesse trabalho e clique em **Próximo**.  

9. Na página **Limitação de Coleção** , configure uma coleção da hierarquia de destino para limitar o escopo de cada coleção listada e clique em **Próximo**. Se não houver coleções listadas, clique em **Próximo**.  

10. Na página **Substituição de Código do Site**, atribua um código do site da hierarquia de destino para substituir o código do site do Configuration Manager 2007 em cada coleção listada e clique em **Avançar**. Se não houver coleções listadas, clique em **Próximo**.  

11. Na página **Informações de Revisão** , clique em **Salvar em Arquivo** para salvar as informações exibidas para visualizações futuras. Quando estiver pronto para continuar, clique em **Próximo**.  

12. Na página **Configurações** , defina quando o trabalho de migração será executado e as configurações adicionais que você necessita para esse trabalho e clique em **Próximo**.  

13. Confirme as configurações e conclua o assistente.  

#### <a name="to-create-a-migration-job-to-migrate-by-objects"></a>Para criar um trabalho de migração para migrar por objetos  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Migração**e clique em **Trabalhos de Migração**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Trabalho de Migração**.  

4.  Na página **Geral** do Assistente para Criar Trabalho de Migração, configure o seguinte e clique em **Próximo**:  

    -   Especifique um nome para o trabalho de migração.  

    -   Na lista suspensa **Tipo de Trabalho** , selecione **Migração de objeto**.  

5.  Na página **Selecionar Objetos** , selecione os tipos de objeto que você deseja migrar. Por padrão, todos os objetos disponíveis estarão selecionados para cada tipo de objeto que você escolher.  

6.  Na página **Propriedade de Conteúdo** , atribua a propriedade de conteúdo de cada site de origem listado a um site na hierarquia de destino e clique em **Próximo**. Se não houver sites de origem listados, clique em **Próximo**.  

7.  Na página **Escopo de Segurança** , selecione um ou mais escopos de segurança de administração baseada em funções para atribuir aos objetos nesse trabalho de migração e clique em **Próximo**.  

8.  Na página **Informações de Revisão** , clique em **Salvar em Arquivo** para salvar as informações exibidas para visualizações futuras. Quando estiver pronto para continuar, clique em **Próximo**.  

9. Na página **Configurações** , defina quando o trabalho de migração será executado e as configurações adicionais que você necessita para esse trabalho de migração. Clique em **Avançar**.  

10. Confirme as configurações e conclua o assistente.  

#### <a name="to-create-a-migration-job-to-migrate-changed-objects"></a>Para criar um trabalho de migração para migrar objetos alterados  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Migração**e clique em **Trabalhos de Migração**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Trabalho de Migração**.  

4.  Na página **Geral** do Assistente para Criar Trabalho de Migração, configure o seguinte e clique em **Próximo**:  

    -   Especifique um nome para o trabalho de migração.  

    -   Na lista suspensa **Tipo de Trabalho** , selecione **Objetos modificados após a migração**.  

5.  Na página **Selecionar Objetos** , selecione os tipos de objeto que você deseja migrar. Por padrão, todos os objetos disponíveis estarão selecionados para cada tipo de objeto que você escolher.  

6.  Na página **Propriedade de Conteúdo** , atribua a propriedade de conteúdo de cada site de origem listado a um site na hierarquia de destino e clique em **Próximo**. Se não houver sites de origem listados, clique em **Próximo**.  

7.  Na página **Escopo de Segurança** , selecione um ou mais escopos de segurança de administração baseada em funções para atribuir aos objetos nesse trabalho de migração e clique em **Próximo**.  

8.  Na página **Informações de Revisão** , clique em **Salvar em Arquivo** para salvar as informações exibidas para visualizações futuras. Quando estiver pronto para continuar, clique em **Próximo**.  

9. Na página **Configurações** , defina quando o trabalho de migração será executado e as configurações adicionais que você requer para esse trabalho de migração. Ao contrário dos outros tipos de trabalho de migração, esse trabalho de migração deve substituir os objetos migrados anteriormente no banco de dados do System Center Configuration Manager. Clique em **Avançar**.  

10. Confirme as configurações e conclua o assistente.  

###  <a name="a-namebkmkmodifyexclusionlista-to-modify-the-exclusion-list-for-migration"></a><a name="BKMK_Modify_Exclusion_List"></a> Para modificar a lista de exclusões para migração  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , clique em **Migração** para obter acesso à lista de exclusões. É possível também acessar a lista de exclusão do nó **Hierarquia de Origem** ou **Trabalhos de Migração** .  

3.  Na guia **Início** , no grupo **Migração** , clique em **Editar Lista de Exclusões**.  

4.  Na caixa de diálogo **Editar Lista de Exclusões** , selecione o objeto excluído a ser removido da lista de exclusões e clique em **Remover**.  

5.  Clique em **OK** para salvar as alterações e conclua a edição. Para cancelar as alterações atuais e restaurar todos os objetos que foram removidos, clique em **Cancelar**e depois em **Não**. Isso cancelará a remoção dos objetos e fechará a caixa de diálogo **Editar Lista de Exclusões** .  

#### <a name="to-share-distribution-points-from-the-source-hierarchy"></a>Para compartilhar os pontos de distribuição da hierarquia de origem  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Migração**, clique em **Hierarquia de Origem**e selecione o site de origem que você deseja configurar.  

3.  Na guia **Início** , no grupo **Site de Origem** , clique em **Configurar**.  

4.  Na caixa de diálogo **Credenciais do Site de Origem** , selecione **Habilitar o compartilhamento de ponto de distribuição para o servidor do site de origem**e clique em **OK**.  

5.  Após a conclusão da coleta de dados, clique em **Fechar**.  

#### <a name="to-change-the-schedule-of-a-migration-job"></a>Para alterar o agendamento de um trabalho de migração  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Migração**e clique em **Trabalhos de Migração**.  

3.  Clique no trabalho de migração que você deseja modificar. Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Nas propriedades do trabalho de migração, selecione a guia **Configurações** , altere a hora de execução do trabalho de migração e clique em **OK**.  

##  <a name="a-namerunmigrationjobsa-run-migration-jobs"></a><a name="Run_Migration_Jobs"></a> Executar trabalhos de migração  
 Use o procedimento a seguir para executar um trabalho de migração que ainda não foi iniciado.  

#### <a name="to-run-migration-jobs"></a>Para executar trabalhos de migração  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Migração**e clique em **Trabalhos de Migração**.  

3.  Clique no trabalho de migração que você deseja executar. Na guia **Início** , no grupo **Trabalho de Migração** , clique em **Iniciar**.  

4.  Clique em **Sim** para iniciar o trabalho de migração agora.  

##  <a name="a-namebkmkprocupgrdssa-upgrade-or-reassign-a-shared-distribution-point"></a><a name="BKMK_ProcUpgrdSS"></a> Atualizar ou reatribuir um ponto de distribuição compartilhado  
 É possível atualizar um ponto de distribuição com suporte compartilhado de um site de origem do Configuration Manager 2007, ou reatribuir um ponto de distribuição com suporte compartilhado de um site de origem do System Center Configuration Manager para ser um ponto de distribuição na hierarquia de destino.  

> [!IMPORTANT]  
>  Para poder atualizar um ponto de distribuição secundário do Configuration Manager 2007, é necessário desinstalar o software cliente do Configuration Manager 2007 de um computador com ponto de distribuição secundário. Se o software cliente do Configuration Manager 2007 estiver instalado quando você tentar atualizar o ponto de distribuição, ocorrerá falha na atualização e o conteúdo anteriormente implantado no ponto de distribuição secundário será removido do computador.  

> [!CAUTION]  
>  Ao atualizar ou reatribuir um ponto de distribuição compartilhado, a função do sistema de site do ponto de distribuição e o computador do sistema do site serão removidos do site de origem e adicionados como um ponto de distribuição ao site na hierarquia de destino que você selecionar.  

#### <a name="to-upgrade-or-reassign-a-shared-distribution-point"></a>Para atualizar ou reatribuir um ponto de distribuição compartilhado  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Migração**e clique em **Hierarquia de Origem**.  

3.  Selecione o site que possui o ponto de distribuição que você deseja atualizar, clique na guia **Pontos de Distribuição Compartilhados** e selecione o ponto de distribuição qualificado para ser atualizado ou reatribuído.  

4.  Na guia **Ponto de Distribuição** , no grupo **Ponto de Distribuição** , clique em **Reatribuir**.  

5.  Especifique as configurações no Assistente para Reatribuir Ponto de Distribuição Compartilhado como se você estivesse instalando um novo ponto de distribuição para a hierarquia de destino, com as seguintes adições:  

    -   Na página **Conversão de Conteúdo** , verifique as diretrizes sobre o espaço necessário para converter o conteúdo existente. Em seguida, na página **Configurações de Unidade** do assistente, verifique se a unidade do ponto de distribuição do computador selecionado contém a quantidade necessária de espaço livre em disco.  

6.  Confirme as configurações e conclua o assistente.  

##  <a name="a-namemonitormigrationa-monitor-migration-activity-in-the-migration-workspace"></a><a name="Monitor_MIgration"></a> Monitorar a atividade de migração no espaço de trabalho Migração  
 Use o procedimento a seguir para utilizar o console do Configuration Manager para monitorar a migração.  

#### <a name="to-monitor-migration-activity-in-the-migration-workspace"></a>Para monitorar a atividade de migração no espaço de trabalho migração  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Migração**e clique em **Trabalhos de Migração**.  

3.  Clique no trabalho de migração que você deseja monitorar.  

4.  Exiba os detalhes e o status do trabalho de migração selecionado nas guias **Resumo** e **Objetos no Trabalho**.  

##  <a name="a-namebkmkmigrateclientsa-migrate-clients"></a><a name="BKMK_MigrateClients"></a> Migrar clientes  
 Após a migração de dados dos clientes entre hierarquias, mas antes de completar a migração, planeje migrar clientes para a hierarquia de destino. A migração de clientes entre hierarquias envolve desinstalar o software cliente do Configuration Manager dos computadores atribuídos à hierarquia de origem e instalar o software cliente do Configuration Manager da hierarquia de destino. Ao instalar o cliente da hierarquia de destino, você também atribui o cliente a um site primário naquela hierarquia. Para obter mais informações sobre a migração de clientes, consulte [Planejando a estratégia de migração de cliente no System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).  

##  <a name="a-namecompletemigrationa-complete-migration"></a><a name="Complete_Migration"></a> Concluir migração  
 Use este procedimento para concluir a migração da hierarquia de origem.  

#### <a name="to-complete-migration"></a>Para concluir a migração  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Migração**e clique em **Hierarquia de Origem**.  

3.  Para hierarquias de origem do Configuration Manager 2007, selecione um site de origem que esteja no nível inferior da hierarquia de origem. Para uma hierarquia de origem do System Center 2012 Configuration Manager ou do System Center Configuration Manager, selecione o sites de origem disponível.  

4.  Na guia **Início** , no grupo **Limpar** , clique em **Parar Coleta de Dados**.  

5.  Clique em **Sim** para confirmar a ação.  

6.  Para uma hierarquia de origem do Configuration Manager 2007, antes de continuar para a próxima etapa, repita as etapas 3, 4 e 5. Realize estas etapas em cada site na hierarquia, da parte inferior da hierarquia até a parte superior. Para uma hierarquia de origem do System Center 2012 Configuration Manager ou do System Center Configuration Manager, selecione a próxima etapa.  

7.  Na guia **Início** , no grupo **Limpar** , clique em **Limpar Dados de Migração**.  

8.  Na caixa de diálogo **Limpar Dados de Migração** , na lista suspensa **Hierarquia de origem** , selecione o código do site e o servidor do site no nível superior do site da hierarquia de origem e clique em **OK**.  

9. Clique em **Sim** para concluir o processo de migração para a hierarquia de origem.  



<!--HONumber=Dec16_HO3-->


