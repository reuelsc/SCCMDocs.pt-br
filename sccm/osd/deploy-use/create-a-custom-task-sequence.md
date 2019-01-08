---
title: Criar uma sequência de tarefas personalizada
titleSuffix: Configuration Manager
description: Edite uma sequência de tarefas personalizada no System Center Configuration Manager para adicionar etapas a ela.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 52a7b81b6ff0d4a0035cf913d925ac5c148b14fc
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417771"
---
# <a name="create-a-custom-task-sequence-with-system-center-configuration-manager"></a>Criar uma sequência de tarefas personalizada com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Quando você cria uma sequência de tarefas personalizada no System Center Configuration Manager, ela não conterá nenhuma etapa de sequência de tarefas. Depois de criar a sequência de tarefas, é preciso editá-la e adicionar as etapas da sequência de tarefas necessárias.  

##  <a name="BKMK_CustomTS"></a> Criar uma sequência de tarefas personalizada  
 Use o procedimento a seguir para criar uma sequência de tarefas personalizada.  

#### <a name="to-create-a-custom-task-sequence"></a>Para criar uma sequência de tarefas personalizada  

1. No console do Configuration Manager, clique em **Biblioteca de Software**.  

2. No workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e clique em **Sequências de Tarefas**.  

3. Na guia **Início** , no grupo **Criar** , clique em **Criar Sequência de Tarefas** para iniciar o Assistente para Criar Sequência de Tarefas.  

4. Na página **Criar uma nova sequência de tarefas** , selecione **Criar uma nova sequência de tarefas personalizada**.  

5. Na página **Informações da Sequência de Tarefas** , especifique o nome e a descrição da sequência de tarefas, uma imagem de inicialização opcional para uso da sequência de tarefas e conclua o assistente.  

   Concluído o Assistente para Criar Sequência de Tarefas, o Configuration Manager adiciona a sequência de tarefas personalizada ao nó **Sequências de Tarefas**. Agora você pode editar essa sequência de tarefas para adicionar etapas da sequência de tarefas a ela.  

   Para obter uma lista das etapas de sequência de tarefas disponíveis, consulte [Etapas da sequência de tarefas](../understand/task-sequence-steps.md).  

   Para obter mais informações sobre como editar uma sequência de tarefas, consulte [Editar uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

   Geralmente, você usará as sequências de tarefas para automatizar tarefas para implantação de sistema operacional, mas é possível criar uma sequência de tarefas personalizada para automatizar uma variedade de tarefas. Para mais informações, consulte [Criar uma sequência de tarefas para implantações que não são de sistema operacional](create-a-task-sequence-for-non-operating-system-deployments.md).  

   ## <a name="next-steps"></a>Próximas etapas
   [Implantar a sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
