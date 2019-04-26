---
title: Atualizações na análise da área de trabalho
titleSuffix: Configuration Manager
description: Saiba mais sobre atualizações de segurança e de recurso na área de trabalho de análise.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: a10a7b5bbb3a1b7d0dada86774f3412e22faff01
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62243488"
---
# <a name="updates-in-desktop-analytics"></a>Atualizações na análise da área de trabalho 

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

No portal de análise de área de trabalho, exiba o status das atualizações de segurança e de recurso. Selecione esses nós no grupo de Monitor do menu principal da área de trabalho de análise. Esses nós fornecem informações sobre o status dessas atualizações em seu ambiente. 



## <a name="security-updates"></a>Atualizações de segurança

Para examinar o status atual das atualizações de segurança, selecione **atualizações de segurança** na **Monitor** seção da área de trabalho de análise:

![Nó de atualizações de segurança da área de trabalho de análise](media/security-updates.png)

Este modo de exibição resume *segurança* atualizações para dispositivos que executam o Windows 10 ou do Office 365 ProPlus. Dispositivos no gráfico de barras são categorizados pelos seguintes rótulos:

#### <a name="latest"></a>mais recente
Dispositivos estão em execução de atualização de segurança mais recente para essa versão e o canal.

#### <a name="latest-1"></a>Versão mais recente-1
Dispositivos estão executando uma atualização uma versão de segurança mais antiga do que a atualização mais recente disponível naquele canal.

#### <a name="older"></a>Mais antigo
Dispositivos estão executando uma atualização de segurança com mais de 1 a versão mais recente.

#### <a name="not-measured"></a>Não é medido
Análise da área de trabalho ainda não avaliou o dispositivo. 

- Para Windows, isso inclui dispositivos que executam o Windows 7, Windows 8.1 ou Windows 10 dispositivos registrados para o programa do Windows Insider  

- Para o Office, isso inclui dispositivos com uma das seguintes versões:  

    - Canal do Office 365 ProPlus, Insider  

    - Uma versão perpétua do Office que usam o Windows installer. Por exemplo, Office 2016, Office 2013 ou Office 2010.  

    - O Office 365 ProPlus em um dispositivo que ainda não retornou dados suficientes para avaliar o status de segurança  



## <a name="feature-updates"></a>Atualizações de recursos

Para examinar o status atual das atualizações de recurso, selecione **atualizações de recursos** na **Monitor** seção da área de trabalho de análise:

![Nó de atualizações de recurso da área de trabalho de análise](media/feature-updates.png)

Este modo de exibição resume *recurso* atualizações para dispositivos que executam o Windows 10 ou do Office 365 ProPlus. 

Para obter mais informações sobre períodos de serviço, consulte os seguintes artigos: 
- [Folha de fatos de ciclo de vida do Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)  
- [Histórico de atualizações do Office 365 ProPlus](https://docs.microsoft.com/officeupdates/update-history-office365-proplus-by-date)  

Dispositivos no gráfico de barras são categorizados pelos seguintes rótulos:

#### <a name="in-service"></a>No serviço
Dispositivos estiver executando a atualização mais recente do recurso para essa versão e o canal.  

#### <a name="near-end-of-service"></a>Próximo ao fim do serviço
Dispositivos estão executando uma atualização de recurso que está dentro de 90 dias de atingir o final do serviço.

#### <a name="end-of-service"></a>Final do serviço
Dispositivos estão executando uma atualização de recurso que ultrapassou o fim da data de serviço. Para obter detalhes sobre o encerramento de datas do serviço, consulte [folha de fatos de ciclo de vida do Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)  <!-- {xlink into relevant section of UDR_monitoring}|-->

#### <a name="not-measured"></a>Não é medido
Análise da área de trabalho ainda não avaliou o dispositivo. 

- Para Windows, isso inclui dispositivos que executam o Windows 7, Windows 8.1 ou Windows 10 dispositivos registrados para o programa do Windows Insider

- Para o Office, isso inclui dispositivos com uma das seguintes versões:  

    - Canal do Office 365 ProPlus, Insider  

    - Uma versão perpétua do Office que usam o Windows installer. Por exemplo, Office 2016, Office 2013 ou Office 2010.  

    - O Office 365 ProPlus em um dispositivo que ainda não retornou dados suficientes para avaliar o status de segurança  



## <a name="next-steps"></a>Próximas etapas

- [Saiba mais sobre os ativos de área de trabalho de análise](/sccm/desktop-analytics/about-assets): dispositivos, aplicativos, os aplicativos do Office, suplementos do Office e as macros do Office  

- [Saiba mais sobre planos de implantação](/sccm/desktop-analytics/about-deployment-plans)  

