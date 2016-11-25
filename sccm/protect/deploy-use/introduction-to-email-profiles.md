---
title: "Introdução aos perfis de email | System Center Configuration Manager"
description: "Saiba como usar perfis de email para permite que os usuários acessem email corporativo em seus dispositivos com uma configuração mínima."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c4e2dc48-91c2-438f-9e1a-947b1125b0e2
caps.latest.revision: 3
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 83066e1f0e3c6536649e9b74ca13562c9d817619


---
# <a name="introduction-to-email-profiles-in-system-center-configuration-manager"></a>Introdução aos perfis de email no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os perfis de email funcionam com o Microsoft Intune para permitir que você provisione dispositivos com restrições e perfis de email usando o Exchange ActiveSync. Isso permite que os usuários acessem email corporativo em seus dispositivos com uma configuração mínima exigida de sua parte.  

 Você pode configurar os seguintes tipos de dispositivo com perfis de email:  

-   Dispositivos que executam o Windows Phone 8  

-   Dispositivos que executam o Windows Phone 8.1  

-   Dispositivos que executam o Windows 10 Mobile  

-   Dispositivos IPhone que executam o iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivos IPad que executam o iOS 5, iOS 6, iOS 7 e iOS 8  

> [!IMPORTANT]  
>  Para implantar perfis em dispositivos iOS, Android, Samsung KNOX, Windows Phone e Windows 8.1 ou 10, esses dispositivos devem ser registrados no Intune. Para obter informações sobre como registrar seus dispositivos, veja [Gerenciar dispositivos móveis com o Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

 Além de configurar uma conta de email no dispositivo, você também pode configurar as configurações de sincronização de contatos, calendários e tarefas.  

 Ao criar um perfil de email, você pode incluir uma grande variedade de configurações de segurança, inclusive certificados de identidade, criptografia e assinatura que foram provisionados usando os perfis de certificado do System Center Configuration Manager. Para obter mais informações sobre perfis de certificado, consulte [Perfis de certificado do System Center Configuration Manager](introduction-to-certificate-profiles.md).  



<!--HONumber=Nov16_HO1-->


