---
title: Gerenciar e monitorar implantações em fases
titleSuffix: Configuration Manager
description: Entenda como gerenciar e monitorar implantações em fases para software no Configuration Manager.
ms.date: 04/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f378fd399a874b0db3844bbf02528dfe92981db5
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500660"
---
# <a name="manage-and-monitor-phased-deployments"></a>Gerenciar e monitorar implantações em fases

Este artigo descreve como gerenciar e monitorar implantações em fases. As tarefas de gerenciamento incluem iniciar manualmente a próxima fase e suspender ou retomar uma fase. 

Primeiro, você precisa criar uma implantação em fases: 
- [Aplicativo](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  
- [Atualização de software](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)  
- [Sequência de tarefas](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)  



## <a name="bkmk_move"></a> Ir para a próxima fase

Quando você seleciona a configuração, **Iniciar manualmente a segunda fase da implantação**, o site não inicia automaticamente a próxima fase com base em critérios de sucesso. Você precisa levar a implantação em fases para a próxima fase.  

1. Como iniciar essa ação varia de acordo com o tipo de software implantado:  

    - **Aplicativo** (somente na versão 1806 ou posteriores): acesse o workspace **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e selecione **Aplicativos**.   

    - **Atualização de software** (somente na versão 1810 ou posterior): vá para o workspace **Biblioteca de Software** e, em seguida, selecione um dos seguintes nós:    
        - Atualizações de software  
            - **Todas as Atualizações de Software**  
            - **Grupos de Atualizações de Software**   
        - Serviço do Windows 10, **Todas as Atualizações do Windows 10**  
        - Gerenciamento de Cliente do Office 365, **Atualizações do Office 365**  

    - **Sequência de tarefas**: acesse o workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Sequência de Tarefas**.   

2. Selecione o software com a implantação em fases.  

3. No painel de detalhes, mude para a guia **Implantações em Fases**.  

4. Selecione a implantação em fases e, em seguida, clique em **Mover para a próxima fase** na faixa de opções.  

    ![Clique com o botão direito do mouse no menu que mostra ações em uma implantação em fases](media/Suspend-phased-deployment.PNG)



## <a name="bkmk_suspend"></a> Suspender e retomar fases 

Talvez você precise suspender manualmente ou retomar uma implantação em fases. Por exemplo, você pode criar uma implantação em fases para uma sequência de tarefas. Enquanto monitora a fase para seu grupo piloto, você observa um grande número de falhas. Você suspende a implantação em fases para impedir que mais dispositivos executem a sequência de tarefas. Depois de resolver o problema, você retoma a implantação em fases para continuar a distribuição. 

1. Como iniciar essa ação varia de acordo com o tipo de software implantado:  

    - **Aplicativo** (somente na versão 1806 ou posteriores): acesse o workspace **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e selecione **Aplicativos**.   

    - **Atualização de software** (somente na versão 1810 ou posterior): vá para o workspace **Biblioteca de Software** e, em seguida, selecione um dos seguintes nós:    
        - Atualizações de software  
            - **Todas as Atualizações de Software**  
            - **Grupos de Atualizações de Software**   
        - Serviço do Windows 10, **Todas as Atualizações do Windows 10**  
        - Gerenciamento de Cliente do Office 365, **Atualizações do Office 365**  

    - **Sequência de tarefas**: acesse o workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Sequência de Tarefas**. Selecione uma sequência de tarefas existente e clique em **Criar Implantação em Fases** na faixa de opções.  

2. Selecione o software com a implantação em fases.  

3. No painel de detalhes, mude para a guia **Implantações em Fases**.  

4. Selecione a implantação em fases e clique em **Suspender** ou **Retomar** na faixa de opções.  

<!-- Removed for 1806, need to clarify behavior with engineering
When you suspend a phased deployment, it sets the available and deadline times on the active deployments to a future time. When you resume, it generates a new schedule based on when you resume the phased deployment. The new schedule helps to avoid problems if you resume after the original deadline. For example, the initial schedule has the required deadline seven days after the deployment is available. You suspend it on the second day. If you aren't ready to resume it until day eight, you don't want the deployment to be immediately past the deadline. So it generates a new deadline starting from when you resume the phased deployment on day eight. 
-->


## <a name="bkmk_monitor"></a> Monitorar
<!--1358577-->
A partir da versão 1902, as implantações em fases têm seu próprio nó de monitoramento dedicado, facilitando a identificação de implantações em fases criadas por você e a navegação até a exibição de monitoramento de implementações em fases. No espaço de trabalho **Monitoramento**, selecione **Implantações em fases** e clique duas vezes em uma das implementações em fases para ver o status. <!--3555949-->

No Configuration Manager 1806 e 1810, você pode ver a experiência de monitoramento nativa para implantações em fases. No nó **Implantações** no workspace **Monitoramento**, selecione uma implantação em fases e clique em **Status da Implantação em Fases** na faixa de opções.

![Painel de status de implantação em fases, mostrando o status de duas fases](media/1358577-phased-deployment-status.png)

Este painel mostra as seguintes informações para cada fase da implantação:  

- **Total de dispositivos** ou **Total de recursos**: quantos dispositivos estão planejados por essa fase.  

- **Status**: o status atual desta fase. Cada fase pode estar em um dos seguintes estados:  

    - **Implantação criada**: a implantação em fases criou uma implantação do software para a coleção para essa fase. Os clientes são direcionados ativamente com este software.  

    - **Aguardando**: a fase anterior ainda não atendeu aos critérios de sucesso para que a implantação passe para essa fase.  

    - **Suspenso**: um administrador suspendeu a implantação.  

- **Progresso**: os estados de implantação com codificação de cores de clientes. Por exemplo: Êxito, Em Andamento, Erro, Requisitos Não Atendidos e Desconhecido. 

#### <a name="success-criteria-tile"></a>Bloco de critérios de sucesso

Use a lista suspensa **Selecionar Fase** para alterar a exibição do bloco **Critérios de Sucesso**. Esse bloco compara a **Meta de Fase** com a conformidade atual da implantação. Com as configurações padrão, a meta da fase é 95%. Esse valor significa que a implantação precisa de 95% de conformidade para ir para a próxima fase.

No exemplo, a meta da fase é de 65% e a conformidade atual é de 66,7%. A implantação em fases é movida automaticamente para a segunda fase, pois a primeira cumpriu os critérios de sucesso.  

   ![Exemplo de Critérios de Êxito do Status da Implantação em Fases em que a meta é de 65%](media/pod-status-success-criteria-tile.png)

A meta da fase é igual ao **Percentual de sucesso da implantação** nas Configurações de Fase para a *próxima* fase. Para a implantação em fases iniciar a próxima fase, essa segunda fase define os critérios para o sucesso da primeira fase. Para exibir essa configuração: 

1. Vá para o objeto de implantação em fases no software e abra as Propriedades de Implantação em Fases.  

2. Mude para a guia **Fases**. Selecione **Fase 2** e clique em **Exibição**.  

3. Na janela Propriedades da fase, mude para a guia **Configurações da Fase**.  

4. Exiba o valor para **Percentual de sucesso da implantação** no grupo *Critérios para o sucesso da fase anterior*.  

Por exemplo, as propriedades a seguir são para a mesma fase que o bloco de critérios de sucesso mostrado acima, em que os critérios são de 65%:  
![Guia Configurações de fase em propriedades da fase](media/phase-properties-phase-settings.png)

