---
title: Gerenciar aplicativos no System Center Configuration Manager | Microsoft Docs
description: Gerencie aplicativos no System Center Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: bc7bb99bc526ed0bbaaad15fc9af39fa8b7c3893
ms.lasthandoff: 03/06/2017

---
# <a name="manage-applications-in-system-center-configuration-manager"></a>Gerenciar aplicativos no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Quando você gerencia dispositivos por meio do gerenciamento de dispositivo local do Microsoft Intune ou do Configuration Manager, é possível gerenciar estes tipos de aplicativos adicionais:
- Pacote de aplicativos do Windows Phone (arquivo *.xap)
- Pacote de aplicativo para iOS (arquivo *.ipa)
- Pacote de aplicativo para Android (arquivo *.apk)
- Pacote do aplicativo para Android no Google Play
- Pacote de aplicativo do Windows Phone (na Windows Store)
- Windows Installer por meio do MDM
- Aplicativo da Web

Esta seção fornece informações detalhadas sobre como criar e gerenciar aplicativos usando o MDM híbrido ou o MDM local.

[Tarefas de gerenciamento para aplicativos do System Center Configuration Manager](../../apps/deploy-use/management-tasks-applications.md) fornece informações gerais sobre como gerenciar aplicativos do System Center Configuration Manager e os tipos de implantação.

## <a name="deploying-and-monitoring-apps"></a>Implantar e monitorar aplicativos

A implantação e monitoramento de aplicativos no System Center Configuration Manager segue os mesmos processos para dispositivos móveis usados em dispositivos locais, como laptops e desktops. Leia os tópicos a seguir para saber mais sobre a implantação e monitoramento de aplicativos:

- [Implantar aplicativos no System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md)
- [Monitorar aplicativos no System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md)

Confira aqui algumas considerações para ter em mente ao implantar e monitorar aplicativos, específicas ao gerenciamento de dispositivos móveis.

- Os dispositivos registrados em MDM não dão suporte às configurações de agendamento, às experiência do usuário nem às implantações simuladas.

- Associe a implantação com uma política de configuração de aplicativo do iOS, se você já tiver configurado uma. Confira [Configurar aplicativos iOS com políticas de configuração de aplicativo](configure-ios-apps-with-app-configuration-policies.md).

### <a name="next-steps"></a>Próximas etapas

Eventualmente, você pode querer fazer alterações em um aplicativo, desinstalá-lo ou substituir um aplicativo já implantado por um novo aplicativo. Leia [Atualizar e desativar aplicativos com o System Center Configuration Manager](../../apps/deploy-use/update-and-retire-applications.md) para entender esses recursos.

