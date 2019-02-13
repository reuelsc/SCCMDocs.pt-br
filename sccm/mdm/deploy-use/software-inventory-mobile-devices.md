---
title: Inventário de software para dispositivos móveis registrados no Microsoft Intune
titleSuffix: Configuration Manager
description: Inventário de software para dispositivos móveis registrados no Microsoft Intune.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: a0eae17a-60a8-4132-91af-0b10ad338c92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 91d298dae14c879e215b85483558898382c12055
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120735"
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
