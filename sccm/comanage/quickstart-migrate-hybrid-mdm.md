---
title: Migrar do MDM híbrido
titleSuffix: Configuration Manager
description: Como o MDM híbrido está preterido, o Intune autônomo é necessário para o cogerenciamento.
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
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754559"
---
# <a name="migrate-from-hybrid-mdm-for-co-management"></a>Migrar do MDM híbrido para o cogerenciamento

O gerenciamento híbrido de dispositivos móveis (MDM) é um recurso preterido. O suporte para MDM híbrido termina em 1º de setembro de 2019. Para saber mais, confira [MDM híbrido com o Configuration Manager e o Microsoft Intune](/sccm/mdm/understand/hybrid-mobile-device-management).

O Intune autônomo é a topologia de implantação recomendada e é necessário para o cogerenciamento. Se você quiser habilitar o cogerenciamento, migre de uma configuração híbrida do Intune para o Intune autônomo. 

No vídeo a seguir, o gerente de programas principal Andrew McMurray e o gerente de marketing de produtos sênior Mayunk Jain discutem e demonstram a migração do MDM híbrido:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Moving-From-Hybrid-MDM-To-Microsoft-Intune/player]



## <a name="how-to-do-it"></a>Como fazer isso

A migração para o Intune autônomo será mais bem-sucedida com o uso de uma abordagem em fases. Com a migração em fases, você move um pequeno subconjunto de usuários e dispositivos, enquanto a maioria de seus usuários e dispositivos ainda é gerenciada com o MDM híbrido. Depois de confirmar que a migração foi bem-sucedida, você pode começar a migrar mais recursos para o Intune.

Para começar a migração, use a [ferramenta Importador de Dados do Microsoft Intune](/sccm/mdm/deploy-use/migrate-import-data) para coletar e automatizar o processo de recriação dos objetos do Configuration Manager em seu locatário do Intune autônomo. Em seguida, altere sua autoridade do MDM para um conjunto específico de usuários e teste a funcionalidade no Intune autônomo. Quando essa verificação for concluída, altere sua autoridade do MDM para o Intune autônomo para todos os usuários.

> [!Important]  
> Se você está usando o acesso condicional local no Configuration Manager, essa funcionalidade atualmente requer o Intune híbrido.  

Para saber mais sobre esse processo de migração, confira [Migrar usuários e dispositivos do MDM híbrido para o Intune autônomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).



## <a name="case-studies"></a>Estudos de caso

Recentemente, a TI da Microsoft transferiu 130.000 usuários do Intune híbrido para o Intune autônomo em três meses. Para saber mais, confira [Como a Microsoft usa o acesso condicional – zona de ponto de extremidade 1812](https://youtu.be/offk-KH7eIA?t=651). Este vídeo é uma conversa entre o vice-presidente corporativo da Microsoft, Brad Anderson, e o chefe de segurança de informações da Microsoft, Bret Arsenault, que supervisionou pessoalmente a migração. 

Uma grande empresa farmacêutica transferiu 10.000 usuários do Intune híbrido para o Intune autônomo dentro de algumas semanas.

Uma grande empresa de consultoria de TI na Índia migrou 40.000 usuários do Intune híbrido para o Intune autônomo em menos de um mês.



## <a name="contact-fasttrack"></a>Entre em contato com o FastTrack

Se você precisar de ajuda para migrar do MDM híbrido em qualquer ponto do processo, acesse o [Microsoft FastTrack](https://Microsoft.com/FastTrack/), entre e solicite assistência. 

Para saber mais, confira [Obter ajuda do FastTrack](/sccm/comanage/quickstart-fasttrack). 

