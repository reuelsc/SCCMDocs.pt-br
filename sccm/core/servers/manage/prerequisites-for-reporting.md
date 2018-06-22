---
title: Pré-requisitos para relatórios
titleSuffix: Configuration Manager
description: Compreenda as várias dependências que afetam o uso de relatórios no System Center Configuration Manager.
ms.date: 01/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9e20321a794f093dbb494034fe256c26be31480
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336741"
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
|SQL Server 2017 com um mínimo de Atualização Cumulativa 2<br /><br /> -   Standard<br />-   Enterprise|Sim, a partir da versão 1710 do Configuration Manager|  
|SQL Server 2016 com SP1<br /><br /> -   Standard<br />-   Enterprise|Sim| 
|SQL Server 2016<br /><br /> -   Standard<br />-   Enterprise|Sim|
|SQL Server 2014 com SP2<br /><br /> -   Standard<br />-   Enterprise|Sim|
|SQL Server 2014 com SP1<br /><br /> -   Standard<br />-   Enterprise|Sim|
|SQL Server 2012 com SP4 <br /><br /> -   Standard<br />-   Enterprise|Sim|  
|SQL Server 2012 com SP3 <br /><br /> -   Standard<br />-   Enterprise|Sim|  
|SQL Server 2008 R2 com SP3<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|Sim, para as versões compatíveis do Configuration Manager anteriores à 1702.|  
|SQL Server Express 2008 R2 com SP3|Sem suporte| 




## <a name="next-steps"></a>Próximas etapas
[Operações e manutenção de relatórios](operations-and-maintenance-for-reporting.md)
