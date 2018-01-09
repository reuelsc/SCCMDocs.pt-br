---
title: "Substituir um computador existente e transferir configurações"
titleSuffix: Configuration Manager
description: "No Configuration Manager, escolha os métodos de implantação, como mídia inicializável, multicast ou Centro de Software, para substituir um computador existente por um novo."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d28f4363-9e8a-4c54-9cb7-0594fabfff26
caps.latest.revision: "6"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 862b3b8da0c1f9be0a5883c3f07b2759606d0fc1
ms.sourcegitcommit: 08f9854fb6c6d21e1e923b13e38a64d0bc2bc9a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/12/2017
---
# <a name="replace-an-existing-computer-and-transfer-settings-with-system-center-configuration-manager"></a>Substituir um computador existente e transferir configurações com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico fornece as etapas gerais no System Center Configuration Manager para substituir um computador existente por um novo. Para este cenário, é possível escolher entre vários métodos de implantação diferentes, como mídia inicializável, multicast ou o Centro de Software. Também é possível optar por instalar um ponto de migração de estado para armazenar as configurações e restaurá-las para o novo sistema operacional após a instalação. Se não tiver certeza de que esse é o cenário de implantação de sistema operacional certo para você, consulte [Cenários para implantar sistemas operacionais corporativos](scenarios-to-deploy-enterprise-operating-systems.md).  

 Use as seções a seguir para atualizar um computador existente com uma nova versão do Windows.  

##  <a name="BKMK_Plan"></a> Planoo  

-   **Planejar e implementar requisitos de infraestrutura**  

     Vários requisitos de infraestrutura devem estar em vigor antes que você possa implantar sistemas operacionais, como Windows ADK, USMT (Ferramenta de Migração do Usuário), WDS (Serviços de Implantação do Windows), configurações de disco rígido com suporte, etc. Para mais informações, consulte [Requisitos de infraestrutura para implantação do sistema operacional](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)  

-   **Instalar um ponto de migração de estado (necessário somente se você transferir as configurações)**  

     Quando você for capturar as configurações do computador existente e restaurá-las para o novo sistema operacional, é necessário instalar um ponto de migração de estado. Para mais informações, consulte [Ponto de migração de estado](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

##  <a name="BKMK_Configure"></a> Configurar  

1.  **Preparar uma imagem de inicialização**  

     Imagens de inicialização iniciam um computador em um ambiente do Windows PE (um sistema operacional mínimo com componentes e serviços limitados) que, em seguida, pode instalar um sistema operacional Windows completo no computador. Ao implantar sistemas operacionais, é necessário selecionar uma imagem de inicialização a ser usada e distribuir a imagem para um ponto de distribuição. Use o seguinte para preparar a imagem de inicialização:  

    -   Para saber mais sobre imagens de inicialização, consulte [Gerenciar imagens de inicialização](../get-started/manage-boot-images.md).  

    -   Para obter mais informações sobre como personalizar uma imagem de inicialização, consulte [Personalizar imagens de inicialização](../get-started/customize-boot-images.md).  

    -   Distribua a imagem de inicialização para pontos de distribuição. Para obter mais informações, consulte [Distribuir conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Preparar uma imagem do sistema operacional**  

     A imagem do sistema operacional contém os arquivos necessários para instalar o sistema operacional no computador de destino. Use o seguinte para preparar a imagem do sistema operacional:  

    -   Para saber mais sobre como criar uma imagem do sistema operacional, consulte [Gerenciar imagens do sistema operacional](../get-started/manage-operating-system-images.md).  

    -   Distribua a imagem do sistema operacional para pontos de distribuição. Para obter mais informações, consulte [Distribuir conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

3.  **Criar uma sequência de tarefas para implantar sistemas operacionais na rede**  

     Use uma sequência de tarefas para automatizar a instalação do sistema operacional na rede. Use as etapas em [Criar uma sequência de tarefas para instalar um sistema operacional](create-a-task-sequence-to-install-an-operating-system.md) para criar a sequência de tarefas para implantar o sistema operacional. Dependendo do método de implantação que você escolher, pode haver considerações adicionais para a sequência de tarefas.  

    > [!NOTE]  
    >  Nesse cenário, se você capturar e restaurar os arquivos e as configurações de usuário, será possível optar por usar um ponto de migração de estado ou salvar os arquivos localmente. Para mais informações, consulte [Gerenciar o estado do usuário](../get-started/manage-user-state.md).  

##  <a name="BKMK_Deploy"></a> Implantar  

-   Use um dos seguintes métodos de implantação para implantar o sistema operacional:  

    -   [Usar o Centro de Software para implantar o Windows pela rede](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [Use a mídia inicializável para implantar o Windows na rede](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [Usar multicast para implantar o Windows pela rede](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Criar uma imagem de um OEM na fábrica ou em um repositório local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

## <a name="monitor"></a>Monitor  

-   **Monitorar a implantação da sequência de tarefas**  

     Para monitorar a implantação da sequência de tarefas para instalar o sistema operacional, consulte [Monitorar implantações do sistema operacional](monitor-operating-system-deployments.md).  
