---
title: "Implantar atualizações de software automaticamente | Configuration Manager"
description: "Implante automaticamente as atualizações de software adicionando novas atualizações a um grupo de atualização associado a uma implantação ativa ou usando ADRs."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 133f29aa3f515054b23ba70f1a1dfd3eedaa56c8

---

#  <a name="a-namebkmkautodeploya-automatically-deploy-software-updates"></a><a name="BKMK_AutoDeploy"></a> Implantar atualizações de software automaticamente  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Você pode implantar automaticamente as atualizações de software adicionando novas atualizações a um grupo de atualização que tenha uma implantação ativa ou usando ADR (regra de implantação automática). Geralmente, as ADRs são usadas para implantar atualizações de software mensais (geralmente conhecidas como "Patch Tuesday") e para o gerenciamento de atualizações de definições. Se você precisar de ajuda para determinar qual método de implantação é adequado para você, consulte [Implantar atualizações de software](deploy-software-updates.md)

##  <a name="a-namebkmkaddupdatestoexistinggroupa-add-software-updates-to-a-deployed-update-group"></a><a name="BKMK_AddUpdatesToExistingGroup"></a> Adicionar atualizações de software a um grupo de atualização implantado  
Depois de criar e implantar um grupo de atualização de software, você pode adicionar novas atualizações ao grupo e elas serão implantadas automaticamente.  

> [!IMPORTANT]  
>  Quando você adiciona atualizações de software a um grupo de atualização de software existente que já foi implantado, pode levar vários minutos antes que as atualizações sejam adicionadas à implantação.  

Use o procedimento a seguir para adicionar atualizações de software a um grupo de atualização existente.  

#### <a name="to-add-software-updates-to-an-existing-software-update-group"></a>Para adicionar atualizações de software a um grupo de atualização de software existente  

1.  No console do Configuration Manager, navegue até **Biblioteca de Software** > **Visão Geral** > **Atualizações de Software**.  

2.  Selecione as atualizações de software a serem adicionadas ao novo grupo de atualização de software.  

3.  Na guia **Início** , no grupo **Atualizar** , clique em **Editar Associação**.  

4.  Selecione o grupo de atualização de software ao qual você deseja adicionar as atualizações de software como membros.  

5.  Clique no nó **Grupos de Atualização de Software** para exibir o grupo de atualização de software.  

6.  Clique no grupo de atualização de software e, na guia **Início** , no grupo **Atualizar** , clique em **Mostrar Membros** para exibir uma lista de atualizações de software no grupo.  

##  <a name="a-namebkmkcreateautomaticdeploymentrulea-create-an-automatic-deployment-rule-adr"></a><a name="BKMK_CreateAutomaticDeploymentRule"></a> Criar uma ADR (regra de implantação automática)  
É possível aprovar e implantar automaticamente atualizações de software usando uma ADR. Você pode fazer com que a regra adicione atualizações de software para um novo grupo de atualização de software sempre que a regra for executada ou que ao adicionar atualizações de software a um grupo existente. Quando uma regra é executada e adiciona as atualizações de software a um grupo existente, a regra remove todas as atualizações de software do grupo e adiciona as atualizações de software que atendem aos critérios que você definir para o grupo. Para executar uma ADR para encontrar atualizações de software recém-liberadas diariamente e implantá-las nos clientes, por exemplo, é necessário escolher a opção para criar um novo grupo de atualização de software em vez de adicionar as atualizações de software a um grupo existente.  

> [!WARNING]  
>  Antes de criar uma ADR pela primeira vez, verifique se a sincronização das atualizações de software foi concluída no local. Isso é especialmente importante quando você executa o Configuration Manager com um idioma diferente do inglês, porque classificações de atualização de software são exibidas em inglês antes da primeira sincronização, e depois exibidas no idioma traduzido após a conclusão da sincronização da atualização de software. Regras criadas antes de sincronizar atualizações de software podem não funcionar corretamente após a sincronização, porque a cadeia de texto pode não corresponder.  

 Use o procedimento a seguir para criar uma ADR.  

#### <a name="to-create-an-adr"></a>Para criar uma ADR  

1.  No console do Configuration Manager, navegue até **Biblioteca de Software****Visão Geral** > **Atualizações de Software** > **Regras de Implantação Automáticas**.  

2.  Na guia **Início** , no grupo **Criar** , clique em **Criar Regra de Implantação Automática**. O Assistente de Criação de Regra de Implantação Automática é aberto.  

3.  Na página **Geral** , defina as seguintes configurações:  

    -   **Nome**: especifique o nome para a ADR. O nome deve ser exclusivo, deve ajudar a descrever a finalidade da regra e diferenciá-la de outras no site do Configuration Manager.  

    -   **Descrição**: especifique uma descrição para a ADR. A descrição deve fornecer uma visão geral da regra de implantação e qualquer outra informação relevante que ajude a identificá-la e a diferenciá-la de outras no site do Configuration Manager. O campo de descrição é opcional, tem um limite de 256 caracteres e um valor em branco por padrão.  

    -   **Selecionar Modelo de Implantação**: especifique se deseja aplicar um modelo de implantação salvo anteriormente. É possível configurar um modelo de implantação para conter várias propriedades comuns da implantação de atualização de software que podem ser usadas ​​na criação de ADRs. Esses modelos ajudam a garantir a consistência em implantações semelhantes e economizar tempo.  

         É possível selecionar entre os modelos internos de implantação de atualização de software do Assistente de Regra de Implantação Automática. O modelo **Atualizações de Definições** fornece configurações comuns a serem usadas durante a implantação das atualizações de definição do software. O modelo **Patch Tuesday** fornece definições comuns a serem usadas ao implantar atualizações de software em um ciclo mensal.  

    -   **Coleção**: especifica a coleção de destino a ser usada na implantação. Os membros da coleção recebem as atualizações de software que são definidas na implantação.  

    -   Decida se deseja adicionar atualizações de software a um grupo de atualização de software novo ou existente. Na maioria dos casos, você provavelmente optará por criar um novo grupo de atualização de software quando a ADR estiver em execução. No entanto, você pode optar por usar um grupo já existente, se a regra for executada em uma programação mais agressiva. Por exemplo, se você executar a regra diária para atualizações de definição, poderá adicionar as atualizações de software a um grupo existente de atualização de software.  

    -   **Habilitar a implantação após a execução desta regra**: especifique se deseja habilitar a implantação de atualização de software após a execução da ADR. Sobre essa especificação, considere o seguinte:  

        -   Quando você habilita a implantação, as atualizações de software que atendem aos critérios definidos na regra são adicionadas a um grupo de atualização de software, o conteúdo da atualização de software é baixado conforme necessário, o conteúdo é copiado nos pontos de distribuição especificados e as atualizações de software são implantadas nos clientes na coleção de destino.  

        -   Quando você não habilita a implantação, as atualizações de software que atendem aos critérios definidos na regra são adicionadas a um grupo de atualização de software e a política de implantação de atualizações de software é configurada, mas as atualizações não são baixadas nem implantadas nos clientes. Essa situação fornece-lhe o tempo necessário para se preparar para implantar as atualizações de software, verificar se as atualizações que atendem aos critérios são adequadas e permitir a implantação em um momento posterior.  

4.  Na página Configurações de Implantação, defina as seguintes configurações:  

    -   **Usar Wake-on-LAN para ativar clientes para implantações obrigatórias**: especifica se o Wake on LAN deve ser habilitado no prazo para enviar pacotes de ativação para os computadores que exigem uma ou mais atualizações de software na implantação. Todos os computadores que estão no modo de suspensão na hora do prazo da instalação serão ativados para que a instalação da atualização de software seja iniciada. Clientes que estão no modo de suspensão e que não necessitam de atualizações de software na implantação não são iniciados. Por padrão, essa configuração não está habilitada.  

        > [!WARNING]  
        >  Antes de usar essa opção, você deve configurar computadores e redes para Wake On LAN.  

    -   **Nível de detalhe**: especifique o nível de detalhe para as mensagens de estado que são relatadas pelos computadores cliente.  

        > [!IMPORTANT]  
        >  Ao implantar atualizações de definição, defina o nível de detalhes como **Apenas erro** para que o cliente relate uma mensagem de estado apenas quando uma atualização de definição deixar de ser entregue ao cliente. Caso contrário, o cliente relatará um grande número de mensagens de estado que podem afetar o desempenho no servidor do site.  

    -   **Configuração dos termos da licença**: especifique se deseja implantar automaticamente atualizações de software com os termos de licença associados. Algumas atualizações de software incluem termos de licença, como um service pack. Quando você implanta atualizações de software automaticamente, os termos da licença não são exibidos e não há uma opção para aceitá-los. Você pode optar por implantar automaticamente todas as atualizações de software, independentemente dos termos de licença associados ou apenas implantar atualizações de software que não têm termos de licença associados.  

        > [!WARNING]  
        >  Para revisar os termos da licença de uma atualização de software, você pode selecionar a atualização no nó **Todas as Atualizações de Software** do espaço de trabalho **Biblioteca de Softwares** e depois, na guia **Início** , no grupo **Atualizar** , clique em **Revisar Licença**.  
        >   
        >  Para encontrar atualizações de software com os termos de licença associados, você pode adicionar a coluna **Termos da Licença** ao painel de resultados no nó **Todas as Atualizações de Software** e, em seguida, clique no cabeçalho da coluna para classificar as atualizações de software, com os termos da licença.  

5.  Na página Atualizações de Software, configure os critérios para as atualizações de software que a ADR recupera e adiciona ao grupo de atualização de software.  

    > [!IMPORTANT]  
    >  O limite para atualizações de software na ADR é de 1.000. Para garantir que os critérios que você especificar nesta página recuperem menos de 1.000 atualizações de software, considere definir os mesmos critérios no nó **Todas as Atualizações de Software** no espaço de trabalho **Biblioteca de Software** .  

6.  Na página Agendamento de Avaliação, especifique se deseja habilitar a ADR para ser executada em um agendamento. Quando habilitada, clique em **Personalizar** para definir o agendamento recorrente.  

    > [!IMPORTANT]  
    >  A agenda de sincronização do ponto de atualização de software é exibida para ajudar a determinar a frequência da agenda de avaliação. Você nunca deve definir a agenda de avaliação com uma frequência que exceda a agenda de sincronização de atualizações de software. A configuração do horário de início da agenda é baseada na hora local do computador que executa o console do Configuration Manager.  

    > [!NOTE]  
    >  Para executar a ADR manualmente, selecione a regra e clique em **Executar Agora** na guia **Início** do grupo **Regra de Implantação Automática** . Antes de executar a ADR manualmente, verifique se a sincronização das atualizações de software foi executada desde a última vez que a regra foi executada.  

    > [!IMPORTANT]  
    >  A avaliação da ADR pode ser executada três vezes por dia.  

7.  Na página Agendamento da Implantação, defina as seguintes configurações:  

    -   **Avaliação do agendamento**: especifique se o Configuration Manager avalia o tempo disponível e os prazos de instalação usando UTC ou a hora local do computador que executa o console do Configuration Manager.  

        > [!NOTE]  
        >  Quando você seleciona a hora local e seleciona **O mais breve possível** para o **Tempo disponível do software** ou o **Prazo de instalação**, a hora atual no computador que executa o console do Configuration Manager é usada para avaliar quando as atualizações estarão disponíveis ou quando serão instaladas em um cliente. Se o cliente estiver em um fuso horário diferente, essas ações ocorrerão quando o tempo do cliente atingir o tempo de avaliação.  

    -   **Tempo disponível do software**: selecione uma das configurações a seguir para especificar quando as atualizações de software estão disponíveis aos clientes:  

        -   **O mais breve possível**: selecione essa configuração para disponibilizar as atualizações de software incluídas na implantação aos computadores cliente o mais breve possível. Quando você cria a implantação com essa configuração selecionada, o Configuration Manager atualiza a política de cliente. Então, no próximo ciclo de sondagem da política do cliente, os clientes ficam informados da implantação e podem obter as atualizações disponíveis para instalação.  

        -   **Horário específico**: selecione essa configuração para disponibilizar as atualizações de software incluídas na implantação aos computadores cliente, em uma data e hora específica. Quando você cria a implantação com essa configuração habilitada, o Configuration Manager atualiza a política de cliente. Em seguida, no próximo ciclo de sondagem de política do cliente, os clientes são informados da implantação. No entanto, as atualizações de software na implantação não estão disponíveis para instalação até após a data e hora configuradas.  

    -   **Prazo de instalação**: selecione uma das seguintes configurações para especificar o prazo de instalação das atualizações de software na implantação:  

        -   **O mais breve possível**: selecione essa configuração para instalar automaticamente as atualizações de software na implantação o mais breve possível.  

        -   **Horário específico**: selecione essa configuração para instalar automaticamente as atualizações de software na implantação, em uma data e hora específica. O Configuration Manager determina o prazo para instalar as atualizações de software, adicionando o intervalo **Horário específico** configurado para o **Tempo disponível do software**.  

        > [!NOTE]  
        >  O prazo real da instalação é o prazo exibido, mais um período de tempo aleatório de até 2 horas. Isso reduz o impacto potencial de todos os computadores cliente na coleção de destino que está instalando as atualizações de software na implantação ao mesmo tempo.  
        >   
        >  É possível configurar a definição do cliente **Agente de Computador** , **Desativar data limite aleatória** para desabilitar o atraso de aleatoriedade das atualizações de software necessárias. Para obter mais informações, consulte [Computer Agent](../../core/clients/deploy/about-client-settings.md#a-namebkmkcomputeragentdevicesettingsa-computer-agent).  

8. Na página Experiência do Usuário, defina as seguintes configurações:  

    -   **Notificações ao usuário**: especifique se quer exibir notificações das atualizações de software no Centro de Software no computador cliente no **Tempo disponível do software** configurado e se deseja exibir as notificações ao usuário nos computadores cliente.  

    -   **Comportamento do prazo**: especifique o comportamento que deve ocorrer quando o prazo for alcançado para a implantação de atualização do software. Especifique se deseja instalar as atualizações de software na implantação. Especifique também se o sistema deve ser reiniciado após a instalação da atualização de software, independentemente de uma janela de manutenção configurada. Para obter mais informações sobre janelas de manutenção, consulte [Como usar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamento de reinicialização do dispositivo**: especifique se uma reinicialização do sistema em servidores e estações de trabalho deve ser suprimida depois que as atualizações de software são instaladas e uma reinicialização do sistema é necessária para concluir a instalação.  

        > [!IMPORTANT]  
        >  A supressão das reinicializações do sistema pode ser útil em ambientes de servidor ou para casos em que você não quer que os computadores que estão instalando as atualizações de software reiniciem por padrão. No entanto, isso pode deixar os computadores em um estado inseguro, ao passo que permitir uma reinicialização forçada ajuda a garantir a conclusão imediata da instalação da atualização de software.  

    -   **Manuseio de filtro de gravação para dispositivos Windows Embedded**: ao implantar atualizações de software em dispositivos Windows Embedded com filtro de gravação habilitado, é possível especificar que a atualização de software seja instalada na sobreposição temporária e que as alterações sejam confirmadas mais tarde, na data limite da instalação ou durante uma janela de manutenção. Ao confirmar as alterações na data limite da instalação ou durante uma janela de manutenção, é necessário reinicializar. Dessa forma, as alterações permanecem no dispositivo.  

        > [!NOTE]  
        >  Ao implantar uma atualização de software em um dispositivo Windows Embedded, verifique se o dispositivo é membro de uma coleção com uma janela de manutenção configurada.  

9. Na página Alertas, configure como o Configuration Manager e o System Center Operations Manager gerarão alertas para essa implantação.  

    > [!WARNING]  
    >  Você pode verificar os alertas de atualizações de software recentes no nó **Atualizações de Software** no espaço de trabalho **Biblioteca de Software** .  

10. Na página Configurações de Download, defina as seguintes configurações:  

    -   Especifique se o cliente irá baixar e instalar as atualizações de software quando estiver conectado a uma rede lenta ou usando um local de conteúdos de fallback.  

    -   Especifique se o cliente deve baixar e instalar as atualizações de software por meio de um ponto de distribuição de fallback quando o conteúdo das atualizações de software não está disponível ou de um ponto de distribuição preferencial.  

    -   **Permitir que os clientes compartilhem conteúdo com outros clientes na mesma sub-rede**: especifique se deseja habilitar o uso do BranchCache para downloads de conteúdo. Para obter mais informações sobre o BranchCache, veja [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    -   Especifique se os clientes que estão conectados à intranet deverão baixar atualizações de software do Microsoft Update se as atualizações de software não estiverem disponíveis nos pontos de distribuição.  

    -   Especifique se os clientes têm permissão para baixar após o prazo de uma instalação quando usam conexão de Internet limitada. Provedores de Internet ocasionalmente cobram por quantidade de dados que você envia e recebe quando está em uma conexão de Internet limitada.  

    > [!NOTE]  
    >  Os clientes solicitam o local do conteúdo de um ponto de gerenciamento de atualizações de software em uma implantação. O comportamento do download depende de como você configurou o ponto de distribuição, o pacote de implantação e as configurações desta página. Para obter mais informações, consulte [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

11. Na página do Pacote de Implantação, selecione um pacote de implantação existente ou configure as seguintes definições para criar um novo pacote de implantação:  

    1.  **Nome**: especifique o nome do pacote de implantação. Deve ser um nome exclusivo que descreva o conteúdo do pacote. Ele é limitado a 50 caracteres.  

    2.  **Descrição**: especifique uma descrição que forneça informações sobre o pacote de implantação. A descrição é limitada a 127 caracteres.  

    3.  **Origem do pacote**: especifica o local dos arquivos de origem de atualização do software.  Digite um caminho de rede para o local de origem, por exemplo, **\\\servidor\nome do compartilhamento\caminho**ou clique em **Procurar** para encontrar o local na rede. É necessário criar a pasta compartilhada para os arquivos de origem do pacote de implantação antes de ir para a próxima página.  

        > [!NOTE]  
        >  O local de origem do pacote de implantação especificado não poderá ser usado por outro pacote de implantação de software.  

        > [!IMPORTANT]  
        >  A conta do computador Provedor de SMS e o usuário que estiver executando o assistente para baixar as atualizações de software deverão ter permissões NTFS de **Gravação** no local de download. É necessário restringir o acesso ao local de download com atenção, para reduzir o risco de ataques de adulteração nos arquivos de origem de atualização de software.  

        > [!IMPORTANT]  
        >  Será possível alterar o local de origem do pacote nas propriedades do pacote de implantação depois que o Configuration Manager criar o pacote de implantação. Mas ao fazer isso, é necessário primeiro copiar o conteúdo da fonte da origem do pacote para o seu novo local de origem.  

    4.  **Prioridade de envio**: especifique a prioridade de envio do pacote de implantação. O Configuration Manager usa a prioridade de envio do pacote de implantação quando envia o pacote para pontos de distribuição. Os pacotes de implantação são enviados por ordem de prioridade: Alta, Média, ou Baixa. Pacotes com prioridades idênticas são enviados na ordem em que foram criados. Se não houver uma lista de pendências, o pacote será processado imediatamente, não importando qual seja a prioridade.  

12. Na página Pontos de Distribuição, especifique os pontos de distribuição ou grupos de pontos de distribuição que irão hospedar os arquivos de atualização de software. Para obter mais informações sobre pontos de distribuição, consulte [Configurações de ponto de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!NOTE]  
    >  A página está disponível somente quando você cria um novo pacote de implantação de atualização de software.  

13. Na página Local de Download, especifique se deseja baixar os arquivos de atualização de software da Internet ou de sua rede local. Defina as seguintes configurações:  

    -   **Baixe as atualizações de software da Internet**: selecione essa configuração para baixar as atualizações de software de um local específico na Internet. Essa configuração é habilitada por padrão.  

    -   **Baixar atualizações de software de um local na rede local**: selecione essa configuração para baixar atualizações de software de um diretório local ou pasta compartilhada. Essa configuração é útil quando o computador que executa o assistente não tem acesso à Internet. Qualquer computador com acesso à Internet pode baixar preliminarmente atualizações de software e armazená-las em um local na rede local que é acessível do computador que executa o assistente.  

14. Na página Seleção de Idioma, selecione os idiomas para os quais as atualizações de software selecionadas são baixadas. As atualizações de software só serão baixadas se estiverem disponíveis nos idiomas selecionados. Atualizações de software que não são específicas do idioma são sempre baixadas. Por padrão, o assistente seleciona os idiomas que você configurou nas propriedades de ponto de atualização de software. Pelo menos um idioma deve ser selecionado para ir para a próxima página. Quando você seleciona apenas os idiomas que não têm suporte de uma atualização de software, o download irá falhar para a atualização.  

15. Na página Resumo, verifique as configurações. Para salvar as configurações em um modelo de implementação, clique em **Salvar como Modelo**, digite um nome e selecione as configurações que você quer incluir no modelo e clique **Salvar**. Para alterar uma configuração, clique na página do assistente associado e altere a configuração.  

    > [!WARNING]  
    >  O nome do modelo pode consistir em caracteres ASCII alfanuméricos, bem como em **\\** (barra invertida) ou **‘** (aspa simples).  

16. Clique em **Avançar** para criar a ADR.  

 Depois de concluir o assistente, a ADR será executada. Isso adicionará as atualizações de software que atendem aos critérios especificados a um grupo de atualização de software, baixará as atualizações de software na biblioteca atual no servidor do site, distribuirá as atualizações de software aos pontos de distribuição configurados e então implantará o grupo de atualizações de software a clientes em uma coleção de destino.  

##  <a name="a-namebkmkadddeploymenttoadra-add-a-new-deployment-to-an-existing-adr"></a><a name="BKMK_AddDeploymentToADR"></a> Adicionar uma nova implantação a uma ADR existente  
 Depois de criar uma ADR, é possível adicionar outras implantações à regra. Isso pode ajudá-lo a gerenciar a complexidade de implantar diferentes atualizações em diferentes coleções. Cada nova implantação tem a gama completa de funcionalidade e experiência de monitoramento da implantação.  

#### <a name="to-add-a-new-deployment-to-an-existing-adr"></a>Para adicionar uma nova implantação a uma ADR existente  

1.  No console do Configuration Manager, navegue até **Biblioteca de Software** > **Visão Geral** > **Atualizações de Software** > **Regras de Implantação Automáticas** e selecione a regra desejada.  

2.  Na guia **Início** , no grupo **Regra de Implantação Automática** , clique em **Adicionar Implantação**. O Assistente para Adicionar de Implantação.  

3.  Na página **Coleção** , defina as seguintes configurações:  

    -   **Coleção**: especifica a coleção de destino a ser usada na implantação. Os membros da coleção recebem as atualizações de software que são definidas na implantação.  

    -   **Habilitar a implantação após a execução desta regra**: especifique se deseja habilitar a implantação de atualização de software após a execução da ADR. Sobre essa especificação, considere o seguinte:  

        -   Quando você habilita a implantação, as atualizações de software que atendem aos critérios definidos na regra são adicionadas a um grupo de atualização de software, o conteúdo da atualização de software é baixado conforme necessário, o conteúdo é copiado nos pontos de distribuição especificados e as atualizações de software são implantadas nos clientes na coleção de destino.  

        -   Quando você não habilita a implantação, as atualizações de software que atendem aos critérios definidos na regra são adicionadas a um grupo de atualização de software e a política de implantação de atualizações de software é configurada, mas as atualizações não são baixadas nem implantadas nos clientes. Essa situação fornece-lhe o tempo necessário para se preparar para implantar as atualizações de software, verificar se as atualizações que atendem aos critérios são adequadas e permitir a implantação em um momento posterior.  

4.  Na página Configurações de Implantação, defina as seguintes configurações:  

    -   **Usar Wake-on-LAN para ativar clientes para implantações obrigatórias**: especifica se o Wake on LAN deve ser habilitado no prazo para enviar pacotes de ativação para os computadores que exigem uma ou mais atualizações de software na implantação. Todos os computadores que estão no modo de suspensão na hora do prazo da instalação serão ativados para que a instalação da atualização de software seja iniciada. Clientes que estão no modo de suspensão e que não necessitam de atualizações de software na implantação não são iniciados. Por padrão, essa configuração não está habilitada.  

        > [!WARNING]  
        >  Antes de usar essa opção, você deve configurar computadores e redes para Wake On LAN.  

    -   **Nível de detalhe**: especifique o nível de detalhe para as mensagens de estado que são relatadas pelos computadores cliente.  

        > [!IMPORTANT]  
        >  Ao implantar atualizações de definição, defina o nível de detalhes como **Apenas erro** para que o cliente relate uma mensagem de estado apenas quando uma atualização de definição deixar de ser entregue ao cliente. Caso contrário, o cliente relatará um grande número de mensagens de estado que podem afetar o desempenho no servidor do site.  

5.  Na página Agendamento da Implantação, defina as seguintes configurações:  

    -   **Avaliação do agendamento**: especifique se o Configuration Manager avalia o tempo disponível e os prazos de instalação usando UTC ou a hora local do computador que executa o console do Configuration Manager.  

        > [!NOTE]  
        >  Quando você seleciona a hora local e seleciona **O mais breve possível** para o **Tempo disponível do software** ou o **Prazo de instalação**, a hora atual no computador que executa o console do Configuration Manager é usada para avaliar quando as atualizações estarão disponíveis ou quando serão instaladas em um cliente. Se o cliente estiver em um fuso horário diferente, essas ações ocorrerão quando o tempo do cliente atingir o tempo de avaliação.  

    -   **Tempo disponível do software**: selecione uma das configurações a seguir para especificar quando as atualizações de software estão disponíveis aos clientes:  

        -   **O mais breve possível**: selecione essa configuração para disponibilizar as atualizações de software incluídas na implantação aos computadores cliente o mais breve possível. Quando você cria a implantação com essa configuração selecionada, o Configuration Manager atualiza a política de cliente. Então, no próximo ciclo de sondagem da política do cliente, os clientes ficam informados da implantação e podem obter as atualizações disponíveis para instalação.  

        -   **Horário específico**: selecione essa configuração para disponibilizar as atualizações de software incluídas na implantação aos computadores cliente, em uma data e hora específica. Quando você cria a implantação com essa configuração habilitada, o Configuration Manager atualiza a política de cliente. Em seguida, no próximo ciclo de sondagem de política do cliente, os clientes são informados da implantação. No entanto, as atualizações de software na implantação não estão disponíveis para instalação até após a data e hora configuradas.  

    -   **Prazo de instalação**: selecione uma das seguintes configurações para especificar o prazo de instalação das atualizações de software na implantação:  

        -   **O mais breve possível**: selecione essa configuração para instalar automaticamente as atualizações de software na implantação o mais breve possível.  

        -   **Horário específico**: selecione essa configuração para instalar automaticamente as atualizações de software na implantação, em uma data e hora específica. O Configuration Manager determina o prazo para instalar as atualizações de software, adicionando o intervalo **Horário específico** configurado para o **Tempo disponível do software**.  

        > [!NOTE]  
        >  O prazo real da instalação é o prazo exibido, mais um período de tempo aleatório de até 2 horas. Isso reduz o impacto potencial de todos os computadores cliente na coleção de destino que está instalando as atualizações de software na implantação ao mesmo tempo.  
        >   
        >  É possível configurar a definição do cliente **Agente de Computador** , **Desativar data limite aleatória** para desabilitar o atraso de aleatoriedade das atualizações de software necessárias. Para obter mais informações, consulte [Computer Agent](../../core/clients/deploy/about-client-settings.md#a-namebkmkcomputeragentdevicesettingsa-computer-agent).  

6.  Na página Experiência do Usuário, defina as seguintes configurações:  

    -   **Notificações ao usuário**: especifique se quer exibir notificações das atualizações de software no Centro de Software no computador cliente no **Tempo disponível do software** configurado e se deseja exibir as notificações ao usuário nos computadores cliente.  

    -   **Comportamento do prazo**: especifique o comportamento que deve ocorrer quando o prazo for alcançado para a implantação de atualização do software. Especifique se deseja instalar as atualizações de software na implantação. Especifique também se o sistema deve ser reiniciado após a instalação da atualização de software, independentemente de uma janela de manutenção configurada. Para obter mais informações sobre janelas de manutenção, consulte [Como usar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamento de reinicialização do dispositivo**: especifique se uma reinicialização do sistema em servidores e estações de trabalho deve ser suprimida depois que as atualizações de software são instaladas e uma reinicialização do sistema é necessária para concluir a instalação.  

        > [!IMPORTANT]  
        >  A supressão das reinicializações do sistema pode ser útil em ambientes de servidor ou para casos em que você não quer que os computadores que estão instalando as atualizações de software reiniciem por padrão. No entanto, isso pode deixar os computadores em um estado inseguro, ao passo que permitir uma reinicialização forçada ajuda a garantir a conclusão imediata da instalação da atualização de software.  

    -   **Manuseio de filtro de gravação para dispositivos Windows Embedded**: ao implantar atualizações de software em dispositivos Windows Embedded com filtro de gravação habilitado, é possível especificar que a atualização de software seja instalada na sobreposição temporária e que as alterações sejam confirmadas mais tarde, na data limite da instalação ou durante uma janela de manutenção. Ao confirmar as alterações na data limite da instalação ou durante uma janela de manutenção, é necessário reinicializar. Dessa forma, as alterações permanecem no dispositivo.  

        > [!NOTE]  
        >  Ao implantar uma atualização de software em um dispositivo Windows Embedded, verifique se o dispositivo é membro de uma coleção com uma janela de manutenção configurada.  

7.  Na página Alertas, configure como o Configuration Manager e o System Center Operations Manager gerarão alertas para essa implantação.  

    > [!WARNING]  
    >  Você pode verificar os alertas de atualizações de software recentes no nó **Atualizações de Software** no espaço de trabalho **Biblioteca de Software** .  

8. Na página Configurações de Download, defina as seguintes configurações:  

    -   Especifique se o cliente irá baixar e instalar as atualizações de software quando estiver conectado a uma rede lenta ou usando um local de conteúdos de fallback.  

    -   Especifique se o cliente deve baixar e instalar as atualizações de software por meio de um ponto de distribuição de fallback quando o conteúdo das atualizações de software não está disponível ou de um ponto de distribuição preferencial.  

    -   **Permitir que os clientes compartilhem conteúdo com outros clientes na mesma sub-rede**: especifique se deseja habilitar o uso do BranchCache para downloads de conteúdo. Para obter mais informações sobre o BranchCache, veja [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    -   Especifique se os clientes que estão conectados à intranet deverão baixar atualizações de software do Microsoft Update se as atualizações de software não estiverem disponíveis nos pontos de distribuição.  

    -   Especifique se os clientes têm permissão para baixar após o prazo de uma instalação quando usam conexão de Internet limitada. Provedores de Internet ocasionalmente cobram por quantidade de dados que você envia e recebe quando está em uma conexão de Internet limitada.  

    > [!NOTE]  
    >  Os clientes solicitam o local do conteúdo de um ponto de gerenciamento de atualizações de software em uma implantação. O comportamento do download depende de como você configurou o ponto de distribuição, o pacote de implantação e as configurações desta página. Para obter mais informações, consulte [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

Para obter mais informações sobre o processo de implantação, veja [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).

## <a name="next-steps"></a>Próximas etapas
[Monitorar atualizações de software](monitor-software-updates.md)



<!--HONumber=Nov16_HO1-->


