---
title: "Pré-requisitos para a implantação do cliente Windows | System Center Configuration Manager"
description: "Conheça os pré-requisitos para a implantação de clientes em computadores Windows no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
caps.latest.revision: 16
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 03ae6de34742ed0030e42c13639ef853d6b2bedc


---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-system-center-configuration-manager"></a>Pré-requisitos para a implantação de clientes em computadores com Windows no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A implantação de clientes do Configuration Manager em seu ambiente tem as seguintes dependências externas e dependências no produto. Além disso, cada método de implantação do cliente tem suas próprias dependências que devem ser atendidas para que as instalações do cliente sejam bem-sucedidas.  

  Certifique-se de examinar também [Configurações com suporte para o System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md) para confirmar se os dispositivos atendem aos requisitos mínimos de hardware e de sistema operacional para o cliente do Configuration Manager.  

 Para obter informações sobre os pré-requisitos do cliente do Configuration Manager para Linux e UNIX, consulte [Planejando a implantação de cliente em computadores Linux e UNIX no System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md).  

> [!NOTE]  
>  Os números de versão de software mostrados neste artigo listam somente os números de versão mínimos.  

##  <a name="a-namebkmkprereqscomputersa-prerequisites-for-computer-clients"></a><a name="BKMK_prereqs_computers"></a> Pré-requisitos para clientes de computadores  
 Use as informações a seguir para determinar os pré-requisitos ao instalar o cliente do Configuration Manager em computadores.  

### <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  

|||  
|-|-|  
|Windows Installer versão 3.1.4000.2435|Necessário para oferecer suporte ao uso dos arquivos de atualização (. msp) do Windows Installer para pacotes e atualizações de software.|  
|[KB2552033](http://go.microsoft.com/fwlink/p/?LinkId=240048)|Instale esse hotfix nos servidores do site que executam o Windows Server 2008 R2 quando a instalação do cliente por push for habilitada.|  
|Serviço de Transferência Inteligente em Segundo Plano (BITS) da Microsoft versão 2.5|Necessário para permitir transferências de dados limitadas entre o computador cliente e os sistemas de sites do Configuration Manager. O BITS não é baixado automaticamente durante a instalação do cliente. Quando o BITS é instalado em computadores, normalmente é necessário reinicializar para concluir a instalação.<br /><br /> A maioria dos sistemas operacionais inclui o BITS, mas se eles não o incluem (por exemplo, Windows Server 2003 R2 SP2), é necessário instalar o BITS antes de instalar o cliente do Configuration Manager.|  
|Agendador de Tarefas Microsoft|Habilite esse serviço no cliente para que a instalação do cliente seja concluída.|  

### <a name="dependencies-external-to-configuration-manager-and-automatically-downloaded-during-installation"></a>Dependências externas ao Configuration Manager e baixadas automaticamente durante a instalação  
 O cliente do Configuration Manager tem algumas dependências externas potenciais. Essas dependências dependem do sistema operacional e do software instalado no computador cliente.  

 Se essas dependências são necessárias para concluir a instalação do cliente, elas são instaladas automaticamente com o software cliente.  

|||  
|-|-|  
|Windows Update Agent versão 7.0.6000.363|Necessário para o Windows a fim de oferecer suporte à detecção de atualização e implantação.|  
|Microsoft Core XML Services (MSXML) versão 6.20.5002 ou posterior|Necessário para oferecer suporte ao processamento de documentos XML no Windows.|  
|Compactação Diferencial Remota da Microsoft (RDC)|Necessário para otimizar a transmissão de dados pela rede.|  
|Microsoft Visual C++ 2013 Redistribuível versão 12.0.21005.1|Necessário para oferecer suporte às operações do cliente. Quando esta atualização é instalada em computadores cliente, pode ser necessário reinicializar para concluir a instalação.|  
|Microsoft Visual C++ 2005 Redistribuível versão 8.0.50727.42|Necessário para oferecer suporte a operações do Microsoft SQL Server Compact.|  
|APIs do Windows Imaging 6.0.6001.18000|Necessário para permitir que o Configuration Manager gerencie arquivos de imagem (.wim) do Windows.|  
|Microsoft Policy Platform 1.2.3514.0|Necessário para permitir que clientes avaliem as configurações de conformidade.|  
|Microsoft Silverlight 5.1.41212.0 (a partir do Configuration Manager versão 1602)|Necessário para oferecer suporte à experiência do usuário de site da Web do catálogo de aplicativos.|  
|Microsoft .NET Framework versão 4.5.2|Necessário para oferecer suporte às operações do cliente. Instalado automaticamente no computador cliente se ele não contém o Microsoft .NET Framework versão 4.5 ou posterior instalado. Para obter mais informações, consulte [Detalhes adicionais sobre o Microsoft .NET Framework versão 4.5.2](#dotNet).|  
|Componentes do Microsoft SQL Server Compact 3.5 SP2|Necessário para armazenar informações relacionadas às operações do cliente.|  
|Componentes do Microsoft Windows Imaging|Necessários para o Microsoft .NET Framework 4.0 para o Windows Server 2003 ou o Windows XP SP2 para computadores de 64 bits.|  

####  <a name="a-namedotneta-additional-details-about-microsoft-net-framework-version-452"></a><a name="dotNet"></a> Detalhes adicionais sobre o Microsoft .NET Framework versão 4.5.2  

> [!NOTE]  
>  Em 12 de janeiro de 2016, o suporte ao .NET 4.0, 4.5 e 4.5.1 expirou. Para obter mais informações, consulte [Perguntas frequentes sobre a política do ciclo de vida de suporte do Microsoft .NET Framework](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update) em support.microsoft.com.  

 Uma reinicialização pode ser necessária para concluir a instalação do Microsoft .NET Framework versão 4.5.2. O usuário verá a notificação **Reinicialização necessária** na bandeja do sistema.  Cenários comuns que exigem a reinicialização dos computadores cliente:  

-   Há aplicativos ou serviços do .NET em execução no computador.  

-   Uma ou mais atualizações de software necessárias para a instalação do .NET estão ausentes.  

-   O computador está aguardando uma reinicialização da instalação anterior das atualizações de software do .NET Framework.  

 Após a instalação do .NET Framework 4.5.2, atualizações adicionais podem ser instaladas posteriormente, o que pode exigir outra reinicialização do computador.  

### <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  
 Para obter mais informações sobre as seguintes funções de sistema de sites, consulte [Adicionar as funções do sistema de sites para os clientes do System Center Configuration Manager](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md)  

|||  
|-|-|  
|Ponto de gerenciamento|Apesar de o ponto de gerenciamento não ser necessário para implantar o cliente do Configuration Manager, será necessário ter um ponto de gerenciamento para transferir informações entre os computadores cliente e os servidores do Configuration Manager. Sem um ponto de gerenciamento não é possível gerenciar computadores cliente.|  
|Ponto de distribuição|O ponto de distribuição é uma função do sistema de site opcional, mas recomendável, para a implantação de clientes. Todos os pontos de distribuição hospedam arquivos de origem de cliente, o que permite que computadores encontrem o ponto de distribuição mais próximo do qual baixar os arquivos de origem de cliente durante a implantação do cliente. Se o site não possui um ponto de distribuição, os computadores baixam os arquivos de origem de cliente de seu ponto de gerenciamento.|  
|Ponto de status de fallback|O ponto de status de fallback é uma função do sistema de site opcional, mas recomendável, para a implantação de clientes. O ponto de status de fallback controla a implantação do cliente e habilita computadores no site do Configuration Manager para enviar mensagens de estado quando eles não podem se comunicar com um ponto de gerenciamento.|  
|Ponto do Reporting Services|O ponto do Reporting Services é uma função do sistema de site opcional, mas recomendável, que pode exibir relatórios relacionados a implantação e gerenciamento do cliente. Para obter mais informações, consulte [Relatórios no System Center Configuration Manager](../../../core/servers/manage/reporting.md).|  

### <a name="installation-method-dependencies"></a>Dependências do método de instalação  
 Os pré-requisitos a seguir são específicos para os diversos métodos de instalação do cliente.  

-   Instalação do cliente por push  

    -   As contas de instalação do cliente por push são usadas para conectar computadores para instalar o cliente e são especificadas na guia **Contas** da caixa de diálogo **Propriedades da Instalação do Cliente por Push** . A conta deve ser membro do grupo local de administradores no computador de destino.  

         Se você não especifica uma conta de instalação do cliente por push, a conta de computador do servidor do site é usada.  

    -   O computador no qual se está instalando o cliente precisa ter sido descoberto por ao menos um método de descoberta do Configuration Manager.  

    -   O computador tem um compartilhamento Admin$.  

    -   **Habilitar a instalação do cliente por push para recursos atribuídos** deve estar selecionado na caixa de diálogo **Propriedades da Instalação do Cliente por Push** se você deseja usar automaticamente o cliente do Configuration Manager por push para recursos descobertos.  

    -   O computador cliente deve ser capaz de contatar um ponto de distribuição ou um ponto de gerenciamento para baixar os arquivos de suporte.  

     É necessário ter as seguintes permissões de segurança para instalar o cliente do Configuration Manager usando o push de clientes:  

    -   Para configurar a conta de Instalação do Cliente por Push: permissão **Modificar** e Ler para o objeto **Site** .  

    -   Para usar o cliente por push para instalar coleções, dispositivos e consultas: permissão **Modificar Recurso** e **Ler** para o objeto de Coleção.  

     A função de segurança **Administrador de Infraestrutura** inclui as permissões necessárias para gerenciar a instalação do cliente por push.  

-   Instalação baseada em ponto de atualização de software  

    -   Se o esquema do Active Directory não foi estendido ou você está instalando clientes de outra floresta, as propriedades da instalação para o CCMSetup.exe devem ser provisionadas no Registro do computador usando a Política de Grupo. Para obter mais informações, consulte  [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

    -   O cliente do Configuration Manager deve ser publicado no ponto de atualização de software.  

    -   O computador cliente deve ser capaz de contatar um ponto de distribuição ou um ponto de gerenciamento a fim de baixar os arquivos de suporte.  

     Para conhecer as permissões de segurança necessárias para gerenciar atualizações de software do Configuration Manager, consulte [Pré-requisitos para atualizações de software no System Center Configuration Manager](../../../sum/plan-design/prerequisites-for-software-updates.md).  

-   Instalação baseada na Política de Grupo  

    -   Se o esquema do Active Directory não foi estendido ou você está instalando clientes de outra floresta, as propriedades da instalação para o CCMSetup.exe devem ser provisionadas no Registro do computador usando a Política de Grupo. Para obter mais informações, consulte  [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

    -   O computador cliente deve ser capaz de contatar um ponto de gerenciamento para baixar os arquivos de suporte.  

-   Instalação baseada em script de logon  

     O computador cliente deve conseguir contatar um ponto de distribuição ou um ponto de gerenciamento a fim de baixar os arquivos de suporte a menos que, no prompt de comando, você especificou o CCMSetup.exe com a propriedade de linha de comando **ccmsetup /source**.  

-   Instalação manual  

     O computador cliente deve conseguir contatar um ponto de distribuição ou um ponto de gerenciamento a fim de baixar os arquivos de suporte a menos que, no prompt de comando, você especificou o CCMSetup.exe com a propriedade de linha de comando **ccmsetup /source**.  

-   Instalação de computador do grupo de trabalho  

     Para acessar recursos no domínio de servidor do site do Configuration Manager, a conta de acesso à rede deve ser configurada para o site.  

     Para obter mais informações sobre como configurar a Conta de Acesso à Rede, consulte [Conceitos fundamentais para o gerenciamento de conteúdo no System Center Configuration Manager](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   Instalação baseada em distribuição de software (somente para atualizações)  

    -   Se o esquema do Active Directory não foi estendido ou você está instalando clientes de outra floresta, as propriedades da instalação para o CCMSetup.exe devem ser provisionadas no Registro do computador usando a Política de Grupo. Para obter mais informações, consulte [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

    -   O computador cliente deve ser capaz de contatar um ponto de distribuição ou um ponto de gerenciamento para baixar os arquivos de suporte.  

     Para conhecer as permissões de segurança necessárias para atualizar o cliente do Configuration Manager usando o gerenciamento de aplicativos, consulte [Segurança e privacidade para gerenciamento de aplicativos no Configuration Manager](../../../apps/plan-design/security-and-privacy-for-application-management.md).  

-   Atualizações automáticas do cliente  

     Você deve ser um membro da função de segurança **Administrador Completo** para configurar atualizações automáticas do cliente.  

### <a name="firewall-requirements"></a>Requisitos de firewall  
 Se houver um firewall entre os servidores de sistema de site e os computadores nos quais você quer instalar o cliente do Configuration Manager, consulte [Configurações do Firewall do Windows e de porta para computadores cliente no System Center Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md).  

##  <a name="a-namebkmkprereqsmobiledevicesa-prerequisites-for-mobile-device-clients"></a><a name="BKMK_prereqs_mobiledevices"></a> Pré-requisitos para clientes de dispositivos móveis  
 Use as informações a seguir para determinar os pré-requisitos ao instalar o cliente do Configuration Manager em dispositivos móveis e use o Configuration Manager para registrá-los.  

### <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  

-   Uma AC (autoridade de certificação) corporativa com modelos de certificado para implantar e gerenciar os certificados necessários para dispositivos móveis.  

     Uma AC emissora deve aprovar automaticamente as solicitações de certificados de usuários de dispositivos móveis durante o processo de registro.  

     Para obter mais informações sobre os requisitos de certificado, consulte [Segurança e privacidade de perfis de certificado no System Center Configuration Manager](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md).  

-   Um grupo de segurança que contém os usuários que podem registrar seus dispositivos móveis.  

     Esse grupo de segurança é usado para configurar o modelo de certificado usado durante o registro do dispositivo móvel.  

-   Opcional, mas recomendado: um alias DNS (registro CNAME) denominado **ConfigMgrEnroll** configurado para o nome do servidor do sistema de sites em que você instalar o ponto proxy do registro.  

     Este alias DNS é necessário para dar suporte à descoberta automática para o serviço de registro: se você não configurar esse registro DNS, os usuários deverão especificar manualmente o nome do servidor de sistema de site para o ponto proxy do registro como parte do processo de registro.  

-   Dependências da função do sistema de site para computadores que executam as funções do sistema de site do ponto de registro e do ponto proxy do registro.  

     Consulte [Sistemas operacionais com suporte para servidores de sistema de sites](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).  

### <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  
 Para obter mais informações sobre as seguintes funções de sistema de sites, consulte [Adicionar as funções do sistema de sites para os clientes do System Center Configuration Manager](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

-   Ponto de gerenciamento que está configurado para conexões de clientes HTTP e habilitado para dispositivos móveis  

     Um ponto de gerenciamento é sempre necessário para instalar o cliente do Configuration Manager em dispositivos móveis. Além dos requisitos de configuração do HTTPS e de estar habilitado para dispositivos móveis, o ponto de gerenciamento deve ser configurado com um FQDN de Internet e deve aceitar conexões de cliente da Internet.  

-   Ponto de registro e ponto proxy do registro  

     O ponto proxy do registro gerencia as solicitações de registro dos dispositivos móveis e o ponto de registro conclui o processo de registro. O ponto de registro deve estar na mesma floresta do Active Directory que o servidor do site, mas o ponto proxy do registro pode estar em outra floresta.  

-   Configurações do cliente para registro do dispositivo móvel  

     Defina as configurações de cliente para permitir que os usuários registrem dispositivos móveis e configurem pelo menos um perfil de registro.  

-   Ponto do Reporting Services  

     O ponto do Reporting Services é uma função do sistema de site opcional, mas recomendada, que pode exibir relatórios relacionados ao registro de dispositivo móvel e gerenciamento de clientes.  

     Para obter mais informações, consulte [Relatórios no System Center Configuration Manager](../../../core/servers/manage/reporting.md).  

-   Para configurar o registro para dispositivos móveis, você deve ter as seguintes permissões de segurança:  

    -   Para adicionar, modificar e excluir as funções do sistema de site de registro: permissão **Modificar** para o objeto **Site** .  

    -   Para definir as configurações de cliente para registro: as configurações de cliente padrão exigem a permissão **Modificar** para o objeto de **Site** , e as configurações de cliente personalizadas exigem as permissões de **Agente cliente**  .  

     A função de segurança **Administrador Completo** inclui as permissões necessárias para configurar as funções do sistema de site de registro.  

     Para gerenciar os dispositivos móveis inscritos, você deve ter as seguintes permissões de segurança:  

    -   Para apagar ou desativar um dispositivo móvel: **Excluir recurso** para o objeto de **Coleção** .  

    -   Para cancelar um comando apagar ou desativar: **Excluir recurso** para o objeto de **Coleção** .  

    -   Para permitir e bloquear dispositivos móveis: **Modificar recurso** para o objeto de **Coleção** .  

    -   Para um bloqueio remoto ou redefinição de senha em um dispositivo móvel: **Modificar** recurso para o objeto de **Coleção** .  

     A função de segurança **Administrador de Operações** inclui as permissões necessárias para gerenciar dispositivos móveis.  

     Para obter mais informações sobre como configurar as permissões de segurança, veja [Fundamentals of role-based administration for System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md) e  [Configure role-based administration for System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md).  

### <a name="firewall-requirements"></a>Requisitos de firewall  
 Os dispositivos de rede intermediária, como roteadores e firewalls, e Windows Firewall, se aplicável, devem permitir o tráfego associado ao registro de dispositivo móvel:  

-   Entre os dispositivos móveis e o ponto proxy do registro: HTTPS (por padrão, TCP 443)  

-   Entre o ponto proxy do registro e o ponto de registro: HTTPS (por padrão, TCP 443)  

 Se você usar um servidor Web proxy, ele deverá ser configurado para túnel SSL; a ponte SSL não tem suporte para dispositivos móveis.  



<!--HONumber=Nov16_HO1-->


