---
title: "Introdução à implantação de sistema operacional"
titleSuffix: Configuration Manager
description: Entenda os conceitos antes de implantar sistemas operacionais no ambiente do seu Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d9a1c545-8301-492c-832f-2c108ff93c77
caps.latest.revision: "12"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 5835bde38cb940d2e38df4a38146753a6842f1d7
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="introduction-to-operating-system-deployment-in-system-center-configuration-manager"></a>Introdução à implantação de sistema operacional no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

É possível usar o Configuration Manager para implantar sistemas operacionais de inúmeras maneiras diferentes. Use as informações desta seção para entender como implantar sistemas operacionais e automatizar tarefas. 

##  <a name="BKMK_OSDeploymentProcess"></a> O processo de implantação de sistema operacional  
 O Configuration Manager fornece diversos métodos que podem ser usados para implantar um sistema operacional. Existem várias ações que devem ser tomadas, independentemente do método de implantação utilizado:  

-   Identifique os drivers de dispositivo Windows necessários para iniciar a imagem de inicialização ou instalar a imagem do sistema operacional que deve ser implantada.  

-   Identifique a imagem de inicialização que deseja usar para iniciar o computador de destino.  

-   Use uma sequência de tarefas para capturar uma imagem do sistema operacional que deseja implantar. Como alternativa, é possível usar uma imagem do sistema operacional padrão.  

-   Distribuir a imagem de inicialização, a imagem do sistema operacional e qualquer conteúdo relacionado a um ponto de distribuição.  

-   Crie uma sequência de tarefas com as etapas para implantar a imagem de inicialização e a imagem do sistema operacional.  

-   Implante a sequência de tarefas em uma coleção de computadores.  

-   Monitore a implantação.  

##  <a name="BKMK_OSDScenarios"></a> Cenários de implantação de sistema operacional  
 Há vários cenários de implantação de sistema operacional no Configuration Manager que podem ser escolhidos, dependendo de seu ambiente e da finalidade da instalação do sistema operacional.  Por exemplo, é possível particionar e formatar um computador existente com uma nova versão do Windows ou atualizar o Windows para a versão mais recente. Para ajudá-lo a determinar o método de implantação que atende às suas necessidades, examine [Scenarios to deploy enterprise operating systems (Cenários para implantar sistemas operacionais corporativos)](../deploy-use/scenarios-to-deploy-enterprise-operating-systems.md).  É possível escolher um dos seguintes cenários de implantação de sistema operacional:  

-   [Atualizar o Windows para a versão mais recente](../deploy-use/upgrade-windows-to-the-latest-version.md)  

-   [Atualizar um computador existente com uma nova versão do Windows](../deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar uma nova versão do Windows em um novo computador (sem sistema operacional)](../deploy-use/install-new-windows-version-new-computer-bare-metal.md)  

-   [Substituir um computador existente e transferir configurações](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="BKMK_OSDMethods"></a> Métodos para implantar sistemas operacionais  
 Existem vários métodos que podem ser usados para implantar sistemas operacionais em computadores cliente do Configuration Manager.  

-   **Implantações iniciadas pelo PXE**: as implantações iniciadas pelo PXE permitem que computadores cliente solicitem uma implantação por meio da rede. Nesse método de implantação, a imagem do sistema operacional e uma imagem de inicialização do Windows PE são enviadas a um ponto de distribuição configurado para aceitar solicitações de inicialização PXE. Para obter mais informações, consulte [Use o PXE para implantar o Windows pela rede com o System Center Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

-   **Disponibilizar sistemas operacionais no Centro de Software**: é possível implantar um sistema operacional e disponibilizá-lo no Centro de Software. Os clientes do Configuration Manager podem iniciar a instalação do sistema operacional no Centro de Software. Para mais informações, consulte [Replace an existing computer and transfer settings (Substituir um computador existente e transferir configurações)](../deploy-use/replace-an-existing-computer-and-transfer-settings.md).  

-   **Implantações multicast**: as implantações multicast conservam a largura de banda da rede enviando simultaneamente dados a vários clientes, em vez de enviar uma cópia dos dados a cada cliente por uma conexão separada. Nesse método de implantação, a imagem do sistema operacional é enviada para um ponto de distribuição. Isso, por sua vez, implanta a imagem quando os computadores cliente solicitam a implantação. Para mais informações, consulte [Usar o multicast para implantar o Windows pela rede](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

-   **Implantações de mídia inicializável**: as implantações de mídia inicializável permitem implantar o sistema operacional quando o computador de destino é iniciado. Quando o computador de destino é iniciado, ele se conecta à rede e recupera a sequência de tarefas, a imagem do sistema operacional e qualquer outro conteúdo necessário da rede. Como esse conteúdo não está incluído na mídia, você pode atualizar o conteúdo sem precisar recriar a mídia. Para obter mais informações, consulte [Criar mídia inicializável](../deploy-use/create-bootable-media.md).  

-   **Implantações de mídia autônoma**: as implantações de mídia autônoma permitem implantar sistemas operacionais com as seguintes condições:  

    -   Em ambientes onde não é prático copiar uma imagem do sistema operacional ou outros pacotes grandes através da rede.  

    -   Em ambientes sem conectividade de rede ou conectividade de rede de baixa largura de banda.  

     Para obter mais informações, consulte [Criar mídia autônoma](../deploy-use/create-stand-alone-media.md).  

-   **Implantações de mídia pré-configurada**: as implantações de mídia pré-configurada permitem implantar um sistema operacional em um computador que não está totalmente provisionado. A mídia pré-configurada é um arquivo em formato WIM (Windows Imaging) que pode ser instalado em um computador sem sistema operacional pelo fabricante ou em um centro de preparo corporativo que não está conectado ao ambiente do Configuration Manager.  

     Posteriormente, no ambiente do Configuration Manager, o computador será iniciado usando a imagem de inicialização fornecida pela mídia e será conectado ao ponto de gerenciamento do site para as sequências de tarefas disponíveis que concluem o processo de download. Esse método de implantação pode reduzir o tráfego de rede, pois a imagem de inicialização e a imagem do sistema operacional já estão no computador de destino. É possível especificar aplicativos, pacotes e pacotes de driver para incluir na mídia pré-configurada. Para mais informações, consulte [Criar mídia pré-configurada](../deploy-use/create-prestaged-media.md).  

##  <a name="BKMK_BootImages"></a> Imagens de inicialização  
 Uma imagem de inicialização no Configuration Manager é uma imagem do WinPE (Windows PE) usada durante uma implantação de sistema operacional. Imagens de inicialização são usadas para iniciar um computador no WinPE, que é um sistema operacional mínimo com componentes e serviços limitados que preparam o computador de destino para a instalação do Windows. O Configuration Manager fornece duas imagens de inicialização: uma para dar suporte a plataformas x86 e outra para dar suporte a plataformas x64. Elas são consideradas imagens de inicialização padrão. Imagens de inicialização criadas e adicionadas ao Configuration Manager são consideradas imagens personalizadas. Imagens de inicialização padrão podem ser substituídas automaticamente com a atualização do Configuration Manager. Para obter mais informações sobre imagens de inicialização, consulte [Gerenciar imagens de inicialização](../get-started/manage-boot-images.md).  

##  <a name="BKMK_OSImages"></a> Imagens do sistema operacional  
 As imagens do sistema operacional no Configuration Manager são armazenadas em arquivos de formato WIM (Windows Imaging) e representam uma coleção compactada de arquivos e pastas de referência necessários para instalar e configurar com êxito um sistema operacional em um computador. Para todos os cenários de implantação de sistema operacional, você deve selecionar uma imagem do sistema operacional. É possível usar a imagem do sistema operacional padrão ou compilar a imagem do sistema operacional de um computador de referência configurado. Para obter mais informações, consulte [Gerenciar imagens do sistema operacional](../get-started/manage-operating-system-images.md).  

##  <a name="BKMK_OSUpgradePackages"></a> Pacotes de atualização de sistema operacional  
 Pacotes de atualização do sistema operacional são usados para atualizar um sistema operacional e são implantações de sistema operacional iniciadas pela instalação. Pacotes de atualização do sistema operacional são importados para o Configuration Manager de um DVD ou um arquivo ISO montado. Para obter mais informações, consulte [Gerenciar pacotes de atualização do sistema operacional](../get-started/manage-operating-system-upgrade-packages.md).  

##  <a name="BKMK_OSDMedia"></a> Mídia usada para implantar sistemas operacionais  
 Você pode criar vários tipos de mídia que pode ser usados para implantar sistemas operacionais. Isso inclui capturar mídia usada para capturar imagens do sistema operacional e mídia autônoma, em pré-teste e inicializável usada para implantar um sistema operacional. Com o uso da mídia, é possível implantar sistemas operacionais em computadores que não têm uma conexão de rede ou que têm uma conexão de baixa largura de banda no site do Configuration Manager. Para obter mais informações sobre como usar a mídia, consulte [Create task sequence media (Criar mídia de sequência de tarefas)](../deploy-use/create-task-sequence-media.md).  

##  <a name="BKMK_DeviceDrivers"></a> Drivers de dispositivo  
 É possível instalar drivers de dispositivo em computadores de destino sem incluí-los na imagem do sistema operacional que está sendo implantada. O Configuration Manager fornece um catálogo de drivers que contém referências a todos os drivers de dispositivos importados para o Configuration Manager. O catálogo de drivers está localizado no espaço de trabalho **Biblioteca de Software** e consiste em dois nós: **Drivers** e **Pacotes de Driver**. O nó **Drivers** lista todos os drivers que você importou no catálogo de drivers. Você pode usar esse nó para descobrir os detalhes sobre cada driver importado, para alterar a qual pacote de driver ou imagem de inicialização um driver pertence, para habilitar ou desabilitar um driver e muito mais. Para mais informações, consulte [Manage drivers (Gerenciar drivers)](../get-started/manage-drivers.md).  

##  <a name="BKMK_OSDUserState"></a> Salvar e restaurar o estado do usuário  
 Ao implantar sistemas operacionais, você pode salvar o estado do usuário do computador de destino, implantar o sistema operacional e restaurar o estado do usuário após a implantação de sistemas operacionais. Geralmente, esse processo é usado ao instalar o sistema operacional em um computador cliente do Configuration Manager.  

 As informações de estado do usuário são capturadas e restauradas usando sequências de tarefas. Quando as informações de estado do usuário são capturadas, elas podem ser armazenadas de uma das seguintes maneiras:  

-   Você pode armazenar os dados de estado do usuário remotamente, configurando um ponto de migração de estado. A sequência de tarefas de captura envia os dados para o ponto de migração de estado. Em seguida, após a implantação do sistema operacional, a sequência de tarefas de restauração recupera os dados e restaura o estado do usuário no computador de destino.  

-   Você pode armazenar os dados de estado do usuário localmente em um local específico. Nesse cenário, a sequência de tarefas de captura copia os dados do usuário para um local específico no computador de destino. Em seguida, após a implantação do sistema operacional, a sequência de tarefas de restauração recupera os dados do usuário desse local.  

-   Você pode especificar links físicos que podem ser usados para restaurar os dados do usuário para o local original. Nesse cenário, os dados de estado do usuário permanecem na unidade quando o sistema operacional antigo é removido. Em seguida, após a implantação do sistema operacional, a sequência de tarefas de restauração usa os links físicos para restaurar os dados de estado do usuário para o local original.  

 Para obter mais informações, consulte [Manage user state (Gerenciar o estado do usuário)](../get-started/manage-user-state.md).  

##  <a name="BKMK_UnknownComputer"></a> Implantar em computadores desconhecidos  
 É possível implantar um sistema operacional em computadores não gerenciados pelo Configuration Manager. Não há registro desses computadores no banco de dados do Configuration Manager. Esses computadores são chamados de computadores desconhecidos. Computadores desconhecidos incluem:  

-   Um computador no qual o cliente do Configuration Manager não está instalado  

-   Um computador que não foi importado para o Configuration Manager  

-   Um computador não descoberto pelo Configuration Manager  

 Para obter mais informações, consulte [Preparar implantações de computador desconhecido](../get-started/prepare-for-unknown-computer-deployments.md).  

##  <a name="BKMK_UDA"></a> Associar usuários a um computador  
 Ao implantar um sistema operacional, você pode associar usuários ao computador de destino para dar suporte a ações de afinidade de dispositivo de usuário. Quando você associa um usuário ao computador de destino, o usuário administrativo pode, mais tarde, realizar ações em qualquer computador associado a esse usuário, como implantar um aplicativo no computador de um usuário específico. No entanto, ao implantar um sistema operacional, você não pode implantá-lo no computador de um usuário específico. Para mais informações, consulte [Associar usuários a um computador de destino](../get-started/associate-users-with-a-destination-computer.md).  

##  <a name="BKMK_TaskSequences"></a> Usar sequências de tarefas para automatizar etapas  
 É possível criar sequências de tarefas para executar uma variedade de tarefas no ambiente do Configuration Manager. As ações da sequência de tarefas são definidas nas etapas individuais da sequência. Quando a sequência de tarefas é executada, as ações de cada etapa são executadas no nível de linha de comando sem exigir intervenção do usuário. É possível usar sequências de tarefas para o seguinte:  

-   [Criar uma sequência de tarefas para instalar um sistema operacional](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md)  

-   [Criar uma sequência de tarefas para implantações que não são de sistema operacional](../deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)  

-   [Criar uma sequência de tarefas para capturar um sistema operacional](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)  

-   [Criar uma sequência de tarefas para capturar e restaurar o estado do usuário](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)  

-   [Criar uma sequência de tarefas personalizada](../deploy-use/create-a-custom-task-sequence.md)  
