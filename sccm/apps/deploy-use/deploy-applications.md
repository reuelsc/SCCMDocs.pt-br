---
title: Implantar aplicativos | System Center Configuration Manager
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e608bcbadc82487018bb29c5e05660275d8fa275


---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>Implantar aplicativos com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*



 Para poder implantar um aplicativo no System Center Configuration Manager, é necessário criar pelo menos um tipo de implantação para o aplicativo. Para obter mais informações sobre a criação de tipos de implantação e aplicativos, consulte [Criar aplicativos](../../apps/deploy-use/create-applications.md).  

> [!IMPORTANT]  
>  É possível implantar (instalar e desinstalar) aplicativos necessários, mas não pacotes ou atualizações de software. Dispositivos móveis também não têm suporte para implantações simuladas.  
>   
>  Além disso, os dispositivos móveis não oferecem suporte para a experiência do usuário e as configurações de agendamento no Assistente de Implantação de Software.  

 Você também pode simular uma implantação de aplicativo. Esse tipo de implantação testa a aplicabilidade de uma implantação de aplicativo em computadores sem instalar ou desinstalar o aplicativo. Uma implantação simulada avalia o método de detecção, os requisitos e as dependências para um tipo de implantação, e relata os resultados no nó **Implantações** do espaço de trabalho **Monitoramento** . Para mais informações, consulte [Simular implantações de aplicativos](../../apps/deploy-use/simulate-application-deployments.md).  

## <a name="deploy-an-application"></a>Implantar um aplicativo  

1.  No console do Configuration Manager, clique em **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.  

3.  Na lista **Aplicativos** , selecione o aplicativo a implantar. Na guia **Início** , no grupo **Implantação** , clique em **Implantar**.  

4.  Na página **Geral** do Assistente para Implantar Software, especifique as seguintes informações:  

    -   **Software** – exibe o aplicativo a implantar. Você pode clicar em **Procurar** para selecionar um aplicativo diferente.  

    -   **Coleção** – clique em **Procurar** para selecionar a coleção na qual o aplicativo será implantado.  

    -   **Usar grupos de pontos de distribuição padrão associados a esta coleção** – selecione essa opção se quiser armazenar o conteúdo do aplicativo no grupo de pontos de distribuição padrão da coleção. Se você não tiver associado à coleção selecionada a um grupo de pontos de distribuição, essa opção estará indisponível.  

    -   **Distribuir automaticamente conteúdo para dependências** – se habilitada e algum tipo de implantação no aplicativo contém dependências, o conteúdo do aplicativo dependente é também enviado aos pontos de distribuição.  

        > [!IMPORTANT]  
        >  Se você atualizar o aplicativo dependente após a implantação do aplicativo primário, qualquer conteúdo novo para a dependência não é distribuído automaticamente.  

    -   **Comentários (opcional)** – opcionalmente, insira uma descrição dessa implantação.  

5.  Na página **Conteúdo**, clique em **Adicionar** para adicionar o conteúdo que está associado a essa implantação aos pontos de distribuição ou aos grupos de pontos de distribuição. Se você selecionou Usar pontos de distribuição padrão associados a esta coleção na página **Geral**, essa opção será automaticamente populada e poderá ser modificada apenas por um membro da função de segurança **Administrador de Aplicativos**.  

6.  Clique em **Avançar**.  

7.  Na página **Configurações de Implantação** do Assistente para Implantar Software, especifique as seguintes informações:  

    -   **Ação** – na lista suspensa, escolha se essa implantação tem a intenção de **Instalar** ou **Desinstalar** o aplicativo.  

        > [!NOTE]  
        >  Se um aplicativo é implantado duas vezes em um dispositivo, uma vez com a ação de **Instalar** e uma vez com a ação de **Desinstalar**, a implantação do aplicativo com a ação de **Instalar** torna-se prioridade.  
        >   
        >  Não é possível alterar a ação de uma implantação após ela ter sido criada.  

    -   **Finalidade** – na lista suspensa, escolha uma das seguintes opções:  

        -   **Disponível** - Se o aplicativo for implantado em um usuário, o usuário verá o aplicativo publicado no Centro de Software e poderá instalá-lo sob demanda.  

        -   **Necessária** - o aplicativo é implantado automaticamente de acordo com o agendamento configurado. No entanto, um usuário poderá acompanhar o status da implantação do aplicativo se ele não estiver oculto e instalar o aplicativo antes da data limite usando o Centro de Software.  

            > [!NOTE]  
            >  Quando a ação de implantação está definida para **Desinstalar**, a finalidade da implantação é definida automaticamente como **Necessária** e não pode ser alterada.  

    -   **Implantar automaticamente de acordo com o agendamento com ou sem um usuário conectado** – se a implantação é para um usuário, selecione essa opção para implantar o aplicativo aos dispositivos primários do usuário. Esta configuração não requer que o usuário faça logon antes de executar a implantação. Não selecione esta opção se o usuário precisar fornecer uma entrada para concluir a instalação. Essa opção está disponível somente quando a implantação tem a finalidade de **Necessária**.  

    -   **Enviar pacotes de ativação** – se a finalidade da implantação está definida como **Necessária** e essa opção está selecionada, um pacote de ativação é enviado aos computadores antes da implantação ser instalada para ativar o computador da suspensão no prazo da instalação. Para usar essa opção, os computadores e as redes devem ser configurados para Wake on LAN.  

    -   **Permitir que clientes com uma conexão de Internet limitada baixem conteúdo após o prazo de instalação, o que pode gerar em custos adicionais** – essa opção está disponível somente para implantações com a finalidade de **Necessária**.  

    -   **Exigir aprovação do administrador, se os usuários solicitarem este aplicativo** – se essa opção está selecionada, o administrador precisa aprovar quaisquer solicitações do usuário para o aplicativo para que ele possa ser instalado. Essa opção não está disponível quando a finalidade da implantação é **Necessária** ou quando o aplicativo é implantado a uma coleção de dispositivos.  

        > [!NOTE]  
        >  As solicitações de aprovação do aplicativo são exibidas no nó **Solicitações de Aprovação** , no **Gerenciamento de Aplicativos** no espaço de trabalho **Biblioteca de Software** . Se uma solicitação de aprovação não for aprovada dentro de 45 dias, ela será removida. Além disso, reinstalar o cliente do Configuration Manager pode cancelar as solicitações de aprovação pendentes.  

    -   **Atualizar automaticamente qualquer versão substituída deste aplicativo** – se essa opção está selecionada, quaisquer versões substituídas do aplicativo são atualizadas com o aplicativo substituto.  

8.  Na página **Agendamento** do Assistente para Implantar Software, configure quando este aplicativo será implantado ou ficará disponível para os dispositivos cliente.  
    As opções dessa página irão diferir dependendo se a ação de implantação for definida como **Disponível** ou **Obrigatória**.  

9. Se o aplicativo que você está implantando substitui outro aplicativo, você pode configurar o prazo de instalação quando os usuários devem receber o novo aplicativo. Faça isso usando a configuração **Prazo de Instalação** para atualizar usuários com aplicativo substituído.  

10. Na página **Experiência do Usuário** do Assistente para Implantar Software, especifique as informações sobre como os usuários podem interagir com a instalação do aplicativo.
    Ao implantar aplicativos em dispositivos Windows Embedded habilitados com filtro de gravação, você pode especificar que o aplicativo seja instalado na sobreposição temporária e que as alterações devam ser confirmadas mais tarde, no prazo da instalação ou durante uma janela de manutenção. Ao confirmar as alterações na data limite da instalação ou durante uma janela de manutenção, é necessário reinicializar. Dessa forma, as alterações permanecem no dispositivo.  
   > [!NOTE]  
   >  Quando você implanta um aplicativo a um dispositivo Windows Embedded, verifique se o dispositivo é um membro de uma coleção com uma janela de manutenção configurada. Para obter mais informações sobre como as janelas de manutenção são usadas ao implantar aplicativos nos dispositivos Windows Embedded, consulte o tópico [Criar aplicativos Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md).  
   >  As opções **Instalação de software** e **Reinicialização do sistema (se necessário para conclusão da instalação)** não são usadas se a finalidade de implantação está definida como **Disponível**. É possível configurar o nível de notificação que um usuário vê quando o aplicativo está instalado.  
11. Na página **Alertas** do Assistente para Implantar Software, configure como o Configuration Manager e o System Center Operations Manager gerarão alertas para essa implantação. É possível configurar limites para relatar alertas e desativar o relatório para a duração da implantação.  

12. (apenas para aplicativos iOS) – Na página **Políticas de Configuração de Aplicativo**, clique em **Novo** para associar essa implantação a uma política de configuração de aplicativo iOS (se você tiver criado uma). Para obter mais informações sobre este tipo de política, consulte [Configurar aplicativos do iOS com as políticas de configuração de aplicativo](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).  

13. Na página **Resumo** do Assistente para Implantar Software, examine as ações a serem tomadas por esta implantação e clique em **Avançar** para concluir o assistente.  

 A nova implantação é exibida na lista **Implantações** no nó **Implantações** no espaço de trabalho **Monitoramento** . É possível editar as propriedades dessa implantação ou excluir a implantação na guia **Implantações** do painel de detalhes do aplicativo.  

## <a name="delete-an-application-deployment"></a>Excluir uma implantação de aplicativo  

1.  No console do Configuration Manager, clique em **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.  

3.  Na lista **Aplicativos** , selecione o aplicativo para o qual a implantação será excluída.  

4.  Na guia **Implantações** da lista *<nome do aplicativo\>*, selecione a implantação do aplicativo que será excluída. Na guia **Implantação** , no grupo **Implantação** , clique em **Excluir**.  

 Ao excluir uma implantação de aplicativo, quaisquer instâncias do aplicativo que já foram instaladas não serão removidas. Para remover esses aplicativos, é necessário implantar o aplicativo em computadores com a ação de **Desinstalar**. Se você excluir uma implantação de aplicativo ou remover um recurso da coleção na qual está implantando, o aplicativo já não estará visível no Centro de Software.  



<!--HONumber=Nov16_HO1-->


