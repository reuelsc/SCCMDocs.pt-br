---
title: Instalar o cliente com o Azure AD
titleSuffix: Configuration Manager
description: Instale e atribua o cliente do Configuration Manager em dispositivos Windows 10 usando o Azure Active Directory para autenticação
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b45c5938e9c1980802055bd73d5fd7e71122fc2a
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558109"
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Instalar e atribuir clientes do Configuration Manager com Windows 10 usando o Azure AD para autenticação

Para instalar o cliente do Configuration Manager em dispositivos Windows 10 usando a autenticação do Azure AD, integre o Configuration Manager ao Azure AD (Azure Active Directory). Os clientes podem estar na intranet comunicando-se diretamente com um ponto de gerenciamento habilitado para HTTPS ou qualquer ponto de gerenciamento em um site habilitado para HTTP aprimorado. Eles também podem se comunicar com base na Internet por meio do CMG ou com um ponto de gerenciamento baseado na Internet. Esse processo usa o Azure AD para autenticar clientes no site do Configuration Manager. O Azure AD substitui a necessidade de configurar e usar certificados de autenticação de cliente.

A configuração do Microsoft Azure AD pode ser mais fácil para alguns clientes do que a configuração de uma infraestrutura de chave pública para autenticação baseada em certificado. Há recursos que exigem integrar o site ao Microsoft Azure AD, mas não exigem necessariamente que os clientes sejam associados do Azure AD.<!-- SCCMDocs issue 1259 --> Para obter mais informações, consulte os seguintes artigos:
- [Planejar-se para o Azure Active Directory](/sccm/core/plan-design/security/plan-for-security#bkmk_planazuread)
- [Usar o Microsoft Azure AD para cogerenciamento](/sccm/comanage/quickstart-hybrid-aad)



## <a name="before-you-begin"></a>Antes de começar

- Um locatário do Azure AD é um pré-requisito  

- Requisitos do dispositivo:  

    - Windows 10  

    - Ingressado no Azure AD, ingressado em domínio de nuvem pura ou ingressado no Azure AD híbrido  

- Requisitos de usuário:  

    - O usuário conectado deve ter uma identidade do Azure AD.   

    - Se o usuário tiver uma identidade federada ou sincronizada, você deverá usar a [descoberta de usuário do Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser) do o Configuration Manager, bem como a [descoberta de usuário do Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc). Para obter mais informações sobre identidades híbridas, consulte [Definir uma estratégia de adoção de identidade híbrida](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->  

- Além dos [pré-requisitos existentes](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012MPpreq) para a função do sistema de sites do ponto de gerenciamento, também habilite o **ASP.NET 4.5** nesse servidor. Inclua as outras opções selecionadas automaticamente ao habilitar o ASP.NET 4.5.  

- Determine se o seu ponto de gerenciamento precisa de HTTPS. Para obter mais informações, consulte [Habilitar ponto de gerenciamento para HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps).  

- Opcionalmente, configure um [CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (gateway de gerenciamento de nuvem) para implantar clientes baseados na Internet. Para os clientes locais que são autenticam no Azure AD, não é necessário um CMG.  


## <a name="configure-azure-services-for-cloud-management"></a>Configurar os Serviços do Azure para o Gerenciamento de Nuvem

Conecte seu site do Configuration Manager ao Azure AD como a primeira etapa. Para obter detalhes sobre esse processo, consulte [Configurar serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard). Crie uma conexão com o serviço **Gerenciamento de Nuvem**.

Habilite a [Descoberta de Usuário do Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc) como parte da integração ao **Gerenciamento de Nuvem**. 

Depois de concluir essas ações, o site do Configuration Manager será conectado ao Azure AD. 



## <a name="configure-client-settings"></a>Definir as configurações do cliente

Essas configurações de cliente ajudam a ingressar dispositivos Windows 10 no Azure AD. Elas também permitem que os clientes baseados na Internet usem o CMG e o ponto de distribuição na nuvem.

1.  Defina as configurações de cliente a seguir na seção **Serviços de Nuvem** usando as informações em [Como definir as configurações de cliente](/sccm/core/clients/deploy/configure-client-settings).  

    - **Permitir acesso ao ponto de distribuição na nuvem**: Habilite essa configuração para ajudar os dispositivos baseados na Internet a obter o conteúdo necessário para instalar o cliente do Configuration Manager. Se o conteúdo não estiver disponível no ponto de distribuição na nuvem, os dispositivos poderão recuperar o conteúdo por meio do CMG. A inicialização da instalação de cliente tentará o ponto de distribuição na nuvem novamente durante quatro horas antes de recorrer ao CMG.<!--495533-->  

    - **Registrar automaticamente novos dispositivos ingressados em domínio do Windows 10 com o Azure Active Directory**: Definido como **Sim** ou **Não**. A configuração padrão é **Sim**. Esse comportamento também é o padrão no Windows 10, versão 1709.

    - **Habilitar clientes a usar um gateway de gerenciamento de nuvem** – Defina como **Sim** (padrão) ou **Não**.  

2.  Implante as configurações do cliente na coleção necessária de dispositivos. Não implante essas configurações em coleções de usuários.

Para confirmar se o dispositivo está ingressado no Azure AD, execute `dsregcmd.exe /status` em um prompt de comando. O campo **AzureAdjoined** nos resultados mostram **SIM** se o dispositivo é ingressado no Azure AD.



## <a name="install-and-register-the-client-using-azure-ad-identity"></a>Instalar e registrar o cliente usando a identidade do Azure AD

Para instalar o cliente manualmente usando a identidade do Azure AD, primeiro examine o processo geral em [Como instalar clientes manualmente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual). 

 > [!Note]  
 > O dispositivo precisa ter acesso à Internet para acessar o Azure AD, mas não precisa ser baseado na Internet. 

O seguinte exemplo mostra a estrutura geral da linha de comando: `ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

Para obter mais informações, consulte [Propriedades de instalação do cliente](/sccm/core/clients/deploy/about-client-installation-properties).

As propriedades /mp e CCMHOSTNAME e especificam uma das seguintes opções, dependendo do cenário:
- Ponto de gerenciamento local. Especifique somente a propriedade /mp. O CCMHOSTNAME não é necessário.
- Gateway de gerenciamento de nuvem
- Ponto de gerenciamento baseado na Internet A propriedade SMSMP especifica o ponto de gerenciamento local ou baseado na Internet.

Esse exemplo usa um gateway de gerenciamento de nuvem. Ele substitui os valores de exemplo de cada propriedade: `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

Começando na versão 1810, o site publica informações adicionais do Microsoft Azure AD no Gateway de Gerenciamento de Nuvem. Um cliente associado ao Azure AD obtém essas informações do CMG durante o processo ccmsetup, usando o mesmo locatário ao qual ele está associado. Este comportamento simplifica ainda mais a instalação do cliente, em um ambiente com mais de um locatário do Microsoft Azure AD. Agora, as duas únicas propriedades necessárias do ccmsetup são **CCMHOSTNAME** e **SMSSiteCode**.<!--3607731-->

Para automatizar a instalação do cliente usando a identidade do Azure AD por meio do Microsoft Intune, consulte [Como preparar dispositivos baseados na Internet para cogerenciamento](/sccm/comanage/how-to-prepare-win10#install-the-configuration-manager-client).



## <a name="next-steps"></a>Próximas etapas

Após a conclusão, você pode continuar a [monitorar e gerenciar clientes](/sccm/core/clients/manage/monitor-clients).
