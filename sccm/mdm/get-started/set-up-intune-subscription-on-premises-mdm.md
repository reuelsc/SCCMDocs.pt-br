---
title: Configurar a assinatura do Intune
titleSuffix: Configuration Manager
description: Configurar uma assinatura do Intune para rastrear o licenciamento para o gerenciamento de dispositivo móvel local no Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: aff4fcc67325645387aea1e57354321769a515ca
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62217007"
---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mdm-in-configuration-manager"></a>Configurar uma assinatura do Microsoft Intune para MDM local no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Configuration Manager local gerenciamento de dispositivo móvel (MDM) requer uma assinatura do Microsoft Intune para rastrear o licenciamento. O serviço do Intune não é usado para gerenciar os dispositivos ou armazenar informações de gerenciamento. Para o MDM local, todo o gerenciamento de dispositivo é manipulado pela infraestrutura do Configuration Manager.  

Antes de instalar as funções do sistema de sites necessárias para o MDM local, configure a assinatura do Intune. Essa ação minimiza o tempo necessário para as funções do sistema de sites recentemente instaladas para se tornar funcional.  

> [!Note]  
> Começando na versão 1810, uma conexão do Intune não é mais necessário para novas implantações de MDM local.<!--3607730, fka 1359124--> Sua organização ainda exige licenças do Intune para usar esse recurso. No momento, não é possível remover a conexão do Intune das implantações de MDM locais existentes. Para obter mais informações, confira a [postagem no blog de suporte do Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  



##  <a name="sign-up-for-microsoft-intune"></a>Inscreva-se no Microsoft Intune  

Intune é necessária para tornar o MDM local funcional. [Inscreva-se](https://docs.microsoft.com/intune/free-trial-sign-up) para uma assinatura de avaliação ou paga. Em seguida, vá para a próxima etapa para adicionar a assinatura para o Configuration Manager.  



##  <a name="add-the-intune-subscription-to-configuration-manager"></a>Adicionar a assinatura do Intune no Configuration Manager  

Para adicionar a assinatura para o Configuration Manager, você seguir as mesmas etapas básicas como faria ao adicionar a assinatura para MDM híbrido com o Intune. Leia as notas abaixo para conhecer as diferenças específicas e, em seguida, use as instruções em [Configurar sua assinatura do Intune](/sccm/mdm/deploy-use/configure-intune-subscription).  

> [!NOTE]
>  Ao adicionar a assinatura do Intune, lembre-se as observações a seguir:  
> 
> - A coleção especificada no Assistente de adição Microsoft Intune assinatura não é usada para delegação do direito de usuário do MDM local. Ele só é usado para gerenciamento de dispositivo móvel com o Intune. No entanto, você precisa especificar uma coleção para que o assistente continuar.  
> 
> - O código do site que você especificar no assistente é ignorado para MDM local. Ele usa o código do site que você especificar em que o registro de perfil que concede aos usuários permissão para registrar dispositivos.  
> 
> - Não habilite a autenticação multifator. Não há suporte no MDM local.  



##  <a name="configure-the-intune-subscription-for-on-premises-mdm"></a>Configurar a assinatura do Intune para MDM local  

1. No console do Configuration Manager, vá para o **Administration** espaço de trabalho, expanda **serviços de nuvem**e selecione o **assinaturas do Microsoft Intune** nó. Selecione sua assinatura e, em seguida, escolha **propriedades** na faixa de opções.   

    1. Na seção Mobile gerenciamento de dispositivo local na parte inferior a **geral** página, escolha uma das seguintes opções:

        - Se você planeja ter somente dispositivos locais gerenciados, selecione a opção para **gerenciar somente dispositivos locais**.  

            > [!NOTE]  
            > Quando você habilitar essa opção, você configura a assinatura do Intune para manter todos os management informações locais. Nenhum dado de gerenciamento de dispositivo é replicado para a nuvem.  

        - Se você planeja ter dispositivos gerenciados pelo Intune e Configuration Manager local, não configure essa opção.  

    Selecione **Okey** para fechar as propriedades de assinatura.

2. Se você planeja gerenciar dispositivos Windows 10 Mobile, selecione sua assinatura na lista, selecione **configurar plataformas** na faixa de opções e, em seguida, selecione **Windows Phone**.  

    1. Selecione a opção **Windows Phone 8.1 e Windows 10 Mobile**e, em seguida, selecione **Okey**.  

3. Se você planeja gerenciar computadores desktop com Windows 10, selecione sua assinatura na lista, selecione **configurar plataformas** na faixa de opções e, em seguida, selecione **Windows**.  

    1. Selecione a opção para **registro do Windows permitem**e, em seguida, selecione **Okey**.  

