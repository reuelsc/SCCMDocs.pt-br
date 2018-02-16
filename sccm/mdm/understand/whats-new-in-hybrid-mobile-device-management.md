---
title: "Novidades no MDM híbrido"
titleSuffix: Configuration Manager
description: "Saiba mais sobre os novos recursos de gerenciamento de dispositivo móvel disponíveis para implantações híbridas com o Configuration Manager e o Intune."
ms.custom: na
ms.date: 02/06/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: c724d9eafde6aa9abc0d3f9bfa867418046b2ecb
ms.sourcegitcommit: 389c4e5b4e9953b74c13b1689195f99c526fa737
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Novidades no gerenciamento de dispositivo móvel híbrido com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo fornece detalhes sobre os novos recursos de MDM (gerenciamento de dispositivo móvel) disponíveis para implantações híbridas com o System Center Configuration Manager e o Microsoft Intune.     

> [!Note]    
> O Intune no Azure é a solução de MDM recomendada pela Microsoft.     
> - Para obter detalhes sobre novos recursos e atualizações no Intune autônomo, consulte [Novidades do Intune](https://docs.microsoft.com/intune/whats-new).    
> - Para obter detalhes de como migrar para o Intune autônomo, consulte [Migrate hybrid MDM users and devices to Intune standalone](https://docs.microsoft.com/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa) (Migrar usuários e dispositivos de MDM híbrido para o Intune autônomo).
> - Para obter detalhes sobre as atualizações da interface do usuário do Intune e o MDM híbrido, consulte [Atualizações da interface do usuário para aplicativos de usuário final do Intune](https://docs.microsoft.com/intune/whats-new-app-ui). 

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilidade com versões do Configuration Manager  
Cada seção deste artigo lista recursos híbridos em três categorias diferentes. Use as seguintes diretrizes para determinar a compatibilidade dos recursos em cada categoria com versões diferentes do Configuration Manager:  

|Categorias do recurso|Descrição|
|-|-|
|**Novo no Microsoft Intune** | De modo geral, todos os recursos listados nesta categoria devem funcionar com todas as versões do Configuration Manager. Isso inclui versões do System Center 2012 R2 Configuration Manager, uma vez que esses recursos exigem apenas o serviço Intune e não exigem funcionalidades adicionais no Configuration Manager.|
|**Novo no Configuration Manager Technical Preview**| Todos os recursos listados nessa categoria funcionam apenas com a versão de Technical Preview especificada. Para testar esses recursos, você deve instalar a versão de Technical Preview especificada na descrição do recurso. Para mais informações, confira [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md).|
|**Novo no Configuration Manager (Branch Atual)**| Todos os recursos listados nessa categoria funcionam apenas com a versão especificada do Configuration Manager (Branch Atual), como a versão 1511 ou 1602. Se estiver usando uma versão mais antiga do Configuration Manager para sua implantação híbrida, atualize para a versão do Configuration Manager (Branch Atual) especificada na descrição do recurso. Para mais informações, confira [Atualização para o System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|


## <a name="january-2018"></a>Janeiro de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Aprovar o aplicativo do Portal da Empresa para Android for Work** <!--1797090 -->    
  Se sua organização usa o Android for Work, é necessário aprovar manualmente o aplicativo de Portal da Empresa para Android, para que ele continue a receber atualizações automáticas da Google Play Store gerenciada.

- **Políticas de Acesso Condicional para o Intune só está disponível no Portal do Azure**  <!-- 1737088 1634311 -->    
  A partir desta versão, é preciso configurar e gerenciar suas políticas de Acesso Condicional no [Portal do Azure](https://portal.azure.com) do **Acesso Condicional** do **Azure Active Directory** > . Para sua conveniência, você também pode acessar esta folha do Intune no Portal do Azure no **Acesso Condicional** do **Intune** > .

- **Atualizações para emails de conformidade** <!--1637547 -->    
  Quando um email é enviado para relatar um dispositivo incompatível, os detalhes sobre o dispositivo não compatível são incluídos na mensagem. 


- **Nova funcionalidade para a ação "Resolver" para dispositivos Android** <!--1583480-->    
  O aplicativo Portal da Empresa para Android está expandindo a ação "Resolver" para **Atualizar configurações do dispositivo** a fim de resolver [problemas de criptografia de dispositivo](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android).

- **Bloqueio remoto disponível no aplicativo de Portal da Empresa para Windows 10**<!--676506-->     
  Agora, os usuários finais podem bloquear remotamente seus dispositivos do aplicativo do Portal da Empresa para Windows 10. Isso não será exibido para o dispositivo local que ele estiver usando ativamente.

- **Resolução mais fácil de problemas de conformidade para o aplicativo de Portal da Empresa para Windows 10** <!--676546-->    
  Usuários finais com dispositivos Windows poderão tocar no motivo da não conformidade no aplicativo Portal da Empresa. Quando possível, isso os levará diretamente para o local correto no aplicativo de configurações para corrigir o problema.

## <a name="december-2017"></a>Dezembro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Implantações de aplicativo disponíveis agora com suporte no Android Enterprise**    
  Agora você pode implantar aplicativos do Android Enterprise (anteriormente Android for Work) como **Disponíveis**, além de **Obrigatórios**. Para obter detalhes, consulte [Criar aplicativos Android com o System Center Configuration Manager](/sccm/mdm/deploy-use/creating-android-applications).


## <a name="november-2017"></a>Novembro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Protocolo de texto permitido de aplicativos gerenciados** <!-- 1414050  -->    
  Aplicativos gerenciados pelo SDK do Aplicativo do Intune podem enviar mensagens SMS.

- **O aplicativo do Portal da Empresa para macOS está disponível** <!--1541700-->    
  O Portal da Empresa do Intune no macOS tem uma experiência atualizada, que foi otimizada para exibir com clareza todas as notificações de conformidade e informações de que seu usuário precisa para todos os dispositivos que eles registraram. E, quando o Portal da Empresa do Intune tiver sido implantado em um dispositivo, a Atualização Automática da Microsoft para macOS fornecerá atualizações para ele. Você pode baixar o novo Portal da Empresa do Intune para macOS fazendo o logon no site do Portal da Empresa do Intune a partir de um dispositivo macOS.

- **Agora o Microsoft Planner faz parte da lista do MAM (gerenciamento de aplicativo móvel) de aplicativos aprovados** <!-- 1248473 -->    
  Agora o aplicativo Microsoft Planner para iOS e Android faz parte dos aplicativos aprovados para o MAM (gerenciamento de aplicativo móvel). O aplicativo pode ser configurado pela folha de Proteção de Aplicativo do Intune no portal do Azure para todos os locatários. Para obter detalhes, confira [Lista MAM de aplicativos aprovados](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).

- **Acesso a logs de aplicativos gerenciados para iOS** <!-- 1469920 -->    
  Agora os usuários finais com o Browser gerenciado instalado podem exibir o status de gerenciamento de todos os aplicativos publicados da Microsoft e enviar logs para solucionar problemas de seus aplicativos iOS gerenciados.
  
  Saiba como habilitar o modo de solução de problemas no Managed Browser em um dispositivo iOS, consulte [How to access to managed app logs using the Managed Browser on iOS](https://docs.microsoft.com/intune/app-configuration-managed-browser#how-to-access-to-managed-app-logs-using-the-managed-browser-on-ios) (Como acessar logs de aplicativos gerenciados usando o Managed Browser no iOS).

- **Melhorias no fluxo de trabalho de configuração do dispositivo no Portal da Empresa para iOS na versão 2.9.0**    
  Melhoramos o fluxo de trabalho de configuração de dispositivo no aplicativo do Portal da Empresa para iOS. A linguagem é mais fácil de usar e combinamos as telas sempre que possível. Também tornamos a linguagem mais específica para sua empresa, usando o nome da empresa em todo o texto da instalação. Veja esse fluxo de trabalho atualizado na página [novidades na interface do usuário do aplicativo](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-november-13-2017).

- **Solicitações de comentários para o aplicativo do Portal da Empresa para Android** <!--1165249-->    
Agora o aplicativo do Portal da Empresa para Android solicita comentários do usuário final. Este comentário será enviado diretamente para a Microsoft e fornecerá aos usuários finais uma oportunidade de avaliar o aplicativo na loja pública do Google Play. Os comentários não são obrigatórios e podem facilmente ser ignorados para que os usuários possam continuar usando o aplicativo. 

- **Informar os usuários finais sobre quais informações do dispositivo podem ser vistas para dispositivos Windows 10** <!--1337920-->    
Adicionamos **Tipo de propriedade** à tela Detalhes do dispositivo no aplicativo do Portal da Empresa para Windows 10. Isso permitirá que os usuários obtenham mais informações sobre privacidade diretamente a partir desta página nos documentos do usuário final do Intune. Eles também poderão localizar essas informações na tela **Sobre**.

- **Nova ação "Resolver" disponível para dispositivos Android** <!--1583480-->    
  O aplicativo do Portal da Empresa para Android está introduzindo uma ação "Resolver" na página _Atualizar as configurações do dispositivo_. Selecionar esta opção levará o usuário final diretamente para a configuração que está causando a incompatibilidade com o seu dispositivo. O aplicativo do Portal da Empresa para Android oferece suporte atualmente a essa ação para as configurações de [senha do dispositivo](https://docs.microsoft.com/intune-user-help/set-your-pin-or-password-android), [criptografia do dispositivo](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android), [depuração de USB](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-usb-debugging-android), e [Fontes Desconhecidas](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-unknown-sources-android). 


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)

- **Ações de não conformidade** <!--1321366 -->    
  Agora é possível configurar uma sequência de ações ordenadas por tempo aplicadas aos dispositivos que estão fora de conformidade. Por exemplo, é possível notificar os usuários sobre dispositivos que não estão em conformidade por email ou marcá-los como não em conformidade. Para obter detalhes, consulte [Set up actions for non-compliance](/sccm/mdm/deploy-use/actions-for-noncompliance) (Configurar ações de não conformidade).

- **Novas configurações de política de gerenciamento de aplicativo móvel** <!-- 1324760 -->    
  As configurações a seguir foram adicionadas nas configurações de política de gerenciamento de aplicativos móveis:
  - **Desabilitar sincronização de contato**: impede que o aplicativo salve dados no aplicativo Contatos nativo do dispositivo.
  - **Desabilitar impressão**: impede que o aplicativo imprima dados corporativos ou de estudante.

  Veja [proteger aplicativos usando políticas de proteção de aplicativos no Configuration Manager](/sccm/mdm/deploy-use/protect-apps-using-mam-policies) para testar as novas configurações de política de proteção do aplicativo.

- **Suporte a dispositivos Windows 10 ARM64** <!-- 1355000 -->    
  Os cenários híbridos de MDM (gerenciamento de dispositivo móvel) terão suporte em dispositivos ARM64 executando o Windows 10 quando esses dispositivos ficarem disponíveis. Para obter mais detalhes, confira [Suporte a dispositivos Windows 10 ARM64](/sccm/core/plan-design/changes/whats-new-in-version-1710#windows-10-arm64-device-support).

- **Melhoria na experiência do perfil de VPN no Console do Configuration Manager** <!-- 1318232 -->    
  Com esta versão, as páginas de assistente e de propriedades do perfil de VPN foram atualizadas para exibir as configurações apropriadas para a plataforma selecionada. Este recurso estava disponível anteriormente no Configuration Manager Technical Preview 1709 agora está disponível em implantações híbridas com o Intune e a versão 1710 do Configuration Manager (Branch Atual):
  - [Melhoria da experiência do perfil de VPN no Console do Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1710#improved-vpn-profile-experience-in-configuration-manager-console).


### <a name="new-in-configuration-manger-technical-preview-1711"></a>Novo no Configuration Manager Technical Preview 1711

- **Novas opções de política de conformidade para Windows 10** Agora, você pode configurar as novas opções de políticas de conformidade para dispositivos Windows 10. As novas configurações incluem políticas de Firewall, Controle de Conta de Usuário, Windows Defender Antivírus e controle de versões de build do sistema operacional. Para obter mais detalhes, confira [Novas opções de política de conformidade para Windows 10](/sccm/core/get-started/capabilities-in-technical-preview-1711#new-compliance-policy-options-for-windows-10).


## <a name="october-2017"></a>Outubro de 2017

### <a name="new-in-configuration-manager-technical-preview-1709"></a>Novo no Configuration Manager Technical Preview 1709

- **Melhoria da experiência do perfil de VPN no Console do Configuration Manager** <!-- 1313282 -->     
  Agora, as configurações de perfil VPN são filtradas de acordo com a plataforma. Quando você cria novos perfis de VPN, cada plataforma com suporte contém apenas as configurações apropriadas para a plataforma. Os perfis de VPN existentes não são afetados. Leia mais sobre essa mudança [aqui](/sccm/core/get-started/capabilities-in-technical-preview-1709#improved-vpn-profile-experience-in-configuration-manager-console).


### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune  

- **Ajudando seus usuários a se ajudarem com o aplicativo de Portal da Empresa para Android** <!-- 1573324, 1573150, 1558616, 1564878 -->      
  O aplicativo de Portal da Empresa para Android adicionou instruções para os usuários finais para ajudá-los a entender e, sempre que possível, solucionar problemas de forma independente em novos casos de uso.
    - Os usuários finais serão levados ao [portal do Azure Active Directory](https://account.activedirectory.windowsazure.com/r/#/profile) para remover um dispositivo se eles tiverem atingido o número máximo de dispositivos que têm permissão para adicionar.
    - Os usuários finais recebem etapas a serem seguidas para ajudá-los a [corrigir erros de ativação em dispositivos Samsung Knox](https://go.microsoft.com/fwlink/?linkid=859718) ou a [desligar o modo de economia de energia](https://docs.microsoft.com/intune-user-help/power-saving-mode-android). Se nenhuma dessas soluções resolver o problema, forneceremos uma explicação de como [enviar logs para a Microsoft](https://docs.microsoft.com/intune-user-help/send-logs-to-microsoft-android).

- **Indicador de progresso da instalação do dispositivo no Portal da Empresa para Android** <!--1565657-->    
  O aplicativo do Portal da Empresa para Android mostra um indicador de progresso da instalação do dispositivo quando um usuário está registrando seu dispositivo. O indicador mostra novos status, começando com "Configurando seu dispositivo...", em seguida, "Registrando seu dispositivo...", "Concluindo o registro do seu dispositivo..." e "Concluindo a instalação do seu dispositivo...".  

- **Suporte a autenticação baseada em certificado no Portal da Empresa para iOS** <!--1029830-->    
  Adicionamos suporte para CBA (autenticação baseada em certificado) no aplicativo do Portal da Empresa para iOS. Usuários com CBA inserem seu nome de usuário, depois, tocam no link "Entrar com um certificado". CBA já é compatível com os aplicativos Portal da Empresa para Android e Windows. Saiba mais na página para [entrar no aplicativo Portal da Empresa](https://docs.microsoft.com/intune-user-help/sign-in-to-the-company-portal).

- **Aprimoramentos no fluxo de trabalho de configuração do dispositivo no Portal da Empresa** <!--1490692-->    
  Melhoramos o fluxo de trabalho de configuração de dispositivo no aplicativo Portal da Empresa para Android. A linguagem é mais fácil de usar e mais específica para sua empresa. Combinamos as telas sempre que possível. Veja isso na página [Novidades na interface do usuário do aplicativo](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-october-2-2017).

- **Orientação aprimorada para a solicitação de acesso aos contatos em dispositivos Android** <!--1484985-->    
  O aplicativo Portal da Empresa para Android geralmente exige que o usuário final aceite a permissão de Contatos. Se um usuário final recusar esse acesso, verá uma notificação no aplicativo alertando-o para concedê-lo para acesso condicional. 

- **Proteger a correção de inicialização para Android** <!--1490712-->    
  Os usuários finais com dispositivos Android poderão tocar no motivo da não conformidade no aplicativo Portal da Empresa. Quando possível, isso os levará diretamente para o local correto no aplicativo de configurações para corrigir o problema. 

- **Notificações por push adicionais para usuários finais no aplicativo Portal da Empresa para Android Oreo** <!--1475932 -->    
  Os usuários finais verão notificações adicionais para indicar quando o aplicativo Portal da Empresa para Android Oreo está executando tarefas em segundo plano, como recuperar as políticas do serviço Intune. As notificações aumentam a transparência para os usuários finais, informando sobre quando o Portal da Empresa estiver executando tarefas administrativas em seu dispositivo. Isso faz parte da [otimização geral da interface de usuário do Portal da Empresa](https://blogs.technet.microsoft.com/intunesupport/2017/08/21/android-8-0-o-behaviour-changes-and-microsoft-intune) para o aplicativo Portal da Empresa para Android Oreo. 

- **Novos comportamentos para o aplicativo Portal da Empresa para Android com perfis de trabalho** <!--1485783-->    
  Quando você registra um dispositivo com Android for Work com um perfil de trabalho, é o aplicativo Portal da Empresa no perfil de trabalho que executa tarefas de gerenciamento no dispositivo. 

  A menos que você esteja usando um aplicativo habilitado para MAM no perfil particular, o aplicativo Portal da Empresa para Android não terá qualquer uso. Para melhorar a experiência do perfil de trabalho, o Intune ocultará automaticamente o aplicativo Portal da Empresa pessoal após um registro de perfil de trabalho bem-sucedido.

  O aplicativo Portal da Empresa para Android pode ser habilitado a qualquer momento no perfil pessoal navegando até [Portal da Empresa na Play Store](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) e tocando em **Habilitar**.

- **Portal da Empresa para Windows 8.1 e Windows Phone 8.1 mudando para o modo de manutenção** <!--1428681-->    
 Foi adicionado um aviso para anunciar que os aplicativos Portal da Empresa para Windows 8.1 e Windows Phone 8.1 estão mudando para modo de manutenção. Para obter mais detalhes, veja [Avisos](#notices).  

- **Bloquear registro de dispositivo Samsung Knox sem suporte** <!-- 1490695 -->    
  O aplicativo Portal da Empresa tenta registrar apenas os dispositivos Samsung Knox com suporte. Para evitar erros de ativação do KNOX que impedem o registro do MDM, a tentativa do registro do dispositivo só ocorrerá se o dispositivo for exibido na [lista de dispositivos publicada pela Samsung](https://www.samsungknox.com/knox-supported-devices/knox-workspace). Os dispositivos Samsung podem ter números de modelo que oferecem suporte a KNOX, enquanto outros não. Verifique a compatibilidade do Knox com o revendedor de seu dispositivo antes de comprar e implantar. Encontre a lista completa de dispositivos verificados nas [configurações de política do Android e Samsung KNOX Standard](https://docs.microsoft.com/intune-classic/deploy-use/android-policy-settings-in-microsoft-intune#supported-samsung-knox-standard-devices).

- **Fim do suporte para Android 4.3 e inferior** <!--1171126, 1326920 -->    
  Um aviso foi adicionado para o fim do suporte para Android 4.3 e inferior. Para obter mais detalhes, veja [Avisos](#notices).

- **Informar aos usuários finais quais informações do dispositivo podem ser vistas em dispositivos registrados** <!--1165314-->    
  Estamos adicionando o **Tipo de Propriedade** à tela de Detalhes do Dispositivo em todos os aplicativos Portal da Empresa. Isso permitirá que os usuários obtenham mais informações sobre privacidade diretamente do artigo [Quais informações sua empresa pode ver?](https://docs.microsoft.com/intune-user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune). Isso será implantado em todos os aplicativos Portal da Empresa em breve. Anunciamos isso para iOS em [setembro](https://docs.microsoft.com/intune/whats-new#week-of-september-11-2017). 


## <a name="september-2017"></a>Setembro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune     

- **Ação de atualização adicionada ao aplicativo Portal da Empresa para Windows 10**<!-- 1132468 -->    
    O aplicativo Portal da Empresa para Windows 10 permite que os usuários atualizem os dados no aplicativo deslizando para atualizar ou, em áreas de trabalho, pressionando F5.

- **Informar os usuários finais quais informações do dispositivo podem ser vistas para o iOS** <!--739894-->    
    Adicionamos **Tipo de Propriedade** à tela de detalhes do dispositivo no aplicativo Portal da Empresa para iOS. Isso permitirá que os usuários obtenham mais informações sobre privacidade diretamente a partir desta página nos documentos do usuário final do Intune. Eles também poderão localizar essas informações na tela Sobre. 

- **Frases mais fáceis de entender para o aplicativo Portal da Empresa para Android** <!---1396349-->       
    O processo de registro para o aplicativo Portal da Empresa para Android foi simplificado com o novo texto para facilitar a inscrição para usuários finais. Se você tiver a documentação de inscrição personalizada, atualize-o para refletir as novas telas. Você pode localizar as imagens de amostra na nossa página [Atualizações de interface do usuário para aplicativos de usuário final do Intune](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-september-11-2017).

- **Aplicativo Portal da Empresa do Windows 10 adicionado à política de permissão de Proteção de Informações do Windows**<!-- 677129 -->    
    O aplicativo Portal da Empresa do Windows 10 foi atualizado para dar suporte ao WIP (Proteção de Informações do Windows). O aplicativo pode ser adicionado à política de permissão do WIP. Com essa alteração, o aplicativo não precisa mais ser adicionado à lista **Isento**. 

     Apenas um item de configuração WIP única pode ser entregue a um dispositivo.  Se dois itens de configuração WIP forem direcionados para o mesmo dispositivo, nenhuma política WIP será aplicável.

- **Aviso de fim de suporte adicionado para iOS 8.0**    
    Um aviso foi adicionado para o fim do suporte para iOS 8.0. Para obter mais detalhes, veja [Avisos](#notices).

## <a name="august-2017"></a>Agosto de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune     

- **Nova experiência conectada para usuários do Portal da Empresa Android e usuários da Política de Proteção de Aplicativo** <!-- 621669 -->    
Os usuários finais agora podem procurar aplicativos, gerenciar dispositivos e exibir as informações de contato de TI usando o aplicativo Portal da Empresa Android sem inscrever os respectivos dispositivos Android. Além disso, se um usuário final já usa um aplicativo protegido pelas Políticas de Proteção de Aplicativo do Intune e iniciar o Portal da Empresa Android, o usuário final não receberá mais uma solicitação para registrar o dispositivo.


## <a name="july-2017"></a>Julho de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Avisos de fim de suporte adicionados para Android e Windows Phone**

    Novos avisos foram adicionados para o fim de suporte das versões Android e Windows Phone. Para obter mais detalhes, veja [Avisos](#notices).


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)

Os seguintes recursos que estavam anteriormente disponíveis nas versões do Configuration Manager Technical Preview agora estão disponíveis em implantações híbridas com o Intune e a versão 1706 do Configuration Manager (branch atual).

- [Suporte do Entrust para autoridades de certificação Entrust](/sccm/core/get-started/capabilities-in-technical-preview-1706#support-for-entrust-certification-authorities)
- [Novas configurações de política de gerenciamento de aplicativo móvel](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-mobile-application-management-policy-settings)
- [Atualizações para configuração de compartilhamento do Android for Work](/sccm/core/plan-design/changes/whats-new-in-version-1706#updates-to-android-for-work-sharing-configuration)
- [Novas regras de política de conformidade do dispositivo](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-device-compliance-policy-rules)
- [Novas definições de configuração para dispositivos com Windows 10 que não são gerenciados com o cliente do Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client)
- [Suporte do Cisco (IPsec) para perfis de VPN do macOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#cisco-ipsec-support-for-macos-vpn-profiles)
- [Restrições de inscrição do Android e iOS](/sccm/core/plan-design/changes/whats-new-in-version-1706#android-and-ios-enrollment-restrictions) 

## <a name="june-2017"></a>Junho de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Alterar sua autoridade de MDM**

  A partir do Configuration Manager versão 1610, você pode alterar sua autoridade MDM sem precisar entrar em contato com o Suporte da Microsoft e sem a necessidade de cancelar o registro e registrar novamente os dispositivos gerenciados existentes. Para obter detalhes, veja [Alterar sua autoridade de MDM](/sccm/mdm/deploy-use/change-mdm-authority).

- **Integração gerenciada de proxy do navegador e aplicativo**

  O Intune Managed Browser agora pode ser integrado ao serviço de Proxy de Aplicativo do Azure AD para permitir que os usuários acessem sites internos, mesmo quando estão trabalhando remotamente. Os usuários do navegador inserem a URL normalmente e o Managed Browser encaminha a solicitação por meio do gateway Web do proxy de aplicativo. Para saber mais, veja [Gerenciar o acesso à Internet usando políticas no navegador gerenciado](https://docs.microsoft.com/intune/app-configuration-managed-browser).

- **Agora, o aplicativo Portal da Empresa para Android tem uma nova experiência do usuário final para as Políticas de Proteção do Aplicativo**

  Com base nos comentários do cliente, modificamos o aplicativo Portal da Empresa para Android mostrar um botão **Acessar Conteúdo da Empresa**. A intenção é impedir que os usuários finais passem desnecessariamente pelo processo de inscrição quando eles só precisam acessar os aplicativos que dão suporte a Políticas de Proteção do Aplicativo, um recurso de gerenciamento de aplicativo móvel do Intune. Veja essas alterações na página [Novidades na interface do usuário do aplicativo](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Nova ação de menu para remover facilmente o Portal da Empresa**

  Com base nos comentários do usuário, o aplicativo Portal da Empresa para Android adicionou uma nova ação de menu para iniciar a remoção do Portal da Empresa de seu dispositivo. Esta ação remove o dispositivo do gerenciamento do Intune para que o aplicativo possa ser removido do dispositivo pelo usuário. Veja essas alterações na página [Novidades na interface do usuário do aplicativo](https://docs.microsoft.com/intune/whats-new-app-ui) e na [documentação de usuário final do Android](https://docs.microsoft.com/intune-user-help/unenroll-your-device-from-intune-android).

- **Aprimoramentos na sincronização de aplicativo com a Atualização do Windows 10 para Criadores**

  O aplicativo Portal da Empresa para Windows 10 iniciará automaticamente uma sincronização para solicitações de instalação de aplicativo para dispositivos com a Atualização do Windows 10 para Criadores (versão 1703). Isso reduzirá o problema de atraso das instalações de aplicativos durante o estado de "Sincronização Pendente". Além disso, os usuários poderão iniciar manualmente uma sincronização de dentro do aplicativo. Veja essas alterações na página [Novidades na interface do usuário do aplicativo](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Nova experiência orientada para o Portal da Empresa do Windows 10**

  O aplicativo do Portal da Empresa para Windows 10 inclui uma experiência passo a passo interativa do Intune para dispositivos que não foram identificados nem registrados. A nova experiência fornece instruções passo a passo que guiam o usuário pelo processo de inscrição no Azure Active Directory (exigido para recursos de Acesso Condicional) e inscrição de MDM (exigido para os recursos de gerenciamento de dispositivo). A experiência guiada estará acessível na home page do Portal da Empresa. Os usuários podem continuar a usar o aplicativo se não concluírem o registro e inscrição, mas enfrentarão uma funcionalidade limitada.

  Esta atualização só fica visível em dispositivos que executam a Atualização de Aniversário do Windows 10 (build 1607) ou superior. Veja essas alterações na página [Novidades na interface do usuário do aplicativo](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Aprimoramentos nos blocos de aplicativo no aplicativo Portal da Empresa para iOS**

  Atualizamos o design dos blocos do aplicativo na home page a fim de refletir a cor de identidade visual que você definiu para o Portal da Empresa. Para saber mais, veja [Novidades na interface do usuário do aplicativo](https://docs.microsoft.com/intune/whats-new-app-ui).

- **O seletor de conta já está disponível para o aplicativo Portal da Empresa para iOS**

  Os usuários de dispositivos iOS poderão ver nosso novo seletor de conta ao entrar no Portal da Empresa se usarem sua conta corporativa ou de estudante para entrar em outros aplicativos da Microsoft. Para saber mais, veja [Novidades na interface do usuário do aplicativo](https://docs.microsoft.com/intune/whats-new-app-ui).

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Novidades da Visualização Técnica 1706 do Configuration Manager

- **Novas definições de item de configuração do Windows**<!-- 1354715 -->    

  Novos itens de configuração do Windows estão disponíveis para as categorias de configuração de Senha, Dispositivo, Armazenamento e Microsoft Edge. Para saber mais, confira [Novas definições de item de configuração do Windows](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings).

- **Novas regras de política de conformidade do dispositivo**    

  Agora você pode definir novas opções de políticas de conformidade que estavam disponíveis somente no Intune autônomo. Para obter detalhes, confira [Aprimoramentos na política de conformidade de dispositivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules).

- **Restrições de inscrição do Android e iOS** <!-- 1290826 -->      

  Os administradores podem especificar que os usuários não podem inscrever dispositivos Android ou iOS pessoais no ambiente híbrido. Isso permite que você limite os dispositivos inscritos a dispositivos da empresa ou iOS previamente declarados inscritos somente com o Programa de Registro de Dispositivos. Para obter detalhes, confira [Restrições de inscrição do Android e iOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions).

- **Suporte para autoridades de certificação Entrust** <!-- 1350740 -->     

  Agora, o Configuration Manager dá suporte a autoridades de certificação Entrust; isso permite o envio de certificados PFX para dispositivos registrados no Microsoft Intune.    

  Você pode configurar o Entrust como a autoridade de certificação ao adicionar a função Ponto de Registro de Certificado no Configuration Manager. Ao adicionar um novo perfil de certificado que emite os certificados PFX, você pode selecionar uma autoridade de certificação Microsoft ou Entrust.

  **Problema conhecido**: na visualização técnica 1706, os certificados PFX não são emitidos para autoridades de certificação da Microsoft. Isso não afeta os certificados PFX importados ou perfis SCEP.

- **Suporte do Cisco (IPsec) para perfis VPN macOS** <!-- 1321367 -->    

  Você pode criar um perfil VPN do macOS com Cisco (IPsec) como o tipo de conexão. Para saber mais, confira [Criar perfis VPN](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).


## <a name="april-2017"></a>Abril de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **MyApps disponível para o Navegador Gerenciado**

  Agora, o Microsoft MyApps tem um suporte melhor dentro do Navegador Gerenciado. Os usuários do Navegador Gerenciado que não são destinados ao gerenciamento serão levados diretamente para o serviço MyApps, onde poderão acessar seus aplicativos SaaS provisionados pelo administrador. Os usuários que são destinados ao gerenciamento do Intune ainda poderão acessar o MyApps no marcador do Navegador Gerenciado.

- **Novos ícones para o Navegador Gerenciado e o Portal da Empresa**

  O Navegador Gerenciado está recebendo ícones atualizados para as versões do Android e iOS do aplicativo. O novo ícone conterá o emblema Intune atualizado para torná-lo mais consistente com outros aplicativos no Enterprise Mobility + Security (EM+S). Você pode ver o ícone novo para o Navegador Gerenciado nas [novidades na página de IU do aplicativo Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

  O Portal da Empresa também está recebendo ícones atualizados para as versões do Android, iOS e Windows do aplicativo para aprimorar a consistência com outros aplicativos EM+S. Esses ícones serão lançados gradualmente nas plataformas de abril até o final de maio.

- **Indicador de progresso de entrada no Portal da Empresa para Android**

  Uma atualização para o aplicativo para Android do Portal da Empresa mostra um indicador de progresso de entrada quando o usuário inicia ou retoma o aplicativo. O indicador avança em novos status, começando com "Conectando …", então, "Entrando..." e "Verificando os requisitos de segurança..." antes de permitir que o usuário acesse o aplicativo. Você pode ver as novas telas do aplicativo de Portal da Empresa para Android nas [novidades na página de IU do aplicativo Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Bloquear os aplicativos de acessarem o SharePoint Online**

  Agora, você pode criar uma política de acesso condicional com base em aplicativos para impedir que os aplicativos, que não têm políticas de proteção do aplicativo aplicadas, acessem o [SharePoint Online](https://docs.microsoft.com/intune-classic/deploy-use/mam-ca-for-sharepoint-online). No cenário de acesso condicional com base em aplicativos, você pode especificar os aplicativos que deseja ter acesso ao SharePoint Online usando o portal do Azure.

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Novidades no Configuration Manager Technical Preview 1704

- **Configurar aplicativos Android com as políticas de configuração de aplicativo**

  Você pode usar políticas de configuração de aplicativo no System Center Configuration Manager (Configuration Manager) para distribuir as configurações pré-definidas quando um usuário executa um aplicativo em dispositivos Android for Work. As políticas de configuração de aplicativo Android só estão disponíveis em dispositivos com Android for Work e aplicam-se a aplicativos aprovados da loja Play for Work. Para saber mais sobre como experimentar este recurso, confira [Configurar aplicativos Android com as políticas de configuração de aplicativo](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies).

## <a name="march-2017"></a>Março de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Nova experiência do usuário para o aplicativo Portal da Empresa para Android**

  O aplicativo Portal da Empresa para Android tem uma aparência mais moderna para sua interface do usuário. As atualizações importantes são:

  - Cores: os cabeçalhos da guia Portal da Empresa estão coloridos na identidade visual definida pela TI.
  - Aplicativos: na guia **Aplicativos**, os botões **Aplicativos em destaque** e **Todos os aplicativos** foram atualizados.
  - Pesquisa: na guia **Aplicativos**, o botão **Pesquisa** é um botão de ação flutuante.
  - Aplicativos de navegação: a exibição **Todos os aplicativos** mostra uma exibição com as guias **Em destaque**, **Todos** e **Categorias** para facilitar a navegação.
  - Suporte: as guias **Meus dispositivos** e **Entrar em contato com a TI** foram atualizadas para melhorar a legibilidade.

  Para obter mais informações sobre essas alterações, confira [Atualizações da interface do usuário para aplicativos de usuário final do Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Assinatura de Script para o Portal de Empresa do Windows 10**

  Se precisar baixar e carregar o aplicativo Portal da Empresa do Windows 10, agora você poderá usar um script para simplificar e facilitar o processo de autenticação de aplicativo para sua organização.  Para baixar o script e suas instruções de uso, consulte [Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/win10cpscript) (Script de assinatura do Microsoft Intune para o Portal da Empresa do Windows 10) na Galeria do TechNet. Para obter mais informações sobre este comunicado, confira [Atualizar seu aplicativo Portal da Empresa do Windows 10](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) no blog da equipe de suporte do Intune.

- **Suporte aprimorado para os usuários Android na China**

  Devido à ausência da Google Play Store na China, os dispositivos Android devem obter aplicativos de marketplaces chineses. O Portal da Empresa dará suporte a este fluxo de trabalho, redirecionando os usuários Android na China para baixarem os aplicativos Portal da Empresa e Outlook de lojas de aplicativos locais. Isso melhorará a experiência do usuário quando as políticas de acesso condicional estiverem habilitadas para gerenciamento de dispositivos e aplicativos móveis. Os aplicativos Portal da Empresa e Outlook para Android estão disponíveis nas seguintes lojas de aplicativos chinesas:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

- **Verifique se seus aplicativos do Portal da Empresa estão atualizados**

  Em dezembro de 2016, lançamos uma atualização que habilitou a imposição da MFA (Autenticação Multifator) em um grupo de usuários quando eles registram um dispositivo iOS, Android, Windows 8.1+ ou Windows Phone 8.1+. Este recurso não funcionará sem determinadas versões de linha de base do aplicativo Portal da Empresa para Android (v5.0.3419.0+) e iOS (v2.1.17+).

  Os recursos de gerenciamento do Intune estão melhorando continuamente e muitas melhorias têm atualizações coordenadas para os aplicativos do Portal da Empresa em todas as plataformas com suporte. Como resultado, é recomendável que você mantenha as versões mais recentes dos aplicativos do Portal da Empresa instaladas nos dispositivos para aproveitar os aprimoramentos do Intune e obter a melhor experiência de usuário.

  >[!Tip]
  > Peça aos seus usuários para definirem seus dispositivos para atualizar automaticamente os aplicativos da loja de aplicativos apropriada. Se tiver disponibilizado o aplicativo Portal da Empresa Android em um compartilhamento de rede, você poderá baixar a versão mais recente do [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=49140).

- **O Microsoft Teams agora está habilitado para MAM no iOS e no Android**

  Os aplicativos do Microsoft Teams para iOS e Android agora estão habilitados com recursos de MAM (gerenciamento de aplicativo móvel) do Intune, para que você possa capacitar as equipes para trabalharem livremente entre dispositivos, garantindo que as conversas e dados corporativos estejam protegidos em cada turno. Para obter mais detalhes, consulte [o comunicado sobre o Microsoft Teams](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) no blog Enterprise Mobility + Security.

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Novidades no Configuration Manager Technical Preview 1703

- **Suporte adicional para cenários do Apple Volume Purchase Program**

   A partir do Technical Preview 1703, agora você tem suporte para os seguintes cenários do Volume Purchase Program (VPP):

   - Licenciamento do dispositivo – Aplicativos com suporte para o licenciamento do dispositivo e que são implantados em coleções de dispositivos agora necessitam apenas de uma licença por dispositivo.  Anteriormente, você deveria usar uma licença para cada usuário em um dispositivo. Para mais informações, confira [Implantar aplicativos iOS adquiridos por volume em coleções de dispositivos](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections).
   - Uso de vários tokens de VPP para um locatário híbrido único com ambos os tokens usados para gerenciar aplicativos VPP.
   - Uso de tokens educacionais de VPP com a capacidade de distinguir entre os tokens corporativos e educacionais.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)

Os seguintes recursos que estavam anteriormente disponíveis nas versões do Configuration Manager Technical Preview agora estão disponíveis em implantações híbridas com o Intune e a versão 1702 do Configuration Manager (branch atual).

- [Suporte do Android for Work](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [Configurações de conformidade de aplicativos fora de conformidade](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [Criação e distribuição de certificado PFX e suporte a S/MIME](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-to-certificate-profiles)
- [Android and iOS versions are no longer targetable in creation wizards for hybrid MDM (As versões do Android e iOS não precisam mais ser indicadas nos assistentes de criação do MDM híbrido)](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

Os seguintes recursos híbridos adicionais também estão incluídos na versão 1702 do Configuration Manager (ramificação atual):

- **Suporte aprimorado para o Apple Volume Purchase Program (VPP)**

  - Agora você pode implantar aplicativos licenciados para dispositivos, bem como os usuários. Dependendo da capacidade dos aplicativos para dar suporte ao licenciamento de dispositivos, uma licença apropriada será solicitada quando você implantá-la, da seguinte maneira:

    | Versão do Configuration Manager | O aplicativo dá suporte ao licenciamento de dispositivos? | Tipo de coleção de implantação | Licença solicitada |
    |-|-|-|-|
    |Anterior à versão 1702|Sim|usuário|Licença de usuário|
    |Anterior à versão 1702|Não|usuário|Licença de usuário|
    |Anterior à versão 1702|Sim|Dispositivo|Licença de usuário|
    |Anterior à versão 1702|Não|Dispositivo|Licença de usuário|
    |Versão 1702 e posterior|Sim|usuário|Licença de usuário|
    |Versão 1702 e posterior|Não|usuário|Licença de usuário|
    |Versão 1702 e posterior|Sim|Dispositivo|Licença de dispositivo|
    |Versão 1702 e posterior|Não|Dispositivo|Licença de usuário|

  - Agora você também pode implantar e controlar aplicativos que você adquiriu do Volume Purchase Program for Education do iOS.

  - Agora você pode associar vários tokens de programa de compra por volume da Apple ao seu Configuration Manager.

  Para saber mais sobre aplicativos do iOS adquiridos por volume, veja [Gerenciar aplicativos iOS adquiridos por volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

- **Suporte para aplicativos de linha de negócios na Microsoft Store para Empresas**

  Agora você pode sincronizar aplicativos personalizados de linha de negócios da Microsoft Store para Empresas.

- **Novas ferramentas de monitoramento de defesa contra ameaças móveis**

    Você agora tem novas maneiras de monitorar o status de conformidade com seu provedor de serviços de defesa contra ameaças móveis.

    Para saber mais, veja [Como monitorar a conformidade com defesa contra ameaças móveis](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).

## <a name="february-2017"></a>Fevereiro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Modernização do site Portal da Empresa**

  O site Portal da Empresa dá suporte a aplicativos destinados a usuários que não têm dispositivos gerenciados. O site se alinha com outros produtos e serviços da Microsoft, usando um novo esquema de cores contrastantes, ilustrações dinâmicas e um "menu de hambúrguer", que contém detalhes de contato de suporte técnico e informações sobre os dispositivos gerenciados existentes. A página inicial é reorganizada para enfatizar os aplicativos que estão disponíveis para usuários, com carrosséis para aplicativos Em Destaque e Atualizados Recentemente. Você pode localizar imagens antes e depois disponíveis na página [Atualizações da interface do usuário](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Novo endereço de servidor MDM para dispositivos Windows**

  O endereço do servidor MDM para o registro de dispositivos do Windows e do Windows Phone foi alterado de manage.microsoft.com para enrollment.manage.microsoft.com. Notifique o usuário para que ele use enrollment.manage.microsoft.com como o endereço do servidor MDM caso solicitado durante o registro de um dispositivo Windows ou Windows Phone. Essa atualização também requer que qualquer CNAME no DNS que redirecione EnterpriseEnrollment.contoso.com para manage.microsoft.com seja substituído por um CNAME no DNS que redirecione EnterpriseEnrollment.contoso.com para EnterpriseEnrollment-s.manage.microsoft.com. Para obter informações adicionais sobre essa alteração, acesse http://aka.ms/intuneenrollsvrchange.

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Novidades no Configuration Manager Technical Preview 1702

- **Suporte do Android for Work**

  Agora você pode gerenciar dispositivos Android usando o Android for Work em ambientes de MDM híbridos com o Configuration Manager Technical Preview 1702. Os dispositivos Android com suporte agora podem ser registrados como dispositivos Android for Work, o que cria um perfil de trabalho no dispositivo no qual os aplicativos aprovados na Play for Work podem ser implantados. Você também pode configurar e implantar itens de configuração, políticas de conformidade e perfis de acesso aos recursos para esses dispositivos. Para saber mais, veja [Suporte do Android for Work](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support).

- **Configurações de conformidade de aplicativos fora de conformidade**

  Agora você pode criar regras de aplicativos fora de conformidade para aplicativos Android e iOS nas políticas de conformidade. Se os dispositivos tiverem os aplicativos especificados instalados, eles serão marcados como "em não conformidade" e perderão o acesso aos recursos da empresa de acordo com as políticas de acesso condicional em vigor. Para saber mais, confira [Aprimoramentos na política de conformidade de dispositivo de acesso condicional](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements).

- **Criação e distribuição de certificado PFX e suporte a S/MIME**

  Agora você pode criar e implantar certificados PFX para usuários em um ambiente híbrido. Esse certificado pode então ser usado para criptografia e descriptografia de email S/MIME pelos dispositivos que o usuário registrou. Para saber mais, veja [Criar certificados PFX com suporte a S MIME](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support).

- **Suporte para parâmetros de configuração adicionais do iOS**
   
    Agora você tem 42 configurações adicionais do iOS que pode configurar como parte de um item de configuração. A maioria das configurações (35 ao todo) foi adicionada para dispositivos iOS supervisionados. Para saber mais, confira [Novas configurações de conformidade para dispositivos iOS](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices).

## <a name="january-2017"></a>Janeiro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Suporte do Android 7.1.1**

  O Intune agora dá suporte total e gerencia o Android 7.1.1.

- **Resolver o problema em que dispositivos iOS estão inativos ou o console do administrador não pode se comunicar com eles**

  Quando os dispositivos dos usuários perdem contato com o Intune, você pode fornecer novas etapas de solução de problemas para ajudá-los a recuperar o acesso aos recursos da empresa. Veja [Dispositivos estão inativos ou o console do administrador não pode se comunicar com eles](https://docs.microsoft.com/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Novo no Configuration Manager Technical Preview 1701

- **Android and iOS versions are no longer targetable in creation wizards for hybrid MDM (As versões do Android e iOS não precisam mais ser indicadas nos assistentes de criação do MDM híbrido)**

  A partir do Technical Preview 1701 para MDM (gerenciamento de dispositivo móvel) híbrido, você não precisa mais indicar versões específicas do Android e do iOS ao criar novas políticas e perfis de dispositivos gerenciados pelo Intune. Com essa alteração, as implantações híbridas podem fornecer suporte com mais rapidez para novas versões do Android e do iOS sem precisar de uma nova versão ou extensão do Configuration Manager. Para obter mais informações, consulte [Android and iOS versions are no longer targetable in creation wizards for hybrid MDM (As versões do Android e iOS não precisam mais ser indicadas nos assistentes de criação do MDM híbrido)](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).


## <a name="notices"></a>Avisos

### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode"></a>Portal da Empresa para Windows 8.1 e Windows Phone 8.1 mudando para o modo de manutenção 
<!--1428681-->
*6 de outubro de 2017*   
 
A partir de outubro de 2017, os aplicativos Portal da Empresa para Windows 8.1 e Windows Phone 8.1 mudarão para o modo de manutenção. Isso significa que os aplicativos e cenários existentes, como registro e conformidade, continuarão recebendo suporte nessas plataformas. Esses aplicativos continuarão disponíveis para download por meio de canais de lançamento existentes, como o Microsoft Store. 

Uma vez no modo de manutenção, esses aplicativos só receberão atualizações críticas de segurança. Nenhuma atualização ou recurso adicional será lançada para esses aplicativos. Para os novos recursos, recomendamos que você atualize os dispositivos para Windows 10 ou Windows 10 Mobile. 

### <a name="end-of-support-for-ios-80"></a>Fim do suporte para iOS 8.0 
<!---1164477--->
Os aplicativos gerenciados e o aplicativo Portal da Empresa para iOS exigirão o iOS 9.0 e superior para acessar os recursos da empresa. Os dispositivos que não forem atualizados até setembro não poderão mais acessar o Portal da Empresa ou esses aplicativos. 

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>Lembrete de suporte à plataforma: o suporte base do Windows Phone 8.1 terminou em 11 de julho de 2017
<!-- 1327781 -->
*11 de julho de 2017*

O suporte base à plataforma Windows Phone 8.1 chegou ao fim. O suporte a computadores Windows 8.1 não foi afetado.

Não há nenhum impacto imediato para os dispositivos Windows Phone 8.1 gerenciados pelo serviço Intune, incluindo aqueles registrados em MDM híbrido. Os dispositivos registrados continuarão a funcionar e todas as políticas, as configurações e os aplicativos continuarão a funcionar conforme o esperado. Observe que não existem melhorias destinadas à plataforma Windows Phone 8.1 no serviço Intune nem ao aplicativo Portal da Empresa do Windows Phone 8.1.

Recomendamos atualizar os dispositivos qualificados do Windows Phone 8.1 para o Windows 10 Mobile assim que possível.  

### <a name="end-of-support-for-android-43-and-lower"></a>Fim do suporte para Android 4.3 e inferior
<!---1171127--->
*6 de julho de 2017*

Os aplicativos gerenciados e o aplicativo Portal da Empresa para Android exigirão o Android 4.4 e superior para acessar os recursos da empresa. Os dispositivos que não forem atualizados até o início de outubro não poderão mais acessar o Portal da Empresa ou esses aplicativos. Até dezembro, todos os dispositivos inscritos serão desativados, resultando na perda do acesso aos recursos da empresa. Se você estiver usando políticas de proteção do aplicativo sem MDM, os aplicativos não receberão atualizações e reduzirão a qualidade da sua experiência ao longo do tempo.


### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 e System Center 2012 R2 Configuration Manager (RTM): o suporte para o gerenciamento de dispositivo móvel híbrido terma em 10 de abril de 2017
*11 de janeiro de 2017*

O suporte para o System Center 2012 Configuration Manager SP1 e o System Center 2012 R2 Configuration Manager RTM terminou em 12 julho de 2016. Consequentemente, o suporte a essas versões em conexão com o serviço Microsoft Intune para MDM híbrido termina em 10 de abril de 2017. Após essa data, o MDM híbrido deixará de funcionar com essas versões. Os dispositivos gerenciados se tornarão essencialmente não gerenciados, pois o Intune Connector não se conectará mais ao serviço do Intune. Os dados do Configuration Manager (como aplicativos e políticas) não fluirão até o Intune, e os dados de dispositivo gerenciados não fluirão para o Configuration Manager até que uma atualização ocorra.

Se você estiver executando uma implantação híbrida com o Configuration Manager 2012 SP1 ou R2 RTM, recomendamos que antes de 10 de abril de 2017 você atualize para o Configuration Manager (ramificação atual) ou para o service pack mais recente com suporte do Configuration Manager 2012 (R2 SP1 ou SP2) para evitar a interrupção do serviço.

Recursos adicionais:
-   [Atualizar para o System Center Configuration Manager (ramificação atual)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-   [Planejar a atualização para o System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-   [Planejar a atualização para o System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Upload do Portal da Empresa do Windows Phone 8 preterido
*25 de outubro de 2016*

A capacidade de carregar um aplicativo do Portal da Empresa assinado foi removida do console do Configuration Manager, uma vez que o suporte do Intune está sendo preterido para Windows 8, Windows Phone 8 e Windows RT e o suporte para o Portal da Empresa para Windows Phone 8 será encerrado em novembro.  Os dispositivos Windows 8, Windows Phone 8 e Windows RT já registrados continuarão a ter suporte, mas o registro de dispositivos adicionais com essas plataformas não terá suporte.


### <a name="see-also"></a>Consulte também

- [Recursos do MDM híbrido anteriores](whats-new-hybrid-archive.md)
- [Novidades do MDM no System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)
