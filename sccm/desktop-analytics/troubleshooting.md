---
title: Solucionar problemas de análise da área de trabalho
titleSuffix: Configuration Manager
description: Detalhes técnicos para ajudá-lo a solucionar problemas com a análise de área de trabalho.
ms.date: 06/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 271803e42ba20d8d0340754b3167210414423014
ms.sourcegitcommit: d8cfd0edf2579e2b08a0ca8a0a7b8f53d1e4196f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67463803"
---
# <a name="troubleshoot-desktop-analytics"></a>Solucionar problemas de análise da área de trabalho

Use os detalhes neste artigo para ajudá-lo a solucionar problemas com a análise de área de trabalho integrado ao Configuration Manager.



## <a name="confirm-prerequisites"></a>Confirmar pré-requisitos

Muitos problemas comuns são causados por pré-requisitos ausentes. Primeiro, confirme as configurações a seguir:

- [Pré-requisitos](/sccm/desktop-analytics/overview#prerequisites)  

- [Atualizações de componentes do Windows](/sccm/desktop-analytics/enroll-devices#update-devices)  

- [Como habilitar o compartilhamento de dados](/sccm/desktop-analytics/enable-data-sharing), que abrange os seguintes tópicos:  

    - Pontos de extremidade de Internet para o qual os clientes precisam para se conectar  

    - Autenticação do servidor proxy  

    - Níveis de dados de diagnóstico  



## <a name="monitor-connection-health"></a>Monitorar a integridade da conexão

Use o **integridade de Conexão** painel no Configuration Manager para fazer uma busca detalhada em categorias por integridade do dispositivo. No console do Configuration Manager, vá para o **biblioteca de Software** espaço de trabalho, expanda o **área de trabalho de análise de manutenção** nó e selecione o **integridade de Conexão** Painel de controle.  

Para obter mais informações, consulte [monitorar a integridade de conexão](/sccm/desktop-analytics/monitor-connection-health).


## <a name="log-files"></a>Arquivos de log

Para obter mais informações, consulte [arquivos de Log para análise de área de trabalho](/sccm/core/plan-design/hierarchy/log-files#desktop-analytics)

### <a name="enable-verbose-logging"></a>Habilitar o log detalhado

1. No ponto de conexão de serviço, vá para a seguinte chave do registro: `HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Defina as **LoggingLevel** valor `0`  
3. (Opcional) Execute o seguinte comando SQL no banco de dados do site:  

    ```SQL
    DELETE FROM M365AProperties WHERE Name = 'M365ATenantUpdateInfo_LastUpdateTime'
    ```

4. Reinicie o **SMS_EXECUTIVE** serviço no servidor do site



## <a name="bkmk_AzureADApps"></a> Aplicativos do Azure AD

Análise da área de trabalho adiciona os seguintes aplicativos ao AD do Azure:

- **Gerenciador de configuração de Microsserviço**: Conecta o Configuration Manager com a análise da área de trabalho. Este aplicativo não tem nenhum requisito de acesso.  

- **MALogAnalyticsReader**: Recupera grupos do OMS e os dispositivos criados no Log Analytics. Para obter mais informações, consulte [função de aplicativo MALogAnalyticsReader](#bkmk_MALogAnalyticsReader).  

Se você precisar provisionar esses aplicativos após concluir a instalação, vá para o **aos serviços conectados** painel. Selecione **configurar o acesso de usuários e aplicativos**e provisionar os aplicativos.  

- **Aplicativo do Azure AD para o Configuration Manager**. Se você precisar provisionar ou solucionar problemas de conexão após concluir a instalação, consulte [importação e criar aplicativos para o Configuration Manager](#create-and-import-app-for-configuration-manager). Este aplicativo requer **gravar dados de coleção do CM** e **ler dados de coleção do CM** no **Configuration Manager Service** API.  


### <a name="create-and-import-app-for-configuration-manager"></a>Criar e importar um aplicativo para o Configuration Manager

Depois de concluir a [inicial integração](/sccm/desktop-analytics/set-up#initial-onboarding) no portal de análise de área de trabalho, use as seguintes etapas para criar e importar o aplicativo para o Configuration Manager se você não pode criar esse aplicativo do Azure AD a configurar serviços do Azure manualmente Assistente.

#### <a name="create-app-in-azure-ad"></a>Criar um aplicativo no Azure AD

1. Abra o [portal do Azure](http://portal.azure.com) como um usuário com *Administrador Global* permissões, vá para **Azure Active Directory**e selecione **registros do aplicativo**. Em seguida, selecione **novo registro**.  

2. No **criar** painel, defina as seguintes configurações:  

    - **Nome**: um nome exclusivo que identifica o aplicativo, por exemplo: `Desktop-Analytics-Connection`  

    - **Suporte para tipos de conta**: **Contas na organização somente o diretório (Contoso)**

    - **(Opcional) do URI de redirecionamento**: **Web**  

    <!--     - **Sign-on URL**: this value isn't used by Configuration Manager, but required by Azure AD. Enter a unique and valid URL, for example: `https://configmgrapp`   -->
  
    Selecione **registrar**.  

3. Selecione o aplicativo, observe o **ID do aplicativo (cliente)** e **ID de diretório (Locatário)** . Os valores são GUIDs são usados para configurar a conexão do Configuration Manager.  

4. No **Manage** menu, selecione **certificados e segredos**. Selecione **novo segredo do cliente**. Insira um **descrição**, especifique uma duração de expiração e, em seguida, selecione **Add**. Cópia de **valor** da chave, que é usado para configurar a conexão do Configuration Manager.

    > [!Important]  
    > Isso é a única oportunidade para copiar o valor da chave. Se você não copiá-lo agora, você precisará criar outra chave.  
    >
    > Salve o valor da chave em um local seguro.  

5. No **Manage** menu, selecione **permissões de API**.  

    1. Sobre o **permissões de API** painel, selecione **adicionar uma permissão**.  

    2. No **permissões de API de solicitação** do painel, alterne para o **APIs minha organização usa**.  

    3. Pesquise e selecione o **Configuration Manager Microservice** API.  

    4. Selecione o **permissões de aplicativo** grupo. Expandir **CmCollectionData**e selecione as seguintes permissões: **Gravar dados de coleção de CM** e **ler dados de coleção de CM**.  

    5. Selecione **adicionar permissões**.  

6. Sobre o **permissões de API** painel, selecione **conceder consentimento do administrador...** . Selecione **Sim**.  


#### <a name="import-app-in-configuration-manager"></a>Importação de aplicativo no Configuration Manager

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Serviços do Azure**. Selecione **configurar serviços do Azure** na faixa de opções.  

2. Sobre o **serviços do Azure** página do Assistente de serviços do Azure, defina as seguintes configurações:  

    - Especifique um **Nome** para o objeto no Configuration Manager.  

    - Especifique uma **Descrição** opcional para ajudá-lo a identificar o serviço.  

    - Selecione **análise de área de trabalho** na lista de serviços disponíveis.  
  
   Selecione **Avançar**.  

3. Sobre o **aplicativo** , selecione apropriado **ambiente do Azure**. Em seguida, selecione **importação** para o aplicativo web. Defina as seguintes configurações na **importar aplicativos** janela:  

    - **Nome do locatário do Azure AD**: Esse nome é como ele é chamado no Configuration Manager  

    - **ID de locatário do Azure AD**: O **ID de diretório** você copiou do Azure AD  

    - **ID do cliente**: O **ID do aplicativo** você copiou do aplicativo Azure AD  

    - **Chave secreta**: A tecla **valor** você copiou do aplicativo Azure AD  

    - **Vencimento da Chave Secreta**: A mesma data de expiração da chave  

    - **URI da ID do aplicativo**: Essa configuração deve preencher automaticamente com o seguinte valor: `https://cmmicrosvc.manage.microsoft.com/`  
  
   Selecione **Verify**e, em seguida, selecione **Okey** para fechar a janela Importar aplicativos. Selecione **próxima** na página do aplicativo do Assistente de serviços do Azure.  

Para continuar o restante do assistente no **dados de diagnóstico** página, consulte [conectar ao serviço](/sccm/desktop-analytics/connect-configmgr#bkmk_connect).

#### <a name="troubleshoot-app-in-configuration-manager"></a>Solucionar problemas de aplicativo no Configuration Manager

Se você está tendo problemas ao criar ou importar o aplicativo, a primeira verificação **Smsadminui** do erro específico. Em seguida, verifique as seguintes configurações:

- Você registrou com êxito o locatário para o serviço de análise de área de trabalho. Para obter mais informações, consulte [como configurar a análise de área de trabalho](/sccm/desktop-analytics/set-up).

- Todos os necessários pontos de extremidade estão acessíveis. Para obter mais informações, consulte [pontos de extremidade](/sccm/desktop-analytics/enable-data-sharing#endpoints).

- Verifique se o usuário que fizer logon tem as permissões corretas. Para obter mais informações, veja [Pré-requisitos](/sccm/desktop-analytics/overview#prerequisites).

- Certifique-se de que o usuário pode entrar no Azure em geral. Essa ação determina se há qualquer geral do Azure AD problemas de autenticação.

- Verificar mensagens de status para o **SMS_SERVICE_CONNECTOR** componente sobre os *trabalho de análise de área de trabalho*.


### <a name="bkmk_MALogAnalyticsReader"></a> Função de aplicativo MALogAnalyticsReader

Quando você configurar a análise de área de trabalho, você consente em nome de sua organização. Esse consentimento é atribuir o aplicativo MALogAnalyticsReader a função de leitor do Log Analytics para o espaço de trabalho. Essa função de aplicativo é necessária pela análise de área de trabalho.

Se houver um problema com esse processo durante a instalação, use o seguinte processo para adicionar manualmente essa permissão:

1. Vá para o [portal do Azure](http://portal.azure.com)e selecione **todos os recursos**. Selecione o espaço de trabalho do tipo **do Log Analytics**.  

2. No menu do espaço de trabalho, selecione **controle de acesso (IAM)** , em seguida, selecione **Add**.  

3. No **adicionar permissões** painel, defina as seguintes configurações:  

    - **Função**: **Reader**  

    - **Atribuir acesso a**: **Usuário, grupo ou aplicativo do Azure AD**  

    - **Selecione**: **MALogAnalyticsReader**  

4. Selecione **Salvar**.

O portal mostrará uma notificação de que ele adicionou a atribuição de função.


## <a name="data-latency"></a>Latência de dados

<!-- 3846531 -->
Ao configurar a análise de área de trabalho pela primeira vez, os relatórios no Configuration Manager e o portal de análise de área de trabalho não podem mostrar dados completo imediatamente. Pode levar 2 a 3 dias para as etapas a seguir ocorra:

- Dispositivos ativos enviam dados de diagnóstico para o serviço de análise de área de trabalho
- O serviço processa os dados
- O serviço sincroniza com o site do Configuration Manager

Ao sincronizar coleções de dispositivos da sua hierarquia do Configuration Manager para análise de área de trabalho, ele pode levar até 10 minutos para as coleções sejam exibidos no portal de análise de área de trabalho. Da mesma forma, quando você cria um plano de implantação na área de trabalho de análise, ele pode levar até 10 minutos para as novas coleções associadas com o plano de implantação para aparecer na sua hierarquia do Configuration Manager. Os sites primários criarem as coleções, e o site de administração central sincroniza com análise de área de trabalho.

No portal de análise de área de trabalho, há dois tipos de dados: **Os dados do administrador** e **dados de diagnóstico**:

- **Os dados do administrador** refere-se a quaisquer alterações feitas à configuração do espaço de trabalho. Por exemplo, quando você altera um ativo **decisão de atualização** ou **importância** você está alterando os dados do administrador. Geralmente, essas alterações têm um efeito de composição, como eles podem alterar o estado de preparação de um dispositivo com o ativo em questão instalado.

- **Dados de diagnóstico** refere-se aos metadados do sistema carregados dos dispositivos cliente para a Microsoft. Esses dados impulsiona a análise de área de trabalho. Ele inclui atributos como inventário de dispositivo e status de atualização de segurança e o recurso.

Por padrão, todos os dados na análise de área de trabalho portal é automaticamente atualizado diariamente. Esta atualização inclui alterações em dados de diagnóstico e de quaisquer alterações feitas na configuração (dados do administrador). Ele deve estar visível em seu portal de análise de área de trabalho por 08:00 AM UTC diariamente.

Quando você faz alterações em dados do administrador, você pode disparar uma atualização sob demanda dos dados de administrador no seu espaço de trabalho. Em qualquer página no portal de análise de área de trabalho, abra o submenu de moeda de dados:

![Captura de tela da guia de submenu de moeda de dados no portal de análise de área de trabalho](media/data-currency-flyout.png)

Em seguida, selecione **aplicar alterações**:

![Captura de tela do menu suspenso de moeda de dados expandidos no portal de análise de área de trabalho](media/data-currency-flyout-expand.png)

Esse processo geralmente leva entre 15 a 60 minutos. O tempo depende do tamanho do seu espaço de trabalho e o escopo das alterações que precisam de processos. Quando você solicitar uma atualização de dados sob demanda, não resulta em todas as alterações aos dados de diagnóstico.  Para obter mais informações, consulte o [perguntas frequentes sobre análise de área de trabalho](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

Se você não estiver vendo as alterações atualizadas dentro dos intervalos indicados acima, aguarde 24 horas para a próxima atualização diária. Se você vir a intervalos mais longos, verifique o painel de integridade do serviço. Se o serviço de relatórios como íntegros, entre em contato com o suporte da Microsoft.<!-- 3896921 -->
