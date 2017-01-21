---
title: Escolha o que migrar | Microsoft Docs
description: "Saiba quais dados você pode migrar e quais dados você não pode migrar para o System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99222dc8-0e1e-4513-8302-7a1acf671e9b
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5e3d3f4194b06442e34c10988a20fe9ca40ac5d7
ms.openlocfilehash: 66e01cbe84206cb1b29893b768c1bc831f2f6cfc


---
# <a name="determine-whether-to-migrate-data-to-system-center-configuration-manager"></a>Determinar se realizará ou não a migração de dados para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

No System Center Configuration Manager, a migração fornece um processo para transferir dados e configurações que você fez de versões do Configuration Manager com suporte para sua nova hierarquia.  Você pode usá-la para:  

-   Combinar várias hierarquias em uma  

-   Mover dados e configurações de uma implantação de laboratório para sua implantação de produção  

-   Mova dados e a configuração de uma versão do Configuration Manager anterior, como o Configuration Manager 2007 que não tem nenhum caminho de atualização para o System Center Configuration Manager, ou do System Center 2012 Configuration Manager (que dá suporte a um caminho de atualização para o System Center Configuration Manager).  

Com exceção da função do sistema de site do ponto de distribuição e dos computadores que hospedam pontos de distribuição, nenhuma infraestrutura (o que inclui sites, funções do sistema de site e computadores que hospedam uma função do sistema de site) migra, transfere ou pode ser compartilhada entre hierarquias.  

 Embora não seja possível migrar a infraestrutura do servidor, é possível migrar clientes do Configuration Manager entre hierarquias. A migração de cliente envolve migrar os dados que os clientes usam da hierarquia de origem para a hierarquia de destino e instalar ou reatribuir o software cliente de forma que o cliente se reporte à nova hierarquia. Após instalar um cliente na nova hierarquia e o cliente enviar seus dados, sua ID exclusiva do Configuration Manager ajuda o Configuration Manager a associar os dados que você migrou anteriormente para cada computador cliente.  

 A funcionalidade proporcionada pela migração ajuda você a manter investimentos feitos em configurações e implantações e aproveitar totalmente as alterações principais do produto introduzidas pela primeira vez no System Center 2012 Configuration Manager e continuadas no System Center Configuration Manager. Essas alterações incluem uma hierarquia simplificada do Configuration Manager, que usa menos sites e recursos, e o processamento melhorado usando código nativo de 64 bits executado em hardware de 64 bits.  

 Para obter informações sobre as versões do Configuration Manager que têm suporte pela migração, consulte [Pré-requisitos para a migração no System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

 As seções a seguir podem ajudar a planejar os dados que você pode ou não migrar:  

-   [Dados que você pode migrar para o System Center Configuration Manager](#Can_Migrate)  

-   [Dados que você não pode migrar para o System Center Configuration Manager](#Cannot_migrate)  

##  <a name="a-namecanmigratea-data-that-you-can-migrate-to-system-center-configuration-manager"></a><a name="Can_Migrate"></a> Dados que você pode migrar para o System Center Configuration Manager  
 A migração pode migrar a maioria dos objetos entre as hierarquias com suporte do Configuration Manager. É necessário modificar as instâncias migradas de alguns objetos de uma versão com suporte do Configuration Manager 2007 para estar em conformidade com o esquema e o formato de objeto do System Center 2012 Configuration Manager. Essas modificações não afetam os dados no banco de dados do site de origem. Objetos migrados de uma versão com suporte do System Center 2012 Configuration Manager ou o System Center Configuration Manager não requer modificação.  

 Veja a seguir os objetos que podem migrar com base na versão do Configuration Manager na hierarquia de origem. Alguns objetos, como consultas, não migram. Se você quiser continuar usando esses objetos que não migram, será preciso recriá-los na nova hierarquia. Outros objetos, o que inclui alguns dados do cliente, são recriados automaticamente na nova hierarquia quando os clientes são gerenciados nessa hierarquia.  

 **Objetos que você pode migrar do System Center 2012 Configuration Manager ou do branch atual do System Center Configuration Manager:**  

-   Anúncios  

-   Aplicativos para o System Center 2012 Configuration Manager e versões posteriores  

-   Ambiente Virtual do App-V do System Center 2012 Configuration Manager e versões posteriores  

-   Personalizações do Asset Intelligence  

-   Limites  

-   Coleções — para migrar coleções de uma versão compatível do System Center 2012 Configuration Manager ou do System Center Configuration Manager, use um trabalho de migração de objeto.  

-   Configurações de conformidade:  

    -   Linhas de base de configuração  

    -   Itens de configuração  

-   Implantação de sistema operacional:  

    -   Imagens de inicialização  

    -   Pacotes de driver  

    -   Drivers  

    -   Imagens  

    -   Pacotes  

    -   Sequências de tarefas  

-   Resultados da pesquisa — critérios de pesquisa salvos  

-   Atualizações de software:  

    -   Implantações  

    -   Pacotes de implantação  

    -   Modelos  

    -   Listas de atualizações de software  

-   Pacotes de distribuição de software  

-   Regras de medição de software  

-   Pacotes de aplicativos virtuais  

 **Objetos que você pode migrar do Configuration Manager 2007 SP2:**  

-   Anúncios  

-   Aplicativos para o System Center 2012 Configuration Manager e versões posteriores  

-   Ambiente Virtual do App-V do System Center 2012 Configuration Manager e versões posteriores  

-   Personalizações do Asset Intelligence  

-   Limites  

-   Coleções — você migra coleções de uma versão compatível do Configuration Manager 2007 usando um trabalho de migração de coleção.  

-   Configurações de conformidade (conhecidas como gerenciamento de configurações desejadas no Configuration Manager 2007):  

    -   Linhas de base de configuração  

    -   Itens de configuração  

-   Implantação de sistema operacional:  

    -   Imagens de inicialização  

    -   Pacotes de driver  

    -   Drivers  

    -   Imagens  

    -   Pacotes  

    -   Sequências de tarefas  

-   Resultados da pesquisa — pastas de pesquisa  

-   Atualizações de software:  

    -   Implantações  

    -   Pacotes de implantação  

    -   Modelos  

    -   Listas de atualizações de software  

-   Pacotes de distribuição de software  

-   Regras de medição de software  

-   Pacotes de aplicativos virtuais  

##  <a name="a-namecannotmigratea-data-that-you-cannot-migrate-to-system-center-configuration-manager"></a><a name="Cannot_migrate"></a> Dados que você não pode migrar para o System Center Configuration Manager  
 Não é possível migrar os seguintes tipos de objetos:  

-   Informações de provisionamento de cliente AMT  

-   Arquivos em clientes, o que inclui:  

    -   Dados de inventário e histórico do cliente  

    -   Arquivos no cache do cliente  

-   Consultas  

-   Instâncias e direitos de segurança do Configuration Manager 2007 para o site e os objetos  

-   Relatórios do Configuration Manager 2007 do SQL Server Reporting Services  

-   Relatórios da Web do Configuration Manager 2007  

-   Relatórios do System Center 2012 Configuration Manager e do System Center Configuration Manager  

-   Administração baseada em função do System Center 2012 Configuration Manager e do System Center Configuration Manager:  

    -   Funções de segurança  

    -   Escopos de segurança  



<!--HONumber=Dec16_HO3-->


