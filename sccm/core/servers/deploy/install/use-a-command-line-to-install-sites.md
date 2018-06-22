---
title: Instalação em linha de comando
titleSuffix: Configuration Manager
description: Saiba como executar a Instalação do System Center Configuration Manager em um prompt de comando para uma variedade de instalações do site.
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3df559dc151950834aab4d909811cb42ec4822d0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32338934"
---
# <a name="use-a-command-line-to-install-system-center-configuration-manager-sites"></a>Usar a linha de comando para instalar sites do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Você pode executar a Instalação do System Center Configuration Manager em um prompt de comando para instalar uma variedade de tipos de site.

## <a name="supported-tasks-for-command-line-installations"></a>Tarefas com suporte para instalações de linha de comando
 Esse método de executar a Instalação oferece dá suporte às seguintes tarefas de manutenção do site e de instalação:

-   **Instalar um site de administração central ou site primário por meio de um prompt de comando**  
  Exibir [Opções de linha de comando para Instalação](../../../../core/servers/deploy/install/command-line-options-for-setup.md)

-  **Modificar os idiomas em uso em um site de administração central ou site primário**  
    Para modificar os idiomas instalados em um site por meio de um prompt de comando (incluindo idiomas para dispositivos móveis), você deve:  

     -   Executar a Instalação de **&lt;ConfigMgrInstallationPath\>\Bin\X64** no servidor do site,
     -   Usar a opção de linha de comando **/MANAGELANGS**,
     -   Especificar um arquivo de script de idioma que indique os idiomas que você deseja adicionar ou remover,  

    Por exemplo, use a seguinte sintaxe de comando: **setupwpf.exe /MANAGELANGS &lt;arquivo de script de idioma\>**  

    Para criar o arquivo de script de idioma, use as informações em [Opções de linha de comando para gerenciar idiomas](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang)  

-  **Usar um arquivo de script de instalação para recuperação de site ou instalações de site autônomas**  
    Você pode executar a Instalação de um prompt de comando usando um script de instalação e executar uma instalação de site autônoma. Você também pode usar essa opção para recuperar um site.    

    Para usar um script com a instalação:  

    -   Execute a Instalação com a opção de linha de comando **/SCRIPT** e especifique um arquivo de script.  

    -   O arquivo de script deve ser configurado com as chaves e os valores necessários.  

    Para uma instalação autônoma de um site de administração central ou site primário, o arquivo de script deve ter as seguintes seções:  

    -   Identificação    
    -   Opções    
    -   SQLConfigOptions    
      -   HierarchyOptions    
    -   CloudConnectorOptions   

    Para recuperar um site, você também deve incluir as seguintes seções do arquivo de script:  

    -   Identificação  
    -   Recuperação

Para saber mais, veja [Recuperação autônoma de sites para o Configuration Manager](/sccm/protect/understand/unattended-recovery).  

Para obter uma lista dos valores e chaves a serem usados em um arquivo de script de instalação autônoma, consulte [Chaves de arquivo de script da instalação autônoma](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended).  

## <a name="about-the-command-line-script-file"></a>Sobre o arquivo de script de linha de comando  
 Para instalações autônomas do Configuration Manager, é possível executar a instalação com a opção de linha de comando **/SCRIPT** e especificar um arquivo de script que contenha opções de instalação. As tarefas a seguir têm suporte usando esse método:  

-   Instalar um site de administração central  
-   Instalar um site primário  
-   Instalar um console do Configuration Manager  
-   Recuperar um site  

> [!NOTE]  
>  Você não pode usar o arquivo de script autônomo para atualizar um site de avaliação para uma instalação licenciada do Configuration Manager.  

### <a name="the-cdlatest-key-name"></a>O nome da chave CDLatest
Quando você usa mídia da pasta CD.Latest para executar uma instalação com scripts das quatro seguintes opções de instalação, o script deve incluir a chave **CDLatest** com um valor de **1**:
- Instalar um novo site de administração central
- Instalar um novo site primário
- Recuperar um site de administração central
- Recuperar um site primário

Esse valor não é suportado para uso com mídia de instalação que você obtém do site de Licenciamento por Volume da Microsoft.
Veja as [opções de linha de comando](/sccm/core/servers/deploy/install/command-line-options-for-setup) para obter informações sobre como usar esse nome de chave no arquivo de script.



### <a name="create-the-script"></a>Criar o script
O script de instalação é automaticamente criado quando você [executa a Instalação de um site usando a interface do usuário](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  Ao confirmar as configurações na página **Resumo** do assistente, o seguinte ocorre:  

-   A instalação cria o script **%TEMP%\ConfigMgrAutoSave.ini**.  Você pode renomear esse arquivo antes de usá-lo, mas ele deve manter a extensão de arquivo .ini.  
-   O script de instalação autônoma contém as configurações que você selecionou no assistente.  
-   Após a criação do script, você poderá modificá-lo para instalar outros sites na sua hierarquia.  
-   Você pode usar esse script para executar uma instalação autônoma do Configuration Manager.  

Esse arquivo de script fornece as mesmas informações que o Assistente de Instalação solicita, porém, não há configurações padrão.   
Você deve especificar todos os valores para as chaves de Instalação que se aplicam ao tipo de instalação que você está usando.   

Quando a Instalação cria o script de instalação autônoma, ele é preenchido com o valor da chave do produto (Product Key) inserido durante a Instalação. Essa pode ser uma chave do produto (Product Key) válida ou a **EVAL** quando você instalar uma versão de avaliação do Configuration Manager. O valor da chave do produto (Product Key) no script é populado para que a verificação de pré-requisitos possa ser concluída.   

Quando a Instalação inicia a instalação real do site, o script criado automaticamente é gravado para novamente limpar o valor da chave do produto no script que ela cria. Antes de usar o script para a instalação autônoma de um novo site, você pode editá-lo para fornecer uma chave do produto (Product Key) válida ou especificar uma instalação de avaliação do Configuration Manager.  

### <a name="section-names-key-names-and-values"></a>Nomes de seção, nomes de chave e valores
O script contém nomes de seção, nomes de chave e valores. Observe as seguintes informações:
-   Os nomes de chave da seção requeridos variam de acordo com o tipo de instalação do script.
-   A ordem das chaves dentro das seções, bem como a ordem das seções dentro do arquivo, não é importante.     
-   As chaves não diferenciam maiúsculas de minúsculas.  
-   Ao fornecer valores para chaves, o nome da chave deve ser seguido por um de sinal de igual (=) e o valor da chave.    

> [!TIP]  
>  Para exibir o conjunto completo de opções, consulte [Opções de linha de comando para instalação e scripts](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  

## <a name="use-the-script-setup-command-line-option"></a>Usar a opção de linha de comando de Instalação /SCRIPT

-   Você deve usar um arquivo de script de Instalação e especificar o nome do arquivo após a opção de linha de comando de instalação **/SCRIPT**. Observe as seguintes informações:   
    -   O nome do arquivo deve ter a extensão de nome de arquivo **.ini**.  
    -   Para fazer referência ao arquivo de script da instalação no prompt de comando, você deve fornecer o caminho completo para o arquivo. Por exemplo, se o arquivo de inicialização da instalação receber o nome Setup.ini e for armazenado na pasta C:\Setup, no prompt de comando, digite: **setup /script c:\setup\setup.ini**.  

-   A conta que executa a Instalação deve ter direitos de **Administrador** no computador. Ao executar a Instalação com o script autônomo, abra a janela Prompt de Comando usando a opção **Executar como administrador**.   
