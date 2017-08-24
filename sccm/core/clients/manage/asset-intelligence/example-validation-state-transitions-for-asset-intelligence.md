---
title: "Exemplos de transições de estado de validação do Asset Intelligence | Microsoft Docs"
description: "Veja exemplos de transições de estado de validação do Asset Intelligence no System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6230a6e5-a1f6-459b-84f1-07fbde0e70f0
caps.latest.revision: "6"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: f280e06f34c0ed355b7c2652c571e36eb6684c59
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="example-validation-state-transitions-for-asset-intelligence-in-system-center-configuration-manager"></a>Exemplos de transições de estado de validação do Asset Intelligence no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os estados de validação do Asset Intelligence no System Center Configuration Manager não são estáticos e podem ser alterados por meio de ações administrativas executadas para afetar os dados armazenados no catálogo do Asset Intelligence. Este tópico fornece exemplos para possíveis transições de estado de validação.

##  <a name="BKMK_UncategorizedIsCategorized"></a> O item de catálogo não categorizado é categorizado pelo usuário administrativo  

|**Transição de estado**|**Descrição de transição de estado**|  
|--------------------------|--------------------------------------|  
|**Não categorizado**|Um título de software inventariado que não foi categorizado anteriormente pelo System Center Online ou que foi inserido no catálogo do Asset Intelligence pelo usuário administrativo.|  
|**Não categorizado** para **Definidopelo Usuário**|O item não categorizado é categorizado pelo usuário administrativo.|  

##  <a name="BKMK_CategorizedIsReCategorized"></a> O item de catálogo categorizado é categorizado novamente pelo usuário administrativo  

|**Transição de estado**|**Descrição de transição de estado**|  
|--------------------------|--------------------------------------|  
|**Validado**|O item de catálogo foi definido pelos pesquisadores do System Center Online e está presente no catálogo do Asset Intelligence.|  
|**Validado** para **Definido pelo Usuário**|O item de catálogo validado é categorizado novamente pelo usuário administrativo.|  

> [!NOTE]  
>  Já que as informações de categorização obtidas do System Center Online são armazenadas no banco de dados e não podem ser excluídas, o usuário administrativo pode reverter para a categorização do System Center Online posteriormente.  

##  <a name="BKMK_UserDefinedIsRecategorized"></a> O item de catálogo definido pelo usuário é categorizado novamente pelo System Center Online  

|**Transição de estado**|**Descrição de transição de estado**|  
|--------------------------|--------------------------------------|  
|**Não categorizado**|Um título de software inventariado que não foi categorizado anteriormente pelo System Center Online ou pelo usuário administrativo é inserido no catálogo do Asset Intelligence.|  
|**Definido pelo Usuário**|O item não categorizado é categorizado pelo usuário administrativo.|  
|**Definido pelo Usuário** para **Atualizável**|Um item de catálogo definido pelo usuário foi categorizado de modo diferente pelo System Center Online durante atualizações manuais posteriores em massa do catálogo do Asset Intelligence.<br /><br /> O usuário administrativo pode usar a caixa de diálogo **Resolução de Conflitos de Detalhes do Software** para decidir se é necessário usar as novas informações de categorização ou o valor anterior definido pelo usuário.|  
|**Atualizável** para **Validado**|O usuário administrativo usa a caixa de diálogo **Resolução de Conflitos de Detalhes do Software** para usar as novas informações de categorização recebidas do System Center Online durante a atualização anterior do catálogo.|  
|ou||  
|**Atualizável** para **Definido pelo Usuário**|O usuário administrativo usa a caixa de diálogo **Resolução de Conflitos de Detalhes do Software** para usar o valor anterior definido pelo usuário.|  

> [!NOTE]  
>  Já que as informações de categorização obtidas do System Center Online são armazenadas no banco de dados e não podem ser excluídas, o usuário administrativo pode reverter para a categorização do System Center Online posteriormente.  

##  <a name="BKMK_UncategorizedIsSubmitted"></a> O item de catálogo não categorizado é enviado para o System Center Online para categorização  

|**Transição de estado**|**Descrição de transição de estado**|  
|--------------------------|--------------------------------------|  
|**Não categorizado**|Um título de software inventariado que não foi categorizado anteriormente pelo System Center Online ou pelo usuário administrativo é inserido no banco de dados do Asset Intelligence.|  
|**Não categorizado** para **Pendente**|O item não categorizado é enviado ao System Center Online para categorização pelo usuário administrativo.|  
|**Pendente** para **Validado**|O item é categorizado pelo System Center Online. O usuário administrativo importa o item no catálogo do Asset Intelligence por meio de uma atualização em massa do catálogo ou da sincronização do catálogo do Asset Intelligence. Ambas estão disponíveis por meio da função do sistema de sites do ponto de sincronização do Asset Intelligence.|  

##  <a name="BKMK_UserDefinedIsSubmitted"></a> O item de catálogo definido pelo usuário é enviado para o System Center Online para categorização  

|**Transição de estado**|**Descrição de transição de estado**|  
|--------------------------|--------------------------------------|  
|**Não categorizado**|Um título de software inventariado que não foi categorizado anteriormente por um usuário administrativo ou pelo System Center Online é inserido no banco de dados do Asset Intelligence.|  
|**Definido pelo Usuário**|O item não categorizado foi categorizado.|  
|**Definido pelo Usuário** para **Pendente**|Você envia o item definido pelo usuário ao System Center Online para categorização.|  
|**Pendente** para **Atualizável**|Um item de catálogo definido pelo usuário foi categorizado de modo diferente pelo System Center Online durante uma sincronização de catálogo posterior. Você pode usar a ação **Resolver Conflito** para decidir se deve usar as novas informações de categorização ou o valor definido pelo usuário anterior. Para obter mais informações sobre como resolver conflitos, consulte [Resolver conflitos de detalhes de software](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  
|**Atualizável** para **Validado**|Você usa a ação **Resolver Conflito** e seleciona as novas informações de categorização recebidas do System Center Online durante a atualização do catálogo anterior. Para obter mais informações sobre como resolver conflitos, consulte [Resolver conflitos de detalhes de software](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  
|ou||  
|**Atualizável** para **Definido pelo Usuário**|Você usa a ação **Resolver Conflito** e seleciona para usar o valor anterior definido pelo usuário. Para obter mais informações sobre como resolver conflitos, consulte [Resolver conflitos de detalhes de software](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  

> [!NOTE]  
>  Já que as informações de categorização obtidas do System Center Online são armazenadas no banco de dados e não podem ser excluídas, é possível reverter para a categorização do System Center Online posteriormente.  
