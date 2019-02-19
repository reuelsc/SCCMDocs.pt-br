---
title: 'Tarefas comuns de gerenciamento de conformidade para dispositivos gerenciados pelo cliente '
titleSuffix: Configuration Manager
description: Saiba mais sobre as configurações de conformidade do System Center Configuration Manager trabalhando em alguns cenários comuns.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: a06c4294e85d3942ea3c795f3621d15ffb0ad32f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120793"
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-system-center-configuration-manager-client"></a>Tarefas comuns para gerenciar a conformidade em dispositivos com o cliente do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os cenários neste tópico oferecem uma introdução ao uso das configurações de conformidade do System Center Configuration Manager, apresentando alguns cenários comuns que podem ser encontrados.  

 Se você já está familiarizado com as configurações de conformidade, pode encontrar a documentação detalhada sobre todos os recursos que você usa na seção [Itens de configuração para dispositivos gerenciados com o cliente do System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md).  

 Antes de começar, leia a [Introdução às configurações de conformidade](../../compliance/get-started/get-started-with-compliance-settings.md) para aprender algumas noções básicas sobre as configurações de conformidade e [Planejar e definir as configurações de conformidade](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) para implementar os pré-requisitos necessários.  

## <a name="general-information-for-each-scenario"></a>Informações gerais para cada cenário  
 Em cada cenário, você criará um item de configuração que executa uma tarefa específica. Para abrir o Assistente de Criação de Item de Configuração, use as seguintes etapas:  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Itens de Configuração**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Item de Configuração**.  

4.  Na guia **Geral** do Assistente de Criação de Item de Configuração, conforme mostrado abaixo, especifique um nome e uma descrição para o item de configuração e escolha o tipo de item de configuração apropriado para cada cenário descrito neste tópico.  

     ![Mostra a página geral do assistente Criar item de configuração.](/sccm/compliance/plan-design/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-10-devices-managed-with-the-configuration-manager-client"></a>Cenários para dispositivos Windows 10 gerenciados com o cliente do Configuration Manager  

### <a name="scenario-disable-the-use-of-bluetooth-on-windows-10-devices"></a>Cenário: desabilitar o uso do Bluetooth em dispositivos Windows 10  
 Nesse cenário, seu departamento de segurança identificou a funcionalidade Bluetooth em dispositivos como um meio que pode ser usado para transmitir informações corporativas confidenciais para fora da empresa. Recentemente, você atualizou todos os seus computadores para o Windows 10 e optou por desabilitar a funcionalidade Bluetooth nesses dispositivos.  

1. Na página **Geral** do Assistente de Criação de Item de Configuração, selecione o tipo de item de configuração **Windows 10** e clique em **Avançar**.  

2. Na página **Plataformas com Suporte** do assistente, selecione todas as plataformas Windows 10.  

3. Na página **Configurações do Dispositivo** , selecione **Dispositivo**e clique em **Avançar**.  

4. Na página **Dispositivo** , selecione **Proibido** como o valor para **Bluetooth**.  

5. Selecione **Corrigir configurações não compatíveis** para garantir que a alteração será aplicada a todos os dispositivos Windows 10.  

6. Conclua o assistente para criar o item de configuração.  

   Agora você pode usar as informações do tópico [Tarefas comuns para criar e implantar linhas de base de configuração com o System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) para ajudar a implantar nos dispositivos a configuração que você criou.  

## <a name="scenarios-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>Cenários para computadores desktop e de servidor com Windows gerenciados com o cliente do Configuration Manager  
 Em computadores Mac que executam o cliente do Configuration Manager, você tem duas opções para avaliar a conformidade:  

- Avalie um arquivo de preferências (plist) do Mac OS X.  

- Use um script personalizado e avalie os resultados retornados pelo script.  

  Para mais informações, consulte [Como criar itens de configuração para dispositivos Mac OS X gerenciados com o cliente do System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md).  

### <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>Cenário: corrigir um valor de registro incorreto em computadores desktop com Windows  
 Nesse cenário, você descobre que um importante aplicativo de linha de negócios não está sendo executando corretamente em alguns computadores gerenciados que executam o Windows 8.1. Após uma investigação, você descobre que isso ocorre porque uma chave do Registro chamada **HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1** foi definida como um valor de **0** em alguns computadores. Para que o aplicativo de linha de negócios seja executado com êxito, esse valor deve ser definido como **1**.  

 Neste procedimento, você criará um item de configuração que monitora e que corrige automaticamente quaisquer valores da chave do Registro incorretos encontrados.  

1. Na página **Geral** do Assistente de Criação de Item de Configuração, selecione o tipo de item de configuração **Servidores e Desktops Windows (personalizado)** e clique em **Avançar**.  

2. Na página **Plataformas com Suporte** do assistente, selecione **Windows 8.1** (para garantir que o item de configuração se aplica somente aos computadores afetados).  

3. Na página **Configurações** , clique em **Novo** para criar uma nova configuração.  

4. Na guia **Geral** da caixa de diálogo **Criar Configuração** , configure o seguinte:  

   -   **Nome** > **Configuração de exemplo**  

   -   **Tipo de configuração** > **Valor do Registro**  

   -   **Tipo de dados** > **Inteiro** (já que o valor contém apenas um número)  

   -   **Hive** > **HKEY_LOCAL_MACHINE**  

   -   **Chave** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

   -   **Valor** > **1** (o valor necessário)  

5. Na guia **Regras de Conformidade** da caixa de diálogo **Criar Configuração** , clique em **Novo**e, na caixa de diálogo **Criar Regra** , configure o seguinte:  

   -   **Nome** > **Regra de Exemplo**  

   -   **Configuração selecionada** – Verifique se a configuração selecionada é **Configuração de exemplo**.  

   -   **Tipo de regra** > **Valor**  

   -   **A configuração deve ser compatível com a regra a seguir** – Verifique se o nome da configuração está correto e configure a opção para especificar que o valor da configuração deve ser igual a **1**.  

   -   **Corrigir regras não compatíveis quando suportadas** – Marque esta caixa para garantir que o Configuration Manager redefinirá o valor da chave do Registro para o valor correto se ela estiver incorreta.  

6. Conclua o assistente para criar o item de configuração.  

   Agora você pode usar as informações do tópico [Tarefas comuns para criar e implantar linhas de base de configuração](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) para ajudar a implantar nos dispositivos a configuração que você criou.  
