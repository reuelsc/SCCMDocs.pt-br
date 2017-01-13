---
title: Configurar sites | Microsoft Docs
description: "Consulte esta lista de verificação para verificar se você considerou as configurações mais comuns que afetam os sites e as hierarquias."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
caps.latest.revision: 15
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: a6936dac2159118b192a930eecb4595b0f4d4a59


---
# <a name="configure-sites-and-hierarchies-for-system-center-configuration-manager"></a>Configurar sites e hierarquias para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Depois de instalar o primeiro site do System Center Configuration Manager ou adicionar sites adicionais à sua hierarquia, use a seguinte lista de verificação para garantir que você considere as configurações mais comuns que afetam os sites e hierarquias.  

## <a name="checklist-of-common-configurations-for-new-and-additional-sites"></a>Lista de verificação das configurações comuns para sites novos e adicionais  
 Na maioria das situações, não será necessário configurar as seguintes opções em nenhuma ordem específica:  

-   Algumas opções baseiam-se umas nas outras, como descoberta de florestas do Active Directory, limites e grupos de limites.  

-   Várias configurações têm valores padrão que podem ser usados sem alterações de configuração, pelo menos temporariamente.  

-   Outras configurações, como grupos de limites e grupos de pontos de distribuição, necessitam de configuração para que se possa usá-las.  

|Ação|Detalhes|  
|------------|-------------|  
|Configurar administração baseada em funções|Administração baseada em função é como você segrega as atribuições administrativas para controlar quais usuários administrativos podem exibir e gerenciar diferentes objetos e dados em seu ambiente do Configuration Manager.<br /><br /> Configurações para administração baseada em função são compartilhadas com todos os sites em uma hierarquia.   <br />Consulte [Configurar administração baseada em função para o System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|  
|Publicar dados do site no AD DS (Serviços de Domínio do Active Directory)|Quando você publica dados do site para o AD DS, torna mais fácil para os clientes localizar serviços e fazer uso eficiente de recursos do site.<br /><br /> Você deve primeiro [Estender o esquema do Active Directory para o System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md), depois cada site deve ser configurado para [Publicar dados do site para o System Center Configuration Manager](../../../../core/servers/deploy/configure/publish-site-data.md) individualmente.|  
|Configurar um ponto de conexão de serviço|No site de nível superior da sua hierarquia, você deve planejar instalar e configurar o ponto da conexão de serviço. Para obter informações, consulte [Sobre o ponto de conexão de serviço no System Center Configuration Manager](../../../../core/servers/deploy/configure/about-the-service-connection-point.md).|  
|Adicionar funções do sistema de sites|Instale uma ou mais funções adicionais do sistema de sites para sites individuais.  Consulte [Add site system roles for System Center Configuration Manager](../../../../core/servers/deploy/configure/add-site-system-roles.md)|  
|Configurar limites de site e grupos de limites|Especifique limites que definem os locais de rede na intranet que podem conter dispositivos que você deseja gerenciar e configure grupos de limites para que os clientes nesses locais de rede possam encontrar recursos de serviços do Configuration Manager. Consulte [Definir limites de site e grupos de limites para o System Center Configuration Manager](../../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)|  
|Configurar grupos de ponto de distribuição|Configurar grupos lógicos de pontos de distribuição para facilitar o gerenciamento de implantações. Consulte [Gerenciar grupos de pontos de distribuição](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) em [Instalar e configurar pontos de distribuição para o System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).|  
|Executar descoberta|Execute a descoberta para localizar os recursos em sua rede, incluindo infraestrutura de rede, dispositivos e usuários.<br /><br /> Consulte [Executar descoberta para o System Center Configuration Manager](../../../../core/servers/deploy/configure/run-discovery.md)|  
|Adicionar capacidade e redundância para aqueles que gerenciam sua infraestrutura|Você pode instalar mais Provedores de SMS e consoles do Configuration Manager para expandir a capacidade para os administradores gerenciarem sua infraestrutura:<br /><br /> **Instale provedores de SMS adicionais** para fornecer redundância para pontos de contato para administrar o site e a hierarquia. Consulte [Manage the SMS Provider](../../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) em [Modify your System Center Configuration Manager infrastructure](../../../../core/servers/manage/modify-your-infrastructure.md)<br /><br /> **Instalar consoles adicionais do Configuration Manager** para fornecer acesso a usuários administrativos adicionais ao mesmo tempo. Consulte [Instalar consoles do Configuration Manager](../../../../core/servers/deploy/install/install-consoles.md)|  
|Configurar componentes do site|Você pode configurar os componentes do site em cada site para modificar o comportamento de funções do sistema de site e o relatório de status do site. Consulte [Site components for System Center Configuration Manager](../../../../core/servers/deploy/configure/site-components.md)|  
|Criar coleções personalizadas|Usando informações detectadas sobre dispositivos e usuários, crie coleções personalizadas de objetos para simplificar as tarefas de gerenciamento no futuro. Consulte [Como criar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md)|  
|Definir configurações para gerenciar implantações de alto risco|Defina configurações em um site que avisará os usuários administrativos quando eles criarem uma implantação de sequência de tarefas de alto risco.  Consulte [Settings to manage high-risk deployments for System Center Configuration Manager](../../../../protect/understand/settings-to-manage-high-risk-deployments.md)|  
|Configurar réplicas de banco de dados para os pontos de gerenciamento|Configure uma réplica de banco de dados para reduzir a carga de CPU colocada no servidor de banco de dados do site por pontos de gerenciamento conforme eles atendem solicitações de clientes. Consulte [Database replicas for management points for System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md)|  
|Configurar um Grupo de Disponibilidade AlwaysOn do SQL Server para hospedar o banco de dados do site|A partir da versão 1602, você pode configurar grupos de disponibilidade como uma solução de alta disponibilidade e recuperação de desastres para hospedar o banco de dados do site em sites primários e no site de administração central. Consulte [AlwaysOn do SQL Server para um banco de dados do site altamente disponível do System Center Configuration Manager](../../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)|  
|Modificar replicação entre sites|Consulte [Transferência de dados entre sites no System Center Configuration Manager](../../../../core/servers/manage/data-transfers-between-sites.md) para saber mais sobre os seguintes temas:<br /><br /> Configurar [File-based replication](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_fileroute) entre sites secundários<br /><br /> Configurar [Database replication links](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_Dblinks)<br /><br /> Configurar [Distributed views](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_distviews)|  



<!--HONumber=Dec16_HO3-->


