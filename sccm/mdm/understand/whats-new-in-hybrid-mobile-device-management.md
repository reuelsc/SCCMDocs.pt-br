---
title: Novidades no MDM híbrido
titleSuffix: Configuration Manager
description: Saiba mais sobre os novos recursos de gerenciamento de dispositivo móvel disponíveis para implantações híbridas com o Configuration Manager e o Intune.
ms.custom: na
ms.date: 04/02/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a47569ee56931d76a41e5f14ed56f8276d264fb
ms.sourcegitcommit: e4ca9fb1fad2caaf61bb46e0a12f4d6b96f15513
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-configuration-manager-and-microsoft-intune"></a>Novidades no gerenciamento de dispositivo móvel híbrido com o Configuration Manager e o Microsoft Intune

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



## <a name="april-2018"></a>Abril de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

#### <a name="updated-help-experience-on-company-portal-app-for-android"></a>Experiência de Ajuda atualizada no aplicativo Portal da Empresa para Android 
<!--1631531-->
Atualizamos a experiência da Ajuda no aplicativo Portal da Empresa para Android para alinhar às práticas recomendadas para a plataforma Android. Agora, quando os usuários encontram um problema no aplicativo, eles podem clicar em **Menu** > **Ajuda** e:
- Carregar os logs de diagnóstico para a Microsoft.
- Enviar um email que descreva o problema e a ID do incidente para uma pessoa de suporte da empresa.


#### <a name="update-where-to-configure-your-app-protection-policies"></a>Atualizar o local em que você configura as políticas de proteção do aplicativo 
<!--2144597-->
No portal do Azure dentro do serviço do Microsoft Intune, você será temporariamente direcionado da folha de serviço da **Proteção de Aplicativo do Intune** para a folha **Aplicativo Móvel**. Observe que todas as suas políticas de proteção de aplicativo já estão na folha de **Aplicativo Móvel** do Intune, em configuração do aplicativo. Em vez de acessar a Proteção de Aplicativo do Intune, basta acessar o Intune. Em abril de 2018, interromperemos o redirecionamento e removeremos totalmente a folha de serviço da **Proteção de Aplicativo do Intune**, para que haja apenas um local para as políticas de proteção de aplicativos no Intune. 

**Como isso me afeta?** Essa alteração afeta os clientes do Intune autônomo e os clientes do híbrido (Intune com o Configuration Manager). Essa integração ajudará a simplificar a administração do gerenciamento da nuvem.

**O que preciso fazer para me preparar para essa alteração?** Marque o **Intune** como um favorito em vez da folha de serviço da **Proteção de Aplicativo do Intune** e familiarize-se com o fluxo de trabalho da Política de proteção de aplicativo, na folha Aplicativo **Móvel** do Intune. Você será redirecionado por um breve período de tempo e, em seguida, a folha da **Proteção de Aplicativo** será removida. Lembre-se de que todas as políticas de proteção de aplicativos já estão no Intune e você pode modificar qualquer política de acesso condicional. Para saber mais sobre como modificar políticas de acesso condicional, confira [Acesso condicional no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Para mais informações, confira [O que são políticas de proteção de aplicativo?](/intune/app-protection-policy) 




#### <a name="user-experience-update-for-the-company-portal-app-for-ios"></a>Atualização de experiência do usuário para o aplicativo Portal da Empresa para iOS 
<!--1412866-->
Lançamos uma atualização principal da experiência do usuário para o aplicativo Portal da Empresa para iOS. A atualização apresenta um novo design de visual completo que inclui aparência e modernizada. Mantivemos a funcionalidade do aplicativo, mas aumentamos sua usabilidade e a acessibilidade.  

Você também verá:
- Suporte para iPhone X.
- Inicialização do aplicativo e carregamento de respostas mais rápidos, para economizar tempo dos usuários.
- Barras de progresso adicionais para fornecer aos usuários as informações de status mais atualizadas.
- Melhorias na forma de carregar os logs aos usuários para ser mais fácil relatar se algo der errado.  

Para ver a aparência atualizada, acesse [Novidades na interface do usuário do aplicativo](/intune/whats-new-app-ui).



## <a name="march-2018"></a>Março de 2018

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

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
  A partir desta versão, é preciso configurar e gerenciar suas políticas de Acesso Condicional no [Portal do Azure](https://portal.azure.com) do **Acesso Condicional** do **Azure Active Directory** > . Para sua conveniência, você também pode acessar esta folha do Intune no Portal do Azure no **Acesso Condicional** do **Intune** > .
  <!-- 1737088 1634311 --> 

- **Atualizações para emails de conformidade**    
  Quando um email é enviado para relatar um dispositivo incompatível, os detalhes sobre o dispositivo não compatível são incluídos na mensagem. 
  <!--1637547 -->

- **Nova funcionalidade para a ação "Resolver" para dispositivos Android**    
  O aplicativo Portal da Empresa para Android está expandindo a ação "Resolver" para **Atualizar configurações do dispositivo** a fim de resolver [problemas de criptografia de dispositivo](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android).
  <!--1583480-->

- **Bloqueio remoto disponível no aplicativo de Portal da Empresa para Windows 10**    
  Agora, os usuários finais podem bloquear remotamente seus dispositivos do aplicativo do Portal da Empresa para Windows 10. Essa ação não será exibida para o dispositivo local que ele estiver usando ativamente.
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
  O Portal da Empresa do Intune no macOS está com a experiência atualizada. Ela foi otimizada para exibir com clareza todas as notificações de conformidade e informações de que seu usuário precisa para todos os dispositivos que eles registraram. E, quando o Portal da Empresa do Intune tiver sido implantado em um dispositivo, a Atualização Automática da Microsoft para macOS fornecerá atualizações para ele. Baixe o novo Portal da Empresa do Intune para macOS fazendo o logon no site do Portal da Empresa do Intune a partir de um dispositivo macOS.
  <!--1541700-->   

- **Agora o Microsoft Planner faz parte da lista do MAM (gerenciamento de aplicativo móvel) de aplicativos aprovados**    
  Agora o aplicativo Microsoft Planner para iOS e Android faz parte dos aplicativos aprovados para o MAM (gerenciamento de aplicativo móvel). Configure o aplicativo por meio da folha de Proteção de Aplicativo do Intune no Portal do Azure para todos os locatários. Para obter detalhes, confira [Lista MAM de aplicativos aprovados](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).
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
  - **Desabilitar sincronização de contato**: impede que o aplicativo salve dados no aplicativo Contatos nativo do dispositivo.
  - **Desabilitar impressão**: impede que o aplicativo imprima dados corporativos ou de estudante.
  <!-- 1324760 -->    

  Veja [proteger aplicativos usando políticas de proteção de aplicativos no Configuration Manager](/sccm/mdm/deploy-use/protect-apps-using-mam-policies) para testar as novas configurações de política de proteção do aplicativo.

- **Suporte a dispositivos com Windows 10 ARM64**     
  Os cenários híbridos de MDM (gerenciamento de dispositivo móvel) têm suporte em dispositivos ARM64 executando o Windows 10 quando esses dispositivos ficarem disponíveis. Para obter mais detalhes, confira [Suporte a dispositivos Windows 10 ARM64](/sccm/core/plan-design/changes/whats-new-in-version-1710#windows-10-arm64-device-support).
  <!-- 1355000 -->    

- **Melhoria na experiência do perfil de VPN no Console do Configuration Manager**     
  Com esta versão, as páginas de assistente e de propriedades do perfil de VPN foram atualizadas para exibir as configurações apropriadas para a plataforma selecionada. Essa funcionalidade estava disponível anteriormente no Configuration Manager Technical Preview 1709. Agora, ele está disponível em implantações híbridas com o Intune e com a versão 1710 do Configuration Manager (Branch Atual). Para saber mais, confira [Melhoria da experiência do perfil de VPN no Console do Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1710#improved-vpn-profile-experience-in-configuration-manager-console).
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
    - Se os usuários finais tiverem atingido o número máximo de dispositivos permitido, serão levados ao [Portal do Azure Active Directory](https://account.activedirectory.windowsazure.com/r/#/profile) para remover um dispositivo.
    - Os usuários finais recebem etapas a serem seguidas para ajudá-los a [corrigir erros de ativação em dispositivos Samsung Knox](https://go.microsoft.com/fwlink/?linkid=859718) ou a [desligar o modo de economia de energia](https://docs.microsoft.com/intune-user-help/power-saving-mode-android). Se nenhuma dessas soluções resolver o problema, forneceremos uma explicação de como [enviar logs para a Microsoft](https://docs.microsoft.com/intune-user-help/send-logs-to-microsoft-android).
  <!-- 1573324, 1573150, 1558616, 1564878 -->      

- **Indicador de progresso da instalação do dispositivo no Portal da Empresa para Android**     
  O aplicativo do Portal da Empresa para Android mostra um indicador de progresso da instalação do dispositivo quando um usuário está registrando seu dispositivo. O indicador mostra novos status, começando com "Configurando seu dispositivo...", em seguida, "Registrando seu dispositivo...", "Concluindo o registro do seu dispositivo..." e "Concluindo a instalação do seu dispositivo...".  
  <!--1565657-->    

- **Suporte a autenticação baseada em certificado no Portal da Empresa para iOS**    
  Adicionamos suporte para CBA (autenticação baseada em certificado) no aplicativo do Portal da Empresa para iOS. Usuários com CBA inserem seu nome de usuário, depois, tocam no link "Entrar com um certificado". CBA já é compatível com os aplicativos Portal da Empresa para Android e Windows. Saiba mais na página para [entrar no aplicativo Portal da Empresa](https://docs.microsoft.com/intune-user-help/sign-in-to-the-company-portal).
  <!--1029830-->   

- **Aprimoramentos no fluxo de trabalho de configuração do dispositivo no Portal da Empresa**     
  Melhoramos o fluxo de trabalho de configuração de dispositivo no aplicativo Portal da Empresa para Android. A linguagem é mais fácil de usar e mais específica para sua empresa. Combinamos as telas sempre que possível. Veja esses aprimoramentos na página [Novidades na interface do usuário do aplicativo](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-october-2-2017).
  <!--1490692-->     

- **Orientação aprimorada para a solicitação de acesso aos contatos em dispositivos Android**     
  O aplicativo Portal da Empresa para Android geralmente exige que o usuário final aceite a permissão de Contatos. Se um usuário final recusar esse acesso, ele verá uma notificação no aplicativo alertando-o para concedê-lo para acesso condicional. 
  <!--1484985-->     

- **Correção da inicialização segura para Android**     
  Os usuários finais com dispositivos Android podem tocar no motivo da não conformidade no aplicativo Portal da Empresa. Quando possível, essa ação os levará diretamente para a localização correta no aplicativo de configurações para corrigir o problema. 
  <!--1490712-->    

- **Notificações por push adicionais para usuários finais no aplicativo Portal da Empresa para Android Oreo**    
  Os usuários finais veem notificações adicionais para indicar quando o aplicativo Portal da Empresa para Android Oreo está executando tarefas em segundo plano, por exemplo, recuperando as políticas do serviço Intune. As notificações aumentam a transparência para os usuários finais, informando sobre quando o Portal da Empresa estiver executando tarefas administrativas em seu dispositivo. Esse aprimoramento faz parte da [otimização geral da interface de usuário do Portal da Empresa](https://blogs.technet.microsoft.com/intunesupport/2017/08/21/android-8-0-o-behaviour-changes-and-microsoft-intune) para o aplicativo Portal da Empresa para Android Oreo. 
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
  O aplicativo Portal da Empresa tenta registrar apenas os dispositivos Samsung Knox com suporte. Para evitar erros de ativação do KNOX que impedem o registro do MDM, a tentativa do registro do dispositivo só ocorrerá se o dispositivo for exibido na [lista de dispositivos publicada pela Samsung](https://www.samsungknox.com/knox-supported-devices/knox-workspace). Os dispositivos Samsung podem ter números de modelo que oferecem suporte a KNOX, enquanto outros não. Verifique a compatibilidade do Knox com o revendedor de seu dispositivo antes de comprar e implantar. Encontre a lista completa de dispositivos verificados nas [configurações de política do Android e Samsung KNOX Standard](https://docs.microsoft.com/intune-classic/deploy-use/android-policy-settings-in-microsoft-intune#supported-samsung-knox-standard-devices).
  <!-- 1490695 -->     

- **Fim do suporte para Android 4.3 e inferior**     
  Um aviso foi adicionado para o fim do suporte para Android 4.3 e inferior. Para obter mais detalhes, veja [Avisos](#notices).
  <!--1171126, 1326920 -->     

- **Informar aos usuários finais quais informações do dispositivo podem ser vistas em dispositivos registrados**     
  Estamos adicionando o **Tipo de Propriedade** à tela de Detalhes do Dispositivo em todos os aplicativos Portal da Empresa. Essas informações permitirão que os usuários obtenham mais informações sobre privacidade diretamente do artigo [Quais informações sua empresa pode ver?](https://docs.microsoft.com/intune-user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune). Esse aprimoramento será implantado em breve em todos os aplicativos do Portal da Empresa. Anunciamos essa funcionalidade para iOS em [setembro](https://docs.microsoft.com/intune/whats-new#week-of-september-11-2017). 
  <!--1165314-->     



## <a name="september-2017"></a>Setembro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune     

- **Ação de atualização adicionada ao aplicativo Portal da Empresa para Windows 10**    
    O aplicativo Portal da Empresa para Windows 10 permite que os usuários atualizem os dados no aplicativo deslizando para atualizar ou, em áreas de trabalho, pressionando F5.
    <!-- 1132468 -->     

- **Mostrar os usuários finais quais informações do dispositivo podem ser vistas para o iOS**   
    Adicionamos **Tipo de Propriedade** à tela de detalhes do dispositivo no aplicativo Portal da Empresa para iOS. Essas informações permitem que os usuários obtenham mais informações sobre privacidade diretamente dos documentos do usuário final do Intune. Eles também pode encontrar essas informações na tela Sobre. 
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



## <a name="july-2017"></a>Julho de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Avisos de fim de suporte adicionados para Android e Windows Phone**    
    Novos avisos foram adicionados para o fim de suporte das versões Android e Windows Phone. Para obter mais detalhes, veja [Avisos](#notices).


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)

As funcionalidades a seguir estavam disponíveis em versões Technical Preview do Configuration Manager. Agora, essas funcionalidades estão disponíveis em implantações híbridas com o Intune e com a versão 1706 do Configuration Manager (branch atual).

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
  A partir do Configuration Manager versão 1610, você pode alterar sua autoridade MDM sem precisar entrar em contato com o Suporte da Microsoft. Você também não precisa cancelar o registro e registrar novamente os dispositivos gerenciados existentes. Para obter detalhes, veja [Alterar sua autoridade de MDM](/sccm/mdm/deploy-use/change-mdm-authority).

- **Integração gerenciada de proxy do navegador e aplicativo**    
  O Intune Managed Browser agora pode ser integrado ao serviço de Proxy de Aplicativo do Azure AD para permitir que os usuários acessem sites internos, mesmo quando estão trabalhando remotamente. Os usuários do navegador inserem a URL normalmente e o Managed Browser encaminha a solicitação por meio do gateway Web do proxy de aplicativo. Para saber mais, veja [Gerenciar o acesso à Internet usando políticas no navegador gerenciado](https://docs.microsoft.com/intune/app-configuration-managed-browser).

- **Agora, o aplicativo Portal da Empresa para Android tem uma nova experiência do usuário final para as Políticas de Proteção do Aplicativo**  
  Com base nos comentários do cliente, modificamos o aplicativo Portal da Empresa para Android mostrar um botão **Acessar Conteúdo da Empresa**. A intenção é impedir que os usuários finais passem desnecessariamente pelo processo de inscrição quando eles só precisam acessar os aplicativos que dão suporte a Políticas de Proteção do Aplicativo, um recurso de gerenciamento de aplicativo móvel do Intune. Veja essas alterações na página [Novidades na interface do usuário do aplicativo](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Nova ação de menu para remover facilmente o Portal da Empresa**  
  Com base nos comentários do usuário, o aplicativo Portal da Empresa para Android adicionou uma nova ação de menu para iniciar a remoção do Portal da Empresa de seu dispositivo. Esta ação remove o dispositivo do gerenciamento do Intune para que o aplicativo possa ser removido do dispositivo pelo usuário. Veja essas alterações na página [Novidades na interface do usuário do aplicativo](https://docs.microsoft.com/intune/whats-new-app-ui) e na [documentação de usuário final do Android](https://docs.microsoft.com/intune-user-help/unenroll-your-device-from-intune-android).

- **Aprimoramentos na sincronização de aplicativo com a Atualização do Windows 10 para Criadores**  
  O aplicativo Portal da Empresa para Windows 10 iniciará automaticamente uma sincronização para solicitações de instalação de aplicativo para dispositivos com a Atualização do Windows 10 para Criadores (versão 1703). Esse comportamento reduz o problema de atraso das instalações de aplicativos durante o estado de "Sincronização Pendente". Além disso, os usuários poderão iniciar manualmente uma sincronização de dentro do aplicativo. Veja essas alterações na página [Novidades na interface do usuário do aplicativo](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Nova experiência orientada para o Portal da Empresa do Windows 10**  
  O aplicativo do Portal da Empresa para Windows 10 inclui uma experiência passo a passo interativa do Intune para dispositivos que não foram identificados nem registrados. A nova experiência fornece instruções passo a passo que guiam o usuário pelo processo de inscrição no Azure Active Directory (exigido para funcionalidades de Acesso Condicional) e inscrição de MDM (exigido para as funcionalidades de gerenciamento de dispositivo). A experiência guiada está acessível na home page do Portal da Empresa. Se os usuários não completarem o registro e a inscrição, poderão continuar usando o aplicativo, mas enfrentarão uma funcionalidade limitada.

  Esta atualização só fica visível em dispositivos que executam a Atualização de Aniversário do Windows 10 (build 1607) ou superior. Veja essas alterações na página [Novidades na interface do usuário do aplicativo](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Aprimoramentos nos blocos de aplicativo no aplicativo Portal da Empresa para iOS**  
  Atualizamos o design dos blocos do aplicativo na home page a fim de refletir a cor de identidade visual que você definiu para o Portal da Empresa. Para saber mais, veja [Novidades na interface do usuário do aplicativo](https://docs.microsoft.com/intune/whats-new-app-ui).

- **O seletor de conta já está disponível para o aplicativo Portal da Empresa para iOS**  
  Se os usuários de dispositivos iOS usarem suas contas corporativas ou de estudante para entrar em outros aplicativos da Microsoft, poderão ver nosso seletor de conta quando entrarem no Portal da Empresa. Para saber mais, veja [Novidades na interface do usuário do aplicativo](https://docs.microsoft.com/intune/whats-new-app-ui).

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Novidades da Visualização Técnica 1706 do Configuration Manager

- **Novas definições de item de configuração do Windows**      
  Novos itens de configuração do Windows estão disponíveis para as categorias de configuração de Senha, Dispositivo, Armazenamento e Microsoft Edge. Para saber mais, confira [Novas definições de item de configuração do Windows](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings).
  <!-- 1354715 -->

- **Novas regras de política de conformidade do dispositivo**   
  Agora você pode definir novas opções de políticas de conformidade que estavam disponíveis somente no Intune autônomo. Para obter detalhes, confira [Aprimoramentos na política de conformidade de dispositivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules).

- **Restrições de inscrição do Android e iOS**       
  Os administradores podem especificar que os usuários não podem inscrever dispositivos Android ou iOS pessoais no ambiente híbrido. Essa ação permite que você limite os dispositivos inscritos a dispositivos da empresa ou iOS previamente declarados inscritos somente com o Programa de Registro de Dispositivos. Para obter detalhes, confira [Restrições de inscrição do Android e iOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions).
  <!-- 1290826 -->

- **Suporte para autoridades de certificação Entrust**      
  Agora, o Configuration Manager dá suporte a autoridades de certificação Entrust. Esse suporte permite a entrega de certificados PFX para dispositivos registrados no Microsoft Intune.    
  <!-- 1350740 -->

  Você pode configurar o Entrust como a autoridade de certificação ao adicionar a função Ponto de Registro de Certificado no Configuration Manager. Ao adicionar um novo perfil de certificado que emite os certificados PFX, você pode selecionar uma autoridade de certificação Microsoft ou Entrust.

  **Problema conhecido**: na technical preview 1706, os certificados PFX não são emitidos para autoridades de certificação da Microsoft. Esse problema não afeta os certificados PFX importados ou os perfis SCEP.

- **Suporte da Cisco (IPsec) para perfis VPN do macOS**      
  Você pode criar um perfil VPN do macOS com Cisco (IPsec) como o tipo de conexão. Para saber mais, confira [Criar perfis VPN](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).
  <!-- 1321367 -->


## <a name="april-2017"></a>Abril de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **MyApps disponível para o Navegador Gerenciado**  
  Agora, o Microsoft MyApps tem um suporte melhor dentro do Navegador Gerenciado. Os usuários do Managed Browser que não são destinados ao gerenciamento serão levados diretamente ao serviço MyApps, onde poderão acessar seus aplicativos SaaS provisionados pelo administrador. Os usuários que são destinados ao gerenciamento do Intune continuam a acessar o MyApps no indicador do Managed Browser.

- **Novos ícones para o Navegador Gerenciado e o Portal da Empresa**  
  O Navegador Gerenciado está recebendo ícones atualizados para as versões do Android e iOS do aplicativo. O novo ícone contém o emblema Intune atualizado para torná-lo mais consistente com outros aplicativos no Enterprise Mobility + Security (EM+S). Você pode ver o ícone novo para o Navegador Gerenciado nas [novidades na página de IU do aplicativo Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

  O Portal da Empresa também está recebendo ícones atualizados para as versões do Android, iOS e Windows do aplicativo para aprimorar a consistência com outros aplicativos EM+S. Esses ícones serão lançados gradualmente nas plataformas de abril até o final de maio.

- **Indicador de progresso de entrada no Portal da Empresa Android**  
  Uma atualização para o aplicativo Android do Portal da Empresa mostra um indicador de progresso de entrada quando o usuário inicia ou retoma o aplicativo. O indicador avança em novos status, começando com "Conectando …", então, "Entrando..." e "Verificando os requisitos de segurança..." antes de permitir que o usuário acesse o aplicativo. Você pode ver as novas telas do aplicativo de Portal da Empresa para Android nas [novidades na página de IU do aplicativo Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Bloquear os aplicativos de acessarem o SharePoint Online**  
  Agora, você pode criar uma política de acesso condicional com base em aplicativos para impedir que os aplicativos, que não têm políticas de proteção do aplicativo aplicadas, acessem o [SharePoint Online](https://docs.microsoft.com/intune-classic/deploy-use/mam-ca-for-sharepoint-online). No cenário de acesso condicional com base em aplicativos, você pode especificar os aplicativos que deseja ter acesso ao SharePoint Online usando o portal do Azure.

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Novidades no Configuration Manager Technical Preview 1704

- **Configurar aplicativos Android com as políticas de configuração de aplicativo**  
  Quando um usuário executa um aplicativo em dispositivos com Android for Work, use as políticas de configuração de aplicativo no Configuration Manager para distribuir as configurações pré-definidas. As políticas de configuração de aplicativo do Android estão disponíveis somente em dispositivos com Android for Work. Essas políticas se aplicam a aplicativos aprovados pela Play for Work Store. Para saber mais, confira [Configurar aplicativos Android com as políticas de configuração de aplicativo](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies).



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
  Se precisar baixar e carregar o aplicativo Portal da Empresa do Windows 10, agora você poderá usar um script para simplificar e facilitar o processo de autenticação de aplicativo para sua organização. Para baixar o script e suas instruções de uso, consulte [Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/win10cpscript) (Script de assinatura do Microsoft Intune para o Portal da Empresa do Windows 10) na Galeria do TechNet. Para obter mais informações sobre este comunicado, confira [Atualizar seu aplicativo Portal da Empresa do Windows 10](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) no blog da equipe de suporte do Intune.

- **Suporte aprimorado para os usuários Android na China**  
  Devido à ausência da Google Play Store na China, os dispositivos Android devem obter aplicativos de marketplaces chineses. O Portal da Empresa oferece suporte a esse fluxo de trabalho. Ele redireciona os usuários do Android na China para baixarem os aplicativos Portal da Empresa e Outlook de lojas de aplicativos locais. Esse comportamento melhora a experiência do usuário quando as políticas de acesso condicional estiverem habilitadas para gerenciamento de dispositivos e aplicativos móveis. Os aplicativos Portal da Empresa e Outlook para Android estão disponíveis nas seguintes lojas de aplicativos chinesas:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

- **Verifique se seus aplicativos do Portal da Empresa estão atualizados**  
  Em dezembro de 2016, lançamos uma atualização que habilitou a imposição da MFA (Autenticação Multifator) em um grupo de usuários quando eles registram um dispositivo iOS, Android, Windows 8.1+ ou Windows Phone 8.1+. Esta funcionalidade não funcionará sem determinadas versões de linha de base do aplicativo Portal da Empresa para Android (v5.0.3419.0+) e iOS (v2.1.17+).

  Os recursos de gerenciamento do Intune estão em aprimoramento contínuo. Muitos aprimoramentos têm atualizações coordenadas para os aplicativos do Portal da Empresa em todas as plataformas com suporte. Recomendamos que você mantenha as versões mais recentes dos aplicativos do Portal da Empresa instaladas nos dispositivos. Essa prática tira proveito dos aprimoramentos no Intune e oferece a melhor experiência de usuário.

  >[!Tip]
  > Peça aos seus usuários para definirem seus dispositivos para atualizar automaticamente os aplicativos da loja de aplicativos apropriada. Se tiver disponibilizado o aplicativo Portal da Empresa Android em um compartilhamento de rede, você poderá baixar a versão mais recente do [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=49140).

- **O Microsoft Teams agora está habilitado para MAM no iOS e no Android**  
  Os aplicativos do Microsoft Teams para iOS e Android estão habilitados com recursos de MAM (gerenciamento de aplicativo móvel) do Intune. Capacite suas equipes para trabalhar livremente entre dispositivos, garantindo que as conversas e os dados corporativos fiquem protegidos. Para saber mais, confira [o comunicado sobre o Microsoft Teams](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) no blog Enterprise Mobility + Security.

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Novidades no Configuration Manager Technical Preview 1703

- **Suporte adicional para cenários do Apple Volume Purchase Program**  
   A partir do Technical Preview 1703, agora você tem suporte para os seguintes cenários do Volume Purchase Program (VPP):

   - Licenciamento do dispositivo – Aplicativos com suporte para o licenciamento do dispositivo e que são implantados em coleções de dispositivos agora necessitam apenas de uma licença por dispositivo. Anteriormente, você deveria usar uma licença para cada usuário em um dispositivo. Para mais informações, confira [Implantar aplicativos iOS adquiridos por volume em coleções de dispositivos](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections).
   - Uso de vários tokens de VPP para um locatário híbrido único com ambos os tokens usados para gerenciar aplicativos VPP.
   - Uso de tokens educacionais de VPP com a capacidade de distinguir entre os tokens corporativos e educacionais.

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)

As funcionalidades a seguir estavam disponíveis em versões Technical Preview do Configuration Manager. Agora, essas funcionalidades estão disponíveis em implantações híbridas com o Intune e com a versão 1702 do Configuration Manager (branch atual).

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



## <a name="notices"></a>Avisos

### <a name="windows-company-portal-send-feedback-option-may-no-longer-work"></a>Opção de enviar comentários do Portal da Empresa do Windows pode não funcionar mais

O aplicativo de Portal da Empresa do Windows tem uma opção de ‘Enviar Comentários’ permitindo que os usuários enviem comentários sobre o aplicativo para a Microsoft. A partir de 30 de abril de 2018, essa opção continua a ter suporte apenas no aplicativo do Portal da Empresa do Windows 10 em execução no Windows 10 versão 1607 e posterior.   

#### <a name="how-does-this-affect-me"></a>Como isso me afeta?

Se você não tiver o aplicativo do Portal da Empresa do Windows instalado para usuários finais, desconsidere esta mensagem.

Se qualquer um dos seus usuários finais tiver o aplicativo de Portal da Empresa, observe que, a partir de 30 de abril, o botão ‘Enviar Comentários’ não funcionará mais para o aplicativo nos seguintes cenários:  

 - Aplicativo de Portal da Empresa do Windows 10 no Windows 10 versão 1507 e versão 1511  

 - Aplicativo do Portal da Empresa do Windows Phone 8.1  

Para dispositivos afetados, a opção ‘Enviar Comentários’ falha e não tem êxito mesmo ao tentar novamente. Para enviar comentários à Microsoft sobre experiências nessas plataformas, existem canais de comentários alternativos listados abaixo.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>O que preciso fazer para me preparar para essa alteração?

Informe aos usuários finais sobre essa alteração e atualize todas as orientações para os usuários, se necessário. 

Informe os usuários finais usando o Portal da Empresa no Windows Phone 8.1, Windows 10 versão 1507 e Windows 10 versão 1511 de que eles têm dois canais de comentários alternativos disponíveis. Eles podem:  

- Use o aplicativo Hub de Comentários no Windows 10  
- Enviar um email para WinCPfeedback@microsoft.com  

Peça aos usuários finais no Windows 10 versão 1607 ou posterior para atualizar para a versão mais recente do Portal da Empresa do Windows disponível na Microsoft Store.



### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode"></a>Portal da Empresa para Windows 8.1 e Windows Phone 8.1 mudando para o modo de manutenção 
<!--1428681-->
*6 de outubro de 2017*   
 
A partir de outubro de 2017, os aplicativos Portal da Empresa para Windows 8.1 e Windows Phone 8.1 mudaram para o modo de manutenção. Esse modo significa que os aplicativos e cenários existentes, como registro e conformidade, continuarão recebendo suporte nessas plataformas. Esses aplicativos continuam disponíveis para download por meio de canais de lançamento existentes, como o Microsoft Store. 

Uma vez no modo de manutenção, esses aplicativos só recebem atualizações críticas de segurança. Nenhuma atualização ou funcionalidade adicional será lançada para esses aplicativos. Para os novos recursos, recomendamos que você atualize os dispositivos para Windows 10 ou Windows 10 Mobile. 

### <a name="end-of-support-for-ios-80"></a>Fim do suporte para iOS 8.0 
<!---1164477--->
Os aplicativos gerenciados e o aplicativo Portal da Empresa para iOS exigem o iOS 9.0 e superior para acessar os recursos da empresa. Os dispositivos que não forem atualizados até setembro não poderão mais acessar o Portal da Empresa ou esses aplicativos. 

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>Lembrete de suporte à plataforma: o suporte base do Windows Phone 8.1 terminou em 11 de julho de 2017
<!-- 1327781 -->
*11 de julho de 2017*

O suporte base à plataforma Windows Phone 8.1 chegou ao fim. O suporte a computadores com Windows 8.1 não foi afetado.

Não há nenhum impacto imediato para os dispositivos Windows Phone 8.1 gerenciados pelo serviço Intune, incluindo os dispositivos registrados em MDM híbrido. Os dispositivos registrados continuam funcionando. Todas as políticas, configurações e aplicativos continuam a funcionar como o esperado. Observe que não há melhorias destinadas à plataforma Windows Phone 8.1 no serviço Intune nem ao aplicativo Portal da Empresa do Windows Phone 8.1.

Recomendamos atualizar os dispositivos qualificados do Windows Phone 8.1 para o Windows 10 Mobile assim que possível.  

### <a name="end-of-support-for-android-43-and-lower"></a>Fim do suporte para Android 4.3 e inferior
<!---1171127--->
*6 de julho de 2017*

Os aplicativos gerenciados e o aplicativo Portal da Empresa para Android exigem o Android 4.4 e superior para acessar os recursos da empresa. Os dispositivos que não forem atualizados até o início de outubro não poderão mais acessar o Portal da Empresa ou esses aplicativos. Até dezembro, todos os dispositivos inscritos serão desativados, resultando na perda do acesso aos recursos da empresa. Se você estiver usando políticas de proteção do aplicativo sem MDM, os aplicativos não receberão atualizações e reduzirão a qualidade da sua experiência ao longo do tempo.



## <a name="see-also"></a>Consulte também

- [Recursos e avisos do MDM híbrido anteriores](whats-new-hybrid-archive.md)
- [Novidades do MDM no System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)
