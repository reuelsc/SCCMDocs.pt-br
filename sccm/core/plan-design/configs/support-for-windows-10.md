---
title: Suporte para Windows 10
titleSuffix: Configuration Manager
description: Saiba mais sobre as versões do Windows 10 compatíveis como clientes ou para implantação de sistema operacional com o System Center Configuration Manager
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: 5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 877732c4095438b19a863335a4a0026b7b088b24
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2018
---
# <a name="support-for-windows-10-in-system-center-configuration-manager"></a>Suporte para o Windows 10 no System Center Configuration Manager  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Saiba mais sobre as versões do Windows 10 compatíveis com o Configuration Manager, incluindo:
 -  Windows 10 como um cliente do Configuration Manager
 -  O ADK (Kit de Avaliação e Implantação do Windows) para Windows 10

## <a name="windows-10-as-a-client"></a>Windows 10 como cliente
O Configuration Manager tenta fornecer suporte como um cliente para cada nova versão do Windows 10, assim que ela fica disponível. Como os produtos têm agendas separadas de desenvolvimento e lançamento, o suporte que o Configuration Manager fornece depende de quando cada uma é disponibilizada.

Por exemplo, uma versão do Configuration Manager é removida da matriz após o fim do [suporte para essa versão](/sccm/core/servers/manage/current-branch-versions-supported). Da mesma forma, o suporte para as versões do Windows 10, como a Enterprise 2015 LTSB ou 1511, sai da matriz quando elas são removidas do suporte. Para obter mais informações, consulte [Sistemas operacionais preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems).


-   As informações a seguir complementam o artigo [Sistemas operacionais com suporte para clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
-   Se você usa o Branch de Manutenção de Longo Prazo do Configuration Manager, consulte [Configurações com suporte para o Branch de Manutenção de Longo Prazo](/sccm/core/understand/supported-configurations-for-ltsb).

| Versão do Windows 10 | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802 |
|---------------------|-----|-----|-----|
| Enterprise 2015 LTSB            <!--10/14/2025-->   | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |
| Enterprise 2016 LTSB            <!--10/13/2026-->   | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |
| 1607   <br />(*consulte as edições*)   <!--04/10/2018-->   | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |
| 1703   <br />(*consulte as edições*)   <!--10/09/2018-->   | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |
| 1709   <br />(*consulte as edições*)   <!--04/09/2019-->   | ![Compatível com versões anteriores](media/blue_compat.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

**Edições:** Enterprise, Pro, Education, Pro Education   

|Chave|
|--|
|![Com suporte](media/green_check.png) = **Com suporte**  |
|![Compatível com versões anteriores](media/blue_compat.png)  = **Backwards compatible** – os recursos de gerenciamento de clientes existentes devem funcionar com a nova versão do Windows 10. Por exemplo, inventário de hardware, inventário de software e atualizações de software. Vamos documentar problemas conhecidos ou advertências. <br><br>Essa abordagem proporciona a capacidade de implantar e gerenciar novas versões do Windows imediatamente com suporte para compatibilidade do aplicativo, sem a necessidade de uma nova versão de atualização do Configuration Manager. |
|![Não compatível](media/Red_X.png) = **Not supported**|

 > [!NOTE]
 > A partir da versão 1802, o Configuration Manager dá suporte ao cliente em dispositivos Windows 10 ARM64. Os recursos existentes de gerenciamento de clientes devem funcionar com esses novos dispositivos. Por exemplo, inventário de hardware e software, atualizações de software e gerenciamento de aplicativos. A implantação de sistema operacional atualmente não tem suporte. <!-- 1353704 --> 



## <a name="windows-10-adk"></a>Windows ADK para Windows 10
Quando você implanta sistemas operacionais com o Configuration Manager, o [Windows ADK é uma dependência externa](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment) necessária.

A tabela a seguir enumera as versões do ADK do Windows 10 que você pode usar com as diferentes versões do Configuration Manager.

| Versão do ADK do Windows 10  | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802   |
|--------------------|-----|-----|-----|
| 1607  | ![Sem suporte](media/Red_X.png)   | ![Sem suporte](media/Red_X.png) | ![Sem suporte](media/Red_X.png) |
| 1703  | ![Com suporte](media/green_check.png) | ![Compatível com versões anteriores](media/blue_compat.png) | ![Compatível com versões anteriores](media/blue_compat.png) |
| 1709  | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |

|Chave|
|--|
|![Com suporte](media/green_check.png) = **Com suporte** – O Windows recomenda o uso do Windows ADK que corresponde à versão do Windows que você está implantando. Por exemplo, use o Windows ADK para Windows 10 versão 1703 quando implantar o Windows 10 versão 1703. Para obter mais informações sobre a compatibilidade de componente do Windows ADK, consulte [Plataformas compatíveis com DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) e [Requisitos de USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
|![Compatível com versões anteriores](media/blue_compat.png)  = **Compatível com versões anteriores** – Não testamos essa combinação, mas ela deve funcionar. Vamos documentar problemas conhecidos ou advertências. |
|![Não compatível](media/Red_X.png) = **Not supported**|

 > [!Note]
 > O Configuration Manager é compatível apenas com os componentes x86 e amd64 do Windows 10 ADK. Atualmente, ele não dá suporte aos componentes arm ou arm64. 