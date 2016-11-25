---
title: "Suporte à Virtualização | System Center Configuration Manager"
description: "Conheça os requisitos para instalar as funções de cliente e do sistema de sites do System Center Configuration Manager em um ambiente de virtualização."
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: be32ccee17bc4829888d42dfff3f2818f4fc2810


---
# <a name="support-for-virtualization-environments-for-system-center-configuration-manager"></a>Suporte para Ambientes de Virtualização do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Configuration Manager dá suporte à instalação de funções de cliente e do sistema de sites em sistemas operacionais com suporte que são executados como uma máquina virtual nos ambientes de virtualização a seguir. Este suporte existe mesmo quando não há suporte para o host da máquina virtual (ambiente de virtualização) como um cliente ou servidor do site.  

 **Por exemplo**, se você usar o Microsoft Hyper-V Server 2012 para hospedar uma máquina virtual que executa o Windows Server 2012, será possível instalar as funções do cliente ou do sistema de sites na máquina virtual (Windows Server 2012), mas não no host (Microsoft Hyper-V Server 2012).  

|Ambiente de virtualização|  
|--------------------------------|  
|Windows Server 2008 R2|  
|Microsoft Hyper-V Server 2008 R2|  
|Windows Server 2012|  
|Microsoft Hyper-V Server 2012|  
|Windows Server 2012 R2|  

 Cada computador virtual usado deve atender ou exceder a mesma configuração de hardware e software que seria usada para um computador físico do Configuration Manager.  

 É possível validar se seu ambiente de virtualização tem suporte no Configuration Manager por meio do Programa de Validação de Virtualização de Servidores e de seu Assistente da Política de Suporte do Programa Virtualização online. Para obter mais informações sobre o Programa de Validação de Virtualização de Servidores, consulte [Programa de Validação do Windows Server Virtualization](https://www.windowsservercatalog.com/svvp.aspx).  

> [!NOTE]  
>  O Configuration Manager não dá suporte a sistemas operacionais convidados com Virtual PC ou Servidor Virtual que são executados em um Mac.  

O Configuration Manager não pode gerenciar máquinas virtuais, a menos que elas estejam online. Uma imagem de máquina virtual offline não pode ser atualizada nem o inventário pode ser coletado por meio do cliente do Configuration Manager no computador host.  

Nenhuma consideração especial é fornecida para máquinas virtuais. Por exemplo, o Configuration Manager poderá não determinar se uma atualização deve ser aplicada novamente a uma imagem de máquina virtual se a máquina virtual for interrompida e reiniciada sem salvar o estado da máquina virtual à qual a atualização foi aplicada.  

##  <a name="a-namebkmkazurea-microsoft-azure-virtual-machines"></a><a name="bkmk_Azure"></a> Máquinas virtuais do Microsoft Azure  
 Há suporte para a execução do Configuration Manager em máquinas virtuais no Microsoft Azure, assim como quando ele é executado localmente na rede corporativa física. Você pode usar o Configuration Manager com as máquinas virtuais do Microsoft Azure nos seguintes cenários:  

-   **Cenário 1:** é possível executar o Configuration Manager em uma máquina virtual do Microsoft Azure e usá-lo para gerenciar os clientes instalados em outras máquinas virtuais do Microsoft Azure.  

-   **Cenário 2:** é possível executar o Configuration Manager em uma máquina virtual do Microsoft Azure e usá-lo para gerenciar os clientes que não são executados no Microsoft Azure.  

-   **Cenário 3:** você pode executar diferentes funções do sistema de sites do Configuration Manager em máquinas virtuais do Microsoft Azure durante a execução de outras funções em sua rede corporativa física (com conectividade de rede apropriada para comunicações).  

Os mesmos requisitos do System Center Configuration Manager para redes, configurações com suporte e requisitos de hardware que se aplicam ao instalar o Configuration Manager local em sua rede corporativa física também se aplicam à instalação no Microsoft Azure.  

> [!IMPORTANT]  
>  Os sites e os clientes do Configuration Manager executados em máquinas virtuais do Azure estão sujeitos aos mesmos requisitos de licença que as instalações locais.  



<!--HONumber=Nov16_HO1-->


