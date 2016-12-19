---
title: Criar aplicativos iOS | Microsoft Docs
description: "Consulte quais considerações você deverá levar em conta ao criar e implantar aplicativos para dispositivos iOS."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d5420109-6538-4430-9ca6-db352ee84c2e
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: e9e34359f4412ba07b9fb49f871a1eb2d36cecf8
ms.openlocfilehash: eb2d1245932d71bd10fd63d95a155eae7d128836


---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>Criar aplicativos iOS com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Lembre-se das seguintes considerações ao criar e implantar aplicativos para dispositivos iOS.  

## <a name="general-considerations"></a>Considerações gerais  
 O Configuration Manager dá suporte à implantação dos seguintes tipos de aplicativo:  

|Tipo de dispositivo|Arquivos com suporte|  
|-----------------|---------------------|  
|iOS|*.ipa<br /><br /> No System Center Configuration Manager, não é necessário especificar um arquivo (.plist) de lista de propriedade ao importar um aplicativo iOS.|  

 Há suporte para as seguintes ações de implantação:  

|Tipo de dispositivo|Ações com suporte|  
|-----------------|-----------------------|  
|iOS|**Disponível**, **Necessário**. O usuário deve concordar com a instalação e com a desinstalação.

> [!IMPORTANT]  
>  No momento, os usuários finais não conseguem instalar aplicativos corporativos do aplicativo de Portal da Empresa do Microsoft Intune para iOS. Isso ocorre porque há restrições colocadas em aplicativos que são publicados na iOS App Store (consulte Diretrizes de análise da App Store, seção 2). Os usuários podem instalar aplicativos corporativos (incluindo aplicativos gerenciados da App Store e pacotes de aplicativos de linha de negócios) navegando até o Portal da Web do Intune no dispositivo deles (portal.manage.microsoft.com). Para obter mais informações sobre os recursos de gerenciamento móvel que são habilitados pelo aplicativo do Portal da Empresa do Intune, consulte [Recursos de gerenciamento de dispositivo registrado do Microsoft Intune](https://technet.microsoft.com/library/dn600287.aspx).  



<!--HONumber=Dec16_HO3-->


