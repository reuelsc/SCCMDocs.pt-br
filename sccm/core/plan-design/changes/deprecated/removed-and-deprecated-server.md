---
title: Preterido para servidores de site do Configuration Manager
titleSuffix: Configuration Manager
description: "Saiba mais sobre os produtos e sistemas operacionais que não são mais compatíveis com os servidores de site do System Center Configuration Manager."
ms.custom: na
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 0124939ae1ea5c1244c5776973297727b292e028
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2018
---
# <a name="removed-and-deprecated-for-system-center-configuration-manager-site-servers"></a>Removidos e preteridos para os servidores de site do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo descreve os produtos e os sistemas operacionais que foram removidos do suporte dos servidores de site do System Center Configuration Manager, ou que serão removidos em uma atualização futura (preteridos). O artigo oferece um aviso antecipado das futuras alterações que poderão afetar o uso do Configuration Manager.  

Essas informações estão sujeitas a alterações em versões futuras e podem não incluir todos os recursos, os produtos ou os sistemas operacionais preteridos.  


## <a name="deprecated-server-operating-systems"></a>Sistemas operacionais de servidor preteridos  

|**Sistemas operacionais**|**Substituição anunciada pela primeira vez**|**Suporte removido** |  
|-|-|-| 
|Windows Server 2008 R2|10 de julho de 2015| Versão 1702 (veja a observação 1)| 
|Windows Server 2008|10 de julho de 2015|Versão 1511 </br></br>O suporte como um sistema de sites foi removido. (veja a observação 2).|  

>[!NOTE]
>-   Começando com a versão 1702, o Windows Server 2008 R2 não é compatível com servidores do site ou com a maioria das funções do sistema de sites. Entretanto, as versões anteriores à 1702 continuam compatíveis com esse uso. Este sistema operacional permanece compatível com a função de ponto de distribuição do sistema de sites (incluindo pontos de distribuição por pull, bem como para PXE e multicast) até o anúncio de que essa compatibilidade será preterida ou a expiração do período de suporte estendido do sistema operacional. Começando pela versão 1602, você pode atualizar in-loco o sistema operacional de um servidor do site do Windows Server 2008 R2 para o Windows Server 2012 R2.  
>- Para obter mais informações sobre a atualização in-loco do sistema operacional de um servidor do site, consulte a seção [Atualização in-loco do sistema operacional dos servidores do site que executam o Windows Server 2008 R2](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#bkmk_from2008r2) em [Atualizar infraestrutura local que seja compatível com o System Center Configuration Manager](/sccm/core/servers/manage/upgrade-on-premises-infrastructure).

>[!NOTE]
>-   O Windows Server 2008 não é compatível com servidores do site ou funções do sistema de sites, exceto pelo ponto de distribuição e pelo ponto de distribuição por pull. Você pode continuar a usar esse sistema operacional como um ponto de distribuição até que a substituição do suporte seja anunciada ou o período de suporte estendido do sistema operacional expire. Para obter mais informações, consulte [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095) (A instalação do CB e do LTSB do System Center Configuration Manager falha no Windows Server 2008).

## <a name="deprecated-support-for-sql-server-versions-as-a-site-database"></a>Suporte preterido para versões do SQL Server como um banco de dados do site  

|**Versões do SQL Server**|**Substituição anunciada pela primeira vez**|**Suporte removido**|   
|-|-|-| 
|SQL Server 2008 R2|10 de julho de 2015|Versão 1702| 
|SQL Server 2008|10 de julho de 2015|Versão 1511|  


Se você precisa atualizar sua versão do SQL Server, recomendamos os seguintes métodos, do mais fácil para o mais complexo.
1. [Atualização do SQL Server no local](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recomendado).
2. Instalar uma nova versão do SQL Server em um novo computador. Em seguida, [use a opção de mover o banco de dados](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) da instalação do Configuration Manager para apontar o servidor do site para o novo SQL Server.
3. Use [backup e recuperação](/sccm/protect/understand/backup-and-recovery).


## <a name="more-information"></a>Mais informações
Para obter mais informações, consulte:
 - [Removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - O site do [Ciclo de Vida do Suporte da Microsoft](https://support.microsoft.com/lifecycle).
 - [Suporte para versões do branch atual do Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).