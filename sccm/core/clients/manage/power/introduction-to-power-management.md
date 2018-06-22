---
title: Introdução ao gerenciamento de energia
titleSuffix: Configuration Manager
description: Veja a introdução ao gerenciamento de energia no System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3ddff2a7-99eb-4ef8-b969-f3f7f24053db
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: adf410b2cfdb45b3f01ac48c53d324b678689cda
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32334582"
---
# <a name="introduction-to-power-management-in-system-center-configuration-manager"></a>Introdução ao gerenciamento de energia no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O gerenciamento de energia no System Center Configuration Manager atende às necessidades que muitas organizações têm de monitorar e reduzir o consumo de energia de seus computadores. O recurso aproveita os recursos de gerenciamento de energia do Windows para aplicar configurações consistentes e relevantes aos computadores na organização. Você pode aplicar diferentes configurações de energia aos computadores durante os horários comercial e não comercial. Por exemplo, talvez você deseje aplicar um plano de energia mais restritivo aos computadores fora do horário comercial. Nos casos em que os computadores precisam permanecer ligados, você pode impedir que as configurações de gerenciamento de energia sejam aplicadas.  

 O gerenciamento de energia no Configuration Manager inclui vários relatórios que ajudam a analisar o consumo de energia e as configurações de energia de computadores em sua organização. Também é possível usar os relatórios para ajudá-lo a solucionar problemas com o gerenciamento de energia.  

 Um ver fluxo de trabalho detalhado sobre como configurar e usar o gerenciamento de energia, consulte [Lista de verificação do administrador do gerenciamento de energia no System Center Configuration Manager](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

> [!IMPORTANT]  
>  Não há suporte para o gerenciamento de energia do Configuration Manager em máquinas virtuais. Não é possível aplicar planos de energia a máquinas virtuais nem é possível relatar dados de energia deles.  

## <a name="the-power-management-workflow"></a>O fluxo de trabalho do gerenciamento de energia  
 Use estas três fases a seguir para planejar e implementar o gerenciamento de energia no Configuration Manager.  

### <a name="monitoring-and-planning-phase"></a>Fases de planejamento e de monitoramento  
 O gerenciamento de energia usa o inventário de hardware do Configuration Manager para coletar dados sobre as configurações de consumo e energia dos computadores no site. Há diversos relatórios que podem ser usados para analisar esses dados e determinar as configurações ideais de gerenciamento de energia para computadores. Por exemplo, durante as fases de planejamento e monitoramento do fluxo de trabalho do gerenciamento de energia, você pode criar coleções baseadas nos dados que estão incluídos no relatório **Recursos de energia** e usar esses dados para identificar os computadores incapazes de executar o gerenciamento de energia. Em seguida, é possível excluir esses computadores do gerenciamento de energia.  

> [!IMPORTANT]  
>  Não aplique planos de energia a computadores em seu site até coletar e analisar os dados de energia de computadores cliente. Se você aplicar novas configurações de gerenciamento de energia a computadores sem primeiro examinar as configurações existentes, você poderá perceber um aumento no consumo de energia.  

### <a name="enforcement-phase"></a>Fase de imposição  
 O gerenciamento de energia permite criar planos de energia que podem ser aplicados a coleções de computadores em seu site. Esses planos de energia definem as configurações de gerenciamento de energia do Windows em computadores. Você pode usar os planos de energia que acompanham o Configuration Manager ou configurar seus próprios planos de energia personalizados. Você pode usar os dados de energia coletados durante as fases de planejamento e monitoramento como uma linha de base para ajudá-lo a avaliar a economia de energia depois de aplicar um plano de energia aos computadores. Para mais informações, consulte [Lista de verificação do administrador do gerenciamento de energia no System Center Configuration Manager](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

### <a name="compliance-phase"></a>Fase de conformidade  
 Na fase de conformidade, você pode executar relatórios que podem ajudá-lo a avaliar o consumo de energia e a economia de energia em sua organização. Você também pode executar relatórios que descrevem os aperfeiçoamentos na quantidade de CO2 gerado por computadores. Relatórios também estão disponíveis, o que ajuda a validar se as configurações de energia foram aplicadas corretamente aos computadores e a resolver problemas com o recurso de gerenciamento de energia.  
