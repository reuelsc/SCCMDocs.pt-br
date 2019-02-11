---
title: Escolher uma solução de gerenciamento de dispositivo
titleSuffix: Configuration Manager
description: Conheça as soluções oferecidas pelo Configuration Manager para gerenciar computadores, servidores e dispositivos.
ms.date: 01/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1214a5b73b3e6b1bddab8a3918ddd32af0cacb68
ms.sourcegitcommit: f7b2fe522134cf102a3447505841cee315d3680c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2019
ms.locfileid: "55570193"
---
# <a name="choose-a-device-management-solution-for-configuration-manager"></a>Escolher uma solução de gerenciamento de dispositivo para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Configuration Manager oferece diferentes soluções para o gerenciamento de computadores, servidores e dispositivos. Escolha a solução adequada para sua organização. Baseie sua decisão nas plataformas de dispositivos que você precisa gerenciar e na funcionalidade de gerenciamento necessária.  


> [!Important]  
> O gerenciamento híbrido de dispositivos móveis é um [recurso preterido](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures) desde 14 de agosto de 2018. Para saber mais, confira [O que é o MDM híbrido](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  
<!-- SCCMDocs issue 1197 -->



## <a name="overview"></a>Visão geral

Este artigo aborda as quatro seguintes soluções de gerenciamento de dispositivo: 
- [Cliente do Configuration Manager](#bkmk_sccm)
- [MDM (Gerenciamento de Dados Mestre) local com o Configuration Manager](#bkmk_opmdm)
- [Cogerenciamento com o Microsoft Intune](#bkmk_intune)
- [Microsoft Exchange](#bkmk_opmdm)

Use essas soluções de gerenciamento de dispositivo sozinhas ou combinadas umas com as outras. Por exemplo, é possível usar a abordagem de gerenciamento baseada em cliente para gerenciar computadores e servidores em sua organização, além do cogerenciamento para os laptops baseados na internet. Ao combinar as abordagens dessa forma, você pode atender a todas as necessidades de gerenciamento de dispositivo.  

Este artigo também inclui duas tabelas que comparam as soluções de gerenciamento pelos seguintes fatores: 
- [Comparação por plataformas com suporte](#bkmk_comp1)
- [Comparação por funcionalidade de gerenciamento](#bkmk_comp2)


### <a name="bkmk_sccm"></a>Cliente do Configuration Manager  

Essa opção requer a instalação do cliente do Configuration Manager nos dispositivos. Ela fornece a maioria dos recursos para gerenciar computadores, servidores e outros dispositivos em seu ambiente. 

Confira mais informações em [Métodos de instalação do cliente](/sccm/core/clients/deploy/plan/client-installation-methods).  


### <a name="bkmk_opmdm"></a> MDM local  

Essa opção usa os recursos internos de gerenciamento de dispositivo do Windows 10. Embora não tão completo quanto o gerenciamento baseado em cliente, o gerenciamento de dispositivo móvel local oferece uma abordagem mais leve de gerenciamento. Ele usa recursos do Configuration Manager local para gerenciar dispositivos.  

Para saber mais, confira [Gerenciar dispositivos móveis com a infraestrutura local](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).  


### <a name="bkmk_comanage"></a>Cogerenciamento com o Microsoft Intune

O cogerenciamento é uma das principais formas de conectar a implantação existente do Configuration Manager à nuvem do Microsoft 365. Ele permite gerenciar simultaneamente os dispositivos com Windows 10 usando o Configuration Manager e o Microsoft Intune. O cogerenciamento permite conectar na nuvem seu investimento existente no Configuration Manager agregando novas funcionalidades. 

Confira mais informações em [O que é cogerenciamento?](/sccm/comanage/overview).  


### <a name="bkmk_exchange"></a>Microsoft Exchange  

Essa opção usa o conector do Exchange Server para conectar vários servidores Exchange ao Configuration Manager. Com isso, o gerenciamento dos dispositivos que podem se conectar ao Exchange ActiveSync é centralizado. Você pode configurar os recursos de gerenciamento de dispositivos móveis do Exchange no console do Configuration Manager. Entre os recursos de exemplo estão o apagamento remoto de dispositivo e o controle de configurações para vários servidores do Exchange.

Para saber mais, confira [Gerenciar dispositivos móveis com o Configuration Manager e o Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  



## <a name="bkmk_comp1"></a> Compare as soluções por plataformas com suporte  

|Plataforma|Cliente do Configuration Manager|MDM local|Configuration Manager com Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Android| | |Sim|  
|iOS| | |Sim|  
|Mac OS X|Sim| |Sim|  
|UNIX/Linux|Sim| |Sim|  
|Windows 10|Sim|Sim|Sim|  
|Windows 10 Mobile| |Sim|Sim|  
|Windows (versões anteriores)|Sim| |Sim|  
|Windows Server|Sim| |Sim|  
|Windows CE|Sim (com cliente herdado de dispositivo móvel)| |Sim|  
|Windows Embedded|Sim| | |  
|Windows Mobile| | |Sim|  

Para ver uma lista das plataformas com suporte, consulte [Sistemas operacionais com suporte para clientes e dispositivos para o System Center Configuration Manager](configs/supported-operating-systems-for-clients-and-devices.md).

A Microsoft recomenda usar o Intune para gerenciar dispositivos móveis Android, iOS e Windows 10. Confira mais informações em [O que é o Microsoft Intune?](https://docs.microsoft.com/intune/what-is-intune)



##  <a name="bkmk_comp2"></a> Compare as soluções por funcionalidade de gerenciamento  

|Funcionalidade de gerenciamento|Cliente do Configuration Manager|MDM local|Configuration Manager com Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Segurança de PKI (infraestrutura de chave pública) entre o dispositivo móvel e o Configuration Manager (usa autenticação mútua e SSL para criptografar transferências de dados)|Sim|Sim| |  
|Instalação do cliente|Sim| | |  
|Suporte pela Internet|Sim| | |  
|Descoberta|Sim| |Sim|  
|Inventário de hardware|Sim|Sim|Sim|  
|Inventário de software|Sim| |Sim|  
|Configurações|Sim|Sim|Sim|  
|Implantação de software|Sim|Sim| |  
|Monitor com ponto de status de fallback|Sim| | |  
|Conexões para pontos de gerenciamento|Sim|Sim| |  
|Conexões para pontos de distribuição|Sim|Sim| |  
|Bloqueio do Configuration Manager|Sim|Sim| |  
|Quarentena e bloqueio do Exchange Server (e Configuration Manager)| | |Sim|  
|Apagamento remoto| |Sim|Sim|  


