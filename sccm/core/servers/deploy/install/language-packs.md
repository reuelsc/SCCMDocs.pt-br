---
title: Pacotes de idiomas | System Center Configuration Manager
description: "Saiba mais sobre o suporte de idioma disponível no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f44ea59b86ace05e6d495aa4311d01518097daf7


---
# <a name="language-packs-in-system-center-configuration-manager"></a>Pacotes de idiomas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico fornece detalhes técnicos sobre o suporte a idioma no System Center Configuration Manager.  

##  <a name="a-namebkmksuplanguagepacksa-supported-operating-system-languages"></a><a name="BKMK_SupLanguagePacks"></a> Idiomas do sistema operacional com suporte  
 Você pode instalar suporte para os idiomas de exibição a seguir instalando **pacotes de idiomas do servidor** ou **pacotes de idiomas do cliente** em um site de administração central e em sites primários. Os arquivos do pacote de idiomas são baixados quando a instalação é executada como parte do download do arquivo de pré-requisito e redistribuível. Também é possível usar o [Downloader de Instalação](setup-downloader.md) para baixar esses arquivos antes de executar a Instalação. Durante a instalação de um site, você seleciona os idiomas de cliente e servidor que terão suporte nesse site nos arquivos do pacote de idiomas disponíveis.  

 Use a tabela a seguir para mapear uma identificação de localidade para um idioma ao qual deseja oferecer suporte em servidores ou clientes. Para obter mais informações sobre as identificações de localidade, consulte [Locale IDs Assigned by Microsoft (IDs de localidade atribuídas pela Microsoft)](http://go.microsoft.com/fwlink/p/?LinkId=252609) na biblioteca online MSDN.  

### <a name="server-languages"></a>Idiomas do servidor  

|Idioma do servidor|LCID (Identificação de localidade)|Código de três letras|  
|---------------------|------------------------|-----------------------|  
|Inglês (padrão)|0409|ENU|  
|Chinês (tradicional, RAE de Hong Kong)|0c04|ZHH|  
|Chinês (simplificado)|0804|CHS|  
|Chinês (tradicional, Taiwan)|0404|CHT|  
|Tcheco|0405|CSY|  
|Holandês - Países Baixos|0413|NLD|  
|Francês|040c|FRA|  
|Alemão|0407|DEU|  
|Húngaro|040e|HUN|  
|Italiano - Itália|0410|ITA|  
|Japonês|0411|JPN|  
|Coreano|0412|KOR|  
|Polonês|0415|PLK|  
|Português - Brasil|0416|PTB|  
|Português - Portugal|0816|PTG|  
|Russo|0419|RUS|  
|Espanhol - Espanha|0c0a|ESN|  
|Sueco|041d|SVE|  
|Turco|041f|TRK|  

### <a name="client-languages"></a>Idiomas do cliente  

|Idioma do cliente|LCID (Identificação de localidade)|Código de três letras|  
|---------------------|------------------------|-----------------------|  
|Inglês (padrão)|0409|ENG|  
|Chinês (tradicional, RAE de Hong Kong)|0c04|ZHH|  
|Chinês - Simplificado|0804|CHS|  
|Chinês (tradicional, Taiwan)|0404|CHT|  
|Tcheco|0405|CSY|  
|Dinamarquês|0406|DAN|  
|Holandês - Países Baixos|0413|NLD|  
|Finlandês|040b|FIN|  
|Francês|040c|FRA|  
|Alemão|0407|DEU|  
|Grego|0408|ELL|  
|Húngaro|040e|HUN|  
|Italiano - Itália|0410|ITA|  
|Japonês|0411|JPN|  
|Coreano|0412|KOR|  
|Norueguês|0414|NOR|  
|Polonês|0415|PLK|  
|Português (Brasil)|0416|PTB|  
|Português (Portugal)|0816|PTG|  
|Russo|0419|RUS|  
|Espanhol - Espanha|0c0a|ESN|  
|Sueco|041d|SVE|  
|Turco|041f|TRK|  

### <a name="mobile-device-client-languages"></a>Idiomas de cliente de dispositivo móvel  
 Quando você adiciona suporte para idiomas de dispositivo móvel, todos os idiomas do cliente de dispositivo móvel são incluídos. Você não pode selecionar pacotes de idiomas individuais para suporte a dispositivo móvel.  

### <a name="how-to-identify-installed-language-packs"></a>Como identificar os pacotes de idiomas instalados  
É possível identificar os pacotes de idiomas instalados em um computador que executa o cliente do Configuration Manager exibindo a LCID (identificação de localidade) dos pacotes de idiomas instalados no Registro do computador. Essa informação está disponível no seguinte local:  

-   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs**  

Você pode usar o inventário de hardware para coletar essa informação e criar um relatório personalizado para exibir os detalhes de idioma. Para obter informações sobre como coletar inventário de hardware personalizado, consulte [Como configurar o inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md). Para obter informações sobre como criar relatórios, veja a seção [Gerenciar relatórios do Configuration Manager](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md#BKMK_ManageReports) no tópico [Operações e manutenção de relatórios no System Center Configuration Manager](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md).  



<!--HONumber=Nov16_HO1-->


