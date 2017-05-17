---
title: Updates Publisher | Microsoft Docs
description: "Usar o System Center Updates Publisher para gerenciar atualizações personalizadas"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
caps.latest.revision: 1
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.translationtype: Human Translation
ms.sourcegitcommit: 31819a1df4e63e1114682490a9b3c3b4e5c99cfa
ms.openlocfilehash: f4951c204b32da58174b94a539b380c278fa9756
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017

---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*Aplica-se ao: System Center Updates Publisher*

O System Center Updates Publisher (Updates Publisher) é uma ferramenta autônoma que permite aos fornecedores de software independentes ou desenvolvedores de aplicativos de linha de negócios o gerenciamento de atualizações personalizadas. Isso inclui atualizações com dependências, como drivers e pacotes de atualização.

Com o Updates Publisher, você pode:

-   Importar atualizações de catálogos externos (catálogos de atualização diferentes da Microsoft).
-   Modificar definições de atualização, incluindo a aplicabilidade e os metadados de implantação.
-   Exportar atualizações para catálogos externos.
-   Publicar atualizações em um servidor de atualização.

Depois de publicar as atualizações em um servidor de atualização, você pode usar System Center Configuration Manager para detectar e implantar essas atualizações em seus dispositivos gerenciados.

> [!TIP]  
> A versão anterior, [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/?LinkId=848111), permanece com suporte. Essa versão atualizada mantém a mesma funcionalidade, mas oferece suporte a outros sistemas operacionais, novos recursos para simplificar algumas tarefas e tem uma interface de usuário atualizada.

## <a name="workspaces"></a>Espaços de trabalho
Quando você abre o Updates Publisher, ele mostra como padrão o nó Visão geral do *Espaço de Trabalho de Atualizações.*

![Console do Updates Publisher](media/console1.png)   


O Updates Publisher tem quatro espaços de trabalho para ajudar a organizá-lo.


**Espaço de Trabalho de Atualizações:** use este espaço de trabalho para [criar](/sccm/sum/tools/create-updates-with-updates-publisher) e [gerenciar](/sccm/sum/tools/manage-updates-with-updates-publisher) atualizações de software e pacotes de atualização. Isso inclui a atribuição de atualizações e pacotes a uma publicação, publicação e exportação para outro repositório do Updates Publisher.

**Espaço de Trabalho de Publicações:** e neste local que você [gerencia as publicações](/sccm/sum/tools/updates-publisher-publications). Uma publicação é um grupo de atualizações que você cria para simplificar a exportação e a publicação das atualizações.

O gerenciamento de publicações inclui a publicação de atualizações em um servidor para que os clientes possam localizar e instalá-las, exportar atualizações e pacotes para uso de outras instalações do Updates Publisher ou modificação do conteúdo ou detalhes de uma publicação.



**Espaço de Trabalho de Regras:** é neste local que você [gerencia regras de aplicabilidade](/sccm/sum/tools/updates-publisher-applicability-rules) que podem ser salvas e, em seguida, usadas com as atualizações implantadas. Há dois tipos de regras:

-   Regras instaláveis – Essas regras ajudam a determinar se um cliente deve instalar uma atualização.
-   Regras instaladas – Essas regras verificam se uma atualização já está instalada.

**Espaço de Trabalho de Catálogos:** use esse espaço de trabalho para adicionar e [gerenciar catálogos de atualizações de software](/sccm/sum/tools/updates-publisher-catalogs). Isso inclui a importação de atualizações de software desses catálogos para o repositório do Updates Publisher.
## <a name="first-steps"></a>Primeiras etapas
Para começar, primeiro [instale](/sccm/sum/tools/install-updates-publisher)e depois [configure as opções](/sccm/sum/tools/updates-publisher-options) do Updates Publisher.

