---
title: "Escolher uma solução de gerenciamento de dispositivo para o System Center Configuration Manager"
description: "Saiba mais sobre as soluções oferecidas pelo System Center Configuration Manager para gerenciar computadores, servidores e dispositivos."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
caps.latest.revision: 14
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b64135826dd49c594167999aebd322fa3ed61345


---
# <a name="choose-a-device-management-solution-for-system-center-configuration-manager"></a>Escolher uma solução de gerenciamento de dispositivo para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager oferece soluções diferentes para o gerenciamento de computadores, servidores e dispositivos. Você pode escolher a solução certa para você com base em plataformas de dispositivos que você precisa gerenciar e a funcionalidade de gerenciamento que você precisa.  


##  <a name="a-namebkmkoverviewa-overview-of-device-management-solutions"></a><a name="bkmk_overview"></a> Visão geral das soluções de gerenciamento de dispositivo  
 As seguintes opções estão disponíveis para gerenciar computadores e dispositivos com o Configuration Manager:  

-   **Gerenciando dispositivos com o cliente do Configuration Manager**  

     Essa opção, que requer a instalação do aplicativo cliente do Configuration Manager em todos os dispositivos a serem gerenciados, fornece a maioria dos recursos e funcionalidades para gerenciar computadores, servidores e outros dispositivos em seu ambiente. Essa opção é a maneira tradicional de o Configuration Manager fornecer gerenciamento de dispositivo em relação ao histórico do produto.  

     Para obter mais informações sobre essa solução, consulte [Métodos de instalação do cliente no System Center Configuration Manager](/sccm/core/client/deploy/plan/client-installation-methods).  

-   **Gerenciando dispositivos móveis com a infraestrutura local no Configuration Manager**  

     Essa opção usa os recursos de gerenciamento de dispositivo integrados aos sistemas operacionais de algumas plataformas de dispositivo. Embora não seja tão completo quanto o gerenciamento baseado em cliente, o Gerenciamento de Dispositivo Móvel Local fornece uma abordagem mais leve de gerenciamento que usa no recursos locais do Configuration Manager para acessar e gerenciar dispositivos. No momento, o Gerenciamento de Dispositivo Móvel Local somente tem suporte para computadores com Windows 10 e dispositivos com Windows 10 Mobile.  

     Para obter mais informações, sobre essa solução, consulte [Gerenciar dispositivos móveis com infraestrutura local no System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

-   **Gerenciando dispositivos móveis com o Microsoft Intune (híbrido)**  

     Essa opção é conhecida como gerenciamento de dispositivo móvel híbrido.  Ela usa o Microsoft Intune para registrar e gerenciar dispositivos em vez de usar os recursos de local do Configuration Manager. Embora o Intune gerencie os dispositivos, você controlar as tarefas de gerenciamento no console do Configuration Manager. Essa opção dá suporte a todos os principais sistemas de operacionais de dispositivos móveis, incluindo Windows 10 Mobile, Windows Phone, iOS e Android. Ela também fornece gerenciamento de computadores com Windows 8.1 e Windows 10 em sua organização.  

     Para obter mais informações sobre essa solução, consulte [MDM (Gerenciamento de Dispositivo Móvel) híbrido com o System Center Configuration Manager e o Microsoft Intune](../../mdm/plan-design/hybrid-mobile-device-management.md).  

-   **Gerenciando dispositivos móveis com o Exchange**  

     Essa opção, que usa o conector do Exchange Server para conectar vários servidores Exchange ao Configuration Manager, centraliza o gerenciamento de dispositivos que podem se conectar ao Exchange ActiveSync. É possível configurar os recursos de gerenciamento de dispositivo móvel do Exchange, como apagamento remoto de dados no dispositivo e controle de configurações para vários servidores Exchange, no console do Configuration Manager.  

     Para obter mais informações sobre esta solução, consulte [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)  

 Você pode usar essas soluções de gerenciamento de dispositivo sozinhas ou combinadas umas com as outras. Por exemplo, é possível usar a abordagem de gerenciamento baseada em cliente para abordar o gerenciamento de computadores e servidores em sua organização e também usar o gerenciamento baseado no Intune para abordar dispositivos móveis. Ao combinar as abordagens dessa forma, é possível atender todas as suas necessidades de gerenciamento de dispositivos e controlar tudo do console do Configuration Manager.  

##  <a name="a-namebkmkcomp1a-compare-device-management-solutions-based-on-supported-mobile-device-platforms"></a><a name="bkmk_comp1"></a> Comparar as soluções de gerenciamento de dispositivo móvel com base nas plataformas de dispositivos móveis com suporte  

|Plataforma|Com o cliente do Configuration Manager|Configuration Manager com Microsoft Intune (híbrido)|\-Gerenciamento de dispositivo móvel local|Configuration Manager com Exchange|  
|--------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Android||Sim||Sim|  
|iOS||Sim||Sim|  
|Mac OS X|Sim|||Sim|  
|UNIX/Linux|Sim|||Sim|  
|Windows 10|Sim|Sim|Sim|Sim|  
|Windows 10 Mobile||Sim|Sim|Sim|  
|Windows (versões anteriores)|Sim|Sim||Sim|  
|Windows CE|Sim (com cliente herdado de dispositivo móvel)|||Sim|  
|Windows Embedded|Sim||||  
|Windows Phone||Sim||Sim|  
|Windows Server|Sim|||Sim|  

 Para ver uma lista das plataformas com suporte, consulte [Sistemas operacionais com suporte para clientes e dispositivos para o System Center Configuration Manager](configs\supported-operating-systems-for-clients-and-devices.md).

##  <a name="a-namebkmkcomp2a-compare-mobile-device-management-solutions-based-on-management-functionality"></a><a name="bkmk_comp2"></a> Compare as soluções de gerenciamento de dispositivo móvel baseadas na funcionalidade de gerenciamento  

|Funcionalidade de gerenciamento|Com o cliente do Configuration Manager|Configuration Manager com Microsoft Intune (híbrido)|\-Gerenciamento de dispositivo móvel local|Configuration Manager com Exchange|  
|------------------------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Segurança de PKI (infraestrutura de chave pública) entre o dispositivo móvel e o Configuration Manager usando a autenticação mútua e o protocolo SSL para criptografar transferências de dados|Sim|Sim|Sim||  
|Instalação do cliente|Sim||||  
|Suporte pela Internet|Sim||||  
|Descoberta|Sim|||Sim|  
|Inventário de hardware|Sim|Sim|Sim|Sim|  
|Inventário de software|Sim|||Sim|  
|Configurações|Sim|Sim|Sim|Sim|  
|Implantação de software|Sim|Sim|Sim||  
|Monitor com ponto de status de fallback|Sim||||  
|Conexões para pontos de gerenciamento|Sim||Sim||  
|Conexões para pontos de distribuição|Sim|Sim|Sim||  
|Bloqueio do Configuration Manager|Sim|Sim|Sim||  
|Quarentena e bloqueio do Exchange Server (e Configuration Manager)||||Sim|  
|Apagamento remoto|Sim|Sim|Sim|Sim|  



<!--HONumber=Nov16_HO1-->


