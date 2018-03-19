---
title: Desinstalar aplicativos
titleSuffix: Configuration Manager
description: Desinstalar aplicativos usando o System Center Configuration Manager
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
caps.latest.revision: 
caps.handback.revision: 
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 11b6f7ad65296131622b707fcb68d77183e3a288
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="uninstall-applications-with-system-center-configuration-manager"></a>Desinstalar aplicativos com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Execute as seguintes ações para desinstalar um aplicativo implantado anteriormente.

-   Especifique a linha de comando para desinstalar o conteúdo do tipo de implantação na página **Conteúdo** do Assistente para Criar Tipo de Implantação.  

-   Implante o aplicativo usando uma ação de implantação de **Desinstalar**.  

> [!IMPORTANT]  
> Alguns tipos de aplicativos não oferecem suporte para a desinstalação.  

 Esta lista fornece mais informações sobre como funciona a desinstalação do aplicativo:  

-   Quando você desinstala um aplicativo do System Center Configuration Manager (Configuration Manager), os aplicativos dependentes não são automaticamente desinstalados.  

-   Se você implantar um aplicativo que utiliza uma ação de **Desinstalar** para um usuário e o aplicativo tiver sido instalado para todos os usuários do computador, a desinstalação poderá falhar caso a conta de usuário não tenha permissões para desinstalar o aplicativo.  

-   Se você remover um usuário ou dispositivo de uma coleção que tem um aplicativo implantado nela, o aplicativo não será automaticamente removido do dispositivo.  

-   Uma implantação com a finalidade da implantação de **Desinstalar** não verifica as regras de requisito. Se o aplicativo estiver instalado no computador em que a implantação é executada, ele será desinstalado.  

> [!IMPORTANT]  
> Exclua quaisquer implantações ou implantações simuladas existentes de um aplicativo para uma coleção para implantar o aplicativo com uma ação de implantação de **Desinstalar**.  

 Para obter mais informações sobre como criar tipos de implantação, consulte [Criar aplicativos](../../apps/deploy-use/create-applications.md).  

 Para obter mais informações sobre como implantar um aplicativo, consulte [Implantar aplicativos](../../apps/deploy-use/deploy-applications.md).  

## <a name="uninstall-an-application"></a>Desinstalar um aplicativo  

1.  Configure o tipo de implantação do aplicativo com a linha de comando de desinstalação usando um dos seguintes métodos:  

    -   Na página **Geral** do Assistente para Criar Implantação, selecione a opção **Identificar automaticamente as informações sobre esse tipo de implantação nos arquivos de instalação**. Se as informações estiverem disponíveis nos arquivos de instalação, a linha de comando de desinstalação será automaticamente adicionada às propriedades do tipo de implantação.  

    -   Na página **Conteúdo** do Assistente para Criar Tipo de Implantação, no campo **Programa de Desinstalação**, especifique a linha de comando para desinstalar o aplicativo.  

        > [!NOTE]  
        >  A página **Conteúdo** será exibida somente se você selecionar a opção **Especificar manualmente as informações do tipo de implantação** na página **Geral** do Assistente para Criar Tipo de Implantação.  

    -   Na guia **Programas** da caixa de diálogo **<*nome do tipo de implantação*>, Propriedades**, especifique a linha de comando para desinstalar o aplicativo no campo **Programa de desinstalação**.  

2.  Implante o aplicativo e selecione a ação de implantação **Desinstalar** da página **Configurações de Implantação** do Assistente de Implantação de Software.  

    > [!NOTE]  
    >  Quando você selecionar uma ação de implantação de **Desinstalar**, a finalidade da implantação será automaticamente configurada como **Necessário**.  
