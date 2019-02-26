---
title: Cogerenciamento para dispositivos Windows 10
titleSuffix: Configuration Manager
description: Saiba como gerenciar dispositivos Windows 10 simultaneamente usando o Configuration Manager e o Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: overview
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.collection: M365-identity-device-management
ms.openlocfilehash: c88bf98e035499c271de8acf9d8fa222e5058447
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754561"
---
# <a name="what-is-co-management"></a>O que é cogerenciamento?

<!-- 1350871 --> O cogerenciamento é uma das principais maneiras para anexar a sua implantação existente do Configuration Manager para a nuvem do Microsoft 365. Ele ajuda você a desbloquear recursos adicionais desenvolvidos por nuvem, como acesso condicional. 

Cogerenciamento permite que você gerencie dispositivos Windows 10 simultaneamente usando o Configuration Manager e o Microsoft Intune. Ele permite que você anexe nuvem seu investimento existente no Configuration Manager, adicionando nova funcionalidade. Usando o cogerenciamento, você tem a flexibilidade para usar a solução de tecnologia que funciona melhor para sua organização. 

Quando um dispositivo Windows 10 tem o cliente do Configuration Manager e está registrado no Intune, você obtém os benefícios de ambos os serviços. Você controlar quais cargas de trabalho, se houver, que você mudar a autoridade do Configuration Manager para o Intune. Configuration Manager continua a gerenciar todas as outras cargas de trabalho, incluindo cargas de trabalho que você não mudar para o Intune e não dá suporte a todos os outros recursos do Configuration Manager que cogerenciamento.

Também é possível criar um piloto de uma carga de trabalho com um conjunto separado de dispositivos. Piloto permite que você teste a funcionalidade do Intune com um subconjunto de dispositivos antes de alternar de um grupo maior. 

![Diagrama de visão geral do cogerenciamento](media/co-management-overview.png)



## <a name="paths-to-co-management"></a>Caminhos para o cogerenciamento

Há dois caminhos principais para usar o cogerenciamento:  

- **Os clientes existentes do Configuration Manager**: Você tem dispositivos Windows 10 que já são clientes do Configuration Manager. Configurar o Azure AD híbrido e registrá-los no Intune.  

- **Novos dispositivos baseados na internet**: Você tem novos dispositivos Windows 10 que ingressem no Azure AD e registrados automaticamente para o Intune. Instalar o cliente do Configuration Manager para atingir um estado de cogerenciamento.  

Para obter mais informações sobre os caminhos, consulte [caminhos para cogerenciamento](/sccm/comanage/quickstart-paths).



## <a name="benefits"></a>Benefícios 

Quando você registra os clientes do Configuration Manager existentes no cogerenciamento, você receberá o seguinte valor de imediato:  

- Acesso condicional com a conformidade do dispositivo  

- Ações de remoto baseado no Intune, por exemplo: reinicialização, controle remoto ou redefinição de fábrica

- Visibilidade centralizada da integridade do dispositivo  

- Vincular usuários, dispositivos e aplicativos com o Azure Active Directory (AD do Azure)  

- Modernos de provisionamento com o Windows Autopilot  

- Ações remotas

Para obter mais informações sobre esse valor imediato de cogerenciamento, consulte a série de guias de início rápido para [Cloud connect com o cogerenciamento](/sccm/comanage/quickstarts).

Cogerenciamento também permite que você coordene com o Intune para várias cargas de trabalho. Para obter mais informações, consulte o [cargas de trabalho](#workloads) seção. 



## <a name="prerequisites"></a>Pré-requisitos

Cogerenciamento tem esses pré-requisitos nas seguintes áreas:

- [Licenciamento](#licensing)  
- [Configuration Manager](#configuration-manager)  
- [Azure Active Directory](#azure-ad) (Azure AD)  
- [Microsoft Intune](#intune)  
- [Windows 10](#windows-10)  
- [Funções e permissões](#permissions-and-roles)  

### <a name="licensing"></a>Licenciamento

- Azure AD Premium 
- Licença do EMS ou do Intune para todos os usuários  

    > [!Note]  
    > Uma Enterprise Mobility + Security (EMS) a assinatura inclui o Azure Active Directory Premium e o Microsoft Intune.

> [!Tip]  
> Certifique-se de que atribuir uma licença do Intune para a conta que você usa para entrar no seu locatário. Caso contrário, Falha ao entrar com a mensagem de erro "O usuário não reconhecido".  


### <a name="configuration-manager"></a>Gerenciador de Configurações

Cogerenciamento exige o Configuration Manager versão 1710 ou posterior.

A partir do Configuration Manager versão 1806, você pode conectar várias instâncias do Configuration Manager para um único locatário do Intune. <!--1357944-->  

Habilitar o cogerenciamento em si não exige que você integre seu site com o Azure AD. Para o [segundo cenário de caminho](#paths-to-co-management), os clientes baseados na internet do Configuration Manager exigem o [gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (CMG). O CMG exige que o site estiver [integrado ao AD do Azure para gerenciamento de nuvem](/sccm/core/servers/deploy/configure/azure-services-wizard). 


### <a name="azure-ad"></a>Azure AD

- Dispositivos Windows 10 devem ser associados ao Azure AD. Eles podem ser de qualquer um dos seguintes tipos:  

    - [Ingressado no Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan), em que o dispositivo ingressa no seu Active Directory local e é registrado com seu Azure Active Directory.  

    - Somente [ingressado no Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan). (Esse tipo é às vezes chamado de "ingressado em domínio de nuvem")<!--SCCMDocs issue 605-->  


### <a name="intune"></a>Intune

- [Configurar o Intune](https://docs.microsoft.com/intune/setup-steps)  

- [Habilitar o registro automático do Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)  

> [!Note]  
> Se você tiver um ambiente de MDM híbrido (Intune integrado ao Configuration Manager), não será possível habilitar o cogerenciamento. No entanto, você pode iniciar a migração de usuários para o Intune autônomo e, em seguida, habilitar seus dispositivos Windows 10 associados para cogerenciamento. Para obter mais informações sobre como migrar para o Intune autônomo, consulte [Iniciar a migração do MDM híbrido para o Intune autônomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).  
> 
> Se você estiver usando [autoridade mista](/sccm/mdm/deploy-use/migrate-mixed-authority), primeiro conclua a migração para o Intune autônomo. Em seguida, defina a autoridade de MDM no Intune antes de configurar o cogerenciamento.<!--SCCMDocs issue #797-->


### <a name="windows-10"></a>Windows 10

Atualize seus dispositivos Windows 10, versão 1709 ou posterior. Para obter mais informações, consulte [adoção do Windows como um serviço](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service).

> [!IMPORTANT]
> Dispositivos móveis Windows 10 não compatíveis com o cogerenciamento.


### <a name="permissions-and-roles"></a>Funções e permissões
<!--SCCMDocs issue #667-->

| Ação | Função necessária |
|----|----|
| Configurar um gateway de gerenciamento de nuvem no Configuration Manager | Azure **Gerenciador de assinatura** |
| Criar aplicativos do Azure AD do Configuration Manager | Azure AD **Administrador Global** |
| Importar aplicativos do Azure no Configuration Manager | Configuration Manager **administrador completo**<br>Não há funções do Azure adicionais necessárias |
| Habilitar o cogerenciamento no Configuration Manager | Um usuário do AD do Azure<br>Configuration Manager **administrador completo** com **todos os** definir o escopo de direitos.<!--SCCMDoc issue 626--> | 

Para obter mais informações sobre as funções do Azure, confira [Entender as diferentes funções](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).

Para obter mais informações sobre funções do Configuration Manager, consulte [fundamentos da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).


## <a name="workloads"></a>Cargas de trabalho 

Você não precise mudar as cargas de trabalho, ou você pode fazê-las individualmente, quando você estiver pronto. Configuration Manager continua a gerenciar todas as outras cargas de trabalho, incluindo cargas de trabalho que você não mudar para o Intune e não dá suporte a todos os outros recursos do Configuration Manager que cogerenciamento.

Cogerenciamento oferece suporte aos seguintes cargas de trabalho:

- Políticas de conformidade  

- Políticas do Windows Update  

- Políticas de acesso a recursos  

- Endpoint Protection  

- Configuração do dispositivo  

- Aplicativos Clique para Executar do Office  

- Aplicativos cliente  

Para obter mais informações, consulte [cargas de trabalho](/sccm/comanage/workloads).



## <a name="monitor-co-management"></a>Monitorar o cogerenciamento

O painel de cogerenciamento ajuda você a analisar os computadores cogerenciados no seu ambiente. Os gráficos podem ajudar a identificar os dispositivos que podem precisar de atenção.

![Captura de tela do painel de cogerenciamento](media/co-management-dashboard.png)

Para obter mais informações, consulte [como monitorar o cogerenciamento](/sccm/comanage/how-to-monitor).



## <a name="next-steps"></a>Próximas etapas

- [Saiba mais sobre o valor imediato e o guia de Introdução do cogerenciamento](/sccm/comanage/quickstarts)  

- [Tutorial: Habilitar o cogerenciamento para clientes existentes do Configuration Manager](/sccm/comanage/tutorial-co-manage-clients)  

