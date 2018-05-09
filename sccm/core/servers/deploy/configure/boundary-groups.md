---
title: Configurar grupos de limites
titleSuffix: Configuration Manager
description: Ajude os clientes a encontrar os sistemas de sites usando grupos de limites para organizar logicamente os locais de rede relacionados chamados limites
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79c6796c116fbe4d182827e24f41ae4d1e5242fe
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="configure-boundary-groups-for-system-center-configuration-manager"></a>Configurar grupos de limites para o System Center Configuration Manager


*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use grupos de limites no Configuration Manager para organizar logicamente os locais de rede ([limites](/sccm/core/servers/deploy/configure/boundaries)) relacionados a fim de facilitar o gerenciamento da infraestrutura. Atribua limites a grupos de limites antes de usar o grupo de limites.

Por padrão, o Configuration Manager cria um grupo de limites de site padrão em cada site.

Para configurar grupos de limites, associe limites (locais de rede) e funções do sistema de sites, como pontos de distribuição, ao grupo de limites. Essa configuração ajuda a associar os clientes aos servidores do sistema de sites como pontos de distribuição que estão localizados próximo aos clientes na rede.

Para aumentar a disponibilidade dos servidores dos sistemas de sites, como pontos de distribuição, para uma maior variedade de locais de rede, atribua o mesmo limite e o mesmo servidor a vários grupos de limites.

Os clientes usam grupos de limites para:  

-   Atribuição automática de site  
-   Para localizar um servidor de sistema de sites que pode fornecer um serviço, incluindo:
    - Pontos de distribuição para o local do conteúdo
    -   Pontos de atualização de software
    - Pontos de migração de estado
    - Pontos de gerenciamento preferenciais (se você usar pontos de gerenciamento preferenciais, deverá habilitar essa opção para a hierarquia, e não de dentro da configuração do grupo de limites. Veja [Para habilitar o uso de pontos de gerenciamento preferenciais](#to-enable-use-of-preferred-management-points) neste tópico).

##  <a name="boundary-groups-and-relationships"></a>Grupos de limites e relações
Para cada grupo de limites na sua hierarquia, você pode atribuir:

-  Um ou mais limites. O grupo de limites **atual** de um cliente é um local de rede definido como um limite atribuído a um grupo de limites específico. Um cliente pode ter mais de um grupo de limites atual.
- Uma ou mais funções do sistema de sites. Os clientes podem sempre usar funções de sistema de sites associadas ao seu grupo de limite atual. Dependendo das configurações adicionais, eles poderão usar funções de sistema de sites em grupos de limites adicionais.  

Para cada grupo de limites que você criar, você pode configurar um link unidirecional para outro grupo de limites. O link é chamado de uma **relação**. Os grupos de limites aos quais você vincula são chamados de grupos de limites **vizinhos**. Um grupo de limites pode ter várias relações, cada uma com um grupo de limites vizinho específico.

Quando um cliente não consegue encontrar um servidor do sistema de sites disponível em seu grupo de limites atual, a configuração de cada relação determina quando começar a pesquisar um grupo de limites vizinho. Essa pesquisa de grupos adicionais é chamada de **fallback**.

## <a name="fallback"></a>Fallback
Para evitar problemas quando os clientes não conseguem encontrar um sistema de sites disponível em seu grupo de limites atual, defina a relação entre grupos de limites para o comportamento de fallback. O fallback permite que um cliente expanda sua pesquisa para grupos de limites adicionais para localizar um sistema de sites disponível.

As relações são configuradas na guia **Relações** das propriedades do grupo de limites. Quando você configura uma relação, define um link para um grupo de limites vizinho. Para cada tipo de função do sistema de sites compatível, defina configurações independentes para o fallback nesse grupo de limites vizinho. Por exemplo, quando você configura uma relação com um grupo de limites específico, defina o fallback para os pontos de distribuição para que ele ocorra após 20 minutos, em vez do padrão de 120. Para obter um exemplo mais abrangente, consulte [Exemplo de como usar grupos de limites](#example-of-using-boundary-groups).

Se um cliente não conseguir encontrar uma função do sistema de sites disponível em seu grupo de limites atual, o cliente usará o tempo de fallback em minutos. O tempo de fallback determina quando o cliente começa a pesquisar um sistema de sites disponível associado ao grupo de limites vizinho.  

Quando um cliente não consegue encontrar um sistema de sites disponível e começa a pesquisar os locais dos grupos de limites vizinhos, ele aumenta o pool de sistemas de sites disponíveis. A configuração de grupos de limites e suas relações define o uso do cliente desse pool de sistemas de sites disponíveis.

- Um grupo de limites pode ter mais de uma relação. Com várias relações, configure o fallback de cada tipo de sistema de sites em vizinhos diferentes para que ele ocorra após períodos diferentes.    
- Os clientes realizam o fallback apenas para um grupo de limites que seja um vizinho de seu gripo de limites atual.
- Quando um cliente é membro de vários grupos de limites, o grupo de limites atual é definido como uma união de todos os grupos de limites do cliente. O cliente pode fazer fallback nos vizinhos de um desses grupos de limites originais.

### <a name="the-default-site-boundary-group"></a>O grupo de limite do site padrão
Além dos grupos de limites que você criar, cada site tem um grupo de limites de site padrão criado pelo Configuration Manager. Esse grupo é denominado ***Default-Site-Boundary-Group&lt;sitecode>***. Por exemplo, o grupo para o site ABC seria nomeado *Default-Site-Boundary-Group&lt;ABC>.*

Para cada grupo de limites que você criar, o Configuration Manager criará automaticamente um link implícito para cada grupo de limites de site padrão na hierarquia.
-   O link implícito é uma opção de fallback padrão de um grupo de limites atual para o grupo de limites padrão de sites que é tem um tempo de fallback padrão de 120 minutos.
-   Para os clientes que não estão em um limite associado a nenhum grupo de limites: para identificar funções do sistema de sites válidas, use o grupo de limites do site padrão de seu site atribuído.

Para gerenciar o fallback para o grupo de limites do site padrão:
- Abra as propriedades do grupo de limites do site padrão e altere os valores na guia **Comportamento Padrão**. As alterações feitas aqui se aplicam a *todos* os links implícitos para esse grupo de limites. Essas configurações poderão ser substituídas quando você configurar o link explícito para esse grupo de limites de site padrão de outro grupo de limites.
- Abra as propriedades de um grupo de limites personalizado. Altere os valores do link explícito para um grupo de limites do site padrão. Quando você define um novo tempo em minutos para realizar ou bloquear o fallback, essa alteração afeta somente o link que você está configurando. A configuração do link explícito substitui as configurações da guia **Comportamento Padrão** do grupo de limites do site padrão.


## <a name="site-assignment"></a>Atribuição de site  
 É possível configurar cada grupo de limites com um site atribuído para clientes.  

-   Um cliente recém-instalado que usa a atribuição automática de site ingressa no site atribuído de um grupo de limites que contém o local de rede atual do cliente.  
-   Depois de atribuir a um site, um cliente não altera a atribuição de site quando altera o local de rede. Por exemplo, se o cliente usa um perfil móvel em um novo local de rede representado por um limite em um grupo de limites com outra atribuição de site, o site atribuído do cliente permanece inalterado.  
-   Quando a Descoberta de Sistemas do Active Directory encontra um novo recurso, as informações de rede para o recurso descoberto são avaliadas com os limites em grupos de limites. Esse processo associa o novo recurso a um site atribuído para uso do método de instalação do cliente por push.  
-   Quando um limite é um membro de vários grupos de limites que têm diferentes locais atribuídos, os clientes selecionarão aleatoriamente um desses sites.  
-   As alterações em um site atribuído de grupos de limite somente se aplicam a novas ações de atribuição de site. Os clientes atribuídos anteriormente a um site não reavaliam sua atribuição de site com base nas alterações da configuração de um grupo de limites (ou de seu próprio local de rede).  

Para obter informações sobre a atribuição de site de cliente, consulte [Usando atribuição de site automática para computadores](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) em [Como atribuir clientes a um site no System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

## <a name="distribution-points"></a>Pontos de distribuição

Quando um cliente solicita o local de um ponto de distribuição, o Configuration Manager envia ao cliente uma lista de sistemas de sites. Esses sistemas de sites são do tipo apropriado associado a cada grupo de limites que inclui o local de rede atual dos clientes:

-   **Durante a distribuição de software**, os clientes solicitam um local para o conteúdo de implantação que está disponível em um ponto de distribuição ou outra fonte de conteúdo válido (como um cliente configurado para cache de pares).

-   **Durante a implantação de sistema operacional**, os clientes solicitam um local para enviar ou receber suas informações de migração de estado.  

Durante a implantação de conteúdo, se um cliente solicita um conteúdo que não está disponível em uma origem em seu grupo de limites atual, o cliente continua solicitando esse conteúdo. O cliente tenta diferentes fontes de conteúdo em seu grupo de limites atual até atingir o período de fallback de um grupo de limites vizinho ou do grupo de limites do site padrão. Se o cliente ainda não tiver encontrado o conteúdo, expandirá a pesquisa de fontes de conteúdo para incluir os grupos de limites vizinhos.

Se o conteúdo é distribuído sob demanda, mas não fica disponível em um ponto de distribuição quando solicitado por um cliente, o processo de transferência do conteúdo para esse ponto de distribuição é iniciado. É possível que o cliente encontre o servidor como uma fonte de conteúdo antes de fazer fallback para usar um grupo de limites vizinho.

## <a name="software-update-points"></a>Pontos de atualização de software
Os clientes usam grupos de limites para encontrar um novo ponto de atualização de software. Para controlar quais servidores um cliente pode encontrar, adicione pontos de atualização de software individuais a grupos de limites diferentes.

Se você atualizar de uma versão anterior à 1702, cada site adicionará todos os pontos de atualização de software existentes ao grupo de limites do site padrão. Esse comportamento de atualização do site mantém o comportamento anterior do cliente para selecionar um ponto de atualização de software no pool de servidores disponíveis. Esse comportamento é mantido até que você escolha adicionar pontos de atualização de software individuais a grupos de limites diferentes para seleção controlada e comportamento de fallback.

Se você instalar um novo site, os pontos de atualização de software não serão adicionados ao grupo de limites do site padrão. Atribua pontos de atualização de software a um grupo de limites para que os clientes possam localizar e usá-los.

### <a name="fallback-for-software-update-points"></a>Fallback para pontos de atualização de software
O fallback para pontos de atualização de software é configurado como outras funções de sistema de site, mas tem as seguintes ressalvas:
- **Os novos clientes usam os grupos de limites para selecionar pontos de atualização de software.** Os novos clientes instalados selecionam um ponto de atualização de software dos servidores associados aos grupos de limites configurados. Esse comportamento substitui o comportamento anterior, em que os clientes selecionam um ponto de atualização de software aleatoriamente de uma lista dos servidores que compartilham a floresta do cliente.

- **Os clientes continuam a usar um último ponto de atualização de software válido até fazerem fallback para localizar um novo.** Os clientes que já têm um ponto de atualização de software continuam usando-o até que ele não possa ser acessado. Esse comportamento inclui o uso contínuo de um ponto de atualização de software que não está associado ao grupo de limites atual do cliente.

  O uso contínuo de um ponto de atualização de software existente, mesmo quando o servidor não está no grupo de limites atual do cliente, é intencional. Quando o ponto de atualização de software é alterado, o cliente sincroniza os dados com o novo servidor, o que gera um uso de rede significativo. Se todos os clientes alternam para um novo servidor ao mesmo tempo, o atraso na transição ajuda a evitar a saturação da rede.

- **Um cliente sempre tenta acessar seu último ponto de atualização de software válido por 120 minutos antes de iniciar o fallback.** Depois de 120 minutos, se o cliente não tiver estabelecido contato, ele começará o fallback. Quando o fallback começa, o cliente recebe uma lista de todos os pontos de atualização de software do grupo de limites atual. Pontos de atualização de software adicionais de grupos de limites vizinhos e do site padrão estão disponíveis com base nas configurações de fallback.

### <a name="fallback-configurations-for-software-update-points"></a>Configurações de fallback para pontos de atualização de software
#### <a name="beginning-with-version-1706"></a>A partir da versão 1706   
Você pode configurar **Tempos de Fallback (em minutos)** para pontos de atualização de software como menos de 120 minutos. No entanto, o cliente ainda tenta atingir seu ponto de atualização de software original de 120 minutos. Em seguida, ele expande sua pesquisa para outros servidores. Os tempos de fallback do grupo de limites começam quando o cliente não consegue acessar primeiro seu servidor original. Quando o cliente expande sua pesquisa, o site fornece os grupos de limites configurados com menos de 120 minutos.

Para bloquear o fallback de um ponto de atualização de software em um grupo de limites vizinho, defina a configuração para **Nunca fazer fallback**.

Após não conseguir acessar o servidor original durante duas horas, o cliente usa um ciclo mais curto para estabelecer uma conexão com um novo ponto de atualização de software. Esse comportamento permite que o cliente pesquise rapidamente a lista cada vez maior de pontos de atualização de software potenciais.

 -  **Exemplo de fallback:**  
    O grupo de limites atual de um cliente tem um fallback para os pontos de atualização de software configurado como *10* minutos para o grupo de limites *A* e *130* minutos para o grupo de limites *B*. Quando o cliente falha em acessar seu último ponto de atualização de software válido:
    -   O cliente tenta acessar somente seu servidor original nos próximos 120 minutos. Após 10 minutos, os pontos de atualização de software do grupo de limites A são adicionados ao pool de servidores disponíveis. No entanto, o cliente não pode tentar contatá-los, ou qualquer outro servidor, até que o período inicial de 120 minutos para reconexão com o servidor original tenha passado.
    -   Depois de tentar localizar o ponto de atualização de software original por 120 minutos, o cliente pode expandir sua pesquisa. Nesse momento, o cliente adiciona servidores ao pool disponível de pontos de atualização de software que estão em seu grupo de limites atual e em grupos de limites vizinhos configurados com 120 minutos ou menos. Esse pool inclui os servidores no grupo de limites A, que foram adicionados anteriormente ao pool de servidores disponíveis.
    -       Após mais 10 minutos (130 minutos de tempo total após a primeira falha do cliente em acessar seu último ponto de atualização de software válido), o cliente expande a pesquisa a fim de incluir os pontos de atualização de software do grupo de limites B.  

#### <a name="prior-to-version-1706"></a>Antes da versão 1706
Antes da versão 1706, as configurações de fallbacks para pontos de atualização de software não dão suporte a um tempo configurável em minutos. Em vez disso, o comportamento de fallback é limitado ao seguinte:

  - **Tempos de fallback (em minutos):** essa fica esmaecida para pontos de atualização de software e não pode ser configurada. Está definido como 120 minutos.
  -     **Nunca realizar fallback:** você poderá bloquear o fallback para um ponto de atualização de software para um grupo de limites vizinho quando usar essa configuração.

Quando um cliente que já tem um ponto de atualização de software não consegue acessá-lo, o cliente pode então fazer fallback para encontrar outro. Ao usar o fallback, o cliente recebe uma lista de todos os pontos de atualização de software do grupo de limites atual. Se ele não consegue encontrar um servidor disponível em 120 minutos, ele faz fallback em seus grupos de limites vizinhos e no grupo de limites do site padrão. O fallback para ambos os grupos de limites ocorre ao mesmo tempo. O tempo de fallback do ponto de atualização de software para grupos vizinhos é definido como 120 minutos. Não é possível alterar esse tempo de fallback. Esse tempo de 120 minutos também é o período padrão de fallback para o grupo de limites de site padrão. Quando um cliente faz fallback para um grupo de site padrão vizinho e padrão, o cliente tentará contatar os pontos de atualização de software do grupo de limites de vizinho antes de tentar usar um do grupo de limites do site padrão.

### <a name="manually-switch-to-a-new-software-update-point"></a>Mudar manualmente para um novo ponto de atualização de software
Além de usar o fallback, você pode usar *Notificação do Cliente* para forçar manualmente um dispositivo a alternar para um novo ponto de atualização de software.

Quando você alternar para um novo servidor, os dispositivos usam fallback para localizar esse novo servidor. Examine as configurações do grupo de limites. Garanta que os pontos de atualização de software estão nos grupos de limites corretos antes de iniciar essa alteração.

Para saber mais, confira [Mudar manualmente clientes para um novo ponto de atualização de software](/sccm/sum/plan-design/plan-for-software-updates#manually-switch-clients-to-a-new-software-update-point).



## <a name="management-points"></a>Pontos de gerenciamento
<!-- 1324594 -->
A partir da versão 1802, configure relações de fallback para os pontos de gerenciamento entre grupos de limites. Esse comportamento proporciona maior controle para os pontos de gerenciamento que os clientes usam. Na guia **Relações** das propriedades do grupo de limites, há uma coluna para o ponto de gerenciamento. Quando você adiciona um novo grupo de limites de fallback, o tempo de fallback para o ponto de gerenciamento é sempre zero (0). Esse comportamento é o mesmo para o **Comportamento padrão** no grupo de limites padrão do site.

Anteriormente, um problema comum ocorre quando você possui um ponto de gerenciamento protegido em uma rede segura. Os clientes da rede corporativa principal recebem políticas que incluem esse ponto de gerenciamento protegido, mesmo que não possam se comunicar com ele em um firewall. Para solucionar esse problema, use a opção **Nunca realizar fallback** para garantir que os clientes apenas retornem aos pontos de gerenciamento com os quais eles podem se comunicar.

Ao atualizar o site para a versão 1802, o Configuration Manager adiciona todos os pontos de gerenciamento que não são direcionados para a Internet ao grupo de limites padrão do site. Esse comportamento de upgrade garante que as versões mais antigas do cliente continuem a se comunicar com pontos de gerenciamento. Para aproveitar ao máximo esse recurso, mova seus pontos de gerenciamento para os grupos de limites desejados.

O fallback do grupo de limites do ponto de gerenciamento não altera o comportamento durante a instalação do cliente (ccmsetup.exe). Se a linha de comando não especificar o ponto de gerenciamento inicial usando o parâmetro /MP, o novo cliente recebe a lista completa de pontos de gerenciamento disponíveis. Para o processo inicial de inicialização, o cliente usa o primeiro ponto de gerenciamento que ele pode acessar. Uma vez que o cliente estiver registrado no site, ele recebe a lista de pontos de gerenciamento ordenada corretamente com esse novo comportamento. 

Para que os clientes usem essa funcionalidade, habilite a seguinte configuração: **Os clientes preferem usar os pontos de gerenciamento especificados nos grupos de limites** em **Configurações da Hierarquia**. 

> [!Note]
> Os processos de implantação de sistema operacional não estão conscientes dos grupos de limites.

### <a name="troubleshooting"></a>Solução de problemas
Novas entradas aparecem no **LocationServices.log**. O atributo **Localidade** identifica um dos seguintes estados:
- 0: Desconhecido
- 1: O ponto de gerenciamento especificado está apenas no grupo de limites padrão do site para o fallback
- 2: O ponto de gerenciamento especificado está em um grupo de limites remoto ou vizinho. Quando o ponto de gerenciamento está em um grupo vizinho ou em grupos de limites padrão do site, a localidade é 2.
- 3: O ponto de gerenciamento especificado está no grupo de limites local ou atual. Quando o ponto de gerenciamento está no grupo de limites atual, bem como em um grupo vizinho ou em um grupo de limites padrão do site, a localidade é 3. Se você não habilitar a configuração de pontos de gerenciamento preferenciais nas Configurações de Hierarquia, a localidade será sempre 3, independentemente do grupo de limites em que o ponto de gerenciamento esteja.

Os clientes usam os pontos de gerenciamento local primeiro (localidade 3), em seguida os remotos (localidade 2) e depois os fallbacks (localidade 1). 

Quando um cliente recebe cinco erros em 10 minutos e não se comunica com um ponto de gerenciamento em seu grupo de limites atual, ele tenta contatar um ponto de gerenciamento em um grupo de limites vizinho ou no grupo de limites padrão do site. Se o ponto de gerenciamento no atual grupo de limites voltar a ficar online mais tarde, o cliente retornará ao ponto de gerenciamento local no próximo ciclo de atualização. O ciclo de atualização é de 24 horas, ou quando o serviço do agente do Configuration Manager é reiniciado.




## <a name="preferred-management-points"></a>Pontos de gerenciamento preferenciais

 > [!Note]
 > O comportamento dessa configuração da hierarquia, **Os clientes preferem usar os pontos de gerenciamento especificados nos grupos de limites**, é alterado a partir da versão 1802. Quando você habilita essa configuração, o Configuration Manager usa a funcionalidade do grupo de limites para o ponto de gerenciamento atribuído. Para obter mais informações, consulte [Pontos de gerenciamento](#management-points). 

 Os pontos de gerenciamento preferenciais permitem que um cliente identifique um ponto de gerenciamento associado ao local de rede (limite) atual.  

-   Um cliente tenta usar um ponto de gerenciamento preferencial de seu site atribuído antes de usar um não configurado como preferencial de seu site atribuído.  
-   Para usar essa opção, habilite a configuração **Os clientes preferem usar os pontos de gerenciamento especificados em grupos de limites** em **Configurações da Hierarquia**. Em seguida, configure grupos de limites em sites primários individuais. Inclua os pontos de gerenciamento que devem ser associados aos limites associados do grupo de limites.
-   Quando você configura os pontos de gerenciamento preferenciais e um cliente organiza sua lista de pontos de gerenciamento, o cliente coloca os pontos de gerenciamento preferenciais no início da lista. Essa lista inclui todos os pontos de gerenciamento do site atribuído do cliente.  

> [!NOTE]  
>  Roaming do cliente significa que ele altera seus locais de rede. Por exemplo, quando um laptop passa para um local de escritório remoto. Quando um cliente usa um perfil móvel, ele pode usar um ponto de gerenciamento ou um ponto de gerenciamento proxy do site local em seu novo local antes de tentar usar um servidor de seu site atribuído. Essa lista de servidores de seu site atribuído inclui os pontos de gerenciamento preferenciais. Para obter mais informações, consulte [Entender como os clientes encontram serviços e recursos do site](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="overlapping-boundaries"></a>Sobreposição de limites  
 O Configuration Manager dá suporte à sobreposição de configurações de limite para o local do conteúdo. Quando o local de rede do cliente pertence a vários grupos de limites:

-   Quando um cliente solicita o conteúdo, o Configuration Manager envia ao cliente uma lista de todos os pontos de distribuição que têm o conteúdo.  
-   Quando um cliente solicita a um servidor o envio ou recebimento de suas informações de migração de estado, o Configuration Manager envia ao cliente uma lista de todos os pontos de migração de estado associados a um grupo de limites que inclui o local de rede atual do cliente.  

Esse comportamento permite que o cliente selecione o servidor mais próximo do qual transferir o conteúdo ou as informações de migração de estado.  



## <a name="example-of-using-boundary-groups"></a>Exemplo de como usar grupos de limites
O exemplo a seguir usa uma pesquisa de cliente por conteúdo de um ponto de distribuição. Este exemplo pode ser aplicado para outras funções de sistema de site que usam grupos de limites. Tenha em mente que pontos de atualização de software não dão suporte à configuração de fallback para um grupo vizinho e sempre usam um período de 120 minutos.

Você cria três grupos de limites que não compartilham limites ou servidores de sistemas de sites:
-   Grupo BG_A com os pontos de distribuição DP_A1 e DP_A2 associados ao grupo
-   Grupo BG_B com os pontos de distribuição DP_B1 e DP_B2 associados ao grupo
-   Grupo BG_C com os pontos de distribuição DP_C1 e DP_C2 associados ao grupo

Adicione os locais de rede dos clientes como limites somente ao grupo de limites BG_A. Em seguida, configure as relações desse grupo de limites com os outros dois grupos de limites:
-   Configure os pontos de distribuição para o primeiro grupo *vizinho* (BG_B) a ser usado após 10 minutos. Esse grupo contém os pontos de distribuição DP_B1 e DP_B2. Ambos estão bem conectadas aos primeiros locais de limite dos grupos.
-   Configure o segundo grupo *vizinho* (BG_C) a ser usado após 20 minutos. Esse grupo contém os pontos de distribuição DP_C1 e DP_C2. Ambos estão em uma WAN dos outros dois grupos de limites.
-   Adicione também ao grupo de limites do site padrão dos sites outro ponto de distribuição localizado no servidor do site. Esse servidor é o local de fonte de conteúdo de menor preferência, mas está localizado centralmente para todos os grupos de limites.

    Exemplo de grupos de limites e tempos de fallback:

     ![Exemplo de grupos de limites e tempos de fallback](media/BG_Fallback.png)


Com essa configuração:
-   O cliente começa a pesquisar o conteúdo nos pontos de distribuição em seu grupo de limites *atual* (BG_A). Ele pesquisa cada ponto de distribuição por dois minutos e, em seguida, alterna para o próximo ponto de distribuição no grupo de limites. O pool de clientes dos locais de fonte de conteúdo válidos incluem o DP_A1 e o DP_A2.
-   Se o cliente não conseguir localizar o conteúdo de seu grupo de limites *atual* depois de pesquisar por 10 minutos, ele adicionará os pontos de distribuição do grupo de limites BG_B à sua pesquisa. Ele então continua pesquisando o conteúdo de um ponto de distribuição em seu pool combinado de servidores. Esse pool agora inclui servidores dos grupos de limites BG_A e BG_B. O cliente continua acessando cada ponto de distribuição por dois minutos e, em seguida, alterna para o próximo servidor em seu pool. O pool de clientes dos locais de fonte de conteúdo válidos incluem DP_A1, DP_A2, DP_B1 e DP_B2.
-   Depois de mais 10 minutos (total de 20 minutos), se o cliente ainda não encontra um ponto de distribuição com o conteúdo, ele expande seu pool para incluir os servidores disponíveis do segundo grupo *vizinho*, o grupo de limites BG_C. O cliente agora tem seis pontos de distribuição de pesquisa (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 e DP_C2). Ele continua mudando para um novo ponto de distribuição a cada dois minutos até encontrar o conteúdo.
-   Se o cliente não tiver encontrado conteúdo depois de um total de 120 minutos, ele realizará o fallback para incluir o *grupo de limites de site padrão* como parte de sua pesquisa contínua. Agora o pool inclui todos os pontos de distribuição dos três grupos de limites configurados e o ponto de distribuição final localizado no servidor do site. O cliente continua, então, a pesquisa do conteúdo, alterando os pontos de distribuição a cada dois minutos até que o conteúdo seja encontrado.

Ao configurar os grupos vizinhos diferentes para estarem disponíveis em horários diferentes, controle quando pontos de distribuição específicos são adicionados como um local de fonte de conteúdo. O cliente usa o fallback para o grupo de limites do site padrão como uma rede de segurança para o conteúdo que não está disponível em nenhum outro local.





<!--
### Update existing boundary groups to the new model
When you update to version prior to 1610, the following configurations are automatically made. This behavior ensures your current fallback behavior remains available until you configure new boundary groups and relationships.

-   Each primary site creates a default site boundary group named ***Default-Site-Boundary-Group&lt;sitecode>***.
  - The primary site adds to the *Default-Site-Boundary-Group&lt;sitecode>* boundary group any state migration points and distribution points configured to **Allow fallback source location for content**.
  - The site adds software update points to the *Default-Site-Boundary-Group&lt;sitecode>* boundary group.
-   The site makes a copy of each existing boundary group that includes a site server configured with a slow connection. The name of the new group is ***&lt;original boundary group name>-&lt;original boundary group ID>***:  
    -   Site systems that have a fast connection are left in the original boundary group.
    -   A copy of site systems (distribution points, management points) that have a slow connection are added to the copy of the boundary group. The original site systems configured as slow remain in their original boundary groups for backward compatibility, but are not used from those boundary groups.
    - This boundary group copy does not have boundaries associated with it. However, A fallback link is created between the original group and the new boundary group copy that has the fallback time set to zero.  


- **Specific to secondary sites:**
  - If a secondary site has at least one state migration point or distribution point enabled to **Allow fallback source location for content**, Configuration Manager creates a boundary group named ***Secondary-Site-Neighbor--Tmp&lt;Sitecode>***. 
  - All distribution points enabled to **Allow fallback source location for content** and state migration points are added to this secondary site boundary group.
  - A fallback link is created between the original boundary group and the newly created neighbor boundary group. The fallback time is set to zero.


 The following table identifies the new fallback behavior you can expect from the combination the original deployment settings and distribution point configurations:

Original deployment configuration for “Do not run program” in slow network  |Original distribution point configuration for “Allow client to use a fallback source location for content”  |New fallback behavior  
---------|---------|---------
Selected     |  Selected    |  **No fallback** - Only use the distribution points in current boundary group       
Selected     |  Not selected|  **No fallback** - Only use the distribution points in current boundary group       
Not selected |  Not selected|  **Fallback to neighbor** - Use the distribution points in current boundary group, and then add the distribution points from the neighbor boundary group. Unless an explicit link to the default site boundary group is configured, clients do not fallback to that group.    
Not selected | Selected     |   **Normal fallback** - Use distribution points in current boundary group, then servers from the neighbor and site default boundary groups

 All other deployment configurations result in **Normal fallback**.  
-->



## <a name="changes-from-prior-versions"></a>Alterações de versões anteriores
Veja a seguir as principais alterações nos grupos de limites e como os clientes encontram o conteúdo no Configuration Manager Branch Atual. Muitas dessas alterações e conceitos funcionam em conjunto.


-   As configurações para Rápido ou Lento foram removidas: você não configura mais pontos de distribuição individuais para serem rápidos ou lentos. Em vez disso, cada sistema de sites associado a um grupo de limites é tratado da mesma forma. Por causa dessa alteração, as guias **Referências** das propriedades do grupo de limites não dão mais suporte à configuração de Rápido ou Lento.
- Novo grupo de limites padrão em cada site: cada site primário tem um novo grupo de limites padrão chamado ***Default-Site-Boundary-Group&lt;sitecode>***. Quando um cliente não está em um local de rede atribuído a um grupo de limites, ele usa os sistemas de sites associados ao grupo padrão de seu site atribuído. Planeje usar esse grupo de limites como uma substituição para o conceito de local de conteúdo de fallback.   
 -  A configuração **Permitir locais de origem de fallback para o conteúdo** foi removida: você não configura mais explicitamente um ponto de distribuição a ser usado para o fallback. As opções para definir essa configuração foram removidas do console.

    Além disso, o resultado da configuração **Permitir que os clientes usem um local de origem de fallback para o conteúdo** em um tipo de implantação para aplicativos foi alterado. Essa configuração em um tipo de implantação agora permite que um cliente use o grupo de limites de site padrão como um local de fonte de conteúdo.

 -  Relações entre grupos de limites: cada grupo de limites pode ser vinculado a um ou mais grupos de limites adicionais. Esses links formam relações que são configuradas na nova guia de propriedades de grupo limites chamada **Relações**:
    -   Cada grupo de limites ao qual o cliente está associado diretamente é chamado de grupo de limites **atual**.  
    -   Qualquer grupo de limites que um cliente pode usar devido a uma associação entre o grupo de limites *atual* desse cliente e outro grupo é chamado de grupo de limites **vizinho**.
    -  Na guia **Relações**, adicione grupos de limites para usá-los como um grupo de limites *vizinho*. Configure também um tempo em minutos para o fallback. Quando um cliente não consegue encontrar o conteúdo em um ponto de distribuição em seu grupo *atual*, esse tempo é quando o cliente começa a pesquisar os locais de conteúdo nos grupos de limites *vizinhos*.

        Quando você adiciona ou altera uma configuração de grupo de limites, você tem a opção de bloquear o fallback para esse grupo de limites específico do grupo atual que está sendo configurado.

    Para usar a nova configuração, defina associações explícitas (links) de um grupo de limites para outro. Configure todos os pontos de distribuição nesse grupo associado com o mesmo tempo em minutos. Quando um cliente não consegue encontrar uma fonte de conteúdo de seu grupo de limites *atual*, o tempo configurado determina quando ele começa a pesquisar as fontes de conteúdo de seu grupo de limites vizinho.

    Além dos grupos de limites configurados explicitamente, cada grupo de limite tem um link implícito para o grupo de limites de site padrão. Esse link se torna ativo após 120 minutos. Em seguida, o grupo de limites do site padrão torna-se um grupo de limites vizinho. Esse comportamento permite que os clientes usem como locais de fonte de conteúdo os pontos de distribuição associados a esse grupo de limites.

    Esse comportamento substitui o que anteriormente era chamado de fallback de conteúdo. Substitua esse comportamento padrão de 120 minutos associando explicitamente o grupo de limites do site padrão a um grupo *atual*. Defina um tempo específico em minutos ou bloqueie o fallback por completo para impedir seu uso.


-   Os clientes tentam obter o conteúdo de cada ponto de distribuição por até dois minutos: quando um cliente pesquisa um local de fonte de conteúdo, ele tenta acessar cada ponto de distribuição por dois minutos antes de tentar outro ponto de distribuição. Esse comportamento é uma alteração de versões anteriores em que os clientes tentavam se conectar a um ponto de distribuição por até duas horas.

    - Os clientes selecionam aleatoriamente o primeiro ponto de distribuição do pool de servidores disponíveis nos grupos de limites *atuais* do cliente.

    - Após dois minutos, se o cliente não encontrou o conteúdo, ele muda para um novo ponto de distribuição e tenta obter o conteúdo daquele servidor. Esse processo se repete a cada dois minutos até que o cliente localize o conteúdo ou atinja o último servidor em seu pool.

    - Se um cliente não consegue encontrar um local de fonte de conteúdo válido em seu pool *atual* antes de atingir o período de fallback para um grupo de limites *vizinho*, o cliente adiciona os pontos de distribuição desse grupo *vizinho* ao fim de sua lista atual. Ele então pesquisa o grupo expandido de locais de origem que inclui os pontos de distribuição de ambos os grupos de limites.

        > [!TIP]  
        > Quando você cria um link explícito do grupo de limites atual para o grupo de limites do site padrão e define um tempo de fallback inferior ao tempo de fallback de um link para um grupo de limites vizinho, os clientes começam a pesquisar os locais de origem do grupo de limites do site padrão antes de incluir o grupo vizinho.

    - Quando o cliente falha em obter o conteúdo do último servidor no pool, ele inicia o processo novamente.


## <a name="procedures-for-boundary-groups"></a>Procedimentos para grupos de limites

### <a name="to-create-a-boundary-group"></a>Para criar um grupo de limites  
1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** >  **Grupos de Limites**.  

2.  Na guia **Início** , no grupo **Criar** , clique em **Criar Grupo de Limites**.  

3.  Na caixa de diálogo **Criar Grupo de Limites**, selecione a guia **Geral** e especifique um **Nome** para esse grupo de limites.  

4.  Clique em **OK** para salvar o novo grupo de limites.  


### <a name="to-configure-a-boundary-group"></a>Para configurar um grupo de limites  
 1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** >  **Grupos de Limites**.  

 2.  Selecione o grupo de limites que você deseja modificar.  

 3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

 4.  Na caixa de diálogo **Propriedades** para o grupo de limites, selecione a guia **Geral** para modificar os limites que são membros desse grupo de limites:  

     -   Para adicionar limites, clique em **Adicionar**, marque a caixa de seleção para um ou mais limites e clique em **OK**.  

     -   Para remover limites, selecione o limite e clique em **Remover**.  

 5.  Selecione a guia **Referências** para modificar a atribuição de site e a configuração do servidor do sistema de sites associado:  

     -   Para habilitar esse grupo de limites para uso pelos clientes para atribuição de site, selecione **Usar este grupo de limites para a atribuição de site**. Em seguida, selecione um site na lista suspensa **Site atribuído**.  

     -   Para configurar quais servidores do sistema de sites disponíveis estão associados a este grupo de limites:  

     1.  Clique em **Adicionar**e marque a caixa de seleção para um ou mais servidores. Os servidores são adicionados como servidores do sistema de sites associados a este grupo de limite. Somente os servidores que têm suporte para a função do sistema de sites instalada neles estão disponíveis.  

         > [!NOTE]  
         >  É possível selecionar qualquer combinação de sistemas de sites disponíveis de qualquer site na hierarquia. Os sistemas de site selecionados são listados na guia **Sistemas de Site** nas propriedades de cada limite membro desse grupo de limites.  

     2.  Para remover um servidor deste grupo de limites, selecione o servidor e clique em **Remover**.  

         > [!NOTE]  
         >  Para interromper o uso desse grupo de limites para a associação de sistemas de sites, remova todos os servidores listados como servidores do sistema de sites associados.  

 6.  Para configurar o comportamento de fallback, selecione a guia **Relações**:  

     - Clique em **Adicionar** e selecione o grupo de limites que deseja configurar.

     - Defina um tempo de fallback para os pontos de distribuição. Após esse período, os clientes no grupo de limites para o qual você está configurando os relacionamentos poderão começar a pesquisar conteúdo dos pontos de distribuição do grupo de limites sendo adicionado.

     - Para evitar o fallback em um grupo de limites específico, incluindo o *grupo de limites do site padrão* configurado por padrão, selecione o grupo de limites e, em seguida, marque a caixa **Nunca fazer fallback**.   

 7.  Clique em **OK** para fechar as propriedades do grupo de limites e salvar a configuração.  

#### <a name="to-associate-a-site-system-server-with-a-boundary-group"></a>Para associar um servidor do sistema de sites a um grupo de limites  
 1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** >  **Grupos de Limites**.  

 2.  Selecione o grupo de limites que você deseja modificar.  

 3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

 4.  Na caixa de diálogo **Propriedades** para o grupo de limites, selecione a guia **Referências** .  

 5.  Em **Selecionar servidores do sistema de sites**, clique em **Adicionar**. Selecione os servidores do sistema de sites a serem associados a esse grupo de limites e, em seguida, clique em **OK**.  

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
