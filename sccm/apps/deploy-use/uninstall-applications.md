---
title: Desinstalar aplicativos
titleSuffix: Configuration Manager
description: Desinstalar aplicativos usando o System Center Configuration Manager
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c0626b94d4ffe97b34a6c8376d6ebaa621d91d44
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142061"
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
> Para implantar o aplicativo com a ação Desinstalar, primeiro você precisa excluir todas as implantações existentes do aplicativo, as implantações simuladas ou as implantações de sequência de tarefas que incluem esse aplicativo. 

 Para obter mais informações sobre como criar tipos de implantação, consulte [Criar aplicativos](../../apps/deploy-use/create-applications.md).  

 Para obter mais informações sobre como implantar um aplicativo, consulte [Implantar aplicativos](../../apps/deploy-use/deploy-applications.md).  

## <a name="uninstall-an-application"></a>Desinstalar um aplicativo  

1.  Configure o tipo de implantação do aplicativo com a linha de comando de desinstalação usando um dos seguintes métodos:  

    -   Na página **Geral** do Assistente para Criar Implantação, selecione a opção **Identificar automaticamente as informações sobre esse tipo de implantação nos arquivos de instalação**. Se as informações estiverem disponíveis nos arquivos de instalação, a linha de comando de desinstalação será automaticamente adicionada às propriedades do tipo de implantação.  

    -   Na página **Conteúdo** do Assistente para Criar Tipo de Implantação, no campo **Programa de Desinstalação**, especifique a linha de comando para desinstalar o aplicativo.  

        > [!NOTE]  
        >  A página **Conteúdo** será exibida somente se você selecionar a opção **Especificar manualmente as informações do tipo de implantação** na página **Geral** do Assistente para Criar Tipo de Implantação.  

    -   Na guia **Programas** da caixa de diálogo **<*nome do tipo de implantação*>, Propriedades**, especifique a linha de comando para desinstalar o aplicativo no campo **Desinstalar programa**.  

2.  Implante o aplicativo e selecione a ação de implantação **Desinstalar** da página **Configurações de Implantação** do Assistente de Implantação de Software.  

    > [!NOTE]  
    >  Quando você selecionar uma ação de implantação de **Desinstalar**, a finalidade da implantação será automaticamente configurada como **Necessário**.  
