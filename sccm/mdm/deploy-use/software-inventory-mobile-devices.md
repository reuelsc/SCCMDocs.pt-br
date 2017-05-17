---
title: "Inventário de software para dispositivos móveis registrados no Microsoft Intune | Microsoft Docs"
description: "Inventário de software para dispositivos móveis registrados no Microsoft Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0eae17a-60a8-4132-91af-0b10ad338c92
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 2ed79d02535768de136947e4a5b63ad186d9a3cd
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017

---
# <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Inventário de software para dispositivos móveis registrados no Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 É possível coletar o inventário de aplicativos instalados nos dispositivos móveis. Os aplicativos inventariados dependerão se o dispositivo é de propriedade corporativa ou pessoal. Para dispositivos pessoais, somente aplicativos inventariados são aplicativos que são gerenciados pelo Microsoft Intune.  

> [!NOTE]  
>  O inventário de aplicativos instalados em dispositivos móveis é coletado como parte do processo de [inventário de hardware](mobile-device-hardware-inventory-hybrid.md).  

 Aqui estão os aplicativos inventariados para dispositivos pessoais ou corporativos.  

|Plataforma|Para dispositivos pessoais|Para dispositivos corporativos|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (sem o cliente do Configuration Manager)|Somente aplicativos gerenciados|Somente aplicativos gerenciados|
|Windows 8.1 (sem o cliente do Configuration Manager)|Somente aplicativos gerenciados|Somente aplicativos gerenciados|  
|Windows Phone 8|Somente aplicativos gerenciados|Somente aplicativos gerenciados|  
|Windows RT|Somente aplicativos gerenciados|Somente aplicativos gerenciados|  
|iOS|Somente aplicativos gerenciados|Todos os aplicativos instalados no dispositivo|  
|Android|Somente aplicativos gerenciados|Todos os aplicativos instalados no dispositivo|  

Confira [Introdução ao inventário de software](../../core/clients/manage/inventory/introduction-to-software-inventory.md) e [Como configurar o inventário de software ](../../core/clients/manage/inventory/configure-software-inventory.md) para obter informações detalhadas sobre como usar o inventário de software para coletar informações de arquivo em dispositivos cliente.

