---
title: "Lista de verificação para a 1606 | Microsoft Docs"
description: "Saiba mais sobre as ações a serem executadas antes de atualizar do System Center Configuration Manager versão 1511 ou 1602 para a 1606."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75652cd2-a95a-46c5-91c1-6d43fc8e787e
caps.latest.revision: 7
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: ba087244ad52087f32acbe413b1e56c7478e4db6

---
# <a name="checklist-for-installing-update-1606-for-system-center-configuration-manager"></a>Lista de verificação para instalar a atualização 1606 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A versão 1606 para System Center Configuration Manager (Branch Atual) é uma atualização que você pode usar para atualizar da versão 1511 ou 1602.

Antes de atualizar a versão 1606 como atualização, leia as informações a seguir e revise a lista de verificação de ações a serem tomadas antes de começar a atualização.

Para obter informações sobre versões da linha de base, consulte [Versões de linha de base e atualização](../../../core/servers/manage/updates.md#bkmk_Baselines) em [Atualizações para o System Center Configuration Manager](../../../core/servers/manage/updates.md).

 ## <a name="about-installing-update-1606"></a>Sobre como instalar a atualização 1606

Como *atualização*, a versão 1606 pode ser instalada somente no site de nível superior da sua hierarquia. Isso significa que você inicia a instalação no site de administração central, se tiver um, ou no site primário autônomo.  

-   Os sites primários filho instalam a atualização automaticamente depois que a instalação da atualização estiver concluída no site de administração central. É possível usar as janelas de serviço para controlar quando o site instala atualizações. Antes da versão 1606, as janelas de serviço eram chamadas de janelas de manutenção. Para obter mais informações, consulte [Períodos de Serviço para servidores do site](../../../core/servers/manage/install-in-console-updates.md#bkmk_ServiceWindow).  

-   Você deve atualizar sites secundários manualmente de dentro do console do Configuration Manager depois que a instalação da atualização estiver concluída no site pai primário. Não há suporte para atualização automática de servidores do site secundário.  

Quando o servidor do site instala a atualização, as funções de sistema de sites instaladas no servidor do site e aquelas instaladas em computadores remotos são atualizadas automaticamente. Portanto, antes de instalar a atualização, verifique se cada servidor do sistema de sites atende algum dos novos pré-requisitos para operação com a nova versão de atualização.  

 Na primeira vez que você usar um console do Configuration Manager após a conclusão da atualização, será solicitada a atualização desse console.  Para isso, você deve executar a Instalação do Configuration Manager no computador que hospeda o console e escolher a opção para atualizar o console. É recomendável não postergar a instalação da atualização no console.

 **Problemas conhecidos desta atualização**   
  Os problemas a seguir se aplicam quando você exibe o Status de instalação do pacote de atualização:
  - Ao atualizar da versão 1602 para 1606, a etapa **Extrair o conteúdo do pacote de atualização** exibe um status de **Não iniciado**, mesmo que o download tenha sido concluído.
  - Ao atualizar da versão 1511 para 1606, algumas etapas mostrarão um status de **Concluído**, mas não será exibido um valor para **Hora da última atualização**.


## <a name="checklist"></a>Lista de Verificação  

 **Verifique se todos os sites executam uma versão com suporte do System Center Configuration Manager:** antes de iniciar a instalação da atualização 1606, todos os servidores do site na hierarquia devem executar a mesma versão do System Center Configuration Manager, seja a versão 1511 ou 1602.

 **Examine as versões do .NET instaladas nos servidores do sistema de sites:** quando um site instala a atualização 1606, o Configuration Manager instala automaticamente o .NET Framework 4.5.2 em cada computador que hospeda uma das seguintes funções do sistema de sites quando o .NET Framework 4.5 ou posterior ainda não está instalado:  

-   ponto proxy do registro  

-   ponto de registro  

-   ponto de gerenciamento  

-   ponto de conexão de serviço  

Essa instalação pode colocar o servidor do sistema de sites em um estado de reinicialização pendente e relatar erros para o visualizador de status de componente do Configuration Manager. Além disso, os aplicativos .NET no servidor podem ter falhas aleatórias até que o servidor seja reinicializado.  

 Para obter mais informações, consulte [Site and site system prerequisites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Pré-requisitos de site e sistema de sites)  

 **Examine o status da hierarquia e do site e verifique se há problemas que não foram resolvidos:** antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, do servidor de banco de dados do site e das funções do sistema de sites que estão instalados nos computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.  
 Para obter mais informações, consulte [Usar alertas e o sistema de status para o System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md)  

 **Examine a replicação de arquivos e dados entre sites:**  assegure-se de que a replicação de arquivos e bancos de dados entre sites esteja funcionando e atualizada. Atrasos ou listas de pendências em qualquer um deles podem impedir uma atualização tranquila ou bem-sucedida.    
Para replicação de banco de dados, você pode usar o Replication Link Analyzer para ajudar na resolução de problemas antes de iniciar a atualização.    
 Para obter mais informações, consulte   
[Sobre o Replication Link Analyzer](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA) no tópico [Monitorar a infraestrutura de hierarquia e de replicação no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

 **Instale todas as atualizações críticas aplicáveis de sistemas operacionais em computadores que hospedam o site, o servidor de banco de dados do site e as funções do sistema de sites remoto:** antes de instalar uma atualização do Configuration Manager, instale todas as atualizações críticas para cada sistema de sites aplicável. Se uma atualização instalada precisar de uma reinicialização, reinicie os computadores aplicáveis antes de iniciar a atualização.  

 **Desabilite as réplicas de banco de dados para pontos de gerenciamento nos sites primários:** o Configuration Manager não pode atualizar com êxito um site primário que tenha uma réplica de banco de dados para pontos de gerenciamento habilitada. Desabilite a replicação de banco de dados antes de você:  

-   Criar um backup do banco de dados do site para testar a atualização do banco de dados  

-   Instalar uma atualização para o Configuration Manager  

Para obter mais informações, consulte   
[Réplicas de banco de dados para pontos de gerenciamento para o System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)  

 **Definir grupos de disponibilidade AlwaysOn do SQL Server para failover manual:**  
 Antes de instalar atualizações, como a versão 1606, certifique-se de que o grupo de disponibilidade esteja definido para failover manual. Após a atualização do site, você pode restaurar o failover para que ele seja automático. Para obter mais informações, consulte [AlwaysOn do SQL Server para um banco de dados do site](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

 **Reconfigure os pontos de atualização de software que usam NLBs:** o Configuration Manager não pode atualizar um site que usa um cluster NLB (Balanceamento de Carga de Rede) para hospedar pontos de atualização de software.  
Se você usar clusters NLB para pontos de atualização de software, use o PowerShell para remover do cluster NLB.    

 Para obter mais informações, consulte [Planejar atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md)  

 **Desabilite todas as tarefas de manutenção em cada site durante a instalação da atualização no site em questão:** antes de instalar a atualização, desabilite todas as tarefas de manutenção do site que possam ser executadas enquanto o processo de atualização estiver ativo. Isso inclui, mas não está limitado ao seguinte:  

-   Servidor do Site de Backup  

-   Excluir Operações Antigas do Cliente  

-   Excluir Dados Antigos de Descoberta  

Há possibilidade de falha na instalação da atualização quando uma tarefa de manutenção do banco de dados do site for executada durante o processo da instalação. Antes de desabilitar uma tarefa, registre o agendamento da tarefa para que você possa restaurar sua configuração depois que a atualização estiver instalada.  
 Para obter mais informações, consulte [Tarefas de manutenção do System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) e [Referência para tarefas de manutenção do System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md)  

 **Crie um backup do banco de dados do site no site de administração central e nos sites primários:** antes de atualizar um site, faça backup do banco de dados do site para garantir que você tenha um backup bem-sucedido a ser usado para recuperação de desastres.   
Para obter mais informações, consulte [Backup and recovery for System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md)  


 **Testar a atualização do banco de dados em uma cópia do backup mais recente do banco de dados do site:** antes de atualizar um site de administração central ou site primário do System Center Configuration Manager, teste o processo de atualização do banco de dados do site em uma cópia do banco de dados do site.  

-   Você deve testar o processo de atualização de banco de dados do site, pois quando você atualiza um site, o banco de dados do site pode ser modificado  

-   Embora o teste de atualização de banco de dados não seja necessário, ele pode identificar problemas na atualização antes que seu banco de dados de produção seja afetado  

-   Uma atualização do banco de dados do site com falha pode deixar o banco de dados do site inoperante e pode requerer uma recuperação do site para restaurar a funcionalidade  

-   Embora o banco de dados do site seja compartilhado entre sites em uma hierarquia, planeje testar o banco de dados em cada site aplicável antes de atualizar esse site  

-   Se você usar réplicas de banco de dados para pontos de gerenciamento em um site primário, desabilite a replicação antes de criar o backup do banco de dados do site  

O Configuration Manager não dá suporte ao backup de sites secundários nem ao teste de atualização de um banco de dados do site secundário.   
Não há suporte para executar um teste da atualização do banco de dados no banco de dados do site de produção. Fazer isso atualiza o banco de dados do site e pode deixar seu site inoperável. Para obter mais informações, consulte a seção [Testar a atualização de banco de dados do site](../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_test) em [Atualizar para o System Center Configuration Manager](../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

 **Planeje o piloto do cliente:** quando você instala uma atualização que atualiza o cliente, é possível testar essa nova atualização do cliente na pré-produção antes que ela seja implantada e atualize todos os seus clientes ativos.   
 Para aproveitar essa opção, antes de começar a instalação da atualização, você deve configurar o site para permitir atualizações automáticas para pré-produção. Para obter mais informações, consulte [Atualizar clientes no System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md) e   
[Como testar atualizações do cliente em uma coleção de pré-produção no System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md)  

 **Planejar para usar janelas de serviço**  
 **para controlar quando os servidores do site instalam as atualizações:** é possível usar janelas de serviço para definir um período que se aplique a um servidor do site primário durante o qual as atualizações desse site podem ser instaladas.   
Isso pode ajudar a controlar quando os sites em sua hierarquia instalam a atualização.
Antes da versão 1606, as janelas de serviço eram chamadas de janelas de manutenção. Para obter mais informações, consulte [Períodos de Serviço para servidores do site](../../../core/servers/manage/install-in-console-updates.md#bkmk_ServiceWindow).  

 **Execute o Verificador de Pré-requisitos de Instalação:** antes de instalar a atualização 1606, você pode executar o Verificador de Pré-requisitos independentemente da instalação de atualização. Quando você instala a atualização no site, o Verificador de Pré-requisitos é executado novamente.  
Para obter mais informações, confira **Etapa 3: Executar o verificador de pré-requisitos antes de instalar uma atualização** no tópico [Atualizações para o System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md).  

> [!IMPORTANT]  
>  Quando o verificador de pré-requisitos for executado como parte de uma instalação de atualização ou de modo independente, o processo atualizará alguns arquivos de origem do produto que são usados para tarefas de manutenção do site. Portanto, após a execução do verificador de pré-requisitos, mas antes da instalação da atualização 1606, se for preciso executar uma tarefa de manutenção do site, execute **Setupwpf.exe** (Instalação do Configuration Manager) na pasta CD.Latest no servidor do site.  

 **Atualize os sites:** agora você está pronto para iniciar a instalação da atualização da sua hierarquia.  
  Recomendamos que você planeje a instalação da atualização fora do horário comercial normal de cada site, quando o processo de instalação da atualização e suas ações de reinstalação dos componentes do site e das funções do sistema de sites terão um efeito mínimo sobre as operações de seu negócio. Para obter mais informações, consulte [Atualizações para o System Center Configuration Manager](../../../core/servers/manage/updates.md).  



<!--HONumber=Dec16_HO3-->

