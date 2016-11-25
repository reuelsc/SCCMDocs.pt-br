---
title: "Simular implantações de aplicativos | System Center Configuration Manager"
description: "Avalie o método de detecção, requisitos e as dependências para um tipo de implantação sem instalar o aplicativo."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: a7d9267d35b58fdc6a01b869eb739e9c721db4a4


---
# <a name="simulate-application-deployments-with-system-center-configuration-manager"></a>Simular implantações de aplicativos com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use implantações simuladas se desejar testar a aplicabilidade de uma implantação de aplicativo em computadores sem instalar ou desinstalar o aplicativo. Uma implantação simulada avalia o método de detecção, os requisitos e as dependências para um tipo de implantação, e relata os resultados no nó **Implantações** do espaço de trabalho **Monitoramento** . Use o procedimento nesse tópico para simular uma implantação de aplicativo no System Center Configuration Manager.  

> [!NOTE]  
>  Você não pode usar implantações simuladas para coleções de dispositivos móveis.  
>   
>  Não será possível implantar um aplicativo com uma finalidade de implantação de **Desinstalar** se uma implantação simulada do mesmo aplicativo estiver ativa.  
  
Use o procedimento a seguir para configurar uma implantação simulada de aplicativos:
  
1.  No console do Configuration Manager, selecione uma das seguintes opções:  

    -   Uma coleção de usuários.  

    -   Uma coleção de dispositivos.  

    -   Um aplicativo do Configuration Manager.  

2.  Na guia **Início** , no grupo **Implantação** , clique em **Implantação Simulada**.  

3.  No **Assistente de Simulação de Implantação de Aplicativo**, especifique as seguintes informações:  

    -   **Aplicativo** - clique em **Procurar** e selecione o aplicativo para o qual deseja criar uma implantação simulada.  

    -   **Coleção** - clique em **Procurar** e selecione a coleção que deseja usar para a implantação simulada.  

    -   **Ação** - Na lista suspensa, selecione se deseja simular a instalação ou a desinstalação do aplicativo selecionado.  

    -   **Implantar automaticamente com ou sem logon de usuário** - Se essa opção estiver marcada, os clientes avaliarão a implantação simulada com ou sem os clientes conectados.  

4.  Clique em **Próximo**, examine as informações na página **Resumo** , e então conclua o assistente para criar a implantação de aplicativo simulado.  

5.  Aplicativos simulados aparecem no nó **Implantações** do espaço de trabalho **Monitoramento** com uma finalidade de **Simular**. Para obter mais informações sobre como monitorar implantações de aplicativos, consulte [Monitorar aplicativos do console do System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md).  



<!--HONumber=Nov16_HO1-->


