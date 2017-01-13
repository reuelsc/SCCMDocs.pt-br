---
title: "Verificador de pré-requisitos | Microsoft Docs"
description: "Saiba como usar o verificador de pré-requisitos para identificar e corrigir problemas que impediriam a instalação real de uma função do sistema de sites ou de um site."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: f30d7a451f47a3ab1efe6f7ac9c3e0151b8cda96

---
# <a name="prerequisite-checker-for-system-center-configuration-manager"></a>Verificador de pré-requisitos para System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


 Antes de executar a Instalação para instalar ou atualizar um site do System Center Configuration Manager ou antes de instalar uma função de sistema de sites em um novo servidor, você pode usar esse aplicativo autônomo (**Prereqchk.exe**) da versão do Configuration Manager que você deseja usar para verificar a preparação do servidor. O uso do verificador de pré-requisitos permite identificar e corrigir problemas que impediriam a instalação real de uma função do sistema de sites ou de um site.  

> [!NOTE]  
>  O verificador de pré-requisitos sempre é executado como parte da instalação.  

Por padrão, quando o verificador de pré-requisitos é executado:  

-   Ele valida o servidor no qual é executado  

-   O computador local é examinado quanto à presença de um servidor do site existente e somente as verificações aplicáveis ao site são executadas  

-   Se nenhum site existente for detectado, todas as regras de pré-requisitos serão executadas  

-   Ele verifica as regras para confirmar se o software e as configurações necessárias para a instalação estão instaladas. É possível que o software necessário exija configurações adicionais ou atualizações de software que não sejam verificadas pelo verificador de pré-requisitos  

-   Ele registra seus resultados no arquivo **ConfigMgrPrereq.log** na unidade do sistema do computador. O arquivo de log pode conter informações adicionais que não são exibidas na interface do usuário.  

Quando você executa o verificador de pré-requisitos no prompt de comando e especifica as opções de linha de comando específicas:  

-   O verificador de pré-requisitos só executa as verificações que estão associadas ao servidor do site ou a sistemas de sites que você especificou na linha de comando  

-   Para verificar um computador remoto, sua conta de usuário deve ter direitos administrativos para o computador remoto  

Para obter mais informações sobre as verificações de pré-requisitos que o verificador de pré-requisitos realiza, consulte [Lista de verificações de pré-requisitos para o System Center Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md)  

## <a name="copy-prerequisite-checker-files-to-another-computer"></a>Copiar os arquivos do verificador de pré-requisitos para outro computador  

1.  No Windows Explorer, navegue até um dos seguintes locais:  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

    -   **&lt;ConfigMgrInstallationPath\>\BIN\X64**  

2.  Copie os seguintes arquivos para a pasta de destino no outro computador:  

    -   Prereqchk.exe  

    -   Prereqcore.dll  

    -   Basesql.dll  

    -   Basesvr.dll  

    -   Baseutil.dll  

##  <a name="run-prerequisite-checker-with-default-checks"></a>Executar o verificador de pré-requisitos com verificações padrão  

1.  No Windows Explorer, navegue até um dos seguintes locais:  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

    -   **&lt;ConfigMgrInstallationPath\>\BIN\X64**  

2.  Execute **prereqchk.exe** para iniciar o Verificador de Pré-requisitos.   
    O Verificador de Pré-requisitos detecta os sites existentes e, se encontrados, executa as verificações quanto à preparação para atualização. Se nenhum site é encontrado, todas as verificações são executadas. A coluna **Tipo de site** fornece informações sobre o servidor do site ou sistema do site a qual regra é associada.  

##  <a name="run-prerequisite-checker-from-a-command-prompt-for-all-default-checks"></a>Executar o verificador de pré-requisitos em um prompt de comando para todas as verificações padrão  

1.  Abra uma janela de Prompt de Comando e altere os diretórios para um dos seguintes locais:  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

    -   **&lt;ConfigMgrInstallationPath\>\BIN\X64**  

2.  Digite  **prereqchk.exe /LOCAL** para iniciar o Verificador de Pré-requisitos e executar todas as verificações de pré-requisitos no servidor.  

## <a name="run-prerequisite-checker-from-a-command-prompt--for-specified-options"></a>Executar o verificador de pré-requisitos em um prompt de comando para as opções especificadas  

1.  Abra uma janela de Prompt de Comando e altere os diretórios para um dos seguintes locais:  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

    -   **&lt;ConfigMgrInstallationPath\>\BIN\X64**  

2.  Digite **prereqchk.exe** com a adição de uma ou mais das seguintes opções de linha de comando.  

    Por exemplo, para verificar um site primário, você pode usar o seguinte:  

    -   **prereqchk.exe [/NOUI] /PRI /SQL &lt;FQDN do SQL Server\> /SDK &lt;FQDN do Provedor de SMS\> [/JOIN &lt;FQDN do site de administração central\>] [/MP &lt;FQDN do ponto de gerenciamento\>] [/DP &lt;FQDN do ponto de distribuição\>]**  

    **Servidor do site de administração central:**  

    -   **/NOUI**  

         Não exigido - Inicia o Verificador de Pré-requisitos sem exibir a interface do usuário. Você deve especificar essa opção antes de qualquer outra opção na linha de comando.  

    -   **/CAS**  

         Exigido - Verifica se o computador local atende aos requisitos do site de administração central.  

    -   **/SQL &lt;*FQDN do SQL Server*>**  

         Exigido – Verifica se o computador especificado atende aos requisitos do SQL Server para hospedar o banco de dados do site do Configuration Manager.  

    -   **/SDK &lt;*FQDN do Provedor de SMS*>**  

         Exigido - Verifica se o computador especificado atende aos requisitos do Provedor de SMS.  

    -   **/Ssbport**  

         Não exigido - Verifica se a exceção de firewall está em vigor para permitir a comunicação na porta SSB. O padrão é o número da porta 4022.  

    -   **InstallDir &lt;*ConfigMgrInstallationPath*>**  

         Não exigido - Verifica o espaço em disco mínimo nos requisitos para a instalação do site.  

    **Servidor do site primário:**  

    -   **/NOUI**  

        Não exigido - Inicia o Verificador de Pré-requisitos sem exibir a interface do usuário. Você deve especificar essa opção antes de qualquer outra opção na linha de comando.  

    -   **/PRI**  

         Exigido - Verifica se o computador local atende aos requisitos do site primário.  

    -   **/SQL &lt;*FQDN do SQL Server*>**  

         Exigido – Verifica se o computador especificado atende aos requisitos do SQL Server para hospedar o banco de dados do site do Configuration Manager.  

    -   **/SDK &lt;*FQDN do Provedor de SMS*>**  

         Exigido - Verifica se o computador especificado atende aos requisitos do Provedor de SMS.  

    -   **/JOIN &lt;*FQDN do site de administração central*>**  

         Não exigido - Verifica se o computador local atende aos requisitos para se conectar ao servidor do site de administração central.  

    -   **/MP &lt;*FQDN do ponto de gerenciamento*>**  

         Não exigido - Verifica se o computador especificado atende aos requisitos da função do sistema de site do ponto de gerenciamento. Há suporte para essa opção apenas quando você usa a opção **/PRI** .  

    -   **/DP &lt;*FQDN do ponto de distribuição*>**  

         Não exigido - Verifica se o computador especificado atende aos requisitos da função do sistema de sites do ponto de distribuição. Há suporte para essa opção apenas quando você usa a opção **/PRI** .  

    -   **/Ssbport**  

         Não exigido - Verifica se a exceção de firewall está em vigor para permitir a comunicação na porta SSB. O padrão é o número da porta 4022.  

    -   **InstallDir &lt;*ConfigMgrInstallationPath*>**  

         Não exigido - Verifica o espaço em disco mínimo nos requisitos para a instalação do site.  

    **Servidor do site secundário:**  

    -   **/NOUI**  

         Não exigido - Inicia o Verificador de Pré-requisitos sem exibir a interface do usuário. Você deve especificar essa opção antes de qualquer outra opção na linha de comando.  

    -   **/SEC &lt;*FQDN do servidor do site secundário*>**  

         Exigido - Verifica se o computador especificado atende aos requisitos do site secundário.  

    -   **/INSTALLSQLEXPRESS**  

         Não exigido - Verifica se o SQL Server Express pode ser instalado no computador especificado.  

    -   **/Ssbport**  

         Não necessário ‑      
        Verifica se a exceção de firewall está em vigor para permitir a comunicação da porta do SSB (SQL Server Service Broker). O padrão é o número da porta 4022.  

    -   **/Sqlport**  

         Não exigido - Verifica se a exceção de firewall está em vigor para permitir a comunicação para a porta de serviço do SQL Server e se a porta não está em uso por outra instância nomeada do SQL Server. A porta padrão é a 1433.  

    -   **InstallDir &lt;*ConfigMgrInstallationPath*>**  

         Não exigido - Verifica o espaço em disco mínimo nos requisitos para a instalação do site.  

    -   **/SourceDir**  

         Não exigido - Verifica se a conta de computador do site secundário pode acessar a pasta que hospeda os arquivos de origem para a Instalação.  

     **Console do Configuration Manager:**  

    -   **/Adminui**  

         Exigido - Verifica se o computador local cumpre os requisitos para instalar o Configuration Manager.  

3.  Na interface do usuário do Verificador de Pré-requisitos, é criada uma lista de problemas descobertos na seção **Resultado de pré-requisito** .  

    -   Clique em um item na lista para obter detalhes sobre como resolver o problema.  

    -   Você deve resolver todos os itens na lista que têm o status de **Erro** para poder instalar o servidor do site, o sistema de sites ou o console do Configuration Manager.  

    -   Você também pode abrir o arquivo **ConfigMgrPrereq.log** na raiz da unidade do sistema para examinar os resultados do Verificador de Pré-requisitos. O arquivo de log pode conter informações adicionais que não são exibidas na interface do usuário.  



<!--HONumber=Dec16_HO3-->


