---
title: Configurar o Azure AD híbrido
titleSuffix: Configuration Manager
description: Se seu ambiente tiver atualmente os dispositivos Windows 10 ingressados no domínio, configurar híbrido do Azure AD antes de habilitar o cogerenciamento
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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754520"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>Configurar híbrido do Azure AD para o cogerenciamento

Se você tiver dispositivos Windows 10 ingressados no Active Directory no local, antes de habilitar o cogerenciamento no Configuration Manager, primeiro associe esses dispositivos ao Azure Active Directory (Azure AD). Esse processo é chamado de ingresso no Azure AD híbrido. 

No vídeo a seguir, Sandeep Deo do gerente de programa sênior e gerente de marketing de produto Adam Harbour abordam em configuração de dispositivos no Azure AD de demonstração:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

O híbrido do Azure AD-processo de ingresso automaticamente registra seus dispositivos de domínio local com o Azure AD. Saiba mais sobre esse processo nos seguintes artigos:
- [Introdução ao gerenciamento de dispositivo no Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/device-management-introduction) 
- [Como planejar o seu ingresso do Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)

Ingresso no Azure AD híbrido é uma das principais bases para o cogerenciamento. Esse processo pode ser um desafio para alguns clientes, por exemplo:
- Sua organização usa uma solução de identidade de terceiros 
- As complexidades da configuração de backup o Active Directory Federation Services (ADFS)

Resolver esses desafios pode levar a algumas diretrizes. Este artigo ajuda a reduzir os atrasos.


## <a name="how-to-do-it"></a>Como fazer isso

Dispositivos são semelhantes aos usuários durante a criação de uma identidade que você deseja proteger. Para proteger a identidade do dispositivo a qualquer momento e em qualquer local, você precisa colocar a identidade do dispositivo ao Azure AD.

Com base no tipo de domínio que você está usando, há duas maneiras principais de fazer isso. Configure o ingresso no Azure AD híbrido para um dos seguintes tipos de domínio:  
- [Domínios federados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [Domínios gerenciados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

Os dois métodos anteriores fornecem a melhor experiência. Para informações mais detalhadas, incluindo o processo totalmente manual, consulte os seguintes artigos:
- [Configurar manualmente os dispositivos de ingressados no Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  
- [Autenticação de passagem do ADFS para o Azure AD híbrido](https://docs.microsoft.com/windows-server/identity/ad-fs/ad-fs-overview), que inclui a descoberta do Azure AD  

Para diretrizes de solução de problemas, consulte o [ingresso no AD do Azure Híbrido Windows 10 guia de solução](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).



## <a name="case-study"></a>Estudo de caso

Uma empresa de software europeus grandes com mais de 100.000 usuários em sua rede levou a uma abordagem em fases e granular para habilitar o ingresso no Azure AD híbrido.

Durante a fase de planejamento, como ingresso no Azure AD híbrido é um elemento-chave com suporte a gerenciamento de coadministradores, os administradores do Configuration Manager trabalharam com a equipe de identidade. Essa empresa de software tinha muitas regras do ADFS e algumas delas eram complexas. Para enfrentar esse desafio, a equipe de identidade analisou as regras existentes do AD FS antes de eles habilitado o ingresso no Azure AD híbrido. A equipe de TI também optou por atualizar o Azure AD Connect para a versão mais recente. Agora, o Azure AD Connect fornece um fluxo de processo automatizado para habilitar o ingresso no Azure AD híbrido.

Após o êxito da implantação e teste em seu ambiente de pré-produção, esse cliente habilitada ingresso no Azure AD híbrido para o estado de produção inteira. Dentro de uma semana, eles tinham de todos os dispositivos Windows 10 cogerenciados.



## <a name="contact-fasttrack"></a>Entre em contato com o FastTrack

Se você precisar do Azure AD em qualquer ponto no processo de configuração de assistência, vá para [Microsoft FastTrack](https://Microsoft.com/FastTrack/), entrar e solicitar assistência. 

Para obter mais informações, consulte [Obtenha ajuda do FastTrack](/sccm/comanage/quickstart-fasttrack). 

