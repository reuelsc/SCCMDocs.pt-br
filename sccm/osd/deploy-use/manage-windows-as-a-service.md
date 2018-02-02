---
title: "Gerenciar o Windows como serviço "
titleSuffix: Configuration Manager
description: "Exibir o estado do Windows como serviço usando o Configuration Manager, criar planos de manutenção para formar anéis de implantação e exibir alertas quando os clientes do Windows 10 estiverem próximos do fim do suporte."
ms.custom: na
ms.date: 03/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da1e687b-28f6-43c4-b14a-ff2b76e60d24
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: a67d75f27cbc2d53cc5d8c418e25232d88b4f067
ms.sourcegitcommit: db9978135d7a6455d83dbe4a5175af2bdeaeafd8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/22/2018
---
# <a name="manage-windows-as-a-service-using-system-center-configuration-manager"></a>Gerenciar o Windows como um serviço usando o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


 No System Center Configuration Manager, é possível exibir o estado do Windows como serviço em seu ambiente, criar planos de serviço para formar anéis de implantação e garantir que os sistemas com o branch atual do Windows 10 permaneçam atualizados quando novos builds forem lançados. Além disso, é possível exibir alertas quando os clientes do Windows 10 estiverem próximos do fim do suporte para o build do CB (Branch Atual) ou do CBB (Branch Atual para Negócios).  

 Para obter mais informações sobre opções de serviço do Windows 10, veja  [Opções para atualizações de serviço do Windows 10](https://technet.microsoft.com/library/mt598226\(v=vs.85\).aspx).  

 Use as seguintes seções para gerenciar o Windows como serviço.

##  <a name="BKMK_Prerequisites"></a> Pré-requisitos  
 Para ver os dados no painel de serviço do Windows 10, faça o seguinte:  

-   Computadores Windows 10 devem usar as atualizações de software do Configuration Manager com o WSUS (Windows Server Update Services) para o gerenciamento de atualização de software. Quando os computadores usarem o Windows Update for Business (ou Windows Insiders) para o gerenciamento de atualização de software, o computador não será avaliado nos planos de serviço do Windows 10. Para obter mais informações, consulte [Integration with Windows Update for Business in Windows 10](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

-   O WSUS 4.0 com o [hotfix 3095113](https://support.microsoft.com/kb/3095113) deve ser instalado em seus pontos de atualização de software e servidores do site. Isso adiciona a classificação de atualização de software **Atualizações** . Para obter mais informações, consulte [Pré-requisitos para atualizações de software](../../sum/plan-design/prerequisites-for-software-updates.md).  

-   O WSUS 4.0 com o [hotfix 3159706](https://support.microsoft.com/kb/3159706) deve estar instalado em seus pontos de atualização de software e servidores de sites para atualizar computadores para a Atualização de Aniversário do Windows 10, bem como para versões posteriores. Há etapas manuais descritas no artigo de suporte que você precisa seguir para instalar esse hotfix. Para obter mais informações, consulte o [Blog do Enterprise Mobility & Security](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/05/update-your-configmgr-1606-sup-servers-to-deploy-the-windows-10-anniversary-update/).

-   Habilite a Descoberta de Pulsação. Os dados exibidos no painel de serviço do Windows 10 são encontrados por meio da descoberta. Para obter mais informações, consulte [Configure Heartbeat Discovery](../../core/servers/deploy/configure/configure-discovery-methods.md#BKMK_ConfigHBDisc).  

     As seguintes informações de branch e build do Windows 10 são descobertas e armazenadas em um dos seguintes atributos:  

    -   **Ramificação de Preparação do Sistema Operacional**: especifica o branch do sistema operacional. Por exemplo, **0** = CB (não adiar upgrades) **1** = CBB (adiar atualizações), **2** = LTSB (Branch de Manutenção em Longo Prazo)

    -   **Compilação do Sistema Operacional**: especifica o build do sistema operacional. Por exemplo, **10.0.10240** (RTM) ou **10.0.10586** (versão 1511)  

-   O ponto de conexão de serviço deve ser instalado e configurado no modo **Online, conexão persistente** para que seja possível ver os dados no painel de serviço do Windows 10. Quando estiver no modo offline, você não verá as atualizações de dados no painel até receber atualizações de serviço do Configuration Manager.   
      Para obter mais informações, consulte [Sobre o ponto de conexão de serviço](../../core/servers/deploy/configure/about-the-service-connection-point.md).  


-   O Internet Explorer 9 ou posterior deve estar instalado no computador que executa o console do Configuration Manager.  

-   As atualizações de software devem ser configuradas e sincronizadas. É necessário selecionar a classificação **Atualizações** e sincronizar as atualizações de software antes as atualizações de recursos do Windows 10 fiquem disponíveis no console do Configuration Manager. Para obter mais informações, consulte [Preparar-se para o gerenciamento de atualização de software](../../sum/get-started/prepare-for-software-updates-management.md).  

##  <a name="BKMK_ServicingDashboard"></a> Painel de serviço do Windows 10  
 O painel de serviço do Windows 10 fornece informações sobre os computadores Windows 10 em seu ambiente, os planos de serviço ativos, as informações de conformidade e assim por diante. Os dados contidos no painel de serviço do Windows 10 dependem da instalação do Ponto de Conexão de Serviço. O painel contém os seguintes blocos:  

-   **Bloco Uso do Windows 10**: fornece uma divisão dos builds públicos do Windows 10. Os builds do Windows Insiders são listados como **outros** , bem como quaisquer builds que ainda não são conhecidos para seu site. O ponto de conexão de serviço baixará os metadados que informam sobre os builds do Windows e, em seguida, esses dados são comparados com os dados de descoberta.  

-   **Bloco Anéis do Windows 10**: fornece uma divisão do Windows 10 por branch e estado de preparação. O segmento LTSB conterá todas as versões de LTSB (enquanto o primeiro bloco divide as versões específicas). Por exemplo, Windows 10 LTSB 2015. O segmento **Pronto para Liberação** corresponde ao CB e o segmento **Pronto para Negócios** refere-se ao CBB.  

-   **Bloco Criar Plano de Serviço**: fornece uma maneira rápida de criar um plano de serviço. Você especifica o nome, a coleção (exibe apenas as dez primeiras coleções por tamanho, em ordem crescente), o pacote de implantação (exibe apenas os dez primeiros pacotes por pacotes modificados mais recentemente) e o estado de preparação. Valores padrão são usados para as outras configurações. Clique em **Configurações Avançadas** para iniciar o assistente de Criação do Plano de Serviço, em que é possível configurar todas as configurações do plano de serviço.  

-   **Bloco Expirado**: exibe o percentual de dispositivos que estão em um build do Windows 10 cuja vida útil já expirou. O Configuration Manager determina o percentual dos metadados baixados pelo Ponto de Conexão de Serviço e o compara com os dados de descoberta. Um build cuja vida útil já expirou não recebe mais atualizações cumulativas mensais, que incluem atualizações de segurança. Os computadores nessa categoria devem ser atualizados para a próxima versão de build. O Configuration Manager arredonda para o próximo número inteiro. Por exemplo, se você tiver 10.000 computadores e apenas um em um build expirado, o bloco exibirá 1%.  

-   **Bloco Expira em breve**: exibe o percentual de computadores que estão em um build cujo fim da vida útil está próximo (em aproximadamente quatro meses), semelhante ao bloco **Expirado** . O Configuration Manager arredonda para o próximo número inteiro.  

-   **Bloco Alertas**: exibe os alertas ativos.  

-   **Bloco Monitoramento do Plano de Serviço**: exibe os planos de serviço criados e um gráfico da conformidade para cada um. Isso fornece uma visão geral rápida do estado atual das implantações de plano de serviço. Se um anel de implantação anterior atender às suas expectativas quanto à conformidade, será possível selecionar um plano de serviço posterior (anel de implantação) e clicar em **Implantar Agora** , em vez de aguardar até que as regras do plano de serviço sejam disparadas automaticamente.  

-   O **bloco Builds do Windows 10**: exibe uma linha do tempo fixa da imagem que fornece uma visão geral das compilações do Windows 10 atualmente liberadas e fornece uma ideia geral de quando as compilações farão a transição para estados diferentes.  

> [!IMPORTANT]  
>  As informações mostradas no painel de serviço do Windows 10 (como o ciclo de vida do suporte para versões do Windows 10) são fornecidas para sua conveniência e somente para uso interno em sua empresa. Você não deve depender exclusivamente dessas informações para confirmar a conformidade da atualização. Certifique-se de verificar a precisão das informações fornecidas a você.  

## <a name="servicing-plan-workflow"></a>Fluxo de trabalho do plano de serviço  
 Os planos de serviço do Windows 10 no Configuration Manager são muito parecidos com as regras de implantação automática das atualizações de software. Você cria um plano de serviço com os seguintes critérios avaliados pelo Configuration Manager:  

-   **Classificação Atualizações**: somente as atualizações que estão na classificação **Atualizações** são avaliadas.  

-   **Estado de preparação**: o estado de preparação definido no plano de serviço é comparado com o estado de preparação da atualização. Os metadados da atualização são recuperados quando o ponto de conexão de serviço verifica se há atualizações.  

-   **Adiamento de tempo**: o número de dias especificados para **Por quantos dias você gostaria de aguardar após a publicação pela Microsoft de uma nova atualização antes de implantá-la em seu ambiente** no plano de serviço. O Configuration Manager avalia se é necessário incluir uma atualização na implantação, caso a data atual seja posterior à data de lançamento, além do número configurado de dias.  

 Quando uma atualização atende aos critérios, o plano de serviço adiciona a atualização ao pacote de implantação, distribui o pacote para os pontos de distribuição e implanta a atualização na coleção com base nas configurações definidas no plano de serviço.  É possível monitorar as implantações no bloco Monitoramento do Plano de Serviço no Painel de Serviço do Windows 10. Para obter mais informações, consulte [Implantar atualizações de software](../../sum/deploy-use/monitor-software-updates.md).  

##  <a name="BKMK_ServicingPlan"></a> Plano de serviço do Windows 10  
 Durante a implantação do Windows 10 CB, é possível criar um ou mais planos de serviço para definir os anéis de implantação que você deseja ter em seu ambiente e, em seguida, monitorá-los no painel de serviço do Windows 10.   
Os planos de manutenção usam apenas a classificação de atualizações de software **Atualizações** , e não as atualizações cumulativas para o Windows 10. Para essas atualizações, você ainda precisará implantar com o fluxo de trabalho das atualizações de software.  A experiência do usuário final com um plano de serviço é a mesma quando comparado às atualizações de software, incluindo as configurações definidas no plano de serviço.  

> [!NOTE]  
>  É possível usar uma sequência de tarefas para implantar uma atualização para cada build do Windows 10, mas isso exige mais trabalho manual. Você precisaria importar os arquivos de origem atualizados como um pacote de atualização do sistema operacional e depois criar e implantar a sequência de tarefas no conjunto apropriado de computadores. No entanto, uma sequência de tarefas fornece opções personalizadas adicionais, como ações pré e pós-implantação.  

 É possível criar um plano de serviço básico no painel de serviço do Windows 10. Depois de especificar o nome, a coleção (exibe apenas as dez primeiras coleções por tamanho, em ordem crescente), o pacote de implantação (exibe apenas os dez primeiros pacotes começando pelos pacotes modificados mais recentemente) e o estado de preparação, o Configuration Manager cria o plano de serviço com valores padrão para as outras configurações. Também é possível iniciar o assistente de Criação do Plano de Serviço para definir todas as configurações. Use o procedimento a seguir para criar um plano de serviço usando o assistente de Criação do Plano de Serviço.  

> [!NOTE]  
>  A partir da versão 1602 do Configuration Manager, você pode gerenciar o comportamento das implantações de alto risco. Uma implantação de alto risco é uma implantação que é instalada automaticamente e que tem o potencial de causar resultados indesejados. Por exemplo, uma sequência de tarefas que tenha uma finalidade **Obrigatória** que implanta o Windows 10 é considerada uma implantação de alto risco. Para obter mais informações, consulte [Configurações para gerenciar implantações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

#### <a name="to-create-a-windows-10-servicing-plan"></a>Para criar um plano de serviço do Windows 10  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho Biblioteca de Software, expanda **Serviço do Windows 10**e clique em **Planos de Serviço**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Plano de Serviço**. O assistente de Criação do Plano de Serviço é aberto.  

4.  Na página **Geral** , defina as seguintes configurações:  

    -   **Nome**: especifique o nome para o plano de serviço. O nome deve ser exclusivo, deve ajudar a descrever a finalidade da regra e diferenciá-la de outras no site do Configuration Manager.  

    -   **Descrição:**especifique uma descrição para o plano de serviço. A descrição deve fornecer uma visão geral do plano de serviço e qualquer outra informação relevante que ajude a identificá-lo e diferenciá-lo de outros planos no site do Configuration Manager. O campo de descrição é opcional, tem um limite de 256 caracteres e um valor em branco por padrão.  

5.  Na página Plano de Serviço, defina as seguintes configurações:  

    -   **Coleção de Destino**: especifica a coleção de destino a ser usada para o plano de serviço. Os membros da coleção recebem as atualizações do Windows 10 definidas no plano de serviço.  

        > [!NOTE]  
        >  A partir da versão 1602 do Configuration Manager, quando você fizer uma implantação de alto risco, como um plano de manutenção, a janela **Selecionar Coleção** exibirá apenas as coleções personalizadas que atendem às configurações de verificação da implantação que são definidas nas propriedades do site.
        >    
        > As implantações de alto risco sempre estão limitadas às coleções personalizadas criadas e à coleção interna de **Computadores desconhecidos** . Ao criar uma implantação de alto risco, não é possível selecionar uma coleção interna como **Todos os Sistemas**. Desmarque **Ocultar coleções com uma contagem de membros maior que a configuração de tamanho mínimo do site** para ver todas as coleções personalizadas que contêm menos clientes do que o tamanho máximo configurado. Para obter mais informações, consulte [Configurações para gerenciar implantações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md).  
        >  
        > As configurações de verificação de implantação baseiam-se na associação atual da coleção. Depois de implantar o plano de manutenção, a associação à coleção não será reavaliada quanto às configurações de implantação de alto risco.  
        >  
        > Por exemplo, suponhamos que você defina **Tamanho padrão** como 100 e o **Tamanho máximo** como 1000. Ao criar uma implantação de alto risco, a janela **Selecionar coleção** exibirá somente as coleções que contêm menos de 100 clientes. Se você desmarcar a definição **Ocultar coleções com uma contagem de membro maior que a configuração de tamanho mínimo do site**, a janela exibirá coleções que contêm menos de 1000 clientes.  
        >
        > Ao selecionar uma coleção que contém uma função de site, o seguinte se aplica:    
        >   
        >    - Se a coleção contiver um servidor do sistema de sites e nas configurações de verificação de implantação você configurar para coleções de bloco com servidores do sistema de sites, ocorrerá um erro e não será possível continuar.    
        >    - Se a coleção contiver um servidor do sistema de sites e nas configurações de verificação de implantação for configurada a opção para avisar se as coleções que têm servidores do sistema de sites, se a coleção exceder o valor do tamanho padrão ou se a coleção contiver um servidor, o Assistente de Implantação de Software exibirá um aviso de alto risco. Você deve concordar em criar uma implantação de alto risco e uma mensagem de status de auditoria é criada.  

6.  Na página Anel de Implantação, defina as seguintes configurações:  

    -   **Especificar o estado de preparação do Windows ao qual este plano de serviço deve ser aplicado**: selecione um dos seguintes:  

        -   **Pronto para Liberação (Branch Atual)**: no modelo de serviço CB, as atualizações de recursos estão disponíveis assim que são lançadas pela Microsoft.

        -   **Pronto para Negócios (Branch Atual para Negócios)**: o branch de manutenção CBB normalmente é usado para a implantação ampla. Os clientes do Windows 10 no branch de manutenção do CBB recebem a mesma compilação do Windows 10 que aqueles no branch de manutenção do CB, mas em um momento posterior.

        Para saber mais sobre manutenção de ramificações e quais opções são melhores para você, veja [Manutenção de ramificações](https://technet.microsoft.com/itpro/windows/manage/waas-overview#servicing-branches).

    -   **Por quantos dias você gostaria de aguardar após a publicação pela Microsoft de uma nova atualização antes de implantá-la em seu ambiente**: o Configuration Manager avalia se inclui uma atualização na implantação, caso a data atual seja posterior à data de lançamento, somada ao número de dias que você definir para essa configuração.

    -   Em uma versão anterior à 1602 do Configuration Manager, clique em **Visualizar** para exibir as atualizações do Windows 10 associadas ao estado de preparação.  

    Para obter mais informações, consulte [Branches de manutenção](https://technet.microsoft.com/itpro/windows/manage/waas-overview#servicing-branches).
7.  A partir da versão 1602 do Configuration Manager, na página Atualizações, configure os critérios de pesquisa para filtrar as atualizações que serão adicionadas ao plano de serviço. Somente as atualizações que atendem aos critérios especificados serão adicionadas à implantação associada.  

     Clique em **Visualizar** para exibir as atualizações que atendem aos critérios especificados.  

8.  Na página Agendamento da Implantação, defina as seguintes configurações:  

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
            >  O prazo real da instalação é o prazo exibido, mais um período de tempo aleatório de até 2 horas. Isso reduz o impacto potencial de todos os computadores cliente na coleção de destino que está instalando as atualizações na implantação ao mesmo tempo.  
            >   
            >  É possível definir a configuração do cliente **Agente de Computador** , **Desativar data limite aleatória** , para desabilitar o atraso de aleatoriedade da instalação das atualizações necessárias. Para obter mais informações, consulte [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

9. Na página Experiência do Usuário, defina as seguintes configurações:  

    -   **Notificações de usuário**: especifique se deseja exibir a notificação das atualizações no Centro de Software no computador cliente no **Tempo disponível do software** configurado e se deseja exibir as notificações de usuário nos computadores cliente.  

    -   **Comportamento da data limite**: especifique o comportamento que deve ocorrer na data limite da implantação de atualização. Especifique se deseja instalar as atualizações na implantação. Especifique também se o sistema deve ser reiniciado após a instalação da atualização, independentemente de uma janela de manutenção configurada. Para obter mais informações sobre janelas de manutenção, consulte [Como usar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamento de reinicialização do dispositivo**: especifique se uma reinicialização do sistema em servidores e estações de trabalho deve ser suprimida depois que as atualizações são instaladas e se uma reinicialização do sistema é necessária para concluir a instalação.  

    -   **Manuseio de filtro de gravação para dispositivos Windows Embedded**: ao implantar atualizações em dispositivos Windows Embedded com filtro de gravação habilitado, é possível especificar que a atualização seja instalada na sobreposição temporária e que as alterações sejam confirmadas mais tarde, na data limite da instalação ou durante uma janela de manutenção. Ao confirmar as alterações na data limite da instalação ou durante uma janela de manutenção, é necessário reinicializar. Dessa forma, as alterações permanecem no dispositivo.  

        > [!NOTE]  
        >  Ao implantar uma atualização em um dispositivo Windows Embedded, verifique se o dispositivo é membro de uma coleção com uma janela de manutenção configurada.  

10. Na página do Pacote de Implantação, selecione um pacote de implantação existente ou configure as seguintes definições para criar um novo pacote de implantação:  

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

11. Na página Pontos de Distribuição, especifique os pontos de distribuição ou grupos de pontos de distribuição que hospedarão os arquivos de atualização. Para obter mais informações sobre pontos de distribuição, consulte [Configurar um ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_configs).

    > [!NOTE]  
    >  A página está disponível somente quando você cria um novo pacote de implantação de atualização de software.  

12. Na página Local de Download, especifique se deseja baixar os arquivos de atualização da Internet ou de sua rede local. Defina as seguintes configurações:  

    -   **Baixar atualizações de software da Internet**: selecione essa configuração para baixar as atualizações de um local específico na Internet. Essa configuração é habilitada por padrão.  

    -   **Baixar atualizações de software de um local na rede local**: selecione essa configuração para baixar as atualizações de um diretório local ou de uma pasta compartilhada. Essa configuração é útil quando o computador que executa o assistente não tem acesso à Internet. Qualquer computador com acesso à Internet pode baixar preliminarmente as atualizações e armazená-las em um local na rede local que é acessível pelo computador que executa o assistente.  

13. Na página Seleção de Idioma, selecione os idiomas nos quais as atualizações selecionadas serão baixadas. As atualizações só serão baixadas se estiverem disponíveis nos idiomas selecionados. Atualizações não específicas do idioma são sempre baixadas. Por padrão, o assistente seleciona os idiomas que você configurou nas propriedades de ponto de atualização de software. Pelo menos um idioma deve ser selecionado para ir para a próxima página. Ao selecionar apenas os idiomas sem suporte de uma atualização, o download da atualização falhará.  

14. Na página Resumo, examine as configurações e clique em **Avançar** para criar o plano de serviço.  

 Depois de concluir o assistente, o plano de serviço será executado. Isso adicionará as atualizações que atendem aos critérios especificados a um grupo de atualização de software, baixará as atualizações na biblioteca de conteúdo no servidor do site, distribuirá as atualizações aos pontos de distribuição configurados e implantará o grupo de atualizações de software nos clientes da coleção de destino.  

##  <a name="BKMK_ModifyServicingPlan"></a> Modificar um plano de serviço  
Depois de criar um plano de serviço básico no painel de serviço do Windows 10 ou precisar alterar as configurações de um plano de serviço existente, é possível ir para as propriedades do plano de serviço.

> [!NOTE]
> Você pode definir configurações nas propriedades do plano de manutenção que não estão disponíveis no assistente ao criar o plano de manutenção. O assistente usa as configurações padrão para as configurações do seguintes itens: baixar as configurações, configurações de implantação e alertas.  

Use o procedimento a seguir para modificar as propriedades de um plano de serviço.  

#### <a name="to-modify-the-properties-of-a-servicing-plan"></a>Para modificar as propriedades de um plano de serviço  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho Biblioteca de Software, expanda **Serviço do Windows 10**, clique em **Planos de Serviço**e selecione o plano de serviço que deseja modificar.  

3.  Na guia **Início** , clique em **Propriedades** para abrir as propriedades do plano de serviço selecionado.

    As seguintes configurações estão disponíveis nas propriedades de plano de manutenção, que não foram configuradas no assistente:

    **Configurações de Implantação**: na guia Configurações de Implantação, defina as seguintes configurações:  

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

    **Configurações de Download**: na guia Configurações de Download, defina as seguintes configurações:  

    - Especifique se o cliente irá baixar e instalar as atualizações de software quando estiver conectado a uma rede lenta ou usando um local de conteúdos de fallback.  

    - Especifique se o cliente deve baixar e instalar as atualizações de software por meio de um ponto de distribuição de fallback quando o conteúdo das atualizações de software não está disponível ou de um ponto de distribuição preferencial.  

    -   **Permitir que os clientes compartilhem conteúdo com outros clientes na mesma sub-rede**: especifique se deseja habilitar o uso do BranchCache para downloads de conteúdo. Para obter mais informações sobre o BranchCache, consulte [Fundamental concepts for content management (Conceitos fundamentais para o gerenciamento de conteúdo)](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    -   Especifique se os clientes deverão baixar as atualizações de software do Microsoft Update se elas não estiverem disponíveis nos pontos de distribuição.
        > [!IMPORTANT]
        > Não use essa configuração para atualizações de serviço do Windows 10. O Configuration Manager (pelo menos até a versão 1610) não baixará as atualizações de serviço do Windows 10 do Microsoft Update.

    -   Especifique se os clientes têm permissão para baixar após o prazo de uma instalação quando usam conexão de Internet limitada. Provedores de Internet ocasionalmente cobram por quantidade de dados que você envia e recebe quando está em uma conexão de Internet limitada.   

    **Alertas**: na guia Alertas, configure como o Configuration Manager e o System Center Operations Manager gerarão alertas para essa implantação. Você só pode configurar alertas quando o **Tipo de implantação** está definido como **Obrigatório** na página Configurações de Implantação.  

    > [!NOTE]  
    >  Você pode verificar os alertas de atualizações de software recentes no nó **Atualizações de Software** no espaço de trabalho **Biblioteca de Software** .  

**Para obter mais informações:** <br/>
[Conceitos básicos do Configuration Manager como um serviço e do Windows como um serviço](/sccm/core/understand/configuration-manager-and-windows-as-service.md)