---
title: "Usar mídia inicializável para implantar o Windows na rede | Microsoft Docs"
description: "Use implantações de mídia inicializável no System Center Configuration Manager para implantar o sistema operacional quando o computador de destino iniciar."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: beb730efbe4d9bae7c4c97f4e587c8919bd79049


---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Use a mídia inicializável para implantar o Windows na rede com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Implantações de mídia inicializável no System Center Configuration Manager permitem implantar o sistema operacional quando o computador de destino iniciar. Quando o computador de destino é iniciado, ele se conecta à rede e recupera a sequência de tarefas, a imagem do sistema operacional e qualquer outro conteúdo necessário da rede. Como esse conteúdo não está incluído na mídia, você pode atualizar o conteúdo sem precisar recriar a mídia.  

 Você pode implantar sistemas operacionais na rede usando multicast nos seguintes cenários de implantação de sistema operacional:  

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar uma nova versão do Windows em um novo computador (sem sistema operacional)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Substituir um computador existente e transferir configurações](replace-an-existing-computer-and-transfer-settings.md)  

 Conclua as etapas em um dos cenários de implantação de sistema operacional e, então, use as seções a seguir para utilizar a mídia inicializável para implantar o sistema operacional.  

## <a name="configure-deployment-settings"></a>Definir configurações de implantação  
 Quando você usa a mídia inicializável para iniciar o processo de implantação do sistema operacional, você deve configurar a implantação para tornar o sistema operacional disponível para a mídia. Você pode configurá-la na página **Configurações de implantação** do Assistente de implantação de Software ou na guia **Configurações de implantação** nas propriedades de implantação.  Para a configuração **Tornar disponível para o seguinte** , defina uma das seguintes opções:  

-   **Clientes do Configuration Manager, mídia e PXE**  

-   **Somente mídia e PXE**  

-   **Somente mídia e PXE (oculto)**  

## <a name="create-the-bootable-media"></a>Criar uma mídia inicializável  
 Você pode especificar se a mídia inicializável é uma unidade flash USB ou um conjunto de CD/DVD. O computador que inicia a mídia deve dar suporte para a opção que você escolher como uma unidade inicializável. Para obter mais informações, consulte [Criar mídia inicializável](create-bootable-media.md).  

##  <a name="a-namebkmkdeploya-install-the-operating-system-from--bootable-media"></a><a name="BKMK_Deploy"></a> Instalar o sistema operacional por meio de uma mídia inicializável  
 Insira a mídia inicializável em uma unidade inicializável no computador e ligue-a para instalar o sistema operacional.  



<!--HONumber=Dec16_HO3-->


