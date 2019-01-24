---
title: Implantar atualizações de software manualmente
titleSuffix: Configuration Manager
description: Crie implantações de software manualmente para atualizar seus clientes com as atualizações de software necessárias ou para implantar atualizações fora de banda.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.openlocfilehash: 8c0752506e410f752f49795470215c30b0928e4e
ms.sourcegitcommit: d5c013a29f53b975fe3a6cb0a41f1e817bd7b235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54342832"
---
# <a name="manually-deploy-software-updates"></a>Implantar atualizações de software manualmente  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Uma implantação manual de atualização de software é o processo de selecionar atualizações de software no console do Configuration Manager e iniciar manualmente o processo de implantação. Também é possível adicionar atualizações de software selecionadas a um grupo de atualização e implantar manualmente o grupo de atualização. Normalmente, as implantações manuais são usadas para atualizar os clientes com as atualizações de software necessárias. Em seguida, as ADR (regras de implantação automática) são usadas para gerenciar as implantações de atualização de software mensais em andamento. Esse método manual também pode ser usado para implantar atualizações de software fora de banda. Para obter mais informações sobre qual método de implantação é adequado para você, confira [Implantar atualizações de software](deploy-software-updates.md).



##  <a name="BKMK_1SearchCriteria"></a> Etapa 1: Especificar critérios de pesquisa para atualizações de software  

Dependendo das combinações e classificações de produtos que o site sincroniza, pode haver milhares de atualizações de software exibidas no console do Configuration Manager. A primeira etapa no fluxo de trabalho para implantar manualmente atualizações de software é identificar aquelas que você deseja implantar. Por exemplo, mostrar todas as atualizações de software necessárias em mais de 50 dispositivos clientes com a classificação **Segurança** ou **Crítica**.  

> [!IMPORTANT]  
>  Uma única implantação de atualização de software tem um limite de 1000 atualizações de software.  

### <a name="process-to-specify-search-criteria-for-software-updates"></a>Processo para especificar critérios de pesquisa para atualizações de software  

1.  No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Atualizações de Software** e clique em **Todas as Atualizações de Software**. Esse nó exibe todas as atualizações de software sincronizadas.  

    > [!NOTE]  
    >  O nó **Todas as Atualizações de Software** exibe somente atualizações de software com as classificações **Crítica** e **Segurança** lançadas nos últimos 30 dias.  

2.  No painel de pesquisa, filtre para identificar as atualizações de software que você precisa. Use uma das seguintes opções ou as duas:  

    -   Na caixa de texto de pesquisa, digite uma cadeia de caracteres de pesquisa para filtrar as atualizações de software. Por exemplo, digite a ID do artigo ou do boletim de uma atualização de software específica. Ou insira uma cadeia de caracteres que aparece no título de várias atualizações de software.  

    -   Clique em **Adicionar Critérios** e selecione os critérios para filtrar as atualizações de software. Clique em **Adicionar** e forneça os valores dos critérios.  

3.  Clique em **Pesquisar** para filtrar as atualizações de software.  

    > [!TIP]  
    >  Salve os critérios de filtro usados com frequência. Na faixa de opções, clique na opção **Salvar Pesquisa Atual**. Recupere as pesquisas anteriores clicando em **Pesquisas Salvas**.   



##  <a name="BKMK_2UpdateGroup"></a> Etapa 2: Criar um grupo de atualização de software que contenha as atualizações de software   

Os grupos de atualizações de software permitem que você organize as atualizações de software em preparação para implantação. Use o procedimento a seguir para adicionar manualmente as atualizações de software a um novo grupo de atualização de software.  

### <a name="process-to-manually-add-software-updates-to-a-new-software-update-group"></a>Processo para adicionar manualmente as atualizações de software a um novo grupo de atualização de software  

1.  No console do Configuration Manager, acesse o workspace **Biblioteca de Software** e selecione **Atualizações de Software**. Selecione as atualizações de software desejadas.  

2.  Clique em **Criar Grupo de Atualização de Software** na faixa de opções.  

3.  Especifique o nome do grupo de atualização de software e, opcionalmente, forneça uma descrição. Use um nome e uma descrição que forneçam informações suficientes para que você possa determinar que tipos de atualizações estão no grupo de atualização de software. Clique em **Criar**.  

4.  Selecione o nó **Grupos de Atualizações de Software** e selecione o novo grupo de atualização de software. Para exibir a lista de atualizações no grupo, clique em **Mostrar Membros** na faixa de opções.  



##  <a name="BKMK_3DownloadContent"></a> Etapa 3: Baixar o conteúdo para o grupo de atualização de software  

Antes de implantar as atualizações de software, baixe o conteúdo das atualizações de software no grupo de atualização de software. Essa etapa permite verificar se o conteúdo está disponível nos pontos de distribuição antes de implantar as atualizações de software. Ele também ajuda a evitar problemas inesperados com a distribuição de conteúdo. Se você ignorar essa etapa, como parte do processo de implantação, o site baixará o conteúdo e distribuirá para os pontos de distribuição. Use o procedimento a seguir para baixar o conteúdo para atualizações de software no grupo de atualização de software.  


### <a name="process-to-download-content-for-the-software-update-group"></a>Processo para baixar o conteúdo para o grupo de atualização de software
[!INCLUDE [downloadupdates](../includes/downloadupdates.md)]

### <a name="process-to-monitor-content-status"></a>Processo para monitorar o status do conteúdo
1. Para monitorar o status do conteúdo das atualizações de software, acesse o workspace **Monitoramento** no console do Configuration Manager. Expanda **Status de Distribuição** e, em seguida, selecione o nó **Status do Conteúdo**.  

2. Selecione o pacote e atualização de software que você identificou anteriormente para baixar as atualizações de software no grupo de atualização de software.  

3. Clique em **Exibir Status** na faixa de opções.  



##  <a name="BKMK_4DeployUpdateGroup"></a> Etapa 4: Implantar o grupo de atualização de software  

Depois de determinar as atualizações que você deseja implantar e adicioná-las a um grupo de atualização de software, implante manualmente o grupo de atualização de software.  

### <a name="process-to-manually-deploy-the-software-updates-in-a-software-update-group"></a>Processo para implantar manualmente as atualizações de software em um grupo de atualização de software  

1. No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Atualizações de Software** e selecione o nó **Grupos de Atualizações de Software**.  

2. Selecione o grupo de atualização de software que você deseja implantar. Clique em **Implantar** na faixa de opções.   

3. Na página **Geral** do Assistente para Implantar Atualizações de Software, defina as seguintes configurações:  

   -   **Nome**: especifique o nome da implantação. A implantação precisa ter um nome exclusivo que descreva sua finalidade e a diferencie das outras implantações no site. Esse campo de nome tem um limite de 256 caracteres. Por padrão, o Configuration Manager fornece um nome para a implantação automaticamente no seguinte formato: `Microsoft Software Updates - YYYY-MM-DD <time>`  

   -   **Descrição**: especifique uma descrição para a implantação. A descrição é opcional, mas fornece uma visão geral da implantação. Inclua qualquer outra informação relevante que ajude a identificar e a diferenciá-la das outras no site. O campo de descrição tem um limite de 256 caracteres e tem um valor em branco por padrão.  

   -   **Atualização de Software/Grupo de Atualização de Software**: Verifique se o grupo de atualização de software exibido ou a atualização de software está correta.  

   -   **Selecionar Modelo de Implantação**: Especifique se deseja aplicar um modelo de implantação salvo anteriormente. Configure um modelo de implantação para salvar as propriedades de implantação de atualização de software comuns. Aplique o modelo ao implantar as próximas atualizações de software. Esses modelos economizam tempo e ajudam a garantir a consistência entre implantações semelhantes.  

   -   **Coleta**: Especifique a coleção para a implantação. Os dispositivos na coleção recebem as atualizações de software dessa implantação.  

4. Na página **Configurações de Implantação**, defina as seguintes configurações:  

   -   **Tipo de implantação**: especifique o tipo de implantação para a implantação de atualização de software.  

       > [!IMPORTANT]  
       >  Depois de criar a implantação de atualização de software, você não pode alterar o tipo de implantação.  

        - Selecione **Obrigatória** para criar uma implantação de atualização de software obrigatória. As atualizações de software são instaladas automaticamente nos clientes antes da data limite de instalação que você configura.  

        - Selecione **Disponível** para criar uma implantação de atualização de software opcional. Essa implantação está disponível para ser instalada pelos usuários por meio do Centro de Software.  

       > [!NOTE]  
       >  Quando você implanta um grupo de atualização de software como **Obrigatório**, os clientes baixam o conteúdo em segundo plano e atendem às configurações do BITS, quando ele está configurado.  
       > 
       > Para os grupos de atualizações de software implantados como **Disponíveis**, os clientes baixam o conteúdo em primeiro plano e ignoram as configurações do BITS.  

   -   **Use o Wake-on-LAN para ativar clientes para implantações necessárias**: Especifica se o Wake On LAN deve ou não ser habilitado na data limite. O Wake On LAN envia pacotes de ativação para os computadores que exigem uma ou mais atualizações de software na implantação. O site ativa todos os computadores que estão no modo de suspensão na data limite da instalação para que a instalação possa ser iniciada. Os clientes que estão no modo de suspensão e que não requerem nenhuma atualização de software na implantação não são iniciados. Por padrão, essa configuração não está habilitada. Ela só está disponível para implantações **Obrigatórias**. Antes de usar essa opção, configure os computadores e as redes para Wake On LAN. Para obter mais informações, confira [Como configurar Wake On LAN](/sccm/core/clients/deploy/configure-wake-on-lan).  

   -   **Nível de detalhe**: Especifique o nível de detalhe das mensagens de estado que os clientes relatam ao site.  

5. Na página **Agendamento**, defina as seguintes configurações:  

   -   **Agendar avaliação**: Especifique o tempo em que o Configuration Manager avalia o horário de disponibilidade e data limite da instalação. Escolha se desejar usar o UTC (Tempo Universal Coordenado) ou a hora local do computador que executa o console do Configuration Manager.  

       - Quando você seleciona **Hora local do cliente** aqui e, em seguida, seleciona **Assim que possível** para o **Horário de disponibilidade do software**, a hora atual no computador que executa o Console do Configuration Manager é usada para avaliar quando as atualizações estão disponíveis. Esse comportamento é o mesmo com a **Data limite da instalação** e a hora em que as atualizações são instaladas em um cliente. Se o cliente está em um fuso horário diferente, essas ações ocorrem quando a hora do cliente atinge o tempo de avaliação.  

   -   **Tempo disponível do software**: Selecione uma das configurações a seguir para especificar quando as atualizações de software estarão disponíveis aos clientes:  

       -   **O mais breve possível**: Disponibiliza as atualizações de software na implantação para os clientes assim que possível. Quando você cria a implantação com essa configuração selecionada, o Configuration Manager atualiza a política de cliente. No próximo ciclo de sondagem da política do cliente, os clientes reconhecem a implantação e as atualizações de software disponíveis para instalação.  

       -   **Horário específico**: Faz com que as atualizações de software incluídas na implantação fiquem disponíveis aos clientes em uma determinada data e hora. Quando você cria a implantação com essa configuração habilitada, o Configuration Manager atualiza a política de cliente. No próximo ciclo de sondagem da política do cliente, os clientes reconhecem a implantação. No entanto, as atualizações de software na implantação só ficam disponíveis para instalação após a data e hora configuradas.  

   -   **Data limite para a instalação**: Essas opções só estão disponíveis para implantações **Obrigatórias**. Selecione uma das seguintes configurações para especificar a data limite de instalação das atualizações de software na implantação  

       -   **O mais breve possível**: Selecione esta configuração para instalar automaticamente as atualizações de software na implantação o mais breve possível.  

       -   **Horário específico**: Selecione esta configuração para instalar automaticamente as atualizações de software na implantação, em uma data e hora específica.  

           - A hora limite da instalação real é a hora limite exibida, mais um período aleatório de até duas horas. A aleatoriedade reduz o possível impacto causado pelos clientes na coleção ao instalarem as atualizações na implantação ao mesmo tempo.   

           - Para desabilitar o atraso aleatório da instalação das atualizações de software necessárias, defina a configuração do cliente como **Desabilitar aleatoriedade de data limite** no grupo **Agente de Computador**. Para obter mais informações, confira [Configurações do cliente do Agente do Computador](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

   -  **Atrase a imposição dessa implantação de acordo com as preferências do usuário, até o período de carência definido nas configurações do cliente**: Habilite essa configuração para conceder mais tempo aos usuários para que instalem as atualizações de software após a data limite.  

       - Esse comportamento geralmente é necessário quando um computador fica desligado por muito tempo e precisa instalar várias atualizações de software ou aplicativos. Por exemplo, quando um usuário retorna de férias, ele precisa esperar bastante tempo para que o cliente instale as implantações vencidas.  

       - Configure esse período de carência com a propriedade **Período de carência para imposição após a data limite da implantação (horas)** nas configurações do cliente. Para obter mais informações, confira a seção [Agente de computador](/sccm/core/clients/deploy/about-client-settings#computer-agent). O período de cortesia de imposição se aplica a todas as implantações com essa opção habilitada e direcionadas aos dispositivos nos quais você implantou também a configuração do cliente.  

       - Após a data limite, o cliente instala as atualizações de software no primeiro período fora do horário comercial, que o usuário configurou, até esse período de carência. No entanto, o usuário ainda pode abrir o Centro de Software e instalar as atualizações de software a qualquer momento. Depois que o período de carência expirar, a imposição retorna ao comportamento normal para implantações atrasadas.  

6. Na página **Experiência do Usuário**, defina as seguintes configurações:  

   -   **Notificações do usuário**: Especifique se deseja exibir notificações no Centro de Software no **Horário de disponibilidade do software** configurado. Essa configuração também controla se os usuários devem ser notificados nos computadores cliente. Para implantações **Disponíveis**, você não pode selecionar a opção **Ocultar no Centro de Software e em todas as notificações**.  

   -   **Comportamento da data limite**: Essa configuração só é permitida para implantações **Obrigatórias**. Especifica os comportamentos quando a implantação de atualização de software atinge a data limite fora de uma janela de manutenção definida. As opções incluem instalar as atualizações de software e executar um reinício do sistema após a instalação. Para obter mais informações sobre janelas de manutenção, consulte [Como usar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows). 
  
       > [!Note]
       > Isso se aplica somente quando a janela de manutenção está configurada para o dispositivo cliente. Se nenhuma janela de manutenção for definida no dispositivo, a atualização da instalação e a reinicialização sempre ocorrerão após o prazo.

   -   **Comportamento de reinicialização de dispositivo**: Essa configuração só é permitida para implantações **Obrigatórias**. Especifique se deseja suprimir a reinicialização do sistema em servidores e estações de trabalho quando há necessidade de reinicialização para concluir a instalação da atualização.  

       > [!WARNING]  
       >  A supressão das reinicializações do sistema pode ser útil em ambientes de servidor ou quando você não deseja que os computadores de destino sejam reiniciados por padrão. No entanto, isso pode deixar os computadores em um estado inseguro. Permitir uma reinicialização forçada ajuda a garantir a conclusão imediata da instalação da atualização de software.  

   -   **Manuseio de filtro de gravação para dispositivos Windows Embedded**: Essa configuração controla o comportamento da instalação em dispositivos Windows Embedded habilitados com um filtro de gravação. Escolha a opção para confirmar as alterações na data limite da instalação ou durante uma janela de manutenção. Quando você seleciona essa opção, a reinicialização é necessária e as alterações permanecem no dispositivo. Caso contrário, a atualização é instalada, aplicada em uma sobreposição temporária e confirmada mais tarde.  

       -  Ao implantar uma atualização de software em um dispositivo Windows Embedded, verifique se o dispositivo é membro de uma coleção que tem uma janela de manutenção configurada.  

   - **Comportamento de reavaliação da implantação de atualizações de software na reinicialização**: Selecione essa configuração para configurar implantações de atualizações de software para que os clientes executem uma verificação de conformidade de atualizações de software imediatamente depois que eles instalam atualizações de software e reiniciam. Essa configuração permite que o cliente verifique se há atualizações adicionais que se tornam aplicáveis depois que o cliente é reiniciado e, em seguida, instala-as durante a mesma janela de manutenção.  

7. Na página **Alertas**, configure como o Configuration Manager gera alertas para essa implantação. Examine os alertas de atualizações de software recentes do Configuration Manager no nó **Atualizações de Software** do workspace **Biblioteca de Software**. Se você também estiver usando o System Center Operations Manager, configure seus alertas. Apenas configure alertas para implantações **Obrigatórias**.  

8. Na página **Configurações de Download**, defina as seguintes configurações:  

    > [!NOTE]  
    >  Os clientes solicitam o local do conteúdo de um ponto de gerenciamento de atualizações de software em uma implantação. O comportamento do download depende de como você configurou o ponto de distribuição, o pacote de implantação e as configurações nesta página.  

    - Especifique se clientes devem baixar e instalar as atualizações ao usarem um ponto de distribuição de um vizinho ou os grupos de limites do site padrão.  

    - Especifique se os clientes devem baixar e instalar as atualizações de um ponto de distribuição no grupo de limites do site padrão quando o conteúdo das atualizações de software não está disponível em um ponto de distribuição nos grupos de limites atuais ou vizinhos.  

    - **Permita que os clientes compartilhem conteúdo com outros clientes na mesma sub-rede**: Especifique se deseja habilitar o uso do BranchCache para downloads de conteúdo. Para obter mais informações, confira [BranchCache](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#branchcache). Começando na versão 1802, o BranchCache está sempre habilitado nos clientes. Essa configuração foi removida, pois os clientes usam o BranchCache quando há suporte para ele no ponto de distribuição.  

    - **Se não houver atualizações de software disponíveis no ponto de distribuição em grupos de limite atuais, vizinhos ou do site, baixe conteúdo do Microsoft Update**: Selecione essa configuração para fazer com que clientes conectados à intranet baixem as atualizações de software do Microsoft Update se elas não estiverem disponíveis nos pontos de distribuição. Os clientes baseados na Internet sempre acessam o Microsoft Update para buscar o conteúdo de atualizações de software.

    - Especifique se deseja permitir que os clientes baixem após a data limite de instalação ao usarem conexões de Internet limitadas. Às vezes, os provedores de Internet cobram pela quantidade de dados que você envia e recebe quando está em uma conexão limitada.  

9. Na página **Pacote de Implantação**, selecione uma das seguintes opções:  

    > [!Note]  
    > Se você já executou a [Etapa 3: Baixar o conteúdo para o grupo de atualização de software](#BKMK_3DownloadContent), o assistente não exibirá as páginas **Pacote de Implantação**, **Pontos de Distribuição** e **Seleção de Idioma**. Acesse a página [Resumo](#bkmk_summary) do assistente.  
    > 
    >  As atualizações de software que já foram baixadas para a biblioteca de conteúdo no servidor do site não são baixadas novamente. Esse comportamento ocorre mesmo quando você cria um pacote de implantação para as atualizações de software. Se todas as atualizações de software já estiverem baixadas, o assistente pulará para a página [Resumo](#bkmk_summary).  

    - **Selecione um Pacote de Implantação**: Adicione essas atualizações a um pacote de implantação existente.  

    - **Crie um novo pacote de implantação**: Adicione essas atualizações a um novo pacote de implantação. Defina as seguintes configurações adicionais:  

        -  **Nome**: especifique o nome do pacote de implantação. Use um nome exclusivo que descreve o conteúdo do pacote. Ele é limitado a 50 caracteres.  

        -  **Descrição**: especifique uma descrição que forneça informações sobre o pacote de implantação. A descrição opcional é limitada a 127 caracteres.  

        -  **Origem do pacote**: Especifique o local dos arquivos de origem de atualização de software. Digite um caminho de rede para o local de origem, por exemplo, `\\server\sharename\path`, ou clique em **Procurar** para encontrar o local de rede. Crie a pasta compartilhada para os arquivos de origem do pacote de implantação antes de continuar na próxima página.  

            - Não é possível usar o local especificado como a origem de outro pacote de implantação de software.  

            - Será possível alterar o local de origem do pacote nas propriedades do pacote de implantação depois que o Configuration Manager criar o pacote de implantação. Se você fizer isso, primeiro copie o conteúdo da origem do pacote original para o novo local de origem do pacote.  

            -  A conta do computador do Provedor de SMS e o usuário que está executando o assistente para baixar as atualizações de software precisam ter permissões de **Gravação** para o local de download. Restringir o acesso ao local de download. Essa restrição reduz o risco de invasores adulterarem arquivos de origem de atualização de software.  

        -  **Prioridade de envio**: Especifique a prioridade de envio do pacote de implantação. O Configuration Manager usa essa prioridade quando envia o pacote para os pontos de distribuição. Os pacotes de implantação são enviados em ordem de prioridade: alta, média ou baixa. Pacotes com prioridades idênticas são enviados na ordem em que foram criados. Quando não há nenhuma lista de pendências, o pacote é processado imediatamente, independentemente de sua prioridade.  

        - **Habilitar replicação diferencial binária**: Habilite essa configuração para minimizar o tráfego de rede entre sites. A BDR (replicação diferencial binária) atualiza apenas o conteúdo que foi alterado no pacote, em vez de atualizar o conteúdo do pacote inteiro. Para obter mais informações, confira [Replicação diferencial binária](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#binary-differential-replication).  

    - **Nenhum pacote de implantação**: Começando com a versão 1806, é possível implantar atualizações de software em dispositivos sem precisar primeiro fazer o download e distribuir o conteúdo para pontos de distribuição. Essa configuração é útil ao lidar com um conteúdo de atualização muito grande. Use-a também quando desejar que os clientes sempre obtenham o conteúdo do serviço de nuvem do Microsoft Update. Os clientes nesse cenário também podem baixar o conteúdo de pares que já tenham o conteúdo necessário. O cliente do Configuration Manager continua a gerenciar o download de conteúdo, portanto, é possível usar o recurso de cache par do Configuration Manager ou outras tecnologias, como a Otimização de Entrega. Esse recurso dá suporte a qualquer tipo de atualização com suporte do gerenciamento de atualizações de software do Configuration Manager, incluindo as atualizações do Windows e do Office.<!--1357933-->  

10. Na página **Pontos de Distribuição**, especifique os pontos de distribuição ou os grupos de pontos de distribuição para hospedar os arquivos de atualização de software. Para obter mais informações sobre pontos de distribuição, consulte [Configurações de ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_configs).  

    > [!Note]  
    > Se você já executou a [Etapa 3: Baixar o conteúdo para o grupo de atualização de software](#BKMK_3DownloadContent), o assistente não exibirá as páginas **Pacote de Implantação**, **Pontos de Distribuição** e **Seleção de Idioma**. Acesse a página [Resumo](#bkmk_summary) do assistente.  

11. Na página **Local de Download**, especifique se deseja baixar os arquivos de atualização de software da Internet ou de sua rede local. Defina as seguintes configurações:  

    -   **Baixar atualizações de software da Internet**: Selecione esta configuração para baixar as atualizações de software de um local especificado na Internet. Essa configuração é habilitada por padrão.  

    -   **Baixar atualizações de software de um local na rede local**: selecione esta opção para baixar atualizações de software de um diretório local ou uma pasta compartilhada. Essa configuração é útil quando o computador que executa o assistente não tem acesso à Internet. Qualquer computador com acesso à Internet pode baixar as atualizações de software antecipadamente. Em seguida, ele pode armazená-las em um local na rede local que seja acessível pelo computador que executa o assistente.  

12. Na página **Seleção de Idioma**, selecione os idiomas para os quais o site deve baixar as atualizações de software selecionadas. O site somente baixa essas atualizações quando elas estão disponíveis nos idiomas selecionados. As atualizações de software que não são específicas a um idioma são sempre baixadas. Por padrão, o assistente seleciona os idiomas que você configurou nas propriedades do ponto de atualização de software. Pelo menos um idioma deve ser selecionado para ir para a próxima página. Quando você seleciona somente idiomas que não têm o suporte de uma atualização de software, o download da atualização falha.  

    > [!Note]  
    > Se você já executou a [Etapa 3: Baixar o conteúdo para o grupo de atualização de software](#BKMK_3DownloadContent), o assistente não exibirá as páginas **Pacote de Implantação**, **Pontos de Distribuição** e **Seleção de Idioma**. Acesse a página [Resumo](#bkmk_summary) do assistente.  

13. <a name="bkmk_summary"></a> Na página **Resumo**, examine as configurações. Para salvar as configurações em um modelo de implantação, clique em **Salvar Como Modelo**. Insira um nome e selecione as configurações que deseja incluir no modelo. Em seguida, clique em **Salvar**. Para alterar uma configuração, clique na página do assistente associado e altere a configuração.  

    -  O nome do modelo pode consistir em caracteres ASCII alfanuméricos, bem como `\` (barra invertida) ou `'` (aspa simples).  

14. Clique em **Próximo** para implantar a atualização de software.  

    Depois que você concluir o assistente, o Configuration Manager baixará as atualizações de software para a biblioteca de conteúdo no servidor do site. Em seguida, ele distribuirá o conteúdo para os pontos de distribuição configurados e implantará o grupo de atualização de software nos clientes na coleção de destino. Para obter mais informações sobre o processo de implantação, veja [Software update deployment process](/sum/understand/software-updates-introduction#BKMK_DeploymentProcess).  



## <a name="next-steps"></a>Próximas etapas
[Monitorar atualizações de software](monitor-software-updates.md)
