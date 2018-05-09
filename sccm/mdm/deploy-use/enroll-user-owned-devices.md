---
title: Registrar dispositivos do usuário para implantações híbridas
titleSuffix: Configuration Manager
description: Conheça os diferentes métodos para registrar dispositivos do usuário para implantações híbridas com o Configuration Manager.
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 2bdaa8a7-6a64-4b0e-b617-309dcd912c45
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 198e5b65b85e10a1aa64f06361f1ba425e156662
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="enroll-user-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Registrar dispositivos do usuário para implantações híbridas com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Dispositivos de propriedade do usuário podem ser colocados no gerenciamento registrando-os, geralmente, um processo chamado "traga seus próprios dispositivos" ou simplesmente "BYOD". Os usuários fazem isso instalando o aplicativo de Portal da Empresa e entrando no dispositivo (iOS, macOS e Android) ou adicionando uma conta corporativa ou de estudante ao dispositivo e ingressando em um domínio (Windows). Esse processo registra o dispositivo no Intune, concedendo ao usuário acesso aos recursos gerenciados pelo Intune e permitindo que o Intune gerencie determinadas configurações de dispositivo, como exigir um PIN.

Para colocar os dispositivos no gerenciamento, como um administrador, você deve primeiro [configurar o gerenciamento de dispositivo móvel](setup-hybrid-mdm.md) e [habilitar o registro](enable-platform-enrollment.md). Após habilitar o registro, os usuários podem registrar seus próprios dispositivos. Consulte [Como instruir os usuários finais sobre o Microsoft Intune](https://docs.microsoft.com/intune/end-user-educate) para considerações e etapas para compartilhar com os usuários.

Empresas ou escolas que adquirem dispositivos podem tirar proveito dos programas que permitem que você [gerencie dispositivos da empresa](enroll-company-owned-devices.md).
