---
title: Acessibilidade
titleSuffix: Configuration Manager
description: Saiba mais sobre os recursos que tornam o Configuration Manager acessível para todos.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1cb96666-98bf-49a9-85ca-dbb53f0655e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5a1bf32c77989c11c55723d5edf271e234ccd4ec
ms.sourcegitcommit: d8d142044586a53709b4478ad945f714737c8d6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58523734"
---
# <a name="accessibility-features-in-configuration-manager"></a>Recursos de acessibilidade no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


O Configuration Manager inclui recursos que ajudam a torná-lo acessível a todas as pessoas.

> [!Note]  
> A partir da versão 1902, para melhorar os recursos de acessibilidade do console do Configuration Manager, atualize o .NET para a versão 4.7 ou posterior no computador que executa o console. <!-- SCCMDocs-pr issue #3228 -->  
> 
> Para saber mais sobre as mudanças de acessibilidade realizadas no .NET 4.7.1 e 4.7.2, confira as [novidades de acessibilidade no .NET Framework](https://docs.microsoft.com/dotnet/framework/whats-new/whats-new-in-accessibility).  



## <a name="keyboard-shortcuts"></a>Atalhos de teclado

### <a name="console-workspaces"></a>Workspaces do console

Para acessar um workspace, use os seguintes atalhos de teclado:  

|Atalho de teclado| Workspace|
|--------|--------|  
|Ctrl + 1| Ativos e conformidade|
|Ctrl + 2|  Biblioteca de software|
|Ctrl + 3|  monitoramento|
|Ctrl + 4|  Administração|


### <a name="other-keyboard-shortcuts"></a>Outros atalhos de teclado

|Atalho de teclado|  Finalidade|
|--------|--------|  
|Ctrl + M|Define o foco no painel principal (central).|
|Ctrl + T|Define o foco o nó superior no painel de navegação. Se o foco já estiver nesse painel, ele será definido para o último nó que você visitou.|
|Ctrl + I|Define o foco para a barra de trilha, abaixo da faixa de opções.|
|Ctrl + L|Define o foco para o campo **Pesquisa**, quando estiver disponível.|
|Ctrl + D|Define o foco para o painel de detalhes, quando estiver disponível.|
|Alt     |Altera o foco para dentro e fora da faixa de opções.|



## <a name="other-accessibility-features"></a>Outros recursos de acessibilidade

- Para navegar no painel de navegação, digite as letras do nome de um nó.

- A navegação por teclado pelo modo de exibição principal e na faixa de opções é circular.

- A navegação pelo teclado no painel de detalhes é circular. Para retornar ao painel ou objeto anterior, use Ctrl + D, depois, Shift + TAB.

- Depois de atualizar um modo de exibição do Workspace, o foco é definido para o painel principal desse workspace.

- Para acessar um menu do workspace, pressione a tecla Tab até que o ícone Expandir/Recolher esteja em foco. Em seguida, pressione a tecla de seta para baixo para acessar o menu do workspace.  

- Para navegar por um menu de workspace, use as teclas de direção.  

- Para acessar diferentes áreas no workspace, use a tecla Tab e as teclas Shift+Tab. Para navegar dentro de uma área do workspace, como a faixa de opções, use as teclas de direção.  

- Para acessar a barra de endereços quando seu foco estiver no nó de árvore, use Shift+Tab três vezes.  

- Em uma página de assistente ou de propriedades, você pode se mover entre as caixas com os atalhos de teclado. Pressione a tecla Alt mais o caractere sublinhado (Alt+_) para selecionar uma caixa específica.     

- Para navegar até os diferentes nós de um workspace, insira a primeira letra do nome do nó. Cada pressionamento de tecla move o cursor para o próximo nó que começa com determinada letra. Quando você estiver usando um leitor de tela, o leitor lê o nome do nó.



## <a name="see-also"></a>Consulte também

Confira mais informações sobre os conceitos básicos de navegação nas interfaces de usuário do Configuration Manager nos seguintes artigos:
- [Usar o console do Configuration Manager](/sccm/core/servers/manage/admin-console)  
- [Guia do usuário do Centro de Software](/sccm/core/understand/software-center)

> [!NOTE]  
> As informações neste artigo podem se aplicar somente a usuários que licenciam produtos da Microsoft nos Estados Unidos. Se você adquiriu este produto fora dos Estados Unidos, pode usar o cartão de informações da subsidiária fornecido com o pacote do software ou acessar o [site de Acessibilidade da Microsoft](https://go.microsoft.com/fwlink/?LinkId=8431) para obter informações de contato dos serviços de suporte da Microsoft. Você pode contatar a subsidiária para descobrir se os tipos de produtos e serviços descritos nessa seção estão disponíveis na sua área. As informações sobre acessibilidade estão disponíveis em outros idiomas, incluindo japonês e francês.  

