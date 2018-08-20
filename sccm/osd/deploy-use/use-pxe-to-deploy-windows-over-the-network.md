---
title: Usar o PXE para implantação de sistema operacional pela rede
titleSuffix: Configuration Manager
description: Use implantações de sistema operacional iniciadas pelo PXE para atualizar o sistema operacional de um computador ou para instalar uma nova versão do Windows em um novo computador.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4c6069f81c9a5d086ef7c3ed13312d4f878d524a
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384084"
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-configuration-manager"></a>Usar o PXE para implantar o Windows pela rede com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As implantações de sistema operacional iniciadas pelo PXE (Pre-Boot Execution Environment) no System Center Configuration Manager permitem que os computadores cliente solicitem e implantem sistemas operacionais pela rede. Nesse cenário de implantação, você envia a imagem do sistema operacional e as imagens de inicialização para um ponto de distribuição habilitado para PXE.

> [!NOTE]  
>  Quando você cria uma implantação de sistema operacional direcionada somente a computadores com BIOS x64, ambas as imagens de inicialização x64 e x86 devem estar disponíveis no ponto de distribuição.

Use as implantações de sistema operacional iniciadas pelo PXE nos seguintes cenários:

-   [Atualizar um computador existente com uma nova versão do Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows)  

-   [Instalar uma nova versão do Windows em um novo computador (sem sistema operacional)](/sccm/osd/deploy-use/install-new-windows-version-new-computer-bare-metal)  

Conclua as etapas de um dos cenários de implantação de sistema operacional e, em seguida, use as seções deste artigo para preparar implantações iniciadas pelo PXE.



##  <a name="BKMK_Configure"></a> Configurar pelo menos um ponto de distribuição para aceitar solicitações PXE

Para implantar sistemas operacionais em clientes do Configuration Manager que fazem solicitações de inicialização PXE, você deve configurar um ou mais pontos de distribuição para aceitar solicitações PXE. Depois de configurar o ponto de distribuição, ele responde às solicitações de inicialização PXE e determina a ação de implantação apropriada a ser tomada. Para mais informações, consulte [Instalar ou modificar um ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="prepare-a-pxe-enabled-boot-image"></a>Preparar uma imagem de inicialização habilitada para PXE

Para usar o PXE para implantar um sistema operacional, você precisa ter imagens de inicialização x86 e x64 habilitadas para PXE distribuídas para um ou mais pontos de distribuição habilitados para PXE. Use as informações para habilitar o PXE em uma imagem de inicialização e distribuí-la para pontos de distribuição:

-   Para habilitar o PXE em uma imagem de inicialização, selecione **Implantar esta imagem de inicialização do ponto de distribuição habilitado para PXE** na guia **Fonte de Dados** nas propriedades da imagem de inicialização.

-   Se você alterar as propriedades da imagem de inicialização, distribua novamente a imagem de inicialização para os pontos de distribuição. Para obter mais informações, consulte [Distribuir conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).



##  <a name="BKMK_PXEExclusionList"></a> Criar uma lista de exclusões para implantações PXE

Ao implantar sistemas operacionais com o PXE, você pode criar uma lista de exclusões em cada ponto de distribuição. Adicione os endereços MAC à lista de exclusões dos computadores dos quais o ponto de distribuição você quer ignorar. Os computadores listados não recebem as sequências de tarefas de implantação usadas pelo Configuration Manager para a implantação PXE.

#### <a name="to-create-the-exclusion-list"></a>Para criar a lista de exclusão

1.  Crie um arquivo de texto no ponto de distribuição habilitado para PXE. Por exemplo, nomeie esse arquivo de texto **pxeExceptions.txt**.  

2.  Use um editor de texto sem formatação, como o Bloco de Notas, e adicione os endereços MAC dos computadores a serem ignorados pelo ponto de distribuição habilitado para PXE. Separe os valores de endereço MAC por dois-pontos e, em seguida, digite cada endereço em uma linha separada. Por exemplo: `01:23:45:67:89:ab`  

3.  Salve o arquivo de texto no servidor do sistema de site do ponto de distribuição habilitado para PXE. O arquivo de texto pode ser salvo em qualquer local no servidor.  

4.  Edite o registro do ponto de distribuição habilitado para PXE para criar uma chave do Registro **MACIgnoreListFile**. Adicione o valor de cadeia de caracteres do caminho completo até o arquivo de texto no servidor do sistema de sites do ponto de distribuição habilitado para PXE. Use o seguinte caminho do registro:  

     `HKLM\Software\Microsoft\SMS\DP`  

    > [!WARNING]  
    >  Se você usar o Editor do Registro incorretamente, você poderá causar sérios problemas e possivelmente precisará reinstalar o sistema operacional. A Microsoft não garante que você conseguirá resolver os problemas resultantes do uso incorreto do Editor do Registro. Use o Editor do Registro por sua conta e risco.  

5. Reinicie o serviço WDS ou o serviço de respondente PXE depois de alterar esse Registro. Você não precisa reiniciar o servidor.<!--512129-->  



## <a name="manage-duplicate-hardware-identifiers"></a>Gerenciar identificadores de hardware duplicados

O Configuration Manager pode reconhecer vários computadores como o mesmo dispositivo se eles têm atributos SMBIOS duplicados ou se você usa um adaptador de rede compartilhado. Atenue esses problemas gerenciando os identificadores de hardware duplicados nas configurações da hierarquia. Para obter mais informações, consulte [Gerenciar identificadores de hardware duplicados](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers).



##  <a name="BKMK_RamDiskTFTP"></a> Tamanho do bloco e da janela do RamDisk TFTP

Personalize o tamanho do bloco e da janela do RamDisk TFTP nos pontos de distribuição habilitados para PXE. Se você personalizou a rede, um tamanho grande de bloco ou de janela pode fazer com que o download da imagem de inicialização falhe com um erro de tempo limite. As personalizações de tamanho do bloco e da janela do RamDisk TFTP permitem otimizar o tráfego TFTP ao usar o PXE para atender aos seus requisitos de rede específicos. Para determinar qual configuração é a mais eficiente, teste as configurações personalizadas no ambiente. Para obter mais informações, consulte [Personalizar o tamanho do bloco e da janela do RamDisk TFTP nos pontos de distribuição habilitados para PXE](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_RamDiskTFTP).



## <a name="configure-deployment-settings"></a>Definir configurações de implantação

Para usar uma implantação de sistema operacional iniciada pelo PXE, configure a implantação para disponibilizar o sistema operacional para solicitações de inicialização PXE. Configure os sistemas operacionais disponíveis na guia **Configurações de Implantação** nas propriedades de implantação. Para a configuração **Tornar disponível para o seguinte**, selecione uma das seguintes opções:

-   Clientes do Configuration Manager, mídia e PXE

-   Somente mídia e PXE

-   Somente mídia e PXE (oculto)



##  <a name="BKMK_Deploy"></a> Implantar a sequência de tarefas

Implante o sistema operacional em uma coleção de destino. Para obter mais informações, consulte [Deploy a task sequence](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS). Ao implantar sistemas operacionais usando o PXE, é possível configurar se a implantação será necessária ou estará disponível.

-   **Implantação necessária**: as implantações necessárias usam o PXE sem nenhuma intervenção do usuário. O usuário não pode ignorar a inicialização PXE. No entanto, se o usuário cancelar a inicialização PXE antes da resposta do ponto de distribuição, o sistema operacional não será implantado.

-   **Implantação disponível**: as implantações disponíveis exigem que o usuário esteja presente no computador de destino. O usuário precisa pressionar a tecla **F12** para continuar o processo de inicialização do PXE. Se não houver um usuário presente para pressionar **F12**, o computador será inicializado no sistema operacional atual ou pelo próximo dispositivo de inicialização disponível.

É possível reimplantar uma implantação PXE necessária apagando o status da última implantação PXE atribuída a uma coleção do Configuration Manager ou a um computador. Para obter mais informações sobre a ação **Limpar Implantações PXE Necessárias**, consulte [Gerenciar clientes](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode) ou [Gerenciar coleções](/sccm/core/clients/manage/collections/manage-collections#how-to-manage-device-collections). Essa ação redefine o status dessa implantação e reinstala as implantações necessárias mais recentes.

> [!IMPORTANT]  
> O protocolo PXE não é seguro. Verifique se o servidor PXE e o cliente PXE estão localizados em uma rede fisicamente segura, como um data center, para evitar acesso não autorizado ao site.



##  <a name="how-is-the-boot-image-selected-for-clients-booting-with-pxe"></a>Como a imagem de inicialização é selecionada para clientes sendo inicializados com o PXE?

Quando um cliente é inicializado com o PXE, o Configuration Manager fornece ao cliente uma imagem de inicialização para usar. O Configuration Manager usa uma imagem de inicialização com uma correspondência exata de arquitetura. Se uma imagem de inicialização com a arquitetura exata não estiver disponível, o Configuration Manager usará uma imagem de inicialização com uma arquitetura compatível. 

A lista a seguir fornece detalhes sobre como uma imagem de inicialização é selecionada para os clientes inicializados com o PXE:  

1. O Configuration Manager examina o banco de dados do site para buscar o Registro do sistema que corresponde ao endereço MAC ou ao SMBIOS do cliente que está tentando ser inicializado.  

    > [!NOTE]  
    > Se um computador atribuído a um site for inicializado para PXE para um site diferente, as políticas não ficarão visíveis para o computador. Por exemplo, se um cliente já estiver atribuído ao site A, o ponto de gerenciamento e o ponto de distribuição do site B não poderão acessar as políticas do site A. O cliente não fará a inicialização PXE com êxito.  

2. O Configuration Manager procura sequências de tarefas implantadas no registro do sistema encontradas na etapa 1.  

3. Na lista de sequências de tarefas encontrada na etapa 2, o Configuration Manager procura uma imagem de inicialização que corresponde à arquitetura do cliente que está tentando ser inicializado. Se uma imagem de inicialização é encontrada com a mesma arquitetura, ela é usada.  

4. Se não for encontrada uma imagem de inicialização com a mesma arquitetura, o Configuration Manager buscará uma imagem de inicialização que seja compatível com a arquitetura do cliente. Ele procura na lista de sequências de tarefas encontrada na etapa 2. Por exemplo, um cliente de 64 bits é compatível com imagens de inicialização de 32 bits e 64 bits. Um cliente de 32 bits é compatível apenas com imagens de inicialização de 32 bits. Um cliente UEFI é compatível apenas com imagens de inicialização de 64 bits.  
