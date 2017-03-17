---
title: Criar aplicativos Android | Microsoft Docs
description: "Consulte quais considerações você deverá levar em conta ao criar e implantar aplicativos para dispositivos Android."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
caps.latest.revision: 6
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 3d90b2cb1e255b9e8827a991779024ccecde9646
ms.lasthandoff: 03/06/2017

---
# <a name="create-android-applications-with-system-center-configuration-manager"></a>Criar aplicativos Android com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Um aplicativo do System Center Configuration Manager tem um ou mais tipos de implantação que abrangem os arquivos de instalação e as informações necessárias para implantar o software em um dispositivo. Um tipo de implantação também tem regras que especificam quando e como o software é implantado.  

 Você pode criar aplicativos com os seguintes métodos:  

-   Crie automaticamente os aplicativos e tipos de implantação, lendo os arquivos de instalação do aplicativo.  

-   Crie manualmente o aplicativo e adicione tipos de implantação posteriormente.  

-   Importe um aplicativo de um arquivo.  

Veja [Iniciar o assistente para criar aplicativo](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) e conheça as etapas necessárias para criar os aplicativos do Configuration Manager e os tipos de implantação. Além disso, lembre-se das seguintes considerações ao criar e implantar aplicativos para dispositivos Android.  

## <a name="general-considerations"></a>Considerações gerais

O Configuration Manager dá suporte à implantação dos seguintes tipos de aplicativos para Android:

|Tipo de dispositivo|Arquivos com suporte|
|-|-|
|Android|.apk|

Há suporte para as seguintes ações de implantação:

|Tipo de dispositivo|Ações com suporte|
|-|-|
|Android|**Disponível**, **Necessário**. O usuário deve concordar com a instalação e com a desinstalação.

