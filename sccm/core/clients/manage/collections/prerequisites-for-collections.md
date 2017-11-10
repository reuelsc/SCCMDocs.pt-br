---
title: "Pré-requisitos de coleções"
titleSuffix: Configuration Manager
description: "Obter pré-requisitos para usar coleções no System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
caps.latest.revision: "7"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 5696a4cc81d8be889f6040a2f9610e1aec17d271
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="prerequisites-for-collections-in-system-center-configuration-manager"></a>Pré-requisitos para coleções no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Coleções no System Center Configuration Manager têm dependências somente dentro do produto.  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Ponto do Reporting Services|A função do sistema de sites do ponto do Reporting Services deve estar instalada antes que seja possível executar relatórios para coleções. Para obter mais informações, consulte [Relatórios no System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Permissões específicas de segurança devem ter sido concedidas para gerenciar coleções|É necessário ter as seguintes permissões de segurança para gerenciar configurações de conformidade:<br /><br /> ‑ Para criar e gerenciar coleções: **Criar**, **Excluir**, **Modificar**, **Modificar Pasta**, **Mover Objeto**, **Ler** e **Ler Recurso** para o objeto **Coleção**.<br /><br /> ‑ Para gerenciar a configurações de coleção: **Modificar Configuração da Coleção** para o objeto **Coleção**.<br /><br /> A permissão **Modificar Pasta** é necessária para todas as pastas da coleção, incluindo a pasta raiz.|  
