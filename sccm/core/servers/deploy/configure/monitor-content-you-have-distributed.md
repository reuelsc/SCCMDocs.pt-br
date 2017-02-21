---
title: "Monitorar o conteúdo | Microsoft Docs"
description: "Entenda como monitorar o conteúdo distribuído usando o console do Configuration Manager."
ms.custom: na
ms.date: 2/8/2017
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
ms.sourcegitcommit: 3b387d78e03cc2d1c535e52016d2de4945328f72
ms.openlocfilehash: c51cf3b3b7563a82db40405677c2edfb6de47cf1

---
# <a name="monitor-content-you-have-distributed-with-system-center-configuration-manager"></a>Monitorar o conteúdo que você distribuiu com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o console do System Center Configuration Manager para monitorar o conteúdo distribuído, incluindo:  

-   O status de todos os tipos de pacotes em relação aos pontos de distribuição associados.  
-   O status de validação de conteúdo para o conteúdo de um pacote.  
-   O status do conteúdo atribuído a um grupo de pontos de distribuição específico.  
-   O estado do conteúdo atribuído a um ponto de distribuição.  
-   O status de recursos opcionais de cada ponto de distribuição (validação de conteúdo, PXE e multicast).  

> [!NOTE]  
>  O Configuration Manager monitora somente o conteúdo em um ponto de distribuição que está na biblioteca de conteúdo. O conteúdo armazenado no ponto de distribuição no pacote ou os compartilhamentos personalizados não são monitorados.  

##  <a name="a-namebkmkcontentstatusa-content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Monitoramento de status do conteúdo  
 O nó **Status do Conteúdo** no espaço de trabalho **Monitoramento** fornece informações sobre os pacotes de conteúdo. No console do Configuration Manager, você pode examinar informações como:  

-   O nome do pacote.  
-   O tipo.  
-   Para quantos pontos de distribuição um pacote foi enviado.  
-   A taxa de conformidade.  
-   Quando o pacote foi criado.  
-   A ID do pacote.  
-   A versão de origem.  

Você também encontrará informações detalhadas de status para qualquer pacote, bem como o status de distribuição para o pacote, incluindo:  

-   A quantidade de falhas.  
-   As distribuições pendentes.  
-   O número de instalações.

Você também pode gerenciar as distribuições que continuam em andamento para um ponto de distribuição ou que falharam em distribuir com êxito o conteúdo para um ponto de distribuição:  

-   A opção para cancelar ou redistribuir o conteúdo fica disponível ao exibir a mensagem de status da implantação de um trabalho de distribuição para um ponto de distribuição no painel **Detalhes de Ativo**. Esse painel pode ser encontrado na guia **Em Andamento** ou na guia **Erro** do nó **Status de Conteúdo**.  
-   Além disso, os detalhes do trabalho exibem a porcentagem do trabalho que foi concluída ao exibir os detalhes de um trabalho na guia **Em Andamento**. Os detalhes do trabalho também exibem a quantidade de tentativas que restam para o trabalho, bem como o tempo para a próxima repetição ao exibir os detalhes de um trabalho que está disponível na guia **Erro**.  

Ao cancelar uma implantação que ainda não foi concluída, o trabalho de distribuição para transferir tal conteúdo é interrompido:  

-   O status da implantação é atualizado para indicar que a distribuição falhou e foi cancelada por uma ação do usuário.  
-   Esse novo status aparece na guia **Erro** .  

> [!TIP]  
>  Quando uma implantação está perto de ser concluída, é possível que a ação para cancelar essa distribuição não seja processada antes que a distribuição para o ponto de distribuição seja concluída. Quando isso ocorre, a ação para cancelar a implantação é ignorada e o status da implantação é exibido como bem-sucedido.  

> [!NOTE]  
>  Embora seja possível selecionar a opção para cancelar uma distribuição a um ponto de distribuição localizado em um servidor do site, isso não tem efeito. Isso ocorre porque o servidor de sites e o ponto de distribuição em um servidor de sites compartilham o mesmo armazenamento de conteúdo de instância única. Não há nenhum trabalho de distribuição real para cancelar.  

Ao redistribuir o conteúdo que, anteriormente, falhou na transferência a um ponto de distribuição, o Configuration Manager imediatamente começa a implantar aquele conteúdo no ponto de distribuição novamente. O Configuration Manager atualiza o status da implantação para mostrar o estado contínuo dessa nova implantação.  

Use os procedimentos a seguir para exibir o status do conteúdo e gerenciar as distribuições que permanecem em andamento ou que falharam.  

### <a name="to-monitor-content-status"></a>Para monitorar o status do conteúdo  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Status da Distribuição**e clique em **Status do Conteúdo**. Os pacotes são exibidos.  

3.  Selecione o pacote para o qual você deseja informações detalhadas de status.  

4.  Na guia **Início** , clique em **Exibir Status**. As informações detalhadas de status para o pacote são exibidas.  

### <a name="to-cancel-a-distribution-that-remains-in-progress"></a>Para cancelar uma distribuição que permanece em andamento  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Status da Distribuição**e clique em **Status do Conteúdo**. Os pacotes são exibidos.  

3.  Selecione o pacote que deseja gerenciar e, no painel de detalhes, clique em **Exibir Status**.  

4.  No painel **Detalhes de Ativo** da guia **Em Andamento**, clique com o botão direito do mouse na entrada da distribuição que deseja cancelar e selecione **Cancelar**.  

5.  Clique em **Sim** para confirmar a ação e cancelar o trabalho de distribuição ao ponto de distribuição.  

### <a name="to-redistribute-content-that-failed-to-distribute"></a>Para redistribuir conteúdo que falhou ao ser distribuído  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Status da Distribuição**e clique em **Status do Conteúdo**. Os pacotes são exibidos.  

3.  Selecione o pacote que deseja gerenciar e, no painel de detalhes, clique em **Exibir Status**.  

4.  No painel **Detalhes de Ativo** da guia **Erro**, clique com o botão direito do mouse na entrada da distribuição que deseja redistribuir e selecione **Redistribuir**.  

5.  Clique em **Sim** para confirmar a ação e iniciar o processo de redistribuição ao ponto de distribuição.  

## <a name="distribution-point-group-status"></a>Status do grupo de pontos de distribuição  
O nó **Status do Grupo de Pontos de Distribuição** no espaço de trabalho **Monitoramento** fornece informações sobre grupos de pontos de distribuição. Você pode examinar informações como:  

-   O nome do grupo de ponto de distribuição.  
-   A descrição.  
-   Quantos pontos de distribuição são membros do grupo de pontos de distribuição.  
-   Quantos pacotes foram atribuídos ao grupo.  
-   O status do grupo de pontos de distribuição.  
-   A taxa de conformidade.  

Você também pode exibir informações detalhadas para o seguinte:  

-   Erros do grupo de pontos de distribuição.  
-   Quantas distribuições estão em andamento.
-   Quantas distribuições foram distribuídas com êxito.  

### <a name="to-monitor-distribution-point-group-status"></a>Para monitorar o status do grupo de pontos de distribuição  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Status da Distribuição**e clique em **Status do Grupo de Pontos de Distribuição**. Os grupos de pontos de distribuição são exibidos.  

3.  Selecione o grupo de pontos de distribuição sobre o qual você deseja informações detalhadas de status.  

4.  Na guia **Início** , clique em **Exibir Status**. As informações detalhadas de status para o grupo de pontos de distribuição são exibidas.  

## <a name="distribution-point-configuration-status"></a>Status de configuração de pontos de distribuição  
 O nó **Status de Configuração de Pontos de Distribuição** no espaço de trabalho **Monitoramento** fornece informações sobre o ponto de distribuição. É possível verificar quais atributos estão habilitados para o ponto de distribuição, como PXE, multicast e validação de conteúdo, e o status da distribuição para o ponto de distribuição. É possível também exibir informações detalhadas para o ponto de distribuição.  

> [!WARNING]  
>  O status de configuração de pontos de distribuição é relativo às últimas 24 horas. Se ocorrer um erro no ponto de distribuição e ele se recuperar, o status de erro poderá ser exibido por até 24 horas após a recuperação do ponto de distribuição.  

Use o procedimento a seguir para exibir o status de configuração de pontos de distribuição.  

### <a name="to-monitor-distribution-point-configuration-status"></a>Para monitorar o status de configuração de pontos de distribuição  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Status da Distribuição**e clique em **Status de Configuração de Pontos de Distribuição**. Os pontos de distribuição são exibidos.  

3.  Selecione o ponto de distribuição sobre qual você deseja informações de status.  

4.  No painel de resultados, clique na guia **Detalhes** . As informações de status para o ponto de distribuição são exibidas.  

## <a name="client-data-sources-dashboard"></a>Painel Fontes de Dados do Cliente
Começando da versão 1610, é possível usar o painel **Fontes de Dados do Cliente** para ajudar a entender o uso do [Cache de Pares](/sccm/core/plan-design/hierarchy/client-peer-cache) em seu ambiente. Esse painel só estará visível no console depois que os clientes baixarem o conteúdo usando o Cache de Pares e relatarem as informações de volta para o site. Isso pode levar até 24 horas.

> [!TIP]  
> Com a versão 1610, o cache de pares e o painel de fontes de dados do cliente são recursos de pré-lançamento. Para habilitá-los, confira [Usar recursos de pré-lançamento de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

No console, acesse **Monitoramento** > **Status do cliente** > **Fontes de Dados do Cliente**. Aqui você pode escolher um período de tempo para aplicar ao painel. Em seguida, na exibição, escolha o grupo de limites ou o pacote do qual quer ver informações. Ao exibir as informações, você pode passar o mouse sobre a superfície para ver mais detalhes sobre conteúdo ou as origens da política.

Esses detalhes incluem o seguinte:  
- **Fontes de Conteúdo de Cliente**: exibe a origem da qual os clientes obtiveram conteúdos.
- **Pontos de distribuição**: exibe o número de pontos de distribuição que fazem parte do Grupo de Limites selecionado.
- **Clientes que usaram um ponto de distribuição**: com base no número de clientes que está no Grupo de Limites selecionado, mostra quantos usaram um ponto de distribuição para obter conteúdo.
- **Fontes de Cache de Pares**: mostra quantas fontes de cache de pares reportaram histórico de downloads para o Grupo de Limites selecionado.
- **Clientes que usaram um par**: com base no número de clientes que está no Grupo de Limites selecionado, mostra quantos usaram uma fonte de cache de pares para obter conteúdo.



Também é possível usar um novo relatório, **Fontes de Dados do Cliente — Resumo**, para exibir um resumo das fontes de dados do cliente de cada grupo de limites.



<!--HONumber=Feb17_HO2-->


