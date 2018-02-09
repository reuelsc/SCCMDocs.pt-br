---
title: Suporte para Windows 10
titleSuffix: Configuration Manager
description: "Saiba mais sobre as versões do Windows 10 que têm suporte como clientes ou para OSD com o System Center Configuration Manager."
ms.custom: na
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2dfe9b63e9e7c41a4f8457dc5622f386c7cceec2
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2018
---
# <a name="support-for-windows-10-for-system-center-configuration-manager"></a>Suporte para Windows 10 para System Center Configuration Manager  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


 Este tópico descreve as versões do Windows 10 que você pode usar com as diferentes versões do Branch Atual do System Center Configuration Manager. Esse suporte inclui:
 -  Windows 10 como um cliente do Configuration Manager
 -  O ADK (Kit de Avaliação e Implantação do Windows) para Windows 10

## <a name="windows-10-as-a-client"></a>Windows 10 como cliente
O Configuration Manager tenta fornecer suporte como cliente para cada versão nova do Windows 10 assim que ela fica disponível. Como os produtos têm agendas separadas de desenvolvimento e lançamento, o suporte que o Configuration Manager fornece depende de quando cada uma é disponibilizada.

Por exemplo, uma versão do Configuration Manager é removida da matriz após o fim do [suporte para essa versão](/sccm/core/servers/manage/current-branch-versions-supported). Da mesma forma, o suporte para as versões do Windows 10, como a Enterprise 2015 LTSB ou 1511, sai da matriz quando elas são removidas do suporte. Para obter mais informações, consulte [Sistemas operacionais preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems).


-   As informações a seguir complementam o artigo [Sistemas operacionais com suporte para clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
-   Se você usa o Branch de Manutenção de Longo Prazo do Configuration Manager, consulte [Configurações com suporte para o Branch de Manutenção de Longo Prazo](/sccm/core/understand/supported-configurations-for-ltsb).

|Versão do Windows 10                    |  Configuration Manager 1702          |    Configuration Manager 1706 |Configuration Manager 1710          |  
|---------------------|-----|-----|-----|
|Enterprise 2015 LTSB                   |![Com suporte](media/green_check.png) |![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |
|Enterprise 2016 LTSB                   |![Com suporte](media/green_check.png) |![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |
|1607   <br />(Também conhecida como Anniversary Update)<br />(*consulte edições*)   |![Com suporte](media/green_check.png) |![Com suporte](media/green_check.png)            |![Com suporte](media/green_check.png) |
|1703   <br />(Também conhecida como Creators Update)<br />(*consulte edições*)      |![Compatível com versões anteriores](media/blue_compat.png) |![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |
|1709   <br />(Também conhecida como Fall Creators Update)<br />(*consulte edições*) |![Sem suporte](media/Red_X.png)   |![Compatível com versões anteriores](media/blue_compat.png) | ![Com suporte](media/green_check.png) |



**Edições:** Enterprise, Pro, Education, Pro Education   

|Chave|
|--|
|![Com suporte](media/green_check.png) = **Com suporte**  |
|![Sem suporte](media/blue_compat.png)  = **Compatível com versões anteriores** – Os recursos de gerenciamento de cliente existentes (inventário de hardware, inventário de software, atualizações de software, etc.) devem funcionar com a nova versão do Windows 10. Vamos documentar problemas conhecidos ou advertências. <br><br>Essa abordagem proporciona a capacidade de implantar e gerenciar novas compilações do Windows no primeiro dia com suporte para compatibilidade do aplicativo sem exigir uma nova versão de atualização do Configuration Manager. |
|![Com suporte](media/Red_X.png) = **Sem suporte**|


## <a name="windows-10-adk"></a>Windows ADK para Windows 10
Quando você implanta sistemas operacionais com o Configuration Manager, o [Windows ADK é uma dependência externa](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment) necessária.

A tabela a seguir enumera as versões do ADK do Windows 10 que você pode usar com as diferentes versões do Configuration Manager.

|Versão do ADK do Windows 10  |Configuration Manager 1702   |Configuration Manager 1706 |Configuration Manager 1710 |
|--------------------|-----|-----|-----|
|1607  |![Compatível com versões anteriores](media/blue_compat.png) |![Sem suporte](media/Red_X.png)| ![Sem suporte](media/Red_X.png) |
|1703  |![Com suporte](media/green_check.png)            |![Com suporte](media/green_check.png) | ![Compatível com versões anteriores](media/blue_compat.png)|
|1709  |![Sem suporte](media/Red_X.png)              |![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png)|

|Chave|
|--|
|![Com suporte](media/green_check.png) = **Com suporte** – O Windows recomenda o uso do Windows ADK que corresponde à versão do Windows que você está implantando. Por exemplo, use o Windows ADK para Windows 10 versão 1703 quando implantar o Windows 10 versão 1703. Para obter mais informações sobre a compatibilidade de componente do Windows ADK, consulte [Plataformas compatíveis com DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) e [Requisitos de USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
|![Compatível com versões anteriores](media/blue_compat.png)  = **Compatível com versões anteriores** – Não testamos essa combinação, mas ela deve funcionar. Vamos documentar problemas conhecidos ou advertências. |
|![Com suporte](media/Red_X.png) = **Sem suporte**|
