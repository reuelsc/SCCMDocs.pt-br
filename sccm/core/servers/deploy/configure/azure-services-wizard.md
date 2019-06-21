---
title: Configurar serviços do Azure
titleSuffix: Configuration Manager
description: Conecte o ambiente do Configuration Manager aos serviços do Azure para o gerenciamento de nuvem, ao Upgrade Readiness, à Microsoft Store para Empresas e ao Log Analytics.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6d7acf1d5c73c59f2ce1e6d2b7f3f7354e21979
ms.sourcegitcommit: 86968fc2f129e404ff8e08f91a05fa17b5c47527
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2019
ms.locfileid: "67251884"
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configurar serviços do Azure para uso com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o **Assistente de Serviços do Azure** para simplificar o processo de configuração dos serviços de nuvem do Azure usados com o Configuration Manager. Esse assistente fornece uma experiência de configuração comum usando os registros do aplicativo Web do Azure AD (Azure Active Directory). Esses aplicativos fornecem detalhes de assinatura e de configuração e autenticam a comunicação com o Azure AD. O aplicativo substitui a necessidade de inserir essas mesmas informações sempre que você configura um novo componente ou serviço do Configuration Manager com o Azure.



## <a name="available-services"></a>Serviços disponíveis

Configure os seguintes serviços do Azure usando esse assistente:  

-   **Gerenciamento de Nuvem**: com esse serviço, o site e os clientes podem se autenticar usando o Azure AD. Essa autenticação possibilita outros cenários, como:  

    - [Instalar e atribuir clientes do Windows 10 do Configuration Manager usando o Azure AD para autenticação](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

    - [Configurar a descoberta de usuários do Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

    - Suporte a alguns [cenários do gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#scenarios)  

-   **Conector do Log Analytics**: [conecta ao Azure Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics). Sincronize dados de coleta para o Log Analytics.  

    > [!Note]  
    > Este artigo refere-se ao *Conector do Log Analytics*, que antes era chamado de *Conector do OMS*. Não há diferença funcional. Para saber mais, veja [Gerenciamento do Azure - Monitoramento](/azure/azure-monitor/terminology#log-analytics).  

-   **Conector do Upgrade Readiness**: conecta ao [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) do Windows Analytics. Exiba os dados de compatibilidade da atualização do cliente.  

-   **Microsoft Store para Empresas**: conecta ao [Microsoft Store para Empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business). Obtenha aplicativos da loja para sua organização que podem ser implantados com o Configuration Manager.  

### <a name="service-details"></a>Detalhes do serviço

A tabela a seguir lista os detalhes sobre cada um dos serviços.  

- **Locatários**: o número de instâncias de serviço que podem ser configuradas. Cada instância deve ser um locatário distinto do Azure.  

- **Nuvens**: todos os serviços são compatíveis com a nuvem global do Azure, mas nem todos são compatíveis com nuvens privadas, como a nuvem do Azure US Government.  

- **Aplicativo Web**: indica se o serviço usa um aplicativo do Azure AD do tipo *aplicativo Web/API*, também chamado de aplicativo para servidores no Configuration Manager.  

- **Aplicativo nativo**: indica se o serviço usa um aplicativo do Azure AD do tipo *Nativo*, também chamado de aplicativo cliente no Configuration Manager.  

- **Ações**: indica que você pode importar ou criar esses aplicativos no Assistente de Serviços do Azure do Configuration Manager.  


|Serviço  |Locatários  |Nuvens  |Aplicativo Web  |Aplicativo nativo  |Ações  |
|---------|---------|---------|---------|---------|---------|
|Gerenciamento de nuvem com<br>Descoberta de usuários do Azure AD | Vários | Público, privado | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | Importar, criar |
|Conector do Log Analytics | Um | Público, privado | ![Com suporte](media/green_check.png) | ![Sem suporte](media/Red_X.png) | Importar |
|Upgrade Readiness | Um | Público | ![Com suporte](media/green_check.png) | ![Sem suporte](media/Red_X.png) | Importar |
|Microsoft Store para<br>Empresas | Um | Público | ![Com suporte](media/green_check.png) | ![Sem suporte](media/Red_X.png) | Importar, criar |


### <a name="about-azure-ad-apps"></a>Sobre os aplicativos do Azure AD

Diferentes serviços do Azure exigem configurações distintas, que podem ser feitas no portal do Azure. Além disso, os aplicativos para cada serviço podem exigir permissões separadas aos recursos do Azure.  

Você pode usar um único aplicativo para mais de um serviço. Há apenas um objeto a ser gerenciado no Configuration Manager e no Azure AD. Quando a chave de segurança no aplicativo expira, você precisa apenas atualizar uma chave.

<!-- The most secure configuration is using separate apps for each service. An app for one service might require additional permissions that another service doesn't require. Using one app for different services can provide the app with more permissions than it otherwise requires. 
 --> 

Quando você cria serviços adicionais do Azure no assistente, o Configuration Manager é projetado para reutilizar as informações comuns entre serviços. Esse comportamento ajuda você a eliminar a necessidade de inserir as mesmas informações mais de uma vez. 

Para obter mais informações sobre as permissões de aplicativo necessárias e as configurações de cada serviço, consulte o artigo relevante do Configuration Manager em [Serviços disponíveis](#available-services). 

Para obter mais informações sobre os aplicativos do Azure, comece com os seguintes artigos:
- [Autenticação e autorização no Serviço de Aplicativo do Azure](/azure/app-service/app-service-authentication-overview)
- [Visão geral dos aplicativos Web](/azure/app-service-web/app-service-web-overview)
- [Noções básicas do registro de um aplicativo no Azure AD](/azure/active-directory/develop/authentication-scenarios#authentication-basics-in-microsoft-identity-platform)  
- [Registrar o aplicativo com o locatário do Azure Active Directory](/azure/active-directory/active-directory-app-registration)



## <a name="before-you-begin"></a>Antes de começar

Depois de decidir sobre o serviço ao qual você deseja se conectar, consulte a tabela em [Detalhes do serviço](#service-details). Esta tabela fornece as informações necessárias para concluir o Assistente de Serviço do Azure. Converse antecipadamente com o administrador do Azure AD. Decida qual das seguintes ações adotar: 

- Crie manualmente os aplicativos com antecedência no portal do Azure. Em seguida, importe os detalhes do aplicativo no Configuration Manager.  

- Use o Configuration Manager para criar diretamente os aplicativos no Azure AD. Para coletar os dados necessários do Azure AD, examine as informações nas outras seções deste artigo.  

Alguns serviços exigem que os aplicativos do Azure AD tenham permissões específicas. Examine as informações de cada serviço para determinar as permissões necessárias. Por exemplo, antes de importar um aplicativo Web, um administrador do Azure deve primeiro criá-lo no [portal do Azure](https://portal.azure.com). 

Ao configurar Upgrade Readiness ou Conector do Log Analytics, dê ao aplicativo Web recém-registrado a permissão *Colaborador* no grupo de recursos que contém o workspace relevante. Com essa permissão, o Configuration Manager pode acessar esse workspace. Ao atribuir a permissão, procure o nome do registro do aplicativo na área **Adicionar usuários** do portal do Azure. Esse processo é semelhante a quando você [fornece ao Configuration Manager as permissões para o Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics). Um administrador do Azure deve atribuir essas permissões antes que você importe o aplicativo para o Configuration Manager.



## <a name="start-the-azure-services-wizard"></a>Iniciar o assistente dos Serviços do Azure

1.  No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Serviços do Azure**.  

2.  Na guia **Página Inicial** da faixa de opções, no grupo **Serviços do Azure**, selecione **Configurar os Serviços do Azure**.  

3.  Na página **Serviços do Azure** do Assistente de Serviços do Azure:  

    1. Especifique um **Nome** para o objeto no Configuration Manager.  

    2. Especifique uma **Descrição** opcional para ajudá-lo a identificar o serviço.  

    3. Selecione o serviço do Azure que você deseja conectar ao Configuration Manager.  

4. Selecione **Avançar** para continuar para a página [Propriedades do aplicativo do Azure](#azure-app-properties) do Assistente de Serviços do Azure.  



## <a name="azure-app-properties"></a>Propriedades do aplicativo do Azure

Na página **Aplicativo** do Assistente de Serviços do Azure, primeiro selecione o **Ambiente do Azure** na lista. Consulte a tabela em [Detalhes do serviço](#service-details) para saber qual ambiente está disponível no momento para o serviço.

O restante da página Aplicativo varia de acordo com o serviço específico. Consulte a tabela em [Detalhes do serviço](#service-details) para saber qual tipo de aplicativo é usado pelo serviço e qual ação pode ser usada. 

- Se o aplicativo der suporte à importação e criação de ações, selecione **Procurar**. Essa ação abre a [caixa de diálogo Aplicativo para servidores](#server-app-dialog) ou a [caixa de diálogo Aplicativo Cliente](#client-app-dialog).  

- Se o aplicativo der suporte apenas à ação de importação, selecione **Importar**. Essa ação abre a [caixa de diálogo Importar Aplicativos (servidor)](#import-apps-dialog-server) ou a [caixa de diálogo Importar Aplicativos (cliente)](#import-apps-dialog-client).

Depois de especificar os aplicativos nessa página, selecione **Avançar** para continuar para a página [Configuração ou Descoberta](#configuration-or-discovery) do Assistente de Serviços do Azure.

### <a name="web-app"></a>Aplicativo Web

Esse aplicativo é o tipo do Azure AD *aplicativo Web/API*, também chamado de aplicativo para servidores no Configuration Manager.

#### <a name="server-app-dialog"></a>Caixa de diálogo Aplicativo para servidores

Quando você seleciona **Procurar** do **Aplicativo Web** na página Aplicativo do Assistente de Serviços do Azure, ele abre a caixa de diálogo Aplicativo para servidores. Ele exibe uma lista que mostra as seguintes propriedades dos aplicativos Web existentes:
- Nome amigável do locatário
- Nome amigável do aplicativo
- Tipo de serviço

Há três ações que você pode executar na caixa de diálogo Aplicativo para servidores:
- Para reutilizar um aplicativo Web existente, selecione-o na lista. 
- Selecione **Importar** para abrir a caixa de diálogo [Importar aplicativos](#import-apps-dialog-server).
- Selecione **Criar** para abrir a [caixa de diálogo Criar Aplicativo para Servidores](#create-server-application-dialog).

Depois de selecionar, importar ou criar um aplicativo Web, selecione **OK** para fechar a caixa de diálogo Aplicativo para servidores. Essa ação retorna à [página Aplicativo](#azure-app-properties) do Assistente de Serviços do Azure.

#### <a name="import-apps-dialog-server"></a>Caixa de diálogo Importar aplicativos (servidor)

Quando você seleciona **Importar** na caixa de diálogo Aplicativo para servidores ou na página Aplicativo do Assistente de Serviços do Azure, ele abre a caixa de diálogo Importar aplicativos. Essa página permite que você insira informações sobre um aplicativo Web do Azure AD que já foi criado no portal do Azure. Ela importa os metadados sobre esse aplicativo Web para o Configuration Manager. Especifique as seguintes informações:
- **Nome do Locatário do Azure AD**
- **ID de Locatário do Azure AD**
- **Nome do aplicativo**: um nome amigável do aplicativo.
- **ID do Cliente**
- **Chave Secreta**
- **Vencimento da Chave Secreta**: selecione uma data futura no calendário. 
- **URI da ID do aplicativo**: esse valor precisa ser exclusivo no locatário do Azure AD. Ele está localizado no token de acesso usado pelo cliente do Configuration Manager para solicitar o acesso ao serviço. Por padrão, esse valor é https\://ConfigMgrService.  

Depois de inserir as informações, selecione **Verificar**. Em seguida, selecione **OK** para fechar a caixa de diálogo Importar aplicativos. Essa ação retorna à [página Aplicativo](#azure-app-properties) do Assistente de Serviços do Azure ou à [caixa de diálogo Aplicativo para servidores](#server-app-dialog).

#### <a name="create-server-application-dialog"></a>Caixa de diálogo Criar Aplicativo para Servidores

Quando você seleciona **Criar** na caixa de diálogo Aplicativo para servidores, ele abre a caixa de diálogo Criar Aplicativo para Servidores. Essa página automatiza a criação de um aplicativo Web no Azure AD. Especifique as seguintes informações:
- **Nome do aplicativo**: um nome amigável do aplicativo.
- **URL da home page**: esse valor não é usado pelo Configuration Manager, mas é exigido pelo Azure AD. Por padrão, esse valor é https\://ConfigMgrService.  
- **URI da ID do aplicativo**: esse valor precisa ser exclusivo no locatário do Azure AD. Ele está localizado no token de acesso usado pelo cliente do Configuration Manager para solicitar o acesso ao serviço. Por padrão, esse valor é https\://ConfigMgrService.  
- **Período de validade da Chave Secreta**: escolha **1 ano** ou **2 anos** na lista suspensa. Um ano é o valor padrão.

Selecione **Entrar** para se autenticar no Azure como um usuário administrativo. Essas credenciais não são salvas pelo Configuration Manager. Essa persona não exige permissões no Configuration Manager e não precisa ser a mesma conta que executa o Assistente de Serviços do Azure. Após a autenticação bem-sucedida no Azure, a página mostra o **Nome do Locatário do Azure AD** para referência. 

Selecione **OK** para criar o aplicativo Web no Azure AD e feche a caixa de diálogo Criar Aplicativo para Servidores. Essa ação retorna à [caixa de diálogo Aplicativo para servidores](#server-app-dialog).


### <a name="native-client-app"></a>Aplicativo Cliente Nativo
    
Esse aplicativo é o tipo *Nativo* do Azure AD, também chamado de aplicativo cliente no Configuration Manager.

#### <a name="client-app-dialog"></a>Caixa de diálogo Aplicativo Cliente

Quando você seleciona **Procurar** do **Aplicativo Cliente Nativo** na página Aplicativo do Assistente de Serviços do Azure, ele abre a caixa de diálogo Aplicativo Cliente. Ele exibe uma lista que mostra as seguintes propriedades dos aplicativos nativos existentes:
- Nome amigável do locatário
- Nome amigável do aplicativo
- Tipo de serviço

Há três ações que você pode executar na caixa de diálogo Aplicativo Cliente:
- Para reutilizar um aplicativo nativo existente, selecione-o na lista. 
- Selecione **Importar** para abrir a caixa de diálogo [Importar aplicativos](#import-apps-dialog-client).
- Selecione **Criar** para abrir a [caixa de diálogo Criar Aplicativo Cliente](#create-client-application-dialog).

Depois de selecionar, importar ou criar um aplicativo nativo, escolha **OK** para fechar a caixa de diálogo Aplicativo Cliente. Essa ação retorna à [página Aplicativo](#azure-app-properties) do Assistente de Serviços do Azure.

#### <a name="import-apps-dialog-client"></a>Caixa de diálogo Importar aplicativos (cliente)

Quando você seleciona **Importar** na caixa de diálogo Aplicativo Cliente, ele abre a caixa de diálogo Importar aplicativos. Essa página permite que você insira informações sobre um aplicativo nativo do Azure AD que já foi criado no portal do Azure. Ela importa os metadados sobre esse aplicativo nativo para o Configuration Manager. Especifique as seguintes informações:
- **Nome do aplicativo**: um nome amigável do aplicativo.
- **ID do Cliente** 

Depois de inserir as informações, selecione **Verificar**. Em seguida, selecione **OK** para fechar a caixa de diálogo Importar aplicativos. Essa ação retorna à [caixa de diálogo Aplicativo Cliente](#client-app-dialog).

#### <a name="create-client-application-dialog"></a>Caixa de diálogo Criar Aplicativo Cliente

Quando você seleciona **Criar** na caixa de diálogo Aplicativo Cliente, ele abre a caixa de diálogo Criar Aplicativo Cliente. Essa página automatiza a criação de um aplicativo nativo no Azure AD. Especifique as seguintes informações:
- **Nome do aplicativo**: um nome amigável do aplicativo.
- **URL de resposta**: esse valor não é usado pelo Configuration Manager, mas é exigido pelo Azure AD. Por padrão, esse valor é https\://ConfigMgrService. 

Selecione **Entrar** para se autenticar no Azure como um usuário administrativo. Essas credenciais não são salvas pelo Configuration Manager. Essa persona não exige permissões no Configuration Manager e não precisa ser a mesma conta que executa o Assistente de Serviços do Azure. Após a autenticação bem-sucedida no Azure, a página mostra o **Nome do Locatário do Azure AD** para referência. 

Selecione **OK** para criar o aplicativo nativo no Azure AD e feche a caixa de diálogo Criar Aplicativo Cliente. Essa ação retorna à [caixa de diálogo Aplicativo Cliente](#client-app-dialog).


### <a name="renew-secret-key-azure-ad-apps"></a>Renovar a chave secreta dos aplicativos do Azure AD
Antes da versão 1806, para renovar a chave secreta de um aplicativo do Azure, você precisa recriar o aplicativo.

Na versão 1806 e posterior:

- Aplicativo criado: em **Nó de Serviços de Nuvem**, acesse **Locatários do Azure Active Directory**. No painel de detalhes, selecione o locatário no qual o aplicativo foi criado e selecione **Renovar a chave de segredo**.  

    - Selecione **Entrar** para se autenticar no Azure como um usuário administrativo.  

    - Selecione **OK** para criar o aplicativo nativo no Azure AD e feche a caixa de diálogo Criar Aplicativo Cliente. Essa ação retorna à [caixa de diálogo Aplicativo Cliente](#client-app-dialog).  

- Aplicativo importado: use o portal do Azure para renovar e anote a nova chave de segredo e a data de vencimento. Adicione essas informações no assistente **Renovar a Chave de Segredo**.  

> [!Note]  
> Salve a chave secreta antes de fechar a página **Chave** das propriedades do aplicativo do Azure. Essa informação é removida ao fechar a página.


## <a name="configuration-or-discovery"></a>Configuração ou descoberta

Depois de especificar os aplicativos Web e nativos na página Aplicativos, o Assistente de Serviços do Azure continua para a página **Configuração** ou **Descoberta**, dependendo do serviço ao qual você está se conectando. Os detalhes dessa página variam conforme o serviço. Para obter mais informações, consulte um dos seguintes artigos:  

-   Serviço **Gerenciamento de nuvem**, página **Descoberta**: [Configurar a descoberta de usuários do Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

-   Serviço **Conector do Log Analytics**, página **Configuração**: [Configurar a conexão ao Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics#configure-the-connection-to-log-analytics)  

-   Serviço **Conector do Upgrade Readiness**, página **Configuração**: [Usar o Assistente do Azure para criar a conexão](/sccm/core/clients/manage/upgrade/upgrade-analytics#use-the-azure-wizard-to-create-the-connection)  

-   Serviço **Microsoft Store para Empresas**, página **Configurações**: [Configurar a sincronização da Microsoft Store para Empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#bkmk_config)  


Por fim, conclua o Assistente de Serviços do Azure pelas páginas Resumo, Progresso e Conclusão. Você concluiu a configuração de um serviço do Azure no Configuration Manager. Repita esse processo para configurar outros serviços do Azure.


## <a name="view-the-configuration-of-an-azure-service"></a>Exibir a configuração de um serviço do Azure
Exiba as propriedades de um serviço do Azure que você configurou para ser usado. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e selecione **Serviços do Azure**. Selecione o serviço que deseja exibir ou editar e, em seguida, selecione **Propriedades**.

Se você selecionar um serviço e, em seguida, selecionar **Excluir** na faixa de opções, essa ação excluirá a conexão no Configuration Manager. Ela não removerá o aplicativo no Azure AD. Solicite que o administrador do Azure exclua o aplicativo quando ele não for mais necessário. Ou execute o Assistente de Serviço do Azure para importar o aplicativo.<!--483440-->


## <a name="cloud-management-data-flow"></a>Fluxo de dados do gerenciamento de nuvem

O diagrama a seguir é um fluxo de dados conceitual para a interação entre o Configuration Manager, o Azure AD e os serviços de nuvem conectados. Esse exemplo específico usa o serviço **Gerenciamento de Nuvem**, que inclui um cliente Windows 10 e aplicativos cliente e para servidores. Os fluxos para outros serviços são semelhantes.

![Diagrama de fluxo de dados do Configuration Manager com o Azure AD e o Gerenciamento de Nuvem](media/aad-auth.png)

1.  O administrador do Configuration Manager importa ou cria os aplicativos cliente e para servidores no Azure AD.  

2.  O método de descoberta de usuários do Azure AD do Configuration Manager é executado. O site usa o token de aplicativo para servidores do Azure AD para consultar o Microsoft Graph em busca de objetos de usuário.  

3.  O site armazena dados sobre os objetos de usuário. Para obter mais informações, consulte [Descoberta de usuários do Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).  

4.  O cliente do Configuration Manager solicita o token de usuário do Azure AD. O cliente faz a declaração usando a ID do aplicativo cliente do Azure AD e o aplicativo para servidores como o público-alvo. Para obter mais informações, consulte [Declarações em tokens de segurança do Azure AD](/azure/active-directory/develop/authentication-scenarios#claims-in-microsoft-identity-platform-security-tokens).  

5.  O cliente se autentica no site apresentando o token do Azure AD ao gateway de gerenciamento de nuvem e/ou ao ponto de gerenciamento habilitado para HTTPS local.  


