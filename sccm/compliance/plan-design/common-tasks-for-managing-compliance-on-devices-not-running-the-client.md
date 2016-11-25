---
title: "Tarefas comuns para gerenciar a conformidade em dispositivos que não executam o cliente do System Center Configuration Manager | System Center Configuration Manager"
description: "Saiba mais sobre as configurações de conformidade do System Center Configuration Manager trabalhando em alguns cenários comuns."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 116cca2a-0a98-43fd-ac9e-e3daeddefce3
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f69250fbe51ea8902a0446a613d66be390ea7434


---
# <a name="common-tasks-for-managing-compliance-on-devices-not-running-the-system-center-configuration-manager-client"></a>Tarefas comuns para gerenciar a conformidade em dispositivos que não executam o cliente do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Esses cenários oferecem uma introdução ao uso das configurações de conformidade do System Center Configuration Manager, apresentando alguns cenários comuns que podem ser encontrados.  

 Se você já está familiarizado com as configurações de conformidade, pode encontrar a documentação detalhada sobre todos os recursos que você usa na seção [Itens de configuração para dispositivos gerenciados sem o cliente do System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md).  

 Antes de começar, leia a [Introdução às configurações de conformidade](../../compliance/get-started/get-started-with-compliance-settings.md) para aprender algumas noções básicas sobre as configurações de conformidade e [Planejar e definir as configurações de conformidade](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) para implementar os pré-requisitos necessários.  

## <a name="general-information-for-each-scenario"></a>Informações gerais para cada cenário  
 Em cada cenário, você criará um item de configuração que executa uma tarefa específica. Para abrir o Assistente de Criação de Item de Configuração, use as seguintes etapas:  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Itens de Configuração**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Item de Configuração**.  

4.  Na guia **Geral** do Assistente de Criação de Item de Configuração, conforme mostrado abaixo, especifique um nome e uma descrição para o item de configuração e escolha o tipo de item de configuração apropriado para cada cenário descrito neste tópico.  

     ![Mostra a página geral do assistente Criar item de configuração.](/sccm/compliance/plan-design/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-81-and-windows-10-devices-managed-without-the-configuration-manager-client"></a>Cenários para dispositivos Windows 8.1 e Windows 10 gerenciados sem o cliente do Configuration Manager  

### <a name="scenario-restrict-access-to-the-app-store-on-all-windows-pcs"></a>Cenário: restringir o acesso à loja de aplicativos em todos os computadores com Windows  
 Nesse cenário, você é o administrador de TI de uma empresa que lida com informações altamente confidenciais. Por isso, você restringe os aplicativos que os usuários podem instalar. Você deseja impedir que os usuários de todos os computadores com Windows 10 baixem aplicativos da Windows Store; para isso, você executa as seguintes ações.  

#### <a name="steps"></a>Etapas  

1.  Na página **Geral** do Assistente de Criação de Item de Configuração, selecione o tipo de item de configuração **Windows 8.1 e Windows 10** e clique em **Avançar**.  

2.  Na página **Plataformas com Suporte**, selecione todas as plataformas Windows 10.  

3.  Na página **Configurações do Dispositivo** , selecione **Loja**e clique em **Avançar**.  

4.  Na página **Loja** , selecione **Proibido** como o valor para **Loja de aplicativos**.  

5.  Selecione **Corrigir configurações não compatíveis** para garantir que a alteração será aplicada a todos os computadores.  

6.  Conclua o assistente para criar o item de configuração.  

 Agora você pode usar as informações do tópico [Tarefas comuns para criar e implantar linhas de base de configuração](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) para ajudar a implantar nos dispositivos a configuração que você criou.  

## <a name="scenarios-for-windows-phone-devices-managed-without-the-configuration-manager-client"></a>Cenários para dispositivos Windows Phone gerenciados sem o cliente do Configuration Manager  

### <a name="scenario-disable-the-use-of-screen-capture-on-a-windows-phone"></a>Cenário: desabilitar o uso da captura de tela em um Windows Phone  
 Nesse cenário, você usa dispositivos Windows Phone 8.1 em sua empresa. Esses dispositivos executam um aplicativo de vendas que contém informações confidenciais. Para proteger sua empresa, você deseja desabilitar o uso da captura de tela no dispositivo, que poderia ser usada para transmitir informações confidenciais para fora de sua empresa.  

1.  Na página **Geral** do Assistente de Criação de Item de Configuração, selecione o tipo de item de configuração **Windows Phone** e clique em **Avançar**.  

2.  Na página **Plataformas com Suporte**, selecione **Todas as plataformas Windows 8.1**.  

3.  Na página **Configurações do Dispositivo** , selecione **Dispositivo**e clique em **Avançar**.  

4.  Na página **Dispositivo** , selecione **Desabilitado** como o valor para **Captura de tela**.  

5.  Selecione **Corrigir configurações não compatíveis** para garantir que a alteração será aplicada a todos os dispositivos Windows Phone 8.1.  

6.  Conclua o assistente para criar o item de configuração.  

 Agora você pode usar as informações do tópico [Tarefas comuns para criar e implantar linhas de base de configuração com o System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) para ajudar a implantar nos dispositivos a configuração que você criou.  

## <a name="scenarios-for-ios-and-mac-os-x-devices-managed-without-the-configuration-manager-client"></a>Cenários para dispositivos iOS e Mac OS X gerenciados sem o cliente do Configuration Manager  

### <a name="scenario-disable-the-camera-on-ios-devices"></a>Cenário: desabilitar a câmera em dispositivos iOS  
 Nesse cenário, sua empresa produz planos gráficos para novos designs de produtos. Eles contêm informações confidenciais que não devem ser vazadas. Como sua empresa emite iPhones ou iPads para todos os funcionários, você deseja desabilitar o uso da câmera nesses dispositivos para evitar que elas sejam usadas para fotografar os planos gráficos.  

1.  Na página **Geral** do Assistente de Criação de Item de Configuração, selecione o tipo de item de configuração **iOS e Mac OS X** e clique em **Avançar**.  

2.  Na página **Plataformas com Suporte**, selecione todas as plataformas de dispositivos iPhone e iPad.  

3.  Na página **Configurações do Dispositivo** , selecione **Segurança**e clique em **Avançar**.  

4.  Na página **Segurança** , selecione **Proibido** como o valor para **Câmera**.  

5.  Selecione **Corrigir configurações não compatíveis** para garantir que a alteração será aplicada a todos os dispositivos iOS.  

6.  Conclua o assistente para criar o item de configuração.  

 Agora você pode usar as informações do tópico [Tarefas comuns para criar e implantar linhas de base de configuração com o System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) para ajudar a implantar nos dispositivos a configuração que você criou.  

## <a name="scenarios-for-android-and-samsung-knox-devices-managed-without-the-configuration-manager-client"></a>Cenários para dispositivos Android e Samsung KNOX gerenciados sem o cliente do Configuration Manager  

### <a name="scenario-require-a-password-on-all-android-5-devices"></a>Cenário: exigir uma senha em todos os dispositivos Android 5  
 Nesse cenário, você criará um item de configuração apenas para dispositivos Android 5 que exige que os usuários configurem uma senha de, pelo menos, 6 caracteres em seus dispositivos. Além disso, se um usuário inserir uma senha incorreta cinco vezes, o dispositivo será apagado.  

1.  Na página **Geral** do Assistente de Criação de Item de Configuração, selecione o tipo de item de configuração **Android e Samsung KNOX** e clique em **Avançar**.  

2.  Na página **Plataformas com Suporte**, selecione apenas **Android 5** (para garantir que as configurações só serão aplicadas a essa plataforma).  

3.  Na página **Configurações do Dispositivo** , selecione **Senha**e clique em **Avançar**.  

4.  Na página **Senha** , defina as seguintes configurações:  

    -   **Exigir configurações de senha em dispositivos** > **Necessário**  

    -   **Comprimento mínimo da senha (caracteres)** > **6**  

    -   **Número de tentativas de logon com falha antes de o dispositivo ser apagado** > **5**  

5.  Conclua o assistente para criar o item de configuração.  

 Agora você pode usar as informações do tópico [Tarefas comuns para criar e implantar linhas de base de configuração](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) para ajudar a implantar nos dispositivos a configuração que você criou.  




<!--HONumber=Nov16_HO1-->


