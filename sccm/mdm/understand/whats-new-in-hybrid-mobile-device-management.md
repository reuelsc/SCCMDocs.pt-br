---
title: "Novidades no MDM híbrido| Microsoft Docs"
description: "Saiba mais sobre os novos recursos de gerenciamento de dispositivo móvel disponíveis para implantações híbridas com o Intune e o System Center Configuration Manager."
ms.custom: na
ms.date: 02/14/2017
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
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 58c64b2e02e5e5eb54cb50a468502ba6f1e4f0c1
ms.lasthandoff: 03/06/2017

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

## <a name="new-hybrid-features-in-february-2017"></a>Novos recursos híbridos em fevereiro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

Os recursos do Intune a seguir introduzidos em fevereiro de 2017 funcionam em implantações híbridas:

- **Modernização do site Portal da Empresa**

  O site Portal da Empresa dá suporte a aplicativos destinados a usuários que não têm dispositivos gerenciados. O site se alinha com outros produtos e serviços da Microsoft, usando um novo esquema de cores contrastantes, ilustrações dinâmicas e um "menu de hambúrguer", que contém detalhes de contato de suporte técnico e informações sobre os dispositivos gerenciados existentes. A página inicial é reorganizada para enfatizar os aplicativos que estão disponíveis para usuários, com carrosséis para aplicativos Em Destaque e Atualizados Recentemente. Você pode localizar imagens antes e depois disponíveis na página [Atualizações da interface do usuário](/intune/whats-new/whats-new-in-intune-app-ui).

- **Novo endereço de servidor MDM para dispositivos Windows**

  O endereço do servidor MDM para o registro de dispositivos do Windows e do Windows Phone foi alterado de manage.microsoft.com para enrollment.manage.microsoft.com. Notifique o usuário para que ele use enrollment.manage.microsoft.com como o endereço do servidor MDM caso solicitado durante o registro de um dispositivo Windows ou Windows Phone. Essa atualização também requer que qualquer CNAME no DNS que redirecione EnterpriseEnrollment.contoso.com para manage.microsoft.com seja substituído por um CNAME no DNS que redirecione EnterpriseEnrollment.contoso.com para EnterpriseEnrollment-s.manage.microsoft.com. Para obter informações adicionais sobre essa alteração, acesse http://aka.ms/intuneenrollsvrchange.

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Novidades no Configuration Manager Technical Preview 1702

- **Suporte do Android for Work**

  Agora você pode gerenciar dispositivos Android usando o Android for Work em ambientes de MDM híbridos com o Configuration Manager Technical Preview 1702. Os dispositivos Android com suporte agora podem ser registrados como dispositivos Android for Work, o que cria um perfil de trabalho no dispositivo no qual os aplicativos aprovados na Play for Work podem ser implantados. Você também pode configurar e implantar itens de configuração, políticas de conformidade e perfis de acesso aos recursos para esses dispositivos.

- **Configurações de conformidade de aplicativos fora de conformidade**

  Agora você pode criar regras de aplicativos fora de conformidade para aplicativos Android e iOS nas políticas de conformidade. Se os dispositivos tiverem os aplicativos especificados instalados, eles serão marcados como “fora de conformidade” e perderão o acesso aos recursos da empresa de acordo com as políticas de acesso condicional em vigor.

- **Criação e distribuição de certificado PFX e suporte a S/MIME**

  Agora você pode criar e implantar certificados PFX para usuários em um ambiente híbrido. Esse certificado pode então ser usado para criptografia e descriptografia de email S/MIME pelos dispositivos que o usuário registrou.

## <a name="new-hybrid-features-in-january-2017"></a>Novos recursos híbridos em janeiro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

Os recursos do Intune a seguir introduzidos em janeiro de 2017 funcionam em implantações híbridas:

- **Suporte do Android 7.1.1**

  O Intune agora dá suporte total e gerencia o Android 7.1.1.

- **Resolver o problema em que dispositivos iOS estão inativos ou o console do administrador não pode se comunicar com eles**

  Quando os dispositivos dos usuários perdem contato com o Intune, você pode fornecer novas etapas de solução de problemas para ajudá-los a recuperar o acesso aos recursos da empresa. Veja [Dispositivos estão inativos ou o console do administrador não pode se comunicar com eles](/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Novo no Configuration Manager Technical Preview 1701

- **Android and iOS versions are no longer targetable in creation wizards for hybrid MDM (As versões do Android e iOS não precisam mais ser indicadas nos assistentes de criação do MDM híbrido)**

  A partir do Technical Preview 1701 para MDM (gerenciamento de dispositivo móvel) híbrido, você não precisa mais indicar versões específicas do Android e do iOS ao criar novas políticas e perfis de dispositivos gerenciados pelo Intune. Com essa alteração, as implantações híbridas podem fornecer suporte com mais rapidez para novas versões do Android e do iOS sem precisar de uma nova versão ou extensão do Configuration Manager. Para obter mais informações, consulte [Android and iOS versions are no longer targetable in creation wizards for hybrid MDM (As versões do Android e iOS não precisam mais ser indicadas nos assistentes de criação do MDM híbrido)](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).


## <a name="new-hybrid-features-in-december-2016"></a>Novos recursos híbridos em dezembro de 2016

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

Os recursos do Intune a seguir introduzidos em dezembro de 2016 funcionam em implantações híbridas:

- **A MFA (Autenticação Multifator) no registro está migrando para o portal do Azure**

  Anteriormente, você tinha que ir para o console do Intune ou para o console do Configuration Manager para definir o MFA para inscrições do Intune. Com esse recurso atualizado, você faz logon no [Portal do Microsoft Azure] (https://manage.windowsazure.com) usando suas credenciais do Intune e configura as definições MFA por meio do Azure AD. Para obter mais informações, consulte [Autenticação multifator para Microsoft Intune] (https://aka.ms/mfa_ad).

- **Aplicativo de Portal da empresa para Android já disponível na China**

  O aplicativo de Portal da empresa para Android agora está disponível na China. Devido à ausência do Google Play Store na China, os dispositivos Android devem obter aplicativos de marketplaces de aplicativos chinês. O aplicativo de Portal da empresa para Android está disponível para download nos seguintes repositórios:

  -    [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  -    [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  -    [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  -    [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)
  -    [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)

  O aplicativo de Portal da Empresa para Android usa o Google Play Services para se comunicar com o serviço Microsoft Intune. Como o Google Play Services ainda não está disponível na China, executar qualquer uma das seguintes tarefas pode levar até 8 horas para ser concluída.

  | Console de Administração do Configuration Manager | Aplicativo Portal da Empresa do Intune para Android | Site do Portal da empresa do Intune |
  |----|----|----|        
  | Desativar/apagar (remover todos os dados)    | Remover um dispositivo remoto | Remover dispositivo (local e remoto) |
  | Desativar/apagar (remover dados da empresa)    | Redefinir o dispositivo | Redefinir o dispositivo|
  | Implantações de aplicativo novo ou atualizado | Instalar aplicativos de linha de negócios disponíveis | Redefinição de senha de dispositivo|
  | Bloqueio remoto    | | |
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


## <a name="notices"></a>Avisos

### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 e System Center 2012 R2 Configuration Manager (RTM): o suporte para o gerenciamento de dispositivo móvel híbrido terma em 10 de abril de 2017

*11 de janeiro de 2017*

O suporte para o System Center 2012 Configuration Manager SP1 e o System Center 2012 R2 Configuration Manager RTM terminou em 12 julho de 2016. Consequentemente, o suporte a essas versões em conexão com o serviço Microsoft Intune para MDM híbrido termina em 10 de abril de 2017. Após essa data, o MDM híbrido deixará de funcionar com essas versões. Os dispositivos gerenciados se tornarão essencialmente não gerenciados, pois o Intune Connector não se conectará mais ao serviço do Intune. Os dados do Configuration Manager (como aplicativos e políticas) não fluirão até o Intune, e os dados de dispositivo gerenciados não fluirão para o Configuration Manager até que uma atualização ocorra.

Se você estiver executando uma implantação híbrida com o Configuration Manager 2012 SP1 ou R2 RTM, recomendamos que antes de 10 de abril de 2017 você atualize para o Configuration Manager (ramificação atual) ou para o service pack mais recente com suporte do Configuration Manager 2012 (R2 SP1 ou SP2) para evitar a interrupção do serviço.

Recursos adicionais:
-    [Atualizar para o System Center Configuration Manager (ramificação atual)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-    [Planejar a atualização para o System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-    [Planejar a atualização para o System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Upload do Portal da Empresa do Windows Phone 8 preterido
*25 de outubro de 2016*

A capacidade de carregar um aplicativo do Portal da Empresa assinado foi removida do console do Configuration Manager, uma vez que o suporte do Intune está sendo preterido para Windows 8, Windows Phone 8 e Windows RT e o suporte para o Portal da Empresa para Windows Phone 8 será encerrado em novembro.  Os dispositivos Windows 8, Windows Phone 8 e Windows RT já registrados continuarão a ter suporte, mas o registro de dispositivos adicionais com essas plataformas não terá suporte.


### <a name="see-also"></a>Consulte também

- [Recursos do MDM híbrido anteriores](whats-new-hybrid-archive.md)
- [Novidades do MDM no System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)

