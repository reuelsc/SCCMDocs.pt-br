---
title: Console do Configuration Manager
titleSuffix: Configuration Manager
description: Saiba mais sobre como navegar por meio do console do Configuration Manager.
ms.date: 2/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 30db8b061f41e8a9255b5a308df6a98ef8c0d81b
ms.sourcegitcommit: 369db96ee84299b5ab6d74b177e6366b3017fc54
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2019
ms.locfileid: "56589893"
---
# <a name="using-the-configuration-manager-console"></a>Usando o console do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os administradores usam o console do Configuration Manager para gerenciar o ambiente do Configuration Manager. Este artigo aborda os conceitos básicos de navegação no console.  



## <a name="connect-to-a-site-server"></a>Conectar a um servidor do site

O console conecta-se ao seu servidor do site de administração central ou aos seus servidores do site primário. Não é possível conectar um console do Configuration Manager a um site secundário. Você pode [instalar o console do Configuration Manager](/sccm/core/servers/deploy/install/install-consoles). Durante a instalação, você especificou o FQDN (nome de domínio totalmente qualificado) do servidor do site ao qual o console se conecta. 

Para conectar-se a um servidor de site diferente, use as etapas a seguir: 

1. Selecione a seta na parte superior da [faixa de opções](#ribbon) e escolha Conectar-se a um **Novo Site**.  

    ![Conectar o console a um novo site](media/connect-to-a-new-site.png)  

2. Digite o FQDN do servidor do site. Se você tiver se conectado anteriormente ao servidor do site, selecione o servidor na lista suspensa.  

    ![Janela de Conexão do Site, digite o FQDN do servidor do site](media/site-server-fqdn.png)  

3. Selecione **Conectar**.  


Da versão 1810 em diante, você pode especificar o nível mínimo de autenticação para os administradores acessarem sites do Configuration Manager. Esse recurso faz com que os administradores entrem no Windows com o nível necessário. Para obter mais informações, veja [Planejar para o provedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth). <!--1357013-->  



## <a name="navigation"></a>Navegação

Algumas áreas do console podem não estar visíveis, dependendo da função de segurança atribuída. Para obter mais informações sobre funções, veja [Fundamentos da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration). 


### <a name="workspaces"></a>Workspaces

O console do Configuration Manager tem quatro **workspaces**:  

- **Ativos e Conformidade**  

- **Biblioteca de Software**  

- **Monitoramento**  

- **Administração**  

![Workspaces do Configuration Manager com o menu de contexto](media/configuration-manager-workspaces.png)  

Reordene os botões de workspace selecionando a seta para baixo e escolhendo **Opções do Painel de Navegação**. Selecione um item para **Mover para Cima** ou **Mover para Baixo**. Selecione **Redefinir** para restaurar a ordem de botões padrão.  

 ![Janela de Opções do Painel de Navegação para reordenar os workspaces](media/navigation-pane-options.png)  

Minimize um botão do workspace selecionando **Mostrar Menos Botões**. O último workspace na lista é minimizado primeiro. Selecione um botão minimizado e escolha **Mostrar Mais Botões** para restaurar o botão ao seu tamanho original.   

![Workspaces minimizados no console do Configuration Manager](media/workspace-buttons.png)  


### <a name="nodes"></a>Nós

Os workspaces são uma coleção de **nós**. Um exemplo de um nó é o nó **Grupos de Atualização de Software** no workspace da **Biblioteca de Software**. 

Quando você está em um nó, pode selecionar a seta para minimizar o painel de navegação.  

![Exemplo de nó e realce da seta para minimizar](media/software-update-groups-node.png)  

Use a **barra de navegação** para percorrer o console ao minimizar o painel de navegação.  

![Painel de navegação minimizado do Configuration Manager](media/minimized-navigation-pane.png)  

No console, os nós às vezes são organizados em pastas. Clicar diretamente na pasta geralmente o leva para um **índice de navegação** ou a um **painel**.  

![O software Configuration Manager atualiza o índice de navegação](media/software-updates-navigation-index.png)  


### <a name="ribbon"></a>Faixa de opções 

A faixa de opções fica na parte superior do console do Configuration Manager. A faixa de opções pode ter mais de uma guia e ser minimizada usando a seta à direita. Os botões na faixa de opções mudam conforme o nó. A maioria dos botões na faixa de opções também está disponível nos menus de contexto.  

![Faixa de opções de exemplo, realçando várias guias e seta para minimizar](media/ribbon.png)   


### <a name="details-pane"></a>Painel de detalhes

Você pode obter informações adicionais sobre itens examinando o painel de detalhes. O painel de detalhes pode ter uma ou mais guias. As guias variam conforme o nó.  

![Painel de detalhes de exemplo do Configuration Manager](media/details-pane.png)   


### <a name="columns"></a>Colunas 

Você pode adicionar, remover, reorganizar e redimensionar colunas. Essas ações permitem que você exiba os dados que preferir. As colunas disponíveis variam conforme o nó. Para adicionar ou remover uma coluna do modo de exibição, clique com o botão direito do mouse em um título de coluna existente e selecione um item. Reordene as colunas arrastando o título de coluna para o local em que deseja posicioná-lo.  

![Coluna adicionar do Configuration Manager](media/add-columns.png)  

Na parte inferior do menu de contexto da coluna, você pode classificar ou agrupar por uma coluna. Além disso, você pode classificar por uma coluna selecionando seu cabeçalho.  

![O Configuration Manager agrupa por coluna](media/column-group-by.png)  



## <a name="command-line-options"></a>Opções de linha de comando

O console do Configuration Manager tem as seguintes opções de linha de comando:

|Opção|Descrição|  
|------------|-----------------|  
|`/sms:debugview=1`|Um DebugView está incluído em todos os ResultViews que especificam uma exibição. O DebugView mostra as propriedades brutas (nomes e valores).|  
|`/sms:NamespaceView=1`|Mostra a exibição de namespace no console.|  
|`/sms:ResetSettings`|O console ignora os estados de exibição e conexão persistente do usuário. O tamanho da janela não é redefinido.|  
|`/sms:IgnoreExtensions`|Desabilita quaisquer extensões do Configuration Manager.|  
|`/sms:NoRestore`|O console ignora a navegação em nó persistente anterior.|  



## <a name="tips"></a>Dicas

### <a name="send-feedback"></a>Enviar comentários
<!--1357542-->

Na versão 1806, envie comentários sobre o produto do console.  

- **Enviar um sorriso**: Enviar comentários sobre o que você gostou  

- **Enviar um rosto triste**: Enviar comentários sobre o que você não gostou  

- **Enviar uma sugestão**: Leva você ao UserVoice para compartilhar sua ideia  
 
Para obter mais informações, confira [Comentários sobre o Produto](/sccm/core/understand/find-help#BKMK_1806Feedback).


### <a name="assets-and-compliance-workspace"></a>Workspace Ativos e Conformidade

#### <a name="view-users-for-a-device"></a>Exibir usuários para um dispositivo
Da versão 1806 em diante, as colunas a seguir estão disponíveis no nó **Dispositivos**:  

- **Usuários primários** <!--1357280-->  

- **Usuário conectado atualmente** <!--1358202-->  
    > [!NOTE]  
    > Exibir o usuário conectado no momento exige [descoberta de usuário](/sccm/core/servers/deploy/configure/configure-discovery-methods#bkmk_config-adud) e [afinidade de dispositivo de usuário](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  

Para obter mais informações sobre como mostrar uma coluna não padrão, confira [Colunas](#columns).


### <a name="monitoring-workspace"></a>Workspace de monitoramento

#### <a name="copy-details-in-monitoring-views"></a>Copiar detalhes em exibições de monitoramento
<!--1357856--> Começando na versão 1806, copie informações do painel **Detalhes do Ativo** para os seguintes nós de monitoramento:  

- **Status da Distribuição de Conteúdo**  

- **Status da implantação**  

![Exibição de Status de Implantação, copiar detalhes do ativo](media/1810-deployment-status.PNG)



## <a name="next-steps"></a>Próximas etapas

[Recursos de acessibilidade](/sccm/core/understand/accessibility-features)

