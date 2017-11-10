---
title: "Defesa contra Ameaças Móveis"
titleSuffix: Configuration Manager
description: "Restrinja o acesso aos recursos da empresa com base no risco ao dispositivo, rede e aplicativo usando o Configuration Manager e os parceiros de Defesa contra Ameaças Móveis do Intune"
ms.custom: na
ms.date: 03/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c0e6824-2dfe-4700-b817-d5631e0eb872
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 83911f35dbe8fc7bc24a4885929fbdf5660e7285
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="intune-mobile-threat-defense-connectors-in-configuration-manager"></a>Conectores da Defesa contra Ameaças Móveis do Intune no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A [implantação de MDM híbrido (SCCM com Intune)](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) e a integração entre o Intune e o parceiro de Defesa contra Ameaça Móvel oferece a você a capacidade de controlar o acesso aos recursos e dados da empresa com base na avaliação de risco ao dispositivo.

Os conectores da Defesa contra Ameaças Móveis do Intune permitem que você aproveite seu fornecedor de Defesa contra Ameaças Móveis escolhido como uma fonte de informações para suas políticas de conformidade e regras de acesso condicional. Isso permite que os Administradores de TI adicionem uma camada de proteção aos seus recursos corporativos, como Exchange e Sharepoint, especificamente de dispositivos móveis comprometidos.

## <a name="what-problem-does-this-solve"></a>Qual problema isso resolve?

As empresas precisam proteger dados confidenciais contra ameaças emergentes, incluindo ameaças físicas, baseadas em aplicativo e em rede, bem como vulnerabilidades do sistema operacional.
Historicamente, as empresas têm sido proativas ao proteger computadores contra ataques, enquanto os dispositivos móveis ficam sem monitoramento e proteção. Plataformas móveis têm proteção interna, como isolamento de aplicativo e lojas de aplicativos de consumidor verificadas, mas permanecerão vulneráveis a ataques sofisticados. Hoje, um número maior de funcionários usa dispositivos para o trabalho e precisam ter acesso a informações confidenciais. Os dispositivos precisam ser protegidos contra ataques cada vez mais sofisticados.

## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Como funcionam os conectores da Defesa contra Ameaças Móveis do Intune?

O conector protege recursos da empresa criando um canal de comunicação entre o Intune e o fornecedor de Defesa contra Ameaças Móveis escolhido. Parceiros de Defesa contra Ameaças Móveis do Intune oferecem aplicativos intuitivos e fáceis de implantar para dispositivos móveis que examinam e analisam ativamente informações sobre ameaças para compartilhar com o Intune, para fins de relatórios ou imposição. Por exemplo, se um aplicativo de Defesa contra Ameaças Móveis conectado informar ao fornecedor de Defesa contra Ameaças Móveis que um telefone em sua rede está conectado a uma rede vulnerável aos ataques de intermediários, essas informações serão compartilhadas e categorizadas em um nível apropriado de risco (baixo/médio/grande) – que, em seguida, pode ser comparado com suas concessões de nível de risco configuradas no Intune, a fim de determinar se o acesso a determinados recursos de sua escolha deve ser revogado enquanto o dispositivo estiver comprometido.

## <a name="sample-scenarios"></a>Exemplo de cenários

Quando um dispositivo é considerado infectado pela solução de Defesa contra Ameaças Móveis:

![](http://i.imgur.com/Li1WUOU.png)

O acesso é concedido quando o dispositivo é corrigido:

![](http://i.imgur.com/VCIwpdz.png)

## <a name="mobile-threat-defense-partners"></a>Parceiros de Defesa contra Ameaças Móveis

Saiba como proteger o acesso aso recursos da empresa com base nos riscos ao dispositivo, rede e aplicativo com:

- [Lookout](https://docs.microsoft.com/sccm/protect/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)
