---
title: Portas usadas para conexões
titleSuffix: Configuration Manager
description: Saiba mais sobre as portas de rede necessárias e personalizáveis que o System Center Configuration Manager usa para conexões.
ms.date: 09/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b074ee02ec5e50fb5e495923538535cf8765dcdb
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53420933"
---
# <a name="ports-used-in-configuration-manager"></a>Portas usadas no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo lista as portas de rede usadas pelo Configuration Manager. Algumas conexões usam portas que não são configuráveis e algumas dão suporte a portas personalizadas que você especifica. Se você usar qualquer tecnologia de filtragem de porta, verifique se as portas necessárias estão disponíveis. Essas tecnologias de filtragem de porta incluem firewalls, roteadores, servidores proxy ou IPsec.   

> [!NOTE]  
>  Se houver suporte a clientes baseados na Internet usando a ponte SSL, além dos requisitos de porta, você também deverá permitir alguns verbos e cabeçalhos HTTP para percorrer seu firewall.   



##  <a name="BKMK_ConfigurablePorts"></a> Portas que você pode configurar  
 O Configuration Manager permite que você configure as portas para os seguintes tipos de comunicação:  

-   Ponto de sites da Web do catálogo de aplicativos com o ponto de serviços Web do catálogo de aplicativos  

-   Ponto proxy do registro com o ponto de registro  

-   Cliente para sistemas de sites que executam o IIS  

-   Cliente com Internet (como configurações do servidor proxy)  

-   Ponto de atualização de software com Internet (como configurações do servidor proxy)  

-   Ponto de atualização de software com o servidor WSUS  

-   Servidor do site com o servidor de banco de dados do site  

-   Pontos do Reporting Services  

    > [!NOTE]  
    >  As portas em uso para a função do sistema de sites do ponto do Reporting Services são configuradas no SQL Server Reporting Services. Essas portas são usadas pelo Configuration Manager durante comunicações com o ponto do Reporting Services. Lembre-se de verificar essas portas que definem as informações de filtro IP para políticas IPsec ou para configurar firewalls.  

Por padrão, a porta HTTP usada para comunicação do cliente com o sistema de sites é a porta 80 e a porta HTTPS padrão é 443. As portas para comunicação do cliente para o sistema de sites por HTTP ou HTTPS podem ser alteradas durante a instalação ou nas propriedades do site do Configuration Manager.  

As portas em uso para a função do sistema de sites do ponto do Reporting Services são configuradas no SQL Server Reporting Services. Essas portas são usadas pelo Configuration Manager durante comunicações com o ponto do Reporting Services. Lembre-se de verificar essas portas quando estiver definindo as informações de filtro IP para políticas IPsec ou para configurar firewalls.  



##  <a name="BKMK_NonConfigurablePorts"></a> Portas não configuráveis  

O Configuration Manager não permite que você configure as portas para os seguintes tipos de comunicação:  

-   Site a site  

-   Servidor do site com o sistema de site  

-   Console do Configuration Manager para Provedor de SMS  

-   Console do Configuration Manager para a Internet  

-   Conexões com serviços de nuvem, como o Microsoft Intune e pontos de distribuição em nuvem  



##  <a name="BKMK_CommunicationPorts"></a> Portas usadas por sistemas de site e clientes do Gerenciador de Configurações  

As seções a seguir detalham as portas usadas para comunicação no Configuration Manager. As setas no título da seção mostram a direção da comunicação:  

-   – > indica que um computador inicia a comunicação e o outro computador sempre responde  

-   &lt; – > indica que qualquer computador pode iniciar a comunicação  


###  <a name="BKMK_PortsAI"></a> Ponto de sincronização do Asset Intelligence – > Microsoft  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="BKMK_PortsAI-to-SQL"></a> Ponto de sincronização do Asset Intelligence – > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  


###  <a name="BKMK_PortsAppCatalogService-SQL"></a> Ponto de serviços Web do catálogo de aplicativos – > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  


###  <a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> Ponto de sites da Web do catálogo de aplicativos – > Ponto de serviços Web do catálogo de aplicativos  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|HTTPS|--|443 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  


###  <a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> Cliente – > Ponto de sites da Web do catálogo de aplicativos  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|HTTPS|--|443 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  


###  <a name="BKMK_PortsClient-ClientWakeUp"></a> Cliente -- &gt; Cliente  

Além das portas listadas nesta tabela, o proxy de ativação também usa mensagens de solicitação de eco ICMP de um cliente com outro cliente. Os clientes usam essa comunicação para confirmar se o outro cliente está ativo na rede. O ICMP é, às vezes, referido como comandos ping. O ICMP não tem um número de protocolo UDP ou TCP, portanto, não está listado na tabela abaixo. No entanto, todos os firewalls baseados em host nesses computadores cliente ou dispositivos de rede de intervenção dentro da sub-rede devem permitir o tráfego de ICMP para que a comunicação de proxy de ativação tenha êxito.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Wake On LAN|9 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|--|  
|Proxy de ativação|25536 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|--|  


###  <a name="BKMK_PortsClient-PolicyModule"></a> Cliente -- > módulo de política NDES (Serviço de Registro de Dispositivo de Rede) do Configuration Manager   

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP||80|  
|HTTPS|--|443|  


###  <a name="BKMK_PortsClient-CloudDP"></a> Cliente -- > Ponto de distribuição em nuvem  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Para obter mais informações, veja [Portas e fluxo de dados](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_dataflow).


###  <a name="bkmk_client-cmg"></a> Cliente -- > CMG (Gateway de Gerenciamento de Nuvem)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Para obter mais informações, veja [Portas e fluxo de dados do CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#ports-and-data-flow).


###  <a name="BKMK_PortsClient-DP"></a> Cliente – > Ponto de distribuição  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|HTTPS|--|443 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  


###  <a name="BKMK_PortsClient-DP2"></a> Cliente – > Ponto de distribuição configurado para multicast  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Protocolo de multicast|63000-64000|--|  

###  <a name="BKMK_PortsClient-DP3"></a> Cliente – > Ponto de distribuição configurado para PXE  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|DHCP|67 e 68|--|  
|TFTP|69 <sup>[Observação 4](#bkmk_note4)</sup> |--|  
|BINL (Boot Information Negotiation Layer)|4011|--|  

> [!Important]  
> Se você habilitar um firewall baseado em host, verifique se as regras permitem que o servidor envie e receba nessas portas. Quando você habilita um ponto de distribuição para PXE, o Configuration Manager pode habilitar a entrada (recebimento) as regras de Firewall do Windows. Ele não configura as regras de saída (envio).<!--SCCMDocs issue #744-->  


###  <a name="BKMK_PortsClient-FSP"></a> Cliente – > Ponto de status de fallback  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  


###  <a name="BKMK_PortsClient-GCDC"></a> Cliente – > Controlador de domínio de catálogo global  
 Clientes do Configuration Manager não entram em contato com servidores de catálogo global quando eles estão em um computador de grupo de trabalho ou configurados para comunicação somente via Internet.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP de catálogo global|--|3268|  


###  <a name="BKMK_PortsClient-MP"></a> Cliente – > Ponto de gerenciamento  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Notificação do cliente (comunicação padrão antes de retornar para HTTP ou HTTPS)|--|10123 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|HTTP|--|80 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|HTTPS|--|443 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  


###  <a name="BKMK_PortsClient-SUP"></a> Cliente – > Ponto de atualização de software  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 ou 8530 <sup>[Observação 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 ou 8531 <sup>[Observação 3](#bkmk_note3)</sup>|  


###  <a name="BKMK_PortsClient-SMP"></a> Cliente – > Ponto de migração de estado  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|HTTPS|--|443 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|Protocolo SMB|--|445|  


###  <a name="bkmk_cmgcp-cmg"></a> Ponto de conexão do CMG -- > serviço de nuvem do CMG  

O Configuration Manager usa essas conexões para criar o canal do CMG. Para obter mais informações, veja [Portas e fluxo de dados do CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#ports-and-data-flow).

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|TCP-TLS (preferencial)|--|10140-10155|  
|HTTPS (fallback com uma VM)|--|443|  
|HTTPS (fallback com duas ou mais VMs)|--|10124-10139|  


###  <a name="bkmk_cmgcp-mp"></a> Ponto de conexão do CMG -- > Ponto de gerenciamento  

#### <a name="version-1706-or-1710"></a>Versão 1706 ou 1710
A porta específica depende da configuração do ponto de gerenciamento. 

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|
|HTTP|--|80|  

#### <a name="version-1802"></a>Versão 1802

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|

Para obter mais informações, veja [Portas e fluxo de dados do CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#ports-and-data-flow).


###  <a name="bkmk_cmgcp-sup"></a> Ponto de conexão do CMG -- > Ponto de atualização de software  

A porta específica depende da configuração do ponto de atualização de software. 

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|
|HTTP|--|80|  

Para obter mais informações, veja [Portas e fluxo de dados do CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#ports-and-data-flow).


###  <a name="BKMK_PortsConsole-Client"></a> Console do Configuration Manager – > Cliente  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Controle remoto (controle)|--|2701|  
|Assistência remota (RDP e RTC)|--|3389|  


###  <a name="BKMK_PortsConsole-Internet"></a> Console do Configuration Manager – > Internet  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  
|HTTPS|--|443|

O console do Configuration Manager usa o acesso à Internet para as seguintes ações: 
- Baixar atualizações de software do Microsoft Update para pacotes de implantação.
- O item Comentários na faixa de opções.
- Links para documentação no console.
<!--506823-->


###  <a name="BKMK_PortsConsole-RSP"></a> Console do Configuration Manager -- > Ponto do Reporting Services  


|Descrição|UDP|TCP|
|-----------------|---------|---------|   
|HTTP|--|80 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|HTTPS|--|443 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  


###  <a name="BKMK_PortsConsole-Site"></a> Console do Configuration Manager – > Servidor do site  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (conexão inicial com o WMI para localizar o sistema do provedor)|--|135|  


###  <a name="BKMK_PortsConsole-Provider"></a> Console do Configuration Manager – > Provedor de SMS  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO <sup>[Observação 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Módulo de política do NDES (Serviço de Registro de Dispositivo de Rede) do Configuration Manager -- > Ponto de registro de certificado  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  


###  <a name="BKMK_PortsDWSPSQL"></a> Ponto de serviço do data warehouse -- > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  


###  <a name="BKMK_PortsDist_MP"></a> Ponto de distribuição – > Ponto de gerenciamento  
 Um ponto de distribuição se comunica com o ponto de gerenciamento nos seguintes cenários:  

-   Para relatar o status do conteúdo pré-teste  

-   Para relatar dados de resumo de uso  

-   Para relatar a validação de conteúdo  

-   Para relatar o status dos downloads de pacote (ponto de distribuição pull)

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|HTTPS|--|443 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  


###  <a name="BKMK_PortsEndpointProtection_Internet"></a> Ponto do Endpoint Protection – > Internet  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  


###  <a name="BKMK_PortsEP-to-SQL"></a> Ponto do Endpoint Protection – > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  


###  <a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> Ponto proxy do registro – > Ponto de registro  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  


###  <a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> Ponto de registro – > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  


###  <a name="BKMK_PortsExchangeConnectorHosted"></a> Conector do Exchange Server -- &gt; Exchange Online  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Gerenciamento Remoto do Windows via HTTPS|--|5986|  


###  <a name="BKMK_PortsExchangeConnectorOnPrem"></a> Conector do Exchange Server – > Exchange Server local  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Gerenciamento Remoto do Windows via HTTP|--|5985|  


###  <a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Computador Mac – > Ponto proxy do registro  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="BKMK_PortsMP-DC"></a> Ponto de gerenciamento – > Controlador de domínio  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo LDAP|389|389|  
|LDAP de catálogo global|--|3268|  
|Mapeador de ponto de extremidade RPC|--|135|  
|RPC|--|DINÂMICO <sup>[Observação 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsMP-Site"></a> Ponto de gerenciamento &lt; – > Servidor do site  
 <sup>[Observação 5](#bkmk_note5)</sup>   

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Mapeador de ponto de extremidade RPC|--|135|  
|RPC|--|DINÂMICO <sup>[Observação 6](#bkmk_note6)</sup>|  
|Protocolo SMB|--|445|  


###  <a name="BKMK_PortsMP-SQL"></a> Ponto de gerenciamento – > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  


###  <a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> Dispositivo móvel – > Ponto proxy do registro  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="BKMK_PortsMobileDeviceClient-WindowsIntune"></a> Dispositivo móvel – > Microsoft Intune  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="BKMK_PortsRSP-SQL"></a> Ponto do Reporting Services – > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  


###  <a name="BKMK_PortsIntuneConnector-WindowsIntune"></a> Ponto de conexão de serviço – > Microsoft Intune  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|

Para saber mais, confira [Requisitos de acesso à Internet](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls) para o ponto de conexão de serviço.


###  <a name="bkmk_scp-cmg"></a> Ponto de conexão de serviço -- > Azure (CMG)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS para a implantação do serviço CMG|--|443|

Para obter mais informações, veja [Portas e fluxo de dados do CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#ports-and-data-flow).


###  <a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> Servidor do site &lt; – > Ponto de serviços Web do catálogo de aplicativos  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO <sup>[Observação 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> Servidor do site &lt; – > Ponto de sites da Web do catálogo de aplicativos  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO <sup>[Observação 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-AISP"></a> Servidor do site &lt; – > Ponto de sincronização do Asset Intelligence  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO <sup>[Observação 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-Client"></a> Servidor do site – > Cliente  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Wake On LAN|9 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|--|  


###  <a name="BKMK_PortsSiteServer-CloudDP"></a> Servidor do site – > Ponto de distribuição em nuvem  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Para obter mais informações, veja [Portas e fluxo de dados](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_dataflow).


###  <a name="BKMK_PortsSite-DP"></a> Servidor do site – > Ponto de distribuição  
 <sup>[Observação 5](#bkmk_note5)</sup>  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO <sup>[Observação 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-DC"></a> Servidor do site – > Controlador de domínio  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo LDAP|389|389|  
|LDAP de catálogo global|--|3268|  
|Mapeador de ponto de extremidade RPC|--|135|  
|RPC|--|DINÂMICO <sup>[Observação 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> Servidor do site &lt; – > Ponto de registro de certificado  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO <sup>[Observação 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsEndpointProtection_SiteServer"></a> Servidor do site &lt; – > Ponto do Endpoint Protection  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO <sup>[Observação 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_EnrollmentPoint_SiteServer"></a> Servidor do site &lt; – > Ponto de registro  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO <sup>[Observação 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> Servidor do site &lt; – > Ponto proxy do registro  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO <sup>[Observação 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-FSP"></a> Servidor do site &lt; – > Ponto de status de fallback  
 <sup>[Observação 5](#bkmk_note5)</sup>  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO <sup>[Observação 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortSite-Internet"></a> Servidor do site – > Internet  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Observação 1](#bkmk_note1)</sup>|  


###  <a name="BKMK_PortsIssuingCA_SiteServer"></a> Servidor do site &lt; – > AC (Autoridade de Certificação) Emissora  
 Essa comunicação é usada quando você implanta perfis de certificado usando o ponto de registro de certificado. A comunicação não é usada para cada servidor do site na hierarquia. Em vez disso, ela é usada somente para o servidor do site na parte superior da hierarquia.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC (DCOM)|--|DINÂMICO <sup>[Observação 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-RSP"></a> Servidor do site &lt; – > Ponto do Reporting Services  
 <sup>[Observação 5](#bkmk_note5)</sup>  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO <sup>[Observação 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-Site"></a> Servidor do site &lt; – > Servidor do site  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  


###  <a name="BKMK_PortsSite-SQL"></a> Servidor do site – > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  

 Durante a instalação de um site que usa o SQL Server remoto para hospedar o banco de dados do site, abra as seguintes portas entre o servidor do site e o SQL Server:  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO <sup>[Observação 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-Provider"></a> Servidor do site – > Provedor de SMS  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  
|RPC|--|DINÂMICO <sup>[Observação 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-SUP"></a> Servidor do site &lt; – > Ponto de atualização de software  
 <sup>[Observação 5](#bkmk_note5)</sup>  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|HTTP|--|80 ou 8530 <sup>[Observação 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 ou 8531 <sup>[Observação 3](#bkmk_note3)</sup>|  


###  <a name="BKMK_PortsSite-SMP"></a> Servidor do site &lt; – > Ponto de migração de estado  
 <sup>[Observação 5](#bkmk_note5)</sup>  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  
|Mapeador de ponto de extremidade RPC|135|135|  


###  <a name="BKMK_PortsProvider-SQL"></a> Provedor de SMS -- &gt; SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  


###  <a name="BKMK_PortsSUP-Internet"></a> Ponto de atualização de software – > Internet  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Observação 1](#bkmk_note1)</sup>|  


###  <a name="BKMK_PortsSUP-WSUS"></a> Ponto de atualização de software – > Servidor upstream do WSUS  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 ou 8530 <sup>[Observação 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 ou 8531 <sup>[Observação 3](#bkmk_note3)</sup>|  


###  <a name="BKMK_PortsSQL-SQL"></a> SQL Server -- &gt; SQL Server  
 A replicação de banco de dados entre sites requer o SQL Server em um site para se comunicar diretamente com o SQL Server no seu site pai ou filho.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Serviço SQL Server|--|1433 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  
|SQL Server Service Broker|--|4022 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  

> [!TIP]  
>  O Configuration Manager não exige o SQL Server Browser, que usa a porta UDP 1434.  


###  <a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> Ponto de migração de estado – > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup>[Observação 2](#bkmk_note2) Porta alternativa disponível</sup>|  


###  <a name="BKMY_PortNotes"></a> Observações de portas usadas por clientes do Gerenciador de Configurações e sistemas de site  

#### <a name="bkmk_note1"></a> Observação 1: porta do servidor proxy
Esta porta não pode ser configurada, mas pode ser roteada por meio de um servidor proxy configurado.  

#### <a name="bkmk_note2"></a> Observação 2: porta alternativa disponível
Uma porta alternativa pode ser definida dentro do Configuration Manager para esse valor. Se tiver sido definida uma porta personalizada, substitua essa porta personalizada ao definir as informações de filtro IP para políticas IPsec ou para configurar firewalls.  

#### <a name="bkmk_note3"></a> Observação 3: Windows Server Update Services (WSUS)
O WSUS pode ser instalado para usar portas 80/443 ou portas 8530/8531 para comunicação do cliente. Ao executar o WSUS no Windows Server 2012 ou Windows Server 2016, o WSUS é configurado por padrão para usar a porta 8530 para HTTP e a porta 8531 para HTTPS.  

Após a instalação, é possível alterar a porta. Não é necessário usar o mesmo número da porta em toda a hierarquia do site.  

- Se a porta HTTP for 80, a porta HTTPS deverá ser 443.  

- Se a porta HTTP for outro número, a porta HTTPS deverá ser 1 número acima, por exemplo, 8530 e 8531.   

    > [!NOTE]  
    >  Ao configurar o ponto de atualização de software para usar HTTPS, a porta HTTP deve também ser aberta. Dados não criptografados, como o EULA para atualizações específicas, usam a porta HTTP.  

#### <a name="bkmk_note4"></a> Observação 4: daemon do TFTP (Trivial FTP)
O serviço do sistema Trivial FTP (TFTP) Daemon não requer um nome de usuário ou senha e é parte integral do WDS (Serviços de Implantação do Windows). O serviço Trivial FTP Daemon implementa o suporte ao protocolo TFTP definido pelos seguintes RFCs:  

- RFC 350: TFTP  

- RFC 2347: extensão da opção  

- RFC 2348: opção de tamanho de bloco  

- RFC 2349: opções de tamanho de transferência e de intervalo de tempo limite  

TFTP é projetado para dar suporte a ambientes de inicialização sem disco. O TFTP Daemons escuta na porta UDP 69, mas responde de uma porta alta alocada dinamicamente. Portanto, a habilitação dessa porta permite que o serviço TFTP receba solicitações TFTP de entrada, mas não permite que o servidor selecionado responda a essas solicitações. Não é possível habilitar o servidor selecionado para responder às solicitações TFTP de entrada a menos que o servidor TFTP esteja configurado para responder à porta 69.  

#### <a name="bkmk_note5"></a> Observação 5: a comunicação entre o servidor do site e o sistemas de site
Por padrão, a comunicação entre o servidor do site e os sistemas de site é bidirecional. O servidor do site inicia a comunicação para configurar o sistema de site, e então a maior parte dos sistemas de site se conecta de volta ao servidor do site para enviar informações de status. Pontos do Reporting Services e pontos de distribuição não enviam informações de status. Se você selecionar **Exigir que o servidor do site inicie conexões com este sistema de site** nas propriedades do sistema de sites depois que o sistema de sites tiver sido instalado, ele não iniciará a comunicação com o servidor. Em vez disso, o servidor do site iniciará a comunicação e utilizará a conta de instalação do sistema de sites para se autenticar no servidor do sistema de site.  

#### <a name="bkmk_note6"></a> Observação 6: Portas dinâmicas
As portas dinâmicas usam um intervalo de números de porta definidos pela versão do sistema operacional. Essas portas são também conhecidas como portas efêmeras. Para obter mais informações sobre os intervalos de porta padrão, consulte [Visão geral do serviço e requisitos de porta de rede para o Windows](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).  



##  <a name="BKMK_AdditionalPorts"></a> Listas de portas adicionais  

 As seções a seguir fornecem informações adicionais sobre as portas usadas pelo Configuration Manager.  

###  <a name="BKMK_ClientShares"></a> Compartilhamentos de cliente para servidor  

 Os clientes usam o protocolo SMB sempre que se conectam aos compartilhamentos UNC. Por exemplo:  

-   Instalação manual do cliente que especifica a propriedade da linha de comando CCMSetup.exe **/source:**  

-   Clientes do Endpoint Protection que baixam arquivos de definição de um caminho UNC

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo SMB|--|445|  


###  <a name="BKMK_SQLPorts"></a> Conexões com o Microsoft SQL Server  

 Para fazer comunicação com o mecanismo de banco de dados do SQL Server e para fazer a replicação entre sites, é possível usar a porta do SQL Server padrão ou especificar portas personalizadas:  

-   Uso de comunicações entre sites:  

    -   SQL Server Service Broker, que usa como padrão a porta TCP 4022.  

    -   Serviço SQL Server, que usa como padrão a porta TCP 1433.  

-   A comunicação entre sites entre o mecanismo de banco de dados do SQL Server e várias funções do sistema de sites do Configuration Manager padroniza a porta TCP 1433.  

- O Configuration Manager usará as mesmas portas e protocolos para se comunicar com cada réplica do Grupo de Disponibilidade do SQL que hospeda o banco de dados do site como se a réplica for uma instância autônoma do SQL Server.

Quando você usar o Azure e o banco de dados do site estiver atrás de um balanceador interno ou externo de carga, configure os seguintes componentes:
- Exceções de firewall em cada réplica
- Regras de balanceamento de carga 

Configure as seguintes portas:
 - SQL por TCP: TCP 1433
 - SQL Server Service Broker: TCP 4022
 - Protocolo SMB: TCP 445
 - Mapeador de pontos de extremidade RPC: TCP 135

> [!WARNING]  
>  O Configuration Manager não dá suporte a portas dinâmicas. Por padrão, as instâncias nomeadas do SQL Server usam portas dinâmicas para conexões com o mecanismo de banco de dados. Quando você usa uma instância nomeada, configure manualmente a porta estática para a comunicação entre sites.  

 As seguintes funções do sistema de site se comunicam diretamente com o banco de dados do SQL Server:  

-   Ponto de serviços Web do Catálogo de Aplicativos  

-   Função de ponto de registro de certificado  

-   Função de ponto de registro  

-   Ponto de gerenciamento  

-   Servidor do site  

-   Ponto do Reporting Services  

-   Provedor de SMS  

-   SQL Server -- > SQL Server  

Quando um SQL Server hospeda um banco de dados de mais de um site, cada banco de dados deve usar uma instância separada do SQL Server. Configure cada instância com um conjunto exclusivo de portas.  

Se você habilitar um firewall baseado em host no SQL Server, configure-o para permitir as portas corretas. Também configure firewalls de rede entre computadores que se comuniquem com o SQL Server.  

Para ver um exemplo sobre como configurar o SQL Server para usar uma porta específica, confira [Configurar um servidor para escutar em uma porta TCP específica](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  


### <a name="bkmk_discovery"> </a> Descoberta e publicação

O Configuration Manager usa as seguintes portas para a descoberta e publicação de informações do site:
 - Protocolo LDAP: 389
 - LDAP de catálogo global: 3268
 - Mapeador de pontos de extremidade RPC: 135
 - RPC: Portas TCP altas alocadas dinamicamente
 - TCP: 1024: 5000
 - TCP:  49152: 65535


###  <a name="BKMK_External"></a> Conexões externas feitas pelo Gerenciador de Configurações  

Clientes do Configuration Manager local ou sistemas de sites podem fazer as seguintes conexões externas:  

-   [Ponto de sincronização do Asset Intelligence – &gt; Microsoft](#BKMK_PortsAI)  

-   [Ponto do Endpoint Protection – &gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

-   [Cliente – &gt; Controlador de domínio de catálogo global](#BKMK_PortsClient-GCDC)  

-   [Console do Configuration Manager – &gt; Internet](#BKMK_PortsConsole-Internet)  

-   [Ponto de gerenciamento – &gt; Controlador de domínio](#BKMK_PortsMP-DC)  

-   [Servidor do site – &gt; Controlador de domínio](#BKMK_PortsSite-DC)  

-   [Servidor do site &lt; -- &gt; AC (Autoridade de Certificação) Emissora](#BKMK_PortsIssuingCA_SiteServer)  

-   [Ponto de atualização de software – &gt; Internet](#BKMK_PortsSUP-Internet)  

-   [Ponto de atualização de software – &gt; Servidor upstream do WSUS](#BKMK_PortsSUP-WSUS)  

-   [Ponto de conexão de serviço – &gt; Microsoft Intune](#BKMK_PortsIntuneConnector-WindowsIntune)  

- [Ponto de conexão de serviço -- > Azure](#bkmk_scp-cmg)  

- [Ponto de conexão do CMG -- > serviço de nuvem do CMG](#bkmk_cmgcp-cmg)  


###  <a name="BKMK_IBCMports"></a> Requisitos de instalação para sistemas de site que oferecem suporte a clientes baseados na Internet  

 > [!Note]  
 > Esta seção se aplica somente ao IBCM (gerenciamento de clientes baseados na Internet). Não se aplica ao Gateway de Gerenciamento de Nuvem. Para obter mais informações, veja [Gerenciar clientes na Internet](/sccm/core/clients/manage/manage-clients-internet).  

 Os pontos de gerenciamento baseados na Internet e os pontos de distribuição que dão suporte a clientes baseados em Internet, o ponto de atualização de software e o ponto de status de fallback usam as seguintes portas para instalação e reparo:  

-   Servidor do site --> sistema de sites: mapeador de ponto de extremidade RPC usando UDP e porta TCP 135.  

-   Servidor do site --> sistema de sites: Portas TCP dinâmicas de RPC  

-   Servidor do site &lt; --> sistema de sites: Protocolo SMB usando a porta TCP 445

Instalações de aplicativos e pacotes nos pontos de distribuição requerem as seguintes portas RPC:  

-   Servidor do site --> ponto de distribuição: Mapeador de pontos de extremidade RPC usando UDP e a porta TCP 135

-   Servidor do site --> ponto de distribuição: Portas TCP dinâmicas de RPC  

Use o IPsec para ajudar a proteger o tráfego entre o servidor do site e os sistemas de site. Se for preciso restringir as portas dinâmicas usadas com RPC, você pode usar a ferramenta de configuração Microsoft RPC (rpccfg.exe) para configurar um intervalo restrito de portas para esses pacotes RPC. Para obter mais informações sobre a ferramenta de configuração RPC, consulte [Como configurar o RPC para usar determinadas portas e como ajudar a proteger essas portas usando o IPsec](https://support.microsoft.com/help/908472/how-to-configure-rpc-to-use-certain-ports-and-how-to-help-secure-those).  

> [!IMPORTANT]  
>  Para poder instalar esses sistemas de sites, verifique se o serviço de Registro remoto está sendo executado no servidor de sistema de sites e se você especificou uma conta de instalação de sistema de site, caso esse sistema esteja em uma floresta do Active Directory diferente, sem relação de confiança.  


###  <a name="BKMK_PortsClientInstall"></a> Portas usadas pela instalação do cliente do Gerenciador de Configurações  

As portas usadas pelo Configuration Manager durante a instalação do cliente dependem do método de implantação. 

- Para obter uma lista de portas para cada método de implantação do cliente, veja [Portas usadas durante a implantação do cliente do Configuration Manager](/sccm/core/clients/deploy/windows-firewall-and-port-settings-for-clients#ports-used-during-configuration-manager-client-deployment)  

- Para obter mais informações sobre como configurar o Firewall do Windows no cliente para instalação de cliente e comunicação pós-instalação, veja [Configurações de porta e Firewall do Windows para clientes](/sccm/core/clients/deploy/windows-firewall-and-port-settings-for-clients)  


###  <a name="BKMK_MigrationPorts"></a> Portas usadas pela migração  

O servidor do site que executa a migração usa várias portas para se conectar aos sites aplicáveis na hierarquia de origem. Para obter mais informações, veja [Configurações necessárias para migração](/sccm/core/migration/prerequisites-for-migration#BKMK_Required_Configurations).  


###  <a name="BKMK_ServerPorts"></a> Portas usadas pelo Windows Server  

 A tabela a seguir lista algumas das principais portas usadas pelo Windows Server. 

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|DNS|53|53|  
|DHCP|67 e 68|--|  
|Resolução de nomes NetBIOS|137|--|  
|Serviço de datagrama NetBIOS|138|--|  
|Serviço de sessão NetBIOS|--|139|  
|Autenticação do Kerberos|--|88|

Para obter mais informações, consulte os seguintes artigos:
- [Visão geral de serviços e requisitos de porta de rede para o sistema Windows Server](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).  

- [Como configurar um firewall para domínios e relações de confiança](https://support.microsoft.com/help/179442/how-to-configure-a-firewall-for-domains-and-trusts)