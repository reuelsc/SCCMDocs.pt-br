---
title: Restringir o acesso com base em riscos
titleSuffix: Configuration Manager
description: Restrinja o acesso aos recursos da empresa com base em risco de dispositivo, rede e aplicativo.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 90098dc0243e8513fe78692fe91a8390f7936eba
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56119642"
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Gerenciar o acesso aos recursos da empresa com base em risco de dispositivo, rede e aplicativo

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os conectores de Defesa contra Ameaças Móveis permitem aproveitar o fornecedor da Defesa contra Ameaças Móveis escolhido como uma fonte de informações para as políticas de conformidade e regras de acesso condicional. Isso possibilita adicionar uma camada de proteção aos seus recursos organizacionais, como Exchange e Sharepoint, especificamente de dispositivos móveis comprometidos.

> [!Important]  
> A partir de 14 de agosto de 2018, o gerenciamento híbrido de dispositivos móveis é um [recurso preterido](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para saber mais, confira [O que é o MDM híbrido](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="what-problem-does-this-solve"></a>Qual problema isso resolve?

As organizações precisam proteger dados confidenciais contra ameaças emergentes que incluem ameaças físicas, baseadas em aplicativo e em rede, além de vulnerabilidades do sistema operacional.

Historicamente, as organizações têm sido proativas ao proteger computadores contra ataques, enquanto os dispositivos móveis ficam sem monitoramento e proteção. Plataformas móveis têm proteção interna, como isolamento de aplicativo e lojas de aplicativos de consumidor verificadas, mas permanecerão vulneráveis a ataques sofisticados. Hoje, um número maior de funcionários usa dispositivos para o trabalho e precisam ter acesso a informações confidenciais. Os dispositivos precisam ser protegidos contra ataques cada vez mais sofisticados.



## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Como funcionam os conectores da Defesa contra Ameaças Móveis do Intune?

O conector protege recursos organizacionais criando um canal de comunicação entre o Intune e o fornecedor de Defesa contra Ameaças Móveis escolhido. Parceiros de Defesa contra Ameaças Móveis do Intune oferecem aplicativos intuitivos e fáceis de implantar para dispositivos móveis, que examinam e analisam ativamente informações sobre ameaças para compartilhar com o Intune. Use essas informações para fins de relatório ou imposição. 

Por exemplo, um aplicativo de Defesa contra Ameaças Móveis conectado informa ao fornecedor da Defesa contra Ameaças Móveis que um dispositivo está atualmente conectado a uma rede vulnerável a ataques de interceptação. Essas informações são compartilhadas e categorizadas em um nível de risco apropriado: baixo, médio ou alto. Compare esse risco com as permissões de nível de risco configuradas no Intune para determinar se o acesso a determinados recursos de sua escolha deve ser revogado enquanto o dispositivo estiver comprometido.



## <a name="sample-scenarios"></a>Exemplo de cenários

Quando um dispositivo é considerado infectado pela solução de Defesa contra Ameaças Móveis:

![Dispositivo infectado da Defesa contra Ameaças Móveis](../media/mtp/MTD-image-1.png)

O acesso é concedido quando o dispositivo é corrigido:

![Acesso concedido à Defesa contra Ameaças Móveis](../media/mtp/MTD-image-2.png)



## <a name="next-steps"></a>Próximas etapas

Saiba como proteger o acesso aso recursos da empresa com base nos riscos ao dispositivo, rede e aplicativo com:

- [Lookout](https://docs.microsoft.com/intune/deploy-use/lookout-mobile-threat-defense-connector)
