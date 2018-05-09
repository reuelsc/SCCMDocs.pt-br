---
title: 'Escolher uma solução de gerenciamento de dispositivo '
titleSuffix: Configuration Manager
description: Saiba mais sobre as soluções oferecidas pelo System Center Configuration Manager para gerenciar computadores, servidores e dispositivos.
ms.date: 12/08/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 616bf5549c80c94b1dd5d27dc15ea693c86e2ca2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="choose-a-device-management-solution-for-system-center-configuration-manager"></a>Escolher uma solução de gerenciamento de dispositivo para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager (também conhecido como ConfgMgr ou SCCM) oferece soluções diferentes para o gerenciamento de computadores, de servidores e de dispositivos. Você pode escolher a solução certa para você com base nas plataformas de dispositivos que você precisa gerenciar e na funcionalidade de gerenciamento que você precisa.  


##  <a name="overview-of-device-management-solutions"></a>Visão geral das soluções de gerenciamento de dispositivo  
 Este artigo aborda quatro soluções de gerenciamento de dispositivo: o aplicativo cliente do Configuration Manager, a infraestrutura local do Configuration Manager, o Microsoft Intune e o Exchange. O artigo é concluído com duas tabelas que comparam as soluções de gerenciamento: uma com base nas [plataformas de dispositivos móveis com suporte](#compare-device-management-solutions-based-on-supported-mobile-device-platforms) e a outra com base na [funcionalidade de gerenciamento](#compare-mobile-device-management-solutions-based-on-management-functionality).


###  <a name="manage-devices-with-the-configuration-manager-client"></a>Gerenciar dispositivos com o cliente do Configuration Manager  

Essa opção, que exige a instalação do aplicativo cliente do Configuration Manager em todos os dispositivos, fornece a maioria dos recursos para gerenciar computadores, servidores e outros dispositivos em seu ambiente. Para mais informações, consulte [Métodos de instalação do cliente no System Center Configuration Manager](/sccm/core/clients/deploy/plan/client-installation-methods).  

###  <a name="manage-devices-with-on-premises-configuration-manager-infrastructure"></a>Gerenciar dispositivos com a infraestrutura local do Configuration Manager  

Essa opção usa os recursos de gerenciamento de dispositivo internos dos sistemas operacionais de algumas plataformas de dispositivo. Embora não seja tão completo quanto o gerenciamento baseado em cliente, o gerenciamento de dispositivo móvel local fornece uma abordagem mais leve de gerenciamento que usa recursos locais do Configuration Manager para acessar e gerenciar dispositivos. Observe que há suporte para essa opção somente nos computadores Windows 10 e nos dispositivos Windows 10 Mobile.  

Para obter mais informações, consulte [Gerenciar dispositivos móveis com infraestrutura local no System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

###  <a name="manage-devices-with-microsoft-intune-hybrid"></a>Gerenciar dispositivos com o Microsoft Intune (híbrido)  

Essa opção usa o Microsoft Intune para registrar e gerenciar dispositivos em vez de usar os recursos locais do Configuration Manager. Embora o Intune gerencie os dispositivos, você acessa suas tarefas de gerenciamento no console do Configuration Manager. Essa opção dá suporte a todos os principais sistemas de operacionais de dispositivos móveis, incluindo Windows 10 Mobile, Windows Phone, iOS, Mac OS X e Android. Ela também fornece gerenciamento de computadores com Windows 8.1 e Windows 10 em sua organização.  

Para obter mais informações, consulte [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../mdm/understand/hybrid-mobile-device-management.md) (MDM [gerenciamento de dispositivo móvel] híbrido com o System Center Configuration Manager e o Microsoft Intune).  

###  <a name="manage-devices-with-microsoft-exchange"></a>Gerenciar dispositivos com o Microsoft Exchange  

Essa opção usa o conector do Exchange Server para conectar vários servidores Exchange ao Configuration Manager. Com isso, o gerenciamento dos dispositivos que podem se conectar ao Exchange ActiveSync é centralizado. Você pode configurar os recursos de gerenciamento de dispositivo móvel do Exchange, como o apagamento remoto de dados no dispositivo e o controle de configurações para vários servidores Exchange, no console do Configuration Manager.  

Para obter mais informações, consulte [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

Use essas soluções de gerenciamento de dispositivo sozinhas ou combinadas umas com as outras. Por exemplo, é possível usar a abordagem de gerenciamento baseada em cliente para gerenciar computadores e servidores em sua organização e também usar o Intune para gerenciar dispositivos móveis. Ao combinar as abordagens dessa forma, é possível atender a todas as suas necessidades de gerenciamento de dispositivo no console do Configuration Manager.  

## <a name="compare-device-management-solutions-based-on-supported-mobile-device-platforms"></a>Comparar as soluções de gerenciamento de dispositivo móvel com base nas plataformas de dispositivos móveis com suporte  

|Plataforma|Com o cliente do Configuration Manager|Configuration Manager com Microsoft Intune (híbrido)|Gerenciamento de dispositivo móvel local|Configuration Manager com Exchange|  
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

##  <a name="bkmk_comp2"></a> Compare as soluções de gerenciamento de dispositivo móvel baseadas na funcionalidade de gerenciamento  

|Funcionalidade de gerenciamento|Com o cliente do Configuration Manager|Configuration Manager com Microsoft Intune (híbrido)|Gerenciamento de dispositivo móvel local|Configuration Manager com Exchange|  
|------------------------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Segurança de PKI (infraestrutura de chave pública) entre o dispositivo móvel e o Configuration Manager (usa autenticação mútua e SSL para criptografar transferências de dados)|Sim|Sim|Sim||  
|Instalação do cliente|Sim||||  
|Suporte pela Internet|Sim||||  
|Descoberta|Sim|||Sim|  
|Inventário de hardware|Sim|Sim|Sim|Sim|  
|Inventário de software|Sim|||Sim|  
|Configurações|Sim|Sim|Sim|Sim|  
|Implantação de software|Sim|Sim|Sim||  
|Monitor com ponto de status de fallback|Sim||||  
|Conexões para pontos de gerenciamento|Sim||Sim||  
|Conexões para pontos de distribuição|Sim||Sim||  
|Bloqueio do Configuration Manager|Sim|Sim|Sim||  
|Quarentena e bloqueio do Exchange Server (e Configuration Manager)||||Sim|  
|Apagamento remoto| |Sim|Sim|Sim|  
