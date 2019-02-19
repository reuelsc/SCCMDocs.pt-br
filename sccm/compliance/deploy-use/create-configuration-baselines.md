---
title: Criar linhas de base de configuração
titleSuffix: Configuration Manager
description: Criar linhas de base de configuração no System Center Configuration Manager que podem ser implantadas para uma coleção.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 67a68975bbd6f9356ecc34ec95007fad3b8b333b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132741"
---
# <a name="create-configuration-baselines-in-system-center-configuration-manager"></a>Criar linhas de base de configuração no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


As linhas de base de configuração no System Center Configuration Manager contêm itens de configuração predefinidos e, opcionalmente, outras linhas de base de configuração. Após a criação de uma linha de base de configuração, você pode implantá-la em uma coleção, para que os dispositivos dessa coleção possam baixá-la e avaliar sua conformidade com ela.  

 As linhas de base de configuração no Configuration Manager podem conter revisões específicas de itens de configuração ou podem ser configuradas para usar sempre a versão mais recente de um item de configuração. Para obter mais informações sobre revisões do item de configuração, consulte [Tarefas de gerenciamento para dados de configuração](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

 Há dois métodos que você pode usar para criar linhas de base de configuração:  

-   Importe dados de configuração de um arquivo. Para iniciar o **Assistente para Importar Dados de Configuração**, no nó **Itens de Configuração** ou **Linhas de Base de Configuração** do workspace **Ativos e Conformidade**, clique em **Importar Dados de Configuração**.  

-   Use a caixa de diálogo **Criar Linha de Base de Configuração** para criar uma nova linha de base de configuração.  

Para criar uma linha de base de configuração usando a caixa de diálogo **Criar linha de base de configuração**, use o procedimento a seguir:  

1. No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Linhas de Base de Configuração**.  

2. Na guia **Início** , no grupo **Criar** , clique em **Criar Linha de Base de Configuração**.  

3. Na caixa de diálogo **Criar Linha de Base de Configuração** , digite um nome exclusivo e uma descrição para a linha de base de configuração. Você pode usar, no máximo, 255 caracteres para o nome e 512 caracteres para a descrição.  

4. A lista **Dados de configuração** exibe todos os itens de configuração ou todas as linhas de base de configuração incluídas nessa linha de base de configuração. Clique em **Adicionar** para adicionar um novo item de configuração ou uma nova linha de base de configuração à lista. Você pode escolher entre os itens a seguir:  

   - **Itens de Configuração**  

   - **Atualizações de software**  

   - **Linhas de Base de Configuração**  
     > [!IMPORTANT]
     > Você deve limitar cada linha de base de configuração a não mais de 1000 atualizações de software.
5. Use a lista **Alterar Finalidade** para especificar o comportamento de um item de configuração que você selecionou na lista **Dados de configuração**. Você pode selecionar os itens a seguir:  

   -   **Obrigatório**: a linha de base será avaliada como fora de conformidade se o item de configuração não for detectado em um dispositivo cliente. Se ele for detectado, ela será avaliada quanto à conformidade  

   -   **Opcional**: a conformidade do item de configuração apenas será avaliada se o aplicativo referenciado por ele for encontrado nos computadores cliente. Se o aplicativo não for encontrado, a linha de base de configuração não será marcada como não compatível (aplicável apenas a itens de configuração de aplicativo).  

   -   **Proibido**: a linha de base de configuração será avaliada como fora de conformidade se o item de configuração for detectado nos computadores cliente (aplicável apenas a itens de configuração de aplicativo).  

   > [!NOTE]
   >  A lista **Alterar Finalidade** estará disponível somente se você clicou na opção **Este item de configuração contém as configurações do aplicativo** na página **Geral** do **Assistente para Criar Item de Configuração**.  

6. Use a lista **Alterar revisão** para selecionar uma versão específica ou a revisão mais recente do item de configuração para avaliar a conformidade em dispositivos cliente; outra opção é selecionar **Sempre usar a mais recente** para usar sempre a versão mais recente. Para obter mais informações sobre revisões do item de configuração, consulte [Tarefas de gerenciamento para dados de configuração](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

7. Para remover um item de configuração da linha de base de configuração, selecione um item de configuração e clique em **Remover**.  

8. Começando na versão 1806, é possível selecionar se você deseja **Sempre aplicar esta linha de base a clientes cogerenciados**. Quando essa opção estiver marcada, esta linha de base será aplicada mesmo em clientes que são gerenciados pelo Intune.  Essa exceção pode ser usada para definir configurações exigidas pela sua organização, mas ainda não disponíveis no Intune. 

9. Opcionalmente, clique em **Categorias** para atribuir categorias à linha de base para pesquisa e filtragem. 

10. Clique em **OK** para fechar a caixa de diálogo **Criar Linha de Base de Configuração** e criar a linha de base de configuração.  

>[!NOTE]
> A modificação de uma linha de base existente, como a configuração **Sempre aplicar esta linha de base para clientes cogerenciados**, incrementará a versão do conteúdo da linha de base. Os clientes precisarão avaliar a nova versão para atualizar o relatório de linha de base. 
