---
title: "Réplicas de banco de dados do ponto de gerenciamento | Microsoft Docs"
description: "Use uma réplica de banco de dados para reduzir a carga de CPU alocada no servidor de banco de dados do site por pontos de gerenciamento."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b06f781b-ab25-4d9a-b128-02cbd7cbcffe
caps.latest.revision: "9"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 130c053c9f2a1817dd85b1f3c01285aab19d59cb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="database-replicas-for-management-points-for-system-center-configuration-manager"></a>Réplicas de banco de dados para pontos de gerenciamento para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os sites primários do System Center Configuration Manager podem usar uma réplica de banco de dados para reduzir a carga de CPU alocada no servidor de banco de dados do site por pontos de gerenciamento conforme eles atendem solicitações de serviço de clientes.  

-   Quando um ponto de gerenciamento usa uma réplica de banco de dados, ele solicita dados do computados SQL Server que hospeda a réplica de banco de dados, em vez do servidor de banco de dados do site.  

-   Isso pode ajudar a reduzir os requisitos de processamento da CPU no servidor de banco de dados do site ao descarregar tarefas de processamento frequentes relacionadas aos clientes.  Um exemplo das tarefas de processamento frequentes para clientes inclui sites em que há um grande número de clientes que fazem solicitações frequentes para a política do cliente  


##  <a name="bkmk_Prepare"></a> Prepare-se para usar réplicas de banco de dados  
**Sobre réplicas de banco de dados para pontos de gerenciamento:**  

-   Réplicas são uma cópia parcial do banco de dados do site que é replicada para uma instância separada do SQL Server:  

    -   Sites primários dão suporte a uma réplica de banco de dados dedicado para cada ponto de gerenciamento no site (sites secundários não dão suporte a réplicas de banco de dados)  

    -   Uma réplica do banco de dados individual pode ser usada por mais de um ponto de gerenciamento do mesmo site  

    -   Um SQL Server pode hospedar várias réplicas de banco de dados para uso por diferentes pontos de gerenciamento, desde que cada uma seja executada em uma instância separada do SQL Server  

-   Réplicas sincronizam uma cópia do banco de dados de site em uma programação fixa de dados publicados pelo servidor de banco de dados de sites para essa finalidade.  

-   Pontos de gerenciamento podem ser configurados para usar uma réplica quando você instala o ponto de gerenciamento ou em um momento posterior reconfigurando o ponto de gerenciamento instalado anteriormente para usar a réplica de banco de dados  

-   Monitore regularmente o servidor de banco de dados do site e cada servidor de réplica de banco de dados para assegurar que a replicação ocorre entre eles, e que o desempenho do servidor de réplica de banco de dados é suficiente para o desempenho do site e do cliente que você requer  

**Pré-requisitos para réplicas de banco de dados:**  

-   **Requisitos do SQL Server:**  

    -   O SQL Server que hospeda a réplica de banco de dados deve atender aos mesmos requisitos do servidor de banco de dados do site. No entanto, o servidor de réplica não precisa executar a mesma versão ou edição do SQL Server que o banco de dados do site, desde que execute uma versão e uma edição com suporte do SQL Server. Para obter informações, consulte [Suporte para versões do SQL Server para o System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md)  

    -   O serviço SQL Server no computador que hospeda o banco de dados de réplica deve executar como a conta do **Sistema** .  

    -   O SQL Server que hospeda o banco de dados do site e o que hospeda uma réplica de banco de dados devem ter ambos a **replicação do SQL Server** instalada.  

    -   O banco de dados do site deve **publicar** a réplica de banco de dados e cada servidor de réplica de banco de dados remoto deve **assinar** os dados publicados.  

    -   O SQL Server que hospeda o banco de dados do site e uma réplica de banco de dados deve ser configurado para dar suporte a um **Tamanho Máximo de Repl. de Texto** de 2 GB. Para ver um exemplo de como configurar isso para o SQL Server 2012, consulte [Configurar a opção de configuração do servidor do tamanho máx. de repl. de texto](http://go.microsoft.com/fwlink/p/?LinkId=273960).  

-   **Certificado autoassinado:** para configurar uma réplica do banco de dados, você deve criar um certificado autoassinado no servidor de réplica de banco de dados e disponibilizar esse certificado para cada ponto de gerenciamento que usará esse servidor.  

    -   O certificado está disponível automaticamente para um ponto de gerenciamento instalado no servidor de réplica de banco de dados.  

    -   Para disponibilizar esse certificado para pontos de gerenciamento remoto, você deve exportá-lo e adicioná-lo ao repositório de certificados de **Pessoas Confiáveis** no ponto de gerenciamento remoto.  

-   **Notificação do cliente** : para dar suporte à notificação do cliente com uma réplica de banco de dados para um ponto de gerenciamento, você deve configurar a comunicação entre o servidor de banco de dados do site e o servidor de réplica de banco de dados no **SQL Server Service Broker**. Isso requer que você:  

    -   Configure cada banco de dados com informações sobre outro banco de dados  

    -   Troque certificados entre dois bancos de dados para comunicação segura  

**Limitações ao usar réplicas de banco de dados:**  

-   Quando seu site estiver configurado para publicar as réplicas de banco de dados, os procedimentos a seguir deverão ser usados no lugar da diretriz normal:  

    -   [Desinstalar um servidor do site que publique uma réplica de banco de dados](#BKMK_DBReplicaOps_Uninstall)  

    -   [Mover um banco de dados de servidor de site que publique uma réplica de banco de dados](#BKMK_DBReplicaOps_Move)  

-   **Atualizações para o System Center Configuration Manager**: antes de atualizar um site do System Center 2012 Configuration Manager para o System Center Configuration Manager, você deve desabilitar as réplicas de banco de dados para os pontos de gerenciamento.  Depois de atualizar seu site, você pode reconfigurar as réplicas de banco de dados de pontos de gerenciamento.  

-   **Várias réplicas em um único SQL Server:** se você configurar um servidor de réplica de banco de dados para hospedar várias réplicas de banco de dados para pontos de gerenciamento (cada réplica deve estar em uma instância separada), deverá usar um script de configuração modificado (da Etapa 4 da seção a seguir) para evitar a substituição do certificado autoassinado em uso pelas réplicas de banco de dados previamente configuradas no servidor.  

##  <a name="BKMK_DBReplica_Config"></a> Configurar réplicas de banco de dados  
Para usar configurar uma réplica de banco de dados, as etapas a seguir são necessárias:  

-   [Etapa 1 – configurar o servidor de banco de dados do site para publicar a réplica de banco de dados](#BKMK_DBReplica_ConfigSiteDB)  

-   [Etapa 2 – configurando o servidor de réplica de banco de dados](#BKMK_DBReplica_ConfigSrv)  

-   [Etapa 3 – configurar os pontos de gerenciamento para usar a réplica de banco de dados](#BKMK_DBReplica_ConfigMP)  

-   [Etapa 4 – configurar um certificado autoassinado para o servidor de réplica de banco de dados](#BKMK_DBReplica_Cert)  

-   [Etapa 5 – configurar o SQL Server Service Broker para o servidor de réplica de banco de dados](#BKMK_DBreplica_SSB)  

###  <a name="BKMK_DBReplica_ConfigSiteDB"></a> Etapa 1 – configurar o servidor de banco de dados do site para publicar a réplica de banco de dados  
 Use o procedimento a seguir como um exemplo de como configurar o servidor de banco de dados do site em um computador Windows Server 2008 R2 para publicar a réplica de banco de dados. Se você tiver uma versão diferente de sistema operacional, consulte a documentação do sistema operacional e ajuste as etapas neste procedimento conforme necessário.  

##### <a name="to-configure-the-site-database-server"></a>Para configurar o servidor de banco de dados do site  

1.  No servidor de banco de dados do site, defina o SQL Server Agent para iniciar automaticamente.  

2.  No servidor de banco de dados do site, crie um grupo de usuários local com o nome **ConfigMgr_MPReplicaAccess**. Você deve adicionar a esse grupo a conta de computador para cada servidor de réplica de banco de dados que você usar nesse site para habilitar esses servidores de réplica de banco de dados a sincronizar com a réplica de banco de dados publicado.  

3.  No servidor de banco de dados do site, configure um compartilhamento de arquivo com o nome **ConfigMgr_MPReplica**.  

4.  Adicione as seguintes permissões ao compartilhamento **ConfigMgr_MPReplica** :  

    > [!NOTE]  
    >  Se o SQL Server Agent usa uma conta diferente da conta do sistema local, substitua SISTEMA pelo nome dessa conta na seguinte lista.  

    -   **Permissões de compartilhamento**:  

        -   SISTEMA: **Gravação**  

        -   ConfigMgr_MPReplicaAccess: **Ler**  

    -   **Permissões NTFS**:  

        -   SISTEMA: **Controle total**  

        -   ConfigMgr_MPReplicaAccess: **Ler**, **Ler e executar** e **Listar conteúdo da pasta**  

5.  Use o **SQL Server Management Studio** para se conectar ao banco de dados do site e executar o seguinte procedimento armazenado como uma consulta: **spCreateMPReplicaPublication**  

Quando o procedimento armazenado for concluído, o servidor de banco de dados do site estará configurado para publicar a réplica de banco de dados.  

###  <a name="BKMK_DBReplica_ConfigSrv"></a> Etapa 2 – configurando o servidor de réplica de banco de dados  
O servidor de réplica de banco de dados é um computador que executa o SQL Server e que hospeda uma réplica do banco de dados do site para pontos de gerenciamento a serem usados. Em um agendamento fixo, o servidor de réplica de banco de dados sincroniza sua cópia do banco de dados com a réplica de banco de dados que é publicado pelo servidor de banco de dados do site.  

O servidor de réplica de banco de dados deve atender os mesmos requisitos do servidor de banco de dados do site. No entanto, o servidor de réplica de banco de dados pode executar uma edição ou versão diferente de SQL Server do que a usada pelo servidor de banco de dados do site. Para obter informações sobre as versões do SQL Server com suporte, consulte o tópico [Suporte para versões do SQL Server para o System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

> [!IMPORTANT]  
>  O serviço SQL Server no computador que hospeda o banco de dados de réplica deve executar como a conta do sistema.  

Use o procedimento a seguir como um exemplo de como configurar o servidor de réplica de banco de dados em um computador Windows Server 2008 R2. Se você tiver uma versão diferente de sistema operacional, consulte a documentação do sistema operacional e ajuste as etapas neste procedimento conforme necessário.  

##### <a name="to-configure-the-database-replica-server"></a>Para configurar o servidor de réplica de banco de dados  

1.  No servidor de réplica de banco de dados do site, defina o SQL Server Agent para inicialização automática.  

2.  No servidor de réplica de banco de dados, use o **SQL Server Management Studio** para conectar-se ao servidor local, navegue até a pasta **Replicação** , clique em Assinaturas Locais e selecione **Novas Assinaturas** para iniciar o **Assistente para Nova Assinatura**:  

    1.  Na página **Publicação** , na caixa de listagem **Publicador** , selecione **Encontrar Publicador SQL Server**, insira o nome do servidor de banco de dados dos sites e clique em **Conectar**.  

    2.  Selecione **ConfigMgr_MPReplica**e clique em **Próximo**.  

    3.  Na página **Local do agente de distribuição** , selecione **Executar cada agente em seu Assinante (assinaturas pull)**e clique em **Próximo**.  

    4.  Na página **Assinantes** , siga um destes procedimentos:  

        -   Selecione um banco de dados existente no servidor de réplica de banco de dados a ser usado para a réplica de banco de dados e clique em **OK**.  

        -   Selecione **Novo banco de dados** para criar um novo banco de dados para a réplica de banco de dados. Na página **Novo banco de dados** , especifique um nome de banco de dados e clique em **OK**.  

    5.  Clique em **Próximo** para continuar.  

    6.  Na página **Segurança do Agente de Distribuição**, clique no botão de propriedades **(.…)** na linha Conexão do Assinante da caixa de diálogo e defina as configurações de segurança para a conexão.  

        > [!TIP]  
        >  O botão de propriedades, **(....)**, está na quarta coluna da caixa de exibição.  

        **Configurações de segurança:**  

        -   Configure a conta que executa o processo do Agente de Distribuição (a conta de processo):  

            -   Se o SQL Server Agent é executado como um sistema local, selecione **Executar na conta de serviço do SQL Server Agent (Essa não é uma prática de segurança recomendada.)**  

            -   Se o SQL Server Agent é executado usando uma conta diferente, selecione **Executar nesta conta do Windows**e configure essa conta. Você pode especificar uma conta do Windows ou uma conta do SQL Server.  

            > [!IMPORTANT]  
            >  Você deve conceder a conta que executa as permissões do Agente de Distribuição ao publicador como uma assinatura pull. Para obter informações sobre a configuração dessas permissões, consulte [Segurança do agente de distribuição](http://go.microsoft.com/fwlink/p/?LinkId=238463) na Biblioteca do TechNet do SQL Server.  

        -   Para **Conectar ao Distribuidor**, selecione **Pela representação da conta do processo**.  

        -   Para **Conectar ao Assinante**, selecione **Pela representação da conta do processo**.  

         Depois de definir as configurações de segurança da conexão, clique em **OK** para salvá-las e clique em **Próximo**.  

    7.  Na página **Agenda de sincronização** , na caixa de listagem **Agenda do Agente** , selecione **Definir agendamento**e configure a **Nova Agenda de Trabalho**. Defina a frequência para ocorrer **Diariamente**, a cada **5 minuto(s)**, e a duração para **Sem data de término**. Clique em **Próximo** para salvar o agendamento e clique em **Próximo** novamente.  

    8.  Na página **Ações do assistente** , marque a caixa de seleção para **Criar a(s) assinatura(s)**e clique em **Próximo**.  

    9. Na página **Concluir o assistente** , clique em **Concluir**e em **Fechar** para concluir o assistente.  

3.  Imediatamente após a conclusão do Assistente para Nova Assinatura, use o **SQL Server Management Studio** para se conectar ao banco de dados de servidor de réplica e executar a consulta a seguir para habilitar a propriedade de banco de dados TRUSTWORTHY:  `ALTER DATABASE <MP Replica Database Name> SET TRUSTWORTHY ON;`  

4.  Examinar o status de sincronização para validar que a assinatura foi bem-sucedida:  

    -   No computador do assinante:  

        -   Use o **SQL Server Management Studio**para conectar-se ao servidor de réplica de banco de dados e expanda **Replicação**.  

        -   Expanda **Assinaturas Locais**, clique com o botão direito na publicação do banco de dados do site e selecione **Exibir Status da Sincronização**.  

    -   No computador do publicador:  

        -   Em **SQL Server Management Studio**, conecte-se ao computador do banco de dados do site, clique com o botão direito na pasta **Replicação** e selecione **Iniciar o Replication Monitor**.  

5.  Para habilitar a integração de Common Language Runtime (CLR) para a réplica de banco de dados, use o **SQL Server Management Studio** para conectar-se à réplica de banco de dados no servidor de réplica de banco de dados e execute o seguinte procedimento armazenado como uma consulta: **exec sp_configure 'clr enabled', 1; RECONFIGURE WITH OVERRIDE**  

6.  Para cada ponto de gerenciamento que usa um servidor de réplica de banco de dados, adicione essa conta de computador dos pontos de gerenciamento ao grupo local **Administradores** nesse servidor de réplica de banco de dados.  

    > [!TIP]  
    >  Esta etapa não é necessária um ponto de gerenciamento executado no servidor de réplica de banco de dados.  

 Agora a réplica de banco de dados está pronta para usar um ponto de gerenciamento.  

###  <a name="BKMK_DBReplica_ConfigMP"></a> Etapa 3 – configurar os pontos de gerenciamento para usar a réplica de banco de dados  
 Você pode configurar um ponto de gerenciamento em um site primário para usar uma réplica de banco de dados quando você instalar a função do ponto de gerenciamento ou pode reconfigurar um ponto de gerenciamento existente para usar uma réplica de banco de dados.  

 Use as informações a seguir para configurar um ponto de gerenciamento para usar uma réplica de banco de dados:  

-   **Para configurar um novo ponto de gerenciamento:** Na página **Banco de Dados do Ponto de Gerenciamento** do assistente usado para instalar o ponto de gerenciamento, selecione **Usar uma réplica de banco de dados**e especifique o FQDN do computador que hospeda a réplica de banco de dados. Em seguida, para **Nome do banco de dados do site do ConfigMgr**, especifique o nome do banco de dados da réplica de banco de dados nesse computador.  

-   **Para configurar um ponto de gerenciamento instalado anteriormente**: Abra a página de propriedades do ponto de gerenciamento, selecione a guia **Banco de Dados do Ponto de Gerenciamento** , selecione **Use uma réplica de banco de dados**e especifique o FQDN do computador que hospeda a réplica de banco de dados. Em seguida, para **Nome do banco de dados do site do ConfigMgr**, especifique o nome do banco de dados da réplica de banco de dados nesse computador.  

-   **Para cada ponto de gerenciamento que usa uma réplica de banco de dados**, você deve adicionar manualmente a conta de computador do servidor do ponto de gerenciamento para a função **db_datareader** da réplica de banco de dados.  

Além de configurar o ponto de gerenciamento para usar o servidor de réplica de banco de dados, você deve habilitar a **Autenticação do Windows** no **IIS** no ponto de gerenciamento:  

1.  Abra o **Gerenciador do IIS (Serviços de Informações da Internet)**.  

2.  Selecione o site da Web usado pelo ponto de gerenciamento e abra **Autenticação**.  

3.  Defina a **Autenticação do Windows** como **Habilitada**e feche o **Gerenciador do IIS (Serviços de Informações da Internet)**.  

###  <a name="BKMK_DBReplica_Cert"></a> Etapa 4 – configurar um certificado autoassinado para o servidor de réplica de banco de dados  
 Você deve criar um certificado autoassinado no servidor de réplica de banco de dados e disponibilizar esse certificado para cada ponto de gerenciamento que usará esse servidor.  

 O certificado está disponível automaticamente para um ponto de gerenciamento instalado no servidor de réplica de banco de dados. No entanto, para disponibilizar esse certificado para pontos de gerenciamento remoto, você deve exportá-lo e adicioná-lo ao repositório de certificados de pessoas confiáveis no ponto de gerenciamento remoto.  

 Use os procedimentos a seguir como um exemplo de como configurar o certificado autoassinado no servidor de réplica de banco de dados para um computador Windows Server 2008 R2. Se você tiver uma versão diferente de sistema operacional, consulte a documentação do sistema operacional e ajuste as etapas nesses procedimentos conforme necessário.  

##### <a name="to-configure-a-self-signed-certificate-for-the-database-replica-server"></a>Para configurar um certificado autoassinado para o servidor de réplica de banco de dados  

1.  No servidor de réplica de banco de dados, abra um prompt de comando do PowerShell com privilégios administrativos e execute o seguinte comando: **set-executionpolicy UnRestricted**  

2.  Copie o script do PowerShell a seguir e salve-o com um arquivo com o nome **CreateMPReplicaCert.ps1**. Coloque uma cópia desse arquivo na pasta raiz da partição do sistema do servidor de réplica de banco de dados.  

    > [!IMPORTANT]  
    >  Se você estiver configurando mais de uma réplica de banco de dados em um único SQL Server, para cada réplica subsequente que você configurar, use uma versão modificada do script para esse procedimento. Consulte  [Script complementar para réplicas de banco de dados adicionais em um único SQL Server](#bkmk_supscript)  

    ```  
    # Script for creating a self-signed certificate for the local machine and configuring SQL Server to use it.  

    Param($SQLInstance)  

    $ConfigMgrCertFriendlyName = "ConfigMgr SQL Server Identification Certificate"  

    # Get local computer name  
    $computerName = "$env:computername"  

    # Get the sql server name  
    #$key="HKLM:\SOFTWARE\Microsoft\SMS\MP"  
    #$value="SQL Server Name"  
    #$sqlServerName= (Get-ItemProperty $key).$value  
    #$dbValue="Database Name"  
    #$sqlInstance_DB_Name= (Get-ItemProperty $key).$dbValue  

    $sqlServerName = [System.Net.Dns]::GetHostByName("localhost").HostName   
    $sqlInstanceName = "MSSQLSERVER"  
    $SQLServiceName = "MSSQLSERVER"  

    if ($SQLInstance -ne $Null)  
    {  
        $sqlInstanceName = $SQLInstance  
        $SQLServiceName = "MSSQL$" + $SQLInstance  
    }  

    # Delete existing cert if one exists  
    function Get-Certificate($storename, $storelocation)  
    {   
        $store=new-object System.Security.Cryptography.X509Certificates.X509Store($storename,$storelocation)   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Certificates   
    }   

    $cert = Get-Certificate "My" "LocalMachine" | ?{$_.FriendlyName -eq $ConfigMgrCertFriendlyName}   
    if($cert -is [Object])  
    {  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()  

        # Remove this cert from Trusted People too...  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("TrustedPeople","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()      
    }  

    # Create the new cert  
    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"  
    $name.Encode("CN=" + $sqlServerName, 0)  

    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"  
    $key.ProviderName = "Microsoft RSA SChannel Cryptographic Provider"  
    $key.KeySpec = 1  
    $key.Length = 1024  
    $key.SecurityDescriptor = "D:PAI(A;;0xd01f01ff;;;SY)(A;;0xd01f01ff;;;BA)(A;;0x80120089;;;NS)"  
    $key.MachineContext = 1  
    $key.Create()  

    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"  
    $serverauthoid.InitializeFromValue("1.3.6.1.5.5.7.3.1")  
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"  
    $ekuoids.add($serverauthoid)  
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"  
    $ekuext.InitializeEncode($ekuoids)  

    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"  
    $cert.InitializeFromPrivateKey(2, $key, "")  
    $cert.Subject = $name  
    $cert.Issuer = $cert.Subject  
    $cert.NotBefore = get-date  
    $cert.NotAfter = $cert.NotBefore.AddDays(3650)  
    $cert.X509Extensions.Add($ekuext)  
    $cert.Encode()  

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"  
    $enrollment.InitializeFromRequest($cert)  
    $enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"  
    $certdata = $enrollment.CreateRequest(0x1)  
    $enrollment.InstallResponse(0x2, $certdata, 0x1, "")  

    # Add this cert to the trusted peoples store  
    [Byte[]]$bytes = [System.Convert]::FromBase64String($certdata)  

    $trustedPeople = new-object System.Security.Cryptography.X509certificates.X509Store "TrustedPeople", "LocalMachine"  
    $trustedPeople.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)  
    $trustedPeople.Add([Security.Cryptography.X509Certificates.X509Certificate2]$bytes)  
    $trustedPeople.Close()  

    # Get thumbprint from cert  
    $sha = new-object System.Security.Cryptography.SHA1CryptoServiceProvider  
    $certHash = $sha.ComputeHash($bytes)  
    $certHashCharArray = "";  
    $certThumbprint = "";  

    # Format the bytes into a hexadecimal string  
    foreach($byte in $certHash)  
    {  
        $temp = ($byte | % {"{0:x}" -f $_}) -join ""  
        $temp = ($temp | % {"{0,2}" -f $_})  
        $certHashCharArray = $certHashCharArray+ $temp;  
    }  
    $certHashCharArray = $certHashCharArray.Replace(' ', '0');  

    # SQL needs the thumbprint in lower case  
    foreach($char in $certHashCharArray)  
    {  
        [System.String]$myString = $char;  
        $certThumbprint = $certThumbprint + $myString.ToLower();  
    }  

    # Configure SQL to use this cert  
    $path = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL"  
    $subKey = (Get-ItemProperty $path).$sqlInstanceName  
    $realPath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\" + $subKey + "\MSSQLServer\SuperSocketNetLib"  
    $certKeyName = "Certificate"  
    Set-ItemProperty -path $realPath -name $certKeyName -Type string -Value $certThumbprint  

    # restart sql service  
    Restart-Service $SQLServiceName -Force  
    ```  

3.  No servidor de réplica de banco de dados, execute o seguinte comando que se aplica à configuração do seu SQL Server:  

    -   Para uma instância padrão do SQL Server: Clique com o botão direito no arquivo **CreateMPReplicaCert.ps1** e selecione **Executar com o PowerShell**. Quando o script é executado, ele cria o certificado autoassinado e configura o SQL Server para usar o certificado.  

    -   Para uma instância nomeada do SQL Server: Use o PowerShell para executar o comando **%path%\CreateMPReplicaCert.ps1 xxxxxx** em que **xxxxxx** é o nome da instância do SQL Server.  

    -   Depois que o script for concluído, verifique se o SQL Server Agent está sendo executado. Se não estiver, reinicie o SQL Server Agent.  

##### <a name="to-configure-remote-management-points-to-use-the-self-signed-certificate-of-the-database-replica-server"></a>Para configurar os pontos de gerenciamento remoto para usar o certificado autoassinado do servidor de réplica de banco de dados  

1.  Execute as seguintes etapas no servidor de réplica de banco de dados para exportar o certificado autoassinado do servidor:  

    1.  Clique em **Iniciar**e, em seguida, em **Executar**e digite **mmc.exe**. No console vazio, clique em **Arquivo**e em **Adicionar/Remover Snap-in**.  

    2.  Na caixa de diálogo **Adicionar ou Remover Snap-ins** , selecione **Certificados** na lista de **Snap-ins disponíveis**e clique em **Adicionar**.  

    3.  Na caixa de diálogo **Snap-in de certificado** , selecione **Conta de computador**e clique em **Próximo**.  

    4.  Na caixa de diálogo **Selecionar Computador** , verifique se a opção **Computador local: (o computador no qual este console está sendo executado)** está marcada e clique em **Concluir**.  

    5.  Na caixa de diálogo **Adicionar ou Remover Snap-ins** , clique em **OK**.  

    6.  No console, expanda **Certificados (computador local)**e, em seguida, **Pessoal**e selecione **Certificados**.  

    7.  Clique com o botão direito do mouse no certificado de nome amigável **Certificado de Identificação de SQL Server do ConfigMgr**, clique em **Todas as Tarefas**e, em seguida, selecione **Exportar**.  

    8.  Conclua o **Assistente para Exportação de Certificados** usando as opções padrão e salve o certificado com a extensão de nome de arquivo **.cer** .  

2.  Execute as seguintes etapas no computador do ponto de gerenciamento para adicionar o certificado autoassinado relativo ao servidor de réplica de banco de dados ao repositório de certificados Pessoas Confiáveis no ponto de gerenciamento:  

    1.  Repita que as etapas anteriores, de 1.a até 1.e para configurar o MMC do snap-in do **Certificado** no computador do ponto de gerenciamento.  

    2.  No console, expanda **Certificados (computador local)**e, em seguida, **Pessoas Confiáveis**; clique com o botão direito do mouse em **Certificados**, selecione **Todas as Tarefas**e, depois, **Importar** para iniciar o **Assistente para Importação de Certificados**.  

    3.  Na página **Arquivo a Ser Importado** , selecione o certificado salvo na etapa 1.h e clique em **Próximo**.  

    4.  Na página **Repositório de Certificados** , selecione **Colocar todos os certificados no repositório a seguir**com o **Repositório de certificados** definido como **Pessoas Confiáveis**; clique em **Próximo**.  

    5.  Clique em **Concluir** para fechar o assistente e concluir a configuração do certificado no ponto de gerenciamento.  

###  <a name="BKMK_DBreplica_SSB"></a> Etapa 5 – configurar o SQL Server Service Broker para o servidor de réplica de banco de dados  
Para dar suporte à notificação do cliente com uma réplica de banco de dados para um ponto de gerenciamento, você deve configurar a comunicação entre o servidor de banco de dados do site e o servidor de réplica de banco de dados no SQL Server Service Broker. Para tanto, é necessário configurar cada banco de dados com informações sobre o outro banco de dados e trocar os certificados entre os dois bancos de dados, para comunicação segura.  

> [!NOTE]  
>  Para que o procedimento a seguir seja possível, o servidor de réplica de banco de dados deve concluir com êxito a sincronização inicial com o servidor de banco de dados do site.  

 O procedimento a seguir não modifica a porta do Service Broker que está configurada no SQL Server para o servidor de banco de dados do site ou para o servidor de réplica de banco de dados. Em vez disso, ele configura cada banco de dados para comunicação com o outro banco de dados usando a porta correta do Service Broker.  

 Use o procedimento a seguir para configurar o Service Broker para o servidor de banco de dados do site e o servidor de réplica de banco de dados.  

##### <a name="to-configure-the-service-broker-for-a-database-replica"></a>Para configurar o Service Broker para uma réplica de banco de dados  

1.  Use o **SQL Server Management Studio** para conectar-se ao banco de dados do servidor de réplica e execute a consulta a seguir para habilitar o Service Broker no servidor de réplica de banco de dados: **ALTER DATABASE &lt;Nome do banco de dados de réplica\> SET ENABLE_BROKER, HONOR_BROKER_PRIORITY ON WITH ROLLBACK IMMEDIATE**  

2.  Em seguida, no servidor de réplica de banco de dados, configure o Service Broker para notificação do cliente e exporte o certificado do Service Broker. Para tanto, execute um procedimento armazenado do SQL Server que configura o Service Broker e exporta o certificado em uma única ação. Ao executar o procedimento armazenado, você deve especificar o FQDN do servidor de réplica de banco de dados, o nome do banco de dados das réplicas e especificar o local para a exportação do arquivo de certificado.  

     Execute a consulta a seguir para configurar os detalhes necessários no servidor de réplica de banco de dados e para exportar o certificado para o servidor de réplica de banco de dados: **EXEC sp_BgbConfigSSBForReplicaDB "&lt;FQDN do SQL Server de réplica\>", "&lt;Nome do banco de dados de réplica\>", "&lt;Caminho do arquivo de backup do certificado\>"**  

    > [!NOTE]  
    >  Se o servidor de réplica de banco de dados não estiver na instância padrão do SQL Server, será necessário especificar, nesta etapa, o nome da instância, além do nome do banco de dados de réplica. Para isso, substitua o **&lt;Nome do banco de dados de réplica\>** pelo **&lt;Nome da instância\\Nome do banco de dados de réplica\>**.  

     Após exportar o certificado do servidor de réplica de banco de dados, coloque uma cópia do certificado no servidor do banco de dados dos sites primários.  

3.  Use o **SQL Server Management Studio** para conectar-se ao banco de dados do site primário. Feita a conexão, execute uma consulta para importar o certificado e especifique a porta do Service Broker que está em uso no servidor de réplica de banco de dados, o FQDN do servidor de réplica e o nome do banco de dados das réplicas de banco de dados. Isso configura o banco de dados dos sites primários para usar o Service Broker para comunicação com o banco de dados do servidor de réplica de banco de dados.  

     Execute a consulta a seguir para importar o certificado do servidor de réplica do banco de dados e especificar os detalhes necessários: **EXEC sp_BgbConfigSSBForRemoteService 'REPLICA', “&lt;Porta do SQL Service Broker\>”, “&lt;Caminho do arquivo de certificado\>”, “&lt;FQDN do SQL Server de réplica\>”, “&lt;Nome do banco de dados de réplica\>”**  

    > [!NOTE]  
    >  Se o servidor de réplica de banco de dados não estiver na instância padrão do SQL Server, será necessário especificar, nesta etapa, o nome da instância, além do nome do banco de dados de réplica. Para isso, substitua o **&lt;Nome do banco de dados de réplica\>** pelo **\Nome da instância\\Nome do banco de dados de réplica\>**.  

4.  Em seguida, no servidor de banco de dados do site, execute o comando a seguir para exportar o certificado para esse servidor: **EXEC sp_BgbCreateAndBackupSQLCert “&lt;Caminho do arquivo de backup do certificado\>”**  

     Após exportar o certificado do servidor de banco de dados do site, coloque uma cópia do certificado no servidor de réplica de banco de dados.  

5.  Use o **SQL Server Management Studio** para conectar-se ao banco de dados do servidor de réplica de banco de dados. Feita a conexão, execute uma consulta para importar o certificado e especificar o código do site primário e a porta do Service Broker que está em uso no servidor de banco de dados do site. Isso configura o servidor de réplica de banco de dados para usar o Service Broker para comunicação com o banco de dados do site primário.  

     Execute a consulta a seguir para importar o certificado do servidor de banco de dados do site: **EXEC sp_BgbConfigSSBForRemoteService “&lt;Código do site\>”,”&lt;Porta do SQL Service Broker\>”, “&lt;Caminho do arquivo de certificado\>”**  

 Alguns minutos após concluir a configuração do banco de dados do site e do banco de dados de réplica do banco de dados, o gerenciador de notificações no site primário definirá a conversa do Service Broker para notificação do cliente, do banco de dados do site primário para a réplica de banco de dados.  

###  <a name="bkmk_supscript"></a> Script complementar para réplicas de banco de dados adicionais em um único SQL Server  
 Quando você usar o script da etapa 4 para configurar um certificado autoassinado para o servidor de réplica de banco de dados em um SQL Server que já tenha uma réplica de banco de dados que você planeje continuar usando, use uma versão modificada do script original. As seguintes modificações impedem que o script exclua um certificado existente no servidor e criam certificados subsequentes com nomes amigáveis exclusivos.  Edite o script original da seguinte maneira:  

-   Comente (impeça a execução) cada linha entre as entradas de script **# Excluir certificado existente se houver** e **# Criar o novo certificado**. Para fazer isso, adicione um  **#**  como o primeiro caractere de cada linha aplicável.  

-   Para cada réplica de banco de dados subsequentes que use esse script para configurar, atualize o nome amigável do certificado.  Para fazer isso, edite a linha **$enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"** e substitua **ConfigMgr SQL Server Identification Certificate** por um novo nome, como  **ConfigMgr SQL Server Identification Certificate1**.  

##  <a name="BKMK_DBReplicaOps"></a> Gerenciar configurações de réplica de banco de dados  
 Ao usar réplica de banco de dados em um site, observe as informações das seções abaixo para suplementar o processo executado para desinstalar uma réplica, desinstalar um site que use réplica de banco de dados ou mover o banco de dados do site para uma nova instalação de SQL Server. Ao usar as informações das seções abaixo para excluir publicações, siga as diretrizes para excluir a replicação transacional da versão de SQL Server utilizada para a réplica de banco de dados. Por exemplo, se você usar o SQL Server 2008 R2, veja [Como: Excluir uma publicação (programação Transact-SQL de replicação)](http://go.microsoft.com/fwlink/p/?LinkId=273934).  

> [!NOTE]  
>  Após restaurar o banco de dados do site que estava configurado para as réplicas de banco de dados, reconfigure cada réplica para poder usá-las, recriando as publicações e assinaturas.  

###  <a name="BKMK_UninstallDbReplica"></a> Desinstalar uma réplica de banco de dados  
 Quando se usa réplica de banco de dados para um ponto de gerenciamento, pode ser preciso desinstalar a réplica por determinado tempo e, depois, reconfigurá-la para uso. Por exemplo, é necessário remover as réplicas de banco de dados para poder atualizar um site do Configuration Manager para um novo service pack. Após a atualização do site, você pode restaurar a réplica de banco de dados para uso.  

 Siga as etapas abaixo para desinstalar uma réplica de banco de dados.  

1.  No espaço de trabalho de **Administração** do console do Configuration Manager, expanda **Configuração de Site** e selecione **Funções de Servidores e Sistema de Sites**; no painel de detalhes, selecione o servidor do sistema de sites que hospeda o ponto de gerenciamento que usa a réplica de banco de dados que você vai desinstalar.  

2.  No painel **Funções do Sistema de Site** , clique com o botão direito do mouse em **Ponto de gerenciamento** e selecione **Propriedades**.  

3.  Na guia **Banco de Dados do Ponto de Gerenciamento** , selecione **Usar o banco de dados do site** para configurar o ponto de gerenciamento de modo a usar o banco de dados do site, em vez da réplica de banco de dados. Em seguida, clique em **OK** para salvar a configuração.  

4.  Em seguida, use o **SQL Server Management Studio** para executar as seguintes tarefas:  

    -   Exclua, do banco de dados do servidor do site, a publicação da réplica de banco de dados.  

    -   Exclua, do servidor de réplica de banco de dados, a assinatura da réplica.  

    -   Exclua, do servidor de réplica de banco de dados, o banco de dados de réplica.  

    -   Desabilite a publicação e a distribuição no servidor de banco de dados do site. Para desabilitar a publicação e a distribuição, clique com o botão direito do mouse na pasta Replicação e, depois, clique em **Desabilitar Publicação e Distribuição**.  

5.  Após a exclusão da publicação, da assinatura e do banco de dados de réplica e a desabilitação da publicação no servidor de banco de dados do site, a réplica de banco de dados estará desinstalada.  

###  <a name="BKMK_DBReplicaOps_Uninstall"></a> Desinstalar um servidor do site que publique uma réplica de banco de dados  
 Antes de desinstalar um site que publique uma réplica de banco de dados, siga as etapas abaixo para limpar a publicação e eventuais assinaturas.  

1.  Use o **SQL Server Management Studio** para excluir, do banco de dados do servidor do site, a publicação da réplica de banco de dados.  

2.  Use o **SQL Server Management Studio** para excluir a assinatura da réplica de banco de dados de cada SQL Server remoto que hospede uma réplica de banco de dados desse site.  

3.  Desinstale o site.  

###  <a name="BKMK_DBReplicaOps_Move"></a> Mover um banco de dados de servidor de site que publique uma réplica de banco de dados  
 Ao mover o banco de dados do site para um novo computador, siga estas etapas:  

1.  Use o **SQL Server Management Studio** para excluir, do banco de dados do servidor do site, a publicação da réplica de banco de dados.  

2.  Use o **SQL Server Management Studio** para excluir a assinatura da réplica de banco de dados de cada servidor de réplica desse site.  

3.  Mova o banco de dados para o novo computador SQL Server. Para obter mais informações, consulte a seção [Modify the site database configuration](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) no tópico [Modify your System Center Configuration Manager infrastructure](../../../../core/servers/manage/modify-your-infrastructure.md) .  

4.  Recrie a publicação da réplica de banco de dados no servidor de banco de dados do site. Para obter mais informações, consulte [Etapa 1 – configurar o servidor de banco de dados do site para publicar a réplica de banco de dados](#BKMK_DBReplica_ConfigSiteDB) neste tópico.  

5.  Recrie as assinaturas da réplica de banco de dados em cada servidor de réplica. Para obter mais informações, consulte [Etapa 2 – configurando o servidor de réplica de banco de dados](#BKMK_DBReplica_ConfigSrv) neste tópico.  
