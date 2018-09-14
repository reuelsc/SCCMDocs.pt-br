---
title: Gerenciar coleções
titleSuffix: Configuration Manager
description: Realize tarefas de gerenciamento de coleções comuns no Configuration Manager.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d7c967ce02c009cd9659c7956f7ca79f4a34faf
ms.sourcegitcommit: be8c0182db9ef55a948269fcbad7c0f34fd871eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42755965"
---
# <a name="how-to-manage-collections-in-configuration-manager"></a>Como gerenciar coleções no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as informações de visão geral contidas neste artigo para ajudá-lo a executar tarefas de gerenciamento de coleções no Configuration Manager.  

> [!NOTE]  
>  Para saber mais sobre como criar coleções no Configuration Manager, consulte [Como criar coleções](/sccm/core/clients/manage/collections/create-collections).  



## <a name="bkmk_device"></a> Como gerenciar coleções de dispositivos  

 No espaço de trabalho **Ativos e Conformidade** , selecione **Coleções de Dispositivos**, selecione a coleção a ser gerenciada e uma tarefa de gerenciamento.  


#### <a name="show-members"></a>Mostrar Membros
 Exibe todos os recursos que são membros da coleção selecionada em um nó temporário do nó **Dispositivos** .


#### <a name="add-selected-items"></a>Adicionar itens selecionados
 Fornece as seguintes opções: 

 - **Adicionar Itens Selecionados à Coleção de Dispositivos Existente**: abre a caixa de diálogo **Selecionar Coleções**. Selecione a coleção à qual você deseja adicionar os membros da coleção selecionada. A coleção selecionada está incluída nesta coleção usando uma regra de associação **Incluir Coleções** .  

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
 Instrui todos os clientes na coleção de dispositivos selecionada a executar imediatamente uma das seguintes ações:

 - **Fazer download da política do computador**: atualizar a política de dispositivo. Para obter mais informações, confira [Iniciar recuperação de política para um cliente do Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  

 - **Fazer download da política do usuário**: atualizar a política de usuário.  

 - **Coletar dados de descoberta**: acionar os clientes para enviar um registro dos dados de descoberta (DDR). Para saber mais, confira [Descoberta de pulsação](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutHeartbeat).  

 - **Coletar inventário de software**: acionar os clientes para executar um ciclo de inventário de software. Para obter mais informações, consulte [Introdução ao inventário de software](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).  

 - **Coletar inventário de hardware**: acionar os clientes para executar um ciclo de inventário de hardware. Para obter mais informações, consulte [Introdução ao inventário de hardware](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).  

 - **Avaliar implantações de aplicativo**: acionar os clientes para executar um ciclo de avaliação de implantação de aplicativos. Para saber mais, confira [Reavaliação de agendamento para implantações](/sccm/core/clients/deploy/about-client-settings#schedule-re-evaluation-for-deployments).  

 - **Avaliar implantações de atualização de software**: acionar os clientes para executar um ciclo de avaliação de implantação de atualizações de software. Para saber mais, confira [Introdução às atualizações de software](/sccm/sum/understand/software-updates-introduction).  

 - **Alternar para o próximo Ponto de atualização de software**: acionar os clientes para alternar para o próximo ponto de atualização de software disponível. Para saber mais, confira [Mudança do ponto de atualização de software](/sccm/sum/plan-design/plan-for-software-updates#BKMK_SUPSwitching).  

 - **Avaliar o Atestado de Integridade do Dispositivo**: acionar os clientes do Windows 10 para verificar e enviar o estado de integridade do dispositivo mais recente. Para obter mais informações, consulte [Atestado de integridade](/sccm/core/servers/manage/health-attestation).  

 - **Verificar a conformidade de Acesso Condicional**: acionar os clientes para verificar sua conformidade com o acesso condicional. Para saber mais, confira [Gerenciar o acesso aos serviços do O365 para computadores](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm).  


#### <a name="endpoint-protection"></a>Endpoint Protection
 Instrui todos os clientes na coleção de dispositivos selecionada a executar imediatamente uma das seguintes ações:

 - **Verificação completa**: acione o Endpoint Protection ou o Windows Defender para executar uma verificação antimalware *completa*  

 - **Verificação rápida**: acione o Endpoint Protection ou o Windows Defender para executar uma verificação antimalware *rápida*  

 - **Fazer download da definição**: acione o Endpoint Protection ou o Windows Defender para baixar as definições antimalware mais recentes  


 Para obter mais informações, confira [Endpoint Protection no Configuration Manager](/sccm/protect/deploy-use/endpoint-protection).


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

 - **Sequência de tarefas**: abre o **Assistente de Implantação de Software**. Selecione e configure uma implantação de sequência de tarefas para a coleção selecionada. Para obter mais informações, consulte [Gerenciar sequências de tarefas para automatizar tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).  

 - **Atualizações de Software**: abre o **Assistente para Implantar Atualizações de Software**. Configure a implantação de atualizações de software para recursos na coleção selecionada. Para saber mais, confira [Gerenciar atualizações de software](/sccm/sum/understand/software-updates-introduction).  


#### <a name="clear-server-group-deployment-locks"></a>Limpar Bloqueios de Implantação de Grupo de Servidores
 Libere manualmente todos os bloqueios de implantação do grupo de servidores para a coleção. Para saber mais, confira [Manutenção de um grupo de servidores](/sccm/sum/deploy-use/service-a-server-group).


#### <a name="move"></a>Mover
 Mova a coleção selecionada para outra pasta no nó **Coleções de Dispositivos**. 


#### <a name="properties"></a>Propriedades
 Para saber mais, confira [Propriedades de coleções](#BKMK_CollProp).  



## <a name="bkmk_user"></a> Como gerenciar coleções de usuários  

 No espaço de trabalho **Ativos e Conformidade** , selecione **Coleções de Usuários**, selecione a coleção a ser gerenciada e uma tarefa de gerenciamento.  

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
