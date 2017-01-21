---
title: "Criar coleções | Microsoft Docs"
description: "Crie coleções no System Center Configuration Manager para gerencie mais facilmente os grupos de usuários e dispositivos."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 5ade6d22e1f04c1528f319e2c2a4b576ac290bd6


---
# <a name="how-to-create-collections-in-system-center-configuration-manager"></a>Como criar coleções no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Crie coleções no System Center Configuration Manager para representar agrupamentos lógicos de usuários ou dispositivos. Você pode usar coleções para ajudá-lo a realizar várias tarefas, incluindo gerenciamento de aplicativos, implantação de configurações de conformidade ou instalação de atualizações de software. Você também pode usar coleções para gerenciar grupos de configurações do cliente ou usá-las com a administração baseada em funções para especificar os recursos que um usuário administrativo pode acessar. O Configuration Manager contém várias coleções internas. Para obter mais informações, consulte [Introdução às coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).  

> [!NOTE]  
>  Uma coleção individual pode conter usuários ou dispositivos, mas não ambos.  

 A tabela a seguir lista as regras que você pode usar para configurar os membros de uma coleção no Configuration Manager.  

|Tipo de regra de associação|Mais informações|  
|--------------------------|----------------------|  
|Regra direta|As diretas regras permitem que você escolha os usuários ou computadores que você deseja adicionar como membros de uma coleção. Esta regra fornece a você controle direto sobre quais recursos são membros da coleção. Esta associação não é alterada a menos que um recurso seja removido do Configuration Manager. O Configuration Manager deve ter descoberto os recursos ou é necessário importar os recursos antes de poder adicioná-los a uma coleção de regra direta. As coleções de regras diretas têm uma maior sobrecarga administrativa que as coleções de regras de consulta, devido ao fato de ser necessário fazer alterações manuais nesse tipo de coleção.|  
|Regra de consulta|As regras de consulta atualizam dinamicamente a associação de uma coleção com base em uma consulta executada pelo Configuration Manager em um agendamento. Por exemplo, é possível criar uma coleção de usuários que são membros da unidade organizacional dos Recursos Humanos nos Serviços de Domínio do Active Directory. Ao contrário das coleções de regra direta, essa associação de coleção é atualizada automaticamente quando novos usuários são adicionados ou removidos da unidade organizacional Recursos Humanos.<br /><br /> Por exemplo, consultas que você pode usar para criar coleções, consulte [Como criar consultas no System Center Configuration Manager](../../../../core/servers/manage/create-queries.md).|  
|Regra de coleção de inclusão|A regra de coleta de inclusão permite incluir os membros de outra coleção em uma coleção do Configuration Manager. A associação atual da coleção atual será atualizada em um agendamento se a associação da coleção incluída tiver mudado.<br /><br /> Você pode adicionar várias regras de coleção de inclusão a uma coleção.<br />              **Exemplo:** você cria uma coleção que tem duas regras de coleção de inclusão. A primeira regra de coleção de inclusão destina-se a uma coleção de laptops e a segunda regra de coleção é uma coleção de desktops. A nova coleção conterá todos os membros da coleção de laptops e da coleção de desktops.|  
|Regra de coleção de exclusão|A regra de coleta de exclusão permite que você exclua os membros de outra coleção de uma coleção do Configuration Manager. A associação da coleção atual será atualizada em um agendamento se a associação da coleção excluída tiver mudado.<br /><br /> Você pode adicionar várias regras de coleção de exclusão a uma coleção. Se uma coleção incluir regras de coleção de inclusão e de coleção de exclusão e houver um conflito, a regra de coleção de exclusão terá prioridade sobre a regra de coleção de inclusão.<br />              **Exemplo:** você cria uma coleção que contém uma regra de coleção de inclusão e uma regra de coleção de exclusão. A regra de coleção de inclusão destina-se a uma coleção de desktops da Dell. A coleção de exclusão destina-se a uma coleção de computadores com menos de 4 GB de RAM. A nova coleção conterá desktops da Dell que têm, pelo menos, 4 GB de RAM.|  

 Use os procedimentos a seguir para ajudá-lo a criar coleções no Configuration Manager. Também é possível importar coleções que foram criadas neste ou em outro site do Configuration Manager. Para obter informações sobre como exportar coleções, consulte [Como gerenciar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md).  

 Para obter informações sobre como criar coleções para computadores com Linux e UNIX, consulte [Como gerenciar clientes para servidores Linux e UNIX no System Center Configuration Manager](../../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md).  

##  <a name="a-namebkmk1a-to-create-a-device-collection"></a><a name="BKMK_1"></a> Para criar uma coleção de dispositivos  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Coleções de Dispositivos**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Coleção de Dispositivos**.  

4.  Na página **Geral** do **Assistente para Criar Coleção de Dispositivos**, especifique as seguintes informações:  

    -   **Nome**: especifique um nome exclusivo para a coleção.  

    -   **Comentário**: especifique uma descrição para a coleção.  

    -   **Limitação de coleção**: clique em **Procurar** para selecionar uma limitação de coleção. A coleção que você está criando conterá somente os membros da coleção de limitação.  

5.  Na página **Regras de Associação** do **Assistente para Criar Coleção de Dispositivos**, especifique as seguintes informações:  

    -   Na lista **Adicionar Regra** , selecione o tipo de regra de associação que deseja usar para esta coleção. É possível configurar várias regras para cada coleção.  

         Use os procedimentos a seguir para configurar cada tipo de regra de associação.  

        ##### <a name="to-configure-a-direct-rule"></a>Para configurar uma regra direta  

        1.  Na página **Pesquisar Recursos** do **Assistente para Criar Regra de Associação Direta**, especifique as seguintes informações:  

            -   **Classe de recurso**: na lista, selecione o tipo de recurso que deseja pesquisar e adicionar à coleção. Selecione um dos valores de **Recursos do Sistema** para pesquisar dados de inventário retornados de computadores cliente ou **Computador Desconhecido** para selecionar valores retornados por computadores desconhecidos.  

            -   **Nome do atributo**: na lista, selecione o atributo associado à classe de recurso selecionada que você deseja pesquisar. Por exemplo, se quiser selecionar computadores por seu nome NetBIOS, selecione **Recurso do Sistema** na lista **Classe de recurso** e **Nome NetBIOS** na lista **Nome do atributo** .  

            -   **Excluir recursos marcados como obsoletos** – se um computador cliente estiver marcado como obsoleto, não inclua esse valor nos resultados da pesquisa.  

            -   **Excluir recursos que não têm o cliente do Configuration Manager instalado** – se os resultados da pesquisa incluírem um recurso que não tem um cliente do Configuration Manager instalado, esse valor não será exibido nos resultados da pesquisa.  

            -   **Valor:** insira um valor que deseja procurar no nome do atributo selecionado. Você pode usar o caractere de porcentagem **%** como um curinga. Por exemplo, se você desejar pesquisar computadores que têm um nome NetBIOS que começa com “M”, digite **M%** nesse campo.  

        2.  Na página **Selecionar Recursos** do **Assistente para Criar Regra de Associação Direta**, selecione os recursos que você deseja adicionar à coleção na lista **Recursos** e clique em **Avançar**.  

        3.  Conclua o **Assistente para Criar Regra de Associação Direta**.  

        ##### <a name="to-configure-a-query-rule"></a>Para configurar uma regra de consulta  

        1.  Na caixa de diálogo **Propriedades de Regra de Consulta** , especifique as seguintes informações:  

            -   **Nome**: especifique um nome exclusivo para a regra de consulta.  

            -   **Importar Instrução de Consulta** – Abre a caixa de diálogo **Procurar Consulta**, em que é possível selecionar uma consulta do Configuration Manager a ser usada como a regra de consulta para a coleção. Para obter mais informações sobre como criar essas consultas e alguns exemplos, consulte [Como criar consultas no System Center Configuration Manager](../../../../core/servers/manage/create-queries.md).  

            -   **Classe de recurso:** na lista, selecione o tipo de recurso que deseja pesquisar e adicionar à coleção. Selecione um dos valores de **Recursos do Sistema** para pesquisar dados de inventário retornados de computadores cliente ou **Computador Desconhecido** para selecionar valores retornados por computadores desconhecidos.  

            -   **Editar Instrução de Consulta** – Abre a caixa de diálogo **	Propriedades da Instrução da Consulta**, em que é possível criar uma consulta a ser usada como a regra para a coleção. Para obter mais informações sobre consultas, consulte [Referência técnica de consultas no System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

        2.  Clique em **OK** para fechar a caixa de diálogo **Propriedades de Instrução de Consulta** e salvar a regra de associação da consulta.  

        ##### <a name="to-configure-an-include-collection-rule"></a>Para configurar uma regra de coleção de inclusão  

        1.  Na caixa de diálogo **Selecionar Coleções** , selecione as coleções que você deseja incluir na nova coleção.  

        2.  Clique em **OK** para fechar a caixa de diálogo **Selecionar Coleções** e salvar a regra de associação de inclusão.  

        ##### <a name="to-configure-an-exclude-collection-rule"></a>Para configurar uma regra de coleção de exclusão  

        1.  Na caixa de diálogo **Selecionar Coleções** , selecione as coleções que você deseja excluir da nova coleção.  

        2.  Clique em **OK** para fechar a caixa de diálogo **Selecionar Coleções** e salvar a regra de associação de exclusão.  

    -   **Usar atualizações incrementais para esta coleção** – Selecione esta opção para examinar periodicamente apenas recursos novos ou alterados da avaliação da coleção anterior e atualizar a associação da coleção apenas com esses recursos, independentemente de uma avaliação completa da coleção. Atualizações incrementais ocorrem em intervalos de 10 minutos.  

        > [!IMPORTANT]  
        >  As coleções configuradas usando regras de consulta que usam as seguintes classes não dão suporte a atualizações incrementais:  
        >   
        >  -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (somente para coleções de usuários)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (somente para coleções de usuários)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    -   **Agendar uma atualização completa para esta coleção** – Selecione esta opção para agendar uma avaliação completa regular da associação da coleção.  

6.  Conclua o assistente para criar a nova coleção. A nova coleção é exibida no nó **Coleções de Dispositivos** do espaço de trabalho **Ativos e Conformidade** .  

> [!NOTE]  
>  É necessário atualizar ou recarregar o console do Configuration Manager para ver os membros da coleção. No entanto, os membros não aparecerão na coleção até após a primeira atualização agendada ou selecionar manualmente **Atualizar Associação** para a coleção. Dependendo da complexidade da regra de coleta e do número de entradas no banco de dados do Configuration Manager, pode levar alguns minutos para concluir uma atualização da coleta.  

##  <a name="a-namebkmk2a-to-create-a-user-collection"></a><a name="BKMK_2"></a> Para criar uma coleção de usuários  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Coleções de Usuários**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Coleção de Usuários**.  

4.  Na página **Geral** do **Assistente para Criar Coleção de Usuários**, especifique as seguintes informações:  

    -   **Nome**: especifique um nome exclusivo para a coleção.  

    -   **Comentário**: especifique uma descrição para a coleção.  

    -   **Limitação de coleção**: clique em **Procurar** para selecionar uma limitação de coleção. A coleção que você está criando conterá somente os membros da coleção de limitação.  

5.  Na página **Regras de Associação** do **Assistente para Criar Coleção de Usuários**, especifique as seguintes informações:  

    -   Na lista **Adicionar Regra** , selecione o tipo de regra de associação que deseja usar para esta coleção. É possível configurar várias regras para cada coleção.  

         Use os procedimentos a seguir para configurar cada tipo de regra de associação.  

        ##### <a name="to-configure-a-direct-rule"></a>Para configurar uma regra direta  

        1.  Na página **Pesquisar Recursos** do **Assistente para Criar Regra de Associação Direta**, especifique as seguintes informações:  

            -   **Classe de recurso**: na lista, selecione o tipo de recurso que deseja pesquisar e adicionar à coleção. Selecione os valores de **Recurso de Usuário** para pesquisar informações de usuário coletadas pelo Configuration Manager ou de **Recurso do Grupo de Usuários** para pesquisar informações de grupo de usuários coletadas pelo Configuration Manager.  

            -   **Nome do atributo**: na lista, selecione o atributo associado à classe de recurso selecionada que você deseja pesquisar. Por exemplo, se quiser selecionar os usuários por nome de UO (Unidade Organizacional), selecione **Recurso de Usuário** na lista **Classe de recurso** e **Nome de UO de usuário** na lista **Nome do atributo** .  

            -   **Valor:** insira um valor que deseja procurar no nome do atributo selecionado. Você pode usar o caractere de porcentagem **%** como um curinga. Por exemplo, se quiser pesquisar usuários na UO da Contoso, digite **Contoso** neste campo.  

        2.  Na página **Selecionar Recursos** do **Assistente para Criar Regra de Associação Direta**, selecione os recursos que você deseja adicionar à coleção na lista **Recursos** e clique em **Avançar**.  

        3.  Conclua o **Assistente para Criar Regra de Associação Direta**.  

        ##### <a name="to-configure-a-query-rule"></a>Para configurar uma regra de consulta  

        1.  Na caixa de diálogo **Propriedades de Regra de Consulta** , especifique as seguintes informações:  

            -   **Nome**: especifique um nome exclusivo para a regra de consulta.  

            -   **Importar Instrução de Consulta** – Abre a caixa de diálogo **Procurar Consulta**, em que é possível selecionar uma consulta do Configuration Manager a ser usada como a regra de consulta para a coleção. Para obter mais informações sobre consultas, consulte [Referência técnica de consultas no System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

            -   **Classe de recurso**: na lista, selecione o tipo de recurso que deseja pesquisar e adicionar à coleção. Selecione os valores de **Recurso de Usuário** para pesquisar informações de usuário coletadas pelo Configuration Manager ou de **Recurso do Grupo de Usuários** para pesquisar informações de grupo de usuários coletadas pelo Configuration Manager.  

            -   **Editar Instrução de Consulta** – Abre a caixa de diálogo **	Propriedades da Instrução da Consulta**, em que é possível criar uma consulta a ser usada como a regra para a coleção. Para obter mais informações sobre consultas, consulte [Referência técnica de consultas no System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

        2.  Clique em **OK** para fechar a caixa de diálogo **Propriedades de Instrução de Consulta** e salvar a regra de associação da consulta.  

        ##### <a name="to-configure-an-include-collection-rule"></a>Para configurar uma regra de coleção de inclusão  

        1.  Na caixa de diálogo **Selecionar Coleções** , selecione as coleções que você deseja incluir na nova coleção.  

        2.  Clique em **OK** para fechar a caixa de diálogo **Selecionar Coleções** e salvar a regra de associação de inclusão.  

        ##### <a name="to-configure-an-exclude-collection-rule"></a>Para configurar uma regra de coleção de exclusão  

        1.  Na caixa de diálogo **Selecionar Coleções** , selecione as coleções que você deseja excluir da nova coleção.  

        2.  Clique em **OK** para fechar a caixa de diálogo **Selecionar Coleções** e salvar a regra de associação de exclusão.  

    -   **Usar atualizações incrementais para esta coleção** – Selecione esta opção para examinar periodicamente apenas recursos novos ou alterados da avaliação da coleção anterior e atualizar a associação da coleção apenas com esses recursos, independentemente de uma avaliação completa da coleção. Atualizações incrementais ocorrem em intervalos de 10 minutos.  

        > [!IMPORTANT]  
        >  As coleções configuradas usando regras de consulta que usam as seguintes classes não dão suporte a atualizações incrementais:  
        >   
        >  -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (somente para coleções de usuários)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (somente para coleções de usuários)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    -   **Agendar uma atualização completa para esta coleção** – Selecione esta opção para agendar uma avaliação completa regular da associação da coleção.  

6.  Conclua o assistente para criar a nova coleção. A nova coleção é exibida no nó **Coleções de Usuários** do espaço de trabalho **Ativos e Conformidade** .  

> [!NOTE]  
>  É necessário atualizar ou recarregar o console do Configuration Manager para ver os membros da coleção. No entanto, os membros não aparecerão na coleção até após a primeira atualização agendada ou selecionar manualmente **Atualizar Associação** para a coleção. Dependendo da complexidade da regra de coleta e do número de entradas no banco de dados do Configuration Manager, pode levar alguns minutos para concluir uma atualização da coleta.  

##  <a name="a-namebkmk3a-to-import-a-collection"></a><a name="BKMK_3"></a> Para importar uma coleção  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Coleções de Usuários** ou **Coleções de Dispositivos**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Importar Coleções**.  

4.  Na página **Geral** do **Assistente para Importar Coleções**, clique em **Avançar**.  

5.  Na página **Nome do Arquivo MOF** , clique em **Procurar** e navegue até o arquivo MOF que contém as informações de coleção que você deseja importar.  

    > [!NOTE]  
    >  O arquivo que você deseja importar deve ter sido exportado de um site que executa a mesma versão do Configuration Manager que esse. Para obter mais informações sobre como exportar coleções, consulte [Como gerenciar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md).  

6.  Conclua o assistente para importar a coleção. A nova coleção é exibida no nó **Coleções de Usuários** ou **Coleções de Dispositivos** do espaço de trabalho **Ativos e Conformidade** .  

> [!NOTE]  
>  É necessário atualizar ou recarregar o console do Configuration Manager para ver os membros da coleção recém-importada.  



<!--HONumber=Dec16_HO3-->


