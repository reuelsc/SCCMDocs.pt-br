---
title: Monitorar aplicativos do console
titleSuffix: Configuration Manager
description: Monitorar a implantação de software, incluindo atualizações, configurações de conformidade e aplicativos usando o workspace de monitoramento no Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 784c295c-b8b8-4202-ab9f-665908d49d6d
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 129223a111085854ede038575653655ad13884dd
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53423806"
---
# <a name="monitor-applications-from-the-system-center-configuration-manager-console"></a>Monitorar aplicativos no console do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


No System Center Configuration Manager, é possível monitorar a implantação de todo software, inclusive de atualizações de software, configurações de conformidade, aplicativos, sequências de tarefas, pacotes e programas. Você pode monitorar implantações usando o workspace **Monitoramento** no console do Configuration Manager ou usando relatórios.  

 Os aplicativos do Configuration Manager dão suporte ao monitoramento baseado em estado, o que permite acompanhar o último estado de implantação do aplicativo para usuários e dispositivos. Essas mensagens de estado exibem informações sobre dispositivos individuais. Por exemplo, se um aplicativo for implantado em um conjunto de usuários, será possível exibir o estado de conformidade e a finalidade da implantação no console do Configuration Manager.  

## <a name="learn-about-compliance-states-in-system-center-configuration-manager"></a>Saiba mais sobre os estados de conformidade do System Center Configuration Manager
 O estado de implantação de um aplicativo apresenta um dos seguintes estados de conformidade:  

-   **Êxito** – A implantação do aplicativo foi bem-sucedida ou o aplicativo já estava instalado.  

-   **Em andamento** – A implantação do aplicativo está em andamento.  

-   **Desconhecido** – O estado da implantação do aplicativo não pôde ser determinado. Esse estado não é aplicável a implantações com a finalidade **Disponível**. Esse estado geralmente é exibido quando mensagens de estado do cliente ainda não foram recebidas.  

-   **Requisitos não atendidos** – O aplicativo não foi implantado porque não estava em conformidade com alguma dependência ou regra obrigatória, ou porque o sistema operacional em que ele estava implantado não era aplicável.  

-   **Erro** – O aplicativo falhou ao ser implantado devido a um erro.  

É possível exibir mais informações para cada estado de conformidade, incluindo subcategorias no estado de conformidade e o número de usuários e dispositivos nessa categoria. Por exemplo, o estado de conformidade **Erro** inclui as seguintes subcategorias:  

- Erro na avaliação de requisitos  

- Erros relacionados ao conteúdo  

- Erros de instalação  

  Quando mais de um estado de conformidade se aplica a uma implantação de aplicativo, é possível ver o estado agregado que representa a conformidade inferior. Por exemplo:  

  -   Se um usuário se conectar a dois dispositivos e o aplicativo for instalado com êxito em um dos dispositivos, mas falhar no outro, o estado de implantação agregado do aplicativo para esse usuário será exibido como **Erro**.  

  -   Se um aplicativo for implantado em todos os usuários que se conectarem a um computador, você receberá vários resultados de implantação nesse computador. Se uma das implantações falhar, o estado de implantação agregado exibido para esse computador será **Erro**.  

O estado de implantação para implantações de pacote e programa não é agregado.  

 Use essas subcategorias para ajudá-lo a identificar rapidamente problemas importantes relacionados a implantações de aplicativos. Você também pode exibir informações adicionais sobre os dispositivos que se encaixarem em uma determinada categoria de um estado de conformidade.  

 O gerenciamento de aplicativos no Configuration Manager inclui diversos relatórios internos que permitem monitorar informações sobre aplicativos e implantações. Esses relatórios possuem a categoria de relatório de **Distribuição de Software - Monitoramento de Aplicativo**.  

 Para obter mais informações sobre como configurar relatórios no Configuration Manager, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  

## <a name="monitor-the-state-of-an-application-in-the-configuration-manager-console"></a>Monitorar o estado de um aplicativo no console do Configuration Manager  

1.  No console do Configuration Manager, escolha **Monitoramento** > **Implantações**.  

3.  Para examinar os detalhes de implantação de cada estado de conformidade, bem como os dispositivos nesses estados, selecione uma implantação e, na guia **Início**, no grupo **Implantação**, escolha **Exibir Status** para abrir o painel **Status da Implantação**. Nesse painel, você pode exibir os ativos com cada estado de conformidade. Escolha qualquer ativo para exibir informações mais detalhadas sobre o status da implantação desse ativo.  

    > [!NOTE]  
    >  O número de itens que podem ser exibidos no painel **Status da Implantação** é limitado a 20.000. Se precisar visualizar mais itens, use os relatórios do Configuration Manager para ver dados de status do aplicativo.  
    >   
    >  O status dos tipos de implantação é agregado ao painel **Status da Implantação** . Para exibir informações mais detalhadas sobre os tipos de implantação, use o relatório **Erros de infraestrutura de aplicativo** na categoria de relatório **Distribuição de Software – Monitoramento de Aplicativo**.  

4.  Para examinar as informações de status geral de uma implantação de aplicativo, selecione uma implantação e escolha a guia **Resumo** na janela **Implantação Selecionada**.  

5.  Para examinar as informações do tipo de implantação de aplicativos, selecione uma implantação e escolha a guia **Tipos de Implantação** na janela **Implantação Selecionada**.  

As informações mostradas no painel **Status da Implantação** após a escolha de **Exibir Status** são dados dinâmicos do banco de dados do Configuration Manager. As informações mostradas nas guias **Resumo** e **Tipos de Implantação** são dados resumidos.

Se os dados mostrados nas guias **Resumo** e **Tipos de Implantação** não corresponderem aos dados mostrados no painel **Status da Implantação**, escolha **Executar Resumo** para atualizar os dados nessas guias. Você pode configurar o intervalo de resumo de implantação de aplicativos padrão da seguinte maneira:  

1. No console do Configuration Manager, escolha **Administração** > **Configuração de Site** > **Sites**.

2. Na lista **Sites**, selecione o site para o qual você deseja configurar o intervalo de resumo e, em seguida, na guia **Início**, no grupo **Configurações**, escolha **Status Summarizers**.

3. Na caixa de diálogo **Status Summarizers**, escolha **Summarizer de Implantação de Aplicativos** e **Editar**.  

4. Na caixa de diálogo **Propriedades do Summarizer de Implantação de Aplicativos**, configure os intervalos de resumo necessários e escolha **OK**.  
