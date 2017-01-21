---
title: "Segurança e privacidade para consultas | Microsoft Docs"
description: "Entenda as práticas recomendadas de segurança e privacidade quando você consulta informações do banco de dados do site."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 09f7bdaa29a01fb2a38aa223db56b5bce3bc5205


---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>Segurança e privacidade de consultas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As consultas no System Center Configuration Manager permitem recuperar informações do banco de dados do site com base nos critérios que você especificar. O Configuration Manager coleta informações de banco de dados do site durante a operação padrão. Por exemplo, usando as informações coletadas da descoberta ou do inventário, você pode configurar uma consulta para identificar os dispositivos que atendem aos critérios especificados.  

 Para obter mais informações sobre consultas, consulte [Introdução a consultas no System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). Para obter mais informações sobre as práticas recomendadas de segurança e informações de privacidade para as operações do Configuration Manager que coletam as informações que podem ser recuperadas por meio de consultas, consulte [Segurança e privacidade no System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Práticas recomendadas de segurança para consultas  
 Use a prática recomendada de segurança a seguir para consultas.  

|Prática recomendada de segurança|Mais informações|  
|----------------------------|----------------------|  
|Ao exportar ou importar uma consulta que é salva em um local da rede, proteja o local e o canal da rede.|Restrinja quem pode acessar a pasta de rede.<br /><br /> Use a assinatura do protocolo SMB ou IPsec entre o local de rede e o servidor do site para impedir que um invasor viole os dados da consulta antes que sejam importados.|  

## <a name="see-also"></a>Consulte também  
 [Referência técnica de consultas no System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)



<!--HONumber=Dec16_HO3-->


