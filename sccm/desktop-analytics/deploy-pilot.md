---
title: Como implantar o piloto
titleSuffix: Configuration Manager
description: Um guia de instruções para a implantação em um grupo piloto de análise de área de trabalho.
ms.date: 04/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4aa078f5a8306cb30ea83d45b93b18971be7764f
ms.sourcegitcommit: 5ee9487c891c37916294bd34a10d04e398f111f7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59069374"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>Como implantar o piloto, com a análise de área de trabalho

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Um dos benefícios da análise de área de trabalho é ajudar a identificar o menor conjunto de dispositivos que fornecem a cobertura mais ampla de fatores. Ele aborda os fatores que são mais importantes para um piloto de atualizações e upgrades do Windows e do Office. Verificando se que o piloto é mais bem-sucedida permite mover com mais rapidez e confiança a ampla implantações em produção.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]



## <a name="address-issues"></a>Solucionar problemas

Use o portal de análise de área de trabalho para examinar os problemas relatados com ativos que podem bloquear a sua implantação. Em seguida, aprovar, rejeitar ou modificar a correção sugerida. Todos os itens devem ser marcados **pronto** ou **pronto (com correção)** antes de inicia a implantação piloto.

1. Acesse o portal de análise de área de trabalho e selecione **planos de implantação** no grupo gerenciar.  

2. Abra um plano de implantação, selecionando seu nome.  

3. Selecione **piloto preparar** no grupo de preparação do menu de plano de implantação.  

4. Sobre o **aplicativos** guia, examine os aplicativos que precisam de sua entrada.  

5. Para cada aplicativo, selecione o nome do aplicativo. No painel de informações, examine a recomendação e selecione o decisão de atualização. Se você escolher **não revisado** ou **não é possível**, em seguida, análise de área de trabalho não inclui os dispositivos com esse aplicativo na implantação piloto. Se você escolher **pronto (com correção)**, use o **anotações de correção** para capturar as ações necessárias para resolver um problema, como *reinstalar* ou *encontrar o versão recomendada do fabricante*.

6. Repita esta revisão de outros ativos.  



## <a name="create-software"></a>Criar software

Antes de implantar o Windows ou do Office, primeiro crie os objetos de software no Configuration Manager.

- [Aplicativo de Office 365 ProPlus](https://docs.microsoft.com/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)  

- [Sequência de tarefas de atualização in-loco do Windows 10](https://docs.microsoft.com/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)



## <a name="deploy-to-pilot-devices"></a>Implantar em dispositivos piloto

Configuration Manager usa os dados da área de trabalho de análise para criar uma coleção para a implantação piloto. Não implante a aplicativo ou sequência de tarefas usando uma implantação tradicional. Use o procedimento a seguir para criar uma implantação integrada de análise de área de trabalho:

1. No console do Configuration Manager, vá para o **biblioteca de Software**, expanda **área de trabalho de análise de manutenção**e selecione o **planos de implantação** nó.  

2. Selecione seu plano de implantação e, em seguida, selecione **detalhes do plano de implantação** na faixa de opções.  

3. No **criar um piloto do status** lado a lado, escolha um dos seguintes tipos de objeto na lista suspensa:  

    - **Aplicativo** para o Office 365 ProPlus  

    - **Sequência de tarefas** para Windows 10  
  
   Selecione **implantar**. Essa ação inicia o Assistente para implantar Software para o tipo de objeto selecionado.

    > [!Note]  
    > Com a integração de análise de área de trabalho, o Configuration Manager cria automaticamente uma coleção para o plano de implantação piloto. Ele pode levar até 10 minutos para esta coleção sincronizar antes de você pode usá-lo.<!-- 3887891 -->
    >
    > Essa coleção é reservada para dispositivos de plano de implantação de área de trabalho de análise. Não há suporte para alterações manuais a esta coleção.<!-- 3866460, SCCMDocs-pr 3544 -->  

Para obter mais informações, consulte os seguintes artigos:  

- [Implantar um aplicativo](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy)  

- [Implantar uma sequência de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)  

Se seu plano de implantação é para Windows 10 e Office 365, repita esse processo para criar uma segunda implantação. Por exemplo, se for a primeira implantação da sequência de tarefas, crie uma segunda implantação para o aplicativo.



## <a name="monitor"></a>Monitor

### <a name="configuration-manager-console"></a>Console do Configuration Manager

Use o Configuration Manager implantação de monitoramento para o mesmo como qualquer outra implantação de sequência de tarefa e de aplicativo. Para obter mais informações, consulte os seguintes artigos:  

- [Monitorar aplicativo de console do Configuration Manager](/sccm/apps/deploy-use/monitor-applications-from-the-console)  

- [Monitorar implantações do sistema operacional](/sccm/osd/deploy-use/monitor-operating-system-deployments)  


### <a name="desktop-analytics-portal"></a>Portal de análise da área de trabalho

Use o portal de análise de área de trabalho para exibir o status de qualquer plano de implantação. Selecione o plano de implantação e, em seguida, selecione **visão geral do plano**.

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

Permitir que a execução do piloto para um período de tempo para coletar dados operacionais. Incentive os usuários de dispositivos piloto para testar aplicativos, suplementos e macros.

Quando sua implantação piloto atende aos seus critérios de êxito, vá para o próximo artigo para implantar na produção.
> [!div class="nextstepaction"]  
> [Implantar na produção](/sccm/desktop-analytics/deploy-prod)  
