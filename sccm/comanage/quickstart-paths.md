---
title: Caminhos para o cogerenciamento
titleSuffix: Configuration Manager
description: Entenda os pré-requisitos das duas principais formas de configurar o cogerenciamento.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 803f05dd14da8d280f08f2bcf3608865f384d273
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754516"
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
    - Serviços de Federação do Active Directory (ADFS) com autenticação de passagem (PTA)
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

