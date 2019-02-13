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
ms.collection: M365-identity-device-management
ms.openlocfilehash: f0288b88187ead39f1cf584ebf88e3943549b01f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124005"
---
# <a name="create-an-mdm-collection-with-system-center-configuration-manager-and-microsoft-intune"></a>Criar uma coleção de MDM usando o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

É necessária uma coleção de usuários do Configuration Manager para especificar os usuários que podem registrar dispositivos no gerenciamento. Você pode usar apenas coleções de usuário (em vez de coleções de dispositivos) porque as licenças do Intune são atribuídas por usuário.

> [!NOTE]
> Para registrar dispositivos com o Intune, você não precisa atribuir licenças a usuários no portal do Office 365 ou Portal do Azure Active Directory. Incluir os usuários em uma coleção que é associada à assinatura do Intune (em uma [etapa posterior](configure-intune-subscription.md)) é tudo o que é necessário.

Para fins de teste você pode configurar uma **regra direta** e adicionar usuários específicos que podem registrar dispositivos. No console do Configuration Manager, escolha **Ativos e Conformidade** > **Coleções de Usuários**, clique na guia **Página Inicial** > grupo **Criar** e clique em **Criar Coleção do Usuário**. Para uma distribuição mais ampla, você deve usar **Regras de consulta** para definir usuários. Para obter mais informações sobre coleções, confira [Como criar coleções](https://technet.microsoft.com/library/mt629371.aspx).

![Criar uma coleção de usuários para MDM](../media/mdm-create-user-collection.png)

> [!div class="button"]
> [Próxima etapa >](confirm-dns.md)
