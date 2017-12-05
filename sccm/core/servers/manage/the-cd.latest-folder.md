---
title: A pasta CD.Latest
titleSuffix: Configuration Manager
description: "Saiba mais sobre o novo processo de atualização que fornece atualizações para o produto de dentro do console do Configuration Manager."
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
caps.latest.revision: "6"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 1dd176f80afa4a9edc5a14d538eef7989614e814
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2017
---
# <a name="the-cdlatest-folder-for-system-center-configuration-manager"></a>A pasta CD.Latest para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager introduz um novo processo de atualização que fornece atualizações para o produto de dentro do console do Configuration Manager. Para dar suporte a esse novo método de atualização do Configuration Manager, foi criada uma nova pasta com o nome **CD.Latest** que contém uma cópia dos arquivos de instalação do Configuration Manager para a versão atualizada do seu site.  

A partir da atualização 1606, a pasta CD.Latest mais recente contém uma pasta chamada **Redist** que contém os arquivos redistribuíveis que a instalação baixa e usa. Esses arquivos são comparados à versão dos arquivos do Configuration Manager encontrados nessa pasta CD.Latest. Ao executar a Instalação de uma pasta CD.Latest, você deve usar os arquivos que correspondem à versão da Instalação. Para fazer isso, você pode instruir a Instalação a baixar arquivos novos e atuais da Microsoft ou instruir a Instalação a usar os arquivos na pasta Redist incluída na pasta CD.Latest.

No entanto, a mídia de linha de base, como a versão de linha de base 1606 lançada em outubro de 2016, não inclui uma pasta Redist. A pasta Redist não será criada até que você instalar uma atualização no console. Nesse ínterim, use a pasta Redist que você usou durante a instalação de sites da mídia de linha de base.  

> [!TIP]
> Se ainda não tiver instalado a versão 1606, certifique-se de que os arquivos de redistribuição usados sejam atuais. Se não tiver baixado arquivos de redistribuição recentemente, planeje para permitir que a Instalação os baixe da Microsoft.   

 Veja a seguir os cenários que criam ou atualizam a pasta CD.Latest em um site de administração central ou servidor de site primário:  

-   Você instala uma atualização ou hotfix de dentro do console do Configuration Manager: a pasta é criada ou atualizada na pasta de instalação do Configuration Manager.  

-   Você executa a tarefa de backup interna do Configuration Manager: a pasta é criada ou atualizada no local da pasta de backup indicada.  

-  A partir da versão 1606, a pasta CD.Latest é criada quando você instala um novo site usando a mídia de linha de base (como a versão 1606 ou 1702).

Os arquivos de origem da pasta CD.Latest têm suporte para o seguinte:  

1.  **Backup e recuperação:** para recuperar um site, você deverá usar os arquivos de origem de uma pasta CD.Latest que corresponde a seu site. Quando você executa um backup do site usando a tarefa interna de backup do site, a pasta CD.Latest é incluída como parte do backup.

    -   **Ao reinstalar um site como parte de uma recuperação de site,** você instala o site da pasta CD.Latest incluída no backup. Isso instala o site usando as versões dos arquivos que correspondem ao backup do seu site e ao banco de dados do site.  Se você não tiver acesso à versão correta da pasta CD.Latest, poderá obter uma pasta CD.Latest com as versões de arquivo corretas instalando um site em um ambiente de laboratório e, em seguida, atualizando esse site para corresponder à versão que você deseja recuperar.

        > [!IMPORTANT]  
        >  Se a pasta CD.Latest correta e seu conteúdo não estiverem disponíveis, você não poderá recuperar um site e deverá reinstalá-lo.  

    -   Quando você não tiver uma pasta CD.Latest, mas tiver um site primário filho funcional ou um site de administração central, poderá usar esse site como um site de referência para uma recuperação de site.  

2.  **Para instalar um site primário filho:** quando você quiser instalar um novo site primário filho abaixo de um site de administração central que instalou uma ou mais atualizações no console, será necessário usar os arquivos de Instalação e os arquivos de origem da pasta CD.Latest do site de administração central. Quando a Instalação é executada de uma cópia da pasta CD.Latest do site de administração central, ela usa os arquivos de origem de instalação que correspondem à versão do site de administração central. Para obter mais informações, consulte [Usar o Assistente de instalação para instalar sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  

3.  **Para expandir um site primário autônomo:** quando você expande um site primário autônomo por meio da instalação de um novo site de administração central, é necessário usar os arquivos da Instalação e de origem da pasta CD.Latest do site primário para instalar o novo site de administração central. Quando é executado a partir de uma cópia da pasta CD.Latest do site primário, ele usa os arquivos de origem da instalação que correspondem à versão do site primário. Para obter mais informações, consulte [Expand a stand-alone primary site](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand) (Expandir um site primário autônomo) no tópico [Use the Setup Wizard to install sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) (Usar o Assistente de Instalação para instalar sites)

> [!IMPORTANT]  
>  Não há suporte para os arquivos de origem da CD.Latest atualizada para:  
>   
>  -   Instalar um novo site para uma nova hierarquia  
>  -   Atualizar um site do Microsoft System Center 2012 Configuration Manager para o System Center Configuration Manager
