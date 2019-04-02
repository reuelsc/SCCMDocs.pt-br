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
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754561"
---
# <a name="what-is-co-management"></a>O que é cogerenciamento?

<!-- 1350871 -->
O cogerenciamento é uma das principais formas de conectar a implantação existente do Configuration Manager à nuvem do Microsoft 365. Ele ajuda você a desbloquear recursos adicionais da nuvem, como acesso condicional. 

O cogerenciamento permite gerenciar simultaneamente os dispositivos Windows 10 usando o Configuration Manager e o Microsoft Intune. Ele permite conectar na nuvem seu investimento existente no Configuration Manager agregando novas funcionalidades. Com o cogerenciamento, você tem flexibilidade para usar a solução de tecnologia que funciona melhor para sua organização. 

Quando um dispositivo com Windows 10 tem o cliente do Configuration Manager e está registrado no Intune, você obtém os benefícios de ambos os serviços. Controle de quais cargas de trabalho, se houver, você pode mudar a autoridade do Configuration Manager para o Intune. O Configuration Manager continua gerenciando todas as outras cargas de trabalho, incluindo as que você não mudar para o Intune e todos os outros recursos do Configuration Manager não compatíveis com cogerenciamento.

Você também pode criar um piloto de uma carga de trabalho com um conjunto separado de dispositivos. O piloto permite testar a funcionalidade do Intune com um subconjunto de dispositivos antes de alternar para um grupo maior. 

![Diagrama de visão geral do cogerenciamento](media/co-management-overview.png)



## <a name="paths-to-co-management"></a>Caminhos para o cogerenciamento

Há dois caminhos principais para usar o cogerenciamento:  

- **Clientes existentes do Configuration Manager**: Você tem dispositivos Windows 10 que já são clientes do Configuration Manager. Configure o Azure AD híbrido e registre-os no Intune.  

- **Novos dispositivos baseados na Internet**: Você tem novos dispositivos Windows 10 que ingressam no Azure AD e se registram automaticamente no Intune. Instale o cliente do Configuration Manager para atingir um estado de cogerenciamento.  

Para saber mais sobre os caminhos, confira [Caminhos para o cogerenciamento](/sccm/comanage/quickstart-paths).



## <a name="benefits"></a>Benefícios 

Quando você registra os clientes do Configuration Manager existentes no cogerenciamento, obtém os seguintes benefícios imediatos:  

- Acesso condicional com conformidade do dispositivo  

- Ações remotas baseadas no Intune, por exemplo: reinicialização, controle remoto ou redefinição de fábrica

- Visibilidade centralizada da integridade do dispositivo  

- Vincular usuários, dispositivos e aplicativos com o Azure Active Directory (Azure AD)  

- Provisionamento moderno com o Windows Autopilot  

- Ações remotas

Para saber mais sobre esses benefícios imediatos do cogerenciamento, confira a série de guias de início rápido para [Conectar-se à nuvem com o cogerenciamento](/sccm/comanage/quickstarts).

O cogerenciamento também permite coordenar várias cargas de trabalho com o Intune. Para saber mais, confira a seção [Cargas de trabalho](#workloads). 



## <a name="prerequisites"></a>Pré-requisitos

O cogerenciamento tem esses pré-requisitos nas seguintes áreas:

- [Licenciamento](#licensing)  
- [Configuration Manager](#configuration-manager)  
- [Azure Active Directory](#azure-ad) (Azure AD)  
- [Microsoft Intune](#intune)  
- [Windows 10](#windows-10)  
- [Permissões e funções](#permissions-and-roles)  

### <a name="licensing"></a>Licenciamento

- Azure AD Premium 
- Licença do EMS ou do Intune para todos os usuários  

    > [!Note]  
    > Uma Assinatura EMS (Enterprise Mobility + Security) inclui o Azure Active Directory Premium e o Microsoft Intune.

> [!Tip]  
> Não deixe de atribuir uma licença do Intune à conta que você usa para entrar no seu locatário. Caso contrário, ocorrerá falha ao entrar, com a mensagem de erro “Usuário não reconhecido”.  


### <a name="configuration-manager"></a>Gerenciador de Configurações

O cogerenciamento exige o Configuration Manager versão 1710 ou posterior.

A partir do Configuration Manager versão 1806, você pode conectar várias instâncias do Configuration Manager a um único locatário do Intune. <!--1357944-->  

A habilitação do cogerenciamento em si não exige que você integre seu site ao Azure AD. Para o [segundo cenário de caminho](#paths-to-co-management), os clientes do Configuration Manager baseados na Internet exigem o [CMG (gateway de gerenciamento de nuvem)](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway). O CMG exige que o site seja [integrado ao Azure AD para gerenciamento de nuvem](/sccm/core/servers/deploy/configure/azure-services-wizard). 


### <a name="azure-ad"></a>Azure AD

- Dispositivos Windows 10 devem ser associados ao Azure AD. Eles podem ser de qualquer um dos seguintes tipos:  

    - [Ingressado no Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan), em que o dispositivo ingressa no seu Active Directory local e é registrado com seu Azure Active Directory.  

    - Somente [ingressado no Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan). (Esse tipo é às vezes chamado de “ingressado em domínio de nuvem”)<!--SCCMDocs issue 605-->  


### <a name="intune"></a>Intune

- [Configurar o Intune](https://docs.microsoft.com/intune/setup-steps)  

- [Habilitar o registro automático no Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)  

> [!Note]  
> Se você tiver um ambiente de MDM híbrido (Intune integrado ao Configuration Manager), não será possível habilitar o cogerenciamento. No entanto, você pode iniciar a migração de usuários para o Intune autônomo e, em seguida, habilitar seus dispositivos Windows 10 associados para cogerenciamento. Para obter mais informações sobre como migrar para o Intune autônomo, confira [Iniciar a migração do MDM híbrido para o Intune autônomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).  
> 
> Se você estiver usando [autoridade mista](/sccm/mdm/deploy-use/migrate-mixed-authority), primeiro conclua a migração para o Intune autônomo. Em seguida, defina a autoridade de MDM no Intune antes de configurar o cogerenciamento.<!--SCCMDocs issue #797-->


### <a name="windows-10"></a>Windows 10

Atualize seus dispositivos para o Windows 10, versão 1709 ou posterior. Para saber mais, confira [Adotar o Windows como um serviço](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service).

> [!IMPORTANT]
> Dispositivos móveis Windows 10 não são compatíveis com o cogerenciamento.


### <a name="permissions-and-roles"></a>Permissões e funções
<!--SCCMDocs issue #667-->

| Ação | Função necessária |
|----|----|
| Configurar o gateway de gerenciamento de nuvem no Configuration Manager | **Gerenciador de assinatura** do Azure |
| Criar aplicativos do Azure AD a partir do Configuration Manager | **Administrador global** do Azure AD |
| Importar aplicativos do Azure no Configuration Manager | **Administrador Completo** do Configuration Manager<br>Não são necessárias funções adicionais do Azure |
| Habilitar o cogerenciamento no Configuration Manager | Um usuário do Azure AD<br>**Administrador Completo** do Configuration Manager com **Todos** os direitos de escopo.<!--SCCMDoc issue 626--> | 

Para obter mais informações sobre as funções do Azure, confira [Entender as diferentes funções](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).

Para saber mais sobre as funções do Configuration Manager, confira [Conceitos básicos da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).


## <a name="workloads"></a>Cargas de trabalho 

Você não precisa mudar as cargas de trabalho, ou pode fazê-las individualmente quando estiver pronto. O Configuration Manager continua gerenciando todas as outras cargas de trabalho, incluindo as que você não mudar para o Intune e todos os outros recursos do Configuration Manager não compatíveis com cogerenciamento.

O cogerenciamento oferece suporte às seguintes cargas de trabalho:

- Políticas de conformidade  

- Políticas do Windows Update  

- Políticas de acesso a recursos  

- Endpoint Protection  

- Configuração do dispositivo  

- Aplicativos Clique para Executar do Office  

- Aplicativos cliente  

Para saber mais, confira [Cargas de trabalho](/sccm/comanage/workloads).



## <a name="monitor-co-management"></a>Monitorar o cogerenciamento

O painel de cogerenciamento ajuda você a analisar os computadores cogerenciados no ambiente. Os gráficos podem ajudar a identificar os dispositivos que podem precisar de atenção.

![Captura de tela do painel de cogerenciamento](media/co-management-dashboard.png)

Para saber mais, confira [Como monitorar o cogerenciamento](/sccm/comanage/how-to-monitor).



## <a name="next-steps"></a>Próximas etapas

- [Saiba mais sobre os benefícios imediatos do cogerenciamento e como começar a usá-lo](/sccm/comanage/quickstarts)  

- [Tutorial: Habilitar o cogerenciamento de clientes existentes do Configuration Manager](/sccm/comanage/tutorial-co-manage-clients)  

