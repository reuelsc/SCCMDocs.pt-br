---
title: "Planejar a migração | System Center Configuration Manager"
description: Saiba mais sobre sites e hierarquias antes de migrar dados para uma hierarquia de destino do System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: a80c7af58f88f76afd00771778411a4842a204c8


---
# <a name="planning-for-migration-to-system-center-configuration-manager"></a>Planejando a migração para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de migrar dados para uma hierarquia de destino do System Center Configuration Manager, você deve estar familiarizado com sites e hierarquias no Configuration Manager. Para obter mais informações sobre sites e hierarquias, consulte [Noções básicas do System Center Configuration Manager](../../core/understand/fundamentals.md).  

 Para poder migrar dados de uma hierarquia de origem com suporte, primeiro você deverá instalar uma hierarquia do System Center Configuration Manager para ser a hierarquia de destino.  

 Concluída a instalação da hierarquia de destino, antes de iniciar a migração de dados, configure os recursos e as funções de gerenciamento que deseja usar em sua hierarquia de destino.  

 Além disso, talvez seja necessário planejar a sobreposição entre a hierarquia de origem e a sua hierarquia de destino. Como exemplo, considere quando a hierarquia de origem é configurada para usar os mesmos locais de rede ou limites como sua hierarquia de destino; em seguida, instale novos clientes na sua hierarquia de destino e use atribuição automática de site. Nesse cenário, devido ao fato de o cliente do Configuration Manager recém-instalado poder escolher um site de qualquer uma das hierarquias para nele ingressar, o cliente poderá ser atribuído incorretamente à sua hierarquia de origem. Portanto, planeje atribuir todo novo cliente na hierarquia de destino a um site específico nessa hierarquia em vez de usar a atribuição automática de site.  

 Para obter mais informações sobre atribuições de site, consulte a seção [Considerações de atribuição de site do cliente](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment), no tópico [Interoperabilidade entre versões diferentes do System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

## <a name="planning-topics"></a>Tópicos de planejamento  
 Use os seguintes tópicos para ajudar a planejar a migração de uma hierarquia de origem com suporte para uma hierarquia de destino do System Center Configuration Manager:  

-   [Pré-requisitos para a migração no System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md)  

-   [Listas de verificação do administrador para o planejamento da migração no System Center Configuration Manager](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Determinar se realizará ou não a migração de dados para o System Center Configuration Manager](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Planejando uma estratégia de hierarquia de origem no System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Listas de verificação do administrador para o planejamento da migração no System Center Configuration Manager](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Planejamento de uma estratégia de migração de cliente no System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md)  

-   [Planejamento de uma estratégia de migração de implantação de conteúdo no System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Planejamento da migração de objetos do Configuration Manager para o System Center Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Planejamento do monitoramento da atividade de migração no System Center Configuration Manager](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Planejamento da conclusão da migração no System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md)  



<!--HONumber=Nov16_HO1-->


