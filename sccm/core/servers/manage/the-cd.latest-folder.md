---
title: A pasta CD.Latest
titleSuffix: Configuration Manager
description: Saiba mais sobre o processo que fornece atualizações para o produto, dentro do console do Configuration Manager.
ms.date: 03/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 70612d3f60802892aa99bbc4fc006b9385cb8756
ms.sourcegitcommit: af8693048e6706ffda72572374f56e0bc7dfce2c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/11/2019
ms.locfileid: "57737321"
---
# <a name="the-cdlatest-folder-for-configuration-manager"></a>A pasta CD.Latest do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Configuration Manager dispõe de um processo que fornece atualizações para o produto, dentro do console do programa. Para fornecer suporte a este novo método de atualização do Configuration Manager, criamos uma nova pasta chamada **CD.Latest**. Esta pasta contém uma cópia dos arquivos de instalação do Configuration Manager para a versão atualizada do site.  

A pasta CD.Latest contém uma pasta chamada **Redist**, que contém os arquivos redistribuíveis baixados e usados pela instalação. Esses arquivos são comparados à versão dos arquivos do Configuration Manager encontrados nessa pasta CD.Latest. Ao executar a Instalação de uma pasta CD.Latest, você deve usar os arquivos que correspondem à versão da Instalação. Você pode instruir a instalação a baixar arquivos novos e atuais da Microsoft ou a usar os arquivos da pasta Redist, incluída na pasta CD.Latest.

A mídia da linha de base não inclui uma pasta **Redist**. O site criará uma pasta Redist apenas quando você instalar uma atualização no console. Nesse ínterim, use a pasta Redist que você usou durante a instalação de sites da mídia de linha de base.  

> [!TIP]  
> Verifique se os arquivos redistribuíveis utilizados são atuais. Se você não baixou os arquivos de redistribuição recentemente, planeje-se para permitir que a instalação baixe esses arquivos da Microsoft.   

Os cenários a seguir criam ou atualizam a pasta CD.Latest em um site de administração central ou no servidor do site primário:  

- Quando você instala uma atualização ou um hotfix de dentro do console do Configuration Manager, o site cria ou atualiza a pasta, na pasta de instalação do Configuration Manager.  

- Quando você executa a tarefa de backup interna do Configuration Manager, o site cria ou atualiza a pasta, no local da pasta de backup indicada.  

- Quando você instala um novo site usando a mídia de linha de base, o site cria a pasta CD.Latest.


## <a name="supported-scenarios"></a>Cenários com suporte

Os arquivos de origem da pasta CD.Latest têm suporte para os seguintes cenários:  

### <a name="backup-and-recovery"></a>Backup e descoberta
Para recuperar um site, use os arquivos de origem de uma pasta CD.Latest que corresponda ao site. Quando você executa um backup do site usando a tarefa interna de backup do site, a pasta CD.Latest é incluída como parte do backup.

- Ao reinstalar um site como parte de uma recuperação de site, você instala o site da pasta CD.Latest incluída no backup. Esta ação instala o site usando as versões dos arquivos que correspondem ao backup e ao banco de dados do site.  

    - Caso não tenha acesso à versão correta da pasta CD.Latest, instale um site em ambiente de laboratório para baixar a pasta CD.Latest com as versões do arquivo corretas. Em seguida, atualize esse site para corresponder à versão que você deseja recuperar.  

    - Se não tiver a pasta CD.Latest correta e o respectivo conteúdo disponível, não será possível recuperar um site. Nessa circunstância, é necessário reinstalar o site.  

- Quando não tem uma pasta CD.Latest, mas tem um site primário filho funcional ou um site de administração central, você pode usar esse site como um site de referência para uma recuperação de site.  

### <a name="install-a-child-primary-site"></a>Instale um site primário filho
Quando quiser instalar um novo site primário filho abaixo de um site de administração central que instalou uma ou mais atualizações no console, use os arquivos de instalação e de origem da pasta CD.Latest do site de administração central. Esse processo usa arquivos de instalação de origem que correspondem à versão do site de administração central. Para obter mais informações, consulte [Usar o Assistente de instalação para instalar sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).  

### <a name="expand-a-stand-alone-primary-site"></a>Expandir um site primário autônomo
Quando expandir um site primário autônomo por meio da instalação de um novo site de administração central, use os arquivos de instalação e de origem da pasta CD.Latest do site primário. Este processo usa arquivos de instalação de origem que correspondem à versão do site primário. Para obter mais informações, confira [Expandir um site primário autônomo](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_expand).

### <a name="install-a-secondary-site"></a>Instale um site secundário
<!-- SCCMDocs-pr issue #3164 --> Quando quiser instalar um novo site secundário abaixo de um site primário que instalou uma ou mais atualizações no console, use os arquivos de origem da pasta CD.Latest do site primário. 

Para saber mais, confira [Instalar um site secundário](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_secondary). 


## <a name="unsupported-scenarios"></a>Cenários sem suporte

Não há suporte para os arquivos de origem da pasta CD.Latest atualizada para:  
   
- Instalar um novo site para uma nova hierarquia  
- Atualizar um site do Configuration Manager do Microsoft System Center 2012 para o Branch Atual do System Center Configuration Manager
- Instalar clientes do Configuration Manager
- Instalar consoles do Configuration Manager

