---
title: "Verificações de pré-requisitos | System Center Configuration Manager"
description: "Veja as verificações de pré-requisitos disponíveis para o System Center Configuration Manager. Inclui verificações de direitos de segurança."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
caps.latest.revision: 12
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 96787d5c4ad92d86ad9172fcfacb92fe4138c7ba


---
# <a name="list-of-prerequisite-checks-for-system-center-configuration-manager"></a>Lista de verificações de pré-requisitos para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As seções a seguir detalham as verificações de pré-requisitos disponíveis.  


 Para obter informações sobre o uso do Verificador de Pré-requisitos, consulte [Verificador de Pré-requisitos](prerequisite-checker.md).  

##  <a name="a-namebkmksecuritya-prerequisite-checks-for-security-rights"></a><a name="BKMK_Security"></a> Verificações de pré-requisitos de Direitos de Segurança  
 Os pré-requisitos a seguir verificam se o Verificador de Pré-requisitos é executado a fim de verificar os direitos de segurança.  

 **Direitos de administrador no site de administração central** – verifica se a conta de usuário que executa a Instalação do Configuration Manager tem direitos de **Administrador** local no computador do site de administração central.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  
      -   Site primário  

**Direitos administrativos no site primário de expansão** – verifica se o usuário que está executando a Instalação tem direitos de **Administrador** local sobre o site primário autônomo que será expandido.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central  

**Direitos administrativos no sistema de site** – verifica se a conta de usuário que executa a Instalação do Configuration Manager tem direitos de **Administrador** local no computador do servidor do site.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central  
    -   Site primário  
    -   Site secundário  

**Direitos administrativos do Computador CAS no site primário de expansão** – verifica se a conta do computador do site de administração central tem direitos de **Administrador** local no site primário autônomo que será expandido.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central  

**Conexão ao SQL Server no site de administração central** – verifica se a conta de usuário que executa a Instalação do Configuration Manager no site primário para ingressar em uma hierarquia existente tem a função **sysadmin** na instância do SQL Server para o site de administração central.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site primário  

**Direitos administrativos da conta de computador do servidor do site** – verifica se a conta de computador do servidor do site tem direitos administrativos no SQL Server e em computadores do ponto de gerenciamento.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site primário  
    -   SQL Server  

**Comunicação do Sistema de Site com o SQL Server** – verifica se um SPN (Nome da Entidade de Serviço) está registrado no Active Directory Domain Services para a conta configurada para executar o serviço SQL Server da instância do SQL Server usada para hospedar o banco de dados do site do Configuration Manager. Um SPN válido deve ser registrado nos Serviços de Domínio do Active Directory para oferecer suporte à autenticação Kerberos.  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Site secundário  
    -   Ponto de gerenciamento  

**Modo de segurança do SQL Server** – verifica se o SQL Server está configurado para segurança de autenticação do Windows.  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   SQL Server  

**Direitos de sysadmin do SQL Server** – verifica se a conta de usuário que executa a Instalação do Configuration Manager tem a função **sysadmin** na instância do SQL Server selecionada para instalação do banco de dados do site. Essa verificação também falha quando a Instalação não puder acessar a instância do SQL Server para verificar as permissões.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   SQL Server  

**Direitos de sysadmin do SQL Server para site de referência** – verifica se a conta de usuário que está executando a Instalação do Configuration Manager tem a função **sysadmin** na instância de função do SQL Server selecionada como banco de dados do site de referência.  As permissões da função **sysadmin** do SQL Server são necessárias para modificar o banco de dados do site.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   SQL Server  

##  <a name="a-namebkmkdependenciesa-prerequisite-checks-for-configuration-manager-dependencies"></a><a name="BKMK_Dependencies"></a> Verificações de pré-requisitos de dependências do Configuration Manager  
 A seguir, temos as verificações de pré-requisitos que o Verificador de Pré-requisitos realiza para as dependências do Configuration Manager.  

**Mapeamentos de migração ativos no site primário de destino**  

 Verifica se não há mapeamentos de migração ativos em sites primários.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central  

**Réplica Ativa do MP** – verifica se há uma réplica do ponto de gerenciamento ativo.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site primário  

**Direitos administrativos no ponto de distribuição** – verifica se o usuário que está executando a Instalação tem direitos de **Administrador** local no computador do ponto de distribuição.  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Ponto de distribuição  

**Direitos administrativos no ponto de gerenciamento** –  verifica se a conta de computador do servidor do site tem direitos de **Administrador** no computador do ponto de gerenciamento e do ponto de distribuição.  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Ponto de gerenciamento  

**Compartilhamento administrativo (Sistema de site)** – verifica se os compartilhamentos administrativos necessários estão presentes no computador do sistema de sites.  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Ponto de gerenciamento  

**Compatibilidade do aplicativo** – verifica se os aplicativos atuais são compatíveis com o esquema do aplicativo.  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário  

**BITS habilitado** – verifica se o BITS (Serviço de Transferência Inteligente em Segundo Plano) está instalado no computador do sistema de sites do ponto de gerenciamento. Quando essa verificação falha, o BITS não é instalado, o componente de compatibilidade do IIS 6 WMI do IIS7 não é instalado no computador ou no host de IIS remoto, ou a Instalação não foi capaz de verificar as configurações remotas do IIS porque os componentes comuns do IIS não foram instalados no computador do servidor do site.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Ponto de gerenciamento  

**BITS instalado** – verifica se o BITS (Serviço de Transferência Inteligente em Segundo Plano) está instalado nos IIS (Serviços de Informações da Internet).  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Ponto de gerenciamento  

**Agrupamento que não diferencia maiúsculas de minúsculas no SQL Server** – verifica se a instalação do SQL Server usa um agrupamento que não diferencia maiúsculas de minúsculas, por exemplo, SQL_Latin1_General_CP1_CI_AS.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   SQL Server  

**Verificar o site primário autônomo existente quanto à versão e ao código do site** – verifica se o site primário que você pretende expandir é um site primário autônomo e se tem a mesma versão do Configuration Manager, mas com um código de site diferente do site de administração central que será instalado.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário  

**Verificar referências de coleção incompatíveis** – durante uma atualização, esta verificação avalia se as coleções fazem referência apenas a outras coleções do mesmo tipo.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central  

**Versão do cliente no computador do ponto de gerenciamento** – verifica se você está instalando o ponto de gerenciamento em um computador que não tem uma versão diferente do cliente do Configuration Manager instalado.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Ponto de gerenciamento  

**Configuração do uso de memória do SQL Server** – verifica se o SQL Server está configurado para uso ilimitado de memória. Você deve configurar a memória do SQL Server para ter um limite máximo.  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   SQL Server  

**Instância dedicada do SQL Server** – verifica se uma instância dedicada do SQL Server está configurada para hospedar o banco de dados do site do Configuration Manager. Se outro site usa a instância, selecione uma instância diferente para o novo site usar. Como alternativa, você pode desinstalar o outro site ou mover seu banco de dados para uma instância diferente do SQL Server.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário    
    -   Site secundário  

**Componentes de servidor do Configuration Manager existentes no servidor** – verifica se uma função de servidor do site ou sistema de sites ainda não está instalada no computador selecionado para instalação do site.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário    
    -   Site secundário  

**Exceção de firewall do SQL Server** – verifica se o Firewall do Windows está desabilitado ou se existe uma exceção do Firewall do Windows relevante para o SQL Server. Você deve permitir que o sqlservr.exe ou as portas TCP necessárias possam ser acessadas remotamente. Por padrão, o SQL Server escuta a porta TCP 1433 e o SQL Broker Service usa a porta TCP 4022.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário    
    -   Site secundário    
    -   Ponto de gerenciamento  

**Exceção de firewall do SQL Server (site primário autônomo)** – verifica se o Firewall do Windows está desabilitado ou se existe exceção relevante do Firewall do Windows para o SQL Server. Você deve permitir que o sqlservr.exe ou as portas TCP necessárias possam ser acessadas remotamente. Por padrão, o SQL Server escuta a porta TCP 1433 e o SQL Broker Service usa a porta TCP 4022.  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Site primário (autônomo apenas)  

**Exceção de firewall para o SQL Server do ponto de gerenciamento** – verifica se o Firewall do Windows está desabilitado ou se existe exceção relevante do Firewall do Windows para o SQL Server.  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Ponto de gerenciamento  

**Configuração HTTPS do IIS** – verifica as associações de site do IIS (Serviços de Informações da Internet) do protocolo de comunicação HTTPS. Ao optar por instalar funções de site que exijam HTTPS, você deve configurar as ligações de site da Web do IIS no servidor especificado com um certificado PKI válido.  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Ponto de gerenciamento    
    -   Ponto de distribuição  

**Serviço IIS em execução** – verifica se o IIS (Serviços de Informações da Internet) está instalado e em execução no computador para instalar o ponto de gerenciamento ou o ponto de distribuição.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Ponto de gerenciamento    
    -   Ponto de distribuição  

**Associar Agrupamento do site primário de expansão** – verifica se o banco de dados de site do site primário autônomo que você vai expandir tem o mesmo agrupamento que o banco de dados do site no site de administração central.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central  

**Biblioteca de RDC (Compactação Diferencial Remota) da Microsoft registrada** – verifica se a Biblioteca de RDC (Compactação Diferencial Remota) da Microsoft está registrada no servidor do site do Configuration Manager.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário    
    -   Site secundário  

**Microsoft Windows Installer** – verifica a versão do Windows Installer. Quando essa verificação falha, a Instalação não pôde verificar a versão ou a versão instalada não atende ao requisito mínimo do Windows Installer versão 4.5.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário    
    -   Site secundário  

**Microsoft XML Core Services 6.0 (MSXML60)** – verifica se o Microsoft Core XML Services (MSXML) 6.0, ou uma versão mais recente, está instalado no computador.  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário    
    -   Site secundário    
    -   Console do Configuration Manager    
    -   Ponto de gerenciamento    
    -   Ponto de distribuição  

**Versão mínima do .NET Framework para console do Configuration Manager** – verifica se o Microsoft .NET Framework versão 4.0 está instalado no computador do console do Configuration Manager. É possível baixar a versão 4.0 do Microsoft .NET Framework por meio do [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=189149).  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Console do Configuration Manager  

**Versão mínima do .NET Framework do servidor do site do Configuration Manager** – verifica se o Microsoft .NET Framework versão 3.5 está instalado no servidor do site do Configuration Manager. Para o Windows Server 2008, é possível baixar o Microsoft .NET Framework versão 3.5 no [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=185604). Para o Windows Server 2008 R2, você pode habilitar o Microsoft .NET Framework versão 3.5 como um recurso do Gerenciador do Servidor.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário    
    -   Site secundário  

**A versão mínima do .NET Framework para instalação do SQL Server Express Edition para o Site Secundário do Configuration Manager** – verifica se o Microsoft .NET Framework versão 4.0 está instalado em computadores de site secundário do Configuration Manager para instalação da edição do SQL Server Express.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site secundário  

**Agrupamento de banco de dados pai/filho** – verifica se o agrupamento do banco de dados do site corresponde ao agrupamento de banco de dados do site pai. Todos os sites em uma hierarquia devem usar o mesmo agrupamento de banco de dados.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site primário    
    -   Site secundário  

**PowerShell 2.0 no servidor do site** – verifica se o Windows PowerShell versão 2.0 ou posterior está instalado no servidor do site do Exchange Connector do Configuration Manager. Para obter mais informações sobre o PowerShell 2.0, consulte o [Artigo 968930](http://go.microsoft.com/fwlink/p/?LinkId=226450) na Base de Dados de Conhecimento Microsoft.  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Site primário  

**FQDN primário** – verifica se o nome NetBIOS do computador corresponde ao nome do host local (primeiro rótulo no FQDN) do computador.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário    
    -   Site secundário    
    -   SQL Server  

**Conexão Remota com WMI no Site Secundário** – verifica se a Instalação pode estabelecer uma conexão remota com o WMI no servidor do site secundário.  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Site secundário  

**Agrupamento do SQL Server Necessário** – verifica se a instância do SQL Server e o banco de dados do site do Configuration Manager, se estiver instalado, estão configurados para usar o agrupamento SQL_Latin1_General_CP1_CI_AS, a menos que você esteja usando um sistema operacional chinês que exija suporte de GB18030.  

 Para obter informações sobre como alterar seus agrupamentos de bancos de dados e instância do SQL Server, consulte [Configurar e Alterar Agrupamentos](http://go.microsoft.com/fwlink/p/?LinkID=234541) nos Manuais Online do SQL Server 2008 R2.  Para obter informações sobre como habilitar o suporte para GB18030, consulte [Suporte internacional no System Center Configuration Manager](../../../../core/plan-design/hierarchy/international-support.md).  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário    
    -   Site secundário  

**Pasta de Origem da Instalação** – verifica se a conta do computador do site secundário tem as permissões do sistema de arquivos NTFS de **Leitura** e permissões de compartilhamento de **Leitura** para a pasta de origem e compartilhamento da Instalação.  

> [!NOTE]  
>  A conta do computador do site secundário deve ser de um administrador no computador se você usa compartilhamentos administrativos (por exemplo, C$ e D$).  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site secundário  

**Versão de Origem da Instalação** – verifica se a versão do Configuration Manager na pasta de origem especificada para a instalação do site secundário deve corresponder à versão do Configuration Manager site primário.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site secundário  

**Código de site em uso** – verifica se o código do site especificado ainda não está em uso na hierarquia do Configuration Manager. Você deve especificar um código de site exclusivo para este site.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site primário  

**O computador Provedor de SMS tem o mesmo domínio do servidor de site** – verifica se o computador que executa uma instância do Provedor de SMS tem o mesmo domínio do servidor do site.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Provedor de SMS  

**Edição do SQL Server** – verifica se a edição do SQL Server no site não é o SQL Server Express.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   SQL Server  

**SQL Server Express no Site Secundário** – verifica se o SQL Server Express pode ser instalado com êxito no computador do servidor do site para um site secundário.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site secundário  

**SQL Server no Computador de Site Secundário** – verifica se o SQL Server está instalado no computador do site secundário. Não há suporte para instalação do SQL Server no sistema de site remoto.  

> [!WARNING]  
>  Esta seleção se aplica somente quando você seleciona para que a Instalação use uma instância existente do SQL Server.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site secundário  

**Alocação de memória de processo do SQL Server** – verifica se o SQL Server reserva um mínimo de 8 GB de memória para o site de administração central e site primário, e um mínimo de 4 GB de memória para o site secundário. Para obter mais informações sobre como definir uma quantidade fixa de memória usando o SQL Server Management Studio, veja [Como: Definir uma quantidade fixa de memória (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759).  

> [!NOTE]  
>  Esta seleção não se aplica ao SQL Server Express em um site secundário, limitado a 1 GB de memória reservada  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   SQL Server  

**Conta executando o serviço do SQL Server** – verifica se a conta de logon do serviço SQL Server não é uma conta de usuário local ou LOCAL SERVICE. Você deve configurar o serviço SQL Server para usar uma conta de domínio válida, NETWORK SERVICE ou LOCAL SYSTEM.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário    
    -   Site secundário  

**Porta Tcp do SQL Server** – verifica se TCP está habilitado para o SQL Server e configurado para usar uma porta estática.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   SQL Server  

**Versão do SQL Server** – verifica se há uma versão com suporte do SQL Server instalada no servidor de banco de dados do site especificado. Para obter mais informações, consulte [Suporte para versões do SQL Server para o System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   SQL Server  

**Versão do sistema operacional do site sem suporte para atualização** – durante uma atualização, esta regra verifica se as funções do sistema de sites, além dos pontos de distribuição, estão instaladas nos computadores que executam o Windows Server 2008 ou anterior.  

> [!NOTE]  
>  Como essa verificação não pode resolver o status das funções do sistema de sites instaladas no Azure ou no armazenamento em nuvem usado pelo Microsoft Intune quando você integra o Intune ao Configuration Manager, você pode considerar os avisos para essas funções como falsos positivos e ignorá-los.  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Site primário    
    -   Site secundário  

**Função do sistema de site 'Ponto de sincronização do Asset Intelligence' sem suporte no site primário expandido** – verifica se a função do sistema de sites do ponto de sincronização do Asset Intelligence não está instalada no site primário autônomo que você está expandindo.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central  

**A função do sistema de site 'Ponto do Endpoint Protection' não tem suporte no site primário expandido** – verifica se a função do sistema de sites ponto do Endpoint Protection não está instalada no site primário autônomo que você está expandindo.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central  

<a name="-head"></a><<<<<<< HEAD
=======

>>>>>>> 5e8e486ea74f66a92696c65e3367aec2e592b001 **A função do sistema de site 'Conector do Microsoft Intune' não tem suporte no site primário expandido** – verifica se a função “Conector do Microsoft Intune” do sistema de sites não está instalada no site primário autônomo que você está expandindo.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central  

**USMT (Ferramenta de Migração do Usuário) instalada** – verifica se o componente USMT (Ferramenta de Migração do Usuário) do ADK (Kit de Avaliação e Implantação) do Windows 8.1 foi instalado.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário (autônomo apenas)  

**Validar o FQDN do Computador SQL Server** – verifica se o FQDN especificado para o computador do SQL Server é válido.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   SQL Server  

**Verificar a Versão do Site de Administração Central** – verifica se o site de administração central tem a mesma versão do Configuration Manager.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site primário  

**Verifique as permissões do servidor do site para publicar no Active Directory** – verifica se a conta de computador do servidor do site tem permissões de **Controle Total** no contêiner de **Gerenciamento do Sistema** no domínio do Active Directory. Para obter mais informações sobre as opções de configuração das permissões necessárias, consulte [Estender o esquema do Active Directory para o System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md).  

> [!NOTE]  
>  Você poderá ignorar este aviso se tiver verificado manualmente essas permissões.  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário    
    -   Site secundário  

**Windows Deployment Tools instalado** – verifica se o componente Windows Deployment Tools do Windows do ADK (Kit de Avaliação e Implantação) do Windows 10 foi instalado.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Provedor de SMS  

**Cluster de Failover do Windows** – verifica se os computadores que têm ponto de gerenciamento ou ponto de distribuição não fazem parte de um Cluster do Windows.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Ponto de gerenciamento    
    -   Ponto de distribuição  

**Ambiente de Pré-Instalação do Windows instalado** – verifica se o componente do Ambiente de Pré-Instalação do ADK (Kit de Avaliação e Implantação) do Windows 10 foi instalado.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Provedor de SMS  

**Windows Remote Management (WinRM) v1.1** – verifica se o WinRM v1.1 está instalado no servidor do site primário ou no computador console do Configuration Manager para executar o console de gerenciamento fora da banda. Para obter mais informações sobre como baixar o WinRM 1.1, consulte o [Artigo 936059](http://go.microsoft.com/fwlink/p/?LinkId=247166) na Base de Dados de Conhecimento Microsoft.  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Site primário    
    -   Console do Configuration Manager  

**WSUS no servidor do site** – verifica se o WSUS (Windows Server Update Services) versão 3.0 Service Pack 2 está instalado no servidor do site. Ao usar um ponto de atualização de software em um computador diferente do servidor do site, instale primeiro o Console de Administração do WSUS no servidor do site. Para obter mais informações sobre o WSUS, consulte a página da Web do [Windows Server Update Services](http://go.microsoft.com/fwlink/p/?LinkID=79477) .  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário  

##  <a name="a-namebkmkrequirementsa-prerequisite-checks-for-system-requirements"></a><a name="BKMK_Requirements"></a> Verificações de pré-requisitos de requisitos do sistema  
 Veja a seguir as verificações de pré-requisitos que o Verificador de Pré-requisitos executa para requisitos de sistema.  

**Verificação do Nível Funcional do Domínio do Active Directory** – verifica se o nível funcional do domínio do Active Directory é, no mínimo, o Windows Server 2008 R2.  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário  

**Verifique se o Serviço do Servidor está em execução** – verifica se o Serviço do Servidor foi iniciado.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário    
    -   Site secundário  

**Associação do domínio** – verifica se o computador do Configuration Manager é membro de um domínio do Windows.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário    
    -   Site secundário    
    -   Provedor SMS    
    -   SQL Server  

**Associação do domínio** – verifica se o computador do Configuration Manager é membro de um domínio do Windows.  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Ponto de gerenciamento    
    -   Ponto de distribuição  

**Unidade FAT no Servidor do Site** – verifica se a unidade de disco foi formatada com o sistema de arquivos FAT. Instale componentes do servidor do site em unidades de disco formatadas com o sistema de arquivos NTFS para aumentar segurança.  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Site primário  

**Espaço livre em disco no servidor do site** – o computador do servidor do site deve ter pelo menos 5 GB de espaço livre em disco para instalar o servidor do site. É necessário ter mais 1 GB de espaço livre para instalar a função do sistema de site do Provedor de SMS no mesmo computador.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário    
    -   Site secundário  

**Reinicialização do sistema pendente** – verifica se outro programa exige que o servidor seja reiniciado antes de executar a Instalação.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário    
    -   Site secundário  
    -   Console do Configuration Manager    
    -   Provedor de SMS    
    -   SQL Server    
    -   Ponto de gerenciamento    
    -   Ponto de distribuição  

**Controlador de domínio somente leitura** – não há suporte para servidores de banco de dados de site e servidores de site secundário em um RODC (controlador de domínio somente leitura). Para obter mais informações, consulte [Você pode encontrar problemas ao instalar o SQL Server em um controlador de domínio](http://go.microsoft.com/fwlink/p/?LinkId=264856) na Base de Dados de Conhecimento Microsoft.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário    
    -   Site secundário  

**Extensões do esquema** – determina se o esquema do Active Directory Domain Services foi estendido; em caso afirmativo, a versão das extensões de esquema que foram usadas. As extensões de esquema do Active Directory Configuration Manager não são obrigatórias para a instalação do servidor do site, mas são recomendadas para dar suporte total ao uso de todos os recursos do Configuration Manager. Para obter mais informações sobre as vantagens de estender o esquema, consulte [Estender o esquema do Active Directory para o System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md).  

-   **Severidade:** Aviso  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário  

**Comprimento do FQDN do servidor do site** – verifica o comprimento do FQDN do computador do servidor do site.  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário    
    -   Site secundário  

**Sistema operacional do console do Configuration Manager sem suporte** – verifica se os consoles do Configuration Manager podem ser instalados em computadores que executam uma versão do sistema operacional com suporte. Para obter mais informações, consulte [Sistemas operacionais com suporte para consoles do System Center Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-consoles).  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Console do Configuration Manager  

**Versão do sistema operacional do servidor do site sem suporte para a Instalação** – verifica se um sistema operacional com suporte está em execução no servidor. Para obter mais informações, consulte [Sistemas operacionais com suporte para sites e clientes para o System Center Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário    
    -   Site secundário    
    -   Console do Configuration Manager    
    -   Ponto de gerenciamento    
    -   Ponto de distribuição  

**Verificar consistência de banco de dados** – a partir da versão 1602, esta verificação avalia a consistência do banco de dados  

-   **Severidade:** Erro  

-   **Aplicabilidade:**  

    -   Site de administração central    
    -   Site primário  



<!--HONumber=Nov16_HO1-->


