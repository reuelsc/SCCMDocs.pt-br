1.  No console do Configuration Manager, vá para o espaço de trabalho **Biblioteca de Software** e selecione o nó **Atualizações de Software**.  

2.  Escolha a atualização de software a ser baixada usando um dos métodos a seguir:  

    -   Selecione um ou mais grupos de atualização de software no nó **Grupos de Atualização de Software**. Em seguida, clique em **Baixar** na faixa de opções.  

    -   Selecione uma ou mais atualizações de software no nó **Todas as Atualizações de Software**. Em seguida, clique em **Baixar** na faixa de opções.  

        > [!NOTE]  
        >  No nó **Todas as Atualizações de Software**, o Configuration Manager exibe somente atualizações de software com classificações **Crítica** e **Segurança** liberadas nos últimos 30 dias.  

        > [!TIP]  
        >  Clique em **Adicionar Critérios** para filtrar as atualizações de software exibidas no nó **Todas as Atualizações de Software**. Salve os critérios de pesquisa que você geralmente usa e, em seguida, gerencie as pesquisas salvas na guia **Pesquisa**.  


3.  Na página **Pacote de Implantação** do Assistente para Baixar Atualizações de Software, defina as seguintes configurações:  

    -  **Selecionar pacote de implantação**: escolha esta configuração para selecionar um pacote de implantação existente para as atualizações do software na implantação.  

        > [!NOTE]  
        >  Atualizações de software que o site já baixou para o pacote de implantação selecionado não serão baixadas novamente.  

    -  **Criar um novo pacote de implantação**: selecione essa configuração para criar um novo pacote de implantação existente para as atualizações do software que estão na implantação. Defina as seguintes configurações:  

        -   **Nome**: especifica o nome do pacote de implantação. O pacote deve ter um nome exclusivo que descreva resumidamente o conteúdo do pacote. Ele é limitado a 50 caracteres.  

        -   **Descrição**: especifique uma descrição que forneça informações sobre o pacote de implantação. A descrição opcional é limitada a 127 caracteres.    

        -   **Origem do pacote**: especifica o local dos arquivos de origem de atualização do software. Digite um caminho de rede para o local de origem, por exemplo, `\\server\sharename\path`, ou clique em **Procurar** para encontrar o local de rede. Crie a pasta compartilhada para os arquivos de origem do pacote de implantação antes de ir para a próxima página.  

             - Não é possível usar o local especificado como a origem de outro pacote de implantação de software.  

             - Será possível alterar o local de origem do pacote nas propriedades do pacote de implantação depois que o Configuration Manager criar o pacote de implantação. Se você fizer isso, primeiro copie o conteúdo da origem do pacote original para o novo local de origem do pacote.  

             -  A conta do computador do Provedor de SMS e o usuário que está executando o assistente para baixar as atualizações de software precisam ter permissões de **Gravação** para o local de download. Restringir o acesso ao local de download. Essa restrição reduz o risco de invasores adulterarem arquivos de origem de atualização de software.  

        - **Habilitar replicação diferencial binária**: habilite essa configuração para minimizar o tráfego de rede entre os sites. A BDR (replicação diferencial binária) atualiza apenas o conteúdo que foi alterado no pacote, em vez de atualizar o conteúdo do pacote inteiro. Para obter mais informações, confira [Replicação diferencial binária](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#binary-differential-replication).  

4.  Na página **Pontos de Distribuição**, especifique os pontos de distribuição ou os grupos de pontos de distribuição para hospedar os arquivos de atualização de software. Para obter mais informações sobre pontos de distribuição, consulte [Configurações de ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_configs). A página está disponível somente quando você cria um novo pacote de implantação de atualização de software.  

5.  A página **Configurações de Distribuição** está disponível somente quando você cria um novo pacote de implantação de atualização de software. Especifique as seguintes configurações:  

    -   **Prioridade de distribuição**: use essa configuração para especificar a prioridade de distribuição do pacote de implantação. A prioridade de distribuição se aplica quando o pacote de implantação é enviado aos pontos de distribuição nos sites filho. Os pacotes de implantação são enviados em ordem de prioridade: alta, média ou baixa. Pacotes com prioridades idênticas são enviados na ordem em que foram criados. Quando não há nenhuma lista de pendências, o pacote é processado imediatamente, independentemente de sua prioridade. Por padrão, o site envia pacotes com prioridade **Média**.  

    -   **Habilitar para distribuição sob demanda**: use essa configuração para habilitar a distribuição de conteúdo sob demanda para pontos de distribuição configurados para esse recurso e no grupo de limites atual do cliente. Quando você habilita essa configuração, o ponto de gerenciamento cria um gatilho para o gerenciador de distribuição distribuir o conteúdo para todos esses pontos de distribuição quando um cliente solicita o conteúdo do pacote e o conteúdo não está disponível. Para obter mais informações, confira [Distribuição de conteúdo sob demanda](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#on-demand-content-distribution).  

    -   **Configurações de pontos de distribuição em pré-teste**: use essa configuração para especificar como você quer distribuir conteúdo para os pontos de distribuição em pré-teste. Selecione uma das seguintes opções:  

        -   **Baixar conteúdo automaticamente quando pacotes forem atribuídos a pontos de distribuição**: use essa configuração para ignorar as configurações de pré-teste e distribuir conteúdo ao ponto de distribuição.   

        -   **Baixar somente alterações de conteúdo para o ponto de distribuição**: use essa configuração para pré-teste do conteúdo inicial do ponto de distribuição e distribua as alterações de conteúdo ao ponto de distribuição.  

        -   **Copiar manualmente o conteúdo deste pacote para o ponto de distribuição**: use essa configuração para sempre realizar o pré-teste do conteúdo no ponto de distribuição. Essa opção é o padrão.  

        Para obter mais informações sobre como realizar o pré-teste de conteúdos para os pontos de distribuição, consulte [Conteúdo de pré-teste](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  


6.  Na página **Local de Download**, especifique o local que o Configuration Manager usa para baixar os arquivos de origem de atualização de software. Use uma das seguintes opções:  

    -   **Baixar atualizações de software da Internet**: selecione essa configuração para baixar as atualizações de software do local na Internet. Essa opção é o padrão.  

    -   **Baixar atualizações de software de um local na minha rede**: selecione essa configuração para baixar atualizações de software de um diretório local ou de uma pasta compartilhada. Essa configuração é útil quando o computador que executa o assistente não tem acesso à Internet. Qualquer computador com acesso à Internet pode baixar as atualizações de software antecipadamente. Em seguida, ele pode armazená-las em um local na rede local que seja acessível pelo computador que executa o assistente.  


7.  Na página **Seleção de Idioma**, selecione os idiomas para os quais o site deve baixar as atualizações de software selecionadas. O site somente baixa essas atualizações quando elas estão disponíveis nos idiomas selecionados. As atualizações de software que não são específicas a um idioma são sempre baixadas. Por padrão, o assistente seleciona os idiomas que você configurou nas propriedades do ponto de atualização de software. Pelo menos um idioma deve ser selecionado para ir para a próxima página. Quando você seleciona somente idiomas que não têm o suporte de uma atualização de software, o download da atualização falha.  

8. Na página **Resumo**, verifique as configurações selecionadas no assistente e clique em **Próximo** para baixar as atualizações de software.  

9. Na página **Conclusão**, verifique se as atualizações de software foram baixadas com êxito e clique em **Fechar**.  
