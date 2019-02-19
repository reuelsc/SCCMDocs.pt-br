---
title: Migrar dados
titleSuffix: Configuration Manager
description: Saiba como transferir dados de uma hierarquia de origem para uma hierarquia de destino do Configuration Manager.
ms.date: 11/05/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f6f0b7f67c1b25fc28f82956a43f9a503ad3d190
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123494"
---
# <a name="migrate-data-between-hierarchies-in-configuration-manager"></a>Migrar dados entre hierarquias no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use a migração para transferir dados de uma hierarquia de origem compatível com uma hierarquia de destino do Configuration Manager (branch atual). Ao migrar dados de uma hierarquia de origem:  

- Você acessa dados dos bancos de dados de site na infraestrutura de origem e, em seguida, transfere esses dados para seu ambiente atual.  

- A migração não altera os dados na hierarquia de origem. Em vez disso, ela descobre os dados e armazena uma cópia no banco de dados da hierarquia de destino.  

Considere os seguintes pontos ao planejar sua estratégia de migração:  

- Você pode migrar uma infraestrutura existente do Configuration Manager 2007 SP2 para o Configuration Manager (branch atual).  

- Você pode migrar alguns ou todos os dados com suporte do site de origem.  

- Você pode migrar os dados de um único site de origem para diversos sites na hierarquia de destino.  

- Você pode mover dados de vários sites de origem para um único site na hierarquia de destino.  


O vídeo a seguir discute e demonstra dois [cenários de migração](#BKMK_MigrationScenarios) comuns. Ele também inclui opções para incluir o Microsoft Azure em planos de migração.
> [!VIDEO https://www.youtube.com/embed/6_0EwW-5b4E]



##  <a name="BKMK_MigrationConcepts"></a> Conceitos  

 O Configuration Manager usa os seguintes conceitos e termos durante a migração.  

#### <a name="source-hierarchy"></a>Hierarquia de origem
Uma hierarquia que executa uma versão com suporte do Configuration Manager e tem dados que você deseja migrar. Quando você configura a migração, identifica a hierarquia de origem ao especificar o site de nível superior de uma hierarquia de origem. Após especificar uma hierarquia de origem, o site de nível superior da hierarquia de destino reúne dados do banco de dados do site de origem designado para identificar os dados que você pode migrar. 

Para obter mais informações, confira [Hierarquias de origem](/sccm/core/migration/planning-a-source-hierarchy-strategy#BKMK_Source_Hierarchies).

#### <a name="source-sites"></a>Sites de origem
Os sites na hierarquia de origem que possuem dados que você pode migrar para a sua hierarquia de destino. 

Para obter mais informações, confira [Sites de origem](/sccm/core/migration/planning-a-source-hierarchy-strategy#BKMK_Source_Sites).

#### <a name="destination-hierarchy"></a>Hierarquia de destino
Uma hierarquia do Configuration Manager (branch atual) em que é executada a migração para importar dados de uma hierarquia de origem.

#### <a name="data-gathering"></a>Coleta de dados
O processo contínuo de identificar as informações em uma hierarquia de origem que podem ser migradas para a hierarquia de destino. O Configuration Manager verifica a hierarquia de origem em um agendamento. Esse processo identifica quaisquer alterações às informações na hierarquia de origem que você migrou anteriormente e que você pode desejar atualizar na hierarquia de destino.

Para obter mais informações, confira [Data warehouse](/sccm/core/migration/planning-a-source-hierarchy-strategy#BKMK_Data_Gathering).

#### <a name="migration-jobs"></a>Trabalhos de migração
O processo de configurar os objetos específicos para migrar, e então gerenciar a migração desses objetos para a hierarquia de destino.

Para obter mais informações, confira [Planejando uma estratégia de trabalho de migração](/sccm/core/migration/planning-a-migration-job-strategy).

#### <a name="client-migration"></a>Migração do cliente
O processo de transferência de informações que clientes usam do banco de dados do site de origem ao banco de dados da hierarquia de destino. Essa migração dos dados é seguida por uma atualização do software cliente nos dispositivos com a versão de software cliente da hierarquia de destino.

Para obter mais informações, confira [Planejando uma estratégia de migração de cliente](/sccm/core/migration/planning-a-client-migration-strategy).

#### <a name="shared-distribution-points"></a>Pontos de distribuição compartilhados
Os pontos de distribuição da hierarquia de origem que o Configuration Manager compartilha com a hierarquia de destino durante o período de migração.

Durante o período de migração, os clientes atribuídos aos sites na hierarquia de destino podem obter conteúdo dos pontos de distribuição compartilhados.

Para obter mais informações, confira [Compartilhar pontos de distribuição entre hierarquias de origem e destino](/sccm/core/migration/planning-a-content-deployment-migration-strategy#About_Shared_DPs_in_Migration).

#### <a name="monitoring-migration"></a>Monitorando a migração
O processo de monitoramento de atividades de migração. Você monitora o progresso e o sucesso da migração no nó **Migração** no workspace **Administração**.

Para mais informações, confira [Planejamento para monitorar a atividade de migração](/sccm/core/migration/planning-to-monitor-migration-activity).

#### <a name="stop-gathering-data"></a>Parar Coleta de Dados
O processo de interromper a coleta de dados de sites de origem. Quando você não tiver mais dados para migrar de uma hierarquia de origem ou se desejar pausar as atividades relacionadas à migração, poderá configurar a hierarquia de destino para interromper a coleta de dados da hierarquia de origem.

Para obter mais informações, confira [Data warehouse](/sccm/core/migration/planning-a-source-hierarchy-strategy#BKMK_Data_Gathering).

#### <a name="clean-up-migration-data"></a>Limpar dados de migração
O processo de concluir a migração de uma hierarquia de origem removendo as informações sobre a migração do banco de dados das hierarquias de destino.

Para mais informações, confira [Planejando para concluir a migração](/sccm/core/migration/planning-to-complete-migration).



## <a name="typical-workflow"></a>Fluxo de trabalho típico  

Para configurar um fluxo de trabalho para migração:

1.  Especifique uma hierarquia de origem com suporte.  

2.  Configure a coleta de dados. A coleta de dados habilita o Configuration Manager a coletar informações sobre dados que podem ser migrados da hierarquia de origem.  

     O Configuration Manager repete automaticamente o processo para coletar dados em um agendamento simples até que você interrompa o processo de coleta de dados. Por padrão, o processo de coleta de dados é repetido a cada quatro horas para que o Configuration Manager possa identificar alterações nos dados na hierarquia de origem. A coleta de dados também é necessária para compartilhar os pontos de distribuição.  

3.  Crie trabalhos de migração para migrar dados entre a hierarquia de origem e a de destino.  

4.  Você pode interromper o processo de coleta de dados a qualquer momento usando a ação **Parar Coleta de Dados**. Quando você para a coleta de dados, o Configuration Manager não identifica mais as alterações nos dados na hierarquia de origem e não pode mais compartilhar pontos de distribuição. Normalmente, você usa essa ação quando não pretende mais migrar dados ou compartilhar pontos de distribuição da hierarquia de origem.  

5.  Opcionalmente, após a coleta de dados ter sido parada em todos os sites da hierarquia de origem, é possível limpar os dados de migração usando a ação **Limpar Dados de Migração**. Essa ação exclui os dados históricos sobre a migração de uma hierarquia de origem do banco de dados da hierarquia de destino.  

Após você migrar os dados e não precisar mais da hierarquia de origem para gerenciar dispositivos em seu ambiente, você pode encerrar a infraestrutura e a hierarquia de origem.  



##  <a name="BKMK_MigrationScenarios"></a> Cenários  

 O Configuration Manager é compatível com os seguintes cenários de migração:
- [Migração de hierarquias do Configuration Manager 2007](#bkmk_2007)  
- [Migração do Configuration Manager 2012 ou outra hierarquia do Configuration Manager](#bkmk_2012)

> [!NOTE]  
>  A expansão de uma hierarquia que tem um site autônomo para uma hierarquia que tem um site de administração central não é categorizada como uma migração. Para obter mais informações sobre a expansão da hierarquia, confira [Expandir um site primário autônomo](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_expand).  


### <a name="bkmk_2007"></a> Migração de hierarquias do Configuration Manager 2007  

 Quando você usa migração para migrar dados do Configuration Manager 2007, pode manter seu investimento na infraestrutura de site existente e obter os seguintes benefícios:  

#### <a name="site-database-improvements"></a>Aprimoramentos de banco de dados do site
O banco de dados do Configuration Manager (branch atual) é compatível com o Unicode completo.

#### <a name="database-replication-between-sites"></a>Replicação de banco de dados entre sites
A replicação no Configuration Manager (branch atual) se baseia no Microsoft SQL Server. Esse comportamento melhora o desempenho da transferência de dados de site para site.

#### <a name="user-centric-management"></a>Gerenciamento centrado no usuário
Os usuários são o foco de tarefas de gerenciamento no Configuration Manager (branch atual). Por exemplo, será possível distribuir software a um usuário mesmo se você não souber o nome do dispositivo para esse usuário. Além disso, o Configuration Manager proporciona aos usuários muito mais controle sobre qual software está instalado em seus dispositivos e quando esse software é instalado.

#### <a name="hierarchy-simplification"></a>Simplificação de hierarquia
O Configuration Manager (branch atual) permite criar uma hierarquia de site mais simples. Esse aprimoramento é devido à introdução do tipo de site de administração central e às alterações no comportamento dos sites primários e secundários. O Configuration Manager (branch atual) usa menos largura de banda de rede e requer menos servidores que as versões anteriores.

#### <a name="role-based-administration"></a>Administração baseada em funções
Esse modelo de segurança central no Configuration Manager (branch atual) oferece segurança por toda a hierarquia e gerenciamento que corresponde aos seus requisitos administrativos e empresariais.

> [!NOTE]  
>  Devido às alterações de design introduzidas no System Center 2012 Configuration Manager, não é possível atualizar o Configuration Manager 2007 para o Configuration Manager (branch atual). A atualização em vigor é compatível desde o System Center 2012 Configuration Manager até o Configuration Manager (branch atual).  


### <a name="bkmk_2012"></a> Migração do Configuration Manager 2012 ou outra hierarquia do Configuration Manager  
 O processo de migração de dados de uma hierarquia do System Center 2012 Configuration Manager ou do Configuration Manager é o mesmo. Esse processo inclui a migração de dados de várias hierarquias de origem para uma única hierarquia de destino. Você pode usar este processo quando sua empresa adquire recursos adicionais que já são gerenciados pelo Configuration Manager. Além disso, é possível migrar dados de um ambiente de teste do Configuration Manager para seu ambiente de produção. Esse processo permite manter seu investimento no ambiente de teste do Configuration Manager.  



## <a name="see-also"></a>Consulte também  

-   [Planejando a migração para o Configuration Manager](/sccm/core/migration/planning-for-migration)  

-   [Configurando hierarquias de origem e sites de origem para migração](/sccm/core/migration/configuring-source-hierarchies-and-source-sites-for-migration)  

-   [Operações de migração](/sccm/core/migration/operations-for-migration)  

-   [Segurança e privacidade da migração](/sccm/core/migration/security-and-privacy-for-migration)  

-   [Começar a usar o Configuration Manager](/sccm/core/servers/deploy/start-using)
