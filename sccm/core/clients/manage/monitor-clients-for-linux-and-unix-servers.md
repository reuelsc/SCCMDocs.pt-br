---
title: 'Monitorar clientes Linux/UNIX '
titleSuffix: Configuration Manager
description: Monitore clientes em servidores Linux e UNIX no System Center Configuration Manager.
ms.custom: na
ms.date: 08/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
caps.latest.revision: "6"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 777842307b280a4f269d68bcb993f3cec6f2e3e3
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Como monitorar clientes para servidores Linux e UNIX no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode exibir informações de servidores Linux e UNIX no console do System Center Configuration Manager usando os mesmos métodos que você pode usar para exibir informações de clientes baseados em Windows.  

 As informações que você pode exibir incluem:  

-   Detalhes sobre o status de clientes nos painéis do console do Configuration Manager  

-   Detalhes sobre os clientes nos relatórios padrão do Configuration Manager  

-   Detalhes sobre inventário no Gerenciador de Recursos  

 As seções a seguir descrevem como obter esses detalhes do gerenciador de recursos, bem como relatórios.  

##  <a name="BKMK_UseResourceExpforLnU"></a> Usar o gerenciador de recursos para exibir o inventário de servidores Linux e UNIX  

 Após um cliente do Configuration Manager enviar o inventário de hardware para o site do Configuration Manager, você pode usar o Gerenciador de Recursos para exibir essas informações. O cliente do Configuration Manager para Linux e UNIX não adiciona novas classes ou exibições de inventário ao Gerenciador de Recursos. Os dados de inventário Linux e UNIX mapeiam para classes WMI existentes. Você pode exibir os detalhes sobre inventário de seus servidores Linux e UNIX nas classificações de baseadas em Windows usando o Gerenciador de Recursos.  

 Por exemplo, você pode coletar a lista de todos os programas nativos instalados encontrados nos servidores Linux e UNIX. Entre os exemplos de programas nativos instalados estão o **.rpms** no Linux ou o **.pkgs** no Solaris. Após o inventário ser enviado por um cliente Linux ou UNIX, você pode exibir a lista de todos os programas nativos Linux ou UNIX instalados no Gerenciador de Recursos no console do Configuration Manager.  

 Para obter informações sobre como usar o Gerenciador de Recursos, consulte [Como usar o Gerenciador de Recursos para exibir o inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

##  <a name="BKMK_UseReportsforLnU"></a> Como usar relatórios para exibir informações para servidores Linux e UNIX  
 Os relatórios do Configuration Manager incluem informações de servidores Linux e UNIX, juntamente com informações de computadores baseados no Windows. Nenhuma configuração adicional é necessária para integrar os dados do Linux e UNIX aos relatórios.  

 Por exemplo, se você executar o relatório chamado Contagem de Versões do Sistema Operacional, ele exibirá a lista de diferentes sistemas operacionais e o número de clientes que executando cada sistema operacional. O relatório se baseia nas informações do inventário de hardware que foram enviadas por diferentes clientes do Configuration Manager que executam diferentes sistemas operacionais.  

 Também é possível criar relatórios personalizados específicos para os dados dos servidores Linux e UNIX. A propriedade **Legenda** da classe de inventário de hardware **Sistema Operacional** é um atributo útil que você pode usar para identificar sistemas operacionais específicos na consulta do relatório.  

 Para obter informações sobre os relatórios no Configuration Manager, consulte [Relatórios no System Center Configuration Manager](../../../core/servers/manage/reporting.md).  
