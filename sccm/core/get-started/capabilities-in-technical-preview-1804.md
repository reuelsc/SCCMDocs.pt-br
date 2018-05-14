---
title: Technical Preview 1804
titleSuffix: Configuration Manager
description: Saiba mais sobre os novos recursos disponíveis no Technical Preview do Configuration Manager versão 1804.
ms.date: 04/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8af43618-ec60-4c3e-a007-12399d1335b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0fcdcc984e267e6c54ad7c6194e8494854f0a1ee
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="capabilities-in-technical-preview-1804-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1804 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do Configuration Manager, versão 1804. Você pode instalar esta versão para atualizar e adicionar novos recursos ao seu site do Technical Preview. 

Examine o artigo de [Technical Preview](/sccm/core/get-started/technical-preview) antes de instalar essa atualização. Este artigo familiariza você com os requisitos gerais e as limitações do uso de um technical preview, como atualizar entre versões e como fornecer comentários.     


<!--  Known Issues Template   -->
## <a name="known-issues-in-this-technical-preview"></a>Problemas conhecidos neste Technical Preview

### <a name="bkmk_appcathttps"></a> O ponto de serviço Web do catálogo de aplicativos não pode ser habilitado para HTTPS
<!--512637-->
Se o ponto de serviço Web do catálogo de aplicativos for habilitado para HTTPS:

- Os aplicativos implantados como disponíveis para os usuários não aparecem no Centro de Software  

- O erro a seguir aparece no awebsctl.log:  

     `Call to HttpSendRequestSync failed for port 443 with status code 500, text: Internal Server Error`

#### <a name="workaround"></a>Solução alternativa
Reconfigure o ponto de serviço Web do catálogo de aplicativo para se comunicar usando conexões HTTP.  




</br>

**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  


## <a name="configure-a-remote-content-library-for-the-site-server"></a>Configurar uma biblioteca de conteúdo remoto para o servidor do site  
<!--1357525-->
Para liberar espaço no disco rígido do seu servidor do site primário, realoque sua [biblioteca de conteúdo](/sccm/core/plan-design/hierarchy/the-content-library) para outra localização de armazenamento. Você pode mover a biblioteca de conteúdo para outra unidade no servidor do site, para um servidor separado ou para discos tolerantes a falhas em uma rede SAN (rede de área de armazenamento). Recomendamos uma rede SAN porque ela fornece armazenamento elástico que aumenta ou diminui ao longo do tempo, a fim de atender às necessidades dinâmicas de conteúdo. 

Essa biblioteca de conteúdo remoto é um novo pré-requisito para [alta disponibilidade da função de servidor do site](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability). 

> [!Note]  
> Essa ação só move a biblioteca de conteúdo no servidor do site. Ela não afeta a localização da biblioteca de conteúdo nos pontos de distribuição. 

### <a name="prerequisites"></a>Pré-requisitos  
- A conta do computador do servidor do site precisa de permissões de **leitura** e **gravação** para o caminho de rede ao qual você está movendo a biblioteca de conteúdo. Nenhum dos componentes são instalados no sistema remoto. 

### <a name="try-it-out"></a>Experimente!
 Tente concluir as tarefas. Depois, envie seus [comentários](#bkmk_feedback) sobre como isso funcionou.

1. No console do Configuration Manager, alterne para o espaço de trabalho **Administração**. Expanda a **Configuração do site** e selecione **Sites**. Na guia **Resumo** na parte inferior do painel de detalhes, observe uma nova coluna para a **Biblioteca de Conteúdo**.  

2. Clique em **Gerenciar biblioteca de conteúdo** na faixa de opções.  

3. Selecione **Em um compartilhamento de rede** e insira um caminho de rede válido. Esse caminho é a localização para o qual o site move a biblioteca de conteúdo. Clique em **OK**.  

4. Observe a propriedade **Status** na coluna Biblioteca de Conteúdo no painel de detalhes. Ela é atualizada para mostrar o progresso da transferência da biblioteca de conteúdo. Durante a transferência, ela exibe a porcentagem concluída. Se houver um estado de erro, ela exibirá o erro. Os erros comuns incluem `access denied` ou `disk full`. Após a conclusão, ela mostra `OK`. Consulte o **distmgr.log** para obter detalhes. Para saber mais, confira [Logs do servidor do site e do sistema de sites](/sccm/core/plan-design/hierarchy/log-files#BKMK_SiteSiteServerLog).  

Se você precisar mover a biblioteca de conteúdo de volta ao servidor do site, repita esse processo, mas selecione a opção **Local para o servidor do site**.  

> [!Tip]  
> Para mover o conteúdo para outra unidade no servidor do site, use a ferramenta **Transferência da Biblioteca de Conteúdo**. Para saber mais, confira [Kit de ferramentas do Configuration Manager](#configuration-manager-toolkit).  



## <a name="bkmk_feedback"></a> Enviar comentários do console do Configuration Manager  
<!--1357542-->

Mande um sorriso! Agora, você pode informar diretamente a equipe do Configuration Manager sobre suas experiências. Enviar comentários do console do Configuration Manager é muito fácil. Queremos ouvir todos os seus comentários: elogios, problemas e sugestões.  

### <a name="try-it-out"></a>Experimente!
 Tente concluir as tarefas. Depois, envie seus **comentários** sobre como isso funcionou.  

1. No console do Configuration Manager, clique no botão de sorriso no canto superior direito, acima da faixa de opções.  

2. Na lista suspensa, selecione uma das opções disponíveis:  

   - **Enviar um sorriso**: você realmente gostou de algo! Para essa opção, insira os detalhes do seu comentário. Se quiser, inclua uma captura de tela e seu endereço de email.  

   - **Enviar um rosto triste**: você encontrou um problema no console ou algo que não funcionou como o esperado. Para essa opção, insira os detalhes do possível problema do produto. Se quiser, inclua uma captura de tela, seu endereço de email e dados de diagnóstico.  

   - **Enviar uma sugestão**: você tem uma ideia para mudar e melhorar o Configuration Manager. Essa opção abre o nosso site [UserVoice](https://configurationmanager.uservoice.com) em seu navegador da Web.  

Esse comentário vai diretamente para a equipe de produtos da Microsoft do Configuration Manager. Apesar de o Hub de Comentários do Windows 10 ainda ter suporte, incentivamos o uso do mecanismo de comentários no console.  

As seguintes informações anônimas são sempre incluídas com os comentários para proporcionar o contexto:  

 - Versão e idioma do console do Configuration Manager  

 - Versão do site do Configuration Manager  

 - ID de suporte, também conhecida como ID da hierarquia  

 - A versão e o idioma do sistema operacional sistema no qual o console está sendo executado  

 - A localização exata no console de onde você clicou no sorriso  

Esses dados são consistentes com a coleção de nossos dados de diagnóstico e de uso. Para obter mais informações, consulte [Dados de diagnóstico e de uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).

### <a name="known-issues"></a>Problemas conhecidos

Se você tentar enviar comentários de um dispositivo que não é capaz de acessar a internet, o aplicativo poderá fechar inesperadamente. Para enviar um sorriso ou rosto triste, verifique se o dispositivo é capaz de acessar petrol.office.microsoft.com.



## <a name="support-center"></a>Centro de Suporte
<!--1357489-->

Use o Centro de Suporte para solução de problemas do cliente, exibição de log em tempo real ou captura do estado de um computador de cliente do Configuration Manager para análise posterior. O Centro de Suporte é uma ferramenta única para consolidação das diversas ferramentas de solução de problemas do administrador. Há uma versão prévia do Centro de Suporte mais recente, contendo correções de bug, melhorias e prévia do nosso novo visualizador de logs, na visualização técnica. Localize o instalador do Centro de Suporte no servidor do site na pasta **cd.latest\SMSSETUP\Tools\SupportCenter**.

 > [!Tip]  
 > Encontre a documentação herdada da funcionalidade existente do Centro de Suporte no [TechNet](https://technet.microsoft.com/library/dn688621.aspx). A migração de informações relevantes para a biblioteca docs.microsoft.com está em andamento.  

### <a name="new-support-center-features"></a>Novos recursos do Centro de Suporte  

 - Um novo visualizador de log, OneTrace. Ele funciona de modo semelhante ao CMTrace e inclui melhorias, como uma exibição com guias e janelas encaixáveis.  

 - Um novo recurso coletor de dados reúne logs de diagnóstico de um cliente do Configuration Manager local ou remoto. Ele fornece o diagnóstico em tempo real do inventário (substitui o Client Spy), da política (substitui o Policy Spy) e do cache do cliente.  



## <a name="configuration-manager-toolkit"></a>Kit de ferramentas do Configuration Manager
<!--1357145-->

Agora, as ferramentas de servidor e cliente do Configuration Manager estão incluídos com a visualização técnica. Encontre-as na pasta **\cd.latest\SMSSETUP\TOOLS** do servidor do site. Nenhuma instalação adicional é necessária.

#### <a name="server-tools"></a>Ferramentas de servidor  

 - **DP Job Manager**: soluciona problemas de trabalhos de distribuição de conteúdo para os pontos de distribuição  

 - **Collection Evaluation Viewer**: exiba detalhes de avaliação da coleta  

 - **Content Library Explorer**: exiba o conteúdo do repositório de instância única da biblioteca de conteúdo  

 - **Content Library Transfer**: transfere a biblioteca de conteúdo entre unidades  

 - **Content Ownership Tool**: altera a propriedade de pacotes órfãos. Esses pacotes existem no site sem um servidor de site proprietário.  

 - **Role-based Administration and Auditing Tool**: ajuda os administradores a realizar a auditoria de funções de configuração  

#### <a name="client-tools"></a>Ferramentas de cliente

 - **CMTrace**: exiba logs  

 - **Deployment Monitoring Tool**: solucione problemas de aplicativos, atualizações e implantações da linha de base  

 - **Policy Spy**: exiba as atribuições de políticas  

 - **Power Viewer Tool**: exiba o status do recurso de gerenciamento de energia  

 - **Send Schedule Tool**: aciona agendas e avaliações de linhas de base do DCM  

> [!Important]  
> O [Centro de Suporte](#support-center) é recomendado para a maioria casos de uso, pois inclui uma funcionalidade igual ou aprimorada para as seguintes ferramentas:  
>  - Client Spy
>  - CMTrace<sup>1</sup> 
>  - Deployment Monitoring Tool
>  - Policy Spy
>  - Send Schedule Tool
> 
> <sup>1</sup> CMTrace não depende do .NET ou do WPF (Windows Presentation Foundation), portanto ainda é usado em imagens de inicialização do Windows PE.

### <a name="known-issues"></a>Problemas conhecidos
Algumas ferramentas de cliente e servidor podem fechar inesperadamente ao iniciar. Esse problema ocorre devido a um arquivo ausente na mídia. Como alternativa, copie o arquivo **Microsoft.Diagnostics.Tracing.EventSource.dll** do diretório AdminConsole\bin nos diretórios SMSSETUP\Tools\ClientTools e ServerTools. Esse arquivo deve ser a mesma versão usada pelo console do Configuration Manager. Outras versões podem não funcionar. <!--513977-->



## <a name="uninstall-application-on-approval-revocation"></a>Desinstalar o aplicativo na revogação da aprovação
<!--1357891-->

O comportamento mudou para quando você revoga a aprovação de um aplicativo. Agora, quando você nega a solicitação para o aplicativo, o cliente desinstala o aplicativo do dispositivo do usuário. 

### <a name="prerequisites"></a>Pré-requisitos
- Habilite o recurso **Aprovar solicitações de aplicativo para usuários por dispositivo**.

### <a name="try-it-out"></a>Experimente!
 Tente concluir as tarefas. Depois, envie seus [comentários](#bkmk_feedback) sobre como isso funcionou.

1. No console do Configuration Manager, implante para um usuário um aplicativo que exige aprovação. Na guia **Configuração de Implantação** da implantação, habilite a opção **Um administrador deve aprovar uma solicitação para este aplicativo no dispositivo**.  

2. No cliente do Configuration Manager, no Centro de Software, o usuário solicita aprovação para instalar o aplicativo.  

3. No console do Configuration Manager, aprove a solicitação desse usuário para instalar o aplicativo no dispositivo. As solicitações de aprovação do aplicativo são exibidas no espaço de trabalho **Biblioteca de Software**, no **Gerenciamento de Aplicativos** no nó **Solicitações de Aprovação**.  

4. No cliente no Centro de Software, o usuário instala o aplicativo.  

5. No console do Configuration Manager, negue a solicitação do usuário para o aplicativo no dispositivo.  

### <a name="known-issues"></a>Problemas conhecidos
- Depois que o usuário instalar o aplicativo no cliente, atualize a política de usuário. No Centro de Software, alterne para a guia **Opções**, expanda **Manutenção do computador** e clique em **Política de Sincronização**.<!--480609-->  

- O ponto de serviço Web do catálogo de aplicativos deve ser HTTP. Para saber mais, confira [Problemas conhecidos nesta visualização técnica](#bkmk_appcathttps).<!--512637-->  



## <a name="exclude-active-directory-containers-from-discovery"></a>Excluir contêineres do Active Directory da descoberta
<!--1358143-->
Para reduzir o número de objetos descobertos, agora você pode excluir contêineres específicos da descoberta do sistema do Active Directory. Esse recurso é resultado de seus [comentários no UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8414520-exclude-virtual-cluster-and-ou-from-discovery).

### <a name="try-it-out"></a>Experimente!
 Tente concluir as tarefas. Depois, envie seus [comentários](#bkmk_feedback) sobre como isso funcionou.

1. No console do Configuration Manager, acesse o espaço de trabalho **Administração**. Expanda **Configuração da Hierarquia** e selecione **Métodos de Descoberta**. Selecione **Descoberta de Sistema do Active Directory** e clique em **Propriedades** na faixa de opções.  

2. Clique no ícone Novo para especificar um novo contêiner do Active Directory.   

3. Na caixa de diálogo Contêiner do Active Directory, procure ou insira o **Caminho** na seção Local para iniciar a descoberta.  

4. Na seção Opções de Pesquisa, habilite a opção para **Pesquisar recursivamente contêineres filho do Active Directory**. Em seguida, clique em **Adicionar** para selecionar sub-recipientes para exclusão desta descoberta.  

5. Na caixa de diálogo Selecionar Novo Contêiner, selecione um contêiner filho para exclusão. Clique em **OK** para fechar a caixa de diálogo Selecionar Novo Contêiner.  

6. Clique em **OK** para fechar a caixa de diálogo Contêiner do Active Directory.  

7. Na janela Propriedades de Descoberta de Sistemas do Active Directory, consulte o caminho do contêiner do Active Directory no qual a descoberta começa. A coluna **Recursiva** mostra **Sim**, e a nova coluna **Tem Exclusões** também mostra **Sim**. Clique em **OK** para fechar a janela Propriedades de Descoberta de Sistemas do Active Directory.  



## <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Especificar a visibilidade do link de site do Catálogo de Aplicativos no Centro de Software
<!--1358214-->

Agora, você pode controlar se o link para **Abrir o site do Catálogo de Aplicativos** aparece no nó **Status da instalação** do Centro de Software.  

> [!Note]  
> O suporte para a experiência de usuário do site do Catálogo de Aplicativos termina com a primeira atualização liberada após 1º de junho de 2018. Para saber mais, consulte [Recursos removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

### <a name="try-it-out"></a>Experimente!
 Tente concluir as tarefas. Depois, envie seus [comentários](#bkmk_feedback) sobre como isso funcionou.

1. No console do Configuration Manager, no espaço de trabalho **Administração**, nó **Configurações do Cliente** , crie uma política personalizada de configurações de dispositivos de cliente.  

2. Selecione o grupo **Centro de Software**.  

3. Para **Configurações do Centro de Software**, clique em **Personalizar**.  

4. Habilite a opção de **Ocultar o link de site do Catálogo de Aplicativos no Centro de Software**.   

Para saber mais sobre configurações do cliente, confira [Definir configurações do cliente](/sccm/core/clients/deploy/configure-client-settings).




## <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Filtrar regras de implantação automática pela arquitetura de atualização de software
 <!--1322266-->
Agora, você pode filtrar as regras de implantação automática para excluir arquiteturas como Itanium e ARM64.

### <a name="try-it-out"></a>Experimente!
Tente concluir as tarefas. Depois, envie seus [comentários](#bkmk_feedback) sobre como isso funcionou.

1. No console do Configuration Manager, alterne para o espaço de trabalho **Biblioteca de Software**. Expanda **Atualizações de Software** e selecione **Regras de Implantação Automática**. Na faixa de opções, selecione **Criar Regra de Implantação Automática**.  

2. Preencha as configurações adequadas da guia **Geral** e da guia **Configurações de Implantação**.  

3. Na guia **Atualizações de Software**, selecione **Arquitetura**, depois, clique em **itens para localizar** nos **Critérios de pesquisa**.  

4. Selecione as arquiteturas que você deseja incluir na regra de implantação automática.  

5. Clique em **Avançar** e prossiga com a criação da regra de implantação automática.  

> [!IMPORTANT]  
> Lembre-se de que há aplicativos e componentes de 32 bits (x86) em execução em sistemas de 64 bits (x64). A menos que você tenha certeza de que não precisa de x86, habilite-o também ao escolher x64.  

### <a name="known-issues"></a>Problemas conhecidos
Depois de adicionar os critérios de arquitetura, a página de propriedades da regra de implantação automática mostra **Título** nos critérios de pesquisa. A regra de implantação automática ainda funciona como esperado, e seleciona as atualizações de software corretas. No entanto, não é possível incluir os dois critérios de **Arquitetura** e **Título** no momento. <!--512634,512632-->



## <a name="improvements-to-os-deployment"></a>Melhorias na implantação do sistema operacional
Fizemos estas melhorias na implantação de sistema operacional, algumas das quais foram resultado de seus comentários no UserVoice.  

 - [Mascarar dados confidenciais armazenados em variáveis de sequência de tarefas](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): na etapa [Definir Variável de Sequência de Tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable), selecione a nova opção para **Não exibir este valor**. Por exemplo, ao especificar uma senha.<!--1358330--> Os comportamentos a seguir se aplicam quando você habilita essa opção:
   - O valor da variável não é exibido no smsts.log.
   - O console do Configuration Manager e o Provedor de SMS lidam com esse valor da mesma forma que outros segredos, como senhas.
   - O valor não será incluído quando você exportar a sequência de tarefas.
   - O editor de sequência de tarefas não lê esse valor quando você edita a etapa. Digite novamente o valor inteiro para fazer alterações.

   > [!Important]  
   > Variáveis e seus valores são salvos com a sequência de tarefas como XML, e são ofuscados no banco de dados. Quando o cliente solicita uma política de sequência de tarefas do ponto de gerenciamento, ela é criptografada em trânsito e armazenada no cliente. No entanto, todos os valores de variáveis são texto sem formatação no ambiente da sequência de tarefas na memória durante a execução no cliente. Se a sequência de tarefas incluir uma etapa para mostrar o valor da variável, essa saída será em texto sem formatação. Esse comportamento exige uma ação explícita do administrador para incluir uma etapa como essa na sequência de tarefas. 


 - [Ocultar o nome do programa durante a Etapa de Execução de Comando de uma sequência de tarefas](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): para evitar a exibição ou registro em log de dados possivelmente confidenciais, defina a variável de sequência de tarefas **OSDDoNotLogCommand** como `TRUE`. Essa variável oculta o nome do programa no smsts.log durante uma etapa da sequência de tarefas [Executar Linha de Comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine). <!--1358493-->  



## <a name="improvements-to-the-configuration-manager-console"></a>Melhorias no console do Configuration Manager
- Agora, as informações de usuário principal estão visíveis ao exibir os membros de uma coleção em **Ativos e Conformidade**, **Coleções de Dispositivos**.<!--510252-->  



## <a name="next-steps"></a>Próximas etapas
Para obter informações de como instalar ou atualizar o branch da technical preview, consulte [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
