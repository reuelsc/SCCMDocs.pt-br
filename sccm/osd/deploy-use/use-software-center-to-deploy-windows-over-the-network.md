---
title: Usar o Centro de Software para implantar o Windows pela rede | Configuration Manager
description: "Você pode implantar um sistema operacional no Centro de Software para atualizar um computador existente com uma nova versão do Windows ou para atualizar o Windows para a versão mais recente."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 189fdac38760b75eb3795348f6af4ef7e83c3f20


---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Use o Centro de Software para implantar o Windows pela rede com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A sequência de tarefas para instalar um sistema operacional no System Center Configuration Manager pode ser disponibilizada no Centro de Software. Você pode implantar um sistema operacional no Centro de Software nos seguintes cenários de implantação de sistema operacional:  

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md)  

 Conclua as etapas em um dos cenários de implantação de sistema operacional e, então, use as seções a seguir para preparar as implantações que estão disponíveis no Centro de Software.  

## <a name="configure-deployment-settings"></a>Definir configurações de implantação  
 Quando você quiser que a implantação de sistema operacional esteja disponível no Centro de Software, você deve configurar a implantação para disponibilizar o sistema operacional para os clientes do Configuration Manager. Você pode configurá-la na página **Configurações de implantação** do Assistente de implantação de Software ou na guia **Configurações de implantação** nas propriedades de implantação.  Para a configuração **Tornar disponível para o seguinte** , configure a opção **Somente os clientes do Configuration Manager** ou **Clientes do Configuration Manager, mídia e PXE**. Depois que o sistema operacional for implantado, ele será exibido no Centro de Software para membros para a coleção de destino.  

##  <a name="a-namebkmkdeploya-deploy-the-task-sequence-to-computers"></a><a name="BKMK_Deploy"></a> Implantar a sequência de tarefas em computadores  
 Implantar o sistema operacional para uma coleção de destino. Para obter mais informações, consulte [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Quando você implanta sistemas operacionais para o Centro de Software, você pode configurar se a implantação será obrigatória ou estará disponível.  

-   **Implantação necessária**: implantações necessárias tornarão o sistema operacional disponível no Centro de Software, mas ele será iniciado automaticamente no agendamento de atribuição configurado.  

-   **Implantação disponível**: o sistema operacional estará disponível no Centro de Software e o usuário poderá instalá-lo sob demanda.  



<!--HONumber=Nov16_HO1-->


