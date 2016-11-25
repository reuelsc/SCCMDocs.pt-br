---
title: "Configurações com suporte | System Center Configuration Manager"
description: "Identifique as principais configurações e requisitos para que você possa planejar, implantar e manter uma implantação funcional do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
caps.latest.revision: 9
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 170bd941bd123b998dd5d6235359aee97adc06bd


---
# <a name="supported-configurations-for-system-center-configuration-manager"></a>Configurações com suporte para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Como uma solução local, o System Center Configuration Manager usa servidores, clientes, configurações de rede e outros produtos como o Microsoft Intune, o SQL Server e o Azure.

As informações deste e dos tópicos a seguir são essenciais para identificar as principais configurações e requisitos ou limitações para planejar, implantar e manter uma implantação funcional do Configuration Manager.  Essas informações são específicas para a infraestrutura dos sites, hierarquia e dispositivos gerenciados do Configuration Manager. Quando um recurso ou uma funcionalidade do Configuration Manager ou requer configurações mais específicas, essas informações serão incluídas com a documentação específica do recurso e complementarão esses detalhes de configuração com suporte mais gerais.  

 Há suporte para os produtos e tecnologias detalhados nos tópicos a seguir no Configuration Manager. No entanto, sua inclusão neste conteúdo não expressa uma extensão do suporte para qualquer produto além do ciclo de vida de suporte individual desses produtos. Os produtos além de seu ciclo de vida de suporte não têm suporte para uso com o Configuration Manager. Para obter mais informações sobre os Ciclos de vida de suporte da Microsoft, visite o site [Ciclo de Vida do Suporte da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) .  

> [!NOTE]  
>  Para obter informações sobre a política de ciclo de vida de suporte da Microsoft, acesse o site de perguntas frequentes sobre a Política de Ciclo de Vida do Suporte da Microsoft em [Microsoft Support Lifecycle Policy FAQ (Perguntas frequentes sobre a Política de Ciclo de Vida do Suporte da Microsoft)](http://go.microsoft.com/fwlink/p/?LinkId=31976).  

 Além disso, os produtos e versões do produto que não estão listados nos tópicos a seguir não têm suporte com o System Center Configuration Manager, a menos que eles tenham sido apresentados no [Enterprise Mobility and Security Blog (Blog do Enterprise Mobility and Security)](https://blogs.technet.microsoft.com/enterprisemobility/).  Às vezes, o conteúdo desse blog antecipará uma atualização para este corpo da documentação.


-  [Números de tamanho e escala](../../../core/plan-design/configs/size-and-scale-numbers.md)  
Detalhes sobre quantos sites, funções do sistema de sites por site e os clientes ou dispositivos têm suporte em diferentes designs de hierarquia do Configuration Manager.

-  [Pré-requisitos de sites e do sistema de sites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Configurações necessárias em um servidor Windows para dar suporte a diferentes tipos de site e de funções do sistema de sites.

-  [Sistemas operacionais com suporte para servidores de sistema de sites](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
Saiba quais sistemas operacionais é possível usar como um servidor do site ou servidor de sistema de sites.

-  [Sistemas operacionais com suporte para clientes e dispositivos](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
Saiba quais sistemas operacionais é possível gerenciar com o Configuration Manager, incluindo Windows, Linux e UNIX, Mac, sistemas operacionais incorporados e dispositivos móveis.

-  [Sistemas operacionais com suporte para o console](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
Saiba quais sistemas operacionais podem hospedar o console do Configuration Manager para fornecer um ponto de acesso para gerenciar sua implantação.  

-  [Suporte para versões do SQL Server](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
Lista as versões do SQL Server que podem hospedar o banco de dados do site e o banco de dados de relatório, bem como configurações obrigatórias e configurações opcionais que você pode escolher usar.

-  [Opções de alta disponibilidade](../../../protect/understand/high-availability-options.md)  
Conheça as opções que você pode implementar ao criar seu ambiente para ajudar a manter um alto nível de serviço disponível para sua implantação do Configuration Manager.

-  [Hardware recomendado](../../../core/plan-design/configs/recommended-hardware.md)  
Diretrizes que podem ajudar a identificam o hardware e as configurações certas para hospedar seus sites e principais serviços do Configuration Manager.

-  [Suporte para domínios do Active Directory](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Conheça as configurações de domínio do Active Directory com suporte que o Configuration Manager exige e às quais ele dá suporte.

-  [Suporte para redes e recursos do Windows](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
O Configuration Manager dá suporte a várias tecnologias do Windows como eliminação de duplicação de dados e o BranchCache. Conheça as tecnologias com suporte e as limitações de uso com o Configuration Manager.

-  [Suporte para ambientes de virtualização](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
Informações para ajudá-lo a usar as tecnologias de máquina virtual com suporte.



<!--HONumber=Nov16_HO1-->


