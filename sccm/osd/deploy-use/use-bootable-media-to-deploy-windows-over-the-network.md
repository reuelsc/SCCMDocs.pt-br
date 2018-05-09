---
title: Use a mídia inicializável para implantar o Windows na rede
titleSuffix: Configuration Manager
description: Use implantações de mídia inicializável no System Center Configuration Manager para implantar o sistema operacional quando o computador de destino iniciar.
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4f7ec06d5bd5f23ac2b8afa2a288dfb8c971f950
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Use a mídia inicializável para implantar o Windows na rede com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode implantar o sistema operacional quando o computador de destino for iniciado usando uma implantação de mídia inicializável. A mídia contém um ponteiro para a sequência de tarefas, a imagem do sistema operacional e outro conteúdo necessário da rede. Quando o computador de destino é iniciado, o computador recupera os itens mencionados no ponteiro. Com a mídia inicializável livre de conteúdo, você pode atualizar o destino sem a necessidade de substituí-lo na mídia.

Você pode implantar sistemas operacionais na rede usando multicast nos seguintes cenários de implantação de sistema operacional:

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Instalar uma nova versão do Windows em um novo computador (sem sistema operacional)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Substituir um computador existente e transferir configurações](replace-an-existing-computer-and-transfer-settings.md)  

Conclua as etapas em um dos cenários de implantação de sistema operacional e, então, use as seções a seguir para utilizar a mídia inicializável para implantar o sistema operacional.  

## <a name="configure-deployment-settings"></a>Definir configurações de implantação  
Ao usar a mídia inicializável para iniciar o processo de implantação de sistema operacional, configure a implantação para tornar o sistema operacional disponível para a mídia. Você pode definir essa opção na página **Configurações de implantação** do Assistente de implantação de Software ou na guia **Configurações de implantação** nas propriedades de implantação. Para a configuração **Tornar disponível para o seguinte** , defina uma das seguintes opções:

-   Clientes do Configuration Manager, mídia e PXE

-   Somente mídia e PXE

-   Somente mídia e PXE (oculto)

## <a name="create-the-bootable-media"></a>Criar uma mídia inicializável
Você pode especificar se a mídia inicializável é uma unidade flash USB ou um conjunto de CD/DVD. O computador que inicia a mídia deve dar suporte à opção que você escolher como uma unidade inicializável. Para obter mais informações, consulte [Criar mídia inicializável](create-bootable-media.md).  

##  <a name="BKMK_Deploy"></a> Instalar o sistema operacional por meio de uma mídia inicializável  
Insira a mídia inicializável em uma unidade inicializável no computador e ligue-a para instalar o sistema operacional.
