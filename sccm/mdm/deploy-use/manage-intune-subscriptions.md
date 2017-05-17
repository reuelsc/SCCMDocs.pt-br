---
title: Gerenciar uma assinatura do Intune associado ao System Center Configuration Manager | Microsoft Docs
description: Gerencie uma assinatura do Intune associado ao System Center Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b494767-68c1-47b1-9a86-591bff0ad491
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 2e0b3cd1070d0f8adb1219acd33c3126d2758a49
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017

---
# <a name="manage-an-intune-subscription-associated-with-system-center-configuration-manager"></a>Gerenciar uma assinatura do Intune associado ao System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Se você adicionar uma assinatura do Microsoft Intune (uma assinatura de avaliação ou uma assinatura paga) ao Configuration Manager e precisar mudar para uma assinatura diferente do Intune, será preciso excluir tanto a **Assinatura do Microsoft Intune** quanto o **Ponto de conexão de serviço** do console do Configuration Manager para poder adicionar uma nova assinatura.

> [!NOTE]
> Configure apenas uma assinatura do Intune por vez no gerenciamento de dispositivos móveis híbrido.

## <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>Como excluir uma assinatura Intune do Configuration Manager

> [!IMPORTANT]
>  Todo o conteúdo, incluindo registros do usuário, políticas e implantações de aplicativo configuradas para dispositivos gerenciados pela assinatura do Intune, serão removidos quando você excluir a assinatura.

1.  No console do Configuration Manager, clique em **Administração** > **Visão Geral** > **Serviços em Nuvem** > **Assinaturas do Microsoft Intune**.

2.  Clique com o botão direito do mouse na opção **Assinatura do Microsoft Intune** listada e clique em **Excluir**.

3.   No assistente, clique em **Remover Assinatura do Microsoft Intune do Configuration Manager**, clique em **Avançar** e, em seguida, clique em **Avançar** novamente para remover a assinatura.


## <a name="how-to-remove-the-service-connection-point-role"></a>Para remover a função do ponto de conexão de serviço

1.  Acesse **Administração** > **Visão Geral** > **Configuração do Site** > **Funções de Servidores e Sistema de Site**.

2.  Escolha o servidor que hospeda a função **Ponto de conexão de serviço**.

3.  Na lista **Funções do Sistema de Sites**, escolha **Ponto de conexão de serviço** e clique em **Remover Função** na faixa de opções. Confirme que deseja remover a função. O ponto de conexão de serviço é excluído.

Agora você pode criar um novo ponto de conexão de serviço, adicionar uma nova assinatura do Intune ao Configuration Manager e definir o Configuration Manager como a Autoridade MDM.

## <a name="how-to-change-mdm-authority-to-intune"></a>Como alterar a autoridade do MDM para o Intune

Começando na versão 1610, é possível mudar a autoridade MDM do Configuration Manager para o Intune. Informações sobre esse recurso estarão disponíveis em breve.

