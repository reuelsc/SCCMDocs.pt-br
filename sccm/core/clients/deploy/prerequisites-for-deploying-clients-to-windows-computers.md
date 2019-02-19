---
title: Pré-requisitos de implantação do cliente Windows
titleSuffix: Configuration Manager
description: Saiba mais sobre os pré-requisitos para implantação do cliente do Configuration Manager em computadores Windows.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a6d93fcc35a6d038b03a0829c6fe66ecc50a5446
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140272"
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-configuration-manager"></a>Pré-requisitos para a implantação de clientes em computadores Windows no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A implantação de clientes do Configuration Manager em seu ambiente tem as seguintes dependências externas e dependências no produto. Além disso, cada método de implantação do cliente tem suas próprias dependências que devem ser atendidas para que as instalações do cliente sejam bem-sucedidas.  

Para obter mais informações sobre os requisitos mínimos de hardware e de sistema operacional do cliente do Configuration Manager, confira [Configurações com suporte](/sccm/core/plan-design/configs/supported-configurations).  

> [!NOTE]  
>  Os números de versão de software mostrados neste artigo listam somente os números de versão mínimos.  



##  <a name="BKMK_prereqs_computers"></a> Pré-requisitos para clientes do Windows  

Use as seguintes informações para determinar os pré-requisitos ao instalar o cliente do Configuration Manager em dispositivos Windows.  

### <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  

|Componente|Descrição|  
|---|---|  
|Windows Installer versão 3.1.4000.2435|Necessário para oferecer suporte ao uso dos arquivos de atualização (. msp) do Windows Installer para pacotes e atualizações de software.|  
|Serviço de Transferência Inteligente em Segundo Plano (BITS) da Microsoft versão 2.5|Necessário para permitir transferências de dados limitadas entre o computador cliente e os sistemas de sites do Configuration Manager. O BITS não é baixado automaticamente durante a instalação do cliente. Quando o BITS é instalado em computadores, normalmente é necessário reinicializar para concluir a instalação.<br /><br /> A maioria dos sistemas operacionais inclui o BITS. Caso contrário, instale o BITS antes de instalar o cliente do Configuration Manager.|  
|Agendador de Tarefas Microsoft|Habilite esse serviço no cliente para que a instalação do cliente seja concluída.|  


### <a name="bkmk_ExternalDependencies"></a> Dependências externas ao Configuration Manager e baixadas automaticamente durante a instalação  

O cliente do Configuration Manager tem dependências externas. Essas dependências dependem da versão do sistema operacional e do software instalado no computador cliente.  

Se o cliente exigir essas dependências para concluir a instalação, ele as instalará automaticamente.  

|Componente|Descrição|  
|---|---|  
|Windows Update Agent versão 7.0.6000.363|Necessário para o Windows a fim de oferecer suporte à detecção de atualização e implantação.|  
|Microsoft Core XML Services (MSXML) versão 6.20.5002 ou posterior|Necessário para oferecer suporte ao processamento de documentos XML no Windows.|  
|Compactação Diferencial Remota da Microsoft (RDC)|Necessário para otimizar a transmissão de dados pela rede.|  
|Microsoft Visual C++ 2013 Redistribuível versão 12.0.21005.1|Necessário para oferecer suporte às operações do cliente. Quando você instala essa atualização em computadores cliente, pode ser necessário reiniciar para concluir a instalação.|  
|Microsoft Visual C++ 2005 Redistribuível versão 8.0.50727.42|Para a versão 1606 e anteriores, necessário para dar suporte a operações do Microsoft SQL Server Compact.|  
|APIs do Windows Imaging 6.0.6001.18000|Necessário para permitir que o Configuration Manager gerencie arquivos de imagem (.wim) do Windows.|  
|Microsoft Policy Platform 1.2.3514.0|Necessário para permitir que clientes avaliem as configurações de conformidade.|  
|Microsoft Silverlight 5.1.41212.0|Necessário para oferecer suporte à experiência do usuário de site da Web do catálogo de aplicativos. Começando no Configuration Manager 1802, o cliente não instala o Silverlight automaticamente. A principal funcionalidade do Catálogo de Aplicativos agora está incluída no Centro de Software. O suporte ao site Catálogo de Aplicativos termina na versão 1806.<!--1356195-->|  
|Microsoft .NET Framework versão 4.5.2|Necessário para oferecer suporte às operações do cliente. Instalado automaticamente no computador cliente se o Microsoft .NET Framework versão 4.5 ou posterior não estiver instalado. Para obter mais informações, consulte [Detalhes adicionais sobre o Microsoft .NET Framework versão 4.5.2](#dotNet).|  
|Componentes do Microsoft SQL Server Compact 4.0 SP1|Necessário para armazenar informações relacionadas às operações do cliente.|  


####  <a name="dotNet"></a> Detalhes adicionais sobre o Microsoft .NET Framework versão 4.5.2  

> [!NOTE]  
>  Não há mais suporte para o .NET 4.0, 4.5 e 4.5.1. Para obter mais informações, consulte [Perguntas frequentes sobre a política do ciclo de vida de suporte do .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).  

O Microsoft .NET Framework versão 4.5.2 pode exigir uma reinicialização para concluir a instalação. O usuário verá a notificação **Reinicialização necessária** na bandeja do sistema. Os cenários comuns a seguir exigem que os computadores cliente sejam reiniciados:  

-   Há aplicativos ou serviços do .NET em execução no computador.  

-   Uma ou mais atualizações de software necessárias para a instalação do .NET estão ausentes.  

-   O computador está aguardando uma reinicialização da instalação anterior das atualizações de software do .NET Framework.  


Depois que o .NET Framework 4.5.2 for instalado, ele poderá exigir atualizações adicionais. Essas atualizações posteriores poderão exigir mais reinicializações do computador.  


### <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

Para obter mais informações, consulte [Determinar as funções do sistema de sites para clientes](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients).  

|Componente|Descrição|  
|---|---|  
|Ponto de gerenciamento|Para implantar o cliente do Configuration Manager, você não precisa de um ponto de gerenciamento. Os clientes exigem um ponto de gerenciamento para transferir informações com o site. Sem um ponto de gerenciamento, você não pode gerenciar computadores cliente.|  
|Ponto de distribuição|O ponto de distribuição é uma função do sistema de sites opcional, mas recomendada, para a implantação e o gerenciamento de clientes. Todos os pontos de distribuição hospedam os arquivos de origem do cliente. Os clientes encontram o ponto de distribuição mais próximo para baixar os arquivos de origem durante a implantação ou a atualização do cliente. Quando o site não tem um ponto de distribuição, os computadores baixam os arquivos de origem do cliente de seu ponto de gerenciamento.|  
|Ponto de status de fallback|O ponto de status de fallback é uma função do sistema de site opcional, mas recomendável, para a implantação de clientes. O ponto de status de fallback controla a implantação do cliente e permite que os computadores no site do Configuration Manager enviem mensagens de estado quando eles não podem se comunicar com um ponto de gerenciamento.|  
|Ponto do Reporting Services|O ponto do Reporting Services é uma função do sistema de sites opcional, mas recomendada. Ele exibe relatórios relacionados à implantação e ao gerenciamento do cliente. Para obter mais informações, confira [Reporting in Configuration Manager](/sccm/core/servers/manage/reporting) (Relatórios no Configuration Manager).|  


### <a name="installation-method-dependencies"></a>Dependências do método de instalação  

Os pré-requisitos a seguir são específicos para os diversos métodos de instalação do cliente.  

#### <a name="client-push-installation"></a>Instalação do cliente por push  

   -   O site usa contas de instalação do cliente por push para conectar-se aos computadores para instalar o cliente. Especifique essas contas na guia **Contas** das propriedades de instalação do cliente por push. A conta deve ser membro do grupo local de administradores no computador de destino.  

         Se você não especificar uma conta de instalação do cliente por push, o servidor do site usará sua conta do computador.  

   -   O site precisa descobrir o computador no qual você está instalando o cliente. É necessário pelo menos um método de descoberta do Configuration Manager.  

   -   O computador tem um compartilhamento Admin$.  

   -   Para efetuar push automaticamente do cliente do Configuration Manager para os recursos descobertos, selecione a opção para **Habilitar a instalação do cliente por push para recursos atribuídos** nas propriedades da instalação do cliente por push.  

   -   O computador cliente precisa se comunicar com um ponto de distribuição ou um ponto de gerenciamento para baixar os arquivos de origem.  

   -   Começando na versão 1806, quando houver necessidade de autenticação mútua do Kerberos, os clientes precisarão estar em uma floresta confiável do Active Directory. O Kerberos no Windows depende do Active Directory para autenticação mútua.<!--1358204-->  


Para usar o cliente por push, você precisará das seguintes permissões de segurança:  

   -   Para configurar a conta de instalação do cliente por push: permissão **Modificar** e **Ler** para o objeto **Site**.  

   -   Para usar o push de clientes para instalar coleções, dispositivos e consultas para clientes: permissão **Modificar Recurso** e **Ler** para o objeto **Coleção**.  


A função de segurança padrão **Administrador de Infraestrutura** inclui as permissões necessárias para gerenciar instalações do cliente por push.  


#### <a name="software-update-point-based-installation"></a>Instalação baseada em ponto de atualização de software  

   -   Se você não estendeu o esquema do Active Directory ou se você está instalando clientes de outra floresta, use a política de grupo para provisionar os parâmetros de instalação do CCMSetup.exe. Para obter mais informações, confira [Como provisionar propriedades de instalação do cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).  

   -   Publique o cliente do Configuration Manager no ponto de atualização de software.  

   -   Para baixar os arquivos de origem, o computador cliente precisa se comunicar com um ponto de distribuição ou um ponto de gerenciamento.  


Para conhecer as permissões de segurança necessárias para gerenciar as atualizações de software do Configuration Manager, consulte [Pré-requisitos para atualizações de software](/sccm/sum/plan-design/prerequisites-for-software-updates).  


#### <a name="group-policy-based-installation"></a>Instalação baseada na política de grupo  

   -   Se você não estendeu o esquema do Active Directory ou se você está instalando clientes de outra floresta, use a política de grupo para provisionar os parâmetros de instalação do CCMSetup.exe. Para obter mais informações, confira [Como provisionar propriedades de instalação do cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).  

   -   Para baixar os arquivos de origem, o computador cliente precisa se comunicar com um ponto de distribuição ou um ponto de gerenciamento.  


#### <a name="logon-script-based-installation"></a>Instalação baseada em script de logon  

Para baixar os arquivos de origem, o computador cliente precisa se comunicar com um ponto de distribuição ou um ponto de gerenciamento. A não ser que tenha especificado o CCMSetup.exe com o parâmetro de linha de comando a seguir: `ccmsetup /source`  


#### <a name="manual-installation"></a>Instalação manual  

Para baixar os arquivos de origem, o computador cliente precisa se comunicar com um ponto de distribuição ou um ponto de gerenciamento. A não ser que tenha especificado o CCMSetup.exe com o parâmetro de linha de comando a seguir: `ccmsetup /source`  


#### <a name="microsoft-intune-mdm-installation"></a>Instalação do Microsoft Intune MDM

 - Exige uma assinatura do Microsoft Intune e as licenças apropriadas.  

 - Requer que o dispositivo tenha acesso à Internet, mesmo se ele não for baseado na Internet.  

 - Dependendo do caso de uso, também poderá ser necessário usar uma das tecnologias a seguir ou ambas:  

     - Azure Active Directory  

     - Gateway de gerenciamento de nuvem  


#### <a name="workgroup-computer-installation"></a>Instalação de computador do grupo de trabalho  

Para acessar recursos no domínio do servidor do site do Configuration Manager, configure uma conta de acesso à rede para o site.  

Para obter mais informações sobre como configurar a conta de acesso à rede, consulte [Conceitos fundamentais para o gerenciamento de conteúdo](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).  


#### <a name="software-distribution-based-installation-for-upgrades-only"></a>Instalação baseada em distribuição de software (somente para atualizações)  

   -   Se você não estendeu o esquema do Active Directory ou se você está instalando clientes de outra floresta, use a política de grupo para provisionar os parâmetros de instalação do CCMSetup.exe. Para obter mais informações, confira [Como provisionar propriedades de instalação do cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).   

   -   Para baixar os arquivos de origem, o computador cliente precisa se comunicar com um ponto de distribuição ou um ponto de gerenciamento.  


Para conhecer as permissões de segurança necessárias para atualizar o cliente do Configuration Manager usando o gerenciamento de aplicativos, consulte [Segurança e privacidade para gerenciamento de aplicativos no Configuration Manager](/sccm/apps/plan-design/security-and-privacy-for-application-management).  


#### <a name="automatic-client-upgrades"></a>Atualizações automáticas do cliente  

Você deve ser um membro da função de segurança **Administrador Completo** para configurar atualizações automáticas do cliente.  


### <a name="firewall-requirements"></a>Requisitos de firewall  

Se houver um firewall entre os servidores do sistema de sites e os computadores nos quais você deseja instalar o cliente do Configuration Manager, confira [Configurações do Firewall do Windows e de porta para clientes](/sccm/core/clients/deploy/windows-firewall-and-port-settings-for-clients).  



##  <a name="BKMK_prereqs_mobiledevices"></a> Pré-requisitos para clientes de dispositivos móveis  

Ao instalar o cliente do Configuration Manager em dispositivos móveis e os registra, use essas informações para determinar os pré-requisitos.  

### <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  

-   Uma AC (autoridade de certificação) corporativa com modelos de certificado para implantar e gerenciar os certificados necessários para dispositivos móveis.  

     Uma AC emissora deve aprovar automaticamente as solicitações de certificados de usuários de dispositivos móveis durante o processo de registro.  

     Para obter mais informações sobre os requisitos de certificado, consulte [Segurança e privacidade de perfis de certificado](/sccm/protect/plan-design/security-and-privacy-for-certificate-profiles).  

-   Um grupo de segurança que contém os usuários que podem registrar seus dispositivos móveis.  

     Esse grupo de segurança é usado para configurar o modelo de certificado usado durante o registro do dispositivo móvel.  

-   Opcional, mas recomendado: um alias DNS (registro CNAME) chamado **ConfigMgrEnroll**. Configure esse alias para o nome do servidor do ponto proxy do registro.  

     Esse alias DNS é necessário para dar suporte à descoberta automática para o serviço de registro. Se você não configura esse registro DNS, os usuários devem especificar manualmente o nome do ponto proxy do registro como parte do processo de registro.  

-   Dependências da função do sistema de sites para os computadores que executam as funções do sistema de sites do ponto de registro e do ponto proxy do registro.  

     Para obter mais informações, confira [Sistemas operacionais com suporte para servidores do sistema de sites](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  


### <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

Para obter mais informações, consulte [Determinar as funções do sistema de sites para clientes](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients).  

- Um ponto de gerenciamento configurado para conexões de cliente HTTPS e habilitado para dispositivos móveis  

   Um ponto de gerenciamento é sempre necessário para instalar o cliente do Configuration Manager em dispositivos móveis. Além dos requisitos de configuração do HTTPS e de estar habilitado para dispositivos móveis, o ponto de gerenciamento deve ser configurado com um FQDN de Internet e aceitar conexões de cliente da Internet.  

- Ponto de registro e ponto proxy do registro  

   O ponto proxy do registro gerencia as solicitações de registro dos dispositivos móveis e o ponto de registro conclui o processo de registro. O ponto de registro deve estar na mesma floresta do Active Directory que o servidor do site, mas o ponto proxy do registro pode estar em outra floresta.  

- Configurações do cliente para registro do dispositivo móvel  

   Defina as configurações de cliente para permitir que os usuários registrem dispositivos móveis e configurem pelo menos um perfil de registro.  

- Ponto do Reporting Services  

   O ponto do Reporting Services é uma função do sistema de site opcional, mas recomendada, que pode exibir relatórios relacionados ao registro de dispositivo móvel e gerenciamento de clientes.  

   Para obter mais informações, confira [Reporting in Configuration Manager](/sccm/core/servers/manage/reporting) (Relatórios no Configuration Manager).  

- Para configurar o registro para dispositivos móveis, você deve ter as seguintes permissões de segurança:  

  - Para adicionar, modificar e excluir as funções do sistema de site de registro: permissão **Modificar** para o objeto **Site**.  

  - Para definir as configurações do cliente para o registro: as configurações de cliente padrão exigem a permissão **Modificar** para o objeto **Site** e as configurações de cliente personalizadas exigem as permissões **Agente cliente**.  

    A função de segurança padrão **Administrador Completo** inclui as permissões necessárias para configurar as funções do sistema de sites de registro.  

    Para gerenciar os dispositivos móveis inscritos, você deve ter as seguintes permissões de segurança:  

  - Para apagar ou desativar um dispositivo móvel: **Excluir recurso** do objeto **Coleção**.  

  - Para cancelar um comando de apagamento ou desativação: **Excluir recurso** do objeto **Coleção**.  

  - Para permitir e bloquear dispositivos móveis: **Modificar recurso** para o objeto **Coleção**.  

  - Para bloquear remotamente ou reconfigurar a senha em um dispositivo móvel: **Modificar** recurso para o objeto **Coleção**.  

    A função de segurança padrão **Administrador de Operações** inclui as permissões necessárias para gerenciar dispositivos móveis.  

    Para obter mais informações sobre como configurar permissões de segurança, consulte [Fundamentos da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration) e [Configurar administração baseada em funções](/sccm/core/servers/deploy/configure/configure-role-based-administration).  


### <a name="firewall-requirements"></a>Requisitos de firewall  

Os dispositivos de rede intermediária, como roteadores e firewalls, e Windows Firewall, se aplicável, devem permitir o tráfego associado ao registro de dispositivo móvel:  

-   Entre os dispositivos móveis e o ponto proxy do registro: HTTPS (por padrão, o TCP 443)  

-   Entre o ponto proxy do registro e o ponto de registro: HTTPS (por padrão, o TCP 443)  


Se você usar um servidor Web proxy, ele precisará ser configurado para o túnel SSL. Não há suporte para SSL em dispositivos móveis.  
