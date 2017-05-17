---
title: "Downloader de instalação | Microsoft Docs"
description: "Leia sobre esse aplicativo autônomo projetado para garantir que a instalação do site use as versões atuais dos principais arquivos de instalação."
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 34e24deb90a39bf655a2e24d16cdbe07528e6193
ms.openlocfilehash: b72148ecc16141843178cbd220fe021fab8be992
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017

---
# <a name="setup-downloader-for-system-center-configuration-manager"></a>Downloader de Instalação para System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de executar a Instalação para instalar ou atualizar um site do System Center Configuration Manager, você pode usar o aplicativo autônomo do Downloader de Instalação da versão do Configuration Manager que deseja instalar para baixar os arquivos de Instalação atualizados.  

Usar arquivos de Instalação atualizados garante que a instalação do site use versões atuais dos principais arquivos de instalação. Na visão geral:   
-   Ao usar o Downloader de Instalação para baixar arquivos antes de iniciar a instalação, você especifica uma pasta para conter os arquivos.  
-   A conta usada para executar o Downloader de Instalação deve ter permissões de **Controle Total** sobre a pasta de download.  
-   Ao executar a instalação para instalar ou atualizar um site, você pode direcioná-la para usar a cópia local dos arquivos baixados anteriormente. Isso impede que a instalação precise se conectar à Microsoft quando você inicia a instalação ou a atualização do site.  
-   Você pode usar a mesma cópia local dos arquivos de instalação para as instalações ou atualizações seguintes do site.  

Os tipos de arquivos a seguir são baixados pelo Downloader de Instalação:  
-   Arquivos redistribuíveis de pré-requisitos necessários  
-   Pacotes de idiomas  
-   As atualizações mais recentes de produto para a instalação  

Você tem duas opções para executar o Downloader de Instalação:
- Executar o aplicativo com a interface do usuário
- Para opções de linha de comando, execute o aplicativo em um prompt de comando


## <a name="run-setup-downloader-with-the-user-interface"></a>Executar o Downloader de Instalação com a interface do usuário  

1.  Em um computador com acesso à Internet, abra o Windows Explorer e vá até **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**.  

2.  Para abrir o Downloader de Instalação, clique duas vezes em **Setupdl.exe**.   

3. Especifique o caminho para a pasta que hospedará os arquivos de instalação atualizados e clique em **Baixar**. O Downloader de Instalação verifica os arquivos que estão atualmente na pasta de download. Ele baixa somente os arquivos que estão faltando ou que são mais recentes que os arquivos existentes. O Downloader de Instalação cria subpastas para os idiomas baixados e outras subpastas necessárias.  

4.  Para examinar os resultados de download, abra o arquivo **ConfigMgrSetup.log** no diretório raiz da unidade C.  

## <a name="run-setup-downloader-from-a-command-prompt"></a>Execute o Downloader de Instalação por meio de um prompt de comando  

1.  Em uma janela de Prompt de Comando, vá até **&lt;*Mídia de instalação do Configuration Manager*\>\SMSSETUP\BIN\X64**.   

2.  Para abrir o Downloader de Instalação, execute **Setupdl.exe**.

    Você pode usar as seguintes opções de linha de comando com o **Setupdl.exe**:   

    -   **/VERIFY**: use essa opção para verificar os arquivos na pasta de download, que incluem os arquivos de idiomas. Examine o arquivo ConfigMgrSetup.log no diretório raiz da unidade C para obter uma lista dos arquivos desatualizados. Nenhum arquivo é baixado quando você usa essa opção.  

    -   **/VERIFYLANG**: use essa opção para verificar os arquivos de idiomas na pasta de download. Examine o arquivo ConfigMgrSetup.log no diretório raiz da unidade C para obter uma lista dos arquivos de idiomas desatualizados.

    -   **/LANG**: use essa opção para baixar somente os arquivos de idiomas para a pasta de download.  

    -   **/NOUI**: use essa opção para iniciar o Downloader de Instalação sem exibir a interface do usuário. Ao usar essa opção, você deve especificar o **caminho de download** como parte da linha de comando no prompt de comando.  

    -   **&lt;DownloadPath\>**: você pode especificar o caminho para a pasta de download para iniciar automaticamente processo de verificação ou download. Você deve especificar o caminho de download ao usar a opção **/NOUI**. Se você não especificar um caminho de download, deverá especificar o caminho quando o Downloader de Instalação for aberto. O Downloader de Instalação criará a pasta caso ela não exista.  

    Comandos de exemplo:

    -   **setupd &lt;DownloadPath\>**  

        -   O Downloader de Instalação inicia, verifica os arquivos na pasta de download especificada e baixa apenas os arquivos ausentes ou que têm versões mais recentes do que os arquivos existentes.     

    -   **setupdl /VERIFY &lt;DownloadPath\>**  

        -   O Downloader de Instalação inicia e verifica os arquivos na pasta de download especificada.  

    -   **setupdl /NOUI &lt;DownloadPath\>**  

        -   O Downloader de Instalação inicia, verifica os arquivos na pasta de download especificada e baixa apenas os arquivos ausentes ou que são mais novos do que os arquivos existentes.  

    -   **setupdl /LANG &lt;DownloadPath\>**  

        -   O Downloader de Instalação inicia, verifica os arquivos de idiomas na pasta de download especificada e baixa apenas os arquivos ausentes ou mais recentes que os arquivos existentes.  

    -   **setupdl /VERIFY**  

        -   O Downloader de Instalação inicia e, em seguida, você deve especificar o caminho para a pasta de download. Em seguida, depois que você clicar em **Verificar**, o Downloader de Instalação verificará os arquivos na pasta de download.  

3.  Para examinar os resultados de download, abra o arquivo **ConfigMgrSetup.log** no diretório raiz da unidade C.

