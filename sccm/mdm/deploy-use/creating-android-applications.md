---
title: Criar aplicativos Android
titleSuffix: Configuration Manager
description: "Consulte quais considerações você deverá levar em conta ao criar e implantar aplicativos para dispositivos Android."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
caps.latest.revision: "6"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 2ec4f4fdd1e351379922302e81af88e311a37c8e
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="create-android-applications-with-system-center-configuration-manager"></a>Criar aplicativos Android com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Um aplicativo do System Center Configuration Manager tem um ou mais tipos de implantação. Os tipos de implantação são compostos pelos arquivos de instalação e informações necessárias para implantar o software em um dispositivo. Um tipo de implantação também tem regras que especificam quando e como o software é implantado.  

 Você pode criar aplicativos com os seguintes métodos:  

-   Crie automaticamente os aplicativos e tipos de implantação, lendo os arquivos de instalação do aplicativo.  
-   Crie manualmente o aplicativo e adicione tipos de implantação posteriormente.  
-   Importe um aplicativo de um arquivo.  

Veja [Iniciar o assistente para criar aplicativo](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) e conheça as etapas necessárias para criar os aplicativos do Configuration Manager e os tipos de implantação. Além disso, lembre-se das seguintes considerações ao criar e implantar aplicativos em dispositivos Android.  

## <a name="general-considerations-for-android-apps"></a>Considerações gerais para aplicativos Android

O Configuration Manager dá suporte à implantação dos seguintes tipos de aplicativos para Android:

|Tipo de dispositivo|Arquivos com suporte|
|-|-|
|Android|.apk|

Há suporte para as seguintes ações de implantação:

|Tipo de dispositivo|Ações com suporte|
|-|-|
|Android|**Disponível**, **Necessária** O usuário deve concordar com a instalação e com a desinstalação.|
|Android for Work | **Necessária** |

## <a name="approve-and-deploy-android-for-work-apps"></a>Aprovar e implantar aplicativos do Android for Work
Como administrador do Configuration Manager, você também pode aprovar aplicativos no [site do Play for Work](https://play.google.com/work)e implantar esses aplicativos em dispositivos gerenciados do Android for Work.

Siga essas etapas para aprovar aplicativos na loja Play for Work, sincronizá-los com o console do Configuration Manager e implantá-los em dispositivos Android for Work gerenciados. Para implantar aplicativos nos perfis de trabalho dos usuários, você precisa aprovar os aplicativos na Play for Work e, então, sincronizar os aplicativos com o console do Configuration Manager.

1. Abra um navegador e acesse: https://play.google.com/work.
2. Entre usando a conta de administrador do Google associada ao seu locatário do Intune.
3. Procure os aplicativos que você deseja implantar em seu ambiente e clique em **Aprovar** para cada um deles para disponibilizar o aplicativo no Android for Work.
4. No console do Configuration Manager, vá para **Administrador** > **Visão Geral** > **Serviços de Nuvem** > **Android for Work** e clique em **Sincronizar**.
5. Aguarde 10 minutos para os aplicativos serem sincronizados e vá para **Biblioteca de Software** > **Visão Geral** > **Gerenciamento de Aplicativos** > **Informações sobre Licença para Aplicativos da Loja**.
6. Escolha um aplicativo sincronizado da Play for Work e, em seguida, escolha **Criar Aplicativo**.
7. Conclua o assistente e clique em **Fechar**.
8. Vá para **Biblioteca de Software** > **Visão Geral** > **Gerenciamento de Aplicativos** > **Aplicativos**, selecione um aplicativo do Android for Work e implante como de costume.

Para sincronizar aplicativos da Play for Work com o Configuration Manager, você deve aprovar pelo menos um aplicativo no site do Play for Work primeiro.
