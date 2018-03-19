---
title: Criar aplicativos do Windows Phone
titleSuffix: Configuration Manager
description: "Consulte quais considerações você deverá levar em conta ao criar e implantar aplicativos para dispositivos Windows Phone."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68fe11fa-5fb2-4b81-b0f5-b6f2392fb4ad
caps.latest.revision: 
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 154cc1f6e8f16f2bfbb717cfd44fe596b9e31ac5
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="create-windows-phone-applications-with-system-center-configuration-manager"></a>Criar aplicativos do Windows Phone com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Um aplicativo do System Center Configuration Manager tem um ou mais tipos de implantação que abrangem os arquivos de instalação e as informações necessárias para implantar o software em um dispositivo. Um tipo de implantação também tem regras que especificam quando e como o software é implantado.  

 Você pode criar aplicativos com os seguintes métodos:  

-   Crie automaticamente os aplicativos e tipos de implantação, lendo os arquivos de instalação do aplicativo.  

-   Crie manualmente o aplicativo e adicione tipos de implantação posteriormente.  

-   Importe um aplicativo de um arquivo.  

Veja [Iniciar o assistente para criar aplicativo](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) e conheça as etapas necessárias para criar os aplicativos do Configuration Manager e os tipos de implantação. Além disso, lembre-se das seguintes considerações ao criar e implantar aplicativos para dispositivos com Windows Phone.  

## <a name="general-considerations"></a>Considerações gerais  
 O Configuration Manager dá suporte à implantação dos seguintes tipos arquivo de aplicativo:  

|Tipo de dispositivo|Tipos de arquivos com suporte|  
|-----------------|---------------------|  
|Windows Phone 8|.xap|  
|Windows Phone 8.1|.xap, .appx, .appxbundle|
|Windows 10 Mobile|.xap, .appx, .appxbundle|

 Há suporte para as seguintes ações de implantação:  

|Tipo de dispositivo|Ações com suporte|  
|-----------------|-----------------------|  
|Windows Phone 8, Windows Phone 8.1 e Windows 10 Mobile|Disponível, Necessário, Desinstalar|  

## <a name="steps-to-deploy-the-latest-windows-phone-company-portal-app-with-supersedence"></a>Etapas para implantar o aplicativo do portal da empresa mais recente do Windows Phone com substituição  
 A tabela a seguir fornece as etapas, os detalhes e informações adicionais para criar e implantar aplicativos do portal da empresa do Windows Phone 8 mais recentes.  

|Etapa|Mais informações|  
|----------|----------------------|  
|**Etapa 1:** obtenha o aplicativo mais recente do portal da empresa.|Baixe o [Windows Phone 8 company portal app (Aplicativo do Portal da Empresa do Windows Phone 8)](http://go.microsoft.com/fwlink/?LinkId=268440).|  
|**Etapa 2:** assine o aplicativo do portal da empresa com o seu certificado da Symantec.|Para obter informações sobre como assinar o aplicativo do portal da empresa, consulte [Configurar o gerenciamento de dispositivo móvel híbrido do Windows Phone e Windows 10 Mobile com o System Center Configuration Manager e o Microsoft Intune](../../mdm/deploy-use/enroll-hybrid-windows.md).|  
|**Etapa 3:** criar um novo aplicativo com a versão mais recente do aplicativo do portal da empresa e especificar uma relação de substituição.|Para mais informações, consulte [Criar aplicativos](../../apps/deploy-use/create-applications.md) e [Revisar e substituir aplicativos](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Etapa 4:** Adicionar o aplicativo ao Assistente de Assinatura do Microsoft Intune.|Para mais informações, consulte [Configurar o gerenciamento de dispositivo móvel híbrido do Windows Phone e Windows 10 Mobile com o System Center Configuration Manager e o Microsoft Intune](../../mdm/deploy-use/enroll-hybrid-windows.md).|  
|**Etapa 5:** Excluir a implantação que foi automaticamente criada quando você adicionou a aplicativo do portal da empresa ao Assistente de Assinatura do Microsoft Intune.|A assinatura do Microsoft Intune criou uma implantação automática desse aplicativo, já que essa implantação não oferece suporte a substituições.|  
|**Etapa 6:** criar uma nova implantação do aplicativo. Na página **Configurações de Implantação** do **Assistente de Implantação de Software**, marque a opção **Atualizar automaticamente todas as versões substituídas deste aplicativo**.|Crie uma nova implantação com substituição com o aplicativo que você criou com a relação de substituição.|  
|**Etapa 7 (opcional):** por padrão, os aplicativos substitutos são instalados nos dispositivos após 7 dias. Para implantar o aplicativo do portal da empresa antes disso em dispositivos registrados anteriormente, altere a configuração **agendar a reavaliação para implantações** para um valor mais baixo.<br /><br /> Se você definir essa configuração para um valor mais baixo, isso poderá afetar negativamente o desempenho da rede e dos computadores cliente.|Nenhuma informação adicional.|  
