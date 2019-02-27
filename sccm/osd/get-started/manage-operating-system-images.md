---
title: Gerenciar imagens do sistema operacional
titleSuffix: Configuration Manager
description: Aprenda métodos para gerenciar imagens do sistema operacional armazenadas em arquivos WIM (imagem do Windows).
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ea320b42bfb08ec0023598d010375042d143c220
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124063"
---
# <a name="manage-os-images-with-configuration-manager"></a>Gerenciar imagens do sistema operacional com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Imagens do sistema operacional no Configuration Manager são armazenadas no formato de arquivo WIM (imagem do Windows). Essas imagens são uma coleção compactada de arquivos de referência e pastas usadas para instalar e configurar um novo sistema operacional em um computador. Muitos cenários de implantação do sistema operacional exigem uma imagem do sistema operacional. 

Você pode usar uma [imagem do sistema operacional padrão](#default-image) ou compilar a imagem do sistema operacional de um [computador de referência](#bkmk_capture) que você configurar. Quando você compila o computador de referência, adiciona arquivos de sistema operacional, drivers, arquivos de suporte, atualizações de software, ferramentas e aplicativos ao sistema operacional. Em seguida, você os captura para criar o arquivo de imagem. 

### <a name="default-image"></a>Imagem padrão

Os arquivos de instalação do Windows incluem a imagem do sistema operacional padrão. Essa imagem é uma imagem básica do sistema operacional que contém um conjunto padrão de drivers. Quando você usa a imagem padrão do sistema operacional, use as etapas da sequência de tarefas instalar aplicativos e fazer outras configurações depois que o sistema operacional estiver instalado em um dispositivo. Localize a imagem padrão do sistema operacional nos arquivos de origem do Windows: `\Sources\install.wim`.  

#### <a name="default-image-advantages"></a>Vantagens da imagem padrão

- O tamanho da imagem é menor do que uma imagem capturada.  

- A instalação de aplicativos e as configurações com etapas de sequências de tarefas são mais dinâmicas. Por exemplo, altere as configurações e os aplicativos que são instalados na sequência de tarefas sem precisar refazer a imagem de dispositivo.  

#### <a name="default-image-disadvantages"></a>Desvantagens da imagem padrão

- A instalação do sistema operacional pode levar mais tempo. A instalação do aplicativo e outras configurações ocorrem após a instalação do sistema operacional ser concluída.  


### <a name="bkmk_capture"></a> Imagem capturada de um computador de referência

Para criar uma imagem personalizada do sistema operacional, crie um computador de referência com o sistema operacional desejado. Em seguida, instale os aplicativos e defina as configurações. Capture a imagem do sistema operacional do computador de referência para criar o arquivo WIM. Compile o computador de referência manualmente ou use uma sequência de tarefas para automatizar algumas ou todas as etapas de build. Para obter mais informações, confira [Personalizar imagens do sistema operacional](/sccm/osd/get-started/customize-operating-system-images).  

#### <a name="captured-image-advantages"></a>Vantagens da imagem capturada

- A instalação pode ser mais rápida que usar a imagem padrão. Por exemplo, os aplicativos podem ser pré-instalados com a imagem capturada do sistema operacional. Em seguida, você não precisa instalar esses mesmos aplicativos mais tarde usando as etapas de sequência de tarefas.  

#### <a name="captured-image-disadvantages"></a>Desvantagens da imagem capturada

- O tamanho da imagem é potencialmente maior que a imagem padrão.  

- É preciso criar uma nova imagem quando você precisar de atualizações a aplicativos e ferramentas.  



##  <a name="BKMK_AddOSImages"></a> Adicionar uma imagem de sistema operacional  

Antes de usar uma imagem do sistema operacional, adicione-a ao seu site do Configuration Manager. 

1.  No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione o nó **Imagens do Sistema Operacional**.  

2.  Na guia **Início** da faixa de opções, no grupo **Criar**, selecione **Adicionar Imagem do Sistema Operacional**. Essa ação inicia o Assistente para Adicionar Imagem do Sistema Operacional.  

3.  Na página **Fonte de Dados**, especifique o **Caminho** de rede para o arquivo de imagem do sistema operacional. Por exemplo, `\\server\share\path\image.wim`.  

4.  Na página **Geral**, especifique as seguintes informações. Essas informações são úteis para fins de identificação quando você tiver mais de uma imagem do sistema operacional.  

    -   **Nome**: um nome exclusivo para a imagem. Por padrão, o nome vem do nome do arquivo WIM.  

    -   **Versão**: um identificador de versão opcional. Essa propriedade não precisa ser a versão do sistema operacional da imagem. Geralmente é a versão da sua organização para o pacote.   

    -   **Comentário**: uma breve descrição opcional.  

5.  Conclua o assistente.  


Em seguida, distribua a imagem do sistema operacional aos pontos de distribuição.  



##  <a name="BKMK_DistributeBootImages"></a> Distribuir conteúdo em pontos de distribuição  

Distribua imagens do sistema operacional para pontos de distribuição da mesma maneira que outros conteúdos. Antes de implantar a sequência de tarefas, distribua a imagem do sistema operacional para pelo menos um ponto de distribuição. Para obter mais informações, consulte [Distribuir conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  



[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]



##  <a name="BKMK_OSImageMulticast"></a> Preparar a imagem do sistema operacional para implantações multicast  

Use implantações multicast para permitir que mais de um computador baixe simultaneamente uma imagem do sistema operacional. A imagem é difundida via multicast para clientes pelo ponto de distribuição, em vez de cada cliente baixar uma cópia da imagem do ponto de distribuição por uma conexão separada. Quando você escolhe o método de implantação do sistema operacional para [Usar o multicast para implantar o Windows pela rede](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network), configure a imagem do sistema operacional para dar suporte a multicast. Em seguida, distribua a imagem para um ponto de distribuição habilitado para multicast. 

1.  No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione o nó **Imagens do Sistema Operacional**.  

2.  Selecione a imagem do sistema operacional que você deseja distribuir para um ponto de distribuição habilitado para multicast.  

3.  Na guia **Início** da faixa de opções, no grupo **Propriedades**, selecione **Propriedades**.  

4.  Mude para a guia **Configurações de Distribuição** e configure as seguintes opções:  

    -   **Permitir que este pacote seja transferido via multicast (WinPE somente)**: selecione essa opção para que o Configuration Manager implante simultaneamente as imagens do sistema operacional usando multicast.  

    -   **Criptografar pacotes multicast**: especifique se o site criptografa a imagem antes que ela seja enviada ao ponto de distribuição. Se a imagem contiver informações confidenciais, use esta opção. Se a imagem não estiver criptografada, seu conteúdo ficará visível em texto não criptografado na rede. Em seguida, um usuário não autorizado poderá interceptar e exibir o conteúdo de imagem.  

    -   **Transferir este pacote somente via multicast**: especifique se deseja que o ponto de distribuição para implantar a imagem somente durante uma sessão de multicast.  

         Se você selecionar **Transferir este pacote somente via multicast**, também será preciso especificar a opção de implantação de sequência de tarefa para **Baixar conteúdo localmente quando necessário executando a sequência de tarefas**. Para obter mais informações, consulte [Deploy a task sequence](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).   

5.  Selecione **OK** para salvar as configurações e fechar as propriedades da imagem.  
