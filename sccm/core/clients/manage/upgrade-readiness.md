---
title: Upgrade Readiness
titleSuffix: Configuration Manager
description: Integre o Upgrade Readiness ao Configuration Manager para acessar os dispositivos de destino e os dados de compatibilidade do Windows 10 para atualização ou correção.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/04/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: ad084aabca6f3b0fd920fd2c9b406efff36005a1
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43995338"
---
# <a name="integrate-upgrade-readiness-with-configuration-manager"></a>Integrar o Upgrade Readiness ao Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Upgrade Readiness faz parte do [Windows Analytics](https://docs.microsoft.com/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness). Ele permite avaliar e analisar a preparação dos dispositivos no ambiente para fazer a atualização para o Windows 10. Integre o Upgrade Readiness ao Configuration Manager para acessar dados de compatibilidade de atualização de cliente no console do Configuration Manager. Em seguida, use esses dados para criar coleções e dispositivos de destino para upgrade ou correção.



## <a name="configure-clients"></a>Configurar clientes

O Upgrade Readiness depende dos dados do Windows Analytics. Para que o Upgrade Readiness receba dados suficientes, configure os seguintes pré-requisitos:

- Configurar todos os clientes com uma *chave de ID comercial*  

- Configurar os clientes do Windows 10 para o Windows Analytics para relatar pelo menos dados de nível básico  

- Para clientes que executam o Windows 7 ou 8.1:  

    - Instalar as atualizações conforme descrito em [Introdução ao Upgrade Readiness](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started#deploy-the-compatibility-update-and-related-kbs)  

    - Habilitar configurações de cliente de análise do Windows  

Configure usando o cliente do Configuration Manager. Para saber mais, confira [Usar o Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics).

> [!NOTE]  
> Implantar as atualizações corretas de pré-requisitos e definir as configurações do cliente deve ser suficiente na maioria dos ambientes. Se o Upgrade Readiness apresentar problemas de não recebimento dos dados de dispositivos do ambiente, alguns desses problemas poderão ser resolvidos com o [script de implantação do Upgrade Readiness](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-deployment-script). 



## <a name="connect-configuration-manager-to-upgrade-readiness"></a>Conectar o Configuration Manager ao Upgrade Readiness

Use o [Assistente de serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para simplificar o processo de configuração dos serviços do Azure usados com o Configuration Manager. Para conectar o Configuration Manager ao Upgrade Readiness, crie um registro de aplicativo do Azure Active Directory (Azure AD) do tipo *aplicativo Web/API* no [Portal do Azure](https://portal.azure.com). Para saber mais sobre como criar um registro de aplicativo, veja [Registrar seu aplicativo com seu locatário do Azure AD](/azure/active-directory/active-directory-app-registration). 

No Portal do Azure, dê permissões de *Colaborador* ao aplicativo Web registrado recentemente. Defina essas permissões no grupo de recursos que contém o espaço de trabalho do Log Analytics que hospeda os dados do Upgrade Readiness. O Assistente de serviços do Azure usa esse registro de aplicativo para permitir que o Configuration Manager se comunique de forma segura com o Azure AD e conecte a sua infraestrutura aos dados do Upgrade Readiness.

> [!IMPORTANT]  
> Conceda as permissões de *colaborador* ao próprio aplicativo não a uma identidade de usuário do Azure AD. É o aplicativo registrado que acessa os dados em nome da sua infraestrutura do Configuration Manager. Para conceder as permissões, pesquise o nome do registro do aplicativo na área **Adicionar usuários** ao atribuir a permissão. 
> 
> Esse processo é semelhante a quando você fornece ao Configuration Manager as permissões para o Log Analytics. Essas etapas devem ser concluídas antes que o registro do aplicativo seja importado para o Configuration Manager com o *Assistente de serviços do Azure*.
> 
> Para saber mais, veja [Conectar o Configuration Manager ao Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm).


### <a name="use-the-azure-wizard-to-create-the-connection"></a>Usar o Assistente do Azure para criar a conexão

Siga as instruções em [Configurar serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para criar uma conexão com o Upgrade Readiness por meio da importação do registro do aplicativo Web criado acima. 

Se a importação do aplicativo Web for bem-sucedida e as permissões corretas forem designadas no Portal do Azure, a página *Configuração*, preencherá previamente os seguintes valores:   
-  Assinaturas do Azure  
-  Grupo de recursos do Azure  
-  Espaço de trabalho do Windows Analytics  

Mais de um grupo de recursos ou espaço de trabalho está disponível nas seguintes circunstâncias: 
- Se o aplicativo Web do Azure AD registrado tiver permissões de *Colaborador* em mais de um grupo de recursos   
- Se o grupo de recursos selecionado tiver mais de um espaço de trabalho do Log Analytics  



## <a name="view-and-use-upgrade-readiness-information-in-configuration-manager"></a>Exibir e usar as informações do Upgrade Readiness no Configuration Manager

Depois de integrar o Upgrade Readiness ao Configuration Manager, você poderá exibir a análise de Upgrade Readiness de seus clientes.

1. No console do Configuration Manager, vá até o espaço de trabalho **Monitoramento** e selecione o nó **Upgrade Readiness**.  

2. Examine os dados. Por exemplo:  
    - O estado de preparação de atualização  
    - O percentual de dispositivos do Windows que estão reportando dados  

3. Filtre o painel para exibir dados para dispositivos em coleções específicas.  

4. Exiba os dispositivos em um estado de preparação específico e, em seguida, crie uma coleção dinâmica para esses dispositivos. Em seguida, use essa coleção para atualizar esses dispositivos ou tome atitudes para corrigir dispositivos que estejam em um estado bloqueado.  

> [!Note]  
> O site sincroniza dados com o Upgrade Readiness uma vez por semana.<!--SCCMDocs issue 732--> Para acionar a sincronização manualmente:
> 1. No console do Configuration Manager, acesse o espaço de trabalho **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Serviços do Azure**.  
> 2. Selecione a conexão do Upgrade Readiness na lista.  
> 3. Na faixa de opções, selecione a opção para sincronizar.  



## <a name="next-steps"></a>Próximas etapas

- [Atualizar o Windows para a versão mais recente](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version)  
- [Criar uma sequência de tarefas para atualizar um sistema operacional](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)  
- [Criar implantações em fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)  
