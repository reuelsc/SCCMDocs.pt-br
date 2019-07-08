---
title: Introdução a consultas
titleSuffix: Configuration Manager
description: Criar e executar consultas para localizar objetos em uma hierarquia do System Center Configuration Manager que correspondem aos critérios de consulta.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28fe8d38b03efaa101cfe01d8a8a054f0b26f2ed
ms.sourcegitcommit: 3a3f40f3d39cbecfb9219a64c0185ea4b2ef9671
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2019
ms.locfileid: "67561949"
---
# <a name="introduction-to-queries-in-system-center-configuration-manager"></a>Introdução a consultas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode criar e executar consultas para localizar objetos em uma hierarquia do System Center Configuration Manager que correspondem aos critérios de consulta. Esses objetos incluem itens como tipos específicos de computadores ou grupos de usuários. As consultas podem retornar a maioria dos tipos de objetos do Configuration Manager, que incluem sites, coleções, aplicativos e dados de inventário.  

## <a name="query-creation-overview"></a>Visão geral de criação de consulta

 Ao criar uma consulta, é necessário especificar, no mínimo, dois parâmetros: o local em que deseja pesquisar e o que deseja pesquisar. Por exemplo, para encontrar a quantidade de espaço disponível em disco rígido em todos os computadores em um site do Configuration Manager, você pode criar uma consulta para pesquisar a classe de atributo **Disco Lógico** e o atributo **Espaço Livre (MB)** do espaço disponível em disco rígido.  

 Depois de criar uma consulta inicial, você pode especificar critérios de consulta adicionais. Por exemplo, você pode especificar uma opção para que os resultados da consulta incluam somente os computadores que são atribuídos a um site especificado. Você também pode alterar como os resultados são exibidos poder exibir os resultados em uma ordem que faça sentido para você. Por exemplo, você pode especificar uma opção para que os resultados sejam classificados pela quantidade de espaço livre em disco rígido em ordem crescente ou decrescente.  

 Ao criar uma consulta, ela é armazenada pelo Configuration Manager e exibida no nó **Consultas** no workspace **Monitoramento**. Nesse local, você pode criar novas consultas e executar, atualizar e gerenciar consultas existentes.  

 Você também pode importar uma consulta para uma regra de consulta em uma coleção do Configuration Manager. Para mais informações, consulte [Como criar coleções no System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

## <a name="next-steps"></a>Próximas etapas

 [Como criar consultas no System Center Configuration Manager](../../../core/servers/manage/create-queries.md)
