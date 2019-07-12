---
title: Capturar e restaurar o estado do usuário
titleSuffix: Configuration Manager
description: Use as sequências de tarefas do Gerenciador de Configurações para capturar e restaurar os dados de estado do usuário em cenários de implantação do sistema operacional.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c82de88250a7faa44747fc897fcfee09bed45823
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678801"
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-configuration-manager"></a>Criar uma sequência de tarefas para capturar e restaurar o estado do usuário no Gerenciador de Configurações

 *Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Use as sequências de tarefas do Gerenciador de Configurações para capturar e restaurar os dados de estado do usuário em cenários de implantação do sistema operacional. Nesses cenários, convém manter o estado do usuário do sistema operacional atual. Dependendo do tipo de sequência de tarefas criado, as etapas de captura e restauração podem ser adicionadas automaticamente como parte da sequência de tarefas. Em outros cenários, talvez seja necessário adicionar manualmente as etapas de captura e restauração à sequência de tarefas. Este artigo fornece as etapas que devem ser adicionadas a uma sequência de tarefas existente para capturar e restaurar dados de estado do usuário.  



## <a name="task-sequence-steps"></a>Etapas da sequência de tarefas  

Para capturar e restaurar o estado do usuário, adicione as seguintes etapas à sequência de tarefas:  

- [Solicitar Armazenamento de Estado](/sccm/osd/understand/task-sequence-steps#BKMK_RequestStateStore): essa etapa é necessária se você armazenar o estado do usuário no ponto de migração de estado.  

- [Capturar Estado do Usuário](/sccm/osd/understand/task-sequence-steps#BKMK_CaptureUserState): essa etapa captura os dados de estado do usuário. Em seguida, os armazena no ponto de migração de estado ou no disco local usando links físicos.  

- [Restaurar Estado do Usuário](/sccm/osd/understand/task-sequence-steps#BKMK_RestoreUserState): essa etapa restaura os dados de estado do usuário no computador de destino. Ela pode recuperar os dados de um ponto de migração de estado ou se houver um link físico no disco local.  

- [Liberar Armazenamento de Estado](/sccm/osd/understand/task-sequence-steps#BKMK_ReleaseStateStore): essa etapa é necessária se você armazenar o estado do usuário no ponto de migração de estado. Ela remove os dados do ponto de migração de estado.  


 Use os procedimentos a seguir para adicionar as etapas de sequência de tarefas necessárias para capturar e restaurar o estado do usuário. Para saber mais sobre a criação de sequências de tarefas em [Gerenciar sequências de tarefas para automatizar tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks).  



## <a name="capture-the-user-state"></a>Capturar o estado do usuário  

 Use os seguintes passos para adicionar etapas de sequência de tarefas para capturar o estado do usuário:

1.  Na lista **Sequência de Tarefa** , selecione uma sequência de tarefas e clique em **Editar**.  

2.  Se estiver usando um ponto de migração de estado para armazenar o estado do usuário, adicione a etapa **Solicitar Armazenamento de Estado** à sequência de tarefas. No **Editor de Sequência de Tarefas**, clique em **Adicionar**. Aponte para **Estado do Usuário**e clique em **Solicitar Armazenamento de Estado**. Configure as propriedades e opções para esta etapa e clique em **Aplicar**. Para saber mais sobre as configurações disponíveis em [Solicitar Armazenamento de Estado](/sccm/osd/understand/task-sequence-steps#BKMK_RequestStateStore).  

3.  Adicione a etapa **Captura Estado do Usuário** à sequência de tarefas. No **Editor de Sequência de Tarefas**, clique em **Adicionar**. Aponte para **Estado do Usuário**e clique em **Capturar Estado do Usuário**. Configure as propriedades e opções para esta etapa e clique em **Aplicar**. Para saber mais sobre as configurações disponíveis em [Capturar Estado do Usuário](/sccm/osd/understand/task-sequence-steps#BKMK_CaptureUserState).  

    > [!IMPORTANT]  
    >  Ao adicionar essa etapa à sequência de tarefas, configure também a variável de sequência de tarefas **OSDStateStorePath** para especificar onde armazenar os dados de estado do usuário. Se você armazenar o estado do usuário localmente, não especifique uma pasta raiz, pois isso pode causar falha da sequência de tarefas. Quando você armazenar os dados do usuário localmente, use sempre uma pasta ou subpasta. Para saber mais sobre esta variável em [Variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath).  

4.  Se estiver usando um ponto de migração de estado, adicione à sequência de tarefas a etapa **Liberar Armazenamento de Estado**. No **Editor de Sequência de Tarefas**, clique em **Adicionar**. Aponte para **Estado do Usuário** e clique em **Liberar Armazenamento de Estado**. Configure as propriedades e opções para esta etapa e clique em **Aplicar**. Para saber mais sobre as configurações disponíveis em [Liberar Armazenamento de Estado](/sccm/osd/understand/task-sequence-steps#BKMK_ReleaseStateStore).  

    > [!IMPORTANT]  
    >  A ação de sequência de tarefas executada antes da etapa **Liberar Armazenamento de Estado** deve ser bem-sucedida para que a etapa **Liberar Armazenamento de Estado** seja iniciada.  


 Implante essa sequência de tarefas para capturar o estado do usuário em um computador de destino. Para obter informações sobre como implantar sequências de tarefas, consulte [Implantar uma sequência de tarefas](/sccm/osd/deploy-use/deploy-a-task-sequence).  



## <a name="restore-the-user-state"></a>Restaurar o estado do usuário  

 Use os passos seguintes para adicionar etapas de sequência de tarefas para restaurar o estado do usuário:

1. Na lista **Sequência de Tarefa** , selecione uma sequência de tarefas e clique em **Editar**.  

2. Adicionar a etapa **Restaurar Estado do Usuário** à sequência de tarefas. No **Editor de Sequência de Tarefas**, clique em **Adicionar**. Aponte para **Estado do Usuário**e clique em **Restaurar Estado do Usuário**. Essa etapa estabelece uma conexão com o ponto de migração de estado, se necessário. Configure as propriedades e opções para esta etapa e clique em **Aplicar**. Para saber mais sobre as configurações disponíveis em [Restaurar Estado do Usuário](/sccm/osd/understand/task-sequence-steps#BKMK_RestoreUserState).  

   > [!Important]  
   >  Quando você usa a etapa [Capturar Estado do Usuário](/sccm/osd/understand/task-sequence-steps#BKMK_CaptureUserState) com a opção de **Capturar todos os perfis de usuário com opções padrão**, você deve selecionar a configuração **Restaurar perfis de usuário do computador local** na etapa **Restaurar Estado do Usuário**. Caso contrário, a sequência de tarefas não funcionará.  

   > [!Note]  
   > Se você armazenar o estado do usuário usando links físicos locais e a restauração não for bem-sucedida, você poderá excluir manualmente os links físicos que foram criados para armazenar os dados. A sequência de tarefas pode executar a ferramenta USMTUtils para automatizar esta ação com uma etapa [Executar linha de comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine). Se você usar o USMTUtils para excluir links físicos, adicione uma etapa [Reiniciar Computador](/sccm/osd/understand/task-sequence-steps#BKMK_RestartComputer) depois de executar o USMTUtils.  

3. Se estiver usando um ponto de migração de estado para armazenar o estado do usuário, adicione à sequência de tarefas a etapa **Liberar Armazenamento de Estado**. No **Editor de Sequência de Tarefas**, clique em **Adicionar**. Aponte para **Estado do Usuário** e clique em **Liberar Armazenamento de Estado**. Configure as propriedades e opções para esta etapa e clique em **Aplicar**. Para saber mais sobre as configurações disponíveis em [Liberar Armazenamento de Estado](/sccm/osd/understand/task-sequence-steps#BKMK_ReleaseStateStore).  

   > [!IMPORTANT]  
   >  A ação de sequência de tarefas executada antes da etapa **Liberar Armazenamento de Estado** deve ser bem-sucedida para que a etapa **Liberar Armazenamento de Estado** seja iniciada.  


 Implante essa sequência de tarefas para restaurar o estado do usuário em um computador de destino. Para obter mais informações sobre como implantar sequências de tarefas, consulte [Implantar uma sequência de tarefas](/sccm/osd/deploy-use/deploy-a-task-sequence).  



## <a name="next-steps"></a>Próximas etapas

[Monitorar a implantação da sequência de tarefas](/sccm/osd/deploy-use/monitor-operating-system-deployments#BKMK_TSDeployStatus)
