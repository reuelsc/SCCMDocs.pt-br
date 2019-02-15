---
title: Monitorar perfis de email, Wi-Fi e VPN
titleSuffix: Configuration Manager
description: Saiba como monitorar o status de conformidade de perfis de email, Wi-Fi e VPN no System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e2315b8b-98bc-40e1-8ef9-bfb5e69ab109
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49602002a789c0bd1e8d8cc128d3062fde9194fc
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137687"
---
# <a name="monitor-email-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Monitorar perfis de email, Wi-Fi e VPN no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Depois de implantar perfis de email, Wi-Fi ou VPN do System Center Configuration Manager para usuários na sua hierarquia, você poderá usar os seguintes procedimentos para monitorar o status de conformidade do perfil:  

-   [Como exibir resultados de conformidade no console do Configuration Manager](#BKMK_console)  

-   [Como exibir resultados de conformidade por meio de relatórios](#BKMK_Reports)  

##  <a name="BKMK_console"></a> Como exibir resultados de conformidade no console do Configuration Manager  
 Use este procedimento para exibir detalhes sobre a conformidade dos perfis implantados no console do System Center Configuration Manager.  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Para exibir resultados de conformidade no console do Configuration Manager  

1.  No console do System Center Configuration Manager, clique em **Monitoramento**.  

2.  No workspace **Monitoramento**, clique em **Implantações**.  

3.  Na lista **Implantações**, selecione a implantação de perfil para a qual você deseja examinar as informações de conformidade.  

4.  Você pode examinar as informações de resumo sobre a conformidade da implantação do perfil na página principal. Para exibir informações mais detalhadas, selecione a implantação do perfil e, na guia **Início**, no grupo **Implantação**, clique em **Exibir Status** para abrir a página **Status da Implantação**.  

     A página **Status da Implantação** contém as seguintes guias:  

    -   **Compatível:** exibe a conformidade do perfil com base no número de ativos afetados. Você pode clicar duas vezes em uma regra para criar um nó temporário no nó **Usuários** no workspace **Ativos e Conformidade**, que contém todos os usuários compatíveis com esse perfil. O painel **Detalhes do Ativo** exibe os usuários compatíveis com o perfil. Clique duas vezes em um usuário na lista para exibir informações adicionais.  

        > [!IMPORTANT]  
        >  Um perfil não será avaliado se ele não for aplicável em um dispositivo cliente; entretanto, ele será devolvido como compatível.  

    -   **Erro:** exibe uma lista de todos os erros da implantação do perfil selecionado com base no número de ativos afetados. Você pode clicar duas vezes em uma regra para criar um nó temporário sob o nó **Usuários** do workspace **Ativos e Conformidade**, que contém todos os usuários que geraram erros com esse perfil. Quando você seleciona um usuário, o painel **Detalhes do Ativo** exibe os usuários afetados pelo problema selecionado. Clique duas vezes em um usuário na lista para exibir informações adicionais sobre o problema.  

    -   **Não Compatível:** exibe uma lista de todas as regras não compatíveis no perfil com base no número de ativos afetados. Você pode clicar duas vezes em uma regra para criar um nó temporário no nó **Usuários** do workspace **Ativos e Conformidade**, que contém todos os usuários que não são compatíveis com esse perfil. Quando você seleciona um usuário, o painel **Detalhes do Ativo** exibe os usuários afetados pelo problema selecionado. Clique duas vezes em um usuário na lista para exibir mais informações sobre o problema.  

    -   **Desconhecido:** exibe uma lista de todos os usuários que não relataram a conformidade para a implantação do perfil selecionado, junto com o status atual do cliente dos dispositivos.  

5.  Na página **Status da Implantação**, você pode examinar informações detalhadas sobre a conformidade do perfil implantado. Um nó temporário é criado no nó **Implantações** , que ajuda você a localizar essas informações novamente com rapidez.  

##  <a name="BKMK_Reports"></a> Como exibir resultados de conformidade por meio de relatórios  
 As configurações de conformidade, como os perfis no System Center Configuration Manager, também incluem vários relatórios internos que permitem monitorar as informações sobre perfis. Esses relatórios têm a categoria de relatório de **Gerenciamento de Conformidade e Configurações**.  

> [!IMPORTANT]  
>  Você deverá usar um caractere curinga (%) ao usar os parâmetros **Filtro de dispositivo** e **Filtro de usuário** nos relatórios de configurações de conformidade.  

 Para obter mais informações sobre como configurar relatórios no System Center Configuration Manager, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  
