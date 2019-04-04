---
title: Serviços e comandos de componentes de cliente UNIX/Linux
titleSuffix: Configuration Manager
description: Saiba mais sobre os serviços e comandos de componentes em clientes Linux e UNIX no Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0f3538265bdd7de801acf3d8f04c5561364989cf
ms.sourcegitcommit: d8d142044586a53709b4478ad945f714737c8d6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58523972"
---
# <a name="linux-and-unix-clients-component-services-and-commands-for-configuration-manager"></a>Serviços e comandos de componentes de cliente Linux e UNIX no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

> [!Important]  
> A partir da versão 1902, o Configuration Manager não dá suporte a clientes Linux ou UNIX. 
> 
> Considere o Gerenciamento do Microsoft Azure para gerenciar servidores Linux. As soluções do Azure têm amplo suporte para Linux que, na maioria dos casos, supera a funcionalidade do Configuration Manager, incluindo o gerenciamento de patches de ponta a ponta para o Linux.


 A tabela a seguir identifica os serviços do componente do cliente do Configuration Manager para Linux e UNIX.  

|Nome do arquivo|Mais informações|  
|---------------|----------------------|  
|ccmexec.bin|Esse serviço é semelhante ao serviço ccmexc em um cliente baseado em Windows. Ele é responsável por todas as comunicações com as funções do sistema de sites do Configuration Manager e também se comunica com o serviço omiserver.bin para coletar o inventário de hardware do computador local.<br /><br /> Para obter uma lista de argumentos de linha de comando com suporte, execute `ccmexec -h`|  
|omiserver.bin|Esse serviço é o servidor CIM. O servidor CIM fornece uma estrutura para módulos de software conectáveis chamados provedores. Os provedores interagem com os recursos de computador Linux e UNIX e coletam os dados de inventário de hardware. Por exemplo, o **provedor processo** para um Linux computador coleta os dados associados com os processos de sistema operacional Linux.|  

 Os seguintes comandos da lista de tabelas que você pode usar para iniciar, parar ou reiniciar os serviços do cliente (CcmExec e omiserver) em cada versão do Linux ou UNIX. Ao iniciar ou parar o serviço ccmexec, o serviço de omiserver também é iniciado ou interrompido.  

|Sistema operacional|Comandos|  
|----------------------|--------------|  
|Agente Universal<br /><br /> RHEL 4 e SLES 9|Início: `/etc/init d/ccmexecd start`<br /><br /> Parar: `/etc/init d/ccmexecd stop`<br /><br /> Reiniciar: `/etc/init d/ccmexecd restart`|  
|Solaris 9|Início: `/etc/init d/ccmexecd start`<br /><br /> Parar: `/etc/init d/ccmexecd stop`<br /><br /> Reiniciar: `/etc/init d/ccmexecd restart`|  
|Solaris 10|Início:<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> Parar:<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|Solaris 11|Início:<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> Parar:<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|AIX|Início:<br /><br /> `startsrc -s omiserver`<br /><br /> `startsrc -s ccmexec`<br /><br /> Parar:<br /><br /> `stopsrc -s ccmexec`<br /><br /> `stopsrc -s omiserver`|  
|HP-UX|Início: `/sbin/init.d/ccmexecd start`<br /><br /> Parar: `/sbin/init.d/ccmexecd stop`<br /><br /> Reiniciar: `/sbin/init.d/ccmexecd restart`|  
