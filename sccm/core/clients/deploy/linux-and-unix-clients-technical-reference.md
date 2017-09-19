---
title: "Serviços e comandos de componentes de cliente UNIX/Linux | Microsoft Docs"
description: "Saiba mais sobre os serviços e comandos de componentes em clientes Linux e UNIX no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
caps.latest.revision: "6"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: f11795b05f1b422e97fd32e7457c44b708fa93e4
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2017
---
# <a name="linux-and-unix-clients-component-services-and-commands-for-system-center-configuration-manager"></a>Serviços e comandos de componentes de cliente Linux e UNIX para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


 A tabela a seguir identifica os serviços do componente do cliente do Configuration Manager para Linux e UNIX.  

|Nome do arquivo|Mais informações|  
|---------------|----------------------|  
|ccmexec.bin|Esse serviço é equivalente ao serviço ccmexc em um cliente baseado em Windows. Ele é responsável por todas as comunicações com as funções de sistema de sites do Configuration Manager e também se comunica com o serviço de omiserver.bin para coletar o inventário de hardware do computador local.<br /><br /> Para obter uma lista de argumentos de linha de comando com suporte, execute **ccmexec -h**|  
|omiserver.bin|Esse serviço é o servidor CIM. O servidor CIM fornece uma estrutura para módulos de software conectáveis chamados provedores. Os provedores interagem com os recursos de computador Linux e UNIX e coletam os dados de inventário de hardware. Por exemplo, o **provedor processo** para um Linux computador coleta os dados associados com os processos de sistema operacional Linux.|  

 Os seguintes comandos da lista de tabelas que você pode usar para iniciar, parar ou reiniciar os serviços do cliente (CcmExec e omiserver) em cada versão do Linux ou UNIX. Ao iniciar ou parar o serviço ccmexec, o serviço de omiserver também é iniciado ou interrompido.  

|Sistema operacional|Comandos|  
|----------------------|--------------|  
|Agente Universal<br /><br /> RHEL 4 e SLES 9|Início: **/etc/init d/ccmexecd start**<br /><br /> Parar: **/etc/init d/ccmexecd stop**<br /><br /> Reiniciar: **/etc/init d/ccmexecd restart**|  
|Solaris 9|Início: **/etc/init d/ccmexecd start**<br /><br /> Parar: **/etc/init d/ccmexecd stop**<br /><br /> Reiniciar: **/etc/init d/ccmexecd restart**|  
|Solaris 10|Início:<br /><br /> **svcadm enable -s svc:/application/management/omiserver**<br /><br /> **svcadm enable -s svc:/application/management/ccmexecd**<br /><br /> Parar:<br /><br /> **svcadm disable -s svc:/application/management/ccmexecd**<br /><br /> **svcadm disable -s svc:/application/management/omiserver**|  
|Solaris 11|Início:<br /><br /> **svcadm enable -s svc:/application/management/omiserver**<br /><br /> **svcadm enable -s svc:/application/management/ccmexecd**<br /><br /> Parar:<br /><br /> **svcadm disable -s svc:/application/management/ccmexecd**<br /><br /> **svcadm disable -s svc:/application/management/omiserver**|  
|AIX|Início:<br /><br /> **startsrc -s omiserver**<br /><br /> **startsrc -s ccmexec**<br /><br /> Parar:<br /><br /> **stopsrc -s ccmexec**<br /><br /> **stopsrc -s omiserver**|  
|HP-UX|Início: **/sbin/init.d/ccmexecd start**<br /><br /> Parar: **/sbin/init.d/ccmexecd stop**<br /><br /> Reiniciar: **/sbin/init.d/ccmexecd restart**|  
