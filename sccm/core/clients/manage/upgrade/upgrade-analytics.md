---
title: Upgrade Readiness
titleSuffix: Configuration Manager
description: "Integre o Upgrade Readiness com o Configuration Manager. Acessar dados de compatibilidade de atualização no seu console de administração. Dispositivos de destino para atualização ou correção."
keywords: 
author: mattbriggs
ms.author: mabrigg
manager: angerobe
ms.date: 7/31/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: df2950551e527788aeb01d57cdbf01ad19817ccd
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="integrate-upgrade-readiness-with-system-center-configuration-manager"></a>Integrar o Upgrade Readiness com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Upgrade Readiness (anteriormente conhecido como Upgrade Analytics) faz parte do [Windows Analytics](https://www.microsoft.com/WindowsForBusiness/windows-analytics), permitindo avaliar e analisar a preparação dos dispositivos no ambiente para fazer a atualização para o Windows 10. Você pode configurar a versão específica. O Upgrade Readiness pode ser integrado ao Configuration Manager para acessar dados de compatibilidade de upgrade do cliente no console de administração do Configuration Manager. É possível direcionar dispositivos para upgrade ou correção usando coleções dinâmicas criadas com base nesses dados.

A solução Upgrade Readiness é executada no [OMS (Operations Management Suite)](/azure/operations-management-suite/operations-management-suite-overview). Leia mais sobre o Upgrade Readiness em [Manage Windows upgrades with Upgrade Readiness](/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness) (Gerenciar upgrades do Windows com o Upgrade Readiness).

## <a name="configure-clients"></a>Configurar clientes

O Upgrade Readiness, como todas as soluções do Windows Analytics, baseia-se em dados de telemetria do Windows. Para que o Upgrade Readiness receba dados de telemetria suficientes, os seguintes pré-requisitos devem ser atendidos:

- Todos os clientes devem ser configurados com uma **chave da ID comercial**. 
- Os clientes do Windows 10 devem ter a telemetria configurada para relatar, pelo menos, o nível básico de telemetria.
-  Os clientes que executam versões anteriores no Windows precisam ter KBs específicos instalados, conforme é descrito em [Get started with Upgrade Readiness](/windows/deployment/upgrade/upgrade-readiness-get-started#deploy-the-compatibility-update-and-related-kbs) (Introdução ao o Upgrade Readiness). Eles também precisam ter a telemetria habilitada em **Configurações do Cliente**.

A chave da ID comercial e a telemetria do Windows podem ser configuradas em **Configurações do Cliente**. Para obter mais informações, consulte [Usar o Windows Analytics com o Configuration Manager](../monitor-windows-analytics.md).

>[!NOTE]
>Se o Upgrade Readiness apresentar problemas de não receber dados de telemetria dos dispositivos em seu ambiente conforme o esperado, alguns desses problemas poderão ser resolvidos usando o [Script de implantação do Upgrade Readiness](/windows/deployment/upgrade/upgrade-readiness-deployment-script). No entanto, na maioria dos ambientes, deve ser suficiente implantar os KBs corretos, configurar a chave da ID comercial e a telemetria em **Configurações do Cliente**.

## <a name="connect-configuration-manager-to-upgrade-readiness"></a>Conectar o Configuration Manager ao Upgrade Readiness

A partir da versão 1706 do Branch Atual, o [Assistente para serviços do Azure](../../../servers/deploy/configure/azure-services-wizard.md) é usado para simplificar o processo de configuração dos serviços do Azure que são usados com o Configuration Manager. Para conectar o Configuration Manager ao Upgrade Readiness, um registro de aplicativo do Azure AD do tipo *aplicativo Web/API* deve ser criado no [Portal do Azure](https://portal.azure.com). Para saber mais sobre como criar um registro de aplicativo, consulte [Registrar seu aplicativo com seu locatário do Azure Active Directory](/azure/active-directory/active-directory-app-registration). No **Portal do Azure**, você também precisará fornecer suas permissões de *colaborador* do aplicativo Web recém-registrado para o grupo de recursos que contém o espaço de trabalho do OMS que hospeda os dados do Upgrade Readiness. O **Assistente de serviços do Azure** usará esse registro de aplicativo para permitir que o Configuration Manager se comunique de forma segura com o Azure AD e conecte a sua infraestrutura aos dados do Upgrade Readiness.

>[!IMPORTANT]
>As permissões de *colaborador* devem ser concedidas ao próprio aplicativo em vez de uma identidade de usuário do Azure AD. O motivo é que é o aplicativo registrado e não um usuário do Azure AD que acessa os dados em nome da sua infraestrutura do Configuration Manager. Para fazer isso, você precisará pesquisar o nome do registro do aplicativo na folha **Adicionar usuários** ao atribuir a permissão. Esse é o mesmo processo que deve ser seguido ao [fornecer ao Configuration Manager as permissões para o OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) para conexões com o [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm). Essas etapas devem ser concluídas antes que o registro do aplicativo seja importado para o Configuration Manager com o *Assistente de serviços do Azure*.

### <a name="use-the-azure-wizard-to-create-the-connection"></a>Usar o Assistente do Azure para criar a conexão

Siga as instruções em [Configurar serviços do Azure para uso com o Configuration Manager](../../../servers/deploy/configure/azure-services-wizard.md) para criar uma conexão com o Upgrade Readiness importando o registro do aplicativo Web criado acima. 

Na página *Configuração*, os seguintes valores serão pré-populados se a importação do aplicativo Web for bem-sucedida e as permissões corretas forem designadas no **Portal do Azure**. 
-  Assinaturas do Azure
-  Grupo de recursos do Azure
-  Espaço de trabalho do Windows Analytics

Haverá mais de um grupo de recursos ou espaço de trabalho disponível somente se o aplicativo Web do Azure AD registrado tiver permissões de *Colaborador* em mais de um grupo de recursos ou se o grupo de recursos selecionado contiver mais de um espaço de trabalho do OMS.
 
## <a name="view-and-use-upgrade-readiness-information-in-configuration-manager"></a>Exibir e usar as informações do Upgrade Readiness no Configuration Manager

Depois de integrar o Upgrade Readiness ao Configuration Manager, você poderá exibir a análise de Upgrade Readiness de seus clientes.

1. No console do Configuration Manager, escolha **Monitoramento** > **Visão Geral** > **Upgrade Readiness**.
2. Examine os dados, que inclui o estado de preparação para atualização e a porcentagem de dispositivos do Windows que estão comunicando telemetria.
3. Você pode filtrar o painel para exibir dados para dispositivos em coleções específicas.
4. Você pode exibir os dispositivos em um estado de preparação específico e criar uma coleção dinâmica com eles para que seja possível atualizar os dispositivos que estiverem prontos ou executar ações para corrigir aqueles que não puderem ser atualizados.

## <a name="using-the-upgrade-readiness-connector-version-1702-and-earlier"></a>Usando o Upgrade Readiness (versão 1702 ou anterior)

No Configuration Manager versão 1702 ou anteriores, é necessário um conjunto de etapas e requisitos diferente para criar uma conexão com o Upgrade Readiness.

### <a name="prerequisites"></a>Pré-requisitos

- Para adicionar a conexão, seu ambiente do Configuration Manager deve configurar primeiro um [ponto de conexão de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point) em um [modo online](https://azure.microsoft.com/documentation/articles/resource-group-create-service-principal-portal/). Quando você adiciona a conexão ao seu ambiente, ele também instalará o Microsoft Monitoring Agent no computador que executa essa função de sistema de sites.
- Registre o Configuration Manager como uma ferramenta de gerenciamento "Aplicativo Web e/ou API Web" e obtenha a [ID do cliente desse registro](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
- Crie uma chave de cliente para a ferramenta de gerenciamento registrada no Azure Active Directory.
- No Portal do Azure, forneça o aplicativo Web registrado com permissão para acessar o OMS, conforme descrito em [Fornecer ao Configuration Manager as permissões para OMS](https://azure.microsoft.com/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

    > [!IMPORTANT]
    > Ao configurar a permissão para acessar o OMS, certifique-se de escolher a função **Colaborador** e atribua a ela permissões para o grupo de recursos do aplicativo registrado.

### <a name="create-the-connection"></a>Criar a conexão

1.  No console do Configuration Manager, escolha **Administração** > **Serviços de Nuvem** > **Atualizar Conector de Preparação** > **Criar Conexão ao Upgrade Analytics** para iniciar o **Assistente para adicionar conexão de análise do Upgrade Analytics**.
3.  Na tela **Azure Active Directory**, forneça o **Locatário**, a **ID do cliente** e a **Chave de segredo do cliente** e, em seguida, selecione **Avançar**.
4.  Na tela **Upgrade Readiness**, forneça as suas configurações de conexão preenchendo sua **Assinatura do Azure**, **Grupo de recursos do Azure** e **Espaço de trabalho do Operations Management Suite**.
5.  Verifique suas configurações de conexão na tela **Resumo** e, em seguida, selecione **Avançar**.

    > [!NOTE]
    > É necessário conectar o Upgrade Readiness ao site de nível superior na sua hierarquia. Se você conectar o Upgrade Readiness a um site primário autônomo e, em seguida, adicionar um site de administração central ao seu ambiente, será necessário excluir e recriar a conexão do OMS dentro da nova hierarquia.
