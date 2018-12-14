---
title: Gerenciar pacotes de atualização do sistema operacional
titleSuffix: Configuration Manager
description: Saiba como gerenciar pacotes de atualização do sistema operacional no Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f7b8b18cbec5a3b5972a448e8a70339533dc11fb
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52455999"
---
# <a name="manage-os-upgrade-packages-with-configuration-manager"></a>Gerenciar pacotes de atualização do sistema operacional com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Um pacote de atualização do sistema operacional no Configuration Manager contém os arquivos de origem de instalação do Windows para atualizar um sistema operacional existente em um computador. Este artigo descreve como adicionar, distribuir e realizar a manutenção de um pacote de atualização do sistema operacional.



##  <a name="BKMK_AddOSUpgradePkgs"></a> Adicione um pacote de atualização do sistema operacional  

Antes de usar um pacote de atualização do sistema operacional, primeiro o adicione ao seu site do Configuration Manager. 

1.  No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione o nó **Pacotes de Atualização do Sistema Operacional**.  

2.  Na guia **Início** da faixa de opções, no grupo **Criar**, selecione **Adicionar Pacote de Atualização do Sistema Operacional**. Essa ação inicia o Assistente para Adicionar Atualização de Sistema Operacional.  

3.  Na página **Fonte de Dados**, especifique as seguintes configurações: 

    - O **Caminho** da rede para os arquivos de origem de instalação do pacote de atualização do sistema operacional. Por exemplo, `\\server\share\path`.  

        > [!NOTE]  
        >  Os arquivos de origem de instalação contêm setup.exe e outros arquivos e pastas para instalar o sistema operacional.  

        > [!IMPORTANT]  
        >  Limite o acesso aos arquivos de origem dessa instalação para impedir violações indesejadas.  

    - Se você quiser armazenar em cache previamente o conteúdo em um cliente, especifique a **Arquitetura** e a **Linguagem** da imagem. Para saber mais, confira [Configurar o conteúdo de armazenamento prévio em cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  

4.  Na página **Geral**, especifique as seguintes informações. Essas informações são úteis para fins de identificação quando você tiver mais de um pacote de atualização do sistema operacional.  

    -   **Nome**: um nome exclusivo para o pacote de atualização do sistema operacional.  

    -   **Versão**: um identificador de versão opcional. Essa propriedade não precisa ser a versão do pacote de atualização do sistema operacional. Geralmente é a versão da sua organização para o pacote.  

    -   **Comentário**: uma breve descrição opcional.  

5.  Conclua o assistente.  


Em seguida, distribua o pacote de atualização do sistema operacional para pontos de distribuição.  



##  <a name="BKMK_Distribute"></a> Distribuir conteúdo para um ponto de distribuição  

Pacotes de atualização do sistema operacional para pontos de distribuição distribuem o mesmo que outros tipos de conteúdo. Antes de implantar a sequência de tarefas, distribua o pacote de atualização do sistema operacional para pelo menos um ponto de distribuição. Para obter mais informações, consulte [Distribuir conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  



[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]



## <a name="next-steps"></a>Próximas etapas

[Criar uma sequência de tarefas para atualizar um sistema operacional](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)