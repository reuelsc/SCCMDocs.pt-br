---
title: Localizar um nome da família de pacotes (PFN) para VPN por aplicativo
titleSuffix: Configuration Manager
description: Saiba mais sobre as duas formas de localizar um nome de família de pacotes para que você possa configurar uma VPN por aplicativo.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 47118499-3d26-4c25-bfde-b129de7eaa59
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7021175062a80dffa48a599266fd257c0967e806
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67551397"
---
# <a name="find-a-package-family-name-pfn-for-per-app-vpn"></a>Localizar um nome da família de pacotes (PFN) para VPN por aplicativo

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Há duas maneiras de localizar um PFN para que você possa configurar uma VPN por aplicativo.

## <a name="find-a-pfn-for-an-app-thats-installed-on-a-windows-10-computer"></a>Localizar um PFN para um aplicativo que é instalado em um computador Windows 10

Se o aplicativo com o qual você está trabalhando já estiver instalado em um computador Windows 10, use o cmdlet [Get-AppxPackage](https://technet.microsoft.com/library/hh856044.aspx) do PowerShell para obter o PFN.

A sintaxe de Get-AppxPackage é:

```
Get-AppxPackage [[-Name] <String> ] [[-Publisher] <String> ] [-AllUsers] [-User <String> ] [ <CommonParameters>]
```

> [!NOTE]
> Talvez você precise executar o PowerShell como administrador para recuperar o PFN

Por exemplo, para obter informações sobre todos os aplicativos universais instalados no computador, use `Get-AppxPackage`.

Para obter informações sobre um aplicativo cujo nome você conhece no todo ou parte, use `Get-AppxPackage *<app_name>`. Observe o uso do caractere curinga, que é especialmente útil se você não tem certeza do nome completo do aplicativo. Por exemplo, para obter as informações sobre o OneNote, use `Get-AppxPackage *OneNote`.


Eis aqui as informações recuperadas do OneNote:

`Name                   : Microsoft.Office.OneNote`

`Publisher              : CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US`

`Architecture           : X64`

`ResourceId             :`

`Version                : 17.6769.57631.0`

`PackageFullName        : Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`InstallLocation        : C:\Program Files\WindowsApps`

`\Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`IsFramework            : False`

**`PackageFamilyName      : Microsoft.Office.OneNote_8wekyb3d8bbwe`**

`PublisherId            : 8wekyb3d8bbwe`



## <a name="find-a-pfn-if-the-app-is-not-installed-on-a-computer"></a>Localizar um PFN se o aplicativo não estiver instalado em um computador

1.  Ir para https://www.microsoft.com/en-us/store/apps
2.  Insira o nome do aplicativo na barra de pesquisa. Em nosso exemplo, procure o OneNote.
3.  Clique no link do aplicativo. Observe que a URL que você acessa tem uma série de letras no final. Em nosso exemplo, a URL tem esta aparência: `https://www.microsoft.com/en-us/store/apps/onenote/9wzdncrfhvjl`
4.  Em uma guia diferente, cole a seguinte URL, `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/<app id>/applockerdata`, substituindo `<app id>` pela ID do aplicativo obtida em https://www.microsoft.com/en-us/store/apps – aquela série de letras no final da URL na etapa 3. Em nosso exemplo, o exemplo do OneNote, você deve colar: `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/9wzdncrfhvjl/applockerdata`.

No Microsoft Edge, as informações que você deseja são exibidas; no Internet Explorer, clique em **Abrir** para ver as informações. O valor do PFN é fornecido na primeira linha. Esta é a aparência dos resultados para o nosso exemplo:

```json
{
  "packageFamilyName": "Microsoft.Office.OneNote_8wekyb3d8bbwe",
  "packageIdentityName": "Microsoft.Office.OneNote",
  "windowsPhoneLegacyId": "ca05b3ab-f157-450c-8c49-a1f127f5e71d",
  "publisherCertificateName": "CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US"
}
