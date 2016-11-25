---
title: "Introdução às coleções | System Center Configuration Manager"
description: "Veja uma introdução às coleções para usar coleções no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
caps.latest.revision: 8
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 47574218dec5069205f9dba5608c6f136fb032bc


---
# <a name="introduction-to-collections-in-system-center-configuration-manager"></a>Introdução às coleções no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As coleções no System Center Configuration Manager fornecem os meios para organizar os recursos em unidades gerenciáveis, que permitem que você crie uma estrutura organizada que logicamente representa os tipos de tarefas que você deseja executar. As coleções também são usadas para executar operações do Configuration Manager em vários recursos ao mesmo tempo. A tabela a seguir mostra alguns exemplos de como você pode usar as coleções no Configuration Manager:  

|Operação|Exemplo|  
|---------|-------|  
|Recursos de agrupamento|É possível criar coleções que agrupam logicamente os recursos baseados na hierarquia da sua organização.<br /><br /> Por exemplo, é possível criar uma coleção de todos os computadores que residem na UO (Unidade Organizacional) “London Headquarters” do Active Directory. Para obter mais informações sobre como criar esse tipo de coleção, consulte [How to Create Collections in System Center Configuration Manager (Como criar coleções no System Center Configuration Manager)](../../../../core/clients/manage/collections/create-collections.md).<br /><br /> É possível usar essa coleção para executar operações, como definir configurações do Endpoint Protection, definir configurações de gerenciamento de energia do dispositivo ou instalar o cliente do Configuration Manager.|  
|Implantação de aplicativo|Você pode criar uma coleção de todos os computadores que não têm o Microsoft Office 2013 instalado e implantar esse software em todos os computadores na coleção.<br /><br /> Você também pode usar os requisitos do aplicativo para executar esta tarefa. Para obter mais informações, consulte [Como criar aplicativos com o System Center Configuration Manager](../../../../apps/deploy-use/create-applications.md).|  
|Gerenciando as configurações do cliente|Embora as configurações padrão do cliente no Configuration Manager sejam aplicáveis a todos os dispositivos e todos os usuários, você pode criar configurações de cliente personalizadas que sejam aplicáveis a uma coleção de dispositivos ou a um conjunto de usuários.<br /><br /> Por exemplo, se desejar que o controle remoto esteja disponível somente para alguns dispositivos, defina as configurações do cliente para permitir o controle remoto e, em seguida, defina as configurações personalizadas do cliente que não permitem o controle remoto. Implante essas configurações personalizadas do cliente em uma coleção que contenha os computadores que não usarão o controle remoto.<br /><br /> Para obter mais informações sobre como usar coleções para as configurações do cliente, consulte [About client settings in System Center Configuration Manager (Sobre as configurações do cliente no System Center Configuration Manager)](../../../../core/clients/deploy/about-client-settings.md).|  
|Gerenciamento de energia|Para cada coleção que você cria, você pode configurar as configurações de energia, como quando computadores na coleção entram no modo de suspensão quando estão inativos.<br /><br /> Para obter mais informações sobre como usar coleções com gerenciamento de energia, consulte [Introduction to power management (Introdução ao gerenciamento de energia)](../power/introduction-to-power-management.md).|  
|Administração baseada em funções|As coleções podem ser usadas com a administração baseada em funções para controlar quais grupos de usuários têm acesso a vários recursos no console do Configuration Manager.<br /><br /> Para obter mais informações sobre como configurar coleções para administração baseada em funções, consulte [Configure role-based administration for System Center Configuration Manager (Configurar administração baseada em funções para o System Center Configuration Manager)](../../../../core/servers/deploy/configure/configure-role-based-administration.md).|  
|Janelas de Manutenção|As janelas de manutenção fornecem um meio pelo qual os usuários administrativos podem definir um período de tempo em que várias operações do Configuration Manager podem ser executadas nos membros de uma coleção de dispositivos. Você pode usar as janelas de manutenção para ajudar a assegurar que as alterações de configuração do cliente ocorram durante períodos que não afetem a produtividade da organização.<br /><br /> Para obter mais informações sobre as janelas de manutenção, consulte [Como usar janelas de manutenção no System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).|  

 A maioria das tarefas de gerenciamento depende do uso de uma ou mais coleções. Por exemplo, antes de implantar as atualizações de software para dispositivos, você deve identificar uma coleção para a implantação de atualizações de software. Embora você possa usar a coleção interna de todos os sistemas, o uso dessa coleção para tarefas de gerenciamento não é uma prática recomendada. Em todos os ambientes, exceto no de testes, normalmente você será beneficiado com suas próprias coleções personalizadas para identificar de forma mais específica os dispositivos ou usuários para gerenciar.  

 As coleções internas e personalizadas são exibidas nos nós **Coleções de Usuários** e **Coleções de Dispositivos**, no espaço de trabalho **Ativos e Conformidade**, no console do Configuration Manager.  

 As coleções que você exibiu recentemente aparecem no nó **Usuários** e no nó **Dispositivos** , no espaço de trabalho **Ativos e Conformidade** , no console do Configuration Manager.  

## <a name="collection-types-in-configuration-manager"></a>Tipos de coleção no Configuration Manager  
 O Configuration Manager tem algumas coleções internas que você pode usar para operações comuns. Além disso, você pode criar suas próprias coleções que agrupam os recursos específicos para suas necessidades de negócios.  

### <a name="built-in-collections"></a>Coleções internas  
 Por padrão, o Configuration Manager inclui as seguintes coleções, que não podem ser modificadas.  

|**Nome da coleção**|Descrição|  
|-------------------------|-----------------|  
|**Todos os grupos de usuários**|Contém grupos de usuários que são descobertos usando a Descoberta de Grupo de Segurança do Active Directory.|  
|**Todos os Usuários**|Contém os usuários que são descobertos usando a Descoberta de Usuário do Active Directory.|  
|**Todos os usuários e grupos de usuários**|Contém as coleções Todos os Usuários e Todos os Grupos de Usuários. A coleção não pode ser modificada e contém o maior escopo do usuário e recursos do grupo de usuário.|  
|**Todos os clientes de Desktop e Servidor**|Contém os dispositivos de área de trabalho e servidor que têm o cliente do Configuration Manager instalado. A associação é mantida pela Descoberta de Pulsação.|  
|**Todos os dispositivos móveis**|Contém os dispositivos móveis gerenciados pelo Configuration Manager. A associação é restrita para os dispositivos móveis que são atribuídos a um site ou descobertos pelo conector do Exchange Server com êxito.|  
|**Todos os sistemas**|Contém todos os clientes de Área de Trabalho e de Servidor, todos os dispositivos móveis, a coleção de todos os computadores desconhecidos e todos os dispositivos móveis registrados pelo Microsoft Intune.<br /><br /> A coleção não pode ser modificada e contém o escopo maior de recursos do dispositivo.|  
|**Todos os computadores desconhecidos**|Contém registros de computador genérico para várias plataformas de computador. Você pode usar essa coleção para implantar um sistema operacional usando uma sequência de tarefas e a inicialização PXE, a mídia inicializável ou a mídia em pré-configuração.|  

### <a name="custom-collections"></a>Coleções personalizadas  
 Quando você cria uma coleção personalizada no Configuration Manager, a associação da coleção é determinada por uma ou mais regras de coleta. Para obter informações sobre como configurar regras de coleta, consulte [How to Create Collections in Configuration Manager (Como criar coletas no System Center Configuration Manager)](../../../../core/clients/manage/collections/create-collections.md). Há quatro regras que você pode usar:  

#### <a name="direct-rule"></a>Regra direta  
 As diretas regras permitem que você escolha os usuários ou computadores que você deseja adicionar como membros de uma coleção. Esta regra fornece a você controle direto sobre quais recursos são membros da coleção. Esta associação não é alterada automaticamente, a menos que um recurso seja removido do Configuration Manager. O Configuration Manager deve descobrir os recursos ou é necessário importar os recursos antes de poder adicioná-los a uma coleção de regra direta. As coleções de regras diretas têm uma maior sobrecarga administrativa que as coleções de regras de consulta, devido ao fato de ser necessário fazer modificações manuais nesse tipo de coleção.  

#### <a name="query-rule"></a>Regra de consulta  
 As regras de consulta atualizam dinamicamente a associação de uma coleção com base em uma consulta executada pelo Configuration Manager em um agendamento. Por exemplo, é possível criar uma coleção de usuários que são membros da unidade organizacional dos Recursos Humanos nos Serviços de Domínio do Active Directory. Ao contrário das coleções de regra direta, essa associação da coleção é atualizada automaticamente quando você adiciona ou remove novos usuários da unidade organizacional de recursos humanos. As regras de consulta removem a sobrecarga administrativa de adicionar manualmente os dispositivos na coleção usando uma regra direta. No entanto, eles reduzem o controle que você tem sobre quais computadores são adicionados à coleção. Os exemplos de regras com base em consulta são:  

-   Todos os usuários em uma OU especificada  

-   Todos os computadores que executam o Windows 8  

-   Todos os computadores que têm mais de 20GB de espaço livre em disco  

#### <a name="include-collections-rule"></a>Incluir regra de coleções  
 A regra de coleções de inclusão permite que você inclua os membros de outra coleção em uma coleção do Configuration Manager. O Configuration Manager atualizará a associação da coleção atual em um agendamento se a associação da coleção incluída tiver mudado.  

#### <a name="exclude-collections-rule"></a>Excluir regra de coleções  
 A regra de coleções de exclusão permite que você exclua os membros de outra coleção de uma coleção do Configuration Manager. O Configuration Manager atualizará a associação da coleção atual em um agendamento se a associação da coleção excluída tiver mudado.  

> [!NOTE]  
>  Se uma coleção incluir regras de coleção de inclusão e de coleção de exclusão e houver um conflito, a regra de exclusão terá prioridade sobre a regra de inclusão.  

## <a name="incremental-collection-updates"></a>Atualizações de coleção incremental  
 Quando você habilita atualizações incrementais para uma coleção, o Configuration Manager verifica periodicamente recursos novos ou alterados de avaliação da coleção anterior e atualiza uma associação de coleções com esses recursos, independentemente de uma avaliação completa. Por padrão, quando você habilita atualizações de coleção incremental, ele é executado a cada 5 minutos e ajuda a manter os dados da coleção atualizados sem a sobrecarga de uma avaliação completa da coleção.  

> [!NOTE]  
>  Quando você cria uma nova coleção, as atualizações incrementais são desabilitadas por padrão.  



<!--HONumber=Nov16_HO1-->


