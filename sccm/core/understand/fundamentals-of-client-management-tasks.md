---
title: "Conceitos básicos do gerenciamento de clientes | Microsoft Docs"
description: "Conheça as tarefas que você pode executar para gerenciar clientes do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 9648fc831e21f8a5ee6e12cfe7754933ba9f6239


---
# <a name="fundamentals-of-client-management-tasks-for-system-center-configuration-manager"></a>Noções básicas das tarefas de gerenciamento de cliente para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Após a instalação de clientes do System Center Configuration Manager, várias tarefas podem ser executadas para gerenciá-los.  Algumas delas você inicia no console do Configuration Manager, enquanto outras podem ser iniciadas ou exibidas em um cliente no aplicativo para clientes do Configuration Manager no Painel de Controle do Windows.  

## <a name="the-console"></a>O console  
 No console do Configuration Manager, é possível realizar diversas tarefas de gerenciamento de clientes, que incluem o seguinte:  

-   Implantar aplicativos, atualizações de software, scripts de manutenção e sistemas operacionais. É possível configurar essas tarefas a serem instaladas em data e hora determinadas ou torná-las disponíveis para os usuários instalarem quando forem solicitados, além de configurar os aplicativos a serem desinstalados.  

-   Ajudar na proteção de computadores contra malware e ameaças à segurança e notificar quando problemas forem detectados.  

-   Definir as configurações de cliente que você deseja monitorar e corrigir se estiverem fora de conformidade.  

-   Coletar informações de inventário de hardware e software, que incluam monitoramento e reconciliação das informações de licença da Microsoft.  

-   Solucionar problemas de computadores usando o controle remoto.  

-   Implementar as configurações de gerenciamento de energia para gerenciar e monitorar o consumo de energia de computadores.  

Para monitorar essas operações quase em tempo real, use o console do Configuration Manager para ver alertas e informações de status. Para capturar dados e tendências históricas, você pode usar os recursos integrados de relatório do SQL Reporting Services.  Os clientes enviam detalhes para o site, como o status do cliente.  As Informações de status do cliente fornecem dados sobre a integridade do cliente e a atividade do cliente, e podem ser exibidas no console ou por meio de relatórios internos para o Configuration Manager. Esses dados ajudam a identificar computadores sem resposta e, em alguns casos, os problemas podem ser corrigidos automaticamente.  

 Para obter mais informações sobre tarefas de gerenciamento para clientes, consulte [Como gerenciar clientes no System Center Configuration Manager](../../core/clients/manage/manage-clients.md) e [Como gerenciar clientes para servidores Linux e UNIX no System Center Configuration Manager](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md). Para saber mais sobre como usar relatórios, confira   
            [Introdução à emissão de relatórios no System Center Configuration Manager](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="the-windows-control-panel-app"></a>O aplicativo Painel de Controle do Windows  
 Quando você instala o software cliente do Configuration Manager, ele instala o aplicativo cliente do **Configuration Manager** no Painel de Controle. Ao contrário da Central de Software, este aplicativo foi projetado para o suporte técnico e não para os usuários finais. Algumas opções de configuração exigem permissões administrativas locais. A maioria das opções exige conhecimento técnico sobre como o Configuration Manager funciona. Você pode usar esse aplicativo para executar as seguintes tarefas em um cliente:  

-   Visualizar propriedades sobre o cliente, como o número da compilação, o site atribuído, o ponto de gerenciamento com o qual está se comunicando e se o cliente está usando um certificado PKI ou um autoatribuído.  

-   Confirmar se a política do cliente foi baixada com êxito após a instalação do cliente pela primeira vez e se as configurações do cliente estão habilitadas ou desabilitadas conforme o esperado, de acordo com a configuração no console do Configuration Manager.  

-   Iniciar ações de clientes, como o download da política do cliente no caso de uma alteração recente da configuração no console do Configuration Manager, e você não deseja esperar até a próxima hora agendada.  

-   Atribuir manualmente um cliente para um site do Configuration Manager ou tentar encontrar um site e especificar o sufixo DNS para os pontos de gerenciamento que publicam no DNS.  

-   Configurar o cache do cliente que temporariamente armazena arquivos e excluir arquivos no cache se for necessário mais espaço em disco para instalar o software.  

-   Definir as configurações de gerenciamento de clientes baseado na Internet.  

-   Exibir as linhas de base de configuração implantadas para o cliente, iniciar a avaliação de conformidade e exibir os relatórios de conformidade.  



<!--HONumber=Dec16_HO3-->


