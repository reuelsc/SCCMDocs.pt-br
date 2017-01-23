---
title: "Configurar o inventário de hardware | Microsoft Docs"
description: "Configure o inventário de hardware para todos os clientes ou para uma coleção no System Center Configuration Manager."
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 05c27c7aa36e0b4236867766dab36125c31467b3
ms.openlocfilehash: deed112cca011b3b410c1197b7abf0f36a864f3c


---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>How to configure hardware inventory in System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este procedimento define as configurações do cliente para o inventário de hardware e se aplica a todos os clientes em sua hierarquia. Se quiser que essas configurações se apliquem somente a alguns clientes, crie uma configuração personalizada do cliente de dispositivo e a atribua a uma coleção que contém os dispositivos nos quais deseja usar o inventário de hardware. Consulte [Como definir as configurações do cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Se um dispositivo cliente receber configurações de inventário de hardware de vários conjuntos de configurações do cliente, as classes de inventário de hardware de cada conjunto de configurações serão mescladas quando o cliente relatar o inventário de hardware.  

### <a name="to-configure-hardware-inventory"></a>Para configurar o inventário de hardware  

1.  No console do Configuration Manager, escolha **Administração** > **Configurações do Cliente** > **Configurações do Cliente Padrão**.  

4.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

5.  Na caixa de diálogo **Configurações Padrão**, escolha **Inventário de Hardware**.  

6.  Na lista **Configurações do Dispositivo** , configure o seguinte:  

    -   **Habilitar o inventário de hardware em clientes** – selecione **True**.  

    -   **Agendamento de inventário de hardware** – clique em **Agendamento** para especificar o intervalo no qual os clientes coletam o inventário de hardware.  

7.  Defina outras [configurações do cliente de inventário de hardware](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory) necessárias.  

Os dispositivos cliente serão definidos com essas configurações na próxima vez que baixarem a política do cliente. Para iniciar a recuperação de política para um cliente individual, veja [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Jan17_HO1-->


