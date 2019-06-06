---
title: Instalar Atualizações de Software
titleSuffix: Configuration Manager
description: Recomendações para utilizar a etapa da sequência de tarefas Instalar Atualizações de Software no Configuration Manager.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 72d1ccd5-3763-4f88-9273-e1a73e8f4286
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6699b73bd9a3a911fef788f25cbf2140e90cbe92
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66355042"
---
# <a name="install-software-updates"></a>Instalar Atualizações de Software

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A etapa **Instalar Atualizações de Software** é geralmente usada em sequências de tarefas do Configuration Manager. Ao instalar ou atualizar o sistema operacional, ela dispara os componentes de atualização de software para verificar e implantar as atualizações. Esta etapa pode representar desafios para alguns clientes, por exemplo, longos atrasos no tempo limite ou atualizações perdidas. Leia as informações neste artigo para ajudar a atenuar os problemas comuns desta etapa e para a melhor solucioná-los quando algo der errado.

Para saber mais sobre esta etapa, confira o item sobre como [instalar atualizações de software](/sccm/osd/understand/task-sequence-steps#BKMK_InstallSoftwareUpdates)



## <a name="recommendations"></a>Recomendações

Para que ajudar a obter êxito neste processo, siga as seguintes recomendações:

- [Usar a manutenção offline](#use-offline-servicing)
- [Índice único](#single-index)
- [Reduzir o tamanho da imagem](#bkmk_resetbase)

### <a name="use-offline-servicing"></a>Usar a manutenção offline

Use o Configuration Manager para instalar regularmente as atualizações de software aplicáveis em seus arquivos de imagem. Essa prática reduz o número de atualizações que são necessárias instalar durante a sequência de tarefas.

Para saber mais, confira o item sobre como [aplicar atualizações de software a uma imagem](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates).

### <a name="single-index"></a>Índice único

Muitos arquivos de imagem incluem vários índices, por exemplo, para edições diferentes do Windows. Reduza o arquivo de imagem para um índice único que você requer. Essa prática reduz o tempo de aplicação das atualizações de software à imagem. Ela também habilita a próxima recomendação para reduzir o tamanho da imagem.

Começando na versão 1902, automatize esse processo quando adicionar uma imagem de sistema operacional ao site. Para saber mais, confira o tópico [Adicionar uma imagem do sistema operacional](/sccm/osd/get-started/manage-operating-system-images#BKMK_AddOSImages).<!--3719699-->

### <a name="bkmk_resetbase"></a> Reduzir o tamanho da imagem

Quando você aplica as atualizações de software a uma imagem, otimize a saída removendo as atualizações substituídas. Use a ferramenta de linha de comando do DISM, por exemplo:

```
dism /Mount-Image /ImageFile:C:\Data\install.wim /MountDir:C:\Mountdir
dism /Image:C:\Mountdir /Cleanup-Image /StartComponentCleanup /ResetBase
dism /Unmount-Image /MountDir:C:\Mountdir /Commit  
```

Começando na versão 1902, há uma nova opção para automatizar esse processo. Para obter mais informações, consulte [Serviço de imagens otimizadas](/sccm/osd/get-started/manage-operating-system-images#bkmk_resetbase).<!--3555951-->


## <a name="image-engineering-decisions"></a>Decisões de engenharia de imagem

Ao projetar o processo de geração de imagens, há várias opções que podem afetar a instalação das atualizações de software:

- [Recapturar a imagem periodicamente](#bkmk_goldimage)  
- [Usar a manutenção offline](#bkmk_offline)  
- [Usar somente a imagem padrão](#bkmk_installwim)

### <a name="bkmk_goldimage"></a> Recapturar a imagem periodicamente

Há um processo automatizado para capturar uma imagem personalizada do sistema operacional de acordo com um agendamento regular. Essa sequência de tarefas de captura instala as atualizações de software mais recentes. Essas atualizações podem ser cumulativas, não cumulativas e outras atualizações críticas, como atualizações da pilha de manutenção (SSU). A sequência de tarefas para implantação instala as atualizações adicionais desde a captura.

Para saber mais sobre esse processo, confira [Criar uma sequência de tarefas para capturar um sistema operacional](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system).

#### <a name="advantages"></a>Vantagens

- Menos atualizações a serem aplicadas no momento da implantação em cada cliente, o que economiza tempo e largura de banda durante a implantação
- Menos atualizações que causam reinicializações com que se preocupar
- Imagem personalizada para a organização
- Menos variáveis no momento da implantação

#### <a name="disadvantages"></a>Desvantagens

- Tempo para criar e capturar a imagem, ainda que seja basicamente automatizado
- Mais tempo para distribuir a imagem aos pontos de distribuição, o que pode ser visto como uma interrupção de implantações ativas
- O tempo para realizar testes em ambientes de pré-produção pode ser maior que o ciclo de patches do sistema operacional, o que pode tornar a imagem atualizada irrelevante


### <a name="bkmk_offline"></a> Usar a manutenção offline

Agende o Configuration Manager para aplicar atualizações de software a suas imagens.

Para saber mais, confira o item sobre como [aplicar atualizações de software a uma imagem](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates).

#### <a name="advantages"></a>Vantagens

- Menos atualizações a serem aplicadas no momento da implantação em cada cliente, o que economiza tempo e largura de banda durante a implantação
- Menos atualizações que causam reinicializações com que se preocupar
- Você pode agendar o processo do serviço no site

#### <a name="disadvantages"></a>Desvantagens

- Seleção manual das atualizações
- Mais tempo para distribuir a imagem aos pontos de distribuição
- Apenas dá suporte a atualizações baseadas em CBS. Não pode aplicar atualizações do Office

> [!Tip]  
> É possível automatizar a seleção das atualizações de software usando o PowerShell. Use o cmdlet [Get-CMSoftwareUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmsoftwareupdate?view=sccm-ps) para obter uma lista de atualizações. Em seguida, use o cmdlet [New-CMOperatingSystemImageUpdateSchedule](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmoperatingsystemimageupdateschedule?view=sccm-ps) para criar o agendamento do serviço offline. O exemplo a seguir mostra um método para automatizar essa ação:
>
> ```PowerShell
> # Get the OS image
> $Win10Image = Get-CMOperatingSystemImage -Name "Windows 10 Enterprise"
>
> # Get the latest cumulative update for Windows 10 1809
> $OSBuild = "1809"
> $LatestUpdate = Get-CMSoftwareUpdate -Fast | Where {$_.LocalizedDisplayName -Like "*Cumulative Update for Windows 10 Version $OSBuild for x64*" -and $_.LocalizedDisplayName -notlike "*Dynamic*"} | Sort-Object ArticleID -Descending | Select -First 1
> Write-Host "Latest update for Windows 10 build" $OSBuild "is" $LatestUpdate.LocalizedDisplayName
>
> # Create a new update schedule to apply the latest update
> New-CMOperatingSystemImageUpdateSchedule -Name $Win10Image.Name -SoftwareUpdate $LatestUpdate -RunNow -ContinueOnError $True
> ```


### <a name="bkmk_installwim"></a> Usar somente a imagem padrão

Use o arquivo de imagem padrão do Windows install.wim em suas sequências de tarefas de implantação.

#### <a name="advantages"></a>Vantagens

- É uma fonte conhecida adequada, o que reduz o risco de imagens corrompidas como um possível problema
- Elimina as modificações na imagem como um possível problema

#### <a name="disadvantages"></a>Desvantagens

- Possibilidade de alto volume de atualizações durante a implantação
- Maior tempo de implantação em cada dispositivo
- Pode não ter precisado de personalizações e requer etapas de sequência de tarefas adicionais para a personalização



## <a name="flowchart"></a>Fluxograma

Este diagrama de fluxograma mostra o processo quando você inclui a etapa Instalar Atualizações de Software em uma sequência de tarefas.

[Ver diagrama em tamanho original](media/ts-step-install-software-updates.svg)

![Diagrama de fluxograma da etapa da sequência de tarefas Instalar Atualizações de Software](media/ts-step-install-software-updates.svg)  

1. **O processo é iniciado no cliente:** uma sequência de tarefas em execução em um cliente inclui a etapa Instalar Atualizações de Software.
2. **Compilar e avaliar políticas**: o cliente compila todas as políticas de atualização de software no namespace RequestedConfigs da WMI. (CIAgent.log)
3. *É a primeira vez que essa instância é chamada?*  
    1. **Sim**: vá para a **Verificação completa**  
    2. **Não**: *A etapa está configurada com a opção para [Avaliar atualizações de software nos resultados da verificação em cache](/sccm/osd/understand/task-sequence-steps#evaluate-software-updates-from-cached-scan-results)?*
        1. **Sim**: vá para **Verificar os resultados em cache**
        2. **Não**: vá para a **Verificação completa**
4. Processo de verificação: uma verificação completa ou uma verificação dos resultados em cache, com monitoramento de processo em paralelo.
    1. **Verificação completa**: o mecanismo de sequência de tarefas chama o agente de atualização de software por meio da API de Verificação de Atualização para fazer uma verificação *completa*. (WUAHandler.log, ScanAgent.log)  
        1. **Verificação do agente SUM – completa**: processo de verificação normal por meio do WUA (Windows Update Agent), que se comunica com o ponto de atualização de software que está executando o WSUS. Ele adiciona todas as atualizações aplicáveis ao armazenamento de atualizações local. (WindowsUpdate.log, UpdateStore.log)
    2. **Verificar os resultados em cache**: o mecanismo da sequência de tarefas chama o agente de atualização de software por meio da API de Verificação de Atualização para verificar os metadados em cache. (WUAHandler.log, ScanAgent.log)
        1. **Verificação do agente SUM – em cache**: o WUA (Windows Update Agent) verifica as atualizações já armazenadas em cache no armazenamento de atualizações local. (WindowsUpdate.log, UpdateStore.log)
    3. **Iniciar temporizador de verificação**: o mecanismo de sequência de tarefas inicia um temporizador e aguarda. (Esse processo ocorre em paralelo com a verificação completa ou com a verificação do processo de resultados em cache).
        1. **Monitoramento**: o mecanismo de sequência de tarefas monitora o agente SUM quanto ao status.
        2. *Qual é resposta do agente SUM?*
            - **Em andamento**: o temporizador atingiu o valor na variável de sequência de tarefas [SMSTSSoftwareUpdateScanTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSSoftwareUpdateScanTimeout)? (O padrão é 1 hora)
                - **Sim**: a etapa falhou.
                - **Não**: vá para o **Monitoramento**
            - **Com falha**: a etapa falhou.
            - **Concluído**: vá para **Enumerar lista de atualização**
5. **Enumerar lista de atualização**: o agente SUM enumera a lista de atualizações retornada pela verificação, determinando quais estão disponíveis ou são obrigatórias.
6. *Existem atualizações na lista dos resultados da verificação?*
    - **Sim**: vá para **Instalar atualizações**
    - **Não**: nada a instalar, a etapa foi concluída com êxito.
7. Processo de implantação: o processo instalação de atualizações acontece em paralelo com o processo de monitoramento da implantação.
    1. **Instalar atualizações**: o mecanismo de sequência de tarefas chama o agente SUM por meio da API de Implantação de Atualização para instalar todas as atualizações disponíveis ou apenas as obrigatórias. Esse comportamento baseia-se na configuração da etapa, ao selecionar as **Necessárias para instalação – Somente atualizações de software obrigatórias** ou aquelas **Disponíveis para instalação – todas as atualizações de software**. É ainda possível especificar esse comportamento usando a variável [SMSInstallUpdateTarget](/sccm/osd/understand/task-sequence-variables#SMSInstallUpdateTarget).
        1. **Instalação do agente SUM**: processo de instalação normal usando a lista em cache existente das atualizações com o download de conteúdo padrão. Instale a atualização por meio do Windows Update Agent (WUA). (UpdatesDeployment.log, UpdatesHandler.log, WuaHandler.log, WindowsUpdate.log)
    2. **Iniciar o temporizador de implantação e exibir o progresso**: o mecanismo de sequência de tarefas inicia o temporizador de instalação, exibe o subprogresso em intervalos de 10% na interface do usuário do Andamento do TS e aguarda.
        1. **Monitoramento**: o mecanismo de sequência de tarefas pesquisa o agente SUM quanto ao status.
        2. *Qual é resposta do agente SUM?*
            - **Em andamento**: *O processo de instalação ficou inativo por 8 horas?*
                - **Sim**: a etapa falhou.
                - **Não**: vá para o **Monitoramento**
            - **Com falha**: a etapa falhou.
            - **Concluído**: vá para *A etapa está configurada com a opção para **Avaliar atualizações de software nos resultados da verificação em cache**?*


### <a name="timeouts"></a>Tempos limite

O diagrama inclui duas variáveis de tempo limite que se aplicam a esta etapa. Há outros temporizadores padrão de outros componentes que podem afetar este processo.

- Tempo limite de verificação de atualização: 1 hora (smsts.log)  
- Tempo limite da solicitação de localização: 1 hora (LocationServices.log, CAS.log)  
- Tempo limite do download de conteúdo: 1 hora (DTS.log)  
- Tempo limite de ponto de distribuição inativo: 1 hora (LocationServices.log, CAS.log)  
- Tempo limite total de instalação inativa: 8 horas (smsts.log)  



## <a name="troubleshooting"></a>Solução de problemas

Use os seguintes recursos e informações adicionais para auxiliar na solução de problemas com esta etapa:

- Certifique-se de direcionar as implantações de atualização de software para a mesma coleção, como a implantação de sequência de tarefas.  

- Inclua os pontos de atualização de software em grupos de limites. Para saber mais, confira este [artigo do Suporte da Microsoft](https://support.microsoft.com/help/4041012/1702-clients-do-not-get-software-updates-from-configuration-manager).  

- Para ajudar a solucionar problemas do processo de gerenciamento de atualizações de software, confira [Solução de problemas do Gerenciamento de Atualização de Software](https://support.microsoft.com/help/10680/software-update-management-troubleshooting-in-configuration-manager).  

- Para ajudar a melhorar o desempenho geral, reduza o tamanho do catálogo de atualização de software. Por exemplo:  

    - remova as classificações, os produtos e os idiomas desnecessários. Para obter mais informações, confira [Configurar classificações e produtos para sincronização](/sccm/sum/get-started/configure-classifications-and-products).  

    - Reindexe o banco de dados do site e recompile as estatísticas. Para saber mais, consulte o [Whitepaper das diretrizes de desempenho e escala do Configuration Manager](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e).  

    - Recuse as atualizações desnecessárias, por exemplo:
        - Substituída (a partir da versão 1810, o Configuration Manager faz essa ação para você. Para saber mais, confira as informações sobre o [comportamento de limpeza do WSUS com a partir da versão 1810](/sccm/sum/deploy-use/software-updates-maintenance#wsus-cleanup-behavior-starting-in-version-1810)).
        - Itanium
        - Beta
        - Próxima versão
        - ARM
        - Versões do Windows que você não está implantado
