---
title: Gerenciar clientes na Internet
titleSuffix: Configuration Manager
description: Saiba como gerenciar clientes com o gateway de gerenciamento de nuvem e o gerenciamento de clientes baseado na Internet no Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 198b044a66bf81ea846d5e4febe655b78c04dd13
ms.sourcegitcommit: 316899b08f2ef372993909e08e069f7edfed1d33
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44111069"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Gerenciar clientes na Internet com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Normalmente, no Configuration Manager, a maioria dos computadores e servidores gerenciados está fisicamente na mesma rede interna dos servidores do sistema de sites que executam funções de gerenciamento. No entanto, você pode gerenciar os clientes fora da rede interna quando eles estão conectados à Internet. Essa capacidade não exige que os clientes se conectem por meio da VPN para acessar os servidores do sistema de sites.

O Configuration Manager fornece duas maneiras para gerenciar clientes conectados à Internet:

-   Gateway de gerenciamento de nuvem

-   Gerenciamento de clientes baseado na Internet


## <a name="cloud-management-gateway"></a>Gateway de gerenciamento de nuvem

O gateway de gerenciamento de nuvem fornece o gerenciamento de clientes baseado na Internet. Ele usa uma combinação de um serviço de nuvem do Microsoft Azure e uma nova função do sistema de sites que se comunica com o serviço. Os clientes baseados na Internet usam o serviço de nuvem para se comunicar com o Configuration Manager local.

#### <a name="advantages"></a>Vantagens  

-   Nenhum investimento adicional em infraestrutura necessário.  

-   Não expõe a infraestrutura local à Internet.  

-   As máquinas virtuais em nuvem que executam o serviço são totalmente gerenciadas pelo Azure e não precisam de nenhuma manutenção.  

-   Facilmente instalado e configurado no console do Configuration Manager.  

#### <a name="disadvantages"></a>Desvantagens  

-   Custo da assinatura na nuvem.  

-   Dados de gerenciamento enviados por meio do serviço de nuvem.  

Para obter mais informações, consulte [Planejar o gateway de gerenciamento de nuvem](plan-cloud-management-gateway.md).  



## <a name="internet-based-client-management"></a>Gerenciamento de clientes baseado na Internet

Esse método se baseia nos servidores do sistema de sites para a Internet com os quais os clientes se comunicam para fins de gerenciamento. Ele exige que os clientes e os servidores do sistema de sites sejam configurados para o gerenciamento baseado na Internet.

#### <a name="advantages"></a>Vantagens  

-   Sem dependência do serviço de nuvem.  

-   Sem custos adicionais associados a uma assinatura na nuvem.  

-   Controle total dos servidores e das funções que fornecem o serviço.  

#### <a name="disadvantages"></a>Desvantagens  

-   Exige investimentos adicionais em infraestrutura.  

-   Sobrecarga e custos operacionais de uma infraestrutura adicional.  

-   A infraestrutura deve ser exposta à Internet.  

Para obter mais informações, consulte [Planejar o gerenciamento de clientes baseado na Internet](plan-internet-based-client-management.md).  
