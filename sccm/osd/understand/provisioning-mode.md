---
title: Modo de provisionamento
titleSuffix: Configuration Manager
description: Saiba mais sobre o modo de provisionamento de cliente durante a sequência de tarefas do Configuration Manager.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 3e3ff3a4-7a75-41bb-bdf9-33ede9c0e3a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 970b1fea320d8fe039062cf81789d14398930be5
ms.sourcegitcommit: 3f43fa8462bf39b2c18b90a11a384d199c2822d8
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66403427"
---
# <a name="provisioning-mode"></a>Modo de provisionamento

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Durante uma sequência de tarefas de implantação do sistema operacional, o Configuration Manager coloca o cliente no modo de provisionamento. (Uma sequência de tarefas de implantação do sistema operacional inclui a atualização in-loco para o Windows 10.) Nesse estado, o cliente não processa a política do site. Esse comportamento permite que a sequência de tarefas seja executada sem o risco de haver implantações adicionais em execução no cliente. Quando a sequência de tarefas é concluída, com sucesso ou falha tratada, ele sai do modo de provisionamento de cliente.

Se a sequência de tarefas falhar inesperadamente, o cliente poderá ser deixado no modo de provisionamento. Por exemplo, se o dispositivo for reiniciado no meio do processamento da sequência de tarefas e não puder se recuperar. Um administrador precisará identificar e corrigir os clientes manualmente nesse estado.


## <a name="manually-remove-provisioning-mode"></a>Remover manualmente o modo de provisionamento

Se um cliente for deixado no modo de provisionamento, use esse processo manual para retornar o cliente à operação normal.

```PowerShell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $false
```

> [!Important]  
> Uma das alterações feitas por esse método WMI é definir um valor de Registro, mas faz outras alterações também. Apenas alterar o valor de Registro não tira totalmente o cliente do modo de provisionamento. Se você editar manualmente o Registro, o cliente poderá apresentar comportamentos inesperados.  


## <a name="client-provisioning-mode-timeout"></a>Tempo limite do modo de provisionamento do cliente

Começando na versão 1902, a sequência de tarefas define um carimbo de data/hora quando coloca o cliente no modo de provisionamento. A cada 60 minutos, um cliente no modo de provisionamento verifica a duração de tempo desde o carimbo de data/hora. Se o cliente estiver no modo de provisionamento a mais de 48 horas, ele sairá automaticamente do modo de provisionamento e reiniciará seu processo.

48 horas é o valor de tempo limite padrão do modo de provisionamento. Você pode ajustar esse temporizador em um dispositivo definindo o valor de **ProvisioningMaxMinutes** na seguinte chave do Registro: `HKLM\Software\Microsoft\CCM\CcmExec`. Se esse valor não existir ou estiver `0`, o cliente usará o padrão de 48 horas.


## <a name="process-flow-diagrams"></a>Diagramas de fluxo de processo

Esses diagramas mostram o fluxo do processo para a sequência de tarefas e o cliente.

### <a name="task-sequence"></a>Sequência de tarefas

O diagrama a seguir mostra como a sequência de tarefas define o modo de provisionamento:

![Diagrama de fluxo do modo de provisionamento de configuração de sequência de tarefas](media/3197824-ts-flow.png)

### <a name="client-remediation"></a>Correção do cliente

O diagrama a seguir mostra como o cliente sai do modo de provisionamento:

![Diagrama de fluxo do cliente saindo do modo de provisionamento](media/3197824-client-flow.png)


## <a name="see-also"></a>Consulte também

[Instalar Windows e ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr)

[Atualizar o sistema operacional](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS)
