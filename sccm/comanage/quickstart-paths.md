---
title: Caminhos para o cogerenciamento
titleSuffix: Configuration Manager
description: Entenda os pré-requisitos das duas principais formas de configurar o cogerenciamento.
ms.date: 06/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4c34cf73133086f08cb390f39ab4fe715dfcefd2
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67550663"
---
# <a name="paths-to-co-management"></a>Caminhos para o cogerenciamento

Há duas principais formas de configurar o cogerenciamento. É importante entender os pré-requisitos de cada caminho. Cada um deles exige uma combinação do Azure Active Directory (Azure AD), Configuration Manager, Microsoft Intune e Windows 10. 

1. [Registrar automaticamente os dispositivos gerenciados existentes pelo Configuration Manager no Intune](#bkmk_path1)  
2. [Iniciar o cliente do Configuration Manager com provisionamento moderno](#bkmk_path2)  

![Diagrama de caminhos de cogerenciamento](media/co-management-paths.png)



## <a name="bkmk_path1"></a> Caminho 1: Registro automático de clientes existentes

Seguir esse caminho pode fazer com que seus dispositivos gerenciados pelo Configuration Manager sejam registrados rapidamente no Intune. O gerenciamento desses dispositivos no Gerenciador de Configurações não é diferente de antes da habilitação do cogerenciamento. Agora você pode obter todos os benefícios baseados em nuvem. Esse caminho é transparente para os usuários.

Veja o que é necessário para configurar:
- Azure AD Híbrido
    - Uma das seguintes [opções de identidade híbrida do Azure AD](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin):  
       - [Sincronização de hash de senha](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#password-hash-synchronization) com [SSO (Logon Único) Contínuo](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [Autenticação de passagem](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta) com [SSO (Logon Único) Contínuo](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [SSO federado (com Serviços de Federação do Active Directory (AD FS))](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)
    - Azure AD Connect
    - Licença do Azure AD Premium
    - Configurar o ingresso no Azure AD híbrido (escolha uma opção):
        - Para domínios gerenciados
        - Para domínios federados
- Configuração do agente cliente para ingresso no Azure híbrido
- Configurar o registro automático de dispositivos ao Intune
- Atribuir licenças de usuário do Intune
- Habilitar o cogerenciamento no Configuration Manager

Para obter um tutorial sobre esse caminho, confira [Tutorial: Habilitar o cogerenciamento de clientes existentes do Configuration Manager](/sccm/comanage/tutorial-co-manage-clients).



## <a name="bkmk_path2"></a> Caminho 2: Iniciar com provisionamento moderno

Veja o que é necessário para configurar:

1. [Configurar o HTTP aprimorado](/sccm/core/plan-design/hierarchy/enhanced-http)  
2. [Criar os serviços de nuvem no Azure](/sccm/core/servers/deploy/configure/azure-services-wizard)  
3. [Configurar o ponto de gerenciamento e os clientes para usar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  
4. [Usar o Intune para implantar o cliente do Configuration Manager](/sccm/comanage/how-to-prepare-win10)  

> [!Note]  
> Um tutorial para esse caminho estará disponível em breve.

