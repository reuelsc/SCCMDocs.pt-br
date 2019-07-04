---
title: Console do Configuration Manager
titleSuffix: Configuration Manager
description: Saiba mais sobre como navegar por meio do console do Configuration Manager.
ms.date: 06/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3fc9e6fad0b7be3762b3d642c94c4cf17266e0b3
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67285746"
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

## <a name="bkmk_viewconnected"></a> Exibir consoles conectados recentemente
<!--3699367-->

Começando na versão 1902, você pode exibir as conexões mais recentes do console do Configuration Manager. O modo de exibição inclui conexões ativas e aqueles que se conectaram recentemente. Você sempre verá sua conexão de console atual na lista e verá apenas as conexões do console do Configuration Manager. Você não verá o PowerShell nem outras conexões baseadas em SDK com o Provedor de SMS. O site remove da lista as instâncias com mais de 30 dias.


### <a name="prerequisites-to-view-connected-consoles"></a>Pré-requisitos para exibir os consoles conectados

- Sua conta precisa da permissão **Leitura** no objeto **SMS_Site** 
- O IIS precisa ser instalado no servidor do Provedor de SMS <!---SCCMDocs-pr issue 1326--> 
- Habilite o Provedor de SMS para usar um certificado.<!--SCCMDocs-pr issue 3135--> Use uma das seguintes opções:  

  - Habilitar [HTTP aprimorado](/sccm/core/plan-design/hierarchy/enhanced-http) (recomendado)
  - Associar manualmente um certificado baseado em PKI à porta 443 no IIS no servidor que hospeda a função de Provedor de SMS  

### <a name="view-connected-consoles"></a>Exibir consoles conectados

1. No console do Configuration Manager, acesse o workspace **Administração**.  

2. Expanda **Segurança** e selecione o nó **Conexões do console**.  

3. Exiba as conexões recentes, com as seguintes propriedades:  

    - Nome de usuário
    - Nome do computador
    - Código do site conectado
    - Versão do console
    - Horário da última conexão: Quando o usuário *abriu* o console pela última vez

![Exibir as conexões de console do Configuration Manager](media/console-connections.png) 


## <a name="bkmk_notify"></a> Notificações do console do Configuration Manager
<!--3556016, fka 1318035-->
A partir do Configuration Manager versão 1902, o console notifica você para os seguintes eventos:

- Quando uma atualização está disponível para o Configuration Manager em si
- Quando ocorrem eventos de ciclo de vida e manutenção no ambiente

Essa notificação é uma barra na parte superior da janela do console abaixo da faixa de opções. Ela substitui a experiência anterior quando atualizações do Configuration Manager estão disponíveis. Essas notificações no console ainda exibem informações críticas, mas não interferem no trabalho no console. Você não pode descartar notificações críticas. O console exibe todas as notificações em uma nova área de notificação da barra de título.

![Barra de notificação e sinalizador no console](./media/1318035-notify-eval-version-expired.png)

### <a name="configure-a-site-to-show-non-critical-notifications"></a>Configurar um site para mostrar notificações não críticas

Você pode configurar cada site para mostrar notificações não críticas nas propriedades do site.

1.  No espaço de trabalho **Administração**, expanda **Configuração do Site** e clique no nó **Sites**.
1. Selecione o site que você deseja configurar para notificações não críticas.
1. Na faixa de opções, clique em **Propriedades**.
1. Na guia **Alertas**, selecione a opção para **Habilitar notificações de console para alterações de integridade do site não críticas**.
   - Se você habilitar essa configuração, todos os usuários do console verão notificações críticas, de aviso e de informações. Essa configuração é habilitada por padrão.  
   - Se você desabilitar essa configuração, os usuários do console verão apenas notificações críticas.  

A maioria das notificações de console é por sessão. O console avalia consultas quando um usuário o inicia. Para ver as alterações nas notificações, reinicie o console. Se um usuário descartar uma notificação não crítica, ele será notificado novamente quando o console for reiniciado, se ainda for aplicável.

As seguintes notificações são reavaliadas a cada cinco minutos:
- O site está no modo de manutenção  
- O site está no modo de recuperação  
- O site está no modo de atualização  

As notificações seguem as permissões de administração baseada em funções. Por exemplo, se um usuário não tiver permissões para ver as atualizações do Configuration Manager, ele não verá essas notificações.

Algumas notificações têm uma ação relacionada. Por exemplo, se a versão do console não corresponder à versão do site, selecione **Instalar a nova versão do console**. Essa ação inicializa o instalador do console. 

As seguintes notificações são mais aplicáveis ao branch de visualização técnica:  

- A versão de avaliação está dentro de 30 dias de término (Aviso): a data atual está dentro de 30 dias após a data do término da versão de avaliação  
- A versão de avaliação expirou (Crítica): a data atual é posterior à data do término da versão de avaliação  
- Incompatibilidade de versão do console (Crítica): a versão do console não corresponde à versão do site  
- Há uma atualização do site disponível (Aviso): há um novo pacote de atualização disponível  

Para obter mais informações e assistência na solução de problemas, confira o arquivo **SmsAdminUI.log** no computador do console. Por padrão, esse arquivo de log está no seguinte caminho: `C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\AdminUILog\SmsAdminUI.log`.

## <a name="bkmk_doc-dashboard"></a> Painel de documentação no console
<!--3556019 FKA 1357546-->

A partir do Configuration Manager versão 1902, há um nó **Documentação** no novo espaço de trabalho **Comunidade**. Esse nó inclui informações atualizadas sobre a documentação e os artigos de suporte do Configuration Manager. Ele inclui as seguintes seções:  

### <a name="product-documentation-library"></a>Biblioteca de documentação do produto

- **Recomendado**: uma lista de artigos importantes coletada manualmente.
- **Tendências**: os artigos mais populares do último mês.
- **Atualizados recentemente**: artigos revisados no último mês.

### <a name="support-articles"></a>Artigos de suporte

- **Artigos de solução de problemas**: orientações passo a passo para ajudar na solução de problemas de componentes e recursos do Configuration Manager.
- **Artigos de suporte novos e atualizados**: artigos de suporte que são novos ou foram atualizados nos últimos dois meses.


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

### <a name="search-device-views-using-mac-address"></a>Pesquisar exibições de dispositivo usando o endereço MAC
<!--3600878-->
*(Apresentado na versão 1902)*

Você pode pesquisar um endereço MAC em uma exibição de dispositivo do console do Configuration Manager. Essa propriedade é útil para os administradores de implantação do sistema operacional durante a solução de problemas de implantações baseadas no PXE. Ao exibir uma lista de dispositivos, adicione a coluna **Endereço MAC** à exibição. Use o campo de pesquisa para adicionar os critérios de pesquisa de **Endereço MAC**.

### <a name="maximize-the-browse-registry-window"></a>Maximizar a janela Procurar Registro
<!--3594151 includes all MMS 1902 console changes-->
*(Apresentado na versão 1902)*
1. No workspace **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e selecione o nó **Aplicativos**. 
1. Selecione um aplicativo que tenha um tipo de implantação com um método de detecção. Por exemplo, um método de detecção do Windows Installer. 
1. No painel de detalhes, mude para a guia **Tipos de Implantação**. 
1. Abra as propriedades de um tipo de implantação e alterne para a guia **Método de Detecção**. Selecione **Adicionar Cláusula**. 
1. Altere o **Tipo de Configuração** para **Registro** e selecione **Procurar** para abrir a janela **Procurar Registro**. Agora você pode maximizar essa janela.  

### <a name="go-to-the-collection-from-an-application-deployment"></a>Ir para a coleção de uma implantação de aplicativo

*(Apresentado na versão 1902)*
1. No workspace **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e selecione o nó **Aplicativos**. 
1. Selecione um aplicativo. No painel de detalhes, mude para a guia **Implantações**.
1. Selecione uma implantação e, em seguida, escolha a nova opção **Coleção** na faixa de opções na guia Implantação. Essa ação alterna a exibição para a coleção que é o destino da implantação.
   - Essa ação também está disponível no menu de contexto do botão direito do mouse na implantação nesta exibição.

### <a name="edit-a-task-sequence-by-default"></a>Editar uma sequência de tarefas por padrão

*(Apresentado na versão 1902)*

No workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione o nó **Sequências de Tarefas**. **Editar** agora é a ação padrão ao abrir uma sequência de tarefas. Antes, a ação padrão era **Propriedades**.  

### <a name="remove-content-from-monitoring-status"></a>Remover o conteúdo do status de monitoramento
*(Apresentado na versão 1902)*

1. No workspace **Monitoramento**, expanda **Status da Distribuição** e selecione **Status do Conteúdo**.
1. Selecione um item na lista e escolha a opção **Status de Exibição** na faixa de opções. 
1. No painel de Detalhes do Ativo, clique com o botão direito do mouse em um ponto de distribuição e selecione a nova opção **Remover**. Esta ação remove esse conteúdo do ponto de distribuição selecionado.

### <a name="views-sort-by-integer-values"></a>Classificação de exibições por valores inteiros
*(Apresentado na versão 1902)*

Fizemos melhorias no modo de como vários modos de exibição classificam dados. Por exemplo, no nó **Implantações** do workspace de **Monitoramento**, as seguintes colunas agora são classificados como números em vez de valores de cadeia de caracteres:  

- Erros de Número
- Número em Progresso
- Outro Número
- Êxito de Número
- Número Desconhecido  

### <a name="move-the-warning-for-a-large-number-of-results"></a>Mover o aviso para um grande número de resultados
*(Apresentado na versão 1902)*

Quando você seleciona um nó no console que retorna mais de 1.000 resultados, o Configuration Manager exibe o seguinte aviso:

> O Configuration Manager retornou um grande número de resultados. Você pode restringir os resultados usando a pesquisa. Ou clique aqui para exibir um máximo de 100 mil resultados.
 
Agora há espaço em branco adicional entre esse aviso e o campo de pesquisa. Essa mudança ajuda a evitar que o aviso para exibir mais resultados seja selecionado inadvertidamente. 



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

- **Usuário conectado no momento** <!--1358202-->  
    > [!NOTE]  
    > Exibir o usuário conectado no momento exige [descoberta de usuário](/sccm/core/servers/deploy/configure/configure-discovery-methods#bkmk_config-adud) e [afinidade de dispositivo de usuário](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  

Para obter mais informações sobre como mostrar uma coluna não padrão, confira [Colunas](#columns).

#### <a name="improvement-to-device-search-performance"></a>Melhoria de desempenho da Pesquisa de Dispositivos
<!-- 3614690 -->
Começando na versão 1806, ao pesquisar em uma coleção de dispositivos, o recurso não pesquisa a palavra-chave em relação a todas as propriedades do objeto. Quando você não especifica o conteúdo que deseja pesquisar, o mecanismo pesquisa as quatro propriedades a seguir:
- Name
- Usuários primários
- Usuário conectado no momento
- Nome de Usuário do Último Logon

Este comportamento melhora significativamente o tempo necessário para pesquisar por nome, principalmente em um ambiente grande. Esta alteração não afeta as pesquisas personalizadas por critérios específicos. 


### <a name="monitoring-workspace"></a>Workspace de monitoramento

#### <a name="copy-details-in-monitoring-views"></a>Copiar detalhes em exibições de monitoramento
<!--1357856-->
Começando na versão 1806, copie informações do painel **Detalhes do Ativo** para os seguintes nós de monitoramento:  

- **Status da Distribuição de Conteúdo**  

- **Status da implantação**  

![Exibição de Status de Implantação, copiar detalhes do ativo](media/1810-deployment-status.PNG)



## <a name="next-steps"></a>Próximas etapas

[Recursos de acessibilidade](/sccm/core/understand/accessibility-features)

