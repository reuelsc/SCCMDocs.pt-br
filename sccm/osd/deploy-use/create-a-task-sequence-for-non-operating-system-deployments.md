---
title: "Criar uma sequência de tarefas para implantações que não são de sistema operacional | Microsoft Docs"
description: "Crie sequências de tarefas que não estão relacionadas à implantação de sistemas operacionais, como distribuição de software, atualização de drivers, edição de estados do usuário, etc."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
caps.latest.revision: 6
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: b4b04907f2cd48d81e864e46ca47c14a0b98a9f7
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017


---
# <a name="create-a-task-sequence-for-non-operating-system-deployments-with-system-center-configuration-manager"></a>Criar uma sequência de tarefas para implantações que não sejam de sistema de operacional com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As sequências de tarefas no System Center Configuration Manager são usadas para automatizar uma variedade de tarefas em seu ambiente. Essas tarefas são principalmente projetadas e testadas para a implantação de sistemas operacionais.  O Configuration Manager traz muitos outros recursos que devem ser a principal tecnologia usada para cenários como [instalação de aplicativos](../../apps/understand/introduction-to-application-management.md), [instalação de atualizações de software](../../sum/understand/software-updates-introduction.md), [definição de configuração](../../compliance/understand/ensure-device-compliance.md) ou automação personalizada. Existem outras tecnologias de automação do Microsoft System Center, como [Orchestrator](https://technet.microsoft.com/library/hh237242.aspx) e [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx) , que também devem ser consideradas.  

O poder das sequências de tarefas está em sua flexibilidade e em como você pode usá-las para definir configurações do cliente, distribuir software, atualizar drivers, editar estados do usuário e executar outras tarefas independentes da implantação de sistema operacional. É possível criar uma sequência de tarefas personalizada para adicionar qualquer quantidade de tarefas. O uso de sequências de tarefas personalizadas para implantação que não do sistema operacional tem suporte no Configuration Manager. No entanto, se uma sequência de tarefa tiver resultados inconsistentes ou indesejados, busque formas de simplificar a operação. Você pode fazer isso usando as etapas mais simples, dividindo as ações em várias sequências de tarefas ou ao usar uma abordagem em fases para criar e testar a sequência de tarefas.

 As seguintes etapas têm suporte para uso em uma sequência de tarefas personalizadas de implantações que não sejam de sistema operacional:  

-   [Verificar Preparação](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

-   [Conectar à Pasta de Rede](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

-   [Baixar o conteúdo do pacote](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

-   [Instalar Aplicativo](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

-   [Instalar Pacote](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

-   [Instalar Atualizações de Software](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

-   [Reiniciar Computador](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer)  

-   [Executar Linha de Comando](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

-   [Executar Script do PowerShell](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

-   [Definir Variáveis Dinâmicas](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

-   [Definir Variável de Sequência de Tarefas](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>Próximas etapas
[Implantar a sequência de tarefas](manage-task-sequences-to-automate-tasks.md#a-namebkmkdeploytsa-deploy-a-task-sequence)

