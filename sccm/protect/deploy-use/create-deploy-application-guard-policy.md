---
title: "Criar e implantar uma política do Windows Defender Application Guard"
titleSuffix: Configuration Manager
description: "Crie e implante uma política do Windows Defender Application Guard."
ms.custom: na
ms.date: 11/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 
caps.latest.revision: "5"
author: ErikjeMS
ms.author: erikje
manager: angrobe
ms.openlocfilehash: db2508e5bbd1435fce432b6ef98d7968e68ea5ab
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="create-and-deploy-windows-defender-application-guard-policy----1351960---"></a>Criar e implantar uma política do Windows Defender Application Guard <!-- 1351960 -->

Você pode criar e implantar políticas do [Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) usando a proteção de ponto de extremidade do Configuration Manager. Essas políticas ajudam a proteger os usuários por meio da abertura de sites não confiáveis em um contêiner isolado seguro que não pode ser acessado pelas outras partes do sistema operacional.

## <a name="prerequisites"></a>Pré-requisitos

Para criar e implantar uma política do Windows Defender Application Guard, você deve usar o Windows 10 Fall Creators Update. Além disso, os dispositivos Windows 10 nos quais você implantará a política deverão ser configurados com uma política de isolamento de rede. Para obter mais informações, consulte a [Visão geral do Windows Defender Application Guard](https://docs.microsoft.com/en-us/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview). Esse recurso só funciona com versões atuais do Windows 10 Insider. Para testá-lo, os clientes deverão estar executando uma versão recente do Windows 10 Insider.


## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Crie uma política e para procurar as configurações disponíveis:

1. No console do Configuration Manager, escolha **Ativos e Conformidade**.
2. No espaço de trabalho **Ativos e Conformidade**, escolha **Visão Geral** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. Na guia **Início**, no grupo **Criar**, clique em **Criar Política do Windows Defender Application Guard**.
4. Usando a [postagem no blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97) como referência, você pode procurar e definir as configurações disponíveis.
5. Na página **Definição de Rede**, especifique a identidade corporativa e defina o limite da rede corporativa.

    > [!NOTE]
    > Os computadores Windows 10 armazenam apenas uma lista de isolamento de rede no cliente. Você pode criar dois tipos diferentes de listas de isolamento de rede e implantá-los no cliente:
    >
    >  - uma da Proteção de Informações do Windows
    >  - e uma do Windows Defender Application Guard
    >
    > Se você implantar as duas políticas, essas listas de isolamento de rede deverão ser correspondentes. Se você implantar listas que não correspondem ao mesmo cliente, a implantação falhará. Para obter mais informações, consulte a [Documentação da Proteção de Informações do Windows](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).
    > 
    > 

6. Quando tiver terminado, conclua o assistente e implante a política para um ou mais dispositivos Windows 10.

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre o Windows Defender Application Guard, veja [esta postagem no blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Além disso, para saber mais sobre o modo autônomo do Windows Defender Application Guard, veja [esta postagem no blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).
