---
title: Criar uma hierarquia de site
titleSuffix: Configuration Manager
description: Compreenda as topologias disponíveis e as opções de gerenciamento para o Configuration Manager para planejar a hierarquia do site.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 74b8f7b099e906856300f5cc76b807daf894e060
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120071"
---
# <a name="design-a-hierarchy-of-sites-for-configuration-manager"></a>Projetar uma hierarquia de sites do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de instalar o primeiro site de uma nova hierarquia do Configuration Manager, é bom compreender:  

- As topologias disponíveis para o Configuration Manager  

- Os tipos de sites disponíveis e suas relações entre si  

- O escopo de gerenciamento que cada tipo de site oferece  

- As opções de gerenciamento de conteúdo que podem reduzir o número de sites que você precisa instalar  

Em seguida, planeje uma topologia que atenda com eficiência às suas necessidades de negócios atuais e depois possa ser expandida para gerenciar o crescimento futuro.  

Ao planejar, lembre-se das limitações para adicionar novos sites a uma hierarquia ou um site autônomo:  

- Você pode instalar um novo site primário abaixo de um site de administração central até o [número compatível de sites primários](/sccm/core/plan-design/configs/size-and-scale-numbers) para a hierarquia.  

- [Expanda um site primário autônomo para instalar um novo site de administração central](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand) para então instalar outros sites primários.  

- Instale novos sites secundários abaixo de um site primário até o [limite compatível para o site primário](/sccm/core/plan-design/configs/size-and-scale-numbers) e a hierarquia geral.  

- Não é possível adicionar um site instalado previamente a uma hierarquia existente para mesclar dois sites autônomos. O Configuration Manager só dá suporte à instalação de novos sites em uma hierarquia de sites existente.  


> [!NOTE]  
> Ao planejar uma nova instalação do Configuration Manager, esteja atento às [notas de versão](/sccm/core/servers/deploy/install/release-notes) que detalham problemas atuais nas versões ativas. As notas de versão se aplicam a todas as ramificações do Configuration Manager. Quando você usa o [branch de visualização técnica](/sccm/core/get-started/technical-preview), encontra questões específicas apenas desse branch na documentação de cada versão da visualização técnica.  



##  <a name="bkmk_topology"></a> Topologia de hierarquia  

Intervalo de topologias de hierarquia de:  

- Mais simples: um único site primário autônomo  

- Mais complexo: um grupo de sites primários e secundários conectados com um site de administração central no site de nível superior da hierarquia  

O driver principal do tipo e contagem de sites que você usa em uma hierarquia normalmente é o número e o tipo de dispositivos aos quais você deve dar suporte.   

### <a name="standalone-primary-site"></a>Site primário autônomo

Use um site primário autônomo quando ele puder dar suporte ao gerenciamento de todos os dispositivos e usuários. Para obter mais informações, veja [Números de escala e dimensionamento](/sccm/core/plan-design/configs/size-and-scale-numbers). Essa topologia também são bem-sucedidas quando as diferentes localizações geográficas de sua empresa podem ser atendidas com êxito por um único site primário. Para ajudar a gerenciar o tráfego de rede, use vários pontos de gerenciamento nos grupos de limite e uma infraestrutura de conteúdo cuidadosamente planejada. Para obter mais informações, veja [Configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) e [Conceitos fundamentais para o gerenciamento de conteúdo](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).  

Essa topologia fornece os seguintes benefícios:  

- Simplifica a sobrecarga administrativa  

- Simplifica a detecção de recursos e serviços disponíveis e a atribuição de site do cliente  

- Eliminação de possíveis atrasos introduzidos pela replicação de banco de dados entre sites  

- Opção para expandir um site primário autônomo em uma hierarquia maior com um site de administração central. Isso permite que você instale novos sites primários para expandir a escala da sua implantação.  


### <a name="central-administration-site-with-one-or-more-child-primary-sites"></a>Site de administração central com um ou mais sites primários filho 

Use essa topologia quando precisar de mais de um site primário para dar suporte ao gerenciamento de todos os seus dispositivos e usuários. É necessário quando você precisa usar mais de um único site primário. 

Essa topologia fornece os seguintes benefícios:  

- Dá suporte para até 25 sites primários que permite que você estenda a escala de sua hierarquia.    

- Você sempre usará o site de administração central, a menos que reinstale seus sites. Essa opção é permanente. Não é possível desanexar um site primário filho para fazer dele um site primário autônomo.  



##  <a name="BKMK_ChooseCAS"></a> Determinar quando usar um site de administração central  

Use um site de administração central para definir configurações em toda a hierarquia e monitorar todos os sites e objetos na hierarquia. Esse tipo de site não gerencia clientes diretamente. Ele coordena a replicação de dados do site a site, que inclui a configuração de sites e clientes em toda a hierarquia.  

As informações a seguir podem ajudar você a decidir quando instalar um site de administração central:  

- O site da administração central é o site de nível superior em uma hierarquia.  

- Ao configurar uma hierarquia que tem mais de um site primário, instale um site de administração central.  

     - Se você precisar imediatamente de dois ou mais sites primários, instale primeiro o site de administração central.  

     - Quando você já tiver um site primário e quiser instalar um site de administração central, [expanda o site primário autônomo](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand) para instalar o site de administração central.  

- O site de administração central oferece suporte a apenas sites primários como sites filho.  

- O site de administração central não pode ter clientes atribuídos a ele.  

- O site de administração central não dá suporte para funções de sistema de sites que dão suporte diretamente para clientes, como pontos de gerenciamento e pontos de distribuição.  

- Gerencie todos os clientes na hierarquia e realize todas as tarefas de gerenciamento do site do console do Configuration Manager que está conectado ao site de administração central. Essas tarefas incluem a instalação de pontos de gerenciamento ou outras funções do sistema de sites em sites filho primários ou secundários.  

- Quando você usa um site de administração central, ele é o único lugar em que você vê dados do site de todos os sites em sua hierarquia. Esses dados incluem informações como dados de inventário e mensagens de status.  

- Configure operações de descoberta em toda a hierarquia do site de administração central. No site de administração central, atribua os métodos de descoberta a serem executados em sites primários individuais.  

- Gerencie a segurança em toda hierarquia ao atribuir diferentes funções de segurança, escopos de segurança e coleções a diferentes usuários administrativos. Essas configurações se aplicam a cada site na hierarquia.  

- Configure a replicação para controlar a comunicação entre os sites na hierarquia. Agendamento de replicação de banco de dados para dados de site e gerenciamento de largura de banda para a transferência de dados baseados em arquivo entre sites.  



##  <a name="BKMK_ChoosePriimary"></a> Determinar quando usar um site primário  

Use sites primários para gerenciar clientes. Instale um site primário como um site filho abaixo do site de administração central ou como o primeiro site de uma nova hierarquia. Um site primário instalado como o primeiro site de uma hierarquia cria um site primário autônomo. Sites primários filho e sites primários autônomos dão suporte a sites secundários.  

Considere adicionar mais sites primários pelos seguintes motivos:  

- Para aumentar o número de dispositivos, gerencie com uma única hierarquia.  

- Para atender aos requisitos de gerenciamento organizacional. Por exemplo, pode ser necessário instalar um site primário em uma localização remota para gerenciar a transferência de conteúdo de implantação pela rede de largura de banda baixa.  

     - Em vez disso, considere usar opções para limitar a largura de banda de rede ao transferir dados para um ponto de distribuição. Essa capacidade de gerenciamento de conteúdo pode substituir a necessidade de instalar sites adicionais.  


As informações a seguir podem ajudar você a decidir quando instalar um site primário:  

- Um site primário pode ser um site primário autônomo ou um site primário filho em uma hierarquia maior. Quando um site primário é membro de uma hierarquia com um site de administração central, os sites usam a replicação de banco de dados para replicar dados entre os sites. A menos que você precise dar suporte a mais clientes e dispositivos do que um único site primário possa dar suporte, considere instalar um site primário autônomo. Depois de instalar um site primário autônomo, expanda-o, se necessário, no futuro para relatar para um novo site de administração central para aumentar sua implantação.  

- Um site primário oferece suporte a somente um site de administração central como um site pai.  

- Um site primário dá suporte somente a sites secundários como sites filho e dá suporte a múltiplos sites secundários.  

- Os sites primários são responsáveis pelo processamento de todos os dados do cliente em seus clientes atribuídos.  

- Sites primários usam a replicação de banco de dados para se comunicar diretamente com seu site de administração central. Esse comportamento é configurado automaticamente quando um novo site é instalado.  



##  <a name="BKMK_ChooseSecondary"></a> Determinar quando usar um site secundário  

Use sites secundários para gerenciar a transferência de dados de cliente e conteúdo de implantação em redes de baixa largura de banda.  

Gerencie um site secundário de um site de administração central ou do site primário pai direto do site secundário. Sites secundários são anexados a um site primário. Você não pode movê-los para um site pai diferente sem desinstalá-los e, em seguida, reinstalá-los como um site filho abaixo do novo site primário.

No entanto, você pode rotear o conteúdo entre dois sites secundários pares para ajudar a gerenciar a replicação baseada em arquivos de conteúdo de implantação. Para transferir os dados do cliente para um site primário, o site secundário usa replicação baseada em arquivo. Um site secundário também usa replicação de banco de dados para se comunicar com seu site primário pai.  

Considere instalar um site secundário se alguma das seguintes condições se aplicar:  

- Você não precisa de um ponto local de conectividade para um usuário administrativo.  

- Você precisa gerenciar a transferência de conteúdo de implantação para sites inferiores na hierarquia.  

- Você precisará gerenciar informações do cliente enviadas para sites mais acima na hierarquia.  

Se você não quiser instalar um site secundário e tiver clientes em locais remotos, considere as seguintes opções:  

- Use tecnologias ponto a ponto, como o Windows BranchCache  

- Habilite pontos de distribuição para agendamento e controle de largura de banda   

Use essas opções de gerenciamento de conteúdo com ou sem sites secundários. Elas ajudam a reduzir o tamanho da sua infraestrutura do Configuration Manager. Para obter mais informações sobre opções de gerenciamento de conteúdo no Configuration Manager, veja [Determinar quando usar as opções de gerenciamento de conteúdo](#BKMK_ChooseSecondaryorDP).  


As informações a seguir podem ajudar você a decidir quando instalar um site secundário:  

- Se uma instância local do SQL Server não estiver disponível, servidores de sites secundários instalarão automaticamente o SQL Server Express durante a instalação do site.  

- A instalação do site secundário é iniciada do console do Configuration Manager, em vez de executar a instalação diretamente em um computador.  

- Sites secundários usam um subconjunto das informações do banco de dados do site. Esse comportamento reduz a quantidade de dados SQL replicados entre o site pai primário e o site secundário.  

- Os sites secundários oferecem suporte ao roteamento de conteúdo baseado em arquivo para outros sites secundários que têm um site primário pai em comum.  

- Instalações do site secundário instalam automaticamente as funções do sistema de sites de ponto de distribuição e ponto de gerenciamento no servidor do site secundário.  



##  <a name="BKMK_ChooseSecondaryorDP"></a> Determinar quando usar as opções de gerenciamento de conteúdo  

Se você tiver clientes em locais de rede remotos, considere usar uma ou mais opções de gerenciamento de conteúdo em vez de um site primário ou secundário. As opções a seguir geralmente removem a necessidade de instalar um site:  

- Otimização de entrega para Windows 10  

- Cache par do Configuration Manager  

- Windows BranchCache  

- Configurar pontos de distribuição para controle de largura de banda  

- Copiar manualmente conteúdo para pontos de distribuição (pré-configurar conteúdo)  


Se qualquer uma das condições a seguir se aplicar, considere implantar um ponto de distribuição, em vez de instalar outro site:  

- Sua largura de banda de rede é suficiente para computadores cliente no local remoto para se comunicar com um ponto de gerenciamento no site primário. Os clientes se comunicam com um ponto de gerenciamento para baixar a política do cliente, enviar inventário, enviar status do relatório e enviar informações de descoberta.  

- O BITS (Serviço de Transferência Inteligente em Segundo Plano) não fornece controle de largura de banda suficiente para suas necessidades de rede.  

Para obter mais informações sobre as opções de gerenciamento de conteúdo no Configuration Manager, veja [Conceitos fundamentais para o gerenciamento de conteúdo](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).  



##  <a name="bkmk_beyond"></a> Além da topologia de hierarquia  

Juntamente com sua topologia de hierarquia inicial, considere também as seguintes perguntas:  

- Que funções do sistema de sites fornecem serviços ou funcionalidades de diferentes sites na hierarquia?  

- Como você está gerenciando configurações e funcionalidades em toda a hierarquia na sua infraestrutura?  


As seguintes considerações comuns são abordadas em artigos separados. Essa informação é importante para influenciar ou receber influência do seu design de hierarquia:  

- Quando você estiver se preparando para [Gerenciar computadores e dispositivos](/sccm/core/clients/manage/manage-clients), considere se os dispositivos são locais, na nuvem ou incluem BYOD (dispositivos pertencentes ao usuário). Além disso, considere como você gerenciará dispositivos que dão suporte a várias opções de gerenciamento. Por exemplo, gerencie dispositivos Windows 10 com o Configuration Manager ou por meio integração com o Microsoft Intune. Para obter mais informações, veja [Escolher uma solução de gerenciamento de dispositivo](/sccm/core/plan-design/choose-a-device-management-solution).  

- Entenda como a infraestrutura de rede disponível pode afetar o fluxo de dados entre locais remotos. Para obter mais informações, veja [Preparar o ambiente de rede](/sccm/core/plan-design/network/configure-firewalls-ports-domains). Considere também a localização geográfica dos seus usuários e dispositivos e se eles acessam sua infraestrutura por meio de sua rede local ou da Internet.  

- Planeje uma infraestrutura de conteúdo para distribuir com eficiência o conteúdo implantado aos dispositivos que você gerencia. Esse conteúdo pode consistir em aplicativos, atualizações de software ou sistemas operacionais. Para mais informações, confira [Manage content and content infrastructure](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure) (Gerenciar o conteúdo e a infraestrutura de conteúdo).  

- Determine quais [recursos e funcionalidades do Configuration Manager](/sccm/core/plan-design/changes/features-and-capabilities) você planeja usar. Diferentes recursos exigem diferentes funções do sistema de sites ou infraestrutura do Windows. Em uma hierarquia de vários sites, decida em que local implantá-los para o uso mais eficiente de seus recursos de rede e servidor.  

- Considere a segurança de dados e dispositivos, incluindo o uso de uma PKI (infraestrutura de chave pública). Para obter mais informações, veja [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


Examine os seguintes artigos sobre configurações específicas do site:  

- [Planejar o Provedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider)  

- [Planejar o banco de dados do site](/sccm/core/plan-design/hierarchy/plan-for-the-site-database)  

- [Planejar funções e servidores do sistema de sites](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles)  

- [Planejar a segurança](/sccm/core/plan-design/security/plan-for-security)  

- [Managing network bandwidth](/sccm/core/plan-design/hierarchy/manage-network-bandwidth) ao implantar conteúdo em um site  


Considerar configurações que abrangem sites e hierarquias  

- [Opções de alta disponibilidade](/sccm/protect/understand/high-availability-options) para sites e hierarquias

- [Estender o esquema do Active Directory](/sccm/core/plan-design/network/extend-the-active-directory-schema) e configurar sites para [publicar os dados](/sccm/core/servers/deploy/configure/publish-site-data)  

- [Transferências de dados entre sites](/sccm/core/servers/manage/data-transfers-between-sites)  

- [Fundamentos da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration)  

- [Gerenciar clientes na Internet](/sccm/core/clients/manage/manage-clients-internet)  

