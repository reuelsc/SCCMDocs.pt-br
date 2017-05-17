---
title: "Configurar o inventário de software | Microsoft Docs"
description: "Configurar o inventário de software e excluir pastas do inventário de software no Configuration Manager."
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
caps.latest.revision: 5
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dacfdf02f04c6bd731ca0fc11e5af371b409c8b4
ms.openlocfilehash: 1cee12d6f9c406e2438a3ed76674c3498fe9abbd
ms.contentlocale: pt-br
ms.lasthandoff: 01/03/2017


---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>Como configurar o inventário de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Este procedimento define as configurações do cliente para o inventário de software e se aplica a todos os computadores em sua hierarquia. Se você quiser aplicar essas configurações somente a alguns computadores, crie uma configuração personalizada do cliente de dispositivo e atribua a uma coleção que contém os computadores nos quais deseja usar o inventário de software. Para obter mais informações sobre como criar configurações personalizadas de dispositivo, consulte [Como configurar as definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

## <a name="to-configure-software-inventory"></a>Para configurar o inventário de software  

1.  No console do Configuration Manager, clique em **Administração** > **Configurações do Cliente****Configurações do Cliente Padrão**.  

4.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

5.  Na caixa de diálogo **Configurações Padrão**, escolha **Inventário de Software**.  

6.  Na lista **Configurações do Dispositivo** , configure os seguintes valores:  

    -   **Habilitar inventário de software em clientes** – Na lista suspensa, selecione **Verdadeiro**.  

    -   **Programar agendamento do inventário de software e da coleção de arquivos** – Configura o intervalo no qual os clientes coletam inventário de software e arquivos.   

7.  Defina as configurações do cliente necessárias. Para obter uma lista de configurações do cliente de inventário de software que podem ser definidas, veja a seção [Inventário de Software](../../../../core/clients/deploy/about-client-settings.md#software-inventory) no tópico [Sobre configurações de cliente no System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).  

 Os computadores cliente serão definidos com essas configurações durante o próximo download da política do cliente. Para iniciar a recuperação de política para um cliente individual, veja [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  


## <a name="to-exclude-folders-from-software-inventory"></a>Para excluir pastas do inventário de software  

1.  Usando o Notepad.exe, crie um arquivo vazio chamado **Skpswi.dat**.  

2.  Clique com o botão direito do mouse no arquivo do **Skpswi.dat** e clique em **Propriedades**. Nas propriedades do arquivo Skpswi.dat, selecione o atributo **Hidden** .  

3.  Coloque o arquivo **Skpswi.dat** na raiz de cada estrutura de pasta ou da unidade de disco rígido do cliente que você deseja excluir do inventário de software.  

> [!NOTE]  
>  O inventário de software não realizará o inventário da unidade do cliente novamente, a menos que esse arquivo seja excluído da unidade no computador cliente.
