---
title: 'Tarefas comuns de gerenciamento de conformidade para dispositivos gerenciados pelo cliente '
titleSuffix: Configuration Manager
description: Saiba mais sobre as configurações de conformidade do System Center Configuration Manager trabalhando em alguns cenários comuns.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 67a23fd5c1791253a7789fda74a30a0e71566f92
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67550831"
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-system-center-configuration-manager-client"></a>Tarefas comuns para gerenciar a conformidade em dispositivos com o cliente do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo fornece uma introdução ao uso de configurações de conformidade do System Center Configuration Manager, guiando você pelas alguns cenários comuns que você pode se deparar com.  

 Se você já estiver familiarizado com as configurações de conformidade, encontre informações detalhadas sobre todos os recursos que você usa em [Itens de configuração para dispositivos gerenciados com o cliente do System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items.md).  

 Antes de começar, leia [Introdução às configurações de conformidade](../../compliance/get-started/get-started-with-compliance-settings.md) para aprender algumas noções básicas sobre configurações de conformidade. Leia [planejar e definir configurações de conformidade](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) para obter informações sobre os pré-requisitos necessários.  

## <a name="general-information-for-each-scenario"></a>Informações gerais para cada cenário  
 Em cada cenário, você criará um item de configuração que executa uma tarefa específica. Para abrir o Assistente para criar Item de configuração e começar, siga estas etapas:  

1.  No console do Configuration Manager, selecione **Ativos e Conformidade** > **Configurações de conformidade** > **Itens de Configuração**.  

1.  Na guia **Início**, no grupo **Criar**, selecione **Criar Item de Configuração**.  

1.  Sobre o **geral** página do the Create Configuration Item Wizard, mostrado na seguinte captura de tela, especifique um nome e uma descrição para o item de configuração. Em seguida, escolha o tipo de item de configuração apropriado para cada cenário neste artigo.  

     ![Página geral do Assistente de Criação de Item de Configuração](/sccm/mdm/deploy-use/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenario-disable-bluetooth-on-windows-10-devices"></a>Cenário: Desabilitar Bluetooth em dispositivos Windows 10

 Neste cenário, seu departamento de segurança determinou que a funcionalidade Bluetooth nos dispositivos poderia ser usada para transmitir informações corporativas confidenciais para fora da empresa. Você atualizou recentemente a todos os seus computadores para o Windows 10. Você optar por desabilitar Bluetooth nesses dispositivos.  

1. Na página **Geral** do Assistente de Criação de Item de Configuração, selecione o tipo de item de configuração **Windows 10** e depois **Avançar**.  

2. Na página **Plataformas com Suporte** do assistente, selecione todas as plataformas Windows 10.  

3. Sobre o **configurações do dispositivo** página, selecione **dispositivo**e, em seguida, selecione **próxima**.  

4. Na página **Dispositivo** , selecione **Proibido** como o valor para **Bluetooth**.  

5. Selecione **Corrigir configurações não compatíveis** para garantir que a alteração será aplicada a todos os dispositivos Windows 10.  

6. Conclua o assistente para criar o item de configuração.  

 Agora você pode usar as informações do artigo [Tarefas comuns para criar e implantar linhas de base de configuração com o System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) para ajudar a implantar nos dispositivos a configuração que você criou.  

## <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>Cenário: corrigir um valor do Registro incorreto em computadores desktop com Windows

> [!NOTE] 
> Em computadores Mac que executam o cliente do Configuration Manager, você tem duas opções para avaliar a conformidade:  
> - Avalie um arquivo de preferências (plist) do Mac OS X.
> - Use um script personalizado e avalie os resultados retornados pelo script.  
>
>Para mais informações, consulte [Como criar itens de configuração para dispositivos Mac OS X gerenciados com o cliente do System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md).  

 Nesse cenário, você descobre que um aplicativo de linha de negócios importante não é executado corretamente em alguns computadores Windows 8.1 que você gerencia. Você determina que isso ocorre porque uma chave do Registro chamada **HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1** foi definida como um valor de **0** em alguns computadores. Para que o aplicativo de linha de negócios seja executado com êxito, esse valor precisa ser definido como **1**.  

 Neste procedimento, você criará um item de configuração que monitora e corrige automaticamente quaisquer valores incorretos da chave do Registro encontrados.  

1. Na página **Geral** do Assistente de Criação de Item de Configuração, selecione o tipo de item de configuração **Servidores e Desktops Windows (personalizado)** e depois **Avançar**.  

2. Na página **Plataformas com Suporte** do assistente, selecione **Windows 8.1** (para garantir que o item de configuração se aplique somente aos computadores afetados).  

3. Na página **Configurações**, selecione **Novo** para criar uma nova configuração.  

4. Na guia **Geral** da caixa de diálogo **Criar Configuração**, configure o seguinte:  

   -   **Nome** > **Configuração de exemplo**  

   -   **Tipo de configuração** > **Valor do Registro**  

   -   **Tipo de dados** > **Inteiro** (já que o valor contém apenas um número)  

   -   **Hive** > **HKEY_LOCAL_MACHINE**  

   -   **Chave** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

   -   **Valor** > **1** (o valor necessário)  

5. Sobre o **regras de conformidade** guia do **criar configuração** caixa de diálogo, selecione **New**. No **Create Rule** caixa de diálogo caixa, defina estas configurações:  

   -   **Nome** > **Regra de Exemplo**  

   -   **Configuração selecionada** > Verifique se a configuração selecionada é **Configuração de exemplo**.

   -   **Tipo de regra** > **Valor**  

   -   **A configuração precisa ser compatível com a regra a seguir** > Verifique se o nome da configuração está correto e configure a opção para especificar que o valor da configuração deve ser igual a **1**.  

   -   **Corrigir regras não compatíveis quando suportadas** > Marque esta caixa de seleção para garantir que o Configuration Manager redefinirá o valor da chave do Registro para o valor correto se ela estiver incorreta.  

6. Conclua o assistente para criar o item de configuração.  

 Agora você pode usar as informações do artigo [Tarefas comuns para criar e implantar linhas de base de configuração](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) para ajudar a implantar nos dispositivos a configuração que você criou.  

## <a name="next-steps"></a>Próximas etapas

[Criar e implantar linhas de base de configuração](/sccm/compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines)
