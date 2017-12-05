---
title: "Perguntas frequentes sobre dados de diagnóstico"
titleSuffix: Configuration Manager
description: "Encontre as perguntas frequentes sobre dados de diagnóstico e de uso do System Center Configuration Manager."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
caps.latest.revision: "6"
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 43e67262ce2b22e604f5b6d3ff1971921cd82637
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Perguntas frequentes sobre dados de diagnóstico e de uso do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Veja a seguir as perguntas frequentes sobre dados de diagnóstico e de uso do System Center Configuration Manager:  

###  <a name="bkmk_off"></a> Como desativo a telemetria?  
A telemetria não pode ser desativada. No entanto, você pode escolher o nível de dados coletados pela telemetria. Você também pode usar um ponto de conexão de serviço no modo offline para ajudar a gerenciar quando os dados de telemetria são enviados.

O ramificação atual do Configuration Manager precisa ser atualizado regularmente para dar suporte a novas versões do Windows 10 e do Microsoft Intune. A Microsoft exige pelo menos o nível Básico de dados de diagnóstico e de uso para manter o produto atualizado, aprimorar a experiência de atualização e melhorar a qualidade e a segurança do produto.

###  <a name="bkmk_retention"></a> Qual é o período de retenção de dados?  
 Dados de diagnóstico e de uso são mantidos por um ano.  

###  <a name="bkmk_update"></a> Os dados de diagnóstico e de uso são enviados na instalação ou atualização do produto?  
 Não. Os dados de diagnóstico e de uso são enviados apenas depois que o site estiver instalado e funcionando.  

###  <a name="bkmk_frequency"></a> Com que frequência os dados são enviados?  
 Os procedimentos armazenados do SQL são executados a cada sete dias (a contar da data que o site é instalado). No modo online, o ponto de conexão de serviço é configurado para carregar os dados depois que as consultas são executadas. No modo offline, o administrador usa a ferramenta de conexão de serviço para carregar os dados. (Observe que, inicialmente, os dados não estarão disponíveis para uso offline antes dos sete dias a contar de quando o site foi instalado.)  

###  <a name="bkmk_network"></a> Os dados podem ser usados para formar um mapa de rede?  
 Como mostrado na descrição dos níveis da coleta de dados de uso e de diagnóstico do System Center Configuration Manager, detalhes do site incluem informações de fuso horário para cada site. Isso pode fornecer informações sobre a localização geográfica geral e a dispersão global de sites em uma hierarquia. No entanto, nenhum detalhe de rede, como endereços IP ou informações geográficas mais detalhadas, é coletado.
 - [Dados de diagnóstico para 1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
 - [Dados de diagnóstico para 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
 - [Dados de diagnóstico para 1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)
 - [Dados de diagnóstico para 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)


###  <a name="bkmk_tables"></a> Você pode ver dados em tabelas personalizadas?  
 Não. Os dados de diagnóstico e de uso são coletados por meio de procedimentos armazenados do SQL em tabelas de produtos padrão no banco de dados (todas elas têm o prefixo **TEL_**). Como parte da consulta de detecção do esquema SQL, todos os nomes de tabela apresentam hash para comparação com os padrões conhecidos. Isso pode determinar que tabelas personalizadas existam no banco de dados (que o esquema de banco de dados seja estendido do padrão) mas não os dados contidos nessas tabelas.  

###  <a name="bkmk_databases"></a> Você vê nomes de outros bancos de dados ou dados em outros bancos de dados?  
 Não. Os procedimentos armazenados para coletar dados são limitados ao banco de dados do site.  

## <a name="see-also"></a>Consulte também  
 [Dados de diagnóstico e de uso para o System Center Configuration Manager](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)
