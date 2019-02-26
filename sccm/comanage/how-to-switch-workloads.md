---
title: Mudar as cargas de trabalho de cogerenciamento
titleSuffix: Configuration Manager
description: Saiba como mudar as cargas de trabalho que no momento são gerenciadas pelo Configuration Manager para serem gerenciadas pelo Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.collection: M365-identity-device-management
ms.openlocfilehash: a4b50d0491644e6be0967c1adcf2db641c1bb1cd
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754578"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>Como mudar cargas de trabalho do Configuration Manager para o Intune

Um dos benefícios de cogerenciamento está alternando as cargas de trabalho do Configuration Manager para o Microsoft Intune. Quando um dispositivo Windows 10 tem o cliente do Configuration Manager e está registrado no Intune, você obtém os benefícios de ambos os serviços. Você controlar quais cargas de trabalho, se houver, que você mudar a autoridade do Configuration Manager para o Intune. Configuration Manager continua a gerenciar todas as outras cargas de trabalho, incluindo cargas de trabalho que você não mudar para o Intune e não dá suporte a todos os outros recursos do Configuration Manager que cogerenciamento.

Para obter mais informações sobre as cargas de trabalho com suporte, consulte [cargas de trabalho](/sccm/comanage/workloads).

Você pode alternar as cargas de trabalho quando você habilitar o cogerenciamento, ou posteriormente, quando você está pronto. Se você ainda não tiver habilitado o cogerenciamento, faça isso primeiro. Para obter mais informações, consulte [como habilitar o cogerenciamento](/sccm/comanage/how-to-enable).


Depois de habilitar o cogerenciamento, modifique as configurações nas propriedades de cogerenciamento. 

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e escolha o nó **Cogerenciamento**.  

2. Selecione o objeto de cogerenciamento e, em seguida, escolha **propriedades** na faixa de opções.  

3. Alterne para o **cargas de trabalho** guia. Por padrão, todas as cargas de trabalho são definidas o **Configuration Manager** configuração. Para alternar uma carga de trabalho, mova o controle deslizante para essa carga de trabalho para a configuração desejada.  

    ![Guia de captura de tela de cargas de trabalho na página de propriedades de cogerenciamento](media/properties-workloads.png)

    - **Configuration Manager**: Configuration Manager continua a gerenciar essa carga de trabalho.  

    - **Criar um piloto do Intune**: Alterne essa carga de trabalho apenas para os dispositivos na coleção piloto. Você pode alterar o **coleção piloto** sobre o **preparo** guia da página de propriedades de cogerenciamento.  

    - **Intune**: Alterne essa carga de trabalho para todos os dispositivos Windows 10 registrados no cogerenciamento.  


> [!Important]  
> Antes de mudar as cargas de trabalho, certifique-se de configurar corretamente e implantar a carga de trabalho correspondente no Intune. As cargas de trabalho sempre devem ser gerenciadas por uma das ferramentas de gerenciamento dos dispositivos.  

<!--1357377--> Começando no Configuration Manager versão 1806, quando você muda uma carga de trabalho de cogerenciamento, os dispositivos cogerenciados sincronizam automaticamente a política de MDM do Microsoft Intune. Essa sincronização também acontece quando você inicia a ação **Baixar Política do Computador** nas notificações do cliente no console do Configuration Manager. Para obter mais informações, confira [Iniciar recuperação de política do cliente usando a notificação do cliente](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).


