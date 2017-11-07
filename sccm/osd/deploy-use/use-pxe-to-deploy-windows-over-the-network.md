---
title: Usar PXE para implantar o Windows na rede
titleSuffix: Configuration Manager
description: "Use implantações de sistema operacional iniciadas pelo PXE para atualizar o sistema operacional de um computador ou para instalar uma nova versão do Windows em um novo computador."
ms.custom: na
ms.date: 06/15/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
caps.latest.revision: "19"
caps.handback.revision: "0"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 017a8f0d5b38145f6708e61ff5d7b2c3614b62a0
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Use o PXE para implantar o Windows pela rede com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As implantações de sistema operacional iniciadas pelo PXE (Pre-Boot Execution Environment) no System Center Configuration Manager permitem que os computadores cliente solicitem e implantem sistemas operacionais pela rede. Nesse cenário de implantação, você envia a imagem do sistema operacional e as imagens de inicialização do x86 e x64 do Windows PE a um ponto de distribuição configurado para aceitar solicitações de inicialização PXE.

> [!NOTE]  
>  Quando você cria uma implantação de sistema operacional que se destina somente a computadores com BIOS x64, ambas as imagens de inicialização x64 e x86 devem estar disponíveis no ponto de distribuição.

É possível usar implantações de sistema operacional iniciadas pelo PXE nos seguintes cenários de implantação de sistema operacional:

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar uma nova versão do Windows em um novo computador (sem sistema operacional)](install-new-windows-version-new-computer-bare-metal.md)  

Conclua as etapas em um dos cenários de implantação de sistema operacional e use as seções a seguir para preparar implantações iniciadas pelo PXE.

##  <a name="BKMK_Configure"></a> Configurar pelo menos um ponto de distribuição para aceitar solicitações PXE
Para implantar sistemas operacionais em clientes que fazem solicitações de inicialização PXE, use um ou mais pontos de distribuição configurados para responder às solicitações de inicialização PXE. Para obter as etapas necessárias para habilitar o PXE em um ponto de distribuição, consulte [Configuring distribution points to accept PXE requests (Configurando pontos de distribuição para aceitar solicitações PXE)](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint).

## <a name="prepare-a-pxe-enabled-boot-image"></a>Preparar uma imagem de inicialização habilitada para PXE
Para usar PXE para implantar um sistema operacional, você precisa ter imagens de inicialização x86 e x64 habilitadas para PXE distribuídas para um ou mais pontos de distribuição habilitados para PXE. Use as informações para habilitar o PXE em uma imagem de inicialização e distribuí-la para pontos de distribuição:

-   Para habilitar o PXE em uma imagem de inicialização, selecione **Implantar esta imagem de inicialização do ponto de distribuição habilitado para PXE** na guia **Fonte de Dados** nas propriedades da imagem de inicialização.

-   Se você alterar as propriedades da imagem de inicialização, distribua novamente a imagem de inicialização para os pontos de distribuição. Para obter mais informações, consulte [Distribuir conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

##  <a name="BKMK_PXEExclusionList"></a> Criar uma lista de exclusões para implantações PXE
Ao implantar sistemas operacionais com o PXE, você pode criar uma lista de exclusões em cada ponto de distribuição. Adicione os endereços MAC à lista de exclusões dos computadores dos quais o ponto de distribuição você quer ignorar. Computadores listados não receberão sequências de tarefas de implantação usadas pelo Configuration Manager para a implantação PXE.

#### <a name="to-create-the-exclusion-list"></a>Para criar a lista de exclusão

1.  Crie um arquivo de texto no ponto de distribuição habilitado para PXE. Por exemplo, nomeie esse arquivo de texto **pxeExceptions.txt**.

2.  Use um editor de texto sem formatação, como o Bloco de Notas, e adicione os endereços MAC dos computadores a serem ignorados pelo ponto de distribuição habilitado para PXE. Separe os valores de endereço MAC por dois-pontos e, em seguida, digite cada endereço em uma linha separada. Por exemplo: `01:23:45:67:89:ab`

3.  Salve o arquivo de texto no servidor do sistema de site do ponto de distribuição habilitado para PXE. O arquivo de texto pode ser salvo em qualquer local no servidor.

4.  Edite o registro do ponto de distribuição habilitado para PXE para criar uma chave do Registro **MACIgnoreListFile**. Adicione o valor de cadeia de caracteres do caminho completo até o arquivo de texto no servidor do sistema de sites do ponto de distribuição habilitado para PXE. Use o seguinte caminho do registro:

     **HKLM\Software\Microsoft\SMS\DP**  

    > [!WARNING]  
    >  Se você usar o Editor do Registro incorretamente, você poderá causar sérios problemas e possivelmente precisará reinstalar o sistema operacional. A Microsoft não garante que você conseguirá resolver os problemas resultantes do uso incorreto do Editor do Registro. Use o Editor do Registro por sua conta e risco.

     Não é necessário reiniciar o servidor após você alterar esse registro.

##  <a name="BKMK_RamDiskTFTP"></a> Tamanho do bloco e da janela do RamDisk TFTP
É possível personalizar o tamanho do bloco e da janela do RamDisk TFTP, e partir do Configuration Manager versão 1606, o tamanho da janela para pontos de distribuição habilitados pelo PXE. Se você tiver personalizado sua rede, isso poderá fazer com que o download da imagem de inicialização falhe com um erro de tempo limite devido ao tamanho muito grande do bloco ou da janela. A personalização do tamanho do bloco e da janela do RamDisk TFTP permite otimizar o tráfego TFTP ao usar o PXE para atender aos seus requisitos de rede específicos. Teste as configurações personalizadas no ambiente para determinar o método mais eficiente. Para obter mais informações, consulte [Personalizar o tamanho do bloco e da janela do RamDisk TFTP nos pontos de distribuição habilitados para PXE](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="configure-deployment-settings"></a>Definir configurações de implantação
Para usar uma implantação de sistema operacional iniciada pelo PXE, é necessário configurar a implantação para disponibilizar o sistema operacional para solicitações de inicialização PXE. Você pode configurar os sistemas operacionais disponíveis na página **Configurações de implantação** do Assistente de implantação de Software ou na guia **Configurações de implantação** nas propriedades de implantação. Para a configuração **Tornar disponível para o seguinte** , defina uma das seguintes opções:

-   Clientes do Configuration Manager, mídia e PXE

-   Somente mídia e PXE

-   Somente mídia e PXE (oculto)

##  <a name="BKMK_Deploy"></a> Implantar a sequência de tarefas
Implantar o sistema operacional em uma coleção de destino. Para obter mais informações, consulte [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Ao implantar sistemas operacionais usando o PXE, é possível configurar se a implantação será necessária ou estará disponível.

-   **Implantação necessária**: as implantações necessárias usam o PXE sem nenhuma intervenção do usuário. O usuário não poderá ignorar a inicialização PXE. No entanto, se o usuário cancelar a inicialização PXE antes de o ponto de distribuição responder, o sistema operacional não será implantado.

-   **Implantação disponível**: as implantações disponíveis requerem que o usuário esteja presente no computador de destino para que o usuário pressione a tecla F12 para continuar o processo de inicialização PXE. Se o usuário não estiver presente para pressionar F12, o computador será inicializado no atual sistema operacional ou do próximo dispositivo de inicialização disponível.

É possível reimplantar uma implantação PXE necessária apagando o status da última implantação PXE atribuída a uma coleção do Configuration Manager ou a um computador. Essa ação redefine o status dessa implantação e reinstala as implantações necessárias mais recentes.

> [!IMPORTANT]
> O protocolo PXE não é seguro. Verifique se o servidor PXE e o cliente PXE estão localizados em uma rede fisicamente segura, como um data center, para evitar acesso não autorizado ao site.

##  <a name="how-is-the-boot-image-selected-for-clients-booting-with-pxe"></a>Como a imagem de inicialização é selecionada para clientes sendo inicializados com o PXE?
Quando um cliente é inicializado com o PXE, o Configuration Manager fornece ao cliente uma imagem de inicialização para usar. A partir do Configuration Manager versão 1606, o Configuration Manager usará uma imagem de inicialização com uma correspondência de arquitetura exata. Se uma imagem de inicialização com a arquitetura exata não estiver disponível, o Configuration Manager usará uma imagem de inicialização com uma arquitetura compatível. A lista a seguir fornece detalhes sobre como uma imagem de inicialização é selecionada para clientes sendo inicializados com o PXE.
1. O Configuration Manager examina o banco de dados do site para o registro do sistema que coincide com o endereço MAC ou o SMBIOS do cliente que está tentando inicializar.  

    > [!NOTE]
    > Se um computador atribuído a um site inicializar para PXE para um site diferente, as políticas não estarão visíveis para o computador. Por exemplo, se um cliente já estiver atribuído ao site A, o ponto de gerenciamento e o ponto de distribuição para o site B não poderão acessar as políticas do site A. O cliente não fará a inicialização PXE com êxito.

2. O Configuration Manager procura sequências de tarefas implantadas no registro do sistema encontradas na etapa 1.

3. Na lista de sequências de tarefas encontrada na etapa 2, o Configuration Manager procura uma imagem de inicialização que corresponde à arquitetura do cliente que está tentando inicializar. Se uma imagem de inicialização é encontrada com a mesma arquitetura, ela é usada.

4. Se uma imagem de inicialização não for encontrada com a mesma arquitetura, o Configuration Manager procurará uma imagem de inicialização compatível com a arquitetura do cliente. Ele procura na lista de sequências de tarefas encontrada na etapa 2. Por exemplo, um cliente de 64 bits é compatível com imagens de inicialização de 32 bits e 64 bits. Um cliente de 32 bits é compatível apenas com imagens de inicialização de 32 bits. Um cliente UEFI é compatível apenas com imagens de inicialização de 64 bits.
