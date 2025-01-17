---
title: Arquivo morto das novidades no MDM híbrido
titleSuffix: Configuration Manager
description: Arquivo morto dos recursos de gerenciamento de dispositivo móvel anteriores disponíveis para implantações híbridas com o Intune e o System Center Configuration Manager.
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7821951461fc03598e91f22a54a49fd3b0c0cf6e
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678590"
---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>Recursos híbridos anteriores com o System Center Configuration Manager e Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo fornece detalhes sobre os recursos de MDM (gerenciamento de dispositivo móvel) anteriores disponíveis para implantações híbridas com o System Center Configuration Manager e o Microsoft Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilidade com versões do Configuration Manager  

 Cada seção deste artigo lista recursos híbridos em três categorias diferentes. Use as diretrizes a seguir para determinar a compatibilidade dos recursos em cada categoria com versões diferentes do Configuration Manager:  

|Categorias do recurso|
|-|  
|**Novo no Microsoft Intune** – em geral, todos os recursos listados nessa categoria devem funcionar com todas as versões do Configuration Manager, incluindo versões do System Center 2012 R2 Configuration Manager, uma vez que esses recursos exigem apenas o serviço Intune e não exigem funcionalidades adicionais no Configuration Manager.<br /><br /> **Novo no Configuration Manager Technical Preview** – todos os recursos listados nessa categoria funcionam apenas com a versão de Technical Preview especificada. Para testar esses recursos, você deve instalar a versão de Technical Preview especificada na descrição do recurso. Para mais informações, confira [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md).<br /><br /> **Novo no Configuration Manager (Branch Atual)** – todos os recursos listados nessa categoria funcionam apenas com a versão especificada do Configuration Manager (Branch Atual), como a versão 1511 ou 1602. Se estiver usando uma versão mais antiga do Configuration Manager para sua implantação híbrida, atualize para a versão do Configuration Manager (Branch Atual) especificada na descrição do recurso. Para mais informações, confira [Atualização para o System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|  



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

  - Cores: Cabeçalhos da guia Portal da empresa estão coloridos na identidade visual do definida por TI.
  - Aplicativos: No **aplicativos** guia, o **aplicativos em destaque** e **todos os aplicativos** botões são atualizados.
  - Pesquisa: No **aplicativos** guia, o **pesquisa** botão é um botão de ação flutuante.
  - Aplicativos de navegação: **Todos os aplicativos** modo de exibição mostra uma exibição com guias de **em destaque**, **todos os**, e **categorias** para facilitar a navegação.
  - Suporte a: **Meus dispositivos** e **contatar TI** guias são atualizadas para melhorar a legibilidade.

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
- [Criação e distribuição de certificado PFX e suporte a S/MIME](/sccm/core/plan-design/changes/whats-new-in-version-1702#mobile-device-management)
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

  O endereço do servidor MDM para o registro de dispositivos do Windows e do Windows Phone foi alterado de manage.microsoft.com para enrollment.manage.microsoft.com. Notifique o usuário para que ele use enrollment.manage.microsoft.com como o endereço do servidor MDM caso solicitado durante o registro de um dispositivo Windows ou Windows Phone. Essa atualização também requer que qualquer CNAME no DNS que redirecione EnterpriseEnrollment.contoso.com para manage.microsoft.com seja substituído por um CNAME no DNS que redirecione EnterpriseEnrollment.contoso.com para EnterpriseEnrollment-s.manage.microsoft.com. Para informações adicionais sobre essa alteração, acesse http://aka.ms/intuneenrollsvrchange.

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

  Quando os dispositivos dos usuários perdem contato com o Intune, você pode fornecer novas etapas de solução de problemas para ajudá-los a recuperar o acesso aos recursos da empresa. Veja [Dispositivos estão inativos ou o console do administrador não pode se comunicar com eles](https://docs.microsoft.com/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cant-communicate-with-them).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Novo no Configuration Manager Technical Preview 1701

- **Android and iOS versions are no longer targetable in creation wizards for hybrid MDM (As versões do Android e iOS não precisam mais ser indicadas nos assistentes de criação do MDM híbrido)**

  A partir do Technical Preview 1701 para MDM (gerenciamento de dispositivo móvel) híbrido, você não precisa mais indicar versões específicas do Android e do iOS ao criar novas políticas e perfis de dispositivos gerenciados pelo Intune. Com essa alteração, as implantações híbridas podem fornecer suporte com mais rapidez para novas versões do Android e do iOS sem precisar de uma nova versão ou extensão do Configuration Manager. Para obter mais informações, consulte [Android and iOS versions are no longer targetable in creation wizards for hybrid MDM (As versões do Android e iOS não precisam mais ser indicadas nos assistentes de criação do MDM híbrido)](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).



## <a name="december-2016"></a>Dezembro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **A MFA (Autenticação Multifator) no registro está migrando para o portal do Azure**

  Anteriormente, você tinha que ir para o console do Intune ou para o console do Configuration Manager para definir o MFA para inscrições do Intune. Com esse recurso atualizado, você faz logon para o [portal do Microsoft Azure](https://manage.windowsazure.com) usando suas credenciais do Intune e definir configurações de MFA por meio do Azure AD. Saiba mais em[Autenticação Multifator para o Microsoft Intune](https://aka.ms/mfa_ad).

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
  | Desativar/apagar (remover todos os dados)| Remover um dispositivo remoto | Remover dispositivo (local e remoto) |
  | Desativar/apagar (remover dados da empresa)| Redefinir o dispositivo | Redefinir o dispositivo|
  | Implantações de aplicativo novo ou atualizado | Instalar aplicativos de linha de negócios disponíveis | Redefinição de senha de dispositivo|
  | Bloqueio remoto| | |
  | Redefinição de senha | | |


## <a name="november-2016"></a>Novembro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Novo Portal da empresa do Microsoft Intune disponível para dispositivos Windows 10**

  A Microsoft lançou um novo [Aplicativo de Portal da empresa para dispositivos Windows 10](https://www.microsoft.com/store/apps/9wzdncrfj3pz). Esse aplicativo, que aproveita o novo formato Universal do Windows 10, fornece uma experiência de usuário atualizada que é idêntica em todos os dispositivos Windows 10 e de forma semelhante em PCs e dispositivos móveis, permitindo ao mesmo tempo a mesma funcionalidade fornecida por aplicativos anteriores do Portal da empresa.

  O novo aplicativo aproveita os recursos de plataforma como logon único (SSO) e autenticação baseada em certificado em dispositivos Windows 10. O aplicativo está disponível como uma atualização para as instalações existentes do Portal da empresa do Windows 8.1 e Portal de empresa do Windows Phone 8.1 da Windows Store. Para obter mais detalhes, acesse o [Blog da equipe de suporte do Intune](http://aka.ms/intunecp_universalapp).

  O novo aplicativo de Portal da Empresa também exibe quaisquer aplicativos Windows Store para Empresas marcados como **Disponível** no console do Configuration Manager.


### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)

Os seguintes recursos que estavam anteriormente disponíveis nas versões do Configuration Manager Technical Preview agora estão disponíveis em implantações híbridas com o Intune e a versão 1610 do Configuration Manager (branch atual).

* [Configurações adicionais e experiência aprimorada para itens de configuração](/sccm/core/plan-design/changes/whats-new-in-version-1610#new-compliance-settings-for-configuration-items)
* [Configurações adicionais para perfis de DEP](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Aplicativos pagos na Windows Store para Empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Tipos de conexão nativa para perfis de VPN do Windows 10](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
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

## <a name="october-2016"></a>Outubro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

Os recursos do Intune a seguir introduzidos em outubro de 2016 funcionam em implantações híbridas.

- **Acesso condicional para o gerenciamento de aplicativo móvel**

  Você pode restringir o acesso ao Exchange Online para que o acesso venha apenas de aplicativos que dão suporte às políticas de gerenciamento de aplicativo móvel do Intune, como o Outlook. [Esse novo recurso](/intune/deploy-use/allow-policy-managed-apps-access-to-o365) é completamente compatível com as políticas de MAM (gerenciamento de aplicativo móvel) do Intune, uma vez que você pode bloquear o acesso a clientes de email internos ou outros aplicativos que não foram configurados com as políticas de MAM do Intune. Isso garante que os usuários estão acessando os dados da sua organização com aplicativos que podem ser protegidos usando o MAM do Intune. Você pode começar no gerenciamento de aplicativo móvel do Intune por meio do Portal do Azure. Procure a nova seção de Acesso Condicional na folha “Configurações”.

- **Ferramenta de Disposição do Aplicativo do Intune para Android**

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

## <a name="september-2016"></a>Setembro de 2016

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

  Você pode obter uma exibição rápida da conformidade geral do dispositivo e os principais motivos de não conformidade usando novos gráficos no workspace Monitoramento. Para mais informações, confira [Gráficos de conformidade do Intune na TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#intune-compliance-charts).

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)

O novo recurso a seguir introduzido em setembro de 2016 está disponível para implantações híbridas com o Microsoft Intune e a versão 1606 do Configuration Manager (Branch Atual).

- **Suporte para iOS 10**

  Se você tiver perfis ou itens de configuração direcionados a todas as plataformas iOS, eles também serão enviados por push para o iOS 10. Também lançamos uma atualização para a versão 1606 do Configuration Manager que permite que você direcione perfis e itens de configuração para plataformas iOS individuais, incluindo o iOS 10. Você pode instalar a atualização com o console de administração do Configuration Manager em **Administração > Visão Geral > Serviços de Nuvem > Atualizações e Manutenção**. Você pode encontrar mais informações sobre a atualização em [http://support.microsoft.com/kb/3192616](http://support.microsoft.com/kb/3192616).

## <a name="august-2016"></a>Agosto de 2016

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

## <a name="july-2016"></a>Julho de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

Os recursos do Intune a seguir introduzidos em julho de 2016 funcionam em implantações híbridas.

- **SDK do Xamarin para aplicativos do Intune está disponível**

  O componente Xamarin do SDK de aplicativos do Intune permite que você habilite os recursos de gerenciamento de aplicativo móvel do Intune em seus aplicativos móveis para iOS e Android criados com o Xamarin. Você pode encontrar o componente na [Loja do Xamarin](https://components.xamarin.com/view/Microsoft.Intune.MAM) ou na [página do Github do Microsoft Intune](https://github.com/msintuneappsdk).

- **Experiência do usuário final melhorada ao registrar dispositivos Windows**

  Ao usar o acesso condicional, as etapas de registro para Windows 8.1, Windows 10 Desktop e Windows 10 Mobile foram esclarecidas no site do Portal da Empresa. Agora os usuários verão etapas de **Registro do dispositivo** e **Ingresso no Local de Trabalho** separadas, facilitando a visualização do status de seu dispositivo e a conclusão do processo caso enfrentem uma falha de WPJ (Ingresso no Local de Trabalho). As etapas separadas também devem simplificar o processo de solução de problemas para os administradores de TI. Anteriormente, quando os usuários finais tentavam realizar o registro e todas as etapas de registro eram bem sucedidas, exceto o WPJ, o dispositivo não aparecia na lista de dispositivos para os usuários o identificarem, causando confusão para os usuários.

  - **Apagamento completo agora disponível para dispositivos Windows 10**

    Os laptops e computadores com Windows 10 registrados como dispositivos móveis podem ser apagados para redefinir o dispositivo para suas configurações de fábrica. Para mais informações, confira [How to protect your devices with remote wipe](/sccm/mdm/deploy-use/wipe-lock-reset-devices) (Como proteger seus dispositivos com o apagamento remoto).

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

* Localizar, gerenciar e distribuir aplicativos da Windows Store para Empresas para dispositivos Windows 10 por meio do console do Configuration Manager ([1604](#new-in-1604-technical-preview))
* Configuração do SmartLock para dispositivos Android ([1604](#new-in-1604-technical-preview))
* VPN acionado por aplicativo para dispositivos Windows 10 ([1605](#new-in-1605-technical-preview))
* Nova experiência para ações de dispositivo remoto ([1605](#new-in-1605-technical-preview))
* Aplicativos da Windows Store para Empresas ([1605](#new-in-1605-technical-preview))
* Melhorias gerais para aplicativos adquiridos por volume ([1605](#new-in-1605-technical-preview))
* WIP (Proteção de Informações do Windows) ([1605](#new-in-1605-technical-preview))
* Pré-declarar dispositivos corporativos com número de série do iOS ou IMEI ([1605](#new-in-1605-technical-preview))
* Categorizar automaticamente dispositivos em coleções ([1606](#new-in-1606-technical-preview))

Para obter informações sobre a nova funcionalidade, consulte a documentação da versão de Technical Preview especificada.

## <a name="june-2016"></a>Junho de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune
Os recursos do Intune a seguir introduzidos em junho de 2016 funcionam em implantações híbridas.

- **Integridade do serviço Intune** As informações de integridade do serviço para o Intune foram movidas para um local central com outros serviços da Microsoft. Agora, você encontrará essas informações no Centro de administração do Microsoft 365 em integridade do serviço. Para mais informações, confira essa [postagem no blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/).

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

##  <a name="may-2016"></a>Maio de 2016  

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune  
 Os recursos do Intune a seguir introduzidos em maio de 2016 funcionam em implantações híbridas.

- **SDK DO MAM: Configuração de comprimento do PIN de suporte**

  Agora você pode especificar o comprimento do PIN para aplicativos MAM semelhantes a um PIN do dispositivo. Isso requer que os usuários finais estejam em conformidade com as novas restrições definidas. A tela de PIN está ligeiramente modificada para considerar a entrada mais longa. Para obter detalhes, confira [Configurações de política de MAM para Android](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings) e [Configurações de política de MAM para iOS](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings).  

- **Skype for Business para iOS e Android**

  Agora você pode direcionar o Skype for Business com [MAM sem políticas de registro](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune). Depois que os usuários fizerem logon, as políticas MAM serão aplicadas.  

- **Novos aplicativos disponíveis para gerenciamento com políticas de MAM**

  Os aplicativos Microsoft Word, Excel e PowerPoint para Android agora podem ser associados a políticas de MAM em dispositivos que não estão registrados no Intune. Para obter uma lista completa de aplicativos com suporte, acesse a galeria de aplicativos móveis do Microsoft Intune na página [Microsoft Intune application partners](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx) (Parceiros de aplicativos do Microsoft Intune).  

- **Aplicativo do portal da empresa para Android: Notificações do usuário final**

  As notificações do sistema do aplicativo do Portal da Empresa para Android aparecem quando os usuários finais registram ou removem seus dispositivos do Portal da Empresa.  

- **Site do Portal da empresa: Faixa de identificação de dispositivo fornecerá mais informações aos usuários finais**

  Agora os usuários finais podem identificar mais facilmente o dispositivo selecionado quando estiverem usando o site do Portal da Empresa. Se o dispositivo incorreto for selecionado, eles poderão selecionar o dispositivo correto tocando no link **Toque aqui** na faixa da home page.  


### <a name="new-in-1605-technical-preview"></a>Novo no Technical Preview 1605  
 Os novos recursos a seguir introduzidos em maio de 2016 estão disponíveis para implantações híbridas com o Intune e com o Configuration Manager Technical Preview 1605. Esses recursos exigem que você use o console do Configuration Manager para configurá-los e gerenciá-los.  

- **VPN acionado por aplicativo para dispositivos Windows 10**

  Para dispositivos Windows 10 gerenciados usando o Configuration Manager com o Intune, você pode adicionar uma lista de aplicativos que abrem automaticamente uma conexão VPN que você configurou por meio do console de administração do Configuration Manager. Para mais informações, confira [VPN acionado por aplicativo para dispositivos Windows 10](/sccm/core/get-started/capabilities-in-technical-preview-1605) em [Funcionalidades no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605)  

- **Nova experiência para ações de dispositivo remoto**

  A experiência para executar as ações de dispositivo remoto do console do Configuration Manager foi aprimorada.

  Ações comuns, como **Desativar/Apagar**, **Redefinir Senha**, **Bloqueio Remoto** e **Ignorar Bloqueio de Ativação** agora podem ser encontradas no menu **Ações do Dispositivo Remoto** acessado pelo workspace **Ativos e Conformidade**

  Para mais informações, confira [Nova experiência para ações de dispositivo remoto](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_Remote) em [Funcionalidades no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Aplicativos da Windows Store para Empresas**

  Na [Windows Store para Empresas](https://www.microsoft.com/en-us/business-store), é possível encontrar e adquirir aplicativos para sua organização, individualmente ou por volume. Ao conectar a loja ao Configuration Manager, é possível gerenciar aplicativos adquiridos por volume no console do Configuration Manager. Para mais informações, confira [Aplicativos da Windows Store para Empresas](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_WSFB) em [Funcionalidades no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Melhorias gerais para aplicativos adquiridos por volume**

  Os aplicativos adquiridos por volume da Windows Store para Empresas e da iOS App Store foram consolidados na mesma exibição, **Informações sobre Licença para Aplicativos da Loja**. Além disso, o modo no qual você cria aplicativos adquiridos por volume para o iOS foi aprimorado. Para mais informações, confira [Melhorias gerais para aplicativos adquiridos por volume](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_VPP2) em [Funcionalidades no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Pré-declarar dispositivos corporativos com número de série do iOS ou IMEI**

  Agora é possível identificar os dispositivos corporativos importando seus números IMEI (identidade da estação internacional do equipamento móvel). Você pode carregar um arquivo .csv (valores separados por vírgula) que contém os números IMEI do dispositivo ou inserir manualmente as informações sobre o dispositivo.  Você também pode importar os números de série para dispositivos iOS.  Para mais informações, confira [Pré-declarar dispositivos corporativos com número de série do iOS ou IMEI](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_IMEI) em [Funcionalidades no Technical Preview 1605 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **WIP (Proteção de Informações do Windows)**

  Você pode criar itens de configuração que permitem implantar suas políticas de WIP (Proteção de Informações do Windows), incluindo permitindo que você escolha seus aplicativos protegidos, seu nível de proteção WIP e como encontrar dados empresariais na rede. Para obter mais informações sobre a WIP, consulte os seguintes tópicos:  

  -   [Proteger os dados empresariais usando a WIP (Proteção de Informações do Windows)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [Criar e implantar uma política de Proteção de Informações do Windows (WIP) usando o System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)  
 Não foi realizada a introdução de nenhum recurso híbrido novo em maio de 2016 para o Configuration Manager (Branch Atual).  

##  <a name="april-2016"></a>Abril de 2016  

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


  O suporte para a Windows Store para Empresas está disponível no Configuration Manager Technical Preview 1604 para ajudá-lo a localizar, gerenciar e distribuir aplicativos para os dispositivos Windows 10 sendo gerenciados. Para detalhes, confira [Gerenciar aplicativos adquiridos por volume da Windows Store para Empresas](/sccm/core/get-started/capabilities-in-technical-preview-1604#BKMK_WindowsVPP) em [Funcionalidades no Technical Preview 1604 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604).  

- **Configuração do SmartLock para dispositivos Android**

  Uma nova configuração foi adicionada ao item de configuração Android e Samsung KNOX Standard que permite controlar o recurso SmartLock em dispositivos Android compatíveis.  Você pode usar essa configuração para impedir que os usuários finais configurem o SmartLock. Confira [Configuração do SmartLock para dispositivos Android](/sccm/core/get-started/capabilities-in-technical-preview-1604#BKMK_Smart) no [Funcionalidades do Technical Preview 1604 do System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604).  

### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)  
 Não foi realizada a introdução de nenhum recurso híbrido novo em abril de 2016 para o Configuration Manager (Branch Atual).  

##  <a name="march-2016"></a>Março de 2016  

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

  Você pode usar seu fornecedor de MDM (gerenciamento de dispositivo móvel) de terceiros para aproveitar o gerenciamento "Open-in" do iOS. Você pode definir as restrições nas definições de perfil de configuração e implantar o aplicativo usando seu software de MDM. Quando o usuário instala o aplicativo gerenciado, as restrições são aplicadas. Leia os detalhes: [Políticas de gerenciamento de aplicativo móvel do Microsoft Intune e iOS Open In](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune) na biblioteca do Intune.  

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



## <a name="notices"></a>Avisos

### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 e System Center 2012 R2 Configuration Manager (RTM): Suporte para gerenciamento de dispositivo móvel híbrido termina em 10 de abril de 2017
*11 de janeiro de 2017*

O suporte para o System Center 2012 Configuration Manager SP1 e o System Center 2012 R2 Configuration Manager RTM terminou em 12 julho de 2016. Consequentemente, o suporte a essas versões em conexão com o serviço Microsoft Intune para MDM híbrido termina em 10 de abril de 2017. Após essa data, o MDM híbrido deixará de funcionar com essas versões. Os dispositivos gerenciados se tornarão essencialmente não gerenciados, pois o Intune Connector não se conectará mais ao serviço do Intune. Os dados do Configuration Manager (como aplicativos e políticas) não fluirão até o Intune, e os dados de dispositivo gerenciados não fluirão para o Configuration Manager até que uma atualização ocorra.

Se você estiver executando uma implantação híbrida com o Configuration Manager 2012 SP1 ou R2 RTM, recomendamos que antes de 10 de abril de 2017 você atualize para o Configuration Manager (ramificação atual) ou para o service pack mais recente com suporte do Configuration Manager 2012 (R2 SP1 ou SP2) para evitar a interrupção do serviço.

Recursos adicionais:
- [Atualizar para o System Center Configuration Manager (ramificação atual)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
- [Planejar a atualização para o System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
- [Planejar a atualização para o System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Upload do Portal da Empresa do Windows Phone 8 preterido
*25 de outubro de 2016*

A capacidade de carregar um aplicativo do Portal da Empresa assinado foi removida do console do Configuration Manager, uma vez que o suporte do Intune está sendo preterido para Windows 8, Windows Phone 8 e Windows RT e o suporte para o Portal da Empresa para Windows Phone 8 será encerrado em novembro.  Os dispositivos Windows 8, Windows Phone 8 e Windows RT já registrados continuarão a ter suporte, mas o registro de dispositivos adicionais com essas plataformas não terá suporte.
