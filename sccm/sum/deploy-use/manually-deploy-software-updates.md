---

title: "Implantar manualmente atualizações de software | Microsoft Docs"
description: "Para implantar atualizações manualmente, selecione atualizações no console do Configuration Manager e implante-as manualmente ou adicione atualizações a um grupo de atualização e implante o grupo."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.translationtype: Human Translation
ms.sourcegitcommit: 78524abd4c45f0b7402d6f1e85afc60bb72ab0ee
ms.openlocfilehash: d736715f1f2c92b4c91f156ecb8abe3513811a34
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017


---

#  <a name="BKMK_ManualDeploy"></a> Implantar atualizações de software manualmente  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Uma implantação manual de atualização de software é o processo de selecionar atualizações de software no console do Configuration Manager e iniciar manualmente o processo de implantação. Ou, você pode adicionar atualizações de software selecionadas a um grupo de atualização e implantar manualmente o grupo de atualização. Geralmente, você usará a implantação manual para atualizar os dispositivos do cliente com as atualizações de software necessárias antes de criar ADRs que gerenciarão implantações mensais e contínuas de atualização de software. Você também usará um método manual para implantar atualizações de software fora de banda. Se você precisar de ajuda para determinar qual método de implantação é adequado para você, consulte [Implantar atualizações de software](deploy-software-updates.md).

 As seções a seguir fornecem as etapas para implantar atualizações de software manualmente.  

##  <a name="BKMK_1SearchCriteria"></a> Etapa 1: Especificar critérios de pesquisa para atualizações de software  
 Potencialmente, existem milhares de atualizações de software exibidas no console do Configuration Manager. A primeira etapa no fluxo de trabalho para implantar manualmente atualizações de software é identificar aquelas que você deseja implantar. Por exemplo, você pode fornecer critérios que recuperam todas as atualizações de software necessárias em mais de 50 dispositivos de clientes e que têm uma classificação de atualização de software de **Segurança** ou **Crítico** .  

> [!IMPORTANT]  
>  O número máximo de atualizações de software que podem ser incluídas em uma única implantação de atualização de software é 1000.  

#### <a name="to-specify-search-criteria-for-software-updates"></a>Para especificar critérios de pesquisa para atualizações de software  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho Biblioteca de Software, expanda **Atualizações de Software**e clique em **Todas as Atualizações de Software**. As atualizações de software sincronizadas são exibidas.  

    > [!NOTE]  
    >  No nó **Todas as Atualizações de Software**, o Configuration Manager exibe somente atualizações de software com uma classificação **Crítico** e **Segurança** e que foram liberadas nos últimos 30 dias.  

3.  No painel de pesquisa, filtre para identificar as atualizações de software de que você precisa usando uma ou ambas das etapas a seguir:  

    -   Na caixa de texto de pesquisa, digite uma cadeia de caracteres de pesquisa que filtrará as atualizações de software. Por exemplo, digite a ID do artigo ou do boletim de uma atualização de software específica ou insira uma cadeia de caracteres que apareceria em um título para várias atualizações de software.  

    -   Clique em **Adicionar Critério**, selecione os critérios que deseja usar para filtrar atualizações de software, clique em **Adicionar**e forneça os valores para os critérios.  

4.  Clique em **Pesquisar** para filtrar as atualizações de software.  

    > [!TIP]  
    >  Você tem a opção de salvar os critérios de filtro na guia **Pesquisar** no grupo **Salvar** .  

##  <a name="BKMK_2UpdateGroup"></a> Etapa 2: Criar um grupo de atualização de software que contém as atualizações do software  
 Os grupos de atualização de software fornecem um método eficaz para organizar as atualizações de software em preparação para implantação. É possível adicionar as atualizações de software manualmente a um grupo de atualização de software ou o Configuration Manager pode adicioná-las automaticamente a um grupo de atualização de software novo ou existente usando uma ADR. Use os procedimentos a seguir para adicionar manualmente as atualizações de software a um novo grupo de atualização de software.  

#### <a name="to-manually-add-software-updates-to-a-new-software-update-group"></a>Para adicionar manualmente atualizações de software a um novo grupo de atualização de software  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho Biblioteca de Software, clique em **Atualizações de Software**.  

3.  Selecione as atualizações de software a serem adicionadas ao novo grupo de atualização de software.  

4.  Na guia **Início** , no grupo **Atualizar** , clique em **Criar Grupo de Atualização de Software**.  

5.  Especifique o nome do grupo de atualização de software e, opcionalmente, forneça uma descrição. Use o nome e a descrição que fornece informações suficientes para que você determine qual tipo de atualizações de software está no grupo de atualização de software. Para continuar, clique em **Criar**.  

6.  Clique no nó **Grupos de Atualização de Software** para exibir o novo grupo de atualização de software.  

7.  Selecione o grupo de atualização de software e, na guia **Início** , no grupo **Atualizar** , clique em **Mostrar Membros** para exibir uma lista de atualizações de software que estão incluídas no grupo.  

##  <a name="BKMK_3DownloadContent"></a> Etapa 3: Baixar o conteúdo para o grupo de atualização de software  
 Opcionalmente, para implantar as atualizações de software, você pode baixar o conteúdo para as atualizações de software incluídas no grupo de atualizações de software. Você pode optar por fazer isso para verificar se o conteúdo está disponível nos pontos de distribuição antes de implantar as atualizações de software. Isso ajudará a evitar problemas inesperados com o fornecimento de conteúdo. Você pode ignorar essa etapa, e o conteúdo será baixado e copiado para os pontos de distribuição como parte do processo de implantação. Use o procedimento a seguir para baixar o conteúdo para atualizações de software no grupo de atualização de software.  



#### <a name="to-download-content-for-the-software-update-group"></a>Para baixar conteúdo para o grupo de atualização de software
[!INCLUDE[downloadupdates](..\includes\downloadupdates.md)]
<!--- 1.  In the Configuration Manager console, click **Software Library**.  

2.  In the Software Library workspace, expand **Software Updates**, and click **Software Update Groups**.  

3.  Select the software update group for which you want to download content.  

4.  On the **Home** tab, in the **Update Group** group, click **Download**. The **Download Software Updates Wizard** opens.  

5.  On the **Deployment Package** page, configure the following settings:  

    1.  **Select deployment package**: Select this setting to use an existing deployment package for the software updates in the deployment.  

        > [!NOTE]  
        >  Software updates that have already been downloaded to the selected deployment package are not downloaded again.  

    2.  **Create a new deployment package**: Select this setting to create a new deployment package for the software updates in the deployment. Configure the following settings:  

        -   **Name**: Specifies the name of the deployment package. This must be a unique name that describes the package content. It is limited to 50 characters.  

        -   **Description**: Specifies the description of the deployment package. The package description provides information about the package contents and is limited to 127 characters.  

        -   **Package source**: Specifies the location of the software update source files.  Type a network path for the source location, for example, **\\\server\sharename\path**, or click **Browse** to find the network location. You must create the shared folder for the deployment package source files before you proceed to the next page.  

            > [!NOTE]  
            >  The deployment package source location that you specify cannot be used by another software deployment package.  

            > [!IMPORTANT]  
            >  The SMS Provider computer account and the user that is running the wizard to download the software updates must both have **Write** NTFS permissions on the download location. You should carefully restrict access to the download location in order to reduce the risk of attackers tampering with the software update source files.  

            > [!IMPORTANT]  
            >  You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. But if you do so, you must first copy the content from the original package source to the new package source location.  

     Click **Next**.  

6.  On the Distribution Points page, select the distribution points or distribution point groups that are used to host the software update files defined in the new deployment package, and then click **Next**.  

7.  On the Distribution Settings page, specify the following settings:  

    -   **Distribution priority**: Use this setting to specify the distribution priority for the deployment package. The distribution priority applies when the deployment package is sent to distribution points at child sites. Distribution packages are sent in priority order: **High**, **Medium**, or **Low**. Packages with identical priorities are sent in the order in which they were created. If there is no backlog, the package will process immediately regardless of its priority. By default, packages are sent using **Medium** priority.  

    -   **Distribute the content for this package to preferred distribution points**: Use this setting to enable on-demand content distribution to preferred distribution points. When this setting is enabled, the management point creates a trigger for the distribution manager to distribute the content to all preferred distribution points when a client requests the content for the package and the content is not available on any preferred distribution points. For more information about preferred distribution points and on-demand content, see [Content source location scenarios](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_CSLscenarios).  

    -   **Prestaged distribution point settings**: Use this setting to specify how you want to distribute content to prestaged distribution points. Choose one of the following options:  

        -   **Automatically download content when packages are assigned to distribution points**: Use this setting to ignore the prestage settings and distribute content to the distribution point.  

        -   **Download only content changes to the distribution point**: Use this setting to prestage the initial content to the distribution point, and then distribute content changes to the distribution point.  

        -   **Manually copy the content in this package to the distribution point**: Use this setting to always prestage content on the distribution point. This is the default setting.  

         For more information about prestaging content to distribution points, see [Use Prestaged content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

     Click **Next**.  

8.  On the Download Location page, specify location that Configuration Manager will use to download the software update source files. As needed, use the following options:  

    -   **Download software updates from the Internet**: Select this setting to download the software updates from the location on the Internet. This is the default setting.  

    -   **Download software updates from a location on the local network**: Select this setting to download software updates from a local folder or shared network folder. Use this setting when the computer running the wizard does not have Internet access.  

        > [!NOTE]  
        >  When you use this setting, download the software updates from any computer with Internet access, and then copy the software updates to a location on the local network that is accessible from the computer running the wizard.  

     Click **Next**.  

9. On the Language Selection page, specify the languages for which the selected software updates are to be downloaded, and then click **Next**. Configuration Manager downloads the software updates only if they are available in the selected languages. Software updates that are not language-specific are always downloaded.  

10. On the Summary page, verify the settings that you selected in the wizard, and then click **Next** to download the software updates.  

11. On the Completion page, verify that the software updates were successfully downloaded, and then click **Close**. --->

#### <a name="to-monitor-content-status"></a>Para monitorar o status do conteúdo
1. Para monitorar o status do conteúdo das atualizações de software, clique em **Monitoramento** no console do Configuration Manager.  

2. No espaço de trabalho Monitoramento, expanda **Status de Distribuição**e clique em **Status do Conteúdo**.  

3. Selecione o pacote e atualização de software que você identificou anteriormente para baixar as atualizações de software no grupo de atualização de software.  

4. Na guia **Início** , no grupo **Conteúdo** , clique em **Exibir Status**.  

##  <a name="BKMK_4DeployUpdateGroup"></a> Etapa 4: Implantar o grupo de atualização de software  
 Depois de determinar quais atualizações de software você pretende implantar e adicioná-las a um grupo de atualização de software, você poderá implantar manualmente as atualizações de software no grupo de atualização de software. Use o procedimento a seguir para implantar manualmente as atualizações de software em um grupo de atualização de software.  

#### <a name="to-manually-deploy-the-software-updates-in-a-software-update-group"></a>Para implantar manualmente as atualizações de software em um grupo de atualização de software  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho Biblioteca de Software, expanda **Atualizações de Software**e clique em **Grupos de Atualização de Software**.  

3.  Selecione o grupo de atualização de software que você deseja implantar.  

4.  Na guia **Início** , no grupo **Implantação** , clique em **Implantar**. O **Assistente para Implantar Atualizações de Software** se abre.  

5.  Na página Geral, defina as seguintes configurações:  

    -   **Nome**: especifique o nome da implantação. A implantação deve ter um nome exclusivo que descreva a finalidade da implantação e diferencie-a de outras implantações no site do Configuration Manager. Por padrão, o Configuration Manager fornece automaticamente um nome para a implantação no seguinte formato: **Atualizações de software da Microsoft -** <*data*><*hora*>  

    -   **Descrição:**especifique uma descrição para a implantação. A descrição fornece uma visão geral da implantação e qualquer outra informação relevante que ajude a identificá-la e a diferenciá-la entre outras no site do Configuration Manager. O campo de descrição é opcional, tem um limite de 256 caracteres e um valor em branco por padrão.  

    -   **Atualização de Software/Grupo de Atualização de Software**: verifique se o grupo de atualização de software exibido ou a atualização de software está correta.  

    -   **Selecionar Modelo de Implantação**: especifique se deseja aplicar um modelo de implantação salvo anteriormente. Você pode configurar um modelo de implantação para conter várias propriedades de implantação da atualização de software e aplicar o modelo ao implantar atualizações de software subsequentes para garantir a consistência em implantações semelhantes e economizar tempo.  

    -   **Coleção**: especifique a coleção para a implantação, conforme aplicável. Os membros da coleção recebem as atualizações de software que são definidas na implantação.  

6.  Na página Configurações de Implantação, defina as seguintes configurações:  

    -   **Tipo de implantação**: especifique o tipo de implantação para a implantação de atualização do software. Selecione **Necessário** para criar uma implantação de atualização de software obrigatória na qual as atualizações de software são instaladas automaticamente em clientes antes do prazo de uma instalação configurada. Selecione **Disponível** para criar uma implantação de atualização de software opcional que esteja disponível para que os usuários instalem do Centro de Software.  

        > [!IMPORTANT]  
        >  Depois de criar a implantação de atualização de software, você não poderá alterar o tipo de implantação.  

        > [!NOTE]  
        >  Um grupo de atualização de software implantado como **Obrigatório** será baixado em segundo plano e atenderá às configurações do BITS, se configurado.  
        > No entanto, os grupos de atualização de software implantados como **Disponíveis** serão baixados em primeiro plano e ignorarão as configurações de BITS.  

    -   **Usar Wake-on-LAN para ativar clientes para implantações obrigatórias**: especifique se o Wake on LAN deve ser habilitado no prazo para enviar pacotes de ativação para os computadores que exigem uma ou mais atualizações de software na implantação. Todos os computadores que estão no modo de suspensão no momento da instalação serão ativados para que a instalação da atualização de software seja iniciada. Clientes que estão no modo de suspensão e que não necessitam de atualizações de software na implantação não são iniciados. Por padrão, essa configuração não está habilitada e está disponível somente quando **Tipo de implantação** está definido como **Necessário**.  

        > [!WARNING]  
        >  Para usar essa opção, os computadores e as redes devem ser configurados para Wake on LAN.  

    -   **Nível de detalhe**: especifique o nível de detalhe para as mensagens de estado que são relatadas pelos computadores cliente.  

7.  Na página Agendamento, defina as seguintes configurações:  

    -   **Avaliação do agendamento**: especifique se os horários e prazos de instalação disponíveis são avaliados de acordo com a UTC ou no horário local do computador que executa o console do Configuration Manager.  

        > [!NOTE]  
        >  Quando você seleciona a hora local e seleciona **O mais breve possível** para o **Tempo disponível do software** ou o **Prazo de instalação**, a hora atual no computador que executa o console do Configuration Manager é usada para avaliar quando as atualizações estarão disponíveis ou quando serão instaladas em um cliente. Se o cliente estiver em um fuso horário diferente, essas ações ocorrerão quando o tempo do cliente atingir o tempo de avaliação.  

    -   **Tempo disponível do software**: selecione uma das configurações a seguir para especificar quando as atualizações de software estarão disponíveis para clientes:  

        -   **O mais breve possível**: selecione essa configuração para disponibilizar as atualizações de software na implantação aos clientes o mais breve possível. Quando a implantação é criada, a política de cliente é atualizada, os clientes são informados sobre a implantação no próximo ciclo de sondagem de política do cliente e as atualizações de software são disponibilizadas para instalação.  

        -   **Horário específico**: selecione essa configuração para disponibilizar as atualizações de software na implantação aos clientes, em uma data e hora específica. Quando a implantação é criada, a política do cliente é atualizada e os clientes são informados sobre a implantação em seu próximo ciclo de sondagem de política do cliente. No entanto, as atualizações de software na implantação não estão disponíveis para instalação até após a data e hora especificadas.  

    -   **Prazo de instalação**: selecione uma das seguintes configurações para especificar o prazo de instalação das atualizações de software na implantação:  

        > [!NOTE]  
        >  Você só pode configurar a definição do prazo de instalação quando **Tipo de implantação** está definido como **Obrigatório** na página Configurações de Implantação.  

        -   **O mais breve possível**: selecione essa configuração para instalar automaticamente as atualizações de software na implantação o mais breve possível.  

        -   **Horário específico**: selecione essa configuração para instalar automaticamente as atualizações de software na implantação, em uma data e hora específica.  

        > [!NOTE]  
        >  O prazo real de instalação é o horário específico que você configura mais um período de tempo aleatório de até 2 horas. Isso reduz o impacto potencial de todos os computadores cliente na coleção de destino que está instalando as atualizações de software na implantação ao mesmo tempo.  
        >   
        >  É possível configurar a definição do cliente **Agente de Computador** , **Desativar data limite aleatória** para desabilitar o atraso de aleatoriedade das atualizações de software necessárias. Para obter mais informações, consulte [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

8.  Na página Experiência do Usuário, defina as seguintes configurações:  

    -   **Notificações ao usuário**: especifique se quer exibir notificações das atualizações de software no Centro de Software no computador cliente no **Tempo disponível do software** configurado e se deseja exibir as notificações ao usuário nos computadores cliente. Quando o **Tipo de implantação** está definido como **Disponível** na página Configurações de implantação, não é possível selecionar **Ocultar no Centro de Software e todas as notificações**.  

    -   **Comportamento do prazo**: *somente disponível quando o **Tipo de implantação** *está definido como **Obrigatório** *na página Configurações de Implantação.*   
    Especifique o comportamento que deve ocorrer quando o prazo é alcançado para a implantação da atualização de software. Especifique se deseja instalar as atualizações de software na implantação. Especifique também se o sistema deve ser reiniciado após a instalação da atualização de software, independentemente de uma janela de manutenção configurada. Para obter mais informações sobre janelas de manutenção, consulte [Como usar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamento de reinício de dispositivo**: *somente disponível quando o **Tipo de implantação** *está definido como **Obrigatório** *na página Configurações de Implantação.*    
    Especifique se uma reinicialização do sistema em servidores e estações de trabalho deve ser suprimida depois que as atualizações de software são instaladas e uma reinicialização do sistema é necessária para concluir a instalação.  

        > [!IMPORTANT]  
        >  A supressão das reinicializações do sistema pode ser útil em ambientes de servidor ou para casos em que você não quer que os computadores que estão instalando as atualizações de software reiniciem por padrão. No entanto, isso pode deixar os computadores em um estado inseguro, ao passo que permitir uma reinicialização forçada ajuda a garantir a conclusão imediata da instalação da atualização de software.

    -   **Manuseio de filtro de gravação para dispositivos Windows Embedded**: ao implantar atualizações de software em dispositivos Windows Embedded com filtro de gravação habilitado, é possível especificar que a atualização de software seja instalada na sobreposição temporária e que as alterações sejam confirmadas mais tarde, na data limite da instalação ou durante uma janela de manutenção. Ao confirmar as alterações na data limite da instalação ou durante uma janela de manutenção, é necessário reinicializar. Dessa forma, as alterações permanecem no dispositivo.  

        > [!NOTE]  
        >  Ao implantar uma atualização de software em um dispositivo Windows Embedded, verifique se o dispositivo é membro de uma coleção com uma janela de manutenção configurada.  

    - **Comportamento de reavaliação da implantação de atualizações de software na reinicialização**: começando com a versão 1606 do Configuration Manager, é possível selecionar este ajuste para configurar as implantações de atualização de software para que os clientes executem uma verificação de conformidade de atualizações de software imediatamente após um cliente instalar atualizações de software e reiniciar. Isso permite que os clientes verifiquem atualizações de software adicionais que se tornam aplicáveis depois que eles são reiniciados e as instalem (e se tornem compatíveis) durante a mesma janela de manutenção.

9. Na página Alertas, configure como o Configuration Manager e o System Center Operations Manager gerarão alertas para essa implantação. Você só pode configurar alertas quando o **Tipo de implantação** está definido como **Obrigatório** na página Configurações de Implantação.  

    > [!NOTE]  
    >  Você pode verificar os alertas de atualizações de software recentes no nó **Atualizações de Software** no espaço de trabalho **Biblioteca de Software** .  

10. Na página Configurações de Download, defina as seguintes configurações:  

    -   Especifique se o cliente irá baixar e instalar as atualizações de software quando estiver conectado a uma rede lenta ou usando um local de conteúdos de fallback.  

    -   Especifique se o cliente deve baixar e instalar as atualizações de software por meio de um ponto de distribuição de fallback quando o conteúdo das atualizações de software não está disponível ou de um ponto de distribuição preferencial.  

    -   **Permitir que os clientes compartilhem conteúdo com outros clientes na mesma sub-rede**: especifique se deseja habilitar o uso do BranchCache para downloads de conteúdo. Para obter mais informações sobre o BranchCache, consulte [Fundamental concepts for content management (Conceitos fundamentais para o gerenciamento de conteúdo)](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    -   Especifique se os clientes que estão conectados à intranet deverão baixar atualizações de software do Microsoft Update se as atualizações de software não estiverem disponíveis nos pontos de distribuição.  

    -   Especifique se os clientes têm permissão para baixar após o prazo de uma instalação quando usam conexão de Internet limitada. Provedores de Internet ocasionalmente cobram por quantidade de dados que você envia e recebe quando está em uma conexão de Internet limitada.  

    > [!NOTE]  
    >  Os clientes solicitam o local do conteúdo de um ponto de gerenciamento de atualizações de software em uma implantação. O comportamento do download depende de como você configurou o ponto de distribuição, o pacote de implantação e as configurações desta página. Para obter mais informações, consulte [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

11. Se você realizou o [Etapa 3: Baixar o conteúdo para o grupo de atualização de software](#BKMK_3DownloadContent), as páginas Pacote de Implantação, Pontos de Distribuição e Seleção de Idioma não são exibidas, e você pode passar para a etapa 15 do assistente.  

    > [!IMPORTANT]  
    >  As atualizações de software previamente baixadas na biblioteca de conteúdo no servidor do site não são baixadas novamente. Isso é verdadeiro mesmo quando você cria um novo pacote de implantação para as atualizações de software. Se todas as atualizações de software já foram previamente baixadas, o assistente vai para a página **Seleção de Idioma** (etapa 15).  

12. Na página do Pacote de Implantação, selecione um pacote de implantação existente ou configure as seguintes definições para especificar um novo pacote de implantação:  

    1.  **Nome**: especifique o nome do pacote de implantação. Deve ser um nome exclusivo que descreva o conteúdo do pacote. Ele é limitado a 50 caracteres.  

    2.  **Descrição**: especifique uma descrição que forneça informações sobre o pacote de implantação. A descrição é limitada a 127 caracteres.  

    3.  **Origem do pacote**: especifique o local dos arquivos de origem de atualização do software.  Digite um caminho de rede para o local de origem, por exemplo, **\\\servidor\nome do compartilhamento\caminho**ou clique em **Procurar** para encontrar o local na rede. É necessário criar a pasta compartilhada para os arquivos de origem do pacote de implantação antes de ir para a próxima página.  

        > [!NOTE]  
        >  O local de origem do pacote de implantação especificado não poderá ser usado por outro pacote de implantação de software.  

        > [!IMPORTANT]  
        >  A conta do computador Provedor de SMS e o usuário que estiver executando o assistente para baixar as atualizações de software deverão ter permissões NTFS de **Gravação** no local de download. É necessário restringir o acesso ao local de download com atenção, para reduzir o risco de ataques de adulteração nos arquivos de origem de atualização de software.  

        > [!IMPORTANT]  
        >  Será possível alterar o local de origem do pacote nas propriedades do pacote de implantação depois que o Configuration Manager criar o pacote de implantação. Mas ao fazer isso, é necessário primeiro copiar o conteúdo da fonte da origem do pacote para o seu novo local de origem.  

    4.  **Prioridade de envio**: especifique a prioridade de envio do pacote de implantação. O Configuration Manager usa a prioridade de envio do pacote de implantação quando envia o pacote para pontos de distribuição. Os pacotes de implantação são enviados por ordem de prioridade: Alta, Média, ou Baixa. Pacotes com prioridades idênticas são enviados na ordem em que foram criados. Se não houver uma lista de pendências, o pacote será processado imediatamente, não importando qual seja a prioridade.  

13. Na página Pontos de Distribuição, especifique os pontos de distribuição ou grupos de pontos de distribuição que irão hospedar os arquivos de atualização de software. Para obter mais informações sobre pontos de distribuição, consulte [Configurações de ponto de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

14. Na página Local de Download, especifique se deseja baixar os arquivos de atualização de software da Internet ou de sua rede local. Defina as seguintes configurações:  

    -   **Baixe as atualizações de software da Internet**: selecione essa configuração para baixar as atualizações de software de um local específico na Internet. Essa configuração é habilitada por padrão.  

    -   **Baixar atualizações de software de um local na rede local**: selecione essa configuração para baixar atualizações de software de uma pasta local ou uma pasta de rede compartilhada. Essa configuração é útil quando o computador que executa o assistente não tem acesso à Internet. As atualizações de software podem ser baixadas preliminarmente de qualquer computador que tenha acesso à Internet e armazenadas em um local na rede local para acesso subsequente na instalação.  

15. Na página Seleção de Idioma, selecione os idiomas para os quais as atualizações de software selecionadas são baixadas. As atualizações de software só serão baixadas se estiverem disponíveis nos idiomas selecionados. Atualizações de software que não são específicas do idioma são sempre baixadas. Por padrão, o assistente seleciona os idiomas que você configurou nas propriedades de ponto de atualização de software. Pelo menos um idioma deve ser selecionado para ir para a próxima página. Quando você seleciona apenas os idiomas que não têm suporte de uma atualização de software, o download irá falhar para a atualização.  

16. Na página Resumo, verifique as configurações. Para salvar as configurações em um modelo de implementação, clique em **Salvar como Modelo**, digite um nome e selecione as configurações que você quer incluir no modelo e clique **Salvar**. Para alterar uma configuração, clique na página do assistente associado e altere a configuração.  

    > [!WARNING]  
    >  O nome do modelo pode consistir em caracteres ASCII alfanuméricos, bem como em **\\** (barra invertida) ou **‘** (aspa simples).  

17. Clique em **Próximo** para implantar a atualização de software.  

 Depois de concluir o assistente, o Configuration Manager baixará as atualizações de software na biblioteca de conteúdo no servidor do site, distribuirá as atualizações de software para os pontos de distribuição configurados e depois implantará o grupo de atualização de software dos clientes na coleção de destino. Para obter mais informações sobre o processo de implantação, veja [Software update deployment process](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).

## <a name="next-steps"></a>Próximas etapas
[Monitorar atualizações de software](monitor-software-updates.md)

