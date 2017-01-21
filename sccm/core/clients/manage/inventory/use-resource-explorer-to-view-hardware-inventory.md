---
title: "Exibir inventário de hardware| Microsoft Docs | Gerenciador de Recursos"
description: "Usar o Gerenciador de Recursos para exibir o inventário de hardware no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
caps.latest.revision: 7
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 2cd138b3bbb437d84f0ff7c2aeef869518bd817d


---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-system-center-configuration-manager"></a>Como usar o Gerenciador de Recursos para exibir o inventário de hardware no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o Gerenciador de Recursos no System Center Configuration Manager para exibir informações sobre o inventário de hardware que foi coletado dos clientes em sua hierarquia.  

> [!NOTE]  
>  Gerenciador de recursos não exibirá nenhum inventário dados até que um ciclo de inventário de hardware tenha executado no cliente que você estão se conectando.  

 O Gerenciador de Recursos no Configuration Manager contém as seguintes seções relacionadas ao inventário de hardware:  

-   **Hardware** ‑ Contém o inventário de hardware mais recente coletado especificado do dispositivo cliente do Configuration Manager. Você pode examinar o item de estoque **Status de estação de trabalho** para descobrir a hora e data em que o dispositivo executado pela última vez um inventário de hardware.  

-   **Histórico de hardware** – Contém um histórico de inventariado itens que foram alterados desde o último inventário de hardware foi executado. Cada item da lista contém um nó **Atual** e um ou mais nós de *<data\>*. Você pode comparar as informações do nó atual para um de nós do históricos para descobrir os itens que foram alterados no inventário de hardware de computadores cliente.  

    > [!NOTE]  
    >  O Configuration Manager retém o histórico de inventário de hardware para o número de dias que você especificar na tarefa de manutenção do site **Excluir históricos de inventários antigos**  

> [!NOTE]  
>  Para obter informações sobre como exibir o inventário de hardware de clientes que executam Linux e UNIX, veja [How to monitor clients for Linux and UNIX servers in System Center Configuration Manager](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md).  

### <a name="how-to-run-resource-explorer-from-the-configuration-manager-console"></a>Como executar o Gerenciador de Recursos no console do Configuration Manager  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Dispositivos** ou abra qualquer coleção que exiba dispositivos.  

3.  Clique no computador que contém o inventário que você deseja exibir e, na guia **Início** , no grupo **Dispositivos** , clique em **Iniciar** e em **Gerenciador de Recursos**. O **Resource Explorer** janela será aberta.  

4.  Você pode clicar com o botão direito do mouse em qualquer item no painel direito da janela do **Gerenciador de Recursos** e clicar em **Propriedades** para abrir a caixa de diálogo *Propriedades\>***do <nome do item**, que pode ajudar você a exibir as informações de inventário coletadas em um formato mais legível.  

5.  Quando tiver terminado, feche a janela **Gerenciador de Recursos** .  



<!--HONumber=Dec16_HO3-->


