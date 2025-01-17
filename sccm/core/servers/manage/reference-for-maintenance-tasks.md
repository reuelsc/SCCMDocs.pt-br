---
title: Referência para tarefas de manutenção
titleSuffix: Configuration Manager
description: Leia detalhes para cada uma das tarefas de manutenção de site do System Center Configuration Manager e se essas tarefas são habilitadas por padrão.
ms.date: 3/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 68dc6acd-5848-47a4-b4c1-ffa40e47890b
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 24e76f9281158aa28e153efe9124ba2adf94a14d
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67676369"
---
# <a name="reference-for-maintenance-tasks-for-system-center-configuration-manager"></a>Referência para tarefas de manutenção do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico lista detalhes de cada uma das tarefas de manutenção de site do System Center Configuration Manager e em quais tipos de site a tarefa está disponível. Cada entrada também indica se a tarefa é habilitada ou não por padrão. Para saber mais sobre como planejar e configurar sites para executar tarefas de manutenção, veja [Tarefas de manutenção do System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md).  

**Fazer backup do servidor do site**: use essa tarefa para preparar a recuperação de dados críticos. Você pode criar um backup de suas informações críticas para restaurar um site e o banco de dados do Configuration Manager. Para obter mais informações, consulte [Backup e recuperação para o System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  

-   **Site de administração central**: Habilitada    
-   **Site primário**: não ativado    
-   Site secundário: Não disponível  

**Verificar título do aplicativo com informações de inventário**: use essa tarefa para manter a consistência entre os títulos de software relatados no inventário de software e os títulos de software no catálogo do Asset Intelligence. Para obter mais informações, consulte [Introdução ao Asset Intelligence no System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

-   **Site de administração central**: Habilitada    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Limpar sinalizador de instalação**: use essa tarefa para remover o sinalizador instalado de clientes que não enviam um registro de descoberta de pulsação durante o período de **Redescoberta de Cliente**. O sinalizador instalado impede a instalação automática do cliente por push em um computador que possa ter um cliente do Configuration Manager ativo.  

-   Site da administração central: Não disponível    
-   **Site primário**: não ativado    
-   Site secundário: Não disponível  

**Excluir dados antigos de solicitação de aplicativo**: use esta tarefa para excluir solicitações de aplicativos antigas do banco de dados. Para obter mais informações sobre solicitações do aplicativo, consulte [Criar e implantar um aplicativo com o System Center Configuration Manager](/sccm/apps/get-started/create-and-deploy-an-application).  

-   Site da administração central: Não disponível
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir histórico antigo de download de cliente**: use essa tarefa para excluir os dados históricos sobre a fonte de download usada pelos clientes. As informações de fonte baixadas são usadas para preencher o [painel de Fontes de Dados do Cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).  
-  Site de administração central – indisponível
-  **Site primário** – habilitado
-  Site secundário - não disponível

**Excluir operações antigas de cliente**: use essa tarefa para excluir todos os dados antigos de operações de cliente do banco de dados do site. Isso inclui, por exemplo, dados de notificações do cliente antigas ou expiradas (como solicitações de download do computador ou políticas do usuário) e do Endpoint Protection (como solicitações de um usuário administrativo para os clientes executarem uma varredura ou baixar definições atualizadas).

-   **Site de administração central**: Habilitada    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir histórico antigo de presença de cliente**: use essa tarefa para excluir informações de histórico sobre o status online de clientes (gravadas pela notificação do cliente) que sejam mais antigas que a hora especificada. Para obter mais informações sobre notificações do cliente, veja [Como monitorar clientes no System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md).  

-   **Site de administração central**: Habilitada   
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir dados antigos de tráfego do Gateway de Gerenciamento de Nuvem**: use essa tarefa para excluir todos os dados antigos sobre o tráfego que passa pelo [Gateway de Gerenciamento de Nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway) do banco de dados do site. Por exemplo, isso inclui dados sobre o número de solicitações, total de bytes de solicitação, total de bytes de resposta, número de solicitações com falha e número máximo de solicitações simultâneas.  
- **Site de administração central** – habilitado
- **Site primário** – habilitado
- Site secundário - não disponível


**Excluir arquivos antigos coletados**: use esta tarefa para excluir informações obsoletas sobre arquivos coletados do banco de dados. Essa tarefa também exclui os arquivos coletados da estrutura de pasta do servidor do site no site selecionado. Por padrão, as cinco cópias mais recentes de arquivos coletados são armazenadas no servidor de sites no diretório **Inboxes\sinv.box\FileCol**. Para obter mais informações, consulte [Introdução ao inventário se software no System Center Configuration Manager](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).  

-   Site da administração central: Não disponível    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir dados antigos de associação de computador**: use esta tarefa para excluir dados antigos de associação do computador de implantação do sistema operacional do banco de dados. Essas informações são usadas como parte da conclusão das restaurações de estado do usuário. Para obter mais informações sobre associações de computador, consulte [Gerenciar estado do usuário no System Center Configuration Manager](../../../osd/get-started/manage-user-state.md).  

-   Site da administração central: Não disponível    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir dados antigos de detecção de exclusão**: use esta tarefa para excluir dados antigos do banco de dados que foi criado pelas Exibições de Extração. Por padrão, as Exibições de Extração estão desabilitadas. Só é possível habilitá-las usando o SDK do Configuration Manager. A menos que as Exibições de Extração sejam habilitadas, não há nenhum dado para esta tarefa excluir.  

-   **Site de administração central**: Habilitada    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir registro antigo de apagamento de dispositivo**: use esta tarefa para excluir dados antigos sobre ações de limpeza de dispositivo móvel do banco de dados. Para saber mais sobre como apagar dispositivos móveis, veja [Proteger seus dados com apagamento, bloqueio ou redefinição de senha remotos usando o System Center Configuration Manager](/sccm/mdm/deploy-use/wipe-lock-reset-devices).  

-   Site da administração central: Não disponível    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir dispositivos antigos gerenciados pelo conector do Exchange Server**: use essa tarefa para excluir dados antigos dos dispositivos móveis gerenciados usando o conector do Exchange Server. Esses dados são excluídos de acordo com o intervalo configurado na opção **Ignorar dispositivos móveis que estejam inativos por mais de () dias** na guia **Descoberta** das propriedades do conector do Exchange Server. Para obter mais informações, consulte [Gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

-   Site da administração central: Não disponível   
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir dados antigos de descoberta**: use esta tarefa para excluir dados antigos de descoberta do banco de dados. Esses dados podem incluir registros resultantes dos métodos de descoberta de pulsação, descoberta de rede e descoberta do Active Directory Domain Services (Sistema, Usuário e Grupo). Essa tarefa também removerá dispositivos antigos marcados como desativados. Quando essa tarefa é executada em um site, os dados associados a esse site são excluídos, e essas alterações são replicadas em outros sites. Para obter mais informações sobre Descoberta, consulte [Run discovery for System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md).  

-   Site da administração central: Não disponível    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir dados antigos de uso do ponto de distribuição**: use esta tarefa para excluir dados antigos do banco de dados para pontos de distribuição que foram armazenados além de um tempo especificado.  

-   **Site de administração central**: Habilitada    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir dados antigo de histórico de status de integridade do Endpoint Protection**: use esta tarefa para excluir informações de status antigas do Endpoint Protection do banco de dados. Para saber mais sobre as informações de status do Endpoint Protection, consulte [Como monitorar o Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md).  

-   Site da administração central: Não disponível    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir dispositivos registrados antigos**: começando com a atualização para a 1602, essa tarefa está desabilitada por padrão. Você pode usar esta tarefa para excluir do banco de dados os dados antigos sobre dispositivos móveis registrados que não relataram informações ao site por um tempo especificado.

Essa tarefa aplica-se a dispositivos registrados pelo Microsoft Intune (híbrido) ou registrados no gerenciamento de dispositivo móvel local do Configuration Manager. Para obter mais informações, consulte [Sistemas operacionais com suporte para clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#bkmk_OnpremOS).

-   Site da administração central: Não disponível    
-   **Site primário**: não ativado    
-   Site secundário: Não disponível  

**Excluir histórico antigo de inventário**: use esta tarefa para excluir dados de inventário do banco de dados, que foram armazenados além do tempo especificado. Para obter informações sobre o histórico de inventário, consulte [Como usar o Gerenciador de Recursos para ver o inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

-   Site da administração central: Não disponível    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir dados antigos de log**: use esta tarefa para excluir dados antigos de log que são usados para solução de problemas do banco de dados. Esses dados não estão relacionados às operações de componente do Configuration Manager.  

> [!IMPORTANT]  
> Por padrão, esta tarefa é executada diariamente em cada site. Em um site de administração central e sites primários, a tarefa exclui dados com mais de 30 dias. Ao usar o SQL Server Express em um site secundário, certifique-se que esta tarefa seja executada diariamente e exclua os dados que ficaram inativos por 7 dias.  

-   **Site de administração central**: Habilitada    
-   **Site primário**: Habilitada    
-   **Site secundário**: Habilitada  

**Excluir histórico antigo de tarefas de notificação**: use essa tarefa para excluir informações sobre tarefas de notificação de cliente do banco de dados do site quando ele não for atualizado durante um período especificado. Para saber mais sobre notificações do cliente, veja [Tarefas de implantação de cliente do System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md).  

-   Site da administração central: Não disponível    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir dados antigos de resumo de replicação**: use essa tarefa para excluir dados antigos de resumo de replicação do banco de dados do site quando ele não for atualizado durante um período determinado. Para obter mais informações, consulte a seção [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) no tópico [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) .  

-   **Site de administração central**: Habilitada    
-   **Site primário**: Habilitada    
-   **Site secundário**: Habilitada  

**Excluir registros de senha antigos**: use essa tarefa no site de nível superior da hierarquia para excluir dados antigos de redefinição de senha de dispositivos Android e Windows Phone. Os dados da Redefinição de Senha são criptografados, mas incluem o PIN de dispositivos. Por padrão, essa tarefa é habilitada e exclui dados com mais de um dia.  

-   **Site de administração central**: Habilitada    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir dados antigos de acompanhamento de replicação**: use essa tarefa para excluir dados antigos de replicação de banco de dados entre os sites do Configuration Manager do banco de dados. Quando você altera a configuração dessa tarefa de manutenção, a configuração se aplica a cada site aplicável na hierarquia. Para obter mais informações, consulte a seção [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) no tópico [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) .  

-   **Site de administração central**: Habilitada    
-   **Site primário**: Habilitada    
-   **Site secundário**: Habilitada  

**Excluir dados antigos de medição de software**: use esta tarefa para excluir dados antigos de medição de software do banco de dados, armazenados além do tempo especificado. Para obter mais informações, consulte [Medição de software no System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Site da administração central: Não disponível    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir dados antigos de resumo de medição de software**: use esta tarefa para excluir dados antigos de resumo de medição de software do banco de dados, armazenados além do tempo especificado. Para obter mais informações, consulte [Medição de software no System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Site da administração central: Não disponível    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir mensagens de status antigas**: use esta tarefa para excluir dados de mensagens antigas de status como configurado nas regras de filtro de status do banco de dados. Para saber mais, veja a seção “Monitorar o sistema de status do Configuration Manager” no tópico [Usar alertas e o sistema de status para o System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   **Site de administração central**: Habilitada    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir dados antigos de ameaça**: use esta tarefa para excluir dados de ameaça do banco de dados ao Endpoint Protection. armazenados além do tempo especificado. Para obter informações sobre o Endpoint Protection, consulte [Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

-   Site da administração central: Não disponível    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir computadores desconhecidos antigos**: use essa tarefa para excluir informações sobre computadores desconhecidos do banco de dados do site quando ele não for atualizado durante um período especificado. Para obter mais informações, consulte [Preparar implantações de computador desconhecido no System Center Configuration Manager](../../../osd/get-started/prepare-for-unknown-computer-deployments.md).  

-   Site da administração central: Não disponível    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir dados antigos de afinidade de dispositivo de usuário**: use esta tarefa para excluir dados antigos de afinidade de usuário do banco de dados. Para obter mais informações, consulte [Vincular usuários e dispositivos com a afinidade de dispositivo de usuário no System Center Configuration Manager](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

-   Site da administração central: Não disponível    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir registros de pacotes expirados registrados em massa do MDM**: use essa tarefa para excluir certificados de registro em massa antigos e os perfis correspondentes depois que o certificado de registro expirar. Para obter mais informações, consulte [Criar perfis de certificado](/sccm/protect/deploy-use/create-certificate-profiles).
-   **Site de administrações central**: Habilitada
-   **Site primário**: Habilitada
-   Site secundário: Não disponível

**Excluir dados inativos de descoberta de cliente**: use esta tarefa para excluir dados de descoberta para clientes inativos do banco de dados. Os clientes são marcados como inativos quando são sinalizados como obsoletos e por configurações feitas no status do cliente.

Esta tarefa só opera em recursos que são clientes do Configuration Manager. É diferente da tarefa **Excluir Dados Antigos de Descoberta**, que exclui qualquer registro de dados de descoberta antigo. Quando esta tarefa é executada em um site, remove os dados do banco de dados em todos os sites em uma hierarquia. Para obter mais informações, consulte [How to configure client status in System Center Configuration Manager](../../../core/clients/deploy/configure-client-status.md).  

> [!IMPORTANT]  
> Quando habilitada, configure essa tarefa para ser executada em intervalos superiores aos do agendamento de **Descoberta de Pulsação**. Isso permite que os clientes ativos enviem um registro de Descoberta de Pulsação para marcar o registro do cliente como ativo, de forma que a tarefa não o exclua.  

-   Site da administração central: Não disponível    
-   **Site primário**: não ativado    
-   Site secundário: Não disponível  

**Excluir alertas obsoletos**: use esta tarefa para excluir alertas obsoletos do banco de dados, armazenados além do tempo especificado. Para obter mais informações, consulte [Usar alertas e o sistema de status para o System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   **Site de administração central**: Habilitada    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir dados obsoletos de descoberta de cliente**: use esta tarefa para excluir registros obsoletos de cliente do banco de dados. Um registro que está marcado como obsoleto geralmente foi substituído por um novo registro para o mesmo cliente. O registro mais recente torna-se o registro atual do cliente. Para obter mais informações sobre Descoberta, consulte [Run discovery for System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md).  

> [!IMPORTANT]  
> Quando habilitada, configure essa tarefa para ser executada em intervalos superiores aos do agendamento de Descoberta de Pulsação. Isso permite que o cliente envie um registro de descoberta de pulsação que define o status obsoleto corretamente.  

-   Site da administração central: Não disponível    
-   **Site primário**: não ativado    
-   Site secundário: Não disponível  

**Excluir sub-redes e sites obsoletos de descoberta de floresta**: Use essa tarefa para excluir dados sobre sites, sub-redes e domínios do Active Directory que não foram descobertos pelo método de descoberta de floresta do Active Directory nos últimos 30 dias. Isso remove os dados de descoberta, mas não afeta os limites criados por meio desses dados de descoberta. Para obter mais informações, consulte [Executar descoberta para o System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md).  

-   **Site de administração central**: Habilitada    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Excluir registros de estado de implantação de cliente órfão**: use essa tarefa para limpar periodicamente a tabela que contém informações de estado de implantação do cliente. Essa tarefa limpará registros associados a dispositivos obsoletos ou encerrados.  
-   **Site de administração central**: Habilitada    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível

**Excluir revisões não usadas de aplicativo**: use esta tarefa para excluir revisões de aplicativos que não são mais referenciadas. Para mais informações, consulte [Como revisar e substituir aplicativos no System Center Configuration Manager](../../../apps/deploy-use/revise-and-supersede-applications.md).  

-   Site da administração central: Não disponível    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Avaliar membros da coleção**: configure a Avaliação de Associação da Coleção como um componente do site. Para obter mais informações sobre os componentes do site consulte [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

-   Site da administração central: Não disponível    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Monitorar chaves**: use essa tarefa para monitorar a integridade das chaves primárias do banco de dados do Configuration Manager. Uma chave primária é uma coluna ou combinação de colunas que identifica exclusivamente uma linha e a distingue de qualquer outra linha em uma tabela de banco de dados do Microsoft SQL Server.  

-   **Site de administração central**: Habilitada    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Recompilar índices**: use essa tarefa para recompilar os índices de banco de dados do Configuration Manager. Um índice é uma estrutura de banco de dados criada em uma tabela de banco de dados para acelerar a recuperação de dados. Por exemplo, pesquisar uma coluna indexada muitas vezes é mais rápido do que pesquisar uma coluna que não está indexada.

Para melhorar o desempenho, os índices do banco de dados do Configuration Manager são frequentemente atualizados para permanecerem sincronizados com os dados que são armazenados no banco de dados. Essa tarefa cria índices em colunas de banco de dados que são pelo menos 50 por cento exclusivas, elimina índices em colunas que são exclusivas em menos 50 por cento e reconstrói todos os índices existentes que atendem aos critérios de exclusividade dos dados.  

-   **Site de administração central**: não ativado    
-   **Site primário**: não ativado    
-   **Site secundário**: não ativado  

**Resumir dados de software instalado**: use essa tarefa para resumir os dados do software instalado de vários registros em um registro geral. O resumo de dados pode compactar a quantidade de dados armazenados no banco de dados do Configuration Manager. Para obter mais informações, consulte [Introdução ao inventário se software no System Center Configuration Manager](../../clients/manage/inventory/introduction-to-software-inventory.md).  

-   Site da administração central: Não disponível    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Resumir dados de uso do arquivo de medição de software**: use essa tarefa para resumir os dados de vários registros do software medindo o uso do arquivo em um registro geral. O resumo de dados pode compactar a quantidade de dados armazenados no banco de dados do Configuration Manager.

É possível usar esta tarefa com a tarefa **Resumir Dados de Uso Mensal de Medição de Software** para resumir dados de medição de software e para conservar o espaço em disco no banco de dados do Configuration Manager. Para obter mais informações, consulte [Medição de software no System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Site da administração central: Não disponível    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Resumir dados de uso mensal de medição de software**: use essa tarefa para resumir os dados de vários registros de uso mensal de medição de software em um registro geral. O resumo de dados pode compactar a quantidade de dados armazenados no banco de dados do Configuration Manager.

É possível usar esta tarefa com a tarefa **Resumir Dados de Uso de Arquivo de Medição de Software** para resumir dados de medição de software e para conservar o espaço no banco de dados do Configuration Manager. Para obter mais informações, consulte [Medição de software no System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Site da administração central: Não disponível    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Atualizar o direcionamento disponível do aplicativo**: use essa tarefa para que o Configuration Manager recalcule o mapeamento das implantações de aplicativo e de política para recursos em coleções. Ao implantar políticas ou aplicativos em uma coleção, o Configuration Manager cria um mapeamento inicial entre os objetos implantados e os membros da coleção.

Esses mapeamentos são armazenados em uma tabela para referência rápida. Quando uma associação de coleções é alterada, esses mapeamentos armazenados são atualizados para que reflitam essas mudanças. No entanto, é possível que esses mapeamentos fiquem fora de sincronia. Por exemplo, se o site não processar corretamente um arquivo de notificação, essa mudança pode não ser refletida em uma alteração nos mapeamentos. Essa tarefa atualiza esse mapeamento com base na associação de coleção atual.  

-   Site da administração central: Não disponível    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  

**Atualizar tabelas do Catálogo de Aplicativos**: use essa tarefa para sincronizar o cache de banco de dados do site de Catálogo do Aplicativo com as informações mais recentes do aplicativo. Quando você altera a configuração dessa tarefa de manutenção, a configuração se aplica a todo site primário na hierarquia.  

-   Site da administração central: Não disponível    
-   **Site primário**: Habilitada    
-   Site secundário: Não disponível  
