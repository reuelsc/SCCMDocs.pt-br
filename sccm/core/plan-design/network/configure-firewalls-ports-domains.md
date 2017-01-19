---
title: "Firewalls e domínios | Microsoft Docs"
description: "Configurar firewalls, portas e domínios para preparar-se para comunicações do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: df0622164ae7784ccfedc0f4c3328c42c1d050c3


---
# <a name="configure-firewalls-ports-and-domains-for-system-center-configuration-manager"></a>Configurar firewalls, portas e domínios para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para preparar sua rede para dar suporte ao System Center Configuration Manager, planeje a configuração da infraestrutura, como firewalls, para passar as cominações usadas pelo Configuration Manager.  

|Consideração|Detalhes|  
|-------------------|-------------|  
|**Portas e protocolos** usados por diferentes funcionalidades do Configuration Manager. Algumas portas são necessárias, enquanto outros **Domínios e serviços** podem ser personalizados.|A maioria das comunicações do Configuration Manager usa portas comuns, como a porta 80 para HTTP ou 443 para comunicação HTTPS. No entanto, [algumas funções do sistema de sites dão suporte ao uso de sites personalizados](/sccm/core/plan-design/network/websites-for-site-system-servers) e portas personalizadas.<br /><br /> **Antes de implantar o Configuration Manager**, identifique as portas que você planeja usar e configure os firewalls devidamente.<br /><br /> **Mais tarde, se você precisar alterar uma porta** após instalar o Configuration Manager, não se esqueça de atualizar os firewalls nos dispositivos e a rede, além de alterar a configuração da porta de dentro do Configuration Manager.<br /><br /> Para obter mais informações, consulte: </br>- [Como configurar as portas de comunicação do cliente](../../../core/clients/deploy/configure-client-communication-ports.md) </br>- [Portas usadas no Configuration Manager](../../../core/plan-design/hierarchy/ports.md) </br>- [Requisitos de acesso à Internet para o ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls)|  
|**Domínios e serviços** que clientes e servidores do site talvez precisem acessar.|Os recursos do Configuration Manager podem exigir que clientes e servidores do site tenham acesso a serviços e domínios específicos na Internet, como o Windowsudpate.microsoft.com ou o serviço Microsoft Intune.<br /><br /> Se você usar o Microsoft Intune para gerenciar dispositivos móveis, também deverá configurar o acesso a [portas e domínios exigidos pelo Intune.](https://docs.microsoft.com/en-us/intune/get-started/network-infrastructure-requirements-for-microsoft-intune)|  
|**Servidores proxy** para servidores de sistema de sites e para comunicações do cliente. Você pode especificar servidores proxy separados para clientes e servidores de sistema de sites diferentes.|Como essas configurações são feitas quando você instala uma função de sistema de sites ou cliente, você só precisar tomar conhecimento das configurações do servidor proxy para referência futura ao configurar funções de sistemas de sites e clientes.<br /><br /> Se você não tiver certeza se sua implantação precisará usar servidores proxy, examine [Suporte ao servidor proxy no System Center Configuration Manager](../../../core/plan-design/network/proxy-server-support.md) para saber mais sobre as funções de sistemas de sites e ações de cliente que podem usar um servidor proxy.|  



<!--HONumber=Dec16_HO3-->

