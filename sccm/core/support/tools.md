---
title: Ferramentas do Configuration Manager
titleSuffix: Configuration Manager
description: Saiba mais sobre as ferramentas para ajudá-lo a gerenciar e solucionar problemas de infraestrutura do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fd23bd523eb64f7d00f71c38c79a180c4e2e569a
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386537"
---
# <a name="configuration-manager-tools"></a>Ferramentas do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As ferramentas do Configuration Manager incluem [ferramentas baseadas em cliente](#client-tools) e [baseadas em servidor](#server-tools). Use essas ferramentas para ajudar a dar suporte e solucionar problemas de infraestrutura do Configuration Manager. 

Do Configuration Manager versão 1806 em diante, essas ferramentas estão incluídas na pasta `CD.Latest\SMSSETUP\Tools` no servidor do site. Nenhuma instalação adicional é necessária.<!--1357145--> Use essas versões das ferramentas com o Configuration Manager versão 1806 e posteriores.

Todos os sistemas operacionais do Windows listados como clientes compatíveis em [Sistemas operacionais compatíveis para clientes e dispositivos](https://docs.microsoft.com/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) podem ser usados com essas ferramentas.

> [!Note]  
> O [Kit de ferramentas do System Center 2012 R2 Configuration Manager](https://www.microsoft.com/en-us/download/details.aspx?id=50012) ainda estará disponível do Centro de Download da Microsoft. Para o Configuration Manager versão 1806 e posteriores, use as versões das ferramentas na pasta CD.Latest no servidor do site. Algumas ferramentas estavam anteriormente no kit de ferramentas, mas não incluídas na versão 1806. Não há mais suporte para essas ferramentas herdadas.


## <a name="client-tools"></a>Ferramentas de cliente

- [CMTrace](/sccm/core/support/cmtrace): exiba, monitore e analise arquivos de log do Configuration Manager  

- [Client Spy](/sccm/core/support/clispy): solucione problemas relacionados a distribuição, inventário e medição de software

- [Deployment Monitoring Tool](/sccm/core/support/deployment-monitoring-tool): solucione problemas de aplicativos, atualizações e implantações da linha de base  

- [Policy Spy](/sccm/core/support/policy-spy): exiba as atribuições de políticas  

- [Power Viewer Tool](/sccm/core/support/power-viewer-tool): exiba o status do recurso de gerenciamento de energia  

- [Ferramenta de Agendamento de Envio](/sccm/core/support/send-schedule-tool): disparar agendas e avaliações de linhas de base de configuração  

> [!Note]  
> A pasta ClientTools também inclui o arquivo Microsoft.Diagnostics.Tracing.EventSource.dll. Várias ferramentas de cliente exigem essa biblioteca. Você não pode usá-lo diretamente.  


## <a name="server-tools"></a>Ferramentas de servidor

- [Gerenciador de Filas de Trabalhos do DP](/sccm/core/support/dp-job-manager): soluciona problemas de trabalhos de distribuição de conteúdo para os pontos de distribuição  

- [Collection Evaluation Viewer](/sccm/core/support/ceviewer): exiba detalhes de avaliação da coleta  

- [Content Library Explorer](/sccm/core/support/content-library-explorer): exiba o conteúdo do repositório de instância única da biblioteca de conteúdo  

- [Content Library Transfer](/sccm/core/support/content-library-transfer): transfere a biblioteca de conteúdo entre unidades  

- [Content Ownership Tool](/sccm/core/support/content-ownership-tool): altera a propriedade de pacotes órfãos. Esses pacotes existem no site sem um servidor de site proprietário.  

- [Role-based Administration and Auditing Tool](/sccm/core/support/rbaviewer): ajuda os administradores a realizar a auditoria de funções de configuração  

- [Ferramenta de Resumo do Medidor de Execução](/sccm/core/support/run-meter-summ): tarefa de resumo de medição de execução e analisar dados de medição

> [!Note]  
> A pasta ServerTools também inclui os seguintes arquivos 
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll. 
>
> Várias ferramentas de servidor exigem essas bibliotecas. Você não pode usá-las diretamente.  



## <a name="other-tools"></a>Outras ferramentas

- [Ferramenta de limpeza da biblioteca de conteúdo](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool): use **ContentLibraryCleanup.exe** em `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` para remover conteúdo órfão de um ponto de distribuição.  

- [Ferramenta de Manutenção de Hierarquia](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe): use **Preinst.exe** na pasta compartilhada `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` no servidor do site para passar comandos para o componente do gerenciador de hierarquia.  

- [Ferramenta de redefinição de atualização](/sccm/core/servers/manage/update-reset-tool): use **CMUpdateReset.exe** em `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` para corrigir problemas quando as atualizações no console tiverem problemas no download ou na replicação.  

- [Ferramenta de Conexão de Serviço](/sccm/core/servers/manage/use-the-service-connection-tool): use **ServiceConnectionTool.exe** em `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` para manter o site atualizado quando o ponto de conexão de serviço estiver offline.  
