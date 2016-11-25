---
title: Pacotes e programas | System Center Configuration Manager
description: "Suporte para implantações que usam pacotes e programas ou aplicativos com o System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: caad0507-9913-415a-b13d-d36f8f0a1b80
caps.latest.revision: 8
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5303edf0fe8a3e322b52cabd116b1877a14f8821


---
# <a name="packages-and-programs-in-system-center-configuration-manager"></a>Pacotes e programas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager continua dando suporte a pacotes e programas usados no Configuration Manager 2007. Uma implantação que usa pacotes e programas pode ser mais adequada do que uma implantação que usa um aplicativo quando você implanta um dos seguintes:  

- Você deseja implantar aplicativos em servidores Linux e UNIX.  
- Scripts que não instalam um aplicativo em um computador, como um script para desfragmentar a unidade de disco do computador.  
- "Únicos" scripts que não precisam ser monitorados continuamente.  
- Scripts que são executados em um agendamento recorrente e que não usam a avaliação global.  
  
Quando migra pacotes de uma versão anterior do Configuration Manager, você pode implantá-los em sua hierarquia do Configuration Manager. Após a conclusão da migração, os pacotes são exibidos no nó **Pacotes** do espaço de trabalho **Biblioteca de Software** . Você pode modificar e implantar esses pacotes da mesma maneira como você fez usando a distribuição de software. O **Assistente para Importar Pacote de Definição** permanece no Configuration Manager para importar pacotes herdados. Anúncios são convertidos em implantações quando são migrados do Configuration Manager 2007 para uma hierarquia do Configuration Manager.  
  
> [!NOTE]  
>  Você pode usar o Package Conversion Manager do Microsoft System Center Configuration Manager para converter pacotes e programas em aplicativos do Configuration Manager.  
>   
>  Para obter mais informações, veja [Configuration Manager Package Conversion Manager](https://technet.microsoft.com/library/hh531519.aspx).  

Os pacotes podem usar alguns recursos novos do Configuration Manager, incluindo grupos de pontos de distribuição e monitoramento. Aplicativos do App-V (Microsoft Application Virtualization) não podem ser distribuídos usando pacotes e programas no Configuration Manager. Para distribuir aplicativos virtuais, você deve criá-los como aplicativos do Configuration Manager.  

##  <a name="create-a-package-and-program"></a>Para criar um pacote e programa  
 Use um desses procedimentos para ajudá-lo a criar ou importar pacotes e programas.  

### <a name="create-a-package-and-program-using-the-create-package-and-program-wizard"></a>Criar um pacote e programa usando o Assistente para Criar Pacote e Programa  

1.  No console do Configuration Manager, clique em **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Pacotes**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Pacote**.  

4.  Na página **Pacote** do Assistente para Criar Pacote e Programa, especifique as seguintes informações:  

    -   **Nome** - Especifique um nome para o pacote que tenha, no máximo, 50 caracteres.  

    -   **Descrição** - Opcionalmente, especifique uma descrição para este pacote com, no máximo, 128 caracteres.  

    -   **Fabricante** – opcionalmente, especifique o nome do fabricante para ajudá-lo a identificar o pacote no console do Configuration Manager. Este nome pode ter, no máximo, 32 caracteres.  

    -   **Idioma** - Opcionalmente, especifique a versão de idioma do pacote com, no máximo, 32 caracteres.  

    -   **Versão** - Opcionalmente, especifique um número de versão para o pacote com, no máximo, 32 caracteres.  

    -   **Este pacote contém arquivos de origem** - Essa configuração indica se o pacote exige que os arquivos de origem estejam presentes nos dispositivos cliente. Por padrão, essa caixa de seleção fica desmarcada e o Configuration Manager não usa pontos de distribuição para o pacote. Quando esta caixa de seleção estiver marcada, pontos de distribuição serão usados.  

    -   **Pasta de origem** - Se o pacote contiver arquivos de origem, clique em **Procurar** para abrir a caixa de diálogo **Definir Pasta de Origem** e especifique o local dos arquivos de origem do pacote.  

        > [!NOTE]  
        >  A conta de computador do servidor do site deve ter direitos de acesso de leitura para a pasta de origem especificada.  

5.  Na página **Tipo de Programa** do Assistente para Criar Pacote e Programa, selecione o tipo de programa a ser criado e clique em **Avançar**. É possível criar um programa para um computador ou dispositivo, ou ignorar esta etapa e criar um programa mais tarde.  

    > [!TIP]  
    >  Para criar um novo programa para um pacote existente, selecione o pacote e, na guia **Início** , no grupo **Pacote** , clique em **Criar Programa** para abrir o Assistente para Criar Programa.  

6.  Use um dos procedimentos a seguir para criar um programa padrão ou um programa do dispositivo.  
  
    #### <a name="create-a-standard-program"></a>Criar um programa padrão  
  
  1.  No **tipo de programa** página o **Criar Assistente de pacote e programa**, selecione **programa padrão**, e, em seguida, clique em **próximo**.     2.  Na página **Programa Padrão**, especifique as seguintes informações:  

        -   **Nome:** Especifique um nome para o programa com um máximo de 50 caracteres.  

            > [!NOTE]  
            >  O nome do programa deve ser exclusivo dentro de um pacote. Depois de criar um programa, você não pode modificar seu nome.  

        -   **Linha de comando** - Insira a linha de comando a ser usada para iniciar o programa ou clique em **Procurar** para navegar até o local do arquivo.  

             Se um nome de arquivo especificado não tiver uma extensão especificada, o Configuration Manager tentará usar .com, .exe e .bat como possíveis extensões.  

             Quando o programa é executado em um cliente, o Configuration Manager primeiro procura o nome do arquivo de linha de comando no pacote, em seguida, procura na pasta local do Windows e, por fim, procura no local *%path%*. Se o arquivo não for encontrado, o programa falhará.  

        -   **Pasta de inicialização** - Opcionalmente, use esse campo para especificar a pasta por meio da qual o programa é executado, com até 127 caracteres. Essa pasta pode ser um caminho absoluto no cliente ou um caminho relativo para a pasta do ponto de distribuição que contém o pacote.  

        -   **Executar** - Especifica o modo no qual o programa será executado nos computadores cliente. Selecione uma das seguintes opções:  

            -   **Normal** -o programa é executado no modo normal com base em padrões do sistema e programa. Este é o modo padrão.  

            -   **Minimizado** – o programa é executado minimizado em dispositivos cliente. Os usuários podem ver a atividade de instalação na área de notificação ou na barra de tarefas.  

            -   **Maximizado** – o programa é executado maximizado em dispositivos cliente. Os usuários verão todas as atividades da instalação.  

            -   **Hidden** – as execuções de programa ocultadas em dispositivos cliente. Os usuários não verão nenhuma atividade de instalação.  

        -   **O programa pode ser executado** - Especifique se o programa pode ser executado somente quando um usuário estiver conectado, executado somente quando nenhum usuário estiver conectado, ou executado sem levar em conta se um usuário está conectado no computador cliente.  

        -   **Modo de execução** - Especifique se o programa será executado com permissões administrativas ou com as permissões de usuários registrados no momento.  

        -   **Permitir que os usuários exibam e interajam com a instalação do programa** - Use essa configuração, se disponível, para especificar se deseja permitir que os usuários interajam com a instalação do programa. Essa caixa de seleção só estará disponível quando a opção **Somente quando nenhum usuário estiver conectado** ou **Se um usuário estiver conectado ou não** estiver marcada para **O programa pode ser executado** e **Executar com direitos administrativos** marcados no **Modo de execução**.  

        -   **Modo de unidade** - Especifica as informações sobre como esse programa será executado na rede. Escolha uma das seguintes opções:  

            -   **é executado com um nome UNC** -indica que o programa for executado com um nome de convenção Universal de nomenclatura (UNC). Essa é a configuração padrão.  

            -   **Requer a letra da unidade** -indica que o programa requer uma letra de unidade para qualificar totalmente o seu local. Para essa configuração, Configuration Manager pode usar qualquer letra da unidade disponível no cliente.  

            -   **Requer a letra de unidade específica (exemplo: Z)** -indica que o programa requer uma letra de unidade específica que você especificar para qualificar totalmente o seu local. Se a letra da unidade especificada já é usada em um cliente, o programa não será executado.  

        -   **Reconectar-se ao ponto de distribuição em log em** -Use esta caixa de seleção para indicar se o computador cliente se reconecta ao ponto de distribuição quando o usuário fizer logon. Por padrão, essa caixa de seleção está desmarcada.  

  3.  Sobre o **requisitos** página do Assistente de programa e criar pacote, especifique as seguintes informações:  

        -   **Executar outro programa primeiro** – você pode usar essa configuração para identificar um pacote e programa será executado antes desse pacote e programa será executado.  

        -   **Requisitos de plataforma** – Selecione **Este programa pode ser executado em qualquer plataforma** ou **Este programa pode ser executado somente nas plataformas especificadas** e escolha os sistemas operacionais que os clientes devem executar para poder instalar o pacote e o programa.  

        -   **Espaço em disco estimado** -Especifique a quantidade de espaço em disco que o programa de software precisa para poder ser executado no computador. Isso pode ser especificado como **Desconhecido** (a configuração padrão) ou como um número inteiro maior ou igual a zero. Se um valor for especificado, as unidades para o valor também devem ser especificadas.  

        -   **Tempo de execução máximo permitido (minutos)** – Especifica o tempo máximo que o programa está previsto para ser executado no computador cliente. Isso pode ser especificado como **Desconhecido** (a configuração padrão) ou como um número inteiro maior que zero.  

             Por padrão, esse valor é definido como 120 minutos.  

            > [!IMPORTANT]  
            >  Se você estiver usando as janelas de manutenção para a coleção em que este programa seja executado, um conflito pode ocorrer se o **tempo de execução máximo permitido** é maior que a janela de manutenção programada. No entanto, se o número máximo de tempo de execução é definido como **desconhecido**, o programa será iniciado para execução durante a janela de manutenção e continuarão sendo executados conforme o necessário depois que a janela de manutenção é fechada. Se o usuário define o tempo máximo de execução para um período específico que excede o comprimento de qualquer janela de manutenção disponível, o programa não será executado.  

             Se o valor for definido como **Desconhecido**, o Configuration Manager definirá o tempo de execução máximo permitido para 12 horas (720 minutos).  

            > [!NOTE]  
            >  Se o tempo de execução máximo (definido pelo usuário ou como o valor padrão) for excedido, o Configuration Manager interromperá o programa se a opção **Executar com direitos administrativos** estiver marcada e a opção **Permitir que os usuários exibam e interajam com a instalação do programa** não estiver marcada.  

  4.  Clique em **Avançar**.  
  
    #### <a name="create-a-device-program"></a>Criar um programa de dispositivo  
  
  1.  No **tipo de programa** página do **Criar Assistente de pacote e programa**, selecione **programa para dispositivo**, e, em seguida, clique em **próximo**.  

  2.  Na página **Programa para Dispositivo**, especifique o seguinte:  

        -   **Nome** – especifique um nome para o programa que tenha, no máximo, 50 caracteres.  

            > [!NOTE]  
            >  O nome do programa deve ser exclusivo em um pacote. Depois de criar um programa, não é possível modificar seu nome.  

        -   **Comentário** - Opcionalmente, especifique um comentário para este programa de dispositivo com, no máximo, 127 caracteres.  

        -   **Pasta de download** - Especifique o nome da pasta no dispositivo com Windows CE na qual serão armazenados os arquivos de origem do pacote. O valor padrão é **\Temp\\**.  

        -   **Linha de comando** - Insira a linha de comando a ser usada para iniciar o programa ou clique em **Procurar** para navegar até o local do arquivo.  

        -   **Executar linha de comando na pasta de download** – Selecione esta opção para executar o programa na pasta de download especificada anteriormente.  

        -   **Executar linha de comando nesta pasta** – Selecione esta opção para especificar uma pasta diferente na qual deseja executar o programa.  

    3.  Na página **Requisitos**, especifique o seguinte:  

        -   **Espaço em disco estimado** -Especifique a quantidade de espaço em disco necessário para o software. Isso será exibido aos usuários de dispositivos móveis antes que eles instalem o programa.  

        -   **Baixar programa** -Especifique as informações sobre quando este programa pode ser baixado em dispositivos móveis. Você pode especificar **O mais rápido possível**, **Somente em uma rede rápida**ou **Somente quando o dispositivo estiver encaixado**.  

        -   **Requisitos adicionais** - Especifique quaisquer requisitos adicionais para este programa. Eles serão exibidos aos usuários antes da instalação do software. Por exemplo, você poderia notificar os usuários que precisam para fechar todos os outros aplicativos antes de executar o programa.  

  4.  Clique em **Avançar**.  

  7.  Na página **Resumo**, examine as ações a serem executadas e conclua o assistente.  

 Verifique se o novo pacote e programa são exibidos no nó **Pacotes** do espaço de trabalho **Biblioteca de Software** .  

## <a name="create-a-package-and-program-from-a-package-definition-file"></a>Criar um pacote e programa de um arquivo de definição de pacote  

1.  No console do Configuration Manager, clique em **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Pacotes**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Pacote com base na Definição**.  

4.  Na página **Definição de Pacote** do Assistente para Criar Pacote da Definição, escolha um arquivo de definição de pacote existente ou clique em **Procurar** para abrir um novo arquivo de definição de pacote. Depois de especificar um novo arquivo de definição de pacote, selecione-o na lista **Definição de pacote** e clique em **Avançar**.  

5.  Na página **Arquivos de Origem**, especifique as informações sobre os arquivos de origem necessários para o pacote e programa e clique em **Avançar**.  

6.  Se o pacote exigir arquivos de origem, na página **Pasta de Origem**, especifique o local do qual os arquivos de origem devem ser obtidos e clique em **Avançar**.  

7.  Na página **Resumo**, examine as ações a serem executadas e conclua o assistente. O novo pacote e programa são exibidos no nó **Pacotes** do espaço de trabalho **Biblioteca de Software** .  

 Para obter mais informações sobre arquivos de definição de pacote, consulte [Sobre o formato de arquivo de definição de pacote](/sccm/apps/deploy-use/packages-and-programs#about-the-package-definition-file-format) neste tópico.  

##  <a name="deploy-packages-and-programs"></a>Implantar pacotes e programas  

1.  No console do Configuration Manager, clique em **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Pacotes**.  

3.  Selecione o pacote que você deseja implantar, e, em seguida, no **Home** guia de **implantação** clique em **implantar**.  

4.  Sobre o **geral** página do Assistente de implantação de Software, especifique o nome do pacote e programa que você deseja implantar, a coleção à qual você deseja implantar o pacote e programa e comentários opcionais para a implantação.  

     Selecione **usar grupos de pontos de distribuição padrão associados a esta coleção** se você deseja armazenar o conteúdo do pacote no grupo de ponto de distribuição de coleções padrão. Se você não associou a coleção selecionada a um grupo de pontos de distribuição, esta opção não estará disponível.  

5.  Na página **Conteúdo**, clique em **Adicionar** e selecione os pontos de distribuição ou grupos de pontos de distribuição nos quais deseja implantar o conteúdo associado a este pacote e este programa.  

6.  Na página **Configurações de Implantação**, escolha uma finalidade para essa implantação e especifique as opções de pacotes de ativação e conexões limitadas:  

    -   **Finalidade** - Escolha entre:  

        -   **Disponível** -se o aplicativo é implantado para um usuário, o usuário vê o pacote publicado e o programa no catálogo de aplicativos e pode solicitá-la sob demanda. Se o pacote e o programa é implantado em um dispositivo, o usuário verá no Centro de Software e instalá-lo sob demanda.  

        -   **Necessária** -o pacote e o programa é implantada automaticamente de acordo com o agendamento configurado. No entanto, um usuário pode acompanhar o status de implantação de pacote e programa e instalá-lo antes do prazo final usando o Centro de Software.  

    -   **Enviar pacotes de ativação** – se a finalidade da implantação for definida como **necessária** e essa opção for selecionada, um pacote de ativação será enviado aos computadores antes da instalação da implantação para ativar o computador da suspensão no prazo da instalação. Antes de usar essa opção, os computadores devem ser configurados para Wake On LAN.  

    -   Selecione **Permitir que clientes em uma conexão de Internet limitada baixem conteúdo após o prazo de instalação, o que pode incorrer custos adicionais**, se for necessário.  

    > [!NOTE]  
    >  A opção **Pré-implantar software no dispositivo primário do usuário** não está disponível quando você implanta um pacote e programa.  

7.  Na página **Agendamento**, configure quando este pacote e este programa serão implantados ou ficarão disponíveis para dispositivos clientes.  

     As opções dessa página variam dependendo se a ação de implantação é definida como **Disponível** ou **Obrigatória**.  

8.  Se a finalidade da implantação for definida como **necessária**, configurar o comportamento execute para o programa a partir de **Reexecutar comportamento** lista suspensa. Escolha dentre as seguintes opções:  

    |Reexecutar comportamento|Mais informações|  
    |--------------------|----------------------|  
    |Nunca executar novamente o programa implantado|O programa não será executado no cliente, mesmo que o programa falha originalmente ou os arquivos de programa são alterados.|  
    |Sempre executar novamente o programa|O programa será sempre executado no cliente quando a implantação é agendada, mesmo que o programa foi executado já com êxito. Isso pode ser útil quando você usa implantações recorrentes nas quais o programa é atualizado, por exemplo com um software antivírus.|  
    |Executar novamente se a tentativa anterior falhar|O programa será executado quando a implantação é agendada somente se ele falha na tentativa de execução anterior.|  
    |Executar novamente se a tentativa anterior tiver êxito|O programa será executado somente se ele anteriormente foi executado com êxito no cliente. Isso é útil ao usar anúncios recorrentes nos quais o programa é atualizado regularmente e, nos quais cada atualização exige que a atualização anterior seja instalada com êxito.|  

9. Na página **Experiência do Usuário** , especifique as seguintes informações:  

    -   **Permitir que os usuários executem o programa de forma independente de atribuições** – Se habilitado, os usuários podem instalar este software no Centro de Software, independentemente de qualquer hora de instalação agendada.  

    -   **Instalação de software** – Permite que o software seja instalado fora de qualquer janela de manutenção configurada.  

    -   **Reinicialização do sistema (se necessário para concluir a instalação)** – Se a instalação do software exigir uma reinicialização do dispositivo para ser concluída, permita que isso ocorra fora de qualquer janela de manutenção configurada.  

    -   **Dispositivos incorporados** - Ao implantar pacotes e programas em dispositivos com Windows Embedded habilitados para filtro de gravação, você pode especificar para instalar os pacotes e programas em sobreposição temporária e confirmar as alterações posteriormente, ou confirmar as alterações na data limite da instalação ou durante uma janela de manutenção. Ao confirmar as alterações na data limite da instalação ou durante uma janela de manutenção, é necessário reinicializar. Dessa forma, as alterações permanecem no dispositivo.  

        > [!NOTE]  
        >  Quando você implanta um pacote ou programa em um dispositivo Windows Embedded, certifique-se de que o dispositivo é um membro de uma coleção com uma janela de manutenção configurada. Para obter mais informações sobre como as janelas de manutenção são usadas na implantação de pacotes e programas em dispositivos Windows Embedded, consulte a seção [Criando aplicativos do Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md).  
  
10. Na página **Pontos de Distribuição** , especifique as seguintes informações:  

    -   **Opções de implantação** – Especifique as ações que um cliente deve tomar para executar o conteúdo do programa. Você pode especificar o comportamento quando o cliente está em um limite de rede rápida ou um limite de rede lenta ou não confiável.  

    -   **Permitem que os clientes compartilhem conteúdo com outros clientes na mesma sub-rede** – Selecione esta opção para reduzir a carga na rede, permitindo que os clientes baixem conteúdo de outros clientes na rede que já baixaram e armazenaram em cache o conteúdo. Essa opção utiliza o Windows BranchCache e pode ser usada em computadores que executam o Windows Vista SP2 e posterior.  

    -   **Permitir que os clientes usem um local de origem de fallback para o conteúdo** – Se habilitado, os clientes podem pesquisar outros pontos de distribuição na hierarquia para ver existe algum conteúdo necessário se isso não estiver disponível no ponto de distribuição ou nos grupos de pontos de distribuição especificados.  

11. Na página **Resumo**, examine as ações a serem executadas e conclua o assistente.  

     Você pode exibir a implantação no nó **Implantações** do espaço de trabalho **Monitoramento** e no painel de detalhes da guia de implantação do pacote ao selecionar a implantação. Para obter mais informações, consulte [Monitorar pacotes e programas](/sccm/apps/deploy-use/packages-and-programs#monitor-packages-and-programs) neste tópico.  

> [!IMPORTANT]  
>  Se você tiver configurado a opção **Executar programa do ponto de distribuição** na página **Pontos de Distribuição** do Assistente para Implantar Software, não desmarque a opção **Copiar o conteúdo deste pacote em um compartilhamento de pacotes nos pontos de distribuição**, pois isso fará com que o pacote não esteja disponível para ser executado dos pontos de distribuição.  

##  <a name="monitor-packages-and-programs"></a>Monitorar pacotes e programas  
 Para monitorar implantações de pacote e programa, você usa os mesmos procedimentos adotados para monitorar os aplicativos, como detalhado em [Monitorar aplicativos](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

 Os pacotes e programas também incluem vários relatórios internos, que permitem monitorar informações sobre o status da implantação de pacotes e programas. Esses relatórios apresentam a categoria de relatório de **distribuição de Software – pacotes e programas** e **distribuição de Software – o pacote e o Status de implantação de programa**.  

 Para obter mais informações sobre como configurar relatórios no Configuration Manager, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  

##  <a name="manage-packages-and-programs"></a>Gerenciar pacotes e programas  
 No espaço de trabalho **Biblioteca de Software** , expanda **Gerenciamento de Aplicativos**, clique em **Pacotes**, selecione o pacote que deseja gerenciar e uma tarefa de gerenciamento na seguinte tabela:  

|Tarefa|Mais informações|  
|----------|----------------------|  
|**Criar arquivo de conteúdo de pré-teste**|Abre o pré-teste conteúdo assistente criar arquivo que permite que você crie um arquivo que contém o conteúdo do pacote que pode ser importado manualmente para outro site. Isso é útil em situações onde você tem pouca largura de banda entre o servidor do site e o ponto de distribuição.|  
|**Criar programa**|Abre o assistente criar programa que permite que você crie um novo programa para esse pacote.|  
|**Exportarar**|Abre o Assistente para Exportar Pacote, que permite exportar o pacote selecionado e seu conteúdo para um arquivo.<br /><br /> Para obter informações sobre como importar pacotes e programas, consulte Criar pacotes e programas neste tópico.|  
|**Implantar**|Abre o Assistente para Implantar Software, que permite implantar o pacote e o programa selecionado em uma coleção. Para obter mais informações, consulte [Implantar pacotes e programas](/sccm/apps/deploy-use/packages-and-programs#deploy-packages-and-programs) neste tópico.|  
|**Distribuir conteúdo**|Abre o Assistente para distribuir conteúdo que permite enviar o conteúdo que está associado ao pacote e programa para pontos de distribuição selecionados ou grupos de pontos de distribuição.|  
|**Atualizar Pontos de Distribuição**|Atualiza os pontos de distribuição com o conteúdo mais recente para o pacote e programa selecionados.|  

##  <a name="about-the-package-definition-file-format"></a>Sobre o formato de arquivo de definição de pacote  
 Arquivos de definição de pacote são scripts que você pode usar para ajudar a automatizar a criação de pacote e de programa com o Configuration Manager. Eles fornecem todas as informações de que o Configuration Manager precisa para criar um pacote e programa, exceto o local do pacote de arquivos de origem. Cada arquivo de definição de pacote é um arquivo de texto ASCII ou UTF-8 seguir o formato do arquivo. ini e que contém as seções descritas a seguir:  

###  <a name="pdf"></a>[PDF]  
 Esta seção identifica o arquivo como um arquivo de definição de pacote. Ele contém as seguintes informações:  

-   **Versão**: Especifica a versão do formato de arquivo de definição de pacote que é usado pelo arquivo. Isso corresponde à versão do System Management Server (SMS) ou Configuration Manager para que ele foi escrito. Essa entrada é necessária.  

###  <a name="package-definition"></a>[Package Definition]  
 Esta seção do arquivo de definição de pacote especifica as propriedades do pacote e programa. Ele fornece as seguintes informações:  

-   **Nome**: O nome do pacote, até 50 caracteres. Essa entrada é necessária.  

-   **Versão**: A versão do pacote, até 32 caracteres. Essa entrada é opcional.  

-   **Ícone**: Opcionalmente, o arquivo que contém o ícone a ser usado para esse pacote. Se especificado, esse ícone substituirá o ícone padrão do pacote no console do Configuration Manager.  

-   **Publisher**: O Editor do pacote, até 32 caracteres. Essa entrada é necessária.  

-   **Idioma**: A versão de idioma do pacote, até 32 caracteres. Essa entrada é necessária.  

-   **Comentário**: Um comentário opcional sobre o pacote, até 127 caracteres.  

-   **ContainsNoFiles**: Essa entrada indica se é ou não uma fonte associada ao pacote.  

-   **Programas**: Os programas definidos para esse pacote. Cada nome de programa corresponde a um **[programa]** seção nesse arquivo de definição de pacote. Essa entrada é necessária.  

     Exemplo:  

     `Programs=Typical, Custom, Uninstall`  

-   **MIFFileName**: O nome do arquivo de formato MIF (Management Information) que contém o status do pacote, até 50 caracteres.  

-   **MIFName**: O nome do pacote (para correspondência de MIF), até 50 caracteres.  

-   **MIFVersion**: O número de versão do pacote (para correspondência de MIF), até 32 caracteres.  

-   **MIFPublisher**: O Editor do software do pacote (para correspondência de MIF), até 32 caracteres.  

###  <a name="program"></a>[programa]  
 Para cada programa especificado no **programas** entrada o **[Package Definition]** seção, o arquivo de definição do pacote deve incluir uma seção [programa] que define esse programa. Cada seção do programa fornece as seguintes informações:  

-   **Nome**: O nome do programa, até 50 caracteres. Essa entrada deve ser exclusiva dentro de um pacote. Esse nome é usado ao definir anúncios. Em computadores cliente, o nome do programa é mostrado na **executar programas anunciados** no painel de controle. Essa entrada é necessária.  

-   **Ícone**: Opcionalmente, especifica o arquivo que contém o ícone a ser usado para este programa. Se especificado, esse ícone substituirá o ícone de programa padrão no console Configuration Manager e será exibido nos computadores cliente quando o programa for anunciado.  

-   **Comentário**: Um comentário opcional sobre o programa, até 127 caracteres.  

-   **CommandLine**: Especifica a linha de comando para o programa, até 127 caracteres. O comando é relativo à pasta de origem do pacote. Essa entrada é necessária.  

-   **Inicialização**: Especifica a pasta de trabalho para o programa, até 127 caracteres. Essa entrada pode ser um caminho absoluto no computador cliente ou um caminho relativo à pasta de origem do pacote. Essa entrada é necessária.  

-   **Executar**: Especifica o modo do programa no qual o programa será executado. Você pode especificar **minimizado**, **maximizado**, ou **Hidden**. Se essa entrada não for incluída, o programa será executado no modo normal.  

-   **AfterRunning**: Especifica nenhuma ação especial que ocorre depois que o programa for concluído com êxito. Opções disponíveis são **SMSRestart**, **ProgramRestart**, ou **SMSLogoff**. Se essa entrada não for incluída, o programa não executará uma ação especial.  

-   **EstimatedDiskSpace**: Especifica a quantidade de espaço em disco exigido pelo programa de software para poder ser executado no computador. Isso pode ser especificado como **desconhecido** (a configuração padrão) ou como um número inteiro maior ou igual a zero. Se um valor for especificado, as unidades para o valor também devem ser especificadas.  

     Exemplo:  

     `EstimatedDiskSpace=38MB`  

-   **EstimatedRunTime**: Especifica a duração estimada (em minutos) que o programa está previsto para ser executado no computador cliente. Isso pode ser especificado como **desconhecido** (a configuração padrão) ou como um número inteiro maior que zero.  

     Exemplo:  

     `EstimatedRunTime=25`  

-   **SupportedClients**: Especifica os processadores e sistemas operacionais em que esse programa será executado. As plataformas especificadas devem ser separadas por vírgulas. Se essa entrada não for incluída, a verificação de plataforma com suporte será desabilitada para este programa.  

-   **SupportedClientMinVersionX**, **SupportedClientMaxVersionX**: Especifica o intervalo inicial e final para números de versão para os sistemas operacionais especificados no **SupportedClients** entrada.  

     Exemplo:  

    ```  
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999   
    ```  

-   **AdditionalProgramRequirements**: Se desejar fornece outras informações ou requisitos para computadores cliente, até 127 caracteres.  

-   **CanRunWhen**: Especifica o status do usuário que o programa requer para poder ser executado no computador cliente. Os valores disponíveis são **UserLoggedOn**, **NoUserLoggedOn**, ou **AnyUserStatus**. O valor padrão é **UserLoggedOn**.  

-   **UserInputRequired**: Especifica se o programa requer interação com o usuário. Os valores disponíveis são **True** ou **False**. O valor padrão é **True**. Essa entrada é definida como **False** se **CanRunWhen** não está definido como **UserLoggedOn**.  

-   **AdminRightsRequired**: Especifica se o programa requer credenciais administrativas no computador para poder executar. Os valores disponíveis são **True** ou **False**. O valor padrão é **False**. Essa entrada é definida como **True** se **CanRunWhen** não está definido como **UserLoggedOn**.  

-   **UseInstallAccount**: Especifica se o programa usa a conta de instalação do Software cliente quando ele é executado em computadores cliente. Por padrão, esse valor é **False**. Esse valor também está **False** se **CanRunWhen** é definido como **UserLoggedOn**.  

-   **DriveLetterConnection**: Especifica se o programa requer uma conexão de letra de unidade para os arquivos de pacote estão localizados no ponto de distribuição. Você pode especificar **True** ou **False**. O valor padrão é **False**, que permite que o programa usa uma conexão de convenção de nomenclatura Universal (UNC). Quando esse valor é definido como **True**, a próxima letra de unidade disponível será usada (começando com z e continuar para trás).  

-   **SpecifyDrive**: Opcionalmente, especifica uma letra de unidade que o programa requer para conectar-se aos arquivos de pacote no ponto de distribuição. Essa especificação força o uso de letra de unidade especificada para conexões de cliente para pontos de distribuição.  

-   **ReconnectDriveAtLogon**: Especifica se o computador for reconectado ao ponto de distribuição quando o usuário fizer logon. Os valores disponíveis são **True** ou **False**. O valor padrão é **False**.  

-   **DependentProgram**: Especifica um programa nesse pacote que deve ser executado antes do programa atual. Esta entrada usa o formato **DependentProgram**=<**NomeDoPrograma>**, em que **<NomeDoPrograma>\>** é a entrada do **Nome** do programa no arquivo de definição de pacote. Se não houver nenhum programa dependente, deixe essa entrada vazia.  

     Exemplo:  

     DependentProgram = administrador  
    DependentProgram =  

-   **Atribuição**: Especifica como o programa é atribuído aos usuários. Esse valor pode ser: **FirstUser,** somente o primeiro usuário que fizer logon executa o programa; ou **EveryUser,** cada usuário que efetua logon em cliente executa o programa. Quando **CanRunWhen** não está definido como **UserLoggedOn**, essa entrada é definida como **FirstUser**.  

-   **Desabilitado**: Especifica se este programa pode ser anunciado aos clientes. Os valores disponíveis são **True** ou **False**. O valor padrão é **False**.  



<!--HONumber=Nov16_HO1-->


