---
title: Requisitos de acesso à Internet
titleSuffix: Configuration Manager
description: Saiba mais sobre os pontos de extremidade de Internet para permitir a funcionalidade completa dos recursos do Configuration Manager.
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9ab7816e017d48b937a634b5031ba80e7dbfa093
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67286961"
---
# <a name="internet-access-requirements"></a>Requisitos de acesso à Internet

Alguns recursos do Configuration Manager dependem da conectividade com a Internet para ter a funcionalidade completa. Se sua organização restringe a comunicação de rede com a Internet usando um dispositivo de firewall ou proxy, dê permissão a esses pontos de extremidade.

<!-- SCCMDocs-pr #3403 -->

## <a name="bkmk_scp"></a> Ponto de conexão de serviço

Essas configurações aplicam-se ao computador que hospeda o ponto de conexão de serviço e os firewalls entre o computador e a Internet. Ambos devem permitir a comunicação pela porta de saída **TCP 443** para HTTPS e pela porta de saída **TCP 80** para HTTP para os locais da Internet abaixo.

O ponto de conexão de serviço dá suporte ao uso de um proxy da Web (com ou sem autenticação) para acessar esses locais. Para obter mais informações, confira [Suporte ao servidor proxy](/sccm/core/plan-design/network/proxy-server-support).

Para saber mais sobre o ponto de conexão de serviço, confira [Sobre o ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point).

> [!TIP]  
> O ponto de conexão de serviço usa o serviço Microsoft Intune ao se conectar ao `go.microsoft.com` ou ao `manage.microsoft.com`. Há um problema conhecido em que o Conector do Intune apresenta problemas de conectividade se o Certificado Raiz do Baltimore CyberTrust não está instalado, expirou ou está corrompido no ponto de conexão de serviço. Para saber mais, confira [KB 3187516: O ponto de conexão de serviço não baixa atualizações](https://support.microsoft.com/help/3187516).  

### <a name="updates-and-servicing"></a>Atualizações e serviços

Para saber mais sobre essa função, confira [Atualizações e serviços para o Configuration Manager](/sccm/core/servers/manage/updates).

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `*.blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

### <a name="microsoft-intune"></a>Microsoft Intune

Para saber mais sobre essa função, confira [MDM híbrido com o Configuration Manager e o Microsoft Intune](/sccm/mdm/understand/hybrid-mobile-device-management).

- `*manage.microsoft.com`  

- `https://bspmts.mp.microsoft.com/V`  

- `https://login.microsoftonline.com/{TenantID}`  

### <a name="windows-10-servicing"></a>Serviço do Windows 10

Para saber mais sobre essa função, confira [Gerenciar o Windows como um serviço](/sccm/osd/deploy-use/manage-windows-as-a-service).

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

### <a name="azure-services"></a>Serviços do Azure

Para saber mais sobre essa função, confira [Configurar serviços do Azure para uso com o Configuration Manager](/sccm/core/servers/deploy/configure/azure-services-wizard).

- `management.azure.com`  


## <a name="co-management"></a>Cogerenciamento

Se você registrar os dispositivos com Windows 10 junto ao Microsoft Intune para realizar o cogerenciamento, verifique se esses dispositivos podem acessar os pontos de extremidade exigidos pelo Intune. Para saber mais, confira [Pontos de extremidade de rede para Microsoft Intune](https://docs.microsoft.com/intune/intune-endpoints).


## <a name="bkmk_cloud"></a> Serviços de nuvem

<!-- SCCMDocs-pr #3402 -->

Esta seção aborda os seguintes recursos:

- Gateway de gerenciamento de nuvem (CMG)
- Ponto de distribuição na nuvem (CDP)
- Integração do Azure Active Directory (Azure AD)
- Descoberta baseada no Azure AD

Para a implantação do serviço CMG/CPD, o **ponto de conexão de serviço** precisa de acesso a:

- Os pontos de extremidade específicos do Azure são diferentes conforme o ambiente, dependendo da configuração. O Configuration Manager armazena esses pontos de extremidade no banco de dados do site. Consulte a tabela **AzureEnvironments** no SQL Server para obter a lista de pontos de extremidade do Azure.  

O **ponto de conexão do CMG** precisa ter acesso aos seguintes pontos de extremidade de serviço:

- ServiceManagementEndpoint: `https://management.core.windows.net/`  

- StorageEndpoint: `blob.core.windows.net` e `table.core.windows.net`

Para a recuperação de token do Azure AD pelo **cliente** e **console do Configuration Manager**:

- ActiveDirectoryEndpoint `https://login.microsoftonline.com/`  

Para a descoberta de usuário do Azure AD, o **ponto de conexão de serviço** precisa de acesso a:

- Versão 1810 e anterior: Ponto de extremidade do Azure AD Graph `https://graph.windows.net/`  

- Versão 1902 e posterior: Ponto de extremidade do Microsoft Graph `https://graph.microsoft.com/`

O sistema de sites do ponto de conexão do ponto de gerenciamento de nuvem (CMG) é compatível com um proxy Web. Para obter mais informações sobre como configurar essa função para um proxy, consulte [Suporte do servidor proxy](/sccm/core/plan-design/network/proxy-server-support#to-set-up-the-proxy-server-for-a-site-system-server). O ponto de conexão do CMG só precisa se conectar aos pontos de extremidade de serviço do CMG. Ele não precisa de acesso a outros pontos de extremidade do Azure.

Para saber mais sobre o CMG, confira [Plano para CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="bkmk_sum"></a> Atualizações de software

Permitir que o ponto de atualização de software ativo acesse os seguintes pontos de extremidade para que o WSUS e as atualizações automáticas possam se comunicar com o serviço de nuvem do Microsoft Update:  

- `http://windowsupdate.microsoft.com`  

- `http://*.windowsupdate.microsoft.com`  

- `https://*.windowsupdate.microsoft.com`  

- `http://*.update.microsoft.com`  

- `https://*.update.microsoft.com`  

- `http://*.windowsupdate.com`  

- `http://download.windowsupdate.com`  

- `http://download.microsoft.com`  

- `http://*.download.windowsupdate.com`  

- `http://test.stats.update.microsoft.com`  

- `http://ntservicepack.microsoft.com`  

Para saber mais sobre atualizações de software, confira [Planejar atualizações de software](/sccm/sum/plan-design/plan-for-software-updates).

### <a name="intranet-firewall"></a>Firewall da intranet

Talvez seja necessário adicionar pontos de extremidade a um firewall entre os dois sistemas de site nos seguintes casos:

- Se os sites filho tiverem um ponto de atualização de software
- Se houver um ponto de atualização de software remoto, baseado na Internet, ativo em um site

#### <a name="software-update-point-on-the-child-site"></a>Ponto de atualização de software no site filho

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  


## <a name="manage-office-365"></a>Gerenciar o Office 365

Se você usar o Configuration Manager para implantar e atualizar o Office 365, permita que os pontos de extremidade:

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com` sincronize o ponto de atualização de software para atualizações de clientes do Office 365

- `config.office.com` crie configurações personalizadas para implantações do Office 365


## <a name="configuration-manager-console"></a>Console do Configuration Manager

Os computadores que tiverem o console do Configuration Manager exigem acesso aos seguintes pontos de extremidade da Internet para recursos específicos:

### <a name="in-console-feedback"></a>Comentários no console

- `http://petrol.office.microsoft.com`

Para saber mais sobre este recurso, confira [Feedback do produto](/sccm/core/understand/find-help#product-feedback).

### <a name="community-workspace-documentation-node"></a>Espaço de trabalho da comunidade, nó de documentação

- `https://aka.ms`

- `https://raw.githubusercontent.com`

Para saber mais neste nó de console, veja [Usando o console do Configuration Manager](/sccm/core/servers/manage/admin-console).

<!-- 
Community Hub
when in current branch, get details from SCCMDocs-pr #3403 
 -->

### <a name="monitoring-workspace-site-hierarchy-node"></a>Workspace de Monitoramento, nó Hierarquia do Site

Se você usar a **Exibição Geográfica**, permita o acesso ao ponto de extremidade a seguir:

- `http://maps.bing.com`


## <a name="desktop-analytics"></a>Análise de Área de Trabalho

Para saber mais sobre os pontos de extremidade necessários para o serviço de nuvem de Análise de Área de Trabalho, confira [Habilitar o compartilhamento de dados](/sccm/desktop-analytics/enable-data-sharing#endpoints).


## <a name="microsoft-public-ip-addresses"></a>Endereços IP públicos da Microsoft

Para saber mais sobre os intervalos de endereços IP da Microsoft, confira [Espaço de IP público da Microsoft](https://www.microsoft.com/download/details.aspx?id=53602). Esses endereços são atualizados regularmente. Não há nenhuma granularidade por serviço, qualquer endereço IP nesses intervalos pode ser usado.


## <a name="see-also"></a>Consulte também

- [Portas usadas no Configuration Manager](/sccm/core/plan-design/hierarchy/ports)

- [Suporte para servidor proxy no Configuration Manager](/sccm/core/plan-design/network/proxy-server-support)
