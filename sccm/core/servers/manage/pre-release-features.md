---
title: Recursos de pré-lançamento
titleSuffix: Configuration Manager
description: Os recursos de pré-lançamento são recursos que estão na Ramificação atual para testes iniciais em um ambiente de produção.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ab1c8e462e22206177e4907df3c5549ec9ba1692
ms.sourcegitcommit: 60d45a5df135b84146f6cfea2bac7fd4921d0469
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67194206"
---
# <a name="pre-release-features-in-configuration-manager"></a>Recursos pré-lançamento no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os recursos de pré-lançamento são aqueles no branch atual para testes iniciais em um ambiente de produção. Esses recursos são totalmente compatíveis, mas ainda em desenvolvimento ativo. Eles podem receber alterações até que saiam da categoria de pré-lançamento.



## <a name="give-consent"></a>Dar consentimento  

Antes de usar recursos de pré-lançamento, dê consentimento para usá-los. Dar o consentimento é uma ação única por hierarquia que não pode ser desfeita. Até dar o consentimento, você não pode habilitar novos recursos de pré-lançamento incluídos com a atualização. Após ativar um recurso de pré-lançamento, não é possível desativá-lo.

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Configuração do Site** e selecione o nó **Sites**.  

2. Clique em **Configurações da hierarquia**  na faixa de opções.  

3. Na guia **Geral** das Propriedades de Configurações de Hierarquia, habilite a opção para **Consentir com o uso de recursos de pré-lançamento**. Clique em **OK**.  



## <a name="enabling-pre-release-features"></a>Habilitando recursos de pré-lançamento

Quando você instala uma atualização que inclui recursos de pré-lançamento, esses recursos ficam visíveis no Assistente de Atualizações e Manutenção com os recursos regulares incluídos na atualização.

#### <a name="if-you-have-given-consent"></a>Se você tiver consentido
No Assistente de Atualizações e Manutenção, habilite recursos de pré-lançamento. Selecione os recursos de pré-lançamento como faria com qualquer outro recurso.     

Opcionalmente, espere para habilitar recursos de pré-lançamento mais tarde usando o nó **Recursos** em **Atualizações e manutenção** no workspace **Administração**. Selecione um recurso e, em seguida, clique em **Ativar** na faixa de opções. Até você dar consentimento, essa opção não está disponível para uso.

#### <a name="if-you-havent-given-consent"></a>Se você ainda não tiver consentido
No Assistente de Atualizações e Manutenção, recursos pré-lançamento estão visíveis, mas você não pode habilitá-los. Após a atualização ser instalada, esses recursos ficarão visíveis no nó **Recursos**. No entanto, você não poderá habilitá-los até dar consentimento.


> [!Important]  
> Em uma hierarquia multisite, somente é possível habilitar recursos opcionais ou de pré-lançamento no site de administração central. Esse comportamento garante que não haja nenhum conflito na hierarquia. <!--507197-->  
> 
> Se você tiver dado consentimento em um site primário autônomo e depois expandir a hierarquia instalando um novo site de administração central, deverá dar consentimento novamente no site de administração central.  

Ao habilitar um recurso de pré-lançamento, o gerenciador de hierarquia (HMAN) do Configuration Manager deve processar a alteração antes desse recurso ser disponibilizado. O processamento da alteração costuma ser imediato. Dependendo do ciclo de processamento do HMAN, ele poderá levar até 30 minutos para ser concluído. Depois que a alteração for processada, reinicie o console antes de usar o recurso.



## <a name="pre-release-features"></a>Recursos de pré-lançamento

<!--Note/tip for target article

> [!Note]  
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](/sccm/core/servers/manage/pre-release-features).  


> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). Beginning with version 1706, this feature is no longer a pre-release feature.  

-->


| Recurso          | Adicionado como pré-lançamento | Adicionado como recurso completo |  
|------------------|----------------------|-------------------------|
| API do Provedor de SMS <!--1359052--> | Versão 1810 | ![Ainda não](media/red_x.png) |
| [Sistema de sites HTTP aprimorado](/sccm/core/plan-design/hierarchy/enhanced-http) <!--1356889,1358228--> | Versão 1806 | Versão 1810 |
| [Aplicativos cliente para dispositivos cogerenciados](/sccm/comanage/workloads#client-apps) <!--1357892--> | Versão 1806 | ![Ainda não](media/red_x.png) |
| [Extensões SCAP](/sccm/compliance/plan-design/scap/about-scap) <!--3607889--> | Versão 1806 | ![Ainda não](media/red_x.png) |
| [Gerenciador de conversão de pacote](/sccm/apps/pcm/package-conversion-manager) <!--1357861--> | Versão 1806 | Versão 1810 |
| [Suporte para o Cisco AnyConnect 4.0.07x e posterior para iOS](/sccm/mdm/deploy-use/create-vpn-profiles) <!--1357393--> | Versão 1802 | Versão 1802 <br>com atualização 4163547 |
| [Implantações em fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) <!--1356837--> | Versão 1802 | Versão 1806 |
| [Executar a etapa de sequência de tarefas](/sccm/osd/understand/task-sequence-steps#child-task-sequence) <!--1261338--> |  Versão 1710 | Versão 1802 |
| [Windows Defender Exploit Guard](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) <!--1355468--> | Versão 1710 | Versão 1802 |
| [Avaliação do atestado de integridade do dispositivo para políticas de conformidade de acesso condicional](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--1235616--> | Versão 1710 | Versão 1802 |
| [Criar e executar scripts do Windows PowerShell](/sccm/apps/deploy-use/create-deploy-scripts) <!--1236459--> | Versão 1706 | Versão 1802 |
| [Gerenciar atualizações de driver do Microsoft Surface](/sccm/sum/get-started/configure-classifications-and-products) <!--1098490--> | Versão 1706 | Versão 1710 |
| [Gerenciamento do Device Guard](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) <!--1355092 (1319346)--> | Versão 1702 | ![Ainda não](media/red_x.png) |
| [Pré-cache do conteúdo de sequência de tarefas](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) <!--1021244--> | Versão 1702 | Versão 1710 |
| [Verificar se há arquivos executáveis antes de instalar um aplicativo](/sccm/apps/deploy-use/deploy-applications#bkmk_exe-check) <!--1284624--> | Versão 1702 | Versão 1706 |
| [Ponto de serviço de data warehouse](/sccm/core/servers/manage/data-warehouse) <!--1277922--> | Versão 1702 | Versão 1706 |
| [Cache par para distribuição de conteúdo para clientes](/sccm/core/plan-design/hierarchy/client-peer-cache) <!--1101436--> | Versão 1610 | Versão 1710 |
| [Gateway de gerenciamento de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway) <!--1101764--> | Versão 1610 | Versão 1802 |
| [Conector do Azure Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics) <!--1236739--> | Versão 1606 | Versão 1802 |
| [Realização de serviços em uma coleção com reconhecimento de cluster (realização de serviços em um grupo de servidores)](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_ServerGroups) <!--1081776--> | Versão 1602 | ![Ainda não](media/red_x.png) |
| [Acesso condicional para PCs gerenciados pelo Configuration Manager](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--  --> | Versão 1602 | Versão 1702 |

<!--Image used = ![Not yet](media/red_x.png) -->

> [!Tip]  
> Para obter mais informações sobre os recursos que não são de pré-lançamento que você precisa habilitar primeiro, confira [Habilitar recursos opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
> 
> Para obter mais informações sobre os recursos que somente estão disponíveis no branch de Technical Preview, confira [Technical Preview](/sccm/core/get-started/technical-preview).  
