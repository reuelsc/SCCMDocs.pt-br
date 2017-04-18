---
title: "Criar uma sequência de tarefas para atualizar um sistema operacional | Microsoft Docs"
description: "Sequências de tarefas no System Center Configuration Manager podem atualizar automaticamente um sistema operacional do Windows 7 ou posterior para o Windows 10."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: 12
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: d7b13f3dea5a3ae413ca6b8150ec24e1632a4d4d
ms.openlocfilehash: e63b639836bc38a030a051e80db4b057ab75a0b0
ms.lasthandoff: 04/12/2017


---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>Crie uma sequência de tarefas para atualizar um sistema operacional no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use sequências de tarefas no System Center Configuration Manager para atualizar automaticamente um sistema operacional do Windows 7 ou posterior para o Windows 10 em um computador de destino. Você cria uma sequência de tarefas que faz referência à imagem do sistema operacional que você deseja instalar no computador de destino e qualquer outro conteúdo adicional, como aplicativos ou atualizações de software que você deseja instalar. A sequência de tarefas para atualizar um sistema operacional faz parte do cenário [Atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md).  

##  <a name="BKMK_UpgradeOS"></a> Criar uma sequência de tarefas para atualizar um sistema operacional  
 Para atualizar o sistema operacional em computadores para o Windows 10, você pode criar uma sequência de tarefas e selecionar a opção **Atualizar um sistema operacional do pacote de atualização** no assistente Criar Sequência de Tarefas. O assistente adicionará as etapas para atualizar o sistema operacional, aplicar atualizações de software e instalar aplicativos. Antes de criar a sequência de tarefas, o seguinte deve estar disponível:  

-   **Necessária**  

     - O [pacote de atualização do sistema operacional](../get-started/manage-operating-system-upgrade-packages.md) do Windows 10 deve estar disponível no console do Configuration Manager.  

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

    -   **Chave do produto (Product Key)**: especifique a chave do produto (Product Key) do sistema operacional Windows que será instalada. Você pode especificar as chaves de licença de volume codificadas e as chaves do produto padrão. Se você usar uma chave de produto sem codificação, cada grupo de 5 caracteres deverá ser separado por um traço (-). Por exemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Quando a atualização é para uma edição de licença de volume, a chave do produto não é necessária. Você só precisa de uma chave do produto quando a atualização é para uma edição de varejo do Windows.  

7.  Na página **Incluir Atualizações** , especifique se deseja instalar as atualizações de software necessárias, todas as atualizações ou nenhuma e clique em **Próximo**. Se optar pela instalação das atualizações de software, o Configuration Manager instalará somente aquelas que fizerem parte das coleções das quais o computador de destino é membro.  

8.  Na página **Instalar Aplicativos** , especifique os aplicativos a instalar no computador de destino e clique em **Próximo**. Se você especificar vários aplicativos, será possível também definir a continuação da sequência de tarefas em caso de falha na instalação de algum aplicativo.  

9. Conclua o assistente.  



## <a name="configure-pre-cache-content"></a>Configurar o conteúdo de armazenamento prévio em cache
A partir da versão 1702, para implantações disponíveis de sequências de tarefas, é possível optar por usar o recurso de armazenamento prévio em cache para que os clientes baixem apenas o conteúdo relevante antes de um usuário instalá-lo.
> [!TIP]  
> Apresentado com a versão 1702, o pré-cache é um recurso de pré-lançamento. Para habilitá-lo, confira [Use pre-release features from updates](/sccm/core/servers/manage/pre-release-features) (Usar recursos de pré-lançamento de atualizações).

Por exemplo, digamos que você deseja implantar uma sequência de tarefas de atualização in-loco do Windows 10, deseja apenas uma sequência de tarefas para todos os usuários e tem várias arquiteturas e/ou idiomas. Antes da versão 1702, se você criar uma implantação disponível e, em seguida, o usuário clicar em **Instalar** no Centro de Software, o conteúdo será baixado neste momento. Isso acrescenta um tempo antes que a instalação esteja pronta para iniciar. Além disso, todo o conteúdo referenciado na sequência de tarefas é baixado. Isso inclui o pacote de atualização do sistema operacional para todas as arquiteturas e idiomas. Se cada um tiver aproximadamente 3 GB de tamanho, o pacote de download poderá ser bastante grande.

O conteúdo de armazenamento prévio em cache oferece a opção de permitir que o cliente baixe apenas o conteúdo aplicável assim que receber a implantação. Portanto, quando o usuário clicar em **Instalar** no Centro de Software, o conteúdo estará pronto e a instalação iniciará rapidamente, pois o conteúdo está no disco rígido local.

### <a name="to-configure-the-pre-cache-feature"></a>Para configurar o recurso de armazenamento prévio em cache

1. Crie pacotes de atualização de sistema operacional para arquiteturas e idiomas específicos. Especifique a arquitetura e o idioma na guia **Fonte de Dados** do pacote. Para o idioma, use a conversão decimal (por exemplo, 1033 é o decimal para inglês e 0x0409 é o equivalente hexadecimal). Para ver mais detalhes, veja [Criar uma sequência de tarefas para atualizar um sistema operacional](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).

    Os valores de arquitetura e idioma são usados para corresponder condições de etapa de sequência de tarefas que você criará na próxima etapa para determinar se o pacote de atualização do sistema operacional deve ser previamente armazenado em cache.
2. Crie uma sequência de tarefas com etapas condicionais para diferentes idiomas e arquiteturas. Por exemplo, para a versão em inglês, você pode criar uma etapa com o seguinte:

    ![Propriedades de armazenamento prévio em cache](../media/precacheproperties2.png)

    ![Opções de armazenamento prévio em cache](../media/precacheoptions2.png)  

3. Implantar a sequência de tarefas. Para o recurso de armazenamento prévio em cache, configure o seguinte:
    - Na guia **Geral**, selecione **Conteúdo previamente baixado para esta sequência de tarefas**.
    - Na guia **Configurações de implantação**, configure a sequência de tarefas com **Disponível** para **Finalidade**. Se você criar uma implantação **Obrigatória**, a funcionalidade de armazenamento prévio em cache não funcionará.
    - Na guia **Agendamento**, para a configuração **Agendar quando essa implantação estará disponível**, escolha uma hora futura que conceda aos clientes tempo suficiente para armazenar previamente em cache o conteúdo para a implantação disponibilizada para os usuários. Por exemplo, você pode definir o tempo disponível para 3 horas no futuro para oferecer tempo suficiente para o conteúdo ser previamente armazenado em cache.  
    - Na guia **Pontos de Distribuição**, defina as configurações **Opções de implantação**. Se o conteúdo não tiver sido armazenado previamente em cache em um cliente antes de um usuário iniciar a instalação, essas configurações serão usadas.


### <a name="user-experience"></a>Experiência do usuário
- Quando o cliente receber a política de implantação, ele começará a armazenar previamente o conteúdo em cache. Isso inclui todo o conteúdo referenciado (todos os demais tipos de pacote) e somente o pacote atualização do sistema operacional que corresponder ao cliente, com base nas condições que você definir na sequência de tarefas.
- Quando a implantação for disponibilizada para os usuários (a configuração na guia **Agendamento** da implantação), uma notificação será exibida para informar os usuários sobre a nova implantação e ela ficará visível no Centro de Software. O usuário poderá acessar o Centro de Software e clicar em **Instalar** para iniciar a instalação.
- Se o conteúdo não tiver sido armazenado previamente em cache em sua totalidade, ele usará as configurações especificadas na guia **Opções de Implantação** da implantação. É recomendável que haja tempo suficiente desde que a implantação é criada até o momento em que ela se fica disponível para os usuários, a fim de conceder aos clientes tempo suficiente para armazenar previamente o conteúdo em cache.



## <a name="download-package-content-task-sequence-step"></a>Baixar etapa de sequência de tarefas do conteúdo do pacote  
 A etapa [Baixar Conteúdo do Pacote](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) pode ser usada antes da etapa **Atualizar o Sistema Operacional** nos seguintes cenários:  

-   Use uma sequência de tarefas de atualização única que possa funcionar com plataformas x86 e x64. Para fazer isso, inclua duas etapas **Baixar Conteúdo do Pacote** no grupo **Preparar para Atualização** com condições para detectar a arquitetura do cliente e baixar apenas o Pacote de atualização do sistema operacional apropriado. Configure cada etapa **Baixar Conteúdo do Pacote** para usar a mesma variável e use a variável para o caminho de mídia na etapa **Atualizar Sistema Operacional** .  

-   Para baixar um pacote de drivers aplicáveis dinamicamente, use duas etapas **Baixar Conteúdo do Pacote** com condições para detectar o tipo de hardware apropriado para cada pacote de drivers. Configure cada etapa **Baixar Conteúdo do Pacote** para usar a mesma variável e use a variável para o valor **Conteúdo de Teste** na seção de drivers da etapa **Atualizar Sistema Operacional** .  

   > [!NOTE]
   > Quando há mais de um pacote, o Configuration Manager adiciona um sufixo numérico ao nome da variável. Por exemplo, se você especificar uma variável de %mycontent% como uma variável personalizada, essa será a raiz de onde todo o conteúdo referenciado está armazenado (que podem ser vários pacotes). Quando você faz referência à variável em uma etapa posterior, como Atualizar Sistema Operacional, ele é usado com um sufixo numérico. Neste exemplo, %mycontent01% ou %mycontent02%, em que o número corresponde à ordem na qual o pacote está listado nesta etapa.

## <a name="optional-post-processing-task-sequence-steps"></a>Etapas opcionais de sequência de tarefas de pós-processamento  
 Depois de criar a sequência de tarefas, você pode configurar edições adicionais como etapas para desinstalar aplicativos com problemas de compatibilidade conhecidos ou adicionar ações de pós-processamento para execução depois que o computador for reiniciado e a atualização do Windows 10 for bem-sucedida. Adicione estas etapas adicionais no grupo de pós-processamento da sequência de tarefas.  

> [!NOTE]  
>  Como esta sequência de tarefas não é linear, existem condições nas etapas que podem afetar os resultados da sequência de tarefas, dependendo se ela atualizar o computador cliente com êxito ou se tiver de reverter o computador cliente para a versão do sistema operacional original.  

## <a name="optional-rollback-task-sequence-steps"></a>Etapas de sequência de tarefas de reversão opcional  
 Quando algo dá errado com o processo de atualização depois que o computador for reiniciado, a instalação vai reverter a atualização para o sistema operacional anterior e a sequência de tarefas continuará com as etapas no grupo de reversão. Depois de criar a sequência de tarefas, você pode adicionar etapas opcionais para o grupo de reversão.  

## <a name="folder-and-files-removed-after-computer-restart"></a>Pasta e arquivos removidos após o computador reiniciar  
 Quando a sequência de tarefas para atualizar um sistema operacional para Windows 10 e todas as outras etapas da sequência de tarefas forem concluídas, os scripts de pós-processamento e reversão não são removidos quando o computador for reiniciado.  Esses arquivos de script não contêm informações confidenciais.  

