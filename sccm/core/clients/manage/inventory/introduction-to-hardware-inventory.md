---
title: "Inventário de hardware – Configuration Manager | Microsoft Docs"
description: "Obtenha uma introdução ao inventário de hardware no System Center Configuration Manager."
ms.custom: na
ms.date: 12/05/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3743c80b0c2b5142f3a537ba3855ffd14794d42b
ms.openlocfilehash: a543b945c4727540faa064c068b175ef63cb5a4b


---
# <a name="introduction-to-hardware-inventory-in-system-center-configuration-manager"></a>Introdução ao inventário de hardware no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o inventário de hardware no System Center Configuration Manager para coletar informações sobre a configuração de hardware de dispositivos cliente em sua organização. Para coletar o inventário de hardware, a configuração **Habilitar inventário de hardware em clientes** deve ser habilitada nas configurações do cliente.  

 Depois que o inventário de hardware é habilitado e um ciclo de inventário de hardware é executado pelo cliente, o cliente envia as informações para um ponto de gerenciamento no site do cliente. Em seguida, o ponto de gerenciamento encaminha as informações de inventário para o servidor do site do Configuration Manager, que armazena as informações de inventário no banco de dados do site. O inventário de hardware é executado em clientes de acordo com o agendamento que você especificar nas configurações do cliente.  

 Você pode usar vários métodos para exibir os dados de inventário de hardware coletados pelo Configuration Manager. Eles incluem o seguinte:  

-   [Crie consultas que retornam dispositivos que se baseiam em uma configuração de hardware específica](../../../../core/servers/manage/queries-technical-reference.md).  

-   [Crie coleções baseadas em consulta que se baseiam em uma configuração de hardware específica](../../../../core/clients/manage/collections/introduction-to-collections.md). Associações de coleção baseada em consulta são atualizadas automaticamente em um agendamento. Você pode usar coleções para várias tarefas, que incluem a implantação de software. .  

-   [Execute os relatórios que exibem detalhes específicos sobre as configurações de hardware em sua organização](../../../../core/servers/manage/reporting.md).   

-   [Usar o Gerenciador de Recursos](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) para exibir informações detalhadas sobre o inventário de hardware que foi coletado dos dispositivos cliente.   

 Quando o inventário de hardware é executado em um dispositivo cliente, os primeiros dados de inventário retornados pelo cliente são sempre um inventário completo. As informações de inventário posteriores contêm apenas informações de inventário delta. O servidor do site processa informações de inventário delta na ordem em que elas são recebidas. Se as informações delta de um cliente estiverem ausentes, o servidor do site rejeitará as informações delta adicionais e instruirá o cliente a executar um ciclo de inventário completo.  

 O Configuration Manager dá suporte limitado a computadores de inicialização dupla. O Configuration Manager pode descobrir computadores com inicialização dupla, mas só retorna informações de inventário do sistema operacional que estava ativo no momento da execução do ciclo do inventário.  

> [!NOTE]  
>  Para obter informações sobre como usar o inventário de hardware com clientes que executam Linux e UNIX, consulte [Inventário de hardware para Linux e UNIX no System Center Configuration Manager](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

## <a name="extending-configuration-manager-hardware-inventory"></a>Estendendo o inventário de hardware do Configuration Manager  
 Além do inventário de hardware interno no Configuration Manager, você também pode usar um dos seguintes métodos para estender o inventário de hardware para coletar mais informações:  

- Você pode habilitar, desabilitar, adicionar e remover classes de inventário para o inventário de hardware do console do Configuration Manager.|  
- Use arquivos NOIDMIF para coletar informações sobre dispositivos de cliente que não podem ser inventariados pelo Configuration Manager. Por exemplo, você talvez queira coletar informações de número de ativo dispositivo que existe apenas como um rótulo no dispositivo. Inventário NOIDMIF é associado automaticamente a que foram coletado do dispositivo cliente.  
- Use arquivos IDMIF para coletar informações sobre os ativos que não estão associados a um cliente do Configuration Manager, por exemplo, projetores, fotocopiadoras e impressoras de rede.  

 Para obter mais informações sobre como usar métodos para estender o inventário de hardware do Configuration Manager, consulte [Como configurar o inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  



<!--HONumber=Jan17_HO4-->


