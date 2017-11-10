---
title: 'Monitorar o gateway de gerenciamento de nuvem '
titleSuffix: Configuration Manager
description: 
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: d88749b09dd5e88f29240cc0db2f2ace7a2f06f4
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Monitorar o gateway de gerenciamento de nuvem no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Começando da versão 1610, depois que o serviço do gateway de gerenciamento de nuvem estiver em execução e os clientes estiverem se conectando por meio dele, é possível monitorar os clientes e o tráfego de rede para garantir que você sabe como o serviço está sendo executado.

## <a name="monitor-clients"></a>Monitorar clientes

Os clientes conectados por meio do serviço do gateway de gerenciamento de nuvem serão exibidos no console do Configuration Manager da mesma forma que os clientes locais. Para obter mais informações, consulte [Como monitorar clientes](monitor-clients.md).

## <a name="monitor-traffic-in-the-console"></a>Monitorar o tráfego no console

É possível monitorar o tráfego no gateway de gerenciamento de nuvem usando o console do Configuration Manager:

1. Acesse **Administração > Serviços de Nuvem > Gateway de Gerenciamento de Nuvem**.

2. Selecione o serviço de gateway de gerenciamento de nuvem no painel de lista.

3. Exiba as informações de tráfego no painel de detalhes para a função de conexão do gateway de gerenciamento de nuvem e as funções do sistema de sites às quais ele se conecta.

## <a name="set-up-outbound-traffic-alerts"></a>Configurar alertas de tráfego de saída

Os alertas de tráfego de saída ajudarão você a saber quando o tráfego se aproxima de um nível de limite de 14 dias (2 semanas). Você terá a opção de configurar alertas de tráfego ao criar o serviço de gateway de gerenciamento de nuvem. Se você tiver ignorado essa parte, ainda será possível configurar os alertas depois que o serviço estiver em execução. Além disso, também é possível ajustar as configurações de alerta a qualquer momento.

1. Acesse **Administração > Serviços de Nuvem > Gateway de Gerenciamento de Nuvem**.

2. Clique com o botão direito do mouse no serviço de gateway de gerenciamento de nuvem no painel de lista e escolha **Propriedades**.

3. Clique na guia Alertas e opte por ativar (ou desativar) o limite e os alertas. Em seguida, especifique o limite de 14 dias (em GB) e os percentuais do limite para acionar os diferentes níveis de alerta.

4. Clique em **OK** quando terminar.

## <a name="monitor-logs"></a>Monitorar os logs

O serviço de gateway de gerenciamento de nuvem gera entradas em vários arquivos de log. Para obter mais informações, consulte [Arquivos de log no System Center Configuration Manager](/sccm/core/plan-design/hierarchy/log-files).
