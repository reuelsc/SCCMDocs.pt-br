---
title: Configurar o Azure AD híbrido
titleSuffix: Configuration Manager
description: Se o seu ambiente tiver dispositivos Windows 10 ingressados no domínio, configure o Azure AD híbrido antes de habilitar o cogerenciamento
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 27dd26d1-e99c-4431-b2f8-60406394b6db
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ec02f740485d3f8b466cde0a644aaaa8885b91f2
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754520"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>Configurar o Azure AD híbrido para cogerenciamento

Se você tem dispositivos Windows 10 ingressados no Active Directory local, antes de habilitar o cogerenciamento no Configuration Manager, ingresse esses dispositivos no Azure Active Directory (Azure AD). Esse processo é chamado de ingresso no Azure AD híbrido. 

No vídeo a seguir, o gerente de programas sênior Sandeep Deo e o gerente de marketing de produto Adam Harbour discutem e demonstram a configuração de dispositivos no Azure AD:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

O processo de ingresso no Azure AD híbrido registra automaticamente no Azure AD seus dispositivos ingressados no domínio local. Saiba mais sobre esse processo nos seguintes artigos:
- [Introdução ao gerenciamento de dispositivos no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-introduction) 
- [Como planejar seu ingresso no Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)

O ingresso no Azure AD híbrido é uma das principais bases para o cogerenciamento. Esse processo pode ser um desafio para alguns clientes, por exemplo:
- Sua organização usa uma solução de identidade de terceiros 
- As complexidades de configurar os Serviços de Federação do Active Directory (ADFS)

Resolver esses desafios pode exigir algumas diretrizes. Este artigo ajuda a reduzir os atrasos.


## <a name="how-to-do-it"></a>Como fazer isso

Os dispositivos são semelhantes aos usuários durante a criação de uma identidade que você deseja proteger. Para proteger a identidade do dispositivo a qualquer momento e em qualquer local, você precisa inserir a identidade do dispositivo no Azure AD.

Com base no tipo de domínio que você está usando, há duas maneiras principais de fazer isso. Configure o ingresso no Azure AD híbrido para um dos seguintes tipos de domínio:  
- [Domínios federados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [Domínios gerenciados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

Os dois métodos anteriores proporcionam a melhor experiência. Para saber mais, incluindo o processo manual completo, confira os seguintes artigos:
- [Configurar manualmente dispositivos híbridos ingressados do Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  
- [Autenticação de passagem do ADFS para o Azure AD híbrido](https://docs.microsoft.com/windows-server/identity/ad-fs/ad-fs-overview), que inclui a descoberta do Azure AD  

Para conhecer as diretrizes de solução de problemas, confira o [Guia de solução de problemas do ingresso no Azure AD híbrido do Windows 10](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).



## <a name="case-study"></a>Estudo de caso

Uma grande empresa de software europeia com mais de 100.000 usuários em sua rede adotou uma abordagem granular e em fases para permitir o ingresso híbrido no Azure AD.

Durante a fase de planejamento, como o ingresso no Azure AD híbrido é um elemento essencial de suporte ao cogerenciamento, os administradores do Configuration Manager trabalharam com a equipe de identidade. Essa empresa de software tinha muitas regras do ADFS, e algumas delas eram complexas. Para enfrentar esse desafio, a equipe de identidade analisou as regras existentes do ADFS antes de habilitar o ingresso no Azure AD híbrido. A equipe de TI também optou por atualizar o Azure AD Connect para a versão mais recente. Agora, o Azure AD Connect fornece um fluxo de processo automatizado para habilitar o ingresso no Azure AD híbrido.

Após a implantação e teste bem-sucedidos no ambiente de pré-produção, esse cliente habilitou o ingresso no Azure AD híbrido em toda a área de produção. Dentro de uma semana, todos os dispositivos Windows 10 deles estavam cogerenciados.



## <a name="contact-fasttrack"></a>Entre em contato com o FastTrack

Se você precisar de ajuda para configurar o Azure AD em qualquer ponto do processo, acesse o [Microsoft FastTrack](https://Microsoft.com/FastTrack/), entre e solicite assistência. 

Para saber mais, confira [Obter ajuda do FastTrack](/sccm/comanage/quickstart-fasttrack). 

