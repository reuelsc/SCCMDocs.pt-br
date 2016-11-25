---
title: "Inventário de software | System Center Configuration Manager"
description: "Veja uma introdução ao inventário de software no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 8d664616e222119f7821a70a7c8f9cdbfca38538


---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>Introdução ao inventário de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o inventário de software no System Center Configuration Manager para coletar informações sobre arquivos contidos em dispositivos clientes em sua organização. Além disso, o inventário de software pode coletar arquivos de dispositivos cliente e armazená-los no servidor do site. O inventário de software é coletado quando a configuração **Habilitar inventário de software em clientes** está habilitada nas configurações do cliente.  

 Depois que o inventário de software é habilitado e os clientes executam um ciclo de inventário de software, o cliente envia as informações de inventário para um ponto de gerenciamento no site do cliente. Em seguida, o ponto de gerenciamento encaminha as informações de inventário para o servidor do site do Configuration Manager, que armazena as informações de inventário no banco de dados do site. O inventário de software é executado em clientes de acordo com o agendamento que você especificar nas configurações do cliente.  

 Você pode usar vários métodos para exibir os dados de inventário de software coletados pelo Configuration Manager. Eles incluem o seguinte:  

-   Crie consultas que retornam dispositivos que se baseiam em arquivos especificados que são encontrados nos dispositivos. Para mais informações, consulte [Referência técnica de consultas no System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

-   Crie coleções baseadas em consulta que se baseiam em arquivos especificados que são encontrados nos dispositivos. Associações de coleção baseada em consulta são atualizadas automaticamente em um agendamento. Você pode usar coleções para diversas tarefas como implantação de software. Para mais informações, consulte [Referência técnica de coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/collections-technical-reference.md).  

-   Execute os relatórios que exibem detalhes específicos sobre os arquivos nos dispositivos em sua organização. Para obter mais informações, consulte [Relatórios no System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

-   Use o Gerenciador de Recursos para examinar informações detalhadas sobre os arquivos que foram inventariados e coletados dos dispositivos cliente. Para mais informações, consulte [Como usar o Gerenciador de Recursos para exibir o inventário de software no System Center Configuration Manager](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

 Quando o inventário de software é executado em um dispositivo cliente, o primeiro relatório de inventário retornado é sempre um inventário completo. Os relatórios de inventário posteriores contêm apenas informações de inventário delta. O servidor do site processa informações de inventário delta na ordem em que elas são recebidas. Se as informações de inventário delta de um cliente estiverem ausentes, o servidor do site rejeitará as informações de inventário delta adicionais e instruirá o cliente a executar um ciclo de inventário completo.  

 O Configuration Manager dá suporte limitado a computadores de inicialização dupla. O Configuration Manager pode descobrir computadores com inicialização dupla, mas só retorna informações de inventário do sistema operacional que estava ativo no momento do inventário.  

## <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Inventário de software para dispositivos móveis registrados no Microsoft Intune  
 É possível coletar o inventário em aplicativos instalados nos dispositivos móveis. Os aplicativos inventariados dependerão se o dispositivo é de propriedade corporativa ou pessoal. Para dispositivos pessoais, somente aplicativos inventariados são aplicativos que são gerenciados pelo Microsoft Intune.  

> [!NOTE]  
>  O inventário de aplicativos instalados em dispositivos móveis é coletado como parte do processo de inventário de hardware no Configuration Manager. Para mais informações, consulte [Como configurar o inventário de hardware para dispositivos móveis registrados pelo Microsoft Intune e pelo System Center Configuration Manager](../../../../core/clients/manage/inventory/mobile-device-hardware-inventory-hybrid.md).  

 A tabela a seguir lista quais aplicativos são inventariados para dispositivos pessoais ou corporativos.  

|Plataforma|Para dispositivos pessoais|Para dispositivos corporativos|  
|--------------|---------------------------------|--------------------------------|  
|Windows 8.1 (sem o cliente do Configuration Manager)|Somente aplicativos gerenciados|Somente aplicativos gerenciados|  
|Windows Phone 8|Somente aplicativos gerenciados|Somente aplicativos gerenciados|  
|Windows RT|Somente aplicativos gerenciados|Somente aplicativos gerenciados|  
|iOS|Somente aplicativos gerenciados|Todos os aplicativos instalados no dispositivo|  
|Android|Somente aplicativos gerenciados|Todos os aplicativos instalados no dispositivo|  



<!--HONumber=Nov16_HO1-->


