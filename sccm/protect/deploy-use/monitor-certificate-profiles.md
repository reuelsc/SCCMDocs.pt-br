---
title: Monitorar perfis de certificado | Microsoft Docs
description: Saiba como monitorar o status de conformidade de perfis de certificado do System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98feaa06-64b1-4e86-a122-93017c97cd4f
caps.latest.revision: 7
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 8a5dc7361da34f3e6b926acd35c72c0c0767ce70
ms.openlocfilehash: 74a0a4274965891869caf838550cd9465b46fd51
ms.lasthandoff: 12/30/2016


---
# <a name="how-to-monitor-certificate-profiles-in-system-center-configuration-manager"></a>Como monitorar perfis de certificado no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Exibir Resultados de conformidade no Console do Configuration Manager  

Para monitorar a conformidade de certificado SCEP, não use o console, em vez disso, use [relatórios](#view-compliance-results-by-using-reports). 

1.  No console do Configuration Manager, escolha **Monitoramento**>  **Implantações**.  

3.  Selecione a implantação do perfil de certificado de interesse.  

4.  Examine o resumo das informações de conformidade do certificado na página principal. Para informações mais detalhadas, selecione o perfil de certificado e, em seguida, na guia **Início**, no grupo **Implantação**, escolha **Exibir Status** para abrir a página **Status da Implantação**.  

     A página **Status da Implantação** contém as seguintes guias:  

    -   **Compatível**: exibe a conformidade do perfil de certificado com base no número de ativos afetados. Você pode clicar duas vezes em uma regra para criar um nó temporário no nó **Usuários** do espaço de trabalho **Ativos e Conformidade** . Esse nó contém todos os usuários que são compatíveis com o perfil de certificado. O painel **Detalhes do Ativo** também exibe os usuários que são compatíveis com esse perfil. Clique duas vezes em um usuário na lista para obter mais informações.  

        > [!IMPORTANT]  
        >  O perfil de certificado não será avaliado se não for aplicável a um dispositivo cliente. No entanto, ele é retornado como compatível.  

    -   **Erro**: exibe uma lista de todos os erros da implantação do perfil de certificado selecionado com base no número de ativos afetados. Você pode clicar duas vezes em uma regra para criar um nó temporário no nó **Usuários** do espaço de trabalho **Ativos e Conformidade** . Esse nó contém todos os usuários que geraram erros com esse perfil. Quando você seleciona um usuário, o painel **Detalhes do Ativo** exibe os usuários afetados pelo problema selecionado. Clique duas vezes para exibir um usuário da lista para obter mais informações.  

    -   **Não Compatível**: exibe uma lista de todas as regras não compatíveis no perfil de certificado com base no número de ativos afetados. Você pode clicar duas vezes em uma regra para criar um nó temporário no nó **Usuários** do espaço de trabalho **Ativos e Conformidade** . Esse nó contém todos os usuários que não são compatíveis com esse perfil. Quando você seleciona um usuário, o painel **Detalhes do Ativo** exibe os usuários afetados pelo problema selecionado. Clique duas vezes em um usuário na lista para exibir mais informações sobre o problema.  

    -   **Desconhecido**: exibe uma lista de todos os usuários que não relataram a conformidade para a implantação do perfil de certificado selecionado, junto com o status atual do cliente dos dispositivos.  

5.  Na página **Status da Implantação**, examine informações detalhadas sobre a conformidade do perfil de certificado implantado. Um nó temporário é criado no nó **Implantações** , que ajuda você a localizar essas informações novamente com rapidez.  

     O status de registro do certificado é exibido como um número. Use a tabela a seguir para entender o que significa cada número:  

    |Status do registro|Descrição|  
    |-----------------------|-----------------|  
    |0x00000001|O registro foi bem-sucedido, e o certificado foi emitido.|  
    |0x00000002|A solicitação foi enviada, e o registro está pendente, ou a solicitação foi emitida fora da banda.|  
    |0x00000004|O registro deve ser adiado.|  
    |0x00000010|Ocorreu um erro.|  
    |0x00000020|O status do registro é desconhecido.|  
    |0x00000040|As informações de status foram ignoradas. Isso pode ocorrer se uma autoridade de certificação HYPERLINK "http://msdn.microsoft.com/en-us/windows/ms721572" \l "_security_certification_authority_gly" não for válida ou não tiver sido selecionada para o monitoramento.|  
    |0x00000100|O registro foi negado.|  

##  <a name="view-compliance-results-by-using-reports"></a>Exibir resultados de conformidade por meio de relatórios

 As configurações de conformidade do System Center Configuration Manager incluem relatórios internos que podem ser usados para monitorar informações sobre perfis de certificado. Esses relatórios têm a categoria de relatório de **Gerenciamento de Conformidade e Configurações**.  

> [!IMPORTANT]  
>  Você deve usar um caractere curinga (%) ao utilizar os parâmetros **Filtro de dispositivo** e **Filtro de usuário** nos relatórios de configurações de conformidade.  

Para monitorar a conformidade de certificado SCEP, use os relatórios de certificado localizados no nó de relatório **Acesso a Recursos da Empresa**:  

 -   Histórico de emissão de certificado  
 -   Lista de ativos com certificados perto do vencimento  
 -   Lista de ativos por status de emissão de certificado  



 Para obter mais informações sobre como configurar relatórios no System Center Configuration Manager, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  

