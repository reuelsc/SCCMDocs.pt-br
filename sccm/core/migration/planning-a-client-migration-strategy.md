---
title: "Planejar a migração de cliente | System Center Configuration Manager"
description: Saiba mais sobre as tarefas que migram clientes de uma hierarquia de origem para uma hierarquia de destino do System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e27b0b7-7bd3-45cd-bc99-9c991606c637
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 6044f9b8116687fca80deeea87abd4652f773db0


---
# <a name="planning-a-client-migration-strategy-in-system-center-configuration-manager"></a>Planejamento de uma estratégia de migração de cliente no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para migrar clientes da hierarquia de origem para uma hierarquia de destino do System Center Configuration Manager, é necessário executar duas tarefas. Você deve migrar os objetos associados ao cliente e reinstalar ou reatribuir os clientes da hierarquia de origem para a hierarquia de destino. Migre os objetos primeiro para que fiquem disponíveis quando os clientes forem migrados. Os objetos associados ao cliente são migrados por meio de trabalhos de migração. Para obter informações sobre como migrar os objetos associados ao cliente, consulte [Planejando estratégia de trabalho de migração no System Center Configuration Manager](../../core/migration/planning-a-migration-job-strategy.md).  

 Use as seções a seguir para ajudar a planejar como migrar clientes para a hierarquia de destino.  

-   [Planejar a migração de clientes para a hierarquia de destino](#Planning_for_Client_Agent_Migration)  

-   [Planejar como tratar os dados mantidos nos clientes durante a migração](#Planning_for_Client_Data_Migration)  

-   [Planejar os dados de inventário e de conformidade durante a migração](#Planning_for_Inventory_data_migration)  

##  <a name="a-nameplanningforclientagentmigrationa-plan-to-migrate-clients-to-the-destination-hierarchy"></a><a name="Planning_for_Client_Agent_Migration"></a> Planejar a migração de clientes para a hierarquia de destino  
 Ao migrar clientes de uma hierarquia de origem, o software do cliente no computador cliente será atualizado para corresponder à versão do produto da hierarquia de destino:  

-   **Uma hierarquia de origem do Configuration Manager 2007:** ao migrar clientes de uma hierarquia de origem que executa uma versão com suporte do Configuration Manager, o software cliente é atualizado para a versão do cliente da hierarquia de destino.  

-   **Uma hierarquia de origem do System Center 2012 Configuration Manager ou posterior:** ao migrar clientes entre hierarquias que são da mesma versão do produto, o software cliente não é alterado nem atualizado. Em vez disso, o cliente é reatribuído da hierarquia de origem para um local na hierarquia de destino.  

    > [!NOTE]  
    >  Quando não há suporte para a versão do produto de uma hierarquia para migração para sua hierarquia de destino, atualize todos os sites e clientes na hierarquia de origem para uma versão compatível do produto. Depois de atualizar a hierarquia de origem para uma versão do produto com suporte, você poderá migrar entre as hierarquias. Para mais informações, consulte a seção [Versões do Configuration Manager com suporte para migração](../../core/migration/prerequisites-for-migration.md#BKMK_supportedmigrationversions) no tópico [Pré-requisitos para a migração no System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

Use as seguintes informações para ajudá-lo a planejar a migração do cliente:  

-   Para atualizar ou reatribuir clientes do site de origem para o site de destino, você poderá usar qualquer método de implantação de cliente com suporte para implantar clientes na hierarquia de destino. Os métodos típicos de implantação de cliente incluem instalação de cliente por push, distribuição de software, Política de Grupo e instalação do cliente com base na atualização de software. Para mais informações, consulte [Métodos de instalação do cliente no System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md).  

-   Verifique se o dispositivo que executa o software cliente na hierarquia de origem atende aos requisitos mínimos de hardware e executa um sistema operacional com suporte para versão do Configuration Manager na hierarquia de destino.  

-   Para poder migrar um cliente, execute o trabalho de migração para migrar as informações que o cliente usará na hierarquia de destino.  

-   Os clientes atualizados mantêm seu histórico de execução em implantações a fim de evitar que implantações sejam executadas desnecessariamente na hierarquia de destino:  

    -   Para clientes do Configuration Manager 2007, o histórico de execução de anúncio é mantido.  

    -   Com clientes do System Center 2012 Configuration Manager ou System Center Configuration Manager, o histórico de execução de implantação é mantido.  

-   Você pode migrar clientes de sites na hierarquia de origem na ordem que desejar. No entanto, é recomendável migrar um número pequeno de clientes por fase, em vez de um número grande de clientes de uma vez. Uma migração em fases reduz os requisitos de largura de banda da rede e o processamento do servidor quando cada cliente recém-atualizado envia a seu site atribuído seu inventário completo inicial e os dados de conformidade.  

-   Ao migrar clientes do Configuration Manager 2007, o software cliente existente é desinstalado do computador cliente e o novo software cliente é instalado.  

-   O Configuration Manager não pode migrar um cliente do Configuration Manager 2007 que tem o cliente App-V instalado, a menos que a versão do cliente App-V seja 4.6 SP1 ou posterior.  

Você pode monitorar o processo de migração do cliente no nó **Migração** do espaço de trabalho **Administração**, no console do Configuration Manager.  

Concluída a migração do cliente para a hierarquia de destino, você não poderá mais gerenciar o dispositivo usando sua hierarquia de origem e deverá considerar remover o cliente dessa hierarquia. Apesar de não ser um requisito para a migração de hierarquias, isso poderá ajudar a evitar a identificação do cliente migrado em um relatório de hierarquia de origem, ou ainda uma contagem incorreta de recursos entre as duas hierarquias durante a migração. Por exemplo, quando um cliente migrado permanecer no banco de dados do site de origem, você possivelmente executará um relatório de atualizações de software que identificará incorretamente o computador como um recurso não gerenciado, quando na verdade ele é gerenciado pela hierarquia de destino.  

##  <a name="a-nameplanningforclientdatamigrationa-plan-to-handle-data-maintained-on-clients-during-migration"></a><a name="Planning_for_Client_Data_Migration"></a> Planejar como tratar os dados mantidos nos clientes durante a migração  
Ao migrar um cliente de sua hierarquia de origem para a hierarquia de destino, algumas informações são mantidas no dispositivo enquanto outras ficam indisponíveis no dispositivo após a migração.  

As informações a seguir são mantidas no dispositivo do cliente:  

-   O GUID (Identificador Exclusivo), que associa um cliente a suas informações no banco de dados do Configuration Manager.  

-   O histórico de anúncio ou implantação, que evita execuções desnecessárias de anúncios e implantações de clientes na hierarquia de destino.  

As informações a seguir não são mantidas no dispositivo do cliente:  

-   Os arquivos no cache de cliente. Se o cliente necessitar desses arquivos para instalar o software, ele deverá baixar os arquivos novamente da hierarquia de destino.  

-   As informações da hierarquia de origem sobre anúncios ou implantações que ainda não foram executados. Se você desejar que o cliente execute anúncios ou implantações após sua migração, será necessário reimplantá-los no cliente na hierarquia de destino.  

-   Informações sobre o inventário. O cliente reenvia essa informação a seu site atribuído na hierarquia de destino após a migração do cliente e os novos dados do cliente são gerados.  

-   Dados de conformidade. O cliente reenvia essa informação a seu site atribuído na hierarquia de destino após a migração do cliente e os novos dados do cliente são gerados.  

Quando um cliente migra, as informações armazenadas no Registro do cliente do Configuration Manager e o caminho do arquivo não são mantidos. Após a migração, reaplique essas configurações. As configurações típicas incluem:  

-   Esquemas de energia  

-   Configurações de log  

-   Configurações de política local  

Além disso, talvez seja necessário você reinstalar alguns aplicativos.  

##  <a name="a-nameplanningforinventorydatamigrationa-plan-for-inventory-and-compliance-data-during-migration"></a><a name="Planning_for_Inventory_data_migration"></a> Planejar os dados de inventário e de conformidade durante a migração  
Os dados de inventário e de conformidade do cliente não são salvos quando você migra um cliente para a hierarquia de destino. Em vez disso, essa informação é recriada na hierarquia de destino quando o cliente envia primeiro informação a seu site atribuído. Para ajudar a reduzir os requisitos de largura de banda da rede e o processamento do servidor resultantes, é recomendável migrar um número pequeno de clientes por fase, em vez de um número grande de clientes de uma vez.  

 Além disso, você não pode migrar de uma hierarquia de origem as personalizações de inventário de hardware. É necessário introduzi-las na hierarquia de destino independentemente da migração. Para obter informações sobre como estender o inventário de hardware personalizado, consulte [Como configurar o inventário de hardware no System Center Configuration Manager](../../core/clients/manage/inventory/configure-hardware-inventory.md).  



<!--HONumber=Nov16_HO1-->


