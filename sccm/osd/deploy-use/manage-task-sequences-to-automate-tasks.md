---
title: Gerenciar sequências de tarefas
titleSuffix: Configuration Manager
description: Crie, edite, implante, importe e exporte sequências de tarefas para gerenciá-las e automatizar tarefas em seu ambiente.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0f3eb6a459eee5d97575b00a4d9de494910bb303
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140364"
---
# <a name="manage-task-sequences-to-automate-tasks-in-configuration-manager"></a>Gerenciar sequências de tarefas para automatizar tarefas no Gerenciador de Configurações

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use sequências de tarefas para automatizar as etapas em seu ambiente do Configuration Manager. Essas etapas podem implantar uma imagem do sistema operacional em um computador de destino, compilar e capturar uma imagem do sistema operacional de um conjunto de arquivos de instalação do sistema operacional, além de capturar e restaurar as informações de estado do usuário. As sequências de tarefas estão localizadas no console do Configuration Manager. No workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Sequências de Tarefas**. O nó **Sequências de Tarefas**, incluindo as subpastas criadas, é replicado em toda a hierarquia do Configuration Manager. Para obter informações sobre planejamento, consulte [Planning considerations for automating tasks (Considerações de planejamento para automatizar tarefas)](/sccm/osd/plan-design/planning-considerations-for-automating-tasks).  



##  <a name="BKMK_CreateTaskSequence"></a> Criar sequências de tarefas  

 Crie sequências de tarefas usando o Assistente para Criar Sequência de Tarefas. Este assistente pode criar os seguintes tipos de sequências de tarefas:  

|Tipo de sequência de tarefas|Mais informações|  
|------------------------|----------------------|  
|[Sequência de tarefas para instalar um sistema operacional](create-a-task-sequence-to-install-an-operating-system.md)|Esse tipo de sequência de tarefas cria as etapas para instalar um sistema operacional. Também inclui opções para migrar dados de usuário, incluir atualizações de software e instalar aplicativos.|  
|[Sequência de tarefas para atualizar um sistema operacional](create-a-task-sequence-to-upgrade-an-operating-system.md)|Esse tipo de sequência de tarefas cria as etapas para atualizar um sistema operacional. Também contém opções para incluir atualizações de software e instalar aplicativos.|  
|[Sequência de tarefas para capturar um sistema operacional](create-a-task-sequence-to-capture-an-operating-system.md)|Esse tipo de sequência de tarefas cria as etapas para compilar e capturar um sistema operacional de um computador de referência. É possível incluir atualizações de software e instalar aplicativos no computador de referência antes de capturar a imagem.|  
|[Sequência de tarefas para capturar e restaurar o estado do usuário](create-a-task-sequence-to-capture-and-restore-user-state.md)|Essa sequência de tarefas fornece as etapas a serem adicionadas a uma sequência de tarefas existente para capturar e restaurar dados de estado do usuário.|  
|[Sequência de tarefas personalizada](create-a-custom-task-sequence.md)|Esse tipo de sequência de tarefas não adiciona etapas à sequência de tarefas. Após a criação dessa sequência de tarefas, edite-a e adicione as etapas.|  



## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Retornar à página anterior quando uma sequência de tarefas falhar

Você pode retornar a uma página anterior quando executar uma sequência de tarefas e ocorrer uma falha. Nas versões anteriores do Configuration Manager, era necessário reiniciar a sequência de tarefas em caso de falha. Use o botão **Anterior** nos seguintes cenários:

- Quando um computador é iniciado no Windows PE, a caixa de diálogo de inicialização da sequência de tarefas pode ser exibida antes da sequência estar disponível. Ao clicar em Avançar nesse cenário, a página final da sequência de tarefas exibe uma mensagem informando que não há sequências de tarefas disponíveis. Agora, você pode clicar em **Anterior** para pesquisar novamente por sequências de tarefas disponíveis. Você pode repetir esse processo até que a sequência de tarefas esteja disponível.  

- Quando você executa uma sequência de tarefas, porém pacotes dependentes de conteúdo ainda não estão disponíveis nos pontos de distribuição, a sequência de tarefas falhará. Se o conteúdo ausente ainda não foi distribuído, distribua-o agora. Se preferir, aguarde até que o conteúdo esteja disponível nos pontos de distribuição. Em seguida, clique em **Anterior** para que a sequência de tarefas pesquise o conteúdo novamente.



##  <a name="BKMK_ModifyTaskSequence"></a> Editar uma sequência de tarefas  

 Modifique uma sequência de tarefas adicionando ou removendo etapas, adicionando ou removendo grupos ou alterando a ordem das etapas. Use o seguinte procedimento para modificar uma sequência de tarefas existente:  

> [!IMPORTANT]  
>  Ao editar uma sequência de tarefas criada com o Assistente para Criar Sequência de Tarefas, o nome da etapa pode ser a ação ou o tipo da etapa. Por exemplo, talvez você veja uma etapa com o nome “Particionar Disco 0”, que corresponde à ação de uma etapa do tipo [Format and Partition Disk (Formatar e Particionar Disco)](/sccm/osd/understand/task-sequence-steps#BKMK_FormatandPartitionDisk). Todas as etapas da sequência de tarefas são documentadas por seu tipo, não necessariamente pelo nome da etapa exibido no editor.  

#### <a name="to-edit-a-task-sequence"></a>Para editar uma sequência de tarefas  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas a editar.  

4.  Na guia **Início** , no grupo **Sequência de Tarefas** , clique em **Editar**e, então, execute uma das seguintes operações:  

    -   Para adicionar uma etapa de sequência de tarefas, clique em **Adicionar**, selecione o tipo da etapa e, em seguida, clique na etapa a ser adicionada. Por exemplo, para adicionar a etapa Executar linha de comando, clique em **Adicionar**, selecione **Geral**e clique em **Executar Linha de Comando**.  

    -   Para adicionar um grupo à sequência de tarefas, clique em **Adicionar**e, em seguida, em **Novo Grupo**. Depois de adicionar um grupo, adicione etapas ao grupo.  

    -   Para alterar a ordem das etapas e dos grupos na sequência de tarefas, selecione a etapa ou o grupo que deseje reordenar e, em seguida, use os ícones **Mover Item para Cima** ou **Mover Item para Baixo**. Você pode mover apenas uma etapa ou grupo por vez.  

    -   Para remover uma etapa ou um grupo, selecione a etapa ou o grupo e clique em **Remover**.  

5.  Clique em **OK** para salvar as alterações.  


 Para obter uma lista das etapas de sequência de tarefas disponíveis, consulte [Task sequence steps (Etapas da sequência de tarefas)](/sccm/osd/understand/task-sequence-steps).  



## <a name="bkmk_prop-general"></a> Configurar as propriedades do Centro de Software

 Use o procedimento a seguir para configurar os detalhes da sequência de tarefas exibida no Centro de Software. Esses detalhes são apenas para fins informativos.  

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Sequências de Tarefas**.  

2. Selecione a sequência de tarefas a ser editada e clique em **Propriedades**.  

3. Na guia **Geral**, as seguintes configurações do Centro de Software estão disponíveis:  

   - **Reinicialização necessária**: permite que o usuário saiba se uma reinicialização é necessária durante a instalação.  

   - **Tamanho do download (MB)**: especifica quantos megabytes são exibidos no Centro de Software para a sequência de tarefas.  

   - **Tempo de execução estimado (minutos)**: especifica o tempo de execução estimado em minutos exibido no Centro de Software para a sequência de tarefas.  



## <a name="bkmk_prop-advanced"></a> Definir as configurações da sequência de tarefas avançadas

 Use o procedimento a seguir para configurar o comportamento da sequência de tarefas no cliente do Gerenciador de Configurações.  

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Sequências de Tarefas**.  

2. Selecione a sequência de tarefas a ser editada e clique em **Propriedades**.  

3. Na guia **Avançado**, as seguintes configurações estão disponíveis:  

   - **Executar outro programa primeiro**: selecione esta opção para executar um programa em outro pacote antes da execução da sequência de tarefas. Por padrão, essa caixa de seleção está desmarcada. Não é necessário implantar separadamente o programa que você especifica para executar primeiro.  

     > [!IMPORTANT]
     >   Essa configuração aplica-se apenas às sequências de tarefas que são executadas no sistema operacional completo. O Gerenciador de Configurações ignorará esta configuração se a sequência de tarefas for iniciada usando o PXE ou a mídia de inicialização.  

     - **Pacote**: procure o pacote que contém o programa para execução antes dessa sequência de tarefas.  

     - **Programa**: selecione o programa a ser executado antes dessa sequência de tarefas.  

       > [!NOTE]    
       > Se o programa selecionado não é executado em um cliente, a sequência de tarefas não é executada. Se o programa selecionado é executado com êxito, ele não é executado novamente, mesmo se a sequência de tarefas é executada novamente no mesmo cliente.  
   
   - **Suprimir notificações de sequência de tarefa**: Selecione esta opção para ocultar a notificação do sistema 'Há um novo software disponível'. Você ainda deverá ver o ícone 'novo software' do Centro de Software na área de notificação. Por padrão, essa caixa de seleção está desmarcada.  
 
   - **Desabilitar esta sequência de tarefas nos computadores nos quais está implantada**: Se você selecionar esta opção, o Configuration Manager desabilitará temporariamente todas as implantações que contêm esta sequência de tarefas. Também remove a sequência de tarefas da lista de implantações disponíveis para execução. A sequência de tarefas não será executada até que você a habilite. Por padrão, esta opção está desmarcada.  

   - **Tempo de execução máximo permitido**: especifica o tempo máximo, em minutos, esperado para a execução da sequência de tarefas no computador de destino. Use um número inteiro igual ou maior que zero. Por padrão, esse valor é de 120 minutos.  

       > [!IMPORTANT]    
       > Se você estiver usando janelas de manutenção para a coleção na qual implanta essa sequência de tarefas, poderá ocorrer um conflito se o **Tempo de execução máximo permitido** for maior do que o tempo da janela de manutenção agendada. Se o tempo de execução máximo for definido como **0**, a sequência de tarefas será iniciada durante a janela de manutenção. Ela continuará sendo executada até ser concluída ou falhar depois que a janela de manutenção for fechada. Como resultado, as sequências de tarefas com um tempo de execução máximo definido como **0** pode ser executado após o término de suas janelas de manutenção. Se você definir o tempo de execução máximo com um período específico (diferente de zero) que excede a duração de qualquer janela de manutenção disponível, essa sequência de tarefas não será executada. Para obter mais informações, consulte [Como usar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).  
 
      Se você definir o valor como **0**, o Gerenciador de Configurações avaliará o tempo de execução máximo permitido para **12** horas (720 minutos) para monitoramento do progresso. No entanto, a sequência de tarefas será iniciada, desde que a duração da contagem regressiva não exceda o valor da janela de manutenção.  

      > [!NOTE]    
      > Ao atingir o tempo de execução máximo, o Gerenciador de Configurações interromperá a sequência de tarefas se você tiver definido a opção **Executar com direitos administrativos** e não a opção **Permitir que os usuários interajam com este programa**. Se a sequência de tarefas não for interrompida, o Gerenciador de Configurações parará de monitorar a sequência de tarefas após atingir o tempo de execução máximo permitido.  

   - **Usar uma imagem de inicialização**: use a imagem de inicialização selecionada quando a sequência de tarefas for executada. Clique em **Procurar** para selecionar uma imagem de inicialização diferente. Desmarque esta opção para desabilitar o uso da imagem de inicialização selecionada quando a sequência de tarefas for executada.  

   - **Essa sequência de tarefas pode ser executada em qualquer plataforma**: Se você selecionar essa opção, o Configuration Manager não verificará o tipo de plataforma do computador de destino quando a sequência de tarefas for executada. Essa opção é habilitada por padrão.  

   - **Essa sequência de tarefas pode ser executada somente nas plataformas clientes especificadas**: Essa opção especifica os processadores, as versões de sistema operacional e os service packs nos quais essa sequência de tarefas pode ser executada. Ao selecionar essa opção, selecione pelo menos uma plataforma na lista. Por padrão, nenhuma plataforma é selecionada. O Configuration Manager usa essas informações quando avalia quais computadores de destino em uma coleção recebem a sequência de tarefas implantada.  

       > [!NOTE]    
       > Quando você executa uma sequência de tarefas na mídia de inicialização ou PXE, o Gerenciador de Configurações ignora essa opção. A sequência de tarefas é executada como se a opção **Este programa pode ser executado em qualquer plataforma** estivesse selecionada.  



## <a name="configure-high-impact-task-sequence-settings"></a>Definir configurações da sequência de tarefas de alto impacto

 Configure uma sequência de tarefas como alto impacto e personalize as mensagens recebidas pelos usuários quando eles executam a sequência de tarefas.


### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Definir uma sequência de tarefas como uma sequência de tarefas de alto impacto

 Use o procedimento a seguir para definir uma sequência de tarefas como de alto impacto.

> [!NOTE]    
> Qualquer sequência de tarefas que atender a determinadas condições será automaticamente definida como de alto impacto. Para obter mais informações, consulte [Gerenciar implantações de alto risco](/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Sequências de Tarefas**.  

2. Selecione a sequência de tarefas a ser editada e clique em **Propriedades**.  

3. Na guia **Notificação do Usuário**, selecione **Essa é uma sequência de tarefas de alto impacto**.  


### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Criar uma notificação personalizada para implantações de alto risco

 Use o procedimento a seguir para criar uma notificação personalizada para implantações de alto impacto.

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Sequências de Tarefas**.  

2. Selecione a sequência de tarefas a ser editada e clique em **Propriedades**.  

3. Na guia **Notificação do Usuário**, selecione **Usar texto personalizado**.  

   > [!NOTE]
   >  Só é possível definir o texto de notificação do usuário quando a opção **Esta é uma sequência de tarefas de alto impacto** for selecionada.  

4. Defina as seguintes configurações:  

    > [!Note]  
    > Cada caixa de texto tem um limite máximo de 255 caracteres.  

    **Texto do título de notificação ao usuário**: especifica o texto azul exibido na notificação ao usuário do Centro de Software. Por exemplo, na notificação de usuário padrão, essa seção contém o texto "Confirme se você deseja atualizar o sistema operacional neste computador".  

    **Texto da mensagem de notificação ao usuário**: há três caixas de texto que fornecem o corpo da notificação personalizada. Todas as caixas de texto exigem que você adicione texto.  

    - Primeira caixa de texto: especifica o corpo principal do texto, geralmente contendo instruções para o usuário. Por exemplo, na notificação de usuário padrão, essa seção contém o texto "A atualização do sistema operacional leva tempo e o computador pode ser reiniciado várias vezes".  

    - Segunda caixa de texto: especifica o texto em negrito abaixo do corpo principal do texto. Por exemplo, na notificação de usuário padrão, essa seção contém o texto "Esta atualização in-loco instala o novo sistema operacional e migra automaticamente seus aplicativos, dados e configurações".  

    - Terceira caixa de texto: especifica a última linha de texto sob o texto em negrito. Por exemplo, na notificação de usuário padrão, essa seção contém o texto "Clique em Instalar para começar. Caso contrário, clique em Cancelar”.   

#### <a name="example"></a>Exemplo
Digamos que você defina a seguinte notificação personalizada nas propriedades.

![Guia Notificação de Usuário Personalizada das propriedades da sequência de tarefas](../media/user-notification.png)

A mensagem de notificação a seguir é exibida quando o usuário final abre a instalação no Centro de Software.

![Notificação personalizada de sequência de tarefas para o usuário final no Centro de Software](../media/user-notification-enduser.png)



##  <a name="BKMK_DistributeTS"></a> Distribuir o conteúdo referenciado por uma sequência de tarefas  

 Para os clientes executarem uma sequência de tarefas que faz referência ao conteúdo, distribua esse conteúdo para pontos de distribuição. A qualquer momento você pode selecionar uma sequência de tarefas e distribuir seu conteúdo para criar uma nova lista de pacotes de referência para distribuição. Se você fizer alterações à sequência de tarefas com o conteúdo atualizado, será necessário redistribuí-lo antes de disponibilizá-lo para os clientes. Use o procedimento a seguir para distribuir o conteúdo que é referenciado por uma sequência de tarefas.  

#### <a name="to-distribute-referenced-content-to-distribution-points"></a>Para distribuir o conteúdo referenciado para pontos de distribuição  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas a distribuir.  

4.  Na guia **Início** , no grupo **Implantação** , clique em **Distribuir Conteúdo** para iniciar o Assistente para Distribuir Conteúdo.  

5.  Na página **Geral**, verifique se a sequência de tarefas correta está selecionada para distribuição. Clique em **Avançar**.  

6.  Na página **Conteúdo** , verifique o conteúdo a distribuir, como, por exemplo, a imagem de inicialização referenciada pela sequência de tarefas, e, em seguida, clique em **Próximo**.  

7.  Na página **Destino de Conteúdo**, especifique as coleções, o ponto de distribuição ou o grupo de pontos de distribuição para os quais deseja distribuir o conteúdo da sequência de tarefas. Clique em **Avançar**.  

    > [!IMPORTANT]  
    >  Se a sequência de tarefas que você selecionou fizer referência ao conteúdo já distribuído a um ponto de distribuição específico, o assistente não listará esse ponto de distribuição.  

8.  Conclua o assistente.  


 Também é possível pré-configurar o conteúdo referenciado na sequência de tarefas. O Configuration Manager cria um arquivo de conteúdo compactado e pré-configurado que contém os arquivos, as dependências associadas e os metadados associados para o conteúdo selecionado. Depois, importe manualmente o conteúdo em um servidor de site, site secundário ou ponto de distribuição. Para obter mais informações sobre como pré-configurar arquivos de conteúdo, consulte [Prestage content (Pré-configurar conteúdo)](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  



##  <a name="BKMK_DeployTS"></a> Implantar uma sequência de tarefas  

 Use o procedimento a seguir para implantar uma sequência de tarefas para computadores em uma coleção.  

> [!WARNING]  
>  Você pode gerenciar o comportamento de implantações de sequência de tarefas de alto risco. Uma implantação de alto risco é uma implantação que é instalada automaticamente e que tem o potencial de causar resultados indesejados. Por exemplo, uma sequência de tarefas que tem uma finalidade **Obrigatória** que implanta um sistema operacional é considerada uma implantação de alto risco. Para obter mais informações, consulte [Configurações para gerenciar implantações de alto risco](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments).  

> [!NOTE]  
>  As mensagens de status para a implantação de sequência de tarefas são exibidas na janela de mensagem no site primário, mas não são exibidas no site de administração central.  

#### <a name="to-deploy-a-task-sequence"></a>Para implantar uma sequência de tarefas    

1. No console do Configuration Manager, clique em **Biblioteca de Software**.  

2. No workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e clique em **Sequências de Tarefas**.  

3. Na lista **Sequência de Tarefas** , selecione a sequência de tarefas a implantar.  

4. Na guia **Início** , no grupo **Implantação** , clique em **Implantar**.  

   > [!NOTE]  
   >  Se **Implantar** não estiver disponível, a sequência de tarefas terá uma referência que não será válida. Corrija a referência e, em seguida, tente implantar a sequência de tarefas novamente.  

5. Na página **Geral** , especifique as seguintes informações e clique em **Próximo**.  

   - **Sequência de tarefas**: especifique a sequência de tarefas para implantação. Por padrão, essa caixa exibe a sequência de tarefas selecionada.  

   - **Coleta**: selecione a coleção que contém os computadores que executarão a sequência de tarefas.  

      Não implante uma sequência de tarefas que instala um sistema operacional em coleções inadequadas, como uma coleção de todos os servidores de data center. A coleção selecionada precisa conter somente os computadores que você quer que executem a sequência de tarefas.  

     > [!NOTE]
     >  Ao executar uma implantação de alto risco, como um sistema operacional, a janela **Selecionar Coleção** exibe somente as coleções personalizadas que atendem às configurações de verificação da implantação definidas nas propriedades do site. As implantações de alto risco sempre estão limitadas às coleções personalizadas criadas e à coleção interna de **Computadores desconhecidos** . Ao criar uma implantação de alto risco, não é possível selecionar uma coleção interna como **Todos os Sistemas**. Desmarque **Ocultar coleções com uma contagem de membros maior que a configuração de tamanho mínimo do site** para ver todas as coleções personalizadas que contêm menos clientes do que o tamanho máximo configurado. Para obter mais informações, consulte [Configurações para gerenciar implantações de alto risco](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments).  
     > 
     >  As configurações de verificação de implantação baseiam-se na associação atual da coleção. Depois de implantar a sequência de tarefas, o Gerenciador de Configurações não reavalia a associação à coleção quanto às configurações de implantação de alto risco.  
     > 
     >  Por exemplo, suponhamos que você defina **Tamanho padrão** como 100 e o **Tamanho máximo** como 1000. Ao criar uma implantação de alto risco, a janela **Selecionar Coleção** exibe somente as coleções que contêm menos de 100 clientes. Se você desmarcar a configuração **Ocultar coleções com uma contagem de membros maior que a configuração mínima de tamanho do site**, a janela exibirá coleções que contêm menos de 1.000 clientes.  
     > 
     >  Ao selecionar uma coleção que contém uma função de site, o seguinte comportamento se aplica:  
     > 
     > - Se a coleção contiver um servidor do sistema de sites e você definiu as configurações de verificação da implantação para bloquear coleções com servidores do sistema de sites, ocorrerá um erro. Você não poderá continuar criando a implantação.  
     >   -   Se um dos critérios a seguir se aplicar, o Assistente de Implantação de Software exibirá um aviso de alto risco. Para continuar, você precisa concordar em criar uma implantação de alto risco. O site gera uma mensagem de status de auditoria.  
     >   - Se a coleção contiver um servidor do sistema de sites e você definiu as configurações de verificação da implantação para alertar sobre coleções com servidores do sistema de sites
     >   - Se a coleção exceder o valor do tamanho padrão
     >   - Se a coleção contiver um servidor  

   - **Usar grupos de pontos de distribuição padrão associados a esta coleção**: Armazene o conteúdo da sequência de tarefas no grupo dos pontos de distribuição padrão das coleções. Se você não tiver associado a coleção selecionada a um grupo de pontos de distribuição, essa opção estará desabilitada.  

   - **Distribuir automaticamente conteúdo para dependências**: se o conteúdo referenciado tiver dependências, o site também enviará o conteúdo dependente aos pontos de distribuição.  

   - **Conteúdo pré-baixado para esta sequência de tarefas**: Para saber mais, confira [Configurar o conteúdo de armazenamento prévio em cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  

   - **Selecionar o Modelo de Implantação**: começando no Configuration Manager versão 1802,<!--1357391--> é possível salvar e especificar um modelo de implantação para uma sequência de tarefas.     

        > [!IMPORTANT]  
        > No Gerenciador de Configurações versão 1802, alguns itens não são salvos no modelo.  <!--510610--> Aplique os itens a seguir ao executar o assistente de implantação:  
        > - Instalação de Software 
        > - Agendamento 
        > - Pré-baixar conteúdo
 
   - **Comentários (opcional)**: especifique informações adicionais que descrevem essa implantação de sequência de tarefas.  

6. Na página **Configurações de Implantação** , especifique as seguintes informações e clique em **Próximo**.  

   - **Finalidade**: Na lista suspensa, escolha uma das seguintes opções:  

     -   **Disponível**: o usuário vê a sequência de tarefas no Centro de Software e poderá instalá-la sob demanda.  

     -   **Obrigatório**: o Configuration Manager executa automaticamente a sequência de tarefas de acordo com o agendamento configurado. Se a sequência de tarefas não estiver oculta, um usuário ainda poderá acompanhar seu status de implantação. Eles também podem usar o Centro de Software para instalar a sequência de tarefas antes do prazo.  

     > [!NOTE]
     >  Se vários usuários estiverem conectados ao dispositivo, as implantações de pacote e sequência de tarefas talvez não sejam exibidas no Centro de Software.  

   - **Disponibilizar para o seguinte**: especifique se a sequência de tarefas está disponível para um dos tipos a seguir:  
     - Somente clientes do Gerenciador de Configurações  
     - Clientes do Configuration Manager, mídia e PXE  
     - Somente mídia e PXE  
     - Somente mídia e PXE (oculto)  

     > [!IMPORTANT]  
     >  Use a configuração **Somente mídia e PXE (oculto)** para implantações automatizadas de sequência de tarefas. Para que o computador seja inicializado automaticamente para a implantação sem a interação do usuário, selecione **Permitir implantação autônoma de sistema operacional** e defina a variável **SMSTSPreferredAdvertID** como parte da mídia. Para saber mais sobre variáveis de sequência de tarefas, confira [Variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#SMSTSPreferredAdvertID).  

   - **Enviar pacotes de ativação**: se a implantação for **Obrigatória** e você selecionar essa opção, o site enviará um pacote de ativação aos computadores antes que o cliente execute a implantação. Esse pacote ativa os computadores na hora limite da instalação. Antes de usar essa opção, os computadores e as redes devem ser configurados para Wake On LAN. Para obter mais informações, confira [Planejar como ativar clientes](/sccm/core/clients/deploy/plan/plan-wake-up-clients).  

   - **Permitir que clientes em uma conexão de Internet limitada baixem conteúdo após o prazo de instalação, o que pode incorrer custos adicionais**: Essa opção só está disponível para implantações **Obrigatórias**. Quando você tem um sequência de tarefas personalizada que instala um aplicativo, mas não implanta um sistema operacional, pode especificar se permite que os clientes baixem conteúdo após o prazo de instalação quando usarem conexões de Internet limitada. Às vezes, os provedores de Internet cobram pela quantidade de dados que você usa quando está em uma conexão de Internet limitada.  

     > [!NOTE]  
     >  Embora o uso de um plano de Internet limitado possa funcionar para sequências de tarefas que não implantam um sistema operacional, não há suporte para esse recurso.  

7. Na página **Agendamento** , especifique as informações a seguir e clique em **Próximo**.  

   > [!IMPORTANT]  
   >  Quando um cliente do Windows PE é iniciado pelo PXE ou pela mídia de inicialização, ele não avalia agendas de implantação. Essas agendas incluem os horários de início, expiração e prazo. Somente configure agendamentos em implantações em clientes que iniciam com o sistema operacional Windows completo. Considere usar outros métodos, como janelas de manutenção, para controlar as sequências de tarefas ativas implantadas nos clientes que iniciam por meio do Windows PE.  

   -   **Agendar quando essa implantação estará disponível**: especifique a data e a hora em que a sequência de tarefas está disponível para ser executada no computador de destino. Quando você marca a caixa de seleção **UTC**, a sequência de tarefas fica disponível para vários computadores ao mesmo tempo. Caso contrário, a implantação ficará disponível em momentos diferentes, acordo com a hora local em cada computador.  

        Se a hora de início for anterior à hora exigida, o cliente baixará o conteúdo da sequência de tarefas na hora de início.  

   -   **Agendar quando esta implantação expirará**: especifique a data e a hora em que a sequência de tarefas expirará no computador de destino. Quando você marca a caixa de seleção **UTC**, a sequência de tarefas expira em vários computadores de destino ao mesmo tempo. Caso contrário, a implantação expira em momentos diferentes, acordo com a hora local em cada computador.  

   -   **Agendamento da atribuição**: para uma implantação **Obrigatória**, especifique quando o cliente executa a sequência de tarefas. Você pode adicionar vários agendamentos. O agendamento da atribuição pode ter uma das seguintes configurações:   
       - Data e hora específicas  
       - Padrão de recorrência mensal, semanal ou personalizado  
       - O mais breve possível  
       - Eventos de logon ou logoff  

       > [!NOTE]  
       >  Se você agendar uma hora de início para uma implantação obrigatória anterior à data e hora de disponibilização da sequência de tarefas, o cliente do Gerenciador de Configurações baixará o conteúdo na hora de início atribuída. Esse comportamento ocorre mesmo que você tenha agendado a sequência de tarefas para disponibilização em um momento posterior.<!--SCCMDocs issue 777-->  

   -   **Executar comportamento novamente**: especifique quando a sequência de tarefas é executada novamente. Selecione uma das seguintes opções:  

       -   **Nunca executar novamente o programa implantado**: se o cliente já tiver executado a sequência de tarefas anteriormente, ela não será executada novamente. A sequência de tarefas não será executada novamente, mesmo se ela falhar originalmente ou se os arquivos da sequência de tarefas forem alterados.  

       -   **Sempre executar novamente o programa**: a sequência de tarefas sempre é executada novamente no cliente quando a implantação é agendada. Executa novamente mesmo se a sequência de tarefas já tiver sido executada com êxito. Essa configuração é útil quando você usa implantações recorrentes nas quais a sequência de tarefas é atualizada regularmente.  

           > [!IMPORTANT]  
           >  Essa opção é habilitada por padrão. No entanto, ela não tem efeito até que você atribua uma implantação obrigatória. O usuário sempre pode executar novamente as implantações disponíveis.  

       -   **Executar novamente se a tentativa anterior falhar**: a sequência de tarefas será executada novamente quando a implantação for agendada e somente se houver falha na execução anterior. Essa configuração é útil para implantações obrigatórias. Se a última tentativa de execução não for bem-sucedida, uma nova tentativa será feita de acordo com o agendamento de atribuição.  

       -   **Executar novamente se a tentativa anterior tiver êxito**: A sequência de tarefas será executada novamente somente se ela tiver sido executada com êxito no cliente. Essa configuração é útil ao usar implantações recorrentes nas quais a sequência de tarefas é atualizada regularmente, e cada atualização requer que a atualização anterior esteja instalada com êxito.  

       > [!NOTE]  
       >  Um usuário pode executar novamente uma implantação de sequência de tarefas disponível. Antes de implantar uma sequência de tarefas disponível em um ambiente de produção, teste o que acontece se um usuário executar várias vezes a sequência de tarefas.  

8. Na página **Experiência do Usuário** , especifique as seguintes informações e clique em **Próximo**.  

   -   **Permitir que o usuário execute o programa de forma independente das atribuições**: especifique se um usuário pode executar uma implantação obrigatória fora do agendamento da atribuição. Essa opção está sempre habilitada para as implantações disponíveis.   

   -   **Mostrar andamento da sequência de tarefas**: especifique se o cliente do Configuration Manager exibe o andamento da sequência de tarefas.  

   -   **Instalação do software**: especifique se o usuário tem permissão para instalar software fora de uma janela de manutenção configurada após a hora agendada.  

   -   **Reinicialização do sistema (se necessário para conclusão da instalação)**: especifique se o usuário tem permissão para reiniciar o computador após uma instalação de software fora de uma janela de manutenção configurada após a hora de atribuição.  

   - **Manuseio de filtro de gravação para dispositivos Windows Embedded**: Essa configuração controla o comportamento da instalação em dispositivos Windows Embedded habilitados com um filtro de gravação. Escolha a opção para confirmar as alterações na data limite da instalação ou durante uma janela de manutenção. Quando você seleciona essa opção, a reinicialização é necessária e as alterações permanecem no dispositivo. Caso contrário, o aplicativo é instalado na sobreposição temporária e confirmado mais tarde. Ao implantar uma sequência de tarefas em um dispositivo Windows Embedded, verifique se o dispositivo é membro de uma coleção com uma janela de manutenção configurada.  

   -   **Permitir que a sequência de tarefas seja executada para cliente na Internet**: especifique se a sequência de tarefas tem permissão para ser executada em um cliente baseado em Internet. Não há suporte para operações que instalam o software, como um sistema operacional, nessa configuração. Use essa opção somente para sequências de tarefas baseadas em script genérico que executam operações no sistema operacional padrão.  

        - A partir da versão 1802, essa configuração é compatível com implantações de uma sequência de tarefas de atualização in-loco do Windows 10 para clientes baseados na Internet por meio do gateway de gerenciamento de nuvem. Para obter mais informações, consulte [Implantar a atualização in-loco do Windows 10 por meio do CMG](#deploy-windows-10-in-place-upgrade-via-cmg).    

9. Na página **Alertas** , especifique as configurações de alerta que você deseja para esta sequência de tarefas e clique em **Próximo**.  

10. Na página **Pontos de Distribuição** , especifique as seguintes informações e clique em **Próximo**.  

    -   **Opções de implantação**: especifique uma das seguintes opções:  

        > [!NOTE]  
        >  Ao usar o multicast para implantar um sistema operacional, baixe o conteúdo nos computadores de destino conforme o necessário ou antes da execução da sequência de tarefas.  

        - **Baixar conteúdo localmente quando necessário pela sequência de tarefas em execução**: especifique se os clientes baixam o conteúdo do ponto de distribuição conforme necessário pela sequência de tarefas. O cliente inicia a sequência de tarefas. Quando uma etapa na sequência de tarefas exigir o conteúdo, ele será baixado antes da execução da etapa.  

        - **Baixar todo o conteúdo localmente antes de iniciar a sequência de tarefas**: especifique se os clientes baixam todo o conteúdo do ponto de distribuição antes da execução da sequência de tarefas. Se a sequência de tarefas for disponibilizada para implantações de PXE e de mídia de inicialização na página **Configurações de implantação**, essa opção não aparecerá.  

        - **Acessar conteúdo diretamente de um ponto de distribuição quando necessário pela sequência de tarefas em execução**: especifique que os clientes executem o conteúdo do ponto de distribuição. Essa opção só é disponibilizada quando todos os pacotes associados à sequência de tarefas estiverem habilitados para usar um compartilhamento de pacotes no ponto de distribuição. Para habilitar o conteúdo a usar um compartilhamento de pacotes, consulte a guia **Acesso a Dados** nas **Propriedades** de cada pacote.  

    -   **Quando não houver nenhum ponto de distribuição local disponível, use um ponto de distribuição remoto**: especifique se os clientes podem usar pontos de distribuição de um grupo de limites vizinho para baixar o conteúdo exigido pela sequência de tarefas.  

    - **Permitir que os clientes usem pontos de distribuição do grupo de limites de site padrão**: especifique se os clientes devem baixar conteúdo de um ponto de distribuição no grupo de limites do site padrão quando ele não está disponível em um ponto de distribuição nos grupos de limites atuais ou vizinhos.  

        > [!Note]  
        > Da versão 1810 em diante, quando um dispositivo executa uma sequência de tarefas e precisa adquirir conteúdo, ele usa comportamentos de grupo de limites semelhantes ao cliente do Configuration Manager. Para obter mais informações, confira [Suporte de sequência de tarefas para grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgr-osd).<!--1359025-->  

11. A partir do Configuration Manager 1802, na guia **Resumo**, clique em **Salvar Como Modelo** se desejar salvar as configurações para serem usadas novamente. Forneça um nome para o modelo e selecione as configurações a serem salvas.  

12. Conclua o assistente.  


### <a name="deploy-windows-10-in-place-upgrade-via-cmg"></a>Implantar a atualização in-loco do Windows 10 por meio do CMG
<!-- 1357149 -->

A partir da versão 1802, a sequência de tarefas de atualização in-loco do Windows 10 é compatível com a implantação de clientes baseados na Internet gerenciados por meio do [CMG](/sccm/core/clients/manage/plan-cloud-management-gateway) (gateway de gerenciamento de nuvem). Essa capacidade proporciona aos usuários remotos uma atualização mais fácil para o Windows 10 sem a necessidade de se conectar à intranet. 

Certifique-se de que todo o conteúdo referenciado pela sequência de tarefas de upgrade in-loco seja distribuído para um [ponto de distribuição da nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point). Caso contrário, os dispositivos não podem executar a sequência da tarefas.

Ao implantar uma sequência de tarefas de upgrade, use as seguintes configurações:

- **Permitir que a sequência de tarefas seja executada para o cliente na Internet**, na guia Experiência do Usuário da implantação.  

- **Baixar todo o conteúdo localmente antes de iniciar a sequência de tarefas**, na guia Pontos de Distribuição da implantação. Outras opções, como **Baixar conteúdo localmente quando necessário, executando a sequência de tarefas**, não funcionam neste cenário. O mecanismo de sequência de tarefas atualmente não consegue obter conteúdo de um ponto de distribuição da nuvem. O cliente do Configuration Manager deve baixar o conteúdo a partir do ponto de distribuição da nuvem antes de iniciar a sequência de tarefas.  

- (*Opcional*) **Conteúdo pré-baixado para esta sequência de tarefas**, na guia Geral da implantação. Para saber mais, confira [Configurar o conteúdo de armazenamento prévio em cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  



##  <a name="BKMK_ExportImport"></a> Exportar e importar sequências de tarefas  

 Exporte e importe sequências de tarefas com ou sem seus objetos relacionados. Esse conteúdo referenciado inclui os seguintes objetos:  
 - Imagens do sistema operacional  
 - Imagens de inicialização  
 - Pacotes como o pacote de instalação do cliente  
 - Pacotes de driver  
 - Aplicativos com dependências  


 Considere os pontos a seguir ao exportar e importar sequências de tarefas:  

 - O Gerenciador de Configurações não exporta as senhas na sequência de tarefas. Se você exportar e importar uma sequência de tarefas que contém senhas, edite a sequência de tarefas importada e insira as senhas novamente. Examine as seguintes etapas que podem incluir uma senha:  
    - [Ingressar no Domínio ou Grupo de Trabalho](/sccm/osd/understand/task-sequence-steps#BKMK_JoinDomainorWorkgroup)  
    - [Conectar à Pasta de Rede](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder)  
    - [Executar Linha de Comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)  

 - Ao exportar uma sequência de tarefas com a etapa **Definir Variáveis Dinâmicas**, o Gerenciador de Configurações não exporta valores para variáveis definidas com a configuração **Valor secreto**. Insira novamente os valores dessas variáveis depois de importar a sequência de tarefas.  

 - Quando você tem vários sites primários, importe as sequências de tarefas no site de administração central.  


### <a name="to-export-task-sequences"></a>Para exportar as sequências de tarefas  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas a exportar. Se você selecionar mais de uma sequência de tarefas, todas serão armazenadas em um arquivo de exportação.  

4.  Na guia **Início** , no grupo **Sequência de Tarefas** , clique em **Exportar** para iniciar o Assistente para Exportar Sequência de Tarefas.  

5.  Na página **Geral** , especifique as seguintes configurações e clique em **Próximo**.  

    -   Na caixa **Arquivo** , especifique o local e o nome do arquivo de exportação. Se você inserir o nome do arquivo diretamente, inclua a extensão .zip ao nome do arquivo. Se você procurar o arquivo de exportação, o assistente adicionará automaticamente essa extensão de nome de arquivo.  

    -   Se você não quiser exportar dependências da sequência de tarefas, desmarque a opção **Exportar todas as dependências de sequência de tarefas**. Por padrão, o assistente procura todos os objetos relacionados e exporta-os com a sequência de tarefas. Essas dependências incluem qualquer uma para aplicativos.  

    -   Se você não quiser copiar o conteúdo da origem do pacote para o local de exportação, desmarque a opção **Exportar todo conteúdo das sequências de tarefas e dependências selecionadas**. Se você selecionar essa opção, o Assistente para Importar Sequência de Tarefas usará o caminho de importação como o novo local da origem do pacote.  

    -   Na caixa **Comentários do administrador** , adicione uma descrição das sequências de tarefas a serem exportadas.  

6.  Conclua o assistente.  


 O assistente cria os seguintes arquivos de saída:  

-   Se você não exportar o conteúdo: um arquivo .zip.  

-   Se você exportar o conteúdo: um arquivo .zip e uma pasta chamada *export*_files, em que *export* é o nome do arquivo .zip que contém o conteúdo exportado.  


 Se você incluir o conteúdo ao exportar uma sequência de tarefas, copie o arquivo .zip e a pasta *export*_files ou a importação falhará.  


### <a name="to-import-task-sequences"></a>Para importar sequências de tarefas  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e clique em **Sequências de Tarefas**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Importar Sequência de Tarefas** para iniciar o Assistente para Importar Sequência de Tarefas.  

4.  Na página **Geral** , especifique o arquivo .zip e clique em **Próximo**.  

5.  Na página **Conteúdo do Arquivo** , selecione a ação que você requer para cada objeto que você importar. Essa página mostra todos os objetos encontrados pelo Configuration Manager a serem importados.  

    -   Se os objeto nunca foi importado, selecione **Criar Novo**.  

    -   Se o objeto foi importado anteriormente, selecione uma das seguintes ações:  

        -   **Ignorar Duplicado** (padrão): essa ação não importa o objeto. Em vez disso, o assistente vincula o objeto existente à sequência de tarefas.  

        -   **Substituir**: essa ação substitui o objeto existente pelo objeto importado. Para aplicativos, você pode adicionar uma revisão para atualizar o aplicativo existente ou criar um novo aplicativo.  

6.  Conclua o assistente.  


 Após importar a sequência de tarefas, edite-a para especificar senhas que estavam na sequência de tarefas original. Por motivos de segurança, as senhas não são exportadas.  



##  <a name="BKMK_CreateTSVariables"></a> Criar variáveis de sequência de tarefas em computadores e coleções  

 Você pode definir variáveis de sequência de tarefas personalizadas para computadores e coleções. As variáveis definidas para um computador são chamadas de variáveis de sequência de tarefas por computador. As variáveis definidas para uma coleção são chamadas de variáveis de sequência de tarefas por coleção. Se houver um conflito, as variáveis por computador prevalecerão sobre as variáveis por coleção. Esse comportamento significa que as variáveis de sequência de tarefas atribuídas a um computador específico têm automaticamente uma prioridade mais alta do que as variáveis atribuídas à coleção que contém o computador.  

 Por exemplo, o computador XYZ é membro da coleção ABC. Você pode atribuir MyVariable à coleção ABC com um valor 1. Você pode atribuir MyVariable ao computador XYZ com um valor 2. A variável atribuída ao computador XYZ tem prioridade maior do que a variável atribuída à coleção ABC. Quando uma sequência de tarefas com essa variável é executada no computador XYZ, MyVariable tem um valor 2. 

 É possível ocultar as variáveis por computador e por coleção de forma que elas não fiquem visíveis no console do Gerenciador de Configurações. Quando você usa a opção **Não exibir este valor no console do Gerenciador de Configurações**, o valor da variável não é exibido no console. A variável ainda pode ser usada pela sequência de tarefas quando ela é executada. Se você não quiser mais ocultar essas variáveis, exclua-as primeiro. Em seguida, redefina as variáveis sem selecionar a opção para ocultá-las.  

 > [!WARNING]    
 > A configuração **Não exibir este valor no console do Configuration Manager** se aplica somente ao console do Configuration Manager. Os valores das variáveis ainda são exibidos no arquivo de log da sequência de tarefas (SMSTS.LOG). 

 É possível gerenciar variáveis por computador em um site primário ou em um site de administração central. O Gerenciador de Configurações não dá suporte a mais de 1.000 variáveis atribuídas para um computador.  

> [!IMPORTANT]  
>  Ao usar variáveis por coleção para as sequências de tarefas, considere os seguintes comportamentos:  
>   
> - As alterações nas coleções sempre são replicadas em toda a hierarquia. As alterações feitas nas variáveis da coleção se aplicam não apenas aos membros do site atual, mas a todos os membros da coleção em toda a hierarquia.  
>  
> - Quando você exclui uma coleção, essa ação também exclui as variáveis da sequência de tarefas configuradas para a coleção.  


### <a name="to-create-task-sequence-variables-for-a-computer"></a>Para criar variáveis de sequência de tarefas para um computador  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade**, selecione o nó **Dispositivos**.  

3.  Selecione o computador de destino e clique em **Propriedades**.  

4.  Na caixa de seleção **Propriedades** , clique na guia **Variáveis** .  

5.  Para cada variável que você deseja criar, clique no ícone **Novo**. Especifique o **Nome** e o **Valor** da variável de sequência de tarefas. Se você quiser ocultar a variável para que ela não fique visível no console do Gerenciador de Configurações, selecione a opção **Não exibir este valor no console do Gerenciador de Configurações**.  

6.  Depois de ter adicionado todas as variáveis às propriedades do computador, clique em **OK**.  


### <a name="to-create-task-sequence-variables-for-a-collection"></a>Para criar variáveis de sequência de tarefas para uma coleção  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade**, selecione o nó **Coleções de Dispositivos**. Selecione a coleção de destino e clique em **Propriedades**.  

3.  Na caixa de seleção **Propriedades** , clique na guia **Variáveis da Coleção** .  

4.  Para cada variável que você deseja criar, clique no ícone **Novo**. Especifique o **Nome** e o **Valor** da variável de sequência de tarefas. Se você quiser ocultar a variável para que ela não fique visível no console do Gerenciador de Configurações, selecione a opção **Não exibir este valor no console do Gerenciador de Configurações**.  

5.  Opcionalmente, especifique a prioridade para o Gerenciador de Configurações usar quando as variáveis de sequência de tarefas são avaliadas.  

6.  Depois de adicionar todas as variáveis às propriedades da coleção, clique em **OK**.  



##  <a name="BKMK_AdditionalActionsTS"></a> Ações adicionais para gerenciar sequências de tarefas  

 Você pode gerenciar sequências de tarefas usando ações adicionais ao selecionar uma sequência de tarefas.  

#### <a name="to-select-a-task-sequence-to-manage"></a>Para selecionar uma sequência de tarefas a ser gerenciada  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas que deseja gerenciar e selecione uma das opções disponíveis.  


### <a name="available-options"></a>Opções disponíveis

#### <a name="edit"></a>Editar
 Para saber mais, confira [Editar uma sequência de tarefas](#BKMK_ModifyTaskSequence).

#### <a name="enable"></a>Habilitar
 Habilita a sequência de tarefas de forma que o cliente possa executá-la. Não é necessário reimplantar uma sequência de tarefas após sua habilitação.  

#### <a name="disable"></a>Desabilitar
 Desativa a sequência de tarefas para que ela não possa ser executada nos computadores. Você pode implantar uma sequência de tarefas desabilitada, mas os computadores não executam a sequência de tarefas até você habilitá-la.  

#### <a name="export"></a>Exportar
 Para saber mais, confira [Exportar e importar sequências de tarefas](#BKMK_ExportImport).

#### <a name="copy"></a>Copiar
 Faz uma cópia da sequência a tarefa selecionada. Essa ação é útil para criar uma nova sequência de tarefas baseada em uma sequência de tarefas existente. 

 Quando você fizer uma cópia de uma sequência de tarefas em uma pasta, a cópia será listada nessa pasta até que você atualize o nó de sequência de tarefas. Após a atualização, a cópia aparecerá na pasta raiz.  

#### <a name="refresh"></a>Atualizar
 Atualiza os detalhes da sequência de tarefas selecionada.

#### <a name="delete"></a>Excluir
 Exclui a sequência de tarefas selecionada.

#### <a name="create-phased-deployment"></a>Criar implantação em fases
 Saiba mais em [Criar implantações em fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).

#### <a name="deploy"></a>Implantar
 Para obter mais informações, consulte [Deploy a task sequence](#BKMK_DeployTS).

#### <a name="distribute-content"></a>Distribuir Conteúdo
 Inicia o Assistente para Distribuir Conteúdo para enviar o conteúdo referenciado aos pontos de distribuição. 

#### <a name="create-prestaged-content-file"></a>Criar Arquivo de Conteúdo de Pré-teste
 Inicia o Assistente para Criar Arquivo de Conteúdo de Pré-Teste para criar um conteúdo de pré-teste de sequência de tarefas. Para obter informações sobre como criar um arquivo de conteúdo pré-teste, consulte [Prestage content (Conteúdo pré-teste)](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).

#### <a name="move"></a>Mover
 Move a sequência de tarefas selecionada para outra pasta no nó **Sequências de Tarefas**. 

#### <a name="set-security-scopes"></a>Definir escopos de segurança
 Selecione os escopos de segurança para a sequência de tarefas selecionada. Para obter mais informações, consulte [Escopos de segurança](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_PlanScope). 

#### <a name="properties"></a>Propriedades
 Saiba mais em [Configurar as propriedades do Centro de Software](#bkmk_prop-general) e [Definir configurações avançadas da sequência de tarefas](#bkmk_prop-advanced).



## <a name="see-also"></a>Consulte também

[Cenários para implantar sistemas operacionais corporativos](scenarios-to-deploy-enterprise-operating-systems.md)
