---
title: Monitorar o gateway de gerenciamento de nuvem
titleSuffix: Configuration Manager
description: Monitore os clientes e o tráfego de rede por meio do CMG (gateway de gerenciamento de nuvem).
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 820d8a4241a6d250ce652f95ea47abe015600d4a
ms.sourcegitcommit: 316899b08f2ef372993909e08e069f7edfed1d33
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44111120"
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Monitorar o gateway de gerenciamento de nuvem no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Depois que o gateway de gerenciamento de nuvem estiver em execução e os clientes estiverem se conectando por meio dele, você poderá monitorar os clientes e o tráfego de rede para garantir que sabe como o serviço está sendo executado.



## <a name="monitor-clients"></a>Monitorar clientes

Os clientes conectados por meio do gateway de gerenciamento de nuvem são exibidos no console do Configuration Manager da mesma forma que os clientes locais. Para obter mais informações, consulte [Como monitorar clientes](/sccm/core/clients/manage/monitor-clients).



## <a name="monitor-traffic-in-the-console"></a>Monitorar o tráfego no console

Monitore o tráfego no gateway de gerenciamento de nuvem usando o console do Configuration Manager:

1. Acesse **Administração > Serviços de Nuvem > Gateway de Gerenciamento de Nuvem**.

2. Selecione o gateway de gerenciamento de nuvem no painel de lista.

3. Exiba as informações de tráfego no painel de detalhes para as funções do sistema de sites e o ponto de conexão do gateway de gerenciamento de nuvem aos quais ele se conecta.



## <a name="set-up-outbound-traffic-alerts"></a>Configurar alertas de tráfego de saída

Os alertas de tráfego de saída ajudam você a saber quando o tráfego de rede se aproxima de um nível de limite de 14 dias. Ao criar o gateway de gerenciamento de nuvem, configure alertas de tráfego. Se você tiver ignorado essa parte, ainda será possível configurar os alertas depois que o serviço estiver em execução. Ajuste as configurações de alerta a qualquer momento.

1. Acesse **Administração > Serviços de Nuvem > Gateway de Gerenciamento de Nuvem**.

2. Clique com o botão direito do mouse no gateway de gerenciamento de nuvem no painel de lista e escolha **Propriedades**.

3. Clique na guia **Alertas**. Habilite o limite e os alertas. Especifique o limite de dados de 14 dias em GB (gigabytes). Especifique também o percentual de limite para elevar os diferentes níveis de alerta.

4. Clique em **OK** quando terminar.



## <a name="monitor-logs"></a>Monitorar os logs

O gateway de gerenciamento de nuvem gera entradas em vários arquivos de log. Para obter mais informações, consulte [Arquivos de log no System Center Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).
