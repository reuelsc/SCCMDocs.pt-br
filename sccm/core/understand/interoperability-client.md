---
title: Usar o cliente de interoperabilidade estendida do Configuration Manager com o Branch Atual | Microsoft Docs
description: "Saiba como usar o cliente do Branch de Manutenção de Longo Prazo do Configuration Manager com um site do Branch Atual."
ms.custom: na
ms.date: 08/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 9772224be78eee2777137225a59b53b1fd77a627
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2017
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Usar o software cliente do Configuration Manager para interoperabilidade estendida com versões futuras de um site do Branch Atual

*Aplica-se a: System Center Configuration Manager (Branch Atual), (Branch de Manutenção de Longo Prazo)*  

Em alguns casos, as políticas de sua empresa podem não permitir a atualização regular do cliente do Configuration Manager em alguns computadores. Por exemplo, talvez você precise estar em conformidade com políticas de gerenciamento de alterações, ou o dispositivo pode ser essencial.

Embora você deva continuar a usar a atualização automática do cliente quando possível para a maioria dos clientes, a partir da atualização 1610 do Configuration Manager, você poderá acomodar essas necessidades instalando um novo cliente para uso de longo prazo, chamado de EIC (cliente de interoperabilidade estendida).

O EIC é compatível com sites do Configuration Manager que executam a versão 1610 ou posterior. O EIC só deve ser usado para computadores específicos que não são atualizados com frequência, como quiosque ou dispositivos de ponto de venda. Use o cliente do Configuration Manager mais recente para todos os outros computadores.

## <a name="how-this-scenario-works"></a>Como este cenário funciona

Normalmente, quando você instala uma nova atualização no console para o Branch Atual, os clientes atualizam automaticamente o software cliente para que possam usar esses novos recursos.

Neste cenário, você usa o Branch Atual e recebe as atualizações e novos recursos. A maioria dos clientes executa o software cliente a do Branch Atual e pode atualizar o software cliente com cada atualização de versão que você instalar. No entanto, em um subconjunto de sistemas críticos que você não deseja receber atualizações de software cliente, instale o cliente de interoperabilidade estendida. Esses clientes não instalam o novo software cliente até que você implante explicitamente uma nova versão do software cliente neles.

>[!IMPORTANT]
>O site do Branch Atual deve executar a versão 1610 ou posterior.

## <a name="how-to-use-the-eic"></a>Como usar o EIC

1. Obtenha o EIC (versão de cliente 5.00.8412) da pasta \SMSSETUP\Client da mídia de instalação da atualização 1606 do Configuration Manager. Copie todo o conteúdo da pasta.
2. Instale manualmente o EIC nos dispositivos. [Leia mais detalhes sobre como instalar manualmente o cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).
3. Exclua essa coleção das atualizações do cliente.

>[!TIP]
>Para localizar o System Center Configuration Manager versão 1606 no VLSC (Centro de Serviços de Licenciamento por Volume), acesse a guia **Downloads e Chaves** do [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), pesquise “configuração do system center” e selecione **System Center Config Mgr (Branch Atual e LTSB)**.

## <a name="the-extended-interoperability-client-software"></a>O software cliente de interoperabilidade estendida

O EIC atual continuará a ser compatível com versões atualizadas do Branch Atual do Configuration Manager até pelo menos 18 de novembro de 2018. Após esse período, confira esta página para obter detalhes de um novo EIC, ou uma extensão de suporte para o EIC existente.

>[!TIP]
>Há suporte para o EIC por pelo menos dois anos a partir da data de lançamento (consulte [Suporte para versões do branch atual do System Center Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported)). Por exemplo, o suporte para o EIC atual é de dois anos após o lançamento do 1610, que é de 18 de novembro de 2018.

Planeje atualizar o cliente de interoperabilidade estendida em dispositivos gerenciados com o Branch Atual antes que o suporte do cliente expire. Para fazer isso, baixe uma nova versão do cliente da Microsoft e, em seguida, implante esse software cliente atualizado nos dispositivos que usam o cliente de interoperabilidade estendida atual.

## <a name="limitations-of-the-extended-interoperability-client"></a>Limitações do cliente de interoperabilidade estendida

- Atualizações para o software cliente de interoperabilidade estendida não estão disponíveis por meio de atualizações no console. Detalhes adicionais para a implantação de um software cliente atualizado serão fornecidos quando um cliente atualizado for liberado.
- O EIC só dá suporte a atualizações de software, inventário e pacotes e programas.

## <a name="next-steps"></a>Próximas etapas

Use as informações em [Como monitorar clientes](/sccm/core/clients/manage/monitor-clients) para garantir que os clientes estejam instalados corretamente nos dispositivos que você deseja.
