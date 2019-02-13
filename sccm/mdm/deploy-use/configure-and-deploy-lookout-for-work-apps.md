---
title: Implantar o aplicativo Lookout for Work
titleSuffix: Configuration Manager
description: Configure e implante aplicativos Lookout for Work.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 3f62b763-4347-453d-b0a7-1f4a0d1d4105
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a4e829d92b099be3fbf77796ea604d9d33db252c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132945"
---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>Configurar e implantar aplicativos Lookout for Work

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo explica como configurar e implantar o aplicativo Lookout for Work em dispositivos Android e iOS.



## <a name="android-google-play-store-app"></a>Android (aplicativo Google Play Store)
1.  No console do Configuration Manager, clique em **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.  

2.  Na página **Geral** do Assistente para Implantar Software, especifique as seguintes informações:  
    - Tipo: selecione **Pacote do aplicativo para Android no Google Play**.
    - Local: copie o link do aplicativo Lookout for Work da Google Play Store e cole-o aqui
    - Publisher: Lookout Mobile Security
    - Nome: Lookout for Work
    - Descrição: o Lookout oferece a melhor proteção contra ameaças móveis para proteger o seu dispositivo. Quando aplicativo Lookout é instalado, ele protege seu dispositivo contra ameaças. Se encontrar qualquer ameaça, ele o alertará você e seu administrador de TI.
    - Categoria administrativa: Gerenciamento do computador  

    Após a conclusão com êxito, o aplicativo Lookout for Work aparece na sua lista de aplicativos.  

3.  Na guia **Início**, no grupo **Implantação**, escolha **Implantar** para implantar o aplicativo Lookout for Work para os usuários.   
    >[!IMPORTANT]  
    >Você deve selecionar os mesmos usuários que foram adicionados à opção Gerenciamento de Registro no console do Lookout MTP.  

    Escolha a opção **Instalação Obrigatória**. Essa opção requer que o aplicativo Lookout seja instalado no dispositivo do usuário.  



## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS (versão do aplicativo Lookout assinada pela empresa)

1. Verifique se o gerenciamento do iOS está configurado em seus dispositivos. Para obter instruções de como configurar seu dispositivo para o gerenciamento do iOS, confira [Configurar o gerenciamento de dispositivos iOS e Mac](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac).  

2. Assine novamente o aplicativo iOS Lookout for Work. A Lookout distribui seu aplicativo Lookout for Work iOS fora da iOS App Store. Antes de distribuir o aplicativo, você precisa assiná-lo novamente com o Certificado do Enterprise Developer do iOS. Para obter instruções detalhadas de como reassinar aplicativos iOS Lookout for Work, consulte [Lookout for Work iOS app re-signing process](https://personal.support.lookout.com/hc/articles/114094038714) (Processo para reassinar o aplicativo iOS Lookout for Work) no site da Lookout.  

3. Habilite a autenticação do Azure AD (Azure Active Directory) para os usuários do iOS.
   1.  Entre na [folha do Azure AD no portal do Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) e navegue até a página de registros de aplicativo.  
   2.  Especifique o Nome como **Aplicativo iOS Lookout for Work** e selecione **Nativo** como o Tipo de Aplicativo.  
   ![captura de tela da caixa de diálogo para adicionar aplicativos mostrando a opção de aplicativo cliente nativo](media/aad-add-app-reg.png)

   3.  Para esse URI de Redirecionamento, use o seguinte formato: `lookoutwork://com.lookout.enterprise.<yourcompanyname>`, substituindo `<yourcompanyname>` pelo nome da sua empresa. Por exemplo: `lookoutwork://com.lookout.enterprise.contoso`
   4. Clique em **Criar** para criar o aplicativo. 
   5.  Abra o novo aplicativo, clique em **Configurações** e adicione um URI de Redirecionamento adicional. Use o seguinte formato: `companyportal://code/<originalURI>`, em que `<originalURI>` é uma versão codificada por URL do URI de Redirecionamento original. Por exemplo, `companyportal://code/lookoutwork%3A%2F%2Fcom.lookout.enterprise.contoso`
   6.  Nas configurações do aplicativo, acesse **Permissões necessárias** e clique em **Adicionar**. Selecione as seguintes permissões delegadas:  

       | API  | Permissão  |
       |---------|---------|
       | Lookout MTP     | Acessar o Lookout MTP         |
       | Microsoft Graph     | Entrar e ler o perfil do usuário        |  

   Para obter mais informações, consulte [Configurar um aplicativo cliente nativo](/azure/app-service/app-service-mobile-how-to-configure-active-directory-authentication#optional-configure-a-native-client-application).  


4. No Configuration Manager, carregue o arquivo .ipa assinado novamente. Defina a versão mínima do sistema operacional para iOS 8.0 ou posterior. Para obter mais informações, confira [Criar aplicativos iOS](/sccm/apps/get-started/creating-ios-applications).   


5. Crie a política de configuração do aplicativo gerenciado. Para obter mais informações, confira [Configurar aplicativos iOS com as políticas de configuração de aplicativo móvel](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).  


6. Implante o aplicativo Lookout for Work para os usuários. Para obter informações, confira [Deploy applications](/sccm/apps/deploy-use/deploy-applications) (Implantar aplicativos).  

   Selecione os mesmos usuários que foram adicionados à opção Gerenciamento de Registro no console do Lookout. Escolha a opção **Instalação Obrigatória**. Essa opção requer que o aplicativo Lookout seja instalado no dispositivo do usuário.



## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>O que acontece quando o aplicativo implantado é aberto no dispositivo

Quando o usuário abre o Lookout for Work no dispositivo, ele solicita então a ativação do aplicativo. Eles devem escolher entrar com a opção do Azure AD. Um passo a passo detalhado com o fluxo do usuário final está nos artigos a seguir:

- [Será solicitada a instalação do Lookout for Work em seu dispositivo Android](/intune-user-help/you-are-prompted-to-install-lookout-for-work-android)

- [Você precisa resolver uma ameaça encontrada pelo Lookout for Work no dispositivo Android](/intune-user-help/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)



## <a name="next-steps"></a>Próximas etapas
- [Habilitar regra de proteção contra ameaças ao dispositivo na política de conformidade](enable-device-threat-protection-rule-compliance-policy.md)
