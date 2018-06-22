---
title: Criar uma sequência de tarefas de atualização do sistema operacional
titleSuffix: Configuration Manager
description: Usar uma sequência de tarefas para a atualização automática do Windows 7 ou posterior para o Windows 10
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d35a5ea3ebde6ce6ab0934832180223c2a634541
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32352525"
---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>Crie uma sequência de tarefas para atualizar um sistema operacional no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use sequências de tarefas no Configuration Manager para fazer upgrade automaticamente de um sistema operacional em um computador de destino. Esse upgrade pode ser do Windows 7 ou posterior para o Windows 10, ou do Windows Server 2012 ou posterior para o Windows Server 2016. Crie uma sequência de tarefas que referencia o pacote de atualização do sistema operacional e outros tipos de conteúdo a serem instalados, como aplicativos ou atualizações de software. A sequência de tarefas para atualizar um sistema operacional faz parte do cenário [Atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md).  



##  <a name="BKMK_UpgradeOS"></a> Criar uma sequência de tarefas para atualizar um sistema operacional  
 Para atualizar o sistema operacional em computadores, você pode criar uma sequência de tarefas e selecionar a opção **Atualizar um sistema operacional do pacote de atualização** no assistente Criar Sequência de Tarefas. O assistente adiciona as etapas de sequência de tarefas para atualizar o sistema operacional, aplicar atualizações de software e instalar aplicativos. Antes de criar a sequência de tarefas, os seguintes requisitos devem estar em vigor:    

-   **Necessária**  

     - O [pacote de atualização do sistema operacional](../get-started/manage-operating-system-upgrade-packages.md) deve estar disponível no console do Configuration Manager.
     - Ao fazer upgrade para o Windows Server 2016, selecione a configuração **Ignorar quaisquer mensagens descartáveis de compatibilidade** na etapa da sequência de tarefas Fazer Upgrade do Sistema Operacional. Caso contrário, a atualização falhará.

-   **Necessário (se usado)**  

    -   As [atualizações de software](../../sum/get-started/synchronize-software-updates.md) devem estar sincronizadas no console do Configuration Manager.  

    -   Os [aplicativos](../../apps/deploy-use/create-applications.md) devem ser adicionados ao console do Configuration Manager.  

#### <a name="to-create-a-task-sequence-that-upgrades-an-operating-system"></a>Para criar uma sequência de tarefas que atualiza um sistema operacional  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Sequência de Tarefas** para iniciar o Assistente para Criar Sequência de Tarefas.  

4.  Na página **Criar uma nova sequência de tarefas** , clique em **Atualizar um sistema operacional do pacote de atualização**e, em seguida, clique em **Avançar**.  

5.  Na página **Informações da Sequência de Tarefas** , especifique as seguintes configurações e clique em **Próximo**.  

    -   **Nome da sequência de tarefas**: especifique um nome que identifique a sequência de tarefas.  

    -   **Descrição**: especifique uma descrição da tarefa executada pela sequência de tarefas.  

6.  Na página **Atualizar o sistema operacional Windows** , especifique as seguintes configurações e, em seguida, clique em **Avançar**.  

    -   **Atualizar pacote**: especifique o pacote de atualização que contenha os arquivos de origem de atualização do sistema operacional. Você pode verificar se você selecionou o pacote de atualização correto examinando as informações no painel **Propriedades** . Para obter mais informações, consulte [Gerenciar pacotes de atualização do sistema operacional](../get-started/manage-operating-system-upgrade-packages.md).  

    -   **Índice de edição**: se houver vários índices de edição do sistema operacional disponíveis no pacote, selecione o índice de edição desejado. Por padrão, o primeiro item é selecionado.  

    -   **Chave do produto (Product Key)**: especifique a chave do produto (Product Key) do sistema operacional Windows que será instalada. Você pode especificar as chaves de licença de volume codificadas e as chaves do produto padrão. Se você usar uma chave de produto sem codificação, cada grupo de cinco caracteres deverá ser separado por um traço (-). Por exemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Quando a atualização é para uma edição de licença de volume, a chave do produto não é necessária. Você só precisa de uma chave do produto quando a atualização é para uma edição de varejo do Windows.  

    -   **Ignorar mensagens descartáveis de compatibilidade**: selecione essa opção se você estiver atualizando para o Windows Server 2016. Se você não selecionar essa configuração, a sequência de tarefas não conseguirá ser concluída porque a Instalação do Windows estará aguardando que o usuário clique em **Confirmar** em uma caixa de diálogo de compatibilidade de aplicativo do Windows.   

7.  Na página **Incluir Atualizações**, especifique se desejar instalar as atualizações de software obrigatórias, todas ou nenhuma. Clique em **Avançar**. Se você optar pela instalação das atualizações de software, o Configuration Manager instalará somente as atualizações de software direcionadas às coleções das quais o computador de destino é membro.  

8.  Na página **Instalar Aplicativos** , especifique os aplicativos a instalar no computador de destino e clique em **Próximo**. Se você especificar vários aplicativos, será possível também definir a continuação da sequência de tarefas em caso de falha na instalação de algum aplicativo.  

9. Conclua o assistente.  


 > [!Important] 
 > Quando a sequência de tarefas é concluída, o cliente não remove os scripts pós-processamento e de reversão até que o computador seja reiniciado. Esses arquivos de script não contêm informações confidenciais.  


 > [!Note]
 > A partir da versão 1802, o modelo de sequência de tarefas padrão para o atualização in-loco do Windows 10 inclui grupos adicionais com ações recomendadas a serem adicionadas antes e após o processo de atualização. Essas ações são comuns entre muitos clientes que atualizam com sucesso os dispositivos para o Windows 10. Para obter mais informações, consulte as etapas de sequência de tarefas recomendadas [para preparar a atualização](#recommended-task-sequence-steps-to-prepare-for-upgrade) e [para o pós-processamento](#recommended-task-sequence-steps-for-post-processing).



## <a name="configure-pre-cache-content"></a>Configurar o conteúdo de armazenamento prévio em cache
<!--1021244-->
O recurso pré-cache para as implantações disponíveis de sequências de tarefas permite que os clientes baixem o conteúdo relevante do pacote de atualização do sistema operacional antes que um usuário instale a sequência de tarefas.  

> [!TIP]  
> Esse recurso foi introduzido na versão 1702 como um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1706, esse recurso não é mais um recurso de pré-lançamento.  


> [!Note]  
> O Configuration Manager não habilita esse recurso opcional por padrão. É necessário habilitar esse recurso antes de usá-lo. Para obter mais informações, veja [Habilitar recursos opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Por exemplo, você deseja apenas ter uma sequência de tarefas de atualização in-loco para todos os usuários e tem muitas arquiteturas e muitos idiomas. Nas versões anteriores, o conteúdo começa a ser baixado quando o usuário instala uma implantação de sequência de tarefas disponível no Centro de Software. Esse atraso acrescenta tempo extra antes que a instalação esteja pronta para ser iniciada. Todo o conteúdo referenciado na sequência de tarefas é baixado. Esse conteúdo inclui o pacote de upgrade do sistema operacional para todas as arquiteturas e linguagens. Se cada pacote de upgrade tiver aproximadamente três GB, o conteúdo total será muito grande.

O conteúdo pré-cache oferece a opção de permitir que o cliente baixe apenas o pacote de atualização do sistema operacional, bem como todos os outros tipos de conteúdo referenciado, assim que ele receber a implantação. Quando o usuário clica em **Instalar** no Centro de Software, o conteúdo está pronto e a instalação é iniciada rapidamente, pois o conteúdo está no disco rígido local.

 > [!NOTE]
 > No momento, esse comportamento se aplica apenas ao pacote de atualização do sistema operacional. Esse pacote é o único conteúdo no qual você especifica a arquitetura ou o idioma correspondente. Por exemplo, se a sequência de tarefas também referencia vários pacotes de driver, atualmente, o cliente baixa todos eles. O mecanismo de sequência de tarefas avalia as condições nas etapas quando a sequência de tarefas é executada, não com antecedência. O cliente usa as marcas nas propriedades do pacote para determinar qual conteúdo pré-armazenar em cache.

### <a name="to-configure-the-pre-cache-feature"></a>Para configurar o recurso de armazenamento prévio em cache

1. Crie pacotes de atualização do sistema operacional para arquiteturas e idiomas específicos. Especifique a arquitetura e o idioma na guia **Fonte de Dados** do pacote. Para o idioma, use a conversão decimal. Por exemplo, 1033 é o valor decimal para o inglês e 0x0409 é o equivalente hexadecimal.

    O cliente avalia os valores de arquitetura e linguagem para determinar qual pacote de atualização do sistema operacional é baixado durante o pré-cache.

1. Crie uma sequência de tarefas com etapas condicionais para diferentes idiomas e arquiteturas. Por exemplo, a seguinte etapa usa a versão em inglês:

    ![Editor de sequência de tarefas mostrando várias etapas de Atualização do sistema operacional para ENU, DEU e JPN](../media/precacheproperties2.png)

    ![Editor de sequência de tarefas, guia Opções, exibindo a consulta WMI WQL para Locale e OSArchitecture](../media/precacheoptions2.png)  

3. Implantar a sequência de tarefas. Para o recurso de pré-cache, defina as seguintes configurações:
    - Na guia **Geral**, selecione **Conteúdo previamente baixado para esta sequência de tarefas**.
    - Na guia **Configurações de implantação**, configure a sequência de tarefas com **Disponível** para **Finalidade**.
    - Na guia **Agendamento**, para a configuração **Agendar quando esta implantação estará disponível**, escolha a hora selecionada no momento. O cliente inicia o pré-armazenamento em cache do conteúdo no tempo disponível da implantação. Quando um cliente de destino recebe essa política, o tempo disponível está no passado e, portanto, o download pré-cache é iniciado imediatamente. Se o cliente recebe essa política, mas o tempo disponível está no futuro, o cliente não inicia o pré-armazenamento em cache do conteúdo até que ocorra o tempo disponível. 
    - Na guia **Pontos de Distribuição**, defina as configurações **Opções de implantação**. Se o conteúdo não for previamente armazenado em cache antes que um usuário inicie a instalação, o cliente usará essas configurações.
  

### <a name="user-experience"></a>Experiência do usuário
- Quando o cliente receber a política de implantação, ele iniciará o pré-cache do conteúdo após o tempo disponível da implantação. Esse conteúdo inclui todos os pacotes referenciados, mas apenas o pacote de atualização do sistema operacional que corresponde aos atributos de arquitetura e de idioma do pacote.
- Quando o cliente disponibiliza a implantação para os usuários, uma notificação é exibida para informar os usuários sobre a nova implantação. Agora a sequência de tarefas está visível no Centro de Software. O usuário poderá acessar o Centro de Software e clicar em **Instalar** para iniciar a instalação.
- Se o conteúdo não for totalmente pré-armazenado em cache quando o usuário instalar a sequência de tarefas, o cliente usará as configurações especificadas na guia **Opção de Implantação** da implantação. 



## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>Etapas recomendadas da sequência de tarefas para preparar a atualização

A partir da versão 1802, o modelo de sequência de tarefas padrão para o atualização in-loco do Windows 10 inclui grupos adicionais com ações recomendadas a serem adicionadas antes do processo de atualização. Essas ações do grupo **Preparar a Atualização** são comuns entre muitos clientes que atualizam com êxito seus dispositivos para o Windows 10. Para os sites com versões anteriores a 1802, adicione essas ações manualmente à sequência de tarefas no grupo **Preparar Atualização**.
- **Verificações da bateria**: adicione etapas neste grupo para verificar se o computador está usando bateria ou energia com fio. Esta ação requer um script personalizado ou um utilitário para executar esta verificação.
- **Verificações de rede/conexão com fio**: adicione etapas neste grupo para verificar se o computador está conectado a uma rede e não está usando uma conexão sem fio. Esta ação requer um script personalizado ou um utilitário para executar esta verificação.
- **Remover aplicativos incompatíveis**: adicione etapas neste grupo para remover quaisquer aplicativos incompatíveis com esta versão do Windows 10. O método para desinstalar um aplicativo varia. Se o aplicativo usar o Windows Installer, copie a linha de comando **Desinstalar programa** da guia **Programas** nas propriedades do tipo de implantação do Windows Installer do aplicativo. Em seguida, adicione uma etapa **Executar linha de comando** neste grupo com a linha de comando Desinstalar programa. Por exemplo: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **Remover drivers incompatíveis**: adicione etapas neste grupo para remover os drivers que são incompatíveis com esta versão do Windows 10.
- **Remover/suspender segurança de terceiros**: adicione etapas neste grupo para remover ou suspender programas de segurança de terceiros, como antivírus.
   - Se você estiver usando um programa de criptografia de disco de terceiros, forneça seu driver de criptografia à Instalação do Windows com a [opção de linha de comando](/windows-hardware/manufacture/desktop/windows-setup-command-line-options) **/ReflectDrivers**. Adicione uma etapa [Definir variável de sequência de tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) para a sequência de tarefas neste grupo. Defina a variável de sequência de tarefas como **OSDSetupAdditionalUpgradeOptions**. Defina o valor para **/ReflectDriver** com o caminho para o driver. Esta [variável de ação de sequências de tarefas](/sccm/osd/understand/task-sequence-action-variables#upgrade-operating-system) anexa a linha de comando da Instalação do Windows usada pela sequência de tarefas. Entre em contato com o fornecedor do software para obter qualquer orientação adicional sobre este processo.

### <a name="download-package-content-task-sequence-step"></a>Baixar etapa de sequência de tarefas do conteúdo do pacote  
 A etapa [Baixar Conteúdo do Pacote](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) pode ser usada antes da etapa **Atualizar o Sistema Operacional** nos seguintes cenários:  

-   Use uma única sequência de tarefas de upgrade para as plataformas x86 e x64. Inclua duas etapas **Baixar Conteúdo do Pacote** no grupo **Preparar Upgrade**. Defina as condições em cada etapa para detectar a arquitetura do cliente. Essa condição faz com que a etapa baixe apenas o pacote de upgrade do sistema operacional apropriado. Configure cada etapa **Baixar Conteúdo do Pacote** para usar a mesma variável e use a variável para o caminho de mídia na etapa **Atualizar Sistema Operacional** .  

-   Para baixar um pacote de drivers aplicáveis dinamicamente, use duas etapas **Baixar Conteúdo do Pacote** com condições para detectar o tipo de hardware apropriado para cada pacote de drivers. Configure cada etapa **Baixar Conteúdo do Pacote** para usar a mesma variável. Em seguida, use essa variável para o valor **Conteúdo de teste** na seção de drivers da etapa **Fazer upgrade do sistema operacional**.  

   > [!NOTE]
   > Quando há mais de um pacote, o Configuration Manager adiciona um sufixo numérico ao nome da variável. Por exemplo, se você especificar uma variável %mycontent% como uma variável personalizada, esse local será onde o cliente armazenará todo o conteúdo referenciado. Quando você faz referência à variável em uma etapa posterior, como **Fazer Upgrade do Sistema Operacional**, use a variável com um sufixo numérico. Neste exemplo, %mycontent01% ou %mycontent02%, em que o número corresponde à ordem na qual a etapa **Baixar Conteúdo do Pacote** lista o conteúdo específico.



## <a name="recommended-task-sequence-steps-for-post-processing"></a>Etapas recomendadas da sequência de tarefas para o pós-processamento   
 Depois de criar a sequência de tarefas, adicione outras etapas ao grupo **Pós-processamento** da sequência de tarefas.  

> [!NOTE]  
>  Essa sequência de tarefas não é linear. Existem condições nas etapas que podem afetar os resultados da sequência de tarefas. Esse comportamento depende de se ele foi atualizado com êxito no computador cliente ou se ele precisa reverter o computador cliente para o sistema operacional original.  

A partir da versão 1802, o modelo de sequência de tarefas padrão para o atualização in-loco do Windows 10 inclui grupos adicionais com ações recomendadas a serem adicionadas após o processo de atualização. Essas ações do grupo **Pós-processamento** são comuns entre muitos clientes que atualizam com êxito seus dispositivos para o Windows 10. Para os sites com versões anteriores a 1802, adicione essas ações manualmente à sequência de tarefas no grupo **Pós-processamento**.
- **Aplicar drivers baseados em instalação**: adicione etapas neste grupo para instalar drivers baseados em instalação (.exe) de pacotes.
- **Instalar/habilitar a segurança de terceiros**: adicione etapas neste grupo para instalar ou habilitar programas de segurança de terceiros, como antivírus. 
- **Definir aplicativos e associações padrão do Windows**: adicione etapas neste grupo para definir aplicativos e associações de arquivos padrão do Windows. Primeiro prepare um computador de referência com suas associações de aplicativos desejadas. Em seguida, execute a seguinte linha de comando para exportar: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Adicione o arquivo XML a um pacote. Em seguida, adicione uma etapa [Executar linha de comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) neste grupo. Especifique o pacote que contém o arquivo XML e, em seguida, especifique a seguinte linha de comando: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Para saber mais, confira [Exportar ou importar associações de aplicativos padrão](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).
- **Aplicar personalizações**: adicione etapas a este grupo para aplicar as personalizações do menu Iniciar, como a organização de grupos de programas. Para saber mais, confira [Personalizar a Tela Inicial](/windows-hardware/manufacture/desktop/customize-the-start-screen).



## <a name="optional-task-sequence-steps-for-rollback"></a>Etapas opcionais da sequência de tarefas para reversão  
 Quando algo der errado com o processo de upgrade depois que o computador for reiniciado, a Instalação do Windows reverterá o upgrade para o sistema operacional anterior. Em seguida, a sequência de tarefas continua com as etapas do grupo **Reversão**. Depois de criar a sequência de tarefas, adicione etapas opcionais ao grupo Reversão. Por exemplo, reverta as alterações feitas no sistema no grupo Preparar Atualização, como a desinstalação de software incompatível.



## <a name="additional-recommendations"></a>Recomendações adicionais
- Examine a documentação do Windows para [Resolver erros de upgrade do Windows 10](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Este artigo também inclui informações detalhadas sobre o processo de upgrade.
- Na etapa padrão **Verificar a prontidão**, ative  **Verificar o espaço mínimo em disco (MB)**. Defina o valor para pelo menos **16384** (16 GB) para um pacote de upgrade do SO de 32 bits ou **20480** (20 GB) de 64 bits. 
- Use a [variável de sequência de tarefas interna](/sccm/osd/understand/task-sequence-built-in-variables) **SMSTSDownloadRetryCount** para repetir a política de download. Atualmente, por padrão, o cliente tenta novamente duas vezes; essa variável é definida como dois (2). Se seus clientes não estiverem conectados a uma conexão de rede corporativa com fio, tentativas adicionais ajudam o cliente a obter uma política. Usar esta variável não causa nenhum efeito colateral negativo, além de uma falha em atraso caso a política não possa ser baixada.<!-- 501016 --> Além disso, aumente a variável **SMSTSDownloadRetryDelay** dos 15 segundos padrão.
- Execute uma avaliação de compatibilidade em linha. 
   - Adicione uma segunda etapa **Atualizar sistema operacional** no início do grupo **Preparar para Upgrade**. Chame-o de *Avaliação de upgrade*. Especifique o mesmo pacote de upgrade e, em seguida, ative a opção para **Executar verificação de compatibilidade da Instalação do Windows sem iniciar o upgrade**. Habilite **Continuar em caso de erro** na guia Opções. 
   - Imediatamente após esta etapa *Avaliação do upgrade*, adicione uma etapa **Executar linha de comando**. Especifique a seguinte linha de comando:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>Na guia **Opções**, adicione as seguintes condições: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Este código de retorno é o equivalente decimal de MOSETUP_E_COMPAT_SCANONLY (0xC1900210), que é uma verificação de compatibilidade bem-sucedida sem problemas. Se a etapa *Avaliação do upgrade* for bem-sucedida e retornar esse código, esta etapa será ignorada. Caso contrário, se a etapa de avaliação retornar qualquer outro código de retorno, esta etapa falha na sequência de tarefas com o código de retorno da verificação de compatibilidade da Instalação do Windows.
   - Para saber mais, confira [Upgrade do sistema operacional](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS).
- Se você quiser mudar o dispositivo do BIOS para UEFI durante esta sequência de tarefas, veja [Converter de BIOS para UEFI durante um upgrade in-loco](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).
