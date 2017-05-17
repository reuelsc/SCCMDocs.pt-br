---
title: "Pré-requisitos para relatórios | Microsoft Docs"
description: "Compreenda as várias dependências que afetam o uso de relatórios no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
caps.latest.revision: 5
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 70034213442f4c3d5a28ab65c2ceb51aa64320ad
ms.openlocfilehash: 2e624eb2ea061a4eb7d92365410fada335640224
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017


---
# <a name="prerequisites-for-reporting-in-system-center-configuration-manager"></a>Pré-requisitos para relatórios no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Relatórios no System Center Configuration Manager têm dependências externas e dependências dentro do produto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  
 A tabela a seguir lista as dependências externas para relatórios.  

|Pré-requisito|Mais informações|  
|------------------|----------------------|  
|SQL Server Reporting Services|Para poder usar relatórios no Configuration Manager, você deverá instalar e configurar o SQL Server Reporting Services.<br /><br /> Para obter informações sobre planejamento e implantação do Reporting Services em seu ambiente, consulte a seção [Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=212032) nos Manuais Online do SQL Server 2008.|  
|As dependências da função do sistema de site para computadores que executam o ponto do Reporting Services.|[Configurações com suporte para o System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md)|  

## <a name="dependencies-internal-to-configuration-manager"></a>Dependências internas do Configuration Manager  
 A tabela a seguir lista as dependências para relatórios no Configuration Manager.  

|Pré-requisito|Mais informações|  
|------------------|----------------------|  
|Ponto do Reporting Services|A função de sistema de sites do ponto do Reporting Services deve ser configurada para usar relatórios no Configuration Manager. Para obter mais informações sobre como instalar e configurar o ponto do Reporting Services, consulte [Configurando relatórios no System Center Configuration Manager](../../../core/servers/manage/configuring-reporting.md).|  

## <a name="supported-sql-server-versions-for-the-reporting-services-point"></a>Versões do SQL Server com suporte para o ponto do Reporting Services  
 O banco de dados do Reporting Services pode ser instalado na instância padrão ou em uma instância nomeada de uma instalação do SQL Server de 64 bits. A instância do SQL Server pode ser colocalizada com o servidor do sistema de site ou em um computador remoto.  

 A tabela a seguir lista as versões do SQL Server para as quais o ponto do Reporting Services dá suporte.  

|Versão do SQL Server|Ponto do Reporting Services|  
|------------------------|------------------------------|  
|SQL Server 2008 SP2 com um mínimo de Atualização Cumulativa 9<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|Sim|  
|SQL Server 2008 SP3 com um mínimo de Atualização Cumulativa 4<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|Sim|  
|SQL Server 2008 R2 com SP1 e com um mínimo de Atualização Cumulativa 6<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|Sim|  
|SQL Server 2008 R2 com SP2<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|Sim|  
|SQL Server Express 2008 R2 com SP1 e um mínimo de Atualização Cumulativa 4|Sem suporte|  
|SQL Server Express 2008 R2 com SP2|Sem suporte|  
|SQL Server 2012 e com um mínimo de Atualização Cumulativa 2<br /><br /> -   Standard<br />-   Enterprise|Sim|  
|SQL Server 2012 com SP1 e nenhuma atualização cumulativa mínima<br /><br /> -   Standard<br />-   Enterprise|Sim|  
|SQL Server 2014<br /><br /> -   Standard<br />-   Enterprise|Sim|
|SQL Server 2016<br /><br /> -   Standard<br />-   Enterprise|Sim|
|SQL Server 2016 com SP1<br /><br /> -   Standard<br />-   Enterprise|Sim|
## <a name="next-steps"></a>Próximas etapas
[Operações e manutenção de relatórios](operations-and-maintenance-for-reporting.md)

