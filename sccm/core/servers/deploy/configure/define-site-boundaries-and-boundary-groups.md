---
title: Definir limites de site | System Center Configuration Manager
description: "Entenda como definir locais de rede na sua intranet que podem conter dispositivos que você deseja gerenciar."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9df8b5d5fd67a5ced5860771295d05dfb56a3982


---
# <a name="define-site-boundaries-and-boundary-groups-for-system-center-configuration-manager"></a>Definir limites de site e grupos de limites para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os limites para o System Center Configuration Manager definem locais de rede na intranet que pode conter dispositivos que você deseja gerenciar. Grupos de limites são grupos lógicos de limites que você configura. Grupos de limites e limites estão disponíveis em uma hierarquia e você não configurá-los para sites individuais.  

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


##  <a name="a-namebkmkboundariesa-boundaries"></a><a name="BKMK_Boundaries"></a> Limites  
 Você pode criar limites individuais manualmente. Além disso, você pode configurar a [Descoberta de Florestas do Active Directory](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) para detecção automática e criar limites para cada sub-rede IP e Site do Active Directory detectado.  

-   Cada limite representa um local de rede e está disponível para uso por todos os sites na sua hierarquia.  

-   O Configuration Manager não dá suporte à entrada direta de uma super-rede como limite. Em vez disso, use o tipo de limite de intervalo de endereços IP.  

-   Quando a descoberta de florestas do Active Directory identifica uma super-rede que é atribuída a um site do Active Directory, o Configuration Manager converte a super-rede em um limite de intervalo de endereços IP.  

-   O limite em que um cliente está é equivalente ao site do Active Directory ou ao endereço IP da rede que o cliente identifica. (Não é incomum um cliente usar um endereço IP de que o administrador do Configuration Manager não esteja ciente. Se o local de rede dos clientes for incerto, confirme o que o cliente informa como seu local usando o comando **IPCONFIG** comando no cliente.)  

Ao criar um limite, ele recebe automaticamente um nome baseado no tipo e no escopo do limite. Não é possível modificar esse nome. Em vez disso, ao configurar o limite, especifique uma descrição para ajudar a identificar o limite no console do Configuration Manager.  

 Depois de criar um limite, você pode modificar suas propriedades para fazer o seguinte:  

-   Adicionar o limite a um ou mais grupos de limites.  

-   Alterar o tipo ou o escopo do limite.  

-   Exiba a guia **Sistemas de Sites** de limites para ver quais servidores do sistema de sites (pontos de distribuição, pontos de migração de estado e pontos de gerenciamento) estão associados ao limite.  

#### <a name="to-create-a-boundary"></a>Para criar um limite  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** > **Limites**  

2.  Na guia **Início** , no grupo **Criar** , clique em **Criar Boundary.**.  

3.  Na guia **Geral** da caixa de diálogo Criar Limite, é possível especificar uma **Descrição** para identificar o limite por um nome amigável ou de referência.  

4.  Selecione um **Tipo** para esse limite:  

    -   Se selecionar **Sub-rede IP**, será necessário especificar uma **ID de Sub-rede** para esse limite.  

        > [!TIP]  
        >  Você pode especificar a **Rede** e a **Máscara de Sub-rede** para que a **ID de Sub-rede** seja especificada automaticamente. Quando você salva o limite, somente o valor da ID de Sub-rede é salvo.  

    -   Se selecionar o **site do Active Directory**, você deverá especificar ou **Procurar** um site do Active Directory na floresta local do servidor do site.  

        > [!IMPORTANT]  
        >  Ao especificar um site do Active Directory para um limite, o limite inclui uma sub-rede IP que é um membro de um site do Active Directory. Se a configuração do site do Active Directory mudar no Active Directory, os locais de rede inclusos nesse limite também mudarão.  

    -   Se selecionar o **Prefixo IPv6**, você deverá especificar um **Prefixo** no formato de prefixo IPv6.  

    -   Se selecionar **Intervalo de endereços IP**, será necessário especificar um **Endereço IP Inicial** e um **Endereço IP Final** que inclui parte de uma sub-rede IP ou várias sub-redes IP.  

5.  Clique em **OK** para salvar o novo limite.  

#### <a name="to-configure-a-boundary"></a>Para configurar um limite  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** > **Limites**  

2.  Selecione o limite que você deseja modificar.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Na caixa de diálogo **Propriedades** do limite, selecione a guia **Geral** para editar a **Descrição** ou **Tipo** do limite. Você também pode alterar o escopo de um limite editando os locais de rede para o limite. Por exemplo, para um limite de site do Active Directory, você pode especificar um novo nome de site do Active Directory.  

5.  Selecione a guia **Sistemas de Site** para exibir os sistemas de site que estão associados a esse limite. Não é possível alterar essa configuração a partir das propriedades de um limite.  

    > [!TIP]  
    >  Para que um servidor do sistema de sites seja listado como um sistema de sites para um limite, ele deve ser associado como um servidor do sistema de sites a pelo menos um grupo de limites que inclui esse limite. Isso é configurado na guia **Referências** de um grupo de limite.  

6.  Selecione a guia **Grupos de Limites** para modificar a associação a um grupo de limites para esse limite:  

    -   Para adicionar esse limite a um ou mais grupos de limites, clique em **Adicionar**, marque a caixa de seleção para um ou mais grupos de limites e clique em **OK**.  

    -   Para remover esse limite de um grupo de limites, selecione o grupo de limites e clique em **Remover**.  

7.  Clique em **OK** para fechar as propriedades de limite e salvar a configuração.  

##  <a name="a-namebkmkboundarygroupsa-boundary-groups"></a><a name="BKMK_BoundaryGroups"></a> Boundary groups  
 Você cria grupos de limites apara agrupar de logicamente locais de rede (limites) relacionados para facilitar o gerenciamento da infraestrutura de rede. É necessário atribuir limites a grupos de limites para poder usar o grupo de limites. Os clientes usam a configuração do grupo de limites para:  

-   Atribuição automática de site  

-   Local do conteúdo  

-   Pontos de gerenciamento preferenciais (se você usar pontos de gerenciamento preferenciais, deverá habilitar essa opção para a hierarquia, e não de dentro da configuração do grupo de limites. Consulte o procedimento a seguir *para habilitar o uso de pontos de gerenciamento preferenciais*)  

Ao configurar grupos de limites, você adiciona um ou mais limites ao grupo de limites e define as configurações adicionais para uso de clientes localizados nesses limites.  

#### <a name="to-create-a-boundary-group"></a>Para criar um grupo de limites  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** >  **Grupos de Limites**.  

2.  Na guia **Início** , no grupo **Criar** , clique em **Criar Grupo de Limites**.  

3.  Na caixa de diálogo **Criar Grupo de Limites** , selecione a guia **Geral** e especifique um **Nome** para esse grupo de limites.  

4.  Clique em **OK** para salvar o novo grupo de limites.  

#### <a name="to-configure-a-boundary-group"></a>Para configurar um grupo de limites  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** >  **Grupos de Limites**.  

2.  Selecione o grupo de limites que você deseja modificar.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Na caixa de diálogo **Propriedades** para o grupo de limites, selecione a guia **Geral** para modificar os limites que são membros desse grupo de limites:  

    -   Para adicionar limites, clique em **Adicionar**, marque a caixa de seleção para um ou mais limites e clique em **OK**.  

    -   Para remover limites, selecione o limite e clique em **Remover**.  

5.  Selecione a guia **Referências** para modificar a atribuição de site e a configuração do servidor do sistema de sites associado:  

    -   Para habilitar esse grupo de limites para uso de clientes para atribuição de site, marque a caixa de seleção **Utilize este grupo de limites para a atribuição de site**e selecione a caixa suspensa **Site Atribuído** .  

    -   Para configurar quais servidores do sistema de sites disponíveis estão associados a este grupo de limites:  

    1.  Clique em **Adicionar**e marque a caixa de seleção para um ou mais servidores. Os servidores são adicionados como servidores do sistema de sites associados a este grupo de limite. Somente os servidores que têm suporte para a função do sistema de sites instalada neles estão disponíveis.  

        > [!NOTE]  
        >  É possível selecionar qualquer combinação de sistemas de sites disponíveis de qualquer site na hierarquia. Os sistemas de site selecionados são listados na guia **Sistemas de Site** nas propriedades de cada limite membro desse grupo de limites.  

    2.  Para remover um servidor deste grupo de limites, selecione o servidor e clique em **Remover**.  

        > [!NOTE]  
        >  Para interromper o uso deste grupo de limites para a associação de sistemas de sites, você deve remover todos os servidores listados como servidores do sistema de sites associados.  

    3.  Para alterar a velocidade de conexão de rede de um servidor do sistema de sites para este grupo de limite, selecione o servidor e clique em **Alterar Conexão**.  

         Por padrão, a velocidade de conexão para cada sistema de site é **Rápida**, podendo ser alterada para **Lenta**. A velocidade de conexão de rede e a configuração de uma implantação determinam se o cliente pode baixar o conteúdo do servidor.  

6.  Clique em **OK** para fechar as propriedades do grupo de limites e salvar a configuração.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>Para associar um servidor de implantação de conteúdo ou um ponto de gerenciamento a um grupo de limite  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** >  **Grupos de Limites**.  

2.  Selecione o grupo de limites que você deseja modificar.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Na caixa de diálogo **Propriedades** para o grupo de limites, selecione a guia **Referências** .  

5.  Em **Selecionar servidores do sistema de sites**clique em **Adicionar**, marque a caixa de seleção para os servidores do sistema de site que deseja associar a esse grupo de limites e clique em **OK**.  

6.  Clique em **OK** para fechar a caixa de diálogo e salvar a configuração do grupo de limites.  

#### <a name="to-enable-use-of-preferred-management-points"></a>para habilitar o uso de pontos de gerenciamento preferenciais  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração do Site** > **Sites** e, na guia **Início**, selecione **Configurações da Hierarquia**.  

2.  Na guia **Geral** das Configurações da Hierarquia, selecione **Os clientes preferem usar os pontos de gerenciamento especificados nos grupos de limite**.  

3.  Clique em **OK** para fechar a caixa de diálogo e salvar a configuração.  

#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>Para configurar um local de fallback para atribuição automática de site  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração do Site** >  **Sites**.  

2.  Na guia **Início** , no grupo **Sites** , clique em **Configurações da Hierarquia**.  

3.  Na guia **Geral** , marque a caixa de seleção **Usar um local de fallback**e selecione um local na lista suspensa **Local de fallback** .  

4.  Clique em **OK** para salvar a configuração.  

 As seções a seguir fornecem detalhes adicionais sobre configurações de grupo de limites.  

###  <a name="a-namebkmkboundarysiteassignmenta-about-site-assignment"></a><a name="BKMK_BoundarySiteAssignment"></a> Sobre atribuição de site  
 É possível configurar cada grupo de limites com um site atribuído para clientes.  

-   Um cliente recém-instalado que usa a atribuição automática de site ingressará no site atribuído de um grupo de limites que contém o local de rede atual do cliente.  

-   Depois de atribuir a um site, um cliente não altera a atribuição de site quando altera o local de rede. Por exemplo, se o cliente usa o perfil móvel em um novo local de rede que está representado por um limite em um grupo de limites com uma atribuição de site diferente, o site atribuído do cliente permanece inalterado.  

-   Quando a Descoberta de Sistemas do Active Directory encontra um novo recurso, as informações de rede para o recurso descoberto são avaliadas com os limites em grupos de limites. Esse processo associa o novo recurso a um site atribuído para uso do método de instalação do cliente por push.  

-   Quando um limite é um membro de vários grupos de limite que têm diferentes locais atribuídos, os clientes selecionarão aleatoriamente um desses sites.  

-   As alterações em um site atribuído de grupos de limite somente se aplicam a novas ações de atribuição de site. Os clientes atribuídos previamente a um site não reavaliam sua atribuição de site com base nas alterações da configuração de um grupo de limites (ou ao seu próprio local de rede).  

Para obter informações sobre a atribuição de site de cliente, consulte [Usando atribuição de site automática para computadores](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) em [Como atribuir clientes a um site no System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="a-namebkmkboundarycontentlocationa-about-content-location"></a><a name="BKMK_BoundaryContentLocation"></a> Sobre o local do conteúdo  
 Você pode configurar cada grupo de limites com um ou mais pontos de distribuição e pontos de migração e associar os mesmos pontos de distribuição e pontos de migração a vários grupos de limites.  

-   **Durante a distribuição de software**, os clientes solicitam um local para o conteúdo de implantação. O Configuration Manager envia ao cliente uma lista de pontos de distribuição associados a cada grupo de limites que inclui o local de rede atual do cliente.  

-   **Durante a implantação de sistema operacional** , os clientes solicitam um local para enviar ou receber suas informações de migração de estado. O Configuration Manager envia ao cliente uma lista de pontos de migração de estado associados a cada grupo de limites que inclui o local de rede atual do cliente.  

Esse comportamento permite que o cliente selecione o servidor mais próximo do qual transferir o conteúdo ou as informações de migração de estado.  

###  <a name="a-namebkmkpreferredmpa-about-preferred-management-points"></a><a name="BKMK_PreferredMP"></a> Sobre pontos de gerenciamento preferenciais  
 Os pontos de gerenciamento preferenciais permitem que um cliente identifique um ponto de gerenciamento associado ao local de rede (limite) atual.  

-   Um cliente tenta usar um ponto de gerenciamento preferencial de seu site atribuído antes de usar um ponto de gerenciamento de seu site atribuído que não está configurado como preferencial.  

-   Para usar esta opção, é necessário habilitá-la para a hierarquia e configurar grupos de limite em sites primários individuais para incluir os pontos de gerenciamento que devem ser associados aos limites associados desse grupo de limites  

-   Quando os pontos de gerenciamento preferenciais são configurados e um cliente organiza sua lista de pontos de gerenciamento, o cliente coloca os pontos de gerenciamento preferenciais na parte superior de sua lista de pontos de gerenciamento atribuídos (que inclui todos os pontos de gerenciamento do site atribuído do cliente)  

> [!NOTE]  
>  Quando um cliente realiza roaming (o que significa alterar seus locais de rede, como quando um laptop passa para um local de escritório remoto), ele pode usar um ponto de gerenciamento (ou ponto de gerenciamento proxy) do site local em seu novo local antes de tentar usar um ponto de gerenciamento do seu site atribuído (que inclui os pontos de gerenciamento preferenciais).  Consulte [Entender como os clientes encontram serviços e recursos do site para o System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) para obter mais informações.  

###  <a name="a-namebkmkboundaryoverlapa-about-overlapping-boundaries"></a><a name="BKMK_BoundaryOverlap"></a> Sobre a sobreposição de limites  
 O Configuration Manager dá suporte à sobreposição de configurações de limite para o local do conteúdo:  

-   **Quando um cliente solicita conteúdo** e o local de rede do cliente pertence a vários grupos de limites, o Configuration Manager envia ao cliente uma lista de todos os pontos de distribuição que têm o conteúdo.  

-   **Quando um cliente solicita a um servidor o envio ou recebimento de suas informações de migração de estado**, e o local de rede do cliente pertence a vários grupos de limites, o Configuration Manager envia ao cliente uma lista de todos os pontos de migração de estado associados a um grupo de limites que inclui o local de rede atual do cliente.  

Esse comportamento permite que o cliente selecione o servidor mais próximo do qual transferir o conteúdo ou as informações de migração de estado.  

###  <a name="a-namebkmkboudnarynetworkspeeda-about-network-connection-speed"></a><a name="BKMK_BoudnaryNetworkSpeed"></a> Sobre a velocidade de conexão de rede  
 Você pode definir a velocidade de conexão de rede para cada servidor de sistema de sites em um grupo de limites. Essa configuração se aplica a clientes que se conectam a um sistema de sites com base nessa configuração de grupos de limites. O mesmo servidor do sistema de sites pode ter uma velocidade de conexão definida para ele em grupos de limites diferentes.  

 Por padrão, a velocidade de conexão de rede é configurada como **Rápida**, mas também pode ser configurada como **Lenta**. A velocidade de conexão de rede e a configuração da implantação determinam se um cliente pode baixar conteúdo de um ponto de distribuição quando o cliente está em um grupo de limites associado.  

 Para obter mais informações sobre como a configuração de velocidade de conexão de rede afeta o modo como os clientes obtêm conteúdos, consulte [Cenários de local de origem de conteúdo](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

##  <a name="a-namebkmkboundarybestpracticesa-best-practices-for-boundaries"></a><a name="BKMK_BoundaryBestPractices"></a> Melhores práticas para limites  

-   **Considere usar o tipo de limite de intervalo de endereços IP apenas quando outros tipos de limite não podem ser usados:**  

     Ao planejar sua estratégia de limite, recomendamos que você use limites baseados nos sites do Active Directory antes de usar outros tipos de limites. Onde os limites baseados nos sites do Active Directory não estiverem disponíveis, use limites de sub-rede IP ou IPv6. Se nenhuma dessas opções estiver disponível para você, reutilize limites de intervalo de endereço IP. Isto se deve ao fato de que o site avalia os membros limites periodicamente e a consulta necessária para acessar os membros de um intervalo de endereços IP necessita, substancialmente, de um uso maior dos recursos do SQL Server que as consultas que acessam membros de outros tipos de limites.  

-   **Evite a sobreposição de limites para atribuição automática de site:**  

     Embora cada grupo de limites dê suporte a configurações de atribuição de site e de local de conteúdo, é uma melhor prática para criar um conjunto separado de grupos de limites para usar apenas para atribuição de site. Significado: garanta que cada limite em um grupo de limites não seja membro de outro grupo de limites com uma atribuição de site diferente. Isso ocorre porque:  

    -   Um único limite pode ser incluído em vários grupos de limites  

    -   Cada grupo de limite pode ser associado um site primário diferente para atribuição de site  

    -   Um cliente em um limite que seja membro de dois grupos de limites diferentes com atribuições de site diferente selecionará aleatoriamente um site para ingressar, que pode não ser o site que você pretendia que o cliente ingressasse.  Essa configuração é chamada de limites sobrepostos.  

     Os limites sobrepostos não são um problema para o local do conteúdo, em vez disso, geralmente são uma configuração desejada que fornece recursos adicionais de clientes ou locais de conteúdo que eles podem usar.  



<!--HONumber=Nov16_HO1-->


