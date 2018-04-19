---
title: Gerenciar o acesso do SharePoint Online
titleSuffix: Configuration Manager
description: Saiba como usar a política de acesso condicional do SharePoint Online no System Center Configuration Manager para gerenciar o acesso ao OneDrive.
ms.custom: na
ms.date: 12/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49cec466-1676-4fe2-a2fe-5004f01d735e
caps.latest.revision: 11
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: ac696941e701dd5d42500b2811bec136e64a28fe
ms.sourcegitcommit: a19e12d5c3198764901d44f4df7c60eb542e765f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="manage-sharepoint-online-access-in-system-center-configuration-manager"></a>Gerenciar o acesso ao SharePoint Online no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


A política de acesso condicional do Configuration Manager para **SharePoint Online** gerencia o acesso ao OneDrive para arquivos comerciais, que são armazenados no SharePoint Online. O acesso é baseado nas condições especificadas.
Você pode controlar o acesso ao SharePoint Online dos aplicativos para as plataformas listadas a seguir:  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android e iOS)  

-   Microsoft Word (Android e iOS)  

-   Microsoft Excel (Android e iOS)  

-   Microsoft PowerPoint (Android e iOS)  

-   Microsoft OneNote (Android e iOS)

Os aplicativos de área de trabalho do Office podem acessar o SharePoint Online em computadores que executam:  

-   Área de trabalho do Office 2013 e posterior com [autenticação moderna](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) habilitada.  

-   Windows 7.0 ou Windows 8.1  

> [!NOTE]  
>  Os computadores devem ser ingressados no domínio ou ser compatíveis com as políticas definidas no Intune.  



 Quando um determinado usuário tenta se conectar a um arquivo usando um aplicativo com suporte assim como o OneDrive em seu dispositivo, ocorre a seguinte avaliação:  

 ![ConditionalAccess8&#45;6](media/ConditionalAccess8-6.png)  

 Para conectar-se aos arquivos necessários, o dispositivo que executa o OneDrive deve:  

-   Estar registrado no Microsoft Intune ou em um computador ingressado no domínio.  

-   Registre o dispositivo no Azure AD (Azure Active Directory). Esse registro ocorre automaticamente quando o dispositivo é registrado com o Intune.  

     Para computadores ingressados no domínio, você deve configurá-los para se [registrarem automaticamente](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) com o Azure AD.  

-   Ser compatível com todas as políticas de conformidade do Configuration Manager implantadas  

    O Azure AD armazena o estado do dispositivo. Ele concede ou bloqueia o acesso a arquivos, com base nas condições especificadas.  

    Se uma condição não for atendida, o usuário receberá uma das seguintes mensagens de erro ao fazer logon:  

-   Se o dispositivo não estiver registrado com o Intune ou não estiver registrado no Azure AD, será exibida uma mensagem com instruções sobre como instalar o aplicativo de Portal da Empresa e registrá-lo.  

-   Se o dispositivo não estiver em conformidade, será exibida uma mensagem que direciona o usuário para o portal da Web do Intune. Lá, ele pode encontrar informações sobre o problema e como corrigi-lo.  

- Para dispositivos móveis:

  Você pode restringir o acesso ao SharePoint Online quando o acesso é feito por meio de um navegador em dispositivos **iOS** e **Android**. O acesso é permitido somente de navegadores com suporte em dispositivos em conformidade:  
    - Safari (iOS)
    - Chrome (Android)
    - Navegador gerenciado (iOS e Android)  

    Navegadores incompatíveis são bloqueados.  

-   Para um PC:  


    -   Se a política estiver definida para exigir o ingresso no domínio e o PC não tiver ingressado no domínio, uma mensagem será exibida para que o usuário entre em contato com o administrador de TI.  

    -   Se a política estiver definida para exigir ingresso no domínio ou conformidade e o PC não atender a nenhum dos dois requisitos, será exibida uma mensagem com instruções sobre como instalar o aplicativo do Portal da Empresa e realizar o registro.  

É possível bloquear o acesso ao SharePoint Online por meio dos seguintes aplicativos:  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android e iOS)  

-   Microsoft Word (Android e iOS)  

-   Microsoft Excel (Android e iOS)  

-   Microsoft PowerPoint (Android e iOS)  

-   Microsoft OneNote (Android e iOS)  



## <a name="configure-conditional-access-for-sharepoint-online"></a>Configurar o acesso condicional para o SharePoint Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Etapa 1: Configurar grupos de segurança do Active Directory  
 Antes de começar, configure grupos de segurança do Azure AD para a política de acesso condicional. Você pode configurar esses grupos no **Centro de administração do Office 365**ou no **Portal de conta do Intune**. Esses grupos incluem os usuários que são afetados ou que ficarão isentos da política. Quando um usuário é afetado por uma política, cada dispositivo que ele usa deve ser compatível para que possa acessar os recursos.  

 Você pode especificar dois tipos de grupo em uma política do SharePoint Online:  

-   **Grupos de destino**: contém grupos de usuários aos quais a política se aplica  

-   **Grupos isentos**: contém grupos de usuários isentos da política (opcional)  

 Se um usuário estiver nos dois grupos, ele ficará isento da política.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Etapa 2: Configurar e implantar uma política de conformidade  
 Crie e implante uma política de conformidade para todos os dispositivos aos quais a política do SharePoint Online é direcionada.  

> [!NOTE]   
>  Enquanto as políticas de conformidade são implantadas em grupos do Intune, ou em coleções do Configuration Manager, as políticas de acesso condicional destinam-se aos grupos de segurança do Azure AD.  

 Para obter detalhes sobre como configurar a política de conformidade, consulte [Gerenciar políticas de conformidade do dispositivo no System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md).  

> [!IMPORTANT]  
>  Se você ainda não tiver implantado uma política de conformidade e habilitado a política do SharePoint Online, todos os dispositivos de destino poderão acessar.  

   

###  <a name="BKMK_OneDrive"></a> Etapa 3: Configurar a política do SharePoint Online  

 Em seguida, configure a política para exigir que somente dispositivos gerenciados e em conformidade possam acessar o SharePoint Online. Essa política é armazenada no Azure AD.

 >[!NOTE]
 >Você também pode criar a política de acesso condicional no console de gerenciamento do Azure AD. O console de gerenciamento do Azure AD permite que você crie políticas de acesso condicional do dispositivo do Intune. O Azure AD se refere a essas políticas como política de acesso condicional baseada em dispositivo. Você também pode criar outras políticas de acesso condicional, como autenticação multifator. No portal, você pode definir políticas de acesso condicional para aplicativos corporativos de terceiros com suporte pelo Azure AD, como o Salesforce e o Box. Para obter mais detalhes, consulte [Como definir a política de acesso condicional com base no dispositivo do Azure Active Directory para controle de acesso dos aplicativos conectados no Azure AD](/azure/active-directory/active-directory-conditional-access-policy-connected-applications).  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  Selecione **Habilitar política de acesso condicional para o SharePoint Online**.  

     ![IntuneSASharePointOnlineCAPolicy](media/IntuneSASharePointOnlineCAPolicy.png)  

3.  Em **Acesso do aplicativo** para o Outlook e aplicativos que usam autenticação moderna, você pode optar por restringir o acesso apenas para dispositivos compatíveis para cada plataforma.  

    > [!TIP]  
    >  **Autenticação moderna** traz a entrada baseada no ADAL (Active Directory Authentication Library) para clientes Office.  
    >   
    >  -   A autenticação com base em ADAL permite que os clientes Office participem de autenticação baseada em navegador (também conhecida como autenticação passiva). Para autenticar, o usuário é direcionado a uma página da Web de entrada.  
    > -   Esse novo método de entrada permite novos cenários, como acesso condicional, com base em **conformidade do dispositivo** e se a **autenticação multifator** foi executada.  
    >   
    >  Para obter mais informações, consulte [Como a autenticação moderna funciona para aplicativos de cliente do Office 2013 e Office 2016](https://support.office.com/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517).  

     Para computadores Windows, este deve estar ingressado no domínio ou então ser registrado no Intune e ser compatível. Você pode definir os seguintes requisitos:  

    -   **Os dispositivos devem estar em conformidade ou ingressados no domínio**: os computadores devem estar em conformidade ou estar ingressados no domínio com as políticas definidas no Intune. Se o computador não atender a esses requisitos, será solicitado que o usuário registre o dispositivo no Intune.  

    -   **Os dispositivos devem estar ingressados no domínio**: os computadores devem estar ingressados no domínio para acessar o Exchange Online. Se o PC não estiver ingressado no domínio, o acesso ao email será bloqueado e será solicitado que o usuário entre em contato com o administrador de TI.  

    -   **Os dispositivos devem estar em conformidade**: os computadores devem estar registrados no Intune e em conformidade. Se o computador não estiver registrado, será exibida uma mensagem com instruções sobre como registrá-lo.  

4.  Em **Acesso do navegador** para o SharePoint Online e o OneDrive for Business, você pode optar por permitir o acesso somente ao Exchange Online por meio dos navegadores com suporte: Safari (iOS) e Chrome (Android). O acesso de outros navegadores será bloqueado. As mesmas restrições de plataforma selecionadas para Acesso do aplicativo para o OneDrive também se aplicarão aqui.

    Em dispositivos **Android**, os usuários devem habilitar a opção **Habilitar o Acesso do Navegador** no dispositivo registrado, da seguinte maneira:
    1.  Inicie o **aplicativo do Portal da Empresa**.
    2.  Vá para a página **Configurações** por meio dos três pontos (...) ou do botão de menu do hardware.
    3.  Pressione o botão **Habilitar o Acesso do Navegador** .
    4.  No navegador Chrome, saia do Office 365 e reinicie o Chrome.

    Em plataformas **iOS e Android**, para identificar o dispositivo que é usado para acessar o serviço, o Azure AD emite um certificado TLS para o dispositivo. O dispositivo exibe o certificado com um prompt para o usuário final para selecionar o certificado conforme visto nas capturas de tela seguir: O usuário final deve selecionar este certificado antes que eles podem continuar a usar o navegador.

     **iOS**

     ![captura de tela do prompt do certificado em um iPad](media/mdm-browser-ca-ios-cert-prompt_v2.png)

     **Android**

      ![captura de tela do prompt do certificado em um dispositivo Android](media/mdm-browser-ca-android-cert-prompt.png)

4.  Na guia **Início** , no grupo **Links** , clique em **Configurar Política de Acesso Condicional no Console do Intune**. Talvez seja necessário fornecer o nome de usuário e a senha da conta usada para conectar o Configuration Manager ao Intune.  

     O console de administração do Intune é aberto.  

5.  No console do [Console de Administração do Microsoft Intune](https://manage.microsoft.com), clique em **Política** > **Acesso Condicional** > **SharePoint Online Política**.  

6.  Selecione **Bloquear o acesso de aplicativos ao SharePoint Online se o dispositivo for incompatível**.  

7.  Em **Grupos Direcionados**, clique em **Modificar** para selecionar os grupos de segurança do Azure AD aos quais a política se aplica.  

8.  Opcionalmente, em **Grupos isentos**, clique em **Modificar** para selecionar os grupos de segurança do Azure AD que são isentos dessa política.  

9. Quando terminar, clique em **Salvar**.  

 Você não precisa implantar a política de acesso condicional; ela entra em vigor imediatamente.  

 Consulte [Gerenciar o acesso do SharePoint Online com o Microsoft Intune](/intune-classic/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune) para obter informações sobre como você pode monitorar a política no console do Intune.  

### <a name="see-also"></a>Consulte também  

 [Gerenciar o acesso a serviços no System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)
