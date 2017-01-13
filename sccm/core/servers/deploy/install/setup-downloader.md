---
title: "Downloader de instalação | Microsoft Docs"
description: "Leia sobre esse aplicativo autônomo projetado para garantir que a instalação do site use as versões atuais dos principais arquivos de instalação."
ms.custom: na
ms.date: 10/06/2016
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
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: cbe6ebfa80ff8253ec7ed5ad71852fb5cd7e7d91

---
# <a name="setup-downloader-for-system-center-configuration-manager"></a>Downloader de Instalação para System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de executar a Instalação para instalar ou atualizar um site do System Center Configuration Manager, você pode usar o aplicativo autônomo (**Setupdl.exe**) da versão do Configuration Manager que você deseja instalar para baixar arquivos de instalação atualizados exigidos pela instalação.  

O uso de arquivos de instalação atualizados garante que a instalação do site use versões atuais dos principais arquivos de instalação:  

-   Ao usar o Downloader de Instalação para baixar arquivos antes de iniciar a instalação, você especifica uma pasta para conter os arquivos.  

-   A conta usada para executar o Downloader de Instalação deve ter permissões de **Controle Total** sobre a pasta de download.  

-   Ao executar a instalação para instalar ou atualizar um site, você pode direcioná-la para usar a cópia local dos arquivos baixados anteriormente. Isso impede que a instalação precise se conectar à Microsoft quando você inicia a instalação ou a atualização do site.  

-   Você pode usar a mesma cópia local dos arquivos de instalação para as instalações ou atualizações seguintes do site.  

Os tipos de arquivos a seguir são baixados pelo Downloader de Instalação:  

-   Arquivos redistribuíveis de pré-requisitos necessários  

-   Pacotes de idiomas  

-   As atualizações mais recentes de produto para a instalação  

Há duas opções para executar o Downloader de Instalação:  

## <a name="run-setup-downloader-with-the-user-interface"></a>Executar o Downloader de Instalação com a interface do usuário  

1.  Em um computador com acesso à Internet, abra o Windows Explorer e navegue até **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

2.  Clique duas vezes em **Setupdl.exe**. O Downloader de Instalação abrirá.  

3.  Especifique o caminho para a pasta que hospedará os arquivos de instalação atualizados e clique em **Baixar**. O Downloader de Instalação verifica os arquivos que estão atualmente na pasta de download e baixa apenas os arquivos que estão faltando ou que são mais recentes que os arquivos existentes. O Downloader de Instalação cria subpastas para os idiomas baixados. O Downloader de Instalação criará a pasta caso ela não exista.  

4.  Consulte o arquivo **ConfigMgrSetup.log** na raiz da unidade C para analisar os resultados do download.  

## <a name="run-setup-downloader-from-a-command-prompt"></a>Execute o Downloader de Instalação por meio de um prompt de comando  

1.  Abra uma janela do Prompt de Comando e navegue até **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

2.  Digite **setupdl.exe** para abrir o Downloader de Instalação. Opcionalmente, você pode usar as seguintes opções de linha de comando com o setupdl.exe:  

    -   **/VERIFY**: use essa opção para verificar os arquivos na pasta de download, que incluem os arquivos de idiomas. Verifique a lista de arquivos desatualizados no arquivo ConfigMgrSetup.log, na raiz da unidade C. Nenhum arquivo é baixado quando você usa essa opção.  

    -   **/VERIFYLANG**: use essa opção para verificar os arquivos de idiomas na pasta de download. Examine a lista de arquivos de idiomas desatualizados no arquivo ConfigMgrSetup.log, na raiz da unidade C/  

    -   **/LANG**: use essa opção para baixar somente os arquivos de idiomas para a pasta de download.  

    -   **/NOUI**: use essa opção para iniciar o Downloader de Instalação sem exibir a interface do usuário. Ao usar essa opção, você deve especificar o **caminho de download** como parte da linha de comando.  

    -   **&lt;DownloadPath\>**: você pode especificar o caminho para a pasta de download para iniciar automaticamente processo de verificação ou download. Você deve especificar o caminho de download ao usar a opção **/NOUI**. Quando o caminho de download não é especificado, você deve especificar o caminho ao abrir o Downloader de Instalação. O Downloader de Instalação criará a pasta caso ela não exista.  

    Exemplos de uso:  

    -   **setupd &lt;DownloadPath\>**  

        -   O Downloader de Instalação inicia, verifica os arquivos na pasta de download especificada e baixa apenas os arquivos ausentes ou mais recentes que os arquivos existentes  

    -   **setupdl /VERIFY &lt;DownloadPath\>**  

        -   O Downloader de Instalação inicia e verifica os arquivos na pasta de download especificada  

    -   **setupdl /NOUI &lt;DownloadPath\>**  

        -   O Downloader de Instalação inicia, verifica os arquivos na pasta de download especificada e baixa apenas os arquivos ausentes ou mais recentes que os arquivos existentes  

    -   **setupdl /LANG &lt;DownloadPath\>**  

        -   O Downloader de Instalação inicia, verifica os arquivos de idiomas na pasta de download especificada e baixa apenas os arquivos ausentes ou mais recentes que os arquivos existentes  

    -   **setupdl /VERIFY**  

        -   O Downloader de Instalação inicia e, em seguida, você deve especificar o caminho para a pasta de download. Em seguida, depois que você clicar em Verificar, o Downloader de Instalação verificará os arquivos na pasta de download  

3.  Consulte o arquivo **ConfigMgrSetup.log** na raiz da unidade C para analisar os resultados do download  



<!--HONumber=Dec16_HO3-->


