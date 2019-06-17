---
title: Como implantar o piloto
titleSuffix: Configuration Manager
description: Um guia de instruções para a implantação em um grupo piloto de análise de área de trabalho.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: e18e2e43e9bb768f81233fb2d2deda0ae05c1961
ms.sourcegitcommit: d47d2f03482e48d343e2139a341e61022331e6c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67145829"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>Como implantar o piloto, com a análise de área de trabalho

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Um dos benefícios da análise de área de trabalho é ajudar a identificar o menor conjunto de dispositivos que fornecem a cobertura mais ampla de fatores. Ele aborda os fatores que são mais importantes para um piloto de atualizações e upgrades do Windows. Verificando se que o piloto é mais bem-sucedida permite mover com mais rapidez e confiança a ampla implantações em produção.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]


## <a name="identify-devices"></a>Identificar os dispositivos

A primeira etapa é identificar os dispositivos para incluir no projeto-piloto. Dispositivos de acordo com os dados relatados recomenda a análise da área de trabalho, e você pode incluir ou substituir os dispositivos nessa lista.

1. Vá para o [portal de análise de área de trabalho](https://aka.ms/desktopanalytics)e no, selecione Gerenciar grupo **planos de implantação**.

1. Selecione um plano de implantação.

1. No grupo de preparação do menu de plano de implantação, selecione **Identify piloto**.

Você verá os dados de análise de área de trabalho que mostra o número de dispositivos que ele recomenda, incluindo a cobertura melhor. Esse algoritmo baseia-se principalmente sobre o uso de aplicativos críticos e importantes e a variedade de configurações de hardware.

Execute as seguintes ações para obter a lista de dispositivos recomendados adicionais:

- **Adicionar tudo para o piloto**: Adiciona todos os dispositivos recomendados no grupo piloto
- **Adicionar ao projeto-piloto**: Apenas adicionar dispositivos individuais
- **Substitua** quaisquer dispositivos específicos do projeto-piloto
- **Recalcular** quando terminar de fazer as alterações

Você também pode tomar decisões de todo o sistema sobre quais coleções do Configuration Manager para incluir ou excluir de pilotos. No menu principal da área de trabalho de análise, no grupo de configurações globais, selecione **piloto Global**.

### <a name="example"></a>Exemplo

- Configurar a conexão de área de trabalho de análise no Configuration Manager para o destino o **todos os sistemas** coleção. Esta ação registra todos os clientes para o serviço.
- Você também pode configurar coleções adicionais para sincronizar com a área de trabalho de análise:
    - Todos os clientes do Windows 10
    - Todos os dispositivos de TI
    - Office CEO
- No **Global piloto** as configurações, você incluir a **dispositivos de TI de todos os** coleções. Excluir o **CEO office** coleção.
- Criar um plano de implantação e selecione o **todos os Windows 10 clientes** coleção.
- Sua **piloto dispositivos incluídos** lista contém os seguintes conjuntos de dispositivo:
    - Todos os dispositivos na sua lista de inclusão de piloto global: **Todos os dispositivos de TI**
    - Coleções que também fazem parte do grupo de destino do plano de implantação: **Todos os clientes do Windows 10**
- Análise da área de trabalho exclui o **recomendável adicionais dispositivos** lista todos os dispositivos em seu projeto-piloto global *exclusão* lista: **Office CEO**
- Somente as primeiras duas coleções são consideradas como parte do piloto. Depois que as atualizações com êxito a esses grupos e os ativos são *pronto*, análise de área de trabalho sincroniza os dispositivos na **CEO office** coleção à coleção de produção do Configuration Manager.


## <a name="address-issues"></a>Solucionar problemas

Use o portal de análise de área de trabalho para examinar os problemas relatados com ativos que podem bloquear a sua implantação. Em seguida, aprovar, rejeitar ou modificar a correção sugerida. Todos os itens devem ser marcados **pronto** ou **pronto (com correção)** antes de inicia a implantação piloto.

1. Vá para o [portal de análise de área de trabalho](https://aka.ms/desktopanalytics)e no, selecione Gerenciar grupo **planos de implantação**.  

2. Selecione um plano de implantação.  

3. No grupo de preparação do menu de plano de implantação, selecione **piloto preparar**.  

4. Sobre o **aplicativos** guia, examine os aplicativos que precisam de sua entrada.  

5. Para cada aplicativo, selecione o nome do aplicativo. No painel de informações, examine a recomendação e selecione o decisão de atualização. Se você escolher **não revisado** ou **não é possível**, em seguida, análise de área de trabalho não inclui os dispositivos com esse aplicativo na implantação piloto. Se você escolher **pronto (com correção)** , use o **anotações de correção** para capturar as ações necessárias para resolver um problema, como *reinstalar* ou *encontrar o versão recomendada do fabricante*.

6. Repita esta revisão de outros ativos.  


## <a name="create-software"></a>Criar software

Antes de implantar o Windows, primeiro crie os objetos de software no Configuration Manager. Para obter mais informações, consulte [sequência de tarefas de atualização in-loco do Windows 10](https://docs.microsoft.com/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).


## <a name="deploy-to-pilot-devices"></a>Implantar em dispositivos piloto

Configuration Manager usa os dados da área de trabalho de análise para criar coleções para as implantações piloto e de produção. Para garantir que os dispositivos estão íntegros após cada fase de implantação, use o procedimento a seguir para criar uma implantação em fases integrada de análise de área de trabalho:

1. No console do Configuration Manager, vá para o **biblioteca de Software**, expanda **área de trabalho de análise de manutenção**e selecione o **planos de implantação** nó.  

2. Selecione seu plano de implantação e, em seguida, selecione **detalhes do plano de implantação** na faixa de opções.  

3. Selecione **criar implantação em fases** na faixa de opções. Essa ação inicia o Assistente para criar implantação em fases.

    > [!Tip]  
    > Se você quiser criar uma implantação de sequência de tarefas de clássico para coleção piloto, selecione **Deploy** na **criar um piloto do status** lado a lado. Essa ação inicia o Assistente de implantação de Software. Para obter mais informações, consulte [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence).  

4. Insira um nome para a implantação e selecione a sequência de tarefas para usar. Usar a opção para **criar automaticamente uma implantação de duas fases padrão**e, em seguida, configure as seguintes coleções:  

    - **Primeira coleção**: Localize e selecione o **piloto** coleção para este plano de implantação. A convenção de nomenclatura padrão para esta coleção é `<deployment plan name> (Pilot)`.

    - **Segunda coleção**: Localize e selecione o **produção** coleção para este plano de implantação. A convenção de nomenclatura padrão para esta coleção é `<deployment plan name> (Production)`.

    > [!Note]  
    > Com a integração de análise de área de trabalho, o Configuration Manager cria automaticamente as coleções de piloto e de produção para o plano de implantação. Ele pode levar até 10 minutos para essas coleções sincronizar antes de você pode usá-los.<!-- 3887891 -->
    >
    > Essas coleções são reservadas para dispositivos de plano de implantação de área de trabalho de análise. Não há suporte para alterações manuais a essas coleções.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Conclua o Assistente para configurar a implantação em fases. Saiba mais em [Criar implantações em fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).

    > [!Note]  
    > Use a configuração padrão para **iniciar automaticamente esta fase após um período de adiamento (em dias)** . Os critérios a seguir devem ser atendidos para a segunda fase iniciar:
    >
    > 1. Necessidade de atualizar e enviar dados de diagnóstico foi revisado back dispositivos piloto.
    > 1. A primeira fase atinge o **percentual de êxito de implantação** critérios para o sucesso. Você pode definir essa configuração na implantação em fases.
    > 1. Você precisa examinar e tomar decisões de atualização na área de trabalho de análise para marcar ativos críticos e importantes, como *pronto*. Para obter mais informações, consulte [examine ativos que precisam de uma decisão de atualização](/sccm/desktop-analytics/deploy-prod#bkmk_review).
    > 1. Análise da área de trabalho sincroniza para coleções do Configuration Manager os dispositivos de produção que atendem a *pronto* critérios.
    >
    > Quando o Configuration Manager em fases implantação move automaticamente para a próxima fase, ele só se aplica a dispositivos que sincroniza de análise de área de trabalho para a coleção de produção.

> [!Important]  
> Essas coleções continuam a sincronização como suas alterações de associação. Por exemplo, se você identifica um problema com um ativo e marque-a como **não é possível**, dispositivos com esse ativo não atendem mais a *pronto* critérios. Esses dispositivos são removidos da coleção de implantação de produção.


## <a name="monitor"></a>Monitor

### <a name="configuration-manager-console"></a>Console do Configuration Manager

Abra o plano de implantação. O **Preparando atualização decisões - status geral** lado a lado fornece um resumo do status para o plano de implantação. Esse status é para coleções de seu piloto e de produção. Dispositivos podem se enquadrar em uma das seguintes categorias:

- **Atualizado**: Dispositivos atualizou para a versão do Windows de destino para este plano de implantação

- **Conclusão da decisão de atualização**: Um dos seguintes estados:
    - Dispositivos com digno de nota ativos que são **pronto** ou **pronto com correção**
    - É o estado do dispositivo **Blocked**, **dispositivo Replace** ou **reinstalar dispositivos**

- **Não revisado**: Dispositivos com ativos digno de nota **não revisado** ou **revisão em andamento**

Atualizações de status do dispositivo na **criar um piloto do status** e **status de produção** lado a lado com as seguintes ações:

- Fazer alterações na avaliação de compatibilidade
- Dispositivos atualizados para a versão de destino do Windows
- O andamento da implantação

Você também pode usar o mesmo que qualquer outra implantação de sequência de tarefas de monitoramento da implantação do Configuration Manager. Para obter mais informações, consulte [implantações de sistema operacional do Monitor](/sccm/osd/deploy-use/monitor-operating-system-deployments).


### <a name="desktop-analytics-portal"></a>Portal de análise da área de trabalho

Use o [portal de análise de área de trabalho](https://aka.ms/desktopanalytics) para exibir o status de qualquer plano de implantação. Selecione o plano de implantação e, em seguida, selecione **visão geral do plano**.

![Captura de tela de visão geral do plano de implantação na área de trabalho de análise](media/deployment-plan-overview.png)

Selecione o **piloto** lado a lado. Ela resume o estado atual da implantação piloto. Esse bloco também exibe dados para o número de dispositivos que não foi iniciados, em andamento, concluído, ou retornando problemas.

Todos os dispositivos relatar erros ou outros problemas também são listados na área de detalhes do projeto-piloto para a direita. Para obter detalhes do problema relatado, selecione **revisão**. Esta ação altera o modo de exibição para o **status de implantação** página

O **status de implantação** página lista os dispositivos nas seguintes categorias:

- Não iniciada
- Em andamento
- Concluído
- Precisa de atenção – dispositivos
- Precisa de atenção – problemas

O **precisa de atenção** categorias mostram as mesmas informações, mas classificados de forma diferente.

Selecione uma lista específica em qualquer modo de exibição para obter mais detalhes sobre o problema detectado.

Conforme você resolver esses problemas de implantação, o painel continua mostrar o progresso de dispositivos. Ele atualiza o que se movem de dispositivos **precisa de atenção** à **concluído**.


## <a name="next-steps"></a>Próximas etapas

Permitir que a execução do piloto por algum tempo coletar dados operacionais. Incentive os usuários de dispositivos piloto para testar aplicativos.

Quando sua implantação piloto atende aos seus critérios de êxito, vá para o próximo artigo para implantar na produção.
> [!div class="nextstepaction"]  
> [Implantar na produção](/sccm/desktop-analytics/deploy-prod)  
