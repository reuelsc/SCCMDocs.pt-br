---
title: Planejar e definir as configurações de conformidade
titleSuffix: Configuration Manager
description: Saiba mais sobre os pré-requisitos e as tarefas de configuração para trabalhar com configurações de conformidade no System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9ea20b01-676a-4cc2-b328-0098a41b202e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2d728dae6dc67a4c66403bdb2299e50dcd6e3557
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67677936"
---
# <a name="plan-for-and-configure-compliance-settings-in-system-center-configuration-manager"></a>Planejar e definir as configurações de conformidade no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de começar a trabalhar com as configurações de conformidade do System Center Configuration Manager, há alguns pré-requisitos que você precisa conhecer e algumas tarefas de configuração que precisará executar.  

## <a name="prerequisites-for-compliance-settings"></a>Pré-requisitos para configurações de conformidade  

|Pré-requisito|Mais informações|  
|------------------|----------------------|  
|Clientes do Windows Configuration Manager devem estar habilitados e configurados para a avaliação da conformidade.|Veja abaixo|  
|Se desejar executar relatórios, você deve configurar relatórios para seu site.|[Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md)|  
|Permissões de segurança necessárias.|A função de segurança **Gerenciador de Configurações de Conformidade** inclui as permissões necessárias para gerenciar configurações de conformidade, itens de configuração de perfis e dados do usuário e perfis de conexão remota.<br /><br /> [Configurar administração baseada em funções](../../core/servers/deploy/configure/configure-role-based-administration.md)|  

##  <a name="enable-and-configure-compliance-settings-for-windows-pcs-only"></a>Habilitar e definir configurações de conformidade (somente para computadores Windows)  

Este procedimento define as configurações de conformidade padrão do cliente e se aplica a todos os computadores em sua hierarquia. Se quiser que essas configurações se apliquem somente a alguns computadores, crie uma configuração personalizada do cliente do dispositivo e atribua-a a uma coleção que contém os computadores nos quais deseja usar as configurações de conformidade. Para obter mais informações sobre como criar configurações personalizadas do dispositivo, consulte [Como definir as configurações do cliente](../../core/clients/deploy/configure-client-settings.md).  

> [!TIP]  
>  Outros tipos de dispositivo não exigem nenhuma configuração específica para avaliar as configurações de conformidade.  

1.  No console do Configuration Manager, escolha **Administração** > **Configurações do Cliente** > **Configurações Padrão**.  
2.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  
3.  Na caixa de diálogo **Configurações Padrão** , clique em **Configurações de Conformidade**.  
4.  Defina as seguintes configurações de conformidade do cliente:
    - **Habilitar a avaliação de conformidade em clientes** ‑ Defina como **Verdadeiro** se desejar avaliar a conformidade em dispositivos cliente.
    - **Agendar avaliação de conformidade** ‑ Clique em **Agenda** se você quiser modificar o agendamento da avaliação de conformidade padrão em dispositivos cliente.
    - **Habilitar Dados e Perfis do Usuário** ‑ Habilite esta opção se deseja criar e implantar itens de configuração de perfis e dados do usuário em computadores com Windows. Para obter detalhes, consulte [Criar itens de configuração de perfis e dados de usuário](/sccm/compliance/deploy-use/create-remote-connection-profiles).
5. Clique em **OK** para fechar a caixa de diálogo **Configurações Padrão** .  

Os computadores cliente são definidos com essas configurações na próxima vez que baixarem a política do cliente.  
