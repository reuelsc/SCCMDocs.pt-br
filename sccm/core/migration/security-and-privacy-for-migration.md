---
title: "Segurança e privacidade da migração | Microsoft Docs"
description: "Conheça as práticas recomendadas de segurança e informações de privacidade para a migração do seu ambiente do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6893fce1-7ad5-4151-9ba9-3096871e8e4a
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5e3d3f4194b06442e34c10988a20fe9ca40ac5d7
ms.openlocfilehash: 8aa6971d75924ab5bcacd70c330913097ecf8717


---
# <a name="security-and-privacy-for-migration-to-system-center-configuration-manager"></a>Segurança e privacidade da migração para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico contém as práticas recomendadas de segurança e informações de privacidade para a migração do seu ambiente do System Center Configuration Manager.  

## <a name="security-best-practices-for-migration"></a>Práticas recomendadas de segurança para a migração  
 Use a prática recomendada de segurança a seguir para a migração.  

|Prática recomendada de segurança|Mais informações|  
|----------------------------|----------------------|  
|Use a conta de computador para a Conta de Provedor de SMS do Site de Origem e para a Conta do SQL Server do Site de Origem em vez de uma conta de usuário.|Se você usar uma conta de usuário para a migração, remova os detalhes da conta quando a migração for concluída.|  
|Use IPsec ao migrar o conteúdo de um ponto de distribuição em um site de origem para um ponto de distribuição no site de destino.|Embora o conteúdo migrado esteja em hash para detectar violação, se os dados forem modificados durante a transferência, a migração falhará.|  
|Restrinja e monitore os usuários administrativos que podem criar trabalhos de migração.|A integridade do banco de dados da hierarquia de destino depende da integridade dos dados que o usuário administrativo escolhe para importar da hierarquia de origem. Além disso, esse usuário administrativo pode ler todos os dados da hierarquia de origem.|  

### <a name="security-issues-for-migration"></a>Problemas de segurança na migração  
A migração tem os seguintes problemas de segurança:  

-   Clientes bloqueados em um site de origem podem ser atribuídos com êxito à hierarquia de destino antes que seu registro de cliente seja migrado.  

     Embora o Configuration Manager mantenha o status bloqueado para os clientes que você migra, o cliente poderá ser atribuído com êxito à hierarquia de destino se a atribuição ocorrer antes que a migração do registro de cliente seja concluída.  

-   Mensagens de auditoria não são migradas.  

Ao migrar dados de um site de origem para um site de destino, você perde todas as informações de auditoria da hierarquia de origem.  

## <a name="privacy-information-for-migration"></a>Informações de privacidade para a migração  
 A migração descobre informações dos bancos de dados do site que você identifica em uma infraestrutura de origem e armazena esses dados no banco de dados na hierarquia de destino. A informação que o System Center Configuration Manager pode descobrir de um site ou hierarquia de origem depende dos recursos que foram habilitados no ambiente de origem, bem como das operações de gerenciamento realizadas nesse ambiente.  

 Para obter mais informações sobre segurança e informações de privacidade, consulte um dos seguintes tópicos:  

-   Para saber mais sobre as informações de privacidade do Configuration Manager 2007, consulte [Segurança e privacidade do Configuration Manager 2007](http://go.microsoft.com/fwlink/p/?LinkId=216450) na biblioteca de documentação do Configuration Manager 2007.  

-   Para saber mais sobre as informações de privacidade do System Center 2012 Configuration Manager, consulte [Segurança e privacidade do System Center 2012 Configuration Manager](https://technet.microsoft.com/library/gg682033.aspx) na biblioteca de documentação do System Center 2012 Configuration Manager.  

-   Para saber mais sobre as informações de privacidade do System Center Configuration Manager, consulte [Segurança e privacidade para o System Center Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

Você pode migrar alguns ou todos os dados com suporte de um site de origem para uma hierarquia de destino.  

A migração não é habilitada por padrão e requer várias etapas de configuração. As informações de migração não são enviadas à Microsoft.  

Antes de migrar dados de uma hierarquia de origem, considere seus requisitos de privacidade.  



<!--HONumber=Dec16_HO3-->


