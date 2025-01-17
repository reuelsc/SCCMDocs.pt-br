---
title: Políticas do Firewall do Windows para o Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba como criar e implantar políticas de firewall para o Endpoint Protection no System Center 2012 Configuration Manager.
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6ecdfad1-6305-45a8-ae75-3f33b967cb8f
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d71ea7cf51d2657cea59ae21f7aa120fe11d191c
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65494555"
---
# <a name="create-and-deploy-windows-firewall-policies-for-endpoint-protection-in-system-center-configuration-manager"></a>Criar e implantar políticas do Firewall do Windows para o Endpoint Protection no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As políticas de firewall para o Endpoint Protection no System Center Configuration Manager permitem executar tarefas básicas de configuração e manutenção do Firewall do Windows em computadores cliente na sua hierarquia. Você pode usar políticas de Firewall do Windows para executar as seguintes tarefas:  

-   Controlar se o Firewall do Windows está ativado ou desativado.  

-   Controlar se as conexões de entrada são permitidas nos computadores cliente.  

-   Controle se os usuários são notificados quando o Firewall do Windows bloquear um novo programa.  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No workspace **Ativos e Conformidade**, expanda **Endpoint Protection** e clique em **Políticas de Firewall do Windows**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Política de Firewall do Windows**.  

4.  Na página **Geral** do **Assistente de Criação de Política de Firewall do Windows**, especifique um nome e uma descrição opcional a política de firewall e clique em **Avançar**.  

5.  Na página de **Configurações do Perfil** do assistente, defina as seguintes configurações para cada perfil de rede:  

    > [!IMPORTANT]  
    >  Se quiser implantar políticas de firewall do Windows em computadores que executam o Windows Server 2008 e o Windows Vista Service Pack 1, você deve primeiro instalar o [Hotfix KB971800](http://go.microsoft.com/fwlink/p/?LinkId=231239) nesses computadores.  

    > [!NOTE]  
    >  Para obter mais informações sobre os perfis de rede, consulte a documentação do Windows.  

    -   **Habilitar o Firewall do Windows**  

        > [!NOTE]  
        >  Se **Habilitar Firewall do Windows** não estiver habilitado, as outras configurações nesta página do assistente ficarão indisponíveis.  

    -   **Bloquear todas as conexões de entrada, incluindo aquelas na lista de programas permitidos**  

    -   **Notificar o usuário quando o Firewall do Windows bloquear um novo programa**  

6.  Na página **Resumo** do assistente, examine as ações a serem tomadas e conclua o assistente.  

7.  Verifique se a nova política de Firewall do Windows é exibida na lista **Políticas de Firewall do Windows** .  

##  <a name="BKMK_Assign"></a> Para implantar uma política de Firewall do Windows  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No workspace **Ativos e Conformidade**, expanda **Endpoint Protection** e clique em **Políticas de Firewall do Windows**.  

3.  Na lista **Políticas de Firewall do Windows** , selecione a política de Firewall do Windows que você deseja implantar.  

4.  Na guia **Início** , no grupo **Implantação** , clique em **Implantar**.  

5.  Na caixa de diálogo **Implantar Política de Firewall do Windows** , especifique a coleção à qual você deseja atribuir a política de Firewall do Windows e especifique um cronograma de atribuição. A política de Firewall do Windows avalia a conformidade usando esse cronograma e as configurações do Firewall do Windows em clientes para reconfigurá-los para coincidir com a política de Firewall do Windows.  

6.  Clique em **OK** para fechar a caixa de diálogo **Implantar Política de Firewall do Windows** e implantar a política de Firewall do Windows.  

    > [!IMPORTANT]  
    >  Quando você implanta uma política de Firewall do Windows a uma coleção, essa política é aplicada aos computadores em ordem aleatória ao longo de duas horas para evitar a saturação da rede.
