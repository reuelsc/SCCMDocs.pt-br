---
title: Atualizar para o Windows 10
titleSuffix: Configuration Manager
description: Saiba como usar o Configuration Manager para atualizar um sistema operacional do Windows 7 ou posterior para o Windows 10.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fbba0306cececebeb7a0e20757e7de3b0d4d0e70
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32348327"
---
# <a name="upgrade-windows-to-the-latest-version-with-system-center-configuration-manager"></a>Atualizar o Windows para a versão mais recente com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo fornece as etapas no Configuration Manager para atualizar o sistema operacional em um computador. É possível escolher entre diferentes métodos de implantação, como mídia autônoma ou o Centro de Software. O cenário de atualização in-loco tem os seguintes recursos:  

-   Atualiza o sistema operacional em computadores que atualmente executam:
    - Windows 7, Windows 8 ou Windows 8.1. Também é possível fazer atualizações de build a build do Windows 10. Por exemplo, atualize o Windows 10 versão 1607 para o Windows 10, versão 1709.  
    
    - Windows Server 2012. Também é possível fazer atualizações de build a build do Windows Server 2016. Para obter mais informações sobre os caminhos de atualização compatíveis, consulte [Caminhos de atualização compatíveis](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016).    

-   Mantém os aplicativos, as configurações e os dados do usuário no computador.  

-   Não tem dependências externas, como o Windows ADK.  

-   É mais rápido e mais resiliente do que as implantações tradicionais de sistema operacional.  


> [!Note]  
> A partir da versão 1802, a sequência de tarefas de atualização in-loco do Windows 10 dá suporte à implantação de clientes baseados na Internet, gerenciados por meio do [gateway de gerenciamento de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway). Essa capacidade proporciona aos usuários remotos uma atualização mais fácil para o Windows 10 sem a necessidade de se conectar à intranet. Para obter mais informações, consulte [Implantar a atualização in-loco do Windows 10 por meio do CMG](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg). <!-- 1357149 -->



##  <a name="BKMK_Plan"></a> Planoo  

### <a name="task-sequence-requirements-and-limitations"></a>Requisitos e limitações da sequência de tarefas

Examine os seguintes requisitos e limitações para a sequência de tarefas atualizar um sistema operacional, a fim de verificar se ela atende às suas necessidades:  

  -   Adicione apenas as etapas da sequência de tarefas relacionadas à tarefa principal de atualização do sistema operacional. Essas etapas incluem principalmente a instalação de pacotes, aplicativos ou atualizações. Use também as etapas que executam linhas de comando, o PowerShell ou que definem variáveis dinâmicas.  

  -   Examine os drivers e os aplicativos que estão instalados nos computadores para garantir que eles são compatíveis com o Windows 10 antes de implantar a sequência de tarefas de atualização.  

  -   As tarefas a seguir não são compatíveis com a atualização in-loco. Elas exigem o uso de implantações tradicionais de sistema operacional:  

     -   Alteração da associação a um domínio do computador ou atualização do grupo local de Administradores.  

     -   Implementação de uma alteração fundamental no computador, como: 
         - Alteração das partições de disco
         - Alteração da arquitetura do sistema de x86 para x64
         - Implementação da UEFI. (Para obter mais informações sobre uma possível opção, consulte [Converter de BIOS em UEFI durante uma atualização in-loco](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).)
         - Modificação do idioma do sistema operacional base  

     -   Você tem requisitos personalizados, incluindo o uso de uma imagem base personalizada, o uso da criptografia de disco de terceiros ou a solicitação de operações offline do WinPE.  

### <a name="infrastructure-requirements"></a>Requisitos de infraestrutura  

O único pré-requisito para o cenário de atualização é ter um ponto de distribuição disponível. Distribua o pacote de atualização do sistema operacional e outros pacotes incluídos na sequência de tarefas. Para mais informações, consulte [Instalar ou modificar um ponto de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).



##  <a name="BKMK_Configure"></a> Configurar  

### <a name="prepare-the-os-upgrade-package"></a>Preparar o pacote de atualização do sistema operacional  

  O pacote de atualização do Windows 10 contém os arquivos de origem necessários para atualizar o sistema operacional no computador de destino. Este pacote de atualização deve ter a mesma edição, arquitetura e linguagem que as dos clientes que receberão a atualização. Para obter mais informações, consulte [Gerenciar pacotes de atualização do sistema operacional](../get-started/manage-operating-system-upgrade-packages.md).  


### <a name="create-a-task-sequence-to-upgrade-the-os"></a>Criar uma sequência de tarefas para atualizar o sistema operacional  

  Use as etapas em [Criar uma sequência de tarefas para atualizar um sistema operacional](create-a-task-sequence-to-upgrade-an-operating-system.md) para automatizar a atualização do sistema operacional.  

   > [!NOTE]  
   > Normalmente, você usa as etapas em [Criar uma sequência de tarefas para atualizar um sistema operacional](create-a-task-sequence-to-upgrade-an-operating-system.md) para criar uma sequência de tarefas para atualizar um sistema operacional para o Windows 10. A sequência de tarefas inclui a etapa Atualizar Sistema Operacional, bem como etapas recomendadas adicionais e os grupos para lidar com o processo de atualização ponta a ponta. No entanto, você pode criar uma sequência de tarefas personalizada e adicionar a etapa [Atualizar Sistema Operacional](../understand/task-sequence-steps.md#BKMK_UpgradeOS) de sequência de tarefas para atualizar o sistema operacional. Esta etapa é a única necessária para atualizar o sistema operacional para o Windows 10. Se você escolher esse método, adicione também a etapa [Reiniciar Computador](../understand/task-sequence-steps.md#BKMK_RestartComputer) após a etapa Atualizar Sistema Operacional para concluir a atualização. Lembre-se de usar a configuração **O sistema operacional padrão instalado atualmente** para reiniciar o computador no sistema operacional instalado e não no Windows PE.  



##  <a name="BKMK_Deploy"></a> Implantar  

Para implantar o sistema operacional, use um dos seguintes métodos de implantação:  

  -   [Usar o Centro de Software para implantar o Windows pela rede](use-software-center-to-deploy-windows-over-the-network.md)  

  -   [Usar a mídia autônoma para implantar o Windows sem uso da rede](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

      > [!IMPORTANT]  
      > Ao usar mídia autônoma, você deve incluir uma imagem de inicialização na sequência de tarefas para que ela fique disponível no Assistente para Mídia de Sequência de Tarefas.




## <a name="monitor"></a>Monitor  

Para monitorar a implantação da sequência de tarefas para atualizar o sistema operacional, consulte [Monitorar implantações de sistema operacional](monitor-operating-system-deployments.md).  
