---
title: "Configurar o gerenciamento de dispositivo híbrido do Android com o System Center Configuration Manager e o Microsoft Intune | Microsoft Docs"
description: "Preparar para gerenciar dispositivos móveis Android com o Configuration Manager e o Intune."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
caps.latest.revision: 9
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: ab892174643e7565ad9a74abc4f83f2f152669bd


---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar o gerenciamento de dispositivo híbrido do Android com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para o System Center Configuration Manager, os usuários podem baixar o aplicativo Android do portal da empresa no Google Play, que permite que eles registrem dispositivos Android (incluindo Samsung KNOX Standard). Com o aplicativo do Android do portal da empresa, você pode gerenciar as configurações de conformidade, apagar ou excluir dispositivos Android, implantar aplicativos e coletar inventários de software e hardware. Se o aplicativo do Android do portal da empresa não estiver instalado nos dispositivos Android, você não terá todos os recursos de gerenciamento, como inventário e configurações de conformidade, mas ainda poderá implantar aplicativos nos dispositivos Android.  

## <a name="prepare-to-manage-android-mobile-devices-with-configuration-manager-and-intune"></a>Preparar para gerenciar dispositivos móveis Android com o Configuration Manager e o Intune  
 As etapas a seguir permitem ao Configuration Manager gerenciar dispositivos Android.  

#### <a name="to-enable-android-enrollment"></a>Para habilitar o registro do Android  

1.  **Pré-requisitos** – Antes de configurar o registro para qualquer plataforma, conclua os pré-requisitos e os procedimentos em [Configurar MDM híbrido](setup-hybrid-mdm.md).  

2.  No console do Configuration Manager, no espaço de trabalho **Administração** , acesse **Serviços de Nuvem** > **Assinatura do Microsoft Intune**.  

3.  Na guia **Início** do grupo **Assinatura** , clique em **Configurar Plataformas** > **Android**.  

4.  Na caixa de diálogo **Propriedades da Assinatura do Microsoft Intune** , selecione a guia **Android** e clique para marcar a caixa de seleção **Habilitar registro do Android** .  

 Depois da configuração, você precisará permitir que os usuários saibam como registrar seus dispositivos. Consulte [O que dizer aos usuários sobre o registro de seus dispositivos](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Essas informações se aplicam a dispositivos móveis gerenciados pelo Microsoft Intune e pelo Configuration Manager.



<!--HONumber=Dec16_HO3-->


