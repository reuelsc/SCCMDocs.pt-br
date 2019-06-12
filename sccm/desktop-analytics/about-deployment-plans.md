---
title: Planos de implantação na área de trabalho de análise
titleSuffix: Configuration Manager
description: Saiba mais sobre planos de implantação na área de trabalho de análise.
ms.date: 06/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 88c78cef4717cc3a51a53b7fd5aba0cbefa93a8e
ms.sourcegitcommit: 0bd336e11c9a7f2de05656496a1bc747c5630452
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66834939"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>Sobre planos de implantação na área de trabalho de análise

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Análise da área de trabalho coleta e analisa dados de dispositivo, o aplicativo e o driver em sua organização. Com base na sua entrada e essa análise, você pode usar o serviço para criar planos de implantação para Windows 10. Planos de implantação têm os seguintes recursos:  

- Recomende automaticamente quais dispositivos para incluir no pilotos  

- Identificar problemas de compatibilidade e atenuações de sugerir  

- Avaliar a integridade da implantação antes, durante e após as atualizações  

- Acompanhar o progresso da implantação  

Como parte do seu plano de implantação, você deve executar as seguintes ações:  

- Definir quais versões do Windows 10 que você deseja implantar  

- Escolha quais grupos de dispositivos aos quais você deseja implantar  

- Criar regras de preparação para a implantação  

- Definir a importância de seus aplicativos  

- Escolher dispositivos piloto com base nas recomendações automática  

- Decida como corrigir problemas com aplicativos com base nas recomendações da área de trabalho de análise  

Por padrão, a análise de área de trabalho atualiza dados do plano de implantação diariamente. As alterações feitas em um plano de implantação, como a atribuição de importância para um aplicativo ou escolher um dispositivo para incluir em um piloto, leva até 24 horas para processar. Para acelerar esse processo, solicite uma atualização de dados sob demanda. Para obter mais informações, consulte [perguntas frequentes sobre análise de área de trabalho](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

Após a conexão da área de trabalho de análise para o Configuration Manager, selecione suas coleções nos planos de implantação. Essa integração, em seguida, permite que você implante o Windows a uma coleção com base nos dados de análise de área de trabalho.



## <a name="readiness-rules"></a>Regras de preparação

As seguintes regras de preparação estão disponíveis nos planos de implantação:

- Se os dispositivos recebem automaticamente drivers do Windows Update. Se os dispositivos recebam as atualizações de driver do Windows Update, então quaisquer problemas de driver identificados como parte da avaliação de prontidão são marcados automaticamente como **pronto**.  

- Baixa instalar o limite de contagem para seus aplicativos do Windows. Se um aplicativo é instalado em uma porcentagem maior de computadores que esse limite, o plano de implantação marcará o aplicativo como **Noteworthy**. Essa marca significa que você pode decidir quanto é importante testar durante a fase piloto.  



## <a name="importance"></a>importância

Como parte do plano de implantação, defina as *importância* dos aplicativos. Análise da área de trabalho detecta esses aplicativos como instalado nos dispositivos de destino. Essa configuração ajuda a área de trabalho de análise determinar quais dispositivos inclui na fase piloto da implantação.

Se um aplicativo é instalado em menos de 2% dos dispositivos de destino, ele é marcado **baixa contagem de instalações**. Dois por cento é o valor padrão. Você pode ajustar o limite nas configurações de preparação de 0% a 10%. Análise da área de trabalho marca automaticamente esses aplicativos conforme **pronto para atualizar**.  

Para aplicativos, escolha uma importância de **crítica**, **importante**, ou **não importante**. Se você marcar um como importante ou crítica, análise de área de trabalho inclui na implantação piloto alguns dispositivos com que o aplicativo. O serviço inclui no piloto, mais instâncias de um aplicativo crítico. Se você marcar um aplicativo como não importante, análise de área de trabalho define automaticamente como **pronto para atualizar**.



## <a name="pilot-devices"></a>Dispositivos piloto

Análise da área de trabalho combina as informações de importância com as configurações globais do piloto. Em seguida, cria uma recomendação para o qual os dispositivos devem ser parte da implantação do piloto. A implantação piloto recomendada inclui dispositivos com diferentes configurações de hardware e uma ou mais instâncias de todos os aplicativos críticos e importantes. Se um aplicativo é marcada como crítico, o serviço recomenda mais dispositivos com esse aplicativo no piloto.



## <a name="deployment-plans-in-configuration-manager"></a>Planos de implantação no Configuration Manager

Depois de criar um plano de implantação, use o Configuration Manager para implantar os produtos. Uma vez do início da implantação, análise da área de trabalho monitora a implantação com base nas configurações no plano.


## <a name="next-steps"></a>Próximas etapas

- [Saiba mais sobre os ativos de área de trabalho de análise](/sccm/desktop-analytics/about-assets): aplicativos, drivers e dispositivos  

- [Saiba mais sobre atualizações de segurança e de recurso](/sccm/desktop-analytics/about-updates)  

- [Criar um plano de implantação](/sccm/desktop-analytics/create-deployment-plans)  
