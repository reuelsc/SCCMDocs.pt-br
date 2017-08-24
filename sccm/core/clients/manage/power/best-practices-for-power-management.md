---
title: "Práticas recomendadas para o gerenciamento de energia | Microsoft Docs"
description: "Conheça as práticas recomendadas para o gerenciamento de energia no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d3cc24c7923141f039dcda26ac27489cb0143e89
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="best-practices-for-power-management-in-system-center-configuration-manager"></a>Práticas recomendadas para o gerenciamento de energia no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as práticas recomendadas para o gerenciamento de energia no System Center Configuration Manager.  

## <a name="perform-the-monitoring-phase-at-a-representative-time"></a>Execute a fase de monitoramento em um horário representativo  
 A fase de monitoramento do gerenciamento de energia fornece informações sobre o consumo de energia, atividade, recursos de gerenciamento de energia e impacto ambiental de computadores em sua organização. Certifique-se de escolher um horário representativo para executar a fase de monitoramento. Por exemplo, executar a fase de monitoramento em um feriado não fornece um relatório realista sobre o uso de energia do computador.  

## <a name="create-a-control-collection-of-computers-with-no-power-plans-applied"></a>Criar uma coleção de controle de computadores sem planos de energia aplicados  
 Crie duas coleções de computadores para ajudar a monitorar os efeitos da aplicação de planos de energia a computadores. A primeira coleção deve conter a maioria dos computadores aos quais você deseja aplicar as configurações de energia e a outra coleção (a coleção de controle) deve conter os computadores restantes. Aplique o plano de gerenciamento de energia necessário à coleção que contém a maioria dos computadores. Em seguida, você pode executar relatórios para comparar o custo de energia, consumo de energia e impacto ambiental dos computadores aos quais você aplicou as configurações de energia com a coleção de controle à qual não foram aplicadas configurações de energia.  

## <a name="run-the-power-settings-report-before-you-apply-a-power-management-plan"></a>Executar o relatório de Configurações de energia antes de aplicar um plano de gerenciamento de energia  
 Antes de aplicar um plano de gerenciamento de energia a uma coleção de computadores, execute o relatório **Configurações de Energia** para ajudá-lo a entender as configurações de gerenciamento de energia que já estão configuradas nos computadores da coleção. Se você aplicar novas configurações de gerenciamento de energia a computadores sem primeiro examinar as configurações existentes, isso poderá levar a um aumento no consumo de energia.  

## <a name="exclude-servers-from-power-management"></a>Excluir servidores do gerenciamento de energia  
 Não há suporte para o gerenciamento de energia para computadores que executam o Windows Server (embora os dados de consumo de energia sejam coletados). Certifique-se de adicionar servidores a uma coleção e excluí-la do gerenciamento de energia.  

## <a name="exclude-computers-that-you-do-not-want-to-manage"></a>Excluir computadores que você não deseja gerenciar  
 Se você tiver computadores que não deseja gerenciar com o gerenciamento de energia, adicione-os a uma coleção e certifique-se de que a coleção é excluída do gerenciamento de energia.  

 Exemplos de computadores que você pode desejar excluir do gerenciamento de energia:  

-   Computadores que precisam permanecer ligados.  

-   Computadores aos quais os usuários precisam se conectar usando a Conexão de Área de Trabalho Remota.  

-   Computadores que não podem usar o gerenciamento de energia.  

-   Computadores que têm a função de sistema de sites do ponto de distribuição.  

-   Computadores públicos, como computadores de quiosque, telas de informações ou consoles de monitoramento, em que o computador e o monitor devem estar sempre ligados.  

 Para mais informações, consulte [Configurar o gerenciamento de energia no System Center Configuration Manager](../../../../core/clients/manage/power/configuring-power-management.md).  

## <a name="first-apply-power-plans-to-a-test-collection-of-computers"></a>Primeiro aplique os planos de energia a uma coleção de teste de computadores  
 Sempre teste o efeito de aplicar um plano de gerenciamento de energia em uma coleção de teste de computadores antes de aplicar o plano de energia a uma coleção maior de computadores.  

 As configurações de energia aplicadas aos computadores com o Windows XP ou Windows Server 2003 não são revertidas para seus valores originais, mesmo que você exclua o computador do gerenciamento de energia. Em versões posteriores do Windows, a exclusão de um computador do gerenciamento de energia faz com que todas as configurações de energia sejam revertidas para seus valores originais. Não é possível reverter as configurações de energia individuais para seus valores originais.  

## <a name="apply-power-plan-settings-individually"></a>Aplicar configurações de plano de energia individualmente  
 Monitore o efeito da aplicação de cada configuração de energia antes de aplicar a próxima para garantir que cada configuração tenha o efeito necessário. Para obter mais informações sobre as configurações de plano de energia, consulte [Configurações de plano de gerenciamento de energia disponíveis](../../../../core/clients/manage/power/create-and-apply-power-plans.md#BKMK_Plans) no tópico [Como criar e aplicar planos de energia no System Center Configuration Manager](../../../../core/clients/manage/power/create-and-apply-power-plans.md).  

## <a name="regularly-monitor-computers-to-see-if-they-have-multiple-power-plans-applied"></a>Monitore os computadores regularmente para ver se eles têm vários planos de energia aplicados  
 O gerenciamento de energia inclui um relatório que exibe os computadores que têm mais de um plano de energia aplicado.  

 Se um computador for membro de várias coleções, e a cada um for aplicável um plano de energia diferente, as seguintes ações serão executadas:  

-   Plano de energia: se vários valores para as configurações de energia forem aplicados a um computador, o valor menos restritivo será usado.  

-   Hora de ativação: se várias horas de ativação forem aplicadas a um computador desktop, a hora mais próxima à meia-noite será usada.  

     Para mais informações, consulte [Computadores com vários planos de energia](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Multiple) no tópico [Como monitorar e planejar o gerenciamento de energia no System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md). Para obter mais informações sobre como o gerenciamento de energia resolve conflitos, consulte [Como criar e aplicar planos de energia no System Center Configuration Manager](../../../../core/clients/manage/power/create-and-apply-power-plans.md).  

## <a name="save-or-export-power-management-information-during-the-monitoring-and-planning-phase-of-power-management"></a>Salvar ou exportar informações de gerenciamento de energia durante as fases de planejamento e monitoramento do gerenciamento de energia  
 As informações de gerenciamento de energia usadas pelos relatórios diários são mantidas no banco de dados do site do Configuration Manager durante 31 dias.  

 As informações de gerenciamento de energia usadas pelos relatórios mensais são mantidas no banco de dados do site do Configuration Manager durante 13 meses.  

 Ao executar relatórios durante as fases de planejamento, monitoramento e conformidade do gerenciamento de energia, salve ou exporte os resultados dos relatórios cujos dados você deseja manter para fazer uma comparação posterior, caso eles sejam removidos mais tarde pelo Configuration Manager.  
