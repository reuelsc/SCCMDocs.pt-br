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
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 34e1f57798a9745303dd6d03a8b4362c01c5efbb


---
# <a name="how-to-monitor-certificate-profiles-in-system-center-configuration-manager"></a>Como monitorar perfis de certificado no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Após implantar perfis de certificado do System Center Configuration Manager para os usuários na sua hierarquia, você poderá usar os seguintes procedimentos para monitorar o status de conformidade do perfil:  

-   [Como exibir resultados de conformidade no console do Configuration Manager](#BKMK_console)  

-   [Como exibir resultados de conformidade por meio de relatórios](#BKMK_Reports)  

##  <a name="a-namebkmkconsolea-how-to-view-compliance-results-in-the-configuration-manager-console"></a><a name="BKMK_console"></a> Como exibir resultados de conformidade no console do Configuration Manager  
 Use este procedimento para exibir detalhes sobre a conformidade dos perfis de certificado implantados no console do System Center Configuration Manager.  

> [!NOTE]  
>  Para monitorar a conformidade de certificado SCEP, não use o console do Configuration Manager; em vez disso, use os relatórios conforme descrito em [How to View Compliance Results by Using Reports](#BKMK_Reports). Especificamente, use os relatórios do certificado localizados no nó de relatório **Acesso a Recursos da Empresa**:  
>   
>  -   Histórico de emissão de certificado  
> -   Lista de ativos com certificados perto do vencimento  
> -   Lista de ativos por status de emissão de certificado  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Para exibir resultados de conformidade no console do Configuration Manager  

1.  No console do System Center Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , clique em **Implantações**.  

3.  Na lista **Implantações** , selecione a implantação de perfil de certificado para a qual deseja examinar as informações de conformidade.  

4.  Você pode examinar as informações de resumo sobre a conformidade do perfil de certificado na página principal. Para exibir informações mais detalhadas, selecione o perfil de certificado e, na guia **Início** , no grupo **Implantação** , clique em **Exibir Status** para abrir a página **Status da Implantação** .  

     A página **Status da Implantação** contém as seguintes guias:  

    -   **Compatível**: exibe a conformidade do perfil de certificado com base no número de ativos afetados. Você pode clicar duas vezes em uma regra para criar um nó temporário no nó **Usuários** do espaço de trabalho **Ativos e Conformidade** . Esse nó contém todos os usuários que são compatíveis com o perfil de certificado. O painel **Detalhes do Ativo** também exibe os usuários que são compatíveis com esse perfil. Clique duas vezes em um usuário na lista para exibir informações adicionais.  

        > [!IMPORTANT]  
        >  O perfil de certificado não será avaliado se não for aplicável a um dispositivo cliente. No entanto, ele é retornado como compatível.  

    -   **Erro**: exibe uma lista de todos os erros da implantação do perfil de certificado selecionado com base no número de ativos afetados. Você pode clicar duas vezes em uma regra para criar um nó temporário no nó **Usuários** do espaço de trabalho **Ativos e Conformidade** . Esse nó contém todos os usuários que geraram erros com esse perfil. Quando você seleciona um usuário, o painel **Detalhes do Ativo** exibe os usuários afetados pelo problema selecionado. Clique duas vezes em um usuário na lista para exibir informações adicionais sobre o problema.  

    -   **Não Compatível**: exibe uma lista de todas as regras não compatíveis no perfil de certificado com base no número de ativos afetados. Você pode clicar duas vezes em uma regra para criar um nó temporário no nó **Usuários** do espaço de trabalho **Ativos e Conformidade** . Esse nó contém todos os usuários que não são compatíveis com esse perfil. Quando você seleciona um usuário, o painel **Detalhes do Ativo** exibe os usuários afetados pelo problema selecionado. Clique duas vezes em um usuário na lista para exibir mais informações sobre o problema.  

    -   **Desconhecido**: exibe uma lista de todos os usuários que não relataram a conformidade para a implantação do perfil de certificado selecionado, junto com o status atual do cliente dos dispositivos.  

5.  Na página **Status da Implantação** , você pode examinar informações detalhadas sobre a conformidade do perfil de certificado implantado. Um nó temporário é criado no nó **Implantações** , que ajuda você a localizar essas informações novamente com rapidez.  

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

##  <a name="a-namebkmkreportsa-how-to-view-compliance-results-by-using-reports"></a><a name="BKMK_Reports"></a> Como exibir resultados de conformidade por meio de relatórios

 As configurações de conformidade do System Center Configuration Manager incluem relatórios internos que podem ser usados para monitorar informações sobre perfis de certificado. Esses relatórios têm a categoria de relatório de **Gerenciamento de Conformidade e Configurações**.  

> [!IMPORTANT]  
>  Você deve usar um caractere curinga (%) ao utilizar os parâmetros **Filtro de dispositivo** e **Filtro de usuário** nos relatórios de configurações de conformidade.  

 Para obter mais informações sobre como configurar relatórios no System Center Configuration Manager, consulte [Relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  



<!--HONumber=Dec16_HO3-->


