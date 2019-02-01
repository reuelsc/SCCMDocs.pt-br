---
title: Planejamento do trabalho de migração
titleSuffix: Configuration Manager
description: Use os trabalhos de migração para configurar os dados que você deseja migrar para o ambiente do System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a70bfbd4-757a-4468-9312-1c3b373ef9fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0e77225fb378a5851dbba9718dd3810463255cf7
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898419"
---
# <a name="plan-a-migration-job-strategy-in-system-center-configuration-manager"></a>Planejar a estratégia de trabalho de migração no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use trabalhos de migração para configurar os dados específicos que você deseja migrar para seu ambiente do System Center Configuration Manager. Os trabalhos de migração identificam os objetos que se planeja migrar e também são executados no site de nível superior na hierarquia de destino. É possível configurar um ou mais trabalhos de migração por site de origem. Isso permite migrar todos os objetos de uma só vez ou as sub-redes limitadas de dados com cada trabalho.  

 É possível criar trabalhos de migração após o Configuration Manager coletar com êxito os dados de um ou mais sites de uma hierarquia de origem. Você pode migrar dados em qualquer sequência dos sites de origem que coletaram os dados. Com um site de origem do Configuration Manager 2007, é possível migrar dados somente de um site onde o objeto foi criado. Com os sites de origem que executam o System Center 2012 Configuration Manager ou posterior, todos os dados que podem ser migrados estão disponíveis no site de nível superior da hierarquia de origem.  

 Antes de migrar clientes entre hierarquias, assegure-se de que os objetos que os clientes usam foram migrados e que esses objetos estão disponíveis na hierarquia de destino. Por exemplo, ao migrar de uma hierarquia de origem do Configuration Manager 2007 SP2, talvez seja necessário ter um anúncio para o conteúdo que é implantado em uma coleção personalizada que tem um cliente. Nesse cenário, é recomendável migrar a coleção, o anúncio e o conteúdo associado antes de migrar o cliente. Esses dados não poderão ser associados ao cliente na hierarquia de destino se o conteúdo, coleção e anúncio não forem migrados antes da migração do cliente. Se um cliente não está associado aos dados relacionados a um anúncio e conteúdo executados anteriormente, o conteúdo para instalação na hierarquia de destino pode ser oferecido para o cliente, o que talvez seja desnecessário. Quando o cliente migra depois que os dados foram migrados, o cliente é associado a esse conteúdo e anúncio, e a menos que o anúncio seja recorrente, não é oferecido a ele esse conteúdo para a anúncio migrado novamente.  

 Alguns objetos requerem mais do que a migração de dados da hierarquia da origem para a hierarquia de destino. Por exemplo, para migrar com êxito as atualizações de software para clientes na hierarquia de destino, você deve implantar um ponto de atualização de software ativo, configurar o catálogo de produtos e sincronizar o ponto de atualização de software com um WSUS (Windows Server Update Services) na hierarquia de destino.  

 Use as seções a seguir para ajudá-lo a planejar seus trabalhos de migração.  

-   [Tipos de trabalhos de migração](#Types_of_Migration)  

-   [Planejamento geral para todos os trabalhos de migração](#About_Migration_Jobs)  

-   [Planejando os trabalhos de migração de coleções](#About_Collection_Migration)  

-   [Planejando os trabalhos de migração de objetos](#About_Object_Migration)  

-   [Planejando trabalhos de migração de objetos migrados anteriormente](#About_Object_Migrations)  

##  <a name="Types_of_Migration"></a> Tipos de trabalhos de migração  
 O Configuration Manager dá suporte aos seguintes tipos de trabalho de migração. Cada tipo de trabalho foi desenvolvido para ajudar a definir os objetos que você pode incluir nesse trabalho.  

 **Migração de coleção** (com suporte apenas ao migrar do Configuration Manager 2007 SP2): Migre os objetos que estão relacionados às coleções selecionadas. Por padrão, a migração da coleção inclui todos os objetos que estão associados aos membros da coleção. Quando você usa um trabalho de migração da coleção, você pode excluir instâncias de objeto específico.  

 **Migração de objeto**: Migre objetos individuais que você selecionou. Você seleciona somente os dados específicos que deseja migrar.  

 **Migração de objetos já migrados**: migre os objetos que você já migrou quando eles foram atualizados na hierarquia de origem após a última migração.  

###  <a name="Objects_that_can_migrate"></a> Objetos que você pode migrar  
 Nem todo objeto pode ser migrado por um tipo específico de trabalho de migração. A lista a seguir identifica o tipo de objeto que pode ser migrado com cada tipo de trabalho de migração.  

> [!NOTE]  
>  Os trabalhos de migração de coleção estão disponíveis somente ao migrar objetos de uma hierarquia de origem do Configuration Manager 2007 SP2.  

 **Tipos de trabalho que você pode usar para migrar cada objeto**  

-   **Anúncios** (disponíveis para migrar de sites de origem do Configuration Manager 2007 com suporte)  

    -   Migração da coleção  


-   **Catálogo do Asset Intelligence**  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Requisitos de hardware do Asset Intelligence**  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Lista de softwares do Asset Intelligence**  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Limites**  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Linhas de base de configuração**  

    -   Migração da coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Itens de configuração**  

    -   Migração da coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Janelas de manutenção**  

    -   Migração da coleção  


-   **Imagens de inicialização para implantação do sistema operacional**  

    -   Migração da coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Pacotes de driver de implantação do sistema operacional**  

    -   Migração da coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Drivers de implantação do sistema operacional**  

    -   Migração da coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Imagens de implantação do sistema operacional**  

    -   Migração da coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Pacotes de implantação do sistema operacional**  

    -   Migração da coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Pacotes de distribuição de software**  

    -   Migração da coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Regras de medição de software**  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Pacotes de implantação de atualização de software**  

    -   Migração da coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Modelos de implantação de atualização de software**  

    -   Migração da coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Implantações de atualização de software**  

    -   Migração da coleção  


-   **Listas de atualizações de software**  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Sequências de tarefas**  

    -   Migração da coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Pacotes de aplicativos virtuais**  

    -   Migração da coleção  

    -   Migração de objeto  

    > [!IMPORTANT]  
    >  Embora você possa migrar um pacote de aplicativos virtuais usando a migração de objeto, os pacotes não podem ser migrados usando o tipo de trabalho de migração **Migração de objetos migrados anteriormente**. Em vez disso, é necessário excluir o pacote de aplicativo virtual migrado do site de destino e criar um novo trabalho de migração para migrar o aplicativo virtual.  

##  <a name="About_Migration_Jobs"></a> Planejamento geral para todos os trabalhos de migração  
 Use o Assistente para Criar Trabalho de Migração para criar um trabalho de migração para migrar objetos para a hierarquia de destino. O tipo de trabalho de migração que você cria determina quais objetos estão disponíveis para migrar. É possível criar e usar vários trabalhos de migração para migrar dados de um mesmo site de origem ou de vários sites de origem. O uso de um tipo de trabalho de migração não bloqueia o uso de um tipo diferente de trabalho de migração.  

 Executado com êxito o trabalho de migração, seu status é listado como **Concluído** e ele não pode ser executado novamente. No entanto, é possível criar um novo trabalho de migração para migrar qualquer objeto migrado pelo trabalho original e o novo trabalho de migração pode também incluir objetos adicionais. Ao criar trabalhos de migração adicionais, os objetos que foram migrados anteriormente mostram o estado de **Migrado**. É possível selecionar esses objetos para migrá-los novamente, mas a menos que o objeto tenha sido atualizado na hierarquia de origem, não é necessário migrar esses objetos novamente. Se o objeto foi atualizado na hierarquia de origem depois que foi migrado originalmente, é possível identificar esse objeto ao usar o tipo de trabalho de migração **Objetos modificados após a migração**.  

 Você pode excluir um trabalho de migração antes de ele ser executado. No entanto, após a conclusão do trabalho de migração, ele permanece visível no console do Configuration Manager e não pode ser excluído. Cada trabalho de migração que foi concluído ou ainda não foi executado permanece visível no console do Configuration Manager até que você conclua o processo de migração e limpe os dados de migração.  

> [!NOTE]  
>  Após a migração usando a ação **Limpar Dados de Migração** ser concluída, é possível reconfigurar a mesma hierarquia como a hierarquia de origem atual para restaurar a visibilidade dos objetos migrados anteriormente.  

 É possível exibir os objetos contidos em qualquer trabalho de migração no console do Configuration Manager selecionando o trabalho de migração e escolhendo a guia **Objetos no Trabalho**.  

 Use as informações nas seções a seguir para ajudá-lo a planejar todos os trabalhos de migração.  

### <a name="data-selection"></a>Seleção de dados  
 Quando você cria um trabalho de migração de coleção, você deve selecionar uma ou mais coleções. Após selecionar as coleções, o Assistente para Criar Trabalho de Migração mostra os objetos que estão associados às coleções. Por padrão, todos os objetos associados às coleções selecionadas são migrados, mas é possível desmarcar os objetos que você não deseja migrar com esse trabalho. Quando você desmarca um objeto que tem objetos dependentes, esses objetos dependentes também são desmarcados. Todos os objetos desmarcados são adicionados a uma lista de exclusões. Os objetos em uma lista de exclusão são removidos da seleção automática para trabalhos de migração futuros. Você deve editar manualmente a lista de exclusão para remover objetos que deseja que sejam selecionados automaticamente para migração em trabalhos de migração que você criará no futuro.  

### <a name="site-ownership-for-migrated-content"></a>Propriedade do site para o conteúdo migrado  
 Ao migrar conteúdo para implantações, você deverá atribuir o objeto do conteúdo a um site na hierarquia de destino. Esse site, então, torna-se o proprietário desse conteúdo na hierarquia de destino. Embora o site de nível superior da hierarquia de destino seja o site que realmente migra os metadados de conteúdo, é o site atribuído que acessa os arquivos originais de conteúdo na rede.  

 Para minimizar a largura de banda de rede usada durante a migração, considere a transferência de propriedade de conteúdo para o site mais próximo disponível. Como as informações de conteúdo são compartilhadas globalmente no System Center Configuration Manager, elas estarão disponíveis em todos os sites.  

 Informações sobre o conteúdo são compartilhadas para todos os sites na hierarquia de destino usando a replicação de banco de dados. No entanto, qualquer conteúdo que você atribui a um site primário e depois implanta nos pontos de distribuição em outros sites primários é transferido usando replicação baseada em arquivo. Essa transferência é roteada através do site de administração central e, em seguida, para cada site primário adicional. Ao centralizar pacotes que pretende distribuir para vários sites primários antes ou durante a migração quando você atribui um site como o proprietário do conteúdo, é possível reduzir a transferência de dados por meio de redes de baixa largura de banda.  

### <a name="role-based-administration-security-scopes-for-migrated-data"></a>Escopos de segurança de administração baseada em funções dados para migrados  
 Ao migrar dados para uma hierarquia de destino, é necessário atribuir um ou mais escopos de segurança de administração baseada em funções a objetos cujos dados são migrados. Isso garante que apenas os usuários administrativos apropriados tenham acesso a esses dados depois de serem migrados. Os escopos de segurança que você especifica são definidos pelo trabalho de migração e são aplicados a cada objeto migrado por esse trabalho. Se você necessita de escopos de segurança diferentes a serem aplicados a diferentes conjuntos de objetos e deseja atribuir esses escopos durante a migração, você deve migrar os diferentes conjuntos de objetos usando diferentes trabalhos de migração.  

 Antes de configurar um trabalho de migração, examine como a administração baseada em função funciona no System Center Configuration Manager. Se necessário, configure um ou mais escopos de segurança para os dados que você migrar para controlar quem terá acesso aos objetos migrados na hierarquia de destino.  

 Para obter mais informações sobre escopos de segurança e administração baseada em funções, veja [Fundamentos de administração baseada em funções para o System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

### <a name="review-migration-actions"></a>Examinar as ações de migração  
 Quando você configura um trabalho de migração, o Assistente para Criar Trabalho de Migração mostra uma lista de ações que você deve executar para garantir uma migração bem-sucedida e uma lista de ações que o Configuration Manager executa durante a migração dos dados selecionados. Examine essas informações cuidadosamente para verificar o resultado esperado.  

### <a name="schedule-migration-jobs"></a>Agendar trabalhos de migração  
 Por padrão, um trabalho de migração é executado imediatamente após a sua criação. No entanto, é possível especificar quando o trabalho de migração é executado ao criar o trabalho ou editando as propriedades do trabalho. É possível agendar o trabalho de migração para ser executado da seguinte maneira:  

-   Executar o trabalho agora  

-   Executar o trabalho em uma hora de início específica  

-   Não executar o trabalho  

### <a name="specify-conflict-resolution-for-migrated-data"></a>Especificar a resolução de conflitos de dados migrados  
 Por padrão, os trabalhos de migração não podem substituir dados no banco de dados de destino, a menos que você configure o trabalho de migração para ignorar ou substituir dados que foram migrados anteriormente para o banco de dados de destino.  

##  <a name="About_Collection_Migration "></a> Planejar os trabalhos de migração da coleção  
 Os trabalhos de migração de coleção estão disponíveis apenas quando você migra dados de uma hierarquia de origem executada em uma versão do Configuration Manager 2007 com suporte. Você deve especificar uma ou mais coleções a serem migradas quando realiza a migração por coleção. Para cada coleção especificada, o trabalho de migração seleciona automaticamente todos os objetos relacionados para migração. Por exemplo, se você selecionar uma coleção específica de usuários, os membros da coleção serão identificados e você poderá migrar as implantações associadas a esta coleção. Como opção, você pode selecionar outros objetos de implantação a serem migrados, que estão associados a esses membros. Todos esses itens selecionados são adicionados à lista de objetos que podem ser migrados.  

 Quando você migra uma coleção, o System Center Configuration Manager também migra as configurações da coleção, inclusive janelas de manutenção e variáveis da coleção, mas ele não pode migrar as configurações da coleção para o provisionamento do cliente AMT.  

 Utilize as informações das seções a seguir para saber mais sobre as configurações adicionais que podem ser aplicadas aos trabalhos de migração baseada em coleção.  

### <a name="exclude-objects-from-collection-migration-jobs"></a>Excluir objetos dos trabalhos de migração de coleção  
 Você pode excluir objetos específicos de um trabalho de migração de coleção. Quando você exclui um objeto específico de um trabalho de migração de coleção, esse objeto é adicionado a uma lista de exclusões global que contém todos os objetos que você excluiu dos trabalhos de migração, criados para qualquer site de origem da hierarquia de origem atual. Os objetos da lista de exclusão ainda estarão disponíveis para migração em trabalhos futuros e não serão incluídos automaticamente quando você criar um novo trabalho de migração baseada em coleção.  

 Você pode editar a lista de exclusão para remover objetos excluídos anteriormente. Depois que você remove um objeto da lista de exclusão, ele é automaticamente selecionado quando uma coleção associada é especificada durante a criação de um novo trabalho de migração.  

### <a name="unsupported-collections"></a>Coleções sem suporte  
 O Configuration Manager pode migrar qualquer uma das coleções de usuários padrão, coleções de dispositivos e a maioria das coleções personalizadas de uma hierarquia de origem do Configuration Manager 2007. No entanto, o Configuration Manager não é capaz de migrar coleções que contêm usuários e dispositivos na mesma coleção.  

 As seguintes coleções não podem ser migradas:  

-   Uma coleção que contém usuários e dispositivos.  

-   Uma coleção que contém uma referência a uma coleção de um tipo de recurso diferente. Por exemplo, uma coleção baseada em dispositivo, com uma subcoleção ou um link para uma coleção baseada em usuário. Neste exemplo, apenas a coleção de nível superior é migrada.  

-   Uma coleção que contém uma regra para incluir computadores desconhecidos. A coleção é migrada, mas a regra para incluir computadores desconhecidos não é migrada.  

### <a name="empty-collections"></a>Coleções vazias  
 Uma coleção vazia não contém recursos associados a ela. Quando o Configuration Manager migra uma coleção vazia, ele converte a coleção em uma pasta organizacional que não contém usuários ou dispositivos. Esta pasta é criada com o nome da coleção vazia no nó **Coleções de Usuários** ou **Coleções de Dispositivos**, no workspace **Ativos e Conformidade** do console do Configuration Manager.  

### <a name="linked-collections-and-subcollections"></a>Coleções e subcoleções vinculadas  
 Quando você migra coleções vinculadas a outras coleções ou que contêm subcoleções, o Configuration Manager cria uma pasta no nó **Coleções de Usuários** ou **Coleções de Dispositivos**, além das coleções e subcoleções vinculadas.  

### <a name="collection-dependencies-and-include-objects"></a>Dependências da coleção e inclusão de objetos  
 Quando você especifica uma coleção a ser migrada no Assistente para Criar Trabalho de Migração, todas as coleções dependentes são automaticamente selecionadas para serem incluídas no trabalho. Este comportamento garante que todos os recursos necessários estejam disponíveis após a migração.  

 Por exemplo: você seleciona uma coleção de dispositivos que executam o Windows 7 e chama-se **Win_7**. Esta coleção está limitada à coleção que contém os sistemas operacionais de todos os seus clientes, nomeada como **All_Clients**. A coleção **All_Clients** será automaticamente selecionada para migração.  

### <a name="collection-limiting"></a>Limitação da coleção  
 Com o System Center Configuration Manager, as coleções são dados globais e são avaliadas em cada site na hierarquia. Portanto, planeje como limitar o escopo de uma coleção depois da migração. Durante a migração, você pode identificar uma coleção da hierarquia de destino a ser usada para limitar o escopo da coleção que você está migrando de modo que a coleção migrada não contenha membros não previstos.  

 Por exemplo, no Configuration Manager 2007, as coleções são avaliadas no site que as cria e em sites filho. Um anúncio pode ser implantado apenas em um site filho, e isso limita o escopo do anúncio a esse site filho. Em comparação, com o System Center Configuration Manager, as coleções são avaliadas em cada site e os anúncios associados então são avaliados para cada site. A limitação da coleção permite que você refine os membros da coleção com base em outra coleção para evitar a adição de membros não previstos da coleção.  

### <a name="site-code-replacement"></a>Substituição de código do site  
 Ao migrar uma coleção que contém critérios que identificam um site do Configuration Manager 2007, você deve determinar um site específico na hierarquia de destino. Isso garante que a coleção migrada permaneça funcional em sua hierarquia de destino e não aumente em escopo.  

### <a name="specify-behavior-for-migrated-advertisements"></a>Especificar o comportamento de anúncios migrados  
 Por padrão, os trabalhos de migração baseados em coleção desativam anúncios migrados para a hierarquia de destino. Isso inclui todos os programas associados ao anúncio. Quando você cria um trabalho de migração baseada em coleção que contém anúncios, você vê a opção **Habilitar programas para implantação no Configuration Manager depois que um anúncio é migrado** na página **Configurações** do Assistente para Criar Trabalho de Migração. Se você selecionar esta opção, os programas associados aos anúncios serão habilitados depois de migrados. Como prática recomendada, não selecione essa opção. Em vez disso, habilite os programas após a migração quando quiser verificar os clientes que os receberão.  

> [!NOTE]  
>  Você vê a opção **Habilitar programas para implantação no Configuration Manager depois que um anúncio é migrado** apenas quando cria um trabalho de migração baseada em coleção e o trabalho de migração contém anúncios.  

 Para habilitar um programa após a migração, desmarque **Desabilitar este programa nos computadores em que é anunciado** na guia **Avançado** das propriedades do programa.  

##  <a name="About_Object_Migration"></a> Planejar trabalhos de migração de objetos  
 Ao contrário da migração de coleção, você deve selecionar cada objeto e instância do objeto que deseja migrar. Você pode selecionar os objetos individuais (como anúncios de uma hierarquia do Configuration Manager 2007 ou uma publicação de uma hierarquia do System Center 2012 Configuration Manager ou do System Center Configuration Manager) para adicionar à lista de objetos a serem migrados para um trabalho de migração específico. Todos os objetos que não forem adicionados à lista de migração não serão migrados para o site de destino pelo trabalho de migração de objeto.  

 Os trabalhos de migração baseada em objeto não têm configurações adicionais a serem planejadas além das aplicáveis a todos os trabalhos de migração.  

##  <a name="About_Object_Migrations"></a> Planejar trabalhos de migração de objetos migrados anteriormente  
 Quando um objeto que você já migrou para a hierarquia de destino é atualizado na hierarquia de origem, você pode migrá-lo novamente usando o tipo de trabalho **Objetos modificados após a migração** . Por exemplo, quando os arquivos de origem são renomeados ou atualizados para um pacote na hierarquia de origem, a versão do pacote é incrementada na hierarquia de origem. Depois que isso ocorre, o pacote pode ser identificado para migração por este tipo de trabalho.  

 Este tipo de trabalho é semelhante ao tipo de migração de objeto; porém, quando você seleciona os objetos a serem migrados, apenas os objetos atualizados após a migração por um trabalho de migração anterior poderão ser selecionados.   

 Quando você seleciona este tipo de trabalho, o comportamento de resolução de conflitos da página **Configurações** do Assistente para criar trabalho de migração é configurado para substituir os objetos migrados anteriormente. Essa configuração não pode ser alterada.  

> [!NOTE]  
>  Este trabalho de migração pode identificar os objetos atualizados automaticamente na hierarquia de origem e aqueles atualizados por um usuário administrativo.  
