---
title: Compartilhar aplicativos no Centro de Software
titleSuffix: Configuration Manager
description: Compartilhe um link para um aplicativo no Centro de Softwares no System Center Configuration Manager.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 309a369358789e1948ab7b17ddb0e3619ae1b129
ms.sourcegitcommit: 2504617dc4db90e205327d06cab32f050e88dbf2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51505152"
---
# <a name="share-an-application-from-software-center"></a>Compartilhar aplicativo do Centro de Software

*Aplica-se a: System Center Configuration Manager (Branch Atual)* <!-- 1706 -->

Você pode copiar um hiperlink para um aplicativo no Centro de Software usando o botão ![Compartilhar](media/share15.png) **Compartilhar** no modo de exibição Detalhes do Aplicativo. Você só pode compartilhar os hiperlinks para aplicativos. Se o aplicativo ficar indisponível, o hiperlink abrirá uma janela com uma mensagem de indisponibilidade do aplicativo.

1. Escolha **Aplicativos**e escolha o aplicativo.
2. Clique no botão ![Compartilhar](media/share15.png) **Compartilhar**.
3. Clique em **Copiar** na janela.
4. Cole a URL em um email para compartilhar o aplicativo.  

> [!TIP]  
>  Para criar um link em um email do Outlook, pressione **CTRL** + **K** e cole a URL.  
>  
> Por padrão, o Outlook mostra um alerta de segurança para o protocolo da Central de Software quando o destinatário clica no link. Evite isso em seu ambiente adicionando uma chave de protocolo confiável ao Registro. Por exemplo, `HKCU\Software\Policies\Microsoft\Office\16.0\Common\Security\Trusted Protocols\All Applications\softwarecenter:`  
