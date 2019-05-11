---
title: Analisador de integridade do aplicativo
titleSuffix: Configuration Manager
description: Um guia de instruções para avaliar a compatibilidade com o analisador de integridade do aplicativo na área de trabalho de análise.
ms.date: 04/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2af150a4-0c18-4b40-8492-c04c5d154596
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: d982094a427f1f67992584e3262493d3f4a96766
ms.sourcegitcommit: 9af73f5c1b93f6ccaea3e6a096f75a5fecd65c2f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64669162"
---
# <a name="how-to-assess-compatibility-with-app-health-analyzer"></a>Como avaliar a compatibilidade com o analisador de integridade do aplicativo

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Use o Kit de ferramentas do analisador de integridade do aplicativo para a área de trabalho de análise para avaliar problemas de compatibilidade de aplicativos de desktop. Ele ajuda a concentrar seus esforços de validação para aplicativos da área de trabalho, incluindo aplicativos de linha de negócios. A ferramenta fornece uma classificação de risco, juntamente com as ações de correção possíveis. Ele também inclui um relatório de prontidão do aplicativo para ajudá-lo a avaliar a preparação do aplicativo para suas atualizações do Windows 10.



## <a name="download"></a>Baixar

Entre em contato com seu representante da Microsoft para obter um link de download. Sempre use a versão mais atual.

O download é um arquivo do Windows Installer (MSI). Instale o Kit de ferramentas do analisador de integridade do aplicativo em um computador do usuário. Quando você executar o Kit de ferramentas, um assistente orienta você pelo processo de criação de um relatório de preparação do aplicativo.

O Kit de ferramentas inclui scripts de exemplo. Se você precisar automatizar a coleta de informações sobre a preparação dos dispositivos em toda a organização, use o Configuration Manager para implantar esses scripts. Para obter mais informações, consulte [automação](#automation).



## <a name="how-it-works"></a>Como isso funciona

A ferramenta faz uma análise estática de aplicativos que já estão instalados em um dispositivo. Ele não faz análise de um instalador de aplicativo do pacote. Um usuário não precisa executar o aplicativo. A ferramenta avalia todos os aplicativos instalados registrados com o Windows no dispositivo.

Analisador de integridade do aplicativo não exige que você mantenha os instaladores para aplicativos herdados que você não gerencia ativamente. Ele identifica problemas de compatibilidade com o aplicativo em seu estado instalado. Todos os aplicativos são avaliados para regras de compatibilidade predefinidos. Esses sinais são problemas comuns de predominantes relatados à Microsoft quando os clientes de atualização para o Windows 10. As informações de compatibilidade também incluem ações de correção possíveis ou correções. Se você tiver aplicativos com problemas, comece com as ações sugeridas.

> [!Important]  
> O Kit de ferramentas não oferece suporte a recursos para reparar ou corrigir seus aplicativos. Se você criar um relatório de prontidão do aplicativo, ele fornece informações e diretrizes para ajudar você a corrigir seus aplicativos antes de atualizar para o Windows 10.  



## <a name="prerequisites"></a>Pré-requisitos

Antes de instalar e usar o Kit de ferramentas, verifique se que o dispositivo atende aos seguintes requisitos:  

- Windows 7 Service Pack 1 ou posterior  

- Você tem privilégios de administrador no dispositivo  

- Microsoft .NET Framework 4.5.1 ou posterior  

- Registrado no serviço de análise de área de trabalho, que inclui os seguintes requisitos:  

    - Atualizações mais recentes. Para obter mais informações, consulte [atualizar dispositivos](/sccm/desktop-analytics/enroll-devices#update-devices).  

    - Nível de dados de diagnóstico. Para obter mais informações, consulte [níveis de dados de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  



## <a name="analyze"></a>Analisar

1. Instale o analisador de integridade do aplicativo para o dispositivo de destino. Por padrão, ele instala o seguinte caminho: `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer`  

2. Vá para o Windows **inicie** menu, expanda o **analisador de integridade do aplicativo Microsoft** e abra o **analisador de integridade do aplicativo** como administrador. Ele pode levar vários minutos para gerar o relatório.  

    > [!Note]  
    > Se qualquer uma das configurações de diagnóstico de dados necessários não estiverem configurados, você verá um erro. Verifique se que você definir corretamente as configurações de pré-requisito. Para obter mais informações, consulte [níveis de dados de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

3. Quando o relatório de prontidão do aplicativo for aberto, ele começa a avaliação de aplicativos. Aguarde até que o Kit de ferramentas ser concluído, que pode demorar dependendo do número de aplicativos no dispositivo.  

![Captura de tela do relatório de disponibilidade do aplicativo do analisador de integridade do aplicativo](media/app-readiness-report-evaluating.png)

Você pode minimizar a janela e continuar com outras tarefas enquanto o Kit de ferramentas é executado em segundo plano.


### <a name="app-readiness-report-features"></a>Recursos de relatório de prontidão do aplicativo

#### <a name="get-started"></a>Introdução

Este guia fornece uma visão geral dos sinais com suporte nesta versão atual. Ele também inclui as ações de correção possíveis.

#### <a name="insights"></a>Insights

Este guia fornece uma exibição de todos os aplicativos que a ferramenta é avaliada. Ele mostra a avaliação de risco e os vários sinais usados para identificar problemas de compatibilidade.

- **Sinais** menu: Filtrar esses aplicativos por sinais usando o menu à esquerda  

- **Exportação de CSV**: Exportar essas informações como um arquivo de valores separados por vírgulas (CSV)  

- **Examinar novamente aplicativos**: Se você instalar qualquer novo aplicativo, use esta opção para executar novamente a ferramenta  

- **Solução de problemas de ID**: Se o dispositivo tiver aplicativos instalados, mas se nenhuma informação no relatório, dar a essa ID para dar suporte  

#### <a name="desktop-analytics"></a>Análise de Área de Trabalho

Essa guia fornece uma visão geral de como você pode usar o analisador de integridade do aplicativo para fornecer informações de preparação para aplicativos em sua organização.



## <a name="automation"></a>Automação

Para obter essas informações de aplicativo em vários dispositivos, implante a versão de linha de comando do analisador de integridade do aplicativo com o Configuration Manager. Implantá-lo a um pequeno conjunto de dispositivos representativos dentro da sua organização. Por exemplo, usar a análise de área de trabalho *piloto* coleção. O mesmo [pré-requisitos](#prerequisites) se aplicam para esses dispositivos.

Antes de fazer uma implantação mais ampla, primeiro verifique se uma execução bem-sucedida. Verifique se que os dados estão aparecendo na área de trabalho de análise.

O Kit de ferramentas do analisador de integridade do aplicativo inclui um exemplo de script, run_silent.cmd. Por padrão, esse script está no seguinte caminho: `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer`. Use esse script para automatizar o processo com o Configuration Manager.


### <a name="tips"></a>Dicas

- Antes de atualizar para o sistema operacional de destino, implante o analisador de integridade do aplicativo para todos os dispositivos em seu projeto-piloto. Para obter insights de preparação em vigor, executá-lo o pelo menos uma vez no grupo piloto para um plano de implantação.  

- Análise da área de trabalho tem funcionalidade interna para recomendar grupos piloto para seus planos de implantação. Execute o Kit de ferramentas em todos os dispositivos piloto para obter cobertura total em seus aplicativos importantes.  

- Agende a ferramenta seja executada quando um usuário não estiver conectado, ou quando não estiver usando o dispositivo.  

- Configure um agendamento recorrente. Por exemplo, executá-lo a cada 30 dias. Esse agendamento obtém as últimas descobertas de preparação de seus dispositivos para ajudá-los a se manter atualizado.  



## <a name="desktop-analytics-integration"></a>Integração da área de trabalho de análise

A seguinte captura de tela da área de trabalho de análise mostra os detalhes da versão 1.15.25 ContosoApp.

- Ele tem um **médio** avaliação de riscos  
- Uma versão adotada está disponível  
- Ele tem uma dependência de driver  

![Análise da área de trabalho, mostrando os fatores de risco de compatibilidade de um aplicativo](media/aha-desktop-analytics-compat-risk-factors.png)



## <a name="troubleshooting"></a>Solução de problemas

Esta seção aborda as etapas de solução de problemas e os problemas operacionais mais comuns que você pode ver com o analisador de integridade do aplicativo. Por exemplo:

- Você não vir a tela de boas-vindas no analisador de integridade do aplicativo  

- Há aplicativos instalados no dispositivo, mas você não vir quaisquer informações no relatório de disponibilidade do aplicativo  

- Nada acontece quando você executar a ferramenta  

### <a name="diagnostic-data-settings"></a>Configurações de dados de diagnóstico

Verifique novamente as configurações para as configurações de dados de diagnóstico do Windows. Configuration Manager deve definir esses valores quando integra o dispositivo para a área de trabalho de análise. Você pode usar outros métodos, como a diretiva de grupo ou de script como uma solução alternativa. Para obter mais informações, consulte [níveis de dados de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

### <a name="verbose-mode"></a>Modo detalhado

Execute a ferramenta no modo detalhado com o script run_verbose.cmd. Por padrão, o script está no seguinte caminho: `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer\run_verbose.cmd`

O modo detalhado gera logs adicionais, que podem ajudar a solucionar os problemas potenciais. Ele salva os logs para o `LogCollection` pasta no local instalado. Por exemplo, o caminho de coleção de log padrão é: `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer\LogCollection\`


## <a name="see-also"></a>Consulte também

O benefício de centro FastTrack para Windows 10 fornece acesso aos **aplicativo de área de trabalho garantir**. Esse benefício é um novo serviço projetado para resolver problemas com a compatibilidade de aplicativo do Office 365 ProPlus e Windows 10. Para obter mais informações, consulte [aplicativo de área de trabalho garantir](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
