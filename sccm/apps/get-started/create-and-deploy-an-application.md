---
title: Criar e implantar um aplicativo com | System Center Configuration Manager
description: "Crie e implante um aplicativo que contém um aplicativo de linha de negócios e saiba como gerenciar aplicativos com eficiência."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3bd1e487-ea18-43c1-b7c3-acbd9b86d429
caps.latest.revision: 15
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 12653342e2e311a9bbfc2a7aad3101c0e7f0bce0


---
# <a name="create-and-deploy-an-application-with-system-center-configuration-manager"></a>Criar e implantar um aplicativo com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Neste tópico, você começará imediatamente e criará um aplicativo com o System Center Configuration Manager. Neste exemplo, você criará e implantará um aplicativo que contém um aplicativo de linha de negócios para computadores Windows chamado **Contoso.msi** , o qual deverá ser instalado em todos os computadores que executam Windows 10 em sua empresa. Ao longo do exemplo, você aprenderá várias coisas que você pode fazer para ajudá-lo a gerenciar aplicativos com eficiência.  

 Este procedimento foi desenvolvido para fornecer uma visão geral de como criar e implantar aplicativos do Configuration Manager. No entanto, ele não aborda todas as opções que você pode configurar ou como criar e implantar aplicativos para outras plataformas.  

 Para obter detalhes específicos relevantes para cada plataforma, consulte um dos seguintes tópicos:  

-   [Criar aplicativos do Windows](../../apps/get-started/creating-windows-applications.md)  
-   [Criar aplicativos iOS](../../apps/get-started/creating-ios-applications.md)  
-   [Criar aplicativos Android](../../apps/get-started/creating-android-applications.md)  
-   [Criar aplicativos do Windows Phone](../../apps/get-started/creating-windows-phone-applications.md)  
-   [Criar aplicativos de computador Mac](../../apps/get-started/creating-mac-computer-applications.md)  
-   [Criar aplicativos de servidores Linux e UNIX](../../apps/get-started/creating-linux-and-unix-server-applications.md) 
-   [Criar aplicativos Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md) 

  
Se você já está familiarizado com os aplicativos do Configuration Manager, é possível ignorar este tópico. No entanto, examine [Create applications (Criar aplicativos)](../../apps/deploy-use/create-applications.md) para saber mais sobre todas as opções disponíveis ao criar e implantar aplicativos.  
  
## <a name="before-you-start"></a>Antes de começar  

Assegure-se de que você examinou as informações em [Introdução ao gerenciamento de aplicativos](/sccm/apps/understand/introduction-to-application-management) de modo que tenha preparado o site para instalar aplicativos e que você entendeu a terminologia usada neste tópico.  

 Além disso, verifique se os arquivos de instalação do aplicativo **Contoso.msi** estão em um local acessível na rede.  
  
## <a name="create-the-configuration-manager-application"></a>Criar o aplicativo do Configuration Manager  
  
### <a name="start-the-create-application-wizard-and-create-the-application"></a>Iniciar o assistente para criar aplicativo e criar o aplicativo  
  
1.  No console do Configuration Manager, clique em **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.  
  
3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Aplicativo**.  

4.  Na página **Geral** do **Assistente para Criar Aplicativo**, selecione **Detectar automaticamente informações sobre este aplicativo em arquivos de instalação**. Isso preencherá previamente algumas das informações no assistente com informações extraídas do arquivo .msi de instalação e especificará as seguintes informações:  

    -   **Tipo** – Escolha **Windows Installer (\*.msi file)**  

    -   **Local** - Insira o local (ou clique em **Procurar** para selecionar o local) do arquivo de instalação **Contoso.msi**. Observe que o local deve ser especificado na forma *\\\Servidor\Compartilhamento\Arquivo* para que o Configuration Manager localize os arquivos de instalação.  
  
    Você verá algo semelhante à captura de tela a seguir:  
  
    ![Página geral do assistente de gerenciamento de aplicativos](/sccm/apps/get-started/media/App-management-wizard-general-page.png)  
  
5.  Clique em **Avançar**. Na página **Importar Informações**, você verá algumas informações sobre o aplicativo e quaisquer arquivos associados que foram importados para o Configuration Manager. Quando terminar, clique em **Avançar** novamente.  

6.  Na página **Informações Gerais**, é possível fornecer mais informações sobre o aplicativo que o ajudem a classificá-lo e localizá-lo no console do Configuration Manager.  

     Além disso, o campo Programa de instalação permite especificar a linha de comando completa que será usada para instalar o aplicativo em computadores. Você pode editá-la para adicionar suas próprias propriedades (por exemplo **/q** para uma instalação autônoma).  

    > [!TIP]  
    >  Alguns dos campos nessa assistente podem ter sido preenchidos automaticamente ao importar os arquivos de instalação do aplicativo.  

     Você verá uma tela semelhante à captura de tela a abaixo:  
  
     ![Página de informações gerais do assistente de gerenciamento de aplicativos](/sccm/apps/get-started/media/App-management-wizard-general-information-page.png)  
  
7.  Clique em **Avançar**. Na página Resumo, é possível confirmar as configurações do aplicativo e concluir o assistente.  

 Você acabou de criar o aplicativo. Para encontrá-lo, no espaço de trabalho **Biblioteca de Software** , expanda **Gerenciamento de Aplicativos**e clique em **Aplicativos**. Para este exemplo, você verá:  
  
 ![Gráfico do aplicativo final](/sccm/apps/get-started/media/Final-app-graphic.png)  
  
## <a name="examine-the-properties-of-the-application-and-its-deployment-type"></a>Examinar as propriedades do aplicativo e o tipo de implantação  

Agora que você criou um aplicativo, pode refinar as configurações do aplicativo, se necessário. Para examinar as propriedades do aplicativo, selecione o aplicativo e, na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

 Na caixa de diálogo **Propriedades do Aplicativo <Contoso\>**, você verá muitos itens que podem ser configurados para ajustar o comportamento do aplicativo. Para obter detalhes sobre todas as configurações que é possível definir, consulte [Create applications (Criar aplicativos)](../../apps/deploy-use/create-applications.md). Para os fins deste exemplo, você somente poderá alterar algumas propriedades do tipo de implantação do aplicativo.  
  
 Clique na guia **Tipos de Implantação** , selecione o tipo de implantação **Aplicativo Contoso** e clique em **Editar**.   
Você verá uma caixa de diálogo como esta:  
 
![Página de propriedades do aplicativo de gerenciamento de aplicativos](/sccm/apps/get-started/media/App-management-app-properties-page.png)  
  
## <a name="add-a-requirement-to-the-deployment-type"></a>Adicionar um requisito ao tipo de implantação  
 Os requisitos especificam condições que devem ser atendidas antes de um aplicativo ser instalado em um dispositivo.  Você pode escolher entre requisitos internos ou criar seus próprios. Neste exemplo, você adicionará um requisito que o aplicativo será instalado somente em computadores que executam o Windows 10.  
  
1.  Na página de propriedades de tipo de implantação que você acabou de abrir, clique na guia **Requisitos** .  

2.  Clique em **Adicionar** para abrir a caixa de diálogo **Criar requisito** .  

3.  Na caixa de diálogo **Criar Requisito** , especifique as seguintes informações:  

    -   **Categoria** - **Dispositivo**  

    -   **Condição** - **Sistema operacional**  

    -   **Tipo de regra** - **Valor**  

    -   **Operador** - **Um de**  

    -   Na lista de sistemas operacionais, selecione **Windows 10**.  
  
    Você verá uma caixa de diálogo semelhante a esta:  
  
    ![Página de requisitos de gerenciamento de aplicativos](/sccm/apps/get-started/media/App-management-requirements-page.png)  
  
4.  Clique em **OK** para fechar cada página de propriedades que você abriu e retorne à lista **Aplicativos** no console do Configuration Manager.  

> [!TIP]  
>  Os requisitos podem ajudar a reduzir o número de coleções do Configuration Manager de que você precisa. Como você acabou de especificar que o aplicativo pode ser instalado em computadores que executam o Windows 10, é possível implantar isso mais tarde em uma coleção que contém computadores que executam vários sistemas operacionais diferentes. Assim, o aplicativo será instalado apenas em computadores com Windows 10.  
  
## <a name="add-the-application-content-to-a-distribution-point"></a>Adicionar o conteúdo do aplicativo a um ponto de distribuição  

Para implantar o aplicativo em computadores, em seguida, é necessário garantir que o conteúdo do aplicativo é copiado em um ponto de distribuição. Os computadores acessarão o ponto de distribuição para instalar o aplicativo.  

> [!TIP]  
>  Para obter mais informações sobre pontos de distribuição e gerenciamento de conteúdo no Configuration Manager, consulte [Manage content and content infrastructure (Gerenciar conteúdo e infraestrutura de conteúdo)](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  
  
1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Aplicativos** e, na lista de aplicativos, selecione o **Aplicativo da Contoso** criado.  

3.  Na guia **Início** , no grupo **Implantação** , clique em **Distribuir Conteúdo**.  

4.  Na página **Geral** do **Assistente para Distribuir Conteúdo**, verifique se o nome do aplicativo está correto e clique em **Avançar**.  

5.  Na página **Conteúdo** , examine as informações que serão copiadas no ponto de distribuição e clique em **Avançar**.  

6.  Na página **Destino do Conteúdo** , clique em Adicionar para selecionar um ou mais pontos de distribuição ou grupos de pontos de distribuição nos quais será instalado o conteúdo do aplicativo.  

7.  Conclua o assistente.  

 É possível verificar se o conteúdo do aplicativo foi copiado com êxito no ponto de distribuição no espaço de trabalho **Monitoramento** sob **Status de Distribuição** > **Status do Conteúdo**.  
  
## <a name="deploy-the-application"></a>Implantar o aplicativo  

Em seguida, implante o aplicativo em uma coleção de dispositivos de sua hierarquia. Para este exemplo, você implantará o aplicativo na coleção de dispositivos **Todos os Sistemas** .  

> [!TIP]  
>  Lembre-se de que somente os computadores com Windows 10 instalarão o aplicativo, devido aos requisitos selecionados anteriormente.  
  
1.  No console do Configuration Manager, clique em **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.  
  
3.  Na lista de aplicativos, selecione o aplicativo criado anteriormente, **Aplicativo da Contoso**e, na guia **Início** , no grupo **Implantação** , clique em **Implantar**.  

4.  Na página **Geral** do **Assistente de Implantação de Software**, clique em **Procurar** para selecionar a coleção de dispositivos **Todos os Sistemas** .  

5.  Na página **Conteúdo**, verifique se o ponto de distribuição do qual você deseja que os computadores instalem o aplicativo foi selecionado.  

6.  Na página **Configurações de Implantação**, certifique-se de que a ação de implantação foi definida como **Instalar** e que a finalidade da implantação foi definida como **Necessária**.  

    > [!TIP]  
    >  Ao definir a finalidade da implantação como **Necessária**, você garante que o aplicativo é instalado em computadores que atendem aos requisitos definidos. Se você definir esse valor como **Disponível**, os usuários poderão instalar o aplicativo sob demanda no Centro de Software.  

7.  Na página **Agendamento** , é possível configurar a data em que o aplicativo será instalado. Para este exemplo, selecione **Logo que possível após o tempo disponível**.  

8.  Na página **Experiência do Usuário**, clique em **Avançar** para aceitar os valores padrão.  

9. Conclua o assistente.  

 Use as informações na seção **Monitorar o aplicativo** abaixo para ver o status da implantação de seu aplicativo.  
  
## <a name="monitor-the-application"></a>Monitorar o aplicativo  
 Nesta seção, você terá uma visão rápida do status da implantação do aplicativo que acabou de ser implantado.  
  
### <a name="to-review-the-deployment-status"></a>Para examinar o status da implantação  
  
1.  No console do Configuration Manager, clique em **Monitoramento** > **Implantações**.  
  
3.  Na lista de implantações, selecione **Aplicativo da Contoso**.  

4.  Na guia **Início** , no grupo **Implantação** , clique em **Exibir Status**.  

5.  Selecione uma das seguintes guias para ver mais status sobre a implantação do aplicativo:  

    -   **Sucesso** - O aplicativo foi instalado com êxito nos computadores indicados.  

    -   **Em Andamento** - A instalação do aplicativo ainda não foi concluída.  

    -   **Erro** - Ocorreu um erro ao instalar o aplicativo nos computadores indicados. Informações adicionais sobre o erro também são exibidas.  

    -   **Requisitos Não Atendidos** - Não houve tentativa de instalar o aplicativo nos dispositivos indicados porque eles não atenderam aos requisitos configurados (neste exemplo, já que eles não executam o Windows 10).  

    -   **Desconhecido** – o Configuration Manager não conseguiu relatar o status da implantação. Verifique novamente mais tarde.  

> [!TIP]  
>  Há várias maneiras pelas quais você pode monitorar implantações de aplicativos. Para obter detalhes completos, consulte [Monitorar aplicativos](/sccm/apps/deploy-use/monitor-applications-from-the-console).  
  
## <a name="end-user-experience"></a>Experiência do usuário final  

Os usuários que têm computadores que executam o Windows 10 gerenciados pelo Configuration Manager verão uma mensagem informando que eles devem instalar o aplicativo da Contoso. Depois de aceitar a instalação, o aplicativo será instalado.  



<!--HONumber=Nov16_HO1-->


