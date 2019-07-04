---
title: Infraestrutura de rede
titleSuffix: Configuration Manager
description: Configure firewalls, portas e domínios para preparar-se para comunicações do Configuration Manager.
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 60a24e06d650b0e25007fb8490eb0c7d8c1996a1
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67285605"
---
# <a name="network-infrastructure-considerations-for-configuration-manager"></a>Considerações sobre infraestrutura de rede para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para preparar sua rede para dar suporte ao Configuration Manager, você precisará configurar alguns componentes de infraestrutura. Por exemplo, abra portas de firewall para passar as comunicações usadas pelo Configuration Manager.  

## <a name="ports-and-protocols"></a>Portas e protocolos

Diferentes recursos do Configuration Manager usam portas de rede diferentes. Algumas portas são necessárias e algumas você pode personalizar.

A maioria das comunicações do Configuration Manager usa portas comuns, como a porta 80 para HTTP ou 443 para HTTPS. Algumas funções do sistema de sites dão suporte ao uso de sites personalizados e portas personalizadas. Para saber mais, confira [Sites para servidores de sistema de sites](/sccm/core/plan-design/network/websites-for-site-system-servers).

Antes de implantar o Configuration Manager, identifique as portas que você planeja usar e configure os firewalls conforme o desejado.

Depois de instalar o Configuration Manager, se precisar alterar uma porta, não se esqueça de atualizar os firewalls em dispositivos e a rede. Também altere a configuração da porta no Configuration Manager.

Para obter mais informações, consulte os seguintes artigos:

- [Como configurar as portas de comunicação do cliente](/sccm/core/clients/deploy/configure-client-communication-ports)
- [Portas usadas no Configuration Manager](/sccm/core/plan-design/hierarchy/ports)


## <a name="internet-access-requirements"></a>Requisitos de acesso à Internet

Alguns recursos do Configuration Manager dependem da conectividade com a Internet para ter a funcionalidade completa. Se sua organização restringe a comunicação de rede com a Internet usando um dispositivo de firewall ou proxy, dê permissão aos pontos de extremidade necessários.

Para saber mais, confira [Requisitos de acesso à Internet](/sccm/core/plan-design/network/internet-endpoints)


## <a name="proxy-servers"></a>Servidores proxy

Você pode especificar servidores proxy separados para clientes e servidores de sistema de sites diferentes. Você deve fazer essas configurações ao instalar um cliente ou função do sistema de site, ou pode alterá-las posteriormente conforme o necessário.

Para obter mais informações, confira [Suporte ao servidor proxy](/sccm/core/plan-design/network/proxy-server-support).
