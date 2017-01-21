---
title: "Instalação da linha de comando | Microsoft Docs"
description: "Saiba como executar a Instalação do System Center Configuration Manager em um prompt de comando para uma variedade de instalações do site."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: a148fd1fd438efc01418c30b059874cfdfa09725

---
# <a name="use-a-command-line-to-install-system-center-configuration-manager-sites"></a>Usar a linha de comando para instalar sites do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Se desejar, execute a Instalação do System Center Configuration Manager em um prompt de comando para uma variedade de instalações do site.

 ## <a name="supported-tasks-for-command-line-installs"></a>Tarefas com suporte para instalações de linha de comando
 Esse método de executar a Instalação oferece dá suporte às seguintes tarefas de manutenção do site e de instalação:

-   **Instalar um site de administração central ou site primário por meio de uma linha de comando:**  
  Exibir [Opções de linha de comando para Instalação](../../../../core/servers/deploy/install/command-line-options-for-setup.md)

 -  **Modificar os idiomas em uso em um site de administração central ou site primário:**  
    Para modificar o idioma instalado em um site por meio de uma linha de comando (incluindo idiomas para dispositivos móveis), você deve:  

     -   Execute a Instalação de **&lt;ConfigMgrInstallationPath\>\Bin\X64** no servidor do site
     -   Usar a opção de linha de comando **/MANAGELANGS**
     -   Especificar um arquivo de script de idioma que indique os idiomas que você deseja adicionar ou remover  

    Por exemplo, use a seguinte sintaxe de comando: **setupwpf.exe /MANAGELANGS &lt;arquivo de script de idioma\>**  

    Para criar o arquivo de script de idioma, use as informações em [Opções de linha de comando para gerenciar idiomas](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang)  

 -  **Usar um arquivo de script de instalação para recuperação de site ou instalações de site autônomas:**  
    Você pode executar a instalação por meio de uma linha de comando, instruí-la a usar um script de instalação e executar uma instalação de site autônoma. Você também pode usar essa opção para recuperar um site.    

    Para usar um script com a instalação:  

    -   Execute a Instalação com a opção de linha de comando **/SCRIPT** e especifique um arquivo de script  

    -   O arquivo de script deve ser configurado com as chaves e os valores necessários  

    Para uma instalação autônoma de um site de administração central ou site primário, o arquivo de script deve ser configurado com as quatro seções a seguir:  

    -   Identificação    
    -   Opções    
    -   SQLConfigOptions    
    -   HierarchyOptions    

    -   CloudConnectorOptions  

    Para recuperar um site, você deve usar as seguintes seções do arquivo de script:  

    -   Identificação  

    -   Recuperação

     Para obter mais informações sobre backup e recuperação, consulte a seção Chaves de arquivo de script de recuperação autônoma do site no tópico Backup e recuperação no Configuration Manager.  

    Veja [Chaves do arquivo de script de Instalação autônoma](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended) para obter uma lista de chaves e valores a serem usados em um arquivo de script de instalação autônoma.  

## <a name="about-the-command-line-script-file"></a>Sobre o arquivo de script de linha de comando  

 Para instalações autônomas do Configuration Manager, é possível executar a instalação com a opção de linha de comando **/SCRIPT** e especificar um arquivo de script que contenha opções de instalação. Esse método dá suporte para as tarefas a seguir:  

-   Instalar um site de administração central  

-   Instalar um site primário  

-   Instalar um console do Configuration Manager  

-   Recuperar um site  

> [!NOTE]  
>  Você não pode usar o arquivo de script autônomo para atualizar um site de avaliação para uma instalação licenciada do Configuration Manager.  

**Para criar o script**:  
O script de instalação é automaticamente criado quando você [executa a Instalação de um site usando a interface do usuário](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  Ao confirmar as configurações na página **Resumo** do assistente:  

-   A instalação cria o script **%TEMP%\ConfigMgrAutoSave.ini**.  Você pode renomear esse arquivo antes de usá-lo, mas ele deve manter a extensão de arquivo .ini.  

-   O script de instalação autônoma contém as configurações que você selecionou no assistente.  

-   Após a criação do script, você poderá modificá-lo para instalar outros sites na sua hierarquia.  

-   Você pode usar esse script para executar uma instalação autônoma do Configuration Manager.  

Esse arquivo de script fornece as mesmas informações que o Assistente de Instalação solicita, porém, não há configurações padrão.   
Todos os valores devem ser especificados para as chaves de instalação que se aplicam ao tipo de instalação usado.  

Quando a Instalação cria o script de instalação autônoma, ele é preenchido com o valor da chave do produto inserido durante a instalação. Essa pode ser uma chave do produto (Product Key) válida ou ser igual a EVAL quando você instalar uma versão de avaliação do Configuration Manager. O valor da chave do produto no script é preenchido para habilitar a verificação de pré-requisitos para conclusão.  

Quando a Instalação inicia a instalação real do site, o script criado automaticamente é gravado para novamente limpar o valor da chave do produto no script que ela cria. Antes de usar o script para a instalação autônoma de um novo site, você pode editá-lo para fornecer uma chave do produto (Product Key) válida ou especificar uma instalação de avaliação do Configuration Manager.  

**O script contém nomes de seção, nomes de chave e valores:**  

-   Os nomes de chave da seção necessários variam de acordo com o tipo de instalação do script  

-   A ordem das chaves dentro das seções, bem como a ordem das seções dentro do arquivo, não é importante  

-   As chaves não diferenciam maiúsculas de minúsculas  

-   Ao fornecer valores para chaves, o nome da chave deve ser seguido por um de sinal de igual (=) e o valor da chave  

> [!TIP]  
>  Para exibir o conjunto completo de opções, consulte [Opções de linha de comando para instalação e scripts](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  

## <a name="to-use-the-script-setup-command-line-option"></a>Para usar a opção de linha de comando de Instalação /SCRIPT:

-   Você deve usar um arquivo de script de instalação e especificar o nome do arquivo após a opção de linha de comando de instalação **/SCRIPT** .  

    -   O nome do arquivo deve ter a extensão de nome de arquivo **.ini**  

    -   Para fazer referência ao arquivo de script da instalação no prompt de comando, você deve fornecer o caminho completo para o arquivo. Por exemplo, se o arquivo de inicialização da instalação receber o nome Setup.ini e for armazenado na pasta C:\Setup, no prompt de comando, digite:  **setup /script c:\setup\setup.ini**  

-   A conta que executa a instalação deve ter credenciais administrativas no computador. Ao executar a instalação com o script autônomo, inicie o prompt de comando usando **Run as administrator**  



<!--HONumber=Dec16_HO3-->


