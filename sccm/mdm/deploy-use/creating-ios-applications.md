---
title: Criar aplicativos para iOS
titleSuffix: Configuration Manager
description: "Consulte quais considerações você deverá levar em conta ao criar e implantar aplicativos para dispositivos iOS."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff633013-5313-4cd3-949c-56d45e777280
caps.latest.revision: 
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 2b21a50b18384740eda8744c3442fe060325fd15
ms.sourcegitcommit: 52080ef1b0f9a27c123711ef274ac3ffe070e8e0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2018
---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>Criar aplicativos iOS com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Um aplicativo do System Center Configuration Manager tem um ou mais tipos de implantação que abrangem os arquivos de instalação e as informações necessárias para implantar o software em um dispositivo. Um tipo de implantação também tem regras que especificam quando e como o software é implantado.  

 Você pode criar aplicativos com os seguintes métodos:  

-   Crie automaticamente os aplicativos e tipos de implantação, lendo os arquivos de instalação do aplicativo.  

-   Crie manualmente o aplicativo e adicione tipos de implantação posteriormente.  

-   Importe um aplicativo de um arquivo.  

Veja [Iniciar o assistente para criar aplicativo](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) e conheça as etapas necessárias para criar os aplicativos do Configuration Manager e os tipos de implantação. Além disso, lembre-se das seguintes considerações ao criar e implantar aplicativos para dispositivos iOS.  

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
