---
title: "Configurar o gerenciamento de dispositivo híbrido do Windows com o System Center Configuration Manager e o Microsoft Intune | Microsoft Docs"
description: "Configurar o gerenciamento do dispositivo Windows híbrido com o System Center Configuration Manager e o Microsoft Intune."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 76cb0c41865859fd410a187435d73c6a23b0c57e
ms.openlocfilehash: 7b53b094eeb1d59d052c63831eeab0e10edb5913


---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar o gerenciamento de dispositivo híbrido do Windows com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode usar o Configuration Manager com o Intune para gerenciar computadores, laptops e outros dispositivos que executam o Windows como dispositivos móveis. Você pode configurar o Azure Active Directory para permitir o registro automático de computadores Windows. Você também pode configurar o Configuration Manager para simplificar o registro usando o aplicativo do Portal da Empresa.


As opções de registro do Windows incluem:

- [Registro automático com o Azure AD](#azure-active-directory-enrollment)
- [Computadores Windows](#set-up-windows-device-enrollment)
- [Dispositivos Windows Mobile 10 e Windows Phone](#enable-windows-phone-devices)

## <a name="azure-active-directory-enrollment"></a>Registro no Azure Active Directory

O registro automático permite que os usuários registrem computadores com Windows 10 e dispositivos com Windows 10 Mobile pessoais ou da empresa no Intune adicionando uma conta corporativa ou de estudante e concordando em ser gerenciado. Em segundo plano, o dispositivo do usuário registra-se e ingressa no Azure Active Directory. Depois de registrado, o dispositivo pode ser gerenciado com o Intune.

**Pré-requisitos**
- Assinatura do Azure Active Directory Premium ([assinatura de avaliação](http://go.microsoft.com/fwlink/?LinkID=816845))
- Assinatura do Microsoft Intune


### <a name="configure-automatic-mdm-enrollment"></a>Configurar o registro automático do MDM

1. No [Portal de Gerenciamento do Azure](https://manage.windowsazure.com) (https://manage.windowsazure.com), navegue até o nó **Active Directory** e selecione o diretório.

2. Clique na guia **Aplicativos** e você verá **Microsoft Intune** na lista de aplicativos.

    ![Aplicativos Azure AD com o Microsoft Intune](../media/aad-intune-app.png)

3. Clique na seta para **Microsoft Intune** e você verá uma página que permite configurar o Microsoft Intune.

4. Clique em **Configurar** para começar a configurar o registro automático do MDM com o Microsoft Intune.

5. Especifique as URLs para o Intune:

  - **URL de Conformidade do MDM**: use o valor padrão.
  - **URL de Termos de Uso do MDM** – Use o valor padrão. Essa URL exibe os termos de uso para os usuários ao registrar dispositivos.
  - **URL de Conformidade do MDM** – Use o valor padrão. Se um dispositivo não estiver em conformidade, uma mensagem de **Acesso negado** será exibida com essa URL. A URL aponta para uma página que ajuda os usuários a entenderem por que o dispositivo não é compatível com a política e como eles podem deixá-lo em conformidade novamente.

6.  Especifique quais dispositivos dos usuários devem ser gerenciados pelo Microsoft Intune. Os dispositivos do Windows 10 desses usuários serão automaticamente registrados para gerenciamento com o Microsoft Intune.

  - **Todos**
  - **Grupos**
  - **Nenhum**

7. Escolha **Salvar**.

## <a name="configure-windows-pc-enrollment"></a>Configurar o registro de computador Windows
 Para habilitar o gerenciamento de dispositivo móvel do Windows, você precisa habilitar o gerenciamento do sistema operacional.  Você também pode adicionar um DNS CNAME para simplificar o registro para os usuários.

### <a name="create-dns-alias-for-device-enrollment"></a>Criar o alias DNS para registro de dispositivo  
 Um alias DNS (tipo de registro CNAME) facilita o registro dos dispositivos para os usuários ao popular automaticamente o nome do servidor durante o registro do dispositivo. Para criar um alias DNS (tipo de registro CNAME), você precisa configurar um CNAME nos registros DNS da sua empresa que redirecione as solicitações enviadas a uma URL no domínio da empresa para os servidores de serviço de nuvem da Microsoft.  Por exemplo, se o domínio da sua empresa for contoso.com, você deverá criar um CNAME no DNS que redirecione EnterpriseEnrollment.contoso.com para EnterpriseEnrollment-s.manage.microsoft.com.  

 Embora a criação de entradas de DNS de CNAME seja opcional, os registros CNAME facilitam o registro para os usuários. Se não for possível encontrar nenhum registro CNAME no registro, os usuários deverão inserir manualmente o nome do servidor MDM: https://enrollment.manage.microsoft.com.

|Tipo|Nome do host|Aponta para|  
|----------|---------------|---------------|  
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com|  
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|  
### <a name="to-enable-enrollment-for-windows-devices"></a>Para habilitar o registro para dispositivos Windows  

1.  **Pré-requisitos** – Antes de configurar o registro para qualquer plataforma, conclua os pré-requisitos e os procedimentos em [Configurar MDM híbrido](setup-hybrid-mdm.md).  

2.  No console do Configuration Manager, no espaço de trabalho **Administração** , acesse **Serviços de Nuvem** > **Assinaturas do Microsoft Intune**.  

    > [!WARNING]  
    >  Se outras caixas de diálogo do Configuration Manager forem abertas, feche-as antes de continuar com este procedimento.  

3.  Na guia **Início** , clique em **Configurar Plataformas**e depois clique em **Windows**.  

4.  Na guia **Geral** , selecione **Habilitar registro do Windows**.  

 Depois da configuração, você precisará permitir que os usuários saibam como registrar seus dispositivos. Consulte [O que dizer aos usuários sobre o registro de seus dispositivos](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Essas informações se aplicam a dispositivos móveis gerenciados pelo Microsoft Intune e pelo Configuration Manager.

## <a name="enable-windows-phone-devices"></a>Habilitar dispositivos Windows Phone  
  Se os usuários forem registrar somente o Windows Phone 8.1 e os dispositivos posteriores e se você não for implantar aplicativos de linha de negócios para dispositivos Windows Phone, nenhum certificado da Symantec será necessário. Depois de habilitar o registro do Windows Phone, você deve instruir os usuários a instalarem o aplicativo Portal da Empresa da Windows Phone Store para registrar seus dispositivos.  

  Conclua as etapas a seguir para os dispositivos com Windows Phone que você gerenciará.  

### <a name="to-enable-enrollment-for-windows-phone-81-and-later-devices"></a>Para habilitar o registro para Windows Phone 8.1 e dispositivos posteriores  

 1.  **Pré-requisitos** – Antes de configurar o registro para qualquer plataforma, conclua os pré-requisitos e os procedimentos em [Configurar MDM híbrido](setup-hybrid-mdm.md).  

 2.  No console do Configuration Manager, no espaço de trabalho **Administração** , acesse **Serviços de Nuvem** > **Assinaturas do Microsoft Intune**.  

     > [!WARNING]  
     >  Se outras caixas de diálogo do Configuration Manager forem abertas, feche-as antes de continuar com este procedimento.  

 3.  Na guia **Início** , clique em **Configurar Plataformas**e depois clique em **Windows Phone**.  

 4.  Na guia **Geral** , escolha  **Windows Phone 8.1 e Windows 10 Mobile**. Você pode carregar os dados do aquivo .xml AET ou um arquivo .pfx para permitir a implantação do Portal da Empresa, ou instruir os usuários a baixar o Portal da Empresa na Loja do Windows Phone.  

      Clique em **OK**.  

  Depois da configuração, você precisará permitir que os usuários saibam como registrar seus dispositivos. Consulte [O que dizer aos usuários sobre o registro de seus dispositivos](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Essas informações se aplicam a dispositivos móveis gerenciados pelo Microsoft Intune e pelo Configuration Manager.  



<!--HONumber=Feb17_HO2-->


