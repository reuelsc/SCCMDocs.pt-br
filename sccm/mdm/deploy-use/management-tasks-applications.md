---
title: Gerenciar aplicativos
titleSuffix: Configuration Manager
description: Gerencie aplicativos no System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a57beb79bf7e4dc51e72d7254ff0f190c6ca32c4
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62227992"
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

- Não adicione mais de 100 localidades para um único aplicativo. Adição de mais de 100 localidades impede que o aplicativo está sincronizando com o Intune. Essa ação também impede que o aplicativo que está sendo instalado ou sendo disponível para instalação no dispositivo.

- Associe a implantação com uma política de configuração de aplicativo do iOS, se você já tiver configurado uma. Confira [Configurar aplicativos iOS com políticas de configuração de aplicativo](configure-ios-apps-with-app-configuration-policies.md).

### <a name="next-steps"></a>Próximas etapas

Eventualmente, você pode querer fazer alterações em um aplicativo, desinstalá-lo ou substituir um aplicativo já implantado por um novo aplicativo. Leia [Atualizar e desativar aplicativos com o System Center Configuration Manager](../../apps/deploy-use/update-and-retire-applications.md) para entender esses recursos.
