---
title: "Monitorar a replicação | Microsoft Docs"
description: "Saiba como monitorar a infraestrutura e as operações no Configuration Manager quando o espaço de trabalho Monitoramento no console."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fab4d67-8d2a-45ce-8b06-471280102cf6
caps.latest.revision: 11
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 132803a1aa9aad5c5462686bd656688418e47d07
ms.contentlocale: pt-br
ms.lasthandoff: 12/16/2016


---
# <a name="monitor-hierarchy-and-replication-infrastructure-in-system-center-configuration-manager"></a>Monitorar a infraestrutura de hierarquia e de replicação no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para monitorar a infraestrutura e as operações no System Center Configuration Manager, use o espaço de trabalho **Monitoramento** no console do Configuration Manager.  

> [!NOTE]  
>  A exceção para esse local é Migração, que é monitorada diretamente no nó **Migração** do espaço de trabalho **Administração** . Para obter mais informações, consulte [Operações de migração para o System Center Configuration Manager](../../../core/migration/operations-for-migration.md).  

 Além de usar o console do Configuration Manager para monitorar, é possível usar os relatórios do Configuration Manager ou exibir arquivos de log do Configuration Manager para componentes do Configuration Manager. Para obter informações sobre os relatórios, consulte [Relatórios no System Center Configuration Manager](../../../core/servers/manage/reporting.md). Para obter informações sobre os arquivos de log, consulte [Arquivos de log no System Center Configuration Manager](../../../core/plan-design/hierarchy/log-files.md).  

 Ao monitorar sites, procure sinais que indiquem problemas que requeiram a execução de uma ação. Por exemplo:  

-   Uma lista de pendências de arquivos em servidores e sistemas de sites.  

-   Mensagens de status que indiquem um erro ou um problema.  

-   Falha na comunicação intrassite.  

-   Erro e mensagens de aviso no log de eventos do sistema nos servidores.  

-   Erro e mensagens de aviso no log de erros do Microsoft SQL Server.  

-   Sites ou clientes que não relatam a muito tempo.  

-   Resposta lenta do banco de dados do SQL Server.  

-   Sinais de falha de hardware.  

Para minimizar o risco de falha em um site, se as tarefas de monitoramento revelarem sinais de problemas, investigue a origem do problema e repare-o assim que possível.  



##  <a name="BKMK_MonintorMgmtTasks"></a> Monitorar tarefas comuns de gerenciamento do Configuration Manager  
 O Configuration Manager fornece monitoramento interno de dentro do console do Configuration Manager. Você pode monitorar muitas tarefas incluindo as relacionadas a atualizações de software, gerenciamento de energia e implantação do conteúdo em toda a hierarquia.  

 Use as informações a seguir para ajudar você a monitorar as tarefas comuns do Configuration Manager:  

 **Alertas**  
   Veja [Monitorar alertas](../../../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorAlerts) em [Usar alertas e o sistema de status para o System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Configurações de conformidade**  
   Veja [Como monitorar as configurações de conformidade no System Center Configuration Manager](../../../compliance/deploy-use/monitor-compliance-settings.md).  

 **Implantação de conteúdo**  
   Para obter informações gerais sobre o monitoramento de conteúdo, consulte [Gerenciar conteúdo e infraestrutura de conteúdo do System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

Para obter informações sobre monitoramento de tipos específicos de implantação de conteúdo:
-   Para monitorar aplicativos, consulte [Monitorar aplicativos com o System Center Configuration Manager](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

-   Para monitorar pacotes e programas, consulte Como gerenciar pacotes e programas em [Pacotes e programas no System Center Configuration Manager](../../../apps/deploy-use/packages-and-programs.md).  

**Endpoint Protection**  
   Consulte [Como monitorar o Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md).  

**Monitorar o gerenciamento de energia**  
 Consulte [Como monitorar e planejar o gerenciamento de energia no System Center Configuration Manager](../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

**Monitorar a medição de software**  
Consulte [Monitorar o uso de aplicativos com a medição de software no System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

**Monitorar atualizações de software**  
 Consulte [Monitorar atualizações de software no System Center Configuration Manager](../../../sum/deploy-use/monitor-software-updates.md).  


##  <a name="BKMK_MonitorInfrastructure"></a> Monitorar a infraestrutura de hierarquia do Configuration Manager  
O Configuration Manager oferece diversos métodos para monitorar o status e as operações da sua hierarquia. Você pode verificar o status dos sites do sistema em toda a hierarquia, monitorar a replicação entre sites em uma hierarquia de sites ou exibição geográfica, monitorar links de replicação entre sites para replicação de banco de dados e usar a ferramenta Replication Link Analyzer para corrigir problemas de replicação.  

###  <a name="BKMK_SH_Node"></a> Sobre o nó da Hierarquia do Site  
O nó **Hierarquia do site** do espaço de trabalho **Monitoramento** oferece uma visão geral da sua hierarquia e dos links entre sites do Configuration Manager. Você pode usar dois modos de exibição:  

-   **Diagrama Hierárquico**: Esse modo de exibição mostra a sua hierarquia como um mapa de topologia que foi simplificado para mostrar somente informações essenciais.  

-   **Exibição Geográfica**: Este modo exibe os sites em um mapa geográfico, mostrando os locais de site que você configurar.  

Use o nó **Hierarquia do Site** para monitorar a saúde de cada site e os links de replicação entre sites e suas relações com fatores externos, como uma localização geográfica.  

Como o status do site e o status do link entre sites são replicados como dados do site e não como dados globais, quando você conecta o console do Configuration Manager a um a site primário filho, não é possível exibir o status do site ou do link a outros sites primários ou seus sites secundários filhos. Por exemplo, em uma hierarquia de site multiprimária, quando o seu console do Configuration Manager se conecta a um site primário, é possível exibir o status de sites secundários filho, do site primário e do site de administração central, mas não é possível ver o status de outros nós da hierarquia abaixo do site de administração central.  

 Use o comando **Definir Configurações** para controlar como a exibição da hierarquia do site é renderizada. As configurações no nó **Hierarquia do Site** feitas quando o seu console do Configuration Manager é conectado a um site são replicadas para todos os outros sites.  

#### <a name="hierarchy-diagram"></a>Diagrama Hierárquico  
 O diagrama hierárquico exibe seus sites em um mapa de topologia. Nessa exibição, você pode selecionar um site e exibir um resumo da mensagem de status desse site, executar uma consulta drill-through para exibir mensagens de status e acessar a caixa de diálogo **Propriedades** dos sites.  

 Além disso, você pode colocar o ponteiro do mouse em um site ou link de replicação entre sites para exibir status de alto nível para esse objeto. Como o status do link de replicação não é replicado globalmente, em uma hierarquia com vários sites primários, é necessário conectar o seu console do Configuration Manager ao site de administração central para exibir os detalhes do link de replicação entre todos os sites.  

 As seguintes opções modificam o diagrama hierárquico:  

-   **Grupos**: Você pode configurar o número de sites primários e secundários que disparam uma alteração na exibição de diagrama hierárquico que combina os sites em um único objeto. Quando os sites são combinados em um único objeto, você pode ver o número total de sites e um rollup de mensagens de status e status de sites de alto nível. As configurações de grupo não afetam o modo de exibição geográfico.  

-   **Sites favoritos**: Você pode especificar sites individuais como favoritos. Um ícone de estrela identifica um site favorito no diagrama hierárquico. Sites favoritos não são combinados com outros sites quando você usa grupos e são sempre exibidos individualmente.  

#### <a name="geographical-view"></a>Exibição Geográfica  
 O modo de exibição geográfica mostra a localização de cada site em um mapa geográfico. Somente os sites configurados com um local serão exibidos. Quando você seleciona um site nesse modo de exibição, os links de replicação para sites pai ou filho são mostrados. Diferentemente da exibição de diagrama hierárquico, não é possível exibir detalhes da mensagem de status do site ou do link de replicação nesse modo de exibição.  

> [!NOTE]  
>  Para usar a exibição geográfica, o computador ao qual o seu console do Configuration Manager se conecta deve ter o Internet Explorer instalado e poder acessar Bing Mapas usando o protocolo HTTP.  

A opção a seguir modifica a exibição geográfica.  

-   **Local do Site**: Você pode especificar uma localização geográfica para cada site. Você pode especificar a localização como um endereço de rua, o nome de um local como o nome de uma cidade ou por coordenadas de latitude e longitude. Por exemplo, para usar a latitude e a longitude de Redmond, Washington, você especificaria **N 47 40 26.3572 W 122 7 17.4432** como a localização do site. Você não precisa especificar os símbolos para graus, minutos ou segundos de longitude ou latitude. O Configuration Manager usa o Bing Mapas para exibir o local na exibição geográfica. Isso oferece a você a opção de exibir sua hierarquia em relação a um local geográfico, o que pode fornecer informações sobre questões regionais que podem afetar sites específicos ou a replicação entre sites.  

     Quando você especifica um local, você pode usar a caixa **Local** para pesquisar um site específico da sua hierarquia. Com o site selecionado, insira o local como um nome de cidade ou endereço na coluna **Local** . O Configuration Manager usa o Bing Mapas para resolver o local.  

###  <a name="BKMK_MonitorRepLinksAndStatuss"></a> Como monitorar o status de replicação e links de replicação de banco de dados  
 Além dos detalhes de alto nível que são acessíveis no nó **Hierarquia do Site** do espaço de trabalho **Monitoramento** . Você também pode monitorar os detalhes da replicação de banco de dados ao usar o nó **Replicação de Banco de Dados** do espaço de trabalho **Monitoramento** . Em **Replicação de Banco de Dados**, é possível monitorar o status dos links de replicação entre sites e os detalhes de inicialização e de replicação de grupos de replicação no site ao qual o seu Configuration Manager está conectado.  

> [!TIP]  
>  Embora um nó **Replicação de Banco de Dados** também apareça no nó **Configuração da Hierarquia** , no espaço de trabalho **Administração** , não é possível exibir o status dos links de replicação de banco de dados desse local.  

####  <a name="BKMK_MonitorReplicationLinks"></a> Status do link de replicação  
A replicação de banco de dados entre sites envolve a replicação de diversos conjuntos de informações, chamados de grupos de replicação. Cada grupo de replicação replica com diferentes prioridades de replicação. Por padrão, os dados contidos em um grupo de replicação e a frequência da replicação não podem ser modificados.  

 Quando um link de replicação está ativo e não tem um status com falha ou degradado, todos os grupos de replicação são replicados em tempo adequado. Quando ocorrer falha de um ou mais grupos de replicação ao concluir a replicação no período de tempo esperado, o link será exibido como degradado. Os links degradados ainda funcionarão, mas será necessário monitorá-los para garantir que eles retornem ao status de ativos ou investigá-los para garantir que não ocorram mais degradações ou falhas de replicação.  

 Para cada link de replicação, é possível especificar o número de vezes que um grupo de replicação que não foi replicado com êxito tenta ser replicado antes de o status do link ser definido como degradado ou com falha. Mesmo que todos, exceto um grupo de replicação seja replicado com êxito, o status do link será definido como degradado ou com falha, pois ocorreu falha em um grupo de replicação ao concluir a replicação no número de tentativas especificada. Para obter informações sobre limites de replicação, veja a seção [Limites de replicação de banco de dados](../../../core/servers/manage/data-transfers-between-sites.md#BKMK_DBRepThresholds) no tópico [Transferência de dados entre sites no System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md).  

 Use as informações da tabela a seguir para saber o status dos links de replicação que podem exigir mais investigação.  

|Descrição do link|Mais informações|  
|----------------------|----------------------|  
|**O link está ativo**|Nenhum problema foi detectado e a comunicação através do link está atualizada.|  
|**O link está degradado**|A replicação está funcional, mas pelo menos um objeto ou grupo de replicação está atrasado. Monitore os links que estão nesse estado e verifique as informações de ambos os sites no link para ver se há indicações que o link pode falhar.<br /><br /> Um link também pode exibir um status de degradado quando o site que recebe dados replicados não consegue confirmar rapidamente os dados no banco de dados. Isso pode acontecer quando grandes volumes de dados são replicados. Por exemplo, se você implantar uma atualização de software em um grande número de computadores, o volume de dados replicados poderá levar algum tempo para ser processado pelo site pai do link. Um atraso de processamento no site pai pode resultar em status do link definido como degradado até que o site pai possa processar a lista de pendências de dados.|  
|**Falha no link**|A replicação não está funcionando. É possível que um link de replicação se recupere sem ação adicional. Você pode usar o Replication Link Analyzer para investigar e ajudar a corrigir a replicação nesse link.<br /><br /> Esse status também pode indicar um problema com a rede física entre o site pai e o site filho no link de replicação.|  

 Embora o site pai esteja em processo de atualização para um novo service pack e você exiba o status do link a partir do site filho, o status do link será exibido como ativo. Após a atualização, até que o site filho também tenha o mesmo service pack que o site pai, o status do link será exibido como ativo, quando exibido a partir do site pai, e como sendo configurado, quando exibido do site filho.  

####  <a name="BKMK_MonitorReplicationStatus"></a> Status de replicação  
 Você pode usar o nó **Replicação de Banco de Dados** no espaço de trabalho **Monitoramento** , para exibir o status da replicação para um link de replicação e exibir detalhes sobre o banco de dados do site em cada site do link de replicação. Também é possível exibir detalhes sobre os grupos de replicação. Para exibir detalhes, selecione um link de replicação e a guia apropriada do status de replicação que deseja exibir. Veja a seguir detalhes sobre as diferentes guias para o status de replicação.  

 **Resumo**  
 Exiba informações de alto nível sobre a replicação de dados do site e dados globais entre os dois sites de um link.  

 Você também pode clicar em **Exibir relatórios para dados de tráfego de histórico** para exibir um relatório que mostre detalhes sobre a largura de banda da rede por replicação no link de replicação.  

 **Site Pai**  
 Para o site pai em um link de replicação, exiba detalhes sobre o banco de dados, que incluem:  

-   Portas de firewall para o SQL Server  

-   Espaço livre em disco  

-   Locais de arquivos de banco de dados  

-   Certificados  

**Site Filho**  
 Para o site filho em um link de replicação, exiba detalhes sobre o banco de dados, que incluem:  

-   Portas de firewall para o SQL Server  

-   Espaço livre em disco  

-   Locais de arquivos de banco de dados  

-   Certificados  

**Detalhe de Inicialização**    
 Exiba o status de inicialização para grupos de replicação que são replicados através do link de replicação. Essas informações podem ajudá-lo a identificar quando a inicialização de dados de replicação está em andamento ou falhou.  

 Além disso, você pode usar essas informações para identificar quando um site pode estar no modo de interoperabilidade. O modo de interoperabilidade ocorre quando o site filho não executa a mesma versão do Configuration Manager que o site pai.  

**Detalhe de Replicação**    
 Exiba o status da replicação para cada grupo de replicação que replica entre o link. Use essas informações para ajudá-lo a identificar problemas e atraso na replicação de dados específicos e também para determinar os limites de replicação de banco de dados apropriados para esse link. Para obter informações sobre limites de replicação de bancos de dados, veja a seção [Limites de replicação de banco de dados](../../../core/servers/manage/data-transfers-between-sites.md#BKMK_DBRepThresholds) no tópico [Transferência de dados entre sites no System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md).  

> [!TIP]  
>  Os grupos de replicação de dados do site são enviados somente do site filho para o site pai. Os grupos de replicação para dados globais replicam em ambas as direções.  

###  <a name="BKMK_RLA"></a> Sobre o Replication Link Analyzer  
 O Configuration Manager inclui o **Replication Link Analyzer**, usado para analisar e reparar problemas de replicação. Você pode usar o Replication Link Analyzer para corrigir as falhas de link de replicação quando a replicação falha ou quando ela para de funcionar, mas não foi ainda reportada com falha. O Replication Link Analyzer pode ser usado para corrigir problemas de replicação entre os computadores a seguir na hierarquia do Configuration Manager (a direção da falha de replicação não importa):  

-   Entre um servidor do site e o servidor de banco de dados do site.  

-   Entre um servidor de banco de dados do site de sites e outro computador do banco de dados de site de sites (replicação entre sites).  

É possível executar o Replication Link Analyzer no console do Configuration Manager ou em um prompt de comando:  

-   Para executar no console do Configuration Manager: no espaço de trabalho **Monitoramento**, clique no nó **Replicação do Banco de Dados**, selecione o link de replicação que deseja analisar e, no grupo **Replicação do Banco de Dados**, na guia **Início**, selecione **Replication Link Analyzer**.  

-   Para executar em um prompt de comando, digite o seguinte comando: **%path%\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManager.ReplicationLinkAnalyzer.Wizard.exe &lt;FQDN do servidor do site de origem\> &lt;FQDN do servidor do site de destino\>**  

Ao executar o Replication Link Analyzer, ele detecta os problemas usando uma série de regras e verificações de diagnóstico. Quando a ferramenta é executada, você pode exibir os problemas que ela identifica. Quando as instruções para resolver um problema são conhecidas, elas são exibidas. Se o Replication Link Analyzer pode corrigir automaticamente o problema, você vai conhecer essa opção. Quando o Replication Link Analyzer é concluído, ele salva os resultados no seguinte relatório baseado em XML e um arquivo de log na área de trabalho do usuário que executa a ferramenta:  

-   ReplicationAnalysis.xml  

-   ReplicationLinkAnalysis.log  

Quando o Replication Link Analyzer é executado, ele interrompe os seguintes serviços enquanto corrige alguns problemas e reinicia esses serviços quando a correção estiver concluída:  

-   SMS_SITE_COMPONENT_MANAGER  

-   SMS_EXECUTIVE  

Se o Replication Link Analyzer falha em concluir a correção, analise o servidor do site e reinicie esses serviços se eles estão interrompidos.  

As ações de correção e investigação com e sem êxito são registradas em log a fim de fornecer detalhes adicionais que não são apresentados na interface da ferramenta.  

**Pré-requisitos para usar o Replication Link Analyzer:**  

-   A conta que você usa para executar o Replication Link Analyzer deve ter os direitos de administrador local em cada computador que está envolvido no link de replicação. A conta não exige uma função de segurança de administração baseada em funções. Portanto, um usuário administrativo com acesso ao nó **Replicação do Banco de Dados** pode executar a ferramenta no console do Configuration Manager ou um administrador do sistema com direitos suficientes em cada computador pode executar a ferramenta em um prompt de comando.  

-   A conta que você usa para executar o Replication Link Analyzer deve ter direitos sysadmin em cada banco de dados do SQL Server que está envolvido no link de replicação.  

**Problemas conhecidos do Replication Link Analyzer:**  

-   Com o lançamento do System Center Configuration Manager versão 1511, o Replication Link Analyzer gera erros de certificado do SQL Server Service Broker para sites primários atualizados do System Center 2012 Configuration Manager. Isso ocorre devido a alterações nos nomes dos certificados introduzidos com a versão 1511, para a qual o Replication Link Analyzer ainda não foi atualizado. Esses erros podem ser ignorados com segurança.  

###  <a name="BKMK_ProcsforMonitoringReplication"></a> Procedimentos para monitorar a replicação de banco de dados  

##### <a name="to-monitor-high-level-site-to-site-database-replication-status"></a>Para monitorar o status de replicação de banco de dados de site a site de alto nível    
1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , clique em **Hierarquia do Site** para abrir a exibição do **Diagrama Hierárquico** .  

3.  Pause brevemente o ponteiro do mouse na linha entre os dois sites para exibir o status da replicação de dados do site e dados globais para esses sites.  

##### <a name="to-monitor-the-replication-status-for-a-replication-link"></a>Para monitorar o status da replicação para um link de replicação    
1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , clique em **Replicação do Banco de Dados**e selecione o link de replicação que deseja monitorar. Em seguida, no espaço de trabalho, selecione a guia apropriada para exibir os diferentes detalhes sobre o status de replicação para esse link.  

