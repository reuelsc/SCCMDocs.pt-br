---
title: Ativos no desktop Analytics
titleSuffix: Configuration Manager
description: Saiba mais sobre dispositivos, drivers e aplicativos na análise de desktops.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 63800bf6c8fa1d35eac44f64f2f03bde4f1d5022
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68536006"
---
# <a name="assets-in-desktop-analytics"></a>Ativos no desktop Analytics

> [!Note]  
> Essas informações se relacionam a um serviço de visualização que pode ser substancialmente modificado antes de ser lançada comercialmente. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Depois que os dispositivos relatam dados para a análise de desktop, ele fornece um inventário dos seguintes ativos:

- Pseudodispositivos
- Aplicativos instalados  

No portal do serviço, selecione **ativos** no menu análise da área de trabalho.


## <a name="devices"></a>Pseudodispositivos

A guia **dispositivos** exibe informações importantes sobre todos os dispositivos em sua organização que você registra no desktop Analytics. Você pode classificar em qualquer coluna ou filtro para valores específicos.

> [!NOTE]  
> Se o painel não relatar o número de dispositivos que você espera ver para seu ambiente, consulte [solução de problemas do desktop Analytics](/sccm/desktop-analytics/troubleshooting).  

Em um plano de implantação, há mais detalhes sobre os dispositivos. Para obter mais informações, consulte [planejar ativos](/sccm/desktop-analytics/about-deployment-plans#plan-assets)

## <a name="apps"></a>Aplicativos

A guia **aplicativos** mostra todos os aplicativos instalados que o serviço detecta em seus dispositivos Windows.

Os aplicativos **notáveis** são instalados em mais de 2% dos dispositivos registrados.

Configure a **importância** dos aplicativos definindo uma das seguintes categorias:

- Crítico
- Fundamental
- Ignorar
- Não revisado

Selecione o aplicativo na lista e selecione **Editar**. Esta ação exibe detalhes para o aplicativo. Selecione o menu suspenso **importância** e defina um valor. Você também pode atribuir um **proprietário**. Se você fizer alterações, selecione **salvar**.

Em um plano de implantação, você também pode definir a **decisão de atualização**. Para obter mais informações, consulte [planejar ativos](/sccm/desktop-analytics/about-deployment-plans#plan-assets)


## <a name="next-steps"></a>Próximas etapas

- [Saiba mais sobre os planos de implantação do desktop Analytics](/sccm/desktop-analytics/about-deployment-plans)  

- [Saiba mais sobre atualizações de segurança e recursos](/sccm/desktop-analytics/about-updates)  

- [Avaliação de compatibilidade no desktop Analytics](/sccm/desktop-analytics/compat-assessment)  
