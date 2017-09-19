---
title: "Criar condições globais | Microsoft Docs"
description: "Crie condições globais para especificar como um aplicativo é fornecido e implantado em dispositivos cliente."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d5f871a-19dc-4bd3-a3ad-4230c7a69f1b
caps.latest.revision: "7"
caps.handback.revision: "0"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 6aedab4ab23749061ec103e0de92edafdad13d33
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2017
---
# <a name="how-to-create-global-conditions-in-system-center-configuration-manager"></a>Como criar condições globais no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

No System Center Configuration Manager, as condições globais são as regras que representam condições técnicas ou de negócios que você pode usar para especificar como um aplicativo é fornecido e implantado nos dispositivos de clientes. As condições globais são acessadas na página **Requisitos** do Assistente para Criar Tipo de Implantação.  

> [!NOTE]  
>  Você pode editar condições globais somente do site em que elas foram criadas.  

 Use os procedimentos a seguir para criar condições globais do Configuration Manager.  

## <a name="provide-basic-information-about-the-global-condition"></a>Fornecer informações básicas sobre a condição global  
 Vários tipos diferentes de condições globais estão disponíveis. Opções diferentes estão associadas aos tipos diferentes de condição global. Quando você seleciona um tipo de condição global específico, o Configuration Manager mostra as opções que se aplicam à sua seleção.  

1.  No console do Configuration Manager, escolha **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Condições Globais**.  

3.  Na guia **Início**, no grupo **Criar**, escolha **Criar Condição Global**.  

4.  Na caixa de diálogo **Criar Condição Global** , forneça um nome e uma descrição opcional para a condição global.  

5.  Na lista suspensa **Tipo de dispositivo**, escolha se a condição global destina-se a um computador **Windows** ou um dispositivo **Windows Mobile**.  

6.  Na lista suspensa **Tipo de Condição** , escolha uma das seguintes opções:  

    -   **Configuração** – Esta opção verifica a existência de um ou mais itens nos dispositivos cliente. Por exemplo, você pode verificar se um arquivo, pasta ou valor de chave do Registro existe em um dispositivo cliente.  

    -   **Expressão** – Esta opção permite configurar regras mais complexas para verificar se a condição é atendida nos dispositivos cliente. Por exemplo, você pode verificar se a memória física em um computador está entre 2 GB e 4 GB ou se um dispositivo móvel usa entrada por tela sensível ao toque.  

## <a name="set-up-rules-for-the-global-condition"></a>Configurar regras para a condição global  
 O procedimento para definir as regras da condição global é diferente dependendo se você está definindo uma configuração ou uma expressão. Use o procedimento aplicável aqui para configurar uma configuração ou uma expressão para a condição global.  

### <a name="to-set-up-a-setting-for-the-global-condition"></a>Para configurar a condição global  

1.  Na lista suspensa **Tipo de Condição** , escolha **Configuração**.  

2.  Na lista suspensa **Tipo de configuração** , escolha o item a ser usado como condição para os quais os requisitos serão verificados. Os seguintes tipos de configuração e definição estão disponíveis.  

    -   **Consulta ao Active Directory**  

        -   **Prefixo LDAP** - Especifique um prefixo LDAP válido para a consulta aos Serviços de Domínio Active Directory para avaliar a conformidade nos computadores cliente. Você pode usar **LDAP://** ou **GC://**.  

        -   **DN (nome diferenciado)** – Especifique o nome diferenciado do objeto do Active Directory Domain Services que será avaliado quanto à conformidade nos computadores cliente.  

        -   **Filtro de pesquisa** - Especifique um filtro LDAP opcional para refinar os resultados da consulta aos Serviços de Domínio Active Directory para avaliar a conformidade nos computadores cliente.  

        -   **Escopo de pesquisa** - Especifique o escopo de pesquisa nos Serviços de Domínio Active Directory:  

            -   **Base** – Consulta apenas o objeto especificado.  

            -   **Um Nível** – Esta opção não é usada nesta versão do Configuration Manager.  

            -   **Subárvore** – Consulta o objeto especificado e sua subárvore completa no diretório.  

        -   **Propriedade** - Especifica a propriedade do objeto de Serviços de Domínio Active Directory que serão usados para avaliar a conformidade nos computadores cliente.  

        -   **Consulta** – Mostra a consulta LDAP que foi construída com base nas entradas no **Prefixo LDAP**, **DN (nome diferenciado)**, **Filtro de Pesquisa**, se especificado, e **Propriedade**. Essa consulta será usada para avaliar a conformidade em computadores cliente.  

    -   **Assembly**  

        -   **Nome do assembly** - Especifica o nome do objeto de assembly a ser pesquisado. O nome não pode ser o mesmo de outro objeto de assembly do mesmo tipo e deve ser registrado no Cache de Assembly Global. O nome do assembly pode ter um máximo de 256 caracteres.  

        > [!NOTE]  
        >  Um assembly é um trecho de código que pode ser compartilhado entre aplicativos. Os assemblies podem ter a extensão de nome de arquivo .dll ou .exe. O Cache de assembly global é uma pasta chamada *%systemroot%\assembly* em computadores cliente em que todos os assemblies compartilhados são armazenados.  

    -   **Sistema de arquivos**  

        -   **Tipo** – Na lista suspensa, escolha se você deseja pesquisar um **Arquivo** ou uma **Pasta**.  

        -   **Caminho** - Especifique os caminho para o arquivo ou a pasta especificada em computadores cliente. Você pode especificar variáveis de ambiente do sistema e a variável de ambiente *%USERPROFILE%* no caminho.  

            > [!NOTE]  
            >  Se você usar a variável de ambiente *%USERPROFILE%* nos campos **Caminho** ou **Nome do arquivo ou pasta** , todos os perfis de usuário no computador cliente serão pesquisados. Isso pode resultar na detecção de várias instâncias do arquivo ou pasta.  

        -   **Nome do arquivo ou pasta** - Especifique o nome do objeto do arquivo ou pasta que será pesquisado. Você pode especificar variáveis de ambiente do sistema e a variável de ambiente *%USERPROFILE%* no nome do arquivo ou da pasta. Você também pode usar os caracteres curinga * e ? no nome do arquivo.  

            > [!NOTE]  
            >  Se você especificar um nome de arquivo ou pasta e usar caracteres curinga, isso poderá gerar um alto número de resultados. Isso pode resultar em um alto uso de recursos no computador cliente e um alto tráfego de rede ao relatar os resultados para o Configuration Manager.  

        -   **Incluir subpastas** – Habilite esta opção se também desejar pesquisar quaisquer subpastas no caminho especificado.  

        -   **Este arquivo ou pasta está associado a um aplicativo de 64 bits** ‑ Escolha se o local do arquivo do sistema de 64 bits (*%windir%*\system32) deve ser pesquisado além do local do arquivo do sistema de 32 bits (*%windir%*\syswow64) em clientes do Configuration Manager que executam uma versão de 64 bits do Windows.  

            > [!NOTE]  
            >  Se o mesmo arquivo ou pasta existir nos dois locais do arquivo do sistema de 64 e de 32 bits no mesmo computador de 64 bits, vários arquivos serão detectados pela condição global.  

         O tipo de configuração **Sistema de arquivos** não dá suporte para especificar um caminho UNC para um compartilhamento de rede no campo **Caminho** .  

    -   **Metabase do IIS**  

        -   **Caminho da metabase** - Especifique um caminho válido para a Metabase do IIS.  

        -   **ID da Propriedade** - Especifique a propriedade numérica da configuração da Metabase do IIS.  

    -   **Chave do Registro**  

        -   **Hive** – Na lista suspensa, escolha o hive de Registro no qual deseja pesquisar.  

        -   **Chave** - Especifique o nome da chave do Registro que deseja pesquisar. O formato usado deve ser *key\subkey*.  

        -   **A chave do Registro está associada ao aplicativo de 64 bits** - Especifica se as chaves do Registro de 64 bits devem ser pesquisadas além das chaves do Registro de 32 bits em clientes que executam uma versão de 64 bits do Windows.  

            > [!NOTE]  
            >  Se a mesma chave do Registro existir nos dois locais do Registro, de 64 e de 32 bits, no mesmo computador de 64 bits, várias chaves do Registro serão detectadas pela condição global.  

    -   **Valor do Registro**  

        -   **Hive** - Na lista suspensa, selecione o hive de Registro que deseja pesquisar.  

        -   **Chave** - Especifique o nome da chave do Registro que deseja pesquisar. O formato usado deve ser *key\subkey*.  

        -   **Valor** – Especifique o valor que deve estar contido na chave do Registro especificado.  

        -   **A chave do Registro está associada ao aplicativo de 64 bits** - Especifica se as chaves do Registro de 64 bits devem ser pesquisadas além das chaves do Registro de 32 bits em clientes que executam uma versão de 64 bits do Windows.  

            > [!NOTE]  
            >  Se a mesma chave do Registro existir nos dois locais do Registro, de 64 e de 32 bits, no mesmo computador de 64 bits, várias chaves do Registro serão detectadas pela condição global.  

    -   **script**  

        -   **Script de descoberta** – Escolha **Adicionar** para digitar ou procure o script a ser usado. Você pode usar scripts do Windows PowerShell, VBScript ou JScript.  

        -   **Executar scripts usando as credenciais do usuário conectado** – Se você habilitar esta opção, o script será executado em computadores cliente usando as credenciais do usuário conectado.  

            > [!NOTE]  
            >  O valor retornado pelo script será usado para avaliar a conformidade da condição global. Por exemplo, quando você usa VBScript, pode usar o comando **WScript.Echo Result** para retornar o valor da variável Result para a condição global.  
            >   
            >  Se seu script retornar vários valores, eles deverão ser dispostos em uma única linha, separados por ponto e vírgula. Se cada valor estiver em uma linha separada, a avaliação falhará.  

    -   **Consulta SQL**  

        -   **Instância do SQL Server** – Escolha se deseja que a consulta SQL seja executada na instância padrão, em todas as instâncias ou em um determinado nome da instância do banco de dados.  

            > [!NOTE]  
            >  O nome da instância deve se referir a uma instância local do SQL Server. Para se referir a uma instância de servidor em cluster do SQL, você deve usar uma configuração de script.  

        -   **Banco de Dados** - Especifique o nome do banco de dados do Microsoft SQL Server para o qual a consulta SQL será executada.  

        -   **Coluna** - Especifique o nome da coluna retornada pela declaração Transact-SQL a ser usada para avaliar a conformidade da condição global.  

        -   **Declaração Transact-SQL** – Especifique a consulta SQL completa para a condição global. Você também pode escolher **Abrir** para abrir uma consulta SQL existente.  

    -   **Consulta WQL**  

        -   **Namespace** - Especifica o namespace WMI que será usado para criar uma consulta WQL que será avaliada quanto à conformidade em computadores cliente. O valor padrão é Root\cimv2.  

        -   **Classe** - Especifica a classe WMI que será usada para criar uma consulta WQL que será avaliada quanto à conformidade em computadores cliente.  

        -   **Propriedade** - Especifica a propriedade WMI que será usada para criar uma consulta WQL que será avaliada quanto à conformidade em computadores cliente.  

        -   **Cláusula WHERE da consulta WQL** - Você pode usar o item **Cláusula WHERE da consulta WQL** para especificar uma cláusula WHERE a ser aplicada ao namespace, à classe e à propriedade especificados em computadores cliente.  

    -   **Consulta XPath**  

        -   **Caminho** – Especifique o caminho para o arquivo XML nos computadores cliente que serão usados para avaliar a conformidade. O Configuration Manager dá suporte ao uso de todas as variáveis de ambiente do sistema Windows e à variável de usuário *%USERPROFILE%* no nome do caminho.  

        -   **Nome do arquivo XML** – Especifique o nome do arquivo que contém a consulta XML a ser usada para avaliar a conformidade em computadores cliente.  

        -   **Incluir subpastas** - Habilite esta opção se também desejar pesquisar quaisquer subpastas no caminho especificado.  

        -   **Este arquivo está associado a um aplicativo de 64 bits** ‑ Escolha se o local do arquivo do sistema de 64 bits (*%windir%*\system32) deve ser pesquisado além do local do arquivo do sistema de 32 bits (*%windir%*\syswow64) em clientes do Configuration Manager que executam uma versão de 64 bits do Windows.  

        -   **Consulta XPath** - Especifique uma consulta XPath (XML path language) válida completa a ser usada para avaliar a conformidade em computadores cliente.  

        -   **Namespaces** - Abre a caixa de diálogo **XML Namespaces** para identificar namespaces e prefixos a serem usados durante a consulta XPath.  

3.  Na lista suspensa **Tipo de dados** , escolha o formato no qual os dados serão retornados pela condição antes de ser usada para verificar os requisitos.  

    > [!NOTE]  
    >  A lista suspensa **Tipo de dados** não é mostrada para todos os tipos de configuração.  

4.  Configure mais detalhes sobre essa configuração abaixo da lista suspensa **Tipo de configuração**. Os itens que você pode configurar variarão dependendo do tipo de configuração que você selecionou.  

5.  Escolha **OK** para salvar a regra e fechar a caixa de diálogo **Criar Condição Global**.  

### <a name="set-up-an-expression-for-the-global-condition"></a>Configurar uma expressão para a condição global  

1.  Na lista suspensa **Tipo de Condição** , escolha **Expressão**.  

2.  Escolha **Adicionar Cláusula** para abrir a caixa de diálogo **Adicionar Cláusula**.  

3.  Na lista suspensa **Selecionar categoria** , selecione se esta expressão é para um dispositivo ou um usuário. Como alternativa, selecione **Personalizado** para usar uma condição global previamente configurada.  

4.  Na lista suspensa **Selecionar uma condição** , selecione a condição a ser usada para avaliar se o usuário ou o dispositivo atende aos requisitos da regra. O conteúdo desta lista varia dependendo da categoria selecionada.  

5.  Na lista suspensa **Escolher operador** , escolha o operador que será usado para comparar a condição selecionada ao valor especificado para avaliar se o usuário ou o dispositivo atende aos requisitos da regra. Os operadores disponíveis variam dependendo da condição selecionada.  

6.  No campo **Valor** , especifique os valores que serão usados com a condição selecionada e o operado para avaliar se o usuário ou o dispositivo atende aos requisitos da regra. Os valores disponíveis irão variar dependendo da condição selecionada e do operador selecionado.  

7.  Escolha **OK** para salvar a expressão e fechar a caixa de diálogo **Adicionar Cláusula**.  

8.  Quando terminar de adicionar cláusulas à condição global, escolha **OK** para fechar a caixa de diálogo **Criar Condição Global** e salvar a condição global.  
