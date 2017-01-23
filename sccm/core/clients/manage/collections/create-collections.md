---
title: "Criar coleções | Microsoft Docs"
description: "Crie coleções no System Center Configuration Manager para gerencie mais facilmente os grupos de usuários e dispositivos."
ms.custom: na
ms.date: 12/27/2016
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
ms.sourcegitcommit: 9555a16d97224a1cf49a426ab225468b07403f60
ms.openlocfilehash: e28fdeae809cadf78017dd2920e3f1a9484ec8a3


---
# <a name="how-to-create-collections-in-system-center-configuration-manager"></a>Como criar coleções no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Coleções são grupos de usuários ou dispositivos. Use coleções para tarefas como gerenciamento de aplicativos, configurações de conformidade de implantação ou instalação de atualizações de software. Você também pode usar coleções para gerenciar grupos de configurações do cliente ou usá-las com a administração baseada em funções para especificar os recursos que um usuário administrativo pode acessar. O Configuration Manager contém várias coleções internas. Para obter mais informações, consulte [Introdução às coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).  

> [!NOTE]  
>  Uma coleção pode conter usuários ou dispositivos, mas não ambos.  

 A tabela a seguir lista as regras que você pode usar para configurar os membros de uma coleção no Configuration Manager.  

|Tipo de regra de associação|Mais informações|  
|--------------------------|----------------------|  
|Regra direta|Use para escolher os usuários ou computadores que você deseja adicionar a uma coleção. Esta associação não é alterada a menos que você remova um recurso do Configuration Manager. O Configuration Manager deve ter descoberto os recursos ou é necessário importar os recursos antes de poder adicioná-los a uma coleção de regra direta. As coleções de regras diretas têm uma maior sobrecarga administrativa que as coleções de regras de consulta, porque requerem alterações manuais.|  
|Regra de consulta|Atualizam dinamicamente a associação de uma coleção com base em uma consulta executada pelo Configuration Manager em um agendamento. Por exemplo, é possível criar uma coleção de usuários que são membros da unidade organizacional dos Recursos Humanos nos Serviços de Domínio do Active Directory. Essa coleção é atualizada automaticamente quando novos usuários são adicionados ou removidos da unidade organizacional Recursos Humanos.<br /><br /> Por exemplo, consultas que você pode usar para criar coleções, consulte [Como criar consultas no System Center Configuration Manager](../../../../core/servers/manage/create-queries.md).|  
|Regra de coleção de inclusão|Incluir os membros de outra coleção em uma coleção do Configuration Manager. A associação atual da coleção atual será atualizada em um agendamento se a coleção incluída for alterada.<br /><br /> Você pode adicionar várias regras de coleção de inclusão a uma coleção.<br /> |  
|Regra de coleção de exclusão|A regra de coleta de exclusão permite que você exclua os membros de outra coleção de uma coleção do Configuration Manager. A associação da coleção atual será atualizada em um agendamento se a coleção excluída for alterada.<br /><br /> Você pode adicionar várias regras de coleção de exclusão a uma coleção. Se uma coleção incluir regras de coleção de inclusão e de coleção de exclusão e houver um conflito, a regra de coleção de exclusão terá prioridade.<br />              **Exemplo:** você cria uma coleção que contém uma regra de coleção de inclusão e uma regra de coleção de exclusão. A regra de coleção de inclusão destina-se a uma coleção de desktops da Dell. A coleção de exclusão destina-se a uma coleção de computadores com menos de 4 GB de RAM. A nova coleção conterá desktops da Dell que têm, pelo menos, 4 GB de RAM.|  

 Use os procedimentos a seguir para ajudá-lo a criar coleções no Configuration Manager. Também é possível importar coleções que foram criadas neste ou em outro site do Configuration Manager. Para obter informações sobre como exportar e importar coleções, consulte [Como gerenciar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md).  

 Para obter informações sobre como criar coleções para computadores com Linux e UNIX, consulte [Como gerenciar clientes para servidores Linux e UNIX no System Center Configuration Manager](../../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md).  

##  <a name="a-namebkmk1a-to-create-a-device-collection"></a><a name="BKMK_1"></a> Para criar uma coleção de dispositivos  

1.  No console do Configuration Manager, escolha **Ativos e Conformidade** > **Coleções de Dispositivos**.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Coleção de Dispositivos**.  

4.  Na página **Geral** forneça um **Nome** e um **Comentário**. Em seguida, em **Limitação de coleção**, escolha **Procurar** para selecionar uma limitação de coleção. A coleção conterá somente os membros da coleção de limitação.  

5.  Na página **Regras de Associação** do **Assistente de Criação de Coleção de Dispositivos**, na lista **Adicionar Regra**, selecione o tipo de regra de associação que você deseja usar para esta coleção. É possível configurar várias regras para cada coleção.  

        
        ##### To configure a direct rule  

        1.  Na página **Pesquisar Recursos** do **Assistente para Criar Regra de Associação Direta**, especifique as seguintes informações:  

            -   **Classe de recurso**: selecione o tipo de recurso que você deseja pesquisar e adicione à coleção. Selecione um dos valores de **Recursos do Sistema** para pesquisar dados de inventário retornados de computadores cliente ou **Computador Desconhecido** para selecionar valores retornados por computadores desconhecidos.  

            -   **Nome do atributo**: selecione o atributo associado à classe de recurso selecionada que você deseja pesquisar. Por exemplo, se quiser selecionar computadores por seu nome NetBIOS, selecione **Recurso do Sistema** na lista **Classe de recurso** e **Nome NetBIOS** na lista **Nome do atributo** .  

            -   **Excluir recursos marcados como obsoletos** – se um computador cliente estiver marcado como obsoleto, não inclua esse valor nos resultados da pesquisa.  

            -   **Excluir recursos que não têm o cliente do Configuration Manager instalado** – eles não serão exibidos nos resultados da pesquisa.  

            -   **Valor:** insira um valor que deseja procurar no nome do atributo selecionado. Você pode usar o caractere de porcentagem **%** como um curinga. Por exemplo, para pesquisar computadores que têm um nome NetBIOS que começa com “M”, digite **M%** nesse campo.  

        2.  Na página **Selecionar Recursos**, selecione os recursos que você deseja adicionar à coleção na lista **Recursos** e escolha **Avançar**.  


        ##### To configure a query rule  

        1.  Na caixa de diálogo **Propriedades de Regra de Consulta** , especifique as seguintes informações:  

            -   **Nome**: especifique um nome exclusivo.  

            -   **Importar Instrução de Consulta** – Abre a caixa de diálogo **Procurar Consulta**, em que é possível selecionar uma [consulta do Configuration Manager](../../../../core/servers/manage/create-queries.md) a ser usada como a regra de consulta para a coleção.   

            -   **Classe de recurso:** selecione o tipo de recurso que você deseja pesquisar e adicione à coleção. Selecione um dos valores de **Recursos do Sistema** para pesquisar dados de inventário retornados de computadores cliente ou **Computador Desconhecido** para selecionar valores retornados por computadores desconhecidos.  

            -   **Editar Instrução de Consulta** – Abre a caixa de diálogo **	Propriedades da Instrução da Consulta**, em que é possível criar uma consulta a ser usada como a regra para a coleção. Para obter mais informações sobre consultas, consulte [Referência técnica de consultas no System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

    
        ##### To configure an include collection rule  

        In the **Select Collections** dialog box, select the collections you want to include in the new collection, then choose **OK**.  

        ##### To configure an exclude collection rule  

        In the **Select Collections** dialog box, select the collections you want to exclude from the new collection, then choose **OK**.  

    -   **Usar atualizações incrementais para esta coleção** – Selecione esta opção para examinar periodicamente apenas recursos novos ou alterados da avaliação da coleção anterior, independentemente de uma avaliação completa da coleção. Atualizações incrementais ocorrem em intervalos de 10 minutos.  

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

    -   **Agendar uma atualização completa para esta coleção** – Agende uma avaliação completa regular da associação da coleção.  

6.  Conclua o assistente para criar a nova coleção. A nova coleção é exibida no nó **Coleções de Dispositivos** do espaço de trabalho **Ativos e Conformidade** .  

> [!NOTE]  
>  É necessário atualizar ou recarregar o console do Configuration Manager para ver os membros da coleção. No entanto, os membros não aparecerão na coleção até depois da primeira atualização agendada ou se você selecionar manualmente **Atualizar Associação** para a coleção. Pode levar alguns minutos para concluir uma atualização da coleção.  

##  <a name="a-namebkmk2a-to-create-a-user-collection"></a><a name="BKMK_2"></a> Para criar uma coleção de usuários  

1.  No console do Configuration Manager, escolha **Ativos e Conformidade** > **Coleções de Usuários**.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Coleção do Usuário**.  

4.  Na página **Geral** do assistente, forneça um **Nome** e um **Comentário**. Em seguida, em **Limitação de coleção**, escolha **Procurar** para selecionar uma limitação de coleção. A coleção que você está criando conterá somente os membros da coleção de limitação.  

5.  Na página **Regras de Associação**, especifique o seguinte:  

    -   Na lista **Adicionar Regra** , selecione o tipo de regra de associação que deseja usar para esta coleção. É possível configurar várias regras para cada coleção.  

         ##### <a name="to-configure-a-direct-rule"></a>Para configurar uma regra direta  

        1.  Na página **Pesquisar Recursos** do **Assistente de Criação de Regra de Associação Direta**, especifique:  

            -   **Classe de recurso**: selecione o tipo de recurso que você deseja pesquisar e adicione à coleção. Selecione os valores de **Recurso de Usuário** para pesquisar informações de usuário coletadas pelo Configuration Manager ou de **Recurso do Grupo de Usuários** para pesquisar informações de grupo de usuários coletadas pelo Configuration Manager.  

            -   **Nome do atributo**: selecione o atributo associado à classe de recurso que você deseja pesquisar. Por exemplo, se quiser selecionar os usuários por nome de UO (Unidade Organizacional), selecione **Recurso de Usuário** na lista **Classe de recurso** e **Nome de UO de usuário** na lista **Nome do atributo** .  

            -   **Valor:** insira um valor que você deseja pesquisar. Você pode usar o caractere de porcentagem **%** como um curinga. Por exemplo, para pesquisar usuários na UO da Contoso, digite **Contoso** neste campo.  

        2.  Na página **Selecionar Recursos**, selecione os recursos que você deseja adicionar à coleção na lista **Recursos**.  

        ##### <a name="to-configure-a-query-rule"></a>Para configurar uma regra de consulta  

        1.  Na caixa de diálogo **Propriedades da Regra de consulta**, forneça:  

            -   **Nome**: um nome exclusivo.  

            -   **Importar Instrução de Consulta** – Abre a caixa de diálogo **Procurar Consulta**, em que é possível selecionar uma [consulta do Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md) a ser usada como a regra de consulta para a coleção.  

            -   **Classe de recurso**: selecione o tipo de recurso que você deseja pesquisar e adicione à coleção. Selecione os valores de **Recurso de Usuário** para pesquisar informações de usuário coletadas pelo Configuration Manager ou de **Recurso do Grupo de Usuários** para pesquisar informações de grupo de usuários coletadas pelo Configuration Manager.  

            -   **Editar Instrução de Consulta** – Abre a caixa de diálogo **Propriedades da Instrução da Consulta**, em que é possível [criar uma consulta](../../../../core/servers/manage/queries-technical-reference.md) a ser usada como a regra para a coleção.  

        ##### <a name="to-configure-an-include-collection-rule"></a>Para configurar uma regra de coleção de inclusão  

        Na caixa de diálogo **Selecionar Coleções**, selecione as coleções que você deseja incluir na nova coleção e, em seguida, escolha **OK**.  

        ##### <a name="to-configure-an-exclude-collection-rule"></a>Para configurar uma regra de coleção de exclusão  

        Na caixa de diálogo **Selecionar Coleções**, selecione as coleções que você deseja excluir da nova coleção e, em seguida, escolha **OK**.  


    -   **Usar atualizações incrementais para esta coleção** – Selecione esta opção para examinar periodicamente apenas recursos novos ou alterados da avaliação da coleção anterior, independentemente de uma avaliação completa da coleção. Atualizações incrementais ocorrem em intervalos de 10 minutos.  

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

    -   **Agendar uma atualização completa para esta coleção** – Agende uma avaliação completa regular da associação da coleção.  

6.  Conclua o assistente. A nova coleção é exibida no nó **Coleções de Usuários** do espaço de trabalho **Ativos e Conformidade** .  

> [!NOTE]  
>  É necessário atualizar ou recarregar o console do Configuration Manager para ver os membros da coleção. No entanto, os membros não aparecerão na coleção até após a primeira atualização agendada ou selecionar manualmente **Atualizar Associação** para a coleção. Pode levar alguns minutos para concluir uma atualização da coleção.  

##  <a name="a-namebkmk3a-to-import-a-collection"></a><a name="BKMK_3"></a> Para importar uma coleção  

1.  No console do Configuration Manager, escolha **Ativos e Conformidade** > **Coleções de Usuários** ou **Coleções de Dispositivos**.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Importar Coleções**.  

4.  Na página **Geral** do **Assistente de Importação de Coleções**, escolha **Avançar**.  

5.  Na página **Nome do Arquivo MOF**, escolha **Procurar** e, em seguida, navegue até o arquivo MOF que contém as informações de coleção que você deseja importar.  

    > [!NOTE]  
    >  O arquivo que você deseja importar deve ter sido exportado de um site que executa a mesma versão do Configuration Manager que esse. Para obter mais informações sobre como exportar coleções, consulte [Como gerenciar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md).  

6.  Conclua o assistente para importar a coleção. A nova coleção é exibida no nó **Coleções de Usuários** ou **Coleções de Dispositivos** do espaço de trabalho **Ativos e Conformidade** . Atualize ou recarregue o console do Configuration Manager para ver os membros da coleção recém-importada.  



<!--HONumber=Dec16_HO5-->


