---
title: "Conceitos básicos do gerenciamento de conteúdo | System Center Configuration Manager"
description: "Use as ferramentas e opções no System Center Configuration Manager para gerenciar o conteúdo que você implanta."
ms.custom: na
ms.date: 10/06/2016
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
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 27342ef83d877c31f39bc232e3e19e37b78e62da


---
# <a name="fundamental-concepts-for-content-management-in-system-center-configuration-manager"></a>Conceitos fundamentais para o gerenciamento de conteúdo no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager dá suporte a um sistema robusto de ferramentas e opções para gerenciar o conteúdo que você implanta aplicativos, pacotes, atualizações de software e implantações de sistema operacional.  

 O conteúdo que você implanta é armazenado em servidores de site e servidores do sistema de sites do ponto de distribuição. Esse conteúdo pode exigir uma grande quantidade de largura de banda de rede durante a transferência entre locais.  Para planejar e usar com eficiência a infraestrutura de gerenciamento de conteúdo, você deve compreender as opções e configurações disponíveis e considerar como usá-las para melhor se ajustarem ao seu ambiente de rede e às suas necessidades de implantação de conteúdo.  

Veja a seguir os conceitos fundamentais para o gerenciamento de conteúdo. Quando um conceito requer informações adicionais ou complexas, são fornecidos links para direcioná-lo a esses detalhes.  

## <a name="accounts-used-for-content-management"></a>Contas usadas para gerenciamento de conteúdo  
 As contas a seguir podem ser usadas com o gerenciamento de conteúdo:  

-   **Conta de acesso à rede** – usada pelos clientes para se conectar a uma distribuição ponto e acessar o conteúdo. Por padrão, os clientes tentarão primeiro a conta de computador  

     Essa conta também é usada pelos pontos de distribuição de recepção para obter o conteúdo de um ponto de distribuição de origem em uma floresta remota  

-   **Conta de acesso ao pacote** – por padrão, o Configuration Manager concede acesso ao conteúdo em um ponto de distribuição a usuários e administradores de contas de acesso genérico. No entanto, você pode configurar permissões adicionais para restringir o acesso. Consulte &lt;Manage Accounts to Access Package Content (Gerenciar contas para acessar o conteúdo do pacote)\>  

-   **Conta de conexão multicast** – usada para implantações de sistema operacional  

Para obter mais informações sobre essas contas, consulte [Gerenciar contas para acessar conteúdo](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md)

## <a name="bandwidth-throttling-and-scheduling"></a>Limitação e agendamento de largura de banda  
 Tanto a limitação quanto o agendamento são opções para ajudar a controlar quando o conteúdo é distribuído por um servidor de site para pontos de distribuição. Isso é semelhante, mas não está diretamente relacionado a controles de largura de banda para replicação baseada em arquivo site a site.  

 Para obter mais informações, consulte [Gerenciar largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)

## <a name="binary-differential-replication"></a>Replicação diferencial binária  
 Um pré-requisito para pontos de distribuição, a BDR (replicação diferencial binária) que às vezes é conhecido como replicação delta, é automaticamente usado para reduzir o uso de largura de banda ao distribuir atualizações ao conteúdo implantado anteriormente para outros sites ou ponto de distribuição remoto.  

 A BDR minimiza a largura de banda de rede utilizada para enviar atualizações para conteúdo distribuído, reenviando apenas o conteúdo novo ou alterado, em vez de enviar todo o conteúdo dos arquivos de origem sempre que uma alteração é feita nesses arquivos.  

 Quando é usada a replicação diferencial binária, o Configuration Manager identifica as alterações que ocorrem nos arquivos de origem para cada conjunto do conteúdo que foi distribuído anteriormente.  

-   Quando os arquivos no conteúdo de origem mudam, o Configuration Manager cria uma nova versão incremental do conjunto de conteúdo e replica apenas os arquivos alterados para os sites de destino e pontos de distribuição. Um arquivo é considerado alterado se for renomeado, movido ou tiver o seu conteúdo alterado. Por exemplo, se você substituir um único arquivo de driver de um pacote de implantação de sistema operacional que você tenha distribuído anteriormente para vários sites, apenas o arquivo de driver alterado será replicado para esses sites de destino.  

-   O Configuration Manager dá suporte a até cinco versões incrementais de um conjunto de conteúdo antes de reenviar o todo o conjunto do conteúdo. Após a quinta atualização, a próxima alteração no conjunto de conteúdo faz com que o Configuration Manager crie uma nova versão do conjunto de conteúdo. O Configuration Manager distribui a nova versão do conteúdo definido para substituir o conjunto anterior e qualquer uma de suas versões incrementais. Depois que o novo conjunto de conteúdo é distribuído, alterações incrementais subsequentes aos arquivos de origem são novamente replicadas pela replicação diferencial binária.  


A BDR tem suporte entre cada site pai e filho de uma hierarquia. Dentro de um site, a BDR tem suporte entre o servidor do site e seus pontos de distribuição. Esse suporte inclui pontos de distribuição de recepção mas não pontos de distribuição baseados em nuvem. Pontos de distribuição com base na nuvem não oferecem suporte a replicação diferencial binária para a transferência de conteúdo.  

Aplicativos sempre usam replicação diferencial binária. A replicação diferencial binária é opcional para pacotes e não é habilitada por padrão. Para usar replicação diferencial binária para pacotes, você deve habilitar esta funcionalidade para cada pacote. Para tanto, selecione a opção **Habilitar replicação diferencial binária** ao criar um novo pacote ou ao editar a guia **Fonte de Dados** das propriedades do pacote.  

## <a name="branchcache"></a>BranchCache  
 Uma tecnologia do Windows que permite que os clientes que dão suporte ao BranchCache e baixaram uma implantação configurada para Branch Cache sirvam como uma fonte de conteúdo para outros clientes habilitados para BranchCache.  

 Por exemplo, quando o primeiro computador cliente habilitado para BranchCache solicita conteúdo de um ponto de distribuição que executa o Windows Server 2012 e está configurado como servidor do BranchCache, o computador cliente baixa o conteúdo e o armazena em cache.  

-   Esse computador cliente então pode disponibilizar o conteúdo a outros clientes habilitados para Branch Cache na mesma sub-rede, que também armazena o conteúdo em cache.  

-   Dessa maneira, os clientes subsequentes na mesma sub-rede não precisam baixar conteúdo do ponto de distribuição, e o conteúdo é distribuído em vários clientes para transferências futuras.  





## <a name="windows-pe-peer-cache"></a>Cache de sistemas pares do Windows PE
Ao implantar um novo sistema operacional no System Center Configuration Manager, os computadores que executam a sequência de tarefas podem usar o Cache Par do Windows PE para obter o conteúdo de um par local (uma fonte de cache par), em vez de baixar o conteúdo de um ponto de distribuição. Isso ajuda a minimizar o tráfego de WAN (rede de longa distância) em cenários de filial em que não há nenhum ponto de distribuição local.

Para obter mais informações, consulte [Cache de sistemas pares do Windows PE](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md)


## <a name="client-locations"></a>Locais do cliente  
 Estes são os locais dos quais os clientes acessam conteúdo:  

-   **Intranet** (local):  

    -   Pontos de distribuição podem usar HTTP ou HTTPs  

    -   Apenas use um ponto de distribuição baseado em nuvem para fallback quando os pontos de distribuição locais estiverem indisponíveis  

-   **Internet** :  

    -   Requer que os pontos de distribuição aceitem HTTPS  

    -   Pode usar um ponto de distribuição baseado em nuvem para fallback  

-   **Grupo de trabalho**:  

    -   Requer que os pontos de distribuição aceitem HTTPS  

    -   Pode usar um ponto de distribuição baseado em nuvem para fallback  



## <a name="content-library"></a>Biblioteca de conteúdo  
 O singleinstance store de conteúdo que o Configuration Manager usa para reduzir o tamanho geral do corpo de conteúdo combinado que você distribui.  

Saiba mais sobre a [biblioteca de conteúdo](../../../core/plan-design/hierarchy/the-content-library.md)


## <a name="distribution-point"></a>Ponto de distribuição  
 O Configuration Manager usa pontos de distribuição para armazenar arquivos necessários para que o software seja executado em computadores cliente. Os clientes devem ter acesso a pelo menos um ponto de distribuição do qual poderão baixar os arquivos para o conteúdo que você implanta.  

 O ponto de distribuição (não especializado) básico é conhecido como ponto de distribuição padrão.  Há duas variações do ponto de distribuição padrão que recebem atenção especial:  

-   **Ponto de distribuição de pull** – uma variação de um ponto de distribuição em que o ponto de distribuição obtém conteúdo de outro ponto de distribuição (um ponto de distribuição de origem) semelhante a como os clientes baixam o conteúdo dos pontos de distribuição. Os pontos de distribuição de pull podem ajudar a evitar gargalos de largura de banda de rede que podem ocorrer quando o servidor do site deve distribuir conteúdo diretamente para cada ponto de distribuição.  [Use um ponto de distribuição de recepção baseado em nuvem com o System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  

-   **Ponto de distribuição baseado em nuvem** – uma variação de um ponto de distribuição instalado no Microsoft Azure. [Use um ponto de distribuição baseado em nuvem com o System Center Configuration Manager](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  


Pontos de distribuição padrão dão suporte a uma variedade de configurações e recursos, como limitação e agendamento, PXE e Multicast, ou conteúdo de pré-teste.  

-   Você pode usar controles como **agendas** ou **limitação de largura de banda** para ajudar a controlar essa transferência.  

-   Você também pode usar outras opções incluindo **conteúdo de pré-teste**, **pontos de distribuição de pull** ou tirar proveito do **BranchCache** para reduzir a largura de banda de rede que é usada quando você implanta conteúdo.  

-   Os pontos de distribuição dão suporte a configurações diferentes, como **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** e **[Multicast](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)** para implantações de sistema operacional, ou configurações para dar suporte a **dispositivos móveis**  

 Pontos de distribuição de pull em baseados em nuvem dão suporte a muitas dessas mesmas configurações, mas têm limitações específicas a cada variação de ponto de distribuição.  

## <a name="distribution-point-group"></a>Grupo de pontos de distribuição  
 Agrupamentos lógicos de pontos de distribuição que podem simplificar a distribuição de conteúdo.  

 Para obter mais informações, consulte [Gerenciar grupos de pontos de distribuição](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage)

## <a name="distribution-point-priority"></a>Prioridade de ponto de distribuição  
 O valor de prioridade do ponto de distribuição se baseia em quanto tempo demorou para transferir implantações anteriores para aquele ponto de distribuição.  

-   Este é um valor de ajuste automático atribuído a um ponto de distribuição que ajuda o Configuration Manager a transferir conteúdo para mais pontos de distribuição em um período de tempo menor  

-   Quando se distribui conteúdo a vários pontos de distribuição ao mesmo tempo ou a um grupo de pontos de distribuição, o Configuration Manager envia o conteúdo ao ponto de distribuição com a prioridade mais alta antes de enviar este mesmo conteúdo a um ponto de distribuição com prioridade menor.  

-   Isso não substitui a prioridade de distribuição para pacotes, que continua sendo o fator decisivo na sequência de quando diferentes distribuições são transferidas  


**Por exemplo** , se você distribuir conteúdo com prioridade de distribuição alta a um ponto de distribuição com uma prioridade de ponto de distribuição baixa, o pacote com prioridade de distribuição alta sempre será transferido antes de um pacote com prioridade de distribuição baixa. A prioridade de distribuição será aplicada mesmo que pacotes com prioridade mais baixa sejam distribuídos para pontos de distribuição que têm prioridades mais altas. A prioridade de distribuição alta do pacote garante que o Configuration Manager distribua esse conteúdo para os pontos de distribuição aplicáveis antes de quaisquer pacotes com prioridade mais baixa serem enviados.  

> [!NOTE]  
>  Pontos de distribuição de recepção também usam um conceito de prioridade para ordenar a sequência dos seus pontos de distribuição de origem.  
>   
>  -   A prioridade das transferências de conteúdo para o ponto de distribuição é diferente da usada pelos pontos de distribuição de recepção quando eles pesquisam conteúdo em um ponto de distribuição de origem  
> -   Para obter mais informações, consulte [Usar um ponto de distribuição de pull com o System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  


## <a name="fallback"></a>Fallback  
 Configurações de fallback estão relacionadas ao uso de **pontos de distribuição preferenciais** e ao local de fonte de conteúdo que são usados por clientes.  

-   Por padrão, os clientes só baixam conteúdo de um ponto de distribuição preferencial (associado a grupos de limites do cliente)  

-   No entanto, quando um ponto de distribuição é configurado com **Permitir que clientes usem esse sistema de sites como local de origem de fallback para conteúdo**, esse ponto de distribuição é oferecido somente como uma origem de conteúdo válida para qualquer cliente que não consiga obter uma implantação de um dos seus pontos de distribuição preferenciais.  


Consulte [Cenários de local de origem de conteúdo](../../../core/plan-design/hierarchy/content-source-location-scenarios.md) para obter informações sobre diferentes cenários de fallback e local de conteúdo.

## <a name="network-bandwidth"></a>Largura de banda da rede  
 Para ajudar a gerenciar a quantidade de largura de banda de rede usada quando você distribui conteúdo, use as seguintes opções:  

-   Usar conteúdo pré-teste: um processo de transferência de conteúdo para um ponto de distribuição sem depender do Configuration Manager para distribuir o conteúdo em toda a rede.  

-   Usar agendamento e limitação: configurações que ajudam a controlar quando e como o conteúdo é distribuído aos pontos de distribuição.  

Para obter mais informações, consulte [Gerenciar largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)

## <a name="network-connection-speed-to-content-source"></a>Velocidade de conexão de rede até a fonte de conteúdo  
 É possível configurar a velocidade de conexão de rede de cada ponto de distribuição em um grupo de limites:  

-   Os clientes usam esse valor quando se conectam ao ponto de distribuição  

-   Por padrão, a velocidade de conexão de rede é configurada como **Rápida**, mas também pode ser configurada como **Lenta**  

-   A **velocidade de conexão de rede** e a configuração da implantação determinam se um cliente pode baixar conteúdo de um ponto de distribuição quando o cliente está em um grupo de limites associado  


Consulte [Cenários de local de origem de conteúdo](../../../core/plan-design/hierarchy/content-source-location-scenarios.md) para obter informações sobre diferentes cenários de fallback e local de conteúdo.  

## <a name="on-demand-content-distribution"></a>Distribuição de conteúdo sob demanda  
 Uma opção que você pode definir para aplicativos e pacotes (implantações) individuais para habilitar a distribuição de conteúdo sob demanda para pontos de distribuição preferenciais.  

-   Para habilitar isso para uma implantação, habilite **Distribuir o conteúdo deste pacote para pontos de distribuição preferenciais**  

-   Quando essa opção é habilitada para uma implantação e um cliente tenta solicitar esse conteúdo, mas ele não está disponível em nenhum um dos pontos de distribuição preferenciais de clientes, o Configuration Manager distribui automaticamente esse conteúdo aos pontos de distribuição preferenciais de clientes  

-   Embora isso acione o Configuration Manager para distribuir automaticamente o conteúdo para os pontos de distribuição preferenciais daqueles clientes, o cliente pode obter o conteúdo de outros pontos de distribuição antes dos pontos de distribuição preferenciais para o cliente receber a implantação. Quando isso ocorre, o conteúdo estará presente no ponto de distribuição para uso pelo próximo cliente que procura essa implantação  


Consulte [Cenários de local de origem de conteúdo](../../../core/plan-design/hierarchy/content-source-location-scenarios.md) para obter informações sobre diferentes cenários de fallback e local de conteúdo.  


## <a name="package-transfer-manager"></a>Gerenciador de transferência de pacote  
 O componente de servidor de site que transfere o conteúdo para pontos de distribuição em outros computadores.  

 Saiba mais sobre o [Gerenciador de transferência de pacote](../../../core/plan-design/hierarchy/package-transfer-manager.md)  

## <a name="preferred-distribution-point"></a>Ponto de distribuição preferencial  
 pontos de distribuição associados a grupos de limites do cliente atual.  

 Você tem a opção de associar cada ponto de distribuição a um ou mais grupos de limites:  

-   Essa associação ajuda o cliente a identificar pontos de distribuição dos quais ele pode baixar conteúdo  

-   Por padrão, os clientes só podem baixar conteúdo de um ponto de distribuição preferencial  


Consulte [Cenários de local de origem de conteúdo](../../../core/plan-design/hierarchy/content-source-location-scenarios.md) para obter informações sobre diferentes cenários de fallback e local de conteúdo.  

## <a name="prestage-content"></a>Pré-configurar conteúdo  
 Um processo de transferência de conteúdo para um ponto de distribuição sem depender do Configuration Manager para distribuir o conteúdo em toda a rede.  

 Para obter mais informações, consulte [Gerenciar largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth)



<!--HONumber=Nov16_HO1-->


