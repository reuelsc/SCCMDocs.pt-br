---
title: Simular implantações de aplicativos
titleSuffix: Configuration Manager
description: Avalie o método de detecção, requisitos e as dependências para um tipo de implantação sem instalar o aplicativo.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bd2f4f24a9bc22daac5b5c6e785ff2ea5d02f49a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="simulate-application-deployments-with-system-center-configuration-manager"></a>Simular implantações de aplicativos com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

É possível usar implantações simuladas para testar a implantação de aplicativo sem instalar ou desinstalar o aplicativo. Uma implantação simulada avalia o método de detecção, os requisitos e as dependências para um tipo de implantação. Ela reporta os resultados no nó **Implantações** do espaço de trabalho **Monitoramento**. Use o procedimento nesse tópico para simular uma implantação de aplicativo no System Center Configuration Manager (Configuration Manager).  

> [!NOTE]  
> Você não pode usar implantações simuladas para coleções de dispositivos móveis.  
>   
> Não será possível implantar um aplicativo com uma finalidade de implantação de **Desinstalar** se uma implantação simulada do mesmo aplicativo estiver ativa.  

## <a name="configure-a-simulated-application-deployment"></a>Configurar uma implantação simulada de aplicativos

1.  No console do Configuration Manager, selecione uma das seguintes opções:  
    -   Uma coleção de usuários.  
    -   Uma coleção de dispositivos.  
    -   Um aplicativo do Configuration Manager.  

2.  Na guia **Início**, no grupo **Implantação**, escolha **Implantação Simulada**.  

3.  No Assistente para simular a implantação de aplicativos, defina os seguintes detalhes para sua implantação simulada:  

    -   **Aplicativo**. Escolha **Procurar** e, então, selecione o aplicativo para o qual deseja criar uma implantação simulada.  

    -   **Coleção**. Escolha **Procurar** e, então, selecione a coleção que deseja usar para a implantação simulada.  

    -   **Ação**. Na lista suspensa, selecione se deseja simular a instalação ou a desinstalação do aplicativo selecionado.  

    -   **Implantar automaticamente com ou sem logon de usuário**. Se essa opção estiver marcada, os clientes avaliarão a implantação simulada com ou sem os clientes conectados.  

4.  Clique em **Avançar**, examine as informações na página **Resumo** e, então, conclua o assistente para criar a implantação de aplicativo simulado.  

5.  Aplicativos simulados aparecem no nó **Implantações** do espaço de trabalho **Monitoramento** com uma finalidade de **Simular**. Para obter mais informações sobre como monitorar implantações de aplicativos, consulte [Monitorar aplicativos do console do System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md).  
