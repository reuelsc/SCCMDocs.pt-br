---
title: Escolher Intune autônomo
titleSuffix: Configuration Manager
description: Escolher Intune autônomo
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 32c28eef77976d83f881a17595fb5e9ec4bb08d4
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898283"
---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mdm-with-configuration-manager"></a>Escolha entre o Microsoft Intune autônomo e o MDM híbrido com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


A partir de 14 de agosto de 2018, o gerenciamento de dispositivo móvel (MDM) híbrido é uma [recurso preterido](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). O Intune no Azure é a solução de MDM recomendada pela Microsoft.  

Para saber mais, confira [O que é o MDM híbrido](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  


<!--
One of the most commonly asked questions regarding mobile device management (MDM) with Microsoft Intune is "Should I integrate Intune with Configuration Manager (hybrid MDM) or run Intune standalone in the cloud only configuration?" 



 
## Intune standalone

Intune standalone is Microsoft’s recommended deployment topology. Intune standalone is a cloud-only MDM solution that you manage using a web console accessed from anywhere in the world. Intune data centers are hosted in North America, Europe, and Asia. Because Intune is a cloud service, you can quickly deploy Intune management to your devices.

Customers generally find it faster and easier to deploy the standalone topology because there's no dependency for on-premise components. Intune standalone is now on the Microsoft Azure cloud platform and provides many advanced features, such as:  

- Integrated enterprise mobility management platform: An integrated cloud platform and admin experience in Azure portal for Intune, Azure AD Premium, and Azure Information Protection  

- Mobile device management: Rich mobile device management and information protection capabilities  

- Scale: Deploy and manage mobile devices without worrying about scale  

- Role-based access control: Restrict access to administrative functions based on assigned roles and scopes  

- Programmatic access (API): Microsoft Graph API support, and SDK and PowerShell management options  

- Web console: An HTML 5-based console built on web standards with support for most modern web browsers  

- Advanced reporting: Ability to create customized reports  

- Agility: Simple setup and rapid delivery of new capabilities  



## Hybrid MDM with Configuration Manager

> [!Important]  
> As of August 14, 2018, hybrid mobile device management is a [deprecated feature](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). For more information, see [What is hybrid MDM](/sccm/mdm/understand/hybrid-mobile-device-management).  

Hybrid MDM is a solution that integrates Intune's mobile device management capabilities into Configuration Manager. It uses Intune as the delivery channel for policies, profiles, and applications to devices but uses Configuration Manager on-premises infrastructure to administer content and manage the devices. A hybrid implementation gives you "single pane of glass" control. This means you can use the same on-premises infrastructure and administrative console to manage mobile devices with Intune as well as PCs and servers with the traditional Configuration Manager client. 

You may choose hybrid MDM for the following reasons:  

- You want to manage both mobile devices enrolled in Intune and devices managed with the Configuration Manager client from the same administrative console  

- Your infrastructure requires that you have multiple NDES servers for certificate delivery to mobile devices  

- Your infrastructure requires that you have multiple Exchange connectors  

- You require S/MIME encryption support

> [!Note]  
> If you set up hybrid MDM in Configuration Manager for conditional access with on-premises Exchange, users can still access email in Outlook for iOS and Android. This same configuration with Intune standalone blocks email for these clients.<!--Intune bug 2285890-->  



#### <a name="change-the-mdm-authority"></a>Alterar a autoridade de MDM

Se precisar alterar a configuração da autoridade MDM, você pode alterá-la por conta própria sem precisar entrar em contato com o Suporte da Microsoft e sem a necessidade de cancelar o registro e registrar novamente os dispositivos gerenciados existentes. Para obter mais informações, consulte [alterar sua autoridade MDM](/sccm/mdm/deploy-use/change-mdm-authority).

