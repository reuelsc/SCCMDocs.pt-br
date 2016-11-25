1.  No console do Configuration Manager, navegue até **Biblioteca de Software** > **Atualizações de Software**.  

2.  Escolha a atualização de software a ser baixada usando um dos métodos a seguir:  

    -   Selecione um ou mais grupos de atualização de software em **Grupos de Atualização de Software**e, na guia **Início** , no **Grupos de Atualização** , clique em **Baixar**.  

    -   Selecione um ou mais grupos de atualização de software em **Grupos de Atualização de Software**e, na guia **Início** , no **Grupos de Atualização** , clique em **Baixar**.  

        > [!NOTE]  
        >  No nó **Todas as Atualizações de Software**, o Configuration Manager exibe somente atualizações de software com classificação **Crítico** e **Segurança** que foram liberadas nos últimos 30 dias.  

        > [!TIP]  
        >  Clique em **Adicionar Critérios** para filtrar as atualizações de software exibidas no nó **Todas as Atualizações de Software** , salve os critérios de pesquisa usados com frequência e gerencie as pesquisas salvas na guia **Pesquisar** .  

         O **Assistente para Baixar Atualizações de Software** será aberto.  

3.  Na página **Pacote de Implantação** , defina as seguintes configurações:  

    1.  **Selecionar pacote de implantação**: escolha esta configuração para selecionar um pacote de implantação existente para as atualizações do software na implantação.  

        > [!NOTE]  
        >  As atualizações de software que já foram baixadas no pacote de implantação selecionado não serão baixadas novamente.  

    2.  **Criar um novo pacote de implantação**: selecione esta configuração para criar um novo pacote de implantação existente para as atualizações do software que estão na implantação. Defina as seguintes configurações:  

        -   **Nome**: especifica o nome do pacote de implantação. O pacote deve ter um nome exclusivo que descreva resumidamente o conteúdo do pacote.  Ele é limitado a 50 caracteres.  

        -   **Descrição**: especifica a descrição do pacote de implantação. A descrição do pacote fornece informações sobre o conteúdo do pacote e limita-se a 127 caracteres.  

        -   **Origem do pacote**: especifica o local dos arquivos de origem de atualização do software. Digite um caminho de rede para o local de origem, por exemplo, **\\\servidor\nome do compartilhamento\caminho**ou clique em **Procurar** para encontrar o local na rede. É necessário criar a pasta compartilhada para os arquivos de origem do pacote de implantação antes de ir para a próxima página.  

            > [!NOTE]  
            >  O local de origem do pacote de implantação especificado não poderá ser usado por outro pacote de implantação de software.  

            > [!IMPORTANT]  
            >  A conta do computador Provedor de SMS e o usuário que estiver executando o assistente para baixar as atualizações de software deverão ter permissões NTFS de **Gravação** no local de download. É necessário restringir o acesso ao local de download com atenção, para reduzir o risco de ataques de adulteração nos arquivos de origem de atualização de software.  

            > [!IMPORTANT]  
            >  Será possível alterar o local de origem do pacote nas propriedades do pacote de implantação depois que o Configuration Manager criar o pacote de implantação. Mas ao fazer isso, é necessário primeiro copiar o conteúdo da fonte da origem do pacote para o seu novo local de origem.  

     Clique em **Avançar**.  

4.  Na página **Pontos de Distribuição**, especifique os pontos de distribuição ou os grupos de pontos de distribuição que vão hospedar os arquivos de atualização de software e clique em **Próximo**. Para obter mais informações sobre pontos de distribuição, consulte [Distribution point configurations](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!NOTE]  
    >  A página de pontos de distribuição está disponível somente quando você cria um novo pacote de implantação de atualização de software.  

6.  Na página **Configurações de Distribuição**, especifique as seguintes configurações:  

    -   **Prioridade de distribuição**: use essa configuração para especificar a prioridade de distribuição do pacote de implantação. A prioridade de distribuição se aplica quando o pacote de implantação é enviado aos pontos de distribuição nos sites filho. Os pacotes de implantação são enviados por ordem de prioridade: **Alta**, **Média**, ou **Baixa**. Pacotes com prioridades idênticas são enviados na ordem em que foram criados. Se não houver uma lista de pendências, o pacote será processado imediatamente, não importando qual seja a prioridade. Por padrão, os pacotes são enviados usando a prioridade **Média** .  

    -   **Distribuir o conteúdo deste pacote para os pontos de distribuição preferenciais**: use essa configuração se quiser habilitar distribuição de conteúdo sob demanda para pontos de distribuição preferenciais. Quando essa configuração está habilitada, o ponto de gerenciamento cria um gatilho para que o gerenciador de distribuição distribua o conteúdo a todos os pontos de distribuição preferenciais quando um cliente solicita o conteúdo para o pacote e o conteúdo não está disponível em nenhum ponto de distribuição preferencial. Para obter mais informações sobre os pontos de distribuição preferenciais e o conteúdo sob demanda, veja [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

    -   **Configurações de pontos de distribuição em pré-teste**: use essa configuração para especificar como você quer distribuir conteúdo para os pontos de distribuição em pré-teste. Selecione uma das seguintes opções:  

        -   **Baixar conteúdo automaticamente quando pacotes forem atribuídos a pontos de distribuição**: use essa configuração para ignorar as configurações de pré-teste e distribuir conteúdo ao ponto de distribuição.  

        -   **Baixar somente alterações de conteúdo para o ponto de distribuição**: use essa configuração para pré-teste do conteúdo inicial do ponto de distribuição e distribua as alterações de conteúdo ao ponto de distribuição.  

        -   **Copiar manualmente o conteúdo deste pacote para o ponto de distribuição**: use essa configuração para sempre realizar o pré-teste do conteúdo no ponto de distribuição. Essa é a configuração padrão.  

         Para obter mais informações sobre como realizar o pré-teste de conteúdos para os pontos de distribuição, consulte [Conteúdo de pré-teste](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

     Clique em **Avançar**.  

6.  Na página **Local de Download**, especifique o local que o Configuration Manager usará para baixar os arquivos de origem de atualização de software. Conforme necessário, use as seguintes opções:  

    -   **Baixar atualizações de software da Internet**: selecione essa configuração para baixar as atualizações de software do local na Internet. Essa é a configuração padrão.  

    -   **Baixar atualizações de software de um local na rede local**: selecione essa configuração para baixar atualizações de software de uma pasta local ou uma pasta de rede compartilhada. Use essa configuração quando o computador que executa o assistente não tiver acesso à Internet.  

        > [!NOTE]  
        >  Ao usar essa configuração, baixe as atualizações de software de qualquer computador com acesso à Internet e copie as atualizações de software em uma rede local que seja acessível do computador que executa o assistente.  

     Clique em **Avançar**.  

7.  Na página **Seleção de Idioma**, especifique os idiomas para os quais as atualizações de software selecionadas devem ser baixadas e clique em **Próximo**. O Configuration Manager baixará as atualizações de software apenas se estiverem disponíveis nos idiomas selecionados. As atualizações de software que não são específicas a um idioma são sempre baixadas.  

8. Na página **Resumo**, verifique as configurações selecionadas no assistente e clique em **Próximo** para baixar as atualizações de software.  

9. Na página **Conclusão**, verifique se as atualizações de software foram baixadas com êxito e clique em **Fechar**.  


<!--HONumber=Nov16_HO1-->


