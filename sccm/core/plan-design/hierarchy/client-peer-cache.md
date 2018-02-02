---
title: Cache de pares do cliente
titleSuffix: Configuration Manager
description: "Use cache de pares para locais de fonte de conteúdo do cliente durante a implantação de conteúdo com o System Center Configuration Manager."
ms.custom: na
ms.date: 12/07/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: 
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 424f4030f2dd2a337a29d48ca831fa3a791de610
ms.sourcegitcommit: e121d8d3dd82b9f2dde2cb5206cbee602ab8e107
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Cache de pares para clientes do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Começando com o System Center Configuration Manager versão 1610, você pode usar o **Cache de pares** para ajudar a gerenciar a implantação de conteúdo para clientes em locais remotos. O Cache de Pares é uma solução interna do Configuration Manager que habilita os clientes a compartilharem conteúdo com outros clientes diretamente do cache local.   

> [!TIP]  
> Esse recurso foi introduzido na versão 1610 como um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1710, esse recurso deixou de ser um recurso de pré-lançamento.

## <a name="overview"></a>Visão geral
Um cliente de Cache de mesmo nível é um cliente do Configuration Manager que está habilitado para uso do Cache de mesmo nível. Um cliente de Cache de mesmo nível que possui conteúdo para compartilhamento com outros clientes é uma fonte de Cache de mesmo nível.
 -  Use as configurações do cliente para habilitar clientes para usar cache de pares.
 -  Para compartilhar o conteúdo como uma fonte de Cache de mesmo nível, um cliente de Cache de mesmo nível:
    -  Deve ingressar no domínio. No entanto, um cliente não associado a um domínio pode obter o conteúdo de um domínio ingressado na fonte de Cache de mesmo nível.
    -  Deve ser membro do grupo de limites atual do cliente que está procurando o conteúdo. Quando um cliente usa o fallback para buscar o conteúdo de um grupo de limites vizinho, a lista de locais de origem de conteúdo não inclui um cliente de Cache Par em um grupo de limites vizinho. Para obter mais informações sobre grupos de limite atuais e próximos, consulte [Grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 - O cliente do Configuration Manager serve todo tipo de conteúdo mantido no cache a outros clientes usando o Cache Par. Esse conteúdo inclui arquivos do Office 365 e arquivos de instalação expressa.<!--SMS.500850-->
 -  O Cache Par não substitui o uso de outras soluções como o BranchCache. O Cache Par funciona junto com outras soluções para dar a você mais opções para estender as soluções tradicionais de implantação de conteúdo, tais como pontos de distribuição. O Cache Par é uma solução personalizada sem nenhuma dependência do BranchCache.  Se você não habilitar ou usar o Windows BranchCache, o Cache Par ainda funcionará.

### <a name="operations"></a>Operações

Para habilitar o Cache Par, implante as configurações do cliente em uma coleção. Os membros dessa coleção agem então como uma fonte de conteúdo par para outros clientes no mesmo grupo de limites.
 -  Um cliente que opera como fonte de conteúdo de pares envia uma lista do conteúdo disponível armazenado em cache para o ponto de gerenciamento.
 -  Quando o próximo cliente no grupo de limites solicita esse conteúdo, cada fonte de cache par, que tem o conteúdo e está online, é retornada na lista de possíveis fontes de conteúdo. Essa lista também inclui os pontos de distribuição e outros locais de fonte de conteúdo nesse grupo de limites.
 -  Para o processo normal, o cliente que está procurando o conteúdo seleciona uma fonte na lista fornecida. O cliente tenta então obter o conteúdo.

> [!NOTE]
> Se o cliente faz fallback para um grupo de limites vizinho para conteúdo, ele não adiciona as localizações das fontes de conteúdo do Cache de Pares no grupo de limites vizinho à lista de possíveis localizações de fontes de conteúdo.  


A prática recomendada é escolher apenas os clientes mais adequados como origens de cache par. Avalie a adequação de cliente com base em atributos como tipo de chassi, espaço em disco e conectividade de rede. Para obter mais informações que podem ajudar você a selecionar os melhores clientes para usar o Cache de Pares, consulte [este blog de um consultor Microsoft](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

**Acesso limitado a uma fonte de cache de pares**  
Desde a versão 1702, um computador de origem de cache de pares rejeita solicitações de conteúdo quando o computador de origem do cache de pares atende a qualquer uma das seguintes condições:  
  -  Está no modo de bateria fraca.
  -  A carga de CPU excede 80% no momento em que o conteúdo é solicitado.
  -  A E/S de disco tem um *AvgDiskQueueLength* que excede 10.
  -  Não há mais conexões disponíveis para o computador.   

Definir essas configurações usando a classe do WMI do servidor de configuração de cliente para o recurso de origem par (*SMS_WinPEPeerCacheConfig*) no SDK do Configuration Manager.

Quando o computador rejeita uma solicitação de conteúdo, o computador solicitante continua a procurar conteúdo da lista de locais de fonte de conteúdo disponíveis.   



### <a name="monitoring"></a>monitoramento   
Para ajudar você a entender o uso do cache de pares, exiba o painel Fontes de Dados do Cliente. Veja o [Painel de fontes de dados do cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

A partir da versão 1702, você pode usar três relatórios para exibir o uso de cache de pares. No console, vá até **Monitoramento** > **Relatórios** > **Relatórios**. Todos os relatórios têm um tipo de **Conteúdo de Distribuição de Software**:
1.  **Rejeição de conteúdo de origem de cache de pares**:  
Use esse relatório para entender com que frequência as fontes de cache de pares em um grupo de limites rejeitam uma solicitação de conteúdo.
 - **Problema conhecido:** ao fazer uma busca detalhada nos resultados como *MaxCPULoad* ou *MaxDiskIO*, você poderá receber um erro que sugere que o relatório ou os detalhes não podem ser encontrados. Para solucionar esse problema, use os seguintes dois relatórios que mostram os resultados diretamente.

2. **Rejeição de conteúdo de origem do cache de pares por condição**:  
Use esse relatório para entender os detalhes de rejeição para um grupo de limites ou tipo de rejeição especificado. É possível especificar

  - **Problema conhecido:** não é possível selecionar a partir de parâmetros disponíveis, é preciso digitá-los manualmente. Insira os valores de *Nome do Grupo de Limites* e *Tipo de Rejeição* como visto no primeiro relatório. Por exemplo, para *Tipo de Rejeição*, você pode inserir *MaxCPULoad* ou *MaxDiskIO*.

3. **Detalhes da rejeição de conteúdo de origem de cache de pares**:   
  Use esse relatório para entender o conteúdo que o cliente estava solicitando quando ele foi rejeitado.

 - **Problema conhecido:** não é possível selecionar a partir de parâmetros disponíveis, é preciso digitá-los manualmente. Insira o valor para *Tipo de Rejeição* conforme exibido no relatório de **Rejeição do conteúdo de origem do cache par**. Em seguida, digite a *ID de Recurso* para a fonte de conteúdo sobre a qual você deseja obter mais informações.  Para localizar a ID de recurso da fonte de conteúdo:  

    1. Localizar o nome do computador que é exibido como a *Origem de cache par* nos resultados da **Rejeição de conteúdo de fonte de cache par por condição**.  
    2. Em seguida, vá para **Ativos e Conformidade** > **Dispositivos** e procure o nome desse computador. Use o valor da coluna de ID de Recurso.  


## <a name="requirements-and-considerations-for-peer-cache"></a>Requisitos e considerações do Cache de Pares
-   O Cache de Pares tem suporte em qualquer sistema operacional Windows com suporte como cliente do Configuration Manager. Não há suporte para sistemas operacionais não Windows para o Cache de Pares.

-   Os clientes só podem transferir conteúdo de clientes de cache de pares que estão em seu grupo de limites atual.

-   Antes da versão 1706, cada site em que os clientes usam Cache Par deve ser configurado com uma [Conta de Acesso à Rede](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account). A partir da versão 1706, essa conta não é mais necessária, com uma exceção.  O cenário de exceção é quando um cliente habilitado para cache par executa uma sequência de tarefas no Centro de Software e essa sequência de tarefas reinicializa para uma imagem de inicialização. Nesse cenário, o cliente ainda exige a Conta de Acesso à Rede. Quando o cliente está no Windows PE, ele usa a Conta de Acesso à Rede para obter o conteúdo da origem do cache par.

    Quando necessário, o computador de origem do Cache Par usa a Conta de Acesso à Rede para autenticar solicitações de download dos pares. Essa conta requer somente permissões de usuário de domínio para essa finalidade.

-   O último envio de inventário de hardware do cliente determina o limite atual de uma fonte de conteúdo do Cache Par. Um cliente que usa perfil móvel para um grupo de limites diferente ainda pode ser um membro de seu grupo de limites anterior para fins de Cache Par. Esse comportamento faz com que seja oferecida ao cliente uma fonte de conteúdo de Cache Par que não está no local de rede imediato desse cliente. É recomendado excluir os clientes que estão sujeitos a essa configuração de participarem como uma fonte do Cache de Pares.
-    Da versão 1706 em diante, o cliente de cache par primeiro valida que a fonte de conteúdo de cache par está online antes de tentar baixar conteúdo. <!--sms.498675-->

## <a name="to-configure-client-peer-cache-client-settings"></a>Para definir as configurações do cliente do Cache Par
Para obter mais informações sobre como definir configurações do cliente, veja [Configurações de cache de cliente](/sccm/core/clients/deploy/about-client-settings#client-cache-settings). Para obter mais informações, consulte [Como definir as configurações de cliente](/sccm/core/clients/deploy/configure-client-settings).

Em clientes habilitados para cache par que usam o Firewall do Windows, o Configuration Manager configura as portas de firewall que você especifica nas configurações do cliente.
