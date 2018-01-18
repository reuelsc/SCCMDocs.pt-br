---
title: "Lista de verificação para 1610"
titleSuffix: Configuration Manager
description: "Conheça as ações a serem executadas antes de atualizar para o System Center Configuration Manager versão 1610."
ms.custom: na
ms.date: 6/6/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b411cb0-4fd1-41f2-a2f6-33738a5bde96
caps.latest.revision: "7"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: c0746dc168394cda88bad682fc3ba185e83758f7
ms.sourcegitcommit: 2867fd119256ec670fc5ae65cdc8a80d39f9b4d4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="checklist-for-installing-update-1610-for-system-center-configuration-manager"></a>Lista de verificação para instalar a atualização 1610 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Ao usar a ramificação atual do System Center Configuration Manager, você pode instalar a atualização no console da versão 1610 para atualizar sua hierarquia da versão 1606. Se sua hierarquia executa a versão 1511, 1602 ou 1606, você pode atualizar para a versão 1610.

Para obter a atualização da versão 1610, você deve usar uma função do sistema de sites do ponto de conexão de serviço no site de nível superior da hierarquia. Isso pode ser no modo online ou offline. Depois que a hierarquia baixar o pacote de atualização da Microsoft, você o encontrará no console em **Administração &gt; Visão Geral &gt; Serviços de Nuvem &gt; Atualizações e Manutenção**.

-   Quando a atualização for listada como **Disponível**, ela estará pronta para ser instalada. Antes de instalar a versão 1610, examine as seguintes informações [sobre a instalação da atualização 1610](#about-installing-update-1610) e a [lista de verificação](#checklist) para saber quais configurações devem ser feitas antes de iniciar a atualização.

-   Se a atualização for exibida como **Baixando** e não mudar, examine o **hman.log** e o **dmpdownloader.log** para verificar se há erros.

    -   Normalmente, você também pode reiniciar o serviço **SMS_Executive** no servidor do site para reiniciar o download dos arquivos de redistribuição de atualizações.

    -   Outro problema de download comum é devido às configurações do servidor proxy que impedem os downloads de <http://silverlight.dlservice.microsoft.com> e <http://download.microsoft.com>.

Para obter mais informações de como instalar atualizações, consulte [Atualizações e manutenção no console](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing).

Para obter informações sobre as versões do Branch Atual, consulte [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#bkmk_Baselines) em [Atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="about-installing-update-1610"></a>Sobre a instalação da atualização 1610

**Sites:**  
A atualização 1610 apenas pode ser instalada no site de nível superior da hierarquia. Isso significa que você inicia a instalação no site de administração central, se tiver um, ou no site primário autônomo. Depois que a atualização for instalada no site de camada superior, os sites filho terão o seguinte comportamento de atualização:

-   Os sites filho primários iniciam automaticamente a atualização após a conclusão da instalação da atualização no site de administração central. Você pode usar períodos de serviço para controlar quando um site instala atualizações. Antes da versão 1606, as janelas de serviço eram chamadas de janelas de manutenção. Para obter mais informações, consulte [Service windows for site servers](/sccm/core/servers/manage/service-windows) (Períodos de serviço para servidores do site).

-   Você deve atualizar sites secundários manualmente de dentro do console do Configuration Manager depois que a instalação da atualização estiver concluída no site pai primário. Não há suporte para atualização automática de servidores do site secundário.

**Funções do sistema de sites:**  
Quando o servidor do site instala a atualização, as funções de sistema de sites instaladas no servidor do site e as instaladas em computadores remotos são atualizadas automaticamente. Portanto, antes de instalar a atualização, verifique se cada servidor do sistema de sites atende algum dos novos pré-requisitos para operação com a nova versão de atualização.

**Consoles do Configuration Manager:**   
Na primeira vez que você usar um console do Configuration Manager após a conclusão da atualização, será solicitada a atualização desse console. Para isso, você deve executar a instalação do Configuration Manager no computador que hospeda o console e escolher a opção para atualizar o console. É recomendável não postergar a instalação da atualização no console.



## <a name="checklist"></a>Lista de Verificação

**Verifique se todos os sites executam uma versão compatível do System Center Configuration Manager:** antes de iniciar a instalação da atualização 1610, cada site na hierarquia deve executar a mesma versão do System Center Configuration Manager, seja a versão 1511, 1602 ou 1606.

**Examine o status do seu Software Assurance ou de seus direitos de assinatura equivalentes:**   
Você precisa ter um contrato de SA (Software Assurance) ativo para instalar a atualização 1610. Ao instalar a versão 1610, haverá uma opção na guia **Licenciamento** para confirmar a **data de expiração do Software Assurance**.

Esse é um valor opcional que você pode especificar como um lembrete conveniente da data de expiração da licença, que ficará visível nas instalações de atualizações futuras. Se você instalou o Configuration Manager da mídia da linha de base da versão 1606, é possível que já tenha especificado esse valor anteriormente durante a instalação ou na guia **Licenciamento** das **Configurações da Hierarquia** após a instalação do site.

Para mais informações, consulte [Licenciamento e branches do System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

**Examine as versões do Microsoft .NET instaladas nos servidores do sistema de sites:** quando um site instala a atualização 1610, o Configuration Manager instala automaticamente o .NET Framework 4.5.2 em cada computador que hospeda uma das seguintes funções do sistema de sites quando o .NET Framework 4.5 ou posterior ainda não está instalado:

-   Ponto proxy do registro
-   Ponto de registro
-   Ponto de gerenciamento
-   Ponto de Conexão de Serviço

Essa instalação pode colocar o servidor do sistema de sites em um estado de reinicialização pendente e relatar erros ao visualizador de status de componente do Configuration Manager. Além disso, os aplicativos .NET no servidor podem ter falhas aleatórias até que o servidor seja reinicializado.

Para obter mais informações, consulte [Site and site system prerequisites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) (Pré-requisitos de site e sistema de sites).

**Examine o status da hierarquia e do site e verifique se há problemas que não foram resolvidos:** antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, do servidor de banco de dados do site e das funções do sistema de sites que estão instalados nos computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.

Para obter mais informações, consulte [Use alerts and the status system for System Center Configuration Manager](/sccm/core/servers/manage/use-alerts-and-the-status-system).

**Examine a replicação de arquivo e dados entre sites:**   
Verifique se a replicação de arquivo e banco de dados entre sites está operacional e atualizada. Atrasos ou listas de pendências em qualquer um deles podem impedir uma atualização tranquila ou bem-sucedida.
Para replicação de banco de dados, você pode usar o Replication Link Analyzer para ajudar na resolução de problemas antes de iniciar a atualização.

Para obter mais informações, consulte [Sobre o Replication Link Analyzer](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA) no tópico [Monitorar a infraestrutura de hierarquia e de replicação no System Center Configuration Manager](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure).

**Instale todas as atualizações críticas aplicáveis aos sistemas operacionais nos computadores que hospedam o site, o servidor de banco de dados do site e as funções do sistema de site remoto:** antes de instalar uma atualização do Configuration Manager, instale todas as atualizações críticas para cada sistema de sites aplicável. Se uma atualização instalada precisar de uma reinicialização, reinicie os computadores aplicáveis antes de iniciar a atualização do Configuration Manager.

**Desabilitar réplicas de banco de dados para pontos de gerenciamento em sites primários:**   
O Configuration Manager não pode atualizar com êxito um site primário que tenha uma réplica de banco de dados habilitada para pontos de gerenciamento. Desabilite a replicação de banco de dados antes de instalar uma atualização para o Configuration Manager.

Para obter mais informações, consulte [Réplicas de banco de dados para pontos de gerenciamento no System Center Configuration Manager](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).

**Definir Grupos de Disponibilidade AlwaysOn do SQL Server para failover manual:**   
Antes de instalar atualizações, como a versão 1610, certifique-se de que o grupo de disponibilidade esteja definido para failover manual. Após a atualização do site, você pode restaurar o failover para que ele seja automático. Para saber mais, veja [SQL Server AlwaysOn para um banco de dados do site](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

**Reconfigure os pontos de atualização de software que usam NLBs:**   
O Configuration Manager não pode atualizar um site que usa um cluster de NLB (balanceamento de carga de rede) para hospedar pontos de atualização de software.

Se você usar clusters NLB para pontos de atualização de software, use o Windows PowerShell para remover o cluster NLB.
Para obter mais informações, consulte [Planejar atualizações de software no System Center Configuration Manager](/sccm/sum/plan-design/plan-for-software-updates).

**Desabilite todas as tarefas de manutenção do site em cada site durante a instalação da atualização nesse site:**   
Antes de instalar a atualização, desabilite todas as tarefas de manutenção do site que possam ser executadas durante o período em que o processo de atualização estiver ativo. Isso inclui, mas não está limitado ao seguinte:

-   Servidor do Site de Backup
-   Excluir Operações Antigas do Cliente
-   Excluir Dados Antigos de Descoberta

Há possibilidade de falha na instalação da atualização quando uma tarefa de manutenção do banco de dados do site for executada durante o processo da instalação. Antes de desabilitar uma tarefa, registre o agendamento da tarefa para que você possa restaurá-la depois que a atualização estiver instalada.

Para obter mais informações, consulte [Tarefas de manutenção do System Center Configuration Manager](/sccm/core/servers/manage/maintenance-tasks) e [Referência para tarefas de manutenção do System Center Configuration Manager](/sccm/core/servers/manage/reference-for-maintenance-tasks).

**Interromper temporariamente qualquer software antivírus nos servidores do System Center Configuration Manager:** antes de atualizar um site, verifique se o software antivírus foi interrompido nos servidores do Configuration Manager. <!--SMS.503481-->

**Crie um backup do banco de dados do site no site de administração central e nos sites primários:** antes de atualizar um site, faça backup do banco de dados do site para garantir que você tenha um backup bem-sucedido a ser usado para recuperação de desastres.

Para obter mais informações, consulte [Backup e recuperação para o System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

<!-- Removed from update guidance 6/6/2017
**Test the database upgrade on a copy of the most recent site database backup:** 
Before you update a System Center Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.

-   We recommend that you test the site database upgrade process because when you upgrade a site, the site database might be modified.

-   Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.

-   A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.

-   Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.

-   If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, see [Step 2: Test the database upgrade before installing an update](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2) from **Before you install an in-console update**.
-->

**Planeje o cliente piloto:**   
Ao instalar uma atualização que atualiza o cliente, você pode testar essa nova atualização do cliente em pré-produção antes que ela seja implantada e atualize todos os clientes ativos.

Para aproveitar essa opção, antes de começar a instalação da atualização, você deve configurar o site para dar suporte às atualizações automáticas para pré-produção.

Para obter mais informações, consulte [Atualizar clientes no System Center Configuration Manager](/sccm/core/clients/manage/upgrade/upgrade-clients) e [Como testar atualizações do cliente em uma coleção de pré-produção no System Center Configuration Manager](/sccm/core/clients/manage/upgrade/test-client-upgrades).

**Planeje usar períodos de serviço para controlar quando os servidores do site instalam atualizações:**   
Você pode usar períodos de serviço para definir um período durante o qual as atualizações de um servidor de sites possam ser instaladas.

Isso pode ajudar a controlar quando os sites em sua hierarquia instalam a atualização. Antes da versão 1606, as janelas de serviço eram chamadas de janelas de manutenção. Para obter mais informações, consulte [Service windows for site servers](/sccm/core/servers/manage/service-windows) (Períodos de serviço para servidores do site).

**Execute o verificador de pré-requisitos de instalação:**   
Quando a atualização está listada no console como **Disponível**, você pode executar o verificador de pré-requisitos independentemente antes de instalar a atualização. (Ao instalar a atualização no site, o verificador de pré-requisitos é executado novamente).

Para executar um verificador de pré-requisitos a partir do console, vá para **Administração > Visão geral > Serviços de Nuvem > Atualizações e Manutenção.** Em seguida, clique com botão direito do mouse em **Pacote de atualização do Configuration Manager 1610** e escolha **Executar verificação de pré-requisitos**.

Para saber mais sobre como iniciar e monitorar a verificação de pré-requisitos, veja **Etapa 3: executar o verificador de pré-requisitos antes de instalar uma atualização** no tópico [Instalações de atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).

> [!IMPORTANT]  
> Quando o verificador de pré-requisitos for executado como parte de uma instalação de atualização ou de modo independente, o processo atualizará alguns arquivos de origem do produto que são usados para tarefas de manutenção do site. Portanto, após executar o verificador de pré-requisitos, mas antes de instalar a atualização 1610, se você precisa executar uma tarefa de manutenção de site, execute **Setupwpf.exe** (Instalação do Configuration Manager) na pasta CD.Latest no servidor de sites.

**Sites de atualização:**   
Agora você está pronto para iniciar a instalação da atualização para sua hierarquia. Para saber mais sobre como instalar a atualização, veja [Instalação de atualizações no console.](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates)

Recomendamos que você planeje a instalação da atualização fora do horário comercial normal de cada site, quando o processo de instalação da atualização e suas ações de reinstalação dos componentes do site e das funções do sistema de sites terão um efeito mínimo sobre as operações de seu negócio.

Para obter mais informações, consulte [Atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).
