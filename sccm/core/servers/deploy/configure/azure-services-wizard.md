---
title: "Assistente para serviços do Azure | Microsoft Docs"
description: "Sobre o assistente para serviços do Azure para System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 0663ba84762c44a5c303562548499f195bae9e1c
ms.openlocfilehash: 22203b358830903cf2e531c0532ae3111b8265fc
ms.contentlocale: pt-br
ms.lasthandoff: 08/01/2017

---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configurar serviços do Azure para uso com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A partir da versão 1706 do Branch Atual, o **Assistente para Serviços do Azure** é usado para simplificar o processo de configuração de serviços do Azure que você usa com o Configuration Manager.

Este assistente fornece uma experiência de configuração comum usando um **aplicativo Web do Azure** para fornecer detalhes de assinatura e configuração. O aplicativo Web substitui a necessidade de inserir essas mesmas informações cada vez que você configurar um novo componente ou serviço do Configuration Manager com o Azure.

Os serviços do Azure a seguir são configurados usando o Assistente para Configurar Serviços do Azure:
-   **Gerenciamento de Nuvem**   
    [Permite que os clientes autentiquem usando o Azure Active Directory]() (Azure AD). Você também pode [configurar a Descoberta de Usuário do Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc).
-   **Conector do OMS**
    [ Conecte-se ao OMS (Operations Manager Suite)](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) e sincronize dados como coleções com o OMS Log Analytics.
-   **Upgrade Readiness**
    [ Conecte-se ao Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) e exiba dados de compatibilidade de atualização do cliente.
-   **Windows Store para Empresas** Conecte-se ao repositório online do [Windows Store para Empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) e obtenha aplicativos para a sua organização que podem ser implantados com o Configuration Manager.

Quando você usa o assistente para configurar um serviço, várias ações comuns ficam disponíveis.
Elas incluem:
-   Configurar o ambiente do Azure: na página **Aplicativo** do assistente, selecione o **ambiente Azure** que você usa. Confira o conteúdo de cada serviço para saber se ele dá suporte apenas à nuvem pública do Azure, ou se ele pode dar suporte a uma nuvem privada.
-   Criar ou Importar um aplicativo de servidor: na página **Aplicativo** do assistente, você pode **Criar** e **Importar** aplicativos Web do Azure. As opções disponíveis dependem do serviço que você está configurando.  Além disso, alguns serviços podem exigir um aplicativo adicional. Por exemplo, um serviço também pode exigir um **aplicativo Cliente Nativo**.


Para saber mais sobre os aplicativos Web do Azure, confira [Autenticação e autorização no serviço de aplicativo do Azure](/azure/app-service/app-service-authentication-overview) e [Visão geral de aplicativos Web](/azure/app-service-web/app-service-web-overview)


## <a name="webapp"></a> Criar o aplicativo Web do Azure para uso com o Configuration Manager

O aplicativo Web de serviços do Azure conecta seu site do Configuration Manager ao Azure AD e é um pré-requisito para usar os serviços do Azure com sua infraestrutura. Para fazer isso:

1.  No espaço de trabalho **Administração** do console do Configuration Manager, expanda **Serviços de Nuvem** e clique em **Serviços do Azure**.
2.  Na guia **Página Inicial**, no grupo **Serviços do Azure**, clique em **Configurar os Serviços do Azure**.
3.  Na página **Serviços do Azure** do Assistente de Serviços do Azure, selecione **Gerenciamento de Nuvem** para permitir que os clientes sejam autenticados com a hierarquia usando o Azure AD.
4.  Na página **Geral** do assistente, especifique um nome e uma descrição para o serviço do Azure.
5.  Na página **Aplicativo** do assistente, selecione o seu ambiente do Azure na lista, clique em **Procurar** para selecionar o *aplicativo Web* e o *aplicativo de Cliente Nativo* que serão usados para configurar o serviço do Azure.     
    **Aplicativo Web:** Procurar abre a janela do Aplicativo de Servidor.    
      Na janela do **aplicativo de servidor**, selecione o aplicativo de servidor que você deseja usar e depois clique em **OK**. Aplicativos de servidor são os aplicativos Web do Azure que contêm as configurações da sua conta do Azure, incluindo sua ID de locatário, ID de cliente e uma chave secreta para clientes.
    Se você não tiver um aplicativo disponível, use um dos seguintes:
        - **Criar**: Para criar um novo aplicativo de servidor, clique em **Criar**. Em seguida, forneça um nome amigável para o aplicativo, a URL da home page, o URI da ID do Aplicativo e o período de validade da Chave secreta. Por padrão, o período de validade da chave secreta é de um ano.

         Para continuar, agora alguém deve entrar no Azure para concluir a criação do aplicativo Web no Azure. A conta que você usa para entrar no Azure não precisa ser a mesma conta que executa o Assistente para Serviços do Azure. Depois de entrar no Azure, o Configuration Manager cria o aplicativo Web no Azure para você, incluindo a ID do Cliente e a chave secreta para uso com o aplicativo Web. Posteriormente, você pode exibi-las no portal do Azure.

         Quando você usar Criar para configurar um aplicativo Web, o Configuration Manager pode criar o aplicativo Web para você no Azure AD.
        - **Importar**: Para usar um aplicativo Web que já existe em sua assinatura do Azure, clique em **Importar**. Forneça um nome amigável para o aplicativo e o locatário e especifique a ID de locatário, ID do cliente e a chave secreta para o aplicativo Web do Azure que você deseja que o Configuration Manager use. Depois que você verificar as informações, clique em **OK** para continuar.

          Essa opção não está disponível para todos os serviços que você pode configurar.

   **Aplicativo Cliente Nativo:** Procurar abre a janela Aplicativo Cliente.  
     Na janela do **Aplicativo Cliente**, selecione o aplicativo cliente que você deseja usar e depois clique em **OK**.

     Se você não tiver um aplicativo cliente disponível, use um dos seguintes:
     - **Criar**: para criar um novo Aplicativo Cliente, clique em **Criar**. Depois, forneça um nome amigável para o aplicativo e a URL de Resposta.

          Para continuar, agora alguém deve entrar no Azure para concluir a criação do aplicativo cliente no Azure. A conta que você usa para entrar no Azure não precisa ser a mesma conta que executa o Assistente para Serviços do Azure. Depois de entrar no Azure, o Configuration Manager cria o aplicativo cliente no Azure para você, incluindo a ID do Cliente para uso com o aplicativo Web. Posteriormente, você pode exibi-las no portal do Azure.
          Quando você usar Criar para configurar o aplicativo, o Configuration Manager pode criar o aplicativo cliente nativo para você no Azure AD.
     - **Importar**: para usar um aplicativo cliente que já existe em sua assinatura do Azure, clique em **Importar**. Forneça um nome amigável para o aplicativo e a ID do Cliente. Depois, clique em **OK** para continuar.
           Essa opção não está disponível para todos os serviços que você pode configurar.

  <!--  MOVE THIS AND STEP 6 TO configure Azure AD User Discover  content
       [!TIP]  
     When you use Import, the account you use to run the wizard must have the *Read directory data* application permission in the Azure portal. This is required to set the correct permissions for the App. When you use Create, Configuration Manager creates the app with the correct permissions. However, you still must give consent to the application in the Azure portal.   -->


6.  Na página **Descoberta** do assistente, clique em **Ativar a Descoberta de Usuário do Azure Active Directory** e, em seguida, clique em **Configurações**.
Na caixa de diálogo **Configurações de Descoberta de Usuário do Azure AD**, configure um agendamento para quando ocorrer a descoberta. Você também pode habilitar a descoberta delta que verifica apenas as contas novas ou alteradas no Azure AD. Saiba mais sobre [Descoberta de usuário do Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).
 
 7. Conclua o assistente.

Neste ponto, você se conectou a seu site do Configuration Manager para o Azure AD.

## <a name="view-the-configuration-of-an-azure-service"></a>Exibir a configuração de um serviço do Azure
Você pode exibir as propriedades de um serviço do Azure que você configurou para uso.

No console, acesse **Administração** > **Visão geral** > **Serviços de Nuvem** > **Serviços do Azure**. Em seguida, escolha o serviço que você deseja exibir ou editar e clique em **Propriedades**.

