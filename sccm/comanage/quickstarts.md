---
title: Conectar-se com o cogerenciamento em nuvem
titleSuffix: Configuration Manager
description: O cogerenciamento oferece valor imediato quando você o habilita.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8d878443-90e7-46e4-9cd3-99e2a19b2ad0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed92d6249e4459f1902f639840b142977994df9e
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754557"
---
# <a name="cloud-connecting-with-co-management"></a>Conectar-se com o cogerenciamento em nuvem

![Banner da série Blastoff](media/blastoff-banner.png)

O cogerenciamento adiciona novas funcionalidades à sua implantação do Configuration Manager, sem alterar o modo como você já trabalha. Ao habilitar o cogerenciamento, você começa a se beneficiar imediatamente da nuvem. Você pode aplicar esse valor à sua infraestrutura e aos processos de gerenciamento existentes.

Nesta série de guias de Início Rápido sobre cogerenciamento, veja como é possível gerar rapidamente um novo valor de gerenciamento. O cogerenciamento foi desenvolvido para criar recursos e ferramentas que você pode usar imediatamente.


No vídeo a seguir, o vice-presidente corporativo da Microsoft, Brad Anderson, apresenta esta série sobre cogerenciamento:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Cloud-Connecting-with-Co-Management/player]


| Valor imediato | Introdução |
|-----------------|-----------------|
| - [Acesso condicional](#bkmk_ca)<br> - [Ações remotas do Intune](#bkmk_remote)<br> - [Integridade do cliente](#bkmk_client-health)<br> - [Azure AD híbrido](#bkmk_hybrid-aad)<br> - [Windows Autopilot](#bkmk_autopilot) | - [Caminhos para o cogerenciamento](#bkmk_paths)<br> - [Configurar o Azure AD híbrido](#bkmk_setup-hybrid-aad)<br> - [Atualizar para o Windows 10](#bkmk_upgrade-win10)<br> - [Migrar do MDM híbrido](#bkmk_migrate-hybrid-mdm)<br> - [Obter ajuda do FastTrack](#bkmk_fasttrack) | 



## <a name="immediate-value"></a>Valor imediato

| | | |
|-|-|-|
| <a name="bkmk_ca"></a>**Acesso condicional com conformidade do dispositivo** | Controlar o acesso dos usuários a recursos corporativos com base nas regras de conformidade do Intune | [![Miniatura do vídeo sobre acesso condicional](media/thumbnail-conditional-access.png)](/sccm/comanage/quickstart-conditional-access) |
| <a name="bkmk_remote"></a>**Ações remotas do Intune** | Execute ações remotas do Intune para dispositivos cogerenciados. Por exemplo, apagar e redefinir um dispositivo e fazer a manutenção do registro e da conta | [![Miniatura do vídeo sobre ações remotas](media/thumbnail-remote-action.png)](/sccm/comanage/quickstart-remote-actions) |
| <a name="bkmk_client-health"></a>**Integridade do cliente do Configuration Manager** | Manter a visibilidade da integridade do cliente do Configuration Manager a partir do Intune no portal do Azure | [![Miniatura do vídeo sobre integridade do cliente](media/thumbnail-client-health.png)](/sccm/comanage/quickstart-client-health) |
| <a name="bkmk_hybrid-aad"></a>**Azure Active Directory (Azure AD)** | Com o Azure AD, você pode tirar proveito de mais produtividade para seus usuários e segurança para seus recursos, em ambientes de nuvem e locais | [![Miniatura do vídeo sobre Azure AD híbrido](media/thumbnail-azure-ad.png)](/sccm/comanage/quickstart-hybrid-aad) |
| <a name="bkmk_autopilot"></a>**Windows Autopilot** | Reduza o tempo, os recursos e a complexidade associados à implantação, ao gerenciamento, à desativação e à reciclagem de dispositivos. O Autopilot também cria uma experiência melhor para os usuários finais. | [![Miniatura do vídeo sobre Windows Autopilot](media/thumbnail-autopilot.png)](/sccm/comanage/quickstart-autopilot) |



## <a name="getting-started"></a>Introdução

Se você quer habilitar o cogerenciamento, comece aqui para abordar as questões técnicas que podem ocorrer.

| | | |
|-|-|-|
| <a name="bkmk_paths"></a>**Caminhos para o cogerenciamento** | Há duas maneiras principais de configurar o cogerenciamento, e é importante entender os pré-requisitos de cada caminho.  Cada caminho requer alguma combinação de cliente do Azure AD, ConfigMgr, Intune e Windows. | [![Miniatura do slide sobre caminhos de cogerenciamento](media/thumbnail-paths.png)](/sccm/comanage/quickstart-paths) |
| <a name="bkmk_setup-hybrid-aad"></a>**Configurar o Azure AD híbrido** | Se o seu ambiente tem dispositivos Windows 10 ingressados no domínio, configure o Azure AD híbrido antes de habilitar o cogerenciamento | [![Miniatura do vídeo sobre a configuração do Azure AD híbrido](media/thumbnail-setup-azure-ad.png)](/sccm/comanage/quickstart-setup-hybrid-aad) |
| <a name="bkmk_upgrade-win10"></a>**Atualizar para o Windows 10** | É necessário ter o Windows 10 versão 1709 ou posterior para usar o cogerenciamento | [![Miniatura do vídeo sobre a atualização do Windows 10](media/thumbnail-upgrade-win10.png)](/sccm/comanage/quickstart-upgrade-win10) |
| <a name="bkmk_migrate-hybrid-mdm"></a>**Migrar do MDM híbrido** | O MDM híbrido (Intune integrado com o Configuration Manager) está preterido. O Intune autônomo é necessário para o cogerenciamento. | [![Miniatura do vídeo sobre a migração do MDM híbrido](media/thumbnail-migrate-hybrid-mdm.png)](/sccm/comanage/quickstart-migrate-hybrid-mdm) |
| <a name="bkmk_fasttrack"></a>**Obter ajuda do FastTrack** | A organização do FastTrack é um grande grupo de engenheiros da Microsoft especializados em ajudar todos os tipos de organizações a implantar o Microsoft 365, incluindo a configuração do coegerenciamento. | [![Miniatura do vídeo sobre o FastTrack](media/thumbnail-fasttrack.png)](/sccm/comanage/quickstart-fasttrack) |

