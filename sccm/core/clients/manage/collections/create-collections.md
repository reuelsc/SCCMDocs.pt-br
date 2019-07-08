---
title: Criar coleções
titleSuffix: Configuration Manager
description: Crie coleções no Configuration Manager para gerenciar mais facilmente os grupos de usuários e dispositivos.
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed08a9abb746681eb8e89d471e19990ced313788
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67550904"
---
# <a name="how-to-create-collections-in-configuration-manager"></a>Como criar coleções no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Coleções são grupos de usuários ou dispositivos. Use coleções para tarefas como gerenciar aplicativos, implantar configurações de conformidade ou instalar atualizações de software. Você também pode usar coleções para gerenciar grupos de configurações do cliente ou usá-las com a administração baseada em funções para especificar os recursos que um usuário administrativo pode acessar. O Configuration Manager contém várias coleções internas. Para mais informações, confira [Introduction to collections](/sccm/core/clients/manage/collections/introduction-to-collections) (Introdução às coleções).  

> [!NOTE]  
> Uma coleção pode conter usuários ou dispositivos, mas não ambos.  


As informações neste artigo podem ajudar a criar coleções no Configuration Manager. Também é possível importar coleções criadas neste site do Configuration Manager ou em outro site. Para saber mais sobre como exportar e importar coleções, confira [Como gerenciar coleções](/sccm/core/clients/manage/collections/manage-collections).  


## <a name="collection-rules"></a>Regras de coleção

É possível usar diferentes tipos de regras para configurar os membros de uma coleção no Configuration Manager.  


### <a name="direct-rule"></a>Regra direta

Use regras diretas para escolher os usuários ou os computadores que você deseja adicionar a uma coleção. Essa associação não muda, a menos que você remova um recurso do Configuration Manager. Antes de poder adicionar recursos a uma coleção de regras direta, o Configuration Manager deve ter descoberto ou importado esses recursos. As coleções de regras diretas têm uma maior sobrecarga administrativa do que as coleções de regras de consulta, pois exigem alterações manuais.


### <a name="query-rule"></a>Regra de consulta

Atualizam dinamicamente a associação de uma coleção com base em uma consulta executada pelo Configuration Manager em um agendamento. Por exemplo, é possível criar uma coleção de usuários que são membros da unidade organizacional dos Recursos Humanos nos Serviços de Domínio do Active Directory. Essa coleção é atualizada automaticamente quando novos usuários são adicionados ou removidos da unidade organizacional Recursos Humanos.

Para obter exemplos de consultas que você pode usar para compilar coleções, veja [Como criar consultas](/sccm/core/servers/manage/create-queries).


### <a name="device-category-rule"></a>Regra de categoria de dispositivo

Facilite o gerenciamento de dispositivos associando categorias de dispositivo com as coleções de dispositivos. 

Para saber mais, confira [Categorizar automaticamente dispositivos em coleções](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections).<!-- SCCMDocs issue 552 -->


### <a name="include-collection-rule"></a>Regra de coleção de inclusão

Inclua os membros de outra coleção em uma coleção do Configuration Manager. Se a coleção incluída mudar, o Configuration Manager atualizará a associação da coleção atual em um agendamento.

Você pode adicionar várias regras de coleção de inclusão a uma coleção.


### <a name="exclude-collection-rule"></a>Regra de coleção de exclusão

As regras de excluir coleção permitem excluir os membros de uma coleção de outra coleção do Configuration Manager. Se a coleção excluída mudar, o Configuration Manager atualizará a associação da coleção atual em um agendamento.

Você pode adicionar várias regras de coleção de exclusão a uma coleção. Se uma coleção incluir regras de inclusão e exclusão de coleção e houver um conflito, a regra de exclusão de coleção terá prioridade.

#### <a name="example"></a>Exemplo
você cria uma coleção que contém uma regra de coleção de inclusão e uma regra de coleção de exclusão. A regra de coleção de inclusão destina-se a uma coleção de desktops da Dell. A exclusão de coleção destina-se a uma coleção de computadores com menos de 4 GB de RAM. A nova coleção contém desktops da Dell com pelo menos 4 GB de RAM.



## <a name="bkmk_create"></a> Criar uma coleção  

1. No console do Configuration Manager, vá até o workspace **Ativos e conformidade**.  

    - Para criar uma *coleção de dispositivos*, selecione o nó **Coleções de Dispositivo**. Na guia **Página Inicial** da faixa de opções, no grupo **Criar**, selecione **Criar Coleção de Dispositivos**.  

    - Para criar uma *coleção de usuários*, selecione o nó **Coleções de Usuário**. Na guia **Página Inicial** da faixa de opções, no grupo **Criar**, selecione **Criar Coleção de Usuários**.  

2. Na página **Geral** do assistente, forneça um **Nome** e um **Comentário**. Na seção **Limitação de coleção**, selecione **Procurar** e selecione uma limitação de coleção. A coleção que você está criando conterá somente os membros da limitação de coleção.  

4. Na página **Regras de Associação**, na lista **Adicionar Regra**, selecione o tipo de regra de associação que você quer usar para a coleção. É possível configurar várias regras para cada coleção. A configuração de cada regra varia. Para saber mais sobre como configurar cada regra, confira as seções a seguir deste artigo:  
    - [Regra direta](#bkmk-direct)
    - [Regra de consulta](#bkmk-query)
    - [Regra de categoria de dispositivo](#bkmk-category)
    - [Regra de inclusão de coleção](#bkmk-include)
    - [Regra de exclusão de coleção](#bkmk-exclude)

5. Além disso, na página **Regras de Associação**, examine as seguintes configurações.

    - **Usar atualizações incrementais para esta coleção**: selecione essa opção para examinar e atualizar periodicamente somente recursos novos ou alterados da avaliação de coleção anterior. Esse processo é independente de uma avaliação completa da coleção. Por padrão, atualizações incrementais ocorrem em intervalos de cinco minutos.  

        > [!IMPORTANT]  
        >  As coleções com regras de consulta que usam as seguintes classes não dão suporte a atualizações incrementais:  
        >   
        > -   SMS_G_System_CollectedFile  
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

    - **Agendar uma atualização completa para esta coleção**: agende uma avaliação regular completa da associação da coleção.  

        Da versão 1810 em diante, estas alterações no comportamento da avaliação da coleção podem melhorar o desempenho do site:<!--3607726-->  

        - Anteriormente, quando você configurava um agendamento em uma coleção baseada em consulta, o site continuava a avaliar a consulta, independentemente de você ter ativado ou não a configuração de coleção para **Agendar uma atualização completa nesta coleção**. Para desabilitar totalmente o agendamento, era preciso alterá-lo para **Nenhum**.

            Agora o site remove o agendamento ao desabilitar essa configuração. Para especificar um agendamento para avaliação de coleção, ative a opção **Agendar uma atualização completa nesta coleção**.  

            Ao atualizar seu site, para qualquer coleção existente na qual você especificou um agendamento, o site ativa a opção para **Agendar uma atualização completa nesta coleção**. Embora essa configuração talvez não seja sua intenção, ela era o comportamento real da agenda antes de você atualizar o site. Para impedir que o site avalie uma coleção em um agendamento, desative essa opção.  

        - Você não pode desabilitar a avaliação de coleções internas como **Todos os sistemas**, mas agora pode configurar o agendamento. Esse comportamento permite que você personalize essa ação em um momento que atenda aos seus requisitos. 

            > [!TIP]  
            > Em coleções internas, altere somente o **Horário** do agendamento personalizado. Não altere o **Padrão de recorrência**. Futuras iterações podem impor um padrão de recorrência específico.  

6. Conclua o assistente para criar a nova coleção. A nova coleção é exibida no nó **Coleções de Dispositivos** do workspace **Ativos e Conformidade**.  

> [!NOTE]  
> É necessário atualizar ou recarregar o console do Configuration Manager para ver os membros da coleção. Eles não aparecem na coleção até a primeira atualização agendada ser executada. Você também pode selecionar manualmente **Atualizar Associação** para a coleção. Podem ser necessários alguns minutos para concluir uma atualização da coleção.  

        
### <a name="bkmk-direct"></a> Configurar uma regra direta  

1. Na página **Pesquisar Recursos** do **Assistente para Criar Regra de Associação Direta**, especifique as informações a seguir.  

    - **Classe de recurso**: selecione o tipo de recurso que você deseja pesquisar e adicione à coleção. Por exemplo:
        - **Recurso do Sistema**: pesquise dados de inventário retornados de computadores cliente.
        - **Computador Desconhecido**: selecione entre os valores retornados por computadores desconhecidos.
        - **Recursos de Usuário**: pesquise informações de usuário coletadas pelo Configuration Manager.
        - **Recurso do Grupo de Usuários**: pesquise informações de grupo de usuários coletadas pelo Configuration Manager.

    - **Nome do atributo**: selecione o atributo associado à classe de recurso selecionada que você deseja pesquisar. Por exemplo:  

        - Se quiser selecionar computadores por seu nome NetBIOS, selecione **Recurso do Sistema** na lista **Classe de recurso** e **Nome NetBIOS** na lista **Nome do atributo**.  

        - Se você desejar selecionar os usuários pelo nome da UO (unidade organizacional), selecione **Recurso de Usuário** na lista **Classe de recurso** e **Nome de UO do usuário** na lista **Nome do atributo**.  

    - **Excluir recursos marcados como obsoletos**: Se um computador cliente estiver marcado como obsoleto, não inclua esse valor nos resultados da pesquisa.  

    - **Excluir recursos que não têm o cliente do Configuration Manager instalado**: esses recursos não serão exibidos nos resultados da pesquisa.  

    - **Valor**: insira um valor de pesquisa no nome do atributo selecionado. Use o caractere de percentual (%) como curinga. Por exemplo:  
        - Para pesquisar computadores que têm um nome NetBIOS que começa com "M", insira **M%** nesse campo.  
        - Para pesquisar usuários na UO da Contoso, digite **Contoso** neste campo.

2. Na página **Selecionar Recursos**, selecione os recursos que você deseja adicionar à coleção na lista **Recursos** e selecione **Avançar**.  


### <a name="bkmk-query"></a> Configurar uma regra de consulta  

Na caixa de diálogo **Propriedades da Regra de Consulta**, especifique as seguintes informações.  

- **Nome**: Especifique um nome exclusivo para a consulta.  

- **Importar Instrução de Consulta**: abre a caixa de diálogo **Procurar Consulta**. Selecione uma [Consulta do Configuration Manager](/sccm/core/servers/manage/create-queries) para usar como a regra de consulta da coleção.   

- **Classe de recurso**: selecione o tipo de recurso que você deseja pesquisar e adicione à coleção. Selecione um dos valores de **Recursos do Sistema** para pesquisar dados de inventário retornados de computadores cliente ou de **Computador Desconhecido** para selecionar entre os valores retornados por computadores desconhecidos.  

- **Editar Instrução de Consulta**: abre a caixa de diálogo **Propriedades da Instrução da Consulta**, em que é possível escrever uma consulta a ser usada como a regra para a coleção. Para saber mais sobre consultas, confira [Introdução a consultas](/sccm/core/servers/manage/introduction-to-queries).  


### <a name="bkmk-category"></a> Regra de categoria de dispositivo

As seguintes ações estão disponíveis na janela **Selecionar Categorias de Dispositivo**.

- **Criar**: especifique um nome para criar uma nova categoria.
- **Renomear**: altere o nome da categoria selecionada.
- **Excluir**: selecione uma ou mais categorias e use essa ação para removê-las da lista.

Para saber mais, confira [Categorizar automaticamente dispositivos em coleções](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections).<!-- SCCMDocs issue 552 -->


### <a name="bkmk-include"></a> Configurar uma regra de inclusão de coleção  

Na caixa de diálogo **Selecionar Coleções**, selecione as coleções que você deseja incluir na nova coleção e, em seguida, selecione **OK**.  


### <a name="bkmk-exclude"></a> Configurar uma regra de exclusão de coleção  

Na caixa de diálogo **Selecionar Coleções**, selecione as coleções que você deseja excluir da nova coleção e, em seguida, selecione **OK**.  



## <a name="bkmk_import"></a> Importar uma coleção  

Quando você exporta uma coleção de um site, o Configuration Manager a salva como um arquivo MOF (Managed Object Format). Use este procedimento para importar esse arquivo para o banco de dados do seu site. Para concluir este procedimento, você precisa de permissões para **Criar** na classe de coleções.

> [!IMPORTANT]  
> - Verifique se o arquivo contém apenas dados de coleção, é de uma fonte confiável e não foi adulterado.  
> 
> - Verifique se o arquivo foi exportado de um site que executa a mesma versão do Configuration Manager que você está usando.  

Para saber mais sobre como exportar coleções, consulte [Como gerenciar coleções](/sccm/core/clients/manage/collections/manage-collections).


1. No console do Configuration Manager, vá até o workspace **Ativos e conformidade**. Selecione o nó **Coleções de Usuários** ou **Coleções de Dispositivos**.  

2. Na guia **Página Inicial** da faixa de opções, no grupo **Criar**, selecione **Importar Coleções**.  

3. Na página **Geral** do **Assistente de Importação de Coleções**, selecione **Avançar**.  

4. Na página **Nome do Arquivo MOF**, selecione **Procurar**. Procure o arquivo MOF que contém as informações de coleção que você deseja importar.  

5. Conclua o assistente para importar a coleção. A nova coleção é exibida no nó **Coleções de Usuários** ou **Coleções de Dispositivos** do workspace **Ativos e Conformidade**. Atualize ou recarregue o console do Configuration Manager para ver os membros da coleção recém-importada.  

## <a name="bkmk_powershell"></a> Uso do PowerShell

É possível usar o PowerShell para criar e importar coleções. Para obter mais informações, consulte:

* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Set-CMCollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Import-CMCollection)
