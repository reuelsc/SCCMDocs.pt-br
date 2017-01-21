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
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: ec146270ef39d48673ae6f3ca405b3f0bd7e8afa


---
# <a name="create-a-task-sequence-for-non-operating-system-deployments-with-system-center-configuration-manager"></a>Criar uma sequência de tarefas para implantações que não sejam de sistema de operacional com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As sequências de tarefas no System Center Configuration Manager são usadas para automatizar uma variedade de tarefas em seu ambiente. Essas tarefas são principalmente projetadas e testadas para a implantação de sistemas operacionais.  O Configuration Manager traz muitos outros recursos que devem ser a principal tecnologia usada para cenários como [instalação de aplicativos](../../apps/understand/introduction-to-application-management.md), [instalação de atualizações de software](../../sum/understand/software-updates-introduction.md), [definição de configuração](../../compliance/understand/ensure-device-compliance.md) ou automação personalizada. Existem outras tecnologias de automação do Microsoft System Center, como [Orchestrator](https://technet.microsoft.com/library/hh237242.aspx) e [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx) , que também devem ser consideradas.  

 O poder das sequências de tarefas está em sua flexibilidade e em como você pode usá-las para definir configurações do cliente, distribuir software, atualizar drivers, editar estados do usuário e executar outras tarefas independentes da implantação de sistema operacional. É possível criar uma sequência de tarefas personalizada para adicionar qualquer quantidade de tarefas. Embora haja suporte para o uso básico das sequências de tarefas personalizadas para implantações que não sejam de sistema operacional, não há uma maneira de testar todas as configurações possíveis, e a possibilidade de ter problemas aumenta, à medida que sequências de tarefas mais complexas são desenvolvidas.  

 As seguintes etapas podem ser usadas em uma sequência de tarefas personalizada de implantações que não sejam de sistema operacional:  

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



<!--HONumber=Dec16_HO3-->


