---
title: Configurações com suporte
titleSuffix: Configuration Manager
description: Identifique as principais configurações e requisitos para que você possa planejar, implantar e manter uma implantação funcional do System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de769a24b44c5ab5e28035e96fef341aecd78006
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="supported-configurations-for-system-center-configuration-manager"></a>Configurações com suporte para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Como uma solução local, o System Center Configuration Manager usa seus servidores, clientes, configurações de rede e outros produtos como Microsoft Intune, SQL Server e Azure.

As informações descritas neste e nos tópicos a seguir são essenciais para ajudá-lo a identificar as principais configurações, os requisitos e as limitações, para que você possa planejar, implantar e manter uma implantação funcional do Configuration Manager.  Essas informações são específicas à infraestrutura dos sites, das hierarquia e dos dispositivos gerenciados do Configuration Manager.

Quando um recurso ou uma funcionalidade do Configuration Manager exige configurações mais específicas, essas informações são incluídas na documentação específica ao recurso e são complementares aos detalhes de configuração mais gerais.  

 No Configuration Manager, há suporte para os produtos e as tecnologias descritos nos tópicos a seguir. No entanto, sua inclusão neste conteúdo não implica uma extensão de suporte para um produto além do ciclo de vida de suporte individual desse produto. Os produtos além de seu ciclo de vida de suporte não têm suporte para uso com o Configuration Manager. Para obter mais informações sobre os Ciclos de vida de suporte da Microsoft, visite o site [Ciclo de Vida do Suporte da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) .  

> [!NOTE]  
>  Para obter informações sobre a política de ciclo de vida de suporte da Microsoft, acesse o site de perguntas frequentes sobre a Política de Ciclo de Vida do Suporte da Microsoft em [Microsoft Support Lifecycle Policy FAQ (Perguntas frequentes sobre a Política de Ciclo de Vida do Suporte da Microsoft)](http://go.microsoft.com/fwlink/p/?LinkId=31976).  

 Além disso, os produtos e versões do produto que não estão listados nos tópicos a seguir não têm suporte com o System Center Configuration Manager, a menos que eles tenham sido apresentados no [Enterprise Mobility and Security Blog (Blog do Enterprise Mobility and Security)](https://blogs.technet.microsoft.com/enterprisemobility/).  Às vezes, o conteúdo desse blog precede uma atualização neste corpo da documentação.


-  [Números de tamanho e escala](../../../core/plan-design/configs/size-and-scale-numbers.md)  
Saiba mais sobre quantos sites, funções do sistema de sites por site e clientes ou dispositivos têm suporte em diferentes designs de hierarquia do Configuration Manager.

-  [Pré-requisitos de sites e do sistema de sites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Saiba mais sobre as configurações necessárias em um Windows Server para dar suporte a diferentes tipos de site e funções do sistema de sites.

-  [Sistemas operacionais com suporte para servidores de sistema de sites](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
Saiba quais sistemas operacionais podem ser usados como um servidor do site ou servidor do sistema de sites.

-  [Sistemas operacionais com suporte para clientes e dispositivos](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
Saiba quais sistemas operacionais podem ser gerenciados com o Configuration Manager, incluindo Windows, Windows Embedded, Linux e UNIX, Mac e dispositivos móveis.

-  [Sistemas operacionais com suporte para o console](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
Saiba quais sistemas operacionais podem hospedar o console do Configuration Manager para fornecer um ponto de acesso para gerenciar sua implantação.  

-  [Suporte para versões do SQL Server](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
Saiba quais versões do SQL Server podem hospedar o banco de dados do site e o banco de dados de relatório, bem como as configurações obrigatórias e opcionais que podem ser usadas.

-  [Opções de alta disponibilidade](../../../protect/understand/high-availability-options.md)  
Conheça as opções que você pode implementar ao criar seu ambiente para ajudar a manter um alto nível de serviço disponível para sua implantação do Configuration Manager.

-  [Hardware recomendado](../../../core/plan-design/configs/recommended-hardware.md)  
Saiba mais sobre as diretrizes que podem ajudá-lo a identificar o hardware e as configurações certas para hospedar seus sites e principais serviços do Configuration Manager.

-  [Suporte para domínios do Active Directory](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Saiba mais sobre as configurações de domínio do Active Directory com suporte que o Configuration Manager exige e às quais ele dá suporte.

-  [Suporte para redes e recursos do Windows](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
Saiba mais sobre as tecnologias do Windows com suporte (como BranchCache e eliminação de duplicação de dados) e as limitações de seu uso com o Configuration Manager.

-  [Suporte para ambientes de virtualização](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
Saiba mais sobre como usar as tecnologias de máquina virtual com suporte.
