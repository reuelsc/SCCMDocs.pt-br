---
title: Planos de implantação na área de trabalho de análise
titleSuffix: Configuration Manager
description: Saiba mais sobre planos de implantação na área de trabalho de análise.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8e1f084f1f3fdfd8b51caa7db696a841ffbf2e57
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159252"
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


## <a name="plan-assets"></a>Plano de ativos

<!-- 4670224 -->

Enquanto o [ativos](/sccm/desktop-analytics/about-assets) área também mostra os dispositivos e aplicativos, o **planejar ativos** área em um plano de implantação específico inclui informações adicionais.

### <a name="devices"></a>Dispositivos

Consulte a **decisão de atualização do Windows** para cada dispositivo no plano de implantação.

Os Windows atualizar decisão **substituir dispositivo** pode ser devido a um dos seguintes motivos:

- Falhou uma verificação de processador do Windows 10 necessários. Para obter mais informações, consulte [requisitos mínimos de hardware](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview#31-processor).
- Ele tem um bloco de BIOS
- Ele não tem memória suficiente
- Um componente crítico de inicialização do sistema tem um driver bloqueado
- Não é possível atualizar a marca e modelo específicos
- Há um componente de exibição de classe com um bloco de driver que tem todos os atributos a seguir:
    - Você não substituir
    - Não há nenhum driver na nova versão do sistema operacional
    - Ele não ainda estiver no Windows Update
- Há outro componente de plug-and-play no sistema que bloqueia a atualização
- Há um componente sem fio que usa um driver de emulação XP
- Um componente de rede com uma conexão ativa perderá seu driver. Em outras palavras, após a atualização, ela poderia perder conectividade de rede.

### <a name="apps"></a>Aplicativos

Defina as **decisão de atualização** , bem como a **importância** para esse aplicativo neste plano de implantação. Para obter mais informações, consulte [como criar planos de implantação](/sccm/desktop-analytics/create-deployment-plans).

Os detalhes do aplicativo, você também pode ver as seguintes informações: Recomendações, os fatores de risco de compatibilidade e problemas conhecidos do Microsoft. Use essas informações para ajudar a definir as **decisão de atualização**. Para obter mais informações, consulte [avaliação de compatibilidade](/sccm/desktop-analytics/compat-assessment).

Os aplicativos que a análise de área de trabalho mostra como *digno de nota* baseiam-se o limite de contagem de instalação baixa para as regras de preparação do plano de implantação. Para obter mais informações, consulte [regras de preparação](/sccm/desktop-analytics/create-deployment-plans#readiness-rules).

### <a name="drivers"></a>Drivers

Consulte a lista de drivers incluído com este plano de implantação. Defina as **decisão de atualização**, examine a recomendação da Microsoft e ver os fatores de risco de compatibilidade.


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
