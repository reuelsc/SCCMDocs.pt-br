---
title: 'Criar itens de configuração para computadores com Windows gerenciados pelo cliente '
titleSuffix: Configuration Manager
description: Gerencie configurações para computadores e servidores Windows com um item personalizado de configuração de Desktops e Servidores Windows.
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ba02c1c3558cc7c0f7280e9517d7b67ee8e46eec
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130370"
---
# <a name="how-to-create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-system-center-configuration-manager-client"></a>Como criar itens de configuração personalizados para computadores desktop e de servidor com Windows gerenciados com o cliente do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Use o item de configuração **Servidores e Desktops Windows personalizados** do System Center Configuration Manager para gerenciar as configurações de computadores e servidores Windows e que são gerenciados pelo cliente do Configuration Manager.  

## <a name="start-the-create-configuration-item-wizard"></a>Iniciar o Assistente para criar item de configuração

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Itens de Configuração**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Item de Configuração**.  

4.  Na página **Geral** do **Assistente para Criar Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  

5.  Em **Especificar o tipo de item de configuração que deseja criar**, selecione **Windows Desktops e Servers (personalizado)**.  

    > [!TIP]  
    >  Se quiser fornecer configurações do método de detecção que verifica a existência de um aplicativo, selecione **Este arquivo de configuração contém as configurações do aplicativo**.  

6.  Se você criar e atribuir categorias, clique em **Categorias** para ajudá-lo a pesquisar e filtrar itens de configuração no console do Configuration Manager.  

## <a name="provide-detection-method-information"></a>Fornecer informações do método de detecção  
 Use este procedimento para fornecer informações sobre o método de detecção para o item de configuração.  

> [!NOTE]  
>  Se aplica somente se você selecionou **este item de configuração contém as configurações do aplicativo** sobre o **geral** página do assistente.  

 Um método de detecção no Configuration Manager contém regras que são usadas para detectar se um aplicativo é instalado em um computador. Essa detecção ocorre antes que o item de configuração é avaliado quanto à conformidade. Para detectar se um aplicativo estiver instalado, você pode detectar a presença de um arquivo do Windows Installer para o aplicativo, use um script personalizado, ou selecione **sempre assumir o aplicativo é instalado** para avaliar o item de configuração para fins de conformidade, independentemente se o aplicativo está instalado.  

 Use estes procedimentos para configurar métodos de detecção no System Center Configuration Manager.  

### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>Para detectar a instalação de um aplicativo usando o arquivo do Windows Installer  

1.  No **métodos de detecção** página do **Criar Assistente de Item de configuração**, selecione o **Use Windows Installer detection** caixa de seleção.  

2.  Clique em **Abrir**, navegue até o arquivo do Windows Installer (. msi) que você deseja detectar e, em seguida, clique em **Abrir**.  

3.  O **versão** caixa é preenchida automaticamente com o número de versão de arquivo do Windows Installer que você selecionou. Você pode inserir um novo número de versão nesta caixa, se o valor exibido está incorreto.  

4.  Marque a caixa de seleção **Este aplicativo está instalado para um ou mais usuários** se desejar detectar o perfil de cada usuário no computador.  

### <a name="to-detect-a-specific-application-and-deployment-type"></a>Para detectar um tipo específico de aplicativo e implantação  

1.  Na página **Métodos de Detecção** do **Assistente para Criar Item de Configuração**, marque a caixa de seleção **Detectar um tipo de implantação e aplicativo específico** e clique em **Selecionar**.  

2.  Na caixa de diálogo **Especificar Aplicativo** , selecione o aplicativo e um tipo de implantação associado que deseja detectar.  

### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>Para detectar a instalação de um aplicativo usando um script personalizado  

1.  No **métodos de detecção** página do **Criar Assistente de Item de configuração**, selecione o **usar um script personalizado para detectar este aplicativo** caixa de seleção.  

2.  Na lista, selecione o idioma do script que você deseja abrir. Escolha entre os seguintes scripts:  

    -   **VBScript**  

    -   **JScript**  

    -   **PowerShell**  

3.  Clique em **Abrir**, navegue até o script que deseja usar e clique em **Abrir**.  

##  <a name="configure-settings"></a>Definir configurações  
 Use este procedimento para definir as configurações no item de configuração.  

 Configurações representam as condições comerciais ou técnicas que são usadas para avaliar a conformidade em dispositivos cliente. Você pode definir uma nova configuração ou navegar até uma configuração existente em um computador de referência.  

1. No **configurações** página do **Criar Assistente de Item de configuração**, clique em **novo**.  

2. Sobre o **geral** guia do **Criar configuração** diálogo caixa, forneça as seguintes informações:  

   - **Nome:** Insira um nome exclusivo para a configuração. Você pode usar no máximo 256 caracteres.  

   - **Descrição:** Insira uma descrição para a configuração. Você pode usar no máximo 256 caracteres.  

   - **Tipo de configuração:** Na lista, escolha e configure um dos seguintes tipos de configuração a ser usado para esta configuração:  

     - **Consulta ao Active Directory**  

        **Prefixo LDAP** - Especifique um prefixo válido para a consulta dos Serviços de Domínio do Active Directory para avaliar a conformidade nos computadores cliente. Você pode usar o **LDAP: / /** para um ou **GC: / /** para realizar uma pesquisa de catálogo global.  

        **DN (nome distinto)** -especifique o nome distinto do objeto Active Directory Domain Services que é avaliada quanto à conformidade nos computadores cliente.  

        Por exemplo, se quiser avaliar um valor relacionado a um usuário chamado João Fernandes no domínio corp.contoso.com, digite o seguinte:  

       - **Filtro de pesquisa** - Especifique um filtro LDAP opcional para refinar os resultados da consulta aos Serviços de Domínio Active Directory para avaliar a conformidade nos computadores cliente.  

          Para retornar todos os resultados da consulta, digite **(objectclass=\*)**.  

       - **Escopo da pesquisa** - especifique o escopo da pesquisa nos Serviços de Domínio do Active Directory. Você pode escolher:  

         -   **Base** -consulta apenas o objeto especificado.  

         -   **Um Nível** – Esta opção não é usada nesta versão do Configuration Manager.  

         -   **Subárvore** -consulta o objeto especificado e sua subárvore completa no diretório.  

       - **Propriedade** -especifique a propriedade do objeto Active Directory Domain Services que é usada para avaliar a conformidade em computadores cliente.  

          Por exemplo, se você quiser consultar a propriedade do Active Directory **badPwdCount**, que armazena o número de vezes que um usuário digitar incorretamente uma senha, digite **badPwdCount** neste campo.  

       - **Consulta** -exibe a consulta construída a partir de entradas no **prefixo LDAP**, **DN (nome distinto)**, **filtro de pesquisa** (se especificado), e **propriedade**, que são usados para avaliar a conformidade em computadores cliente.  

         Para obter mais informações sobre como construir consultas LDAP, consulte a documentação do Windows Server.  

     - **Assembly**  

        Defina o seguinte para esse tipo de configuração:  

       - **Nome do assembly:** Especifica o nome do objeto de assembly que você deseja pesquisar. O nome não pode ser o mesmo que outros objetos de assembly do mesmo tipo e deve ser registrado no Cache de Assembly Global. O nome do assembly pode ter até 256 caracteres.  

         Um assembly é um trecho de código que pode ser compartilhado entre aplicativos. Módulos (assemblies) podem ter a extensão de nome de arquivo. dll ou .exe. Cache de Assembly Global é uma pasta chamada *%systemroot%\Assembly* no cliente computadores em que todos os assemblies compartilhados são armazenados.  

     - **Sistema de arquivos**  

       - **Tipo** – Na lista, selecione se deseja pesquisar um **Arquivo** ou uma **Pasta**.  

       - **Caminho** -especifique o caminho da pasta ou arquivo especificado nos computadores cliente. Você pode especificar variáveis de ambiente do sistema e a variável de ambiente *%USERPROFILE%* no caminho.  

         > [!NOTE]  
         >  Se você usar a variável de ambiente *%USERPROFILE%* nas caixas **Caminho** ou **Nome do arquivo ou da pasta** , todos os perfis de usuário no computador cliente serão pesquisados, o que poderá resultar em várias instâncias do arquivo ou da pasta que foi encontrada.  
         >   
         >  Se as configurações de conformidade não tiverem acesso ao caminho especificado, será gerado um erro de descoberta. Além disso, se o arquivo que você está procurando está em uso, é gerado um erro de detecção.  

       - **Nome de arquivo ou pasta** -especifique o nome do objeto de arquivo ou pasta para pesquisar. Você pode especificar variáveis de ambiente do sistema e a variável de ambiente *%USERPROFILE%* no nome do arquivo ou da pasta. Você também pode usar os caracteres curinga * e ? no nome do arquivo.  

         > [!NOTE]  
         >  Se você especificar um nome de arquivo ou de pasta e usar caracteres curinga, essa combinação poderá produzir um grande número de resultados e poderá resultar em alta utilização de recursos no computador cliente e em alto tráfego de rede ao relatar resultados para o Configuration Manager.  

       - **Incluir subpastas** – Habilite esta opção se também desejar pesquisar quaisquer subpastas no caminho especificado.  

       - **Esse arquivo ou pasta está associada um aplicativo de 64 bits** - se habilitada, somente os locais de arquivo de 64 bits (como *% ProgramFiles %*) será verificada em computadores de 64 bits. Se essa opção não estiver habilitada, ambos os locais de 32 bits (como *%ProgramFiles(x86)%*) e de 64 bits serão verificados.  

         > [!NOTE]  
         >  Se o mesmo arquivo ou pasta existir nos dois locais do arquivo do sistema de 64 e de 32 bits no mesmo computador de 64 bits, vários arquivos serão detectados pela condição global.  

         O tipo de configuração **Sistema de arquivos** não dá suporte à especificação de um caminho UNC para um compartilhamento de rede na caixa **Caminho** .  

     - **Metabase do IIS**  

       -   **Caminho de metabase** -Especifique um caminho válido para a Metabase do IIS (Serviços de Informações da Internet).  

       -   **ID da Propriedade** - Especifique a propriedade numérica da configuração da Metabase do IIS.  

     - **Chave do Registro**  

       -   **Hive** - Na lista, selecione o hive de Registro que deseja pesquisar.  

       -   **Chave** - Especifique o nome da chave do Registro que deseja pesquisar. Use o formato *key\subkey*.  

       -   **Essa chave do registro está associada um aplicativo de 64 bits** -Especifica se as chaves do registro de 64 bits devem ser pesquisadas além as chaves de registro de 32 bits em clientes que executam uma versão de 64 bits do Windows.  

           > [!NOTE]  
           >  Se a mesma chave do Registro existir nos dois locais do Registro, de 64 e de 32 bits, no mesmo computador de 64 bits, ambas as chaves do Registro serão detectadas pela condição global.  

     - **Valor do Registro**  

       - **Hive** - Na lista, selecione o hive de Registro que deseja pesquisar.  

       - **Chave** - Especifique o nome da chave do Registro que deseja pesquisar. Use o formato *key\subkey*.  

       - **Valor** – Especifique o valor que deve estar contido na chave do Registro especificado.  

       - **A chave do Registro está associada ao aplicativo de 64 bits** - Especifica se as chaves do Registro de 64 bits devem ser pesquisadas além das chaves do Registro de 32 bits em clientes que executam uma versão de 64 bits do Windows.  

         > [!NOTE]  
         >  Se a mesma chave do Registro existir nos dois locais do Registro, de 64 e de 32 bits, no mesmo computador de 64 bits, ambas as chaves do Registro serão detectadas pela condição global.  

         Você também pode clicar em **Procurar** para navegar até um local do Registro no computador ou em um computador remoto. Para procurar um computador remoto, você deve ter direitos de administrador no computador remoto e o computador remoto deve estar executando o serviço Registro remoto.  

     - **script**  

       -   **Script de descoberta** – Clique em **Adicionar** para digitar ou procure o script que deseja usar. Você pode usar scripts do Windows PowerShell, VBScript ou Microsoft JScript.  

       -   **Executar scripts usando as credenciais do usuário conectado** – Se você habilitar esta opção, o script será executado em computadores cliente que usam as credenciais de usuários conectados.  

           > [!NOTE]  
           >  O valor retornado pelo script será usado para avaliar a conformidade da condição global. Por exemplo, ao usar o VBScript, você poderá usar o comando **WScript.Echo Result** para retornar o valor da variável *Result* para a condição global.  

     - **Consulta SQL**  

       -   **Instância do SQL Server** – Escolha se deseja que a consulta SQL seja executada na instância padrão, em todas as instâncias ou em um determinado nome da instância do banco de dados.  

           > [!NOTE]  
           >  O nome da instância deve se referir a uma instância local do SQL Server. Para se referir a uma instância de servidor em cluster do SQL, você deve usar uma configuração de script.  

       -   **Banco de dados** -especifique o nome do banco de dados Microsoft SQL Server no qual você deseja executar a consulta SQL.  

       -   **Coluna** -especifique o nome da coluna retornado pela instrução Transact-SQL que é usada para avaliar a conformidade da condição global.  

       -   **Instrução Transact-SQL** – especifique a consulta SQL completa que deseja usar para a condição global. Você também pode clicar **Abrir** para abrir uma consulta SQL existente.  

           > [!IMPORTANT]  
           >  As configurações da consulta SQL não dão suporte a comandos SQL que modificam o banco de dados. Só é possível usar comandos SQL que leem as informações do banco de dados.  

     - **Consulta WQL**  

       -   **Namespace** -especifique o namespace do Windows Management Instrumentation (WMI) que é usado para criar uma consulta WQL que é avaliada quanto à conformidade nos computadores cliente. O valor padrão é Root\cimv2.  

       -   **Classe** -Especifica a classe WMI que é usada para criar uma consulta WQL que é avaliada quanto à conformidade nos computadores cliente.  

       -   **Propriedade** -Especifica a propriedade WMI que é usada para criar uma consulta WQL que é avaliada quanto à conformidade nos computadores cliente.  

       -   **Cláusula WHERE da consulta WQL** - Você pode usar o item **Cláusula WHERE da consulta WQL** para especificar uma cláusula WHERE a ser aplicada ao namespace, à classe e à propriedade especificados em computadores cliente.  

     - **Consulta XPath**  

       - **Caminho** - Especifique o caminho para o arquivo .xml nos computadores cliente que será usado para avaliar a conformidade. O Configuration Manager dá suporte ao uso de todas as variáveis de ambiente do sistema Windows e à variável de usuário *%USERPROFILE%* no nome do caminho.  

       - **Nome do arquivo XML** -especifique o nome do arquivo que contém a consulta XML que é usada para avaliar a conformidade em computadores cliente.  

       - **Incluir subpastas** - Habilite esta opção se também desejar pesquisar quaisquer subpastas no caminho especificado.  

       - **Este arquivo está associado a um aplicativo de 64 bits** ‑ Escolha se o local do arquivo do sistema de 64 bits (*%windir%* \System32) deve ser pesquisado além do local do arquivo do sistema de 32 bits (*%windir%* \Syswow64) em clientes do Configuration Manager que executam uma versão de 64 bits do Windows.  

       - **Consulta XPath** -especifique uma completa XML caminho language (XPath) consulta válida que é usada para avaliar a conformidade em computadores cliente.  

       - **Namespaces** - Abre a caixa de diálogo **Namespaces do XML** para identificar namespaces e prefixos a ser usados durante a consulta XPath.  

         Se você tentar descobrir um arquivo .XML criptografado, as configurações de conformidade encontram o arquivo, mas a consulta XPath não produzirá nenhum resultado e nenhum erro será gerado.  

         Se a consulta XPath não for válida, a configuração será avaliada como não compatível nos computadores cliente.  

   - **Tipo de dados:** Na lista, escolha o formato no qual a condição retorna os dados antes que sejam usados para avaliar a configuração. O **tipo de dados** lista não é exibida para todos os tipos de configuração.  

     > [!NOTE]  
     >  O **ponto flutuante** tipo de dados suporta apenas 3 dígitos após o ponto decimal.  

3. Configurar detalhes adicionais sobre essa configuração sob o **Definindo tipo** lista. Os itens que você pode configurar variam dependendo do tipo de configuração que você selecionou.  

   > [!NOTE]  
   >  Quando você cria as configurações do tipo **sistema de arquivos**, **chave do registro**, e **valor do registro**, você pode clicar em **Procurar** para definir a configuração de valores em um computador de referência. Para procurar uma chave do registro ou um valor em um computador remoto, o computador remoto deve ter o serviço Registro remoto habilitado.  

4. Clique em **OK** para salvar a configuração e fechar a caixa de diálogo **Criar Configuração** .  

##  <a name="configure-compliance-rules"></a>Configurar regras de conformidade  
 Use o procedimento a seguir para configurar as regras de conformidade para o item de configuração.  

 Regras de conformidade especificam as condições que definem a conformidade de um item de configuração. Antes que uma configuração possa ser avaliada quanto à conformidade, ela deve ter pelo menos uma regra de conformidade. WMI, registro e as configurações de script permitem corrigir os valores encontrados são incompatíveis. Você pode criar novas regras ou navegue até uma configuração existente em qualquer item de configuração para selecionar regras nele.  

### <a name="to-create-a-compliance-rule"></a>Para criar uma regra de conformidade  

1.  No **as regras de conformidade** página do **Criar Assistente de Item de configuração**, clique em **novo**.  

2.  Na caixa de diálogo **Criar Regra** , forneça as seguintes informações:  

    -   **Nome:** insira um nome para a regra de conformidade.  

    -   **Descrição:** insira uma descrição para a regra de conformidade.  

    -   **Configuração selecionada:** clique em **Procurar** para abrir a caixa de diálogo **Selecionar Configuração**. Selecione a configuração que você deseja definir uma regra de, ou clique em **nova configuração**. Quando tiver terminado, clique em **Selecione**.  

        > [!NOTE]  
        >  Você também pode clicar em **propriedades** para exibir informações sobre a configuração selecionada no momento.  

    -   **Tipo de regra:** selecione o tipo de regra de conformidade que você deseja usar:  

        -   **Valor** criar uma regra que compara o valor retornado pelo item de configuração com um valor que você especificar.  

        -   **Existential** criar uma regra que avalia a configuração dependendo se ela existe em um dispositivo cliente ou no número de vezes que ele for encontrado.  

    -   Para um tipo de regra de **valor**, especifique as seguintes informações:  

        -   **a configuração deve estar de acordo com a seguinte regra** – selecione um operador e um valor que é avaliada quanto à conformidade com a configuração selecionada. Você pode usar os seguintes operadores:  

            |Operador|Mais informações|  
            |--------------|----------------------|  
            |Igual a|Nenhuma informação adicional|  
            |Não é igual a|Nenhuma informação adicional|  
            |Maior que|Nenhuma informação adicional|  
            |Menor que|Nenhuma informação adicional|  
            |Entre|Nenhuma informação adicional|  
            |Maior ou igual a|Nenhuma informação adicional|  
            |Menor ou igual a|Nenhuma informação adicional|  
            |Um dos|Na caixa de texto, especifique uma entrada em cada linha.|  
            |Nenhum dos|Na caixa de texto, especifique uma entrada em cada linha.|  

        -   **Corrigir regras não compatíveis quando houver suporte** – Selecione esta opção se desejar que o Configuration Manager corrija automaticamente as regras não compatíveis. O Configuration Manager pode corrigir automaticamente os seguintes tipos de regra:  

            -   **Valor do registro** – o valor do registro é corrigido se ele está em conformidade e criado se ele não existir.  

            -   **Script** (executando automaticamente um script de correção).  

            -   **Consulta WQL**  

            > [!IMPORTANT]  
            >  Só é possível corrigir regras não compatíveis quando o operador de regra é definido como **É igual a**.  

        -   **Não conformidade de relatório se essa instância de configuração não foi encontrada** – o item de configuração relatórios de não conformidade se essa configuração não for encontrada em computadores cliente.  

        -   **Gravidade de não conformidade para relatórios:** Especifique o nível de gravidade relatado (nos relatórios do Configuration Manager) se a regra de conformidade não for cumprida. Os níveis de severidade disponíveis são os seguintes:  

            -   **Nenhum** Computadores que não cumprem essa regra de conformidade não relatam uma severidade de falha.  

            -   **Informações** Computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Informações**.  

            -   **Aviso** Computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Aviso**.  

            -   **Crítico** Computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico**.  

            -   **Crítico com evento** Computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico**. Esse nível de severidade também é registrado como um evento do Windows no log de eventos de aplicativos.  

        -   Para um tipo de regra de **Existential**, especifique as seguintes informações:  

            > [!NOTE]  
            >  As opções exibidas podem variar dependendo do tipo de configuração que você estiver configurando uma regra.  

            -   **A configuração deve existir em dispositivos cliente**  

            -   **A configuração não deve existir em dispositivos cliente**  

            -   **A configuração ocorre o seguinte número de vezes:**  

        -   **Gravidade de não conformidade para relatórios:** Especifique o nível de gravidade relatado (nos relatórios do Configuration Manager) se a regra de conformidade não for cumprida. Os níveis de severidade disponíveis são os seguintes:  

            -   **Nenhum** Computadores que não cumprem essa regra de conformidade não relatam uma severidade de falha.  

            -   **Informações** Computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Informações**.  

            -   **Aviso** Computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Aviso**.  

            -   **Crítico** Computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico**.  

            -   **Crítico com evento** Computadores que não cumprem essa regra de conformidade relatam uma severidade de falha de **Crítico**. Esse nível de severidade também é registrado como um evento do Windows no log de eventos de aplicativos.  

3.  Clique em **OK** para fechar a caixa de diálogo **Criar Regra** .  

##  <a name="specify-supported-platforms"></a>Especificar as plataformas com suporte  
 Plataformas com suporte são os sistemas operacionais nos quais um item de configuração é avaliado quanto à conformidade.  

Na página **Plataformas com Suporte** do **Assistente para Criar Item de Configuração**, na lista, selecione as versões do Windows nas quais você deseja que o item de configuração seja avaliado quanto à conformidade, ou clique em **Selecionar tudo**.  

## <a name="complete-the-wizard"></a>Concluir o assistente  
 Na página **Resumo** do Assistente, examine as ações a serem tomadas e conclua o assistente. O novo item de configuração é exibido no nó **Itens de Configuração** do workspace **Ativos e Conformidade**.  
