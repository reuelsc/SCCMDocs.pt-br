---
title: "Práticas recomendadas de coleções | Microsoft Docs"
description: "Veja as práticas recomendadas para coletas no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 8f3086adac2c6886316a2fd65b3d471acac9077c


---
# <a name="best-practices-for-collections-in-system-center-configuration-manager"></a>Práticas recomendadas para coletas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as práticas recomendadas a seguir para coletas no System Center Configuration Manager.  

## <a name="do-not-use-incremental-updates-for-a-large-number-of-collections"></a>Não use atualizações incrementais para um grande número de coleções  
 Quando você habilita a opção **Usar atualizações incrementais para esta coleção** , essa configuração poderá causar atrasos de avaliação ao habilitá-la para várias coleções. O limite é de cerca de 200 coleções em sua hierarquia. O número exato depende dos seguintes fatores:  

-   O número total de coleções  

-   A frequência de novos recursos adicionados e alterados na hierarquia  

-   O número de clientes na hierarquia  

-   A complexidade das regras de associação da coleção na hierarquia  

## <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Verifique se as janelas de manutenção são grandes o suficiente para implantar atualizações de software críticas  
 Você pode configurar janelas de manutenção para coleções de dispositivos, para restringir os momentos em que o Configuration Manager pode instalar software nesses dispositivos. Se você configurar a janela de manutenção como muito pequena, o cliente não poderá instalar atualizações críticas de software, o que o deixa vulnerável ao ataque mitigado pela atualização de software.  



<!--HONumber=Dec16_HO3-->


