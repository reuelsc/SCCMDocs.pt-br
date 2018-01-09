---
title: "Monitorar implantações de sistema operacional"
titleSuffix: Configuration Manager
description: "Para ajudar a monitorar objetos de implantação do sistema operacional, o console do Configuration Manager fornece alertas, relatórios e vários indicadores de status."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 08085d94-295c-432f-b5e3-9736bce0193b
caps.latest.revision: "6"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 2540bc214530318c7efa75020ea0ea59ca5f6b85
ms.sourcegitcommit: 08f9854fb6c6d21e1e923b13e38a64d0bc2bc9a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/12/2017
---
# <a name="monitor-operating-system-deployments-in-system-center-configuration-manager"></a>Monitorar implantações de sistema operacional no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O console do Configuration Manager fornece as seguintes maneiras para ajudar a monitorar objetos de implantação do sistema operacional.  


##  <a name="BKMK_OSDAlerts"></a> Alertas para implantações de sistema operacional  
 É possível configurar um alerta nas configurações de implantação da sequência de tarefas para notificar os usuários administrativos quando os níveis de conformidade da implantação estiverem abaixo do percentual configurado.  

 Depois de definir as configurações de alerta, se ocorrerem as condições especificadas, o Configuration Manager gerará um alerta. É possível examinar os alertas de implantação da sequência de tarefas nos seguintes locais:  

1.  Examine os alertas recentes no nó **Sistemas Operacionais** no espaço de trabalho **Biblioteca de Software** .  

2.  Gerencie os alertas configurados no nó **Alertas** no espaço de trabalho **Monitoramento** .  

##  <a name="BKMK_TSDeployStatus"></a> Status de implantação da sequência de tarefas  
 Depois de implantar uma sequência de tarefas, é possível monitorar o status da implantação. Use o procedimento a seguir para monitorar o status de implantação de uma sequência de tarefas.  

#### <a name="to-monitor-deployment-status"></a>Para monitorar o status da implantação  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho Monitoramento, clique em **Implantações**.  

3.  Clique na sequência de tarefas das quais você deseja monitorar o status da implantação.  

4.  Na guia **Início** , no grupo **Implantação** , clique em **Exibir Status**.  

##  <a name="BKMK_TSReports"></a> Relatórios de implantação de sistema operacional  
 Há vários relatórios de implantação de sistema operacional predefinidos disponíveis. Eles são organizados em diversas categorias e podem ser usados para relatar informações específicas sobre migração de estado e implantações da sequência de tarefas. Além de usar relatórios pré-configurados, você também pode criar relatórios de atualização de software personalizados, de acordo com as necessidades de sua empresa. Para mais informações, consulte [Operações e manutenção de relatórios](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

##  <a name="BKMK_MonitorContent"></a> Monitorar o conteúdo  
 Você pode monitorar o conteúdo no console do Configuration Manager para revisar o status de todos os tipos de pacotes em relação aos pontos de distribuição associados. Isso pode incluir o status de validação do conteúdo para o conteúdo no pacote, o status do conteúdo atribuído a um grupo de ponto de distribuição específico, o estado do conteúdo atribuído a um ponto de distribuição e o status de recursos opcionais para cada ponto de distribuição (validação de conteúdo, PXE e multicast).  

###  <a name="BKMK_ContentStatus"></a> Monitoramento de status do conteúdo  
 O nó **Status do Conteúdo** no espaço de trabalho **Monitoramento** fornece informações sobre os pacotes de conteúdo. Você pode revisar informações gerais sobre o pacote, status de distribuição para o pacote e informações de status detalhadas sobre o pacote. Use o procedimento a seguir para exibir o status do conteúdo.  

#### <a name="to-monitor-content-status"></a>Para monitorar o status do conteúdo  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho Monitoramento, expanda **Status de Distribuição**e clique em **Status do Conteúdo**. Os pacotes são exibidos.  

3.  Selecione o pacote para exibir informações detalhadas de status.  

4.  Na guia **Início** , clique em **Exibir Status**. As informações detalhadas de status para o pacote são exibidas.  

###  <a name="BKMK_DPGroupStatus"></a> Status do grupo de pontos de distribuição  
 O nó **Status do Grupo de Pontos de Distribuição** no espaço de trabalho **Monitoramento** fornece informações sobre grupos de pontos de distribuição. Você pode rever informações sobre o grupo de pontos de distribuição, como o status do grupo de pontos de distribuição e a taxa de conformidade, bem como informações detalhadas do status do grupo de pontos de distribuição. Use o procedimento a seguir para exibir o status do grupo de pontos de distribuição.  

#### <a name="to-monitor-distribution-point-group-status"></a>Para monitorar o status do grupo de pontos de distribuição  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho de monitoramento, expanda **Status da Distribuição**e clique em **Status do Grupo de Pontos de Distribuição**. Os grupos de pontos de distribuição são exibidos.  

3.  Selecione o grupo de pontos de distribuição para exibir informações detalhadas de status.  

4.  Na guia **Início** , clique em **Exibir Status**. As informações detalhadas de status para o grupo de pontos de distribuição são exibidas.  

###  <a name="BKMK_DPConfigStatus"></a> Status de configuração do ponto de distribuição  
 O nó **Status de Configuração de Pontos de Distribuição** no espaço de trabalho **Monitoramento** fornece informações sobre o ponto de distribuição. Você pode rever quais atributos estão habilitados para o ponto de distribuição, como o PXE, Multicast e validação de conteúdo. É possível também exibir informações detalhadas para o ponto de distribuição. Use o procedimento a seguir para exibir o status de configuração de pontos de distribuição.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Para monitorar o status de configuração de pontos de distribuição  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho de monitoramento, expanda **Status da Distribuição**e clique em **Status de Configuração do Ponto de Distribuição**. Os pontos de distribuição são exibidos.  

3.  Selecione o ponto de distribuição para exibir informações de status do ponto de distribuição.  

4.  No painel de resultados, clique na guia **Detalhes** . As informações de status para o ponto de distribuição são exibidas.  
