---
title: "Gerenciar coleções"
titleSuffix: Configuration Manager
description: "Realize tarefas de gerenciamento de coleções comuns no System Center Configuration Manager."
ms.custom: na
ms.date: 4/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
caps.latest.revision: "8"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 0655a1dc566657cb27cdc7537603871dc36cc568
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-manage-collections-in-system-center-configuration-manager"></a>Como gerenciar coleções no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as informações de visão geral contidas neste tópico para ajudá-lo a executar tarefas de gerenciamento para coleções no System Center Configuration Manager.  

> [!NOTE]  
>  Para obter informações sobre como criar coleções do Configuration Manager, consulte [Como criar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).  

## <a name="how-to-manage-device-collections"></a>Como gerenciar coleções de dispositivos  
 No espaço de trabalho **Ativos e Conformidade** , selecione **Coleções de Dispositivos**, selecione a coleção a ser gerenciada e uma tarefa de gerenciamento.  

 Use a tabela a seguir para obter mais informações sobre as tarefas de gerenciamento que podem requerer informações adicionais antes de você selecioná-las.  

|Tarefa de gerenciamento|Detalhes|Mais informações|  
|---------------------|-------------|----------------------|  
|**Mostrar Membros**|Exibe todos os recursos que são membros da coleção selecionada em um nó temporário do nó **Dispositivos** .|Nenhuma informação adicional.|  
|**Adicionar itens selecionados**|Fornece as seguintes opções para executar uma das seguintes ações:<br /><br /> - <br />                    **Adicionar Itens Selecionados à Coleção de Dispositivos Existente** – Abre a caixa de diálogo **Selecionar Coleção**, em que é possível selecionar a coleção à qual você deseja adicionar os membros da coleção selecionada. A coleção selecionada está incluída nesta coleção usando uma regra de associação **Incluir Coleções** .<br /><br /> - **Adicionar Itens Selecionados à Nova Coleção de Dispositivos** – Abre o **Assistente para Criar Coleção de Dispositivos**, em que é possível criar uma nova coleção. A coleção selecionada está incluída nesta coleção usando uma regra de associação **Incluir Coleções** .|[Como criar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md)|  
|**Instalar o cliente**|Abre o **Assistente para Instalar Cliente**, que usa a instalação do cliente por push para instalar um cliente do Configuration Manager em todos os computadores da coleção selecionada.|[Como implantar clientes em computadores com Windows](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)|  
|**Gerenciar solicitações de afinidade**|Abre a caixa de diálogo **Gerenciar Solicitações de Afinidade de Dispositivo de Usuário** , em que você pode aprovar ou rejeitar solicitações pendentes para estabelecer as afinidades de dispositivo de usuário para os dispositivos na coleção selecionada.|[Vincular usuários e dispositivos com a afinidade de dispositivo de usuário no System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)|  
|**Desmarcar implantações PXE necessárias**|Desmarca quaisquer implantações de inicialização PXE necessárias de todos os membros da coleção selecionada.|[Introdução à implantação de sistema operacional](../../../../osd/understand/introduction-to-operating-system-deployment.md)|  
|**Atualizar associação**|Avalia a associação da coleção selecionada. Para coleções com vários membros, essa atualização pode levar algum tempo para ser concluída. Use a ação **Atualizar** para atualizar a exibição com os novos membros de coleções depois que a atualização for concluída.|Nenhuma informação adicional.|  
|**Adicionar recursos**|Abre a caixa de diálogo **Adicionar Recursos à Coleção** , em que você pode procurar novos recursos para adicionar à coleção selecionada.<br /><br /> O ícone da coleção selecionada exibe um símbolo de ampulheta enquanto a atualização está em andamento.|Nenhuma informação adicional.|  
|**Notificação de Cliente**|Instrui a todos os clientes na coleção de dispositivos selecionada para baixar a política de computador ou de usuário.|Nenhuma informação adicional.|  
|**Endpoint Protection**|Executa uma verificação completa ou rápida de antimalware ou baixa as definições de antimalware mais recentes para os computadores na coleção selecionada.|[Endpoint Protection no System Center Configuration Manager](../../../../protect/deploy-use/endpoint-protection.md)|  
|**Exportarar**|Abre o **Assistente para Exportar Coleção**, que ajuda a exportar esta coleção para um formato MOF (Managed Object Format) que pode ser arquivado ou usado mais tarde em outro site do Configuration Manager.<br /><br /> Ao exportar uma coleção, as coleções que são referenciadas pela coleção selecionada com o uso de uma regra **Incluir** ou **Excluir** não são exportadas.|Nenhuma informação adicional.|  
|**Copiar**|Cria uma cópia da coleção selecionada. A nova coleção usa a coleção selecionada como uma limitação de coleção.|Nenhuma informação adicional.|  
|**Excluir**|Exclui a coleção selecionada. Você também pode excluir todos os recursos na coleção do banco de dados do site.<br /><br /> Você não pode excluir as coleções que estão integradas ao Configuration Manager.|Para obter uma lista das coleções internas, consulte [Introdução às coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).|  
|**Simular Implantação**|Abre o **Assistente de Simulação de Implantação de Aplicativo** , que permite testar os resultados de uma implantação de aplicativo sem instalar ou desinstalar o aplicativo.|[Como simular implantações de aplicativos com o System Center Configuration Manager](../../../../apps/deploy-use/simulate-application-deployments.md)|  
|**Implantar**|Exibe as seguintes opções:<br /><br /> - <br />                    **Aplicativo** – Abre o **Assistente de Implantação de Software**, em que é possível selecionar e configurar uma implantação de aplicativo na coleção selecionada.<br /><br /> - <br />                    **Programa** – Abre o **Assistente de Implantação de Software** , em que é possível selecionar e configurar uma implantação de pacote e programa na coleção selecionada.<br /><br /> - **Linha de Base de Configuração** – Abre a caixa de diálogo **Implantar Linhas de Base de Configuração**, em que é possível configurar a implantação de uma ou mais linhas de base de configuração na coleção selecionada.<br /><br /> - <br />                    **Sequência de Tarefas** - Abre o **Assistente para Implantar Software** , em que você pode selecionar e configurar uma implantação da sequência de tarefas na coleção selecionada.<br /><br /> - <br />                    **Atualizações de software** – Abre o **Assistente para Implantar Atualizações de Software**, em que você pode configurar a implantação de atualizações de software nos recursos da coleção selecionada.|[Como implantar aplicativos com o System Center Configuration Manager](../../../../apps/deploy-use/deploy-applications.md)<br /><br /> [Pacotes e programas no System Center Configuration Manager](../../../../apps/deploy-use/packages-and-programs.md)<br /><br /> [Como implantar linhas de base de configuração no System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md)<br /><br /> [Gerenciar sequências de tarefas para automatizar tarefas no System Center Configuration Manager](../../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)<br /><br /> [Gerenciar atualizações de software no System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction)|  

## <a name="how-to-manage-user-collections"></a>Como gerenciar coleções de usuários  
 No espaço de trabalho **Ativos e Conformidade** , selecione **Coleções de Usuários**, selecione a coleção a ser gerenciada e uma tarefa de gerenciamento.  

 Use a tabela a seguir para obter mais informações sobre as tarefas de gerenciamento que podem requerer informações adicionais antes de você selecioná-las.  

|Tarefa de gerenciamento|Detalhes|Mais informações|  
|---------------------|-------------|----------------------|  
|**Mostrar Membros**|Exibe todos os recursos que são membros da coleção selecionada em um nó temporário do nó **Usuários** .|Nenhuma informação adicional.|  
|**Adicionar itens selecionados**|Essa opção permite que você execute uma das seguintes ações:<br /><br /> - <br />                    **Adicionar Itens Selecionados à Coleção de Usuários Existente** – Abre a caixa de diálogo **Selecionar Coleção**, em que é possível selecionar a coleção à qual você deseja adicionar os membros da coleção selecionada. A coleção selecionada está incluída nesta coleção usando uma regra de associação **Incluir Coleções** .<br /><br /> - **Adicionar Itens Selecionados à Nova Coleção de Usuários** – Abra o **Assistente para Criar Coleção de Usuários**, no qual é possível criar uma nova coleção. A coleção selecionada está incluída nesta coleção usando uma regra de associação **Incluir Coleções** .|[Como criar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md)|  
|**Gerenciar solicitações de afinidade**|Abre a caixa de diálogo **Gerenciar Solicitações de Afinidade de Dispositivo de Usuário** , em que você pode aprovar ou rejeitar solicitações pendentes para estabelecer as afinidades de dispositivo de usuário para os usuários na coleção selecionada.|[Vincular usuários e dispositivos com a afinidade de dispositivo de usuário no System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)|  
|**Atualizar associação**|Avalia a associação da coleção selecionada. Para coleções com vários membros, essa atualização pode levar algum tempo para ser concluída. Use a ação **Atualizar** para atualizar a exibição com os novos membros de coleções depois que a atualização for concluída.<br /><br /> O ícone da coleção selecionada exibe um símbolo de ampulheta enquanto a atualização está em andamento.|Nenhuma informação adicional.|  
|**Adicionar recursos**|Abre a caixa de diálogo **Adicionar Recursos à Coleção** , em que você pode procurar novos recursos para adicionar à coleção selecionada.|Nenhuma informação adicional.|  
|**Exportarar**|Abre o **Assistente para Exportar Coleção**, que ajuda a exportar esta coleção para um formato MOF (Managed Object Format) que pode ser arquivado ou usado mais tarde em outro site do Configuration Manager.<br /><br /> Ao exportar uma coleção, as coleções que são referenciadas pela coleção selecionada com o uso de uma regra **Incluir** ou **Excluir** não são exportadas.|Nenhuma informação adicional.|  
|**Copiar**|Cria uma cópia da coleção selecionada. A nova coleção usa a coleção selecionada como uma limitação de coleção.|Nenhuma informação adicional.|  
|**Excluir**|Exclui a coleção selecionada. Você também pode excluir todos os recursos na coleção do banco de dados do site.<br /><br /> Você não pode excluir as coleções que estão integradas ao Configuration Manager.|Para obter uma lista das coleções internas, consulte [Introdução às coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).|  
|**Simular Implantação**|Abre o **Assistente de Simulação de Implantação de Aplicativo** , que permite testar os resultados de uma implantação de aplicativo sem instalar ou desinstalar o aplicativo.|[Como simular implantações de aplicativos com o System Center Configuration Manager](../../../../apps/deploy-use/simulate-application-deployments.md)|  
|**Implantar**|Exibe as seguintes opções:<br /><br /> - **Aplicativo** – Abre o **Assistente de Implantação de Software**, em que é possível selecionar e configurar uma implantação de aplicativo na coleção selecionada.<br /><br /> - <br />                    **Programa** – Abre o **Assistente de Implantação de Software** , em que é possível selecionar e configurar uma implantação de pacote e programa na coleção selecionada.<br /><br /> - **Linha de Base de Configuração** – Abre a caixa de diálogo **Implantar Linhas de Base de Configuração**, em que é possível configurar a implantação de uma ou mais linhas de base de configuração na coleção selecionada.|[Como implantar aplicativos com o System Center Configuration Manager](../../../../apps/deploy-use/deploy-applications.md)<br /><br /> [Pacotes e programas no System Center Configuration Manager](../../../../apps/deploy-use/packages-and-programs.md)<br /><br /> [Como implantar linhas de base de configuração no System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md)|  

##  <a name="BKMK_CollProp"></a> Propriedades de coleção  
 Quando você abre a caixa de diálogo **Propriedades** de uma coleção, é possível exibir e configurar as propriedades a seguir de uma coleção.  

|Nome da guia|Mais informações|  
|--------------|----------------------|  
|**Geral**|Permite exibir e configurar informações gerais sobre a coleção selecionada, incluindo o nome da coleção e a limitação da coleção.|  
|**Regras de associação**|Permite configurar as regras de associação que definem a associação desta coleção. Para mais informações, consulte [Como criar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).|  
|**Gerenciamento de energia**|Permite configurar planos de gerenciamento de energia que são atribuídos aos computadores na coleção selecionada. Para mais informações, consulte [Introdução ao gerenciamento de energia](../../../../core/clients/manage/power/introduction-to-power-management.md).|  
|**Implantações**|Exibe qualquer software implantado nos membros da coleção selecionada.|  
|**Janelas de Manutenção**|Permite exibir e configurar as janelas de manutenção que são aplicadas aos membros da coleção selecionada. Para obter mais informações, consulte [Como usar as janelas de manutenção no System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).|  
|**Variáveis de coleção**|Permite configurar as variáveis que se aplicam a esta coleção e que podem ser usadas pelas sequências de tarefas. Para obter mais informações, consulte [Variáveis internas da sequência de tarefas](../../../../osd/understand/task-sequence-built-in-variables.md).|  
|**Grupos de pontos de distribuição**|Permite que você associe um ou mais grupos de pontos de distribuição aos membros da coleção selecionada. Para mais informações, consulte [Gerenciar conteúdo e infraestrutura de conteúdo do System Center Configuration Manager](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Segurança**|Exibe os usuários administrativos que têm permissões sobre a coleção selecionada das funções associadas e dos escopos de segurança.|  
|**Monitor**|Permite configurar quando os alertas são gerados para o status do cliente e o Endpoint Protection. Para mais informações, consulte [Como configurar o status do cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-status.md) e [Como monitorar o Endpoint Protection no System Center Configuration Manager](../../../../protect/deploy-use/monitor-endpoint-protection.md).|  
