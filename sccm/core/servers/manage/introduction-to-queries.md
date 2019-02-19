---
title: Introdução a consultas
titleSuffix: Configuration Manager
description: Criar e executar consultas para localizar objetos em uma hierarquia do System Center Configuration Manager que correspondem aos critérios de consulta.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3812953df11daff9d768aa808edd0bcb08ab66f5
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124806"
---
# <a name="introduction-to-queries-in-system-center-configuration-manager"></a>Introdução a consultas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode criar e executar consultas para localizar objetos em uma hierarquia do System Center Configuration Manager que correspondem aos critérios de consulta. Esses objetos incluem itens como tipos específicos de computadores ou grupos de usuários. As consultas podem retornar a maioria dos tipos de objetos do Configuration Manager, que incluem sites, coleções, aplicativos e dados de inventário.  

 Ao criar uma consulta, é necessário especificar, no mínimo, dois parâmetros: o local em que deseja pesquisar e o que deseja pesquisar. Por exemplo, para encontrar a quantidade de espaço em disco que está disponível em todos os computadores em um site do Configuration Manager, você pode criar uma consulta para pesquisar a classe de atributo **Disco Lógico** e o atributo **Espaço Livre (MB)** do espaço em disco disponível.  

 Depois de criar uma consulta inicial, você pode especificar critérios de consulta adicionais. Por exemplo, você pode especificar uma opção para que os resultados da consulta incluam somente os computadores que são atribuídos a um site especificado. Você também pode modificar o modo como os resultados são exibidos para que seja possível exibir os resultados em uma ordem que seja significativa para você. Por exemplo, você pode especificar uma opção para que os resultados sejam classificados pela quantidade de espaço livre em disco em ordem crescente ou decrescente.  

 Ao criar uma consulta, ela é armazenada pelo Configuration Manager e exibida no nó **Consultas** do workspace **Monitoramento**. Nesse local, você pode criar uma nova consulta e executar, atualizar ou gerenciar uma consulta existente.  

 Você também pode importar uma consulta para uma regra de consulta em uma coleção do Configuration Manager. Para mais informações, consulte [Como criar coleções no System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

## <a name="see-also"></a>Consulte também  
 [Referência técnica de consultas no System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)
