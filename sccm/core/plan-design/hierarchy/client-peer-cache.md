---
title: Cache de pares do cliente | System Center Configuration Manager
description: "Use cache de pares para locais de fonte de conteúdo do cliente durante a implantação de conteúdo com o System Center Configuration Manager."
ms.custom: na
ms.date: 12/05/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3329c3180899a4de96f5d9fed46f97744cf5e7da
ms.openlocfilehash: e983358e32502a130f95647a11cd73ff4bbef05f

---
# <a name="peer-cache-for-configuration-manager-clients"></a>Cache de pares para clientes do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Começando com o System Center Configuration Manager versão 1610, você pode usar o **Cache de pares** para ajudar a gerenciar a implantação de conteúdo para clientes em locais remotos. O cache de pares é uma solução interna do Configuration Manager para clientes compartilharem conteúdo com outros clientes diretamente do cache local.   

> [!TIP]  
> Com a versão 1610, o cache de pares e o painel de fontes de dados do cliente são recursos de pré-lançamento. Para habilitá-los, confira [Usar recursos de pré-lançamento de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

 -  Use as configurações do cliente para habilitar clientes para usar cache de pares.
 -  Para compartilhar conteúdo, ambos os clientes de cache de pares devem ser membros do grupo de limite do cliente que procura o conteúdo. Clientes de cache de pares em grupos de limites vizinhos não estão incluídos no pool de locais de origem de conteúdo disponíveis quando um cliente usa o fallback para buscar o conteúdo de um grupo de limites vizinho. Para obter mais informações sobre grupos de limite atuais e próximos, consulte [Grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 -  Cada tipo de conteúdo que é mantido no cache de um cliente do Configuration Manager pode ser servido a outros clientes que usam o cache de pares.
 -  O Cache de Mesmo Nível não substitui o uso de outras soluções como o BranchCache, mas ele trabalha lado a lado para fornecer a você mais opções para estender as soluções tradicionais de implantação de conteúdo, como pontos de distribuição. Essa solução ainda funciona como uma solução personalizada sem dependência do BranchCache, se você não habilitar ou não usar o Windows BranchCache.

Depois de implantar configurações do cliente que habilitam o cache de pares para uma coleção, os membros dessa coleção podem atuar como uma fonte de conteúdo de pares para outros clientes no mesmo grupo de limites:
 -  Um cliente que opera como fonte de conteúdo de pares enviará uma lista do conteúdo disponível que ele armazenou em cache para seu ponto de gerenciamento.
 -  Em seguida, quando o próximo cliente nesse grupo de limite solicita aquele conteúdo, cada fonte de cache de pares que tem o conteúdo é retornada como uma fonte de conteúdo potencial, juntamente com os pontos de distribuição e outros locais de origem de conteúdo nesse grupo de limites.
 -  Através do processo normal de operação, o cliente que procura o conteúdo seleciona uma fonte de conteúdo do pool de fontes fornecidas e prossegue para tentar obter o conteúdo.
 -  Se o fallback para um grupo de limites vizinho para conteúdo ocorrer, os locais de origem de conteúdo do cache de pares do grupo de limite de vizinho não serão adicionados ao pool do cliente de possíveis locais de origem de conteúdo.  

Mesmo que você possa fazer com que todos os clientes participem do cache de pares, é recomendável escolher somente os clientes que são mais adequados para serem fontes de cache de pares.  A adequação de clientes pode ser avaliada com base no tipo de chassi do cliente, espaço em disco, conectividade de rede e muito mais. Para obter mais informações que podem ajudá-lo a selecionar os melhores clientes para usar o cache de pares, consulte [este blog, por um consultor Microsoft](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

Para ajudar você a entender o uso do cache de pares, exiba o painel Fontes de Dados do Cliente. Veja o [Painel de fontes de dados do cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).


## <a name="requirements-and-considerations-for-peer-cache"></a>Requisitos e considerações para o cache de pares:
- É necessário configurar seu site com uma **Conta de Acesso à Rede** que tenha **Controle Total** da pasta de cache em cada cliente. Por padrão, a pasta é ***%windir%\ccmcache***.

- Os clientes só podem transferir conteúdo de clientes de cache de pares que estão em seu grupo de limites atual.

-   Como o limite atual de uma fonte de conteúdo do cache de pares é determinado pelo último envio de inventário de hardware daquele cliente, um cliente que usa um perfil móvel em um local de rede que está em um grupo de limites diferentes ainda poderá ser considerado um membro de seu grupo de limite anterior para fins de cache de pares. Isso pode resultar em uma fonte de conteúdo de cache de pares sendo oferecida a um cliente que não está em seu local de rede imediato. É recomendável excluir clientes, que estão sujeitos a essa configuração, da participação no cache de pares.

## <a name="to-configure-client-peer-cache-client-settings"></a>Para definir as configurações do cliente do Cache Par
1.  No console do Configuration Manager, vá para **Administração** > **Configurações do Cliente** e abra o objeto de configurações do cliente do dispositivo que deseja usar. Também é possível alterar o objeto de Configurações Padrão do Cliente.
2.  Na lista de configurações disponíveis, selecione **Configurações de Cache do Cliente**.
3.  Defina **Habilitar cliente do Configuration Manager em um SO completo para compartilhar conteúdo** como **Sim**.
4.  Defina as seguintes configurações para definir as portas que você deseja usar para o cache de pares:  
  -  **Porta para difusão de rede inicial**
  -  **Habilitar HTTPS para comunicação de par do cliente**
  -  **Porta para download de conteúdo de pares (HTTP/HTTPS)**

Em cada computador habilitado para o cache de pares, se o Firewall do Windows estiver em uso, o Configuration Manager o configura para permitir o uso de portas que você configurar.



<!--HONumber=Dec16_HO1-->


