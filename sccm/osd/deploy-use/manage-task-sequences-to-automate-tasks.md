---
title: "Gerenciar sequências de tarefas para automatizar tarefas | Microsoft Docs"
description: "É possível criar, editar, implantar, importar e exportar as sequências de tarefas para gerenciá-las em seu ambiente do System Center Configuration Manager."
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
caps.latest.revision: "10"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: c9d94ffb61ed7a7fa40a01eedc763a16a8df30cb
ms.sourcegitcommit: 31c670a4bce74fd64a7d46ebf7702f65b80d4147
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2017
---
# <a name="manage-task-sequences-to-automate-tasks-in-system-center-configuration-manager"></a>Gerenciar sequências de tarefas para automatizar tarefas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as sequências de tarefas para automatizar etapas no seu ambiente do System Center Configuration Manager. Essas etapas podem implantar uma imagem do sistema operacional em um computador de destino, compilar e capturar uma imagem do sistema operacional de um conjunto de arquivos de instalação do sistema operacional, além de capturar e restaurar as informações de estado do usuário. As sequências de tarefas estão localizadas no console do Configuration Manager na **Biblioteca de Software** > **Sistemas Operacionais** > **Sequência de Tarefas**. O nó **Sequência de Tarefas**, incluindo as subpastas criadas, é replicado em toda a hierarquia do Configuration Manager. Para obter informações sobre planejamento, consulte [Planning considerations for automating tasks (Considerações de planejamento para automatizar tarefas)](../plan-design/planning-considerations-for-automating-tasks.md).  

 Use as seções a seguir para gerenciar as sequências de tarefas.

##  <a name="BKMK_CreateTaskSequence"></a> Criar sequências de tarefas  
 Crie sequências de tarefas usando o Assistente para Criar Sequência de Tarefas. Este assistente pode criar os seguintes tipos de sequências de tarefas:  

|Tipo de sequência de tarefas|Mais informações|  
|------------------------|----------------------|  
|[Sequência de tarefas para instalar um sistema operacional](create-a-task-sequence-to-install-an-operating-system.md)|Esse tipo de sequência de tarefas cria as etapas para instalar um sistema operacional, bem como a opção para migrar dados do usuário, incluir atualizações de software e instalar aplicativos.|  
|[Sequência de tarefas para atualizar um sistema operacional](create-a-task-sequence-to-upgrade-an-operating-system.md)|Esse tipo de sequência de tarefas cria as etapas para atualizar um sistema operacional, bem como a opção para incluir atualizações de software e instalar aplicativos.|  
|[Sequência de tarefas para capturar um sistema operacional](create-a-task-sequence-to-capture-an-operating-system.md)|Esse tipo de sequência de tarefas cria as etapas para compilar e capturar um sistema operacional de um computador de referência. É possível incluir atualizações de software e instalar aplicativos no computador de referência antes que a imagem seja capturada.|  
|[Sequência de tarefas para capturar e restaurar o estado do usuário](create-a-task-sequence-to-capture-and-restore-user-state.md)|Essa sequência de tarefas fornece as etapas a serem adicionadas a uma sequência de tarefas existente para capturar e restaurar dados de estado do usuário.|  
|[Sequência de tarefas para gerenciar discos rígidos virtuais](use-a-task-sequence-to-manage-virtual-hard-disks.md)|Esse tipo de sequência de tarefas contém as etapas para criar um VHD, que inclui instalar um sistema operacional e aplicativos, que podem ser publicados no System Center VMM (Virtual Machine Manager) por meio do console do Configuration Manager.|  
|[Sequência de tarefas personalizada](create-a-custom-task-sequence.md)|Esse tipo de sequência de tarefas não adiciona etapas à sequência de tarefas. É necessário editar a sequência de tarefas e adicionar etapas a ela após sua criação.|  

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Retornar à página anterior quando uma sequência de tarefas falhar
A partir do Configuration Manager versão 1702, você pode retornar à página anterior ao executar uma sequência de tarefas e ocorrer uma falha. Antes dessa versão, era necessário reiniciar a sequência de tarefas ao ocorrer uma falha. Por exemplo, você pode usar o botão **Anterior** nos seguintes cenários:

- Quando um computador é iniciado no Windows PE, a caixa de diálogo de inicialização da sequência de tarefas pode ser exibida antes da sequência estar disponível. Ao clicar em Avançar nesse cenário, a página final da sequência de tarefas exibe uma mensagem informando que não há sequências de tarefas disponíveis. Agora, você pode clicar em **Anterior** para pesquisar novamente por sequências de tarefas disponíveis. Você pode repetir esse processo até que a sequência de tarefas esteja disponível.
- Quando você executa uma sequência de tarefas, porém pacotes dependentes de conteúdo ainda não estão disponíveis nos pontos de distribuição, a sequência de tarefas falhará. Agora, você poderá distribuir o conteúdo ausente (se ainda não tiver sido distribuído) ou aguardar o conteúdo estar disponível nos pontos de distribuição e, em seguida, clicar em **Anterior** para que a pesquisa de sequência de tarefas pesquise novamente o conteúdo.

##  <a name="BKMK_ModifyTaskSequence"></a> Editar uma sequência de tarefas  
 Você pode modificar uma sequência de tarefas adicionando ou removendo etapas de sequência de tarefas e grupos de sequência de tarefas, ou alterando a ordem das etapas. Use o procedimento a seguir para modificar uma sequência de tarefas existente.  

> [!IMPORTANT]  
>  Ao editar uma sequência de tarefas criada com o Assistente para Criar Sequência de Tarefas, o nome da etapa pode ser a ação ou o tipo da etapa. Por exemplo, talvez você veja uma etapa com o nome “Particionar Disco 0”, que corresponde à ação de uma etapa do tipo [Format and Partition Disk (Formatar e Particionar Disco)](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk). Todas as etapas da sequência de tarefas são documentadas por seu tipo e não necessariamente pelo nome da etapa exibida no Editor.  

#### <a name="to-edit-a-task-sequence"></a>Para editar uma sequência de tarefas  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas a editar.  

4.  Na guia **Início** , no grupo **Sequência de Tarefas** , clique em **Editar**e, então, execute uma das seguintes operações:  

    -   Para adicionar uma etapa de sequência de tarefas, clique em **Adicionar**, selecione o tipo da etapa e clique na etapa de sequência de tarefas que deseja adicionar. Por exemplo, para adicionar a etapa Executar linha de comando, clique em **Adicionar**, selecione **Geral**e clique em **Executar Linha de Comando**.  

         Para ver a lista de todas as etapas de sequência de tarefas com seu tipo, consulte a tabela que segue esse procedimento.  

    -   Para adicionar um grupo à sequência de tarefas, clique em **Adicionar**e, em seguida, em **Novo Grupo**. Concluída a adição do grupo, você pode adicionar etapas a ele.  

    -   Para alterar a ordem de etapas e grupos na sequência de tarefas, selecione a etapa ou o grupo a reordenar e, em seguida, use os ícones **Mover Item para Cima** ou **Mover Item para Baixo** . Você pode mover apenas uma etapa ou grupo por vez.  

    -   Para remover uma etapa ou um grupo, selecione a etapa ou o grupo e clique em **Remover**.  

5.  Clique em **OK** para salvar as alterações.  

 Para obter uma lista das etapas de sequência de tarefas disponíveis, consulte [Task sequence steps (Etapas da sequência de tarefas)](../understand/task-sequence-steps.md).  

## <a name="configure-software-center-properties"></a>Configurar as propriedades do Centro de Software
Use o procedimento a seguir para configurar os detalhes da sequência de tarefas exibida no Centro de Software. Esses detalhes são apenas para fins informativos.  
1. No console do Configuration Manager, acesse **Biblioteca de Software** > **Sistemas Operacionais** > **Sequências de Tarefas**.
2. Selecione a sequência de tarefas a ser editada e clique em **Propriedades**.
3. Na guia **Geral**, as seguintes configurações do Centro de Software estão disponíveis:
  - **Reinicialização Necessária**: permite que o usuário saiba se uma reinicialização é necessária durante a instalação.
  - **Tamanho do download (MB)**: especifica quantos megabytes são exibidos no Centro de Software para a sequência de tarefas.  
  - **Tempo de execução estimado (minutos)**: especifica o tempo de execução estimado em minutos exibido no Centro de Software para a sequência de tarefas.

## <a name="configure-advanced-task-sequence-settings"></a>Definir as configurações da sequência de tarefas avançadas
Use o procedimento a seguir para configurar os detalhes da sequência de tarefas exibida no Centro de Software. Esses detalhes são apenas para fins informativos.  
1. No console do Configuration Manager, acesse **Biblioteca de Software** > **Sistemas Operacionais** > **Sequências de Tarefas**.
2. Selecione a sequência de tarefas a ser editada e clique em **Propriedades**.
3. Na guia **Avançado**, as seguintes configurações estão disponíveis:

    - **Executar outro programa primeiro**    
    Marque esta caixa de seleção para executar outro programa (em outro pacote) antes da sequência de tarefas ser executada. Por padrão, essa caixa de seleção está desmarcada. O programa que você especificar para executar primeiro não precisa ser anunciado separadamente.

        > [!IMPORTANT]     
        Esta configuração aplica-se apenas às sequências de tarefas que são executadas no sistema operacional completo. O Configuration Manager ignorará esta configuração se a sequência de tarefas for iniciada usando o PXE ou a mídia de inicialização.

    - **Pacote**     
        Quando você seleciona **Executar outro programa primeiro**, digite ou navegue para o pacote que contém o programa que deve ser executado antes dessa sequência de tarefas.

    - **Programa**     
    Quando você seleciona **Executar outro programa primeiro**, selecione o programa que deve ser executado antes dessa sequência de tarefas na lista suspensa **Programa**.

        > [!NOTE]    
        > Se o programa selecionado não for executado em um cliente, a sequência de tarefas não será executada. Se o programa selecionado for executado com êxito, ele não será executado novamente, mesmo se a sequência de tarefas for executada novamente no mesmo cliente.
 
    - **Desabilitar esta sequência de tarefas nos computadores onde está implantada**    
    Se você selecionar essa opção, todas as implantações que contêm essa sequência de tarefas serão temporariamente desabilitadas. A sequência de tarefas é removida da lista de anúncios disponíveis para execução e não será executada até que ela tenha sido habilitada novamente. Por padrão, esta opção está desmarcada.

    - **Tempo de execução máximo permitido**    
    Especifica o tempo máximo (em minutos) que é esperado para executar a sequência de tarefas no computador de destino. Você deve usar um número inteiro igual ou maior que zero. Por padrão, esse valor é definido como 120 minutos.

        > [!IMPORTANT]    
        > Se você estiver usando janelas de manutenção para a coleção em que essa sequência de tarefas é executada, poderá ocorrer um conflito se o **Tempo de execução máximo permitido** for maior do que o tempo da janela de manutenção agendada. Se o tempo de execução máximo for definido como **0**, a sequência de tarefas será iniciada durante a janela de manutenção e continuará sendo executado até que seja concluído ou que ocorra uma falha após a janela de manutenção ser fechada. Como resultado, as sequências de tarefas com um tempo de execução máximo definido como **0** pode ser executado após o término de suas janelas de manutenção. Se você definir o tempo de execução máximo para um período específico (ou seja, não definido como **0**) que exceda a duração de qualquer janela de manutenção disponível, essa sequência de tarefas não será executada. Para obter mais informações, consulte [Como usar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).
 
        Se o valor for definido como **0**, o Configuration Manager avaliará o tempo de execução máximo permitido para **12** horas (720 minutos) para monitoramento do progresso. No entanto, a sequência de tarefas será iniciada, desde que a duração da contagem regressiva não exceda o valor da janela de manutenção.

    > [!NOTE]    
    > Se o tempo de execução máximo for atingido, o Configuration Manager interromperá a sequência de tarefas se ela estiver definida para ser executada com direitos administrativos e a configuração para permitir que os usuários interajam com esse programa não estiver selecionada. Se a sequência de tarefas não for interrompida, o Configuration Manager parará de monitorar a sequência de tarefas após o tempo de execução máximo permitido ser atingido. 

    - **Usar uma imagem de inicialização**   
        Habilite esta opção para usar a imagem de inicialização selecionada quando a sequência de tarefas for executada. 

        Clique em **Procurar** para selecionar uma imagem de inicialização diferente. Desmarque esta opção para desabilitar o uso da imagem de inicialização selecionada quando a sequência de tarefas for executada.

    - **Essa sequência de tarefas pode ser executada em qualquer plataforma**     
        Se você selecionar essa opção, o Configuration Manager não verificará o tipo de plataforma do computador de destino quando a sequência de tarefas for implantada. Essa opção é habilitada por padrão.

    - **Essa sequência de tarefas pode ser executada somente nas plataformas clientes especificadas**    
        Esta opção especifica os processadores, os sistemas operacionais e os service packs em que essa sequência de tarefas pode ser executada. Quando você seleciona essa opção, pelo menos uma plataforma também deve ser selecionada na lista. Por padrão, nenhuma plataforma é selecionada. O Configuration Manager usa essas informações quando avalia quais computadores de destino em uma coleção recebem a sequência de tarefas implantada.

        > [!NOTE]    
        > Quando uma sequência de tarefas é executada da mídia de inicialização ou pela inicialização de PXE, essa opção é ignorada e a sequência de tarefas é executada como se a opção **Este programa pode ser executado em qualquer plataforma** estiver selecionada.

## <a name="configure-high-impact-task-sequence-settings"></a>Definir configurações da sequência de tarefas de alto impacto
A partir do Configuration Manager versão 1702, você pode definir uma sequência de tarefas como alto impacto e personalizar as mensagens recebidas pelos usuários quando eles executam a sequência de tarefas.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Definir uma sequência de tarefas como uma sequência de tarefas de alto impacto
Use o procedimento a seguir para definir uma sequência de tarefas como de alto impacto.
> [!NOTE]    
> Qualquer sequência de tarefas que atender a determinadas condições será automaticamente definida como de alto impacto. Para obter detalhes, consulte [Gerenciar implantações de alto risco](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. No console do Configuration Manager, acesse **Biblioteca de Software** > **Sistemas Operacionais** > **Sequências de Tarefas**.
2. Selecione a sequência de tarefas a ser editada e clique em **Propriedades**.
3. Na guia **Notificação do Usuário**, selecione **Essa é uma sequência de tarefas de alto impacto**.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Criar uma notificação personalizada para implantações de alto risco
Use o procedimento a seguir para criar uma notificação personalizada para implantações de alto impacto.
1. No console do Configuration Manager, acesse **Biblioteca de Software** > **Sistemas Operacionais** > **Sequências de Tarefas**.
2. Selecione a sequência de tarefas a ser editada e clique em **Propriedades**.
3. Na guia **Notificação do Usuário**, selecione **Usar texto personalizado**.
>  [!NOTE]    
>  É possível definir o texto de notificação do usuário apenas quando **Essa é uma sequência de tarefas de alto impacto** está selecionado.

4. Defina as seguintes configurações (máximo de 255 caracteres para cada caixa de texto):

  **Texto do título da notificação do usuário**: especifica o texto azul exibido na notificação do usuário do Centro de Software. Por exemplo, na notificação do usuário padrão, esta seção contém algo como "Confirmar que você deseja atualizar o sistema operacional neste computador".

  **Texto da mensagem da notificação do usuário**: há três caixas de texto que fornecem o corpo da notificação personalizada. Todas as caixas de texto exigem que você adicione texto.
  - 1º de caixa de texto: especifica o corpo do texto principal, geralmente contendo instruções para o usuário. Por exemplo, na notificação de usuário padrão, esta seção contém algo como "Atualizar o sistema operacional levará tempo e o computador poderá ser reiniciado várias vezes".
  - 2ª caixa de texto: especifica o texto em negrito abaixo do corpo do texto principal. Por exemplo, na notificação de usuário padrão, esta seção contém algo como “Essa atualização in-loco instala o novo sistema operacional e migra automaticamente seus aplicativos, dados e configurações”.
  - 3ª caixa de texto: especifica a última linha de texto sob o texto em negrito. Por exemplo, na notificação do usuário padrão, essa seção contém algo como “Clique em Instalar para começar. Caso contrário, clique em Cancelar”.   
    
Digamos que você defina a seguinte notificação personalizada nas propriedades.

![Notificação personalizado para uma sequência de tarefas](..\media\user-notification.png)

A mensagem de notificação a seguir será exibida quando o usuário final abrir a instalação do Centro de Software.

![Notificação personalizado para uma sequência de tarefas](..\media\user-notification-enduser.png)


##  <a name="BKMK_DistributeTS"></a> Distribuir o conteúdo referenciado por uma sequência de tarefas  
 Para os clientes executarem uma sequência de tarefas que faz referência ao conteúdo, distribua esse conteúdo para pontos de distribuição. A qualquer momento você pode selecionar uma sequência de tarefas e distribuir seu conteúdo para criar uma nova lista de pacotes de referência para distribuição. Se você fizer alterações à sequência de tarefas com o conteúdo atualizado, será necessário redistribuí-lo antes de disponibilizá-lo para os clientes. Use o procedimento a seguir para distribuir o conteúdo que é referenciado por uma sequência de tarefas.  

#### <a name="to-distribute-referenced-content-to-distribution-points"></a>Para distribuir o conteúdo referenciado para pontos de distribuição  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas a distribuir.  

4.  Na guia **Início** , no grupo **Implantação** , clique em **Distribuir Conteúdo** para iniciar o Assistente para Distribuir Conteúdo.  

5.  Na página **Geral** , verifique se a sequência de tarefas correta está selecionada para distribuição e, em seguida, clique em **Próximo**.  

6.  Na página **Conteúdo** , verifique o conteúdo a distribuir, como, por exemplo, a imagem de inicialização referenciada pela sequência de tarefas, e, em seguida, clique em **Próximo**.  

7.  Na página **Destino de Conteúdo** , especifique as coleções, o ponto de distribuição ou o grupo de pontos de destino onde deseja distribuir os conteúdos de sequência de tarefas e, em seguida, clique em **Próximo**.  

    > [!IMPORTANT]  
    >  Se a sequência de tarefas que você selecionou faz referência ao conteúdo já distribuído a um ponto de distribuição específico, esse ponto não é listado pelo assistente.  

8.  Conclua o assistente.  

 É possível pré-configurar o conteúdo referenciado na sequência de tarefas. O Configuration Manager cria um arquivo de conteúdo compactado e pré-configurado que contém os arquivos, as dependências associadas e os metadados associados para o conteúdo selecionado. Você pode importar manualmente o conteúdo em um servidor de site, site secundário ou ponto de distribuição. Para obter mais informações sobre como pré-configurar arquivos de conteúdo, consulte [Prestage content (Pré-configurar conteúdo)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

##  <a name="BKMK_DeployTS"></a> Implantar uma sequência de tarefas  
 Use o procedimento a seguir para implantar uma sequência de tarefas para computadores em uma coleção.  

> [!WARNING]  
>  Você pode gerenciar o comportamento de implantações de sequência de tarefas de alto risco. Uma implantação de alto risco é uma implantação que é instalada automaticamente e que tem o potencial de causar resultados indesejados. Por exemplo, uma sequência de tarefas que tem a finalidade de **Obrigatória** e que implanta um sistema operacional é considerada uma implantação de alto risco. Para obter mais informações, consulte [Configurações para gerenciar implantações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

> [!NOTE]  
>  As mensagens de status para a implantação de sequência de tarefas são exibidas na janela de mensagem no site primário, mas não são exibidas no site de administração central.  

#### <a name="to-deploy-a-task-sequence"></a>Para implantar uma sequência de tarefas  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas a implantar.  

4.  Na guia **Início** , no grupo **Implantação** , clique em **Implantar**.  

    > [!NOTE]  
    >  Se **Implantar** não estiver disponível, a sequência de tarefas terá uma referência que não será válida.  Corrija a referência e, em seguida, tente implantar a sequência de tarefas novamente.  

5.  Na página **Geral** , especifique as seguintes informações e clique em **Próximo**.  

    -   **Sequência de tarefas**: especifique a sequência de tarefas que deseja implantar. Por padrão, esta caixa exibe a sequência de tarefas que você selecionou.  

    -   **Coleção**: especifique a coleção que contém os computadores que executarão a sequência de tarefas.  

         Não implante sequências de tarefas que instalam sistemas operacionais em coleção inadequadas, como, por exemplo, a coleção **Todos os Sistemas** . É importante selecionar a coleção que contém somente os computadores que você deseja que executem a sequência de tarefas.  

        > [!NOTE]  
        >  Ao executar uma implantação de alto risco, como um sistema operacional, a janela **Selecionar Coleção** exibe somente as coleções personalizadas que atendem às configurações de verificação de implantação definidas nas propriedades do site. As implantações de alto risco sempre estão limitadas às coleções personalizadas criadas e à coleção interna de **Computadores desconhecidos** . Ao criar uma implantação de alto risco, não é possível selecionar uma coleção interna como **Todos os Sistemas**. Desmarque **Ocultar coleções com uma contagem de membros maior que a configuração de tamanho mínimo do site** para ver todas as coleções personalizadas que contêm menos clientes do que o tamanho máximo configurado. Para obter mais informações, consulte [Configurações para gerenciar implantações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md).  
        >   
        >  As configurações de verificação de implantação baseiam-se na associação atual da coleção. Depois de implantar a sequência de tarefas, a associação à coleção não será reavaliada quanto às configurações de implantação de alto risco.  
        >   
        >  Por exemplo, suponhamos que você defina **Tamanho padrão** como 100 e o **Tamanho máximo** como 1000. Ao criar uma implantação de alto risco, a janela **Selecionar coleção** exibirá somente as coleções que contêm menos de 100 clientes. Se você desmarcar a definição **Ocultar coleções com uma contagem de membro maior que a configuração de tamanho mínimo do site**, a janela exibirá coleções que contêm menos de 1000 clientes.  
        >   
        >  Ao selecionar uma coleção que contém uma função de site, o seguinte se aplica:  
        >   
        >  -   Se a coleção contiver um servidor do sistema de sites e nas configurações de verificação de implantação você configurar para coleções de bloco com servidores do sistema de sites, ocorrerá um erro e não será possível continuar.  
        > -   Se a coleção contiver um servidor do sistema de sites e nas configurações de verificação de implantação for configurada a opção para avisar se as coleções que têm servidores do sistema de sites, se a coleção exceder o valor do tamanho padrão ou se a coleção contiver um servidor, o Assistente de Implantação de Software exibirá um aviso de alto risco. Você deve concordar em criar uma implantação de alto risco e uma mensagem de status de auditoria é criada.  

    -   **Comentários (opcional)**: especifique informações adicionais que descrevem essa implantação da sequência de tarefas.  

6.  Na página **Configurações de Implantação** , especifique as seguintes informações e clique em **Próximo**.  

    -   **Finalidade**: na lista suspensa, escolha uma das seguintes opções:  

        -   **Disponível**: se a sequência de tarefas for implantada em um usuário, ele verá a sequência de tarefas publicada no Catálogo de Aplicativos e poderá solicitá-la sob demanda. Se ela for implantada a um dispositivo, o usuário a visualizará no Centro de Software e poderá instalá-la por demanda.  

        -   **Necessária**: a sequência de tarefas é implantada automaticamente, de acordo com o agendamento configurado. No entanto, o usuário poderá acompanhar o status da implantação da sequência de tarefas (se não estiver oculto) e instalar a sequência de tarefas antes da data limite usando o Centro de Software.  

    -   **Implantar automaticamente, de acordo com o agendamento, com ou sem um usuário conectado**: essa opção não está disponível quando uma sequência de tarefas é implantada.  

    -   **Enviar pacotes de ativação**: se a finalidade da implantação estiver definida como **Necessária** e essa opção estiver selecionada, um pacote de ativação será enviado aos computadores antes que a implantação seja instalada para ativar o computador do modo de suspensão na hora do prazo da instalação. Para usar essa opção, os computadores e as redes devem ser configurados para Wake on LAN.  

    -   **Permitir que os clientes em uma conexão de Internet limitada baixem conteúdo após o prazo de instalação, o que pode incorrer em custos adicionais**: quando você tem uma sequência de tarefas que instala um aplicativo, mas que não implanta um sistema operacional, é possível especificar se deseja permitir que os clientes baixem conteúdo após o prazo de instalação quando estiverem usando conexões de Internet limitadas. Provedores de Internet ocasionalmente cobram por quantidade de dados que você envia e recebe quando está em uma conexão de Internet limitada.  

        > [!NOTE]  
        >  Enquanto estiver em uso, uma conexão de Internet limitada pode funcionar para sequências de tarefas que não implantar um sistema operacional, pois não há suporte.  

    -   **Exigir aprovação do administrador se os usuários solicitarem este aplicativo**: essa opção não está disponível quando você implanta uma sequência de tarefas.  

    -   **Tornar disponível para o seguinte**: especifique se a sequência de tarefas está disponível para clientes do Configuration Manager, mídia ou PXE.  

        > [!IMPORTANT]  
        >  Use a configuração **Somente mídia e PXE (oculto)** para implantações automatizadas de sequência de tarefas. Selecione **Permitir implantação autônoma do sistema operacional** e defina a variável SMSTSPreferredAdvertID como parte da mídia para que o computador se inicialize automaticamente para a implantação sem interação do usuário. Para obter mais informações sobre variáveis de sequência de tarefas, consulte [Task sequence built-in variables (Variáveis internas de sequência de tarefas)](../understand/task-sequence-built-in-variables.md)  

7.  Na página **Agendamento** , especifique as informações a seguir e clique em **Próximo**.  

    > [!IMPORTANT]  
    >  Quando um cliente do Windows PE é iniciado pelo PXE ou pela mídia de inicialização, o cliente não avalia agendas de implantação (horas de início, expiração ou prazo). Configure agendas somente em implantações para clientes que iniciam com o sistema operacional Windows completo. Considere usar outros métodos, como janelas de manutenção, para controlar as sequências de tarefas ativas implantadas nos clientes que iniciam por meio do Windows PE.  

    -   **Agendar quando essa implantação estará disponível**: especifique a data e a hora em que a sequência de tarefas estará disponível para ser executada no computador de destino. Quando você marca a caixa de seleção **UTC** , essa configuração garante que a sequência de tarefas está disponível para vários computadores de destino ao mesmo tempo em vez em momentos diferentes, de acordo com a hora local nos computadores de destino.  

         Se a hora de início é anterior à hora exigida, o cliente baixa a sequência de tarefas na hora de início que você especifica.  

    -   **Agendar quando essa implantação expirará**: especifique a data e a hora em que a sequência de tarefas expirará no computador de destino. Quando você marca a caixa de seleção **UTC** , essa configuração garante que a sequência de tarefas expira em vários computadores de destino ao mesmo tempo em vez em momentos diferentes, de acordo com a hora local nos computadores de destino.  

    -   **Agendamento de atribuição**: especifique quando a sequência de tarefas necessária será executada no computador de destino. Você pode adicionar vários agendamentos.  

         Você pode especificar a data e hora de início do agendamento, se a sequência de tarefas é executada de forma semanal, mensal ou em um intervalo personalizado e se a sequência de tarefas é executada após um evento, como logon ou logout do computador.  

        > [!NOTE]  
        >  Se você agendar uma hora de início para uma sequência de tarefas necessária que seja anterior à data e hora em que a sequência de tarefas está disponível, o cliente do Configuration Manager baixará a sequência de tarefas na hora de início agendada, mesmo se ela estiver disponível em um momento anterior.  

    -   **Executar comportamento novamente**: especifique quando a sequência de tarefas será executada novamente. Você pode especificar uma das seguintes opções.  

        -   **Nunca executar novamente o programa implantado**: a sequência de tarefas não será executada novamente no cliente se ela já tiver sido executada anteriormente nele. A sequência de tarefas não é executada novamente mesmo se ela teve falha originalmente ou se os arquivos da sequência de tarefas foram alterados.  

        -   **Sempre executar novamente o programa**: a sequência de tarefas sempre é executada novamente no cliente quando a implantação está agendada, mesmo se a sequência de tarefas foi implantada com êxito anteriormente. Essa configuração é particularmente útil quando você usa implantações recorrentes nas quais a sequência de tarefas é atualizada regularmente.  

            > [!IMPORTANT]  
            >  Embora esta opção esteja definida por padrão, ela não terá efeito até que você atribua uma implantação necessária. As implantações disponíveis sempre podem ser executadas novamente por um usuário.  

        -   **Executar novamente se a tentativa anterior falhar**: a sequência de tarefas é executada novamente quando a implantação é agendada somente se houve falha na execução da sequência de tarefas anteriormente. Essa configuração é particularmente útil para implantações necessárias para que elas tentem ser executadas automaticamente de acordo com o agendamento da atribuição se a última tentativa de execução foi malsucedida.  

        -   Executar novamente se a tentativa anterior tiver êxito: a sequência de tarefas é executada novamente somente se foi executada com êxito no cliente. Essa configuração é útil ao usar implantações recorrentes nas quais a sequência de tarefas é atualizada regularmente, e cada atualização requer que a atualização anterior esteja instalada com êxito.  

        > [!NOTE]  
        >  Como um usuário pode executar novamente um implantação de sequência de tarefas disponível, antes de implantar uma sequência de tarefas disponível em um ambiente de produtos, avalie cuidadosamente e teste o que acontece se um usuário executar novamente a sequência de tarefas várias vezes.  

8.  Na página **Experiência do Usuário** , especifique as seguintes informações e clique em **Próximo**.  

    -   **Permitir que o usuário execute o programa, independentemente das atribuições**: especifique se o usuário tem permissão para executar uma sequência de tarefas necessária, independentemente das atribuições de implantação.  

    -   **Mostrar andamento da sequência de tarefas**: especifique se o cliente do Configuration Manager exibe o andamento da sequência de tarefas.  

    -   **Instalação de software**: especifique se o usuário tem permissão para instalar software fora de uma janela de manutenção configurada após a hora agendada.  

    -   **Reinicialização do sistema (se necessário para conclusão da instalação)**: especifique se o usuário tem permissão para reiniciar o computador após uma instalação de software fora de uma janela de manutenção configurada após a hora de atribuição.  

    -   **Permitir que a sequência de tarefas seja executada para cliente na Internet**: especifique se a sequência de tarefas tem permissão para ser executada em um cliente baseado na Internet que o Configuration Manager detectar na Internet. Não há suporte para operações que instalam o software, como um sistema operacional, com essa configuração. Use esta opção somente para as sequências de tarefas baseadas em script genérico que executam operações no sistema operacional padrão.  

9. Na página **Alertas** , especifique as configurações de alerta que você deseja para esta sequência de tarefas e clique em **Próximo**.  

10. Na página **Pontos de Distribuição** , especifique as seguintes informações e clique em **Próximo**.  

    -   **Opções de implantação**: especifique uma das seguintes opções:  

        > [!NOTE]  
        >  Quando você usa multicast para implantar um sistema operacional, o conteúdo deve ser baixado para os computadores de destino conforme o necessário ou antes da execução da sequência de tarefas.  

        -   Especifique se os clientes baixam o conteúdo do ponto de distribuição para o computador de destino conforme necessário pela sequência de tarefas.  

        -   Especifique se os cliente baixam todo o conteúdo do ponto de distribuição para o computador de destino antes da execução da sequência de tarefas. Essa opção não será mostrada se você tiver especificado que a sequência de tarefas está disponível para implantações de PXE e de mídia de inicialização (consulte a página **Configurações de Implantação** ).  

        -   especifique que os clientes executem o conteúdo do ponto de distribuição. Essa opção está disponível somente quando todos os pacotes associados à sequência de tarefas estão habilitados para usar um compartilhamento de pacotes no ponto de distribuição. Para habilitar o conteúdo a usar um compartilhamento de pacotes, consulte a guia **Acesso a Dados** nas **Propriedades** de cada pacote.  

    -   **Quando não houver nenhum ponto de distribuição local disponível, use um ponto de distribuição remoto**: especifique se os clientes podem usar pontos de distribuição que estão em redes lentas ou não confiáveis para baixar o conteúdo exigido pela sequência de tarefas.  

11. Conclua o assistente.  

##  <a name="BKMK_ExportImport"></a> Exportar e importar sequências de tarefas  
 Você pode exportar e importar sequências de tarefas com ou sem seus objetos relacionados, como uma imagem do sistema operacional, uma imagem de inicialização, um pacote do agente cliente, um pacote de driver e aplicativos que têm dependências.  

 Considere o seguinte ao exportar e importar sequências de tarefas.  

-   Senhas que são armazenadas na sequência de tarefas não são exportadas. Se você exportar e importar uma sequência de tarefas que contenha senhas, deverá editar a sequência de tarefas importada e especificar alguma senha novamente. Certifique-se de especificar senhas para as ações [Ingressar no Domínio ou Grupo de Trabalho](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup), [Conectar à Pasta de Rede](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) e [Executar Linha de Comando](../understand/task-sequence-steps.md#BKMK_RunCommandLine).  

- Ao exportar uma sequência de tarefas com a etapa **Definir Variáveis Dinâmicas**, nenhum valor é exportado para as variáveis definidas com a configuração **Valor secreto**. É necessário inserir os valores novamente para essas variáveis depois de importar a sequência de tarefas.

-   Como prática recomendada, quando você tem vários sites primários, importe as sequências de tarefas no site de administração central.  

 Use os procedimentos a seguir para exportar e importar uma sequência de tarefas.  

#### <a name="to-export-task-sequences"></a>Para exportar as sequências de tarefas  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas a exportar. Se você selecionar mais de uma sequência de tarefas, elas serão armazenadas em um arquivo de exportação.  

4.  Na guia **Início** , no grupo **Sequência de Tarefas** , clique em **Exportar** para iniciar o Assistente para Exportar Sequência de Tarefas.  

5.  Na página **Geral** , especifique as seguintes configurações e clique em **Próximo**.  

    -   Na caixa **Arquivo** , especifique o local e o nome do arquivo de exportação. Se você inserir o nome do arquivo diretamente, inclua a extensão .zip ao nome do arquivo. Se você procurar o arquivo de exportação, o assistente adicionará automaticamente essa extensão de nome de arquivo.  

    -   Desmarque a caixa de seleção **Exportar todas as dependências de sequência de tarefas** se não desejar exportar dependências da sequência de tarefas. Por padrão, o assistente procura todos os objetos relacionados e exporta-os com a sequência de tarefas. Isso inclui quaisquer dependências de aplicativos.  

    -   Desmarque a caixa de seleção **Exportar todo conteúdo das sequências de tarefas e dependências selecionadas** se não desejar copiar o conteúdo da origem do pacote para o local de exportação. Se essa caixa de seleção estiver marcada, o Assistente para Importar Sequência de Tarefas usará o caminho de importação como o novo local da origem do pacote.  

    -   Na caixa **Comentários do administrador** , adicione uma descrição das sequências de tarefas a serem exportadas.  

6.  Conclua o assistente.  

 O assistente cria os seguintes arquivos de saída:  

-   Se você não exportar o conteúdo: um arquivo .zip.  

-   Se você exportar o conteúdo: um arquivo .zip e uma pasta chamada *export*_files, em que *export* é o nome do arquivo .zip que contém o conteúdo exportado.  

 Se você incluir o conteúdo ao exportar uma sequência de tarefas, copie o arquivo .zip e a pasta *export*_files, caso contrário haverá falha na importação.  

#### <a name="to-import-task-sequences"></a>Para importar sequências de tarefas  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Importar Sequência de Tarefas** para iniciar o Assistente para Importar Sequência de Tarefas.  

4.  Na página **Geral** , especifique o arquivo .zip e clique em **Próximo**.  

5.  Na página **Conteúdo do Arquivo** , selecione a ação que você requer para cada objeto que você importar. Essa página mostra todos os objetos que o Configuration Manager importará.  

    -   Se os objeto nunca foi importado, selecione **Criar Novo**.  

    -   Se o objeto foi importado anteriormente, selecione uma das seguintes ações:  

        -   **Ignorar Duplicado** (padrão): essa ação não importa o objeto. Em vez disso, o assistente vincula o objeto existente à sequência de tarefas.  

        -   **Substituir**: essa ação substitui o objeto existente pelo objeto importado. Para aplicativos, você pode adicionar uma revisão para atualizar o aplicativo existente ou criar um novo aplicativo.  

6.  Conclua o assistente.  

 Após importar a sequência de tarefas, edite-a para especificar senhas que estavam na sequência de tarefas original. Por motivos de segurança, as senhas não são exportadas.  

##  <a name="BKMK_CreateTSVariables"></a> Criar variáveis de sequência de tarefas em computadores e coleções  
Você pode definir variáveis de sequência de tarefas personalizadas para computadores e coleções. As variáveis definidas para um computador são chamadas de variáveis de sequência de tarefas por computador. As variáveis definidas para uma coleção são chamadas de variáveis de sequência de tarefas por coleção. Se houver um conflito, as variáveis por computador prevalecerão sobre as variáveis por coleção. Isso significa que as variáveis de sequência de tarefas associadas a um computador específico possuem prioridade sobre variáveis atribuídas à coleção que contém o computador.  

Por exemplo, se a coleção ABC tiver uma variável atribuída a ela e o computador XYZ, que é um membro da coleção ABC, tiver uma variável com o mesmo nome atribuída a ele, a variável atribuída ao computador XYZ terá prioridade sobre a variável atribuída à coleção ABC.  

É possível ocultar as variáveis por computador e por coleção de forma que elas não fiquem visíveis no console do Configuration Manager. Se você não deseja mais que essas variáveis fiquem ocultas, deve excluí-las e redefini-las sem selecionar a opção para ocultá-las. Quando você usa a opção **Não exibir esse valor no console do Configuration Manager**, o valor da variável não é exibido no console, mas pode ainda ser usado pela sequência de tarefas quando for executada.  

> [!WARNING]    
> A configuração **Não exibir esse valor no console do Configuration Manager** aplica-se ao console do Configuration Manager, mas os valores das variáveis ainda são exibidos no arquivo de log da sequência de tarefas (SMSTS.LOG). 

É possível gerenciar variáveis por computador em um site primário ou em um site de administração central. O Configuration Manager não dá suporte a mais de 1.000 variáveis atribuídas para um computador.  

> [!IMPORTANT]  
>  Ao usar variáveis por coleção para sequências de tarefas, considere o seguinte:  
>   
> - Como as alterações nas coleções são sempre replicadas por meio da hierarquia, quaisquer alterações feitas nas variáveis da coleção serão aplicadas não somente aos membros do site atual, mas a todos os membros da coleção, por meio da hierarquia.  
> - Quando você exclui uma coleção, essa ação também exclui as variáveis da sequência de tarefas que estão configuradas para a coleção.  

 Use os procedimentos a seguir para criar variáveis de sequência de tarefas para um computador ou uma coleção.  

#### <a name="to-create-task-sequence-variables-for-a-computer"></a>Para criar variáveis de sequência de tarefas para um computador  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , expanda a coleção que contém o computador ao qual você deseja adicionar a variável.  

3.  Selecione o computador e clique em **Propriedades**.  

4.  Na caixa de seleção **Propriedades** , clique na guia **Variáveis** .  

5.  Para cada variável que desejar criar, clique no ícone **Novo** na caixa de diálogo **<Nova\> Variável** e especifique o nome e o valor da variável de sequência de tarefas. Desmarque a caixa de seleção **Não exibir este valor no console do Configuration Manager** se desejar ocultar as variáveis para que elas não fiquem visíveis no console do Configuration Manager.  

6.  Depois de ter excluído todas as variáveis do computador, clique em **OK**.  

#### <a name="to-create-task-sequence-variables-for-a-collection"></a>Para criar variáveis de sequência de tarefas para uma coleção  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , selecione a coleção na qual deseja adicionar a variável e clique em **Propriedades**.  

3.  Na caixa de seleção **Propriedades** , clique na guia **Variáveis da Coleção** .  

4.  Para cada variável que desejar criar, clique no ícone **Novo** na caixa de diálogo **<Nova\> Variável** e especifique o nome e o valor da variável de sequência de tarefas. Desmarque a caixa de seleção **Não exibir este valor no console do Configuration Manager** se desejar ocultar as variáveis para que elas não fiquem visíveis no console do Configuration Manager.  

5.  Opcionalmente, especifique a prioridade para o Configuration Manager usar quando as variáveis de sequência de tarefas são avaliadas.  

6.  Depois de adicionar todas as variáveis à coleção, clique em **OK**.  

##  <a name="BKMK_AdditionalActionsTS"></a> Ações adicionais para gerenciar sequências de tarefas  
 Você pode gerenciar sequências de tarefas usando ações adicionais ao selecionar uma sequência de tarefas.  

#### <a name="to-select-a-task-sequence-to-manage"></a>Para selecionar uma sequência de tarefas a ser gerenciada  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais** e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas que deseja gerenciar e selecione uma das opções disponíveis.  

 Use a tabela a seguir para obter mais informações sobre algumas das ações adicionais para gerenciar sequências de tarefas.  

|Ação|Descrição|  
|------------|-----------------|  
|**Copiar**|Faz uma cópia da sequência a tarefa selecionada. Você pode achar essa ação útil quando deseja criar uma nova sequência de tarefas baseada em uma sequência de tarefas existente.<br /><br /> Quando você fizer uma cópia de uma sequência de tarefas em uma pasta, a cópia será listada nessa pasta até que você atualize o nó de sequência de tarefas.  Após a atualização, a cópia aparecerá na pasta raiz.|  
|**Desabilitar**|Desativa a sequência de tarefas para que ela não possa ser executada nos computadores. As sequências de tarefas desativadas podem ser implantadas em computadores, mas os computadores não executam a sequência de tarefas até que ela seja habilitada.|  
|**Habilitar**|Habilita a sequência de tarefas, de forma que ela possa ser executada. Não é necessário reimplantar uma sequência de tarefas implantada após ser habilitada.|  
|**Criar Arquivo de Conteúdo de Pré-teste**|Inicia o Assistente para Criar Arquivo de Conteúdo de Pré-Teste para criar um conteúdo de pré-teste de sequência de tarefas. Para obter informações sobre como criar um arquivo de conteúdo pré-teste, consulte [Prestage content (Conteúdo pré-teste)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).|  
|**Moverr**|Move a sequência de tarefas selecionada para outra pasta.|  

## <a name="next-steps"></a>Próximas etapas
[Cenários para implantar sistemas operacionais corporativos](scenarios-to-deploy-enterprise-operating-systems.md)
