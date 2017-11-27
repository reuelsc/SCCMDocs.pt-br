---
title: Suporte para Windows 10
titleSuffix: Configuration Manager
description: "Saiba mais sobre as versões do Windows 10 que têm suporte como clientes ou para OSD com o System Center Configuration Manager."
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: "5"
author: brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: aae4a3d504ea5dad901a6248cb219aff7a03b585
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="support-for-windows-10-for-system-center-configuration-manager"></a>Suporte para Windows 10 para System Center Configuration Manager  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


 Este tópico descreve as versões do Windows 10 que você pode usar com as diferentes versões do Branch Atual do System Center Configuration Manager. Isso inclui:
 -  Windows 10 como cliente do Configuration Manager.
 -  Windows ADK (Kit de Avaliação e Implantação do Windows) para Windows 10.

## <a name="windows-10-as-a-client"></a>Windows 10 como cliente
O Configuration Manager tenta fornecer suporte como cliente para cada versão nova do Windows 10 assim que ela fica disponível. Como os produtos têm agendas separadas de desenvolvimento e lançamento, o suporte que o Configuration Manager fornece depende de quando cada uma é disponibilizada.

Por exemplo, uma versão do Configuration Manager será removida da matriz após o fim do [suporte para essa versão](/sccm/core/servers/manage/current-branch-versions-supported). Da mesma forma, o suporte para as versões do Windows 10 como o Enterprise 2015 LTSB ou 1511 sairá da matriz quando for removido. Consulte [Sistemas operacionais preteridos](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems) para obter mais informações.

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
|![Sem suporte](media/blue_compat.png)  = **Compatível com versões anteriores** Isso significa que os recursos de gerenciamento de cliente existentes (inventário de hardware, inventário de software, atualizações de software, etc.) devem funcionar com a nova versão do Windows 10. Problemas conhecidos ou advertências serão documentados. <br><br>Essa abordagem proporciona a capacidade de implantar e gerenciar novas compilações do Windows no primeiro dia com suporte para compatibilidade do aplicativo sem exigir uma nova versão de atualização do Configuration Manager. |
|![Com suporte](media/Red_X.png) = **Sem suporte**|


## <a name="windows-10-adk"></a>Windows ADK para Windows 10
Quando você implanta sistemas operacionais com o Configuration Manager, o [Windows ADK é uma dependência externa](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment) necessária.

A tabela a seguir enumera as versões do Windows ADK para Windows 10 que você pode usar com as diferentes versões do Configuration Manager.

|Versão do ADK do Windows 10  |Configuration Manager 1702   |Configuration Manager 1706 |Configuration Manager 1710 |
|--------------------|-----|-----|-----|
|1607  |![Compatível com versões anteriores](media/blue_compat.png) |![Sem suporte](media/Red_X.png)| ![Sem suporte](media/Red_X.png) |
|1703  |![Com suporte](media/green_check.png)            |![Com suporte](media/green_check.png) | ![Compatível com versões anteriores](media/blue_compat.png)|
|1709  |![Sem suporte](media/Red_X.png)              |![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png)|

|Chave|
|--|
|![Com suporte](media/green_check.png) = **Com suporte** – O Windows recomenda o uso do Windows ADK que corresponde à versão do Windows que você está implantando. Por exemplo, use o Windows ADK para Windows 10 versão 1703 quando implantar o Windows 10 versão 1703.  |
|![Compatível com versões anteriores](media/blue_compat.png)  = **Compatível com versões anteriores** – Não testamos essa combinação, mas ela deve funcionar. Problemas conhecidos ou advertências serão documentados. |
|![Com suporte](media/Red_X.png) = **Sem suporte**|
