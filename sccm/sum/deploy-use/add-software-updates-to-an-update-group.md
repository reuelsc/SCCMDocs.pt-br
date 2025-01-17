---
title: 'Adicionar atualizações a um grupo de atualização '
titleSuffix: Configuration Manager
description: Adicione atualizações de software manualmente ou automaticamente a um grupo de atualização de software no seu ambiente.
ms.date: 03/18/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a0767664-fd60-46a8-9da5-86cc431ce53c
manager: dougeby
author: mestew
ms.author: mstewart
ms.collection: M365-identity-device-management
ms.openlocfilehash: b207d0c210aa25489d67a5a551bf795e86c1582b
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500240"
---
# <a name="add-software-updates-to-an-update-group"></a>Adicionar atualizações de software a um grupo de atualização  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Os grupos de atualização de software fornecem um método eficaz para organizar as atualizações de software em seu ambiente. É possível adicionar atualizações de software manual ou automaticamente a um grupo de atualização de software usando uma ADR. Além disso, é possível implantar um grupo de atualização de software manual ou automaticamente usando uma ADR. Depois de implantar um grupo de atualização de software, você pode adicionar novas atualizações de software ao grupo e o Configuration Manager as implantará automaticamente. Use os procedimentos a seguir para adicionar atualizações de software a um grupo de atualização de software novo ou existente.  

#### <a name="to-add-software-updates-to-a-new-software-update-group"></a>Para adicionar atualizações de software a um novo grupo de atualização de software  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No workspace Biblioteca de Software, expanda **Atualizações de Software** e clique em **Todas as Atualizações de Software**.  

3.  Selecione as atualizações de software a serem adicionadas ao novo grupo de atualização de software.  

4.  Na guia **Início** , no grupo **Atualizar** , clique em **Criar Grupo de Atualização de Software**.  

5.  Especifique o nome do grupo de atualização de software e, opcionalmente, forneça uma descrição. Use o nome e a descrição que fornece informações suficientes para que você determine qual tipo de atualizações de software está no grupo de atualização de software. Para continuar, clique em **Criar**.  

6.  Clique em **Grupos de Atualização de Software** para exibir o novo grupo de atualização de software.  

7.  Selecione o grupo de atualização de software e, na guia **Início** , no grupo **Atualizar** , clique em **Mostrar Membros** para exibir uma lista de atualizações de software que estão incluídas no grupo.  

#### <a name="to-add-software-updates-to-an-existing-software-update-group"></a>Para adicionar atualizações de software a um grupo de atualização de software existente  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No workspace Biblioteca de Software, expanda **Atualizações de Software** e clique em **Todas as Atualizações de Software**.  

3.  Selecione as atualizações de software que deseja adicionar ao novo grupo de atualização de software.  

    > [!NOTE]  
    >  No nó **Todas as Atualizações de Software**, o Configuration Manager exibe todas as atualizações, exceto aquelas na classificação **Atualizações** e na classificação do produto **Cliente Office 365**.  

4.  Na guia **Início** , no grupo **Atualizar** , clique em **Editar Associação**.  

5.  Selecione o grupo de atualização de software ao qual você deseja adicionar as atualizações de software.  

6.  Clique no nó **Grupos de Atualização de Software** para exibir o grupo de atualização de software.  

7.  Selecione o grupo de atualização de software e, na guia **Início** , no grupo **Atualizar** , clique em **Mostrar Membros** para exibir uma lista de atualizações de software que estão incluídas no grupo de atualização de software.  
