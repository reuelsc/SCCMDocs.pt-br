---
title: Configurar a assinatura do Intune | Local | System Center Configuration Manager
description: "Configure uma assinatura do Intune rastrear o licenciamento do Gerenciamento de Dispositivo Móvel Local no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
caps.latest.revision: 8
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4daf5d6ea30aa1fb4aa189ef6da9b364fe197805


---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Configure uma assinatura do Microsoft Intune para o gerenciamento de dispositivo móvel local no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Gerenciamento de Dispositivo Móvel Local do System Center Configuration Manager requer uma assinatura do Microsoft Intune para rastrear o licenciamento. O serviço do Intune não é usado para gerenciar os dispositivos ou para armazenar informações de gerenciamento. Para o Gerenciamento de Dispositivo Móvel Local, todo o gerenciamento de dispositivo local é manipulado pela infraestrutura do Configuration Manager.  

> [!IMPORTANT]  
>  O Configuration Manager não dá suporte ao uso do Microsoft Intune e à infraestrutura do Configuration Manager local como autoridades de gerenciamento ao mesmo tempo. Portanto, quando você configura a assinatura do Intune para gerenciamento local, você desabilita efetivamente o gerenciamento do Intune.  

 Configurar o serviço do Intune para funcionar com o Gerenciamento de Dispositivo Móvel Local inclui as seguintes etapas de alto nível:  

-   [Inscreva-se no Microsoft Intune](#bkmk_signup)  

-   [Adicionar a assinatura do Intune no Configuration Manager](#bkmk_addSub)  

-   [Configure a assinatura do Intune para gerenciamento de dispositivo móvel local](#bkmk_configure)  

> [!TIP]  
>  É recomendável configurar a assinatura do Intune para o Gerenciamento de Dispositivo Móvel Local antes de instalar as funções do sistema de sites necessárias para minimizar o tempo exigido para as funções do sistema de sites recentemente instaladas para se tornarem funcionais.  

##  <a name="a-namebkmksignupa-sign-up-for-microsoft-intune"></a><a name="bkmk_signup"></a> Inscrever-se no Microsoft Intune  
 O Intune é para o Gerenciamento de Dispositivo Móvel Local funcionar. Basta [inscrever-se](http://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/) para obter uma avaliação ou assinatura paga e ir para a próxima etapa para adicionar a assinatura ao Configuration Manager.  

##  <a name="a-namebkmkaddsuba-add-the-intune-subscription-to-configuration-manager"></a><a name="bkmk_addSub"></a> Adicionar a assinatura do Intune no Configuration Manager  
 Para adicionar a assinatura ao Configuration Manager, siga as mesmas etapas básicas como faria ao adicionar a assinatura no gerenciamento de dispositivo móvel com o Intune. Leia as notas abaixo para ver as diferenças específicas e use as instruções em [Para criar a assinatura do Microsoft Intune](../../mdm/plan-design/hybrid-mobile-device-management.md#bkmk_subscription) em [Gerenciamento de dispositivo móvel (MDM) híbrido com o System Center Configuration Manager e o Microsoft Intune](../../mdm/plan-design/hybrid-mobile-device-management.md).  

> [!NOTE]  
>  Ao adicionar a assinatura do Intune, tenha em mente o seguinte:  
>   
>  -   A coleção especificada no assistente de adição de assinatura do Microsoft Intune não é usada para delegação do direito de usuário do Gerenciamento de Dispositivo Móvel Local. Ela é usada somente para o gerenciamento de dispositivo móvel com o Intune. No entanto, você precisa especificar uma coleção para que o assistente continue.  
> -   A configuração de código do site especificada no assistente é ignorada para o Gerenciamento de Dispositivo Móvel Local. O código do site usado é aquele que você especifica no perfil de registro que concede aos usuários permissão para registrar dispositivos.  
> -   Não habilite a autenticação multifatores. Não há suporte no Gerenciamento de Dispositivo Móvel Local.  

##  <a name="a-namebkmkconfigurea-configure-the-intune-subscription-for-on-premises-mobile-device-management"></a><a name="bkmk_configure"></a> Configure a assinatura do Intune para o Gerenciamento de Dispositivo Móvel Local  

1.  No console do Configuration Manager, clique com o botão direito do mouse em **Assinatura do Microsoft Intune** e clique em **Propriedades**.  

2.  Na caixa Gerenciamento de Dispositivo Móvel Local, clique na caixa de seleção próxima à opção **Gerenciar somente dispositivos locais**, e clique em **OK**.  

    > [!NOTE]  
    >  Ao clicar nesta caixa de seleção, você configura a assinatura do Intune para manter todas as informações de gerenciamento local e não replica os dados para a nuvem.  

3.  Se você planeja gerenciar dispositivos do Windows Mobile 10, clique com o botão direito do mouse em **Assinatura do Microsoft Intune**, clique em **Configurar Plataformas**e, em seguida, em  **Windows Phone**.  

4.  Clique na caixa de seleção próxima ao **Windows Phone 8.1 e Windows Mobile 10**e, em seguida, clique em **OK**.  

5.  Se você planeja gerenciar computadores desktop com Windows 10, clique com o botão direito do mouse em **Assinatura do Microsoft Intune**, clique em **Configurar plataformas**e, em seguida, em **Habilitar registro do Windows**.  

6.  Clique na caixa de seleção próxima da opção **Habilitar registro do Windows**e, em seguida, clique em **OK**.  



<!--HONumber=Nov16_HO1-->


