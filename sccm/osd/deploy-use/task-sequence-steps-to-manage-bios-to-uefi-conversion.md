---
title: "Etapas de sequência de tarefas para gerenciar o BIOS para a conversão de UEFI | Configuration Manager"
description: "Saiba como personalizar uma sequência de tarefas de implantação do sistema operacional para preparar uma partição FAT32 para a transição para UEFI."
ms.custom: na
ms.date: 11/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 54089ac8aa95154534d010bee8c7e2cbd70d1c7e
ms.openlocfilehash: 30838ed3ad045f781a748f96c874bf543ea05462


---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Etapas de sequência de tarefas para gerenciar o BIOS para a conversão de UEFI
Agora, começando do Configuration Manager versão 1610, é possível personalizar uma sequência de tarefas de implantação do sistema operacional com uma nova variável, TSUEFIDrive, para que a etapa **Reiniciar o Computador** prepare uma partição FAT32 no disco rígido para a transição para UEFI. O procedimento a seguir fornece um exemplo de como você pode criar etapas de sequência de tarefas para preparar o disco rígido para a conversão de BIOS para UEFI.

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Para preparar a partição FAT32 para a conversão para UEFI:
Em uma sequência de tarefas existente para instalar um sistema operacional, você adicionará um novo grupo com etapa para realizar a conversão de BIOS para UEFI.

1. Crie um novo grupo de sequências de tarefas após as etapas para capturar arquivos e configurações e antes das etapas para instalar o sistema operacional. Por exemplo, crie um grupo após o grupo de **Capturar Arquivos e Configurações** denominado **BIOS-to-UEFI (BIOS para UEFI)**.
2. Na guia **Opções** do novo grupo, adicione uma nova variável de sequência de tarefas como uma condição em que **_SMSTSBootUEFI** é **diferente** de **true**. Isso impede que as etapas no grupo sejam executadas quando um computador já estiver no modo UEFI.
![Grupo BIOS to UEFI (BIOS para UEFI)](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. No novo grupo, adicione a etapa de sequência de tarefas **Reiniciar Computador**. Em **Especifique o que executar após reiniciar**, selecione **The boot image assigned to this task sequence is selected (A imagem de inicialização atribuída a essa sequência de tarefas está selecionada)** para iniciar o computador no Windows PE.  
4. Na guia **Opções**, adicione uma variável de sequência de tarefa como uma condição em que **_SMSTSInWinPE equals false (_SMSTSInWinPE é igual a falso)**. Isso impede que esta etapa seja executada se o computador já estiver no Windows PE.

    ![Etapa Reiniciar Computador](../../core/get-started/media/restart-in-windows-pe.png)
5. Adicione uma etapa para iniciar a ferramenta de OEM que converterá o firmware de BIOS para UEFI. Isso geralmente será uma etapa de sequência de tarefas **Executar Linha de Comando** com uma linha de comando para iniciar a ferramenta de OEM.
6.  Adicione a etapa de sequência de tarefas Formatar e Particionar Disco que particionará e formatará o disco rígido. Na etapa, faça o seguinte:
    1.  Crie a partição FAT32 que será convertida em UEFI antes de o sistema operacional ser instalado. Escolha **GGT** para **Tipo de disco**.
    ![Etapa Formatar e particionar disco](../../core/get-started/media/format-and-partition-disk.png)
    2.  Vá para as propriedades da partição FAT32. Digite **TSUEFIDrive** no campo **Variável**. Quando a sequência de tarefas detectar essa variável, ela preparará para a transição de UEFI antes de reiniciar o computador.
    ![Propriedades da partição](../../core/get-started/media/partition-properties.png)
    3. Crie uma partição NTFS que o mecanismo de sequência de tarefas usa para salvar seu estado e para armazenar arquivos de log.
6.  Adicione a etapa de sequência de tarefas **Reiniciar Computador**. Em **Especifique o que executar após reiniciar**, selecione **The boot image assigned to this task sequence is selected (A imagem de inicialização atribuída a essa sequência de tarefas está selecionada)** para iniciar o computador no Windows PE.  



<!--HONumber=Dec16_HO3-->


