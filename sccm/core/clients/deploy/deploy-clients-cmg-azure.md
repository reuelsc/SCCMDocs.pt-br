---
title: Instalar o cliente com o Azure AD
titleSuffix: Configuration Manager
description: Instale e atribua o cliente do Configuration Manager em dispositivos Windows 10 usando o Azure Active Directory para autenticação
ms.date: 03/28/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 91ebb0c35687b231a6f08b7bc92cccb83cf0e602
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32344680"
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Instalar e atribuir clientes do Configuration Manager com Windows 10 usando o Azure AD para autenticação

Para instalar o cliente do Configuration Manager em dispositivos Windows 10 usando a autenticação do Azure AD, integre o Configuration Manager ao Azure AD (Azure Active Directory). Os clientes podem estar na intranet comunicando-se diretamente com um ponto de gerenciamento habilitado para HTTPS. Eles também podem se comunicar com base na Internet por meio do CMG ou com um ponto de gerenciamento baseado na Internet. Esse processo usa o Azure AD para autenticar clientes no site do Configuration Manager. O Azure AD substitui a necessidade de configurar e usar certificados de autenticação de cliente.



## <a name="before-you-begin"></a>Antes de começar

- Um locatário do Azure AD é um pré-requisito  

- Requisitos do dispositivo:  

    - Windows 10  

    - Ingressado no Azure AD, ingressado em domínio de nuvem pura ou ingressado no Azure AD híbrido  

- Requisitos de usuário:  

    - O usuário conectado deve ter uma identidade do Azure AD.   

    - Se o usuário tiver uma identidade federada ou sincronizada, você deverá usar a [descoberta de usuário do Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser) do o Configuration Manager, bem como a [descoberta de usuário do Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc). Para obter mais informações sobre identidades híbridas, consulte [Definir uma estratégia de adoção de identidade híbrida](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->  

- Além dos [pré-requisitos existentes](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012MPpreq) para a função do sistema de sites do ponto de gerenciamento, também habilite o **ASP.NET 4.5** nesse servidor. Inclua as outras opções selecionadas automaticamente ao habilitar o ASP.NET 4.5.  

- Configure todos os pontos de gerenciamento para o modo HTTPS. Para obter mais informações, consulte [Requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements) e [Implantar o certificado do servidor Web em sistemas de sites que executam o IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  
    - Se você estiver usando o gateway de gerenciamento de nuvem, precisará apenas configurar o HTTPS para pontos de gerenciamento que você habilitar para o gateway de gerenciamento de nuvem.
    - Se estiver implantando os clientes da intranet usando a autenticação baseada em token do Azure AD, todos os pontos de gerenciamento com os quais esses clientes poderão entrar em contato devem ser habilitados para HTTPS. 

- Opcionalmente, configure um [CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (gateway de gerenciamento de nuvem) para implantar clientes baseados na Internet. Para os clientes locais que são autenticam no Azure AD, não é necessário um CMG.  


## <a name="configure-azure-services-for-cloud-management"></a>Configurar os Serviços do Azure para o Gerenciamento de Nuvem

Conecte seu site do Configuration Manager ao Azure AD como a primeira etapa. Para obter detalhes sobre esse processo, consulte [Configurar serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard). Crie uma conexão com o serviço **Gerenciamento de Nuvem**.

Habilite a [Descoberta de Usuário do Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc) como parte da integração ao **Gerenciamento de Nuvem**. 

Depois de concluir essas ações, o site do Configuration Manager será conectado ao Azure AD. 



## <a name="configure-client-settings"></a>Definir as configurações do cliente

Essas configurações de cliente ajudam a ingressar dispositivos Windows 10 no Azure AD. Elas também permitem que os clientes baseados na Internet usem o CMG e o ponto de distribuição na nuvem.

1.  Defina as configurações de cliente a seguir na seção **Serviços de Nuvem** usando as informações em [Como definir as configurações de cliente](/sccm/core/clients/deploy/configure-client-settings).  

    - **Permitir o acesso ao ponto de distribuição na nuvem**: habilite essa configuração para ajudar os dispositivos baseados na Internet a obter o conteúdo necessário para instalar o cliente do Configuration Manager. Se o conteúdo não estiver disponível no ponto de distribuição na nuvem, os dispositivos poderão recuperar o conteúdo por meio do CMG. A inicialização da instalação de cliente tentará o ponto de distribuição na nuvem novamente durante quatro horas antes de recorrer ao CMG.<!--495533-->  

    - **Registrar automaticamente os novos dispositivos ingressados em domínio do Windows 10 no Azure Active Directory**: defina como **Sim** ou **Não**. A configuração padrão é **Sim**. Esse comportamento também é o padrão no Windows 10, versão 1709.

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

Para automatizar a instalação do cliente usando a identidade do Azure AD por meio do Microsoft Intune, consulte o processo de [Preparar dispositivos Windows 10 para o cogerenciamento](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client).



## <a name="next-steps"></a>Próximas etapas

Após a conclusão, você pode continuar a [monitorar e gerenciar clientes](/sccm/core/clients/manage/monitor-clients).
