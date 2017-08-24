---
title: Use limites e grupos de limites | Microsoft Docs
description: "Use os limites e os grupos de limites para definir locais de rede e sistemas de site acessíveis para dispositivos que você gerencia."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
caps.latest.revision: "10"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0fea1dece0768a2b7bcd3fcedc2288ea2d52e73d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="define-site-boundaries-and-boundary-groups-for-system-center-configuration-manager"></a>Definir limites de site e grupos de limites para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os limites para o System Center Configuration Manager definem locais de rede na intranet que pode conter dispositivos que você deseja gerenciar. Grupos de limites são grupos lógicos de limites que você configura.

 Uma hierarquia pode incluir qualquer número de grupos de limites, e cada grupo de limite pode conter qualquer combinação dos seguintes tipos de limites:  

-   Sub-rede IP,  
-   Nome do site do Active Directory  
-   Prefixo IPv6  
-   Intervalo de Endereços IP  

Os clientes da intranet avaliam seu local de rede atual e, em seguida, usam essas informações para identificar grupos de limites aos quais eles pertencem.  

 Os clientes usam grupos de limites para:  
-   **Encontrar um site atribuído:** grupos de limites permitem que os clientes localizem um site primário para atribuição do cliente (atribuição automática de site).  
-   **Localizar determinadas funções de sistema de site que eles podem usar:**  quando você associa um grupo de limites com certas funções do sistema de sites, o grupo de limite fornece aos clientes a lista de sistemas de sites para uso durante a localização de conteúdo e como pontos de gerenciamento preferenciais.  

Os clientes que estão na Internet ou configurados como clientes somente de Internet não usam informações de limites. Esses clientes não podem usar a atribuição automática de site e sempre podem baixar conteúdo de qualquer ponto de distribuição do site atribuído quando o ponto de distribuição está configurado para permitir conexões de clientes da Internet.  

**Para iniciar:**
- Primeiro, [defina locais de rede como limites](/sccm/core/servers/deploy/configure/boundaries).
- Em seguida, continue [configurando grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) para associar os clientes dentro desses limites nos servidores de sistema de sites que eles podem usar.



##  <a name="BKMK_BoundaryBestPractices"></a> Práticas recomendadas para limites e grupos de limites  

-   **Use uma combinação do menor número de limites que atendem às suas necessidades:**  
   No passado, era recomendável o uso de alguns tipos de limites em relação a os outros. Com as alterações para melhorar o desempenho, agora é recomendável que você use o tipo ou tipos de limites que escolher que funcionam para seu ambiente e que permitem que você use o menor número de limites possível para simplificar as tarefas de gerenciamento.      

-   **Evite a sobreposição de limites para atribuição automática de site:**  
     Embora cada grupo de limites dê suporte a configurações de atribuição de site e de local de conteúdo, é uma melhor prática para criar um conjunto separado de grupos de limites para usar apenas para atribuição de site. Significado: garanta que cada limite em um grupo de limites não seja membro de outro grupo de limites com uma atribuição de site diferente. Isso ocorre porque:  

    -   Um único limite pode ser incluído em vários grupos de limites  

    -   Cada grupo de limite pode ser associado um site primário diferente para atribuição de site  

    -   Um cliente em um limite que seja membro de dois grupos de limites diferentes com atribuições de site diferente selecionará aleatoriamente um site para ingressar, que pode não ser o site que você pretendia que o cliente ingressasse.  Essa configuração é chamada de limites sobrepostos.  

     Os limites sobrepostos não são um problema para o local do conteúdo, em vez disso, geralmente são uma configuração desejada que fornece recursos adicionais de clientes ou locais de conteúdo que eles podem usar.  
