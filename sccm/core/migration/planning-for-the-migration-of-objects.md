---
title: Migrar objetos | System Center Configuration Manager
description: "Saiba como planejar a migração de objetos entre hierarquias em um ambiente do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 066caf00-e419-4efb-93d3-ba4ba878297c
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 243b1eeac2536e3e63e9f8cbe132d36ea2aba39a


---
# <a name="planning-for-the-migration-of-configuration-manager-objects-to-system-center-configuration-manager"></a>Planejamento da migração de objetos do Configuration Manager para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Com o System Center Configuration Manager, é possível migrar vários objetos diferentes associados a diferentes recursos encontrados em um site de origem. Use as seções a seguir para ajudá-lo a planejar a migração de objetos entre hierarquias.  

-   [Planejando a migração de atualizações de software](#Plan_migrate_Software_updates)  

-   [Planejando a migração de conteúdo](#Plan_Migrate_content)  

-   [Planejando a migração de coleções](#BKMK_MigrateCollections)  

-   [Planejando a migração de implantações de sistema operacional](#Plan_migrate_OSD)  

-   [Planejando a migração do gerenciamento de configuração desejado](#Plan_Migrate_Compliance_settings)  

-   [Planejando a migração de limites](#Plan_migrate_Boundaries)  

-   [Planejando a migração de relatórios](#Plan_Migrate_reports)  

-   [Planejando a migração de pastas organizacionais e de pesquisa](#Plan_Migrate_Org_Folders)  

-   [Planejando a migração de personalizações do Asset Intelligence](#Plan_Migrate_AI)  

-   [Planejando a migração de personalizações de regras de medição de software](#Plan_Migrate_SWM_Rules)  

##  <a name="a-nameplanmigratesoftwareupdatesa-planning-to-migrate-software-updates"></a><a name="Plan_migrate_Software_updates"></a> Planejando a migração de atualizações de software  
 É possível migrar objetos de atualização de software, como os pacotes de atualização de software e implantações de atualização de software.  

 Para migrar com êxito os objetos de atualização de software, é necessário primeiro configurar sua hierarquia de destino com configurações que correspondem ao ambiente da hierarquia de origem. Isso requer as seguintes ações:  

-   Implantar um ponto de atualização de software ativo na hierarquia de destino.  

-   Configurar o catálogo de produtos e idiomas para corresponder à configuração da hierarquia de origem.  

-   Sincronizar o ponto de atualização de software na hierarquia do destino com um WSUS (Windows Server Update Services).  

Ao migrar as atualizações de software, considere o seguinte:  

-   A migração dos objetos de atualização de software pode falhar quando você não sincroniza as informações na hierarquia de destino para corresponder à hierarquia de origem.  

    > [!WARNING]  
    >  Não há suporte para usar a ferramenta WSUSutil para sincronizar dados entre a hierarquia de origem e destino.  

-   Você não pode migrar as atualizações personalizadas que são publicadas usando o System Center Updates Publisher. Em vez disso, as atualizações personalizadas devem ser republicadas na hierarquia de destino.  

Quando você migra de uma hierarquia de origem do Configuration Manager 2007, o processo de migração modifica alguns objetos de atualização de software para o formato usado na hierarquia de destino. Use a tabela a seguir para planejar a migração dos objetos de atualização de software do Configuration Manager 2007.  

|Objeto do Configuration Manager 2007|Nome do objeto após a migração|  
|-----------------------------------|---------------------------------|  
|Listas de atualizações de software|As listas de atualizações de software são convertidas em grupos de atualização de software.|  
|Implantações de atualização de software|As implantações de atualização de software são convertidas em implantações e grupos de atualizações.<br /><br /> Após migrar uma implantação de atualização de software do Configuration Manager 2007, você precisará habilitá-la na hierarquia de destino para implantá-la.|  
|Pacotes de atualizações de software|Os pacotes de atualizações de software permanecem como pacotes de atualizações de software.|  
|Modelos de atualizações de software|Os modelos de atualizações de software permanecem como modelos de atualizações de software.<br /><br /> O valor de **Duração** nos modelos de implantação do Configuration Manager 2007 não é migrado.|  

Quando você migra objetos de uma hierarquia de origem do System Center 2012 Configuration Manager ou do System Center Configuration Manager, os objetos de atualizações de software não são modificados.  

##  <a name="a-nameplanmigratecontenta-planning-to-migrate-content"></a><a name="Plan_Migrate_content"></a> Planejando a migração de conteúdo  
 É possível migrar o conteúdo de uma hierarquia de origem com suporte para a hierarquia de destino. Para uma hierarquia de origem do Configuration Manager 2007, esse conteúdo inclui programas e pacotes de distribuição de software e aplicativos virtuais, como o Microsoft Application Virtualization (App-V). Para hierarquias de origem do System Center 2012 Configuration Manager e do System Center Configuration Manager, esse conteúdo inclui aplicativos e aplicativos virtuais do App-V. Ao migrar o conteúdo entre hierarquias, são os arquivos de origem compactados que migram para a hierarquia de destino.  

### <a name="packages-and-programs"></a>Pacotes e programas  
 Quando você migrar pacotes e programas, eles não foram modificados pela migração. No entanto, para migrá-los, é necessário configurar cada pacote para usar um caminho UNC (convenção de nomenclatura universal) para seu local de arquivo de origem. Como parte da configuração para migrar pacotes e programas, é necessário atribuir um site na hierarquia de destino para gerenciar esse conteúdo. Esse conteúdo não é migrado de um site atribuído, mas após a migração, o site atribuído acessa o local do arquivo de origem original usando o mapeamento UNC.  

 Após migrar um pacote ou programa para a hierarquia de destino e enquanto a migração da hierarquia de origem permanece ativa, é possível tornar o conteúdo disponível para clientes nessa hierarquia usando um ponto de distribuição compartilhado. Para usar um ponto de distribuição compartilhado, o conteúdo deverá permanecer acessível no ponto de distribuição do site de origem. Para obter informações sobre pontos de distribuição compartilhados, consulte a seção [Share distribution points between source and destination hierarchies](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) no tópico [Planning a content deployment migration strategy in System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md) .  

 Para o conteúdo que foi migrado, se a versão do conteúdo for alterada na hierarquia de origem ou de destino, os clientes não poderão mais acessar o conteúdo do ponto de distribuição compartilhado na hierarquia de destino. Neste cenário, é necessário migrar o conteúdo novamente para restaurar uma versão consistente do pacote entre as hierarquias de origem e de destino. Essas informações são sincronizadas durante o ciclo de coleta de dados.  

> [!TIP]  
>  Para cada pacote que você migrar, atualize o pacote na hierarquia de destino. Essa ação pode evitar problemas com a implantação do pacote nos pontos de distribuição na hierarquia de destino. No entanto, quando você atualiza um pacote no ponto de distribuição na hierarquia de destino, os clientes nessa hierarquia não poderão mais adquirir esse pacote de um ponto de distribuição compartilhado. Para atualizar um pacote na hierarquia de destino, no console do Configuration Manager, navegue até a Biblioteca de Software, clique com o botão direito do mouse no pacote e selecione **Atualizar Pontos de Distribuição**. Execute essa ação para cada pacote que você migrou.  

> [!TIP]  
>  Você pode usar o Package Conversion Manager do Microsoft System Center Configuration Manager para converter pacotes e programas em aplicativos do System Center Configuration Manager. Baixe o Package Conversion Manager do site [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=212950) . Para obter mais informações, confira [Configuration Manager Package Conversion Manager](http://go.microsoft.com/fwlink/p/?LinkId=247245).  

### <a name="virtual-applications"></a>Aplicativos virtuais  
Quando você migra pacotes do App-V de um site do Configuration Manager 2007 com suporte, o processo de migração os converte em aplicativos na hierarquia de destino. Além disso, com base nos anúncios existentes do pacote do App-V, os seguintes tipos de implantação são criados na hierarquia de destino:  

-   Se não há nenhum anúncio, cria-se um tipo de implantação que usa as configurações de tipo de implantação padrão.  

-   Se houver um anúncio, será criado um tipo de implantação que usa as mesmas configurações que o anúncio do Configuration Manager 2007.  

-   Se houver vários anúncios, será criado um tipo de implantação para cada anúncio do Configuration Manager 2007, usando as configurações do anúncio em questão.  

> [!IMPORTANT]  
>  Se você migrar um App-V do Configuration Manager 2007 migrado anteriormente, a migração falhará porque pacotes de aplicativos virtuais não dão suporte ao comportamento de substituição de migração. Nesse cenário, é necessário excluir o pacote de aplicativos virtuais migrado da hierarquia de destino e criar um novo trabalho de migração para migrar o aplicativo virtual.  

> [!NOTE]  
>  Feita a migração de um pacote do App-V, é possível usar o Assistente para Atualizar Conteúdo para alterar o caminho de origem para os tipos de implantação do App-V. Para obter informações sobre como atualizar o conteúdo de um tipo de implantação, consulte a seção *Como gerenciar tipos de implantação* no tópico [Tarefas de gerenciamento para aplicativos do System Center Configuration Manager](../../apps/deploy-use/management-tasks-applications.md).  

Ao migrar de uma hierarquia de origem do System Center 2012 Configuration Manager ou do System Center Configuration Manager, além de aplicativos e tipos de implantação do App-V, é possível migrar objetos para o ambiente virtual do App-V. Para obter mais informações sobre ambientes do App-V, consulte [Implantando aplicativos virtuais do App-V com o System Center Configuration Manager](../../apps/get-started/deploying-app-v-virtual-applications.md).  

### <a name="advertisements"></a>Anúncios  
É possível migrar anúncios de um site de origem do Configuration Manager 2007 com suporte para a hierarquia de destino usando a migração baseada em coleção. Ao atualizar um cliente, ele retém o histórico de anúncios executados anteriormente para evitar que o cliente execute novamente os anúncios migrados.  

> [!NOTE]  
>  Não é possível migrar anúncios para pacotes virtuais. Essa é uma exceção para a migração de anúncios.  

### <a name="applications"></a>Aplicativos  
 É possível migrar aplicativos de uma hierarquia de origem do System Center 2012 Configuration Manager ou do System Center Configuration Manager com suporte para uma hierarquia de destino. Se você reatribuir um cliente da hierarquia de origem para a hierarquia de destino, o cliente retém o histórico de aplicativos instalados anteriormente para evitar que o cliente execute novamente o aplicativo migrado.  

##  <a name="a-namebkmkmigratecollectionsa-planning-to-migrate-collections"></a><a name="BKMK_MigrateCollections"></a> Planejando a migração de coleções  
 É possível migrar os critérios das coleções de uma hierarquia de origem do System Center 2012 Configuration Manager ou do System Center Configuration Manager com suporte. Para isso, use um trabalho de migração com base em objeto. Ao migrar uma coleção, você migra as regras para a coleção e não as informações sobre os membros da coleção e nem informações ou objetos relacionados a eles.  

 Não há suporte para a migração do objeto de coleção quando você migra de uma hierarquia de origem do Configuration Manager 2007.  

##  <a name="a-nameplanmigrateosda-planning-to-migrate-operating-system-deployments"></a><a name="Plan_migrate_OSD"></a> Planejando a migração de implantações de sistema operacional  
É possível migrar os seguintes objetos de implantação do sistema operacional de uma hierarquia de origem com suporte:  

-   Pacotes e imagens do sistema operacional. O caminho de origem das imagens de inicialização é atualizado para o local de imagem padrão para o Windows AIK (Kit de Instalação Automatizada do Windows) no site de destino. Estes são os requisitos e as limitações para migrar pacotes e imagens do sistema operacional:  

    -   Para migrar os arquivos de imagem com êxito, a conta do computador do servidor do Provedor de SMS Provider para o site de nível superior de hierarquias de destino deve ter a permissão de **Ler** e **Gravar** para os arquivos de origem da imagem para o local do Windows AIK dos sites de origem.  

    -   Ao migrar um pacote de instalação do sistema operacional, garanta que a configuração do pacote nos pontos do site de origem para a pasta contenha o arquivo WIM e não para o próprio arquivo WIM. Se os pontos de pacote de instalação apontam para o arquivo WIM, a migração do pacote de instalação falha.  

    -   Quando você migra um pacote de imagem de inicialização de um site de origem do Configuration Manager 2007, a ID do pacote não é mantida no site de destino. Consequentemente, os clientes na hierarquia de destino não podem usar os pacotes de imagem de inicialização que estão disponíveis em pontos de distribuição compartilhados.  

-   Sequências de tarefas. Ao migrar uma sequência de tarefas que contém uma referência ao pacote de instalação do cliente, essa referência é substituída por uma referência ao pacote de instalação de cliente da hierarquia de destino.  

    > [!NOTE]  
    >  Quando você migra uma sequência de tarefas, o Configuration Manager pode migrar objetos que não são necessários na hierarquia de destino. Esses objetos incluem imagens de inicialização e pacotes de instalação de cliente do Configuration Manager 2007.  

-   Drivers e pacotes de driver.  

##  <a name="a-nameplanmigratecompliancesettingsa-planning-to-migrate-desired-configuration-management"></a><a name="Plan_Migrate_Compliance_settings"></a> Planejando a migração do gerenciamento de configuração desejado  
É possível migrar itens de configuração e as linhas de base de configuração.  

> [!NOTE]  
>  Não há suporte para migração de itens de configuração não interpretados das hierarquias de origem do Configuration Manager 2007. Não é possível migrar ou importar esses itens de configuração para a hierarquia de destino. Para obter informações sobre itens de configuração não interpretados, consulte a seção "Uninterpreted Configuration Item" (“Item de configuração não interpretado”) no tópico [About Configuration Items in Desired Configuration Management (Sobre itens de configuração no gerenciamento de configuração desejado)](http://go.microsoft.com/fwlink/?LinkId=103846) na biblioteca de documentação do Configuration Manager 2007.  

É possível importar Pacotes de configuração do Configuration Manager 2007. O processo de importação converte automaticamente o Pacote de configuração para ser compatível com o System Center Configuration Manager.  

##  <a name="a-nameplanmigrateboundariesa-planning-to-migrate-boundaries"></a><a name="Plan_migrate_Boundaries"></a> Planejamento da migração de limites  
 É possível migrar os limites entre hierarquias. Quando você migra limites do Configuration Manager 2007, cada limite do site de origem é migrado ao mesmo tempo e é adicionado a um novo grupo de limites que é criado na hierarquia de destino. Quando você migra limites de uma hierarquia do System Center 2012 Configuration Manager ou do System Center Configuration Manager, cada limite selecionado é adicionado a um novo grupo de limites na hierarquia de destino.  

 Cada grupo de limites criado automaticamente está habilitado para localização de conteúdo, mas não para atribuição de site. Isso impede que os limites sejam sobrepostos para a atribuição de site entre as hierarquias de origem e de destino. Quando você migra de ou para um site de origem do Configuration Manager 2007, isso ajuda a impedir que novos clientes do Configuration Manager 2007 instalados sejam atribuídos incorretamente à hierarquia de destino. Por padrão, os clientes do System Center Configuration Manager não são atribuídos automaticamente a sites do Configuration Manager 2007.  

 Durante a migração, se você compartilhar um ponto de distribuição com a hierarquia de destino, todos os limites associados a essa distribuição serão automaticamente migrados para a hierarquia de destino. Na hierarquia de destino, a migração cria um novo grupo de limites somente leitura para cada ponto de distribuição compartilhado. Se você alterar os limites do ponto de distribuição na hierarquia de destino, o grupo de limites da hierarquia de destino será atualizado com essas alterações durante o ciclo seguinte de coleta de dados.  

##  <a name="a-nameplanmigratereportsa-planning-to-migrate-reports"></a><a name="Plan_Migrate_reports"></a> Planejamento da migração de relatórios  
O Configuration Manager não dá suporte à migração de relatórios. Em vez disso, use o Construtor de Relatórios do SQL Server Reporting Services para exportar os relatórios da hierarquia de origem e, depois, importá-los na hierarquia de destino.  

> [!NOTE]  
>  Como há alterações no esquema dos relatórios entre o Configuration Manager 2007 e o System Center Configuration Manager, teste cada relatório que você importar de uma hierarquia do Configuration Manager 2007 para garantir que ele funcione conforme o esperado.  

Para obter mais informações sobre relatórios, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  

##  <a name="a-nameplanmigrateorgfoldersa-planning-to-migrate-organizational-and-search-folders"></a><a name="Plan_Migrate_Org_Folders"></a> Planejamento da migração de pastas organizacionais e de pesquisa  
 Você pode migrar pastas organizacionais e de pesquisa de uma hierarquia de origem com suporte para uma hierarquia de destino. Além disso, de uma hierarquia de origem do System Center 2012 Configuration Manager ou do System Center Configuration Manager, é possível migrar os critérios de uma pesquisa salva para uma hierarquia de destino.  

 Por padrão, o processo de migração mantém suas estruturas de pasta de pesquisa e pasta administrativa para os objetos e as coleções quando você realiza a migração. No entanto, no Assistente para Criar Trabalho de Migração, na página **Configurações** , você pode configurar um trabalho de migração para que não migre a estrutura organizacional de objetos ao desmarcar a caixa de seleção dessa opção. As estruturas organizacionais das coleções são sempre mantidas.  

 Uma exceção a isso é uma pasta de pesquisa que contém aplicativos virtuais. Quando um pacote do App-V é migrado, ele é transformado em um aplicativo no System Center Configuration Manager. Após a migração da pasta de pesquisa, apenas os pacotes restantes são encontrados, e a pasta de pesquisa não é capaz de localizar o pacote de App-V em virtude dessa conversão para um aplicativo ocorrida quando ele é migrado.  

 Quando migra uma pesquisa salva de uma hierarquia de origem do System Center 2012 Configuration Manager ou do System Center Configuration Manager, você migra os critérios da pesquisa, e não as informações sobre os resultados da pesquisa. A migração de uma pesquisa salva não é aplicável de um site de origem do Configuration Manager 2007.  

##  <a name="a-nameplanmigrateaia-planning-to-migrate-asset-intelligence-customizations"></a><a name="Plan_Migrate_AI"></a> Planejamento da migração de personalizações do Asset Intelligence  
 Você pode migrar personalizações do Asset Intelligence de uma hierarquia de origem com suporte para uma hierarquia de destino. Não há alterações significativas na estrutura das personalizações do Asset Intelligence entre o Configuration Manager 2007 e o System Center Configuration Manager.  

> [!NOTE]  
>  O System Center Configuration Manager não dá suporte à migração de objetos do Asset Intelligence de um site do Configuration Manager 2007 que estiver usando o Asset Intelligence Service 2.0 (AIS 2.0).  

##  <a name="a-nameplanmigrateswmrulesa-planning-to-migrate-software-metering-rules-customizations"></a><a name="Plan_Migrate_SWM_Rules"></a> Planejamento da migração de personalizações de regras de medição de software  
 Não há alterações significativas na medição de software entre o Configuration Manager 2007 e o System Center Configuration Manager. Você pode migrar suas regras de medição de software de uma hierarquia de origem com suporte para uma hierarquia de destino.  

 Por padrão, as regras de medição de software que você migra para uma hierarquia de destino não são associadas a um site específico da hierarquia de destino e, em vez disso, são aplicadas a todos os clientes da hierarquia. Para aplicar uma regra de medição de software a clientes em um site específico, você deve editar a regra de medição depois que ela é migrada.  



<!--HONumber=Nov16_HO1-->


