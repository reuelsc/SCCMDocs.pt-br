---
title: Procedimentos para grupos de limites
titleSuffix: Configuration Manager
description: Configure grupos de limites para organizar de maneira lógica os locais de rede relacionados chamados limites.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a1fe22d0-4695-4de0-8bf0-e3475b03cf0e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7a7438a2815f615b029888d8fb1ca28f601735d5
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140003"
---
# <a name="how-to-configure-boundary-groups-for-configuration-manager"></a>Como configurar grupos de limites para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo inclui procedimentos sobre como configurar grupos de limites. Antes de começar, é preciso entender os conceitos de grupo de limites. Para obter mais informações, consulte [Grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).



## <a name="bkmk_create"></a> Criar um grupo de limites  

1.  No console do Configuration Manager, acesse o espaço de trabalho **Administração**, expanda a **Configuração da Hierarquia** e selecione o nó **Grupos de Limite**.  

2.  Na guia **Início**, no grupo **Criar**, selecione **Criar Grupo de Limites**.  

3.  Na caixa de diálogo **Criar Grupo de Limites**, na guia **Geral** e especifique um **Nome** para esse grupo de limites. Opcionalmente, inclua uma **Descrição**.  

4.  Selecione **OK** para salvar o novo grupo de limites, ou continue na próxima seção para configurar o grupo de limites.  


## <a name="bkmk_config"></a> Configurar um grupo de limites  

1.  No console do Configuration Manager, acesse o espaço de trabalho **Administração**, expanda a **Configuração da Hierarquia** e selecione o nó **Grupos de Limite**.  

2.  Selecione o grupo de limites que você deseja modificar e, em seguida, selecione **Propriedades** na faixa de opções. Essa ação abre a janela Propriedades do grupo de limites.  

Defina as seguintes configurações:  
- [Adicionar ou remover limites](#bkmk_add)  
- [Configurar a atribuição de site e selecionar servidores do sistema de site](#bkmk_references)  
- [Configurar o comportamento de fallback](#bkmk_bg-fallback)  
- [Configurar as opções de grupo de limites](#bkmk_options)  


### <a name="bkmk_add"></a> Adicionar ou remover limites

Na janela Propriedades do grupo de limites, use a guia **Geral** para modificar os limites membros desse grupo de limites:  

- Para adicionar limites, selecione **Adicionar**. Na janela Adicionar Limites, marque a caixa de seleção de um ou mais limites e selecione **OK**.  

- Para remover limites, selecione o limite na lista e selecione **Remover**.  


### <a name="bkmk_references"></a> Configurar a atribuição de site e selecionar servidores do sistema de site

Mara modificar a atribuição de site e a configuração do servidor do sistema de sites associado, alterne para a guia **Referências** na janela Propriedades do grupo de limites.  

- Para habilitar esse grupo de limites para uso pelos clientes para atribuição de site, selecione **Usar este grupo de limites para a atribuição de site**. Em seguida, selecione um site na lista suspensa **Site atribuído**. Para saber mais, confira [Atribuição de site](/sccm/core/servers/deploy/configure/boundary-groups#site-assignment).  

- Para associar os servidores do sistema de sites disponíveis a este grupo de limites, selecione **Adicionar**. A janela Adicionar Sistemas de Site lista apenas os servidores com suporte para funções do sistema de site. Marque a caixa de seleção de um ou mais servidores e selecione **OK**. Isso os adiciona como servidores do sistema de sites associados a este grupo de limites.  

    > [!NOTE]  
    >  É possível selecionar qualquer combinação de sistemas de sites disponíveis de qualquer site na hierarquia. Os sistemas de site selecionados são listados na guia **Sistemas de Site** nas propriedades de cada limite membro desse grupo de limites.  

- Para remover um servidor deste grupo de limites, selecione o servidor e selecione **Remover**.  

    > [!NOTE]  
    >  Para interromper o uso desse grupo de limites para a associação de sistemas de sites, remova todos os servidores listados como servidores do sistema de sites associados.  


### <a name="bkmk_bg-fallback"></a> Configurar o comportamento de fallback

Para configurar o comportamento de fallback, alterne para a guia **Relações** na janela Propriedades do grupo de limites.  

- Para criar uma relação com outro grupo de limites:  

  - Selecione **Adicionar**. Na janela Grupos de Limites de Fallback, selecione o grupo de limites para configuração.  

  - Defina o tempo de fallback para as seguintes funções do sistema de site:  
    - Ponto de distribuição  
    - Ponto de atualização de software  
    - Ponto de gerenciamento  

      > [!Note]  
      > Por exemplo, abra a janela Propriedades do grupo de limites Filial. Na janela Grupos de Limites de Fallback, selecione o grupo de limites Escritório Principal. Defina o tempo de fallback do ponto de distribuição como `20`. Ao salvar essa configuração, os clientes no grupo de limites Filial começam a pesquisar o conteúdo dos pontos de distribuição no grupo de limites Escritório Principal após 20 minutos.  

  - Para evitar o fallback para um grupo de limites específico, selecione o grupo de limites e selecione **Nunca fazer fallback** para o tipo de função do sistema de site. Essa ação pode incluir o *grupo de limites de site padrão*.  

- Para modificar a configuração de uma relação existente, selecione o grupo de limites na lista e selecione **Alterar**. Essa ação abre a janela Grupos de Limite de Fallback apenas para este grupo de limites.  
 
- Para remover uma relação, selecione o grupo de limites na lista e selecione **Remover**.  

Para saber mais, confira [Fallback](/sccm/core/servers/deploy/configure/boundary-groups#fallback). 


### <a name="bkmk_options"></a> Configurar as opções de grupo de limites
<!--1356193--> A partir da versão 1806, para configurar outras opções para clientes nesse grupo de limites, alterne para a guia **Opções**. Para saber mais, confira [Opções de grupo de limites para downloads de pares](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgoptions).

- **Permitir downloads de par nesse grupo de limites**: Essa opção é habilitada por padrão. O ponto de gerenciamento fornece aos clientes uma lista de locais de conteúdo que inclui fontes de pares.  

    - **Durante o download de par, usar apenas pares dentro da mesma sub-rede**: Essa configuração depende do que foi mostrado acima. Se você habilitar essa opção, o ponto de gerenciamento incluirá apenas as origens de pares de lista do local do conteúdo que estão na mesma sub-rede que o cliente.  


## <a name="bkmk_site-fallback"></a> Configurar um local de fallback para atribuição automática de site  

Se os clientes não estiverem em um grupo de limites com um site atribuído, atribua-os a esse site após a instalação.

1.  No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**.  

2.  Na guia **Início** da faixa de opções, no grupo **Sites**, selecione **Configurações de Hierarquia**.  

3.  Na guia **Geral**, marque a caixa de seleção para **Usar um local de fallback**. Depois, selecione um site na lista suspensa **Local de fallback**.  

4.  Selecione **OK** para salvar a configuração.  

Para saber mais, confira [Atribuição de site](/sccm/core/servers/deploy/configure/boundary-groups#site-assignment).


## <a name="bkmk_proc-prefer"></a> Habilitar o uso de pontos de gerenciamento preferenciais  

Para saber mais, confira [Pontos de gerenciamento preferidos](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_preferred).

1.  No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**.  

2. Na guia **Início** da faixa de opções, no grupo **Sites**, selecione **Configurações de Hierarquia**.  

3. Na guia **Geral**, selecione **Os clientes preferem usar os pontos de gerenciamento especificados em grupos de limite**.  

4. Selecione **OK** para salvar a configuração.  

