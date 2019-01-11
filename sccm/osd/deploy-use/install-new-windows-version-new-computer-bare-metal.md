---
title: Instalar o Windows em um novo computador
titleSuffix: Configuration Manager
description: Use o Configuration Manager para instalar um sistema operacional em um novo computador (sem sistema operacional) usando PXE, OEM ou mídia autônoma.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f5ad22d5-7df1-49c6-8a0f-db1c3f0cda19
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 23c3a8b379accac0e514cfb8a88197baa6463fee
ms.sourcegitcommit: 54e5786875c4e5f5c1b54e38ed59e96344faf9b4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53817725"
---
# <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal-with-system-center-configuration-manager"></a>Instalar uma nova versão do Windows em um novo computador (sem sistema operacional) com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico fornece as etapas gerais no System Center Configuration Manager para instalar um sistema operacional em um novo computador. Para este cenário, é possível escolher entre vários métodos de implantação diferentes, como PXE, OEM ou mídia autônoma. Se não tiver certeza de que esse é o cenário de implantação de sistema operacional certo para você, consulte [Cenários para implantar sistemas operacionais corporativos](scenarios-to-deploy-enterprise-operating-systems.md).  

Use as seções a seguir para atualizar um computador existente com uma nova versão do Windows.  

##  <a name="BKMK_Plan"></a> Planoo  

-   **Planejar e implementar requisitos de infraestrutura**  

     Existem vários requisitos de infraestrutura que devem estar em vigor antes que você possa implantar sistemas operacionais, como Windows ADK, WDS (Serviços de Implantação do Windows), configurações de disco rígido com suporte, etc. Para mais informações, consulte [Requisitos de infraestrutura para implantação do sistema operacional](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).

##  <a name="BKMK_Configure"></a> Configurar  

1.  **Preparar uma imagem de inicialização**  

     Imagens de inicialização iniciam um computador em um ambiente do Windows PE (um sistema operacional mínimo com componentes e serviços limitados) que, em seguida, pode instalar um sistema operacional Windows completo no computador.   Ao implantar sistemas operacionais, é necessário selecionar uma imagem de inicialização a ser usada e distribuir a imagem para um ponto de distribuição. Use o seguinte para preparar a imagem de inicialização:  

    -   Para saber mais sobre imagens de inicialização, consulte [Gerenciar imagens de inicialização](../get-started/manage-boot-images.md).  

    -   Para obter mais informações sobre como personalizar uma imagem de inicialização, consulte [Personalizar imagens de inicialização](../get-started/customize-boot-images.md).  

    -   Distribua a imagem de inicialização para pontos de distribuição. Para obter mais informações, consulte [Distribuir conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Preparar uma imagem do sistema operacional**  

     A imagem do sistema operacional contém os arquivos necessários para instalar o sistema operacional no computador de destino. Use o seguinte para preparar a imagem do sistema operacional:  

    -   Para saber mais sobre como criar uma imagem do sistema operacional, consulte [Gerenciar imagens do sistema operacional](../get-started/manage-operating-system-images.md).

    -   Distribua a imagem do sistema operacional para pontos de distribuição. Para obter mais informações, consulte [Distribuir conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

    > [!NOTE]
    > Novas instalações do Windows também podem ser executadas usando arquivos de origem de instalação por meio de pacotes de atualização do sistema operacional, mas use imagens do sistema operacional, como **install.wim**.
    >
    > Ainda há suporte para a implantação de novas instalações do Windows por meio de pacotes de atualização do sistema operacional, mas depende da compatibilidade dos drivers com esse método. Ao instalar o Windows a partir do pacote de atualização do sistema operacional, os drivers são instalados enquanto ainda estão no Windows PE, em vez de simplesmente serem injetados no Windows PE. Alguns drivers não são compatíveis com a instalação no Windows PE. Se os drivers não forem compatíveis com a instalação no Windows PE, então use uma imagem do sistema operacional.  

3.  **Criar uma sequência de tarefas para implantar sistemas operacionais na rede**  

     Use uma sequência de tarefas para automatizar a instalação do sistema operacional na rede. Use as etapas em [Criar uma sequência de tarefas para instalar um sistema operacional](create-a-task-sequence-to-install-an-operating-system.md) para criar a sequência de tarefas para implantar o sistema operacional. Dependendo do método de implantação que você escolher, pode haver considerações adicionais para a sequência de tarefas.  

##  <a name="BKMK_Deploy"></a> Implantar  

-   Use um dos seguintes métodos de implantação para implantar o sistema operacional:  

    -   [Usar PXE para implantar o Windows na rede](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Usar multicast para implantar o Windows pela rede](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Criar uma imagem de um OEM na fábrica ou em um repositório local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Usar a mídia autônoma para implantar o Windows sem uso da rede](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [Use a mídia inicializável para implantar o Windows na rede](use-bootable-media-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Monitor  

-   **Monitorar a implantação da sequência de tarefas**  

     Para monitorar a implantação da sequência de tarefas para instalar o sistema operacional, consulte [Monitorar implantações do sistema operacional](monitor-operating-system-deployments.md).  
