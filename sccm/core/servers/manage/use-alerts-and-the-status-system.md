---
title: Alertas e o sistema de status | Microsoft Docs
description: "Configure alertas e use o sistema de status para ficar informado quanto ao estado da sua implantação do Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7341cc6e-9e08-41e4-bcc6-6c1ff12e85ca
caps.latest.revision: "10"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: ed692bdea055775890535d2666f09ba5f5c7c4e1
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="use-alerts-and-the-status-system-for-system-center-configuration-manager"></a>Usar alertas e o sistema de status para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Configure alertas e use o sistema de status interno para ficar informado quanto ao estado da sua implantação do System Center Configuration Manager.  


##  <a name="bkmk_Status"></a> Sistema de status  
 Todos os principais componentes do site geram mensagens de status que fornecem feedback sobre operações de site e hierarquia.    Essas informações podem mantê-lo informado sobre a integridade dos diferentes processos do site. Você pode ajustar o sistema de alerta para ignorar ruídos de problemas enquanto aumenta a visibilidade inicial de outras questões que precisam de atenção.  

 Por padrão, o sistema de status do Configuration Manager funciona sem configuração, usando as configurações apropriadas para a maioria dos ambientes. No entanto, você pode configurar:  

-   **Status summarizers:** você pode editar os status summarizers em cada site para controlar a frequência das mensagens de status que geram uma alteração de indicador de status para os quatro summarizers a seguir:  

    -   Summarizer de implantação de aplicativos  

    -   Summarizer de estatística de aplicativos  

    -   Summarizer de Status do Componente  

    -   Summarizer de status do sistema de site  

-   **Regras de filtro de status:** você pode criar novas regras de filtro de status, modificar a prioridade das regras, desabilitar ou habilitar regras e excluir regras não usadas em cada site.  

    > [!NOTE]  
    >  As regras de filtro de estado não oferecem suporte a uso de variáveis de ambiente para executar comandos externos.  

-   **Relatórios de status:** você pode configurar relatórios dos componentes do servidor e do cliente para modificar a forma como as mensagens de status são relatadas para o sistema de status do Configuration Manager e especificar para onde são enviadas as mensagens de status.  

    > [!WARNING]  
    >  Como as configurações de relatório padrão são apropriadas para a maioria dos ambientes, altere-as com cuidado. Quando aumenta o nível do relatório de status escolhendo relatar todos os detalhes de status, você pode aumentar a quantidade de mensagens de status a serem processadas, o que aumenta a carga de processamento no site do Configuration Manager. Se diminuir o nível de relatório de status, você poderá limitar a utilidade do status summarizers.  

Como o sistema de status mantém configurações separadas para cada site, você deve editar cada site individualmente.  

###  <a name="bkmk_configstatus"></a> Procedimentos para configurar o sistema de status  

##### <a name="to-configure-status-summarizers"></a>Para configurar os status summarizers  

1.  No console do Configuration Manager, navegue até **Administração** > **Configuração de Site** >**Sites** e selecione o site para o qual deseja configurar o sistema de status.  

2.  Na guia **Início** , no grupo **Configurações** , clique em **Summarizers de Status**.  

3.  Na caixa de diálogo **Summarizers de Status** , selecione o status summarizer que você deseja configurar e clique em **Editar** para abrir as propriedades desse summarizer. Se estiver editando o summarizer de Implantação de Aplicativos ou de Estatística de Aplicativos, vá para a etapa 5. Se estiver editando o Status do Componente, vá para a etapa 6. Se estiver editando o summarizer de Status do Sistema de Sites, vá para a etapa 7.  

4.  Use as etapas a seguir depois de abrir a página de propriedades do summarizer de implantação de aplicativos ou do summarizer de estatística de aplicativos:  

    1.  Na guia **Geral** da página de propriedades dos summarizers, configure os intervalos de resumo e clique em **OK** para fechar a página de propriedades.  

    2.  Clique em **OK** para fechar a caixa de diálogo **Summarizers de Status** e conclua esse procedimento.  

5.  Depois de abrir as páginas de propriedades para o Summarizer de Status do Componente, use as seguintes etapas:  

    1.  Na guia **Geral** da página de propriedades dos summarizers, configure os valores de período de limite e replicação.  

    2.  Na guia **Limites** , selecione o **Tipo de mensagem** que deseja configurar e então clique no nome de um componente na lista **Limites** .  

    3.  Na caixa de diálogo **Propriedades de Limite de Status** , edite os valores de aviso e limite crítico e clique em **OK**.  

    4.  Repita as etapas 6.b e 6.c conforme necessário e, quando tiver concluído, clique em **OK** para fechar as propriedades do summarizer.  

    5.  Clique em **OK** para fechar a caixa de diálogo **Summarizers de Status** e conclua esse procedimento.  

6.  Depois de abrir as páginas de propriedades para o summarizer de status do sistema de site, use as seguintes etapas:  

    1.  Na guia **Geral** da página de propriedades dos summarizers, configure os valores de replicação e de agendamento.  

    2.  Na guia **Limites** , especifique valores para os **Limites padrão** para configurar os limites padrão para exibições de status crítico e de aviso.  

    3.  Para editar os valores para **Objetos de armazenamento**específicos, selecione o objeto na lista **Limites específicos** , então clique no botão **Propriedades** para acessar e editar limites de aviso e críticos dos objetos de armazenamento. Clique em **OK** para fechar as propriedades dos objetos de armazenamento.  

    4.  Para criar um novo objeto de armazenamento, clique no botão **Criar Objeto** e especifique os valores de objetos de armazenamento. Clique em **OK** para fechar as propriedades dos objetos.  

    5.  Para excluir um objeto de armazenamento, selecione o objeto e então clique no botão **Excluir** .  

    6.  Repita as etapas de 7.b até 7.e conforme necessário. Quando tiver terminado, clique em **OK** para fechar as propriedades do summarizer.  

    7.  Clique em **OK** para fechar a caixa de diálogo **Summarizers de Status** e conclua esse procedimento.  

##### <a name="to-create-a-status-filter-rule"></a>Para criar uma regra de filtro de estado  

1.  No console do Configuration Manager, navegue até **Administração** > **Configuração de Site** >**Sites** e selecione o site em que deseja configurar o sistema de status.  

2.  Na guia **Início** , no grupo **Configurações** , clique em **Regras de Filtros de Status**. A caixa de diálogo **Regras de Filtro de Status** é aberta.  

3.  Clique em **Criar**.  

4.  No **Assistente para Criar Regra de Filtro de Status**, na página **Geral** , especifique um nome para a nova regra de filtro de estado e critérios de correspondência de mensagem para a regra, e então clique em **Avançar**.  

5.  Na página **Ações** , especifique as ações a serem realizadas quando as mensagens de status correspondem à regra de filtro, e clique em **Avançar**.  

6.  Na página **Resumo** , examine os detalhes da nova regra e conclua o assistente.  

    > [!NOTE]  
    >  O Configuration Manager requer apenas que a nova regra de filtro de status tenha um nome. Se a regra for criada mas você não especificar nenhum critério para processar mensagens de status, a regra de filtro de estado não terá efeito. Esse comportamento permite que você crie e organize regras antes de configurar os critérios de filtro de estado para cada regra.  

##### <a name="to-modify-or-delete-a-status-filter-rule"></a>Para modificar ou excluir uma regra de filtro de estado  

1.  No console do Configuration Manager, navegue até **Administração** > **Configuração de Site** >**Sites** e selecione o site em que deseja configurar o sistema de status.  

2.  Na guia **Início** , no grupo **Configurações** , clique em **Regras de Filtros de Status**.  

3.  Na caixa de diálogo **Regras de Filtros de Status** , selecione a regra que deseja modificar e então execute uma das ações a seguir:  

    -   Clique em **Aumentar Prioridade** ou **Diminuir Prioridade** para alterar a ordem de processamento da regra de filtro de estado. Em seguida, selecione outra ação ou vá para a etapa 8 deste procedimento para concluir essa tarefa.  

    -   Clique em **Desabilitar** ou **Habilitar** para alterar o estado da regra. Depois de alterar o estado da regra, selecione outra ação ou vá para a etapa 8 deste procedimento para concluir essa tarefa.  

    -   Clique em **Excluir** se deseja excluir a regra de filtro de estado desse site, e clique em **Sim** para confirmar a ação. Depois de excluir uma regra, selecione outra ação ou vá para a etapa 8 deste procedimento para concluir essa tarefa.  

    -   Clique em **Editar** se deseja alterar os critérios da regra de mensagem de estado e continue na etapa 5 deste procedimento.  

4.  Na guia **Geral** da caixa de diálogo propriedades de regra de filtro de status, modifique a regra e os critérios de correspondência de mensagem.  

5.  Na guia **Ações** , modifique as ações a serem realizadas quando as mensagens de status correspondem à regra de filtro.  

6.  Clique em **OK** para salvar as alterações.  

7.  Clique em **OK** para fechar a caixa de diálogo **Regras de Filtros de Status** .  

##### <a name="to-configure-status-reporting"></a>Para configurar o relatório de status  

1.  No console do Configuration Manager, navegue até **Administração** > **Configuração de Site** > **Sites** e selecione o site em que deseja configurar o sistema de status.  

2.  Na guia **Início** , no grupo **Configurações** , clique em **Configurar Componentes do Site**e selecione **Relatório de Status**.  

3.  Na caixa de diálogo **Propriedades do Componente de Relatório de Status** , especifique as mensagens de status do componente servidor e cliente que deseja relatar ou registrar em log:  

    1.  Configure o **Relatório** para enviar mensagens de status para o sistema de mensagens de status do Configuration Manager.  

    2.  Configure **Log** para gravar o tipo e a gravidade das mensagens de status para o log de eventos do Windows.  

4.  Clique em **OK**.  

###  <a name="BKMK_MonitorSystemStatus"></a> Monitorar o sistema de status do Gerenciador de Configurações  
 O**status do sistema** no Configuration Manager fornece uma visão geral das operações gerais de sites e de servidor do site de sua hierarquia. Ele pode revelar problemas operacionais de componentes ou servidores do sistema de sites, e você pode usar o status do sistema para analisar detalhes específicos de diferentes operações do Configuration Manager. Você monitora o status do sistema no nó **Status do Sistema** do espaço de trabalho **Monitoramento** no console do Configuration Manager.  

 A maioria dos componentes e funções do sistema de sites do Configuration Manager gera mensagens de status. Os detalhes das mensagens de status são registrados em cada log operacional de componentes, mas também enviados ao banco de dados do site onde estão resumidos e apresentados em um pacote cumulativo de atualizações geral de cada componente ou da integridade do sistema de site. Esses pacotes cumulativos de atualizações de mensagens de status fornecem detalhes sobre informações de operações normais e os detalhes de avisos e erros. Você pode configurar os limites em que os avisos e erros são acionados e ajustar o sistema para garantir que as informações de pacote cumulativo de atualizações ignorem os problemas conhecidos que não são relevantes para você enquanto chama a atenção para problemas reais em servidores e operações de componentes que você talvez precise investigar.  

 O status do sistema é replicado para outros sites em uma hierarquia como dados do site e não dados globais. Isso significa que você vê somente o status do site ao qual seu console do Configuration Manager se conecta e dos sites filho abaixo desse site. Portanto, considere conectar seu console do Configuration Manager ao site de nível superior de sua hierarquia ao exibir o status do sistema.  

 Use a tabela a seguir para identificar e saber quando usar as diferentes exibições de status do sistema.  

|Nó|Mais informações|  
|----------|----------------------|  
|Status do site|Use esse nó para exibir um pacote cumulativo de atualizações do status de cada sistema de site para analisar a integridade de cada servidor do sistema de site. A integridade do sistema de site é determinada pelos limites que você configura para cada site no **Summarizer de Status do Sistema de Site**.<br /><br /> Você pode exibir as mensagens de status para cada sistema de site, definir limites para as mensagens de status e gerenciar a operação dos componentes em sistemas de site usando o **Configuration Manager Service Manager**.|  
|Status do componente|Use esse nó para ver um pacote cumulativo de atualizações do status de cada componente do Configuration Manager para analisar a integridade operacional do componente. A integridade do componente é determinada pelos limites que você configura para cada site no **Summarizer de Status do Componente**.<br /><br /> Você pode exibir as mensagens de status para cada componente, definir limites para as mensagens de status e gerenciar a operação dos componentes usando o **Configuration Manager Service Manager**.|  
|Registros conflitantes|Use esse nó para exibir mensagens de status sobre clientes que podem ter registros conflitantes.<br /><br /> O Configuration Manager usa a ID de hardware para tentar identificar clientes que possam ser duplicatas e alertar você quando houver registros conflitantes. Por exemplo, se você precisar reinstalar um computador, a ID de hardware será a mesma, mas o GUID que o Configuration Manager usa poderá ser alterado.|  
|Consultas de mensagens de status|Use esse nó para consultar mensagens de status sobre eventos específicos e os detalhes relacionados. Você pode usar consultas de mensagens de status para localizar as mensagens de status relacionadas a eventos específicos.<br /><br /> É possível usar com frequência as consultas de mensagens de status para identificar quando um componente, uma operação ou um objeto específico do Configuration Manager foi modificado, bem como a conta que foi usada para fazer a modificação. Por exemplo, você pode executar uma consulta interna em **Coleções Criadas, Modificadas ou Excluídas** para identificar quando uma coleção específica foi criada e a conta de usuário usada para criá-la.|  

####  <a name="bkmk_managestatus"></a> Gerenciar o status do site e do componente  
 Use as seguintes informações para gerenciar o status do site e do componente:  

-   Para configurar os limites para o status do sistema, consulte [Procedimentos para configurar o sistema de status](#bkmk_configstatus).  

-   Para gerenciar componentes individuais no Configuration Manager, use o **Configuration Manager Service Manager**.  

####  <a name="bkmk_view"></a> Exibir mensagens de status  
 Você pode exibir as mensagens de status para servidores do sistema de site individuais e componentes.  

 Para exibir as mensagens de status no console do Configuration Manager, selecione um componente ou servidor específico do sistema de sites e clique em **Mostrar Mensagens**. Ao exibir mensagens, você pode selecionar para exibir tipos específicos de mensagens ou mensagens de um período de tempo especificado e também pode filtrar os resultados baseados nos detalhes de mensagens de status.  

##  <a name="bkmk_Alerts"></a> Alertas  
 Os alertas do Configuration Manager são gerados por algumas operações quando ocorre uma condição específica.  

-   Normalmente, os alertas são gerados quando ocorre um erro que você deve resolver.  

-   Podem ser gerados alertas para alertá-lo de que uma condição existe, para que você possa continuar a monitorar a situação.  

-   Alguns alertas são configurados por você, como alertas de status do cliente e do Endpoint Protection, enquanto outros são configurados automaticamente  

-   Você pode configurar assinaturas para alertas, que por sua vez podem enviar detalhes por email, aumentando o conhecimento dos principais problemas  

 Use a tabela a seguir para encontrar informações sobre como configurar alertas e inscrições de alerta no Configuration Manager:  


|Ação|Mais informações|  
|------------|----------------------|  
|Configurar alertas do Endpoint Protection para uma coleção|Consulte **Como configurar alertas para o Endpoint Protection no Configuration Manager** em [Configurando o Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/configure-endpoint-protection.md)|  
|Configurar alertas de status do cliente para uma coleção|Consulte [Como configurar o status do cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-status.md).|  
|Gerenciar alertas do Configuration Manager|Consulte a seção [Management tasks for alerts](#BKMK_Manage) neste tópico.|  
|Configurar assinaturas de email para alertas|Consulte a seção [Management tasks for alerts](#BKMK_Manage) neste tópico.|  
|Monitorar alertas|Consulte a seção [Monitorar alertas](#BKMK_MonitorAlerts)|  

###  <a name="BKMK_Manage"></a> Management tasks for alerts  

##### <a name="to-manage-general-alerts"></a>Para gerenciar alertas gerais  

1.  No console do Configuration Manager, navegue até **Monitoramento** > **Alertas** e selecione uma tarefa de gerenciamento.  

  Use a tabela a seguir para obter mais informações sobre as tarefas de gerenciamento que podem requerer informações adicionais antes de você selecioná-las.  

|Tarefa de gerenciamento|Detalhes|  
    |---------------------|-------------|  
    |**Configure**|Abra a caixa de diálogo *&lt;nome do alerta*\>**Propriedades**, em que você pode modificar o nome, a severidade e os limites do alerta selecionado. Se você alterar a severidade do alerta, essa configuração afetará a forma como os alertas são exibidos no console do Configuration Manager.|  
    |**Editar comentário**|Insira um comentário para os alertas selecionados. Esses comentários são exibidos com o alerta no console do Configuration Manager.|  
    |**Adiar**|Suspende o monitoramento do alerta até a data especificada. Nessa data, o estado do alerta será atualizado.<br /><br /> Você só pode adiar um alerta quando ele estiver ativo.|  
    |**Criar assinatura**|Abre a caixa de diálogo **Nova Assinatura** , em que você pode criar uma assinatura de email para o alerta selecionado.|  

##### <a name="to-configure-endpoint-protection-alerts-for-a-collection"></a>Para configurar alertas do Endpoint Protection para uma coleção  

1.  pendente  

##### <a name="to-configure-client-status-alerts-for-a-collection"></a>Para configurar alertas de status do cliente para uma coleção  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** >   **Coleções de Dispositivos**.  

2.  Na lista **Coleções de Dispositivos** , selecione a coleção para a qual deseja configurar alertas e, então, na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

    > [!NOTE]  
    >  Você não pode configurar alertas para coleções de usuário.  

3.  Na guia **Alertas** da caixa de diálogo *&lt;Nome da Coleção*\>**Propriedades**, clique em **Adicionar**.  

    > [!NOTE]  
    >  A guia **Alertas** torna-se visível somente se a função de segurança com a qual você está associado tiver permissões para alertas.  

4.  Na caixa de diálogo **Adicionar Novas Alertas da Coleção** , escolha os alertas que você deseja que sejam gerados quando os limites de status do cliente ficarem abaixo de um valor específico, então clique em **OK**.  

5.  Na lista **Condições** da guia **Alertas** , selecione cada alerta de status do cliente e então especifique as informações a seguir.  

    -   **Nome do Alerta** – Aceite o nome padrão ou insira um novo nome para o alerta.  

    -   **Severidade do Alerta** – Na lista suspensa, escolha o nível de alerta que será exibido no console do Configuration Manager.  

    -   **Gerar alerta** – Especifique o percentual de limite para o alerta.  

6.  Clique em **OK** para fechar a caixa de diálogo *&lt;Nome da Coleção*\>**Propriedades**.  

##### <a name="to-configure-email-notification-for-alerts"></a>Para configurar notificações por email para alertas  

1.  No console do Configuration Manager, navegue para **Monitoramento** > **Alertas** > **Assinaturas**.  

2.  Na guia **Início** , no grupo **Criar** , clique em **Configurar Notificação de Email**.  

3.  Na caixa de diálogo **Propriedades do Componente de Notificação de Email** , especifique as seguintes informações:  

    -   **Habilitar notificação por email de alertas**: marque esta caixa de seleção para habilitar o Configuration Manager a usar um servidor SMTP para enviar alertas por email.  

    -   **FQDN ou Endereço IP do servidor SMTP para enviar alertas de email**: insira o FQDN (nome de domínio totalmente qualificado) ou o endereço IP e a porta SMTP do servidor de email que você deseja usar para esses alertas.  

    -   **Conta de Conexão de Servidor SMTP**: especifique o método de autenticação que o Configuration Manager deve usar para conectar o servidor de email.  

    -   **Endereço de remetente para alertas de email**: especifique o endereço de email do qual os emails de alerta são enviados.  

    -   **Testar Servidor SMTP**: envia um email de teste para o endereço de email especificado em **Endereço de remetente para alertas de email**.  

4.  Clique em **OK** para salvar as configurações e fechar a caixa de diálogo **Propriedades dos Componentes de Configuração de Email** .  

##### <a name="to-subscribe-to-email-alerts"></a>Para se inscrever em alertas de email  

1.  No console do Configuration Manager, navegue até **Monitoramento** > **Alertas**.  

2.  Selecione um alerta e, na guia **Início** , no grupo **Assinatura** , clique em **Criar assinatura**.  

3.  Na caixa de diálogo **Nova Assinatura** , especifique as seguintes informações:  

    -   **Nome**: forneça um nome para identificar a assinatura de email. Você pode usar até 255 caracteres.  

    -   **Endereço de email**: insira os endereços de email para os quais deseja que o alerta seja enviado. Você pode separar vários endereços de email usando ponto-e- vírgula.  

    -   **Idioma do email**: na lista, especifique o idioma do email.  

4.  Clique em **OK** para fechar a caixa de diálogo **Nova Assinatura** e criar a assinatura de email.  

    > [!NOTE]  
    >  Você pode excluir e editar assinaturas no espaço de trabalho **Monitoramento** expandindo o nó **Alertas** e clicando no nó **Assinaturas** .  

###  <a name="BKMK_MonitorAlerts"></a> Monitorar alertas  
 Você pode exibir alertas no nó **Alertas** no espaço de trabalho **Monitoramento** . Alertas têm um dos seguintes estados de alerta:  

-   **Nunca disparado**: a condição do alerta ainda não foi atendida.  

-   **Ativo**: a condição do alerta foi atendida.  

-   **Cancelado**: a condição de um alerta ativo deixou de ser atendida. Esse estado indica que a condição que causou o alerta agora está resolvida.  

-   **Adiado**: um usuário administrativo configurou o Configuration Manager para avaliar o estado do alerta posteriormente.  

-   **Desabilitado**: o alerta foi desabilitado por um usuário administrativo. Quando um alerta está nesse estado, o Configuration Manager não atualiza o alerta mesmo que o estado do alerta seja alterado.  

 Você pode executar uma das ações a seguir quando o Configuration Manager gerar um alerta:  

-   Resolva a condição que causou o alerta, por exemplo, você resolve um problema de rede ou de configuração que gerou o alerta. Após o Configuration Manager detectar que o problema não existe mais, o estado do alerta mudará para **Cancelado**.  

-   Se o alerta é um problema conhecido, você pode adiar o alerta para um período específico. No período especificado, o Configuration Manager atualizará o alerta para seu estado atual.  

     Você pode adiar um alerta apenas quando ele está ativo.  

-   Você pode editar o **Comentário** de um alerta para que os outros usuários administrativos possam ver que você está ciente do alerta. Por exemplo, no comentário você pode identificar como resolver a condição, fornecer informações sobre o status atual da condição ou explicar o motivo de ter adiado o alerta.  
