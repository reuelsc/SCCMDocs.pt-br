---
title: "Mudanças do Configuration Manager 2012 | System Center Configuration Manager "
description: "Identifique as mudanças e os novos recursos do System Center Configuration Manager com relação ao System Center 2012 Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0f3b68fb17920b0abacc1428c8763ec8c06e6b22


---
# <a name="what39s-changed-in-system-center-configuration-manager-from-system-center-2012-configuration-manager"></a>O que mudou no System Center Configuration Manager com relação ao System Center 2012 Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


 O branch atual do System Center Configuration Manager introduz mudanças importantes com relação ao System Center 2012 Configuration Manager. As informações neste tópico identificam as mudanças e novos recursos mais significativos encontrados na versão de linha de base 1511 do System Center Configuration Manager. Para saber mais sobre as mudanças adicionais introduzidas nas atualizações posteriores do System Center Configuration Manager, consulte [Novidades nas versões incrementais do System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).



 A versão de dezembro de 2015 do System Center Configuration Manager (versão 1511) é a versão de produto mais recente do Configuration Manager da Microsoft.   Normalmente, é chamada de branch atual do System Center Configuration Manager. *Branch atual* indica que esta é uma versão que dá suporte a atualizações incrementais do produto e pode ser uma distinção importante entre esta versão e versões anteriores do Configuration Manager.  

 Notas de versão do System Center Configuration Manager:  

-   Não usa um identificador de produto ou ano no nome do produto, como visto nas versões anteriores, como Configuration Manager 2007 ou System Center 2012 Configuration Manager.

-   Dá suporte a atualizações incrementais no produto, também chamadas de versões de atualização. A versão de inicial é a 1511. Versões subsequentes são lançadas várias vezes no ano como atualizações no console, como a versão 1602 ou 1606.




##  <a name="a-namebkmkupdatesa-in-console-updates-for-configuration-manager"></a><a name="bkmk_updates"></a> Atualizações no console para o Configuration Manager  
 O System Center Configuration Manager usa um método de serviço no console chamado **Atualizações e Manutenção** que facilita a localização e a instalação das atualizações recomendadas para o Configuration Manager.  

 Algumas versões estão disponíveis apenas como atualizações para sites existentes (dentro do console do Configuration Manager) e não podem ser usadas para instalar novos sites do Configuration Manager.   
Por exemplo, a atualização 1602 está disponível somente do console do Configuration Manager e é usada para atualizar um site que executa uma versão de linha de base do 1511 para o 1602.  

Periodicamente, uma versão de atualização também é lançada como uma nova versão de linha de base (como a atualização 1606), que pode ser usada para instalar uma nova hierarquia sem a necessidade de começar com uma versão mais antiga da linha de base (como a 1511) e atualizar até chegar à versão mais atual.


 Para obter mais informações sobre o uso de atualizações, consulte [Atualizações para o System Center Configuration Manager](../../../core/servers/manage/updates.md).  

##  <a name="a-namebkmkservicepointa-service-connection-point-replaces-microsoft-intune-connector"></a><a name="bkmk_servicepoint"></a> O ponto de conexão de serviço substitui o conector do Microsoft Intune  
 O **conector do Microsoft Intune** é substituído por uma nova função de sistema de sites que habilita uma funcionalidade adicional, o **ponto de conexão de serviço**. O ponto de conexão de serviço:  

-   Substitui o conector do Microsoft Intune quando você integra o Intune ao Gerenciamento de Dispositivo Móvel local do System Center Configuration Manager  

-   É usado como ponto de contato para dispositivos gerenciados com  

-   Carrega dados de uso sobre sua implantação para o serviço de nuvem da Microsoft  

-   Faz atualizações que se aplicam à sua implantação disponível de dentro do console do Configuration Manager  

Essa função de sistema de sites dá suporte aos modos online e offline de operação, o que pode afetar seu uso adicional. Para obter mais informações, consulte [Sobre o ponto de conexão de serviço no System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

##  <a name="a-namebkmkusagea-usage-data-collection"></a><a name="bkmk_usage"></a> Coleta de dados de uso  
 O System Center Configuration Manager coleta dados de uso sobre seus sites e sua infraestrutura. Essas informações são compiladas e enviadas ao serviço de nuvem da Microsoft pelo ponto de conexão de serviço (uma nova função do sistema de sites) e são necessárias para permitir que o Configuration Manager baixe atualizações para sua implantação que se aplicam à versão do Configuration Manager utilizada. Ao configurar o ponto de conexão de serviço, é possível configurar o nível de dados que são coletados e se eles são enviados automática (modo online) ou manualmente (modo offline).  

 Para obter mais informações, consulte [Usage data levels and settings](../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

##  <a name="a-namebkmkamta-support-for-intel-active-management-technology-amt"></a><a name="bkmk_AMT"></a> Suporte para Intel AMT (Active Management Technology)  
 Com o System Center Configuration Manager, o suporte nativo para computadores baseados em AMT de dentro do console do Configuration Manager foi removido.  

-   Os computadores baseados em AMT permanecem totalmente gerenciados, quando você usa o [Complemento Intel SCS para o Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)  

-   O uso do complemento fornece acesso aos recursos mais recentes para gerenciar o AMT, ao mesmo tempo em que remove limitações introduzidas até que o Configuration Manager pudesse incorporar essas mudanças  

-   O Gerenciamento fora de banda no System Center 2012 Configuration Manager não é afetado por essa alteração  

A remoção do AMT integrado para o System Center Configuration Manager inclui:  

-   A função do sistema de sites de ponto de gerenciamento fora de banda não é mais usada nem está disponível  

##  <a name="a-namebkmkouta-deprecated-functionality"></a><a name="bkmk_out"></a> Funcionalidade preterida  
 Com o System Center Configuration Manager, alguns recursos, como computadores baseados no [Suporte para Intel AMT (Active Management Technology)](#bkmk_AMT) nativo, foram removidos do console do Configuration Manager, enquanto outros recursos, como a Proteção de Acesso à Rede, foram removidos por completo. Além disso, não há mais suporte para alguns produtos mais antigos da Microsoft como o Windows Vista, Windows Server 2008 e SQL Server 2008.  

 Para obter uma lista dos recursos preteridos, consulte [Recursos removidos e preteridos para o System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

 Para obter detalhes sobre configurações, sistemas operacionais e produtos com suporte, consulte [Configurações com suporte para o System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md).  

## <a name="client-deployment"></a>Implantação do cliente  
 O System Center Configuration Manager apresenta uma nova funcionalidade para testar novas versões do cliente do Configuration Manager antes de atualizar o restante do site com o novo software.  Essa nova funcionalidade oferece a oportunidade de configurar uma coleção de pré-produção na qual é possível fazer um piloto de um novo cliente. Quando estiver satisfeito com o novo software cliente na pré-produção, é possível promover o cliente para atualizar automaticamente o restante do site com a nova versão.  

 Para obter mais informações sobre como testar clientes, consulte [Como testar atualizações do cliente em uma coleção de pré-produção no System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

## <a name="operating-system-deployment"></a>Implantação de sistema operacional  

-   Um novo tipo de sequência de tarefas está disponível no Assistente para Criar Sequência de Tarefas,  **Atualizar um sistema operacional do pacote de atualização**, que cria as etapas para atualizar os computadores do Windows 7, Windows 8 ou Windows 8.1 para o Windows 10.  Para obter mais informações, consulte [Upgrade Windows to the latest version with System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   O Cache par do Windows PE agora está disponível ao implantar sistemas operacionais. Os computadores que executam uma sequência de tarefas para implantar um sistema operacional podem usar o Cache de sistemas pares do Windows PE para obter o conteúdo de um par local (uma fonte de cache de sistemas pares), em vez de baixar o conteúdo de um ponto de distribuição. Isso ajuda a minimizar o tráfego de WAN (rede de longa distância) em cenários de filial em que não há nenhum ponto de distribuição local. Para obter mais informações, consulte [Prepare Windows PE peer cache to reduce WAN traffic in System Center Configuration Manager](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic).  

-   Agora é possível exibir o estado do Windows como Serviço em seu ambiente, criar planos de serviço para formar anéis de implantação e garantir que os computadores com o branch atual do Windows 10 permanecem atualizados quando novos builds forem liberados; além disso, é possível exibir alertas quando os clientes Windows 10 estiverem próximos do fim do suporte de seu build do CB (Branch Atual) ou do CBB (Branch Atual para Negócios). Para obter mais informações, consulte [Manage Windows as a service using System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md).  

## <a name="application-management"></a>Gerenciamento de aplicativos  

-   O System Center Configuration Manager permite implantar aplicativos UWP (Plataforma Universal do Windows) para dispositivos que executam o Windows 10 e posterior. Consulte [Criando aplicativos do Windows com o System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   O Centro de Software tem uma aparência nova e moderna, e os aplicativos que antes só eram exibidos no Catálogo de Aplicativos (aplicativos disponíveis para o usuário) agora aparecem no Centro de Software sob a guia Aplicativos. Isso torna essas implantações mais detectáveis para os usuários e elimina a necessidade de usar o catálogo de aplicativos. Além disso, um navegador habilitado do Silverlight não será mais necessário. Consulte [Planejar e configurar o gerenciamento de aplicativos no System Center Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   O novo tipo de aplicativo Windows Installer por meio do MDM permite criar e implantar aplicativos baseados no Windows Installer em computadores registrados que executam o Windows 10. Consulte [Criando aplicativos do Windows com o System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   Ao criar um aplicativo para um aplicativo iOS internamente, você precisa apenas especificar o arquivo do instalador (.ipa) para o aplicativo. Não é mais necessário especificar um arquivo de lista de propriedade (.plist) correspondente. Consulte [Criando aplicativos iOS com o System Center Configuration Manager](../../../apps/get-started/creating-ios-applications.md).  

-   No Configuration Manager 2012, para especificar um link para um aplicativo na Windows Store, é possível especificar o link diretamente ou navegar até um computador remoto que tem o aplicativo instalado. No System Center Configuration Manager, ainda é possível inserir o link diretamente, mas agora, em vez de navegar até um computador de referência, você pode procurar o aplicativo diretamente na loja usando o console do Configuration Manager.  

## <a name="software-updates"></a>Atualizações de software  

-   Agora, o System Center Configuration Manager diferencia um computador com Windows 10 que se conecta ao WUfB (Windows Update for Business) para o gerenciamento de atualizações de software em comparação com os computadores conectados ao WSUS para o gerenciamento de atualizações de software. O atributo **UseWUServer** é novo e especifica se o computador é gerenciado com o WUfB. É possível usar essa configuração em uma coleção para remover esses computadores do gerenciamento de atualizações de software. Para obter mais informações, consulte [Integration with Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

-   Agora, é possível agendar e executar a tarefa de limpeza do WSUS no console do Configuration Manager.  
    Agora você pode executar a tarefa de limpeza do WSUS manualmente nas propriedades do Componente do ponto de atualização de software. Quando você seleciona para executar a tarefa de limpeza do WSUS, ela será executada na próxima sincronização de atualizações de software. As atualizações expiradas do software serão definidas com o status de recusadas no servidor WSUS, e o Windows Update Agent nos computadores não verificará mais essas atualizações de software. Para obter mais informações, consulte [Schedule and run the WSUS clean up task](../../../sum/deploy-use/software-updates-maintenance.md).  

## <a name="compliance-settings"></a>Configurações de conformidade  

-   O System Center Configuration Manager introduz um fluxo de trabalho aperfeiçoado para a criação de itens de configuração. Agora, ao criar um item de configuração e selecionar as plataformas com suporte, apenas as configurações relevantes para essa plataforma estarão disponíveis. Consulte [Introdução às configurações de conformidade no System Center Configuration Manager](../../../compliance/get-started/get-started-with-compliance-settings.md).  

-   O assistente de criação de item de configuração agora facilita a escolha do tipo de item de configuração que você deseja criar. Além disso, itens de configuração novos e atualizados estão disponíveis para:  

    -   Dispositivos Windows 10 gerenciados com o cliente do Configuration Manager  

    -   Dispositivos Mac OS X gerenciados com o cliente do Configuration Manager  

    -   Computadores desktop e de servidor com Windows gerenciados com o cliente do Configuration Manager  

    -   Dispositivos Windows 8.1 e Windows 10 gerenciados sem o cliente do Configuration Manager  

    -   Dispositivos Windows Phone gerenciados sem o cliente do Configuration Manager  

    -   Dispositivos iOS e Mac OS X gerenciados sem o cliente do Configuration Manager  

    -   Dispositivos Android e Samsung KNOX gerenciados sem o cliente do Configuration Manager  

     Consulte [Como criar itens de configuração no System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items.md).  

-   Suporte para o gerenciamento de configurações em computadores Mac OS X que são registrados no Microsoft Intune ou gerenciados usando o cliente do Configuration Manager. Consulte [Como criar itens de configuração para dispositivos iOS e Mac OS X gerenciados sem o cliente do System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md).  

## <a name="protect-data-and-site-infrastructure"></a>Proteger a infraestrutura de dados e do site  
-   O System Center Configuration Manager permite a integração com o Windows Hello para Empresas (anteriormente, Microsoft Passport for Work), que é um método de entrada alternativo que usa o Active Directory ou uma conta do Azure Active Directory para substituir uma senha, cartão inteligente ou cartão inteligente virtual em dispositivos que executam o Windows 10. Consulte [Windows Hello for Business settings in System Center Configuration Manager](../../../protect/deploy-use/windows-hello-for-business-settings.md) (Configurações do Windows Hello for Business no System Center Configuration Manager).

## <a name="mobile-device-management-with-microsoft-intune"></a>Gerenciamento de dispositivo móvel com o Microsoft Intune  
 O System Center Configuration Manager introduz melhorias à experiência de gerenciamento de dispositivo móvel, incluindo:  

-   Limitar o número de dispositivos que um usuário pode registrar  

-   Especificar os termos e condições que os usuários do Portal da Empresa devem aceitar antes de registrar ou usar o aplicativo  

-   Adicionada uma função do gerenciador de registro de dispositivo para ajudar a gerenciar um grande número de dispositivos  

Para obter mais informações sobre recursos de gerenciamento de dispositivos móveis com o Configuration Manager e o Intune, consulte [MDM (gerenciamento de dispositivo móvel) híbrido com o System Center Configuration Manager e o Microsoft Intune](../../../mdm/plan-design/hybrid-mobile-device-management.md).  

## <a name="on-premises-mobile-device-management"></a>Gerenciamento de dispositivo móvel local  
 Com o System Center Configuration Manager, agora você pode gerenciar dispositivos móveis usando a infraestrutura local do Configuration Manager. Todo o gerenciamento de dispositivo e todos os dados de gerenciamento são processados localmente e não fazem parte do Microsoft Intune ou de outros serviços de nuvem. Esse tipo de gerenciamento de dispositivo não exige software cliente, uma vez que os recursos usados pelo Configuration Manager para gerenciar os dispositivos são internos aos sistemas operacionais dos dispositivos.  

 Para saber mais, consulte [Gerenciar dispositivos móveis com a infraestrutura local no System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).



<!--HONumber=Nov16_HO1-->


