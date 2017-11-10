---
title: Restringir o acesso com base em riscos
titleSuffix: Configuration Manager
description: Restrinja o acesso aos recursos da empresa com base em risco de dispositivo, rede e aplicativo.
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: e013c2a3758685aacdacf0707ca0df2c258976b2
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Gerenciar o acesso aos recursos da empresa com base em risco de dispositivo, rede e aplicativo

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os conectores de Defesa contra Ameaças Móveis permitem aproveitar o fornecedor da Defesa contra Ameaças Móveis escolhido como uma fonte de informações para as políticas de conformidade e regras de acesso condicional. Isso permite que os Administradores de TI adicionem uma camada de proteção aos seus recursos corporativos, como Exchange e Sharepoint, especificamente de dispositivos móveis comprometidos.

## <a name="what-problem-does-this-solve"></a>Qual problema isso resolve?

As empresas precisam proteger dados confidenciais contra ameaças emergentes, incluindo ameaças físicas, baseadas em aplicativo e em rede, bem como vulnerabilidades do sistema operacional.
Historicamente, as empresas têm sido proativas ao proteger computadores contra ataques, enquanto os dispositivos móveis ficam sem monitoramento e proteção. Plataformas móveis têm proteção interna, como isolamento de aplicativo e lojas de aplicativos de consumidor verificadas, mas permanecerão vulneráveis a ataques sofisticados. Hoje, um número maior de funcionários usa dispositivos para o trabalho e precisam ter acesso a informações confidenciais. Os dispositivos precisam ser protegidos contra ataques cada vez mais sofisticados.

A [implantação de MDM híbrida (SCCM com o Intune)](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) oferece a capacidade de controlar o acesso aos recursos e dados da empresa com base na avaliação de risco que os parceiros de soluções de Proteção contra Ameaças do Dispositivo fornecem, como a Defesa contra Ameaças Móveis.

## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Como funcionam os conectores da Defesa contra Ameaças Móveis do Intune?

O conector protege recursos da empresa criando um canal de comunicação entre o Intune e o fornecedor de Defesa contra Ameaças Móveis escolhido. Parceiros de Defesa contra Ameaças Móveis do Intune oferecem aplicativos intuitivos e fáceis de implantar para dispositivos móveis que examinam e analisam ativamente informações sobre ameaças para compartilhar com o Intune, para fins de relatórios ou imposição. Por exemplo, se um aplicativo de Defesa contra Ameaças Móveis conectado informar ao fornecedor de Defesa contra Ameaças Móveis que um telefone em sua rede está conectado a uma rede vulnerável aos ataques de intermediários, essas informações serão compartilhadas e categorizadas em um nível apropriado de risco (baixo/médio/grande) – que, em seguida, pode ser comparado com suas concessões de nível de risco configuradas no Intune, a fim de determinar se o acesso a determinados recursos de sua escolha deve ser revogado enquanto o dispositivo estiver comprometido.

## <a name="sample-scenarios"></a>Exemplo de cenários

Quando um dispositivo é considerado infectado pela solução de Defesa contra Ameaças Móveis:

![Dispositivo infectado da Defesa contra Ameaças Móveis](../media/mtp/MTD-image-1.png)

O acesso é concedido quando o dispositivo é corrigido:

![Acesso concedido à Defesa contra Ameaças Móveis](../media/mtp/MTD-image-2.png)

## <a name="next-steps"></a>Próximas etapas

Saiba como proteger o acesso aso recursos da empresa com base nos riscos ao dispositivo, rede e aplicativo com:

- [Lookout](https://docs.microsoft.com/intune/deploy-use/lookout-mobile-threat-defense-connector)