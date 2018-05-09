---
title: Lista de verificação do administrador do gerenciamento de energia
titleSuffix: Configuration Manager
description: Use a lista de verificação do administrador para ajudar a planejar e implementar o gerenciamento de energia no System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 94e42cbe-9df8-4228-a04e-0ad7626180ca
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c556cb51ff071d40fcf5e4bb24c0b6b5f85c512a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="administrator-checklist-for-power-management-in-system-center-configuration-manager"></a>Lista de verificação do administrador do gerenciamento de energia no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Esta lista de verificação do administrador fornece as etapas recomendadas para usar o gerenciamento de energia do System Center Configuration Manager em sua organização.  

## <a name="configuring-power-management"></a>Configurando o gerenciamento de energia  
 Use estas etapas para ajudá-lo a configurar sua hierarquia para coletar informações de gerenciamento de energia dos computadores cliente.  

> [!IMPORTANT]  
>  Não aplique planos de energia a computadores em sua hierarquia até coletar e analisar os dados de energia de computadores cliente. Se você aplicar novas configurações de gerenciamento de energia a computadores sem primeiro examinar as configurações existentes, isso poderá levar a um aumento no consumo de energia.  

|Tarefa|Detalhes|  
|----------|-------------|  
|Reveja os conceitos de gerenciamento de energia na biblioteca de documentação do Configuration Manager.|Consulte [Introdução ao gerenciamento de energia](introduction-to-power-management.md).|  
|Reveja os pré-requisitos do gerenciamento de energia na biblioteca de documentação do Configuration Manager.|Consulte [Pré-requisitos do gerenciamento de energia](prerequisites-for-power-management.md).|  
|Reveja as informações de práticas recomendadas para o gerenciamento de energia.|Consulte [Práticas recomendadas para o gerenciamento de energia](best-practices-for-power-management.md).|  
|Configure suas coleções para gerenciar o consumo de energia de computadores no seu ambiente.|Use **Coleção para relatórios de dados de linha de base**, **Coleção para relatórios de dados de linha de base**, **Coleção de computadores incapazes de realizar gerenciamento de energia**, **Coleções de computadores aos quais os planos de energia serão aplicados**, **Coleções de computadores aos quais os planos de energia serão aplicados** e **Coleções de computadores que executam o Windows Server** para ajudar a gerenciar as configurações de energia de computadores na sua hierarquia. Você pode criar várias coleções e aplicar diferentes planos de energia a cada coleção.|  
|Habilite o gerenciamento de energia.|Antes de começar a usar o gerenciamento de energia, você deve habilitá-lo e definir as configurações do cliente necessárias. Para mais informações, consulte [Configurando o gerenciamento de energia](configuring-power-management.md).|  
|Colete informações de gerenciamento de energia de computadores cliente.|Os dados de gerenciamento de energia são relatados pelos clientes por meio do inventário de hardware do Configuration Manager. Dependendo do agendamento de inventário de hardware configurado, pode levar algum tempo para recuperar o inventário de todos os computadores cliente.|  

## <a name="monitoring-and-planning-phase"></a>Fases de planejamento e de monitoramento  

|Tarefa|Detalhes|  
|----------|-------------|  
|Execute o relatório **Atividade do computador**.|O relatório **Atividade do computador** exibe um gráfico que mostra a atividade do monitor, computador e usuário para uma coleção específica em um período de tempo especificado. Este relatório contém links para o relatório **Detalhes da atividade do computador** , que exibe os recursos de suspensão e ativação dos computadores na coleção especificada. Para mais informações, consulte [Como monitorar e planejar o gerenciamento de energia](monitor-and-plan-for-power-management.md).|  
|Execute o relatório **Consumo de energia** ou **Consumo de energia por dia**.|Os relatórios **Consumo de energia** e **Consumo de energia por dia** exibem o consumo de energia mensal total em kWh (quilowatts por hora) para uma coleção especificada em um período de tempo especificado. Para mais informações, consulte [Como monitorar e planejar o gerenciamento de energia](monitor-and-plan-for-power-management.md).|  
|Execute o relatório **Impacto ambiental** ou  **Impacto ambiental por dia**.|Os relatórios **Impacto ambiental** e **Impacto ambiental por dia** exibem um gráfico que mostra a economia em emissões de CO2 (dióxido de carbono) por uma coleção especificada de computadores em um período de tempo especificado. Para mais informações, consulte [Como monitorar e planejar o gerenciamento de energia](monitor-and-plan-for-power-management.md).|  
|Execute o relatório **Custo de energia** ou **Custo de energia por dia**.|Os relatórios **Custo de energia** e **Custo de energia por dia** exibem o custo do consumo total de energia para um período de tempo especificado. Para mais informações, consulte [Como monitorar e planejar o gerenciamento de energia](monitor-and-plan-for-power-management.md).|  
|Execute o relatório **Recursos de energia**.|O relatório **Recursos de energia** exibe os recursos de gerenciamento de energia de computadores na coleção especificada. Para mais informações, consulte [Como monitorar e planejar o gerenciamento de energia](monitor-and-plan-for-power-management.md).|  
|Execute o relatório **Configurações de energia**.|O relatório **Configurações de energia** exibe uma lista agregada das configurações atuais de energia usadas por computadores em uma coleção especificada. Para mais informações, consulte [Como monitorar e planejar o gerenciamento de energia](monitor-and-plan-for-power-management.md).|  
|Exclua todas as coleções de computadores necessárias do gerenciamento de energia.|Consulte [Configurando o gerenciamento de energia](configuring-power-management.md).|  

> [!IMPORTANT]  
>  Certifique-se de salvar as informações dos relatórios de gerenciamento de energia geradas durante as fases de planejamento e monitoramento. É possível comparar esses dados às informações de gerenciamento de energia geradas durante as fases de imposição e conformidade para ajudá-lo a avaliar o consumo de energia, o custo de energia e a redução do impacto ambiental ao aplicar um plano de energia aos computadores em sua hierarquia.  

## <a name="enforcement-phase"></a>Fase de imposição  

|Tarefa|Detalhes|  
|----------|-------------|  
|Selecione os planos de energia existentes ou crie novos planos de energia para as coleções de computadores em sua organização.|Consulte [Como criar e aplicar planos de energia](create-and-apply-power-plans.md).|  
|Aplique esses planos de energia aos computadores.|Consulte [Como criar e aplicar planos de energia](create-and-apply-power-plans.md).|  

## <a name="compliance-phase"></a>Fase de conformidade  

|Tarefa|Detalhes|  
|----------|-------------|  
|Execute o relatório **Atividade do computador**.|O relatório **Atividade do computador** exibe um gráfico que mostra a atividade do monitor, computador e usuário para uma coleção específica em um período de tempo especificado. Este relatório contém links para o relatório **Detalhes da atividade de energia do computador** , que exibe os recursos de suspensão e ativação dos computadores na coleção especificada. Para mais informações, consulte [Como monitorar e planejar o gerenciamento de energia](monitor-and-plan-for-power-management.md).|  
|Execute o relatório **Consumo de energia** ou **Consumo de energia por dia**.|Os relatórios **Consumo de energia** e **Consumo de energia por dia** exibem o consumo de energia mensal total em kWh (quilowatts por hora) para uma coleção especificada em um período de tempo especificado. Para mais informações, consulte [Como monitorar e planejar o gerenciamento de energia](monitor-and-plan-for-power-management.md).|  
|Execute o relatório **Impacto ambiental** ou **Impacto ambiental por dia**.|Os relatórios **Impacto ambiental** e **Impacto ambiental por dia** exibem um gráfico que mostra a economia em emissões de CO2 (dióxido de carbono) por uma coleção especificada de computadores em um período de tempo especificado. Para mais informações, consulte [Como monitorar e planejar o gerenciamento de energia](monitor-and-plan-for-power-management.md).|  
|Execute o relatório **Custo de energia** ou **Custo de energia por dia**.|Os relatórios **Custo de energia** e **Custo de energia por dia** exibem o custo do consumo total de energia para um período de tempo especificado. Para mais informações, consulte [Como monitorar e planejar o gerenciamento de energia](monitor-and-plan-for-power-management.md).|  

## <a name="troubleshooting"></a>Solução de problemas  

|Tarefa|Detalhes|  
|----------|-------------|  
|Se os computadores em sua hierarquia não tiverem entrado no modo de suspensão ou hibernação, execute o **Relatório de Insônia** para exibir as possíveis causas.|O **Relatório de Insônia** exibe uma lista das causas comuns que impediram os computadores de entrarem no modo de suspensão ou hibernação e o número de computadores que foram afetados por cada causa em um período de tempo especificado. Para mais informações, consulte [Como monitorar e planejar o gerenciamento de energia](monitor-and-plan-for-power-management.md).|  
|Se vários planos de energia forem aplicados a um computador, o plano de energia menos restritivo será aplicado. Execute o relatório **Computadores com vários planos de energia** para ver os computadores com vários planos de energia aplicados.|Consulte **Computadores com vários planos de energia** em [Como monitorar e planejar o gerenciamento de energia](monitor-and-plan-for-power-management.md).|  
