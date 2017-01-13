---
title: Implantar o aplicativo Lookout for Work | System Center Configuration Manager
description: Configure e implante aplicativos Lookout for Work.
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dfdbfee6-4b9b-4d53-816a-62bbc3a43b6e
caps.latest.revision: 
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c13c6268fa76ade7feb0981f9c4a6e325e393aca
ms.openlocfilehash: 947393796043dcc3916a5f8e09898bb8a7cd347d


---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>Configurar e implantar aplicativos Lookout for Work

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo explica como configurar e implantar o aplicativo Lookout for Work em dispositivos Android e iOS.

## <a name="android-google-play-store-app"></a>Android (aplicativo da Google Play Store)
1.  No console do Configuration Manager, clique em **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Aplicativos**.

2.  Na página **Geral** do Assistente para Implantar Software, especifique as seguintes informações:
  * Tipo: selecione **Pacote do aplicativo para Android no Google Play**.
  * Local: copie o link do aplicativo Lookout for Work da Google Play Store e cole-o aqui
  * Editor: Lookout Mobile Security
  * Nome: Lookout for Work
  * Descrição: o Lookout oferece a melhor proteção contra ameaças a dispositivos móveis para proteger o seu dispositivo. Quando o aplicativo Lookout está instalado no dispositivo, ele o protege contra ameaças e alerta você e o administrador da sua empresa quando alguma ameaça é encontrada.
  * Categoria administrativa: gerenciamento de computador

  Após a conclusão com êxito, o aplicativo Lookout for Work aparecerá na sua lista de aplicativos.

3.  Na guia **Início**, no grupo **Implantação**, escolha **Implantar** para implantar o aplicativo Lookout for Work para os usuários.
>[!IMPORTANT]
>Você deve selecionar os mesmos usuários que foram adicionados à opção Gerenciamento de Registro no console do Lookout MTP.

  Escolha a opção **Instalação Obrigatória** para exigir que o aplicativo Lookout seja instalado no dispositivo do usuário.

## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS (versão do aplicativo Lookout assinada pela empresa)

* **Etapa 1:** verifique se o **gerenciamento do iOS** está configurado no dispositivo. Para obter instruções de como configurar o dispositivo para o gerenciamento do iOS, consulte [Configurar gerenciamento de dispositivos iOS e Mac]().

* **Etapa 2:** **reassinar** o aplicativo Lookout for Work iOS. A Lookout distribui seu aplicativo Lookout for Work iOS fora da iOS App Store. **Antes de distribuir o aplicativo**, você deve reassinar o aplicativo com seu certificado de desenvolvedor iOS corporativo. Para obter instruções detalhadas de como reassinar aplicativos iOS Lookout for Work, consulte [Lookout for Work iOS app re-signing process](https://personal.support.lookout.com/hc/en-us/articles/114094038714) (Processo para reassinar o aplicativo iOS Lookout for Work) no site da Lookout.


* **Etapa 3:** habilitar a autenticação do Azure Active Directory para os usuários do iOS, fazendo o seguinte:
  1.  Faça logon no [Portal de Gerenciamento do Azure Active Directory](https://manage.windowsazure.com) e navegue até a página do aplicativo.
  2.  Adicione o **aplicativo Lookout for Work iOS** como um **aplicativo cliente nativo**.
  ![captura de tela da caixa de diálogo para adicionar aplicativos mostrando a opção de aplicativo cliente nativo](../media/aad-add-app.png)

  3. Substitua o **com.lookout.enterprise.yourcompanyname** pela ID do grupo do cliente que você selecionou quando assinou o IPA.
  4.  Adicione o URI de redirecionamento adicional: **&lt;companyportal://code/>** seguido por uma versão codificada da URL do URI de redirecionamento original.
  5.  Adicione **Permissões delegadas** ao aplicativo.

  Para obter mais detalhes, consulte [Configurar um aplicativo cliente nativo](https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-how-to-configure-active-directory-authentication/#optional-configure-a-native-client-application).


* **Etapa 4:** carregar o arquivo .ipa reassinado, conforme a descrição no tópico [Criar aplicativos iOS com o System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/apps/get-started/creating-ios-applications). Defina a versão mínima do sistema operacional para iOS 8.0 ou posterior.


* **Etapa 5:** criar a política de configuração de aplicativo gerenciado, conforme a descrição no tópico [Configure iOS apps with mobile app configuration policies in System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies) (Configurar aplicativos iOS com políticas de configuração de aplicativo móvel no System Center Configuration Manager).


* **Etapa 6:** **para implantar o aplicativo para usuários**, selecione o aplicativo Lookout for Work na página **Aplicativos**, da guia **Início** e no grupo **Implantação** escolha **Implantar**.

  Você deve selecionar os mesmos usuários que foram adicionados à opção Gerenciamento de Registro no console do Lookout.  
Escolha a opção **Instalação Obrigatória** para exigir que o aplicativo Lookout seja instalado no dispositivo do usuário.

## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>O que acontece quando o aplicativo implantado é aberto no dispositivo




Quando o usuário abre o Lookout for Work no dispositivo, é solicitado que ele ative o aplicativo e escolha a opção Entrar com o Azure Active Directory. Um passo a passo detalhado com o fluxo do usuário final pode ser encontrado nos tópicos a seguir:

* [Será solicitada a instalação do Lookout for Work em seu dispositivo Android](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

* [Você precisa resolver uma ameaça encontrada pelo Lookout for Work no dispositivo Android](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)

## <a name="next-steps"></a>Próximas etapas
* [Habilitar regra de proteção contra ameaças ao dispositivo na política de conformidade](enable-device-threat-protection-rule-compliance-policy.md)



<!--HONumber=Dec16_HO3-->


