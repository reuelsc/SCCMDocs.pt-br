---
title: Criar aplicativos do Windows Phone
titleSuffix: Configuration Manager
description: Como criar e implantar aplicativos para dispositivos Windows Phone no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 68fe11fa-5fb2-4b81-b0f5-b6f2392fb4ad
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 77eb0b750934641ceb66b2c8aa611544c654f54f
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385432"
---
# <a name="create-windows-phone-applications-in-configuration-manager"></a>Criar aplicativos do Windows Phone no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Um aplicativo do Configuration Manager tem um ou mais tipos de implantação. O tipo de implantação inclui os arquivos de instalação e as informações necessárias para implantar o software em um dispositivo. Um tipo de implantação também tem regras que especificam quando e como o software é implantado.  

Confira [Criar um aplicativo](/sccm/apps/deploy-use/create-applications#bkmk_create) para obter as etapas para criar aplicativos do Configuration Manager e tipos de implantação. 

Lembre-se também das seguintes considerações ao criar e implantar aplicativos para dispositivos Windows Phone:  


O Configuration Manager dá suporte à implantação dos seguintes tipos arquivo de aplicativo:  

|Tipo de dispositivo|Tipos de arquivos com suporte|  
|-----------------|---------------------|  
|Windows Phone 8|xap|  
|Windows Phone 8.1|xap, appx, appxbundle|
|Windows 10 Mobile|xap, appx, appxbundle|

Implante os aplicativos Windows Phone como **Disponíveis** ou **Obrigatórios**. Também use implantações para desinstalar aplicativos.  
