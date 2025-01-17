---
title: Acesso condicional
titleSuffix: Configuration Manager
description: Saiba como usar o acesso condicional no System Center Configuration Manager para proteger emails e outros serviços.
ms.date: 03/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b04727b-d563-422f-8d59-4dd66215d0b3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: da2c809c4aaf95de450570814a5b967ca563a2c2
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68340284"
---
# <a name="manage-access-to-services-in-system-center-configuration-manager"></a>Gerenciar o acesso a serviços no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o acesso condicional para especificar condições para ajudar a proteger o email e outros serviços nos dispositivos registrados no Microsoft Intune.  

> [!Important]  
> O MDM híbrido, incluindo acesso condicional local, são [recursos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)preteridos. Para saber mais, confira [O que é o MDM híbrido](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  
> 
> Se você usar o acesso condicional em dispositivos gerenciados com o cliente do Configuration Manager, para certificar-se de que eles ainda estão protegidos, primeiro habilite o acesso condicional no Intune para esses dispositivos antes de migrar. Habilite o cogerenciamento no Configuration Manager, mova a carga de trabalho da política de conformidade para o Intune e conclua a migração do Intune híbrido para o Intune autônomo. Para obter mais informações, consulte [acesso condicional com](https://docs.microsoft.com/sccm/comanage/quickstart-conditional-access)o cogerenciamento. 


 Para obter informações sobre o acesso condicional em dispositivos que são gerenciados com o cliente do Configuration Manager, consulte [gerenciar o acesso aos serviços do Office 365 para PCs gerenciados pelo System Center Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  


 Um fluxo típico de acesso condicional será semelhante ao seguinte:  

 ![ConditionalAccess4](media/ConditionalAccess4.png)  

 Use o acesso condicional para gerenciar o acesso aos seguintes serviços:  

- Microsoft Exchange Local  

- Microsoft Exchange Online  

- Exchange Online dedicado  

- SharePoint Online  

- Skype for Business Online

- Dynamics CRM Online

  Para implementar o acesso condicional, você define dois tipos de política no Configuration Manager:  

- **Políticas de conformidade** são políticas opcionais que você pode implantar em coleções de usuários e avaliar configurações como:  

  - Senha  

  - Criptografia  

  - Se o dispositivo está desbloqueado ou com raiz  

  - Se o email no dispositivo é gerenciado por uma política do Configuration Manager ou do Microsoft Intune  

    Um dispositivo relata conformidade com quaisquer políticas de acesso condicional aplicáveis, caso você não implante nenhuma política de conformidade nele.

- **Políticas de acesso condicional** destinam-se a um serviço específico. Essas políticas definem regras, como quais grupos de usuários de segurança do Azure Active Directory ou coleções de usuários do Configuration Manager devem ser direcionados ou excluídos.  

   Configure a política de acesso condicional do Exchange Local no console do Configuration Manager. No entanto, ao configurar uma política do Exchange Online ou do SharePoint Online, o console do Microsoft Intune será aberto para configurar a política.  

   Ao contrário de outras políticas do Microsoft Intune ou Configuration Manager, você não implanta políticas de acesso condicional. Em vez disso, você configura essas políticas uma vez e elas se aplicam a todos os usuários direcionados.  

  Quando os dispositivos não atendem às condições configuradas, o usuário é orientado pelo registro do dispositivo e pela correção do problema de conformidade do dispositivo.  

Antes de começar a usar o acesso condicional, certifique-se de que você tenha os requisitos corretos no lugar:  

## <a name="requirements-for-exchange-online-using-the-shared-multi-tenant-environment"></a>Requisitos para o Exchange Online (usando o ambiente de multilocatário compartilhado)
O Acesso condicional ao Exchange Online dá suporte a dispositivos que executam:
- Windows 8.1 e posterior (quando registrado com o Intune)
- Windows 7.0 ou Windows 8.1 (quando ingressado no domínio)
- Windows Phone 8.1 e posterior
- iOS 7.1 e posterior
- Android 4.0 e posterior, Samsung KNOX Standard 4.0 e posterior

  **Além disso**:
- Os dispositivos devem ser ingressados no local de trabalho, que registra o dispositivo com o AAD DRS (Serviço de registro de dispositivo do Active Directory do Azure).<br />     
- Os PCs ingressados no domínio devem ser registrados automaticamente no Active Directory do Azure por meio da política de grupo ou do MSI.

  A seção **Acesso condicional para computadores** deste artigo descreve todos os requisitos para habilitar o acesso condicional em um computador.<br />     
  O AAD DRS é ativado automaticamente para clientes do Microsoft Intune e Office 365. Clientes que já implantaram o Serviço de Registro de Dispositivos do ADFS não veem os dispositivos registrados no Active Directory local.
- Use uma assinatura do Office 365 que inclui o Exchange Online (como E3). Os usuários devem ser licenciados para o Exchange Online.
- O conector do Exchange Server é opcional e conecta o Configuration Manager ao Microsoft Exchange Online. Esse conector ajuda você a monitorar as informações do dispositivo por meio do console do Configuration Manager. Para obter mais informações, consulte [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
  Não é necessário ter o conector para usar políticas de conformidade ou políticas de acesso condicional. A execução de relatórios sobre o impacto do acesso condicional exige o conector.

## <a name="requirements-for-exchange-online-dedicated"></a>Requisitos para o Exchange Online dedicado
O acesso condicional ao Exchange Online dedicado dá suporte a dispositivos que executam:
- Windows 8 e posterior (quando registrado com o Intune)
- Windows 7.0 ou Windows 8.1 (quando ingressado no domínio)

  Acesso condicional para PCs ingressados no domínio somente para locatários no novo ambiente dedicado do Exchange Online.
- Windows Phone 8 e posterior
- Qualquer dispositivo iOS que usa um cliente de email do Exchange ActiveSync (EAS)
- Android 4 e posterior.
- Para locatários no ambiente herdado do Exchange Online dedicado:    

  Use o conector do Exchange Server, que conecta o Configuration Manager ao Microsoft Exchange Local. O conector permite gerenciar dispositivos móveis e habilitar o acesso condicional. Para obter mais informações, consulte [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
- Para locatários no novo ambiente do Exchange Online dedicado:     
  O conector do Exchange Server é opcional, que conecta o Configuration Manager ao Microsoft Exchange Online e ajuda você a gerenciar as informações do dispositivo. Para obter mais informações, consulte [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md). Não é necessário ter o conector para usar políticas de conformidade ou políticas de acesso condicional. A execução de relatórios sobre o impacto do acesso condicional exige o conector.  

## <a name="requirements-for-exchange-on-premises"></a>Requisitos do Exchange Local
O acesso condicional ao Exchange Local dá suporte a:
- Windows 8 e posterior (quando registrado com o Intune)
- Windows Phone 8 e posterior
- Aplicativo de email nativo no iOS
- Aplicativo de email nativo no Android 4 ou posterior
- Não há suporte para o aplicativo Microsoft Outlook (Android e iOS)

**Além disso**:

- A versão do Exchange deve ser Exchange 2010 ou posterior
- Há suporte para a matriz de CAS (Servidor de Acesso de Cliente) do servidor Exchange

> [!TIP]
> Se o ambiente do Exchange estiver em uma configuração de servidor de CAS, instale o conector do Exchange local em qualquer um dos servidores de CAS.
> - Use o conector do Exchange Server, que conecta o Configuration Manager ao Microsoft Exchange Local. O conector permite gerenciar dispositivos móveis e habilitar o acesso condicional. Para obter mais informações, consulte [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
>   - Use a última versão do conector do Exchange Local. Configure o conector do Exchange Connector Local pelo console do Configuration Manager. Para obter instruções detalhadas, veja [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
>   - Configurar somente o conector no site primário do Configuration Manager

- O Exchange ActiveSync pode ser configurado com autenticação baseada em certificado ou na entrada de credenciais do usuário


## <a name="requirements-for-skype-for-business-online"></a>Requisitos para o Skype for Business Online
O acesso condicional ao Skype Online oferece suporte a dispositivos que executam:
- iOS 7.1 e posterior
- Android 4.0 e posterior
- Samsung KNOX Standard 4.0 ou posterior

Habilite a [autenticação moderna](https://aka.ms/SkypeModernAuth) para o Skype for Business Online. 

Todos os usuários devem usar o Skype for Business Online. Se você tiver uma implantação com o Skype for Business Online e o Skype for Business local, a política de acesso condicional não será aplicada aos usuários locais.

## <a name="requirements-for-sharepoint-online"></a>Requisitos para o SharePoint Online
O Acesso condicional ao SharePoint Online dá suporte a dispositivos que executam:
- Windows 8.1 e posterior (quando registrado com o Intune)
- Windows 7.0 ou Windows 8.1 (quando ingressado no domínio)
- Windows Phone 8.1 e posterior
- iOS 7.1 e posterior
- Android 4.0 e posterior, Samsung KNOX Standard 4.0 e posterior

  **Além disso**:
- Os dispositivos devem ser ingressados no local de trabalho, que registra o dispositivo com o AAD DRS (Serviço de registro de dispositivo do Active Directory do Azure).

  Os PCs ingressados no domínio devem ser registrados automaticamente no Active Directory do Azure por meio da política de grupo ou do MSI. A seção **Acesso condicional para computadores** deste artigo descreve todos os requisitos para habilitar o acesso condicional em um computador.

  O AAD DRS é ativado automaticamente para clientes do Microsoft Intune e Office 365. Clientes que já implantaram o Serviço de Registro de Dispositivos do ADFS não veem os dispositivos registrados no Active Directory local.
- Uma assinatura do SharePoint Online é necessária e os usuários devem ser licenciados para o SharePoint Online.

  ### <a name="conditional-access-for-pcs"></a>Acesso condicional para PCs

  Configure o acesso condicional para computadores que executam aplicativos da área de trabalho do Office e acesse o Exchange Online ou SharePoint Online. Os PCs devem atender aos seguintes requisitos:
- O computador deve executar o Windows 7.0 ou Windows 8.1
- O computador deve estar ingressado no domínio ou estar em conformidade

  Para estar em conformidade, o computador deve ser registrado no Microsoft Intune e obedecer às políticas.

  Para PCs ingressados no domínio, você deve configurá-lo para [registrar o dispositivo automaticamente](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/) com o Active Directory do Azure.
- [A autenticação moderna do Office 365 deve estar habilitada](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)e ter todas as atualizações mais recentes do Office.<br />     A autenticação moderna leva a entrada baseada na ADAL (Active Directory Authentication Library) para os clientes do Windows com Office 2013 e permite uma melhor segurança como a autenticação multifator e a autenticação baseada em certificado.
- Configure as regras de declarações do ADFS para bloquear protocolos de autenticação não moderna.  

## <a name="next-steps"></a>Próximas etapas  
 Leia os tópicos a seguir para saber como configurar políticas de conformidade e políticas de acesso condicional para seu cenário necessário:  

- [Gerenciar políticas de conformidade do dispositivo no System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)  

- [Gerenciar acesso a email no System Center Configuration Manager](../../protect/deploy-use/manage-email-access.md)  

- [Gerenciar o acesso ao SharePoint Online no System Center Configuration Manager](../../protect/deploy-use/manage-sharepoint-online-access.md)  

- [Gerenciar o acesso do Skype for Business Online](../../protect/deploy-use/manage-skype-for-business-online-access.md)  

### <a name="see-also"></a>Consulte também  

 [Introdução às configurações de conformidade no System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md)
