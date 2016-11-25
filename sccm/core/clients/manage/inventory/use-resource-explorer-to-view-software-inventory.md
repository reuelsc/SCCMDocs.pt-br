---
title: "Exibir o inventário de software | Gerenciador de Recursos | System Center Configuration Manager"
description: "Usar o Gerenciador de Recursos para exibir o inventário de software no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b4ecb27cfb119ae80d1ed7d90d84c61a87b183c8


---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-system-center-configuration-manager"></a>Como usar o Gerenciador de Recursos para exibir o inventário de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o Gerenciador de Recursos no System Center Configuration Manager para exibir informações sobre o inventário de software que foi coletado dos computadores em sua hierarquia.  

> [!NOTE]  
>  O Gerenciador de Recursos não exibirá dados de inventário até que um ciclo de inventário de software seja executado no cliente ao qual você está se conectando.  

 O Gerenciador de Recursos no Configuration Manager contém as seguintes seções relacionadas ao inventário de software:  

-   **Software** – A seção de software do Gerenciador de Recursos contém quatro seções:  

    -   **Arquivos Coletados** – Exibe informações sobre os arquivos que foram coletados durante o inventário de software.  

    -   **Detalhes do Arquivo** – exibe informações sobre os arquivos que foram inventariados durante o inventário de software, mas que não estão associados a um fabricante ou produto específico.  

    -   **Última Verificação de Software** – Exibe a data e hora do último inventário de software e a coleta de arquivos que foi executada no computador cliente.  

    -   **Detalhes do Produto** – Exibe informações sobre os produtos de software que foram inventariados pelo inventário de software, agrupados por fabricante.  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Para executar o Gerenciador de Recursos no console do Configuration Manager  
 Use o procedimento a seguir para executar o Gerenciador de Recursos no Configuration Manager.  

#### <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Para executar o Gerenciador de Recursos no console do Configuration Manager  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Dispositivos** ou abra qualquer coleção que exiba dispositivos.  

3.  Clique no computador que contém o inventário que você deseja exibir e, na guia **Início** , no grupo **Dispositivos** , clique em **Iniciar** e em **Gerenciador de Recursos**. A janela **Gerenciador de Recursos** será aberta.  

4.  Você pode clicar com o botão direito do mouse em qualquer item no painel direito da janela do Gerenciador de Recursos e clicar em **Propriedades** para abrir a caixa de diálogo *Propriedades\>***do <nome do item**, que pode ajudar você a exibir as informações de inventário coletadas em um formato mais legível.  

5.  Quando tiver terminado, feche a janela **Gerenciador de Recursos** .  



<!--HONumber=Nov16_HO1-->


