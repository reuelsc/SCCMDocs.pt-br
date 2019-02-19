---
title: Preparar-se para o gerenciamento de atualização de software
titleSuffix: Configuration Manager
description: Para preparar-se para gerenciar atualizações, conclua essas tarefas para exibir os dados de avaliação de conformidade no console do System Center Configuration Manager.
author: aczechowski
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 01907900-e28b-4cd7-9479-42906416707b
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 57d83601af5aa41a61b80d539bf87f4e9616792c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138017"
---
# <a name="prepare-for-software-updates-management"></a>Preparar-se para o gerenciamento de atualização de software

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para que os dados da avaliação de conformidade da atualização de software sejam exibidos no console do System Center Configuration Manager e para poder implantar as atualizações de software nos computadores cliente, é necessário concluir as etapas nas seções a seguir.

## <a name="step-1-install-a-software-update-point"></a>Etapa 1: Instalar um ponto de atualização de software  
O ponto de atualização de software é necessário no site de administração central, ou site primário autônomo, e nos sites primários para habilitar a avaliação de conformidade das atualizações de software e implantar atualizações de software em clientes. O ponto de atualização de software é opcional em sites secundários. Para ver os detalhes, consulte [Instalar um ponto de atualização de software](install-a-software-update-point.md)  

## <a name="step-2-synchronize-software-updates"></a>Etapa 2: Sincronizar atualizações de software
A sincronização de atualização de software é o processo de recuperar metadados de atualização de software que atendem aos critérios configurados. Atualizações de software não são exibidas no console do Configuration Manager até que você sincronize as atualizações de software. Para ver mais detalhes, consulte [Sincronizar atualizações de software](synchronize-software-updates.md).   

## <a name="step-3-configure-classifications-and-products-to-synchronize"></a>Etapa 3: configurar classificações e produtos para sincronizar
Execute essa configuração no site da administração central ou no site primário autônomo. Depois de sincronizar atualizações de software na primeira vez, o Configuration Manager recupera uma lista atualizada de produtos e classificações. Agora, você pode selecionar entre as novas opções nas propriedades do Componente de Ponto de Atualização de Software. Depois de configurar as novas classificações e produtos, repita a etapa 2 para iniciar a sincronização de atualizações de software para recuperar metadados de atualizações de software para os novos critérios. Para ver os detalhes, consulte [Configurar classificações e produtos para sincronizar](configure-classifications-and-products.md).

## <a name="step-4-manage-settings-for-software-updates"></a>Etapa 4: Gerenciar configurações de atualizações de software
Depois de sincronizar atualizações de software, verifique as configurações de cliente do Configuration Manager, as configurações de política de grupo e as configurações de atualizações de software antes de implantar as atualizações de software. Para ver os detalhes, consulte [Gerenciar configurações de atualizações de software](manage-settings-for-software-updates.md).
