---
title: Instalar e atribuir o cliente da internet | Microsoft Docs
description: Instale e atribua o cliente do System Center Configuration Manager da internet.
ms.custom: na
ms.date: 8/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
caps.latest.revision: "14"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: d783cc2f12400084ad1cd62a338a31c9747c05fb
ms.sourcegitcommit: f6a428a8db7145affa388f59e0ad880bdfcf17b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2017
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Instalar e atribuir clientes do Configuration Manager com Windows 10 usando o Azure AD para autenticação

Você pode usar os serviços de nuvem do Configuration Manager com Azure AD para dar suporte aos seguintes cenários:

- Instalar manualmente o cliente do Configuration Manager em dispositivos com Windows 10 na Internet e atribui-lo a um site do Configuration Manager (exige a função de sistema de site do gateway de gerenciamento de nuvem).
- Use o Azure AD para autenticar clientes a fim de acessar seus sites do Configuration Manager. O Azure AD substitui a necessidade de configurar e usar certificados de autenticação de cliente.
- Descubra os usuários do Azure AD em seu site para usar nas coleções e outras operações do Configuration Manager.

Use as etapas a seguir para ajudar a fazer isso:

- **Etapa 1: Configurar o aplicativo dos Serviços do Azure em serviços de nuvem do Configuration Manager e configurar a descoberta de usuário do Azure AD**
- **Etapa 2: Configurar o Gateway de Gerenciamento de Nuvem** (opcional para clientes locais)
- **Etapa 3: Definir as configurações de cliente para unir dispositivos com Windows 10 ao Azure AD e permitir que os clientes usem o Gateway de Gerenciamento de Nuvem**
- **Etapa 4: Instalar e registrar o cliente do Configuration Manager usando a identidade do Azure Active Directory**


## <a name="before-you-start"></a>Antes de começar

- Você deve ter um locatário do Azure AD.
- Seus dispositivos devem executar o Windows 10, devem ter ingressado no Azure AD e conectados usando uma identidade do Azure AD. Os clientes também podem ser ingressados ao domínio além de ingressados ao Azure AD).
- Além de [pré-requisitos existentes](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) para a função do sistema de site do ponto de gerenciamento, você deverá garantir que o **ASP.NET 4.5** (e as outras opções que estiverem automaticamente selecionadas) esteja habilitado no computador que hospeda esta função do sistema de site.
- Para usar o Configuration Manager para implantar o cliente:
    - Configure pelo menos um ponto de gerenciamento para o modo HTTPS se quiser usar o Azure AD para autenticar em vez de usar certificados de cliente.
        Se você estiver usando certificados de cliente em vez do Gateway de Gerenciamento de Nuvem, um ponto de gerenciamento HTTPS será opcional, mas recomendado. Se você estiver usando o Azure AD para autenticação, mesmo se for para clientes locais ou na Internet, o ponto de gerenciamento HTTPS será necessário.
    - Configure um Gateway de Gerenciamento de Nuvem, se você quiser implantar os clientes da Internet. Para clientes locais, que você autentica com o Azure AD, não é necessário configurar o Gateway de Gerenciamento de Nuvem.


## <a name="step-1-set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Etapa 1: Configurar o aplicativo dos Serviços do Azure em serviços de nuvem do Configuration Manager

Isso conecta o site do Configuration Manager ao Azure AD e é um pré-requisito para todas as outras operações nesta seção. 

A Descoberta de Usuários do Azure AD está configurada como parte do *Gerenciamento de Nuvem*. O procedimento para fazer isso é detalhado na etapa **6** do procedimento [Criar o aplicativo Web do Azure para uso com o Configuration Manager](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp) no tópico *Configurar serviços do Azure para uso com o Configuration Manager*.
    
Após a conclusão do procedimento, você terá conectado seu site do Configuration Manager ao Azure AD. 

## <a name="step-2-set-up-the-cloud-management-gateway"></a>Etapa 2: Configurar o Gateway de Gerenciamento de Nuvem

Configure o Gateway de Gerenciamento de Nuvem para ajudar a habilitar os cenários de gerenciamento de nuvem descritos neste tópico. Encontre ajuda nos tópicos a seguir: 

- [Planejar o gateway de gerenciamento de nuvem no Configuration Manager](/sccm/core/clients/manage/plan-cloud-management-gateway).
- [Configurar o gateway de gerenciamento de nuvem para o Configuration Manager](/sccm/core/clients/manage/setup-cloud-management-gateway).
- [Monitorar o gateway de gerenciamento de nuvem no Configuration Manager](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway).

## <a name="step-3-configure-client-settings-to-join-windows-10-devices-with-azure-ad-and-enable-clients-to-use-the-cloud-management-gateway"></a>Etapa 3: Definir as configurações de cliente para unir dispositivos com Windows 10 ao Azure AD e permitir que os clientes usem o Gateway de Gerenciamento de Nuvem

1.  Defina a seguinte seção de configurações de cliente (encontradas nos **Serviços de Nuvem**) usando as informações em [Como definir as configurações de cliente](/sccm/core/clients/deploy/configure-client-settings).
    - **Permitir o acesso ao ponto de distribuição na nuvem** - Habilite essa configuração para ajudar dispositivos baseados na Internet a obter o conteúdo necessário para instalar o cliente do Configuration Manager. Se o conteúdo não estiver disponível no ponto de distribuição de nuvem, os dispositivos poderão recuperar o conteúdo de um ponto de gerenciamento conectado ao gateway de gerenciamento de nuvem.
    - **Registrar automaticamente os novos dispositivos ingressados em domínio do Windows 10 com o Azure Active Directory** – Defina como **Sim** (padrão) ou **Não**.
    - **Habilitar clientes a usar um gateway de gerenciamento de nuvem** – Defina como **Sim** (padrão) ou **Não**.
2.  Implante as configurações do cliente na coleção necessária de dispositivos. Não implante essas configurações em coleções de usuários.

Para confirmar o ingresso do dispositivo ao Azure AD, execute o comando **dsregcmd.exe /status** em uma janela do prompt de comando. O campo **AzureAdjoined** nos resultados mostram **SIM** se o dispositivo tiver ingressado no Azure AD.


## <a name="step-4-install-and-register-the-configuration-manager-client-using-azure-active-directory-identity"></a>Etapa 4: Instalar e registrar o cliente do Configuration Manager usando a identidade do Azure Active Directory

Para instalar o cliente, use as instruções em [Como implantar clientes em computadores com Windows no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually) usando a seguinte linha de comando de instalação: 

**ccmsetup.exe /mp&#58; https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=DFD SMSMP=https://SCCMDFPSS.contoso.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011DB47 AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d17026 AADRESOURCEURI=https://contososerver**

- **/MP** – origem do download. Pode definir como CMG se for inicializado da internet.
- **CCMHOSTNAME**: o nome do seu ponto de gerenciamento da Internet. Você pode encontrá-lo executando **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** de um prompt de comando em um cliente gerenciado.
- **SMSSiteCode**: o código do site do Configuration Manager.
- **SMSMP**: o nome do seu ponto de gerenciamento de pesquisa – o ponto de gerenciamento pode estar em sua intranet.
- **AADTENANTID:**, **AADTENANTNAME:** a ID e o nome do locatário do Azure AD vinculado ao Configuration Manager. Você pode localizar isso executando dsregcmd.exe /status em um prompt de comando em um dispositivo unido do Azure AD.
- **AADCLIENTAPPID**: a ID do aplicativo cliente do Azure AD. Para obter ajuda sobre como localizar isso, veja [Usar o portal para criar um aplicativo e uma entidade de serviço do Azure Active Directory que pode acessar recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key).
- **AADResourceUri:** o URI do identificador do aplicativo de servidor integrado do Azure AD. Para saber mais, confira [Configurar serviços do Azure para uso com o Configuration Manager](/sccm/core/servers/deploy/configure/azure-services-wizard).




## <a name="next-steps"></a>Próximas etapas

Após a conclusão, você pode continuar a [monitorar e gerenciar clientes](/sccm/core/clients/manage/monitor-clients).
