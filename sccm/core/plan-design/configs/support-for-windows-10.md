---
title: Suporte para Windows 10
titleSuffix: Configuration Manager
description: Saiba mais sobre as versões do Windows 10 compatíveis como clientes ou para implantação de sistema operacional com o System Center Configuration Manager
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f5aac395c71b76a0b83826e8f7c9de1e656aa884
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383626"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Suporte para Windows 10 no Configuration Manager  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Saiba mais sobre as versões do Windows 10 compatíveis com o Configuration Manager, incluindo:
 -  [Windows 10 como um cliente do Configuration Manager](#windows-10-as-a-client)
 -  [O ADK (Kit de Avaliação e Implantação do Windows) para Windows 10](#windows-10-adk)



## <a name="windows-10-as-a-client"></a>Windows 10 como cliente
O Configuration Manager tenta fornecer suporte como um cliente para cada nova versão do Windows 10, assim que ela fica disponível. Como os produtos têm agendas separadas de desenvolvimento e lançamento, o suporte que o Configuration Manager fornece depende de quando cada uma é disponibilizada.

Por exemplo, uma versão do Configuration Manager é removida da matriz após o fim do [suporte para essa versão](/sccm/core/servers/manage/current-branch-versions-supported). Da mesma forma, o suporte para as versões do Windows 10, como a Enterprise 2015 LTSB ou 1511, sai da matriz quando elas são removidas do suporte. Para obter mais informações, consulte [Sistemas operacionais preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems).

-   As informações a seguir complementam o artigo [Sistemas operacionais com suporte para clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).  

-   Se você usa o branch de manutenção em longo prazo do Configuration Manager, veja [Configurações com suporte para o branch de manutenção em longo prazo](/sccm/core/understand/supported-configurations-for-ltsb).  

<br/>
A tabela a seguir enumera as versões do Windows 10 que você pode usar, como cliente, com as diferentes versões do Configuration Manager.

| Versão do Windows 10 | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802 | Configuration Manager 1806 |
|---------------------|-----|-----|-----|-----|
| Enterprise 2015 LTSB            <!--10/14/2025-->   | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |
| Enterprise 2016 LTSB            <!--10/13/2026-->   | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |
| 1607   <br />(*consulte as edições*)   <!--04+6/10/2018-->   | ![Com suporte](media/green_check.png) <sup>1</sup> | ![Com suporte](media/green_check.png) <sup>1</sup> | ![Com suporte](media/green_check.png) <sup>1</sup> | ![Com suporte](media/green_check.png) <sup>1</sup> |
| 1703   <br />(*consulte as edições*)   <!--10+6/09/2018-->   | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |
| 1709   <br />(*consulte as edições*)   <!--04+6/09/2019-->   | ![Compatível com versões anteriores](media/blue_compat.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |
| 1803   <br />(*consulte as edições*)   <!--11/12/2019-->   | ![Sem suporte](media/Red_X.png) | ![Sem suporte](media/Red_X.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

**Edições**: Enterprise, Pro, Education, Pro Education   

<sup>1</sup> Para obter mais informações, veja [Folha de fatos de ciclo de vida do Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet) e a seção sobre "Extensão de manutenção para as edições Enterprise e Education".

| Chave |
|--|
| ![Com suporte](media/green_check.png) = **Com suporte**  |
| ![Compatibilidade com versões anteriores](media/blue_compat.png)  = **Compatibilidade com versões anteriores** <br/> Os recursos existentes de gerenciamento de clientes devem funcionar com essa nova versão do Windows 10. Por exemplo, inventário de hardware, inventário de software e atualizações de software. Vamos documentar problemas conhecidos ou advertências. <br><br>Essa abordagem proporciona a capacidade de implantar e gerenciar novas versões do Windows imediatamente com suporte para compatibilidade do aplicativo, sem a necessidade de uma nova versão de atualização do Configuration Manager. |
| ![Não compatível](media/Red_X.png) = **Not supported** |

 > [!NOTE]  
 > A partir da versão 1802, o Configuration Manager dá suporte ao cliente em dispositivos Windows 10 ARM64. Os recursos existentes de gerenciamento de clientes devem funcionar com esses novos dispositivos. Por exemplo, inventário de hardware e software, atualizações de software e gerenciamento de aplicativos. A implantação de sistema operacional não tem suporte atualmente. <!-- 1353704 --> 



## <a name="windows-10-adk"></a>Windows ADK para Windows 10
Quando você implanta sistemas operacionais com o Configuration Manager, o [Windows ADK é uma dependência externa](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment) necessária.

A tabela a seguir enumera as versões do ADK do Windows 10 que você pode usar com as diferentes versões do Configuration Manager.

| Versão do ADK do Windows 10  | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802 | Configuration Manager 1806 |
|--------------------|-----|-----|-----|-----|
| 1703  | ![Com suporte](media/green_check.png) | ![Compatível com versões anteriores](media/blue_compat.png) | ![Compatível com versões anteriores](media/blue_compat.png) | ![Sem suporte](media/Red_X.png)   |
| 1709  | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Compatível com versões anteriores](media/blue_compat.png) |
| 1803  | ![Sem suporte](media/Red_X.png)   | ![Sem suporte](media/Red_X.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |

|Chave|
|--|
| ![Com suporte](media/green_check.png) = **Com suporte** <br/> A Microsoft recomenda o uso do Windows ADK que corresponde à versão do Windows que você está implantando. Por exemplo, use o Windows ADK para Windows 10 versão 1703 quando implantar o Windows 10 versão 1703. Para obter mais informações sobre a compatibilidade de componente do Windows ADK, consulte [Plataformas compatíveis com DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) e [Requisitos de USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
| ![Compatível com versões anteriores](media/blue_compat.png)  = **compatível com versões anteriores** <br/> Essa combinação não foi testada, mas deve funcionar. Vamos documentar problemas conhecidos ou advertências. |
| ![Não compatível](media/Red_X.png) = **Not supported** |

 > [!Note]  
 > O Configuration Manager é compatível apenas com os componentes x86 e amd64 do Windows 10 ADK. Atualmente, ele não dá suporte aos componentes ARM ou ARM64. 
