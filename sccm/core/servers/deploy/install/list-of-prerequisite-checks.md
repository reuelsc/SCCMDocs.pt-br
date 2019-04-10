---
title: Verificações de pré-requisitos
titleSuffix: Configuration Manager
description: Referência das verificações de pré-requisito específicos para atualizações do Configuration Manager.
ms.date: 04/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 50c613e30304dc9208dfd8bf6d0fd3e5afb41ff2
ms.sourcegitcommit: deb28cdc95a456d4a38499ef1bc71e765ef6dc13
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2019
ms.locfileid: "58901478"
---
# <a name="list-of-prerequisite-checks-for-configuration-manager"></a>Lista de verificações de pré-requisitos para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo fornece detalhes sobre as verificações de pré-requisitos que são executados quando você instala ou atualiza o Configuration Manager. Para obter informações, veja [Verificador de pré-requisitos](/sccm/core/servers/deploy/install/prerequisite-checker).  



## <a name="errors"></a>Erros

### <a name="active-migration-mappings-on-the-target-primary-site"></a>Mapeamentos de migração ativos no site primário de destino

*Aplica-se a: Site de administração central*

Não há mapeamentos de migração ativos em sites primários.

### <a name="active-replica-mp"></a>MP de réplica ativo

*Aplica-se a: Site primário*

Há uma réplica do ponto de gerenciamento ativo.

### <a name="administrative-rights-on-expand-primary-site"></a>Direitos administrativos sobre o site primário de expansão

*Aplica-se a: Site de administração central*

Quando você expande um site primário para uma hierarquia, a conta de usuário que executa a instalação tem direitos de **Administrador** no servidor do site primário autônomo.

### <a name="administrative-rights-on-site-system"></a>Direitos administrativos sobre o sistema do site

*Aplica-se a: Site de administração central, site primário, site secundário*

A conta de usuário que executa a Instalação do Configuration Manager tem direitos de **Administrador** no servidor do site.

### <a name="administrator-rights-on-central-administration-site"></a>Direitos de administrador sobre o site de administração central

*Aplica-se a: Site primário*

A conta de usuário que executa a Instalação do Configuration Manager tem direitos de **Administrador** no servidor do site de administração central.

### <a name="asset-intelligence-synchronization-point-on-the-expanded-primary-site"></a>Ponto de sincronização do Asset Intelligence no site primário expandido

*Aplica-se a: Site de administração central*

Quando você expande um site primário para uma hierarquia, a função de ponto de sincronização do Asset Intelligence não é instalada no site primário autônomo.

### <a name="bits-enabled"></a>Habilitado para BITS

*Aplica-se a: Ponto de gerenciamento*

O BITS (Serviço de Transferência Inteligente em Segundo Plano) é instalado no ponto de gerenciamento. Essa verificação pode falhar por um dos seguintes motivos:

- BITS não está instalado  

- O componente de compatibilidade do WMI do IIS 6.0 para o IIS 7.0 não está instalado no servidor ou host remoto do IIS  

- A instalação não pôde verificar as configurações de IIS remotas. Os componentes comuns do IIS não estão instalados no servidor do site.  

### <a name="case-insensitive-collation-on-sql-server"></a>Ordenação que não diferencia maiúsculas de minúsculas no SQL Server

*Aplica-se a: Servidor de banco de dados do site*

A instalação do SQL Server usa ordenação que não diferencia maiúsculas de minúsculas, por exemplo, **SQL_Latin1_General_CP1_CI_AS**.

### <a name="central-administration-site-server-administrative-rights-on-expand-primary-site"></a>Direitos administrativos de servidor do site de administração central sobre expandir site primário

*Aplica-se a: Site de administração central*

Quando você expande um site primário para uma hierarquia, a conta de computador do servidor do site de administração central tem direitos de **Administrador** no servidor do site primário autônomo.

### <a name="client-version-on-management-point-computer"></a>Versão do cliente no computador do ponto de gerenciamento

*Aplica-se a: Ponto de gerenciamento*

Você está instalando o ponto de gerenciamento em um servidor que não tem uma versão diferente do cliente do Configuration Manager instalado.

### <a name="cloud-management-gateway-on-the-expanded-primary-site"></a>Gateway de Gerenciamento de Nuvem no site primário expandido

*Aplica-se a: Site de administração central*

Quando você expande um site primário para uma hierarquia, a função de gateway de gerenciamento de nuvem não é instalada no site primário autônomo.

### <a name="connection-to-sql-server-on-central-administration-site"></a>Conexão ao SQL Server no site de administração central

*Aplica-se a: Site primário*

A conta de usuário que executa a Instalação do Configuration Manager no site primário para associar a uma hierarquia existente tem a função **sysadmin** na instância do SQL Server para o site de administração central.

### <a name="custom-client-agent-settings-have-nap-enabled"></a>As configurações do agente cliente personalizadas têm a NAP habilitada

*Aplica-se a: Site de administração central, site primário*

Não há nenhuma configuração de cliente personalizada que habilite a NAP (Proteção de Acesso à Rede).

### <a name="data-warehouse-service-point-on-the-expanded-primary-site"></a>Ponto de serviço do data warehouse no site primário expandido

*Aplica-se a: Site de administração central*

Quando você expande um site primário para uma hierarquia, a função de ponto de serviço do data warehouse não é instalada no site primário autônomo.

### <a name="dedicated-sql-server-instance"></a>Instância dedicada do SQL Server

*Aplica-se a: Site de administração central, site primário, site secundário*

Você configurou uma instância dedicada do SQL Server para hospedar o banco de dados do site do Configuration Manager.

Se outro site usar a instância, selecione uma instância diferente para o novo site. Como alternativa, você também pode desinstalar o outro site ou mover seu banco de dados para uma instância diferente do SQL Server.

### <a name="default-client-agent-settings-have-nap-enabled"></a>As configurações do agente cliente padrão têm a NAP habilitada

*Aplica-se a: Site de administração central, site primário*

As configurações de cliente padrão não habilitam a NAP (Proteção de Acesso à Rede).

### <a name="domain-membership-error"></a>Associação do domínio (erro)

*Aplica-se a: Site de administração central, site primário, site secundário, Provedor de SMS, SQL Server*

O computador do Configuration Manager é membro de um domínio do Windows.

### <a name="endpoint-protection-point-on-the-expanded-primary-site"></a>Ponto do Endpoint Protection no site primário expandido

*Aplica-se a: Site de administração central*

Quando você expande um site primário para uma hierarquia, a função de ponto do Endpoint Protection não é instalada no site primário autônomo.

### <a name="existing-configuration-manager-server-components-on-server"></a>Componentes de servidor do Configuration Manager existentes no servidor

*Aplica-se a: Site de administração central, site primário, site secundário*

Um servidor do site ou função do sistema de site já não está instalada no servidor selecionado para instalação do site.

### <a name="existing-stand-alone-primary-site-for-version-and-site-code"></a>Site primário autônomo existente quanto à versão e ao código do site

*Aplica-se a: Site de administração central, site primário*

O site primário que você planeja expandir é um site primário autônomo. Ele tem a mesma versão do Configuration Manager, mas um código do site diferente que o site de administração central a ser instalado.

### <a name="firewall-exception-for-sql-server"></a>Exceção de firewall do SQL Server

*Aplica-se a: Site de administração central, site primário, site secundário, ponto de gerenciamento*

O Firewall do Windows está desabilitado ou existe uma exceção relevante do Firewall do Windows relativa ao SQL Server.

Permita que o Sqlservr.exe ou as portas TCP necessárias possam ser acessadas remotamente. Por padrão, o SQL Server escuta a porta TCP 1433 e o SQL SSB (Server Service Broker) usa a porta TCP 4022.

### <a name="free-disk-space-on-site-server"></a>Espaço livre em disco no servidor do site

*Aplica-se a: Site de administração central, site primário, site secundário*

Para instalar o servidor do site, ele deve ter pelo menos 15 GB de espaço livre em disco. Se você instalar o Provedor de SMS no mesmo servidor, ele precisará de mais 1 GB de espaço livre.

### <a name="iis-service-running"></a>Serviço IIS em execução

*Aplica-se a: Ponto de gerenciamento, ponto de distribuição*

O IIS está instalado e em execução no servidor para o ponto de gerenciamento ou ponto de distribuição.

### <a name="incompatible-collection-references"></a>Referências de coleções incompatíveis

*Aplica-se a: Site de administração central*

Durante uma atualização, as coleções fazem referência somente a outras coleções do mesmo tipo.

### <a name="match-collation-of-expand-primary-site"></a>Corresponder ordenação do site primário de expansão

*Aplica-se a: Site de administração central*

Quando você expande um site primário para uma hierarquia, o banco de dados do site para o site primário autônomo tem a mesma ordenação que o banco de dados do site no site de administração central.

### <a name="maximum-text-replication-size-for-sql-server-always-on-availability-groups"></a>Tamanho máximo de replicação de texto para grupos de disponibilidade Always On do SQL Server

*Aplica-se a: Servidor de banco de dados do site*

Ao usar o SQL Server Always On, a configuração de **tamanho máximo de replicação de texto** deve ser configurada corretamente. Para obter mais informações, confira [Preparar para usar os grupos de disponibilidade Always On do SQL Server com o Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

### <a name="microsoft-intune-connector-on-the-expanded-primary-site"></a>Microsoft Intune Connector no site primário expandido

*Aplica-se a: Site de administração central*

Quando você expande um site primário para uma hierarquia, a função do Microsoft Intune Connector não é instalada no site primário autônomo.

### <a name="microsoft-remote-differential-compression-rdc-library-registered"></a>Biblioteca de RDC (Compactação Diferencial Remota da Microsoft) registrada

*Aplica-se a: Site de administração central, site primário, site secundário*

A biblioteca de RDC está registrada no servidor do site do Configuration Manager.

### <a name="microsoft-windows-installer"></a>Microsoft Windows Installer

*Aplica-se a: Site de administração central, site primário, site secundário*

Verifica a versão do Windows Installer.

Quando essa verificação falha, a instalação não pôde verificar a versão ou a versão instalada não atende ao requisito mínimo do Windows Installer 4.5.

### <a name="minimum-net-framework-version-for-configuration-manager-console"></a>Versão mínima do .NET Framework do console do Configuration Manager

*Aplica-se a: Console do Configuration Manager*

O Microsoft .NET Framework 4.0 está instalado no computador do console do Configuration Manager.

### <a name="minimum-net-framework-version-for-configuration-manager-site-server"></a>Versão mínima do .NET Framework do servidor do site do Configuration Manager

*Aplica-se a: Site de administração central, site primário, site secundário*

O .NET Framework 3.5 está instalado ou habilitado no servidor do site do Configuration Manager.

### <a name="minimum-net-framework-version-for-sql-server-express-edition-installation-for-configuration-manager-secondary-site"></a>A versão mínima do .NET Framework para instalação do SQL Server Express Edition para o site secundário do Configuration Manager

*Aplica-se a: Site secundário*

O .NET Framework 4.0 está instalado ou habilitado no servidor do site secundário do Configuration Manager. Essa versão é exigida pelo SQL Server Express.

### <a name="parent-database-collation"></a>Ordenação de banco de dados pai

*Aplica-se a: Site primário, site secundário*

A ordenação do banco de dados de site corresponde à ordenação de banco de dados do site pai. Todos os sites em uma hierarquia devem usar a mesma ordenação de banco de dados.

### <a name="parent-site-replication-status"></a>Status de replicação de site pai

*Aplica-se a: Site de administração central, site primário*

O status de replicação do site pai é **Replicação ativa** (estado **125**).

### <a name="pending-system-restart"></a>Reinicialização do sistema pendente

*Aplica-se a: Site de administração central, site primário, site secundário*

Antes de executar a instalação, outro programa exige que o servidor seja reiniciado.

Da versão 1810 em diante, essa verificação é mais resiliente. Para ver se o computador está em um estado de reinicialização pendente, ela verifica os seguintes locais do registro:<!--SCCMDocs-pr issue 3010-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="primary-fqdn"></a>FQDN Primário

*Aplica-se a: Site de administração central, site primário, site secundário, servidor de banco de dados do site*

O nome NetBIOS do computador corresponde ao nome do host local no FQDN (nome de domínio totalmente qualificado).

### <a name="read-only-domain-controller"></a>Controlador de domínio somente leitura

*Aplica-se a: Site de administração central, site primário, site secundário*

Não há suporte para servidores de banco de dados de sites e servidores de sites secundários em um controlador de domínio somente leitura (RODC).

Para obter mais informações, consulte o artigo do Suporte da Microsoft sobre [Problemas ao instalar o SQL Server em um controlador de domínio](https://support.microsoft.com/help/2032911).

### <a name="required-sql-server-collation"></a>Ordenação do SQL Server necessária

*Aplica-se a: Site de administração central, site primário, site secundário*

A instância do SQL Server está configurada para usar a ordenação **SQL_Latin1_General_CP1_CI_AS**.

Se o banco de dados do site do Configuration Manager já está instalado, essa verificação também se aplica ao banco de dados. Para obter informações sobre como alterar suas ordenações de bancos de dados e instância do SQL Server, veja [Ordenação SQL e suporte a Unicode](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support).

Se você estiver usando um sistema operacional chinês e precisar de suporte para GB18030, essa verificação não se aplicará. Para obter mais informações sobre como habilitar o suporte para GB18030, veja [Suporte internacional](/sccm/core/plan-design/hierarchy/international-support).

### <a name="server-service-is-running"></a>Serviço do Servidor está em execução

*Aplica-se a: Site de administração central, site primário, site secundário*

O serviço do Servidor foi iniciado e está em execução.

### <a name="setup-source-folder"></a>Pasta de origem da instalação

*Aplica-se a: Site secundário*

A conta de computador para o site secundário tem as seguintes permissões para a pasta de origem de instalação e compartilhamento:

- Permissões do sistema de arquivos NTFS de **Leitura**  

- Permissões de compartilhamento de **Leitura**  

> [!Note]  
> Se você usa compartilhamentos administrativos, por exemplo, C$ e D$, a conta de computador de site secundário deve ser um **Administrador** no servidor.  

### <a name="setup-source-version"></a>Versão de origem da instalação

*Aplica-se a: Site secundário*

A versão do Configuration Manager na pasta de origem especificada para a instalação do site secundário corresponde à versão do Configuration Manager site primário.

### <a name="site-code-in-use"></a>Código do site em uso

*Aplica-se a: Site primário*

O código do site especificado ainda não está em uso na hierarquia do Configuration Manager. Especifique um código do site exclusivo para este site.

### <a name="site-server-computer-account-administrative-rights"></a>Direitos administrativos da conta de computador do servidor do site

*Aplica-se a: Site primário, servidor de banco de dados do site*

A conta de computador do servidor do site tem direitos de **Administrador** sobre o SQL Server e ponto de gerenciamento.

### <a name="site-server-fqdn-length"></a>Comprimento do FQDN do servidor do site

*Aplica-se a: Site de administração central, site primário, site secundário*

O comprimento do FQDN do servidor do site.

### <a name="site-server-in-passive-mode-on-the-expanded-primary-site"></a>Servidor do site no modo passivo no site primário expandido

*Aplica-se a: Site de administração central*

Quando você expande um site primário para uma hierarquia, o servidor do site na função de modo passivo não é instalado no site primário autônomo.

### <a name="sms-provider-in-same-domain-as-site-server"></a>Provedor de SMS no mesmo domínio do servidor do site

*Aplica-se a: Provedor de SMS*

Qualquer instância do provedor de SMS está no mesmo domínio que o servidor do site.

### <a name="software-update-point-in-nlb-configuration"></a>Ponto de atualização de software na Configuração de NLB

*Aplica-se a: Ponto de atualização de software*

O site não está usando o NLB (Balanceamento de Carga de Rede) com nenhum dos locais virtuais para pontos de atualização de software ativos.

### <a name="software-update-point-using-a-load-balancer"></a>Ponto de atualização de software usando um balanceador de carga

*Aplica-se a: Ponto de atualização de software*

O Configuration Manager não é compatível com pontos de atualização de software no NLB (Balanceamento de Carga de Rede) ou no HLB (Balanceador de Carga de Hardware).

### <a name="sql-server-always-on-availability-groups"></a>Grupos de disponibilidade Always On do SQL Server

*Aplica-se a: Servidor de banco de dados do site*

Ao usar o SQL Server Always On, ele deve atender aos requisitos mínimos para hospedar um grupo de disponibilidade. Para obter mais informações, confira [Preparar para usar os grupos de disponibilidade Always On do SQL Server com o Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

### <a name="sql-server-availability-group-configured-for-readable-secondaries"></a>Grupo de disponibilidade SQL Server configurado para secundários legíveis

*Aplica-se a: Servidor de banco de dados do site*

Ao usar o SQL Server Always On, verifique o estado de leitura secundário de réplicas do grupo de disponibilidade.

### <a name="sql-server-availability-group-configured-for-manual-failover"></a>Grupo de disponibilidade SQL Server configurado para failover manual

*Aplica-se a: Servidor de banco de dados do site*

Ao usar o SQL Server Always On, as réplicas do grupo de disponibilidade são configuradas para o failover manual.

### <a name="sql-server-availability-group-replicas-on-default-instance"></a>Réplicas do grupo de disponibilidade do SQL Server na instância padrão

*Aplica-se a: Servidor de banco de dados do site*

Ao usar o SQL Server Always On, as réplicas do grupo de disponibilidade estão na instância padrão.

### <a name="sql-server-configuration-for-site-upgrade"></a>Configuração do SQL Server para a atualização do site

*Aplica-se a: Servidor de banco de dados do site*

O SQL Server especificado atende aos requisitos mínimos para a atualização do site. Para obter mais informações, confira [Versões do SQL Server com suporte](/sccm/core/plan-design/configs/support-for-sql-server-versions).

### <a name="sql-server-edition"></a>Edição do SQL Server

*Aplica-se a: Servidor de banco de dados do site*

SQL Server no site não é SQL Server Express.

### <a name="sql-server-express-on-secondary-site"></a>SQL Server Express no site secundário

*Aplica-se a: Site secundário*

O SQL Server Express pode ser instalado com êxito no servidor do site secundário.

### <a name="sql-server-on-the-secondary-site-server"></a>SQL Server no servidor do site secundário

*Aplica-se a: Site secundário*

O SQL Server é instalado no servidor do site secundário. Não é possível instalar o SQL Server em um sistema de site remoto para um site secundário.

> [!Warning]  
> Esta seleção se aplica somente quando você seleciona para que a instalação use uma instância existente do SQL Server.  

### <a name="sql-server-service-running-account"></a>Conta executando o serviço do SQL Server

*Aplica-se a: Site de administração central, site primário, site secundário*

A conta de conexão para o serviço SQL Server não é uma conta de usuário local ou **SERVIÇO LOCAL**.

Configure o serviço SQL Server para usar uma conta de domínio válida, **SERVIÇO DE REDE** ou **SISTEMA LOCAL**.

### <a name="sql-server-site-database-consistency"></a>Consistência de banco de dados do site do SQL Server

*Aplica-se a: Servidor de banco de dados do site*

Verificar consistência de banco de dados.

### <a name="sql-server-sysadmin-rights"></a>Direitos sysadmin do SQL Server

*Aplica-se a: Servidor de banco de dados do site*

A conta de usuário que executa a Instalação do Configuration Manager tem a função **sysadmin** na instância do SQL Server selecionada para instalação do banco de dados do site. Essa verificação também falha quando a configuração não pode acessar a instância do SQL Server para verificar as permissões.

### <a name="sql-server-sysadmin-rights-for-reference-site"></a>Direitos sysadmin do SQL Server para site de referência

*Aplica-se a: Servidor de banco de dados do site*

A conta de usuário que executa a Instalação do Configuration Manager tem a função **sysadmin** na instância de função do SQL Server selecionada como o banco de dados do site de referência. As permissões da função **sysadmin** do SQL Server são necessárias para modificar o banco de dados do site.

### <a name="sql-server-tcp-port"></a>Porta TCP do SQL Server

*Aplica-se a: Servidor de banco de dados do site*

O TCP está habilitado para a instância do SQL Server e está configurado para usar a porta estática.

### <a name="sql-server-version"></a>Versão do SQL Server

*Aplica-se a: Servidor de banco de dados do site*

Uma versão com suporte do SQL Server instalada no servidor de banco de dados do site especificado.

Para obter mais informações, veja [Suporte a versões do SQL Server](/sccm/core/plan-design/configs/support-for-sql-server-versions).

### <a name="unsupported-os-for-configuration-manager-console"></a>Sistema operacional sem suporte para o console do Configuration Manager

*Aplica-se a: Console do Configuration Manager*

Instale o console do Configuration Manager em computadores que executam uma versão de sistema operacional com suporte.

Para obter mais informações, confira [Versões do sistema operacional com suporte para o console do Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-consoles).

### <a name="unsupported-os-for-site-server"></a>Sistema operacional sem suporte para servidor do site

*Aplica-se a: Site de administração central, site primário, site secundário, console do Configuration Manager, ponto de gerenciamento, ponto de distribuição*

O servidor executa uma versão de sistema operacional com suporte.

Para obter mais informações, confira [versões de sistemas operacionais com suporte para servidores de sistema de sites do Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).

### <a name="unsupported-site-system-role-out-of-band-service-point"></a>Função do sistema de sites sem suporte: ponto de serviço fora da banda

*Aplica-se a: Site primário*

A função do sistema de sites de ponto de serviço fora de banda não está instalada.

### <a name="unsupported-site-system-role-system-health-validation-point"></a>Função do sistema de sites sem suporte: ponto de validação de integridade do sistema

*Aplica-se a: Site primário*

A função do sistema de sites do ponto de validação de integridade do sistema não está instalada.

### <a name="unsupported-upgrade-path"></a>Caminho de atualização sem suporte

*Aplica-se a: Site de administração central, site primário*

Todos os servidores do site na hierarquia atendem a versão mínima do Configuration Manager exigida para a atualização.

### <a name="usmt-installed"></a>USMT instalada

*Aplica-se a: Site de administração central, site primário (somente autônomo)*

O componente USMT (Ferramenta de Migração do Usuário) do Windows ADK (Kit de Avaliação e Implantação do Windows) do Windows foi instalado.

### <a name="validate-fqdn-of-sql-server"></a>Validar o FQDN do SQL Server

*Aplica-se a: Servidor de banco de dados do site*

Você especificou um FQDN válido para o computador do SQL Server.

### <a name="verify-central-administration-site-version"></a>Verificar a versão do site de administração central

*Aplica-se a: Site primário*

O site de administração central tem a mesma versão do Configuration Manager.

### <a name="verify-database-consistency"></a>Verificar consistência de banco de dados

*Aplica-se a: Site de administração central, site primário*

Verifica a consistência do banco de dados do site no SQL Server.  

### <a name="windows-deployment-tools-installed"></a>Windows Deployment Tools instalado

*Aplica-se a: Provedor de SMS*

O componente Windows Deployment Tools do Windows ADK está instalado.

### <a name="windows-failover-cluster"></a>Cluster de Failover do Windows

*Aplica-se a: Servidor, ponto de gerenciamento, ponto de distribuição*

Servidor com servidor do site, ponto de gerenciamento ou funções de ponto de distribuição não fazem parte de um Cluster do Windows.

Da versão 1810 em diante, o processo de instalação do Configuration Manager não bloqueia mais a instalação da função de servidor de site em um computador com a função do Windows para clustering de failover. O Always On do SQL requer essa função; portanto, anteriormente não era possível colocar o banco de dados do site no servidor do site. Com essa alteração, é possível criar um site altamente disponível com menos servidores usando o Always On do SQL e um servidor do site no modo passivo. Para obter mais informações, confira [Opções de alta disponibilidade](/sccm/core/servers/deploy/configure/high-availability-options). <!--1359132-->  

### <a name="windows-pe-installed"></a>Windows PE instalado

*Aplica-se a: Provedor de SMS*

O componente PE (Ambiente de Pré-Instalação) do Windows ADK está instalado.



## <a name="warnings"></a>Avisos

### <a name="active-directory-domain-functional-level"></a>Nível funcional de domínio do Active Directory

*Aplica-se a: Site de administração central, site primário*

O nível funcional do Domínio do Active Directory é, no mínimo, de Windows Server 2008 R2.

### <a name="administrative-rights-on-distribution-point"></a>Direitos administrativos no ponto de distribuição

*Aplica-se a: Ponto de distribuição*

A conta de usuário que está executando a instalação tem direitos de **Administrador** no ponto de distribuição.

### <a name="administrative-rights-on-management-point"></a>Direitos administrativos no ponto de gerenciamento

*Aplica-se a: Ponto de gerenciamento, ponto de distribuição*

A conta de computador do servidor do site tem direitos de **Administrador** no ponto de gerenciamento e do ponto de distribuição.

### <a name="administrative-share-site-system"></a>Compartilhamento administrativo (sistema de sites)

*Aplica-se a: Ponto de gerenciamento*

Os compartilhamentos administrativos necessários estão presentes no computador do sistema de site.

### <a name="application-compatibility"></a>Compatibilidade do aplicativo

*Aplica-se a: Site de administração central, site primário*

Os aplicativos atuais estão em conformidade com o esquema do aplicativo.

### <a name="backlogged-inboxes"></a>Caixas de entrada acumuladas

*Aplica-se a: Site de administração central, site primário*

O servidor do site está processando as caixas de entrada críticas de forma oportuna. As caixas de entrada não contêm arquivos com mais de um dia.

Ele verifica as seguintes pastas de caixa de entrada:

- `despoolr.box\receive\*.i??`

- `despoolr.box\receive\*.s??`

- `despoolr.box\receive\*.nil`

- `schedule.box\requests\*.sr?`

Para resolver este aviso, verifique se o despooler e os componentes de sistema de site do agendador estão em execução.

### <a name="bits-installed"></a>BITS instalado

*Aplica-se a: Ponto de gerenciamento*

O BITS (Serviço de Transferência Inteligente em Segundo Plano) está instalado e habilitado no IIS.

### <a name="cloud-management-gateway-requires-either-token-based-authentication-or-an-https-management-point"></a>O gateway de gerenciamento de nuvem requer uma autenticação baseada em token ou um ponto de gerenciamento HTTPS

*Aplica-se a: Gateway de gerenciamento de nuvem*

Com algumas versões do Configuration Manager, você não pode usar um ponto de gerenciamento de HTTP com o CMG (gateway de gerenciamento de nuvem). Configure o CMG para HTTPS ou configure o site para HTTP aprimorado. Para obter mais informações, consulte [Planejar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).

### <a name="configuration-for-sql-server-memory-usage"></a>Configuração do uso de memória do SQL Server

*Aplica-se a: Servidor de banco de dados do site*

O SQL Server está configurado para uso ilimitado de memória. Configure a memória do SQL Server para ter um limite máximo.

### <a name="distribution-point-package-version"></a>Versão do pacote de ponto de distribuição

*Aplica-se a: Pontos de distribuição*

Todos os pontos de distribuição no site têm a versão mais recente dos pacotes de distribuição de software.

### <a name="domain-membership-warning"></a>Associação do domínio (aviso)

*Aplica-se a: Ponto de gerenciamento, ponto de distribuição*

O computador do Configuration Manager é membro de um domínio do Windows.

### <a name="firewall-exception-for-sql-server-standalone-primary-site"></a>Exceção de firewall do SQL Server (site primário autônomo)

*Aplica-se a: Site primário (somente autônomo)*

O Firewall do Windows está desabilitado ou existe uma exceção relevante do Firewall do Windows relativa ao SQL Server.

Permita que o Sqlservr.exe ou as portas TCP necessárias possam ser acessadas remotamente. Por padrão, o SQL Server escuta na porta TCP 1433 e o SSB (Server Service Broker) usa a porta TCP 4022.

### <a name="firewall-exception-for-sql-server-for-management-point"></a>Exceção de firewall do SQL Server do ponto de gerenciamento

*Aplica-se a: Ponto de gerenciamento*

O Firewall do Windows está desabilitado ou existe uma exceção relevante do Firewall do Windows relativa ao SQL Server.

### <a name="iis-https-configuration"></a>Configuração de IIS HTTPS

*Aplica-se a: Ponto de gerenciamento, ponto de distribuição*

O site IIS tem associações para o protocolo de comunicação HTTPS.

Ao instalar funções de site que exijam HTTPS, configure as ligações de site do IIS no servidor especificado com um certificado PKI (infraestrutura de chave pública) válido.

### <a name="microsoft-xml-core-services-60-msxml60"></a>Microsoft XML Core Services 6.0 (MSXML60)

*Aplica-se a site de administração central, site primário, site secundário, console do Configuration Manager, ponto de gerenciamento, ponto de distribuição*

Verifica se o MSXML 6.0 ou uma versão mais recente está instalado.

### <a name="network-access-protection-nap-is-no-longer-supported"></a>A NAP (Proteção de Acesso à Rede) não é mais compatível

*Aplica-se a: Site primário*

Não há atualizações de software habilitadas para NAP.

### <a name="ntfs-drive-on-site-server"></a>Unidade NTFS no servidor do site

*Aplica-se a: Site primário*

A unidade de disco é formatada com o sistema de arquivos NTFS. Para aumentar a segurança, instale componentes do servidor do site em unidades de disco formatadas com o sistema de arquivos NTFS.

### <a name="bkmk_pending-policy"></a> Atualizações de política do item de configuração pendentes

<!--SCCMDocs-pr issue 2814-->

*Aplica-se a: Site primário*

Da versão 1806 em diante, se você estiver atualizando da versão 1706 ou posterior, você poderá ver esse aviso se você tiver muitas implantações de aplicativo e pelo menos uma delas exigir aprovação.

Você tem duas opções:  

- Ignorar o aviso e continuar com a atualização. Essa ação gera maior processamento no servidor do site durante a atualização conforme ela processa as políticas. Você também poderá ver o mais carga sobre o processador no ponto de gerenciamento após a atualização.  

- Revisar um dos aplicativos que não tem requisitos ou um requisito de SO específico. Pré-processe uma parte da carga no servidor do site nesse momento. Examine **objreplmgr.log** e, em seguida, monitore o processador no ponto de gerenciamento. Depois que o processamento for concluído, atualize o site. Ainda haverá algum processamento adicional após a atualização, mas será menor do que se você ignorar o aviso com a primeira opção.  

### <a name="pending-system-restart-on-the-remote-sql-server"></a>Reinicialização do sistema pendente no servidor SQL remoto

*Aplica-se a: Versão 1902 e posterior, SQL Server remoto*

Antes de executar a instalação, outro programa exige que o servidor seja reiniciado.

Para ver se o computador está em um estado de reinicialização pendente, ela verifica os seguintes locais do registro:<!--SCCMDocs-pr issue 3377-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="powershell-20-on-site-server"></a>PowerShell 2.0 no servidor do site

*Aplica-se a: Site primário com o conector do Exchange*

O Windows PowerShell 2.0 ou uma versão posterior está instalada no servidor do site do Exchange Connector do Configuration Manager.

### <a name="remote-connection-to-wmi-on-secondary-site"></a>Conexão remota com WMI no site secundário

*Aplica-se a: Site secundário*

A instalação pode estabelecer uma conexão remota com WMI no servidor do site secundário.

### <a name="schema-extensions"></a>Extensões de esquema

*Aplica-se a: Site de administração central, site primário*

O esquema do Active Directory foi estendido. Se ele tiver estendido, a versão das extensões de esquema que foram usadas.

O Configuration Manager não requer extensões de esquema do Active Directory para a instalação de servidor do site. A Microsoft as recomenda para o uso completo de todos os recursos do Configuration Manager. Para obter mais informações sobre as vantagens de estender o esquema, consulte [Preparar o Active Directory para publicação de sites](/sccm/core/plan-design/network/extend-the-active-directory-schema).

### <a name="share-name-in-package"></a>Nome do compartilhamento no pacote

*Aplica-se a: Site de administração central, site primário*

Os pacotes não têm caracteres inválidos no nome do compartilhamento, tais como `#`.

### <a name="site-system-to-sql-server-communication"></a>Comunicação do Sistema de sites com o SQL Server

*Aplica-se a: Site secundário, ponto de gerenciamento*

A conta que você configurou para executar o serviço do SQL Server para a instância de banco de dados do site tem um SPN (nome da entidade de serviço) válido nos Active Directory Domain Services. Registre um SPN válido no Active Directory para dar suporte à autenticação Kerberos.

### <a name="bkmk_changetracking"></a> Limpeza do controle de alterações do SQL Server

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

### <a name="sql-server-native-client"></a>SQL Server Native Client

<!--SCCMDocs-pr issue 3094-->

Quando você instala um novo site, o Configuration Manager instala automaticamente o SQL Server Native Client como um componente redistribuível. Depois que o site é instalado, o Configuration Manager não atualizará o SQL Server Native Client. A atualização do SQL Server Native Client pode exigir uma reinicialização, que pode afetar o processo de instalação do site.

Essa verificação garante que o site tem uma versão compatível do SQL Native Client. Começando na versão 1810, a versão mínima é SQL 2012 SP4 (`11.*.7001.0`).

Esta versão do SQL Native Client dá suporte a TLS 1.2. Para obter mais informações, consulte os seguintes artigos:

- [Suporte ao TLS 1.2 para o Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)  

- [Como habilitar o TLS 1.2 para o Configuration Manager](https://support.microsoft.com/help/4040243/how-to-enable-tls-1-2-for-configuration-manager)  

O Configuration Manager usa o SQL Server Native Client nas seguintes funções de sistema de sites:<!-- SCCMDocs issue 1150 -->

- Servidor de banco de dados do site
- Servidor do site: site de administração central, site primário ou site secundário
- Ponto de gerenciamento
- Ponto de gerenciamento de dispositivo
- Ponto de migração de estado
- Provedor de SMS
- Ponto de atualização de software
- Ponto de distribuição habilitado para multicast
- Ponto de serviço de atualização do Asset Intelligence
- Ponto do Reporting Services
- Serviço Web do catálogo de aplicativos
- Ponto de registro
- Ponto do Endpoint Protection
- Ponto de Conexão de Serviço
- Ponto de registro de certificado
- Ponto de serviço de data warehouse

### <a name="sql-server-process-memory-allocation"></a>Alocação de memória de processo do SQL Server

*Aplica-se a: Servidor de banco de dados do site*

O SQL Server reserva um mínimo de 8 GB de memória para o site de administração central e site primário e um mínimo de 4 GB de memória para o site secundário.

Para obter mais informações, veja [Como configurar opções de memória usando o SQL Server Management Studio](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options#how-to-configure-memory-options-using-includessmanstudiofullincludesssmanstudiofull-mdmd).

> [!NOTE]  
> Essa verificação não é aplicável ao SQL Server Express em um site secundário. Esta edição é limitada a 1 GB de memória reservada.  

### <a name="sql-server-security-mode"></a>Modo de segurança do SQL Server

*Aplica-se a: Servidor de banco de dados do site*

O SQL Server está configurado para segurança de autenticação do Windows.

### <a name="unsupported-site-system-os-version-for-upgrade"></a>Versão de sistema operacional do sistema de site sem suporte para atualização

*Aplica-se a: Site primário, site secundário*

Funções do sistema de site além dos pontos de distribuição são instaladas em servidores que executam o Windows Server 2012 ou posterior.

Para obter mais informações, confira [Sistemas operacionais com suporte para servidores de sistema de sites do Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).

> [!NOTE]  
> Essa verificação não pode resolver o status das funções de sistema de sites instaladas no Azure ou para o armazenamento em nuvem usado pelo Microsoft Intune. Ignore os avisos para essas funções como falsos positivos.

### <a name="upgrade-assessment-toolkit-is-unsupported"></a>Não há suporte para o Kit de Ferramentas de Avaliação de Atualização

*Aplica-se a: Site de administração central, site primário*

O Kit de Ferramentas de Avaliação de Atualização não está instalado. Para saber mais, consulte [Recursos removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).

### <a name="verify-site-server-permissions-to-publish-to-active-directory"></a>Verifique as permissões do servidor do site para publicar no Active Directory

*Aplica-se a: Site de administração central, site primário, site secundário*

A conta de computador do servidor do site tem permissões de **Controle Total** no contêiner do **System Management** no domínio do Active Directory.

Para obter mais informações, consulte [Preparar o Active Directory para publicação de sites](/sccm/core/plan-design/network/extend-the-active-directory-schema).

> [!NOTE]  
> Se você verificar as permissões manualmente, poderá ignorar este aviso.

### <a name="windows-remote-management-winrm-v11"></a>Gerenciamento Remoto do Windows (WinRM) v1.1

*Aplica-se a: Site primário, console do Configuration Manager*

O WinRM 1.1 está instalado no servidor do site primário ou no computador console do Configuration Manager para executar o console de gerenciamento fora da banda.

Para obter mais informações sobre como baixar o WinRM 1.1, confira o [Artigo de suporte 936059](https://support.microsoft.com/help/936059).

### <a name="wsus-on-site-server"></a>WSUS no servidor do site

*Aplica-se a: Site de administração central, site primário*

Uma versão com suporte do WSUS (Windows Server Update Services) é instalada no servidor do site.

Ao usar um ponto de atualização de software em um servidor que não o servidor do site, instale primeiro o Console de Administração do WSUS no servidor do site. Para obter mais informações sobre o WSUS, consulte [Windows Server Update Services](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus).
