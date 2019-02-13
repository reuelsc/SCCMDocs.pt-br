---
title: Configurar gerenciamento adicional
titleSuffix: Configuration Manager
description: Configure o gerenciamento adicional usando o System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 4877d674-6bbc-4e16-810c-daad70c74daa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d866ce901640b6e7fafb13a6c24318f26c5d5feb
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131788"
---
# <a name="set-up-additional-management-with-system-center-configuration-manager"></a>Configurar o gerenciamento adicional usando o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

(Opcional) Você pode configurar o gerenciamento adicional antes dos dispositivos serem registrados. Essas soluções de gerenciamento podem ser criadas e implantadas após a dispositivos serem registrados, embora muitas empresas prefiram implantá-las conforme os dispositivos são trazidos para o gerenciamento.

Os **Itens de configuração** permitem que você gerencie as configurações como exigir um PIN ou exigir criptografia em dispositivos registrados com base na plataforma de dispositivo:
- [Dispositivos Windows 10 e Windows 8.1](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Dispositivos Windows Phone](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)
- [Dispositivos iOS e Mac](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)
- [Dispositivos Android e Samsung KNOX Standard](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)

Os **Aplicativos** podem ser implantados em dispositivos gerenciados:
- [Aplicativos iOS](creating-ios-applications.md)
- [Aplicativos Mac](../../apps/get-started/creating-mac-computer-applications.md)
- [Aplicativos de computador Windows](../../apps/get-started/creating-windows-applications.md)
- [Aplicativos de Windows Phone](creating-windows-phone-applications.md)
- [Aplicativos Android](creating-android-applications.md)

O **Acesso condicional** permite que você gerencie o acesso aos recursos da empresa, incluindo:  
- [Acesso ao email](manage-email-access.md)
- [Acesso ao SharePoint](manage-sharepoint-online-access.md)
- [Acesso ao Skype for Business](manage-skype-for-business-online-access.md)
- [Dynamics CRM Online](manage-dynamics-crm-online-access.md)

**Autenticação Multifator (MFA)** permite que você exija mais de um método de verificação, o que adiciona uma segunda camada crítica de segurança aos logons de usuário e transações.
Anteriormente, você tinha que ir para o console do Intune ou para o console do Configuration Manager para definir o MFA para inscrições do Intune. Agora, faça logon no [Portal do Microsoft Azure](https://manage.windowsazure.com) usando suas credenciais do Intune e defina as configurações da MFA por meio do Azure AD. Saiba mais em[Autenticação Multifator para o Microsoft Intune](https://aka.ms/mfa_ad).

> [!div class="button"]
> [< Etapa anterior](enable-platform-enrollment.md)  [Próxima etapa >](verify-mdm-configuration.md)
