---
title: Pacotes de idiomas
titleSuffix: Configuration Manager
description: Saiba mais sobre o suporte de idioma disponível no Configuration Manager.
ms.date: 06/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 54034ec94ad2a0ea2b7ce095d9da669aea02f0b3
ms.sourcegitcommit: 702e6017b6dee4629b67bb9f3bd5d9b5a889ebee
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37340219"
---
# <a name="language-packs-in-configuration-manager"></a>Pacotes de idioma no Gerenciador de Configurações

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo fornece detalhes técnicos sobre o suporte a idioma no Configuration Manager. Os clientes e servidores de site do Configuration Manager são considerados como tendo neutralidade de idioma. Adicione suporte para idiomas de exibição instalando **pacotes de idiomas do servidor** ou **pacotes de idiomas do cliente** em um site de administração central e em sites primários. Você seleciona os idiomas de cliente e servidor que terão suporte em um site, nos arquivos do pacote de idiomas disponíveis, durante o processo de instalação do site.
 
Instale vários idiomas em cada site. Você só precisa instalar os idiomas que usa.  

- Cada site dá suporte a vários idiomas para consoles do Configuration Manager.  

- Adicione suporte apenas para os idiomas do cliente aos quais você deseja dar suporte instalando pacotes de idiomas de cliente individuais em cada site.  

Quando você instala o suporte para um idioma que corresponde aos seguintes componentes:  

- O idioma de exibição de um computador: o console do Configuration Manager e a interface do usuário que é executada nesse computador exibem informações nesse idioma.  

- A preferência de idioma em uso pelo navegador da Web de um computador, as conexões com informações baseadas na web, incluindo o Catálogo de Aplicativos ou o SQL Server Reporting Services, são exibidas nesse idioma.  


Quando você executa a instalação do Configuration Manager, ele baixa os arquivos de pacote de idiomas como parte dos pré-requisitos e arquivos redistribuíveis. Também é possível usar o [downloader de instalação](setup-downloader.md) para baixar esses arquivos antes de executar a Instalação.   



## <a name="server-languages"></a>Idiomas do servidor  

Use a tabela a seguir para mapear uma identificação de localidade para um idioma ao qual deseja oferecer suporte em servidores. Para obter mais informações sobre as IDs de localidade, consulte [IDs de localidade atribuídas pela Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=252609).  

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



## <a name="client-languages"></a>Idiomas do cliente  

Use a tabela a seguir para mapear uma identificação de localidade para um idioma ao qual deseja oferecer suporte em computadores cliente. Para obter mais informações sobre as IDs de localidade, consulte [IDs de localidade atribuídas pela Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=252609).  

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



## <a name="identify-installed-language-packs"></a>Identificar pacotes de idiomas instalados  
Para identificar os pacotes de idiomas instalados em um computador que executa o cliente do Configuration Manager, procure a LCID (identificação de localidade) dos pacotes de idiomas instalados no Registro do computador. Estas informações estão disponíveis no seguinte caminho do Registro:  

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs`  

Personalize o inventário de hardware para coletar essas informações. Em seguida, crie um relatório personalizado para exibir os detalhes de idioma. Para saber mais sobre a coleta de inventário de hardware personalizado, confira [Como configurar o inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory). Para saber mais sobre como criar relatórios, veja [Gerenciar relatórios do Configuration Manager](/sccm/core/servers/manage/operations-and-maintenance-for-reporting#BKMK_ManageReports).  
