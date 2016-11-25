---
title: "Categorizar dispositivos em coleções automaticamente | System Center Configuration Manager"
description: "Categorize os dispositivos em coleções com o System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 6e1e8c1da1209be03d4a1377dcc0c9ce9478a216

---
# <a name="automatically-categorize-devices-into-collections-with-system-center-configuration-manager"></a>Categorizar dispositivos em coleções automaticamente com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode criar categorias de dispositivos, que podem ser usadas para colocar automaticamente os dispositivos em coleções de dispositivos ao usar o Configuration Manager com o Microsoft Intune. Os usuários devem, então, escolher uma categoria de dispositivo ao registrar um dispositivo no Intune. Além disso, você pode alterar a categoria de um dispositivo do console do Configuration Manager.

> [!IMPORTANT]  
    >  Essa funcionalidade funciona com a versão de **junho de 2016** do Microsoft Intune. Verifique se você atualizou para essa versão antes de experimentar esses procedimentos.

## <a name="create-device-categories"></a>Criar categorias de dispositivos

1.  No espaço de trabalho **Ativos e Conformidade** do console do Configuration Manager, expanda **Visão Geral** e clique em **Coleções de Dispositivos**.
2.  Na guia **Início**, no grupo **Coleções de Dispositivos**, clique em **Gerenciar Categorias de Dispositivo**.
3.  Na caixa de diálogo **Gerenciar Categorias de Dispositivo**, você pode criar, editar ou remover categorias.

## <a name="associate-a-collection-with-a-device-category"></a>Associar uma coleção a uma categoria de dispositivos

Quando você associa uma coleção a uma categoria de dispositivos, todos os dispositivos na categoria especificada serão adicionados à coleção.

> [!IMPORTANT]  
    >  Não é possível adicionar uma regra de categoria de dispositivo a uma coleção interna como **Todos os Sistemas**.

1.  Na caixa de diálogo **Regras de Associação** da caixa de diálogo **Propriedades** de uma coleção de dispositivos, clique em **Adicionar Regra** > **Regra de Categoria de Dispositivo**.
2.  Na caixa de diálogo **Selecionar Categorias de Dispositivos**, selecione uma ou mais categorias de dispositivos que será aplicada a todos os dispositivos na coleção.
3.  Feche a caixa de diálogo **Selecionar Categoria de Dispositivos** e a caixa de diálogo de propriedades da coleção.


## <a name="change-the-category-of-a-device"></a>Alterar a categoria de um dispositivo

1.  No espaço de trabalho **Ativos e Conformidade** do console do Configuration Manager, expanda **Visão Geral** e clique em **Dispositivos**.
2.  Selecione um dispositivo na lista **Dispositivos** e, na guia **Início**, no grupo **Dispositivo**, clique em **Alterar Categoria**.
3.  Na caixa de diálogo **Editar Categoria de Dispositivo**, selecione a categoria a ser aplicada a esse dispositivo e clique em **OK**.

## <a name="view-which-category-a-device-belongs-to"></a>Exibir a qual categoria um dispositivo pertence

1.  No espaço de trabalho **Ativos e Conformidade** do console do Configuration Manager, expanda **Visão Geral** e clique em **Dispositivos**.
2.  Na lista **Dispositivos**, a categoria é exibida na coluna **Categoria do Dispositivo**.
> [!TIP]  
    >  Se a coluna **Categoria do Dispositivo** não for exibida, clique com o botão direito do mouse no título de uma das colunas na lista **Dispositivos** (como **Nome**) e selecione **Categoria do Dispositivo**.

Se você atribuir um dispositivo a uma categoria e depois excluir a categoria, o relatório **Lista de Dispositivos registrados por usuário no Microsoft Intune** exibirá um GUID na coluna **Categoria do Dispositivo**, em vez de um nome de categoria.



<!--HONumber=Nov16_HO1-->


