---
title: Plano para o Centro de Software
titleSuffix: Configuration Manager
description: Decida como você deseja configurar e marcar o Centro de Software para que os usuários interajam com o Configuration Manager.
ms.date: 05/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: c6826794-aa19-469d-ae47-1a0db68a1ff1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 50683b43cff113f7cd77efb5d8798fd24b53f90a
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106515"
---
# <a name="plan-for-software-center"></a>Plano para o Centro de Software

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os usuários alteram configurações, procuram e instalam aplicativos do Centro de Software. Quando você instala o cliente do Configuration Manager em um dispositivo do Windows, ele automaticamente instala o Centro de Software. O novo Centro de Software tem uma aparência moderna. Os aplicativos que só eram exibidos no Catálogo de Aplicativos dependente do Silverlight (aplicativos disponíveis para o usuário) agora aparecem no Centro de Software sob a guia **Aplicativos**.

Para saber mais sobre os outros recursos do Centro de Software, veja o [Guia do usuário do Centro de Software](/sccm/core/understand/software-center).  


## <a name="bkmk_userex"></a> Configurar Centro de Software  

Analise as melhorias a seguir ao Centro de Software:

### <a name="starting-in-version-1802"></a>A partir da versão 1802

- A configuração do cliente **Usar o novo Centro de Software** no grupo **Agente de computador** está habilitada por padrão. A versão anterior do Centro de Software não tem mais suporte. Para saber mais, consulte [Recursos removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

- Os usuários podem procurar e instalar aplicativos disponíveis para usuários em dispositivos ingressados no Azure Active Directory (Azure AD). Para obter mais informações, consulte [Implantar aplicativos disponíveis para o usuário em dispositivos ingressados no Azure AD](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices).  

### <a name="starting-in-version-1806"></a>A partir da versão 1806

- Especifique a visibilidade do link do site do Catálogo de Aplicativos na guia **Status da Instalação** no Centro de Software. Para saber mais, veja [Configurações de cliente do Centro de Software](/sccm/core/clients/deploy/about-client-settings#software-center).  

- As funções do catálogo de aplicativos não são mais necessárias para exibir aplicativos disponíveis para o usuário no Centro de Software. Essa alteração ajuda a reduzir a infraestrutura de servidor necessária para fornecer aplicativos aos usuários. O Centro de Software agora depende do ponto de gerenciamento para obter essas informações, o que ajuda ambientes maiores a serem melhor dimensionados por meio de suas atribuições a [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups#management-points).<!--1358309-->  

    > [!Note]  
    > Se você estiver usando o catálogo de aplicativos e atualizar o Configuration Manager para a versão 1806, ele continuará a funcionar. As funções de ponto de site do catálogo de aplicativos e ponto de serviço Web não são mais *necessárias*, mas ainda são *compatíveis*. Não há mais suporte para a **experiência do usuário do Silverlight** para o *ponto do site* do Catálogo de Aplicativos. Para saber mais, consulte [Recursos removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).
    >
    > Comece planejando a remoção das funções de catálogo do aplicativo de sua infraestrutura no futuro. Aproveite as melhorias do Centro de Software para usar o ponto de gerenciamento e simplifique seu ambiente do Configuration Manager.  

Use a tabela a seguir para ajudar a reconhecer os requisitos do Centro de Software, dependendo da versão específica do Configuration Manager:

| Tipo de dispositivo | Versão do site | Infraestrutura |
|-----------------|--------------|----------------|
| Dispositivo ingressado no Azure AD<br>(ou "ingressado no domínio de nuvem") | 1802 ou 1806 | Ponto de gerenciamento para todas as implantações de aplicativo |
| [Dispositivo híbrido que tenha ingressado no Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) na Internet | 1802 ou 1806 | Gateway de gerenciamento de nuvem e ponto de gerenciamento para todas as implantações de aplicativo |
| Dispositivo ingressado no domínio do Active Directory no local | 1802 | Catálogo de aplicativos necessário para os aplicativos disponíveis para o usuário por meio do Centro de Software |
| Dispositivo ingressado no domínio do Active Directory no local | 1806 | Ponto de gerenciamento para todas as implantações de aplicativo |

> [!Important]  
> Para aproveitar os novos recursos do Configuration Manager, primeiro atualize os clientes para a versão mais recente. Embora a nova funcionalidade seja exibida no console do Configuration Manager quando você atualiza o site e o console, o cenário completo só funcionará quando a versão do cliente também for a mais recente.


## <a name="bkmk_impact"></a> Substituir as notificações do sistema por uma janela de diálogo

<!--3555947-->
Às vezes, os usuários não veem a notificação do sistema do Windows sobre uma reinicialização ou implantação necessária. Assim, eles não veem a experiência de adiar o lembrete. Esse comportamento pode levar a uma experiência ruim para o usuário quando o cliente alcança um prazo final.

A partir da versão 1902, quando [alterações de software são necessárias](#software-changes-are-required) ou implantações [precisam de uma reinicialização](#restart-required), você tem a opção de usar uma janela de caixa de diálogo mais intrusiva.

### <a name="software-changes-are-required"></a>São necessárias alterações de software

Ao [implantar um aplicativo](/sccm/apps/deploy-use/deploy-applications) conforme necessário, com uma data limite no futuro, na página **Experiência do Usuário** do Assistente para Implantar Software, selecione as seguintes opções de notificação de usuários:

- **Exibir no Centro de Software e mostrar todas as notificações**
- **Quando forem necessárias alterações no software, mostrar uma janela de caixa de diálogo ao usuário em vez de uma notificação do sistema**

Esta configuração de implantação altera a experiência do usuário para esse cenário.

Na seguinte notificação do sistema:

![Notificação do sistema de que são necessárias alterações de Software](media/3555947-required-toast.png)  

Para a janela de diálogo a seguir:

![Janela de diálogo para alterações de software necessárias](media/3555947-required-dialog.png)


### <a name="restart-required"></a>Reinicialização necessária

No grupo [Reinicialização do Computador](/sccm/core/clients/deploy/about-client-settings#computer-restart) de configurações do cliente, habilite a opção a seguir: **Quando uma implantação exigir uma reinicialização, mostrar uma janela de caixa de diálogo ao usuário em vez de uma notificação do sistema**.  

Essa configuração de cliente altera a experiência do usuário para todas as implantações necessárias que exigem uma reinicialização dos seguintes tipos:

- [Aplicativo](/sccm/apps/deploy-use/deploy-applications)
- [Sequência de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)
- [Atualização de software](/sccm/sum/deploy-use/deploy-software-updates)

Na seguinte notificação do sistema:

![Notificação do sistema de Reinicialização necessária](media/3555947-restart-toast.png)  

Para a janela de diálogo a seguir:

![Janela de diálogo para Reiniciar o computador](media/3555947-restart-dialog.png)


## <a name="branding-software-center"></a>Centro de Software de identidade visual

Altere a aparência do Centro de Software para atender aos requisitos e identidade visual da sua organização. Essa configuração ajuda os usuários a confiar no Centro de Software.

O Configuration Manager aplica a identidade visual personalizada para o Centro de Software de acordo com as seguintes prioridades:  

- Se você ainda não instalou o catálogo de aplicativos (recomendado):  

    1. Configurações do cliente do **Centro de Software**. Para obter mais informações, consulte [Sobre as configurações do cliente](/sccm/core/clients/deploy/about-client-settings#software-center).  

    2. Configurações do cliente **Nome da organização** no grupo **Agente de computador**. Para obter mais informações, consulte [Sobre as configurações do cliente](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

- Se você tiver instalado o catálogo de aplicativos:  

    1. Configurações do cliente do **Centro de Software**. Para obter mais informações, consulte [Sobre as configurações do cliente](/sccm/core/clients/deploy/about-client-settings#software-center).  

    2. Se você conectar uma assinatura do Microsoft Intune ao Configuration Manager, o Centro de Software exibirá o *nome da organização*, a *cor* e o *logotipo da empresa* especificados nas propriedades de assinatura do Intune. Para obter mais informações, consulte [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription).  

    3. O *nome da organização* e a *cor* que você especificar nas propriedades de ponto de site do Catálogo de Aplicativos. Para obter mais informações, consulte [Configuration options for Application Catalog website point (Opções de configuração do ponto de sites da Web do catálogo de aplicativos)](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website).  

    4. Configurações do cliente **Nome da organização** no grupo **Agente de computador**. Para obter mais informações, consulte [Sobre as configurações do cliente](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

### <a name="configure-software-center-branding"></a>Configurar identidade visual do Centro de Software

<!-- 1351224 -->
Personalize a aparência do Centro de Software, adicionando os elementos de identidade visual da sua organização e especificando a visibilidade de guias.

Para obter mais informações, consulte os seguintes artigos:

- Configurações do grupo de cliente do [Centro de Software](/sccm/core/clients/deploy/about-client-settings#software-center)  
- [Como definir as configurações do cliente](/sccm/core/clients/deploy/configure-client-settings)  


## <a name="see-also"></a>Consulte também

- [Guia do usuário do Centro de Software](/sccm/core/understand/software-center)
- [Planejar e configurar o gerenciamento de aplicativos](/sccm/apps/plan-design/plan-for-and-configure-application-management)
