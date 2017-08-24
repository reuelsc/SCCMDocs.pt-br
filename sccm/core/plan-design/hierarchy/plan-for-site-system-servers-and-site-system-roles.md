---
title: "Planejar as funções do sistema de site | Microsoft Docs"
description: "Considere os servidores e as funções do sistema de sites enquanto você planeja sua hierarquia do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
caps.latest.revision: "11"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0a3704a2d3b75ed7e0a7f718b681448ab6fc078d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-site-system-servers-and-site-system-roles-for-system-center-configuration-manager"></a>Plano para funções e servidores do sistema de sites para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Cada site do System Center Configuration Manager que você instala inclui um servidor do site, que é um **servidor do sistema de sites**. O site também pode incluir servidores adicionais do sistema de sites em computadores que são remotos do servidor do site. Servidores de sistemas de sites (o servidor do site ou um servidor do sistema de sites remoto) dão suporte a **funções de sistema de sites**.


##  <a name="bkmk_siteservers"></a> Servidores de sistema de sites  
 Quando você instala uma função do sistema de sites em um computador, esse computador torna-se um servidor do sistema de sites. Em cada site, você instala um ou mais servidores adicionais do sistema de sites. Também é possível optar por não instalar servidores adicionais do sistema de sites e executar todas as funções do sistema de sites diretamente no computador do servidor do site. Cada servidor de sistema de site dá suporte a uma ou mais funções de sistema de site. Servidores adicionais podem expandir os recursos e a capacidade de um site, compartilhando a carga de processamento da CPU que funções do sistema de site colocam em um servidor.  

 Ao considerar a adição de um servidor de sistema de site, verifique se o servidor atende aos pré-requisitos para o uso pretendido. Também é uma boa ideia adicioná-lo a um local de rede com largura de banda suficiente para se comunicar com pontos de extremidade esperados, incluindo o servidor do site, os recursos de domínio, um local baseado em nuvem, os servidores de sistema de site e os clientes).  

 Se você configurar o servidor do sistema de sites com um proxy para ser usado pelas funções de sistema de sites, confira [Funções do sistema de sites que podem usar um servidor proxy](#bkmk_proxy).  

##  <a name="bkmk_planroles"></a> Site system roles  
 As funções do sistema de sites são instaladas em um computador para fornecer recursos adicionais ao site. Os exemplos incluem:  

-   Pontos de gerenciamento adicionais para que o site possa dar suporte a mais dispositivos, até chegar à capacidade com suporte pelos sites.  

-   Pontos de distribuição adicionais para expandir sua infraestrutura de conteúdo, melhorando o desempenho de distribuições de conteúdo para usuários e dispositivos.  

-   Uma ou mais funções do sistema de site de recursos específicos. Por exemplo, um ponto de atualização de software permite que você gerencie atualizações de software para dispositivos gerenciados ou um ponto do Reporting Services permite executar relatórios para monitorar e compreender ou compartilhar informações sobre a implantação.  


Diferentes sites do Configuration Manager podem dar suporte a conjuntos diferentes de funções do sistema de sites. O conjunto de funções do sistema de sites com suporte depende do tipo do site (site de administração central, site primário ou site secundário). A topologia da sua hierarquia pode limitar o posicionamento de algumas funções em determinados tipos de site. Por exemplo, o ponto de conexão de serviço só é permitido no site de camada superior da hierarquia, que pode ser um site de administração central ou um site primário autônomo. Não há suporte para esta função em um site primário filho ou em sites secundários.  

Depois de instalar um site, você pode mover o local de algumas funções de sistema de site do local padrão no servidor de site para outro servidor. Por exemplo, isso se aplica ao ponto de gerenciamento ou ao ponto de distribuição, que são instalados por padrão em um servidor de site primário ou secundário. Você também pode instalar instâncias adicionais de algumas funções do sistema de sites para expandir os recursos de seu site (fornecer mais serviços aos clientes) e para atender aos requisitos de negócios. Algumas funções são obrigatórias, enquanto outras são opcionais.  

-   **Servidor do site do Configuration Manager.** Essa função identifica o servidor em que a Instalação do Configuration Manager é executada para instalar um site ou o servidor no qual você instala um site secundário. Essa função não pode ser movida ou desinstalada até que o site seja desinstalado.  

-   **Sistemas de site do Configuration Manager.** Essa função é atribuída a qualquer computador em que você instala um site ou uma função do sistema de sites. Essa função não pode ser movida nem desinstalada até que a última função do sistema de sites seja removida do computador.  

-   **Função de sistema de site de componente do Configuration Manager.** Essa função identifica um sistema de sites que executa uma instância do serviço SMS Executive e é obrigatória para permitir outras funções, como pontos de gerenciamento. Essa função não pode ser movida nem desinstalada até que a última função do sistema de sites aplicável seja removida do computador.  

-   **Servidor de banco de dados de site do Configuration Manager.** Essa função é atribuída aos servidores do sistema de sites que mantêm uma instância do banco de dados do site para um site. Essa função pode ser movida para um novo servidor apenas ao modificar o site para usar uma instância diferente do SQL Server para hospedar o banco de dados do site.  

-   **Provedor de SMS.** A função Provedor de SMS é atribuída a cada computador que hospeda uma instância do Provedor de SMS, a interface entre um console do Configuration Manager e o banco de dados do site. Por padrão, essa função é instalada automaticamente no servidor de site de um site de administração central e sites primários. Você pode instalar instâncias adicionais em cada site para fornecer acesso a usuários administrativos adicionais.  

     Para instalar provedores adicionais, você deve executar a Instalação do Configuration Manager para [Gerenciar o Provedor de SMS](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider). Em seguida, você instala provedores adicionais em computadores adicionais. Você só pode instalar uma instância do Provedor de SMS em um computador e o computador deve estar no mesmo domínio que o servidor do site.  

-   **Ponto de serviços Web do Catálogo de Aplicativos.** Uma função do sistema de site que fornece informações sobre softwares para o site do Catálogo de Aplicativos da Biblioteca de Software. Embora essa função tenha suporte em sites primários, você pode instalar várias instâncias dela em um site ou em vários sites na mesma hierarquia.  

-   **Ponto de sites da Web do Catálogo de Aplicativos.** Uma função do sistema de site que fornece aos usuários uma lista de softwares disponíveis no Catálogo de Aplicativos. Embora essa função tenha suporte em sites primários, você pode instalar várias instâncias dela em um site ou em vários sites na mesma hierarquia.  

     Quando o catálogo de aplicativos dá suporte a computadores cliente na Internet, é prática recomendada de segurança instalar o ponto de site da Web do Catálogo de Aplicativos em uma rede de perímetro para segurança e instalar o ponto de serviço Web do Catálogo de Aplicativos na intranet.  

-   **Ponto de sincronização do Asset Intelligence.** Uma função de sistema de site que se conecta à Microsoft para baixar informações de catálogo do Asset Intelligence. Essa função também carrega títulos não categorizados, para que eles possam ser considerados para inclusão futura no catálogo. Uma hierarquia dá suporte a apenas uma única instância dessa função, e esta deve estar no site de camada superior da hierarquia (um site de administração central ou o site primário autônomo). Se expandir um site primário autônomo para uma hierarquia maior, você deverá desinstalar essa função do site primário e, em seguida, instalá-lo no site de administração central.   Para obter mais informações, consulte [Asset Intelligence no System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

-   **Ponto de registro de certificado.** Uma função de sistema de site que se comunica com um servidor que executa o Serviço de Registro de Dispositivo de Rede. Essa função gerencia solicitações de certificado de dispositivo que usam SCEP (Simple Certificate Enrollment Protocol). Essa função tem suporte apenas em sites primários e no site de administração central.

     Embora um ponto de registro de certificado único possa fornecer funcionalidade a uma hierarquia inteira, para ajudar no balanceamento de carga das solicitações de certificado, convém instalar várias instâncias dessa função em um site e em vários sites na mesma hierarquia. Isso pode ajudar no balanceamento de carga. Quando houver várias instâncias em uma hierarquia, os clientes serão atribuídos aleatoriamente a um dos pontos de registro de certificado.  

     Cada ponto de registro de certificado requer acesso a uma instância separada de um Serviço de Registro de Dispositivo de Rede. Você não pode configurar dois ou mais pontos de registro de certificado para usar o mesmo Serviço de Registro de Dispositivo de Rede. Além disso, o ponto de registro de certificado não deve ser instalado no mesmo servidor que executa o Serviço de Registro de Dispositivo de Rede.  

- **Ponto de gerenciamento de conector de gateway de nuvem.** Uma função de sistema de site para se comunicar com o [gateway de gerenciamento de nuvem](/sccm/core/clients/manage/setup-cloud-management-gateway).

-   **Ponto de distribuição.** Uma função do sistema de site que contém arquivos de origem para serem baixados por clientes, como conteúdo de aplicativos, pacotes de software, atualizações de software, imagens de sistemas operacionais e imagens de inicialização. Por padrão, essa função é instalada no computador do servidor do site de novos sites primários e secundários quando o site é instalado. Não há suporte para essa função em um site de administração central. Você pode instalar múltiplas instâncias dessa função em um site com suporte, e em vários sites na mesma hierarquia. Para obter mais informações, consulte [Conceitos fundamentais para o gerenciamento de conteúdo no System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) e [Gerenciar conteúdo e infraestrutura de conteúdo do System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   **Ponto de status de fallback.** Uma função do sistema de site que ajuda a monitorar a instalação do cliente e identificar os clientes não gerenciados, pois eles não podem se comunicar com o ponto de gerenciamento. Embora essa função tenha suporte em sites primários, você pode instalar várias instâncias dela em um site e em vários sites na mesma hierarquia.     


-   **Ponto do Endpoint Protection.** Função do sistema de site que o Configuration Manager usa para aceitar os termos de licença do Endpoint Protection e configurar a associação padrão para o Cloud Protection Service. Uma hierarquia dá suporte a apenas uma única instância dessa função, e esta deve estar no site de camada superior da hierarquia (um site de administração central ou o site primário autônomo). Se expandir um site primário autônomo para uma hierarquia maior, você deverá desinstalar essa função do site primário e, em seguida, instalá-lo no site de administração central. Para saber mais, confira [Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

-   **Ponto de registro.** Uma função do sistema de sites que usa certificados PKI para que o Configuration Manager registre dispositivos móveis e computadores Mac. Embora essa função tenha suporte em sites primários, você pode instalar várias instâncias dela em um site ou em vários sites na mesma hierarquia.  

     Se um usuário registrar dispositivos móveis usando o Configuration Manager e sua conta do Active Directory estiver em uma floresta em que a floresta do servidor de site não confia, será necessário instalar um ponto de registro na floresta do usuário. O usuário pode então ser autenticado.  

-   **Ponto proxy do registro.** Função do sistema de site que gerencia as solicitações de registro do Configuration Manager de dispositivos móveis e computadores Mac. Embora essa função tenha suporte em sites primários, você pode instalar várias instâncias dela em um site ou em vários sites na mesma hierarquia.  

     Quando você der suporte a dispositivos móveis na Internet, instale o ponto proxy do registro em uma rede de perímetro, para segurança, e instale o ponto de registro na intranet.  

-   **Conector do Exchange Server** Para saber mais sobre essa função, confira [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)  

-   **Ponto de gerenciamento.** Uma função do sistema de site que fornece informações sobre o local da política e do serviço para clientes e recebe dados de configuração de clientes.  

    Por padrão, essa função é instalada no computador do servidor do site de novos sites primários e secundários quando o site é instalado. Sites primários dão suporte a várias instâncias dessa função. Sites secundários dão suporte a um único ponto de gerenciamento, para fornecer um ponto de contato local para que os clientes obtenham políticas de computador e usuário (um ponto de gerenciamento em um site secundário é conhecido como um ponto de gerenciamento de proxy).  

     Pontos de gerenciamento podem ser configurados para dar suporte a HTTP ou HTTPs, bem como a dispositivos móveis que você gerencia com o Gerenciamento de Dispositivo Móvel local do System Center Configuration Manager. Você pode usar [Réplicas de banco de dados para os pontos de gerenciamento no System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md) para reduzir a carga de CPU colocada no servidor de banco de dados do site por pontos de gerenciamento conforme eles atendem solicitações de clientes.  

-   **Ponto do Reporting Services.** Uma função do sistema de site que se integra ao SQL Server Reporting Services para criar e gerenciar relatórios do Configuration Manager. Essa função tem suporte em sites primários e no site de administração central, e você pode instalar várias instâncias dela em um site compatível. Para obter mais informações, consulte [Planejamento para emissão de relatórios no System Center Configuration Manager](../../../core/servers/manage/planning-for-reporting.md).  

-   **Ponto de conexão de serviço.** Uma função de sistema de site que você usa para gerenciar dispositivos móveis com o Microsoft Intune e MDM local. Essa função também carrega dados de uso do seu site e é necessária para fazer atualizações do Configuration Manager disponíveis no console do Configuration Manager. Uma hierarquia dá suporte a apenas uma única instância dessa função, e esta deve estar no site de camada superior da hierarquia (um site de administração central ou o site primário autônomo). Se expandir um site primário autônomo para uma hierarquia maior, você deverá desinstalar essa função do site primário e, em seguida, instalá-lo no site de administração central. Para obter mais informações, consulte [Sobre o ponto de conexão de serviço no System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   **Ponto de atualização de software.** Uma função do sistema de site que se integra ao WSUS (Windows Server Update Services) para fornecer atualizações de software a clientes do Configuration Manager. Essa função tem suporte em todos os sites:  

    -   Instale esse sistema de site no site de administração central para sincronização com o WSUS.  

    -   Configure cada instância da função em sites primários filho para sincronizar com o site de administração central.  

    -   Considere a instalação de um ponto de atualização de software em sites secundários quando a transferência de dados pela rede for lenta.  

    Para obter mais informações, consulte [Planejar atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

-   **Ponto de migração de estado.** Uma função do sistema de site que armazena dados do estado do usuário quando um computador é migrado para um novo sistema operacional. Essa função tem suporte em sites primários e secundários. Você pode instalar múltiplas instâncias dessa função em um site e em vários sites na mesma hierarquia. Para obter mais informações sobre o armazenamento do estado do usuário ao implantar sistemas operacionais, consulte [Gerenciar o estado do usuário no System Center Configuration Manager](../../../osd/get-started/manage-user-state.md).  

-   **Ponto do Validador da Integridade do Sistema.** Embora essa função de sistema de site permaneça visível no console do Configuration Manager, não é mais usada.  

###  <a name="bkmk_proxy"></a> Funções do sistema de sites que podem usar um servidor proxy  
 Algumas funções do sistema de sites do Configuration Manager requerem conexões com a Internet e usarão um servidor proxy quando o servidor do sistema de sites que hospeda a função for configurado para um. Normalmente, essa conexão é feita no contexto do **sistema** do computador em que a função de sistema de site está instalada. A conexão não pode usar uma configuração de proxy para contas de usuário típicas. Quando um servidor proxy é solicitado a concluir uma conexão com a Internet, você deve configurar o computador para usar um servidor proxy:  

-   Você pode configurar um servidor proxy ao instalar uma função de sistema de site.  

-   É possível adicionar ou modificar uma configuração do servidor proxy quando usa o console do Configuration Manager.  

-   A mesma configuração de servidor proxy é usada para todas as funções do sistema de sites em um servidor de sistema de sites que pode usar uma configuração de servidor proxy. Se precisar de diferentes funções do sistema de site para usar diferentes servidores proxy, você deverá instalar as funções do sistema de site em diferentes computadores servidores.  

-   Se você modificar a configuração do servidor proxy ou instalar uma nova função do sistema de sites em um computador que já tenha uma configuração de servidor proxy, a configuração original será substituída pela nova.  


Para ver procedimentos de configuração do servidor proxy para funções do sistema de site, confira o tópico [Adicionar funções do sistema de sites ao System Center Configuration Manager](../../../core/servers/deploy/configure/add-site-system-roles.md).  

Veja a seguir as funções do sistema de sites que podem usar um servidor proxy:  

-   **Ponto de sincronização do Asset Intelligence.** Esta função do sistema de site conecta-se à Microsoft e usa uma configuração de servidor proxy no computador que hospeda o ponto de sincronização do Asset Intelligence.  

-   **Ponto de distribuição baseado em nuvem.** Quando você usa um ponto de distribuição baseado em nuvem, o site primário que gerencia esse ponto de distribuição deve ser capaz de se conectar ao Microsoft Azure para provisionar, monitorar e distribuir conteúdo ao ponto de distribuição. Se um servidor proxy for necessário para essa conexão, você deverá configurar o servidor proxy no servidor primário. Não é possível configurar um servidor proxy em um ponto de distribuição baseado em nuvem no Azure. Para saber mais, confira a seção [Definir configurações de proxy para sites primários que gerenciam serviços de nuvem](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#BKMK_ConfigProxyforCloud) no tópico [Instalar pontos de distribuição baseados em nuvem no Microsoft Azure para o System Center Configuration Manager](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md).  

-   **Conector do Exchange Server** Esta função do sistema de site conecta-se a um Exchange Server e usa uma configuração de servidor proxy no computador que hospeda o conector do Exchange Server.  

-   **Ponto de atualização de software.** Esta função do sistema de site pode exigir conexões com o Microsoft Update para baixar patches e sincronizar informações sobre atualizações. Normalmente, quando você configura o servidor proxy, cada função de sistema de site no computador que dá suporte ao uso do servidor proxy usa o servidor proxy. Nenhuma configuração adicional é necessária. Uma exceção é o ponto de atualizações de software. Por padrão, pontos de atualizações de software não usam um servidor proxy disponível, a menos que você habilite também as seguintes opções ao configurar o ponto de atualizações de software:  

    -   **Usar um servidor proxy ao sincronizar atualizações de software**  

    -   **Usar um servidor proxy ao baixar conteúdo usando as regras de implantação automática**  

    > [!TIP]  
    >  Antes de você selecionar uma das opções, um servidor proxy deve ser configurado no servidor de sistema de site que hospeda o ponto de atualizações de software. O servidor proxy será usado somente nas opções específicas que você selecionar.  

 Para saber mais sobre servidores proxy para pontos de atualização de software, confira a seção "Configurações do servidor proxy" no tópico [Instalar um ponto de atualização de software](../../../sum/get-started/install-a-software-update-point.md).  

-   **Ponto de conexão de serviço.** Quando configurado para estar online (não offline), essa função de sistema de site conecta-se ao Microsoft Intune e ao serviço de nuvem da Microsoft.  
