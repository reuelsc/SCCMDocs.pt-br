---
title: Suporte para Windows 10
titleSuffix: Configuration Manager
description: Saiba mais sobre as versões do Windows 10 compatíveis como clientes ou para implantação de sistema operacional com o System Center Configuration Manager
ms.date: 10/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 67a25cc788c417409306e506de97cb0fdf1cf2e8
ms.sourcegitcommit: 265d38d55ca0db043e3a7131a56f123e1d98aa5b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/03/2018
ms.locfileid: "48236133"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Suporte para Windows 10 no Configuration Manager  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Saiba mais sobre as versões do Windows 10 compatíveis com o Configuration Manager, incluindo:
 -  [Windows 10 como um cliente do Configuration Manager](#windows-10-as-a-client)
 -  [O ADK (Kit de Avaliação e Implantação do Windows) para Windows 10](#windows-10-adk)

> [!Tip]
> Há suporte para builds do Windows Server como um cliente da mesma maneira que com a versão do Windows 10 associada. Por exemplo, o Windows Server 2016 tem a merma versão de build do Windows 10 LTSB 2016 e o Windows Server versão 1803 tem a mesma versão de build do Windows 10 versão 1803.
> 
> Para obter mais informações sobre o Windows Server como um sistema de sites, confira [Sistemas operacionais com suporte para servidores de sistema de sites do Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers#the-server-core-installation-of-windows-server-version-1803).



## <a name="windows-10-as-a-client"></a>Windows 10 como cliente

O Configuration Manager tenta fornecer suporte como um cliente para cada nova versão do Windows 10, assim que ela fica disponível. Como os produtos têm agendas separadas de desenvolvimento e lançamento, o suporte que o Configuration Manager fornece depende de quando cada uma é disponibilizada.

Uma versão do Configuration Manager é removida da matriz após o fim do [suporte para essa versão](/sccm/core/servers/manage/current-branch-versions-supported). Da mesma forma, o suporte para as versões do Windows 10, como a Enterprise 2015 LTSB ou 1511, é removido da matriz quando elas são removidas do suporte.

-   A versão mais recente do branch atual do Configuration Manager recebe atualizações críticas e de segurança, que podem incluir correções para problemas com versões do Windows 10. Quando a Microsoft lança uma nova versão do branch atual do Configuration Manager, as versões anteriores só recebem atualizações de segurança. Para obter mais informações, confira [Suporte para versões do branch atual do System Center Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).  

    > [!Note]  
    > A melhor maneira de manter o Windows 10 atualizado é manter o Configuration Manager em dia. Para obter mais informações, confira [Configuration Manager e Windows como um serviço](/sccm/core/understand/configuration-manager-and-windows-as-service).  

-   As informações a seguir complementam o artigo [Sistemas operacionais com suporte para clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).  

-   Se você usa o branch de manutenção em longo prazo do Configuration Manager, veja [Configurações com suporte para o branch de manutenção em longo prazo](/sccm/core/understand/supported-configurations-for-ltsb).  

<br/>
A tabela a seguir enumera as versões do Windows 10 que você pode usar, como cliente, com as diferentes versões do Configuration Manager.

| Versão do Windows 10 | Configuration Manager 1710 | Configuration Manager 1802 | Configuration Manager 1806 |
|---------------------|-----|-----|-----|-----|
| Enterprise 2015 LTSB            <!--10/14/2025-->   | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |
| Enterprise 2016 LTSB            <!--10/13/2026-->   | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |
| 1607   <!--04/09/2019-->   | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |
| 1703   <!--10/08/2019-->   | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |
| 1709   <!--04/14/2020-->   | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |
| 1803   <!--11/10/2020-->   | ![Sem suporte](media/Red_X.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |
| 1809   <!--04/12/2021?-->   | ![Sem suporte](media/Red_X.png) | ![Sem suporte](media/Red_X.png) | ![Com suporte](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

> [!Note]  
> O suporte para versões de canal semestrais do Windows 10 inclui as seguintes edições: Enterprise, Pro, Education e Pro Education.   

| Chave |
|--|
| ![Com suporte](media/green_check.png) = **Com suporte**  |
| ![Não compatível](media/Red_X.png) = **Not supported** |

 > [!NOTE]  
 > A partir da versão 1802, o Configuration Manager dá suporte ao cliente em dispositivos Windows 10 ARM64. Os recursos existentes de gerenciamento de clientes devem funcionar com esses novos dispositivos. Por exemplo, inventário de hardware e software, atualizações de software e gerenciamento de aplicativos. A implantação de sistema operacional não tem suporte atualmente. <!-- 1353704 --> 

Para obter mais informações sobre o ciclo de vida do Windows, confira a [folha de fatos sobre o ciclo de vida do Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)



## <a name="windows-10-adk"></a>Windows ADK para Windows 10

Quando você implanta sistemas operacionais com o Configuration Manager, o Windows ADK é uma dependência externa necessária. Para obter mais informações, confira [Requisitos de infraestrutura para implantação do sistema operacional](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment#windows-adk-for-windows-10).

A tabela a seguir enumera as versões do ADK do Windows 10 que você pode usar com as diferentes versões do Configuration Manager.

| Versão do ADK do Windows 10  | Configuration Manager 1710 | Configuration Manager 1802 | Configuration Manager 1806 |
|--------------------|-----|-----|-----|-----|
| 1703  | ![Compatível com versões anteriores](media/blue_compat.png) | ![Compatível com versões anteriores](media/blue_compat.png) | ![Sem suporte](media/Red_X.png)   |
| 1709  | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) | ![Compatível com versões anteriores](media/blue_compat.png) |
| 1803  | ![Sem suporte](media/Red_X.png) | ![Com suporte](media/green_check.png) | ![Com suporte](media/green_check.png) |
| 1809  | ![Sem suporte](media/Red_X.png) | ![Sem suporte](media/Red_X.png) | ![Com suporte](media/green_check.png) |

|Chave|
|--|
| ![Com suporte](media/green_check.png) = **Com suporte** <br/> A Microsoft recomenda o uso do Windows ADK que corresponde à versão do Windows que você está implantando. Por exemplo, use o Windows ADK para Windows 10 versão 1703 quando implantar o Windows 10 versão 1703. Para obter mais informações sobre a compatibilidade de componente do Windows ADK, consulte [Plataformas compatíveis com DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) e [Requisitos de USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
| ![Compatível com versões anteriores](media/blue_compat.png)  = **compatível com versões anteriores** <br/> Essa combinação não foi testada, mas deve funcionar. Documentaremos quaisquer problemas ou advertências conhecidos. |
| ![Não compatível](media/Red_X.png) = **Not supported** |

 > [!Note]  
 > O Configuration Manager é compatível apenas com os componentes x86 e amd64 do Windows 10 ADK. Atualmente, ele não dá suporte aos componentes ARM ou ARM64. 

> [!Tip]
> Os builds do Windows Server têm o mesmo requisito do Windows ADK que a versão do Windows 10 associada. Por exemplo, o Windows Server 2016 é a mesma versão de build do Windows 10 LTSB 2016.
