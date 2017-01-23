---
title: "Suporte para virtualização | Microsoft Docs"
description: "Conheça os requisitos para instalar as funções de cliente e do sistema de sites do System Center Configuration Manager em um ambiente de virtualização."
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10192da2633555ab3bae60dbb1156d1926f9a4a0
ms.openlocfilehash: b49bd179da850cee35b2487a353bb1788df03d58


---
# <a name="support-for-virtualization-environments-for-system-center-configuration-manager"></a>Suporte para ambientes de virtualização do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Configuration Manager dá suporte à instalação de funções de cliente e do sistema de sites em sistemas operacionais com suporte que são executados como uma máquina virtual nos ambientes de virtualização listados neste artigo. Este suporte existe mesmo quando não há suporte para o host da máquina virtual (ambiente de virtualização) como um cliente ou servidor do site.  

 Por exemplo, se você usar o Microsoft Hyper-V Server 2012 para hospedar uma máquina virtual que executa o Windows Server 2012, será possível instalar as funções do cliente ou do sistema de sites na máquina virtual (Windows Server 2012), mas não no host (Microsoft Hyper-V Server 2012).  

|Ambiente de virtualização|  
|--------------------------------|  
|Windows Server 2008 R2|  
|Microsoft Hyper-V Server 2008 R2|  
|Windows Server 2012|  
|Microsoft Hyper-V Server 2012|  
|Windows Server 2012 R2|
|Windows Server 2016 <sup>(consulte a *observação 1*)</sup>|
|Microsoft Hyper-V Server 2016 <sup>(consulte a *observação 1*)|
-  *Observação 1*: o Configuration Manager não dá suporte à [virtualização aninhada](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/what-s-new-in-hyper-v-on-windows#a-namebkmknestedanested-virtualization-new), que é uma novidade no Windows Server 2016.


 Cada computador virtual usado deve atender ou exceder aos mesmos requisitos de hardware e software que seriam usados para um computador físico do Configuration Manager.  

 É possível validar se seu ambiente de virtualização tem suporte no Configuration Manager por meio do Programa de Validação de Virtualização de Servidores e de seu Assistente da Política de Suporte do Programa Virtualização online. Para obter mais informações sobre o Programa de Validação de Virtualização de Servidores, consulte [Programa de Validação do Windows Server Virtualization](https://www.windowsservercatalog.com/svvp.aspx).  

> [!NOTE]  
>  O Configuration Manager não dá suporte a sistemas operacionais convidados com Virtual PC ou Servidor Virtual que são executados em computadores Mac.  

O Configuration Manager não pode gerenciar máquinas virtuais, a menos que elas estejam online. Uma imagem de máquina virtual offline não pode ser atualizada nem o inventário pode ser coletado por meio do cliente do Configuration Manager no computador host.  

Nenhuma consideração especial é fornecida para máquinas virtuais. Por exemplo, o Configuration Manager poderá não determinar se uma atualização deve ser aplicada novamente a uma imagem de máquina virtual se a máquina virtual tiver sido interrompida e reiniciada sem salvar o estado da máquina virtual à qual a atualização foi aplicada.  

##  <a name="a-namebkmkazurea-microsoft-azure-virtual-machines"></a><a name="bkmk_Azure"></a> Máquinas virtuais do Microsoft Azure  
 O Configuration Manager pode ser executado em máquinas virtuais no Azure da mesma forma que é executado localmente dentro da rede corporativa física. Você pode usar o Configuration Manager com as máquinas virtuais do Azure nos seguintes cenários:  

-   **Cenário 1:** é possível executar o Configuration Manager em uma máquina virtual do Azure e usá-lo para gerenciar os clientes instalados em outras máquinas virtuais do Azure.  

-   **Cenário 2:** é possível executar o Configuration Manager em uma máquina virtual do Azure e usá-lo para gerenciar clientes que não estão sendo executados no Azure.  

-   **Cenário 3:** é possível executar diferentes funções do sistema de sites do Configuration Manager em máquinas virtuais do Azure durante a execução de outras funções em sua rede corporativa física (com conectividade de rede apropriada para comunicações).  

Os mesmos requisitos do System Center Configuration Manager para redes, configurações com suporte e requisitos de hardware que se aplicam ao instalar o Configuration Manager localmente em sua rede corporativa física também se aplicam à instalação em máquinas virtuais do Azure.  

Para mais informações, consulte [Configuration Manager no Azure – Perguntas frequentes](/sccm/core/understand/configuration-manager-on-azure).

> [!IMPORTANT]  
>  Os sites e os clientes do Configuration Manager executados em máquinas virtuais do Azure estão sujeitos aos mesmos requisitos de licença que as instalações locais.  



<!--HONumber=Jan17_HO2-->


