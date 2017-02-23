---
title: "Segurança e privacidade de coleções | Microsoft Docs"
description: "Veja as práticas recomendadas de segurança e privacidade em coleções no System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30bf2451-5415-4be2-ba8d-21759370cd83
caps.latest.revision: 5
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 3379494824804c6be5c051c67a79d25e7eed88f0


---
# <a name="security-and-privacy-for-collections-in-system-center-configuration-manager"></a>Segurança e privacidade de coleções no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico contém as práticas recomendadas de segurança e informações de privacidade para coleções no System Center Configuration Manager.  

 Não há informações de privacidade especificamente para coleções no Configuration Manager. Coleções são contêineres de recursos, como usuários e dispositivos. Em geral, a associação da coleção depende das informações coletadas pelo Configuration Manager durante a operação padrão. Por exemplo, usando as informações de recursos que foram coletadas da descoberta ou do inventário, uma coleção pode ser configurada para conter os dispositivos que atendem aos critérios especificados. As coleções também podem se basear nas informações atuais de status para as operações de gerenciamento de cliente, como a implantação de software e a verificação de conformidade. Além dessas coleções baseadas em consulta, os usuários administrativos também podem adicionar recursos a coleções.  

 Para obter mais informações sobre coleções, consulte [Introdução a coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md). Para obter mais informações sobre as práticas recomendadas de segurança e informações de privacidade para as operações do Configuration Manager que podem ser usadas para configurar a associação da coleção, consulte [Práticas recomendadas de segurança e informações de privacidade do System Center Configuration Manager](../../../../core/plan-design/security/security-best-practices-and-privacy-information.md).  

## <a name="security-best-practices-for-collections"></a>Práticas recomendadas de segurança para coleções  
 Use a prática recomendada de segurança a seguir para coleções.  

|Prática recomendada de segurança|Mais informações|  
|----------------------------|----------------------|  
|Ao exportar ou importar uma coleção usando um arquivo MOF (Managed Object Format) que é salvo em um local da rede, proteja o local e o canal da rede.|Restrinja quem pode acessar a pasta de rede.<br /><br /> Use a assinatura do protocolo SMB ou IPsec entre o local de rede e o servidor do site para impedir que um invasor viole os dados exportados da coleção. Use IPsec para criptografar os dados na rede e para evitar a divulgação de informações.|  

### <a name="security-issues-for-collections"></a>Problemas de segurança para coleções  
 As coleções apresentam os seguintes problemas de segurança:  

-   Se você usar variáveis de coleção, os administradores locais poderão ler informações potencialmente confidenciais.  

     Variáveis de coleção podem ser usadas quando você implanta um sistema operacional.  



<!--HONumber=Dec16_HO3-->


