---
title: "Etapas de sequência de tarefas para gerenciar o BIOS para a conversão de UEFI | Configuration Manager"
description: "Saiba como personalizar uma sequência de tarefas de implantação do sistema operacional para preparar uma partição FAT32 para a transição para UEFI."
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 528ce515c86c4e778532290026a90a46476c4576
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Etapas de sequência de tarefas para gerenciar o BIOS para a conversão de UEFI
O Windows 10 oferece muitos novos recursos de segurança que exigem dispositivos habilitados para UEFI. Você pode ter PCs modernos com Windows que oferecem suporte a UEFI, mas que usam BIOS herdada. Converter um dispositivo em UEFI exigiria realizar a operação em cada computador, reparticionar o disco rígido e reconfigurar o firmware. Ao usar as sequências de tarefas no Configuration Manager, você poderá preparar um disco rígido para o BIOS para a conversão de UEFI, converter do BIOS para UEFI como parte do processo de atualização in-loco e coletar informações de UEFI como parte do inventário de hardware.

## <a name="hardware-inventory-collects-uefi-information"></a>O inventário de hardware coleta informações de UEFI
A partir de 1702, uma nova classe de inventário de hardware (**SMS_Firmware**) e a propriedade (**UEFI**) estão disponíveis para ajudá-lo a determinar se um computador é iniciado no modo UEFI. Quando um computador é iniciado no modo UEFI, a propriedade **UEFI** é definida como **TRUE**. Isso é habilitado no inventário de hardware por padrão. Para obter mais informações sobre o inventário de hardware, consulte [Como configurar o inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive-for-bios-to-uefi-conversion"></a>Criar uma sequência de tarefas personalizada para preparar o disco rígido para a conversão de BIOS para UEFI
Agora, começando do Configuration Manager versão 1610, é possível personalizar uma sequência de tarefas de implantação do sistema operacional com uma nova variável, TSUEFIDrive, para que a etapa **Reiniciar o Computador** prepare uma partição FAT32 no disco rígido para a transição para UEFI. O procedimento a seguir fornece um exemplo de como você pode criar etapas de sequência de tarefas para preparar o disco rígido para a conversão de BIOS para UEFI.

### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Para preparar a partição FAT32 para a conversão para UEFI:
Em uma sequência de tarefas existente para instalar um sistema operacional, você adicionará um novo grupo com etapa para realizar a conversão de BIOS para UEFI.

1. Crie um novo grupo de sequências de tarefas após as etapas para capturar arquivos e configurações e antes das etapas para instalar o sistema operacional. Por exemplo, crie um grupo após o grupo de **Capturar Arquivos e Configurações** denominado **BIOS-to-UEFI (BIOS para UEFI)**.
2. Na guia **Opções** do novo grupo, adicione uma nova variável de sequência de tarefas como uma condição em que **_SMSTSBootUEFI** é **diferente** de **true**. Isso impede que as etapas no grupo sejam executadas quando um computador já estiver no modo UEFI.

  ![Grupo BIOS para UEFI](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. No novo grupo, adicione a etapa de sequência de tarefas **Reiniciar Computador**. Em **Especifique o que executar após reiniciar**, selecione **The boot image assigned to this task sequence is selected (A imagem de inicialização atribuída a essa sequência de tarefas está selecionada)** para iniciar o computador no Windows PE.  
4. Na guia **Opções**, adicione uma variável de sequência de tarefa como uma condição em que **_SMSTSInWinPE equals false (_SMSTSInWinPE é igual a falso)**. Isso impede que esta etapa seja executada se o computador já estiver no Windows PE.

  ![Etapa Reiniciar Computador](../../core/get-started/media/restart-in-windows-pe.png)
5. Adicione uma etapa para iniciar a ferramenta de OEM que converterá o firmware de BIOS para UEFI. Isso geralmente será uma etapa de sequência de tarefas **Executar Linha de Comando** com uma linha de comando para iniciar a ferramenta de OEM.
6. Adicione a etapa de sequência de tarefas Formatar e Particionar Disco que particionará e formatará o disco rígido. Na etapa, faça o seguinte:
  1. Crie a partição FAT32 que será convertida em UEFI antes de o sistema operacional ser instalado. Escolha **GGT** para **Tipo de disco**.
    ![Etapa Formatar e particionar disco](../media/format-and-partition-disk.png)
  2. Vá para as propriedades da partição FAT32. Digite **TSUEFIDrive** no campo **Variável**. Quando a sequência de tarefas detectar essa variável, ela preparará para a transição de UEFI antes de reiniciar o computador.
    ![Propriedades da partição](../../core/get-started/media/partition-properties.png)
  3. Crie uma partição NTFS que o mecanismo de sequência de tarefas usa para salvar seu estado e para armazenar arquivos de log.
7. Adicione a etapa de sequência de tarefas **Reiniciar Computador**. Em **Especifique o que executar após reiniciar**, selecione **The boot image assigned to this task sequence is selected (A imagem de inicialização atribuída a essa sequência de tarefas está selecionada)** para iniciar o computador no Windows PE.  

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Converter de BIOS para UEFI durante uma atualização in-loco
A Atualização do Windows 10 para Criadores apresenta uma ferramenta de conversão simples que automatiza o processo para reparticionar o disco rígido para hardware habilitado para UEFI e integra a ferramenta de conversão ao processo de atualização in-loco do Windows 7 para o Windows 10. Quando você combina essa ferramenta com a sequência de tarefas de atualização do sistema operacional e a ferramenta de OEM que converte o firmware do BIOS para UEFI, pode converter os computadores de BIOS para UEFI durante uma atualização in-loco para a Atualização do Windows 10 para Criadores.

**Requisitos**:
- Atualização do Windows 10 para Criadores
- Computadores que dão suporte a UEFI
- Ferramenta de OEM que converte o firmware do computador de BIOS para UEFI

### <a name="to-convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Para converter de BIOS para UEFI durante uma atualização in-loco
1. Crie uma sequência de tarefas de atualização do sistema operacional que executa uma atualização in-loco para a Atualização do Windows 10 para Criadores.
2. Edite a sequência de tarefas. No **Grupo de pós-processamento**, adicione as seguintes etapas:
   1. Em Geral, adicione uma etapa **Executar linha de comando**. Você adicionará a linha de comando para a ferramenta MBR2GPT que converte um disco de MBR para GPT sem modificar ou excluir dados do disco. Na linha de comando, digite o seguinte: **MBR2GPT /convert /disk:0 /AllowFullOS**. Você pode optar por executar a ferramenta MBR2GPT.EXE no Windows PE em vez de no sistema operacional completo. Você pode fazer isso adicionando uma etapa para reiniciar o computador no WinPE antes da etapa executar a ferramenta MBR2GPT.EXE e removendo a opção /AllowFullOS na linha de comando. Para obter detalhes sobre a ferramenta e as opções disponíveis, veja [MBR2GPT. EXE](https://technet.microsoft.com/itpro/windows/deploy/mbr-to-gpt).
   2. Adicione uma etapa para iniciar a ferramenta de OEM que converterá o firmware de BIOS para UEFI. Isso geralmente será uma etapa de sequência de tarefas Executar Linha de Comando com uma linha de comando para iniciar a ferramenta de OEM.
   3. Em Geral, adicione a etapa **Reiniciar o computador**. Para especificar o que deve ser executado após a reinicialização, selecione **O sistema operacional padrão atualmente instalado**.
3. Implantar a sequência de tarefas.
