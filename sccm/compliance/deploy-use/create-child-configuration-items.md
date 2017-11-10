---
title: "Criar itens de configuração filho"
titleSuffix: Configuration Manager
description: "Crie itens de configuração filho no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: c1a59bbedbe157c491800064ba54079c4a980b04
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-create-child-configuration-items-in-system-center-configuration-manager"></a>Como criar itens de configuração filho no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os itens de configuração filho no System Center Configuration Manager são cópias dos itens de configuração que mantêm uma relação com o item de configuração original, portanto, eles herdam a configuração original do item de configuração pai.  

Quando você vê as propriedades de um item de configuração filho no console do Configuration Manager, não é possível editar os objetos herdados e as configurações com seus critérios de validação. No entanto, você pode adicionar e editar critérios de validação adicionais para o item de configuração filho e também pode adicionar novos objetos e configurações a ele.
A finalidade comum para criar e editar um item de configuração filho é refinar o item de configuração original para atender às suas necessidades comerciais.  

> [!NOTE]  
>  Só é possível criar itens de configuração filho por meio de itens de configuração do tipo **Windows Desktops e Servers (personalizados)**.  

## <a name="to-create-a-child-configuration-item"></a>Para criar um item de configuração filho  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Itens de Configuração**.  

3.  Na lista **Itens de Configuração** , selecione o item de configuração para o qual deseja criar um item de configuração filho e, na guia **Início** , no grupo **Item de Configuração** , clique em **Criar Item de Configuração Filho**.  

4.  Na página **Geral** do **Assistente para Criar Item de Configuração Filho**, você pode escolher uma revisão específica do item de configuração pai a ser usada para criar o filho. As outras etapas deste assistente são idênticas às que você usaria para criar um item de configuração padrão. Para mais informações, consulte [Como criar itens de configuração personalizados para computadores desktop e de servidor com Windows](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md).  

5.  Conclua o assistente. O novo item de configuração filho é exibido na lista **Itens de Configuração** .  
