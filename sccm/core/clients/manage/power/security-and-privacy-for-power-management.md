---
title: Segurança e privacidade do gerenciamento de energia
titleSuffix: Configuration Manager
description: Obtenha as informações de segurança e privacidade do gerenciamento de energia no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: a7bba23bf35d60d83fcff01acb20c8f404b6445d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123394"
---
# <a name="security-and-privacy-for-power-management-in-system-center-configuration-manager"></a>Segurança e privacidade do gerenciamento de energia no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Esta seção contém as informações de segurança e privacidade do gerenciamento de energia no System Center Configuration Manager.  

## <a name="security-best-practices-for-power-management"></a>Práticas recomendadas de segurança para o gerenciamento de conteúdo  
 Não há práticas recomendadas relacionadas à segurança para o gerenciamento de energia.  

## <a name="privacy-information-for-power-management"></a>Informações sobre privacidade para o gerenciamento de conteúdo  
 Gerenciamento de energia usa recursos que são integrados do Windows para monitorar o uso de energia e aplicar as configurações de energia em computadores durante o horário comercial e horários. O Configuration Manager coleta informações de consumo de energia de computadores, o que inclui dados sobre o período em que um usuário está usando um computador. Embora o Configuration Manager monitore o consumo de energia para uma coleção em vez de para cada computador, uma coleção pode conter apenas um computador. Por padrão, o gerenciamento de energia não está habilitado e deve ser configurado por um administrador.  

 As informações de consumo de energia são armazenadas no banco de dados do Configuration Manager e não são enviadas à Microsoft. As informações detalhadas são mantidas no banco de dados durante 31 dias e as informações resumidas são mantidas por 13 meses. Não é possível configurar o intervalo de exclusão.  

 Antes de configurar o gerenciamento de energia, considere seus requisitos de privacidade.  
