---
title: Instalar console
titleSuffix: Configuration Manager
description: Instale o console do Configuration Manager para se conectar a um site de administração central ou um site primário.
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ebbbf62bb3cc1e2b96d83ad109064d643544fdb9
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65498243"
---
# <a name="install-the-configuration-manager-console"></a>Instalar o console do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os administradores usam o console do Configuration Manager para gerenciar o ambiente do Configuration Manager. Cada console do Configuration Manager pode se conectar a um site de administração central (CAS) ou a um site primário. Não é possível conectar um console do Configuration Manager a um site secundário.

O console do Configuration Manager é sempre instalado no servidor do site para o CAS ou um site primário. Para instalar o console separadamente da instalação do servidor do site, execute o instalador autônomo.  



## <a name="prerequisites"></a>Pré-requisitos

- Você tem direitos de **Administrador** local no computador de destino do console.  

- Você tem permissão de **Leitura** para o local dos arquivos de instalação do console do Configuration Manager.  



## <a name="source-paths"></a>Caminhos de origem

Decida qual caminho de origem será usado:  

- a pasta ConsoleSetup no servidor do site: `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    Ao instalar um servidor do site, ele copia os arquivos de instalação do console e os pacotes de idioma compatíveis do site na subpasta **Tools\ConsoleSetup**. Opcionalmente, você pode copiar a pasta **ConsoleSetup** para um local alternativo para iniciar a instalação. Quando você atualiza o site, ele sempre mantém sua versão local atualizada.  

- Mídia de instalação do Configuration Manager: `<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    A instalação do console do Configuration Manager por meio da mídia de instalação sempre instala a versão em inglês. Esse comportamento ocorre mesmo se o servidor do site der suporte a idiomas diferentes, ou se o sistema operacional do computador de destino for definido com outro idioma.  

Quando possível, inicie o instalador do console a partir de **ConsoleSetup** pasta em vez da mídia de origem.

> [!Important]  
> Não instale o console usando os arquivos de origem de **CD.Latest**. Este é um cenário sem suporte e pode causar problemas na instalação do console. Para obter mais informações, veja [A pasta CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder#unsupported-scenarios).<!-- SCCMDocs issue 1359 -->  

Se você criar um pacote para a instalação do console em outros computadores, verifique se que o pacote inclui os seguintes arquivos:<!--3612513-->

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab (começando na versão 1902)
- ConfigMgr.AC_Extension.amd64.cab (começando na versão 1902)



## <a name="use-the-setup-wizard"></a>Usar o Assistente de Instalação  

1. Navegue até o caminho de origem e abra **ConsoleSetup.exe**.  

    > [!IMPORTANT]  
    > Sempre instale o console usando **ConsoleSetup.exe**. Embora seja possível instalar o console do Configuration Manager executando adminconsole.msi, esse método não executa os pré-requisitos nem as verificações de dependência. A instalação pode não ser instalada corretamente.  

2. No assistente, selecione **Avançar**.  

3. Na página **Servidor do Site**, insira o FQDN (nome de domínio totalmente qualificado) do servidor do site ao qual o console do Configuration Manager se conecta.  

4. Na página **Pasta de Instalação**, insira a pasta de instalação para o console do Configuration Manager. O caminho da pasta não pode incluir espaços à direita ou caracteres Unicode.  

5. Na página **Programa de Aperfeiçoamento da Experiência do Usuário**, selecione se deseja ingressar no programa.  

    > [!Note]  
    > A partir do Configuration Manager versão 1802, o recurso Programa de Aperfeiçoamento da Experiência do Usuário é removido do produto.

6. Na página **Pronto para Instalar**, clique em **Instalar**.  



## <a name="install-from-a-command-prompt"></a>Instalar a partir de um prompt de comando  

> [!TIP]  
> A instalação do console do Configuration Manager por meio de um prompt de comando sempre instala a versão em inglês. Esse comportamento ocorre mesmo se o sistema operacional do computador de destino for definido com outro idioma. Para instalar o console do Configuration Manager em um idioma diferente do inglês, [use o Assistente de Instalação](#use-the-setup-wizard).  


### <a name="consolesetupexe-command-line-options"></a>Opções de linha de comando de ConsoleSetup.exe

#### <a name="q"></a>/q

Instala o console do Configuration Manager autônomo. As opções **EnableSQM**, **TargetDir**e **DefaultSiteServerName** são necessárias ao usar essa opção.

#### <a name="uninstall"></a>/uninstall

Desinstala o console do Configuration Manager. Especifique essa opção primeiro ao usá-la com a opção **/q**.

#### <a name="langpackdir"></a>LangPackDir

Especifica o caminho para a pasta que contém os arquivos de idioma. Você pode usar o **Downloader de Instalação** para baixar os arquivos de idioma. Se você não usar essa opção, o programa de instalação procurará a pasta de idioma na pasta atual. Se a pasta de idioma não for encontrada, o programa de instalação continuará instalando somente o idioma inglês. Para obter mais informações, consulte [Downloader de Instalação](setup-downloader.md).

#### <a name="targetdir"></a>TargetDir

Especifica a pasta de instalação para instalar o console do Configuration Manager. Essa opção é necessária ao usar a opção **/q** .

#### <a name="enablesqm"></a>EnableSQM

Especifica se deve associar-se o CEIP (Programa de Aperfeiçoamento da experiência do Usuário). Use um valor de **1** para ingressar no Programa de Aperfeiçoamento da Experiência do Usuário e um valor de **0** para não ingressar no programa. Essa opção é necessária ao usar a opção **/q** .

> [!Important]  
> A partir do Configuration Manager versão 1802, o recurso Programa de Aperfeiçoamento da Experiência do Usuário é removido do produto. Usar o parâmetro causará falha na instalação.

#### <a name="defaultsiteservername"></a>DefaultSiteServerName

Especifica o FQDN do servidor do site ao qual o console se conecta quando ele é aberto. Essa opção é necessária ao usar a opção **/q** .


### <a name="examples"></a>Exemplos

> [!Important]  
> Na versão 1802 e mais recentes, NÃO inclua o parâmetro **EnableSQM**

#### <a name="silent-install"></a>Instalação silenciosa

`ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

#### <a name="silent-install-with-language-packs"></a>Instalação silenciosa com pacotes de idiomas

`ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com LangPackDir=C:\Downloads\ConfigMgr`  

#### <a name="silent-uninstall"></a>Desinstalação silenciosa

`ConsoleSetup.exe /uninstall /q`  



## <a name="see-also"></a>Consulte também

Um administrador vê os objetos no console com base nas permissões atribuídas à sua conta de usuário. Para obter mais informações, consulte [Fundamentos da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).

Para ver mais informações sobre os conceitos básicos de navegação no console do Configuration Manager, confira [Usando o console](/sccm/core/servers/manage/admin-console).
