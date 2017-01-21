---
title: Implantar aplicativos | Microsoft Docs
description: "Crie um tipo de implantação ou simule uma implantação de um aplicativo usando o System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
caps.latest.revision: 10
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 7be9abadeb51d4f9e862f69c332756b19ce3e110
ms.openlocfilehash: a52bef3c8d12ffe2d9b13dc79cbc8950d3f36aea


---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>Implantar aplicativos com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Para poder implantar um aplicativo no System Center Configuration Manager, é necessário criar pelo menos um tipo de implantação para o aplicativo. Para obter mais informações sobre a criação de tipos de implantação e aplicativos, consulte [Criar aplicativos](../../apps/deploy-use/create-applications.md).

 Você também pode simular uma implantação de aplicativo. Esse tipo de implantação testa a aplicabilidade de uma implantação de aplicativo em computadores sem instalar ou desinstalar o aplicativo. Uma implantação simulada avalia o método de detecção, os requisitos e as dependências para um tipo de implantação e relata os resultados no nó **Implantações** do espaço de trabalho **Monitoramento**. Para mais informações, consulte [Simular implantações de aplicativos](../../apps/deploy-use/simulate-application-deployments.md).

> [!IMPORTANT]
>  É possível implantar (instalar ou desinstalar) aplicativos necessários, mas não pacotes ou atualizações de software. Os dispositivos registrados em MDM também não dão suporte às configurações de agendamento, às experiência do usuário nem às implantações simuladas.

## <a name="deploy-an-application"></a>Implantar um aplicativo

1.  No console do Configuration Manager, vá para **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.

2.  Na lista **Aplicativos** , selecione o aplicativo a implantar. Na guia **Início** , no grupo **Implantação** , clique em **Implantar**.

### <a name="specify-general-information-about-the-deployment"></a>Especificar informações gerais sobre a implantação

Na página **Geral** do Assistente para Implantar Software, especifique as seguintes informações:

- **Software** – Exibe o aplicativo a ser implantado. Você pode clicar em **Procurar** para selecionar um aplicativo diferente.
- **Coleção** – Clique em **Procurar** para selecionar a coleção na qual o aplicativo será implantado.
- **Usar grupos de pontos de distribuição padrão associados a esta coleção** – Selecione essa opção se quiser armazenar o conteúdo do aplicativo no grupo de pontos de distribuição padrão da coleção. Se você não tiver associado a coleção selecionada a um grupo de pontos de distribuição, essa opção estará indisponível.
- **Distribuir automaticamente conteúdo para dependências** – Se estiver habilitada e algum tipo de implantação no aplicativo contiver dependências, o conteúdo do aplicativo dependente também será enviado aos pontos de distribuição.

    >[!IMPORTANT]
    > Se você atualizar o aplicativo dependente após a implantação do aplicativo primário, qualquer conteúdo novo para a dependência não é distribuído automaticamente.

- **Comentários (opcional)** – opcionalmente, insira uma descrição dessa implantação.

### <a name="specify-content-options-for-the-deployment"></a>Especificar as opções de conteúdo para a implantação

Na página **Conteúdo**, clique em **Adicionar** para adicionar o conteúdo associado a essa implantação aos pontos de distribuição ou aos grupos de pontos de distribuição. Se você selecionou **Usar pontos de distribuição padrão associados a esta coleção** na página **Geral**, essa opção será automaticamente populada e poderá ser modificada apenas por um membro da função de segurança Administrador de Aplicativos.

### <a name="specify-deployment-settings"></a>Especificar configurações da implantação

Na página **Configurações de Implantação** do Assistente para Implantar Software, especifique as seguintes informações:

- **Ação** – Na lista suspensa, escolha se essa implantação tem a intenção de **Instalar** ou **Desinstalar** o aplicativo.

    > [!NOTE]
    >  Se um aplicativo é implantado duas vezes em um dispositivo, uma vez com a ação de **Instalar** e uma vez com a ação de **Desinstalar**, a implantação do aplicativo com a ação de **Instalar** torna-se prioridade.

Não é possível alterar a ação de uma implantação após ela ter sido criada.

- **Finalidade** – Na lista suspensa, escolha uma das seguintes opções:
    - **Disponível** – Se o aplicativo for implantado em um usuário, o usuário verá o aplicativo publicado no Centro de Software e poderá instalá-lo sob demanda.
    - **Necessária** – O aplicativo é implantado automaticamente de acordo com o agendamento. Se o status de implantação de aplicativo não estiver oculto, qualquer pessoa que usar o aplicativo poderá acompanhar o status de implantação e instalar o aplicativo do Centro de Software antes da data limite.

    > [!NOTE]   
    >  Quando a ação de implantação está definida para **Desinstalar**, a finalidade da implantação é definida automaticamente como **Necessária** e não pode ser alterada.  

- **Implantar automaticamente de acordo com o agendamento com ou sem um usuário conectado** – Se a implantação for para um usuário, selecione essa opção para implantar o aplicativo aos dispositivos primários do usuário. Esta configuração não requer que o usuário faça logon antes de executar a implantação. Não selecione esta opção se o usuário precisar fornecer uma entrada para concluir a instalação. Essa opção está disponível somente quando a implantação tem a finalidade de **Necessária**.


- **Enviar pacotes de ativação** – Se a finalidade da implantação estiver definida como **Necessária** e essa opção estiver selecionada, um pacote de ativação será enviado aos computadores antes de a implantação ser instalada. Esse pacote ativa os computadores na data limite da instalação. Para usar essa opção, os computadores e as redes devem ser configurados para Wake on LAN.
- **Todos os clientes com uma conexão de Internet limitada para baixar conteúdo após a data limite de instalação, o que pode estar sujeito a custos adicionais** – Essa opção está disponível somente para implantações com a finalidade de **Necessária**.
- **Exigir aprovação do administrador, se os usuários solicitarem este aplicativo** – Se essa opção estiver selecionada, o administrador precisará aprovar todas as solicitações do usuário para o aplicativo antes que ele possa ser instalado. Essa opção estará esmaecida quando a finalidade da implantação for **Necessária** ou quando o aplicativo for implantado em uma coleção de dispositivos.

    > [!NOTE]
    >  As solicitações de aprovação do aplicativo são exibidas no nó **Solicitações de Aprovação** , no **Gerenciamento de Aplicativos** no espaço de trabalho **Biblioteca de Software** . Se uma solicitação não for aprovada dentro de 45 dias, ela será removida. Além disso, reinstalar o cliente do Configuration Manager pode cancelar as solicitações de aprovação pendentes.
    > Depois de ter aprovado um aplicativo para a instalação, você pode escolher subsequentemente para negar a solicitação clicando em **Negar** no console do Configuration Manager (anteriormente esse botão estava esmaecido após aprovação).
    > Essa ação não faz com que o aplicativo seja desinstalado de nenhum dispositivo, mas impede que os usuários instalem novas cópias do aplicativo do Centro de Software.



- **Atualizar automaticamente qualquer versão substituída deste aplicativo** – Se essa opção estiver selecionada, quaisquer versões substituídas do aplicativo serão atualizadas com o aplicativo substituto.

### <a name="specify-scheduling-settings-for-the-deployment"></a>Especificar configurações de agendamento para a implantação

Na página **Agendamento** do Assistente para Implantar Software, defina a hora em que este aplicativo será implantado ou ficará disponível para os dispositivos cliente.
As opções dessa página irão diferir dependendo se a ação de implantação for definida como **Disponível** ou **Obrigatória**.

Em alguns casos, talvez você queira conceder aos usuários mais tempo instalar as atualizações de software ou as implantações de aplicativo obrigatórias além das datas limite definidas. Isso normalmente é necessário quando um computador ficou desligado por um período estendido e precisa instalar uma grande quantidade de implantações de aplicativo ou atualizações. Por exemplo, se um usuário acabou de voltar de férias, eles terá que aguardar um longo período enquanto as implantações de aplicativo atrasadas são instaladas. Para ajudar a resolver esse problema, agora você pode definir um período de carência para a imposição implantando configurações de cliente do Configuration Manager para uma coleção.

Para configurar o período de carência, execute as seguintes ações:

- Na página **Agente de Computador** das configurações do cliente, configure a nova propriedade **Período de carência para a imposição após a data limite da implantação (horas):** com um valor entre **1** e **120** horas.
- Na página **Agendamento** em uma nova implantação de aplicativo necessária, ou nas propriedades de uma implantação existente, selecione a caixa **Atrasar a imposição dessa implantação de acordo com as preferências do usuário até o período de carência definido nas configurações do cliente**. O período de carência de imposição é usado por todas as implantações que têm essa caixa selecionada e são voltadas para dispositivos nos quais você também implantou a configuração do cliente.

Após a data limite de instalação do aplicativo ser atingida, o aplicativo será instalado na primeira janela fora do horário comercial que o usuário configurou até o período de carência. No entanto, o usuário ainda poderá abrir o Centro de Software e instalar o aplicativo a qualquer momento que desejar. Depois que o período de carência expirar, a imposição retorna ao comportamento normal para implantações atrasadas.

Se o aplicativo que você está implantando substitui outro aplicativo, você pode definir a data limite de instalação quando os usuários devem receber o novo aplicativo. Faça isso usando a configuração **Data Limite de Instalação** para atualizar usuários com aplicativo substituído.

### <a name="specify-user-experience-settings-for-the-deployment"></a>Especificar as configurações de experiência do usuário para a implantação


Na página **Experiência do Usuário** do Assistente para Implantar Software, especifique as informações sobre como os usuários podem interagir com a instalação do aplicativo.

Ao implantar aplicativos em dispositivos Windows Embedded habilitados com filtro de gravação, você pode especificar que o aplicativo seja instalado na sobreposição temporária e que as alterações devam ser confirmadas mais tarde, no prazo da instalação ou durante uma janela de manutenção. Ao confirmar as alterações na data limite da instalação ou durante uma janela de manutenção, é necessário reiniciar o dispositivo. As alterações permanecem no dispositivo.

>[!NOTE]
    >  Quando você implanta um aplicativo a um dispositivo Windows Embedded, verifique se o dispositivo é um membro de uma coleção com uma janela de manutenção configurada. Para obter mais informações sobre como as janelas de manutenção são usadas ao implantar aplicativos nos dispositivos Windows Embedded, consulte o tópico [Criar aplicativos Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md).

    >  The options **Software Installation** and **System restart (if required to complete the installation)** are not used if the deployment purpose is set to **Available**. You can also configure the level of notification a user sees when the application is installed.

### <a name="specify-alert-options-for-the-deployment"></a>Especificar as opções de alerta para a implantação

Na página **Alertas** do Assistente para Implantar Software, defina como o Configuration Manager e o System Center Operations Manager gerarão alertas para essa implantação. É possível configurar limites para relatar alertas e desativar o relatório para a duração da implantação.

### <a name="associate-the-deployment-with-an-ios-app-configuration-policy"></a>Associar a implantação a uma política de configuração de aplicativo iOS

Na página **Políticas de Configuração de Aplicativo**, clique em **Novo** para associar essa implantação a uma política de configuração de aplicativo iOS (se você tiver criado uma). Para obter mais informações sobre este tipo de política, consulte [Configurar aplicativos do iOS com as políticas de configuração de aplicativo](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).

### <a name="finish-up"></a>Concluir

Na página **Resumo** do Assistente para Implantar Software, examine as ações a serem tomadas por esta implantação e clique em **Avançar** para concluir o assistente.

A nova implantação é exibida na lista **Implantações** no nó **Implantações** no espaço de trabalho **Monitoramento** . É possível editar as propriedades dessa implantação ou excluir a implantação na guia **Implantações** do painel de detalhes do aplicativo.

## <a name="delete-an-application-deployment"></a>Excluir uma implantação de aplicativo

1.  No console do Configuration Manager, vá para **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.

3.  Na lista **Aplicativos**, selecione o aplicativo que inclui a implantação que será excluída.

4.  Na guia **Implantações** da lista *<nome do aplicativo\>*, selecione a implantação do aplicativo que será excluída. Na guia **Implantação**, no grupo **Implantação**, clique em **Excluir**.

 Ao excluir uma implantação de aplicativo, quaisquer instâncias do aplicativo que já foram instaladas não serão removidas. Para remover esses aplicativos, é necessário implantar o aplicativo em computadores com **Desinstalar**. Se você excluir uma implantação de aplicativo ou remover um recurso da coleção na qual está implantando, o aplicativo já não estará visível no Centro de Software.

## <a name="user-notifications-for-required-deployments"></a>Notificações do usuário para implantações necessárias
Quando receber software necessário, na configuração **Suspender e lembrar dentro de**, você pode selecionar na seguinte lista suspensa de valores:
- **Mais tarde** – especifica que as notificações são agendadas com base nas configurações de notificação definidas nas configurações do Agente Cliente.
- **Tempo fixo** – especifica que a notificação será agendada para ser exibida novamente após o tempo selecionado. Por exemplo, se você selecionar 30 minutos, a notificação será exibida novamente em 30 minutos.

![Página do Agente de Computador nas configurações do Agente Cliente](media/ComputerAgentSettings.png)

O tempo máximo de adiamento sempre se baseia nos valores de notificação definidos nas configurações do Agente Cliente em cada ponto na linha do tempo de implantação. Por exemplo, se a configuração **Prazo de implantação superior a 24 horas, lembrar o usuário a cada (horas)** na página do **Agente de Computador** estiver definida como 10 horas e demorar mais de 24 horas até o prazo em que a caixa de diálogo será iniciada, você verá um conjunto de opções de adiamento de até 10 horas, mas nunca superior a esse valor. Conforme o prazo se aproximar, a caixa de diálogo mostrará menos opções, consistentes com as configurações do Agente Cliente relevantes para cada componente da linha do tempo de implantação.

Além disso, para uma implantação de alto risco, como uma sequência de tarefas que implanta um sistema operacional, a experiência de notificação do usuário agora será mais invasiva. Em vez de uma notificação transitória na barra de tarefas, uma caixa de diálogo como a seguinte será exibida no computador cada vez que você for notificado de que uma manutenção de software crítica é necessária:

![Caixa de diálogo Software Exigido](media/client-toast-notification.png)

## <a name="for-more-information"></a>Para obter mais informações:
- [Configurações para gerenciar implantações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Como definir as configurações do cliente](../../core/clients/deploy/configure-client-settings.md)



<!--HONumber=Dec16_HO3-->


