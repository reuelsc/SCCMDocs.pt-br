---
title: Coexistência do MDM de terceiros
titleSuffix: Configuration Manager
description: Saiba mais sobre como usar um serviço MDM de terceiros com o Configuration Manager
ms.date: 05/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: ed4dc65e-e5d5-4f75-88ac-f4849ec8fc10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5fbb2d4a902c21ac2fa2186bba70f58d66e50c48
ms.sourcegitcommit: 18ad7686d194d8cc9136a761b8153a1ead1cdc6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66176843"
---
# <a name="third-party-mdm-coexistence-with-configuration-manager"></a>Coexistência do MDM de terceiros com o Configuration Manager

Ao gerenciar simultaneamente os dispositivos Windows 10 com o Configuration Manager e o Microsoft Intune, essa funcionalidade é chamada de [cogerenciamento](/sccm/comanage/overview). Quando você gerencia dispositivos com o Configuration Manager e se registra a um serviço MDM de terceiros, essa funcionalidade é chamada de *coexistência*. Ter duas autoridades de gerenciamento para um único dispositivo pode ser um desafio se ambas não forem orquestradas corretamente. Com o cogerenciamento, o Configuration Manager e o Intune equilibram as [cargas de trabalho](/sccm/comanage/workloads) para garantir que haja nenhum conflito. Essa interação não existe com os serviços de terceiros, portanto, há limitações nos recursos de gerenciamento da coexistência.

O cliente do Configuration Manager pode coexistir com um serviço MDM de terceiros em um dispositivo que executa o Windows 10 versão 1709 ou posterior e tenha ingressado no Azure Active Directory. O dispositivo pode ser de qualquer um dos seguintes tipos:

- Somente [ingressado no Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan). (Esse tipo é às vezes chamado de “ingressado em domínio de nuvem”)  

- [Ingresso no domínio híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan), em que o dispositivo ingressa no seu Active Directory local e é registrado com seu Azure Active Directory.  

> [!Note]  
> Ele não dá suporte a [dispositivos pessoais](https://docs.microsoft.com/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device).  

Quando o cliente do Configuration Manager detecta que um serviço MDM de terceiros também está gerenciando o dispositivo, ele desativará automaticamente determinadas cargas de trabalho no Configuration Manager. Esse comportamento permite que o serviço MDM assuma o controle dessas funções. Também impede configurações conflitantes no cliente que poderiam afetar negativamente a experiência do usuário e o dispositivo. As seguintes cargas de trabalho no Configuration Manager são desativadas neste caso:

- Políticas de acesso a recursos para as configurações de VPN, Wi-Fi, email e certificado
- Gerenciamento de aplicativos, incluindo pacotes herdados
- Verificação e instalação de atualização de softwares
- Proteção de ponto de extremidade, o pacote do Windows Defender com recursos de proteção antimalware
- Política de conformidade para acesso condicional
- Configuração do dispositivo
- Gerenciamento de Clique para Executar do Office

O cliente do Configuration Manager evita conflitos com a autoridade de gerenciamento de terceiros ao dar continuidade às seguintes operações somente leitura:

- Inventário de hardware e software
- Asset Intelligence
- Medição de software
- Relatório de gerenciamento de energia

Para saber mais sobre os benefícios do cogerenciamento com o Configuration Manager e o Intune, confira os [Benefícios do cogerenciamento](/sccm/comanage/overview#benefits).
