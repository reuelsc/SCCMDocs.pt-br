---
title: "Monitorar conteúdo | System Center Configuration Manager"
description: "Entenda como monitorar o conteúdo distribuído usando o console do Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 402c06ed92bbfe509206d3e7800e41e90c5d3a38

---
# <a name="monitor-content-you-have-distributed-with-system-center-configuration-manager"></a>Monitorar o conteúdo que você distribuiu com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o console do System Center Configuration Manager para monitorar o conteúdo distribuído, incluindo:  

-   O status de todos os tipos de pacotes em relação aos pontos de distribuição associados  

-   O status de validação de conteúdo para o conteúdo de um pacote  

-   O status do conteúdo atribuído a um grupo de pontos de distribuição específico  

-   O estado do conteúdo atribuído a um ponto de distribuição  

-   O status de recursos opcionais de cada ponto de distribuição (validação de conteúdo, PXE e multicast).  

> [!NOTE]  
>  O Configuration Manager monitora somente o conteúdo em um ponto de distribuição que está na biblioteca de conteúdo. O conteúdo armazenado no ponto de distribuição no pacote ou os compartilhamentos personalizados não são monitorados.  

##  <a name="a-namebkmkcontentstatusa-content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Monitoramento de status do conteúdo  
 O nó **Status do Conteúdo** no espaço de trabalho **Monitoramento** fornece informações sobre os pacotes de conteúdo. No console do Configuration Manager, você pode examinar informações como:  

-   O nome do pacote  

-   Tipo  

-   Para quantos pontos de distribuição um pacote foi enviado  

-   A taxa de conformidade  

-   Quando o pacote foi criado  

-   ID do Pacote  

-   Versão de origem  

Você também encontrará informações detalhadas de status para qualquer pacote, bem como o status de distribuição para o pacote, incluindo:  

-   Número de falhas  

-   distribuições pendentes  

-   O número de instalações  

Você também pode gerenciar as distribuições que continuam em andamento para um ponto de distribuição ou que falharam em distribuir com sucesso o conteúdo para um ponto de distribuição:  

-   A opção aplicável para cancelar ou redistribuir o conteúdo estará disponível ao exibir a mensagem de status de implantação de um trabalho de distribuição a um ponto de distribuição no painel **Detalhes de Ativo** ou na guia **Em andamento** ou na **Erro** do nó **Status de Conteúdo** .  

-   Adicionalmente, os detalhes do trabalho exibem a porcentagem do trabalho que já foi concluída ao exibir os detalhes de um trabalho na guia **Em andamento** e o número de novas tentativas que restam para o trabalho, assim como quanto tempo antes de acontecer uma nova tentativa, ao exibir os detalhes do trabalho disponível na guia **Erro** .  

Ao cancelar uma implantação que ainda não foi concluída, o trabalho de distribuição para transferir tal conteúdo é interrompido:  

-   O status da implantação é atualizado para indicar que a distribuição falhou e foi cancelada por uma ação do usuário.  

-   Esse novo status aparece na guia **Erro** .  

> [!TIP]  
>  Quando uma implantação está perto de ser concluída, é possível que a ação para cancelar essa distribuição não seja processada antes que a distribuição para o ponto de distribuição seja concluída. Quando isso ocorre, a ação para cancelar a implantação é ignorada e o status da implantação é exibido como bem-sucedido.  

> [!NOTE]  
>  Embora seja possível selecionar a opção para cancelar uma distribuição a um ponto de distribuição localizado em um servidor do site, isso não tem efeito. Isso ocorre porque o servidor do site e o ponto de distribuição em um servidor do site compartilham o mesmo armazenamento de conteúdo de instância única e, na verdade, não há nenhum trabalho de distribuição a ser cancelado.  

Ao redistribuir o conteúdo que previamente falhou na transferência a um ponto de distribuição, o Configuration Manager imediatamente começa a implantar aquele conteúdo ao ponto de distribuição novamente e atualiza o status da implantação para refletir o estado em andamento da reimplantação.  

Use os procedimentos a seguir para exibir o status do conteúdo e gerenciar as distribuições que permanecem em andamento ou que falharam.  

#### <a name="to-monitor-content-status"></a>Para monitorar o status do conteúdo  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Status da Distribuição**e clique em **Status do Conteúdo**. Os pacotes são exibidos.  

3.  Selecione o pacote no qual você deseja informações detalhadas de status.  

4.  Na guia **Início** , clique em **Exibir Status**. As informações detalhadas de status para o pacote são exibidas.  

#### <a name="to-cancel-a-distribution-that-remains-in-progress"></a>Para cancelar uma distribuição que permanece em andamento  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Status da Distribuição**e clique em **Status do Conteúdo**. Os pacotes são exibidos.  

3.  Selecione o pacote que deseja gerenciar e, no painel de detalhes, clique em **Exibir Status**.  

4.  No painel **Detalhes de Ativo** da guia **Em andamento** , clique com o botão direito do mouse na entrada da distribuição que deseja cancelar e selecione **Cancelar**.  

5.  Clique em **Sim** para confirmar a ação e cancelar o trabalho de distribuição ao ponto de distribuição.  

#### <a name="to-redistribute-content-that-failed-to-distribute"></a>Para redistribuir conteúdo que falhou ao ser distribuído  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Status da Distribuição**e clique em **Status do Conteúdo**. Os pacotes são exibidos.  

3.  Selecione o pacote que deseja gerenciar e, no painel de detalhes, clique em **Exibir Status**.  

4.  No painel **Detalhes de Ativo** da guia **Erro** , clique com o botão direito do mouse na entrada da distribuição que deseja redistribuir e selecione **Redistribuir**.  

5.  Clique em **Sim** para confirmar a ação e iniciar o processo de redistribuição ao ponto de distribuição.  

## <a name="distribution-point-group-status"></a>Status do grupo de pontos de distribuição  
O nó **Status do Grupo de Pontos de Distribuição** no espaço de trabalho **Monitoramento** fornece informações sobre grupos de pontos de distribuição. Você pode examinar informações como:  

-   O nome do grupo de ponto de distribuição  

-   Descrição  

-   Quantos pontos de distribuição são membros do grupo de pontos de distribuição  

-   Quantos pacotes foram atribuídos ao grupo  

-   Status do grupo de pontos de distribuição  

-   Taxa de conformidade  

Você também pode exibir informações detalhadas para o seguinte:  

-   Erros para o grupo de pontos de distribuição,  

-   Quantas distribuições estão em andamento  

-   Quantas foram sido distribuídas com sucesso  

#### <a name="to-monitor-distribution-point-group-status"></a>Para monitorar o status do grupo de pontos de distribuição  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Status da Distribuição**e clique em **Status do Grupo de Pontos de Distribuição**. Os grupos de pontos de distribuição são exibidos.  

3.  Selecione o grupo de pontos de distribuição no qual você deseja informações detalhadas de status.  

4.  Na guia **Início** , clique em **Exibir Status**. As informações detalhadas de status para o grupo de pontos de distribuição são exibidas.  

## <a name="distribution-point-configuration-status"></a>Status de configuração de pontos de distribuição  
 O nó **Status de Configuração de Pontos de Distribuição** no espaço de trabalho **Monitoramento** fornece informações sobre o ponto de distribuição. É possível verificar quais atributos estão habilitados para o ponto de distribuição, como PXE, multicast e validação de conteúdo, e o status da distribuição para o ponto de distribuição. É possível também exibir informações detalhadas para o ponto de distribuição.  

> [!WARNING]  
>  O status de configuração de pontos de distribuição é relativo às últimas 24 horas. Se ocorrer um erro no ponto de distribuição e ele se recuperar, o status de erro poderá ser exibido por até 24 horas após a recuperação do ponto de distribuição.  

Use o procedimento a seguir para exibir o status de configuração de pontos de distribuição.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Para monitorar o status de configuração de pontos de distribuição  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Status da Distribuição**e clique em **Status de Configuração de Pontos de Distribuição**. Os pontos de distribuição são exibidos.  

3.  Selecione o ponto de distribuição no qual você deseja informações sobre o status de ponto de distribuição.  

4.  No painel de resultados, clique na guia **Detalhes** . As informações de status para o ponto de distribuição são exibidas.  



<!--HONumber=Nov16_HO1-->


