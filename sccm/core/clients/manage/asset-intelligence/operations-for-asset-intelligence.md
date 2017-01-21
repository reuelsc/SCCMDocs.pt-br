---
title: Usar o Asset Intelligence | Microsoft Docs
description: Realize tarefas comuns do Asset Intelligence no System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e8159bd9-5c2b-4d25-82f9-78fcfd732ba9
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 6bfbfbcce6ef5c38164e161d197f5a3fb4b4e353


---
# <a name="how-to-use-asset-intelligence-in-system-center-configuration-manager"></a>Como usar o Asset Intelligence no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico contém informações para ajudar a gerenciar tarefas típicas do Asset Intelligence na sua hierarquia do System Center Configuration Manager:  

##  <a name="a-namebkmkviewinformationa-view-asset-intelligence-information"></a><a name="BKMK_ViewInformation"></a> Exibir informações do Asset Intelligence  
 Você pode exibir informações do Asset Intelligence na home page do **Asset Intelligence** e nos relatórios do Asset Intelligence.  

###  <a name="a-namebkmkassetintelligencehomepagea-asset-intelligence-home-page"></a><a name="BKMK_AssetIntelligenceHomePage"></a> Home page do Asset Intelligence  
 A home page do **Asset Intelligence** exibe um painel de resumo das informações do catálogo do Asset Intelligence. Na home page, você pode exibir informações sobre a sincronização do catálogo e o status de software inventariado. A home page do **Asset Intelligence** é dividida nas seguintes seções:  

-   **Sincronização de catálogo**: fornece informações sobre se o Asset Intelligence está habilitado, o status atual do ponto de sincronização do Asset Intelligence, o agendamento de sincronização, se o demonstrativo de licença do cliente foi importado, a última atualização de status e a hora da próxima atualização agendada e o número de alterações que ocorreram depois que o sistema de sites do ponto de sincronização do Asset Intelligence foi instalado.  

    > [!NOTE]  
    >  A seção de sincronização do catálogo do Asset Intelligence da home page do **Asset Intelligence** é exibida somente se uma função do sistema de sites do ponto de sincronização do Asset Intelligence tiver sido instalada.  

-   **Status de Software Inventariado**: fornece a contagem e o percentual de software inventariado, categorias de software e famílias de software que são identificadas pela Microsoft, identificados por um usuário administrativo, com identificação online pendente ou não identificados e não pendentes. As informações exibidas em formato de tabela mostram a contagem para cada um, enquanto as informações exibidas no gráfico mostram o percentual de cada um.  

 Use o procedimento a seguir para exibir informações do Asset Intelligence na home page do **Asset Intelligence** .  

##### <a name="to-view-asset-intelligence-information-on-the-asset-intelligence-home-page"></a>Para exibir informações do Asset Intelligence na home page do Asset Intelligence  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Asset Intelligence**. Os relatórios do Asset Intelligence são exibidos.  

###  <a name="a-namebkmkassetintelligencereportsa-asset-intelligence-reports"></a><a name="BKMK_AssetIntelligenceReports"></a> Relatórios do Asset Intelligence  
 Há mais de 60 relatórios do Asset Intelligence que exibem as informações coletadas pelo Asset Intelligence. Muitos desses relatórios contêm links para relatórios mais específicos nos quais você pode executar consultas para obter informações gerais e fazer uma busca detalhada das informações. Os relatórios do Asset Intelligence estão localizados no console do Configuration Manager, no espaço de trabalho **Monitoramento**, no nó **Relatórios**. Os relatórios fornecem informações sobre hardware, gerenciamento de licenças e software. Para obter mais informações sobre os relatórios no Configuration Manager, consulte [Relatórios no System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

> [!NOTE]  
>  A precisão das quantidades de título de software instaladas e das informações de licença exibidas nos relatórios do Asset Intelligence pode variar do número real dos títulos de software instalados ou das licenças usadas no ambiente, devido a dependências complexas e limitações envolvidas no inventário das informações de licença de software para títulos de software instalados em ambientes corporativos. Os relatórios do Asset Intelligence não devem ser usados como a única origem para determinar a conformidade das licenças de software adquiridas.  

 Use o procedimento a seguir para exibir informações do Asset Intelligence usando os relatórios do Asset Intelligence.  

##### <a name="to-view-collected-asset-intelligence-information-by-using-asset-intelligence-reports"></a>Para exibir as informações do Asset Intelligence coletadas usando relatórios do Asset Intelligence  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Relatório**, expanda **Relatórios**e clique em **Asset Intelligence**. Os relatórios do Asset Intelligence são exibidos.  

    > [!WARNING]  
    >  Se não houver nenhuma pasta de relatório no nó **Relatórios** , verifique se você configurou o relatório. Para mais informações, consulte [Configurando relatórios no System Center Configuration Manager](../../../../core/servers/manage/configuring-reporting.md).  

3.  Selecione o relatório do Asset Intelligence que deseja executar e, na guia **Início** , no grupo **Grupo de Relatório** , clique em **Executar**.  

##  <a name="a-namebkmksynchronizethecataloga-synchronize-the-asset-intelligence-catalog"></a><a name="BKMK_SynchronizeTheCatalog"></a> Sincronizar o catálogo do Asset Intelligence  
 Você pode sincronizar o catálogo do Asset Intelligence local com o System Center Online para recuperar a categorização de título de software mais recente. Quando você solicita manualmente a sincronização do catálogo com o System Center Online, pode levar 15 minutos ou mais para concluir o processo de sincronização com o System Center Online. O Configuration Manager atualiza a configuração **Última Atualização Bem-sucedida** na home page do **Asset Intelligence** com a hora atual em que a sincronização foi concluída com êxito.  

> [!NOTE]  
>  Uma função do sistema de sites do ponto de sincronização do Asset Intelligence deve ser instalada primeiro antes de usar os procedimentos. Para obter informações sobre a instalação de um ponto de sincronização do Asset Intelligence, consulte [Configuração do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Use o procedimento a seguir para criar um agendamento de sincronização para o catálogo do Asset Intelligence.  

#### <a name="to-create-a-synchronization-schedule-for-the-asset-intelligence-catalog"></a>Para criar uma agendamento de sincronização para o catálogo do Asset Intelligence  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Asset Intelligence**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Sincronizar**e em **Agendar Sincronização**.  

4.  Na caixa de diálogo **Agendamento do Ponto de Sincronização do Asset Intelligence** , selecione **Habilitar sincronização em um agendamento**e configure um agendamento simples ou personalizado.  

5.  Clique em **OK** para salvar as alterações.  

    > [!NOTE]  
    >  Para obter informações sobre o agendamento de sincronização, incluindo a próxima sincronização agendada, veja o nó **Asset Intelligence** do espaço de trabalho **Ativos e Conformidade** no site de nível superior da hierarquia.  

 Use o procedimento a seguir para sincronizar manualmente o catálogo do Asset Intelligence.  

> [!WARNING]  
>  O System Center Online aceita apenas uma solicitação de sincronização manual em um período de 12 horas.  

###  <a name="a-namebkmkmanuallysynchronizecataloga-to-manually-synchronize-the-asset-intelligence-catalog"></a><a name="BKMK_ManuallySynchronizeCatalog"></a> Para sincronizar manualmente o catálogo do Asset Intelligence  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Asset Intelligence**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Sincronizar**, em **Sincronizar Catálogo do Asset Intelligence**e em **OK**.  

##  <a name="a-namebkmkcustomizecataloga-customize-the-asset-intelligence-catalog"></a><a name="BKMK_CustomizeCatalog"></a> Personalizar o catálogo do Asset Intelligence  
 As informações de categorização do catálogo do Asset Intelligence recebidas do System Center Online são armazenadas no banco de dados do site com permissões somente leitura e não podem ser modificadas ou excluídas. No entanto, você pode criar, modificar e excluir categorias de software personalizado, famílias de software, rótulos de software e informações do catálogo de requisitos de hardware. Em seguida, você pode usar os dados personalizados de categorização em vez das informações fornecidas pelo System Center Online para informações de título de software existentes ou definidas pelo usuário. Ao alterar ou adicionar informações de categorização, as informações do catálogo são consideradas definidas pelo usuário. As informações de categorização definidas pelo usuário são armazenadas em tabelas de banco de dados diferentes das informações do catálogo validadas.  

###  <a name="a-namebkmksoftwarecategoriesa-software-categories"></a><a name="BKMK_SoftwareCategories"></a> Categorias de software  
 As categorias de software do Asset Intelligence são usadas para categorizar de forma generalizada os títulos de software inventariados e também são usadas como agrupamentos de alto nível de famílias de software mais específicas. Por exemplo, uma categoria de software pode ser empresas de energia, e uma família de software nessa categoria de software pode ser petróleo e gás ou hidrelétrica. Muitas categorias de software são predefinidas no catálogo do Asset Intelligence, e outras categorias definidas pelo usuário podem ser criadas para definir com mais detalhes o software inventariado. O estado de validação para todas as categorias de software predefinido é sempre **Validado**, enquanto as informações de categorias de software personalizado adicionadas ao catálogo do Asset Intelligence são **Definidas pelo Usuário**.  

 Use o procedimento a seguir para criar uma categoria de software definida pelo usuário.  

##### <a name="to-create-a-user-defined-software-category"></a>Para criar uma categoria de software definida pelo usuário  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Asset Intelligence**e em **Catálogo**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Categoria de Software**.  

4.  Na página **Geral** , insira um nome para a nova categoria de software e, opcionalmente, uma descrição.  

    > [!NOTE]  
    >  O estado de validação para todas as novas categorias de software personalizado é sempre definido como **Definido pelo Usuário**.  

     Clique em **Avançar**.  

5.  Na página **Resumo** , examine as configurações e clique em **Avançar**.  

6.  Na página **Conclusão** , clique em **Fechar** para sair do assistente.  

###  <a name="a-namebkmksoftwarefamiliesa-software-families"></a><a name="BKMK_SoftwareFamilies"></a> Famílias de software  
 As famílias de software do Asset Intelligence são usadas para definir mais detalhadamente os títulos de software inventariados em categorias de software. Por exemplo, uma categoria de software pode ser empresas de energia, e uma família de software nessa categoria de software pode ser petróleo e gás ou hidrelétrica. Muitas famílias de software são predefinidas no catálogo do Asset Intelligence, e outras famílias definidas pelo usuário podem ser criadas para definir o software inventariado. O estado de validação para todas as famílias de software predefinido é sempre **Validado**, enquanto as informações de famílias de software personalizado adicionadas ao catálogo do Asset Intelligence são **Definidas pelo Usuário**.  

 Use o procedimento a seguir para criar uma família de software definida pelo usuário.  

##### <a name="to-create-a-user-defined-software-family"></a>Para criar uma família de software definida pelo usuário  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Asset Intelligence**e em **Catálogo**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Família de Software**.  

4.  Na página **Geral** , insira um nome para a nova família de software e, opcionalmente, uma descrição.  

    > [!NOTE]  
    >  O estado de validação para todas as novas famílias de software personalizado é sempre definido como **Definido pelo Usuário**.  

5.  Na página **Resumo** , examine as configurações e clique em **Avançar**.  

6.  Na página **Conclusão** , clique em **Fechar** para sair do assistente.  

###  <a name="a-namebkmksoftwarelabelsa-software-labels"></a><a name="BKMK_SoftwareLabels"></a> Rótulos de software  
 Os rótulos de software personalizado do Asset Intelligence permitem criar filtros que você pode usar para agrupar títulos de software e exibi-los usando os relatórios do Asset Intelligence. Por exemplo, é possível criar um rótulo de software chamado shareware, associá-lo a uma quantidade de aplicativos e depois executar um relatório que mostra todos os títulos com o rótulo de software chamado shareware. O estado de validação é **Definido pelo Usuário** para todos os rótulos de software personalizado que você adicionar ao catálogo do Asset Intelligence.  

 Use o procedimento a seguir para criar um rótulo personalizado definido pelo usuário.  

##### <a name="to-create-a-user-defined-software-label"></a>Para criar um rótulo de software definido pelo usuário  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Asset Intelligence**e em **Catálogo**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Rótulo de Software**.  

4.  Na página **Geral** , insira um nome para a nova família de software e, opcionalmente, uma descrição.  

    > [!NOTE]  
    >  O estado de validação para todos os novos rótulos de software personalizado é sempre definido como **Definido pelo Usuário**.  

5.  Na página **Resumo** , examine as configurações e clique em **Avançar**.  

6.  Na página **Conclusão** , clique em **Fechar** para sair do assistente.  

###  <a name="a-namebkmkhardwarerequirementsa-hardware-requirements"></a><a name="BKMK_HardwareRequirements"></a> Requisitos de hardware  
 As informações sobre requisitos de hardware podem ajudá-lo a verificar se os computadores atendem aos requisitos de hardware para títulos de software antes que sejam afetados por implantações de software. Vários requisitos de hardware são predefinidos no catálogo do Asset Intelligence. Assim, você pode criar novas informações de requisitos de hardware definido pelo usuário para atender a requisitos personalizados. O estado de validação para todos os requisitos de hardware predefinido é sempre **Validado**, enquanto as informações de requisitos de hardware adicionadas ao catálogo do Asset Intelligence são **Definidas pelo Usuário**.  

> [!IMPORTANT]  
>  Os requisitos de hardware exibidos no console do Configuration Manager são recuperados do catálogo do Asset Intelligence no computador local e não são baseados em informações de título de software inventariados de clientes do System Center 2012 Configuration Manager. As informações de requisitos de hardware não são atualizadas como parte do processo de sincronização com o System Center Online. Você pode criar requisitos de hardware definidos pelo usuário para o software inventariado que não contém requisitos de hardware associado.  

 Use o procedimento a seguir para criar um requisito de hardware definido pelo usuário.  

##### <a name="to-create-a-user-defined-hardware-requirements"></a>Para criar requisitos de hardware definidos pelo usuário  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Asset Intelligence**e em **Requisitos de Hardware**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Requisitos de Hardware**.  

4.  Na página **Geral** , insira as seguintes informações:  

    1.  **Título de software**: especifica o título de software ao qual os requisitos de hardware estão associados. O título de software não pode existir no catálogo do Asset Intelligence.  

    2.  **Estado de validação**: lista o estado de validação como **Definido pelo Usuário** para os requisitos de hardware. Não é possível modificar essa configuração.  

    3.  **CPU Mínima (MHz)**: especifica a velocidade mínima do processador, em MHz (mega-hertz), requerida pelo título de software.  

    4.  **RAM Mínima (KB)**: especifica a RAM mínima, em KB (quilobytes), requerida pelo título de software.  

    5.  **Espaço Mínimo em Disco (KB)**: especifica o espaço mínimo livre em disco, em KB, necessário para o título de software.  

    6.  **Tamanho Mínimo de Disco (KB)**: especifica o tamanho mínimo de disco, em KB, requerido pelo título de software.  

     Clique em **Avançar**.  

5.  Na página **Resumo** , examine as configurações e clique em **Avançar**.  

6.  Na página **Conclusão** , clique em **Fechar** para sair do assistente.  

###  <a name="a-namebkmkmodifycategorizationa-modify-categorization-information-for-inventoried-software"></a><a name="BKMK_ModifyCategorization"></a> Modificar informações de categorização de software inventariado  
 O software predefinido no catálogo do Asset Intelligence é configurado com informações de categorização específicas, como nome do produto, fornecedor, categoria de software e família de software. Quando as informações de categorização predefinidas não atenderem a seus requisitos, você poderá modificar as informações nas propriedades do título de software. Quando você modifica informações de categorização de software predefinido, o estado de validação para o software muda de **Validado** para **Definido pelo Usuário**.  

> [!IMPORTANT]  
>  As informações de categorização só podem ser modificadas no site de nível superior.  

 Use o procedimento a seguir para modificar informações de categorização de software inventariado.  

##### <a name="to-modify-the-categorizations-for-software-titles"></a>Para modificar as categorizações para títulos de software  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Asset Intelligence**e em **Software Inventariado**.  

3.  Selecione um título de software ou vários títulos de software para os quais você deseja modificar as categorizações.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Na guia **Geral** , é possível modificar as seguintes informações de categorização:  

    -   **Nome do Produto**: especifica o nome do título de software inventariado.  

    -   **Fornecedor**: especifica o nome do fornecedor que desenvolveu o título de software inventariado.  

    -   **Categoria**: especifica a categoria de software que está atribuída no momento ao título de software inventariado.  

    -   **Família**: especifica a família de software que está atribuída no momento ao título de software inventariado.  

6.  Clique em **OK** para salvar as alterações.  

 Use o procedimento a seguir para reverter o software para as informações de categorização originais.  

### <a name="revert-categorization-information-to-original-settings-for-software"></a>Reverter informações de categorização para as configurações originais de software  
 O Configuration Manager armazena as informações de categorização obtidas do System Center Online no banco de dados. As informações não podem ser excluídas. Depois que as informações foram modificadas, você poderá reverter as informações de categorização para a categorização do System Center Online. O software inventariado que não está no catálogo do Asset Intelligence também pode ser revertido para as configurações originais.  

 Use o procedimento a seguir para reverter as informações de categorização para as configurações originais.  

##### <a name="to-revert-categorization-information-to-original-settings"></a>Para retornar informações de categorização às configurações originais  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Asset Intelligence**e em **Software Inventariado**.  

3.  Selecione um título de software ou vários títulos de software que você deseja reverter para as configurações originais. Apenas o software que tem um estado **Definido pelo Usuário** pode ser revertido.  

    > [!TIP]  
    >  Clique na coluna **Estado** para classificar por estado de validação. As classificação permite que você veja todos os softwares por estado de validação e selecione rapidamente vários itens para reverter para as configurações originais.  

4.  Na guia **Início** , no grupo **Produto** , clique em **Reverter**.  

5.  Clique em **Sim** para reverter o software para as informações de categorização originais.  

6.  Ao reverter as informações de categorização de software que estão no catálogo do Asset Intelligence, o estado de validação muda de **Definido pelo Usuário** para **Validado**. Ao reverter o software que não está no catálogo, o estado de validação muda de **Definido pelo Usuário** para **Não categorizado**.  

##  <a name="a-namebkmkrequestcatalogupdatea-request-a-catalog-update-for-uncategorized-software-titles"></a><a name="BKMK_RequestCatalogUpdate"></a> Solicitar uma atualização do catálogo para títulos de software não categorizados  
 As informações de títulos de software não categorizados podem ser enviadas para o System Center Online para pesquisa e categorização. Depois que um título de software não categorizado é enviado e houver, pelo menos, quatro solicitações de categorização de clientes pelo mesmo título de software, os pesquisadores identificam, categorizam e disponibilizam as informações de categorização de título de software para todos os clientes que estão usando o serviço do System Center Online. A Microsoft oferece a prioridade mais alta para títulos de software que têm a maioria das solicitações por categorização. É pouco provável que software personalizado e aplicativos de linha de negócios recebam uma categoria; por isso, como uma prática recomendada, você não deve enviar esses títulos de software à Microsoft para categorização.  

 Quando as informações de título de software são enviadas para o System Center Online para categorização, as seguintes condições se aplicam:  

-   Somente as informações básicas do título de software são transmitidas para o System Center Online e as informações do título de software a ser categorizadas podem ser examinadas antes do envio.  

-   As informações de licença de software nunca são transmitidas.  

-   Qualquer título de software carregado se torna disponível publicamente como parte do catálogo do System Center Online e pode ser baixado por outros clientes.  

-   A origem do título de software não é armazenada no catálogo do System Center Online. No entanto, os títulos de aplicativos que contêm informações confidenciais ou proprietárias não devem ser enviados para categorização pelo System Center Online.  

> [!NOTE]  
>  Para obter mais informações sobre informações de privacidade do Asset Intelligence, consulte [Segurança e privacidade do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/security-and-privacy-for-asset-intelligence.md).  

 Use o procedimento a seguir para solicitar a categorização de título de software do catálogo do Asset Intelligence ao System Center Online.  

#### <a name="to-request-a-catalog-update-for-uncategorized-software-titles"></a>Para solicitar uma atualização do catálogo para títulos de software não categorizados  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Asset Intelligence**e em **Software Inventariado**.  

3.  Selecione um nome de produto ou vários nomes de produto a ser enviados para o System Center Online para categorização. Somente títulos de software inventariados não categorizados podem ser enviados para o System Center Online para categorização. Se um título de software inventariado tiver sido categorizado por um administrador, resultando em um estado definido pelo usuário, você deve clicar com o botão direito do mouse no título de software inventariado e clicar em **Reverter** para reverter o título do software para o estado **Não categorizado** antes que ele seja enviado ao System Center Online para categorização.  

    > [!NOTE]  
    >  O Configuration Manager pode processar até 100 títulos de software para categorização por vez. Se você selecionar mais de 100 títulos de software, somente os primeiros 100 títulos de software serão processados. É necessário selecionar os títulos de software restantes para categorização em lotes de menos de 100.  

    > [!TIP]  
    >  Clique na coluna **Estado** para classificar por estado de validação. Isso permite que você veja todos os nomes de produtos não categorizados e selecione rapidamente vários itens para enviar para categorização.  

4.  Na guia **Início** , no grupo **Produto** , clique em **Solicitar Atualização do Catálogo**.  

5.  Examine a mensagem de privacidade de envio de categorização do System Center Online. Clique em **Detalhes** para exibir as informações que serão enviadas para o System Center Online.  

6.  Selecione **Li e entendi a mensagem**e clique em **OK** para permitir que os títulos de software selecionados sejam enviados para categorização.  

7.  Verifique se o estado dos nomes de produto de software inventariado enviados para o System Center Online para categorização mudou de **Não categorizado** para **Pendente**.  

    > [!NOTE]  
    >  O software enviado ao System Center Online para categorização tem um estado de validação de **Pendente** em um site de administração central, mas ainda é exibido com um estado de validação de **Não categorizado** nos sites primários filho.  

##  <a name="a-namebkmkresolvesoftwaredetailsa-resolve-software-details-conflicts"></a><a name="BKMK_ResolveSoftwareDetails"></a> Resolver conflitos de detalhes de software  
 Depois que os detalhes da categorização de software recém-atualizado que entram em conflito com informações detalhadas existentes de software tiverem sido recebidos do System Center Online, é possível escolher como resolver o conflito. O software que tem um conflito atual apresenta um estado de validação de **Atualizável**. Depois que um conflito de detalhes de software é resolvido, as informações de categorização de software são mantidas no catálogo do Asset Intelligence de acordo com a configuração que você especificar. Não ocorre um conflito de detalhes do software para o mesmo valor de categorização de software novamente, a menos que o valor do System Center Online seja alterado depois que o conflito for resolvido.  

 Use o procedimento a seguir para resolver um conflito de detalhes de software.  

#### <a name="to-resolve-a-software-details-conflict"></a>Para resolver um conflito de detalhes de software  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Asset Intelligence**e em **Software Inventariado**.  

3.  Examine a coluna **Estado** para ver se existem títulos de software no estado **Atualizável** .  

4.  Selecione o título de software para o qual você precisa resolver um conflito e, na guia **Início** , no grupo **Produto** , clique em **Resolver Conflito**.  

5.  Reveja as seguintes informações:  

    -   **Valor local**: especifica as informações existentes de categorização de software no catálogo do Asset Intelligence que entram em conflito com os detalhes mais recentes de categorização de software do System Center Online.  

    -   **Valor baixado**: especifica as informações conflitantes de categorização de software do catálogo do Asset Intelligence nas novas informações de categorização de software do System Center Online.  

6.  Selecione uma das seguintes configurações para resolver o conflito de detalhes de software:  

    -   **Não alterar o valor das informações do catálogo editadas localmente**: resolve os conflitos de detalhes de software mantendo as informações existentes de categorização de software do catálogo do Asset Intelligence. Quando você seleciona essa configuração, o estado de título de software muda de **Atualizável** para **Definido pelo Usuário**.  

    -   **Substituir o valor de informações do catálogo editado localmente pelo valor baixado do System Center Online**: resolve os conflitos de detalhes do software com a substituição das informações existentes de categorização de software do catálogo do Asset Intelligence pelas novas informações obtidas do System Center Online. Quando você seleciona essa configuração, o estado de título de software muda de **Atualizável** para **Validado**.  

     Clique em **OK** para salvar a resolução de conflitos.  



<!--HONumber=Dec16_HO3-->


