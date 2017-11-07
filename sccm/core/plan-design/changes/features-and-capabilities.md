---
title: Recursos e funcionalidades
titleSuffix: Configuration Manager
description: "Saiba mais sobre os recursos de gerenciamento primário do System Center Configuration Manager."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
caps.latest.revision: "18"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: c9b6720d08260c7a2a06e0ccc525228e5089b279
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="features-and-capabilities-of-system-center-configuration-manager"></a>Recursos e funcionalidades do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os seguintes são os recursos de gerenciamento primário do System Center Configuration Manager. Cada funcionalidade tem seus próprios pré-requisitos, e os recursos que você deseja usar podem influenciar o design e a implementação da hierarquia do Configuration Manager. Por exemplo, se você deseja implantar o software em dispositivos na hierarquia, você deve instalar a função do sistema de site do ponto de distribuição.  

 Para obter mais informações sobre como planejar e instalar o Configuration Manager para dar suporte a esses recursos de gerenciamento em seu ambiente, consulte [Prepare-se para o System Center Configuration Manager](../../../core/plan-design/get-ready.md).  

 **Gerenciamento de aplicativo**  

 Fornece um conjunto de ferramentas e recursos que podem ajudá-lo a criar, gerenciar, implantar e monitorar aplicativos para uma variedade de dispositivos diferentes gerenciados. Além disso, o Configuration Manager fornece ferramentas que o ajudarão a proteger os dados de sua empresa em aplicativos do usuário. Consulte [Introdução ao gerenciamento de aplicativos](/sccm/apps/understand/introduction-to-application-management).

 **Acesso de recursos da empresa**  

 Fornece um conjunto de ferramentas e recursos que permitem que você conceda acesso a usuários da sua organização a dados e aplicativos de locais remotos. Essas ferramentas incluem perfis de Wi-Fi, perfis de VPN, perfis de certificado e acesso condicional ao Exchange e SharePoint online. Consulte [Proteger a infraestrutura de dados e do site com o System Center Configuration Manager](../../../protect/understand/protect-data-and-site-infrastructure.md) e [Gerenciar o acesso a serviços no System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-services.md).  

 **Configurações de conformidade**  

 Fornece um conjunto de ferramentas e recursos que podem ajudar a avaliar, acompanhar e corrigir a conformidade de configuração de dispositivos de clientes na empresa. Além disso, é possível usar as configurações de conformidade para definir uma variedade de recursos e configurações de segurança nos dispositivos gerenciados. Consulte [Ensure device compliance with System Center Configuration Manager (Garantir a conformidade do dispositivo com o System Center Configuration Manager)](../../../compliance/understand/ensure-device-compliance.md).  

 **Endpoint Protection**  

 Fornece segurança, antimalware e gerenciamento do Firewall do Windows para computadores na empresa. Consulte [Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

 **Inventário**  

 Fornece um conjunto de ferramentas para ajudar a identificar e monitorar ativos:  

-   **Inventário de hardware**: coleta informações detalhadas sobre o hardware dos dispositivos na empresa. Consulte [Introdução ao inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-hardware-inventory.md).  

-   **Inventário de software**: coleta e relata informações sobre os arquivos que são armazenados nos computadores cliente na organização. Consulte [Introdução ao inventário de software no System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-software-inventory.md).  

-   **Asset Intelligence**: fornece ferramentas para coletar dados de inventário e para monitorar o uso de licença de software na empresa. Consulte [Introdução ao Asset Intelligence no System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

**Gerenciamento de dispositivo móvel com o Microsoft Intune**  

 É possível usar o Configuration Manager para gerenciar dispositivos iOS, Android (incluindo Samsung KNOX Standard), Windows Phone e Windows usando o serviço do Microsoft Intune pela Internet.

 Apesar de você usar o serviço do Intune, as tarefas de gerenciamento são concluídas usando a função do sistema de sites do ponto de conexão do serviço disponível por meio do console do Configuration Manager. Consulte [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune (MDM (Gerenciamento de dispositivo móvel) híbrido com o System Center Configuration Manager e Microsoft Intune)](../../../mdm/understand/hybrid-mobile-device-management.md).  

 **Gerenciamento de dispositivo móvel local**  

 Registra e gerencia computadores e dispositivos móveis usando a funcionalidade de gerenciamento e infraestrutura local do Configuration Manager incorporada às plataformas de dispositivo (em vez de se basear em um cliente do Configuration Manager instalado separadamente). Atualmente, dá suporte ao gerenciamento de dispositivos Windows 10 Enterprise e Windows 10 Mobile. Consulte [Gerenciar dispositivos móveis com a infraestrutura local no System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

 **Implantação do sistema operacional**  

 Fornece uma ferramenta para criar imagens do sistema operacional. Você pode usar essas imagens para implantar os sistemas operacionais em computadores, usando a inicialização PXE ou mídias inicializáveis como um conjunto de CD, DVD ou unidades flash USB. Observe que isso se aplica a computadores que são gerenciados pelo Configuration Manager, bem como a computadores não gerenciados. Consulte [Introdução à implantação de sistema operacional no System Center Configuration Manager](../../../osd/understand/introduction-to-operating-system-deployment.md).  

 **Gerenciamento de energia**  

 Fornece um conjunto de ferramentas e recursos que podem ajudar a gerenciar e monitorar o consumo de energia de computadores cliente na empresa. Consulte [Introdução ao gerenciamento de energia no System Center Configuration Manager](../../../core/clients/manage/power/introduction-to-power-management.md).  

 **Consultas**  

 Fornece uma ferramenta para recuperar informações sobre recursos na hierarquia e informações sobre dados de inventário e mensagens de status. É possível usar essas informações para relatórios ou para definir coleções de dispositivos ou de usuários para implantação de software e definições de configuração. Consulte [Introdução a consultas no System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md).  

 **Perfis de conexão remota**  

 Fornece um conjunto de ferramentas e recursos para ajudá-lo a criar, implantar e monitorar configurações de conexão remota em dispositivos na sua organização. Ao implantar essas configurações, você minimiza o esforço exigido dos usuários para se conectar aos computadores na rede corporativa. Consulte [Trabalhando com perfis de conexão remota no System Center Configuration Manager](/sccm/compliance/deploy-use/create-remote-connection-profiles).  

 **Itens de configuração de perfis e dados do usuário**  

 Os itens de configuração de perfis e dados do usuário no Configuration Manager contêm definições que podem gerenciar o redirecionamento de pasta, arquivos offline e perfis móveis em computadores que executam o Windows 8 e posterior para usuários em sua hierarquia. Consulte [Trabalhando com itens de configuração de perfis e dados de usuário no System Center Configuration Manager](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items).  

 **Controle remoto**  

 Fornece ferramentas para administrar remotamente computadores cliente no console do Configuration Manager. Consulte [Introdução ao controle remoto no System Center Configuration Manager](../../../core/clients/manage/remote-control/introduction-to-remote-control.md).  

 **Relatórios**  

 Fornece um conjunto de ferramentas e recursos que ajudam a usar os recursos de relatórios avançados do SQL Server Reporting Services no console do Configuration Manager. Consulte [Introdução à emissão de relatórios no System Center Configuration Manager](../../../core/servers/manage/introduction-to-reporting.md).  

 **Medição de software**  

 Fornece ferramentas para monitorar e coletar dados de uso de software de clientes do Configuration Manager. Consulte [Monitorar o uso de aplicativos com a medição de software no System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

 **Atualizações de software**  

 Fornece um conjunto de ferramentas e recursos que podem ajudar a gerenciar, implantar e monitorar atualizações de software na empresa. Consulte [Introdução às atualizações de software no System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction).  
