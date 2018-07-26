---
title: Implantar aplicativos
titleSuffix: Configuration Manager
description: Criar ou simular uma implantação de um aplicativo em uma coleção de dispositivos ou usuários
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ed6174bcb3c99461b00ec5fc57d4508b9390747d
ms.sourcegitcommit: acad0674b2743193f87990fb50194c4f17823a8e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39146921"
---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>Implantar aplicativos com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Crie ou simule uma implantação de um aplicativo em uma coleção de dispositivos ou usuários no Configuration Manager. Essa implantação fornece instruções para o cliente do Configuration Manager sobre como e quando instalar o software. 

Antes de implantar um aplicativo, crie, pelo menos, um tipo de implantação para o aplicativo. Para mais informações, consulte [Criar aplicativos](/sccm/apps/deploy-use/create-applications).

 Você também pode simular uma implantação de aplicativo. Essa simulação testa a aplicabilidade de uma implantação sem instalar ou desinstalar o aplicativo. Uma implantação simulada avalia o método de detecção, os requisitos e as dependências para um tipo de implantação e relata os resultados no nó **Implantações** do espaço de trabalho **Monitoramento**. Para saber mais, confira [Simular implantações de aplicativos](/sccm/apps/deploy-use/simulate-application-deployments).

> [!IMPORTANT]
>  Simule a implantação de aplicativos obrigatórios, mas não pacotes nem atualizações de software.   
>  Os dispositivos registrados em MDM não dão suporte às configurações de agendamento, de experiência do usuário nem de implantações simuladas.



## <a name="deploy-an-application"></a>Implantar um aplicativo

1.  No console do Configuration Manager, vá para **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.

2.  Na lista **Aplicativos** , selecione o aplicativo a implantar. Na guia **Início** , no grupo **Implantação** , clique em **Implantar**.

### <a name="specify-general-information-about-the-deployment"></a>Especificar informações gerais sobre a implantação

Na página **Geral** do Assistente para Implantar Software, especifique as seguintes informações:

- **Software**: esse valor exibe o aplicativo a ser implantado. Clique em **Procurar** para selecionar outro aplicativo.
- **Coleção**: clique em **Procurar** para selecionar a coleção na qual implantar o aplicativo.
- **Usar grupos de pontos de distribuição padrão associados a esta coleção**: armazene o conteúdo do aplicativo no grupo de pontos de distribuição padrão da coleção. Se você não tiver associado a coleção selecionada a um grupo de pontos de distribuição, essa opção estará indisponível.
- **Distribuir o conteúdo automaticamente para dependências**: se um dos tipos de implantação no aplicativo contiver dependências, o site também enviará o conteúdo do aplicativo dependente aos pontos de distribuição.

    >[!IMPORTANT]
    > Se você atualizar o aplicativo dependente após a implantação do aplicativo primário, o site não distribuirá automaticamente nenhum conteúdo novo para a dependência.

- **Comentários (opcional)**: opcionalmente, insira uma descrição para essa implantação.

### <a name="specify-content-options-for-the-deployment"></a>Especificar as opções de conteúdo para a implantação

Na página **Conteúdo**, clique em **Adicionar** para adicionar o conteúdo associado a essa implantação aos pontos de distribuição ou aos grupos de pontos de distribuição. Se você selecionar **Usar os pontos de distribuição padrão associados a esta coleção** na página **Geral**, em seguida, essa opção será populada automaticamente. Somente um membro da função de segurança Administrador de Aplicativos pode modificá-la.

### <a name="specify-deployment-settings"></a>Especificar configurações da implantação

Na página **Configurações de Implantação** do Assistente para Implantar Software, especifique as seguintes informações:

- **Ação**: na lista suspensa, escolha se essa implantação tem a finalidade de **Instalar** ou **Desinstalar** o aplicativo.

    > [!NOTE]
    >  Se um aplicativo é implantado duas vezes em um dispositivo, uma vez com a ação de **Instalar** e uma vez com a ação de **Desinstalar**, a implantação do aplicativo com a ação de **Instalar** torna-se prioridade.

  Não é possível alterar a ação de uma implantação após sua criação.

- **Finalidade**: na lista suspensa, escolha uma das seguintes opções:  
    - **Disponível**: se o aplicativo for implantado em um usuário, o usuário verá o aplicativo publicado no Centro de Software e poderá instalá-lo sob demanda.
    - **Obrigatório**: o aplicativo é implantado automaticamente de acordo com o agendamento. Se o status de implantação de aplicativo não estiver oculto, qualquer pessoa que usar o aplicativo poderá acompanhar o status de implantação e instalar o aplicativo do Centro de Software antes da data limite.

    > [!NOTE]   
    >  Quando a ação de implantação é definida como **Desinstalar**, a finalidade da implantação é definida automaticamente como **Obrigatória**. Não é possível alterar esse comportamento.  

- **Implantar automaticamente de acordo com o agendamento com ou sem um usuário conectado**: se a implantação for para um usuário, selecione essa opção para implantar o aplicativo nos dispositivos primários do usuário. Esta configuração não requer que o usuário faça logon antes de executar a implantação. Não selecione essa opção se o usuário precisar interagir com a instalação. Essa opção está disponível somente quando a implantação tem a finalidade de **Necessária**.

- **Enviar pacotes de ativação**: se a finalidade da implantação for **Obrigatória**, um pacote de ativação será enviado aos computadores antes de o cliente executar a implantação. Esse pacote ativa os computadores na data limite da instalação. Antes de usar essa opção, os computadores e as redes devem ser configurados para Wake On LAN.
- **Permitir que os clientes com um plano de Internet limitado baixem o conteúdo após a data limite da instalação, o que pode incorrer em custos adicionais**: essa opção está disponível somente para implantações com a finalidade **Obrigatória**.
- **Fechar automaticamente os arquivos executáveis em execução especificados na guia de comportamento da instalação da caixa de diálogo de propriedades do tipo de implantação**: para obter mais informações, consulte [Verificar arquivos executáveis em execução antes de instalar um aplicativo](#how-to-check-for-running-executable-files-before-installing-an-application).

- **Exigir a aprovação do administrador se os usuários solicitarem este aplicativo**: para as versões 1710 e anterior, o administrador aprova as solicitações do usuário para o aplicativo antes de o usuário o instalar. Essa opção fica esmaecida quando a finalidade da implantação é **Obrigatória** ou quando o aplicativo é implantado em uma coleção de dispositivos.  

    > [!NOTE]
    >  As solicitações de aprovação do aplicativo são exibidas no nó **Solicitações de Aprovação** , no **Gerenciamento de Aplicativos** no espaço de trabalho **Biblioteca de Software** . Se uma solicitação não é aprovada no prazo de 45 dias, ela é removida. A reinstalação do cliente pode cancelar as solicitações de aprovação pendentes.  
    >  Depois de aprovar um aplicativo para instalação, você pode **Negar** a solicitação no console do Configuration Manager. Essa ação não faz com que o aplicativo seja desinstalado de nenhum dispositivo, mas impede que os usuários instalem novas cópias do aplicativo por meio do Centro de Software.

- **Um administrador deve aprovar uma solicitação para este aplicativo no dispositivo**: a partir da versão 1802, o administrador aprova as solicitações do usuário para o aplicativo antes de o usuário instalá-lo no dispositivo solicitado. Se o administrador aprova o pedido, o usuário só poderá instalar o aplicativo nesse dispositivo. O usuário deve enviar outro pedido para instalar o aplicativo em outro dispositivo. Essa opção fica esmaecida quando a finalidade da implantação é **Obrigatória** ou quando o aplicativo é implantado em uma coleção de dispositivos. <!--1357015-->  

    Esse é um recurso opcional. Para obter mais informações, consulte [Enable optional features from updates (Habilitar recursos opcionais de atualizações)](/sccm/core/servers/manage/install-in-console-updates#bkmk_options). Se esse recurso não estiver habilitado, você verá a experiência anterior.  

    > [!Important]  
    > O cliente do Configuration Manager também deve estar na versão 1802. Você também deve usar o novo Centro de Software.  

    > [!Note]  
    > Exiba **Solicitações de aprovação**, no **Gerenciamento de aplicativos**, no espaço de trabalho **Biblioteca de software** do console do Configuration Manager. Agora há uma coluna **Dispositivo** na lista para cada solicitação. Quando você toma ação no pedido, a caixa de diálogo Solicitação de Aplicativo também inclui o nome do dispositivo do qual o usuário enviou a solicitação.  
    >  Se uma solicitação não é aprovada no prazo de 45 dias, ela é removida. A reinstalação do cliente pode cancelar as solicitações de aprovação pendentes.  
    >  Depois de aprovar um aplicativo para instalação, você pode **Negar** a solicitação no console do Configuration Manager. Essa ação não faz com que o aplicativo seja desinstalado de nenhum dispositivo, mas impede que os usuários instalem novas cópias do aplicativo por meio do Centro de Software.

- **Atualizar automaticamente qualquer versão substituída deste aplicativo**: o cliente atualiza a versão substituída do aplicativo pelo aplicativo substituto.    

    > [!NOTE]  
    > A partir da versão 1802, para uma finalidade de instalação **Disponível**, você pode habilitar ou desabilitar essa opção. <!--1351266--> 


### <a name="specify-scheduling-settings-for-the-deployment"></a>Especificar configurações de agendamento para a implantação

Na página **Agendamento** do Assistente para Implantar Software, defina a hora em que este aplicativo será implantado ou ficará disponível para os dispositivos cliente.
As opções nesta página diferem dependendo a definição da implantação como **Disponível** ou **Obrigatória**.

Em alguns casos, talvez você queira conceder aos usuários mais tempo instalar as atualizações de software ou as implantações de aplicativo obrigatórias além das datas limite definidas. Esse comportamento geralmente é necessário quando um computador fica desativado por um longo tempo e precisa instalar muitos aplicativos. Por exemplo, se um usuário voltou de férias, ele terá que aguardar um longo período enquanto as implantações de aplicativo atrasadas são instaladas. Para ajudar a resolver esse problema, agora você pode definir um período de carência para a imposição implantando configurações de cliente do Configuration Manager para uma coleção.

Para configurar o período de carência, execute as seguintes ações:

- Na página **Agente de Computador** das configurações do cliente, configure a nova propriedade **Período de carência para a imposição após a data limite da implantação (horas):** com um valor entre **1** e **120** horas.
- Na página **Agendamento** de uma implantação de aplicativo obrigatória, escolha **Atrasar a imposição desta implantação de acordo com as preferências do usuário, até o período de cortesia definido nas configurações do cliente**. O período de cortesia de imposição se aplica a todas as implantações com essa opção habilitada e direcionadas aos dispositivos nos quais você implantou também a configuração do cliente.

Depois que a data limite de instalação do aplicativo for atingida, o cliente instalará o aplicativo na primeira janela fora do horário comercial que o usuário configurou até o período de cortesia. No entanto, o usuário ainda poderá abrir o Centro de Software e instalar o aplicativo a qualquer momento que desejar. Depois que o período de carência expirar, a imposição retorna ao comportamento normal para implantações atrasadas.

Se o aplicativo que estiver sendo implantado substituir outro aplicativo, você poderá definir a data limite de instalação quando os usuários receberem o novo aplicativo. Defina a **Data Limite de Instalação** para atualizar os usuários com o aplicativo substituído.

### <a name="specify-user-experience-settings-for-the-deployment"></a>Especificar as configurações de experiência do usuário para a implantação

Na página **Experiência do Usuário** do Assistente para Implantar Software, especifique as informações sobre como os usuários podem interagir com a instalação do aplicativo.

Ao implantar aplicativos em dispositivos Windows Embedded habilitados para filtro de gravação, especifique para instalar o aplicativo na sobreposição temporária e confirmar as alterações mais tarde. Especifique também a confirmação das alterações na data limite de instalação ou durante uma janela de manutenção. Se você confirmar as alterações na data limite de instalação ou durante uma janela de manutenção, precisará reiniciar o dispositivo. As alterações permanecem no dispositivo.

>[!NOTE]
    >  Ao implantar um aplicativo em um dispositivo Windows Embedded, verifique se ele é membro de uma coleção com uma janela de manutenção. Para obter mais informações sobre janelas de manutenção e dispositivos Windows Embedded, consulte [Criar aplicativos Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md).
    > As opções **Instalação de software** e **Reinicialização do sistema (se necessário para conclusão da instalação)** não são usadas se a finalidade de implantação está definida como **Disponível**. É possível configurar o nível de notificação que um usuário vê quando o aplicativo está instalado.

### <a name="specify-alert-options-for-the-deployment"></a>Especificar as opções de alerta para a implantação

Na página **Alertas** do Assistente para Implantar Software, defina como o Configuration Manager e o System Center Operations Manager geram alertas para essa implantação. É possível configurar limites para relatar alertas e desativar o relatório para a duração da implantação.

### <a name="associate-the-deployment-with-an-ios-app-configuration-policy"></a>Associar a implantação a uma política de configuração de aplicativo iOS

Na página **Políticas de Configuração de Aplicativo**, clique em **Novo** para associar essa implantação a uma política de configuração de aplicativo iOS (se você tiver criado uma). Para obter mais informações sobre este tipo de política, consulte [Configurar aplicativos do iOS com as políticas de configuração de aplicativo](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).

### <a name="deployment-properties"></a>Propriedades de implantação

Encontre a nova implantação no nó **Implantações** do espaço de trabalho **Monitoramento**. É possível editar as propriedades dessa implantação ou excluir a implantação na guia **Implantações** do painel de detalhes do aplicativo.



## <a name="delete-an-application-deployment"></a>Excluir uma implantação de aplicativo

1.  No console do Configuration Manager, vá para **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.
3.  Na lista **Aplicativos**, selecione o aplicativo que inclui a implantação excluída.
4.  Na guia **Implantações** da lista *<nome do aplicativo\>*, selecione a implantação do aplicativo que será excluída. Na guia **Implantação**, no grupo **Implantação**, clique em **Excluir**.

Ao excluir uma implantação de aplicativo, as instâncias do aplicativo que já foram instaladas não serão removidas. Para remover esses aplicativos, é necessário implantar o aplicativo em computadores com **Desinstalar**. Se você excluir uma implantação de aplicativo ou remover um recurso da coleção na qual está implantando, o aplicativo não estará mais visível no Centro de Software.



## <a name="user-notifications-for-required-deployments"></a>Notificações do usuário para implantações necessárias
Quando receber software necessário, na configuração **Suspender e lembrar dentro de**, você pode selecionar na seguinte lista suspensa de valores:
- **Mais tarde**: especifica que as notificações são agendadas com base nas configurações de notificação definidas nas configurações do cliente.
- **Horário fixo**: especifica que a notificação é agendada para ser exibida novamente após o horário selecionado. Por exemplo, se você selecionar 30 minutos, a notificação será exibida novamente em 30 minutos.

![Grupo do Agente de Computador nas configurações padrão do cliente](media/ComputerAgentSettings.png)

O tempo máximo de adiamento sempre se baseia nos valores de notificação definidos nas configurações do cliente em cada horário na linha do tempo de implantação. Por exemplo:
- Defina a configuração **Data limite da implantação superior a 24 horas, lembrar os usuários a cada (horas)** na página **Agente do Computador** com 10 horas.
- O cliente exibe a caixa de diálogo de notificação com um prazo superior a 24 horas antes da data limite de implantação.
- A caixa de diálogo mostra as opções de adiamento até um período de 10 horas, mas nunca superior a esse período. 
- À medida que a data limite de implantação se aproxima, a caixa de diálogo mostra menos opções. Essas opções são consistentes com as configurações do cliente relevantes para cada componente da linha do tempo da implantação.

Para uma implantação de alto risco, como uma sequência de tarefas que implanta um sistema operacional, a experiência de notificação do usuário é mais invasiva. Em vez de uma notificação transitória na barra de tarefas, uma caixa de diálogo como a seguinte é exibida sempre que você é notificado de que uma manutenção de software crítica é necessária:

![A caixa de diálogo Software obrigatório notifica sobre manutenção de software crítico](media/client-toast-notification.png)



## <a name="how-to-check-for-running-executable-files-before-installing-an-application"></a>Como verificar se há arquivos executáveis antes de instalar um aplicativo

Na caixa de diálogo **Propriedades** de um tipo de implantação, na guia **Comportamento da Instalação**, especifique um ou mais arquivos executáveis. Se um desses arquivos executáveis estiver em execução no cliente, ele bloqueará a instalação do tipo de implantação. O usuário deve fechar o arquivo executável em execução para que o cliente possa instalar o tipo de implantação. Para implantações com a finalidade obrigatória, o cliente pode fechar automaticamente o arquivo executável em execução.

1. Abra a caixa de diálogo **Propriedades** para qualquer tipo de implantação.
2. Na guia **Comportamento da Instalação** da caixa de diálogo *<deployment type name>* **Propriedades**, clique em **Adicionar**.
3. Na caixa de diálogo **Adicionar ou Editar Arquivo Executável**, digite o nome do arquivo executável que, se estiver em execução, bloqueará a instalação do aplicativo. Opcionalmente, você também pode inserir um nome amigável para o aplicativo para ajudar a identificá-lo na lista.
4. Clique em **OK** e feche a caixa de diálogo *<deployment type name>* **Propriedades**.
5. Ao implantar o aplicativo, na página **Configurações de Implantação** do Assistente de Implantação de Software, selecione **Fechar automaticamente todos os executáveis em execução especificados na guia de comportamento da instalação da caixa de diálogo de propriedades do tipo de implantação**.

Depois que os clientes recebem a implantação, o seguinte comportamento se aplica:

- Se você implantar o aplicativo como **Disponível** e um usuário final tentar instalá-lo, o cliente solicitará ao usuário o fechamento dos arquivos executáveis em execução especificados antes de continuar com a instalação.

- Se você implantar o aplicativo como **Obrigatório** e especificar a opção **Fechar automaticamente todos os executáveis em execução especificados na guia de comportamento de instalação da caixa de diálogo de propriedades do tipo de implantação**, o usuário verá uma caixa de diálogo informando que os arquivos executáveis especificados serão fechados automaticamente quando a data limite de instalação for atingida. Você pode agendar essas caixas de diálogo em **Configurações do Cliente** > **Agente de Computador**. Se você não quiser que o usuário final veja essas mensagens, selecione **Ocultar no Centro de Software e todas as notificações** na guia **Experiência do Usuário** das propriedades da implantação.

- Se você implantar o aplicativo como **Obrigatório** e não especificar a opção **Fechar automaticamente todos os executáveis em execução especificados na guia de comportamento de instalação da caixa de diálogo de propriedades do tipo de implantação**, a instalação do aplicativo falhará se um ou mais dos aplicativos especificados estarão em execução.



## <a name="deploy-user-available-applications-on-azure-ad-joined-devices"></a>Implantar aplicativos disponíveis para o usuário em dispositivos ingressados no Azure AD
<!-- 1322613 --> Se você implantar aplicativos como disponíveis para os usuários, a partir da versão 1802, eles poderão procurá-los e instalá-los por meio do Centro de Software nos dispositivos Azure AD (Azure Active Directory).  

#### <a name="prerequisites"></a>Pré-requisitos

- Habilitar o HTTPS no ponto de gerenciamento  

- Integrar o site com o [Azure AD](/sccm/core/servers/deploy/configure/azure-services-wizard) para o **Gerenciamento de Nuvem**  

    - Configurar a [descoberta de usuários do Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

- Implantar um aplicativo como disponível em uma coleção de usuários por meio do Azure AD  

- Distribuir qualquer conteúdo do aplicativo para um [ponto de distribuição na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)  

- Habilite a configuração do cliente **Usar o novo Centro de Software** no grupo [Agente de computador](/sccm/core/clients/deploy/about-client-settings#computer-agent)  

- O sistema operacional cliente deve ser o Windows 10 e estar ingressado no Azure AD. Ingressado no domínio puramente de nuvem ou ingressado no Azure AD híbrido.  

- Para dar suporte a clientes baseados na Internet:  

    - [Gateway de gerenciamento de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway)  

    - Habilite a configuração do cliente: **Habilitar solicitações da política de usuário de clientes da Internet** no grupo [Política do Cliente](/sccm/core/clients/deploy/about-client-settings#client-policy)  

- Para dar suporte aos clientes na intranet:  

    - Adicione o ponto de distribuição da nuvem a um grupo de limites usado pelos clientes  

    - Os clientes devem ser capazes de resolver o nome de domínio totalmente qualificado (FQDN) do ponto de gerenciamento habilitado para HTTPS  



## <a name="next-steps"></a>Próximas etapas

   -  [Configurações para gerenciar implantações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md)  
   -  [Como definir as configurações do cliente](../../core/clients/deploy/configure-client-settings.md)
   -  [Guia do usuário do Centro de Software](/sccm/core/understand/software-center)

