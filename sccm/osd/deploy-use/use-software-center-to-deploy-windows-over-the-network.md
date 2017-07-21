---
title: Usar o Centro de Software para implantar o Windows pela rede | Microsoft Docs
description: "Você pode implantar um sistema operacional no Centro de Software para atualizar um computador existente com uma nova versão do Windows ou para atualizar o Windows para a versão mais recente."
ms.custom: na
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
caps.latest.revision: 5
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: f4c46bfab9b40b29654f4e883817a5508ab25b74
ms.openlocfilehash: 8988409c68b7f69439ed03872c316b2139d25616
ms.contentlocale: pt-br
ms.lasthandoff: 06/28/2017


---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Use o Centro de Software para implantar o Windows pela rede com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode disponibilizar a sequência de tarefas para instalar um sistema operacional no System Center Configuration Manager no Centro de Software. Você pode implantar um sistema operacional no Centro de Software nos seguintes cenários de implantação de sistema operacional:

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md)

Conclua as etapas em um dos cenários de implantação de sistema operacional. Em seguida, use as seções a seguir para preparar para implantações disponíveis no Centro de Software.

## <a name="configure-deployment-settings"></a>Definir configurações de implantação  
Para disponibilizar a implantação de sistema operacional no Centro de Software, configure a implantação. Você pode configurar a implantação na página **Configurações de Implantação** do Assistente de Implantação de Software ou na guia **Configurações de Implantação** nas propriedades de implantação. Para a configuração **Tornar disponível para o seguinte** , configure a opção **Somente os clientes do Configuration Manager** ou **Clientes do Configuration Manager, mídia e PXE**. Após a implantação do sistema operacional pelo sistema, o sistema operacional será exibido no Centro de Software para membros da coleção de destino.

##  <a name="BKMK_Deploy"></a> Implantar a sequência de tarefas em computadores  
Implantar o sistema operacional para uma coleção de destino. Para obter mais informações, consulte [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Quando você implanta sistemas operacionais para o Centro de Software, você pode configurar se a implantação será obrigatória ou estará disponível.

-   **Implantação necessária**: implantações necessárias tornarão o sistema operacional disponível no Centro de Software, mas ele será iniciado automaticamente no agendamento de atribuição configurado.

-   **Implantação disponível**: o sistema operacional estará disponível no Centro de Software e o usuário poderá instalá-lo sob demanda.

