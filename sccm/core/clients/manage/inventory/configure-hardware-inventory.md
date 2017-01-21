---
title: "Configurar o inventário de hardware | Microsoft Docs"
description: "Configure o inventário de hardware para todos os clientes ou para uma coleção no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1a4a9da88caba55d9e340c7fb1f31f4e3b957f3e
ms.openlocfilehash: f39714e53e1b38c162e2c0418356d223432fdd87


---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>How to configure hardware inventory in System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as etapas a seguir para configurar o inventário de hardware do System Center Configuration Manager para seu site.  

 Este procedimento define as configurações do cliente para o inventário de hardware e se aplica a todos os clientes em sua hierarquia. Se quiser que essas configurações se apliquem somente a alguns clientes, crie uma configuração personalizada do cliente de dispositivo e a atribua a uma coleção que contém os dispositivos nos quais deseja usar o inventário de hardware. Para obter mais informações sobre como criar configurações personalizadas de dispositivo, consulte [Como configurar as definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Se um dispositivo cliente receber configurações de inventário de hardware de vários conjuntos de configurações do cliente, as classes de inventário de hardware de cada conjunto de configurações serão mescladas quando o cliente relatar o inventário de hardware.  

### <a name="to-configure-hardware-inventory"></a>Para configurar o inventário de hardware  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , clique em **Configurações do Cliente**.  

3.  Clique em **Configurações do Cliente Padrão**.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Na caixa de diálogo **Configurações Padrão** , clique em **Inventário de Hardware**.  

6.  Na lista **Configurações do Dispositivo** , configure o seguinte:  

    -   **Habilitar inventário de hardware em clientes** - Na lista suspensa, selecione **True**.  

    -   **Agendamento de inventário de hardware** – Especifique o intervalo no qual os clientes coletam o inventário de hardware. Use o valor padrão de **7 dias** ou clique em **Agendamento** para configurar um intervalo personalizado.  

7.  Defina outras configurações do cliente necessárias. Para obter uma lista de configurações do cliente de inventário de hardware que podem ser definidas, consulte a seção [Inventário de Hardware](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory) no tópico [Sobre as configurações de cliente no System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).  

8.  Clique em **OK** para fechar a caixa de diálogo **Configurações Padrão** .  

 Os dispositivos cliente serão definidos com essas configurações na próxima vez que baixarem a política do cliente. Para iniciar a recuperação de política para um cliente individual, veja [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Dec16_HO3-->


