---
title: Suporte para Windows 10 | Microsoft Docs
description: "Saiba quais versões do Windows 10 têm suporte para executar o cliente do System Center Configuration Manager."
ms.custom: na
ms.date: 2/10/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: 5
author: brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3702993d6cf9644d5aebaadd168749668fbcb62c
ms.openlocfilehash: 4b90384621dd20475ab9ea33ea062c24f5ecf5fa
ms.lasthandoff: 02/22/2017

---
# <a name="support-for-windows-10-as-a-client-of-system-center-configuration-manager"></a>Suporte para Windows 10 como um cliente do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


 Este tópico identifica as versões do Windows 10 que você pode usar como um cliente com as diferentes versões do Branch Atual do System Center Configuration Manager.

- Ele suplementa o artigo [Sistemas operacionais com suporte para clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
- Se você usa o Branch de Manutenção de Longo Prazo do Configuration Manager, consulte [Configurações com suporte para o Branch de Manutenção de Longo Prazo](/sccm/core/understand/supported-configurations-for-ltsb).

O Configuration Manager tenta fornecer suporte para cada nova versão do Windows 10 logo após o lançamento da versão do Windows. Como os produtos têm agendas separadas de desenvolvimento e lançamento, o suporte que o Configuration Manager fornece depende de quando as versões e ramificações de cada produto são liberadas.  



|Versões do Windows 10 |Configuration Manager 1602|Configuration Manager 1606|Configuration Manager 1610|
|---------------------|-----|-----|-----|
|Enterprise 2015 LTSB |![Com suporte](media/green_check.png) |![Com suporte](media/green_check.png) |![Com suporte](media/green_check.png) |
|1507 <br />Enterprise, Pro | ![Com suporte](media/green_check.png)| ![Com suporte](media/green_check.png)|![Com suporte](media/green_check.png) |
|1511 <br />Enterprise, Pro <br />(CB), (CBB) |![Com suporte](media/green_check.png) |![Com suporte](media/green_check.png) |![Com suporte](media/green_check.png) |
|Enterprise 2016 LTSB    |![Sem suporte](media/Red_X.png) |![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png)|
|1607 <br />Enterprise, Pro<br /> (CB)    |![Sem suporte](media/Red_X.png) |![Compatível com versões anteriores](media/blue_compat.png) |![Com suporte](media/green_check.png) |
|1607 <br />Enterprise, Pro <br />(CBB)    |![Sem suporte](media/Red_X.png) |![Compatível com versões anteriores](media/Red_X.png) |![Com suporte](media/green_check.png) |


|Chave|
|--|
|![Com suporte](media/green_check.png) = **Com suporte**  |
|![Sem suporte](media/blue_compat.png)  = **Compatível com versões anteriores** Isso significa que os recursos de gerenciamento de cliente existentes (inventário de hardware, inventário de software, atualizações de software, etc.) devem funcionar com o novo build do Branch Atual do Windows 10. Problemas conhecidos ou advertências serão documentados. <br><br>Essa abordagem proporciona a capacidade de implantar e gerenciar novas compilações do Windows 10 no primeiro dia com suporte para compatibilidade do aplicativo sem exigir uma nova versão de atualização do Configuration Manager. |
|![Com suporte](media/Red_X.png) = **Sem suporte**|

