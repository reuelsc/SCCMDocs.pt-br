---
title: Criar mídia de captura
titleSuffix: Configuration Manager
description: Use uma mídia de captura no Configuration Manager para capturar uma imagem do SO de um computador de referência.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: article
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6e1e007387a50146a899bca767aa5d1f2d85a3a
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65082755"
---
# <a name="create-capture-media"></a>Criar mídia de captura

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Uma mídia de captura no Configuration Manager permite capturar uma imagem do SO de um computador de referência. A mídia de captura contém a imagem de inicialização que inicia o computador de referência e a sequência de tarefas que captura a imagem do SO. Use a mídia de captura do cenário para [Criar uma sequência de tarefas para capturar um sistema operacional](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system).  


## <a name="prerequisites"></a>Pré-requisitos

Antes de criar uma mídia de captura usando o Assistente para Criar Mídia de Sequência de Tarefas, verifique se todas essas condições foram atendidas.

### <a name="boot-image"></a>Imagem de inicialização

Considere os seguintes pontos sobre a imagem de inicialização usada na sequência de tarefas para implantar o SO:

- A arquitetura da imagem de inicialização deve ser apropriada para a arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode iniciar e executar uma imagem de inicialização x86 ou x64. No entanto, um computador de destino x86 pode iniciar e executar apenas uma imagem de inicialização x86.
- Certifique-se de que a imagem de inicialização contenha os drivers de rede e de armazenamento necessários para provisionar o computador de destino.

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuir todo o conteúdo associado à sequência de tarefas

Distribua todo o conteúdo exigido pela sequência de tarefas para pelo menos um ponto de distribuição. Esse conteúdo inclui a imagem de inicialização, a imagem do SO e outros arquivos associados. O assistente reúne o conteúdo do ponto de distribuição ao criar a mídia de captura.

Sua conta de usuário precisa pelo menos de direitos de acesso de **Leitura** à biblioteca de conteúdo nesse ponto de distribuição. Para obter mais informações, consulte [Distribuir conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Preparar a unidade USB removível

Se estiver usando uma unidade USB removível, conecte-a ao computador em que você executa o Assistente para Criar Mídia de Sequência de Tarefas. A unidade USB deve ser detectável pelo Windows como um dispositivo de remoção. O assistente grava diretamente na unidade USB ao criar a mídia.

### <a name="create-an-output-folder"></a>Criar uma pasta de saída

Antes de executar o Assistente para Criar Mídia de Sequência de Tarefas para criar a mídia para um conjunto de CD ou DVD, crie uma pasta para os arquivos de saída que são gerados. A mídia criada para um conjunto de CD ou DVD é gravada como um arquivo .ISO diretamente na pasta.


## <a name="process"></a>Processar

1. No console do Configuration Manager, acesse o espaço de trabalho **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione o nó **Sequências de Tarefas**.  

2. Na guia **Início** da faixa de opções, no grupo **Criar**, selecione **Criar Mídia de Sequência de Tarefas**. Essa ação inicia o Assistente para Criar Mídia de Sequência de Tarefas.  

3. Na página **Selecionar o Tipo de Mídia**, selecione **Capturar mídia**.  

4. Na página **Tipo de Mídia**, especifique se a mídia é uma **Unidade USB removível** ou um **Conjunto de CD/DVD**. Em seguida, configure as seguintes opções:  

    > [!IMPORTANT]  
    > A mídia usa um sistema de arquivos FAT32. Você não pode criar uma mídia em uma unidade USB cujo conteúdo inclua um arquivo com mais de 4 GB.  

    - Se você selecionar **Unidade USB removível**, selecione a unidade na qual deseja armazenar o conteúdo.  

        - **Formatar a unidade USB removível (FAT32) e torná-la inicializável**: por padrão, permita que o Configuration Manager prepare a unidade USB. Muitos dispositivos UEFI mais recentes requerem uma partição FAT32 inicializável. No entanto, esse formato também limita o tamanho dos arquivos e a capacidade geral da unidade. Se você já formatou e configurou a unidade de disco removível, desabilite essa opção.

    - Se você selecionar **Conjunto de CD/DVD**, especifique a capacidade da mídia (**Tamanho da mídia**) e o nome e o caminho do arquivo de saída (**Arquivo de mídia**). O assistente grava os arquivos de saída nesse local. Por exemplo: `\\servername\folder\outputfile.iso`  

        Se a capacidade da mídia for muito pequena para armazenar todo o conteúdo, ela criará vários arquivos. Portanto, você precisará armazenar o conteúdo em vários CDs ou DVDs. Quando vários arquivos de mídia são necessários, o Configuration Manager adiciona um número de sequência ao nome de cada arquivo de saída criado.  

        > [!IMPORTANT]  
        > Se você selecionar uma imagem .iso existente, o Assistente de Mídia de Sequência de Tarefas excluirá essa imagem da unidade ou do compartilhamento assim que você prosseguir para a próxima página do assistente. A imagem existente será excluída mesmo se você cancelar o assistente.  

    - **Pasta de preparo**<!--1359388-->: o processo de criação da mídia pode exigir muito espaço em disco temporário. Por padrão, essa localização é semelhante ao seguinte caminho: `%UserProfile%\AppData\Local\Temp`. A partir da versão 1902, para fornecer maior flexibilidade quando se trata de armazenar esses arquivos temporários, altere esse valor para outra unidade e caminho.  

    - **Rótulo de mídia**<!--1359388-->: a partir da versão 1902, adicione um rótulo à mídia de sequência de tarefas. Esse rótulo ajuda a identificar melhor a mídia depois de criá-la. O valor padrão é `Configuration Manager`. Esse campo de texto é exibido nos seguintes locais:  

        - Se você montar um arquivo ISO, o Windows exibirá esse rótulo como o nome da unidade montada  

        - Se você formatar uma unidade USB, ela usará os primeiro 11 caracteres do rótulo como seu nome  

        - O Configuration Manager grava um arquivo de texto chamado `MediaLabel.txt` na raiz da mídia. Por padrão, o arquivo inclui uma única linha de texto: `label=Configuration Manager`. Se você personalizar o rótulo de mídia, essa linha usará o rótulo personalizado, em vez do valor padrão.  

    - **Incluir arquivo autorun.inf na mídia**<!-- 4090666 -->: a partir da versão 1902, o Configuration Manager não adiciona um arquivo autorun.inf por padrão. Normalmente, esse arquivo é bloqueado por produtos antimalware. Para obter mais informações sobre o recurso AutoRun do Windows, confira [Creating an AutoRun-enabled CD-ROM Application](https://docs.microsoft.com/windows/desktop/shell/autoplay) (Criando um aplicativo de CD-ROM habilitado para AutoRun). Se ainda for necessário para o seu cenário, selecione essa opção para incluir o arquivo.  

5. Na página **Imagem de inicialização**, especifique as seguintes opções:  

    > [!IMPORTANT]  
    > A arquitetura da imagem de inicialização que você distribuir deve ser apropriada para a arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode iniciar e executar uma imagem de inicialização x86 ou x64. No entanto, um computador de destino x86 pode iniciar e executar apenas uma imagem de inicialização x86.  

    - **Imagem de inicialização**: selecione a imagem de inicialização para iniciar o computador de destino.  

    - **Ponto de distribuição**: selecione o ponto de distribuição que possui a imagem de inicialização. O assistente recupera a imagem de inicialização do ponto de distribuição e a grava na mídia.  

        > [!NOTE]  
        > Sua conta de usuário precisa pelo menos de permissões de **Leitura** à biblioteca de conteúdo no ponto de distribuição.  

6. Conclua o assistente.  


## <a name="next-steps"></a>Próximas etapas

[Criar uma sequência de tarefas para capturar um sistema operacional](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system)
