---
title: Terms and Conditions in System Center Configuration Manager
description: "Implante os termos e condições nos grupos de usuários no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d3f9e6b-4d71-4fc4-9b91-47f1bfbd8c70
caps.latest.revision: 9
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: a7b99bed3186ab8ff817ef5f420d7a55d60b1c14


---
# <a name="terms-and-conditions-in-system-center-configuration-manager"></a>Terms and Conditions in System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode implantar os termos e condições do System Center Configuration Manager em grupos de usuários para explicar como o registro do dispositivo, o acesso aos recursos de trabalho e o uso do Portal de Empresa afetam usuários e dispositivos. Os usuários devem aceitar estes termos e condições antes de poderem usar o Portal da Empresa para registrar e acessar o trabalho.  

 ## <a name="working-with-terms-and-conditions-policies-in-system-center-configuration-manager"></a>Trabalhando com políticas de termos e condições no System Center Configuration Manager  
 Você pode criar e implantar vários conjuntos de termos e condições. Você pode também gerar versões dos mesmos termos e condições em idiomas diferentes e, em seguida, implantá-las aos grupos apropriados.  

## <a name="to-create-a-terms-and-conditions"></a>Para criar os termos e condições  

1.  No console do Configuration Manager, acesse **Ativos e conformidade** > **Visão geral** > **Configurações de conformidade** > **Termos e condições**.  

2.  Clique em **Criar termos e condições** para criar novos termos e condições.  

3.  Na página **Geral** , especifique as seguintes informações:  

    -   **Nome** ‑ Um nome exclusivo exibido no console do Configuration Manager  

    -   **Descrição** ‑ Detalhes que ajudam a identificar os termos e condições no console do Configuration Manager  

     Em seguida, clique em **Avançar**.  

4.  Na página **Termos** , especifique as seguintes informações:  

    -   **Título** - O título exibido aos usuários do Portal da Empresa  

    -   **Texto para termos** - Os termos e condições exibidos aos usuários no Portal da empresa  

    -   **Texto para explicar o que significa se o usuário aceitar** - Usuários de rótulo veem de acordo com a aceitação. **Exemplo**: “Eu concordo com os termos e condições”.  

     Em seguida, clique em **Avançar**.  

5.  Conclua o assistente para criar novos termos e condições. Os novos termos e condições são exibidos no nó dos Termos e Condições do espaço de trabalho Ativos e Conformidade.  

## <a name="to-deploy-a-terms-and-conditions"></a>Para implantar os termos e condições  

1.  No console do Configuration Manager, acesse **Ativos e Conformidade** > **Visão geral** > **Configurações de Conformidade** > **Termos e Condições**.  

2.  Na lista **Termos e condições** , selecione o item que você deseja implantar e clique em **Implantar**.  

3.  **Navegue** para a **Coleção** que você deseja implantar os termos e condições e, em seguida, clique em **OK**.  

     Quando os dispositivos de destino acessam o aplicativo Portal da Empresa, ele exibe os termos e condições que você implantou. Os usuários devem aceitar esses termos antes de que possam obter acesso aos recursos da empresa.  

    > [!NOTE]  
    >  Se você implantar um conjunto de termos em várias coleções de usuários nas quais um usuário pertence, este usuário verá várias cópias dos termos idênticos ao abrir o Portal da empresa. Visto que os usuários só podem aceitar ou recusar todos os termos, não há nenhum risco de haver um estado de aceitação ambígua no qual o usuário tenha aceitado e rejeitado os termos ao mesmo tempo. O relatório de aceitação dos Termos e Condições incluirá apenas uma linha para cada conjunto de termos para cada usuário. Portanto, não há nenhum erro no relatório.  

## <a name="to-monitor-terms-and-conditions"></a>Para monitorar termos e condições  

1.  A partir da versão 1602, você pode monitorar as implantações de termos e condições no console do Configuration Manager. No console do Configuration Manager, acesse **Monitoramento** > **Visão Geral** > **Implantações**.  

2.  Selecione a implantação dos termos e condições na lista de implantações  

     A área de resumo mostrará as seguintes estatísticas:  

    -   **Compatível** – usuários que aceitaram a versão mais recente dos termos e condições  

    -   **Erro**  

    -   **Incompatível** – usuários que aceitaram uma versão dos termos e condições, mas não a versão mais recente  

    -   **Desconhecido** – usuários que nunca aceitaram os termos e condições, incluindo aqueles sem um dispositivo registrado  

3.  Escolha uma implantação dos termos e condições e selecione **Executar Resumo** para ver o Status da Implantação de usuários individuais.  

     Na tela Status da Implantação, você pode escolher as guias de status para exibir os usuários com esse status. Você pode clicar em **Executar Resumo** para atualizar os dados em toda a hierarquia. Clique em **Atualizar** para atualizar dados no console  

## <a name="to-view-a-terms-and-conditions-report"></a>Para exibir um relatório de termos e condições  

1.  No console do Configuration Manager, acesse **Monitoramento** > **Visão Geral** > **Relatórios** > **Relatório**.  

2.  Escolha **Aceitação dos termos e condições** e clique em **Executar**. O relatório de aceitação dos termos e condições é aberto. O relatório exibe cada usuário para quem os termos e condições foram implantados. Os campos incluem:  

    -   Nome dos termos e condições  

    -   Nome de usuário  

    -   Versão aceita  

    -   Data da aceitação  

    -   Aceitou o mais recente  

## <a name="updates-and-version-control-for-terms-and-conditions"></a>Atualizações e controle de versão dos termos e condições  
 Quando você editar os termos e condições existentes, você pode escolher o comportamento ao implantar os termos e condições. Use o procedimento a seguir para ajudar você a atualizar os termos e condições existentes.  

### <a name="how-to-work-with-multiple-versions-of-terms-and-conditions"></a>Como trabalhar com várias versões dos termos e condições  

1.  No console do Configuration Manager, acesse **Ativos e conformidade** > **Visão geral** > **Configurações de conformidade** > **Termos e condições**.  

2.  Selecione a instância de termos e condições que você deseja editar e clique duas vezes para abri-la.  

3.  Você pode modificar o conteúdo e fazer qualquer edição necessária na página **Geral** ou na página **Termos** .  

4.  Na página **Termos** , você pode, então, especificar se essa nova versão exige que todos os usuários aceitem os termos e condições, ou se somente os novos usuários verão a nova versão.  

     É recomendável aumentar o número de versão e exigir aceitação sempre que você fizer alterações significativas em seus termos e condições. Se você estiver corrigindo erros de digitação ou alterando a formatação, por exemplo, mantenha o número de versão atual.



<!--HONumber=Nov16_HO1-->


