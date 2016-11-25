---
title: "Pré-provisionar o BitLocker no Windows PE | Configuration Manager"
description: "A tarefa de Pré-provisionar o BitLocker no Configuration Manager habilita o BitLocker no Ambiente de Pré-Instalação do Windows antes da implantação de sistema operacional."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c7c94ba0-d709-4129-8077-075a8abaea1c
caps.latest.revision: 4
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f047e4a7c9325e0f8662b4f567529fd439c76b0c


---
# <a name="preprovision-bitlocker-in-windows-pe-with-system-center-configuration-manager"></a>Pré-provisionar o BitLocker no Windows PE com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A etapa da sequência de tarefas **Pré-provisionar o BitLocker** do System Center Configuration Manager permite habilitar o BitLocker no Ambiente de Pré-Instalação do Windows (Windows PE) antes da implantação do sistema operacional. Apenas o espaço em disco usado é criptografado e, portanto, os tempos de criptografia são muito mais rápidos. Para isso, um protetor de limpeza gerado aleatoriamente é aplicado ao volume formatado, e o volume é criptografado antes da execução do processo de instalação do Windows. A capacidade de pré-provisionar o BitLocker foi introduzida com o Windows 8 e Windows Server 2012. No entanto, é possível pré-provisionar o BitLocker em um disco rígido e instalar o Windows 7 contanto que você siga as etapas específicas. Uma vez concluída a Instalação do Windows 7, você deve definir um protetor de chave BitLocker porque o painel de controle do BitLocker do Windows 7 não oferece suporte ao BitLocker com um protetor de limpeza. Você deve adicionar um protetor de chave usando a etapa **Habilitar BitLocker** ou a ferramenta de linha de comando manage-bde.exe.  

 Em geral, você deve fazer o seguinte para pré-provisionar com êxito o BitLocker em um computador que instalará o Windows 7:  

-   Reinicie o computador no Windows PE  

    > [!IMPORTANT]  
    >  Você deve usar uma imagem de inicialização com o Windows PE 4 ou posterior para pré-provisionar o BitLocker. Para obter mais informações sobre as versões do Windows PE com suporte no Configuration Manager, consulte [Dependências externas ao Configuration Manager](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_ExternalDependencies).  

-   Particione e formate o disco rígido  

-   Pré-provisionar o BitLocker  

-   Instale o Windows 7 com as configurações específicas de rede e sistema operacional  

-   Adicione um protetor de chave ao BitLocker  

 No Configuration Manager, a maneira recomendada de pré-provisionar o BitLocker em um disco rígido e instalar o Windows 7 é criar uma nova sequência de tarefas e selecionar **Instalar um pacote de imagem existente** na página **Criar Nova Sequência de Tarefas** do **Assistente para Criar Sequência de Tarefas**. O assistente cria as etapas da sequência de tarefas listadas na tabela a seguir.  

> [!NOTE]  
>  A sequência de tarefas poderá ter mais etapas dependendo de como você tiver definido as configurações no assistente. Por exemplo, você poderá ter a etapa **Capturar Configurações do Windows** se tiver selecionado **Configurações do Microsoft Windows capturadas** na página **Migração de Estado** do assistente.  

|Etapa da sequência de tarefas|Detalhes|  
|------------------------|-------------|  
|Desabilitar BitLocker|Esta etapa desabilitará a criptografia do BitLocker se ela estiver habilitada no momento. Para mais informações, consulte [Desabilitar BitLocker](../understand/task-sequence-steps.md#BKMK_DisableBitLocker).|  
|Reiniciar o computador no Windows PE|Esta etapa reinicia o computador no Windows PE executando a imagem de inicialização atribuída à sequência de tarefas. Você deve usar uma imagem de inicialização com o Windows PE 4 ou posterior para pré-provisionar o BitLocker. Para mais informações, consulte [Reiniciar Computer](../understand/task-sequence-steps.md#BKMK_RestartComputer).|  
|Particionar Disco 0 - BIOS<br /><br /> Particionar Disco 0 – UEFI|Estas etapas formatam e particionam a unidade especificada no computador de destino usando BIOS ou UEFI. A sequência de tarefas usa UEFI quando detecta que o computador de destino está no modo UEFI. Para mais informações, consulte [Formatar e Particionar Disco](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk).|  
|Pré-provisionar o BitLocker|Esta etapa habilita o BitLocker em uma unidade durante a execução do Windows PE. Somente o espaço em disco utilizado é criptografado. Como você particionou e formatou o disco rígido na etapa anterior, não há dados, e a criptografia é concluída de maneira muito rápida. Para mais informações, consulte [Pré-provisionar o BitLocker](../understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker).|  
|Aplicar Sistema Operacional|Esta etapa prepara o arquivo de resposta usado para instalar o sistema operacional no computador de destino e define a variável de sequência de tarefas OSDTargetSystemDrive como a letra da unidade da partição que contém os arquivos do sistema operacional. O arquivo de resposta e a variável são usados pela etapa Instalar Windows e ConfigMgr para instalar o sistema operacional. Para obter mais informações, consulte [Apply Operating System Image](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).|  
|Aplicar as Configurações do Windows|Esta etapa adiciona as configurações do Windows ao arquivo de resposta. O arquivo de resposta é usado pela etapa Instalar Windows e ConfigMgr para instalar o sistema operacional. Para mais informações, consulte [Aplicar as Configurações do Windows](../understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings).|  
|Aplicar Configurações de Rede|Esta etapa adiciona as configurações de rede ao arquivo de resposta. O arquivo de resposta é usado pela etapa Instalar Windows e ConfigMgr para instalar o sistema operacional. Para mais informações, consulte [Aplicar a Etapa de Configurações de Rede](../understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings).|  
|Aplicar Drivers de Dispositivo|Esta etapa faz a correspondência dos drivers e instala-os como parte da implantação do sistema operacional. Para mais informações, consulte [Aplicar Drivers Automaticamente](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).|  
|Instalar Windows e ConfigMgr|Esta etapa faz a transição do Windows PE para o novo sistema operacional. Esta etapa da sequência de tarefas é necessária em qualquer implantação de sistema operacional. Ele instala o cliente do Configuration Manager no novo sistema operacional e prepara a sequência de tarefas para continuar a execução no novo sistema operacional. Para mais informações, consulte [Configurar Windows e ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).|  
|Habilitar BitLocker|Esta etapa habilita a criptografia BitLocker no disco rígido e define os protetores de chave. Como o disco rígido foi pré-provisionado com o BitLocker, esta etapa é concluída de maneira muito rápida. Para o Windows 7, é necessário adicionar um protetor de chave. Se não usar esta etapa, você poderá executar a ferramenta de linha de comando manage-bde.exe para definir um protetor de chave. Para mais informações, consulte [Habilitar BitLocker](../understand/task-sequence-steps.md#BKMK_EnableBitLocker).|  



<!--HONumber=Nov16_HO1-->


