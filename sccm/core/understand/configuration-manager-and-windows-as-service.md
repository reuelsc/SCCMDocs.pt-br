---
title: "Conceitos básicos do Configuration Manager como um serviço e do Windows como um serviço"
titleSuffix: Configuration Manager
description: "Obtenha informações básicas sobre adoção do Configuration Manager como um serviço para dar suporte ao Windows como um serviço."
ms.custom: na
ms.date: 01/04/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 6d93be3ec04396c9980b039617c673985090cdc6
ms.sourcegitcommit: fbd4a9d2fa8ed4ddd3a0fecc4a2ec4fc0ccc3d0c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/19/2018
---
# <a name="keep-windows-10-up-to-date-in-the-enterprise-using-configuration-manager"></a>Manter o Windows 10 atualizado na empresa usando o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual), Windows 10 (Canal Semestral)*

O System Center Configuration Manager fornece amplo controle sobre atualizações de recurso para o Windows 10. Para adotar completamente o modelo de Windows como um serviço, você também deve adotar o modelo de Configuration Manager como um serviço. Para manter-se atualizado com o Windows 10 e obter a melhor experiência, é necessário manter-se atualizado com o Configuration Manager. Novas versões do Configuration Manager são necessárias para aproveitar ao máximo os novos e empolgantes recursos corporativos para Windows 10. Este conteúdo deve ser uma página de aterrissagem para os artigos importantes necessários para a adoção do Configuration Manager como um serviço. O Configuration Manager como um serviço é uma etapa para a obtenção do Windows como um serviço.

## <a name="key-topics-about-adopting-configuration-manager-as-a-service"></a>Tópicos importantes sobre a adoção do Configuration Manager como um serviço

| Tópico        | Descrição          | 
| ------------- |-------------|
|[Visão geral do Configuration Manager como um serviço](/sccm/core/plan-design/changes/whats-new-incremental-versions)|Fornece um breve resumo dos principais pontos para o novo modelo de serviço do Configuration Manager (Branch Atual)|
|[Ciclo de vida de suporte](/sccm/core/servers/manage/current-branch-versions-supported)|Explica o novo modelo de suporte e de serviço.|
|[Itens removidos e preteridos](/sccm//core/plan-design/changes/deprecated/removed-and-deprecated)|Fornece aviso antecipado sobre as futuras alterações que poderão afetar o uso do Configuration Manager.|
|[Configuration Manager como um serviço](/sccm/core/servers/manage/updates)|Explica o método fácil no console para aplicação de atualizações de recurso para o Configuration Manager.|
|[Obter atualizações disponíveis](/sccm/core/servers/manage/install-in-console-updates.md#get-available-updates)|Explica os dois modos disponíveis para obter as novas atualizações de recurso do Configuration Manager.|
|[Lista de verificação da atualização](/sccm/core/servers/manage/install-in-console-updates#bkmk_beforeinstall)|Fornece listas de verificação específicas a uma versão de atualização, se aplicável.| 
|[Instalar novas atualizações de recurso do Configuration Manager](/sccm/core/servers/manage/install-in-console-updates#bkmk_install)|Explica as etapas de instalação simples para atualizações de recurso.|
|[Suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)|Fornece uma matriz de suporte para versões do Windows 10 (e ADK).|
|[Technical Previews do Configuration Manager](/sccm/core/get-started/technical-preview)|Fornece informações sobre o programa de Technical Preview do ConfigMgr.|


## <a name="key-topics-about-adopting-windows-as-a-service"></a>Tópicos importantes sobre a adoção do Windows como um serviço
| Tópico        | Descrição          | 
| ------------- |-------------|
|[Gerenciar o Windows como serviço](/sccm/osd/deploy-use/manage-windows-as-a-service)|Explica como usar planos de serviço para implantar atualizações de recurso do Windows 10.|
|[Integração do Windows Update para Empresas (opcional)](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)|Explica como definir e implantar políticas do WUfB (Windows Update para Empresas) usando o Configuration Manager.|
|[Usar o cogerenciamento com o Microsoft Intune e o Windows Update para Empresas (opcional)](/sccm/core/clients/manage/co-management-overview)|Fornece uma visão geral do cogerenciamento| 


## <a name="related-articles"></a>Artigos relacionados

- [Atualização in-loco do ConfigMgr 2012 para o System Center Configuration Manager (Branch Atual)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
- [Planejar para migração do ConfigMgr 2007 para o System Center Configuration Manager (Branch Atual)](/sccm/core/migration/planning-for-migration)