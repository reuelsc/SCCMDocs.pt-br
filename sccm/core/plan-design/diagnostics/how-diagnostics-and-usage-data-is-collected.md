---
title: Coleta de dados de diagnóstico
titleSuffix: Configuration Manager
description: Saiba mais sobre como o System Center Configuration Manager coleta dados de diagnóstico e de uso sobre si mesmo.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 704c64d314f2eaf4fe2678f316ea729584752d2e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125571"
---
# <a name="how-diagnostics-and-usage-data-is-collected-by-system-center-configuration-manager"></a>Como os dados de diagnóstico e de uso são coletados pelo System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para coletar dados de diagnóstico e de uso para o System Center Configuration Manager, cada site primário executa consultas do SQL Server semanalmente. Em uma hierarquia com vários local, os dados são replicados para o site de administração central.  

No site de nível superior de uma hierarquia, a função do sistema de sites do ponto de conexão de serviço envia essas informações quando verifica se há atualizações. O modo do ponto de conexão de serviço determina como os dados são transferidos:  

-   **No modo online:** os dados de diagnóstico e de uso são enviados automaticamente uma vez por semana do ponto de conexão de serviço para o serviço de nuvem.  

-   **No modo offline:** os dados de diagnóstico e de uso são transferidos manualmente usando a ferramenta de conexão de serviço. Para obter mais informações, consulte [Usar a Ferramenta de Conexão de Serviço do System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md)  

Para obter mais informações, consulte [Sobre o ponto de conexão de serviço no System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  
