---
title: "Gerenciar clientes na Internet – Configuration Manager | Microsoft Docs"
description: Saiba como gerenciar clientes com o gateway de gerenciamento da nuvem e gerenciamento de clientes baseado na Internet no Configuration Manager.
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3743c80b0c2b5142f3a537ba3855ffd14794d42b
ms.openlocfilehash: 6104107429184f31df12db84089f41df1ef81539

---

# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Gerenciar clientes na Internet com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Normalmente, no Configuration Manager, a maioria dos computadores e servidores gerenciados está fisicamente na mesma rede privada ou corporativa interna que os servidores do sistema de sites que executam funções de gerenciamento. No entanto, você poderá gerenciar computadores cliente fora da rede corporativa se eles estiverem conectados à Internet sem a necessidade de os clientes se conectarem por meio de redes virtuais privadas para acessar os servidores do sistema de sites.

O Configuration Manager fornece duas maneiras para gerenciar clientes conectados à Internet:

-   Gateway de gerenciamento de nuvem

-   Gerenciamento de clientes baseado na Internet

## <a name="cloud-management-gateway"></a>Gateway de gerenciamento de nuvem

Começando da versão 1610, o Configuration Manager introduz o gateway de gerenciamento de nuvem. Esse novo método fornece uma maneira de gerenciar clientes baseados na Internet usando uma combinação de um serviço de nuvem implantado no Microsoft Azure e uma nova função do sistema de sites que se comunica com o serviço. Em seguida, os clientes usam o serviço para se comunicarem com o Configuration Manager.

Vantagens:

-   Nenhum investimento adicional em infraestrutura necessário.

-   Não expõe a infraestrutura local à Internet.

-   As máquinas virtuais em nuvem que executam o serviço são totalmente gerenciadas pelo Azure e não precisam de nenhuma manutenção.

-   Facilmente instalado e configurado no console do Configuration Manager.

Desvantagens:

-   Custo da assinatura na nuvem.

-   Dados de gerenciamento enviados por meio do serviço de nuvem.

Para obter mais informações, consulte [Planejar o gateway de gerenciamento de nuvem](plan-cloud-management-gateway.md).

## <a name="internet-based-client-management"></a>Gerenciamento de clientes baseado na Internet

Esse método se baseia nos servidores do sistema de sites para a Internet com os quais os clientes se comunicam para fins de gerenciamento. Esse método exige que os clientes e os servidores do sistema de sites sejam configurados para o gerenciamento baseado na Internet.

Vantagens:

-   Sem dependência do serviço de nuvem.

-   Sem custos adicionais associados a uma assinatura na nuvem.

-   Controle total dos servidores e das funções que fornecem o serviço.

Desvantagens:

-   Exige investimentos adicionais em infraestrutura.

-   Sobrecarga e custos operacionais de uma infraestrutura adicional.

-   A infraestrutura deve ser exposta à Internet.

Para obter mais informações, consulte [Planejar o gerenciamento de clientes baseado na Internet](plan-internet-based-client-management.md).



<!--HONumber=Jan17_HO4-->


