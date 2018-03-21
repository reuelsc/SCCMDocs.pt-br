---
title: Criar aplicativos do Windows
titleSuffix: Configuration Manager
description: "Consulte quais considerações você deverá levar em conta ao criar e implantar aplicativos para dispositivos Windows."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
caps.latest.revision: 
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 76e421571fa96d5e9ee808ac5d61361f52c6cbe3
ms.sourcegitcommit: 52080ef1b0f9a27c123711ef274ac3ffe070e8e0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2018
---
# <a name="create-windows-applications-with-system-center-configuration-manager"></a>Criar aplicativos do Windows com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Além dos outros requisitos e procedimentos do System Center Configuration Manager para criar um aplicativo, você também precisa levar em conta as considerações a seguir ao criar e implantar aplicativos para dispositivos Windows.  

## <a name="general-considerations"></a>Considerações gerais  
 O Configuration Manager dá suporte à implantação dos seguintes tipos arquivo de aplicativo:  

|Tipo de dispositivo|Tipos de arquivos com suporte|  
|-----------------|---------------------|  
|Windows RT e Windows RT 8.1|\*.appx, \*.appxbundle|  
|Windows 8.1 e posterior registrados como um dispositivo móvel|\*.appx, \*.appxbundle|  

 Há suporte para as seguintes ações de implantação:  

|Tipo de dispositivo|Ações com suporte|  
|-----------------|-----------------------|  
|Windows 8.1 e posterior|disponível, necessário, desinstalar|  
|Windows RT|disponível, necessário, desinstalar|  

## <a name="support-for-universal-windows-platform-uwp-apps"></a>Suporte para aplicativos da UWP (Plataforma Universal do Windows)  
 Dispositivos Windows 10 não exigem uma chave de sideload para instalar aplicativos de linha de negócios. No entanto, para habilitar o sideload, a chave do Registro **HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps** deve ter um valor de 1.  

 Se essa chave do Registro não estiver configurada, o Configuration Manager define automaticamente esse valor como **1** na primeira vez que um aplicativo for implantado no dispositivo. Se você definiu o valor como **0**, o Configuration Manager não poderá alterar o valor automaticamente e a implantação de aplicativos de linha de negócios falhará.  

 Os aplicativos de linha de negócios da Plataforma Universal do Windows devem ser assinados com um certificado de assinatura de código confiável em cada dispositivo no qual o aplicativo será implantado. Você pode usar certificados de uma infra-estrutura de PKI interna ou um certificado de um certificado de raiz pública de terceiros instalado no dispositivo.  

 Em dispositivos Windows Mobile 10, você pode usar um certificado de assinatura de código que não seja da Symantec para assinar aplicativos **. appx** . Para aplicativos **. xap** , bem como pacotes **.appx** criados para Windows Phone 8.1 que você deseja instalar em dispositivos Windows Mobile 10, você deve usar um certificado de assinatura de código da Symantec.  

## <a name="deploy-windows-installer-apps-to-enrolled-windows-10-pcs"></a>Implantar aplicativos do Windows Installer em computadores com Windows 10 registrados  
 O tipo de instalador **Windows Installer por meio de MDM (\*.msi)** permite que você crie e implante aplicativos baseados no Windows Installer em computadores registrados que executam o Windows 10.  

 As seguintes considerações se aplicam quando você usa esse tipo de instalador:  

-   Só é possível carregar um único arquivo com a extensão .msi.  

-   O código do produto do arquivo e a versão do produto são usados para a detecção de aplicativo.  

-   O comportamento de reinicialização padrão do aplicativo é usado. O Configuration Manager não controla isto.  

-   São instalados pacotes do MSI por usuário para um único usuário.  

-   São instalados pacotes do MSI por computador para todos os usuários no dispositivo.  

-   Há suporte para atualizações de aplicativos quando o código do produto MSI de cada versão é o mesmo.  
