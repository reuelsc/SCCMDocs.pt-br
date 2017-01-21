---
title: "Selecionar métodos de descoberta | Microsoft Docs"
description: "Examine as considerações sobre quais métodos usar e em quais sites executá-los."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 127ce713-d085-430f-ac7b-2701637fe126
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 54beff9bc8624d67efda7393db6334ebc96937d7

---
# <a name="select-discovery-methods-to-use-for-system-center-configuration-manager"></a>Selecione os métodos de descoberta para usar com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para usar a descoberta com êxito e eficiência para o System Center Configuration Manager, você deve considerar quais métodos usar e em quais sites executá-los.  

 Como a descoberta pode gerar um grande volume de tráfego de rede, e os DDRs (registros dos dados de descoberta) resultantes podem ocasionar um uso significativo de recursos da CPU durante o processamento, use somente os métodos de descoberta que você precisa para atingir as suas metas. Você pode começar usando somente um ou dois métodos de descoberta e, posteriormente, habilitar métodos adicionais de forma controlada para estender o nível de descoberta em seu ambiente. As informações neste tópico podem ajudá-lo a tomar decisões informadas.  

 Para obter informações sobre os métodos de descoberta diferentes, consulte [Sobre métodos de descoberta para o System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  

## <a name="select-methods-to-discover-different-things"></a>Selecionar métodos para descobrir coisas diferentes  
 Para descobrir possíveis computadores cliente do Configuration Manager ou recursos de usuários, você deve habilitar os métodos de descoberta apropriados. Você pode usar combinações diferentes de métodos de descoberta para localizar recursos diferentes e descobrir informações adicionais sobre esses recursos. Os métodos de descoberta que você usa determinam o tipo de recursos que são descobertos e quais serviços e agentes do Configuration Manager são usados no processo de descoberta. Eles também determinam o tipo de informações sobre recursos que você pode descobrir.  

 **Descobrir computadores**   
Quando desejar descobrir computadores, você poderá usar a descoberta de sistemas do Active Directory ou a descoberta de rede.  

 Como exemplo, se desejar descobrir recursos que podem instalar o cliente do Configuration Manager antes de você usar a instalação do cliente por push, execute a descoberta de sistemas do Active Directory. Como alternativa, você pode executar a descoberta de re e usar suas opções para descobrir o sistema operacional de recursos (necessário para uso posterior na instalação do cliente por push). Entretanto, ao usar a descoberta de sistemas do Active Directory, você descobre o recurso e as informações básicas, e pode descobrir informações estendidas sobre ele dos Serviços de Domínio Active Directory. Essas informações podem ser úteis na criação de consultas e coleções complexas para uso na atribuição de configurações de clientes ou implantação de conteúdo. A descoberta de rede, por outro lado, fornece informações sobre a topologia de rede que você não pode adquirir com outros métodos de descoberta, mas a descoberta de rede não fornece nenhuma informação sobre seu ambiente do Active Directory.  

 Também é possível usar somente a descoberta de pulsação para forçar a descoberta de clientes que você instalou por métodos diferentes da instalação do cliente por push. Entretanto, ao contrário de outros métodos de descoberta, a descoberta de pulsação não pode descobrir computadores que não têm um cliente ativo do Configuration Manager, e retorna um conjunto limitado de informações. Ela se destina a manter um registro do banco de dados existente, em vez de ser a base desse registro. As informações enviadas pela descoberta de pulsação podem não ser suficientes para criar consultas complexas ou coleções.  

 Se você usar a descoberta de grupos do Active Directory para descobrir a associação de um grupo especificado, poderá descobrir informações limitadas do sistema ou do computador. Isso não substitui uma descoberta completa de computadores, mas pode fornecer informações básicas. Essas informações básicas são insuficientes para a instalação do cliente por push.  

 **Descobrir usuários**   
Quando desejar descobrir informações sobre usuários, você poderá usar a descoberta de usuários do Active Directory. Semelhante à descoberta de sistemas do Active Directory, esse método descobre usuários do Active Directory e inclui informações básicas, além de informações estendidas do Active Directory. Você pode usar essas informações para criar consultas complexas e coleções semelhantes a essas para computadores.  

 **Descobrir informações do grupo**   
Quando desejar descobrir informações sobre grupos e associações de grupo, você poderá usar a descoberta de grupos do Active Directory. Esse método de descoberta cria registros de recursos para grupos de segurança.  

 Você pode usar esse método para pesquisar um grupo específico do Active Directory para identificar os membros desse grupo, além de quaisquer grupos aninhados nele. Além disso, pode usar esse método para pesquisar um local do Active Directory para grupos e, de modo repetitivo, pesquisar cada contêiner filho desse local nos Serviços de Domínio Active Directory.  

 Este método de descoberta também pode pesquisar a associação de grupos de distribuição. Isso pode identificar as relações de grupo de usuários e computadores.  

 Ao descobrir um grupo, você também pode descobrir informações limitadas sobre seus membros. Isso não substitui a descoberta de usuários ou de sistemas do Active Directory e, geralmente, não é suficiente para criar consultas complexas e coleções ou servir como base de uma instalação do cliente por push.  

 **Descobrir infraestrutura**   
Existem dois métodos que podem ser usados para descobrir a infraestrutura de rede: descoberta de florestas do Active Directory e descoberta de rede.  

 Você pode usar a descoberta de florestas do Active Directory para pesquisar uma floresta do Active Directory quanto a informações sobre sub-redes e configurações do site do Active Directory. Essas configurações podem ser inseridas automaticamente no Configuration Manager como locais limites.  

 Quando você deseja descobrir a topologia de rede, use a descoberta de rede. Enquanto outros métodos de descoberta retornam informações relacionadas aos Serviços de Domínio Active Directory e podem identificar o local da rede atual, eles não fornecer informações sobre infraestrutura com base nas sub-redes e na topologia do roteador da sua rede.  

##  <a name="a-namebkmkshareda-discovery-data-is-shared-between-sites"></a><a name="bkmk_shared"></a> Os dados de descoberta são compartilhados entre sites  
 Depois que o Configuration Manager adiciona dados de descoberta a um banco de dados, eles são compartilhados rapidamente entre todos os sites da hierarquia. Como normalmente não há vantagem em descobrir as mesmas informações em vários sites em sua hierarquia, considere configurar uma única instância de cada método de descoberta usado para ser executado em um único site em vez de executar várias instâncias de um único método em sites diferentes.  

 No entanto, para alguns ambientes, pode ser útil atribuir o mesmo método de descoberta para ser executado em vários sites, cada um com uma configuração e um cronograma à parte. Isso ocorre porque as configurações para executar um método de descoberta são específicas a um único site. Isso permite executar a descoberta em um site e compartilhar os resultados com outros sites ou usar o mesmo método em dois sites diferentes, em que a descoberta é executada em relação a um recurso local e não tenta descobrir informações de locais em uma WAN.  Por exemplo, isso geralmente é útil ao usar a descoberta de rede, na qual você direciona cada site para descobrir sua rede local em vez de tentar executar a descoberta de todos os locais de rede em uma WAN. Se você configurar várias instâncias dos mesmos métodos de descoberta para serem executadas em sites diferentes, planeje a configuração de cada site cuidadosamente para evitar que dois ou mais sites descubram os mesmos recursos da sua rede ou do Active Directory. A descoberta dos mesmos locais e recursos em vários sites pode consumir largura de banda de rede adicional e pode criar DDRs (registros dos dados de descoberta) duplicados para recursos que não agregam valor, mas que ainda devem ser processados por seus servidores do site.  

 A tabela a seguir identifica em quais sites é possível configurar os diferentes métodos de descoberta.  

|Método de Descoberta|Locais com suporte|  
|----------------------|-------------------------|  
|Descoberta de Florestas do Active Directory|Site de administração central<br /><br /> Site primário|  
|Descoberta de grupos do Active Directory|Site primário|  
|Descoberta de sistemas do Active Directory|Site primário|  
|Descoberta de Usuário do Active Directory|Site primário|  
|Descoberta de Pulsação<sup>1</sup>|Site primário|  
|Descoberta de Rede|Site primário<br /><br /> Site secundário|  

 <sup>1</sup> Sites secundários não podem configurar a Descoberta de Pulsação, mas podem receber o DDR de pulsação de um cliente.  

 Quando sites secundários executam a Descoberta de Rede ou recebem DDRs de Descoberta de Pulsação, eles transferem o DDR por replicação baseada em arquivo ao site primário pai. Isso porque somente sites primários e sites de administração central podem processar DDRs. Para obter mais informações sobre como os DDRs são processados, veja [Sobre registros dos dados de descoberta](../../../../core/servers/deploy/configure/run-discovery.md#BKMK_DDRs).  

## <a name="considerations-for-different-discovery-methods"></a>Considerações para diferentes métodos de descoberta  
 Como cada ambiente de servidor do site e de rede é diferente, limite suas configurações iniciais de descoberta e monitore atentamente cada servidor do site em termos de capacidade para processar os dados de descoberta gerados.  

-   Ao usar um método de descoberta do Active Directory para sistemas, usuários ou grupos:  

    -   Execute a descoberta em um site que tenha uma conexão de rede rápida com os controladores de domínio.  

    -   Considere a topologia de replicação do Active Directory para garantir que a descoberta possa acessar as informações mais recentes.  

    -   Considere o escopo da configuração de descoberta e limite a descoberta a apenas locais e grupos do Active Directory que devem ser descobertos.  

-   Se você usar a Descoberta de Rede:  

    -   Use uma configuração inicial limitada para identificar a topografia de rede.  

    -   Depois de identificar a topografia de rede, configure a Descoberta de Rede para ser executada em sites específicos centralizados nas áreas de rede que você deseja descobrir de forma mais completa.  

-   Como a Descoberta de Pulsação não é executada em um site específico, não é necessário considerá-la no planejamento geral de onde executar a descoberta.  

-   Como cada ambiente de servidor do site e de rede é diferente, limite suas configurações iniciais de descoberta e monitore atentamente cada servidor do site em termos de capacidade para processar os dados de descoberta gerados.  

##  <a name="a-namebkmkbesta-best-practices-for-discovery"></a><a name="bkmk_best"></a> Práticas recomendadas para descoberta  
 **Execute a Descoberta de Sistemas do Active Directory e a Descoberta de Usuários do Active Directory antes de executar a Descoberta de Grupos do Active Directory:**  

 Quando a Descoberta de Grupos do Active Directory identifica um usuário ou um computador não descoberto anteriormente como membro de um grupo, ela tenta descobrir detalhes básicos do usuário ou do computador. Como a Descoberta de Grupos do Active Directory não é otimizada para esse tipo de descoberta, esse processo pode causar a execução lenta da Descoberta de Grupos do Active Directory. Além disso, a Descoberta de Grupos do Active Directory identifica somente os detalhes básicos sobre os usuários e computadores descobertos, e não cria um registro completo de descoberta de usuários e computadores. Ao executar a Descoberta de Sistemas do Active Directory e a Descoberta de Usuários do Active Directory, os atributos adicionais do Active Directory de cada tipo de objeto ficam disponíveis e, portanto, a Descoberta de Grupos do Active Directory é executada com mais eficiência.  

 **Ao configurar a Descoberta de Grupos do Active Directory, especifique apenas os grupos usados com o Configuration Manager:**  

 Para ajudar a controlar o uso de recursos pela Descoberta de Grupos do Active Directory, especifique somente os grupos usados com o Configuration Manager. Isso porque a Descoberta de Grupos do Active Directory pesquisa recursivamente usuários, computadores e grupos aninhados em cada grupo descoberto. A pesquisa de cada grupo aninhado pode expandir o escopo da Descoberta de Grupos do Active Directory e reduzir o desempenho. Além disso, ao configurar a descoberta delta para a Descoberta de Grupos do Active Directory, o método de descoberta monitora as alterações de cada grupo. Reduz-se mais ainda o desempenho quando o método deve pesquisar grupos desnecessários.  

 **Configurar métodos de descoberta com um intervalo mais longo entre a descoberta completa e um período mais frequente de descoberta delta:**  

 Como a descoberta delta usa menos recursos do que um ciclo de descoberta completo e pode identificar recursos novos ou modificados no Active Directory, ao se usar a descoberta delta, é possível reduzir a frequência dos ciclos de descoberta completa para serem executados uma vez por semana ou menos. A descoberta delta para Descoberta de Sistemas do Active Directory, Descoberta de Usuários do Active Directory e Descoberta de Grupos do Active Directory identifica quase todas as alterações de objetos do Active Directory e pode manter dados de descoberta precisos para recursos.  

 **Execute os métodos de descoberta do Active Directory em um site primário que tem um local de rede mais próximo do controlador de domínio do Active Directory:**  

 Para melhorar o desempenho da descoberta do Active Directory, é recomendável executar a descoberta em um site primário que tenha uma conexão de rede rápida com os controladores de domínio. Se o mesmo método de descoberta do Active Directory for executado em vários sites, é recomendável configurar cada método de descoberta para evitar sobreposição. Diferente das versões anteriores do Configuration Manager, os dados de descoberta são compartilhados entre sites. Portanto, não é necessário descobrir as mesmas informações em vários sites. Para mais informações, consulte [Os dados de descoberta são compartilhados entre sites](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md#bkmk_shared).  

 **Execute a Descoberta de Florestas do Active Directory em somente um site quando planejar criar limites automaticamente por meio dos dados de descoberta:**  

 Se a Descoberta de Florestas do Active Directory for executada em mais de um site em uma hierarquia, é recomendável habilitar somente opções para criar limites automaticamente em um único site. Isso porque quando a Descoberta de Florestas do Active Directory é executada em cada site e cria limites, o Configuration Manager não pode mesclar esses limites em um objeto de limite único. Ao configurar a Descoberta de Florestas do Active Directory para criar limites automaticamente em vários sites, o resultado poderá ser objetos de limite duplicados no console do Configuration Manager.  



<!--HONumber=Dec16_HO3-->


