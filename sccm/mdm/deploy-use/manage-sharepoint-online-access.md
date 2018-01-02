---
title: Gerenciar o acesso do SharePoint Online
titleSuffix: Configuration Manager
description: "Saiba como usar a política de acesso condicional do SharePoint Online no System Center Configuration Manager para gerenciar o acesso ao OneDrive."
ms.custom: na
ms.date: 12/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49cec466-1676-4fe2-a2fe-5004f01d735e
caps.latest.revision: "11"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 99b2aca418b7ce28a4216b38e711b3d38973e2b7
ms.sourcegitcommit: 372171a5cd8d143d6d47b651018cda0c91cad67c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/09/2017
---
# <a name="manage-sharepoint-online-access-in-system-center-configuration-manager"></a>Gerenciar o acesso ao SharePoint Online no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Use a política de acesso condicional do **SharePoint Online** no System Center Configuration Manager para gerenciar o acesso aos arquivos do OneDrive for Business localizados no SharePoint Online, com base nas condições especificadas.
Você pode controlar o acesso ao SharePoint Online dos aplicativos para as plataformas listadas a seguir:  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android e iOS)  

-   Microsoft Word (Android e iOS)  

-   Microsoft Excel (Android e iOS)  

-   Microsoft PowerPoint (Android e iOS)  

-   Microsoft OneNote (Android e iOS)

Os aplicativos de área de trabalho do Office podem acessar o SharePoint Online em computadores que executam:  

-   Área de trabalho do Office 2013 e posterior com [autenticação moderna](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) habilitada.  

-   Windows 7.0 ou Windows 8.1  

> [!NOTE]  
>  Os computadores devem ser ingressados no domínio ou ser compatíveis com as políticas definidas no Intune.  



 Quando um determinado usuário tenta se conectar a um arquivo usando um aplicativo com suporte assim como o OneDrive em seu dispositivo, ocorre a seguinte avaliação:  

 ![ConditionalAccess8&#45;6](media/ConditionalAccess8-6.png)  

 Para conectar-se aos arquivos necessários, o dispositivo que executa o OneDrive deve:  

-   Estar registrado no Microsoft Intune ou em um computador ingressado no domínio.  

-   Registre o dispositivo no Azure Active Directory (isso ocorre automaticamente quando o dispositivo é registrado no Intune).  

     Para PCs ingressados no domínio, você deve configurá-los para [registrarem-se automaticamente](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) no Active Directory do Azure.  

-   Ser compatível com todas as políticas de conformidade do Configuration Manager implantadas  

 O estado do dispositivo é armazenado no Active Directory do Azure que concede ou bloqueia o acesso a arquivos, com base nas condições que você especifica.  

 Se uma condição não for atendida, o usuário receberá uma das seguintes mensagens de erro ao fazer logon:  

-   Se o dispositivo não estiver registrado no Intune ou não estiver registrado no Azure Active Directory, será exibida uma mensagem com instruções sobre como instalar o aplicativo do portal da empresa e registrá-lo.  

-   Se o dispositivo não for compatível, será exibida uma mensagem direcionando o usuário para o portal da Web do Intune, no qual ele poderá encontrar informações sobre o problema e como corrigi-lo.  

- Para dispositivos móveis:

  Você pode restringir o acesso ao SharePoint Online quando o acesso é feio por meio de um navegador de dispositivos **iOS** e **Android**.  O acesso será permitido somente de navegadores com suporte em dispositivos compatíveis:
* Safari (iOS)
* Chrome (Android)
* Navegador gerenciado (iOS e Android)

  Navegadores sem suporte serão bloqueados.
-   Para um PC:  


    -   Se a política estiver definida para exigir o ingresso no domínio e o PC não tiver ingressado no domínio, uma mensagem será exibida para que o usuário entre em contato com o administrador de TI.  

    -   Se a política estiver definida para exigir ingresso no domínio ou compatibilidade e o PC não atender a nenhum dos dois requisitos, será exibida uma mensagem com instruções sobre como instalar o aplicativo do portal da empresa e realizar o registro.  

 É possível bloquear o acesso ao SharePoint Online por meio dos seguintes aplicativos:  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android e iOS)  

-   Microsoft Word (Android e iOS)  

-   Microsoft Excel (Android e iOS)  

-   Microsoft PowerPoint (Android e iOS)  

-   Microsoft OneNote (Android e iOS)  

## <a name="configure-conditional-access-for-sharepoint-online"></a>Configurar o acesso condicional para o SharePoint Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Etapa 1: Configurar grupos de segurança do Active Directory  
 Antes de começar, configure os grupos de segurança do Active Directory do Azure para a política de acesso condicional. Você pode configurar esses grupos no **Centro de administração do Office 365**ou no **Portal de conta do Intune**. Esses grupos contêm os usuários que serão afetados ou que ficarão isentos da política. Quando um usuário é afetado por uma política, cada dispositivo que ele usa deve ser compatível para que possa acessar os recursos.  

 Você pode especificar dois tipos de grupo em uma política do SharePoint Online:  

-   **Grupos de destino** â€“ Contém grupos de usuários aos quais a política será aplicada  

-   **Grupos isentos** â€“ Contém grupos de usuários isentos da política (opcional)  

 Se um usuário estiver nos dois grupos, ele ficará isento da política.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Etapa 2: Configurar e implantar uma política de conformidade  
 Certifique-se de criar e implantar uma política de conformidade para todos os dispositivos aos quais a política do SharePoint Online se destinará.  

> [!NOTE]  
>  Enquanto as políticas de conformidade são implantadas em grupos do Intune, ou em coleções do Configuration Manager, as políticas de acesso condicional destinam-se aos grupos de segurança do Azure Active Directory.  

 Para obter detalhes sobre como configurar a política de conformidade, consulte [Gerenciar políticas de conformidade do dispositivo no System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md).  

> [!IMPORTANT]  
>  Se você habilitar a política do SharePoint Online sem antes ter implantado uma política de conformidade, todos os dispositivos de destino terão acesso permitido.  

 Quando estiver pronto, continue na **Etapa 3**.  

###  <a name="BKMK_OneDrive"></a> Etapa 3: Configurar a política do SharePoint Online  


 Em seguida, configure a política para exigir que somente dispositivos gerenciados e compatíveis possam acessar o SharePoint Online. Essa política será armazenada no Active Directory do Azure.

 >[!NOTE]
 >Você também pode criar a política de acesso condicional no console de gerenciamento do Azure AD. O console de gerenciamento do Azure AD permite que você crie políticas de acesso condicional no dispositivo do Intune (chamada de política de acesso condicional baseada em dispositivos no Azure AD), além de outras políticas de acesso condicional, como a autenticação multifator. Você também pode definir políticas de acesso condicional para aplicativos corporativos de terceiros com suporte pelo Azure AD, como o Salesforce e o Box. Para obter mais detalhes, consulte [Como definir a política de acesso condicional com base no dispositivo do Azure Active Directory para controle de acesso dos aplicativos conectados no Azure Active Directory](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-policy-connected-applications/).  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  Selecione **Habilitar política de acesso condicional para o SharePoint Online**.  

     ![IntuneSASharePointOnlineCAPolicy](media/IntuneSASharePointOnlineCAPolicy.png)  

3.  Em **Acesso do aplicativo** para o Outlook e aplicativos que usam autenticação moderna, você pode optar por restringir o acesso apenas para dispositivos compatíveis para cada plataforma.  

    > [!TIP]  
    >  **Autenticação moderna** traz a entrada baseada no ADAL (Active Directory Authentication Library) para clientes Office.  
    >   
    >  -   A autenticação com base em ADAL permite que os clientes Office participem de autenticação baseada em navegador (também conhecida como autenticação passiva).  Para autenticar, o usuário é direcionado a uma página da Web de entrada.  
    > -   Esse novo método de entrada permite novos cenários, como acesso condicional, com base em **conformidade do dispositivo** e se a **autenticação multifator** foi executada.  
    >   
    >  Esse [artigo](https://support.office.com/en-US/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517) traz informações mais detalhadas sobre como funciona a autenticação moderna.  

     Para computadores Windows, este deve estar ingressado no domínio ou então ser registrado no Intune e ser compatível. Você pode definir os seguintes requisitos:  

    -   **Os dispositivos devem estar ingressados no domínio ou ser compatíveis.** Isso significa que os computadores devem estar ingressados no domínio ou ser compatíveis com as políticas definidas no Intune. Se o computador não atender a esses requisitos, será solicitado que o usuário registre o dispositivo no Intune.  

    -   **Os dispositivos devem estar ingressados no domínio.** Isso significa que os PCs devem estar ingressados no domínio para acessar o Exchange Online. Se o PC não estiver ingressado no domínio, o acesso ao email será bloqueado e será solicitado que o usuário entre em contato com o administrador de TI.  

    -   **Os dispositivos devem ser compatíveis.** Isso significa que os computadores devem ser compatíveis e estar registrados no Intune. Se o computador não estiver registrado, será exibida uma mensagem com instruções sobre como registrá-lo.  

4.  Em **Acesso do navegador** para o SharePoint Online e o OneDrive for Business, você pode optar por permitir o acesso somente ao Exchange Online por meio dos navegadores com suporte: Safari (iOS) e Chrome (Android). O acesso de outros navegadores será bloqueado.  As mesmas restrições de plataforma selecionadas para Acesso do aplicativo para o OneDrive também se aplicarão aqui.

    Em dispositivos **Android** , os usuários devem habilitar o acesso do navegador.  Para fazer isso, o usuário final deve habilitar a opção **Habilitar o Acesso do Navegador** no dispositivo registrado, da seguinte maneira:
    1.  Inicie o **aplicativo do Portal da Empresa**.
    2.  Vá para a página **Configurações** por meio dos três pontos (â€¦) ou do botão de menu do hardware.
    3.  Pressione o botão **Habilitar o Acesso do Navegador** .
    4.  No navegador Chrome, saia do Office 365 e reinicie o Chrome.

    Em plataformas **iOS e Android** , para identificar o dispositivo que é usado para acessar o serviço, o Azure Active Directory emitirá um certificado de TLS (protocolo TLS) para o dispositivo.  O dispositivo exibe o certificado com um prompt para que o usuário final selecione o certificado, conforme mostrado nas capturas de tela abaixo. O usuário final deve selecionar este certificado antes que possa continuar usando o navegador.

     **iOS**

     ![captura de tela do prompt do certificado em um ipad](media/mdm-browser-ca-ios-cert-prompt_v2.png)

     **Android**

      ![captura de tela do prompt do certificado em um dispositivo Android](media/mdm-browser-ca-android-cert-prompt.png)

4.  Na guia **Início** , no grupo **Links** , clique em **Configurar Política de Acesso Condicional no Console do Intune**. Talvez seja necessário fornecer o nome de usuário e a senha da conta usada para conectar o Configuration Manager ao Intune.  

     O console de administração do Intune será aberto.  

5.  No console do [Console de Administração do Microsoft Intune](https://manage.microsoft.com), clique em **Política** > **Acesso Condicional** > **SharePoint Online Política**.  

6.  Selecione **Bloquear o acesso de aplicativos ao SharePoint Online se o dispositivo for incompatível**.  

7.  Em **Grupos de Destino**, clique em **Modificar** para selecionar os grupos de segurança do Active Directory do Azure aos quais a política será aplicada.  

8.  Opcionalmente, em **Grupos isentos**, clique em **Modificar** para selecionar os grupos de segurança do Active Directory do Azure que são isentos dessa política.  

9. Quando terminar, clique em **Salvar**.  

 Você não precisa implantar a política de acesso condicional, ele entra em vigor imediatamente.  

 Consulte [Gerenciar o acesso do SharePoint Online com o Microsoft Intune](https://technet.microsoft.com/library/dn705844.aspx) para obter informações sobre como você pode monitorar a política no console do Intune.  

### <a name="see-also"></a>Consulte também  

 [Gerenciar o acesso a serviços no System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)
