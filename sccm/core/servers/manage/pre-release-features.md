---
title: "Recursos de pré-lançamento"
titleSuffix: Configuration Manager
description: "Recursos de pré-lançamento no System Center Configuration Manager"
ms.custom: na
ms.date: 12/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
caps.latest.revision: "36"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: c132f1512d8a1d6a4657079c8ecd2d7a050797b9
ms.sourcegitcommit: 52b956cfe32c3f06ae68d6ba6fc3244ce5a66325
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/06/2017
---
# <a name="pre-release-features-in-system-center-configuration-manager"></a>Recursos de pré-lançamento no System Center Configuration Manager
*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os recursos de pré-lançamento são recursos que estão na Ramificação atual para testes iniciais em um ambiente de produção. Esses recursos têm suporte total, mas ainda estão em desenvolvimento ativo e podem receber alterações até que saiam da categoria de pré-lançamento.

 Antes de poder usar os recursos de pré-lançamento, você deverá dar consentimento para usar Recursos de pré-lançamento dentro do console do Configuration Manager antes de selecionar e habilitar seu uso.  

Dar o consentimento é uma ação única por hierarquia que não pode ser desfeita. Até dar o consentimento, você não pode habilitar novos recursos de pré-lançamento incluídos com a atualização. Após ativar um recurso de pré-lançamento, não será possível desativá-lo.

Para dar consentimento, no console, vá até **Administração** > **Configuração do Site** > **Sites** e escolha **Configurações da Hierarquia**. Na guia **Geral**, escolha **Consentir com o uso de recursos de pré-lançamento**.

Quando você instala uma atualização que inclui recursos de pré-lançamento, esses recursos são visíveis no Assistente de Atualizações e Manutenção com os recursos regulares incluídos na atualização:
  - **Se você tiver consentido:** você poderá habilitar os recursos de pré-lançamento no Assistente de Atualizações e Manutenção quando estiver instalando a atualização. Para fazer isso, selecione os recursos de pré-lançamento como faria com qualquer outro recurso.     

    Você também pode esperar para habilitar um recurso de pré-lançamento mais tarde do nó **Administração** > **Atualizações e Manutenção** > **Recursos** do console. No nó **Recursos**, escolha o recurso e escolha **Ativar**. Essa opção está esmaecida até você dar consentimento. (Antes da versão 1702, Atualizações e Manutenção ficava em **Administração** > **Serviços de Nuvem**.)
  -   **Se você não tiver consentido:** ao instalar uma atualização, os recursos de pré-lançamento ficarão visíveis no Assistente de Atualizações e Manutenção, mas ficarão esmaecidos e não poderão ser habilitados. Após a atualização ser instalada, você poderá exibir esses recursos no nó **Recursos**. No entanto, você não poderá habilitá-las até dar consentimento nas **Configurações de Hierarquia**.

Se você tiver dado consentimento em um site primário autônomo e, depois, expandir a hierarquia instalando um novo site de administração central, você deverá dar consentimento novamente no site de administração central.

 Ao habilitar um recurso de pré-lançamento, o gerenciador de hierarquia (HMAN) do Configuration Manager deve processar a alteração antes desse recurso ser disponibilizado. O processamento da alteração costuma ser imediato, mas pode levar até 30 minutos para ser concluído, dependendo do ciclo de processamento do HMAN. Após o processamento da alteração, é necessário reiniciar o console antes de exibir a nova interface do usuário relacionada a esse recurso.

**Os seguintes recursos de pré-lançamento estão disponíveis:**

 |Recurso          |Adicionado como pré-lançamento | Adicionado como recurso completo|  
|------------------|---------------------|---------------------|
| Executar Etapa da Sequência de Tarefas <!-- 1261338 --> |  [Versão 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Windows Defender Exploit Guard <!-- 1355468 --> |  [Versão 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Criar e executar scripts do PowerShell do console do Configuration Manager <!-- 1236459 --> |  [Versão 1706](/sccm/apps/deploy-use/create-deploy-scripts)|![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Gerenciamento do Device Guard com Configuration Manager <!-- 1319346 --> |  [Versão 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Pré-cache do conteúdo de sequência de tarefas <!-- 1021244 --> |  [Versão 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) | [Versão 1706](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
| Verificar se há arquivos executáveis antes de instalar um aplicativo <!-- 1284624 --> |   [Versão 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |[Versão 1706](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application)|
| Ponto de serviço do Data Warehouse <!-- 1277922 --> |  [Versão 1702](/sccm/core/servers/manage/data-warehouse) |[Versão 1706](/sccm/core/servers/manage/data-warehouse)|
| Cache de Pares para distribuição de conteúdo para clientes <!-- 1101436 --> |  [Versão 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) | [Versão 1710](/sccm/core/plan-design/hierarchy/client-peer-cache)|
| Gateway de gerenciamento de nuvem <!-- 1101764 --> |  [Versão 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Conector do Microsoft Operations Management Suite <!-- 1236739 --> | [Versão 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Realização de serviços em uma coleção com reconhecimento de cluster (realização de serviços em um grupo de servidores) <!-- 1081776 --> | [Versão 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Acesso condicional para PCs gerenciados pelo System Center Configuration Manager <!--  --> | [Versão 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     | [Versão 1702](/sccm/mdm/deploy-use/manage-access-to-services)                     |
