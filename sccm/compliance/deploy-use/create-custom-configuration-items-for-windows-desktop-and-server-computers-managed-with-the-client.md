---
title: Criar itens de configuração personalizada
titleSuffix: Configuration Manager
description: Gerenciar configurações para computadores e servidores Windows com um item personalizado de configuração para desktops e servidores Windows
ms.date: 03/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4253fdd94985a8a9adbc9e782f8397c2f76f5f2c
ms.sourcegitcommit: 4ab85212268e76d3fd22f00e6c74edaa5abde60c
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57426882"
---
# <a name="create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>Criar itens de configuração personalizados para desktops e servidores Windows gerenciados com o cliente do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Use o item de configuração **Servidores e Desktops Windows personalizados** do Configuration Manager para gerenciar as configurações de computadores e servidores Windows e que são gerenciados pelo cliente do Configuration Manager.  



## <a name="start-the-wizard"></a>Iniciar o Assistente

1. No console do Configuration Manager, vá para o workspace **Ativos e Conformidade**, expanda **Configurações de Conformidade** e selecione o nó **Itens de Configuração**.  

2. Na guia **Início** da faixa de opções, no grupo **Criar**, selecione **Criar Item de Configuração**.  

3. Na página **Geral** do **Assistente para Criar Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  

4. Em **Especificar o tipo de item de configuração que deseja criar**, selecione **Windows Desktops e Servers (personalizado)**.  

    > [!TIP]  
    > Se quiser fornecer configurações do método de detecção que verifica a existência de um aplicativo, selecione **Este arquivo de configuração contém as configurações do aplicativo**.  

5. Para ajudar você a pesquisar e filtrar itens de configuração no console do Configuration Manager, selecione **Categorias** para criar e atribuir categorias.  



## <a name="detection-methods"></a>Métodos de detecção  

Use este procedimento para fornecer informações sobre o método de detecção para o item de configuração.  

> [!NOTE]  
> Essas informações se aplicam somente se você selecionou **Este item de configuração contém as configurações do aplicativo** na página **Geral** do assistente.  

Um método de detecção no Configuration Manager contém regras que são usadas para detectar se um aplicativo é instalado em um computador. Essa detecção ocorre antes que o cliente avalia a conformidade para o item de configuração. Para detectar se um aplicativo estiver instalado, você pode detectar a presença de um arquivo do Windows Installer para o aplicativo, use um script personalizado, ou selecione **sempre assumir o aplicativo é instalado** para avaliar o item de configuração para fins de conformidade, independentemente se o aplicativo está instalado.  


### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>Para detectar a instalação de um aplicativo usando o arquivo do Windows Installer  

1. Na página **Métodos de Detecção** do **Assistente para Criar Item de Configuração**, selecione a opção **Usar detecção do Windows Installer**.  

2. Selecione **Abrir**, navegue até o arquivo do Windows Installer (.msi) que você deseja detectar e, em seguida, selecione **Abrir**.  

3. O **versão** campo é preenchido automaticamente com o número de versão do arquivo do Windows Installer. Se o valor exibido está incorreto, insira o número da nova versão aqui.  

4. Se quiser detectar o perfil de cada usuário no computador, selecione **Este aplicativo está instalado para um ou mais usuários**.  


### <a name="to-detect-a-specific-application-and-deployment-type"></a>Para detectar um tipo específico de aplicativo e implantação  

1. Na página **Métodos de Detecção** do **Assistente para Criar Item de Configuração**, selecione **Detectar um tipo de implantação e de aplicativo específico**. Escolha **Selecionar**.   

2. Na caixa de diálogo **Especificar Aplicativo** , selecione o aplicativo e um tipo de implantação associado que deseja detectar.  


### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>Para detectar a instalação de um aplicativo usando um script personalizado  

1. Na página **Métodos de Detecção** do **Assistente para Criar Item de Configuração**, selecione a opção **Usar um script personalizado para detectar este aplicativo**.  

2. Na lista, selecione o idioma do script. Escolha entre os seguintes formatos:  

    - **VBScript**  

    - **JScript**  

    - **PowerShell**  

        > [!Note]  
        > Começando na versão 1810, quando um script do Windows PowerShell é executado como um método de detecção, o cliente do Configuration Manager chama PowerShell com o `-NoProfile` parâmetro. Essa opção inicia o PowerShell sem perfis. Um perfil do PowerShell é um script executado quando o PowerShell é iniciado. <!--3607762-->  

3. Selecione **Abrir**, navegue até o script que deseja usar e selecione **Abrir**.  



##  <a name="specify-supported-platforms"></a>Especificar as plataformas com suporte  

Na página **Plataformas com Suporte** do **Assistente para Criar Item de Configuração**, selecione as versões do Windows nas quais você deseja que o item de configuração seja avaliado quanto à conformidade, ou selecione **Selecionar tudo**. 

Você também pode **especificar a versão do Windows manualmente**. Selecione **adicionar** e especifique o número de build de cada parte do Windows. 



##  <a name="configure-settings"></a>Definir configurações  

Use este procedimento para definir as configurações no item de configuração.  

Configurações representam as condições comerciais ou técnicas que são usadas para avaliar a conformidade em dispositivos cliente. Você pode definir uma nova configuração ou navegar até uma configuração existente em um computador de referência.  

1. Na página **Configurações** do **Assistente para Criar Item de Configuração**, selecione **Novo**.  

2. Sobre o **geral** guia do **Criar configuração** diálogo caixa, forneça as seguintes informações:  

    - **Nome**: insira um nome exclusivo para a configuração. Você pode usar no máximo 256 caracteres.  

    - **Descrição**: insira uma descrição para a configuração. Você pode usar no máximo 256 caracteres.  

    - **Tipo de configuração:** na lista, escolha e configure um dos seguintes tipos de configuração a ser usado para esta configuração:  
        - [Consulta ao Active Directory](#bkmk_adquery)
        - [Assembly](#bkmk_assembly)
        - [Sistema de arquivos](#bkmk_file)
        - [Metabase do IIS](#bkmk_iis)
        - [Chave do Registro](#bkmk_regkey)
        - [Valor do Registro](#bkmk_regval)
        - [script](#bkmk_script)
        - [Consulta SQL](#bkmk_sql)
        - [Consulta WQL](#bkmk_wql)
        - [Consulta XPath](#bkmk_xpath)

    - **Tipo de Dados**: escolha o formato no qual a condição retorna os dados antes que sejam usados para avaliar a configuração. A lista **Tipo de dados** não é exibida para todos os tipos de configuração.  

        > [!Tip]  
        > O tipo de dados **Ponto flutuante** dá suporte apenas a três dígitos após o ponto decimal.  

3. Configurar detalhes adicionais sobre essa configuração sob o **Definindo tipo** lista. Os itens que você pode configurar variam, dependendo do tipo de configuração que você selecionou.  

4. Selecione **OK** para salvar a configuração e fechar a caixa de diálogo **Criar Configuração**.  


### <a name="bkmk_adquery"></a> Consulta do Active Directory

- **Prefixo LDAP**: especifique um prefixo válido para a consulta dos Active Directory Domain Services para avaliar a conformidade nos computadores cliente. Para fazer uma pesquisa de catálogo global, use `LDAP://` ou `GC://`.  

- **DN (nome distinto)**: especifique o nome distinto do objeto Active Directory Domain Services que é avaliado quanto à conformidade nos computadores cliente.  

- **Filtro de pesquisa**: especifique um filtro LDAP opcional para refinar os resultados da consulta ao Active Directory Domain Services para avaliar a conformidade nos computadores cliente. Para retornar todos os resultados da consulta, digite `(objectclass=*)`.  

- **Escopo de pesquisa**: especifique o escopo de pesquisa no Active Directory Domain Services  

    - **Base**: consulta apenas o objeto especificado  

    - **Um Nível**: esta opção não é usada nesta versão do Configuration Manager  

    - **Subárvore**: consulta o objeto especificado e sua subárvore completa no diretório  

- **Propriedade**: especifique a propriedade do objeto Active Directory Domain Services que é usada para avaliar a conformidade em computadores cliente.  

    Por exemplo, se quiser consultar a propriedade do Active Directory, que armazena o número de vezes que um usuário digita uma senha incorretamente, insira `badPwdCount` neste campo.  

- **Consulta**: exibe a consulta construída a com base nas entradas no **prefixo LDAP**, **DN (Nome distinto)**, **Filtro de Pesquisa** (se for especificado) e **Propriedade**.  


### <a name="bkmk_assembly"></a> Assembly

Um assembly é um trecho de código que pode ser compartilhado entre aplicativos. Módulos (assemblies) podem ter a extensão de nome de arquivo. dll ou .exe. O cache de assembly global é a pasta `%SystemRoot%\Assembly` em computadores cliente. Esse cache é onde o Windows armazena todos os assemblies compartilhados.  

- **Nome do assembly:** Especifica o nome do objeto de assembly que você deseja pesquisar. O nome não pode ser o mesmo que outros objetos de assembly do mesmo tipo. Primeiro, registrá-lo no cache de assembly global. O nome do assembly pode ter até 256 caracteres.  


### <a name="bkmk_file"></a> Sistema de arquivos

- **Tipo**: na lista, selecione se deseja pesquisar um **Arquivo** ou uma **Pasta**.  

- **Caminho**: especifique o caminho da pasta ou arquivo especificado nos computadores cliente. Você pode especificar variáveis de ambiente do sistema e a variável de ambiente `%USERPROFILE%` no caminho.  

    > [!NOTE]  
    > Se você usar o `%USERPROFILE%` variável de ambiente na **caminho** ou **nome do arquivo ou pasta** caixas, o cliente do Configuration Manager procura todos os perfis de usuário no computador cliente. Esse comportamento pode resultar em que ele encontrar várias instâncias do arquivo ou pasta.  
    >   
    > Se as configurações de conformidade não tiverem acesso ao caminho especificado, será gerado um erro de descoberta. Além disso, se o arquivo que você está procurando está em uso, é gerado um erro de detecção.  

    > [!Tip]  
    > Selecione **procurar** para definir a configuração de valores em um computador de referência.   

- **Nome de arquivo ou pasta**: especifique o nome do objeto de arquivo ou pasta para pesquisar. Você pode especificar variáveis de ambiente do sistema e a variável de ambiente `%USERPROFILE%` no nome do arquivo ou da pasta. Você também pode usar os caracteres curinga `*` e `?` no nome de arquivo.  

    > [!NOTE]  
    > Se você especificar um nome de arquivo ou pasta e usar caracteres curinga, essa combinação poderá gerar muitos resultados. Também poderia resultar na alta utilização de recursos no computador cliente e muito tráfego de rede ao relatar os resultados para o Configuration Manager.  

- **Incluir subpastas**: também pesquisar quaisquer subpastas no caminho especificado.  

- **Este arquivo ou pasta está associada com um aplicativo de 64 bits**: se habilitada, somente pesquisar locais de arquivo de 64 bits, como `%ProgramFiles%` em computadores de 64 bits. Se essa opção não estiver habilitada, pesquise os locais de 64 bits e 32 bits locais como `%ProgramFiles(x86)%`.  

    > [!NOTE]  
    > Se o mesmo arquivo ou pasta existir nos dois locais do arquivo do sistema de 64 e de 32 bits no mesmo computador de 64 bits, vários arquivos serão detectados pela condição global.  

    O tipo de configuração **Sistema de arquivos** não dá suporte à especificação de um caminho UNC para um compartilhamento de rede na caixa **Caminho**.  


### <a name="bkmk_iis"></a> Metabase do IIS

- **Caminho de metabase**: especifique um caminho válido para a metabase do IIS (Serviços de Informações da Internet). Por exemplo, `/LM/W3SVC/`.  

- **ID da Propriedade**: especifique a propriedade numérica da configuração de metabase do IIS.  


### <a name="bkmk_regkey"></a> Chave do Registro

- **Hive**: selecione o hive do registro que você deseja pesquisar

    > [!Tip]  
    > Selecione **procurar** para definir a configuração de valores em um computador de referência. Para procurar uma chave do registro em um computador remoto, habilitar o **registro remoto** serviço no computador remoto.  

- **Chave**: especifique o nome da chave do Registro que você deseja pesquisar. Use o formato `key\subkey`.  

- **Essa chave do registro está associada um aplicativo de 64 bits**: pesquise chaves do Registro de 64 bits, além das chaves do Registro de 32 bits, em clientes que executam uma versão de 64 bits do Windows.  

    > [!NOTE]  
    > Se a mesma chave do Registro existir nos dois locais do Registro, de 64 e de 32 bits, no mesmo computador de 64 bits, ambas as chaves do Registro serão detectadas pela condição global.  


### <a name="bkmk_regval"></a> Valor do Registro

- **Hive**: selecione o hive do registro para pesquisar.  

    > [!Tip]  
    > Selecione **procurar** para definir a configuração de valores em um computador de referência. Para procurar um valor de registro em um computador remoto, habilitar o **registro remoto** serviço no computador remoto. Você também precisa de permissões de administrador para acessar o computador remoto.  

- **Chave**: especifique o nome da chave do registro a ser pesquisado. Use o formato `key\subkey`.  

- **Valor**: especifique o valor que deve estar contido na chave do Registro especificado.  

- **Essa chave do registro está associada um aplicativo de 64 bits**: pesquise as chaves do Registro de 64 bits, além das chaves do Registro de 32 bits, em clientes que executam uma versão de 64 bits do Windows.  

    > [!NOTE]  
    > Se a mesma chave do Registro existir nos dois locais do Registro, de 64 e de 32 bits, no mesmo computador de 64 bits, ambas as chaves do Registro serão detectadas pela condição global.  


### <a name="bkmk_script"></a> Script

O valor retornado pelo script será usado para avaliar a conformidade da condição global. Por exemplo, ao usar o VBScript, você poderá usar o comando **WScript.Echo Result** para retornar o valor da variável *Result* para a condição global.  

- **Script de descoberta**: selecione **Adicionar Script**e insira ou navegue até um script. Esse script é usado para localizar o valor. Você pode usar scripts do Windows PowerShell, VBScript ou Microsoft JScript.  

- **Script de correção (opcional)**: selecione **Adicionar Script**e insira ou navegue até um script. Esse script é usado para corrigir os valores de configuração fora de conformidade. Você pode usar scripts do Windows PowerShell, VBScript ou Microsoft JScript.  

- **Executar scripts usando as credenciais do usuário conectado**: se você habilitar esta opção, o script será executado em computadores cliente que usam as credenciais do usuário conectado.  

> [!Note]  
> Começando na versão 1810, quando você usa o Windows PowerShell como um script de descoberta ou a correção, o cliente do Configuration Manager chama PowerShell com o `-NoProfile` parâmetro. Essa opção inicia o PowerShell sem perfis. Um perfil do PowerShell é um script executado quando o PowerShell é iniciado. <!--3607762-->  


### <a name="bkmk_sql"></a> Consulta SQL

- **Instância do SQL Server**: escolha se deseja que a consulta SQL seja executada na instância padrão, em todas as instâncias ou em um determinado nome da instância do banco de dados.  

    > [!NOTE]  
    > O nome da instância deve se referir a uma instância local do SQL Server. Para se referir a uma instância de servidor em cluster do SQL, você deve usar uma configuração de script.  

- **Banco de dados**: especifique o nome do banco de dados Microsoft SQL Server no qual você deseja executar a consulta SQL.  

- **Coluna**: especifique o nome da coluna retornado pela instrução Transact-SQL que é usada para avaliar a conformidade da condição global.  

- **Instrução Transact-SQL**: especifique a consulta SQL completa que deseja usar para a condição global. Para usar uma consulta SQL existente, selecione **aberto**.  

    > [!IMPORTANT]  
    > As configurações da consulta SQL não dão suporte a comandos SQL que modificam o banco de dados. Só é possível usar comandos SQL que leem as informações do banco de dados.  


### <a name="bkmk_wql"></a> Consulta WQL

- **Namespace**: especifique o namespace WMI que é avaliada quanto à conformidade nos computadores cliente. O valor padrão é `root\cimv2`.  

- **Classe**: especificar o destino de classe do WMI no namespace acima.  

- **Propriedade**: especifique a propriedade WMI de destino na classe acima.  

- **Cláusula WHERE da consulta WQL**: Especifique uma cláusula de qualificação para reduzir os resultados. Por exemplo, para consultar apenas o serviço DHCP na classe Win32_Service, a cláusula WHERE pode ser `Name = 'DHCP' and StartMode = 'Auto'`.   


### <a name="bkmk_xpath"></a> Consulta XPath

- **Caminho**: especifique o caminho para o arquivo .xml nos computadores cliente, que será usado para avaliar a conformidade. O Configuration Manager dá suporte ao uso de todas as variáveis de ambiente do sistema Windows e à variável de usuário `%USERPROFILE%` no nome do caminho.  

- **Nome do arquivo XML**: especifique o nome do arquivo que contém a consulta XML no caminho acima.  

- **Incluir subpastas**: habilite esta opção para pesquisar quaisquer subpastas no caminho especificado.  

- **Esse arquivo está associado um aplicativo de 64 bits**: procure o local do arquivo de sistema de 64 bits `%Windir%\System32` além do local de arquivo do sistema de 32 bits `%Windir%\Syswow64` em clientes do Configuration Manager que estão executando uma versão de 64 bits do Windows.  

- **Consulta XPath**: Especifique uma completa XML caminho language (XPath) consulta válida.  

- **Namespaces**: identificar namespaces e prefixos a ser usado durante a consulta XPath.  

Se você tentar descobrir um arquivo .XML criptografado, as configurações de conformidade encontrarão o arquivo, mas a consulta XPath não produzirá nenhum resultado. O cliente do Configuration Manager não gera um erro.  

Se a consulta XPath não for válida, a configuração será avaliada como não compatível nos computadores cliente.  



##  <a name="configure-compliance-rules"></a>Configurar regras de conformidade  

Regras de conformidade especificam as condições que definem a conformidade de um item de configuração. Antes que uma configuração possa ser avaliada quanto à conformidade, ela deve ter pelo menos uma regra de conformidade. WMI, registro e as configurações de script permitem corrigir os valores encontrados são incompatíveis. Você pode criar novas regras ou navegue até uma configuração existente em qualquer item de configuração para selecionar regras nele.  


### <a name="to-create-a-compliance-rule"></a>Para criar uma regra de conformidade  

1. Na página **Regras de Conformidade** do **Assistente para Criar Item de Configuração**, selecione **Novo**.  

2. Na caixa de diálogo **Criar Regra** , forneça as seguintes informações:  

    - **Nome**: insira um nome para a regra de conformidade.  

    - **Descrição:** insira uma descrição para a regra de conformidade.  

    - **Configuração selecionada:** selecione **Procurar** para abrir a caixa de diálogo **Selecionar Configuração**. Selecione a configuração para a qual você deseja definir uma regra, ou selecione **Nova Configuração**. Quando tiver terminado, escolha **selecionar**.  

        > [!Tip]  
        > Para exibir informações sobre a configuração selecionada no momento, selecione **propriedades**.  

    - **Tipo de regra**: Selecione o tipo de regra de conformidade que você deseja usar:  

        - **Valor**: crie uma regra que compara o valor retornado pelo item de configuração com um valor especificado. Para obter mais informações sobre as configurações adicionais, consulte [regras de valor](#bkmk_value).  

        - **Existencial**: crie uma regra que avalia a configuração dependendo se ela existe em um dispositivo cliente ou do número de vezes que ele é encontrada. Para obter mais informações sobre as configurações adicionais, consulte [Existenciais regras](#bkmk_exist).  

3. Selecione **OK** para fechar a caixa de diálogo **Criar Regra**.  




### <a name="bkmk_value"></a> Regras de valor  

- **Propriedade**: A propriedade do objeto a ser verificado varia de acordo com a configuração selecionada. As propriedades disponíveis variam com base no tipo de configuração. 

- **A configuração deve ser compatível com o seguinte...** : As permissões ou regras disponíveis variam de acordo com o tipo de configuração.

- **Corrigir regras não compatíveis quando houver suporte**: selecione esta opção para que o Configuration Manager corrija automaticamente as regras não compatíveis. Configuration Manager dá suporte a essa ação com os seguintes tipos de regra:  

    - **Valor do registro**: se não for compatível, o cliente define o valor do registro. Se ele não existir, o cliente cria o valor.  

    - **Script**: O cliente usa o script de correção que você especificou com a configuração.  

    - **Consulta WQL**  

    > [!IMPORTANT]  
    > Só é possível corrigir regras não compatíveis quando o operador de regra é definido como **É igual a**.  

- **Relatar não conformidade se esta instância de configuração não for encontrada**: se essa configuração não for encontrada em computadores cliente, habilite esta opção para o item de configuração Relatar não conformidade.  

- **Severidade de não conformidade para relatórios**: especifique o nível de severidade relatado nos relatórios do Configuration Manager, se essa regra de conformidade falhar. Os níveis de severidade a seguir estão disponíveis:  
    - **Nenhum**  
    - **Informações**  
    - **Aviso**  
    - **Crítico**  
    - **Crítico com evento**: computadores que não cumprem essa regra de conformidade relatam uma severidade de falha **Crítica**. Esse nível de severidade também é registrado como um evento do Windows no log de eventos de aplicativos.  


### <a name="bkmk_exist"></a> Regras existenciais 

> [!NOTE]  
> As opções exibidas podem variar, dependendo do tipo de configuração que está sendo usado para definir uma regra.  

- **A configuração deve existir em dispositivos cliente**  

- **A configuração não deve existir em dispositivos cliente**  

- **A configuração ocorre o seguinte número de vezes:**  

- **Severidade de não conformidade para relatórios**: especifique o nível de severidade relatado nos relatórios do Configuration Manager, se essa regra de conformidade falhar. Os níveis de severidade a seguir estão disponíveis:  
    - **Nenhum**  
    - **Informações**  
    - **Aviso**  
    - **Crítico**  
    - **Crítico com evento**: computadores que não cumprem essa regra de conformidade relatam uma severidade de falha **Crítica**. Esse nível de severidade também é registrado como um evento do Windows no log de eventos de aplicativos.  



## <a name="next-steps"></a>Próximas etapas

[Criar linhas de base de configuração](/sccm/compliance/deploy-use/create-configuration-baselines)
