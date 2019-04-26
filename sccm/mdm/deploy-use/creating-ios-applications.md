---
title: Criar aplicativos para iOS
titleSuffix: Configuration Manager
description: Como criar e implantar aplicativos para dispositivos iOS no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ff633013-5313-4cd3-949c-56d45e777280
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e4a2d84fe31c3a524b876e3beb34f0e3d25d0089
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62251376"
---
# <a name="create-ios-applications-in-configuration-manager"></a>Criar aplicativos iOS no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Um aplicativo do Configuration Manager tem um ou mais tipos de implantação que abrangem os arquivos de instalação e as informações necessárias para implantar o software em um dispositivo. Um tipo de implantação também tem regras que especificam quando e como o software é implantado.  

Confira [Criar um aplicativo](/sccm/apps/deploy-use/create-applications#bkmk_create) para obter as etapas para criar aplicativos do Configuration Manager e tipos de implantação. 

Lembre-se das seguintes considerações ao criar e implantar aplicativos para dispositivos iOS:  

- O Configuration Manager dá suporte à implantação de pacotes .ipa do iOS. Não é necessário especificar um arquivo (.plist) de lista de propriedade ao importar um aplicativo iOS. 

- Implante aplicativos iOS como **Disponível** ou **Obrigatório**. O usuário deve concordar com a instalação e com a desinstalação.

> [!IMPORTANT]  
>  No momento, os usuários finais não conseguem instalar aplicativos corporativos usando o aplicativo Portal da Empresa do Microsoft Intune para iOS. Essa limitação existe porque há restrições para aplicativos publicados na iOS App Store. [Confira as App Store Review Guidelines (Diretrizes de Revisão da App Store), seção 2]. Os usuários podem instalar aplicativos corporativos navegando até o portal do Intune em seu dispositivo. Esses aplicativos incluem pacotes de aplicativos de linha de negócios e de aplicativos da App Store gerenciados. Para obter mais informações sobre as funcionalidades de gerenciamento móvel habilitadas pelo aplicativo Portal da Empresa do Intune, confira [Funcionalidades de gerenciamento de dispositivo registrado no Microsoft Intune](https://docs.microsoft.com/intune/device-enrollment).  
