---
title: Pré-requisitos de coleções
titleSuffix: Configuration Manager
description: Obter pré-requisitos para usar coleções no System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c05bbd53880e61687c76c1b8caee9f7c541092c3
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130200"
---
# <a name="prerequisites-for-collections-in-system-center-configuration-manager"></a>Pré-requisitos para coleções no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Coleções no System Center Configuration Manager têm dependências somente dentro do produto.  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Ponto do Reporting Services|A função do sistema de sites do ponto do Reporting Services deve estar instalada antes que seja possível executar relatórios para coleções. Para obter mais informações, consulte [Relatórios no System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Permissões específicas de segurança devem ter sido concedidas para gerenciar coleções|É necessário ter as seguintes permissões de segurança para gerenciar configurações de conformidade:<br /><br /> ‑ Para criar e gerenciar coleções: **Criar**, **Excluir**, **Modificar**, **Modificar Pasta**, **Mover Objeto**, **Ler** e **Ler Recurso** para o objeto **Coleção**.<br /><br /> ‑ Para gerenciar configurações de coleção: **Modificar Configuração da Coleção** para o objeto **Coleção**.<br /><br /> A permissão **Modificar Pasta** é necessária para todas as pastas da coleção, incluindo a pasta raiz.|  
