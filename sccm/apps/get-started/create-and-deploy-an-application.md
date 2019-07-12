---
title: Criar e implantar um aplicativo
titleSuffix: Configuration Manager
description: Crie e implante um aplicativo que contém um aplicativo de linha de negócios e saiba como gerenciar aplicativos com eficiência.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 3bd1e487-ea18-43c1-b7c3-acbd9b86d429
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 979409f34e4c32ce812f2a84ce062d2312a85d3c
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67676132"
---
# <a name="create-and-deploy-an-application-with-system-center-configuration-manager"></a>Criar e implantar um aplicativo com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Neste tópico, você começará imediatamente e criará um aplicativo com o System Center Configuration Manager. Neste exemplo, você criará e implantará um aplicativo que contém um aplicativo de linha de negócios para computadores Windows chamado **Contoso.msi**, que deverá ser instalado em todos os computadores que executam Windows 10 em sua empresa. Ao longo do exemplo, você aprenderá várias coisas que você pode fazer para gerenciar aplicativos com eficiência.  

 Este procedimento foi desenvolvido para fornecer uma visão geral de como criar e implantar aplicativos do Configuration Manager. No entanto, ele não aborda todas as opções de configuração ou como criar e implantar aplicativos para outras plataformas.  

 Para obter detalhes específicos que sejam relevantes para cada plataforma, consulte um dos seguintes tópicos:  

-   [Criar aplicativos do Windows](../../apps/get-started/creating-windows-applications.md)  
-   [Criar aplicativos iOS](../../apps/get-started/creating-ios-applications.md)  
-   [Criar aplicativos Android](../../apps/get-started/creating-android-applications.md)  
-   [Criar aplicativos do Windows Phone](../../apps/get-started/creating-windows-phone-applications.md)  
-   [Criar aplicativos de computador Mac](../../apps/get-started/creating-mac-computer-applications.md)  
-   [Criar aplicativos de servidores Linux e UNIX](../../apps/get-started/creating-linux-and-unix-server-applications.md)
-   [Criar aplicativos Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md)


Se você já está familiarizado com os aplicativos do Configuration Manager, é possível ignorar este tópico. No entanto, talvez você queira examinar [Criar aplicativos](../../apps/deploy-use/create-applications.md) para saber mais sobre todas as opções que estão disponíveis ao criar e implantar aplicativos.  

## <a name="before-you-start"></a>Antes de começar  

Verifique se você conferiu as informações em [Introdução ao gerenciamento de aplicativos](/sccm/apps/understand/introduction-to-application-management) para preparar seu site para instalar aplicativos e entender a terminologia usada neste tópico.  

 Além disso, verifique se os arquivos de instalação do aplicativo **Contoso.msi** estão em um local acessível na rede.  

## <a name="create-the-configuration-manager-application"></a>Criar o aplicativo do Configuration Manager  

### <a name="to-start-the-create-application-wizard-and-create-the-application"></a>Iniciar o Assistente para Criar aplicativo e criar o aplicativo  

1. No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.  

2. Na guia **Início**, no grupo **Criar**, escolha **Criar Aplicativo**.  

3. Na página **Geral** do **Assistente para Criar Aplicativo**, selecione **Detectar automaticamente informações sobre este aplicativo em arquivos de instalação**. Isso preenche previamente algumas das informações no assistente com informações que são extraídas do arquivo de instalação .msi. Em seguida, especifique as seguintes informações:  

   -   **Tipo**: escolha **Windows Installer (\*arquivo .msi)** .  

   -   **Local**: digite o local (ou escolha **Procurar** para selecionar o local) do arquivo de instalação **Contoso.msi**. Observe que o local deve ser especificado na forma *\\\Server\Share\File* para que o Configuration Manager localize os arquivos de instalação.  

   Você verá algo semelhante à captura de tela a seguir:  

   ![Página geral do assistente de gerenciamento de aplicativos](/sccm/apps/get-started/media/App-management-wizard-general-page.png)  

4. Escolha **Próxima**. Na página **Importar Informações**, você verá algumas informações sobre o aplicativo e quaisquer arquivos associados que foram importados para o Configuration Manager. Quando terminar, escolha **Avançar** novamente.  

5. Na página **Informações Gerais**, é possível fornecer mais informações sobre o aplicativo que o ajudem a classificá-lo e localizá-lo no console do Configuration Manager.  

    Além disso, o campo **Programa de instalação** permite especificar a linha de comando completa que será usada para instalar o aplicativo nos computadores. Você pode editá-la para adicionar suas próprias propriedades (por exemplo **/q** para uma instalação autônoma).  

   > [!TIP]  
   >  Alguns dos campos nessa assistente podem ter sido preenchidos automaticamente ao importar os arquivos de instalação do aplicativo.  

    Você verá uma tela semelhante à captura de tela a seguir:  

    ![Página de informações gerais do assistente de gerenciamento de aplicativos](/sccm/apps/get-started/media/App-management-wizard-general-information-page.png)  

6. Escolha **Próxima**. Na página Resumo, é possível confirmar as configurações do aplicativo e concluir o assistente.  

   Você acabou de criar o aplicativo. Para encontrá-lo, no workspace **Biblioteca de Software**, expanda o **Gerenciamento de Aplicativos**e escolha **Aplicativos**. Para este exemplo, você verá:  

   ![Gráfico do aplicativo final](/sccm/apps/get-started/media/Final-app-graphic.png)  

## <a name="examine-the-properties-of-the-application-and-its-deployment-type"></a>Examinar as propriedades do aplicativo e o tipo de implantação  

Agora que você criou um aplicativo, é possível refinar as configurações do aplicativo, se necessário. Para examinar as propriedades do aplicativo, selecione o aplicativo e, na guia **Início**, no grupo **Propriedades**, escolha **Propriedades**.  

 Na caixa de diálogo **Propriedades do Aplicativo <Contoso\>** , você verá muitos itens que podem ser configurados para refinar o comportamento do aplicativo. Para obter detalhes sobre todas as configurações que é possível definir, consulte [Create applications (Criar aplicativos)](../../apps/deploy-use/create-applications.md). Para os fins deste exemplo, você somente poderá alterar algumas propriedades do tipo de implantação do aplicativo.  

 Escolha a guia **Tipos de Implantação** > **Aplicativo Contoso** Tipo de Implantação > **Editar**. 

Você verá uma caixa de diálogo como esta:  

![Página de propriedades do aplicativo de gerenciamento de aplicativos](/sccm/apps/get-started/media/App-management-app-properties-page.png)  

## <a name="add-a-requirement-to-the-deployment-type"></a>Adicionar um requisito ao tipo de implantação  
 Os requisitos especificam condições que devem ser atendidas antes de um aplicativo ser instalado em um dispositivo.  Você pode escolher entre os requisitos internos ou pode criar os seus próprios. Neste exemplo, você adiciona um requisito em que o aplicativo será instalado somente em computadores que executam o Windows 10.  

1.  Na página de propriedades de tipo de implantação que você acabou de abrir, escolha a guia **Requisitos**.  

2.  Escolha **Adicionar** para abrir a caixa de diálogo **Criar requisito**.  

3.  Na caixa de diálogo **Criar Requisito** , especifique as seguintes informações:  

    -   **Categoria**: **Dispositivo**  

    -   **Condição**: **Sistema operacional**  

    -   **Tipo de regra**: **Valor**  

    -   **Operador**: **Um de**  

    -   Na lista de sistemas operacionais, selecione **Windows 10**.  

    Você verá uma caixa de diálogo semelhante a esta:  

    ![Página de requisitos de gerenciamento de aplicativos](/sccm/apps/get-started/media/App-management-requirements-page.png)  

4.  Escolha **OK** para fechar cada página de propriedades que você abriu. Em seguida, volte para a lista **Aplicativos** no console do Configuration Manager.  

> [!TIP]  
>  Os requisitos podem ajudar a reduzir o número de coleções do Configuration Manager de que você precisa. Como você acabou de especificar que o aplicativo só pode ser instalado em computadores que executam o Windows 10, é possível implantar isso mais tarde em uma coleção que contém computadores que executam vários sistemas operacionais diferentes. Mas o aplicativo será instalado apenas em PCs com Windows 10.  

## <a name="add-the-application-content-to-a-distribution-point"></a>Adicionar o conteúdo do aplicativo a um ponto de distribuição  

Em seguida, para implantar o aplicativo em computadores, é necessário garantir que o conteúdo do aplicativo seja copiado para um ponto de distribuição. Os computadores acessam o ponto de distribuição para instalar o aplicativo.  

> [!TIP]  
>  Para obter mais informações sobre pontos de distribuição e gerenciamento de conteúdo no Configuration Manager, consulte [Manage content and content infrastructure (Gerenciar conteúdo e infraestrutura de conteúdo)](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

1.  No console do Configuration Manager, escolha **Biblioteca de Software**.  

2.  No workspace **Biblioteca de Software**, expanda **Aplicativos**. Em seguida, na lista de aplicativos, selecione o **Aplicativo Contoso** que você criou.  

3.  Na guia **Início**, no grupo **Implantação**, escolha **Distribuir Conteúdo**.  

4.  Na página **Geral** do **Assistente para Distribuir Conteúdo**, verifique se o nome do aplicativo está correto e escolha **Avançar**.  

5.  Na página **Conteúdo**, examine as informações que serão copiadas para o ponto de distribuição e escolha **Avançar**.  

6.  Na página **Destino do Conteúdo**, escolha **Adicionar** para selecionar um ou mais pontos de distribuição ou grupos de pontos de distribuição nos quais será instalado o conteúdo do aplicativo.  

7.  Conclua o assistente.  

É possível verificar se o conteúdo do aplicativo foi copiado com êxito no ponto de distribuição no workspace **Monitoramento** em **Status de Distribuição** > **Status do Conteúdo**.  

## <a name="deploy-the-application"></a>Implantar o aplicativo  

Em seguida, implante o aplicativo em uma coleção de dispositivos de sua hierarquia. Neste exemplo, você implanta o aplicativo na coleção de dispositivos **Todos os Sistemas**.  

> [!TIP]  
>  Lembre-se de que somente os computadores com Windows 10 instalarão o aplicativo, devido aos requisitos selecionados anteriormente.  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.  

3.  Na lista de aplicativos, selecione o aplicativo criado anteriormente, (**Aplicativo Contoso**) e, na guia **Início**, no grupo **Implantação**, clique em **Implantar**.  

4.  Na página **Geral** do **Assistente de Implantação de Software**, escolha **Procurar** para selecionar a coleção de dispositivos **Todos os Sistemas**.  

5.  Na página **Conteúdo**, verifique se o ponto de distribuição do qual você deseja que os computadores instalem o aplicativo foi selecionado.  

6.  Na página **Configurações de Implantação**, certifique-se de que a ação de implantação foi definida como **Instalar** e que a finalidade da implantação foi definida como **Necessária**.  

    > [!TIP]  
    >  Ao definir a finalidade da implantação como **Necessária**, você garante que o aplicativo é instalado em computadores que atendam aos requisitos definidos. Se você definir esse valor como **Disponível**, os usuários poderão instalar o aplicativo sob demanda no Centro de Software.  

7.  Na página **Agendamento** , é possível configurar a data em que o aplicativo será instalado. Para este exemplo, selecione **Logo que possível após o tempo disponível**.  

8.  Na página **Experiência do Usuário**, escolha **Avançar** para aceitar os valores padrão.  

9. Conclua o assistente.  

Use as informações na seção a seguir **Monitorar o aplicativo** para ver o status da implantação de seu aplicativo.  

## <a name="monitor-the-application"></a>Monitorar o aplicativo  
 Nesta seção, você terá uma visão rápida do status da implantação do aplicativo que acabou de ser implantado.  

### <a name="to-review-the-deployment-status"></a>Para examinar o status da implantação  

1.  No console do Configuration Manager, escolha **Monitoramento** > **Implantações**.  

3.  Na lista de implantações, selecione **Aplicativo da Contoso**.  

4.  Na guia **Início**, no grupo **Implantação**, escolha **Exibir Status**.  

5.  Selecione uma das seguintes guias para ver mais atualizações de status sobre a implantação do aplicativo:  

    -   **Sucesso**: o aplicativo foi instalado com êxito nos computadores indicados.  

    -   **Em Andamento**: a instalação do aplicativo ainda não foi concluída.  

    -   **Erro**: ocorreu um erro ao instalar o aplicativo nos computadores indicados. Informações adicionais sobre o erro também são exibidas.  

    -   **Requisitos Não Atendidos**: Não houve tentativa de instalar o aplicativo nos dispositivos indicados porque eles não atenderam aos requisitos configurados (neste exemplo, pois eles não são executados no Windows 10).  

    -   **Desconhecido**: o Configuration Manager não conseguiu relatar o status da implantação. Verifique novamente mais tarde.  

> [!TIP]  
>  Há várias maneiras pelas quais você pode monitorar implantações de aplicativos. Para obter detalhes completos, consulte [Monitorar aplicativos](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

## <a name="end-user-experience"></a>Experiência do usuário final  

Os usuários que têm computadores gerenciados pelo Configuration Manager e executam o Windows 10 verão uma mensagem informando que eles devem instalar o aplicativo da Contoso. Depois de aceitar a instalação, o aplicativo é instalado.  
