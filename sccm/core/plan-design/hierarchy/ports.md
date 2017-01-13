---
title: Portas usadas pelo Configuration Manager | Microsoft Docs
description: "Saiba mais sobre as portas necessárias e personalizáveis que o System Center Configuration Manager usa para conexões."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
caps.latest.revision: 8
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 41000b978f1add9ec6910bfa86f13e92bf93c4e4


---
# <a name="ports-used-in-system-center-configuration-manager"></a>Portas usadas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager é um sistema cliente/servidor distribuído. A natureza distribuída do Configuration Manager significa que as conexões podem ser estabelecidas entre os servidores de site, sistemas de sites e clientes. Algumas conexões usam portas que não são configuráveis e algumas oferecem suporte a portas personalizadas que você especifica. Verifique se as portas necessárias estão disponíveis, se você usar tecnologia de filtragem de porta, como firewalls, roteadores, servidores proxy e IPsec.  

> [!NOTE]  
>  Se houver suporte a clientes baseados na Internet usando a ponte SSL, além dos requisitos de porta, você também deverá permitir alguns verbos e cabeçalhos HTTP para transpor seu firewall. .  

 As listagens de portas a seguir são usadas pelo Configuration Manager e não incluem informações para serviços padrão do Windows, como configurações da Política de Grupo para Active Directory Domain Services e autenticação Kerberos. Para obter informações sobre serviços e portas do Windows Server, consulte [Visão geral de serviços e requisitos de porta de rede para o sistema do Windows Server](http://go.microsoft.com/fwlink/p/?LinkID=123652).  

##  <a name="a-namebkmkconfigurableportsa-ports-you-can-configure"></a><a name="BKMK_ConfigurablePorts"></a> Portas que você pode configurar  
 O Configuration Manager permite que você configure as portas para os seguintes tipos de comunicação:  

-   Ponto de sites da Web do catálogo de aplicativos com o ponto de serviços Web do catálogo de aplicativos  

-   Ponto proxy do registro com o ponto de registro  

-   Cliente com sistemas de site que executam o IIS  

-   Cliente com Internet (como configurações do servidor proxy)  

-   Ponto de atualização de software com Internet (como configurações do servidor proxy)  

-   Ponto de atualização de software com o servidor WSUS  

-   Servidor do site com o servidor de banco de dados do site  

-   Pontos do Reporting Services  

    > [!NOTE]  
    >  As portas em uso para a função do sistema de site do ponto do Reporting Services são configuradas no SQL Server Reporting Services. Essas portas são usadas pelo Configuration Manager durante comunicações com o ponto do Reporting Services. Lembre-se de verificar essas portas que definem as informações de filtro IP para políticas IPsec ou para configurar firewalls.  

Por padrão, a porta HTTP usada para comunicação do cliente com o sistema de sites é a porta 80 e a porta HTTPS padrão é 443. As portas para comunicação do cliente para o sistema de sites por HTTP ou HTTPS podem ser alteradas durante a Instalação ou nas Propriedades do Site do Configuration Manager.  

As portas em uso para a função do sistema de site do ponto do Reporting Services são configuradas no SQL Server Reporting Services. Essas portas são usadas pelo Configuration Manager durante comunicações com o ponto do Reporting Services. Lembre-se de verificar essas portas que definem as informações de filtro IP para políticas IPsec ou para configurar firewalls.  

##  <a name="a-namebkmknonconfigurableportsa-non-configurable-ports"></a><a name="BKMK_NonConfigurablePorts"></a> Portas não configuráveis  
O Configuration Manager não permite que você configure as portas para os seguintes tipos de comunicação:  

-   Site a site  

-   Servidor do site com o sistema de site  

-   Console do Configuration Manager para Provedor de SMS  

-   Console do Configuration Manager para a Internet  

-   Conexões com serviços de nuvem, como o Microsoft Intune e pontos de distribuição baseados em nuvem  

##  <a name="a-namebkmkcommunicationportsa-ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMK_CommunicationPorts"></a> Portas usadas por sistemas de site e clientes do Gerenciador de Configurações  
As seções a seguir detalham as portas usadas para comunicação no Configuration Manager. As setas no título da seção, entre os computadores, representam a direção da comunicação:  

-   -- > indica que um computador inicia a comunicação e o outro computador sempre responde  

-   &lt; -- > indica que qualquer computador pode iniciar a comunicação  

###  <a name="a-namebkmkportsaia-asset-intelligence-synchronization-point-----microsoft"></a><a name="BKMK_PortsAI"></a> Ponto de sincronização do Asset Intelligence -- &gt; Microsoft  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo S-HTTP (HTTPS)|--|443|  

###  <a name="a-namebkmkportsai-to-sqla-asset-intelligence-synchronization-point-----sql-server"></a><a name="BKMK_PortsAI-to-SQL"></a> Ponto de sincronização do Asset Intelligence -- &gt; SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 (Veja a observação 2, **Porta alternativa disponível**)|  

###  <a name="a-namebkmkportsappcatalogservice-sqla-application-catalog-web-service-point-----sql-server"></a><a name="BKMK_PortsAppCatalogService-SQL"></a> Ponto de serviços Web do catálogo de aplicativos -- &gt; SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 (Veja a observação 2, **Porta alternativa disponível**)|  

###  <a name="a-namebkmkportsappcatalogwebsitepointappcatalogwebservicepointa-application-catalog-website-point-----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> Ponto de sites da Web do catálogo de aplicativos -- &gt; Ponto de serviços Web do catálogo de aplicativos  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP|--|80 (Veja a observação 2, **Porta alternativa disponível**)|  
|Protocolo S-HTTP (HTTPS)|--|443 (Veja a observação 2, **Porta alternativa disponível**)|  

###  <a name="a-namebkmkportsclient-appcatalogwebsitepointa-client-----application-catalog-website-point"></a><a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> Cliente -- &gt; Ponto de sites da Web do catálogo de aplicativos  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP|--|80 (Veja a observação 2, **Porta alternativa disponível**)|  
|Protocolo S-HTTP (HTTPS)|--|443 (Veja a observação 2, **Porta alternativa disponível**)|  

###  <a name="a-namebkmkportsclient-clientwakeupa-client-----client"></a><a name="BKMK_PortsClient-ClientWakeUp"></a> Cliente -- &gt; Cliente  
 Além das portas relacionadas na tabela a seguir, o proxy de ativação também utiliza mensagens de solicitação de eco do protocolo ICMP de um cliente para outro quando estão configurados com o proxy de ativação. Essa comunicação é usada para confirmar se o outro computador cliente está ativo na rede. O ICMP é, por vezes, referido como comandos ping TCP/IP. O ICMP não tem um número de protocolo UDP ou TCP, portanto, não está listado na tabela a seguir. No entanto, todos os firewalls baseados em host nesses computadores cliente ou dispositivos de rede de intervenção dentro da sub-rede devem permitir o tráfego de ICMP para que a comunicação de proxy de ativação tenha êxito.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Wake on LAN|9 (Veja a observação 2, **Porta alternativa disponível**)|--|  
|Proxy de ativação|25536 (Veja a observação 2, **Porta alternativa disponível**)|--|  

###  <a name="a-namebkmkportsclient-policymodulea-client-----configuration-manager-policy-module-network-device-enrollment-service"></a><a name="BKMK_PortsClient-PolicyModule"></a> Cliente -- &gt; Módulo de política do Configuration Manager (Serviço de Registro de Dispositivo de Rede)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP||80|  
|Protocolo S-HTTP (HTTPS)|--|443|  

###  <a name="a-namebkmkportsclient-clouddpa-client-----cloud-based-distribution-point"></a><a name="BKMK_PortsClient-CloudDP"></a> Cliente -- &gt; Ponto de distribuição baseado em nuvem  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo S-HTTP (HTTPS)|--|443|  

###  <a name="a-namebkmkportsclient-dpa-client-----distribution-point"></a><a name="BKMK_PortsClient-DP"></a> Cliente -- &gt; Ponto de distribuição  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP|--|80 (Veja a observação 2, **Porta alternativa disponível**)|  
|Protocolo S-HTTP (HTTPS)|--|443 (Veja a observação 2, **Porta alternativa disponível**)|  

###  <a name="a-namebkmkportsclient-dp2a-client-----distribution-point-configured-for-multicast"></a><a name="BKMK_PortsClient-DP2"></a> Cliente -- &gt; Ponto de distribuição configurado para multicast  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Protocolo de multicast|63000-64000|--|  

###  <a name="a-namebkmkportsclient-dp3a-client-----distribution-point-configured-for-pxe"></a><a name="BKMK_PortsClient-DP3"></a> Cliente -- &gt; Ponto de distribuição configurado para PXE  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo DHCP|67 e 68|--|  
|Protocolo TFTP|69 (Consulte a observação 4 **Trivial FTP (TFTP) Daemon**)|--|  
|BINL (Boot Information Negotiation Layer)|4011|--|  

###  <a name="a-namebkmkportsclient-fspa-client-----fallback-status-point"></a><a name="BKMK_PortsClient-FSP"></a> Cliente -- &gt; Ponto de status de fallback  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP|--|80 (Veja a observação 2, **Porta alternativa disponível**)|  

###  <a name="a-namebkmkportsclient-gcdca-client-----global-catalog-domain-controller"></a><a name="BKMK_PortsClient-GCDC"></a> Cliente -- &gt; Controlador de domínio de catálogo global  
 Clientes do Configuration Manager não entram em contato com servidores de catálogo global quando eles estão em um computador de grupo de trabalho ou configurados para comunicação somente via Internet.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP de catálogo global|--|3268|  
|LDAP SSL de catálogo global|--|3269|  

###  <a name="a-namebkmkportsclient-mpa-client-----management-point"></a><a name="BKMK_PortsClient-MP"></a> Cliente -- &gt; Ponto de gerenciamento  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Notificação do cliente (comunicação padrão antes de retornar para HTTP ou HTTPS)|--|10123 (Veja a observação 2, **Porta alternativa disponível**)|  
|Protocolo HTTP|--|80 (Veja a observação 2, **Porta alternativa disponível**)|  
|Protocolo S-HTTP (HTTPS)|--|443 (Veja a observação 2, **Porta alternativa disponível**)|  

###  <a name="a-namebkmkportsclient-supa-client-----software-update-point"></a><a name="BKMK_PortsClient-SUP"></a> Cliente -- &gt; Ponto de atualização de software  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP|--|80 ou 8530 (Consulte a observação 3, **Windows Server Update Services**)|  
|Protocolo S-HTTP (HTTPS)|--|443 ou 8531 (Consulte a observação 3, **Windows Server Update Services**)|  

###  <a name="a-namebkmkportsclient-smpa-client-----state-migration-point"></a><a name="BKMK_PortsClient-SMP"></a> Cliente -- &gt; Ponto de migração de estado  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP|--|80 (Veja a observação 2, **Porta alternativa disponível**)|  
|Protocolo S-HTTP (HTTPS)|--|443 (Veja a observação 2, **Porta alternativa disponível**)|  
|Protocolo SMB|--|445|  

###  <a name="a-namebkmkportsconsole-clienta-configuration-manager-console-----client"></a><a name="BKMK_PortsConsole-Client"></a> Console do Configuration Manager -- &gt; Cliente  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Controle remoto (controle)|--|2701|  
|Assistência remota (RDP e RTC)|--|3389|  

###  <a name="a-namebkmkportsconsole-interneta-configuration-manager-console-----internet"></a><a name="BKMK_PortsConsole-Internet"></a> Console do Configuration Manager -- &gt; Internet  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP|--|80|  

###  <a name="a-namebkmkportsconsole-rspa-configuration-manager-console-----reporting-services-point"></a><a name="BKMK_PortsConsole-RSP"></a> Console do Configuration Manager -- &gt; Ponto do Reporting Services  

||||  
|-|-|-|  
|Descrição|UDP|TCP|  
|Protocolo HTTP|--|80 (Veja a observação 2, **Porta alternativa disponível**)|  
|Protocolo S-HTTP (HTTPS)|--|443 (Veja a observação 2, **Porta alternativa disponível**)|  

###  <a name="a-namebkmkportsconsole-sitea-configuration-manager-console-----site-server"></a><a name="BKMK_PortsConsole-Site"></a> Console do Configuration Manager -- &gt; Servidor do site  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (conexão inicial com o WMI para localizar o sistema do provedor)|--|135|  

###  <a name="a-namebkmkportsconsole-providera-configuration-manager-console-----sms-provider"></a><a name="BKMK_PortsConsole-Provider"></a> Console do Configuration Manager -- &gt; Provedor de SMS  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO (consulte a nota 6, **Portas dinâmicas**)|  

###  <a name="a-namebkmkportscertificateregistationpointpolicymodulea-configuration-manager-policy-module-network-device-enrollment-service-----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Módulo de política do Configuration Manager (Serviço de Registro de Dispositivo de Rede) -- &gt; Ponto de registro de certificado  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo S-HTTP (HTTPS)|--|443 (Veja a observação 2, **Porta alternativa disponível**)|  

###  <a name="a-namebkmkportsdistmpa-distribution-point-----management-point"></a><a name="BKMK_PortsDist_MP"></a> Ponto de distribuição --&gt; Ponto de gerenciamento  
 Um ponto de distribuição se comunica com o ponto de gerenciamento nos seguintes cenários:  

-   Para relatar o status do conteúdo pré-configurado  

-   Para relatar dados de resumo de uso  

-   Para relatar a validação de conteúdo  

-   Um ponto de distribuição de recepção relata o status de download do pacote  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP|--|80 (Veja a observação 2, **Porta alternativa disponível**)|  
|Protocolo S-HTTP (HTTPS)|--|443 (Veja a observação 2, **Porta alternativa disponível**)|  

###  <a name="a-namebkmkportsendpointprotectioninterneta-endpoint-protection-point-----internet"></a><a name="BKMK_PortsEndpointProtection_Internet"></a> Ponto do Endpoint Protection -- &gt; Internet  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP|--|80|  

###  <a name="a-namebkmkportsep-to-sqla-endpoint-protection-point-----sql-server"></a><a name="BKMK_PortsEP-to-SQL"></a> Ponto do Endpoint Protection -- &gt; SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 (Veja a observação 2, **Porta alternativa disponível**)|  

###  <a name="a-namebkmkportsenrollmentproxyenrollmentpointa-enrollment-proxy-point-----enrollment-point"></a><a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> Ponto proxy do registro -- &gt; Ponto de registro  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo S-HTTP (HTTPS)|--|443 (Veja a observação 2, **Porta alternativa disponível**)|  

###  <a name="a-namebkmkportsenrollmentenrollmentsqla-enrollment-point-----sql-server"></a><a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> Ponto de registro -- &gt; SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 (Veja a observação 2, **Porta alternativa disponível**)|  

###  <a name="a-namebkmkportsexchangeconnectorhosteda-exchange-server-connector-----exchange-online"></a><a name="BKMK_PortsExchangeConnectorHosted"></a> Conector do Exchange Server -- &gt; Exchange Online  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Gerenciamento Remoto do Windows via HTTPS|--|5986|  

###  <a name="a-namebkmkportsexchangeconnectoronprema-exchange-server-connector-----on-premises-exchange-server"></a><a name="BKMK_PortsExchangeConnectorOnPrem"></a> Conector do Exchange Server -- &gt; Exchange Server local  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Gerenciamento Remoto do Windows via HTTP|--|5985|  

###  <a name="a-namebkmkportsmacenrollmentproxypointa-mac-computer-----enrollment-proxy-point"></a><a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Computador Mac -- &gt; Ponto proxy do registro  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo S-HTTP (HTTPS)|--|443|  

###  <a name="a-namebkmkportsmp-dca-management-point-----domain-controller"></a><a name="BKMK_PortsMP-DC"></a> Ponto de gerenciamento -- &gt; Controlador de domínio  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo LDAP|--|389|  
|LDAP (conexão com protocolo SSL)|636|636|  
|LDAP de catálogo global|--|3268|  
|LDAP SSL de catálogo global|--|3269|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO (consulte a nota 6, **Portas dinâmicas**)|  

###  <a name="a-namebkmkportsmp-sitea-management-point-lt-----site-server"></a><a name="BKMK_PortsMP-Site"></a> Ponto de gerenciamento &lt; -- > Servidor do site  
 (Consulte a observação 5, **Comunicação entre o servidor do site e sistemas de site**)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Mapeador de ponto de extremidade RPC|--|135|  
|RPC|--|DINÂMICO (consulte a nota 6, **Portas dinâmicas**)|  
|Protocolo SMB|--|445|  

###  <a name="a-namebkmkportsmp-sqla-management-point-----sql-server"></a><a name="BKMK_PortsMP-SQL"></a> Ponto de gerenciamento -- &gt; SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 (Veja a observação 2, **Porta alternativa disponível**)|  

###  <a name="a-namebkmkportsmobiledeviceclient-enrollmentproxypointa-mobile-device-----enrollment-proxy-point"></a><a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> Dispositivo móvel -- &gt; Ponto proxy do registro  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo S-HTTP (HTTPS)|--|443|  

###  <a name="a-namebkmkportsmobiledeviceclient-windowsintunea-mobile-device-----microsoft-intune"></a><a name="BKMK_PortsMobileDeviceClient-WindowsIntune"></a> Dispositivo móvel--&gt; Microsoft Intune  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo S-HTTP (HTTPS)|--|443|  

###  <a name="a-namebkmkportsrsp-sqla-reporting-services-point-----sql-server"></a><a name="BKMK_PortsRSP-SQL"></a> Ponto do Reporting Services -- &gt; SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 (Consulte a observação 2, Porta alternativa disponível)|  

###  <a name="a-namebkmkportsintuneconnector-windowsintunea-service-connection-point-----microsoft-intune"></a><a name="BKMK_PortsIntuneConnector-WindowsIntune"></a> Ponto de conexão de serviço--&gt; Microsoft Intune  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo S-HTTP (HTTPS)|--|443|
Para obter mais informações, consulte [Requisitos de acesso à Internet](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls) para o ponto de conexão de serviço.

###  <a name="a-namebkmkportsappcatalogwebservicepointsiteservera-site-server-lt-----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> Servidor do site &lt; -- > Ponto de serviços Web do catálogo de aplicativos  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO (consulte a nota 6, **Portas dinâmicas**)|  

###  <a name="a-namebkmkportsappcatalogwebsitepointsiteservera-site-server-lt-----application-catalog-website-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> Servidor do site &lt; -- > Ponto de sites da Web do catálogo de aplicativos  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO (consulte a nota 6, **Portas dinâmicas**)|  

###  <a name="a-namebkmkportssite-aispa-site-server-lt-----asset-intelligence-synchronization-point"></a><a name="BKMK_PortsSite-AISP"></a> Servidor do site &lt; -- > Ponto de sincronização do Asset Intelligence  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO (consulte a nota 6, **Portas dinâmicas**)|  

###  <a name="a-namebkmkportssite-clienta-site-server-----client"></a><a name="BKMK_PortsSite-Client"></a> Servidor do site -- &gt; Cliente  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Wake on LAN|9 (Veja a observação 2, **Porta alternativa disponível**)|--|  

###  <a name="a-namebkmkportssiteserver-clouddpa-site-server-----cloud-based-distribution-point"></a><a name="BKMK_PortsSiteServer-CloudDP"></a> Servidor do site -- &gt; Ponto de distribuição baseado em nuvem  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo S-HTTP (HTTPS)|--|443|  

###  <a name="a-namebkmkportssite-dpa-site-server-----distribution-point"></a><a name="BKMK_PortsSite-DP"></a> Servidor do site -- &gt; Ponto de distribuição  
 (Consulte a observação 5, **Comunicação entre o servidor do site e sistemas de site**)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO (consulte a nota 6, **Portas dinâmicas**)|  

###  <a name="a-namebkmkportssite-dca-site-server-----domain-controller"></a><a name="BKMK_PortsSite-DC"></a> Servidor do site -- &gt; Controlador de domínio  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo LDAP|--|389|  
|LDAP (conexão com protocolo SSL)|636|636|  
|LDAP de catálogo global|--|3268|  
|LDAP SSL de catálogo global|--|3269|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO (consulte a nota 6, **Portas dinâmicas**)|  

###  <a name="a-namebkmkportscertificateregistrationpointsiteservera-site-server-lt-----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> Servidor do site &lt; -- > Ponto de registro de certificado  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO (consulte a nota 6, **Portas dinâmicas**)|  

###  <a name="a-namebkmkportsendpointprotectionsiteservera-site-server-lt-----endpoint-protection-point"></a><a name="BKMK_PortsEndpointProtection_SiteServer"></a> Servidor do site &lt; -- > Ponto do Endpoint Protection  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO (consulte a nota 6, **Portas dinâmicas**)|  

###  <a name="a-namebkmkenrollmentpointsiteservera-site-server-lt-----enrollment-point"></a><a name="BKMK_EnrollmentPoint_SiteServer"></a> Servidor do site &lt; -- > Ponto de registro  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO (consulte a nota 6, **Portas dinâmicas**)|  

###  <a name="a-namebkmkenrollmentproxypointsiteservera-site-server-lt-----enrollment-proxy-point"></a><a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> Servidor do site &lt; -- > Ponto proxy do registro  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO (consulte a nota 6, **Portas dinâmicas**)|  

###  <a name="a-namebkmkportssite-fspa-site-server-lt-----fallback-status-point"></a><a name="BKMK_PortsSite-FSP"></a> Servidor do site &lt; -- > Ponto de status de fallback  
 (Consulte a observação 5, **Comunicação entre o servidor do site e sistemas de site**)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO (consulte a nota 6, **Portas dinâmicas**)|  

###  <a name="a-namebkmkportsite-interneta-site-server-----internet"></a><a name="BKMK_PortSite-Internet"></a> Servidor do site -- &gt; Internet  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP|--|80 (Consulte a observação 1, **Porta do servidor proxy**)|  

###  <a name="a-namebkmkportsissuingcasiteservera-site-server-lt-----issuing-certification-authority-ca"></a><a name="BKMK_PortsIssuingCA_SiteServer"></a> Servidor do site &lt; -- > AC (Autoridade de Certificação) emissora  
 Essa comunicação é usada quando você implanta perfis de certificado usando o ponto de registro de certificado. A comunicação não é usada para cada servidor do site na hierarquia; é usada apenas para o servidor do site na parte superior da hierarquia.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC (DCOM)|--|DINÂMICO (consulte a nota 6, **Portas dinâmicas**)|  

###  <a name="a-namebkmkportssite-rspa-site-server-lt-----reporting-services-point"></a><a name="BKMK_PortsSite-RSP"></a> Servidor do site &lt; -- > Ponto do Reporting Services  
 (Consulte a observação 5, **Comunicação entre o servidor do site e sistemas de site**)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO (consulte a nota 6, **Portas dinâmicas**)|  

###  <a name="a-namebkmkportssite-sitea-site-server-lt-----site-server"></a><a name="BKMK_PortsSite-Site"></a> Servidor do site &lt; -- > Servidor do site  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  

###  <a name="a-namebkmkportssite-sqla-site-server-----sql-server"></a><a name="BKMK_PortsSite-SQL"></a> Servidor do site -- &gt; SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 (Veja a observação 2, **Porta alternativa disponível**)|  

 Durante a instalação de um site que usará o SQL Server remoto para hospedar o banco de dados do site, é necessário abrir as seguintes portas entre o servidor do site e o SQL Server:  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO (consulte a nota 6, **Portas dinâmicas**)|  

###  <a name="a-namebkmkportssite-providera-site-server-----sms-provider"></a><a name="BKMK_PortsSite-Provider"></a> Servidor do site -- &gt; Provedor de SMS  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO (consulte a nota 6, **Portas dinâmicas**)|  

###  <a name="a-namebkmkportssite-supa-site-server-lt-----software-update-point"></a><a name="BKMK_PortsSite-SUP"></a> Servidor do site &lt; -- > Ponto de atualização de software  
 (Consulte a observação 5, **Comunicação entre o servidor do site e sistemas de site**)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Protocolo HTTP|--|80 ou 8530 (Consulte a observação 3, Windows Server Update Services)|  
|Protocolo S-HTTP (HTTPS)|--|443 ou 8531 (Consulte a observação 3, Windows Server Update Services)|  

###  <a name="a-namebkmkportssite-smpa-site-server-lt-----state-migration-point"></a><a name="BKMK_PortsSite-SMP"></a> Servidor do site &lt; -- > Ponto de migração de estado  
 (Consulte a observação 5, **Comunicação entre o servidor do site e sistemas de site**)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  

###  <a name="a-namebkmkportsprovider-sqla-sms-provider-----sql-server"></a><a name="BKMK_PortsProvider-SQL"></a> Provedor de SMS -- &gt; SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 (Consulte a observação 2, Porta alternativa disponível)|  

###  <a name="a-namebkmkportssup-interneta-software-update-point-----internet"></a><a name="BKMK_PortsSUP-Internet"></a> Ponto de atualização de software -- &gt; Internet  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP|--|80 (Consulte a observação 1, **Porta do servidor proxy**)|  

###  <a name="a-namebkmkportssup-wsusa-software-update-point-----upstream-wsus-server"></a><a name="BKMK_PortsSUP-WSUS"></a> Ponto de atualização de software -- &gt; Servidor upstream do WSUS  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP|--|80 ou 8530 (Consulte a observação 3, **Windows Server Update Services**)|  
|Protocolo S-HTTP (HTTPS)|--|443 ou 8531 (Consulte a observação 3, **Windows Server Update Services**)|  

###  <a name="a-namebkmkportssql-sqla-sql-server----sql-server"></a><a name="BKMK_PortsSQL-SQL"></a> SQL Server -- &gt; SQL Server  
 A replicação de banco de dados entre sites requer o SQL Server em um site para se comunicar diretamente com o SQL Server de seu site pai ou filho.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Serviço SQL Server|--|1433 (Consulte a observação 2, Porta alternativa disponível)|  
|SQL Server Service Broker|--|4022 (Veja a observação 2, Porta alternativa disponível)|  

> [!TIP]  
>  O Configuration Manager não exige o SQL Server Browser, que usa a porta UDP 1434.  

###  <a name="a-namebkmkportsstatemigrationpoint-to-sqla-state-migration-point-----sql-server"></a><a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> Ponto de migração de estado --&gt; SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 (Veja a observação 2, **Porta alternativa disponível**)|  



###  <a name="a-namebkmyportnotesa-notes-for-ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMY_PortNotes"></a> Observações de portas usadas por clientes do Gerenciador de Configurações e sistemas de site  

1.  **Porta do servidor proxy**: esta porta não pode ser configurada, mas pode ser roteada por meio de um servidor proxy configurado.  

2.  **Porta alternativa disponível**: uma porta alternativa pode ser definida dentro do Configuration Manager para esse valor. Se tiver sido definida uma porta personalizada, substitua essa porta personalizada ao definir as informações de filtro IP para políticas IPsec ou para configurar firewalls.  

3.  **Windows Server Update Services**: o WSUS pode ser instalado no site da Web padrão (porta 80) ou em um site da Web personalizado (porta 8530).  

     Após a instalação, a porta pode ser alterada. Não é necessário usar o mesmo número de porta em toda a hierarquia do site.  

    -   Se a porta HTTP for 80, a porta HTTPS deverá ser 443.  

    -   Se a porta HTTP tiver outro número, a porta HTTPS deverá ser um número acima. Por exemplo, 8530 e 8531.  

    > [!NOTE]  
    >  Ao configurar o ponto de atualização de software para usar HTTPS, a porta HTTP deve também ser aberta. Dados não criptografados, como o EULA para atualizações específicas, usam a porta HTTP.  

4.  **Trivial FTP (TFTP) Daemon**: o serviço do sistema Trivial FTP (TFTP) Daemon não requer um nome de usuário ou senha e é parte integral do Windows Deployment Services (WDS). O serviço Trivial FTP Daemon implementa suporte ao protocolo TFTP definido pelos seguintes RFCs:  

    -   RFC 350 – TFTP  

    -   RFC 2347 – Opções de extensão  

    -   RFC 2348 – Opções de tamanho de bloco  

    -   RFC 2349 – Opções de intervalo de tempo limite e de tamanho da transferência  

     O Protocolo TFTP é projetado para oferecer suporte a ambientes de inicialização sem disco. O TFTP Daemons escuta na porta UDP 69, mas responde de uma porta alta alocada dinamicamente. Portanto, a ativação dessa porta permitirá que o serviço TFTP receba solicitações TFTP de entrada, mas não permitirá que o servidor selecionado responda a essas solicitações. A permissão para que o servidor selecionado responda às solicitações TFTP de entrada não pode ser obtida, a menos que o servidor TFTP esteja configurado para responder da porta 69.  

5.  **Comunicação entre o servidor do site e os sistemas de sites**: por padrão, a comunicação entre o servidor do site e os sistemas de site é bidirecional. O servidor do site inicia a comunicação para configurar o sistema de site, e então a maior parte dos sistemas de site se conecta de volta ao servidor do site para enviar informações de status. Pontos do Reporting Services e pontos de distribuição não enviam informações de status. Se você selecionar **Exigir que o servidor do site inicie conexões com este sistema de site** nas propriedades do sistema de site, depois que o sistema de site estiver instalado, ele não iniciará comunicação com o servidor do site. Em vez disso, o servidor do site iniciará as conexões e utilizará a conta de instalação do sistema de site para se autenticar no servidor do sistema de site.  

6.  **Portas dinâmicas**: as portas dinâmicas (também conhecidas como portas efêmeras) usam um intervalo de número de porta definido pela versão do sistema operacional. Para obter mais informações sobre os intervalos de porta padrão, consulte [Visão geral do serviço e requisitos de porta de rede para o Windows](http://go.microsoft.com/fwlink/p/?LinkId=317965).  

##  <a name="a-namebkmkadditionalportsa-additional-lists-of-ports"></a><a name="BKMK_AdditionalPorts"></a> Listas de portas adicionais  
 As seções a seguir fornecem informações adicionais sobre as portas usadas pelo Configuration Manager.  

###  <a name="a-namebkmkclientsharesa-client-to-server-shares"></a><a name="BKMK_ClientShares"></a> Compartilhamentos de cliente para servidor  
 Os clientes usam o protocolo SMB sempre que se conectam aos compartilhamentos UNC. Por exemplo:  

-   Instalação manual do cliente que especifica a propriedade da linha de comando CCMSetup.exe **/source:** .  

-   Clientes do Endpoint Protection que baixam arquivos de definição de um caminho UNC.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  

###  <a name="a-namebkmksqlportsa-connections-to-microsoft-sql-server"></a><a name="BKMK_SQLPorts"></a> Conexões com o Microsoft SQL Server  
 Para fazer comunicação com o mecanismo de banco de dados do SQL Server e para fazer a replicação entre sites, é possível usar a porta do SQL Server padrão ou especificar portas personalizadas:  

-   Uso de comunicações entre sites:  

    -   SQL Server Service Broker, que usa como padrão a porta TCP 4022.  

    -   Serviço SQL Server, que usa como padrão a porta TCP 1433  

-   A comunicação entre sites entre o mecanismo de banco de dados do SQL Server e várias funções do sistema de sites do Configuration Manager padroniza a porta TCP 1433.  

> [!WARNING]  
>  O Configuration Manager não dá suporte a portas dinâmicas. Como as instâncias nomeadas do SQL Server por padrão usam as portas dinâmicas para fazer conexões com o mecanismo de banco de dados, ao usar uma instância nomeada, configure manualmente a porta estática que deseja usar para a comunicação entre sites.  

 As seguintes funções do sistema de site se comunicam diretamente com o banco de dados do SQL Server:  

-   Ponto de serviços Web do Catálogo de Aplicativos  

-   Função de ponto de registro de certificado  

-   Função de ponto de registro  

-   Ponto de gerenciamento  

-   Servidor do site  

-   Ponto do Reporting Services  

-   Provedor de SMS  

-   SQL Server -- > SQL Server  

Quando um SQL Server hospeda bancos de dados de mais de um site, cada banco de dados deve usar uma instância separada do SQL Server, e cada instância deve ser configurada com um conjunto de portas exclusivo.  

Se você tiver um firewall habilitado no computador SQL Server, verifique se ele está configurado para permitir as portas em uso em sua implantação e em todos os locais na rede entre computadores que se comunicam com o SQL Server.  

Para obter um exemplo de como configurar o SQL Server para usar uma porta específica, veja [Como: configurar um servidor para escutar em uma porta TCP específica (SQL Server Configuration Manager)](http://go.microsoft.com/fwlink/p/?LinkID=226349) na biblioteca do TechNet do SQL Server.  


### <a name="bkmk_discovery"> </a> Descoberta e publicação
As seguintes portas são usadas para Descoberta e publicação de informações do site:
 - Protocolo LDAP – 389
 - LDAP (conexão com protocolo SSL) – 636


 - LDAP de catálogo global – 3268
 - LDAP SSL de catálogo global – 3269


 - Mapeador de ponto de extremidade RPC – 135
 - RPC – portas TCP altas alocadas dinamicamente


 - TCP: 1024 – 5000
 - TCP:  49152 – 65535


###  <a name="a-namebkmkexternala-external-connections-made-by-configuration-manager"></a><a name="BKMK_External"></a> Conexões externas feitas pelo Gerenciador de Configurações  
 Clientes do Configuration Manager ou sistemas de sites podem fazer as seguintes conexões externas:  

-   [Ponto de sincronização do Asset Intelligence -- &gt; Microsoft](#BKMK_PortsAI)  

-   [Ponto do Endpoint Protection -- &gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

-   [Cliente -- &gt; Controlador de domínio de catálogo global](#BKMK_PortsClient-GCDC)  

-   [Console do Configuration Manager -- &gt; Internet](#BKMK_PortsConsole-Internet)  

-   [Ponto de gerenciamento -- &gt; Controlador de domínio](#BKMK_PortsMP-DC)  

-   [Servidor do site -- &gt; Controlador de domínio](#BKMK_PortsSite-DC)  

-   [Servidor do site &lt; -- &gt; AC (Autoridade de Certificação) Emissora](#BKMK_PortsIssuingCA_SiteServer)  

-   [Ponto de atualização de software -- &gt; Internet](#BKMK_PortsSUP-Internet)  

-   [Ponto de atualização de software -- &gt; Servidor upstream do WSUS](#BKMK_PortsSUP-WSUS)  

-   [Ponto de conexão de serviço -- &gt; Microsoft Intune](#BKMK_PortsIntuneConnector-WindowsIntune)  

###  <a name="a-namebkmkibcmportsa-installation-requirements-for-site-systems-that-support-internet-based-clients"></a><a name="BKMK_IBCMports"></a> Requisitos de instalação para sistemas de site que oferecem suporte a clientes baseados na Internet  
 Os pontos de gerenciamento e os pontos de distribuição que oferecem suporte a clientes baseados em Internet, o ponto de atualização de software e o ponto de status de fallback usam as seguintes portas para instalação e reparo:  

-   Servidor do site --> sistema de sites: mapeador de ponto de extremidade RPC usando UDP e porta TCP 135.  

-   Servidor do site--> sistema de sites: portas TCP dinâmicas de RPC.  

-   Servidor do site &lt; --> sistema de sites: protocolo SMB usando porta TCP 445.  

Instalações de aplicativos e pacotes nos pontos de distribuição requerem as seguintes portas RPC:  

-   Servidor do site --> ponto de distribuição: mapeador de ponto de extremidade RPC usando UDP e porta TCP 135.  

-   Servidor do site--> ponto de distribuição: portas TCP dinâmicas de RPC  

Use o IPsec para ajudar a proteger o tráfego entre o servidor do site e os sistemas de site. Se for preciso restringir as portas dinâmicas usadas com RPC, você pode usar a ferramenta de configuração Microsoft RPC (rpccfg.exe) para configurar um intervalo restrito de portas para esses pacotes RPC. Para obter mais informações sobre a ferramenta de configuração RPC, consulte [Como configurar o RPC para usar determinadas portas e como ajudar a proteger essas portas usando o IPsec](http://go.microsoft.com/fwlink/p/?LinkId=124096).  

> [!IMPORTANT]  
>  Para poder instalar esses sistemas de site, verifique se o serviço de registro remoto está sendo executado no servidor de sistema de site e se você especificou uma conta de instalação de sistema de site, caso esse sistema esteja em uma floresta do Active Directory diferente, sem relação de confiança.  

###  <a name="a-namebkmkportsclientinstalla-ports-used-by-configuration-manager-client-installation"></a><a name="BKMK_PortsClientInstall"></a> Portas usadas pela instalação do cliente do Gerenciador de Configurações  
As portas usadas durante a instalação do cliente dependem do método de implantação do cliente. Consulte **Portas usadas durante a implantação do cliente do Configuration Manager**, no tópico [Firewall do Windows e configurações de porta para clientes no System Center Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md), para obter uma lista de portas para cada método de implantação de cliente. Para obter informações sobre como configurar o Firewall do Windows no cliente para instalação de cliente e comunicação pós-instalação, consulte [Firewall do Windows e configurações de porta para clientes no System Center Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md).  

###  <a name="a-namebkmkmigrationportsa-ports-used-by-migration"></a><a name="BKMK_MigrationPorts"></a> Portas usadas pela migração  
O servidor de site que executa a migração usa várias portas para se conectar a sites aplicáveis na hierarquia de origem para coletar dados do banco de dados do SQL Server dos sites de origem e para compartilhar pontos de distribuição.  

 Para obter informações sobre essas portas, consulte a seção [Configurações necessárias para a migração](../../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations) nos Pré-requisitos para o tópico [Pré-requisitos para a migração no System Center Configuration Manager](../../../core/migration/prerequisites-for-migration.md).  

###  <a name="a-namebkmkserverportsa-ports-used-by-windows-server"></a><a name="BKMK_ServerPorts"></a> Portas usadas pelo Windows Server  
 A tabela a seguir lista algumas das principais portas que o Windows Server usa e suas respectivas funções. Para obter uma lista completa dos serviços do Windows Server e requisitos de portas de rede, consulte [Visão geral de serviços e requisitos de porta de rede para o sistema do Windows Server](http://go.microsoft.com/fwlink/p/?LinkID=123652).  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|DNS (Sistema de Nomes de Domínio)|53|53|  
|Protocolo DHCP|67 e 68|--|  
|Resolução de nomes NetBIOS|137|--|  
|Serviço de datagrama NetBIOS|138|--|  
|Serviço de sessão NetBIOS|--|139|  



<!--HONumber=Dec16_HO3-->


