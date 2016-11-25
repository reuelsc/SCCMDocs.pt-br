---
title: "Listas de verificação de migração | System Center Configuration Manager"
description: "Use as listas de verificação do administrador para ajudá-lo a planejar uma estratégia de migração para o System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 295fdf07-93cc-490c-acdd-ce3ee88cb36f
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f3912de04aa3e6196137a7034753013c35180d64


---
# <a name="administrator-checklists-for-migration-planning-in-system-center-configuration-manager"></a>Listas de verificação do administrador para o planejamento da migração no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as listas de verificação do administrador a seguir para ajudá-lo a planejar sua estratégia de migração para o System Center Configuration Manager:  

-   [Lista de verificação do administrador para planejamento de migração](#Checklist_Migraiton_Planning)  

-   [Lista de verificação do administrador para migração de hierarquia](#Checklist_Hierarchy_for_migration)  

-   [Lista de verificação do administrador para migração](#Checklisit_Migration)  

##  <a name="a-namechecklistmigraitonplanninga-administrator-checklist-for-migration-planning"></a><a name="Checklist_Migraiton_Planning"></a> Lista de verificação do administrador para planejamento de migração  
 Use a seguinte lista de verificação para as etapas de planejamento da pré-migração:  

-   **Avalie o ambiente atual:**  

     Identifique os requisitos de negócios existentes que são atendidos pela hierarquia de origem e planos de desenvolvimento para continuar a atender esses requisitos na hierarquia de destino.  

-   **Examine a funcionalidade e as alterações disponíveis com a versão do Configuration Manager que você utiliza e use essas informações para ajudá-lo a criar sua hierarquia de destino:**  

    Para obter mais informações, consulte [Fundamentals of System Center Configuration Manager](../../core/understand/fundamentals.md) e [What's new in System Center Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).  


-   **Determine o modelo de segurança administrativa a ser usado para a administração baseada em função:**  

    Para obter mais informações, consulte [Fundamentos de administração baseada em funções para o System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   **Avalie sua rede e a topologia do Active Directory:**  

    Examine sua estrutura de domínio existente e topologia de rede e considere como isso influencia seu design de hierarquia e suas tarefas de migração.  

-   **Finalize seu design de hierarquia de destino:**  

    Decida o posicionamento de um site de administração central, de sites primários e secundários, e opções de distribuição de conteúdo.  

-   **Mapeie sua hierarquia nos computadores que serão usados para sites e servidores do site na hierarquia de destino:**  

    Identifique os computadores que os sites e servidores de sistema de site usarão na hierarquia de destino, e verifique se possuem capacidade suficiente para atender aos requisitos operacionais existentes e futuros.  

-   **Planeje sua estratégia de migração do objeto:**  

    Planeje usar os trabalhos de migração disponíveis para migrar objetos diferentes, que incluem limites de site, coleções, anúncios e implantações. Para obter mais informações, consulte [Tipos de Trabalho de Migração](../../core/migration/planning-a-migration-job-strategy.md#Types_of_Migration) em [Planejando estratégia de trabalho de migração no System Center Configuration Manager](../../core/migration/planning-a-migration-job-strategy.md)  

    O Configuration Manager migrará apenas os objetos que você selecionar. Os objetos que não são migrados e que são necessários na hierarquia de destino devem ser recriados na hierarquia de destino.  

    Os objetos que podem ser migrados são exibidos quando você configura os trabalhos de migração.  

-   **Planeje sua estratégia de migração de cliente:**  

    Planeje a migração de clientes usando uma abordagem controlada que limita a largura de banda da rede e os requisitos de processamento do servidor quando você migra clientes para a hierarquia de destino. Para obter mais informações sobre como planejar uma estratégia de migração de cliente, consulte [Planning a client migration strategy in System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Planeje os dados de inventário e de conformidade:**  

    O Configuration Manager não dá suporte à migração de inventário de hardware e de software ou dados de conformidade de gerenciamento de configuração desejado para atualizações de software ou clientes.  

    Em vez disso, após o cliente migrar para seu novo site na hierarquia de destino e receber a política dessas configurações, o cliente envia essas informações para seu site atribuído. Essa ação preenche o banco de dados do site de destino com dados de conformidade e de inventário atuais.  

-   **Planeje a conclusão da migração da hierarquia de origem:**  

    Decida quando objetos e clientes serão migrados. Após a conclusão da migração, você pode planejar o encerramento dos servidores do site na hierarquia de origem.  

##  <a name="a-namechecklisthierarchyformigrationa-administrator-checklist-for-hierarchy-migration"></a><a name="Checklist_Hierarchy_for_migration"></a> Lista de verificação do administrador para migração de hierarquia  
Use a seguinte lista de verificação para ajudá-lo a planejar uma hierarquia de destino antes de começar a migração.  

-   **Identifique os computadores para usar na hierarquia de destino:**  

    O Configuration Manager não dá suporte a uma atualização in-loco da infraestrutura do Configuration Manager 2007. Em vez disso, use a migração para mover os dados do Configuration Manager 2007 para o System Center Configuration Manager. Isso exige que você use uma implantação lado a lado e instale o System Center Configuration Manager em novos computadores.  

    Do mesmo modo, ao migrar de outra hierarquia do System Center Configuration Manager, instale uma nova hierarquia de destino que seja uma implantação lado a lado para sua hierarquia de origem.  

-   **Crie sua hierarquia de destino:**  

    Para preparar a migração, instale e configure uma hierarquia de destino do System Center Configuration Manager que inclui um site primário. Por exemplo:  

    -   Instale um site de administração central e depois instale pelo menos um site primário filho  

    -   Instale um primário autônomo se você não planeja usar um site de administração central.  

-   **Se desejar migrar informações relacionadas a atualizações de software, configure um ponto de atualização de software na hierarquia de destino e sincronize as atualizações de software:**  

    Configure e sincronize as atualizações de software na hierarquia de destino para migrar informações de atualizações de software da hierarquia de origem.  


-   **Instale e configure funções de sistema de sites adicionais na hierarquia de destino:**  

    Configure funções de sistema de site adicionais e sistemas de site que você precisará.  

-   **Verifique a funcionalidade operacional na hierarquia de destino:**  

    Verifique o seguinte:  

    -   Se a hierarquia de destino inclui vários sites, confirme se a replicação de banco de dados está funcionando entre sites. A replicação de banco de dados não é aplicável a sites primários autônomos.  

    -   Verifique se todas as funções de sistema de site instaladas estão operacionais.  

    -   Verifique se os clientes do Configuration Manager instalados na hierarquia de destino podem se comunicar bem com o site atribuído.  


##  <a name="a-namechecklisitmigrationa-administrator-checklist-for-migration"></a><a name="Checklisit_Migration"></a> Lista de verificação do administrador para migração  
Use a seguinte lista de verificação para migrar dados da hierarquia de origem para a hierarquia de destino.  

-   **Habilite a migração na hierarquia de destino:**  

    Configure uma hierarquia de origem especificando o site de nível superior da hierarquia de origem. Para obter mais informações sobre como especificar o site de origem, consulte [Planning a source hierarchy strategy in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).  

-   **Selecione e configure sites adicionais na hierarquia de origem quando ela executar o Configuration Manager 2007 SP2:**  

    Para cada site adicional na hierarquia de origem do Configuration Manager 2007 SP2 do qual deseja coletar dados, configure credenciais para coleta de dados. Quando você configura cada site de origem, o processo de coleta de dados começa imediatamente e continua por todo o período de migração, até que você interrompa a coleta de dados para aquele site. A coleta de dados assegura que você possa migrar objetos da hierarquia de origem que estão atualizados ou novos desde o processo de coleta de dados anterior.  

    > [!NOTE]  
    >  Quando a hierarquia de origem executa o System Center 2012 Configuration Manager ou posterior, não é necessário configurar sites de origem adicionais.  

-   **Configure o compartilhamento de ponto de distribuição:**  

    É possível compartilhar pontos de distribuição entre as duas hierarquias para tornar o conteúdo de objetos que você migra disponível aos clientes na hierarquia de destino. Isso assegura que o mesmo conteúdo permaneça disponível a clientes nas duas hierarquias e que você possa manter esse conteúdo até parar a coleta de dados e concluir a migração.  

    Para obter informações sobre pontos de distribuição compartilhados, consulte a seção *Share Distribution Points Between Source and Destination Hierarchies* no tópico [Planning a content deployment migration strategy in System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md) .  

-   **Crie e execute trabalhos de migração para migrar objetos associados aos clientes na hierarquia de origem:**  

    Crie trabalhos de migração para migrar objetos entre as hierarquias. As configurações necessárias para cada trabalho de migração podem variar, dependendo de quais dados o trabalho migra.  

    Por exemplo, quando migrar o conteúdo, independentemente do trabalho de migração utilizado, atribua um site na hierarquia de destino para gerenciamento próprio desse conteúdo. O site atribuído acessará o local do arquivo fonte original para o conteúdo e é responsável por distribuir esse conteúdo aos pontos de distribuição na hierarquia de destino.  

    Para obter mais informações, consulte a seção [Create and Edit Migration Jobs for System Center Configuration Manager](../../core/migration/operations-for-migration.md#create_edit_migration_jobs) no tópico [Operations for migrating to System Center Configuration Manager](../../core/migration/operations-for-migration.md) .  

-   **Migre clientes para a hierarquia de destino:**  

    O processo de migração de clientes depende de seu cenário de migração:  

    -   Quando você migra clientes que possuem uma versão de cliente que não é a mesma da hierarquia de destino, o software do cliente deve ser atualizado. A atualização requer a remoção do cliente do Configuration Manager atual, seguida pela instalação da nova versão de cliente que corresponde ao site de destino.  

    -   Quando você migra clientes que possuem uma versão de cliente que corresponde à versão da hierarquia de destino, o cliente não se atualiza nem se reinstala. Em vez disso, o cliente atribui novamente para um site primário na hierarquia de destino.  

    Quando você migra um cliente para a hierarquia de destino, ele é associado aos dados que você migrou anteriormente para essa hierarquia de destino.  

    Para obter mais informações, consulte [Planning a client migration strategy in System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Atualizar ou reatribuir pontos de distribuição compartilhados:**  

    Quando você não precisar mais dar suporte a clientes em sua hierarquia de origem, poderá atualizar pontos de distribuição compartilhados por meio de um site de origem do Configuration Manager 2007 ou reatribuir pontos de distribuição compartilhados por meio de um site de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager. Ao atualizar ou reatribuir um ponto de distribuição, a função de sistema do site é transferida para um site primário na hierarquia de destino e o ponto de distribuição é removido do site de origem na hierarquia de origem. Ao atualizar ou reatribuir um ponto de distribuição compartilhado, o conteúdo permanece no computador do ponto de distribuição e você não precisa reimplantar o conteúdo que está no computador do ponto de distribuição para novos pontos de distribuição na hierarquia de destino.  

    É possível também atualizar um ponto de distribuição do Configuration Manager 2007 que está colocalizado em um servidor do site secundário. Isso remove o site secundário e resulta em apenas um ponto de distribuição na hierarquia de destino.  

    Para obter informações sobre pontos de distribuição compartilhados, consulte a seção [Share Distribution Points Between Source and Destination Hierarchies](../../core/migration/planning-a-content-deployment-migration-strategy.md#about_shared_dps_in_migrations) no tópico [Planning a content deployment migration strategy in System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md) .  

-   **Concluir migração:**  

    Após ter migrado dados e clientes de todos os sites na hierarquia de origem e ter atualizado os pontos de distribuição aplicáveis, então você pode concluir a migração. Para concluir a migração, interrompa a coleta de dados para cada site de origem na hierarquia de origem. Em seguida, remova as informações de migração das quais não precisa e encerre sua infraestrutura de hierarquia de origem. Para obter mais informações, consulte [Planning to complete migration in System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md).  



<!--HONumber=Nov16_HO1-->


