---
title: Sincronizar dados com o Log Analytics
titleSuffix: Configuration Manager
description: Sincronizar dados do Configuration Manager com o Azure Log Analytics.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9b3ba4c5179069e5443beaf1b7f733c797cfd680
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156518"
---
#  <a name="sync-data-from-configuration-manager-to-azure-log-analytics"></a>Sincronizar dados do Configuration Manager com o Azure Log Analytics

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

<!--1258052--> Use o **Assistente dos Serviços do Azure** para configurar uma conexão do Configuration Manager com o serviço de nuvem do Azure Log Analytics. Essa conexão sincroniza os dados de coleção de dispositivo com o Log Analytics. 

> [!Note]  
> O Configuration Manager não habilita esse recurso opcional por padrão. É necessário habilitar esse recurso antes de usá-lo. Para obter mais informações, veja [Habilitar recursos opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

> [!TIP]
> A partir do Configuration Manager 1802, o Conector do Log Analytics deixa de ser um recurso de pré-lançamento. Para saber mais, confira [Usar recursos de pré-lançamento de atualizações](/sccm/core/servers/manage/pre-release-features).



## <a name="prerequisites-for-the-log-analytics-connector"></a>Pré-requisitos para o Conector do Log Analytics

> [!Note]  
> Este artigo refere-se ao *Conector do Log Analytics*, que antes era chamado de *Conector do OMS*. Não há diferença funcional. Para saber mais, veja [Gerenciamento do Azure - Monitoramento](https://docs.microsoft.com/azure/monitoring/#operations-management-suite).  

- Antes de instalar o conector do Log Analytics no Configuration Manager, forneça as permissões ao Configuration Manager. Conceda *acesso de colaborador* ao *grupo de recursos* do Azure que contém o espaço de trabalho do Log Analytics. Para saber mais, veja [Fornecer ao Configuration Manager permissões para o Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics).  

- Instale o conector do Log Analytics no computador que hospeda o [ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) no modo online.  

- Instale um Microsoft Monitoring Agent para Log Analytics no ponto de conexão de serviço com o conector. Configure esse agente e o conector para que usem o mesmo espaço de trabalho do Log Analytics. Para saber mais sobre como instalar esse agente, veja [Baixar e instalar o agente](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent).  

- Depois de instalar o conector e o agente, configure o Log Analytics para usar dados do Configuration Manager. Para saber mais, veja [Importar as coleções do Configuration Manager](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections).  



## <a name="configure-the-connection-to-log-analytics"></a>Configurar a conexão ao Log Analytics

Use o **Assistente dos Serviços do Azure** para configurar uma conexão do Configuration Manager com o serviço de nuvem do Azure Log Analytics. Para obter mais informações e detalhes desse processo, confira [Configurar serviços do Azure](https://docs.microsoft.com/sccm/core/servers/deploy/configure/azure-services-wizard). Selecione a opção do **Conector do OMS** no assistente. 

> [!Note]  
> Este artigo refere-se ao *Conector do Log Analytics*, que antes era chamado de *Conector do OMS*. Não há diferença funcional. Para saber mais, veja [Gerenciamento do Azure - Monitoramento](https://docs.microsoft.com/azure/monitoring/#operations-management-suite).  

Se você tiver concluído todos os outros procedimentos com êxito, as informações na tela **Configuração de Conexão** aparecerão automaticamente depois que você importar o aplicativo Web. As informações para as configurações de conexão devem aparecer para sua **Assinatura do Azure**, **Grupo de recursos do Azure** e **Workspace do Operations Management Suite**.

O assistente conecta-se ao serviço do Log Analytics usando as informações que você inseriu. Selecione as coleções de dispositivos que você deseja sincronizar com o serviço de nuvem e, em seguida, clique em **Adicionar**.


## <a name="verify-the-connector-properties"></a>Verifique as propriedades do conector

Depois de vincular o Configuration Manager ao Log Analytics, exiba as propriedades da conexão para adicionar ou remover coleções. 

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Serviços do Azure**.  

2. Selecione sua conexão do Log Analytics. Na faixa de opções, selecione **Propriedades**.  

A página de propriedades tem as duas guias a seguir:  

#### <a name="azure-active-directory"></a>Azure Active Directory
Essa guia mostra os seguintes atributos: 
- **Locatário**  
- **ID do Cliente**  
- **Expiração da chave secreta do cliente**  

Também verifique a data de expiração da chave secreta do cliente.

#### <a name="connection-properties"></a>Propriedades da Conexão
Essa guia mostra os seguintes atributos: 
- **Assinatura do Azure**  
- **Grupo de recursos do Azure**  
- **Espaço de trabalho do Log Analytics**  

Ela também mostra a lista de **Coleções de dispositivos**. Use os botões **Adicionar** e **Remover** para modificar as coleções que devem ser sincronizadas.
