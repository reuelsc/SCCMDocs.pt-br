---
title: "Descobrir recursos de dispositivo e de usuário | Microsoft Docs"
description: "Leia uma visão geral do processo de descoberta e dos registros dos dados de descoberta."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
caps.latest.revision: 20
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 7b6674f331c82cc7899b8661cf38b9d3022cf21b
ms.openlocfilehash: 647826e9d340d3ef97abab0dba51041a3727dedc
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017


---
# <a name="run-discovery-for-system-center-configuration-manager"></a>Executar descoberta para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use um ou mais métodos de descoberta no System Center Configuration Manager para encontrar recursos de dispositivo e usuário que você pode gerenciar. Também é possível usar a descoberta para identificar a infraestrutura de rede em seu ambiente. Há vários métodos de descoberta diferentes que você pode usar para descobrir coisas diferentes, cada um dos quais com configurações e limitações próprias.  

## <a name="overview-of-discovery"></a>Visão geral da descoberta  
 Descoberta é o processo pelo qual o Configuration Manager aprende sobre as coisas que você pode gerenciar. Veja a seguir os métodos de descoberta disponíveis:  

-   Descoberta de Florestas do Active Directory  

-   Descoberta de grupos do Active Directory  

-   Descoberta de sistemas do Active Directory  

-   Descoberta de Usuário do Active Directory  

-   Descoberta de pulsação  

-   Descoberta de Rede  

-   Descoberta de Servidor  

> [!TIP]  
>  Você pode aprender sobre os métodos de descoberta individuais em [Sobre métodos de descoberta para o System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  
>   
>  Para obter ajuda na seleção de quais métodos usar e em quais sites na hierarquia, veja [Selecione os métodos de descoberta para usar com o System Center Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md).  

 Para usar a maioria dos métodos de descoberta, você deve habilitar o método em um site e configurá-lo para pesquisar locais de rede ou do Active Directory específicos. Quando for executado, ele consultará o local especificado em busca de informações sobre dispositivos ou usuários que o Configuration Manager pode gerenciar. Quando um método de descoberta encontra informações com êxito, ele coloca essas informações em um arquivo chamado DDR (registro dos dados de descoberta). Esse arquivo é processado por um site de administração central ou primário. O processamento de um DDR cria um novo registro no banco de dados do site para recursos recém-descobertos ou atualiza os registros existentes com as novas informações.  

 Alguns métodos de descoberta podem gerar um grande volume de tráfego de rede, e os DDRs resultantes podem ocasionar um uso significativo de recursos da CPU durante o processamento. Portanto, planeje usar somente os métodos de descoberta que você precisa para atingir suas metas. Você pode começar usando somente um ou dois métodos de descoberta e, posteriormente, habilitar métodos adicionais de forma controlada para estender o nível de descoberta em seu ambiente.  

 Depois que as informações de descoberta são adicionadas ao banco de dados do site, elas são replicadas em cada site na hierarquia, independentemente do site em que foram descobertas ou processadas. Portanto, embora você possa definir diferentes agendamentos e configurações para métodos de descoberta em sites diferentes, um método de descoberta específico pode ser executado em apenas um único site. Isso reduz o uso de largura de banda de rede por meio de ações de descoberta duplicadas e reduz o processamento de dados de descoberta redundantes em vários sites.  

 Você pode usar dados de descoberta para criar coleções e consultas personalizadas que agrupam logicamente os recursos para tarefas de gerenciamento. Por exemplo:  

-   Enviar por push as instalações de cliente ou atualizar.  

-   Implantar conteúdo para usuários ou dispositivos.  

-   Implantar configurações de cliente e as configurações relacionadas.

##  <a name="BKMK_DDRs"></a> Sobre os registros dos dados de descoberta  
 Os DDRs são arquivos criados por um método de descoberta. Eles contêm informações sobre um recurso que você pode gerenciar no Configuration Manager, como computadores, usuários e, em alguns casos, infraestrutura de rede. Eles são processados em sites primários ou em sites de administração central. Depois que as informações de recursos do DDR são inseridas no banco de dados, o DDR é excluído e as informações são replicadas como dados globais em todos os sites da hierarquia.  

 O site em que um DDR é processado depende das informações que ele contém:  

-   Os DDRs de recursos recém-descobertos que não estão no banco de dados são processados no site de nível superior da hierarquia. O site de nível superior cria um novo registro de recurso no banco de dados e atribui um identificador exclusivo a ele. Os DDRs são transferidos por replicação baseada em arquivo até chegarem ao site de nível superior.  

-   Os DDRs para objetos descobertos anteriormente são processados em sites primários. Os sites primários filho não transferem os DDRs para o site de administração central quando o DDR contém informações sobre um recurso que já está no banco de dados.  

-   Os sites secundários não processam DDRs e sempre os transferem por replicação baseada em arquivo para o respectivo site pai primário.  

Os arquivos DDR são identificados pela extensão .ddr e têm um tamanho típico de aproximadamente 1 KB.  

## <a name="get-started-with-discovery"></a>Introdução à descoberta:  
 Antes de usar o console do Configuration Manager para configurar a descoberta, você deve compreender as diferenças entre os métodos, o que eles podem fazer e para alguns, suas limitações.  

Os seguintes tópicos podem construir uma base que ajudarão você a usar métodos de descoberta com êxito:  

-   [Sobre métodos de descoberta para o System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Selecione os métodos de descoberta que serão usados com o System Center Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

Em seguida, quando compreender os métodos que deseja usar, encontre orientações para configurar cada método em [Configurar métodos de descoberta para o System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

