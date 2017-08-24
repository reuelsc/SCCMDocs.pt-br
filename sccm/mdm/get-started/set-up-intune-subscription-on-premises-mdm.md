---
title: Configurar a assinatura do Intune | Microsoft Docs
description: "Configure uma assinatura do Intune rastrear o licenciamento do Gerenciamento de Dispositivo Móvel Local no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 5a81ec06e16992ae1c41b0fc98ebcd07386c5381
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Configure uma assinatura do Microsoft Intune para o gerenciamento de dispositivo móvel local no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Gerenciamento de Dispositivo Móvel Local do System Center Configuration Manager requer uma assinatura do Microsoft Intune para rastrear o licenciamento. O serviço do Intune não é usado para gerenciar os dispositivos ou para armazenar informações de gerenciamento. Para o Gerenciamento de Dispositivo Móvel Local, todo o gerenciamento de dispositivo local é manipulado pela infraestrutura do Configuration Manager.  

> [!NOTE]  
> Com início na versão 1610, o Configuration Manager dá suporte ao uso do Microsoft Intune e à infraestrutura local do Configuration Manager para o gerenciamento de dispositivos móveis ao mesmo tempo.   

> [!TIP]  
>  É recomendável configurar a assinatura do Intune para o Gerenciamento de Dispositivo Móvel Local antes de instalar as funções do sistema de sites necessárias para minimizar o tempo exigido para as funções do sistema de sites recentemente instaladas para se tornarem funcionais.  

##  <a name="sign-up-for-microsoft-intune"></a>Inscreva-se no Microsoft Intune  
 O Intune é para o Gerenciamento de Dispositivo Móvel Local funcionar. Basta [inscrever-se](http://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/) para obter uma avaliação ou assinatura paga e ir para a próxima etapa para adicionar a assinatura ao Configuration Manager.  

##  <a name="add-the-intune-subscription-to-configuration-manager"></a>Adicionar a assinatura do Intune no Configuration Manager  
 Para adicionar a assinatura ao Configuration Manager, siga as mesmas etapas básicas como faria ao adicionar a assinatura no gerenciamento de dispositivo móvel com o Intune. Leia as notas abaixo para conhecer as diferenças específicas e, em seguida, use as instruções em [Configurar sua assinatura do Intune](../deploy-use/configure-intune-subscription.md).  

> [!NOTE]  
>  Ao adicionar a assinatura do Intune, tenha em mente o seguinte:  
>   
>  -   A coleção especificada no assistente de adição de assinatura do Microsoft Intune não é usada para delegação do direito de usuário do Gerenciamento de Dispositivo Móvel Local. Ela é usada somente para o gerenciamento de dispositivo móvel com o Intune. No entanto, você precisa especificar uma coleção para que o assistente continue.  
> -   A configuração de código do site especificada no assistente é ignorada para o Gerenciamento de Dispositivo Móvel Local. O código do site usado é aquele que você especifica no perfil de registro que concede aos usuários permissão para registrar dispositivos.  
> -   Não habilite a autenticação multifatores. Não há suporte no Gerenciamento de Dispositivo Móvel Local.  

##  <a name="configure-the-intune-subscription-for-on-premises-mobile-device-management"></a>Configure a assinatura do Intune para gerenciamento de dispositivo móvel local  

1.  No console do Configuration Manager, clique com o botão direito do mouse em **Assinatura do Microsoft Intune** e clique em **Propriedades**.  

2.  Na caixa Gerenciamento de Dispositivo Móvel Local, escolha um destes procedimentos:

  - Se planejar ter apenas dispositivos locais gerenciados, clique na caixa de seleção próxima à opção **Gerenciar somente dispositivos locais**, e clique em **OK**.  

      > [!NOTE]  
      >  Ao clicar nesta caixa de seleção, você configura a assinatura do Intune para manter todas as informações de gerenciamento local e não replica os dados para a nuvem.  

    - Se você planeja ter dispositivos gerenciados pelo Intune e pelo Configuration Manager local, deixe a caixa desmarcada.

3.  Se você planeja gerenciar dispositivos do Windows Mobile 10, clique com o botão direito do mouse em **Assinatura do Microsoft Intune**, clique em **Configurar Plataformas**e, em seguida, em  **Windows Phone**.  

4.  Clique na caixa de seleção próxima ao **Windows Phone 8.1 e Windows Mobile 10**e, em seguida, clique em **OK**.  

5.  Se você planeja gerenciar computadores desktop com Windows 10, clique com o botão direito do mouse em **Assinatura do Microsoft Intune**, clique em **Configurar plataformas**e, em seguida, em **Habilitar registro do Windows**.  

6.  Clique na caixa de seleção próxima da opção **Habilitar registro do Windows**e, em seguida, clique em **OK**.  
