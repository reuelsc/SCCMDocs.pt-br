---
title: "Criar relatórios personalizados | System Center Configuration Manager"
description: "Defina modelos de relatório para atender aos requisitos de negócios e, em seguida, implante os modelos de relatório no Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f2df88b4-c348-4dcf-854a-54fd6eedf485
caps.latest.revision: 5
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4b286fbca3c71b14e0b82ff421132408df7c6e8b


---
# <a name="creating-custom-report-models-for-system-center-configuration-manager-in-sql-server-reporting-services"></a>Criando modelos de relatório personalizados para o System Center Configuration Manager no SQL Server Reporting Services

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Exemplos de modelos de relatórios estão incluídos no System Center Configuration Manager, mas você também pode definir modelos de relatórios para atender aos seus próprios requisitos de negócios e implantar o modelo de relatório para o Configuration Manager a ser usado ao criar novos relatórios baseados no modelo. A tabela a seguir fornece as etapas para criar e implantar um modelo de relatório básico.  

> [!NOTE]  
>  Para ver as etapas para criar um modelo de relatório mais avançado, consulte a seção [Steps for Creating an Advanced Report Model in SQL Server Reporting Services](#AdvancedReportModel) deste tópico.  

|Etapa|Descrição|Mais informações|  
|----------|-----------------|----------------------|  
|Verifique se o SQL Server Business Intelligence Development Studio está instalado|Os modelos de relatório são projetados e criados usando o SQL Server Business Intelligence Development Studio. Verifique se o SQL Server Business Intelligence Development Studio está instalado no computador em que você está criando o modelo de relatório personalizado.|Para obter mais informações sobre o SQL Server Business Intelligence Development Studio, consulte a documentação do SQL Server 2008.|  
|Criar um projeto de modelo de relatório|Um projeto de modelo de relatório contém a definição da fonte de dados (um arquivo .ds), a definição de uma exibição da fonte de dados (um arquivo .dsv) e o modelo de relatório (um arquivo .smdl).|Para obter mais informações, consulte a seção [To create the report model project](#BKMK_CreateReportModelProject) neste tópico.|  
|Definir uma fonte de dados para um modelo de relatório|Após criar um projeto de modelo de relatório, você deverá definir uma fonte de dados da qual os dados corporativos serão extraídos. Normalmente, este é o banco de dados do site do Configuration Manager.|Para obter mais informações, consulte a seção [To define the data source for the report model](#BKMK_DefineReportModelDataSource) neste tópico.|  
|Definir uma exibição de fonte de dados para um modelo de relatório|Após definir as fontes de dados usadas no projeto do modelo de relatório, a próxima etapa é definir uma exibição de fonte de dados para o projeto. Uma exibição de fonte de dados é um modelo lógico de dados baseado em uma ou mais fontes de dados. As exibições de fontes de dados encapsulam o acesso a objetos físicos, como tabelas e exibições, contidas em fontes de dados subjacentes. O SQL Server Reporting Services gera o modelo de relatório a partir da exibição de fonte de dados.<br /><br /> As exibições de fonte de dados facilitam o processo de criação do modelo fornecendo uma representação útil dos dados especificados. Sem alterar a fonte de dados subjacente, você pode renomear tabelas e campos e adicionar campos agregados e tabelas derivadas em uma exibição de fonte de dados. Para obter um modelo eficiente, adicione somente essas tabelas à exibição de fonte de dados que pretender usar.|Para obter mais informações, consulte a seção [To define the data source view for the report model](#BKMK_DefineReportModelDataSourceView) neste tópico.|  
|Criar um modelo de relatório|Um modelo de relatório é uma camada no início do banco de dados que identifica as entidade, os campos e as funções corporativas. Quando publicado, usando esses modelos, os usuários do Construtor de Relatórios podem desenvolver relatórios sem ter de estar familiarizados com estruturas de bancos de dados ou entender e gravar consultas. Os modelos são compostos de conjuntos de itens de relatórios relacionados que são agrupados em um nome amigável, com relações predefinidas entre esses itens corporativos e com cálculos predefinidos. Os modelos são definidos usando uma linguagem XML chamada SMDL. A extensão do nome do arquivo para os arquivos de modelo de relatório é .smdl.|Para obter mais informações, consulte a seção [To create the report model](#BKMK_CreateReportModel) neste tópico.|  
|Publicar um modelo de relatório|Para criar um relatório usando o modelo que você acabou de criar, é necessário publicá-lo em um servidor de relatório. A fonte de dados e a exibição de fonte de dados serão incluídas no modelo quando ele for publicado.|Para obter mais informações, consulte a seção [To publish the report model for use in SQL Server Reporting Services](#BKMK_PublishReportModel) neste tópico.|  
|Para implantar o modelo de relatório no Configuration Manager|Antes de usar um modelo de relatório personalizado no **Assistente para Criar Relatório** para criar um relatório baseado no modelo, é necessário implantar o modelo de relatório no Configuration Manager.|Para obter mais informações, consulte a seção [To deploy the custom report model to Configuration Manager](#BKMK_DeployReportModel) neste tópico.|  

## <a name="steps-for-creating-a-basic-report-model-in-sql-server-reporting-services"></a>Etapas para criar um modelo de relatório básico no SQL Server Reporting Services  
 É possível usar os seguintes procedimentos para criar um modelo de relatório básico que os usuários do seu site poderão usar para criar relatórios baseados em modelos particulares de acordo com os dados de uma única exibição do banco de dados do Configuration Manager. Você cria um modelo de relatório que apresenta informações sobre os computadores cliente do seu site ao autor do relatório. Essas informações foram retiradas da exibição **v_R_System** no banco de dados do Configuration Manager.  

 No computador em que você executa esses procedimentos, verifique se você instalou o SQL Server Business Intelligence Development Studio e se o computador tem conectividade de rede ao servidor do ponto do Reporting Services. Para obter informações detalhadas sobre o SQL Server Business Intelligence Development Studio, consulte a documentação do SQL Server 2008.  

###  <a name="a-namebkmkcreatereportmodelprojecta-to-create-the-report-model-project"></a><a name="BKMK_CreateReportModelProject"></a> Para criar o projeto do modelo de relatório  

1.  Na área de trabalho, clique em **Iniciar**, **Microsoft SQL Server 2008**e **SQL Server Business Intelligence Development Studio**.  

2.  Após o **SQL Server Business Intelligence Development Studio** abrir no Microsoft Visual Studio, clique em **Arquivo**, **Novo**e **Projeto**.  

3.  Na caixa de diálogo **Novo Projeto** , selecione **Projeto do Modelo de Relatório** na lista **Modelos** .  

4.  Na caixa **Nome** , especifique um nome para esse modelo de relatório. Nesse exemplo, digite **Simple_Model**.  

5.  Para criar o projeto de modelo de relatório, clique em **OK**.  

6.  A solução **Simple_Model** será exibida no **Gerenciador de Soluções**.  

    > [!NOTE]  
    >  Se você não conseguir ver o painel **Gerenciador de Soluções** , clique em **Exibir**e em **Gerenciador de Soluções**.  

###  <a name="a-namebkmkdefinereportmodeldatasourcea-to-define-the-data-source-for-the-report-model"></a><a name="BKMK_DefineReportModelDataSource"></a> Para definir a fonte de dados para o modelo de relatório  

1.  No painel **Gerenciador de Soluções** do **SQL Server Business Intelligence Development Studio**, clique com o botão direito do mouse em **Fontes de Dados** para selecionar **Adicionar Nova Fonte de Dados**.  

2.  Na página **Bem-vindo ao Assistente de Fonte de Dados** , clique em **Próximo**.  

3.  Na página **Selecione como definir a conexão** , verifique se a opção **Criar uma fonte de dados com base em uma conexão nova ou existente** está selecionada e clique em **Nova**.  

4.  Na caixa de diálogo **Gerenciador de Conexões** , especifique as seguintes propriedades de conexão para a fonte de dados:  

    -   **Nome do servidor**: digite o nome do seu servidor de banco de dados do site do Configuration Manager ou selecione-o na lista. Se você estiver trabalhando com uma instância nomeada em vez da instância padrão, digite &lt;*servidor de banco de dados*>\\&lt;*nome da instância*>.  

    -   Selecione **Usar Autenticação do Windows**.  

    -   Na lista **Selecionar ou digitar nome do banco de dados**, selecione o nome do banco de dados do site do Configuration Manager.  

5.  Para verificar a conexão do banco de dados, clique em **Testar Conexão**.  

6.  Se a conexão for bem-sucedida, clique em **OK** para fechar a caixa de diálogo **Gerenciador de Conexões** . Se a conexão não for bem-sucedida, verifique se as informações inseridas estão corretas e clique em **Testar Conexão** novamente.  

7.  Na página **Selecione como definir a conexão** , verifique se a opção **Criar uma fonte de dados com base em uma conexão nova ou existente** está selecionada, verifique se a fonte de dados especificada está selecionada em **Conexões de Dados**e clique em **Próximo**.  

8.  Em **Nome da fonte de dados**, especifique um nome para a fonte de dados e clique em **Concluir**. Nesse exemplo, digite **Simple_Model**.  

9. A fonte de dados **Simple_Model.ds** será exibida no **Gerenciador de Soluções** no nó **Fontes de Dados** .  

    > [!NOTE]  
    >  Para editar as propriedades de uma fonte de dados existente, clique duas vezes na fonte de dados na pasta **Fontes de Dados** do painel **Gerenciador de Soluções** para exibir as propriedades da fonte de dados no Designer de Fonte de Dados.  

###  <a name="a-namebkmkdefinereportmodeldatasourceviewa-to-define-the-data-source-view-for-the-report-model"></a><a name="BKMK_DefineReportModelDataSourceView"></a> Para definir a exibição da fonte de dados par ao modelo de relatório  

1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Exibições da Fonte de Dados** para selecionar **Adicionar Nova Exibição da Fonte de Dados**.  

2.  Na página **Bem-vindo ao Assistente de Exibição da Fonte de Dados** , clique em **Próximo**. A página **Selecionar uma Fonte de Dados** é exibida.  

3.  Na janela **Fontes de dados relacionais** , verifique se a fonte de dados **Simple_Model** está selecionada e clique em **Próximo**.  

4.  Na página **Selecionar Tabelas e Exibições** , selecione a seguinte exibição na lista **Objetos disponíveis** que será usada no modelo de relatório: **v_R_System (dbo)**.  

    > [!TIP]  
    >  Para ajudar a localizar exibições na lista **Objetos disponíveis** , clique no cabeçalho **Nome** na parte superior da lista para classificar os objetos em ordem alfabética.  

5.  Depois de selecionar a exibição, clique em **>** para transferir o objeto para a lista **Objetos incluídos** .  

6.  Se a página **Correspondência de Nomes** for exibida, aceite as seleções padrão e clique em **Próximo**.  

7.  Após selecionar os objetos desejados, clique em **Próximo**e especifique um nome para a exibição da fonte de dados. Nesse exemplo, digite **Simple_Model**.  

8.  Clique em **Finalizar**. A exibição da fonte de dados **Simple_Model.dsv** será exibida na pasta **Exibições da Fonte de Dados** do **Gerenciador de Soluções**.  

###  <a name="a-namebkmkcreatereportmodela-to-create-the-report-model"></a><a name="BKMK_CreateReportModel"></a> Para criar o modelo de relatório  

1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Modelos de Relatório** para selecionar **Adicionar Novo Modelo de Relatório**.  

2.  Na página **Bem-vindo ao Assistente de Modelos de Relatório** , clique em **Próximo**.  

3.  Na página **Selecionar Exibições da Fonte de Dados** , selecione a exibição da fonte de dados na lista **Exibições da fonte de dados disponíveis** e clique em **Próximo**. Para esse exemplo, selecione **Simple_Model.dsv**.  

4.  Na página **Selecione as regras de geração automática do modelo de relatório** , aceite os valores padrão e clique em **Próximo**.  

5.  Na página **Coletar Estatísticas do Modelo** , verifique se a opção **Atualizar as estatísticas do modelo antes da geração automática** está selecionada e clique em **Próximo**.  

6.  Na página **Concluindo o Assistente** , especifique um nome para o modelo de relatório. Para esse exemplo, verifique se **Simple_Model** é exibida.  

7.  Para concluir o assistente e criar o modelo de relatório, clique em **Executar**.  

8.  Para sair do assistente, clique em **Concluir**. O modelo de relatório é mostrado na janela Design.  

###  <a name="a-namebkmkpublishreportmodela-to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a><a name="BKMK_PublishReportModel"></a> Para publicar o modelo de relatório para uso no SQL Server Reporting Services  

1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse para selecionar **Implantar**. Nesse exemplo, o modelo de relatório é **Simple_Model.smdl**.  

2.  Examine o status da implantação no canto inferior esquerdo da janela do **SQL Server Business Intelligence Development Studio** . Quando a implantação for concluída, a mensagem **Implantação bem-sucedida** será exibida. Se a implantação falhar, o motivo da falha será exibido na janela **Saída** . O novo modelo de relatório estará disponível no seu site do SQL Server Reporting Services.  

3.  Clique em **Arquivo**, **Salvar Tudo**e feche o **SQL Server Business Intelligence Development Studio**.  

###  <a name="a-namebkmkdeployreportmodela-to-deploy-the-custom-report-model-to-configuration-manager"></a><a name="BKMK_DeployReportModel"></a> Para implantar o modelo de relatório personalizado no Configuration Manager  

1.  Localize a pasta na qual você criou o projeto de modelo de relatório. Por exemplo, %*USERPROFILE*%\Documentos\Visual Studio 2008\Projetos\\*&lt;Nome do Projeto\>.*  

2.  Copie os seguintes arquivos da pasta do projeto de modelo de relatório para uma pasta temporária em seu computador:  

    -   *&lt;Nome do Modelo\>* **.dsv**  

    -   *&lt;Nome do Modelo\>* **.smdl**  

3.  Abra os arquivos acima usando um editor de texto, como o Bloco de Notas.  

4.  No arquivo *&lt;Nome do Modelo\>***.dsv**, localize a primeira linha do arquivo, que é a seguinte:  

     **&lt;DataSourceView xmlns="http://schemas.microsoft.com/analysisservices/2003/engine"\>**  

     Edite essa linha da seguinte forma:  

     **&lt;DataSourceView xmlns="http://schemas.microsoft.com/analysisservices/2003/engine" xmlns:xsi="RelationalDataSourceView"\>**  

5.  Copie todo o conteúdo do arquivo na área de transferência do Windows.  

6.  Feche o arquivo *&lt;Nome do Modelo\>***.dsv**.  

7.  No arquivo *&lt;Nome do Modelo\>***.smdl**, localize as três últimas linhas do arquivo, que aparecem da seguinte maneira:  

     `</Entity>`  

     `</Entities>`  

     `</SemanticModel>`  

8.  Cole o conteúdo do arquivo *&lt;Nome do Modelo\>***.dsv** diretamente antes da última linha do arquivo (**&lt;SemanticModel\>**).  

9. Salve e feche o arquivo *&lt;Nome do Modelo\>***.smdl**.  

10. Copie o arquivo *&lt;Nome do Modelo\>***.smdl** para a pasta *%programfiles%*\Microsoft Configuration Manager \AdminConsole\XmlStorage\Other no servidor do site do Configuration Manager.  

    > [!IMPORTANT]  
    >  Depois de copiar o arquivo do modelo de relatório para o servidor do site do Configuration Manager, saia e reinicie o console do Configuration Manager antes de usar o modelo de relatório no **Assistente para Criar Relatório**.  

##  <a name="a-nameadvancedreportmodela-steps-for-creating-an-advanced-report-model-in-sql-server-reporting-services"></a><a name="AdvancedReportModel"></a> Etapas para criar um modelo de relatório avançado no SQL Server Reporting Services  
 É possível usar os seguintes procedimentos para criar um modelo de relatório avançado que os usuários em seu site poderão usar para criar relatórios baseados em modelos particulares, de acordo com os dados de várias exibições do banco de dados do Configuration Manager. Você cria um modelo de relatório que apresente as informações sobre os computadores cliente e o sistema operacional instalados nesses computadores ao autor do relatório. Essas informações foram retiradas das seguintes exibições no banco de dados do Configuration Manager:  

-   **V_R_System**: contém informações sobre os computadores descobertos e sobre o cliente do Configuration Manager.  

-   **V_GS_OPERATING_SYSTEM**: contém informações sobre o sistema operacional instalado no computador cliente.  

 Os itens selecionados nas exibições anteriores são consolidados em uma lista, recebem nomes amigáveis e são apresentados ao autor do relatório no Construtor de Relatórios para inclusão em determinados relatórios.  

 No computador em que você executa esses procedimentos, verifique se você instalou o SQL Server Business Intelligence Development Studio e se o computador tem conectividade de rede ao servidor do ponto do Reporting Services. Para obter informações detalhadas sobre o SQL Server Business Intelligence Development Studio, consulte a documentação do SQL Server.  

#### <a name="to-create-the-report-model-project"></a>To create the report model project  

1.  Na área de trabalho, clique em **Iniciar**, **Microsoft SQL Server 2008**e **SQL Server Business Intelligence Development Studio**.  

2.  Após o **SQL Server Business Intelligence Development Studio** abrir no Microsoft Visual Studio, clique em **Arquivo**, **Novo**e **Projeto**.  

3.  Na caixa de diálogo **Novo Projeto** , selecione **Projeto do Modelo de Relatório** na lista **Modelos** .  

4.  Na caixa **Nome** , especifique um nome para esse modelo de relatório. Nesse exemplo, digite **Advanced_Model**.  

5.  Para criar o projeto de modelo de relatório, clique em **OK**.  

6.  A solução **Advanced_Model** será exibida no **Gerenciador de Soluções**.  

    > [!NOTE]  
    >  Se você não conseguir ver o painel **Gerenciador de Soluções** , clique em **Exibir**e em **Gerenciador de Soluções**.  

#### <a name="to-define-the-data-source-for-the-report-model"></a>To define the data source for the report model  

1.  No painel **Gerenciador de Soluções** do **SQL Server Business Intelligence Development Studio**, clique com o botão direito do mouse em **Fontes de Dados** para selecionar **Adicionar Nova Fonte de Dados**.  

2.  Na página **Bem-vindo ao Assistente de Fonte de Dados** , clique em **Próximo**.  

3.  Na página **Selecione como definir a conexão** , verifique se a opção **Criar uma fonte de dados com base em uma conexão nova ou existente** está selecionada e clique em **Nova**.  

4.  Na caixa de diálogo **Gerenciador de Conexões** , especifique as seguintes propriedades de conexão para a fonte de dados:  

    -   **Nome do servidor**: digite o nome do seu servidor de banco de dados do site do Configuration Manager ou selecione-o na lista. Se você estiver trabalhando com uma instância nomeada em vez da instância padrão, digite &lt;*servidor de banco de dados*>\\&lt;*nome da instância*>.  

    -   Selecione **Usar Autenticação do Windows**.  

    -   Na lista **Selecionar ou digitar nome do banco de dados**, selecione o nome do banco de dados do site do Configuration Manager.  

5.  Para verificar a conexão do banco de dados, clique em **Testar Conexão**.  

6.  Se a conexão for bem-sucedida, clique em **OK** para fechar a caixa de diálogo **Gerenciador de Conexões** . Se a conexão não for bem-sucedida, verifique se as informações inseridas estão corretas e clique em **Testar Conexão** novamente.  

7.  Na página **Selecione como definir a conexão** , verifique se a opção **Criar uma fonte de dados com base em uma conexão nova ou existente** está selecionada, verifique se a fonte de dados especificada está selecionada na caixa de listagem **Conexões de Dados** e clique em **Próximo**.  

8.  Em **Nome da fonte de dados**, especifique um nome para a fonte de dados e clique em **Concluir**. Nesse exemplo, digite **Advanced_Model**.  

9. A fonte de dados **Advanced_Model.ds** é exibida no **Gerenciador de Soluções** no nó **Fontes de Dados** .  

    > [!NOTE]  
    >  Para editar as propriedades de uma fonte de dados existente, clique duas vezes na fonte de dados na pasta **Fontes de Dados** do painel **Gerenciador de Soluções** para exibir as propriedades da fonte de dados no Designer de Fonte de Dados.  

#### <a name="to-define-the-data-source-view-for-the-report-model"></a>To define the data source view for the report model  

1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Exibições da Fonte de Dados** para selecionar **Adicionar Nova Exibição da Fonte de Dados**.  

2.  Na página **Bem-vindo ao Assistente de Exibição da Fonte de Dados** , clique em **Próximo**. A página **Selecionar uma Fonte de Dados** é exibida.  

3.  Na janela **Fontes de dados relacionais** , verifique se a fonte de dados **Advanced_Model** está selecionada e clique em **Próximo**.  

4.  Na página **Selecionar Tabelas e Exibições** , selecione as seguintes exibições na lista **Objetos disponíveis** a ser usada no modelo de relatório:  

    -   **v_R_System (dbo)**  

    -   **v_GS_OPERATING_SYSTEM (dbo)**  

     Depois de selecionar cada exibição, clique em **>** para transferir o objeto para a lista **Objetos incluídos** .  

    > [!TIP]  
    >  Para ajudar a localizar exibições na lista **Objetos disponíveis** , clique no cabeçalho **Nome** na parte superior da lista para classificar os objetos em ordem alfabética.  

5.  Se a caixa de diálogo **Correspondência de Nomes** for exibida, aceite as seleções padrão e clique em **Próximo**.  

6.  Após selecionar os objetos desejados, clique em **Próximo**e especifique um nome para a exibição da fonte de dados. Nesse exemplo, digite **Advanced_Model**.  

7.  Clique em **Finalizar**. A exibição da fonte de dados **Advanced_Model.dsv** é exibida na pasta **Exibições da Fonte de Dados** do **Gerenciador de Soluções**.  

#### <a name="to-define-relationships-in-the-data-source-view"></a>Para definir relacionamentos na exibição da fonte de dados  

1.  No **Gerenciador de Soluções**, clique duas vezes em **Advanced_Model.dsv** para abrir a janela Design.  

2.  Clique com o botão direito do mouse na barra de título da janela **v_R_System** para selecionar **Substituir Tabela**e clique em **Nova Consulta Nomeada**.  

3.  Na caixa de diálogo **Criar Consulta Nomeada** , clique no ícone **Adicionar Tabela** (geralmente o último ícone da faixa de opções).  

4.  Na caixa de diálogo **Adicionar Tabela** , clique na guia **Exibições** , selecione **V_GS_OPERATING_SYSTEM** na lista e clique em **Adicionar**.  

5.  Clique em **Fechar** para fechar a caixa de diálogo **Adicionar Tabela** .  

6.  Na caixa de diálogo **Criar Consulta Nomeada** , especifique as seguintes informações:  

    -   **Nome:** especifique o nome para a consulta. Nesse exemplo, digite **Advanced_Model**.  

    -   **Descrição:** especifique uma descrição para a consulta. Neste exemplo, digite **Exemplo de modelo de relatório do Reporting Services**.  

7.  Na janela **v_R_System** , selecione os seguintes itens na lista de objetos para que sejam exibidos no modelo de relatório:  

    -   **ResourceID**  

    -   **ResourceType**  

    -   **Active0**  

    -   **AD_Domain_Name0**  

    -   **AD_SiteName0**  

    -   **Client0**  

    -   **Client_Type0**  

    -   **Client_Version0**  

    -   **CPUType0**  

    -   **Hardware_ID0**  

    -   **User_Domain0**  

    -   **User_Name0**  

    -   **Netbios_Name0**  

    -   **Operating_System_Name_and0**  

8.  Na caixa **v_GS_OPERATING_SYSTEM** , selecione os seguintes itens na lista de objetos para que sejam exibidos no modelo de relatório:  

    -   **ResourceID**  

    -   **Caption0**  

    -   **CountryCode0**  

    -   **CSDVersion0**  

    -   **Description0**  

    -   **InstallDate0**  

    -   **LastBootUpTime0**  

    -   **Locale0**  

    -   **Manufacturer0**  

    -   **Version0**  

    -   **WindowsDirectory0**  

9. Para apresentar os objetos dessas exibições como uma lista ao autor do relatório, é necessário especificar um relacionamento entre as duas tabelas ou exibições usando uma junção. Você pode juntar as duas exibições usando o objeto **ResourceID**, que aparece em ambas as exibições.  

10. Na janela **v_R_System** , clique e segure o objeto **ResourceID** e arraste-o para o objeto **ResourceID** na janela **v_GS_OPERATING_SYSTEM** .  

11. Clique em **OK**  

12. A janela **Advanced_Model** substitui a janela **v_R_System** e contém todos os objetos necessários exigidos para o modelo de relatório nas exibições **v_R_System** e **v_GS_OPERATING_SYSTEM** . Agora você pode excluir a janela **v_GS_OPERATING_SYSTEM** do Designer de Exibição de Fonte de Dados. Clique com o botão direito do mouse na barra de título da janela **v_GS_OPERATING_SYSTEM** para selecionar a opção **Excluir Tabela de DSV**. Na caixa de diálogo **Excluir Objetos** , clique em **OK** para confirmar a exclusão.  

13. Clique em **Arquivo**e em **Salvar Tudo**.  

#### <a name="to-create-the-report-model"></a>To create the report model  

1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Modelos de Relatório** para selecionar **Adicionar Novo Modelo de Relatório**.  

2.  Na página **Bem-vindo ao Assistente de Modelos de Relatório** , clique em **Próximo**.  

3.  Na página **Selecionar Exibição da Fonte de Dados** , selecione a exibição da fonte de dados na lista **Exibições da fonte de dados disponíveis** e clique em **Próximo**. Para esse exemplo, selecione **Simple_Model.dsv**.  

4.  Na página **Selecione as regras de geração automática do modelo de relatório** , não altere os valores padrão e clique em **Próximo**.  

5.  Na página **Coletar Estatísticas do Modelo** , verifique se a opção **Atualizar as estatísticas do modelo antes da geração automática** está selecionada e clique em **Próximo**.  

6.  Na página **Concluindo o Assistente** , especifique um nome para o modelo de relatório. Para esse exemplo, verifique se **Advanced_Model** é exibida.  

7.  Para concluir o assistente e criar o modelo de relatório, clique em **Executar**.  

8.  Para sair do assistente, clique em **Concluir**.  

9. O modelo de relatório é mostrado na janela Design.  

#### <a name="to-modify-object-names-in-the-report-model"></a>Para modificar nomes de objeto no modelo de relatório  

1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em um modelo de relatório para selecionar **Designer de Exibição**. Para esse exemplo, selecione **Advanced_Model.smdl**.  

2.  Na exibição do design do modelo de relatório, clique com o botão direito do mouse em qualquer nome de objeto para selecionar **Renomear**.  

3.  Digite um novo nome para o objeto selecionado e pressione Enter. Por exemplo, você pode renomear o objeto **CSD_Version_0** para que passe a ser **Versão do Service Pack do Windows**.  

4.  Quando terminar de renomear objetos, clique em **Arquivo**e em **Salvar Tudo**.  

#### <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a>To publish the report model for use in SQL Server Reporting Services  

1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Advanced_Model.smdl** para selecionar **Implantar**.  

2.  Examine o status da implantação no canto inferior esquerdo da janela do **SQL Server Business Intelligence Development Studio** . Quando a implantação for concluída, a mensagem **Implantação bem-sucedida** será exibida. Se a implantação falhar, o motivo da falha será exibido na janela **Saída** . O novo modelo de relatório estará disponível no seu site do SQL Server Reporting Services.  

3.  Clique em **Arquivo**, **Salvar Tudo**e feche o **SQL Server Business Intelligence Development Studio**.  

#### <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a>To deploy the custom report model to Configuration Manager  

1.  Localize a pasta na qual você criou o projeto de modelo de relatório. Por exemplo, %*USERPROFILE*%\Documentos\Visual Studio 2008\Projetos\\*&lt;Nome do Projeto\>.*  

2.  Copie os seguintes arquivos da pasta do projeto de modelo de relatório para uma pasta temporária em seu computador:  

    -   *&lt;Nome do Modelo\>* **.dsv**  

    -   *&lt;Nome do Modelo\>* **.smdl**  

3.  Abra os arquivos acima usando um editor de texto, como o Bloco de Notas.  

4.  No arquivo *&lt;Nome do Modelo\>***.dsv**, localize a primeira linha do arquivo, que é a seguinte:  

     **&lt;DataSourceView xmlns="http://schemas.microsoft.com/analysisservices/2003/engine"\>**  

     Edite essa linha da seguinte forma:  

     **&lt;DataSourceView xmlns="http://schemas.microsoft.com/analysisservices/2003/engine" xmlns:xsi="RelationalDataSourceView"\>**  

5.  Copie todo o conteúdo do arquivo na área de transferência do Windows.  

6.  Feche o arquivo *&lt;Nome do Modelo\>***.dsv**.  

7.  No arquivo *&lt;Nome do Modelo\>***.smdl**, localize as três últimas linhas do arquivo, que aparecem da seguinte maneira:  

     `</Entity>`  

     `</Entities>`  

     `</SemanticModel>`  

8.  Cole o conteúdo do arquivo *&lt;Nome do Modelo\>***.dsv** diretamente antes da última linha do arquivo (**&lt;SemanticModel\>**).  

9. Salve e feche o arquivo *&lt;Nome do Modelo\>***.smdl**.  

10. Copie o arquivo *&lt;Nome do Modelo\>***.smdl** para a pasta *%programfiles%*\Microsoft Configuration Manager\AdminConsole\XmlStorage\Other no servidor do site do Configuration Manager.  

    > [!IMPORTANT]  
    >  Depois de copiar o arquivo do modelo de relatório para o servidor do site do Configuration Manager, saia e reinicie o console do Configuration Manager antes de usar o modelo de relatório no **Assistente para Criar Relatório**.  



<!--HONumber=Nov16_HO1-->


