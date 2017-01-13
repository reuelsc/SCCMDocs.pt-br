---
title: Alta disponibilidade | Microsoft Docs
description: "Aprenda a implantar o System Center Configuration Manager usando as opções que mantêm um alto nível de serviço disponível."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1a4a9da88caba55d9e340c7fb1f31f4e3b957f3e
ms.openlocfilehash: d3e9afb90cdc85bc7299626b642c52be659e3bdf

---
# <a name="high-availability-options-for-system-center-configuration-manager"></a>Opções de alta disponibilidade para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*



É possível implantar o System Center Configuration Manager usando opções que mantêm um alto nível de serviço disponível.   

Opções que dão suporte à alta disponibilidade:   

-   Os sites oferecem suporte a várias instâncias de servidores do sistema de site que prestam serviços importantes aos clientes.  

-   Os sites de administração central e sites primários oferecem suporte ao backup do banco de dados do site. O banco de dados do site contêm todas as configurações para sites e clientes, e é compartilhado entre sites em uma hierarquia que contém um site de administração central.  

-   As opções de recuperação de site interna podem reduzir o tempo de inatividade do servidor e incluem opções avançadas que simplificam a recuperação quando você tem uma hierarquia com um site de administração central.  

-   Os clientes podem corrigir automaticamente problemas típicos sem intervenção administrativa.  

-   Os sites geram alertas sobre clientes que falham ao enviar dados recentes, os quais alertam os administradores sobre possíveis problemas.  

-   O Configuration Manager fornece vários relatórios internos que permitem identificar problemas e tendências antes que se tornem problemas para as operações do cliente ou do servidor.  

 O Configuration Manager não fornece um serviço em tempo real, e você deve esperar que ele opere com alguma latência de dados. Portanto, é incomum para a maioria dos cenários que envolvem um interrupção temporária de serviço se tornarem um problema crítico. Quando você tiver configurado sites e hierarquias tendo a alta disponibilidade em mente, o tempo de inatividade pode ser minimizado, a autonomia das operações mantida e um alto nível de serviço fornecido.  

 Por exemplo, os clientes do Configuration Manager geralmente operam de forma autônoma usando agendamentos conhecidos e configurações para operações, e agendamento para enviar dados ao site para processamento.  

-   Quando os clientes não podem entrar em contato com o site, eles armazenam os dados em cache para serem enviados até que eles possam contatar o site.  

-   Os clientes que não podem entrar em contato com o site continuam a operar usando os últimos agendamentos conhecidos e as informações em cache, como um aplicativo baixado anteriormente que eles devem executar ou instalar, até que eles possam contatar o site e receber políticas novas.  

-   O site monitora seus sistemas de site e clientes para atualizações de status periódicas e pode gerar alertas quando há falhas no registro.  

-   Relatórios internos fornecem informações para operações contínuas, bem como operações e tendências históricas. O Configuration Manager dá suporte a mensagens baseadas em estado que fornecem informações quase em tempo real para operações contínuas.  

  Use as informações neste tópico com as informações nos seguintes artigos:
-   [Hardware recomendado](../../core/plan-design/configs/recommended-hardware.md)
-   [Sistemas operacionais com suporte para servidores de sistema de sites](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  

-   [Pré-requisitos de sites e do sistema de sites](../../core/plan-design/configs/site-and-site-system-prerequisites.md)


##  <a name="a-namebkmksnha-high-availability-for-sites-and-hierarchies"></a><a name="bkmk_snh"></a> Alta disponibilidade para sites e hierarquias  
 **Use um cluster do SQL Server para hospedar o banco de dados do site:**  

 Ao usar um cluster do SQL Server para o banco de dados em um site de administração central ou site primário, você usa o suporte a failover embutido no SQL Server.  

 Os sites secundários não podem usar um cluster do SQL Server e não oferecem suporte ao backup nem à restauração de seu banco de dados do site. Recupere um site secundário reinstalando-o do site primário pai.  

 **Use o grupo de disponibilidade AlwaysOn do SQL Server para hospedar o banco de dados do site:**  

 A partir da versão 1602, você pode usar grupos de disponibilidade AlwaysOn do SQL Server para hospedar o banco de dados do site em sites primários e o site de administração central como uma solução de alta disponibilidade e de recuperação de desastres. Para mais informações, consulte [AlwaysOn do SQL Server para um banco de dados de site altamente disponível para o System Center Configuration Manager](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

 **Implante uma hierarquia de sites com um site de administração central e um ou mais sites primários filho:**  

 Esta configuração pode fornecer tolerância a falhas quando os sites gerenciam segmentos sobrepostos da sua rede. Além disso, essa configuração oferece uma opção de recuperação adicional para usar as informações no banco de dados compartilhado disponível em outro site, para recriar o banco de dados do site no site recuperado. Você pode usar essa opção para substituir um backup indisponível ou com falha do banco de dados de sites com falha.  

 **Crie backups regulares em sites de administração central e sites primários:**  

 Ao criar e testar um backup regular do site, você pode verificar se tem os dados necessários para recuperar um site, e a experiência para recuperar um site no período mínimo de tempo.  

 **Instale diversas instâncias das funções do sistema de site:**  

 Ao instalar diversas instâncias de funções críticas do sistema de site, como o ponto de gerenciamento e o ponto de distribuição, você fornece pontos de contato redundantes para clientes caso um servidor do sistema de site específico esteja offline.  

 **Instale várias instâncias do Provedor de SMS no site:** o Provedor de SMS fornece o ponto de contato administrativo para um ou mais consoles do Configuration Manager. Ao instalar vários Provedores de SMS, você pode fornecer redundância para pontos de contato para administrar o site e a hierarquia.  

##  <a name="a-namebkmkssra-high-availability-for-site-system-roles"></a><a name="bkmk_ssr"></a> Alta disponibilidade para funções do sistema de sites  
 Em cada site, você implanta funções do sistema de site para fornecer os serviços que você deseja que os clientes usem nesse site. O banco de dados do site contém as informações de configuração do site e de todos os clientes. Use uma ou mais das opções disponíveis para fornecer alta disponibilidade do banco de dados do site, e a recuperação do site e o banco de dados do site se necessário.  

 **Redundância para funções importantes do sistema de sites:**  

-   Ponto de serviços Web do Catálogo de Aplicativos  

-   Ponto de sites da Web do catálogo de aplicativos  

-   Ponto de distribuição  

-   Ponto de gerenciamento  

-   Ponto de atualização de software  

-   Ponto de migração de estado  

 Você pode instalar diversas instâncias da função do ponto do Reporting Services para fornecer redundância para relatar sobre sites e clientes.

 Você pode usar o PowerShell para instalar a função do sistema de sites do ponto de atualização de software em um cluster NLB (Balanceamento de Carga de Rede) do Windows para dar suporte a failover  


 **Backup do site interno:**  

 O Configuration Manager inclui uma tarefa de backup interno para ajudá-lo a fazer backup do site e das informações críticas regularmente. Além disso, o assistente de instalação do Configuration Manager oferece suporte a ações de restauração do site para ajudá-lo a restaurar um site para operações.  

 **Como publicar no Active Directory Domain Services e no DNS:**  

 Você pode configurar cada site para publicar dados sobre servidores do sistema de site e serviços nos Serviços de Domínio Active Directory e no DNS. Isso permite que os clientes identifiquem o servidor mais acessível na rede e identifiquem quando novos servidores do sistema de site que podem fornecer serviços importantes, como pontos de gerenciamento, estão disponíveis.  

 **Provedor de SMS e console do Configuration Manager:**  

 O Configuration Manager dá suporte à instalação de vários Provedores de SMS, cada um em um computador separado, para assegurar diversos pontos de acesso para o console do Configuration Manager. Isso garante que se um computador do Provedor de SMS estiver offline, você continuará com a capacidade de exibir e reconfigurar sites e clientes do site do Configuration Manager.  

 Quando um console do Configuration Manager se conecta a um site, ele se conecta a uma instância do Provedor de SMS desse site. A instância do Provedor de SMS é selecionada de forma não determinística. Se o Provedor de SMS selecionado não estiver disponível, você terá as seguintes opções:  

-   Reconectar o console ao site. Cada solicitação de conexão nova é atribuída de forma não determinística a uma instância do Provedor de SMS e é possível que a nova conexão seja atribuída a uma instância disponível.  

-   Conecte o console a um site diferente do site do Configuration Manager e gerencie a configuração dessa conexão. Isso apresenta um ligeiro atraso das alterações de configuração de não mais do que alguns minutos. Depois que o Provedor de SMS do site estiver online, você poderá reconectar o console do Configuration Manager diretamente ao site que deseja gerenciar.  

 Você pode instalar o console do Configuration Manager em diversos computadores para uso por usuários administrativos. Cada Provedor de SMS oferece suporte a conexões de vários consoles do Configuration Manager.  

 **Ponto de gerenciamento:**  

 Instale vários pontos de gerenciamento em cada site primário e permita que os sites publiquem dados do site na sua infraestrutura do Active Directory e no DNS.  

 Vários pontos de gerenciamento ajudam a equilibrar a carga do uso de qualquer ponto de gerenciamento único por vários clientes. Além disso, você pode instalar uma ou mais réplicas de banco de dados para pontos de gerenciamento para diminuir as operações com uso intensivo de CPU do ponto de gerenciamento e aumentar a disponibilidade dessa função crítica do sistema de site  

 Como você pode instalar somente um ponto de gerenciamento em um site secundário, o qual deve estar localizado no servidor do site secundário, os pontos de gerenciamento em sites secundários não são considerados como tendo uma configuração de alta disponibilidade.  

> [!NOTE]  
>  Os dispositivos gerenciados pelo gerenciamento local de dispositivos móveis se conectam apenas a um ponto de gerenciamento em um site primário. O ponto de gerenciamento é atribuído pelo Configuration Manager ao dispositivo móvel durante o registro e não se altera. Quando você instala vários pontos de gerenciamento e habilita mais de um para dispositivos móveis, o ponto de gerenciamento que está atribuído a um cliente de dispositivo móvel é não determinístico.  
>   
>  Se o ponto de gerenciamento usado por um cliente de dispositivo móvel ficar indisponível, você deverá resolver o problema nesse ponto de gerenciamento ou apagar o dispositivo móvel e registrá-lo novamente para que ele possa ser atribuído a um ponto de gerenciamento operacional habilitado para dispositivos móveis.  

 **Ponto de distribuição:**  

 Instale vários pontos de distribuição e implante conteúdo em vários pontos de distribuição. Você pode configurar grupos de limite de sobreposição para o local do conteúdo para assegurar que os clientes em cada sub-rede possam acessar uma implantação de dois ou mais pontos de distribuição. Finalmente, considere a possibilidade de configurar um ou mais pontos de distribuição como locais de fallback para o conteúdo.  

 Para obter mais informações sobre locais de fallback, consulte [Gerenciar conteúdo e infraestrutura de conteúdo do System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 **Pontos de serviços Web do catálogo de aplicativos e ponto de sites da Web do catálogo de aplicativos:**  

 É possível instalar diversas instâncias de cada função do sistema de site e implantar uma de cada no mesmo computador do sistema de site para obter um melhor desempenho.  

 Cada função do sistema de site do catálogo de aplicativos fornece as mesmas informações que outras instâncias da função do sistema de site, independentemente da localização dessa função de servidor do site na hierarquia. Portanto, quando um cliente fizer uma solicitação ao catálogo de aplicativos e tiver sido definida a configuração do cliente do dispositivo Ponto de sites da Web do catálogo de aplicativos padrão para Detectar automaticamente, o cliente poderá ser direcionado a uma instância disponível. É dada preferência aos servidores do sistema de sites do catálogo de aplicativos local, de acordo com o local de rede atual do cliente.  

 Para obter mais informações sobre esta configuração de cliente e como a detecção automática funciona, veja a seção [Agente de Computador](../../core/clients/deploy/about-client-settings.md#computer-agent) no tópico [Sobre configurações do cliente no System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

##  <a name="a-namebkmkclienta-high-availability-for-clients"></a><a name="bkmk_client"></a> Alta disponibilidade para clientes  
 **As operações do cliente são autônomas:**  

 A autonomia do cliente do Configuration Manager inclui o seguinte:  

-   Os clientes não exigem contato contínuo com servidores do sistema de site específicos. Eles usam configurações conhecidas para realizar ações predefinidas em um agendamento.  

-   Os clientes podem usar qualquer instância disponível de uma função do sistema de site que preste serviços para clientes, e eles tentam contatar servidores conhecidos até que um servidor disponível seja localizado.  

-   Os clientes podem executar implantações de inventário, software e ações agendadas semelhantes independente de contato direto com servidores do sistema de site.  

-   Os clientes configurados para usar um ponto de status de fallback podem enviar detalhes ao ponto de status de fallback quando não podem se comunicar com um ponto de gerenciamento.  

 **Os clientes podem corrigir a si mesmos:**  

 Os clientes corrigem automaticamente a maioria dos problemas típicos sem intervenção administrativa direta:  

-   Periodicamente, os clientes autoavaliam seu status e têm iniciativa para corrigir problemas típicos usando um cache local de etapas de correção e arquivos de origem para reparos.  

-   Quando um cliente não consegue enviar informações de status para seu site, o site pode gerar um alerta. Os usuários administrativos que recebem esses alertas podem tomar uma medida imediata para restaurar a operação normal do cliente.  

 **Os clientes armazenam em cache informações a serem utilizadas no futuro:**  

 Quando um cliente se comunica com um ponto de gerenciamento, o cliente pode obter e armazenar em cache as informações a seguir:  

-   Configurações do cliente.  

-   Agendamentos do cliente.  

-   Informações sobre implantações de software e um download do software com agendamento para instalação pelo cliente, quando a implantação está configurada para esta ação.  

 Quando um cliente não pode contatar um ponto de gerenciamento, os clientes armazenam em cache localmente o status, o estado e as informações que eles relatam ao site e transferem esses dados depois de estabelecer contato com um ponto de gerenciamento.  

 **O cliente pode enviar o status para um ponto de status de fallback:**  

 Ao configurar um cliente para usar um ponto de status de fallback, você fornece um ponto de contato adicional para que o cliente envie detalhes importantes sobre sua operação. Os clientes configurados para usar um ponto de status de fallback continuam a enviar um status sobre suas operações para a função do sistema de site mesmo quando o cliente não pode se comunicar com um ponto de gerenciamento.  

 **Gerenciamento central de dados do cliente e identidade do cliente:**  

 O banco de dados do site retém informações importantes sobre cada identidade do cliente, em vez do cliente individual, e associa esses dados a um computador ou usuário específico. Isso significa que:  

-   Os arquivos de origem do cliente em um computador podem ser instalados e reinstalados sem afetar os registros históricos do computador no qual o cliente está instalado.  

-   A falha de um computador cliente não afeta a integridade das informações armazenadas no banco de dados. Essas informações podem permanecer disponíveis para emissão de relatórios.  

##  <a name="a-namebkmknonhaoptionsa-options-for-sites-and-site-system-roles-that-are-not-highly-available"></a><a name="bkmk_nonHAoptions"></a> Opções para sites e funções do sistema de sites que não estão altamente disponíveis  
 Vários sistemas de site não oferecem suporte a múltiplas instâncias em um site ou na hierarquia. Estas informações podem ajudar você a se preparar para quando esses sistemas de sites ficarem offline.  

 **Servidor do site (site):**  

 O Configuration Manager não dá suporte à instalação do servidor de site para cada site em um cluster do Windows Server ou NLB.  

 As seguintes informações podem ajudá-lo a se preparar caso o servidor de site falhe ou não esteja operacional:  

-   Use a tarefa de backup interna para criar regularmente um backup do site. Em um ambiente de teste, pratique regularmente a restauração de sites a partir de um backup.  

-   Implante vários sites primários do Configuration Manager em uma hierarquia com um site de administração central para criar redundância. Se houver uma falha no site, considere usar a política de grupo do Windows ou os scripts de logon para transferir clientes a um site funcional.  

-   Se possuir uma hierarquia com um site de administração central, você poderá recuperar o site de administração central ou um site primário filho usando a opção de recuperar o banco de dados de um site a partir de outro site na hierarquia.  

-   Os sites secundários não podem ser restaurados e devem ser reinstalados.  

 **Ponto de sincronização do Asset Intelligence (hierarquia):**  

 Essa função do sistema de sites não é considerada crítica e fornece funcionalidade opcional no Configuration Manager. Se esse sistema de site ficar offline, use uma das seguintes opções:  

-   Resolva o motivo do sistema de site estar offline.  

-   Desinstale a função do servidor atual e instale-a em um novo servidor.  

 **Ponto do Endpoint Protection (hierarquia):**  

 Essa função do sistema de sites não é considerada crítica e fornece funcionalidade opcional no Configuration Manager. Se esse sistema de site ficar offline, use uma das seguintes opções:  

-   Resolva o motivo do sistema de site estar offline.  

-   Desinstale a função do servidor atual e instale-a em um novo servidor.  

 **Ponto de registro (site):**  

 Essa função do sistema de sites não é considerada crítica e fornece funcionalidade opcional no Configuration Manager. Se esse sistema de site ficar offline, use uma das seguintes opções:  

-   Resolva o motivo do sistema de site estar offline.  

-   Desinstale a função do servidor atual e instale-a em um novo servidor.  

 **Ponto proxy do registro (site):**  

 Essa função do sistema de sites não é considerada crítica e fornece funcionalidade opcional no Configuration Manager. Entretanto, você pode instalar múltiplas instâncias dessa função do sistema de site em um site, e em vários sites na hierarquia. Se esse sistema de site ficar offline, use uma das seguintes opções:  

-   Resolva o motivo do sistema de site estar offline.  

-   Desinstale a função do servidor atual e instale-a em um novo servidor.  

 Quando você tiver mais de um servidor proxy do registro em um site, use um alias DNS para o nome do servidor. Quando se utiliza essa configuração, o round robin do DNS fornece alguma tolerância a falhas e balanceamento de carga caso os usuários registrem seus dispositivos móveis.  

 **Ponto de status de fallback (site ou hierarquia):**  

 Essa função do sistema de sites não é considerada crítica e fornece funcionalidade opcional no Configuration Manager. Se esse sistema de site ficar offline, use uma das seguintes opções:  

-   Resolva o motivo do sistema de site estar offline.  

-   Desinstale a função do servidor atual e instale-a em um novo servidor. Como os clientes são atribuídos ao ponto de status de fallback durante a instalação do cliente, é necessário modificar os clientes existentes para usar o novo servidor do sistema de site.  

### <a name="see-also"></a>Consulte também  
 [Configurações com suporte para o System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md)



<!--HONumber=Dec16_HO3-->


