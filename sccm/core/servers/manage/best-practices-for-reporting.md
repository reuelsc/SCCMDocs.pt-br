---
title: "Práticas recomendadas de relatórios | Microsoft Docs"
description: "Leia algumas dicas úteis sobre como usar a funcionalidade de relatórios do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 64f9d931-33f1-456f-a4e4-0ec077465bd0
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 759258999f3eaa810803a6a7f856f00fe7771a9e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
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
