---
title: "Conceitos básicos do gerenciamento de cliente"
titleSuffix: Configuration Manager
description: "Saiba mais sobre as tarefas que você executa para gerenciar clientes do System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: a88be6397e1e2b1f86a517d2c068e1c0cb8a40bc
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="fundamentals-of-client-management-tasks-for-system-center-configuration-manager"></a>Noções básicas das tarefas de gerenciamento de cliente para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Após instalar clientes do System Center Configuration Manager, há várias tarefas que você executa para gerenciá-los.  Algumas das tarefas são executadas no console do Configuration Manager. Outras tarefas são executadas de um aplicativo cliente do Configuration Manager. O aplicativo cliente do Configuration Manager é instalado com o software cliente do Configuration Manager.

## <a name="configuration-manager-console-tasks"></a>Tarefas do console do Configuration Manager
 No console do Configuration Manager, é possível realizar diversas tarefas de gerenciamento de clientes:  

-   Implantar aplicativos, atualizações de software, scripts de manutenção e sistemas operacionais. Configurar a instalação para uma data e hora específica, disponibilizar o software para os usuários instalarem quando forem solicitados ou configurar os aplicativos a serem desinstalados.  

-   Ajudar na proteção de computadores contra malware e ameaças à segurança e notificar quando problemas forem detectados.  

-   Definir as configurações de cliente que você deseja monitorar e corrigir se estiverem fora de conformidade.  

-   Coletar informações de inventário de hardware e software, que incluam monitoramento e reconciliação das informações de licença da Microsoft.  

-   Solucionar problemas de computadores usando o controle remoto.  

-   Implementar as configurações de gerenciamento de energia para gerenciar e monitorar o consumo de energia de computadores.  

O console do Configuration Manager monitora as tarefas anteriores quase em tempo real. A notificação e as informações de status para cada tarefa estão disponíveis no console do Configuration Manager. Para capturar dados e tendências históricas, use os recursos integrados de relatório do SQL Server Reporting Services. Os clientes enviam detalhes para o site, como o status do cliente.  As informações de status do cliente fornecem dados sobre a integridade do cliente e a atividade do cliente, e são exibidas no console ou por meio dos relatórios internos para o Configuration Manager. Esses dados ajudam a identificar computadores sem resposta e, em alguns casos, os problemas são corrigidos automaticamente.  

 Para obter mais informações sobre tarefas de gerenciamento para clientes, consulte [Como gerenciar clientes no System Center Configuration Manager](../../core/clients/manage/manage-clients.md) e [Como gerenciar clientes para servidores Linux e UNIX no System Center Configuration Manager](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md). Para saber mais sobre como usar relatórios, confira   
            [Introdução à emissão de relatórios no System Center Configuration Manager](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="configuration-manager-client-application"></a>Aplicativo cliente do Configuration Manager  
 Quando você instala o software cliente do Configuration Manager, o aplicativo cliente do Configuration Manager também é instalado. Ao contrário do Centro de Software, o aplicativo cliente do Configuration Manager foi projetado para o suporte técnico e não para os usuários finais. Algumas opções de configuração exigem permissões administrativas locais e a maioria das opções exige conhecimento técnico sobre como o aplicativo cliente do Configuration Manager funciona. Você pode usar esse aplicativo para executar as seguintes tarefas em um cliente:  

-   Exibir propriedades sobre o cliente, como o número de build, o site atribuído, o ponto de gerenciamento com o qual está se comunicando e se o cliente está usando um certificado de PKI (infraestrutura de chave pública) ou um certificado autoassinado.  

-   Confirmar se o cliente baixou com êxito uma política de cliente depois que o cliente foi instalado pela primeira vez. Além disso, confirmar se as configurações de cliente estão habilitadas ou desabilitadas conforme o esperado, de acordo com as configurações de cliente que são definidas no console do Configuration Manager.  

-   Iniciar ações de cliente. Por exemplo, baixar a política de cliente, se houve uma alteração recente da configuração no console do Configuration Manager e você não deseja esperar até a próxima hora agendada.  

-   Atribuir manualmente um cliente a um site do Configuration Manager ou tentar encontrar um site. Em seguida, especificar o sufixo do DNS (Sistema de Nomes de Domínio) para pontos de gerenciamento que publicam no DNS.  

-   Configurar o cache de cliente que armazena arquivos temporariamente. E, em seguida, excluirá os arquivos no cache se você precisar de mais espaço em disco para instalar software.  

-   Definir as configurações de gerenciamento de clientes baseado na Internet.  

-   Exibir as linhas de base de configuração implantadas para o cliente, iniciar a avaliação de conformidade e exibir os relatórios de conformidade.  
