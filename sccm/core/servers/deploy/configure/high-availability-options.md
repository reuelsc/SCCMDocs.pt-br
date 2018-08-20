---
title: Alta disponibilidade
titleSuffix: Configuration Manager
description: Aprenda a implantar o Configuration Manager usando as opções que mantêm um alto nível de serviço disponível.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18435bd43ed74daee646096d1e8d8b6ed7b7bc27
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386337"
---
# <a name="high-availability-options-for-configuration-manager"></a>Opções de alta disponibilidade para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este artigo descreve como implantar o Configuration Manager usando opções que mantêm um alto nível de serviço disponível.   

As seguintes opções do Configuration Manager são compatíveis com alta disponibilidade:   

- Da versão 1806 em diante, configure o site de administração central e cada site primário com um servidor do site adicional no modo passivo.  
 
- Configure um grupo de disponibilidade Always On do SQL Server para o banco de dados do site em sites primários e no site de administração central.

- Os sites são compatíveis com várias instâncias de funções do sistema de sites que prestam serviços importantes aos clientes. Por exemplo, pontos de gerenciamento e pontos de distribuição.  

- Os sites de administração central e sites primários oferecem suporte ao backup do banco de dados do site. O banco de dados do site armazena todas as configurações para sites e clientes. Os sites em uma hierarquia compartilham esses dados de configuração.  

- Opções de recuperação de site internas podem reduzir o tempo de inatividade do servidor. Essas opções avançadas simplificam a recuperação quando você tem uma hierarquia com um site de administração central.  

- Os clientes podem corrigir automaticamente problemas típicos sem intervenção administrativa.  

- Os sites geram alertas sobre clientes que falham ao enviar dados recentes, os quais alertam os administradores sobre possíveis problemas.  

- O Configuration Manager fornece vários relatórios e painéis internos. Use-os para identificar problemas e tendências antes que eles se tornem problemas para as operações do servidor ou do cliente.  


O Configuration Manager inclui vários recursos que oferecem serviço quase em tempo real. Se esses recursos são essenciais para atender às suas necessidades de negócios, planeje e configure seus sites e hierarquias para alta disponibilidade. Por exemplo:  

- [Ações de notificação do cliente](/sccm/core/clients/manage/manage-clients), como reiniciar, iniciar verificações do Windows Defender ou Área de Trabalho Remota.  

- Mensagens baseadas em estado para monitorar recursos como atualizações de software e proteção de ponto de extremidade. 

- [Scripts](/sccm/apps/deploy-use/create-deploy-scripts), começando na versão 1706  

- [CMPivot](/sccm/core/servers/manage/cmpivot), começando na versão 1806  


Outros recursos do Configuration Manager não fornecem serviço em tempo real. Esses recursos incluem, entre outros, configurações do cliente, inventário de hardware e software, implantações de software e configurações de conformidade. Espere que eles operem com alguma latência de dados. É incomum que a maioria dos cenários que envolvem uma interrupção temporária de serviço se torne um problema crítico. Para minimizar o tempo de inatividade, manter a autonomia das operações e fornecer um alto nível de serviço, configure seus sites e hierarquias pensando em alta disponibilidade.  

Por exemplo, os clientes do Configuration Manager geralmente operam de forma autônoma usando agendamentos conhecidos e configurações para operações, e agendamento para enviar dados ao site para processamento.  

- Quando os clientes não conseguem entrar em contato com o site, eles armazenam em cache os dados a serem enviados até que possam contatar o site.  

- Os clientes que não conseguem contatar o site continuam a operar. Eles usam os últimos agendamentos conhecidos e as informações armazenadas em cache até que possam contatar o site e receber políticas novas. Por exemplo, um cliente pode manter um aplicativo baixado anteriormente que ele deve executar ou instalar.   

- O site monitora seus sistemas de sites e clientes para atualizações de status periódicas. Ele pode gerar alertas quando o registro desses componentes falhar.  

- Relatórios internos fornecem insights sobre operações contínuas, bem como operações históricas e tendências. O Configuration Manager dá suporte a mensagens baseadas em estado que fornecem informações quase em tempo real para operações contínuas.  



##  <a name="bkmk_snh"></a> Alta disponibilidade para sites e hierarquias  

#### <a name="use-a-site-server-in-passive-mode"></a>Usar um servidor do site no modo passivo
Da versão 1806 em diante, instale um servidor de site adicional no modo *passivo*. O servidor do site no modo passivo é usado além do servidor do site existente no modo *ativo*. Um servidor do site no modo passivo está disponível para uso imediato quando for necessário. Para obter mais informações, confira [Alta disponibilidade do servidor do Site](/sccm/core/servers/deploy/configure/site-server-high-availability).  

#### <a name="use-a-remote-content-library"></a>Usar uma biblioteca de conteúdo remota
Da versão 1806 em diante, mova a biblioteca de conteúdo do site para um local remoto que forneça armazenamento altamente disponível. Esse recurso é um requisito para alta disponibilidade do servidor do site. Para obter mais informações, confira [A biblioteca de conteúdo](/sccm/core/plan-design/hierarchy/the-content-library#bkmk_remote).

#### <a name="centralize-content-sources"></a>Centralizar fontes de conteúdo
Todo o conteúdo de software no Configuration Manager requer um local de origem do pacote na rede. Use o armazenamento centralizado e altamente disponível para hospedar um local de origem do pacote comuns para todo o conteúdo. 

#### <a name="use-a-sql-server-always-on-availability-group-to-host-the-site-database"></a>Use o grupo de disponibilidade Always On do SQL Server para hospedar o banco de dados do site  
Hospede o banco de dados do site em sites primários e no site de administração central em grupos de disponibilidade Always On do SQL Server. Para obter mais informações, confira [SQL Server Always On para um banco de dados do site altamente disponível](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).  

#### <a name="use-a-sql-server-cluster-to-host-the-site-database"></a>Usar um cluster do SQL Server para hospedar o banco de dados do site  
Ao usar um cluster do SQL Server para o banco de dados em um site de administração central ou site primário, você usa o suporte a failover embutido no SQL Server.  

Os sites secundários não podem usar um cluster do SQL Server e não são compatíveis com backup ou restauração do banco de dados do site. Recupere um site secundário reinstalando-o do site primário pai.  

#### <a name="deploy-a-hierarchy-of-sites-with-a-central-administration-site-and-one-or-more-child-primary-sites"></a>Implantar uma hierarquia de sites com um site de administração central e um ou mais sites primários filhos  
Esta configuração pode fornecer tolerância a falhas quando os sites gerenciam segmentos sobrepostos da sua rede. Ela oferece uma opção de recuperação adicional para usar as informações no banco de dados compartilhado disponível em outro site para recompilar o banco de dados do site no site recuperado. Use essa opção para substituir um backup não disponível ou com falha do banco de dados de sites com falha.  

#### <a name="create-regular-backups-at-central-administration-sites-and-primary-sites"></a>Criar backups regulares em sites de administração central e sites primários  
Quando você cria e testa um backup regular do site, isso garante que você tenha os dados necessários para recuperar um site. Você também pode praticar a recuperação de um site no período mínimo de tempo.  

#### <a name="install-multiple-instances-of-site-system-roles"></a>Instalar diversas instâncias das funções do sistema de site  
Quando você instala diversas instâncias das funções do sistema de sites fundamentais, fornece pontos de contato redundantes para os clientes. Por exemplo, vários pontos de gerenciamento e pontos de distribuição fornecem serviço redundante no caso de um servidor específico estar offline.  

#### <a name="install-multiple-instances-of-the-sms-provider-at-a-site"></a>Instalar diversas instâncias do Provedor de SMS em um site  
O Provedor de SMS fornece o ponto de contato administrativo para um ou mais consoles do Configuration Manager. Para fornecer redundância para pontos de contato para administrar seu site e hierarquia, instale vários Provedores de SMS.  



##  <a name="bkmk_ssr"></a> Alta disponibilidade para funções do sistema de sites  
Em cada site, você implanta funções do sistema de site para fornecer os serviços que você deseja que os clientes usem nesse site. O banco de dados do site contém as informações de configuração do site e de todos os clientes. Use uma ou mais das opções disponíveis para fornecer alta disponibilidade do banco de dados do site, e a recuperação do site e o banco de dados do site se necessário.  

#### <a name="redundancy-for-important-site-system-roles"></a>Redundância para funções importantes do sistema de site  
-   Ponto de serviços Web do catálogo de aplicativos  

-   Ponto de site da Web do Catálogo de Aplicativos  

-   Ponto de distribuição  

-   Ponto de gerenciamento  

-   Ponto de atualização de software  

-   Ponto de migração de estado  

Para oferecer redundância para relatório em sites e clientes, instale várias instâncias do ponto do Reporting Services.

Para suporte a failover com o ponto de atualização de software, use o Windows PowerShell para instalar essa função em um cluster NLB (balanceamento de carga de rede) do Windows.  

#### <a name="built-in-site-backup"></a>Backup do site interno  
O Configuration Manager inclui uma tarefa de backup interno para ajudá-lo a fazer backup do site e das informações críticas regularmente. Além disso, o assistente de instalação do Configuration Manager dá suporte a ações de restauração do site para ajudá-lo a restaurar um site para operações.  

#### <a name="publishing-to-active-directory-domain-services-and-dns"></a>Publicando nos Serviços de Domínio Active Directory e no DNS  
Configure cada site para publicar dados sobre o site no Active Directory Domain Services e no DNS. Essa publicação permite que os clientes identifiquem o servidor mais acessível na rede. Os clientes também a usam para identificar quando novos servidores de sistema de sites estão disponíveis para fornecer serviços importantes, como pontos de gerenciamento.  

#### <a name="sms-provider-and-configuration-manager-console"></a>Provedor de SMS e console do Configuration Manager  
O Configuration Manager dá suporte à instalação de vários Provedores de SMS em servidores separados como vários pontos de acesso para o console. Se um servidor de Provedor de SMS estiver offline, você poderá exibir e gerenciar sites e clientes.  

Quando um console do Configuration Manager se conecta a um site, ele se conecta a uma instância do Provedor de SMS desse site. A instância do Provedor de SMS é selecionada aleatoriamente. Se o Provedor de SMS selecionado não estiver disponível, você terá as seguintes opções:  

-   Reconectar o console ao site. Cada nova solicitação de conexão é atribuída aleatoriamente a uma instância do Provedor de SMS. É possível que a nova conexão seja atribuída a uma instância disponível.  

-   Conecte o console a um site diferente do site do Configuration Manager e gerencie a configuração dessa conexão. Essa opção gera um leve atraso das alterações de configuração de não mais do que alguns minutos. Depois que o Provedor de SMS do site estiver online, reconecte o console do Configuration Manager diretamente ao site que você deseja gerenciar.  

Instale o console do Configuration Manager em diversos computadores para uso por administradores. Cada provedor de SMS dá suporte para conexões de mais de um console.  

#### <a name="management-point"></a>Ponto de gerenciamento  
Instale vários pontos de gerenciamento em cada site primário e permita que os sites publiquem dados do site na sua infraestrutura do Active Directory e no DNS.  

Vários pontos de gerenciamento ajudam a equilibrar a carga do uso de qualquer ponto de gerenciamento único por vários clientes. Também considere instalar uma ou mais réplicas de banco de dados para pontos de gerenciamento. Essa configuração reduz as operações que fazem uso intenso do processamento do ponto de gerenciamento. Isso também aumenta a disponibilidade dessa função fundamental do sistema de sites.  

Sites secundários só dão suporte à instalação de um ponto de gerenciamento, que deve estar localizado no servidor do site secundário. Pontos de gerenciamento em sites secundários não são considerados como tendo uma configuração altamente disponível.  

> [!NOTE]  
>  Os dispositivos gerenciados pelo gerenciamento local de dispositivos móveis se conectam apenas a um ponto de gerenciamento em um site primário. O ponto de gerenciamento é atribuído pelo Configuration Manager ao dispositivo móvel durante o registro e não muda. Quando você instala vários pontos de gerenciamento e habilita mais de um para dispositivos móveis, o ponto de gerenciamento que está atribuído a um cliente de dispositivo móvel é não determinístico.  
>   
>  Se o ponto de gerenciamento usado por um cliente de dispositivo móvel ficar indisponível, você deverá resolver o problema nesse ponto de gerenciamento ou apagar o dispositivo móvel e registrá-lo novamente para que ele possa ser atribuído a um ponto de gerenciamento operacional habilitado para dispositivos móveis.  

#### <a name="distribution-point"></a>Ponto de distribuição  
Instale vários pontos de distribuição e implante conteúdo em vários pontos de distribuição. Adicione mais de um ponto de distribuição por grupo de limites para garantir que os clientes obtenham várias opções em sua solicitação de conteúdo. Configure relações de grupo de limites para que eles tenham um comportamento de fallback previsível para outro grupo de limites ou ponto de distribuição na nuvem. Para obter mais informações, consulte [Configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).  

#### <a name="application-catalog-web-service-point-and-application-catalog-website-point"></a>Ponto de serviço Web do catálogo de aplicativos e ponto de site do catálogo de aplicativos  
Instale mais de uma instância de cada função do sistema de sites. Para obter o melhor desempenho, implante um de cada no mesmo servidor do sistema de sites.  

Cada função do sistema de sites do catálogo de aplicativos fornece as mesmas informações que outras instâncias daquela função, não importa seu local na hierarquia. Quando um cliente faz uma solicitação para o catálogo de aplicativos, e você configurou os clientes para que detectem automaticamente o ponto do site do catálogo de aplicativos padrão, o cliente é direcionado para uma instância disponível. Os clientes preferem instâncias de catálogo de aplicativo local, com base no local de rede atual do cliente.  

Para obter mais informações sobre essa configuração de cliente e como a detecção automática funciona, veja a seção [Agente de Computador](/sccm/core/clients/deploy/about-client-settings#computer-agent) no artigo [Sobre configurações do cliente](/sccm/core/clients/deploy/about-client-settings).  



##  <a name="bkmk_client"></a> Alta disponibilidade para clientes  

#### <a name="client-operations-are-autonomous"></a>As operações do cliente são autônomas  
A autonomia do cliente do Configuration Manager inclui os seguintes comportamentos:  

-   Os clientes não exigem contato contínuo com nenhum servidor do sistema de sites específico. Eles usam configurações conhecidas para realizar ações predefinidas em um agendamento.  

-   Os clientes podem usar qualquer instância disponível de uma função do sistema de sites que fornece serviços para clientes. Eles tentam contatar servidores conhecidos até que localizem um servidor disponível.  

-   Os clientes podem executar implantações de inventário, software e ações agendadas semelhantes independente de contato direto com servidores do sistema de site.  

-   Os clientes configurados para usar um ponto de status de fallback podem enviar detalhes ao ponto de status de fallback quando não podem se comunicar com um ponto de gerenciamento.  

#### <a name="clients-can-repair-themselves"></a>Os clientes podem corrigir a si mesmos  
Os clientes corrigem automaticamente a maioria dos problemas típicos sem intervenção administrativa direta.  

-   Periodicamente, a clientes fazem a autoavaliação do seu status. Eles agem para corrigir problemas típicos usando um cache local de etapas de remediação e arquivos de origem para reparos.  

-   Quando um cliente não consegue enviar informações de status para seu site, o site pode gerar um alerta. Os usuários administrativos que recebem esses alertas podem tomar uma medida imediata para restaurar a operação normal do cliente.  

#### <a name="clients-cache-information-to-use-in-the-future"></a>Os clientes armazenam em cache informações a serem utilizadas no futuro  
Quando um cliente se comunica com um ponto de gerenciamento, o cliente pode obter e armazenar em cache as informações a seguir:  

-   Configurações do cliente  

-   Agendamentos do cliente  

-   Informações sobre implantações de software e um download do software com agendamento para instalação pelo cliente, quando a implantação está configurada para esta ação.  

Quando um cliente não consegue contatar um ponto de gerenciamento, os clientes armazenam em cache localmente informações de status, estado e cliente que eles relatam ao site. O cliente transfere esses dados depois de estabelecer contato com um ponto de gerenciamento.  

#### <a name="client-can-submit-status-to-a-fallback-status-point"></a>O cliente pode enviar o status para um ponto de status de fallback  
Ao configurar um cliente para usar um ponto de status de fallback, você fornece um ponto de contato adicional para que o cliente envie detalhes importantes sobre sua operação. Os clientes configurados para usar um ponto de status de fallback continuam a enviar um status sobre suas operações para a função do sistema de site mesmo quando o cliente não consegue se comunicar com um ponto de gerenciamento.  

#### <a name="central-management-of-client-data-and-client-identity"></a>Gerenciamento central de dados do cliente e identidade do cliente  
O banco de dados do site retém informações importantes sobre cada identidade do cliente, em vez do cliente individual, e associa esses dados a um computador ou usuário específico.  

-   Os arquivos de origem do cliente em um computador podem ser instalados e reinstalados sem afetar os registros históricos do computador no qual o cliente está instalado.  

-   A falha de um computador cliente não afeta a integridade das informações armazenadas no banco de dados. Essas informações podem permanecer disponíveis para emissão de relatórios.  



##  <a name="bkmk_nonHAoptions"></a> Opções para funções do sistema de sites e para sites não são altamente disponíveis  
Vários sistemas de site não dão suporte a múltiplas instâncias em um site ou na hierarquia. Essas informações podem ajudar você a se preparar para quando esses sistemas de sites ficarem offline.  

#### <a name="site-server-site"></a>Servidor do site (site)  

> [!Note]  
> Esta seção se aplica somente às versões do Configuration Manager 1802 e anteriores. Da versão 1806 em diante, o Configuration Manager fornece uma opção de alta disponibilidade para o servidor do site. Para obter mais informações, confira [Alta disponibilidade do servidor do Site](/sccm/core/servers/deploy/configure/site-server-high-availability).  

O Configuration Manager não dá suporte à instalação do servidor do site para cada site em um cluster do Windows Server ou NLB.  

As informações a seguir podem ajudá-lo a se preparar caso o servidor do site falhe ou não esteja operacional:  

-   Use a tarefa de backup interna para criar regularmente um backup do site. Em um ambiente de teste, pratique regularmente a restauração de sites a partir de um backup.  

-   Implante vários sites primários do Configuration Manager em uma hierarquia com um site de administração central para criar redundância. Se houver uma falha no site, considere usar a política de grupo do Windows ou os scripts de logon para transferir clientes a um site funcional.  

-   Se possuir uma hierarquia com um site de administração central, você poderá recuperar o site de administração central ou um site primário filho usando a opção de recuperar o banco de dados de um site a partir de outro site na hierarquia.  

-   Os sites secundários não podem ser restaurados e devem ser reinstalados.  

#### <a name="asset-intelligence-synchronization-point-hierarchy"></a>Ponto de sincronização do Asset Intelligence (hierarquia)  
Essa função do sistema de sites não é considerada crítica e fornece funcionalidade opcional no Configuration Manager. Se esse sistema de site ficar offline, use uma das seguintes opções:  

-   Resolva o motivo para o sistema de sites estar offline.  

-   Desinstale a função do servidor atual e instale-a em um novo servidor.  

#### <a name="endpoint-protection-point-hierarchy"></a>Ponto de proteção do ponto de extremidade (hierarquia)  
Essa função do sistema de sites não é considerada crítica e fornece funcionalidade opcional no Configuration Manager. Se esse sistema de site ficar offline, use uma das seguintes opções:  

-   Resolva o motivo para o sistema de sites estar offline.  

-   Desinstale a função do servidor atual e instale-a em um novo servidor.  

#### <a name="enrollment-point-site"></a>Ponto de registro (site)  
Essa função do sistema de sites não é considerada crítica e fornece funcionalidade opcional no Configuration Manager. Se esse sistema de site ficar offline, use uma das seguintes opções:  

-   Resolva o motivo para o sistema de sites estar offline.  

-   Desinstale a função do servidor atual e instale-a em um novo servidor.  

#### <a name="enrollment-proxy-point-site"></a>Ponto proxy do registro (site)  
Essa função do sistema de sites não é considerada crítica e fornece funcionalidade opcional no Configuration Manager. Entretanto, você pode instalar múltiplas instâncias dessa função do sistema de site em um site, e em vários sites na hierarquia. Se esse sistema de site ficar offline, use uma das seguintes opções:  

-   Resolva o motivo para o sistema de sites estar offline.  

-   Desinstale a função do servidor atual e instale-a em um novo servidor.  

Quando você tiver mais de um servidor proxy do registro em um site, use um alias DNS para o nome do servidor. Quando se utiliza essa configuração, o round robin do DNS fornece alguma tolerância a falhas e balanceamento de carga caso os usuários registrem seus dispositivos móveis.  

#### <a name="fallback-status-point-site-or-hierarchy"></a>Ponto de status de fallback (site ou hierarquia)  
Essa função do sistema de sites não é considerada crítica e fornece funcionalidade opcional no Configuration Manager. Se esse sistema de site ficar offline, use uma das seguintes opções:  

-   Resolva o motivo para o sistema de sites estar offline.  

-   Desinstale a função do servidor atual e instale-a em um novo servidor. Uma vez que os clientes são atribuídos ao ponto de status de fallback durante a instalação do cliente, é necessário modificar os clientes existentes para usar o novo servidor do sistema de sites.  


#### <a name="service-connection-point-hierarchy"></a>Ponto de conexão de serviço (hierarquia)
Embora essa função do sistema de sites seja essencial para manter o branch atual do Configuration Manager atualizado, ela geralmente não é usada com frequência. Se esse sistema ficar offline, use uma das seguintes opções:

-   Resolva o motivo para o sistema de sites estar offline.  

-   Desinstale a função do servidor atual e instale-a em um novo servidor.  



## <a name="see-also"></a>Consulte também  
- [Configurações com suporte](/sccm/core/plan-design/configs/supported-configurations)  

- [Hardware recomendado](/sccm/core/plan-design/configs/recommended-hardware)  

- [Sistemas operacionais com suporte para servidores de sistema de sites](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers)   

- [Pré-requisitos de sites e do sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)  

- [Impactos de falha do site](/sccm/core/servers/manage/site-failure-impacts)  

