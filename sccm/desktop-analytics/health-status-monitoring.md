---
title: Monitoramento do status de integridade
titleSuffix: Configuration Manager
description: Saiba mais sobre como funciona o monitoramento de status de integridade na área de trabalho de análise.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 834b7d30aa5331ae73125e1cdfc3c9c7095d58b7
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62255132"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>Análise de área de trabalho de monitoramento de status de integridade

Como você [implantar uma atualização em produção](/sccm/desktop-analytics/deploy-prod), usar a análise de área de trabalho para ajudar a monitorar o estado de integridade de seus dispositivos. Este artigo explica detalhadamente como funciona o monitoramento de integridade.

Para obter mais informações sobre como usar esse recurso, consulte [monitorar a integridade dos dispositivos atualizadas](/sccm/desktop-analytics/deploy-prod#bkmk_monitor).

![Captura de tela da página de monitorar a integridade da área de trabalho de análise](media/monitor-health.png)

> [!NOTE]  
> Análise da área de trabalho apenas coleta dados de integridade de dispositivos que fornecem dados de uso, que ele pode usar como um denominador. Isso significa que ele não inclui dispositivos que executam o Windows 7 e Windows 10 que não estão definidos para compartilhar dados de diagnóstico no nível avançado (limitado). Se mais de 10% dos dispositivos que executam o Windows 10 estiverem definidas para compartilhar dados de diagnóstico em níveis diferentes avançado (limitado), o **monitorar a integridade** página exibirá um aviso na área do banner.  

Para exibir mais informações sobre um aplicativo específico, suplemento ou macro consultoria, selecione-o na lista. 



## <a name="apps-and-office-apps"></a>Aplicativos e aplicativos do Office

![Fatores de status de integridade para um aplicativo em área de trabalho de análise](media/monitor-health-status-factors.png)

Análise da área de trabalho monitora os seguintes fatores de status de integridade para aplicativos e aplicativos do Office:

- **% De dispositivos com falhas**: Para as duas últimas semanas, o número de dispositivos nos quais esse aplicativo específico foi paralisado dividido pelo número de dispositivos em que o aplicativo foi usado. Essa exibição permite que você veja se a estabilidade do aplicativo aumentou ou diminuiu na nova versão do sistema operacional. Análise da área de trabalho calcula essa porcentagem para os seguintes conjuntos:  

    - **Após a atualização**: Dispositivos que foram atualizados para a versão do sistema operacional de destino especificada no plano de implantação. Para reduzir o número de ativos com dados insuficientes, área de trabalho Analytics coleta esses dados para todos os seus dispositivos atualizados. Esse conjunto inclui esses dispositivos não no plano de implantação.  

    - **Antes da atualização**: Dispositivos que estão em uma versão do sistema operacional anterior ao que é especificado no plano de implantação. Essa lista não inclui dispositivos que executam o Windows 7.   

    - **Méd. comercial**: A média (avg) taxa de falhas em todos os dispositivos comerciais. Essa média é calculada *todos os* versões do aplicativo. Se sua versão mostra uma taxa de falha acima da média comercial, pode haver uma versão estável mais disponível.  

- **% Sessões com falhas**: Semelhante ao anterior, mas a porcentagem de sessões com falha nas últimas duas semanas de contagens.  

Para determinar o status de integridade de um aplicativo, análise de área de trabalho requer dados de dispositivos de pelo menos 20. Caso contrário, ele relata **dados insuficientes** para o aplicativo. O serviço calcula o status de integridade com base nas *taxa de falhas de sessão* desses dispositivos. A taxa de falha do dispositivo é fornecida apenas para fins informativos. Ele não é usado no cálculo de status de integridade.

Na parte inferior da página de detalhes do aplicativo, as três guias a seguir podem ajudá-lo a solucionar problemas:

- **Outras versões**: Uma lista de versões alternativas deste aplicativo. Para cada versão, ele mostra as alterações relativas às taxas de falha em sua organização e a média comercial. Se você encontrar uma versão posterior do aplicativo com uma taxa mais baixa de falhas, atualizando o aplicativo pode ajudar.  

    Ele também mostra se a versão tem um **pronto para o Windows** sinal. Para obter mais informações, consulte [riscos de compatibilidade para aplicativos do Windows](/sccm/desktop-analytics/compat-risk#risk-assessment-engine).  

- **Principais problemas**: Uma lista da falha mais frequente IDs pela contagem de instância. Uma ID de falha identifica o rastreamento de pilha associado com a falha. Você pode usar essa ID ao chamar o fornecedor do aplicativo para obter suporte.  

- **Falhas recentes**:  Uma lista de dispositivos nos quais o aplicativo recentemente com falha. Você pode filtrar por ID da falha e outros critérios. Use essas informações para solucionar o problema pela coleta de logs ou a tentativa de correções em dispositivos específicos antes de tentar uma implantação mais ampla.  

Se você encontrar uma regressão de integridade sério que você não consegue corrigir, alterar o aplicativo **decisão de atualização** à **não é possível**. Essa ação impede que as implantações futuras da atualização para dispositivos com esse ativo.



## <a name="office-add-ins"></a>Suplementos do Office

![Captura de tela de fatores de status de integridade para um suplemento do Office](media/office-add-in-health-status-factors.png)

Análise da área de trabalho monitora os seguintes fatores de status de integridade para suplementos do Office:

- **% De dispositivos com incidentes**: Um incidente é algo que impede que um suplemento funcione corretamente. Por exemplo, ele falha ao carregar ou não responde. Esta seção mostra o número de dispositivos para as últimas duas semanas no qual o suplemento selecionado tinha um incidente dividido pelo número de dispositivos em que o suplemento está instalado. Análise da área de trabalho calcula essa porcentagem para os seguintes conjuntos:  

    - **Após a atualização**: Dispositivos que foram atualizados para a versão do Office de destino especificada no plano de implantação. Para reduzir o número de ativos com dados insuficientes, área de trabalho Analytics coleta esses dados para todos os seus dispositivos atualizados. Esse conjunto inclui esses dispositivos não no plano de implantação.  

    - **Antes da atualização**: Dispositivos que executam qualquer versão do Office mais antigo do que a versão que a implantação do plano de destinos. <!-- This does not include {include min version of Office}  --> Para avaliar a integridade do suplemento, compare essa métrica para o **após a atualização** percentual.  

    - **Méd. comercial**: A taxa média (avg) incidentes em todos os dispositivos comerciais que usam a mesma versão do suplemento na mesma versão do Office. Use essa taxa para comparar em relação a dispositivos na sua organização. Se esta versão do suplemento é ter uma taxa maior de incidentes que a média comercial, você pode ter algum fator ambiental que contribuem para os incidentes.  

- **% Sessões com incidentes**: Semelhante ao anterior, mas a porcentagem de sessões com falha nas últimas duas semanas de contagens.  

Para determinar o status de integridade de suplementos, análise de área de trabalho requer pelo menos três dispositivos para a taxa de incidentes do dispositivo e pelo menos 10 sessões para a taxa de incidente de sessão. Para ambas as taxas, ele compara os valores para determinar se há uma regressão antes e depois. Nenhuma regressão é considerada para atender as metas. 

Área de trabalho Analytics calcula o status de integridade geral do suplemento Office com base em uma combinação de taxas de incidentes dispositivo e de sessão usando a matriz a seguir:

|  | Dados insuficientes para falhas de dispositivo  | Métricas de falha de dispositivo de integridade | Regressão em métricas de falha do dispositivo |
|----------------|---------------------|-----------------------|------------------------|
| **Dados insuficientes para sessões com incidentes**| Dados insuficientes| Metas de reunião | Dados insuficientes |
| **Métricas de íntegras para sessões com incidentes** | Metas de reunião | Metas de reunião | Metas de reunião |
| **Regressão nas métricas para sessões com incidentes** | Dados insuficientes | Metas de reunião | Atenção necessária |


A página de detalhes do suplemento do Office também inclui os seguintes detalhes para ajudá-lo a solucionar problemas: 

- **Incidentes recentes**: Uma lista de dispositivos em que um suplemento incidente ocorreu recentemente. Use esta lista para solucionar o problema pela coleta de logs ou a tentativa de correções nesses dispositivos específicos antes de tentar uma distribuição mais ampla.  



## <a name="office-macros"></a>Macros do Office

![Captura de tela de fatores de status de integridade para uma consultoria de macro do Office](media/office-macros-health-status-factors.png)

Análise da área de trabalho relata status de integridade *consultorias de macro*. As consultorias de macro são problemas potenciais detectados nos arquivos do Office que contém macros. Esses problemas são específicos para um aplicativo do Office. Por exemplo, Word, Excel, PowerPoint ou Visio. 

Análise da área de trabalho monitora os seguintes fatores de status de integridade para macros do Office:

- **% De dispositivos com erro de compilação**: Para as últimas duas semanas, o número de dispositivos nos quais erros relacionados ao comunicado ocorreu durante a habilitação de macro dividida pelo número de dispositivos no qual o comunicado foi detectado. Análise da área de trabalho calcula essa porcentagem para os seguintes conjuntos: 

    - **Após a atualização**: Os dispositivos em que a versão do Office é o mesmo que o destino do plano de implantação  

    - **Antes da atualização**: Os dispositivos que executam qualquer versão do Office mais antigo que o destino do plano de implantação  

    - **Méd. comercial**: A média (avg) de todos os dispositivos comerciais executando a mesma versão do Office como destino do plano de implantação  

- **% De dispositivos com o erro de tempo de execução** semelhante à anterior, mas para as últimas duas semanas, os dispositivos nos quais erros relacionados ao comunicado ocorreram durante a execução de macro dividida pelo número de dispositivos no qual o comunicado foi detectado.  

A página de detalhes de macros do Office também inclui os seguintes detalhes para ajudá-lo a solucionar problemas: 

- **Incidentes recentes**: Uma lista de dispositivos em macro erros de tempo de execução e compilação ocorreram recentemente. Use esta lista para solucionar o problema pela coleta de logs ou a tentativa de correções nesses dispositivos específicos antes de tentar uma distribuição mais ampla.



## <a name="see-also"></a>Consulte também

- [Risco de compatibilidade de aplicativos do Windows na área de trabalho de análise](/sccm/desktop-analytics/compat-risk)  

- [Como implantar em produção com a análise de área de trabalho](/sccm/desktop-analytics/deploy-prod)  
