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
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754578"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>Como mudar as cargas de trabalho do Configuration Manager para o Intune

Um dos benefícios de cogerenciamento é mudar as cargas de trabalho do Configuration Manager para o Microsoft Intune. Quando um dispositivo com Windows 10 tem o cliente do Configuration Manager e está registrado no Intune, você obtém os benefícios de ambos os serviços. Controle de quais cargas de trabalho, se houver, você pode mudar a autoridade do Configuration Manager para o Intune. O Configuration Manager continua gerenciando todas as outras cargas de trabalho, incluindo as que você não mudar para o Intune e todos os outros recursos do Configuration Manager não compatíveis com cogerenciamento.

Para saber mais sobre as cargas de trabalho compatíveis, confira [Cargas de trabalho](/sccm/comanage/workloads).

Você pode mudar as cargas de trabalho ao habilitar o cogerenciamento ou posteriormente, quando estiver pronto. Se você ainda não habilitou o cogerenciamento, faça isso primeiro. Para saber mais, confira [Como habilitar o cogerenciamento](/sccm/comanage/how-to-enable).


Depois de habilitar o cogerenciamento, modifique as configurações nas propriedades de cogerenciamento. 

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e escolha o nó **Cogerenciamento**.  

2. Selecione o objeto de cogerenciamento e, em seguida, escolha **Propriedades** na faixa de opções.  

3. Mude para a guia **Cargas de trabalho**. Por padrão, todas as cargas de trabalho são definidas para a configuração do **Configuration Manager**. Para mudar uma carga de trabalho, mova o controle deslizante dessa carga de trabalho para a configuração desejada.  

    ![Captura de tela da guia Cargas de trabalho na página de propriedades de cogerenciamento](media/properties-workloads.png)

    - **Configuration Manager**: O Configuration Manager continua a gerenciar essa carga de trabalho.  

    - **Intune piloto**: mude essa carga de trabalho apenas para os dispositivos da coleção Piloto. Você pode alterar a **coleção Piloto** na guia **Preparo** da página de propriedades de cogerenciamento.  

    - **Intune**: mude essa carga de trabalho em todos os dispositivos Windows 10 registrados no cogerenciamento.  


> [!Important]  
> Antes de mudar cargas de trabalho, não se esqueça de configurar e implantar corretamente a carga de trabalho correspondente no Intune. As cargas de trabalho sempre devem ser gerenciadas por uma das ferramentas de gerenciamento dos dispositivos.  

<!--1357377-->
A partir do Configuration Manager versão 1806, quando você muda uma carga de trabalho de cogerenciamento, os dispositivos cogerenciados sincronizam automaticamente a política de MDM do Microsoft Intune. Essa sincronização também acontece quando você inicia a ação **Baixar Política do Computador** nas notificações do cliente no console do Configuration Manager. Para obter mais informações, confira [Iniciar recuperação de política do cliente usando a notificação do cliente](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).


