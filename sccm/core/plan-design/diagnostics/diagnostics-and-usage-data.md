---
title: "Dados de uso e diagnóstico | Microsoft Docs"
description: "Saiba mais sobre os dados de diagnóstico e de uso que o System Center Configuration Manager coleta sobre si mesmo."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
caps.latest.revision: 9
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 4a4b7c9c0d40b6bd3ea2f318e37d744f1a0cc084
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017


---
# <a name="diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Dados de diagnóstico e de uso para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager coleta dados de diagnóstico e de uso sobre si mesmo, que são usados pela Microsoft para aprimorar a experiência, a qualidade e a segurança da instalação de versões futuras.  

 Os dados de diagnóstico e de uso são habilitados para cada hierarquia do System Center Configuration Manager. Eles consistem em consultas do SQL Server que são executadas semanalmente em cada site primário e no site de administração central. Quando a hierarquia usa um site de administração central, os dados dos sites primários são replicados nesse site. No site de nível superior da hierarquia, o ponto de conexão de serviço envia essas informações quando verifica se há atualizações. Se o ponto de conexão de serviço estiver no modo offline, as informações serão transferidas por meio da ferramenta de conexão de serviço.  

> [!NOTE]  
>  O Configuration Manager coleta dados apenas do banco de dados SQL Server do site e não coleta dados diretamente de clientes ou de servidores do site.  

 Para obter mais informações, veja a [Política de Privacidade do System Center Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=626527).  

 Saiba mais sobre os dados de diagnóstico e de uso do System Center Configuration Manager nos seguintes artigos:  

-   [Como os dados de diagnóstico e de uso são usados no System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md)  

-   Níveis da coleta de dados de diagnóstico e de uso:
    - [Dados de diagnóstico para 1702](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1702)      
    - [Dados de diagnóstico para 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)  
    - [Dados de diagnóstico para 1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)    

<!--
    - [Diagnostic data for 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
    - [Diagnostic data for  1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
-->

-   [Como os dados de diagnóstico e de uso são coletados pelo System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected.md)  

-   [Como exibir dados de diagnóstico e de uso no System Center Configuration Manager](../../../core/plan-design/diagnostics/view-diagnostics-and-usage-data.md)  

-   [CEIP (Programa de Aperfeiçoamento da Experiência do Usuário) do System Center Configuration Manager](../../../core/plan-design/diagnostics/customer-experience-improvement-program-ceip.md)  

-   [Perguntas frequentes sobre dados de diagnóstico e de uso do System Center Configuration Manager](../../../core/understand/frequently-asked-questions-about-diagnostics-and-usage-data.md)  

## <a name="see-also"></a>Consulte também  
 [Sobre o ponto de conexão de serviço no System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md)

