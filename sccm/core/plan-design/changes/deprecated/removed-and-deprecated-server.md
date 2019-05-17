---
title: Itens preteridos para os servidores do site
titleSuffix: Configuration Manager
description: Saiba mais sobre os produtos e sistemas operacionais que não são mais compatíveis com os servidores de site do Configuration Manager.
ms.date: 01/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 52e3384f1922e1a8322f316fd99bdd967e34b131
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65496220"
---
# <a name="removed-and-deprecated-for-configuration-manager-site-servers"></a>Itens removidos e preteridos dos servidores do site do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo descreve os produtos e os sistemas operacionais que foram removidos do suporte dos servidores de site do Configuration Manager, ou que serão removidos em uma atualização futura (preteridos). Fornece aviso antecipado sobre as futuras alterações que poderão afetar o uso do Configuration Manager.  

Essas informações podem ser alteradas no futuro. Elas poderão não incluir cada sistema operacional, produto ou recurso preterido.  



## <a name="server-os"></a>Sistema operacional do Servidor  

|**Sistemas operacionais**|**Substituição anunciada pela primeira vez**|**Suporte removido** |  
|-|-|-| 
|Windows Server 2008 R2 com SP1|10 de julho de 2015| Versão 1702 <sup>[Observação 1](#bkmk_note1)</sup>| 
|Windows Server 2008 com SP2|10 de julho de 2015|Versão 1511 <sup>[Observação 2](#bkmk_note2)</sup>|  

#### <a name="bkmk_note1"></a> Observação 1: Windows Server 2008 R2 com SP1
O Windows Server 2008 R2 com Service Pack 1 não é compatível com servidores do site ou com a maioria das funções do sistema de sites. Esse sistema operacional ainda é compatível com a função de ponto de distribuição. Esse suporte inclui pontos de distribuição de pull, PXE e multicast. 

> [!Important]  
> A data de término do suporte estendido para o Windows Server 2008 R2 com SP1 é 14 de janeiro de 2020. Após essa data, o Configuration Manager não dará mais suporte a esse sistema operacional como uma função do sistema de sites. 

Você pode atualizar o sistema operacional do servidor do site do Windows Server 2008 R2 para Windows Server 2012 R2. Para obter mais informações, confira [Atualização in-loco do sistema operacional dos servidores do site que executam o Windows Server 2008 R2](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#bkmk_from2008r2).  


#### <a name="bkmk_note2"></a> Observação 2: Windows Server 2008 com SP2
O Windows Server 2008 com Service Pack 2 não é compatível com servidores do site ou com a maioria das funções do sistema de sites. Esse sistema operacional ainda é compatível com a função de ponto de distribuição. Esse suporte inclui pontos de distribuição de pull, PXE e multicast. 

> [!Important]  
> A data de término do suporte estendido para o Windows Server 2008 com SP2 é 14 de janeiro de 2020. Após essa data, o Configuration Manager não dará mais suporte a esse sistema operacional como uma função do sistema de sites.  



## <a name="sql-server"></a>SQL Server   

|**Versões do SQL Server**|**Substituição anunciada pela primeira vez**|**Suporte removido**|   
|-|-|-| 
|SQL Server 2008 R2|10 de julho de 2015|Versão 1702| 
|SQL Server 2008|10 de julho de 2015|Versão 1511|  


Se você precisa atualizar sua versão do SQL Server, recomendamos os seguintes métodos, do mais fácil para o mais complexo:

1. [Atualização do SQL Server no local](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recomendado).  

2. Instalar uma nova versão do SQL Server em um novo computador. Em seguida, [use a opção de mover o banco de dados](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) da instalação do Configuration Manager para apontar o servidor do site para o novo SQL Server.  

3. Use [backup e recuperação](/sccm/protect/understand/backup-and-recovery).  



## <a name="more-information"></a>Mais informações

Para obter mais informações, consulte os seguintes artigos: 

- [Removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)  

- [Ciclo de vida do Suporte da Microsoft](https://support.microsoft.com/lifecycle)  

- [Suporte para versões atuais de branch do Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported)  

