---
title: Definir grupos de limites | Microsoft Docs
description: Entenda os grupos de limites que vinculam os clientes a sistemas de site no System Center Configuration Manager.
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: d940fd1bbf96767d44f8c55315e814be55a83897
ms.openlocfilehash: 5684fd4fbfd0ffb8f3ffbcfa122eef3dafd77327
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017


---
# <a name="configure-boundary-groups-for-system-center-configuration-manager"></a>Configurar grupos de limites para o System Center Configuration Manager


*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você usa grupos de limites no System Center Configuration Manager para agrupar de logicamente locais de rede ([limites](/sccm/core/servers/deploy/configure/boundaries)) relacionados para facilitar o gerenciamento da infraestrutura de rede. É necessário atribuir limites a grupos de limites para poder usar o grupo de limites.

Por padrão, o Configuration Manager cria um grupo de limites de site padrão em cada site.

> [!IMPORTANT]  
>  **As informações nesta seção de Grupos de limites e suas seções filho se aplicam à versão 1610 ou posterior.** Este conteúdo foi revisado para ser específico para alterações de design introduzidas para grupos de limites com esta versão de atualização.
>
> **Se você usar versões anteriores à 1610**, veja [Grupos de limites para as versões 1511, 1602 e 1606 do System Center Configuration Manager](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) para saber mais sobre como usar e configurar os grupos de limites com essas versões do produto.

Para configurar grupos de limites, associa limites (locais de rede) e funções do sistema de sites, como pontos de distribuição, ao grupo de limites. Isso ajuda a associar os clientes aos servidores do sistema de sites como pontos de distribuição que estão localizados próximos aos clientes na rede.

Quando você atribui o mesmo limite a vários grupos de limites e atribuir os mesmos servidores de sistema de sites, como pontos de distribuição, a vários grupos de limites, aumenta a disponibilidade dos sistemas de sites para uma ampla variedade de locais de rede.

Os clientes usam grupos de limites para:  

-   Atribuição automática de site  
-   Para localizar um servidor de sistema de sites que pode fornecer um serviço, incluindo:
    - Pontos de distribuição para o local do conteúdo
    -    Pontos de atualização de software (a partir da versão 1702)
    - Pontos de migração de estado
    - Pontos de gerenciamento preferenciais (se você usar pontos de gerenciamento preferenciais, deverá habilitar essa opção para a hierarquia, e não de dentro da configuração do grupo de limites. Veja [Para habilitar o uso de pontos de gerenciamento preferenciais](#to-enable-use-of-preferred-management-points) neste tópico).

##  <a name="boundary-groups-and-relationships"></a>Grupos de limites e relações
Para cada grupo de limites na sua hierarquia, você pode atribuir:

-  Um ou mais limites. Quando um cliente está em um local de rede que é definido como um limite atribuído a um grupo de limites específico, que é chamado de grupo de limites **atual**. Um cliente pode ter mais de um grupo de limites atual.
- Uma ou mais funções do sistema de sites.  Os clientes podem sempre usar funções de sistema de sites associadas ao seu grupo de limite atual. Dependendo das configurações adicionais, eles poderão usar funções de sistema de sites em grupos de limites adicionais.  

Para cada grupo de limites que você criar, você pode configurar um link unidirecional para outro grupo de limites. O link é chamado de uma **relação**. Os grupos de limites aos quais você vincula são chamados de grupos de limites **vizinhos**. Um grupo de limites pode ter várias relações, cada uma com um grupo de limites vizinho específico.

A configuração de cada relação determina quando um cliente que não consegue localizar que um servidor de sistema de sites disponível no seu grupo de limite atual pode começar a procurar um grupo de limites vizinho para localizar um sistema de site disponível. Essa pesquisa de grupos adicionais é chamada de **fallback**.

## <a name="fallback"></a>Fallback
Para evitar problemas para clientes quando eles não conseguem encontrar um sistema de sites disponível no seu grupo de limites atual, você deverá definir relações entre grupos de limites que definem o comportamento de fallback. O fallback permite que um cliente expanda sua pesquisa para grupos de limites adicionais para localizar um sistema de sites disponível.

As relações são configuradas na guia **Relações** das propriedades do grupo de limites. Quando você configura uma relação, define um link para um grupo de limites vizinho. Para cada tipo de função de sistema de site que tem suporte, você pode definir parâmetros de configuração independentes para fallback para esse grupo de limites vizinho. Por exemplo, quando você configura uma relação com um grupo de limites específico, pode definir fallback para pontos de distribuição ocorrerem após 20 minutos em vez do padrão de 120. Veja [Exemplo de como usar grupos de limites](#example-of-using-boundary-groups) para obter um exemplo mais amplo.

Se um cliente não conseguir localizar uma função de sistema de site disponível no seu grupo de limites atual, o cliente usará o tempo do fallback em minutos para determinar depois de quanto tempo ele pode começar a procurar um sistema de sites disponível que está associado com esse grupo de limites vizinho.  

Quando um cliente não consegue localizar um sistema de sites disponível e começa a pesquisar locais de grupos de limites vizinhos, ele aumenta o pool de sistemas de sites disponíveis que pode usar de maneira que seja definida pela sua configuração de grupos de limites e suas relações.

- Um grupo de limites pode ter mais de uma relação. Isso permite que você configure o fallback para cada tipo de sistema de site para vizinhos diferentes para que ele ocorra após períodos de tempo diferentes.    
- Os clientes realizarão o fallback apenas para um grupo de limites que seja um vizinho de seu gripo de limites atual.
- Quando um cliente é um membro de vários grupos de limites, o grupo de limite atual é definido como uma união de todos os grupos de limites do cliente. Esse cliente pode, então, realizar o fallback para vizinhos de qualquer um desses grupos de limites original.

### <a name="the-default-site-boundary-group"></a>O grupo de limite do site padrão
Além dos grupos de limites que você criar, cada site tem um grupo de limites de site padrão criado pelo Configuration Manager. Esse grupo é denominado ***Default-Site-Boundary-Group&lt;sitecode>***. Por exemplo, o grupo para o site ABC seria nomeado *Default-Site-Boundary-Group&lt;ABC>.*

Para cada grupo de limites que você criar, o Configuration Manager criará automaticamente um link implícito para cada grupo de limites de site padrão na hierarquia.
-    O link implícito é uma opção de fallback padrão de um grupo de limites atual para o grupo de limites padrão de sites que é tem um tempo de fallback padrão de 120 minutos.
-    Os clientes que não estão em um limite associado a um grupo de limites na sua hierarquia usam o grupo de limites de site padrão do seu site atribuído para identificar as funções de sistema de site válidas que podem usar.

Para gerenciar o fallback para o grupo de limites do site padrão:
- Você pode ir para as propriedades do grupo de limites de sites padrão e alterar os valores na guia **Comportamento Padrão**. As alterações feitas aqui se aplicam a *todos* os links implícitos para esse grupo de limites. Essas configurações poderão ser substituídas quando você configurar o link explícito para esse grupo de limites de site padrão de outro grupo de limites.
- Você pode ir para as propriedades de um grupo de limites que você criou e alterar os valores para o link explícito que vai para um grupo de limites de site padrão. Quando você define um novo tempo em minutos para realizar ou bloquear o fallback, essa alteração afeta somente o link que você está configurando. As configurações do link explícito substituem as da guia **Comportamento Padrão** do grupo de limites de site padrão.


## <a name="site-assignment"></a>Atribuição de site  
 É possível configurar cada grupo de limites com um site atribuído para clientes.  

-   Um cliente recém-instalado que usa a atribuição automática de site ingressará no site atribuído de um grupo de limites que contém o local de rede atual do cliente.  
-   Depois de atribuir a um site, um cliente não altera a atribuição de site quando altera o local de rede. Por exemplo, se o cliente usa o perfil móvel em um novo local de rede que está representado por um limite em um grupo de limites com uma atribuição de site diferente, o site atribuído do cliente permanece inalterado.  
-   Quando a Descoberta de Sistemas do Active Directory encontra um novo recurso, as informações de rede para o recurso descoberto são avaliadas com os limites em grupos de limites. Esse processo associa o novo recurso a um site atribuído para uso do método de instalação do cliente por push.  
-   Quando um limite é um membro de vários grupos de limite que têm diferentes locais atribuídos, os clientes selecionarão aleatoriamente um desses sites.  
-   As alterações em um site atribuído de grupos de limite somente se aplicam a novas ações de atribuição de site. Os clientes atribuídos previamente a um site não reavaliam sua atribuição de site com base nas alterações da configuração de um grupo de limites (ou ao seu próprio local de rede).  

Para obter informações sobre a atribuição de site de cliente, consulte [Usando atribuição de site automática para computadores](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) em [Como atribuir clientes a um site no System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

## <a name="distribution-points"></a>Pontos de distribuição

Quando um cliente solicita o local do ponto de distribuição, o Configuration Manager envia ao cliente uma lista que inclui os sistemas de site do tipo apropriado que estão associados a cada grupo de limites que inclui o local de rede atual dos clientes:

-   **Durante a distribuição de software**, os clientes solicitam um local para o conteúdo de implantação que está disponível em um ponto de distribuição ou outra fonte de conteúdo válido (como um cliente configurado para cache de pares).

-   **Durante a implantação de sistema operacional**, os clientes solicitam um local para enviar ou receber suas informações de migração de estado.  

Durante a implantação de conteúdo, se um cliente solicitar conteúdo que não está disponível de uma fonte no seu grupo de limites atual, o cliente continuará a solicitar esse conteúdo tentando diferentes fontes de conteúdo no seu grupo de limites atual até que o período de fallback para o grupo de limites vizinho ou grupo de limites de site padrão seja atingido. Se o cliente ainda não tiver encontrado o conteúdo, expandirá a pesquisa de fontes de conteúdo para incluir os grupos de limites vizinhos.

No entanto, se o conteúdo for distribuído sob demanda e não estiver disponível em um ponto de distribuição quando solicitado por um cliente, o processo para transferir o conteúdo para esse ponto de distribuição iniciará, e é possível que o cliente encontre esse servidor como uma fonte de conteúdo antes de fazer fallback para usar um grupo de limites vizinho.

## <a name="software-update-points"></a>Pontos de atualização de software
A partir da versão 1702, os clientes usam grupos de limites para localizar um novo ponto de atualização de software. Você pode adicionar pontos de atualização de software individuais a grupos de limites diferentes para controlar quais servidores um cliente pode encontrar.

Quando você atualiza de uma versão anterior à 1702, todos os pontos de atualização de software existentes são adicionados ao grupo de limites de site padrão em cada site. Isso mantém o comportamento anterior à atualização onde os clientes selecionam um ponto de atualização de software do conjunto de pontos de atualização de software disponíveis que você configurou para a hierarquia.  Esse comportamento é mantido até que você escolha adicionar pontos de atualização de software individuais a grupos de limites diferentes para seleção controlada e comportamento de fallback.

Se você instala um novo site que executa a versão 1702 ou posterior, atribua pontos de atualização de software para um grupo de limites para que os clientes possam localizar e usá-los.


O fallback para pontos de atualização de software é configurado como outras funções de sistema de site, mas tem as seguintes ressalvas:
- **Os novos clientes usam os grupos de limites para selecionar pontos de atualização de software.** Depois de instalar a versão 1702, os novos clientes que você instalar selecionarão um ponto de atualização de software dos que estiverem associados aos grupos de limites que você configurou.

  Isso substitui o comportamento anterior em que os clientes selecionavam um ponto de atualização de software aleatoriamente de uma lista dos que compartilham a floresta de clientes.

- **Clientes instalados anteriormente continuam a usar seu atual ponto de atualização de software até fazerem fallback para localizar um novo.** Os clientes que foram instalados anteriormente e que já têm um ponto de atualização de software continuarão a usar o ponto de atualização de software até esse servidor não poder ser alcançado. Isso inclui o uso contínuo de um ponto de atualização de software que não está associado ao grupo de limite atual do cliente.

  Quando um cliente que já tiver um ponto de atualização de software não conseguir localizá-lo, o cliente poderá então realizar fallback para localizar outro. Ao usar o fallback, o cliente recebe uma lista de todos os pontos de atualização de software do grupo de limites atual. Se ele não conseguir localizar um servidor disponível para 120 minutos, fará o fallback para seus grupos de limites vizinhos e o grupo de limites de sites padrão. O fallback para ambos os grupos de limites acontece ao mesmo tempo porque o tempo de fallback dos pontos de atualização de software para grupos de vizinho é definido como 120 minutos e não pode ser alterado. Esse tempo de 120 minutos também é o período padrão de fallback para o grupo de limites de site padrão. Quando um cliente faz fallback para um grupo de site padrão vizinho e padrão, o cliente tentará contatar os pontos de atualização de software do grupo de limites de vizinho antes de tentar usar um do grupo de limites do site padrão.

  O uso contínuo de um ponto de atualização de software existente, mesmo quando o servidor não estiver no grupo de limite atual do cliente, é intencional. Isso ocorre porque uma alteração do ponto de atualização de software pode resultar em um grande uso de largura de banda de rede à medida que o cliente sincroniza dados com o novo ponto de atualização de software. O atraso na transição pode ajudar a evitar a saturação de sua rede se todos os clientes mudarem para um novo ponto de atualização de software ao mesmo tempo.

- **Configurações de tempo de fallback:** ao contrário de configurações de fallback para outras funções do sistema de sites, os pontos de atualização de software ainda não dão suporte a um tempo configurável em minutos. Em vez disso, o comportamento de fallback é limitado ao seguinte:  
  - **Tempos de fallback (em minutos):** esta opção está desabilitada para pontos de atualização de software e não pode ser configurada. Está definido como 120 minutos.
  -     **Nunca realizar fallback:** você poderá bloquear o fallback para um ponto de atualização de software para um grupo de limites vizinho quando usar essa configuração.

## <a name="preferred-management-points"></a>Pontos de gerenciamento preferenciais

 Os pontos de gerenciamento preferenciais permitem que um cliente identifique um ponto de gerenciamento associado ao local de rede (limite) atual.  

-   Um cliente tenta usar um ponto de gerenciamento preferencial de seu site atribuído antes de usar um ponto de gerenciamento de seu site atribuído que não está configurado como preferencial.  
-   Para usar esta opção, é necessário habilitá-la para a hierarquia e, em seguida, configurar grupos de limite em sites primários individuais para incluir os pontos de gerenciamento que devem ser associados aos limites associados desse grupo de limites.  
-   Quando os pontos de gerenciamento preferenciais são configurados e um cliente organiza sua lista de pontos de gerenciamento, o cliente coloca os pontos de gerenciamento preferenciais na parte superior de sua lista de pontos de gerenciamento atribuídos (que inclui todos os pontos de gerenciamento do site atribuído do cliente).  

> [!NOTE]  
>  Quando um cliente realiza roaming (o que significa alterar seus locais de rede, como quando um laptop passa para um local de escritório remoto), ele pode usar um ponto de gerenciamento (ou ponto de gerenciamento proxy) do site local em seu novo local antes de tentar usar um ponto de gerenciamento do seu site atribuído (que inclui os pontos de gerenciamento preferenciais).  Consulte [Entender como os clientes encontram serviços e recursos do site para o System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) para obter mais informações.  

### <a name="overlapping-boundaries"></a>Sobreposição de limites  
 O Configuration Manager dá suporte à sobreposição de configurações de limite para o local do conteúdo:  

-   **Quando um cliente solicita conteúdo** e o local de rede do cliente pertence a vários grupos de limites, o Configuration Manager envia ao cliente uma lista de todos os pontos de distribuição que têm o conteúdo.  
-   **Quando um cliente solicita a um servidor o envio ou recebimento de suas informações de migração de estado**, e o local de rede do cliente pertence a vários grupos de limites, o Configuration Manager envia ao cliente uma lista de todos os pontos de migração de estado associados a um grupo de limites que inclui o local de rede atual do cliente.  

Esse comportamento permite que o cliente selecione o servidor mais próximo do qual transferir o conteúdo ou as informações de migração de estado.  



## <a name="example-of-using-boundary-groups"></a>Exemplo de como usar grupos de limites
O exemplo a seguir usa uma pesquisa de cliente por conteúdo de um ponto de distribuição. Este exemplo pode ser aplicado para outras funções de sistema de site que usam grupos de limites. No entanto, como se aplica a pontos de atualização de software, tenha em mente que os pontos de atualização de software não dão suporte à configuração de um tempo em minutos para fallback para um grupo de vizinho e sempre usam um período de 120 minutos.

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
Quando você atualiza para a versão anterior à 1610, as configurações a seguir são feitas automaticamente. Elas devem garantir que o comportamento de fallback atual permaneça disponível, até que você configure novos grupos de limites e relações.

-    Um grupo de limites de site padrão é criado para cada site primário, o nome é ***Default-Site-Boundary-Group&lt;sitecode>.***
  -    Os pontos de distribuição com *Permitir local de origem de fallback para conteúdo* marcado e os pontos de migração de estado como sites primários são adicionados ao grupo de limites *Default-Site-Boundary-Group&lt;sitecode>* desse site.
  -    A partir da versão 1702, os pontos de atualização de software são adicionados a *Default-Site-Boundary-Group&lt;sitecode>* de cada site.
-    É feita uma cópia de cada grupo de limites existente que inclui um servidor do site configurado com uma conexão lenta. O nome do novo grupo é ***&lt;nome do grupo de limites original>-&lt;ID do grupo de limites original>***:  
    -    Os sistemas de sites que têm uma conexão rápida são deixados no grupo de limites original.
    -    Uma cópia dos sistemas de sites (pontos de distribuição, pontos de gerenciamento) que têm uma conexão lenta é adicionada à cópia do grupo de limites. Os sistemas de sites originais configurados como lentos permanecem no grupo de limites original para compatibilidade com versões anteriores, mas não são usados desse grupo de limites.
    - Esta cópia do grupo de limites não tem limites associados a ela. No entanto, um link de fallback é criado entre o grupo original e a nova cópia de grupo de limites que tem o tempo de fallback definido como zero.  


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




## <a name="changes-from-prior-versions-for-ui-and-behavior-for-content-locations"></a>Alterações de versões anteriores para a interface do usuário e comportamento para locais de conteúdo
A seguir estão as principais alterações de grupos de limites e como os clientes encontram conteúdo. Essas alterações são introduzidas com a versão 1610. Muitas dessas alterações e conceitos funcionam em conjunto.


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


## <a name="procedures-for-boundary-groups"></a>Procedimentos para grupos de limites
Os procedimentos a seguir se aplicam à versão 1610 ou posterior. Se você usa a versão anterior à 1610, veja os procedimentos em [Grupos de limites para as versões 1511, 1602 e 1606 do System Center Configuration Manager](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).


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

#### <a name="to-associate-a-site-systme-server-with-a-boundary-group"></a>Para associar um servidor de sistema de sites a um grupo de limites  
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

