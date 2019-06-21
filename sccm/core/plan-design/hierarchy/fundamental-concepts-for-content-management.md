---
title: Conceitos básicos do gerenciamento de conteúdo
titleSuffix: Configuration Manager
description: Use as ferramentas e as opções do Configuration Manager para gerenciar o conteúdo implantado.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bf0b57ad1753d797b163b0016517cdad09459013
ms.sourcegitcommit: 86968fc2f129e404ff8e08f91a05fa17b5c47527
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2019
ms.locfileid: "67251630"
---
# <a name="fundamental-concepts-for-content-management-in-configuration-manager"></a>Conceitos fundamentais para o gerenciamento de conteúdo no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Configuration Manager dá suporte a um sistema robusto de ferramentas e opções para gerenciar o conteúdo de software. As implantações de software, como aplicativos, pacotes, atualizações de software e implantações de sistema operacional, precisam de conteúdo. O Configuration Manager armazena o conteúdo em servidores do site e pontos de distribuição. Esse conteúdo exige uma grande quantidade de largura de banda da rede quando está sendo transferido entre locais. Para planejar e usar a infraestrutura de gerenciamento de conteúdo com eficiência, primeiro entenda as opções e configurações disponíveis. Em seguida, considere como usá-las para que elas sejam ajustadas da melhor forma às suas necessidades de implantação de conteúdo e ambiente de rede.  

> [!TIP]    
> Para obter mais informações sobre o processo de distribuição de conteúdo e para encontrar ajuda no diagnóstico e na resolução de problemas gerais de distribuição de conteúdo, consulte [Noções básicas e solução de problemas de distribuição de conteúdo no Microsoft Configuration Manager ](https://support.microsoft.com/help/4000401/content-distribution-in-mcm).

Os tópicos a seguir são os principais conceitos do gerenciamento de conteúdo. Quando um conceito requer informações adicionais ou complexas, são fornecidos links para direcioná-lo a esses detalhes.



## <a name="accounts-used-for-content-management"></a>Contas usadas para gerenciamento de conteúdo  
 As contas a seguir podem ser usadas com o gerenciamento de conteúdo:  

#### <a name="network-access-account"></a>Conta de acesso à rede
Usada pelos clientes para conectar a um ponto de distribuição e acessar o conteúdo. Por padrão, a conta de computador será tentada primeiro.  

Essa conta também é usada pelos pontos de distribuição pull para baixar o conteúdo de um ponto de distribuição de origem em uma floresta remota.  

Começando pela versão 1806, alguns cenários não exigem mais uma conta de acesso de rede. Você pode habilitar o site para usar HTTP aprimorado com a autenticação do Azure Active Directory.<!--1358228--> 

Para obter mais informações, confira [Conta de acesso à rede](/sccm/core/plan-design/hierarchy/accounts#network-access-account).

#### <a name="package-access-account"></a>Conta de acesso ao pacote
Por padrão, o Configuration Manager concede acesso ao conteúdo em um ponto de distribuição a usuários e administradores de contas de acesso genérico. No entanto, você pode configurar permissões adicionais para restringir o acesso.   

Para obter mais informações, confira [Conta de acesso de pacote](/sccm/core/plan-design/hierarchy/accounts#package-access-account).



## <a name="bandwidth-throttling-and-scheduling"></a>Limitação e agendamento de largura de banda  
 Tanto a limitação quanto o agendamento são opções para ajudar a controlar quando o conteúdo é distribuído por um servidor de site para pontos de distribuição. Essas funcionalidades são semelhantes, mas não estão diretamente relacionadas aos controles de largura de banda para replicação baseada em arquivo site a site.  

 Para obter mais informações, consulte [Gerenciar largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="binary-differential-replication"></a>Replicação diferencial binária  
 A BDR (replicação diferencial binária) às vezes é conhecida como replicação delta. Ela é usada para distribuir atualizações para conteúdo que você implantou anteriormente em outros sites ou em pontos de distribuição remotos. Para dar suporte à redução do BDR de uso de largura de banda, instale o recurso **Compactação Diferencial Remota** nos pontos de distribuição. Para obter mais informações, confira [Pré-requisitos de pontos de distribuição](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012dppreq).

 A BDR minimiza a largura de banda da rede usada para enviar atualizações para o conteúdo distribuído. Ela reenvia somente o conteúdo novo ou alterado, em vez de enviar todo o conjunto de arquivos de fonte de conteúdo sempre que você altera esses arquivos.  

 Quando a BDR é usada, o Configuration Manager identifica as alterações ocorridas nos arquivos de origem em cada conjunto de conteúdo distribuído anteriormente.  

-   Quando os arquivos no conteúdo da fonte são alterados, o site cria uma nova versão incremental do conteúdo. Ele então replica apenas os arquivos alterados nos sites e pontos de distribuição de destino. Um arquivo é considerado alterado se ele é renomeado ou movido, ou se o conteúdo dele é alterado. Por exemplo, se você substituir um único arquivo de driver de um pacote de driver distribuído anteriormente para vários sites, apenas o arquivo de driver alterado será replicado.  

-   O Configuration Manager dá suporte a até cinco versões incrementais de um conjunto de conteúdo antes de reenviar o todo o conjunto do conteúdo. Após a quinta atualização, a próxima alteração no conjunto de conteúdo faz com que o site crie uma nova versão do conjunto de conteúdo. O Configuration Manager distribui a nova versão do conteúdo definido para substituir o conjunto anterior e qualquer uma de suas versões incrementais. Depois que o novo conjunto de conteúdo é distribuído, as alterações incrementais seguintes nos arquivos de origem são novamente replicadas pela BDR.  

A BDR tem suporte entre cada site pai e filho de uma hierarquia. Há suporte para a BDR em um site entre o servidor do site e seus pontos de distribuição normais. No entanto, os pontos de distribuição por pull e os pontos de distribuição na nuvem não dão suporte à BDR para transferência de conteúdo. Os pontos de distribuição pull dão suporte a deltas de nível de arquivo, transferindo novos arquivos, mas não os blocos em um arquivo.

Aplicativos sempre usam replicação diferencial binária. A BDR é opcional para pacotes e não está habilitada por padrão. Para usar a BDR para pacotes, habilite essa funcionalidade em cada pacote. Selecione a opção **Habilitar replicação diferencial binária** ao criar ou editar um pacote.   



## <a name="branchcache"></a>BranchCache  
 O [BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) é uma tecnologia do Windows. Os clientes que dão suporte ao BranchCache e baixaram uma implantação configurada para o BranchCache servem como uma fonte de conteúdo para outros clientes habilitados para o BranchCache.  

 Por exemplo, você tem um ponto de distribuição que executa o Windows Server 2012 ou posterior e é configurado como um servidor do BranchCache. Quando o primeiro cliente habilitado para BranchCache solicita o conteúdo desse servidor, o cliente baixa esse conteúdo e armazena-o em cache.  

- Esse cliente então disponibiliza o conteúdo aos outros clientes habilitados para o Branch Cache na mesma sub-rede que também armazena o conteúdo em cache.  
- Os outros clientes na mesma sub-rede não precisam baixar o conteúdo do ponto de distribuição.  
- O conteúdo é distribuído entre vários clientes para transferências futuras.  

Para saber mais, confira [Suporte para o Windows BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmk_branchcache).



## <a name="delivery-optimization"></a>Otimização de Entrega
<!-- 1324696 -->
Você usa os grupos de limites do Configuration Manager para definir e regular a distribuição de conteúdo em sua rede corporativa e para escritórios remotos. A [Otimização de Entrega do Windows](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) é uma tecnologia ponto-a-ponto baseada na nuvem para compartilhar conteúdo entre dispositivos do Windows 10. A partir da versão 1802, configure a Otimização de Entrega para que ela use os grupos de limites ao compartilhar o conteúdo entre pares. As configurações do cliente aplicam o identificador do grupo de limites como o identificador do grupo da Otimização de Entrega no cliente. Quando o cliente se comunica com o serviço de nuvem da Otimização de Entrega, ele usa esse identificador para localizar os pares com o conteúdo desejado. Para obter mais informações, consulte as configurações do cliente [Otimização de entrega](/sccm/core/clients/deploy/about-client-settings#delivery-optimization).

A Otimização de Entrega é a tecnologia recomendada para [otimizar a distribuição de atualização do Windows 10](/sccm/sum/deploy-use/optimize-windows-10-update-delivery) dos arquivos de instalação expressa para atualizações de qualidade do Windows 10.



## <a name="windows-ledbat"></a>LEDBAT do Windows
<!--1358112-->
O LEDBAT (Low Extra Delay Background Transport) do Windows é um recurso de controle de congestionamento de rede do Windows Server para ajudar a gerenciar as transferências na rede em segundo plano. Para pontos de distribuição em execução nas versões com suporte do Windows Server, habilite uma opção para ajudar a ajustar o tráfego da rede. Assim, os clientes usam a largura de banda de rede somente quando ela está disponível. 

Para obter mais informações sobre o LEDBAT do Windows em geral, confira a postagem no blog [New transport advancements](https://blogs.technet.microsoft.com/networking/2016/07/18/announcing-new-transport-advancements-in-the-anniversary-update-for-windows-10-and-windows-server-2016/) (Novos avanços de transporte).

Para obter mais informações de como usar o LEDBAT do Windows com pontos de distribuição do Configuration Manager, confira a configuração para **Ajustar a velocidade do download para usar a largura de banda de rede não utilizada (LEDBAT do Windows)** quando você [Definir as configurações gerais de um ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-general).



## <a name="peer-cache"></a>Cache de pares
O cache par do cliente ajuda você a gerenciar a implantação de conteúdo nos clientes em locais remotos. O cache par é uma solução interna do Configuration Manager que o os clientes podem usar para compartilhar conteúdo com outros clientes diretamente do cache local.

Primeiro, implante as configurações do cliente que habilitam o cache par para uma coleção. Assim, os membros dessa coleção poderão agir como uma fonte de conteúdo par para outros clientes no mesmo grupo de limites.

Começando na versão 1806, as fontes de cache par do cliente podem dividir o conteúdo em partes. Essas partes minimizam a transferência de rede para reduzir a utilização de WAN. O ponto de gerenciamento fornece acompanhamento mais detalhado das partes do conteúdo. Ele tentará eliminar mais de um download do mesmo conteúdo por grupo de limites.<!--1357346-->

Para saber mais, confira [Cache par para clientes do Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).



## <a name="windows-pe-peer-cache"></a>Cache de sistemas pares do Windows PE
Quando você implanta um novo sistema operacional com o Configuration Manager, os computadores que executam a sequência de tarefas podem usar o cache par do Windows PE. Eles baixam o conteúdo de uma origem de cache par, em vez de um ponto de distribuição. Esse comportamento ajuda a minimizar o tráfego de WAN em cenários de filial em que não há nenhum ponto de distribuição local.

Para obter mais informações, consulte [Cache de pares do Windows PE](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic).



## <a name="client-locations"></a>Locais do cliente  
 Estes são os locais dos quais os clientes acessam conteúdo:  

-   **Intranet** (local):  

    -   Pontos de distribuição podem usar HTTP ou HTTPs.  

    -   Apenas use um ponto de distribuição na nuvem para fallback quando não houver pontos de distribuição locais disponíveis.  

-   **Internet**:  

    -   Requer que os pontos de distribuição para Internet aceitem HTTPS.  

    -   Pode usar um ponto de distribuição na nuvem ou um CMG (gateway de gerenciamento de nuvem).  
    
        *   Da versão 1806 em diante, um CMG pode também fornecer conteúdo aos clientes. Essa funcionalidade reduz os certificados necessários e o custo das VMs do Azure. Para obter mais informações, consulte [Modificar um CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway).

-   **Grupo de trabalho**:  

    -   Requer que os pontos de distribuição aceitem HTTPS.  

    -   Pode usar um ponto de distribuição na nuvem ou CMG.  



## <a name="content-source-priority"></a>Prioridade da fonte de conteúdo

Quando um cliente precisa de conteúdo, ele faz uma solicitação de local de conteúdo ao ponto de gerenciamento. O ponto de gerenciamento retorna uma lista de locais de fonte que são válidos para o conteúdo solicitado. Essa lista varia de acordo com o cenário específico, as tecnologias em uso, o design de site, os grupos de limites e as configurações de implantação. A lista a seguir contém todos os locais de fonte de conteúdo possíveis que um cliente pode usar, na ordem em que ele os prioriza:  

1.  O ponto de distribuição no mesmo computador que o cliente
2.  Uma fonte par na mesma sub-rede da rede
3.  Um ponto de distribuição na mesma sub-rede da rede
4.  Uma fonte par no mesmo grupo de limites
5.  Um ponto de distribuição no grupo de limites atual
6.  Um ponto de distribuição em um grupo de limites vizinho configurado para fallback
9.  Um ponto de distribuição no grupo de limites do site padrão 
10. O serviço de nuvem do Windows Update
11. Um ponto de distribuição para Internet
12. Um ponto de distribuição na nuvem no Azure



## <a name="content-library"></a>Biblioteca de conteúdo  
 A biblioteca de conteúdo é o armazenamento de instância única do conteúdo no Configuration Manager. Essa biblioteca reduz o tamanho geral do conteúdo distribuído.  

- Saiba mais sobre a [biblioteca de conteúdo](/sccm/core/plan-design/hierarchy/the-content-library).
- Use a [ferramenta de limpeza da biblioteca de conteúdo](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) para remover o conteúdo que não está mais associado a um aplicativo.  



## <a name="distribution-points"></a>Pontos de distribuição  
 O Configuration Manager usa pontos de distribuição para armazenar arquivos necessários para que o software seja executado em computadores cliente. Os clientes devem ter acesso a pelo menos um ponto de distribuição do qual poderão baixar os arquivos para o conteúdo que você implanta.  

 O ponto de distribuição (não especializado) básico é conhecido como ponto de distribuição padrão. Há duas variações do ponto de distribuição padrão que recebem atenção especial:  

-   **Ponto de distribuição de pull**: Uma variação de um ponto de distribuição em que o ponto de distribuição obtém conteúdo de outro ponto de distribuição (um ponto de distribuição de origem). Esse processo é semelhante a como os clientes baixam o conteúdo dos pontos de distribuição. Os pontos de distribuição de pull podem ajudar a evitar gargalos de largura de banda de rede que ocorrem quando o servidor do site deve distribuir conteúdo diretamente para cada ponto de distribuição. [Use um ponto de distribuição pull](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

-   **Ponto de distribuição na nuvem**: Uma variação de um ponto de distribuição instalado no Microsoft Azure. [Saiba como usar um ponto de distribuição na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point).  


Os pontos de distribuição padrão dão suporte a uma variedade de recursos e configurações:  

- Use controles como **agendamentos** ou **limitação da largura de banda** para ajudar a controlar essa transferência.  

- Use outras opções, incluindo **conteúdo pré-teste** e **pontos de distribuição pull**, para minimizar e controlar o consumo de rede.  

- O **BranchCache**, o **cache par** e a **Otimização de Entrega** são tecnologias ponto a ponto para reduzir a largura de banda da rede usada quando o conteúdo é implantado.  

- Existem diferentes configurações para implantações de sistema operacional, como **[PXE](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_PXEDistributionPoint)** e **[Multicast](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_DPMulticast)**  

- Opções de **dispositivos móveis**   
  
Os pontos de distribuição por pull e em nuvem dão suporte a muitas dessas mesmas configurações, mas têm limitações específicas de cada variação de ponto de distribuição.  



## <a name="distribution-point-groups"></a>Grupos de pontos de distribuição  
 Os grupos de pontos de distribuição são agrupamentos lógicos de pontos de distribuição que podem simplificar a distribuição de conteúdo.  

 Para obter mais informações, consulte [Gerenciar grupos de pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_manage).



## <a name="distribution-point-priority"></a>Prioridade de ponto de distribuição  
 O valor de prioridade do ponto de distribuição se baseia em quanto tempo demorou para transferir implantações anteriores para aquele ponto de distribuição.  

-   Esse valor tem um ajuste automático. Ele é definido em cada ponto de distribuição para ajudar o Configuration Manager a transferir o conteúdo mais rapidamente para mais pontos de distribuição.  

-   Quando você distribui o conteúdo para vários pontos de distribuição ao mesmo tempo, ou para um grupo de pontos de distribuição, o site envia primeiro o conteúdo para o servidor com a prioridade mais alta. Em seguida, ele envia esse mesmo conteúdo a um ponto de distribuição com uma prioridade mais baixa.  

-   A prioridade do ponto de distribuição não substitui a prioridade de distribuição dos pacotes. A prioridade de pacote continua sendo o fator decisivo de quando o site envia um conteúdo diferente.  

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

Para obter mais informações, consulte [Grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).



## <a name="network-bandwidth"></a>Largura de banda da rede  
 Para ajudar a gerenciar a quantidade de largura de banda de rede usada quando você distribui conteúdo, use as seguintes opções:  

-   **Conteúdo pré-teste**: A transferência de conteúdo para um ponto de distribuição sem a distribuição do conteúdo pela rede.  

-   **Agendamento e limitação**: Configurações que ajudam a controlar quando e como o conteúdo é distribuído aos pontos de distribuição.  

Para obter mais informações, consulte [Gerenciar largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="network-connection-speed-to-content-source"></a>Velocidade de conexão de rede até a fonte de conteúdo  
 Várias coisas mudaram com o Configuration Manager Branch Atual, na forma como os clientes encontram um ponto de distribuição que tem conteúdo. Essas alterações incluem a velocidade da rede para uma fonte de conteúdo. 

Velocidades de conexão de rede que definem um ponto de distribuição como **Rápido** ou **Lento** não são mais usadas. Em vez disso, cada sistema de sites associado a um grupo de limites é tratado da mesma forma.

Para obter mais informações, consulte [Grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).



## <a name="on-demand-content-distribution"></a>Distribuição de conteúdo sob demanda  
 A distribuição de conteúdo sob demanda é uma opção para implantações de aplicativos e pacotes individuais. Com essa opção é possível distribuir conteúdo sob demanda para servidores preferenciais.  

-   Para habilitar essa configuração para uma implantação, habilite: **Distribuir o conteúdo deste pacote para pontos de distribuição preferenciais**.  

-   Quando você habilita essa opção para uma implantação e um cliente solicita esse conteúdo, mas ele não está disponível em nenhum dos pontos de distribuição preferenciais do cliente, o Configuration Manager distribui automaticamente esse conteúdo para os pontos de distribuição preferenciais do cliente.  

-   Embora isso acione o Configuration Manager para distribuir automaticamente o conteúdo para os pontos de distribuição preferenciais daqueles clientes, o cliente pode obter o conteúdo de outros pontos de distribuição antes dos pontos de distribuição preferenciais para o cliente receber a implantação. Quando esse comportamento ocorrer, o conteúdo estará presente no ponto de distribuição para uso pelo próximo cliente que busca essa implantação.  

Para obter mais informações, consulte [Grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).



## <a name="package-transfer-manager"></a>Gerenciador de transferência de pacote  
 O gerenciador de transferência de pacote é o componente do servidor do site que transfere o conteúdo para os pontos de distribuição em outros computadores.  

 Para obter mais informações, consulte [Gerenciador de transferência de pacote](/sccm/core/plan-design/hierarchy/package-transfer-manager).  



## <a name="prestage-content"></a>Pré-configurar conteúdo  
 A pré-configuração de conteúdo é um processo de transferência de conteúdo para um ponto de distribuição sem a distribuição do conteúdo pela rede.  

 Para obter mais informações, consulte [Gerenciar largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).
