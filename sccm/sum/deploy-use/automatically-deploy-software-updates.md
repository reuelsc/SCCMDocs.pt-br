---
title: Implantar atualizações de software automaticamente
titleSuffix: Configuration Manager
description: Implante as atualizações de software automaticamente por meio das ADR (regras de implantação automática).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 10/02/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8d83085637e971b47ee9941d76fef749660861aa
ms.sourcegitcommit: 223549003829fce7c6dc63959ee71e8b88542417
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2019
ms.locfileid: "56951844"
---
#  <a name="automatically-deploy-software-updates"></a>Implantar atualizações de software automaticamente  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use uma ADR (regra de implantação automática) em vez de adicionar novas atualizações a um grupo de atualização de software existente. Normalmente, você usa ADRs para implantar atualizações de software mensais (também conhecidas como atualizações de "Patch Tuesday") e para o gerenciamento de atualizações de definições do Endpoint Protection. Se você precisar de ajuda para determinar qual método de implantação é adequado para você, consulte [Implantar atualizações de software](deploy-software-updates.md).


##  <a name="BKMK_CreateAutomaticDeploymentRule"></a> Criar uma ADR (regra de implantação automática)  
Aprove e implante atualizações de software automaticamente usando uma ADR. Sempre que for executada, a regra pode adicionar atualizações de software a um novo grupo de atualização de software ou a um grupo existente. Quando uma regra é executada e adiciona atualizações de software a um grupo existente, ela remove todas as atualizações do grupo. Em seguida, ela adiciona ao grupo as atualizações que atendem aos critérios já definidos. 

> [!WARNING]  
>  Antes de criar uma ADR pela primeira vez, verifique se o site concluiu a sincronização de atualizações de software. Essa etapa é importante quando você executa o Configuration Manager com um idioma diferente do inglês. As classificações da atualização de software são exibidas em inglês antes da primeira sincronização e, após a conclusão da sincronização de atualizações de software, elas passam a ser exibidas nos idiomas localizados. As regras criadas antes da sincronização das atualizações de software podem não funcionar corretamente após a sincronização, porque a cadeia de caracteres de texto pode não corresponder.  


### <a name="bkmk_adr-process"></a> Processo para criar uma ADR  

1.  No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Atualizações de Software** e selecione o nó **Regras de Implantação Automática**.  

2.  Na faixa de opções, clique em **Criar Regra de Implantação Automática**.  

3.  Na página **Geral** do Assistente para Criar Regra de Implantação Automática, defina as seguintes configurações:  

    -   **Nome**: Especifique o nome para a ADR. O nome deve ser exclusivo, ajudar a descrever a finalidade da regra e identificá-la em relação a outros usuários no site do Configuration Manager.  

    -   **Descrição**: Especifique uma descrição para a ADR. A descrição deve fornecer uma visão geral da regra de implantação e outras informações relevantes que ajudam a diferenciar a regra das outras. O campo de descrição é opcional, tem um limite de 256 caracteres e um valor em branco por padrão.  

    -   **Modelo**: Selecione um modelo de implantação para especificar se deseja aplicar as configurações de ADR já salvas. Configure um modelo de implantação contendo várias propriedades comuns de implantação de atualização que você poderá usar na criação de ADRs adicionais. Esses modelos economizam tempo e ajudam a garantir a consistência entre implantações semelhantes. Selecione um dos seguintes modelos de implantação de atualização de software internos:  

         - O modelo **Patch Tuesday** fornece definições comuns a serem usadas ao implantar atualizações de software em um ciclo mensal.  

         - O modelo **Atualizações do Cliente do Office 365** fornece definições comuns a serem usadas ao implantar atualizações para clientes do Office 365 Pro Plus.  

         - O modelo **Atualizações do SCEP e do Windows Defender Antivírus** fornece definições comuns a serem usadas ao implantar atualizações de definições do Endpoint Protection.  

    -   **Coleta**: Especifica a coleção de destino a ser usada na implantação. Os membros da coleção recebem as atualizações de software que são definidas na implantação.  

    -   Decida se deseja adicionar atualizações de software a um grupo de atualização de software novo ou existente. Na maioria dos casos, escolha criar um novo grupo de atualização de software quando a ADR for executada. Se a regra for executada em um agendamento mais agressivo, você poderá optar por usar um grupo existente. Por exemplo, ao executar a regra diariamente para atualizações de definição, você poderá adicionar as atualizações de software a um grupo de atualização de software existente.  

    -   **Habilitar a implantação após essa regra ser executada**: Especifique se deseja habilitar a implantação de atualização de software após a execução da ADR. Considere as seguintes opções para essa configuração:  

        -   Quando você habilita a implantação, as atualizações que atendem aos critérios definidos da regra são adicionadas a um grupo de atualização de software. O conteúdo de atualização de software é baixado, conforme necessário. O conteúdo é copiado para pontos de distribuição especificados e as atualizações são implantadas nos clientes na coleção de destino.  

        -   Quando você não habilita a implantação, as atualizações que atendem aos critérios definidos da regra são adicionadas a um grupo de atualização de software. O conteúdo da implantação da atualização de software é baixado, conforme o necessário, e distribuído para os pontos de distribuição especificados. O site cria uma implantação desabilitada no grupo de atualização de software para impedir que as atualizações sejam implantadas nos clientes. Essa opção oferece o tempo necessário para preparar a implantação das atualizações, verificar se as atualizações que atendem aos critérios são adequadas e, em seguida, permitir a implantação.  

4.  Na página **Configurações de Implantação**, defina as seguintes configurações:  

    -   **Usar Wake On LAN para ativar clientes para implantações obrigatórias**: Especifica se o Wake On LAN deve ou não ser habilitado na data limite. O Wake On LAN envia pacotes de ativação para os computadores que exigem uma ou mais atualizações de software na implantação. O site ativa todos os computadores que estão no modo de suspensão na data limite da instalação para que a instalação possa ser iniciada. Os clientes que estão no modo de suspensão e que não requerem nenhuma atualização de software na implantação não são iniciados. Por padrão, essa configuração não está habilitada. Antes de usar essa opção, configure os computadores e as redes para Wake On LAN. Para obter mais informações, confira [Como configurar Wake On LAN](/sccm/core/clients/deploy/configure-wake-on-lan).  

    -   **Nível de detalhe**: Especifique o nível de detalhe para as mensagens de estado relatadas por clientes.  

        > [!IMPORTANT]  
        >  Ao implantar atualizações de definição, defina o nível de detalhes como **Apenas erro** para que o cliente relate uma mensagem de estado apenas quando uma atualização de definição falhar. Caso contrário, o cliente relatará um grande número de mensagens de estado que podem afetar o desempenho do servidor do site.  

    -   **Configuração de termos da licença**: Especifique se deseja implantar automaticamente atualizações de software com os termos de licença associados. Algumas atualizações de software incluem termos de licença. Quando você implanta atualizações de software automaticamente, os termos de licença não são exibidos e não há nenhuma opção para aceitá-los. Opte por implantar automaticamente todas as atualizações de software, independentemente de haver termos de licença associados, ou implante apenas as atualizações que não têm termos de licença associados.  

         - Para examinar os termos de licença de uma atualização de software, selecione a atualização de software no nó **Todas as Atualizações de Software** do workspace **Biblioteca de Software**. Na faixa de opções, clique em **Examinar Licença**.    

         - Para encontrar atualizações de software com os termos de licença associados, adicione a coluna **Termos de Licença** ao painel de resultados ano nó **Todas as Atualizações de Software**. Clique no título da coluna para classificar as atualizações de software com os termos de licença.  

5.  Na página **Atualizações de Software**, configure os critérios para as atualizações de software que a ADR recupera e adiciona ao grupo de atualização de software.  

     - O limite para atualizações de software na ADR é de 1.000.  

     - Se necessário, filtre o tamanho do conteúdo para atualizações de software nas regras de implantação automática. Para obter mais informações, confira [Configuration Manager and simplified Windows servicing on down level operating systems](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/) (Configuration Manager e manutenção simplificada do Windows em sistemas operacionais de nível inferior).  

     - Começando na versão 1806, uma propriedade de filtro para **Arquitetura** está disponível. Use esse filtro para excluir arquiteturas, como Itanium e ARM64, que são menos comuns. Lembre-se de que há aplicativos e componentes de 32 bits (x86) em execução em sistemas de 64 bits (x64). A menos que você tenha certeza de que não precisa da x86, habilite-o também ao escolher a x64.<!--1322266-->  


6.  Na página **Agendamento de Avaliação**, especifique se deseja habilitar a ADR para ser executada de acordo com um agendamento. Quando habilitada, clique em **Personalizar** para definir o agendamento recorrente.  

    - A configuração do horário de início da agenda é baseada na hora local do computador que executa o console do Configuration Manager.  

    - A avaliação da ADR pode ser executada três vezes por dia.  

    - Nunca defina o agendamento de avaliação com uma frequência que excede o agendamento de sincronização das atualizações de software. Esta página exibe o agendamento de sincronização de ponto de atualização de software para ajudá-lo a determinar a frequência do agendamento da avaliação.  
    
    - Para executar a ADR manualmente, selecione a regra no nó **Regra de Implantação Automática** do console e, em seguida, clique em **Executar Agora** na faixa de opções.  
    
       > [!NOTE]  
       > Começando na versão 1802, as ADRs podem ser agendadas para avaliar o deslocamento a partir de um dia base. Por exemplo, se "Patch Tuesday", na verdade, cair na quarta-feira, defina o agendamento de avaliação para a segunda terça-feira do deslocamento de um dia do mês.<!--1357133-->  
       >  
       > Ao agendar a avaliação com um deslocamento durante a última semana do mês, se você escolher um deslocamento que continuará no próximo mês, o site agendará a avaliação para o último dia do mês.<!--506731-->  
       >  
       > ![Deslocamento do agendamento de avaliação personalizado da ADR do dia base](./media/ADR-evaluation-schedule-offset.PNG)

   
7.  Na página **Agendamento da Implantação**, defina as seguintes configurações:  

    -   **Agendar avaliação**: Especifique o tempo em que o Configuration Manager avalia o horário de disponibilidade e data limite da instalação. Escolha se desejar usar o UTC (Tempo Universal Coordenado) ou a hora local do computador que executa o console do Configuration Manager.  

          - Quando você seleciona **Hora local do cliente** aqui e, em seguida, seleciona **Assim que possível** para o **Horário de disponibilidade do software**, a hora atual no computador que executa o Console do Configuration Manager é usada para avaliar quando as atualizações estão disponíveis. Esse comportamento é o mesmo com a **Data limite da instalação** e a hora em que as atualizações são instaladas em um cliente. Se o cliente está em um fuso horário diferente, essas ações ocorrem quando a hora do cliente atinge o tempo de avaliação.  

    -   **Tempo disponível do software**: Selecione uma das configurações a seguir para especificar quando as atualizações de software estarão disponíveis aos clientes:  

        -   **O mais breve possível**: Disponibiliza as atualizações de software na implantação para os clientes assim que possível. Quando você cria a implantação com essa configuração selecionada, o Configuration Manager atualiza a política de cliente. No próximo ciclo de sondagem da política do cliente, os clientes reconhecem a implantação e as atualizações de software disponíveis para instalação.  

        -   **Horário específico**: Faz com que as atualizações de software incluídas na implantação fiquem disponíveis aos clientes em uma determinada data e hora. Quando você cria a implantação com essa configuração habilitada, o Configuration Manager atualiza a política de cliente. No próximo ciclo de sondagem da política do cliente, os clientes reconhecem a implantação. No entanto, as atualizações de software na implantação só ficam disponíveis para instalação após a data e hora configuradas.  

    -   **Data limite para a instalação**: Selecione uma das seguintes configurações para especificar o prazo de instalação das atualizações de software na implantação:  

        -   **O mais breve possível**: Selecione esta configuração para instalar automaticamente as atualizações de software na implantação o mais breve possível.  

        -   **Horário específico**: Selecione esta configuração para instalar automaticamente as atualizações de software na implantação, em uma data e hora específica. O Configuration Manager determina o prazo para instalar as atualizações de software, adicionando o intervalo **Horário específico** configurado para o **Tempo disponível do software**.  

             - A hora limite da instalação real é a hora limite exibida, mais um período aleatório de até duas horas. A aleatoriedade reduz o possível impacto causado pelos clientes na coleção ao instalarem as atualizações na implantação ao mesmo tempo.  

             - Para desabilitar o atraso aleatório da instalação das atualizações de software necessárias, defina a configuração do cliente como **Desabilitar aleatoriedade de data limite** no grupo **Agente de Computador**. Para obter mais informações, confira [Configurações do cliente do Agente do Computador](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

    -  **Atrase a imposição dessa implantação de acordo com as preferências do usuário, até o período de carência definido nas configurações do cliente**: Habilite essa configuração para conceder mais tempo aos usuários para que instalem as atualizações de software após a data limite.  

        - Esse comportamento geralmente é necessário quando um computador fica desligado por muito tempo e precisa instalar várias atualizações de software ou aplicativos. Por exemplo, quando um usuário retorna de férias, ele precisa esperar bastante tempo para que o cliente instale as implantações vencidas.  

        - Configure esse período de carência com a propriedade **Período de carência para imposição após a data limite da implantação (horas)** nas configurações do cliente. Para obter mais informações, confira a seção [Agente de computador](/sccm/core/clients/deploy/about-client-settings#computer-agent). O período de cortesia de imposição se aplica a todas as implantações com essa opção habilitada e direcionadas aos dispositivos nos quais você implantou também a configuração do cliente.  

        - Após a data limite, o cliente instala as atualizações de software no primeiro período fora do horário comercial, que o usuário configurou, até esse período de carência. No entanto, o usuário ainda pode abrir o Centro de Software e instalar as atualizações de software a qualquer momento. Depois que o período de carência expirar, a imposição retorna ao comportamento normal para implantações atrasadas.  

8. Na página **Experiência do Usuário**, defina as seguintes configurações:  

    -   **Notificações do usuário**: Especifique se deseja exibir notificações no Centro de Software no **Horário de disponibilidade do software** configurado. Essa configuração também controla se os usuários devem ser notificados nos clientes.  

    -   **Comportamento da data limite**: Especifica os comportamentos quando a implantação de atualização de software atinge a data limite fora de uma janela de manutenção definida. As opções incluem instalar as atualizações de software e executar um reinício do sistema após a instalação. Para obter mais informações sobre janelas de manutenção, consulte [Como usar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).  
        
        > [!Note]
        > Isso se aplica somente quando a janela de manutenção está configurada para o dispositivo cliente. Se nenhuma janela de manutenção for definida no dispositivo, a atualização da instalação e a reinicialização sempre ocorrerão após o prazo.

    -   **Comportamento de reinicialização de dispositivo**: Especifique se deseja suprimir a reinicialização do sistema em servidores e estações de trabalho quando há necessidade de reinicialização para concluir a instalação da atualização.  

        > [!WARNING]  
        >  A supressão das reinicializações do sistema pode ser útil em ambientes de servidor ou quando você não deseja que os computadores de destino sejam reiniciados por padrão. No entanto, isso pode deixar os computadores em um estado inseguro. Permitir uma reinicialização forçada ajuda a garantir a conclusão imediata da instalação da atualização de software.  

    -   **Manuseio de filtro de gravação para dispositivos Windows Embedded**: Essa configuração controla o comportamento da instalação em dispositivos Windows Embedded habilitados com um filtro de gravação. Escolha a opção para confirmar as alterações na data limite da instalação ou durante uma janela de manutenção. Quando você seleciona essa opção, a reinicialização é necessária e as alterações permanecem no dispositivo. Caso contrário, a atualização é instalada, aplicada em uma sobreposição temporária e confirmada mais tarde.  

           -  Ao implantar uma atualização de software em um dispositivo Windows Embedded, verifique se o dispositivo é membro de uma coleção que tem uma janela de manutenção configurada.  

    - **Comportamento de reavaliação da implantação de atualizações de software na reinicialização**: Selecione essa configuração para configurar implantações de atualizações de software para que os clientes executem uma verificação de conformidade de atualizações de software imediatamente depois que eles instalam atualizações de software e reiniciam. Essa configuração permite que o cliente verifique se há atualizações adicionais que se tornam aplicáveis depois que o cliente é reiniciado e, em seguida, instala-as durante a mesma janela de manutenção.  

9. Na página **Alertas**, configure como o Configuration Manager gera alertas para essa implantação. Examine os alertas de atualizações de software recentes do Configuration Manager no nó **Atualizações de Software** do workspace **Biblioteca de Software**. Se você também estiver usando o System Center Operations Manager, configure seus alertas.  

10. Na página **Configurações de Download**, defina as seguintes configurações:  

    - Especifique se clientes devem baixar e instalar as atualizações ao usarem um ponto de distribuição de um vizinho ou os grupos de limites do site padrão.  

    - Especifique se os clientes devem baixar e instalar as atualizações de um ponto de distribuição no grupo de limites do site padrão quando o conteúdo das atualizações de software não está disponível em um ponto de distribuição nos grupos de limites atuais ou vizinhos.  

    - **Permita que os clientes compartilhem conteúdo com outros clientes na mesma sub-rede**: Especifique se deseja habilitar o uso do BranchCache para downloads de conteúdo. Para obter mais informações, confira [BranchCache](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#branchcache). Começando na versão 1802, o BranchCache está sempre habilitado nos clientes. Essa configuração foi removida, pois os clientes usam o BranchCache quando há suporte para ele no ponto de distribuição.  

    - **Se não houver atualizações de software disponíveis no ponto de distribuição em grupos de limite atuais, vizinhos ou do site, baixe conteúdo do Microsoft Update**: Selecione essa configuração para fazer com que clientes conectados à intranet baixem as atualizações de software do Microsoft Update se elas não estiverem disponíveis nos pontos de distribuição. Os clientes baseados na Internet sempre acessam o Microsoft Update para buscar o conteúdo de atualizações de software.  

    - Especifique se deseja permitir que os clientes baixem após a data limite de instalação ao usarem conexões de Internet limitadas. Às vezes, os provedores de Internet cobram pela quantidade de dados que você envia e recebe quando está em uma conexão limitada.  

    > [!NOTE]  
    >  Os clientes solicitam o local do conteúdo de um ponto de gerenciamento de atualizações de software em uma implantação. O comportamento do download depende de como você configurou o ponto de distribuição, o pacote de implantação e as configurações nesta página.   

11. Na página **Pacote de Implantação**, selecione uma das seguintes opções:  

    - **Selecione um Pacote de Implantação**: Adicione essas atualizações a um pacote de implantação existente.  

    - **Crie um novo pacote de implantação**: Adicione essas atualizações a um novo pacote de implantação. Defina as seguintes configurações adicionais:  

        -  **Nome**: especifique o nome do pacote de implantação. Use um nome exclusivo que descreve o conteúdo do pacote. Ele é limitado a 50 caracteres.  

        -  **Descrição**: especifique uma descrição que forneça informações sobre o pacote de implantação. A descrição opcional é limitada a 127 caracteres.  

        -  **Origem do pacote**: especifica o local dos arquivos de origem da atualização de software. Digite um caminho de rede para o local de origem, por exemplo, `\\server\sharename\path`, ou clique em **Procurar** para encontrar o local de rede. Crie a pasta compartilhada para os arquivos de origem do pacote de implantação antes de ir para a próxima página.  

            - Não é possível usar o local especificado como a origem de outro pacote de implantação de software.  

            - Será possível alterar o local de origem do pacote nas propriedades do pacote de implantação depois que o Configuration Manager criar o pacote de implantação. Se você fizer isso, primeiro copie o conteúdo da origem do pacote original para o novo local de origem do pacote.  

            -  A conta do computador do Provedor de SMS e o usuário que está executando o assistente para baixar as atualizações de software precisam ter permissões de **Gravação** para o local de download. Restringir o acesso ao local de download. Essa restrição reduz o risco de invasores adulterarem arquivos de origem de atualização de software.  

        -  **Prioridade de envio**: Especifique a prioridade de envio do pacote de implantação. O Configuration Manager usa essa prioridade quando envia o pacote para os pontos de distribuição. Os pacotes de implantação são enviados em ordem de prioridade: alta, média ou baixa. Pacotes com prioridades idênticas são enviados na ordem em que foram criados. Quando não há nenhuma lista de pendências, o pacote é processado imediatamente, independentemente de sua prioridade.  

        - **Habilitar replicação diferencial binária**: Habilite essa configuração para minimizar o tráfego de rede entre sites. A BDR (replicação diferencial binária) atualiza apenas o conteúdo que foi alterado no pacote, em vez de atualizar o conteúdo do pacote inteiro. Para obter mais informações, confira [Replicação diferencial binária](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#binary-differential-replication).  

    - **Nenhum pacote de implantação**: Começando com a versão 1806, é possível implantar atualizações de software em dispositivos sem precisar primeiro fazer o download e distribuir o conteúdo para pontos de distribuição. Essa configuração é útil ao lidar com um conteúdo de atualização muito grande. Use-a também quando desejar que os clientes sempre obtenham o conteúdo do serviço de nuvem do Microsoft Update. Os clientes nesse cenário também podem baixar o conteúdo de pares que já tenham o conteúdo necessário. O cliente do Configuration Manager continua a gerenciar o download de conteúdo, portanto, é possível usar o recurso de cache par do Configuration Manager ou outras tecnologias, como a Otimização de Entrega. Esse recurso dá suporte a qualquer tipo de atualização com suporte do gerenciamento de atualizações de software do Configuration Manager, incluindo as atualizações do Windows e do Office.<!--1357933-->  

        > [!Note]  
        > Depois de selecionar essa opção e aplicar as configurações, ela não poderá mais ser alterada. As outras opções ficarão cinza.<!--SCCMDocs-pr issue 3003-->  

12. Na página **Pontos de Distribuição**, especifique os pontos de distribuição ou os grupos de pontos de distribuição para hospedar os arquivos de atualização de software. Para obter mais informações sobre pontos de distribuição, consulte [Configurações de ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_configs). A página está disponível somente quando você cria um novo pacote de implantação de atualização de software.  
  

13. Na página **Local de Download**, especifique se deseja baixar os arquivos de atualização de software da Internet ou de sua rede local. Defina as seguintes configurações:  

    -   **Baixar atualizações de software da Internet**: Selecione esta configuração para baixar as atualizações de software de um local especificado na Internet. Essa configuração é habilitada por padrão.  

    -   **Baixar atualizações de software de um local na rede local**: selecione esta opção para baixar atualizações de software de um diretório local ou uma pasta compartilhada. Essa configuração é útil quando o computador que executa o assistente não tem acesso à Internet. Qualquer computador com acesso à Internet pode baixar as atualizações de software antecipadamente. Em seguida, ele pode armazená-las em um local na rede local que seja acessível pelo computador que executa o assistente.  

14. Na página **Seleção de Idioma**, selecione os idiomas para os quais o site deve baixar as atualizações de software selecionadas. O site somente baixa essas atualizações quando elas estão disponíveis nos idiomas selecionados. As atualizações de software que não são específicas a um idioma são sempre baixadas. Por padrão, o assistente seleciona os idiomas que você configurou nas propriedades do ponto de atualização de software. Pelo menos um idioma deve ser selecionado para ir para a próxima página. Quando você seleciona somente idiomas que não têm o suporte de uma atualização de software, o download da atualização falha.  

15. Na página de **Resumo** , analise as configurações. Para salvar as configurações em um modelo de implantação, clique em **Salvar Como Modelo**. Insira um nome e selecione as configurações que deseja incluir no modelo. Em seguida, clique em **Salvar**. Para alterar uma configuração, clique na página do assistente associado e altere a configuração.  

    -  O nome do modelo pode consistir em caracteres ASCII alfanuméricos, bem como `\` (barra invertida) ou `'` (aspa simples).  

16. Clique em **Avançar** para criar a ADR.  

Depois que você concluir o assistente, a ADR será executada. Ela adiciona as atualizações de software que atendem aos critérios especificados a um grupo de atualização de software. Em seguida, a ADR baixa as atualizações na biblioteca de conteúdo no servidor do site e as distribui para os pontos de distribuição configurados. A ADR então implanta o grupo de atualização de software nos clientes da coleção de destino.  



##  <a name="BKMK_AddDeploymentToADR"></a> Adicionar uma nova implantação a uma ADR existente  

Depois de criar uma ADR, adicione mais implantações à regra. Essa ação ajuda a gerenciar a complexidade da implantação de diferentes atualizações em diferentes coleções. Cada nova implantação tem a gama completa de funcionalidade e experiência de monitoramento da implantação.  


### <a name="process-to-add-a-new-deployment-to-an-existing-adr"></a>Processo para adicionar uma nova implantação a uma ADR existente  

1.  No console do Configuration Manager, acesse o workspace **Biblioteca de Software**, expanda **Atualizações de Software**, selecione o nó **Regras de Implantação Automática** e, em seguida, selecione a regra desejada.  

2.  Na faixa de opções, clique em **Adicionar Implantação**.   

3.  Na página **Coleção** do Assistente para Adicionar Implantação, defina as configurações disponíveis da mesma forma que na página **Geral** do Assistente para Criar Regra de Implantação Automática. Para obter mais informações, consulte a seção anterior sobre o [Processo para criar uma ADR](#bkmk_adr-process). O restante do Assistente para Adicionar Implantação inclui as seguintes páginas, que também correspondem às descrições detalhadas acima:  

     - Configurações da Implantação
     - Agendamento da Implantação
     - Experiência do usuário
     - Alertas
     - Configurações de download  

Implantações também podem ser adicionadas via programação usando os cmdlets do Windows PowerShell. Confira uma descrição completa sobre o uso desse método em [New-CMSoftwareUpdateDeployment](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmsoftwareupdatedeployment) .

Para obter mais informações sobre o processo de implantação, veja [Software update deployment process](/sccm/sum/understand/software-updates-introduction#BKMK_DeploymentProcess).


## <a name="next-steps"></a>Próximas etapas
[Monitorar atualizações de software](monitor-software-updates.md)
