---
title: Ferramenta de Resumo do Medidor de Execução
titleSuffix: Configuration Manager
description: Use a ferramenta Resumo do Medidor de Execução para disparar tarefas de resumo de medição de software no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d27f88fe-817f-4af4-b290-c16f2e46cf31
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7bfb6758d62fb76650e019d00eef1ac2b2803d4b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126956"
---
# <a name="run-meter-summarization-tool"></a>Ferramenta de Resumo do Medidor de Execução

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A Ferramenta Resumo do Medidor de Execução é uma das [ferramentas do Configuration Manager](/sccm/core/support/tools). Use-a para disparar imediatamente as tarefas de manutenção para resumo de medição de software em sites primários. Por padrão, essas tarefas são executadas como agendadas em tarefas de **Manutenção do Site**, que iniciam após a meia-noite todos os dias. 

Essas tarefas resumem os dados na tabela SQL do **MeterData** e gravam os resultados do resumo nas tabelas **FileUsageSummary** e **MonthlyUsageSummary**. Então você verá o resultado resumido em relatórios de medição de software. Qualquer usuário administrativo do Configuration Manager que pode se conectar ao banco de dados do site primário pode usar essa ferramenta para executar o resumo. 

Essa ferramenta executa as tarefas de resumo de dados de medição de software **Resumo de Uso do Arquivo** e **Resumo de Uso Mensal**. Ela resume todos os dados de medidor existentes sem o período de espera usual de 12 horas. Execute-a no SQL Server que hospeda o banco de dados do site. Se o resumo for bem-sucedido, o código de saída será definido como `0`. Se houver um erro, o código de saída será `1`.



## <a name="usage"></a>Uso

### <a name="command-line"></a>Linha de comando

`runmetersumm  [sms database name]  <delay in hours for summarization <default=0>>`


### <a name="options"></a>Opções

#### <a name="database-name"></a>Nome do banco de dados
O nome do banco de dados do site no SQL Server.

#### <a name="delay-in-hours-for-summarization"></a>Atraso em horas para resumo
A ferramenta resume o uso de medição de software gerado antes do atraso. Por padrão, esse atraso é zero.


### <a name="example"></a>Exemplo

#### <a name="summarize-the-software-metering-usage-generated-12-hours-ago"></a>Resumir o uso de medição de software gerado 12 horas atrás

`runmetersumm CCM_ABC <12>`



## <a name="see-also"></a>Consulte também

- [Tarefas de manutenção](/sccm/core/servers/manage/maintenance-tasks)
- [Monitorar o uso de aplicativos com a medição de software](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering)
