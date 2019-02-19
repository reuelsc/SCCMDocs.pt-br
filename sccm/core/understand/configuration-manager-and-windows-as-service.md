---
title: Configuration Manager e Windows como um serviço
titleSuffix: Configuration Manager
description: Obtenha informações básicas sobre adoção do branch atual do Configuration Manager para dar suporte ao Windows como um serviço.
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1ea9e2ef8da09d0ab344d56fe0ad4f1b3fb9d94b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130496"
---
# <a name="configuration-manager-and-windows-as-a-service"></a>Configuration Manager e Windows como um serviço

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager fornece amplo controle sobre atualizações de recurso para o Windows 10. Para adotar completamente o modelo de Windows como um serviço, você também deve adotar o modelo do branch atual do Configuration Manager. Para manter-se atualizado com o Windows 10 e obter a melhor experiência, é necessário manter-se atualizado com o Configuration Manager. Novas versões do Configuration Manager são necessárias para aproveitar ao máximo os novos e empolgantes recursos corporativos para Windows 10. Este artigo deve ser uma página de aterrissagem para os artigos importantes necessários para a adoção do branch atual do Configuration Manager. O branch atual do Configuration Manager é uma etapa para a obtenção do Windows como um serviço.

## <a name="key-articles-about-adopting-configuration-manager-current-branch"></a>Artigos importantes sobre a adoção do branch atual do Configuration Manager

| Artigo        | Descrição          | 
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


## <a name="key-articles-about-adopting-windows-as-a-service"></a>Artigos importantes sobre a adoção do Windows como um serviço

| Artigo        | Descrição          | 
| ------------- |-------------|
|[Gerenciar o Windows como serviço](/sccm/osd/deploy-use/manage-windows-as-a-service)|Explica como usar planos de serviço para implantar atualizações de recurso do Windows 10.|
|[Atualizar o Windows 10 por meio da sequência de tarefas](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)|Os detalhes da criação de uma sequência de tarefas para atualizar o Windows 10 com recomendações adicionais.|
|[Implantações em fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|As implantações em fases automatizam uma distribuição coordenada e sequenciada de uma sequência de tarefas em várias coleções.|  
|[Otimizar a entrega de atualização do Windows 10](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)|Use o Configuration Manager para gerenciar o conteúdo da atualização para ficar atualizado com o Windows 10.|
|[Integrar com o Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics)|O Upgrade Readiness permite avaliar e analisar a preparação dos dispositivos no ambiente para fazer a atualização para o Windows 10.| 
|[Integração do Windows Update para Empresas (opcional)](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)|Explica como definir e implantar políticas do WUfB (Windows Update para Empresas) usando o Configuration Manager.|
|[Usar o cogerenciamento com o Microsoft Intune e o Windows Update para Empresas (opcional)](/sccm/comanage/overview)|Fornece uma visão geral do cogerenciamento| 


## <a name="related-articles"></a>Artigos relacionados

- [Atualização in-loco do ConfigMgr 2012 para o System Center Configuration Manager (Branch Atual)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
- [Planejar para migração do ConfigMgr 2007 para o System Center Configuration Manager (Branch Atual)](/sccm/core/migration/planning-for-migration)
