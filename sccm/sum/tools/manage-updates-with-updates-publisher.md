---
title: Gerenciar atualizações
titleSuffix: Configuration Manager
description: Gerencie as atualizações implantadas e criadas com o System Center Updates Publisher
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cd64994c-b426-4465-96cd-54b0edc2778d
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: d0d69990fe99f9b08c9c14222a2d1a9c6ec06b4c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="manage-software-updates-in-updates-publisher"></a>Gerenciar atualizações de software no Updates Publisher

*Aplica-se ao: System Center Updates Publisher*     

No System Center Updates Publisher, use o **Espaço de Trabalho de Atualizações** para gerenciar atualizações de software e pacotes que você importou para o repositório.  

As tarefas de gerenciamento incluem duplicação, edição e expiração ou reativação de atualizações e pacotes, e atribuição de atualizações e pacotes às publicações. Você também pode exportar catálogos personalizados para uso com outras instalações do Updates Publisher.

Para obter atualizações que você pode gerenciar:
-  [Adicione um catálogo de atualizações](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs) à sua instalação do Updates Publisher
-  [Importe](/sccm/sum/tools/updates-publisher-catalogs#import-updates) as atualizações desse catálogo para seu repositório.

Você também pode [criar suas próprias atualizações](/sccm/sum/tools/create-updates-with-updates-publisher).



## <a name="create-a-duplicate-of-an-update"></a>Criar uma duplicata de uma atualização
Você pode criar duplicatas, ou cópias, de atualizações que estão no repositório. Depois, você pode modificar a cópia em vez de modificar a atualização original. Não é possível criar cópias dos pacotes de atualização.

Para criar uma cópia, selecione uma atualização no **Espaço de Trabalho de Atualizações** e depois escolha **Duplicar**. A cópia da atualização aparece no mesmo local no Espaço de Trabalho de Atualizações com *Cópia de* adicionado ao seu nome.

Uma nova cópia criada por você tem um status de **Não expirada**, mas, caso contrário, retém as configurações do original.

## <a name="edit-updates-and-bundles"></a>Editar atualizações e pacotes
Você pode selecionar atualizações e pacotes que estão em seu repositório para modificá-los.

No **Espaço de Trabalho de Atualizações**, selecione uma atualização ou pacote e selecione **Editar** na guia **Início** para abrir o assistente para edição. Cada atualização e pacote possui assistentes separados, porém bem relacionados que apresentam as mesmas opções que os assistentes [Criar Atualização](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard) ou [Criar Pacote](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-bundle-wizard).

Durante a edição, você pode alterar todos os detalhes disponíveis sobre a atualização ou pacote para que possa ser usado em seu ambiente. Por exemplo, você pode editar as regras de aplicabilidade ou precedência ou alterar o idioma. Você também pode alterar o produto e o fornecedor para mover a atualização ou agrupar para uma pasta personalizada, a fim de agrupar as atualizações para seu próprio uso.

## <a name="assign-updates-and-bundles-to-a-publication"></a>Atribuir pacotes e atualizações a uma publicação
Você pode selecionar as atualizações e pacotes no **Espaço de Trabalho de Atualizações** e, em seguida, escolher **Atribuir** na guia **Início** da faixa de opções para adicioná-las a uma publicação. Isso inicia o assistente **Atribuir Atualizações de Software**.
-  Consulte [Publicar atualizações e pacotes](#publish-updates-and-bundles-from-the-updates-workspace) para obter informações sobre como selecionar e publicar atualizações e pacotes como uma única tarefa.
-  Confira [Gerenciar publicações](/sccm/sum/tools/updates-publisher-publications) para obter informações sobre como gerenciar grupos de atualizações e pacotes como um único objeto. Depois de atribuir atualizações a uma publicação, você pode gerenciar essa publicação, que, por sua vez, incluirá todas as suas atualizações atribuídas.

Ao atribuir atualizações a uma publicação:

-   Você pode incluir atualizações e pacotes expirados e não expirados na mesma publicação.

-   Especifique o tipo de publicação:

    -   **Conteúdo Completo** – Isso publica todo o conteúdo da atualização no servidor WSUS. Isso inclui os metadados e os binários de atualização.

    -   **Somente metadados** – Isso publica apenas os metadados; os binários de atualização não são publicados. Você pode escolher essa opção quando quiser coletar dados de conformidade.

    -   **Automático** – Esse modo só estará disponível quando você conectar o Updates Publisher ao Configuration Manager (consulte a opção [Servidor do ConfigMgr](/sccm/sum/tools/updates-publisher-options#configmgr-server).)

    Com esse tipo, o Updates Publisher consulta o Configuration Manager para determinar se as atualizações ou pacotes devem ser publicados com conteúdo completo ou somente metadados. O conteúdo completo de uma atualização é publicado somente quando a atualização atinge o **Limite de contagem de solicitação do cliente** e **Limite de tamanho de origem do pacote**, que são especificados na página de opções do Updates Publisher do **Servidor do ConfigMgr**.

-   Selecione uma publicação:

    -   Use **Atribuir a atualização de software para publicações existentes** quando você já tiver criado uma publicação que deseja usar. Essa opção não está disponível até que exista pelo menos uma publicação.

    -   Use **Atribuir a atualização de software para uma nova publicação** quando você não tiver uma publicação adequada. Isso criará uma nova publicação com o nome especificado por você.

Depois de atribuir atualizações a uma publicação, use o **Espaço de Trabalho de Publicação** para [publicar](/sccm/sum/tools/updates-publisher-publications#publish-pubilcations) ou [exportar](/sccm/sum/tools/updates-publisher-publications#export-a-pubilcation) a publicação como um grupo.

## <a name="publish-updates-and-bundles-from-the-updates-workspace"></a>Publicar atualizações e pacotes do Espaço de Trabalho de Atualizações
Quando você publica atualizações e pacotes, o Updates Publisher adiciona informações sobre essas atualizações e pacotes (metadados) e, possivelmente, os binários para as atualizações (conteúdo completo) para um servidor de atualização para implantação em dispositivos.

Antes de você ter a opção de publicar, é necessário configurar a opção [Servidor de Atualização](/sccm/sum/tools/updates-publisher-options#update-server) para o Updates Publisher. Para abrir essa opção de configuração, acesse **Espaço de Trabalho de Atualizações** &gt; **Visão geral** e selecione **Configurar WSUS e Certificado de Assinatura.** Você também pode acessar a página do Servidor de Atualização nas opções do Updates Publisher.

Há duas maneiras de publicar pacotes e atualizações:
-   Diretamente do Espaço de Trabalho de Atualizações. (Consulte o procedimento a seguir, *Para publicar atualizações e pacotes*.)
-   Como uma [publicação](/sccm/sum/tools/updates-publisher-publications#publish-pubilcations) do Espaço de Trabalho de Publicações.  

> [!NOTE]   
> O Updates Publisher só pode publicar atualizações com 375 megabytes (MB) ou menos de tamanho.

### <a name="to-publish-updates-and-bundles"></a>Para publicar atualizações e pacotes
1.  Acesse **Espaço de Trabalho de Atualizações** e selecione uma ou mais atualizações e pacotes que você deseja publicar. Em seguida, escolha **Publicar** na guia **Início** da faixa de opções.

2.  Na página **Selecionar** do assistente **Publicar**, selecione como você deseja publicar as atualizações. As opções são as mesmas para [atribuição de atualizações](#assign-updates-and-bundles-to-a-publication): **Conteúdo Completo**, **Somente metadados** ou **Automáticas**.

    Também é possível escolher assinar todas as atualizações com um novo certificado de publicação.

3.  Conclua o assistente.

Se a publicação falhar, você receberá um link para o arquivo UpdatesPublisher.log que pode fornecer mais informações.

## <a name="export-updates"></a>Exportar atualizações
Você pode exportar atualizações e pacotes de seu repositório do Updates Publisher para criar um catálogo de atualizações personalizadas. Em seguida, você pode [adicionar](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs) e depois [importar](/sccm/sum/tools/updates-publisher-catalogs#mport-updates) esse catálogo para outra instância do Updates Publisher. (Você também pode [exportar atualizações como uma publicação](/sccm/sum/tools/updates-publisher-publications##export-a-publication).)

Para exportar diretamente, acesse o **Espaço de Trabalho de Atualizações** > **Todas as Atualizações de Software** e selecione um ou mais pacotes e atualizações. Não é possível exportar uma pasta de fornecedor ou de produto, mas você pode selecionar uma pasta e, depois, selecionar as atualizações dessa pasta para exportação.

Com uma ou mais atualizações selecionadas, escolha **Exportar** na guia **Início** da faixa de opções e forneça um caminho e nome de arquivo para a exportação do catálogo.

Você terá a opção de exportar (incluir) atualizações de software dependentes.

## <a name="delete-updates-and-bundles"></a>Excluir atualizações e pacotes
Você pode excluir atualizações e pacotes de atualizações para removê-los do repositório do Updates Publisher.

Acesse o **Espaço de Trabalho de Atualizações** > **Todas as Atualizações de Software** e selecione uma ou mais atualizações individuais. Escolha **Excluir** na guia **Início** da faixa de opções.

-   Se a seleção contiver apenas atualizações ou pacotes que não foram publicados ou que expiraram, você receberá uma solicitação para confirmar a exclusão antes da remoção.

-   Se a seleção incluir uma atualização ou um pacote que tenha sido publicado e ainda não expirou, você receberá um aviso. Você deve [expirar](/sccm/sum/tools/updates-publisher-pubilcations#expire-or-reactivate-updates-and-bundles) essas atualizações e, em seguida, publicar essa alteração antes de excluí-las do repositório.  

Se você excluir uma atualização ou pacote de um fornecedor e, depois, importar novamente esse catálogo, essa atualização será restaurada para seu repositório.

## <a name="manage-vendor-and-product-folders"></a>Gerenciar pastas de fornecedor e de produto
Para exibir uma lista de fornecedores, e produtos para cada fornecedor para o qual você importou ou criou atualizações, acesse **Espaço de Trabalho de Atualizações** > **Visão geral** > **Todas as Atualizações de Software**.

Pastas de fornecedores e produtos são criadas automaticamente pelo Updates Publisher quando você usa um assistente para importar ou criar uma atualização de software ou pacote. Você também pode criar essas pastas manualmente.

-   Para criar uma pasta de fornecedor, no painel de navegação do **Espaço de Trabalho de Atualizações**, clique com o botão direito em **Todas as Atualizações de Software** e escolha **Criar Fornecedor**.

-   Para criar uma pasta de produto em uma pasta de fornecedor, clique na pasta de fornecedor e escolha **Criar Produto**.

Além de criar pastas, você pode renomear ou excluir qualquer pasta de fornecedor ou produto no repositório. Para fazer isso, clique com o botão direito na pasta e escolha a opção desejada, **Renomear** ou **Excluir**. A exclusão de uma pasta remove todas as atualizações e pacotes nessa pasta e suas pastas de produto respectivas do repositório do Updates Publisher.

Você pode mover as atualizações entre fornecedores e pastas do produto, incluindo para pastas que você criar. Para mover uma atualização ou pacote para uma nova pasta, selecione e **Edite** a atualização ou pacote. Em seguida, na página **Informações** do assistente para Editar Atualização, reatribua o fornecedor e o produto. Quando o assistente para **Editar Atualização** for concluído, a alteração se aplicará e a atualização será transferida para a nova pasta.

## <a name="view-the-xml-of-an-update-or-bundle"></a>Exibir o XML de uma atualização ou pacote
Você pode selecionar uma única atualização ou pacote no **Espaço de Trabalho de Atualizações** e, em seguida, escolher **Exibir** XML para exibir a estrutura em XML da atualização. Não há opções para editar a estrutura em XML diretamente.
