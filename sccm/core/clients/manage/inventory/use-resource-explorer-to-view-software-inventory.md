---
title: Exibir inventário de software com o Gerenciador de Recursos
titleSuffix: Configuration Manager
description: Usar o Gerenciador de Recursos para exibir o inventário de software no System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4aa4b118b87015389762ca4ec6ea79ba5ea2034f
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499654"
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-system-center-configuration-manager"></a>Como usar o Gerenciador de Recursos para exibir o inventário de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o Gerenciador de Recursos no System Center Configuration Manager para exibir informações sobre o inventário de software que foi coletado dos computadores em sua hierarquia.  

> [!NOTE]  
>  O Gerenciador de Recursos não exibirá dados de inventário até um ciclo de inventário de software tiver sido executado no cliente.  

 O Gerenciador de Recursos fornece as seguintes informações de inventário de software:  

-   **Software**:  

    -   **Arquivos Coletados** –arquivos que foram coletados durante o inventário de software.  

    -   **Detalhes do Arquivo** – arquivos que foram inventariados durante o inventário de software, mas que não estão associados a um fabricante nem a um produto específico.  

    -   **Última Verificação de Software** – data e hora do último inventário de software e da última coleta de arquivos no computador cliente.  

    -   **Detalhes do Produto** – produtos de software que foram inventariados pelo inventário de software, agrupados por fabricante.  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Para executar o Gerenciador de Recursos no console do Configuration Manager  

1.  No console do Configuration Manager, escolha **Ativos e Conformidade**

2.  No workspace **Ativos e Conformidade**, escolha **Dispositivos** ou abra uma coleção que exibe os dispositivos.  

3.  Escolha o computador que contém o inventário que você deseja exibir e, em seguida, na guia **Início** > grupo **Dispositivos**, escolha **Iniciar** > **Gerenciador de Recursos**.

4.  É possível clicar com o botão direito do mouse em qualquer item do painel direito da janela do Gerenciador de Recursos e escolher **Propriedades** para exibir as informações de inventário coletadas em um formato mais legível.  
 
