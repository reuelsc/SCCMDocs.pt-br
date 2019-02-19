---
title: Send Schedule Tool
titleSuffix: Configuration Manager
description: Use a Ferramenta de Agendamento de Envio para disparar um agendamento em um cliente do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d5ce547d-3b3b-47d3-bcd7-6ff94692c046
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 38829a249ca87ca87f9c5005ed7ae73e1500e2ab
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131193"
---
# <a name="send-schedule-tool"></a>Send Schedule Tool

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A ferramenta de agendamento de envio é uma das [ferramentas do Configuration Manager](/sccm/core/support/tools). Use-a para disparar um agendamento em um cliente ou disparar a avaliação de uma linha de base de configuração especificada. Ela funciona para o computador local ou tendo um cliente remoto como destino.  

Por exemplo, use a ferramenta para disparar uma avaliação de conformidade ou um agendamento de inventário. Se vários clientes do Configuration Manager recentemente não tiverem relatado o status de conformidade ou inventário, execute a ferramenta para iniciar o agendamento necessário em cada cliente.



## <a name="usage"></a>Uso

Execute **SendSchedule.exe** como administrador. 

`SendSchedule /L [Computer Name]`
`SendSchedule "<Message GUID | DCM UID>" [Computer Name]` 

Depois de disparar uma mensagem (GUID), veja **SMSClientMethodProvider.log**. Para obter mais informações sobre GUIDs de mensagens disponíveis, veja [IDs de mensagem](#bkmk_sendschedule-guids).

Depois de disparar a avaliação de uma linha de base de configuração ( UID do DCM), veja **DCMAgent.log**.



## <a name="command-line-options"></a>Opções de linha de comando


### <a name="option-l"></a>Opção: `/L` 
Liste todas as Mensagens GUID ou UID de DCM disponíveis para envio. Exiba o nome significativo de mensagens na tabela de dados para cada. Se o nome do computador estiver ausente, será usado o computador local. Se você especificar uma mensagem sem um nome de computador, será enviada a mensagem para o computador local. 



## <a name="examples"></a>Exemplos

#### <a name="list-the-available-messages-on-the-local-machine"></a>Lista as mensagens disponíveis no computador local 
`SendSchedule /L` 

#### <a name="list-the-available-messages-on-the-client-mypc"></a>Liste as mensagens disponíveis no cliente MyPC: 
`SendSchedule /L MyPC`

#### <a name="trigger-hardware-inventory-on-the-local-machine"></a>Disparar inventário de hardware no computador local
`SendSchedule {00000000-0000-0000-0000-000000000001}`

#### <a name="trigger-hardware-inventory-on-mypc"></a>Disparar inventário de hardware em MyPC: 
`SendSchedule {00000000-0000-0000-0000-000000000001} MyPC` 

#### <a name="trigger-the-evaluation-of-a-specific-configuration-baseline-on-mypc"></a>Disparar a avaliação de uma linha de base de configuração específica em MyPC: 
`SendSchedule ScopeId_611E8382-C064-4B62-B0DE-EFFB52AE8994/Baseline_36722778-69dd-4423-9632-b61148b2b67e MyPC` 



## <a name="bkmk_sendschedule-guids"></a> IDs da Mensagem

|ID da mensagem  |Nome para Exibição  |
|---------|---------|
|{00000000-0000-0000-0000-000000000001}|Inventário de hardware|
|{00000000-0000-0000-0000-000000000002}|Inventário de software|
|{00000000-0000-0000-0000-000000000003}|Inventário de Descoberta|
|{00000000-0000-0000-0000-000000000010}|Coleta de Arquivos|
|{00000000-0000-0000-0000-000000000011}|Coleta de IDMIF|
|{00000000-0000-0000-0000-000000000021}|Solicitar Atribuições de Computador|
|{00000000-0000-0000-0000-000000000022}|Avaliar Políticas de Computador|
|{00000000-0000-0000-0000-000000000023}|Atualizar Tarefa de MP Padrão|
|{00000000-0000-0000-0000-000000000024}|Tarefa de Locais de Atualização do LS (Serviço de Localização)|
|{00000000-0000-0000-0000-000000000025}|Tarefa de Atualização de Tempo Limite do LS|
|{00000000-0000-0000-0000-000000000026}|Atribuição de Solicitação de Agente de Política (Usuário)|
|{00000000-0000-0000-0000-000000000027}|Atribuição de Avaliação de Agente de Política (Usuário)|
|{00000000-0000-0000-0000-000000000031}|Medição de Software Gerando Relatório de Uso|
|{00000000-0000-0000-0000-000000000032}|Mensagem de Atualização de Origem|
|{00000000-0000-0000-0000-000000000037}|Limpeza do cache de configurações de proxy|
|{00000000-0000-0000-0000-000000000040}|Limpeza do Agente de Política de Computador|
|{00000000-0000-0000-0000-000000000041}|Limpeza do Agente de Política de Usuário|
|{00000000-0000-0000-0000-000000000042}|Política de Computador de Validação do Agente de Política/Atribuição|
|{00000000-0000-0000-0000-000000000043}|Política de Usuário de Validação do Agente de Política/Atribuição|
|{00000000-0000-0000-0000-000000000051}|Repetição/Atualização de certificados do AD no MP|
|{00000000-0000-0000-0000-000000000061}|Relatório de Status de DP de par|
|{00000000-0000-0000-0000-000000000062}|Agendamento da verificação de pacote Pendente do DP de par|
|{00000000-0000-0000-0000-000000000063}|Agendamento de instalação de Atualizações de SUM|
|{00000000-0000-0000-0000-000000000071}|Ação de NAP|
|{00000000-0000-0000-0000-000000000101}|Ciclo de Coleta de Inventário de Hardware|
|{00000000-0000-0000-0000-000000000102}|Ciclo de Coleta de Inventário de Software|
|{00000000-0000-0000-0000-000000000103}|Ciclo de Coleta de Dados de Descoberta|
|{00000000-0000-0000-0000-000000000104}|Ciclo de Coleta de Arquivos|
|{00000000-0000-0000-0000-000000000105}|Ciclo de Coleta de IDMIF|
|{00000000-0000-0000-0000-000000000106}|Ciclo de Relatório de Uso de Medição de Software|
|{00000000-0000-0000-0000-000000000107}|Ciclo de Atualização de Lista de Origens do Windows Installer|
|{00000000-0000-0000-0000-000000000108}|Ciclo de Avaliação de Atribuições de Atualizações de Software da Ação da Política de Atualizações de Software|
|{00000000-0000-0000-0000-000000000109}|Tarefa de Manutenção de Ponto de Distribuição de Branch de Política de Manutenção de PDP|
|{00000000-0000-0000-0000-000000000110}|Política de DCM|
|{00000000-0000-0000-0000-000000000111}|Enviar Mensagem de Estado Não Enviada|
|{00000000-0000-0000-0000-000000000112}|Limpeza de cache de política do Sistema de Estado|
|{00000000-0000-0000-0000-000000000113}|Atualizar a política de origem|
|{00000000-0000-0000-0000-000000000114}|Atualizar a Política de Repositório|
|{00000000-0000-0000-0000-000000000115}|Envio em massa da política do sistema de estado alta|
|{00000000-0000-0000-0000-000000000116}|Envio em massa da política do sistema de estado baixa|
|{00000000-0000-0000-0000-000000000120}|Política de Verificação de Status de AMT|
|{00000000-0000-0000-0000-000000000121}|Ação da política do gerenciador de aplicativo|
|{00000000-0000-0000-0000-000000000122}|Ação da política de usuário do gerenciador de aplicativo|
|{00000000-0000-0000-0000-000000000123}|Ação de avaliação global do gerenciador de aplicativo|
|{00000000-0000-0000-0000-000000000131}|Summarizer de início do gerenciamento de energia|
|{00000000-0000-0000-0000-000000000221}|Reavaliar implantação do ponto de extremidade|
|{00000000-0000-0000-0000-000000000222}|Reavaliar política de AM do ponto de extremidade|
|{00000000-0000-0000-0000-000000000223}|Detecção de evento externo|



