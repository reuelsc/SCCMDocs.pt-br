---
title: Criar aplicativos do Windows Phone | Microsoft Docs
description: "Consulte quais considerações você deverá levar em conta ao criar e implantar aplicativos para dispositivos Windows Phone."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 866113ff-efd0-40d2-ac3a-2edd49732a24
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 557888d1f1f899e3198c430bbe5ccdd44178f824
ms.openlocfilehash: 5cd1ba42afd13e98565d24d1ec8a3ee209e8532c


---
# <a name="create-windows-phone-applications-with-system-center-configuration-manager"></a>Criar aplicativos do Windows Phone com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Além dos outros requisitos e procedimentos do System Center Configuration Manager para criar um aplicativo, você também precisa levar em conta as considerações a seguir ao criar e implantar aplicativos para dispositivos Windows Phone.  

## <a name="general-considerations"></a>Considerações gerais  
 O Configuration Manager dá suporte à implantação dos seguintes tipos arquivo de aplicativo:  

|Tipo de dispositivo|Tipos de arquivos com suporte|  
|-----------------|---------------------|  
|Windows Phone 8|.xap|  
|Windows Phone 8.1|.xap, .appx, .appxbundle|  

 Há suporte para as seguintes ações de implantação:  

|Tipo de dispositivo|Ações com suporte|  
|-----------------|-----------------------|  
|Windows Phone 8 e Windows Phone 8.1|disponível, necessário, desinstalar|  

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



<!--HONumber=Dec16_HO1-->


