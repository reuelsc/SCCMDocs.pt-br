---
title: Criar uma coleção de MDM
titleSuffix: Configuration Manager
description: Crie uma coleção de MDM usando o System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: d1b4337f-85e8-45e6-8bbe-9f18b49041c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8aba9fb658072ce4eaa2e4b2a364cf2b52f9c51b
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53414643"
---
# <a name="create-an-mdm-collection-with-system-center-configuration-manager-and-microsoft-intune"></a>Criar uma coleção de MDM usando o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch atual)*

É necessária uma coleção de usuários do Configuration Manager para especificar os usuários que podem registrar dispositivos no gerenciamento. Você pode usar apenas coleções de usuário (em vez de coleções de dispositivos) porque as licenças do Intune são atribuídas por usuário.

> [!NOTE]
> Para registrar dispositivos com o Intune, você não precisa atribuir licenças a usuários no portal do Office 365 ou Portal do Azure Active Directory. Incluir os usuários em uma coleção que é associada à assinatura do Intune (em uma [etapa posterior](configure-intune-subscription.md)) é tudo o que é necessário.

Para fins de teste você pode configurar uma **regra direta** e adicionar usuários específicos que podem registrar dispositivos. No console do Configuration Manager, escolha **Ativos e Conformidade** > **Coleções de Usuários**, clique na guia **Página Inicial** > grupo **Criar** e clique em **Criar Coleção do Usuário**. Para uma distribuição mais ampla, você deve usar **Regras de consulta** para definir usuários. Para obter mais informações sobre coleções, confira [Como criar coleções](https://technet.microsoft.com/library/mt629371.aspx).

![Criar uma coleção de usuários para MDM](../media/mdm-create-user-collection.png)

> [!div class="button"]
> [Próxima etapa >](confirm-dns.md)
