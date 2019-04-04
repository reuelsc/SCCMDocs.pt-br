---
title: Verificações de pré-requisitos
titleSuffix: Configuration Manager
description: Referência das verificações de pré-requisito específicos para atualizações do Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 81689907f326399de704b075b8500b82803b4d3d
ms.sourcegitcommit: d8d142044586a53709b4478ad945f714737c8d6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58524176"
---
# <a name="list-of-prerequisite-checks-for-configuration-manager"></a>Lista de verificações de pré-requisitos para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo fornece detalhes sobre as verificações de pré-requisitos que são executados quando você instala ou atualiza o Configuration Manager. Para obter informações, veja [Verificador de pré-requisitos](/sccm/core/servers/deploy/install/prerequisite-checker).  



##  Direitos de segurança <a name="BKMK_Security"></a>  


### <a name="security-rights-errors"></a>Direitos de segurança: Erros

#### <a name="administrator-rights-on-central-administration-site"></a>Direitos de administrador sobre o site de administração central 
*Aplica-se a: Site primário*

A conta de usuário que executa a Instalação do Configuration Manager tem direitos de **Administrador** no servidor do site de administração central.

#### <a name="administrative-rights-on-expand-primary-site"></a>Direitos administrativos sobre o site primário de expansão 
*Aplica-se a: Site de administração central*

Quando você expande um site primário para uma hierarquia, a conta de usuário que executa a instalação tem direitos de **Administrador** no servidor do site primário autônomo.

#### <a name="administrative-rights-on-site-system"></a>Direitos administrativos sobre o sistema do site 
*Aplica-se a: Site de administração central, site primário, site secundário*

A conta de usuário que executa a Instalação do Configuration Manager tem direitos de **Administrador** no servidor do site.

#### <a name="central-administration-site-server-administrative-rights-on-expand-primary-site"></a>Direitos administrativos de servidor do site de administração central sobre expandir site primário 
*Aplica-se a: Site de administração central*

Quando você expande um site primário para uma hierarquia, a conta de computador do servidor do site de administração central tem direitos de **Administrador** no servidor do site primário autônomo.

#### <a name="connection-to-sql-server-on-central-administration-site"></a>Conexão ao SQL Server no site de administração central 
*Aplica-se a: Site primário*

A conta de usuário que executa a Instalação do Configuration Manager no site primário para associar a uma hierarquia existente tem a função **sysadmin** na instância do SQL Server para o site de administração central.

#### <a name="site-server-computer-account-administrative-rights"></a>Direitos administrativos da conta de computador do servidor do site 
*Aplica-se a: Site primário, servidor de banco de dados do site*

A conta de computador do servidor do site tem direitos de **Administrador** sobre o SQL Server e ponto de gerenciamento.

#### <a name="sql-server-sysadmin-rights"></a>Direitos sysadmin do SQL Server 
*Aplica-se a: Servidor de banco de dados do site*

A conta de usuário que executa a Instalação do Configuration Manager tem a função **sysadmin** na instância do SQL Server selecionada para instalação do banco de dados do site. Essa verificação também falha quando a configuração não pode acessar a instância do SQL Server para verificar as permissões.

#### <a name="sql-server-sysadmin-rights-for-reference-site"></a>Direitos sysadmin do SQL Server para site de referência 
*Aplica-se a: Servidor de banco de dados do site*

A conta de usuário que executa a Instalação do Configuration Manager tem a função **sysadmin** na instância de função do SQL Server selecionada como o banco de dados do site de referência. As permissões da função **sysadmin** do SQL Server são necessárias para modificar o banco de dados do site.


### <a name="security-rights-warnings"></a>Direitos de segurança: Avisos

#### <a name="site-system-to-sql-server-communication"></a>Comunicação do Sistema de sites com o SQL Server  
*Aplica-se a: Site secundário, ponto de gerenciamento*

A conta que você configurou para executar o serviço do SQL Server para a instância de banco de dados do site tem um SPN (nome da entidade de serviço) válido nos Active Directory Domain Services. Registre um SPN válido no Active Directory para dar suporte à autenticação Kerberos.

#### <a name="sql-server-security-mode"></a>Modo de segurança do SQL Server 
*Aplica-se a: Servidor de banco de dados do site*

O SQL Server está configurado para segurança de autenticação do Windows.



##  <a name="BKMK_Dependencies"></a> Dependências

### <a name="dependencies-errors"></a>Dependências: Erros

#### <a name="active-migration-mappings-on-the-target-primary-site"></a>Mapeamentos de migração ativos no site primário de destino 
*Aplica-se a: Site de administração central*

Não há mapeamentos de migração ativos em sites primários.

#### <a name="active-replica-mp"></a>Réplica do ponto de gerenciamento ativo 
*Aplica-se a: Site primário*

Há uma réplica do ponto de gerenciamento ativo.

#### <a name="bits-enabled"></a>Habilitado para BITS 
*Aplica-se a: Ponto de gerenciamento*

O BITS (Serviço de Transferência Inteligente em Segundo Plano) é instalado no ponto de gerenciamento. Essa verificação pode falhar por um dos seguintes motivos: 
- BITS não está instalado  
- O componente de compatibilidade do WMI do IIS 6.0 para o IIS 7.0 não está instalado no servidor ou host remoto do IIS  
- A instalação não pôde verificar as configurações de IIS remotas. Os componentes comuns do IIS não estão instalados no servidor do site.  

#### <a name="case-insensitive-collation-on-sql-server"></a>Ordenação que não diferencia maiúsculas de minúsculas no SQL Server 
*Aplica-se a: Servidor de banco de dados do site*

A instalação do SQL Server usa ordenação que não diferencia maiúsculas de minúsculas, por exemplo, **SQL_Latin1_General_CP1_CI_AS**.

#### <a name="check-existing-stand-alone-primary-site-for-version-and-site-code"></a>Verificar o site primário autônomo existente quanto à versão e ao código do site 
*Aplica-se a: Site de administração central, site primário*

O site primário que você planeja expandir é um site primário autônomo. Ele tem a mesma versão do Configuration Manager, mas um código do site diferente que o site de administração central a ser instalado.

#### <a name="check-for-incompatible-collection-references"></a>Verificar referências de coleções incompatíveis 
*Aplica-se a: Site de administração central*

Durante uma atualização, as coleções fazem referência somente a outras coleções do mesmo tipo.

#### <a name="client-version-on-management-point-computer"></a>Versão do cliente no computador do ponto de gerenciamento 
*Aplica-se a: Ponto de gerenciamento*

Você está instalando o ponto de gerenciamento em um servidor que não tem uma versão diferente do cliente do Configuration Manager instalado.

#### <a name="dedicated-sql-server-instance"></a>Instância dedicada do SQL Server 
*Aplica-se a: Site de administração central, site primário, site secundário*

Você configurou uma instância dedicada do SQL Server para hospedar o banco de dados do site do Configuration Manager. 

Se outro site usar a instância, selecione uma instância diferente para o novo site. Como alternativa, você também pode desinstalar o outro site ou mover seu banco de dados para uma instância diferente do SQL Server.

#### <a name="existing-configuration-manager-server-components-on-server"></a>Componentes de servidor do Configuration Manager existentes no servidor 
*Aplica-se a: Site de administração central, site primário, site secundário*

Um servidor do site ou função do sistema de site já não está instalada no servidor selecionado para instalação do site.

#### <a name="firewall-exception-for-sql-server"></a>Exceção de firewall do SQL Server 
*Aplica-se a: Site de administração central, site primário, site secundário, ponto de gerenciamento*

O Firewall do Windows está desabilitado ou existe uma exceção relevante do Firewall do Windows relativa ao SQL Server. 

Permita que o Sqlservr.exe ou as portas TCP necessárias possam ser acessadas remotamente. Por padrão, o SQL Server escuta a porta TCP 1433 e o SQL SSB (Server Service Broker) usa a porta TCP 4022.

#### <a name="iis-service-running"></a>Serviço IIS em execução 
*Aplica-se a: Ponto de gerenciamento, ponto de distribuição*

O IIS está instalado e em execução no servidor para o ponto de gerenciamento ou ponto de distribuição.

#### <a name="match-collation-of-expand-primary-site"></a>Corresponder ordenação do site primário de expansão 
*Aplica-se a: Site de administração central*

Quando você expande um site primário para uma hierarquia, o banco de dados do site para o site primário autônomo tem a mesma ordenação que o banco de dados do site no site de administração central.

#### <a name="microsoft-remote-differential-compression-rdc-library-registered"></a>Biblioteca de RDC (Compactação Diferencial Remota da Microsoft) registrada 
*Aplica-se a: Site de administração central, site primário, site secundário*

A biblioteca de RDC está registrada no servidor do site do Configuration Manager.

#### <a name="microsoft-windows-installer"></a>Microsoft Windows Installer 
*Aplica-se a: Site de administração central, site primário, site secundário*

Verifica a versão do Windows Installer. 

Quando essa verificação falha, a instalação não pôde verificar a versão ou a versão instalada não atende ao requisito mínimo do Windows Installer 4.5.

#### <a name="minimum-net-framework-version-for-configuration-manager-console"></a>Versão mínima do .NET Framework do console do Configuration Manager 
*Aplica-se a: Console do Configuration Manager*

O Microsoft .NET Framework 4.0 está instalado no computador do console do Configuration Manager. 

#### <a name="minimum-net-framework-version-for-configuration-manager-site-server"></a>Versão mínima do .NET Framework do servidor do site do Configuration Manager 
*Aplica-se a: Site de administração central, site primário, site secundário*

O .NET Framework 3.5 está instalado ou habilitado no servidor do site do Configuration Manager. 

#### <a name="minimum-net-framework-version-for-sql-server-express-edition-installation-for-configuration-manager-secondary-site"></a>A versão mínima do .NET Framework para instalação do SQL Server Express Edition para o site secundário do Configuration Manager 
*Aplica-se a: Site secundário*

O .NET Framework 4.0 está instalado ou habilitado no servidor do site secundário do Configuration Manager. Essa versão é exigida pelo SQL Server Express.

#### <a name="parent-database-collation"></a>Ordenação de banco de dados pai 
*Aplica-se a: Site primário, site secundário*

A ordenação do banco de dados de site corresponde à ordenação de banco de dados do site pai. Todos os sites em uma hierarquia devem usar a mesma ordenação de banco de dados.

#### <a name="primary-fqdn"></a>FQDN Primário 
*Aplica-se a: Site de administração central, site primário, site secundário, servidor de banco de dados do site*

O nome NetBIOS do computador corresponde ao nome do host local no FQDN (nome de domínio totalmente qualificado).

#### <a name="required-sql-server-collation"></a>Ordenação do SQL Server necessária 
*Aplica-se a: Site de administração central, site primário, site secundário*

A instância do SQL Server está configurada para usar a ordenação **SQL_Latin1_General_CP1_CI_AS**. 

Se o banco de dados do site do Configuration Manager já está instalado, essa verificação também se aplica ao banco de dados. Para obter informações sobre como alterar suas ordenações de bancos de dados e instância do SQL Server, veja [Ordenação SQL e suporte a Unicode](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support). 

Se você estiver usando um sistema operacional chinês e precisar de suporte para GB18030, essa verificação não se aplicará. Para obter mais informações sobre como habilitar o suporte para GB18030, veja [Suporte internacional](/sccm/core/plan-design/hierarchy/international-support).

#### <a name="setup-source-folder"></a>Pasta de origem da instalação 
*Aplica-se a: Site secundário*

A conta de computador para o site secundário tem as seguintes permissões para a pasta de origem de instalação e compartilhamento: 
- Permissões do sistema de arquivos NTFS de **Leitura**
- Permissões de compartilhamento de **Leitura** 

> [!Note]  
> Se você usa compartilhamentos administrativos, por exemplo, C$ e D$, a conta de computador de site secundário deve ser um **Administrador** no servidor.  

#### <a name="setup-source-version"></a>Versão de origem da instalação 
*Aplica-se a: Site secundário*

A versão do Configuration Manager na pasta de origem especificada para a instalação do site secundário corresponde à versão do Configuration Manager site primário.

#### <a name="site-code-in-use"></a>Código do site em uso 
*Aplica-se a: Site primário* O código do site especificado ainda não está em uso na hierarquia do Configuration Manager. Especifique um código do site exclusivo para este site.

#### <a name="sms-provider-in-same-domain-as-site-server"></a>Provedor de SMS no mesmo domínio do servidor do site 
*Aplica-se a: Provedor de SMS*

Qualquer instância do provedor de SMS está no mesmo domínio que o servidor do site.

#### <a name="sql-server-edition"></a>Edição do SQL Server 
*Aplica-se a: Servidor de banco de dados do site*

SQL Server no site não é SQL Server Express.

#### <a name="sql-server-express-on-secondary-site"></a>SQL Server Express no site secundário 
*Aplica-se a: Site secundário*

O SQL Server Express pode ser instalado com êxito no servidor do site secundário.

#### <a name="sql-server-on-the-secondary-site-server"></a>SQL Server no servidor do site secundário 
*Aplica-se a: Site secundário*

O SQL Server é instalado no servidor do site secundário. Não é possível instalar o SQL Server em um sistema de site remoto para um site secundário.

> [!Warning]  
> Esta seleção se aplica somente quando você seleciona para que a instalação use uma instância existente do SQL Server.  

#### <a name="sql-server-service-running-account"></a>Conta executando o serviço do SQL Server 
*Aplica-se a: Site de administração central, site primário, site secundário*

A conta de conexão para o serviço SQL Server não é uma conta de usuário local ou **SERVIÇO LOCAL**. 

Configure o serviço SQL Server para usar uma conta de domínio válida, **SERVIÇO DE REDE** ou **SISTEMA LOCAL**.

#### <a name="sql-server-tcp-port"></a>Porta TCP do SQL Server 
*Aplica-se a: Servidor de banco de dados do site*

O TCP está habilitado para a instância do SQL Server e está configurado para usar a porta estática.

#### <a name="sql-server-version"></a>Versão do SQL Server 
*Aplica-se a: Servidor de banco de dados do site*

Uma versão com suporte do SQL Server instalada no servidor de banco de dados do site especificado. 

Para obter mais informações, veja [Suporte a versões do SQL Server](/sccm/core/plan-design/configs/support-for-sql-server-versions).

#### <a name="asset-intelligence-synchronization-point-on-the-expanded-primary-site"></a>Ponto de sincronização do Asset Intelligence no site primário expandido 
*Aplica-se a: Site de administração central*

Quando você expande um site primário para uma hierarquia, a função de ponto de sincronização do Asset Intelligence não é instalada no site primário autônomo.

#### <a name="endpoint-protection-point-on-the-expanded-primary-site"></a>Ponto do Endpoint Protection no site primário expandido 
*Aplica-se a: Site de administração central*

Quando você expande um site primário para uma hierarquia, a função de ponto do Endpoint Protection não é instalada no site primário autônomo.

#### <a name="microsoft-intune-connector-on-the-expanded-primary-site"></a>Microsoft Intune Connector no site primário expandido 
*Aplica-se a: Site de administração central*

Quando você expande um site primário para uma hierarquia, a função do Microsoft Intune Connector não é instalada no site primário autônomo.

#### <a name="usmt-installed"></a>USMT instalada 
*Aplica-se a: Site de administração central, site primário (somente autônomo)*

O componente USMT (Ferramenta de Migração do Usuário) do Windows ADK (Kit de Avaliação e Implantação do Windows) do Windows foi instalado.

#### <a name="validate-fqdn-of-sql-server"></a>Validar o FQDN do SQL Server 
*Aplica-se a: Servidor de banco de dados do site*

Você especificou um FQDN válido para o computador do SQL Server.

#### <a name="verify-central-administration-site-version"></a>Verificar a versão do site de administração central 
*Aplica-se a: Site primário*

O site de administração central tem a mesma versão do Configuration Manager.

#### <a name="windows-deployment-tools-installed"></a>Windows Deployment Tools instalado 
*Aplica-se a: Provedor de SMS*

O componente Windows Deployment Tools do Windows ADK está instalado.

#### <a name="windows-failover-cluster"></a>Cluster de Failover do Windows 
*Aplica-se a: Servidor, ponto de gerenciamento, ponto de distribuição*

Servidor com servidor do site, ponto de gerenciamento ou funções de ponto de distribuição não fazem parte de um Cluster do Windows.

Da versão 1810 em diante, o processo de instalação do Configuration Manager não bloqueia mais a instalação da função de servidor de site em um computador com a função do Windows para clustering de failover. O Always On do SQL requer essa função; portanto, anteriormente não era possível colocar o banco de dados do site no servidor do site. Com essa alteração, é possível criar um site altamente disponível com menos servidores usando o Always On do SQL e um servidor do site no modo passivo. Para obter mais informações, confira [Opções de alta disponibilidade](/sccm/core/servers/deploy/configure/high-availability-options). <!--1359132-->  

#### <a name="windows-pe-installed"></a>Windows PE instalado 
*Aplica-se a: Provedor de SMS*

O componente PE (Ambiente de Pré-Instalação) do Windows ADK está instalado.


### <a name="dependencies-warnings"></a>Dependências: Avisos

#### <a name="administrative-rights-on-distribution-point"></a>Direitos administrativos no ponto de distribuição 
*Aplica-se a: Ponto de distribuição*

A conta de usuário que está executando a instalação tem direitos de **Administrador** no ponto de distribuição.

#### <a name="administrative-rights-on-management-point"></a>Direitos administrativos no ponto de gerenciamento 
*Aplica-se a: Ponto de gerenciamento, ponto de distribuição*

A conta de computador do servidor do site tem direitos de **Administrador** no ponto de gerenciamento e do ponto de distribuição.

#### <a name="administrative-share-site-system"></a>Compartilhamento administrativo (sistema de sites) 
*Aplica-se a: Ponto de gerenciamento*

Os compartilhamentos administrativos necessários estão presentes no computador do sistema de site.

#### <a name="application-compatibility"></a>Compatibilidade do aplicativo 
*Aplica-se a: Site de administração central, site primário*

Os aplicativos atuais estão em conformidade com o esquema do aplicativo.

#### <a name="bits-installed"></a>BITS instalado 
*Aplica-se a: Ponto de gerenciamento*

O BITS (Serviço de Transferência Inteligente em Segundo Plano) está instalado e habilitado no IIS.

#### <a name="configuration-for-sql-server-memory-usage"></a>Configuração do uso de memória do SQL Server 
*Aplica-se a: Servidor de banco de dados do site*

O SQL Server está configurado para uso ilimitado de memória. Configure a memória do SQL Server para ter um limite máximo.

#### <a name="firewall-exception-for-sql-server-standalone-primary-site"></a>Exceção de firewall do SQL Server (site primário autônomo) 
*Aplica-se a: Site primário (somente autônomo)*

O Firewall do Windows está desabilitado ou existe uma exceção relevante do Firewall do Windows relativa ao SQL Server. 

Permita que o Sqlservr.exe ou as portas TCP necessárias possam ser acessadas remotamente. Por padrão, o SQL Server escuta na porta TCP 1433 e o SSB (Server Service Broker) usa a porta TCP 4022.

#### <a name="firewall-exception-for-sql-server-for-management-point"></a>Exceção de firewall do SQL Server do ponto de gerenciamento 
*Aplica-se a: Ponto de gerenciamento*

O Firewall do Windows está desabilitado ou existe uma exceção relevante do Firewall do Windows relativa ao SQL Server.

#### <a name="iis-https-configuration"></a>Configuração de IIS HTTPS 
*Aplica-se a: Ponto de gerenciamento, ponto de distribuição*

O site IIS tem associações para o protocolo de comunicação HTTPS. 

Ao instalar funções de site que exijam HTTPS, configure as ligações de site do IIS no servidor especificado com um certificado PKI (infraestrutura de chave pública) válido.

#### <a name="microsoft-xml-core-services-60-msxml60"></a>Microsoft XML Core Services 6.0 (MSXML60) 
*Aplica-se a site de administração central, site primário, site secundário, console do Configuration Manager, ponto de gerenciamento, ponto de distribuição*

Verifica se o MSXML 6.0 ou uma versão mais recente está instalado.

#### <a name="powershell-20-on-site-server"></a>PowerShell 2.0 no servidor do site 
*Aplica-se a: Site primário com o conector do Exchange*

O Windows PowerShell 2.0 ou uma versão posterior está instalada no servidor do site do Exchange Connector do Configuration Manager. 

#### <a name="remote-connection-to-wmi-on-secondary-site"></a>Conexão remota com WMI no site secundário 
*Aplica-se a: Site secundário*

A instalação pode estabelecer uma conexão remota com WMI no servidor do site secundário.

#### <a name="sql-server-process-memory-allocation"></a>Alocação de memória de processo do SQL Server 
*Aplica-se a: Servidor de banco de dados do site* 

O SQL Server reserva um mínimo de 8 GB de memória para o site de administração central e site primário e um mínimo de 4 GB de memória para o site secundário.

Para obter mais informações, veja [Como configurar opções de memória usando o SQL Server Management Studio](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options#how-to-configure-memory-options-using-includessmanstudiofullincludesssmanstudiofull-mdmd).

> [!NOTE]  
> Essa verificação não é aplicável ao SQL Server Express em um site secundário. Esta edição é limitada a 1 GB de memória reservada.  

#### <a name="unsupported-site-system-os-version-for-upgrade"></a>Versão de sistema operacional do sistema de site sem suporte para atualização 
*Aplica-se a: Site primário, site secundário*

Funções do sistema de site além dos pontos de distribuição são instaladas em servidores que executam o Windows Server 2012 ou posterior.

Para obter mais informações, confira [Sistemas operacionais com suporte para servidores de sistema de sites do Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).

> [!NOTE]  
> Essa verificação não pode resolver o status das funções de sistema de sites instaladas no Azure ou para o armazenamento em nuvem usado pelo Microsoft Intune. Ignore os avisos para essas funções como falsos positivos.

#### <a name="verify-site-server-permissions-to-publish-to-active-directory"></a>Verifique as permissões do servidor do site para publicar no Active Directory 
*Aplica-se a: Site de administração central, site primário, site secundário*

A conta de computador do servidor do site tem permissões de **Controle Total** no contêiner do **System Management** no domínio do Active Directory. 

Para obter mais informações, consulte [Preparar o Active Directory para publicação de sites](/sccm/core/plan-design/network/extend-the-active-directory-schema).

> [!NOTE]  
> Se você verificar as permissões manualmente, poderá ignorar este aviso.

#### <a name="windows-remote-management-winrm-v11"></a>Gerenciamento Remoto do Windows (WinRM) v1.1 
*Aplica-se a: Site primário, console do Configuration Manager*

O WinRM 1.1 está instalado no servidor do site primário ou no computador console do Configuration Manager para executar o console de gerenciamento fora da banda. 

Para obter mais informações sobre como baixar o WinRM 1.1, confira o [Artigo de suporte 936059](https://support.microsoft.com/help/936059).

#### <a name="wsus-on-site-server"></a>WSUS no servidor do site 
*Aplica-se a: Site de administração central, site primário*

Uma versão com suporte do WSUS (Windows Server Update Services) é instalada no servidor do site. 

Ao usar um ponto de atualização de software em um servidor que não o servidor do site, instale primeiro o Console de Administração do WSUS no servidor do site. Para obter mais informações sobre o WSUS, consulte [Windows Server Update Services](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus).

#### <a name="pending-configuration-item-policy-updates"></a>Atualizações de política do item de configuração pendentes 
<!--SCCMDocs-pr issue 2814-->
*Aplica-se a: Site primário*

Da versão 1806 em diante, se você estiver atualizando da versão 1706 ou posterior, você poderá ver esse aviso se você tiver muitas implantações de aplicativo e pelo menos uma delas exigir aprovação. 

Você tem duas opções:  

- Ignorar o aviso e continuar com a atualização. Essa ação gera maior processamento no servidor do site durante a atualização conforme ela processa as políticas. Você também poderá ver o mais carga sobre o processador no ponto de gerenciamento após a atualização.  

- Revisar um dos aplicativos que não tem requisitos ou um requisito de SO específico. Pré-processe uma parte da carga no servidor do site nesse momento. Examine **objreplmgr.log** e, em seguida, monitore o processador no ponto de gerenciamento. Depois que o processamento for concluído, atualize o site. Ainda haverá algum processamento adicional após a atualização, mas será menor do que se você ignorar o aviso com a primeira opção.  



##  <a name="BKMK_Requirements"></a> Requisitos do sistema  

### <a name="system-requirements-errors"></a>Requisitos do sistema: Erros

#### <a name="server-service-is-running"></a>Serviço do Servidor está em execução 
*Aplica-se a: Site de administração central, site primário, site secundário*

O serviço do Servidor foi iniciado e está em execução.

#### <a name="domain-membership"></a>Associação do domínio 
*Aplica-se a: Site de administração central, site primário, site secundário, Provedor de SMS, SQL Server*

O computador do Configuration Manager é membro de um domínio do Windows.

#### <a name="free-disk-space-on-site-server"></a>Espaço livre em disco no servidor do site 
*Aplica-se a: Site de administração central, site primário, site secundário*

Para instalar o servidor do site, ele deve ter pelo menos 15 GB de espaço livre em disco. Se você instalar o Provedor de SMS no mesmo servidor, ele precisará de mais 1 GB de espaço livre.

#### <a name="pending-system-restart"></a>Reinicialização do sistema pendente 
*Aplica-se a: Site de administração central, site primário, site secundário*

Antes de executar a instalação, outro programa exige que o servidor seja reiniciado.

Da versão 1810 em diante, essa verificação é mais resiliente. Para ver se o computador está em um estado de reinicialização pendente, ela verifica os seguintes locais do registro:<!--SCCMDocs-pr issue 3010-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  
- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  
- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  
- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

#### <a name="read-only-domain-controller"></a>Controlador de domínio somente leitura 
*Aplica-se a: Site de administração central, site primário, site secundário*

Não há suporte para servidores de banco de dados de sites e servidores de sites secundários em um controlador de domínio somente leitura (RODC). 

Para obter mais informações, consulte o artigo do Suporte da Microsoft sobre [Problemas ao instalar o SQL Server em um controlador de domínio](https://support.microsoft.com/help/2032911).

#### <a name="site-server-fqdn-length"></a>Comprimento do FQDN do Servidor do Site 
*Aplica-se a: Site de administração central, site primário, site secundário*

O comprimento do FQDN do servidor do site.

#### <a name="unsupported-os-for-configuration-manager-console"></a>Sistema operacional sem suporte para o console do Configuration Manager
*Aplica-se a: Console do Configuration Manager*

Instale o console do Configuration Manager em computadores que executam uma versão de sistema operacional com suporte. 

Para obter mais informações, confira [Versões do sistema operacional com suporte para o console do Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-consoles).

#### <a name="unsupported-os-for-site-server"></a>Sistema operacional sem suporte para servidor do site 
*Aplica-se a: Site de administração central, site primário, site secundário, console do Configuration Manager, ponto de gerenciamento, ponto de distribuição*

O servidor executa uma versão de sistema operacional com suporte. 

Para obter mais informações, confira [versões de sistemas operacionais com suporte para servidores de sistema de sites do Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).

#### <a name="verify-database-consistency"></a>Verificar consistência de banco de dados 
*Aplica-se a: Site de administração central, site primário*

Verifica a consistência do banco de dados do site no SQL Server.  


### <a name="system-requirements-warnings"></a>Requisitos do sistema: Avisos

#### <a name="active-directory-domain-functional-level"></a>Nível funcional do domínio do Active Directory 
*Aplica-se a: Site de administração central, site primário*

O nível funcional do Domínio do Active Directory é, no mínimo, de Windows Server 2008 R2.

#### <a name="domain-membership"></a>Associação do domínio 
*Aplica-se a: Ponto de gerenciamento, ponto de distribuição*

O computador do Configuration Manager é membro de um domínio do Windows.

#### <a name="ntfs-drive-on-site-server"></a>Unidade NTFS no servidor do site 
*Aplica-se a: Site primário*

A unidade de disco é formatada com o sistema de arquivos NTFS. Para aumentar a segurança, instale componentes do servidor do site em unidades de disco formatadas com o sistema de arquivos NTFS.

#### <a name="pending-system-restart-on-the-remote-sql-server"></a>Reinicialização do sistema pendente no servidor SQL remoto
*Aplica-se a: Versão 1902 e posterior, SQL Server remoto*

Antes de executar a instalação, outro programa exige que o servidor seja reiniciado.

Para ver se o computador está em um estado de reinicialização pendente, ela verifica os seguintes locais do registro:<!--SCCMDocs-pr issue 3377-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  
- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  
- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  
- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

#### <a name="schema-extensions"></a>Extensões de esquema 
*Aplica-se a: Site de administração central, site primário*

O esquema do Active Directory foi estendido. Se ele tiver estendido, a versão das extensões de esquema que foram usadas. 

O Configuration Manager não requer extensões de esquema do Active Directory para a instalação de servidor do site. A Microsoft as recomenda para o uso completo de todos os recursos do Configuration Manager. Para obter mais informações sobre as vantagens de estender o esquema, consulte [Preparar o Active Directory para publicação de sites](/sccm/core/plan-design/network/extend-the-active-directory-schema).

#### <a name="bkmk_changetracking"></a> Limpeza do controle de alterações do SQL
*Aplica-se a: Servidor de banco de dados do site*

A partir da versão 1810, verifique se o banco de dados do site tem uma lista de pendências de dados de controle de alterações do SQL.<!--SCCMDocs-pr issue 3023-->  

Verifique manualmente essa verificação executando um procedimento armazenado de diagnóstico no banco de dados do site. Primeiro, crie uma [conexão de diagnóstico](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators?view=sql-server-2017) para seu banco de dados do site. O método mais fácil é usar o Editor de Consultas do Mecanismo de Banco de Dados do SQL Server Management Studio e se conectar ao `admin:<instance name>`. 

Em uma janela de consulta da conexão de administrador dedicada, execute os seguintes comandos:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking
```

Dependendo do tamanho do banco de dados e da lista de pendências, esse procedimento armazenado pode executar em alguns minutos ou várias horas. Quando a consulta for concluída, você verá duas seções de dados relacionadas à lista de pendências. Primeiro, examine **CT_Days_Old**. Esse valor informa a idade (dias) da entrada mais antiga em sua tabela syscommittab. Deve ter cinco dias, que é o valor padrão do Configuration Manager. Não altere esse valor padrão. Em momentos de processamento ou replicação de dados intenso, a entrada mais antiga no syscommittab pode ter mais de cinco dias. Se esse valor estiver acima de sete dias, execute uma limpeza manual de dados de controle de alterações.  

Para limpar os dados de controle de alterações, execute o seguinte comando em uma conexão de administração dedicada: 

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking @CleanupChangeTracking = 1
```

Esse comando inicia uma limpeza de syscommittab e todas as tabelas secundárias associadas. Pode ser executado em vários minutos ou várias horas. Para monitorar o progresso, consulte a exibição **vLogs**. Para ver o progresso atual, execute a consulta a seguir: 

```SQL
SELECT * FROM vLogs WHERE ProcedureName = 'spDiagChangeTracking'
```

#### <a name="sql-native-client"></a>SQL Native Client
<!--SCCMDocs-pr issue 3094-->
*Aplica-se a: Site de administração central, site primário, site secundário*

Quando você instala um novo site, o Configuration Manager instala automaticamente o SQL Server Native Client como um componente redistribuível. Depois que o site é instalado, o Configuration Manager não atualizará o SQL Server Native Client. Essa verificação garante que o site tem uma versão compatível do SQL Native Client. Começando na versão 1810, a versão mínima é SQL 2012 SP4 (`11.*.7001.0`). 

Esta versão do SQL Native Client dá suporte a TLS 1.2. Para obter mais informações, consulte os seguintes artigos:
- [Suporte ao TLS 1.2 para o Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)  
- [Como habilitar o TLS 1.2 para o Configuration Manager](https://support.microsoft.com/help/4040243/how-to-enable-tls-1-2-for-configuration-manager)  
