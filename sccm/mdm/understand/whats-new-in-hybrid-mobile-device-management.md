---
title: Novidades no MDM híbrido
titleSuffix: Configuration Manager
description: Saiba mais sobre os novos recursos de gerenciamento de dispositivo móvel disponíveis para implantações híbridas com o Configuration Manager e o Intune.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b6a4cfbc7e9db5f4402278b73c2ca7ea1d869953
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66355010"
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-configuration-manager-and-microsoft-intune"></a>Novidades no gerenciamento de dispositivo móvel híbrido com o Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo fornece detalhes sobre os novos recursos de MDM (gerenciamento de dispositivo móvel) disponíveis para implantações híbridas com o System Center Configuration Manager e o Microsoft Intune.

> [!Important]  
> O gerenciamento híbrido de dispositivos móveis é um [recurso preterido](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures) desde 14 de agosto de 2018. Para saber mais, confira [O que é o MDM híbrido](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  

> [!Note]  
> O Intune no Azure é a solução de MDM recomendada pela Microsoft.
>
> - Para obter detalhes sobre novos recursos e atualizações no Intune autônomo, consulte [Novidades do Intune](https://docs.microsoft.com/intune/whats-new).
> - Para obter detalhes de como migrar para o Intune autônomo, consulte [Migrate hybrid MDM users and devices to Intune standalone](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa) (Migrar usuários e dispositivos de MDM híbrido para o Intune autônomo).
> - Para obter detalhes sobre as atualizações da interface do usuário do Intune e o MDM híbrido, consulte [Atualizações da interface do usuário para aplicativos de usuário final do Intune](https://docs.microsoft.com/intune/whats-new-app-ui).



## <a name="compatibility-with-configuration-manager-versions"></a>Compatibilidade com versões do Configuration Manager  

Cada seção deste artigo lista recursos híbridos em três categorias diferentes. Use as seguintes diretrizes para determinar a compatibilidade dos recursos em cada categoria com versões diferentes do Configuration Manager:  

|Categorias do recurso|Descrição|
|-|-|
|**Novo no Microsoft Intune** | De modo geral, todos os recursos listados nesta categoria devem funcionar com todas as versões do Configuration Manager. Isso inclui versões do System Center 2012 R2 Configuration Manager, uma vez que esses recursos exigem apenas o serviço Intune e não exigem funcionalidades adicionais no Configuration Manager.|
|**Novo no Configuration Manager Technical Preview**| Todos os recursos listados nessa categoria funcionam apenas com o branch de visualização técnica especificado. Para testar esses recursos, você deve instalar a versão de visualização técnica especificada na descrição do recurso. Para obter mais informações, confira [Visualização técnica para o Configuration Manager](/sccm/core/get-started/technical-preview).|
|**Novo no Configuration Manager (Branch Atual)**| Todos os recursos listados nessa categoria funcionam apenas com a versão especificada do Configuration Manager (branch atual). Se estiver usando uma versão mais antiga do Configuration Manager para sua implantação híbrida, atualize para a versão do Configuration Manager (branch atual) especificada na descrição do recurso. Para obter mais informações, veja [Atualizar para o Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).|


## <a name="may-2019"></a>Maio de 2019

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="windows-company-portal-app"></a>Aplicativo do Portal da Empresa para Windows

<!-- 3316993 -->

O aplicativo de Portal de empresa do Windows agora tem uma nova página rotulada **dispositivos**. O **dispositivos** página mostra aos usuários todos os seus dispositivos registrados. Os usuários verão essa alteração no Portal da empresa quando eles usam a versão 10.3.4291.0 e posterior. Para obter mais informações, consulte [como configurar o aplicativo de Portal da empresa do Microsoft Intune](https://docs.microsoft.com/intune/company-portal-app).

#### <a name="android-enterprise-app-management"></a>Gerenciamento de aplicativo do Android Enterprise

<!-- 4459905 -->

Para tornar mais fácil para que você possa configurar e usar o gerenciamento de Android Enterprise, o Intune adiciona automaticamente os quatro seguintes Android Enterprise comuns relacionados a aplicativos para o console de administração do Intune:

- [Microsoft Intune](https://play.google.com/store/apps/details?id=com.microsoft.intune): Usado para cenários empresariais Android totalmente gerenciado
- [Microsoft Authenticator](https://play.google.com/store/apps/details?id=com.azure.authenticator): Se você usar a verificação de dois fatores, esse aplicativo ajuda você a entrar em suas contas
- [Portal da empresa Intune](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal): Usado para as políticas de proteção de aplicativo (aplicativo) e cenários de perfil de trabalho do Android Enterprise
- [Tela inicial de gerenciado](https://play.google.com/store/apps/details?id=com.microsoft.launcher.enterprise): Usado para cenários de dedicado/quiosque do Android Enterprise

Anteriormente, durante a instalação necessária para localizar manualmente e aprovar a esses aplicativos na [loja Google Play gerenciado](https://play.google.com/store/apps). Essa alteração remove essas etapas manuais anteriormente para torná-lo mais fácil e rápido para usar o gerenciamento de Android Enterprise.

Quando você primeiro se conectar seu locatário do Intune ao Google Play gerenciado, você verá esses quatro aplicativos adicionados automaticamente à lista aplicativos do Intune. Para obter mais informações, consulte [habilitar registro do Android for Work](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-for-work-enrollment). Se você já estiver conectado a seu locatário ou já usa o Android Enterprise, não há nada que você precise fazer. Esses quatro aplicativos aparecem automaticamente dentro de sete dias após a atualização de serviço de maio de 2019.

#### <a name="intune-policies-update-authentication-method-and-company-portal-app-installation"></a>As políticas do Intune atualizar método de autenticação e a instalação do aplicativo de Portal da empresa

<!-- 1927359 -->

Em dispositivos já registrados por meio do Assistente de instalação por meio de um dos métodos de registro de dispositivo corporativo da Apple, Intune não dá suporte a Portal da empresa quando ele é instalado manualmente pelos usuários da app store. Essa alteração só é relevante quando você autenticar com o Assistente de configuração da Apple durante o registro. Ele afeta somente os dispositivos iOS registrados por meio dos seguintes métodos:  

- Apple Configurator
- Gerente de negócios da Apple
- Apple School Manager
- Programa de registro de dispositivo (DEP) da Apple

Se usuários instalar o aplicativo de Portal da empresa da loja de aplicativos e, em seguida, tente registrar esses dispositivos por meio dele, eles receberão um erro. Além disso, o **identificar o dispositivo** tela no aplicativo Portal da empresa em breve se tornarão obsoleta.

Para instalar o Portal da empresa em dispositivos já registrados no DEP, enviar por push como um aplicativo gerenciado com as políticas de configuração de aplicativo. Para obter mais informações sobre esse processo, consulte [aplicar as configurações para aplicativos iOS com políticas de configuração de aplicativo no Configuration Manager](/sccm/mdm/deploy-use/configure-ios-apps-with-app-configuration-policies).


## <a name="april-2019"></a>Abril de 2019

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="openssl-encryption-for-android-app-protection-policies"></a>Criptografia do OpenSSL para políticas de proteção de aplicativo do Android

<!-- 3747362 -->
Políticas de proteção de aplicativo do Intune (aplicativo) em dispositivos Android agora usam uma biblioteca de criptografia do OpenSSL que tem certificação FIPS 140-2. Para obter mais informações, consulte [configurações de política de proteção de aplicativo do Android no Microsoft Intune](https://docs.microsoft.com/intune/app-protection-policy-settings-android#encryption).


## <a name="march-2019"></a>Março de 2019

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="user-experience-update-for-the-company-portal-app-for-ios"></a>Atualização de experiência do usuário para o aplicativo Portal da Empresa para iOS

<!-- 2536024 -->
A home page do aplicativo Portal da empresa para dispositivos iOS foi reprojetada. Com essa alteração, a home page segue melhor os padrões de interface do usuário do iOS. Ele também fornece detectabilidade aprimorada para aplicativos e livros eletrônicos.

#### <a name="install-available-apps-using-the-company-portal-app-after-windows-bulk-enrollment"></a>Instalar aplicativos disponíveis usando o aplicativo de Portal da empresa após o registro em massa do Windows

<!-- 2751523 -->
Dispositivos Windows registrados no Intune usando [registro do Windows em massa](https://docs.microsoft.com/intune/windows-bulk-enroll) (pacotes de provisionamento) poderão usar o aplicativo de Portal da empresa para instalar aplicativos disponíveis. Para obter mais informações sobre o aplicativo de Portal da empresa, consulte [adicionar manualmente o Portal da empresa do Windows 10](https://docs.microsoft.com/intune/store-apps-company-portal-app) e [como configurar o aplicativo de Portal da empresa do Microsoft Intune](https://docs.microsoft.com/intune/company-portal-app).

> [!Note]  
> Esse recurso ainda não está totalmente implantado em todos os clientes. Se você não pode usar o Portal da empresa em dispositivos em massa registrado, talvez você precise aguardar até que essa alteração distribui para sua conta.

#### <a name="app-icons-are-displayed-with-an-automatically-generated-background"></a>Ícones do aplicativo são exibidos com um plano de fundo gerado automaticamente

<!-- 1429026 -->
O aplicativo do Portal de empresa do Windows agora exibe ícones de aplicativo com um plano de fundo gerado automaticamente. Este plano de fundo baseia-se na cor dominante do ícone, se ele puder ser detectado. Quando aplicável, o plano de fundo substituirá a borda cinza que era visível anteriormente em blocos de aplicativos. Você verá essa alteração em versões mais recentes que 10.3.3451.0 do Portal da empresa.

#### <a name="changes-to-company-portal-enrollment-for-ios-12-devices"></a>Alterações no registro do Portal da empresa para dispositivos iOS 12

<!-- 3448635 -->  
Portal da empresa para iOS atualiza as telas de registro do aplicativo e as etapas para se alinhar com as alterações de registro do MDM lançadas no Apple iOS 12.2. O fluxo de trabalho atualizado agora solicita que você:

- Permitir Safari abrir o site do Portal da empresa (por meio do Safari) e baixar o perfil de gerenciamento antes de retornar ao aplicativo Portal da empresa. 
- Abra o aplicativo de configurações para instalar o perfil de gerenciamento em seu dispositivo.
- Retorne ao aplicativo Portal da empresa para concluir o registro.  

Para obter mais informações sobre como preparar para que essas alterações, consulte o [postagem do Microsoft Tech Community](https://aka.ms/CP_changes_iOS12). Para dar suporte a novos registros de iOS no Portal da empresa, consulte [registrar o dispositivo de iOS no Intune](https://docs.microsoft.com/intune/ios-enroll).



## <a name="february-2019"></a>Fevereiro de 2019

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="create-new-intune-tenants-in-azure-portal"></a>Criar novos locatários do Intune no portal do Azure

<!--3754067-->  
A capacidade de criar um novo locatário MDM híbrido foi removida como do 1902 Intune atualização. Crie todos os novos locatários do Intune no portal do Azure. Como um lembrete [híbrida MDM é preterido](/sccm/mdm/understand/hybrid-mobile-device-management). Os clientes atuais do MDM híbrido devem migrar para o Intune autônomo, assim que possível.

Para saber mais, confira [a postagem no blog de suporte do Intune](https://aka.ms/hybrid_notification).

#### <a name="intune-uses-google-play-protect-apis-on-android-devices"></a>O Intune usa o Google Play proteger APIs em dispositivos Android

<!--2577355-->  
Alguns administradores se deparam com um cenário BYOD, onde os usuários podem raiz ou jailbreak telefone celular. Esse comportamento, embora, às vezes, não mal-intencionados, resulta em um desvio de muitas políticas do Intune que são definidas para proteger os dados da organização em dispositivos de usuário final. Assim, o Intune fornece detecção de raiz e jailbreak para dispositivos registrados e não registrados.

Com esta versão, o Intune agora aproveita reproduzir proteger APIs do Google para adicionar a nossas verificações de detecção de raiz existentes para dispositivos não registrados. Enquanto o Google não compartilha as verificações de detecção de raiz que ocorrem na íntegra, esperamos que essas APIs para detectar os usuários que têm enraizada seus dispositivos por qualquer motivo de personalização de dispositivo para ser capaz de obter as atualizações mais recentes do sistema operacional em dispositivos mais antigos. Esses usuários, em seguida, podem ser impedidos de acessar dados corporativos ou suas contas corporativas podem ser apagadas de seus aplicativos de política estiver habilitada.

#### <a name="new-app-categories-screen-in-the-company-portal-app-for-windows-10"></a>Novos **categorias de aplicativo** tela no aplicativo Portal da empresa para Windows 10

<!--3834780-->  
Para melhorar a experiência de navegação e seleção do aplicativo no Portal de empresa para Windows 10, agora ele inclui uma nova tela chamada **categorias de aplicativo**. Os usuários agora ver seus aplicativos classificados em categorias, como **em destaque**, **educação**, e **produtividade**. Essa alteração aparece nas versões de Portal da empresa 10.3.3451.0 e versões posteriores. Para exibir a nova tela, consulte [o que há de novo no aplicativo de interface do usuário](https://docs.microsoft.com/intune/whats-new). Para obter mais informações sobre os aplicativos no Portal da empresa, consulte [instalar e compartilhar aplicativos no seu dispositivo](https://docs.microsoft.com/intune-user-help/install-apps-cpapp-windows).  

#### <a name="macos-users-are-prompted-to-update-their-password"></a>os usuários do macOS são solicitados para atualizar sua senha

<!--1873216-->  
Em dispositivos macOS, os usuários finais serão solicitados para atualizar sua senha. Esse aviso ocorre sempre que um usuário executa uma tarefa que requer autenticação, como entrar no dispositivo. Usuários também precisará atualizar suas senhas quando fazer nada que requer privilégios administrativos, como solicitar acesso ao conjunto de chaves.  

#### <a name="intune-macos-company-portal-dark-mode"></a>MacOS do Intune modo escuro do Portal da empresa

<!--3300524-->  
O Portal da empresa do macOS do Intune agora dá suporte ao modo de escuro para macOS. Quando você habilita o modo escuro em um dispositivo macOS 10.14 +, o Portal da empresa ajusta sua aparência para as cores que refletem esse modo.



## <a name="january-2019"></a>Janeiro de 2019

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="intune-app-protection-policies-ui-update"></a>Atualização da interface do usuário de políticas de proteção do Intune app

<!--3251427-->  
Alteramos os rótulos para as configurações e os botões para proteção de aplicativo do Intune tornar mais fácil entender cada. Algumas dessas alterações incluem:  

- Controles são alterados do **Sim** / **nenhum** controla principalmente para **bloco** / **permitir** e **desabilitar** / **habilitar** controles. Os rótulos também são atualizados.  

- As configurações são reformatadas, portanto, a configuração e seu rótulo são lado a lado no controle, para fornecer uma navegação melhor.  

As configurações padrão e o número de configurações permanecem os mesmos, mas essa alteração permite que o usuário entender, navegar e utilizar as configurações mais facilmente para aplicar políticas de proteção do aplicativo selecionado. Para obter mais informações, consulte [configurações do iOS](https://docs.microsoft.com/intune/app-protection-policy-settings-ios#access-requirements) e [configurações do Android](https://docs.microsoft.com/intune/app-protection-policy-settings-android#access-requirements).

#### <a name="tenant-status-dashboard"></a>Painel de Status do locatário

<!--1124854-->  
O novo [página de Status do locatário](https://docs.microsoft.com/intune/tenant-status) fornece um único local onde você pode exibir o status e os detalhes relacionados para seu locatário. O painel é dividido em quatro áreas:

- **Detalhes do locatário**: Exibe informações que incluem o nome do locatário e o local, sua autoridade de MDM, o total os dispositivos registrados no seu locatário e contagens de suas licenças. Esta seção também lista a versão atual do serviço para seu locatário.  

- **Status do conector**: Exibe informações sobre conectores disponíveis, você configurou e também pode listar os que ainda não tiver habilitado.  

    Com base no estado atual de cada conector, eles são sinalizados como não íntegro, aviso ou íntegro. Selecione um conector do drill-through e exibir detalhes ou configurar as informações adicionais para ele.  

- **Integridade do serviço Intune**: Exibe detalhes sobre incidentes ativos ou interrupções para seu locatário. As informações nesta seção são recuperadas diretamente do Centro de mensagens do Office.  

- **Notícias sobre o Intune**: Exibe mensagens ativas para seu locatário. Mensagens incluem coisas como notificações quando seu locatário recebe os recursos mais recentes do Intune.  As informações nesta seção são recuperadas diretamente do Centro de mensagens do Office.  

#### <a name="new-help-and-support-experience-in-company-portal-for-windows-10"></a>Novo ajuda e suporte experiência no Portal de empresa para Windows 10

<!--1488939-->  
A nova página de Ajuda do Portal da empresa e suporte ajuda os usuários a solucionar problemas e solicitar ajuda para problemas de acesso e de aplicativo. Na página de novo, podem erro e detalhes de log de diagnóstico de email e encontrar detalhes de suporte técnico de sua organização. Eles também encontrará uma seção de perguntas Frequentes com links para a documentação relevante do Intune. Para obter mais informações e capturas de tela, consulte [Obtenha ajuda e suporte no Portal de empresa para Windows 10](https://docs.microsoft.com/intune-user-help/help-and-support-windows-cpapp).

#### <a name="some-bitlocker-settings-support-windows-10-pro-edition"></a>Suportam a algumas configurações de disco BitLocker do Windows 10 Pro edition

<!--2727036-->  
Você pode criar um item de configuração que define as configurações do endpoint protection em dispositivos Windows 10, incluindo o BitLocker. Essa atualização adiciona suporte para Windows 10 Professional edition para algumas configurações de disco BitLocker.

Para obter mais informações, consulte [configurações de criptografia para o Windows 10](/sccm/mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#encryption).



## <a name="december-2018"></a>Dezembro de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="microsoft-auto-update-version-450-required-for-macos-devices"></a>Versão de atualização automática de Microsoft 4.5.0 necessária para dispositivos macOS

<!--3503442-->  
Para continuar recebendo atualizações para o Portal da empresa e outros aplicativos do Office, os dispositivos macOS gerenciados pelo Intune devem atualizar para Microsoft automática 4.5.0. Os usuários talvez já tenha esta versão para seus aplicativos do Office.

#### <a name="the-intune-app-sdk-will-support-256-bit-encryption-keys"></a>O SDK do App Intune dará suporte a chaves de criptografia de 256 bits

<!--1832174-->  
SDK do Intune App para Android agora usa as chaves de criptografia de 256 bits quando a criptografia é habilitada por políticas de proteção do aplicativo. O SDK continuará fornecer suporte a chaves de 128 bits para compatibilidade com o conteúdo e aplicativos que usam versões mais antigas do SDK.

#### <a name="intune-requires-macos-1012-or-later"></a>O Intune exige o macOS 10.12 ou posterior

<!--2827778-->  
O Intune agora requer o macOS versão 10.12 ou posterior. Dispositivos que usam versões anteriores do macOS não podem usar o Portal da empresa para registrar no Intune. Para receber suporte e novos recursos, os usuários devem atualizar seus dispositivos MacOS 10.12 ou posterior e atualizar o Portal da empresa para a versão mais recente.

Para obter mais informações, consulte [plano para alteração: Intune dá suporte a macOS 10.12 e superior em dezembro](#plan-for-change-intune-supports-macos-1012-and-higher-in-december).



## <a name="november-2018"></a>Novembro de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="new-intune-device-subscription-sku"></a>Nova assinatura do dispositivo Intune SKU

<!--3312071-->  
Para ajudar a reduzir o custo do gerenciamento de dispositivos nas empresas, uma assinatura com base em dispositivo novo SKU agora está disponível. Este dispositivo do Intune SKU é licenciado por dispositivo mensalmente. Preço varia de acordo com o programa de licenciamento. Ele está disponível no canal direto, Enterprise Agreement (EA), Products da Microsoft e serviços de programa (MPSA) e abrir e provedor de solução de nuvem (CSP).

#### <a name="new-apps-support-with-app-protection-policies"></a>Suportam a novos aplicativos com políticas de proteção de aplicativo

<!--3330037-->  
Agora você pode gerenciar os seguintes aplicativos com [políticas de proteção de aplicativo do Intune](https://docs.microsoft.com/intune/app-protection-policies):

- Stream (iOS)  
- Tarefas pendentes (Android, iOS)  
- PowerApps (Android, iOS)  
- Fluxo (Android, iOS)  

Use a políticas de proteção do aplicativo para proteger corporativa transferência de dados de controle e de dados para esses aplicativos, como outro aplicativos gerenciados pela política do Intune.

> [!Note]  
> Se o fluxo ainda não está visível no console do, adicionar fluxo ao criar ou editar as políticas de proteção do aplicativo. Selecione **mais aplicativos**e, em seguida, especifique a *ID do aplicativo* para o fluxo no campo de entrada. Para uso do Android `com.microsoft.flow`, e para iOS, use `com.microsoft.procsimo`.  



## <a name="october-2018"></a>Outubro de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="updates-for-application-transport-security"></a>Atualizações de Segurança do Transporte de Aplicativo

<!--748318-->  
Microsoft Intune dá suporte a segurança TLS (Transport Layer) 1.2 + para fornecer o melhor da criptografia, para garantir que o Intune é mais seguro por padrão e para se alinhar com outros serviços da Microsoft, como o Microsoft Office 365. Para cumprir esse requisito, os portais da empresa iOS e macOS imporão requisitos de ATS (Segurança do Transporte de Aplicativo) da Apple atualizados que também exigem TLS 1.2+. O ATS é usado para impor a segurança mais rígida em todas as comunicações de aplicativo via HTTPS. Essa alteração afeta os clientes do Intune que usam os aplicativos de Portal da Empresa do iOS e macOS. Para saber mais, confira [Mudança do Intune para TLS 1.2 para criptografia ](https://blogs.technet.microsoft.com/intunesupport/2018/06/05/intune-moving-to-tls-1-2-for-encryption/).

#### <a name="remove-an-email-profile-from-a-device-even-when-theres-only-one-email-profile"></a>Remover um perfil de email de um dispositivo, mesmo quando há apenas um email perfil

<!--1818139-->  
Anteriormente, você não foi possível remover um perfil de email de um dispositivo se ele for o único perfil de email. Com essa atualização, esse comportamento mudará. Agora, você pode remover um perfil de email mesmo que ele seja o único perfil de email no dispositivo.

#### <a name="remove-pkcs-and-scep-certificates-from-your-devices"></a>Remover certificados PKCS e SCEP de seus dispositivos

<!--3218390-->  
Em alguns cenários, Certificados PKCS e SCEP permaneceram em dispositivos, mesmo quando a remoção de uma política de um grupo de exclusão de uma configuração ou implantação de conformidade ou um administrador atualizando um perfil SCEP ou PKCS existente.

Essa atualização altera o comportamento. Há alguns cenários em que os certificados PKCS e SCEP são removidos dos dispositivos e alguns cenários em que esses certificados permanecem no dispositivo.

#### <a name="access-to-key-profile-properties-using-the-company-portal-app"></a>Acesso a propriedades-chave do perfil usando o aplicativo do portal da empresa

<!--772203-->  
Os usuários finais agora podem acessar as propriedades e ações da conta principal, como a redefinição de senha, no aplicativo Portal da Empresa.

#### <a name="pin-prompt-when-you-change-fingerprints-or-face-id-on-an-ios-device"></a>Solicitação de PIN ao alterar impressões digitais ou identificação de rosto em um dispositivo iOS

<!--2637704-->  
Os usuários agora são solicitados a inserir um PIN após fazerem alterações biométricas em seu dispositivo iOS. Isso inclui alterações em impressões digitais ou identificação facial registradas. O tempo da solicitação depende da configuração do tempo limite em *Verificar novamente os requisitos de acesso após (minutos)* .  Quando não há um PIN definido, o usuário é solicitado a definir um.  

Esse recurso está disponível apenas para iOS e requer a participação de aplicativos que integram o SDK do aplicativo Intune para iOS, versão 8.1.1 ou posterior. A integração do SDK é necessária para que o comportamento possa ser aplicado aos aplicativos de destino. Essa integração ocorre sem interrupção, e depende de equipes do aplicativo específico. Alguns aplicativos que participam incluem WXP, Outlook, Managed Browser e Yammer.

#### <a name="end-user-device-and-app-content-menu"></a>Dispositivo de usuário final e menu de conteúdo do aplicativo

<!--2771453-->  
Os usuários finais agora podem usar o menu de contexto no dispositivo e nos aplicativos para acionar ações comuns, como renomear um dispositivo ou verificar a conformidade.

#### <a name="windows-company-portal-keyboard-shortcuts"></a>Atalhos de teclado do Portal da Empresa do Windows

<!--2771518-->  
Os usuários finais agora podem iniciar ações de aplicativos e dispositivos no Portal da Empresa do Windows usando atalhos de teclado (aceleradores).



## <a name="august-2018"></a>Agosto de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="new-user-experience-update-for-the-company-portal-website"></a>Nova atualização de experiência do usuário para o site do Portal da Empresa

<!--2000968-->  
Com base nos seus comentários, adicionamos novos recursos para o site de Portal da empresa. Você fará uma melhoria significativa na funcionalidade existente e na usabilidade dos seus dispositivos Android, iOS e Windows. Áreas do site receberam um novo design, moderno e responsivo. Essas áreas incluem detalhes do dispositivo, comentários e suporte e visão geral do dispositivo. Você também verá os seguintes aprimoramentos:

- Fluxos de trabalho simplificados em todas as plataformas de dispositivo
- Fluxos de identificação e registro de dispositivo aprimorados
- Mensagens de erro mais úteis
- Linguagem mais amigável, menos jargão técnico
- Capacidade de compartilhar links diretos para aplicativos
- Melhor desempenho para grandes catálogos de aplicativos
- Maior acessibilidade para todos os usuários



## <a name="july-2018"></a>Julho de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="updated-intune-app-sdk-for-android-is-now-available"></a>O SDK do Aplicativo Intune para Android atualizado está disponível

<!--2744271-->  
Uma versão atualizada do SDK do Intune App para Android está disponível para dar suporte a versão do Android pizza de 9. Se você for desenvolvedor de aplicativo e usa o SDK do Intune para Android, instale a versão atualizada do SDK do aplicativo Intune. Essa atualização garante o funcionamento esperado dessa funcionalidade do Intune em seus aplicativos Android nos dispositivos com Android 9 Pie. Esta versão do SDK do Aplicativo Intune fornece um plug-in interno que executa as atualizações do SDK. Você não precisa reescrever qualquer código integrado. Para saber mais, confira [SDK do Intune para Android](https://github.com/msintuneappsdk/ms-intune-app-sdk-android).

Se você estiver usando o estilo de selo antigo para Intune, alterne para usar o ícone de pasta. Saiba mais sobre a identidade visual em [Sistema de atribuição de selo do aplicativo Intune](https://github.com/msintuneappsdk/intune-app-partner-badge).

#### <a name="support-for-security-enhancement-in-intune-service"></a>Suporte para o aprimoramento de segurança no serviço Intune

<!--2520152-->  
Agora você pode especificar que os dispositivos sem quaisquer políticas de conformidade atribuída não são compatíveis em híbrida. Defina essa configuração no Intune no portal do Azure. É altamente recomendável que você habilite esse recurso para proteger seus recursos internos.

Esse recurso está desativado por padrão em locatários híbridos. Quando você habilita esse recurso, os dispositivos que não têm uma política de conformidade atribuída são considerados em não conformidade. Se você também habilitar o acesso condicional, esses dispositivos perderão o acesso aos recursos internos. Esses recursos podem ser do Outlook ou do SharePoint, com base em políticas de acesso condicional em seu ambiente. Se você deixar essa configuração desativada, esses dispositivos continuarão a ter o mesmo nível de acesso que têm atualmente.

Para ajudá-lo a determinar o impacto de ativar esse recurso, fornecemos um [script na Galeria TechNet](https://gallery.technet.microsoft.com/SQL-Query-for-Hybrid-MDM-5bcb8695). Quando você executa esse script em seu banco de dados do Configuration Manager, ele lista os dispositivos aos quais nenhuma política de conformidade é direcionada.

Para obter mais informações, consulte os seguintes artigos:

- Postagem no blog [Aprimoramentos de Segurança no Serviço Intune](https://aka.ms/compliance_policies)
- [Políticas de conformidade de dispositivo no Configuration Manager](/sccm/mdm/deploy-use/device-compliance-policies)

#### <a name="updates-to-out-of-compliance-messages-in-company-portal-app"></a>Atualizações para as mensagens de fora de conformidade no aplicativo Portal da Empresa

<!--1832222-->  
Podemos está revisando as mensagens que os usuários de dispositivos Consulte quando um dispositivo está fora de conformidade. As mensagens mantêm seus significados originais, mas são atualizadas com linguagem mais amigável e jargão menos técnico. Também estamos atualizando os links para as etapas de documentação e correção para mantê-los atualizados.  

O seguinte texto é um exemplo das melhorias nas mensagens que você vê:  

- Antes: *Este dispositivo não tiver contatado o serviço do Intune no período de tempo especificado exigido pelo seu administrador de TI. Para resolver esse problema, abra o aplicativo do portal da empresa no seu dispositivo e clique no botão Verificar Conformidade.*  

- Depois de: *Seu dispositivo não foi marcada com sua organização em instantes. Para restabelecer uma conexão, abra o aplicativo Portal da Empresa no dispositivo e toque em Verificar Configurações do seu dispositivo.*  

#### <a name="select-device-categories-by-using-the-access-work-or-school-settings"></a>Selecionar as categorias de dispositivo usando as configurações de Acessar Trabalho ou Escola

<!--1058963-->  
Se você tiver habilitado [mapeamento do grupo de dispositivos](https://docs.microsoft.com/intune/device-group-mapping), os usuários no Windows 10 agora serão solicitados a selecionar uma categoria de dispositivo após o registro por meio das **Connect** botão na **configurações**  >  **Contas** > **acessar trabalho ou escola**.  

#### <a name="new-browsing-experiences-in-the-company-portal-app-for-windows"></a>Novas experiências de navegação no aplicativo Portal da Empresa para Windows

<!--2317227-->  
Agora ao procurar ou pesquisar para aplicativos no aplicativo Portal da empresa para Windows, alternar entre existente **blocos** exibição e adicionados recentemente **detalhes** modo de exibição. A nova exibição lista detalhes do aplicativo, como nome, editor, data de publicação e status da instalação.

Na página **Aplicativos**, exibição **Instalado**, é possível ver detalhes sobre instalações de aplicativos concluídos e em andamento. Para ver a aparência da nova exibição, veja [O que há de novo na interface do usuário](https://docs.microsoft.com/intune/whats-new-app-ui).

#### <a name="more-opportunities-to-sync-in-the-company-portal-app-for-windows"></a>Mais oportunidades para sincronização no aplicativo do Portal da Empresa para Windows

<!--2683177-->  
O aplicativo de Portal da empresa para Windows agora permite que você inicie uma sincronização diretamente da barra de tarefas do Windows e do menu Iniciar. Esse recurso será especialmente útil se a sua única tarefa for sincronizar dispositivos e obter acesso aos recursos corporativos. Para acessar o novo recurso, clique com o botão direito do mouse no ícone Portal da Empresa fixado na barra de tarefas ou no menu Iniciar. Nas opções de menu, selecione **sincronizar esse dispositivo**. (Esse menu também é chamado para de lista de atalhos.) O Portal da Empresa se abre para a página **Configurações** e inicia sua sincronização. Para o procedimento atualizado, veja [Sincronizar seu dispositivo Windows manualmente](https://docs.microsoft.com/intune/intune-user-help/sync-your-device-manually-windows#sync-from-device-taskbar-or-start-menu).



## <a name="june-2018"></a>Junho de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="access-to-macos-company-portal-pre-release-build"></a>Acesso ao build de pré-lançamento do Portal da Empresa do macOS

<!--1734766-->  
Usando Microsoft AutoUpdate, inscreva-se para recebimento das compilações no início ao ingressar no programa Insider. A inscrição permite que você use o Portal da Empresa atualizado antes que ele esteja disponível para seus usuários finais.

#### <a name="intune-app-protection-policies-and-microsoft-edge"></a>Políticas de proteção de aplicativo do Intune e Microsoft Edge

<!--1818968,1818969-->  
O navegador Microsoft Edge para dispositivos móveis (iOS e Android) agora é compatível com as políticas de proteção de aplicativo do Microsoft Intune. Os usuários de dispositivos iOS e Android que entram com suas contas corporativas do Azure Active Directory no aplicativo Microsoft Edge são protegidos pelo Intune. Nos dispositivos iOS, a política para **Exigir navegador gerenciado para conteúdo da Web** permite que os usuários abram links no Microsoft Edge quando ele é gerenciado.



## <a name="may-2018"></a>Maio de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="requesting-help-in-the-company-portal-for-windows-10"></a>Solicitar ajuda no aplicativo Portal da Empresa para Windows 10

<!--1874137-->  
O Portal da Empresa para Windows 10 agora envia logs de aplicativos diretamente para a Microsoft quando o usuário inicia o fluxo de trabalho para obter ajuda com um problema. Esse comportamento facilita a solução de problemas que são gerados para a Microsoft.  


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)

#### <a name="android-for-work-and-lookout-onboarding-moved-to-intune-on-azure"></a>Integração do Android for Work e do Lookout movida para o Intune no Azure

<!--2355022,2357366-->  
Com a atualização mais recente do Intune, você pode habilitar e gerenciar a integração do Android for Work e a integração da defesa contra ameaças móveis do Lookout em locatários de gerenciamento de dispositivo móvel híbrido do Intune no portal do Azure. Antes da atualização, essas configurações apenas podiam ser definidas no portal Clássico do Intune (Silverlight).

Observação: Lookout é o provedor MTD (defesa contra) contra ameaças móveis só tem suportado em híbrida. Se você já tiver realizado a integração com qualquer outro provedor de MTD, ele ainda aparecerá no Intune no portal do Azure. Se você excluir o conector dele, não será mais possível adicioná-lo novamente.

Essas alterações não afetam a funcionalidade existente. Continue a usar o console do Configuration Manager para gerenciar os aplicativos relacionados, os relatórios e as políticas.

Para obter mais informações, consulte os seguintes artigos:

- [Configurar o gerenciamento de dispositivo híbrido Android](/sccm/mdm/deploy-use/enroll-hybrid-android)
- [Gerenciar o acesso aos recursos da empresa com base em dispositivo, rede e risco do aplicativo](/sccm/mdm/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)

#### <a name="support-for-new-versions-of-cisco-anyconnect-client-for-ios"></a>Suporte para novas versões do cliente Cisco AnyConnect para iOS

<!--1357393-->  
Você pode habilitar o suporte para Cisco AnyConnect para iOS versão 4.0.7 ou posterior. Se fizer isso, os perfis de VPN do Cisco AnyConnect existentes serão rotulados como **Cisco Legacy AnyConnect** e continuarão a funcionar como antes. A opção **Cisco AnyConnect** é para perfis de VPN novos que funcionam com o Cisco AnyConnect em iOS na versão 4.0.7 ou posterior.

  > [!Tip]  
  > O Cisco AnyConnect 4.0.07x e posterior para iOS foi introduzido na versão 1802, como um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features). Na [atualização 4163547](https://support.microsoft.com/help/4163547) da versão 1802, esse recurso deixou de ser um recurso de pré-lançamento.  

> [!Note]  
> Continue a usar a opção **Cisco Legacy AnyConnect** para perfis de VPN do macOS.



## <a name="april-2018"></a>Abril de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="intune-adapts-to-fluent-design-system-in-the-company-portal-app-for-windows-10"></a>O Intune se adapta ao Fluent Design System no aplicativo Portal da empresa para o Windows 10

<!--1195010-->  
O aplicativo do Portal da Empresa do Intune para Windows 10 foi atualizado com a [Visualização de navegação do Fluent Design System](/windows/uwp/design/basics/navigation-basics). Ao longo da lateral do aplicativo, observe uma lista vertical estática de todas as páginas de nível superior. Clique em qualquer link para visualizar e alternar rapidamente entre as páginas. Esta atualização é a primeira de várias que você verá como parte do nosso esforço contínuo para criar uma experiência mais adaptável, empática e familiar no Intune. Para ver a aparência atualizada, acesse [Novidades na interface do usuário do aplicativo](/intune/whats-new-app-ui).

#### <a name="improved-device-tiles-in-the-windows-10-company-portal"></a>Blocos de dispositivo aprimorados no Portal da Empresa do Windows 10

<!--2213364-->  
Os blocos foram atualizados para serem mais acessíveis a usuários com deficiência visual e para desempenho melhor com ferramentas de leitura de tela.

#### <a name="test-the-company-portal-for-macos-on-virtual-machines"></a>Testar o Portal da Empresa para macOS em máquinas virtuais

<!--2216679-->  
Publicamos uma orientação para ajudar os administradores de TI a testar o aplicativo Portal da Empresa para macOS em máquinas virtuais em Parallels Desktop e VMware Fusion. Para obter mais informações, veja [Registrar máquinas virtuais macOS para testes](/intune/macos-enroll#enroll-virtual-macos-machines-for-testing).

#### <a name="send-diagnostic-reports-in-company-portal-app-for-macos"></a>Enviar relatórios de diagnóstico no aplicativo Portal da Empresa para macOS

<!--2216677-->  
O aplicativo Portal da Empresa para dispositivos macOS foi atualizado para melhorar o modo como os usuários relatam erros relacionados ao Intune. No aplicativo Portal da Empresa, seus funcionários podem:

- Carrega relatórios de diagnóstico diretamente para a equipe de desenvolvedores Microsoft.
- Envie por email uma ID de incidente à equipe de suporte de TI da sua empresa.

#### <a name="updated-help-experience-on-company-portal-app-for-android"></a>Experiência de Ajuda atualizada no aplicativo Portal da Empresa para Android

<!--1631531-->  
Atualizamos a experiência da Ajuda no aplicativo Portal da Empresa para Android para alinhar às práticas recomendadas para a plataforma Android. Agora, quando os usuários encontram um problema no aplicativo, eles podem clicar em **Menu** > **Ajuda** e:

- Carregar os logs de diagnóstico para a Microsoft.
- Enviar um email que descreva o problema e a ID do incidente para uma pessoa de suporte da empresa.

#### <a name="update-where-to-configure-your-app-protection-policies"></a>Atualizar o local em que você configura as políticas de proteção do aplicativo

<!--2144597-->  
No portal do Azure no serviço do Microsoft Intune, vamos temporariamente direcionado dos **Intune App Protection** área para o **aplicativo móvel** seção. Todas as suas políticas de proteção de aplicativo já estão na seção **Aplicativo Móvel** do Intune, em configuração do aplicativo. Em vez de acessar a Proteção de Aplicativo do Intune, basta acessar o Intune. Em abril de 2018, paramos o redirecionamento e removemos completamente a **Proteção de Aplicativo do Intune**. Após esse período, há apenas um local para políticas de proteção de aplicativo no Intune.

**Como essa alteração me afeta?** Essa alteração afeta os clientes do Intune autônomo e os clientes do híbrido (Intune com o Configuration Manager). Essa integração ajudará a simplificar a administração do gerenciamento da nuvem.

**O que preciso fazer para me preparar para essa alteração?** Marque o **Intune** como um favorito, em vez da **Proteção de Aplicativo do Intune**. Familiarize-se com o fluxo de trabalho de política de proteção de aplicativo na área **Aplicativo móvel** no Intune. Redirecionaremos por um breve período e então removeremos a **Proteção de Aplicativo**. Lembre-se de que todas as políticas de proteção de aplicativos já estão no Intune e você pode modificar qualquer política de acesso condicional. Para saber mais sobre como modificar políticas de acesso condicional, confira [Acesso condicional no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Para obter mais informações, consulte [quais são as políticas de proteção de aplicativo?](https://docs.microsoft.com/intune/app-protection-policy).

#### <a name="user-experience-update-for-the-company-portal-app-for-ios"></a>Atualização de experiência do usuário para o aplicativo Portal da Empresa para iOS

<!--1412866-->  
Lançamos uma atualização principal da experiência do usuário para o aplicativo Portal da Empresa para iOS. A atualização apresenta um novo design de visual completo que inclui aparência e modernizada. Mantivemos a funcionalidade do aplicativo, mas aumentamos sua usabilidade e a acessibilidade.  

Você também verá:

- Suporte para iPhone X.
- Inicialização do aplicativo e carregamento de respostas mais rápidos, para economizar tempo dos usuários.
- Barras de progresso adicionais para fornecer aos usuários as informações de status mais atualizadas.
- Melhorias na forma de carregar os logs aos usuários para ser mais fácil relatar se algo der errado.  

Para ver a aparência atualizada, acesse [Novidades na interface do usuário do aplicativo](https://docs.microsoft.com/intune/whats-new-app-ui).



## <a name="march-2018"></a>Março de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="windows-company-portal-send-feedback-option-may-no-longer-work"></a>Opção de enviar comentários do Portal da Empresa do Windows pode não funcionar mais

<!--2070166-->  
O aplicativo de Portal da Empresa do Windows tem uma opção de ‘Enviar Comentários’ permitindo que os usuários enviem comentários sobre o aplicativo para a Microsoft. A partir de 30 de abril de 2018, essa opção continua a ter suporte apenas no aplicativo do Portal da Empresa do Windows 10 em execução no Windows 10 versão 1607 e posterior.

**Como essa alteração me afeta?**

Se você não tiver o aplicativo do Portal da Empresa do Windows instalado para usuários finais, desconsidere esta mensagem.

Se qualquer um dos seus usuários finais tiver o aplicativo de Portal da Empresa, a partir de 30 de abril, o botão "Enviar Comentários" não funcionará mais para o aplicativo nos seguintes cenários:  

- Aplicativo de Portal da Empresa do Windows 10 no Windows 10 versão 1507 e versão 1511  

- Aplicativo do Portal da Empresa do Windows Phone 8.1  

Para dispositivos afetados, a opção ‘Enviar Comentários’ falha e não tem êxito mesmo ao tentar novamente. Para enviar comentários à Microsoft sobre experiências nessas plataformas, existem canais de comentários alternativos listados abaixo.

**O que preciso fazer para me preparar para essa alteração?**

Informe aos usuários finais sobre essa alteração e atualize todas as diretrizes para os usuários se necessário.

Informe os usuários finais usando o Portal da Empresa no Windows Phone 8.1, Windows 10 versão 1507 e Windows 10 versão 1511 de que eles têm dois canais de comentários alternativos disponíveis. Eles podem:  

- Use o aplicativo Hub de Comentários no Windows 10  
- Enviar um email para WinCPfeedback@microsoft.com  

Peça aos usuários finais no Windows 10 versão 1607 ou posterior para atualizar para a versão mais recente do Portal da Empresa do Windows disponível na Microsoft Store.

#### <a name="azure-active-directory-web-sites-can-require-the-intune-managed-browser-app-and-support-single-sign-on-for-the-managed-browser-public-preview"></a>Os sites do Azure Active Directory podem exigir o aplicativo Intune Managed Browser e dar suporte ao Logon Único para o Managed Browser (Versão Prévia Pública)

<!-- 710595 -->  
Usando o Azure AD (Azure Active Directory), agora você pode restringir o acesso a sites em dispositivos móveis para o aplicativo Intune Managed Browser. No Managed Browser, os dados do site permanecerão seguros e separados dos dados pessoais do usuário final. Além disso, o Managed Browser dará suporte aos recursos de Logon Único para sites protegidos pelo Azure AD. Entrar no Managed Browser ou usar o Managed Browser em um dispositivo com outro aplicativo gerenciado pelo Intune permite que o Managed Browser acesse sites corporativos protegidos pelo Azure AD sem precisar inserir as credenciais. Essa funcionalidade se aplica a sites como o OWA (Outlook Web Access) e o SharePoint Online, bem como outros sites corporativos, como os recursos de intranet acessados por meio do Proxy de Aplicativo do Azure.



## <a name="february-2018"></a>Fevereiro de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Suporte ao Portal da Empresa para macOS para registros que usam o Gerenciador de Registros do Dispositivo**  
    Os usuários agora podem usar o Gerenciador de Registro do Dispositivo ao se inscreverem no Portal da Empresa do macOS.
    <!-- 1352411 -->  


## <a name="january-2018"></a>Janeiro de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Aprovar o aplicativo do Portal da Empresa para Android for Work**  
  Se a sua organização usa o Android for Work, aprove manualmente o aplicativo Portal da Empresa para Android. Assim, ele continuará a receber atualizações automáticas da Google Play Store gerenciada.
  <!--1797090 -->  

- **As Políticas de Acesso Condicional para o Intune só estão disponíveis no Portal do Azure**   
  A partir desta versão, é preciso configurar e gerenciar suas políticas de Acesso Condicional no [Portal do Azure](https://portal.azure.com) do **Acesso Condicional** do **Azure Active Directory** > . Para sua conveniência, você também pode acessar essas configurações do Intune no portal do Azure em **Intune** > **Acesso Condicional**.
  <!-- 1737088 1634311 -->  

- **Atualizações para emails de conformidade**    
  Quando um email é enviado para relatar um dispositivo incompatível, os detalhes sobre o dispositivo não compatível são incluídos na mensagem. 
  <!--1637547 -->  

- **Nova funcionalidade para a ação "Resolver" para dispositivos Android**    
  O aplicativo Portal da Empresa para Android está expandindo a ação "Resolver" para **Atualizar configurações do dispositivo** a fim de resolver [problemas de criptografia de dispositivo](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android).
  <!--1583480-->  

- **Bloqueio remoto disponível no aplicativo de Portal da Empresa para Windows 10**    
  Agora, os usuários finais podem bloquear remotamente seus dispositivos do aplicativo do Portal da Empresa para Windows 10. Essa ação não será exibida para o dispositivo local que eles estiverem usando ativamente.
  <!--676506-->  

- **Resolução mais fácil de problemas de conformidade para o aplicativo Portal da Empresa para Windows 10**   
  Usuários finais com dispositivos Windows podem tocar no motivo da não conformidade no aplicativo Portal da Empresa. Quando possível, essa ação os levará diretamente para a localização correta no aplicativo de configurações para corrigir o problema.
  <!--676546-->    



## <a name="december-2017"></a>Dezembro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Implantações de aplicativo disponíveis agora com suporte no Android Enterprise**    
  Agora você pode implantar aplicativos do Android Enterprise (anteriormente Android for Work) como **Disponíveis**, além de **Obrigatórios**. Para obter detalhes, consulte [Criar aplicativos Android com o System Center Configuration Manager](/sccm/mdm/deploy-use/creating-android-applications).



## <a name="november-2017"></a>Novembro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Protocolo de texto permitido de aplicativos gerenciados**  
  Aplicativos gerenciados pelo SDK do Aplicativo do Intune podem enviar mensagens SMS.
  <!-- 1414050  -->   

- **O aplicativo do Portal da Empresa para macOS está disponível**   
  O Portal da Empresa do Intune no macOS está com a experiência atualizada. Ela foi otimizada para exibir com clareza todas as notificações de conformidade e informações de que os usuários precisam para todos os dispositivos que eles registram. E, quando o Portal da Empresa do Intune tiver sido implantado em um dispositivo, a Atualização Automática da Microsoft para macOS fornecerá atualizações para ele. Baixe o novo Portal da Empresa do Intune para macOS fazendo o logon no site do Portal da Empresa do Intune a partir de um dispositivo macOS.
  <!--1541700-->   

- **Agora o Microsoft Planner faz parte da lista do MAM (gerenciamento de aplicativo móvel) de aplicativos aprovados**    
  Agora o aplicativo Microsoft Planner para iOS e Android faz parte dos aplicativos aprovados para o MAM (gerenciamento de aplicativo móvel). Configure o aplicativo da Proteção de Aplicativo do Intune no portal do Azure para todos os locatários. Para obter detalhes, confira [Lista MAM de aplicativos aprovados](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).
  <!-- 1248473 -->    

- **Acesso a logs de aplicativos gerenciados para iOS**    
  Agora os usuários finais com o Browser gerenciado instalado podem exibir o status de gerenciamento de todos os aplicativos publicados da Microsoft e enviar logs para solucionar problemas de seus aplicativos iOS gerenciados.
  <!-- 1469920 -->    

  Saiba como habilitar o modo de solução de problemas no Managed Browser em um dispositivo iOS, consulte [How to access to managed app logs using the Managed Browser on iOS](https://docs.microsoft.com/intune/app-configuration-managed-browser#how-to-access-to-managed-app-logs-using-the-managed-browser-on-ios) (Como acessar logs de aplicativos gerenciados usando o Managed Browser no iOS).

- **Melhorias no fluxo de trabalho de configuração do dispositivo no Portal da Empresa para iOS na versão 2.9.0**    
  Melhoramos o fluxo de trabalho de configuração de dispositivo no aplicativo do Portal da Empresa para iOS. A linguagem é mais fácil de usar e combinamos as telas sempre que possível. Também tornamos a linguagem mais específica para sua empresa, usando o nome da empresa em todo o texto da instalação. Veja esse fluxo de trabalho atualizado na página [novidades na interface do usuário do aplicativo](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-november-13-2017).

- **Solicitações de comentários para o aplicativo do Portal da Empresa para Android**    
  Agora o aplicativo do Portal da Empresa para Android solicita comentários do usuário final. Este comentário é enviado diretamente para a Microsoft e fornece aos usuários finais uma oportunidade de avaliar o aplicativo na Google Play Store pública. Os comentários não são obrigatórios e podem facilmente ser ignorados para que os usuários possam continuar usando o aplicativo. 
  <!--1165249-->    

- **Informar os usuários finais sobre quais informações do dispositivo podem ser vistas para dispositivos Windows 10**    
  Adicionamos **Tipo de propriedade** à tela Detalhes do dispositivo no aplicativo do Portal da Empresa para Windows 10. Essas informações permitem que os usuários obtenham mais informações sobre privacidade diretamente dos documentos do usuário final do Intune. Eles também pode encontrar essas informações na tela **Sobre**.
  <!--1337920-->    

- **Nova ação "Resolver" disponível para dispositivos Android**    
  O aplicativo do Portal da Empresa para Android está introduzindo uma ação "Resolver" na página _Atualizar as configurações do dispositivo_. Selecionar esta opção leva o usuário final diretamente para a configuração que está causando a incompatibilidade com o seu dispositivo. O aplicativo do Portal da Empresa para Android oferece suporte atualmente a essa ação para as configurações de [senha do dispositivo](https://docs.microsoft.com/intune-user-help/set-your-pin-or-password-android), [criptografia do dispositivo](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android), [depuração de USB](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-usb-debugging-android), e [Fontes Desconhecidas](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-unknown-sources-android). 
  <!--1583480-->    


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)

- **Ações de não conformidade**    
  Agora é possível configurar uma sequência de ações ordenadas por tempo aplicadas aos dispositivos que estão fora de conformidade. Por exemplo, é possível notificar os usuários sobre dispositivos que não estão em conformidade por email ou marcá-los como não em conformidade. Para obter detalhes, consulte [Set up actions for non-compliance](/sccm/mdm/deploy-use/actions-for-noncompliance) (Configurar ações de não conformidade).
  <!--1321366 -->  

- **Novas configurações de política de gerenciamento de aplicativo móvel**     
  As configurações a seguir foram adicionadas nas configurações de política de gerenciamento de aplicativos móveis:
  - **Desabilitar sincronização de contatos**: impede que o aplicativo salve dados no aplicativo Contatos nativo do dispositivo.
  - **Desabilitar impressão**: impede que o aplicativo imprima dados corporativos ou de estudante.
  <!-- 1324760 -->    

  Veja [proteger aplicativos usando políticas de proteção de aplicativos no Configuration Manager](/sccm/mdm/deploy-use/protect-apps-using-mam-policies) para testar as novas configurações de política de proteção do aplicativo.

- **Suporte a dispositivos com Windows 10 ARM64**     
  Os cenários híbridos de MDM (gerenciamento de dispositivo móvel) têm suporte em dispositivos ARM64 executando o Windows 10 quando esses dispositivos ficarem disponíveis. Para obter mais detalhes, confira [Suporte a dispositivos Windows 10 ARM64](/sccm/core/plan-design/changes/whats-new-in-version-1710#windows-10-arm64-device-support).
  <!-- 1355000 -->    

- **Melhoria na experiência do perfil de VPN no Console do Configuration Manager**     
  Nesta versão, atualizamos as páginas do assistente de perfil VPN e de propriedades para exibir as configurações apropriadas para a plataforma selecionada. Essa funcionalidade estava disponível anteriormente no Configuration Manager Technical Preview 1709. Agora, ele está disponível em implantações híbridas com o Intune e com a versão 1710 do Configuration Manager (Branch Atual). Para saber mais, confira [Melhoria da experiência do perfil de VPN no Console do Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1710#improved-vpn-profile-experience-in-configuration-manager-console).
  <!-- 1318232 -->  


### <a name="new-in-configuration-manger-technical-preview-1711"></a>Novo no Configuration Manager Technical Preview 1711

- **Novas opções de política de conformidade para Windows 10**   
  Agora é possível configurar as novas opções de políticas de conformidade para dispositivos com Windows 10. As novas configurações incluem políticas de Firewall, Controle de Conta de Usuário, Windows Defender Antivírus e controle de versões de build do sistema operacional. Para obter mais detalhes, confira [Novas opções de política de conformidade para Windows 10](/sccm/core/get-started/capabilities-in-technical-preview-1711#new-compliance-policy-options-for-windows-10).



## <a name="october-2017"></a>Outubro de 2017

### <a name="new-in-configuration-manager-technical-preview-1709"></a>Novo no Configuration Manager Technical Preview 1709

- **Melhoria da experiência do perfil de VPN no Console do Configuration Manager**      
  Agora, as configurações de perfil VPN são filtradas de acordo com a plataforma. Quando você cria novos perfis de VPN, cada plataforma com suporte contém apenas as configurações apropriadas para a plataforma. Os perfis de VPN existentes não são afetados. Leia mais sobre essa mudança [aqui](/sccm/core/get-started/capabilities-in-technical-preview-1709#improved-vpn-profile-experience-in-configuration-manager-console).
  <!-- 1313282 -->  


### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune  

- **Ajude seus usuários a se ajudarem com o aplicativo Portal da Empresa para Android**     
  O aplicativo Portal da Empresa para Android adicionou instruções para os usuários finais para ajudá-los a entender e, sempre que possível, solucionar problemas de forma independente em novos casos de uso.
    - Se os usuários finais tiverem atingido o número máximo de dispositivos que eles podem adicionar, serão levados ao [Portal do Azure Active Directory](https://account.activedirectory.windowsazure.com/r/#/profile) para remover um dispositivo.
    - Os usuários finais recebem etapas a serem seguidas para ajudá-los a [corrigir erros de ativação em dispositivos Samsung Knox](https://go.microsoft.com/fwlink/?linkid=859718) ou a [desligar o modo de economia de energia](https://docs.microsoft.com/intune-user-help/power-saving-mode-android). Se nenhuma dessas soluções resolver o problema, forneceremos uma explicação de como [enviar logs para a Microsoft](https://docs.microsoft.com/intune-user-help/send-logs-to-microsoft-android).
  <!-- 1573324, 1573150, 1558616, 1564878 -->      

- **Indicador de progresso da instalação do dispositivo no Portal da Empresa para Android**     
  O aplicativo do Portal da Empresa para Android mostra um indicador de progresso da instalação do dispositivo quando um usuário está registrando seu dispositivo. O indicador mostra novos status, começando com "Configurando seu dispositivo...", em seguida, "Registrando seu dispositivo...", "Concluindo o registro do seu dispositivo..." e "Concluindo a instalação do seu dispositivo...".  
  <!--1565657-->    

- **Suporte a autenticação baseada em certificado no Portal da Empresa para iOS**    
  Adicionamos suporte para CBA (autenticação baseada em certificado) no aplicativo do Portal da Empresa para iOS. Usuários com CBA inserem seu nome de usuário e então tocam no link "Entrar com um certificado". CBA já é compatível com os aplicativos Portal da Empresa para Android e Windows. Saiba mais na página para [Entrar no aplicativo Portal da Empresa](https://docs.microsoft.com/intune-user-help/sign-in-to-the-company-portal).
  <!--1029830-->   

- **Aprimoramentos no fluxo de trabalho de configuração do dispositivo no Portal da Empresa**     
  Melhoramos o fluxo de trabalho de configuração de dispositivo no aplicativo Portal da Empresa para Android. A linguagem é mais fácil de usar e mais específica para sua empresa. Combinamos as telas sempre que possível. Veja esses aprimoramentos na página [Novidades na interface do usuário do aplicativo](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-october-2-2017).
  <!--1490692-->     

- **Orientação aprimorada para a solicitação de acesso aos contatos em dispositivos Android**     
  O aplicativo Portal da Empresa para Android geralmente exige que o usuário final aceite a permissão de Contatos. Se um usuário final recusar esse acesso, ele verá uma notificação no aplicativo alertando-o para concedê-lo para acesso condicional. 
  <!--1484985-->     

- **Correção da inicialização segura para Android**     
  Os usuários finais com dispositivos Android podem tocar no motivo da não conformidade no aplicativo Portal da Empresa. Quando possível, essa ação os levará diretamente para o local correto no aplicativo de configurações para corrigir o problema. 
  <!--1490712-->    

- **Notificações por push adicionais para usuários finais no aplicativo Portal da Empresa para Android Oreo**    
  Os usuários finais veem notificações adicionais para indicar quando o aplicativo Portal da Empresa para Android Oreo está executando tarefas em segundo plano, por exemplo, recuperando as políticas do serviço Intune. As notificações aumentam a transparência para os usuários finais, informando sobre quando o Portal da Empresa estiver executando tarefas administrativas em seu dispositivo. Esse aprimoramento faz parte da geral [otimização da interface de usuário do Portal da empresa](https://blogs.technet.microsoft.com/intunesupport/2017/08/21/android-8-0-o-behaviour-changes-and-microsoft-intune) para o aplicativo de Portal da empresa para Android Oreo. 
  <!--1475932 -->     

- **Novos comportamentos para o aplicativo Portal da Empresa para Android com perfis de trabalho**     
  Quando você registra um dispositivo com Android for Work com um perfil de trabalho, é o aplicativo Portal da Empresa no perfil de trabalho que executa tarefas de gerenciamento no dispositivo. 

  A menos que você esteja usando um aplicativo habilitado para MAM no perfil particular, o aplicativo Portal da Empresa para Android não terá qualquer uso. Para melhorar a experiência do perfil de trabalho, o Intune oculta automaticamente o aplicativo Portal da Empresa pessoal após um registro de perfil de trabalho bem-sucedido.

  O aplicativo Portal da Empresa para Android pode ser habilitado a qualquer momento no perfil pessoal navegando até [Portal da Empresa na Play Store](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) e tocando em **Habilitar**.
  <!--1485783-->    

- **Portal da Empresa para Windows 8.1 e Windows Phone 8.1 mudando para o modo de manutenção**    
  Foi adicionado um aviso para anunciar que os aplicativos Portal da Empresa para Windows 8.1 e Windows Phone 8.1 estão mudando para modo de manutenção. Para obter mais detalhes, veja [Avisos](#notices).  
  <!--1428681-->    

- **Bloquear registro de dispositivo Samsung Knox sem suporte**   
  O aplicativo Portal da Empresa tenta registrar apenas os dispositivos Samsung Knox com suporte. Para evitar erros de ativação do KNOX que impedem o registro do MDM, a tentativa do registro do dispositivo só ocorrerá se o dispositivo for exibido na [lista de dispositivos publicada pela Samsung](https://www.samsungknox.com/knox-supported-devices/knox-workspace). Os dispositivos Samsung podem ter números de modelo que oferecem suporte a KNOX, enquanto outros não. Verifique a compatibilidade do Knox com o revendedor de seu dispositivo antes de comprar e implantar. Encontre a lista completa de dispositivos verificados nas [configurações de política do Android e Samsung KNOX Standard](https://docs.microsoft.com/intune-classic/deploy-use/android-policy-settings-in-microsoft-intune#supported-samsung-knox-standard-devices).
  <!-- 1490695 -->     

- **Fim do suporte para Android 4.3 e inferior**     
  Um aviso foi adicionado para o fim do suporte para Android 4.3 e inferior. Para obter mais detalhes, veja [Avisos](#notices).
  <!--1171126, 1326920 -->     

- **Informar aos usuários finais quais informações do dispositivo podem ser vistas em dispositivos registrados**     
  Estamos adicionando o **Tipo de Propriedade** à tela de Detalhes do Dispositivo em todos os aplicativos do Portal da Empresa. Essas informações permitirão que os usuários obtenham mais informações sobre privacidade diretamente do artigo [Quais informações sua empresa pode ver?](https://docs.microsoft.com/intune-user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune). Esse aprimoramento será implantado em breve em todos os aplicativos do Portal da Empresa. Anunciamos essa funcionalidade para iOS em [setembro](https://docs.microsoft.com/intune/whats-new#week-of-september-11-2017). 
  <!--1165314-->     



## <a name="september-2017"></a>Setembro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune     

- **Ação de atualização adicionada ao aplicativo Portal da Empresa para Windows 10**    
    O aplicativo Portal da Empresa para Windows 10 permite que os usuários atualizem os dados no aplicativo deslizando para atualizar ou, em áreas de trabalho, pressionando F5.
    <!-- 1132468 -->     

- **Mostrar os usuários finais quais informações do dispositivo podem ser vistas para o iOS**   
    Adicionamos **tipo de propriedade** para a tela de detalhes do dispositivo no aplicativo Portal da empresa para iOS. Essas informações permitem que os usuários obtenham mais informações sobre privacidade diretamente dos documentos do usuário final do Intune. Eles também pode encontrar essas informações na tela Sobre. 
    <!--739894-->    

- **Frases mais fáceis de entender para o aplicativo Portal da Empresa para Android**   
    O processo de registro para o aplicativo Portal da Empresa para Android foi simplificado com o novo texto para facilitar a inscrição para usuários finais. Se você tiver a documentação de inscrição personalizada, atualize-a para refletir as novas telas. Você pode localizar as imagens de amostra na nossa página [Atualizações de interface do usuário para aplicativos de usuário final do Intune](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-september-11-2017).
    <!---1396349-->    

- **Aplicativo Portal da Empresa do Windows 10 adicionado à política de permissão de Proteção de Informações do Windows**    
    O aplicativo Portal da Empresa do Windows 10 foi atualizado para dar suporte ao WIP (Proteção de Informações do Windows). O aplicativo pode ser adicionado à política de permissão do WIP. Com essa alteração, o aplicativo não precisa mais ser adicionado à lista **Isento**. 

    Apenas um item de configuração WIP única pode ser entregue a um dispositivo. Se dois itens de configuração WIP forem direcionados para o mesmo dispositivo, nenhuma política WIP será aplicável.
    <!-- 677129 -->    

- **Aviso de fim de suporte adicionado para iOS 8.0**    
    Um aviso foi adicionado para o fim do suporte para iOS 8.0. Para obter mais detalhes, veja [Avisos](#notices).



## <a name="august-2017"></a>Agosto de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune     

- **Nova experiência conectada para usuários do Portal da Empresa Android e usuários da Política de Proteção de Aplicativo**    
  Os usuários finais agora podem procurar aplicativos, gerenciar dispositivos e exibir as informações de contato de TI usando o aplicativo Portal da Empresa Android sem inscrever os respectivos dispositivos Android. Além disso, se um usuário final já usa um aplicativo protegido pelas Políticas de Proteção de Aplicativo do Intune e iniciar o Portal da Empresa Android, o usuário final não receberá mais uma solicitação para registrar o dispositivo.
  <!-- 621669 -->  



## <a name="notices"></a>Avisos

### <a name="update-your-android-company-portal-app-to-the-latest-version"></a>Atualize o aplicativo de Portal da empresa Android para a versão mais recente

<!-- 4536963 -->

Periodicamente, o Intune lança atualizações para o aplicativo de Portal da empresa Android. Em novembro de 2018, lançamos uma atualização do Portal da empresa que inclui uma opção de back-end para preparar para a alteração do Google de sua plataforma de notificação existente para o do Google Firebase Cloud Messaging (FCM). Quando o Google desativa sua plataforma de notificação existente e move para FCM, os usuários precisam atualizar seu aplicativo de Portal da empresa pelo menos a versão de novembro de 2018 continue se comunicando com o Google Play Store.

#### <a name="how-does-this-change-affect-me"></a>Como essa alteração me afeta?

Nossos dados indicam que há locatários que têm dispositivos com uma versão do Portal da empresa anterior ao 5.0.4269.0. Se esta versão (ou posterior) do Portal da empresa aplicativo não estiver instalado, ações iniciadas pelo administrador de dispositivo podem não funcionar conforme o esperado. Essas ações incluem a redefinição de senha, apagamento, instalações de aplicativos disponíveis e necessários e registro de certificado.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>O que preciso fazer para me preparar para essa alteração?

Peça aos usuários de dispositivos Android que ainda não tiverem atualizado a versão do Portal da empresa para atualizá-lo por meio do Google Play. Notifique o suporte técnico no caso de um usuário não tiver mantido a atualização automática o aplicativo de Portal da empresa. Para obter mais informações sobre a plataforma do FCM e a alteração do Google, consulte [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/).


### <a name="plan-for-change-intune-supports-macos-1012-and-higher-in-december"></a>Plano para alteração: Intune dá suporte a macOS 10.12 e superior em dezembro

<!--2970975-->  

A Apple lançou o macOS 10.14, portanto, a partir de dezembro de 2018, o Intune será compatível com macOS 10.12 e posterior. 

#### <a name="how-does-this-affect-me"></a>Como isso me afeta?

A partir de dezembro, os usuários em dispositivos com macOS 10.11 e anteriores não poderão usar o Portal da Empresa para se registrar no Intune. Para continuar recebendo suporte e novos recursos, eles precisarão atualizar seu dispositivo para o macOS 10.12 ou superior, e atualizar o aplicativo Portal da Empresa para a versão mais recente. 

No momento, o macOS versões 10.12 e posterior são compatíveis com o: 
- MacBook (fim de 2009 ou mais recente)  
- iMac (fim de 2009 ou mais recente)
- MacBook Air (fim de 2010 ou mais recente)  
- MacBook Pro (fim de 2010 ou mais recente)  
- Mac Mini (fim de 2010 ou mais recente)  
- Mac Pro (fim de 2010 ou mais recente)  

Após dezembro, os usuários finais que têm dispositivos diferente dos listados acima não poderão acessar a versão mais recente do aplicativo Portal da Empresa para macOS. É possível continuar gerenciando os dispositivos registrados que executam versões sem suporte abaixo do macOS 10.12.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>O que preciso fazer para me preparar para essa alteração?

- Solicite que seus usuários atualizem seus dispositivos para uma versão do sistema operacional compatível antes de dezembro de 2018.  
- Verifique o relatório do Intune no portal do Azure, para ver quais dispositivos ou usuários podem ser afetados. Vá para **Dispositivos** > **Todos os dispositivos** e filtrar por **sistema operacional**. É possível adicionar mais colunas para ajudar a identificar quem em sua organização tem dispositivos que executam o macOS 10.11.  
- Se estiver usando o MDM (gerenciamento de dispositivo móvel) híbrido, no console do Configuration Manager, acesse o workspace **Ativos e Conformidade** e selecione o nó **Dispositivos**. Clique com o botão direito do mouse nas colunas para adicionar as colunas **Sistema Operacional** e **Versão do cliente**. Em seguida, classifique pela versão do sistema operacional. Observe que agora o MDM híbrido foi preterido e você deve migrar para o Intune no Azure assim que possível. 
 
#### <a name="additional-information"></a>Informações adicionais
Para obter mais informações, confira [Registrar seu dispositivo macOS no Intune com o aplicativo Portal da Empresa](https://docs.microsoft.com/intune-user-help/enroll-your-device-in-intune-macos-cp).


### <a name="plan-for-change-use-intune-on-azure-now-for-your-mdm-management"></a>Plano para alteração: Use o Intune no Azure agora para o gerenciamento MDM 
<!--1227338-->  
Mais de um ano atrás, anunciamos [visualização pública do Intune no Azure](https://cloudblogs.microsoft.com/enterprisemobility/2016/12/07/public-preview-of-intune-on-azure/) e, após seis meses, a [disponibilidade geral da nova experiência de administração](https://cloudblogs.microsoft.com/enterprisemobility/2017/06/08/the-new-intune-and-conditional-access-admin-consoles-are-ga/) para o Intune. No dia 31 de agosto de 2018, o MDM (gerenciamento de dispositivo móvel) será desabilitado no console do Silverlight clássico para os clientes que usam o Intune autônomo. Nesse caso, use o [Intune no Azure](https://aka.ms/Intune_on_Azure) para atender às suas necessidades de MDM. Se você ainda estiver usando o console clássico do MDM, deixe de usá-lo e familiarize-se com o Intune no Azure. Não esperamos que haja nenhum impacto para o usuário final com essa alteração. O gerenciamento de computador clássico com o Intune permanece no Silverlight. Para saber mais, confira [a postagem no blog da equipe de suporte do Intune](https://aka.ms/Intune_on_Azure_mdm).


### <a name="plan-for-change-upcoming-macos-and-intune-password-enforcement-change"></a>Plano para alteração: MacOS futuros e alteração de imposição de senha do Intune
<!--1873216-->  
Na versão de setembro de serviço, planos do Intune para integrar da Apple recentemente lançado "Alterar senha no próximo autenticação" configuração para dispositivos que executam o macOS 10.13 de versões e acima. Antes de essa configuração ter sido introduzida, provedores de MDM não tinham como verificar se a senha em um dispositivo havia sido alterada para garantir a conformidade. As políticas de configuração e conformidade do Intune apenas validavam que, na próxima vez que uma senha fosse alterada no dispositivo, ela seria marcada como em conformidade. Os usuários do macOS receberão uma solicitação para atualizar a senha quando integrarmos esse novo recurso da Apple, mesmo que a senha já esteja em conformidade.

#### <a name="how-does-this-change-affect-me"></a>Como essa alteração me afeta?
Essa alteração afetará apenas o clientes do MDM híbrido ou autônomo do Intune com uma política de dispositivo macOS. A Apple introduziu a configuração Alterar Senha na Nova Autenticação. Agora, o Intune pode forçar os usuários a atualizar a senha para uma que esteja em conformidade quando você efetuar push de uma política de senha. Se você bloquear os recursos da empresa até que o dispositivo seja marcado como em conformidade, saiba que seus usuários finais poderão ser impedidos de acessar recursos da empresa, como email ou sites do SharePoint, até que redefinam a senha. No futuro, todas as atualizações às políticas de senha de configuração e conformidade forçarão os usuários de destino a atualizar suas senhas.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>O que preciso fazer para me preparar para essa alteração?
Você talvez queira informar a assistência técnica. Se você não quiser impor essa política de dispositivo macOS, cancele ou exclua a política existente do macOS. Nossa pesquisa de cliente antes de implementar essa alteração indicou que a maioria dos clientes não será afetada por essa alteração. Normalmente, os usuários finais atualizam sua senha depois de receberem uma solicitação para registrarem-se com uma senha, ou redefinem a senha para permanecerem em conformidade.  


### <a name="plan-for-change-intune-moving-to-support-ios-10-and-later-in-september-2018"></a>Plano para alteração: Intune movendo para dar suporte ao iOS 10 e posterior, em setembro de 2018 
<!--2454656-->  

Em setembro de 2018, a Apple deve lançar o iOS 12. Logo após o lançamento, mudaremos o registro no Intune, o Portal da Empresa e o navegador gerenciado para dar suporte ao iOS 10 e versões posteriores.

#### <a name="how-does-this-change-affect-me"></a>Como essa alteração me afeta?

Os aplicativos móveis do Office 365 têm suporte no iOS 10 e posterior, portanto, você já pode ter atualizado seu sistema operacional ou dispositivos. Nesse caso, essa mudança não afetará você.

No entanto, se você tiver algum dos dispositivos listados abaixo ou quiser inscrever qualquer um dos dispositivos listados abaixo, saiba que eles só darão suporte ao iOS 9 e versões anteriores. Para continuar acessando o Portal da Empresa do Intune, você deve atualizar esses dispositivos até setembro para dispositivos que ofereçam suporte ao iOS 10 ou posterior: 

- iPhone 4S
- iPod Touch 
- iPad 2
- iPad (Terceira Geração)
- iPad Mini (Primeira Geração)

A partir de julho, os dispositivos inscritos no MDM com o iOS 9 e o Portal da Empresa receberão uma solicitação para atualizar seu sistema operacional ou dispositivo. Se você usar políticas de proteção de aplicativos, também poderá definir a configuração de acesso "Exigir sistema operacional mínimo do iOS (somente Aviso)".  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>O que preciso fazer para me preparar para essa alteração?

Verifique se há dispositivos ou usuários afetados em sua organização. No Intune, no portal do Azure, acesse **Dispositivos** > **Todos os dispositivos** e filtre por **SO**.  Clique em **Colunas** para exibir detalhes como a versão do sistema operacional. Solicite que seus usuários atualizem seus dispositivos para uma versão do sistema operacional compatível antes de setembro.


### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode"></a>Portal da Empresa para Windows 8.1 e Windows Phone 8.1 mudando para o modo de manutenção 
<!--1428681-->  
*6 de outubro de 2017*   
 
A partir de outubro de 2017, os aplicativos Portal da Empresa para Windows 8.1 e Windows Phone 8.1 mudaram para o modo de manutenção. Esse modo significa que os aplicativos e cenários existentes, como registro e conformidade, continuarão recebendo suporte nessas plataformas. Esses aplicativos continuam disponíveis para download por meio de canais de lançamento existentes, como o Microsoft Store. 

Uma vez no modo de manutenção, esses aplicativos só recebem atualizações críticas de segurança. Nenhuma atualização ou funcionalidade adicional será lançada para esses aplicativos. Para os novos recursos, recomendamos que você atualize os dispositivos para Windows 10 ou Windows 10 Mobile. 

### <a name="end-of-support-for-ios-80"></a>Fim do suporte para iOS 8.0 
<!---1164477--->  
Os aplicativos gerenciados e o aplicativo Portal da Empresa para iOS exigem o iOS 9.0 e superior para acessar os recursos da empresa. Os dispositivos que não forem atualizados até setembro não poderão mais acessar o Portal da Empresa ou esses aplicativos. 

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>Lembrete de suporte de plataforma: Suporte base do Windows Phone 8.1 terminou em 11 de julho de 2017
<!-- 1327781 -->  
*11 de julho de 2017*

O suporte base à plataforma Windows Phone 8.1 chegou ao fim. O suporte a computadores com Windows 8.1 não foi afetado.

Não há nenhum impacto imediato aos dispositivos Windows Phone 8.1 gerenciados pelo serviço Intune, incluindo os dispositivos registrados em MDM híbrido. Os dispositivos registrados continuam funcionando. Todas as políticas, configurações e aplicativos continuam a funcionar como o esperado. Observe que não há melhorias destinadas à plataforma Windows Phone 8.1 no serviço Intune nem ao aplicativo Portal da Empresa do Windows Phone 8.1.

Recomendamos atualizar os dispositivos qualificados do Windows Phone 8.1 para o Windows 10 Mobile assim que possível.  

### <a name="end-of-support-for-android-43-and-lower"></a>Fim do suporte para Android 4.3 e inferior
<!---1171127--->  
*6 de julho de 2017*

Os aplicativos gerenciados e o aplicativo Portal da Empresa para Android exigem o Android 4.4 e superior para acessar os recursos da empresa. Os dispositivos que não forem atualizados até o início de outubro não poderão mais acessar o Portal da Empresa ou esses aplicativos. Até dezembro, todos os dispositivos inscritos serão desativados, resultando na perda do acesso aos recursos da empresa. Se você estiver usando políticas de proteção do aplicativo sem MDM, os aplicativos não receberão atualizações e reduzirão a qualidade da sua experiência ao longo do tempo.



## <a name="see-also"></a>Consulte também

- [Recursos e avisos do MDM híbrido anteriores](whats-new-hybrid-archive.md)
- [Novidades do MDM no System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)
