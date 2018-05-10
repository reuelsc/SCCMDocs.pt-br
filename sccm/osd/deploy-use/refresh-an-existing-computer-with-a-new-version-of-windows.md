---
title: Atualizar um computador existente com uma nova versão do Windows
titleSuffix: Configuration Manager
description: Você pode usar vários métodos no Configuration Manager para particionar e formatar (apagar) um computador existente e instalar um novo sistema operacional nele.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 622b49b9fb689db8238be8254a66b3a0264b4399
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows-using-system-center-configuration-manager"></a>Atualizar um computador existente com uma nova versão do Windows usando o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico fornece as etapas gerais no System Center Configuration Manager para particionar e formatar (apagar) um computador existente e instalar um novo sistema operacional nele. Para este cenário, é possível escolher entre vários métodos de implantação diferentes, como PXE, mídia inicializável ou o Centro de Software. Também é possível optar por instalar um ponto de migração de estado para armazenar as configurações e restaurá-las para o novo sistema operacional após a instalação. Se não tiver certeza de que esse é o cenário de implantação de sistema operacional certo para você, consulte [Cenários para implantar sistemas operacionais corporativos](scenarios-to-deploy-enterprise-operating-systems.md).  

 Use as seções a seguir para atualizar um computador existente com uma nova versão do Windows.  

##  <a name="BKMK_Plan"></a> Planoo  

-   **Planejar e implementar requisitos de infraestrutura**  

     Vários requisitos de infraestrutura devem estar em vigor antes que você possa implantar sistemas operacionais, como Windows ADK, USMT (Ferramenta de Migração do Usuário), WDS (Serviços de Implantação do Windows), configurações de disco rígido com suporte, etc. Para mais informações, consulte [Requisitos de infraestrutura para implantação do sistema operacional](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

-   **Instalar um ponto de migração de estado (necessário somente se você transferir as configurações)**  

     Quando você for capturar as configurações do computador existente e restaurá-las para o novo sistema operacional, é necessário instalar um ponto de migração de estado. Para mais informações, consulte [Ponto de migração de estado](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

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

3.  **Criar uma sequência de tarefas para implantar sistemas operacionais na rede**  

     Use uma sequência de tarefas para automatizar a instalação do sistema operacional na rede. Use as etapas em [Criar uma sequência de tarefas para instalar um sistema operacional](create-a-task-sequence-to-install-an-operating-system.md) para criar a sequência de tarefas para implantar o sistema operacional. Dependendo do método de implantação que você escolher, pode haver considerações adicionais para a sequência de tarefas.  

    > [!NOTE]  
    >  Nesse cenário, a sequência de tarefas formata e particiona os discos rígidos no computador. Para capturar as configurações do usuário, é necessário usar o ponto de migração de estado e selecionar **Salvar configurações e arquivos de usuário em um Ponto de Migração de Estado** no página **Migração de Estado** do assistente para Criar Sequência de Tarefas. Se você salvar as configurações de usuário e os arquivos localmente, eles serão perdidos quando o disco rígido for formatado e o Configuration Manager não conseguirá restaurar as configurações. Para mais informações, consulte [Gerenciar o estado do usuário](../get-started/manage-user-state.md).  

##  <a name="BKMK_Deploy"></a> Implantar  

-   Use um dos seguintes métodos de implantação para implantar o sistema operacional:  

    -   [Usar PXE para implantar o Windows na rede](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Usar multicast para implantar o Windows pela rede](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Criar uma imagem de um OEM na fábrica ou em um repositório local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Usar a mídia autônoma para implantar o Windows sem uso da rede](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [Use a mídia inicializável para implantar o Windows na rede](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [Usar o Centro de Software para implantar o Windows pela rede](use-software-center-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Monitor  

-   **Monitorar a implantação da sequência de tarefas**  

     Para monitorar a implantação da sequência de tarefas para instalar o sistema operacional, consulte [Monitorar implantações do sistema operacional](monitor-operating-system-deployments.md).  
