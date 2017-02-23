---
title: "Inventário de software | Microsoft Docs"
description: "Veja uma introdução ao inventário de software no System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
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
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 9206b82eca02877c30eebf146d42bcca7290eb42
ms.openlocfilehash: c9956dd4ef94a1b109d761e44e42f512c42eb8d2


---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>Introdução ao inventário de software no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use o inventário de software para coletar informações sobre arquivos em dispositivos cliente. O inventário de software também pode coletar arquivos de dispositivos cliente e armazená-los no servidor do site. O inventário de software é coletado quando você escolhe a configuração **Habilitar inventário de software em clientes** nas configurações do cliente, em que também é possível agendar a operação.  

Depois que o inventário de software é habilitado e os clientes executam um ciclo de inventário de software, o cliente envia as informações para um ponto de gerenciamento no site do cliente. Em seguida, o ponto de gerenciamento encaminha as informações de inventário para o servidor do site do Configuration Manager, que armazena as informações no banco de dados do site.   

 Aqui estão algumas maneiras para exibir os dados de inventário de software:  

-   [Criar consultas](../../../../core/servers/manage/queries-technical-reference.md) que retornam dispositivos com arquivos especificados.   

-   Criar [coleções com base em consulta](../../../../core/clients/manage/collections/introduction-to-collections.md) que incluem dispositivos com arquivos especificados.   

-   [Executar relatórios](../../../../core/servers/manage/reporting.md) que fornecem detalhes sobre arquivos nos dispositivos. 

-   Use o [Gerenciador de Recursos](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) para examinar informações detalhadas sobre os arquivos que foram inventariados e coletados dos dispositivos cliente.   

 Quando o inventário de software é executado em um dispositivo cliente, o primeiro relatório é um inventário completo. Os relatórios posteriores contêm apenas informações de delta de inventário. O servidor do site processa as informações de delta na ordem em que são recebidas. Se as informações de delta de um cliente estiverem ausentes, o servidor do site rejeitará as informações de delta adicionais e instruirá o cliente a executar um inventário completo.  

 O Configuration Manager pode descobrir computadores com inicialização dupla, mas só retorna informações de inventário do sistema operacional que estava ativo no momento do inventário.  

## <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Inventário de software para dispositivos móveis registrados no Microsoft Intune  
 É possível coletar o inventário de aplicativos instalados nos dispositivos móveis. Os aplicativos inventariados dependerão se o dispositivo é de propriedade corporativa ou pessoal. Para dispositivos pessoais, somente aplicativos inventariados são aplicativos que são gerenciados pelo Microsoft Intune.  

> [!NOTE]  
>  O inventário de aplicativos instalados em dispositivos móveis é coletado como parte do processo de [inventário de hardware](../../../../core/clients/manage/inventory/mobile-device-hardware-inventory-hybrid.md).  

 Aqui estão os aplicativos inventariados para dispositivos pessoais ou corporativos.  

|Plataforma|Para dispositivos pessoais|Para dispositivos corporativos|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (sem o cliente do Configuration Manager)|Somente aplicativos gerenciados|Somente aplicativos gerenciados| 
|Windows 8.1 (sem o cliente do Configuration Manager)|Somente aplicativos gerenciados|Somente aplicativos gerenciados|  
|Windows Phone 8|Somente aplicativos gerenciados|Somente aplicativos gerenciados|  
|Windows RT|Somente aplicativos gerenciados|Somente aplicativos gerenciados|  
|iOS|Somente aplicativos gerenciados|Todos os aplicativos instalados no dispositivo|  
|Android|Somente aplicativos gerenciados|Todos os aplicativos instalados no dispositivo|  





<!--HONumber=Dec16_HO5-->


