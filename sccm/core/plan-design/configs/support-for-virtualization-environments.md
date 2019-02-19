---
title: Suporte para virtualização
titleSuffix: Configuration Manager
description: Os requisitos para instalar as funções de cliente e do sistema de sites do Configuration Manager em um ambiente de virtualização.
ms.date: 01/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6a2200a72330fab2f0584c419e6b66b2fc25c44b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135595"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Suporte para ambientes de virtualização com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Configuration Manager oferece suporte à instalação de funções de cliente e do sistema de sites em sistemas operacionais compatíveis que são executados como uma máquina virtual nos ambientes de virtualização deste artigo. Este suporte existe mesmo quando não há suporte para o host da máquina virtual (ambiente de virtualização) como um cliente ou servidor de sites.  

Por exemplo, use o Microsoft Hyper-V Server 2012 para hospedar uma máquina virtual que executa o Windows Server 2012. Você pode instalar as funções de cliente ou de sistema de sites na máquina virtual que está executando o Windows Server 2012. Não é possível instalar o cliente no host que está executando o Microsoft Hyper-V Server 2012.  


## <a name="virtualization-environments"></a>Ambientes de virtualização

- Windows Server 2019  
- Windows Server 2016 <sup>[Observação 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup>[Observação 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  
- Microsoft Hyper-V Server 2008 R2  
- Windows Server 2008 R2  

#### <a name="bkmk_note1"></a> Observação 1: Virtualização aninhada
O Configuration Manager não oferece suporte à [virtualização aninhada](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#BKMK_nested), que é nova no Windows Server 2016.


### <a name="virtualization-environment-support"></a>Suporte ao ambiente de virtualização

Cada computador virtual usado deve atender ou exceder os requisitos de hardware e software usados para um computador físico com Configuration Manager.  

Para confirmar se o seu ambiente de virtualização tem suporte no Configuration Manager use o Programa de Validação de Virtualização de Servidores. Ele inclui um Assistente de Política de Suporte do Programa de Virtualização online. Para saber mais, consulte [Programa de Validação de Virtualização de Servidores do Windows](https://www.windowsservercatalog.com/svvp.aspx).  

> [!NOTE]  
> O Configuration Manager não oferece suporte a sistemas operacionais convidados com Virtual PC ou Servidor Virtual que são executados em computadores Mac.  

O Configuration Manager não pode gerenciar máquinas virtuais se elas estiverem offline. Uma imagem de máquina virtual offline não pode ser atualizada, nem o inventário pode ser coletado por meio do cliente do Configuration Manager no computador host.  

Nenhuma consideração especial é fornecida para máquinas virtuais. Por exemplo, o Configuration Manager pode não determinar se uma atualização deve ser aplicada novamente a uma imagem de máquina virtual caso a máquina virtual tenha sido interrompida e reiniciada sem salvar o estado da máquina virtual à qual a atualização foi aplicada.  



##  <a name="bkmk_Azure"></a> Máquinas virtuais do Microsoft Azure  

O Configuration Manager pode ser executado em máquinas virtuais no Azure da mesma forma que é executado localmente dentro do seu data center. Use o Configuration Manager com máquinas virtuais do Azure nos seguintes cenários:  

- **Cenário 1**: execute o Configuration Manager em uma máquina virtual do Azure. Use-o para gerenciar clientes em outras máquinas virtuais do Azure.  

- **Cenário 2**: execute o Configuration Manager em uma máquina virtual do Azure. Use-o para gerenciar clientes que não estejam em execução no Azure.  

- **Cenário 3**: execute diferentes funções do sistema de sites do Configuration Manager em máquinas virtuais do Azure. Execute outras funções em seu data center local conectado corretamente ao Azure.  

Os mesmos requisitos do Configuration Manager para redes, configurações compatíveis e requisitos de hardware que se aplicam ao instalá-lo localmente também se aplicam à instalação em máquinas virtuais do Azure.  

Para saber mais, consulte [Configuration Manager no Azure](/sccm/core/understand/configuration-manager-on-azure).

> [!IMPORTANT]  
> Os sites e os clientes do Configuration Manager executados em máquinas virtuais do Azure estão sujeitos aos mesmos requisitos de licença que as instalações locais.  
