---
title: Criar uma sequência de tarefas para implantações que não são de sistema operacional
titleSuffix: Configuration Manager
description: Criar sequências de tarefas não destinadas para implantar um SO, mas sim para distribuir softwares ou automatizar tarefas
ms.date: 05/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17ba0f146a80928b1eaae6334e6418a5e08b1114
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65083071"
---
# <a name="create-a-task-sequence-for-non-os-deployments"></a>Criar uma sequência de tarefas para outras implantações que não sejam do sistema operacional

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Sequências de tarefas no Configuration Manager são usadas para automatizar diferentes tipos de tarefas no seu ambiente. Essas tarefas são principalmente projetadas e testadas para a implantação de sistemas operacionais. O Configuration Manager tem muitos outros recursos que devem ser a tecnologia principal usada nos seguintes cenários:

- [Instalação de aplicativos](/sccm/apps/understand/introduction-to-application-management)
- [Instalação de atualizações de software](/sccm/sum/understand/software-updates-introduction)
- [Definição de configuração](/sccm/compliance/understand/ensure-device-compliance)

Considere também outras tecnologias de automação do Microsoft System Center, como o [Orchestrator](https://docs.microsoft.com/system-center/orchestrator/) e o [Service Management Automation](https://docs.microsoft.com/system-center/sma/).  

O poder das sequências de tarefas está em sua flexibilidade e em como você as usa. Elas podem definir configurações de cliente, distribuir softwares, atualizar drivers, editar estados de usuários e realizar outras tarefas independentemente da implementação do SO. É possível criar uma sequência de tarefas personalizada para adicionar qualquer quantidade de tarefas. O Configuration Manager dá suporte ao uso de sequências de tarefas personalizadas para implementações não relacionadas ao SO. No entanto, se uma sequência de tarefas gerar resultados indesejados ou inconsistentes, procure formas de simplificar a operação:

- Use etapas mais simples
- Divida as ações em várias sequências de tarefas
- Faça uma abordagem em fases para criar e testar a sequência de tarefas

As etapas a seguir têm suporte para uso em uma sequência de tarefas personalizada para implementações não relacionadas ao SO:  

- [Verificar Preparação](/sccm/osd/understand/task-sequence-steps#BKMK_CheckReadiness)  

- [Conectar à Pasta de Rede](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder)  

- [Baixar o conteúdo do pacote](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent)  

- [Instalar Aplicativo](/sccm/osd/understand/task-sequence-steps#BKMK_InstallApplication)  

- [Instalar Pacote](/sccm/osd/understand/task-sequence-steps#BKMK_InstallPackage)  

- [Instalar Atualizações de Software](/sccm/osd/understand/task-sequence-steps#BKMK_InstallSoftwareUpdates)  

- [Reiniciar Computador](/sccm/osd/understand/task-sequence-steps#BKMK_RestartComputer)  

- [Executar Linha de Comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)  

- [Executar Script do PowerShell](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript)  

- [Executar Sequência de Tarefas](/sccm/osd/understand/task-sequence-steps#child-task-sequence)  

- [Definir Variáveis Dinâmicas](/sccm/osd/understand/task-sequence-steps#BKMK_SetDynamicVariables)  

- [Definir Variável de Sequência de Tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable)  
