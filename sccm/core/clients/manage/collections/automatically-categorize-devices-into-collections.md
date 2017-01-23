---
title: "Categorizar automaticamente dispositivos em coleções | Microsoft Docs"
description: "Categorize os dispositivos em coleções com o System Center Configuration Manager."
ms.custom: na
ms.date: 01/07/2016
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
ms.sourcegitcommit: 05c27c7aa36e0b4236867766dab36125c31467b3
ms.openlocfilehash: b1bac05e9335dd757b8f499f97daea24e0f4acbd

---
# <a name="automatically-categorize-devices-into-collections-with-system-center-configuration-manager"></a>Categorizar dispositivos em coleções automaticamente com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode criar categorias de dispositivos, que podem ser usadas para colocar automaticamente os dispositivos em coleções de dispositivos ao usar o Configuration Manager com o Microsoft Intune. Em seguida, os usuários devem escolher uma categoria de dispositivo ao registrar um dispositivo no Intune. É possível alterar uma categoria de dispositivo no console do Configuration Manager.

> [!IMPORTANT]  
    >  Essa funcionalidade funciona com a versão de **junho de 2016** e posterior do Microsoft Intune. Verifique se você atualizou para essa versão antes de experimentar esses procedimentos.

## <a name="create-device-categories"></a>Criar categorias de dispositivos

1.  Acesse **Ativos e Conformidade** > **Visão Geral** > **Coleções de Dispositivos**.
2.  Na guia **Início**, no grupo **Coleções de Dispositivos**, escolha **Gerenciar Categorias de Dispositivo**.
3.  Crie, edite ou remova categorias.

## <a name="associate-a-collection-with-a-device-category"></a>Associar uma coleção a uma categoria de dispositivos

Quando você associar uma coleção a uma categoria de dispositivo, todos os dispositivos dessa categoria serão adicionados à coleção. Não é possível adicionar uma regra de categoria de dispositivo a uma coleção interna como **Todos os Sistemas**.

1.  Na guia **Regras de Associação** da caixa de diálogo **Propriedades** de uma coleção de dispositivos, escolha **Adicionar Regra** > **Regra de Categoria de Dispositivo**.
2.  Na caixa de diálogo **Selecionar Categorias de Dispositivos**, selecione uma ou mais categorias de dispositivos que será aplicada a todos os dispositivos na coleção.

## <a name="change-the-category-of-a-device"></a>Alterar a categoria de um dispositivo

1.  Em **Ativos e Conformidade** > **Visão Geral** > **Dispositivos**, selecione um dispositivo na lista **Dispositivos**.
2.  Na guia **Início**, no grupo **Dispositivo**, escolha **Alterar Categoria**.
3.  Escolha uma categoria e, em seguida, **OK**.

## <a name="view-which-category-a-device-belongs-to"></a>Exibir a qual categoria um dispositivo pertence

Em **Ativos e Conformidade** > **Visão Geral** > **Dispositivos**, na lista **Dispositivos**, a categoria é exibida na coluna **Categoria de Dispositivo**.

Se a coluna **Categoria do Dispositivo** não for exibida, clique com o botão direito do mouse no título de uma das colunas na lista **Dispositivos** (como **Nome**) e selecione **Categoria do Dispositivo**.

Se você atribuir um dispositivo a uma categoria e depois excluir a categoria, o relatório **Lista de Dispositivos registrados por usuário no Microsoft Intune** exibirá um GUID na coluna **Categoria do Dispositivo**, em vez de um nome de categoria.



<!--HONumber=Jan17_HO1-->


