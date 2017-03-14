---
title: "Assistente de instalação | Microsoft Docs"
ms.custom: na
ms.date: 2/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 37865f1f3dc959ee8acf8ab06df5cae6e07e4257
ms.openlocfilehash: 97eb95c1c6ac31ce9bca22df13bcc4f248026298
ms.lasthandoff: 03/01/2017

---
# <a name="use-the-setup-wizard-to-install-system-center-configuration-manager-sites"></a>Use o Assistente de Instalação para instalar sites do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Para instalar um novo site do System Center Configuration Manager usando uma interface do usuário interativa, use o Assistente de Instalação do Configuration Manager (setup.exe). O assistente dá suporte à instalação de um site primário ou de um site de administração central. Você também usa o assistente para [atualizar uma instalação de avaliação](../../../../core/servers/deploy/install/upgrade-an-evaluation-install-to-a-full-install.md) do Configuration Manager para uma instalação totalmente licenciada. Quando não quiser usar o assistente, você pode usar um [script de instalação](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md) e executar uma instalação de linha de comando autônoma.

Para instalar um site secundário, você precisa instalar o site de dentro do console do Configuration Manager. Sites secundários não dão suporte a uma instalação de linha de comando com scripts.

## <a name="bkmk_primary"></a> Instalar um site de administração central ou site primário
Use o procedimento a seguir para instalar um site de administração central, um site primário ou para atualizar um site de avaliação para um site do Configuration Manager totalmente licenciado.   

Antes de iniciar a instalação do site, familiarize-se com os detalhes fornecidos nos seguintes artigos:
 -  [Preparar para instalar sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md)
 -  [Pré-requisitos para instalar sites](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md)

Se você estiver instalando um site de administração central como parte de um cenário de expansão de site, examine a seção [Expandir um site primário autônomo](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand) neste tópico antes de usar o procedimento a seguir.

### <a name="bkmk_installpri"></a> Para instalar um site de administração central ou primário

1.  No computador no qual deseja instalar o site, execute **&lt;InstallationMedia\>\SMSSETUP\BIN\X64\Setup.exe** para iniciar o **Assistente de Instalação do System Center Configuration Manager**.  

    > [!NOTE]  
    > Quando instala um site de administração central para expandir um site primário autônomo ou instala um novo site primário filho em uma hierarquia existente, você precisa usar a mídia de instalação (arquivos de origem) que corresponde à versão do site ou sites existentes. Se você tiver instalado atualizações no console que alteraram a versão dos sites instalados anteriormente, não use a mídia de instalação original. Em vez disso, use os arquivos de origem da [pasta CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) de um site atualizado. O Configuration Manager exige que você use arquivos de origem que correspondam à versão do site existente ao qual seu novo site se conectará.  

2.  Na página **Antes de Começar** escolha **Avançar**.  

3.  Na página **Introdução**, escolha o tipo de site que deseja instalar:  

    -   **Site de administração central**, como o primeiro site de uma nova hierarquia ou ao expandir um site primário autônomo:  

        Selecione **Instalar um site de administração central do Configuration Manager**.  

         Durante uma etapa posterior desse procedimento, você terá a opção de instalar um site de administração central como o primeiro site de uma nova hierarquia ou instalar um site de administração central para expandir um site primário autônomo.  

    -    **Site primário**, como um site primário autônomo que é o primeiro site de uma nova hierarquia ou como um primário filho:  

        Selecione **Instalar um site primário do Configuration Manager**.  

        > [!TIP]  
        > Normalmente, você seleciona apenas **Usar opções de instalação típicas de um site primário autônomo** quando deseja instalar o site primário autônomo em um ambiente de teste. Quando você seleciona essa opção, a Instalação:  

        > -   Configura automaticamente o site como um site primário autônomo.  
        > -   Usa um caminho de instalação padrão.  
        > -   Usa uma instalação local da instância padrão do SQL Server para o banco de dados do site.  
        > -   Instala um ponto de gerenciamento e um ponto de distribuição no computador do servidor do site.  
        > -   Configura o site com o idioma inglês e o idioma de exibição do sistema operacional no servidor do site primário, se ele corresponder a um dos idiomas a que o Configuration Manager dá suporte.  

4.  Na página **Chave do Produto (Product Key)**:
    - escolha se deseja instalar o Configuration Manager como uma edição de avaliação ou uma edição licenciada.  

      -   Se você selecionar uma edição licenciada, insira a chave do produto (Product Key) e escolha **Avançar**.  

      -   Se você selecionar uma edição de avaliação, escolha **Avançar**. (Você pode atualizar uma instalação de avaliação para uma instalação completa posteriormente.)  
    - Começando com a versão de outubro de 2016 da mídia de linha de base da versão 1606 do System Center Configuration Manager, você pode especificar a data de validade do contrato do Software Assurance. Nessa página, você tem a opção de especificar a **Data de validade do Software Assurance** do seu contrato de licença como um lembrete conveniente dessa data. Se não inserir essa informação durante a Instalação, você poderá especificá-la posteriormente no console do Configuration Manager.

      > [!NOTE]   
      > A Microsoft não valida a data de validade inserida e não usará essa data para validação da licença. No entanto, você pode usá-la como um lembrete da data de vencimento. Isso é útil porque o Configuration Manager verifica periodicamente se há novas atualizações de software oferecidas online e o status de licença do Software Assurance deve estar atualizado para que você esteja qualificado para usar essas atualizações adicionais.    

      Para mais informações, consulte [Licenciamento e branches do System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

5.  Na página **Termos de Licença para Software Microsoft** , leia e aceite os termos de licença.  

6.  Na página **Licenças de Pré-requisito** , leia e aceite os termos de licença do software de pré-requisito. A Instalação baixa e instala automaticamente o software nos clientes ou sistemas do site quando necessário. Você deve marcar todas as caixas antes de poder avançar para a próxima página.  

7.  Na página **Downloads de Pré-requisitos** , especifique se a instalação deve baixar os arquivos redistribuíveis de pré-requisitos mais recentes da Internet ou usar os arquivos baixados anteriormente:  

    -   Se você desejar que a instalação baixe os arquivos neste momento, selecione **Baixar arquivos necessários** e especifique um local para armazenar os arquivos.  

    -   Se você tiver baixado os arquivos usando o [Downloader de Instalação](../../../../core/servers/deploy/install/setup-downloader.md), selecione **Usar arquivos baixados anteriormente** e especifique a pasta de download.  

        > [!TIP]  
        > Se você usar os arquivos baixados anteriormente, verifique se o caminho para a pasta de download contém a versão mais recente dos arquivos.  

8.  Na página **Seleção do Idioma do Servidor**, selecione os idiomas que estão disponíveis para o console do Configuration Manager e para os relatórios. (O inglês é selecionado por padrão e não pode ser removido.)  

9. Na página **Seleção do Idioma do Cliente**, selecione os idiomas que estão disponíveis em computadores cliente e especifique se deseja habilitar todos os idiomas do cliente para clientes de dispositivos móveis. (O inglês é selecionado por padrão e não pode ser removido.)  

    > [!IMPORTANT]  
    > Quando usar um site de administração central, verifique se os idiomas do cliente que você configurou no site de administração central incluem todos os idiomas do cliente que você configurou em cada site primário filho. Isso é recomendado porque os clientes que são instalados por meio de um ponto de distribuição têm acesso aos idiomas do cliente por meio do site de nível superior, enquanto os clientes que são instalados de um ponto de gerenciamento têm acesso aos idiomas do cliente por meio do site primário atribuído a eles.  

10. Na página **Configurações do Site e de Instalação**, especifique o seguinte para o novo site que você está instalando:  

    -   **Código do site:** [cada código do site em uma hierarquia deve ser exclusivo](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_sitecodes) e composto por três dígitos alfanuméricos (A até Z e 0 até 9). Como o código do site é usado em nomes de pasta, não use nomes reservados do Windows para o site, incluindo:    
        -   AUX  
        -   CON    
        -   NUL    
        -   PRN    
        -   SMS  

        > [!NOTE]  
        > A instalação não verifica se o código do site especificado já está em uso ou se tem um nome reservado.  

    -   **Nome do site:** cada site requer esse nome amigável, o qual pode ajudar a identificar o site.  

    -   **Pasta de instalação**: é o caminho de pasta para a instalação do Configuration Manager. Você não pode alterar o local depois de instalar o site. Além disso, o caminho não pode conter espaços à direita ou caracteres Unicode.  

11. Na página **Instalação do Site**, use a opção a seguir que corresponde ao seu cenário:  

    -   **Estou instalando um site de administração central:**  

         Na página **Instalação do Site de Administração Central**, selecione **Instalar como o primeiro site em uma nova hierarquia** e escolha **Avançar** para continuar.  

    -   **Estou expandindo um site primário autônomo em uma hierarquia com um site de administração central:**  

         Na página **Instalação do Site de Administração Central**, selecione **Expandir um primário autônomo existente em uma hierarquia**, especifique o FQDN do servidor do site primário autônomo e escolha **Avançar** para continuar.  

         A mídia que você usa para instalar o novo site de administração central deve corresponder à versão do site primário.  

    -   **Estou instalando um site primário autônomo:**  

         Na página **Instalação de Site Primário**, selecione **Instalar o site primário como site autônomo** e escolha **Avançar**.  

    -   **Estou instalando um site primário filho:**  

         Na página **Instalação de Site Primário**, selecione **Ingressar o site primário em uma hierarquia existente**, especifique o FQDN para o site de administração central e escolha **Próximo**.  

12. Na página **Informações do Banco de Dados**, especifique as informações a seguir:  

    -   **Nome do SQL Server (FQDN):** por padrão, é definido para ser o computador do servidor do site.  

    -   **Nome da instância:** por padrão, fica em branco. Ele usa a instância padrão do SQL no computador do servidor do site.  

    -   **Nome do banco de dados:** por padrão, é definido como CM_&lt;Código do site\>. Você é livre para usar um nome diferente que você especificar.  

    -   **Porta do Service Broker:** por padrão, isso é definido para usar a porta do SQL SSB (Server Service Broker) padrão de 4022. O SQL a usa para se comunicar diretamente com o banco de dados do site em outros sites.  

13. Na segunda página **Informações do Banco de Dados**, você pode especificar locais não padrão para o arquivo de dados do SQL Server e o arquivo de log do SQL Server para o banco de dados do site:  

    -   Locais de arquivo padrão para o SQL Server são fornecidos.  

    -   A opção de especificar locais de arquivo não padrão não está disponível quando você usa um cluster do SQL Server.  

    -   O verificador de pré-requisitos não executa uma verificação de espaço livre em disco para locais de arquivo não padrão.  

14. Na página **Configurações do Provedor de SMS** , especifique o FQDN para o servidor no qual você deseja instalar o provedor de SMS.  

    -   Por padrão, o servidor do site é especificado.  

    -   Depois de instalar o site, você pode configurar outros Provedores de SMS.  

15. Na página **Configurações de Comunicação do Cliente** , escolha se é para configurar todos os sistemas de sites para aceitar somente a comunicação HTTPS de clientes ou se o método de comunicação deve ser configurado para cada função do sistema de sites.  

    Ao selecionar **Todas as funções do sistema de sites aceitam apenas comunicação HTTPS de clientes**, o computador cliente deverá ter um certificado PKI válido para autenticação do cliente. Para obter mais informações sobre os requisitos de certificado PKI, consulte [Requisitos de certificado PKI para o Configuration Manager](https://technet.microsoft.com/library/gg699362.aspx).  

    > [!NOTE]  
    > Esta etapa se aplica somente quando você instala um site primário. Se você estiver instalando um site de administração central, ignore esta etapa.  

16. Na página **Funções do Sistema de Site** , escolha se é para instalar um ponto de gerenciamento ou um ponto de distribuição. Para cada função que você opta que o programa de Instalação instale:  

    -   Você deve inserir o **FQDN** do computador que hospedará a função e escolher o método de conexão do cliente ao qual o servidor dará suporte (HTTP ou HTTPS).  

    -   Se você selecionou **Todas as funções do sistema de sites aceitam apenas comunicação HTTPS de clientes** na página anterior, as definições de conexão do cliente serão automaticamente configuradas para HTTPS e não poderão ser alteradas a menos que você volte e mude a configuração.  

    > [!NOTE]  
    > Esta etapa se aplica somente quando você instala um site primário. Se você estiver instalando um site de administração central, ignore esta etapa.  

    > [!NOTE]  
    > Para instalar funções do sistema de sites, a instalação usa a **conta de instalação do sistema de sites**. Por padrão, a conta de computador do site primário é usada. Para instalar a função do sistema de sites, essa conta deve ser um administrador local em um computador remoto. Se essa conta não tiver as permissões necessárias, desmarque as funções do sistema de sites e instale-as mais tarde usando o console do Configuration Manager depois de configurar contas adicionais a serem usadas como contas de instalação do sistema de sites.  

17. Na página **Dados de Uso**, examine as informações sobre os dados que a Microsoft coleta e escolha **Avançar**.  

18. A página **Instalação do Ponto de Conexão de Serviço** está disponível apenas durante a Instalação:  

    -   Quando você estiver instalando um site primário autônomo.  

    -   Quando você estiver instalando um site de administração central.  

    > [!NOTE]  
    > Se você estiver instalando um site primário filho, ignore esta etapa (esta página não estará disponível).  

     Se você estiver instalando um site de administração central como parte de um cenário de expansão do site e essa função já estiver instalada no site primário autônomo, desinstale a função do site primário autônomo. Apenas uma instância dessa função é permitida em uma hierarquia, sendo permitida somente no site da camada superior da hierarquia.  

     Depois de selecionar uma configuração para o **Ponto de Conexão de Serviço**, escolha **Avançar**. (Após a conclusão da Instalação, você poderá alterar essa configuração no console do Configuration Manager.)  

19. Na página **Resumo das Configurações**, examine as configurações que você selecionou. Quando você estiver pronto, escolha **Avançar** para iniciar o Verificador de Pré-requisitos.  

20. Na página **Verificação de Instalação de Pré-requisitos**, todos os problemas que podem ser identificados são listados.  

    -   Quando o Verificador de Pré-requisitos encontrar um problema, escolha um item da lista para exibir os detalhes sobre como solucionar o problema.  

    -   Você deve resolver todos os itens com status de **Falha** antes de continuar a instalar o site. Itens com o status de **Aviso** devem ser resolvidos, mas não bloqueiam a instalação do site.  

    -   Depois de resolver os problemas, escolha **Executar Verificação** para executar novamente o Verificador de Pré-requisitos.  

     Se o Verificador de Pré-requisitos for executado e nenhuma verificação receber um status de **Falha**, você poderá escolher **Iniciar Instalação** para iniciar a instalação do site.  

    > [!TIP]  
    > Além dos comentários fornecidos no assistente, você pode encontrar informações adicionais sobre problemas de pré-requisito ao exibir o arquivo **ConfigMgrPrereq.log** na raiz da unidade do sistema do computador que está instalando. Para obter uma lista das regras e descrições dos pré-requisitos de instalação, consulte [Lista de verificações de pré-requisitos para o System Center Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md).  

21. Na página **Instalação** , o programa de instalação exibe o status da instalação. Quando a instalação do servidor do site principal for concluída, você terá a opção de **Fechar** o assistente de instalação. Quando você fecha o assistente, a instalação e as configurações iniciais do site continuam em segundo plano.  

    -   Você pode conectar um console do Configuration Manager ao site antes de a Instalação ser concluída. Esse console se conecta no modo somente leitura e permite a exibição de objetos e de configurações, mas você não pode introduzir edições.  

    -   Após a conclusão da instalação, você poderá conectar um console que permite a edição de objetos e de configurações.  


## <a name="bkmk_expand"></a> Expandir um site primário autônomo
Ao instalar um site primário autônomo como seu primeiro site, você tem a opção de expandir posteriormente o site em uma hierarquia maior instalando um site de administração central.   

Ao expandir um site primário autônomo, você pode instalar um novo site de administração central que usa o banco de dados do site primário autônomo existente como referência. Depois de instalar o novo site de administração central, o site primário autônomo funciona como um site primário filho.

-   Somente um site primário autônomo pode ser expandido em uma nova hierarquia.  

-   Somente um site primário autônomo pode ser expandido em uma hierarquia específica. Você não pode usar essa opção para adicionar mais sites primários autônomos à mesma hierarquia. Em vez disso, use a Migração para migrar dados de uma hierarquia para outra.  

-   Depois de expandir um site autônomo em uma hierarquia com um site de administração central, você pode adicionar mais sites primários filhos.  

-   Para remover um site primário de uma hierarquia com um site de administração central, desinstale o site primário.  

Para expandir o site, use o Assistente de Instalação do System Center Configuration Manager para instalar um novo site de administração central com as seguintes condições:  

-   Instale o site de administração central usando a mesma versão do Configuration Manager que o site primário autônomo.  

-   Na página de **Introdução** do Assistente de Instalação, selecione a opção para instalar um site de administração central. Em um estágio posterior da Instalação, você escolherá uma opção para expandir um site primário autônomo existente.  

-   Ao configurar a página **Seleção do Idioma do Cliente** para o novo site de administração central, você deve selecionar os mesmos idiomas do cliente que estão configurados para o site primário autônomo que você está expandindo.  

-   Na página **Instalação do Site**, selecione a opção para expandir o site primário autônomo.  

Para expandir um site primário autônomo, use o procedimento *[Para instalar um site de administração central ou primário](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_installpri)*, anteriormente neste artigo.


## <a name="bkmk_secondary"></a> Instalar um site secundário
 Use o console do Configuration Manager para instalar um site secundário.  

-   Se o console usado não estiver conectado ao site primário que será o site pai do novo site secundário, o comando para instalar o site será replicado para o site primário correto.  

-   Antes de iniciar a instalação do site, verifique se sua conta de usuário tem as permissões de pré-requisito e se o computador que hospedará o novo site secundário cumpre todos os pré-requisitos para uso como um servidor do site secundário.  

-   Quando você instala o site secundário, o Configuration Manager configura o novo site para usar as portas de comunicação do cliente configuradas no site primário pai.  

### <a name="bkmk_installsecondary"></a> Para instalar um site secundário  


1.  No console do Configuration Manager, navegue até **Administração** > **Configuração de Site** > **Sites**. Selecione o site que será o site primário pai do novo site secundário.  

2.  Escolha **Criar Site Secundário** para iniciar o **Assistente de Criação de Site Secundário**.  

3.  Na página **Antes de Começar**, confirme se o site primário listado é o site que você deseja que seja o pai do novo site secundário. Em seguida, escolha **Avançar**.  

4.  Na página **Geral** , especifique o seguinte:  

    -   **Código do site**: cada código do site em uma hierarquia deve ser exclusivo e composto por três dígitos alfanuméricos (A até Z e 0 até 9). Como o código do site é usado em nomes de pasta, não use nomes reservados do Windows para o site, incluindo:  

        -   AUX    
        -   CON    
        -   NUL    
        -   PRN  
        -   SMS  

       > [!NOTE]  
       > A instalação não verifica se o código do site especificado já está em uso ou se é um nome reservado.  

    -   **Nome do servidor do site**: esse é o FQDN do servidor no qual o novo site secundário será instalado.  

    -   **Nome do site**: cada site requer esse nome amigável, o qual pode ajudar a identificar o site.  

    -   **Pasta de instalação**: esse é o caminho de pasta para a instalação do Configuration Manager. Você não pode alterar o local depois de instalar o site. O caminho não pode conter espaços à direita ou caracteres Unicode.  

    > [!IMPORTANT]  
    > Depois de especificar detalhes nesta página, você pode escolher **Resumo** para usar as configurações padrão para o restante das opções de site secundário e ir diretamente para a página **Resumo** do assistente.  

    > -   Use essa opção apenas quando estiver familiarizado com as configurações padrão do assistente e elas forem as configurações que você deseja usar.  
    > -   Grupos de limites não são associados ao ponto de distribuição quando você usa as configurações padrão. Portanto, até que você configure grupos de limites que incluam o servidor do site secundário, os clientes não usarão o ponto de distribuição que está instalado no site secundário como um local de origem do conteúdo.  

5.  Na página **Arquivos de Origem de Instalação** , escolha como o computador do site secundário obtém os arquivos de origem para instalar o site.  

     Quando você usa arquivos de origem que são armazenados na rede ou armazenados no computador do site secundário:  

    -   O local do arquivo de origem deve incluir uma pasta chamada **Redist** que inclui todos os arquivos que foram baixados anteriormente usando o Downloader de Instalação.  

    -   Se qualquer um dos arquivos de **Redist** não estiver disponível, haverá falha na instalação do site secundário.  

    -   A conta de computador do computador do site secundário deve ter permissões de **Leitura** para o compartilhamento e a pasta do arquivo de origem.  

6.  Na página **Configurações do SQL Server** , especifique a versão do SQL Server a ser usada e defina as configurações relacionadas.  

    > [!NOTE]  
    > A Instalação não valida as informações inseridas nesta página até que se inicie a instalação. Antes de prosseguir, verifique essas configurações.  

     **Instalar e configurar uma cópia local do SQL Express no computador do site secundário**  

    -   **Porta do Serviço SQL Server**: especifique a porta do serviço SQL Server para o SQL Server Express a ser usado. A porta de serviço geralmente é configurada para usar a porta TCP 1433, mas você pode configurar outra porta.  

    -   **Porta do SQL Server Broker**: especifique a porta do SSB (SQL Server Service Broker) a ser usada pelo SQL Server Express. O Service Broker geralmente é configurado para usar a porta TCP 4022, mas você pode configurar outra porta. É necessário especificar uma porta válida que nenhum outro site ou serviço esteja usando e que nenhuma restrição de firewall esteja bloqueando.  

    > [!IMPORTANT]  
    > Quando o Configuration Manager instala o SQL Server Express, ele instala o SQL Server Express 2012 sem service pack:  

    > -   Para que o site secundário tenha suporte, depois de ser instalado, é necessário atualizar o SQL Server Express 2012 instalando o Service Pack 2 (ou posterior).
    > -   Além disso, se a instalação do novo site secundário falhar ao concluir, mas primeiro concluir a instalação do SQL Server Express 2012, você deverá atualizar essa instância do SQL Server Express antes que o Configuration Manager possa tentar novamente a instalação do site secundário com êxito.  

     **Usar uma instância existente do SQL Server**  

    -   **FQDN do SQL Server**: examine o FQDN do computador executando o SQL Server. É necessário usar um servidor local executando o SQL Server para hospedar o banco de dados do site secundário e não é possível modificar essa configuração.  

    -   **Instância do SQL Server**: especifique a instância do SQL Server a ser usada como o banco de dados do site secundário. Deixe essa opção em branco para usar a instância padrão.  

    -   **Nome do banco de dados do site do ConfigMgr**: especifique o nome a ser usado para o banco de dados do site secundário.  

    -   **Porta do SQL Server Broker**: especifique a porta do SSB (SQL Server Service Broker) a ser usada pelo SQL Server. É necessário especificar uma porta válida que nenhum outro site ou serviço esteja usando, e sem bloqueio por restrições de firewall.  

    > [!TIP]  
    > Consulte [Versões do SQL Server com suporte](../../../../core/plan-design/configs/support-for-sql-server-versions.md) para obter uma lista das versões do SQL Server com suporte pelo System Center Configuration Manager.  

7.  Na página **Ponto de Distribuição** , defina as configurações para o ponto de distribuição que será instalado no servidor do site secundário.  

     **Configurações obrigatórias:**  

    -   **Especificar como os dispositivos cliente se comunicam com o ponto de distribuição**: escolha entre HTTP e HTTPS.  

    -   **Criar um certificado autoassinado ou importar um certificado de cliente PKI**: escolha entre usar um certificado autoassinado (que possibilita também permitir conexões anônimas de clientes do Configuration Manager à biblioteca de conteúdo) ou importar um certificado de sua PKI.  

         Esse certificado é usado para autenticar o ponto de distribuição para um ponto de gerenciamento antes que o ponto de distribuição envie mensagens de status.  

         Para obter informações sobre os requisitos de certificado, consulte [Requisitos de certificado PKI para o Configuration Manager](https://technet.microsoft.com/library/gg699362.aspx).  

    **Configurações opcionais:**  

    -   **Instalar e configurar o IIS se exigido pelo Configuration Manager**: selecione esta configuração para permitir que o Configuration Manager instale e configure o IIS (Serviços de Informações da Internet) no servidor se ele ainda não estiver instalado. O IIS deve ser instalado em todos os pontos de distribuição.  

        > [!NOTE]  
        > Embora essa configuração seja opcional, o IIS deve ser instalado no servidor antes de um ponto de distribuição ser instalado com êxito.  

    -   **Habilitar e configurar o BranchCache para este ponto de distribuição**.  

    -   **Descrição**. Essa é uma descrição amigável do ponto de distribuição para ajudá-lo a reconhecê-lo.  

    -   **Habilitar este ponto de distribuição para conteúdo pré-teste**.  

8.  Na página **Configurações de Unidade** , especifique as configurações da unidade para o ponto de distribuição do site secundário.  

     Você pode configurar até duas unidades de disco para a biblioteca de conteúdo e duas unidades de disco para o compartilhamento de pacote. No entanto, o Configuration Manager pode usar outras unidades quando as duas primeiras atingirem a reserva de espaço de unidade configurada. A página **Configurações de Unidade** é o local em que você configura a prioridade das unidades de disco e a quantidade de espaço livre em disco a permanecer em cada unidade de disco.  

    -   **Reserva de espaço de unidade (MB)**: o valor que você define para esta configuração determina a quantidade de espaço livre na unidade antes que o Configuration Manager escolha uma unidade diferente e continue o processo de cópia nessa unidade. Arquivos de conteúdo podem abranger várias unidades.  

    -   **Locais de Conteúdo**: Especifique os locais de conteúdo para a biblioteca de conteúdo e o compartilhamento de pacotes. O Configuration Manager copia conteúdo para o local de conteúdo primário até que a quantidade de espaço livre atinja o valor especificado para **Reserva de espaço de unidade (MB)**.

     Por padrão, os locais de conteúdo são definidos para **Automático**. O local do conteúdo primário é definido como a unidade de disco com mais espaço em disco no momento da instalação. O local secundário é definido como a unidade de disco que tem o maior espaço em disco após a unidade primária. Quando as unidades primárias e secundárias atingirem a reserva de espaço de unidade, o Configuration Manager selecionará outra unidade disponível com o maior espaço em disco e continuará o processo de cópia.  

9. Na página **Validação de Conteúdo** , especifique se a integridade dos arquivos de conteúdo no ponto de distribuição deve ser validada.  

    -   Quando você habilita a validação de conteúdo segundo um cronograma, o Configuration Manager inicia o processo no horário agendado e todo o conteúdo no ponto de distribuição é verificado.  

    -   Também é possível configurar a **Prioridade de validação de conteúdo**.  

    -   Para exibir os resultados do processo de validação de conteúdo, no console do Configuration Manager, navegue até **Monitoramento** > **Status da Distribuição** > **Status do Conteúdo**. O conteúdo de cada tipo de pacote (por exemplo, aplicativo, pacote de atualização de software e imagem de inicialização) é exibido.  

10. Na página **Grupos de Limite**, gerencie os grupos de limite aos quais esse ponto de distribuição está atribuído:  

    -   Durante a implantação do conteúdo, os clientes devem estar em um grupo de limites associado ao ponto de distribuição para usá-lo como um local de origem para conteúdo.  

    -   Você pode selecionar a opção **Permitir local de origem de fallback para conteúdo** para permitir que clientes fora desses grupos de limites façam fallback e usem o ponto de distribuição como um local de origem para conteúdo quando não houver disponíveis pontos de distribuição preferenciais.  

     Para obter informações sobre os pontos de distribuição preferenciais, consulte o tópico [Conceitos fundamentais para o gerenciamento de conteúdo](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

11. Na página **Resumo**, verifique as configurações e escolha **Avançar** para instalar o site secundário. Quando o assistente apresentar a página **Conclusão**, você poderá fechar o assistente. A instalação do site secundário continua em segundo plano.  


### <a name="bkmk_verify"></a> Para verificar o status da instalação do site secundário  

1.  No console do Configuration Manager, navegue até **Administração** > **Configuração de Site** > **Sites**.  

2.  Selecione o servidor do site secundário que você está instalando e escolha **Mostrar Status da Instalação**.  

    > [!TIP]  
    > Quando você instala mais de um site secundário de cada vez, o Verificador de Pré-requisitos executado em um único site por vez e deve ser concluído antes da verificação do próximo site.  

