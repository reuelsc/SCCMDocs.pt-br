---
title: "Alterações do Configuration Manager 2012 | Microsoft Docs "
description: "Identifique as mudanças e os novos recursos do System Center Configuration Manager com relação ao System Center 2012 Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
caps.latest.revision: 51
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 6b1a4584ebcd4dadd983677b714486402c93e190
ms.lasthandoff: 03/27/2017


---
# <a name="what39s-changed-in-system-center-configuration-manager-from-system-center-2012-configuration-manager"></a>O que mudou no System Center Configuration Manager com relação ao System Center 2012 Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


 A ramificação atual do System Center Configuration Manager introduz alterações importantes com relação ao System Center 2012 Configuration Manager. Este tópico identifica alterações significativas e as novas funcionalidades encontradas na versão de linha de base 1511 do System Center Configuration Manager. Para saber mais sobre as alterações introduzidas em atualizações posteriores do System Center Configuration Manager, consulte [Novidades nas versões incrementais do System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).



 A versão de dezembro de 2015 do System Center Configuration Manager (versão 1511) é a versão inicial do produto atual do Configuration Manager da Microsoft. Normalmente, é chamada de branch atual do System Center Configuration Manager. *Ramificação atual* indica que esta é uma versão que dá suporte a atualizações incrementais para o produto. Também fornece uma maneira de distinguir entre esta versão e as versões anteriores do Configuration Manager.  

 System Center Configuration Manager:  

-   Não usa um ano nem um identificador de produto no nome do produto, diferente das versões anteriores como Configuration Manager 2007 ou System Center 2012 Configuration Manager.

-   Dá suporte a atualizações incrementais no produto, também chamadas de versões de atualização. A versão de inicial era a 1511. As versões subsequentes são lançadas várias vezes no ano como atualizações no console, como a versão 1610.
-   É instalado usando uma versão de linha de base. Embora a 1511 fosse a versão de linha de base original, novas versões de linha de base também são liberadas de tempos em tempos, como a 1606. As versões de linha de base podem ser usadas para instalar um novo site do System Center Configuration Manager e para atualizar de uma versão com suporte do Configuration Manager 2012.




##  <a name="bkmk_updates"></a> Atualizações no console para o Configuration Manager  
 O System Center Configuration Manager usa um método de serviço no console chamado **Atualizações e Manutenção** que facilita a localização e instalação das atualizações recomendadas.  

 Algumas versões estão disponíveis apenas como atualizações para sites existentes (dentro do console do Configuration Manager) e não podem ser usadas para instalar novos sites do Configuration Manager.   
Por exemplo, a atualização 1610 está disponível apenas no console do Configuration Manager. Ele é usado para atualizar um site que já executa uma versão do System Center Configuration Manager.

Periodicamente, uma versão de atualização também é liberada como uma nova versão de linha de base (como a atualização 1606). Esse tipo de atualização pode ser usado para instalar uma nova hierarquia, sem a necessidade de iniciar com uma versão de linha de base mais antiga (como 1511) e atualizá-la para a versão mais atual.


Para obter mais informações sobre o uso de atualizações, consulte [Atualizações para o System Center Configuration Manager](../../../core/servers/manage/updates.md).  
Para mais informações sobre linhas de base, confira [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions).

##  <a name="bkmk_servicepoint"></a> Nova função do sistema de sites: ponto de conexão de serviço  
 O **conector do Microsoft Intune** é substituído por uma nova função de sistema de sites que habilita uma funcionalidade adicional, o **ponto de conexão de serviço**. O ponto de conexão de serviço:  

-   Substitui o conector do Microsoft Intune ao integrar o Intune ao gerenciamento de dispositivo móvel local do System Center Configuration Manager.  

-   É usado como um ponto de contato para os dispositivos gerenciados.  

-   Carrega dados de uso sobre a implantação para o serviço de nuvem da Microsoft.  

-   Disponibiliza atualizações que se aplicam à sua implantação no console do Configuration Manager.  

Essa função do sistema de sites dá suporte aos modos de operação online e offline. Para obter mais informações, consulte [About the service connection point in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

##  <a name="bkmk_usage"></a> Coleta de dados de uso  
 O System Center Configuration Manager coleta dados de uso sobre seus sites e sua infraestrutura. Essas informações são compiladas e enviadas ao serviço de nuvem da Microsoft pelo ponto de conexão de serviço. Elas são necessárias para permitir que o Configuration Manager baixe atualizações para sua implantação que se aplicam à versão utilizada do Configuration Manager. Ao configurar o ponto de conexão de serviço, é possível especificar o nível de dados coletados e se eles são enviados automática (modo online) ou manualmente (modo offline).  

 Para obter mais informações, consulte [Configurações e níveis de dados de uso](../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

##  <a name="bkmk_AMT"></a> Suporte para Intel AMT (Active Management Technology)  
 Com o System Center Configuration Manager, o suporte nativo para computadores baseados em AMT de dentro do console do Configuration Manager foi removido. Os computadores baseados em AMT permanecem totalmente gerenciados quando você usa o [Complemento Intel SCS para o Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). O uso do complemento fornece acesso aos recursos mais recentes para gerenciar o AMT e, ao mesmo tempo, remove as limitações introduzidas até que o Configuration Manager possa incorporar essas mudanças.  

A remoção do AMT integrado para o System Center Configuration Manager inclui o Gerenciamento Fora de Banda. A função do sistema de sites do ponto de Gerenciamento Fora de Banda não é mais usada nem está disponível.  

Observe que o Gerenciamento Fora de Banda no System Center 2012 Configuration Manager não é afetado por essa alteração.

##  <a name="bkmk_out"></a> Funcionalidade preterida  
 Algumas funcionalidades, como o [Suporte nativo para computadores baseados em Intel AMT (Active Management Technology)](#bkmk_AMT), foram removidas do console do Configuration Manager. Outras funcionalidades, como a Proteção de Acesso à Rede, foram totalmente removidas. Além disso, não há mais suporte para alguns produtos mais antigos da Microsoft como o Windows Vista, Windows Server 2008 e SQL Server 2008.  

 Para obter uma lista dos recursos preteridos, consulte [Recursos removidos e preteridos para o System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

 Para obter detalhes sobre configurações, sistemas operacionais e produtos com suporte, consulte [Configurações com suporte para o System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md).  

## <a name="client-deployment"></a>Implantação do cliente  
 O System Center Configuration Manager introduz uma nova funcionalidade para testar novas versões do cliente do Configuration Manager antes de atualizar o restante do site com o novo software. É possível configurar uma coleção de pré-produção na qual um novo cliente será testado como piloto. Quando estiver satisfeito com o novo software cliente em pré-produção, você poderá promover o cliente para atualizar o restante do site automaticamente com a nova versão.  

 Para obter mais informações sobre como testar clientes, consulte [Como testar atualizações do cliente em uma coleção de pré-produção no System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

## <a name="operating-system-deployment"></a>Implantação de sistema operacional  

Esteja ciente das seguintes alterações na implantação de sistema operacional:

-   No Assistente para Criar Sequência de Tarefas, **Atualizar um sistema operacional do pacote de atualização**, um novo tipo de sequência de tarefas está disponível. Ele cria as etapas para atualizar os computadores do Windows 7, Windows 8 ou Windows 8.1 para o Windows 10. Para obter mais informações, consulte [Upgrade Windows to the latest version with System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   O Cache par do Windows PE agora está disponível ao implantar sistemas operacionais. Os computadores que executam uma sequência de tarefas para implantar um sistema operacional podem usar o Cache Par do Windows PE para obter o conteúdo de um par local (uma fonte de cache par), em vez de baixar o conteúdo de um ponto de distribuição. Isso ajuda a minimizar o tráfego de WAN (rede de longa distância) em cenários de filial em que não há nenhum ponto de distribuição local. Para obter mais informações, consulte [Prepare Windows PE peer cache to reduce WAN traffic in System Center Configuration Manager](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic).  

-   Agora é possível exibir o estado do Windows como um serviço no ambiente. Também é possível criar planos de manutenção para formar anéis de implantação e garantir que os computadores com a ramificação atual do Windows 10 serão mantidos atualizados quando novos builds forem liberados. Além disso, é possível exibir alertas quando os clientes do Windows 10 estiverem próximos ao fim de suporte de seu build do CB (Branch Atual) ou CBB (Branch Atual para Empresas). Para obter mais informações, consulte [Manage Windows as a service using System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md).  

## <a name="application-management"></a>Gerenciamento de aplicativos  

Esteja ciente das seguintes alterações no gerenciamento de aplicativos:

-   O System Center Configuration Manager permite implantar aplicativos UWP (Plataforma Universal do Windows) para dispositivos que executam o Windows 10 e posterior. Consulte [Criando aplicativos do Windows com o System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   O Centro de Software traz uma aparência nova e moderna. Os aplicativos que anteriormente eram exibidos apenas no Catálogo de Aplicativos (aplicativos disponíveis para o usuário) agora são exibidos no Centro de Software na guia Aplicativos. Isso torna essas implantações mais detectáveis e elimina a necessidade de os usuários consultarem o Catálogo de Aplicativos. Além disso, um navegador habilitado do Silverlight não será mais necessário. Consulte [Planejar e configurar o gerenciamento de aplicativos no System Center Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   O novo tipo de aplicativo Windows Installer por meio do MDM permite criar e implantar aplicativos baseados no Windows Installer em computadores registrados que executam o Windows 10. Consulte [Criando aplicativos do Windows com o System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   Ao criar um aplicativo para um aplicativo iOS internamente, você precisa apenas especificar o arquivo do instalador (.ipa) para o aplicativo. Não é mais necessário especificar um arquivo de lista de propriedade (.plist) correspondente. Consulte [Criando aplicativos iOS com o System Center Configuration Manager](../../../apps/get-started/creating-ios-applications.md).  

-   No Configuration Manager 2012, para especificar um link para um aplicativo na Windows Store, é possível especificar o link diretamente ou navegar até um computador remoto que tem o aplicativo instalado. No System Center Configuration Manager, ainda é possível inserir o link diretamente, mas agora, em vez de acessar um computador de referência, você pode procurar o aplicativo diretamente na loja por meio do console do Configuration Manager.  

## <a name="software-updates"></a>Atualizações de software  

Esteja ciente das seguintes alterações nas atualizações de software:

-   O System Center Configuration Manager agora pode detectar a diferença entre métodos de gerenciamento de atualização de software em computadores. Especificamente, ele pode diferenciar entre um computador Windows 10 que se conecta ao WUfB (Windows Update para Empresas) para o gerenciamento de atualizações de software e um computador conectado ao WSUS (Windows Server Update Services) para o gerenciamento de atualizações de software. O atributo **UseWUServer** é novo e especifica se o computador é gerenciado com o WUfB. É possível usar essa configuração em uma coleção para remover esses computadores do gerenciamento de atualizações de software. Para obter mais informações, consulte [Integration with Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

-   Agora é possível agendar e executar a tarefa de limpeza do WSUS no console do Configuration Manager. Nas propriedades do **Componente de Ponto de Atualização de Software**, ao selecionar para executar a tarefa de limpeza do WSUS, ela será executada na próxima sincronização de atualizações de software. As atualizações expiradas do software serão definidas com o status de recusadas no servidor WSUS e o Windows Update Agent nos computadores não examinará mais essas atualizações de software. Para obter mais informações, consulte [Schedule and run the WSUS clean up task](../../../sum/deploy-use/software-updates-maintenance.md).  

## <a name="compliance-settings"></a>Configurações de conformidade  

Esteja ciente das seguintes alterações nas configurações de conformidade:

-   O System Center Configuration Manager melhora o fluxo de trabalho para a criação de itens de configuração. Agora, ao criar um item de configuração e selecionar as plataformas com suporte, apenas as configurações relevantes para essa plataforma estarão disponíveis. Consulte [Introdução às configurações de conformidade no System Center Configuration Manager](../../../compliance/get-started/get-started-with-compliance-settings.md).  

-   O assistente **Criar Item de Configuração** agora facilita a escolha do tipo de item de configuração que você deseja criar. Além disso, itens de configuração novos e atualizados estão disponíveis para:  

    -   Dispositivos Windows 10 gerenciados com o cliente do Configuration Manager.  

    -   Dispositivos Mac OS X gerenciados com o cliente do Configuration Manager.  

    -   Computadores desktop e de servidor Windows gerenciados com o cliente do Configuration Manager.  

    -   Dispositivos Windows 8.1 e Windows 10 gerenciados sem o cliente do Configuration Manager.  

    -   Dispositivos Windows Phone gerenciados sem o cliente do Configuration Manager.  

    -   Dispositivos iOS e Mac OS X gerenciados sem o cliente do Configuration Manager.  

    -   Dispositivos Android e Samsung KNOX Standard gerenciados sem o cliente do Configuration Manager.  

 Consulte [Como criar itens de configuração no System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items.md).  

-   Suporte para o gerenciamento de configurações em computadores Mac OS X que são registrados no Microsoft Intune ou gerenciados usando o cliente do Configuration Manager. Consulte [Como criar itens de configuração para dispositivos iOS e Mac OS X gerenciados sem o cliente do System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md).  

## <a name="protect-data-and-site-infrastructure"></a>Proteger a infraestrutura de dados e do site  
O System Center Configuration Manager permite a integração ao Windows Hello para Empresas (anteriormente conhecido como Microsoft Passport for Work). O Windows Hello para Empresas é um método de conexão alternativo que usa o Active Directory ou uma conta do Azure Active Directory, para substituir uma senha, um cartão inteligente ou um cartão inteligente virtual em dispositivos que executam o Windows 10. Consulte [Windows Hello for Business settings in System Center Configuration Manager](../../../protect/deploy-use/windows-hello-for-business-settings.md) (Configurações do Windows Hello for Business no System Center Configuration Manager).

## <a name="mobile-device-management-with-microsoft-intune"></a>Gerenciamento de dispositivo móvel com o Microsoft Intune  
 O System Center Configuration Manager introduz melhorias à experiência de gerenciamento de dispositivo móvel, incluindo:  

-   Limitar o número de dispositivos que um usuário pode registrar.  

-   Especificar os termos e condições que os usuários do Portal da Empresa devem aceitar antes de registrar ou usar o aplicativo.  

-   Adicionar uma função do gerenciador de registro do dispositivo para ajudar a gerenciar um grande número de dispositivos.  

Para obter mais informações sobre recursos de gerenciamento de dispositivos móveis com o Configuration Manager e o Intune, consulte [MDM (gerenciamento de dispositivo móvel) híbrido com o System Center Configuration Manager e o Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

## <a name="on-premises-mobile-device-management"></a>Gerenciamento de dispositivo móvel local  
 Agora é possível gerenciar dispositivos móveis usando a infraestrutura local do Configuration Manager. Todo o gerenciamento de dispositivos e todos os dados de gerenciamento são manipulados localmente e não fazem parte do Microsoft Intune nem de outros serviços de nuvem. Esse tipo de gerenciamento de dispositivos não exige software cliente. O Configuration Manager gerencia dispositivos com funcionalidades internas dos sistemas operacionais dos dispositivos.  

 Para saber mais, consulte [Gerenciar dispositivos móveis com a infraestrutura local no System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

