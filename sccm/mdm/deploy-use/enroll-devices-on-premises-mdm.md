---

title: Gerenciar dispositivos | Microsoft Docs
description: "Conheça os métodos para registrar dispositivos para o gerenciamento de dispositivo móvel local no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
caps.latest.revision: 6
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 8f9667388c3557a84fc84c742e25f0c3bd2e2a5f
ms.lasthandoff: 03/06/2017


---
# <a name="enroll-devices-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Registrar dispositivos para o gerenciamento de dispositivo móvel local no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para gerenciar computadores e dispositivos com o Gerenciamento de Dispositivo Móvel Local do System Center Configuration Manager, os dispositivos precisam ser registrados para que o Configuration Manager possa se comunicar com os dispositivos para tarefas de gerenciamento. O Configuration Manager fornece dois métodos para o registro de dispositivos:  

-   **Registro de usuário** - Nesse método, os usuários iniciam o processo de registro em seus dispositivos. Para que o registro de usuário seja bem-sucedido, o dispositivo deve ter um certificado raiz confiável instalado e o usuário deve ser provisionado para registro pelo Configuration Manager.  Para registrar o dispositivo, basta que o usuário forneça as credenciais de trabalho e o dispositivo é registrado para ser gerenciado.  

     Para mais informações, consulte [Como os usuários registram dispositivos com o Gerenciamento de Dispositivo Móvel Local no System Center Configuration Manager](../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

-   **Registro em massa** - Nesse método, o usuário do dispositivo não é obrigado a iniciar o registro. Em vez disso, um pacote de registro em massa criado no Configuration Manager e é colocado no dispositivo e aberto. Quando aberto, o pacote fornece as informações necessárias para registrar o dispositivo.  

     Para mais informações, consulte [Como registrar dispositivos em massa com o Gerenciamento de Dispositivo Móvel Local no System Center Configuration Manager](../../mdm/deploy-use/bulk-enroll-devices-on-premises-mdm.md)  

 > [!NOTE]  
>  O branch atual do Configuration Manager dá suporte ao registro no Gerenciamento de Dispositivo Móvel Local para dispositivos que executam os seguintes sistemas operacionais:  
>   
>  -   Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team \(a partir do Configuration Manager versão 1602\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise   

