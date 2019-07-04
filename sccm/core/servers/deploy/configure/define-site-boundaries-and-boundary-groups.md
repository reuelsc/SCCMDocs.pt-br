---
title: Usar Limites e grupos de limites
titleSuffix: Configuration Manager
description: Use os limites e os grupos de limites para definir locais de rede e sistemas de site acessíveis para dispositivos que você gerencia.
ms.date: 06/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d160c6ab64c5ad097bf5986882b65171b0df4651
ms.sourcegitcommit: 60d45a5df135b84146f6cfea2bac7fd4921d0469
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67194154"
---
# <a name="define-site-boundaries-and-boundary-groups"></a>Configurar limites de site e grupos de limites

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

*Limites* no Configuration Manager definem os locais de rede na sua intranet. Esses locais incluem dispositivos que você deseja gerenciar. *Grupos de limites* são grupos lógicos de limites que você configura.

Uma hierarquia pode incluir qualquer número de grupos de limites. Cada grupo de limites pode conter qualquer combinação dos seguintes tipos de limites:  

- Sub-rede IP  
- Nome do site do Active Directory  
- Prefixo IPv6  
- Intervalo de Endereços IP  

Os clientes da intranet avaliam seu local de rede atual e, em seguida, usam essas informações para identificar grupos de limites aos quais eles pertencem.  

Os clientes usam grupos de limites para:  

- **encontrar um site atribuído:** os grupos de limites permitem que clientes encontrem um site primário para atribuição de cliente. Esse comportamento também é conhecido como *atribuição automática de site*.  

- **encontrar determinadas funções do sistema de sites que eles possam usar:** Associe um grupo de limites com certas funções do sistema de sites. Em seguida, o site fornece clientes com essa lista de sistemas de site no grupo de limites. Os clientes usam esses sistemas de site para ações como a localização de conteúdo ou um ponto de gerenciamento mais próximo.  

Os clientes que estão na Internet ou configurados como clientes somente de Internet não usam informações de limites. Esses clientes não podem usar a atribuição automática de site. Eles podem baixar conteúdo de um ponto de distribuição baseado na Internet do seu site atribuído ou um ponto de distribuição baseado na nuvem.  

A partir da versão 1902, é possível associar um gateway de gerenciamento de nuvem (CMG) a um grupo de limites. Para saber mais, confira [Design de hierarquia do CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#hierarchy-design).<!--3640932-->


## <a name="BKMK_BoundaryBestPractices"></a> Recomendações

### <a name="use-a-mix-of-the-fewest-boundaries-that-meet-your-needs"></a>Use uma combinação do menor número de limites que atendem às suas necessidades

Use qualquer tipo de limite ou tipos que você escolher que funcione para o seu ambiente. Para simplificar suas tarefas de gerenciamento, use os tipos de limites que permitem que você use o menor número de limites que puder.

### <a name="avoid-overlapping-boundaries-for-automatic-site-assignment"></a>Evite a sobreposição de limites para atribuição automática de site

Embora cada grupo de limites dê suporte a atribuição de site e referência de sistema de sites, crie um conjunto separado de grupos de limites para usar apenas para atribuição de site. Verifique se cada limite em um grupo de limites não é membro de outro grupo de limites com uma atribuição de site diferente.

- Um único limite pode ser incluído em vários grupos de limites  

- Cada grupo de limite pode ser associado um site primário diferente para atribuição de site  

- Para um limite que seja um membro de dois grupos de limites diferentes com atribuições de site diferentes, os clientes selecionam aleatoriamente um site para entrar. Esse comportamento pode não ser para o site que você deseja que o cliente entre. Essa configuração é chamada de *limites sobrepostos*.  

    Os limites de sobreposição não são um problema para o local de conteúdo. Pode ser uma configuração útil que fornece aos clientes recursos adicionais ou locais de conteúdo que eles podem usar.  


## <a name="next-steps"></a>Próximas etapas

- [Definir locais de rede como limites](/sccm/core/servers/deploy/configure/boundaries)

- [Configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups)
