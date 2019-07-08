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
ms.openlocfilehash: 456289520e25fe94da7e94f6a795537f68ba069e
ms.sourcegitcommit: 3a3f40f3d39cbecfb9219a64c0185ea4b2ef9671
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2019
ms.locfileid: "67561972"
---
# <a name="how-to-manage-queries-in-system-center-configuration-manager"></a>Como gerenciar consultas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo pode ajudá-lo a gerenciar consultas no System Center Configuration Manager.  

 Para obter informações sobre como criar consultas, veja [Como criar consultas no System Center Configuration Manager](../../../core/servers/manage/create-queries.md).  

## <a name="manage-queries"></a>Gerenciar consultas
 No workspace **Monitoramento**, selecione **Consultas**, selecione a consulta a ser gerenciada e uma tarefa de gerenciamento.  

 A tabela a seguir fornece informações sobre as tarefas de gerenciamento.  

|Tarefa de gerenciamento|Detalhes| 
|---------------------|-------------|
|**Executar**|Executa a consulta selecionada e exibe os resultados no console do Configuration Manager.|
|**Instalar o cliente**|Abre o **Assistente para Instalar Cliente**, que permite instalar o cliente do Configuration Manager nos computadores retornados pela consulta selecionada.<br /><br /> Essa opção não está disponível para consultas que retornam dispositivos móveis, usuários ou grupos de usuários. <br /><br /> Para obter mais informações sobre como instalar clientes do Configuration Manager usando push de cliente, consulte [Implantar clientes em computadores Windows](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).| 
|**Exportarar**|Abre o **Assistente de Objetos de Exportação**. Este assistente permite exportar a consulta para um arquivo MOF (Managed Object Format) que pode ser importado em outro site.
|**Moverr**|Abre a caixa de diálogo **Mover Itens Selecionados**. Essa caixa de diálogo permite mover a consulta selecionada para uma pasta criada anteriormente no nó **Consultas**.|

## <a name="next-steps"></a>Próximas etapas 
 [Como criar consultas no System Center Configuration Manager](../../../core/servers/manage/create-queries.md)
