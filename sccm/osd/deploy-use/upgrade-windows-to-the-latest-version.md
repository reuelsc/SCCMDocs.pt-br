---
title: "Atualizar o Windows para a versão mais recente | Configuration Manager"
description: "Saiba como usar mídia autônoma ou o Centro de Software no Configuration Manager para atualizar um sistema operacional do Windows 7 ou posterior para Windows 10."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
caps.latest.revision: 13
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b44258255345c2e5488846736ddc1df48a147616


---
# <a name="upgrade-windows-to-the-latest-version-with-system-center-configuration-manager"></a>Atualizar o Windows para a versão mais recente com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico fornece as etapas no System Center Configuration Manager para atualizar um sistema operacional em um computador do Windows 7 ou posterior para o Windows 10. É possível escolher entre diferentes métodos de implantação, como mídia autônoma ou o Centro de Software. O cenário de atualização in-loco do Windows 10:  

-   Atualiza o sistema operacional em computadores que, atualmente, executam o Windows 7, Windows 8 ou Windows 8.1. Também é possível fazer atualizações de build a build do Windows 10. Por exemplo, é possível atualizar o Windows 10 RTM para o Windows 10, versão 1511.  

-   Mantém os aplicativos, as configurações e os dados do usuário no computador.  

-   Não tem dependências externas, como o Windows ADK.  

-   É normalmente mais rápido e mais resiliente do que as implantações tradicionais de sistema operacional.  

 Use as etapas a seguir para implantar sistemas operacionais na rede usando uma sequência de tarefas.  

##  <a name="a-namebkmkplana-plan"></a><a name="BKMK_Plan"></a> Planejar  

-   **Examine as limitações da sequência de tarefas para atualizar um sistema operacional**  

     Examine os seguintes requisitos e limitações para a sequência de tarefas atualizar um sistema operacional, a fim de verificar se ela atende às suas necessidades:  

    -   Você deve adicionar apenas as etapas da sequência de tarefas relacionadas à tarefa principal de implantação de sistemas operacionais e de configuração de computadores após a instalação da imagem. Isso inclui as etapas que instalam pacotes, aplicativos ou atualizações e as etapas que executam linhas de comando, o PowerShell ou que definem variáveis dinâmicas.  

    -   Examine os drivers e os aplicativos que estão instalados nos computadores para garantir que eles são compatíveis com o Windows 10 antes de implantar a sequência de tarefas de atualização.  

    -   As seguintes tarefas não são compatíveis com a atualização in-loco e exigem o uso de implantações tradicionais de sistema operacional:  

        -   Alterar a associação de domínio de computadores ou atualizar os Administradores Locais.  

        -   Implementar uma alteração fundamental no computador, incluindo o particionamento de disco, uma alteração de uma arquitetura do x86 para x64, a implementação da UEFI ou a modificação do idioma do sistema operacional base.  

        -   Tenha requisitos personalizados, incluindo o uso de uma imagem de base personalizada, com criptografia de disco de <sup>terceiros</sup> ou exija operações offline do WinPE.  

-   **Planejar e implementar requisitos de infraestrutura**  

     Os únicos pré-requisitos para o cenário de atualização é que você tenha um ponto de distribuição disponível para o pacote de atualização de sistema operacional e quaisquer outros pacotes incluídos na sequência de tarefas. Para mais informações, consulte [Instalar ou modificar um ponto de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).

##  <a name="a-namebkmkconfigurea-configure"></a><a name="BKMK_Configure"></a> Configurar  

1.  **Preparar o pacote de atualização de sistema operacional**  

     O pacote de atualização do Windows 10 contém os arquivos de origem necessários para atualizar o sistema operacional no computador de destino. Este pacote de atualização deve ter a mesma edição, arquitetura e linguagem que às dos clientes que receberão a atualização.  Para obter mais informações, consulte [Gerenciar pacotes de atualização do sistema operacional](../get-started/manage-operating-system-upgrade-packages.md).  

2.  **Criar uma sequência de tarefas para atualizar o sistema operacional**  

     Normalmente, você usará as etapas em [Criar uma sequência de tarefas para atualizar um sistema operacional](create-a-task-sequence-to-upgrade-an-operating-system.md) para automatizar a atualização do sistema operacional.  

    > [!NOTE]  
    >  Normalmente, você usará as etapas em [Criar uma sequência de tarefas para atualizar um sistema operacional](create-a-task-sequence-to-upgrade-an-operating-system.md) para criar uma sequência de tarefas para atualizar um sistema operacional para o Windows 10. A sequência de tarefas inclui a etapa Atualizar Sistema Operacional, bem como etapas recomendadas adicionais e os grupos para lidar com o processo de atualização ponta a ponta. No entanto, é possível criar uma sequência de tarefas personalizada e adicionar a etapa [Atualizar Sistema Operacional](../understand/task-sequence-steps.md#BKMK_UpgradeOS) da sequência de tarefas para atualizar o sistema operacional. Essa é a única etapa necessária para atualizar o sistema operacional para o Windows 10. Se você escolher esse método, adicione também a etapa [Reiniciar Computador](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer) após a etapa Atualizar Sistema Operacional para concluir a atualização. Certifique-se de usar a configuração **Sistema operacional padrão instalado atualmente** para reiniciar o computador no sistema operacional instalado e não no Windows PE.  

##  <a name="a-namebkmkdeploya-deploy"></a><a name="BKMK_Deploy"></a> Implantar  

-   Use um dos seguintes métodos de implantação para implantar o sistema operacional:  

    -   [Usar o Centro de Software para implantar o Windows pela rede](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [Usar a mídia autônoma para implantar o Windows sem uso da rede](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

## <a name="monitor"></a>Monitor  

-   **Monitorar a implantação da sequência de tarefas**  

     Para monitorar a implantação da sequência de tarefas para atualizar o sistema operacional, consulte [Monitorar implantações do sistema operacional](monitor-operating-system-deployments.md).  



<!--HONumber=Nov16_HO1-->


