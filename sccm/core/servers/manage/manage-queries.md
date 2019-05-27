---
title: Gerenciar consultas
titleSuffix: Configuration Manager
description: Saiba como gerenciar suas consultas. Inclui uma tabela de referência detalhada.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5394cd86e1f137bd7cf76549b117cb53f242f8f1
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65497297"
---
# <a name="how-to-manage-queries-in-system-center-configuration-manager"></a>Como gerenciar consultas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use as informações neste tópico para ajudar a gerenciar consultas no System Center Configuration Manager.  

 Para obter informações sobre como criar consultas, veja [Como criar consultas no System Center Configuration Manager](../../../core/servers/manage/create-queries.md).  

## <a name="how-to-manage-queries"></a>Como gerenciar consultas  
 No workspace **Monitoramento**, selecione **Consultas**, selecione a consulta a ser gerenciada e uma tarefa de gerenciamento.  

 Use a tabela a seguir para obter mais informações sobre as tarefas de gerenciamento que podem requerer informações adicionais antes de você selecioná-las.  

|Tarefa de gerenciamento|Detalhes|Mais informações|  
|---------------------|-------------|----------------------|  
|**Executar**|Executa a consulta selecionada e exibe os resultados no console do Configuration Manager.|Nenhuma informação adicional.|  
|**Instalar o cliente**|Abre o **Assistente para Instalar Cliente**, que permite instalar o cliente do Configuration Manager nos computadores retornados pela consulta selecionada.<br /><br /> Essa opção não está disponível para consultas que retornam dispositivos móveis, usuários ou grupos de usuários.|Para obter mais informações sobre como instalar clientes do Configuration Manager usando push de cliente, consulte [Implantar clientes em computadores Windows](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).|  
|**Exportar**|Abre o **Assistente para Exportar Objetos** , que permite exportar esta consulta para um formato MOF (Managed Object Format) que pode ser importado mais tarde em outro site.|Nenhuma informação adicional.|  
|**Moverr**|Abre a caixa de diálogo **Mover Itens Selecionados** , em que você pode mover a consulta selecionada para uma pasta que você criou anteriormente no nó **Consultas** .|Nenhuma informação adicional.|  

## <a name="next-steps"></a>Próximas etapas 
 [Como criar consultas no System Center Configuration Manager](../../../core/servers/manage/create-queries.md)
