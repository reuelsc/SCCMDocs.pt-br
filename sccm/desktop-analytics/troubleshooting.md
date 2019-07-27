---
title: Solucionar problemas do desktop Analytics
titleSuffix: Configuration Manager
description: Detalhes técnicos para ajudá-lo a solucionar problemas com a análise de desktops.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f9e13911ef7337ca4f1f9fb2291aa026c90cfee8
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68536025"
---
# <a name="troubleshoot-desktop-analytics"></a>Solucionar problemas do desktop Analytics

Use os detalhes neste artigo para ajudá-lo a solucionar problemas com a análise de desktop integrada com o Configuration Manager.



## <a name="confirm-prerequisites"></a>Confirmar pré-requisitos

Muitos problemas comuns são causados por pré-requisitos ausentes. Primeiro, confirme as seguintes configurações:

- [Pré-requisitos](/sccm/desktop-analytics/overview#prerequisites)  

- [Atualizações de componentes do Windows](/sccm/desktop-analytics/enroll-devices#update-devices)  

- [Como habilitar o compartilhamento de dados](/sccm/desktop-analytics/enable-data-sharing), que abrange os seguintes tópicos:  

    - Pontos de extremidade de Internet aos quais os clientes precisam se conectar  

    - Autenticação do servidor proxy  

    - Níveis de dados de diagnóstico  



## <a name="monitor-connection-health"></a>Monitorar a integridade da conexão

Use o painel de **integridade da conexão** no Configuration Manager para analisar categorias por integridade do dispositivo. No console do Configuration Manager, vá para o espaço de trabalho **biblioteca de software** , expanda o nó **manutenção do desktop Analytics** e selecione o painel de **integridade da conexão** .  

Para obter mais informações, consulte [monitorar a integridade da conexão](/sccm/desktop-analytics/monitor-connection-health).


## <a name="log-files"></a>Arquivos de log

Para obter mais informações, consulte [arquivos de log para análise de desktop](/sccm/core/plan-design/hierarchy/log-files#desktop-analytics)

A partir do Configuration Manager versão 1906, use a ferramenta **DesktopAnalyticsLogsCollector. ps1** do diretório de instalação do Configuration Manager para ajudar a solucionar problemas do desktop Analytics. Ele executa algumas etapas básicas de solução de problemas e coleta os logs relevantes em um único diretório de trabalho. Para obter mais informações, consulte [coletor de logs](/sccm/desktop-analytics/log-collector).

### <a name="enable-verbose-logging"></a>Habilitar o log detalhado

1. No ponto de conexão de serviço, vá para a seguinte chave do registro:`HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Defina o valor **LoggingLevel** como`0`  


## <a name="bkmk_AzureADApps"></a>Aplicativos do Azure AD

O desktop Analytics adiciona os seguintes aplicativos ao Azure AD:

- **Configuration Manager Microservice**: Conecta Configuration Manager com análise de desktop. Este aplicativo não tem requisitos de acesso.  

- **MALogAnalyticsReader**: Recupera os grupos e dispositivos do OMS criados no Log Analytics. Para obter mais informações, consulte [função de aplicativo MALogAnalyticsReader](#bkmk_MALogAnalyticsReader).  

Se você precisar provisionar esses aplicativos depois de concluir a instalação, vá para o painel **Serviços conectados** . Selecione **Configurar usuários e aplicativos acesso**e provisionar os aplicativos.  

- **Aplicativo do Azure ad para Configuration Manager**. Se você precisar provisionar ou solucionar problemas de conexão depois de concluir a instalação, consulte [criar e importar aplicativo para Configuration Manager](#create-and-import-app-for-configuration-manager). Este aplicativo requer **dados de coleção cm de gravação** e **leitura dos dados da coleção cm** na API do **serviço de Configuration Manager** .  


### <a name="create-and-import-app-for-configuration-manager"></a>Criar e importar aplicativo para Configuration Manager

Se você não puder criar o aplicativo do Azure AD para Configuration Manager no Assistente para configurar serviços do Azure ou se quiser reutilizar um aplicativo existente, será necessário criá-lo e importá-lo manualmente. Depois de concluir a [integração inicial](/sccm/desktop-analytics/set-up#initial-onboarding) no portal do desktop Analytics, use as seguintes etapas:

#### <a name="create-app-in-azure-ad"></a>Criar aplicativo no Azure AD

1. Abra o [portal do Azure](http://portal.azure.com) como um usuário com permissões de *administrador global* , vá para **Azure Active Directory**e selecione **registros de aplicativo**. Em seguida, selecione **novo registro**.  

2. No painel **criar** , defina as seguintes configurações:  

    - **Nome**: um nome exclusivo que identifica o aplicativo, por exemplo:`Desktop-Analytics-Connection`  

    - **Tipos de conta com suporte**: **Contas somente neste diretório organizacional (contoso)**

    - **URI de redirecionamento (opcional)** : **Web**  

    <!--     - **Sign-on URL**: this value isn't used by Configuration Manager, but required by Azure AD. Enter a unique and valid URL, for example: `https://configmgrapp`   -->
  
    Selecione **registrar**.  

3. Selecione o aplicativo, observe a **ID do aplicativo (cliente)** e a **ID do diretório (locatário)** . Os valores são GUIDs que são usados para configurar a conexão de Configuration Manager.  

4. No menu **gerenciar** , selecione **certificados & segredos**. Selecione **novo segredo do cliente**. Insira uma **Descrição**, especifique uma duração de expiração e, em seguida, selecione **Adicionar**. Copie o **valor** da chave, que é usado para configurar a conexão de Configuration Manager.

    > [!Important]  
    > Essa é a única oportunidade para copiar o valor da chave. Se você não copiá-lo agora, precisará criar outra chave.  
    >
    > Salve o valor da chave em um local seguro.  

5. No menu **gerenciar** , selecione **permissões de API**.  

    1. No painel **permissões de API** , selecione **Adicionar uma permissão**.  

    2. No painel **solicitar permissões de API** , alterne para **APIs que minha organização usa**.  

    3. Pesquise e selecione a API de **microserviço Configuration Manager** .  

    4. Selecione o grupo de **permissões de aplicativo** . Expanda **CmCollectionData**e selecione as duas permissões a seguir: **Gravar dados de coleta cm** e **ler dados da coleção cm**.  

    5. Selecione **adicionar permissões**.  

6. No painel **permissões de API** , selecione **conceder consentimento de administrador...** . Selecione **Sim**.  


#### <a name="import-app-in-configuration-manager"></a>Importar aplicativo no Configuration Manager

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Serviços do Azure**. Selecione **Configurar serviços do Azure** na faixa de opções.  

2. Na página **Serviços do Azure** do assistente de serviços do Azure, defina as seguintes configurações:  

    - Especifique um **Nome** para o objeto no Configuration Manager.  

    - Especifique uma **Descrição** opcional para ajudá-lo a identificar o serviço.  

    - Selecione **análise de desktop** na lista de serviços disponíveis.  
  
   Selecione **Avançar**.  

3. Na página do **aplicativo** , selecione o **ambiente do Azure**apropriado. Em seguida, selecione **importar** para o aplicativo Web. Defina as seguintes configurações na janela **importar aplicativos** :  

    - **Nome do locatário do Azure ad**: Esse nome é como ele é nomeado em Configuration Manager  

    - **ID do locatário do Azure ad**: A **ID de diretório** que você copiou do Azure AD  

    - **ID do cliente**: A **ID do aplicativo** que você copiou do aplicativo do Azure AD  

    - **Chave secreta**: O **valor** de chave que você copiou do aplicativo do Azure AD  

    - **Vencimento da Chave Secreta**: A mesma data de expiração da chave  

    - **URI da ID do aplicativo**: Essa configuração deve ser preenchida automaticamente com o seguinte valor:`https://cmmicrosvc.manage.microsoft.com/`  
  
   Selecione **verificar**e, em seguida, selecione **OK** para fechar a janela importar aplicativos. Selecione **Avançar** na página aplicativo do assistente de serviços do Azure.  

Para continuar o restante do assistente na página de **dados de diagnóstico** , consulte [conectar-se ao serviço](/sccm/desktop-analytics/connect-configmgr#bkmk_connect).

#### <a name="troubleshoot-app-in-configuration-manager"></a>Solucionar problemas de aplicativo no Configuration Manager

Se você estiver tendo problemas ao criar ou importar o aplicativo, primeiro verifique **SMSAdminUI. log** para obter o erro específico. Em seguida, verifique as seguintes configurações:

- Você registrou o locatário com êxito no serviço de análise de desktop. Para obter mais informações, consulte [como configurar o desktop Analytics](/sccm/desktop-analytics/set-up).

- Todos os pontos de extremidade necessários estão acessíveis. Para obter mais informações, consulte [pontos de extremidade](/sccm/desktop-analytics/enable-data-sharing#endpoints).

- Verifique se o usuário que se conecta tem as permissões corretas. Para obter mais informações, veja [Pré-requisitos](/sccm/desktop-analytics/overview#prerequisites).

- Verifique se o usuário pode entrar no Azure em geral. Essa ação determina se há algum problema geral de autenticação do Azure AD.

- Verifique as mensagens de status do componente **SMS_SERVICE_CONNECTOR** em relação ao *trabalho do desktop Analytics*.


### <a name="bkmk_MALogAnalyticsReader"></a>Função de aplicativo MALogAnalyticsReader

Ao configurar o desktop Analytics, você concorda em nome da sua organização. Esse consentimento é atribuir ao aplicativo MALogAnalyticsReader a função leitor de Log Analytics para o espaço de trabalho. Essa função de aplicativo é necessária para o desktop Analytics.

Se houver um problema com esse processo durante a instalação, use o seguinte processo para adicionar manualmente essa permissão:

1. Vá para a [portal do Azure](http://portal.azure.com)e selecione **todos os recursos**. Selecione o espaço de trabalho do tipo **log Analytics**.  

2. No menu do espaço de trabalho, selecione **controle de acesso (iam)** e, em seguida, selecione **Adicionar**.  

3. No painel **adicionar permissões** , defina as seguintes configurações:  

    - **Função**: **Leitora**  

    - **Atribuir acesso a**: **Usuário, grupo ou aplicativo do Azure AD**  

    - **Selecione**: **MALogAnalyticsReader**  

4. Selecione **Salvar**.

O portal mostra uma notificação de que adicionou a atribuição de função.


## <a name="data-latency"></a>Latência de dados

<!-- 3846531 -->
Quando você configura pela primeira vez a análise de desktops, os relatórios no Configuration Manager e no portal do desktop Analytics podem não mostrar dados completos imediatamente. Pode levar de 2-3 a alguns dias para que as seguintes etapas ocorram:

- Os dispositivos ativos enviam dados de diagnóstico para o serviço de análise de desktop
- O serviço processa os dados
- O serviço é sincronizado com seu site Configuration Manager

Ao sincronizar coleções de dispositivos de sua hierarquia de Configuration Manager com o desktop Analytics, pode levar até 10 minutos para que essas coleções apareçam no portal de análise de desktop. Da mesma forma, quando você cria um plano de implantação no desktop Analytics, pode levar até 10 minutos para que as novas coleções associadas ao plano de implantação apareçam em sua hierarquia de Configuration Manager. Os sites primários criam as coleções e o site de administração central sincroniza com o desktop Analytics.

No portal do desktop Analytics, há dois tipos de dados: **Dados do administrador** e **dados de diagnóstico**:

- Os **dados do administrador** referem-se a quaisquer alterações feitas na configuração do seu espaço de trabalho. Por exemplo, quando você altera a decisão ou a **importância** de **atualização** de um ativo, você está alterando os dados do administrador. Essas alterações geralmente têm um efeito de composição, pois podem alterar o estado de preparação de um dispositivo com o ativo em questão instalada.

- **Dados de diagnóstico** referem-se aos metadados do sistema carregados de dispositivos cliente para a Microsoft. Esses dados impulsionam a análise de desktops. Ele inclui atributos como inventário de dispositivos e status de atualização de recursos e segurança.

Por padrão, todos os dados no portal do desktop Analytics são automaticamente atualizados diariamente. Essa atualização inclui alterações nos dados de diagnóstico e quaisquer alterações feitas na configuração (dados do administrador). Ele deve estar visível no portal de análise de desktop pelo 08:00 AM UTC a cada dia.

Ao fazer alterações nos dados do administrador, você pode disparar uma atualização sob demanda dos dados do administrador em seu espaço de trabalho. Em qualquer página no portal do desktop Analytics, abra o submenu de moeda de dados:

![Captura de tela da guia submenu de moeda de dados no portal de análise de desktop](media/data-currency-flyout.png)

Em seguida, selecione **aplicar alterações**:

![Captura de tela do submenu de moeda de dados expandido no portal de análise de desktop](media/data-currency-flyout-expand.png)

Esse processo geralmente leva entre 15-60 minutos. O tempo depende do tamanho do espaço de trabalho e do escopo das alterações que precisam de processos. Quando você solicita uma atualização de dados sob demanda, isso não resulta em nenhuma alteração nos dados de diagnóstico.  Para obter mais informações, consulte as [perguntas frequentes sobre o desktop Analytics](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

Se você não estiver vendo as alterações atualizadas nos quadros de tempo indicados acima, aguarde mais 24 horas para a próxima atualização diária. Se você vir atrasos maiores, verifique o painel de integridade do serviço. Se o serviço relatar como íntegro, entre em contato com o suporte da Microsoft.<!-- 3896921 -->
