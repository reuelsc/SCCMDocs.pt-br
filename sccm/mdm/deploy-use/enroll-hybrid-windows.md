---
title: "Configurar o gerenciamento de dispositivo híbrido do Windows com o System Center Configuration Manager e o Microsoft Intune | Microsoft Docs"
description: "Configurar o gerenciamento do dispositivo Windows híbrido com o System Center Configuration Manager e o Microsoft Intune."
ms.custom: na
ms.date: 03/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: 4189fe34efc2ae134150a89791dc10bbab1b9d02
ms.lasthandoff: 03/17/2017


---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar o gerenciamento de dispositivo híbrido do Windows com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico informa aos administradores de TI, como eles podem permitir que seus usuários tragam os PCs com Windows e dispositivos móveis para o gerenciamento usando o Gerenciador de Configuração e o Microsoft Intune. Existem dois métodos de registro:
-  O registro automático do Azure Active Directory (AD) quando os usuários conectam a sua conta a um dispositivo
- Registro por instalação e inscrição no aplicativo de Portal da empresa

## <a name="choose-how-to-enroll-windows-devices"></a>Escolha como registrar os dispositivos Windows

Dois fatores determinam como você vai registrar os dispositivos Windows:
- **Você usa o Azure Active Directory Premium?** <br>[O Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) está incluído no Enterprise Mobility + Security e outros planos de licenciamento.
- **Quais versões de clientes Windows serão registradas?** <br>Dispositivos Windows 10 podem registrar automaticamente adicionando uma conta corporativa ou escolar. Versões anteriores devem ser registrados usando o aplicativo de Portal da Empresa.

||**Azure AD Premium**|**Outro AD**|
|----------|---------------|---------------|  
|**Windows 10**|[Registro automático](#automatic-enrollment) |[Registro do Portal da Empresa](#company-portal-enrollment)|
|**Versões anteriores do Windows**|[Registro do Portal da Empresa](#company-portal-enrollment)|[Registro do Portal da Empresa](#company-portal-enrollment)|

## <a name="automatic-enrollment"></a>Registro automático

O registro automático permite que os usuários registrem computadores da empresa ou dispositivos pessoais com Windows 10, adicionando uma conta corporativa ou de estudante e concordando em ser gerenciado. Em segundo plano, o dispositivo do usuário registra-se e ingressa no Azure Active Directory. Depois de registrado, o dispositivo pode ser gerenciado com o Intune. Dispositivos gerenciados ainda podem usar o Portal da empresa para tarefas, mas não é necessário instalá-lo para ser registrado.

**Pré-requisitos**
- Assinatura do Azure Active Directory Premium ([assinatura de avaliação](http://go.microsoft.com/fwlink/?LinkID=816845))
- Assinatura do Microsoft Intune

### <a name="configure-automatic-enrollment"></a>Configurar o registro automático

1. Entre no [portal do Azure](https://manage.windowsazure.com), navegue até o nó do **Active Directory** no painel esquerdo e selecione o diretório.
2. Selecione a guia **Configurar** e role até a seção chamada **Dispositivos**.
3. Selecione **Todos** para **Usuários podem unir dispositivos de área de trabalho**.
4. Selecione o número máximo de dispositivos que deseja autorizar por usuário.

Por padrão, autenticação de dois fatores não está habilitada para o serviço. No entanto, a autenticação de dois fatores é recomendável ao registrar um dispositivo. Antes de solicitar a autenticação de dois fatores para esse serviço, você deve configurar um provedor de autenticação de dois fatores no Azure Active Directory e configurar suas contas de usuário para autenticação multifator. Consulte [Guia de Introdução com o servidor de autenticação multifator do Azure](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).

## <a name="company-portal-enrollment"></a>Registro do Portal da Empresa
Os usuários finais ou um [gerenciador de registro de dispositivo](enroll-devices-with-device-enrollment-manager.md) pode registrar dispositivos Windows instalando o aplicativo de Portal da Empresa e, em seguida, entre com suas credenciais de trabalho. Para simplificar o registro para seus usuários finais, você deve adicionar um CNAME em seu registro de DNS.

### <a name="enable-windows-device-management"></a>Habilite o gerenciamento do dispositivo Windows
Para habilitar o gerenciamento de dispositivos do Windows para PCs ou dispositivos móveis, use as seguintes etapas:

1.  Antes de configurar o registro para qualquer plataforma, conclua os pré-requisitos e os procedimentos em [Configurar MDM híbrido](setup-hybrid-mdm.md).  
2.  No console do Gerenciador de Configuração, no espaço de trabalho **Administração**, acesse **Visão Geral** > **Serviços de Nuvem** > **Assinaturas do Microsoft Intune**.  
3.  Na faixa de opções, escolha **Configurar Plataformas** e clique na plataforma Windows:
    - **Windows** para Windows PCs e laptops, em seguida, execute as seguintes etapas:
      1. Na guia **Geral**, selecione **Habilitar registro do Windows**.
      2. Se você usa um certificado de assinatura de código e implantar o aplicativo de Portal da Empresa, navegue até o **certificado de assinatura de código**. Os usuários de dispositivo também podem instalar o aplicativo de Portal da empresa na Windows Store ou você pode implantar o aplicativo da Windows Store para Empresas sem assinatura de código.
      3. Você também pode configurar as [configurações do Windows Hello para Empresas](windows-hello-for-business-settings.md).
    - **Windows Phone** para telefones e tablets com Windows, em seguida, execute as seguintes etapas:
      1. Na guia **Geral**, clique em **Windows Phone 8.1 e Windows 10 Mobile**. Não há suporte para o Windows Phone 8.0.
      2. Se sua organização precisa carregar aplicativos da empresa, você pode carregar o arquivo ou o token necessário. Para obter mais informações sobre aplicativos de sideload, consulte [Criar aplicativos para Windows](https://docs.microsoft.com/sccm/apps/get-started/creating-windows-applications).
        - **Token de registro de aplicativo**
        - **arquivo .pfx**
        - **Nenhum** se você usar um certificado da Symantec, você poderá especificar **mostrar um alerta antes de expirarem os certificados da Symantec**.
4. Clique em **OK** para fechar a caixa de diálogo.  Para simplificar o processo de registro usando o Portal da Empresa, você deve criar um alias DNS para o registro do dispositivo. Em seguida, você pode dizer aos usuários como registrar seus dispositivos.

### <a name="create-dns-alias-for-device-enrollment"></a>Criar o alias DNS para registro de dispositivo  
Um DNS alias (tipo de registro CNAME) facilita para os usuários registrem seus dispositivos ao se conectar ao serviço sem exigir que o usuário insira um endereço de servidor. Para criar um alias DNS (tipo de registro CNAME), você deve configurar um CNAME nos registros DNS da sua empresa que redirecione as solicitações enviadas a uma URL no domínio da empresa para os servidores de serviço de nuvem da Microsoft.  Por exemplo, se o domínio da sua empresa for contoso.com, você deverá criar um CNAME no DNS que redirecione EnterpriseEnrollment.contoso.com para EnterpriseEnrollment-s.manage.microsoft.com.  

 Embora a criação de entradas de DNS de CNAME seja opcional, os registros CNAME facilitam o registro para os usuários. Se não for possível encontrar nenhum registro CNAME no registro, os usuários deverão inserir manualmente o nome do servidor MDM: https://enrollment.manage.microsoft.com.

|Tipo|Nome do host|Aponta para|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hora|

Se você tiver mais de um sufixo UPN, você precisará criar um CNAME para cada nome de domínio e apontar cada um para EnterpriseEnrollment-s.manage.microsoft.com. Por exemplo, se os usuários da Contoso usarem name@contoso.com, mas também usarem name@us.contoso.com e name@eu.constoso.com como seu email/UPN, o administrador de DNS da Contoso precisará criar os seguintes CNAMEs.

|Tipo|Nome do host|Aponta para|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hora|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hora|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hora|

## <a name="tell-users-how-to-enroll-devices"></a>Informe aos usuários para registrarem os dispositivos  

 Depois da configuração, você precisará permitir que os usuários saibam como registrar seus dispositivos. Consulte [O que dizer aos usuários sobre o registro de seus dispositivos](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune) para obter diretrizes. Você pode direcionar os usuários para [registrar seu dispositivo Windows no Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows). Essas informações se aplicam a dispositivos móveis gerenciados pelo Microsoft Intune e pelo Configuration Manager.

> [!div class="button"]
[< Etapa anterior](create-service-connection-point.md)  [Próxima etapa >](set-up-additional-management.md)

