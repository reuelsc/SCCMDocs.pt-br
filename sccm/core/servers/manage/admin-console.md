---
title: Console do Configuration Manager
titleSuffix: Configuration Manager
description: Saiba mais sobre como navegar por meio do console do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f936cf1c1317940f28691863eafdb4aa883fc1cb
ms.sourcegitcommit: aa91f0d376de03b614b70d5fc513cb384ff58db4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50216907"
---
# <a name="using-the-system-center-configuration-manager-console"></a>Uso do console do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os administradores usam o console do System Center Configuration Manager para gerenciar o ambiente do Configuration Manager. Este artigo aborda os conceitos básicos de navegação no console. Melhorias ao console são listadas por versão na parte inferior deste artigo. 

## <a name="connect-the-console-to-a-site-server"></a>Conectar o console a um servidor do site
O console conecta-se ao seu servidor do site de administração central ou aos seus servidores do site primário. Porém, não é possível conectar um console do Configuration Manager a um site secundário. Se necessário, [instale o console do Configuration Manager](../deploy/install/install-consoles.md). Durante a instalação, você especificou o FQDN (nome de domínio totalmente qualificado) do servidor do site ao qual o console do Configuration Manager se conecta. Para conectar-se a um servidor de site diferente, use as instruções a seguir: 

1. Clique na seta na parte superior da faixa de opções e selecione **Conectar-se a um Novo Site**.
    ![Conectar o console a um novo site](media/connect-to-a-new-site.png)
2. Digite o FQDN do servidor do site. Se você tiver se conectado anteriormente ao servidor do site, selecione o servidor na lista suspensa.  
    ![Digitar o FQDN do servidor do site](media/site-server-fqdn.png)
3. Clique em **Conectar**. 

## <a name="navigate-the-console"></a>Navegar no console
Algumas opções no console podem não estar visíveis, dependendo da sua função de segurança atribuída. Para obter mais informações sobre funções, veja [Fundamentos da administração baseada em funções](../../understand/fundamentals-of-role-based-administration.md). 

### <a name="workspaces"></a>Workspaces
O console do Configuration Manager tem quatro **workspaces**: 
   - **Ativos e Conformidade**
   - **Biblioteca de Software**
   - **Monitoramento**
   - **Administração**

 ![Workspaces do Configuration Manager](media/configuration-manager-workspaces.png)

Reordene os botões de workspace clicando na seta para baixo e selecionando **Opções do Painel de Navegação**. Selecione um item para **Mover para Cima** ou **Mover para Baixo**. Clique em **Redefinir** para restaurar a ordem de botões padrão. 

 ![Reordenar workspaces do Configuration Manager](media/navigation-pane-options.png)

Você pode minimizar um botão do workspace selecionando **Mostrar Menos Botões**. O último workspace na lista de workspaces é minimizado primeiro. Clicar em um botão minimizado e selecionar **Mostrar Mais Botões** restaura o botão ao seu tamanho original.  

![Workspaces do Configuration Manager](media/workspace-buttons.png)


### <a name="nodes"></a>Nós
Os workspaces são uma coleção de **nós**. Um exemplo de um nó é o nó **Grupos de Atualização de Software**. Quando você está em um nó, pode clicar na seta para minimizar o painel de navegação. 

![Workspaces do Configuration Manager](media/software-update-groups-node.png)

Você pode usar a **barra de navegação** para percorrer o console quando o painel de navegação é minimizado. 

![Painel de navegação minimizado do Configuration Manager](media/minimized-navigation-pane.png)

No console, os nós às vezes são organizados em pastas. Clicar diretamente na pasta geralmente o leva para um **índice de navegação** ou a um **painel**.

![O software Configuration Manager atualiza o índice de navegação](media/software-updates-navigation-index.png)

### <a name="ribbon"></a>Faixa de opções 
A faixa de opções fica na parte superior do console do Configuration Manager. A faixa de opções pode ter mais de uma guia e ser minimizada usando a seta à direita. Os botões na faixa de opções mudam conforme o nó. A maioria dos botões na faixa de opções também está disponível nos menus de clique com o botão direito do mouse. 
 
![O software Configuration Manager atualiza o índice de navegação](media/ribbon.png)

### <a name="details-pane"></a>Painel de detalhes
Você pode obter informações adicionais sobre itens examinando o painel de detalhes. O painel de detalhes pode ter uma ou mais guias. As guias vão variar conforme o nó. 
![Painel de detalhes do Configuration Manager](media/details-pane.png)

### <a name="columns"></a>Colunas 
Você pode adicionar, remover, reorganizar e redimensionar colunas. Essas ações permitem que você exiba os dados que preferir. As colunas disponíveis vão variar conforme o nó. Clique com o botão direito do mouse em um título de coluna existente e, em seguida, clique em um item a adicionar ou remover da exibição. Reordene as colunas arrastando o título de coluna para o local em que deseja posicioná-lo. 
![Coluna adicionar do Configuration Manager](media/add-columns.png)

Na parte inferior do menu de clique com o botão direito do mouse da coluna, você pode classificar ou agrupar por uma coluna. Além disso, pode classificar por uma coluna clicando em seu cabeçalho. 

![O Configuration Manager agrupa por coluna](media/column-group-by.png)

##<a name="console-command-line-options"></a>Opções de linha de comando do console
O console do Microsoft System Center Configuration Manager tem as seguintes opções de linha de comando.

|Opção|Descrição|  
|------------|-----------------|  
|**/sms:debugview=1**|Um DebugView está incluído em todos os ResultViews que especificam uma exibição. O DebugView mostra as propriedades brutas (nomes e valores).|  
|**/sms:NamespaceView=1**|Mostra a exibição de namespace no console do System Center Configuration Manager.|  
|**/sms:ResetSettings**|O console do System Center Configuration Manager ignora a conexão persistente do usuário e exibe os estados (o tamanho da janela do Console de Gerenciamento Microsoft não é redefinido).|  
|**/sms:IgnoreExtensions**|Desabilita quaisquer extensões do System Center Configuration Manager.|  
|**/sms:NoRestore**|O console do System Center Configuration Manager ignora a navegação de nó persistente anterior.|  

## <a name="console-improvements-in-version-1806"></a>Melhorias do console na versão 1806
No Configuration Manager versão 1806, as seguintes melhorias do console foram adicionadas:

- **Usuários primários** estão disponíveis como uma coluna no nó do dispositivo. <!--1357280-->
- **Usuário conectado no momento** está disponível como uma coluna no nó do dispositivo.<!--1358202-->
- Copiar as informações do painel **Detalhes do Ativo** para as seguintes exibições de monitoramento: <!--1357856-->
    - Status da Distribuição de Conteúdo
    - Status de Implantação 

    ![Detalhes do ativo de cópia do Configuration Manager](media/1810-deployment-status.PNG)

 - Envie comentários do console. Você poderá salvar uma cópia para enviar mais tarde se você não tiver acesso à Internet. <!--1357542-->
   
    - **Enviar um Smiley**: envie comentários sobre o que você gostou.
    - **Enviar um rosto triste**: envie comentários sobre o que você não gostou. 
    - **Enviar uma sugestão**: leva você ao UserVoice para compartilhar sua ideia. 
 
       ![Enviar comentários para o Configuration Manager](media/1810-send-a-smile.PNG)
![Formulário de comentários do Configuration Manager](media/1810-feedback-form.PNG)

## <a name="next-steps"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Recursos de Acessibilidade](../../understand/accessibility-features.md)

