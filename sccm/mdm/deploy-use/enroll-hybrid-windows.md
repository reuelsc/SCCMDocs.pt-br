---
title: Configurar o gerenciamento do dispositivo híbrido do Windows com o Microsoft Intune
titleSuffix: Configuration Manager
description: Configurar o gerenciamento do dispositivo Windows híbrido com o System Center Configuration Manager e o Microsoft Intune.
ms.date: 03/17/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7811e1ab4a323660f16b707076015d9e81bda2bb
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121287"
---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar o gerenciamento de dispositivo híbrido do Windows com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico informa aos administradores de TI, como eles podem permitir que seus usuários tragam os PCs com Windows e dispositivos móveis para o gerenciamento usando o Gerenciador de Configuração e o Microsoft Intune.

## <a name="enable-windows-device-management"></a>Habilite o gerenciamento do dispositivo Windows
Para habilitar o gerenciamento de dispositivos do Windows para PCs ou dispositivos móveis, use as seguintes etapas:

1. Antes de configurar o registro para qualquer plataforma, conclua os pré-requisitos e os procedimentos em [Configurar MDM híbrido](setup-hybrid-mdm.md).  
2. No console do Gerenciador de Configuração, no workspace **Administração**, acesse **Visão Geral** > **Serviços de Nuvem** > **Assinaturas do Microsoft Intune**.  
3. Na faixa de opções, escolha **Configurar Plataformas** e clique na plataforma Windows:
   - **Windows** para Windows PCs e laptops, em seguida, execute as seguintes etapas:
     1. Na guia **Geral**, selecione **Habilitar registro do Windows**.
     2. Se você usa um certificado de assinatura de código e implantar o aplicativo de Portal da Empresa, navegue até o **certificado de assinatura de código**. Os usuários de dispositivos também podem instalar o aplicativo do Portal da Empresa por meio da Microsoft Store ou você pode implantar o aplicativo da Microsoft Store para Empresas sem assinatura de código.
     3. Você também pode configurar as [configurações do Windows Hello para Empresas](windows-hello-for-business-settings.md).
   - **Windows Phone** para telefones e tablets com Windows, em seguida, execute as seguintes etapas:
     1. Na guia **Geral**, clique em **Windows Phone 8.1 e Windows 10 Mobile**. Não há suporte para o Windows Phone 8.0.
     2. Se sua organização precisa carregar aplicativos da empresa, você pode carregar o arquivo ou o token necessário. Para obter mais informações sobre aplicativos de sideload, consulte [Criar aplicativos para Windows](https://docs.microsoft.com/sccm/apps/get-started/creating-windows-applications).
        - **Token de registro de aplicativo**
        - **arquivo .pfx**
        - **Nenhum** se você usar um certificado da Symantec, você poderá especificar **mostrar um alerta antes de expirarem os certificados da Symantec**.
4. Clique em **OK** para fechar a caixa de diálogo.  Para simplificar o processo de registro usando o Portal da Empresa, você deve criar um alias DNS para o registro do dispositivo. Em seguida, você pode dizer aos usuários como registrar seus dispositivos.

## <a name="choose-how-to-enroll-windows-devices"></a>Escolha como registrar os dispositivos Windows

Depois de atribuir licenças do Intune aos usuários, os dispositivos Windows poderão ser registrados sem etapas adicionais, mas você pode facilitar o registro para os usuários.

Dois fatores determinam como você pode simplificar o registro do dispositivo do Windows:
- **Você usa o Azure Active Directory Premium?** <br>[O Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) está incluído no Enterprise Mobility + Security e outros planos de licenciamento.
- **Quais versões de clientes Windows serão registradas?** <br>Dispositivos Windows 10 podem registrar automaticamente adicionando uma conta corporativa ou escolar. Versões anteriores devem ser registrados usando o aplicativo de Portal da Empresa.

||**Azure AD Premium**|**Outro AD**|
|----------|---------------|---------------|  
|**Windows 10**|[Registro automático](#enable-windows-10-automatic-enrollment) |[Registro de usuário](#enable-windows-enrollment-without-azure-ad-premium)|
|**Versões anteriores do Windows**|[Registro de usuário](#enable-windows-enrollment-without-azure-ad-premium)|[Registro de usuário](#enable-windows-enrollment-without-azure-ad-premium)|

## <a name="enable-windows-10-automatic-enrollment"></a>Habilitar o registro automático do Windows 10

O registro automático permite que os usuários registrem os PCs e dispositivos móveis com Windows 10 pessoais ou da empresa no Intune adicionando uma conta corporativa ou de estudante, e concordando em ser gerenciados. Simples assim. Em segundo plano, o dispositivo do usuário registra-se e ingressa no Azure Active Directory. Depois de registrado, o dispositivo é gerenciado com o Intune.

**Pré-requisitos**
- Assinatura do Azure Active Directory Premium ([assinatura de avaliação](http://go.microsoft.com/fwlink/?LinkID=816845))
- Assinatura do Microsoft Intune


### <a name="configure-automatic-mdm-enrollment"></a>Configurar o registro automático do MDM

1. Entre no [Portal de Gerenciamento do Azure](https://portal.azure.com) (https://manage.windowsazure.com) e selecione **Azure Active Directory**.

   ![Captura de tela do portal do Azure](../media/auto-enroll-azure-main.png)

2. Selecione **Mobilidade (MDM e MAM)**.

   ![Captura de tela do portal do Azure](../media/auto-enroll-mdm.png)

3. Selecione **Microsoft Intune**.

   ![Captura de tela do portal do Azure](../media/auto-enroll-intune.png)

4. Configure o **escopo do Usuário MDM**. Especifique quais dispositivos dos usuários devem ser gerenciados pelo Microsoft Intune. Os dispositivos do Windows 10 desses usuários serão automaticamente registrados para gerenciamento com o Microsoft Intune.

    - **Nenhum**
    - **Alguns**
    - **Todos**

   ![Captura de tela do portal do Azure](../media/auto-enroll-scope.png)

5. Use os valores padrão para as seguintes URLs:
    - **URL dos termos de uso MDM**
    - **URL de Descoberta do MDM**
    - **URL de Conformidade do MDM**

6. Selecione **Salvar**.


Por padrão, autenticação de dois fatores não está habilitada para o serviço. No entanto, a autenticação de dois fatores é recomendável ao registrar um dispositivo. Antes de solicitar a autenticação de dois fatores para esse serviço, você deve configurar um provedor de autenticação de dois fatores no Azure Active Directory e configurar suas contas de usuário para autenticação multifator. Consulte [Guia de Introdução com o servidor de autenticação multifator do Azure](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).

## <a name="enable-windows-enrollment-without-azure-ad-premium"></a>Habilitar o registro do Windows sem o Azure AD Premium
Você pode permitir que os usuários registrem seus dispositivos sem o registro automático do Azure AD Premium. Depois de atribuir as licenças, os usuários poderão registrar depois de adicionar sua conta de trabalho aos seus dispositivos pessoais ou ingressar seus dispositivos corporativos no Azure AD. Criar um alias DNS (tipo de registro CNAME) facilita que os usuários registrem seus dispositivos. Se você criar registros de recursos DNS CNAME, os usuários irão conectar-se e registrar-se no Intune sem precisarem digitar o nome do servidor Intune.

### <a name="create-cnames-to-simplify-enrollment"></a>Criar CNAMEs para simplificar o registro
Crie registros de recursos DNS CNAME para o domínio de sua empresa. Por exemplo, se o site da empresa fosse contoso.com, você criaria um CNAME no DNS que redirecione EnterpriseEnrollment.contoso.com para enterpriseenrollment-s.manage.microsoft.com.

Embora a criação de entradas de DNS de CNAME seja opcional, os registros CNAME facilitam o registro para os usuários. Se não for possível encontrar nenhum registro CNAME no registro, os usuários deverão inserir manualmente o nome do servidor MDM enrollment.manage.microsoft.com.

|Digite|Nome do host|Aponta para|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hora|

Se você tiver mais de um sufixo UPN, você precisará criar um CNAME para cada nome de domínio e apontar cada um para EnterpriseEnrollment-s.manage.microsoft.com. Por exemplo, se os usuários da Contoso usarem name@contoso.com, mas também usarem name@us.contoso.com e name@eu.constoso.com como seu email/UPN, o administrador de DNS da Contoso precisará criar os seguintes CNAMEs.

|Digite|Nome do host|Aponta para|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hora|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hora|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hora|

`EnterpriseEnrollment-s.manage.microsoft.com` – Dá suporte ao redirecionamento para o serviço Intune com o reconhecimento de domínio a partir do nome de domínio do email

As alterações nos registros DNS podem levar até 72 horas para serem propagadas. Você não pode verificar a alteração do DNS no Intune até o registro DNS propagar.

## <a name="tell-users-how-to-enroll-devices"></a>Informe aos usuários para registrarem os dispositivos  

 Depois da configuração, você precisará permitir que os usuários saibam como registrar seus dispositivos. Consulte [O que dizer aos usuários sobre o registro de seus dispositivos](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune) para obter diretrizes. Você pode direcionar os usuários para [registrar seu dispositivo Windows no Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows). Essas informações se aplicam a dispositivos móveis gerenciados pelo Microsoft Intune e pelo Configuration Manager.

> [!div class="button"]
> [< Etapa anterior](create-service-connection-point.md)  [Próxima etapa >](set-up-additional-management.md)
