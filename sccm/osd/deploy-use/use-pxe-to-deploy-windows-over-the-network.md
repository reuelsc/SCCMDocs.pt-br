---
title: Usar PXE para implantar o Windows na rede | Microsoft Docs
description: "Use implantações de sistema operacional iniciadas pelo PXE para atualizar o sistema operacional de um computador ou para instalar uma nova versão do Windows em um novo computador."
ms.custom: na
ms.date: 12/07/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
caps.latest.revision: 19
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3f44505c977b511223a083a960f871371c0ff133
ms.openlocfilehash: b22cdbd42693078caa47f41182ce73ea881c3515


---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Use o PXE para implantar o Windows pela rede com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As implantações de sistema operacional iniciadas pelo PXE no System Center Configuration Manager permitem que os computadores cliente solicitem e implantem sistemas operacionais pela rede. Nesse cenário de implantação de sistema operacional, a imagem do sistema operacional e ambas as imagens de inicialização do x86 e x64 do Windows PE são enviadas para um ponto de distribuição configurado para aceitar solicitações de inicialização PXE.  

> [!NOTE]  
>  Quando você cria uma implantação de sistema operacional que se destina somente a computadores com BIOS x64, ambas as imagens de inicialização x64 e x86 devem estar disponíveis no ponto de distribuição.  

 É possível usar implantações de sistema operacional iniciadas pelo PXE nos seguintes cenários de implantação de sistema operacional:  

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar uma nova versão do Windows em um novo computador (sem sistema operacional)](install-new-windows-version-new-computer-bare-metal.md)  

 Conclua as etapas em um dos cenários de implantação de sistema operacional e use as seções a seguir para preparar implantações iniciadas pelo PXE.  

##  <a name="a-namebkmkconfigurea-configure-at-least-one-distribution-point-to-accept-pxe-requests"></a><a name="BKMK_Configure"></a> Configurar pelo menos um ponto de distribuição para aceitar solicitações PXE  
 Para implantar sistemas operacionais em clientes do Configuration Manager que fazem solicitações de inicialização PXE, é necessário usar um ou mais pontos de distribuição que estão configurados para responder às solicitações de inicialização PXE.  Para obter as etapas necessárias para habilitar o PXE em um ponto de distribuição, consulte [Configuring distribution points to accept PXE requests (Configurando pontos de distribuição para aceitar solicitações PXE)](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint).  

## <a name="prepare-a-pxe-enabled-boot-image"></a>Preparar uma imagem de inicialização habilitada para PXE  
 Para usar PXE para implantar um sistema operacional, você precisa ter imagens de inicialização x86 e x64 habilitadas para PXE distribuídas para um ou mais pontos de distribuição habilitados para PXE. Use as informações para habilitar o PXE em uma imagem de inicialização e distribuí-la para pontos de distribuição:  

-   Para habilitar o PXE em uma imagem de inicialização, selecione  **Implantar esta imagem de inicialização do ponto de distribuição habilitado para PXE** na guia **Fonte de Dados** nas propriedades da imagem de inicialização.  

-   Se você alterar as propriedades da imagem de inicialização, distribua novamente a imagem de inicialização para os pontos de distribuição. Para obter mais informações, consulte [Distribuir conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content).  

##  <a name="a-namebkmkpxeexclusionlista-create-an-exclusion-list-for-pxe-deployments"></a><a name="BKMK_PXEExclusionList"></a> Criar uma lista de exclusões para implantações PXE  
 Ao usar PXE para implantar sistemas operacionais, você pode criar uma lista de exclusões em cada ponto de distribuição para ignorar solicitações de inicialização PXE de computadores que estão na lista de exclusões. A lista de exclusões contém endereços MAC de computadores que você deseja que o ponto de distribuição ignore. Esses computadores não receberão sequências de tarefas de implantação que o Configuration Manager usa para a implantação PXE.  

 Use as seguintes etapas para criar a lista de exclusão do PXE.  

#### <a name="to-create-the-exclusion-list"></a>Para criar a lista de exclusão  

1.  Crie um arquivo de texto no ponto de distribuição habilitado para PXE. Por exemplo, nomeie esse arquivo de texto **pxeExceptions.txt**.  

2.  Use um editor de texto padrão, como o Bloco de Notas, e adicione os endereços MAC dos computadores a serem ignorados pelo ponto de distribuição habilitado para PXE. Separe os valores de endereço MAC por dois-pontos e, em seguida, digite cada endereço em uma linha separada. Por exemplo: `01:23:45:67:89:ab`  

3.  Salve o arquivo de texto no servidor do sistema de site do ponto de distribuição habilitado para PXE. O arquivo de texto pode ser salvo em qualquer local no servidor.  

4.  Edite o registro do ponto de distribuição habilitado para PXE para criar uma chave do registro do **MACIgnoreListFile** que contém um valor de sequência do caminho completo da localização do arquivo de texto no servidor do sistema de site do ponto de distribuição habilitado para PXE. Use o seguinte caminho do registro:  

     **HKLM\Software\Microsoft\SMS\DP**  

    > [!WARNING]  
    >  Se você usar o Editor do Registro incorretamente, você poderá causar sérios problemas e possivelmente precisará reinstalar o sistema operacional. A Microsoft não garante que você conseguirá resolver os problemas resultantes do uso incorreto do Editor do Registro. Use o Editor do Registro por sua conta e risco.  

     Não é necessário reiniciar o servidor após você alterar esse registro.  

##  <a name="a-namebkmkramdisktftparamdisk-tftp-block-size-and-window-size"></a><a name="BKMK_RamDiskTFTP"></a> Tamanho do bloco e da janela do RamDisk TFTP  
É possível personalizar o tamanho do bloco e da janela do RamDisk TFTP, e partir do Configuration Manager versão 1606, o tamanho da janela para pontos de distribuição habilitados pelo PXE. Se você tiver personalizado sua rede, isso poderá fazer com que o download da imagem de inicialização falhe com um erro de tempo limite devido ao tamanho muito grande do bloco ou da janela. A personalização do tamanho do bloco e da janela do RamDisk TFTP permite otimizar o tráfego TFTP ao usar o PXE para atender aos seus requisitos de rede específicos. Você precisará testar as configurações personalizadas no ambiente para determinar o que é mais eficiente. Para obter mais informações, consulte [Personalizar o tamanho do bloco e da janela do RamDisk TFTP nos pontos de distribuição habilitados para PXE](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="configure-deployment-settings"></a>Definir configurações de implantação  
 Para usar uma implantação de sistema operacional iniciada pelo PXE, é necessário configurar a implantação para disponibilizar o sistema operacional para solicitações de inicialização PXE. Você pode configurá-la na página **Configurações de implantação** do Assistente de implantação de Software ou na guia **Configurações de implantação** nas propriedades de implantação.  Para a configuração **Tornar disponível para o seguinte** , defina uma das seguintes opções:  

-   Clientes do Configuration Manager, mídia e PXE  

-   Somente mídia e PXE  

-   Somente mídia e PXE (oculto)  

##  <a name="a-namebkmkdeploya-deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Implantar a sequência de tarefas  
 Implantar o sistema operacional em uma coleção de destino. Para obter mais informações, consulte [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Ao implantar sistemas operacionais usando o PXE, é possível configurar se a implantação será necessária ou estará disponível.  

-   **Implantação necessária**: as implantações necessárias usarão o PXE sem nenhuma intervenção do usuário. O usuário não poderá ignorar a inicialização PXE. No entanto, se o usuário cancelar a inicialização PXE antes de o ponto de distribuição responder, o sistema operacional não será implantado.  

-   **Implantação disponível**: as implantações disponíveis requerem que o usuário esteja presente no computador de destino para que o usuário pressione a tecla F12 para continuar o processo de inicialização PXE. Se o usuário não estiver presente para pressionar F12, o computador será inicializado no atual sistema operacional ou do próximo dispositivo de inicialização disponível.  

 É possível reimplantar uma implantação PXE necessária apagando o status da última implantação PXE atribuída a uma coleção do Configuration Manager ou a um computador. Essa ação redefine o status dessa implantação e reimplanta as implantações necessárias mais recentes.  

> [!IMPORTANT]  
>  O protocolo PXE não é seguro. Verifique se o servidor PXE e o cliente PXE estão localizados em uma rede fisicamente segura, como um data center, para evitar acesso não autorizado ao site.  

##  <a name="how-is-the-boot-image-selected-for-clients-booting-with-pxe"></a>Como a imagem de inicialização é selecionada para clientes sendo inicializados com o PXE?
Quando um cliente é inicializado com o PXE, o Configuration Manager fornece ao cliente uma imagem de inicialização para usar. A partir do Configuration Manager versão 1606, o Configuration Manager usará uma imagem de inicialização com uma correspondência de arquitetura exata, se houver uma disponível. Se uma imagem de inicialização com a arquitetura exata não estiver disponível, o Configuration Manager usará uma imagem de inicialização com uma arquitetura compatível. A lista a seguir fornece detalhes sobre como uma imagem de inicialização é selecionada para clientes sendo inicializados com o PXE.
1. O Configuration Manager examina o banco de dados do site para o registro do sistema que coincide com o endereço MAC ou o SMBIOS do cliente que está tentando inicializar.
    > [!NOTE]
    > Se um computador atribuído a um site inicializar para PXE para um site diferente, as políticas não estarão visíveis para o computador. Por exemplo, se um cliente já está atribuído a um site A, o ponto de gerenciamento e ponto de distribuição no site B não poderão acessar as políticas do site A e o cliente não fará a inicialização PXE com êxito.
2. O Configuration Manager procura sequências de tarefas implantadas no registro do sistema encontradas na etapa 1.
3. Na lista de sequências de tarefas encontrada na etapa 2, o Configuration Manager procura uma imagem de inicialização que corresponde à arquitetura do cliente que está tentando inicializar. Se uma imagem de inicialização é encontrada com a mesma arquitetura, ela é usada.

4. Se uma imagem de inicialização não é encontrada com a mesma arquitetura, o Configuration Manager procura uma imagem de inicialização (na lista de sequências de tarefas encontrada na etapa 2) compatível com a arquitetura do cliente que está tentando inicializar. Por exemplo, um cliente de 64 bits é compatível com imagens de inicialização de 32 bits e 64 bits. Um cliente de 32 bits é compatível apenas com imagens de inicialização de 32 bits. Um cliente UEFI é compatível apenas com imagens de inicialização de 64 bits.



<!--HONumber=Dec16_HO3-->


