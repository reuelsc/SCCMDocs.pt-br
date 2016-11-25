---
title: Monitorar e planejar o gerenciamento de energia | System Center Configuration Manager
description: Saiba como monitorar e planejar o gerenciamento de energia no System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 507bf676-2679-4e4d-8831-3ffc9cf8557e
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 04ada4c90a5763a454c859eb7af9ac6ac84ceb3a


---
# <a name="how-to-monitor-and-plan-for-power-management-in-system-center-configuration-manager"></a>Como monitorar e planejar o gerenciamento de energia no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as informações a seguir para aprender a monitorar e planejar o gerenciamento de energia no System Center Configuration Manager.  

##  <a name="a-namebkmkhowtousereportsa-how-to-use-reports-for-power-management"></a><a name="BKMK_How_to_use_reports"></a> Como usar relatórios para o gerenciamento de energia  
 O gerenciamento de energia no Configuration Manager inclui vários relatórios que ajudam a analisar o consumo de energia e as configurações de energia de computadores em sua organização. Os relatórios também podem ser usados para ajudá-lo a resolver problemas.  

 Para poder usar os relatórios de gerenciamento de energia, você precisará configurar relatórios para sua hierarquia. Para obter mais informações sobre os relatórios do Configuration Manager, consulte [Relatórios no System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

> [!NOTE]  
>  As informações de gerenciamento de energia usadas pelos relatórios diários são mantidas no banco de dados do site do Configuration Manager durante 31 dias.  
>           As informações de gerenciamento de energia usadas pelos relatórios mensais são mantidas no banco de dados do site do Configuration Manager durante 13 meses.  
>   
>  Ao executar relatórios durante as fases de planejamento, monitoramento e conformidade do gerenciamento de energia, salve ou exporte os resultados dos relatórios cujos dados você deseja manter para fazer uma comparação posterior, caso eles sejam removidos mais tarde pelo Configuration Manager.  

## <a name="list-of-power-management-reports"></a>Lista de relatórios de gerenciamento de energia  
 A lista a seguir detalha os relatórios de gerenciamento de energia que estão disponíveis no Configuration Manager.  

> [!NOTE]  
>  Os relatórios de gerenciamento de energia exibem o número de computadores físicos e o número de computadores virtuais em uma coleção selecionada. No entanto, apenas as informações sobre gerenciamento de energia de computadores físicos são exibidas nos relatórios de gerenciamento de energia.  

###  <a name="a-namebkmkactivitya-computer-activity-report"></a><a name="BKMK_Activity"></a> Relatório Atividades do computador  
 O relatório **Atividade do computador** exibe um gráfico que mostra a seguinte atividade para uma coleção específica em um período de tempo especificado:  

-   **Computador ligado** – O computador foi ligado.  

-   **Monitor ligado** – O monitor foi ligado.  

-   **Usuário Ativo** – Foi detectada a atividade do mouse do computador, do teclado de computador ou de uma conexão de Área de Trabalho Remota ao computador  

 Esse relatório é usado durante as fases de planejamento e monitoramento e de imposição para ajudá-lo a entender o alinhamento entre a atividade do computador, a atividade do monitor e a atividade do usuário em um período de 24 horas. Se você executar o relatório durante vários dias, os dados serão agregados durante esse período. Este relatório pode ajudá-lo a determinar horários comerciais (de pico) e horários não comerciais (fora de pico) de uma coleção selecionada para ajudá-lo a decidir quando aplicar os planos de gerenciamento de energia configurados.  

 O gráfico mostra os períodos de tempo em que um computador pode ser ligado, mas que não há qualquer atividade de usuário. Considere a aplicação de configurações de energia mais restritivas durante esses horários para economizar nos custos de energia de computadores que estão ligados, mas que não estão sendo usados. Um computador é considerado ativo se houve atividade de monitor, usuário ou computador durante um minuto ou mais em relação a uma hora exibida no gráfico. Se um computador não estiver relatando dados de gerenciamento de energia, ele não será incluído no relatório **Atividade do computador** .  

 Use os parâmetros a seguir para configurar este relatório.  

#### <a name="required-report-parameters"></a>Parâmetros de relatório necessários  
 Para executar este relatório, os parâmetros a seguir devem ser especificados.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Data de Início**|Na lista suspensa, selecione a data de início para este relatório.|  
|**Data de término (opcional)**|Na lista suspensa, selecione uma data de término opcional para este relatório.|  
|**Nome da coleção**|Na lista suspensa, selecione uma coleção a ser usada para este relatório.|  
|**Tipo de dispositivo**|Na lista suspensa, selecione o tipo de computador para o qual deseja obter um relatório. Os valores válidos são **Todos** (computadores desktop e portáteis), **Desktop** (somente computadores desktop) e **Laptop** (somente computadores portáteis).|  

#### <a name="hidden-report-parameters"></a>Parâmetros de relatório ocultos  
 Este relatório não contém parâmetros ocultos que podem ser definidos.  

#### <a name="report-links"></a>Links de relatório  
 Se um valor para **Data de término (opcional)** não for especificado, este relatório conterá um link para o relatório a seguir, que fornece outras informações.  

|Nome do relatório|Detalhes|  
|-----------------|-------------|  
|**Detalhes da atividade do computador**|Clique no link **Clique para obter informações detalhadas** para ver uma lista de computadores ativos, inativos e que não forneceram relatórios na data especificada.<br /><br /> Para obter mais informações, consulte [Computer Activity Details Report](#BKMK_Activity_Details) neste tópico.|  

###  <a name="a-namebkmkcompactivitybycomputera-computer-activity-by-computer-report"></a><a name="BKMK_Comp_Activity_by_computer"></a> Atividades do computador por relatório de computador  
 O relatório **Atividade do computador por computador** exibe um gráfico que mostra a seguinte atividade de um computador especificado em determinada data:  

-   **Computador ligado** – O computador foi ligado.  

-   **Monitor ligado** – O monitor foi ligado.  

-   **Usuário Ativo** – Foi detectada a atividade do mouse do computador, do teclado de computador ou de uma conexão de Área de Trabalho Remota ao computador.  

 Este relatório pode ser executado de forma independente ou chamado pelo relatório **Detalhes da atividade do computador** .  

> [!NOTE]  
>  Informações sobre a atividade do computador são coletadas de computadores cliente durante o inventário de hardware. Dependendo do tempo em que é executado o inventário de hardware, a atividade que ocorre durante um horário de pico aplicado ou um plano de energia para horário fora de pico pode ser coletada.  

 Use os parâmetros a seguir para configurar este relatório.  

#### <a name="required-report-parameters"></a>Parâmetros de relatório necessários  
 Para executar este relatório, os parâmetros a seguir devem ser especificados.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Data do relatório**|Na lista suspensa, selecione uma data para este relatório.|  
|**Nome do computador**|Insira um nome do computador para o qual você deseja obter um relatório.|  

#### <a name="hidden-report-parameters"></a>Parâmetros de relatório ocultos  
 Este relatório não contém parâmetros ocultos que podem ser definidos.  

#### <a name="report-links"></a>Links de relatório  
 Este relatório contém links para o relatório a seguir, que fornece mais informações sobre o item selecionado.  

|Nome do relatório|Detalhes|  
|-----------------|-------------|  
|**Detalhes do Computador**|Clique no link **Clique para obter informações detalhadas** para ver os recursos de energia, as configurações de energia e os planos de energia aplicados para o computador selecionado.|  

###  <a name="a-namebkmkactivitydetailsa-computer-activity-details-report"></a><a name="BKMK_Activity_Details"></a> Computer Activity Details report  
 O relatório **Detalhes da atividade do computador** exibe uma lista de computadores ativos ou inativos com seus recursos de suspensão e ativação. Esse relatório é chamado pelo [Computer Activity Report](#BKMK_Activity) e não foi projetado para ser executado diretamente pelo administrador do site.  

 Use os parâmetros a seguir para configurar este relatório.  

#### <a name="required-report-parameters"></a>Parâmetros de relatório necessários  
 Para executar este relatório, os parâmetros a seguir devem ser especificados.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Nome da coleção**|Na lista suspensa, selecione uma coleção a ser usada para este relatório.|  
|**Data do relatório**|Na lista suspensa, selecione uma data a ser usada para este relatório.|  
|**Hora do relatório**|Na lista suspensa, selecione uma hora da data especificada na qual este relatório deve ser executado. Os valores válidos são entre **00h** e **23h**.|  
|**Estado do computador**|Na lista suspensa, selecione o estado do computador no qual este relatório deve ser executado. Os valores válidos são **Todos** (computadores que ativados ou desativados) **Ativado** (computadores ativados) e **Desativado** (computadores desativados, no modo de suspensão ou em hibernação). Esses valores são retornados apenas para o período de relatório selecionado.|  
|**Tipo de dispositivo**|Na lista suspensa, selecione o tipo de computador para o qual deseja obter um relatório. Os valores válidos são **Todos** (computadores desktop e portáteis), **Desktop** (somente computadores desktop) e **Laptop** (somente computadores portáteis). Esses valores são retornados apenas para o período de relatório selecionado.|  
|**Capacidade de suspensão**|Na lista suspensa, selecione se deseja exibir computadores com capacidade de suspensão no relatório. Os valores válidos são **Todos** (computadores com e sem capacidade de suspensão), **Não** (computadores sem capacidade de suspensão) e **Sim** (computadores com capacidade de suspensão).|  
|**Com capacidade de sair do modo de suspensão**|Na lista suspensa, selecione se deseja exibir computadores com capacidade de sair do modo de suspensão no relatório. Os valores válidos são **Todos** (computadores com e sem capacidade de retornar da suspensão), **Não** (computadores sem capacidade retornar da suspensão) e **Sim** (computadores com capacidade de retornar da suspensão).|  
|**Plano de energia**|Na lista suspensa, selecione os tipos de plano de energia que deseja exibir no relatório. Os valores válidos são **Todos** (computadores que não têm planos de gerenciamento de energia aplicados; computadores que têm um plano de gerenciamento de energia aplicado; computadores excluídos do gerenciamento de energia), **Não especificado** (computadores que não têm um plano de gerenciamento de energia aplicado), **Definido** (computadores que têm um plano de gerenciamento de energia aplicado) e **Excluído** (computadores que foram excluídos do gerenciamento de energia).|  
|**Sistema operacional**|Na lista suspensa, selecione os sistemas operacionais de computador que deseja exibir no relatório ou selecione **Todos** para exibir todos os sistemas operacionais.|  

#### <a name="hidden-report-parameters"></a>Parâmetros de relatório ocultos  
 Este relatório não contém parâmetros ocultos que podem ser definidos.  

#### <a name="report-links"></a>Links de relatório  
 Este relatório contém links para o relatório a seguir, que fornece mais informações sobre o item selecionado.  

|Nome do relatório|Detalhes|  
|-----------------|-------------|  
|**Atividade do computador por computador**|Clique no nome de um computador para ver a atividade específica do computador no período de relatório escolhido. Essas atividades incluem **Computador ativado** (o computador foi ativado?), **Monitor ativado** (o monitor foi ativado?) e **Usuário Ativo** (foi detectada atividade do mouse ou do teclado do computador ou uma conexão de área de trabalho remota).<br /><br /> Para obter mais informações, consulte [Computer Activity by Computer Report](#BKMK_Comp_Activity_by_computer) neste tópico.|  

###  <a name="a-namebkmkcomputerdetailsa-computer-details-report"></a><a name="BKMK_Computer_Details"></a> Relatório Detalhes do computador  
 O relatório **Detalhes do computador** exibe informações detalhadas sobre os recursos de energia, configurações de energia e planos de energia aplicados a um computador especificado. Esse relatório é chamado pelos relatórios **Atividade do computador por computador** , **Computadores com vários planos de energia** , **Recursos de energia** e **Detalhes de configurações de energia** . Ele não foi projetado para ser executado diretamente pelo administrador do site.  

#### <a name="required-report-parameters"></a>Parâmetros de relatório necessários  
 Para executar este relatório, os parâmetros a seguir devem ser especificados.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Nome do computador**|Insira um nome do computador para o qual você deseja obter um relatório.|  
|**Modo de energia**|Na lista suspensa, selecione o tipo de configurações de energia que deseja exibir nos resultados do relatório. Selecione **Conectado** para exibir as configurações de energia definidas para quando o computador está conectado e **Funcionando com bateria** para exibir as configurações de energia definidas para quando o computador está funcionando com bateria.|  

#### <a name="hidden-report-parameters"></a>Parâmetros de relatório ocultos  
 Este relatório não contém parâmetros ocultos que podem ser definidos.  

#### <a name="report-links"></a>Links de relatório  
 Este relatório não contém links para outros relatórios de gerenciamento de energia.  

###  <a name="a-namebkmknotreportinga-computer-not-reporting-details-report"></a><a name="BKMK_Not_Reporting"></a> Relatório Computadores que não relataram detalhes  
 O relatório **Computadores que não relataram detalhes** exibe uma lista de computadores em uma coleção especificada que não têm atividade de energia em uma data e hora especificadas. Esse relatório é chamado pelo **Computer Activity Report** e não foi projetado para ser executado diretamente pelo administrador do site.  

> [!NOTE]  
>  Os computadores relatam informações sobre gerenciamento de energia como parte do seu agendamento de inventário de hardware. Antes de considerar que um computador não está relatando, certifique-se de que ele relatou o inventário de hardware.  

 Use os parâmetros a seguir para configurar este relatório.  

#### <a name="required-report-parameters"></a>Parâmetros de relatório necessários  
 Para executar este relatório, os parâmetros a seguir devem ser especificados.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Nome da coleção**|Na lista suspensa, selecione uma coleção a ser usada para este relatório.|  
|**Data do relatório**|Na lista suspensa, selecione uma data para este relatório.|  
|**Hora do relatório**|Na lista suspensa, selecione uma hora da data especificada na qual este relatório deve ser executado. Os valores válidos são entre **00h** e **23h**.|  
|**Tipo de dispositivo**|Na lista suspensa, selecione o tipo de computador para o qual deseja obter um relatório. Os valores válidos são **Todos** (computadores desktop e portáteis), **Desktop** (somente computadores desktop) e **Laptop** (somente computadores portáteis). Esses valores são retornados apenas para o período de relatório selecionado.|  

#### <a name="hidden-report-parameters"></a>Parâmetros de relatório ocultos  
 Este relatório não contém parâmetros ocultos que podem ser definidos.  

#### <a name="report-links"></a>Links de relatório  
 Este relatório não contém links para outros relatórios de gerenciamento de energia.  

###  <a name="a-namebkmkexcludeda-computers-excluded"></a><a name="BKMK_Excluded"></a> Computadores excluídos  
 O relatório **Computadores excluídos** exibe uma lista de computadores em uma coleção especificada que foram excluídos do gerenciamento de energia do Configuration Manager.  

 Use os parâmetros a seguir para configurar este relatório.  

#### <a name="required-report-parameters"></a>Parâmetros de relatório necessários  
 Para executar este relatório, os parâmetros a seguir devem ser especificados.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Coleta**|Na lista suspensa, selecione uma coleção para este relatório.|  
|**Motivo**|Na lista suspensa, selecione o motivo pelo qual os computadores foram excluídos do gerenciamento de energia. Você pode exibir **Todos** (todos os computadores excluídos), **Excluído pelo administrador** (apenas computadores que foram excluídos por um usuário administrativo) e **Excluídos pelo usuário** (apenas computadores que foram excluídos por um usuário do Centro de Software).|  

#### <a name="hidden-report-parameters"></a>Parâmetros de relatório ocultos  
 Este relatório não contém parâmetros ocultos que podem ser definidos.  

#### <a name="report-links"></a>Links de relatório  
 Este relatório contém links para o relatório a seguir, que fornece mais informações sobre o item selecionado.  

|Nome do relatório|Detalhes|  
|-----------------|-------------|  
|**Detalhes de energia do computador**|Clique em um nome do computador para ver os recursos de energia, as configurações de energia e os planos de energia aplicados para o computador selecionado.<br /><br /> Para obter mais informações, consulte [Computer Details Report](#BKMK_Computer_Details) neste tópico.|  

###  <a name="a-namebkmkmultiplea-computers-with-multiple-power-plans"></a><a name="BKMK_Multiple"></a> Computadores com vários planos de energia  
 O relatório **Computadores com vários planos de energia** exibe uma lista de computadores que são membros de várias coleções, e a cada um é aplicável um plano de energia diferente. Para cada computador com configurações de energia potencialmente conflitantes, o relatório exibe o nome do computador e os planos de energia aplicados a cada coleção do qual o computador é membro.  

> [!IMPORTANT]  
>  Se um computador for membro de várias coleções, e cada coleção tiver planos de energia diferentes, o plano de energia menos restritivo será aplicado.  
>   
>  Se um computador for membro de várias coleções, e cada coleção tiver horários de ativação diferentes, o horário mais próximo à meia-noite será usado.  

 Use os parâmetros a seguir para configurar este relatório.  

#### <a name="required-report-parameters"></a>Parâmetros de relatório necessários  
 Para executar este relatório, os parâmetros a seguir devem ser especificados.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Nome da coleção**|Na lista suspensa, selecione uma coleção para este relatório.|  

#### <a name="hidden-report-parameters"></a>Parâmetros de relatório ocultos  
 Este relatório não contém parâmetros ocultos que podem ser definidos.  

#### <a name="report-links"></a>Links de relatório  
 Este relatório contém links para o relatório a seguir, que fornece mais informações sobre o item selecionado.  

|Nome do relatório|Detalhes|  
|-----------------|-------------|  
|**Detalhes de energia do computador**|Clique em um nome do computador para ver os recursos de energia, as configurações de energia e os planos de energia aplicados para o computador selecionado.<br /><br /> Para obter mais informações, consulte [Computer Details Report](#BKMK_Computer_Details) neste tópico.|  

###  <a name="a-namebkmkconsumptiona-energy-consumption-report"></a><a name="BKMK_Consumption"></a> Relatório Consumo de energia  
 O relatório **Consumo de energia** exibe as seguintes informações:  

-   Um gráfico que mostra o consumo de energia mensal total de computadores em kWh (quilowatts por hora) na coleção especificada, no período de tempo especificado.  

-   Um gráfico que mostra o consumo de energia médio em kWh (quilowatts por hora) de cada computador na coleção especificada, no período de tempo especificado.  

-   Uma tabela que mostra o consumo de energia mensal total em kWh (quilowatts por hora) e o consumo de energia médio de computadores na coleção especificada, no período de tempo especificado.  

 Essas informações podem ser usadas para ajudá-lo a entender as tendências de consumo de energia em seu ambiente. Depois de aplicar um plano de energia aos computadores na coleção selecionada, o consumo de energia dos computadores deverá diminuir.  

> [!NOTE]  
>  Se você adicionar ou remover membros da coleção depois de aplicar um plano de energia, isso afetará os resultados mostrados pelo relatório **Consumo de energia** e poderá dificultar a comparação dos resultados das fases de monitoramento e de planejamento e da fase de imposição.  

 Use os parâmetros a seguir para configurar este relatório.  

#### <a name="required-report-parameters"></a>Parâmetros de relatório necessários  
 Para executar este relatório, os parâmetros a seguir devem ser especificados.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Data de Início**|Na lista suspensa, selecione uma data de início para este relatório.|  
|**Data de término**|Na lista suspensa, selecione uma data de término para este relatório.|  
|**Nome da coleção**|Na lista suspensa, selecione uma coleção para este relatório.|  
|**Tipo de dispositivo**|Na lista suspensa, selecione o tipo de computador para o qual deseja obter um relatório. Os valores válidos são **Todos** (computadores desktop e portáteis), **Desktop** (somente computadores desktop) e **Laptop** (somente computadores portáteis). Esses valores são retornados apenas para o período de relatório selecionado.|  

#### <a name="hidden-report-parameters"></a>Parâmetros de relatório ocultos  
 Opcionalmente, os parâmetros ocultos a seguir podem ser especificados para alterar o comportamento deste relatório.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Computador desktop ligado**|Especifique o consumo de energia de um computador desktop quando ele está ligado. O valor padrão é **0,07** kW por hora.|  
|**Computador laptop ligado**|Especifique o consumo de energia de um computador portátil quando ele está ligado. O valor padrão é **0,02** kW por hora.|  
|**Computador desktop em suspensão**|Especifique o consumo de energia de um computador desktop que entrou em suspensão. O valor padrão é **0,003** kW por hora.|  
|**Computador laptop em suspensão**|Especifique o consumo de energia de um computador portátil que entrou em suspensão. O valor padrão é **0,001** kW por hora.|  
|**Computador desktop desligado**|Especifique o consumo de energia de um computador desktop quando ele está desligado. O valor padrão é **0** kW por hora.|  
|**Computador laptop desligado**|Especifique o consumo de energia de um computador portátil quando ele está desligado. O valor padrão é **0** kW por hora.|  
|**Monitor de desktop ligado**|Especifique o consumo de energia do monitor de um computador desktop quando ele está ligado. O valor padrão é **0,028** kW por hora.|  
|**Monitor de laptop ligado**|Especifique o consumo de energia do monitor de um computador portátil quando ele está ligado. O valor padrão é **0** kW por hora.|  

#### <a name="report-links"></a>Links de relatório  
 Este relatório não contém links para outros relatórios de gerenciamento de energia.  

###  <a name="a-namebkmkconsumptionbydaya-energy-consumption-by-day-report"></a><a name="BKMK_Consumption_by_Day"></a> Relatório Consumo de energia por dia  
 O relatório **Consumo de energia por dia** exibe as seguintes informações:  

-   Um gráfico que mostra o consumo de energia diário total de computadores em kWh (quilowatts por hora) na coleção especificada, nos últimos 31 dias.  

-   Um gráfico que mostra o consumo de energia diário médio em kWh (quilowatts por hora) de cada computador na coleção especificada, nos últimos 31 dias.  

-   Uma tabela que mostra o consumo de energia diário total em kWh (quilowatts por hora) e o consumo de energia diário médio de computadores na coleção especificada, nos últimos 31 dias.  

 Essas informações podem ser usadas para ajudá-lo a entender as tendências de consumo de energia em seu ambiente. Depois de aplicar um plano de energia aos computadores na coleção selecionada, o consumo de energia dos computadores deverá diminuir.  

> [!NOTE]  
>  Se você adicionar ou remover membros da coleção depois de aplicar um plano de energia, isso afetará os resultados mostrados pelo relatório **Consumo de energia** e poderá dificultar a comparação dos resultados das fases de monitoramento e de planejamento e da fase de imposição.  

 Use os parâmetros a seguir para configurar este relatório.  

#### <a name="required-report-parameters"></a>Parâmetros de relatório necessários  
 Para executar este relatório, os parâmetros a seguir devem ser especificados.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Coleta**|Na lista suspensa, selecione uma coleção para este relatório.|  
|**Device Type**|Na lista suspensa, selecione o tipo de computador para o qual deseja obter um relatório. Os valores válidos são **Todos** (computadores desktop e portáteis), **Desktop** (somente computadores desktop) e **Laptop** (somente computadores portáteis). Esses valores são retornados apenas para o período de relatório selecionado.|  

#### <a name="hidden-report-parameters"></a>Parâmetros de relatório ocultos  
 Opcionalmente, os parâmetros ocultos a seguir podem ser especificados para alterar o comportamento deste relatório.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Computador desktop ligado**|Especifique o consumo de energia de um computador desktop quando ele está ligado. O valor padrão é **0,07** kW por hora.|  
|**Computador laptop ligado**|Especifique o consumo de energia de um computador portátil quando ele está ligado. O valor padrão é **0,02** kW por hora.|  
|**Computador desktop em suspensão**|Especifique o consumo de energia de um computador desktop que entrou em suspensão. O valor padrão é **0,003** kW por hora.|  
|**Computador laptop em suspensão**|Especifique o consumo de energia de um computador portátil que entrou em suspensão. O valor padrão é **0,001** kW por hora.|  
|**Computador desktop desligado**|Especifique o consumo de energia de um computador desktop quando ele está desligado. O valor padrão é **0** kW por hora.|  
|**Computador laptop desligado**|Especifique o consumo de energia de um computador portátil quando ele está desligado. O valor padrão é **0** kW por hora.|  
|**Monitor de desktop ligado**|Especifique o consumo de energia do monitor de um computador desktop quando ele está ligado. O valor padrão é **0,028** kW por hora.|  
|**Monitor de laptop ligado**|Especifique o consumo de energia do monitor de um computador portátil quando ele está ligado. O valor padrão é **0** kW por hora.|  

#### <a name="report-links"></a>Links de relatório  
 Este relatório não contém links para outros relatórios de gerenciamento de energia.  

###  <a name="a-namebkmkcosta-energy-cost-report"></a><a name="BKMK_Cost"></a> Relatório Custo de energia  
 O relatório **Custo de energia** exibe as seguintes informações:  

-   Um gráfico que mostra o consumo de energia mensal total de computadores na coleção especificada, no período de tempo especificado.  

-   Um gráfico que mostra o custo de energia médio mensal para cada computador na coleção especificada, no período de tempo especificado.  

-   Uma tabela que mostra o custo de energia mensal total e o custo de energia mensal médio de computadores na coleção especificada, nos últimos 31 dias.  

 Essas informações podem ser usadas para ajudá-lo a entender as tendências de custo de energia em seu ambiente. Depois de aplicar um plano de energia aos computadores na coleção selecionada, o custo de energia dos computadores deverá diminuir.  

 Use os parâmetros a seguir para configurar este relatório.  

#### <a name="required-report-parameters"></a>Parâmetros de relatório necessários  
 Para executar este relatório, os parâmetros a seguir devem ser especificados.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Data de Início**|Na lista suspensa, selecione uma data de início para este relatório.|  
|**Data de término**|Na lista suspensa, selecione uma data de término para este relatório.|  
|**Custo de KwH**|Especifique o custo por kWh de eletricidade. O valor padrão é **0,09**.<br /><br /> Você pode modificar a unidade de moeda usada por este relatório na seção de parâmetros ocultos.|  
|**Nome da coleção**|Na lista suspensa, selecione uma coleção a ser usada para este relatório.|  
|**Tipo de dispositivo**|Na lista suspensa, selecione o tipo de computador para o qual deseja obter um relatório. Os valores válidos são **Todos** (computadores desktop e portáteis), **Desktop** (somente computadores desktop) e **Laptop** (somente computadores portáteis). Esses valores são retornados apenas para o período de relatório selecionado.|  

#### <a name="hidden-report-parameters"></a>Parâmetros de relatório ocultos  
 Opcionalmente, os parâmetros ocultos a seguir podem ser especificados para alterar o comportamento deste relatório.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Computador desktop ligado**|Especifique o consumo de energia de um computador desktop quando ele está ligado. O valor padrão é **0,07** kW por hora.|  
|**Computador laptop ligado**|Especifique o consumo de energia de um computador portátil quando ele está ligado. O valor padrão é **0,02** kW por hora.|  
|**Computador desktop em suspensão**|Especifique o consumo de energia de um computador desktop que entrou em suspensão. O valor padrão é **0,003** kW por hora.|  
|**Computador laptop em suspensão**|Especifique o consumo de energia de um computador portátil que entrou em suspensão. O valor padrão é **0,001** kW por hora.|  
|**Computador desktop desligado**|Especifique o consumo de energia de um computador desktop quando ele está desligado. O valor padrão é **0** kW por hora.|  
|**Computador laptop desligado**|Especifique o consumo de energia de um computador portátil quando ele está desligado. O valor padrão é **0** kW por hora.|  
|**Monitor de desktop ligado**|Especifique o consumo de energia do monitor de um computador desktop quando ele está ligado. O valor padrão é **0,028** kW por hora.|  
|**Monitor de laptop ligado**|Especifique o consumo de energia do monitor de um computador portátil quando ele está ligado. O valor padrão é **0** kW por hora.|  
|**Moeda**|Especifique o rótulo de moeda a ser usado para este relatório. O valor padrão é **USD (US$)**.|  

#### <a name="report-links"></a>Links de relatório  
 Este relatório não contém links para outros relatórios de gerenciamento de energia.  

###  <a name="a-namebkmkcostbydaya-energy-cost-by-day-report"></a><a name="BKMK_Cost_by_Day"></a> Relatório Custo de energia por dia  
 O relatório **Custo de energia por dia** exibe as seguintes informações:  

-   Um gráfico que mostra o custo de energia diário total para computadores na coleção especificada, nos últimos 31 dias.  

-   Um gráfico que mostra o custo de energia diário médio de cada computador na coleção especificada, nos últimos 31 dias.  

-   Uma tabela que mostra o custo de energia diário total e o custo de energia diário médio de computadores na coleção especificada, nos últimos 31 dias.  

 Essas informações podem ser usadas para ajudá-lo a entender as tendências de custo de energia em seu ambiente. Depois de aplicar um plano de energia aos computadores na coleção selecionada, o custo de energia dos computadores deverá diminuir.  

 Use os parâmetros a seguir para configurar este relatório.  

#### <a name="required-report-parameters"></a>Parâmetros de relatório necessários  
 Para executar este relatório, os parâmetros a seguir devem ser especificados.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Nome da coleção**|Na lista suspensa, selecione uma coleção a ser usada para este relatório.|  
|**Tipo de dispositivo**|Na lista suspensa, selecione o tipo de computador sobre o qual deseja fornecer um relatório. Os valores válidos são **Todos** (computadores desktop e portáteis), **Desktop** (somente computadores desktop) e **Laptop** (somente computadores portáteis). Esses valores são retornados apenas para o período de relatório selecionado.|  
|**Custo de KwH**|Especifique o custo por kWh de eletricidade. O valor padrão é **0,09**.<br /><br /> Você pode modificar a unidade de moeda usada por este relatório na seção de parâmetros ocultos.|  

#### <a name="hidden-report-parameters"></a>Parâmetros de relatório ocultos  
 Opcionalmente, os parâmetros ocultos a seguir podem ser especificados para alterar o comportamento deste relatório.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Computador desktop ligado**|Especifique o consumo de energia de um computador desktop quando ele está ligado. O valor padrão é **0,07** kW por hora.|  
|**Computador laptop ligado**|Especifique o consumo de energia de um computador portátil quando ele está ligado. O valor padrão é **0,02** kW por hora.|  
|**Computador desktop em suspensão**|Especifique o consumo de energia de um computador desktop que entrou em suspensão. O valor padrão é **0,003** kW por hora.|  
|**Computador laptop em suspensão**|Especifique o consumo de energia de um computador portátil que entrou em suspensão. O valor padrão é **0,001** kW por hora.|  
|**Computador desktop desligado**|Especifique o consumo de energia de um computador desktop quando ele está desligado. O valor padrão é **0** kW por hora.|  
|**Computador laptop desligado**|Especifique o consumo de energia de um computador portátil quando ele está desligado. O valor padrão é **0** kW por hora.|  
|**Monitor de desktop ligado**|Especifique o consumo de energia do monitor de um computador desktop quando ele está ligado. O valor padrão é **0,028** kW por hora.|  
|**Monitor de laptop ligado**|Especifique o consumo de energia do monitor de um computador portátil quando ele está ligado. O valor padrão é **0** kW por hora.|  
|**Moeda**|Especifique o rótulo de moeda a ser usado para este relatório. O valor padrão é **USD (US$)**.|  

#### <a name="report-links"></a>Links de relatório  
 Este relatório não contém links para outros relatórios de gerenciamento de energia.  

###  <a name="a-namebkmkenvironmentalimpacta-environmental-impact-report"></a><a name="BKMK_Environmental_Impact"></a> Relatório Impacto ambiental  
 O relatório **Impacto ambiental** exibe as seguintes informações:  

-   Um gráfico que mostra a quantidade total mensal de CO2 gerado (em toneladas) para cada computador na coleção especificada, no período especificado.  

-   Um gráfico que mostra a quantidade média mensal de CO2 gerado (em toneladas) para cada computador na coleção especificada, no período especificado.  

-   Uma tabela que mostra a quantidade total mensal de CO2 gerado e a quantidade média mensal de CO2 gerado dos computadores na coleção especificada, no período especificado.  

 O relatório **Impacto ambiental** calcula a quantidade de CO2 gerado (em toneladas) usando o tempo que um computador ou monitor permaneceu ligado em um período de 24 horas.  

 Use os parâmetros a seguir para configurar este relatório.  

#### <a name="required-report-parameters"></a>Parâmetros de relatório necessários  
 Para executar este relatório, os parâmetros a seguir devem ser especificados.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Data de início do relatório**|Na lista suspensa, selecione uma data de início para este relatório.|  
|**Data de término do relatório**|Na lista suspensa, selecione uma data de término para este relatório.|  
|**Nome da coleção**|Na lista suspensa, selecione uma coleção para este relatório.|  
|**Tipo de dispositivo**|Na lista suspensa, selecione o tipo de computador para o qual deseja obter um relatório. Os valores válidos são **Todos** (computadores desktop e portáteis), **Desktop** (somente computadores desktop) e **Laptop** (somente computadores portáteis). Esses valores são retornados apenas para o período de relatório selecionado.|  

#### <a name="hidden-report-parameters"></a>Parâmetros de relatório ocultos  
 Opcionalmente, os parâmetros ocultos a seguir podem ser especificados para alterar o comportamento deste relatório.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Computador desktop ligado**|Especifique o consumo de energia de um computador desktop quando ele está ligado. O valor padrão é **0,07** kW por hora.|  
|**Computador laptop ligado**|Especifique o consumo de energia de um computador portátil quando ele está ligado. O valor padrão é **0,02** kW por hora.|  
|**Computador desktop em suspensão**|Especifique o consumo de energia de um computador desktop que entrou em suspensão. O valor padrão é **0,003** kW por hora.|  
|**Computador laptop em suspensão**|Especifique o consumo de energia de um computador portátil que entrou em suspensão. O valor padrão é **0,001** kW por hora.|  
|**Computador desktop desligado**|Especifique o consumo de energia de um computador desktop quando ele está desligado. O valor padrão é **0** kW por hora.|  
|**Computador laptop desligado**|Especifique o consumo de energia de um computador portátil quando ele está desligado. O valor padrão é **0** kW por hora.|  
|**Monitor de desktop ligado**|Especifique o consumo de energia do monitor de um computador desktop quando ele está ligado. O valor padrão é **0,028** kW por hora.|  
|**Monitor de laptop ligado**|Especifique o consumo de energia do monitor de um computador portátil quando ele está ligado. O valor padrão é **0** kW por hora.|  
|**Fator de carbono (toneladas/kWh)** (CO2Mix)|Especifique o valor para o fator de carbono (em toneladas/kWh) que você geralmente pode obter de sua companhia elétrica. O valor padrão é **0,0015** toneladas por kWh.|  

#### <a name="report-links"></a>Links de relatório  
 Este relatório não contém links para outros relatórios de gerenciamento de energia.  

###  <a name="a-namebkmkenvironmentalimpactbydaya-environmental-impact-by-day-report"></a><a name="BKMK_Environmental_Impact_by_Day"></a> Relatório Impacto ambiental por dia  
 O relatório **Impacto ambiental por dia** exibe as seguintes informações:  

-   Um gráfico que mostra a quantidade diária total de CO2 gerado (em toneladas) para computadores na coleção especificada, nos últimos 31 dias.  

-   Um gráfico que mostra a quantidade diária média de CO2 gerado (em toneladas) para cada computador na coleção especificada, nos últimos 31 dias.  

-   Uma tabela que mostra a quantidade diária total de CO2 gerado e a quantidade diária média de CO2 gerado por computadores na coleção especificada, nos últimos 31 dias.  

 O relatório **Impacto ambiental por dia** calcula a quantidade de CO2 gerado (em toneladas) usando o tempo que um computador ou monitor permaneceu ligado em um período de 24 horas.  

#### <a name="required-report-parameters"></a>Parâmetros de relatório necessários  
 Para executar este relatório, os parâmetros a seguir devem ser especificados.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Nome da coleção**|Na lista suspensa, selecione uma coleção para este relatório.|  
|**Tipo de dispositivo**|Na lista suspensa, selecione o tipo de computador sobre o qual deseja fornecer um relatório. Os valores válidos são **Todos** (computadores desktop e portáteis), **Desktop** (somente computadores desktop) e **Laptop** (somente computadores portáteis). Esses valores são retornados apenas para o período de relatório selecionado.|  

#### <a name="hidden-report-parameters"></a>Parâmetros de relatório ocultos  
 Opcionalmente, os parâmetros ocultos a seguir podem ser especificados para alterar o comportamento deste relatório.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Computador desktop ligado**|Especifique o consumo de energia de um computador desktop quando ele está ligado. O valor padrão é **0,07** kWh.|  
|**Computador laptop ligado**|Especifique o consumo de energia de um computador portátil quando ele está ligado. O valor padrão é **0,02** kWh.|  
|**Computador desktop desligado**|Especifique o consumo de energia de um computador desktop quando ele está desligado. O valor padrão é **0** kWh.|  
|**Computador laptop desligado**|Especifique o consumo de energia de um computador portátil quando ele está desligado. O valor padrão é **0** kWh.|  
|**Computador desktop em suspensão**|Especifique o consumo de energia de um computador desktop que entrou em suspensão. O valor padrão é **0,003** kWh.|  
|**Computador laptop em suspensão**|Especifique o consumo de energia de um computador portátil que entrou no modo de suspensão. O valor padrão é **0,001** kWh.|  
|**Monitor de desktop ligado**|Especifique o consumo de energia do monitor de um computador desktop quando ele está ligado. O valor padrão é **0,028** kWh.|  
|**Monitor de laptop ligado**|Especifique o consumo de energia do monitor de um computador portátil quando ele está ligado. O valor padrão é **0** kWh.|  
|**Fator de carbono (toneladas/kWh)** (CO2Mix)|Especifique um valor para o fator de carbono (em toneladas/kWh) que você geralmente pode obter de sua companhia elétrica. O valor padrão é **0,0015** toneladas por kWh.|  

#### <a name="report-links"></a>Links de relatório  
 Este relatório não contém links para outros relatórios de gerenciamento de energia.  

###  <a name="a-namebkmkinsomniacomputerdetailsa-insomnia-computer-details-report"></a><a name="BKMK_Insomnia_Computer_Details"></a> Relatório Detalhes de computadores com insônia  
 O relatório **Detalhes de computadores com insônia** exibe uma lista de computadores que não entraram no modo de suspensão ou hibernação por um motivo específico em um período de tempo especificado. Esse relatório é chamado pelo **Relatório de Insônia** e não foi projetado para ser executado diretamente pelo administrador do site.  

 O **Relatório de Insônia** exibe computadores como **Sem capacidade de suspensão** quando eles não são capazes de entrar no modo de suspensão e foram ligados durante todo o intervalo do relatório especificado. O relatório exibe computadores como **Sem capacidade de hibernar** quando não são capazes de hibernar e foram ligados durante todo o intervalo do relatório especificado.  

> [!NOTE]  
>  O gerenciamento de energia pode coletar apenas causas que impediram que os computadores entrassem em suspensão ou hibernação de computadores que executam o Windows 7 ou Windows Server 2008 R2.  

 Use os parâmetros a seguir para configurar este relatório.  

#### <a name="required-report-parameters"></a>Parâmetros de relatório necessários  
 Para executar este relatório, os parâmetros a seguir devem ser especificados.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Nome da coleção**|Na lista suspensa, selecione uma coleção a ser usada para este relatório.|  
|**Intervalo do relatório (dias)**|Especifique o número de dias até o relatório. O valor padrão é **7** dias.|  
|**Causa de insônia**|Na lista suspensa, selecione uma das causas que podem impedir que os computadores entrem em suspensão ou hibernação.|  

#### <a name="hidden-report-parameters"></a>Parâmetros de relatório ocultos  
 Este relatório não contém parâmetros ocultos que podem ser definidos.  

#### <a name="report-links"></a>Links de relatório  
 Este relatório contém links para o relatório a seguir, que fornece mais informações sobre o item selecionado.  

|Nome do relatório|Detalhes|  
|-----------------|-------------|  
|**Detalhes do Computador**|Clique no link **Clique para obter informações detalhadas** para ver os recursos de energia, as configurações de energia e os planos de energia aplicados para o computador selecionado.<br /><br /> Para obter mais informações, consulte [Computer Details Report](#BKMK_Computer_Details) neste tópico.|  

###  <a name="a-namebkmkinsomniaa-insomnia-report"></a><a name="BKMK_Insomnia"></a> Insomnia report  
 O **Relatório de Insônia** exibe uma lista das causas comuns que impediram os computadores de entrarem no modo de suspensão ou hibernação e o número de computadores que foram afetados por cada causa em um período de tempo especificado. Há várias causas que podem impedir que um computador entre no modo de suspensão ou hibernação, como um processo em execução no computador, uma sessão aberta da Área de Trabalho Remota ou o fato de o computador não ter a capacidade de entrar no modo de suspensão ou hibernação. Nesse relatório, você pode abrir o relatório **Detalhes de computadores com insônia** , que exibe uma lista de computadores afetados por motivos individuais de computadores que não entraram em suspensão ou hibernação.  

 O relatório de Insônia de energia exibe computadores como **Sem capacidade de suspensão** quando eles não são capazes de entrar no modo de suspensão e foram ligados durante todo o intervalo do relatório especificado. O relatório exibe computadores como **Sem capacidade de hibernar** quando não são capazes de hibernar e foram ligados durante todo o intervalo do relatório especificado.  

> [!NOTE]  
>  O gerenciamento de energia pode coletar apenas causas que impediram que os computadores entrassem em suspensão ou hibernação de computadores que executam o Windows 7 ou Windows Server 2008 R2.  

 Use os parâmetros a seguir para configurar este relatório.  

#### <a name="required-report-parameters"></a>Parâmetros de relatório necessários  
 Para executar este relatório, os parâmetros a seguir devem ser especificados.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Nome da coleção**|Na lista suspensa, selecione uma coleção a ser usada para este relatório.|  
|**Intervalo do relatório (dias)**|Especifique o número de dias até o relatório. O valor padrão é **7** dias. O valor máximo é de **365** dias. Especifique **0** para executar o relatório de hoje.|  

#### <a name="hidden-report-parameters"></a>Parâmetros de relatório ocultos  
 Este relatório não contém parâmetros ocultos que podem ser definidos.  

#### <a name="report-links"></a>Links de relatório  
 Este relatório contém links para o relatório a seguir, que fornece mais informações sobre o item selecionado.  

|Nome do relatório|Detalhes|  
|-----------------|-------------|  
|**Detalhes de computadores com insônia**|Clique em um número na coluna **Computadores Afetados** para ver uma lista de computadores que não conseguiram ser suspensos ou hibernados devido à causa selecionada.<br /><br /> Para obter mais informações, consulte [Insomnia Computer Details Report](#BKMK_Insomnia_Computer_Details) neste tópico.|  

###  <a name="a-namebkmkcapabilitesa-power-capabilities-report"></a><a name="BKMK_Capabilites"></a> Relatório Recursos de energia  
 O relatório **Recursos de energia** exibe os recursos de gerenciamento de hardware de computadores na coleção especificada. Normalmente, esse relatório é usado na fase de monitoramento do gerenciamento de energia para determinar os recursos de gerenciamento de energia dos computadores em sua organização. As informações exibidas no relatório podem ser usadas para criar coleções de computadores aos quais os planos de energia serão aplicados, ou para excluir do gerenciamento de energia. Os recursos de gerenciamento de energia exibidos por este relatório são:  

-   **Com capacidade de suspensão** – Indica se o computador pode entrar no modo de suspensão se estiver configurado para fazer isso.  

-   **Com capacidade de hibernação** – Indica se o computador pode entrar no modo de hibernação se estiver configurado para fazer isso.  

-   **Sair do modo de suspensão** – Indica se o computador pode sair do modo de suspensão se estiver configurado para fazer isso.  

-   **Sair do modo de hibernação** – Indica se o computador pode sair do modo de hibernação se estiver configurado para fazer isso.  

 Os valores relatados pelo relatório **Recursos de energia** indicam os recursos de suspensão e hibernação de computadores, conforme relatado pelo Windows. No entanto, os valores relatados não refletem os casos em que as configurações do Windows ou do BIOS impedem essas funções de funcionar.  

 Use os parâmetros a seguir para configurar este relatório.  

#### <a name="required-report-parameters"></a>Parâmetros de relatório necessários  
 Para executar este relatório, os parâmetros a seguir devem ser especificados.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Coleta**|Na lista suspensa, selecione uma coleção para este relatório.|  
|**Exibir filtro**|Na lista suspensa, selecione **Sem suporte** para exibir apenas os computadores na coleção especificada que não são capazes de suspensão, hibernação, retornar da suspensão ou retornar da hibernação. Selecione **Mostrar Tudo** para exibir todos os computadores na coleção especificada.|  

#### <a name="hidden-report-parameters"></a>Parâmetros de relatório ocultos  
 Este relatório não contém parâmetros ocultos que podem ser definidos.  

#### <a name="report-links"></a>Links de relatório  
 Este relatório contém links para o relatório a seguir, que fornece mais informações sobre o item selecionado.  

|Nome do relatório|Detalhes|  
|-----------------|-------------|  
|**Detalhes do Computador**|Clique em um nome do computador para ver os recursos de energia, as configurações de energia e os planos de energia aplicados para o computador selecionado.<br /><br /> Para obter mais informações, consulte [Computer Details Report](#BKMK_Computer_Details) neste tópico.|  

###  <a name="a-namebkmksettingsa-power-settings-report"></a><a name="BKMK_Settings"></a> Relatório Configurações de energia  
 O relatório **Configurações de energia** exibe uma lista agregada de configurações de energia usadas por computadores na coleção especificada. Para cada configuração de energia, os possíveis modos de energia, valores e unidades são exibidos com uma contagem do número de computadores que usam esses valores. Este relatório pode ser usado durante a fase de monitoramento do gerenciamento de energia para ajudar o administrador a entender as configurações de energia existentes usadas pelos computadores no site e para ajudar a planejar a aplicação de configurações de energia ideais usando um plano de gerenciamento de energia. O relatório também é útil ao resolver problemas para validar que as configurações de energia foram aplicadas corretamente.  

> [!NOTE]  
>  As configurações exibidas são coletadas de computadores cliente durante o inventário de hardware. Dependendo do tempo em que é executado o inventário de hardware, as configurações do horário de pico aplicado ou dos planos de energia para horário fora de pico podem ser coletadas.  

 Use os parâmetros a seguir para configurar este relatório.  

#### <a name="required-report-parameters"></a>Parâmetros de relatório necessários  
 Para executar este relatório, os parâmetros a seguir devem ser especificados.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Nome da coleção**|Na lista suspensa, selecione uma coleção para este relatório.|  

#### <a name="hidden-report-parameters"></a>Parâmetros de relatório ocultos  
 Opcionalmente, os parâmetros ocultos a seguir podem ser especificados para alterar o comportamento deste relatório.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**numberOfLocalizations**|Especifique o número de idiomas nos quais você deseja exibir os nomes de configuração de energia relatados pelos computadores cliente. Se quiser exibir a linguagem mais popular, deixe essa configuração no padrão de **1**. Para exibir todas as linguagens, defina esse valor como **0**.|  

#### <a name="report-links"></a>Links de relatório  
 Este relatório contém links para o relatório a seguir, que fornece mais informações sobre o item selecionado.  

|Nome do relatório|Detalhes|  
|-----------------|-------------|  
|**Detalhes de configurações de energia**|Clique no número de computadores na coluna **Computadores** para ver uma lista de todos os computadores que usam as configurações de energia nessa linha.<br /><br /> Para obter mais informações, consulte [Power Settings Details Report](#BKMK_Settings_Details) neste tópico.|  

###  <a name="a-namebkmksettingsdetailsa-power-settings-details-report"></a><a name="BKMK_Settings_Details"></a> Power Settings Details report  
 O relatório **Detalhes de configurações de energia** exibe mais informações sobre os computadores selecionados no relatório **Configurações de energia** . Esse relatório é chamado pelo relatório **Configurações de energia** e não foi projetado para ser executado diretamente pelo administrador do site.  

#### <a name="required-report-parameters"></a>Parâmetros de relatório necessários  
 Para executar este relatório, os parâmetros a seguir devem ser especificados.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**Coleta**|Na lista suspensa, selecione uma coleção a ser usada para este relatório.|  
|**GUID de configuração de energia**|Na lista suspensa, selecione o GUID da configuração de energia no qual você deseja relatar. Para obter uma lista de todas as configurações de energia e seus usos, consulte [Configurações de plano de gerenciamento de energia disponíveis](../../../../core/clients/manage/power/create-and-apply-power-plans.md#BKMK_Plans) no tópico [Como criar e aplicar planos de energia no System Center Configuration Manager](../../../../core/clients/manage/power/create-and-apply-power-plans.md).|  
|**Power Mode**|Na lista suspensa, selecione o tipo de configurações de energia que deseja exibir nos resultados do relatório. Selecione **Conectado** para exibir as configurações de energia definidas para quando o computador está conectado e **Funcionando com bateria** para exibir as configurações de energia definidas para quando o computador está funcionando com bateria.|  
|**Índice de configuração**|Na lista suspensa, selecione o valor para o nome da configuração de energia selecionado sobre o qual deseja fornecer um relatório. Por exemplo, se você deseja exibir todos os computadores com a configuração **desligar disco rígido após** definida como **10** minutos, selecione **desligar disco rígido após** como o **Nome da Configuração de Energia** e **10** como o **Índice de Configuração**.|  

#### <a name="hidden-report-parameters"></a>Parâmetros de relatório ocultos  
 Opcionalmente, os parâmetros ocultos a seguir podem ser especificados para alterar o comportamento deste relatório.  

|Nome do parâmetro|Descrição|  
|--------------------|-----------------|  
|**numberOfLocalizations**|Especifique o número de idiomas nos quais você deseja exibir os nomes de configuração de energia relatados pelos computadores cliente. Se quiser exibir a linguagem mais popular, deixe essa configuração no padrão de **1**. Para exibir todas as linguagens, defina esse valor como **0**.|  

#### <a name="report-links"></a>Links de relatório  
 Este relatório contém links para o relatório a seguir, que fornece mais informações sobre o item selecionado.  

|Nome do relatório|Detalhes|  
|-----------------|-------------|  
|**Detalhes do Computador**|Clique em um nome do computador para ver os recursos de energia, as configurações de energia e os planos de energia aplicados para o computador selecionado.<br /><br /> Para obter mais informações, consulte [Computer Details Report](#BKMK_Computer_Details) neste tópico.|  



<!--HONumber=Nov16_HO1-->


