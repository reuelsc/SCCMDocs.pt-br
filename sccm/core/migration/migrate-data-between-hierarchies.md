---
title: Migrar dados
titleSuffix: Configuration Manager
description: Saiba como transferir dados de uma hierarquia de origem para uma hierarquia de destino do System Center Configuration Manager.
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d832e820421784ce33df880463632050741eedd7
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="migrate-data-between-hierarchies-in-system-center-configuration-manager"></a>Migrar dados entre hierarquias no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use a migração para transferir dados de uma hierarquia de origem com suporte para uma hierarquia de destino do System Center Configuration Manager.  Ao migrar dados de uma hierarquia de origem:  

-   Você acessa dados dos bancos de dados de site identificados na infraestrutura de origem e, em seguida, transfere esses dados para seu ambiente atual.  

-   A migração não altera os dados na hierarquia de origem, mas, em vez disso, descobre os dados e armazena uma cópia no banco de dados da hierarquia de destino.  

Considere o seguinte ao planejar sua estratégia de migração:  

-   Você pode migrar uma infraestrutura existente do Configuration Manager 2007 SP2 para o System Center Configuration Manager.  

-   Você pode migrar alguns ou todos os dados com suporte do site de origem.  

-   Você pode migrar os dados de um único site de origem para diversos sites na hierarquia de destino.  

-   Você pode mover dados de vários sites de origem para um único site na hierarquia de destino.  

##  <a name="BKMK_MigrationConcepts"></a> Conceitos de migração  
 Você pode encontrar os seguintes conceitos e termos ao usar a migração.  

|Conceito ou termo|Mais informações|  
|---------------------|----------------------|  
|Hierarquia de origem|Uma hierarquia que executa uma versão com suporte do Configuration Manager e tem dados que você deseja migrar. Quando você configura a migração, identifica a hierarquia de origem ao especificar o site de nível superior de uma hierarquia de origem. Após especificar uma hierarquia de origem, o site de nível superior da hierarquia de destino reúne dados do banco de dados do site de origem designado para identificar os dados que você pode migrar.<br /><br /> Para obter mais informações, consulte [Hierarquias de origem](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies) em [Planejamento de uma estratégia de hierarquia de origem no System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Sites de origem|Os sites na hierarquia de origem que possuem dados que você pode migrar para a sua hierarquia de destino.<br /><br /> Para obter mais informações, consulte [Sites de origem](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites) em [Planejamento de uma estratégia de hierarquia de origem no System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Hierarquia de destino|Uma hierarquia do System Center Configuration Manager em que é executada a migração para importar dados de uma hierarquia de origem.|  
|Coleta de dados|O processo contínuo de identificar as informações em uma hierarquia de origem que podem ser migradas para a hierarquia de destino. O Configuration Manager verifica a hierarquia de origem em um agendamento para identificar alterações às informações na hierarquia de origem que você migrou anteriormente e que você pode desejar atualizar na hierarquia de destino.<br /><br /> Para obter mais informações, consulte [Coleta de dados](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering) em [Planejamento de uma estratégia de hierarquia de origem no System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Trabalhos de migração|O processo de configurar os objetos específicos para migrar, e então gerenciar a migração desses objetos para a hierarquia de destino.<br /><br /> Para mais informações, consulte [Planejamento de uma estratégia de trabalho de migração no System Center Configuration Manager](../../core/migration/planning-a-migration-job-strategy.md)|  
|Migração do cliente|O processo de transferência de informações que clientes usam do banco de dados do site de origem ao banco de dados da hierarquia de destino. A migração dos dados é seguida por uma atualização do software do cliente nos dispositivos com a versão de software do cliente da hierarquia de destino.<br /><br /> Para obter mais informações, consulte [Planejamento de uma estratégia de migração de cliente no System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).|  
|Pontos de distribuição compartilhados|Os pontos de distribuição da hierarquia de origem que são compartilhados com a hierarquia de destino durante o período de migração.<br /><br /> Durante o período de migração, os clientes atribuídos aos sites na hierarquia de destino podem obter conteúdo dos pontos de distribuição compartilhados.<br /><br /> Para obter mais informações, veja [Compartilhar pontos de distribuição entre hierarquias de origem e de destino](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) em [Planejamento de uma estratégia de migração de implantação de conteúdo no System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).|  
|Monitorando a migração|O processo de monitoramento de atividades de migração. Você monitora o progresso e o sucesso da migração no nó **Migração** no espaço de trabalho **Administração**.<br /><br /> Para mais informações, consulte [Planejamento para monitorar a atividade de migração no System Center Configuration Manager](../../core/migration/planning-to-monitor-migration-activity.md).|  
|Parar Coleta de Dados|O processo de interromper a coleta de dados de sites de origem. Quando você não tiver mais dados para migrar de uma hierarquia de origem ou se desejar pausar as atividades relacionadas à migração, poderá configurar a hierarquia de destino para interromper a coleta de dados da hierarquia de origem.<br /><br /> Para obter mais informações, consulte [Coleta de dados](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering) em [Planejamento de uma estratégia de hierarquia de origem no System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Limpar dados de migração|O processo de concluir a migração de uma hierarquia de origem removendo as informações sobre a migração do banco de dados das hierarquias de destino.<br /><br /> Para obter mais informações, consulte [Planejamento da conclusão da migração no System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md).|  

## <a name="typical-workflow-for-migration"></a>Fluxo de trabalho típico para migração  
Para configurar um fluxo de trabalho para migração:

1.  Especifique uma hierarquia de origem com suporte.  

2.  Configure a coleta de dados. A coleta de dados habilita o Configuration Manager a coletar informações sobre dados que podem ser migrados da hierarquia de origem.  

     O Configuration Manager repete automaticamente o processo para coletar dados em um agendamento simples até que você interrompa o processo de coleta de dados. Por padrão, o processo de coleta de dados é repetido a cada quatro horas para que o Configuration Manager possa identificar alterações nos dados na hierarquia de origem que você talvez deseje migrar. A coleta de dados também é necessária para compartilhar pontos de distribuição da hierarquia de origem para a hierarquia de destino.  

3.  Crie trabalhos de migração para migrar dados entre a hierarquia de origem e a de destino.  

4.  Você pode interromper o processo de coleta de dados a qualquer momento usando o comando **Parar Coleta de Dados** . Quando você para a coleta de dados, o Configuration Manager não identifica mais as alterações nos dados na hierarquia de origem e não pode mais compartilhar pontos de distribuição entre a hierarquia de origem e a de destino. Normalmente, você usa essa ação quando não pretende mais migrar dados ou compartilhar pontos de distribuição da hierarquia de origem.  

5.  Opcionalmente, após a coleta de dados ter sido parada em todos os sites da hierarquia de origem, é possível limpar os dados de migração usando o comando **Limpar Dados de Migração** . Esse comando exclui os dados históricos sobre a migração de uma hierarquia de origem do banco de dados da hierarquia de destino.  

Depois de migrar dados de uma hierarquia de origem do Configuration Manager que não usará mais para gerenciar seu ambiente, você pode encerrar essa hierarquia de origem e essa infraestrutura.  

##  <a name="BKMK_MigrationScenarios"></a> Cenários de migração  
 O Configuration Manager dá suporte aos seguintes cenários de migração.  

> [!NOTE]  
>  A expansão de uma hierarquia que tem um site autônomo para uma hierarquia que tem um site de administração central não é categorizada como uma migração. Para obter informações sobre expansão de hierarquia, confira [Expandir um site primário autônomo](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand) em [Usar o Assistente de Instalação para instalar sites](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  

### <a name="migration-from-configuration-manager-2007-hierarchies"></a>Migração de hierarquias do Gerenciador de Configurações 2007  
 Quando você usa migração para migrar dados do Configuration Manager 2007, pode manter seu investimento na infraestrutura de site existente e obter os seguintes benefícios:  

|Benefício|Mais informações|  
|-------------|----------------------|  
|Aprimoramentos de banco de dados do site|O banco de dados do System Center Configuration Manager dá suporte a Unicode completo.|  
|Replicação de banco de dados entre sites|A replicação no System Center Configuration Manager se baseia no Microsoft SQL Server. Isso melhora o desempenho da transferência de dados de site para site.|  
|Gerenciamento centrado no usuário|Os usuários são o foco de tarefas de gerenciamento no System Center Configuration Manager. Por exemplo, será possível distribuir software a um usuário mesmo se você não souber o nome do dispositivo para esse usuário. Além disso, o System Center Configuration Manager proporciona aos usuários muito mais controle sobre qual software está instalado em seus dispositivos e quando esse software é instalado.|  
|Simplificação de hierarquia|No System Center Configuration Manager, o tipo de site de administração central e as alterações no comportamento dos sites primário e secundário permitem que você crie uma hierarquia de site muito mais simples, que utiliza menos largura de banda da rede e requer menos servidores.|  
|Administração baseada em funções|Esse modelo de segurança central no System Center Configuration Manager oferece segurança por toda a hierarquia e gerenciamento que corresponde aos seus requisitos administrativos e de negócios.|  

> [!NOTE]  
>  Devido às alterações de design introduzidas no System Center 2012 Configuration Manager, não é possível atualizar a infraestrutura do Configuration Manager 2007 para o System Center Configuration Manager. A atualização em vigor tem suporte desde o System Center 2012 Configuration Manager até o System Center Configuration Manager.  

### <a name="migration-from-configuration-manager-2012-or-another-system-center-configuration-manager-hierarchy"></a>Migração do Configuration Manager 2012 ou outra hierarquia do System Center Configuration Manager  
 O processo de migração de dados de uma hierarquia do System Center 2012 Configuration Manager ou do System Center Configuration Manager é o mesmo. Isso inclui migrar dados de várias hierarquias de origem para uma única hierarquia de destino, como quando sua empresa adquire recursos adicionais que já são gerenciados pelo Configuration Manager. Além disso, é possível migrar dados de um ambiente de teste do Configuration Manager para seu ambiente de produção. Isso permite manter seu investimento no ambiente de teste do Configuration Manager.  

## <a name="additional-topics-for-migration"></a>Tópicos adicionais para migração:  

-   [Planejamento para a migração para o System Center Configuration Manager](../../core/migration/planning-for-migration.md)  

-   [Configuração de hierarquias de origem e sites de origem para migração para o System Center Configuration Manager](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [Operações de migração para o System Center Configuration Manager](../../core/migration/operations-for-migration.md)  

-   [Segurança e privacidade da migração para o System Center Configuration Manager](../../core/migration/security-and-privacy-for-migration.md)  

## <a name="see-also"></a>Consulte também  
 [Começar a usar o System Center Configuration Manager](../../core/servers/deploy/start-using.md)
