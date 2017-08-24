---
title: Tarefas de gerenciamento para aplicativos do System Center Configuration Manager | Microsoft Docs
description: "Gerenciar aplicativos e tipos de implantação do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c4041e21-21ff-4d95-ab05-14007e0047cf
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 72f99f0c90951f80de3d6e5ed8786d3fa482107e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="management-tasks-for-system-center-configuration-manager-applications"></a>Tarefas de gerenciamento para aplicativos do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as informações descritas neste tópico para ajudá-lo a gerenciar tipos de implantação e aplicativos do System Center Configuration Manager.  

Para obter ajuda na criação de aplicativos e tipos de implantação, consulte [Criar aplicativos](../../apps/deploy-use/create-applications.md).  

> [!IMPORTANT]  
>  Dependendo do tipo de aplicativo ou de implantação, algumas opções de gerenciamento poderão não estar disponíveis.  

##  <a name="manage-applications"></a>Gerenciar aplicativos  
 No espaço de trabalho **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** > **Aplicativos**, escolha o aplicativo a ser gerenciado e uma tarefa de gerenciamento.  

|Tarefa|Detalhes|  
|----------|-------------|  
|**Gerenciar Contas de Acesso**|Abre a caixa de diálogo **Gerenciar Contas de Acesso** , na qual você pode especificar o nível de acesso permitido para o conteúdo associado ao aplicativo selecionado.|  
|**Criar arquivo de conteúdo de pré-teste**|Abre o **Assistente para Criar Arquivo de Conteúdo de Pré-Teste** , que ajuda a gerenciar o conteúdo para pontos de distribuição remotos. Quando o agendamento e a limitação não fornecem uma solução válida para o ponto de distribuição remoto, é possível pré-configurar o conteúdo no ponto de distribuição<br /><br /> Consulte [Gerenciar conteúdo e infraestrutura de conteúdo](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Histórico de Revisão**|Abre a caixa de diálogo **Histórico de Revisão de Aplicativo**, que permite exibir as propriedades das revisões feitas nesse aplicativo, excluir as revisões antigas e restaurar as versões antigas do aplicativo.<br /><br /> Consulte [Como revisar e substituir aplicativos](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Criar Tipo de Implantação**|Abre o **Assistente para Criar Tipo de Implantação**, que permite adicionar um novo tipo de implantação ao aplicativo selecionado.<br /><br /> Consulte [Criar aplicativos](../../apps/deploy-use/create-applications.md).|  
|**Atualizar Estatísticas**|Atualiza as informações exibidas no nó **Implantações** do espaço de trabalho **Monitoramento** sobre as implantações desse aplicativo.<br /><br /> Consulte [Monitorar aplicativos no console do System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md).|  
|**Restabelecer**|Restabelece um aplicativo que foi desativado com a tarefa de gerenciamento **Desativar**.|  
|**Desativar**|Quando você desativa um aplicativo, ele não fica mais disponível para implantação, mas o aplicativo e suas implantações não são excluídos. As cópias existentes desse aplicativo que foram instaladas em computadores cliente não serão removidas. Quaisquer revisões para o aplicativo serão excluídas do Configuration Manager após 60 dias. No entanto, as cópias instaladas do aplicativo não são removidas.<br /><br /> Para excluir um aplicativo, é necessário desativá-lo primeiro, excluir todas implantações, remover as referências a ele por outras implantações e, em seguida, excluir todas as revisões dele.<br /><br /> Consulte [Revisar e substituir aplicativos](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Exportarar**|Abre o **Assistente para Exportar Aplicativo**, que permite exportar os aplicativos selecionados para um arquivo .zip que poderá ser arquivado ou instalado em outro site. Se você optar por exportar o conteúdo do aplicativo, será criada uma pasta que tem o conteúdo.<br /><br /> Também é possível exportar as dependências do aplicativo, as relações e condições de substituição, bem como o conteúdo do aplicativo e suas dependências.<br /><br /> O cmdlet **Export-CMApplication** do Windows PowerShell executa a mesma função. Para obter mais informações, consulte [Export-CMApplication](http://go.microsoft.com/fwlink/p/?LinkID=258880) na documentação de referência de cmdlet do Microsoft System Center 2012 Configuration Manager SP1.|  
|**Excluir**|Exclui o aplicativo selecionado atualmente.<br /><br /> Não será possível excluir um aplicativo se outros aplicativos dependerem dele, se ele tiver uma implantação ativa ou sequências de tarefas dependentes.|  
|**Simular Implantação**|Abre o **Assistente de Simulação de Implantação de Aplicativo** , no qual é possível testar os resultados de uma implantação de aplicativo em computadores sem instalar ou desinstalar o aplicativo.<br /><br /> Consulte [Simular implantações de aplicativos](../../apps/deploy-use/simulate-application-deployments.md).|  
|**Implantar**|Abre o **Assistente de Implantação de Software** , no qual é possível implantar o aplicativo selecionado em coleções de computadores em sua hierarquia.<br /><br /> Consulte [Implantar aplicativos](../../apps/deploy-use/deploy-applications.md).|  
|**Distribuir conteúdo**|Abre o **Assistente para Distribuir Conteúdo** , no qual é possível copiar o conteúdo do aplicativo selecionado para pontos de distribuição em sua hierarquia.<br /><br /> Consulte [Gerenciar conteúdo e infraestrutura de conteúdo](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Exibir Relações**|Mostra um diagrama gráfico das relações entre os aplicativos selecionados e outros aplicativos. Escolha um destes procedimentos:<br><br><ul><li>**Dependência** – mostra os aplicativos que dependem do aplicativo selecionado e os aplicativos dos quais o aplicativo selecionado depende.</li><li>**Substituição** – mostra os aplicativos que são substituídos pelo aplicativo selecionado e os aplicativos pelos quais o aplicativo selecionado é substituído.</li><li>**Condições Globais** – mostra as condições globais referenciadas por esse aplicativo.</li></ol><br /> Consulte [Revisar e substituir aplicativos](../../apps/deploy-use/revise-and-supersede-applications.md) e [Criar condições globais](../../apps/deploy-use/create-global-conditions.md).|  

##  <a name="manage-deployment-types"></a>Gerenciar tipos de implantação  
 No espaço de trabalho **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos**, escolha **Aplicativos** e o aplicativo que tem o tipo de implantação que você deseja gerenciar. No painel de detalhes, escolha a guia **Tipos de Implantação**, o tipo de implantação que você deseja gerenciar e uma tarefa de gerenciamento.  

|Tarefa|Detalhes|  
|----------|-------------|  
|**Aumentar Prioridade**|Aumenta a prioridade do tipo de implantação selecionado. Os tipos de implantação são avaliados na ordem. Quando um tipo de implantação atender aos requisitos especificados, ele será executado, e nenhum outro tipo de implantação na lista de prioridades será avaliado.|  
|**Diminuir Prioridade**|Diminui a prioridade do tipo de implantação selecionado.|  
|**Excluir**|Exclui o tipo de implantação selecionado.<br><br>Se um tipo de implantação for referenciado por um tipo de implantação em outro aplicativo, você não poderá excluí-lo.<br>Para excluir um tipo de implantação, é necessário remover todas as dependências do tipo de implantação que estão em outros tipos de implantação.<br>Além disso, também é necessário remover as revisões anteriores de todos os aplicativos que têm um tipo de implantação que faz referência ao tipo de implantação que você deseja excluir.|  
|**Atualizar Conteúdo**|Atualiza o conteúdo para o tipo de implantação selecionado.<br /><br /> Quando você inicia esse assistente para um tipo de implantação que tem um aplicativo virtual, o **Assistente para Atualizar Conteúdo** é iniciado. Esse assistente permite alterar as opções de publicação e as regras de requisitos para o aplicativo virtual selecionado. Para mais informações, consulte [Criar aplicativos](../../apps/deploy-use/create-applications.md).<br /><br /> Quando você atualiza o conteúdo de um tipo de implantação, é criada uma nova revisão do aplicativo. Isso pode fazer com que dispositivos cliente sejam atualizados com o novo aplicativo.|  
