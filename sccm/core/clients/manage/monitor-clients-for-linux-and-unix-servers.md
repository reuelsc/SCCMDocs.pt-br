---
title: Monitorar clientes Linux/UNIX
titleSuffix: Configuration Manager
description: Monitorar clientes em servidores Linux e UNIX no Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 47a85ec7dea72f08a0ec48ebb151566b8563ba9a
ms.sourcegitcommit: d8d142044586a53709b4478ad945f714737c8d6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58523683"
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Como monitorar clientes em servidores Linux e UNIX no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

> [!Important]  
> A partir da versão 1902, o Configuration Manager não dá suporte a clientes Linux ou UNIX. 
> 
> Considere o Gerenciamento do Microsoft Azure para gerenciar servidores Linux. As soluções do Azure têm amplo suporte para Linux que, na maioria dos casos, supera a funcionalidade do Configuration Manager, incluindo o gerenciamento de patches de ponta a ponta para o Linux.

Você pode exibir as informações de servidores Linux e UNIX no console do System Center Configuration Manager usando os mesmos métodos que utiliza para exibir as informações de clientes baseados em Windows.  

 As informações que você pode exibir incluem:  

- Detalhes sobre o status de clientes nos painéis do console do Configuration Manager  

- Detalhes sobre os clientes nos relatórios padrão do Configuration Manager  

- Detalhes sobre inventário no Gerenciador de Recursos  

  As seções a seguir descrevem como obter esses detalhes do gerenciador de recursos, bem como relatórios.  

##  <a name="BKMK_UseResourceExpforLnU"></a> Usar o gerenciador de recursos para exibir o inventário de servidores Linux e UNIX  

 Após um cliente do Configuration Manager enviar o inventário de hardware para o site do Configuration Manager, você pode usar o Gerenciador de Recursos para exibir essas informações. O cliente do Configuration Manager para Linux e UNIX não adiciona novas classes ou exibições de inventário ao Gerenciador de Recursos. Os dados de inventário Linux e UNIX mapeiam para classes WMI existentes. Você pode exibir os detalhes sobre inventário de seus servidores Linux e UNIX nas classificações de baseadas em Windows usando o Gerenciador de Recursos.  

 Por exemplo, você pode coletar a lista de todos os programas nativos instalados encontrados nos servidores Linux e UNIX. Entre os exemplos de programas nativos instalados estão o **.rpms** no Linux ou o **.pkgs** no Solaris. Após o inventário ser enviado por um cliente Linux ou UNIX, você pode exibir a lista de todos os programas nativos Linux ou UNIX instalados no Gerenciador de Recursos no console do Configuration Manager.  

 Para obter informações sobre como usar o Gerenciador de Recursos, consulte [Como usar o Gerenciador de Recursos para exibir o inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

##  <a name="BKMK_UseReportsforLnU"></a> Como usar relatórios para exibir informações para servidores Linux e UNIX  
 Os relatórios do Configuration Manager incluem informações de servidores Linux e UNIX, juntamente com informações de computadores baseados no Windows. Nenhuma configuração adicional é necessária para integrar os dados do Linux e UNIX aos relatórios.  

 Por exemplo, se você executar o relatório chamado Contagem de Versões do Sistema Operacional, ele exibirá a lista de diferentes sistemas operacionais e o número de clientes que executando cada sistema operacional. O relatório se baseia nas informações do inventário de hardware que foram enviadas por diferentes clientes do Configuration Manager que executam diferentes sistemas operacionais.  

 Também é possível criar relatórios personalizados específicos para os dados de servidores Linux e UNIX. A propriedade **Legenda** da classe de inventário de hardware **Sistema Operacional** é um atributo útil que você pode usar para identificar sistemas operacionais específicos na consulta do relatório.  

 Para obter informações sobre os relatórios no Configuration Manager, consulte [Relatórios no System Center Configuration Manager](../../../core/servers/manage/reporting.md).  
