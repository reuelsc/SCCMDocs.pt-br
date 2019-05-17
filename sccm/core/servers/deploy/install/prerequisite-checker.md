---
title: Verificador de Pré-requisitos
titleSuffix: Configuration Manager
description: Saiba como usar o Verificador de Pré-requisitos para identificar e corrigir problemas que podem impedir a instalação de um site ou função de sistema de sites.
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 303092686611d08d8b05a5dafd9ee669ea2271a6
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65497737"
---
# <a name="prerequisite-checker-for-system-center-configuration-manager"></a>Verificador de pré-requisitos para System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Antes de executar a Instalação para instalar ou atualizar um site do System Center Configuration Manager ou antes de instalar uma função de sistema de sites em um novo servidor, você pode usar esse aplicativo autônomo (**Prereqchk.exe**) da versão do Configuration Manager que você deseja usar para verificar a preparação do servidor. Use o Verificador de Pré-requisitos para identificar e corrigir problemas que impediriam a instalação de um site ou função de sistema de sites.  

> [!NOTE]  
>  O Verificador de Pré-requisitos sempre é executado como parte da instalação.  

Por padrão, quando o Verificador de Pré-requisitos é executado:  

-   Ele valida o servidor no qual é executado.  
-   O computador local é examinado quanto à presença de um servidor do site existente e somente as verificações aplicáveis ao site são executadas.  
-   Se nenhum site existente é detectado, todas as regras de pré-requisitos são executadas.  
-   Ele verifica as regras para confirmar se o software e as configurações necessárias para a instalação estão instaladas. É possível que o software necessário exija configurações adicionais ou atualizações de software que não sejam verificadas pelo Verificador de Pré-requisitos.  
-   Ele registra seus resultados no arquivo **ConfigMgrPrereq.log** na unidade do sistema do computador. O arquivo de log pode conter informações adicionais que não aparecem na interface do aplicativo.  

Quando você executa o Verificador de Pré-requisitos no prompt de comando e especifica as opções de linha de comando específicas:  

-   O Verificador de Pré-requisitos executa apenas as verificações que estão associadas ao servidor do site ou aos sistemas de sites especificados na linha de comando.  
-   Para verificar um computador remoto, sua conta de usuário deve ter direitos de Administrador para remover o computador.  

Para obter mais informações sobre as verificações que o Verificador de Pré-requisitos realiza, consulte [Lista de verificações de pré-requisitos para o System Center Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md).  

## <a name="copy-prerequisite-checker-files-to-another-computer"></a>Copiar os arquivos do Verificador de Pré-requisitos para outro computador  

1.  No Windows Explorer, vá até um dos seguintes locais:  

    -   **&lt;*Mídia de instalação do Configuration Manager*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Caminho de instalação do Configuration Manager*\>\BIN\X64**  

2.  Copie os seguintes arquivos para a pasta de destino no outro computador:  

    -   Prereqchk.exe  
    -   Prereqcore.dll  
    -   Basesql.dll  
    -   Basesvr.dll  
    -   Baseutil.dll  

##  <a name="run-prerequisite-checker-with-default-checks"></a>Executar o Verificador de Pré-requisitos com verificações padrão  

1.  No Windows Explorer, vá até um dos seguintes locais:  

    -   **&lt;*Mídia de instalação do Configuration Manager*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Caminho de instalação do Configuration Manager*\>\BIN\X64**  

2.  Execute **prereqchk.exe** para iniciar o Verificador de Pré-requisitos.   
    O Verificador de Pré-requisitos detecta os sites existentes e, se encontrados, executa as verificações quanto à preparação para atualização. Se nenhum site é encontrado, todas as verificações são executadas. A coluna **Tipo de site** fornece informações sobre o servidor do site ou sistema do site a qual regra é associada.  

##  <a name="run-prerequisite-checker-from-a-command-prompt-for-all-default-checks"></a>Executar o Verificador de Pré-requisitos em um prompt de comando para todas as verificações padrão  

1.  Abra uma janela de Prompt de Comando e altere os diretórios para um dos seguintes locais:  

    -   **&lt;*Mídia de instalação do Configuration Manager*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Caminho de instalação do Configuration Manager*\>\BIN\X64**  

2.  Digite  **prereqchk.exe /LOCAL** para iniciar o Verificador de Pré-requisitos e executar todas as verificações de pré-requisitos no servidor.  

## <a name="run-prerequisite-checker-from-a-command-prompt-to-use-options"></a>Executar o Verificador de Pré-requisitos em um prompt de comando para usar opções  

1. Abra uma janela de Prompt de Comando e altere os diretórios para um dos seguintes locais:  

   -   **&lt;*Mídia de instalação do Configuration Manager*\>\SMSSETUP\BIN\X64**  
   -   **&lt;*Caminho de instalação do Configuration Manager*\>\BIN\X64**  

2. Digite **prereqchk.exe** com a adição de uma ou mais das seguintes opções de linha de comando.  

   Por exemplo, para verificar um site primário, você pode usar o seguinte:  

      **prereqchk.exe [/NOUI] /PRI /SQL &lt;FQDN do SQL Server\> /SDK &lt;FQDN do Provedor de SMS\> [/JOIN &lt;FQDN do site de administração central\>] [/MP &lt;FQDN do ponto de gerenciamento\>] [/DP &lt;FQDN do ponto de distribuição\>]**  

   **Servidor do site de administração central:**  

   -   **/NOUI**  

        Não necessário. Inicia o Verificador de Pré-requisitos sem exibir a interface do usuário. Você deve especificar essa opção antes de qualquer outra opção na linha de comando.  

   -   **/CAS**  

        Necessário. Verifica se o computador local atende aos requisitos do site de administração central.  

   -   **/SQL &lt;*FQDN do SQL Server*>**  

        Necessário. Usando o FQDN (nome de domínio totalmente qualificado), verifica se o computador especificado atende aos requisitos do SQL Server para hospedar o banco de dados do site do Configuration Manager.  

   -   **/SDK &lt;*FQDN do Provedor de SMS*>**  

        Necessário. Verifica se o computador especificado atende aos requisitos do Provedor de SMS.  

   -   **/Ssbport**  

        Não necessário. Verifica se a exceção de firewall está em vigor para permitir a comunicação na porta do SQL SSB (Server Service Broker). A porta padrão do SSB é a 4022.  

   -   **InstallDir &lt;*caminho de instalação do Configuration Manager*>**  

        Não necessário. Verifica o espaço em disco mínimo nos requisitos para a instalação do site.  

   **Servidor do site primário:**  

   -   **/NOUI**  

       Não necessário. Inicia o Verificador de Pré-requisitos sem exibir a interface do usuário. Você deve especificar essa opção antes de qualquer outra opção na linha de comando.  

   -   **/PRI**  

        Necessário. Verifica se o computador local atende aos requisitos do site primário.  

   -   **/SQL &lt;*FQDN do SQL Server*>**  

        Necessário. Verifica se o computador especificado atende aos requisitos do SQL Server para hospedar o banco de dados do site do Configuration Manager.  

   -   **/SDK &lt;*FQDN do Provedor de SMS*>**  

        Necessário. Verifica se o computador especificado atende aos requisitos do Provedor de SMS.  

   -   **/JOIN &lt;*FQDN do site de administração central*>**  

        Não necessário. Verifica se o computador local atende aos requisitos para se conectar ao servidor do site de administração central.  

   -   **/MP &lt;*FQDN do ponto de gerenciamento*>**  

        Não necessário. Verifica se o computador especificado atende aos requisitos da função do sistema de site do ponto de gerenciamento. Há suporte para essa opção apenas quando você usa a opção **/PRI** .  

   -   **/DP &lt;*FQDN do ponto de distribuição*>**  

        Não necessário. Verifica se o computador especificado atende aos requisitos da função do sistema de site do ponto de distribuição. Há suporte para essa opção apenas quando você usa a opção **/PRI** .  

   -   **/Ssbport**  

        Não necessário. Verifica se a exceção de firewall está em vigor para permitir a comunicação na porta SSB. A porta padrão do SSB é a 4022.  

   -   **InstallDir &lt;*caminho de instalação do Configuration Manager*>**  

        Não necessário. Verifica o espaço em disco mínimo nos requisitos para a instalação do site.  

   **Servidor do site secundário:**  

   -   **/NOUI**  

        Não necessário. Inicia o Verificador de Pré-requisitos sem exibir a interface do usuário. Você deve especificar essa opção antes de qualquer outra opção na linha de comando.  

   -   **/SEC &lt;*FQDN do servidor do site secundário*>**  

        Necessário. Verifica se o computador especificado atende aos requisitos do site secundário.  

   -   **/INSTALLSQLEXPRESS**  

        Não necessário. Verifica se o SQL Server Express pode ser instalado no computador especificado.  

   -   **/Ssbport**  

        Não necessário. Verifica se a exceção de firewall está em vigor para permitir a comunicação para a porta SSB. A porta padrão do SSB é a 4022.  

   -   **/Sqlport**  

        Não necessário. Verifica se a exceção de firewall está em vigor para permitir a comunicação para a porta de serviço do SQL Server e se a porta não está em uso por outra instância nomeada do SQL Server. A porta padrão é a 1433.  

   -   **InstallDir &lt;*caminho de instalação do Configuration Manager*>**  

        Não necessário. Verifica o espaço em disco mínimo nos requisitos para a instalação do site.  

   -   **/SourceDir**  

        Não necessário. Verifica se a conta de computador do site secundário pode acessar a pasta que hospeda os arquivos de origem para a Instalação.  

   **Console do Configuration Manager:**  

   -   **/Adminui**  

        Necessário. Verifica se o computador local cumpre os requisitos para instalar o Configuration Manager.  

3. Na interface do usuário do Verificador de Pré-requisitos, é criada uma lista de problemas descobertos na seção **Resultado de pré-requisito**.  

   -   Clique em um item na lista para obter detalhes sobre como resolver o problema.  
   -   Você deve resolver todos os itens na lista que têm o status de **Erro** para poder instalar o servidor do site, o sistema de sites ou o console do Configuration Manager.  
   -   Você também pode abrir o arquivo **ConfigMgrPrereq.log** na raiz da unidade do sistema para examinar os resultados do Verificador de Pré-requisitos. O arquivo de log pode conter informações adicionais que não são exibidas na interface do usuário do Verificador de Pré-requisitos.  
