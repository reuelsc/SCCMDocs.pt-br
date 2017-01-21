---
title: Criar aplicativos do Windows | Microsoft Docs
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
caps.latest.revision: 8
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 557888d1f1f899e3198c430bbe5ccdd44178f824
ms.openlocfilehash: 9c80cc42f9ce6775067a89a9f5a63c1bf4a0c7ca

---
# <a name="create-windows-applications-with-system-center-configuration-manager"></a>Criar aplicativos do Windows com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Além dos outros requisitos e procedimentos do System Center Configuration Manager para criar um aplicativo, você também precisa levar em conta as considerações a seguir ao criar e implantar aplicativos para dispositivos Windows.  

## <a name="general-considerations"></a>Considerações gerais  
 O Configuration Manager dá suporte à implantação dos seguintes tipos arquivo de aplicativo:  

|Tipo de dispositivo|Tipos de arquivos com suporte|  
|-----------------|---------------------|  
|Windows RT e Windows RT 8.1|*.appx, \*.appxbundle|  
|Windows 8.1 e posterior registrados como um dispositivo móvel|*.appx, \*.appxbundle|  

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



<!--HONumber=Dec16_HO3-->


