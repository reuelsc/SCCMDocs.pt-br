---
title: "Novidades na híbrida MDM | Microsoft Docs"
description: "Saiba mais sobre os novos recursos de gerenciamento de dispositivo móvel disponíveis para implantações híbridas com o Intune e o System Center Configuration Manager."
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
caps.latest.revision: 40
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 776c606f8e9ebfd7348d9d3a8f1e038d47bdf7a1
ms.openlocfilehash: 891638f920a5bf807b17c7f55b9153be45fc3b93

---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Novidades no gerenciamento de dispositivo móvel híbrido com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo fornece detalhes sobre os novos recursos de MDM (gerenciamento de dispositivo móvel) disponíveis para implantações híbridas com o System Center Configuration Manager e o Microsoft Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilidade com versões do Configuration Manager  

 Cada seção deste artigo lista recursos híbridos em três categorias diferentes. Use as diretrizes a seguir para determinar a compatibilidade dos recursos em cada categoria com versões diferentes do Configuration Manager:  

|Categorias do recurso|Descrição|
|-|-|
|**Novo no Microsoft Intune** | Em geral, todos os recursos listados nessa categoria devem funcionar com todas as versões do Configuration Manager, incluindo versões do System Center 2012 R2 Configuration Manager, uma vez que esses recursos exigem apenas o serviço Intune e não exigem funcionalidades adicionais no Configuration Manager.|
|**Novo no Configuration Manager Technical Preview**| Todos os recursos listados nessa categoria funcionam apenas com a versão de Technical Preview especificada. Para testar esses recursos, você deve instalar a versão de Technical Preview especificada na descrição do recurso. Para mais informações, confira [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md).|
|**Novo no Configuration Manager (Branch Atual)**| Todos os recursos listados nessa categoria funcionam apenas com a versão especificada do Configuration Manager (Branch Atual), como a versão 1511 ou 1602. Se estiver usando uma versão mais antiga do Configuration Manager para sua implantação híbrida, atualize para a versão do Configuration Manager (Branch Atual) especificada na descrição do recurso. Para mais informações, confira [Atualização para o System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|

## <a name="new-hybrid-features-in-december-2016"></a>Novos recursos híbridos em dezembro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

Os recursos do Intune a seguir introduzidos em dezembro de 2016 funcionam em implantações híbridas:

- **A MFA (Autenticação Multifator) no registro está migrando para o portal do Azure**

  Anteriormente, você tinha que ir para o console do Intune ou para o console do Configuration Manager para definir o MFA para inscrições do Intune. Com esse recurso atualizado, você faz logon no [Portal do Microsoft Azure] (https://manage.windowsazure.com) usando suas credenciais do Intune e configura as definições MFA por meio do Azure AD. Para obter mais informações, consulte [Autenticação multifator para Microsoft Intune] (https://aka.ms/mfa_ad).

- **Aplicativo de Portal da empresa para Android já disponível na China**

  O aplicativo de Portal da empresa para Android agora está disponível na China. Devido à ausência do Google Play Store na China, os dispositivos Android devem obter aplicativos de marketplaces de aplicativos chinês. O aplicativo de Portal da empresa para Android está disponível para download nos seguintes repositórios:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)

  O aplicativo de Portal da Empresa para Android usa o Google Play Services para se comunicar com o serviço Microsoft Intune. Como o Google Play Services ainda não está disponível na China, executar qualquer uma das seguintes tarefas pode levar até 8 horas para ser concluída.

  | Console de Administração do Configuration Manager | Aplicativo Portal da Empresa do Intune para Android | Site do Portal da empresa do Intune |
  |----|----|----|      
  | Desativar/apagar (remover todos os dados)   | Remover um dispositivo remoto | Remover dispositivo (local e remoto) |
  | Desativar/apagar (remover dados da empresa)   | Redefinir o dispositivo | Redefinir o dispositivo|
  | Implantações de aplicativo novo ou atualizado | Instalar aplicativos de linha de negócios disponíveis | Redefinição de senha de dispositivo|
  | Bloqueio remoto | | |
  | Redefinição de senha | | |        


## <a name="new-hybrid-features-in-november-2016"></a>Novos recursos híbridos em novembro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

Os recursos do Intune a seguir introduzidos em novembro de 2016 funcionam em implantações híbridas:

- **Novo Portal da empresa do Microsoft Intune disponível para dispositivos Windows 10**

  A Microsoft lançou um novo [Aplicativo de Portal da empresa para dispositivos Windows 10](https://www.microsoft.com/store/apps/9wzdncrfj3pz). Esse aplicativo, que aproveita o novo formato Universal do Windows 10, fornece uma experiência de usuário atualizada que é idêntica em todos os dispositivos Windows 10 e de forma semelhante em PCs e dispositivos móveis, permitindo ao mesmo tempo a mesma funcionalidade fornecida por aplicativos anteriores do Portal da empresa.

  O novo aplicativo aproveita os recursos de plataforma como logon único (SSO) e autenticação baseada em certificado em dispositivos Windows 10. O aplicativo está disponível como uma atualização para as instalações existentes do Portal da empresa do Windows 8.1 e Portal de empresa do Windows Phone 8.1 da Windows Store. Para obter mais detalhes, acesse o [Blog da equipe de suporte do Intune](http://aka.ms/intunecp_universalapp).

  O novo aplicativo de Portal da Empresa também exibe quaisquer aplicativos Windows Store para Empresas marcados como **Disponível** no console do Configuration Manager.


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)

Os seguintes recursos que estavam anteriormente disponíveis nas versões do Configuration Manager Technical Preview agora estão disponíveis em implantações híbridas com o Intune e a versão 1610 do Configuration Manager (branch atual).

* [Configurações adicionais e experiência aprimorada para itens de configuração](/sccm/core/plan-design/changes/whats-new-in-version-1610?branch=sccm-1610-release#new-compliance-settings-for-configuration-items)
* [Configurações adicionais para perfis de DEP](#new-in-configuration-manager-technical-preview-1609)
* [Aplicativos pagos na Windows Store para Empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Tipos de conexão nativa para perfis de VPN do Windows 10](#new-in-configuration-manager-technical-preview-1609)
* [Gráficos de conformidade do Intune](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)
* [Solicitação da sincronização de política do console](/sccm/mdm/deploy-use/sync-intune-device)
* [Definições de configuração do Windows Defender](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#windows-defender)

Os seguintes recursos híbridos adicionais também estão incluídos na versão 1610 do Configuration Manager (Branch Atual):

- **Aumento do número de dispositivos registrados**

  Agora você pode habilitar os usuários para registrarem até 15 dispositivos. O limite anterior era cinco dispositivos por usuário.


- **Suporte de segurança adicional**

  Além de Administrador Completo, as seguintes funções de segurança internas agora têm acesso completo aos itens no nó Todos os dispositivos de propriedade corporativa, incluindo Dispositivos Pré-Declarados, perfis de registro do iOS e perfis de registro do Windows:

    - Gerenciador de Ativos
    - Gerenciador de acesso aos recursos da empresa

  O acesso somente leitura para essas áreas do console do Configuration Manager ainda é concedido à função de Analista somente leitura.

- **Acesso VPN de disparo automático de aplicativos da Proteção de Informações do Windows**

  Você pode adicionar um domínio primário de Proteção de Informações do Windows aos perfis de VPN do Windows 10, que faz com que todos os aplicativos associados disparem uma conexão VPN automaticamente quando são executados no dispositivo. Essa opção só está disponível ao escolher um tipo de conexão nativo.

- **Acesso condicional para perfis VPN do Windows 10**

    Agora é possível exigir que dispositivos Windows 10, registrados no Azure Active Directory, sejam compatíveis para terem acesso VPN por meio de perfis de VPN do Windows 10 criados no console do Configuration Manager. Isso é possível por meio da nova caixa de seleção **Habilitar o acesso condicional para esta conexão VPN** na página Método de autenticação no Assistente para Criar Perfil VPN e as propriedades de perfil VPN para perfis de VPN do Windows 10. Essa opção só está disponível ao escolher um tipo de conexão nativo.

    Também será possível especificar um certificado diferente para autenticação de logon único se você habilitar o acesso condicional para o perfil.

## <a name="new-hybrid-features-in-october-2016"></a>Novos recursos híbridos em outubro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

Os recursos do Intune a seguir introduzidos em outubro de 2016 funcionam em implantações híbridas.

- **Acesso condicional para o gerenciamento de aplicativo móvel**

  Você pode restringir o acesso ao Exchange Online para que o acesso venha apenas de aplicativos que dão suporte às políticas de gerenciamento de aplicativo móvel do Intune, como o Outlook. [Esse novo recurso](/intune/deploy-use/allow-policy-managed-apps-access-to-o365) é completamente compatível com as políticas de MAM (gerenciamento de aplicativo móvel) do Intune, uma vez que você pode bloquear o acesso a clientes de email internos ou outros aplicativos que não foram configurados com as políticas de MAM do Intune. Isso garante que os usuários estão acessando os dados da sua organização com aplicativos que podem ser protegidos usando o MAM do Intune. Você pode começar no gerenciamento de aplicativo móvel do Intune por meio do Portal do Azure. Procure a nova seção de Acesso Condicional na folha “Configurações”.

-   **Ferramenta de Disposição do Aplicativo do Intune para Android**

  Você pode habilitar seus aplicativos para usar políticas de MAM (gerenciamento de aplicativo móvel) usando a Ferramenta de Disposição do Aplicativo do Intune.

- **Compatibilidade do Samsung Android KNOX Standard com o Intune**

  Alguns modelos de telefone Samsung Galaxy Ace não podem ser gerenciados pelo Intune, como os dispositivos Samsung KNOX padrão. Quando você registrar esses dispositivos com o Intune, eles serão gerenciados como dispositivos Android padrão.

  Os números de modelo afetados são:

  - SM-G313HU
  - SM-G313HY
  - SM-G313M
  - SM-G313MY
  - SM-G313U

  Você e seus usuários finais não precisa executar nenhuma ação adicional. Para mais informações, visite o site da Samsung KNOX.

### <a name="new-in-configuration-manager-technical-preview-1610"></a>Novo no Configuration Manager Technical Preview 1610

Os novos recursos híbridos a seguir foram introduzidos em outubro de 2016 para o Configuration Manager Technical Preview 1610.

- **Solicitar uma sincronização de política do console de administração**

  Você pode solicitar uma sincronização de política em um dispositivo móvel registrado no console do Configuration Manager, em vez de precisar solicitar a sincronização no aplicativo do Portal da Empresa no próprio dispositivo. Esta é uma nova ação chamada **Send Sync Request (Enviar Solicitação de Sincronização)** no menu Ações do Dispositivo Remoto, que aparece na faixa de opções quando um dispositivo móvel é selecionado no nó Dispositivos.

- **Definições de configuração do Windows Defender**

  Agora você pode definir as configurações de cliente do Windows Defender em computadores Windows 10 registrados no Intune usando itens de configuração no console do Configuration Manager. Há um novo grupo de configurações chamado **Windows Defender** no Assistente de Item de Configuração. Observe que isso tem suporte apenas no Windows 10 versão 1511 e acima.


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)

Não foi realizada a introdução de nenhum recurso híbrido novo em agosto de 2016 para o Configuration Manager (Branch Atual).

## <a name="new-hybrid-features-in-september-2016"></a>Novos recursos híbridos em setembro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

Os recursos do Intune a seguir introduzidos em setembro de 2016 funcionam em implantações híbridas.

- **Adição de "Notificações" no Portal da Empresa para Android**

  Um novo ícone de Notificações foi adicionado ao Portal da Empresa para Android na home page. Tocar o ícone acessa a página Notificações, que mostra aos usuários finais todos os itens que requerem atenção no aplicativo do Portal da Empresa, como a falta de conformidade do dispositivo, a atualização de registro e a ativação do registro. O aplicativo do Portal da Empresa para iOS já tem essa experiência de notificações. Ter a nova página Notificações significa que os usuários não verão a página Configuração do Acesso da Empresa sempre que iniciarem ou retomarem o Portal da Empresa, contanto que o dispositivo já esteja registrado. Se você criar suas próprias diretrizes do usuário final, atualize sua documentação para refletir essas alterações. Encontre capturas de tela atualizadas [aqui](https://aka.ms/androidcpupdate).

- **Alterações no suporte para o aplicativo do Portal da Empresa para iOS**

  Todos os usuários do aplicativo do Portal da Empresa do Microsoft Intune para iOS agora devem usar sua versão mais recente. Os novos usuários podem baixar apenas a versão mais recente e os usuários atuais devem atualizá-lo para ela. A versão mais recente requer o iOS 8.0 ou posterior, portanto, dispositivos executando versões do iOS anteriores não podem usar o Portal da Empresa ou se registrar até atualizarem seu dispositivo para o iOS 8.0 ou posterior e, então, atualizar o aplicativo do Portal da Empresa para a versão mais recente. Os dispositivos registrados que executam versões inferiores ao iOS 8.0 continuarão a ser gerenciados e listados no Console do Administrador do Intune.

- **Botão de comentários adicionado ao aplicativo do Portal da Empresa para Windows Phone 8.1.**

  O aplicativo do Portal da Empresa para Windows Phone 8.1 permite que os usuários finais enviem comentários sobre o aplicativo usando um novo botão “enviar comentários”. Para localizar o botão, os usuários tocam no menu de “três pontos” na parte inferior direita da tela do aplicativo do Portal da Empresa e tocam em **enviar comentários**. Os comentários anônimos coletados ajudarão a Microsoft a aprimorar a experiência do aplicativo do Portal da Empresa para os usuários.

### <a name="new-in-configuration-manager-technical-preview-1609"></a>Novo no Configuration Manager Technical Preview 1609

Os novos recursos híbridos a seguir foram introduzidos em setembro de 2016 para o Configuration Manager Technical Preview 1609.

- **Configurações adicionais e experiência aprimorada para configurações do Item de Configuração**

  Foram adicionadas novas configurações para Windows, iOS e Android e apenas as configurações que se aplicam às plataformas selecionadas na página Plataformas com Suporte são exibidas no assistente. Para mais informações, confira [Novas configurações de conformidade para itens de configuração na TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#new-compliance-settings-for-configuration-items).

- **Configurações adicionais para perfis de DEP**

  Zoom, TouchID e ApplePay foram adicionados como definições configuráveis em perfis de DEP para dispositivos iOS.

- **Aplicativos pagos na Windows Store para Empresas**

  Agora você pode adicionar aplicativos pagos e gratuitos à Windows Store para Empresas e implantá-los para os usuários em sua organização. Para mais informações, confira [Aprimoramentos para a Windows Store para Empresas na TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#enhancements-to-windows-store-for-business-integration-with-configuration-manager).

- **Tipos de conexão nativa para perfis de VPN do Windows 10**

  Agora você pode criar perfis de VPN do Windows 10 para MDM com os tipos de conexão Microsoft Automatic, IKEv2 e PPTP no console do Configuration Manager sem usar o OMA-URI.

- **Gráficos de conformidade do Intune**

  Você pode obter uma exibição rápida da conformidade geral do dispositivo e os principais motivos de não conformidade usando novos gráficos no espaço de trabalho Monitoramento. Para mais informações, confira [Gráficos de conformidade do Intune na TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#intune-compliance-charts).

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)

O novo recurso a seguir introduzido em setembro de 2016 está disponível para implantações híbridas com o Microsoft Intune e a versão 1606 do Configuration Manager (Branch Atual).

- **Suporte para iOS 10**

  Se você tiver perfis ou itens de configuração direcionados a todas as plataformas iOS, eles também serão enviados por push para o iOS 10. Também lançamos uma atualização para a versão 1606 do Configuration Manager que permite que você direcione perfis e itens de configuração para plataformas iOS individuais, incluindo o iOS 10. Você pode instalar a atualização com o console de administração do Configuration Manager em **Administração > Visão Geral > Serviços de Nuvem > Atualizações e Manutenção**. Você pode encontrar mais informações sobre a atualização em [http://support.microsoft.com/kb/3192616](http://support.microsoft.com/kb/3192616).

## <a name="new-hybrid-features-in-august-2016"></a>Novos recursos híbridos em agosto de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

Os recursos do Intune a seguir introduzidos em agosto de 2016 funcionam em implantações híbridas.

- **Suporte para Android 7 no aplicativo do Portal da Empresa**

  O aplicativo do Portal da Empresa do Intune para Android dá suporte inicial para o próximo sistema operacional Android 7.0 para dispositivos móveis.

- **Remoção pelo Google da funcionalidade de redefinição de senha remota em dispositivos Android 7.0**

  O Google está removendo a capacidade dos administradores de TI e usuários finais redefinirem remotamente a senha de dispositivos Android 7.0. Anteriormente, os administradores de TI poderiam redefinir remotamente a senha de um usuário e os usuários finais poderiam redefinir suas senhas pelo site do Portal da Empresa.

- **Política de aplicativos permitidos e bloqueados para dispositivos Samsung KNOX Standard**

  Agora você pode configurar uma política personalizada para dispositivos Standard Samsung KNOX que permite que você crie um dos itens a seguir:

  - Uma lista de aplicativos que são impedidos de serem executados no dispositivo. Mesmo se instalado, um aplicativo definido na lista bloqueada não poderá ser ativado no dispositivo.
  - Uma lista de aplicativos que os usuários do dispositivo podem instalar da Google Play Store. Nenhum outro aplicativo pode ser instalado por meio da Store.

  Essas configurações podem ser usadas apenas por dispositivos que executam o Samsung KNOX Standard. Para detalhes, confira [Usar políticas personalizadas para permitir e bloquear aplicativos para dispositivos Samsung KNOX Standard](/intune/deploy-use/custom-policy-to-allow-and-block-samsung-knox-apps).

- **Link de comentários do Portal da Empresa para a Microsoft**

   O site do Portal da Empresa permite que os usuários finais toquem em um novo link “Comentário”, na parte inferior da página, para enviar comentários para a Microsoft sobre sua experiência com o site. Os comentários anônimos coletados ajudarão a Microsoft a aprimorar a experiência do site do Portal da Empresa para os usuários.

- **Versão mínima do Managed Browser para iOS atualizada para 8.0**

  O aplicativo Microsoft Intune Managed Browser para iOS foi atualizado para dar suporte a dispositivos executando o iOS 8.0 ou posterior. Embora os dispositivos iOS 7.1 ainda possam usar o aplicativo Managed Browser existente, incentive seus usuários a atualizarem para o iOS 8.0 ou posterior para acessar e aproveitar totalmente os novos recursos do Managed Browser.

### <a name="new-in-configuration-manager-technical-preview"></a>Novo no Configuration Manager Technical Preview

Não foi realizada a introdução de nenhum recurso híbrido novo em agosto de 2016 para o Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)

Não foi realizada a introdução de nenhum recurso híbrido novo em agosto de 2016 para o Configuration Manager (Branch Atual).

## <a name="new-hybrid-features-in-july-2016"></a>Novos recursos híbridos em julho de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

Os recursos do Intune a seguir introduzidos em julho de 2016 funcionam em implantações híbridas.

- **SDK do Xamarin para aplicativos do Intune está disponível**

  O componente Xamarin do SDK de aplicativos do Intune permite que você habilite os recursos de gerenciamento de aplicativo móvel do Intune em seus aplicativos móveis para iOS e Android criados com o Xamarin. Você pode encontrar o componente na [Loja do Xamarin](https://components.xamarin.com/view/Microsoft.Intune.MAM) ou na [página do Github do Microsoft Intune](https://github.com/msintuneappsdk).

- **Experiência do usuário final melhorada ao registrar dispositivos Windows**

  Ao usar o acesso condicional, as etapas de registro para Windows 8.1, Windows 10 Desktop e Windows 10 Mobile foram esclarecidas no site do Portal da Empresa. Agora os usuários verão etapas de **Registro do dispositivo** e **Ingresso no Local de Trabalho** separadas, facilitando a visualização do status de seu dispositivo e a conclusão do processo caso enfrentem uma falha de WPJ (Ingresso no Local de Trabalho). As etapas separadas também devem simplificar o processo de solução de problemas para os administradores de TI. Anteriormente, quando os usuários finais tentavam realizar o registro e todas as etapas de registro eram bem sucedidas, exceto o WPJ, o dispositivo não aparecia na lista de dispositivos para os usuários o identificarem, causando confusão para os usuários.

 - **Apagamento completo agora disponível para dispositivos Windows 10**

    Os laptops e computadores com Windows 10 registrados como dispositivos móveis podem ser apagados para redefinir o dispositivo para suas configurações de fábrica. Para mais informações, confira [How to protect your devices with remote wipe](/sccm/mdm/deploy-use/wipe-lock-reset) (Como proteger seus dispositivos com o apagamento remoto).

- **Alterações nas contas dos Gerenciadores de Registro de Dispositivo no aplicativo do Portal da Empresa para iOS**

  Para melhorar o desempenho e a escala, o Intune não exibe mais todos os dispositivos de DEM (Gerenciadores de Registro de Dispositivo) no painel Meus Dispositivos do aplicativo do Portal da Empresa para iOS. Somente o dispositivo local executando o aplicativo será exibido e somente se ele estiver registrado por meio do aplicativo do Portal da Empresa.

  O usuário DEM pode realizar ações no dispositivo local, mas o gerenciamento remoto de outros dispositivos registrados pode ser executado apenas no console de administração do Intune. Além disso, o Intune está preterindo o uso de contas de DEM com o Programa de Registro de Dispositivo da Apple ou com a ferramenta Apple Configurator. Esses dois métodos de registro já dão suporte ao registro sem usuário para dispositivos iOS compartilhados.

  Use contas de DEM somente quando o registro sem usuário para dispositivos compartilhados estiver indisponível. Para mais informações, confira [Enroll corporate-owned devices with the Device Enrollment Manager in Microsoft Intune](../deploy-use/enroll-devices-with-device-enrollment-manager.md) (Registrar dispositivos corporativos com o Gerenciador de Registro de Dispositivos no Microsoft Intune).

- **Alterações no aplicativo do Portal da Empresa para Android**

  Se os usuários finais do Android virem uma mensagem de erro dizendo que o dispositivo não tem um certificado necessário, eles poderão tocar no botão “Como resolver isso” para encontrar as etapas para instalar o certificado ausente. Se os usuários concluírem as etapas, mas virem uma mensagem de erro de “certificado ausente” adicional, será solicitado que eles entrem em contato com o administrador de TI e forneçam esse link, que contém as etapas que os administradores de TI podem usar para corrigir o problema do certificado.

- **Restringir instalações de aplicativos de sideload para dispositivos Android registrados**

  Os dispositivos Android não podem mais instalar aplicativos por meio do site do Portal da Empresa a menos que os dispositivos tenham sido registrados pelo aplicativo do Portal da Empresa do Intune para Android.


### <a name="new-in-configuration-manager-technical-preview"></a>Novo no Configuration Manager Technical Preview

Não foi realizada a introdução de nenhum recurso híbrido novo em julho de 2016 para o Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)

Os seguintes recursos que estavam anteriormente disponíveis nas versões do Configuration Manager Technical Preview agora estão disponíveis em implantações híbridas com o Intune e a versão 1606 do Configuration Manager.

* Localizar, gerenciar e distribuir aplicativos da Windows Store para Empresas para dispositivos Windows 10 por meio do console do Configuration Manager ([1604](whats-new-hybrid-archive.md#new-in-1604-technical-preview))
*   Configuração do SmartLock para dispositivos Android ([1604](whats-new-hybrid-archive.md#new-in-1604-technical-preview))
*   VPN acionado por aplicativo para dispositivos Windows 10 ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Nova experiência para ações de dispositivo remoto ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Aplicativos da Windows Store para Empresas ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Melhorias gerais para aplicativos adquiridos por volume ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   WIP (Proteção de Informações do Windows) ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Pré-declarar dispositivos corporativos com número de série do iOS ou IMEI ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Categorizar automaticamente dispositivos em coleções ([1606](whats-new-hybrid-archive.md#new-in-1606-technical-preview))

Para obter informações sobre a nova funcionalidade, consulte a documentação da versão de Technical Preview especificada.

## <a name="notices"></a>Avisos

- **25 de outubro de 2016: upload do Portal da Empresa do Windows Phone 8 preterido**

  A capacidade de carregar um aplicativo do Portal da Empresa assinado foi removida do console do Configuration Manager, uma vez que o suporte do Intune está sendo preterido para Windows 8, Windows Phone 8 e Windows RT e o suporte para o Portal da Empresa para Windows Phone 8 será encerrado em novembro.  Os dispositivos Windows 8, Windows Phone 8 e Windows RT já registrados continuarão a ter suporte, mas o registro de dispositivos adicionais com essas plataformas não terá suporte.


### <a name="see-also"></a>Consulte também

- [Recursos do MDM híbrido anteriores](whats-new-hybrid-archive.md)
- [Novidades do MDM no System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)



<!--HONumber=Dec16_HO3-->


