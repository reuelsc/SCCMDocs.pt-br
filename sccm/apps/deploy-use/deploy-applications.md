---
title: Implantar aplicativos
titleSuffix: Configuration Manager
description: Criar ou simular uma implantação de um aplicativo em uma coleção de dispositivos ou usuários
ms.date: 06/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5760b36ddb29c39d6887afb61445f1353f46bbec
ms.sourcegitcommit: 7dd42b5a280e64feb69a947dae082fdaf1571272
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66715687"
---
# <a name="deploy-applications-with-configuration-manager"></a>Implantar aplicativos com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Crie ou simule uma implantação de um aplicativo em uma coleção de dispositivos ou usuários no Configuration Manager. Essa implantação fornece instruções para o cliente do Configuration Manager sobre como e quando instalar o software.

Antes de implantar um aplicativo, crie, pelo menos, um tipo de implantação para o aplicativo. Para mais informações, consulte [Criar aplicativos](/sccm/apps/deploy-use/create-applications).

Você também pode simular uma implantação de aplicativo. Essa simulação testa a aplicabilidade de uma implantação sem instalar ou desinstalar o aplicativo. Uma implantação simulada avalia o método de detecção, os requisitos e as dependências para um tipo de implantação e relata os resultados no nó **Implantações** do workspace **Monitoramento**. Para saber mais, confira [Simular implantações de aplicativos](/sccm/apps/deploy-use/simulate-application-deployments).

> [!Note]
> Você só pode simular a implantação de aplicativos obrigatórios, mas não de pacotes ou atualizações de software.
>
> Os dispositivos registrados em MDM não dão suporte às configurações de agendamento, de experiência do usuário nem de implantações simuladas.



## <a name="bkmk_deploy"></a> Implantar um aplicativo

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e selecione o nó **Aplicativos**.  

2. Na lista **Aplicativos**, selecione um aplicativo a ser implantado. Na faixa de opções, clique em **Implantar**.  

> [!Note]  
> Quando você exibe as propriedades de uma implantação existente, as seções a seguir correspondem às guias da janela Propriedades da implantação:  
>
> - [Geral](#bkmk_deploy-general)
> - [Conteúdo](#bkmk_deploy-content)
> - [Configurações de Implantação](#bkmk_deploy-settings)
> - [Agendamento](#bkmk_deploy-sched)
> - [Experiência do Usuário](#bkmk_deploy-ux)
> - [Alertas](#bkmk_deploy-alerts)
> - [iOS: Políticas de Configuração de Aplicativo](#bkmk_deploy-ios)


### <a name="bkmk_deploy-general"></a> Informações **Gerais** da Implantação

Na página **Geral** do Assistente para Implantar Software, especifique as seguintes informações:  

- **Software**: esse valor exibe o aplicativo a ser implantado. Clique em **Procurar** para selecionar outro aplicativo.  

- **Coleção**: clique em **Procurar** para selecionar a coleção na qual implantar o aplicativo.  

- **Usar grupos de pontos de distribuição padrão associados a esta coleção**: armazene o conteúdo do aplicativo no grupo de pontos de distribuição padrão da coleção. Se você não tiver associado a coleção selecionada a um grupo de pontos de distribuição, essa opção estará desabilitada.  

- **Distribuir o conteúdo automaticamente para dependências**: se um dos tipos de implantação no aplicativo contiver dependências, o site também enviará o conteúdo do aplicativo dependente aos pontos de distribuição.  

    >[!Note]  
    > Se você atualizar o aplicativo dependente após a implantação do aplicativo primário, o site não distribuirá automaticamente nenhum conteúdo novo para a dependência.  

- **Comentários (opcional)** : opcionalmente, insira uma descrição para essa implantação.  


### <a name="bkmk_deploy-content"></a> Opções de **Conteúdo** da implantação

Na página **Conteúdo**, clique em **Adicionar** para distribuir o conteúdo desse aplicativo a um ponto de distribuição ou a um grupo de pontos de distribuição.

Se você tiver selecionado a opção **Usar pontos de distribuição padrão associados a essa coleção** na página Geral, essa opção será populada automaticamente. Somente um membro da função de segurança **Administrador de Aplicativos** pode modificá-lo.

Se o conteúdo do aplicativo já estiver distribuído, ele aparecerá aqui.


### <a name="bkmk_deploy-settings"></a> **Configurações de Implantação**

Na página **Configurações da implantação**, especifique as seguintes informações:  

- **Ação**: na lista suspensa, escolha se essa implantação tem a finalidade de **Instalar** ou **Desinstalar** o aplicativo.  

    > [!NOTE]  
    > Se você criar uma implantação para **Instalar** um aplicativo e outra implantação para **Desinstalar** o mesmo aplicativo no mesmo dispositivo, a implantação para **Instalar** terá prioridade.  

    Você não pode alterar a ação de uma implantação depois de criá-la.  

- **Finalidade**: na lista suspensa, escolha uma das seguintes opções:  

  - **Disponível**: o usuário vê o aplicativo no Centro de Software. Ele pode instalar o aplicativo sob demanda.  

  - **Obrigatório**: o cliente instala o aplicativo automaticamente de acordo com o agendamento que você define. Quando o aplicativo não está oculto, os usuários podem acompanhar o status da implantação. Eles também podem usar o Centro de Software para instalar o aplicativo antes da data limite.  

    > [!NOTE]  
    > Quando você define a ação de implantação como **Desinstalar**, a finalidade da implantação é definida automaticamente como **Obrigatória**. Não é possível alterar esse comportamento.  

- **Permita que os usuários finais tentem reparar esse aplicativo**: da versão 1810 em diante, se você tiver criado o aplicativo com uma linha de comando de reparo, habilite esta opção. Os usuários veem uma opção no Centro de Software para **Reparar** o aplicativo.<!--1357866-->  

- **Pré-implantar o software no dispositivo primário do usuário**: se a implantação for para um usuário, selecione essa opção para implantar o aplicativo no dispositivo primário do usuário. Essa configuração não exige que o usuário entre para que a implantação seja executada. Se o usuário precisar interagir com a instalação, não selecione essa opção. Essa opção só está disponível quando a implantação é **Obrigatória**.  

- **Enviar pacotes de ativação**: se a implantação for **Obrigatória**, o Configuration Manager enviará um pacote de ativação aos computadores antes que o cliente execute a implantação. Esse pacote ativa os computadores na data limite da instalação. Antes de usar essa opção, os computadores e as redes devem ser configurados para Wake On LAN. Para obter mais informações, confira [Planejar como ativar clientes](/sccm/core/clients/deploy/plan/plan-wake-up-clients).  

- **Permitir que os clientes com um plano de Internet limitado baixem o conteúdo após a data limite da instalação, o que pode incorrer em custos adicionais**: essa opção está disponível somente para implantações com a finalidade **Obrigatória**.  

- **Atualizar automaticamente qualquer versão substituída deste aplicativo**: o cliente atualiza a versão substituída do aplicativo pelo aplicativo substituto.

    > [!Note]  
    > Essa opção funciona independentemente da aprovação do administrador. Se um administrador já aprovou a versão substituída, a versão substituta não precisa ser aprovada. A aprovação é apenas para novas solicitações, não substituindo as atualizações.<!--515824-->  

    > [!NOTE]  
    > A partir da versão 1802, para uma finalidade de instalação **Disponível**, você pode habilitar ou desabilitar essa opção. <!--1351266-->


#### <a name="bkmk_approval"></a> Configurações de aprovação

Uma das seguintes configurações de aprovação é exibida, dependendo da versão do Configuration Manager:

- **Exigir a aprovação do administrador se os usuários solicitarem este aplicativo**: para as versões 1710 e anterior, o administrador aprova as solicitações do usuário para o aplicativo antes de o usuário o instalar. Essa opção fica desabilitada quando a finalidade da implantação é **Obrigatória** ou quando o aplicativo é implantado em uma coleção de dispositivos.  

- **Um administrador deve aprovar uma solicitação para este aplicativo no dispositivo**: a partir da versão 1802, o administrador aprova as solicitações do usuário para o aplicativo antes de o usuário instalá-lo no dispositivo solicitado. Se o administrador aprova o pedido, o usuário só poderá instalar o aplicativo nesse dispositivo. O usuário deve enviar outro pedido para instalar o aplicativo em outro dispositivo. Essa opção fica desabilitada quando a finalidade da implantação é **Obrigatória** ou quando o aplicativo é implantado em uma coleção de dispositivos.

Começando na versão 1810, você também pode definir uma lista de endereços de email para notificar sobre a solicitação de aprovação.<!--1357015-->  

Para obter mais informações, confira [Aprovar aplicativos](/sccm/apps/deploy-use/app-approval).


#### <a name="deployment-properties-deployment-settings"></a>**Configurações da implantação** das propriedades de implantação

Quando você exibir as propriedades de uma implantação, se houver suporte da tecnologia do tipo de implantação, a opção a seguir aparecerá na guia **Configurações da Implantação**:

**Fechar automaticamente todos os executáveis em execução especificados na guia de comportamento de instalação da caixa de diálogo de propriedades do tipo de implantação**. Para obter mais informações, confira [verificar se há arquivos executáveis antes de instalar um aplicativo](#bkmk_exe-check).



### <a name="bkmk_deploy-sched"></a> Configurações de **Agendamento** da implantação

Na página **Agendamento**, defina a hora em que este aplicativo será implantado ou ficará disponível para os dispositivos clientes.

Por padrão, o Configuration Manager disponibiliza a política de implantação para os clientes imediatamente. Se você quiser criar a implantação, mas não disponibilizá-la aos clientes até uma data posterior, configure a opção para **Agendar a disponibilidade do aplicativo**. Em seguida, selecione a data e hora, incluindo se está em UTC ou na hora do local do cliente.

Se a implantação for **Obrigatória**, especifique também a **Data limite da instalação**. Por padrão, essa data limite é o quanto antes.

Por exemplo, você precisa implantar um novo aplicativo de linha de negócios. Todos os usuários precisam instalá-lo até um determinado prazo, mas você quer dar a eles a opção de aceitar antes. Você também precisa verificar se o site distribuiu o conteúdo a todos os pontos de distribuição. Você agenda o aplicativo para ficar disponível daqui a cinco dias a partir de hoje. Esse agendamento permite que haja tempo para distribuir o conteúdo e confirmar seu status. Em seguida, você define a data limite da instalação para um mês a partir de hoje. Os usuários verão o aplicativo no Centro de Software quando ele ficar disponível daqui a cinco dias. Se eles não fizerem nada, o cliente instalará automaticamente o aplicativo na data limite da instalação.

Se o aplicativo que você está implantando substitui outro aplicativo, defina a data limite da instalação para quando os usuários receberem o novo aplicativo. Defina a **Data Limite de Instalação** para atualizar os usuários com o aplicativo substituído.


#### <a name="delay-enforcement-with-a-grace-period"></a>Imposição de atraso com um período de cortesia

Talvez você queira dar aos usuários mais tempo para instalar os aplicativos obrigatórios *além das* datas limites definidas. Esse comportamento geralmente é necessário quando um computador fica desligado por um longo tempo e precisa instalar muitos aplicativos. Por exemplo, quando um usuário retorna de férias, ele precisa esperar bastante tempo para que o cliente instale as implantações vencidas. Para ajudar a resolver esse problema, defina um período de carência de imposição.

- Primeiro, configure esse período de carência com a propriedade **Período de carência para imposição após a data limite da implantação (horas)** nas configurações do cliente. Para obter mais informações, confira o grupo [Agente de computador](/sccm/core/clients/deploy/about-client-settings#computer-agent). Especifique um valor entre **1** e **120** horas.  

- Na página **Agendamento** de uma implantação de aplicativo obrigatória, habilite a opção **Atrasar a imposição desta implantação de acordo com as preferências do usuário, até o período de carência definido nas configurações do cliente**. O período de cortesia de imposição se aplica a todas as implantações com essa opção habilitada e direcionadas aos dispositivos nos quais você implantou também a configuração do cliente.

Após a data limite, o cliente instala o aplicativo no primeiro período fora do horário comercial, que o usuário configurou, até esse período de carência. No entanto, o usuário ainda poderá abrir o Centro de Software e instalar o aplicativo a qualquer momento que desejar. Depois que o período de carência expirar, a imposição retorna ao comportamento normal para implantações atrasadas.

![Diagrama de linha do tempo do período de cortesia](media/grace-period.svg)

<!-- SCCMDocs issue #1599 -->

> [!Note]  
> Na maioria das vezes, esse recurso aborda o cenário quando o dispositivo está desligado enquanto o usuário está fora do escritório. Tecnicamente, o período de cortesia começa quando o cliente obtém a política após o prazo de implantação. O mesmo comportamento ocorre se você parar o serviço de cliente do Configuration Manager (CcmExec) e depois reiniciá-lo em algum momento após o prazo de implantação.

### <a name="bkmk_deploy-ux"></a> Configurações da **Experiência do Usuário** da implantação

Na página **Experiência do Usuário**, especifique as informações de como os usuários podem interagir com a instalação do aplicativo.

- **Notificações do usuário**: especifique se deseja exibir notificações no Centro de Software no horário de disponibilidade configurado. Essa configuração também controla se os usuários devem ser notificados nos computadores cliente. Para implantações disponíveis, você não pode selecionar a opção **Ocultar no Centro de Software e em todas as notificações**.  

    - **Quando forem necessárias alterações no software, mostrar uma janela de caixa de diálogo ao usuário em vez de uma notificação do sistema**<!--3555947-->: a partir da versão 1902, selecione essa opção para tornar a experiência do usuário mais intrusiva. Isso só se aplica a implantações necessárias. Para saber mais, confira [Plano para o Centro de Software](/sccm/apps/plan-design/plan-for-software-center#bkmk_impact).

- **Instalação de Software** e **Reinicialização do sistema**: apenas defina essas configurações para as implantações obrigatórias. Elas especificam os comportamentos quando a implantação atinge a data limite fora de uma janela de manutenção definida. Para obter mais informações sobre janelas de manutenção, consulte [Como usar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).  

- **Tratamento de filtro de gravação para dispositivos Windows Embedded com filtro de gravação**: essa configuração controla o comportamento da instalação em dispositivos Windows Embedded habilitados com um filtro de gravação. Escolha a opção para confirmar as alterações na data limite da instalação ou durante uma janela de manutenção. Quando você seleciona essa opção, a reinicialização é necessária e as alterações permanecem no dispositivo. Caso contrário, o aplicativo é instalado na sobreposição temporária e confirmado mais tarde.  

    - Ao implantar uma atualização de software em um dispositivo Windows Embedded, verifique se o dispositivo é membro de uma coleção que tem uma janela de manutenção configurada. Para obter mais informações sobre janelas de manutenção e dispositivos Windows Embedded, consulte [Criar aplicativos Windows Embedded](/sccm/apps/get-started/creating-windows-embedded-applications).  


### <a name="bkmk_deploy-alerts"></a> **Alertas** de implantação

Na página **Alertas**, configure como o Configuration Manager gera alertas para essa implantação. Se você também estiver usando o System Center Operations Manager, configure seus alertas. Você só pode configurar alguns alertas para implantações obrigatórias. 


### <a name="bkmk_deploy-ios"></a> iOS: **Políticas de Configuração de Aplicativo**

Durante a implantação de um tipo de implantação do iOS, você também verá a página **Políticas de Configuração de Aplicativo**. Se você já tiver criado uma política de configuração de aplicativo iOS, clique em **Novo** para associar essa implantação com a política. Para obter mais informações sobre este tipo de política, consulte [Configurar aplicativos do iOS com as políticas de configuração de aplicativo](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).



## <a name="bkmk_phased"></a> Criar uma implantação em fases

<!--1358147-->
A partir da versão 1806, crie uma implantação em fases para um aplicativo. As implantações em fases permitem que você coordene uma distribuição coordenada e sequenciada do software com base em grupos e critérios personalizáveis. Por exemplo, implante o aplicativo em uma coleção piloto e, em seguida, continue automaticamente a distribuição com base nos critérios de sucesso. 

Para obter mais informações, consulte os seguintes artigos:  

- [Criar uma implantação em fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Gerenciar e monitorar as implantações em fases](/sccm/osd/deploy-use/manage-monitor-phased-deployments?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  



## <a name="bkmk_delete"></a> Excluir uma implantação

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e selecione o nó **Aplicativos**.  

2. Na lista **Aplicativos**, selecione o aplicativo que inclui a implantação que será excluída.  

3. Mude para a guia **Implantações** do painel de detalhes e selecione a implantação do aplicativo.  

4. Na faixa de opções, na guia **Implantação** e no grupo de **Implantação**, clique em **Excluir**.  

Quando você exclui uma implantação de aplicativo, as instâncias do aplicativo que os clientes já têm instaladas não são removidas. Para remover esses aplicativos, implante o aplicativo nos computadores para **Desinstalar**. Se você excluir uma implantação de aplicativo ou remover um recurso da coleção na qual está implantando, o aplicativo não será mais exibido no Centro de Software.



## <a name="bkmk_notify"></a> Notificações do usuário sobre implantações obrigatórias

Quando os usuários recebem o software obrigatório e selecionam a configuração **Adiar e lembrar-me**, eles podem escolher entre as seguintes opções:  

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



## <a name="bkmk_exe-check"></a> Verificar arquivos executáveis

Configure uma implantação para verificar se determinados arquivos executáveis estão em execução no cliente. Use essa opção para verificar se há processos que possam interromper a instalação do aplicativo. Se um desses arquivos executáveis estiver em execução, o cliente bloqueará a instalação do tipo de implantação. O usuário deve fechar o arquivo executável em execução para que o cliente possa instalar o tipo de implantação. Para implantações com a finalidade obrigatória, o cliente pode fechar automaticamente o arquivo executável em execução.

1. Abra a caixa de diálogo **Propriedades** do tipo de implantação.  

2. Mude para a guia **Comportamento da Instalação** e, em seguida, clique em **Adicionar**.  

3. Na caixa de diálogo **Adicionar Arquivo Executável**, digite o nome do arquivo executável de destino. Opcionalmente, insira um nome amigável para o aplicativo para ajudar a identificá-lo na lista.  

4. Clique em **OK** e, em seguida, em **OK** novamente para fechar a janela Propriedades do tipo de implantação.  

5. Ao implantar o aplicativo, selecione a opção para **Fechar automaticamente todos os executáveis em execução especificados na guia de comportamento de instalação da caixa de diálogo de propriedades do tipo de implantação**. Essa opção está na guia **Configurações de Implantação** das propriedades da implantação.  


### <a name="client-behaviors-and-user-notifications"></a>Comportamentos do cliente e notificações do usuário

Depois que os clientes recebem a implantação, o seguinte comportamento se aplica:  

- Se você implantar o aplicativo como **Disponível** e um usuário final tentar instalá-lo, o cliente solicitará ao usuário o fechamento dos arquivos executáveis em execução especificados antes de continuar a instalação.  

- Se você implantar o aplicativo como **Obrigatório** e especificar a opção **Fechar automaticamente todos os executáveis em execução especificados na guia de comportamento de instalação da caixa de diálogo de propriedades do tipo de implantação**, o cliente exibirá uma notificação. Ela informará ao usuário que os arquivos executáveis especificados serão fechados automaticamente quando a data limite da instalação do aplicativo for atingida.  

    - Agende essas caixas de diálogo no grupo **Agente de Computador** das configurações do cliente. Para obter mais informações, confira [Agente de computador](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

    - Se você não quiser que o usuário veja essas mensagens, selecione a opção para **Ocultar no Centro de Software e todas as notificações** na guia **Experiência do Usuário** das propriedades da implantação. Para obter mais informações, confira [Configurações de experiência do usuário da implantação](#bkmk_deploy-ux).  

- Se você implantar o aplicativo como **Obrigatório** e não especificar a opção **Fechar automaticamente todos os executáveis em execução especificados na guia de comportamento de instalação da caixa de diálogo de propriedades do tipo de implantação**, a instalação do aplicativo falhará se um ou mais dos aplicativos especificados estarão em execução.  



## <a name="deploy-user-available-applications-on-azure-ad-joined-devices"></a>Implantar aplicativos disponíveis para o usuário em dispositivos ingressados no Azure AD

<!-- 1322613 -->
Se você implantar aplicativos como disponíveis para os usuários, a partir da versão 1802, eles poderão procurá-los e instalá-los por meio do Centro de Software nos dispositivos Azure AD (Azure Active Directory).  

### <a name="prerequisites"></a>Pré-requisitos

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

    - Os clientes precisam ser capazes de resolver o FQDN (nome de domínio totalmente qualificado) do ponto de gerenciamento habilitado para HTTPS  



## <a name="next-steps"></a>Próximas etapas

- [Monitorar aplicativos](/sccm/apps/deploy-use/monitor-applications-from-the-console)
- [Solucionar problemas de implantação do aplicativo](/sccm/apps/deploy-use/troubleshoot-application-deployment)
- [Tarefas de gerenciamento de aplicativos](/sccm/apps/deploy-use/management-tasks-applications)
- [Guia do usuário do Centro de Software](/sccm/core/understand/software-center)
