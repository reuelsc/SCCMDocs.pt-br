---
title: Configurar grupos de limites
titleSuffix: Configuration Manager
description: Ajude os clientes a encontrar os sistemas de sites usando grupos de limites para organizar logicamente os locais de rede relacionados chamados limites
ms.date: 06/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 716b36060f4fdc768f98e4cc22be1653a967246c
ms.sourcegitcommit: 60d45a5df135b84146f6cfea2bac7fd4921d0469
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67194257"
---
# <a name="configure-boundary-groups-for-configuration-manager"></a>Configurar grupos de limites para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use grupos de limites no Configuration Manager para organizar logicamente os locais de rede ([limites](/sccm/core/servers/deploy/configure/boundaries)) relacionados a fim de facilitar o gerenciamento da infraestrutura. Atribua limites a grupos de limites antes de usar o grupo de limites.

Por padrão, o Configuration Manager cria um grupo de limites de site padrão em cada site.

Para configurar grupos de limites, associe limites (locais de rede) e funções do sistema de sites, como pontos de distribuição, ao grupo de limites. Essa configuração ajuda a associar os clientes aos servidores do sistema de sites como pontos de distribuição que estão localizados próximo aos clientes na rede.

Para aumentar a disponibilidade dos servidores para uma gama mais ampla de locais de rede, atribua o mesmo limite e o mesmo servidor a mais de um grupo de limites.

Os clientes usam grupos de limites para:  

- Atribuição automática de site  
- Para localizar um servidor de sistema de sites que pode fornecer um serviço, incluindo:  
    - Pontos de distribuição para o local do conteúdo  
    - Pontos de atualização de software  
    - Pontos de migração de estado  
    - Pontos de gerenciamento preferenciais  
    - Gateway de gerenciamento de nuvem (a partir da versão 1902)

        > [!Note]  
        > Se você usar pontos de gerenciamento preferenciais, habilite essa opção para a hierarquia, e não de dentro da configuração do grupo de limites. Saiba mais em [Habilitar o uso de pontos de gerenciamento preferenciais](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_proc-prefer).  


## <a name="boundary-groups-and-relationships"></a>Grupos de limites e relações

Para cada grupo de limites na sua hierarquia, você pode atribuir:

- Um ou mais limites. O grupo de limites **atual** de um cliente é um local de rede definido como um limite atribuído a um grupo de limites específico. Um cliente pode ter mais de um grupo de limites atual.  

- Uma ou mais funções do sistema de sites. Os clientes podem sempre usar funções associados ao atual grupo de limites. Dependendo das configurações adicionais, eles podem usar as funções nos grupos de limites adicionais.  

Para cada grupo de limites que você criar, você pode configurar um link unidirecional para outro grupo de limites. O link é chamado de uma **relação**. Os grupos de limites aos quais você vincula são chamados de grupos de limites **vizinhos**. Um grupo de limites pode ter várias relações, cada uma com um grupo de limites vizinho específico.

Quando um cliente não consegue encontrar um sistema de sites disponível em seu grupo de limites atual, a configuração de cada relação determina quando começar a pesquisar um grupo de limites vizinho. Essa pesquisa de grupos adicionais é chamada de **fallback**.

Para saber mais, confira os procedimentos a seguir:  

- [Criar um grupo de limites](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_create)  
- [Configurar um grupo de limites](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_config)  


## <a name="fallback"></a>Fallback

Para evitar problemas quando os clientes não conseguem encontrar um sistema de sites disponível em seu grupo de limites atual, defina a relação entre grupos de limites para o comportamento de fallback. O fallback permite que um cliente expanda sua pesquisa para grupos de limites adicionais para localizar um sistema de sites disponível.

As relações são configuradas na guia **Relações** das propriedades do grupo de limites. Quando você configura uma relação, define um link para um grupo de limites vizinho. Para cada tipo de função do sistema de sites compatível, defina configurações independentes para o fallback nesse grupo de limites vizinho. Para saber mais, confira [Configurar o comportamento de fallback](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_bg-fallback).

Por exemplo, quando você configura uma relação com um grupo de limites específico, defina o fallback para os pontos de distribuição para que ele ocorra após 20 minutos. O padrão é de 120 minutos. Para obter um exemplo mais abrangente, confira [Exemplo de como usar grupos de limites](#example-of-using-boundary-groups).

Se um cliente não conseguir encontrar uma função do sistema de sites disponível em seu grupo de limites atual, o cliente usará o tempo de fallback em minutos. O tempo de fallback determina quando o cliente começa a pesquisar um sistema de sites disponível associado ao grupo de limites vizinho.  

Quando um cliente não consegue encontrar um sistema de sites disponível, ele começa a pesquisar os locais nos grupos de limites vizinhos. Esse comportamento aumenta o pool de sistemas de sites disponíveis. A configuração de grupos de limites e suas relações define o uso do cliente desse pool de sistemas de sites disponíveis.

- Um grupo de limites pode ter mais de uma relação. Com essa configuração, você pode configurar o fallback de cada tipo de sistema de sites em vizinhos diferentes para que ele ocorra após períodos diferentes.  

- Os clientes só executam o fallback em um grupo de limites que seja vizinho direto de seu grupo de limites atual.  

- Quando um cliente for membro de mais de um grupo de limites, ele definirá o grupo de limite atual como uma união de todos os seus grupos de limites. O cliente pode fazer fallback nos vizinhos de um desses grupos de limites originais.  

### <a name="the-default-site-boundary-group"></a>O grupo de limite do site padrão

Você pode criar seus próprios grupos de limites e cada site tem um grupo de limites de site padrão que o Configuration Manager cria. Esse grupo é denominado **Default-Site-Boundary-Group&lt;sitecode>** . Por exemplo, o grupo para o site ABC seria nomeado **Default-Site-Boundary-Group&lt;ABC>** .

Para cada grupo de limites que você criar, o Configuration Manager criará automaticamente um link implícito para cada grupo de limites de site padrão na hierarquia.  

- O link implícito é uma opção de fallback padrão de um grupo de limites atual para o grupo de limites padrão de sites. O tempo de fallback padrão é de 120 minutos.  

- Para os clientes que não estão em um limite associado a nenhum grupo de limites: para identificar funções do sistema de sites válidas, use o grupo de limites do site padrão de seu site atribuído.  

Para gerenciar o fallback para o grupo de limites do site padrão:  

- Abra as propriedades do grupo de limites do site padrão e altere os valores na guia **Comportamento Padrão**. As alterações feitas aqui se aplicam a *todos* os links implícitos para esse grupo de limites. Ao configurar um link explícito para esse grupo de limites de site padrão de outro grupo de limites, você substitui as configurações padrão.  

- Abra as propriedades de um grupo de limites personalizado. Altere os valores do link explícito para um grupo de limites do site padrão. Quando você define um novo tempo em minutos para realizar ou bloquear o fallback, essa alteração afeta somente o link que você está configurando. A configuração do link explícito substitui as configurações da guia **Comportamento Padrão** do grupo de limites do site padrão.  


## <a name="site-assignment"></a>Atribuição de site  

É possível configurar cada grupo de limites com um site atribuído para clientes.  

- Um cliente recém-instalado que usa a atribuição automática de site ingressa no site atribuído de um grupo de limites que contém o local de rede atual do cliente.  

- Depois de atribuir a um site, um cliente não altera a atribuição de site quando altera o local de rede. Por exemplo, um cliente passa para um novo local de rede. Esse local é um limite em um grupo de limites com uma atribuição de site diferente. O site atribuído do cliente não muda.  

- Quando a Descoberta de Sistemas do Active Directory encontra um novo recurso, o site avalia as informações de rede para o recurso com base nos limites em grupos de limites. Esse processo associa o novo recurso a um site atribuído para uso do método de instalação do cliente por push.  

- Quando um limite é membro de vários grupos de limites que têm diferentes locais atribuídos, os clientes selecionarão aleatoriamente um desses sites.  

- As alterações em um site atribuído de grupos de limite só se aplicam a novas ações de atribuição de site. Os clientes atribuídos anteriormente a um site não reavaliam sua atribuição de site com base nas alterações da configuração de um grupo de limites (ou de seu próprio local de rede).  

Para saber mais sobre a atribuição de site do cliente, confira [Usar a atribuição automática de site para computadores](/sccm/core/clients/deploy/assign-clients-to-a-site#BKMK_AutomaticAssignment).  

Saiba mais sobre como configurar a atribuição de site nos procedimentos a seguir:

- [Configurar a atribuição de site e selecionar servidores do sistema de site](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_references)
- [Configurar um local de fallback para atribuição automática de site](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_site-fallback)


## <a name="distribution-points"></a>Pontos de distribuição

Quando um cliente solicita o local de um ponto de distribuição, o Configuration Manager envia ao cliente uma lista de sistemas de sites. Esses sistemas de sites são do tipo apropriado associado a cada grupo de limites que inclui a localização de rede atual dos clientes:

- **Durante a distribuição de software**, os clientes solicitam um local para implantação de conteúdo em uma fonte de conteúdo válida. Esse local pode ser um ponto de distribuição, ou uma fonte de cache par.  

- **Durante a implantação do sistema operacional**, os clientes solicitam um local para enviar ou receber suas informações de migração de estado.  

    - Começando na versão 1810, os clientes adquirem conteúdo com base em comportamentos do grupo de limites. Para obter mais informações, confira [Suporte de sequência de tarefas para grupos de limites](#bkmk_bgr-osd).  

Durante a implantação de conteúdo, se um cliente solicita um conteúdo que não está disponível em uma origem em seu grupo de limites atual, o cliente continua solicitando esse conteúdo. O cliente tenta diferentes fontes de conteúdo em seu grupo de limites atual até atingir o período de fallback para um vizinho ou o grupo de limites de site padrão. Se o cliente ainda não tiver encontrado o conteúdo, expandirá a pesquisa de fontes de conteúdo para incluir os grupos de limites vizinhos.

Se você configurar o conteúdo a distribuir sob demanda e ele não estiver disponível em um ponto de distribuição quando um cliente o solicita, o site começará a transferir o conteúdo ao ponto de distribuição. É possível que o cliente encontre o servidor como uma fonte de conteúdo antes de fazer fallback para usar um grupo de limites vizinho.

### <a name="bkmk_ccmsetup"></a> Instalação do cliente

<!--1358840-->
Ao instalar o cliente do Configuration Manager, o processo ccmsetup contata o ponto de gerenciamento para localizar o conteúdo necessário. Durante esse processo nas versões 1806 e anteriores, o ponto de gerenciamento retorna apenas os pontos de distribuição no grupo de limites atual do cliente. Se nenhum conteúdo estiver disponível, o processo de instalação regredirá para baixar o conteúdo do ponto de gerenciamento. Não há nenhuma opção de regredir para os pontos de distribuição em outros grupos de limites que podem ter o conteúdo necessário.

Da versão 1810 em diante, o ponto de gerenciamento retorna pontos de distribuição com base na configuração do grupo de limites. Se você definir relações no grupo de limites, o ponto de gerenciamento retornará pontos de distribuição na seguinte ordem:

1. Grupo de limites atual  
2. Grupo de limites vizinho  
3. O grupo de limites padrão do site  

> [!Note]  
> O processo de instalação do cliente não usa o tempo de fallback. Para localizar o conteúdo o mais rápido possível, ele regride imediatamente para o próximo grupo de limites.  

### <a name="bkmk_bgr-osd"></a> Suporte a sequência de tarefas para grupos de limites

<!--1359025-->
Da versão 1810 em diante, quando um dispositivo executa uma sequência de tarefas e precisa adquirir conteúdo, ele agora usa comportamentos de grupo de limites semelhantes ao cliente do Configuration Manager.

Configure esse comportamento usando as configurações a seguir na página **Pontos de Distribuição** da implantação da sequência de tarefas:

- **Quando não houver nenhum ponto de distribuição local disponível, use um ponto de distribuição remoto**: para essa implantação, a sequência de tarefas pode fazer fallback para pontos de distribuição em um grupo de limites vizinho.  

- **Permitir que os clientes usem pontos de distribuição do grupo de limites de site padrão**: para essa implantação, a sequência de tarefas pode fazer fallback para pontos de distribuição em um grupo de limites do site padrão.  

Para usar esse novo comportamento, certifique-se de atualizar os clientes para a versão mais recente.

#### <a name="location-priority"></a>Prioridade da localização  

A sequência de tarefas tenta adquirir conteúdo na seguinte ordem:  

1. Fontes de cache par  

2. Pontos de distribuição no grupo de limites *atual*  

3. Pontos de distribuição no grupo de limites *vizinho*  

    > [!Important]  
    > Devido à natureza em tempo real do processamento da sequência de tarefas, ela não aguarda o tempo de failover em um grupo de limites vizinho. Ela usa os tempos de failover para priorizar os grupos de limites vizinhos. Por exemplo, se a sequência de tarefas falhar em adquirir conteúdo de um ponto de distribuição em seu grupo de limites atual, ela tentará imediatamente um ponto de distribuição em um grupo de limites vizinhos com o menor tempo de failover. Se esse processo falhar, então ele fará failover para um ponto de distribuição em um grupo de limites vizinho com um maior tempo de failover.  

4. Pontos de distribuição no grupo de limites de *padrão do site*  

O arquivo de log **smsts.log** da sequência de tarefas mostra a prioridade das fontes de localização que ele usa com base nas propriedades da implantação.

### <a name="bkmk_bgoptions"></a> Opções de grupo de limites para downloads de pares

<!--1356193-->
A partir da versão 1806, os grupos de limites incluem as seguintes configurações adicionais para dar a você mais controle sobre a distribuição de conteúdo em seu ambiente:  

- [Permitir downloads de par neste grupo de limites](#bkmk_bgoptions1)  

- [Durante os downloads de pares, use apenas pares na mesma sub-rede](#bkmk_bgoptions2)  

<!--1358749-->
A versão 1810 adiciona as seguintes opções:  

- [Preferir pontos de distribuição a de pares na mesma sub-rede](#bkmk_bgoptions3)  

- [Preferir a pontos de distribuição em nuvem a pontos de distribuição](#bkmk_bgoptions4)  

Para obter mais informações sobre como definir essas configurações, confira [Configurar um grupo de limites](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_config).

#### <a name="bkmk_bgoptions1"></a> Permitir downloads de par neste grupo de limites

Essa configuração é habilitada por padrão. O ponto de gerenciamento fornece aos clientes uma lista de locais de conteúdo que inclui fontes de pares. Essa configuração também afeta a aplicação de IDs de grupo para [Otimização de Entrega](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization).  

Há dois cenários comuns em que você deve considerar a desabilitação dessa opção:  

- Se você tiver um grupo de limites que inclua limites de locais geograficamente dispersos, como uma VPN. Dois clientes podem estar no mesmo grupo de limites, pois estão conectados por meio de VPN, mas em locais muito diferentes que são inadequados para o compartilhamento de conteúdo de pares.  

- Se você usar um grupo de limites único e grande para a atribuição de site que não faça referência a nenhum ponto de distribuição.  

#### <a name="bkmk_bgoptions2"></a> Durante os downloads de pares, use apenas pares na mesma sub-rede

Essa configuração depende da opção anterior. Se você habilitar essa opção, o ponto de gerenciamento incluirá apenas as origens de pares de lista do local do conteúdo que estão na mesma sub-rede que o cliente.

Cenários comuns para habilitar essa opção:

- O design de grupo de limites para distribuição de conteúdo inclui um grupo de limites grandes que se sobrepõe a outros grupos de limites menores. Com essa nova configuração, a lista de fontes de conteúdo que o ponto de gerenciamento fornece aos clientes inclui apenas as fontes de pares da mesma sub-rede.

- Você tem um grupo de limites grande e único para todos os locais remotos. Habilite esta opção e os clientes só compartilharão conteúdo dentro da sub-rede no local remoto, em vez de colocar em risco o compartilhamento de conteúdo entre os locais.

#### <a name="bkmk_bgoptions3"></a> Preferir pontos de distribuição a de pares na mesma sub-rede

Por padrão, o ponto de gerenciamento prioriza as fontes de cache par na parte superior da lista de locais de conteúdo. Essa configuração reverte essa prioridade para clientes que estão na mesma sub-rede que a fonte de cache par.  

#### <a name="bkmk_bgoptions4"></a> Preferir a pontos de distribuição em nuvem a pontos de distribuição

Se você tiver uma filial com um link da Internet mais rápido, poderá priorizar o conteúdo de nuvem.  

Na versão 1902, essa configuração agora é intitulada **Prefira fontes na nuvem em vez de fontes locais**. O comportamento permanece o mesmo.<!-- SCCMDocs#1529 -->


## <a name="software-update-points"></a>Pontos de atualização de software

Os clientes usam grupos de limites para encontrar um novo ponto de atualização de software. Para controlar quais servidores um cliente pode encontrar, adicione pontos de atualização de software individuais a grupos de limites diferentes.

Se você atualizar de uma versão anterior à 1702, cada site adicionará todos os pontos de atualização de software existentes ao grupo de limites do site padrão. Esse comportamento de atualização do site mantém o comportamento anterior do cliente para selecionar um ponto de atualização de software no pool de servidores disponíveis. Esse comportamento é mantido até que você escolha adicionar pontos de atualização de software individuais a grupos de limites diferentes para seleção controlada e comportamento de fallback.

Se você instalar um novo site, os pontos de atualização de software não serão adicionados ao grupo de limites do site padrão. Atribua pontos de atualização de software a um grupo de limites para que os clientes possam localizar e usá-los.

### <a name="fallback-for-software-update-points"></a>Fallback para pontos de atualização de software

O fallback para pontos de atualização de software é configurado como outras funções de sistema de site, mas tem as seguintes ressalvas:  

#### <a name="new-clients-use-boundary-groups-to-select-software-update-points"></a>Os novos clientes usam os grupos de limites para selecionar pontos de atualização de software

Ao instalar novos clientes, ele selecionam um ponto de atualização de software dos servidores associados aos grupos de limites configurados. Esse comportamento substitui o comportamento anterior, em que os clientes selecionam um ponto de atualização de software aleatoriamente de uma lista dos servidores que compartilham a floresta do cliente.

#### <a name="clients-continue-to-use-a-last-known-good-software-update-point-until-they-fallback-to-find-a-new-one"></a>Os clientes continuam a usar um último ponto de atualização de software válido até fazerem fallback para localizar um novo

Os clientes que já têm um ponto de atualização de software continuam usando-o até que ele não possa ser acessado. Esse comportamento inclui o uso contínuo de um ponto de atualização de software que não está associado ao grupo de limites atual do cliente.

Esse comportamento é intencional. O cliente continua usando um ponto de atualização de software existente, mesmo quando o servidor não está no grupo de limites atual do cliente. Quando o ponto de atualização de software é alterado, o cliente sincroniza os dados com o novo servidor, o que gera um uso de rede significativo. Se todos os clientes alternam para um novo servidor ao mesmo tempo, o atraso na transição ajuda a evitar a saturação da rede.

#### <a name="a-client-always-tries-to-reach-its-last-known-good-software-update-point-for-120-minutes-before-starting-fallback"></a>Um cliente sempre tenta acessar seu último ponto de atualização de software válido por 120 minutos antes de iniciar o fallback

Depois de 120 minutos, se o cliente não tiver estabelecido contato, ele começará o fallback. Quando o fallback começa, o cliente recebe uma lista com todos os pontos de atualização de software em seu grupo de limites atual. Pontos de atualização de software adicionais em grupos de limites vizinhos e do site padrão estão disponíveis com base nas configurações de fallback.

### <a name="fallback-configurations-for-software-update-points"></a>Configurações de fallback para pontos de atualização de software

Você pode configurar **Tempos de Fallback (em minutos)** para pontos de atualização de software como menos de 120 minutos. No entanto, o cliente ainda tenta atingir seu ponto de atualização de software original de 120 minutos. Em seguida, ele expande sua pesquisa para outros servidores. Os tempos de fallback do grupo de limites começam quando o cliente não consegue acessar primeiro seu servidor original. Quando o cliente expande sua pesquisa, o site fornece os grupos de limites configurados com menos de 120 minutos.

Para bloquear o fallback de um ponto de atualização de software em um grupo de limites vizinho, defina a configuração para **Nunca fazer fallback**.

Após não conseguir acessar o servidor original durante duas horas, o cliente usa um ciclo mais curto para estabelecer uma conexão com um novo ponto de atualização de software. Esse comportamento permite que o cliente pesquise rapidamente a lista cada vez maior de pontos de atualização de software potenciais.

#### <a name="example"></a>Exemplo

Configure os pontos de atualização de software no grupo de limites *A* para fallback após **10** minutos. Defina a mesma configuração para o grupo de limites *B* como **130** minutos. Um cliente no grupo de limite *Z* não consegue acessar seu último ponto de atualização de software válido.

- Nos próximos 120 minutos, o cliente tentará acessar somente o servidor original no grupo de limites Z. Após 10 minutos, o Configuration Manager adicionará os pontos de atualização de software do grupo de limites A para o pool de servidores disponíveis. No entanto, o cliente não tentará entrar em contato com eles ou com qualquer outro servidor até que o período inicial de 120 minutos tenha passado.  

- Depois de tentar contatar o ponto de atualização de software original por 120 minutos, o cliente expandirá sua pesquisa. Ele adiciona servidores ao pool disponível de pontos de atualização de software que estão em seu grupo de limites atual e em grupos de limites vizinhos configurados com 120 minutos ou menos. Esse pool inclui os servidores no grupo de limites A, que foram adicionados anteriormente ao pool de servidores disponíveis.  

- Após mais 10 minutos, o cliente expande a pesquisa a fim de incluir os pontos de atualização de software do grupo de limites B. Esse período é de 130 minutos no total após a primeira falha do cliente em acessar seu último ponto de atualização de software válido.  

### <a name="manually-switch-to-a-new-software-update-point"></a>Mudar manualmente para um novo ponto de atualização de software

Além do fallback, use a notificação do cliente para forçar manualmente um dispositivo a alternar para um novo ponto de atualização de software.

Quando você alternar para um novo servidor, os dispositivos usam fallback para localizar esse novo servidor. Os clientes mudam para o novo ponto de atualização de software durante seu próximo ciclo de verificação de atualizações de software.<!-- SCCMDocs#1537 -->

Examine as configurações do grupo de limites. Antes de começar essa alteração, verifique se os pontos de atualização de software estão nos grupos de limites corretos.

Para saber mais, confira [Mudar manualmente clientes para um novo ponto de atualização de software](/sccm/sum/plan-design/plan-for-software-updates#BKMK_ManuallySwitchSUPs).


## <a name="management-points"></a>Pontos de gerenciamento

<!-- 1324594 -->
A partir da versão 1802, configure relações de fallback para os pontos de gerenciamento entre grupos de limites. Esse comportamento proporciona maior controle para os pontos de gerenciamento que os clientes usam. Na guia **Relações** das propriedades do grupo de limites, há uma coluna para o ponto de gerenciamento. Quando você adiciona um novo grupo de limites de fallback, o tempo de fallback para o ponto de gerenciamento é sempre zero (0). Esse comportamento é o mesmo para o **Comportamento padrão** no grupo de limites padrão do site.

Anteriormente, um problema comum ocorre quando você possui um ponto de gerenciamento protegido em uma rede segura. Os clientes da rede corporativa principal recebem políticas que incluem esse ponto de gerenciamento protegido, mesmo que não possam se comunicar com ele em um firewall. Para solucionar esse problema, use a opção **Nunca realizar fallback** para garantir que os clientes apenas retornem aos pontos de gerenciamento com os quais eles podem se comunicar.

Ao atualizar o site para a versão 1802, o Configuration Manager adiciona todos os pontos de gerenciamento de intranet ao grupo de limites padrão do site. Esse grupo de servidores não inclui os pontos de gerenciamento voltados apenas para a internet. Esse comportamento de upgrade garante que as versões mais antigas do cliente continuem a se comunicar com pontos de gerenciamento. Para aproveitar ao máximo esse recurso, mova seus pontos de gerenciamento para os grupos de limites desejados.

> [!Note]  
> Se você habilitar pontos de distribuição no grupo de limites do site padrão para fallback, e um ponto de gerenciamento for colocado em um ponto de distribuição, o site também adiciona o ponto de gerenciamento para o grupo de limites do site padrão.<!--VSO 2841292-->  

Se um cliente estiver em um grupo de limites sem um ponto de gerenciamento atribuído, o site dará ao cliente toda a lista de pontos de gerenciamento. Esse comportamento garante que um cliente sempre receba uma lista de pontos de gerenciamento.

O fallback do grupo de limites do ponto de gerenciamento não altera o comportamento durante a instalação do cliente (ccmsetup.exe). Se a linha de comando não especificar o ponto de gerenciamento inicial usando o parâmetro /MP, o novo cliente recebe a lista completa de pontos de gerenciamento disponíveis. Para o processo inicial de inicialização, o cliente usa o primeiro ponto de gerenciamento que ele pode acessar. Uma vez que o cliente estiver registrado no site, ele recebe a lista de pontos de gerenciamento ordenada corretamente com esse novo comportamento.

Para obter mais informações sobre o comportamento do cliente para adquirir conteúdo durante a instalação, confira [Instalação do cliente](#bkmk_ccmsetup).

Durante a atualização do cliente, se você não especificar o parâmetro de linha de comando /MP, o cliente consultará fontes como o Active Directory e o WMI em busca de qualquer ponto de gerenciamento disponível. A atualização do cliente não respeita a configuração do grupo de limites. <!--VSO 2841292-->  

Para usar essa opção, habilite a configuração: **Os clientes preferem usar os pontos de gerenciamento especificados em grupos de limites** em **Configurações da Hierarquia**.

> [!Note]  
> Processos de implantação de sistema operacional não estão cientes dos grupos de limites para pontos de gerenciamento.  

### <a name="troubleshooting"></a>Solução de problemas

Novas entradas aparecem no **LocationServices.log**. O atributo **Localidade** identifica um dos seguintes estados:

- **0**: Desconhecida  

- **1**: O ponto de gerenciamento especificado é somente no grupo de limites padrão do site de fallback  

- **2**: O ponto de gerenciamento especificado está em um grupo de limites remoto ou vizinho. Quando o ponto de gerenciamento está em um grupo vizinho ou em grupos de limites padrão do site, a localidade é 2.  

- **3**: O ponto de gerenciamento especificado está no grupo de limites local ou atual. Quando o ponto de gerenciamento está no grupo de limites atual, bem como em um grupo vizinho ou no grupo de limites padrão do site, a localidade é 3. Se você não habilitar a configuração de pontos de gerenciamento preferenciais nas Configurações de Hierarquia, a localidade será sempre 3, independentemente do grupo de limites em que o ponto de gerenciamento esteja.  

Os clientes usam os pontos de gerenciamento local primeiro (localidade 3), em seguida os remotos (localidade 2) e depois os fallbacks (localidade 1).

Quando um cliente recebe cinco erros em 10 minutos e não se comunica com um ponto de gerenciamento em seu grupo de limites atual, ele tenta contatar um ponto de gerenciamento em um grupo de limites vizinho ou no grupo de limites padrão do site. Se o ponto de gerenciamento no atual grupo de limites voltar a ficar online mais tarde, o cliente retornará ao ponto de gerenciamento local no próximo ciclo de atualização. O ciclo de atualização é de 24 horas, ou quando o serviço do agente do Configuration Manager é reiniciado.


## <a name="bkmk_preferred"></a> Pontos de gerenciamento preferenciais

> [!Note]
> O comportamento dessa configuração da hierarquia, **Os clientes preferem usar os pontos de gerenciamento especificados nos grupos de limites**, é alterado a partir da versão 1802. Quando você habilita essa configuração, o Configuration Manager usa a funcionalidade do grupo de limites para o ponto de gerenciamento atribuído. Para obter mais informações, consulte [Pontos de gerenciamento](#management-points).

Os pontos de gerenciamento preferenciais permitem que um cliente identifique um ponto de gerenciamento associado ao local de rede (limite) atual.  

- Um cliente tenta usar um ponto de gerenciamento preferencial de seu site atribuído antes de usar um não configurado como preferencial de seu site atribuído.  

- Para usar essa opção, habilite a configuração **Os clientes preferem usar os pontos de gerenciamento especificados em grupos de limites** em **Configurações da Hierarquia**. Em seguida, configure grupos de limites em sites primários individuais. Inclua os pontos de gerenciamento que devem ser associados aos limites associados do grupo de limites. Saiba mais em [Habilitar o uso de pontos de gerenciamento preferenciais](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_proc-prefer).  

- Quando você configura os pontos de gerenciamento preferenciais e um cliente organiza sua lista de pontos de gerenciamento, o cliente coloca os pontos de gerenciamento preferenciais no início da lista. Essa lista inclui todos os pontos de gerenciamento do site atribuído do cliente.  

> [!NOTE]  
> Roaming do cliente significa que ele altera seus locais de rede. Por exemplo, quando um laptop passa para um local de escritório remoto. Quando um cliente usa um perfil móvel, ele pode usar um ponto de gerenciamento do site local antes de tentar usar um servidor de seu site atribuído. Essa lista de servidores de seu site atribuído inclui os pontos de gerenciamento preferenciais. Para obter mais informações, consulte [Entender como os clientes encontram serviços e recursos do site](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services).  


## <a name="overlapping-boundaries"></a>Sobreposição de limites  

O Configuration Manager dá suporte à sobreposição de configurações de limite para o local do conteúdo. Quando o local de rede do cliente pertence a mais de um grupos de limites:

- Quando um cliente solicita o conteúdo, o Configuration Manager envia ao cliente uma lista de todos os pontos de distribuição que têm o conteúdo.  

- Quando um cliente solicita a um servidor o envio ou recebimento de suas informações de migração de estado, o Configuration Manager envia ao cliente uma lista de todos os pontos de migração de estado associados a um grupo de limites que inclui o local de rede atual do cliente.  

Esse comportamento permite que o cliente selecione o servidor mais próximo do qual transferir o conteúdo ou as informações de migração de estado.  


## <a name="example-of-using-boundary-groups"></a>Exemplo de como usar grupos de limites

O exemplo a seguir usa uma pesquisa de cliente por conteúdo de um ponto de distribuição. Este exemplo pode ser aplicado para outras funções de sistema de site que usam grupos de limites.

Crie três grupos de limites que não compartilham limites ou servidores de sistemas de sites:  

- Grupo BG_A com os pontos de distribuição DP_A1 e DP_A2  

- Grupo BG_B com os pontos de distribuição DP_B1 e DP_B2  

- Grupo BG_C com os pontos de distribuição DP_C1 e DP_C2  

Adicione os locais de rede dos clientes como limites somente ao grupo de limites BG_A. Em seguida, configure as relações desse grupo de limites com os outros dois grupos de limites:  

- Configure os pontos de distribuição para o primeiro grupo *vizinho* (BG_B) a ser usado após 10 minutos. Esse grupo contém os pontos de distribuição DP_B1 e DP_B2. Ambos estão bem conectados aos primeiros locais de limite dos grupos.  

- Configure o segundo grupo *vizinho* (BG_C) a ser usado após 20 minutos. Esse grupo contém os pontos de distribuição DP_C1 e DP_C2. Ambos estão em uma WAN dos outros dois grupos de limites.  

- Adicione também ao grupo de limites do site padrão outro ponto de distribuição localizado no servidor do site. Esse servidor é o local de fonte de conteúdo de menor preferência, mas está localizado centralmente para todos os grupos de limites.

    Exemplo de grupos de limites e tempos de fallback:

    ![Exemplo de grupos de limites e tempos de fallback](media/BG_Fallback.png)  

Com essa configuração:  

- O cliente começa a pesquisar o conteúdo nos pontos de distribuição em seu grupo de limites *atual* (BG_A). Ele pesquisa cada ponto de distribuição por dois minutos e, em seguida, alterna para o próximo ponto de distribuição no grupo de limites. O pool de clientes dos locais de fonte de conteúdo válidos incluem o DP_A1 e o DP_A2.  

- Se o cliente não conseguir localizar o conteúdo de seu grupo de limites *atual* depois de pesquisar por 10 minutos, ele adicionará os pontos de distribuição do grupo de limites BG_B à sua pesquisa. Ele então continua pesquisando o conteúdo de um ponto de distribuição em seu pool combinado de servidores. Esse pool agora inclui servidores dos grupos de limites BG_A e BG_B. O cliente continua acessando cada ponto de distribuição por dois minutos e, em seguida, alterna para o próximo servidor em seu pool. O pool de clientes dos locais de fonte de conteúdo válidos incluem DP_A1, DP_A2, DP_B1 e DP_B2.  

- Depois de mais 10 minutos (total de 20 minutos), se o cliente ainda não encontra um ponto de distribuição com o conteúdo, ele expande seu pool para incluir os servidores disponíveis do segundo grupo *vizinho*, o grupo de limites BG_C. O cliente agora tem seis pontos de distribuição para pesquisar: DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 e DP_C2. Ele continua mudando para um novo ponto de distribuição a cada dois minutos até encontrar o conteúdo.  

- Se o cliente não tiver encontrado conteúdo depois de um total de 120 minutos, ele realizará o fallback para incluir o *grupo de limites de site padrão* como parte de sua pesquisa contínua. Agora o pool inclui todos os pontos de distribuição dos três grupos de limites configurados e o ponto de distribuição final localizado no servidor do site. O cliente continua, então, a pesquisa do conteúdo, alterando os pontos de distribuição a cada dois minutos até que o conteúdo seja encontrado.  

Ao configurar os grupos vizinhos diferentes para estarem disponíveis em horários diferentes, controle quando pontos de distribuição específicos são adicionados como um local de fonte de conteúdo. O cliente usa o fallback para o grupo de limites do site padrão como uma rede de segurança para o conteúdo que não está disponível em nenhum outro local.


## <a name="changes-from-prior-versions"></a>Alterações de versões anteriores

Veja a seguir as principais alterações nos grupos de limites e como os clientes encontram o conteúdo no branch atual do Configuration Manager. Muitas dessas alterações e conceitos funcionam em conjunto.

### <a name="configurations-for-fast-or-slow-are-removed"></a>Ocorre a remoção das configurações de pontos rápidos ou lentos

Você não configura mais os pontos de distribuição individuais como rápidos ou lentos. Em vez disso, cada sistema de sites associado a um grupo de limites é tratado da mesma forma. Por causa dessa alteração, as guias **Referências** das propriedades do grupo de limites não dão mais suporte à configuração de Rápido ou Lento.  

### <a name="new-default-boundary-group-at-each-site"></a>Novo grupo de limites padrão em cada site

Cada site primário tem um novo grupo de limites padrão chamado **Default-Site-Boundary-Group&lt;sitecode>** . Quando um cliente não está em um local de rede atribuído a um grupo de limites, ele usa os sistemas de sites associados ao grupo padrão de seu site atribuído. Planeje usar esse grupo de limites como uma substituição para o conceito de local de conteúdo de fallback.

#### <a name="allow-fallback-source-locations-for-content-is-removed"></a>Remoção de **Permitir locais de origem de fallback para conteúdo**

Você não configura mais explicitamente um ponto de distribuição a ser usado para fallback. As opções para definir essa configuração foram removidas do console.

Além disso, o resultado da configuração **Permitir que os clientes usem um local de origem de fallback para o conteúdo** em um tipo de implantação para aplicativos foi alterado. Essa configuração em um tipo de implantação agora permite que um cliente use o grupo de limites de site padrão como um local de fonte de conteúdo.

#### <a name="boundary-groups-relationships"></a>Relações de grupos de limites

Você pode vincular cada grupo de limites a um ou mais grupos de limites adicionais. Esses links formam relações configuradas na nova guia de propriedades de grupo limites chamada **Relações**:  

- Cada grupo de limites ao qual o cliente está associado diretamente é chamado de grupo de limites **atual**.  

- Qualquer grupo de limites que um cliente possa usar devido a uma associação entre o grupo de limites *atual* desse cliente e outro grupo é chamado de grupo de limites **vizinho**.  

- Na guia **Relações**, adicione grupos de limites para usá-los como um grupo de limites *vizinho*. Configure também um tempo em minutos para o fallback. Quando um cliente não consegue encontrar o conteúdo em um ponto de distribuição em seu grupo *atual*, esse tempo é quando o cliente começa a pesquisar os locais de conteúdo nos grupos de limites *vizinhos*.  

    Quando você adiciona ou altera uma configuração de grupo de limites, você pode bloquear o fallback para esse grupo de limites específico do grupo atual que está sendo configurado.  

Para usar a nova configuração, defina associações explícitas (links) de um grupo de limites para outro. Configure todos os pontos de distribuição nesse grupo associado com o mesmo tempo em minutos. Quando um cliente não consegue encontrar uma fonte de conteúdo de seu grupo de limites *atual*, o tempo configurado determina quando ele começa a pesquisar as fontes de conteúdo de seu grupo de limites vizinho.

Além dos grupos de limites configurados explicitamente, cada grupo de limite tem um link implícito para o grupo de limites de site padrão. Esse link se torna ativo após 120 minutos. Em seguida, o grupo de limites do site padrão torna-se um grupo de limites vizinho. Esse comportamento permite que os clientes usem como locais de fonte de conteúdo os pontos de distribuição associados a esse grupo de limites.

Esse comportamento substitui o que anteriormente era chamado de fallback de conteúdo. Substitua esse comportamento padrão de 120 minutos associando explicitamente o grupo de limites do site padrão a um grupo *atual*. Defina um tempo específico em minutos ou bloqueie o fallback por completo para impedir seu uso.

### <a name="clients-try-to-get-content-from-each-distribution-point-for-up-to-two-minutes"></a>Os clientes tentam obter o conteúdo de cada ponto de distribuição por até dois minutos

Quando um cliente pesquisa um local de fonte de conteúdo, ele tenta acessar cada ponto de distribuição por dois minutos antes de tentar outro ponto de distribuição. Esse comportamento é uma alteração de versões anteriores em que os clientes tentavam se conectar a um ponto de distribuição por até duas horas.

- Os clientes selecionam aleatoriamente o primeiro ponto de distribuição do pool de servidores disponíveis nos grupos de limites *atuais* do cliente.  

- Após dois minutos, se o cliente não encontrou o conteúdo, ele muda para um novo ponto de distribuição e tenta obter o conteúdo daquele servidor. Esse processo se repete a cada dois minutos até que o cliente localize o conteúdo ou atinja o último servidor em seu pool.  

- Se um cliente não consegue encontrar um local de fonte de conteúdo válido em seu pool *atual* antes de atingir o período de fallback para um grupo de limites *vizinho*, o cliente adiciona os pontos de distribuição desse grupo *vizinho* ao fim de sua lista atual. Ele então pesquisa o grupo expandido de locais de origem que inclui os pontos de distribuição de ambos os grupos de limites.  

    > [!TIP]  
    > Quando você cria um link explícito do grupo de limites atual para o grupo de limites do site padrão e define um tempo de fallback inferior ao tempo de fallback de um link para um grupo de limites vizinho, os clientes começam a pesquisar os locais de origem do grupo de limites do site padrão antes de incluir o grupo vizinho.  

- Quando o cliente falha em obter o conteúdo do último servidor no pool, ele inicia o processo novamente.  


## <a name="see-also"></a>Consulte também

- [Procedimentos para grupos de limites](/sccm/core/servers/deploy/configure/boundary-group-procedures)  

- [Sobre limites](/sccm/core/servers/deploy/configure/boundaries)  

- [Conceitos fundamentais para o gerenciamento de conteúdo](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)  
