---
title: Acessibilidade | Microsoft Docs
description: "Saiba mais sobre os recursos que tornam o System Center Configuration Manager acessível para pessoas com deficiências."
ms.custom: na
ms.date: 7/31/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1cb96666-98bf-49a9-85ca-dbb53f0655e9
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: ca518796477dda149a9f4c0ebd65f0a082eab806
ms.contentlocale: pt-br
ms.lasthandoff: 07/29/2017

---
# <a name="accessibility-features-in-system-center-configuration-manager"></a>Recursos de acessibilidade no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


O System Center Configuration Manager inclui recursos para ajudar a torná-lo acessível para pessoas com deficiências.


## <a name="bkmk_aconsole"></a> Recursos de acessibilidade para o console do Configuration Manager  

**Atalhos e aprimoramentos na versão 1706 e posterior**

|Atalho de teclado|  Finalidade|
|--------|--------|  
|Ctrl + M|Define o foco no painel principal (central).|
|Ctrl + T|Define o foco o nó superior no painel de navegação. Se o foco já estiver nesse painel, ele será definido para o último nó que você visitou.|
|Ctrl + I|Define o foco para a barra de trilha, abaixo da faixa de opções.|
|Ctrl + L|Define o foco para o campo **Pesquisa**, quando estiver disponível.|
|Ctrl + D|Define o foco para o painel de detalhes, quando estiver disponível.|
|Alt     |Altera o foco para dentro e fora da faixa de opções.|


- Melhora a navegação no painel de navegação quando você digita as letras de um nome de nó.
- A navegação por teclado no modo de exibição principal e na faixa de opções agora é circular.
- Agora, a navegação por teclado no painel de detalhes é circular. Para retornar ao painel ou objeto anterior, use Ctrl + D, depois, Shift + TAB.
- Depois de atualizar um modo de exibição do Espaço de Trabalho, o foco é definido para o painel principal desse espaço de trabalho.
- Correção de um problema para permitir que os leitores de tela anunciem os nomes dos itens de lista.
- Adição de nomes acessíveis para vários controles na página, o que permite aos leitores de tela anunciarem informações importantes.


**Os atalhos de teclado a seguir estão disponíveis para todas as versões**

- Para acessar um espaço de trabalho, use os seguintes atalhos de teclado:  

|Atalho de teclado| Espaço de trabalho|
|--------|--------|  
|Ctrl + 1| Ativos e conformidade|
|Ctrl + 2|  Biblioteca de software|
|Ctrl + 3|  monitoramento|
|Ctrl + 4|  Administração|


-   Para acessar um menu do espaço de trabalho, pressione a tecla Tab até que o ícone Expandir/Recolher esteja em foco. Em seguida, pressione a tecla de seta para baixo para acessar o menu do espaço de trabalho.  

-   Para navegar por um menu de espaço de trabalho, use as teclas de direção.  

-   Para acessar diferentes áreas no espaço de trabalho, use a tecla Tab e as teclas Shift+Tab. Para navegar dentro de uma área do espaço de trabalho, como a faixa de opções, use as teclas de direção.  

-   Para acessar a barra de endereços quando seu foco estiver no nó de árvore, use Shift+Tab três vezes.  

-   Em uma página de assistente ou de propriedades, você pode se mover entre as caixas com os atalhos de teclado. Pressione a tecla Alt mais o caractere sublinhado (Alt+_) para selecionar uma caixa específica.     

-  Para navegar até os diferentes nós de um espaço de trabalho, insira a primeira letra do nome do nó. Cada pressionamento de tecla move o cursor para o próximo nó que começa com determinada letra. Quando você estiver usando um leitor de tela, o leitor lê o nome do nó.

> [!NOTE]  
>  As informações nessa seção podem se aplicar somente a usuários que licenciam produtos da Microsoft nos Estados Unidos. Se você adquiriu este produto fora dos Estados Unidos, pode usar o cartão de informações da subsidiária fornecido com o pacote do software ou acessar o [site de Acessibilidade da Microsoft](http://go.microsoft.com/fwlink/?LinkId=8431) para obter informações de contato dos serviços de suporte da Microsoft. Você pode contatar a subsidiária para descobrir se os tipos de produtos e serviços descritos nessa seção estão disponíveis na sua área. As informações sobre acessibilidade estão disponíveis em outros idiomas, incluindo japonês e francês.  

##  <a name="bkmk_ahelp"></a> Recursos de acessibilidade para a Ajuda do Configuration Manager  
 A Ajuda do Configuration Manager inclui recursos que o tornam acessível a um maior número de usuários, incluindo aqueles que têm destreza limitada, visão subnormal ou outras deficiências.  

|Para fazer isso|Usar este atalho de teclado|  
|----------------|--------------------------------|  
|Exibir a janela da Ajuda.|F1|  
|Mover o cursor entre o painel do tópico da Ajuda e o painel de navegação (as guias **Conteúdo**, **Pesquisar**e **Índice** ).|F6|  
|Alterar entre as guias (por exemplo, **Conteúdo**, **Pesquisar** e **Índice**) enquanto estiver no painel de navegação.|Alt + letra sublinhada da guia|  
|Selecionar o próximo texto oculto ou hiperlink.|Guia|  
|Selecionar o texto oculto ou hiperlink anterior|Shift+Tab|  
|Executar a ação de Mostrar tudo, Ocultar tudo, Texto oculto ou hiperlink.|Entrar|  
|Exibir o menu **Opções** para acessar qualquer comando na barra de ferramentas da Ajuda.|Alt+O|  
|Ocultar ou mostrar o painel que contém as guias **Conteúdo**, **Pesquisar** e **Índices**.|Alt+O e depois pressione T|  
|Exibir o tópico visualizado anteriormente.|Alt+O e depois pressione B|  
|Exibir o próximo tópico em uma sequencia de tópicos exibidos anteriormente.|Alt+O e depois pressione F|  
|Retornar à página inicial especificada.|Alt+O e depois pressione H|  
|Impedir que a janela da Ajuda abra um tópico da Ajuda, como para interromper o download de uma página da Web.|Alt+O e depois pressione S|  
|Abrir a caixa de diálogo **Opções da Internet** no Internet Explorer, na qual é possível alterar as configurações de acessibilidade.|Alt+O e depois pressione I|  
|Atualizar o tópico, como uma página da Web vinculada.|Alt+O e depois pressione R|  
|Imprimir todos os tópicos em um livro ou apenas um tópico selecionado.|Alt+O e depois pressione P|  
|Fechar a janela da Ajuda.|Alt+F4|  

#### <a name="to-change-the-appearance-of-a-help-topic"></a>Para alterar a aparência de um tópico da Ajuda  

1.  Para se preparar para personalizar cores, estilos e tamanhos de fontes na Ajuda, abra a janela da Ajuda.  

2.  Clique em **Opções** e, em seguida, clique em **Opções da Internet**.  

3.  Na guia **Geral**, clique em **Acessibilidade**. Selecione **Ignorar cores especificadas em páginas da Web**, **Ignorar estilos de fonte especificados em páginas da Web** e **Ignorar tamanhos de fonte especificados em páginas da Web**. Você também pode optar por usar as configurações especificadas na sua própria folha de estilo.  

#### <a name="to-change-the-color-of-the-background-or-text-in-help"></a>Para alterar a cor do plano de fundo ou texto na Ajuda  

1.  Abra a janela da Ajuda.  

2.  Clique em **Opções** e, em seguida, clique em **Opções da Internet**.  

3.  Na guia **Geral**, clique em **Acessibilidade**. Em seguida, selecione **Ignorar cores especificadas em páginas da Web**. Você também pode optar por usar as configurações especificadas na sua própria folha de estilo.  

4.  Para personalizar as cores usadas na Ajuda, na guia **Geral**, clique em **Cores**. Desmarque a caixa de seleção **Usar cores do Windows** e selecione as cores de fonte e de plano de fundo que deseja usar.  

    > [!NOTE]  
    >  Se você alterar a cor de plano de fundo dos tópicos da Ajuda na janela da Ajuda, a alteração também afetará a cor de plano de fundo das páginas da Web no Internet Explorer.  

#### <a name="to-change-the-font-in-help"></a>Para alterar a fonte na Ajuda  

1.  Abra a janela da Ajuda.  

2.  Clique em **Opções** e, em seguida, clique em **Opções da Internet**.  

3.  Na guia **Geral**, clique em **Acessibilidade**. Para usar as mesmas configurações usadas em sua instância do Windows Internet Explorer, selecione **Ignorar estilos de fonte especificados em páginas da Web** e **Ignorar tamanhos de fonte especificados em páginas da Web**. Você também pode optar por usar as configurações especificadas na sua própria folha de estilo.  

4.  Para personalizar o estilo de fonte usado na Ajuda, na guia **Geral**, clique em **Fontes** e escolha o estilo de fonte desejado.  

    > [!NOTE]  
    >  Se você alterar a fonte dos tópicos da Ajuda na janela da Ajuda, a alteração também afetará a fonte das páginas da Web no Internet Explorer.  

