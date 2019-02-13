---
title: Monitorar a conformidade de Defesa contra Ameaças Móveis
titleSuffix: Configuration Manager
description: Monitorar o status de conformidade do parceiro de Defesa contra Ameaças Móveis no console do Configuration Manager
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 408190da-bea6-4122-9dd6-f90155040e88
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: cc5b38894155df35812d14397fb0d3aaea79c585
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122484"
---
# <a name="monitor-mobile-threat-defense-compliance"></a>**Monitorar a conformidade de Defesa contra Ameaças Móveis**

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

## <a name="to-monitor-the-overall-compliance-status"></a>Para monitorar o status geral de conformidade

Para monitorar o status de defesa contra ameaças móveis:

1.  No console do Configuration Manager, clique no workspace **Monitoramento**.

2.  No workspace **Monitoramento**, clique no nó **Segurança**.

Você pode ver um resumo do status da conformidade com níveis de ameaça diferentes, que é exibido em um formato gráfico visual. Você pode clicar em seções específicas dos gráficos para ver mais informações como: 

- O número de dispositivos que são relatados como sem conformidade por plataforma
- Erros relacionados ao status de conformidade do dispositivo

![](http://i.imgur.com/bmPsiWk.png)

## <a name="to-monitor-the-individual-compliance-status"></a>Para monitorar o status individual de conformidade

Você também pode ver o status individual do dispositivo:

1.  No console do Configuration Manager, clique no workspace **Ativos e conformidade**.

2.  Clique em **Dispositivos**.

> [!TIP] 
> Você pode adicionar as colunas **Conformidade do dispositivo contra ameaça** e **Nível de ameaça do dispositivo** para ver o status. Essas colunas não são exibidas por padrão.

## <a name="device-threat-protection-tab"></a>Guia Proteção contra Ameaças ao Dispositivo

Além disso, na tela **Dispositivos**, você pode selecionar dispositivos específicos e clicar na guia **Proteção contra Ameaças ao Dispositivo** que fornece mais detalhes sobre o status de conformidade do dispositivo. Veja abaixo as descrições da coluna e seus valores esperados para ajudar a analisar o status de conformidade do dispositivo.

> [!IMPORTANT] 
> A guia Proteção contra Ameaças ao Dispositivo aparecerá apenas se o dispositivo selecionado for um dispositivo móvel.

|Nome da coluna|Visível por padrão|Descrição| 
|-|-|-|
|**Descrição**| Sim | Detalhes sobre a ameaça fornecida pelo parceiro de Defesa contra Ameaças Móveis. |
|**Hora da última atualização**| Sim | A última vez em que o parceiro de Defesa contra Ameaças Móveis enviou detalhes atualizados sobre a ameaça para o Intune. |
|**Gravidade da ameaça**| Sim | A gravidade da ameaça é a definição de uma ameaça individual com base na configuração do administrador no console do parceiro de Defesa contra Ameaças Móveis. Ele tem um dos três valores: **Baixa**, **médio** ou **alta** |
|**Status da ameaça**| Sim | O estado atual da ameaça no dispositivo. Estados possíveis: **Active Directory**, **resolvido** ou **ignorado:** Indica que o usuário ignorou a ameaça em seu dispositivo, mas a ameaça ainda está presente. |
|**Tipo de ameaça**| Sim | Tipo de ameaça de parceiro de Defesa contra Ameaças Móveis. Valores possíveis: **Aplicativo**, **arquivo** ou **SO** |
|**ID da conta do AAD**| Não | O identificador exclusivo do Azure Active Directory. |
|**Classificação**| Sim | O parceiro de Defesa contra Ameaças Móveis forneceu a classificação de ameaça. Valores possíveis: **Habilitador de raiz, Riskware, Adware, Chargeware, DataLeak, cavalo de Troia, worms, vírus, Exploit, Backdoor, Bot, AppDropper, ClickFraud, Spam, Spyware, SurveillanceWare, vulnerabilidade, Unknown, Root Jailbrake, conectividade, TollFraud, SideloadedApp** |
|**ID do Dispositivo**| Não | A ID de objeto do Azure Active Directory que representa o dispositivo ingressado no local de trabalho com informações sobre a ameaça. |
|**ID da Ameaça**| Não | O parceiro de Defesa contra Ameaças Móveis gerou um identificador exclusivo para a ameaça. A ID da Ameaça é usada para a resolução de acompanhamento. |
|**URL da Ameaça**| Não | Quando presente, a URL de ameaça vincula-se de volta para a exibição do console de gerenciamento do parceiro de Defesa contra Ameaças Móveis dessa ameaça específica. |

> [!TIP] 
> Habilite as colunas que não estão **visíveis por padrão** para ver mais detalhes sobre o status de conformidade de Defesa contra Ameaças Móveis para seus dispositivos.
