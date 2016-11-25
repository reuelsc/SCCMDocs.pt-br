---
title: Tarefas de gerenciamento de aplicativos do System Center Configuration Manager | System Center Configuration Manager
description: "Gerenciar aplicativos e tipos de implantação do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c4041e21-21ff-4d95-ab05-14007e0047cf
caps.latest.revision: 8
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b8ecf5334304f0aaae62b3fa5d6f84da84d97799


---
# <a name="management-tasks-for-system-center-configuration-manager-applications"></a>Tarefas de gerenciamento para aplicativos do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as informações neste tópico para ajudar a gerenciar aplicativos e tipos de implantação no System Center Configuration Manager.  
  
Para obter ajuda na criação de aplicativos e tipos de implantação, consulte [Criar aplicativos](../../apps/deploy-use/create-applications.md).  
  
> [!IMPORTANT]  
>  Dependendo do tipo de aplicativo e implantação, algumas opções de gerenciamento podem não estar disponíveis.  

##  <a name="manage-applications"></a>Gerenciar aplicativos  
 No espaço de trabalho **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** > **Aplicativos**, selecione o aplicativo a ser gerenciado e uma tarefa de gerenciamento.  
  
|Tarefa|Detalhes|  
|----------|-------------|  
|**Gerenciar Contas de Acesso**|Abre a caixa de diálogo **Gerenciar Contas de Acesso** , na qual você pode especificar o nível de acesso permitido para o conteúdo associado ao aplicativo selecionado.|  
|**Criar arquivo de conteúdo de pré-teste**|Abre o **Assistente para Criar Arquivo de Conteúdo de Pré-Teste** , que ajuda a gerenciar o conteúdo para pontos de distribuição remotos. Quando o agendamento e a limitação não fornecem uma solução válida para o ponto de distribuição remoto, é possível pré-configurar o conteúdo no ponto de distribuição<br /><br /> Consulte [Gerenciar conteúdo e infraestrutura de conteúdo](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Histórico de Revisão**|Abre a caixa de diálogo **Histórico de Revisão de Aplicativo** , que permite que você exiba as propriedades de revisões feitas nesse aplicativo, exclua as revisões de aplicativo antigas e restaure as versões antigas desse aplicativo.<br /><br /> Consulte [Como revisar e substituir aplicativos](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Criar Tipo de Implantação**|Abre o **Assistente para Criar Tipo de Implantação** , que permite a adição de um novo tipo de implantação ao aplicativo selecionado.<br /><br /> Consulte [Criar aplicativos](../../apps/deploy-use/create-applications.md).|  
|**Atualizar Estatísticas**|Atualiza as informações exibidas no nó **Implantações** do espaço de trabalho **Monitoramento** sobre as implantações desse aplicativo.<br /><br /> Consulte [Monitorar aplicativos no console do System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md).|  
|**Restabelecer**|Essa opção restabelece um aplicativo que foi desativado usando a tarefa de gerenciamento **Desativar** .|  
|**Desativar**|Quando você desativa um aplicativo, ele não fica mais disponível para implantações, mas o aplicativo e suas implantações não são excluídos. As cópias existentes desse aplicativo que foram instaladas em computadores cliente não serão removidas. Quaisquer revisões para o aplicativo serão excluídas do Configuration Manager após 60 dias. No entanto, quaisquer cópias instaladas do aplicativo não serão removidas.<br /><br /> Para excluir um aplicativo, primeiro desative-o, exclua quaisquer implantações, remova as referências a ele por outras implantações e então exclua todas as revisões dele.<br /><br /> Consulte [Revisar e substituir aplicativos](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Exportarar**|Abre o **Assistente para Exportar Aplicativo** , que permite que você exporte os aplicativos selecionados para um arquivo .zip que você pode então arquivar ou instalar em outro local. Se você optar por exportar o conteúdo do aplicativo, uma pasta será criada e irá guardar o conteúdo.<br /><br /> Também é possível exportar dependências do aplicativo, relações e condições de substituição, e conteúdo para o aplicativo e suas dependências.<br /><br /> O cmdlet do Windows PowerShell, **Export-CMApplication**, executa a mesma função. Para mais informações, consulte [http://go.microsoft.com/fwlink/p/?LinkID=258880](http://go.microsoft.com/fwlink/p/?LinkID=258880) na documentação de Referência de Cmdlet do Microsoft System Center 2012 Configuration Manager SP1.|  
|**Excluir**|Exclui o aplicativo selecionado atualmente.<br /><br /> Não será possível excluir um aplicativo se outros aplicativos dependerem dele, se ele tiver uma implantação ativa ou sequências de tarefas dependentes.|  
|**Simular Implantação**|Abre o **Assistente de Simulação de Implantação de Aplicativo** , no qual é possível testar os resultados de uma implantação de aplicativo em computadores sem instalar ou desinstalar o aplicativo.<br /><br /> Consulte [Simular implantações de aplicativos](../../apps/deploy-use/simulate-application-deployments.md).|  
|**Implantar**|Abre o **Assistente de Implantação de Software** , no qual é possível implantar o aplicativo selecionado em coleções de computadores em sua hierarquia.<br /><br /> Consulte [Implantar aplicativos](../../apps/deploy-use/deploy-applications.md).|  
|**Distribuir conteúdo**|Abre o **Assistente para Distribuir Conteúdo** , no qual é possível copiar o conteúdo do aplicativo selecionado para pontos de distribuição em sua hierarquia.<br /><br /> Consulte [Gerenciar conteúdo e infraestrutura de conteúdo](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Exibir Relações**|Exibe um diagrama gráfico mostrando as relações entre os aplicativos selecionados para outros aplicativos. Escolha um destes procedimentos:<br><br> - **Dependência** – Exibe os aplicativos dependentes e os aplicativos dos quais o aplicativo selecionado depende.<br>-                    **Substituição** – Exibe os aplicativos substituídos e aqueles pelos quais o item selecionado foi substituído.<br>- **Condições Globais** – Exibe as condições globais que são referenciadas por esse aplicativo.<br /><br /> Consulte [Revisar e substituir aplicativos](../../apps/deploy-use/revise-and-supersede-applications.md) e [Criar condições globais](../../apps/deploy-use/create-global-conditions.md).|  
  
##  <a name="manage-deployment-types"></a>Gerenciar tipos de implantação  
 No espaço de trabalho **Biblioteca de Software** , expanda **Gerenciamento de Aplicativos**, selecione **Aplicativos**, selecione o aplicativo que contém o tipo de implantação que você deseja gerenciar, no painel de detalhes, clique na guia **Tipos de Implantação** , selecione o tipo de implantação que se quer gerenciar e então selecione uma tarefa de gerenciamento.  
  
|Tarefa|Detalhes|  
|----------|-------------|  
|**Aumentar Prioridade**|Aumenta a prioridade do tipo de implantação selecionado. Os tipos de implantação são avaliados na ordem. Quando um tipo de implantação atende aos requisitos especificados, ele é executado, e nenhum outro tipo de implantação na lista de prioridades é avaliado.|  
|**Diminuir Prioridade**|Diminui a prioridade do tipo de implantação selecionado.|  
|**Excluir**|Exclui o tipo de implantação selecionado.<br><br>Se um tipo de implantação for referenciado por um tipo de implantação em outro aplicativo, você não poderá excluí-lo.<br>Para excluir um tipo de implantação, remova quaisquer dependências dele que estiverem contidas em outros tipos de implantação.<br>Além disso, remova também as revisões anteriores de qualquer aplicativo que contém um tipo de implantação que faz referência ao tipo de implantação que você deseja excluir.|  
|**Atualizar Conteúdo**|Atualiza o conteúdo para o tipo de implantação selecionado.<br /><br /> Quando você inicia esse assistente para um tipo de implantação que contém um aplicativo virtual, o **Assistente para Atualizar Conteúdo** é iniciado. Esse assistente permite que você modifique as opções de publicação e as regras de requisitos para o aplicativo virtual selecionado. Para mais informações, consulte [Criar aplicativos](../../apps/deploy-use/create-applications.md).<br /><br /> Quando você atualiza o conteúdo de um tipo de implantação, é criada uma nova revisão do aplicativo. Isso pode fazer com que dispositivos cliente sejam atualizados com o novo aplicativo.|  
  




<!--HONumber=Nov16_HO1-->


