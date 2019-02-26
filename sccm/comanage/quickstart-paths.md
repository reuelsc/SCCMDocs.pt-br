---
title: Caminhos para o cogerenciamento
titleSuffix: Configuration Manager
description: Entenda os pré-requisitos para as duas principais formas para que você possa configurar o cogerenciamento.
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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754516"
---
# <a name="paths-to-co-management"></a>Caminhos para o cogerenciamento

Há duas maneiras principais para configurar o cogerenciamento. É importante entender os pré-requisitos para cada caminho. Cada um deles exigem uma combinação do Azure Active Directory (Azure AD), o Configuration Manager, o Microsoft Intune e o Windows 10. 

1. [Registrar automaticamente os dispositivos gerenciados pelo Configuration Manager existentes no Intune](#bkmk_path1)  
2. [Inicializar o cliente do Configuration Manager com o provisionamento modernos](#bkmk_path2)  

![Diagrama dos caminhos de cogerenciamento](media/co-management-paths.png)



## <a name="bkmk_path1"></a> Caminho 1: Registro automático de clientes existentes

Levando esse caminho pode obter os dispositivos gerenciados pelo Configuration Manager existentes rapidamente registrados no Intune. O gerenciamento desses dispositivos do Configuration Manager não é diferente de antes de habilitar o cogerenciamento. Agora você pode obter todos os benefícios baseados em nuvem. Esse caminho é transparente para os usuários.

Aqui está o que você precisa configurá-lo:
- Azure AD Híbrido
    - Active Directory Federation Services (ADFS) com autenticação de passagem (PTA)
    - Azure AD Connect
    - Licença do Azure AD Premium
    - Configurar híbrido do Azure AD-junção (escolha uma opção):
        - Para domínios gerenciados
        - Para domínios federados
- Agente cliente de configuração para híbrido do Azure AD-junção
- Configurar o registro automático de dispositivos ao Intune
- Atribuir licenças de usuário do Intune
- Habilitar o cogerenciamento no Configuration Manager

Para obter um tutorial sobre esse caminho, consulte [Tutorial: Habilitar o cogerenciamento para clientes existentes do Configuration Manager](/sccm/comanage/tutorial-co-manage-clients).



## <a name="bkmk_path2"></a> Caminho 2: Inicializar com o provisionamento modernos

Aqui está o que você precisa configurá-lo:

1. [Instalação aprimorada HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)  
2. [Criar os serviços de nuvem no Azure](/sccm/core/servers/deploy/configure/azure-services-wizard)  
3. [Configurar o ponto de gerenciamento e os clientes usem o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  
4. [Usar o Intune para implantar o cliente do Configuration Manager](/sccm/comanage/how-to-prepare-win10)  

> [!Note]  
> Um tutorial para esse caminho está disponível em breve.

