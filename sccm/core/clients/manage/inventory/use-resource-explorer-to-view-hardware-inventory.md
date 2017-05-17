---
title: "Exibir inventário de hardware| Microsoft Docs | Gerenciador de Recursos"
description: "Usar o Gerenciador de Recursos para exibir o inventário de hardware no System Center Configuration Manager."
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
caps.latest.revision: 7
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 05c27c7aa36e0b4236867766dab36125c31467b3
ms.openlocfilehash: 6265ee70b70a715862b1651d2f3760bef096ee8a
ms.contentlocale: pt-br
ms.lasthandoff: 01/03/2017


---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-system-center-configuration-manager"></a>Como usar o Gerenciador de Recursos para exibir o inventário de hardware no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o Gerenciador de Recursos no System Center Configuration Manager para exibir informações sobre o inventário de hardware que foi coletado dos clientes em sua hierarquia.  

> [!NOTE]  
>  Gerenciador de recursos não exibirá nenhum inventário dados até que um ciclo de inventário de hardware tenha executado no cliente que você estão se conectando.  

 O Gerenciador de Recursos contém as seguintes seções relacionadas ao inventário de hardware:  

-   **Hardware** – contém o inventário de hardware mais recente coletado do dispositivo cliente especificado.  **Status da Estação de Trabalho** contém a hora e data em que o dispositivo executou um inventário de hardware pela última vez.  

-   **Histórico de Hardware** – contém um histórico de itens inventariados que foram alterados desde a execução do último inventário de hardware. Cada item contém um nó **Atual** e um ou mais nós de *<data\>*. É possível comparar as informações do nó atual com um dos nós históricos para descobrir itens que foram alterados.  

    > [!NOTE]  
    >  O Configuration Manager retém o histórico de inventário de hardware para o número de dias que você especificar na tarefa de manutenção do site **Excluir históricos de inventários antigos**  

> [!NOTE]  
>  Para obter informações sobre como exibir o inventário de hardware de clientes que executam Linux e UNIX, veja [How to monitor clients for Linux and UNIX servers in System Center Configuration Manager](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md).  

### <a name="how-to-run-resource-explorer-from-the-configuration-manager-console"></a>Como executar o Gerenciador de Recursos no console do Configuration Manager  

1.  No console do Configuration Manager, escolha **Ativos e Conformidade** > **Dispositivos** ou abra uma coleção que exibe os dispositivos.  

3.  Escolha o computador que contém o inventário que você deseja exibir e, em seguida, na guia **Início** > grupo **Dispositivos**, escolha **Iniciar** >  **Gerenciador de Recursos**.   

4.  Clique com o botão direito do mouse em qualquer item do painel direito da janela **Gerenciador de Recursos** e escolha **Propriedades** para abrir a caixa de diálogo *Propriedades do <nome do item\>***** para exibir as informações de inventário coletadas em um formato mais legível.  


