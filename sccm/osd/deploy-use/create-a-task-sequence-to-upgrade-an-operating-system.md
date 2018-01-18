---
title: "Criar uma sequência de tarefas para atualizar um sistema operacional"
titleSuffix: Configuration Manager
description: "Sequências de tarefas no System Center Configuration Manager podem atualizar automaticamente um sistema operacional do Windows 7 ou posterior para o Windows 10."
ms.custom: na
ms.date: 12/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: "12"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 058b0710484a0452ddf19655bf2cabbb43f624ad
ms.sourcegitcommit: 92c3f916e6bbd35b6208463ff406e0247664543a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>Crie uma sequência de tarefas para atualizar um sistema operacional no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use sequências de tarefas no Configuration Manager para fazer upgrade automaticamente de um sistema operacional em um computador de destino. Esse upgrade pode ser do Windows 7 ou posterior para o Windows 10, ou do Windows Server 2012 ou posterior para o Windows Server 2016. Você cria uma sequência de tarefas que referencia o pacote de upgrade do sistema operacional e qualquer outro conteúdo a ser instalado, como aplicativos ou atualizações de software. A sequência de tarefas para atualizar um sistema operacional faz parte do cenário [Atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md).  

##  <a name="BKMK_UpgradeOS"></a> Criar uma sequência de tarefas para atualizar um sistema operacional  
 Para atualizar o sistema operacional em computadores, você pode criar uma sequência de tarefas e selecionar a opção **Atualizar um sistema operacional do pacote de atualização** no assistente Criar Sequência de Tarefas. O assistente adicionará as etapas para atualizar o sistema operacional, aplicar atualizações de software e instalar aplicativos. Antes de criar a sequência de tarefas, os seguintes requisitos devem estar em vigor:    

-   **Necessária**  

     - O [pacote de atualização do sistema operacional](../get-started/manage-operating-system-upgrade-packages.md) deve estar disponível no console do Configuration Manager.
     - Ao fazer upgrade para o Windows Server 2016, selecione a configuração **Ignorar quaisquer mensagens descartáveis de compatibilidade** na etapa da sequência de tarefas Fazer Upgrade do Sistema Operacional. Caso contrário, o upgrade falhará.

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

7.  Na página **Incluir Atualizações** , especifique se deseja instalar as atualizações de software necessárias, todas as atualizações ou nenhuma e clique em **Próximo**. Se você optar pela instalação das atualizações de software, o Configuration Manager instalará somente as atualizações de software direcionadas às coleções das quais o computador de destino é membro.  

8.  Na página **Instalar Aplicativos** , especifique os aplicativos a instalar no computador de destino e clique em **Próximo**. Se você especificar vários aplicativos, será possível também definir a continuação da sequência de tarefas em caso de falha na instalação de algum aplicativo.  

9. Conclua o assistente.  



## <a name="configure-pre-cache-content"></a>Configurar o conteúdo de armazenamento prévio em cache
A partir da versão 1702, o recurso pré-cache para as implantações disponíveis de sequências de tarefas permite que os clientes baixem apenas o conteúdo relevante antes que um usuário instale a sequência de tarefas.
> [!TIP]  
> Esse recurso foi introduzido na versão 1702 como um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1706, esse recurso não é mais um recurso de pré-lançamento.

Por exemplo, digamos que você deseja implantar uma sequência de tarefas de atualização in-loco do Windows 10, deseja apenas uma sequência de tarefas para todos os usuários e tem várias arquiteturas e/ou idiomas. Nas versões anteriores, o conteúdo começa a ser baixado quando o usuário instala uma implantação de sequência de tarefas disponível no Centro de Software. Esse atraso acrescenta tempo extra antes que a instalação esteja pronta para ser iniciada. Além disso, todo o conteúdo referenciado na sequência de tarefas é baixado. Esse conteúdo inclui o pacote de upgrade do sistema operacional para todas as arquiteturas e linguagens. Se cada pacote de upgrade tiver aproximadamente três GB, o conteúdo total será muito grande.

O conteúdo de armazenamento prévio em cache oferece a opção de permitir que o cliente baixe apenas o conteúdo aplicável assim que receber a implantação. Portanto, quando o usuário clicar em **Instalar** no Centro de Software, o conteúdo estará pronto e a instalação iniciará rapidamente, pois o conteúdo está no disco rígido local.

### <a name="to-configure-the-pre-cache-feature"></a>Para configurar o recurso de armazenamento prévio em cache

1. Crie pacotes de atualização de sistema operacional para arquiteturas e idiomas específicos. Especifique a arquitetura e o idioma na guia **Fonte de Dados** do pacote. Para o idioma, use a conversão decimal (por exemplo, 1033 é o decimal para inglês e 0x0409 é o equivalente hexadecimal). Para ver mais detalhes, veja [Criar uma sequência de tarefas para atualizar um sistema operacional](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).

    Os valores de arquitetura e linguagem correspondem a condições nas etapas da sequência de tarefas para determinar se o pacote de upgrade do sistema operacional é pré-armazenado em cache.
1. Crie uma sequência de tarefas com etapas condicionais para diferentes idiomas e arquiteturas. Por exemplo, a seguinte etapa usa a versão em inglês:

    ![Propriedades de armazenamento prévio em cache](../media/precacheproperties2.png)

    ![Opções de armazenamento prévio em cache](../media/precacheoptions2.png)  

3. Implantar a sequência de tarefas. Para o recurso de pré-cache, defina as seguintes configurações:
    - Na guia **Geral**, selecione **Conteúdo previamente baixado para esta sequência de tarefas**.
    - Na guia **Configurações de implantação**, configure a sequência de tarefas com **Disponível** para **Finalidade**.
    - Na guia **Agendamento**, para a configuração **Agendar quando esta implantação estará disponível**, escolha a hora selecionada no momento. O cliente inicia o pré-armazenamento em cache do conteúdo no tempo disponível da implantação. Quando um cliente de destino recebe essa política, o tempo disponível está no passado e, portanto, o download pré-cache é iniciado imediatamente. Se o cliente recebe essa política, mas o tempo disponível está no futuro, o cliente não inicia o pré-armazenamento em cache do conteúdo até que ocorra o tempo disponível. 
    - Na guia **Pontos de Distribuição**, defina as configurações **Opções de implantação**. Se o conteúdo não tiver sido armazenado previamente em cache em um cliente antes de um usuário iniciar a instalação, essas configurações serão usadas.


### <a name="user-experience"></a>Experiência do usuário
- Quando o cliente receber a política de implantação, ele iniciará o pré-armazenamento em cache do conteúdo após o tempo disponível da implantação. Esse conteúdo inclui todos os pacotes referenciados e somente o pacote de upgrade do sistema operacional que corresponde ao cliente, com base nas condições definidas na sequência de tarefas.
- Quando a implantação é disponibilizada para os usuários, uma notificação é exibida para informar os usuários sobre a nova implantação e a sequência de tarefas fica visível no Centro de Software. O usuário poderá acessar o Centro de Software e clicar em **Instalar** para iniciar a instalação.
- Se o conteúdo não for totalmente pré-armazenado em cache quando o usuário instalar a sequência de tarefas, o cliente usará as configurações especificadas na guia **Opção de Implantação** da implantação. 



## <a name="download-package-content-task-sequence-step"></a>Baixar etapa de sequência de tarefas do conteúdo do pacote  
 A etapa [Baixar Conteúdo do Pacote](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) pode ser usada antes da etapa **Atualizar o Sistema Operacional** nos seguintes cenários:  

-   Use uma única sequência de tarefas de upgrade para as plataformas x86 e x64. Inclua duas etapas **Baixar Conteúdo do Pacote** no grupo **Preparar Upgrade**. Defina as condições em cada etapa para detectar a arquitetura do cliente. Essa condição faz com que a etapa baixe apenas o pacote de upgrade do sistema operacional apropriado. Configure cada etapa **Baixar Conteúdo do Pacote** para usar a mesma variável e use a variável para o caminho de mídia na etapa **Atualizar Sistema Operacional** .  

-   Para baixar um pacote de drivers aplicáveis dinamicamente, use duas etapas **Baixar Conteúdo do Pacote** com condições para detectar o tipo de hardware apropriado para cada pacote de drivers. Configure cada etapa **Baixar Conteúdo do Pacote** para usar a mesma variável. Em seguida, use essa variável para o valor **Conteúdo de teste** na seção de drivers da etapa **Fazer upgrade do sistema operacional**.  

   > [!NOTE]
   > Quando há mais de um pacote, o Configuration Manager adiciona um sufixo numérico ao nome da variável. Por exemplo, se você especificar uma variável %mycontent% como uma variável personalizada, esse local será onde o cliente armazenará todo o conteúdo referenciado. Quando você faz referência à variável em uma etapa posterior, como **Fazer Upgrade do Sistema Operacional**, use a variável com um sufixo numérico. Neste exemplo, %mycontent01% ou %mycontent02%, em que o número corresponde à ordem na qual a etapa **Baixar Conteúdo do Pacote** lista o conteúdo específico.

## <a name="optional-post-processing-task-sequence-steps"></a>Etapas opcionais de sequência de tarefas de pós-processamento  
 Depois de criar a sequência de tarefas, adicione outras etapas, conforme necessário. Por exemplo, desinstalar aplicativos com problemas de compatibilidade conhecidos ou adicionar ações de pós-processamento para execução depois que o computador for reiniciado e o upgrade para o Windows 10 for bem-sucedido. Adicione estas etapas adicionais no grupo de pós-processamento da sequência de tarefas.  

> [!NOTE]  
>  Como esta sequência de tarefas não é linear, existem condições nas etapas que podem afetar os resultados da sequência de tarefas, dependendo se ela atualizar o computador cliente com êxito ou se tiver de reverter o computador cliente para a versão do sistema operacional original.  

## <a name="optional-rollback-task-sequence-steps"></a>Etapas de sequência de tarefas de reversão opcional  
 Quando algo der errado com o processo de upgrade depois que o computador for reiniciado, a Instalação do Windows reverterá o upgrade para o sistema operacional anterior. Em seguida, a sequência de tarefas continuará com as etapas no grupo de Reversão. Depois de criar a sequência de tarefas, você pode adicionar etapas opcionais para o grupo de reversão.  

## <a name="folder-and-files-removed-after-computer-restart"></a>Pasta e arquivos removidos após o computador reiniciar  
 Quando a sequência de tarefas é concluída, o cliente não remove os scripts pós-processamento e de reversão até que o computador seja reiniciado. Esses arquivos de script não contêm informações confidenciais.  
