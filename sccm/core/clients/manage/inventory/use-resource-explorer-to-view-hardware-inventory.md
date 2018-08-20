---
title: Como usar o Gerenciador de Recursos
titleSuffix: Configuration Manager
description: Use o Gerenciador de Recursos para exibir o inventário de hardware no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e4f39d06072222c14627481f21139f06ee6656c4
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384965"
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-configuration-manager"></a>Como usar o Gerenciador de Recursos para exibir o inventário de hardware no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o Gerenciador de Recursos no Configuration Manager para exibir informações sobre o inventário de hardware. O site coleta essas informações dos clientes em sua hierarquia.  

> [!Tip]  
>  O Gerenciador de Recursos não exibe todos os dados até que um ciclo de inventário de hardware seja executado no cliente ao qual você está se conectando.  



## <a name="overview"></a>Visão geral

O Gerenciador de Recursos contém as seguintes seções relacionadas ao inventário de hardware:  

- **Hardware**: mostra o inventário de hardware mais recente coletado do dispositivo cliente especificado.  

    - O nó **Status da Estação de Trabalho** mostra a hora e a data do último inventário de hardware do dispositivo.  

- **Histórico de Hardware**: um histórico de itens inventariados que foram alterados desde o último ciclo de inventário de hardware.  

    - Expandir um item para ver um nó **Atual** e um ou mais nós com a data do histórico. Compare as informações do nó atual com um dos nós históricos para descobrir os itens que foram alterados.  

> [!NOTE]  
> Por padrão, o Configuration Manager exclui os dados de inventário de hardware que ficam inativos por 90 dias. Ajuste esse número de dias na tarefa de manutenção de site **Excluir Histórico de Inventário Antigo**. Para obter mais informações, confira [Tarefas de manutenção](/sccm/core/servers/manage/maintenance-tasks).  



## <a name="bkmk_open"></a> Como abrir o Gerenciador de Recursos   

1.  No console do Configuration Manager, acesse o espaço de trabalho **Ativos e Conformidade** e selecione o nó **Dispositivos**. Você também pode selecionar qualquer coleção no nó **Coleções de Dispositivos**.  

2.  Selecione um dispositivo. Na faixa de opções, na guia **Início** e no grupo **Dispositivos**, clique em **Iniciar** e, em seguida, selecione **Gerenciador de Recursos**.   

> [!Tip]  
> No Gerenciador de Recursos, clique com o botão direito do mouse em um item no painel de resultados correto para obter ações adicionais. Clique em **Propriedades** para exibir esse item em um formato diferente.  



## <a name="bkmk_bigint"></a> Uso de valores inteiros grandes
<!--1357880--> No Configuration Manager 1802 e nas versões anteriores, o inventário de hardware tem um limite de inteiros maiores que 4.294.967.296 (2^32). Esse limite pode ser alcançado para atributos como tamanhos de disco rígido em bytes. O ponto de gerenciamento não processa os valores inteiros acima desse limite, portanto, nenhum valor é armazenado no banco de dados. 

Começando na versão 1806, o limite foi aumentado para 18.446.744.073.709.551.616 (2^64). 

Para uma propriedade com um valor que não é alterado, como o tamanho total do disco, talvez não seja possível observar o valor logo após atualizar o site. A maioria dos inventários de hardware é um relatório delta. O cliente envia somente os valores que são alterados. Para contornar esse comportamento, adicione outra propriedade à mesma classe. Essa ação faz com que o cliente atualize todas as propriedades na classe que foi alterada. 



## <a name="see-also"></a>Consulte também

Para obter informações de como exibir o inventário de hardware de clientes que executam Linux e UNIX, veja [Como monitorar clientes para servidores Linux e UNIX](/sccm/core/clients/manage/monitor-clients-for-linux-and-unix-servers).  

O Gerenciador de Recursos também mostra o inventário de software. Para obter mais informações, confira [Como usar o Gerenciador de Recursos para exibir o inventário de software](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory).
