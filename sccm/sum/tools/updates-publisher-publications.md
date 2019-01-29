---
title: Gerenciar publicações
titleSuffix: Configuration Manager
description: Gerenciar grupos de atualizações de software como uma publicação com o System Center Updates Publisher
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: e6c1df1d-7728-4980-9199-bc32cde5439e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f626d07d1fe25d8277ab2189f136862079dc503c
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54896617"
---
# <a name="manage-publications-in-updates-publisher"></a>Gerenciar publicações no Updates Publisher

*Aplica-se a: System Center Updates Publisher*

Use publicações para gerenciar grupos de atualizações e pacotes como um único objeto. Isso inclui a publicação de atualizações para um servidor de gerenciamento e a exportação da publicação como grupo para uso com outra instalação do Updates Publisher.

## <a name="create-publications"></a>Criar publicações
As publicações são criadas de duas maneiras:

-   Quando você gerencia atualizações e pacotes no **Workspace de Atualizações**, é possível [atribui-las](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication) a uma nova publicação criada no momento.

-   No **Workspace de Publicações,** você pode usar o botão **Criar** na guia **Publicação** da faixa de opções. Este método permite que você crie uma publicação para uso futuro. Posteriormente, ao atribuir as atualizações, você pode usar essa publicação.

## <a name="rename-a-publication"></a>Renomear uma publicação
Para renomear uma publicação, selecione a publicação de dentro do **Workspace de Publicações** e, na guia **Publicação** da faixa de opções, escolha **Editar**.

## <a name="change-the-publication-type-of-updates-in-a-publication"></a>Alterar o tipo de publicação de atualizações em uma publicação
No **Workspace de Publicação**, você pode modificar o **tipo de publicação** de atualizações e pacotes que são atribuídos a uma publicação.

1. Selecione a publicação que contém as atualizações que você deseja modificar e, em seguida, selecione uma ou mais atualizações ou pacotes na lista **Todas&lt;nome da publicação > atualizações de membro**.

2. Em seguida, na guia **Início**, escolha uma das seguintes opções. As opções disponíveis dependem do tipo de publicação das atualizações que você selecionou.

   -   **Automática**
   -   **Conteúdo Completo**
   -   **Somente metadados**

Depois de fazer uma alteração, você precisará atualizar a exibição da publicação para ver os novos valores.

Para saber mais sobre os tipos de publicação diferentes, veja [Atribuir pacotes e atualizações para uma publicação](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication).

> [!TIP]    
> Ao definir o tipo de publicação de um pacote, todas as atualizações de software nesse pacote são publicadas com o tipo de publicação desse pacote.

## <a name="remove-updates-from-a-publication"></a>Remover as atualizações de uma publicação
Para remover as atualizações ou pacotes de uma publicação, no **Workspace de Publicações**, selecione a publicação que você deseja modificar e, em seguida, selecione as atualizações e os pacotes que você quer remover. Em seguida, na guia **Início** da faixa de opções, escolha **Remover**.

Após a remoção das atualizações de uma publicação, elas permanecem disponíveis no repositório do Updates Publisher.

## <a name="publish-publications"></a>Publicar publicações
Quando você publica atualizações e pacotes, o Updates Publisher adiciona informações sobre essas atualizações e pacotes (metadados) e, possivelmente, os binários para as atualizações (conteúdo completo) para um servidor de atualização para implantação em dispositivos.

Antes de você ter a opção de publicar, é necessário configurar a opção [Servidor de Atualização](/sccm/sum/tools/updates-publisher-options#update-server) para o Updates Publisher. Para abrir essa opção de configuração, acesse **Workspace de Atualizações**&gt;**Visão geral** e selecione **Configurar WSUS e Certificado de Assinatura.** Você também pode acessar a página do Servidor de Atualização nas opções do Updates Publisher.

> [!NOTE]   
> O Updates Publisher só pode publicar atualizações com 375 megabytes (MB) ou menos de tamanho.

### <a name="to-publish-a-publication"></a>Para publicar uma publicação

1. Acesse o **Workspace de Publicações** e, em seguida, selecione uma publicação que contém o grupo de atualizações e pacotes que você deseja publicar ou exportar. Em seguida, escolha **Publicar** na guia **Início** da faixa de opções.

2. Na página **Selecionar** do assistente para **Publicar**, você pode escolher assinar todas as atualizações com um novo certificado de publicação, mas não pode alterar o tipo de publicação.

3. Conclua o assistente.

   Se a publicação falhar, você receberá um link para o arquivo UpdatesPublisher.log que pode fornecer mais informações.

## <a name="export-a-publication"></a>Exportar uma publicação
Você pode exportar uma publicação de seu repositório do Updates Publisher. Isso exporta as atualizações e os pacotes que são atribuídos a essa publicação e cria um catálogo de atualizações. Depois, você pode [adicionar](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs) e depois [importar](/sccm/sum/tools/updates-publisher-catalogs#mport-updates) esse catálogo para outra instância do Updates Publisher. Você também pode [exportar atualizações](/sccm/sum/tools/manage-updates-with-updates-publisher#export-updates) que não fazem parte de uma publicação.

Para exportar uma publicação, acesse o **Workspace de Publicações** e selecione a publicação que contém as atualizações que você deseja exportar. Você só pode selecionar uma publicação por vez.

Com a publicação selecionada, escolha **Exportar** na guia **Início** da faixa de opções e forneça um caminho e nome de arquivo para a exportação do catálogo.

Você também tem a opção de exportar (incluir) atualizações de software dependentes como parte da exportação.

## <a name="rename-a-publication"></a>Renomear uma publicação
Para renomear uma publicação, selecione a publicação no **Workspace de Publicações** e escolha **Editar** na guia **Publicação** da faixa de opções.

## <a name="delete-a-publication"></a>Excluir uma publicação
Para excluir uma publicação, selecione a publicação no **Workspace de Publicações** e escolha **Excluir** na guia **Publicação** da faixa de opções.

Após a remoção da publicação do Updates Publisher, as atualizações que estavam na publicação permanecerão disponíveis no repositório do Updates Publisher.

## <a name="expire-or-reactivate-updates-and-bundles"></a>Expirar ou reativar pacotes e atualizações
Você pode usar o **Workspace de Atualizações** para selecionar e, em seguida, expirar ou reativar pacotes e atualizações. Você pode expirar e reativar atualizações e pacotes quantas vezes quiser.

-   **Para expirar atualizações ou pacotes**, no Workspace de Atualizações, selecione uma ou mais atualizações ou pacotes que não expiraram e, em seguida, escolha **Expirar** na guia **Início**. Até que você publique a atualização ou o pacote como expirados no Configuration Manager, você poderá reativá-la.

    Antes de remover (excluir) uma atualização ou pacote personalizado do Configuration Manager, você deve expirá-la e publicar esse status de expirado no Configuration Manager. Após a expiração das atualizações ou pacotes no Configuration Manager, não será mais possível implantar ou reativar o pacote ou a atualização.

-   **Para reativar as atualizações ou pacotes**, no Workspace de Atualizações, selecione uma ou mais atualizações expiradas e escolha **Reativar** na guia **Início** da faixa de opções. Se a atualização expirada tiver sido publicada anteriormente como expirada no Configuration Manager, não será possível reativá-la.
