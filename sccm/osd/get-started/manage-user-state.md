---
title: 'Gerenciar o estado do usuário '
titleSuffix: Configuration Manager
description: O System Center Configuration Manager usa a Ferramenta de Migração do Usuário para capturar e restaurar os dados de estado do usuário em cenários de implantação de sistema operacional.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d8d5c345-1e91-410b-b8a9-0170dcfa846e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 676131965165acda9633e7fbceaee7f25d823efe
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53420372"
---
# <a name="manage-user-state-in-system-center-configuration-manager"></a>Gerenciar estado do usuário no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode usar as sequências da tarefas do System Center Configuration Manager para capturar e restaurar dados de estado do usuário em cenários de implantação do sistema operacional no qual você deseja manter o estado do usuário do sistema operacional atual. Por exemplo:  

- Implantações em que você deseja capturar o estado do usuário de um computador para restaurá-lo em outro computador.  

- Atualização de implantações em que você deseja capturar e restaurar o estado do usuário no mesmo computador.  

  O Configuration Manager usa a USMT (Ferramenta de Migração do Usuário) 10.0 para gerenciar a migração dos dados de estado do usuário de um computador de origem para um computador de destino após a conclusão da instalação do sistema operacional. Para obter mais informações sobre cenários comuns de migração para a USMT 10.0, veja  [Cenários comuns de migração](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx).  

  Use as seções a seguir para ajudar a capturar e restaurar os dados do usuário.


##  <a name="BKMK_StoringUserData"></a> Armazenar dados de estado do usuário  
 Ao capturar o estado do usuário, é possível armazenar os dados de estado do usuário no computador de destino ou em um ponto de migração de estado. Para armazenar o estado do usuário em um ponto de migração de estado do usuário, você deve usar um servidor do sistema de sites do Configuration Manager que hospeda a função do sistema de sites do ponto de migração de estado. Para armazenar o estado de usuário no computador de destino, você deve configurar sua sequência de tarefas para armazenar os dados localmente usando links.  

> [!NOTE]  
>  Os links que são usados para armazenar o estado do usuário localmente são chamados de links físicos. Links físicos são um recurso da USMT 10.0 que verifica os arquivos e as configurações de usuário no computador e cria um diretório de links físicos para esses arquivos. Em seguida, os links físicos são usados para restaurar os dados do usuário após a implantação de um novo sistema operacional.  

> [!IMPORTANT]  
>  Não é possível usar um ponto de migração de estado e usar links físicos para armazenar os dados de estado do usuário ao mesmo tempo.  

 Quando as informações de estado do usuário são capturadas, elas podem ser armazenadas de uma das seguintes maneiras:  

-   Você pode armazenar os dados de estado do usuário remotamente, configurando um ponto de migração de estado. A sequência de tarefas **Capturar** envia os dados para o ponto de migração de estado. Em seguida, após a implantação do sistema operacional, a sequência de tarefas **Restaurar** recupera os dados e restaura o estado do usuário no computador de destino.  

-   Você pode armazenar os dados de estado do usuário localmente em um local específico. Nesse cenário, a sequência de tarefas **Capturar** copia os dados do usuário para um local específico no computador de destino. Em seguida, após a implantação do sistema operacional, a sequência de tarefas **Restaurar** recupera os dados do usuário desse local.  

-   Você pode especificar links físicos que podem ser usados para restaurar os dados do usuário para o local original. Nesse cenário, os dados de estado do usuário permanecem na unidade quando o sistema operacional antigo é removido. Em seguida, após a implantação do novo sistema operacional, a sequência de tarefas **Restaurar** usa os links físicos para restaurar os dados de estado do usuário para o local original.  

###  <a name="BKMK_UserDataSMP"></a> Armazenar dados do usuário em um ponto de migração de estado  
 Para armazenar os dados de estado do usuário em um ponto de migração de estado, é preciso fazer o seguinte:  

1.  [Configure a state migration point](#BKMK_StateMigrationPoint) para armazenar os dados de estado do usuário.  

2.  [Create a computer association](#BKMK_ComputerAssociation) entre o computador de origem e o computador de destino. Você deve criar essa associação antes de capturar o estado do usuário no computador de origem.  

3.  [Criar uma sequência de tarefas para capturar e restaurar o estado de usuário no System Center Configuration Manager](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). Especificamente, é necessário adicionar as seguintes etapas da sequência de tarefas para capturar dados do usuário de um computador, armazená-los em um ponto de migração de estado e restaurá-los em um computador:  

    -   [Solicitar Repositório de Estado](../understand/task-sequence-steps.md#BKMK_RequestStateStore) para solicitar acesso a um ponto de migração de estado durante a captura de estado ou a restauração de estado em um computador.  

    -   [Capturar Estado do Usuário](../understand/task-sequence-steps.md#BKMK_CaptureUserState) para capturar e armazenar os dados de estado do usuário no ponto de migração de estado.  

    -   [Restaurar Estado do Usuário](../understand/task-sequence-steps.md#BKMK_RestoreUserState) para restaurar o estado do usuário no computador de destino recuperando os dados de um ponto de migração de estado do usuário.  

    -   [Liberar Repositório de Estado](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) para notificar o ponto de migração de estado de que a ação de captura ou restauração foi concluída.  

###  <a name="BKMK_UserDataDestination"></a> Armazenar dados do usuário localmente  
 Para armazenar os dados de estado do usuário localmente, é preciso fazer o seguinte:  

-   [Crie uma sequência de tarefas para capturar e restaurar o estado do usuário](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). Especificamente, é necessário adicionar as seguintes etapas da sequência de tarefas para capturar dados do usuário de um computador e restaurá-los em um computador usando links físicos:  

    -   [Capturar Estado de Usuário](../understand/task-sequence-steps.md#BKMK_CaptureUserState) para capturar e armazenar os dados de estado do usuário em uma pasta local usando links físicos.  

    -   [Restaurar Estado de Usuário](../understand/task-sequence-steps.md#BKMK_RestoreUserState) para recuperar o estado do usuário no computador de destino recuperando os dados com links físicos.  

        > [!NOTE]  
        >  Os dados de estado do usuário aos quais os links físicos se referem permanecem no computador depois que a sequência de tarefas remove o sistema operacional antigo. Esses são os dados usados para restaurar o estado do usuário quando o novo sistema operacional é implantado.  

##  <a name="BKMK_StateMigrationPoint"></a> Configure a state migration point  
 O ponto de migração de estado armazena dados de estado do usuário, que são capturados em um computador e restaurados em outro. No entanto, ao capturar as configurações de usuário para uma implantação de sistema operacional no mesmo computador, como em uma implantação em que você atualiza o sistema operacional no computador de destino, é possível armazenar os dados no mesmo computador usando links físicos ou em um ponto de migração de estado. Em certas implantações de computador, quando você cria o armazenamento de estado, o Configuration Manager automaticamente cria uma associação entre o armazenamento de estado e o computador de destino. É possível usar os seguintes métodos para configurar um ponto de migração de estado para armazenar os dados de estado do usuário:  

- Use o **Assistente para Criar Servidor do Sistema de Site** para criar um novo servidor do sistema de site para o ponto de migração de estado.  

- Use o **Assistente para Adicionar Funções do Sistema de Site** para adicionar um ponto de migração de estado a um servidor existente.  

  Ao usar esses assistentes, você é solicitado a fornecer as seguintes informações do ponto de migração de estado:  

- As pastas para armazenar os dados de estado do usuário.  

- O número máximo de clientes que podem armazenar dados no ponto de migração de estado.  

- O espaço livre mínimo para o ponto de migração de estado armazenar dados de estado do usuário.  

- A política de exclusão para a função. Você pode especificar se os dados de estado do usuário serão excluídos imediatamente depois de serem restaurados em um computador ou após um número específico de dias depois que os dados do usuário são restaurados em um computador.  

- Se você deseja que o ponto de migração de estado responda apenas às solicitações para restaurar dados de estado do usuário. Ao habilitar essa opção, você não pode usar o ponto de migração de estado para armazenar dados de estado do usuário.  

  Para obter mais informações sobre o ponto de migração de estado e as etapas para configurá-lo, consulte [Ponto de migração de estado](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

##  <a name="BKMK_ComputerAssociation"></a> Create a computer association  
 Crie uma associação de computador para definir uma relação entre um computador de origem e um computador de destino ao instalar um sistema operacional em um novo hardware e desejar capturar e restaurar as configurações de dados do usuário. O computador de origem é um computador existente que o Configuration Manager gerencia. Quando você implanta o novo sistema operacional no computador de destino, o computador de origem contém o estado do usuário que é migrado para o computador de destino.  

> [!NOTE]  
>  Não há suporte para criar uma associação entre computadores localizados em um site pai do Configuration Manager com computadores localizados em um site filho. As associações de computador são específicas do site e não são replicadas.  

#### <a name="to-create-a-computer-association"></a>Para criar uma associação de computador  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No workspace **Ativos e Conformidade**, clique em **Migração de Estado de Usuário**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Associação de Computador**.  

4.  Na guia **Associação de Computador** da caixa de diálogo **Propriedades da Associação de Computador** , especifique o computador de origem que tem o estado do usuário a ser capturado e o computador de destino no qual restaurar os dados de estado do usuário.  

5.  Na guia **Contas de Usuário** , especifique as contas de usuário a serem migradas para o computador de destino. Especifique uma das seguintes configurações:  

    -   **Capturar e restaurar todas as contas de usuário**: essa configuração captura e restaura todas as contas de usuário. Use essa configuração para criar várias associações ao mesmo computador de origem.  

    -   **Capturar todas as contas de usuário e restaurar contas especificadas**: essa configuração captura todas as contas de usuário no computador de origem e restaura somente as contas que você especificar no computador de destino. Além disso, você pode usar essa configuração para criar várias associações ao mesmo computador de origem.  

    -   **Capturar e restaurar contas de usuário especificadas**: essa configuração captura e restaura apenas as contas que você especificar. Você não pode criar várias associações ao mesmo computador de origem quando seleciona essa configuração.  

##  <a name="BKMK_MigrationFails"></a> Restaurar os dados de estado do usuário quando uma implantação de sistema operacional falhar  
 Se a implantação de sistema operacional falhar, use o recurso LoadState da USMT 10.0 para recuperar os dados de estado do usuário capturados durante o processo de implantação. Isso inclui dados armazenados em um ponto de migração de estado ou dados salvos localmente no computador de destino. Para mais informações sobre esse recurso USMT, consulte [LoadState Syntax (Sintaxe LoadState)](https://technet.microsoft.com/library/mt299188\(v=vs.85\).aspx).  
