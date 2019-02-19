---
title: Usar multicast para implantar o Windows na rede
titleSuffix: Configuration Manager
description: Use o multicast em seu ambiente do System Center Configuration Manager para que vários computadores possam baixar a imagem do sistema operacional simultaneamente.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a256435c927c880363d20e6e52a22179a3271f3a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142367"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Usar o multicast para implantar o Windows pela rede com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O multicast é um método de otimização da rede que pode ser usado no ambiente do System Center Configuration Manager, no qual diversos clientes podem baixar a mesma imagem de sistema operacional ao mesmo tempo. Ao se usar multicast, vários computadores baixam simultaneamente a imagem do sistema operacional, pois ela é difundida via multicast pelo ponto de distribuição, em vez de ter um ponto de distribuição que envia uma cópia dos dados para cada cliente por meio de uma conexão separada.  

 Você pode implantar sistemas operacionais na rede usando multicast nos seguintes cenários de implantação de sistema operacional:  

- [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Instalar uma nova versão do Windows em um novo computador (sem sistema operacional)](install-new-windows-version-new-computer-bare-metal.md)  

  Conclua as etapas em um dos cenários de implantação de sistema operacional e use as seções a seguir para dar suporte a multicast.  

##  <a name="BKMK_Configure"></a> Configurar um ponto de distribuição para dar suporte a multicast  
 Para usar o multicast ao implantar sistemas operacionais, é necessário configurar um ponto de distribuição para dar suporte a multicast. Para mais informações, consulte [Configurar pontos de distribuição para dar suporte a multicast](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast).  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>Preparar uma imagem do sistema operacional para implantações multicast  
 Para configurar o pacote de imagens do sistema operacional para dar suporte a multicast, veja [Preparar a imagem do sistema operacional para implantações multicast](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).  

##  <a name="BKMK_Deploy"></a> Implantar a sequência de tarefas  
 Implantar o sistema operacional para uma coleção de destino. Para obter mais informações, consulte [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  
