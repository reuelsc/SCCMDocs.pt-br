---
title: "Coleta de dados de diagnóstico"
titleSuffix: Configuration Manager
description: "Saiba mais sobre como o System Center Configuration Manager coleta dados de diagnóstico e de uso sobre si mesmo."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
caps.latest.revision: "5"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: ba18ae0eae0d55d098646670d7208bcdb27d7a4a
ms.sourcegitcommit: da27d37cc4e4e06cf23758846cdd7acb617f744b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="how-diagnostics-and-usage-data-is-collected-by-system-center-configuration-manager"></a>Como os dados de diagnóstico e de uso são coletados pelo System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para coletar dados de diagnóstico e de uso para o System Center Configuration Manager, cada site primário executa consultas do SQL Server semanalmente. Em uma hierarquia com vários local, os dados são replicados para o site de administração central.  

No site de nível superior de uma hierarquia, a função do sistema de sites do ponto de conexão de serviço envia essas informações quando verifica se há atualizações. O modo do ponto de conexão de serviço determina como os dados são transferidos:  

-   **No modo online:** os dados de diagnóstico e de uso são enviados automaticamente uma vez por semana do ponto de conexão de serviço para o serviço de nuvem.  

-   **No modo offline:** os dados de diagnóstico e de uso são transferidos manualmente usando a ferramenta de conexão de serviço. Para obter mais informações, consulte [Usar a Ferramenta de Conexão de Serviço do System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

Para obter mais informações, consulte [Sobre o ponto de conexão de serviço no System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  
