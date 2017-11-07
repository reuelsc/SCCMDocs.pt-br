---
title: "Operações e manutenção para relatórios "
titleSuffix: Configuration Manager
description: "Conheça os detalhes de gerenciar relatórios e assinaturas de relatório no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
caps.latest.revision: "5"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 05a81cdfd46ba2bf0bea17b06bd72f79296b3930
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="operations-and-maintenance-for-reporting-in-system-center-configuration-manager"></a>Operações e manutenção para relatórios no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Após implantar a infraestrutura para geração de relatórios no System Center Configuration Manager, haverá diversas operações que você poderá realizar para gerenciar relatórios e assinaturas de relatório.  

##  <a name="BKMK_ManageReports"></a> Gerenciar relatórios do Configuration Manager  
 O Configuration Manager oferece mais de 400 relatórios predefinidos que o ajudarão a coletar, organizar e apresentar informações sobre usuários, inventário de hardware e software, atualizações de software, aplicativos, status do site e outras operações do Configuration Manager na sua organização. Você pode usar os relatórios predefinidos como estão ou modificar um relatório para que atenda às suas necessidades. Você também pode criar relatórios baseados em SQL e em modelos personalizados para atender às suas necessidades. Use as seções a seguir para ajudá-lo a gerenciar os relatórios do Configuration Manager.  

###  <a name="BKMK_RunReport"></a> Executar um relatório do Configuration Manager  
 Relatórios no Configuration Manager são armazenados no SQL Server Reporting Services e os dados renderizados no relatório são recuperados do banco de dados de site do Configuration Manager. Você pode acessar relatórios no console do Configuration Manager ou usando o Gerenciador de relatórios, acessar em um navegador da web. Você pode abrir relatórios em qualquer computador que tenha acesso ao computador que está executando o SQL Server Reporting Services, e é necessário ter direitos suficientes para exibir os relatórios. Ao executar um relatório, o título, a descrição e a categoria do mesmo são exibidos no idioma do sistema operacional local.  

> [!NOTE]  
>  Em alguns idiomas diferentes do inglês, os caracteres podem não aparecer corretamente nos relatórios.  Nesse caso, os relatórios podem ser exibidos usando o Report Manager baseado na Web ou o Console do Administrador Remoto.  

> [!WARNING]  
>  Para executar relatórios, é necessário ter direitos de **Leitura** para a permissão **Site** e a permissão **Executar Relatório** configuradas para objetos específicos.  

> [!IMPORTANT]    
> Deve haver uma relação de confiança bidirecional estabelecida para usuários de um domínio diferente do que a conta do ponto do Reporting Services para executar com sucesso os relatórios.

> [!NOTE]  
>  O Report Manager é uma ferramenta de gerenciamento e acesso a relatórios baseada na Web que é usada para administrar uma única instância do servidor de relatório em um local remoto por meio de uma conexão HTTP. Você pode usar o Report Manager para realizar tarefas operacionais como, por exemplo, exibir relatórios, modificar propriedades de relatórios e gerenciar assinaturas de relatório associadas. Este tópico oferece as etapas para exibir um relatório e modificar propriedades de relatórios no Report Manager. Para obter mais informações sobre as outras opções oferecidas pelo Report Manager, consulte [Report Manager](http://go.microsoft.com/fwlink/p/?LinkId=224916) nos Manuais Online do SQL Server 2008.  

 Use os procedimentos a seguir para executar um relatório do Configuration Manager.  

##### <a name="to-run-a-report-in-the-configuration-manager-console"></a>Para executar um relatório no console do Configuration Manager  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Relatórios**e clique em **Relatórios** na lista de relatórios disponíveis.  

    > [!IMPORTANT]  
    >  Nesta versão do Configuration Manager, os relatórios **Todo o conteúdo** exibem somente pacotes, e não aplicativos.  

    > [!TIP]  
    >  Se não houver relatórios listados, verifique se que o ponto do Reporting Services está instalado e configurado. Para mais informações, consulte [Configuração de relatórios](configuring-reporting.md).  

3.  Selecione o relatório que deseja executar, e na guia **Início** , na seção **Grupo de Relatórios** , clique em **Executar** para abrir o relatório.  

4.  Quando houver parâmetros obrigatórios, especifique-os e clique em **Exibir Relatório**.  

#### <a name="to-run-a-report-in-a-web-browser"></a>Para executar um relatório em um navegador da Web  

1.  No navegador da Web, insira a URL do Report Manager, por exemplo, **http:\/\/Server1\/Reports**. Você pode determinar a URL do Gerenciador de relatórios no **URL do Gerenciador de relatórios** página no Reporting Services Configuration Manager.  

2.  No Report Manager, clique na pasta de relatórios do Configuration Manager, por exemplo, **ConfigMgr\_CAS**.  

    > [!TIP]  
    >  Se não houver relatórios listados, verifique se que o ponto do Reporting Services está instalado e configurado. Para mais informações, consulte [Configuração de relatórios](configuring-reporting.md).  

3.  Clique na categoria do relatório que deseja executar e no link do relatório. O relatório será aberto no Report Manager.  

4.  Quando houver parâmetros obrigatórios, especifique-os e clique em **Exibir Relatório**.  

###  <a name="BKMK_ModifyReportProperties"></a> Modificar as propriedades de um relatório do Configuration Manager  
 No console do Configuration Manager, é possível exibir as propriedades de um relatório, como o seu nome e a sua descrição, mas para alterar suas propriedades, use o Report Manager. Use o procedimento a seguir para modificar as propriedades de um relatório do Configuration Manager.  

#### <a name="to-modify-report-properties-in-report-manager"></a>Para modificar as propriedades de um relatório no Report Manager  

1.  No navegador da Web, insira a URL do Report Manager, por exemplo, **http:\/\/Server1\/Reports**. Você pode determinar a URL do Gerenciador de relatórios no **URL do Gerenciador de relatórios** página no Reporting Services Configuration Manager.  

2.  No Report Manager, clique na pasta de relatórios do Configuration Manager, por exemplo, **ConfigMgr\_CAS**.  

    > [!TIP]  
    >  Se não houver relatórios listados, verifique se que o ponto do Reporting Services está instalado e configurado. Para mais informações, consulte [Configuração de relatórios](configuring-reporting.md)  

3.  Clique na categoria do relatório do qual deseja modificar as propriedades e clique no link do relatório. O relatório será aberto no Report Manager.  

4.  Clique na guia **Propriedades** . Você pode modificar o nome e a descrição do relatório.  

5.  Ao terminar, clique em **aplicar**. As propriedades do relatório serão salvas no servidor de relatório e o console do Configuration Manager vai recuperar as propriedades do relatório atualizado para o relatório.  

###  <a name="BKMK_EditReport"></a> Editar um relatório do Configuration Manager  
 Quando um relatório existente do Configuration Manager não recuperar as informações necessárias ou não fornecer o layout ou o design desejado, você poderá editar o relatório no Construtor de Relatórios.  

> [!NOTE]  
>  É possível optar por clonar um relatório existente ao abri-lo para edição ou clicar em **Salvar como** para salvá-lo como um novo relatório.  

> [!IMPORTANT]  
>  A conta do usuário deve ter a permissão **Modificar do site** e a permissão **Modificar Relatório** dos objetos específicos associados ao relatório que você deseja modificar.  

> [!IMPORTANT]  
>  Quando o Configuration Manager é atualizado para uma versão mais recente, os relatórios predefinidos são substituídos por novos relatórios. Se você modificar um relatório predefinido, será necessário fazer backup do relatório antes de instalar a nova versão, e depois restaurar o relatório no Reporting Services. Se você estiver fazendo alterações significativas em um relatório predefinido, considere criar um novo relatório, em vez disso. Os novos relatórios criados antes da atualização de um site não serão substituídos.  

 Use o procedimento a seguir para editar as propriedades de um relatório do Configuration Manager.  

#### <a name="to-edit-report-properties"></a>Para editar as propriedades de um relatório  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Relatórios**e clique em **Relatórios** na lista de relatórios disponíveis.  

3.  Selecione o relatório que deseja modificar e na guia **Início** , na seção **Grupo de Relatórios** , clique em **Editar**. Especifique a sua conta e senha de usuário, se necessário, e clique em **OK**. Se o Construtor de Relatórios não estiver instalado no computador, será necessário instalá-lo. Clique em **Executar** para instalar o Construtor de Relatórios, o qual é necessário para modificar e criar relatórios.  

4.  No Construtor de Relatórios, modifique as configurações apropriadas do relatório e clique em **Salvar** para salvar o relatório no servidor de relatório.  

###  <a name="BKMK_CreateModelBasedReport"></a> Criar um relatório baseado em um modelo  
 Um relatório baseado em modelo permite selecionar de modo interativo os itens que você deseja incluir no relatório. Para obter mais informações sobre a criação de modelos de relatório, veja [Criando modelos de relatório personalizados para o System Center Configuration Manager no SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).  

> [!IMPORTANT]  
>  A conta do usuário deve ter a permissão **Modificar do site** para criar um novo relatório. O usuário só poderá criar um relatório nas pastas para as quais tenha permissões para **Modificar Relatório** .  

 Use o procedimento a seguir para criar um relatório do Configuration Manager baseado em modelo.  

#### <a name="to-create-a-model-based-report"></a>Para criar um relatório baseado em modelo  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Relatórios** e clique em **Relatórios**.  

3.  Na guia **Início** , na seção **Criar** , clique em **Criar Relatório** para abrir o **Assistente para Criar Relatório**.  

4.  Na página **Informações** , defina as seguintes configurações:  

    -   **Tipo:** Selecione **Relatório baseado em modelo** para criar um relatório no Construtor de Relatórios usando um modelo do Reporting Services.  

    -   **Nome**: Especifique um nome para o relatório.  

    -   **Descrição**: Especifique uma descrição para o relatório.  

    -   **Servidor**: Exibe o nome do servidor de relatório no qual você está criando o relatório.  

    -   **Caminho**: Clique em **Procurar** para especificar uma pasta na qual você deseja armazenar o relatório.  

     Clique em **Avançar**.  

5.  Na página **Seleção de Modelo** , selecione um modelo disponível na lista usada para criar o relatório. Ao selecionar o modelo de relatório, a seção **Visualização** mostra as exibições e as entidades do SQL Server disponibilizadas pelo modelo de relatório selecionado.  

6.  Na página de **Resumo** , analise as configurações. Clique em **Anterior** para alterar as configurações ou clique em **Próximo** para criar o relatório no Configuration Manager.  

7.  Na página **Confirmação** , clique em **Fechar** para sair do assistente, depois, abra o Construtor de Relatórios para definir as configurações do relatório. Especifique a sua conta e senha de usuário, se necessário, e clique em **OK**. Se o Construtor de Relatórios não estiver instalado no computador, será necessário instalá-lo. Clique em **Executar** para instalar o Construtor de Relatórios, o qual é necessário para modificar e criar relatórios.  

8.  No Construtor de Relatórios, crie o layout do relatório, selecione os dados nas exibições disponíveis do SQL Server, adicione os parâmetros no relatório e assim por diante. Para obter mais informações sobre como usar o Construtor de Relatórios para criar um novo relatório, consulte a Ajuda do Construtor de Relatórios.  

9. Clique em **Executar** para executar o relatório. Verifique se o relatório contém as informações desejadas. Clique em **Design** para retornar à exibição Design e modificar o relatório, se necessário.  

10. Clique em **Salvar** para salvar o relatório no servidor de relatório. Você pode executar e modificar o novo relatório no nó **Relatórios** do espaço de trabalho **Monitoramento** .  

###  <a name="BKMK_CreateSQLBasedReport"></a> Criar um relatório baseado em SQL  
 Um relatório baseado em SQL permite recuperar dados baseados em uma instrução SQL do relatório.  

> [!IMPORTANT]  
>  Ao criar uma instrução SQL para um relatório personalizado, não faça referência diretamente a tabelas do SQL Server. Em vez disso, faça referência às exibições do relatório do SQL Server \(nomes de exibições que comecem com v\_\) no banco de dados do site. Você também pode fazer referência a procedimentos armazenados públicos \(nomes de procedimentos armazenados que comecem com sp\_\) no banco de dados do site.  

> [!IMPORTANT]  
>  A conta do usuário deve ter a permissão **Modificar do site** para criar um novo relatório. O usuário só poderá criar um relatório nas pastas para as quais tenha permissões para **Modificar Relatório** .  

 Use o procedimento a seguir para criar um relatório do Configuration Manager baseado em SQL.  

#### <a name="to-create-a-sql-based-report"></a>Para criar um relatório baseado em SQL  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Relatórios**e clique em **Relatórios**.  

3.  Na guia **Início** , na seção **Criar** , clique em **Criar Relatório** para abrir o **Assistente para Criar Relatório**.  

4.  Na página **Informações** , defina as seguintes configurações:  

    -   **Tipo**: Selecione **Relatório baseado em SQL** para criar um relatório no Construtor de Relatórios usando uma instrução SQL.  

    -   **Nome**: Especifique um nome para o relatório.  

    -   **Descrição**: Especifique uma descrição para o relatório.  

    -   **Servidor**: Exibe o nome do servidor de relatório no qual você está criando o relatório.  

    -   **Caminho**: Clique em **Procurar** para especificar uma pasta na qual você deseja armazenar o relatório.  

     Clique em **Avançar**.  

5.  Na página de **Resumo** , analise as configurações. Clique em **Anterior** para alterar as configurações ou clique em **Próximo** para criar o relatório no Configuration Manager.  

6.  Na página **Confirmação** , clique em **Fechar** para sair do assistente, e abra o Construtor de Relatórios para definir as configurações do relatório. Especifique a sua conta e senha de usuário, se necessário, e clique em **OK**. Se o Construtor de Relatórios não estiver instalado no computador, será necessário instalá-lo. Clique em **Executar** para instalar o Construtor de Relatórios, o qual é necessário para modificar e criar relatórios.  

7.  No Construtor de Relatórios da Microsoft, especifique a instrução SQL para o relatório ou crie a mesma usando as colunas nas exibições disponíveis do SQL Server, adicione os parâmetros no relatório e assim por diante.  

8.  Clique em **Executar** para executar o relatório. Verifique se o relatório contém as informações desejadas. Clique em **Design** para retornar à exibição Design e modificar o relatório, se necessário.  

9. Clique em **Salvar** para salvar o relatório no servidor de relatório. Você pode executar o novo relatório no nó **Relatórios** do espaço de trabalho **Monitoramento** .  

##  <a name="BKMK_ManageReportSubscriptions"></a> Gerenciar assinaturas de relatório  
 As assinaturas de relatório no SQL Server Reporting Services permitem que você configure a entrega automática de relatórios especificados por email ou para um compartilhamento de arquivos em intervalos agendados. Use o **Assistente para Criar Assinatura** no System Center 2012 Configuration Manager para configurar assinaturas de relatório.  

###  <a name="BKMK_ReportSubscriptionFileShare"></a> Criar uma assinatura de relatório para entregar um relatório a um compartilhamento de arquivo  
 Quando você cria uma assinatura de relatório para entregá-lo a um compartilhamento de arquivo, o relatório é copiado no formato definido para o compartilhamento especificado. Você pode se inscrever e solicitar a entrega de apenas um relatório de cada vez.  

 Diferentemente dos relatórios hospedados e gerenciados por um servidor de relatório, os relatórios entregues a uma pasta de compartilhamento são arquivos estáticos. Os recursos interativos definidos para o relatório não funcionam para relatórios armazenados como arquivos no sistema de arquivos. Recursos de interação são representados como elementos estáticos. Se o relatório incluir gráficos, a apresentação padrão será usada. Se o relatório apresenta vínculo com outro relatório, o link é processado como texto estático. Se você deseja manter os recursos interativos em um relatório entregue, use a entrega de email. Para obter mais informações sobre a entrega de email, veja a seção [Criar uma assinatura de relatório para entregar um relatório por email](#BKMK_ReportSubscriptionEmail) mais adiante neste tópico.  

 Ao criar uma assinatura que utiliza a entrega de compartilhamento de arquivos, especifique uma pasta existente como a pasta de destino. O servidor de relatório não cria pastas no sistema de arquivos. A pasta especificada deve ser acessível através de uma conexão de rede. Ao especificar a pasta de destino em uma assinatura, use um caminho UNC e não inclua barras invertidas no caminho da pasta. Por exemplo, um caminho UNC válido para a pasta de destino é: \\\\&lt;nomedoservidor\>\\reportfiles\\operations\\2011.  

 Os relatórios podem ser processados em uma variedade de formatos de arquivo, como MHTML ou Excel. Para salvar o relatório em um formato de arquivo específico, selecione esse formato de renderização ao criar sua assinatura. Por exemplo, escolher o Excel salva o relatório como um arquivo do Microsoft Excel. Embora você possa selecionar qualquer formato de renderização com suporte, alguns formatos funcionam melhor do que outros na renderização de um arquivo.  

 Use o procedimento a seguir para criar uma assinatura de relatório para entregar um relatório a um compartilhamento de arquivo.  

#### <a name="to-create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a>Para criar uma assinatura de relatório para entregar um relatório a um compartilhamento de arquivo  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Gerando Relatórios** e clique em **Relatórios** para listar os relatórios disponíveis. Você pode selecionar uma pasta de relatório para listar somente os relatórios associados à pasta.  

3.  Selecione o relatório que deseja adicionar à assinatura, e na guia **Início** , na seção **Grupo de Relatórios** , clique em **Criar Inscrição** para abrir o **Assistente para Criar Assinatura**.  

4.  Na página **Entrega de Assinatura** , defina as seguintes configurações:  

    -   Relatório entregue por: Selecione **Compartilhamento de Arquivo do Windows** para entregar o relatório a um compartilhamento de arquivos.  

    -   **Nome do Arquivo**: Especifique o nome do arquivo para o relatório. Por padrão, o arquivo de relatório não inclui uma extensão de nome de arquivo. Selecione **Adicionar extensão de arquivo quando criada** para adicionar automaticamente uma extensão de nome de arquivo a esse relatório com base no formato de renderização.  

    -   **Caminho**: especifique um caminho UNC para uma pasta existente para a qual você deseja enviar este relatório \(por exemplo, \\\\&lt;nome do servidor\>\\&lt;compartilhamento do servidor\>\\&lt;pasta do relatório\>\).  

        > [!NOTE]  
        >  O nome de usuário especificado posteriormente nesta página deve ter acesso a esse compartilhamento de servidor e ter permissões de gravação na pasta de destino.  

    -   **Renderizar Formato**: Selecione um dos seguintes formatos do arquivo de relatório:  

        -   **Arquivo XML com dados de relatório**: Salva o relatório no formato de linguagem XML.  

        -   **CSV \(delimitado por vírgula\)**: Salva o relatório no formato de valores separados por vírgula.  

        -   **Arquivo TIFF**: Salva o relatório no formato TIFF.  

        -   **Arquivo do Acrobat \(PDF\)**: Salva o relatório no formato PDF do Acrobat.  

        -   **HTML 4.0**: Salva o relatório como uma página da Web visível apenas em navegadores que oferecem suporte a HTML 4.0. O Internet Explorer 5 e as versões posteriores oferecem suporte a HTML 4.0.  

            > [!NOTE]  
            >  Se houver imagens em seu relatório, o formato HTML 4.0 não irá incluí-las no arquivo.  

        -   **MHTML \(arquivo Web\)**: Salva o relatório no formato MIME HTML \(mhtml\), que é visível em muitos navegadores da Web.  

        -   **Processador RPL**: Salva o relatório no formato RPL \(Report Page Layout\).  

        -   **Excel**: Salva o relatório como uma planilha do Microsoft Excel.  

        -   **Word**: Salva o relatório como um documento do Microsoft Word.  

    -   **Nome de usuário**: Especifique uma conta de usuário do Windows com permissões para acessar o compartilhamento do servidor de destino e a pasta. A conta de usuário deve ter acesso a esse compartilhamento de servidor e ter permissão de gravação na pasta de destino.  

    -   **Senha**: Especifique a senha para a conta de usuário do Windows. Em **Confirmar Senha**, insira a senha novamente.  

    -   Selecione uma das seguintes opções para configurar o comportamento quando um arquivo com o mesmo nome existe na pasta de destino:  

        -   **Substituir um arquivo existente por uma versão mais nova**: Especifica que, quando o arquivo de relatório já existe, a nova versão o substitui.  

        -   **Não substituir um arquivo existente**: Especifica que, quando o arquivo de relatório já existe, nenhuma ação ocorre.  

        -   **Incrementar nomes de arquivo à medida que versões mais novas forem adicionadas**: Especifica que, quando o arquivo de relatório já existe, um número é adicionado ao novo relatório para o nome de arquivo distingui-lo de outras versões.  

    -   **Descrição**: Especifica a descrição para a assinatura de relatório.  

     Clique em **Avançar**.  

5.  Na página **Agendamento da Assinatura** , selecione uma das seguintes opções de agendamento de entrega para a assinatura do relatório:  

    -   **Usar agendamento compartilhado**: Um agendamento compartilhado é um agendamento previamente definido que pode ser usado por outras assinaturas de relatório. Marque essa caixa de seleção e selecione um agendamento compartilhado na lista, se algum tiver sido especificado.  

    -   **Criar novo agendamento**: Configure o agendamento no qual é executado esse relatório, incluindo o intervalo, a data e a hora de início e a data de término para essa assinatura.  

6.  Na página **Parâmetros de Assinatura** , especifique os parâmetros usados para esse relatório quando ele é executado de forma autônoma. Quando não existem parâmetros para o relatório, essa página não é exibida.  

7.  Na página **Resumo** , revise as configurações de assinatura de relatório. Clique em **Anterior** para alterar as configurações ou clique em **Próxima** para criar a assinatura do relatório.  

8.  Na página **Conclusão** , clique em **Fechar** para sair do assistente. Verifique se a assinatura do relatório foi criada com êxito. É possível exibir e modificar as assinaturas de relatório no nó **Assinaturas** sob **Gerando Relatórios** no espaço de trabalho **Monitoramento** .  

###  <a name="BKMK_ReportSubscriptionEmail"></a> Criar uma assinatura de relatório para entregar um relatório por email  
 Quando você cria uma assinatura de relatório para entregar um relatório por email, um email é enviado aos destinatários que você configurar, e o relatório é incluído como um anexo. O servidor de relatório não valida endereços de email ou os obtém a partir de um servidor de email. Você precisa saber com antecedência quais endereços de email deseja usar. Por padrão, é possível enviar por email relatórios a qualquer conta de email válida, dentro ou fora de sua organização. Você pode selecionar uma ou ambas as opções de entrega de email a seguir:  

-   Enviar uma notificação e um hiperlink para o relatório gerado.  

-   Enviar um relatório anexado ou inserido. O formato de renderização e o navegador determinam se o relatório é inserido ou anexado. Se seu navegador der suporte para HTML 4.0 e MHTML e se for possível selecionar o formato de renderização MHTML \(arquivo Web\), o relatório será inserido como parte da mensagem. Todos os outros formatos de renderização \(CSV, PDF, Word e assim por diante\) entregam os relatórios como anexos. O Reporting Services não verifica o tamanho do anexo ou da mensagem antes de enviar o relatório. Se o anexo ou a mensagem exceder o limite máximo permitido por seu servidor de email, o relatório não será entregue.  

> [!IMPORTANT]  
>  Você deve definir as configurações de email no Reporting Services para a opção de entrega **Email** ficar disponível. Para obter mais informações sobre como definir as configurações de email no Reporting Services, consulte [Configurando um servidor de relatório para entrega de email](http://go.microsoft.com/fwlink/p/?LinkId=226668) nos Manuais Online do SQL Server.  

 Use o procedimento a seguir para criar uma assinatura de relatório para entregar um relatório por email.  

#### <a name="to-create-a-report-subscription-to-deliver-a-report-by-email"></a>Para criar uma assinatura de relatório para entregar um relatório por email  

-   No console do Configuration Manager, clique em **Monitoramento**.  

-   No espaço de trabalho **Monitoramento** , expanda **Gerando Relatórios** e clique em **Relatórios** para listar os relatórios disponíveis. Você pode selecionar uma pasta de relatório para listar somente os relatórios associados à pasta.  

-   Selecione o relatório que deseja adicionar à assinatura, e na guia **Início** , na seção **Grupo de Relatórios** , clique em **Criar Inscrição** para abrir o **Assistente para Criar Assinatura**.  

-   Na página **Entrega de Assinatura** , defina as seguintes configurações:  

    -   **Relatório entregue por**: Selecione **Email** para entregar o relatório como um anexo em uma mensagem de email.  

    -   **Para**: Especifique um endereço de email válido ao qual enviar esse relatório.  

        > [!NOTE]  
        >  Você pode inserir vários destinatários de email separando cada endereço de email com ponto e vírgula.  

    -   **Cc**: Opcionalmente, especifique um endereço de email ao qual copiar esse relatório.  

    -   **Cco**: Opcionalmente, especifique um endereço de email ao qual enviar uma cópia oculta desse relatório.  

    -   **Responder para**: Especifique o endereço de resposta a ser usado se o destinatário responder à mensagem de email.  

    -   **Assunto**: Especifique uma linha de assunto para a mensagem de email de assinatura.  

    -   **Prioridade**: Selecione o sinalizador de prioridade para essa mensagem de email. Selecione **Baixa**, **Normal**ou **Alta**. A configuração de prioridade é usada pelo Microsoft Exchange para definir um sinalizador que indica a importância da mensagem de email.  

    -   **Comentário**: Especifique o texto a ser adicionado ao corpo da mensagem de email de assinatura.  

    -   **Descrição**: Especifique a descrição para essa assinatura de relatório.  

    -   **Incluir Link**: Inclui uma URL ao relatório inscrito no corpo da mensagem de email.  

    -   **Incluir Relatório**: Especifique que o relatório é anexado à mensagem de email. O formato no qual o relatório será anexado é especificado na lista **Renderizar Formato** .  

    -   **Renderizar Formato**: Selecione um dos seguintes formatos para o relatório anexado:  

        -   **Arquivo XML com dados de relatório**: Salva o relatório no formato de linguagem XML.  

        -   **CSV \(delimitado por vírgula\)**: Salva o relatório no formato de valores separados por vírgula.  

        -   **Arquivo TIFF**: Salva o relatório no formato TIFF.  

        -   **Arquivo do Acrobat \(PDF\)**: Salva o relatório no formato PDF do Acrobat.  

        -   **MHTML \(arquivo Web\)**: Salva o relatório no formato MIME HTML \(mhtml\), que é visível em muitos navegadores da Web.  

        -   **Excel**: Salva o relatório como uma planilha do Microsoft Excel.  

        -   **Word**: Salva o relatório como um documento do Microsoft Word.  

-   Na página **Agendamento da Assinatura** , selecione uma das seguintes opções de agendamento de entrega para a assinatura do relatório:  

    -   **Usar agendamento compartilhado**: Um agendamento compartilhado é um agendamento previamente definido que pode ser usado por outras assinaturas de relatório. Marque essa caixa de seleção e selecione um agendamento compartilhado na lista, se algum tiver sido especificado.  

    -   **Criar novo agendamento**: Configure o agendamento no qual esse relatório será executado, incluindo o intervalo, a data e a hora de início e a data de término para essa assinatura.  

-   Na página **Parâmetros de Assinatura** , especifique os parâmetros usados para esse relatório quando ele é executado de forma autônoma. Quando não existem parâmetros para o relatório, essa página não é exibida.  

-   Na página **Resumo** , revise as configurações de assinatura de relatório. Clique em **Anterior** para alterar as configurações ou clique em **Próxima** para criar a assinatura do relatório.  

-   Na página **Conclusão** , clique em **Fechar** para sair do assistente. Verifique se a assinatura do relatório foi criada com êxito. É possível exibir e modificar as assinaturas de relatório no nó **Assinaturas** sob **Gerando Relatórios** no espaço de trabalho **Monitoramento** .  
