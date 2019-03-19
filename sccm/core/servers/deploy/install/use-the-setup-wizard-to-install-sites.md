---
title: Assistente para Instalação
titleSuffix: Configuration Manager
ms.date: 03/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 67c82a884a5d3df3b1e61e1f9f2c109ff2b7fef6
ms.sourcegitcommit: af8693048e6706ffda72572374f56e0bc7dfce2c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/11/2019
ms.locfileid: "57737343"
---
# <a name="use-the-setup-wizard-to-install-configuration-manager-sites"></a>Usar o Assistente para Instalação para instalar sites do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para instalar um novo site do Configuration Manager usando uma interface do usuário interativa, use o Assistente para Instalação do Configuration Manager (setup.exe). O assistente dá suporte à instalação de um site primário ou de um site de administração central. Você também usa o assistente para [fazer upgrade de uma instalação de avaliação](/sccm/core/servers/deploy/install/upgrade-an-evaluation-install-to-a-full-install) do Configuration Manager para uma instalação totalmente licenciada. Quando não quiser usar o assistente, você pode usar um [script de instalação](/sccm/core/servers/deploy/install/use-a-command-line-to-install-sites) e executar uma instalação de linha de comando autônoma.

Instale um site secundário do console do Configuration Manager. Sites secundários não dão suporte a uma instalação de linha de comando com scripts.



## <a name="bkmk_primary"></a> Instalar um site de administração central ou site primário

Use o procedimento a seguir para instalar um site de administração central ou um site primário. Use-o também para atualizar um site de avaliação para um site totalmente licenciado do Configuration Manager.   

Antes de iniciar a instalação do site, familiarize-se com os detalhes fornecidos nos seguintes artigos:
- [Preparar para instalar sites](/sccm/core/servers/deploy/install/prepare-to-install-sites)
- [Pré-requisitos para instalar sites](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites)

Se você estiver instalando um site de administração central como parte de um cenário de expansão de site, examine [Expandir um site primário autônomo](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_expand) antes de usar o procedimento a seguir.

### <a name="bkmk_installpri"></a> Processo para instalar um site de administração central ou primário

1. No computador no qual você deseja instalar o site, execute `<InstallationMedia>\SMSSETUP\BIN\X64\Setup.exe` para iniciar o **Assistente de Instalação do System Center Configuration Manager**.  

    > [!NOTE]  
    > Quando instala um site de administração central para expandir um site primário autônomo ou instala um novo site primário filho em uma hierarquia existente, você usa a mídia de instalação (arquivos de origem) que corresponde à versão do site ou sites existentes. Se você tiver instalado atualizações no console que alteraram a versão dos sites instalados anteriormente, não use a mídia de instalação original. Em vez disso, use os arquivos de origem da [pasta CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder) de um site atualizado. O Configuration Manager exige que você use arquivos de origem que correspondam à versão do site existente ao qual seu novo site se conectará.  

2. Na página **Antes de Começar** escolha **Avançar**.  

3. Na página **Introdução**, escolha o tipo de site que deseja instalar:  

    - **Site de administração central**, como o primeiro site de uma nova hierarquia ou ao expandir um site primário autônomo:  

        Selecione **Instalar um site de administração central do Configuration Manager**.  

        Durante uma etapa posterior desse procedimento, você terá a opção de instalar um site de administração central como o primeiro site de uma nova hierarquia ou instalar um site de administração central para expandir um site primário autônomo.  

    - **Site primário**, como um site primário autônomo que é o primeiro site de uma nova hierarquia ou como um primário filho:  

        Selecione **Instalar um site primário do Configuration Manager**.  

        > [!TIP]  
        > Normalmente, você seleciona apenas **Usar opções de instalação típicas de um site primário autônomo** quando deseja instalar o site primário autônomo em um ambiente de teste. Quando você seleciona essa opção, a instalação executa as seguintes ações:  
        > 
        > - Configura automaticamente o site como um site primário autônomo.  
        > - Usa um caminho de instalação padrão.  
        > - Usa uma instalação local da instância padrão do SQL Server para o banco de dados do site.  
        > - Instala um ponto de gerenciamento e um ponto de distribuição no computador do servidor do site.  
        > - Configura o site com o idioma inglês e o idioma de exibição do sistema operacional no servidor do site primário, se ele corresponder a um dos idiomas a que o Configuration Manager dá suporte.  

4. Na página **Chave do Produto (Product Key)**:  

    - escolha se deseja instalar o Configuration Manager como uma edição de avaliação ou uma edição licenciada.  

        - Se você selecionar uma edição licenciada, insira a chave do produto (Product Key) e escolha **Avançar**.  

        - Se você selecionar uma edição de avaliação, escolha **Avançar**. (Você pode atualizar uma instalação de avaliação para uma instalação completa posteriormente.)  

    - Você também pode especificar a **data de expiração do Software Assurance** do seu contrato de licença. É um lembrete conveniente dessa data. Se não inserir essa data durante a Instalação, você poderá especificá-la posteriormente no console do Configuration Manager.  

        > [!NOTE]   
        > A Microsoft não valida a data de validade inserida e não usa essa data para validação da licença. Você pode usá-la como um lembrete da data de vencimento. Esta data é útil porque o Configuration Manager verifica periodicamente as novas atualizações de software oferecidas online. O status de licença do software assurance deve estar atualizado para que você possa usar essas atualizações adicionais.    

    Para obter mais informações, veja [Licenciamento e branches](/sccm/core/understand/learn-more-editions).  

5. Na página **Termos de Licença para Software Microsoft** , leia e aceite os termos de licença.  

6. Na página **Licenças de Pré-requisito** , leia e aceite os termos de licença do software de pré-requisito. A Instalação baixa e instala automaticamente o software nos clientes ou sistemas do site quando necessário. Aceite todos os termos antes de prosseguir para a próxima página.  

7. Na página **Downloads de Pré-requisitos**, especifique se a instalação deve baixar os arquivos redistribuíveis de pré-requisitos mais recentes da Internet ou usar os arquivos baixados anteriormente:  

    - Se você desejar que a instalação baixe os arquivos neste momento, selecione **Baixar arquivos necessários**. Em seguida, especifique um local para armazenar os arquivos.  

    - Se você tiver baixado os arquivos usando o [Downloader de Instalação](/sccm/core/servers/deploy/install/setup-downloader), selecione **Usar arquivos baixados anteriormente**. Em seguida, especifique a pasta de download.  

        > [!TIP]  
        > Se você usar os arquivos baixados anteriormente, verifique se o caminho para a pasta de download contém a versão mais recente dos arquivos.  

8. Na página **Seleção do Idioma do Servidor**, selecione os idiomas que estão disponíveis para o console do Configuration Manager e para os relatórios. (O inglês é selecionado por padrão e não pode ser removido.) Para saber mais, [Pacotes de idiomas](/sccm/core/servers/deploy/install/language-packs).  

9. Na página **Seleção de Idioma do Cliente**, selecione os idiomas disponíveis para computadores clientes. Além disso, especifique se deseja habilitar todos os idiomas do cliente para clientes de dispositivos móveis. (O inglês é selecionado por padrão e não pode ser removido.)  

    > [!IMPORTANT]  
    > Quando usar um site de administração central, verifique se os idiomas do cliente que você configurou no site de administração central incluem todos os idiomas do cliente que você configurou em cada site primário filho. Os clientes instalados por meio de um ponto de distribuição têm acesso aos idiomas do cliente por meio do site de nível superior, enquanto os clientes que são instalados de um ponto de gerenciamento têm acesso aos idiomas do cliente por meio do site primário atribuído a eles.  

10. Na página **Configurações do Site e de Instalação**, especifique as seguintes configurações para o novo site que você está instalando:  

    - **Código do site**: [O código de cada site em uma hierarquia deve ser exclusivo](/sccm/core/servers/deploy/install/prepare-to-install-sites#bkmk_sitecodes). Use três dígitos alfanuméricos: A até Z e 0 a 9. Como o código do site é usado em nomes de pasta, não use nomes reservados do Windows, incluindo:    
        - AUX  
        - CON    
        - NUL    
        - PRN    
        - SMS  

        > [!NOTE]  
        > A instalação não verifica se o código do site especificado já está em uso ou se é um nome reservado.  

    - **Nome do site**: cada site exige esse nome amigável, que pode ajudá-lo a identificar o site.  

    - **Pasta de instalação**: esse é o caminho para a instalação do Configuration Manager. Você não pode alterar o local depois de instalar o site. O caminho não pode conter espaços à direita ou caracteres Unicode.  

11. Na página **Instalação do Site**, use a opção a seguir que corresponde ao seu cenário:  

    - **Estou instalando um site de administração central:**  

        Na página **Instalação do Site de Administração Central**, selecione **Instalar como o primeiro site em uma nova hierarquia** e escolha **Avançar** para continuar.  

    - **Estou expandindo um site primário autônomo em uma hierarquia com um site de administração central:**  

        Na página **Instalação do Site de Administração Central**, selecione a opção **Expandir um autônomo primário existente em uma hierarquia**. Em seguida, especifique o FQDN do servidor do site primário autônomo e escolha **Avançar** para continuar.  

        A mídia que você usa para instalar o novo site de administração central deve corresponder à versão do site primário.  

    - **Estou instalando um site primário autônomo:**  

        Na página **Instalação de Site Primário**, selecione **Instalar o site primário como site autônomo** e escolha **Avançar**.  

    - **Estou instalando um site primário filho:**  

        Na página **Instalação de Site Primário**, selecione **Ingressar o site primário a uma hierarquia existente**. Depois, especifique o FQDN do site de administração central e escolha **Avançar**.  

12. Na página **Informações do Banco de Dados**, especifique as informações a seguir:  

    - **Nome do SQL Server (FQDN)**: por padrão, esse valor é definido como o computador do servidor do site.  

        Se você usar uma porta personalizada, adicione-a ao FQDN do SQL Server. Coloque uma vírgula e depois o número da porta após o FQDN do SQL Server. Por exemplo, para o servidor *SQLServer1.fabrikam.com*, use o seguinte para especificar a porta *1551*: `SQLServer1.fabrikam.com,1551`  

    - **Nome da instância**: por padrão, esse valor está em branco. Ele usa a instância padrão do SQL no computador do servidor do site.  

    - **Nome do banco de dados**: Por padrão, esse valor é definido como `CM_<Sitecode>`. Você pode personalizar esse valor.  

    - **Porta do Service Broker:** por padrão, esse valor é definido para usar a porta padrão do SSB (Server Service Broker) do SQL, 4022. O SQL a usa para se comunicar diretamente com o banco de dados do site em outros sites.  

13. Na segunda página **Informações do Banco de Dados**, você pode especificar locais personalizados para o arquivo de dados do SQL Server e o arquivo de log do SQL Server para o banco de dados do site:  

    - Por padrão, ele usa locais de arquivo padrão para o SQL Server.  

    - Quando você usa um cluster do SQL Server, a opção de especificar locais de arquivo personalizados não fica disponível.  

    - O verificador de pré-requisitos não executa uma verificação de espaço livre em disco para locais de arquivo personalizados.  

14. Na página **Configurações do Provedor de SMS** , especifique o FQDN para o servidor no qual você deseja instalar o provedor de SMS.  

    - Por padrão, ele especifica o servidor do site.  

    - Depois de instalar o site, você pode configurar outros Provedores de SMS. Para obter mais informações, veja [Planejar para o provedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).  

15. Na página **Configurações de Comunicação do Cliente** , escolha se é para configurar todos os sistemas de sites para aceitar somente a comunicação HTTPS de clientes ou se o método de comunicação deve ser configurado para cada função do sistema de sites.  

    Ao selecionar **Todas as funções do sistema de sites aceitam apenas comunicação HTTPS de clientes**, o computador cliente deverá ter um certificado PKI válido para autenticação do cliente. Para obter mais informações, veja [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

    > [!NOTE]  
    > Esta etapa se aplica somente quando você instala um site primário. Se você estiver instalando um site de administração central, ignore esta etapa.  

16. Na página **Funções do Sistema de Site** , escolha se é para instalar um ponto de gerenciamento ou um ponto de distribuição. Para cada função que você opta que o programa de Instalação instale:  

    - Insira o **FQDN** para o servidor que hospedará a função. Em seguida, escolha o método de conexão de cliente ao qual o servidor dará suporte: HTTP ou HTTPS.  

    - Se você selecionou **Todas as funções do sistema de sites aceitam apenas comunicação HTTPS de clientes** na página anterior, as definições de conexão do cliente serão automaticamente configuradas para HTTPS. Não será possível alterar essa configuração a menos que você para a página anterior.  

    > [!NOTE]  
    > Esta etapa se aplica somente quando você instala um site primário. Se você estiver instalando um site de administração central, ignore esta etapa.  

    > [!NOTE]  
    > Para instalar funções do sistema de sites, a instalação usa a **conta de instalação do sistema de sites**. Por padrão, a conta de computador do site primário é usada. Para instalar a função do sistema de sites, essa conta deve ser um administrador local em um computador remoto. Se essa conta não tiver as permissões necessárias, desmarque as funções do sistema de sites e instale-as mais tarde usando o console do Configuration Manager depois de configurar contas adicionais a serem usadas como contas de instalação do sistema de sites. Para saber mais, confira [Contas](/sccm/core/plan-design/hierarchy/accounts#site-system-installation-account).  

17. Na página **Dados de Uso**, examine as informações sobre os dados que a Microsoft coleta e escolha **Avançar**. Para obter mais informações, consulte [Dados de diagnóstico e de uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  

18. A página **Instalação do Ponto de Conexão de Serviço** fica disponível apenas durante os cenários a seguir:  

    - Quando você estiver instalando um site primário autônomo.  

    - Quando você estiver instalando um site de administração central.  

    > [!NOTE]  
    > Se você estiver instalando um site primário filho, ignore esta etapa.  

     Se você estiver instalando um site de administração central como parte de um cenário de expansão do site e essa função já estiver instalada no site primário autônomo, primeiro desinstale a função do site primário autônomo. Apenas uma instância dessa função é permitida em uma hierarquia, e ela tem suporte no site da camada superior da hierarquia.  

     Depois de selecionar uma configuração para o **Ponto de Conexão de Serviço**, escolha **Avançar**. Após a conclusão da Instalação, você poderá alterar essa configuração no console do Configuration Manager. Para obter mais informações, consulte [Sobre o ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point).  

19. Na página **Resumo das Configurações**, examine as configurações que você selecionou. Quando você estiver pronto, escolha **Avançar** para iniciar o Verificador de Pré-requisitos.  

20. A página **Verificação de Instalação de Pré-requisitos** mostra todos os problemas que podem ser identificados.  

    - Quando o Verificador de Pré-requisitos encontrar um problema, escolha um item da lista para exibir os detalhes sobre como solucionar o problema.  

    - Antes de poder continuar a instalação do site, resolva os itens com **Falha**. Resolva também os itens com status de **Aviso**, mas eles não bloqueiam a instalação do site.  

    - Depois de resolver os problemas, escolha **Executar Verificação** para executar novamente o Verificador de Pré-requisitos.  

        Se o Verificador de Pré-requisitos for executado e nenhuma verificação receber um status de **Falha**, você poderá escolher **Iniciar Instalação** para iniciar a instalação do site.  

    > [!TIP]  
    > Além dos comentários fornecidos pelo assistente, encontre outras informações sobre problemas de pré-requisito no arquivo **ConfigMgrPrereq.log**. Ele está na raiz da unidade do sistema do computador no qual você está instalando o site. Para saber mais, confira a [Lista de verificações de pré-requisitos](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).  

21. Na página **Instalação** , o programa de instalação exibe o status da instalação. Quando a instalação do servidor do site principal for concluída, você poderá **Fechar** o assistente para instalação. Quando você fecha o assistente, a instalação e as configurações iniciais do site continuam em segundo plano.  

    - Você pode conectar um console do Configuration Manager ao site antes de a Instalação ser concluída. Esse console se conecta no modo somente leitura e permite a exibição de objetos e de configurações, mas você não pode fazer modificações.  

    - Após a conclusão da instalação, você poderá conectar um console que permite a edição de objetos e de configurações.  



## <a name="bkmk_expand"></a> Expandir um site primário autônomo

Ao instalar um site primário autônomo como seu primeiro site, você tem a opção de expandir posteriormente o site em uma hierarquia maior instalando um site de administração central.   

Ao expandir um site primário autônomo, você pode instalar um novo site de administração central que usa o banco de dados do site primário autônomo existente como referência. Depois de instalar o novo site de administração central, o site primário autônomo funciona como um site primário filho.

- Você só pode expandir um site primário autônomo em uma nova hierarquia.  

- Você só pode expandir um site primário autônomo em uma hierarquia específica. Você não pode usar essa opção para adicionar mais sites primários autônomos à mesma hierarquia. Em vez disso, use o Assistente de Migração para migrar dados de uma hierarquia para outra. Para saber mais, confira [Migrar dados entre hierarquias](/sccm/core/migration/migrate-data-between-hierarchies).  

- Depois de expandir um site autônomo em uma hierarquia com um site de administração central, você pode adicionar mais sites primários filhos.  

- Para remover um site primário de uma hierarquia com um site de administração central, primeiro desinstale o site primário.  


Para expandir o site, use o Assistente para Instalação do Configuration Manager para instalar um novo site de administração central com as seguintes condições:  

- Instale o site de administração central usando a mesma versão do Configuration Manager que o site primário autônomo.  

- Na página de **Introdução** do Assistente de Instalação, selecione a opção para instalar um site de administração central. Em um estágio posterior da Instalação, você escolherá uma opção para expandir um site primário autônomo existente.  

- Ao configurar a página **Seleção do Idioma do Cliente** para o novo site de administração central, selecione os mesmos idiomas do cliente que estão configurados para o site primário autônomo que você está expandindo.  

- Na página **Instalação do Site**, selecione a opção para expandir o site primário autônomo.  


Para expandir o site primário autônomo, primeiro selecione os [Pré-requisitos para expandir um site](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand). Depois, use o procedimento [Para instalar um site de administração central ou primário](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_installpri) anteriormente neste artigo.




## <a name="bkmk_secondary"></a> Instalar um site secundário

Use o console do Configuration Manager para instalar um site secundário.  

- Se o console usado não estiver conectado ao site primário que será o site pai do novo site secundário, o comando para instalar o site será replicado para o site primário correto.  

- Antes de iniciar a instalação do site, verifique se a sua conta de usuário tem as permissões de pré-requisito. Além disso, verifique se o servidor que hospedará o novo site secundário cumpre todos os pré-requisitos de uso como um servidor do site secundário.  

- Quando você instala o site secundário, o Configuration Manager configura o novo site para usar as portas de comunicação do cliente configuradas no site primário pai.  


### <a name="bkmk_installsecondary"></a> Processo para instalar um site secundário  

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**. Selecione o site que será o site primário pai do novo site secundário.  

2. Para iniciar o **Assistente para Criar Site Secundário**, escolha **Criar Site Secundário**.  

3. Na página **Antes de Começar**, confirme se o site primário listado é o site que você deseja que seja o pai do novo site secundário. Em seguida, escolha **Avançar**.  

4. Na página **Geral** , especifique as seguintes configurações:  

    - **Código do site**: O código de cada site em uma hierarquia deve ser exclusivo. Use três dígitos alfanuméricos: A até Z e 0 a 9. Como o código do site é usado em nomes de pasta, não use nomes reservados do Windows, incluindo:  

        - AUX    
        - CON    
        - NUL    
        - PRN  
        - SMS  

    > [!NOTE]  
    > A instalação não verifica se o código do site especificado já está em uso ou se é um nome reservado.  

    - **Nome do servidor do site**: esse valor é o FQDN do servidor no qual o novo site secundário será instalado.  

    - **Nome do site**: cada site exige esse nome amigável, que pode ajudá-lo a identificar o site.  

    - **Pasta de instalação**: esse é o caminho para a instalação do Configuration Manager. Você não pode alterar o local depois de instalar o site. O caminho não pode conter espaços à direita ou caracteres Unicode.  

    > [!IMPORTANT]  
    > Depois de especificar os detalhes nesta página, escolha **Resumo** para acessar diretamente a página **Resumo** do assistente. Essa ação usa as configurações padrão para o restante das opções de site secundário.  
    > 
    > - Use essa opção apenas quando estiver familiarizado com as configurações padrão deste assistente, e elas forem as configurações que você deseja usar.  
    > - Quando você usa as configurações padrão, os grupos de limites não são associados ao ponto de distribuição. Até que você configure grupos de limites que incluam o servidor do site secundário, os clientes não usarão o ponto de distribuição que está instalado no site secundário como um local de origem do conteúdo.  

5. Na página **Arquivos de Origem de Instalação** , escolha como o computador do site secundário obtém os arquivos de origem para instalar o site.  

    Quando você usa arquivos de origem CD.Latest compartilhados na rede ou copiados localmente no servidor do site secundário de destino:  

    - **Windows 1802 e anterior**

        - O local do arquivo de origem CD.Latest inclui uma pasta denominada **Redist**. Mova essa pasta **Redist** como uma subpasta sob a pasta **SMSSETUP**.  

            > [!Note]  
            > Se ocorrerem erros de incompatibilidade de hash durante a instalação, atualize a pasta **Redist**. Use o [Downloader de Instalação](/sccm/core/servers/deploy/install/setup-downloader) para obter os arquivos mais recentes. Para todos os arquivos que causam um erro de incompatibilidade de hash, copie-os também da pasta **Redist** atualizada para a pasta **SMSSETUP\BIN\X64**. 

    - **Versão 1806 e posterior**<!-- SCCMDocs-pr issue 3164 -->

        - O local do arquivo de origem CD.Latest inclui uma pasta denominada **Redist**. Mova essa pasta **Redist** como uma subpasta sob a pasta **SMSSETUP**.  

        - Copie os seguintes arquivos da pasta **Redist** para a pasta **SMSSETUP\BIN\X64**:   
            - SharedManagementObjects.msi
            - SQLSysClrTypes.msi
            - sqlncli.msi

    - Se qualquer um dos arquivos de **Redist** não estiver disponível, haverá falha na instalação do site secundário.  

    - A conta de computador do servidor do site secundário deve ter permissões de **Leitura** para o compartilhamento e a pasta do arquivo de origem.  

6. Na página **Configurações do SQL Server** , especifique a versão do SQL Server a ser usada e defina as configurações relacionadas.  

    > [!NOTE]  
    > A Instalação não valida as informações inseridas nesta página até que se inicie a instalação. Antes de prosseguir, verifique essas configurações.  

    - **Instalar e configurar uma cópia local do SQL Express no computador do site secundário**  

        - **Porta de serviço do SQL Server**: especifique a porta de serviço do SQL Server a ser usada pelo SQL Server Express. A porta de serviço geralmente é configurada para usar a porta TCP 1433, mas você pode configurar outra porta.  

        - **Porta do SQL Server Broker**: especifique a porta do SQL Server Service Broker (SSB) a ser usada pelo SQL Server Express. O Service Broker geralmente é configurado para usar a porta TCP 4022, mas você pode configurar outra porta. Especifique uma porta válida que nenhum outro site ou serviço esteja usando e que nenhuma restrição de firewall esteja bloqueando.  

    - **Usar uma instância existente do SQL Server**  

        - **FQDN do SQL Server**: examine o FQDN do computador que está executando o SQL Server. É necessário usar um servidor local executando o SQL Server para hospedar o banco de dados do site secundário e não é possível modificar essa configuração.  

        - **Instância do SQL Server**: especifique a instância do SQL Server a ser usada como o banco de dados do site secundário. Deixe essa opção em branco para usar a instância padrão.  

        - **Nome do banco de dados do site do ConfigMgr**: especifique o nome para o banco de dados do site secundário.  

        - **Porta do SQL Server Broker**: especifique a porta do SQL Server Service Broker (SSB) a ser usada pelo SQL Server. É necessário especificar uma porta válida que nenhum outro site ou serviço esteja usando, e sem bloqueio por restrições de firewall.  

    > [!TIP]  
    > Para obter uma lista das versões de SQL Server com suporte do System Center Configuration Manager confira [Versões do SQL Server com suporte](/sccm/core/plan-design/configs/support-for-sql-server-versions).  

7. Na página **Ponto de Distribuição** , defina as configurações para o ponto de distribuição que será instalado no servidor do site secundário.  

    - **Configurações obrigatórias:**  

        - **especifique como os dispositivos clientes se comunicam com o ponto de distribuição**: escolha entre HTTP e HTTPS.  

        - **Criar um certificado autoassinado ou importar um certificado de cliente PKI**: Escolha entre usar um certificado autoassinado ou importar um certificado do PKI. Um certificado autoassinado permite conexões anônimas de clientes do Configuration Manager à biblioteca de conteúdo. Esse certificado é usado para autenticar o ponto de distribuição para um ponto de gerenciamento antes que o ponto de distribuição envie mensagens de status. Para obter mais informações, veja [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

    - **Configurações opcionais:**  

        - **Instalar e configurar o IIS se exigido pelo Configuration Manager**: selecione esta configuração para permitir que o Configuration Manager instale e configure o IIS (Serviços de Informações da Internet) no servidor se ele ainda não estiver instalado. O IIS é necessário em todos os pontos de distribuição.  

            > [!NOTE]  
            > Embora essa configuração seja opcional, o IIS deve ser instalado no servidor antes de um ponto de distribuição ser instalado com êxito.  

        - **Habilitar e configurar o BranchCache para este ponto de distribuição**  

        - **Descrição**: Esse valor é uma descrição amigável do ponto de distribuição para ajudá-lo a reconhecê-lo.  

        - **Habilitar este ponto de distribuição para conteúdo pré-configurado**  

8. Na página **Configurações de Unidade** , especifique as configurações da unidade para o ponto de distribuição do site secundário.  

    Você pode configurar até duas unidades de disco para a biblioteca de conteúdo e duas unidades de disco para o compartilhamento de pacote. No entanto, o Configuration Manager pode usar outras unidades quando as duas primeiras atingirem a reserva de espaço de unidade configurada. A página **Configurações de Unidade** é o local em que você configura a prioridade das unidades de disco e a quantidade de espaço livre em disco a permanecer em cada unidade de disco.  

    - **Reserva de espaço na unidade (MB)**: o valor que você define para esta configuração determina a quantidade de espaço livre na unidade antes que o Configuration Manager escolha uma unidade diferente e continue o processo de cópia nessa unidade. Arquivos de conteúdo podem abranger várias unidades.  

    - **Localizações de conteúdo**: Especifique os locais de conteúdo para a biblioteca de conteúdo e o compartilhamento de pacotes. O Configuration Manager copia conteúdo para o local de conteúdo primário até que a quantidade de espaço livre atinja o valor especificado para **Reserva de espaço de unidade (MB)**.  

    Por padrão, os locais de conteúdo são definidos para **Automático**. O local do conteúdo primário é definido como a unidade de disco com mais espaço em disco no momento da instalação. O local secundário é definido como a unidade de disco que tem o maior espaço em disco após a unidade primária. Quando as unidades primárias e secundárias atingirem a reserva de espaço de unidade, o Configuration Manager selecionará outra unidade disponível com o maior espaço em disco e continuará o processo de cópia.  

9. Na página **Validação de Conteúdo** , especifique se a integridade dos arquivos de conteúdo no ponto de distribuição deve ser validada.  

    - Quando você habilita a validação de conteúdo segundo um agendamento, o Configuration Manager inicia o processo no horário agendado. Todo o conteúdo no ponto de distribuição é verificado.  

    - Também é possível configurar a **Prioridade de validação de conteúdo**.  

    - Para exibir os resultados do processo de validação de conteúdo, no console do Configuration Manager, acesse o espaço de trabalho **Monitoramento**, expanda **Status da Distribuição** e selecione o nó **Status do Conteúdo**. Isso exibe o conteúdo de cada tipo de pacote. Esses tipos incluem aplicativos, pacotes de atualização de software e imagens de inicialização.  

10. Na página **Grupos de Limite**, gerencie os grupos de limite aos quais esse ponto de distribuição está atribuído:  

    - Durante a implantação do conteúdo, os clientes devem estar em um grupo de limites associado ao ponto de distribuição para usá-lo como um local de origem para conteúdo.  

    - Você pode selecionar a opção **Permitir local de origem de fallback para conteúdo** para permitir que clientes fora desses grupos de limites façam fallback e usem o ponto de distribuição como um local de origem para conteúdo quando não houver disponíveis pontos de distribuição preferenciais.  

        Para saber mais, confira [Conceitos fundamentais para o gerenciamento de conteúdo](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).  

11. Na página **Resumo**, verifique as configurações e escolha **Avançar** para instalar o site secundário. Quando o assistente apresentar a página **Conclusão**, você poderá fechar o assistente. A instalação do site secundário continua em segundo plano.  


### <a name="bkmk_verify"></a> Como verificar o status da instalação do site secundário  

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**.  

2. Selecione o site secundário que você está instalando e escolha **Mostrar Status da Instalação** na faixa de opções.  

    > [!TIP]  
    > Quando você instala mais de um site secundário de cada vez, o Verificador de Pré-requisitos é executado em um único site por vez. Ele deve ser concluído antes de iniciar a verificação do próximo site.  

