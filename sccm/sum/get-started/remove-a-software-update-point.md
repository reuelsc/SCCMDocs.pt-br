---

title: "Remover um ponto de atualização de software | Configuration Manager"
description: "Siga esse procedimento para remover a função do sistema de sites do ponto de atualização de software em um site no console do Configuration Manager."
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
ms.assetid: 2486375c-d4a2-4cf2-9124-9bee02bbf173
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e95e3fc2aafde2d947f08d32e2b2130a313e7328


---
#  <a name="a-namebkmkremovesupa-remove-the-software-update-point-site-system-role"></a><a name="BKMK_RemoveSUP"></a> Remover a função do sistema de sites do ponto de atualização de software  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode remover a função do sistema de sites do ponto de atualização de software em um site no console do Configuration Manager. A política do cliente é atualizada para remover o ponto de atualização de software da lista. Ao remover o último ponto de atualização de software no site, a lista de pontos de atualização de software não terá pontos de atualização de software e as atualizações de software serão basicamente desabilitadas no site. Quando há mais de um ponto de atualização de software em um site primário e o ponto de atualização de software configurado como a origem de sincronização é removido, é necessário escolher outro ponto de atualização de software no site para ser a nova origem de sincronização.  

> [!NOTE]  
>  Ao remover a função do site do ponto de atualização de software a partir do sistema de site, aguarde pelo menos 15 minutos para poder reinstalar a função do site do ponto de atualização.  

 Use o procedimento a seguir para remover um ponto de atualização de software.  

#### <a name="to-remove-the-software-update-point"></a>Para remover o ponto de atualização de software  

1.  No console do **Configuration Manager** , clique em **Administração**.  

2.  No espaço de trabalho Administração, expanda **Configuração do Site**e clique em **Funções de Servidores e Sistema de Site**.  

3.  Selecione o servidor do sistema de site com o ponto de atualização de software a remover e em **Funções do Sistema de Site**, selecione **Ponto de atualização de software**.  

4.  Na guia **Função de Site** , no grupo **Função de Site** , clique em **Remover Função**. Confirme se deseja remover o ponto de atualização de software ou selecione uma nova origem de sincronização para os outros pontos de atualização de software no site.  



<!--HONumber=Nov16_HO1-->


