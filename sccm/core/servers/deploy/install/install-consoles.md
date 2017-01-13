---
title: Instalar consoles | Microsoft Docs
description: "Leia sobre como instalar consoles do Configuration Manager para se conectar a um site de administração central ou um site primário."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: e3bc8341b384be975098d1b9d7824ef117a47ccb

---
# <a name="install-system-center-configuration-manager-consoles"></a>Instalar consoles do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Os usuários administrativos usam o console do System Center Configuration Manager para gerenciar o ambiente do Configuration Manager. Cada console do Configuration Manager pode se conectar a um site de administração central ou um site primário. Você não pode conectar um console do Configuration Manager a um site secundário.


> [!NOTE]  
>  Os objetos exibidos para o usuário administrativo que está executando o console dependem dos direitos atribuídos ao usuário administrativo. Para obter mais informações sobre administração baseada em funções, veja [Fundamentals of role-based administration for System Center Configuration Manager (Conceitos básicos de administração baseada em funções do System Center Configuration Manager)](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 É possível instalar o console do Configuration Manager durante a instalação do servidor do site no Assistente de Instalação ou executar o aplicativo autônomo.  

 Use o procedimento a seguir para instalar um console do Configuration Manager usando o aplicativo autônomo.  

## <a name="to-install-a-configuration-manager-console"></a>Para instalar um console do Configuration Manager  

1.  Verifique se o usuário administrativo que executa o aplicativo do console do Configuration Manager tem os seguintes direitos de segurança:  

    -   Direitos de**Administrador Local** no computador no qual o console será executado.  

    -   Permissão de**Leitura** para o local dos arquivos de instalação do console do Configuration Manager.  

2.  Navegue até um dos seguintes locais:  

    -   Na mídia de origem do Configuration Manager, navegue até **&lt;ConfigMgrSourceFiles\>\Smssetup\Bin\I386**  

    -   No servidor do site, navegue até **&lt;ConfigMgrSiteServerInstallationPath\>\Tools\ConsoleSetup**  

    > [!TIP]  
    >  Como uma melhor prática, inicie a instalação do console do Configuration Manager de um servidor do site em vez da mídia de instalação do System Center Configuration Manager. O método de instalação do servidor do site copia os arquivos de instalação do console do Configuration Manager e os pacotes de idioma com suporte do site para a subpasta **Tools\ConsoleSetup**. Se você instalar o console do Configuration Manager da mídia de instalação, esse método de instalação sempre instalará a versão em inglês, independentemente dos idiomas com suporte no servidor do site ou das configurações de idioma para o sistema operacional executado no computador. Opcionalmente, você pode copiar a pasta **ConsoleSetup** para um local alternativo para iniciar a instalação.  

3.  Clique duas vezes em **consolesetup.exe**. O Assistente de Instalação do Console do Configuration Manager se abre.  

    > [!IMPORTANT]  
    >  Sempre instale o console do Configuration Manager usando consolesetup.exe. Embora o console do Configuration Manager possa ser instalado executando AdminConsole.msi, esse método não executa verificações de pré-requisito nem de dependência e a instalação poderá não ser realizada corretamente.  

4.  Na página que se abre, clique em **Próximo**.  

5.  Na página **Servidor do Site**, especifique o FQDN (nome de domínio totalmente qualificado) do servidor do site ao qual o console do Configuration Manager se conectará.  

6.  Na página **Pasta de Instalação**, especifique a pasta de instalação do console do Configuration Manager. O caminho da pasta não deve conter espaços à direita ou caracteres Unicode.  

7.  Na página **Programa de Aperfeiçoamento da Experiência do Usuário** , escolha se deseja ingressar no programa.  

8.  Na página **Pronto para instalar**, clique em **Instalar** para instalar o console do Configuration Manager.  

## <a name="to-install-a-configuration-manager-console-from-a-command-prompt"></a>Para instalar um console do Configuration Manager por meio de um prompt de comando  

1.  No servidor do qual você instala do console do Configuration Manager, abra uma janela do prompt de comando e navegue até um dos locais a seguir:  

    -   **&lt;ConfigMgrSiteServerInstallationPath\>\Tools\ConsoleSetup**  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\I386**  

    > [!TIP]  
    >  Quando você instala um console do Configuration Manager de um prompt de comando, ele sempre instala a versão em inglês, independentemente da configuração de idioma do sistema operacional em execução no computador. Para instalar o console do Configuration Manager em outro idioma, é necessário usar o procedimento anterior para instalá-lo.  

2.  Digite **consolesetup.exe** e escolha entre as seguintes opções de linha de comando.  

|  Opção de linha de comando     | Descrição     |
  | :------------- | :------------- |
  |/q|Instala o console do Configuration Manager autônomo. As opções **EnableSQM**, **TargetDir**e **DefaultSiteServerName** são necessárias ao usar essa opção.|  
  |/uninstall|Desinstala o console do Configuration Manager. Você deve especificar essa opção primeiro ao usá-la com a opção **/q** .|  
  |LangPackDir|Especifica o caminho para a pasta que contém os arquivos de idioma. Você pode usar o **Downloader de Instalação** para baixar os arquivos de idioma. Se você não usar esta opção, o programa de instalação procurará a pasta de idioma na pasta atual. Se a pasta de idioma não for encontrada, o programa de instalação continuará instalando somente o idioma inglês. Para obter mais informações, consulte [Downloader de Instalação](/sccm/core/servers/deploy/install/setup-downloader).|  
  |TargetDir|Especifica a pasta de instalação para instalar o console do Configuration Manager. Essa opção é necessária ao usar a opção **/q** .|  
  |EnableSQM|Especifica se deve associar-se o CEIP (Programa de Aperfeiçoamento da experiência do Usuário). Use um valor de 1 para se associar ao Programa de Aperfeiçoamento da Experiência do Usuário, e um valor de 0 para não se associar ao programa. Essa opção é necessária ao usar a opção **/q** .|  
  |DefaultSiteServerName|Especifica o FQDN do servidor do site ao qual o console se conecta quando ele é aberto. Essa opção é necessária ao usar a opção **/q** .|  


  **Exemplos de uso:**  
  -  **consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr" Console EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /uninstall /q**  



<!--HONumber=Dec16_HO3-->


