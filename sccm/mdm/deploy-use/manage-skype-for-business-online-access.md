---
title: Gerenciar o acesso do Skype for Business Online | Microsoft Docs
description: "Saiba como usar a política de acesso condicional para gerenciar o acesso ao Skype for Business Online."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71c44250-626e-482c-8794-434c6aeb2fb1
caps.latest.revision: "6"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: cacb22a85e74a7d9cae75ad907d0206487cd4dc7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="manage-skype-for-business-online-access"></a>Gerenciar o acesso do Skype for Business Online

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Use a política de acesso condicional para o  **Skype for Business Online** para gerenciar o acesso ao Skype for Business Online, com base nas condições que você especificar.  


 Quando um determinado usuário tentar usar o Skype for Business Online em seu dispositivo, a seguinte avaliação ocorrerá:![ConditionalAccess&#95;SFBFlow](media/ConditionalAccess_SFBFlow.png)  

## <a name="prerequisites"></a>Pré-requisitos  

-   Habilitar a autenticação moderna para o Skype for Business Online. Preencha este [formulário do Connect](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) para ser registrado no programa de autenticação moderna.  

-   Todos os usuários finais deverão usar o Skype for Business Online. Se você tiver uma implantação com o Skype for Business Online e o Skype for Business local, a política de acesso condicional não será aplicada aos usuários finais.  

-   O dispositivo que precisa acessar Skype for Business Online deve:  

    -   Ser um dispositivo Android ou iOS.  

    -   Estar registrado no Intune.  

    -   Ser compatível com qualquer política de conformidade do Intune implantada.  

 O estado do dispositivo é armazenado no Azure Active Directory que concede ou bloqueia o acesso, com base nas condições que você especifica.  
Se uma condição não for atendida, o usuário receberá uma das seguintes mensagens de erro ao fazer logon:  

-   Se o dispositivo não estiver registrado no Intune ou não estiver registrado no Azure Active Directory, será exibida uma mensagem com instruções sobre como instalar o aplicativo do portal da empresa e registrá-lo.  

-   Se o dispositivo não for compatível, será exibida uma mensagem que direciona o usuário ao site do Portal da Empresa do Intune ou ao aplicativo Portal da Empresa, onde ele pode encontrar informações sobre o problema e como corrigi-lo.  

## <a name="configure-conditional-access-for-skype-for-business-online"></a>Configurar o acesso condicional para o Skype for Business Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Etapa 1: Configurar grupos de segurança do Active Directory  
 Antes de começar, configure os grupos de segurança do Active Directory do Azure para a política de acesso condicional. Você pode configurar esses grupos no Centro de administração do Office 365. Esses grupos contêm os usuários que serão afetados ou que ficarão isentos da política. Quando um usuário é afetado por uma política, cada dispositivo que ele usa deve ser compatível para que possa acessar os recursos.  

 Você pode especificar dois tipos de grupo para uso com a política do Skype for Business:  

-   Grupos de destino â€“ Contém grupos de usuários aos quais a política será aplicada  

-   Grupos isentos â€“ Contém grupos de usuários isentos da política (opcional)  
    Se um usuário estiver nos dois grupos, ele ficará isento da política.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Etapa 2: Configurar e implantar uma política de conformidade  
 Certifique-se de criar e implantar uma política de conformidade para todos os dispositivos aos quais a política do Skype for Business Online se destinará.  

 Para obter detalhes sobre como configurar a política de conformidade, consulte [Gerenciar políticas de conformidade do dispositivo no System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md).  

> [!NOTE]  
>  Se você não tiver implantado uma política de conformidade e habilitar a política do Skype for Business Online, todos os dispositivos de destino terão acesso permitido se estiverem registrados no Intune.  

 Quando estiver pronto, continue na Etapa 3.  

### <a name="step-3-configure-the-skype-for-business-online-policy"></a>Etapa 3: Configurar a política do Skype for Business Online  
 Em seguida, configure a política para exigir que somente dispositivos gerenciados e compatíveis possam acessar o Skype for Business Online. Essa política será armazenada no Active Directory do Azure.  

1.  No [Console de Administração do Microsoft Intune](https://manage.microsoft.com), clique em **Política** > **Acesso Condicional** > **Skype for Business Online Política**.  

     ![ConditionalAccess&#95;SFBPolicy](media/ConditionalAccess_SFBPolicy.png)  

2.  Selecione **Habilitar a política de acesso condicional**.  

3.  Em **Acesso do aplicativo**, você pode optar por aplicar a política de acesso condicional a:  

    -   iOS  

    -   Android  

4.  Em **Grupos de Destino**, clique em **Modificar** para selecionar os grupos de segurança do Active Directory do Azure aos quais a política será aplicada. Você pode escolher aplicar isso a todos os usuários ou apenas a um grupo seleto de usuários.  

5.  Opcionalmente, em **Grupos isentos**, clique em **Modificar** para selecionar os grupos de segurança do Active Directory do Azure que são isentos dessa política.  

6.  Quando terminar, clique em **Salvar**.  

 Você configurou o acesso condicional para o Skype for Business Online. Você não precisa implantar a política de acesso condicional, ele entra em vigor imediatamente.  

## <a name="monitor-the-compliance-and-conditional-access-policies"></a>Monitorar a conformidade e políticas de acesso condicional  
 No espaço de trabalho Grupos, você pode exibir o status de acesso condicional de seus dispositivos.  

 Selecione qualquer grupo de dispositivos móveis e, na guia **Dispositivos** , selecione um dos seguintes **Filtros**:  

-   **Dispositivos não registrados com o AAD** â€“ Esses dispositivos estão bloqueados no Skype for Business Online.  

-   **Dispositivos que não são compatíveis** â€“ Esses dispositivos estão bloqueados no Skype for Business Online.  

-   **Dispositivos registrados com o AAD e que são compatíveis** â€“ Esses dispositivos podem acessar o Skype for Business Online.  

### <a name="see-also"></a>Consulte também  

 [Gerenciar políticas de conformidade do dispositivo no System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)
