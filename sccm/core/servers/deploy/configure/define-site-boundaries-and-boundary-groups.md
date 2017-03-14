---
title: Definir limites de site | Microsoft Docs
description: "Entenda como definir locais de rede na sua intranet que podem conter dispositivos que você deseja gerenciar."
ms.custom: na
ms.date: 2/27/2017
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
ms.sourcegitcommit: 6d83570e3210709c5ef39b50d9c483f99017664b
ms.openlocfilehash: 13b79c920a64698660ee1c041b9166646789634c
ms.lasthandoff: 02/28/2017


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


##  <a name="BKMK_Boundaries"></a> Limites  
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

### <a name="to-create-a-boundary"></a>Para criar um limite  

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

### <a name="to-configure-a-boundary"></a>Para configurar um limite  

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

##  <a name="BKMK_BoundaryGroups"></a> Boundary groups
> [!IMPORTANT]  
>  **As informações nesta seção de Grupos de limites e suas seções filho se aplicam à versão 1610 ou posterior.** Este conteúdo foi revisado para ser específico para alterações de design introduzidas para grupos de limites com esta versão de atualização.
>
> **Se você usar versões 1511, 1602 ou 1606**, consulte [Boundary groups for System Center Configuration Manager versions 1511, 1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) (Grupos de limites para o System Center Configuration Manager versões 1511, 1602 e 1606) para obter informações sobre como usar e configurar os grupos de limites com essas versões do produto.

A versão 1610 introduz alterações importantes para os grupos de limites e como eles funcionam com pontos de distribuição. Essas alterações ajudam simplificar o design da infraestrutura de conteúdo, enquanto proporcionam a você mais controle sobre como e quando os clientes realizam o fallback para pesquisar pontos de distribuição adicionais como locais de fonte de conteúdo. Isso inclui pontos de distribuição baseados em nuvem e locais.

**Sobre os grupos de limites:**  
 Você cria grupos de limites apara agrupar de logicamente locais de rede (limites) relacionados para facilitar o gerenciamento da infraestrutura de rede. É necessário atribuir limites a grupos de limites para poder usar o grupo de limites. Os clientes usam a configuração do grupo de limites para:  

-   Atribuição automática de site  
-   Local do conteúdo  
-   Pontos de gerenciamento preferenciais (se você usar pontos de gerenciamento preferenciais, deverá habilitar essa opção para a hierarquia, e não de dentro da configuração do grupo de limites. Consulte o procedimento a seguir [para habilitar o uso de pontos de gerenciamento preferenciais](#to-enable-use-of-preferred-management-points) nesse tópico.)  

Ao configurar grupos de limites, você adiciona um ou mais limites ao grupo de limites e define as configurações adicionais para uso de clientes localizados nesses limites.  

Você pode encontrar [procedimentos para gerenciar grupos de limites](#procedures-for-boundary-groups) mais adiante neste tópico.


###  <a name="BKMK_BoundarySiteAssignment"></a> Sobre atribuição de site  
 É possível configurar cada grupo de limites com um site atribuído para clientes.  

-   Um cliente recém-instalado que usa a atribuição automática de site ingressará no site atribuído de um grupo de limites que contém o local de rede atual do cliente.  
-   Depois de atribuir a um site, um cliente não altera a atribuição de site quando altera o local de rede. Por exemplo, se o cliente usa o perfil móvel em um novo local de rede que está representado por um limite em um grupo de limites com uma atribuição de site diferente, o site atribuído do cliente permanece inalterado.  
-   Quando a Descoberta de Sistemas do Active Directory encontra um novo recurso, as informações de rede para o recurso descoberto são avaliadas com os limites em grupos de limites. Esse processo associa o novo recurso a um site atribuído para uso do método de instalação do cliente por push.  
-   Quando um limite é um membro de vários grupos de limite que têm diferentes locais atribuídos, os clientes selecionarão aleatoriamente um desses sites.  
-   As alterações em um site atribuído de grupos de limite somente se aplicam a novas ações de atribuição de site. Os clientes atribuídos previamente a um site não reavaliam sua atribuição de site com base nas alterações da configuração de um grupo de limites (ou ao seu próprio local de rede).  

Para obter informações sobre a atribuição de site de cliente, consulte [Usando atribuição de site automática para computadores](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) em [Como atribuir clientes a um site no System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="BKMK_BoundaryContentLocation"></a> Sobre o local do conteúdo  
Quando você configura grupos de limites, associa limites (locais de rede) e funções do sistema de sites, como pontos de distribuição, ao grupo de limites. Isso ajuda a vincular os clientes aos servidores do sistema de sites como pontos de distribuição que estão localizados próximos aos clientes na rede.

Você pode atribuir o mesmo limite a vários grupos de limites e servidores de sistema de sites, como pontos de distribuição, podem ser associados a vários grupos de limites. Isso os torna disponíveis para uma variedade maior de locais de rede.

-   **Durante a distribuição de software**, os clientes solicitam um local para o conteúdo de implantação. O Configuration Manager envia ao cliente uma lista de pontos de distribuição associados a cada grupo de limites que inclui o local de rede atual do cliente.  
-   **Durante a implantação de sistema operacional**, os clientes solicitam um local para enviar ou receber suas informações de migração de estado. O Configuration Manager envia ao cliente uma lista de pontos de migração de estado associados a cada grupo de limites que inclui o local de rede atual do cliente.  

Você define os relacionamentos entre os grupos de limites para configurar o comportamento de fallback para os locais de fonte de conteúdo. Introduzido com a versão 1610, você configura os relacionamentos na nova guia **Relacionamentos** das propriedades do grupo de limites. Os relacionamentos substituem a necessidade de configurar os sistemas de sites para serem lentos ou rápidos ou de configurar um grupo de limites para permitir o local de origem de fallback para conteúdo.

Ao configurar um grupo de limites, que é chamado de grupo de limites **atual**, você adiciona outros grupos de limites para criar um link unidirecional do grupo de limites atual para cada grupo de limites adicionado. Os grupos de limites adicionados são chamados de grupos de limites **vizinhos**. Para cada link para um vizinho que criar, você poderá configurar pontos de distribuição com um tempo de fallback em minutos. Este tempo é usado para determinar após quanto tempo os clientes no grupo de limites atual poderão começar a usar os pontos de distribuição no grupo de limites vizinho se os clientes não conseguirem encontrar um local de fonte de conteúdo válido de seu grupo de limites atual.

Quando um cliente não consegue encontrar conteúdo e começa a pesquisar os locais dos grupos de limites vizinho, ele aumenta o pool de pontos de distribuição disponíveis para aquele cliente de uma maneira controlada.

-    Um grupo de limites pode ter mais de uma Relação. Isso permite que você configure o fallback para vizinhos diferentes para que ele ocorra após períodos de tempo diferentes.
-     Os clientes realizarão o fallback apenas para um grupo de limites que seja um vizinho de seu gripo de limites atual.
-    Quando um cliente é um membro de vários grupos de limites, o grupo de limite atual é definido como uma união de todos os grupos de limites do cliente. Esse cliente pode, então, realizar o fallback para um vizinho de qualquer um desses grupos de limites original.

Além dos links que você define, há um link implícito que é criado automaticamente entre os grupos de limites que você cria e o grupo de limites padrão que é criado automaticamente para cada site. Esse link automático:
-     É usado por clientes que não estão em um limite associado a nenhum grupo de limites na hierarquia. Os clientes usam automaticamente o grupo de limite padrão do seu site atribuído para identificar localizações de fontes de conteúdo válidas.
-     É uma opção de fallback padrão do grupo de limites atual para o grupo de limites padrão de sites que é usada após 120 minutos.

**Quando o conteúdo não está disponível de um grupo de limites atual:**  
Quando o conteúdo que está sendo solicitado por um cliente não está disponível de uma fonte de conteúdo válida em um grupo de limites atual, o cliente aguardará até o período de fallback para um grupo de limites do vizinho ou o grupo de limites do site padrão ser atingido antes que o cliente possa pesquisar fontes de conteúdo adicionais.

Se o conteúdo for distribuído sob demanda, mas não estiver disponível quando solicitado por um cliente, o processo para transferir o conteúdo para um ponto de distribuição no limite atual será iniciado.  



**Exemplo de uso do novo modelo:**   
Você cria três grupos de limites que não compartilham limites ou servidores de sistemas de sites:
-    Grupo BG_A com os pontos de distribuição DP_A1 e DP_A2 associados ao grupo
-    Grupo BG_B com os pontos de distribuição DP_B1 e DP_B2 associados ao grupo
-    Grupo BG_C com os pontos de distribuição DP_C1 e DP_C2 associados ao grupo

Você adiciona os locais de rede dos seus clientes como limites apenas para o grupo BG_A e, em seguida, configura relações daquele grupo de limites para os outros dois grupos de limites:
-    Você configura os pontos de distribuição para o primeiro grupo *vizinho* (BG_B) a ser usado depois de 10 minutos. Esse grupo contém os pontos de distribuição DP_B1 e DP_B2. Ambos estão bem conectadas aos primeiros locais de limite dos grupos.
-    Você configura o segundo grupo *vizinho* (BG_C) a ser usado depois de 20 minutos. Esse grupo contém os pontos de distribuição DP_C1 e DP_C2. Ambos estão em uma WAN dos outros dois grupos de limites.
-    Você também adiciona um ponto de distribuição que está localizado no servidor de site ao grupo de limites de site padrão dos sites. Esse é o local de fonte de conteúdo de menor preferência, mas está localizado centralmente para todos os seus grupos de limites.

    Exemplo de grupos de limites e tempos de fallback:

     ![BG_Fallack](media/BG_Fallback.png)


Com essa configuração:
-    O cliente inicia a pesquisa de conteúdo dos pontos de distribuição em seu grupo de limites *atual* (BG_A), pesquisando cada ponto de distribuição por dois minutos antes de alternar para o próximo ponto de distribuição no grupo de limites. O pool de clientes dos locais de fonte de conteúdo válidos incluem o DP_A1 e o DP_A2.
-    Se o cliente não conseguir localizar o conteúdo de seu grupo de limites *atual* depois de pesquisar por 10 minutos, ele adicionará os pontos de distribuição do grupo de limites BG_B à sua pesquisa. Então, ele continua a pesquisar o conteúdo de um ponto de distribuição em seu pool combinado de pontos de distribuição que agora inclui os dos grupos de limites BG_A e BG_B. O cliente continua a entrar em contato com cada ponto de distribuição por dois minutos antes de mudar para o próximo ponto de distribuição de seu pool. O pool de clientes dos locais de fonte de conteúdo válidos incluem DP_A1, DP_A2, DP_B1 e DP_B2.
-    Depois de mais 10 minutos (total de 20 minutos), se o cliente ainda não encontra um ponto de distribuição com o conteúdo, ele expande seu pool de pontos de distribuição disponíveis para os pontos do segundo grupo *vizinho*, o grupo de limites BG_C. O cliente agora tem 6 pontos de distribuição para pesquisar (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 e DP_C2) e continua a mudar para um novo ponto de distribuição a cada dois minutos até que o conteúdo seja encontrado.
-    Se o cliente não tiver encontrado conteúdo depois de um total de 120 minutos, ele realizará o fallback para incluir o *grupo de limites de site padrão* como parte de sua pesquisa contínua. Agora o pool de pontos de distribuição inclui todos os pontos de distribuição dos três grupos de limites configurados e o ponto de distribuição final localizado no computador do servidor do site.  O cliente continua, então, a pesquisa do conteúdo, alterando os pontos de distribuição a cada dois minutos até que o conteúdo seja encontrado.

Ao configurar os diferentes grupos vizinhos para estarem disponíveis em momentos diferentes, você controla quando pontos de distribuição específicos são adicionados como um local de fonte de conteúdo e quando, ou se, o cliente usa o fallback para o grupo de limites de site padrão como uma rede de segurança para o conteúdo que não está disponível em nenhum outro local.




### <a name="update-existing-boundary-groups-to-the-new-model"></a>Atualizar grupos de limites existentes para o novo modelo
Quando você atualiza para a versão 1610, as configurações a seguir são feitas automaticamente. Elas devem garantir que o comportamento de fallback atual permaneça disponível, até que você configure novos grupos de limites e relações.
-    Um grupo de limites de site padrão é criado para cada site primário, o nome é ***Default-Site-Boundary-Group&lt;sitecode>.***
-    Os pontos de distribuição com *Permitir local de origem de fallback para conteúdo* marcado e os pontos de migração de estado como sites primários são adicionados ao grupo de limites *Default-Site-Boundary-Group&lt;sitecode>* desse site.
-    É feita uma cópia de cada grupo de limites existente que inclui um servidor do site configurado com uma conexão lenta. O nome do novo grupo é ***&lt;nome do grupo de limites original>-&lt;ID do grupo de limites original>***:  
    -    Os sistemas de sites que têm uma conexão rápida são deixados no grupo de limites original.
    -    Uma cópia dos sistemas de sites (pontos de distribuição, pontos de gerenciamento e pontos de migração) que têm uma conexão lenta é adicionada à cópia do grupo de limites. Os sistemas de sites originais configurados como lentos permanecem no grupo de limites original para compatibilidade com versões anteriores, mas não são usados desse grupo de limites.
    -     Esta cópia do grupo de limites não tem limites associados a ela. No entanto, um link de fallback é criado entre o grupo original e a nova cópia de grupo de limites que tem o tempo de fallback definido como zero.  


- **Específico para sites secundários:**
  - Um grupo de limites será criado se um site secundário tiver pelo menos um ponto de distribuição com *Permitir local de origem de fallback para conteúdo* marcado ou um ponto de migração de estado. O nome do grupo de limites é ***Secondary-Site-Neighbor--Tmp&lt;Sitecode>.***
  - Todos os pontos de distribuição com *Permitir local de origem de fallback para conteúdo* marcado e pontos de migração de estado são adicionados a esse grupo de limites de site secundário recém-criado.
  - Um link de fallback é criado entre o grupo de limites original e o grupo de limites vizinho recém-criado e o tempo de fallback é definido como zero.


 A tabela a seguir identifica o novo comportamento de fallback que você pode esperar da combinação das configurações de ponto a distribuição e as configurações de implantação originais:

A configuração de implantação original para "Não executar programa" na rede lenta  |A configuração do ponto de distribuição original para “Allow client to use a fallback source location for content” (Permitir que o cliente use um local de fonte de fallback para o conteúdo)  |Novo comportamento de fallback  
---------|---------|---------
Selecionada     |  Selecionada    |  **Sem fallback** – usar apenas os pontos de distribuição no grupo de limites atual       
Selecionada     |  Não selecionada|  **Sem fallback** – usar apenas os pontos de distribuição no grupo de limites atual       
Não selecionada |  Não selecionada|  **Fallback para o vizinho** – usar os pontos de distribuição no grupo de limites atual e, em seguida, adicionar os pontos de distribuição do grupo de limite vizinho. A menos que um link explícito para o grupo de limites de site padrão esteja configurado, os clientes não realizarão o fallback para esse grupo.    
Não selecionada | Selecionada        |   **Fallback normal** – usar pontos de distribuição no grupo de limites atual, em seguida, os dos grupos de limites vizinho e padrão de site

 Todas as outras configurações de implantação resultam em **Fallback normal**.  



### <a name="changes-from-prior-versions-for-ui-and-behavior-for-content-locations"></a>Alterações de versões anteriores para a interface do usuário e comportamento para locais de conteúdo
A seguir estão as principais alterações de grupos de limites e como os clientes encontram conteúdo que foram introduzidas com a versão 1610. Muitas dessas alterações e conceitos funcionam em conjunto.


-    **As configurações para rápido ou lento foram removidas:** você não configura mais pontos de distribuição individuais para serem rápidos ou lentos.  Em vez disso, cada sistema de sites associado a um grupo de limites é tratado da mesma forma. Por causa dessa alteração, as guias **Referências** das propriedades do grupo de limites não dão mais suporte à configuração de Rápido ou Lento.
-     **Novo grupo de limites padrão em cada site:** cada site primário tem um novo grupo de limites padrão chamado ***Default-Site-Boundary-Group&lt;sitecode>***.  Quando um cliente não está em um local de rede que é atribuído a um grupo de limites, o cliente usará os sistemas de sites associados ao grupo padrão do seu site atribuído. Planeje usar esse grupo de limites como uma substituição para o conceito de local de conteúdo de fallback.      
 -    **'Allow fallback source locations for content' (Permitir locais de origem de fallback para conteúdo)** foi removido: você não configura mais explicitamente um ponto de distribuição para ser usado para o fallback e as opções essa configuração foram removidos da interface do usuário.

    Além disso, o resultado da configuração **Permitir que os clientes usem um local de origem de fallback para o conteúdo** em um tipo de implantação para aplicativos foi alterado. Essa configuração em um tipo de implantação agora permite que um cliente use o grupo de limites de site padrão como um local de fonte de conteúdo.

 -    **Relações de grupos de limites:** cada grupo de limites pode ser vinculado a um ou mais grupos de limites adicionais. Esses links formam relações que são configuradas na nova guia de propriedades de grupo limites chamada **Relações**:
     -    Cada grupo de limites ao qual o cliente está associado diretamente é chamado de grupo de limites **atual**.  
    -     Qualquer grupo de limites que um cliente possa usar devido a uma associação entre o grupo de limites *atual* desse cliente e outro grupo é chamado de grupo de limites **vizinho**.
    -  A guia **Relações** é o local em que você adiciona grupos de limites que podem ser usados como um grupo de limites *vizinho*. Você também pode configurar um tempo em minutos que determina quando um cliente que não consegue localizar o conteúdo de um ponto de distribuição no grupo *atual* começará a pesquisar locais de conteúdo daqueles grupos de limites *vizinhos*.

        Quando você adicionar ou alterar uma configuração de grupo de limites, terá a opção de bloquear o fallback para aquele grupo de limites específico daquele grupo atual que está sendo configurado.

    Para usar a nova configuração, você define associações explícitas (links) de um grupo de limites para outro e configura todos os pontos de distribuição nesse grupo associado com o mesmo tempo em minutos. O tempo que você configurar determina quando um cliente que não consegue localizar uma fonte de conteúdo de seu grupo de limites *atual* pode começar a pesquisar fontes de conteúdo desse grupo de limites vizinho.

    Além dos grupos de limites configurados explicitamente, cada grupo de limite tem um link implícito para o grupo de limites de site padrão. Este link se torna ativo após 120 minutos, momento em que o grupo de limites de site padrão se torna um grupo de limites vizinho, o que permite que os clientes usem os pontos de distribuição associados a aquele grupo de limites como locais de fonte de conteúdo.

    Esse comportamento substitui o que anteriormente era chamado de fallback de conteúdo.  Você pode substituir esse comportamento padrão de 120 minutos associando explicitamente o grupo de limites de site padrão a um grupo *atual* e definindo um tempo específico em minutos ou bloqueando totalmente o fallback para impedir seu uso.


-     **Os clientes tentam obter o conteúdo de cada ponto de distribuição por até dois minutos:** quando um cliente pesquisa um local de fonte de conteúdo, ele tenta acessar cada ponto de distribuição por dois minutos antes de tentar outro ponto de distribuição. Essa é uma alteração de versões anteriores em que os clientes tentavam se conectar a um ponto de distribuição por até duas horas.

    - O primeiro ponto de distribuição que um cliente tenta usar é selecionado aleatoriamente do pool de pontos de distribuição disponíveis no grupo (ou grupos) de limites *atual* do cliente.

    - Após dois minutos, se o cliente não encontrou o conteúdo, ele muda para um novo ponto de distribuição e tenta obter o conteúdo daquele servidor. Esse processo se repete a cada dois minutos até que o cliente localize o conteúdo ou atinja o último servidor em seu pool.

    - Se um cliente não conseguir encontrar um local de fonte de conteúdo válido de seu pool *atual* antes do período de fallback para um grupo de limites *vizinho*, ele adicionará os pontos de distribuição daquele grupo *vizinho* ao final de sua lista atual e pesquisará o grupo de locais de fonte de conteúdo expandido que inclui os pontos de distribuição dos dois grupos de limites.

        > [!TIP]  
        > Quando você cria um link explícito do grupo de limites atual para o grupo de limites de site padrão e define um tempo de fallback menor do que o tempo de fallback de um link para um grupo de limites vizinho, os clientes começam a pesquisar os locais de origem do grupo de limites de site padrão antes de incluir o grupo vizinho.

    - Quando o cliente falha em obter o conteúdo do último servidor no pool, ele inicia o processo novamente.





###  <a name="BKMK_PreferredMP"></a> Sobre pontos de gerenciamento preferenciais  
 Os pontos de gerenciamento preferenciais permitem que um cliente identifique um ponto de gerenciamento associado ao local de rede (limite) atual.  

-   Um cliente tenta usar um ponto de gerenciamento preferencial de seu site atribuído antes de usar um ponto de gerenciamento de seu site atribuído que não está configurado como preferencial.  
-   Para usar esta opção, é necessário habilitá-la para a hierarquia e configurar grupos de limite em sites primários individuais para incluir os pontos de gerenciamento que devem ser associados aos limites associados desse grupo de limites  
-   Quando os pontos de gerenciamento preferenciais são configurados e um cliente organiza sua lista de pontos de gerenciamento, o cliente coloca os pontos de gerenciamento preferenciais na parte superior de sua lista de pontos de gerenciamento atribuídos (que inclui todos os pontos de gerenciamento do site atribuído do cliente)  

> [!NOTE]  
>  Quando um cliente realiza roaming (o que significa alterar seus locais de rede, como quando um laptop passa para um local de escritório remoto), ele pode usar um ponto de gerenciamento (ou ponto de gerenciamento proxy) do site local em seu novo local antes de tentar usar um ponto de gerenciamento do seu site atribuído (que inclui os pontos de gerenciamento preferenciais).  Consulte [Entender como os clientes encontram serviços e recursos do site para o System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) para obter mais informações.  

###   <a name="BKMK_BoundaryOverlap"></a> Sobre a sobreposição de limites  
 O Configuration Manager dá suporte à sobreposição de configurações de limite para o local do conteúdo:  

-   **Quando um cliente solicita conteúdo** e o local de rede do cliente pertence a vários grupos de limites, o Configuration Manager envia ao cliente uma lista de todos os pontos de distribuição que têm o conteúdo.  
-   **Quando um cliente solicita a um servidor o envio ou recebimento de suas informações de migração de estado**, e o local de rede do cliente pertence a vários grupos de limites, o Configuration Manager envia ao cliente uma lista de todos os pontos de migração de estado associados a um grupo de limites que inclui o local de rede atual do cliente.  

Esse comportamento permite que o cliente selecione o servidor mais próximo do qual transferir o conteúdo ou as informações de migração de estado.  






## <a name="procedures-for-boundary-groups"></a>Procedimentos para grupos de limites
Os procedimentos a seguir se aplicam à versão 1610 ou posterior. Se você usa a versão 1511, 1602 ou 1606, consulte os procedimentos em [Boundary groups for System Center Configuration Manager versions 1511, 1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) (Grupos de limites para o System Center Configuration Manager versões 1511, 1602 e 1606).


### <a name="to-create-a-boundary-group"></a>Para criar um grupo de limites  
1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** >  **Grupos de Limites**.  

2.  Na guia **Início** , no grupo **Criar** , clique em **Criar Grupo de Limites**.  

3.  Na caixa de diálogo **Criar Grupo de Limites** , selecione a guia **Geral** e especifique um **Nome** para esse grupo de limites.  

4.  Clique em **OK** para salvar o novo grupo de limites.  


### <a name="to-configure-a-boundary-group"></a>Para configurar um grupo de limites  
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

 6.  Selecione a guia **Relacionamentos** para configurar o comportamento de fallback:  

     - Clique em **Adicionar** e selecione o grupo de limites que deseja configurar.

     - Defina um tempo de fallback para os pontos de distribuição. Após esse período, os clientes no grupo de limites para o qual você está configurando os relacionamentos poderão começar a pesquisar conteúdo dos pontos de distribuição do grupo de limites sendo adicionado.

     - Para evitar o fallback para um grupo de limites específico, incluindo o *grupo de limites de site padrão* que é configurado por padrão, selecione o grupo de limites e, em seguida, marque a caixa de seleção **Never fallback (Nunca realizar fallback)**.   

 7.  Clique em **OK** para fechar as propriedades do grupo de limites e salvar a configuração.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>Para associar um servidor de implantação de conteúdo ou um ponto de gerenciamento a um grupo de limite  
 1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** >  **Grupos de Limites**.  

 2.  Selecione o grupo de limites que você deseja modificar.  

 3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

 4.  Na caixa de diálogo **Propriedades** para o grupo de limites, selecione a guia **Referências** .  

 5.  Em **Selecionar servidores do sistema de sites**clique em **Adicionar**, marque a caixa de seleção para os servidores do sistema de site que deseja associar a esse grupo de limites e clique em **OK**.  

 6.  Clique em **OK** para fechar a caixa de diálogo e salvar a configuração do grupo de limites.  


#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>Para configurar um local de fallback para atribuição automática de site  

  1.  No console do Configuration Manager, clique em **Administração** > **Configuração do Site** >  **Sites**.  

  2.  Na guia **Início** , no grupo **Sites** , clique em **Configurações da Hierarquia**.  

  3.  Na guia **Geral** , marque a caixa de seleção **Usar um local de fallback**e selecione um local na lista suspensa **Local de fallback** .  

  4.  Clique em **OK** para salvar a configuração.  

#### <a name="to-enable-use-of-preferred-management-points"></a>para habilitar o uso de pontos de gerenciamento preferenciais  

 1.  No console do Configuration Manager, clique em **Administração** > **Configuração do Site** > **Sites** e, na guia **Início**, selecione **Configurações da Hierarquia**.  

 2.  Na guia **Geral** das Configurações da Hierarquia, selecione **Os clientes preferem usar os pontos de gerenciamento especificados nos grupos de limite**.  

 3.  Clique em **OK** para fechar a caixa de diálogo e salvar a configuração.  


### <a name="to-enable-use-of-pre-release-features"></a>Para habilitar o uso de recursos de pré-lançamento
1.  No console do Configuration Manager, clique em **Administração** > **Configuração do Site** > **Sites** e, na guia **Início**, selecione **Configurações da Hierarquia**.  

2.  Na guia **Geral** das Configurações de Hierarquia, selecione **Consentir o uso de recursos de pré-lançamento**.  

3.  Clique em **OK** para fechar a caixa de diálogo e salvar a configuração.  



##  <a name="BKMK_BoundaryBestPractices"></a> Melhores práticas para limites  

-   **Use uma combinação do menor número de limites que atendem às suas necessidades:**  
   No passado, era recomendável o uso de alguns tipos de limites em relação a os outros. Com as alterações para melhorar o desempenho, agora é recomendável que você use o tipo ou tipos de limites que escolher que funcionam para seu ambiente e que permitem que você use o menor número de limites possível para simplificar as tarefas de gerenciamento.      

-   **Evite a sobreposição de limites para atribuição automática de site:**  
     Embora cada grupo de limites dê suporte a configurações de atribuição de site e de local de conteúdo, é uma melhor prática para criar um conjunto separado de grupos de limites para usar apenas para atribuição de site. Significado: garanta que cada limite em um grupo de limites não seja membro de outro grupo de limites com uma atribuição de site diferente. Isso ocorre porque:  

    -   Um único limite pode ser incluído em vários grupos de limites  

    -   Cada grupo de limite pode ser associado um site primário diferente para atribuição de site  

    -   Um cliente em um limite que seja membro de dois grupos de limites diferentes com atribuições de site diferente selecionará aleatoriamente um site para ingressar, que pode não ser o site que você pretendia que o cliente ingressasse.  Essa configuração é chamada de limites sobrepostos.  

     Os limites sobrepostos não são um problema para o local do conteúdo, em vez disso, geralmente são uma configuração desejada que fornece recursos adicionais de clientes ou locais de conteúdo que eles podem usar.  

