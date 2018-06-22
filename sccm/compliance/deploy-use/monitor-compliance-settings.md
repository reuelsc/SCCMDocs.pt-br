---
title: Monitorar as configurações de conformidade
titleSuffix: Configuration Manager
description: Use um ou mais dos procedimentos deste tópico para exibir o status de conformidade da linha de base de configuração.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 92c1ccca-a748-44cd-a52e-e41d34bf981d
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 9920bd48ad7b953469261602c21a6664580143a2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32335772"
---
# <a name="monitor-compliance-settings-in-system-center-configuration-manager"></a>Monitorar as configurações de conformidade no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Depois de as implantar linhas de base de configuração do System Center Configuration Manager em dispositivos na sua hierarquia, você pode usar um ou mais dos procedimentos deste tópico para exibir o status de conformidade da linha de base de configuração:

> [!NOTE]  
>  Os campos de critérios de validação nos relatórios de configurações de conformidade (o equivalente no relatório do lado do cliente é **Restrições**) exibem o SML subjacente (Service Modeling Language). Isso pode dificultar para os administradores que criaram o item de configuração no console do Configuration Manager entenderem quais são os critérios de validação, caso não tenham conhecimento do SML. Nesse caso, use o espaço de trabalho **Monitoramento** do console do Configuration Manager para exibir as propriedades do item de configuração e seus critérios de validação.  

##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Exibir resultados de conformidade no console do Configuration Manager  
 Use este procedimento para exibir detalhes sobre a conformidade das linhas de base de configuração implantadas no console do Configuration Manager.  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>Exibir resultados de conformidade no console do Configuration Manager  

1.  No console do Configuration Manager, clique em **Monitoramento** > **Implantações**.  

3.  Na lista **Implantações** , selecione a implantação de linha de base de configuração da qual deseja examinar as informações de conformidade.  

4.  Você pode examinar as informações de resumo sobre a conformidade da implantação da linha de base de configuração na página principal. Para exibir informações mais detalhadas, selecione a implantação de linha de base de configuração e, na guia **Início** , no grupo **Implantação** , clique em **Exibir Status** para abrir a página **Status da Implantação** .  

     A página **Status da Implantação** contém as seguintes guias:  

    -   **Compatível**: exibe a conformidade da linha de base de configuração com base no número de ativos afetados. É possível clicar em uma regra para criar um nó temporário no nó **Usuários** ou **Dispositivos** que estão localizados no espaço de trabalho **Ativos e Conformidade** , que contém todos os usuários ou dispositivos que são compatíveis com esta regra. O painel **Detalhes do Ativo** exibe os usuários e os dispositivos compatíveis com a linha de base de configuração. Clique duas vezes em um usuário dispositivo na lista para exibir informações adicionais.  

        > [!IMPORTANT]  
        >  Uma regra de item de configuração não será avaliada se não for detectada nem aplicável em um dispositivo cliente; no entanto, será retornada como compatível.  

    -   **Erro**: exibe uma lista de todos os erros da implantação da linha de base de configuração selecionada com base no número de ativos afetados. É possível clicar em uma regra para criar um nó temporário no nó **Usuários** ou **Dispositivos** do espaço de trabalho **Ativos e Conformidade** , que contém todos os usuários ou dispositivos que geraram erros com esta regra. Ao selecionar um usuário ou dispositivo, o painel **Detalhes do Ativo** exibe os usuários ou os dispositivos afetados pelo problema selecionado. Clique duas vezes em um usuário ou dispositivo na lista para exibir informações adicionais sobre o problema.  

    -   **Não Compatível**: exibe uma lista de todas as regras não compatíveis na linha de base de configuração com base no número de ativos afetados. É possível clicar em uma regra para criar um nó temporário no nó **Usuários** ou **Dispositivos** do espaço de trabalho **Ativos e Conformidade** , que contém todos os usuários ou dispositivos que não são compatíveis com esta regra. Ao selecionar um usuário ou dispositivo, o painel **Detalhes do Ativo** exibe os usuários ou os dispositivos afetados pelo problema selecionado. Clique duas vezes em um usuário ou dispositivo na lista para exibir informações adicionais sobre o problema.  

    -   **Desconhecido**: exibe uma lista de todos os usuários e dispositivos que não relataram a conformidade para a implantação da linha de base de configuração selecionada, junto com o status atual do cliente dos dispositivos.  

5.  Na página **Status da Implantação** , você pode examinar informações detalhadas sobre a conformidade da linha de base de configuração implantada. Um nó temporário é criado no nó **Implantações** , que ajuda você a localizar essas informações novamente com rapidez.  

##  <a name="view-compliance-results-by-using-reports"></a>Exibir resultados de conformidade por meio de relatórios  
 As configurações de conformidade no Configuration Manager incluem diversos relatórios internos que permitem monitorar informações sobre itens de configuração, linhas de base de configuração e implantações. Esses relatórios têm a categoria de relatório de **Gerenciamento de Conformidade e Configurações**.  

> [!IMPORTANT]  
>  Você deverá usar um caractere curinga (**%**) ao usar os parâmetros **Filtro de dispositivo** e Filtro de usuário nos relatórios de configurações de conformidade.  

 Para obter mais informações sobre como configurar relatórios no Configuration Manager, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md)  

##  <a name="view-compliance-results-on-a-configuration-manager-windows-client-computer"></a>Para exibir os resultados de conformidade em um computador cliente Windows do Configuration Manager

> [!NOTE]  
>  Não será possível exibir informações sobre o cliente Windows do Configuration Manager se você estiver conectado com uma conta de domínio Convidado.    

1.  Navegue até **Configuration Manager** no Painel de Controle do computador cliente e clique duas vezes para abrir suas propriedades.  

2.  Clique na guia **Configurações** e exiba a lista de linhas de base de configuração implantadas.  

3.  Exibir o **Estado de Conformidade** para cada linha de base de configuração:  

    > [!IMPORTANT]  
    >  Os resultados da avaliação são armazenados em cache por 15 minutos. Se você iniciar uma reavaliação no período de 15 minutos, os resultados de conformidade serão retornados desse cache em vez de uma nova avaliação. Portanto, se você fizer uma alteração no cliente que possa afetar os resultados da avaliação de conformidade, aguarde 15 minutos antes de iniciar uma reavaliação.  

    -   **Compatível**: o computador cliente está em conformidade com a linha de base de configuração avaliada.  

    -   **Não Compatível**: o computador cliente não está em conformidade com a linha de base de configuração avaliada.  

    -   **Desconhecido**: o computador cliente ainda não avaliou a linha de base de configuração. Se deseja iniciar a avaliação fora do agendamento de avaliação de conformidade, selecione as linhas de base de configuração a ser avaliadas e clique em **Avaliar**.  

        > [!NOTE]  
        >  Se você tiver credenciais de administrador local no computador cliente, é possível exibir detalhes de cada linha de base de configuração avaliada para determinar qual item de configuração está relatando um status não compatível. Para fazer isso, selecione a linha de base de configuração e clique em **Exibir Relatório**.  

4.  Clique em **OK**.  

##  <a name="create-collections-based-on-configuration-baseline-compliance"></a>Criar coleções baseadas na conformidade da linha de base de configuração  
 Use o procedimento a seguir para criar uma coleção do Configuration Manager com base em dispositivos com uma conformidade especificada. É possível criar coleções com base nos seguintes estados de conformidade:  

-   **Compatível**  

-   **Erro**  

-   **Non-compliant**  

-   **Desconhecida**  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Linhas de Base de Configuração**.  

3.  Na lista **Linhas de Base de Configuração** , selecione a linha de base por meio da qual você deseja criar uma coleção.  

4.  Na guia **Implantação** , no **Grupo de Implantação**, clique em **Criar Nova Coleção** e, na lista suspensa, selecione o nível de conformidade para o qual deseja criar uma coleção.  

5.  O **Assistente para Criar Coleção de Usuários** ou o **Assistente para Criar Coleção de Dispositivos** é aberto, dependendo se o item de configuração foi implantado em usuários ou dispositivos. O assistente é populado automaticamente com os valores corretos para criar a coleção; no entanto, é possível editar esses valores.  

6.  Depois de concluir o assistente, a coleção é exibida no nó **Coleções de Usuários** ou **Coleções de Dispositivos** do espaço de trabalho **Ativos e Conformidade** .  
