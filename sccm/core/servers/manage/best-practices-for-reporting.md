---
title: Práticas recomendadas para relatórios
titleSuffix: Configuration Manager
description: Leia algumas dicas úteis sobre como usar a funcionalidade de relatórios do System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 64f9d931-33f1-456f-a4e4-0ec077465bd0
author: mestew
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: f6e57099ae31ccc51324dca342265337c79afddd
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65497633"
---
# <a name="best-practices-for-reporting-in-system-center-configuration-manager"></a>Práticas recomendadas para relatórios no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as práticas recomendadas a seguir para relatórios no System Center Configuration Manager:  

## <a name="for-best-performance-install-the-reporting-services-point-on-a-remote-site-system-server"></a>Para obter o melhor desempenho, instale o ponto do Reporting Services em um servidor do sistema de site remoto  
 Embora você possa instalar o ponto do Reporting Services no servidor do site ou em um sistema de site remoto, o desempenho aumenta quando o ponto do Reporting Services é instalado em um servidor do sistema de site remoto.  

## <a name="optimize-sql-server-reporting-services-queries"></a>Otimizar as consultas do SQL Server Reporting Services  
 Normalmente, os atrasos na geração de relatório se devem ao tempo necessário para executar as consultas e recuperar os resultados. Se você estiver usando o Microsoft SQL Server, ferramentas como Query Analyzer e Profiler podem ajudar a otimizar as consultas.  

## <a name="schedule-report-subscription-processing-to-run-outside-standard-office-hours"></a>Agendar o processamento de assinatura de relatório para execução fora do expediente padrão  
 Sempre que possível, agende o processamento de assinatura de relatório para execução fora do horário de expediente normal padrão para reduzir o processamento da CPU no servidor de banco de dados do site do Configuration Manager. Essa prática também melhora a disponibilidade para solicitações de relatório imprevistas.  

## <a name="next-steps"></a>Próximas etapas
[Configurar relatórios](configuring-reporting.md)
