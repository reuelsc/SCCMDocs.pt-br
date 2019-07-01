---
title: Updates Publisher
titleSuffix: Configuration Manager
description: Usar o System Center Updates Publisher para gerenciar atualizações personalizadas
ms.date: 6/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 26ad3be032a3dd8ea21d7eeb6a4755c32d546f38
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67158624"
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*Aplica-se ao: System Center Updates Publisher*

O System Center Updates Publisher (Updates Publisher) é uma ferramenta autônoma que permite que os fornecedores independentes de software ou os desenvolvedores de aplicativos de linha de negócios gerenciem atualizações personalizadas. Esse gerenciamento de atualizações personalizadas inclui as atualizações que têm dependências, como drivers e pacotes de atualização.

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


**Workspace de Atualizações:** use este workspace para [criar](/sccm/sum/tools/create-updates-with-updates-publisher) e [gerenciar](/sccm/sum/tools/manage-updates-with-updates-publisher) atualizações de software e pacotes de atualização. Esse workspace inclui a atribuição de atualizações e pacotes a uma publicação, a própria publicação e exportação para outro repositório do Updates Publisher.

**Workspace de Publicações:** é nesse workspace que você [gerencia as publicações](/sccm/sum/tools/updates-publisher-publications). Uma publicação é um grupo de atualizações que você cria para simplificar a exportação e a publicação das atualizações.

O gerenciamento de publicações inclui a publicação de atualizações em um servidor para que os clientes possam localizar e instalá-las, exportar atualizações e pacotes para uso de outras instalações do Updates Publisher ou modificação do conteúdo ou detalhes de uma publicação.

**Workspace de Regras:** é neste local que você [gerencia regras de aplicabilidade](/sccm/sum/tools/updates-publisher-applicability-rules) que podem ser salvas e, em seguida, usadas com as atualizações implantadas. Há dois tipos de regras:

-   Regras instaláveis – Essas regras ajudam a determinar se um cliente deve instalar uma atualização.
-   Regras instaladas – Essas regras verificam se uma atualização já está instalada.

**Workspace de Catálogos:** use esse workspace para adicionar e [gerenciar catálogos de atualizações de software](/sccm/sum/tools/updates-publisher-catalogs). Esse workspace inclui a importação de atualizações de software desses catálogos para o repositório do Updates Publisher.

## <a name="whats-new-in-the-system-center-updates-publisher-preview"></a>O que há de novo na versão prévia do System Center Updates Publisher

>[!NOTE] 
>As informações nesta seção se aplicam somente a versão de visualização do System Center Updates publisher. Para instalar a versão prévia, baixá-lo a [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=58390).

Há um modo de criação de novo na versão prévia para o System Center Updates Publisher para ajudá-lo a criar suas atualizações. Quando você habilita o modo de criação, uma **espaço de trabalho de categorias** é adicionado à tela inicial. Uma nova **Detectoid** botão também é adicionado para o **espaço de trabalho atualizações** quando o modo de criação está habilitado. 

### <a name="to-enable-authoring-mode-in-the-preview"></a>Para habilitar o modo de criação na versão prévia

1. No canto superior esquerdo do console, clique no **Updates Publisher** **Properties** guia e, em seguida, escolha **opções**.
1. Vá para o **Authoring** opções.
1. Marque a caixa **habilitar modo de criação**.

![Habilitar o modo de criação para o Updates Publisher](media/scup-enable-authoring-mode.png)

### <a name="about-the-categories-workspace"></a>Sobre o espaço de trabalho de categorias

O espaço de trabalho de categorias permite que os autores de atualização organizar as atualizações que pertencem juntas. Por exemplo, se você for um OEM, talvez você queira organizar suas atualizações com base em modelos ou linhas de produtos. Você pode definir várias categorias e categorias filho, mas a categorias filho não geral como você está limitadas a dois níveis.

![Captura de tela do espaço de trabalho de categorias](media/scup-categories-workspace.png)

### <a name="assign-an-update-to-a-category"></a>Atribuir uma atualização a uma categoria

Depois que você tiver criado sua atualização, você pode atribuí-lo a uma categoria selecionando a atualização, em seguida, clicando na **categorizar** botão. Você pode também a atualização com o botão direito e selecione **categorizar**.

![Captura de tela de categorizar uma atualização](media/scup-categorize-update.png)


### <a name="about-detectoids"></a>Sobre detectoids

Após habilitar o modo de criação, você pode criar detectoids para atualizações. Detectoids são úteis quando você tem várias atualizações que usam a mesma regra (ou um conjunto de regras) para determinar a aplicabilidade. Nesses casos, crie um detectoid e atribuí-lo como um pré-requisito para uma atualização. Você pode atribuir várias detectoids para uma atualização de autoria.


### <a name="create-a-detectoid"></a>Criar um detectoid

1. Abra o **Workspace de Atualizações**.
1. Na faixa de opções, clique o **Detectoid** botão.
1. Siga os prompts no Assistente para criar seu detectoid.



![Pré-requisitos de atualização usando um detectoid](media/scup-detectoid-as-prerequisite.png)


## <a name="next-steps"></a>Próximas etapas
Para começar, primeiro [instale](/sccm/sum/tools/install-updates-publisher)e depois [configure as opções](/sccm/sum/tools/updates-publisher-options) do Updates Publisher.
