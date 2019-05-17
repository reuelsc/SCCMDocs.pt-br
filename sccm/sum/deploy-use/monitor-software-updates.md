---
title: Monitorar atualizações de software
titleSuffix: Configuration Manager
description: O console do System Center Configuration Manager fornece alertas e status para monitorar atualizações e a conformidade.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 9afd7b0f-5c8e-48bc-9a65-1f7d74103688
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5cd5c27aa04f25b044f74533983a214dc9f9341b
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500147"
---
# <a name="monitor-software-updates-in-system-center-configuration-manager"></a>Monitorar atualizações de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager fornece muitas maneiras de ajudar a monitorar objetos de atualizações de software, processos e informações de conformidade. Use as seções a seguir para monitorar atualizações de software.

## <a name="software-updates-dashboard"></a>Painel de atualizações de software
Começando do Configuration Manager versão 1610, é possível usar o Painel de Atualizações de Software para exibir o status atual de conformidade dos dispositivos em sua organização e analisar rapidamente os dados para ver quais dispositivos estão em risco. Para exibir o painel, navegue até **Monitoramento** > **Visão Geral** > **Segurança** > **Painel de Atualizações de Software**.   

##  <a name="BKMK_SUAlerts"></a> Alertas de atualizações de software  
 Você pode definir alertas para atualizações de software para notificar os usuários administrativos quando os níveis de conformidade para implantações de atualização de software estão abaixo da porcentagem configurada. Você pode configurar alertas para implantações de atualização de software nos seguintes locais:  

-   Configuração de ADR: é possível definir as configurações de alertas no Assistente de Regra de Implantação Automática e nas propriedades da ADR.  

-   Configuração de implantação: é possível definir as configurações de alertas no Assistente para Implantar Atualizações de Software e nas propriedades de implantação.  

Depois de definir as configurações de alerta, se ocorrerem as condições especificadas, o Configuration Manager gerará um alerta. Você pode revisar os alertas de atualização de software nos seguintes locais:  

1.  Reveja alertas recentes no nó **Atualizações de Software** no workspace **Biblioteca de Software**.  

2.  Gerencie os alertas configurados no nó **Alertas** no workspace **Monitoramento**.  

##  <a name="BKMK_SUSyncStatus"></a> Status da sincronização de atualizações de software  
 Após iniciar o processo de sincronização, você poderá monitorar o processo de sincronização do console do Configuration Manager para todos os pontos de atualização de software da hierarquia. Use o procedimento a seguir para monitorar o processo de sincronização de atualização de software.  

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Para monitorar o processo de sincronização de atualizações de software  

- No console do Configuration Manager, navegue até **Monitoramento** > **Visão Geral** > **Status de Sincronização do Ponto de Atualização de Software**.  

    Os pontos de atualização de software na sua hierarquia do Configuration Manager são exibidos no painel de resultados. Nessa exibição, você pode monitorar o status de sincronização de todos os pontos de atualização de software. Para obter informações mais detalhadas sobre o processo de sincronização, é possível ver o arquivo wsyncmgr.log, localizado em <*ConfigMgrInstallationPath*>\Logs em cada servidor do site.  

##  <a name="BKMK_SUDeployStatus"></a> Status de implantação de atualização de software  
 Depois de implantar as atualizações de software em um grupo de atualização de software ou implantar uma atualização de software individual, você poderá monitorar o status da implantação. Use o procedimento a seguir para monitorar o status da implantação de um grupo de atualização de software ou uma atualização de software.  

#### <a name="to-monitor-deployment-status"></a>Para monitorar o status da implantação  

1.  No console do Configuration Manager, navegue para **Monitoramento** > **Visão Geral** > **Implantações**.  

2.  Clique no grupo de atualização de software ou na atualização de software para a qual você deseja monitorar o status da implantação.  

3.  Na guia **Início** , no grupo **Implantação** , clique em **Exibir Status**.  

##  <a name="BKMK_SUReports"></a> Relatórios de atualizações de software  
 As mensagens de estado para atualizações de software fornecem informações sobre a conformidade de atualizações de software e sobre a avaliação e o estado de imposição das implantações de atualização de software. Você pode executar relatórios de atualização de software para exibir essas mensagens de estado. Há mais de 30 relatórios de atualização de software predefinidos disponíveis. Eles estão organizados em diversas categorias e podem ser usados para reportar informações específicas sobre atualizações de software e implantações. Além de usar relatórios pré-configurados, você também pode criar relatórios de atualização de software personalizados, de acordo com as necessidades de sua empresa. Para mais informações, consulte [Operações e manutenção de relatórios](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

### <a name="recommended-software-updates-reports"></a>Relatórios de atualizações de software recomendados
A seguir há alguns dos relatórios que são úteis para a identificação de possíveis problemas: 

#### <a name="compliance-9---overall-health-and-compliance-starting-in-version-1806"></a>Conformidade 9 – integridade e conformidade gerais (começando na versão 1806)
O relatório inclui as seguintes partes:

- **Clientes Íntegro vs Total de Clientes**: esse gráfico de barras compara os clientes "íntegros" que se comunicaram com o site no período de tempo especificado em relação ao número total de clientes na coleção especificada.
- **Visão Geral de Conformidade**: esse gráfico de pizza mostra o estado de conformidade geral do grupo de atualização de software específico em clientes ativos na coleção especificada.
- **Cinco principais atualizações sem conformidade por ID de artigo**: esse gráfico de barras exibe as cinco principais atualizações de software no grupo especificado que estão fora de conformidade em clientes ativos na coleção especificada.
- A parte inferior do relatório é uma tabela com mais detalhes, que lista as atualizações de software no grupo especificado.

#### <a name="management-2---updates-required-but-not-deployed"></a>gerenciamento 2 - Atualizações necessárias, mas não implantadas

Este relatório exibe as atualizações de software específicas do fornecedor em uma classificação de atualizações específicas que foram detectadas como obrigatórias nos clientes, mas que não foram implantadas em uma coleção específica. 

#### <a name="troubleshooting-2---deployment-errors"></a>Solução de problemas 2 – erros de implantação

Este relatório retorna os erros de implantação no site e uma contagem dos computadores que apresentaram cada erro. 


##  <a name="BKMK_MonitorContent"></a> Monitorar o conteúdo  
 Você pode monitorar o conteúdo no console do Configuration Manager para revisar o status de todos os tipos de pacotes em relação aos pontos de distribuição associados. Isso pode incluir o status de validação do conteúdo para o conteúdo no pacote, o status do conteúdo atribuído a um grupo de ponto de distribuição específico, o estado do conteúdo atribuído a um ponto de distribuição e o status de recursos opcionais para cada ponto de distribuição (validação de conteúdo, PXE e multicast).  

###  <a name="BKMK_ContentStatus"></a> Monitoramento de status do conteúdo  
 O nó **Status do Conteúdo** no workspace **Monitoramento** fornece informações sobre os pacotes de conteúdo. Você pode revisar informações gerais sobre o pacote, status de distribuição para o pacote e informações de status detalhadas sobre o pacote. Use o procedimento a seguir para exibir o status do conteúdo.  

#### <a name="to-monitor-content-status"></a>Para monitorar o status do conteúdo  

1.  No console do Configuration Manager, navegue para **Monitoramento** > **Visão Geral** > **Status de Distribuição** > **Status de Conteúdo**. Os pacotes são exibidos.  

2.  Selecione o pacote para exibir informações detalhadas de status.  

3.  Na guia **Início** , clique em **Exibir Status**. As informações detalhadas de status para o pacote são exibidas.  

###  <a name="BKMK_DPGroupStatus"></a> Status do grupo de pontos de distribuição  
 O nó **Status do Grupo de Pontos de Distribuição** no workspace **Monitoramento** fornece informações sobre grupos de pontos de distribuição. Você pode rever informações sobre o grupo de pontos de distribuição, como o status do grupo de pontos de distribuição e a taxa de conformidade, bem como informações detalhadas do status do grupo de pontos de distribuição. Use o procedimento a seguir para exibir o status do grupo de pontos de distribuição.  

#### <a name="to-monitor-distribution-point-group-status"></a>Para monitorar o status do grupo de pontos de distribuição  

1.  No console do Configuration Manager, navegue para **Monitoramento** > **Visão Geral** > **Status de Distribuição** > **Status do Grupo de Pontos de Distribuição**. Os grupos de pontos de distribuição são exibidos.  

2.  Selecione o grupo de pontos de distribuição para exibir informações detalhadas de status.  

3.  Na guia **Início** , clique em **Exibir Status**. As informações detalhadas de status para o grupo de pontos de distribuição são exibidas.  

###  <a name="BKMK_DPConfigStatus"></a> Status de configuração do ponto de distribuição  
 O nó **Status de Configuração de Pontos de Distribuição** no workspace **Monitoramento** fornece informações sobre o ponto de distribuição. Você pode rever quais atributos estão habilitados para o ponto de distribuição, como o PXE, Multicast e validação de conteúdo. É possível também exibir informações detalhadas para o ponto de distribuição. Use o procedimento a seguir para exibir o status de configuração de pontos de distribuição.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Para monitorar o status de configuração de pontos de distribuição  

1.  No console do Configuration Manager, navegue para **Monitoramento** > **Visão Geral** > **Status de Distribuição** > **Status da Configuração do Ponto de Distribuição**. Os pontos de distribuição são exibidos.  

2.  Selecione o ponto de distribuição para exibir informações de status do ponto de distribuição.  

3.  No painel de resultados, clique na guia **Detalhes** . As informações de status para o ponto de distribuição são exibidas.  
