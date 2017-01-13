---
title: Usar o cliente de interoperabilidade estendida com o Branch Atual | Microsoft Docs
description: "Saiba como usar o cliente do Branch de Manutenção de Longo Prazo do Configuration Manager com um site do Branch Atual."
ms.custom: na
ms.date: 01/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
Robots: NOINDEX,NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 30d0177dc7fcc7f39d00c48067130d587435bf2d

---
# <a name="use-the-client-software-from-the-version-1606-baseline-media-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Usar o software cliente da mídia versão 1606 da linha de base para interoperabilidade estendida com futuras versões de um site do Branch Atual

*Aplica-se a: System Center Configuration Manager (Branch Atual), (Branch de Manutenção de Longo Prazo)*  

Você pode usar o software cliente do Configuration Manager para computadores com Windows (client.msi) do DVD da mídia de linha de base versão 1606 que você obtém com o System Center 2016 ou de uma versão do System Center Configuration Manager (Branch Atual e Branch de Manutenção de Longo Prazo 1606) para gerenciar dispositivos que pertencem a um site de Branch Atual. Esse cliente é chamado de cliente de interoperabilidade estendida.

## <a name="how-this-scenario-works"></a>Como esse cenário funciona:
Normalmente, quando você instala uma nova atualização no console para o Branch Atual, os clientes atualizam automaticamente o software cliente para que possam usar esses novos recursos.

Neste cenário, você usa o Branch Atual e recebe as atualizações e novos recursos. A maioria dos clientes executa o software cliente a do Branch Atual e pode atualizar o software cliente com cada atualização de versão que você instalar. No entanto, em um subconjunto de sistemas críticos que você não deseja receber atualizações de software cliente, instale o cliente de interoperabilidade estendida. Esses clientes não instalarão o novo software cliente até que você implante explicitamente uma nova versão do software cliente neles.

Mais informações sobre como impedir que os clientes do Branch Atual atualizem automaticamente quando você instala uma nova versão do Configuration Manager estarão disponíveis com o Branch Atual versão 1610.

O site do Branch Atual deve executar a versão 1606 ou posterior.

## <a name="the-extended-interoperability-client-software"></a>O software cliente de interoperabilidade estendida
Quando você usa o cliente de interoperabilidade estendida da versão do System Center 2016 ou System Center Configuration Manager (Branch Atual e Branch de Manutenção de Longo Prazo 1606) com um site de Branch Atual, o cliente tem suporte para dois anos após a disponibilidade geral da versão, que é 12 de outubro de 2016.

Planeje atualizar o cliente de interoperabilidade estendida em dispositivos gerenciados com o Branch Atual antes que o suporte do cliente expire. Para fazer isso, baixe uma nova versão do cliente da Microsoft e, em seguida, implante esse software cliente atualizado nos dispositivos que usam o cliente de interoperabilidade estendida atual.

**Limitações do cliente de interoperabilidade estendida:**
-   Atualizações para o software cliente de interoperabilidade estendida não estão disponíveis por meio de atualizações no console. Detalhes adicionais para a implantação de um software cliente atualizado serão fornecidos quando um cliente atualizado for liberado.

## <a name="identify-the-client-version-you-use"></a>Identificar a versão de cliente que você usa
A seguir estão as versões principais de clientes disponíveis para o Branch Atual e LTSB:

|Versão do cliente|Branch e versão |  
|----------------|---------------------|
|5.00.8325.xxxx |   - Branch Atual 1511|
|5.00.8355.xxxx |- Branch Atual 1602|
|5.00.8412.1307 |- Branch Atual 1606 </br> - Branch Atual 1606 com o pacote cumulativo de atualizações do hotfix 1606 (KB3186654)</br>- Cliente de interoperabilidade estendida da mídia da linha de base versão 1606|  

No cliente, você pode exibir a versão do cliente na guia **Geral** do miniaplicativo do painel de controle do Configuration Manager.

Na guia **Componentes** do miniaplicativo, alguns componentes mostram valores diferentes. Por exemplo, para uma versão de cliente 8412.1307, alguns componentes podem estar listados como 5.00.8412.**1000** ou 5.00.8412.**1006**.  Essa diferença nos últimos quatro dígitos para alguns componentes é normal e não indica uma falha do componente em atualizar para a versão atual do cliente.



<!--HONumber=Dec16_HO3-->


