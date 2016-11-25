---
title: Monitorar aplicativos no console do System Center Configuration Manager | System Center Configuration Manager
description: "Monitorar a implantação de software, incluindo atualizações, configurações de conformidade e aplicativos usando o espaço de trabalho de monitoramento no Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 784c295c-b8b8-4202-ab9f-665908d49d6d
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ca82638267d6d9e1bb4eb6855785ac383a2191e9


---
# <a name="monitor-applications-from-the-system-center-configuration-manager-console"></a>Monitorar aplicativos no console do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


## <a name="introduction"></a>Introdução

No System Center Configuration Manager, é possível monitorar a implantação de todo software, inclusive de atualizações de software, configurações de conformidade, aplicativos, sequências de tarefas, pacotes e programas. Você pode monitorar implantações usando o espaço de trabalho **Monitoramento** no console do Configuration Manager ou usando relatórios.  

 Aplicativos no Configuration Manager dão suporte a monitoramento com base no estado, o que permite que você controle o último estado da implantação do aplicativo para usuários e dispositivos. Essas mensagens de estado exibem informações sobre dispositivos individuais. Por exemplo, se um aplicativo for implantado em um conjunto de usuários, será possível exibir o estado de conformidade e a finalidade da implantação no console do Configuration Manager.  

 O estado de implantação de um aplicativo apresenta um dos seguintes estados de conformidade:  

-   **Êxito** – A implantação do aplicativo foi bem-sucedida ou o aplicativo já estava instalado.  

-   **Em andamento** – A implantação do aplicativo está em andamento.  

-   **Desconhecido** – O estado da implantação do aplicativo não pôde ser determinado. Esse estado não é aplicável a implantações com a finalidade **Disponível**. Esse estado geralmente é exibido quando mensagens de estado do cliente ainda não foram recebidas.  

-   **Requisitos não atendidos** – O aplicativo não foi implantado porque não estava em conformidade com alguma dependência ou regra obrigatória, ou porque o sistema operacional em que ele estava implantado não era aplicável.  

-   **Erro** – O aplicativo falhou ao ser implantado devido a um erro.  
  
Você pode obter informações adicionais sobre todos os estados de conformidade, incluindo subcategorias dentro dos estados, bem como o número de usuários e dispositivos nessa categoria. Por exemplo, o estado de conformidade **Erro** inclui as seguintes subcategorias:  
  
-   Erro na avaliação de requisitos  

-   Erros relacionados ao conteúdo  

-   Erros de instalação  

 Quando mais de um estado de conformidade se aplica a uma implantação de aplicativo, é possível ver o estado agregado que representa a conformidade inferior. Por exemplo:  

-   Se um usuário fizer logon em dois dispositivos e o aplicativo for instalado com êxito em um dos dispositivos, mas falhar no outro, o estado de implantação agregado do aplicativo exibido para esse usuário será **Erro**.  

-   Se um aplicativo for implantado em todos os usuários que fizerem logon em um computador, você receberá vários resultados de implantação nesse computador. Se uma das implantações falhar, o estado de implantação agregado exibido para esse computador será **Erro**.  
  
O estado de implantação para implantações de pacote e programa não é agregado.  
  
 Use essas subcategorias para ajudá-lo a identificar rapidamente problemas importantes relacionados a implantações de aplicativos. Você também pode exibir informações adicionais sobre os dispositivos que se encaixarem em uma determinada categoria de um estado de conformidade.  

 O gerenciamento de aplicativos no Configuration Manager inclui diversos relatórios integrados que permitem monitorar informações sobre aplicativos e implantações. Esses relatórios possuem a categoria de relatório de **Distribuição de Software - Monitoramento de Aplicativo**.  

 Para obter mais informações sobre como configurar relatórios no Configuration Manager, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  
  
## <a name="monitor-the-state-of-an-application-in-the-configuration-manager-console"></a>Monitorar o estado de um aplicativo no console do Configuration Manager  
  
1.  No console do Configuration Manager, clique em **Monitoramento** > **Implantações**.  
  
3.  Para rever detalhes da implantação, sobre cada estado de conformidade e os dispositivos nesses estados, selecione uma implantação e, então, na guia **Início** , no grupo **Implantação** , clique em **Exibir Status** para abrir o painel **Status da Implantação** . Nesse painel, você pode exibir os ativos com cada estado de conformidade. Clique em qualquer ativo para exibir informações mais detalhadas sobre o status da implantação para esse ativo.  

    > [!NOTE]  
    >  O número de itens que podem ser exibidos no painel **Status da Implantação** é limitado a 20.000. Se precisar visualizar mais itens, use os relatórios do Configuration Manager para ver dados de status do aplicativo.  
    >   
    >  O status dos tipos de implantação é agregado ao painel **Status da Implantação** . Para exibir informações mais detalhadas sobre os tipos de implantação, use o relatório **Erros de infraestrutura de aplicativo** na categoria de relatório **Distribuição de Software – Monitoramento de Aplicativo**.  

4.  Para rever informações de status geral de uma implantação de aplicativo, selecione uma implantação e, então, clique na guia **Resumo** na janela **Implantação Selecionada** .  

5.  Para rever informações sobre o tipo de implantação de aplicativos, selecione uma implantação e, então, clique na guia **Tipos de Implantação** na janela **Implantação Selecionada** .  

As informações mostradas no painel **Status da Implantação**, após clicar em **Exibir Status**, são dados reais do banco de dados do Configuration Manager. As informações mostradas na guia **Resumo** e na guia **Tipos de Implantação** são dados resumidos. Se os dados mostrados na guia **Resumo** e na guia **Tipos de Implantação** não corresponderem aos dados mostrados no painel **Status da Implantação** , clique em **Executar Resumo** para atualizar os dados nessas guias. Você pode configurar o intervalo de resumo de implantação de aplicativos padrão da seguinte maneira:  
1. No console do Configuration Manager, clique em **Administração** > **Configuração do Site** > **Sites**.
2. Na lista **Locais** , selecione o local para o qual deseja configurar o intervalo de resumo e, então, na guia **Início** , no grupo **Configurações** , clique em **Summarizers de Status**.
3. Na caixa de diálogo **Summarizers de Status** , clique em **Summarizer de Implantação de Aplicativos**e, então, clique em **Editar**.  
4. Na caixa de diálogo **Propriedades do Summarizer de Implantação de Aplicativos** , configure os intervalos de resumo necessários e clique em **OK**.  



<!--HONumber=Nov16_HO1-->


