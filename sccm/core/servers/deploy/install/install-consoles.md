---
title: Instalar console
titleSuffix: Configuration Manager
description: "Leia sobre a instalação do console do Configuration Manager para se conectar a um site de administração central ou um site primário."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: f367f94f809863403ed562a65cf44f21de698005
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="install-the-system-center-configuration-manager-console"></a>Instalar o console do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os administradores usam o console do System Center Configuration Manager para gerenciar o ambiente do Configuration Manager. Cada console do Configuration Manager pode se conectar a um site de administração central ou a um site primário. Você não pode conectar um console do Configuration Manager a um site secundário.

> [!NOTE]  
>  Os objetos que um administrador que executa o console vê depende das permissões atribuídas à sua conta de usuário. Para obter mais informações sobre administração baseada em funções, veja [Fundamentals of role-based administration for System Center Configuration Manager (Conceitos básicos de administração baseada em funções do System Center Configuration Manager)](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 Você pode instalar o console do Configuration Manager durante a instalação do servidor do site por meio do Assistente de Instalação ou pode executar um aplicativo de instalação autônomo que usa o Assistente de Instalação.  

 Use o procedimento a seguir para instalar um console do Configuration Manager usando o aplicativo autônomo.  

## <a name="to-install-the-configuration-manager-console-by-using-the-setup-wizard"></a>Para instalar o console do Configuration Manager usando o Assistente de Instalação  

1.  Verifique se você atende a esses requisitos:  

    -  Você tem direitos de **Administrador Local** no computador no qual o console será executado.  

    -   Você tem permissão de **Leitura** para o local dos arquivos de instalação do console do Configuration Manager.  

2.  Vá até um destes locais:  

    -   No servidor do site, vá para **<*Caminho de instalação do servidor do site do Configuration Manager*> \Tools\ConsoleSetup**.  

    -   Da mídia de origem do Configuration Manager, vá para **<*Arquivos de origem do Configuration Manager*>\Smssetup\Bin\I386**.  

    > [!TIP]  
    >  Como uma melhor prática, inicie a instalação do console do Configuration Manager de um servidor do site em vez de iniciar com a mídia de instalação do System Center Configuration Manager. O método de instalação do servidor do site copia os arquivos de instalação do console do Configuration Manager e os pacotes de idioma com suporte do site para a subpasta **Tools\ConsoleSetup**. A instalação do console do Configuration Manager da mídia de instalação sempre instalará a versão em inglês, independentemente dos idiomas com suporte no servidor do site ou das configurações de idioma do sistema operacional executado no computador. Opcionalmente, você pode copiar a pasta **ConsoleSetup** para um local alternativo para iniciar a instalação.

3.  Para abrir o Assistente de Instalação do Console do Configuration Manager, clique duas vezes em **consolesetup.exe**.  

    > [!IMPORTANT]  
    >  Sempre instale o console do Configuration Manager usando consolesetup.exe. Embora o console do Configuration Manager possa ser instalado executando adminconsole.msi, esse método não executa verificações de pré-requisito nem de dependência e a instalação poderá não ser realizada corretamente.  

4.  No assistente, selecione **Avançar**.  

5.  Na página **Servidor do Site**, insira o FQDN (nome de domínio totalmente qualificado) do servidor do site ao qual o console do Configuration Manager se conectará.  

6.  Na página **Pasta de Instalação**, insira a pasta de instalação para o console do Configuration Manager. O caminho da pasta não deve conter espaços à direita ou caracteres Unicode.  

7.  Na página **Programa de Aperfeiçoamento da Experiência do Usuário**, selecione se deseja ingressar no programa.  

8.  Na página **Pronto para Instalar**, selecione **Instalar** para instalar o console do Configuration Manager.  

## <a name="to-install-the-configuration-manager-console-from-a-command-prompt"></a>Para instalar o console do Configuration Manager de um prompt de comando  

1.  No servidor do qual você instala do console do Configuration Manager, abra uma janela do Prompt de Comando e vá para um dos locais a seguir:  

    -   **<*Caminho de instalação do servidor de site do Configuration Manager*>\Tools\ConsoleSetup**  

    -   **<*Mídia de instalação do Configuration Manager*>\SMSSETUP\BIN\I386**  

    > [!TIP]  
    >  Ao instalar o console do Configuration Manager de um prompt de comando, a versão em inglês é sempre instalada, independentemente da configuração de idioma do sistema operacional em execução no computador. Para instalar o console do Configuration Manager em um idioma diferente do inglês, você deve [instalar o console do Configuration Manager usando o Assistente de Instalação](#to-install-the-configuration-manager-console-by-using-the-setup-wizard).  

2.  No prompt de comando, digite **consolesetup.exe**. Escolha entre as seguintes opções de linha de comando.  

|  Opção de linha de comando     | Descrição     |
  | :------------- | :------------- |
  |/q|Instala o console do Configuration Manager autônomo. As opções **EnableSQM**, **TargetDir**e **DefaultSiteServerName** são necessárias ao usar essa opção.|  
  |/uninstall|Desinstala o console do Configuration Manager. Você deve especificar essa opção primeiro ao usá-la com a opção **/q** .|  
  |LangPackDir|Especifica o caminho para a pasta que contém os arquivos de idioma. Você pode usar o **Downloader de Instalação** para baixar os arquivos de idioma. Se você não usar esta opção, o programa de instalação procurará a pasta de idioma na pasta atual. Se a pasta de idioma não for encontrada, o programa de instalação continuará instalando somente o idioma inglês. Para obter mais informações, consulte [Downloader de Instalação](setup-downloader.md).|  
  |TargetDir|Especifica a pasta de instalação para instalar o console do Configuration Manager. Essa opção é necessária ao usar a opção **/q** .|  
  |EnableSQM|Especifica se deve associar-se o CEIP (Programa de Aperfeiçoamento da experiência do Usuário). Use um valor de **1** para ingressar no Programa de Aperfeiçoamento da Experiência do Usuário e um valor de **0** para não ingressar no programa. Essa opção é necessária ao usar a opção **/q** .|  
  |DefaultSiteServerName|Especifica o FQDN do servidor do site ao qual o console se conecta quando ele é aberto. Essa opção é necessária ao usar a opção **/q** .|  


  **Exemplos:**

  -  **consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr" Console EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /uninstall /q**  
