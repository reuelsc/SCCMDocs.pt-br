---

title: "Manutenção de atualizações de software | Configuration Manager"
description: "Para manter as atualizações no Configuration Manager, você pode agendar a tarefa de limpeza do WSUS ou executá-la manualmente."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1495aa474c39723767ec2d81bc60eb1582ac5504



---
# <a name="software-updates-maintenance"></a>Manutenção de atualizações de software

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode agendar e executar a tarefa de limpeza do WSUS do Configuration Manager ou executá-la manualmente nas propriedades do Componente de Ponto de Atualização de Software. Quando você seleciona para executar a tarefa de limpeza do WSUS, ela será executada na próxima sincronização de atualizações de software. As atualizações expiradas do software serão definidas com o status de recusadas no servidor WSUS, e o Windows Update Agent nos computadores não verificará mais essas atualizações de software. Por padrão, a tarefa de limpeza do WSUS é executada a cada 30 dias.  

#### <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>Para agendar e executar o trabalho de limpeza do WSUS  

1.  No console do Configuration Manager, navegue até **Administração** > **Visão Geral** > **Configuração de Site** > **Sites**.  

2.  Clique em **Configurar componentes do Site** no grupo **Configurações** e, em seguida, clique em **Ponto de atualização de Software** para abrir as propriedades do componente do Ponto de atualização de Software.  

3.  Clique na guia **Regras de substituição** , selecione **Executar o assistente de limpeza do WSUS**e, em seguida, clique em **OK**.



<!--HONumber=Nov16_HO1-->


