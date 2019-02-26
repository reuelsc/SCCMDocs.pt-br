---
title: Usar o Azure AD para o cogerenciamento
titleSuffix: Configuration Manager
description: Com o Azure AD você pode tirar proveito de maior produtividade para seus usuários e segurança para seus recursos, em ambientes de nuvem e local
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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754571"
---
# <a name="use-azure-ad-for-co-management"></a>Usar o Azure AD para o cogerenciamento

Na nuvem, a identidade é o novo plano de controle. Azure Active Directory (AD do Azure) permite vincular seus usuários, dispositivos e aplicativos em ambientes de nuvem e locais. Registrar seus dispositivos ao Azure AD permite que você melhore a produtividade para seus usuários e segurança para os recursos. Ter dispositivos no Azure AD é a base para o cogerenciamento e acesso condicional baseado no dispositivo. 

Para obter mais informações sobre o acesso condicional baseado em dispositivo, consulte [How To: Exigir que os dispositivos gerenciados para acesso de aplicativo de nuvem com acesso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)

No vídeo a seguir, gerente de programa sênior Sandeep Deo e produto marketing manager Adam Harbour discutir e demonstração do Azure AD para o cogerenciamento:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Embedding-Co-management-With-Azure-Active-Directory/player]

Azure AD fornece duas opções para dispositivos da empresa atender às necessidades da sua organização:  

- **Dispositivo ingressado no AD do Azure**: Ingressar seus dispositivos Windows 10 no Azure AD sem a necessidade de uni-las ao Active Directory local  

    - Dá suporte ao Windows 10

    - Configurar sem a necessidade de qualquer configuração adicional para seus ambientes locais  

    - Habilitando a algumas configurações no Azure AD, você pode habilitar seus usuários ingressar dispositivos no Azure AD por meio da experiência de instalação do Windows (OOBE)  

    - Para obter mais informações, veja [How to: Planejar sua implementação de junção do Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  

- **Híbrido dispositivo ingressado no AD do Azure**: Junte-se os dispositivos de domínio existentes para o Azure AD  

    - Dá suporte ao Windows 10, Windows 8.1 e Windows 7

    - Configure usando as declarações do AD FS ou Azure AD Connect  

    - Para Windows 10 a junção ocorre no contexto do computador, para que os usuários não precisarão executar etapas adicionais  

    - Para obter mais informações, consulte [como planejar sua implementação de junção do Azure Active Directory híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)  

As duas opções fornecem funcionalidade semelhante para os usuários. Ela é flexível para que você escolha deles com base em suas necessidades. Por exemplo, você pode [acessar seus recursos locais](https://docs.microsoft.com/azure/active-directory/devices/azuread-join-sso) de computadores que ingressaram no AD do Azure, embora eles não estão associados ao Active Directory. 

Você pode unir dispositivos ao Azure AD em vários ambientes, não importa sua [método de autenticação](https://docs.microsoft.com/azure/security/azure-ad-choose-authn). Por exemplo, autenticação federada ou autenticação de nuvem. 

Se você já tiver um Active Directory no local, configurando uma das opções é simples. 



## <a name="benefits"></a>Benefícios

Ingresso de dispositivos para o Azure AD oferece os seguintes benefícios à sua organização:

#### <a name="single-sign-on-to-cloud-resources"></a>Logon único para recursos de nuvem
Em dispositivos ingressados no Azure AD, você obtém uma experiência integrada acessar quaisquer recursos de nuvem ou local. Depois que você entrar um computador Windows que tenha ingressado no Azure AD, você obter logon único para todos os aplicativos sem os prompts de entrada adicionais.  

#### <a name="windows-hello-for-business"></a>Windows Hello para empresas
Windows Hello para empresas traz uma autenticação sem senha forte para o Windows 10. Ao ingressar seus dispositivos no AD do Azure, você pode habilitar Windows Hello para empresas em toda a base para os recursos de nuvem e locais de usuários. Windows Hello para empresas elimina o problema de lembrar senhas complexas ou inadvertidamente expô-los. Seu processo de entrada é simples e seguro. 

Para obter mais informações, confira [Windows Hello para Empresas](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

#### <a name="device-based-conditional-access"></a>Acesso condicional baseado em dispositivo
Habilite o acesso condicional com base no estado do dispositivo para proteger melhor os dados da sua organização. Acesso condicional baseado em dispositivo requer um dispositivo gerenciado. Este dispositivo deve ser um dispositivo em conformidade ou um dispositivo ingressado no AD do Azure híbrido. Para dispositivos ingressados no AD do Azure, você precisa do Intune para marcar o dispositivo como compatível. Mas para híbrido do Azure dispositivos ingressados no AD, o estado do dispositivo em si é usada para avaliar o acesso condicional. Cogerenciamento oferece a vantagem adicional de avaliação de conformidade por meio do Intune para o Azure híbrido dispositivos ingressados no AD. Esse recurso torna-se de que a configuração do dispositivo está intacta. 

Para obter mais informações sobre o acesso condicional baseado em dispositivo, consulte [How To: Exigir que os dispositivos gerenciados para acesso de aplicativo de nuvem com acesso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).  

#### <a name="automatic-device-licensing"></a>Licenciamento de dispositivo automático
Todos os dispositivos Windows 10 ingressados no AD do Azure passam por verificações de licença. Essas verificações permitem atualizar automaticamente-los do Pro para Enterprise por meio da nuvem da Microsoft. Quando você remove a assinatura relevante do usuário, o dispositivo desatualiza automaticamente sua licença. Esse recurso fornece um único painel de controle para gerenciar licenças do Windows, sem qualquer processos complicados ou sistemas locais.

#### <a name="self-service-functionality"></a>Funcionalidade de autoatendimento
Funcionalidade de autoatendimento inclui a redefinição de senha de autoatendimento e a chave de recuperação do BitLocker. Azure AD também fornece opções diretas para redefinir sua senha ou acessar as chaves de recuperação do BitLocker. Você pode usar o AD do Azure para redefinir sua senha diretamente da tela de bloqueio do Windows, em vez de em um navegador da web. Esses recursos reduzem o atrito para usuários e ajudar a reduzir os custos de assistência técnica para a sua organização.  

Para obter mais informações, consulte [guia de início rápido: Redefinição de senha de autoatendimento](https://docs.microsoft.com/azure/active-directory/authentication/quickstart-sspr).

#### <a name="enterprise-state-roaming"></a>Enterprise state roaming
Todos os dispositivos ingressados no Azure AD podem sincronizar suas configurações para a nuvem. Qualquer dispositivo para o qual um usuário entra em sincronizações todas as suas configurações para uma experiência mais produtiva.  



## <a name="value-proposition"></a>Proposta de valor

Ingressar seus dispositivos no AD do Azure por meio de qualquer um dos métodos aceleram sua transformação digital. Ele permite mais funcionalidade fornecida pelo Microsoft 365. Você terá melhores experiências, e você terá uma segurança maior para seus dados. 

O Azure AD fornece várias opções para facilitar seu trabalho de carga, por exemplo:

- Gerenciar todas as identidades de dispositivo em sua organização a partir de um único lugar  

- Reduza os custos de assistência técnica, permitindo a redefinição de senha de autoatendimento. Em seguida, os usuários podem redefinir sua senha da tela de bloqueio do Windows 10 em seu dispositivo a qualquer momento.  



## <a name="configure"></a>Configurar

Se você já tiver um ambiente do Active Directory local e você deseja ingressar seus dispositivos ingressados no domínio ao AD do Azure, configure hybrid Azure dispositivos ingressados no AD. Para obter mais informações, [como planejar sua implementação de junção do Azure Active Directory híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan). 

O Configuration Manager tem uma configuração de cliente para [registrar automaticamente novos dispositivos ingressados no domínio do Windows 10 com o Azure AD](/sccm/core/clients/deploy/about-client-settings#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory). Para obter mais informações sobre como definir configurações de cliente, consulte [como definir as configurações de cliente](/sccm/core/clients/deploy/configure-client-settings).

Se você quiser configurar o Azure AD – junção de seus dispositivos sem também uni-las ao seu domínio local, examine as considerações para o Azure AD-junção em seu ambiente. Depois de você decidir ir com o ingresso no Azure AD, você tem várias opções para implantá-lo com base nas necessidades da sua organização. Para obter mais informações, consulte os seguintes artigos:
- [Como: Planejar sua implementação de junção do Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  
- [Entenda suas opções de provisionamento](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options)  

