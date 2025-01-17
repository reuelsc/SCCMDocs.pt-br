---
title: 'Inventário de hardware '
titleSuffix: Configuration Manager
description: Obtenha uma introdução ao inventário de hardware no System Center Configuration Manager.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ebe3414ad8db1a76761954579a7668179ee1fd74
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67550714"
---
# <a name="introduction-to-hardware-inventory-in-system-center-configuration-manager"></a>Introdução ao inventário de hardware no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o inventário de hardware no System Center Configuration Manager para coletar informações sobre a configuração de hardware de dispositivos cliente em sua organização. Para coletar o inventário de hardware, é preciso selecionar a configuração **Habilitar inventário de hardware em clientes** nas configurações do cliente.  

 Depois que o inventário de hardware estiver habilitado e o cliente executar um ciclo de inventário de hardware, o cliente enviará as informações a um ponto de gerenciamento no site do cliente. Em seguida, o ponto de gerenciamento encaminha as informações de inventário para o servidor do site do Configuration Manager, que armazena as informações de inventário no banco de dados do site. O inventário de hardware é executado em clientes de acordo com o agendamento que você especificar nas configurações do cliente.  
## <a name="view-hardware-inventory"></a>Exibir inventário de hardware 

 Você pode usar vários métodos para exibir os dados de inventário de hardware coletados pelo Configuration Manager, incluindo estes métodos:  

- [Crie consultas que retornam dispositivos que se baseiam em uma configuração de hardware específica](../../../../core/servers/manage/introduction-to-queries.md).  

- [Crie coleções baseadas em consulta que se baseiam em uma configuração de hardware específica](../../../../core/clients/manage/collections/introduction-to-collections.md). Associações de coleção baseada em consulta são atualizadas automaticamente em um agendamento. Você pode usar coleções para várias tarefas, incluindo implantação de software.

- [Execute os relatórios que exibem detalhes específicos sobre as configurações de hardware em sua organização](../../../../core/servers/manage/reporting.md).

- [Use o Gerenciador de Recursos](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) para exibir informações detalhadas sobre o inventário de hardware coletado dos dispositivos cliente.

Quando o inventário de hardware é executado em um dispositivo cliente, os primeiros dados de inventário retornados pelo cliente são sempre um inventário completo. Os dados de inventário posteriores contêm apenas informações de inventário delta. O servidor do site processa as informações de inventário delta na ordem em que são recebidas. Se as informações delta para um cliente estiverem ausentes, o servidor do site rejeitará informações delta adicionais e instruirá o cliente a executar um ciclo de inventário completo.  

 O Configuration Manager dá suporte limitado a computadores de inicialização dupla. O Configuration Manager pode descobrir computadores com inicialização dupla, mas retorna informações de inventário apenas do sistema operacional ativo no momento da execução do ciclo do inventário.  

> [!NOTE]  
>  Para obter informações sobre como usar o inventário de hardware com clientes que executam Linux e UNIX, consulte [Inventário de hardware para Linux e UNIX no System Center Configuration Manager](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

## <a name="extending-configuration-manager-hardware-inventory"></a>Estendendo o inventário de hardware do Configuration Manager  
 Além do inventário de hardware interno no Configuration Manager, também é possível pode usar um destes métodos para estender o inventário de hardware para coletar mais informações:  

- Habilitar, desabilitar, adicionar e remover classes de inventário para o inventário de hardware do console do Configuration Manager.  
- Usar arquivos NOIDMIF para coletar informações sobre dispositivos cliente que não podem ser inventariados pelo Configuration Manager. Por exemplo, você talvez queira coletar informações de número de ativo dispositivo que existe apenas como um rótulo no dispositivo. Inventário NOIDMIF é associado automaticamente a que foram coletado do dispositivo cliente.  
- Use arquivos IDMIF para coletar informações sobre os ativos que não estão associados a um cliente do Configuration Manager, por exemplo, projetores, fotocopiadoras e impressoras de rede.


## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre como usar métodos para estender o inventário de hardware do Configuration Manager, consulte [Como configurar o inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
