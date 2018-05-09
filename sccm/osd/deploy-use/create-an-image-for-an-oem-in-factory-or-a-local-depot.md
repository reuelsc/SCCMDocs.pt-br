---
title: Criar uma imagem de um OEM na fábrica ou em um repositório local
titleSuffix: Configuration Manager
description: Use implantações de mídia de pré-teste para reduzir o tráfego de rede ao implantar um sistema operacional em um computador que não está totalmente provisionado.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0c8cf0af19017f4acfd95bcd01f8226229c05a14
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-system-center-configuration-manager"></a>Criar uma imagem de um OEM na fábrica ou em um repositório local com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Implantações de mídia de pré-teste no System Center Configuration Manager permitem implantar um sistema operacional em um computador que não está totalmente provisionado. A mídia de pré-teste é um arquivo em formato WIM (Windows Imaging) que pode ser instalado em um computador bare-metal pelo fabricante (OEM) ou em um centro de preparo corporativo que não está conectado ao ambiente do Configuration Manager. Posteriormente, no ambiente do Configuration Manager, quando o computador for iniciado usando a imagem de inicialização fornecida pela mídia, uma verificação de hash será executada na mídia pré-configurada para verificar se ela é válida e, em seguida, o computador será conectado ao ponto de gerenciamento do site para as sequências de tarefas disponíveis que concluem o processo de download.


Esse método de implantação pode reduzir o tráfego de rede, pois a imagem de inicialização e a imagem do sistema operacional já estão no computador de destino. É possível especificar aplicativos, pacotes e pacotes de driver para incluir na mídia pré-configurada. Após o sistema operacional ser instalado no computador, o cache de sequência de tarefas local será verificado primeiro para detectar aplicativos, pacotes ou pacotes de driver. Caso não seja encontrado ou tenha sido revisado, o conteúdo será baixado de um ponto de distribuição configurado na mídia em pré-teste e será instalado.  

 Você pode usar a mídia de pré-teste nos seguintes cenários de implantação de sistema operacional:  

-   [Instalar uma nova versão do Windows em um novo computador (sem sistema operacional)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Substituir um computador existente e transferir configurações](replace-an-existing-computer-and-transfer-settings.md)  

 Conclua as etapas em um dos cenários de implantação de sistema operacional e use as seções a seguir para preparar e criar a mídia pré-configurada.  

## <a name="configure-deployment-settings"></a>Definir configurações de implantação  
 Ao usar a mídia pré-configurada para iniciar o processo de implantação de sistema operacional, é necessário configurar a implantação para disponibilizar o sistema operacional para a mídia. Você pode configurá-la na página **Configurações de implantação** do Assistente de implantação de Software ou na guia **Configurações de implantação** nas propriedades de implantação.  Para a configuração **Tornar disponível para o seguinte** , defina uma das seguintes opções:  

-   **Clientes do Configuration Manager, mídia e PXE**  

-   **Somente mídia e PXE**  

-   **Somente mídia e PXE (oculto)**  

## <a name="create-the-prestaged-media"></a>Criar a mídia pré-configurada  
 Crie o arquivo de mídia pré-configurada para enviar ao OEM ou repositório local. Para obter mais informações, consulte [Criar mídia pré-configurada com o System Center Configuration Manager](create-prestaged-media.md).  

## <a name="send-the-prestaged-media-file-to-the-oem-or-local-depot"></a>Enviar o arquivo de mídia pré-configurada ao OEM ou repositório local  
 Envie a mídia ao OEM ou a seu repositório local para pré-configurar os computadores. O arquivo de mídia pré-configurada é aplicado a um disco rígido formatado no computador.  

## <a name="start-the-computer-to-install-the-operating-system"></a>Iniciar o computador para instalar o sistema operacional  
 O arquivo de mídia pré-configurada é aplicado aos computadores. Quando o computador é iniciado pela primeira vez, o processo de instalação do sistema operacional é iniciado.  
