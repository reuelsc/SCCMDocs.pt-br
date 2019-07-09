---
title: Tutorial – implantar o Windows 10
titleSuffix: Configuration Manager
description: Um tutorial sobre como usar a área de trabalho de análise e o Configuration Manager para implantar o Windows 10 em um grupo piloto.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: tutorial
ms.assetid: 3e82cd96-0ce0-474a-a597-d65fceadc95a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d564a5161011a1af0a4ec70f9bf7b45d87dd9dcb
ms.sourcegitcommit: 20bbb870baf624c7809d3972f2d09a8d2df79cda
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/08/2019
ms.locfileid: "67623167"
---
# <a name="tutorial-deploy-windows-10-to-pilot"></a>Tutorial: Implantar o Windows 10 para piloto

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Este tutorial usa a análise de área de trabalho e o Configuration Manager para implantar o Windows 10 em um grupo piloto. Ele destaca a integração do serviço de nuvem para fornecer ideias para implantar o Windows com o produto no local. Use análise de área de trabalho para determinar os melhores dispositivos para colocar em um grupo piloto. Em seguida, use o Configuration Manager para obter atual com o Windows.

Neste tutorial, você aprenderá como:  

> [!div class="checklist"]  
> * Configurar análise de área de trabalho no portal do Azure  
> * Conectar o Configuration Manager e definir configurações de dispositivo  
> * Criar um plano de implantação de área de trabalho de análise para Windows 10  
> * Use o Configuration Manager para implantar o Windows 10 para o grupo piloto  

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free) antes de começar. Quando configurado corretamente, o uso da área de trabalho de análise não incorre em custos do Azure.

A análise da área de trabalho usa um *espaço de trabalho do Log Analytics* na sua assinatura do Azure. Um espaço de trabalho é essencialmente um contêiner que inclui informações de conta e informações de configuração simples para a conta. Para obter mais informações, consulte [gerenciar espaços de trabalho](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json).



## <a name="prerequisites"></a>Pré-requisitos

Antes de iniciar este tutorial, certifique-se de que ter os seguintes pré-requisitos:  

- Uma assinatura do Azure Active Directory, com [ **Administrador Global** ](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator) permissões  

    Para obter mais informações, consulte [pré-requisitos de análise de área de trabalho](/sccm/desktop-analytics/overview#prerequisites).

- O Configuration Manager, versão 1902 com pacote cumulativo de atualizações (4500571) ou posterior, com **administrador completo** função  

- Mídia de instalação para a versão mais recente do Windows 10

- Pelo menos um dispositivo Windows 10 com as seguintes configurações:  

    - Windows 10, versão 1709 ou posterior, mas menor do que a versão da mídia de instalação que você planeja usar

    - A atualização de qualidade cumulativa mais recente do Windows 10  

    - 1902 de versão do cliente do Configuration Manager com pacote cumulativo de atualizações (4500571) ou posterior  

- Aprovação de negócios para configurar o nível de dados de diagnóstico do Windows para **avançado (limitado)** nos dispositivos piloto  

    Para obter mais informações, consulte [privacidade de área de trabalho de análise](/sccm/desktop-analytics/privacy).

- Conectividade de rede do dispositivo para os seguintes pontos de extremidade de internet:

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://graph.windows.net` (na função servidor do Configuration Manager somente)
    - `https://fef.msua06.manage.microsoft.com` (na função servidor do Configuration Manager somente)

    Para obter mais informações, consulte [como habilitar o compartilhamento de área de trabalho de análise de dados](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

> [!Important]  
> Estes pré-requisitos são para os fins deste tutorial. Para obter mais informações sobre os pré-requisitos gerais para análise de área de trabalho com o Configuration Manager, consulte [pré-requisitos](/sccm/desktop-analytics/overview#prerequisites).  



## <a name="set-up-desktop-analytics"></a>Configurar Análise de Área de Trabalho

Use este procedimento para entrar no Analytics de área de trabalho e configurá-lo em sua assinatura. Esse procedimento é um processo único para configurar a análise de área de trabalho para sua organização.  

1. Abra o [portal de análise de área de trabalho](https://aka.ms/desktopanalytics) no gerenciamento de dispositivo do Microsoft 365 como um usuário com **Administrador Global** permissões. Selecione **iniciar**.  Se você for solicitado um código de convite, use: `DesktopAnalyticsRocks!`

2. Sobre o **aceite o contrato de serviço** página, examine o contrato de serviço e selecione **Accept**.  

3. Sobre o **confirmar sua assinatura** página, a lista de licenças qualificadas necessárias são para recursos de integridade de dispositivo do Windows da área de trabalho de análise. Selecione **Avançar** para continuar.  

4. Sobre o **dar aos usuários acesso** página:

    - **Permitir a análise de área de trabalho para gerenciar funções de diretório em seu nome**: Análise da área de trabalho atribui automaticamente o **proprietários do espaço de trabalho** as **administrador de análise de área de trabalho** função. Se esses grupos já estão uma **Administrador Global**, não há nenhuma alteração.  

        Se você não selecionar essa opção, análise de área de trabalho ainda adiciona usuários como membros do grupo de segurança. Um **Administrador Global** precisa atribuir manualmente as **administrador de análise de área de trabalho** função para os usuários.  

        Para obter mais informações sobre como atribuir permissões de função de administrador no Azure Active Directory e as permissões atribuídas às **os administradores de análise de área de trabalho**, consulte [permissões da função de administrador no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Análise da área de trabalho pré-configura a **proprietários do espaço de trabalho** grupo de segurança no Azure Active Directory para criar e gerenciar espaços de trabalho e planos de implantação. 

        Para adicionar um usuário ao grupo, digite seu nome ou endereço de email na **insira o nome ou endereço de email** seção. Quando terminar, selecione **próxima**.

5. Na página para **definir seu espaço de trabalho**:  

    > [!Note]  
    > Para concluir esta etapa, o usuário precisa **proprietário do espaço de trabalho** permissões e acesso adicional para a assinatura do Azure e o grupo de recursos. Para obter mais informações, consulte [pré-requisitos](/sccm/desktop-analytics/overview#prerequisites).  

    - Selecione sua assinatura do Azure.  

    - Para usar um espaço de trabalho para análise de área de trabalho, selecione-o e continue com a próxima etapa.  

    - Para criar um espaço de trabalho para análise de área de trabalho, selecione **adicionar espaço de trabalho**.  

        1. Insira um **nome do espaço de trabalho**.  

        2. Selecione a lista suspensa para **selecione o nome de assinatura do Azure para este espaço de trabalho**e escolha a assinatura do Azure para este espaço de trabalho.  

        3. **Criar um novo** grupo de recursos ou **usar existente**.  

        4. Selecione o **região** na lista e, em seguida, selecione **Add**.  

6. Selecione um espaço de trabalho novo ou existente e, em seguida, selecione **definido como espaço de trabalho de análise de área de trabalho**.  Em seguida, selecione **Continue** na **confirmar e conceder acesso** caixa de diálogo.  

7. Na nova guia do navegador, escolha uma conta para usar para entrar. Selecione a opção para **consentir em nome de sua organização** e selecione **Accept**.  


    > [!Note]  
    > Esse consentimento é atribuir o aplicativo MALogAnalyticsReader a função de leitor do Log Analytics para o espaço de trabalho. Essa função de aplicativo é necessária pela análise de área de trabalho. Para obter mais informações, consulte [função de aplicativo MALogAnalyticsReader](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader).  

8. Volta na página para **definir seu espaço de trabalho**, selecione **próxima**.  

9. Sobre o **última etapa** página, selecione **vá para a área de trabalho de análise**. O portal do Azure mostra a área de trabalho de analítica **Home** página.  



## <a name="connect-configuration-manager"></a>Conectar o Configuration Manager

Use este procedimento para atualizar do Configuration Manager, conecte-se à área de trabalho de análise e definir as configurações do dispositivo. Esse procedimento é um processo único para anexar a sua hierarquia para o serviço de nuvem.  

### <a name="update-configuration-manager"></a>Atualizar do Configuration Manager

Instale o pacote de cumulativo de atualizações do Configuration Manager versão 1902 (4500571) para dar suporte à integração com a área de trabalho de análise. Para obter mais informações sobre esta atualização, consulte [atualização cumulativa para o branch atual do Configuration Manager, versão 1902](https://support.microsoft.com/help/4500571).

1. Atualize o site com o pacote cumulativo de atualizações para a versão 1902. Para obter mais informações, confira [Instalar atualizações no console](/sccm/core/servers/manage/install-in-console-updates).  

2. Atualize clientes. Para simplificar este processo, considere o uso da atualização automática do cliente. Para obter mais informações, consulte [Atualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  


### <a name="connect-to-the-service"></a>Conectar-se ao serviço

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Serviços do Azure**. Selecione **configurar serviços do Azure** na faixa de opções.  

2. Sobre o **serviços do Azure** página do Assistente de serviços do Azure, defina as seguintes configurações:  

    - Especifique um **nome** para o objeto no Configuration Manager  

    - Especifique um opcional **descrição** para ajudá-lo a identificar o serviço  

    - Selecione **análise de área de trabalho** na lista de serviços disponíveis  
  
   Selecione **Avançar**.  

3. Sobre o **aplicativo** , selecione apropriado **ambiente do Azure**. Em seguida, selecione **procurar** para o aplicativo web.

4. Selecione **criar** adicionar facilmente um aplicativo do Azure AD para a conexão de área de trabalho de análise.

5. Defina as seguintes configurações na **criar aplicativo de servidor** janela:  

    - **Nome do aplicativo**: Um nome amigável para o aplicativo no Azure AD.

    - **URL da home page**: esse valor não é usado pelo Configuration Manager, mas é exigido pelo Azure AD. Por padrão, esse valor é `https://ConfigMgrService`.  

    - **URI da ID do aplicativo**: esse valor precisa ser exclusivo no locatário do Azure AD. Ele é no token de acesso usado pelo cliente do Configuration Manager para solicitar acesso ao serviço. Por padrão, esse valor é `https://ConfigMgrService`.  

    - **Período de validade da Chave Secreta**: escolha **1 ano** ou **2 anos** na lista suspensa. Um ano é o valor padrão.  

    Selecione **entrar**. Após a autenticação bem-sucedida no Azure, a página mostra o **Nome do Locatário do Azure AD** para referência.

    > [!Note]  
    > Conclua esta etapa como uma **Administrador Global**. Essas credenciais não são salvas pelo Configuration Manager. Essa persona não exige permissões no Configuration Manager e não precisa ser a mesma conta que executa o Assistente de Serviços do Azure.  

    Selecione **OK** para criar o aplicativo Web no Azure AD e feche a caixa de diálogo Criar Aplicativo para Servidores. Na caixa de diálogo do aplicativo de servidor, selecione **Okey**. Em seguida, selecione **próxima** na página do aplicativo do Assistente de serviços do Azure.  

6. Sobre o **dados de diagnóstico** página, defina as seguintes configurações:  

    - **ID comercial**: esse valor deve preencher automaticamente com a ID da sua organização  

    - **Nível de dados de diagnóstico do Windows 10**: Selecione pelo menos **avançado (limitado)**  

    - **Permitir que o nome do dispositivo nos dados de diagnóstico**: selecione **habilitar**  
  
   Selecione **Avançar**. O **funcionalidade disponível** página mostra a funcionalidade de análise de área de trabalho que está disponível com as configurações de dados de diagnóstico da página anterior. Selecione **Avançar**.  

7. Sobre o **coleções** página, defina as seguintes configurações:  

    - **Nome de exibição**: O portal de análise de área de trabalho exibe essa conexão do Configuration Manager usando esse nome. Usá-lo para diferenciar entre hierarquias diferentes. Por exemplo, *laboratório de teste* ou *produção*.  

    - **Coleção de destino**: Esta coleção inclui todos os dispositivos que o Configuration Manager configura com sua ID comercial e as configurações de dados de diagnóstico. É o conjunto completo de dispositivos do Configuration Manager se conecta ao serviço de análise de área de trabalho.  

    - **Dispositivos na coleção de destino usam um proxy de usuário autenticado para comunicação de saída**: Por padrão, esse valor é **não**. Se for necessário em seu ambiente, definido como **Sim**.  

    - **Selecione as coleções específicas para sincronizar com a área de trabalho de análise**: Selecione **adicionar** incluir coleções adicionais. Essas coleções estão disponíveis no portal de análise de área de trabalho para o agrupamento com planos de implantação. Certifique-se de incluir coleções de exclusão do projeto-piloto e piloto.  

        Essas coleções continuam a sincronização como suas alterações de associação. Por exemplo, o seu plano de implantação usa uma coleção com uma regra de associação do Windows 7. Como esses dispositivos de atualização para o Windows 10, e o Configuration Manager avalia a associação da coleção, esses dispositivos soltem fora a coleta e o plano de implantação.  

8. Conclua o assistente.  

O Configuration Manager cria uma política de configurações para configurar dispositivos na coleção de destino. Esta política inclui as configurações de dados de diagnóstico para habilitar dispositivos para enviar dados à Microsoft. Por padrão, clientes atualizam a política a cada hora. Depois de receber as novas configurações, pode ser mais várias horas, antes que os dados estão disponíveis na área de trabalho de análise.

> [!Note]  
> Para obter mais informações sobre essas configurações, consulte [configurações do Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Monitore a configuração de seus dispositivos para análise de área de trabalho. No console do Configuration Manager, vá para o **biblioteca de Software** espaço de trabalho, expanda o **área de trabalho de análise de manutenção** nó e selecione o **integridade de Conexão** Painel de controle.  

Configuration Manager sincroniza suas coleções dentro de 60 minutos de criar a conexão. No portal de análise de área de trabalho, vá para **piloto Global**e ver suas coleções de dispositivos do Configuration Manager.


## <a name="create-a-desktop-analytics-deployment-plan"></a>Criar um plano de implantação de área de trabalho de análise

Use este procedimento para criar um plano de implantação na área de trabalho de análise.

1. Abra o [portal de análise de área de trabalho](https://aka.ms/desktopanalytics). Usar credenciais que tenham pelo menos **colaboradores do espaço de trabalho** permissões.  

2. Selecione **planos de implantação** no grupo gerenciar.  

3. No **planos de implantação** painel, selecione **criar**.  

4. No **criar plano de implantação** painel, defina as seguintes configurações:  

    - **Nome**: Planejar um nome exclusivo para a implantação, por exemplo `Windows 10 pilot`  

    - **Produtos e versões**: Selecione o **Windows** produto e a versão mais recente disponível recomendada. Por exemplo, **Windows 10, versão 1809 (recomendado)** .  

    - **Grupos de dispositivos**: Selecione um ou mais grupos da guia do Configuration Manager e, em seguida, selecione **definido como grupos de destino**. Esses grupos são coleções sincronizadas do Configuration Manager.  

    - **Regras de preparação**: Essas regras ajudam a determinar quais dispositivos está qualificado para atualização. Selecione **sistema operacional WIndows** e defina as seguintes configurações:  

        - **Meus computadores obtém automaticamente os drivers do Windows Update**: A configuração padrão é **desativar**, que é recomendado ao implantar com o Configuration Manager.  

        - **Definir um limite de contagem de instalação baixa para seus aplicativos**: A configuração padrão é `2%`. Aplicativos abaixo desse limite são definidos automaticamente para *baixa contagem de instalações*. Análise da área de trabalho não valida esses suplementos durante o piloto.  

            Se um aplicativo é instalado em uma porcentagem maior de computadores que esse limite, o plano de implantação marcará o aplicativo como *Noteworthy*. Em seguida, você pode decidir sua importância para testar durante a fase piloto.  

    - **Data de conclusão**: Escolha a data pelo qual Windows devem ser totalmente implantada para todos os dispositivos de destino.  

5. Selecione **Criar**. O novo plano é exibida na lista de planos de implantação ao seu que está sendo processado. Para acelerar o processamento, solicite uma atualização de dados sob demanda. Para obter mais informações, consulte [perguntas frequentes sobre análise de área de trabalho](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

6. Abra o plano de implantação, selecionando seu nome.  

7. No menu de plano de implantação, nos **preparação** grupo, selecione **identificar importância**.  

    1. Sobre o **aplicativos** , selecione para mostrar apenas **não revisado** ativos.  

    2. Selecione cada aplicativo e, em seguida, selecione **editar**. Você pode selecionar mais de um aplicativo para editar ao mesmo tempo.  

    3. Escolha um nível de importância do **importância** lista. Se quiser que a área de trabalho de análise para validar o aplicativo durante o piloto, selecione **crítica** ou **importante**. Ele não valida os aplicativos marcados como **importante não**. Avalie suas [compatibilidade](/sccm/desktop-analytics/compat-assessment) e outras informações de plano ao se atribuírem níveis de importância.  

        Ao se atribuírem níveis de importância, você também pode escolher o decisão de atualização.  

    4. Selecione **salvar** ao concluir.  

8. No menu de plano de implantação, nos **preparação** grupo, selecione **identificar piloto**.  

    1. Examine os dispositivos recomendados para o piloto.  

    2. Selecione cada dispositivo e selecione **adicionar ao projeto-piloto**. Se discordar com a recomendação, selecione **substituir**.  

        Para obter mais informações sobre como a área de trabalho de análise torna essas recomendações, selecione o ícone de informações no canto superior direito dos **Identify piloto** painel.



## <a name="deploy-windows-10-in-configuration-manager"></a>Implantar o Windows 10 no Configuration Manager

Use este procedimento para implantar o Windows 10 no Configuration Manager para o grupo piloto.

- Se você ainda não tiver um, primeiro [criar um pacote de atualização do sistema operacional para Windows 10](#bkmk_create-package)  

- Se você ainda não tiver um, [criar uma sequência de tarefas de atualização do sistema operacional para Windows 10](#bkmk_create-ts)  

- [Implantar a sequência de tarefas](#bkmk_deploy-ts) usando o plano de implantação de área de trabalho de análise  

- [Instalar a sequência de tarefas](#bkmk_install-ts) no Centro de Software em um dispositivo de destino  

<!-- 
- [Monitor](#bkmk_monitor-ts) status in Configuration Manager  
 -->

### <a name="bkmk_create-package"></a> Criar um pacote de atualização do sistema operacional para Windows 10

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione o nó **Pacotes de Atualização do Sistema Operacional**.  

2. Na guia **Início** da faixa de opções, no grupo **Criar**, selecione **Adicionar Pacote de Atualização do Sistema Operacional**. Essa ação inicia o Assistente para Adicionar Atualização de Sistema Operacional.  

3. Sobre o **fonte de dados** , especifique a rede **caminho** para a instalação, os arquivos de origem do sistema operacional atualizarem pacote. Por exemplo, `\\server\share\path`.  

    > [!NOTE]  
    > Os arquivos de origem de instalação contêm setup.exe e outros arquivos e pastas para instalar o sistema operacional.  

4. Sobre o **geral** , especifique uma única **nome** pacote de atualização para o sistema operacional.  

5. Conclua o Assistente de pacote de atualização do sistema operacional de adicionar.  

#### <a name="distribute-content"></a>Distribuir conteúdo

Em seguida, distribua o pacote de atualização do sistema operacional para pontos de distribuição.  

1. Selecione o pacote de atualização do sistema operacional na lista. Na guia **Início** da faixa de opções, no grupo **Implantação**, selecione **Distribuir Conteúdo**. O Assistente para Distribuir Conteúdo é aberto.  

2. Sobre o **gerais** , verifique se que o conteúdo listado é o conteúdo que você deseja distribuir e, em seguida, selecione **próxima**.  

3. Sobre o **destino de conteúdo** página, selecione **Add**e escolha **ponto de distribuição**. Selecione um ponto de distribuição existente e, em seguida, selecione **Okey**. Quando você terminar de adicionar destinos de conteúdo, selecione **próxima**.  

4. Conclua o Assistente para distribuir conteúdo.  


### <a name="bkmk_create-ts"></a> Criar uma sequência de tarefas de atualização do sistema operacional para Windows 10

1. No console do Configuration Manager, vá para o **biblioteca de Software** espaço de trabalho, expanda **sistemas operacionais**e, em seguida, selecione **sequências de tarefas**.  

2. Sobre o **Home** guia da faixa de opções, no **criar** grupo, selecione **criar sequência de tarefas**.  

3. Sobre o **criar uma New Task Sequence** página do assistente criar tarefas sequência, selecione **atualizar um sistema operacional de um pacote de atualização**e, em seguida, selecione **próxima**.  

4. Sobre o **informações da sequência de tarefas** , especifique um **nome da sequência de tarefas** que identifica a sequência de tarefas.  

5. Sobre o **atualização do sistema operacional Windows** página, especifique as seguintes configurações e, em seguida, selecione **próxima**:  

    - **Pacote de atualização**: especifique o pacote de atualização que contém os arquivos de origem de atualização do sistema operacional.  

    - **Índice de edição**: se houver vários índices de edição do sistema operacional disponíveis no pacote, selecione o índice de edição desejado. Por padrão, o assistente seleciona o primeiro índice.  

    - **Chave do produto (Product Key)** : especifique a chave do produto do Windows para o sistema operacional instalar. Especifique as chaves de licença de volume codificadas ou as chaves do produto padrão. Se você usar uma chave do produto (Product Key) padrão, separe cada grupo de cinco caracteres com um traço (-). Por exemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Quando a atualização for para uma edição de licença de volume, a chave do produto (Product Key) não será necessária.  

        > [!Note]  
        > Essa chave de produto pode ser uma MAK (chave de ativação múltipla) ou uma GVLK (chave genérica de licenciamento por volume). Uma GVLK também é conhecida como uma chave de instalação de cliente do KMS (Serviço de Gerenciamento de Chaves). Para obter mais informações, consulte [Planejar a ativação de volume](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Para obter uma lista de chaves de instalação de cliente do KMS, veja o [Apêndice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) do guia de ativação do Windows Server.

6. Sobre o **incluir atualizações** página, selecione **próxima** não instalar nenhum software atualiza.  

7. Sobre o **instalar aplicativos** página, selecione **próxima** não instalar nenhum aplicativo.

8. Conclua o Assistente para criar sequência de tarefas.  


### <a name="bkmk_deploy-ts"></a> Implantar a sequência de tarefas usando o plano de implantação de área de trabalho de análise

1. No console do Configuration Manager, vá para o **biblioteca de Software**, expanda **área de trabalho de análise de manutenção**e selecione o **planos de implantação** nó.  

2. Selecione seu plano de implantação piloto do Windows 10 e, em seguida, selecione **detalhes do plano de implantação** na faixa de opções.  

3. No **criar um piloto do status** lado a lado, escolha **sequência de tarefas** na lista suspensa e selecione **implantar**.  

4. No **geral** página do assistente par implantar Software, selecione **procurar** ao lado de **Software** campo. Selecione sua sequência de tarefas de atualização in-loco do Windows 10 e, em seguida, selecione **próxima**.  

    > [!Note]  
    > Com a integração de análise de área de trabalho, o Configuration Manager cria automaticamente uma coleção para o plano de implantação piloto. Ele pode levar até 10 minutos para esta coleção sincronizar antes de você pode usá-lo.<!-- 3887891 -->
    >
    > Essa coleção é reservada para dispositivos de plano de implantação de área de trabalho de análise. Não há suporte para alterações manuais a esta coleção.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Sobre o **conteúdo** página, selecione **Add**e, em seguida, selecione **ponto de distribuição**. Selecione um ponto de distribuição disponíveis para hospedar o conteúdo de instalação e, em seguida, selecione **Okey**. Em seguida, selecione **Avançar**.  

6. Sobre o **configurações de implantação** página, selecione **próxima** para aceitar as configurações padrão. (Uma instalação disponível).  

7. Sobre o **agendamento** página, selecione **próxima** para aceitar as configurações padrão. (Disponível assim que possível.)  

8. Sobre o **experiência de usuário** página, selecione **próxima** para aceitar as configurações padrão. (Exibir no Centro de Software e mostrar apenas as notificações para reinicializações do computador).  

9. Sobre o **alertas** página, selecione **próxima** para aceitar as configurações padrão.  

10. Conclua o assistente.  


### <a name="bkmk_install-ts"></a> Instalar a sequência de tarefas no Centro de Software

1. Entrar em um dispositivo que é um membro do plano de implantação piloto.  

2. Abra **Centro de Software** e instalar o sistema operacional disponível para Windows 10.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>Próximas etapas

Avance para o próximo artigo para saber mais sobre planos de implantação de área de trabalho de análise.
> [!div class="nextstepaction"]  
> [Planos de implantação](/sccm/desktop-analytics/about-deployment-plans)
