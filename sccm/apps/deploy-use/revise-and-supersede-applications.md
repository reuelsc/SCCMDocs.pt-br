---
title: Revisar e substituir aplicativos | System Center Configuration Manager
description: "Trabalhe com versões de aplicativos do System Center Configuration Manager e os substitua."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30170d70-489f-47f7-bebf-9ed0115db26b
caps.latest.revision: 7
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ae6440375d6e801ac9c3932872ec1367d9c601a8


---
# <a name="how-to-revise-and-supersede-applications-in-system-center-configuration-manager"></a>Como revisar e substituir aplicativos no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Neste tópico, você aprenderá a trabalhar com versões de aplicativo do System Center Configuration Manager e como substituir aplicativos por uma nova versão.  

##  <a name="application-revisions"></a>Revisões de aplicativos  
 Quando você faz revisões em um aplicativo ou em um tipo de implantação contido em um aplicativo, o Configuration Manager cria uma nova revisão do aplicativo. Você pode exibir o histórico de revisão de cada aplicativo. Além disso, você pode exibir suas propriedades, restaurar uma revisão anterior de um aplicativo ou excluir uma revisão antiga.  

### <a name="to-display-an-application-revision-history"></a>Para exibir um histórico de revisão do aplicativo  

1.  No console do Configuration Manager, clique em **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos** e clique no aplicativo desejado.  

3.  Na guia **Início** , no grupo **Aplicativo** , clique em **Histórico de Revisão** para abrir a caixa de diálogo **Histórico de Revisão de Aplicativo** .  

### <a name="to-view-an-application-revision"></a>Para exibir uma revisão do aplicativo  

1.  Na caixa de diálogo **Histórico de Revisão de Aplicativo** , selecione uma revisão do aplicativo e clique em **Exibir**.  

2.  Na caixa de diálogo **Propriedades** , examine as propriedades do aplicativo selecionado.  

    > [!NOTE]  
    >  As propriedades do aplicativo que são exibidas são somente leitura.  

3.  Feche a caixa de diálogo **Propriedades** .  

### <a name="to-restore-an-application-revision"></a>Para restaurar uma revisão do aplicativo  

1.  Na caixa de diálogo **Histórico de Revisão de Aplicativo** , selecione uma revisão do aplicativo e clique em **Restaurar**.  

2.  Na caixa de diálogo **Confirmar Restauração da Revisão** , clique em **Sim** para restaurar a revisão do aplicativo selecionado.  

### <a name="to-delete-an-application-revision"></a>Para excluir uma revisão do aplicativo  

1.  Na caixa de diálogo **Histórico de Revisão de Aplicativo** , selecione uma revisão do aplicativo e clique em **Excluir**.  

2.  Na caixa de diálogo **Excluir Revisão do Aplicativo** , clique em **Sim**.  

> [!IMPORTANT]  
>  Você só pode excluir a revisão atual do aplicativo se o aplicativo está desativado e não contém nenhuma referência.  

##  <a name="application-supersedence"></a>Substituição de aplicativos  
 O gerenciamento de aplicativos no Configuration Manager permite que você atualize ou substitua os aplicativos existentes usando uma relação de substituição. Ao substituir um aplicativo, é possível especificar um novo tipo de implantação para substituir o tipo de implantação do aplicativo substituído e também configurar para atualizar ou desinstalar o aplicativo substituído antes do aplicativo substituto ser instalado.  

> [!IMPORTANT]  
>  Ao selecionar a opção para desinstalar o tipo de implantação substituído, o tipo de implantação não pode ser substituído por um tipo de implantação que foi implantado em um tipo de coleção diferente.  Por exemplo, um tipo de implantação que foi feito em uma coleção de dispositivos não poderá ser substituído por outro tipo de implantação feito em uma coleção de usuários se a opção para desinstalar o tipo de implantação substituído estiver selecionada.  

### <a name="decide-whether-to-upgrade-or-replace-an-application"></a>Decida se deseja atualizar ou substituir um aplicativo  
 Especifique se deseja substituir ou atualizar um aplicativo na caixa de diálogo **Especificar Relação de Substituição** da caixa de diálogo Propriedades do aplicativo. O tipo de substituição dependerá se a opção **Desinstalar** estiver marcada nesta caixa de diálogo:  

-   Se desejar atualizar para uma versão mais recente do mesmo aplicativo (com a mesma ID de aplicativo), **não** marque **Desinstalar**.  

-   Se desejar alterar para um aplicativo diferente (com uma ID de aplicativo diferente), marque **Desinstalar**. Você precisará remover a versão substituída do aplicativo.  

### <a name="superseding-dependent-applications"></a>Substituindo aplicativos dependentes  
 Neste exemplo, **aplicativo mestre** refere-se ao aplicativo que está sendo implantado e que contém as dependências.  

 É possível criar uma relação de substituição que atualiza o aplicativo dependente para uma nova versão.  

1.  Verifique se o novo aplicativo dependente e o aplicativo dependente original estão no mesmo grupo de dependência do aplicativo mestre.  

2.  Crie uma relação de substituição que substitui o aplicativo dependente original pelo novo aplicativo dependente.  

 Durante novas instalações do aplicativo mestre, o novo aplicativo dependente será instalado. As instalações existentes do aplicativo mestre serão atualizadas com o novo aplicativo dependente.  

 O resultado final é que todas as implantações do aplicativo mestre usarão o novo aplicativo dependente.  

### <a name="further-considerations"></a>Considerações adicionais  

-   É possível especificar várias relações de substituição para aplicativos dependentes. O aplicativo dependente mais alto na cadeia de substituição é instalado.  

-   Os aplicativos dependentes devem ser implantados no dispositivo em que o aplicativo mestre está instalado, ou o aplicativo dependente não será instalado.  

-   Para novas instalações do aplicativo mestre, quando você tiver várias dependências, a ordem de dependência determina qual versão do aplicativo dependente será instalada.  

### <a name="specify-a-supersedence-relationship"></a>Especificar uma relação de substituição  

1.  No console do Configuration Manager, clique em **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos** e clique no aplicativo que substituirá outro.  

3.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades** para abrir a caixa de diálogo **Propriedades**.  

4.  Na guia **Substituição** da caixa de diálogo *<Nome de Aplicativo\>***Propriedades**, clique em **Adicionar**.  

5.  Na caixa de diálogo **Especifique a Relação de Substituição** , clique em **Procurar**.  

6.  Na caixa de diálogo **Escolher Aplicativo** , selecione o aplicativo que deseja substituir e clique em **OK**.  

7.  Na caixa de diálogo **Especifique a Relação de Substituição** , selecione o tipo de implantação que irá substituir o tipo de substituição do aplicativo substituído.  

    > [!NOTE]  
    >  Por padrão, o novo tipo de implantação não desinstala o tipo de implantação do aplicativo substituído. Esse cenário normalmente é usado quando você deseja implantar uma atualização para um aplicativo existente. Selecione **Desinstalar** para remover o tipo de implantação existente para poder instalar o novo tipo de implantação. Se você decidir atualizar um aplicativo, certifique-se de testar isso primeiramente em um ambiente de laboratório.  

8.  Clique em **OK** para fechar a caixa de diálogo **Especifique a Relação de Substituição** .  

9. Clique em **OK** para fechar a caixa de diálogo **Propriedades do***<Nome do Aplicativo\>*.  

### <a name="to-display-applications-that-supersede-the-current-application"></a>Para exibir os aplicativos que substituem o aplicativo atual  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Gerenciamento de Aplicativos**, clique em **Aplicativos**e clique no aplicativo desejado.  

3.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades** para abrir a caixa de diálogo *<Nome do Aplicativo\>***Propriedades**.  

4.  Na guia **Referências** da caixa de diálogo *<Nome do Aplicativo\>***Propriedades**, selecione **Aplicativos que substituem este aplicativo** na lista suspensa **Tipo de relacionamento**.  

5.  Examine a lista de aplicativos que substituem o aplicativo selecionado e clique em **OK** para fechar a caixa de diálogo *<Nome do Aplicativo\>***Propriedades**.  



<!--HONumber=Nov16_HO1-->


