---
title: Configurar sites e hierarquias
titleSuffix: Configuration Manager
description: Consulte esta lista de verificação para verificar se você considerou as configurações mais comuns que afetam os sites e as hierarquias.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 051958c5fa524c97de0e42784cdab73288a24b82
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383704"
---
# <a name="configure-sites-and-hierarchies-for-configuration-manager"></a>Configurar sites e hierarquias do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Depois de instalar o primeiro site do Configuration Manager ou adicionar mais sites à sua hierarquia, use esta lista de verificação para garantir que você considere as configurações mais comuns que afetam os sites e as hierarquias.  

As observações de configuração a seguir se aplicam à maioria das implantações:  

- Algumas opções baseiam-se umas nas outras, como a Descoberta de Florestas do Active Directory, limites e grupos de limites.  

- Várias configurações têm valores padrão a serem usados sem alterações de configuração, pelo menos para iniciar.  

- Outras configurações, como grupo de limites e grupos de pontos de distribuição exigem que você os configure antes de usar.  

| Ação | Detalhes |  
|------------|-------------|  
| Configurar administração baseada em funções | As atribuições administrativas segregadas para controlar quais usuários administrativos podem exibir e gerenciar diferentes objetos e dados em seu ambiente do Configuration Manager.<br /><br /> Configurações para administração baseada em função são compartilhadas com todos os sites em uma hierarquia.   <br/><br/>Para obter mais informações, confira [Configurar a administração baseada em função](/sccm/core/servers/deploy/configure/configure-role-based-administration). |  
| Publicar dados do site no Active Directory Domain Services | Facilite a localização dos serviços e o uso dos recursos do site com eficiência para os clientes.<br /><br /> Primeiro [estenda o esquema do Active Directory](/sccm/core/plan-design/network/extend-the-active-directory-schema). Em seguida, configure cada site individualmente para [publicar dados do site](/sccm/core/servers/deploy/configure/publish-site-data) |  
| Configurar um ponto de conexão de serviço | Planeje instalar e configurar o ponto de conexão de serviço no site de nível superior da sua hierarquia. Para obter mais informações, consulte [Sobre o ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point). |  
| Adicionar funções do sistema de sites | Instale uma ou mais funções adicionais do sistema de sites para sites individuais. Para obter mais informações, confira [Adicionar funções do sistema de sites](/sccm/core/servers/deploy/configure/add-site-system-roles). |  
| Configurar limites de site e grupos de limites | Especifique limites que definem locais de rede na Intranet que podem conter dispositivos que você deseja gerenciar. Em seguida, configure grupos de limites para que os clientes nesses locais de rede possam encontrar recursos do Configuration Manager. Para obter mais informações, confira [Definir limites e grupos de limites do site](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups). |  
| Configurar grupos de ponto de distribuição | Configure grupos lógicos de pontos de distribuição para facilitar o gerenciamento de implantações. Para obter mais informações, consulte [Gerenciar grupos de pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_manage). |  
| Executar descoberta | Execute a descoberta para localizar os recursos em sua rede, incluindo usuários, dispositivos e infraestrutura de rede.<br /><br /> Para mais informações, consulte [Executar descoberta](/sccm/core/servers/deploy/configure/run-discovery). |  
| Adicionar capacidade e redundância para administradores | Instale mais provedores de SMS e consoles do Configuration Manager para expandir a capacidade que os administradores têm de gerenciar a infraestrutura:<br /><br /> **Instale provedores de SMS adicionais** para fornecer redundância às conexões do console e de API com o site. Para obter mais informações, confira [Gerenciar o provedor de SMS](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ManageSMSprovider).<br /><br /> **Instale consoles adicionais do Configuration Manager** para fornecer acesso a mais usuários administrativos ao mesmo tempo. Para saber mais, veja [Instalar consoles do Configuration Manager](/sccm/core/servers/deploy/install/install-consoles). |  
| Configurar componentes do site | Configure os componentes do site em cada site para modificar o comportamento de funções do sistema de sites e do relatório de status do site. Para obter mais informações, confira [Componentes do site](/sccm/core/servers/deploy/configure/site-components). |  
| Criar coleções personalizadas | Usando informações que o site descobre sobre dispositivos e usuários, crie coleções personalizadas de objetos para simplificar as tarefas de gerenciamento futuras. Para obter mais informações, confira [Como criar coleções](/sccm/core/clients/manage/collections/create-collections). |  
| Definir configurações para gerenciar implantações de alto risco | Defina as configurações em um site para avisar os administradores quando eles criarem uma implantação de alto risco. Para obter mais informações, consulte [Configurações para gerenciar implantações de alto risco](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments). |  
| Configurar réplicas de banco de dados para os pontos de gerenciamento | Configure uma réplica de banco de dados para reduzir a carga do processador colocada no servidor de banco de dados do site pelos pontos de gerenciamento conforme eles atendem a solicitações de serviço de clientes. Para obter mais informações, consulte [Réplicas de banco de dados para pontos de gerenciamento](/sccm/core/servers/deploy/configure/database-replicas-for-management-points). |  
| Configurar um grupo de disponibilidade Always On do SQL Server | Configure grupos de disponibilidade como soluções de alta disponibilidade e de recuperação de desastres para hospedar o banco de dados do site em sites primários e no site de administração central. Para obter mais informações, confira [SQL Server AlwaysOn para um banco de dados do site altamente disponível](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database). |  
| Modificar replicação entre sites | Confira [Transferências de dados entre sites](/sccm/core/servers/manage/data-transfers-between-sites) para saber mais sobre os seguintes assuntos:<br /><br /> Configurar a [replicação baseada em arquivo](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_fileroute) entre sites secundários<br /><br /> Configurar os [Links de replicação de banco de dados](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_Dblinks)<br /><br /> Configurar as [Exibições distribuídas](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_distviews) |  
| Configurar servidores do site no modo passivo | Começando na versão 1806, configure um servidor do site no modo passivo para cada site primário e para o site de administração central. Esse recurso fornece um servidor do site altamente disponível. Para obter mais informações, confira [Alta disponibilidade do servidor do Site](/sccm/core/servers/deploy/configure/site-server-high-availability). |  
