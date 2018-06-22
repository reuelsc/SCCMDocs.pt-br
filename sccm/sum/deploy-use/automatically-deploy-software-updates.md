---
title: Implantar atualizações de software automaticamente
titleSuffix: Configuration Manager
description: Implante automaticamente as atualizações de software adicionando novas atualizações a um grupo de atualização associado a uma implantação ativa ou usando ADRs.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.openlocfilehash: 3b267e122370cc12ecec2f42dcb1dfc62c45fe63
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32353579"
---
#  <a name="BKMK_AutoDeploy"></a> Implantar atualizações de software automaticamente  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Use uma ADR (regra de implantação automática) em vez de adicionar novas atualizações a um grupo de atualização de software existente. Geralmente, você usará ADRs para implantar atualizações de software mensais (conhecidas como atualizações do "Patch de Terça-feira") e para o gerenciamento de atualizações de definição. Se você precisar de ajuda para determinar qual método de implantação é adequado para você, consulte [Implantar atualizações de software](deploy-software-updates.md).

<!--##  <a name="BKMK_AddUpdatesToExistingGroup"></a> Add software updates to a deployed update group  
After you create and deploy a software update group, you can add software updates to the update group and they will be automatically deployed.  

> [!IMPORTANT]  
>  When you add software updates to an existing software update group that has already been deployed, it might take several minutes before the additional software updates are added to the deployment.  

Use the following procedure to add software updates to an existing update group.  

#### To add software updates to an existing software update group  

1.  In the Configuration Manager console, navigate to **Software Library** > **Overview** > **Software Updates**.  

2.  Select the software updates that are to be added to the new software update group.  

3.  On the **Home** tab, in the **Update** group, click **Edit Membership**.  

4.  Select the software update group to which you want to add the software updates as members.  

5.  Click the **Software Update Groups** node to display the software update group.  

6.  Click the software update group, and in the **Home** tab, in the **Update** group, click **Show Members** to display a list of the software updates in the group.  --mstewart this is already doc'd on the SUG page. -->

##  <a name="BKMK_CreateAutomaticDeploymentRule"></a> Criar uma ADR (regra de implantação automática)  
É possível aprovar e implantar automaticamente atualizações de software usando uma ADR. Você pode fazer com que a regra adicione atualizações de software para um novo grupo de atualização de software sempre que a regra for executada ou que ao adicionar atualizações de software a um grupo existente. Quando uma regra é executada e adiciona as atualizações de software a um grupo existente, a regra remove todas as atualizações do grupo e adiciona as atualizações que atendem aos critérios definidos para o grupo. 

> [!WARNING]  
>  Antes de criar uma ADR pela primeira vez, verifique se a sincronização das atualizações de software foi concluída no local. Isso é importante quando você executa o Configuration Manager com um idioma diferente do inglês, porque as classificações de atualização de software são exibidas em inglês antes da primeira sincronização e, em seguida, exibidas no idioma localizado após a conclusão da sincronização da atualização de software. Regras criadas antes de sincronizar atualizações de software podem não funcionar corretamente após a sincronização, porque a cadeia de texto pode não corresponder.  

 Use o procedimento a seguir para criar uma ADR.  

#### <a name="to-create-an-adr"></a>Para criar uma ADR  

1.  No console do Configuration Manager, navegue até **Biblioteca de Software****Visão Geral** > **Atualizações de Software** > **Regras de Implantação Automáticas**.  

2.  Na guia **Início** , no grupo **Criar** , clique em **Criar Regra de Implantação Automática**. O Assistente de Criação de Regra de Implantação Automática é aberto.  

3.  Na página **Geral** , defina as seguintes configurações:  

    -   **Nome**: especifique o nome para a ADR. O nome deve ser exclusivo, deve ajudar a descrever a finalidade da regra e diferenciá-la de outras no site do Configuration Manager.  

    -   **Descrição**: especifique uma descrição para a ADR. A descrição deve fornecer uma visão geral da regra de implantação e outras informações relevantes que ajudam a diferenciar a regra das outras. O campo de descrição é opcional, tem um limite de 256 caracteres e um valor em branco por padrão.  

    -   **Selecionar Modelo de Implantação**: especifique se deseja aplicar um modelo de implantação salvo anteriormente. Configure um modelo de implantação que contém várias propriedades comuns de implantação de atualização que podem ser usadas na criação de ADRs. Esses modelos ajudam a garantir a consistência em implantações semelhantes e economizar tempo.  

         - É possível selecionar entre os modelos internos de implantação de atualização de software do Assistente de Regra de Implantação Automática. O modelo **Atualizações de Definições** fornece configurações comuns a serem usadas durante a implantação das atualizações de definição do software. O modelo **Patch Tuesday** fornece definições comuns a serem usadas ao implantar atualizações de software em um ciclo mensal.  

    -   **Coleção**: especifica a coleção de destino a ser usada na implantação. Os membros da coleção recebem as atualizações de software que são definidas na implantação.  

    -   Decida se deseja adicionar atualizações de software a um grupo de atualização de software novo ou existente. Na maioria dos casos, você provavelmente optará por criar um novo grupo de atualização de software quando a ADR estiver em execução. No entanto, você pode optar por usar um grupo já existente, se a regra for executada em uma programação mais agressiva. Por exemplo, se você executar a regra diária para atualizações de definição, poderá adicionar as atualizações de software a um grupo existente de atualização de software.  

    -   **Habilitar a implantação após a execução desta regra**: especifique se deseja habilitar a implantação de atualização de software após a execução da ADR. Sobre essa especificação, considere o seguinte:  

        -   Quando você habilita a implantação, as atualizações que atendem aos critérios definidos da regra são adicionadas a um grupo de atualização de software. O conteúdo de atualização de software é baixado, conforme necessário. O conteúdo é copiado para os pontos de distribuição especificados e as atualizações são implantadas nos clientes na coleção de destino.  

        -   Quando você não habilita a implantação, as atualizações que atendem aos critérios definidos da regra são adicionadas a um grupo de atualização de software. A política de implantação de atualizações de software é configurada. No entanto, as atualizações não são baixadas nem implantadas nos clientes. Essa situação proporciona o tempo necessário para preparar a implantação das atualizações, verificar se as atualizações que atendem aos critérios são adequadas e, em seguida, permitir a implantação em um momento posterior.  

4.  Na página Configurações de Implantação, defina as seguintes configurações:  

    -   **Usar Wake-on-LAN para ativar clientes para implantações obrigatórias**: especifica se o Wake on LAN deve ser habilitado no prazo para enviar pacotes de ativação para os computadores que exigem uma ou mais atualizações de software na implantação. Todos os computadores que estão no modo de suspensão na hora limite da instalação serão ativados para que a instalação possa ser iniciada. Clientes que estão no modo de suspensão e que não necessitam de atualizações de software na implantação não são iniciados. Por padrão, essa configuração não está habilitada. Antes de usar essa opção, você deve configurar computadores e redes para Wake On LAN. 

    -   **Nível de detalhe**: especifique o nível de detalhe para as mensagens de estado que são relatadas pelos computadores cliente.  

        > [!IMPORTANT]  
        >  Ao implantar atualizações de definição, defina o nível de detalhes como **Apenas erro** para que o cliente relate uma mensagem de estado apenas quando uma atualização de definição falhar. Caso contrário, o cliente relatará um grande número de mensagens de estado que podem afetar o desempenho no servidor do site.  

    -   **Configuração dos termos da licença**: especifique se deseja implantar automaticamente atualizações de software com os termos de licença associados. Algumas atualizações de software incluem termos de licença, como um service pack. Quando você implanta atualizações de software automaticamente, os termos da licença não são exibidos e não há uma opção para aceitá-los. Opte por implantar automaticamente todas as atualizações de software, independentemente dos termos de licença associados, ou apenas implantar atualizações que não têm termos de licença associados.  
        - Para examinar os termos de licença de uma atualização de software, selecione a atualização de software no nó **Todas as Atualizações de Software** do espaço de trabalho **Biblioteca de Software**. Na guia **Página Inicial**, no grupo **Atualização**, clique em **Examinar Licença**.    
        - Para encontrar atualizações de software com os termos de licença associados, adicione a coluna **Termos de Licença** ao painel de resultados no nó **Todas as Atualizações de Software**. Clique no título da coluna para classificar as atualizações de software com os termos de licença.  

5.  Na página Atualizações de Software, configure os critérios para as atualizações de software que a ADR recupera e adiciona ao grupo de atualização de software. O limite para atualizações de software na ADR é de 1.000. Se necessário, filtre o tamanho do conteúdo para atualizações de software em regras de implantação automática. Para obter detalhes, consulte [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/) (Configuration Manager e Serviço do Windows simplificado em sistemas operacionais de nível inferior).


6.  Na página Agendamento de Avaliação, especifique se deseja habilitar a ADR para ser executada em um agendamento. Quando habilitada, clique em **Personalizar** para definir o agendamento recorrente. A configuração do horário de início da agenda é baseada na hora local do computador que executa o console do Configuration Manager.
    - A configuração do horário de início da agenda é baseada na hora local do computador que executa o console do Configuration Manager.
    - A avaliação da ADR pode ser executada três vezes por dia.
    - Nunca defina o agendamento de avaliação com uma frequência que excede o agendamento de sincronização das atualizações de software. O agendamento de sincronização do ponto de atualização de software é exibido para ajudá-lo a determinar a frequência do agendamento de avaliação. 
    - Para executar a ADR manualmente, selecione a regra e clique em **Executar Agora** na guia **Início** do grupo **Regra de Implantação Automática** .
    
       > [!NOTE]  
       >A partir do Configuration Manager versão 1802, as ADRs podem ser agendadas para avaliar o deslocamento de um dia base. Ou seja, se o patch de terça-feira, na verdade, cair na quarta-feira para você, o agendamento de avaliação poderá ser definido para a segunda terça-feira do deslocamento do mês por um dia. <!--1357133-->
       > - Quando o agendamento de avaliação ocorrer com um deslocamento durante a última semana do mês, a avaliação será agendada para o último dia do mês se o deslocamento escolhido estourar para dentro do próximo mês. <!--506731-->

       > ![Deslocamento do agendamento de avaliação personalizado da ADR do dia base](./media/ADR-evaluation-schedule-offset.PNG)

   
7.  Na página Agendamento da Implantação, defina as seguintes configurações:  

    -   **Avaliação do agendamento**: especifique se o Configuration Manager avalia o tempo disponível e os prazos de instalação usando UTC ou a hora local do computador que executa o console do Configuration Manager.  
         - Quando você seleciona a hora local e seleciona **O mais breve possível** para o **Tempo disponível do software** ou o **Prazo de instalação**, a hora atual no computador que executa o console do Configuration Manager é usada para avaliar quando as atualizações estarão disponíveis ou quando serão instaladas em um cliente. Se o cliente estiver em um fuso horário diferente, essas ações ocorrerão quando o tempo do cliente atingir o tempo de avaliação.  

    -   **Tempo disponível do software**: selecione uma das configurações a seguir para especificar quando as atualizações de software estão disponíveis aos clientes:  

        -   **Assim que possível**: disponibiliza as atualizações de software incluídas na implantação aos computadores cliente o mais breve possível. Quando você cria a implantação com essa configuração selecionada, o Configuration Manager atualiza a política de cliente. No próximo ciclo de sondagem da política do cliente, os clientes reconhecem a implantação e podem obter as atualizações disponíveis para instalação.  

        -   **Hora específica**: disponibiliza as atualizações de software incluídas na implantação aos computadores cliente em uma data e hora específicas. Quando você cria a implantação com essa configuração habilitada, o Configuration Manager atualiza a política de cliente. Em seguida, no próximo ciclo de sondagem de política do cliente, os clientes são informados da implantação. No entanto, as atualizações de software na implantação não estão disponíveis para instalação até após a data e hora configuradas.  

    -   **Prazo de instalação**: selecione uma das seguintes configurações para especificar o prazo de instalação das atualizações de software na implantação:  

        -   **O mais breve possível**: selecione essa configuração para instalar automaticamente as atualizações de software na implantação o mais breve possível.  

        -   **Horário específico**: selecione essa configuração para instalar automaticamente as atualizações de software na implantação, em uma data e hora específica. O Configuration Manager determina o prazo para instalar as atualizações de software, adicionando o intervalo **Horário específico** configurado para o **Tempo disponível do software**.  

            - A hora limite da instalação real é a hora limite exibida, mais um período aleatório de até duas horas. A aleatoriedade reduz o impacto potencial de que os computadores cliente na coleção instalem atualizações na implantação ao mesmo tempo.  
          
             - É possível configurar a definição do cliente **Agente de Computador** , **Desativar data limite aleatória** para desabilitar o atraso de aleatoriedade das atualizações de software necessárias. Para obter mais informações, consulte [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

8. Na página Experiência do Usuário, defina as seguintes configurações:  

    -   **Notificações ao usuário**: especifique se quer exibir notificações das atualizações de software no Centro de Software no computador cliente no **Tempo disponível do software** configurado e se deseja exibir as notificações ao usuário nos computadores cliente.  

    -   **Comportamento do prazo**: especifique o comportamento que deve ocorrer quando o prazo for alcançado para a implantação de atualização do software. Especifique se deseja instalar as atualizações de software na implantação. Especifique também se o sistema deve ser reiniciado após a instalação da atualização de software, independentemente de uma janela de manutenção configurada. Para obter mais informações sobre janelas de manutenção, consulte [Como usar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamento de reinicialização do dispositivo**: especifique se uma reinicialização do sistema em servidores e estações de trabalho deve ser suprimida, caso uma reinicialização seja necessária para concluir a instalação da atualização.  

        > [!WARNING]  
        >  A supressão das reinicializações do sistema pode ser útil em ambientes de servidor ou para casos em que você não quer que os computadores que estão instalando as atualizações de software reiniciem por padrão. No entanto, isso pode deixar os computadores em um estado inseguro, ao passo que permitir uma reinicialização forçada ajuda a garantir a conclusão imediata da instalação da atualização de software.  

    -   **Manuseio de filtro de gravação para dispositivos Windows Embedded**: ao implantar atualizações de software em dispositivos Windows Embedded com filtro de gravação habilitado, é possível especificar que a atualização de software seja instalada na sobreposição temporária e que as alterações sejam confirmadas mais tarde, na data limite da instalação ou durante uma janela de manutenção. Ao confirmar as alterações na data limite da instalação ou durante uma janela de manutenção, é necessário reinicializar. Dessa forma, as alterações permanecem no dispositivo.  

           -  Ao implantar uma atualização de software em um dispositivo Windows Embedded, verifique se o dispositivo é membro de uma coleção que tem uma janela de manutenção configurada.  

    - **Comportamento de reavaliação da implantação de atualizações de software na reinicialização**: selecione essa configuração para definir as implantações de atualização de software para que os clientes executem uma verificação de conformidade das atualizações de software imediatamente depois que um cliente instalar atualizações de software e for reiniciado. Essa configuração permite que o cliente verifique se há atualizações adicionais que se tornam aplicáveis depois que o cliente é reiniciado e, em seguida, instala-as durante a mesma janela de manutenção.

9. Na página Alertas, configure como o Configuration Manager e o System Center Operations Manager gerarão alertas para essa implantação. Você pode verificar os alertas de atualizações de software recentes no nó **Atualizações de Software** no espaço de trabalho **Biblioteca de Software** .  

10. Na página Configurações de Download, defina as seguintes configurações:  

    - Especifique se os clientes devem baixar e instalar as atualizações quando estão conectados a uma rede lenta ou usando um local de conteúdo de fallback.  

    - Especifique se os clientes devem baixar e instalar as atualizações de software de um ponto de distribuição de fallback quando o conteúdo das atualizações de software não está disponível em um ponto de distribuição preferencial.  

    - **Permitir que os clientes compartilhem conteúdo com outros clientes na mesma sub-rede**: especifique se deseja habilitar o uso do BranchCache para downloads de conteúdo. Para obter mais informações sobre o BranchCache, veja [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Se as atualizações de software não estiverem disponíveis no ponto de distribuição nos grupos do site, atuais ou vizinhos, baixar o conteúdo do Microsoft Update**: selecione essa configuração para que os clientes conectados à intranet baixem as atualizações de software do Microsoft Update, caso as atualizações de software não estejam disponíveis nos pontos de distribuição. Os clientes baseados na Internet sempre podem ir para o Microsoft Update para obter o conteúdo das atualizações de software.

    - Especifique se os clientes têm permissão para baixar após o prazo de uma instalação quando usam conexão de Internet limitada. Provedores de Internet ocasionalmente cobram por quantidade de dados que você envia e recebe quando está em uma conexão de Internet limitada.  

    > [!NOTE]  
    >  Os clientes solicitam o local do conteúdo de um ponto de gerenciamento de atualizações de software em uma implantação. O comportamento do download depende de como você configurou o ponto de distribuição, o pacote de implantação e as configurações desta página. Para obter mais informações, consulte [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

11. Na página do Pacote de Implantação, selecione um pacote de implantação existente ou configure as seguintes definições para criar um novo pacote de implantação:  

    1.  **Nome**: especifique o nome do pacote de implantação. Use um nome exclusivo que descreve o conteúdo do pacote. Ele é limitado a 50 caracteres.  

    2.  **Descrição**: especifique uma descrição que forneça informações sobre o pacote de implantação. A descrição é limitada a 127 caracteres.  

    3.  **Origem do pacote**: especifica o local dos arquivos de origem de atualização do software.  Digite um caminho de rede para o local de origem, por exemplo, **\\\servidor\nome do compartilhamento\caminho**ou clique em **Procurar** para encontrar o local na rede. Crie a pasta compartilhada para os arquivos de origem do pacote de implantação antes de ir para a próxima página.  

        - O local de origem do pacote de implantação especificado não pode ser usado por outro pacote de implantação de software.
        - Será possível alterar o local de origem do pacote nas propriedades do pacote de implantação depois que o Configuration Manager criar o pacote de implantação. Mas se você fizer isso, precisará primeiro copiar o conteúdo da origem do pacote original para o novo local de origem do pacote  
        -  A conta do computador Provedor de SMS e o usuário que estiver executando o assistente para baixar as atualizações de software deverão ter permissões NTFS de **Gravação** no local de download. É necessário restringir o acesso ao local de download com atenção, para reduzir o risco de ataques de adulteração nos arquivos de origem de atualização de software.  
       

    4.  **Prioridade de envio**: especifique a prioridade de envio do pacote de implantação. O Configuration Manager usa a prioridade de envio do pacote de implantação quando envia o pacote para pontos de distribuição. Os pacotes de implantação são enviados por ordem de prioridade: Alta, Média, ou Baixa. Pacotes com prioridades idênticas são enviados na ordem em que foram criados. Se não houver uma lista de pendências, o pacote será processado imediatamente, não importando qual seja a prioridade.  

12. Na página Pontos de Distribuição, especifique os pontos de distribuição ou grupos de pontos de distribuição que irão hospedar os arquivos de atualização de software. Para obter mais informações sobre pontos de distribuição, consulte [Configurações de ponto de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). A página está disponível somente quando você cria um novo pacote de implantação de atualização de software.
  

13. Na página Local de Download, especifique se deseja baixar os arquivos de atualização de software da Internet ou de sua rede local. Defina as seguintes configurações:  

    -   **Baixe as atualizações de software da Internet**: selecione essa configuração para baixar as atualizações de software de um local específico na Internet. Essa configuração é habilitada por padrão.  

    -   **Baixar atualizações de software de um local na rede local**: selecione essa configuração para baixar atualizações de software de um diretório local ou pasta compartilhada. Essa configuração é útil quando o computador que executa o assistente não tem acesso à Internet. Qualquer computador com acesso à Internet pode baixar preliminarmente atualizações de software e armazená-las em um local na rede local que é acessível do computador que executa o assistente.  

14. Na página Seleção de Idioma, selecione os idiomas para os quais as atualizações de software selecionadas são baixadas. As atualizações de software só serão baixadas se estiverem disponíveis nos idiomas selecionados. As atualizações de software que não são específicas a um idioma são sempre baixadas. Por padrão, o assistente seleciona os idiomas que você configurou nas propriedades de ponto de atualização de software. Pelo menos um idioma deve ser selecionado para ir para a próxima página. Quando você selecionar apenas os idiomas não compatíveis com uma atualização de software, o download falhará para a atualização.  

15. Na página Resumo, verifique as configurações. Para salvar as configurações em um modelo de implantação, clique em **Salvar Como Modelo**. Insira um nome e selecione as configurações que deseja incluir no modelo. Em seguida, clique em **Salvar**. Para alterar uma configuração, clique na página do assistente associado e altere a configuração.  
    -  O nome do modelo pode consistir em caracteres ASCII alfanuméricos, bem como em **\\** (barra invertida) ou **‘** (aspa simples).  

16. Clique em **Avançar** para criar a ADR.  

 Depois de concluir o assistente, a ADR será executada. Isso adicionará as atualizações de software que atendem aos critérios especificados a um grupo de atualização de software. Em seguida, a ADR baixa as atualizações na biblioteca de conteúdo no servidor do site e as distribui para os pontos de distribuição configurados. A ADR então implanta o grupo de atualização de software nos clientes da coleção de destino.  

##  <a name="BKMK_AddDeploymentToADR"></a> Adicionar uma nova implantação a uma ADR existente  
 Depois de criar uma ADR, é possível adicionar outras implantações à regra. Isso pode ajudá-lo a gerenciar a complexidade de implantar diferentes atualizações em diferentes coleções. Cada nova implantação tem a gama completa de funcionalidade e experiência de monitoramento da implantação.  

#### <a name="to-add-a-new-deployment-to-an-existing-adr"></a>Para adicionar uma nova implantação a uma ADR existente  

1.  No console do Configuration Manager, navegue até **Biblioteca de Software** > **Visão Geral** > **Atualizações de Software** > **Regras de Implantação Automáticas** e selecione a regra desejada.  

2.  Na guia **Início** , no grupo **Regra de Implantação Automática** , clique em **Adicionar Implantação**. O Assistente para Adicionar de Implantação.  

3.  Na página **Coleção** , defina as seguintes configurações:  

    -   **Coleção**: especifica a coleção de destino a ser usada na implantação. Os membros da coleção recebem as atualizações de software que são definidas na implantação.  

    -   **Habilitar a implantação após a execução desta regra**: especifique se deseja habilitar a implantação de atualização de software após a execução da ADR. Sobre essa especificação, considere o seguinte:  

        -   Quando você habilita a implantação, as atualizações que atendem aos critérios definidos da regra são adicionadas a um grupo de atualização de software. O conteúdo de atualização de software é baixado, conforme necessário. O conteúdo é copiado para os pontos de distribuição especificados e as atualizações são implantadas nos clientes na coleção de destino.  

        -  Quando você não habilita a implantação, as atualizações que atendem aos critérios definidos da regra são adicionadas a um grupo de atualização de software. A política de implantação de atualizações de software é configurada. No entanto, as atualizações não são baixadas nem implantadas nos clientes. Essa situação proporciona o tempo necessário para preparar a implantação das atualizações, verificar se as atualizações que atendem aos critérios são adequadas e, em seguida, permitir a implantação em um momento posterior.  

4.  Na página Configurações de Implantação, defina as seguintes configurações:  

    -   **Usar Wake-on-LAN para ativar clientes para implantações obrigatórias**: especifica se o Wake on LAN deve ser habilitado no prazo para enviar pacotes de ativação para os computadores que exigem uma ou mais atualizações de software na implantação. Todos os computadores que estão no modo de suspensão na hora limite da instalação serão ativados para que a instalação possa ser iniciada. Clientes que estão no modo de suspensão e que não necessitam de atualizações de software na implantação não são iniciados. Por padrão, essa configuração não está habilitada. Antes de usar essa opção, você deve configurar computadores e redes para Wake On LAN.  

    -   **Nível de detalhe**: especifique o nível de detalhe para as mensagens de estado que são relatadas pelos computadores cliente.  

        > [!IMPORTANT]  
        >  Ao implantar atualizações de definição, defina o nível de detalhes como **Apenas erro** para que o cliente relate uma mensagem de estado apenas quando uma atualização de definição deixar de ser entregue ao cliente. Caso contrário, o cliente relatará um grande número de mensagens de estado que podem afetar o desempenho no servidor do site.  

5.  Na página Agendamento da Implantação, defina as seguintes configurações:  

    -   **Avaliação do agendamento**: especifique se o Configuration Manager avalia o tempo disponível e os prazos de instalação usando UTC ou a hora local do computador que executa o console do Configuration Manager.  

           -  Quando você seleciona a hora local e seleciona **O mais breve possível** para o **Tempo disponível do software** ou o **Prazo de instalação**, a hora atual no computador que executa o console do Configuration Manager é usada para avaliar quando as atualizações estarão disponíveis ou quando serão instaladas em um cliente. Se o cliente estiver em um fuso horário diferente, essas ações ocorrerão quando o tempo do cliente atingir o tempo de avaliação.  

    -   **Tempo disponível do software**: selecione uma das configurações a seguir para especificar quando as atualizações de software estão disponíveis aos clientes:  

        -   **O mais breve possível**: selecione essa configuração para disponibilizar as atualizações de software incluídas na implantação aos computadores cliente o mais breve possível. Quando você cria a implantação com essa configuração selecionada, o Configuration Manager atualiza a política de cliente. No próximo ciclo de sondagem da política do cliente, os clientes reconhecem a implantação e podem obter as atualizações disponíveis para instalação.  

        -   **Hora específica**: disponibiliza as atualizações de software incluídas na implantação aos computadores cliente em uma data e hora específicas. Quando você cria a implantação com essa configuração habilitada, o Configuration Manager atualiza a política de cliente. Em seguida, no próximo ciclo de sondagem de política do cliente, os clientes são informados da implantação. No entanto, as atualizações de software na implantação não estão disponíveis para instalação até após a data e hora configuradas. 

    -   **Prazo de instalação**: selecione uma das seguintes configurações para especificar o prazo de instalação das atualizações de software na implantação:  

        -   **O mais breve possível**: selecione essa configuração para instalar automaticamente as atualizações de software na implantação o mais breve possível.  

        -   **Horário específico**: selecione essa configuração para instalar automaticamente as atualizações de software na implantação, em uma data e hora específica. O Configuration Manager determina o prazo para instalar as atualizações de software, adicionando o intervalo **Horário específico** configurado para o **Tempo disponível do software**.  

               - A hora limite da instalação real é a hora limite exibida, mais um período aleatório de até duas horas. Isso reduz o impacto potencial de que os computadores cliente na coleção instalem atualizações na implantação ao mesmo tempo.  
              - É possível configurar a definição do cliente **Agente de Computador** , **Desativar data limite aleatória** para desabilitar o atraso de aleatoriedade das atualizações de software necessárias. Para obter mais informações, consulte [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

6.  Na página Experiência do Usuário, defina as seguintes configurações:  

    -   **Notificações ao usuário**: especifique se quer exibir notificações das atualizações de software no Centro de Software no computador cliente no **Tempo disponível do software** configurado e se deseja exibir as notificações ao usuário nos computadores cliente.  

    -   **Comportamento do prazo**: especifique o comportamento que deve ocorrer quando o prazo for alcançado para a implantação de atualização do software. Especifique se deseja instalar as atualizações de software na implantação. Especifique também se o sistema deve ser reiniciado após a instalação da atualização de software, independentemente de uma janela de manutenção configurada. Para obter mais informações sobre janelas de manutenção, consulte [Como usar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamento de reinicialização do dispositivo**: especifique se uma reinicialização do sistema em servidores e estações de trabalho deve ser suprimida, caso uma reinicialização seja necessária para concluir a instalação da atualização.  
 
           > [!WARNING]  
           >  A supressão das reinicializações do sistema pode ser útil em ambientes de servidor ou para casos em que você não quer que os computadores que estão instalando as atualizações de software reiniciem por padrão. No entanto, isso pode deixar os computadores em um estado inseguro, ao passo que permitir uma reinicialização forçada ajuda a garantir a conclusão imediata da instalação da atualização de software.  

    - **Manuseio de filtro de gravação para dispositivos Windows Embedded**: ao implantar atualizações de software em dispositivos Windows Embedded com filtro de gravação habilitado, é possível especificar que a atualização de software seja instalada na sobreposição temporária e que as alterações sejam confirmadas mais tarde, na data limite da instalação ou durante uma janela de manutenção. Ao confirmar as alterações na data limite da instalação ou durante uma janela de manutenção, é necessário reinicializar. Dessa forma, as alterações permanecem no dispositivo.  

        - Ao implantar uma atualização de software em um dispositivo Windows Embedded, verifique se o dispositivo é membro de uma coleção com uma janela de manutenção configurada.  

7.  Na página Alertas, configure como o Configuration Manager e o System Center Operations Manager gerarão alertas para essa implantação. Você pode verificar os alertas de atualizações de software recentes no nó **Atualizações de Software** no espaço de trabalho **Biblioteca de Software** .  

8. Na página Configurações de Download, defina as seguintes configurações:  

    - Especifique se os clientes devem baixar e instalar as atualizações de software quando estão conectados a uma rede lenta ou usando um local de conteúdo de fallback.  

    - Especifique se o cliente deve baixar e instalar as atualizações de software por meio de um ponto de distribuição de fallback quando o conteúdo das atualizações de software não está disponível ou de um ponto de distribuição preferencial.  

    - **Permitir que os clientes compartilhem conteúdo com outros clientes na mesma sub-rede**: especifique se deseja habilitar o uso do BranchCache para downloads de conteúdo. Para obter mais informações sobre o BranchCache, veja [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Se as atualizações de software não estiverem disponíveis no ponto de distribuição nos grupos do site, atuais ou vizinhos, baixar o conteúdo do Microsoft Update**: selecione essa configuração para que os clientes conectados à intranet baixem as atualizações de software do Microsoft Update, caso as atualizações de software não estejam disponíveis nos pontos de distribuição. Os clientes baseados na Internet sempre podem ir para o Microsoft Update para obter o conteúdo das atualizações de software.

    - Especifique se os clientes têm permissão para baixar após o prazo de uma instalação quando usam conexão de Internet limitada. Provedores de Internet ocasionalmente cobram por quantidade de dados que você envia e recebe quando está em uma conexão de Internet limitada.  

    > [!NOTE]  
    > Os clientes solicitam o local do conteúdo de um ponto de gerenciamento de atualizações de software em uma implantação. O comportamento do download depende de como você configurou o ponto de distribuição, o pacote de implantação e as configurações desta página. Para obter mais informações, consulte [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

Para obter mais informações sobre o processo de implantação, veja [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).

## <a name="next-steps"></a>Próximas etapas
[Monitorar atualizações de software](monitor-software-updates.md)
