---
title: Configurar o inventário de hardware
titleSuffix: Configuration Manager
description: Configure o inventário de hardware para todos os clientes ou para uma coleção no System Center Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fecaa5a9fb74c9f8d473cc9dba6a307800fd70f9
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499941"
---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>How to configure hardware inventory in System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este procedimento define as configurações do cliente para o inventário de hardware e se aplica a todos os clientes em sua hierarquia. Se quiser que essas configurações se apliquem somente a alguns clientes, crie uma configuração personalizada do cliente de dispositivo e a atribua a uma coleção que contém os dispositivos nos quais deseja usar o inventário de hardware. Consulte [Como definir as configurações do cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Se um dispositivo cliente receber configurações de inventário de hardware de vários conjuntos de configurações do cliente, as classes de inventário de hardware de cada conjunto de configurações serão mescladas quando o cliente relatar o inventário de hardware. Além disso, não marcar uma classe em uma configuração com uma prioridade mais alta do cliente personalizado não desabilita a inclusão dessa classe no inventário pelo cliente. 

Para desabilitar uma classe de inventário de hardware específica na maioria dos sistemas, exceto alguns, a classe precisa ser desmarcada nas configurações do cliente padrão. Em seguida, crie uma configuração do cliente personalizada para habilitar a classe e implante-a nos sistemas de destino.


### <a name="to-configure-hardware-inventory"></a>Para configurar o inventário de hardware  

1.  No console do Configuration Manager, escolha **Administração** > **Configurações do Cliente** > **Configurações do Cliente Padrão**.  

4.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

5.  Na caixa de diálogo **Configurações Padrão**, escolha **Inventário de Hardware**.  

6.  Na lista **Configurações do Dispositivo** , configure o seguinte:  

    -   **Habilitar o inventário de hardware em clientes** – selecione **Sim**.  

    -   **Agendamento de inventário de hardware** – clique em **Agendamento** para especificar o intervalo no qual os clientes coletam o inventário de hardware.  

7.  Defina outras [configurações do cliente de inventário de hardware](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory) necessárias.  

Os dispositivos cliente serão definidos com essas configurações na próxima vez que baixarem a política do cliente. Para iniciar a recuperação de política para um cliente individual, veja [Como gerenciar clientes no System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  
