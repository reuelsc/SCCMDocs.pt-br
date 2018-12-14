---
title: Criar implantações em fases
titleSuffix: Configuration Manager
description: Use implantações em fases para automatizar a distribuição de software para várias coleções.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d103f7f7b92003605d92d34d6294ed06009118c
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456508"
---
# <a name="create-phased-deployments-with-configuration-manager"></a>Criar implantações em fases com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As implantações em fases automatizam uma distribuição coordenada e sequenciada do software em várias coleções. Por exemplo, implante o software em uma coleção piloto e, em seguida, continue a distribuição automaticamente com base em critérios de sucesso. Crie implantações em fases com o padrão de duas fases ou configure várias fases manualmente. 

Crie implantações em fases para os seguintes objetos:
- **Sequência de tarefas**  
    - A implantação em fases de sequências de tarefas não dá suporte para PXE ou mídia de instalação   
- **Aplicativo** (começando na versão 1806) <!--1358147-->  
- **Atualização de software** (começando na versão 1810) <!--1358146-->  
    - Você não pode usar uma regra de implantação automática com uma implantação em fases

> [!Tip]  
> O recurso de implantação em fases foi introduzido na versão 1802 como um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features). Começando com a versão 1806, ele não é mais um recurso de pré-lançamento.<!--1356837-->  



## <a name="prerequisites"></a>Pré-requisitos

#### <a name="security-scope"></a>Escopo de segurança
As implantações criadas por implantações em fases não ficam visíveis para usuários administrativos que não têm o escopo de segurança **Todos**. Para obter mais informações, consulte [Escopos de segurança](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_PlanScope).

#### <a name="distribute-content"></a>Distribuir conteúdo
Antes de criar uma implantação em fases, distribua o conteúdo associado a um ponto de distribuição.<!--518293-->  

- **Aplicativo**: selecione o aplicativo de destino no console e use a ação **Distribuir Conteúdo** na faixa de opções. Para obter mais informações, confira [Implantar e gerenciar o conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content).   

- **Sequência de tarefas**: você precisa criar referenciado pacote de atualização de objetos, como o sistema operacional antes de criar a sequência de tarefas. Distribua esses objetos antes de criar uma implantação. Use a ação **Distribuir Conteúdo** em cada objeto ou a sequência de tarefas. Para exibir o status de todo o conteúdo referenciado, selecione a sequência de tarefas e mude para a guia **Referências** no painel de detalhes. Para obter mais informações, confira o tipo de objeto específico em [Preparar para implantação de sistema operacional](/sccm/osd/get-started/prepare-for-operating-system-deployment).   

- **Atualização de software**: crie o pacote de implantação e distribua-o. Use o Assistente para Baixar Atualizações de Software. Para obter mais informações, confira [Baixar atualizações de software](/sccm/sum/deploy-use/download-software-updates).  



## <a name="bkmk_settings"></a> Configurações de fase

Essas configurações são exclusivas das implantações em fases. Defina essas configurações ao criar ou editar as fases para controlar o agendamento e o comportamento do processo de implantação em fases. 


#### <a name="criteria-for-success-of-the-first-phase"></a>Critérios para o sucesso da primeira fase  

- **Percentual de sucesso da implantação**: especifique a percentagem de dispositivos que precisam concluir com sucesso a implantação para que a primeira fase tenha êxito. Por padrão, esse valor é 95%. Em outras palavras, o site considera a primeira fase como bem-sucedida quando o estado de conformidade de 95% dos dispositivos é **Sucesso** para essa implantação. O site, em seguida, continua a segunda fase e cria uma implantação do software para a próxima coleção.  


#### <a name="conditions-for-beginning-second-phase-of-deployment-after-success-of-the-first-phase"></a>Condições para iniciar a segunda fase da implantação após o sucesso da primeira fase  

- **Iniciar automaticamente esta fase após um período de adiamento (em dias)**: escolha o número de dias para esperar antes de iniciar a segunda fase após o sucesso da primeira. Por padrão, esse valor é um dia.  

- **Iniciar manualmente a segunda fase da implantação**: o site não inicia a segunda fase automaticamente depois que a primeira fase é bem-sucedida. Essa opção exige que você inicie a segunda fase manualmente. Para obter mais informações, confira [Passar para a próxima fase](/sccm/osd/deploy-use/manage-monitor-phased-deployments#bkmk_move).  

    > [!Note]  
    > Essa opção não está disponível para implantações de aplicativos em fases.  


#### <a name="gradually-make-this-software-available-over-this-period-of-time-in-days"></a>Disponibilizar esse software gradualmente durante esse período de tempo (em dias)
<!--1358578--> Começando na versão 1806, é possível definir essa configuração para que a distribuição em cada fase ocorra gradualmente. Esse comportamento ajuda a reduzir o risco de problemas de implantação e diminui a carga na rede que é causada pela distribuição de conteúdo aos clientes. O site disponibiliza o software gradualmente, dependendo da configuração de cada fase. Todos os clientes em uma fase têm um prazo em relação à hora em que o software é disponibilizado. A janela entre o horário disponível e o prazo final é a mesma para todos os clientes em uma fase. O valor padrão dessa configuração é zero, portanto, por padrão, a implantação não é limitada. Não defina o valor para mais de 30.<!--SCCMDocs-pr issue 2767--> 


#### <a name="configure-the-deadline-behavior-relative-to-when-the-software-is-made-available"></a>Configurar o comportamento da data limite em relação a quando o software é disponibilizado  

- **A instalação é obrigatória O mais breve possível**: defina a data limite para a instalação no dispositivo assim que ocorrer o direcionamento ao dispositivo.  

- **A instalação é obrigatória após esse período de tempo**: defina uma data limite para a instalação um determinado número de dias depois que ocorrer o direcionamento ao dispositivo. Por padrão, esse valor é sete dias.   


<!--### Examples
Include a timeline diagram
-->



## <a name="bkmk_auto"></a> Criar automaticamente uma implantação em duas fases padrão

1. Inicie o Assistente para Criar Implantação em Fases no console do Configuration Manager. Essa ação varia de acordo com o tipo de software que você está implantando:  

    - **Aplicativo** (somente na versão 1806 ou posteriores): acesse a **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e selecione **Aplicativos**. Selecione um aplicativo existente e escolha **Criar Implantação em Fases** na faixa de opções.  

    - **Atualização de software** (somente na versão 1810 ou posterior): vá para a **Biblioteca de Software**, expanda **Atualizações de Software** e selecione **Todas as Atualizações de Software**. Selecione uma ou mais atualizações e, em seguida, escolha **Criar Implantação em Fases** na faixa de opções.  

        Essa ação está disponível para atualizações de software dos seguintes nós:  
        - Atualizações de software  
            - **Todas as Atualizações de Software**  
            - **Grupos de Atualizações de Software**   
        - Serviço do Windows 10, **Todas as Atualizações do Windows 10**  
        - Gerenciamento de Cliente do Office 365, **Atualizações do Office 365**  

    - **Sequência de tarefas**: acesse o workspace **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Sequência de Tarefas**. Selecione uma sequência de tarefas existente e escolha **Criar Implantação em Fases** na faixa de opções.  

2. Na página **Geral**, forneça à implantação em fases um **Nome** e uma **Descrição** (opcional) e, em seguida, selecione **Criar automaticamente uma implantação em duas fases padrão**.  

3. Selecione **Procurar** e escolha uma coleção de destino para os campos **Primeira Coleção** e **Segunda Coleção**. Para uma sequência de tarefas e atualizações de software, selecione entre coleções de dispositivos. Para um aplicativo, selecione das coleções de usuário ou de dispositivo. Selecione **Avançar**.  

    > [!Important]  
    > O Assistente para Criar Implantação em Fases não notifica quando uma implantação é possivelmente de alto risco. Para obter mais informações, confira [Settings to manage high-risk deployments](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments) (Configurações para gerenciar implantações de alto risco) e a observação quando você [Implanta uma sequência de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).  

4. Na página **Configurações**, escolha uma opção para cada uma das configurações de agendamento. Para obter mais informações, confira [Configurações de fase](#bkmk_settings). Clique em **Avançar** ao concluir.  

5. Na página **Fases**, veja as duas fases que o assistente cria para as coleções especificadas. Selecione **Avançar**.   

    > [!Note]  
    > Esta seção aborda o procedimento para criar automaticamente uma implantação em duas fases padrão. O assistente permite adicionar, remover, reordenar, editar ou exibir as fases de uma implantação em fases. Para obter mais informações sobre essas ações adicionais, confira [Criar uma implantação em fases com fases configuradas manualmente](#bkmk_manual).  

6. Confirme as seleções na guia **Resumo** e, em seguida, selecione **Avançar** e conclua o assistente.  



## <a name="bkmk_manual"></a> Criar uma implantação em fases com fases configuradas manualmente
<!--1358148--> 

Começando na versão 1806, é possível criar uma implantação em fases com fases configuradas manualmente para uma sequência de tarefas. Adicione até 10 fases extras usando a guia **Fases** do assistente para Criar Implantação em Fases. 

> [!Note]  
> No momento, não é possível criar fases manualmente para um aplicativo. O assistente cria automaticamente duas fases para implantações de aplicativos.


1. Inicie o assistente Criar Implantação em Fases para uma sequência de tarefas ou atualizações de software.  

2. Na página **Geral** do assistente para Criar Implantação em Fases forneça um **Nome** e uma **Descrição** (opcional) à implantação em fases e selecione **Configurar todas as fases manualmente**.  

3. Na página **Fases** do assistente para Criar Implantação em Fases, as seguintes ações estão disponíveis:  

    - **Filtrar** a lista de fases de implantação. Insira uma cadeia de caracteres para uma correspondência que não diferencia maiúsculas de minúsculas das colunas Ordem, Nome ou Coleção. 

    - **Adicionar** uma nova fase:  

        1. Na página **Geral** do Assistente para Adicionar Fase, especifique um **Nome** para a fase e, em seguida, navegue até a **Coleção de Fases** de destino. As configurações adicionais nesta página são iguais às da implantação normal de uma sequência de tarefas ou atualizações de software.  

        2. Na página **Configurações de Fase** do Assistente para Adicionar Fase, defina as configurações de agendamento e selecione **Avançar** ao concluir. Para obter mais informações, confira [Configurações](#bkmk_settings).   

            > [!Note]  
            > Você não pode editar a configuração da fase **Percentual de sucesso da implantação** na primeira fase. Essa configuração aplica-se somente às fases que têm uma fase anterior.  

        3. As configurações nas páginas **Experiência do Usuário** e **Pontos de Distribuição** do Assistente para Adicionar Fase são as mesmos que às da implantação normal de uma sequência de tarefas ou atualizações de software.  

        4. Examine as configurações na página **Resumo** e, em seguida, conclua o Assistente para Adicionar Fase.  

    - **Editar**: essa ação abre a janela Propriedades da fase seleciona, que tem as mesmas guias que as páginas do Assistente para Adicionar Fase.  

    - **Remover**: essa ação exclui a fase selecionada.  

       > [!Warning]  
       > Não há nenhuma confirmação nem nenhuma maneira de desfazer essa ação.  

    - **Mover para cima** ou **Mover para Baixo**: o assistente ordena as fases pela maneira em que elas são adicionadas. A fase adicionada por último fica por último na lista. Para alterar a ordem, selecione uma fase e use um destes botões para mover a localização da fase na lista.  

       > [!Important]  
       > Examine as configurações da fase após a alteração da ordem. Verifique se as configurações a seguir ainda estão consistentes com seus requisitos para essa implantação em fases:  
       > 
       > - Critérios para o sucesso da fase anterior  
       > - Condições para começar esta fase de implantação após êxito da fase anterior   

5. Selecione **Avançar**. Examine as configurações na página **Resumo** e, em seguida, conclua o Assistente para Criar Implantação em Fases.  


Depois de criar uma implantação em fases, abra suas propriedades para fazer alterações:  

- **Adicione** fases adicionais a uma implantação em fases existente.  

- Se uma fase não estiver ativa, você poderá **Editar**, **Remover** ou **Movê-la** para cima ou para baixo. Você não pode movê-la para antes de uma fase ativa.  

- Quando uma fase está ativa, ela é somente leitura. Você não pode editá-la, removê-la ou mover seu local na lista. A única opção é **Exibir** as propriedades da fase.  

- Uma implantação de aplicativo em fases é sempre somente leitura.  



## <a name="next-steps"></a>Próximas etapas

Gerenciar e monitorar implantações em fases:
- [Aplicativo](/sccm/osd/deploy-use/manage-monitor-phased-deployments?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  
- [Atualização de software](/sccm/osd/deploy-use/manage-monitor-phased-deployments?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)  
- [Sequência de tarefas](/sccm/osd/deploy-use/manage-monitor-phased-deployments)  

