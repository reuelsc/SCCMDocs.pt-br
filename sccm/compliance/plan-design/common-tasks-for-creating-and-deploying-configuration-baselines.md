---
title: 'Tarefas comuns para linhas de base de configuração '
titleSuffix: Configuration Manager
description: Saiba como criar e implantar as linhas de base de configuração no System Center Configuration Manager.
ms.date: 07/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4bb6afeb-d267-4f9b-ade2-26e5400c223b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: acccaf1994d758fbb089aebe16d22dc10e09e765
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156824"
---
# <a name="common-tasks-for-creating-and-deploying-configuration-baselines-with-system-center-configuration-manager"></a>Tarefas comuns para criar e implantar linhas de base de configuração com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico contém cenários comuns para ajudar a saber mais sobre como criar e implantar linhas de base de configuração do System Center Configuration Manager.  

 Se você já está familiarizado com as configurações de conformidade, é possível encontrar a documentação detalhada sobre todos os recursos que podem ser usados nos tópicos [Criar linhas de base de configuração](../../compliance/deploy-use/create-configuration-baselines.md) e [Implantar linhas de base de configuração](../../compliance/deploy-use/deploy-configuration-baselines.md).  

 Antes de começar, leia a [Introdução às configurações de conformidade no System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md) para aprender algumas noções básicas sobre as configurações de conformidade e [Planejar e definir as configurações de conformidade](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) para implementar os pré-requisitos necessários.  

## <a name="create-a-configuration-baseline"></a>Criar uma linha de base de configuração  
 Neste exemplo, você criou um item de configuração apenas para computadores com Windows 10 que executam o cliente do Configuration Manager.  

 Este item de configuração impõe uma senha necessária de, pelo menos, 6 caracteres em PCs com Windows 10. O item de configuração é nomeado **Imposição de Senha do Windows 10**.  

Use o procedimento a seguir para aprender a adicionar este item de configuração a uma linha de base de configuração para prepará-lo para implantação.  

1. No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Linhas de Base de Configuração**.  

2. Na guia **Início** , no grupo **Criar** , clique em **Criar Linha de Base de Configuração**.  

3. Na caixa de diálogo **Criar Linha de Base de Configuração**, defina as seguintes configurações:  

   -   **Nome** -Digite **Senhas do Windows 10** (ou outro nome de sua escolha)  

4. Clique em **Adicionar** > **Itens de Configuração**.  

5. Na caixa de diálogo **Adicionar Itens de Configuração** , selecione o item de configuração **Imposição de Senha do Windows 10** que você criou anteriormente e clique em **Adicionar**.  

6. Clique em OK para fechar a caixa de diálogo **Adicionar Itens de Configuração** e voltar para a caixa de diálogo **Criar Linha de Base de Configuração**.

7. Clique em **OK** para fechar a caixa de diálogo **Criar Linha de Base de Configuração** .  

   Agora você pode ver a linha de base de configuração no nó **Linhas de Base de Configuração** do console do Configuration Manager.  

## <a name="deploy-the-configuration-baseline"></a>Implantar a linha de base de configuração  
 Neste exemplo, você implantará a linha de base de configuração criada no procedimento anterior em uma coleção de computadores.  

1. No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Linhas de Base de Configuração**.  

2. Na lista de linhas de base de configuração, selecione **Senhas do Windows 10**.  

3. Na guia **Início** , no grupo **Implantação** , clique em **Implantar**.  

4. Na caixa de diálogo **Implantar Linhas de Base de Configuração**, defina as seguintes configurações:  

   -   **Linhas de base de configuração selecionadas** - Verifique se a linha de base de configuração das **Senhas do Windows 10** foi automaticamente adicionada a essa lista.  

   -   **Corrigir regras não compatíveis quando possível** – Marque esta caixa para garantir que, se as configurações corretas não estiverem presentes nos dispositivos de destino, elas serão corrigidas pelo Configuration Manager.  

   -   **Coleção** – Clique em **Procurar** para escolher a coleção de computadores em que a linha de base de configuração será avaliada e corrigida quanto à conformidade. Neste exemplo, a linha de base de configuração foi implantada na coleção interna **Todos os Clientes de Desktop e de Servidor** .  

       > [!TIP]  
       >  Não se preocupe se a coleção que você escolher contém computadores ou dispositivos que não executam o Windows 10. Já que você configurou as plataformas com suporte no item de configuração criado, somente os PCs com Windows 10 serão avaliados quanto à conformidade.  

   -   Se necessário, configure o agendamento pelo qual a linha de base de configuração será avaliada. Caso contrário, mantenha o padrão de **7 Dias**.  

5. Clique em **OK** para fechar a caixa de diálogo **Implantar Linhas de Base de Configuração** e criar a implantação.  

   Se quiser dar uma olhada rápida nas estatísticas de conformidade dessa implantação, no workspace **Monitoramento**, clique em **Implantações**. Na parte inferior da tela, você verá um gráfico **Estatísticas de Conformidade** .  

## <a name="next-steps"></a>Próximas etapas 

Para obter informações mais detalhadas sobre como monitorar linhas de base de configuração, confira [Monitorar configurações de conformidade](../../compliance/deploy-use/monitor-compliance-settings.md).  
