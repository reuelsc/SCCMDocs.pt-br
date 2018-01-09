---
title: Suporte internacional
titleSuffix: Configuration Manager
description: "Configure o System Center Configuration Manager para atender a requisitos internacionais específicos."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
caps.latest.revision: "6"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 2b54bc3977d1c5b2aa67fb51ed582b8a220a56a6
ms.sourcegitcommit: ca9d15dfb1c9eb47ee27ea9b5b39c9f8cdcc0748
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2018
---
# <a name="international-support-in-system-center-configuration-manager"></a>Suporte internacional no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As seções a seguir fornecem detalhes técnicos para ajudá-lo a tornar o System Center Configuration Manager em conformidade com requisitos internacionais específicos.  

## <a name="gb18030-requirements"></a>Requisitos GB18030  
 O Configuration Manager atende aos padrões que estão definidos no GB18030, portanto é possível usar o Configuration Manager na China. Uma implantação do Configuration Manager deve ter as seguintes configurações para atender aos requisitos GB18030:  

-   Cada computador do servidor de site e computador do SQL Server utilizado com o Configuration Manager deve usar um sistema operacional chinês.  

-   Cada banco de dados do site e cada instância do SQL Server na hierarquia deve usar o mesmo agrupamento, e deve ser um dos seguintes:  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  Estes agrupamentos de banco de dados são uma exceção aos requisitos observados na seção [Suporte para versões do SQL Server para o System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   Você deve colocar um arquivo com o nome **GB18030.SMS** na pasta raiz do volume do sistema de cada computador do servidor do site na hierarquia. Esse arquivo não contém dados e pode ser um arquivo de texto vazio que está nomeado para atender a esse requisito.  
