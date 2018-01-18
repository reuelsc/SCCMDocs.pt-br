---
title: Gerenciar o acesso do Skype for Business Online
titleSuffix: Configuration Manager
description: "Saiba como usar a política de acesso condicional para gerenciar o acesso ao Skype for Business Online."
ms.custom: na
ms.date: 12/22/2017
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
ms.openlocfilehash: 3c1d0c84dc28fb886048cf8d7ea310c2b4dfc4aa
ms.sourcegitcommit: 92c3f916e6bbd35b6208463ff406e0247664543a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="manage-skype-for-business-online-access"></a>Gerenciar o acesso do Skype for Business Online

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Use a política de acesso condicional do Skype for Business Online para gerenciar o acesso ao Skype for Business Online, com base nas condições que você especificar.  


 Quando um determinado usuário tentar usar o Skype for Business Online em seu dispositivo, a seguinte avaliação ocorrerá:![ConditionalAccess&#95;SFBFlow](media/ConditionalAccess_SFBFlow.png)  

## <a name="prerequisites"></a>Pré-requisitos  

-   Habilite a [autenticação moderna](https://aka.ms/SkypeModernAuth) para o Skype for Business Online.   

-   Todos os usuários devem usar o Skype for Business Online. Se você tiver uma implantação com o Skype for Business Online e o Skype for Business local, a política de acesso condicional não será aplicada aos usuários locais.  

-   O dispositivo que precisa acessar Skype for Business Online deve:  

    -   Ser um dispositivo Android ou iOS

    -   Ser registrado no Microsoft Intune

    -   Estar em conformidade com qualquer política de conformidade do Microsoft Intune implantada

 O Azure Active Directory armazena o estado do dispositivo, que concede ou bloqueia o acesso de acordo com as condições especificadas.  
Se uma condição não for atendida, o usuário receberá uma das seguintes mensagens ao fazer logon:  

-   Se o dispositivo não estiver registrado no Microsoft Intune ou se não estiver registrado no Azure Active Directory, o usuário receberá instruções sobre como instalar o aplicativo do Portal da Empresa e registrá-lo.  

-   Se o dispositivo não estiver em conformidade, o usuário verá uma mensagem que o direcionará para o site do Portal da Empresa ou o aplicativo do Portal da Empresa. O Portal da Empresa contém informações sobre o problema e como corrigi-lo.  

## <a name="configure-conditional-access-for-skype-for-business-online"></a>Configurar o acesso condicional para o Skype for Business Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Etapa 1: Configurar grupos de segurança do Active Directory  
 Antes de começar, configure os grupos de segurança do Active Directory do Azure para a política de acesso condicional. Configure esses grupos no Centro de administração do Office 365. Esses grupos contêm os usuários a serem afetados pela política ou excluídos dela. Quando um usuário é afetado por uma política, cada dispositivo que ele usa deve ser compatível para que possa acessar os recursos.  

 Você pode especificar dois tipos de grupo para uso com a política do Skype for Business:  

-   **Grupos direcionados** contêm os usuários aos quais a política se aplica  

-   **Grupos isentos** contêm os usuários a serem excluídos da política  
    Se um usuário estiver nos dois grupos, ele será isento.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Etapa 2: Configurar e implantar uma política de conformidade  
 Crie e implante uma política de conformidade para todos os dispositivos aos quais a política do Skype for Business Online é direcionada.  

 Para obter detalhes sobre como configurar a política de conformidade, consulte [Gerenciar políticas de conformidade do dispositivo](../../protect/deploy-use/device-compliance-policies.md).  

> [!NOTE]  
>  Se você não implantou uma política de conformidade e, em seguida, habilitou a política do Skype for Business Online, todos os dispositivos direcionados terão acesso permitido se estiverem registrados no Microsoft Intune.  


### <a name="step-3-configure-the-skype-for-business-online-policy"></a>Etapa 3: Configurar a política do Skype for Business Online  
 Configure a política para exigir que somente dispositivos gerenciados e em conformidade possam acessar o Skype for Business Online. Essa política é armazenada no Azure Active Directory.  

1.  No [Console de Administração do Microsoft Intune](https://manage.microsoft.com), clique em **Política** > **Acesso Condicional** > **Skype for Business Online Política**.  

     ![ConditionalAccess&#95;SFBPolicy](media/ConditionalAccess_SFBPolicy.png)  

2.  Selecione **Habilitar a política de acesso condicional**.  

3.  Em **Acesso do aplicativo**, você pode optar por aplicar a política de acesso condicional a:  

    -   iOS  

    -   Android  

4.  Em **Grupos Direcionados**, clique em **Modificar** para selecionar os grupos de segurança do Azure Active Directory aos quais a política se aplica. Opte por direcionar essa política a todos os usuários ou apenas a um grupo seleto de usuários.  

5.  Opcionalmente, em **Grupos isentos**, clique em **Modificar** para selecionar os grupos de segurança do Azure Active Directory que são isentos dessa política.  

6.  Quando terminar, clique em **Salvar**.  

 Você configurou o acesso condicional para o Skype for Business Online. Você não precisa implantar a política de acesso condicional, ele entra em vigor imediatamente.  

## <a name="monitor-the-compliance-and-conditional-access-policies"></a>Monitorar a conformidade e políticas de acesso condicional  
 No espaço de trabalho Grupos, você pode exibir o status de acesso condicional de seus dispositivos.  

 Selecione qualquer grupo de dispositivos móveis e, na guia **Dispositivos** , selecione um dos seguintes **Filtros**:  

-   **Dispositivos não registrados no AAD** estão bloqueados no Skype for Business Online

-   **Dispositivos que não estão em conformidade** estão bloqueados no Skype for Business Online  

-   **Dispositivos registrados no AAD e que estão em conformidade** podem acessar o Skype for Business Online  

### <a name="see-also"></a>Consulte também  

 [Gerenciar políticas de conformidade do dispositivo no System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)
