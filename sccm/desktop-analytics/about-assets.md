---
title: Ativos na análise da área de trabalho
titleSuffix: Configuration Manager
description: Saiba mais sobre dispositivos, drivers e aplicativos na área de trabalho de análise.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b0e47541d7acf5e1f5a74a58f6d39603bfcb9269
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159245"
---
# <a name="assets-in-desktop-analytics"></a>Ativos na análise da área de trabalho

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Depois que dispositivos relatam dados para análise de área de trabalho, ele fornece um inventário de ativos a seguir:

- Dispositivos  
- Drivers de hardware  
- Aplicativos instalados  

No portal do serviço, selecione **ativos** no menu de análise de área de trabalho.


## <a name="devices"></a>Dispositivos

O **dispositivos** guia exibe informações importantes sobre todos os dispositivos em sua organização que podem ser registrados para análise de área de trabalho. Você pode classificar qualquer coluna ou filtro para valores específicos.

> [!NOTE]  
> Se o painel não está relatando o número de dispositivos que você espera para o seu ambiente, consulte [solução de problemas de análise de área de trabalho](/sccm/desktop-analytics/troubleshooting).  

Em um plano de implantação, há mais detalhes sobre os dispositivos. Para obter mais informações, consulte [planejar ativos](/sccm/desktop-analytics/about-deployment-plans#plan-assets)

## <a name="apps"></a>Aplicativos

O **aplicativos** guia instalado mostra todos os aplicativos que o serviço detecta nos seus dispositivos Windows.

**Vale a pena observar** aplicativos são instalados em mais de 2% de dispositivos registrados.

Configurar o **importância** de aplicativos, definindo uma das seguintes categorias:

- Crítico
- Importante
- Ignorar
- Não revisado

Selecione o aplicativo na lista e, em seguida, selecione **editar**. Essa ação exibe os detalhes para o aplicativo. Selecione o **importância** menu suspenso e defina um valor. Você também pode atribuir um **proprietário**. Se você fizer alterações, selecione **salvar**.

Em um plano de implantação, você também pode definir as **decisão de atualização**. Para obter mais informações, consulte [planejar ativos](/sccm/desktop-analytics/about-deployment-plans#plan-assets)


## <a name="next-steps"></a>Próximas etapas

- [Saiba mais sobre planos de implantação de área de trabalho de análise](/sccm/desktop-analytics/about-deployment-plans)  

- [Saiba mais sobre atualizações de segurança e de recurso](/sccm/desktop-analytics/about-updates)  

- [Avaliação de compatibilidade na área de trabalho de análise](/sccm/desktop-analytics/compat-assessment)  
