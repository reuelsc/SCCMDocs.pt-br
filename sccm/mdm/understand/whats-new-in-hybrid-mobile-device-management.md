---
title: "O que há de novo no MDM híbrido com o Configuration Manager | Microsoft Docs"
description: "Saiba mais sobre os novos recursos de gerenciamento de dispositivo móvel disponíveis para implantações híbridas com o Configuration Manager e o Intune."
ms.custom: na
ms.date: 06/30/2017
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
ms.translationtype: HT
ms.sourcegitcommit: c0d94b8e6ca6ffd82e879b43097a9787e283eb6d
ms.openlocfilehash: 8e660c667daec9b1f7630e15599df5e3cfe55b5e
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

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

## <a name="july-2017"></a>Julho de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Avisos de fim de suporte adicionados para Android e Windows Phone**

    Novos avisos foram adicionados em relação ao fim do suporte para versões do Android e do Windows Phone. Para obter mais detalhes, veja [Avisos](#notices).



### <a name="new-in-configuration-manager-current-branch"></a>Novo no Configuration Manager (Branch Atual)

Os seguintes recursos que estavam anteriormente disponíveis nas versões do Configuration Manager Technical Preview agora estão disponíveis em implantações híbridas com o Intune e a versão 1706 do Configuration Manager (branch atual).

- [Suporte do Entrust para autoridades de certificação Entrust](/sccm/core/get-started/capabilities-in-technical-preview-1706#support-for-entrust-certification-authorities)
- [Novas configurações de política de gerenciamento de aplicativo móvel](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-mobile-application-management-policy-settings)
- [Atualizações para configuração de compartilhamento do Android for Work](/sccm/core/plan-design/changes/whats-new-in-version-1706#updates-to-android-for-work-sharing-configuration)
- [Novas regras de política de conformidade do dispositivo](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-device-compliance-policy-rules)
- [Novas definições de configuração para dispositivos com Windows 10 que não são gerenciados com o cliente do Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client)
- [Suporte do Cisco (IPsec) para perfis de VPN do macOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#cisco-ipsec-support-for-macos-vpn-profiles)

## <a name="june-2017"></a>Junho de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Alterar sua autoridade de MDM**

  A partir do Configuration Manager versão 1610 e do Microsoft Intune versão 1705, você pode alterar sua autoridade MDM sem precisar entrar em contato com o Suporte da Microsoft e sem a necessidade de cancelar o registro e registrar novamente os dispositivos gerenciados existentes. Para obter detalhes, veja [Alterar sua autoridade de MDM]( /sccm/mdm/deploy-use/change-mdm-authority).

- **Integração gerenciada de proxy do navegador e aplicativo**

  O Intune Managed Browser agora pode ser integrado ao serviço de Proxy de Aplicativo do Azure AD para permitir que os usuários acessem sites internos, mesmo quando estão trabalhando remotamente. Os usuários do navegador simplesmente inserem a URL normalmente e o Managed Browser encaminha a solicitação através do gateway Web do proxy de aplicativo. Para saber mais, veja [Gerenciar o acesso à Internet usando políticas no navegador gerenciado](/intune/app-configuration-managed-browser).

- **Agora, o aplicativo Portal da Empresa para Android tem uma nova experiência do usuário final para as Políticas de Proteção do Aplicativo**

  Com base nos comentários do cliente, modificamos o aplicativo Portal da Empresa para Android mostrar um botão **Acessar Conteúdo da Empresa**. A intenção é impedir que os usuários finais passem desnecessariamente pelo processo de inscrição quando eles só precisam acessar os aplicativos que dão suporte a Políticas de Proteção do Aplicativo, um recurso de gerenciamento de aplicativo móvel do Intune. Veja essas alterações na página [Novidades na interface do usuário do aplicativo](/intune/whats-new-app-ui).

- **Nova ação de menu para remover facilmente o Portal da Empresa**

  Com base nos comentários do usuário, o aplicativo Portal da Empresa para Android adicionou uma nova ação de menu para iniciar a remoção do Portal da Empresa de seu dispositivo. Esta ação remove o dispositivo do gerenciamento do Intune para que o aplicativo possa ser removido do dispositivo pelo usuário. Veja essas alterações na página [Novidades na interface do usuário do aplicativo](/intune/whats-new-app-ui) e na [documentação de usuário final do Android](/intune-user-help/unenroll-your-device-from-intune-android).

- **Aprimoramentos na sincronização de aplicativo com a Atualização do Windows 10 para Criadores**

  O aplicativo Portal da Empresa para Windows 10 iniciará automaticamente uma sincronização para solicitações de instalação de aplicativo para dispositivos com a Atualização do Windows 10 para Criadores (versão 1703). Isso reduzirá o problema de atraso das instalações de aplicativos durante o estado de "Sincronização Pendente". Além disso, os usuários poderão iniciar manualmente uma sincronização de dentro do aplicativo. Veja essas alterações na página [Novidades na interface do usuário do aplicativo](/intune/whats-new-app-ui).

- **Nova experiência orientada para o Portal da Empresa do Windows 10**

  O aplicativo do Portal da Empresa para o Windows 10 incluirá uma experiência passo a passo interativa do Intune para dispositivos que não foram identificados ou registrados. A nova experiência fornece instruções passo a passo que guiam o usuário pelo processo de inscrição no Azure Active Directory (exigido para recursos de Acesso Condicional) e inscrição de MDM (exigido para os recursos de gerenciamento de dispositivo). A experiência guiada estará acessível na home page do Portal da Empresa. Os usuários podem continuar a usar o aplicativo se não concluírem o registro e inscrição, mas enfrentarão uma funcionalidade limitada.

  Esta atualização só fica visível em dispositivos que executam a Atualização de Aniversário do Windows 10 (build 1607) ou superior. Veja essas alterações na página [Novidades na interface do usuário do aplicativo](/intune/whats-new-app-ui).

- **Aprimoramentos nos blocos de aplicativo no aplicativo Portal da Empresa para iOS**

  Atualizamos o design dos blocos do aplicativo na home page a fim de refletir a cor de identidade visual que você definiu para o Portal da Empresa. Para saber mais, veja [Novidades na interface do usuário do aplicativo](/intune/whats-new-app-ui).

- **O seletor de conta já está disponível para o aplicativo Portal da Empresa para iOS**

  Os usuários de dispositivos iOS poderão ver nosso novo seletor de conta ao entrar no Portal da Empresa se usarem sua conta corporativa ou de estudante para entrar em outros aplicativos da Microsoft. Para saber mais, veja [Novidades na interface do usuário do aplicativo](/intune/whats-new-app-ui).

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Novidades da Visualização Técnica 1706 do Configuration Manager

- **Novas configurações de política de gerenciamento de aplicativo móvel**    

  As seguintes configurações de política MAM (gerenciamento de aplicativo móvel) estão disponíveis:

  - **Bloquear captura de tela (somente dispositivos Android):** especifica que as funcionalidades de captura de tela do dispositivo sejam bloqueadas ao usar esse aplicativo.
  - **Desabilitar a sincronização de contato:** impede que o aplicativo salve dados no aplicativo de Contatos nativo do dispositivo.
  - **Desabilitar impressão:** impede que o aplicativo imprima dados corporativos ou de estudante.

  Veja [proteger aplicativos usando políticas de proteção de aplicativos no Configuration Manager](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies) para testar as novas configurações de política de proteção do aplicativo.

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

  O Navegador Gerenciado está recebendo ícones atualizados para as versões do Android e iOS do aplicativo. O novo ícone conterá o emblema Intune atualizado para torná-lo mais consistente com outros aplicativos no Enterprise Mobility + Security (EM+S). Você pode ver o ícone novo para o Navegador Gerenciado nas [novidades na página de IU do aplicativo Intune](/intune/whats-new/whats-new-in-intune-app-ui.md).

  O Portal da Empresa também está recebendo ícones atualizados para as versões do Android, iOS e Windows do aplicativo para aprimorar a consistência com outros aplicativos EM+S. Esses ícones serão lançados gradualmente nas plataformas de abril até o final de maio.

- **Indicador de progresso de entrada no Portal da Empresa para Android**

  Uma atualização para o aplicativo para Android do Portal da Empresa mostra um indicador de progresso de entrada quando o usuário inicia ou retoma o aplicativo. O indicador avança em novos status, começando com "Conectando …", então, "Entrando..." e "Verificando os requisitos de segurança..." antes de permitir que o usuário acesse o aplicativo. Você pode ver as novas telas do aplicativo de Portal da Empresa para Android nas [novidades na página de IU do aplicativo Intune](/intune/whats-new/whats-new-in-intune-app-ui.md).

- **Bloquear os aplicativos de acessarem o SharePoint Online**

  Agora, você pode criar uma política de acesso condicional com base em aplicativos para impedir que os aplicativos, que não têm políticas de proteção do aplicativo aplicadas, acessem o [SharePoint Online](/InTune/deploy-use/mam-ca-for-sharepoint-online). No cenário de acesso condicional com base em aplicativos, você pode especificar os aplicativos que deseja ter acesso ao SharePoint Online usando o portal do Azure.

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

  Para obter mais informações sobre essas alterações, confira [Atualizações da interface do usuário para aplicativos de usuário final do Intune](/intune/whats-new/whats-new-in-intune-app-ui).

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

- **Suporte para aplicativos de linha de negócios na Windows Store para Empresas**

  Agora você pode sincronizar aplicativos personalizados de linha de negócios da Windows Store para Empresas.

- **Novas ferramentas de monitoramento de defesa contra ameaças móveis**

    Você agora tem novas maneiras de monitorar o status de conformidade com seu provedor de serviços de defesa contra ameaças móveis.

    Para saber mais, veja [Como monitorar a conformidade com defesa contra ameaças móveis](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).

## <a name="february-2017"></a>Fevereiro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Modernização do site Portal da Empresa**

  O site Portal da Empresa dá suporte a aplicativos destinados a usuários que não têm dispositivos gerenciados. O site se alinha com outros produtos e serviços da Microsoft, usando um novo esquema de cores contrastantes, ilustrações dinâmicas e um "menu de hambúrguer", que contém detalhes de contato de suporte técnico e informações sobre os dispositivos gerenciados existentes. A página inicial é reorganizada para enfatizar os aplicativos que estão disponíveis para usuários, com carrosséis para aplicativos Em Destaque e Atualizados Recentemente. Você pode localizar imagens antes e depois disponíveis na página [Atualizações da interface do usuário](/intune/whats-new/whats-new-in-intune-app-ui).

- **Novo endereço de servidor MDM para dispositivos Windows**

  O endereço do servidor MDM para o registro de dispositivos do Windows e do Windows Phone foi alterado de manage.microsoft.com para enrollment.manage.microsoft.com. Notifique o usuário para que ele use enrollment.manage.microsoft.com como o endereço do servidor MDM caso solicitado durante o registro de um dispositivo Windows ou Windows Phone. Essa atualização também requer que qualquer CNAME no DNS que redirecione EnterpriseEnrollment.contoso.com para manage.microsoft.com seja substituído por um CNAME no DNS que redirecione EnterpriseEnrollment.contoso.com para EnterpriseEnrollment-s.manage.microsoft.com. Para obter informações adicionais sobre essa alteração, acesse http://aka.ms/intuneenrollsvrchange.

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Novidades no Configuration Manager Technical Preview 1702

- **Suporte do Android for Work**

  Agora você pode gerenciar dispositivos Android usando o Android for Work em ambientes de MDM híbridos com o Configuration Manager Technical Preview 1702. Os dispositivos Android com suporte agora podem ser registrados como dispositivos Android for Work, o que cria um perfil de trabalho no dispositivo no qual os aplicativos aprovados na Play for Work podem ser implantados. Você também pode configurar e implantar itens de configuração, políticas de conformidade e perfis de acesso aos recursos para esses dispositivos. Para saber mais, veja [Suporte do Android for Work](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support).

- **Configurações de conformidade de aplicativos fora de conformidade**

  Agora você pode criar regras de aplicativos fora de conformidade para aplicativos Android e iOS nas políticas de conformidade. Se os dispositivos tiverem os aplicativos especificados instalados, eles serão marcados como "em não conformidade" e perderão o acesso aos recursos da empresa de acordo com as políticas de acesso condicional em vigor. Para saber mais, veja [Aprimoramentos na política de conformidade de dispositivo de acesso condicional](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements).

- **Criação e distribuição de certificado PFX e suporte a S/MIME**

  Agora você pode criar e implantar certificados PFX para usuários em um ambiente híbrido. Esse certificado pode então ser usado para criptografia e descriptografia de email S/MIME pelos dispositivos que o usuário registrou. Para saber mais, veja [Criar certificados PFX com suporte a S MIME](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support).

- **Suporte para parâmetros de configuração adicionais do iOS**
   
    Agora você tem 42 configurações adicionais do iOS que pode configurar como parte de um item de configuração. A maioria das configurações (35 ao todo) foi adicionada para dispositivos iOS supervisionados. Para saber mais, confira [Novas configurações de conformidade para dispositivos iOS](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices).

## <a name="january-2017"></a>Janeiro de 2017

### <a name="new-in-microsoft-intune"></a>Novo no Microsoft Intune

- **Suporte do Android 7.1.1**

  O Intune agora dá suporte total e gerencia o Android 7.1.1.

- **Resolver o problema em que dispositivos iOS estão inativos ou o console do administrador não pode se comunicar com eles**

  Quando os dispositivos dos usuários perdem contato com o Intune, você pode fornecer novas etapas de solução de problemas para ajudá-los a recuperar o acesso aos recursos da empresa. Veja [Dispositivos estão inativos ou o console do administrador não pode se comunicar com eles](/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Novo no Configuration Manager Technical Preview 1701

- **Android and iOS versions are no longer targetable in creation wizards for hybrid MDM (As versões do Android e iOS não precisam mais ser indicadas nos assistentes de criação do MDM híbrido)**

  A partir do Technical Preview 1701 para MDM (gerenciamento de dispositivo móvel) híbrido, você não precisa mais indicar versões específicas do Android e do iOS ao criar novas políticas e perfis de dispositivos gerenciados pelo Intune. Com essa alteração, as implantações híbridas podem fornecer suporte com mais rapidez para novas versões do Android e do iOS sem precisar de uma nova versão ou extensão do Configuration Manager. Para obter mais informações, consulte [Android and iOS versions are no longer targetable in creation wizards for hybrid MDM (As versões do Android e iOS não precisam mais ser indicadas nos assistentes de criação do MDM híbrido)](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).


## <a name="notices"></a>Avisos

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

