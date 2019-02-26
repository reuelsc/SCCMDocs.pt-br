---
title: Conectar-se com o cogerenciamento em nuvem
titleSuffix: Configuration Manager
description: Cogerenciamento oferece valor imediato, quando você habilitá-lo.
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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754557"
---
# <a name="cloud-connecting-with-co-management"></a>Conectar-se com o cogerenciamento em nuvem

![Faixa da série blastoff](media/blastoff-banner.png)

Cogerenciamento adiciona nova funcionalidade à sua implantação existente do Configuration Manager, sem alterar a forma como você já trabalha. Quando você habilita o cogerenciamento, você começar imediatamente se beneficia da nuvem. Você pode aplicar esse valor para seus processos e a infraestrutura de gerenciamento existente.

Nesta série de início rápido de cogerenciamento, consulte como você pode manter rapidamente o novo valor de gerenciamento. Cogerenciamento é compilado para criar recursos e ferramentas que você pode usar no momento.


No vídeo a seguir, a Microsoft vice-presidente corporativo, Brad Anderson, apresenta esta série de cogerenciamento:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Cloud-Connecting-with-Co-Management/player]


| Valor imediato | Introdução |
|-----------------|-----------------|
| - [Acesso condicional](#bkmk_ca)<br> - [Ações remotas do Intune](#bkmk_remote)<br> - [Integridade do cliente](#bkmk_client-health)<br> - [Azure AD híbrido](#bkmk_hybrid-aad)<br> - [Windows Autopilot](#bkmk_autopilot) | - [Caminhos para cogerenciamento](#bkmk_paths)<br> - [Configurar o Azure AD híbrido](#bkmk_setup-hybrid-aad)<br> - [Atualizar para o Windows 10](#bkmk_upgrade-win10)<br> - [Migrar do MDM híbrido](#bkmk_migrate-hybrid-mdm)<br> - [Obtenha ajuda do FastTrack](#bkmk_fasttrack) | 



## <a name="immediate-value"></a>Valor imediato

| | | |
|-|-|-|
| <a name="bkmk_ca"></a>**Acesso condicional com a conformidade do dispositivo** | Controlar o acesso do usuário aos recursos corporativos com base nas regras de conformidade do Intune | [![Miniatura de vídeo de acesso condicional](media/thumbnail-conditional-access.png)](/sccm/comanage/quickstart-conditional-access) |
| <a name="bkmk_remote"></a>**Ações remotas do Intune** | Execute ações remotas do Intune para dispositivos cogerenciados. Por exemplo, apagar e redefinir um dispositivo e manter o registro e conta | [![Miniatura de vídeo de ações remota](media/thumbnail-remote-action.png)](/sccm/comanage/quickstart-remote-actions) |
| <a name="bkmk_client-health"></a>**Integridade do cliente do Configuration Manager** | Manter a visibilidade da integridade do cliente do Configuration Manager do Intune no portal do Azure | [![Miniatura de vídeo de integridade do cliente](media/thumbnail-client-health.png)](/sccm/comanage/quickstart-client-health) |
| <a name="bkmk_hybrid-aad"></a>**Azure Active Directory (AD do Azure)** | Com o Azure AD você pode tirar proveito de maior produtividade para seus usuários e segurança para seus recursos, em ambientes de nuvem e local | [![Miniatura de vídeo do Azure AD híbrido](media/thumbnail-azure-ad.png)](/sccm/comanage/quickstart-hybrid-aad) |
| <a name="bkmk_autopilot"></a>**Windows Autopilot** | Reduza tempo, recursos e complexidade associada ao implantar, gerenciar e desativando ou reciclagem de dispositivos. Piloto automático também cria uma melhor experiência para os usuários finais. | [![Miniatura de vídeo do Windows Autopilot](media/thumbnail-autopilot.png)](/sccm/comanage/quickstart-autopilot) |



## <a name="getting-started"></a>Introdução

Se você quiser habilitar o cogerenciamento, comece aqui para desbloquear as questões técnicas que você pode ter.

| | | |
|-|-|-|
| <a name="bkmk_paths"></a>**Caminhos para cogerenciamento** | Há duas maneiras principais para configurar o cogerenciamento e é importante entender os pré-requisitos para cada caminho.  Cada caminho requer alguma combinação do Azure AD, cliente do ConfigMgr, o Intune e Windows. | [![Miniatura de slide de caminhos de cogerenciamento](media/thumbnail-paths.png)](/sccm/comanage/quickstart-paths) |
| <a name="bkmk_setup-hybrid-aad"></a>**Configurar o Azure AD híbrido** | Se seu ambiente tiver atualmente os dispositivos Windows 10 ingressados no domínio, configurar híbrido do Azure AD antes de habilitar o cogerenciamento | [![Miniatura de híbrido do Azure AD configurar o vídeo](media/thumbnail-setup-azure-ad.png)](/sccm/comanage/quickstart-setup-hybrid-aad) |
| <a name="bkmk_upgrade-win10"></a>**Atualizar para o Windows 10** | Windows 10 versão 1709 ou posterior é necessário para o cogerenciamento | [![Miniatura de vídeo do Windows 10 atualização](media/thumbnail-upgrade-win10.png)](/sccm/comanage/quickstart-upgrade-win10) |
| <a name="bkmk_migrate-hybrid-mdm"></a>**Migrar do MDM híbrido** | MDM híbrido (Intune integrado com o Configuration Manager) foi preterido. Intune autônomo é necessário para o cogerenciamento. | [![Migrar de miniatura de vídeo do MDM híbrido](media/thumbnail-migrate-hybrid-mdm.png)](/sccm/comanage/quickstart-migrate-hybrid-mdm) |
| <a name="bkmk_fasttrack"></a>**Obtenha ajuda do FastTrack** | A organização do FastTrack é um grande grupo de engenheiros da Microsoft que são especializados em ajudar todos os tipos de organizações implantar aplicativos do Microsoft 365, incluindo a configuração de cogerenciamento. | [![Miniatura de vídeo do FastTrack](media/thumbnail-fasttrack.png)](/sccm/comanage/quickstart-fasttrack) |

