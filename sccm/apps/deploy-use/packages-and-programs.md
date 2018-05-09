---
title: Pacotes e programas
titleSuffix: Configuration Manager
description: Suporte para implantações que usam pacotes e programas ou aplicativos com o System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: caad0507-9913-415a-b13d-d36f8f0a1b80
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 6f34fd322e5f94550602d7883a0303d10059b702
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="packages-and-programs-in-system-center-configuration-manager"></a>Pacotes e programas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager continua dando suporte a pacotes e programas usados no Configuration Manager 2007. Uma implantação que usa pacotes e programas pode ser mais adequada do que uma implantação que usa um aplicativo quando você implanta um dos seguintes:  

- Aplicativos para servidores Linux e UNIX
- Scripts que não instalam um aplicativo em um computador, como um script para desfragmentar a unidade de disco do computador
- Scripts “únicos” que não precisam ser monitorados continuamente  
- Scripts que são executados em um agendamento recorrente e que não usam a avaliação global

Quando migra pacotes de uma versão anterior do Configuration Manager, você pode implantá-los em sua hierarquia do Configuration Manager. Após a conclusão da migração, os pacotes são exibidos no nó **Pacotes** do espaço de trabalho **Biblioteca de Software** .

É possível modificar e implantar esses pacotes da mesma maneira como você fez usando a distribuição de software. O **Assistente para Importar Pacote de Definição** permanece no Configuration Manager para importar pacotes herdados. Anúncios são convertidos em implantações quando são migrados do Configuration Manager 2007 para uma hierarquia do Configuration Manager.  

> [!NOTE]  
>  Você pode usar o Package Conversion Manager do Microsoft System Center Configuration Manager para converter pacotes e programas em aplicativos do Configuration Manager.  
>   
>  Para obter mais informações, veja [Configuration Manager Package Conversion Manager](https://technet.microsoft.com/library/hh531519.aspx).  

Os pacotes podem usar alguns recursos novos do Configuration Manager, incluindo grupos de pontos de distribuição e monitoramento. Aplicativos do App-V (Microsoft Application Virtualization) não podem ser distribuídos usando pacotes e programas no Configuration Manager. Para distribuir aplicativos virtuais, é necessário criá-los como aplicativos do Configuration Manager.  

##  <a name="create-a-package-and-program"></a>Para criar um pacote e programa  
 Use um destes procedimentos para ajudá-lo a criar ou importar pacotes e programas.  

### <a name="create-a-package-and-program-using-the-create-package-and-program-wizard"></a>Criar um pacote e programa usando o Assistente para Criar Pacote e Programa  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Pacotes**.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Pacote**.  

4.  Sobre o **pacote** página do **Criar Assistente de pacote e programa**, especifique as seguintes informações:  

    -   **Nome**: especifique um nome para o pacote com, no máximo, 50 caracteres.  

    -   **Descrição**: especifique uma descrição para este pacote com, no máximo, 128 caracteres.  

    -   **Fabricante** (opcional): especifique um nome de fabricante para ajudá-lo a identificar o pacote no console do Configuration Manager. Este nome pode ter, no máximo, 32 caracteres.

    -   **Idioma** (opcional): especifique a versão do idioma do pacote com, no máximo, 32 caracteres.  

    -   **Versão** (opcional): especifique um número de versão para o pacote com, no máximo, 32 caracteres.

    -   **Este pacote contém arquivos de origem**: essa configuração indica se o pacote exige que os arquivos de origem estejam presentes nos dispositivos cliente. Por padrão, essa caixa de seleção fica desmarcada e o Configuration Manager não usa pontos de distribuição para o pacote. Quando esta caixa de seleção estiver marcada, pontos de distribuição serão usados.  

    -   **Pasta de origem**: se o pacote contiver arquivos de origem, escolha **Procurar** para abrir a caixa de diálogo **Definir Pasta de Origem** e especifique o local dos arquivos de origem do pacote.  

        > [!NOTE]  
        >  A conta de computador do servidor do site deve ter direitos de acesso de leitura para a pasta de origem especificada.  

5.  Na página **Tipo de Programa** do **Assistente para Criar Pacote e Programa**, selecione o tipo de programa a ser criado e escolha **Avançar**. É possível criar um programa para um computador ou dispositivo, ou ignorar esta etapa e criar um programa mais tarde.  

    > [!TIP]  
    >  Para criar um novo programa para um pacote existente, primeiro selecione o pacote. Em seguida, na guia **Início**, no grupo **Pacote**, escolha **Criar Programa** para abrir o **Assistente para Criar Programa**.  

6.  Use um dos procedimentos a seguir para criar um programa padrão ou um programa do dispositivo.  

    #### <a name="create-a-standard-program"></a>Criar um programa padrão  

  1.  Na página **Tipo de Programa** do **Assistente para Criar Pacote e Programa**, escolha **Programa Padrão** e, em seguida, **Avançar**.     

    2.  Na página **Programa Padrão**, especifique as seguintes informações:  

        -   **Nome:** Especifique um nome para o programa com um máximo de 50 caracteres.  

            > [!NOTE]  
            >  O nome do programa deve ser exclusivo dentro de um pacote. Depois de criar um programa, não é possível modificar seu nome.  

        -   **Linha de Comando**: insira a linha de comando a ser usada para iniciar o programa ou escolha **Procurar** para procurar o local do arquivo.  

            Se um nome de arquivo não tiver uma extensão especificada, o Configuration Manager tentará usar .com, .exe e .bat como possíveis extensões.  

             Quando o programa é executado em um cliente, o Configuration Manager primeiro procura o nome do arquivo de linha de comando no pacote, em seguida, procura na pasta local do Windows e, por fim, procura no local *%path%*. Se o arquivo não for encontrado, o programa falhará.  

        -   **Pasta de inicialização** (opcional): especifique a pasta por meio da qual o programa é executado, com até 127 caracteres. Essa pasta pode ser um caminho absoluto no cliente ou um caminho relativo à pasta do ponto de distribuição que contém o pacote.

        -   **Executar**: especifique o modo em que o programa é executado nos computadores cliente. Selecione uma das seguintes opções:  

            -   **Normal**: o programa é executado no modo normal, de acordo com os padrões do sistema e do programa. Este é o modo padrão.  

            -   **Minimizado**: o programa é executado de modo minimizado nos dispositivos cliente. Os usuários podem ver as atividades de instalação na área de notificação ou na barra de tarefas.  

            -   **Maximizado**: o programa é executado de modo maximizado nos dispositivos cliente. Os usuários veem todas as atividades de instalação.  

            -   **Oculto**: o programa é executado de modo oculto nos dispositivos cliente. Os usuários não veem nenhuma atividade de instalação.  

        -   **O programa pode ser executado**: especifique se o programa é executado somente quando um usuário está conectado, somente quando nenhum usuário está conectado ou independentemente de um usuário estar conectado ao computador cliente.  

        -   **Modo de execução**: especifique se o programa é executado com permissões administrativas ou com as permissões do usuário conectado no momento.  

        -   **Permitir que os usuários exibam e interajam com a instalação do programa**: use essa configuração, se disponível, para especificar se deseja permitir que os usuários interajam com a instalação do programa. Essa caixa de seleção só estará disponível quando a opção **Somente quando nenhum usuário estiver conectado** ou **Se um usuário estiver conectado ou não** estiver marcada em **O programa pode ser executado** e quando a opção **Executar com direitos administrativos** estiver marcada em **Modo de execução**.  

        -   **Modo de unidade**: especifique as informações sobre como esse programa é executado na rede. Escolha uma das seguintes opções:  

            -   **Executa com nome UNC**: especifique se o programa é executado com um nome UNC. Essa é a configuração padrão.  

            -   **Exige letra da unidade**: especifique se o programa exige uma letra da unidade para qualificar totalmente seu local. Para essa configuração, Configuration Manager pode usar qualquer letra da unidade disponível no cliente.  

            -   **Exige letra da unidade específica**: especifique se o programa exige uma letra da unidade específica especificada para qualificar totalmente seu local (por exemplo, **Z:**). Se a letra da unidade especificada já é usada em um cliente, o programa não será executado.  

        -   **Reconectar ao ponto de distribuição no logon**: use essa caixa de seleção para indicar se o computador cliente é reconectado ao ponto de distribuição quando o usuário se conecta. Por padrão, essa caixa de seleção está desmarcada.  

  3.  Na página **Requisitos** do **Assistente para Criar Pacote e Programa**, especifique as seguintes informações:  

        -   **Executar outro programa primeiro**: use essa configuração para identificar um pacote e um programa que são executados antes da execução desse pacote e programa.  

        -   **Requisitos de plataforma**: selecione **Este programa pode ser executado em qualquer plataforma** ou **Este programa pode ser executado somente nas plataformas especificadas** e, em seguida, escolha os sistemas operacionais que os clientes devem executar para poder instalar o pacote e o programa.  

        -   **Espaço em disco estimado**: especifique a quantidade de espaço em disco de que o programa de software precisa para ser executado no computador. Isso pode ser especificado como **desconhecido** (a configuração padrão) ou como um número inteiro maior ou igual a zero. Se um valor for especificado, as unidades para o valor também devem ser especificadas.  

        -   **Tempo de execução máximo permitido (minutos)**: especifique o tempo máximo previsto para que o programa seja executado no computador cliente. Isso pode ser especificado como **desconhecido** (a configuração padrão) ou como um número inteiro maior que zero.  

             Por padrão, esse valor é definido como 120 minutos.  

            > [!IMPORTANT]  
            >  Se você estiver usando janelas de manutenção para a coleção em que esse programa é executado, poderá ocorrer um conflito se o **Tempo de execução máximo permitido** for maior que a janela de manutenção agendada. No entanto, se o tempo de execução máximo for definido como **Desconhecido**, o programa iniciará sua execução durante a janela de manutenção e continuará sendo executado quando necessário depois que a janela de manutenção for fechada. Se o usuário definir o tempo de execução máximo como um período específico que excede a duração de uma janela de manutenção disponível, o programa não será executado.  

             Se o valor for definido como **Desconhecido**, o Configuration Manager definirá o tempo de execução máximo permitido como 12 horas (720 minutos).  

            > [!NOTE]  
            >  Se o tempo de execução máximo (definido pelo usuário ou como o valor padrão) for excedido, o Configuration Manager interromperá o programa se a opção **Executar com direitos administrativos** estiver marcada e a opção **Permitir que os usuários exibam e interajam com a instalação do programa** não estiver marcada.  

  4.  Escolha **Próxima**.  

    #### <a name="create-a-device-program"></a>Criar um programa de dispositivo  

  1.  Na página **Tipo de Programa** do **Assistente para Criar Pacote e Programa**, selecione **Programa para dispositivo** e escolha **Avançar**.  

  2.  Na página **Programa para Dispositivo**, especifique o seguinte:  

        -   **Nome**: especifique um nome para o programa com, no máximo, 50 caracteres.  

            > [!NOTE]  
            >  O nome do programa deve ser exclusivo em um pacote. Depois de criar um programa, não é possível modificar seu nome.  

        -   **Comentário** (opcional): especifique um comentário para esse programa de dispositivo com, no máximo, 127 caracteres.  

        -   **Pasta de download**: especifique o nome da pasta no dispositivo Windows CE na qual serão armazenados os arquivos de origem do pacote. O valor padrão é **\Temp\\**.  

        -   **Linha de Comando**: insira a linha de comando a ser usada para iniciar o programa ou escolha **Procurar** para procurar o local do arquivo.  

        -   **Executar linha de comando na pasta de download**: selecione essa opção para executar o programa na pasta de download especificada anteriormente.  

        -   **Executar linha de comando nesta pasta**: selecione essa opção para especificar outra pasta na qual o programa será executado.  

    3.  Na página **Requisitos**, especifique o seguinte:  

        -   **Espaço em disco estimado**: especifique a quantidade de espaço em disco necessária para o software. Isso será exibido aos usuários de dispositivos móveis antes da instalação do programa.  

        -   **Baixar programa**: especifique as informações sobre quando esse programa pode ser baixado em dispositivos móveis. Você pode especificar **O mais rápido possível**, **Somente em uma rede rápida**ou **Somente quando o dispositivo estiver encaixado**.  

        -   **Requisitos adicionais**: especifique os requisitos adicionais para esse programa. Eles serão exibidos aos usuários antes da instalação do software. Por exemplo, você poderia notificar os usuários que precisam para fechar todos os outros aplicativos antes de executar o programa.  

  4.  Escolha **Próxima**.  

  7.  Na página **Resumo**, examine as ações a serem executadas e conclua o assistente.  

 Verifique se o novo pacote e programa são exibidos no nó **Pacotes** do espaço de trabalho **Biblioteca de Software**.  

## <a name="create-a-package-and-program-from-a-package-definition-file"></a>Criar um pacote e programa de um arquivo de definição de pacote  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Pacotes**.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Pacote com base na Definição**.  

4.  Na página **Definição de Pacote** do **Assistente para Criar Pacote com base na Definição**, escolha um arquivo de definição de pacote existente ou escolha **Procurar** para abrir um novo arquivo de definição de pacote. Depois de especificar um novo arquivo de definição de pacote, selecione-o na lista **Definição de pacote** e escolha **Avançar**.  

5.  Na página **Arquivos de Origem**, especifique as informações sobre os arquivos de origem necessários para o pacote e o programa e escolha **Avançar**.  

6.  Se o pacote exigir arquivos de origem, na página **Pasta de Origem**, especifique o local do qual os arquivos de origem devem ser obtidos e escolha **Avançar**.  

7.  Na página **Resumo**, examine as ações a serem executadas e conclua o assistente. O novo pacote e programa são exibidos no nó **Pacotes** do espaço de trabalho **Biblioteca de Software**.  

 Para obter mais informações sobre arquivos de definição de pacote, consulte [Sobre o formato de arquivo de definição de pacote](/sccm/apps/deploy-use/packages-and-programs#about-the-package-definition-file-format) neste tópico.  

##  <a name="deploy-packages-and-programs"></a>Implantar pacotes e programas  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Pacotes**.  

2.  Selecione o pacote que você deseja implantar e, na guia **Início** no grupo **Implantação**, escolha **Implantar**.  

3.  Na página **Geral** do **Assistente para Implantar Software**, especifique o nome do pacote e do programa que você deseja implantar, a coleção na qual você deseja implantar o pacote e o programa, bem como comentários opcionais para a implantação.  

     Selecione **usar grupos de pontos de distribuição padrão associados a esta coleção** se você deseja armazenar o conteúdo do pacote no grupo de ponto de distribuição de coleções padrão. Se você não tiver associado a coleção selecionada a um grupo de pontos de distribuição, essa opção não estará disponível.  

4.  Na página **Conteúdo**, escolha **Adicionar** e selecione os pontos de distribuição ou os grupos de pontos de distribuição nos quais você deseja implantar o conteúdo associado a esse pacote e esse programa.  

5.  Na página **Configurações de Implantação**, escolha uma finalidade para essa implantação e especifique as opções de pacotes de ativação e conexões limitadas:  

    -   **Finalidade**: escolha entre:  

        -   **Disponível**: se o aplicativo for implantado em um usuário, o usuário verá o pacote e o programa publicados no Catálogo de Aplicativos e poderá solicitá-los sob demanda. Se o pacote e o programa forem implantados em um dispositivo, o usuário os verá no Centro de Software e poderá instalá-los sob demanda.  

        -   **Obrigatória**: o pacote e o programa são implantados automaticamente, de acordo com o agendamento configurado. No entanto, um usuário pode acompanhar o status de implantação de pacote e programa e instalá-lo antes do prazo final usando o Centro de Software.  

    -   **Enviar pacotes de ativação**: se a finalidade da implantação estiver definida como **Obrigatória** e essa opção estiver selecionada, um pacote de ativação será enviado aos computadores antes que a implantação seja instalada para ativar o computador da suspensão na hora limite da instalação. Antes de usar essa opção, os computadores devem ser configurados para Wake On LAN.  

    -  **Permitir que os clientes com uma conexão de Internet limitada baixem conteúdo após a hora limite da instalação, o que poderá incorrer custos adicionais**: selecione essa opção, se necessário.  

    > [!NOTE]  
    >  A opção **Pré-implantar software no dispositivo primário do usuário** não está disponível quando você implanta um pacote e programa.  

6.  Na página **Agendamento**, configure quando este pacote e este programa serão implantados ou ficarão disponíveis para dispositivos clientes.  

     As opções dessa página variam dependendo se a ação de implantação é definida como **Disponível** ou **Obrigatória**.  

7.  Se a finalidade da implantação for definida como **Obrigatória**, configure o comportamento da nova execução para o programa no menu suspenso **Comportamento da nova execução**. Escolha dentre as seguintes opções:  

    |Reexecutar comportamento|Mais informações|  
    |--------------------|----------------------|  
    |Nunca executar novamente o programa implantado|O programa não será executado novamente no cliente, mesmo se o programa tiver falhado originalmente ou se os arquivos de programa tiverem sido alterados.|  
    |Sempre executar novamente o programa|O programa será sempre executado novamente no cliente quando a implantação for agendada, mesmo se o programa já tiver sido executado com êxito. Isso pode ser útil quando você usa implantações recorrentes nas quais o programa é atualizado, por exemplo com um software antivírus.|  
    |Executar novamente se a tentativa anterior falhar|O programa será executado novamente quando a implantação for agendada somente se ele falhar na tentativa de execução anterior.|  
    |Executar novamente se a tentativa anterior tiver êxito|O programa será executado novamente somente se tiver sido executado com êxito no cliente anteriormente. Isso é útil ao usar anúncios recorrentes nos quais o programa é atualizado regularmente e, nos quais cada atualização exige que a atualização anterior seja instalada com êxito.|  

8. Na página **Experiência do Usuário** , especifique as seguintes informações:  

    -   **Permitir que os usuários executem o programa de forma independente das atribuições**: se essa opção estiver habilitada, os usuários poderão instalar esse software no Centro de Software, independentemente da hora de instalação agendada.  

    -   **Instalação de software**: permite que o software seja instalado fora de qualquer janela de manutenção configurada.  

    -   **Reinicialização do sistema (se necessário para conclusão da instalação)**: se a instalação do software exigir uma reinicialização do dispositivo para ser concluída, permita que isso ocorra fora das janelas de manutenção configuradas.  

    -   **Dispositivos inseridos**: ao implantar pacotes e programas em dispositivos Windows Embedded habilitados para filtro de gravação, é possível especificar se os pacotes e os programas serão instalados na sobreposição temporária e confirmar as alterações mais tarde. Como alternativa, confirme as alterações na hora limite da instalação ou durante uma janela de manutenção. Ao confirmar as alterações na hora limite da instalação ou durante uma janela de manutenção, uma reinicialização é necessária e as alterações são persistidas no dispositivo.  

        > [!NOTE]  
        >  Quando você implanta um pacote ou programa em um dispositivo Windows Embedded, certifique-se de que o dispositivo é um membro de uma coleção com uma janela de manutenção configurada. Para obter mais informações sobre como as janelas de manutenção são usadas na implantação de pacotes e programas em dispositivos Windows Embedded, consulte a seção [Criando aplicativos do Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md).  

9. Na página **Pontos de Distribuição** , especifique as seguintes informações:  

    -   **Opções de implantação**: especifique as ações que um cliente deve executar para executar o conteúdo do programa. Você pode especificar o comportamento quando o cliente está em um limite de rede rápida ou um limite de rede lenta ou não confiável.  

    -   **Permitir que os clientes compartilhem conteúdo com outros clientes na mesma sub-rede**: selecione essa opção para reduzir a carga na rede, permitindo que os clientes baixem conteúdo de outros clientes na rede que já baixaram e armazenaram em cache o conteúdo. Essa opção utiliza o Windows BranchCache e pode ser usada em computadores que executam o Windows Vista SP2 e posterior.  

    -   **Permitir que os clientes usem um local de origem de fallback para o conteúdo**:  

        -  **Versões anteriores a 1610**: é possível marcar a caixa de seleção **Permitir local de origem de fallback para o conteúdo** para permitir que os clientes fora desses grupos de limite executem fallback e usem o ponto de distribuição como um local de origem para o conteúdo quando nenhum outro ponto de distribuição estiver disponível.

        - **Versão 1610 e posterior**: não é mais possível configurar a opção **Permitir local de origem de fallback para o conteúdo**.  Em vez disso, você configura as relações entre grupos de limite que determinam quando um cliente pode iniciar a pesquisa de uma localização de fonte de conteúdo válida em grupos de limite adicionais.

10. Na página **Resumo**, examine as ações a serem executadas e conclua o assistente.  

     Você pode exibir a implantação no nó **Implantações** do espaço de trabalho **Monitoramento** e no painel de detalhes da guia de implantação do pacote ao selecionar a implantação. Para obter mais informações, consulte [Monitorar pacotes e programas](/sccm/apps/deploy-use/packages-and-programs#monitor-packages-and-programs) neste tópico.  

> [!IMPORTANT]  
>  Se você tiver configurado a opção **Executar programa do ponto de distribuição** na página **Pontos de Distribuição** do **Assistente para Implantar Software**, não desmarque a opção **Copiar o conteúdo deste pacote para um compartilhamento de pacotes nos pontos de distribuição**, pois isso fará com que o pacote não esteja disponível para ser executado por meio dos pontos de distribuição.  

##  <a name="monitor-packages-and-programs"></a>Monitorar pacotes e programas  
 Para monitorar as implantações de pacote e programa, use os mesmos procedimentos adotados para monitorar os aplicativos, conforme detalhado em [Monitorar aplicativos](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

 Os pacotes e os programas também incluem vários relatórios internos, que permitem monitorar informações sobre o status da implantação de pacotes e programas. Esses relatórios apresentam a categoria de relatório de **distribuição de Software – pacotes e programas** e **distribuição de Software – o pacote e o Status de implantação de programa**.  

 Para obter mais informações sobre como configurar relatórios no Configuration Manager, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  

##  <a name="manage-packages-and-programs"></a>Gerenciar pacotes e programas  
 No espaço de trabalho **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos**, escolha **Pacotes**, escolha o pacote que você deseja gerenciar e, em seguida, uma tarefa de gerenciamento na seguinte tabela:  

|Tarefa|Mais informações|  
|----------|----------------------|  
|**Criar arquivo de conteúdo de pré-teste**|Abre o **Assistente para Criar Arquivo de Conteúdo Pré-teste**, que permite criar um arquivo que contém o conteúdo do pacote que pode ser importado manualmente para outro site. Isso é útil em situações onde você tem pouca largura de banda entre o servidor do site e o ponto de distribuição.|  
|**Criar programa**|Abre o **Assistente para Criar Programa**, que permite criar um novo programa para esse pacote.|  
|**Exportarar**|Abre o **Assistente para Exportar Pacote**, que permite exportar o pacote selecionado e seu conteúdo para um arquivo.<br /><br /> Para obter informações sobre como importar pacotes e programas, consulte [Criar pacotes e programas](/sccm/apps/deploy-use/packages-and-programs#create-packages-and-programs) neste tópico.|  
|**Implantar**|Abre o **Assistente para Implantar Software**, que permite implantar o pacote e o programa selecionados em uma coleção. Para obter mais informações, consulte [Implantar pacotes e programas](/sccm/apps/deploy-use/packages-and-programs#deploy-packages-and-programs) neste tópico.|  
|**Distribuir Conteúdo**|Abre o **Assistente para Distribuir Conteúdo**, que permite enviar o conteúdo associado ao pacote e ao programa para pontos de distribuição ou grupos de pontos de distribuição selecionados.|  
|**Atualizar Pontos de Distribuição**|Atualiza os pontos de distribuição com o conteúdo mais recente para o pacote e programa selecionados.|  

##  <a name="about-the-package-definition-file-format"></a>Sobre o formato de arquivo de definição de pacote  
 Arquivos de definição de pacote são scripts que você pode usar para ajudar a automatizar a criação de pacote e de programa com o Configuration Manager. Eles fornecem todas as informações de que o Configuration Manager precisa para criar um pacote e um programa, exceto o local dos arquivos de origem do pacote. Cada arquivo de definição de pacote é um arquivo de texto ASCII ou UTF-8 que usa o formato de arquivo .ini e que contém as seguintes seções:  

###  <a name="pdf"></a>[PDF]  
 Esta seção identifica o arquivo como um arquivo de definição de pacote. Ele contém as seguintes informações:  

-   **Versão**: especifique a versão do formato de arquivo de definição de pacote usada pelo arquivo. Isso corresponde à versão do System Management Server (SMS) ou Configuration Manager para que ele foi escrito. Essa entrada é necessária.  

###  <a name="package-definition"></a>[Package Definition]  
 Especifique as propriedades do pacote e do programa. Ele fornece as seguintes informações:  

-   **Nome**: O nome do pacote, até 50 caracteres.  

-   **Versão** (opcional): a versão do pacote, com até 32 caracteres.  

-   **Ícone** (opcional): o arquivo que contém o ícone a ser usado para esse pacote. Se for especificado, esse ícone substituirá o ícone padrão do pacote no console do Configuration Manager.

-   **Publisher**: O Editor do pacote, até 32 caracteres.

-   **Idioma**: A versão de idioma do pacote, até 32 caracteres.

-   **Comentário** (opcional): um comentário sobre o pacote, com até 127 caracteres.

-   **ContainsNoFiles**: Essa entrada indica se é ou não uma fonte associada ao pacote.  

-   **Programas**: os programas definidos para esse pacote. Cada nome de programa corresponde a um **[programa]** seção nesse arquivo de definição de pacote.  

     Exemplo:  

     `Programs=Typical, Custom, Uninstall`  

-   **MIFFileName**: O nome do arquivo de formato MIF (Management Information) que contém o status do pacote, até 50 caracteres.  

-   **MIFName**: O nome do pacote (para correspondência de MIF), até 50 caracteres.  

-   **MIFVersion**: O número de versão do pacote (para correspondência de MIF), até 32 caracteres.  

-   **MIFPublisher**: O Editor do software do pacote (para correspondência de MIF), até 32 caracteres.  

###  <a name="program"></a>[programa]  
 Para cada programa especificado na entrada **Programas** da seção **[Definição de Pacote]**, o arquivo de definição de pacote deve incluir uma seção [Programa] que define o programa. Cada seção do programa fornece as seguintes informações:  

-   **Nome**: O nome do programa, até 50 caracteres. Essa entrada deve ser exclusiva dentro de um pacote. Esse nome é usado ao definir anúncios. Em computadores cliente, o nome do programa é mostrado na **executar programas anunciados** no painel de controle.  

-   **Ícone** (opcional): especifique o arquivo que contém o ícone a ser usado para esse programa. Se for especificado, esse ícone substituirá o ícone padrão do programa no console do Configuration Manager e será exibido nos computadores cliente quando o programa for anunciado.

-   **Comentário** (opcional): um comentário sobre o programa, com até 127 caracteres.

-   **CommandLine**: especifique a linha de comando para o programa, em até 127 caracteres. O comando é relativo à pasta de origem do pacote.

-   **StartIn**: especifique a pasta de trabalho para o programa, em até 127 caracteres. Essa entrada pode ser um caminho absoluto no computador cliente ou um caminho relativo à pasta de origem do pacote.

-   **Executar**: especifique o modo de programa no qual o programa é executado. Você pode especificar **minimizado**, **maximizado**, ou **Hidden**. Se essa entrada não for incluída, o programa será executado no modo normal.  

-   **AfterRunning**: especifique uma ação especial que ocorre depois que o programa é concluído com êxito. Opções disponíveis são **SMSRestart**, **ProgramRestart**, ou **SMSLogoff**. Se essa entrada não for incluída, o programa não executará uma ação especial.  

-   **EstimatedDiskSpace**: especifique a quantidade de espaço em disco de que o programa de software precisa para ser executado no computador. Isso pode ser especificado como **desconhecido** (a configuração padrão) ou como um número inteiro maior ou igual a zero. Se um valor for especificado, as unidades para o valor também devem ser especificadas.  

     Exemplo:  

     `EstimatedDiskSpace=38MB`  

-   **EstimatedRunTime**: especifique a duração estimada (em minutos) para o programa ser executado no computador cliente. Isso pode ser especificado como **desconhecido** (a configuração padrão) ou como um número inteiro maior que zero.  

     Exemplo:  

     `EstimatedRunTime=25`  

-   **SupportedClients**: especifique os processadores e sistemas operacionais nos quais esse programa é executado. As plataformas especificadas devem ser separadas por vírgulas. Se essa entrada não for incluída, a verificação de plataforma com suporte será desabilitada para esse programa.  

-   **SupportedClientMinVersionX**, **SupportedClientMaxVersionX**: especifique o intervalo inicial e final para os números de versão dos sistemas operacionais especificados na entrada **SupportedClients**.  

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

-   **AdditionalProgramRequirements** (opcional): forneça outras informações ou outros requisitos para os computadores cliente, em até 127 caracteres.

-   **CanRunWhen**: especifique o status do usuário de que o programa precisa para ser executado no computador cliente. Os valores disponíveis são **UserLoggedOn**, **NoUserLoggedOn**, ou **AnyUserStatus**. O valor padrão é **UserLoggedOn**.  

-   **UserInputRequired**: especifique se o programa exige a interação com o usuário. Os valores disponíveis são **True** ou **False**. O valor padrão é **True**. Essa entrada é definida como **False** se **CanRunWhen** não está definido como **UserLoggedOn**.  

-   **AdminRightsRequired**: especifique se o programa exige credenciais administrativas no computador para ser executado. Os valores disponíveis são **True** ou **False**. O valor padrão é **False**. Essa entrada é definida como **True** se **CanRunWhen** não está definido como **UserLoggedOn**.  

-   **UseInstallAccount**: especifique se o programa usa a Conta de Instalação do Software Cliente quando ele é executado nos computadores cliente. Por padrão, esse valor é **False**. Esse valor também está **False** se **CanRunWhen** é definido como **UserLoggedOn**.  

-   **DriveLetterConnection**: especifique se o programa exige uma conexão de letra da unidade para os arquivos de pacote localizados no ponto de distribuição. Você pode especificar **True** ou **False**. O valor padrão é **False**, o que habilita o programa usar uma conexão UNC. Quando esse valor for definido como **True**, a próxima letra da unidade disponível será usada (começando com Z: e continuando com as anteriores).  

-   **SpecifyDrive** (opcional): especifique uma letra da unidade de que o programa precisa para se conectar aos arquivos de pacote no ponto de distribuição. Essa especificação força o uso de letra de unidade especificada para conexões de cliente para pontos de distribuição.

-   **ReconnectDriveAtLogon**: especifique se o computador é reconectado ao ponto de distribuição quando o usuário se conecta. Os valores disponíveis são **True** ou **False**. O valor padrão é **False**.  

-   **DependentProgram**: especifique um programa nesse pacote que deve ser executado antes do programa atual. Esta entrada usa o formato **DependentProgram**=<**NomeDoPrograma>**, em que **<NomeDoPrograma>\>** é a entrada do **Nome** do programa no arquivo de definição de pacote. Se não houver nenhum programa dependente, deixe essa entrada vazia.  

     Exemplo:  

     DependentProgram = administrador  
    DependentProgram =  

-   **Atribuição**: especifique como o programa é atribuído aos usuários. Esse valor pode ser: **FirstUser** (somente o primeiro usuário que se conecta ao cliente executa o programa) ou **EveryUser** (todos os usuários que se conectam executam o programa). Quando **CanRunWhen** não está definido como **UserLoggedOn**, essa entrada é definida como **FirstUser**.  

-   **Desabilitado**: especifique se esse programa pode ser anunciado para os clientes. Os valores disponíveis são **True** ou **False**. O valor padrão é **False**.  
