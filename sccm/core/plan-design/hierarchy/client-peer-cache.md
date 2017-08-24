---
title: Cache de pares do cliente | System Center Configuration Manager
description: "Use cache de pares para locais de fonte de conteúdo do cliente durante a implantação de conteúdo com o System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 89fcd16887ae77299f9d18472ee6a1ba56794eca
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Cache de pares para clientes do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Começando com o System Center Configuration Manager versão 1610, você pode usar o **Cache de pares** para ajudar a gerenciar a implantação de conteúdo para clientes em locais remotos. O Cache de Pares é uma solução interna do Configuration Manager que habilita os clientes a compartilharem conteúdo com outros clientes diretamente do cache local.   

> [!TIP]  
> Apresentado com a versão 1610, o cache de pares e o painel de fontes de dados do cliente são recursos de pré-lançamento. Para habilitá-los, confira [Usar recursos de pré-lançamento de atualizações](/sccm/core/servers/manage/pre-release-features).

## <a name="overview"></a>Visão geral
Um cliente de Cache de mesmo nível é um cliente do Configuration Manager que está habilitado para uso do Cache de mesmo nível. Um cliente de Cache de mesmo nível que possui conteúdo para compartilhamento com outros clientes é uma fonte de Cache de mesmo nível.
 -  Use as configurações do cliente para habilitar clientes para usar cache de pares.
 -  Para compartilhar o conteúdo como uma fonte de Cache de mesmo nível, um cliente de Cache de mesmo nível:
    -  Deve ingressar no domínio. No entanto, um cliente não associado a um domínio pode obter o conteúdo de um domínio ingressado na fonte de Cache de mesmo nível.
    -  Deve ser membro do grupo de limites atual do cliente que está procurando o conteúdo. Um cliente de Cache de mesmo nível em um grupo de limites vizinho não está incluído no pool de locais de origem de conteúdo disponíveis quando um cliente usa o fallback para buscar o conteúdo de um grupo de limites vizinho. Para obter mais informações sobre grupos de limite atuais e próximos, consulte [Grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 - Todo tipo de conteúdo mantido no cache de um cliente do Configuration Manager pode ser servido a outros clientes usando o Cache de Pares.
 -  O Cache de Pares não substitui o uso de outras soluções como o BranchCache, em vez disso, ele funciona lado a lado com ele para fornecer a você mais opções para estender as soluções tradicionais de implantação de conteúdo, como os pontos de distribuição. Trata-se de uma solução personalizada sem dependência do BranchCache, portanto se você não habilitar nem usar o Windows BranchCache, ele ainda funcionará.

### <a name="operations"></a>Operações

Depois de implantar configurações do cliente que habilitam o cache de pares para uma coleção, os membros dessa coleção podem atuar como uma fonte de conteúdo de pares para outros clientes no mesmo grupo de limites:
 -  Um cliente que opera como fonte de conteúdo de pares envia uma lista do conteúdo disponível armazenado em cache para o ponto de gerenciamento.
 -  Em seguida, quando o próximo cliente nesse grupo de limite solicita aquele conteúdo, cada fonte de cache de pares que tem o conteúdo é retornada como uma fonte de conteúdo potencial, juntamente com os pontos de distribuição e outros locais de origem de conteúdo nesse grupo de limites.
 -  De acordo com o processo normal de operação, o cliente que procura o conteúdo seleciona uma fonte de conteúdo do pool de fontes fornecidas e tenta obter o conteúdo.

> [!NOTE]
> Se o fallback para um grupo de limites vizinho para conteúdo ocorrer, as localizações das fontes de conteúdo do Cache de Pares no grupo de limites vizinho não serão adicionadas ao pool de possíveis localizações de fontes de conteúdo do cliente.  


Mesmo que seja possível fazer com que todos os clientes participem como fonte do cache de pares, é recomendado escolher somente os clientes mais adequados para serem fontes de cache de pares.  A adequação dos clientes pode ser avaliada com base no tipo de chassi do cliente, no espaço em disco, na conectividade de rede e muito mais. Para obter mais informações que podem ajudar você a selecionar os melhores clientes para usar o Cache de Pares, consulte [este blog de um consultor Microsoft](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

**Acesso limitado a uma fonte de cache de pares**  
A partir da versão 1702, um computador de origem de cache de pares rejeitará uma solicitação de conteúdo quando o computador de origem do cache de pares atender a qualquer uma das seguintes condições:  
  -  Está no modo de bateria fraca.
  -  A carga de CPU excede 80% no momento em que o conteúdo é solicitado.
  -  A E/S de disco tem um *AvgDiskQueueLength* que excede 10.
  -  Não há mais conexões disponíveis para o computador.   

Você pode definir essas configurações usando a classe do WMI do servidor de configuração de cliente para o recurso de origem par (*SMS_WinPEPeerCacheConfig*) quando usar o SDK do System Center Configuration Manager.

Quando o computador rejeita uma solicitação de conteúdo, o computador solicitante continuará a procurar conteúdo de fontes alternativas em seu pool de locais de fonte de conteúdo disponíveis.   



### <a name="monitoring"></a>monitoramento   
Para ajudar você a entender o uso do cache de pares, exiba o painel Fontes de Dados do Cliente. Veja o [Painel de fontes de dados do cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

A partir da versão 1702, você pode usar três relatórios para exibir o uso de cache de pares. No console, vá até **Monitoramento** > **Relatórios** > **Relatórios**. Todos os relatórios têm um tipo de **Conteúdo de Distribuição de Software**:
1.  **Rejeição de conteúdo de origem de cache de pares**:  
Use esse relatório para entender com que frequência as fontes de cache de pares em um grupo de limites rejeitou uma solicitação de conteúdo.
 - **Problema conhecido:** ao fazer uma busca detalhada nos resultados como *MaxCPULoad* ou *MaxDiskIO*, você poderá receber um erro que sugere que o relatório ou os detalhes não podem ser encontrados. Para solucionar esse problema, use os seguintes dois relatórios que mostram os resultados diretamente.

2. **Rejeição de conteúdo de origem do cache de pares por condição**:  
Use esse relatório para entender os detalhes de rejeição para um grupo de limites ou tipo de rejeição especificado. É possível especificar

  - **Problema conhecido:** não é possível selecionar a partir de parâmetros disponíveis, é preciso digitá-los manualmente. Insira os valores de *Nome do Grupo de Limites* e *Tipo de Rejeição* como visto no primeiro relatório. Por exemplo, para *Tipo de Rejeição*, você pode inserir *MaxCPULoad* ou *MaxDiskIO*.

3. **Detalhes da rejeição de conteúdo de origem de cache de pares**:   
  Use esse relatório para entender o conteúdo que estava sendo solicitado quando ele foi rejeitado.

 - **Problema conhecido:** não é possível selecionar a partir de parâmetros disponíveis, é preciso digitá-los manualmente. Insira o valor para *Tipo de Rejeição* conforme exibido no primeiro relatório (rejeição de conteúdo de fonte de cache de pares) e insira a *ID de Recurso* para a fonte de conteúdo sobre a qual você deseja obter mais informações.  Para localizar a ID de recurso da fonte de conteúdo:  

    1. Localizar o nome do computador que é exibido como a *Fonte de cache de pares* nos resultados do 2º relatório (rejeição de conteúdo de fonte de cache de pares por condição).  
    2. Em seguida, vá para **Ativos e Conformidade** > **Dispositivos** e procure o nome desse computador. Use o valor da coluna de ID de Recurso.  


## <a name="requirements-and-considerations-for-peer-cache"></a>Requisitos e considerações do Cache de Pares
-   O Cache de Pares tem suporte em qualquer sistema operacional Windows com suporte como cliente do Configuration Manager. Não há suporte para sistemas operacionais não Windows para o Cache de Pares.

-   Os clientes só podem transferir conteúdo de clientes de cache de pares que estão em seu grupo de limites atual.

-   Antes da versão 1706, cada site em que os clientes usam Cache Par deve ser configurado com uma [Conta de Acesso à Rede](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account). A partir da versão 1706, essa conta não é mais necessária, com uma exceção.  A exceção é quando um cliente usa o cache de pares para obter e executar uma sequência de tarefas no Centro de Software, e essa sequência de tarefas reinicia o cliente no WinPE.  Nesse cenário, o cliente ainda precisa da Conta de Acesso à Rede quando estiver no WinPE, para que possa acessar a fonte de cache de pares para obter o conteúdo.

    Quando é necessária, a Conta de Acesso à Rede é usada pelo computador de origem do Cache Par para autenticar solicitações de download de colegas e exige apenas permissões de usuário de domínio para essa finalidade.

-   Como o limite atual de uma fonte de conteúdo do Cache de Pares é determinado pelo último envio de inventário de hardware daquele cliente, um cliente que usa um perfil móvel para um local de rede e que está em um grupo de limites diferente ainda poderá ser considerado um membro de seu grupo de limites anterior para o Cache de Pares. Isso pode resultar em uma fonte de conteúdo de cache de pares sendo oferecida a um cliente que não está em seu local de rede imediato. É recomendado excluir os clientes que estão sujeitos a essa configuração de participarem como uma fonte do Cache de Pares.

## <a name="to-configure-client-peer-cache-client-settings"></a>Para definir as configurações do cliente do Cache Par
1.  No console do Configuration Manager, acesse **Administração** > **Configurações do Cliente** e abra o objeto de configurações do cliente do dispositivo que deseja usar. Também é possível alterar o objeto de Configurações Padrão do Cliente.
2.  Na lista de configurações disponíveis, escolha **Configurações do Cache do Cliente**.
3.  Defina **Habilitar cliente do Configuration Manager em um SO completo para compartilhar conteúdo** como **Sim**.
4.  Defina as seguintes configurações para definir as portas que você deseja usar para o cache de pares:  
  -  **Porta para difusão de rede inicial**
  -  **Habilitar HTTPS para comunicação de par do cliente**
  -  **Porta para download de conteúdo de pares (HTTP/HTTPS)**

Em cada computador habilitado para o Cache de Pares, se o Firewall do Windows estiver em uso, o Configuration Manager o configurará para permitir o uso das portas que você configurar.
