---
title: Usar o Azure AD para cogerenciamento
titleSuffix: Configuration Manager
description: Com o Azure AD, você pode tirar proveito de mais produtividade para seus usuários e segurança para seus recursos, em ambientes de nuvem e locais
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2af37410-d04c-4059-801c-9edb8bf72d89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3b773c0bfe8cd0f8253a67ac96f5a0113b7206c0
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754571"
---
# <a name="use-azure-ad-for-co-management"></a>Usar o Azure AD para cogerenciamento

Na nuvem, a identidade é o novo plano de controle. O Azure Active Directory (Azure AD) permite vincular seus usuários, dispositivos e aplicativos em ambientes de nuvem e locais. Registrar seus dispositivos no Azure AD permite melhorar a produtividade para seus usuários e a segurança para seus recursos. Ter dispositivos no Azure AD é a base para o cogerenciamento e o acesso condicional baseado no dispositivo. 

Para saber mais sobre o acesso condicional baseado em dispositivo, confira [Como exigir dispositivos gerenciados para acesso de aplicativo de nuvem com o acesso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)

No vídeo a seguir, o gerente de programas sênior Sandeep Deo e o gerente de marketing de produto Adam Harbour discutem e demonstram o Azure AD para cogerenciamento:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Embedding-Co-management-With-Azure-Active-Directory/player]

O Azure AD fornece duas opções para que dispositivos corporativos atendam às necessidades da sua organização:  

- **Dispositivo vinculado ao Azure AD**: vincular seus dispositivos Windows 10 ao Azure AD sem a necessidade de vinculá-los ao Active Directory local  

    - Compatível com Windows 10

    - Configurar sem a necessidade de definições adicionais para seus ambientes locais  

    - Ao habilitar algumas configurações no Azure AD, você pode permitir que seus usuários vinculem dispositivos ao Azure AD por meio da experiência de instalação do Windows (OOBE)  

    - Para obter mais informações, veja [How to: Planejar sua implementação de ingresso no Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  

- **Dispositivo ingressado no Azure AD híbrido**: Ingresse seus dispositivos existentes do domínio no Azure AD  

    - Compatível com Windows 10, Windows 8.1 e Windows 7

    - Configurar usando declarações do AD FS ou do Azure AD Connect  

    - No Windows 10, o ingresso ocorre no contexto do computador, de modo que os usuários não precisam executar etapas adicionais  

    - Para saber mais, confira [Como planejar a implementação do ingresso no Azure Active Directory híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan).  

As duas opções oferecem funcionalidades semelhantes para os usuários. Você pode escolher qualquer uma com base em suas necessidades. Por exemplo, você pode [acessar seus recursos locais](https://docs.microsoft.com/azure/active-directory/devices/azuread-join-sso) de computadores que ingressaram no Azure AD, mesmo se não estiverem ingressados no Active Directory. 

Você pode ingressar dispositivos no Azure AD em vários ambientes, independentemente do [método de autenticação](https://docs.microsoft.com/azure/security/azure-ad-choose-authn). Por exemplo, autenticação federada ou autenticação de nuvem. 

Se você já tem um Active Directory local, configurar uma das opções é simples. 



## <a name="benefits"></a>Benefícios

Ingressar dispositivos no Azure AD oferece os seguintes benefícios à sua organização:

#### <a name="single-sign-on-to-cloud-resources"></a>Logon único para recursos de nuvem
Em dispositivos ingressados no Azure AD, você obtém uma experiência integrada acessando quaisquer recursos de nuvem ou local. Depois de entrar em um computador Windows que tenha ingressado no Azure AD, você obtém logon único em todos os aplicativos sem solicitações de entrada adicionais.  

#### <a name="windows-hello-for-business"></a>Windows Hello para Empresas
O Windows Hello para empresas leva uma autenticação sem senha forte ao Windows 10. Ao ingressar seus dispositivos no Azure AD, você pode habilitar o Windows Hello para Empresas em toda a base de usuários para obter recursos de nuvem e locais. O Windows Hello para Empresas elimina o problema de ter que se lembrar de senhas complexas ou de exibi-las inadvertidamente. Seu processo de entrada é simples e seguro. 

Para obter mais informações, confira [Windows Hello para Empresas](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

#### <a name="device-based-conditional-access"></a>Acesso condicional baseado no dispositivo
Habilite o acesso condicional baseado no estado do dispositivo para proteger melhor os dados da sua organização. O acesso condicional baseado em dispositivo requer um dispositivo gerenciado. Esse dispositivo deve estar em conformidade ou ser um dispositivo ingressado no Azure AD híbrido. Em dispositivos ingressados no Azure AD, você precisa do Intune para marcar o dispositivo como em conformidade. No entanto, em dispositivos ingressados no Azure AD híbrido, o estado do dispositivo em si é usado para avaliar o acesso condicional. O cogerenciamento oferece a vantagem adicional de avaliar por meio do Intune a conformidade de dispositivos ingressados no Azure AD híbrido. Esse recurso garante que a configuração dos dispositivos esteja intacta. 

Para saber mais sobre o acesso condicional baseado em dispositivo, confira [Como exigir dispositivos gerenciados para acesso de aplicativo de nuvem com o acesso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).  

#### <a name="automatic-device-licensing"></a>Licenciamento automático de dispositivos
Todos os dispositivos Windows 10 ingressados no Azure AD passam por verificações de licença. Essas verificações permitem atualizá-los automaticamente de Pro para Enterprise por meio da nuvem da Microsoft. Quando você remove a assinatura relevante do usuário, o downgrade da licença do dispositivo é feito automaticamente. Esse recurso fornece um único painel de controle para gerenciar licenças do Windows, sem processos complicados ou sistemas locais.

#### <a name="self-service-functionality"></a>Funcionalidade de autoatendimento
A funcionalidade de autoatendimento inclui a redefinição de senha e a chave de recuperação do BitLocker. O Azure AD também fornece opções diretas para redefinir sua senha ou acessar as chaves de recuperação do BitLocker. Você pode usar o Azure AD para redefinir sua senha diretamente da tela de bloqueio do Windows, ao invés de fazer isso em um navegador da Web. Esses recursos reduzem o atrito para os usuários e ajudam a reduzir os custos de assistência técnica para a sua organização.  

Para saber mais, confira [Início Rápido: redefinição de senha de autoatendimento](https://docs.microsoft.com/azure/active-directory/authentication/quickstart-sspr).

#### <a name="enterprise-state-roaming"></a>Enterprise State Roaming
As configurações de todos os dispositivos ingressados no Azure AD podem ser sincronizadas para a nuvem. Qualquer dispositivo em que um usuário entra sincroniza todas as configurações para proporcionar uma experiência mais produtiva.  



## <a name="value-proposition"></a>Proposta de valor

Ingressar seus dispositivos no Azure AD por meio de qualquer um dos métodos acelera sua transformação digital. Isso permite que mais funcionalidade seja fornecida pelo Microsoft 365. Você terá melhores experiências e uma segurança maior para seus dados. 

O Azure AD fornece várias opções para facilitar sua carga de trabalho, por exemplo:

- Gerenciar todas as identidades de dispositivo de sua organização em um único lugar  

- Reduzir os custos de assistência técnica, permitindo a redefinição de senha de autoatendimento. Assim, os usuários podem redefinir suas senhas na tela de bloqueio do Windows 10 em seus dispositivos a qualquer momento.  



## <a name="configure"></a>Configurar

Se você já tem um ambiente do Active Directory local e quer vincular seus dispositivos ingressados no domínio do Azure AD, configure dispositivos ingressados no Azure AD híbrido. Para saber mais, confira [Como planejar a implementação do ingresso no Azure Active Directory híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan). 

O Configuration Manager tem uma configuração de cliente para [Registrar automaticamente novos dispositivos ingressados no domínio do Windows 10 com o Azure AD](/sccm/core/clients/deploy/about-client-settings#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory). Para saber mais sobre como definir essas configurações de cliente, confira [Como definir as configurações do cliente](/sccm/core/clients/deploy/configure-client-settings).

Se você quiser configurar o ingresso no Azure AD de seus dispositivos sem ingressá-los também no seu domínio local, analise as considerações para o ingresso no Azure AD em seu ambiente. Depois que você optar pelo ingresso no Azure AD, terá muitas opções para implantá-lo com base nas necessidades de sua organização. Para obter mais informações, confira os seguintes artigos:
- [Como: Planejar sua implementação de ingresso no Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  
- [Entender suas opções de provisionamento](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options)  

