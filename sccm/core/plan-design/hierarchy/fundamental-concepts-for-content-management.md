---
title: Conceitos básicos do gerenciamento de conteúdo
titleSuffix: Configuration Manager
description: Use as ferramentas e as opções do Configuration Manager para gerenciar o conteúdo implantado.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
caps.latest.revision: 28
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0595e34d096b2d7f6450b3255bae03ae3aa57862
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2018
---
# <a name="fundamental-concepts-for-content-management-in-system-center-configuration-manager"></a>Conceitos fundamentais para o gerenciamento de conteúdo no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Configuration Manager dá suporte a um sistema robusto de ferramentas e opções para gerenciar o conteúdo implantado como aplicativos, pacotes, atualizações de software e implantações de sistema operacional. O Configuration Manager armazena o conteúdo em servidores do site e pontos de distribuição. Esse conteúdo exige uma grande quantidade de largura de banda da rede quando está sendo transferido entre locais. Para planejar e usar a infraestrutura de gerenciamento de conteúdo com eficiência, recomendamos que você entenda as opções e configurações disponíveis. Em seguida, considere como usá-las para que elas sejam ajustadas da melhor forma às suas necessidades de implantação de conteúdo e ambiente de rede.  

> [!TIP]    
> Para obter mais informações sobre o processo de distribuição de conteúdo e para encontrar ajuda no diagnóstico e na resolução de problemas gerais de distribuição de conteúdo, consulte [Noções básicas e solução de problemas de distribuição de conteúdo no Microsoft Configuration Manager ](https://support.microsoft.com/help/4000401/content-distribution-in-mcm).

Os tópicos a seguir são os principais conceitos do gerenciamento de conteúdo. Quando um conceito requer informações adicionais ou complexas, são fornecidos links para direcioná-lo a esses detalhes.



## <a name="accounts-used-for-content-management"></a>Contas usadas para gerenciamento de conteúdo  
 As contas a seguir podem ser usadas com o gerenciamento de conteúdo:  

-   **Conta de acesso à rede**: usada pelos clientes para se conectar a uma distribuição ponto e acessar o conteúdo. Por padrão, a conta de computador será tentada primeiro.  

     Essa conta também é usada pelos pontos de distribuição pull para baixar o conteúdo de um ponto de distribuição de origem em uma floresta remota.  

-   **Conta de acesso ao pacote**: por padrão, o Configuration Manager concede acesso ao conteúdo em um ponto de distribuição a usuários e administradores de contas de acesso genérico. No entanto, você pode configurar permissões adicionais para restringir o acesso.   

-   **Conta de conexão multicast**: usada para implantações de sistema operacional.  

Para obter mais informações sobre essas contas, consulte [Gerenciar contas para acessar conteúdo](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).



## <a name="bandwidth-throttling-and-scheduling"></a>Limitação e agendamento de largura de banda  
 Tanto a limitação quanto o agendamento são opções para ajudar a controlar quando o conteúdo é distribuído por um servidor de site para pontos de distribuição. Essas funcionalidades são semelhantes, mas não estão diretamente relacionadas aos controles de largura de banda para replicação baseada em arquivo site a site.  

 Para obter mais informações, consulte [Gerenciar largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="binary-differential-replication"></a>Replicação diferencial binária  
 A BDR (replicação diferencial binária) é um pré-requisito para os pontos de distribuição. Às vezes, ela é conhecida como replicação delta. Quando você está distribuindo atualizações para o conteúdo implantado anteriormente em outros sites ou em pontos de distribuição remotos, a BDR é usada automaticamente para reduzir a largura de banda.  

 A BDR minimiza a largura de banda da rede usada para enviar atualizações para o conteúdo distribuído. Ela reenvia somente o conteúdo novo ou alterado, em vez de enviar todo o conjunto de arquivos de fonte de conteúdo sempre que você altera esses arquivos.  

 Quando a BDR é usada, o Configuration Manager identifica as alterações ocorridas nos arquivos de origem em cada conjunto de conteúdo distribuído anteriormente.  

-   Quando os arquivos no conteúdo de origem são alterados, o site cria uma nova versão incremental do conjunto de conteúdo. Ele então replica apenas os arquivos alterados nos sites e pontos de distribuição de destino. Um arquivo é considerado alterado se ele é renomeado ou movido, ou se o conteúdo dele é alterado. Por exemplo, se você substituir um único arquivo de driver de um pacote de driver distribuído anteriormente para vários sites, apenas o arquivo de driver alterado será replicado.  

-   O Configuration Manager dá suporte a até cinco versões incrementais de um conjunto de conteúdo antes de reenviar o todo o conjunto do conteúdo. Após a quinta atualização, a próxima alteração no conjunto de conteúdo faz com que o site crie uma nova versão do conjunto de conteúdo. O Configuration Manager distribui a nova versão do conteúdo definido para substituir o conjunto anterior e qualquer uma de suas versões incrementais. Depois que o novo conjunto de conteúdo é distribuído, as alterações incrementais seguintes nos arquivos de origem são novamente replicadas pela BDR.  

A BDR tem suporte entre cada site pai e filho de uma hierarquia. Há suporte para a BDR em um site entre o servidor do site e seus pontos de distribuição normais. No entanto, os pontos de distribuição pull e os pontos de distribuição baseados em nuvem não dão suporte à BDR para transferência de conteúdo. Os pontos de distribuição pull dão suporte a deltas de nível de arquivo, transferindo novos arquivos, mas não os blocos em um arquivo.

Aplicativos sempre usam replicação diferencial binária. A BDR é opcional para pacotes e não está habilitada por padrão. Para usar a BDR para pacotes, habilite essa funcionalidade em cada pacote. Selecione a opção **Habilitar replicação diferencial binária** ao criar ou editar um pacote.   



## <a name="branchcache"></a>BranchCache  
 O [BranchCache](/windows-server/networking/branchcache/branchcache) é uma tecnologia do Windows. Os clientes que dão suporte ao BranchCache e baixaram uma implantação configurada para o Branch Cache servem, em seguida, como uma fonte de conteúdo para outros clientes habilitados para o BranchCache.  

 Por exemplo, você tem um ponto de distribuição que executa o Windows Server 2012 ou posterior e é configurado como um servidor do BranchCache. Quando o primeiro cliente habilitado para BranchCache solicita o conteúdo desse servidor, o cliente baixa esse conteúdo e armazena-o em cache.  

- Esse cliente então disponibiliza o conteúdo aos outros clientes habilitados para o Branch Cache na mesma sub-rede que também armazena o conteúdo em cache.  
- Os outros clientes na mesma sub-rede não precisam baixar o conteúdo do ponto de distribuição.  
- O conteúdo é distribuído entre vários clientes para transferências futuras.  



## <a name="delivery-optimization"></a>Otimização de Entrega
<!-- 1324696 -->
Você usa os grupos de limites do Configuration Manager para definir e regular a distribuição de conteúdo em sua rede corporativa e para escritórios remotos. A [Otimização de Entrega do Windows](/windows/deployment/update/waas-delivery-optimization) é uma tecnologia ponto-a-ponto baseada na nuvem para compartilhar conteúdo entre dispositivos do Windows 10. A partir da versão 1802, configure a Otimização de Entrega para que ela use os grupos de limites ao compartilhar o conteúdo entre pares. As configurações do cliente aplicam o identificador do grupo de limites como o identificador do grupo da Otimização de Entrega no cliente. Quando o cliente se comunica com o serviço de nuvem da Otimização de Entrega, ele usa esse identificador para localizar os pares com o conteúdo desejado. Para obter mais informações, consulte as configurações do cliente [Otimização de entrega](/sccm/core/clients/deploy/about-client-settings#delivery-optimization).



## <a name="peer-cache"></a>Cache de Pares
O cache par do cliente ajuda você a gerenciar a implantação de conteúdo nos clientes em locais remotos. O cache par é uma solução interna do Configuration Manager que o os clientes podem usar para compartilhar conteúdo com outros clientes diretamente do cache local.

Depois de implantar as configurações do cliente que habilitam o cache par em uma coleção, os membros dessa coleção podem atuar como uma fonte de conteúdo par para outros clientes no mesmo grupo de limites.

Para obter mais informações, consulte [Cache de pares para clientes do Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).



## <a name="windows-pe-peer-cache"></a>Cache de sistemas pares do Windows PE
Quando você implanta um novo sistema operacional com o Configuration Manager, os computadores que executam a sequência de tarefas podem usar o cache par do Windows PE. Eles baixam o conteúdo de uma origem de cache par, em vez de um ponto de distribuição. Esse comportamento ajuda a minimizar o tráfego de WAN em cenários de filial em que não há nenhum ponto de distribuição local.

Para obter mais informações, consulte [Cache de pares do Windows PE](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).



## <a name="client-locations"></a>Locais do cliente  
 Estes são os locais dos quais os clientes acessam conteúdo:  

-   **Intranet** (local):  

    -   Pontos de distribuição podem usar HTTP ou HTTPs.  

    -   Apenas use um ponto de distribuição baseado em nuvem para fallback quando os pontos de distribuição locais estiverem indisponíveis.  

-   **Internet**:  

    -   Requer que os pontos de distribuição aceitem HTTPS.  

    -   Pode usar um ponto de distribuição baseado em nuvem para fallback.  

-   **Grupo de trabalho**:  

    -   Requer que os pontos de distribuição aceitem HTTPS.  

    -   Pode usar um ponto de distribuição baseado em nuvem para fallback.  



## <a name="content-library"></a>Biblioteca de conteúdo  
 A biblioteca de conteúdo é o armazenamento de instância única do conteúdo no Configuration Manager. Essa biblioteca reduz o tamanho geral do conteúdo distribuído.  

- Saiba mais sobre a [biblioteca de conteúdo](../../../core/plan-design/hierarchy/the-content-library.md).
- Use a [ferramenta de limpeza da biblioteca de conteúdo](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) para remover o conteúdo que não está mais associado a um aplicativo.  



## <a name="distribution-points"></a>Pontos de distribuição  
 O Configuration Manager usa pontos de distribuição para armazenar arquivos necessários para que o software seja executado em computadores cliente. Os clientes devem ter acesso a pelo menos um ponto de distribuição do qual poderão baixar os arquivos para o conteúdo que você implanta.  

 O ponto de distribuição (não especializado) básico é conhecido como ponto de distribuição padrão. Há duas variações do ponto de distribuição padrão que recebem atenção especial:  

-   **Ponto de distribuição de pull**: uma variação de um ponto de distribuição em que o ponto de distribuição obtém conteúdo de outro ponto de distribuição (um ponto de distribuição de origem). Esse processo é semelhante a como os clientes baixam o conteúdo dos pontos de distribuição. Os pontos de distribuição de pull podem ajudar a evitar gargalos de largura de banda de rede que ocorrem quando o servidor do site deve distribuir conteúdo diretamente para cada ponto de distribuição. [Use um ponto de distribuição pull](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

-   **Ponto de distribuição baseado em nuvem**: uma variação de um ponto de distribuição instalado no Microsoft Azure. [Saiba como planejar o uso de um ponto de distribuição baseado em nuvem](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md).  


Os pontos de distribuição padrão dão suporte a uma variedade de recursos e configurações:  

- Use controles como **agendamentos** ou **limitação da largura de banda** para ajudar a controlar essa transferência.  
- Use outras opções, incluindo **conteúdo pré-teste** e **pontos de distribuição pull**, para minimizar e controlar o consumo de rede. 
- O **BranchCache**, o **cache par** e a **Otimização de Entrega** são tecnologias ponto a ponto para reduzir a largura de banda da rede usada quando o conteúdo é implantado.  
- Existem diferentes configurações para implantações de sistema operacional, como **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** e **[Multicast](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)**
- Opções de **dispositivos móveis**   
  
  
Pontos de distribuição de pull em baseados em nuvem dão suporte a muitas dessas mesmas configurações, mas têm limitações específicas a cada variação de ponto de distribuição.  



## <a name="distribution-point-groups"></a>Grupos de pontos de distribuição  
 Os grupos de pontos de distribuição são agrupamentos lógicos de pontos de distribuição que podem simplificar a distribuição de conteúdo.  

 Para obter mais informações, consulte [Gerenciar grupos de pontos de distribuição](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).



## <a name="distribution-point-priority"></a>Prioridade de ponto de distribuição  
 O valor de prioridade do ponto de distribuição se baseia em quanto tempo demorou para transferir implantações anteriores para aquele ponto de distribuição.  

-   Esse valor tem um ajuste automático. Ele é definido em cada ponto de distribuição para ajudar o Configuration Manager a transferir o conteúdo mais rapidamente para mais pontos de distribuição.  

-   Quando você distribui o conteúdo para vários pontos de distribuição ao mesmo tempo, ou para um grupo de pontos de distribuição, o site envia primeiro o conteúdo para o servidor com a prioridade mais alta. Em seguida, ele envia esse mesmo conteúdo a um ponto de distribuição com uma prioridade mais baixa.  

-   A prioridade de ponto de distribuição não substitui a prioridade de distribuição para pacotes. A prioridade de pacote continua sendo o fator decisivo de quando o site envia um conteúdo diferente.  

Por exemplo, você tem um pacote que tem uma alta prioridade de pacote. Distribua-o para um servidor com uma prioridade baixa de ponto de distribuição. Esse pacote com prioridade alta sempre é transferido antes de um pacote que tem uma prioridade mais baixa. A prioridade de pacote se aplica mesmo se o site distribui os pacotes de prioridade mais baixa para servidores com prioridades mais altas de ponto de distribuição.

A prioridade alta do pacote garante que o Configuration Manager distribua esse conteúdo para os pontos de distribuição antes de enviar os pacotes com uma prioridade mais baixa.  

> [!NOTE]  
>  Pontos de distribuição de recepção também usam um conceito de prioridade para ordenar a sequência dos seus pontos de distribuição de origem.  
>   
>  -   A prioridade de ponto de distribuição para transferências de conteúdo ao servidor é diferente da prioridade usada pelos pontos de distribuição pull. Os pontos de distribuição pull usam sua prioridade quando pesquisam um conteúdo em um ponto de distribuição de origem.  
>  -   Para obter mais informações, consulte [Usar um ponto de distribuição pull](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).  



## <a name="fallback"></a>Fallback  
 Várias coisas mudaram com o Configuration Manager Branch Atual, na forma como os clientes encontram um ponto de distribuição que tem conteúdo, incluindo fallback. 

Os clientes que não conseguem encontrar o conteúdo em um ponto de distribuição associado a seu grupo de limite atual fazem fallback para usar locais de fonte de conteúdo associados a grupos de limites vizinhos. Para ser usado para fallback, um grupo de limites vizinho deve ter uma relação definida com o grupo de limite atual do cliente. Essa relação inclui um tempo configurado que deve decorrer antes que um cliente que não consegue encontrar o conteúdo localmente inclua fontes de conteúdo do grupo de limites vizinho como parte de sua pesquisa.

Os conceitos de pontos de distribuição preferenciais não são mais usados e as configurações para **Permitir fallback para locais de origem de conteúdo** não estão mais disponíveis ou nem são impostas.

Para obter mais informações, consulte [Grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

<!--
**Version 1511, 1602, and 1606**   
Fallback settings are related to the use of **preferred distribution points** and to content source locations that are used by clients.

-   By default, clients only download content from a preferred distribution point (one that is associated with the client's boundary groups).  

-   However, when a distribution point is configured with **Allow clients to use this site system as a fallback source location for content**, that distribution point is only offered as a valid content source to any client that can't get a deployment from one of its preferred distribution points.  

For information about the different content location and fallback scenarios, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). For information about boundary groups, see [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).
-->



## <a name="network-bandwidth"></a>Largura de banda da rede  
 Para ajudar a gerenciar a quantidade de largura de banda de rede usada quando você distribui conteúdo, use as seguintes opções:  

-   **Conteúdo pré-teste**: transferência de conteúdo para um ponto de distribuição sem a distribuição do conteúdo pela rede.  

-   **Agendamento e limitação**: configurações que ajudam a controlar quando e como o conteúdo é distribuído aos pontos de distribuição.  

Para obter mais informações, consulte [Gerenciar largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="network-connection-speed-to-content-source"></a>Velocidade de conexão de rede até a fonte de conteúdo  
 Várias coisas mudaram com o Configuration Manager Branch Atual, na forma como os clientes encontram um ponto de distribuição que tem conteúdo. Essas alterações incluem a velocidade da rede para uma fonte de conteúdo. 

Velocidades de conexão de rede que definem um ponto de distribuição como **Rápido** ou **Lento** não são mais usadas. Em vez disso, cada sistema de sites associado a um grupo de limites é tratado da mesma forma.

Para obter mais informações, consulte [Grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

<!--
**Version 1511, 1602, and 1606**   
 You can configure the network connection speed of each distribution point in a boundary group:  

-   Clients use this value when they connect to the distribution point.

-   By default, the network connection speed is configured as **Fast**, but it can also be set as **Slow**.  

-   The **network connection speed**, along with the configuration of a deployment, determine if a client can download content from a distribution point when the client is in an associated boundary group  

For information about the different content location and fallback scenarios, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). For information about boundary groups, see [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).
-->



## <a name="on-demand-content-distribution"></a>Distribuição de conteúdo sob demanda  
 A distribuição de conteúdo sob demanda é uma opção para implantações de aplicativos e pacotes individuais. Com essa opção é possível distribuir conteúdo sob demanda para servidores preferenciais.  

-   Para habilitar essa configuração em uma implantação, habilite **Distribuir o conteúdo deste pacote para pontos de distribuição preferenciais**.  

-   Quando essa opção é habilitada para uma implantação e um cliente tenta solicitar esse conteúdo, mas ele não está disponível em nenhum um dos pontos de distribuição preferenciais de clientes, o Configuration Manager distribui automaticamente esse conteúdo aos pontos de distribuição preferenciais de clientes.  

-   Embora isso acione o Configuration Manager para distribuir automaticamente o conteúdo para os pontos de distribuição preferenciais daqueles clientes, o cliente pode obter o conteúdo de outros pontos de distribuição antes dos pontos de distribuição preferenciais para o cliente receber a implantação. Quando esse comportamento ocorrer, o conteúdo estará presente no ponto de distribuição para uso pelo próximo cliente que busca essa implantação.  

Para obter mais informações, consulte [Grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

<!--
If you use version 1511, 1602, or 1606, see  [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md) for information about the different content location and fallback scenarios.
-->



## <a name="package-transfer-manager"></a>Gerenciador de transferência de pacote  
 O gerenciador de transferência de pacote é o componente do servidor do site que transfere o conteúdo para os pontos de distribuição em outros computadores.  

 Para obter mais informações, consulte [Gerenciador de transferência de pacote](../../../core/plan-design/hierarchy/package-transfer-manager.md).  



<!--
## Preferred distribution point  
 A preferred distribution point includes any distribution points that are associated with a client's current boundary groups.  

 You have the option to associate each distribution point with one or more boundary groups:  

-   This association helps the client identify distribution points from which it can download content.  
-   By default, clients can only download content from a preferred distribution point.  


For more information:
 - If you use version 1610 or later, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
 - If you use version 1511, 1602, or 1606, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).
-->



## <a name="prestage-content"></a>Pré-configurar conteúdo  
 A pré-configuração de conteúdo é um processo de transferência de conteúdo para um ponto de distribuição sem a distribuição do conteúdo pela rede.  

 Para obter mais informações, consulte [Gerenciar largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).
