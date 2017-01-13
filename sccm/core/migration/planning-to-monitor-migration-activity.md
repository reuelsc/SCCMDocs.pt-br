---
title: "Monitorar a migração | Microsoft Docs"
description: "Saiba como usar o console do Configuration Manager para monitorar o progresso e o sucesso dos trabalhos de migração."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc731d3f-edd7-4049-b17b-653d6693a564
caps.latest.revision: 4
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5e3d3f4194b06442e34c10988a20fe9ca40ac5d7
ms.openlocfilehash: 896807ec2c4be2835094a27add59d4cc09e93add


---
# <a name="planning-to-monitor-migration-activity-in-system-center-configuration-manager"></a>Planejamento do monitoramento da atividade de migração no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Com o System Center Configuration Manager, você pode monitorar a migração no console do Configuration Manager que se conecta à hierarquia de destino. No console do Configuration Manager, no espaço de trabalho **Administração**, é possível usar o nó **Migração** para monitorar o progresso e o sucesso dos trabalhos de migração. É possível exibir informações de resumo para cada trabalho de migração que identifique objetos que migraram, objetos que ainda não foram migrados e o número de objetos excluídos de um trabalho de migração. Você também verá detalhes sobre problemas de migração.  

## <a name="view-migration-progress"></a>Exibir andamento da migração  
 Para exibir o andamento de um trabalho de migração, execute uma das seguintes ações:  

-   No espaço de trabalho **Administração** do console do Configuration Manager, expanda o nó **Trabalhos de Migração**, selecione um trabalho de migração e selecione a guia **Objetos no Trabalho**.  

-   Use os arquivos de log do Configuration Manager para examinar o andamento da migração ou para identificar problemas. O Gerenciador de Migração é o processo do Configuration Manager que controla as ações de migração e as registra no arquivo migmctrl.log, na pasta **\&lt;CaminhoDeInstalação\>\\LOGS** do servidor do site.  

    > [!NOTE]  
    >  Se ocorrer falha em um trabalho de migração, verifique os detalhes no arquivo migmctrl.log o mais rápido possível. As entradas do log de migração são continuamente adicionadas ao arquivo e substituem os detalhes antigos. Se as entradas forem substituídas, talvez você não consiga identificar se os problemas encontrados nos objetos migrados estão associados aos problemas de migração. A atividade de migração é registrada no site de nível superior da hierarquia, independentemente do site ao qual o seu console do Configuration Manager se conecta quando você configura a migração.  

-   Use os relatórios do Configuration Manager. O Configuration Manager fornece diversos relatórios internos de migração, ou você pode editar os relatórios para que se adaptem às suas necessidades. Para obter mais informações sobre os relatórios no Configuration Manager, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  



<!--HONumber=Dec16_HO3-->


