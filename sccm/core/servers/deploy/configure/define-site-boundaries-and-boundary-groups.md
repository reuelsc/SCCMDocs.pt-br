---
title: Usar Limites e grupos de limites
titleSuffix: Configuration Manager
description: Use os limites e os grupos de limites para definir locais de rede e sistemas de site acessíveis para dispositivos que você gerencia.
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c747301f6a076902227a2044e4f116207ed811ff
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499208"
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
-   **encontrar um site atribuído:** os grupos de limites permitem que clientes encontrem um site primário para atribuição de cliente (atribuição automática de site).  
-   **encontrar determinadas funções do sistema de sites que eles possam usar:** quando você associa um grupo de limites com certas funções do sistema de sites, o grupo de limites fornece aos clientes a lista de sistemas de sites a serem usados durante a localização de conteúdo e como pontos de gerenciamento preferenciais.  

Os clientes que estão na Internet ou configurados como clientes somente de Internet não usam informações de limites. Esses clientes não podem usar a atribuição automática de site e sempre podem baixar conteúdo de qualquer ponto de distribuição do site atribuído quando o ponto de distribuição está configurado para permitir conexões de clientes da Internet.  

**Para iniciar:**
- Primeiro, [defina locais de rede como limites](/sccm/core/servers/deploy/configure/boundaries).
- Em seguida, continue [configurando grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) para associar os clientes dentro desses limites nos servidores de sistema de sites que eles podem usar.



##  <a name="BKMK_BoundaryBestPractices"></a> Práticas recomendadas para limites e grupos de limites  

- **Use uma combinação do menor número de limites que atendem às suas necessidades:**  
  No passado, era recomendável o uso de alguns tipos de limites em relação a os outros. Com as alterações para melhorar o desempenho, agora é recomendável que você use o tipo ou tipos de limites que escolher que funcionam para seu ambiente e que permitem que você use o menor número de limites possível para simplificar as tarefas de gerenciamento.      

- **Evite a sobreposição de limites para atribuição automática de site:**  
   Embora cada grupo de limites dê suporte a configurações de atribuição de site e de local de conteúdo, é uma melhor prática para criar um conjunto separado de grupos de limites para usar apenas para atribuição de site. Significado: garanta que cada limite em um grupo de limites não seja membro de outro grupo de limites com uma atribuição de site diferente. Isso ocorre porque:  

  - Um único limite pode ser incluído em vários grupos de limites  

  - Cada grupo de limite pode ser associado um site primário diferente para atribuição de site  

  - Um cliente em um limite que seja membro de dois grupos de limites diferentes com atribuições de site diferente selecionará aleatoriamente um site para ingressar, que pode não ser o site que você pretendia que o cliente ingressasse.  Essa configuração é chamada de limites sobrepostos.  

    Os limites sobrepostos não são um problema para o local do conteúdo, em vez disso, geralmente são uma configuração desejada que fornece recursos adicionais de clientes ou locais de conteúdo que eles podem usar.  
