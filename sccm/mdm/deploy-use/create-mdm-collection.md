---
title: Criar uma coleção de MDM
titleSuffix: Configuration Manager
description: Crie uma coleção de MDM usando o System Center Configuration Manager.
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: d1b4337f-85e8-45e6-8bbe-9f18b49041c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3ec7c4cd58fbb717ab586d355ba4f0bf5f91fd06
ms.sourcegitcommit: ec4411fe30770f90128cf6cbd181047db90040cb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/14/2019
ms.locfileid: "57881649"
---
# <a name="create-an-mdm-collection-with-system-center-configuration-manager-and-microsoft-intune"></a>Criar uma coleção de MDM usando o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

É necessária uma coleção de usuários do Configuration Manager para especificar os usuários que podem registrar dispositivos no gerenciamento. Você pode usar apenas coleções de usuário (em vez de coleções de dispositivos) porque as licenças do Intune são atribuídas por usuário.

> [!NOTE]
> Para registrar dispositivos com o Intune, você não precisa atribuir licenças aos usuários no Centro de administração do Microsoft 365 ou portal do Azure Active Directory. Incluir os usuários em uma coleção que é associada à assinatura do Intune (em uma [etapa posterior](configure-intune-subscription.md)) é tudo o que é necessário.

Para fins de teste você pode configurar uma **regra direta** e adicionar usuários específicos que podem registrar dispositivos. No console do Configuration Manager, escolha **Ativos e Conformidade** > **Coleções de Usuários**, clique na guia **Página Inicial** > grupo **Criar** e clique em **Criar Coleção do Usuário**. Para uma distribuição mais ampla, você deve usar **Regras de consulta** para definir usuários. Para obter mais informações sobre coleções, confira [Como criar coleções](https://technet.microsoft.com/library/mt629371.aspx).

![Criar uma coleção de usuários para MDM](../media/mdm-create-user-collection.png)

> [!div class="button"]
> [Próxima etapa >](confirm-dns.md)
