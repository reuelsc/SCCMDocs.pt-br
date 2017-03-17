---
title: Acesso condicional | Microsoft Docs
description: "Saiba como usar o acesso condicional no System Center Configuration Manager para proteger emails e outros serviços."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b04727b-d563-422f-8d59-4dd66215d0b3
caps.latest.revision: 26
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: ea9184cd4fdc87513ed489f0f568efa6d64c1caa
ms.lasthandoff: 03/06/2017


---

# <a name="manage-access-to-services-in-system-center-configuration-manager"></a>Gerenciar o acesso a serviços no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


## <a name="conditional-access-in-system-center-configuration-manager"></a>Acesso condicional no System Center Configuration Manager
Use o **acesso condicional** para proteger emails e outros serviços nos dispositivos registrados no Microsoft Intune, com base nas condições especificadas.  

 Para saber mais sobre **acesso condicional em computadores que são gerenciados com o System Center Configuration Manager** e avaliados quanto à conformidade, consulte [Gerenciar o acesso aos serviços O365 para computadores gerenciados pelo System Center Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  


 Um fluxo típico de acesso condicional será semelhante ao seguinte:  

 ![ConditionalAccess4](media/ConditionalAccess4.png)  

 Use o acesso condicional para gerenciar o acesso aos seguintes serviços:  

-   Microsoft Exchange Local  

-   Microsoft Exchange Online  

-   Exchange Online dedicado  

-   SharePoint Online  

-   Skype for Business Online

-   Dynamics CRM Online

 Para implementar o acesso condicional, você define dois tipos de política no Configuration Manager:  

-   **Políticas de conformidade** são políticas opcionais que você pode implantar em coleções de usuários e avaliar configurações como:  

    -   Senha  

    -   Criptografia  

    -   Se o dispositivo está desbloqueado ou com raiz  

    -   Se o email no dispositivo for gerenciado por uma política do Configuration Manager ou o Intune  

     **Se nenhuma política de conformidade for implantada em um dispositivo, então todas as políticas de acesso condicional aplicável tratarão o dispositivo como compatível**.  

-   **Políticas de acesso condicional** são configuradas para um serviço específico e definem regras como, por exemplo, quais grupos de usuário de segurança do Azure Active Directory ou coleções de usuários do Configuration Manager serão definidos como destino, ou isentos.  

     Configure uma política de acesso condicional para o Exchange no Local por meio do console do Configuration Manager. No entanto, ao configurar uma política do Exchange Online ou do SharePoint Online, isso abrirá o console de administração do Intune no qual a política é configurada.  

     Ao contrário de outras políticas do Intune ou Configuration Manager, você não implanta políticas de acesso condicional. Em vez disso, você as configura uma vez e elas se aplicam a todos os seus usuários de destino.  

 Quando dispositivos não atendem às condições que você configurou, o usuário é guiado pelo processo de registro do dispositivo e correção do problema que está impedindo o dispositivo de estar em conformidade.  

**Antes** de começar a usar o acesso condicional, certifique-se de que você tenha os **requisitos** corretos em vigor:  

## <a name="requirements-for-exchange-online-using-the-shared-multi-tenant-environment"></a>Requisitos para o Exchange Online (usando o ambiente de multilocatário compartilhado)
O Acesso condicional ao Exchange Online dá suporte a dispositivos que executam:
-   Windows 8.1 e posterior (quando registrado com o Intune)
-   Windows 7.0 ou Windows 8.1 (quando ingressado no domínio)
-   Windows Phone 8.1 e posterior
-   iOS 7.1 e posterior
-   Android 4.0 e posterior, Samsung KNOX Standard 4.0 e posterior

 **Além disso**:
-   Os dispositivos devem ser ingressados no local de trabalho, que registra o dispositivo com o AAD DRS (Serviço de registro de dispositivo do Active Directory do Azure).<br />     
- Os PCs ingressados no domínio devem ser registrados automaticamente no Active Directory do Azure por meio da política de grupo ou do MSI.

  A seção **Acesso condicional para PCs** neste tópico descreve todos os requisitos para habilitar o acesso condicional de um PC.<br />     
  O AAD DRS será ativado automaticamente para clientes do Intune e do Office 365. Clientes que já tiverem implantado o Serviço de Registro de Dispositivos do ADFS não verão dispositivos registrados no seu Active Directory local.
-   Você deve usar uma assinatura do Office 365 que inclui o Exchange Online (como E3) e os usuários devem ser licenciados para o Exchange Online.
-   O **conector do Exchange Server** é opcional, conecta o Configuration Manager ao Microsoft Exchange Online e ajuda você a monitorar informações de dispositivo por meio do console do Configuration Manager (veja [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
O conector não é necessário para usar políticas de conformidade ou políticas de acesso condicional, mas é necessário para executar relatórios que ajudam a avaliar o impacto de acesso condicional.

## <a name="requirements-for-exchange-online-dedicated"></a>Requisitos para o Exchange Online dedicado
O acesso condicional ao Exchange Online dedicado dá suporte a dispositivos que executam:
-   Windows 8 e posterior (quando registrado com o Intune)
-   Windows 7.0 ou Windows 8.1 (quando ingressado no domínio)

  Acesso condicional para PCs ingressados no domínio somente para locatários no novo ambiente dedicado do Exchange Online.
-   Windows Phone 8 e posterior
-   Qualquer dispositivo iOS que usa um cliente de email do Exchange ActiveSync (EAS)
-   Android 4 e posterior.
-   Para locatários no **ambiente herdado do Exchange Online dedicado**:    

  Você deve usar o **conector do Exchange Server** que conecta o Configuration Manager ao Microsoft Exchange no Local. Isso permite que você gerencie dispositivos móveis e habilita o acesso condicional (veja [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
-   Para locatários no **novo ambiente do Exchange Online dedicado**:     
  O **conector do Exchange Server** opcional conecta o Configuration Manager ao Microsoft Exchange Online e ajuda você a gerenciar informações de dispositivo (veja [Gerenciar dispositivos móveis usando o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)). O conector não é necessário para usar políticas de conformidade ou políticas de acesso condicional, mas é necessário para executar relatórios que ajudam a avaliar o impacto de acesso condicional.  

## <a name="requirements-for-exchange-on-premises"></a>Requisitos para o Exchange Local
O acesso condicional ao Exchange no Local dá suporte a:
-   Windows 8 e posterior (quando registrado com o Intune)
-   Windows Phone 8 e posterior
-   Aplicativo de email nativo no iOS
-   Aplicativo de email nativo no Android 4 ou posterior
-   Não há suporte para o aplicativo Microsoft Outlook (Android e iOS).

**Além disso**:

-  A versão do Exchange deve ser Exchange 2010 ou posterior. Há suporte para a matriz de CAS (Servidor de Acesso de Cliente) do servidor Exchange.

> [!TIP]
> Se o ambiente do Exchange estiver em uma configuração de servidor de CAS, instale o conector do Exchange local em qualquer um dos servidores de CAS.
- Você deve usar o **conector do Exchange Server** que conecta o Configuration Manager ao Microsoft Exchange no Local. Isso permite que você gerencie dispositivos móveis e habilita o acesso condicional (veja [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
  - Certifique-se de estar usando a versão mais recente do **conector do Exchange local**. O Exchange Connector local deve ser configurado pelo console do Configuration Manager. Para obter instruções detalhadas, veja [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
  - O conector deve ser configurado somente no site primário do System Center Configuration Manager.</li><li>Esse conector dá suporte a ambiente de CAS do Exchange. <br />        Ao configurar o conector, você deve configurá-lo para que ele se comunique com um dos servidores de CAS do Exchange.

- O Exchange ActiveSync pode ser configurado com autenticação baseada em certificado ou em entrada de credenciais de usuário


## <a name="requirements-for-skype-for-business-online"></a>Requisitos para o Skype for Business Online
O Acesso condicional ao SharePoint Online dá suporte a dispositivos que executam:
 -   iOS 7.1 e posterior
 -   Android 4.0 e posterior
 -   Samsung KNOX Standard 4.0 ou posterior

**Além disso,** você deve habilitar a autenticação moderna para o Skype for Business Online. Preencha este [formulário do Connect](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) para ser registrado no programa de autenticação moderna.

Todos os usuários finais deverão usar o Skype for Business Online. Se você tiver uma implantação com o Skype for Business Online e o Skype for Business no local, política de acesso condicional não será aplicada aos usuários finais que estão na implantação local.

## <a name="requirements-for-sharepoint-online"></a>Requisitos para o SharePoint Online
O Acesso condicional ao SharePoint Online dá suporte a dispositivos que executam:
 -   Windows 8.1 e posterior (quando registrado com o Intune)
 -   Windows 7.0 ou Windows 8.1 (quando ingressado no domínio)
 -   Windows Phone 8.1 e posterior
 -   iOS 7.1 e posterior
 -   Android 4.0 e posterior, Samsung KNOX Standard 4.0 e posterior

 **Além disso**:
 -   Os dispositivos devem ser ingressados no local de trabalho, que registra o dispositivo com o AAD DRS (Serviço de registro de dispositivo do Active Directory do Azure).

 Os PCs ingressados no domínio devem ser registrados automaticamente no Active Directory do Azure por meio da política de grupo ou do MSI. A seção **Acesso condicional para PCs** neste tópico descreve todos os requisitos para habilitar o acesso condicional de um PC.

 O AAD DRS será ativado automaticamente para clientes do Intune e do Office 365. Clientes que já tiverem implantado o Serviço de Registro de Dispositivos do ADFS não verão dispositivos registrados no seu Active Directory local.
 -   Uma assinatura do SharePoint Online é necessária e os usuários devem ser licenciados para o SharePoint Online.

 ### <a name="conditional-access-for-pcs"></a>Acesso condicional para PCs

 É possível configurar o acesso condicional para PCs que executam aplicativos da área de trabalho do Office para acessar o **Exchange Online** e o **SharePoint Online** para PCs que atendam aos seguintes requisitos:
 -   O PC deve estar executando o Windows 7.0 ou Windows 8.1.
 -   O PC deve ser ingressado no domínio ou compatível.

 Para ser compatível, o computador deve ser registrado no Intune e obedecer às políticas.

 Para PCs ingressados no domínio, você deve configurá-lo para [registrar o dispositivo automaticamente](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) com o Active Directory do Azure.
 -   [A autenticação moderna do Office 365 deve estar habilitada](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)e ter todas as atualizações mais recentes do Office.<br />     A autenticação moderna leva as credenciais baseadas na ADAL (Active Directory Authentication Library) para os clientes do Windows com Office 2013 e permite uma melhor segurança como a **autenticação multifator**e a **autenticação baseada em certificado**.
 -   Configure as regras de declarações do ADFS para bloquear protocolos de autenticação não moderna.  

## <a name="next-steps"></a>Próximas etapas  
 Leia os tópicos a seguir para saber como configurar políticas de conformidade e políticas de acesso condicional para seu cenário necessário:  

-   [Gerenciar políticas de conformidade do dispositivo no System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)  

-   [Gerenciar acesso a email no System Center Configuration Manager](../../protect/deploy-use/manage-email-access.md)  

-   [Gerenciar o acesso ao SharePoint Online no System Center Configuration Manager](../../protect/deploy-use/manage-sharepoint-online-access.md)  

-   [Gerenciar o acesso do Skype for Business Online](../../protect/deploy-use/manage-skype-for-business-online-access.md)  

### <a name="see-also"></a>Consulte também  

 [Introdução às configurações de conformidade no System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md)

