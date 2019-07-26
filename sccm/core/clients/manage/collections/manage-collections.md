---
title: Gerenciar coleções
titleSuffix: Configuration Manager
description: Realize tarefas de gerenciamento de coleções comuns no Configuration Manager.
ms.date: 04/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f3099e61b28687ac2705d3da140af272d9de9fe2
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68339034"
---
# <a name="how-to-manage-collections-in-configuration-manager"></a>Como gerenciar coleções no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as informações de visão geral contidas neste artigo para ajudá-lo a executar tarefas de gerenciamento de coleções no Configuration Manager.  

> [!NOTE]  
>  Para saber mais sobre como criar coleções no Configuration Manager, consulte [Como criar coleções](/sccm/core/clients/manage/collections/create-collections).



## <a name="bkmk_device"></a> Como gerenciar coleções de dispositivos  

No workspace **Ativos e Conformidade**, selecione **Coleções de Dispositivos**, selecione a coleção a ser gerenciada e uma tarefa de gerenciamento.  


#### <a name="show-members"></a>Mostrar Membros
Exibe todos os recursos que são membros da coleção selecionada em um nó temporário do nó **Dispositivos** .


#### <a name="add-selected-items"></a>Adicionar itens selecionados
Fornece as seguintes opções: 

- **Adicionar Itens Selecionados à Coleção de Dispositivos Existente**: Abra a caixa de diálogo **Selecionar Coleção** . Selecione a coleção à qual você deseja adicionar os membros da coleção selecionada. A coleção selecionada está incluída nesta coleção usando uma regra de associação **Incluir Coleções** .  

- **Adicionar Itens Selecionados à Nova Coleção de Dispositivos**: abre o **Assistente para Criar Coleção de Dispositivos**, em que é possível criar uma nova coleção. A coleção selecionada está incluída nesta coleção usando uma regra de associação **Incluir Coleções** .  


Para obter mais informações, confira [Como criar coleções](/sccm/core/clients/manage/collections/create-collections).


#### <a name="install-client"></a>Instalar o cliente
Abre o **Assistente para Instalar Cliente**. Esse assistente usa a instalação no cliente por push para instalar um cliente do Configuration Manager em todos os computadores da coleção selecionada. Para saber mais, confira [Instalação no cliente por push](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).


#### <a name="run-script"></a>Executar Script
Abre o assistente **Executar Script** para executar um script do PowerShell em todos os clientes da coleção. Para saber mais, confira [Criar e executar scripts do PowerShell](/sccm/apps/deploy-use/create-deploy-scripts).


#### <a name="manage-affinity-requests"></a>Gerenciar solicitações de afinidade
Abre a caixa de diálogo **Gerenciar Solicitações de Afinidade de Dispositivo de Usuário**. Aprove ou rejeite solicitações pendentes para estabelecer as afinidades de dispositivo de usuário para os dispositivos na coleção selecionada. Para saber mais, confira [Vincular usuários e dispositivos com afinidade de dispositivo de usuário](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity)


#### <a name="clear-required-pxe-deployments"></a>Implantações PXE necessária Clear
Desmarca quaisquer implantações de inicialização PXE necessárias de todos os membros da coleção selecionada. Para obter mais informações, consulte [Usar PXE para implantar o Windows na rede](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).


#### <a name="update-membership"></a>Atualizar associação
Avalia a associação para a coleção selecionada. Para coleções com vários membros, essa atualização pode levar algum tempo para ser concluída. Use a ação **Atualizar** para atualizar a exibição com os novos membros de coleções depois que a atualização for concluída.


#### <a name="add-resources"></a>Adicionar recursos
Abre a caixa de diálogo **Adicionar Recursos à Coleção**. Procure novos recursos para adicionar à coleção selecionada. O ícone da coleção selecionada exibe um símbolo de ampulheta enquanto a atualização está em andamento.


#### <a name="client-notification"></a>Notificação de Cliente
Para obter mais informações, confira [Notificações do cliente](/sccm/core/clients/manage/client-notification).


#### <a name="endpoint-protection"></a>Endpoint Protection
Para obter mais informações, confira [Notificações do cliente](/sccm/core/clients/manage/client-notification).


#### <a name="export"></a>Exportar
Abre o **Assistente para exportação de coleção** que ajuda a exportar essa coleção para um arquivo de formato MOF (Managed Object). Esse arquivo pode, então, ser arquivado ou importado em outro site do Configuration Manager. Ao exportar uma coleção, as coleções referenciadas não são exportadas. As coleções são referenciadas pela coleção selecionada com o uso de uma regra **Incluir** ou **Excluir**.


#### <a name="copy"></a>Copiar
Cria uma cópia da coleção selecionada. A nova coleção usa a coleção selecionada como uma limitação de coleção.


#### <a name="refresh"></a>Atualizar
Atualize a exibição.


#### <a name="delete"></a>Excluir
Exclui a coleção selecionada. Você também pode excluir todos os recursos na coleção do banco de dados do site. 

Você não pode excluir as coleções que estão integradas ao Configuration Manager. Para obter uma lista das coleções internas, consulte [Introdução às coleções ](/sccm/core/clients/manage/collections/introduction-to-collections#built-in-collections).


#### <a name="simulate-deployment"></a>Simular Implantação
Abre o **Assistente de Simulação de Implantação de Aplicativo**. Esse assistente permite testar os resultados de uma implantação de aplicativo sem instalar ou desinstalar o aplicativo. Para saber mais, confira [Como simular implantações de aplicativos](/sccm/apps/deploy-use/simulate-application-deployments).


#### <a name="deploy"></a>Implantar
Exibe as seguintes opções:  

- **Aplicativo**: abre o **Assistente de Implantação de Software**. Selecione e configure uma implantação de aplicativo para a coleção selecionada. Para saber mais, confira [Como implantar aplicativos](/sccm/apps/deploy-use/deploy-applications).  

- **Programa**: abre o **Assistente de Implantação de Software**. Selecione e configure uma implantação de pacote e programa para a coleção selecionada. Para obter mais informações, consulte [Pacotes e programas](/sccm/apps/deploy-use/packages-and-programs).  

- **Linha de Base de Configuração**: abre a caixa de diálogo **Implantar Linhas de Base de Configuração**. Configure a implementação de uma ou mais linhas de base de configuração para a coleção selecionada. Para obter mais informações, veja [Como implantar linhas de base de configuração](/sccm/compliance/deploy-use/deploy-configuration-baselines).  

- **Sequência de Tarefas**: abre o **Assistente de Implantação de Software**. Selecione e configure uma implantação de sequência de tarefas para a coleção selecionada. Para obter mais informações, consulte [Gerenciar sequências de tarefas para automatizar tarefas](/sccm/osd/deploy-use/deploy-a-task-sequence).  

- **Atualizações de Software**: abre o **Assistente para Implantar Atualizações de Software**. Configure a implantação de atualizações de software para recursos na coleção selecionada. Para saber mais, confira [Gerenciar atualizações de software](/sccm/sum/understand/software-updates-introduction).  


#### <a name="clear-server-group-deployment-locks"></a>Limpar Bloqueios de Implantação de Grupo de Servidores
Libere manualmente todos os bloqueios de implantação do grupo de servidores para a coleção. Para saber mais, confira [Manutenção de um grupo de servidores](/sccm/sum/deploy-use/service-a-server-group).


#### <a name="move"></a>Mover
Mova a coleção selecionada para outra pasta no nó **Coleções de Dispositivos**. 


#### <a name="properties"></a>Propriedades
Para saber mais, confira [Propriedades de coleções](#BKMK_CollProp).  


## <a name="bkmk_user"></a> Como gerenciar coleções de usuários  

No workspace **Ativos e Conformidade**, selecione **Coleções de Usuários**, selecione a coleção a ser gerenciada e uma tarefa de gerenciamento.  

> [!Note]  
> As ações a seguir estão disponíveis nas coleções de usuários, mas os comportamentos são os mesmos das coleções de dispositivos. Exceto pelo que se aplica a coleções de usuários e aos usuários ali contidos. Para saber mais, confira a ação correspondente em [Como gerenciar coleções de dispositivos](#bkmk_device).  

- **Mostrar Membros**  
- **Adicionar itens selecionados**  
    - **Adicionar Itens Selecionados à Coleção de Usuários Existente**  
    - **Adicionar Itens Selecionados à Nova Coleção de Usuários**  
- **Gerenciar solicitações de afinidade**  
- **Atualizar associação**  
- **Adicionar recursos**  
- **Exportarar**  
- **Copiar**  
- **Atualizar**  
- **Excluir**  
- **Simular Implantação**  
- **Implantar**  
    - **Aplicativo**  
    - **Programa**  
    - **Linha de Base de Configuração**
- **Moverr**  
- **Propriedades**


##  <a name="BKMK_CollProp"></a> Propriedades de coleção  

Ao abrir a caixa de diálogo **Propriedades** de uma coleção, é possível exibir e configurar as seguintes opções:  

#### <a name="general"></a>Geral
Exiba e configure informações gerais sobre a coleção selecionada, incluindo o nome da coleção e a limitação da coleção.

#### <a name="membership-rules"></a>Regras de associação
Configure as regras de associação que definem os membros dessa coleção. Para obter mais informações, confira [Como criar coleções](/sccm/core/clients/manage/collections/create-collections).  

#### <a name="power-management"></a>Gerenciamento de energia
Configure os planos de gerenciamento de energia atribuídos aos computadores na coleção selecionada. Para mais informações, consulte [Introdução ao gerenciamento de energia](/sccm/core/clients/manage/power/introduction-to-power-management).  

#### <a name="deployments"></a>Implantações
Exibe qualquer software que você implantou nos membros da coleção selecionada.  

#### <a name="maintenance-windows"></a>Janelas de Manutenção
Exiba e configure as janelas de manutenção aplicadas aos membros da coleção selecionada. Para obter mais informações, consulte [Como usar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).

#### <a name="collection-variables"></a>Variáveis da coleção
Configure variáveis que se aplicam a esta coleção e podem ser usadas pelas sequências de tarefas. Para saber mais, confira [Como definir variáveis ​​de sequência de tarefas](/sccm/osd/understand/using-task-sequence-variables#bkmk_set).  

#### <a name="distribution-point-groups"></a>Grupos de pontos de distribuição
Associe um ou mais grupos de pontos de distribuição a membros da coleção selecionada. Para mais informações, confira [Manage content and content infrastructure](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure) (Gerenciar o conteúdo e a infraestrutura de conteúdo).

#### <a name="security"></a>Segurança
Exibe os usuários administrativos que têm permissões sobre a coleção selecionada das funções associadas e dos escopos de segurança. Para obter mais informações, consulte [Fundamentos da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).  

#### <a name="alerts"></a>Alertas 
Configure quando os alertas são gerados para o status do cliente e o Endpoint Protection. Para saber mais, confira [Como configurar o status do cliente](/sccm/core/clients/deploy/configure-client-status) e [Como monitorar a Endpoint Protection](/sccm/protect/deploy-use/monitor-endpoint-protection).  
## <a name="bkmk_powershell"></a> Uso do PowerShell

O PowerShell pode ser usado para gerenciar coleções.  Para obter mais informações, consulte:

* [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection)
* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Copy-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/copy-cmcollection)
* [Remove-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmcollection)
* [Export-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmcollection)
* [Get-CMCollectionMember](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionmember)
* [Get-CMCollectionSetting](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionsetting)
* [Invoke-CMCollectionUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/invoke-cmcollectionupdate)
* [Add-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule)
* [Set-CMCollectionPowerManagement](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollectionpowermanagement)
* [Get-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionmembershiprule)
* [Remove-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionmembershiprule)
* [Get-CMCollectionDirectMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectiondirectmembershiprule)
* [Get-CMCollectionQueryMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionquerymembershiprule)
* [Get-CMCollectionIncludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionincludemembershiprule)
* [Add-CMCollectionToAdministrativeUser](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectiontoadministrativeuser)
* [Remove-CMCollectionQueryMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionquerymembershiprule)
* [Remove-CMCollectionDirectMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectiondirectmembershiprule)
* [Get-CMCollectionExcludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionexcludemembershiprule)
* [Add-CMCollectionToDistributionPointGroup](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectiontodistributionpointgroup)
* [Remove-CMCollectionIncludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionincludemembershiprule)
* [Remove-CMCollectionExcludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionexcludemembershiprule)
* [Remove-CMCollectionFromAdministrativeUser](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionfromadministrativeuser)
