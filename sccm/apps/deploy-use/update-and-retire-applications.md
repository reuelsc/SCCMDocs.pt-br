---
title: Atualizar e desativar aplicativos | Microsoft Docs
description: Revise, substitua ou desinstale aplicativos implantados usando o System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68ac8a07-8e54-4a3c-91e3-e50dc1cabf5d
caps.latest.revision: "9"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 805e04c447747b4d12350b692880dbc005bd7168
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="update-and-retire-applications-with-system-center-configuration-manager"></a>Atualizar e desativar aplicativos com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Você provavelmente desejará fazer alterações em um aplicativo, desinstalá-lo ou substituir um aplicativo já implantado por um novo aplicativo. O System Center Configuration Manager oferece esses recursos para ajudá-lo a atualizar e desativar os aplicativos:  

-   **Revisar aplicativos**. Quando você faz alterações em um tipo de aplicativo ou implantação, o Configuration Manager mantém um histórico dessas alterações. Você pode reverter o aplicativo para uma revisão anterior a qualquer momento. Além disso, você pode exibir suas propriedades, restaurar uma revisão anterior de um aplicativo ou excluir uma revisão antiga.  

  Para mais informações, consulte [Revisões de aplicativos](revise-and-supersede-applications.md#application-revisions).  

-   **Substituir aplicativos**. Você pode atualizar ou substituir os aplicativos existentes usando uma relação de substituição. Quando você substitui um aplicativo, é possível especificar um novo tipo de implantação para substituir o tipo de implantação do aplicativo substituído. Além disso, também é possível decidir se atualiza ou desinstala o aplicativo substituído antes que o aplicativo substituto seja instalado.  

  Para mais informações, consulte [Substituição de aplicativos](revise-and-supersede-applications.md#application-supersedence).  

-   **Desinstalar aplicativos**. O Configuration Manager simplifica a desinstalação de aplicativos. Ela pode ser realizada silenciosamente, sem qualquer intervenção do usuário do dispositivo ou do aplicativo.  

  Para mais informações, consulte [Desinstalar aplicativos](uninstall-applications.md).  
