---
title: Monitoramento do status de integridade
titleSuffix: Configuration Manager
description: Saiba mais sobre como funciona o monitoramento de status de integridade na área de trabalho de análise.
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5dc3123763430dc35d566b68e3c1c04762d26de5
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159044"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>Análise de área de trabalho de monitoramento de status de integridade

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Como você [implantar uma atualização em produção](/sccm/desktop-analytics/deploy-prod), usar a análise de área de trabalho para ajudar a monitorar o estado de integridade de seus dispositivos. Este artigo explica detalhadamente como funciona o monitoramento de integridade.

Para obter mais informações sobre como usar esse recurso, consulte [monitorar a integridade dos dispositivos atualizadas](/sccm/desktop-analytics/deploy-prod#bkmk_monitor).

![Captura de tela da página de monitorar a integridade da área de trabalho de análise](media/monitor-health.png)

> [!NOTE]  
> Análise da área de trabalho apenas coleta dados de integridade de dispositivos que fornecem dados de uso, que ele pode usar como um denominador. Isso significa que ele não inclui dispositivos que executam o Windows 7 e Windows 10 que não estão definidos para compartilhar dados de diagnóstico no nível avançado (limitado). Se mais de 10% dos dispositivos que executam o Windows 10 estiverem definidas para compartilhar dados de diagnóstico em níveis diferentes avançado (limitado), o **monitorar a integridade** página exibirá um aviso na área do banner.  

Para exibir mais informações sobre um aplicativo específico, selecione-o na lista.



## <a name="apps"></a>Aplicativos

![Fatores de status de integridade para um aplicativo em área de trabalho de análise](media/monitor-health-status-factors.png)

Análise da área de trabalho monitora os seguintes fatores de status de integridade para aplicativos:

- **% De dispositivos com falhas**: Para as duas últimas semanas, o número de dispositivos nos quais esse aplicativo específico foi paralisado dividido pelo número de dispositivos em que o aplicativo foi usado. Essa exibição permite que você veja se a estabilidade do aplicativo aumentou ou diminuiu na nova versão do sistema operacional. Análise da área de trabalho calcula essa porcentagem para os seguintes conjuntos:  

    - **Após a atualização**: Dispositivos que foram atualizados para a versão do sistema operacional de destino especificada no plano de implantação. Para reduzir o número de ativos com dados insuficientes, área de trabalho Analytics coleta esses dados para todos os seus dispositivos atualizados. Esse conjunto inclui esses dispositivos não no plano de implantação.  

    - **Antes da atualização**: Dispositivos que estão em uma versão do sistema operacional anterior ao que é especificado no plano de implantação. Essa lista não inclui dispositivos que executam o Windows 7.  

    - **Méd. comercial**: A média (avg) taxa de falhas em todos os dispositivos comerciais. Essa média é calculada *todos os* versões do aplicativo. Se sua versão mostra uma taxa de falha acima da média comercial, pode haver uma versão estável mais disponível.  

- **% Sessões com falhas**: Semelhante ao anterior, mas a porcentagem de sessões com falha nas últimas duas semanas de contagens.  

Para determinar o status de integridade de um aplicativo, análise de área de trabalho requer dados de dispositivos de pelo menos 20. Caso contrário, ele relata **dados insuficientes** para o aplicativo. O serviço calcula o status de integridade com base nas *taxa de falhas de sessão* desses dispositivos. A taxa de falha do dispositivo é fornecida apenas para fins informativos. Ele não é usado no cálculo de status de integridade.

Na parte inferior da página de detalhes do aplicativo, as três guias a seguir podem ajudá-lo a solucionar problemas:

- **Outras versões**: Uma lista de versões alternativas deste aplicativo. Para cada versão, ele mostra as alterações relativas às taxas de falha em sua organização e a média comercial. Se você encontrar uma versão posterior do aplicativo com uma taxa mais baixa de falhas, atualizando o aplicativo pode ajudar.  

    Ele também mostra se a versão tem um **pronto para o Windows** sinal. Para obter mais informações, consulte [avaliação de compatibilidade](/sccm/desktop-analytics/compat-assessment#risk-assessment-engine).  

- **Principais problemas**: Uma lista da falha mais frequente IDs pela contagem de instância. Uma ID de falha identifica o rastreamento de pilha associado com a falha. Você pode usar essa ID ao chamar o fornecedor do aplicativo para obter suporte.  

- **Falhas recentes**:  Uma lista de dispositivos nos quais o aplicativo recentemente com falha. Você pode filtrar por ID da falha e outros critérios. Use essas informações para solucionar o problema pela coleta de logs ou a tentativa de correções em dispositivos específicos antes de tentar uma implantação mais ampla.  

Se você encontrar uma regressão de integridade sério que você não consegue corrigir, alterar o aplicativo **decisão de atualização** à **não é possível**. Essa ação impede que as implantações futuras da atualização para dispositivos com esse ativo.


## <a name="see-also"></a>Consulte também

- [Avaliação de compatibilidade na área de trabalho de análise](/sccm/desktop-analytics/compat-assessment)  

- [Como implantar em produção com a análise de área de trabalho](/sccm/desktop-analytics/deploy-prod)  
