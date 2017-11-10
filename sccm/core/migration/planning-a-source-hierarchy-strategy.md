---
title: "Estratégia de hierarquia de origem"
titleSuffix: Configuration Manager
description: "Configure uma hierarquia de origem e colete dados de um site de origem antes de configurar um trabalho de migração do System Center Configuration Manager."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4800a800-66c8-4c35-aebe-e413a23790c1
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: deebf706c885dfb1f0838c64df0d201274eee3d8
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="plan-a-source-hierarchy-strategy-in-system-center-configuration-manager"></a>Planejar uma estratégia de hierarquia de origem no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de configurar um trabalho de migração no ambiente do System Center Configuration Manager, é necessário configurar uma hierarquia de origem e coletar dados de pelo menos um site de origem nessa hierarquia. Use as seções a seguir para ajudá-lo a se planejar para configurar as hierarquias de origem, configurar os sites de origem e determinar como o Configuration Manager coleta as informações de sites de origem na hierarquia de origem. 

##  <a name="BKMK_Source_Hierarchies"></a> Hierarquias de origem  
A hierarquia de origem é uma hierarquia do Configuration Manager que contém dados que você deseja migrar. Ao configurar uma hierarquia de migração e especificar a hierarquia de origem, você especifica o site de nível superior da hierarquia da origem. Este site também é chamado de site de origem. Os sites adicionais dos quais você pode migrar os dados na hierarquia de origem também são chamados de sites de origem.  

-   Ao configurar um trabalho de migração para migrar dados de uma hierarquia de origem do Configuration Manager 2007, você o configura para migrar dados de um ou mais sites de origem na hierarquia de origem.  

-   Ao configurar um trabalho de migração para migrar dados de uma hierarquia de origem que execute o System Center 2012 Configuration Manager ou posterior, basta especificar o site de nível superior.  

Você pode configurar apenas uma hierarquia de origem por vez.  

-   Se você configurar uma nova hierarquia de origem, essa hierarquia se tornará automaticamente a hierarquia de origem atual que substitui a hierarquia de origem anterior.  

-   Ao configurar uma hierarquia de origem, você deve especificar o site de nível superior da hierarquia de origem e especificar as credenciais do Configuration Manager a serem usadas para se conectar ao Provedor de SMS e ao banco de dados do site desse site de origem.  

-   O Configuration Manager usa essas credenciais para executar a coleta de dados, a fim de recuperar informações sobre os objetos e os pontos de distribuição do site de origem.  

-   Como parte do processo de coleta de dados, sites filho na hierarquia de origem são identificados.  

-   Se a hierarquia de origem for uma hierarquia do Configuration Manager 2007, você poderá configurar sites adicionais como sites de origem, com credenciais separadas para cada site de origem.  

Apesar de você poder configurar várias hierarquias de origem sucessivamente, a migração estará ativa somente para uma hierarquia de origem de cada vez.  

-   Se você configurar uma hierarquia de origem adicional antes de concluir a migração da hierarquia de origem atual, o Configuration Manager cancelará os trabalhos de migração ativos e adiará todos os trabalhos de migração agendados para a hierarquia de origem atual.  

-   A hierarquia de origem configurada recentemente se torna a hierarquia de origem atual e a hierarquia de origem original agora está inativa.  

-   Você pode configurar credenciais de conexão, sites de origem adicionais e trabalhos de migração para a nova hierarquia de origem.  

Se você restaurar uma hierarquia de origem inativa e não tiver usado **Limpar Dados de Migração** anteriormente, você pode exibir os trabalhos de migração configurados anteriormente para essa hierarquia de origem. No entanto, para poder continuar a migração dessa hierarquia, é necessário reconfigurar as credenciais para se conectar aos sites de origem aplicáveis na hierarquia e reagendar os trabalhos de migração que não foram concluídos.  

> [!CAUTION]  
>  Se você migrar os dados de uma única hierarquia de origem, cada hierarquia de origem adicional deverá conter um conjunto exclusivo de códigos do site.  

Para obter mais informações sobre como configurar uma hierarquia de origem, consulte [Configurando hierarquias de origem e sites de origem para migração para o System Center Configuration Manager](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)  

##  <a name="BKMK_Source_Sites"></a> Sites de origem  
 Os sites de origem são sites na hierarquia de origem que possuem os dados que você deseja migrar. O site de nível superior da hierarquia da origem é sempre o primeiro site de origem. Quando a migração coleta os dados do primeiro site de origem de uma nova hierarquia de origem, ela descobre informações sobre os sites adicionais nessa hierarquia.  

 Concluída a coleta de dados para o site de origem inicial, as ações a serem tomadas dependerão da versão do produto da hierarquia de origem.  

### <a name="source-sites-that-run-configuration-manager-2007-sp2"></a>Sites de origem que executam o Gerenciador de Configurações 2007 SP2  
 Após a coleta de dados do site de origem inicial da hierarquia do Configuration Manager 2007 SP2, não é necessário configurar os sites de origem adicionais para poder criar os trabalhos de migração. No entanto, para poder migrar dados de sites adicionais, é necessário configurar os sites adicionais como sites de origem e o System Center Configuration Manager coletar com êxito os dados daqueles sites.  

 Para coletar os dados de sites adicionais, você deve configurar cada site como site de origem. Para tanto, é necessário especificar as credenciais de conexão do System Center Configuration Manager ao Provedor de SMS e ao banco de dados de cada site de origem. Depois de você configurar as credenciais para um site de origem, o processo de coleta de dados para esse site é iniciado.  

 Ao configurar sites de origem adicionais em uma hierarquia de origem do Configuration Manager 2007 SP2, é necessário configurar os sites de origem de cima para baixo, o que significa que os sites na parte inferior da camada serão configurados por último. A qualquer momento é possível configurar os sites de origem em uma ramificação da hierarquia, mas para isso é preciso configurar um site como site de origem antes de configurar seus sites filho como sites de origem.  

> [!NOTE]  
>  Há suporte para migração somente para sites primários em uma hierarquia do Configuration Manager 2007 SP2.  

### <a name="source-sites-that-run-system-center-2012-configuration-manager-or-later"></a>Sites de origem que executam o System Center 2012 Configuration Manager ou posterior  
 Após a coleta de dados do site de origem inicial da hierarquia do System Center 2012 Configuration Manager ou posterior, não é necessário configurar sites de origem adicionais nessa hierarquia de origem. Isso ocorre porque, diferentemente do Configuration Manager 2007, estas versões do Configuration Manager usam um banco de dados compartilhado e este banco de dados permite que você identifique e migre todos os objetos disponíveis do site de origem inicial.  

 Ao configurar as contas de acesso para coletar dados, talvez você precise ao **Provedor de SMS do Site de Origem** o acesso a vários computadores na hierarquia de origem. Isso pode ser necessário quando o site de origem dá suporte a várias instâncias do provedor de SMS, cada um em um computador diferente. Quando a coleta de dados é iniciada, o site de nível superior da hierarquia de destino entra em contato com o site de nível superior da hierarquia de origem para identificar o local do Provedor de SMS para esse site. Somente a primeira instância do Provedor de SMS é identificada. Se o processo de coleta de dados não puder acessar o Provedor de SMS no local identificado, o processo falhará e não tentará se conectar aos computadores adicionais que executam uma instância do Provedor de SMS para esse site.  

##  <a name="BKMK_Data_Gathering"></a> Coleta de dados  
 Imediatamente após você especificar a hierarquia de origem, configurar as credenciais para cada site de origem adicional em uma hierarquia de origem ou compartilhar os pontos de distribuição para um site de origem, o Configuration Manager iniciará a coleta de dados do site de origem.  

 O processo de coleta de dados se repete em um agendamento simples para manter a sincronização com todas as alterações nos dados no site de origem. Por padrão, o processo se repete a cada quatro horas. É possível alterar o agendamento para esse ciclo editando as **Propriedades** do site de origem. O processo inicial de coleta de dados deve examinar todos os objetos no banco de dados do Configuration Manager, o que pode demorar muito até a sua conclusão. Os processos de coleta de dados subsequentes identificam apenas as alterações nos dados e requerem menos tempo para sua conclusão.  

 Para coletar dados, o site de nível superior na hierarquia de destino conecta-se ao Provedor de SMS e ao banco de dados do site de origem para recuperar uma lista de objetos e pontos de distribuição. Essas conexões usam as contas de acesso do site de origem. Para obter informações sobre as configurações necessárias para a coleta de dados, consulte [Pré-requisitos para a migração no System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

 Você pode iniciar e interromper o processo de coleta de dados usando **Coletar Dados Agora** e **Parar Coleta de Dados** no console do Configuration Manager.  

 Após usar **Parar Coleta de Dados** para um site de origem, seja por qual motivo for, será necessário reconfigurar as credenciais para o site antes de poder coletar dados dele novamente. Até que você reconfigure o site de origem, o Configuration Manager não poderá identificar novos objetos nem alterações em objetos migrados anteriormente nesse site.  

> [!NOTE]  
>  Para poder expandir um site primário autônomo em uma hierarquia com um site de administração central, você deverá interromper toda a coleta de dados. Você pode reconfigurar a coleta de dados após a conclusão da expansão do site.  

### <a name="gather-data-now"></a>Coletar Dados Agora  
 Após a execução do processo inicial de coleta de dados para o site, esse processo se repete para identificar os objetos que foram atualizados desde o último ciclo de coleta de dados. Você também pode usar a ação **Coletar Dados Agora** no console do Configuration Manager para iniciar imediatamente o processo e redefinir a hora de início do próximo ciclo.  

 Concluído com êxito o processo de coleta de dados para o site de origem, você pode compartilhar os pontos de distribuição do site de origem e configurar os trabalhos de migração de dados do site. A coleta de dados é um processo de repetição na migração, que continua até você alterar a hierarquia de origem ou usar **Parar Coleta de Dados** para finalizar o processo de coleta de dados para o site.  

### <a name="stop-gathering-data"></a>Parar Coleta de Dados  
 Você pode usar **Parar Coleta de Dados** para finalizar o processo de coleta de dados para um site de origem quando você não deseja mais que o Configuration Manager identifique objetos novos e alterados desse site. Essa ação também impede que o Configuration Manager ofereça a clientes na hierarquia de destino algum ponto de distribuição compartilhado da origem como local de conteúdo para o conteúdo que você migrou.  

 Para interromper a coleta de dados de cada site de origem, é necessário executar **Parar Coleta de Dados** nos sites de origem da camada inferior e repetir o processo em cada site pai. O site de nível superior da hierarquia de origem deve ser o último site em que a coleta de dados seja interrompida. É necessário interromper a coleta de dados em todo site filho para poder executar essa ação em um site pai. Normalmente, você interrompe a coleta de dados somente quando está pronto para concluir o processo de migração.  

 Após interromper a coleta de dados para um site de origem, as informações de objetos e coleções desse site coletadas anteriormente permanecem disponíveis para uso quando você configurar novos trabalhos de migração. No entanto, você não vê novos objetos ou novas coleções, nem alterações feitas em objetos existentes. Ao reconfigurar o site de origem e iniciar novamente a coleta de dados, você verá as informações e o status de objetos migrados anteriormente.  
