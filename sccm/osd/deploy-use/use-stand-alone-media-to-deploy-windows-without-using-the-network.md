---
title: Usar a mídia autônoma para implantar o Windows sem uso da rede
titleSuffix: Configuration Manager
description: Use a mídia autônoma no Configuration Manager para implantar sistemas operacionais em que a largura de banda é limitada ou como uma opção para atualizar, instalar ou atualizar computadores.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18e50806868955eac807645a5378aea53acdc899
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="use-stand-alone-media-to-deploy-windows-without-using-the-network-in-system-center-configuration-manager"></a>Usar a mídia autônoma para implantar o Windows sem uso da rede no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A mídia autônoma no System Center Configuration Manager contém tudo o que é necessário para implantar um sistema operacional em um computador. Isso inclui a imagem de inicialização, a imagem do sistema operacional e a sequência de tarefas para instalar o sistema operacional, incluindo aplicativos, drivers e assim por diante. as implantações de mídia autônoma permitem implantar sistemas operacionais nas seguintes condições:  

-   Em ambientes onde não é prático copiar uma imagem do sistema operacional ou outros pacotes grandes através da rede.  

-   Em ambientes sem conectividade de rede ou conectividade de rede de baixa largura de banda.  

É possível usar uma mídia autônoma nos seguintes cenários de implantação de sistema operacional:  

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar uma nova versão do Windows em um novo computador (sem sistema operacional)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md)  

 Conclua as etapas em um dos cenários de implantação de sistema operacional e use as seções a seguir para preparar e criar a mídia autônoma.  

## <a name="task-sequence-actions-not-supported-when-using-stand-alone-media"></a>Ações da sequência de tarefas sem suporte com o uso de mídia autônoma  
 Se você concluiu as etapas em um dos cenários de implantação de sistema operacional com suporte, a sequência de tarefas para implantar, ou atualizar, o sistema operacional foi criada e todo o conteúdo associado foi distribuído para um ponto de distribuição. Ao usar uma mídia autônoma, não há suporte para as seguintes ações na sequência de tarefas:  

-   A etapa Aplicação automática de drivers na sequência de tarefas. Não há suporte para aplicação automática de drivers de dispositivo do catálogo de driver, mas você pode escolher a etapa Aplicar pacote de driver para tornar um conjunto especificado de drivers disponíveis para instalação do Windows.  

-   Instalação de atualizações de software.  

-   Instalação do software antes de implantar o sistema operacional.  

-   Associação dos usuários ao computador de destino para dar suporte à afinidade de dispositivo do usuário.  

-   O pacote dinâmico é instalado por meio da tarefa Instalar pacotes.  

-   O aplicativo dinâmico é instalado por meio da tarefa Instalar aplicativo.  

> [!NOTE]  
>  Se a sequência de tarefas para implantar um sistema operacional incluir a etapa [Instalar Pacote](../understand/task-sequence-steps.md#BKMK_InstallPackage) e você criar a mídia autônoma em um site de administração central, poderá ocorrer um erro. O site de administração central não possui as políticas de configuração de cliente necessárias para habilitar o agente de distribuição de software durante a execução da sequência de tarefas. O erro a seguir pode aparecer no arquivo CreateTsMedia.log:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>   
>  Para mídia autônoma que inclui uma etapa **Instalar Pacote**, é necessário criar a mídia autônoma em um site primário que contém o agente de distribuição de software habilitado ou adicionar uma etapa [Executar Linha de Comando](../understand/task-sequence-steps.md#BKMK_RunCommandLine) após a etapa [Configurar Windows e ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) e antes da primeira etapa **Instalar Pacote** na sequência de tarefas. A etapa **Executar linha de comando** executa como um comando WMIC para habilitar o agente de distribuição de software antes da primeira etapa de Instalar pacote ser executada. Você pode usar o seguinte em sua etapa de sequência de tarefas de **Executar linha de comando** :  
>   
>  **Linha de comando**: **WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  

## <a name="configure-deployment-settings"></a>Definir configurações de implantação  
 Ao usar uma mídia autônoma para iniciar o processo de implantação de sistema operacional, é necessário configurar a implantação para disponibilizar o sistema operacional para a mídia. Você pode configurá-la na página **Configurações de implantação** do Assistente de implantação de Software ou na guia **Configurações de implantação** nas propriedades de implantação.  Para a configuração **Tornar disponível para o seguinte** , defina uma das seguintes opções:  

-   **Clientes do Configuration Manager, mídia e PXE**  

-   **Somente mídia e PXE**  

-   **Somente mídia e PXE (oculto)**  

## <a name="create-the-stand-alone-media"></a>Criar a mídia autônoma  
 É possível especificar se a mídia autônoma é uma unidade flash USB ou um conjunto de CDs/DVDs. O computador que inicia a mídia deve dar suporte para a opção que você escolher como uma unidade inicializável. Para obter mais informações, consulte [Criar mídia autônoma](create-stand-alone-media.md).  

## <a name="install-the-operating-system-from-stand-alone-media"></a>Instalar o sistema operacional por meio de uma mídia autônoma  
 Insira a mídia autônoma em uma unidade inicializável no computador e ligue-a para instalar o sistema operacional.  
