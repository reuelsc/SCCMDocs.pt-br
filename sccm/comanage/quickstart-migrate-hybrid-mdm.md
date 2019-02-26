---
title: Migrar do MDM híbrido
titleSuffix: Configuration Manager
description: MDM híbrido é preterido, o Intune autônomo é necessário para o cogerenciamento.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 456f32d5-8590-499f-a54d-d00618bc61f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 84625c12c9cac643fe5a895c066632f44ffeacdc
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754559"
---
# <a name="migrate-from-hybrid-mdm-for-co-management"></a>Migrar do MDM híbrido para o cogerenciamento

Gerenciamento de dispositivo móvel (MDM) híbrido é um recurso preterido. Suporte para MDM híbrido termina em 1 de setembro de 2019. Para obter mais informações, consulte [MDM híbrido com o Configuration Manager e o Microsoft Intune](/sccm/mdm/understand/hybrid-mobile-device-management).

Intune autônomo é a topologia de implantação recomendada e é necessário para o cogerenciamento. Se você quiser habilitar o cogerenciamento, migre de uma configuração híbrida do Intune para o Intune autônomo. 

No vídeo a seguir, gerente de programa principal Andrew McMurray e gerente de marketing de produto sênior Mayunk Jain discutem e migração do MDM híbrido de demonstração:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Moving-From-Hybrid-MDM-To-Microsoft-Intune/player]



## <a name="how-to-do-it"></a>Como fazer isso

A migração para o Intune autônomo será mais bem-sucedidas quando usar uma abordagem em fases. Com uma migração em fases, mover um pequeno subconjunto de usuários e dispositivos enquanto a maioria dos usuários e dispositivos ainda é gerenciada com o MDM híbrido. Depois de confirmar que a migração seja bem-sucedida, você pode começar a migração de mais recursos para o Intune.

Para começar a migração, use o [ferramenta importador de dados do Microsoft Intune](/sccm/mdm/deploy-use/migrate-import-data) para coletar e automatizar o processo de recriar os objetos do Configuration Manager em seu locatário do Intune autônomo. Em seguida, alterar sua autoridade MDM para um conjunto específico de usuários e testar a funcionalidade no Intune autônomo. Quando essa verificação é feita, altere sua autoridade MDM para o Intune autônomo para todos os usuários.

> [!Important]  
> Se você estiver usando o acesso condicional local no Configuration Manager, essa funcionalidade requer atualmente Intune híbrido.  

Para obter mais informações sobre esse processo de migração, consulte [migrar dispositivos e usuários do MDM híbrido para Intune autônomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).



## <a name="case-studies"></a>Estudos de caso

Microsoft IT recentemente movido 130.000 usuários do Intune híbrido para Intune autônomo em três meses. Para obter mais informações, consulte [como a Microsoft usa o acesso condicional – 1812 de zona do ponto de extremidade](https://youtu.be/offk-KH7eIA?t=651). Este vídeo é uma conversa entre Microsoft vice-presidente corporativo Brad Anderson e executivo de segurança de informações-chefe da Microsoft Bret Arsenault, que pessoalmente supervisionava a migração. 

Uma grande empresa farmacêutica movido 10.000 usuários do Intune híbrido para Intune autônomo dentro de algumas semanas.

Uma grande empresa de consultoria de IT na Índia 40.000 usuários migrados do Intune híbrido para Intune autônomo em menos de um mês.



## <a name="contact-fasttrack"></a>Entre em contato com o FastTrack

Se precisar de assistência de migração do MDM híbrido em qualquer ponto no processo, acesse [Microsoft FastTrack](https://Microsoft.com/FastTrack/), entrar e solicitar assistência. 

Para obter mais informações, consulte [Obtenha ajuda do FastTrack](/sccm/comanage/quickstart-fasttrack). 

