---
title: Pacotes de idiomas
titleSuffix: Configuration Manager
description: Saiba mais sobre o suporte de idioma disponível no System Center Configuration Manager.
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a198e15a1ef389d792acc73f2253aa4a704ac35a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="language-packs-in-system-center-configuration-manager"></a>Pacotes de idiomas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico fornece detalhes técnicos sobre o suporte a idioma no System Center Configuration Manager.  

## <a name="BKMK_SupLanguagePacks"></a> Idiomas do sistema operacional com suporte  
 Você pode instalar suporte para os idiomas de exibição nas seguintes tabelas instalando os **pacotes de idiomas do servidor** ou **pacotes de idiomas do cliente** em um site de administração central e em sites primários. Você seleciona os idiomas de cliente e servidor que terão suporte em um site, nos arquivos do pacote de idiomas disponíveis, durante o processo de instalação do site.

 Os arquivos do pacote de idiomas são baixados quando a Instalação é executada como parte do download do arquivo de pré-requisito e redistribuível. Também é possível usar o [Downloader de Instalação](setup-downloader.md) para baixar esses arquivos antes de executar a Instalação.   

 Use a tabela a seguir para mapear uma identificação de localidade para um idioma ao qual deseja oferecer suporte em servidores ou computadores cliente. Para obter mais informações sobre as IDs de localidade, consulte [IDs de localidade atribuídas pela Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=252609).  

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
 Quando você adiciona suporte para idiomas de dispositivo móvel, todos os idiomas do cliente de dispositivo móvel com suporte são incluídos. Você não pode selecionar pacotes de idiomas individuais para suporte a dispositivo móvel.  

### <a name="identify-installed-language-packs"></a>Identificar pacotes de idiomas instalados  
Para identificar os pacotes de idiomas instalados em um computador que executa o cliente do Configuration Manager, procure a LCID (identificação de localidade) dos pacotes de idiomas instalados no Registro do computador. Essas informações estão disponíveis em:

 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs**  

Você pode usar o inventário de hardware para coletar essa informação e criar um relatório personalizado para exibir os detalhes de idioma. Para obter informações sobre como coletar inventário de hardware personalizado, consulte [Como configurar o inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md). Para obter informações sobre como criar relatórios, veja a seção [Gerenciar relatórios do Configuration Manager](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md#BKMK_ManageReports) no tópico [Operações e manutenção de relatórios no System Center Configuration Manager](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md).  
