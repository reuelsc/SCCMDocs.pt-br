---
title: "Configurar relatórios | System Center Configuration Manager"
description: "Saiba como configurar relatórios em sua hierarquia do Configuration Manager, incluindo informações sobre o SQL Server Reporting Services."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
caps.latest.revision: 6
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 7c7fb75ec6be7a24afe2bb8038998fb58b10e331


---
# <a name="configuring-reporting-in-system-center-configuration-manager"></a>Configurando relatórios no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de criar, modificar e executar relatórios no console do System Center Configuration Manager, é necessário realizar algumas tarefas de configuração. Use as seguintes seções deste tópico para ajudá-lo a configurar relatórios na sua hierarquia do Configuration Manager:  

 Antes de prosseguir com a instalação e configuração do Reporting Services em sua hierarquia, veja os seguintes tópicos sobre relatórios no Configuration Manager:  

-   [Introdução à emissão de relatórios no System Center Configuration Manager](../../../core/servers/manage/introduction-to-reporting.md)  

-   [Planejamento para emissão de relatórios no System Center Configuration Manager](../../../core/servers/manage/planning-for-reporting.md)  

##  <a name="a-namebkmksqlreportingservicesa-sql-server-reporting-services"></a><a name="BKMK_SQLReportingServices"></a> SQL Server Reporting Services  
 O SQL Server Reporting Services é uma plataforma de relatórios baseada em servidor que oferece funcionalidade de relatório abrangente para uma variedade de fontes de dados. O ponto do Reporting Services no Configuration Manager se comunica com o SQL Server Reporting Services para copiar relatórios do Configuration Manager para uma pasta de relatórios específica, para definir configurações do Reporting Services, bem como definir suas configurações de segurança. O Reporting Services se conecta ao banco de dados do site do Configuration Manager para recuperar dados retornados ao executar relatórios.  

 Antes de instalar o ponto do Reporting Services em um site do Configuration Manager, você precisa instalar e configurar o SQL Server Reporting Services no sistema de sites que hospeda a função de sistema de sites do ponto do Reporting Services. Para obter informações sobre como instalar o Reporting Services, consulte a [TechNet Library do SQL Server](http://go.microsoft.com/fwlink/p/?LinkId=266389).  

 Use o procedimento a seguir para verificar o SQL Server Reporting Services está instalado e funcionando corretamente.  

#### <a name="to-verify-that-sql-server-reporting-services-is-installed-and-running"></a>Para verificar se o SQL Server Reporting Services está instalado e em execução  

1.  Na área de trabalho, clique em **Iniciar**, **Todos os Programas**, **Microsoft SQL Server 2008 R2**, **Ferramentas de Configuração**e **Gerenciador de Configuração do Reporting Services**.  

2.  Na caixa de diálogo **Conexão de Configuração do Reporting Services** , especifique o nome do servidor que está hospedando o SQL Server Reporting Services, no menu, selecione a instância do SQL Server em que o SQL Reporting Services foi instalado e clique em **Conectar**. O Gerenciador de Configuração do Reporting Services será aberto.  

3.  Na página **Status do Servidor de Relatório** , verifique se o **Status do Servidor de Relatório** está definido como **Iniciado**. Se não estiver, clique em **iniciar**.  

4.  Na página **URL de Serviço Web** , clique na URL em **URLs de Serviço Web do Report Service** para testar a conexão com a pasta de relatórios. A caixa de diálogo **Segurança do Windows** poderá abrir e solicitar credenciais de segurança. Por padrão, a conta de usuário é exibida. Digite sua senha e clique em **OK**. Verifique se a página da Web é aberta com êxito. Feche a janela do navegador.  

5.  Na página **Banco de Dados** , verifique se o **Modo do Servidor de Relatório** está configurado com **Nativo**.  

6.  Na página **URL do Gerenciador de Relatório** , clique na URL em **Identificação do Site do Gerenciador de Relatórios** para testar a conexão com o diretório virtual do Gerenciador de Relatórios. A caixa de diálogo **Segurança do Windows** poderá abrir e solicitar credenciais de segurança. Por padrão, a conta de usuário é exibida. Digite sua senha e clique em **OK**. Verifique se a página da Web é aberta com êxito. Feche a janela do navegador.  

    > [!NOTE]  
    >  O Gerenciador de Relatórios do Reporting Services não é necessário para gerar relatórios no Configuration Manager, mas será necessário se você quiser executar relatórios em um navegador da Internet ou gerenciar relatórios usando o Gerenciador de Relatórios.  

7.  Clique em **Sair** para fechar o Reporting Services Configuration Manager.  

##  <a name="a-namebkmkreportbuilder3a-configure-reporting-to-use-report-builder-30"></a><a name="BKMK_ReportBuilder3"></a> Configurar relatórios para usar o Construtor de Relatórios 3.0  

#### <a name="to-change-the-report-builder-manifest-name-to-report-builder-30"></a>Para alterar o nome manifesto do Construtor de Relatórios para Construtor de Relatórios 3.0  

1.  No computador que executa o console do Configuration Manager, abra o Editor do Registro do Windows.  

2.  Navegue até **HKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Microsoft/ConfigMgr10/AdminUI/Reporting**.  

3.  Clique duas vezes na chave **ReportBuilderApplicationManifestName** para editar os dados do valor.  

4.  Altere **ReportBuilder_2_0_0_0.application** para **ReportBuilder_3_0_0_0.application**e clique em **OK**.  

5.  Feche o Editor do Registro do Windows.  

##  <a name="a-namebkmkinstallreportingservicespointa-install-a-reporting-services-point"></a><a name="BKMK_InstallReportingServicesPoint"></a> Instalar um ponto do Reporting Services  
 O ponto do Reporting Services deve ser instalado em um site para gerenciar relatórios no site. O ponto do Reporting Services copia pastas de relatórios e relatórios no SQL Server Reporting Services, aplica a política de segurança nos relatórios e pastas e define as configurações no Reporting Services. É necessário configurar um ponto do Reporting Services antes que os relatórios sejam exibidos no console do Configuration Manager e antes de gerenciar os relatórios no Configuration Manager. O ponto do Reporting Services é uma função do sistema de site que deve ser configurada em um servidor com o Microsoft SQL Server Reporting Services instalado e em execução. Para obter mais informações sobre os pré-requisitos, consulte [Pré-requisitos para relatórios](prerequisites-for-reporting.md).  

> [!IMPORTANT]  
>  Ao selecionar um site para instalar o ponto do Reporting Services, é importante lembrar que os usuários que acessarão os relatórios devem estar no mesmo escopo de segurança do site onde o ponto do Reporting Services está instalado.  

> [!IMPORTANT]  
>  Após instalar um ponto do Reporting Services em um sistema de site, não altere a URL do servidor de relatório. Por exemplo, se você criar o ponto do Reporting Services e, no Reporting Services Configuration Manager, modificar a URL do servidor de relatório, o console do Configuration Manager continuará usando a URL antiga e você não poderá executar, editar nem criar relatórios por meio do console. Quando você tiver que alterar o servidor de relatório da URL, remova o ponto do Reporting Services, altere a URL e reinstale o ponto do Reporting Services.  

 Use o procedimento a seguir para instalar o ponto do Reporting Services.  

#### <a name="to-install-the-reporting-services-point-on-a-site-system"></a>Para instalar o ponto do Reporting Services em um sistema de site  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Configuração de Site**e clique em **Funções de Servidores e Sistema de Site**.  

    > [!TIP]  
    >  Para listar somente sistemas de site que hospedam a função do site do ponto do Reporting Services, clique com o botão direito do mouse em **Funções de Servidores e Sistema de Site** para selecionar o **Ponto do Reporting Services**.  

3.  Adicione a função do sistema de site do ponto do Reporting Services a um servidor de sistema de site novo ou existente usando a etapa associada:  

    > [!NOTE]  
    >  Para obter mais informações sobre como configurar sistemas de sites, consulte [Adicionar funções do sistema de sites ao System Center Configuration Manager](../deploy/configure/add-site-system-roles.md).  

    -   **Novo sistema de sites**: na guia **Início** , no grupo **Criar** , clique em **Criar Servidor do Sistema de Sites**. O **Assistente para Criar Servidor do Sistema de Site** será aberto.  

    -   **Sistema de sites existente**: clique no servidor no qual deseja instalar a função do sistema de sites do ponto do Reporting Services. Ao clicar em um servidor, uma lista das funções do sistema de site que já estão instaladas no servidor será exibida no painel de resultados.  

         Na guia **Início** , no grupo **Servidor** , clique em **Adicionar Função do Sistema de Site**. O **Assistente para Adicionar Funções do Sistema de Site** será aberto.  

4.  Na página **Geral** , especifique as configurações gerais para o servidor do sistema de site. Ao adicionar o ponto do Reporting Services em um servidor de sistema de site existente, verifique os valores previamente configurados.  

5.  Na página **Seleção de Função do Sistema** , selecione **Ponto do Reporting Services** , na lista de funções disponíveis e clique em **Próximo**.  

6.  Na página **Ponto do Reporting Services** , defina as seguintes configurações:  

    -   **Nome do servidor de banco de dados do site**: especifique o nome do servidor que hospeda o banco de dados do site do Configuration Manager. Geralmente, o assistente automaticamente recupera o FQDN (nome de domínio totalmente qualificado) do servidor. Para especificar uma instância do banco de dados, use o formato &lt;*Nome do Servidor*>\&lt;*Nome da Instância*>.  

    -   **Nome do banco de dados**: especifique o nome do banco de dados do Configuration Manager e clique em **Verificar** para confirmar se o assistente tem acesso ao banco de dados do site.  

        > [!IMPORTANT]  
        >  A conta de usuário que está criando o ponto do Reporting Services deve ter acesso de **Leitura** ao banco de dados do site. Se o teste de conexão falhar, será exibido um ícone de aviso vermelho. Mova o cursor sobre esse ícone para ler os detalhes da falha. Corrija a falha e clique em **Testar** novamente.  

    -   **Nome da pasta**: especifique o nome da pasta criada e usada para hospedar os relatórios do Configuration Manager no Reporting Services.  

    -   **Instância do servidor do Reporting Services**: selecione na lista a instância do SQL Server para o Reporting Services. Quando apenas uma instância for encontrada, por padrão, ela será listada e selecionada. Quando nenhuma instância for encontrada, verifique se o SQL Server Reporting Services está instalado e configurado e se o serviço do SQL Server Reporting Services foi iniciado no sistema.  

        > [!IMPORTANT]  
        >  O Configuration Manager faz uma conexão no contexto do usuário atual à WMI (Instrumentação de Gerenciamento do Windows) do sistema de sites selecionado para recuperar a instância do SQL Server para o Reporting Services. O usuário atual deve ter acesso de **Leitura** à WMI do sistema de site ou as instâncias do Reporting Services não poderão ser recuperadas.  

    -   **Conta do ponto do Reporting Services**: clique em **Definir** e selecione uma conta a ser usada quando o SQL Server Reporting Services no ponto do Reporting Services se conectar ao banco de dados do site do Configuration Manager para recuperar os dados exibidos em um relatório. Selecione **Conta existente** para especificar uma conta de usuário do Windows que tenha sido configurada anteriormente como uma conta do Configuration Manager, ou selecione **Nova conta** para especificar uma conta de usuário do Windows que não esteja configurada como uma conta do Configuration Manager. O Configuration Manager concede automaticamente o acesso do usuário especificado ao banco de dados do site. O usuário será exibido na subpasta **Contas** do nó **Segurança** no espaço de trabalho **Administração** com o nome de conta **Ponto do Reporting Services do ConfigMgr** .  

         A conta que executa o Reporting Services deve pertencer ao grupo de segurança local de domínio **Grupo de Acesso de Autorização do Windows**e ter a permissão **Ler tokenGroupsGlobalAndUniversal** configurada como **Permitir**.  

         A conta de usuário e a senha especificadas do Windows serão criptografadas e armazenadas no banco de dados do Reporting Services. O Reporting Services recupera os dados para os relatórios a partir do banco de dados do site usando essa conta e senha.  

        > [!IMPORTANT]  
        >  A conta especificada deve ter permissões de **Logon Localmente** no computador que hospeda o banco de dados do Reporting Services.  

7.  Na página **Ponto do Reporting Services** , clique em **Próximo**.  

8.  Na página **Resumo** , verifique as configurações e clique em **Próximo** para instalar o ponto do Reporting Services.  

     Após o assistente ser concluído, as pastas de relatórios serão criadas e os relatórios do Configuration Manager serão copiados para as pastas de relatórios especificadas.  

    > [!NOTE]  
    >  Quando as pastas de relatórios forem criadas e os relatórios forem copiados para o servidor de relatórios, o Configuration Manager determinará o idioma apropriado para os objetos. Se o pacote do idioma associado estiver instalado no site, o Configuration Manager criará os objetos no mesmo idioma em que o sistema operacional em execução no servidor de relatórios do site. Se o idioma não estiver disponível, os relatórios serão criados e exibidos em inglês. Ao instalar um ponto do Reporting Services em um site sem pacotes de idiomas, os relatórios são instalados em inglês. Se você instalar um pacote de idiomas após instalar o ponto do Reporting Services, será necessário desinstalar e reinstalar o ponto do Reporting Services para que os relatórios fiquem disponíveis no idioma do pacote de idiomas apropriado. Para obter mais informações sobre pacotes de idiomas, consulte [Pacotes de idiomas no System Center Configuration Manager](../deploy/install/language-packs.md).  

###  <a name="a-namebkmkfileinstallationandsecuritya-file-installation-and-report-folder-security-rights"></a><a name="BKMK_FileInstallationAndSecurity"></a> Instalação de arquivos e direitos de segurança da pasta de relatórios  
 O Configuration Manager realiza as seguintes ações para instalar o ponto do Reporting Services e configurar o Reporting Services:  

> [!IMPORTANT]  
>  As ações na lista a seguir são executadas usando as credenciais da conta configurada para o serviço SMS_Executive, que geralmente é a conta Sistema Local do servidor do site.  

-   Instala a função do site do ponto do Reporting Services.  

-   Cria a fonte de dados no Reporting Services com as credenciais armazenadas que você especificou no assistente. Essa é a conta de usuário e a senha do Windows que o Reporting Services usa para se conectar ao banco de dados do site quando você executa relatórios.  

-   Cria a pasta raiz do Configuration Manager no Reporting Services.  

-   Adiciona as funções de segurança **Usuários de Relatório do ConfigMgr** e **Administradores de Relatório do ConfigMgr** no Reporting Services.  

-   Cria subpastas e implanta relatórios do Configuration Manager por meio de %ProgramFiles%\SMS_SRSRP no Reporting Services.  

-   Adiciona a função **Usuários de Relatório do ConfigMgr** do Reporting Services às pastas raiz de todas as contas de usuários do Configuration Manager que têm direitos de **Leitura do Site**.  

-   Adiciona a função **Usuários de Relatório do ConfigMgr** do Reporting Services às pastas raiz de todas as contas de usuários do Configuration Manager que têm direitos de **Modificar o Site**.  

-   Recupera o mapeamento entre as pastas de relatórios e os tipos de objetos protegidos do Configuration Manager (mantidos no banco de dados do site do Configuration Manager).  

-   Configura os seguintes direitos para usuários administrativos do Configuration Manager para especificar pastas de relatórios no Reporting Services:  

    -   Adiciona e atribui a função **Usuários de Relatório do ConfigMgr** à pasta de relatórios associada para usuários administrativos que têm permissões **Executar Relatório** para o objeto do Configuration Manager.  

    -   Adiciona e atribui a função **Administradores de Relatório do ConfigMgr** à pasta de relatórios associada para usuários administrativos que têm permissões **Modificar Relatório** para o objeto do Configuration Manager.  

     O Configuration Manager se conecta ao Reporting Services e define as permissões para usuários nas pastas raiz do Configuration Manager e do Reporting Services e pastas de relatórios específicas. Após a instalação inicial do ponto do Reporting Services, o Configuration Manager se conecta ao Reporting Services em um intervalo de 10 minutos para verificar se os direitos de usuário configurados nas pastas de relatórios são os direitos associados definidos para usuários do Configuration Manager. Quando usuários são adicionados ou direitos de usuários são modificados na pasta de relatórios usando o Gerenciador de Relatórios do Reporting Services, o Configuration Manager substitui essas alterações usando as atribuições baseadas em funções armazenadas no banco de dados do site. O Configuration Manager também remove usuários que não têm direitos de gerar relatórios no Configuration Manager.  

##  <a name="a-namebkmksecurityrolesa-reporting-services-security-roles-for-configuration-manager"></a><a name="BKMK_SecurityRoles"></a> Funções de segurança do Reporting Services para o Configuration Manager  
 Quando o Configuration Manager instala o ponto do Reporting Services, ele adiciona as seguintes funções de segurança no Reporting Services:  

-   **Usuários de Relatório do ConfigMgr**: os usuários que recebem essa função de segurança podem apenas executar relatórios do Configuration Manager.  

-   **Administradores de Relatório do ConfigMgr**: os usuários que recebem essa função de segurança podem executar todas as tarefas relacionadas a relatórios no Configuration Manager.  

##  <a name="a-namebkmkverifyreportingservicespointinstallationa-verify-the-reporting-services-point-installation"></a><a name="BKMK_VerifyReportingServicesPointInstallation"></a> Verifique a instalação do ponto do Reporting Services  
 Após adicionar a função do site do ponto do Reporting Services, você poderá verificar a instalação observando mensagens de status e entradas de arquivo de log específicos. Use o procedimento a seguir para verificar se a instalação do ponto do Reporting Services foi bem-sucedida.  

> [!WARNING]  
>  Ignore esse procedimento se os relatórios forem exibidos na subpasta **Relatórios** do nó **Relatórios** no espaço de trabalho **Monitoramento** do console do Configuration Manager.  

#### <a name="to-verify-the-reporting-services-point-installation"></a>Para verificar a instalação do ponto do Reporting Services  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Status do Sistema**e clique em **Status do Componente**.  

3.  Clique em **SMS_SRS_REPORTING_POINT** na lista de componentes.  

4.  Na guia **Início** , no grupo **Componente** , clique em **Mostrar Mensagens**e em **Tudo**.  

5.  Especifique uma data e hora para um período, anterior à instalação do ponto do Reporting Services e clique em **OK**.  

6.  Verifique se a ID 1015 da mensagem de status está listada, a qual indica que o ponto do Reporting Services foi instalado com êxito. Ou você pode abrir o arquivo Srsrp.log, localizado em &lt;*Caminho de instalação do ConfigMgr*>\Logs, e procurar **Instalação bem-sucedida**.  

     No Windows Explorer, navegue até &lt;*Caminho de instalação do ConfigMgr*>\Logs.  

7.  Abra o Srsrp.log e percorra o arquivo de log começando pela hora em que o ponto do Reporting Services foi instalado com êxito. Verifique se as pastas de relatórios foram criadas, os relatórios implantados e a política de segurança de cada pasta confirmada. Procure **Verificado com êxito que o Serviço web SRS está adequado no servidor** após a última linha de confirmações de política de segurança.  

##  <a name="a-namebkmkcertificatea-configure-a-self-signed-certificate-for-configuration-manager-console-computers"></a><a name="BKMK_Certificate"></a> Configurar um certificado autoassinado para computadores de console do Configuration Manager  
 Há muitas opções para a criação de relatórios do SQL Server Reporting Services. Quando você cria ou edita relatórios no console do Configuration Manager, o Configuration Manager abre o Construtor de Relatórios para usá-lo como ambiente de criação. Independentemente da forma como você cria seus relatórios do Configuration Manager, um certificado autoassinado é necessário para autenticação do servidor no servidor de banco de dados do site. O Configuration Manager instala automaticamente o certificado no servidor do site e nos computadores com o Provedor de SMS instalado. Portanto, você poderá criar ou editar relatórios no console do Configuration Manager quando ele for executado de um desses computadores. No entanto, quando cria ou modifica relatórios em um console do Configuration Manager instalado em um computador diferente, você precisa exportar o certificado do servidor do site e adicioná-lo ao repositório de certificados **Pessoas Confiáveis** do computador que executa o console do Configuration Manager.  

> [!NOTE]  
>  Para obter mais informações sobre outros ambientes de criação de relatório para o SQL Server Reporting Services, consulte [Comparando ambientes de criação de relatório](http://go.microsoft.com/fwlink/p/?LinkId=242805) nos Manuais Online do SQL Server 2008.  

 Use o procedimento a seguir como exemplo de como transferir uma cópia do certificado autoassinado do servidor do site para outro computador que executa o console do Configuration Manager quando ambos os computadores executarem o Windows Server 2008 R2. Se você não conseguir seguir esse procedimento porque possui outra versão do sistema operacional, consulte a documentação do mesmo para ver o procedimento equivalente.  

#### <a name="to-transfer-a-copy-of-self-signed-certificate-from-the-site-server-to-another-computer"></a>Para transferir uma cópia do certificado autoassinado do servidor do site para outro computador  

1.  Execute as seguintes etapas no servidor do site para exportar o certificado autoassinado:  

    1.  Clique em **Iniciar**, depois em **Executar**e digite **mmc.exe**. No console vazio, clique em **Arquivo**e em **Adicionar/Remover Snap-in**.  

    2.  Na caixa de diálogo **Adicionar ou Remover Snap-ins** , selecione **Certificados** na lista de **Snap-ins disponíveis**e clique em **Adicionar**.  

    3.  Na caixa de diálogo **Snap-in de certificado** , selecione **Conta de computador**e clique em **Próximo**.  

    4.  Na caixa de diálogo **Selecionar Computador** , verifique se a opção **Computador local: (o computador no qual este console está sendo executado)** está marcada e clique em **Concluir**.  

    5.  Na caixa de diálogo **Adicionar ou Remover Snap-ins** , clique em **OK**.  

    6.  No console, expanda **Certificados (computador local)**, **Pessoas Confiáveis**e selecione **Certificados**.  

    7.  Clique com o botão direito do mouse no certificado com o nome amigável de &lt;*FQDN do servidor do site*>, clique em **Todas as Tarefas** e selecione **Exportar**.  

    8.  Conclua o **Assistente para Exportação de Certificados** usando as opções padrão e salve o certificado com a extensão de nome de arquivo **.cer** .  

2.  Conclua as etapas a seguir no computador que executa o console do Configuration Manager para adicionar o certificado autoassinado ao repositório de certificados Pessoas Confiáveis:  

    1.  Repita que as etapas anteriores, de 1.a até 1.e para configurar o MMC do snap-in do **Certificado** no computador do ponto de gerenciamento.  

    2.  No console, expanda **Certificados (computador local)**e, em seguida, **Pessoas Confiáveis**; clique com o botão direito do mouse em **Certificados**, selecione **Todas as Tarefas**e, depois, **Importar** para iniciar o **Assistente para Importação de Certificados**.  

    3.  Na página **Arquivo a Ser Importado** , selecione o certificado salvo na etapa 1.h e clique em **Próximo**.  

    4.  Na página **Repositório de Certificados** , selecione **Colocar todos os certificados no repositório a seguir**com o **Repositório de certificados** definido como **Pessoas Confiáveis**; clique em **Próximo**.  

    5.  Clique em **Concluir** para fechar o assistente e concluir a configuração do certificado no computador.  

##  <a name="a-namebkmkmodifyreportingservicespointa-modify-reporting-services-point-settings"></a><a name="BKMK_ModifyReportingServicesPoint"></a> Modificar as configurações de ponto do Reporting Services  
 Após a instalação do ponto do Reporting Services, você pode modificar as configurações de conexão do banco de dados do site e de autenticação nas propriedades do ponto do Reporting Services. Use o procedimento a seguir para modificar as configurações do ponto do Reporting Services.  

#### <a name="to-modify-reporting-services-point-settings"></a>Para modificar as configurações do ponto do Reporting Services  

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Configuração de Site**e clique em **Funções de Servidores e Sistema de Site** na lista de sistemas de site.  

    > [!TIP]  
    >  Para listar somente sistemas de site que hospedam a função do site do ponto do Reporting Services, clique com o botão direito do mouse em **Funções de Servidores e Sistema de Site** para selecionar o **Ponto do Reporting Services**.  

3.  Selecione o sistema de site que hospeda o ponto do Reporting Services no qual você deseja modificar as configurações e selecione **Ponto do Reporting Services** em **Funções do Sistema de Site**.  

4.  Na guia **Função do Site** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Na caixa de diálogo **Propriedades do Ponto do Reporting Services** , você pode modificar as seguintes configurações:  

    -   **Nome do servidor de banco de dados do site**: especifique o nome do servidor que hospeda o banco de dados do site do Configuration Manager. Geralmente, o assistente automaticamente recupera o FQDN (nome de domínio totalmente qualificado) do servidor. Para especificar uma instância do banco de dados, use o formato &lt;*Nome do Servidor*>\&lt;*Nome da Instância*>.  

    -   **Nome do banco de dados**: especifique o nome do banco de dados do site do System Center 2012 Configuration Manager e clique em **Verificar** para confirmar se o assistente tem acesso ao banco de dados do site.  

        > [!IMPORTANT]  
        >  A conta de usuário que está criando o ponto do Reporting Services deve ter acesso de Leitura ao banco de dados do site. Se o teste de conexão falhar, será exibido um ícone de aviso vermelho. Mova o cursor sobre esse ícone para ler os detalhes da falha. Corrija a falha e clique em **Testar** novamente.  

    -   **Conta de usuário**: clique em **Definir**e selecione uma conta a ser usada quando o SQL Server Reporting Services do ponto do Reporting Services se conectar ao banco de dados do site do Configuration Manager para recuperar os dados exibidos em um relatório. Selecione **Conta existente** para especificar uma conta de usuário do Windows que tem direitos existentes no Configuration Manager ou selecione **Nova conta** para especificar uma conta de usuário do Windows que atualmente não tem direitos no Configuration Manager. O Configuration Manager concede automaticamente à conta de usuário especificada acesso ao banco de dados do site. A conta será exibida como a conta **Ponto de relatório SRS do ConfigMgr** na subpasta **Contas** do nó **Segurança** no espaço de trabalho **Administração** .  

         A conta de usuário e a senha especificadas do Windows serão criptografadas e armazenadas no banco de dados do Reporting Services. O Reporting Services recupera os dados para os relatórios a partir do banco de dados do site usando essa conta e senha.  

        > [!IMPORTANT]  
        >  Quando o banco de dados do site estiver em um sistema de site remoto, a conta especificada deverá ter a permissão **Logon Local** para o computador.  

6.  Clique em **OK** para salvar as alterações e sair da caixa de diálogo.  

## <a name="upgrading-sql-server"></a>Atualizando o SQL Server  
 Após atualizar o SQL Server e o SQL Server Reporting Services usado como fonte de dados para um ponto do Reporting Services, talvez você veja alguns erros ao executar ou editar relatórios no console do Configuration Manager. Para que o relatório seja executado adequadamente no console do Configuration Manager, é necessário remover a função do sistema de sites do ponto do Reporting Services para o site e reinstalá-la. No entanto, após a atualização você poderá continuar executando e editando relatórios com êxito em um navegador da Internet.  

##  <a name="a-namebkmkconfigurereportoptionsa-configure-report-options"></a><a name="BKMK_ConfigureReportOptions"></a> Configurar opções de relatório  
 Use as opções de relatório de um site do Configuration Manager para selecionar o ponto do Reporting Services padrão que será usado para gerenciar seus relatórios. Embora você possa ter mais de um ponto do Reporting Services em um site, somente o servidor de relatório padrão selecionado nas opções de relatório será usado para gerenciar relatórios. Use o procedimento a seguir para configurar as opções de relatório para o seu site.  

#### <a name="to-configure-report-options"></a>Para configurar as opções de relatório  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Relatórios**e clique em **Relatórios**.  

3.  Na guia **Início** , no grupo **Configurações** , clique em **Opções de Relatório**.  

4.  Selecione o servidor de relatório padrão na lista e clique em **OK**. Se nenhum ponto do Reporting Services estiver na lista, verifique se você possui um ponto do Reporting Services instalado e configurado com êxito no site.  

## <a name="next-steps"></a>Próximas etapas
[Operações e manutenção de relatórios](operations-and-maintenance-for-reporting.md)



<!--HONumber=Nov16_HO1-->


