---
title: Criar uma hierarquia | Microsoft Docs
description: "Compreenda as topologias disponíveis e as opções de gerenciamento para o System Center Configuration Manager para poder planejar a hierarquia do site."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
caps.latest.revision: 22
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 238ef5814c0c1b832c28d63c9f3879e21a6c439b
ms.openlocfilehash: 000acfec2cd61cc2d69e1bbd555b10fc22a40318


---
# <a name="design-a-hierarchy-of-sites-for-system-center-configuration-manager"></a>Criar uma hierarquia de sites para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de instalar o primeiro site de uma nova hierarquia do System Center Configuration Manager, você precisa compreender as topologias disponíveis para o Configuration Manager, os tipos de sites disponíveis e suas relações entre si e o escopo do gerenciamento fornecido por cada site. Em seguida, após considerar as opções de gerenciamento de conteúdo que podem reduzir o número de sites que precisa instalar, você pode planejar uma topologia que atenda de maneira eficaz suas necessidades de negócios atuais e, posteriormente, possa ser expandida para gerenciar o crescimento futuro.  

> [!NOTE]
> Ao planejar uma nova instalação do Configuration Manager, esteja atento às [notas de versão]( /sccm/core/servers/deploy/install/release-notes) que detalham problemas atuais nas versões ativas. As notas de versão se aplicam a todas as ramificações do Configuration Manager.  No entanto, ao usar a [Ramificação do Technical Preview]( /sccm/core/get-started/technical-preview), você encontrará problemas específicos apenas a essa ramificação na documentação de cada versão do Technical Preview.  

##  <a name="a-namebkmktopologya-hierarchy-topology"></a><a name="bkmk_topology"></a> Topologia de hierarquia  
 Intervalo de topologias de hierarquia de um único site primário autônomo para um grupo de sites primários e secundários conectados com um site de administração central no site de nível superior (camada superior) da hierarquia.    
O driver de chave do tipo e contagem de sites que você usa em uma hierarquia é normalmente o número e tipo de dispositivos aos quais você deve dar suporte:  

 **Site primário autônomo:** use um site primário autônomo quando um único site primário puder dar suporte ao gerenciamento de todos os seus dispositivos e usuários (consulte [Números de tamanho e escala](/sccm/core/plan-design/configs/size-and-scale-numbers)). Essa topologia também é bem-sucedida quando as diferentes localizações geográficas de sua empresa podem ser atendidas com êxito por um único site primário.  Para ajudar a gerenciar o tráfego de rede, você pode usar pontos de gerenciamento preferenciais e uma infraestrutura de conteúdo cuidadosamente planejada (Consulte [Conceitos fundamentais para o gerenciamento de conteúdo no System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)).  

 Benefícios dessa topologia incluem:  

-   Simplifica a sobrecarga administrativa  

-   Simplifica a detecção de recursos e serviços disponíveis e a atribuição de site do cliente  

-   Elimina a latência possível introduzida pela replicação de banco de dados entre sites  

-   Essa opção não é permanente e você pode expandir uma hierarquia primária autônoma em uma hierarquia maior com um site de administração central. Isso permite que você instale novos sites primários para expandir a escala de sua implantação.  


**Site de administração central com um ou mais sites primários filho:** use essa topologia quando precisar de mais de um site primário para dar suporte ao gerenciamento de todos os seus dispositivos e usuários.  Benefícios dessa topologia incluem:  

-   Necessário quando você precisa usar mais de um único site primário  

-   Dá suporte para até 25 sites primários, permitindo que você estenda a escala de sua hierarquia  

-   Essa opção é permanente. Não é possível desanexar um site filho primário para torná-lo um site primário autônomo. Portanto, a menos que você reinstale seus sites, você sempre usará o site de administração central  

 As seções a seguir podem ajudar você a entender quando usar um site específico ou a opção de gerenciamento de conteúdo no lugar de um site adicional.  

##  <a name="a-namebkmkchoosecasa-determine-when-to-use-a-central-administration-site"></a><a name="BKMK_ChooseCAS"></a> Determinar quando usar um site de administração central  
 Use um site de administração central para definir configurações em toda a hierarquia e monitorar todos os sites e objetos na hierarquia. Esse tipo de site não gerencia clientes diretamente, mas coordena a replicação de dados entre sites, o que inclui a configuração de sites e clientes em toda a hierarquia.  

**As informações a seguir podem ajudar você a decidir quando instalar um site de administração central:**  

-   O site da administração central é o site de nível superior em uma hierarquia  

-   Ao configurar uma hierarquia que tem mais de um site primário, você deve instalar um site de administração central e ele deve ser o primeiro site a ser instalado  

-   O site de administração central dá suporte a apenas sites primários como sites filho  

-   O site de administração central não pode ter clientes atribuídos a ele  

-   O site de administração central não dá suporte para funções de sistema de site que dão suporte diretamente para clientes, como pontos de gerenciamento e pontos de distribuição  

-   Você pode gerenciar todos os clientes na hierarquia e executar as tarefas de gerenciamento de site em qualquer site filho ao usar o console do Configuration Manager que está conectado ao site de administração central. Isso pode incluir a instalação de pontos de gerenciamento ou outras funções do sistema de site em sites filho primários ou secundários  

-   Ao usar um site de administração central, ele é o único lugar no qual é possível exibir dados de site de todos os sites em sua hierarquia. Esses dados incluem informações como dados de inventário e mensagens de status  

-   Você pode configurar operações de descoberta em toda a hierarquia no site de administração central ao atribuir métodos de descoberta a serem executados em sites individuais  

-   Você pode gerenciar a segurança em toda hierarquia ao atribuir diferentes funções de segurança, escopos de segurança e coleções a diferentes usuários administrativos. Essas configurações se aplicam a cada site na hierarquia  

-   Você pode configurar a replicação de arquivo e a de banco de dados para controlar a comunicação entre sites na hierarquia. Isso inclui o agendamento de replicação de banco de dados para dados de site e o gerenciamento de largura de banda para a transferência de dados baseados em arquivo entre sites  

##  <a name="a-namebkmkchoosepriimarya-determine-when-to-use-a-primary-site"></a><a name="BKMK_ChoosePriimary"></a> Determinar quando usar um site primário  
 Use sites primários para gerenciar clientes. É possível instalar um site primário como um site primário filho abaixo do site de administração central ou como o primeiro site de uma nova hierarquia. Um site primário que é instalado como o primeiro site de uma hierarquia cria um site primário autônomo. Ambos os sites primários filho e os sites primários autônomos oferecem suporte a sites secundários como sites filho do site primário.  

 Considere usar um site primário para qualquer um dos seguintes motivos:  

-   Para gerenciar usuários e dispositivos  

-   Para aumentar o número de dispositivos, é possível gerenciá-los com uma única hierarquia  

-   Para fornecer um ponto adicional de conectividade para administração de sua implantação  

-   Para atender aos requisitos de gerenciamento organizacional. Por exemplo, pode ser necessário instalar um site primário em uma localização remota para gerenciar a transferência de conteúdo de implantação pela rede de largura de banda baixa. No entanto, com o System Center Configuration Manager você pode usar opções para restringir o uso de largura de banda de rede ao transferir dados para um ponto de distribuição e essa capacidade de gerenciamento de conteúdo pode substituir a necessidade de instalar sites adicionais.  


**As informações a seguir podem ajudar você a decidir quando instalar um site primário:**  

-   Um site primário pode ser um site primário autônomo ou um site primário filho em uma hierarquia maior. Quando um site primário é membro de uma hierarquia com um site de administração central, os sites usam a replicação de banco de dados para replicar dados entre os sites. Recomenda-se instalar um site primário autônomo somente se você precisa oferecer suporte a mais clientes e dispositivos que um único site primário pode dar suporte.  Depois de instalar um site primário autônomo, você pode expandi-lo para relatar para um novo site de administração central para escalar verticalmente sua implantação.  

-   Um site primário dá suporte a somente um site de administração central como um site pai  

-   Um site primário dá suporte somente a sites secundários como sites filho e pode dar suporte a múltiplos sites secundários filho  

-   Os sites primários são responsáveis pelo processamento de todos os dados do cliente em seus clientes atribuídos  

-   Sites primários usam a replicação de banco de dados para se comunicar diretamente com seu site de administração central (isso é configurado automaticamente quando um novo site é instalado)  

##  <a name="a-namebkmkchoosesecondarya-determine-when-to-use-a-secondary-site"></a><a name="BKMK_ChooseSecondary"></a> Determinar quando usar um site secundário  
 Use sites secundários para gerenciar a transferência de dados de cliente e conteúdo de implantação em redes de baixa largura de banda.  

 Gerencie um site secundário de um site de administração central ou do site primário pai direto do site secundário. Os sites secundários devem ser anexados ao site primário, e você não pode movê-los para um site pai diferente sem desinstalá-los, e depois reinstalá-los como um site filho abaixo do novo site primário. No entanto, você pode rotear o conteúdo entre dois sites secundários pares para ajudar a gerenciar a replicação baseada em arquivos de conteúdo de implantação. Para transferir os dados do cliente para um site primário, o site secundário usa replicação baseada em arquivo. Um site secundário também usa replicação de banco de dados para se comunicar com seu site primário pai.  

 Considere instalar um site secundário se alguma das seguintes condições se aplicar:  

-   Você não precisa de um ponto local de conectividade para um usuário administrativo  

-   Você deve gerenciar a transferência de conteúdo de implantação para sites inferiores na hierarquia  

-   Você deve gerenciar informações do cliente que são enviadas para sites mais altos na hierarquia  

 Se não desejar instalar um site secundário e tiver clientes em locais remotos, considere usar o Windows BranchCache ou instalar pontos de distribuição que está habilitado para controle da largura de banda e agendamento. Você pode usar essas opções de gerenciamento de conteúdo com ou sem sites secundários, e eles podem ajudá-lo a reduzir o número de sites e servidores que você deve instalar. Para obter informações sobre opções de gerenciamento de conteúdo no Configuration Manager, consulte [Determinar quando usar as opções de gerenciamento de conteúdo](#BKMK_ChooseSecondaryorDP).  


**As informações a seguir podem ajudar você a decidir quando instalar um site secundário:**  

-   Os sites secundários instalam automaticamente o SQL Server Express durante a instalação do site se uma instância local do SQL Server não estiver disponível  

-   A instalação do site secundário é iniciada no console do Configuration Manager, em vez de executar a configuração do Configuration Manager diretamente em um computador  

-   Os sites secundários usam um subconjunto das informações do banco de dados do site, o que reduz a quantidade de dados replicados pela replicação de banco de dados entre o site pai primário e secundário  

-   Os sites secundários dão suporte ao roteamento de conteúdo baseado em arquivo para outros sites secundários que têm um site primário pai em comum  

-   As instalações do site secundário implantam automaticamente um ponto de gerenciamento e um ponto de distribuição que estão localizados no servidor do site secundário  

##  <a name="a-namebkmkchoosesecondaryordpa-determine-when-to-use-content-management-options"></a><a name="BKMK_ChooseSecondaryorDP"></a> Determinar quando usar as opções de gerenciamento de conteúdo  
 Se você tiver clientes em locais de rede remotos, considere usar uma ou mais opções de gerenciamento de conteúdo em vez de um site primário ou secundário. Geralmente, você pode remover a necessidade de instalar um site quando você usa o Windows BranchCache, configurar pontos de distribuição para controle de largura de banda ou copiar manualmente conteúdo para pontos de distribuição (conteúdo de pré-teste).  


**Considere a implantação de um ponto de distribuição em vez de instalar outro site se alguma das seguintes condições se aplicar:**  

-   Sua largura de banda de rede é suficiente para computadores cliente no local remoto para se comunicar com um ponto de gerenciamento para baixar política de cliente e enviar inventário, status do relatório e informações de descoberta  

-   O BITS (Serviço de Transferência Inteligente em Segundo Plano) não fornece controle de largura de banda suficiente para suas necessidades de rede  

 Para obter mais informações sobre as opções de gerenciamento de conteúdo do Configuration Manager, consulte [Conceitos fundamentais para o gerenciamento de conteúdo no System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

##  <a name="a-namebkmkbeyonda-beyond-hierarchy-topology"></a><a name="bkmk_beyond"></a> Além da topologia de hierarquia  
 Além de uma topologia de hierarquia inicial, considere quais serviços ou funcionalidades estarão disponíveis em sites diferentes da hierarquia (funções de sistema de sites) e como as funcionalidades e configurações que afetam toda a hierarquia serão gerenciadas na sua infraestrutura. A lista a seguir inclui as considerações mais comuns, que são abordadas em tópicos separados. Eles devem ser considerados como eles podem influenciar ou ser influenciados por seu design de hierarquia:  

-   Quando estiver se preparando para [Gerenciar computadores e dispositivos com o System Center Configuration Manager](/sccm/core/clients/manage/manage-clients), considere se os dispositivos que você gerencia residem localmente, na nuvem ou incluem dispositivos de usuários (BYOD).  Além disso, considere como você gerenciará dispositivos que têm suporte de diversas opções de gerenciamento, como computadores com Windows 10, que podem ser gerenciados diretamente pelo Configuration Manager ou por meio da integração com o Microsoft Intune.  

-   Compreenda como a infraestrutura de rede disponível pode afetar o fluxo de dados entre locais remotos (consulte [Preparar o ambiente de rede para o System Center Configuration Manager](/sccm/core/plan-design/network/configure-firewalls-ports-domains)). Considere também onde os usuários e dispositivos que você gerencia estão localizados geograficamente e se eles acessarão sua infraestrutura por meio do domínio corporativo ou da Internet.  

-   Planeje uma infraestrutura de conteúdo que distribua com eficiência as informações que você implantar (arquivos e aplicativos) nos dispositivos gerenciados (consulte [Gerenciar conteúdo e infraestrutura de conteúdo no System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)).  

-   Determine quais [Recursos e funcionalidades do System Center Configuration Manager](../../../core/plan-design/changes/features-and-capabilities.md) você planeja usar, as funções de sistema de sites ou infraestrutura do Windows de que eles precisam e em quais sites em uma hierarquia de sites múltiplos você pode implantá-los para atingir o uso mais eficiente de seus recursos de rede e servidor.  

-   Considere a segurança de dados e dispositivos, incluindo o uso de uma PKI. Consulte [Requisitos de certificado de PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md)  


**Examine os seguintes recursos para ver configurações específicas dos sites:**  

-   [Planejar o Provedor de SMS para o System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)  

-   [Planejar o banco de dados do site para o System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-site-database.md)  

-   [Plano para funções e servidores do sistema de sites para o System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)  

-   [Planejar a segurança no System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md)  

-   [Managing network bandwidth](../../../core/plan-design/hierarchy/manage-network-bandwidth.md) ao implantar conteúdo em um site  


**Considere as configurações que estendem sites e hierarquias:**  

-   [Opções de alta disponibilidade para o System Center Configuration Manager](/sccm/protect/understand/high-availability-options) para sites e hierarquias  

-   Você vai [Estender o esquema do Active Directory para o System Center Configuration Manager](../../../core/plan-design/network/extend-the-active-directory-schema.md) e configurar os sites para [Publicar dados do site para o System Center Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md)?  

-   Para gerenciar a largura de banda da rede entre sites em uma hierarquia, consulte [Transferências de dados entre sites no System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md)  

-   [Fundamentos de administração baseada em funções para o System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md)  



<!--HONumber=Dec16_HO3-->


