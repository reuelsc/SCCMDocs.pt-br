---
title: "Opções de linha de comando de instalação | Microsoft Docs"
description: "Use as informações neste artigo para configurar scripts ou instalar o System Center Configuration Manager de uma linha de comando."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: f2b5a1dfa654a30e03bce2b56100bc876358c9fe

---
# <a name="command-line-options-for-setup-for-system-center-configuration-manager"></a>Opções de linha de comando para instalação do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


 Use as informações nas tabelas a seguir ao configurar scripts ou instalar o System Center Configuration Manager de uma linha de comando.  

##  <a name="a-namebkmksetupa-command-line-options-for-setup"></a><a name="bkmk_setup"></a> Opções de linha de comando para instalação  
 **/DEINSTALL**  
 Desinstala o site. É necessário executar a Instalação no computador de servidor do site.  

 **/DONTSTARTSITECOMP**  
 Instala um site, mas impede que o serviço do Gerenciador de Componentes do Site seja iniciado. Até que o serviço do Gerenciador de Componentes do Site seja iniciado, o site não ficará ativo. O Gerenciador de Componentes do Site é responsável por instalar e iniciar o serviço SMS_Executive e processos adicionais no site. Após a conclusão da instalação do site, ao iniciar o serviço do Gerenciador de Componentes do Site, ele instalará o SMS_Executive e os processos adicionais necessários para que o site funcione.  

 **/HIDDEN**  
 Oculta a interface do usuário durante a instalação. Essa opção deve ser usada em conjunto com a opção **/SCRIPT** e o arquivo de script autônomo deve fornecer todas as opções necessárias, caso contrário, a instalação falhará.  

 **/NOUSERINPUT**  
 Desativa a entrada do usuário durante a Instalação, mas exibe a interface do **Assistente de Instalação** . Essa opção deve ser usada em conjunto com a opção **/SCRIPT** e o arquivo de script autônomo deve fornecer todas as opções necessárias, caso contrário, a instalação falhará.  

 **/RESETSITE**  
 Executa uma redefinição de site que redefine o banco de dados e as contas de serviço do site. É necessário executar a Instalação em **&lt;ConfigMgrInstallationPath\>\BIN\X64** no servidor do site. Para obter mais informações sobre a redefinição de site, consulte a seção [Executar uma redefinição de site](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_reset) no tópico [Modificar a infraestrutura do System Center Configuration Manager](../../../../core/servers/manage/modify-your-infrastructure.md).  

 **/TESTDBUPGRADE &lt;*NomeDaInstância\NomeDoBancoDeDados*>**  
 Executa um teste em um backup do banco de dados do site para garantir que ele seja capaz de fazer uma atualização. É necessário fornecer o nome da instância e o nome de banco de dados para o banco de dados do site. Se você especificar somente o nome do banco de dados, a Instalação usará o nome padrão da instância.  

> [!IMPORTANT]  
>  Não há suporte para executar essa opção de linha de comando no banco de dados do site de produção. Isso atualiza o banco de dados do site e pode deixar o site inoperante.  

 **/UPGRADE**  
 Executa a atualização autônoma de um site. Ao usar /UPGRADE, é necessário especificar a chave do produto, incluindo os traços (-). Além disso, é necessário especificar o caminho para os arquivos de pré-requisito da Instalação baixados anteriormente.  

 Exemplo: **setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx &lt;caminho para arquivos de componente externos\>**  

 Para obter informações sobre os arquivos de pré-requisitos da instalação, consulte  [Downloader de Instalação](#bkmk_SetupDownloader) neste tópico.  

 **/SCRIPT &lt;*SetupScriptPath*>**  
 executa instalações autônomas. É necessário ter um arquivo de inicialização da Instalação ao usar a opção **/SCRIPT**. Para obter mais informações sobre como executar a Instalação autônoma, consulte a seção [Instalar sites usando uma linha de comando](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).  

 **/SDKINST &lt;*FQDN*>**  
 Instala o Provedor de SMS no computador especificado. É necessário fornecer o FQDN para o computador do Provedor de SMS. Para obter mais informações sobre o Provedor de SMS, consulte [Planejar o Provedor de SMS para o System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

 **/SDKDEINST &lt;*FQDN*>**  
 Desinstala o Provedor de SMS do computador especificado. É necessário fornecer o FQDN para o computador do Provedor de SMS.  

 **/MANAGELANGS &lt;*LanguageScriptPath*>**  
 gerencia os idiomas instalados em um site instalado anteriormente. Para usar esta opção, é necessário executar a Instalação em **&lt;ConfigMgrInstallationPath\>\BIN\X64** no servidor do site e fornecer o local do arquivo de script de idioma que contém as configurações de idioma. Para obter mais informações sobre as opções de idioma disponíveis no arquivo de script de instalação de idioma, consulte [Opções de linha de comando para gerenciar idiomas](#bkmk_Lang) neste tópico.  

##  <a name="a-namebkmklanga-command-line-options-to-manage-languages"></a><a name="bkmk_Lang"></a> Opções de linha de comando para gerenciar idiomas  
 **Identificação**  

-   **Nome da chave:** Action  

    -   **Obrigatória:** Sim  

    -   **Valores:** ManageLanguages  

    -   **Detalhes:** gerencia o servidor, o cliente e o suporte ao idioma do cliente móvel em um site.  

**Opções**  

-   **Nome da chave:** AddServerLanguages  

    -   **Obrigatória:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** especifica os idiomas do servidor que estarão disponíveis para o console do Configuration Manager, relatórios e objetos do Configuration Manager. Inglês está disponível por padrão.  

-   **Nome da chave:** AddClientLanguages  

    -   **Obrigatória:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Details:** especifica os idiomas que estarão disponíveis para computadores cliente. Inglês está disponível por padrão.  

-   **Nome da chave:** DeleteServerLanguages  

    -   **Obrigatória:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** especifica os idiomas para remoção, que não estarão mais disponíveis para o console do Configuration Manager, relatórios e objetos do Configuration Manager. Inglês está disponível por padrão e não pode ser removido.  

-   **Nome da chave:** DeleteClientLanguages  

    -   **Obrigatória:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** especifica os idiomas a serem removidos e que não estarão mais disponíveis para computadores cliente. Inglês está disponível por padrão e não pode ser removido.  

-   **Nome da chave:** MobileDeviceLanguage  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = não instalar  

         1 = instalar  

    -   **Detalhes:** especifica se os idiomas do cliente do dispositivo móvel estão instalados.  

-   **Nome da chave:** PrerequisiteComp  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = baixar  

         1 = já baixado  

    -   **Detalhes:** especifica se os arquivos de pré-requisito da Instalação já foram baixados. Por exemplo, se você usar o valor 0, a Instalação baixará os arquivos.  

-   **Nome da chave:** PrerequisitePath  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Detalhes:** especifica o caminho para os arquivos de pré-requisito da Instalação. Dependendo do valor do **PrerequisiteComp** , a Instalação usará esse caminho para armazenar arquivos baixados ou para localizar arquivos baixados anteriormente.  

##  <a name="a-namebkmkunattendeda-unattended-setup-script-file-keys"></a><a name="bkmk_Unattended"></a> Chaves de arquivo de script da instalação autônoma  
 Use as seções a seguir para ajudá-lo a criar seu script para a Instalação autônoma. As tabelas listam as chaves de script de instalação disponíveis, seus valores correspondentes, se são necessárias, em que tipo de instalação são usadas e uma descrição breve da chave.  

### <a name="unattended-install-for-a-central-administration-site"></a>Instalação autônoma de um site de administração central  
 Use os detalhes a seguir para instalar um site de administração central usando um arquivo de script de Instalação autônoma.  

**Identificação**  

-   **Nome da chave:** Action  

    -   **Obrigatória:** Sim  

    -   **Valores:** InstallCAS  

    -   **Detalhes:** instala um site de administração central.  

**Opções**  

-   **Nome da chave:** ProductID  

    -   **Obrigatória:** Sim  

    -   **Valores:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* ou *Eval*  

    -   **Detalhes:** especifica a chave do produto (Product Key) de instalação do Configuration Manager, incluindo os traços. Insira **Eval** para instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** SiteCode  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*SiteCode*>  

    -   **Detalhes:** especifica três caracteres alfanuméricos que identificam de forma exclusiva o site na hierarquia.  

-   **Nome da chave:** SiteName  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*SiteName*>  

    -   **Detalhes:** especifica o nome do site.  

-   **Nome da chave:** SMSInstallDir  

    -   **Obrigatória:** Sim  

    -   **Valores:** *ConfigMgrInstallationPath*  

    -   **Detalhes:** especifica a pasta de instalação dos arquivos de programa do Configuration Manager.  

-   **Nome da chave:** SDKServer  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*FQDN do Provedor de SMS*>  

    -   **Detalhes:** especifica o FQDN para o servidor que hospedará o Provedor de SMS.  
        Você pode configurar outros Provedores de SMS para o site após a instalação inicial.  

-   **Nome da chave:** PrerequisiteComp  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = baixar  

         1 = já baixado  

    -   **Detalhes:** especifica se os arquivos de pré-requisito da Instalação já foram baixados. Por exemplo, se você usar o valor 0, a Instalação baixará os arquivos.  

-   **Nome da chave:** PrerequisitePath  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Detalhes:** especifica o caminho para os arquivos de pré-requisito da Instalação. Dependendo do valor do PrerequisiteComp, a Instalação usará esse caminho para armazenar arquivos baixados ou para localizar arquivos baixados anteriormente.  

-   **Nome da chave:** AdminConsole  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = não instalar  

         1 = instalar  

    -   **Detalhes:** especifica se deseja instalar o console do Configuration Manager.  

-   **Nome da chave:** JoinCEIP  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = não ingressar  

         1 = ingressar  

    -   **Detalhes:** especifica se deve ingressar no Programa de Aperfeiçoamento da Experiência do Usuário.  

-   **Nome da chave:** AddServerLanguages  

    -   **Obrigatória:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** especifica os idiomas do servidor que estarão disponíveis para o console do Configuration Manager, relatórios e objetos do Configuration Manager. Inglês está disponível por padrão.  

-   **Nome da chave:** AddClientLanguages  

    -   **Obrigatória:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Details:** especifica os idiomas que estarão disponíveis para computadores cliente. Inglês está disponível por padrão.  

-   **Nome da chave:** DeleteServerLanguages  

    -   **Obrigatória:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** modifica um site após sua instalação.  
        Especifica os idiomas para remoção e que não estarão mais disponíveis para o console do Configuration Manager, relatórios e objetos do Configuration Manager. Inglês está disponível por padrão e não pode ser removido.  

-   **Nome da chave:** DeleteClientLanguages  

    -   **Obrigatória:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** modifica um site após sua instalação.  
        Especifica os idiomas a serem removidos e que não estarão mais disponíveis para computadores cliente. Inglês está disponível por padrão e não pode ser removido.  

-   **Nome da chave:** MobileDeviceLanguage  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = não instalar  

         1 = instalar  

    -   **Detalhes:** especifica se os idiomas do cliente do dispositivo móvel estão instalados.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Obrigatória:** Sim  

    -   **Valores:** *SQLServerName*  

    -   **Detalhes:** especifica o nome do servidor ou o nome da instância clusterizada que está executando o SQL Server. Ele irá hospedar o banco de dados do site.  

-   **Nome da chave:** DatabaseName  

    -   **Obrigatória:** Sim  

    -   **Valores:** *&lt;SiteDatabaseName\>* ou *&lt;InstanceName\>\&lt;SiteDatabaseName\>*  

    -   **Detalhes:**  

         Especifica o nome do banco de dados do SQL Server a ser criado ou usado para instalar o banco de dados do site de administração central.  

        > [!IMPORTANT]  
        >  Você deverá especificar o nome da instância e o nome do banco de dados do site se você não usar a instância padrão.  

-   **Nome da chave:** SQLSSBPort  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*SSBPortNumber*>  

    -   **Detalhes:** especifica a porta do SQL SSB (Server Service Broker) a ser usada pelo SQL Server. Normalmente, o SSB está configurado para usar a porta TCP 4022, mas há suporte para outras portas.  

-   **Nome da chave:** SQLDataFilePath  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*FilePath para o arquivo .MDB do banco de dados*>  

    -   **Detalhes:** especifica um local alternativo para criar o arquivo .MDB do banco de dados.  

-   **Nome da chave:** SQLLogFilePath  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*FilePath para o arquivo .LDF do banco de dados*>  

    -   **Detalhes:** especifica um local alternativo para criar o arquivo .LDF do banco de dados.  

**CloudConnectorOptions**  

-   **Nome da chave:** CloudConnector  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = não instalar  

         1 = instalar  

    -   **Detalhes:** especifica se você instalará um ponto de conexão de serviço no site. Como o ponto de conexão de serviço pode ser instalado somente no site de nível superior de uma hierarquia, esse valor deverá ser 0 para um site primário filho.  

-   **Nome da chave:** CloudConnectorServer  

    -   **Obrigatória:** obrigatória quando CloudConnector for igual a 1  

    -   **Valores:** &lt;*FQDN do servidor de ponto de conexão do serviço*>  

    -   **Detalhes:** especifica o FQDN do servidor que hospedará a função do sistema de sites do ponto de conexão do serviço.  

-   **Nome da chave:** UseProxy  

    -   **Obrigatória:** obrigatória quando CloudConnector for igual a 1  

    -   **Valores:** 0 ou 1  

         0 = não instalar  

         1 = instalar  

    -   **Detalhes:** especifica se o ponto de conexão do serviço usará um servidor proxy.  

-   **Nome da chave:** ProxyName  

    -   **Obrigatória:** obrigatória quando UseProxy for igual a 1  

    -   **Valores:** &lt;*FQDN do servidor proxy*>  

    -   **Detalhes:** especifica o FQDN do servidor proxy que será usado pela função do sistema de sites do ponto de conexão do serviço.  

-   **Nome da chave:** ProxyPort  

    -   **Obrigatória:** obrigatória quando UseProxy for igual a 1  

    -   **Valores:** &lt;*PortNumber*>  

    -   **Detalhes:** especifica o número da porta a ser usado.  

### <a name="unattended-install-for-a-primary-site"></a>Instalação autônoma de um site primário  
Use os detalhes a seguir para instalar um site primário usando um arquivo de script de Instalação autônoma.  

Use os detalhes a seguir para instalar um site de administração central usando um arquivo de script de Instalação autônoma.  

**Identificação**  

-   **Nome da chave:** Action  

    -   **Obrigatória:** Sim  

    -   **Valores:** InstallPrimarySite  

    -   **Detalhes:** instala um site primário.  

**Opções**  

-   **Nome da chave:** ProductID  

    -   **Obrigatória:** Sim  

    -   **Valores:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* ou *Eval*  

    -   **Detalhes:** especifica a chave do produto (Product Key) de instalação do Configuration Manager, incluindo os traços. Insira **Eval** para instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** SiteCode  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*SiteCode*>  

    -   **Detalhes:** especifica três caracteres alfanuméricos que identificam de forma exclusiva o site na hierarquia.  

-   **Nome da chave:** SiteName  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*SiteName*>  

    -   **Detalhes:** especifica o nome do site.  

-   **Nome da chave:** SMSInstallDir  

    -   **Obrigatória:** Sim  

    -   **Valores:** *ConfigMgrInstallationPath*  

    -   **Detalhes:** especifica a pasta de instalação dos arquivos de programa do Configuration Manager.  

-   **Nome da chave:** SDKServer  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*FQDN do Provedor de SMS*>  

    -   **Detalhes:** especifica o FQDN para o servidor que hospedará o Provedor de SMS.  
        Você pode configurar outros Provedores de SMS para o site após a instalação inicial.  

-   **Nome da chave:** PrerequisiteComp  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = baixar  

         1 = já baixado  

    -   **Detalhes:** especifica se os arquivos de pré-requisito da Instalação já foram baixados. Por exemplo, se você usar o valor 0, a Instalação baixará os arquivos.  

-   **Nome da chave:** PrerequisitePath  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Detalhes:** especifica o caminho para os arquivos de pré-requisito da Instalação. Dependendo do valor do **PrerequisiteComp** , a Instalação usará esse caminho para armazenar arquivos baixados ou para localizar arquivos baixados anteriormente.  

-   **Nome da chave:** AdminConsole  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = não instalar  

         1 = instalar  

    -   **Detalhes:** especifica se deseja instalar o console do Configuration Manager.  

-   **Nome da chave:** JoinCEIP  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = não ingressar  

         1 = ingressar  

    -   **Detalhes:** especifica se deve ingressar no Programa de Aperfeiçoamento da Experiência do Usuário.  

-   **Nome da chave:** ManagementPoint  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*FQDN do servidor de sites do ponto de gerenciamento*>  

    -   **Detalhes:** especifica o FQDN do servidor que hospedará a função de sistema de sites do ponto de gerenciamento.  

-   **Nome da chave:** ManagementPointProtocol  

    -   **Obrigatória:** Não  

    -   **Valores:** HTTPS ou HTTP  

    -   **Detalhes:** especifica o protocolo a ser usado para o ponto de gerenciamento.  

-   **Nome da chave:** DistributionPoint  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*FQDN do servidor de sites do Ponto de distribuição*>  

    -   **Detalhes:** especifica o protocolo a ser usado para o ponto de gerenciamento.  

-   **Nome da chave:** DistributionPointProtocol  

    -   **Obrigatória:** Não  

    -   **Valores:** HTTPS ou HTTP  

    -   **Detalhes:** especifica o protocolo a ser usado para o ponto de distribuição.  

-   **Nome da chave:** RoleCommunicationProtocol  

    -   **Obrigatória:** Sim  

    -   **Valores:** EnforceHTTPS ou HTTPorHTTPS  

    -   **Detalhes:** especifica se deve configurar todos os sistemas de sites para aceitar somente comunicação HTTPS de clientes, ou se o método de comunicação será definido para cada função do sistema de sites. Quando você selecionar **EnforceHTTPS**, o computador cliente deverá ter um certificado PKI válido para autenticação de cliente.  

-   **Nome da chave:** ClientsUsePKICertificate  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = não usar  

         1 = usar  

    -   **Detalhes:** especifica se os clientes usarão um certificado PKI de cliente para se comunicar com as funções do sistema de sites.  

-   **Nome da chave:** AddServerLanguages  

    -   **Obrigatória:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** especifica os idiomas do servidor que estarão disponíveis para o console do Configuration Manager, relatórios e objetos do Configuration Manager. Inglês está disponível por padrão.  

-   **Nome da chave:** AddClientLanguages  

    -   **Obrigatória:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Details:** especifica os idiomas que estarão disponíveis para computadores cliente. Inglês está disponível por padrão.  

-   **Nome da chave:** DeleteServerLanguages  

    -   **Obrigatória:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** modifica um site após sua instalação.  
        Especifica os idiomas para remoção e que não estarão mais disponíveis para o console do Configuration Manager, relatórios e objetos do Configuration Manager. Inglês está disponível por padrão e não pode ser removido.  

-   **Nome da chave:** DeleteClientLanguages  

    -   **Obrigatória:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** modifica um site após sua instalação.  
        Especifica os idiomas a serem removidos e que não estarão mais disponíveis para computadores cliente. Inglês está disponível por padrão e não pode ser removido.  

-   **Nome da chave:** MobileDeviceLanguage  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = não instalar  

         1 = instalar  

    -   **Detalhes:** especifica se os idiomas do cliente do dispositivo móvel estão instalados.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Obrigatória:** Sim  

    -   **Valores:** *SQLServerName*  

    -   **Detalhes:** especifica o nome do servidor ou o nome da instância clusterizada que está executando o SQL Server. Ele irá hospedar o banco de dados do site.  

-   **Nome da chave:** DatabaseName  

    -   **Obrigatória:** Sim  

    -   **Valores:** *&lt;SiteDatabaseName\>* ou *&lt;InstanceName\>\&lt;SiteDatabaseName\>*  

    -   **Detalhes:**  

         Especifica o nome do banco de dados do SQL Server a ser criado ou usado para instalar o banco de dados do site primário.  

        > [!IMPORTANT]  
        >  Você deverá especificar o nome da instância e o nome do banco de dados do site se você não usar a instância padrão.  

-   **Nome da chave:** SQLSSBPort  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*SSBPortNumber*>  

    -   **Detalhes:** especifica a porta do SQL SSB (Server Service Broker) a ser usada pelo SQL Server. Normalmente, o SSB está configurado para usar a porta TCP 4022, mas há suporte para outras portas.  

-   **Nome da chave:** SQLDataFilePath  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*FilePath para o arquivo .MDB do banco de dados*>  

    -   **Detalhes:** especifica um local alternativo para criar o arquivo .MDB do banco de dados.  

-   **Nome da chave:** SQLLogFilePath  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*FilePath para o arquivo .LDF do banco de dados*>  

    -   **Detalhes:** especifica um local alternativo para criar o arquivo .LDF do banco de dados.  

**HierarchyExpansionOption**  

-   **Nome da chave:** CCARSiteServer  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*FQDN do site de administração central*>  

    -   **Detalhes:** especifica o site de administração central ao qual o site primário será anexado quando ingressar na hierarquia do Configuration Manager. Você deve especificar o site de administração central durante a instalação.  

-   **Nome da chave:** CASRetryInterval  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*Interval*>  

    -   **Detalhes:** especifica o intervalo de repetição (em minutos) para tentar uma conexão ao site de administração central depois de a conexão falhar. Por exemplo, se a conexão com o site de administração central falhar, o site primário aguardará o número de minutos especificado para CASRetryInterval e tentará novamente se conectar.  

-   **Nome da chave:** WaitForCASTimeout  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*Timeout*>  

         Um valor de 0 a 100  

    -   **Detalhes:** especifica o valor máximo do tempo limite (em minutos) para um site primário se conectar ao site de administração central. Por exemplo, se um site primário falhar ao se conectar com um site de administração central, o site primário tentará novamente se conectar ao site de administração central baseado no CASRetryInterval até atingir o período de WaitForCASTimeout. Você pode especificar um valor de 0 a 100.  

**CloudConnectorOptions**  

-   **Nome da chave:** CloudConnector  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = não instalar  

         1 = instalar  

    -   **Detalhes:** especifica se você instalará um ponto de conexão de serviço no site. Como o ponto de conexão de serviço pode ser instalado somente no site de nível superior de uma hierarquia, esse valor deverá ser 0 para um site primário filho.  

-   **Nome da chave:** CloudConnectorServer  

    -   **Obrigatória:** obrigatória quando CloudConnector for igual a 1  

    -   **Valores:** &lt;*FQDN do servidor de ponto de conexão do serviço*\>  

    -   **Detalhes:** especifica o FQDN do servidor que hospedará a função do sistema de sites do ponto de conexão do serviço.  

-   **Nome da chave:** UseProxy  

    -   **Obrigatória:** obrigatória quando CloudConnector for igual a 1  

    -   **Valores:** 0 ou 1  

         0 = não instalar  

         1 = instalar  

    -   **Detalhes:** especifica se o ponto de conexão do serviço usará um servidor proxy.  

-   **Nome da chave:** ProxyName  

    -   **Obrigatória:** obrigatória quando UseProxy for igual a 1  

    -   **Valores:** &lt;*FQDN do servidor proxy*>  

    -   **Detalhes:** especifica o FQDN do servidor proxy que será usado pela função do sistema de sites do ponto de conexão do serviço.  

-   **Nome da chave:** ProxyPort  

    -   **Obrigatória:** obrigatória quando UseProxy for igual a 1  

    -   **Valores:** &lt;*PortNumber*>  

    -   **Detalhes:** especifica o número da porta a ser usado.  

### <a name="unattended-recovery-for-a-central-administration-site"></a>Recuperação autônoma de um site de administração central  
 Use os detalhes a seguir para recuperar um site de administração central usando um arquivo de script da Instalação autônoma.  

**Identificação**  

-   **Nome da chave:** Action  

    -   **Obrigatória:** Sim  

    -   **Valores:** RecoverCCAR  

    -   **Detalhes:** recupera um site de administração central.  

**RecoveryOptions**  

-   **Nome da chave:** ServerRecoveryOptions  

    -   **Obrigatória:** Sim  

    -   **Valores:** 1, 2 ou 4  

         1 = Servidor do site de recuperação e SQL Server.  

         2 = Recuperar apenas o servidor do site.  

         4 = Recuperar apenas o SQL Server.  

    -   **Detalhes:** especifica se a Instalação recuperará o servidor do site, o SQL Server ou ambos. As chaves associadas são necessárias quando o seguinte valor é definido para a configuração de ServerRecoveryOptions:  

        -   Valor = 1: você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.  

        -   Valor = 2: você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.  

        -   Valor = 4: a chave **BackupLocation** é necessária quando o valor **10** é configurado para a chave **DatabaseRecoveryOptions** , que restaura o banco de dados do site por meio do backup.  

-   **Nome da chave:** DatabaseRecoveryOptions  

    -   **Obrigatória:** essa chave será obrigatória quando a configuração ServerRecoveryOptions tiver um valor de **1** ou **4**.  

    -   **Valores:** 10, 20, 40, 80  

         10 = Restaurar, por meio do backup, o banco de dados do site.  

         20 = Usar um banco de dados do site recuperado manualmente usando outro método.  

         40 = Criar um novo banco de dados para o site. Use essa opção quando não houver backup do banco de dados do site disponível. Os dados globais e do site são recuperados por meio da replicação de outros sites.  

         80 = Ignorar recuperação do banco de dados.  

    -   **Detalhes:** especifica como a Instalação recupera o banco de dados do site no SQL Server.  

-   **Nome da chave:** ReferenceSite  

    -   **Obrigatória:** essa chave será obrigatória quando a configuração **DatabaseRecoveryOptions** tiver um valor de **40**.  

    -   **Valores:** &lt;*ReferenceSiteFQDN*>  

    -   **Detalhes:** especificará o site primário de referência que o site de administração central usa para recuperar dados globais se o backup do banco de dados for mais antigo que o período de retenção do controle de alterações ou quando o site for recuperado sem backup.  

         Quando um site de referência não é especificado e o backup é mais antigo que o período de retenção do controle de alterações, todos os sites primários são reinicializados com os dados restaurados por meio do site de administração central.  

         Caso você não especifique um site de referência e o backup esteja dentro do período de retenção do controle de alterações, somente as alterações ocorridas após o backup são replicadas dos sites primários. Quando houver alterações conflitantes de sites primários diferentes, o site de administração central usará a primeira alteração que receber.  

-   **Nome da chave:** SiteServerBackupLocation  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*PathToSiteServerBackupSet*>  

    -   **Detalhes:** especifica o caminho para o conjunto de backups do servidor de site. Essa chave é opcional quando a configuração **ServerRecoveryOptions** tem o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.  

-   **Nome da chave:** BackupLocation  

    -   **Obrigatória:** essa chave será obrigatória quando você configurar um valor de **1** ou **4** para a chave **ServerRecoveryOptions**, e configurar um valor de **10** para a chave **DatabaseRecoveryOptions**.  

    -   **Valores:** &lt;*PathToSiteDatabaseBackupSet*>  

    -   **Detalhes:** especifica o caminho para o conjunto de backup do banco de dados do site.  

**Opções**  

-   **Nome da chave:** ProductID  

    -   **Obrigatória:** Sim  

    -   **Valores:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* ou *Eval*  

    -   **Detalhes:** especifica a chave do produto (Product Key) de instalação do Configuration Manager, incluindo os traços. Insira **Eval** para instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** SiteCode  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*SiteCode*>  

    -   **Detalhes:** especifica três caracteres alfanuméricos que identificam de forma exclusiva o site na hierarquia. É necessário especificar o código do site usado pelo site antes da falha. Para obter mais informações sobre as restrições de código do site, consulte a seção [Sobre nomes de site e códigos de site](#bkmk_codes) neste tópico.  

-   **Nome da chave:** SiteName  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*SiteName*>  

    -   **Detalhes:** especifica o nome do site.  

-   **Nome da chave:** SMSInstallDir  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*ConfigMgrInstallationPath*>  

    -   **Detalhes:** especifica a pasta de instalação dos arquivos de programa do Configuration Manager.  

-   **Nome da chave:** SDKServer  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*FQDN do Provedor de SMS*>  

    -   **Detalhes:** especifica o FQDN para o servidor que hospedará o Provedor de SMS. Você deve especificar o servidor que hospedou o Provedor de SMS antes da falha.  

         Você pode configurar outros Provedores de SMS para o site após a instalação inicial. Para obter mais informações sobre o Provedor de SMS, consulte [Planejar o Provedor de SMS para o System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Nome da chave:** PrerequisiteComp  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = baixar  

         1 = já baixado  

    -   **Detalhes:** especifica se os arquivos de pré-requisito da Instalação já foram baixados. Por exemplo, se você usar o valor **0**, a instalação baixará os arquivos.  

-   **Nome da chave:** PrerequisitePath  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Detalhes:** especifica o caminho para os arquivos de pré-requisito da Instalação. Dependendo do valor do **PrerequisiteComp** , a Instalação usará esse caminho para armazenar arquivos baixados ou para localizar arquivos baixados anteriormente.  

-   **Nome da chave:** AdminConsole  

    -   **Obrigatória:** essa chave é obrigatória, exceto quando a configuração **ServerRecoveryOptions** tiver um valor de **4**.  

    -   **Valores:** 0 ou 1  

         0 = não instalar  

         1 = instalar  

    -   **Detalhes:** especifica se deseja instalar o console do Configuration Manager.  

-   **Nome da chave:** JoinCEIP  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = não ingressar  

         1 = ingressar  

    -   **Detalhes:** especifica se deve ingressar no Programa de Aperfeiçoamento da Experiência do Usuário.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Obrigatória:** Sim  

    -   **Valores:** *SQLServerName*  

    -   **Detalhes:** especifica o nome do servidor ou o nome da instância clusterizada que está executando o SQL Server que hospedará o banco de dados do site. Você deverá especificar o mesmo servidor que hospedou o banco de dados do site antes da falha.  

-   **Nome da chave:** DatabaseName  

    -   **Obrigatória:** Sim  

    -   **Valores:** *&lt;SiteDatabaseName\>* ou *&lt;InstanceName\>\&lt;SiteDatabaseName\>*  

    -   **Detalhes:**  

         Especifica o nome do banco de dados do SQL Server a ser criado ou usado para instalar o banco de dados do site de administração central. Você deverá especificar o mesmo nome do banco de dados usado antes da falha.  

        > [!IMPORTANT]  
        >  Você deverá especificar o nome da instância e o nome do banco de dados do site se você não usar a instância padrão.  

-   **Nome da chave:** SQLSSBPort  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*SSBPortNumber*>  

    -   **Detalhes:** especifica a porta do SQL SSB (Server Service Broker) a ser usada pelo SQL Server. Normalmente, o SSB está configurado para usar a porta TCP 4022. Você deve especificar a mesma porta do SSB que foi usada antes da falha.  

-   **Nome da chave:** SQLDataFilePath  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*FilePath para o arquivo .MDB do banco de dados*>  

    -   **Detalhes:** especifica um local alternativo para criar o arquivo .MDB do banco de dados.  

-   **Nome da chave:** SQLLogFilePath  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*FilePath para o arquivo .LDF do banco de dados*>  

    -   **Detalhes:** especifica um local alternativo para criar o arquivo .LDF do banco de dados.  

**CloudConnectorOptions**  

-   **Nome da chave:** CloudConnector  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = não instalar  

         1 = instalar  

    -   **Detalhes:** especifica se você instalará um ponto de conexão de serviço no site. Como o ponto de conexão de serviço pode ser instalado somente no site de nível superior de uma hierarquia, esse valor deverá ser 0 para um site primário filho.  

-   **Nome da chave:** CloudConnecorServer  

    -   **Obrigatória:** obrigatória quando CloudConnector for igual a 1  

    -   **Valores:** &lt;*FQDN do servidor de ponto de conexão do serviço*>  

    -   **Detalhes:** especifica o FQDN do servidor que hospedará a função do sistema de sites do ponto de conexão do serviço.  

-   **Nome da chave:** UseProxy  

    -   **Obrigatória:** obrigatória quando CloudConnector for igual a 1  

    -   **Valores:** 0 ou 1  

         0 = não instalar  

         1 = instalar  

    -   **Detalhes:** especifica se o ponto de conexão do serviço usará um servidor proxy.  

-   **Nome da chave:** ProxyName  

    -   **Obrigatória:** obrigatória quando CloudConnector for igual a 1  

    -   **Valores:** &lt;*FQDN do servidor proxy*>  

    -   **Detalhes:** especifica o FQDN do servidor proxy que será usado pela função do sistema de sites do ponto de conexão do serviço.  

-   **Nome da chave:** ProxyPort  

    -   **Obrigatória:** obrigatória quando CloudConnector for igual a 1  

    -   **Valores:** &lt;*PortNumber*>  

    -   **Detalhes:** especifica o número da porta a ser usado.  

### <a name="unattended-recovery-for-a-primary-site"></a>Recuperação autônoma de um site primário  
 Use os detalhes a seguir para recuperar um site primário usando um arquivo de script de Instalação autônoma.  

**Identificação**  

-   **Nome da chave:** Action  

    -   **Obrigatória:** Sim  

    -   **Valores:** RecoverPrimarySite  

    -   **Detalhes:** recupera um site primário.  

**RecoveryOptions**  

-   **Nome da chave:** ServerRecoveryOptions  

    -   **Obrigatória:** Sim  

    -   **Valores:** 1, 2 ou 4  

         1 = Servidor do site de recuperação e SQL Server.  

         2 = Recuperar apenas o servidor do site.  

         4 = Recuperar apenas o SQL Server.  

    -   **Detalhes:** especifica se a Instalação recuperará o servidor do site, o SQL Server ou ambos. As chaves associadas são necessárias quando o seguinte valor é definido para a configuração de ServerRecoveryOptions:  

        -   Valor = 1: você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.  

        -   Valor = 2: você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.  

        -   Valor = 4: a chave **BackupLocation** é necessária quando o valor **10** é configurado para a chave **DatabaseRecoveryOptions** , que restaura o banco de dados do site por meio do backup.  

-   **Nome da chave:** DatabaseRecoveryOptions  

    -   **Obrigatória:** essa chave será obrigatória quando a configuração ServerRecoveryOptions tiver um valor de **1** ou **4**.  

    -   **Valores:** 10, 20, 40, 80  

         10 = Restaurar, por meio do backup, o banco de dados do site.  

         20 = Usar um banco de dados do site recuperado manualmente usando outro método.  

         40 = Criar um novo banco de dados para o site. Use essa opção quando não houver backup do banco de dados do site disponível. Os dados globais e do site são recuperados por meio da replicação de outros sites.  

         80 = Ignorar recuperação do banco de dados.  

    -   **Detalhes:** especifica como a Instalação recupera o banco de dados do site no SQL Server.  

-   **Nome da chave:** SiteServerBackupLocation  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*PathToSiteServerBackupSet*>  

    -   **Detalhes:**  

         Especifica o caminho para o conjunto de backup do servidor de site. Essa chave é opcional quando a configuração **ServerRecoveryOptions** tem o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.  

-   **Nome da chave:** BackupLocation  

    -   **Obrigatória:** essa chave será obrigatória quando você configurar um valor de **1** ou **4** para a chave **ServerRecoveryOptions**, e configurar um valor de **10** para a chave **DatabaseRecoveryOptions**.  

    -   **Valores:** &lt;*PathToSiteDatabaseBackupSet*>  

    -   **Detalhes:** especifica o caminho para o conjunto de backup do banco de dados do site.  

**Opções**  

-   **Nome da chave:** ProductID  

    -   **Obrigatória:** Sim  

    -   **Valores:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* ou *Eval*  

    -   **Detalhes:** especifica a chave do produto (Product Key) de instalação do Configuration Manager, incluindo os traços. Insira **Eval** para instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** SiteCode  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*SiteCode*>  

    -   **Detalhes:** especifica três caracteres alfanuméricos que identificam de forma exclusiva o site na hierarquia. É necessário especificar o código do site usado pelo site antes da falha. Para obter mais informações sobre as restrições de código do site, consulte a seção [Sobre nomes de site e códigos de site](#bkmk_codes) neste tópico.  

-   **Nome da chave:** SiteName  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*SiteName*>  

    -   **Detalhes:** especifica o nome do site.  

-   **Nome da chave:** SMSInstallDir  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*ConfigMgrInstallationPath*>  

    -   **Detalhes:** especifica a pasta de instalação dos arquivos de programa do Configuration Manager.  

-   **Nome da chave:** SDKServer  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*FQDN do Provedor de SMS*>  

    -   **Detalhes:** especifica o FQDN para o servidor que hospedará o Provedor de SMS. Você deve especificar o servidor que hospedou o Provedor de SMS antes da falha. Você pode configurar outros Provedores de SMS para o site após a instalação inicial. Para obter mais informações sobre o Provedor de SMS, consulte [Planejar o Provedor de SMS para o System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Nome da chave:** PrerequisiteComp  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = baixar  

         1 = já baixado  

    -   **Detalhes:** especifica se os arquivos de pré-requisito da Instalação já foram baixados. Por exemplo, se você usar o valor **0**, a instalação baixará os arquivos.  

-   **Nome da chave:** PrerequisitePath  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Detalhes:** especifica o caminho para os arquivos de pré-requisito da Instalação. Dependendo do valor do **PrerequisiteComp** , a Instalação usará esse caminho para armazenar arquivos baixados ou para localizar arquivos baixados anteriormente.  

-   **Nome da chave:** AdminConsole  

    -   **Obrigatória:** essa chave é obrigatória, exceto quando a configuração **ServerRecoveryOptions** tiver um valor de **4**.  

    -   **Valores:** 0 ou 1  

         0 = não instalar  

         1 = instalar  

    -   **Detalhes:** especifica se deseja instalar o console do Configuration Manager.  

-   **Nome da chave:** JoinCEIP  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = não ingressar  

         1 = ingressar  

    -   **Detalhes:** especifica se deve ingressar no Programa de Aperfeiçoamento da Experiência do Usuário.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Obrigatória:** Sim  

    -   **Valores:** *SQLServerName*  

    -   **Detalhes:** especifica o nome do servidor ou o nome da instância clusterizada que está executando o SQL Server que hospedará o banco de dados do site. Você deverá especificar o mesmo servidor que hospedou o banco de dados do site antes da falha.  

-   **Nome da chave:** DatabaseName  

    -   **Obrigatória:** Sim  

    -   **Valores:**  &lt;*SiteDatabaseName*\> ou                                &lt;*InstanceName*\>\\&lt;*SiteDatabaseName*\>

    -   **Detalhes:**  

         Especifica o nome do banco de dados do SQL Server a ser criado ou usado para instalar o banco de dados do site de administração central. Você deverá especificar o mesmo nome do banco de dados usado antes da falha.  

        > [!IMPORTANT]  
        >  Você deverá especificar o nome da instância e o nome do banco de dados do site se você não usar a instância padrão.  

-   **Nome da chave:** SQLSSBPort  

    -   **Obrigatória:** Sim  

    -   **Valores:** &lt;*SSBPortNumber*>  

    -   **Detalhes:** especifica a porta do SQL SSB (Server Service Broker) a ser usada pelo SQL Server. Normalmente, o SSB está configurado para usar a porta TCP 4022. Você deve especificar a mesma porta do SSB que foi usada antes da falha.  

-   **Nome da chave:** SQLDataFilePath  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*FilePath para o arquivo .MDB do banco de dados*>  

    -   **Detalhes:** especifica um local alternativo para criar o arquivo .MDB do banco de dados.  

-   **Nome da chave:** SQLLogFilePath  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*FilePath para o arquivo .LDF do banco de dados*>  

    -   **Detalhes:** especifica um local alternativo para criar o arquivo .LDF do banco de dados.  

**HierarchyExpansionOptions**  

-   **Nome da chave:** CCARSiteServer  

    -   **Obrigatória:** ver detalhes.  

    -   **Valores:** &lt;*SiteCodeForCentralAdministrationSite*>  

    -   **Detalhes:** especifica o site de administração central ao qual o site primário é anexado quando ingressa na hierarquia do Configuration Manager. Essa configuração é necessária se o site primário foi anexado ao site de administração central antes da falha. É necessário especificar o código do site usado para o site de administração central antes da falha.  

-   **Nome da chave:** CASRetryInterval  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*Interval*>  

    -   **Detalhes:** especifica o intervalo de repetição (em minutos) para tentar uma conexão ao site de administração central depois de a conexão falhar. Por exemplo, se a conexão ao site de administração central falhar, o site primário aguardará o número de minutos que você especificar para **CASRetryInterval**e tentará novamente a conexão.  

-   **Nome da chave:** WaitForCASTimeout  

    -   **Obrigatória:** Não  

    -   **Valores:** &lt;*Timeout*>  

    -   **Detalhes:** especifica o valor máximo do tempo limite (em minutos) para um site primário se conectar ao site de administração central. Por exemplo, se um site primário falhar ao se conectar com um site de administração central, o site primário tentará novamente se conectar ao site de administração central baseado no **CASRetryInterval** até atingir o período de **WaitForCASTimeout** . Você pode especificar um valor de 0 a 100.  

**CloudConnectorOptions**  

-   **Nome da chave:** CloudConnector  

    -   **Obrigatória:** Sim  

    -   **Valores:** 0 ou 1  

         0 = não instalar  

         1 = instalar  

    -   **Detalhes:** especifica se você instalará um ponto de conexão de serviço no site. Como o ponto de conexão de serviço pode ser instalado somente no site de nível superior de uma hierarquia, esse valor deverá ser 0 para um site primário filho.  

-   **Nome da chave:** CloudConnecorServer  

    -   **Obrigatória:** obrigatória quando CloudConnector for igual a 1  

    -   **Valores:** &lt;*FQDN do servidor de ponto de conexão do serviço*>  

    -   **Detalhes:** especifica o FQDN do servidor que hospedará a função do sistema de sites do ponto de conexão do serviço.  

-   **Nome da chave:** UseProxy  

    -   **Obrigatória:** obrigatória quando CloudConnector for igual a 1  

    -   **Valores:** 0 ou 1  

         0 = não instalar  

         1 = instalar  

    -   **Detalhes:** especifica se o ponto de conexão do serviço usará um servidor proxy.  

-   **Nome da chave:** ProxyName  

    -   **Obrigatória:** obrigatória quando CloudConnector for igual a 1  

    -   **Valores:** &lt;*FQDN do servidor proxy*>  

    -   **Detalhes:** especifica o FQDN do servidor proxy que será usado pela função do sistema de sites do ponto de conexão do serviço.  

-   **Nome da chave:** ProxyPort  

    -   **Obrigatória:** obrigatória quando CloudConnector for igual a 1  

    -   **Valores:** &lt;*PortNumber*>  

    -   **Detalhes:** especifica o número da porta a ser usado.  



<!--HONumber=Dec16_HO3-->


