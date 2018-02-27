---
title: "Configurações do cliente"
titleSuffix: Configuration Manager
description: "Escolha as configurações do cliente usando o console de administração no System Center Configuration Manager."
ms.custom: na
ms.date: 01/05/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
caps.latest.revision: 
caps.handback.revision: 
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: dddfde242a67a0b4a9311c0fb6f0b2f0e6742cc2
ms.sourcegitcommit: fbd4a9d2fa8ed4ddd3a0fecc4a2ec4fc0ccc3d0c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/19/2018
---
# <a name="about-client-settings-in-system-center-configuration-manager"></a>Sobre as configurações do cliente no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Gerencie todas as configurações de cliente no console do Configuration Manager por meio do nó **Configurações de Cliente** no espaço de trabalho **Administração**. O Configuration Manager é fornecido com um conjunto de configurações padrão. Quando você altera as configurações padrão do cliente, essas configurações são aplicadas a todos os clientes na hierarquia. Você também pode configurar configurações personalizadas do cliente, que substituem as configurações padrão do cliente ao atribuí-las a coleções. Para obter mais informações, consulte [Como definir as configurações de cliente](../../../core/clients/deploy/configure-client-settings.md).

As seções a seguir descrevem as configurações e as opções com mais detalhes.  
 

## <a name="background-intelligent-transfer-service-bits"></a>BITS (Serviço de Transferência Inteligente em Segundo Plano)  

### <a name="limit-the-maximum-network-bandwidth-for-bits-background-transfers"></a>Limitar a largura de banda de rede máxima para transferências em segundo plano do BITS
Quando essa opção é **Sim**, os clientes usam a limitação da largura de banda do BITS. Para definir as outras configurações nesse grupo, é necessário habilitar essa configuração. 

### <a name="throttling-window-start-time"></a>Hora de início do período de limitação
Especifique a hora de início local para o período de limitação do BITS.  

### <a name="throttling-window-end-time"></a>Hora de término do período de limitação
Especifique a hora de início final para o período de limitação do BITS. Se a hora de término for igual a **Hora de início do período de limitação**, a limitação do BITS sempre estará habilitada.  

### <a name="maximum-transfer-rate-during-throttling-window-kbps"></a>Taxa de transferência máxima durante o período de limitação (Kbps)
Especifique a taxa de transferência máxima que pode ser usada pelos clientes durante o período.  

### <a name="allow-bits-downloads-outside-the-throttling-window"></a>Permitir downloads de BITS fora do período de limitação
Permita que os clientes usem configurações de BITS separadas fora da janela especificada.  

### <a name="maximum-transfer-rate-outside-the-throttling-window-kbps"></a>Taxa de transferência máxima fora do período de limitação (Kbps)
Especifique a taxa de transferência máxima que os clientes podem usar fora da janela de limitação do BITS.  



## <a name="client-cache-settings"></a>Configurações de cache do cliente

### <a name="configure-branchcache"></a>Configurar o BranchCache
Configure o computador cliente para o [Windows BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache). Para permitir o armazenamento em cache do BranchCache no cliente, defina **Habilitar o BranchCache** como **Sim**.

- **Habilitar o BranchCache** </br>
    Habilite o BranchCache nos computadores cliente.

- **Tamanho máximo do cache do BranchCache (percentual do disco)** </br>
    O percentual do disco que é permitido que o BranchCache use. 

### <a name="configure-client-cache-size"></a>Configurar o tamanho do cache do cliente
O cache do cliente do Configuration Manager em computadores Windows armazena arquivos temporários usados para instalar aplicativos e programas. Se essa opção for definido como **Não**, o tamanho padrão será 5.120 MB.

Se escolher **Sim**, em seguida, especifique:
- **Tamanho máximo de cache (MB)**
- **Tamanho máximo do cache (percentual do disco)** </br>
O tamanho do cache do cliente expande até o tamanho máximo em MB (megabytes) ou o percentual do disco, o que for menor. 

### <a name="enable-configuration-manager-client-in-full-os-to-share-content"></a>Habilitar cliente do Configuration Manager em um SO completo para compartilhar conteúdo
Habilite o [cache par](/sccm/core/plan-design/hierarchy/client-peer-cache) para clientes do Configuration Manager. Escolha **Sim** e, em seguida, especifique a porta pela qual o cliente se comunica com o computador par. 
- **Porta para difusão de rede inicial** (padrão 8004)
- **Porta para download de conteúdo do par** (padrão 8003) </br>
O Configuration Manager configura automaticamente as regras do Firewall do Windows para permitir esse tráfego. Se você usar um firewall diferente, deverá configurar manualmente as regras para permitir esse tráfego.




## <a name="client-policy"></a>Política do cliente  

### <a name="client-policy-polling-interval-minutes"></a>Intervalo de sondagem da política do cliente (minutos)

Especifica a frequência com que os seguintes clientes do Configuration Manager baixam a política do cliente:
-   Computadores Windows (por exemplo, desktops, servidores, laptops)  
-   Dispositivos móveis registrados pelo Configuration Manager  
-   Computadores Mac  
-   Computadores que executam o Linux ou UNIX  

### <a name="enable-user-policy-on-clients"></a>Habilitar política de usuário em clientes

Quando você define essa opção como **Sim** e usa a [descoberta de usuário](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser), os clientes recebem aplicativos e programas direcionados ao usuário conectado.  

O Catálogo de Aplicativos recebe a lista de softwares disponíveis para usuários do servidor do site. Assim, essa configuração não precisa ser **Sim** para que os usuários vejam e solicitem aplicativos do Catálogo de Aplicativos. Se essa configuração for **Não**, os seguintes comportamentos não funcionarão quando os usuários usarem o Catálogo de Aplicativos:  

-   Os usuários não podem instalar os aplicativos que veem no Catálogo de Aplicativos.  

-   Os usuários não veem as notificações sobre suas solicitações de aprovação de aplicativo. Em vez disso, eles devem atualizar o catálogo de aplicativos e verificar o status de aprovação.  

-   Os usuários não recebem as revisões e atualizações para aplicativos publicadas no Catálogo de Aplicativos. O usuários veem as alterações nas informações do aplicativo no Catálogo de Aplicativos.  

-   Se você remover uma implantação de aplicativo depois que o cliente instalar o aplicativo por meio do Catálogo de Aplicativos, os clientes continuarão verificando se o aplicativo está instalado por até dois dias.  

Além disso, se essa configuração for **Não**, os usuários não receberão os aplicativos obrigatórios implantados em usuários. Os usuários também não recebem outras tarefas de gerenciamento em políticas de usuário.  

Essa configuração se aplica aos usuários quando o computador está na intranet ou Internet. Ela deverá ser **Sim** se você desejar habilitar políticas de usuário pela Internet.  

### <a name="enable-user-policy-requests-from-internet-clients"></a>Ativar solicitações de política de usuário de clientes da Internet

Defina isso como **Sim** para que os usuários recebam a política de usuário em computadores baseados na Internet. Os seguintes requisitos também se aplicam:  

-   O cliente e o site são configurados para o gerenciamento de clientes baseado na Internet.

-   A configuração **Habilitar política de usuário em clientes** é **Sim**.  

-   O ponto de gerenciamento baseado na Internet autentica com êxito o usuário usando a autenticação do Windows (Kerberos ou NTLM).  

Se você definir essa opção como **Não** ou se um dos requisitos anteriores não forem atendidos, um computador na Internet receberá somente as políticas do computador. Nesse cenário, os usuários ainda podem ver, solicitar e instalar aplicativos de um catálogo de aplicativos baseados na Internet. Se essa configuração for **Não**, mas **Habilitar política de usuário em clientes** for **Sim**, os usuários não receberão as políticas de usuário até que o computador esteja conectado à intranet.  

Para saber mais sobre como gerenciar clientes na Internet, consulte [Considerações sobre a comunicação do cliente pela Internet ou por uma floresta não confiável](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

> [!NOTE]  
>  As solicitações de aprovação de aplicativo dos usuários não exigem autenticação de usuário nem políticas de usuário.  


## <a name="cloud-services"></a>Serviços de Nuvem

### <a name="allow-access-to-cloud-distribution-point"></a>Permitir acesso ao ponto de distribuição na nuvem
Defina isso como **Sim** para que os clientes obtenham o conteúdo de um ponto de distribuição na nuvem. Essa configuração não exige que o dispositivo seja baseado na Internet.

### <a name="automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory"></a>Registrar automaticamente novos dispositivos ingressados em domínio do Windows 10 com o Azure Active Directory 
Quando você configura o Azure Active Directory para dar suporte à junção híbrida, o Configuration Manager configura dispositivos Windows 10 para essa funcionalidade. Para obter mais informações, consulte [Como configurar dispositivos híbridos ingressados no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).

### <a name="enable-clients-to-use-a-cloud-management-gateway"></a>Habilitar clientes a usarem um gateway de gerenciamento de nuvem
Por padrão, todos os clientes de roaming na Internet usam qualquer [gateway de gerenciamento de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway) disponível. Um exemplo de quando definir essa configuração como **Não** é para definir o escopo do uso do serviço, como durante um projeto piloto ou para economizar custos.



##  <a name="compliance-settings"></a>Configurações de conformidade  

### <a name="enable-compliance-evaluation-on-clients"></a>Habilitar a avaliação de conformidade em clientes
Defina isso como **Sim** para definir as outras configurações nesse grupo.
 
### <a name="schedule-compliance-evaluation"></a>Agendar a avaliação da conformidade
Selecione **Agendamento** para criar o agendamento padrão para as implantações de linha de base de configuração. Esse valor é configurável para cada linha de base na caixa de diálogo **Implantar Linha de Base de Configuração**.  

### <a name="enable-user-data-and-profiles"></a>Habilitar perfis e dados do usuário
Escolha **Sim** se deseja implantar itens de configuração de [perfis e dados de usuário](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md).



## <a name="computer-agent"></a>Agente de Computador  

### <a name="user-notifications-for-required-deployments"></a>Notificações do usuário para implantações necessárias

Para obter mais informações sobre as três seguintes configurações, consulte [Notificações do usuário para implantações obrigatórias](/sccm/apps/deploy-use/deploy-applications#user-notifications-for-required-deployments):

-   **Data limite de implantação superior a 24 horas, lembrar o usuário a cada (horas)**
-   **Data limite de implantação inferior a 24 horas, lembrar o usuário a cada (horas)** 
-   **Data limite de implantação inferior a 1 hora, lembrar o usuário a cada (minutos)** 

### <a name="default-application-catalog-website-point"></a>Ponto de sites da Web do Catálogo de Aplicativos padrão

O Configuration Manager usa essa configuração para conectar usuários ao Catálogo de Aplicativos do Centro de Software. Selecione **Definir Site** para especificar um servidor que hospeda o ponto de sites da Web do Catálogo de Aplicativos. Insira seu nome NetBIOS ou FQDN, especifique a detecção automática ou uma URL para implantações personalizadas. Na maioria dos casos, a detecção automática é a melhor opção porque oferece os seguintes benefícios:  

-   Se o site tiver um ponto de sites da Web do Catálogo de Aplicativos, os clientes receberão automaticamente um ponto de sites da Web do Catálogo de Aplicativos em seus sites.  

-   O cliente prefere pontos de sites da Web do Catálogo de Aplicativos habilitados para HTTPS na intranet em servidores somente HTTP. Essa funcionalidade ajuda a proteger contra um servidor não autorizado.

-   O ponto de gerenciamento fornece um ponto de sites da Web do Catálogo de Aplicativos baseado na Internet a clientes baseados na Internet. O ponto de gerenciamento fornece um ponto de sites da Web do Catálogo de Aplicativos baseado na intranet a clientes baseados na intranet.  

A detecção automática não garante que os clientes receberão o ponto de sites da Web do Catálogo de Aplicativos mais próximo. Você pode decidir por não usar a **Detecção automática** pelos seguintes motivos:  

-   Você deseja configurar manualmente o servidor mais próximo para clientes ou garantir que eles não se conectem a um servidor em uma conexão de rede lenta.  

-   Você deseja controlar quais clientes se conectam a qual servidor. Essa configuração pode ser por motivos comerciais, de desempenho ou teste.  

-   Você não quer esperar até 25 horas ou uma alteração de rede para que os clientes usem outro ponto de sites da Web do Catálogo de Aplicativos.  

Se você especificar o ponto de sites da Web do catálogo de aplicativos em vez de usa a detecção automática, especifique o nome NetBIOS em vez do FQDN da intranet. Essa configuração reduz a probabilidade de que o navegador da Web solicite aos usuários as credenciais quando ele acessar um Catálogo de Aplicativos baseado na intranet. Para usar o nome NetBIOS, as seguintes condições devem ser aplicáveis:  

-   O nome NetBIOS é especificado nas propriedades do ponto de sites da Web do catálogo de aplicativos.  

-   Você usa o WINS ou todos os clientes estão no mesmo domínio do ponto de sites da Web do catálogo de aplicativos.  

-   Configure o ponto de sites da Web do Catálogo de Aplicativos para conexões do cliente HTTP ou configure o servidor para HTTPS e o certificado do servidor Web contém o nome NetBIOS.  

Geralmente, os usuários apresentam credenciais quando a URL contém um FQDN, mas não quando a URL é um nome NetBIOS. Espere que os usuários sempre sejam solicitados quando eles se conectam à Internet, pois essa conexão deve usar o FQDN de Internet. Para um cliente baseado na Internet, quando o navegador da Web solicita aos usuários as credenciais, verifique se o ponto de Sites da Web do Catálogo de Aplicativos pode se conectar a um controlador de domínio para a conta do usuário. Essa configuração permite que o usuário seja autenticado usando o Kerberos.  

> [!NOTE]  
>  Eis como funciona a detecção automática:  
>   
>  O cliente faz uma solicitação de local de serviço para um ponto de gerenciamento. Se houver um ponto de sites da Web do catálogo de aplicativos no mesmo site do cliente, o servidor é fornecido ao cliente como o servidor do catálogo de aplicativos a ser usado. Quando mais de um ponto de sites da Web do catálogo de aplicativos está disponível no site, um servidor habilitado para HTTPS tem prioridade sobre um servidor não habilitado para HTTPS. Após esta filtragem, todos os clientes recebem um dos servidores para serem usados como Catálogo de Aplicativos. O Configuration Manager não faz balanceamento de carga entre vários servidores. Quando o site do cliente não contém um ponto de sites da Web do catálogo de aplicativos, o ponto de gerenciamento retorna de forma não determinística um ponto de sites da Web do catálogo de aplicativos da hierarquia.  
>   
>  Para clientes baseados na intranet, se você configurar o ponto de sites da Web do Catálogo de Aplicativos com um nome NetBIOS para a URL do Catálogo de Aplicativos, o ponto de gerenciamento usa isso. Ele não usa o FQDN da intranet. Para clientes baseados na Internet, o ponto de gerenciamento só fornece o FQDN da Internet ao cliente.  
>   
>  O cliente faz a solicitação de local de serviço a cada 25 horas ou sempre que detecta uma alteração de rede. Por exemplo, se o cliente muda da intranet para a Internet, isso é uma mudança de rede. Se o cliente localizar um ponto de gerenciamento baseado na Internet, o ponto de gerenciamento baseado na Internet fornece servidores de ponto de sites da Web do Catálogo de Aplicativos baseados na Internet para os clientes.  

### <a name="add-default-application-catalog-website-to-internet-explorer-trusted-sites-zone"></a>Adicionar sites da Web do Catálogo de Aplicativos padrão à zona de sites confiáveis do Internet Explorer

Se essa opção for **Sim**, o cliente adicionará automaticamente a URL padrão atual do site do Catálogo de Aplicativos à zona de sites confiáveis do Internet Explorer.  

Essa definição garante que a configuração do Internet Explorer para Modo Protegido não está habilitada. Se o Modo Protegido estiver habilitado, o cliente do Configuration Manager poderá não conseguir instalar aplicativos do Catálogo de Aplicativos. Por padrão, a zona de sites confiáveis oferece suporte à entrada de usuário para o catálogo de aplicativos, o que requer autenticação do Windows.  

Se você deixar essa opção como **Não**, o cliente do Configuration Manager poderá não conseguir instalar aplicativos por meio do Catálogo de Aplicativos. Um método alternativo é definir essas configurações do Internet Explorer em outra zona para a URL do Catálogo de Aplicativos usada pelos clientes.  

> [!NOTE]  
>  Sempre que o Configuration Manager adiciona uma URL de Catálogo de Aplicativos padrão à zona de sites confiáveis, ele remove as URLs do Catálogo de Aplicativos adicionadas anteriormente.  
>   
>  Se a URL já estiver especificada em uma das zonas de segurança, o Configuration Manager não poderá adicionar a URL. Nesse cenário, você deve remover a URL da outra zona ou definir manualmente as configurações necessárias do Internet Explorer.  

### <a name="allow-silverlight-applications-to-run-in-elevated-trust-mode"></a>Permitir que os aplicativos Silverlight sejam executados no modo de confiança elevada

Essa configuração deve ser **Sim** para que os usuários usem o Catálogo de Aplicativos.  

Se você alterar essa configuração, ela terá efeito quando o usuário carregar o navegador da próxima vez ou atualizar a janela do navegador aberta no momento.  

Para obter mais informações sobre essa configuração, consulte [Certificados para o Microsoft Silverlight 5 e modo de confiança elevada necessários para o catálogo de aplicativos](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5).  

### <a name="organization-name-displayed-in-software-center"></a>Nome da organização exibido no Centro de Software

Digite o nome que os usuários veem no Centro de Software. Essa informação de identidade visual ajuda os usuários a identificarem este aplicativo como uma fonte confiável.  

### <a name="use-new-software-center"></a>Usar o novo Centro de Software

Se você definir isso como **Sim**, todos os computadores clientes usam o Centro de Software. O Centro de Software mostra os aplicativos disponíveis para o usuário que estavam acessíveis anteriormente apenas no Catálogo de Aplicativos. O Catálogo de Aplicativos exige o Silverlight, que não é um pré-requisito para o Centro de Software.   

As funções do sistema de sites do ponto de sites da Web do catálogo de aplicativos e do ponto de serviços Web do catálogo de aplicativos ainda são necessárias para que os aplicativos disponíveis para o usuário sejam exibidos no Centro de Software.  

Para obter mais informações, consulte [Plan for and configure application management (Planejar e configurar o gerenciamento de aplicativos)](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

### <a name="enable-communication-with-health-attestation-service"></a>Habilitar comunicação com o Serviço de Atestado de Integridade

Defina isso como **Sim** para que os dispositivos Windows 10 usem o [Atestado de integridade](/sccm/core/servers/manage/health-attestation). Quando você habilitar essa configuração, a configuração a seguir também estará disponível para configuração.

### <a name="use-on-premises-health-attestation-service"></a>Usar o Serviço de Atestado de Integridade local

Defina isso como **Sim** para que os dispositivos usem um serviço local. Defina como **Não** para que os dispositivos usem o serviço da Microsoft baseado em nuvem.  

### <a name="install-permissions"></a>Permissões de instalação

> [!IMPORTANT]  
>  Essa configuração aplica-se o Centro de Software e ao Catálogo de Aplicativos. Essa configuração não tem nenhum efeito quando os usuários usam o Portal da Empresa.  

Configure como os usuários podem iniciar a instalação de software, as atualizações de software e as sequências de tarefas:  

-   **Todos os Usuários**: os usuários com qualquer permissão, exceto Convidado.  

-   **Somente Administradores**: os usuários devem ser membros do grupo local de Administradores.  

-   **Somente Administradores e usuários primários**: os usuários devem ser membros do grupo local de Administradores ou um usuário primário no computador.  

-   **Nenhum Usuário**: nenhum usuário conectado a um computador cliente pode iniciar a instalação de software, as atualizações de software e as sequências de tarefas. Implantações obrigatórias para o computador são sempre instaladas na data limite. Os usuários não podem iniciar a instalação do software usando o Catálogo de Aplicativos ou o Centro de Software.  

### <a name="suspend-bitlocker-pin-entry-on-restart"></a>Suspender a entrada de PIN do BitLocker na reinicialização

Se os computadores exigirem a entrada de PIN do BitLocker, essa opção ignorará o requisito de inserção de um PIN quando o computador for reiniciado após uma instalação de software.  

-   **Sempre**: o Configuration Manager suspende temporariamente o BitLocker após ele ter instalado um software que exige reinicialização e ter iniciado a reinicialização do computador. Essa configuração se aplica somente a uma reinicialização do computador iniciada pelo Configuration Manager. Essa configuração não suspende o requisito de inserção de PIN do BitLocker quando o usuário reinicia o computador. O requisito de entrada de PIN do BitLocker é retomado após a inicialização do Windows.

-   **Nunca**: o Configuration Manager não suspende o BitLocker após ter instalado o software que exige a reinicialização. Nesse cenário, a instalação do software não pode terminar até que o usuário insira o PIN para concluir o processo de inicialização padrão e carregar o Windows.

### <a name="additional-software-manages-the-deployment-of-applications-and-software-updates"></a>O software adicional gerencia a implantação de aplicativos e as atualizações de software

Habilite essa opção somente se uma das seguintes condições forem aplicáveis:  

-   Você usa uma solução de fornecedor que requer que essa configuração seja habilitada.  

-   Você usa o SDK (Software Development Kit) do Configuration Manager para gerenciar notificações do agente cliente e a instalação de atualizações de aplicativos e software.  

> [!WARNING]  
>  Se você escolher essa opção quando nenhuma dessas condições for aplicável, o cliente não instalará as atualizações de software e os aplicativos obrigatórios. Essa configuração não impede que os usuários instalem aplicativos por meio do Catálogo de Aplicativos nem a instalação de pacotes, programas e sequências de tarefas.  

### <a name="powershell-execution-policy"></a>Política de execução do PowerShell

Configurar como os clientes do Configuration Manager podem executar scripts do Windows PowerShell. Você pode usar esses scripts para detecção e configuração de itens em configurações de conformidade. Você também pode enviar os scripts em uma implantação como um script padrão.  

-   **Ignorar**: o cliente do Configuration Manager ignora a configuração do Windows PowerShell no computador cliente para que os scripts não assinados possam ser executados.  

-   **Restrito**: o cliente do Configuration Manager usa a configuração atual do PowerShell no computador cliente. Essa configuração determina se é possível executar scripts não assinados.  

-   **Tudo Assinado**: o cliente do Configuration Manager executará scripts apenas se forem assinados por um fornecedor confiável. Essa restrição aplica-se, independentemente da configuração atual do PowerShell no computador cliente.  

Essa opção exige no mínimo a versão do Windows PowerShell 2.0. O padrão é todos **Tudo Assinado**.  

> [!TIP]  
>  Se os scripts não assinados não forem executados devido a essa configuração do cliente, o Configuration Manager relatará esse erro das seguintes maneiras:  
>   
> -   O espaço de trabalho **Monitoramento** no console exibe a ID de erro de estado de implantação **0x87D00327**. Ele também exibe a descrição **O script não está assinado**.  
> -   Os relatórios exibem o tipo **Erro de descoberta**. Em seguida, os relatórios exibem o tipo de erro **0x87D00327** e a descrição **O script não está assinado** ou o código de erro **0x87D00320** e a descrição **O host de script ainda não foi instalado**. Um relatório de exemplo é **Detalhes de erros de itens de configuração em uma linha de base de configuração para um ativo**.  
> -   O arquivo **DcmWmiProvider.log** exibe a mensagem **O script não está assinado (erro: 87D00327; fonte: CCM)**.  

### <a name="show-notifications-for-new-deployments"></a>Mostrar notificações para novas implantações

Escolha **Sim** para exibir uma notificação para implantações disponíveis em menos de uma semana. Essa mensagem é exibida sempre que o agente cliente é iniciado.

### <a name="disable-deadline-randomization"></a>Desabilitar data limite aleatória

Após a data limite da implantação, essa configuração determina se o cliente usa um atraso de ativação de até duas horas para instalar as atualizações de software obrigatórias. Por padrão, o atraso de ativação está desabilitado.  

Para cenários de VDI (Virtual Desktop Infrastructure), esse atraso ajuda a distribuir o processamento da CPU e a transferência de dados para um computador host com várias máquinas virtuais. Mesmo que você não use VDI, ter muitos clientes instalando as mesmas atualizações ao mesmo tempo pode aumentar negativamente o uso da CPU no servidor do site. Esse comportamento também pode causar lentidão nos pontos de distribuição e reduzir significativamente a largura de banda de rede disponível.  

Se os clientes precisarem instalar as atualizações de software obrigatórias até a data limite de implantação sem atraso, defina essa configuração como **Sim**. 

### <a name="grace-period-for-enforcement-after-deployment-deadline-hours"></a>Período de carência para a imposição após a data limite da implantação (horas)

Caso deseje oferecer aos usuários mais tempo para instalar as implantações de atualização de software ou os aplicativos obrigatórios além da data limite, defina isso como **Sim**. Esse período de carência destina-se a um computador desativado por um período estendido e o usuário precisa instalar vários aplicativos ou implantações de atualização. Por exemplo, essa configuração é útil se um usuário retorna de férias e precisa esperar muito tempo enquanto o cliente instala as implantações de aplicativo vencidas. 

Defina um período de carência entre 1 e 120 horas. Use essa configuração em conjunto com a propriedade de implantação **Atrasar a imposição dessa implantação de acordo com as preferências do usuário**. Para obter informações, confira [Deploy applications](/sccm/apps/deploy-use/deploy-applications) (Implantar aplicativos).


##  <a name="computer-restart"></a>Reinicialização do computador  
As configurações a seguir devem ter uma duração mais curta do que a menor janela de manutenção aplicada ao computador.  

-   **Exibir uma notificação temporária para o usuário que indica o intervalo antes que o usuário seja desconectado ou o computador seja reiniciado (minutos)**
-   **Exibir uma caixa de diálogo que o usuário não pode fechar, que exibe o intervalo de contagem regressiva antes que o usuário seja desconectado ou o computador seja reiniciado (minutos)**

Para obter mais informações sobre as janelas de manutenção, consulte [Como usar janelas de manutenção no System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).

##  <a name="endpoint-protection"></a>Endpoint Protection  
>  [!Tip]   
> Além das informações a seguir, você pode encontrar detalhes de como usar as configurações do cliente do Endpoint Protection no [Cenário de exemplo: usar o System Center Endpoint Protection para proteger os computadores contra malware no System Center Configuration Manager](/sccm/protect/deploy-use/scenarios-endpoint-protection).

### <a name="manage-endpoint-protection-client-on-client-computers"></a>Gerenciar o cliente Endpoint Protection em computadores cliente

Escolha **Sim** se deseja gerenciar clientes existentes do Endpoint Protection e do Windows Defender em computadores da hierarquia.  

Escolha esta opção se você já tiver instalado o cliente Endpoint Protection e desejar gerenciá-lo com o Configuration Manager. Essa instalação separada inclui um processo com script que usa um aplicativo do Configuration Manager ou um pacote e programa.

### <a name="install-endpoint-protection-client-on-client-computers"></a>Instalar o cliente do Endpoint Protection em computadores cliente

Escolha **Sim** para instalar e habilitar o cliente Endpoint Protection em computadores cliente que ainda não executam o cliente.  

> [!NOTE]  
>  Se o cliente do Endpoint Protection já estiver instalado, escolher **Não** não o desinstalará. Para desinstalar o cliente do Endpoint Protection, defina a configuração do cliente **Gerenciar cliente do Endpoint Protection em computadores cliente** como **Não**. Em seguida, implante um pacote e programa para desinstalar o cliente do Endpoint Protection.  

### <a name="automatically-remove-previously-installed-antimalware-software-before-endpoint-protection-is-installed"></a>Remover automaticamente software antimalware já instalado antes que o Endpoint Protection seja instalado

Defina isso como **Sim** para que o cliente do Endpoint Protection tente desinstalar outros aplicativos antimalware. Vários clientes de antimalware no mesmo dispositivo podem entrar em conflito e afetar o desempenho do sistema.

### <a name="allow-endpoint-protection-client-installation-and-restarts-outside-maintenance-windows-maintenance-windows-must-be-at-least-30-minutes-long-for-client-installation"></a>Permitir a instalação do cliente do Endpoint Protection e reiniciar fora das janelas de manutenção. As janelas de manutenção devem ter, pelo menos, 30 minutos para a instalação do cliente

Defina isso como **Sim** para substituir os comportamentos de instalação típicos por janelas de manutenção. A configuração atende aos requisitos de negócios para a prioridade de manutenção do sistema para fins de segurança. 

### <a name="for-windows-embedded-devices-with-write-filters-commit-endpoint-protection-client-installation-requires-restarts"></a>Para dispositivos Windows Embedded com filtros de gravação, confirme a instalação do cliente do Endpoint Protection (exige reinicialização)

Escolha **Sim** para desabilitar o filtro de gravação no dispositivo Windows Embedded e reiniciar o dispositivo. Essa ação confirma a instalação no dispositivo.  

Se você escolher **Não**, o cliente será instalado em uma sobreposição temporária que é limpa quando o dispositivo é reiniciado. Neste cenário, o cliente do Endpoint Protection não é instalado por completo até que outra instalação confirme as alterações no dispositivo. Essa configuração é o padrão.  

### <a name="suppress-any-required-computer-restarts-after-the-endpoint-protection-client-is-installed"></a>Suprimir qualquer reinicialização necessária do computador após o Endpoint Protection ser instalado

Escolha **Sim** para suprimir a reinicialização do computador após a instalação do cliente do Endpoint Protection.  

> [!IMPORTANT]  
>  Se o cliente do Endpoint Protection exigir uma reinicialização do computador e essa configuração for **Não**, o computador será reiniciado, independentemente das janelas de manutenção configuradas.  

### <a name="allowed-period-of-time-users-can-postpone-a-required-restart-to-complete-the-endpoint-protection-installation-hours"></a>Período de tempo permitido durante o qual os usuários podem adiar o reinício necessário para concluir a instalação do Endpoint Protection (horas)

Se uma reinicialização for necessária após a instalação do cliente do Endpoint Protection, essa configuração especificará o número de horas pelas quais os usuários podem adiar a reinicialização obrigatória. Essa configuração exige que a configuração para **Suprimir qualquer reinicialização obrigatória do computador após a instalação do Endpoint Protection** seja **Não**.  

### <a name="disable-alternate-sources-such-as-microsoft-windows-update-microsoft-windows-server-update-services-or-unc-shares-for-the-initial-definition-update-on-client-computers"></a>Desabilitar fontes alternativas (como Microsoft Windows Update, Microsoft Windows Server Update Services ou compartilhamentos UNC) para a atualização de definição inicial em computadores cliente

Escolha **Sim** se deseja que o Configuration Manager instale somente a atualização de definição inicial em computadores cliente. Essa configuração pode ser útil para evitar conexões de rede desnecessárias e reduzir a largura de banda da rede durante a instalação inicial da atualização da definição.  



##  <a name="enrollment"></a>Registro

### <a name="polling-interval-for-mobile-device-legacy-clients"></a>Intervalo de sondagem para clientes herdados de dispositivos móveis
Selecione **Definir Intervalo** para especificar o período, em minutos ou horas, durante o qual os dispositivos móveis herdados sondam para a política. Esses dispositivos incluem plataformas como Windows CE, Mac OS X e Unix ou Linux.

### <a name="polling-interval-for-modern-devices-minutes"></a>Intervalo de sondagem para dispositivos modernos (minutos)
Insira o número de minutos durante os quais os dispositivos modernos sondam para a política. Essa configuração destina-se a dispositivos Windows 10 gerenciados por meio do gerenciamento de dispositivo móvel local.

### <a name="allow-users-to-enroll-mobile-devices-and-mac-computers"></a>Permitir que os usuários registrem dispositivos móveis e computadores Mac
Para habilitar o registro baseado em usuário de dispositivos herdados, defina isso como **Sim** e, em seguida, defina a seguinte configuração:

-   **Perfil de registro** </br>
Selecione **Definir Perfil** para criar ou selecionar um perfil de registro. Para obter mais informações, consulte [Definir as configurações do cliente para o registro](/sccm/core/clients/deploy/deploy-clients-to-macs#configure-client-settings-for-enrollment).

### <a name="allow-users-to-enroll-modern-devices"></a>Permitir que os usuários registrem dispositivos modernos
Para habilitar o registro baseado em usuário de dispositivos modernos, defina isso como **Sim** e, em seguida, defina a seguinte configuração:

-   **Perfil de registro de dispositivo moderno** </br>
Selecione **Definir Perfil** para criar ou selecionar um perfil de registro. Para obter mais informações, consulte [Criar um perfil de registro que permite que os usuários registrem dispositivos modernos](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm#bkmk_createProf).



##  <a name="hardware-inventory"></a>Inventário de hardware  

### <a name="enable-hardware-inventory-on-clients"></a>Habilitar o inventário de hardware em clientes

Por padrão, essa configuração é **Sim**. Para obter mais informações, consulte [Introdução ao inventário de hardware](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).

### <a name="hardware-inventory-schedule"></a>Agenda de inventário de hardware

Selecione **Agendamento** para ajustar a frequência com que os clientes executam o ciclo de inventário de hardware. Por padrão, esse ciclo ocorre a cada sete dias.

### <a name="maximum-random-delay-minutes"></a>Atraso máximo aleatório (minutos)

Especifique o número máximo de minutos até o qual o cliente do Configuration Manager tornará aleatório o ciclo de inventário de hardware com base no agendamento definido. Essa operação aleatória em todos os clientes ajudam a balancear a carga do processamento de inventário no servidor do site. Você pode especificar qualquer valor entre 0 e 480 minutos. Por padrão, esse valor é definido como 240 minutos (4 horas).

### <a name="maximum-custom-mif-file-size-kb"></a>Tamanho máximo de arquivo MIF personalizado (KB)

Especifique o tamanho máximo, em KB (quilobytes), permitido para cada arquivo personalizado MIF (Formato de Informações de Gerenciamento) que será coletado por um cliente durante um ciclo de inventário de hardware. O agente de inventário de hardware do Configuration Manager não processa nenhum arquivo MIF personalizado que excede esse tamanho. É possível especificar um tamanho de 1 a 5.120 KB. Por padrão, esse valor é definido como 250 KB. Essa configuração não afeta o tamanho do arquivo de dados de inventário de hardware regular.  

> [!NOTE]  
>  Essa definição só está disponível nas configurações do cliente padrão.  

### <a name="hardware-inventory-classes"></a>Classes de inventário de hardware

Selecione **Definir Classes** para estender as informações de hardware coletadas dos clientes sem editar manualmente o arquivo sms_def.mof. Para obter informações, consulte [Como configurar o inventário de hardware](../../../core/clients/manage/inventory/configure-hardware-inventory.md).  

### <a name="collect-mif-files"></a>Coletar arquivos MIF

Use esta configuração para especificar se os arquivos MIF devem ser coletados de clientes Configuration Manager durante o Inventário de Hardware.  

Para que um arquivo MIF seja coletado pelo inventário de hardware, ele deve estar no local correto no computador cliente. Por padrão, os arquivos estão localizados nos seguintes caminhos:  

-   Os **arquivos IDMIF** devem estar na pasta Windows\System32\CCM\Inventory\Idmif. 

-   Os **arquivos NOIDMIF** devem estar na pasta Windows\System32\CCM\Inventory\Noidmif.

> [!NOTE]  
>  Essa definição só está disponível nas configurações do cliente padrão.

   

##  <a name="metered-internet-connections"></a>Planos de Internet Limitados  
 Gerencie como os computadores Windows 8 e posterior usam conexões limitadas com a Internet para se comunicar com o Configuration Manager. Provedores de Internet ocasionalmente cobram por quantidade de dados que você envia e recebe quando está em uma conexão de Internet limitada.  

> [!NOTE]  
>  A configuração de cliente definida não é aplicada nos seguintes cenários:  
>   
> -   Se computador estiver em uma conexão de dados em roaming, o cliente do Configuration Manager não executa tarefas que exigem que os dados sejam transferidos para sites do Configuration Manager.  
> -   Se as propriedades de conexão de rede do Windows são configuradas como ilimitadas, o cliente do Configuration Manager se comporta como se a conexão fosse ilimitada e, por isso, transfere os dados para o site.  

### <a name="client-communication-on-metered-internet-connections"></a>Comunicação de cliente em conexões de Internet limitadas

Escolha uma das seguintes opções para essa configuração:  

-   **Permitir**: todas as comunicações do cliente são permitidas pela conexão de Internet limitada, a menos que o dispositivo cliente esteja usando uma conexão de dados móvel.  

-   **Limite**: somente as seguintes comunicações do cliente são permitidas pela conexão de Internet limitada:  

    -   Recuperação de política do cliente  

    -   Mensagens de estado do cliente para enviar ao site  

    -   Solicitações de instalação de software usando o catálogo de aplicativos  

    -   Implantações necessárias (quando é atingido o prazo de instalação)  

    > [!IMPORTANT]  
    >  O cliente sempre permite instalações de software por meio do Centro de Software ou do Catálogo de Aplicativos, independentemente das configurações de conexão limitada com a Internet.  

    Se o cliente atingir o limite de transferência de dados para a conexão da Internet limitada, o cliente não tentará mais se comunicar com os sites do Configuration Manager.  

-   **Bloquear**: o cliente do Configuration Manager não tenta se comunicar com os sites do Configuration Manager quando ele está em uma conexão de Internet limitada. Esta é a opção padrão.  



##  <a name="power-management"></a>Gerenciamento de Energia  

### <a name="allow-power-management-of-devices"></a>Permitir o gerenciamento de energia de dispositivos

Defina isso como **Sim** para habilitar o gerenciamento de energia nos clientes. Para mais informações, consulte [Introdução ao gerenciamento de energia](/sccm/core/clients/manage/power/introduction-to-power-management).

### <a name="allow-users-to-exclude-their-device-from-power-management"></a>Permitir que os usuários excluam seu dispositivo do gerenciamento de energia

Escolha **Sim** para permitir que usuários do Centro de Software excluam seus computadores das configurações de gerenciamento de energia definidas.  

### <a name="enable-wake-up-proxy"></a>Habilitar proxy de ativação

Especifique **Sim** para complementar a configuração Wake On LAN do site quando estiver definida para pacotes unicast.  

Para mais informações sobre o proxy de ativação, confira [Planejar a ativação de clientes no System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

> [!WARNING]  
>  Não habilite o proxy de ativação em uma rede de produção sem primeiro entender como ele funciona e avaliá-lo em um ambiente de teste.  

Em seguida, defina as seguintes configurações adicionais, conforme necessário:

-   **Número de porta proxy de ativação (UDP)**  </br>
         O número da porta que os clientes usam para enviar pacotes de ativação para computadores suspensos. Mantenha a porta padrão 25536 ou altere o número para um valor de sua escolha.  

-   **Número de porta Wake On LAN (UDP)** </br> 
         Mantenha o valor padrão 9, a menos que você tenha alterado o número da porta Wake On LAN (UDP) na guia **Portas** das **Propriedades** do site.  

    > [!IMPORTANT]  
    >  Esse número deve corresponder ao número nas **Propriedades**do site. Se você alterar esse número em um só lugar, ele não será atualizado automaticamente em outro lugar.  

-   **Exceção do Windows Defender Firewall para proxy de ativação** </br>
         O cliente do Configuration Manager configura automaticamente o número da porta do proxy de ativação em dispositivos que executam o Windows Defender Firewall. Selecione **Configurar** para especificar os perfis de firewall desejados.

    Se os clientes executarem outro firewall, você deverá configurá-lo manualmente para permitir o **Número da porta do proxy de ativação (UDP)**.  
        
-   **Prefixos IPv6, se necessário, para DirectAccess ou outros dispositivos de rede intermediários. Use uma vírgula para especificar várias entradas** </br>
        Insira os prefixos IPv6 necessários para que o proxy de ativação funcione na rede.



##  <a name="remote-tools"></a>Ferramentas remotas  

### <a name="enable-remote-control-on-clients-and-firewall-exception-profiles"></a>Habilitar o controle remoto em clientes e Perfis de exceção do firewall

Selecione **Configurar** para habilitar o recurso de controle remoto do Configuration Manager. Outra opção é definir configurações de firewall para permitir que o controle remoto funcione em computadores cliente.  

O controle remoto está desativado por padrão.  

> [!IMPORTANT]  
>  Se as configurações de firewall não estiverem definidas, o controle remoto poderá não funcionar corretamente.  

### <a name="users-can-change-policy-or-notification-settings-in-software-center"></a>Os usuários podem alterar as configurações de política ou notificação no Centro de Software

Escolha se os usuários podem alterar as opções de controle remoto do Centro de Software.  

### <a name="allow-remote-control-of-an-unattended-computer"></a>Permitir o controle remoto de um computador autônomo

Escolha se um administrador pode usar o controle remoto para acessar um computador cliente que está desconectado ou bloqueado. Apenas um computador conectado e desbloqueado pode ser controlado remotamente quando essa configuração está desabilitada.  

### <a name="prompt-user-for-remote-control-permission"></a>Solicitar permissão de Controle Remoto ao usuário

Escolha se o computador cliente mostra uma mensagem solicitando a permissão do usuário antes de permitir uma sessão de controle remoto.  

### <a name="prompt-user-for-permission-to-transfer-content-from-shared-clipboard"></a>Solicitar ao usuário permissão para transferir conteúdo da área de transferência compartilhada

Conceda aos usuários a oportunidade de aceitar ou negar transferências de arquivo antes de transferir conteúdo da área de transferência compartilhada em uma seção de controle remoto. Os usuários precisam apenas conceder permissão uma vez por sessão e o visualizador não terá a capacidade de conceder a si mesmo a permissão de continuar a transferência de arquivo.

### <a name="grant-remote-control-permission-to-local-administrators-group"></a>Conceder permissão de Controle Remoto para o grupo local de administradores

Escolha se os administradores locais no servidor que inicia a conexão de controle remoto pode estabelecer sessões de controle remoto com computadores cliente.  

### <a name="access-level-allowed"></a>Nível de acesso permitido

Especifique o nível de acesso de controle remoto que será permitido. Escolha uma das seguintes configurações:  
- **Sem Acesso**
- **Somente Exibição**
- **Controle Total**  

### <a name="permitted-viewers-of-remote-control-and-remote-assistance"></a>Visualizadores permitidos de Controle Remoto e Assistência Remota

Selecione **Definir Visualizadores** para especificar os nomes de usuários do Windows que podem estabelecer sessões de controle remoto em computadores cliente.  

### <a name="show-session-notification-icon-on-taskbar"></a>Mostrar ícone de notificação de sessão na barra de tarefas

Defina essa configuração como **Sim** para mostrar um ícone na barra de tarefas do Windows do cliente para indicar uma sessão de controle remoto ativa.  

### <a name="show-session-connection-bar"></a>Mostrar barra de conexão da sessão

Defina isso como **Sim** para mostrar a barra de conexão de sessão de alta visibilidade em clientes para indicar uma sessão de controle remoto ativa.  

### <a name="play-a-sound-on-client"></a>Tocar um som no cliente

Selecione isso para usar som para indicar quando uma sessão de controle remoto está ativa em um computador cliente. Selecione uma das seguintes opções:
- **Sem som**
- **Início e envio de sessão** (padrão)
- **Várias vezes durante a sessão**  

### <a name="manage-unsolicited-remote-assistance-settings"></a>Gerenciar configurações de assistência remota não solicitada

Defina essa configuração como **Sim** para permitir que o Configuration Manager gerencie sessões não solicitadas da Assistência Remota.  

Em uma sessão de Assistência Remota não solicitada, o usuário no computador cliente não solicitou assistência para iniciar uma sessão.  

### <a name="manage-solicited-remote-assistance-settings"></a>Gerenciar configurações de assistência remota solicitada

Defina isso para **Sim** para permitir que o Configuration Manager gerencie sessões de assistência remota solicitada.  

Em uma sessão de Assistência Remota solicitada, o usuário no computador cliente enviou uma solicitação de assistência remota ao administrador.  

### <a name="level-of-access-for-remote-assistance"></a>Nível de acesso para assistência remota

Escolha o nível de acesso a ser atribuído às sessões de Assistência Remota iniciadas no console do Configuration Manager. Selecione uma das seguintes opções:
- **Nenhum** (padrão)
- **Exibição Remota**
- **Controle Total**

> [!NOTE]  
>  O usuário no computador cliente sempre deve conceder permissão para que uma sessão de assistência remota ocorra.  

### <a name="manage-remote-desktop-settings"></a>Gerenciar configurações da Área de Trabalho Remota

Defina isso para **Sim** para permitir que o Configuration Manager gerencie sessões da Área de Trabalho Remota para computadores.  

### <a name="allow-permitted-viewers-to-connect-by-using-remote-desktop-connection"></a>Permitir que os visualizadores autorizados se conectem usando a conexão de Área de Trabalho Remota

Defina isso como **Sim** para adicionar os usuários especificados na lista de visualizadores permitidos ao grupo local de usuários da Área de Trabalho Remota em clientes.  

### <a name="require-network-level-authentication-on-computers-that-run-windows-vista-operating-system-and-later-versions"></a>Exigir autenticação no nível da rede em computadores que executam o sistema operacional Windows Vista e versões posteriores

Defina isso como **Sim** para usar a NLA (autenticação no nível da rede) para estabelecer conexões de Área de Trabalho Remota com computadores cliente. A NLA inicialmente exige menos recursos do computador remoto, pois conclui a autenticação de usuário antes de estabelecer uma conexão de Área de Trabalho Remota. O uso da NLA é uma configuração mais segura. A NLA ajuda a proteger o computador contra usuários ou software mal-intencionados e reduz o risco de ataques de negação de serviço.  



## <a name="software-center"></a>Centro de software

### <a name="select-these-new-settings-to-specify-company-information"></a>Selecionar estas novas configurações para especificar as informações da empresa
Defina isso como **Sim** e, em seguida, especifique as seguintes configurações para criar uma identidade visual do Centro de Software para sua organização:

- **Nome da empresa** </br>
Insira o nome da organização que os usuários veem no Centro de Software.
- **Esquema de cores para o Centro de Software** </br>
Selecione **Selecionar Cor** para definir a cor primária usada pelo Centro de Software.
- **Selecionar um logotipo para o Centro de Software** </br>
Selecione **Procurar** para selecionar uma imagem a ser exibida no Centro de Software. O logotipo deve ser um JPEG, PNG ou BMP de 400 x 100 pixels com tamanho máximo de 750 KB. O nome do arquivo de logotipo não deve conter espaços. <!--SMS.503731 space in filename, noticed BMP missing as filetype-->

### <a name="software-center-tab-visibility"></a>Visibilidade da guias do Centro de Software
Defina as configurações adicionais nesse grupo como **Sim** para tornar as seguintes guias visíveis no Centro de Software:
- **Aplicativos**
- **Atualizações**
- **Sistemas Operacionais**
- **Status da Instalação**
- **Conformidade do Dispositivo**
- **Opções**

Por exemplo, caso sua organização não use políticas de conformidade e você deseje ocultar a guia Conformidade do Dispositivo no Centro de Software, defina **Habilitar guia Conformidade do Dispositivo** como **Não**.



## <a name="software-deployment"></a>Implantação de software  

### <a name="schedule-re-evaluation-for-deployments"></a>Reavaliação de agendamento para implantações
Configure um agendamento para quando o Configuration Manager reavalia as regras de requisito para todas as implantações. O valor padrão é um intervalo de sete dias.  

> [!IMPORTANT]  
>  É recomendável que você não altere esse valor para um valor menor do que o padrão. Um agendamento de reavaliação mais agressivo afeta negativamente o desempenho da rede e dos computadores cliente.  

Inicie essa ação em um cliente da seguinte maneira: no painel de controle **Configuration Manager**, na guia **Ações**, selecione **Ciclo de avaliação de implantação de aplicativo**.  



##  <a name="software-inventory"></a>Inventário de software  

### <a name="enable-software-inventory-on-clients"></a>Habilitar inventário de software em clientes

Isso é definido como **Sim** por padrão. Para obter mais informações, consulte [Introdução ao inventário de software](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).

### <a name="schedule-software-inventory-and-file-collection"></a>Agendar inventário de software e coleta de arquivos

Selecione **Agendamento** para ajustar a frequência com que os clientes executam os ciclos de inventário de software e coleta de arquivos. Por padrão, esse ciclo ocorre a cada sete dias.

### <a name="inventory-reporting-detail"></a>Detalhe no relatório de inventário

Especifique um dos seguintes níveis de informações de arquivo para o inventário:
- **Somente arquivo**
- **Somente produto**
- **Detalhes completos** (padrão)

### <a name="inventory-these-file-types"></a>Inventariar estes tipos de arquivo

Se desejar especificar os tipos de arquivo a serem inventariados, selecione **Definir Tipos** e, em seguida, configure as seguintes opções:  

> [!NOTE]  
>  Se várias configurações personalizadas do cliente forem aplicadas a um computador, o inventário retornado por cada configuração será mesclado.  

-   Selecione **Novo** para adicionar um novo tipo de arquivo ao inventário. Em seguida, especifique as seguintes informações na caixa de diálogo **Propriedades de Arquivo Inventariado**:  

    -   **Nome**: forneça um nome para o arquivo que você deseja inventariar. Use um asterisco (**&#42;**) curinga para representar qualquer cadeia de texto e um ponto de interrogação (**?**) para representar qualquer caractere único. Por exemplo, se você desejar inventariar todos os arquivos com a extensão .doc, especifique o nome do arquivo **\*.doc**.  

    -   **Local**: selecione **Definir** para abrir a caixa de diálogo **Propriedades de Caminho**. Configure o inventário de software para pesquisar o arquivo especificado em todos os discos rígidos do cliente, pesquisar um caminho especificado (por exemplo, **C:\Folder**) ou uma variável especificada (por exemplo, *%windir%*). Também é possível pesquisar todas as subpastas no caminho especificado.  

    -   **Excluir arquivos criptografados e compactados**: quando você escolhe essa opção, os arquivos compactados ou criptografados não são inventariados.  

    -   **Excluir arquivos da pasta do Windows**: quando você seleciona essa opção, os arquivos da pasta do Windows e suas subpastas não são inventariados.  

    Selecione **OK** para fechar a caixa de diálogo **Propriedades de Arquivo Inventariado**. Adicione todos os arquivos que você deseja inventariar e, em seguida, selecione **OK** para fechar a caixa de diálogo **Definir Configuração do Cliente**.  

### <a name="collect-files"></a>Coletar arquivos

Se você deseja coletar arquivos de computadores cliente, selecione **Definir Arquivos** e, em seguida, defina as seguintes configurações:  

> [!NOTE]  
>  Se várias configurações personalizadas do cliente forem aplicadas a um computador, o inventário retornado por cada configuração será mesclado.  

-   Na caixa de diálogo **Definir Configuração do Cliente**, selecione **Novo** para adicionar um arquivo a ser coletado.  

-   Na caixa de diálogo **Propriedades do Arquivo Coletado** , forneça as seguintes informações:  

    -   **Nome**: forneça um nome para o arquivo que você deseja coletar. Use um asterisco (**&#42;**) curinga para representar qualquer cadeia de texto e um ponto de interrogação (**?**) para representar qualquer caractere único.  

    -   **Local**: selecione **Definir** para abrir a caixa de diálogo **Propriedades de Caminho**. Configure o inventário de software para pesquisar o arquivo que você deseja coletar em todos os discos rígidos do cliente, pesquisar um caminho especificado (por exemplo, **C:\Folder**) ou em uma variável especificada (por exemplo, *%windir%*). Também é possível pesquisar todas as subpastas no caminho especificado.  

    -   **Excluir arquivos criptografados e compactados**: quando você escolhe essa opção, os arquivos que foram compactados ou criptografados não são coletados.  

    -   **Parar a coleta de arquivos quando o tamanho total dos arquivos exceder (KB)**: especifique o tamanho do arquivo, em KB (quilobytes), após o qual o cliente interromperá a coleta dos arquivos especificados.  

    > [!NOTE]  
    >  O servidor do site coleta as cinco versões alteradas mais recentemente de arquivos coletados e as armazena no *&lt;Diretório de instalação do ConfigMgr\>*\Inboxes\Sinv.box\Filecol. Se um arquivo não foi alterado desde o último ciclo de inventário de software, o arquivo não será coletado novamente.  
    >   
    >  O inventário de software não coleta arquivos maiores que 20 MB.  
    >   
    >  O valor **Tamanho máximo para todos os arquivos coletados (KB)** na caixa de diálogo **Definir a Configuração do Cliente** exibe o tamanho máximo para todos os arquivos coletados. Quando esse tamanho é atingido, a coleta é interrompida. Todos os arquivos já coletados são retidos e enviados para o servidor do site.  

    > [!IMPORTANT]
    >  Se você configurar o inventário de software para coletar muitos arquivos grandes, essa configuração pode afetar negativamente o desempenho da rede e do servidor do site.  

    Para obter informações sobre como exibir os arquivos coletados, consulte [Como usar o Gerenciador de Recursos para exibir o inventário de software](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    Selecione **OK** para fechar a caixa de diálogo **Propriedades do Arquivo Coletado**. Adicione todos os arquivos que você deseja coletar e, em seguida, selecione **OK** para fechar a caixa de diálogo **Definir Configuração do Cliente**.  

### <a name="set-names"></a>Definir Nomes

O agente de inventário de software recupera os nomes de produto e fabricante nas informações de cabeçalho do arquivo. Esses nomes nem sempre são padronizados nas informações de cabeçalho do arquivo. Quando você exibe o inventário de software no Gerenciador de Recursos, podem aparecer versões diferentes do mesmo fabricante ou nome de produto. Para padronizar esses nomes de exibição, selecione **Definir Nomes** e, em seguida, defina as seguintes configurações:  

-   **Tipo de nome**: o inventário de software coleta informações sobre produtos e fabricantes. Escolha se você deseja configurar nomes de exibição para um **Fabricante** ou um **Produto**.  

-   **Nome de exibição:** especifique o nome de exibição que você deseja usar em vez dos nomes na lista **Nomes inventariados**. Para especificar um novo nome de exibição, selecione **Novo**.  

-   **Nomes inventariados**: Para adicionar um nome inventariado, selecione **Novo**. Esse nome é substituído no inventário de software pelo nome escolhido na lista **Nome de exibição**. Você pode adicionar vários nomes a serem substituídos.  



##  <a name="software-metering"></a>Medição de software

### <a name="enable-software-metering-on-clients"></a>Habilitar medição de software em clientes
Essa configuração é definida como **Sim** por padrão. Para obter mais informações, consulte [Medição de software](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering#configure-software-metering).

### <a name="schedule-data-collection"></a>Agendar coleta de dados
Selecione **Agendamento** para ajustar a frequência com que os clientes executam o ciclo de medição de software. Por padrão, esse ciclo ocorre a cada sete dias.



##  <a name="software-updates"></a>Atualizações de software  

### <a name="enable-software-updates-on-clients"></a>Habilitar atualizações de software em clientes

Use essa configuração para habilitar atualizações de software em clientes do Configuration Manager. Ao desabilitar essa configuração, o Configuration Manager removerá as políticas de implantação existentes do cliente. Quando você reativa essa configuração, o cliente baixa a política de implantação atual.  

> [!IMPORTANT]  
>  Quando você desabilitar essa configuração, as políticas de conformidade que dependem das atualizações de software não funcionarão mais.  

### <a name="software-update-scan-schedule"></a>Agendamento de verificação de atualização de software

Selecione **Agendamento** para especificar a frequência com que o cliente inicia uma verificação de avaliação de conformidade. Essa verificação determina o estado das atualizações de software no cliente (por exemplo, obrigatórias ou instaladas). Para mais informações sobre a avaliação de conformidade, confira [Software updates compliance assessment](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance) (Avaliação de conformidade de atualizações de software).  

Por padrão, essa verificação usa um agendamento simples a ser iniciado a cada sete dias. Você pode criar um agendamento personalizado. Você pode especificar uma data e hora exatas de início, usar o UTC (Horário Coordenado Universal) ou a hora local, e configurar o intervalo recorrente para um dia específico da semana.  

> [!NOTE]  
>  Se você especificar um intervalo inferior a um dia, o Configuration Manager usará um dia como padrão automaticamente.  

> [!WARNING]  
>  A hora de início real em computadores cliente é a hora de início mais um período aleatório de até duas horas. Essa operação aleatória evita que os computadores cliente iniciem a verificação e se conectem simultaneamente ao ponto de atualização de software ativo.  

### <a name="schedule-deployment-re-evaluation"></a>Reavaliação de implantação da agenda

Selecione **Agendamento** para configurar a frequência com que o agente cliente de atualizações de software reavalia as atualizações de software para o status de instalação em computadores cliente do Configuration Manager. Quando as atualizações de software instaladas anteriormente não são mais encontradas em clientes, mas ainda são necessárias, o cliente reinstala as atualizações de software.

Ajuste esse agendamento com base na política da empresa para conformidade de atualizações de software e indique se os usuários podem desinstalar as atualizações de software. Cada ciclo de reavaliação de implantação resulta em uma atividade da rede e do processador do computador cliente. Por padrão, essa configuração usa um agendamento simples para iniciar a verificação de reavaliação de implantação a cada sete dias.  

> [!NOTE]  
>  Se você especificar um intervalo inferior a um dia, o Configuration Manager usará um dia como padrão automaticamente.  

### <a name="when-any-software-update-deployment-deadline-is-reached-install-all-other-software-update-deployments-with-deadline-coming-within-a-specified-period-of-time"></a>Quando a data limite de implantação da atualização de software for alcançada, instalar todas as outras implantações de atualização de software com a data limite dentro de um período especificado

Defina isso como **Sim** para instalar todas as atualizações de software de implantações obrigatórias com datas limite que ocorrem dentro de um período especificado. Quando uma implantação de atualização de software obrigatória alcança uma data limite, o cliente inicia a instalação das atualizações de software na implantação. Essa configuração determina se devem ser instaladas as atualizações de software de outras implantações obrigatórias que têm uma data limite dentro do tempo especificado.  

Use essa configuração para agilizar a instalação de atualizações de software obrigatórias. Essa configuração também tem o potencial de aumentar a segurança do cliente, diminuir as notificações para o usuário e reduzir as reinicializações do cliente. Por padrão, essa configuração é definida como **Não**.  

### <a name="period-of-time-for-which-all-pending-deployments-with-deadline-in-this-time-will-also-be-installed"></a>Período de tempo para o qual todas as implantações pendentes com prazo nesse período também serão instaladas

Use essa configuração para especificar o período da configuração anterior. Você pode inserir um valor entre 1 e 23 horas e de 1 a 365 dias. Por padrão, essa configuração é definida para 7 dias.  

### <a name="enable-installation-of-express-installation-files-on-clients"></a>Habilitar instalação dos arquivos de instalação do Express em clientes

Defina isso como **Sim** para permitir que os clientes usem os arquivos da instalação expressa. Para saber mais, confira [Gerenciar os arquivos de instalação expressa para atualizações do Windows 10](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).

### <a name="port-used-to-download-content-for-express-installation-files"></a>Porta usada para baixar conteúdo para arquivos de instalação do Express

Essa configuração define a porta local para que o ouvinte HTTP baixe o conteúdo expresso. Ela é definida como 8005 por padrão. Não é necessário abrir essa porta no firewall do cliente.

### <a name="enable-management-of-the-office-365-client-agent"></a>Habilitar o gerenciamento do Agente Cliente do Office 365

Quando você configura isso como **Sim**, ele habilita a definição das configurações de instalação do Office 365. Ele também permite o download de arquivos das Redes de Distribuição de Conteúdo (CDNs) do Office e a implantação dos arquivos como um aplicativo no Configuration Manager. Para obter mais informações, consulte [Gerenciar o Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates).



## <a name="state-messaging"></a>Mensagem de Estado

### <a name="state-message-reporting-cycle-minutes"></a>Ciclo de relatórios de mensagens de estado (minutos)
Especifica a frequência com que os clientes relatam mensagens de estado. Essa configuração é de 15 minutos por padrão.



##  <a name="user-and-device-affinity"></a>Afinidade de dispositivo e de usuário  

### <a name="user-device-affinity-usage-threshold-minutes"></a>Limite de uso de afinidade de dispositivo do usuário (minutos)
Especifique o número de minutos antes que o Configuration Manager crie um mapeamento de afinidade de dispositivo de usuário.  Por padrão, esse valor é de 2880 minutos (dois dias).

### <a name="user-device-affinity-usage-threshold-days"></a>Limite de uso de afinidade de dispositivo do usuário (dias)
Especifique o número de dias durante os quais o cliente mede o limite de afinidade de dispositivo baseado no uso.  Por padrão, esse valor é de 30 dias.

> [!NOTE]  
>  Por exemplo, especifique **Limite de uso da afinidade de dispositivo de usuário (minutos)** como **60** minutos e **Limite de uso da afinidade de dispositivo de usuário (dias)** como **5** dias. Em seguida, o usuário deve usar o dispositivo por 60 minutos em um período de cinco dias para criar a afinidade automática com o dispositivo.  

### <a name="automatically-configure-user-device-affinity-from-usage-data"></a>Configurar automaticamente a afinidade de dispositivo de usuário por meio de dados de uso
Escolha **Sim** para criar a afinidade de dispositivo de usuário automática com base nas informações de uso coletadas do Configuration Manager.  

### <a name="allow-user-to-define-their-primary-devices"></a>Permitir ao usuário definir os seus dispositivos primários
Quando essa configuração for **Sim**, os usuários poderão identificar seus próprios dispositivos primários no Centro de Software.



## <a name="windows-analytics"></a>Windows Analytics

Para obter mais informações sobre essas configurações, consulte [Configurar clientes para relatar dados ao Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics).
    
