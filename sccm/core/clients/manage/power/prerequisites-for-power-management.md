---
title: Pré-requisitos para o gerenciamento de energia
titleSuffix: Configuration Manager
description: Conheça os pré-requisitos para o gerenciamento de energia no System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c6630ef07c0b7947875ea2adac4e6612143aaee8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32344425"
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
