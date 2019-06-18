---
title: Como implantar em produção
titleSuffix: Configuration Manager
description: Um guia de instruções para a implantação em um grupo de produção de análise de área de trabalho.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d1a71558c6b87c79c6d4667746e081c6db85ce18
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159161"
---
# <a name="how-to-deploy-to-production-with-desktop-analytics"></a>Como implantar em produção com a análise de área de trabalho

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Depois que você [implantado para o piloto](/sccm/desktop-analytics/deploy-pilot) e revisar o status de seus ativos, você está pronto para atualizar o restante do seu ambiente de produção.

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

Há três partes principais para realizar a implantação de atualizações para dispositivos de produção:

1. [Examine os ativos que precisam de uma decisão de atualização](#bkmk_review): Para tornar os dispositivos pronto para implantação de produção, seus ativos devem ter sua decisão de atualização definido como **pronto** ou **pronto, as correções necessárias**.  

2. [Implantar em dispositivos que estão prontos](#bkmk_deploy): Use o Configuration Manager para atualizar dispositivos que estão prontos. A análise da área de trabalho fornece a lista de dispositivos prontos para implantação de produção e relatórios para monitorar o êxito da implantação.  

3. [Monitorar a integridade dos dispositivos atualizadas](#bkmk_monitor): Conforme o andamento da implantação de atualização, monitore a integridade dos ativos importantes. Se alguns precisam de atenção, solucionar problemas e corrigir esses problemas. Se você decidir que não podem ser corrigidos os problemas, parar a implantação nos dispositivos afetados, definindo sua decisão de atualização para **não é possível**.  

> [!NOTE]  
> Quando estiver seguro para o sucesso da implantação piloto, inicie a implantação de produção a qualquer momento. Não há nenhum requisito de que todos os dispositivos piloto alcançar o estado "concluído" pela primeira vez.  



## <a name="bkmk_review"></a> Examine os ativos que precisam de uma decisão de atualização

Análise da área de trabalho orienta o processo de revisão de seus ativos para implantação de produção. No portal do Azure, acesse **planos de implantação**, selecione um plano de implantação e, em seguida, selecione **preparar produção** no menu à esquerda.

![Exibição da captura de tela de produção preparar na área de trabalho de análise](media/prepare-production.png)

Examine o estado de seus aplicativos. Use essas informações para definir o decisão de atualização para cada um desses ativos.

Use cada uma das guias para examinar o status dos aplicativos. Em cada exibição com guias, você pode filtrar os resultados para mostrar os dispositivos que estão no caminho certo para a atualização, precisa de atenção, dispositivos com resultados mistos e esses dispositivos em um estado indeterminado.

Selecione **metas de reunião** para filtrar a exibição para ativos que são provável pronto para implantação de produção com base nos seguintes critérios:

- : Uma pré-atualização avaliação de risco dos riscos conhecidos para atualizar dispositivos que têm esse ativo instalado  

- Status de integridade: uma avaliação após a atualização dos dispositivos de outras implantações e se eles apresentou problemas após a atualização foi instalada. Para obter mais informações sobre integridade, consulte [monitorar a integridade dos dispositivos atualizadas](#bkmk_monitor).  

Para aprovar um ativo para a atualização, selecione o nome na lista e, em seguida, selecione uma das seguintes opções do **decisão de atualização** lista:

- Revisão em andamento
- Pronto
- Pronto (com correção)
- Não é possível
- Não revisado

Para definir esse valor para vários aplicativos ao mesmo tempo, use a primeira coluna **selecionar este item**e, em seguida, escolha **decisão de atualização definido**.

![Decisão de atualização de definição de opção em vários aplicativos](media/prep-prod-set-upgrade-decision.png)

Selecione **nenhum dado** aos ativos de exibição que não podem ser classificados. Esses ativos geralmente são ativos que não tem suficiente cobertura para análise de área de trabalho executar uma análise do status de integridade ou risco. Para melhorar a cobertura, adicionar dispositivos adicionais com esses ativos para o piloto ou solicitar que os usuários piloto para experimentar esses ativos.

Também pode haver ativos na **necessária atenção** ou **resultados misturados** estado. Esses ativos podem exigir análise adicional antes de você tomar uma decisão de atualização para eles.

Examine todos os aplicativos. Uma vez que um determinado dispositivo tem uma decisão de atualização positiva para todos os ativos, em seguida, seu estado é alterado para "pronto para produção." Para ver a contagem atual na página principal para o plano de implantação, selecione a terceira etapa de implantação, **Deploy**.


## <a name="bkmk_deploy"></a> Implantar em dispositivos que estão prontos

Configuration Manager usa os dados da área de trabalho de análise para criar uma coleção para a implantação de produção. Não implante a sequência de tarefas usando uma implantação tradicional. Use o procedimento a seguir para criar uma implantação integrada de análise de área de trabalho:

Se você seguiu o processo recomendado para [implantar no piloto dispositivos](/sccm/desktop-analytics/deploy-pilot#deploy-to-pilot-devices), a implantação em fases do Configuration Manager está pronta. Como você marca ativos como *pronto*, análise de área de trabalho sincroniza automaticamente os dispositivos para o Configuration Manager. Esses dispositivos são adicionados à coleção de produção. Quando a implantação em fases é movida para a segunda fase, esses dispositivos de produção recebem a implantação da atualização.

Se você tiver configurado a implantação em fases **iniciar manualmente a implantação da segunda fase**, em seguida, você precisa manualmente movê-lo para a próxima fase. Para obter mais informações, veja [Gerenciar e monitorar implantações em fases](/sccm/osd/deploy-use/manage-monitor-phased-deployments#bkmk_move).

Se você criou uma implantação única integrada de análise de área de trabalho na coleção piloto, você precisará repetir esse processo para implantar na coleção de produção.


### <a name="address-deployment-alerts"></a>Lidar com alertas de implantação

Como com a implantação do piloto, análise de área de trabalho avisa você de quaisquer problemas que exigem sua atenção durante a implantação de produção. Na área de trabalho de análise, vá para o plano de implantação e selecione **status de implantação** no menu à esquerda. O modo de exibição de status de implantação lista dispositivos nas seguintes categorias:  

- Não iniciada
- Em andamento
- Concluído
- Precisa de atenção – dispositivos (classificados por nome do dispositivo)
- Precisa de atenção – problemas (classificados por tipo de problema)

![Status da implantação de produção de análise de captura de tela da área de trabalho](media/prod-deployment-status.png)


## <a name="bkmk_monitor"></a> Monitorar a integridade dos dispositivos atualizadas

O **preparar produção** página se concentra em ajudá-lo a fazer a atualização decisões para seus ativos. Essa página por padrão mostra somente os ativos que ainda não estão na **pronto** estado. O **monitorar a integridade** página mostra problemas de integridade em qualquer ativo digno de nota, até mesmo os ativos que são marcados **pronto**. Se encontrar problemas, você pode solucionar e corrigir o problema ou alterar a decisão de atualização **não é possível**. Quando você altera o decisão de atualização, essa ação impede que atualizações futuras em dispositivos com esse ativo.

Esta página por ativos com os seguintes estados de integridade do filtro:

| Filtro de status de integridade | Descrição |
|----------------------|-------------|
| **Atenção necessária** | (Padrão de filtro) Área de trabalho Analytics detecta uma regressão estatisticamente significativa para alguma métrica de integridade para esse ativo
| **Metas de reunião** | Análise da área de trabalho não detecta nenhuma regressão no comportamento |
| **Dados insuficientes** | Análise da área de trabalho não tem dados suficientes sobre esse ativo para fazer recomendações |
| **Nenhum dado** | Nenhum dado de uso ainda está disponível para este ativo |

Para mostrar uma exibição não filtrada de todos os ativos, selecione o filtro atual. Esta ação remove o filtro.

> [!NOTE]  
> Para reduzir o número de ativos com dados insuficientes, área de trabalho de análise monitora os ativos em todos os dispositivos que atualizaram para a versão do Windows de destino especificada em seu plano de implantação. Esses dispositivos incluem aqueles não incluído no plano de implantação específico.  

A ordem de classificação padrão é o número de dispositivos que tiveram um incidente com este ativo em particular, portanto, você pode ver rapidamente quais delas estão causando a maioria dos problemas. Por exemplo, ao exibir **aplicativos**, ele classifica por **últimas duas semanas de falhas de dispositivos com o aplicativo**.

Se você quiser examinar a integridade de todos os ativos, até mesmo os ativos com dados insuficientes para análise de área de trabalho Criar inferências estatísticas, use o seguinte processo:

1. Selecione na lista suspensa na **dispositivos com incidentes nas duas últimas semanas** coluna. Adicione um filtro a somente os ativos que tem tido a incidentes em algum número mínimo de dispositivos para que seja interessante. Por exemplo, Mostrar itens com valores **maior que** 100.  

2. Selecione na lista suspensa na **% de dispositivos com incidentes nas últimas duas semanas** coluna e selecione para classificar por **decrescente**.  

    A exibição resultante mostra os ativos com a taxa mais alta de incidente em um número mínimo de incidentes.  

3. Selecione um ativo para obter mais detalhes ou alterar sua decisão de atualização.  

Para obter mais informações, consulte [monitoramento de status de integridade](/sccm/desktop-analytics/health-status-monitoring).
