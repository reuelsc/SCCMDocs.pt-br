---
title: "Configurar o gerenciamento de dispositivo híbrido de iOS e Mac com o System Center Configuration Manager e o Microsoft Intune | Microsoft Docs"
description: Configure o gerenciamento de dispositivos iOS com o System Center Configuration Manager e o Microsoft Intune.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5eae4400-58ca-4c71-804c-6a585cd3df5d
caps.latest.revision: 10
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 2288be606d7d586de5dc18d640f295e823daf266
ms.lasthandoff: 03/06/2017


---
# <a name="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar o gerenciamento de dispositivo híbrido do iOS com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Com o Configuration Manager e o Intune, você pode habilitar o registro de dispositivo BYOD (“traga seu próprio dispositivo”) do iOS e Mac OS X para dar acesso ao email da empresa e aos recursos para os usuários do iPhone, iPad e Mac. Depois que os usuários instalam o aplicativo do portal da empresa do Intune, seus dispositivos podem ser afetados pela política. Para poder gerenciar dispositivos iOS e Mac, você precisará importar um certificado APNs (Apple Push Notification Service). Esse certificado permite ao Intune gerenciar dispositivos iOS e Mac estabelece uma conexão IP reconhecida e criptografada com os serviços de autoridade de gerenciamento de dispositivo móvel.  

 Você também pode registrar dispositivos iOS corporativos.  Consulte [Registar dispositivos corporativos](enroll-company-owned-devices.md).  

## <a name="enable-ios-device-enrollment"></a>Habilitar o registro de dispositivo iOS  
 Para dar suporte ao registro de dispositivos iOS, siga estas etapas:  

#### <a name="set-up-ios-device-enrollment-in-configuration-manager"></a>Configurar o registro de dispositivo iOS no Configuration Manager  

1.  **Pré-requisitos** – Antes de configurar o registro para qualquer plataforma, conclua os pré-requisitos e os procedimentos em [Configurar MDM híbrido](setup-hybrid-mdm.md).    

2.  **Baixar uma solicitação de assinatura de certificado** - Um arquivo de solicitação de assinatura de certificado (.csr) é necessário para solicitar um certificado APNs da Apple.  

    1.  No console do Configuration Manager, no espaço de trabalho **Administração** , acesse **Serviços de Nuvem**> **Assinaturas do Microsoft Intune**.  

    2.  Na guia **Início** , clique em **Criar solicitação de certificado APNs**. A caixa de diálogo **Solicitar Solicitação de Assinatura de Certificado Apple Push Notification Service** é aberta.  

    3.  **Navegue** até o caminho para salvar o novo arquivo de solicitação de assinatura de certificado (.csr). Salve o arquivo (.csr) da solicitação de assinatura do certificado localmente.  

    4.  Clique em **Baixar**. O novo arquivo .csr do Microsoft Intune é baixado e salvo pelo Configuration Manager. O arquivo .csr é usado para solicitar um certificado de relação de confiança do Portal de Certificados Apple Push.  

3.  **Solicitar um certificado APNs da Apple** O certificado APNs (Apple Push Notification Service) é usado para estabelecer uma relação de confiança entre o serviço de gerenciamento, o Intune e os dispositivos móveis iOS registrados.  

    1.  Em um navegador, vá para o [Portal de Certificados por Push da Apple](http://go.microsoft.com/fwlink/?LinkId=269844) e entre com sua ID corporativa da Apple. Essa ID da Apple deve ser usada no futuro para renovar seu certificado APNs.  

    2.  Conclua o assistente usando o arquivo (.csr) de solicitação de assinatura do certificado. Baixe o certificado APNs e salve o arquivo .pem localmente. Este arquivo de certificado APNs (.pem) é usado para estabelecer uma relação de confiança entre o servidor do Apple Push Notification e a autoridade de gerenciamento de dispositivo móvel do Intune.  

4.  **Habilitar registro e carregar o certificado APNs** - Para habilitar o registro do iOS, carregue o certificado APNs.  

    1.  No console do Configuration Manager, no espaço de trabalho **Administração** , acesse **Serviços de Nuvem** > **Assinatura do Microsoft Intune**.  

    2.  Na guia **Início** do grupo **Assinatura** , clique em **Configurar Plataformas** > **IOS**.  

        > [!NOTE]  
        >  Não carregue o certificado APNs (Apple Push Notification Service) antes de habilitar o registro do iOS no console do Configuration Manager.  

    3.  Na caixa de diálogo **Propriedades da Assinatura do Microsoft Intune** , selecione a guia **iOS** e clique para marcar a caixa de seleção **Habilitar registro do iOS** .  

    4.  Clique em **Procurar**e vá para o arquivo de certificado APNs (.cer) baixado da Apple. O Configuration Manager exibe as informações de certificado APNs. Clique em **OK** para salvar o certificado APNs no Intune.  

 Depois da configuração, você precisará permitir que os usuários saibam como registrar seus dispositivos. Consulte [O que dizer aos usuários sobre o registro de seus dispositivos](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Essas informações se aplicam a dispositivos móveis gerenciados pelo Microsoft Intune e pelo Configuration Manager.

 > [!div class="button"]
 [< Etapa anterior](create-service-connection-point.md)  [Próxima etapa >](set-up-additional-management.md)

