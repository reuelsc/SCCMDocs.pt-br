---
title: Segurança e privacidade de consultas
titleSuffix: Configuration Manager
description: Entenda as práticas recomendadas de segurança e privacidade quando você consulta informações do banco de dados do site.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0315124b44af4359528b590bf0a6b325bfd14eb1
ms.sourcegitcommit: 3a3f40f3d39cbecfb9219a64c0185ea4b2ef9671
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2019
ms.locfileid: "67561979"
---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>Segurança e privacidade de consultas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As consultas no System Center Configuration Manager permitem recuperar informações do banco de dados do site conforme os critérios que você especificar. O Configuration Manager coleta informações de banco de dados do site durante a operação padrão. Por exemplo, usando as informações coletadas durante a descoberta ou o inventário, você pode configurar uma consulta para identificar os dispositivos que cumprem os critérios especificados.  

 Para obter mais informações sobre consultas, consulte [Introdução a consultas no System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). Para obter as melhores práticas de segurança e as informações de privacidade para as operações do Configuration Manager que coletam os dados que você pode recuperar usando consultas, confira [Segurança e privacidade para o System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Práticas recomendadas de segurança para consultas

 Use essa prática recomendada de segurança para consultas.  

|Prática recomendada de segurança|Mais informações|  
|----------------------------|----------------------|  
|Ao exportar ou importar uma consulta salva em um local da rede, proteja o local e o canal da rede.|Restrinja quem pode acessar a pasta de rede.<br /><br /> Use a assinatura de protocolo SMB ou protocolo IPsec entre o local de rede e o servidor do site para impedir que um invasor adultere os dados da consulta antes de eles serem importados.|  

## <a name="next-steps"></a>Próximas etapas
  
[Security and privacy for System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md)
