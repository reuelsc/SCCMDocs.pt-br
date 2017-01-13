---
title: "Coleção de dados de diagnóstico | Microsoft Docs"
description: "Saiba mais sobre como o System Center Configuration Manager coleta dados de diagnóstico e de uso sobre si mesmo."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: f0a992139ad1bc516df2f6ea947509e3e4a77c54


---
# <a name="how-diagnostics-and-usage-data-is-collected-by-system-center-configuration-manager"></a>Como os dados de diagnóstico e de uso são coletados pelo System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para coletar dados de diagnóstico e de uso para o System Center Configuration Manager, cada site primário executa consultas do SQL Server semanalmente. Em uma hierarquia com vários local, os dados são replicados para o site de administração central.  

No site de nível superior de uma hierarquia, a função do sistema de sites do ponto de conexão de serviço envia essas informações quando verifica se há atualizações. Como as transferências de dados dependem do modo do ponto de conexão de serviço:  

-   **No modo online:** os dados de diagnóstico e de uso são enviados automaticamente uma vez por semana do ponto de conexão de serviço para o serviço de nuvem.  

-   **No modo offline:** os dados de diagnóstico e de uso são transferidos manualmente usando a ferramenta de conexão de serviço. Para obter mais informações, consulte [Use the Service Connection Tool for System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

Para obter mais informações, consulte [About the service connection point in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  



<!--HONumber=Dec16_HO3-->


