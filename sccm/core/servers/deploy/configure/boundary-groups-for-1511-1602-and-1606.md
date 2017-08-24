---
title: Grupos de limites para 1511, 1602 e 1606 | System Center Configuration Manager
description: "Use grupos de limites com as versões 1511, 1602 e 1606 do Configuration Manager."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dec1e0d7-5864-43a8-9f56-413923b3914e
caps.latest.revision: "10"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 311606b8d52645d3ca89642be4cc341b8a64ec56
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="boundary-groups-for-system-center-configuration-manager-version-1511-1602-and-1606"></a>Grupos de limites para as versões 1511, 1602 e 1606 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*
<!-- This topic drops from TOC with the release of version 1706 -->

As informações neste tópico são específicas para usar os grupos de limites com as versões 1511, 1602 e 1606 do System Center Configuration Manager.
Se você usar a versão 1610 ou posterior, veja [Configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) para obter informações sobre como usar os grupos de limites reprojetados.  


##  <a name="BKMK_BoundaryGroups"></a> Boundary groups  
 Você cria grupos de limites apara agrupar de logicamente locais de rede (limites) relacionados para facilitar o gerenciamento da infraestrutura de rede. É necessário atribuir limites a grupos de limites para poder usar o grupo de limites. Os clientes usam a configuração do grupo de limites para:  

-   Atribuição automática de site  

-   Local do conteúdo  

-   Pontos de gerenciamento preferenciais

    Se você usar pontos de gerenciamento preferenciais, deverá habilitar essa opção para a hierarquia, e não de dentro da configuração do grupo de limites. Veja o procedimento *Para habilitar o uso de pontos de gerenciamento preferenciais* posteriormente nesse tópico.  

Ao configurar grupos de limites, você adiciona um ou mais limites ao grupo de limites. Em seguida, define configurações adicionais para uso por clientes localizados nesses limites.  

#### <a name="to-create-a-boundary-group"></a>Para criar um grupo de limites  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** >  **Grupos de Limites**.  

2.  Na guia **Início**, no grupo **Criar**, clique em **Criar Grupo de Limites**.  

3.  Na caixa de diálogo **Criar Grupo de Limites**, selecione a guia **Geral** e especifique um **Nome** para esse grupo de limites.  

4.  Clique em **OK** para salvar o novo grupo de limites.  

#### <a name="to-set-up-a-boundary-group"></a>Para configurar um grupo de limites  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** >  **Grupos de Limites**.  

2.  Escolha o grupo de limites que você deseja alterar.  

3.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

4.  Na caixa de diálogo **Propriedades** do grupo de limites, selecione a guia **Geral** para alterar os limites que são membros desse grupo de limites:  

    -   Para adicionar limites, clique em **Adicionar**, marque a caixa de seleção para um ou mais limites e clique em **OK**.  

    -   Para remover limites, selecione o limite e clique em **Remover**.  

5.  Selecione a guia **Referências** para modificar a atribuição de site e a configuração do servidor do sistema de sites associado:  

    -   Para habilitar esse grupo de limites para uso de clientes para atribuição de sites, marque a caixa de seleção **Utilize este grupo de limites para a atribuição de site** e escolha um site na caixa suspensa **Site atribuído**.  

    -   Para configurar quais servidores do sistema de sites disponíveis estão associados a este grupo de limites:  

    1.  Selecione **Adicionar** e marque a caixa de seleção de um ou mais servidores. Os servidores são adicionados como servidores do sistema de sites associados a este grupo de limite. Somente os servidores que têm suporte para a função do sistema de sites instalada neles estão disponíveis.  

        > [!NOTE]  
        >  É possível selecionar qualquer combinação de sistemas de sites disponíveis de qualquer site na hierarquia. Os sistemas de site selecionados são listados na guia **Sistemas de Site** nas propriedades de cada limite membro desse grupo de limites.  

    2.  Para remover um servidor deste grupo de limites, selecione o servidor e clique em **Remover**.  

        > [!NOTE]  
        >  Para interromper o uso deste grupo de limites para a associação de sistemas de sites, você deve remover todos os servidores listados como servidores do sistema de sites associados.  

    3.  Para alterar a velocidade de conexão de rede de um servidor do sistema de sites para este grupo de limite, selecione o servidor e clique em **Alterar Conexão**.  

         Por padrão, a velocidade de conexão para cada sistema de sites é **Rápida**, podendo ser alterada para **Lenta**. A velocidade de conexão de rede e a configuração de uma implantação determinam se o cliente pode baixar o conteúdo do servidor.  

6.  Clique em **OK** para fechar as propriedades do grupo de limites e salvar a configuração.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>Para associar um servidor de implantação de conteúdo ou um ponto de gerenciamento a um grupo de limite  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** >  **Grupos de Limites**.  

2.  Escolha o grupo de limites que você deseja alterar.  

3.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

4.  Na caixa de diálogo **Propriedades** para o grupo de limites, selecione a guia **Referências**.  

5.  Em **Selecionar servidores do sistema de sites**, clique em **Adicionar**, marque a caixa de seleção para os servidores do sistema de sites que deseja associar a esse grupo de limites e clique em **OK**.  

6.  Clique em **OK** para fechar a caixa de diálogo e salvar a configuração do grupo de limites.  

#### <a name="to-enable-use-of-preferred-management-points"></a>para habilitar o uso de pontos de gerenciamento preferenciais  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração do Site** > **Sites** e, na guia **Início**, selecione **Configurações da Hierarquia**.  

2.  Na guia **Geral** das **Configurações da Hierarquia**, selecione **Os clientes preferem usar os pontos de gerenciamento especificados em grupos de limite**.  

3.  Clique em **OK** para fechar a caixa de diálogo e salvar a configuração.  

#### <a name="to-set-up-a-fallback-site-for-automatic-site-assignment"></a>Para configurar um local de fallback para atribuição automática de site  

1.  No console do Configuration Manager, escolha **Administração** > **Configuração de Site** >  **Sites**.  

2.  Na guia **Início**, no grupo **Sites**, escolha **Configurações da Hierarquia**.  

3.  Na guia **Geral**, marque a caixa de seleção **Usar um local de fallback** e selecione um local na lista suspensa **Local de fallback**.  

4.  Clique em **OK** para salvar a configuração.  

 As seções a seguir fornecem detalhes adicionais sobre configurações de grupo de limites.  

###  <a name="BKMK_BoundarySiteAssignment"></a> Sobre atribuição de site  
 É possível configurar cada grupo de limites com um site atribuído para clientes.  

-   Um cliente recém-instalado que usa a atribuição automática de site ingressará no site atribuído de um grupo de limites que contém o local de rede atual do cliente.  

-   Depois de atribuir a um site, o cliente não altera a atribuição de site quando o local de rede é alterado. Por exemplo, se o cliente usa o perfil móvel em um novo local de rede que está representado por um limite em um grupo de limites com uma atribuição de site diferente, o site atribuído do cliente permanece inalterado.  

-   Quando a Descoberta de Sistemas do Active Directory encontra um novo recurso, as informações de rede para o recurso descoberto são avaliadas com os limites em grupos de limites. Esse processo associa o novo recurso a um site atribuído para uso do método de instalação do cliente por push.  

-   Quando um limite é um membro de vários grupos de limites que têm diferentes locais atribuídos, os clientes selecionarão aleatoriamente um desses sites.  

-   As alterações em um site atribuído de grupos de limites somente se aplicam a novas ações de atribuição de site. Os clientes atribuídos previamente a um site não reavaliam sua atribuição de site com base nas alterações da configuração de um grupo de limites (ou ao seu próprio local de rede).  

Para saber mais sobre a atribuição de site de cliente, veja [Usar atribuição automática de site para computadores](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) em [Como atribuir clientes a um site no System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="BKMK_BoundaryContentLocation"></a> Sobre o local do conteúdo  
 Você pode configurar cada grupo de limites com um ou mais pontos de distribuição e pontos de migração de estado e associar os mesmos pontos de distribuição e pontos de migração de estado a vários grupos de limites.  

-   **Durante a distribuição de software**, os clientes solicitam um local para o conteúdo de implantação. O Configuration Manager envia ao cliente uma lista de pontos de distribuição associados a cada grupo de limites que inclui o local de rede atual do cliente.  

-   **Durante a implantação de sistema operacional**, os clientes solicitam um local para enviar ou receber suas informações de migração de estado. O Configuration Manager envia ao cliente uma lista de pontos de migração de estado associados a cada grupo de limites que inclui o local de rede atual do cliente.  

Esse comportamento permite que o cliente selecione o servidor mais próximo do qual transferir o conteúdo ou as informações de migração de estado.  

###  <a name="BKMK_PreferredMP"></a> Sobre pontos de gerenciamento preferenciais  
 Os pontos de gerenciamento preferenciais permitem que um cliente identifique um ponto de gerenciamento associado ao local de rede (limite) atual.  

-   Um cliente tenta usar um ponto de gerenciamento preferencial de seu site atribuído antes de usar um ponto de gerenciamento de seu site atribuído que não está configurado como preferencial.  

-   Para usar esta opção, é necessário habilitá-la para a hierarquia e configurar grupos de limites em sites primários individuais para incluir os pontos de gerenciamento que devem ser associados aos limites associados desse grupo de limites  

-   Quando os pontos de gerenciamento preferenciais são configurados e um cliente organiza sua lista de pontos de gerenciamento, o cliente coloca os pontos de gerenciamento preferenciais na parte superior de sua lista de pontos de gerenciamento atribuídos, que inclui todos os pontos de gerenciamento do site atribuído do cliente.  

> [!NOTE]  
>  Quando um cliente realiza roaming (o que significa alterar seus locais de rede, como quando um laptop passa para um local de escritório remoto), ele pode usar um ponto de gerenciamento (ou ponto de gerenciamento de proxy) do site local em seu novo local antes de tentar usar um ponto de gerenciamento do seu site atribuído (que inclui os pontos de gerenciamento preferenciais).  Consulte [Entender como os clientes encontram serviços e recursos do site para o System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) para obter mais informações.  

###  <a name="BKMK_BoundaryOverlap"></a> Sobre a sobreposição de limites  
 O Configuration Manager dá suporte à sobreposição de configurações de limite para o local do conteúdo:  

-   **Quando um cliente solicita conteúdo** e o local de rede do cliente pertence a vários grupos de limites, o Configuration Manager envia ao cliente uma lista de todos os pontos de distribuição que têm o conteúdo.  

-   **Quando um cliente solicita a um servidor o envio ou recebimento de suas informações de migração de estado**, e o local de rede do cliente pertence a vários grupos de limites, o Configuration Manager envia ao cliente uma lista de todos os pontos de migração de estado associados a um grupo de limites que inclui o local de rede atual do cliente.  

Esse comportamento permite que o cliente selecione o servidor mais próximo do qual transferir o conteúdo ou as informações de migração de estado.  

###  <a name="BKMK_BoudnaryNetworkSpeed"></a> Sobre a velocidade de conexão de rede  
 Você pode definir a velocidade de conexão de rede para cada servidor do sistema de sites em um grupo de limites. Essa configuração aplica-se a clientes que se conectam a um sistema de sites com base nessa configuração de grupos de limites. O mesmo servidor do sistema de sites pode ter uma velocidade de conexão definida para ele em grupos de limites diferentes.  

 Por padrão, a velocidade de conexão de rede é definida como **Rápida**, mas você pode alterá-la para **Lenta**. A velocidade de conexão de rede e a configuração da implantação determinam se um cliente pode baixar conteúdo de um ponto de distribuição quando o cliente está em um grupo de limites associado.  

 Para saber mais sobre como a configuração de velocidade de conexão de rede afeta o modo como os clientes obtêm conteúdo, veja [Cenários de local de origem de conteúdo](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  
