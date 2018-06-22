---
title: Implantar linhas de base de configuração
titleSuffix: Configuration Manager
description: Implante linhas de base de configuração para definir implantações da linha de base de configuração e para adicionar ou remover linhas de base de configuração de implantações.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9be8aaf3-075e-4acd-abd2-7459254e16e2
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c55382bf1fc377fd7e86f433a0cb92a5240eafa1
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32334701"
---
# <a name="how-to-deploy-configuration-baselines-in-system-center-configuration-manager"></a>Como implantar linhas de base de configuração no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As linhas de base de configuração no System Center Configuration Manager devem ser implantadas em uma ou mais coleções de usuários ou dispositivos antes que os dispositivos cliente nessas coleções possam avaliar sua própria conformidade com a linha de base de configuração.  

Use a caixa de diálogo **Implantar Linhas de Base de Configuração** para definir implantações da linha de base de configuração, que inclui a adição ou remoção de linhas de base de configuração de implantações, além de especificar o agendamento da avaliação.  

## <a name="deploy-a-configuration-baseline"></a>Implantar uma linha de base de configuração  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Linhas de Base de Configuração**.  

3.  Na lista **Linhas de Base de Configuração** , selecione a linha de base de configuração que deseja implantar e, na guia **Início** , no grupo **Implantação** , clique em **Implantar**.  

4.  Na caixa de diálogo **Implantar Linhas de Base de Configuração** , selecione as linhas de base de configuração que deseja implantar na lista **Linhas de Base de Configuração Disponíveis** . Clique em **Adicionar** para adicioná-los à lista **Linhas de base de configuração selecionadas** .  

    > [!IMPORTANT]  
    >  Se você alterar um item de configuração que foi adicionado a uma linha de base de configuração implantado, o item de configuração revisado não será avaliado quanto à conformidade até seu próximo horário de avaliação agendado.  

5.  Especifique essas outras informações:  

    -   **Corrigir regras não compatíveis quando suportadas** – Corrige automaticamente quaisquer regras não compatíveis para o WMI (Instrumentação de Gerenciamento do Windows), o Registro, scripts e todas as configurações de dispositivos móveis registrados pelo Configuration Manager.  

    -   **Permitir correção fora da janela de manutenção** – Se uma janela de manutenção foi configurada para a coleção na qual você está implantando a linha de base de configuração, habilite esta opção para permitir que as configurações de conformidade corrijam o valor fora da janela de manutenção. Para obter mais informações sobre janelas de manutenção, consulte [Como usar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).  

6.  **Gerar um alerta** – Configura um alerta que será gerado se a conformidade da linha de base de configuração for menor que um percentual especificado por uma data e hora determinadas. Você também pode especificar se deseja que um alerta seja enviado para o System Center Operations Manager.  

7.  **Coleção** - Clique em **Procurar** para selecionar a coleção na qual deseja implantar a linha de base de configuração.  

8.  **Especificar o agendamento de avaliação de conformidade para esta linha de base de configuração** especifica o agendamento pelo qual a linha de base de configuração implantada é avaliada nos computadores cliente. Pode ser um agendamento simples ou personalizado.  

    > [!NOTE]  
    >  Se a linha de base de configuração for implantada em um computador, ela será avaliada quanto à conformidade no prazo de duas horas após a hora de início agendada. Se ela for implantada em um usuário, ela é avaliada quanto à conformidade quando o usuário fizer logon.  

9. Clique em **OK** para fechar a caixa de diálogo **Implantar Linhas de Base de Configuração** e criar a implantação. Para obter mais informações sobre como monitorar a implantação, consulte [Monitorar configurações de conformidade](/sccm/compliance/deploy-use/monitor-compliance-settings).  
