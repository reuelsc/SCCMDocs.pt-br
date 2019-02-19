---
title: Atualizar e desativar aplicativos
titleSuffix: Configuration Manager
description: Revise, substitua ou desinstale aplicativos implantados usando o System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 68ac8a07-8e54-4a3c-91e3-e50dc1cabf5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 767d6b54d19158a33b582dc3ab605d780914b18e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132809"
---
# <a name="update-and-retire-applications-with-system-center-configuration-manager"></a>Atualizar e desativar aplicativos com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Você provavelmente desejará fazer alterações em um aplicativo, desinstalá-lo ou substituir um aplicativo já implantado por um novo aplicativo. O System Center Configuration Manager oferece esses recursos para ajudá-lo a atualizar e desativar os aplicativos:  

- **Revisar aplicativos**. Quando você faz alterações em um tipo de aplicativo ou implantação, o Configuration Manager mantém um histórico dessas alterações. Você pode reverter o aplicativo para uma revisão anterior a qualquer momento. Além disso, você pode exibir suas propriedades, restaurar uma revisão anterior de um aplicativo ou excluir uma revisão antiga.  

  Para mais informações, consulte [Revisões de aplicativos](revise-and-supersede-applications.md#application-revisions).  

- **Substituir aplicativos**. Você pode atualizar ou substituir os aplicativos existentes usando uma relação de substituição. Quando você substitui um aplicativo, é possível especificar um novo tipo de implantação para substituir o tipo de implantação do aplicativo substituído. Além disso, também é possível decidir se atualiza ou desinstala o aplicativo substituído antes que o aplicativo substituto seja instalado.  

  Para mais informações, consulte [Substituição de aplicativos](revise-and-supersede-applications.md#application-supersedence).  

- **Desinstalar aplicativos**. O Configuration Manager simplifica a desinstalação de aplicativos. Ela pode ser realizada silenciosamente, sem qualquer intervenção do usuário do dispositivo ou do aplicativo.  

  Para mais informações, consulte [Desinstalar aplicativos](uninstall-applications.md).  
