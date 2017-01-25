---
title: "Planejar as funções do sistema de site | Microsoft Docs"
description: "Considere os servidores e as funções do sistema de sites enquanto você planeja sua hierarquia do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
caps.latest.revision: 11
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2b00cfcec0959716d69a1605018f33d30287fee9
ms.openlocfilehash: a2e57aac01fff3c28b4acfcf58bcd786bd3e62c4


---
# <a name="plan-for-site-system-servers-and-site-system-roles-for-system-center-configuration-manager"></a>Plano para funções e servidores do sistema de sites para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Cada site do System Center Configuration Manager que você instala inclui um servidor do site, que é um **servidor do sistema de sites**. O site também pode incluir servidores adicionais do sistema de sites em computadores que são remotos do servidor do site.   Servidores de sistemas de sites (o servidor do site ou um servidor do sistema de sites remoto) dão suporte a **funções de sistema de sites**.


##  <a name="a-namebkmksiteserversa-site-system-servers"></a><a name="bkmk_siteservers"></a> Servidores de sistema de sites  
 Quando você instala uma função do sistema de sites em um computador, esse computador torna-se um servidor do sistema de sites. Em cada site, você instala um ou mais servidores adicionais do sistema de sites. Também é possível optar por não instalar servidores adicionais do sistema de sites e executar todas as funções do sistema de sites diretamente no computador do servidor do site.  Cada servidor do sistema de sites permite uma ou mais funções do sistema de sites, além de ajudar a expandir os recursos e a capacidade de uma site compartilhando a carga do processamento da CPU que as funções do sistema de sites coloca em um servidor.  

 Ao considerar a adição de um servidor do sistema de sites, garanta que o servidor atenda aos pré-requisitos para o uso pretendido e que ele esteja em um local de rede que tenha largura de banda suficiente para se comunicar com os pontos de extremidade esperados, incluindo o servidor do site, os recursos do domínio, o local baseado na nuvem, os servidores do sistema de sites e os clientes).  

 Se você configurar o servidor do sistema de sites com um proxy para ser usado pelas funções de sistema de sites, confira [Funções do sistema de sites que podem usar um servidor proxy](#bkmk_proxy)  

##  <a name="a-namebkmkplanrolesa-site-system-roles"></a><a name="bkmk_planroles"></a> Site system roles  
 As funções do sistema de sites são instaladas em um computador para fornecer recursos adicionais ao site. Os exemplos incluem:  

-   Pontos de gerenciamento adicionais para que o site possa dar suporte a mais dispositivos, até chegar à capacidade com suporte pelos sites  

-   Pontos de distribuição adicionais para expandir sua infraestrutura de conteúdo, melhorando o desempenho de distribuições de conteúdo para usuários e dispositivos  

-   Uma ou mais funções de sistema de sites específicas do recurso, como um ponto de atualização de software, que você usa para gerenciar atualizações de software para dispositivos gerenciados, ou um ponto do Reporting Services para que você possa executar relatórios para monitorar e compreender ou compartilhar informações sobre a implantação  


Diferentes sites do Configuration Manager podem dar suporte a conjuntos diferentes de funções do sistema de sites. As funções do sistema de sites com suporte dependem do tipo do site (uma site de administração central, site primário ou site secundário). A topologia da sua hierarquia pode limitar o posicionamento de algumas funções em determinados tipos de site. Por exemplo, o ponto de conexão de serviço só é permitido no site de camada superior da hierarquia, que pode ser um site de administração central ou um site primário autônomo. Não há suporte para esta função em um site primário filho ou em sites secundários.  

Após a instalação de um site, você pode mover o local de algumas funções do sistema de sites do respectivo local padrão no servidor do site para outro servidor (como o ponto de gerenciamento ou ponto de distribuição, que são instalados por padrão em um servidor de site primário ou secundário). Você também pode instalar instâncias adicionais de algumas funções do sistema de sites para expandir os recursos de seu site (fornecer mais serviços aos clientes) e para atender aos requisitos de negócios. Algumas funções são obrigatórias, enquanto outras são opcionais:  

-   **Servidor do site do Configuration Manager** – essa função identifica o servidor em que a Instalação do Configuration Manager é executada para instalar um site ou o servidor no qual você instala um site secundário. Essa função não pode ser movida ou desinstalada até que o site seja desinstalado.  

-   **Sistema de sites do Configuration Manager** – essa função é atribuída a qualquer computador em que você instala um site ou instala uma função do sistema de sites.  Essa função não pode ser movida nem desinstalada até que a última função do sistema de sites seja removida do computador.  

-   **Função do sistema de sites do componente do Configuration Manager** – esta função identifica um sistema de sites que executa uma instância do serviço SMS Executive e é obrigatória para permitir outras funções, como pontos de gerenciamento. Essa função não pode ser movida nem desinstalada até que a última função do sistema de sites aplicável seja removida do computador.  

-   **Servidor de banco de dados do site do Configuration Manager** – esta função é atribuída aos servidores do sistema de sites que mantêm uma instância do banco de dados do site para um site.  Essa função pode ser movida para um novo servidor apenas ao modificar o site para usar um SQL Server diferente para hospedar o banco de dados do site.  

-   **Provedor de SMS** – a função Provedor de SMS é atribuída a cada computador que hospeda uma instância do Provedor de SMS, a interface entre um console do Configuration Manager e o banco de dados do site.  Por padrão, essa função é instalada automaticamente no servidor do site de um site de administração central e sites primários, e você pode instalar instâncias adicionais em cada site para fornecer acesso administrativo a um site para usuários administrativos adicionais.  

     Diferente da maioria das funções do sistema de sites que é instalada de dentro do console, para instalar provedores adicionais, você deve executar a Instalação do Configuration Manager para [Gerenciar o Provedor de SMS](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) e, em seguida, instalar provedores adicionais em outros computadores. Você só pode instalar uma instância do Provedor de SMS em um computador e o computador deve estar no mesmo domínio que o servidor do site.  

-   **Ponto de serviços Web do Catálogo de Aplicativos** – uma função de sistema de sites que fornece informações de software ao site do Catálogo de Aplicativos da Biblioteca de Software. Embora essa função tenha suporte em sites primários, você pode instalar várias instâncias dela em um site ou em vários sites na mesma hierarquia.  

-   **Ponto de sites da Web do catálogo de aplicativos** – uma função de sistema de sites que fornece aos usuários uma lista de softwares disponíveis do Catálogo de Aplicativos. Embora essa função tenha suporte em sites primários, você pode instalar várias instâncias dela em um site ou em vários sites na mesma hierarquia.  

     Quando o catálogo de aplicativos dá suporte a computadores cliente na Internet, como prática recomendada de segurança, instale o ponto de site da Web do catálogo de aplicativos em uma rede de perímetro e o ponto de serviço da Web do catálogo de aplicativos na intranet.  

-   **Ponto de sincronização do Asset Intelligence** – uma função do sistema de sites que se conecta à Microsoft para baixar informações do catálogo do Asset Intelligence e carregar títulos não categorizados para que eles sejam considerados para futura inclusão no catálogo.  Uma hierarquia dá suporte a apenas uma única instância dessa função, e esta deve estar no site de camada superior da hierarquia (um site de administração central ou o site primário autônomo). Se expandir um site primário autônomo para uma hierarquia maior, você deve desinstalar essa função do site primário e, em seguida, pode instalá-lo no site de administração central.   Para obter mais informações, consulte [Asset Intelligence no System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

-   **Ponto de registro de certificado** – uma função do sistema de sites que se comunica com um servidor que executa o Serviço de Registro de Dispositivo de Rede para gerenciar solicitações de certificado de dispositivos que usam o protocolo SCEP (Serviço de Registro de Dispositivo de Rede).  Essa função tem suporte apenas em sites primários e no site de administração central.   Embora um ponto de registro de certificado único possa fornecer funcionalidade a uma hierarquia inteira, para ajudar no balanceamento de carga das solicitações de certificado, você pode instalar várias instâncias dessa função em um site e em vários sites na mesma hierarquia. Quando houver várias instâncias em uma hierarquia, os clientes serão atribuídos aleatoriamente a um dos pontos de registro de certificado.  

     Cada ponto de registro de certificado requer acesso a uma instância separada de um Serviço de Registro de Dispositivo de Rede. Você não pode configurar dois ou mais pontos de registro de certificado para usar o mesmo Serviço de Registro de Dispositivo de Rede. Além disso, o ponto de registro de certificado não deve ser instalado no mesmo servidor que executa o Serviço de Registro de Dispositivo de Rede.  

- **Ponto de conector de gateway de gerenciamento de nuvem** – uma função de sistema de site para se comunicar com o [gateway de gerenciamento de nuvem](/sccm/core/clients/manage/setup-cloud-management-gateway). 

-   **Ponto de distribuição** – uma função do sistema de site que contém arquivos de origem para serem baixados por clientes, como conteúdo de aplicativos, pacotes de software, atualizações de software, imagens de sistemas operacionais e imagens de inicialização. Por padrão, essa função é instalada no computador do servidor do site de novos sites primários e secundários quando o site é instalado, mas não tem suporte em um site de administração central.  Você pode instalar múltiplas instâncias dessa função em um site com suporte, e em vários sites na mesma hierarquia.  Para obter mais informações, consulte [Conceitos fundamentais para o gerenciamento de conteúdo no System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) e [Gerenciar conteúdo e infraestrutura de conteúdo do System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   **Ponto de status de fallback** – uma função do sistema de sites que ajuda a monitorar a instalação do cliente e identificar os clientes não gerenciados, pois eles não podem se comunicar com o ponto de gerenciamento.  Embora essa função tenha suporte apenas em sites primários, você pode instalar várias instâncias dela em um site ou em vários sites na mesma hierarquia.  Para obter mais informações, consulte [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).


-   **Ponto do Endpoint Protection** – uma função do sistema de sites que o Configuration Manager usa para aceitar os termos de licença do Endpoint Protection e para configurar a associação padrão para o Cloud Protection Service (anteriormente conhecido como MAPS). Uma hierarquia dá suporte a apenas uma única instância dessa função, e esta deve estar no site de camada superior da hierarquia (um site de administração central ou o site primário autônomo). Se expandir um site primário autônomo para uma hierarquia maior, você deve desinstalar essa função do site primário e, em seguida, pode instalá-lo no site de administração central. Para obter mais informações, consulte [Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

-   **Ponto de registro** – uma função do sistema de sites que usa certificados PKI para que o Configuration Manager registre dispositivos móveis e computadores Mac. Embora essa função tenha suporte em sites primários, você pode instalar várias instâncias dela em um site ou em vários sites na mesma hierarquia.  

     Se um usuário registrar dispositivos móveis usando o Configuration Manager e sua conta do Active Directory estiver em uma floresta em que a floresta do servidor de site não confia, será necessário instalar um ponto de registro na floresta do usuário para que ele possa ser autenticado.  

-   **Ponto proxy do registro** – função do sistema de sites que gerencia as solicitações de registro do Configuration Manager de dispositivos móveis e computadores Mac. Embora essa função tenha suporte em sites primários, você pode instalar várias instâncias dela em um site ou em vários sites na mesma hierarquia.  

     Quando você oferece suporte a dispositivos móveis na Internet, como prática recomendada de segurança, instale o ponto proxy do registro em uma rede de perímetro e o ponto de registro na intranet.  

-   **Conector do Exchange Server** – para obter mais informações, consulte [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)  

-   **Ponto de gerenciamento** – uma função do sistema de sites que fornece informações sobre o local da política e do serviço para clientes e recebe dados de configuração de clientes.  
    Por padrão, essa função é instalada no computador do servidor do site de novos sites primários e secundários quando o site é instalado. Sites primários dão suporte a várias instâncias dessa função e sites secundários dão suporte a um único ponto de gerenciamento para fornecer um ponto de contato local para que os clientes obtenham as políticas do usuário e computador (um ponto de gerenciamento no site secundário é conhecido como ponto de gerenciamento proxy).  

     Pontos de gerenciamento podem ser configurados para dar suporte a HTTP ou HTTPs, bem como a dispositivos móveis que você gerencia com o Gerenciamento de Dispositivo Móvel local do System Center Configuration Manager. Você pode usar [Réplicas de banco de dados para os pontos de gerenciamento no System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md) para reduzir a carga de CPU colocada no servidor de banco de dados do site por pontos de gerenciamento conforme eles atendem solicitações de clientes.  

-   **Ponto do Reporting Services** – uma função do sistema de sites que se integra ao SQL Server Reporting Services para criar e gerenciar relatórios do Configuration Manager. Essa função tem suporte em sites primários e no site de administração central, e você pode instalar várias instâncias dela em um site compatível. Para obter mais informações, consulte [Planejamento para emissão de relatórios no System Center Configuration Manager](../../../core/servers/manage/planning-for-reporting.md).  

-   **Ponto de conexão de serviço** – uma função do sistema de sites que você usa para gerenciar dispositivos móveis com o Microsoft Intune e o MDM local. Essa função também carrega dados de uso do seu site e é necessária para fazer atualizações do Configuration Manager disponíveis no console do Configuration Manager. Uma hierarquia dá suporte a apenas uma única instância dessa função, e esta deve estar no site de camada superior da hierarquia (um site de administração central ou o site primário autônomo). Se expandir um site primário autônomo para uma hierarquia maior, você deve desinstalar essa função do site primário e, em seguida, pode instalá-lo no site de administração central. Para obter mais informações, consulte [Sobre o ponto de conexão de serviço no System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   **Ponto de atualização de software** – Uma função do sistema de sites que se integra ao WSUS (Windows Server Update Services) para fornecer atualizações de software a clientes do Configuration Manager. Essa função tem suporte em todos os sites:  

    -   Instale esse sistema de sites no site da administração central para sincronizar com o Windows Server Update Services.  

    -   Configure cada instância da função em sites primários filho para sincronizar com o site de administração central.  

    -   Considere a instalação de um ponto de atualização de software em sites secundários quando a transferência de dados pela rede for lenta.  

    Para obter mais informações, consulte [Planejar atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

-   **Ponto de migração de estado** – função do sistema de sites que armazena dados do estado do usuário quando um computador é migrado para um novo sistema operacional. Essa função tem suporte apenas em sites primários e em sites secundários, e você pode instalar várias instâncias dessa função em um site ou em vários sites na mesma hierarquia. Para obter mais informações sobre o armazenamento do estado do usuário ao implantar sistemas operacionais, consulte [Gerenciar o estado do usuário no System Center Configuration Manager](../../../osd/get-started/manage-user-state.md).  

-   **Ponto do Validador da Integridade do Sistema** – essa função do sistema de sites não é mais usada com o System Center Configuration Manager embora ele permaneça visível no console do Configuration Manager.  

##  <a name="a-namebkmkproxya-site-system-roles-that-can-use-a-proxy-server"></a><a name="bkmk_proxy"></a> Funções do sistema de sites que podem usar um servidor proxy  
 Algumas funções do sistema de sites do Configuration Manager requerem conexões com a Internet e usarão um servidor proxy quando o servidor do sistema de sites que hospeda a função for configurado para um. Geralmente, essa conexão é estabelecida no contexto do **sistema** do computador em que a função do sistema de site está instalada e não pode usar uma configuração de proxy para contas de usuário típicas. Quando um servidor proxy é solicitado a concluir uma conexão com a Internet, você deve configurar o computador para usar um servidor proxy:  

-   Você pode configurar um servidor proxy ao instalar uma função do sistema de sites.  

-   É possível adicionar ou modificar uma configuração do servidor proxy quando usa o console do Configuration Manager.  

-   Todas as funções do sistema de sites em um servidor do sistema de sites que podem usar uma configuração de servidor proxy usam a mesma configuração do servidor proxy. Se precisar de diferentes funções do sistema de sites para usar diferentes servidores proxy, você deverá instalar as funções do sistema de sites em diferentes computadores servidores do sistema de sites.  

-   Se você modificar a configuração do servidor proxy ou instalar uma nova função do sistema de sites em um computador que já tenha uma configuração de servidor proxy, a configuração original será substituída pela nova.  


Para ver procedimentos de configuração do servidor proxy para funções do sistema de site, consulte o tópico [Adicionar funções do sistema de sites ao System Center Configuration Manager](../../../core/servers/deploy/configure/add-site-system-roles.md).  

Veja a seguir as funções do sistema de sites que podem usar um servidor proxy:  

-   **Ponto de sincronização do Asset Intelligence** – essa função do sistema de sites conecta-se à Microsoft e usa uma configuração de servidor proxy no computador que hospeda o ponto de sincronização do Asset Intelligence.  

-   **Ponto de distribuição baseado em nuvem** – quando você usa um ponto de distribuição baseado em nuvem, o site primário que gerencia esse ponto de distribuição deve ser capaz de se conectar ao Microsoft Azure para provisionar, monitorar e distribuir conteúdo ao ponto de distribuição. Se um servidor proxy for necessário para essa conexão, você deverá configurar o servidor proxy no servidor primário. Você não pode configurar um servidor proxy no ponto de distribuição baseado em nuvem no Windows Azure.  Para obter mais informações, consulte a seção [Configure proxy settings for primary sites that manage cloud services (Definir configurações de proxy para sites primários que gerenciam serviços de nuvem)](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#BKMK_ConfigProxyforCloud) no tópico [Install cloud-based distribution points in Microsoft Azure for System Center Configuration Manager (Instalar pontos de distribuição baseados em nuvem no Microsoft Azure para o System Center Configuration Manager)](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md).  

-   **Conector do Exchange Server** – essa função do sistema de sites conecta-se a um Exchange Server e usa uma configuração de servidor proxy no computador que hospeda o conector do Exchange Server.  

-   **Ponto de atualização de software** – essa função do sistema de sites pode exigir conexões com o Microsoft Update para baixar patches e sincronizar informações sobre atualizações. Geralmente, quando você configura o servidor proxy, cada função do sistema de site naquele computador que dá suporte usando o servidor proxy usará o servidor proxy sem a configuração adicional necessária. Uma exceção é o ponto de atualização de software. Por padrão, pontos de atualização de software não usam um servidor proxy disponível, a menos que você habilite também as seguintes opções ao configurar o ponto de atualização de software:  

    -   **Usar um servidor proxy ao sincronizar atualizações de software**  

    -   **Usar um servidor proxy ao baixar conteúdo usando as regras de implantação automática**  

    > [!TIP]  
    >  Para você poder selecionar uma das duas opções, um servidor proxy deverá ser configurado no servidor do sistema de site que hospeda o ponto de atualização de software. O servidor proxy será usado somente nas opções específicas que você selecionar.  

 Para obter mais informações sobre servidores proxy para pontos de atualização de software, consulte a seção Configurações do servidor proxy no tópico [Install a software update point (Instalar um ponto de atualização de software)](../../../sum/get-started/install-a-software-update-point.md).  

-   **Ponto de conexão de serviço** – quando configurado para estar online (não offline), essa função do sistema de sites se conecta com o Microsoft Intune e o serviço de nuvem da Microsoft.  



<!--HONumber=Jan17_HO4-->


