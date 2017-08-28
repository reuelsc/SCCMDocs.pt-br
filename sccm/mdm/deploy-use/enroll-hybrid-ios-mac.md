---
title: "Configurar o gerenciamento de dispositivo híbrido de iOS e Mac com o System Center Configuration Manager e o Microsoft Intune | Microsoft Docs"
description: Configure o gerenciamento de dispositivos iOS com o System Center Configuration Manager e o Microsoft Intune.
ms.custom: na
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5eae4400-58ca-4c71-804c-6a585cd3df5d
caps.latest.revision: "10"
caps.handback.revision: "0"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: d84d6f3dba65f1d8114ef2eef9f19a2bb5389027
ms.sourcegitcommit: 9a6f8e028fb5eb2e752da70f42a5b548339bd8f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2017
---
# <a name="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar o gerenciamento de dispositivo híbrido do iOS com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Com o Configuration Manager e o Intune, você habilita o registro do dispositivo do iOS e macOS para dar acesso ao email da empresa e aos recursos para os usuários do iPhone, iPad e Mac. Depois que os usuários instalam o aplicativo do portal da empresa do Intune, seus dispositivos podem ser afetados pela política. Para poder gerenciar dispositivos iOS e Mac, você precisará importar um certificado APNs (Apple Push Notification Service). Este certificado permite que o Intune gerencie dispositivos iOS e Mac estabelecendo uma conexão com o serviço de gerenciamento de dispositivos da Apple.  

 Você também pode registrar dispositivos iOS corporativos.  Consulte [Registar dispositivos corporativos](enroll-company-owned-devices.md).  

**Pré-requisitos**<br>
Antes de poder configurar o registro para qualquer plataforma, conclua os pré-requisitos e os procedimentos em [Configurar MDM híbrido](setup-hybrid-mdm.md).

Para dar suporte ao registro de dispositivos iOS, siga estas etapas:  

## <a name="download-a-certificate-signing-request"></a>Baixar uma solicitação de assinatura de certificado
Um arquivo de solicitação de assinatura de certificado é necessário para solicitar um certificado APNs da Apple.  

1.  No console do Configuration Manager, no espaço de trabalho **Administração** , acesse **Serviços de Nuvem**> **Assinaturas do Microsoft Intune**.  

2.  Na guia **Início** , clique em **Criar solicitação de certificado APNs**. A caixa de diálogo **Solicitar Solicitação de Assinatura de Certificado Apple Push Notification Service** é aberta.  

3.  **Navegue** até o caminho para salvar o novo arquivo de solicitação de assinatura de certificado. Salve o arquivo da solicitação de assinatura do certificado localmente.  

4.  Clique em **Baixar**. O novo arquivo de solicitação da assinatura do certificado do Microsoft Intune é baixado e salvo peloConfiguration Manager. O arquivo de solicitação da assinatura do certificado é usado para solicitar um certificado de relação de confiança do Portal de Certificados Apple Push.  

## <a name="request-an-mdm-push-certificate-from-apple"></a>Solicitar um certificado de PUSH MDM da Apple
O certificado Push MDM é usado para estabelecer uma relação de confiança entre o serviço de gerenciamento, o Intune e os dispositivos móveis iOS registrados.  

1.  Em um navegador, vá para o [Portal de Certificados por Push da Apple](http://go.microsoft.com/fwlink/?LinkId=269844) e entre com sua ID corporativa da Apple. Essa ID da Apple deve ser usada no futuro para renovar seu certificado APNs.  

2.  Conclua o assistente usando o arquivo (.csr) de solicitação de assinatura do certificado. Baixe o certificado Push MDM e salve o arquivo pem localmente. Este arquivo de certificado (.pem) é usado para estabelecer uma relação de confiança entre o servidor do Apple Push Notification e a autoridade de gerenciamento de dispositivo móvel do Intune.  

> [!NOTE]  
>  Não carregue o certificado APNs (Apple Push Notification Service) no Intune antes de habilitar o registro do iOS no console do Configuration Manager.  

## <a name="enable-enrollment-and-upload-the-mdm-push-certificate"></a>Habilitar o registro e carregar o certificado Push MDM
Para habilitar o registro do iOS, carregue o certificado APNs.  

1.  No console do Configuration Manager, no espaço de trabalho **Administração** , acesse **Serviços de Nuvem** > **Assinatura do Microsoft Intune**.  

2.  Na guia **Início** do grupo **Assinatura** , clique em **Configurar Plataformas** > **IOS**.  

3.  Na caixa de diálogo **Propriedades da Assinatura do Microsoft Intune** , selecione a guia **iOS** e clique para marcar a caixa de seleção **Habilitar registro do iOS** .  
4.  Clique em **Procurar**e vá para o arquivo de certificado APNs (.cer) baixado da Apple. O Configuration Manager exibe as informações de certificado APNs. Clique em **OK** para salvar o certificado APNs no Intune.  

Após a configuração, será necessário permitir que os usuários saibam como registrar seus dispositivos. Consulte [O que dizer aos usuários sobre o registro de seus dispositivos](https://docs.microsoft.com/intune/end-user-educate). Essas informações se aplicam a dispositivos móveis gerenciados pelo Microsoft Intune e pelo Configuration Manager.

## <a name="configure-enrollment-restrictions"></a>Configurar restrições de registro

Você pode limitar os dispositivos que podem ser registrados bloqueando dispositivos de propriedade pessoal. Isso impede que os usuários registrem seus dispositivos usando o Portal da Empresa. Se você bloquear dispositivos pessoais, somente os dispositivos a seguir poderão ser registrados:
- [Dispositivos pré-declarados](predeclare-devices-with-hardware-id.md)
- [Dispositivos gerenciados do Apple Configurator](ios-hybrid-enrollment-using-apple-configurator.md)
- [Dispositivos gerenciados por DEP (Programa de registro de dispositivos)](ios-device-enrollment-program-for-hybrid.md)
- Dispositivos registrados com uma [conta de gerenciador de registro do dispositivo](enroll-devices-with-device-enrollment-manager.md)

### <a name="to-enable-enrollment-restrictions"></a>Para habilitar as restrições de registro
1.  No console do Configuration Manager, no espaço de trabalho **Administração** , acesse **Serviços de Nuvem** > **Assinatura do Microsoft Intune**.
2.  Na guia **Início** do grupo **Assinatura** , clique em **Configurar Plataformas** > **IOS**.
3.  Escolha **Bloquear dispositivos de propriedade pessoal** para limitar o registro a dispositivos da empresa.

> [!div class="button"]
[< Etapa anterior](create-service-connection-point.md)  [Próxima etapa >](set-up-additional-management.md)
