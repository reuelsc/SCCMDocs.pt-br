---
title: Instalar console
titleSuffix: Configuration Manager
description: Instale o console do Configuration Manager para se conectar a um site de administração central ou um site primário.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f17e479ef6b285cdb70960471dced73e83af520c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32339427"
---
# <a name="install-the-system-center-configuration-manager-console"></a>Instalar o console do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os administradores usam o console do Configuration Manager para gerenciar o ambiente do Configuration Manager. Cada console do Configuration Manager pode se conectar a um site de administração central ou a um site primário. Não é possível conectar um console do Configuration Manager a um site secundário.

> [!NOTE]  
>  Um administrador vê os objetos no console com base nas permissões atribuídas à sua conta de usuário. Para obter mais informações sobre a administração baseada em funções, consulte [Fundamentos da administração baseada em funções](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 Ao instalar o servidor do site, instale o console do Configuration Manager ao mesmo tempo. Para instalar o console separadamente da instalação do servidor do site, execute o instalador autônomo.  

 Use o procedimento a seguir para instalar o console do Configuration Manager usando o instalador autônomo.  

## <a name="to-install-the-configuration-manager-console-by-using-the-setup-wizard"></a>Para instalar o console do Configuration Manager usando o Assistente de Instalação  

1.  Verifique se você atende a esses requisitos:  

    -  Você tem direitos de **Administrador** local no computador de destino do console.  

    -   Você tem permissão de **Leitura** para o local dos arquivos de instalação do console do Configuration Manager.  

2.  Vá até um destes locais:  

    -   No servidor do site, acesse: `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    -   Na mídia de origem do Configuration Manager, acesse: `<Configuration Manager source files>\Smssetup\Bin\I386`  

    > [!TIP]  
    >  Como uma melhor prática, inicie o instalador do console do Configuration Manager em um servidor do site, em vez de em uma mídia de instalação do System Center Configuration Manager. Ao instalar um servidor do site, ele copia os arquivos de instalação do console do Configuration Manager e os pacotes de idioma compatíveis do site para a subpasta **Tools\ConsoleSetup**. A instalação do console do Configuration Manager por meio da mídia de instalação sempre instala a versão em inglês. Esse comportamento ocorre mesmo se o servidor do site der suporte a idiomas diferentes, ou se o sistema operacional do computador de destino for definido com outro idioma. Opcionalmente, você pode copiar a pasta **ConsoleSetup** para um local alternativo para iniciar a instalação.

3.  Para abrir o Assistente de Instalação do Console do Configuration Manager, clique duas vezes em **consolesetup.exe**.  

    > [!IMPORTANT]  
    >  Sempre instale o console do Configuration Manager usando **consolesetup.exe**. Embora seja possível instalar o console do Configuration Manager executando adminconsole.msi, esse método não executa os pré-requisitos nem as verificações de dependência. A instalação pode não ser instalada corretamente.  

4.  No assistente, selecione **Avançar**.  

5.  Na página **Servidor do Site**, insira o FQDN (nome de domínio totalmente qualificado) do servidor do site ao qual o console do Configuration Manager se conecta.  

6.  Na página **Pasta de Instalação**, insira a pasta de instalação para o console do Configuration Manager. O caminho da pasta não deve conter espaços à direita ou caracteres Unicode.  

7.  Na página **Programa de Aperfeiçoamento da Experiência do Usuário**, selecione se deseja ingressar no programa.  
    > [!Note]  
    > A partir do Configuration Manager versão 1802, o recurso Programa de Aperfeiçoamento da Experiência do Usuário é removido do produto.

8.  Na página **Pronto para Instalar**, selecione **Instalar** para instalar o console do Configuration Manager.  



## <a name="to-install-the-configuration-manager-console-from-a-command-prompt"></a>Para instalar o console do Configuration Manager de um prompt de comando  

1.  No servidor por meio do qual você instala o console do Configuration Manager, abra uma janela do prompt de comando e acesse um dos seguintes locais:  

    -   `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    -   `<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    > [!TIP]  
    >  A instalação do console do Configuration Manager por meio de um prompt de comando sempre instala a versão em inglês. Esse comportamento ocorre mesmo se o sistema operacional do computador de destino for definido com outro idioma. Para instalar o console do Configuration Manager em um idioma diferente do inglês, você deve [instalar o console do Configuration Manager usando o Assistente de Instalação](#to-install-the-configuration-manager-console-by-using-the-setup-wizard).  

2.  No prompt de comando, digite **consolesetup.exe**. Escolha uma das seguintes opções de linha de comando:  

|  Opção de linha de comando     | Descrição     |
  |-------------|-------------|
  |/q|Instala o console do Configuration Manager autônomo. As opções **EnableSQM**, **TargetDir**e **DefaultSiteServerName** são necessárias ao usar essa opção.|  
  |/uninstall|Desinstala o console do Configuration Manager. Especifique essa opção primeiro ao usá-la com a opção **/q**.|  
  |LangPackDir|Especifica o caminho para a pasta que contém os arquivos de idioma. Você pode usar o **Downloader de Instalação** para baixar os arquivos de idioma. Se você não usar esta opção, o programa de instalação procurará a pasta de idioma na pasta atual. Se a pasta de idioma não for encontrada, o programa de instalação continuará instalando somente o idioma inglês. Para obter mais informações, consulte [Downloader de Instalação](setup-downloader.md).|  
  |TargetDir|Especifica a pasta de instalação para instalar o console do Configuration Manager. Essa opção é necessária ao usar a opção **/q** .|  
  |EnableSQM|Especifica se deve associar-se o CEIP (Programa de Aperfeiçoamento da experiência do Usuário). Use um valor de **1** para ingressar no Programa de Aperfeiçoamento da Experiência do Usuário e um valor de **0** para não ingressar no programa. Essa opção é necessária ao usar a opção **/q** .</br></br>Observação: a partir do Configuration Manager versão 1802, o recurso Programa de Aperfeiçoamento da Experiência do Usuário é removido do produto.|  
  |DefaultSiteServerName|Especifica o FQDN do servidor do site ao qual o console se conecta quando ele é aberto. Essa opção é necessária ao usar a opção **/q** .|  


  ### <a name="examples"></a>Exemplos

  -  `consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com`  

  -  `consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr Console" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com`  

  -  `consolesetup.exe /uninstall /q`  
