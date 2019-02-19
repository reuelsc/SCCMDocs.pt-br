---
title: Updates Publisher
titleSuffix: Configuration Manager
description: Usar o System Center Updates Publisher para gerenciar atualizações personalizadas
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0f21e087e73a26191af56793e0015cbb21e8714c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136527"
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*Aplica-se a: System Center Updates Publisher*

O System Center Updates Publisher (Updates Publisher) é uma ferramenta autônoma que permite que os fornecedores independentes de software ou os desenvolvedores de aplicativos de linha de negócios gerenciem atualizações personalizadas. Isso inclui atualizações com dependências, como drivers e pacotes de atualização.

Com o Updates Publisher, você pode:

-   Importar atualizações de catálogos externos (catálogos de atualização diferentes da Microsoft).
-   Modificar definições de atualização, incluindo a aplicabilidade e os metadados de implantação.
-   Exportar atualizações para catálogos externos.
-   Publicar atualizações em um servidor de atualização.

Depois de publicar as atualizações em um servidor de atualização, você pode usar System Center Configuration Manager para detectar e implantar essas atualizações em seus dispositivos gerenciados.

> [!TIP]  
> A versão anterior, [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/?LinkId=848111), permanece com suporte. Essa versão atualizada mantém a mesma funcionalidade, mas oferece suporte a outros sistemas operacionais, novos recursos para simplificar algumas tarefas e tem uma interface de usuário atualizada.

## <a name="workspaces"></a>Workspaces
Quando você abre o Updates Publisher, ele mostra como padrão o nó Visão geral do *Workspace de Atualizações.*

![Console do Updates Publisher](media/console1.png)   


O Updates Publisher tem quatro workspaces para ajudar a organizá-lo.


**Workspace de atualizações:** use este workspace para [criar](/sccm/sum/tools/create-updates-with-updates-publisher) e [gerenciar](/sccm/sum/tools/manage-updates-with-updates-publisher) atualizações de software e pacotes de atualização. Isso inclui a atribuição de atualizações e pacotes a uma publicação, publicação e exportação para outro repositório do Updates Publisher.

**Workspace de publicações:** é nesse local que você [gerencia as publicações](/sccm/sum/tools/updates-publisher-publications). Uma publicação é um grupo de atualizações que você cria para simplificar a exportação e a publicação das atualizações.

O gerenciamento de publicações inclui a publicação de atualizações em um servidor para que os clientes possam localizar e instalá-las, exportar atualizações e pacotes para uso de outras instalações do Updates Publisher ou modificação do conteúdo ou detalhes de uma publicação.



**Workspace de regras:** é nesse local que você [gerencia as regras de aplicabilidade](/sccm/sum/tools/updates-publisher-applicability-rules) que podem ser salvas e, em seguida, usadas com as atualizações implantadas. Há dois tipos de regras:

-   Regras instaláveis – Essas regras ajudam a determinar se um cliente deve instalar uma atualização.
-   Regras instaladas – Essas regras verificam se uma atualização já está instalada.

**Workspace de catálogos:** use esse workspace para adicionar e [gerenciar catálogos de atualizações de software](/sccm/sum/tools/updates-publisher-catalogs). Isso inclui a importação de atualizações de software desses catálogos para o repositório do Updates Publisher.
## <a name="first-steps"></a>Primeiras etapas
Para começar, primeiro [instale](/sccm/sum/tools/install-updates-publisher)e depois [configure as opções](/sccm/sum/tools/updates-publisher-options) do Updates Publisher.
