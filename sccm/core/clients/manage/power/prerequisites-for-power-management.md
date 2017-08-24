---
title: "Pré-requisitos para o gerenciamento de energia | Microsoft Docs"
description: "Conheça os pré-requisitos para o gerenciamento de energia no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
caps.latest.revision: "4"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 711ef491899846b86bfed0355ac7fd0f9d509c4f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-power-management-in-system-center-configuration-manager"></a>Pré-requisitos para o gerenciamento de energia no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O gerenciamento de energia no System Center Configuration Manager tem dependências externas e dependências dentro do produto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  
 A tabela a seguir lista as dependências externas ao Configuration Manager para uso do gerenciamento de energia.  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Os computadores cliente devem poder dar suporte aos estados de energia necessários|Para usar todos os recursos de gerenciamento de energia, os computadores cliente devem ter a capacidade de dar suporte às ações de entrar e sair do modo de suspensão e de hibernação. Você pode usar o relatório **Recursos de energia** para determinar se os computadores podem dar suporte a essas ações. Para mais informações, consulte [Relatório de Recursos de Energia](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) no tópico [Como monitorar e planejar gerenciamento de energia no System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).|  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  
 A tabela a seguir lista as dependências internas ao Configuration Manager para uso do gerenciamento de energia.  

|Dependência|Mais informações|  
|----------------|----------------------|  
|O gerenciamento de energia deve ser habilitado antes de criar e monitorar planos de energia.|Para obter informações sobre como habilitar e configurar o gerenciamento de energia, consulte [Configurando o gerenciamento de energia no System Center Configuration Manager](../../../../core/clients/manage/power/configuring-power-management.md).|  
|Ponto do Reporting Services|É necessário configurar um ponto do Reporting Services antes de exibir relatórios de gerenciamento de energia. Para obter mais informações, consulte [Relatórios no System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
