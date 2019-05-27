---
title: Criar mídia autônoma
titleSuffix: Configuration Manager
description: Use uma mídia autônoma para implantar o SO em um computador sem uma conexão de rede.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a00da1511c6410088f318fc619bbddc537e20708
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65083232"
---
# <a name="create-stand-alone-media"></a>Criar mídia autônoma

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A mídia autônoma no Configuration Manager contém tudo o que é necessário para implantar o SO em um computador sem uma conexão de rede.

Use a mídia autônoma nos seguintes cenários de implantação de sistema operacional:  

- [Atualizar um computador existente com uma nova versão do Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows)  

- [Instalar uma nova versão do Windows em um novo computador (sem sistema operacional)](/sccm/osd/deploy-use/install-new-windows-version-new-computer-bare-metal)  

- [Atualizar o Windows para a versão mais recente](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version)  


## <a name="usage"></a>Uso

A mídia autônoma inclui a sequência de tarefas que automatiza as etapas para instalar o sistema operacional e todos os demais conteúdos necessários. Esse conteúdo inclui a imagem de inicialização, a imagem do SO e os drivers de dispositivos. Como a mídia autônoma armazena tudo para implantar o sistema operacional, é necessário mais espaço em disco do que para outros tipos de mídia.

Quando você cria mídia autônoma em um site de administração central, o cliente recupera seu código do site atribuído do Active Directory. A mídia autônoma criada em sites filho atribui automaticamente o código desse site ao cliente.  


## <a name="prerequisites"></a>Pré-requisitos

Antes de criar uma mídia independente usando o Assistente para Criar Mídia de Sequência de Tarefas, verifique se todas essas condições foram atendidas.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Criar uma sequência de tarefas para implantar um SO

Como parte da mídia autônoma, especifique a sequência de tarefas para implantar um SO. Para saber mais, confira [Criar uma sequência de tarefas para instalar um SO](/sccm/osd/deploy-use/create-a-task-sequence-to-install-an-operating-system).

#### <a name="unsupported-actions-for-stand-alone-media"></a>Ações sem suporte para mídias autônomas

As seguintes ações não têm suporte para mídias autônomas:

- A etapa [Aplicação Automática de Drivers](/sccm/osd/understand/task-sequence-steps#BKMK_AutoApplyDrivers) na sequência de tarefas. A mídia autônoma não dá suporte à aplicação automática de drivers de dispositivo do catálogo de drivers. Use a etapa [Aplicar Pacote de Driver](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyDriverPackage) para tornar um conjunto especificado de drivers disponível para Instalação do Windows.  

- A etapa [Baixar Conteúdo do Pacote](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent) na sequência de tarefas. As informações do ponto de gerenciamento não estão disponíveis na mídia autônoma e, portanto, a etapa falha ao tentar enumerar as localizações de conteúdo.  

- Instalação de atualizações de software.  

- A instalação do software antes de implantar o SO.  

- As sequências de tarefas personalizadas para implementações não relacionadas ao SO.  

- Associação dos usuários ao computador de destino para dar suporte à afinidade de dispositivo do usuário.  

- O pacote dinâmico é instalado na etapa [Instalar Pacotes](/sccm/osd/understand/task-sequence-steps#BKMK_InstallPackage).  

- O aplicativo dinâmico é instalado na etapa [Instalar Aplicativo](/sccm/osd/understand/task-sequence-steps#BKMK_InstallApplication).

- A configuração **Usar pacote de cliente de pré-produção quando disponível** na etapa da sequência de tarefas **Instalar Windows e ConfigMgr**. Para obter mais informações sobre essa configuração, consulte [Instalar o Windows e o ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr).  

> [!NOTE]  
> Poderá ocorrer um erro se a sequência de tarefas incluir a etapa [Instalar Pacote](/sccm/osd/understand/task-sequence-steps#BKMK_InstallPackage) e você criar a mídia autônoma em um site de administração central. O site de administração central não tem as políticas de configuração de cliente necessárias. Essas políticas são necessárias para habilitar o agente de distribuição de software quando a sequência de tarefas é executada. O seguinte erro pode aparecer no arquivo **CreateTsMedia.log**:  
>
> `WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)`
>
> Para mídia autônoma que inclui uma etapa **Instalar Pacote**, crie a mídia autônoma em um site primário que tem o agente de distribuição de software habilitado.
>
> Como alternativa, use uma etapa [Executar Linha de Comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) personalizada. Adicione-a após a etapa [Instalar o Windows e o ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr) e antes da primeira etapa **Instalar Pacote**. A etapa **Executar Linha de Comando** executa o seguinte comando WMIC para habilitar o agente de distribuição de software antes da primeira etapa Instalar Pacote:  
>
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuir todo o conteúdo associado à sequência de tarefas

Distribua todo o conteúdo exigido pela sequência de tarefas para pelo menos um ponto de distribuição. Esse conteúdo inclui a imagem de inicialização, a imagem do SO e outros arquivos associados. O assistente reúne o conteúdo do ponto de distribuição ao criar a mídia.

Sua conta de usuário precisa pelo menos de direitos de acesso de **Leitura** à biblioteca de conteúdo nesse ponto de distribuição. Para obter mais informações, consulte [Distribuir conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Preparar a unidade USB removível

Se estiver usando uma unidade USB removível, conecte-a ao computador em que você executa o Assistente para Criar Mídia de Sequência de Tarefas. A unidade USB deve ser detectável pelo Windows como um dispositivo de remoção. O assistente grava diretamente na unidade USB ao criar a mídia.

A mídia autônoma usa um sistema de arquivos FAT32. Você não pode criar uma mídia autônoma em uma unidade USB removível cujo conteúdo inclua um arquivo com mais de 4 GB.

### <a name="create-an-output-folder"></a>Criar uma pasta de saída

Antes de executar o Assistente para Criar Mídia de Sequência de Tarefas para criar a mídia para um conjunto de CD ou DVD, crie uma pasta para os arquivos de saída que são gerados. A mídia criada para um conjunto de CD ou DVD é gravada como um arquivo .ISO diretamente na pasta.


## <a name="process"></a>Processar

1. No console do Configuration Manager, acesse o espaço de trabalho **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione o nó **Sequências de Tarefas**.  

2. Na guia **Início** da faixa de opções, no grupo **Criar**, selecione **Criar Mídia de Sequência de Tarefas**. Essa ação inicia o Assistente para Criar Mídia de Sequência de Tarefas.  

3. Na página **Selecionar o Tipo de Mídia**, especifique as seguintes opções:  

    - Selecione **Mídia autônoma**.  

    - Opcionalmente, se quiser permitir que o SO seja implantado sem exigir a entrada do usuário, selecione **Permitir implantação autônoma do sistema operacional**.  

        > [!IMPORTANT]  
        > Quando você seleciona essa opção, o usuário não recebe uma solicitação para fornecer informações de configuração da rede ou sequências de tarefas opcionais. Se você configurar a mídia para proteção por senha, o usuário ainda será solicitado a fornecer uma senha.  

4. Na página **Tipo de Mídia**, especifique se a mídia é uma **Unidade USB removível** ou um **Conjunto de CD/DVD**. Em seguida, configure as seguintes opções:  

    > [!IMPORTANT]  
    > A mídia usa um sistema de arquivos FAT32. Você não pode criar uma mídia em uma unidade USB cujo conteúdo inclua um arquivo com mais de 4 GB.  

    - Se você selecionar **Unidade USB removível**, selecione a unidade na qual deseja armazenar o conteúdo.  

        - **Formatar a unidade USB removível (FAT32) e torná-la inicializável**: por padrão, permita que o Configuration Manager prepare a unidade USB. Muitos dispositivos UEFI mais recentes requerem uma partição FAT32 inicializável. No entanto, esse formato também limita o tamanho dos arquivos e a capacidade geral da unidade. Se você já formatou e configurou a unidade de disco removível, desabilite essa opção.

    - Se você selecionar **Conjunto de CD/DVD**, especifique a capacidade da mídia (**Tamanho da mídia**) e o nome e o caminho do arquivo de saída (**Arquivo de mídia**). O assistente grava os arquivos de saída nesse local. Por exemplo: `\\servername\folder\outputfile.iso`  

        Se a capacidade da mídia for muito pequena para armazenar todo o conteúdo, ela criará vários arquivos. Portanto, você precisará armazenar o conteúdo em vários CDs ou DVDs. Quando vários arquivos de mídia são necessários, o Configuration Manager adiciona um número de sequência ao nome de cada arquivo de saída criado.  

        Se você implantar um aplicativo junto com o SO, e o aplicativo não couber em uma única mídia, o Configuration Manager armazenará o aplicativo em várias mídias. Quando a mídia autônoma é executada, o Configuration Manager solicita ao usuário a próxima mídia, na qual o aplicativo está armazenado.  

        > [!IMPORTANT]  
        > Se você selecionar uma imagem .iso existente, o Assistente de Mídia de Sequência de Tarefas excluirá essa imagem da unidade ou do compartilhamento assim que você prosseguir para a próxima página do assistente. A imagem existente será excluída mesmo se você cancelar o assistente.  

    - **Pasta de preparo**<!--1359388-->: o processo de criação da mídia pode exigir muito espaço em disco temporário. Por padrão, essa localização é semelhante ao seguinte caminho: `%UserProfile%\AppData\Local\Temp`. A partir da versão 1902, para fornecer maior flexibilidade quando se trata de armazenar esses arquivos temporários, altere esse valor para outra unidade e caminho.  

    - **Rótulo de mídia**<!--1359388-->: a partir da versão 1902, adicione um rótulo à mídia de sequência de tarefas. Esse rótulo ajuda a identificar melhor a mídia depois de criá-la. O valor padrão é `Configuration Manager`. Esse campo de texto é exibido nos seguintes locais:  

        - Se você montar um arquivo ISO, o Windows exibirá esse rótulo como o nome da unidade montada  

        - Se você formatar uma unidade USB, ela usará os primeiro 11 caracteres do rótulo como seu nome  

        - O Configuration Manager grava um arquivo de texto chamado `MediaLabel.txt` na raiz da mídia. Por padrão, o arquivo inclui uma única linha de texto: `label=Configuration Manager`. Se você personalizar o rótulo de mídia, essa linha usará o rótulo personalizado, em vez do valor padrão.  

    - **Incluir arquivo autorun.inf na mídia**<!-- 4090666 -->: a partir da versão 1902, o Configuration Manager não adiciona um arquivo autorun.inf por padrão. Normalmente, esse arquivo é bloqueado por produtos antimalware. Para obter mais informações sobre o recurso AutoRun do Windows, confira [Creating an AutoRun-enabled CD-ROM Application](https://docs.microsoft.com/windows/desktop/shell/autoplay) (Criando um aplicativo de CD-ROM habilitado para AutoRun). Se ainda for necessário para o seu cenário, selecione essa opção para incluir o arquivo.  

5. Na página **Segurança**, especifique as seguintes opções:

    - **Proteger mídia com senha**: insira uma senha forte para ajudar a proteger a mídia contra acesso não autorizado. Quando você especificar uma senha, o usuário deverá fornecer essa senha para usar a mídia.  

        > [!IMPORTANT]  
        > Como prática recomendada de segurança, atribua sempre uma senha para ajudar a proteger a mídia.  
        >
        > Na mídia autônoma, ele criptografa apenas as etapas da sequência de tarefas e suas variáveis. Ele não criptografa o conteúdo restante da mídia. Não inclua informações confidenciais em scripts de sequência de tarefas. Armazene e implemente todas as informações confidenciais usando as variáveis da sequência de tarefas.  

    - **Selecione o intervalo de datas para o qual essa mídia autônoma deve ser válida**: defina datas de início e vencimento opcionais na mídia. Essa configuração fica desabilitada por padrão. As datas são comparadas com a hora do sistema no computador antes de a mídia autônoma ser executada. Quando a hora do sistema é anterior à hora de início ou posterior à hora de expiração, a mídia autônoma não é iniciada. Essas opções também estão disponíveis usando o cmdlet do PowerShell [New-CMStandaloneMedia](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmstandalonemedia?view=sccm-ps).  

6. Na página **CD/DVD Autônomo**, selecione a sequência de tarefas que implanta o SO. Você pode selecionar apenas as sequências de tarefas associadas a uma imagem de inicialização. Verifique a lista de conteúdo consultada pela sequência de tarefas.  

    - **Detectar dependências de aplicativos associados e adicioná-las a esta mídia**: também adicione conteúdo à mídia para dependências de aplicativos.  

        > [!TIP]  
        > Se você não vir as dependências de aplicativo esperadas, desmarque e depois selecione novamente essa opção para atualizar a lista.  

7. Na página **Selecionar Aplicativo**, especifique o conteúdo adicional do aplicativo para incluir como parte do arquivo de mídia.  

8. Na página **Selecionar Pacote**, especifique o conteúdo do pacote adicional para incluir como parte do arquivo de mídia.  

9. Na página **Selecionar Pacote de Driver**, especifique o conteúdo do pacote de driver adicional para incluir como parte do arquivo de mídia.  

10. Na página **Pontos de Distribuição**, especifique os pontos de distribuição que incluem o conteúdo necessário.  

    O Configuration Manager exibe apenas pontos de distribuição que tenham conteúdo. Distribua todo o conteúdo associado à sequência de tarefas para pelo menos um ponto de distribuição antes de continuar. Após distribuir o conteúdo, atualize a lista de pontos de distribuição. Remova os pontos de distribuição que já foram selecionados nessa página, vá para a página anterior e volte para a página **Pontos de Distribuição**. Como alternativa, reinicie o assistente. Para obter mais informações, consulte [Distribuir o conteúdo referenciado por uma sequência de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DistributeTS) e [Gerenciar conteúdo e infraestrutura de conteúdo](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

11. Na página **Personalização**, especifique as seguintes opções:  

    - Adicione quaisquer variáveis usadas pela sequência de tarefas.  

    - **Habilitar comando prestart**: especifique qualquer comando prestart que você queira executar antes da execução da sequência de tarefas. Comandos prestart são um script ou executável que pode interagir com o usuário no Windows PE antes da execução da sequência de tarefas. Para mais informações, consulte [Comandos prestart para mídia de sequência de tarefas](/sccm/osd/understand/prestart-commands-for-task-sequence-media).  

        > [!TIP]  
        > Durante a criação da mídia, a sequência de tarefas grava o ID do pacote e a linha do comando prestart, incluindo o valor de qualquer variável de sequência de tarefas, no arquivo **CreateTSMedia.log** no computador que executa o console do Configuration Manager. Você poderá analisar esse arquivo de log para verificar o valor das variáveis de sequência de tarefas.  

        Se o comando prestart exigir algum conteúdo, selecione a opção **Incluir arquivos no comando prestart**.  

12. Conclua o assistente.  

Os arquivos de mídia autônoma (.ISO) são criados na pasta de destino. Se você selecionou **Conjunto de CD/DVD**, copie os arquivos de saída para um conjunto de CDs ou DVDs.


## <a name="next-steps"></a>Próximas etapas

[Usar a mídia autônoma para implantar o Windows sem uso da rede](/sccm/osd/deploy-use/use-stand-alone-media-to-deploy-windows-without-using-the-network)
