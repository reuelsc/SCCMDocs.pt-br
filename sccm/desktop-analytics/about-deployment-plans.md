---
title: Planos de implantação na área de trabalho de análise
titleSuffix: Configuration Manager
description: Saiba mais sobre planos de implantação na área de trabalho de análise.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: ce726ffa0dfc8a46bd0891e50ff087ad4931d901
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62243347"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>Sobre planos de implantação na área de trabalho de análise 

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Análise da área de trabalho coleta e analisa dados de dispositivo, o aplicativo e o driver em sua organização. Com base na sua entrada e essa análise, você pode usar o serviço para criar planos de implantação para Windows 10 e Office 365 ProPlus. Planos de implantação têm os seguintes recursos:  

- Recomende automaticamente quais dispositivos para incluir no pilotos  

- Identificar problemas de compatibilidade e atenuações de sugerir  

- Avaliar a integridade da implantação antes, durante e após as atualizações  

- Acompanhar o progresso da implantação  


Como parte do seu plano de implantação, você deve executar as seguintes ações:  

 - Defina quais produtos e versões que você deseja implantar: Windows 10, Office 365 ProPlus, ou ambos  

 - Escolha quais grupos de dispositivos aos quais você deseja implantar  

 - Criar regras de preparação para a implantação  

 - Definir a importância de seus aplicativos e suplementos do Office  

 - Escolher dispositivos piloto com base nas recomendações automática  

 - Decida como corrigir problemas com aplicativos e do Office com base nas recomendações da área de trabalho de análise  


Análise da área de trabalho atualiza os dados de plano de implantação diariamente. As alterações feitas não podem aparecer para 24 horas. Essas alterações incluem a atribuição de importância para um aplicativo ou escolhendo um dispositivo para incluir em um piloto.  

Se você conectar a área de trabalho de análise para o Configuration Manager, selecione suas coleções nos planos de implantação. Essa integração, em seguida, permite que você implante o Windows ou do Office para uma coleção com base nos dados de análise de área de trabalho. 

Se você não usar o Configuration Manager, você pode criar grupos no Log Analytics. Para obter mais informações, consulte [pesquisas de log de grupos de computadores no Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-computer-groups). 



## <a name="readiness-rules"></a>Regras de preparação

As seguintes regras de preparação estão disponíveis nos planos de implantação:

- Se os dispositivos recebem automaticamente drivers do Windows Update. Se os dispositivos recebam as atualizações de driver do Windows Update, então quaisquer problemas de driver identificados como parte da avaliação de prontidão são marcados automaticamente como **pronto**.  

- Baixa instalar o limite de contagem para seus aplicativos do Windows. Se um aplicativo é instalado em uma porcentagem maior de computadores que esse limite, o plano de implantação marcará o aplicativo como **Noteworthy**. Essa marca significa que você pode decidir quanto é importante testar durante a fase piloto.  

- Atualizar o Office 365 ProPlus de 32 bits para 64 bits em dispositivos que têm uma versão de 64 bits do Windows. Esse comportamento é o padrão.  

- Ao atualizar de uma versão anterior do Office, deixe a aplicativos do Office mais antigos, mesmo que esses aplicativos não existem na versão mais recente do Office. Esse comportamento não é em por padrão.  

- Baixa instalar o limite de contagem para seus suplementos do Office. O limite padrão é `2%`. Suplementos abaixo desse limite são definidos automaticamente *baixa contagem de instalações*. Análise da área de trabalho não valida esses suplementos durante o piloto. 

    Se um suplemento é instalado em uma porcentagem maior de computadores que esse limite, o plano de implantação marcará o suplemento como *Noteworthy*. Em seguida, você pode decidir sua importância para testar durante a fase piloto.   



## <a name="importance"></a>importância

Como parte do plano de implantação, defina as *importância* dos suplementos do Office e aplicativos. Análise da área de trabalho detecta esses aplicativos como instalado nos dispositivos de destino. Essa configuração ajuda a área de trabalho de análise determinar quais dispositivos inclui na fase piloto da implantação. 

Se um aplicativo ou suplemento é instalado em menos de 2% dos dispositivos de destino, ele é marcado **baixa contagem de instalações**. Dois por cento é o valor padrão. Você pode ajustar o limite nas configurações de preparação de 0% a 10%. Análise da área de trabalho marca automaticamente esses aplicativos e suplementos como **pronto para atualizar**.  

Para aplicativos e complementos, escolha uma importância de **crítica**, **importante**, ou **não importante**. Se você marcar um como importante ou crítica, análise de área de trabalho inclui na implantação piloto alguns dispositivos com esse aplicativo ou suplemento. O serviço inclui no piloto, mais instâncias de um aplicativo crítico ou de suplemento. Se você marca um aplicativo ou suplemento como não importante, análise de área de trabalho define automaticamente como **pronto para atualizar**.



## <a name="pilot-devices"></a>Dispositivos piloto

Análise da área de trabalho combina as informações de importância com as configurações globais do piloto. Em seguida, cria uma recomendação para o qual os dispositivos devem ser parte da implantação do piloto. A implantação piloto recomendada inclui dispositivos com diferentes configurações de hardware e uma ou mais instâncias de todos os aplicativos críticos e importantes. Se um aplicativo é marcada como crítico, o serviço recomenda mais dispositivos com esse aplicativo no piloto.



## <a name="deployment-plans-in-configuration-manager"></a>Planos de implantação no Configuration Manager

Depois de criar um plano de implantação, use o Configuration Manager para implantar os produtos. Uma vez do início da implantação, análise da área de trabalho monitora a implantação com base nas configurações no plano.

<!--more on deployment plans in SCCM-->

<!-- test comment-->

## <a name="next-steps"></a>Próximas etapas

- [Saiba mais sobre os ativos de área de trabalho de análise](/sccm/desktop-analytics/about-assets): dispositivos, aplicativos, os aplicativos do Office, suplementos do Office e as macros do Office  

- [Saiba mais sobre atualizações de segurança e de recurso](/sccm/desktop-analytics/about-updates)  

- [Criar um plano de implantação](/sccm/desktop-analytics/create-deployment-plans)  

