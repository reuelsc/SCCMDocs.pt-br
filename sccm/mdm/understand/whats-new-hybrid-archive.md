---
title: "Arquivo morto das novidades no MDM híbrido | Microsoft Docs"
description: "Arquivo morto dos recursos de gerenciamento de dispositivo móvel anteriores disponíveis para implantações híbridas com o Intune e o System Center Configuration Manager."
ms.custom: na
ms.date: 10/25/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: Mtillman
ms.author: mtillman
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: 8f092ed5745c925f624f00efa9274895f0df7260
ms.openlocfilehash: 1c469f89ee06ba8da80673db83e80e5c33618146

---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>Recursos híbridos anteriores com o System Center Configuration Manager e Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo fornece detalhes sobre os recursos de MDM (gerenciamento de dispositivo móvel) anteriores disponíveis para implantações híbridas com o System Center Configuration Manager e o Microsoft Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilidade com versões do Configuration Manager  

 Cada seção deste artigo lista recursos híbridos em três categorias diferentes. Use as diretrizes a seguir para determinar a compatibilidade dos recursos em cada categoria com versões diferentes do Configuration Manager:  

|Categorias do recurso|
|-|  
|**Novo no Microsoft Intune** – em geral, todos os recursos listados nessa categoria devem funcionar com todas as versões do Configuration Manager, incluindo versões do System Center 2012 R2 Configuration Manager, uma vez que esses recursos exigem apenas o serviço Intune e não exigem funcionalidades adicionais no Configuration Manager.<br /><br /> **Novo no Configuration Manager Technical Preview** – todos os recursos listados nessa categoria funcionam apenas com a versão de Technical Preview especificada. Para testar esses recursos, você deve instalar a versão de Technical Preview especificada na descrição do recurso. Para mais informações, confira [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md).<br /><br /> **Novo no Configuration Manager (Branch Atual)** – todos os recursos listados nessa categoria funcionam apenas com a versão especificada do Configuration Manager (Branch Atual), como a versão 1511 ou 1602. Se estiver usando uma versão mais antiga do Configuration Manager para sua implantação híbrida, atualize para a versão do Configuration Manager (Branch Atual) especificada na descrição do recurso. Para mais informações, confira [Atualização para o System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|  

## <a name="new-hybrid-features-in-june-2016"></a>Novos recursos híbridos em junho de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune
Os recursos do Intune a seguir introduzidos em junho de 2016 funcionam em implantações híbridas.

- **Integridade do serviço Intune** As informações de integridade do serviço para o Intune foram movidas para um local central com outros serviços da Microsoft. Agora, você encontrará essas informações no portal de gerenciamento do Office 365 em Integridade do Serviço. Para mais informações, confira essa [postagem no blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/).

- **Experiência de configuração de política de dados empresariais do Windows 10 aprimorada**

  Agora o Intune tem uma experiência melhorada para a configuração da política de proteção de informações do Windows 10. As melhorias incluem melhores maneiras de criar regras de aplicativo, especificar a definição de limites de rede e outras configurações de Proteção de Informações do Windows. Para saber mais, confira [Criar uma política de WIP (Proteção de Informações do Windows) usando o Microsoft Intune](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-intune).

- **Política de controle de acesso à rede do Cisco ISE**

  Os clientes que usam o Cisco ISE (Identity Service Engine) 2.1 e usam o Microsoft Intune também podem definir uma política de controle de acesso de rede no ISE. Usando essa política, os dispositivos que precisam se conectar à rede usando o WiFi ou VPN devem atender às seguintes condições antes de terem permissão de acesso:

  - Devem ser gerenciados pelo Intune
  - Devem ser compatíveis com qualquer política de conformidade do Intune implantada

  Os usuários finais de dispositivos incompatíveis deverão realizar o registro e corrigir quaisquer problemas de conformidade para obter o acesso.

- **Acesso condicional para o navegador**

  Você pode definir uma política de acesso condicional para o Exchange Online e o SharePoint Online para que eles possam ser acessados apenas de navegadores Web com suporte em dispositivos Android e iOS gerenciados e compatíveis. Os usuários finais que tentarem entrar no OWA (Outlook Web Access) e em sites do SharePoint com dispositivos iOS e Android deverão registrar seu dispositivo no Intune, bem como corrigir quaisquer problemas de não conformidade antes de poderem entrar. Para obter mais informações, consulte

  * [Restringir acesso a email ao Exchange Online e ao novo Exchange Online Dedicado com o Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-online-with-microsoft-intune)
  * [Restringir o acesso ao SharePoint Online com o Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)

- **O Dynamics CRM Online dá suporte ao acesso condicional**

  Você pode definir uma política de acesso condicional para o Dynamics CRM Online para que ele possa ser acessado apenas por dispositivos Android e iOS gerenciados e compatíveis. Os usuários finais que tentar entrar no aplicativo móvel do Dynamics CRM no iOS e Android deverão se registrar no Intune, bem como corrigir quaisquer erros de não conformidade antes de ser possível concluir a entrada. Para mais informações, confira [Restringir o acesso ao Dynamics CRM Online com o Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-dynamics-crm-online-with-microsoft-intune).

- **Atualizações no aplicativo do Portal da Empresa para Android**

  Agora, o Intune tem as seguintes novas políticas que afetarão os usuários do Portal da Empresa para Android:   

  Política  |Impacto sobre os usuários  
  ---------|---------
  Exigir que dispositivos não permitam a instalação de aplicativos de fontes desconhecidas (Android 4.0+)     |  Os usuários finais com dispositivos Android 4.0 ou posteriores verão a mensagem “A instalação de fontes desconhecidas deve ser desabilitada”. Os usuários precisarão ir para **Configurações > Segurança** em seus dispositivos e desativar **Fontes desconhecidas**. Um link na mensagem de conformidade permite que os usuários obtenham mais informações sobre a mensagem e porque eles devem desativar a configuração.
  Exigir que dispositivos não permitam a instalação de aplicativos de fontes desconhecidas (Android 4.0+)  |    Os usuários finais com dispositivos Android 4.0 ou posteriores verão a mensagem “Verificar ameaças à segurança no dispositivo”. Os usuários precisarão ir para **Configurações > Google > Segurança** em seus dispositivos e ativar **Verificar ameaças à segurança no dispositivo**. Um link na mensagem de conformidade permite que os usuários obtenham mais informações sobre a mensagem e porque eles devem ativar a configuração.     
  Exigir que a depuração de USB esteja desabilitada (Android 4.2+)  | Os usuários finais com dispositivos Android 4.2 ou posteriores verão a mensagem “A depuração de USB deve ser desabilitada”. Os usuários precisarão ir para **Configurações > Opções do desenvolvedor** em seus dispositivos e desativar a **Depuração de USB**. Um link na mensagem de conformidade permite que os usuários obtenham mais informações sobre a mensagem e porque eles devem desativar a configuração.
  Nível mínimo do patch de segurança do Android (Android 6.0+)  | Os usuários finais com dispositivos Android 6.0 ou posteriores verão a mensagem “Esse dispositivo não atende o nível de patch de segurança do Android mínimo”. Os usuários precisarão instalar o patch de segurança necessário. Um link na mensagem de conformidade permite aos usuários obter informações sobre como instalar o patch de segurança necessário e ver qual patch de segurança eles têm instalado no momento.

- **Atualizações no aplicativo do Portal da Empresa para iOS**

  * Quando os usuários finais estiverem instalando aplicativos de linha de negócios, agora eles verão uma experiência de instalação de aplicativo aprimorada. Se a instalação do aplicativo estiver demorando muito, os usuários poderão sincronizar manualmente seus dispositivos para forçar o processo de sincronização a continuar. Para examinar as instruções do usuário final, consulte Sync your iOS device manually (Sincronizar seu dispositivo iOS manualmente).
  * O aplicativo de Portal da Empresa do Microsoft Intune para iOS foi atualizado para dar suporte à versão 8.0 e posteriores do iOS. Essa atualização significa que os usuários finais poderão instalar o aplicativo do Portal da Empresa e registrar novos dispositivos no Intune somente se o dispositivo estiver executando o iOS versão 8.0 ou posterior. Usuários que já registraram dispositivos que estão executando uma versão sem suporte do iOS podem continuar usando o aplicativo de Portal da Empresa que está no dispositivo.


### <a name="new-in-1606-technical-preview"></a>Novo no Technical Preview 1606
Os novos recursos a seguir introduzidos em junho de 2016 estão disponíveis para implantações híbridas com o Intune e com o Configuration Manager Technical Preview 1606.

- **Categorizar automaticamente dispositivos em coleções**

  Você pode criar categorias de dispositivos, que podem ser usadas para colocar automaticamente os dispositivos em coleções de dispositivos ao usar o Configuration Manager com o Intune. Os usuários devem, então, escolher uma categoria de dispositivo ao registrar um dispositivo no Intune. Além disso, você pode alterar a categoria de um dispositivo do console do Configuration Manager. Para mais informações, confira [Categorizar automaticamente dispositivos em coleções](/sccm/core/get-started/capabilities-in-technical-preview-1606#dmp_category) em [Funcionalidades no Technical Preview 1606 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1606).

  > [!IMPORTANT]
  > Essa funcionalidade funciona com a versão de junho de 2016 do Microsoft Intune. Verifique se você atualizou para essa versão antes de experimentar esses procedimentos.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)
Não foi realizada a introdução de nenhum recurso híbrido novo em junho de 2016 para o Configuration Manager (Branch Atual).

##  <a name="new-hybrid-features-in-may-2016"></a>Novos recursos híbridos em maio de 2016  

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune  
 Os recursos do Intune a seguir introduzidos em maio de 2016 funcionam em implantações híbridas.

- **SDK do MAM: suporte para a configuração de comprimento do PIN**

  Agora você pode especificar o comprimento do PIN para aplicativos MAM semelhantes a um PIN do dispositivo. Isso requer que os usuários finais estejam em conformidade com as novas restrições definidas. A tela de PIN está ligeiramente modificada para considerar a entrada mais longa. Para obter detalhes, confira [Configurações de política de MAM para Android](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings) e [Configurações de política de MAM para iOS](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings).  

- **Skype for Business para iOS e Android**

  Agora você pode direcionar o Skype for Business com [MAM sem políticas de registro](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune). Depois que os usuários fizerem logon, as políticas MAM serão aplicadas.  

- **Novos aplicativos disponíveis para gerenciamento com políticas de MAM**

  Os aplicativos Microsoft Word, Excel e PowerPoint para Android agora podem ser associados a políticas de MAM em dispositivos que não estão registrados no Intune. Para obter uma lista completa de aplicativos com suporte, acesse a galeria de aplicativos móveis do Microsoft Intune na página [Microsoft Intune application partners](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx) (Parceiros de aplicativos do Microsoft Intune).  

- **Aplicativo do Portal da Empresa para Android: notificações do sistema do usuário final**

  As notificações do sistema do aplicativo do Portal da Empresa para Android aparecem quando os usuários finais registram ou removem seus dispositivos do Portal da Empresa.  

- **Site do Portal da Empresa: a faixa de identificação do dispositivo fornecerá mais informações para os usuários finais**

  Agora os usuários finais podem identificar mais facilmente o dispositivo selecionado quando estiverem usando o site do Portal da Empresa. Se o dispositivo incorreto for selecionado, eles poderão selecionar o dispositivo correto tocando no link **Toque aqui** na faixa da home page.  


### <a name="new-in-1605-technical-preview"></a>Novo no Technical Preview 1605  
 Os novos recursos a seguir introduzidos em maio de 2016 estão disponíveis para implantações híbridas com o Intune e com o Configuration Manager Technical Preview 1605. Esses recursos exigem que você use o console do Configuration Manager para configurá-los e gerenciá-los.  

- **VPN acionado por aplicativo para dispositivos Windows 10**

  Para dispositivos Windows 10 gerenciados usando o Configuration Manager com o Intune, você pode adicionar uma lista de aplicativos que abrem automaticamente uma conexão VPN que você configurou por meio do console de administração do Configuration Manager. Para mais informações, confira [VPN acionado por aplicativo para dispositivos Windows 10](/sccm/core/get-started/capabilities-in-technical-preview-1605) em [Funcionalidades no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605)  

- **Nova experiência para ações de dispositivo remoto**

  A experiência para executar as ações de dispositivo remoto do console do Configuration Manager foi aprimorada.

  Ações comuns, como **Desativar/Apagar**, **Redefinir Senha**, **Bloqueio Remoto** e **Ignorar Bloqueio de Ativação** agora podem ser encontradas no menu **Ações do Dispositivo Remoto** acessado pelo espaço de trabalho **Ativos e Conformidade**

  Para mais informações, confira [Nova experiência para ações de dispositivo remoto](/sccm/core/get-started/capabilities-in-technical-preview-1605#new-experience-for-remote-device-actions) em [Funcionalidades no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Aplicativos da Windows Store para Empresas**

  Na [Windows Store para Empresas](https://www.microsoft.com/en-us/business-store), é possível encontrar e adquirir aplicativos para sua organização, individualmente ou por volume. Ao conectar a loja ao Configuration Manager, é possível gerenciar aplicativos adquiridos por volume no console do Configuration Manager. Para mais informações, confira [Aplicativos da Windows Store para Empresas](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#windows-store-for-business-apps) em [Funcionalidades no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Melhorias gerais para aplicativos adquiridos por volume**

  Os aplicativos adquiridos por volume da Windows Store para Empresas e da iOS App Store foram consolidados na mesma exibição, **Informações sobre Licença para Aplicativos da Loja**. Além disso, o modo no qual você cria aplicativos adquiridos por volume para o iOS foi aprimorado. Para mais informações, confira [Melhorias gerais para aplicativos adquiridos por volume](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#general-improvements-for-volume-purchased-apps) em [Funcionalidades no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Pré-declarar dispositivos corporativos com número de série do iOS ou IMEI**

  Agora é possível identificar os dispositivos corporativos importando seus números IMEI (identidade da estação internacional do equipamento móvel). Você pode carregar um arquivo .csv (valores separados por vírgula) que contém os números IMEI do dispositivo ou inserir manualmente as informações sobre o dispositivo.  Você também pode importar os números de série para dispositivos iOS.  Para mais informações, confira [Pré-declarar dispositivos corporativos com número de série do iOS ou IMEI](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_IMEI) em [Funcionalidades no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **WIP (Proteção de Informações do Windows)**

  Você pode criar itens de configuração que permitem implantar suas políticas de WIP (Proteção de Informações do Windows), incluindo permitindo que você escolha seus aplicativos protegidos, seu nível de proteção WIP e como encontrar dados empresariais na rede. Para obter mais informações sobre a WIP, consulte os seguintes tópicos:  

  -   [Proteger os dados empresariais usando a WIP (Proteção de Informações do Windows)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [Criar e implantar uma política de Proteção de Informações do Windows (WIP) usando o System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)  
 Não foi realizada a introdução de nenhum recurso híbrido novo em maio de 2016 para o Configuration Manager (Branch Atual).  

##  <a name="new-hybrid-features-in-april-2016"></a>Novos recursos híbridos em abril de 2016  

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune  
 Os recursos do Intune a seguir introduzidos em abril de 2016 funcionam em implantações híbridas.  

- **Conformidade de usuário do MAM**

  Agora você pode exibir o status de suas políticas de gerenciamento de aplicativo para qualquer usuário no seu locatário do AAD (Azure Active Directory).  Para mais informações, confira [Monitor mobile app management policies with Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) (Monitorar as políticas de gerenciamento de aplicativo móvel como Microsoft Intune) na biblioteca do Intune.  

- **Controles de MAM para impedir a sincronização de contatos do Outlook (Android)**

  Há uma nova configuração disponível que permite que você impeça que um aplicativo sincronize contatos para o catálogo de endereços nativo em dispositivos Android. Essa nova configuração tem suporte inicialmente pelo aplicativo Outlook em dispositivos Android. Para mais informações, confira [Create and deploy mobile app management policies with Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) (Criar e implantar políticas de gerenciamento de aplicativo móvel com o Microsoft Intune) na biblioteca do Intune.  

- **Aprimoramentos no site do Portal da Empresa**

  Quando os usuários do Windows 10 Mobile e Windows Phone 8.1 estiverem instalando aplicativos de linha de negócios, agora eles verão os seguintes novos status, que fornecem a eles mais detalhes sobre o status de sua instalação:  

  -   **Aguardando sincronização do dispositivo** – o usuário tocou em "Instalar" e o dispositivo agora tenta sincronizar com a infraestrutura do Intune. A sincronização é necessária antes de concluir a instalação. A mensagem "Aguardando sincronização do dispositivo" também é um link que os usuários poderão tocar para ver instruções sobre como sincronizar manualmente seu dispositivo com o Intune se o processo de sincronização estiver demorando muito ou ficar paralisado.  

  -   **Baixando** – a solicitação de download do usuário está sendo processada e o dispositivo está baixando e instalando o aplicativo.  

- **Aprimoramentos no aplicativo do Portal da Empresa para Android**

  Os usuários que não tiverem registrado seu dispositivo no Intune e que não tiverem o certificado correto instalado não conseguirão entrar no aplicativo do Portal da Empresa para Android e verão a mensagem “Não é possível se conectar porque seu dispositivo não tem um certificado exigido.” A mensagem inclui um link "Como resolver isso" que os usuários podem tocar para ver as instruções para a instalação do certificado. Para ver as etapas que os usuários finais seguem para resolver o problema, confira [Falta ao dispositivo um certificado necessário](/intune/enduser/using-your-android-device-with-intune) na biblioteca do Intune.  

- **Aprimoramentos no aplicativo do Portal da Empresa para iOS**

  Foi adicionado suporte para a ação de puxar para atualizar a fim de atualizar o conteúdo na tela inicial, que inclui os aplicativos listados, os dispositivos listados e as informações de contato de TI. A ação de puxar para atualizar não verifica as informações de política ou conformidade, o que pode ser feito selecionando o bloco do dispositivo atual e tocando no botão **Sincronizar**.  

- **Aprimoramentos no aplicativo do Portal da Empresa para Windows 10 Mobile e Windows Phone 8.1**

  Quando os usuários finais estiverem instalando aplicativos de linha de negócios, agora eles verão uma experiência de instalação de aplicativo aprimorada. Se a instalação do aplicativo estiver demorando muito, os usuários poderão sincronizar manualmente seus dispositivos para forçar o processo de sincronização a continuar. Para examinar as instruções do usuário final, confira [Sync your device manually to speed up app installations](/intune/enduser/using-your-windows-device-with-intune) (Sincronizar o dispositivo manualmente para acelerar as instalações de aplicativo) na biblioteca do Intune.  

###  <a name="new-in-1604-technical-preview"></a>Novo no Technical Preview 1604
 Os novos recursos a seguir introduzidos em abril de 2016 estão disponíveis para implantações híbridas com o Intune e com o Configuration Manager Technical Preview 1604. Esses recursos exigem que você use o console do Configuration Manager para configurá-los e gerenciá-los.  

- **Localizar, gerenciar e distribuir aplicativos da Windows Store para Empresas para dispositivos Windows 10 por meio do console do Configuration Manager**


  O suporte para a Windows Store para Empresas está disponível no Configuration Manager Technical Preview 1604 para ajudá-lo a localizar, gerenciar e distribuir aplicativos para os dispositivos Windows 10 sendo gerenciados. Para detalhes, confira [Gerenciar aplicativos adquiridos por volume da Windows Store para Empresas](/sccm/core/get-started/capabilities-in-technical-preview-1604#manage-volume-purchased-apps-from-the-windows-store-for-business) em [Funcionalidades no Technical Preview 1604 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604).  

- **Configuração do SmartLock para dispositivos Android**

  Uma nova configuração foi adicionada ao item de configuração Android e Samsung KNOX Standard que permite controlar o recurso SmartLock em dispositivos Android compatíveis.  Você pode usar essa configuração para impedir que os usuários finais configurem o SmartLock. Confira [Configuração do SmartLock para dispositivos Android](/sccm/get-started/capabilities-in-technical-preview-1604#smartlock-setting-for-android-devices) no [Funcionalidades do Technical Preview 1604 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604.md).  

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)  
 Não foi realizada a introdução de nenhum recurso híbrido novo em abril de 2016 para o Configuration Manager (Branch Atual).  

##  <a name="new-hybrid-features-in-march-2016"></a>Novos recursos híbridos em março de 2016  

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune  
 Os recursos do Intune a seguir introduzidos em março de 2016 funcionam em implantações híbridas.  

- **Controles de MAM para impedir a sincronização de contatos do Outlook (iOS)**

  Há uma nova configuração disponível que permite que você impeça que um aplicativo sincronize contatos para o catálogo de endereços nativo em dispositivos iOS. Essa nova configuração tem suporte pelo aplicativo Outlook em dispositivos iOS. Para obter mais detalhes sobre esta e outras configurações, confira [Create and deploy MAM policies](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) (Criar e implantar políticas de MAM) na biblioteca do Intune.  

- **O Skype for Business Online dá suporte ao acesso condicional**

  Você pode definir uma política de acesso condicional para o Skype for Business Online para que ele possa ser acessado apenas por dispositivos Android e iOS gerenciados e compatíveis.  Para obter detalhes, confira [Manage access to Skype for Business Online](/intune/deploy-use/restrict-access-to-skype-for-business-online-with-microsoft-intune) (Gerenciar o acesso ao Skype for Business Online) na biblioteca do Intune.  

- **Suporte para iOS 9.3**

  Na segunda-feira de 21 de março, a Apple anunciou a disponibilidade do iOS 9.3. Todos os recursos existentes do Intune disponíveis no momento para o gerenciamento de dispositivos iOS continuarão a funcionar perfeitamente quando os usuários atualizarem seus dispositivos para o iOS 9.3.  

- **Pacotes de aplicativos Windows disponíveis diretamente do site do Portal da Empresa**

  Os usuários de computadores Windows 8, Windows 8.1 e Windows RT agora podem instalar pacotes de aplicativos Windows (com a extensão .appx) diretamente do site do Portal da Empresa. Anteriormente, você precisava implantar ou os usuários precisavam instalar o aplicativo do Portal da Empresa em seus dispositivos para instalar aplicativos.  

- **Os usuários podem bloquear remotamente o dispositivo pelo site do Portal da Empresa**

  Uma nova opção de Bloqueio Remoto foi adicionada ao site do Portal da Empresa para permitir que os usuários bloqueiem remotamente seu dispositivo pelo Portal caso o dispositivo seja perdido ou roubado.  

- **Aproveitar o gerenciamento "Open-in" do iOS para dispositivos que são registrados em uma solução de MDM de terceiros**

  Você pode usar seu fornecedor de MDM (gerenciamento de dispositivo móvel) de terceiros para aproveitar o gerenciamento "Open-in" do iOS. Você pode definir as restrições nas definições de perfil de configuração e implantar o aplicativo usando seu software de MDM. Quando o usuário instala o aplicativo gerenciado, as restrições são aplicadas. Leia os detalhes: [Microsoft Intune mobile app management policies and iOS Open In](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune) (Políticas de gerenciamento de aplicativo móvel do Microsoft Intune e Open in do iOS) na biblioteca do Intune.  

- **Aplicativos da Microsoft que dão suporte ao MAM**

  A lista de aplicativos da Microsoft que podem ser usados com políticas de gerenciamento de aplicativo móvel do Intune foi atualizada para incluir os aplicativos mais recentes (para dispositivos que são registrados apenas no Intune).  

- **Implantar o Adobe Reader para o Microsoft Intune para dispositivos iOS gerenciados pelo Intune em sua empresa**

  O aplicativo Adobe Reader para iOS agora pode ser gerenciado em dispositivos registrados com a política de gerenciamento de aplicativo móvel do Intune.  

- O aplicativo de compartilhamento Rights Management tem suporte pelo Android

  Os administradores de TI podem implantar políticas de gerenciamento de aplicativo móvel para que os usuários finais possam exibir arquivos de imagens, AV e PDF de forma mais segura, independentemente de a equipe de TI usar ou não o Intune para gerenciar os dispositivos.  

- **Aprimoramentos no aplicativo do Portal da Empresa para Android e iOS**

  -   Quando os usuários iniciarem um aplicativo que é gerenciado pelo MAM (gerenciamento de aplicativo móvel), eles verão uma mensagem notificando-os de que o aplicativo é gerenciado pela empresa. Os usuários agora podem tocar no link “Saiba Mais” para obter mais informações aqui sobre o que significa “aplicativos gerenciados”. Eles também podem tocar em “Não Mostrar Novamente” para que a mensagem não apareça mais ao iniciar o aplicativo.  

  -   Foram adicionadas novas telas para orientar os usuários pelo processo de registro e fornecer mais informações sobre por que os usuários devem registrar e o que os administradores de TI podem e não podem ver em seus dispositivos registrados.  

  -   Mensagens de erro de registro agora são exibidas no aplicativo do Portal da Empresa.  

### <a name="new-in-configuration-manager-technical-preview"></a>Novo no Configuration Manager Technical Preview  
 Não foi realizada a introdução de nenhum recurso híbrido novo em março de 2016 para o Configuration Manager Technical Preview.  

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)  
 Os novos recursos a seguir introduzidos em março de 2016 estão disponíveis para implantações híbridas com o Intune e com a versão 1602 do Configuration Manager (Branch Atual). Esses recursos exigem que você use o console do Configuration Manager para configurá-los e gerenciá-los.  

- **Políticas de configuração de aplicativo iOS**

  Na versão 1602 do Configuration Manager (Branch Atual), você pode usar as políticas de configuração de aplicativo para fornecer configurações que podem ser necessárias quando o usuário executa um aplicativo iOS. Para obter detalhes, consulte [Configurar aplicativos iOS com políticas de configuração de aplicativos no System Center Configuration Manager](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).  

- **Gerenciar aplicativos iOS adquiridos por volume**

  Na versão 1602 do Configuration Manager (Branch Atual), você implantar e gerenciar aplicativos comprados em volume com o VPP (Programa de Licenciamento por Volume) da Apple, importando as informações de licença da loja de aplicativos e acompanhando quantas licenças você usou. Para obter detalhes, consulte [Gerenciar aplicativos iOS adquiridos por volume com o System Center Configuration Manager](/sccm/apps/deploy-use/manage-volume-purchased-ios-apps).  

- **Criação automática de aplicativos móveis do Office**

  A partir da versão 1602 do Configuration Manager (Branch Atual), os seguintes aplicativos móveis do Microsoft Office para Android e iOS são criados ao atualizar da versão 1511:  

  -   Microsoft Word  
  -   Microsoft Excel  
  -   Microsoft PowerPoint  
  -   Microsoft OneDrive  
  -   Microsoft OneNote (apenas iOS)  
  -   Microsoft Outlook  

  Você encontrará esses aplicativos no nó Aplicativos do console do Configuration Manager. Para mais informações sobre a implantação de aplicativos, confira [Como implantar aplicativos com o System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).  

- **Configurações do modo de quiosque para dispositivos Android Samsung KNOX Standard**

  O modo de quiosque permite bloquear um dispositivo para permitir que somente alguns recursos funcionem.  Começando na versão 1602 do Configuration Manager (branch atual), você pode especificar configurações do modo de quiosque para dispositivos Samsung KNOX Standard. Para obter detalhes, consulte [Como criar itens de configuração para dispositivos Android e Samsung KNOX Standard gerenciados sem o cliente do System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client).  

- **Bloqueio de Ativação do iOS**

  A partir da versão 1602 do Configuration Manager (Branch Atual), você pode gerenciar o Bloqueio de Ativação do iOS, um recurso do aplicativo Buscar Meu iPhone para dispositivos com iOS 7.1 e posteriores. O Bloqueio de Ativação é habilitado automaticamente quando o aplicativo Buscar meu iPhone for usado em um dispositivo.  Para obter detalhes, confira [Manage iOS Activation Lock bypass for System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock) (Gerenciar o bypass do Bloqueio de Ativação do iOS para o System Center Configuration Manager).  



<!--HONumber=Jan17_HO1-->


