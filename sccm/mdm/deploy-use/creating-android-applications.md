---
title: Criar aplicativos Android
titleSuffix: Configuration Manager
description: Como criar e implantar aplicativos para dispositivos Android no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ef070186112642d204aade24039da87c0e3a22f0
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139663"
---
# <a name="create-android-applications-in-configuration-manager"></a>Criar aplicativos Android no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Um aplicativo do Configuration Manager tem um ou mais tipos de implantação. Os tipos de implantação são compostos pelos arquivos de instalação e informações necessárias para implantar o software em um dispositivo. Um tipo de implantação também tem regras que especificam quando e como o software é implantado.  

Confira [Criar um aplicativo](/sccm/apps/deploy-use/create-applications#bkmk_create) para obter as etapas para criar aplicativos do Configuration Manager e tipos de implantação. 

Lembre-se das seguintes considerações ao criar e implantar aplicativos para dispositivos Android:  



## <a name="general-considerations-for-android-apps"></a>Considerações gerais para aplicativos Android

O Configuration Manager dá suporte à implantação de pacotes .apk do Android. 

Ele permite as seguintes ações de implantação:

|Tipo de dispositivo|Ações com suporte|
|-|-|
|Android|**Disponível**, **necessária**: O usuário deve concordar com a instalação e com a desinstalação.|
|Android for Work |**Disponível**, **Obrigatória** |



## <a name="approve-and-deploy-android-for-work-apps"></a>Aprovar e implantar aplicativos do Android for Work

Como administrador do Configuration Manager, você também pode aprovar aplicativos no [site Play for Work](https://play.google.com/work). Em seguida, implante esses aplicativos em dispositivos Android for Work gerenciados.

Siga essas etapas para aprovar aplicativos na loja Play for Work, sincronizá-los com o console do Configuration Manager e implantá-los em dispositivos Android for Work gerenciados. Para implantar aplicativos nos perfis de trabalho dos usuários, você precisa aprovar os aplicativos no Play for Work. Em seguida, sincronize os aplicativos com o console do Configuration Manager.

1. Abra um navegador e acesse: https://play.google.com/work.  

2. Entre usando a conta do administrador do Google associada ao seu locatário do Microsoft Intune.  

3. Procure aplicativos que você deseja implantar em seu ambiente. Escolha **Aprovar** para cada um deles para disponibilizar o aplicativo ao Android for Work.  

4. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Android for Work**.  

5. Clique em **Sincronizar** na faixa de opções.  

6. Espere até 10 minutos para que os aplicativos sejam sincronizados. Em seguida, acesse o workspace **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e selecione o nó **Informações sobre Licença para Aplicativos da Store**.  

7. Selecione um aplicativo sincronizado do Play for Work e clique em **Criar Aplicativo**.  

8. Conclua o assistente.  

9. Acesse o workspace **Biblioteca de Software**, expanda **Gerenciamento de Aplicativos** e selecione o nó **Aplicativos**. Selecione um aplicativo Android for Work e implante-o como de costume.  

Para sincronizar aplicativos do Play for Work com o Configuration Manager, primeiro aprove pelo menos um aplicativo no site Play for Work.

Os aplicativos implantados como **Disponíveis** são exibidos no aplicativo Google Play com selo de trabalho em vez de no Portal da Empresa. Isso permite que você implante aplicativos de uma fonte confiável. O aplicativo Google Play com selo de trabalho é uma fonte confiável. Você não precisa permitir aplicativos de fontes não confiáveis.
