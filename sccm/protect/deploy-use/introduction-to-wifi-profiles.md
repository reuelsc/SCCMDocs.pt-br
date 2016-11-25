---
title: "Introdução aos perfis de Wi-Fi | System Center Configuration Manager"
description: "Saiba como usar perfis de Wi-Fi no System Center Configuration Manager para implantar as configurações de rede sem fio para usuários em sua organização."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 86725460-c2f3-49ed-90aa-6b2724d34d69
caps.latest.revision: 8
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 30fefb291a6fccb630d5e3272ce7266339c9139c


---
# <a name="introduction-to-wi-fi-profiles-in-system-center-configuration-manager"></a>Introdução aos perfis de Wi-Fi no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use perfis de Wi-Fi no System Center Configuration Manager para implantar as configurações de rede sem fio para usuários na sua organização. Ao implantar essas configurações, você minimiza o esforço do usuário final necessário para conectar-se à rede sem fio.  

 Por exemplo, você instalou uma nova rede Wi-Fi chamada **Contoso Wi-Fi**. Agora você deseja provisionar todos os dispositivos que executam o sistema operacional iOS com as configurações necessárias para conectar-se a essa rede. Você pode criar um perfil de Wi-Fi contendo as configurações necessárias para conectar-se à rede sem fio **Contoso Wi-Fi** . Em seguida, você pode implantar esse perfil a todos os usuários que possuem dispositivos que executam o iOS na sua hierarquia. Os usuários de dispositivos iOS veem a rede da empresa na lista de redes sem fio e prontamente podem se conectar a essa rede.  

 Você pode configurar os seguintes tipos de dispositivo com perfis Wi-Fi:  

-   Dispositivos que executam o Windows 8.1 32 bits  

-   Dispositivos que executam o Windows 8.1 64-bit  

-   Dispositivos que executam o Windows RT 8.1  

-   Dispositivos que executam o Windows Phone 8.1  

-   Dispositivos que executam o Windows 10 Desktop ou Mobile  

-   Dispositivos IPhone que executam o iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivos IPad que executam o iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivos Android que executam a versão 4  

> [!IMPORTANT]  
>  Para implantar perfis em dispositivos Android, iOS, Windows Phone e em dispositivos Windows 8.1 ou posteriores registrados, esses dispositivos devem ser registrados no Microsoft Intune]. Para obter informações sobre como registrar seus dispositivos, veja [Gerenciar dispositivos móveis com o Microsoft Intune](https://technet.microsoft.com/library/dn646962.aspx).  

 Ao criar um perfil Wi-Fi, você pode incluir uma várias configurações de segurança. Essas configurações incluem os certificados para validação de servidor e autenticação de cliente que foram provisionados com os perfis de certificado do Configuration Manager. Para obter mais informações sobre perfis de certificado, consulte [Perfis de certificado do System Center Configuration Manager](introduction-to-certificate-profiles.md).  



<!--HONumber=Nov16_HO1-->


