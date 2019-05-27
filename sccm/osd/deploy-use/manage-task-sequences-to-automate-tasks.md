---
title: Gerenciar sequências de tarefas
titleSuffix: Configuration Manager
description: Crie, edite, implante, importe e exporte sequências de tarefas para gerenciá-las e automatizar tarefas em seu ambiente.
ms.date: 05/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: cbc76a4f2ada16edfbdc139aca77e6a43d3c4a8b
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65082933"
---
# <a name="manage-task-sequences-to-automate-tasks"></a>Gerenciar sequências de tarefas para automatizar tarefas

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use sequências de tarefas para automatizar as etapas em seu ambiente do Configuration Manager. Essas etapas podem implantar uma imagem do sistema operacional em um computador de destino, compilar e capturar uma imagem do sistema operacional de um conjunto de arquivos de instalação do sistema operacional, além de capturar e restaurar as informações de estado do usuário. As sequências de tarefas estão localizadas no console do Configuration Manager. No workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Sequências de Tarefas**. O nó **Sequências de Tarefas**, incluindo as subpastas criadas, é replicado em toda a hierarquia do Configuration Manager. Para obter informações sobre planejamento, consulte [Planning considerations for automating tasks (Considerações de planejamento para automatizar tarefas)](/sccm/osd/plan-design/planning-considerations-for-automating-tasks).  



## <a name="BKMK_CreateTaskSequence"></a> Criar sequências de tarefas  

Crie sequências de tarefas usando o Assistente para Criar Sequência de Tarefas. Este assistente pode criar os seguintes tipos de sequências de tarefas:  

|Tipo de sequência de tarefas|Mais informações|  
|------------------------|----------------------|  
|[Sequência de tarefas para instalar um sistema operacional](create-a-task-sequence-to-install-an-operating-system.md)|Esse tipo de sequência de tarefas cria as etapas para instalar um sistema operacional. Também inclui opções para migrar dados de usuário, incluir atualizações de software e instalar aplicativos.|  
|[Sequência de tarefas para atualizar um sistema operacional](create-a-task-sequence-to-upgrade-an-operating-system.md)|Esse tipo de sequência de tarefas cria as etapas para atualizar um sistema operacional. Também contém opções para incluir atualizações de software e instalar aplicativos.|  
|[Sequência de tarefas para capturar um sistema operacional](create-a-task-sequence-to-capture-an-operating-system.md)|Esse tipo de sequência de tarefas cria as etapas para compilar e capturar um sistema operacional de um computador de referência. É possível incluir atualizações de software e instalar aplicativos no computador de referência antes de capturar a imagem.|  
|[Sequência de tarefas para capturar e restaurar o estado do usuário](create-a-task-sequence-to-capture-and-restore-user-state.md)|Essa sequência de tarefas fornece as etapas a serem adicionadas a uma sequência de tarefas existente para capturar e restaurar dados de estado do usuário.|  
|[Sequência de tarefas personalizada](create-a-custom-task-sequence.md)|Esse tipo de sequência de tarefas não adiciona etapas à sequência de tarefas. Após a criação dessa sequência de tarefas, edite-a e adicione as etapas.|  



## <a name="BKMK_ModifyTaskSequence"></a> Editar  

Modifique uma sequência de tarefas adicionando ou removendo etapas, adicionando ou removendo grupos ou alterando a ordem das etapas. Use o seguinte procedimento para modificar uma sequência de tarefas existente:  

> [!IMPORTANT]  
> Ao editar uma sequência de tarefas criada com o Assistente para Criar Sequência de Tarefas, o nome da etapa pode ser a ação ou o tipo da etapa. Por exemplo, talvez você veja uma etapa com o nome “Particionar Disco 0”, que corresponde à ação de uma etapa do tipo [Format and Partition Disk (Formatar e Particionar Disco)](/sccm/osd/understand/task-sequence-steps#BKMK_FormatandPartitionDisk). Todas as etapas da sequência de tarefas são documentadas por tipo, e não necessariamente por nome da etapa exibida pelo editor.  

### <a name="process-to-edit-a-task-sequence"></a>Processo para editar uma sequência de tarefas  

1. No console do Configuration Manager, acesse o espaço de trabalho **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione o nó **Sequências de Tarefas**.  

2. Na lista **Sequência de Tarefas** , selecione a sequência de tarefas a editar.  

3. Na guia **Início** da faixa de opções, no grupo **Sequência de Tarefas**, selecione **Editar**. Em seguida, realize qualquer uma das seguintes operações:  

    - Para adicionar uma etapa de sequência de tarefas, selecione **Adicionar**, selecione o tipo da etapa e, em seguida, selecione a etapa a ser adicionada. Por exemplo, para adicionar a etapa [Executar Linha de Comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine), selecione **Adicionar**, escolha **Geral** e selecione **Executar Linha de Comando**.  

    - Para adicionar um grupo à sequência de tarefas, selecione **Adicionar** e, em seguida, escolha **Novo Grupo**. Depois de adicionar um grupo, adicione etapas ao grupo.  

    - Para alterar a ordem das etapas e dos grupos na sequência de tarefas, selecione a etapa ou o grupo que deseje reordenar e, em seguida, use os ícones **Mover Item para Cima** ou **Mover Item para Baixo**. Você pode mover apenas uma etapa ou grupo por vez.  

    - Para remover uma etapa ou um grupo, selecione o item desejado e escolha **Remover**.  

4. Selecione **OK** para salvar as alterações e fechar a janela. Selecione **Aplicar** para salvar as alterações e manter o editor de sequência de tarefas aberto.  

Para obter uma lista das etapas de sequência de tarefas disponíveis, consulte [Task sequence steps (Etapas da sequência de tarefas)](/sccm/osd/understand/task-sequence-steps).  



## <a name="bkmk_prop-general"></a> Configurar as propriedades do Centro de Software

Use o procedimento a seguir para configurar os detalhes da sequência de tarefas exibida no Centro de Software. Esses detalhes são apenas para fins informativos.  

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Sequências de Tarefas**.  

2. Selecione a sequência de tarefas a ser editada e depois **Propriedades**.  

3. Na guia **Geral**, as seguintes configurações do Centro de Software estão disponíveis:  

    - **Reinicialização Necessária**: permite que o usuário saiba se uma reinicialização é necessária durante a instalação.  

    - **Tamanho do download (MB)**: especifica quantos megabytes são exibidos no Centro de Software para a sequência de tarefas.  

    - **Tempo de execução estimado (minutos)**: especifica o tempo de execução estimado em minutos exibido no Centro de Software para a sequência de tarefas.  



## <a name="bkmk_prop-advanced"></a> Definir as configurações da sequência de tarefas avançadas

Use o procedimento a seguir para configurar o comportamento da sequência de tarefas no cliente do Gerenciador de Configurações.  

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Sequências de Tarefas**.  

2. Selecione a sequência de tarefas a ser editada e depois **Propriedades**.  

3. Na guia **Avançado**, as seguintes configurações estão disponíveis:  

    - **Executar outro programa primeiro**: selecione esta opção para executar um programa em outro pacote antes da execução da sequência de tarefas. Por padrão, essa caixa de seleção está desmarcada. Não é necessário implantar separadamente o programa que você especifica para executar primeiro.  

        > [!IMPORTANT]
        > Essa configuração aplica-se apenas às sequências de tarefas que são executadas no sistema operacional completo. O Gerenciador de Configurações ignorará esta configuração se a sequência de tarefas for iniciada usando o PXE ou a mídia de inicialização.  

        - **Pacote**: procure o pacote que contém o programa para execução antes dessa sequência de tarefas.  

        - **Programa**: selecione o programa a ser executado antes dessa sequência de tarefas.  

        > [!NOTE]  
        > Se o programa selecionado não é executado em um cliente, a sequência de tarefas não é executada. Se o programa selecionado é executado com êxito, ele não é executado novamente, mesmo se a sequência de tarefas é executada novamente no mesmo cliente.  

    - **Suprimir notificações de sequência de tarefa**: selecione essa opção para ocultar a notificação do sistema **Novos softwares disponíveis**. Você ainda verá o ícone **Novo software** do Centro de Software na área de notificação. Por padrão, essa opção está desabilitada.  

    - **Desabilitar esta sequência de tarefas em computadores onde ela é implantada**: se você selecionar essa opção, o Gerenciador de Configurações desabilitará temporariamente todas as implantações que contêm essa sequência de tarefas. Também remove a sequência de tarefas da lista de implantações disponíveis para execução. A sequência de tarefas não será executada até que você a habilite. Por padrão, essa opção está desabilitada.  

    - **Tempo de execução máximo permitido**: especifica o tempo máximo, em minutos, esperado para a execução da sequência de tarefas no computador de destino. Use um número inteiro igual ou maior que zero. Por padrão, esse valor é de 120 minutos.  

        > [!IMPORTANT]  
        > Se você estiver usando janelas de manutenção para a coleção na qual implanta essa sequência de tarefas, poderá ocorrer um conflito se o **Tempo de execução máximo permitido** for maior do que o tempo da janela de manutenção agendada. Se o tempo de execução máximo for definido como **0**, a sequência de tarefas será iniciada durante a janela de manutenção. Ela continuará sendo executada até ser concluída ou falhar depois que a janela de manutenção for fechada. Como resultado, as sequências de tarefas com um tempo de execução máximo definido como **0** pode ser executado após o término de suas janelas de manutenção. Se você definir o tempo de execução máximo com um período específico (diferente de zero) que excede a duração de qualquer janela de manutenção disponível, essa sequência de tarefas não será executada. Para obter mais informações, consulte [Como usar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).  

        Se você definir o valor como **0**, o Gerenciador de Configurações avaliará o tempo de execução máximo permitido para **12** horas (720 minutos) para monitoramento do progresso. No entanto, a sequência de tarefas será iniciada, desde que a duração da contagem regressiva não exceda o valor da janela de manutenção.  

        > [!NOTE]  
        > Ao atingir o tempo de execução máximo, o Gerenciador de Configurações interromperá a sequência de tarefas se você tiver definido a opção **Executar com direitos administrativos** e não a opção **Permitir que os usuários interajam com este programa**. Se a sequência de tarefas não for interrompida, o Gerenciador de Configurações parará de monitorar a sequência de tarefas após atingir o tempo de execução máximo permitido.  

    - **Usar uma imagem de inicialização**: use a imagem de inicialização selecionada quando a sequência de tarefas for executada. Selecione **Procurar** para selecionar uma imagem de inicialização diferente. Desmarque esta opção para desabilitar o uso da imagem de inicialização selecionada quando a sequência de tarefas for executada.  

    - **Esta sequência de tarefas pode ser executada em qualquer plataforma**: se você selecionar essa opção, o Gerenciador de Configurações não verificará o tipo de plataforma do computador de destino durante a execução da sequência de tarefas. Essa opção é habilitada por padrão.  

    - **Esta sequência de tarefas só pode ser executada nas plataformas de cliente especificadas**: essa opção especifica os processadores, as versões de sistema operacional e os service packs nos quais essa sequência de tarefas pode ser executada. Ao selecionar essa opção, selecione pelo menos uma plataforma na lista. Por padrão, nenhuma plataforma é selecionada. O Configuration Manager usa essas informações quando avalia quais computadores de destino em uma coleção recebem a sequência de tarefas implantada.  

        > [!NOTE]  
        > Quando você executa uma sequência de tarefas na mídia de inicialização ou PXE, o Gerenciador de Configurações ignora essa opção. A sequência de tarefas é executada como se a opção **Este programa pode ser executado em qualquer plataforma** estivesse selecionada.  



## <a name="configure-high-impact-task-sequence-settings"></a>Definir configurações da sequência de tarefas de alto impacto

Configure uma sequência de tarefas como alto impacto e personalize as mensagens recebidas pelos usuários quando eles executam a sequência de tarefas.


### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Definir uma sequência de tarefas como uma sequência de tarefas de alto impacto

Use o procedimento a seguir para definir uma sequência de tarefas como de alto impacto.

> [!NOTE]  
> Qualquer sequência de tarefas que atender a determinadas condições será automaticamente definida como de alto impacto. Para obter mais informações, consulte [Gerenciar implantações de alto risco](/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Sequências de Tarefas**.  

2. Selecione a sequência de tarefas a ser editada e depois **Propriedades**.  

3. Na guia **Notificação do Usuário**, selecione **Essa é uma sequência de tarefas de alto impacto**.  


### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Criar uma notificação personalizada para implantações de alto risco

Use o procedimento a seguir para criar uma notificação personalizada para implantações de alto impacto.

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Sequências de Tarefas**.  

2. Selecione a sequência de tarefas a ser editada e depois **Propriedades**.  

3. Na guia **Notificação do Usuário**, selecione **Usar texto personalizado**.  

    > [!NOTE]
    > Só é possível definir o texto de notificação do usuário quando a opção **Esta é uma sequência de tarefas de alto impacto** for selecionada.  

4. Defina as seguintes configurações:  

    > [!Note]  
    > Cada caixa de texto tem um limite máximo de 255 caracteres.  

    - **Texto do título da notificação do usuário**: especifica o texto azul exibido na notificação do usuário do Centro de Software. Por exemplo, na notificação de usuário padrão, essa seção contém o texto "Confirme se você deseja atualizar o sistema operacional neste computador".  

    - **Texto da mensagem da notificação do usuário**: há três caixas de texto que fornecem o corpo da notificação personalizada. Todas as caixas de texto exigem que você adicione texto.  

        - Primeira caixa de texto: especifica o corpo do texto principal, geralmente, contendo instruções para o usuário. Por exemplo, na notificação de usuário padrão, essa seção contém o texto "A atualização do sistema operacional leva tempo e o computador pode ser reiniciado várias vezes".  

        - Segunda caixa de texto: especifica o texto em negrito abaixo do corpo do texto principal. Por exemplo, na notificação de usuário padrão, essa seção contém o texto "Esta atualização in-loco instala o novo sistema operacional e migra automaticamente seus aplicativos, dados e configurações".  

        - Terceira caixa de texto: especifica a última linha de texto abaixo do texto em negrito. Por exemplo, na notificação de usuário padrão, essa seção contém o texto "Clique em Instalar para começar. Caso contrário, clique em Cancelar”.  

#### <a name="example"></a>Exemplo

Digamos que você defina a seguinte notificação personalizada nas propriedades.

![Guia Notificação de Usuário Personalizada das propriedades da sequência de tarefas](../media/user-notification.png)

A mensagem de notificação a seguir é exibida quando o usuário final abre a instalação no Centro de Software.

![Notificação personalizada de sequência de tarefas para o usuário final no Centro de Software](../media/user-notification-enduser.png)



## <a name="BKMK_DistributeTS"></a> Distribuir conteúdo referenciado  

Para os clientes executarem uma sequência de tarefas que faz referência ao conteúdo, distribua esse conteúdo para pontos de distribuição. A qualquer momento você pode selecionar uma sequência de tarefas e distribuir seu conteúdo para criar uma nova lista de pacotes de referência para distribuição. Se você fizer alterações à sequência de tarefas com o conteúdo atualizado, será necessário redistribuí-lo antes de disponibilizá-lo para os clientes. Use o procedimento a seguir para distribuir o conteúdo que é referenciado por uma sequência de tarefas.  

### <a name="process-to-distribute-referenced-content-to-distribution-points"></a>Processo para distribuir conteúdo referenciado a pontos de distribuição  

1. No console do Configuration Manager, acesse o espaço de trabalho **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione o nó **Sequências de Tarefas**.  

2. Na lista **Sequência de Tarefas** , selecione a sequência de tarefas a distribuir.  

3. Na guia **Início** da faixa de opções, no grupo **Implantação**, selecione **Distribuir Conteúdo**. Essa ação inicia o Assistente para Distribuir Conteúdo.  

4. Na página **Geral**, verifique se a sequência de tarefas correta está selecionada para distribuição.  

5. Na página **Conteúdo**, verifique o conteúdo a ser distribuído, como a imagem de inicialização consultada pela sequência de tarefas.  

6. Na página **Destino de Conteúdo**, especifique as coleções, o ponto de distribuição ou o grupo de pontos de distribuição para os quais deseja distribuir o conteúdo da sequência de tarefas.  

    > [!IMPORTANT]  
    > Se a sequência de tarefas que você selecionou fizer referência ao conteúdo já distribuído a um ponto de distribuição específico, o assistente não listará esse ponto de distribuição.  

7. Conclua o assistente.  

Também é possível pré-configurar o conteúdo referenciado na sequência de tarefas. O Configuration Manager cria um arquivo de conteúdo compactado e pré-configurado que contém os arquivos, as dependências associadas e os metadados associados para o conteúdo selecionado. Depois, importe manualmente o conteúdo em um servidor de site, site secundário ou ponto de distribuição. Para obter mais informações sobre como pré-configurar arquivos de conteúdo, consulte [Prestage content (Pré-configurar conteúdo)](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  



## <a name="BKMK_DeployTS"></a> Implantar  

Para obter mais informações, consulte [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence).

## <a name="BKMK_ExportImport"></a> Exportar e importar  

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


### <a name="process-to-export-task-sequences"></a>Processo para exportar sequências de tarefas  

1. No console do Configuration Manager, acesse o espaço de trabalho **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione o nó **Sequências de Tarefas**.  

2. Na lista **Sequência de Tarefas** , selecione a sequência de tarefas a exportar. Se você selecionar mais de uma sequência de tarefas, todas serão armazenadas em um arquivo de exportação.  

3. Na guia **Início** da faixa de opções, no grupo **Sequência de Tarefas**, selecione **Exportar**. Essa ação inicia o Assistente para Exportar Sequência de Tarefas.  

4. Na página **Geral** , especifique as seguintes configurações:  

    - **Arquivo**: especifique a localização e o nome do arquivo de exportação. Se você inserir o nome do arquivo diretamente, inclua a extensão .zip ao nome do arquivo. Se você procurar o arquivo de exportação, o assistente adicionará automaticamente essa extensão de nome de arquivo.  

    - Se você não quiser exportar dependências da sequência de tarefas, desmarque a opção **Exportar todas as dependências de sequência de tarefas**. Por padrão, o assistente procura todos os objetos relacionados e exporta-os com a sequência de tarefas. Essas dependências incluem qualquer uma para aplicativos.  

    - Se você não quiser copiar o conteúdo da origem do pacote para o local de exportação, desmarque a opção **Exportar todo conteúdo das sequências de tarefas e dependências selecionadas**. Se você selecionar essa opção, o Assistente para Importar Sequência de Tarefas usará o caminho de importação como o novo local da origem do pacote.  

    - **Comentários do administrador**: adicione uma descrição das sequências de tarefas para exportar.  

5. Conclua o assistente.  

O assistente cria os seguintes arquivos de saída:  

- Se você não exportar o conteúdo: um arquivo .zip.  

- Se você exportar o conteúdo: um arquivo .zip e uma pasta chamada *export*_files, em que *export* é o nome do arquivo .zip que contém o conteúdo exportado.  

Se você incluir o conteúdo ao exportar uma sequência de tarefas, copie o arquivo .zip e a pasta *export*_files ou a importação falhará.  


### <a name="process-to-import-task-sequences"></a>Processo para importar sequências de tarefas  

1. No console do Configuration Manager, acesse o espaço de trabalho **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione o nó **Sequências de Tarefas**.  

2. Na guia **Início** da faixa de opções, no grupo **Criar**, selecione **Importar Sequência de Tarefas**. Essa ação inicia o Assistente para Importar Sequência de Tarefas.  

3. Na página **Geral** da faixa de opções, especifique o arquivo .zip exportado.  

4. Na página **Conteúdo do Arquivo** , selecione a ação que você requer para cada objeto que você importar. Essa página mostra todos os objetos encontrados pelo Configuration Manager a serem importados.  

    - Se os objeto nunca foi importado, selecione **Criar Novo**.  

    - Se o objeto foi importado anteriormente, selecione uma das seguintes ações:  

        - **Ignorar Duplicado** (padrão): essa ação não importa o objeto. Em vez disso, o assistente vincula o objeto existente à sequência de tarefas.  

        - **Substituir**: essa ação substitui o objeto existente pelo objeto importado. Para aplicativos, você pode adicionar uma revisão para atualizar o aplicativo existente ou criar um novo aplicativo.  

5. Conclua o assistente.  

Após importar a sequência de tarefas, edite-a para especificar senhas que estavam na sequência de tarefas original. Por motivos de segurança, as senhas não são exportadas.  



## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Retornar à página anterior quando uma sequência de tarefas falhar

Você pode retornar a uma página anterior quando executar uma sequência de tarefas e ocorrer uma falha. Nas versões anteriores do Configuration Manager, era necessário reiniciar a sequência de tarefas em caso de falha. Use o botão **Anterior** nos seguintes cenários:

- Quando um computador é iniciado no Windows PE, a caixa de diálogo de inicialização da sequência de tarefas pode ser exibida antes da sequência estar disponível. Quando você seleciona Próximo neste cenário, a página final da sequência de tarefas é exibida com uma mensagem informando que não há sequências de tarefas disponíveis. Agora, você pode selecionar **Anterior** para procurar novamente as sequências de tarefas disponíveis. Você pode repetir esse processo até que a sequência de tarefas esteja disponível.  

- Quando você executa uma sequência de tarefas, porém pacotes dependentes de conteúdo ainda não estão disponíveis nos pontos de distribuição, a sequência de tarefas falhará. Se o conteúdo ausente ainda não foi distribuído, distribua-o agora. Se preferir, aguarde até que o conteúdo esteja disponível nos pontos de distribuição. Em seguida, selecione **Anterior** para que a sequência de tarefas procure o conteúdo novamente.



## <a name="BKMK_CreateTSVariables"></a> Criar variáveis de sequência de tarefas em computadores e coleções  

Você pode definir variáveis de sequência de tarefas personalizadas para computadores e coleções. As variáveis definidas para um computador são chamadas de variáveis de sequência de tarefas por computador. As variáveis definidas para uma coleção são chamadas de variáveis de sequência de tarefas por coleção. Se houver um conflito, as variáveis por computador prevalecerão sobre as variáveis por coleção. Esse comportamento significa que as variáveis de sequência de tarefas atribuídas a um computador específico têm automaticamente uma prioridade mais alta do que as variáveis atribuídas à coleção que contém o computador.  

Por exemplo, o computador XYZ é membro da coleção ABC. Você pode atribuir MyVariable à coleção ABC com um valor 1. Você pode atribuir MyVariable ao computador XYZ com um valor 2. A variável atribuída ao computador XYZ tem prioridade maior do que a variável atribuída à coleção ABC. Quando uma sequência de tarefas com essa variável é executada no computador XYZ, MyVariable tem um valor 2.

É possível ocultar as variáveis por computador e por coleção de forma que elas não fiquem visíveis no console do Gerenciador de Configurações. Quando você usa a opção **Não exibir este valor no console do Gerenciador de Configurações**, o valor da variável não é exibido no console. A variável ainda pode ser usada pela sequência de tarefas quando ela é executada. Se você não quiser mais ocultar essas variáveis, exclua-as primeiro. Em seguida, redefina as variáveis sem selecionar a opção para ocultá-las.  

> [!WARNING]  
> A configuração para **Não exibir este valor no console do Configuration Manager** aplica-se apenas ao console do Configuration Manager. Os valores das variáveis ainda são exibidos no arquivo de log da sequência de tarefas (SMSTS.LOG).

É possível gerenciar variáveis por computador em um site primário ou em um site de administração central. O Gerenciador de Configurações não dá suporte a mais de 1.000 variáveis atribuídas para um computador.  

> [!IMPORTANT]  
> Ao usar variáveis por coleção para as sequências de tarefas, considere os seguintes comportamentos:  
>
> - As alterações nas coleções sempre são replicadas em toda a hierarquia. As alterações feitas nas variáveis da coleção se aplicam não apenas aos membros do site atual, mas a todos os membros da coleção em toda a hierarquia.  
>  
> - Quando você exclui uma coleção, essa ação também exclui as variáveis da sequência de tarefas configuradas para a coleção.  


### <a name="process-to-create-task-sequence-variables-for-a-computer"></a>Processo para criar variáveis de sequência de tarefas para um computador  

1. No console do Configuration Manager, acesse o workspace **Ativos e Conformidade** e selecione o nó **Dispositivos**.  

2. Selecione o computador de destino e escolha **Propriedades**.  

3. Na caixa de diálogo **Propriedades**, mude para a guia **Variáveis**.  

4. Para cada variável que você deseja criar, selecione o ícone **Novo**. Especifique o **Nome** e o **Valor** da variável de sequência de tarefas. Se você quiser ocultar a variável para que ela não fique visível no console do Gerenciador de Configurações, selecione a opção **Não exibir este valor no console do Gerenciador de Configurações**.  

5. Depois de adicionar todas as variáveis às propriedades do computador, selecione **OK**.  


### <a name="process-to-create-task-sequence-variables-for-a-collection"></a>Processo para criar variáveis de sequência de tarefas para uma coleção  

1. No console do Configuration Manager, acesse o workspace **Ativos e Conformidade** e escolha o nó **Coleções de Dispositivos**. Selecione a coleção de destino e escolha **Propriedades**.  

2. Na caixa de diálogo **Propriedades**, mude para a guia **Variáveis da Coleção**.  

3. Para cada variável que você deseja criar, selecione o ícone **Novo**. Especifique o **Nome** e o **Valor** da variável de sequência de tarefas. Se você quiser ocultar a variável para que ela não fique visível no console do Gerenciador de Configurações, selecione a opção **Não exibir este valor no console do Gerenciador de Configurações**.  

4. Opcionalmente, especifique a prioridade para o Gerenciador de Configurações usar quando as variáveis de sequência de tarefas são avaliadas.  

5. Depois de adicionar todas as variáveis às propriedades da coleção, selecione **OK**.  



## <a name="BKMK_AdditionalActionsTS"></a> Ações adicionais para gerenciar sequências de tarefas  

Você pode gerenciar sequências de tarefas usando ações adicionais ao selecionar uma sequência de tarefas.  

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

Para obter mais informações, consulte [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence).

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

#### <a name="view"></a>Exibir

<!--3633146-->
A partir da versão 1902, a ação **Exibir** em sequências de tarefas é o padrão. Essa ação permite ver as etapas da sequência de tarefas sem bloqueá-la para edição.  


## <a name="see-also"></a>Consulte também

[Cenários para implantar sistemas operacionais corporativos](scenarios-to-deploy-enterprise-operating-systems.md)
