---
title: Hierarquias de origem de migração
titleSuffix: Configuration Manager
description: Configure uma hierarquia de origem e sites de origem para que você possa migrar dados para seu ambiente do System Center Configuration Manager.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ccce7cb5-e18f-4337-8adf-2018edca3c00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d9ef1ca2dd2763cf5b96fd82031a2ef38ef64927
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="configure-source-hierarchies-and-source-sites-for-migration-to-system-center-configuration-manager"></a>Configurar hierarquias de origem e sites de origem para migração para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para habilitar a migração de dados para o seu ambiente do System Center Configuration Manager, é necessário configurar uma hierarquia de origem do Configuration Manager com suporte e um ou mais sites de origem nessa hierarquia que contenham os dados que você deseja migrar.  

> [!NOTE]  
>  As operações de migração são executadas no site de nível superior na hierarquia de destino. Se você configurar a migração ao usar um console do Configuration Manager que esteja conectado a um site filho primário, você deverá dar tempo para a configuração replicar no site da administração central, iniciar e, em seguida, replicar o status de volta para o site primário ao qual você está conectado.  

 Use as informações e os procedimentos nas seções a seguir para especificar a hierarquia de origem e adicionar outros sites de origem. Após concluir esses procedimentos, você poderá criar trabalhos de migração e começar a migrar dados da hierarquia de origem para a hierarquia de destino.  

-   [Especificar uma hierarquia de origem para migração](#BKBM_ConfigSrcHierarchy)  

-   [Identificar sites de origem adicionais da hierarquia de origem](#BKBM_ConfigSrcSites)  

##  <a name="BKBM_ConfigSrcHierarchy"></a> Especificar uma hierarquia de origem para migração  
 Para migrar dados para a sua hierarquia de destino, é necessário especificar uma hierarquia de origem com suporte que tem os dados que você deseja migrar. Por padrão, o site de nível superior dessa hierarquia torna-se um site de origem da hierarquia de origem. Se você migrar de uma hierarquia do Configuration Manager 2007, será possível configurar sites de origem adicionais para migração, depois que os dados forem coletados do site de origem inicial. Se você migrar de uma hierarquia do System Center 2012 Configuration Manager ou do System Center Configuration Manager, não será necessário configurar sites de origem adicionais para migrar dados da hierarquia de origem. Isso se deve ao fato de essas versões do Configuration Manager usarem um banco de dados compartilhado que está disponível no site de nível superior da hierarquia de origem. O banco de dados compartilhado tem todas as informações que você pode migrar.  

 Use os procedimentos a seguir para especificar uma hierarquia de origem para migração e para identificar sites de origem adicionais em uma hierarquia do Configuration Manager 2007.  

 Execute este procedimento com um console do Configuration Manager conectado à hierarquia de destino:  

### <a name="to-configure-a-source-hierarchy"></a>Para configurar uma hierarquia de origem   

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Migração**e clique em **Hierarquia de Origem**.  

3.  Na guia **Início** , no grupo **Migração** , clique em **Especificar Hierarquia de Origem**.  

4.  Na caixa de diálogo **Especificar Hierarquia de Origem** , para **Hierarquia de Origem**, selecione **Nova Hierarquia de Origem**.  

5.  Para **Servidor do site do Configuration Manager da camada superior**, insira o nome ou endereço IP do site de nível superior de uma hierarquia de origem com suporte.  

6.  Especifique as contas de acesso do site de origem que têm as seguintes permissões:  

    -   Conta do site de origem: Permissão de **Leitura** ao Provedor de SMS para o site de nível superior especificado na hierarquia de origem. Atualizações e compartilhamentos de pontos de distribuição requerem as permissões **Modificar** e **Excluir** para o site na Hierarquia de Origem.

    -   Conta do banco de dados do site de origem: Permissão de **Leitura** e **Executar** ao banco de dados do SQL Server para o site de nível superior especificado na hierarquia de origem.  

     Se você especificar o uso da conta de computador, o Configuration Manager usará a conta de computador do site de nível superior da hierarquia de destino. Para essa opção, certifique-se de que essa conta é membro do grupo de segurança **Distributed COM – Usuários** no domínio em que reside o site de nível superior da hierarquia de origem.  

7.  Para compartilhar pontos de distribuição entre as hierarquias de origem e de destino, marque a caixa de seleção **Habilitar o compartilhamento de ponto de distribuição para o servidor do site de origem** . Se você não habilitar o compartilhamento do ponto de distribuição agora, poderá fazê-lo editando as credenciais do site de origem após a conclusão da coleta de dados.  

8.  Clique em **OK** para salvar a configuração. Esse procedimento abrirá a caixa de diálogo **Status da Coleta de Dados** , e a coleta de dados será iniciada automaticamente.  

9. Quando a coleta de dados for concluída, clique em **Fechar** para fechar a caixa de diálogo **Status da Coleta de Dados** e concluir a configuração.  

##  <a name="BKBM_ConfigSrcSites"></a> Identificar sites de origem adicionais da hierarquia de origem  
 Quando você configura uma hierarquia de origem suportada, o site de nível superior dessa hierarquia é automaticamente configurado como um site de origem e os dados são automaticamente coletados. A próxima ação que você executar dependerá da versão do Configuration Manager executada pela hierarquia de origem:  

-   Para uma hierarquia de origem do Configuration Manager 2007, é possível iniciar a migração desse site de origem inicial ou configurar sites de origem adicionais na hierarquia de origem, após a conclusão da coleta de dados para o site de origem inicial. Para migrar dados disponíveis apenas em um site filho, configure sites de origem adicionais para uma hierarquia do Configuration Manager 2007. Por exemplo, você poderia configurar sites de origem adicionais para coletar dados sobre o conteúdo que você deseja migrar quando este conteúdo foi criado em um site filho na hierarquia de origem e não está disponível no site de nível superior da hierarquia de origem.  

-   Para uma hierarquia de origem do System Center 2012 Configuration Manager ou do System Center Configuration Manager, não é necessário configurar sites de origem adicionais. Isso se deve ao fato de essas versões do Configuration Manager usarem um banco de dados compartilhado que está disponível no site de nível superior da hierarquia de origem. O banco de dados compartilhado tem todas as informações que você pode migrar de todos os sites nessa hierarquia de origem. Isso torna os dados que você pode migrar disponíveis no site de nível superior da hierarquia de origem.  

Quando você configura sites de origem adicionais para uma hierarquia de origem do Configuration Manager 2007, é necessário configurar sites de origem adicionais do nível superior até o nível inferior da hierarquia. É necessário configurar um site pai como um site de origem antes de configurar qualquer um de seus sites filho como sites de origem.  

Use o procedimento a seguir para configurar sites de origem adicionais para hierarquias de origem do Configuration Manager 2007:  

### <a name="to-identify-additional-source-sites-in-the-source-hierarchy"></a>Para identificar sites de origem adicionais na hierarquia de origem 

1.  No console do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **Administração** , expanda **Migração**e clique em **Hierarquia de Origem**.  

3.  Escolha o site que deseja configurar como um site de origem.  

4.  Na guia **Início** , no grupo **Site de Origem** , clique em **Configurar**.  

5.  Na caixa de diálogo **Credenciais do Site de Origem** , para as contas de acesso do site de origem, especifique as contas que têm as seguintes permissões:  

    -   Conta do site de origem: Permissão de **Leitura** ao Provedor de SMS para o site de nível superior especificado na hierarquia de origem. Atualizações e compartilhamentos de pontos de distribuição requerem as permissões **Modificar** e **Excluir** para o site na Hierarquia de Origem.  

    -   Conta do banco de dados do site de origem: Permissão de **Leitura** e **Executar** ao banco de dados do SQL Server para o site de nível superior especificado na hierarquia de origem.  

    Se você especificar o uso da conta de computador, o Configuration Manager usará a conta de computador do site de nível superior da hierarquia de destino. Para essa opção, certifique-se de que essa conta é membro do grupo de segurança **Distributed COM – Usuários** no domínio em que reside o site de nível superior da hierarquia de origem.  

6.  Para compartilhar pontos de distribuição entre as hierarquias de origem e de destino, marque a caixa de seleção **Habilitar o compartilhamento de ponto de distribuição para o servidor do site de origem** . Se você não habilitar o compartilhamento do ponto de distribuição agora, poderá fazê-lo editando as credenciais do site de origem após a conclusão da coleta de dados.  

7. Clique em **OK** para salvar a configuração. Esse procedimento abrirá a caixa de diálogo **Status da Coleta de Dados** , e a coleta de dados será iniciada automaticamente.  

8.  Quando a coleta de dados for concluída, clique em **Fechar** para finalizar a configuração.  
