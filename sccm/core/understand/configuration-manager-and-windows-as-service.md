---
title: Conceitos básicos do Windows como um serviço
titleSuffix: Configuration Manager
description: Obtenha informações básicas sobre adoção do branch atual do Configuration Manager para dar suporte ao Windows como um serviço.
ms.date: 04/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6ca2b72cb3533c3b857b3edbb4e37ca846d4cfa4
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="keep-windows-10-up-to-date-in-the-enterprise-using-configuration-manager"></a>Manter o Windows 10 atualizado na empresa usando o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager fornece amplo controle sobre atualizações de recurso para o Windows 10. Para adotar completamente o modelo de Windows como um serviço, você também deve adotar o modelo do branch atual do Configuration Manager. Para manter-se atualizado com o Windows 10 e obter a melhor experiência, é necessário manter-se atualizado com o Configuration Manager. Novas versões do Configuration Manager são necessárias para aproveitar ao máximo os novos e empolgantes recursos corporativos para Windows 10. Este conteúdo deve ser uma página de aterrissagem para os artigos importantes necessários para a adoção do branch atual do Configuration Manager. O branch atual do Configuration Manager é uma etapa para a obtenção do Windows como um serviço.

## <a name="key-topics-about-adopting-configuration-manager-current-branch"></a>Tópicos importantes sobre a adoção do branch atual do Configuration Manager

| Tópico        | Descrição          | 
| ------------- |-------------|
|[Visão geral do branch atual do Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)|Fornece um breve resumo dos principais pontos para o novo modelo de serviço do Configuration Manager (Branch Atual)|
|[Ciclo de vida de suporte](/sccm/core/servers/manage/current-branch-versions-supported)|Explica o novo modelo de suporte e de serviço.|
|[Itens removidos e preteridos](/sccm//core/plan-design/changes/deprecated/removed-and-deprecated)|Fornece aviso antecipado sobre as futuras alterações que poderão afetar o uso do Configuration Manager.|
|[Atualizações no branch atual do Configuration Manager](/sccm/core/servers/manage/updates)|Explica o método fácil no console para aplicação de atualizações de recurso para o Configuration Manager.|
|[Obter atualizações disponíveis](/sccm/core/servers/manage/install-in-console-updates#get-available-updates)|Explica os dois modos disponíveis para obter as novas atualizações de recurso do Configuration Manager.|
|[Lista de verificação da atualização](/sccm/core/servers/manage/install-in-console-updates#bkmk_beforeinstall)|Fornece listas de verificação específicas a uma versão de atualização, se aplicável.| 
|[Instalar novas atualizações de recurso do Configuration Manager](/sccm/core/servers/manage/install-in-console-updates#bkmk_install)|Explica as etapas de instalação simples para atualizações de recurso.|
|[Suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)|Fornece uma matriz de suporte para versões do Windows 10 (e ADK).|
|[Technical Previews do Configuration Manager](/sccm/core/get-started/technical-preview)|Fornece informações sobre o programa de Technical Preview do ConfigMgr.|


## <a name="key-topics-about-adopting-windows-as-a-service"></a>Tópicos importantes sobre a adoção do Windows como um serviço
| Tópico        | Descrição          | 
| ------------- |-------------|
|[Gerenciar o Windows como serviço](/sccm/osd/deploy-use/manage-windows-as-a-service)|Explica como usar planos de serviço para implantar atualizações de recurso do Windows 10.|
|[Atualizar o Windows 10 por meio da sequência de tarefas](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)|Os detalhes da criação de uma sequência de tarefas para atualizar o Windows 10 com recomendações adicionais.|
|[Implantações em fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|As implantações em fases automatizam uma distribuição coordenada e sequenciada de uma sequência de tarefas em várias coleções.|  
|[Integrar com o Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics)|O Upgrade Readiness permite avaliar e analisar a preparação dos dispositivos no ambiente para fazer a atualização para o Windows 10.| 
|[Integração do Windows Update para Empresas (opcional)](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)|Explica como definir e implantar políticas do WUfB (Windows Update para Empresas) usando o Configuration Manager.|
|[Usar o cogerenciamento com o Microsoft Intune e o Windows Update para Empresas (opcional)](/sccm/core/clients/manage/co-management-overview)|Fornece uma visão geral do cogerenciamento| 


## <a name="related-articles"></a>Artigos relacionados

- [Atualização in-loco do ConfigMgr 2012 para o System Center Configuration Manager (Branch Atual)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
- [Planejar para migração do ConfigMgr 2007 para o System Center Configuration Manager (Branch Atual)](/sccm/core/migration/planning-for-migration)