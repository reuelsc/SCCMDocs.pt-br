---
title: "Criar linhas de base de configuração | Microsoft Docs"
description: "Criar linhas de base de configuração no System Center Configuration Manager que podem ser implantadas para uma coleção."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 649942d3d468ec35c7246e08f741cdebd22fb3ac
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="create-configuration-baselines-in-system-center-configuration-manager"></a>Criar linhas de base de configuração no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


As linhas de base de configuração no System Center Configuration Manager contêm itens de configuração predefinidos e, opcionalmente, outras linhas de base de configuração. Após a criação de uma linha de base de configuração, você pode implantá-la em uma coleção, para que os dispositivos dessa coleção possam baixá-la e avaliar sua conformidade com ela.  

 As linhas de base de configuração no Configuration Manager podem conter revisões específicas de itens de configuração ou podem ser configuradas para usar sempre a versão mais recente de um item de configuração. Para obter mais informações sobre revisões do item de configuração, consulte [Tarefas de gerenciamento para dados de configuração](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

 Há dois métodos que você pode usar para criar linhas de base de configuração:  

-   Importe dados de configuração de um arquivo. Para iniciar o **Assistente para Importar Dados de Configuração**, no nó **Itens de Configuração** ou **Linhas de Base de Configuração** do espaço de trabalho **Ativos e Conformidade** , clique em **Importar Dados de Configuração**.  

-   Use a caixa de diálogo **Criar Linha de Base de Configuração** para criar uma nova linha de base de configuração.  

 Use o procedimento a seguir para criar uma linha de base de configuração usando a caixa de diálogo **Criar Linha de Base de Configuração** .  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Linhas de Base de Configuração**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Linha de Base de Configuração**.  

4.  Na caixa de diálogo **Criar Linha de Base de Configuração** , digite um nome exclusivo e uma descrição para a linha de base de configuração. Você pode usar, no máximo, 255 caracteres para o nome e 512 caracteres para a descrição.  

5.  A lista **Dados de configuração** exibe todos os itens de configuração ou todas as linhas de base de configuração incluídas nessa linha de base de configuração. Clique em **Adicionar** para adicionar um novo item de configuração ou uma nova linha de base de configuração à lista. É possível escolher entre as seguintes opções:  

    -   **Itens de Configuração**  

    -   **Atualizações de software**  

    -   **Linhas de Base de Configuração**  
      > [!IMPORTANT]
      > Você deve limitar cada linha de base de configuração a não mais de 1000 atualizações de software.
6.  Use a lista **Alterar Finalidade** para especificar o comportamento de um item de configuração que você selecionou na lista **Dados de configuração** . Você pode selecionar na seguinte lista:  

    -   **Obrigatório** A linha de base de configuração é avaliada como não compatível se o item de configuração não é detectado em um dispositivo cliente. Se ele for detectado, ele será avaliado quanto à conformidade  

    -   **Opcional** O item de configuração somente é avaliado quanto à conformidade se o aplicativo ao qual ele faz referência for encontrado nos computadores cliente. Se o aplicativo não for encontrado, a linha de base de configuração não será marcada como não compatível (aplicável apenas a itens de configuração de aplicativo).  

    -   **Proibido** A linha de base de configuração é avaliada como não compatível se o item de configuração for detectado nos computadores cliente (somente aplicável a itens de configuração de aplicativo).  

    > [!NOTE]
    >  A lista **Alterar Finalidade** estará disponível somente se você clicou na opção **Este item de configuração contém as configurações do aplicativo** na página **Geral** do **Assistente para Criar Item de Configuração**.  

7.  Use a lista **Alterar revisão** para selecionar uma versão específica ou a revisão mais recente do item de configuração para avaliar a conformidade em dispositivos cliente; outra opção é selecionar **Sempre usar a mais recente** para usar sempre a versão mais recente. Para obter mais informações sobre revisões do item de configuração, consulte [Tarefas de gerenciamento para dados de configuração](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

8.  Para remover um item de configuração da linha de base de configuração, selecione um item de configuração e clique em **Remover**.  

9. Clique em **OK** para fechar a caixa de diálogo **Criar Linha de Base de Configuração** e criar a linha de base de configuração.  
