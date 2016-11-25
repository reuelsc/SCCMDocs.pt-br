---
title: "Tarefas comuns para criar e implantar linhas de base de configuração com o System Center Configuration Manager | System Center Configuration Manager"
description: "Saiba como criar e implantar as linhas de base de configuração no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4bb6afeb-d267-4f9b-ade2-26e5400c223b
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0d66240408dcd65576954ffb27395d3f05f5a41e


---
# <a name="common-tasks-for-creating-and-deploying-configuration-baselines-with-system-center-configuration-manager"></a>Tarefas comuns para criar e implantar linhas de base de configuração com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico contém cenários comuns para ajudar a saber mais sobre como criar e implantar linhas de base de configuração do System Center Configuration Manager.  

 Se já está familiarizado com as configurações de conformidade, a documentação detalhada sobre todos os recursos que podem ser usados pode ser encontrada nos tópicos [Criar linhas de base de configuração](../../compliance/deploy-use/create-configuration-baselines.md) e [Implantar linhas de base de configuração](../../compliance/deploy-use/deploy-configuration-baselines.md).  

 Antes de começar, leia a [Introdução às configurações de conformidade no System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md) para aprender algumas noções básicas sobre as configurações de conformidade e [Planejar e definir as configurações de conformidade](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) para implementar os pré-requisitos necessários.  

## <a name="create-a-configuration-baseline"></a>Criar uma linha de base de configuração  
 Neste exemplo, você criou um item de configuração apenas para computadores com Windows 10 que executam o cliente do Configuration Manager.  

 Este item de configuração impõe uma senha necessária de, pelo menos, 6 caracteres em PCs com Windows 10. O item de configuração é nomeado **Imposição de Senha do Windows 10**.  

No procedimento a seguir, você aprenderá a adicionar este item de configuração a uma linha de base de configuração para prepará-lo para implantação.  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Linhas de Base de Configuração**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Linha de Base de Configuração**.  

4.  Na caixa de diálogo **Criar Linha de Base de Configuração** , configure o seguinte:  

    -   **Nome** -Digite **Senhas do Windows 10** (ou outro nome de sua escolha)  

5.  Clique em **Adicionar** > **Itens de Configuração**.  

6.  Na caixa de diálogo **Adicionar Itens de Configuração** , selecione o item de configuração **Imposição de Senha do Windows 10** que você criou anteriormente e clique em **Adicionar**.  

7.  Clique em OK para fechar a caixa de diálogo **Adicionar Itens de Configuração** e voltar para a caixa de diálogo **Criar Linha de Base de Configuração** , que deve ser semelhante a esta captura de tela:  

     ![Caixa de diálogo Criar Linha de Base de Configuração](/sccm/compliance/plan-design/media/Create-Configuration-Baseline.png)  

8.  Clique em **OK** para fechar a caixa de diálogo **Criar Linha de Base de Configuração** .  

 Agora você pode ver a linha de base de configuração recém-criada no nó **Linhas de Base de Configuração** do console do Configuration Manager.  

## <a name="deploy-the-configuration-baseline"></a>Implantar a linha de base de configuração  
 Neste exemplo, você implantará a linha de base de configuração criada no procedimento anterior em uma coleção de computadores.  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Linhas de Base de Configuração**.  

3.  Na lista de linhas de base de configuração, selecione **Senhas do Windows 10**.  

4.  Na guia **Início** , no grupo **Implantação** , clique em **Implantar**.  

5.  Na caixa de diálogo **Implantar Linhas de Base de Configuração** , configure o seguinte:  

    -   **Linhas de base de configuração selecionadas** - Verifique se a linha de base de configuração das **Senhas do Windows 10** foi automaticamente adicionada a essa lista.  

    -   **Corrigir regras não compatíveis quando suportadas** ‑ Marque esta caixa para garantir que, se as configurações corretas não estiverem presentes nos dispositivos de destino, elas serão corrigidas pelo Configuration Manager.  

    -   **Coleção** - Clique em **Procurar** para escolher a coleção de computadores em que a linha de base de configuração será avaliada e corrigida quanto à conformidade. Neste exemplo, a linha de base de configuração foi implantada na coleção interna **Todos os Clientes de Desktop e de Servidor** .  

        > [!TIP]  
        >  Não se preocupe se a coleção que você escolher contém computadores ou dispositivos que não executam o Windows 10. Já que você configurou as plataformas com suporte no item de configuração criado, somente os PCs com Windows 10 serão avaliados quanto à conformidade.  

    -   Se necessário, configure o agendamento pelo qual a linha de base de configuração será avaliada. Caso contrário, mantenha o padrão de **7 Dias**.  

6.  A caixa de diálogo agora terá a seguinte aparência:  

     ![Caixa de diálogo Implantar linhas de base de configuração](/sccm/compliance/plan-design/media/Deploy-configuration-baselines.png)  

7.  Clique em **OK** para fechar a caixa de diálogo **Implantar Linhas de Base de Configuração** e criar a implantação.  

 Se quiser dar uma olhada rápida nas estatísticas de conformidade dessa implantação, no espaço de trabalho **Monitoramento** , clique em **Implantações**. Na parte inferior da tela, você verá um gráfico **Estatísticas de Conformidade** .  

 Para obter informações mais detalhadas sobre como monitorar linhas de base de configuração, consulte [Monitorar configurações de conformidade](../../compliance/deploy-use/monitor-compliance-settings.md)  



<!--HONumber=Nov16_HO1-->


