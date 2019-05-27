---
title: Configurar opções de linha de comando
titleSuffix: Configuration Manager
description: Crie scripts de automação para instalar o System Center Configuration Manager por meio de uma linha de comando.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 434b53d24d050cc66cbb5e8bec7a681311f945b8
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65498679"
---
# <a name="command-line-options-for-setup-in-system-center-configuration-manager"></a>Opções de linha de comando para instalação no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


 Use as informações a seguir para configurar scripts ou instalar o System Center Configuration Manager por meio de uma linha de comando.  

##  <a name="bkmk_setup"></a> Opções de linha de comando para instalação  
 **/DEINSTALL**  
 Desinstala o site. Execute a instalação no computador do servidor do site.  

 **/DONTSTARTSITECOMP**  
 Instala um site, mas impede a inicialização do serviço Gerenciador de Componentes de Site. Até que o serviço do Gerenciador de Componentes do Site seja iniciado, o site não ficará ativo. O Gerenciador de Componentes de Site é responsável por instalar e iniciar o serviço SMS_Executive e por outros processos no site. Após a conclusão da instalação do site, ao iniciar o serviço Gerenciador de Componentes de Site, ele instalará o SMS_Executive e os outros processos necessários para a operação do site.  

 **/HIDDEN**  
 Oculta a interface do usuário durante a instalação. Use essa opção somente junto com a opção **/SCRIPT**. O arquivo de script autônomo deverá fornecer todas as opções necessárias ou a instalação falhará.  

 **/NOUSERINPUT**  
 Desabilita a entrada do usuário durante a instalação, mas exibe o assistente de instalação. Use essa opção somente junto com a opção **/SCRIPT**. O arquivo de script autônomo deverá fornecer todas as opções necessárias ou a instalação falhará.  

 **/RESETSITE**  
 Executa uma redefinição de site que redefine o banco de dados e as contas de serviço do site. Execute a instalação por meio do **<*caminho de instalação do Configuration Manager*>\BIN\X64** no servidor do site. Para obter mais informações sobre a redefinição de site, consulte a seção [Executar uma redefinição de site](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_reset) em [Modificar a infraestrutura do System Center Configuration Manager](../../../../core/servers/manage/modify-your-infrastructure.md).  

 **/TESTDBUPGRADE <*Instance name*>\\<*Database name*>**  
 Executa um teste em um backup do banco de dados do site para garantir que o banco de dados pode fazer uma atualização. Forneça o nome da instância e o nome do banco de dados para o banco de dados do site. Se você especificar somente o nome do banco de dados, a instalação usará o nome da instância padrão.  

> [!IMPORTANT]  
>  Não execute essa opção de linha de comando no banco de dados do site de produção. A execução dessa opção de linha de comando no banco de dados do site de produção atualizará o banco de dados do site e poderá deixar o site inoperante.  

 **/UPGRADE**  
 Executa a atualização autônoma de um site. Ao usar **/UPGRADE**, é necessário especificar a chave do produto (Product Key), incluindo os traços (-). Além disso, é necessário especificar o caminho para os arquivos de pré-requisito da instalação baixados anteriormente.  

 Exemplo: `setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx <path to external component files>`  

 Para obter mais informações sobre os arquivos de pré-requisito da instalação, consulte [Downloader de instalação](setup-downloader.md).  

 **/SCRIPT <*setup script path*>**  
 Executa instalações autônomas. É necessário ter um arquivo de inicialização da instalação ao usar a opção **/SCRIPT**. Para obter mais informações sobre como executar a instalação autônoma, consulte [Instalar sites usando uma linha de comando](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).  

 **/SDKINST <*SMS Provider FQDN*>**  
 Instala o Provedor de SMS no computador especificado. Forneça o FQDN (nome de domínio totalmente qualificado) do computador do Provedor de SMS. Para obter mais informações sobre o Provedor de SMS, consulte [Planejar o Provedor de SMS](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

 **/SDKDEINST <*SMS Provider FQDN*>**  
 Desinstala o Provedor de SMS do computador especificado. Forneça o FQDN do computador do Provedor de SMS.  

 **/MANAGELANGS <*Language script path*>**  
 Gerencia os idiomas instalados em um site previamente instalado. Para usar essa opção, execute a instalação por meio do **<*caminho de instalação do Configuration Manager*>\BIN\X64** no servidor do site. Forneça o local para o arquivo de script de idioma que contém as configurações de idioma. Para obter mais informações sobre as opções de idioma disponíveis no arquivo de script de instalação de idioma, consulte a seção [Opções de linha de comando para gerenciar idiomas](#bkmk_Lang).  

##  <a name="bkmk_Lang"></a> Opções de linha de comando para gerenciar idiomas  
 **Identificação**  

-   **Nome da chave:** Ação  

    -   **Obrigatório:** Sim  

    -   **Valores:** ManageLanguages  

    -   **Detalhes:** gerencia o servidor, o cliente e o suporte ao idioma do cliente móvel em um site.  

**Opções**  

-   **Nome da chave:** AddServerLanguages  

    -   **Obrigatório:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** especifica os idiomas do servidor que estarão disponíveis para o console do Configuration Manager, relatórios e objetos do Configuration Manager. Inglês está disponível por padrão.  

-   **Nome da chave:** AddClientLanguages  

    -   **Obrigatório:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** especifica os idiomas que estarão disponíveis para computadores cliente. Inglês está disponível por padrão.  

-   **Nome da chave:** DeleteServerLanguages  

    -   **Obrigatório:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** Especifica os idiomas a serem removidos e que não estarão mais disponíveis para o console, os relatórios e objetos do Configuration Manager. Inglês está disponível por padrão e não pode ser removido.  

-   **Nome da chave:** DeleteClientLanguages  

    -   **Obrigatório:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** Especifica os idiomas a serem removidos e que não estarão mais disponíveis para os computadores cliente. Inglês está disponível por padrão e não pode ser removido.  

-   **Nome da chave:** MobileDeviceLanguage  

    -   **Obrigatório:** Sim  

    -   **Valores:** 0 ou 1  

         0 = Não instalar  

         1 = Instalar  

    -   **Detalhes:** especifica se os idiomas do cliente do dispositivo móvel estão instalados.  

-   **Nome da chave:** PrerequisiteComp  

    -   **Obrigatório:** Sim  

    -   **Valores:** 0 ou 1  

         0 = Baixar  

         1 = Já baixado  

    -   **Detalhes:** Especifica se os arquivos de pré-requisito da instalação já foram baixados. Por exemplo, se você usar o valor **0**, a instalação baixará os arquivos.  

-   **Nome da chave:** PrerequisitePath  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Caminho para os arquivos de pré-requisito da instalação*>  

    -   **Detalhes:** Especifica o caminho para os arquivos de pré-requisito da instalação. Dependendo do valor de **PrerequisiteComp**, a instalação usará esse caminho para armazenar os arquivos baixados ou para localizar os arquivos baixados anteriormente.  

##  <a name="bkmk_Unattended"></a> Chaves de arquivo de script de instalação autônoma  
 Use as seções a seguir para ajudá-lo a criar seu script para a instalação autônoma. As listas mostram as chaves de script da instalação disponíveis, seus valores correspondentes, se elas são obrigatórias, em que tipo de instalação são usadas e uma breve descrição da chave.  

### <a name="unattended-install-for-a-central-administration-site"></a>Instalação autônoma de um site de administração central  
 Use os detalhes a seguir para instalar um site de administração central usando um arquivo de script de instalação autônoma.  

**Identificação**  

-   **Nome da chave:** Ação  

    -   **Obrigatório:** Sim  

    -   **Valores:** InstallCAS  

    -   **Detalhes:** Instala um site de administração central.  

-   **Nome da chave:** CDLatest  

    -   **Obrigatório:** Sim – somente ao usar a mídia da pasta CD.Latest.    

    -   **Valores:** 1 qualquer valor diferente de 1 é considerado como não usando o CD.Latest.

    -   **Detalhes:** seu script deve incluir essa chave e o valor ao executar a instalação de uma mídia em uma pasta CD.Latest com a finalidade de instalar um site primário ou de administração central ou recuperar um site de administração central ou primário. Esse valor informa à instalação que a forma de mídia CD.Latest está sendo usada.

**Opções**  

-   **Nome da chave:** ProductID  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *ou* Eval  

    -   **Detalhes:** especifica a chave do produto (Product Key) de instalação do Configuration Manager, incluindo os traços. Insira **Eval** para instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** SiteCode  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Código do site*>  

    -   **Detalhes:** especifica três caracteres alfanuméricos que identificam exclusivamente o site na hierarquia.  

-   **Nome da chave:** Nome do site  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Nome do site*>  

    -   **Detalhes:** especifica o nome para esse site.  

-   **Nome da chave:** SMSInstallDir  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Caminho de instalação do Configuration Manager*>  

    -   **Detalhes:** especifica a pasta de instalação dos arquivos de programa do Configuration Manager.  

-   **Nome da chave:** SDKServer  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*FQDN do Provedor de SMS*>  

    -   **Detalhes:** especifica o FQDN para o servidor que hospedará o Provedor de SMS. Você pode configurar outros Provedores de SMS para o site após a instalação inicial.  

-   **Nome da chave:** PrerequisiteComp  

    -   **Obrigatório:** Sim  

    -   **Valores:** 0 ou 1  

         0 = Baixar  

         1 = Já baixado  

    -   **Detalhes:** Especifica se os arquivos de pré-requisito da instalação já foram baixados. Por exemplo, se você usar o valor **0**, a instalação baixará os arquivos.  

-   **Nome da chave:** PrerequisitePath  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Caminho para os arquivos de pré-requisito da instalação*>  

    -   **Detalhes:** Especifica o caminho para os arquivos de pré-requisito da instalação. Dependendo do valor de **PrerequisiteComp**, a instalação usará esse caminho para armazenar os arquivos baixados ou para localizar os arquivos baixados anteriormente.  

-   **Nome da chave:** AdminConsole  

    -   **Obrigatório:** Sim  

    -   **Valores:** 0 ou 1  

         0 = Não instalar  

         1 = Instalar  

    -   **Detalhes:** especifica se deseja instalar o console do Configuration Manager.  

-   **Nome da chave:** JoinCEIP  
    > [!Note]  
    > A partir do Configuration Manager versão 1802, o recurso Programa de Aperfeiçoamento da Experiência do Usuário é removido do produto.

    -   **Obrigatório:** Sim  

    -   **Valores:** 0 ou 1  

         0 = Não ingressar  

         1 = Ingressar  

    -   **Detalhes:** Especifica se deve associar-se o CEIP (Programa de Aperfeiçoamento da experiência do Usuário).  

-   **Nome da chave:** AddServerLanguages  

    -   **Obrigatório:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** especifica os idiomas do servidor que estarão disponíveis para o console do Configuration Manager, relatórios e objetos do Configuration Manager. Inglês está disponível por padrão.  

-   **Nome da chave:** AddClientLanguages  

    -   **Obrigatório:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** especifica os idiomas que estarão disponíveis para computadores cliente. Inglês está disponível por padrão.  

-   **Nome da chave:** DeleteServerLanguages  

    -   **Obrigatório:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** modifica um site após a instalação. Especifica os idiomas a serem removidos e que não estarão mais disponíveis para o console, os relatórios e objetos do Configuration Manager. Inglês está disponível por padrão e não pode ser removido.  

-   **Nome da chave:** DeleteClientLanguages  

    -   **Obrigatório:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** modifica um site após a instalação. Especifica os idiomas a serem removidos e que não estarão mais disponíveis para os computadores cliente. Inglês está disponível por padrão e não pode ser removido.  

-   **Nome da chave:** MobileDeviceLanguage  

    -   **Obrigatório:** Sim  

    -   **Valores:** 0 ou 1  

         0 = Não instalar  

         1 = Instalar  

    -   **Detalhes:** especifica se os idiomas do cliente do dispositivo móvel estão instalados.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Nome do SQL Server*>  

    -   **Detalhes:** especifica o nome do servidor ou da instância clusterizada que executa o SQL Server e que hospedará o banco de dados do site.  

-   **Nome da chave:** DatabaseName  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Nome do banco de dados do site*> ou <*Nome da instância*>\\<*Nome do banco de dados do site*>  

    -   **Detalhes:** especifica o nome do banco de dados do SQL Server a ser criado ou o banco de dados do SQL Server a ser usado durante a instalação do banco de dados do site de administração central.  

        > [!IMPORTANT]  
        >  Se você não usar a instância padrão, precisará especificar o nome da instância e o nome do banco de dados do site.  

-   **Nome da chave:** SQLSSBPort  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*Número da porta SSB*>  

    -   **Detalhes:** especifica a porta do SSB (SQL Server Service Broker) a ser usada pelo SQL Server. Normalmente, o SSB está configurado para usar a porta TCP 4022, mas é possível usar outra porta.  

-   **Nome da chave:** SQLDataFilePath  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*Caminho para o arquivo .mdb do banco de dados*>  

    -   **Detalhes:** especifica um local alternativo para criar o arquivo .mdb do banco de dados.  

-   **Nome da chave:** SQLLogFilePath  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*Caminho para o arquivo .ldf do banco de dados*>  

    -   **Detalhes:** especifica um local alternativo para criar o arquivo .ldf do banco de dados.  

**CloudConnectorOptions**  

-   **Nome da chave:** CloudConnector  

    -   **Obrigatório:** Sim  

    -   **Valores:** 0 ou 1  

         0 = Não instalar  

         1 = Instalar  

    -   **Detalhes:** especifica se um ponto de conexão de serviço será instalado neste site. Como o ponto de conexão de serviço pode ser instalado somente no site de camada superior de uma hierarquia, esse valor deverá ser **0** para um site primário filho.  

-   **Nome da chave:** CloudConnectorServer  

    -   **Obrigatório:** obrigatório quando **CloudConnector** for igual a 1  

    -   **Valores:**  <*FQDN do servidor de ponto de conexão de serviço*>  

    -   **Detalhes:** especifica o FQDN do servidor que hospedará a função do sistema de sites do ponto de conexão do serviço.  

-   **Nome da chave:** UseProxy  

    -   **Obrigatório:** obrigatório quando **CloudConnector** for igual a 1  

    -   **Valores:** 0 ou 1  

         0 = Não instalar  

         1 = Instalar  

    -   **Detalhes:** especifica se o ponto de conexão de serviço usa um servidor proxy.  

-   **Nome da chave:** ProxyName  

    -   **Obrigatório:** obrigatório quando **UseProxy** for igual a 1  

    -   **Valores:**  <*FQDN do servidor proxy*>  

    -   **Detalhes:** especifica o FQDN do servidor proxy usado pelo ponto de conexão de serviço.  

-   **Nome da chave:** ProxyPort  

    -   **Obrigatório:** obrigatório quando **UseProxy** for igual a 1  

    -   **Valores:**  <*Número da porta*>  

    -   **Detalhes:** especifica o número da porta a ser usado para a porta do proxy.  

### <a name="unattended-install-for-a-primary-site"></a>Instalação autônoma de um site primário  
Use os detalhes a seguir para instalar um site primário usando um arquivo de script de instalação autônoma.  

**Identificação**  

-   **Nome da chave:** Ação  

    -   **Obrigatório:** Sim  

    -   **Valores:** InstallPrimarySite  

    -   **Detalhes:** instala um site primário.  

-   **Nome da chave:** CDLatest  

    -   **Obrigatório:** Sim – somente ao usar a mídia da pasta CD.Latest.    

    -   **Valores:** 1 qualquer valor diferente de 1 é considerado como não usando o CD.Latest.

    -   **Detalhes:** seu script deve incluir essa chave e o valor ao executar a instalação de uma mídia em uma pasta CD.Latest com a finalidade de instalar um site primário ou de administração central ou recuperar um site de administração central ou primário. Esse valor informa à instalação que a forma de mídia CD.Latest está sendo usada.

**Opções**  

-   **Nome da chave:** ProductID  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *ou* Eval  

    -   **Detalhes:** especifica a chave do produto (Product Key) de instalação do Configuration Manager, incluindo os traços. Insira **Eval** para instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** SiteCode  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Código do site*>  

    -   **Detalhes:** especifica três caracteres alfanuméricos que identificam exclusivamente o site na hierarquia.  

-   **Nome da chave:** SiteName  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Nome do site*>  

    -   **Detalhes:** especifica o nome para esse site.  

-   **Nome da chave:** SMSInstallDir  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Caminho de instalação do Configuration Manager*>

    -   **Detalhes:** especifica a pasta de instalação dos arquivos de programa do Configuration Manager.  

-   **Nome da chave:** SDKServer  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*FQDN do Provedor de SMS*>  

    -   **Detalhes:** especifica o FQDN para o servidor que hospedará o Provedor de SMS. Você pode configurar outros Provedores de SMS para o site após a instalação inicial.  

-   **Nome da chave:** PrerequisiteComp  

    -   **Obrigatório:** Sim  

    -   **Valores:** 0 ou 1  

         0 = Baixar  

         1 = Já baixado  

    -   **Detalhes:** Especifica se os arquivos de pré-requisito da instalação já foram baixados. Por exemplo, se você usar o valor **0**, a instalação baixará os arquivos.  

-   **Nome da chave:** PrerequisitePath  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Caminho para os arquivos de pré-requisito da instalação*>  

    -   **Detalhes:** Especifica o caminho para os arquivos de pré-requisito da instalação. Dependendo do valor de **PrerequisiteComp**, a instalação usará esse caminho para armazenar os arquivos baixados ou para localizar os arquivos baixados anteriormente.  

-   **Nome da chave:** AdminConsole  

    -   **Obrigatório:** Sim  

    -   **Valores:** 0 ou 1  

         0 = Não instalar  

         1 = Instalar  

    -   **Detalhes:** especifica se deseja instalar o console do Configuration Manager.  

-   **Nome da chave:** JoinCEIP  
    > [!Note]  
    > A partir do Configuration Manager versão 1802, o recurso Programa de Aperfeiçoamento da Experiência do Usuário é removido do produto.

    -   **Obrigatório:** Sim  

    -   **Valores:** 0 ou 1  

         0 = Não ingressar  

         1 = Ingressar  

    -   **Detalhes:** especifica o ingresso ou não no Programa de Aperfeiçoamento da Experiência do Usuário.  

-   **Nome da chave:** ManagementPoint  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*FQDN do servidor do site do ponto de gerenciamento*>  

    -   **Detalhes:** especifica o FQDN do servidor que hospedará a função de sistema de site do ponto de gerenciamento.  

-   **Nome da chave:** ManagementPointProtocol  

    -   **Obrigatório:** Não  

    -   **Valores:** HTTPS *ou* HTTP  

    -   **Detalhes:** especifica o protocolo a ser usado para o ponto de gerenciamento.  

-   **Nome da chave:** DistributionPoint  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*FQDN do servidor do site do ponto de distribuição*>  

    -   **Detalhes:** especifica o protocolo a ser usado para o ponto de distribuição.  

-   **Nome da chave:** DistributionPointProtocol  

    -   **Obrigatório:** Não  

    -   **Valores:** HTTPS *ou* HTTP  

    -   **Detalhes:** especifica o protocolo a ser usado para o ponto de distribuição.  

-   **Nome da chave:** RoleCommunicationProtocol  

    -   **Obrigatório:** Sim  

    -   **Valores:** EnforceHTTPS *ou* HTTPorHTTPS  

    -   **Detalhes:** especifica se deve configurar todos os sistemas de sites para aceitar somente a comunicação HTTPS de clientes ou para o método de comunicação a ser definido para cada função do sistema de sites. Ao selecionar **EnforceHTTPS**, o computador cliente deverá ter um certificado PKI (infraestrutura de chave pública) válido para a autenticação de cliente.  

-   **Nome da chave:** ClientsUsePKICertificate  

    -   **Obrigatório:** Sim  

    -   **Valores:** 0 ou 1  

         0 = Não usar  

         1 = Usar  

    -   **Detalhes:** especifica se os clientes usarão um certificado PKI de cliente para se comunicar com as funções do sistema de site.  

-   **Nome da chave:** AddServerLanguages  

    -   **Obrigatório:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** especifica os idiomas do servidor que estarão disponíveis para o console do Configuration Manager, relatórios e objetos do Configuration Manager. Inglês está disponível por padrão.  

-   **Nome da chave:** AddClientLanguages  

    -   **Obrigatório:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** especifica os idiomas que estarão disponíveis para computadores cliente. Inglês está disponível por padrão.  

-   **Nome da chave:** DeleteServerLanguages  

    -   **Obrigatório:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** modifica um site após a instalação. Especifica os idiomas a serem removidos e que não estarão mais disponíveis para o console, os relatórios e objetos do Configuration Manager. Inglês está disponível por padrão e não pode ser removido.  

-   **Nome da chave:** DeleteClientLanguages  

    -   **Obrigatório:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** modifica um site após a instalação. Especifica os idiomas a serem removidos e que não estarão mais disponíveis para os computadores cliente. Inglês está disponível por padrão e não pode ser removido.  

-   **Nome da chave:** MobileDeviceLanguage  

    -   **Obrigatório:** Sim  

    -   **Valores:** 0 ou 1  

         0 = Não instalar  

         1 = Instalar  

    -   **Detalhes:** especifica se os idiomas do cliente do dispositivo móvel estão instalados.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Nome do SQL Server*>  

    -   **Detalhes:** especifica o nome do servidor ou da instância clusterizada que executa o SQL Server e que hospedará o banco de dados do site.  

-   **Nome da chave:** DatabaseName  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Nome do banco de dados do site*> ou <*Nome da instância*>\\<*Nome do banco de dados do site*>  

    -   **Detalhes:** especifica o nome do banco de dados SQL Server a ser criado ou o banco de dados SQL Server a ser usado durante a instalação do banco de dados do site primário.  

        > [!IMPORTANT]  
        >  Se você não usar a instância padrão, precisará especificar o nome da instância e o nome do banco de dados do site.  

-   **Nome da chave:** SQLSSBPort  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*Número da porta SSB*>  

    -   **Detalhes:** especifica a porta SSB usada pelo SQL Server. Normalmente, o SSB está configurado para usar a porta TCP 4022, mas é possível usar outra porta.  

-   **Nome da chave:** SQLDataFilePath  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*Caminho para o arquivo .mdb do banco de dados*>  

    -   **Detalhes:** especifica um local alternativo para criar o arquivo .mdb do banco de dados.  

-   **Nome da chave:** SQLLogFilePath  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*Caminho para o arquivo .ldf do banco de dados*>  

    -   **Detalhes:** especifica um local alternativo para criar o arquivo .ldf do banco de dados.  

**HierarchyExpansionOption**  

-   **Nome da chave:** CCARSiteServer  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*FQDN do site de administração central*>  

    -   **Detalhes:** especifica o site de administração central ao qual o site primário é anexado quando ele ingressa na hierarquia do Configuration Manager. Especifique o site de administração central durante a instalação.  

-   **Nome da chave:** CASRetryInterval  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*Interval*>  

    -   **Detalhes:** especifica o intervalo de repetição (em minutos) para tentar uma conexão ao site de administração central depois de a conexão falhar. Por exemplo, se a conexão com o site de administração central falhar, o site primário aguardará o número de minutos especificados para o valor de **CASRetryInterval** e, em seguida, tentará a conexão novamente.  

-   **Nome da chave:** WaitForCASTimeout  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*Timeout*>  

         Um valor de **0** a **100**  

    -   **Detalhes:** especifica o valor máximo do tempo limite (em minutos) para o site primário se conectar ao site de administração central. Por exemplo, se o site primário falhar ao se conectar ao site de administração central, o site primário tentará a conexão novamente ao site de administração central com base no valor de **CASRetryInterval** até atingir o período de **WaitForCASTimeout**. É possível especificar um valor de **0** a **100**.  

**CloudConnectorOptions**  

-   **Nome da chave:** CloudConnector  

    -   **Obrigatório:** Sim  

    -   **Valores:** 0 ou 1  

         0 = Não instalar  

         1 = Instalar  

    -   **Detalhes:** especifica se um ponto de conexão de serviço será instalado neste site. Como o ponto de conexão de serviço pode ser instalado somente no site de camada superior de uma hierarquia, esse valor deverá ser **0** para um site primário filho.  

-   **Nome da chave:** CloudConnectorServer  

    -   **Obrigatório:** obrigatório quando **CloudConnector** for igual a 1  

    -   **Valores:**  <*FQDN do servidor de ponto de conexão de serviço*\>  

    -   **Detalhes:** especifica o FQDN do servidor que hospedará a função do sistema de sites do ponto de conexão do serviço.  

-   **Nome da chave:** UseProxy  

    -   **Obrigatório:** obrigatório quando **CloudConnector** for igual a 1  

    -   **Valores:** 0 ou 1  

         0 = Não instalar  

         1 = Instalar  

    -   **Detalhes:** especifica se o ponto de conexão de serviço usa um servidor proxy.  

-   **Nome da chave:** ProxyName  

    -   **Obrigatório:** obrigatório quando **UseProxy** for igual a 1  

    -   **Valores:**  <*FQDN do servidor proxy*>  

    -   **Detalhes:** especifica o FQDN do servidor proxy usado pelo ponto de conexão de serviço.  

-   **Nome da chave:** ProxyPort  

    -   **Obrigatório:** obrigatório quando **UseProxy** for igual a 1  

    -   **Valores:**  <*Número da porta*>  

    -   **Detalhes:** especifica o número da porta a ser usado para a porta do proxy.  

### <a name="unattended-recovery-for-a-central-administration-site"></a>Recuperação autônoma de um site de administração central  
 Use os detalhes a seguir para recuperar um site de administração central usando um arquivo de script de instalação autônoma.  

**Identificação**  

-   **Nome da chave:** Ação  

    -   **Obrigatório:** Sim  

    -   **Valores:** RecoverCCAR  

    -   **Detalhes:** recupera um site de administração central.  

-   **Nome da chave:** CDLatest  

    -   **Obrigatório:** Sim – somente ao usar a mídia da pasta CD.Latest.    

    -   **Valores:** 1 qualquer valor diferente de 1 é considerado como não usando o CD.Latest.

    -   **Detalhes:** seu script deve incluir essa chave e o valor ao executar a instalação de uma mídia em uma pasta CD.Latest com a finalidade de instalar um site primário ou de administração central ou recuperar um site de administração central ou primário. Esse valor informa à instalação que a forma de mídia CD.Latest está sendo usada.

**RecoveryOptions**  

-   **Nome da chave:** ServerRecoveryOptions  

    -   **Obrigatório:** Sim  

    -   **Valores:** 1, 2 ou 4  

         1 = Recuperar servidor do site e SQL Server.  

         2 = Recuperar apenas o servidor do site.  

         4 = Recuperar apenas o SQL Server.  

    -   **Detalhes:** especifica se a instalação recupera o servidor do site, o SQL Server ou ambos. As chaves associadas são necessárias quando o seguinte valor é definido para a configuração **ServerRecoveryOptions**:  

        -   Valor = 1: Você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.  

        -   Valor = 2: Você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.  

        -   Valor = 4: A chave **BackupLocation** é necessária quando o valor **10** é configurado para a chave **DatabaseRecoveryOptions** , que restaura o banco de dados do site por meio do backup.  

-   **Nome da chave:** DatabaseRecoveryOptions  

    -   **Obrigatório:** Essa chave é necessária quando a configuração **ServerRecoveryOptions** tem o valor **1** ou **4**.  

    -   **Valores:** 10, 20, 40 ou 80  

         10 = Restaurar, por meio do backup, o banco de dados do site.  

         20 = Usar um banco de dados do site recuperado manualmente usando outro método.  

         40 = Criar um novo banco de dados para o site. Use essa opção quando não houver backup do banco de dados do site disponível. Os dados globais e do site são recuperados por meio da replicação de outros sites.  

         80 = Ignorar recuperação do banco de dados.  

    -   **Detalhes:** Especifica como a instalação recupera o banco de dados do site no SQL Server.  

-   **Nome da chave:** ReferenceSite  

    -   **Obrigatório:** Essa chave é necessária quando a configuração **DatabaseRecoveryOptions** tem o valor **40**.  

    -   **Valores:**  <*FQDN do site de referência*>  

    -   **Detalhes:** especifica o site primário de referência que o site de administração central usará para recuperar dados globais se o backup do banco de dados for mais antigo que o período de retenção do controle de alterações ou quando o site for recuperado sem backup.  

         Quando um site de referência não é especificado e o backup é mais antigo que o período de retenção do controle de alterações, todos os sites primários são reinicializados com os dados restaurados por meio do site de administração central.  

         Caso você não especifique um site de referência e o backup esteja dentro do período de retenção do controle de alterações, somente as alterações feitas após o backup serão replicadas dos sites primários. Quando houver alterações conflitantes de sites primários diferentes, o site de administração central usará a primeira alteração que receber.  

-   **Nome da chave:** SiteServerBackupLocation  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*Caminho para o conjunto de backup do servidor do site*>  

    -   **Detalhes:** Especifica o caminho para o conjunto de backup do servidor de site. Essa chave é opcional quando a configuração **ServerRecoveryOptions** tem o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.  

-   **Nome da chave:** BackupLocation  

    -   **Obrigatório:** essa chave é obrigatória quando você configura um valor **1** ou **4** para a chave **ServerRecoveryOptions** e um valor **10** para a chave **DatabaseRecoveryOptions**.  

    -   **Valores:**  <*Caminho para o conjunto de backup do banco de dados do site*>  

    -   **Detalhes:** especifica o caminho para o conjunto de backup do banco de dados do site.  

**Opções**  

-   **Nome da chave:** ProductID  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *ou* Eval  

    -   **Detalhes:** especifica a chave do produto (Product Key) de instalação do Configuration Manager, incluindo os traços. Insira **Eval** para instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** SiteCode  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Código do site*>  

    -   **Detalhes:** especifica três caracteres alfanuméricos que identificam exclusivamente o site na hierarquia. Especifique o código do site usado pelo site antes da falha.

-   **Nome da chave:** SiteName  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*Nome do site*>  

    -   **Detalhes:** especifica o nome para esse site.  

-   **Nome da chave:** SMSInstallDir  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Caminho de instalação do Configuration Manager*>  

    -   **Detalhes:** especifica a pasta de instalação dos arquivos de programa do Configuration Manager.  

-   **Nome da chave:** SDKServer  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*FQDN do Provedor de SMS*>  

    -   **Detalhes:** especifica o FQDN do servidor que hospeda o Provedor de SMS. Especifique o servidor que hospedou o Provedor de SMS antes da falha.  

         Você pode configurar outros Provedores de SMS para o site após a instalação inicial. Para obter mais informações sobre o Provedor de SMS, consulte [Planejar o Provedor de SMS para o System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Nome da chave:** PrerequisiteComp  

    -   **Obrigatório:** Sim  

    -   **Valores:** 0 ou 1  

         0 = Baixar  

         1 = Já baixado  

    -   **Detalhes:** Especifica se os arquivos de pré-requisito da instalação já foram baixados. Por exemplo, se você usar o valor **0**, a instalação baixará os arquivos.  

-   **Nome da chave:** PrerequisitePath  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Caminho para os arquivos de pré-requisito da instalação*>  

    -   **Detalhes:** Especifica o caminho para os arquivos de pré-requisito da instalação. Dependendo do valor de **PrerequisiteComp**, a instalação usará esse caminho para armazenar os arquivos baixados ou para localizar os arquivos baixados anteriormente.  

-   **Nome da chave:** AdminConsole  

    -   **Obrigatório:** Essa chave é necessária quando a configuração de **ServerRecoveryOptions** tem o valor **4**.  

    -   **Valores:** 0 ou 1  

         0 = Não instalar  

         1 = Instalar  

    -   **Detalhes:** especifica se deseja instalar o console do Configuration Manager.  

-   **Nome da chave:** JoinCEIP  
    > [!Note]  
    > A partir do Configuration Manager versão 1802, o recurso Programa de Aperfeiçoamento da Experiência do Usuário é removido do produto.

    -   **Obrigatório:** Sim  

    -   **Valores:** 0 ou 1  

         0 = Não ingressar  

         1 = Ingressar  

    -   **Detalhes:** especifica o ingresso ou não no Programa de Aperfeiçoamento da Experiência do Usuário.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Nome do SQL Server*>  

    -   **Detalhes:** especifica o nome do servidor ou da instância clusterizada que executa o SQL Server e que hospeda o banco de dados do site. Especifique o mesmo servidor que hospedou o banco de dados do site antes da falha.  

-   **Nome da chave:** DatabaseName  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Nome do banco de dados do site*> ou <*Nome da instância*>\\<*Nome do banco de dados do site*>  

    -   **Detalhes:** Especifica o nome do banco de dados SQL Server a ser criado ou o banco de dados SQL Server a ser usado durante a instalação do banco de dados do site de administração central. Especifique o mesmo nome do banco de dados usado antes da falha.  

        > [!IMPORTANT]  
        >  Se você não usar a instância padrão, precisará especificar o nome da instância e o nome do banco de dados do site.  

-   **Nome da chave:** SQLSSBPort  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Número da porta SSB*>  

    -   **Detalhes:** especifica a porta SSB usada pelo SQL Server. Normalmente, o SSB está configurado para usar a porta TCP 4022. Especifique a mesma porta SSB usada antes da falha.  

-   **Nome da chave:** SQLDataFilePath  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*Caminho para o arquivo .mdb do banco de dados*>  

    -   **Detalhes:** especifica um local alternativo para criar o arquivo .mdb do banco de dados.  

-   **Nome da chave:** SQLLogFilePath  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*Caminho para o arquivo .ldf do banco de dados*>  

    -   **Detalhes:** especifica um local alternativo para criar o arquivo .ldf do banco de dados.  

**CloudConnectorOptions**  

-   **Nome da chave:** CloudConnector  

    -   **Obrigatório:** Sim  

    -   **Valores:** 0 ou 1  

         0 = Não instalar  

         1 = Instalar  

    -   **Detalhes:** especifica se um ponto de conexão de serviço será instalado neste site. Como o ponto de conexão de serviço pode ser instalado somente no site de camada superior de uma hierarquia, esse valor deverá ser **0** para um site primário filho.  

-   **Nome da chave:** CloudConnectorServer  

    -   **Obrigatório:** obrigatório quando **CloudConnector** for igual a 1  

    -   **Valores:**  <*FQDN do servidor de ponto de conexão de serviço*>  

    -   **Detalhes:** especifica o FQDN do servidor que hospedará a função do sistema de sites do ponto de conexão do serviço.  

-   **Nome da chave:** UseProxy  

    -   **Obrigatório:** obrigatório quando **CloudConnector** for igual a 1  

    -   **Valores:** 0 ou 1  

         0 = Não instalar  

         1 = Instalar  

    -   **Detalhes:** especifica se o ponto de conexão de serviço usa um servidor proxy.  

-   **Nome da chave:** ProxyName  

    -   **Obrigatório:** obrigatório quando **CloudConnector** for igual a 1  

    -   **Valores:**  <*FQDN do servidor proxy*>  

    -   **Detalhes:** especifica o FQDN do servidor proxy usado pelo ponto de conexão de serviço.  

-   **Nome da chave:** ProxyPort  

    -   **Obrigatório:** obrigatório quando **CloudConnector** for igual a 1  

    -   **Valores:**  <*Número da porta*>  

    -   **Detalhes:** especifica o número da porta a ser usado para a porta do proxy.  

### <a name="unattended-recovery-for-a-primary-site"></a>Recuperação autônoma de um site primário  
 Use os detalhes a seguir para recuperar um site primário usando um arquivo de script de instalação autônoma.  

**Identificação**  

-   **Nome da chave:** Ação  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*RecoverPrimarySite*>  

    -   **Detalhes:** recupera um site primário.  

-   **Nome da chave:** CDLatest  

    -   **Obrigatório:** Sim – somente ao usar a mídia da pasta CD.Latest.    

    -   **Valores:** 1 qualquer valor diferente de 1 é considerado como não usando o CD.Latest.

    -   **Detalhes:** seu script deve incluir essa chave e o valor ao executar a instalação de uma mídia em uma pasta CD.Latest com a finalidade de instalar um site primário ou de administração central ou recuperar um site de administração central ou primário. Esse valor informa à instalação que a forma de mídia CD.Latest está sendo usada.    

**RecoveryOptions**  

-   **Nome da chave:** ServerRecoveryOptions  

    -   **Obrigatório:** Sim  

    -   **Valores:** 1, 2 ou 4  

         1 = Recuperar servidor do site e SQL Server.  

         2 = Recuperar apenas o servidor do site.  

         4 = Recuperar apenas o SQL Server.  

    -   **Detalhes:** especifica se a instalação recupera o servidor do site, o SQL Server ou ambos. As chaves associadas são necessárias quando o seguinte valor é definido para a configuração **ServerRecoveryOptions**:  

        -   Valor = 1: Você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.  

        -   Valor = 2: Você tem a opção de especificar um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.  

        -   Valor = 4: A chave **BackupLocation** é necessária quando o valor **10** é configurado para a chave **DatabaseRecoveryOptions** , que restaura o banco de dados do site por meio do backup.  

-   **Nome da chave:** DatabaseRecoveryOptions  

    -   **Obrigatório:** Essa chave é necessária quando a configuração **ServerRecoveryOptions** tem o valor **1** ou **4**.  

    -   **Valores:** 10, 20, 40 ou 80  

         10 = Restaurar, por meio do backup, o banco de dados do site.  

         20 = Usar um banco de dados do site recuperado manualmente usando outro método.  

         40 = Criar um novo banco de dados para o site. Use essa opção quando não houver backup do banco de dados do site disponível. Os dados globais e do site são recuperados por meio da replicação de outros sites.  

         80 = Ignorar recuperação do banco de dados.  

    -   **Detalhes:** Especifica como a instalação recupera o banco de dados do site no SQL Server.  

-   **Nome da chave:** SiteServerBackupLocation  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*Caminho para o conjunto de backup do servidor do site*>  

    -   **Detalhes:**  

         Especifica o caminho para o conjunto de backup do servidor de site. Essa chave é opcional quando a configuração **ServerRecoveryOptions** tem o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** recuperar o site usando um backup do site. Caso não especifique um valor, o site é reinstalado sem ser restaurado por meio de um conjunto de backup.  

-   **Nome da chave:** BackupLocation  

    -   **Obrigatório:** essa chave é obrigatória quando você configura um valor **1** ou **4** para a chave **ServerRecoveryOptions** e um valor **10** para a chave **DatabaseRecoveryOptions**.  

    -   **Valores:**  <*Caminho para o conjunto de backup do banco de dados do site*>  

    -   **Detalhes:** especifica o caminho para o conjunto de backup do banco de dados do site.  

**Opções**  

-   **Nome da chave:** ProductID  

    -   **Obrigatório:** Sim  

    -   **Valores:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* ou *Eval*  

    -   **Detalhes:** especifica a chave do produto (Product Key) de instalação do Configuration Manager, incluindo os traços. Insira **Eval** para instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** SiteCode  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Código do site*>  

    -   **Detalhes:** especifica três caracteres alfanuméricos que identificam exclusivamente o site na hierarquia. Especifique o código do site usado pelo site antes da falha.

-   **Nome da chave:** SiteName  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*Nome do site*>  

    -   **Detalhes:** especifica o nome para esse site.  

-   **Nome da chave:** SMSInstallDir  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Caminho de instalação do Configuration Manager*>  

    -   **Detalhes:** especifica a pasta de instalação dos arquivos de programa do Configuration Manager.  

-   **Nome da chave:** SDKServer  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*FQDN do Provedor de SMS*>  

    -   **Detalhes:** especifica o FQDN do servidor que hospeda o Provedor de SMS. Especifique o servidor que hospedou o Provedor de SMS antes da falha. Configure Provedores de SMS adicionais para o site após a instalação inicial. Para obter mais informações sobre o Provedor de SMS, consulte [Planejar o Provedor de SMS](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Nome da chave:** PrerequisiteComp  

    -   **Obrigatório:** Sim  

    -   **Valores:** 0 ou 1  

         0 = Baixar  

         1 = Já baixado  

    -   **Detalhes:** Especifica se os arquivos de pré-requisito da instalação já foram baixados. Por exemplo, se você usar o valor **0**, a instalação baixará os arquivos.  

-   **Nome da chave:** PrerequisitePath  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Caminho para os arquivos de pré-requisito da instalação*>  

    -   **Detalhes:** Especifica o caminho para os arquivos de pré-requisito da instalação. Dependendo do valor de **PrerequisiteComp**, a instalação usará esse caminho para armazenar os arquivos baixados ou para localizar os arquivos baixados anteriormente.  

-   **Nome da chave:** AdminConsole  

    -   **Obrigatório:** Essa chave é necessária quando a configuração de **ServerRecoveryOptions** tem o valor **4**.  

    -   **Valores:** 0 ou 1  

         0 = Não instalar  

         1 = Instalar  

    -   **Detalhes:** especifica se deseja instalar o console do Configuration Manager.  

-   **Nome da chave:** JoinCEIP  
    > [!Note]  
    > A partir do Configuration Manager versão 1802, o recurso Programa de Aperfeiçoamento da Experiência do Usuário é removido do produto.

    -   **Obrigatório:** Sim  

    -   **Valores:** 0 ou 1  

         0 = Não ingressar  

         1 = Ingressar  

    -   **Detalhes:** especifica o ingresso ou não no Programa de Aperfeiçoamento da Experiência do Usuário.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Nome do SQL Server*>  

    -   **Detalhes:** especifica o nome do servidor ou da instância clusterizada que executa o SQL Server e que hospeda o banco de dados do site. Especifique o mesmo servidor que hospedou o banco de dados do site antes da falha.  

-   **Nome da chave:** DatabaseName  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Nome do banco de dados do site*> ou <*Nome da instância*>\\<*Nome do banco de dados do site*>

    -   **Detalhes:**  

         Especifica o nome do banco de dados SQL Server a ser criado ou o banco de dados SQL Server a ser usado durante a instalação do banco de dados do site de administração central. Especifique o mesmo nome do banco de dados usado antes da falha.  

        > [!IMPORTANT]  
        >  Se você não usar a instância padrão, precisará especificar o nome da instância e o nome do banco de dados do site.  

-   **Nome da chave:** SQLSSBPort  

    -   **Obrigatório:** Sim  

    -   **Valores:**  <*Número da porta SSB*>  

    -   **Detalhes:** especifica a porta SSB usada pelo SQL Server. Normalmente, o SSB está configurado para usar a porta TCP 4022. Especifique a mesma porta SSB usada antes da falha.  

-   **Nome da chave:** SQLDataFilePath  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*Caminho para o arquivo .mdb do banco de dados*>  

    -   **Detalhes:** especifica um local alternativo para criar o arquivo .mdb do banco de dados.  

-   **Nome da chave:** SQLLogFilePath  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*Caminho para o arquivo .ldf do banco de dados*>  

    -   **Detalhes:** especifica um local alternativo para criar o arquivo .ldf do banco de dados.  

**HierarchyExpansionOptions**  

-   **Nome da chave:** CCARSiteServer  

    -   **Obrigatório:** ver detalhes.  

    -   **Valores:**  <*Código do site de administração central*>  

    -   **Detalhes:** especifica o site de administração central ao qual o site primário é anexado quando ingressa na hierarquia do Configuration Manager. Essa configuração é necessária se o site primário foi anexado ao site de administração central antes da falha. Especifique o código do site usado para o site de administração central antes da falha.  

-   **Nome da chave:** CASRetryInterval  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*Interval*>  

    -   **Detalhes:** especifica o intervalo de repetição (em minutos) para tentar uma conexão ao site de administração central depois de a conexão falhar. Por exemplo, se a conexão com o site de administração central falhar, o site primário aguardará o número de minutos especificados para o valor de **CASRetryInterval** e, em seguida, tentará a conexão novamente.  

-   **Nome da chave:** WaitForCASTimeout  

    -   **Obrigatório:** Não  

    -   **Valores:**  <*Timeout*>  

    -   **Detalhes:** especifica o valor máximo do tempo limite (em minutos) para o site primário se conectar ao site de administração central. Por exemplo, se o site primário falhar ao se conectar ao site de administração central, o site primário tentará a conexão novamente ao site de administração central com base no valor de **CASRetryInterval** até atingir o período de **WaitForCASTimeout**. É possível especificar um valor de **0** a **100**.  

**CloudConnectorOptions**  

-   **Nome da chave:** CloudConnector  

    -   **Obrigatório:** Sim  

    -   **Valores:** 0 ou 1  

         0 = Não instalar  

         1 = Instalar  

    -   **Detalhes:** especifica se um ponto de conexão de serviço será instalado neste site. Como o ponto de conexão de serviço pode ser instalado somente no site de camada superior de uma hierarquia, esse valor deverá ser **0** para um site primário filho.  

-   **Nome da chave:** CloudConnectorServer  

    -   **Obrigatório:** obrigatório quando **CloudConnector** for igual a 1  

    -   **Valores:**  <*FQDN do servidor de ponto de conexão de serviço*>  

    -   **Detalhes:** especifica o FQDN do servidor que hospedará a função do sistema de sites do ponto de conexão do serviço.  

-   **Nome da chave:** UseProxy  

    -   **Obrigatório:** obrigatório quando **CloudConnector** for igual a 1  

    -   **Valores:** 0 ou 1  

         0 = Não instalar  

         1 = Instalar  

    -   **Detalhes:** especifica se o ponto de conexão de serviço usa um servidor proxy.  

-   **Nome da chave:** ProxyName  

    -   **Obrigatório:** obrigatório quando **CloudConnector** for igual a 1  

    -   **Valores:**  <*FQDN do servidor proxy*>  

    -   **Detalhes:** especifica o FQDN do servidor proxy usado pelo ponto de conexão de serviço.  

-   **Nome da chave:** ProxyPort  

    -   **Obrigatório:** obrigatório quando **CloudConnector** for igual a 1  

    -   **Valores:**  <*Número da porta*>  

    -   **Detalhes:** especifica o número da porta a ser usado para a porta do proxy.  
