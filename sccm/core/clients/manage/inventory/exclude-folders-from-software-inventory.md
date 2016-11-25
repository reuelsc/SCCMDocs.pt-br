---
title: "Excluir pastas do inventário de software | System Center Configuration Manager"
description: "Excluir pastas do inventário de software no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 07328e086a09e924a4807b05759937929152bda9


---
# <a name="how-to-exclude-folders-from-software-inventory-in-system-center-configuration-manager"></a>Como excluir pastas do inventário de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as etapas a seguir para configurar o inventário de software do System Center Configuration Manager para seu site.  

 Este procedimento define as configurações do cliente para o inventário de software e se aplica a todos os computadores em sua hierarquia. Se quiser que essas configurações se apliquem somente a alguns computadores, crie uma configuração personalizada do cliente de dispositivo e a atribua a uma coleção que contém os computadores nos quais deseja usar o inventário de software. Para obter mais informações sobre como criar configurações personalizadas de dispositivo, consulte [Como configurar as definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

### <a name="to-configure-software-inventory"></a>Para configurar o inventário de software  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , clique em **Configurações do Cliente**.  

3.  Clique em **Configurações do Cliente Padrão**.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Na caixa de diálogo **Configurações Padrão** , clique em **Inventário de Software**.  

6.  Na lista **Configurações do Dispositivo** , configure os seguintes valores:  

    -   **Habilitar inventário de software em clientes** – Na lista suspensa, selecione **Verdadeiro**.  

    -   **Programar agendamento do inventário de software e da coleção de arquivos** – Configura o intervalo no qual os clientes coletam inventário de software e arquivos. Use o valor padrão de **7 dias** ou clique em **Agendamento** para configurar um intervalo personalizado.  

7.  Defina as configurações do cliente necessárias. Para obter uma lista de configurações do cliente de inventário de software que podem ser definidas, veja a seção [Inventário de Software](../../../../core/clients/deploy/about-client-settings.md#BKMK_SoftInventoryDeviceSettings) no tópico [Sobre configurações de cliente no System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).  

8.  Clique em **OK** para fechar a caixa de diálogo **Definir Configuração do Cliente** .  

 Os computadores cliente serão definidos com essas configurações durante o próximo download da política do cliente. Para iniciar a recuperação de política para um cliente individual, veja [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Nov16_HO1-->


