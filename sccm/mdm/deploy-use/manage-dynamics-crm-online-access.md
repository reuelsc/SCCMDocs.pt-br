---
title: Gerenciar o acesso ao Dynamics CRM Online | Microsoft Docs
description: Saiba como controlar o acesso ao Microsoft Dynamics CRM Online de dispositivos iOS e Android com acesso condicional do Microsoft Intune.
ms.custom: na
ms.date: 03/05/2017
ms.reviewer: na
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bfc4c51-b25c-4c70-b81e-8a3b6ddf02c8
caps.latest.revision: "5"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: bd00f12ae3bc14a34d24c22c3d5277d275d51e85
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="manage-dynamics-crm-online-access-in-system-center-configuration-manager"></a>Gerenciar o acesso ao Dynamics CRM Online no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode controlar o acesso ao Microsoft Dynamics CRM Online de dispositivos iOS e Android com acesso condicional do Microsoft Intune.  O acesso condicional do Intune tem dois componentes:
* [Política de conformidade do dispositivo](../../protect/deploy-use/device-compliance-policies.md) que o dispositivo deve cumprir para ser considerado compatível.
* [Política de acesso condicional](../../protect/deploy-use/manage-access-to-services.md) na qual você especifica as condições que o dispositivo deve atender para acessar o serviço.

Para saber mais sobre como funciona o acesso condicional, leia o artigo [Gerenciar o acesso a serviços](../../protect/deploy-use/manage-access-to-services.md).


Quando determinado usuário tentar usar o aplicativo Dynamics CRM em seu dispositivo, a seguinte avaliação ocorrerá:

![O diagrama mostra os pontos de decisão usados para determinar se um dispositivo tem acesso permitido a um serviço ou está bloqueado](media/mdm-ca-dynamics-crm-flow-diagram.png)

O dispositivo que precisa acessar o Dynamics CRM Online deve:
* Ser um dispositivo **Android** ou **iOS**.
* Ser **registrado** no Microsoft Intune.
* Ser **compatível** com qualquer política de conformidade do Microsoft Intune implantada.

O estado do dispositivo é armazenado no Azure Active Directory que concede ou bloqueia o acesso, com base nas condições que você especifica.

Se uma condição não for atendida, o usuário receberá uma das seguintes mensagens de erro ao fazer logon:
* Se o dispositivo não estiver registrado no Microsoft Intune ou não estiver registrado no Azure Active Directory, será exibida uma mensagem com instruções sobre como instalar o aplicativo do portal da empresa e registrá-lo.
* Se o dispositivo não for compatível, será exibida uma mensagem que direciona o usuário ao site do Portal da Empresa do Microsoft Intune ou ao aplicativo Portal da Empresa, em que ele pode encontrar informações sobre o problema e como corrigi-lo.

## <a name="configure-conditional-access-for-dynamics-crm-online"></a>Configurar o acesso condicional do Dynamics CRM Online  
### <a name="step-1-configure-active-directory-security-groups"></a>Etapa 1: Configurar grupos de segurança do Active Directory

Antes de começar, configure os grupos de segurança do Active Directory do Azure para a política de acesso condicional. Você pode configurar esses grupos no **Centro de administração do Office 365**. Esses grupos serão usado para o destino ou usuários isentos da política. Quando um usuário é afetado por uma política, cada dispositivo que ele usa deve ser compatível para que possa acessar os recursos.

Você pode especificar dois tipos de grupo para a política do Dynamics CRM:
* **Grupos de destino** – Contém grupos de usuários aos quais a política será aplicada.
* **Grupos isentos** – Contém grupos de usuários isentos da política.

Se um usuário estiver nos dois grupos, ele ficará isento da política.

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Etapa 2: Configurar e implantar uma política de conformidade
[Crie e implante](../../protect/deploy-use/device-compliance-policies.md) uma política de conformidade para todos os dispositivos que serão afetados pela política. Esses seriam todos os dispositivos usados pelos usuários nos grupos de destino.

> [!NOTE]
> Enquanto as políticas de conformidade são implantadas em grupos do Microsoft Intune, as políticas de acesso condicional são destinadas a grupos de segurança do Azure Active Directory.

> [!IMPORTANT]
> Se você não tiver implantado uma política de conformidade, os dispositivos serão tratados como compatíveis.

Quando estiver pronto, continue na Etapa 3.
### <a name="step-3-configure-the-dynamics-crm-policy"></a>Etapa 3: Configurar a política do Dynamics CRM
Em seguida, configure a política para exigir que somente dispositivos gerenciados e compatíveis possam acessar o Dynamics CRM. Essa política será armazenada no Active Directory do Azure.

1.  No Console de administração do Microsoft Intune, escolha **Política > Acesso Condicional > Política do Dynamics CRM Online**.

     ![Captura de tela da página de política de acesso condicional do Dynamics CRM Online](media/mdm-ca-dynamics-crm-policy-configuration.png)

2.  Selecione **Habilitar a política de acesso condicional**.
3.  Em **Acesso do aplicativo**, você pode optar por aplicar a política de acesso condicional a:
  * **iOS**
  * **Android**
4.  Em **Grupos de Destino**, escolha **Modificar** para selecionar os grupos de segurança do Azure Active Directory aos quais a política será aplicada. Você pode escolher aplicar isso a todos os usuários ou apenas a um grupo seleto de usuários.
5.  Opcionalmente, em **Grupos Isentos**, escolha em **Modificar** para selecionar os grupos de segurança do Azure Active Directory que são isentos dessa política.
6.  Quando terminar, escolha **Salvar**.

Você configurou o acesso condicional para o Dynamics CRM. Você não precisa implantar a política de acesso condicional, ele entra em vigor imediatamente.
##  <a name="monitor-the-compliance-and-conditional-access-policies"></a>Monitorar a conformidade e políticas de acesso condicional

No espaço de trabalho **Grupos**, você pode exibir o status de acesso condicional de seus dispositivos.

Selecione qualquer grupo de dispositivos móveis e, na guia **Dispositivos** , selecione um dos seguintes **Filtros**:
* **Dispositivos que não estão registrados no AAD** – esses dispositivos estão bloqueados do Dynamics CRM.
* **Dispositivos que não são compatíveis** – esses dispositivos estão bloqueados do Dynamics CRM.
* **Dispositivos que estão registrados no AAD e são compatíveis** – esses dispositivos podem acessar o Dynamics CRM.

###  <a name="see-also"></a>Consulte também
[Gerenciar acesso ao email](../../protect/deploy-use/manage-email-access.md)

[Gerenciar acesso ao SharePoint Online](../../protect/deploy-use/manage-sharepoint-online-access.md)

[Gerenciar acesso ao Skype for Business Online](../../protect/deploy-use/manage-skype-for-business-online-access.md)
