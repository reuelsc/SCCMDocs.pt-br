---
title: Criar uma sequência de tarefas de atualização do sistema operacional
titleSuffix: Configuration Manager
description: Usar uma sequência de tarefas para a atualização automática do Windows 7 ou posterior para o Windows 10
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bc20a7e9be271bde8a5cd6464e2cebdf1ee9bad9
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138595"
---
# <a name="create-a-task-sequence-to-upgrade-an-os-in-configuration-manager"></a>Criar uma sequência de tarefas para atualizar um sistema operacional no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use sequências de tarefas no Configuration Manager para atualizar um sistema operacional automaticamente em um computador de destino. Esse upgrade pode ser do Windows 7 ou posterior para o Windows 10, ou do Windows Server 2012 ou posterior para o Windows Server 2016. Crie uma sequência de tarefas que referencia o pacote de atualização do sistema operacional e outros tipos de conteúdo a serem instalados, como aplicativos ou atualizações de software. A sequência de tarefas para atualizar um sistema operacional faz parte do cenário [Atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md).  



## <a name="prerequisites"></a>Pré-requisitos

Antes de criar a sequência de tarefas, os seguintes requisitos devem estar em vigor:    

#### <a name="required"></a>Necessária  

- O [Pacote de atualização do sistema operacional](/sccm/osd/get-started/manage-operating-system-upgrade-packages) precisa estar disponível no console do Configuration Manager.  

- Ao fazer upgrade para o Windows Server 2016, selecione a configuração **Ignorar quaisquer mensagens descartáveis de compatibilidade** na etapa da sequência de tarefas Fazer Upgrade do Sistema Operacional. Caso contrário, a atualização falhará.  

#### <a name="required-if-used"></a>Necessário (se usado)  

-   As [atualizações de software](/sccm/sum/get-started/synchronize-software-updates) devem estar sincronizadas no console do Configuration Manager.  

-   Os [aplicativos](/sccm/apps/deploy-use/create-applications) devem ser adicionados ao console do Configuration Manager.  



##  <a name="BKMK_UpgradeOS"></a> Criar uma sequência de tarefas para atualizar um sistema operacional  

Para atualizar o sistema operacional nos clientes, crie uma sequência de tarefas e selecione **Atualizar um sistema operacional usando o pacote de atualização** no Assistente para Criar Sequência de Tarefas. O assistente adiciona as etapas da sequência de tarefas para atualizar o sistema operacional, aplicar atualizações de software e instalar aplicativos. 

#### <a name="to-create-a-task-sequence-that-upgrades-an-os"></a>Para criar uma sequência de tarefas que atualiza um sistema operacional  

1.  No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e clique em **Sequências de Tarefas**.  

2.  Na guia **Início** da faixa de opções, no grupo **Criar**, clique em **Criar Sequência de Tarefas**.  

3.  Na página **Criar uma Nova Sequência de Tarefas** do Assistente para Criar Sequência de Tarefas, selecione **Atualizar um sistema operacional usando um pacote de atualização** e, em seguida, clique em **Avançar**.  

4.  Na página **Informações da Sequência de Tarefas**, especifique as seguintes configurações e clique em **Avançar**:  

    -   **Nome da sequência de tarefas**: especifique um nome que identifique a sequência de tarefas.  

    -   **Descrição**: opcionalmente, especifique uma descrição.  

5.  Na página **Atualizar o Sistema Operacional Windows**, especifique as seguintes configurações e, em seguida, clique em **Avançar**:  

    -   **Pacote de atualização**: especifique o pacote de atualização que contém os arquivos de origem de atualização do sistema operacional. Verifique se você selecionou o pacote de atualização correto examinando as informações no painel **Propriedades**. Para obter mais informações, confira [Gerenciar pacotes de atualização do sistema operacional](/sccm/osd/get-started/manage-operating-system-upgrade-packages).  

    -   **Índice de edição**: se houver vários índices de edição do sistema operacional disponíveis no pacote, selecione o índice de edição desejado. Por padrão, o assistente seleciona o primeiro índice.  

    -   **Chave do produto (Product Key)**: especifique a chave do produto do Windows para o sistema operacional instalar. Especifique as chaves de licença de volume codificadas ou as chaves do produto padrão. Se você usar uma chave do produto (Product Key) padrão, separe cada grupo de cinco caracteres com um traço (-). Por exemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Quando a atualização for para uma edição de licença de volume, a chave do produto (Product Key) não será necessária.  

        > [!Note]  
        > Essa chave de produto pode ser uma MAK (chave de ativação múltipla) ou uma GVLK (chave genérica de licenciamento por volume). Uma GVLK também é conhecida como uma chave de instalação de cliente do KMS (Serviço de Gerenciamento de Chaves). Para obter mais informações, consulte [Planejar a ativação de volume](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Para obter uma lista de chaves de instalação de cliente do KMS, veja o [Apêndice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) do guia de ativação do Windows Server. 

    -   **Ignorar quaisquer mensagens de compatibilidade rejeitadas**: selecione esta configuração se estiver atualizando para o Windows Server 2016. Se você não selecionar essa configuração, a sequência de tarefas não conseguirá ser concluída porque a Instalação do Windows estará esperando que o usuário clique em **Confirmar** em uma caixa de diálogo de compatibilidade de aplicativo do Windows.   

7.  Na página **Incluir Atualizações**, especifique se desejar instalar as atualizações de software obrigatórias, todas ou nenhuma. Clique em **Avançar**. Se você especificar a instalação das atualizações de software, o Configuration Manager instalará somente as atualizações direcionadas às coleções das quais o computador de destino é membro.  

8.  Na página **Instalar Aplicativos** , especifique os aplicativos a instalar no computador de destino e clique em **Próximo**. Se você selecionar mais de um aplicativo, especifique também se a sequência de tarefas deverá continuar se a instalação de um aplicativo específico falhar.  

9. Conclua o assistente.  


> [!Important]  
> Quando a sequência de tarefas é executada em um dispositivo, o cliente do Configuration Manager cria vários scripts para controlar o comportamento da sequência de tarefas em vários cenários. Quando a sequência de tarefas é concluída, o cliente não remove esses scripts até que o computador seja reiniciado. Esses arquivos de script não contêm informações confidenciais.  


A partir da versão 1802, o modelo de sequência de tarefas padrão para o atualização in-loco do Windows 10 inclui grupos adicionais com ações recomendadas a serem adicionadas antes e após o processo de atualização. Essas ações são comuns entre muitos clientes que atualizam com sucesso os dispositivos para o Windows 10. Para obter mais informações, consulte as etapas de sequência de tarefas recomendadas [para preparar a atualização](#recommended-task-sequence-steps-to-prepare-for-upgrade) e [para o pós-processamento](#recommended-task-sequence-steps-for-post-processing).

Começando na versão 1806, esse modelo de sequência de tarefas também inclui um grupo com as ações recomendadas a serem adicionadas no caso de falha do processo de atualização. Essas ações facilitam a solução de problemas. Para obter mais informações, confira [etapas de sequência de tarefas recomendadas em caso de falha](#recommended-task-sequence-steps-on-failure).<!--1358500-->  



## <a name="configure-pre-cache-content"></a>Configurar o conteúdo de armazenamento prévio em cache
<!--1021244--> O recurso pré-cache para as implantações disponíveis de sequências de tarefas permite que os clientes baixem o conteúdo relevante do pacote de atualização do sistema operacional antes que um usuário instale a sequência de tarefas.  

> [!Note]  
> O Configuration Manager não habilita esse recurso opcional por padrão. É necessário habilitar esse recurso antes de usá-lo. Para obter mais informações, veja [Habilitar recursos opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Por exemplo, você deseja apenas ter uma sequência de tarefas de atualização in-loco para todos os usuários e tem muitas arquiteturas e muitos idiomas. Nas versões anteriores, o conteúdo começa a ser baixado quando o usuário instala uma implantação de sequência de tarefas disponível no Centro de Software. Esse atraso acrescenta tempo extra antes que a instalação esteja pronta para ser iniciada. Todo o conteúdo referenciado na sequência de tarefas é baixado. Esse conteúdo inclui o pacote de atualização do sistema operacional para todas as arquiteturas e idiomas. Se cada pacote de atualização tiver aproximadamente 3 GB, o conteúdo total será muito grande.

O conteúdo pré-cache oferece a opção para que o cliente baixe apenas o pacote de atualização do sistema operacional aplicável e todos os outros tipos de conteúdo referenciados, assim que ele recebe a implantação. Quando o usuário clica **Instalar** no Centro de Software, o conteúdo está pronto. A instalação inicia-se rapidamente, pois o conteúdo está no disco rígido local.

> [!NOTE]  
> No momento, esse comportamento se aplica apenas ao pacote de atualização do sistema operacional. Esse pacote é o único conteúdo no qual você especifica a arquitetura ou o idioma correspondente. Por exemplo, se a sequência de tarefas também referencia vários pacotes de driver, atualmente, o cliente baixa todos eles. O mecanismo de sequência de tarefas avalia as condições nas etapas quando a sequência de tarefas é executada, não com antecedência. O cliente usa as marcas nas propriedades do pacote para determinar qual conteúdo pré-armazenar em cache.


### <a name="to-configure-the-pre-cache-feature"></a>Para configurar o recurso de armazenamento prévio em cache

1. Crie pacotes de atualização do sistema operacional para arquiteturas e idiomas específicos. Especifique a arquitetura e o idioma na guia **Fonte de Dados** do pacote. Para o idioma, use a conversão decimal. Por exemplo, **1033** é o valor decimal para inglês, e **0x0409** é o equivalente hexadecimal.  

    O cliente avalia os valores de arquitetura e linguagem para determinar qual pacote de atualização do sistema operacional é baixado durante o pré-cache.  

2. Crie uma sequência de tarefas com etapas condicionais para diferentes idiomas e arquiteturas. Por exemplo, a seguinte etapa usa a versão em inglês:  

    ![Editor de sequência de tarefas mostrando várias etapas de Atualização do sistema operacional para ENU, DEU e JPN](../media/precacheproperties2.png)

    ![Editor de sequência de tarefas, guia Opções, exibindo a consulta WMI WQL para Locale e OSArchitecture](../media/precacheoptions2.png)  

3. Implantar a sequência de tarefas. Para o recurso de pré-cache, defina as seguintes configurações:  

    - Na guia **Geral**, selecione **Conteúdo previamente baixado para esta sequência de tarefas**.  

    - Na guia **Configurações de implantação**, configure a sequência de tarefas com **Disponível**.  

    - Na guia **Agendamento**, escolha a hora selecionada no momento para a configuração **Agendar quando esta implantação estiver disponível**. O cliente inicia o pré-armazenamento em cache do conteúdo no tempo disponível da implantação. Quando um cliente de destino recebe essa política, o tempo disponível está no passado e, portanto, o download pré-cache é iniciado imediatamente. Se o cliente recebe essa política, mas o tempo disponível está no futuro, o cliente não inicia o conteúdo de pré-armazenamento em cache até que chegue o horário de disponibilidade.  

    - Na guia **Pontos de Distribuição**, defina as configurações **Opções de implantação**. Se o conteúdo não for pré-armazenado em cache antes que um usuário inicie a instalação, o cliente usará essas configurações.  
  

### <a name="user-experience"></a>Experiência do usuário

- Quando o cliente receber a política de implantação, ele iniciará o pré-cache do conteúdo após o tempo disponível da implantação. Esse conteúdo inclui todos os pacotes referenciados, mas apenas o pacote de atualização do sistema operacional que corresponde aos atributos de arquitetura e de idioma do pacote.  

- Quando o cliente disponibiliza a implantação para os usuários, uma notificação é exibida para informar os usuários sobre a nova implantação. Agora a sequência de tarefas está visível no Centro de Software. O usuário poderá acessar o Centro de Software e clicar em **Instalar** para iniciar a instalação.  

- Se o cliente não pré-armazenar o conteúdo em cache totalmente quando o usuário instalar a sequência de tarefas, ele usará as configurações especificadas na guia **Opção de Implantação** da implantação.  



## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>Etapas recomendadas da sequência de tarefas para preparar a atualização

A partir da versão 1802, o modelo de sequência de tarefas padrão para o atualização in-loco do Windows 10 inclui grupos adicionais com ações recomendadas a serem adicionadas antes do processo de atualização. Essas ações do grupo **Preparar a Atualização** são comuns entre muitos clientes que atualizam com êxito seus dispositivos para o Windows 10. Para os sites com versões anteriores a 1802, adicione essas ações manualmente à sequência de tarefas no grupo **Preparar Atualização**.  

- **Verificações de bateria**: adicione etapas nesse grupo para verificar se o computador está usando bateria ou alimentação com fio. Esta ação requer um script personalizado ou um utilitário para executar esta verificação.  

- **Verificações de conexão de rede/com fio**: adicione etapas nesse grupo para verificar se o computador está conectado a uma rede e não está usando uma conexão sem fio. Esta ação requer um script personalizado ou um utilitário para executar esta verificação.  

- **Remover aplicativos incompatíveis**: adicione etapas nesse grupo para remover todos os aplicativos que são incompatíveis com esta versão do Windows 10. O método para desinstalar um aplicativo varia.  

    - Se o aplicativo usar o Windows Installer, copie a linha de comando **Desinstalar programa** da guia **Programas** nas propriedades do tipo de implantação do Windows Installer do aplicativo. Em seguida, adicione uma etapa **Executar linha de comando** neste grupo com a linha de comando Desinstalar programa. Por exemplo: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br>  

- **Remover drivers incompatíveis**: adicione etapas nesse grupo para remover os drivers que são incompatíveis com esta versão do Windows 10.  

- **Remover/suspender segurança de terceiros**: adicione etapas nesse grupo para remover ou suspender programas de segurança de terceiros, como antivírus.  

   - Se você estiver usando um programa de criptografia de disco de terceiros, forneça seu driver de criptografia à Instalação do Windows com a [opção de linha de comando](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#23)`/ReflectDrivers`. Adicione uma etapa [Definir variável de sequência de tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) para a sequência de tarefas neste grupo. Defina a variável de sequência de tarefas como **OSDSetupAdditionalUpgradeOptions**. Defina o valor como `/ReflectDrivers` com o caminho para o driver. Esta [variável de sequências de tarefas](/sccm/osd/understand/task-sequence-variables#OSDSetupAdditionalUpgradeOptions) anexa a linha de comando da Instalação do Windows usada pela sequência de tarefas. Entre em contato com o fornecedor do software para obter qualquer orientação adicional sobre este processo.  


### <a name="download-package-content-task-sequence-step"></a>Baixar etapa de sequência de tarefas do conteúdo do pacote  

Use a etapa [Baixar Conteúdo do Pacote](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent) antes da etapa **Atualizar o Sistema Operacional** nos seguintes cenários:  

-   Use uma única sequência de tarefas de upgrade para as plataformas x86 e x64. Inclua duas etapas **Baixar Conteúdo do Pacote** no grupo **Preparar Upgrade**. Defina as condições em cada etapa para detectar a arquitetura do cliente. Essa condição faz com que a etapa baixe apenas o pacote de atualização do sistema operacional apropriado. Configure cada etapa **Baixar Conteúdo do Pacote** para usar a mesma variável e use a variável para o caminho de mídia na etapa **Atualizar Sistema Operacional** .  

-   Para baixar um pacote de drivers aplicáveis dinamicamente, use duas etapas **Baixar Conteúdo do Pacote** com condições para detectar o tipo de hardware apropriado para cada pacote de drivers. Configure cada etapa **Baixar Conteúdo do Pacote** para usar a mesma variável. Em seguida, use essa variável para o valor **Conteúdo de teste** na seção de drivers da etapa **Fazer upgrade do sistema operacional**.  

    > [!NOTE]  
    > Quando há mais de um pacote, o Configuration Manager adiciona um sufixo numérico ao nome da variável. Por exemplo, se você especificar `%mycontent%` como uma variável personalizada, o cliente armazenará todo o conteúdo referenciado nesse local. Quando você faz referência à variável em uma etapa posterior, como **Fazer Upgrade do Sistema Operacional**, use a variável com um sufixo numérico. Neste exemplo, `%mycontent01%` ou `%mycontent02%`, em que o número corresponde à ordem na qual a etapa **Baixar Conteúdo do Pacote** lista o conteúdo específico.  



## <a name="recommended-task-sequence-steps-for-post-processing"></a>Etapas recomendadas da sequência de tarefas para o pós-processamento   

Depois de criar a sequência de tarefas, adicione outras etapas ao grupo **Pós-processamento** da sequência de tarefas.  

> [!NOTE]  
>  Essa sequência de tarefas não é linear. Existem condições nas etapas que podem afetar os resultados da sequência de tarefas. Esse comportamento depende de se ele foi atualizado com êxito no computador cliente ou se ele precisa reverter o computador cliente para o sistema operacional original.  

A partir da versão 1802, o modelo de sequência de tarefas padrão para o atualização in-loco do Windows 10 inclui grupos adicionais com ações recomendadas a serem adicionadas após o processo de atualização. Essas ações do grupo **Pós-processamento** são comuns entre muitos clientes que atualizam com êxito seus dispositivos para o Windows 10. Para os sites com versões anteriores a 1802, adicione essas ações manualmente à sequência de tarefas no grupo **Pós-processamento**.  

- **Aplicar drivers baseados em instalação**: Adicione etapas nesse grupo para instalar drivers baseados em instalação (.exe) de pacotes.  

- **Instalar/habilitar segurança de terceiros**: adicione etapas nesse grupo para instalar ou habilitar programas de segurança de terceiros, como antivírus.  

- **Definir aplicativos e associações padrão do Windows**: adicione etapas nesse grupo para definir os aplicativos e as associações de arquivo padrão do Windows. Primeiro prepare um computador de referência com suas associações de aplicativos desejadas. Em seguida, execute a seguinte linha de comando para exportar: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Adicione o arquivo XML a um pacote. Em seguida, adicione uma etapa [Executar linha de comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) neste grupo. Especifique o pacote que contém o arquivo XML e, em seguida, especifique a seguinte linha de comando: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Para saber mais, confira [Exportar ou importar associações de aplicativos padrão](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).  

- **Aplicar personalizações**: adicione etapas nesse grupo para aplicar personalizações do menu Iniciar, como organizar grupos de programas. Para saber mais, confira [Personalizar a Tela Inicial](/windows-hardware/manufacture/desktop/customize-the-start-screen).  



## <a name="optional-task-sequence-steps-for-rollback"></a>Etapas opcionais da sequência de tarefas para reversão  

Quando algo der errado com o processo de atualização depois que o computador for reiniciado, a Instalação do Windows reverterá a atualização para o sistema operacional anterior. Em seguida, a sequência de tarefas continua com as etapas do grupo **Reversão**. Depois de criar a sequência de tarefas, adicione etapas opcionais neste grupo, conforme o necessário. Por exemplo, reverta as alterações feitas no sistema no grupo Preparar Atualização, como a desinstalação de software incompatível.



## <a name="recommended-task-sequence-steps-on-failure"></a>Etapas de sequência de tarefas recomendada em caso de falha
<!--1358500-->

Começando na versão 1806, o modelo de sequência de tarefas padrão para a atualização in-loco do Windows 10 inclui um grupo para **Executar ações em caso de falha**. Esse grupo inclui as ações recomendadas a serem adicionadas em caso de falha do processo de atualização. Essas ações facilitam a solução de problemas.

- **Coletar logs**: para reunir logs do cliente, adicione etapas a este grupo.  

    - Uma prática comum é copiar os arquivos de log para um compartilhamento de rede. Para estabelecer essa conexão, use a etapa [Conectar à Pasta de Rede](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder).  

    - Para executar a operação de cópia, use um script ou utilitário personalizado com a etapa [Executar Linha de Comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) ou [Executar script do PowerShell](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript).  

    - Os arquivos a coletar podem incluir os seguintes logs:  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  

    - Para saber mais sobre o setupact.log e outros logs da Instalação do Windows, confira [Arquivos de Log de Instalação do Windows](https://docs.microsoft.com/windows/deployment/upgrade/log-files).  

    - Para obter mais informações sobre os logs do cliente do Configuration Manager, confira [Logs do cliente do Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs).  

    - Para saber mais sobre **_SMSTSLogPath** e outras variáveis ​​úteis, consulte [Variáveis ​​da sequência de tarefas](/sccm/osd/understand/task-sequence-variables).  

- **Executar as ferramentas de diagnóstico**: para executar ferramentas de diagnóstico adicionais, adicione etapas a este grupo. Automatize essas ferramentas para coletar informações adicionais do sistema logo após a falha.  

    - Uma dessas ferramentas é o Windows [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag). É uma ferramenta de diagnóstico autônoma para obter detalhes sobre por que uma atualização do Windows 10 não foi bem-sucedida.  

        - No Configuration Manager, [crie um pacote](/sccm/apps/deploy-use/packages-and-programs#create-a-package-and-program) para a ferramenta.  

        - Adicionar uma etapa [Executar Linha de comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) para este grupo da sua sequência de tarefas. Use a opção **Pacote** para fazer referência à ferramenta. A cadeia de caracteres a seguir é um exemplo de **Linha de Comando**:  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`  



## <a name="additional-recommendations"></a>Recomendações adicionais

- Examine a documentação do Windows para [Resolver erros de upgrade do Windows 10](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Este artigo também inclui informações detalhadas sobre o processo de upgrade.  

- Na etapa padrão **Verificar a prontidão**, ative  **Verificar o espaço mínimo em disco (MB)**. Defina o valor para pelo menos **16384** (16 GB) para um pacote de upgrade do SO de 32 bits ou **20480** (20 GB) de 64 bits.  

- Use a **variável de sequência de tarefas** [SMSTSDownloadRetryCount](/sccm/osd/understand/task-sequence-variables#SMSTSDownloadRetryCount) para repetir a política de download. Atualmente, por padrão, o cliente tenta novamente duas vezes; essa variável é definida como dois (2). Se os clientes não estiverem conectados por uma conexão de rede de intranet com fio, haverá tentativas adicionais para ajudar o cliente a obter uma política. O uso dessa variável não causa nenhum efeito colateral negativo, além de uma falha em atraso caso a política não possa ser baixada.<!--501016--> Além disso, aumente a variável **SMSTSDownloadRetryDelay** dos 15 segundos padrão.  

- Execute uma avaliação de compatibilidade embutida:  

   - Adicione uma segunda etapa **Atualizar sistema operacional** no início do grupo **Preparar para Upgrade**. Chame-o de *Avaliação de upgrade*. Especifique o mesmo pacote de upgrade e, em seguida, ative a opção para **Executar verificação de compatibilidade da Instalação do Windows sem iniciar o upgrade**. Habilite **Continuar em caso de erro** na guia Opções.  

   - Imediatamente após esta etapa *Avaliação do upgrade*, adicione uma etapa **Executar linha de comando**. Especifique a seguinte linha de comando:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>Na guia **Opções**, adicione as seguintes condições: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Este código de retorno é o equivalente decimal de MOSETUP_E_COMPAT_SCANONLY (0xC1900210), que é uma verificação de compatibilidade bem-sucedida sem problemas. Quando a etapa *Avaliação de Atualização* é bem-sucedida e retorna esse código, a sequência de tarefas ignora esta etapa. Caso contrário, se a etapa de avaliação retornar qualquer outro código de retorno, esta etapa falha na sequência de tarefas com o código de retorno da verificação de compatibilidade da Instalação do Windows. Para saber mais sobre **_SMSTSOSUpgradeActionReturnCode**, consulte [Variáveis ​​da sequência de tarefas](/sccm/osd/understand/task-sequence-variables#SMSTSOSUpgradeActionReturnCode).  

   - Para saber mais, confira [Upgrade do sistema operacional](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS).  

- Se você quiser mudar o dispositivo do BIOS para UEFI durante esta sequência de tarefas, veja [Converter de BIOS para UEFI durante um upgrade in-loco](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).  

- Se você estiver usando a criptografia de disco do BitLocker, por padrão, a Instalação do Windows a suspenderá automaticamente durante a atualização. Começando no Windows 10 versão 1803, a Instalação do Windows inclui o parâmetro de linha de comando `/BitLocker` para controlar esse comportamento. Se os requisitos de segurança exigirem a criptografia de disco sempre ativa, use a [variável de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#OSDSetupAdditionalUpgradeOptions) **OSDSetupAdditionalUpgradeOptions** no grupo **Preparar para Atualização** para incluir `/BitLocker TryKeepActive`. Para obter mais informações, confira [Opções de linha de comando da Instalação do Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#33).<!--SCCMDocs issue #494-->  

- Alguns clientes removem os aplicativos padrão provisionados no Windows 10. Por exemplo, o aplicativo Bing Meteorologia ou o Microsoft Solitaire Collection. Em algumas situações, esses aplicativos retornam após a atualização do Windows 10. Para obter mais informações, confira [Como manter os aplicativos removidos do Windows 10](https://docs.microsoft.com/windows/application-management/remove-provisioned-apps-during-update). Adicione uma etapa **Executar Linha de Comando** à sequência de tarefas no grupo **Preparar para Atualização**. Especifique uma linha de comando semelhante ao exemplo a seguir:</br> `cmd /c reg delete "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Deprovisioned\Microsoft.BingWeather_8wekyb3d8bbwe" /f` <!--SCCMDocs issue #526-->  
