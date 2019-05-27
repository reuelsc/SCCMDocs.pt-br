---
title: Lista de verificação para 1602
titleSuffix: Configuration Manager
description: Saiba mais sobre as ações a serem executadas antes de atualizar do System Center Configuration Manager versão 1511 para a 1602.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b63ef197-01f0-4894-b929-5ef8403c5195
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: ba54ff30f880520106ef615ef713781149776eda
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65501215"
---
# <a name="checklist-for-installing-update-1602-for-system-center-configuration-manager"></a>Lista de verificação para instalar a atualização 1602 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Antes de atualizar o System Center Configuration Manager da versão 1511 para a 1602, leia as informações a seguir e revise a lista de verificação das ações a serem tomadas antes de iniciar a atualização.  

 **Sobre como instalar a atualização 1602:**  

 A atualização 1602 pode ser instalada somente no site de nível superior da sua hierarquia. Isso significa que você inicia a instalação no site de administração central, se tiver um, ou no site primário autônomo.  

-   Os sites primários filho instalam a atualização automaticamente depois que a instalação da atualização estiver concluída no site de administração central. É possível usar as janelas de serviço para controlar quando o site instala atualizações. A partir da versão de atualização 1602, as janelas de manutenção passam a ser chamadas de *janelas de serviço*. Para obter mais informações, consulte [Service windows for site servers](/sccm/core/servers/manage/service-windows) (Períodos de serviço para servidores do site).  

-   Você deve atualizar sites secundários manualmente de dentro do console do Configuration Manager depois que a instalação da atualização estiver concluída no site pai primário. Não há suporte para a atualização automática de servidores do site secundário.  

Quando o servidor do site instala a atualização, as funções do sistema de sites instaladas no servidor de sites e as instaladas em computadores remotos são atualizadas automaticamente. Portanto, antes de instalar a atualização, verifique se cada servidor do sistema de sites atende aos novos pré-requisitos para operação com a nova versão de atualização.  

Na primeira vez que você usar um console do Configuration Manager após a conclusão da atualização, será solicitada a atualização desse console. Para isso, execute a instalação do Configuration Manager no computador que hospeda o console e escolha a opção para atualizar o console. É recomendável não postergar a instalação da atualização no console.  

 **Lista de verificação:**  

 **Verifique se todos os sites executam uma versão compatível do System Center Configuration Manager:**  cada servidor do site na hierarquia precisa executar o System Center Configuration Manager versão 1511 para que você possa iniciar a instalação da atualização 1602.  

 **Examine as versões do Microsoft .NET instaladas nos servidores do sistema de sites:** quando a atualização 1602 é instalada em um site, o Configuration Manager instala o .NET Framework 4.5.2 automaticamente em cada computador que hospeda uma das seguintes funções do sistema de sites (quando o .NET Framework 4.5 ou posterior ainda não está instalado):  

-   Ponto proxy do registro  

-   Ponto de registro  

-   Ponto de gerenciamento  

-   Ponto de Conexão de Serviço  

Essa instalação pode colocar o servidor do sistema de sites em um estado de reinicialização pendente e relatar erros para o visualizador de status de componente do Configuration Manager. Além disso, os aplicativos .NET no servidor podem ter falhas aleatórias até que o servidor seja reinicializado.  

 Para obter mais informações, consulte [Site and site system prerequisites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Pré-requisitos de site e sistema de sites).  

 **Examinar o status do site e da hierarquia e verificar se não existem problemas não resolvidos:** Antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, do servidor de banco de dados do site e das funções do sistema de site que estão instalados em computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.  

Para obter mais informações, consulte [Usar alertas e o sistema de status para o System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Examine a replicação de arquivos e dados entre sites:**  Verifique se a replicação de arquivo e banco de dados entre sites está operacional e atualizada. Atrasos ou listas de pendências em qualquer um deles podem impedir uma atualização tranquila ou bem-sucedida.    

Para replicação de banco de dados, você pode usar o Replication Link Analyzer para ajudar na resolução de problemas antes de iniciar a atualização.    

 Para saber mais, veja [Sobre o Replication Link Analyzer](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA) no tópico [Monitorar a infraestrutura de hierarquia e de replicação no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

 **Instale todas as atualizações críticas aplicáveis para os sistemas operacionais nos computadores que hospedam o site, o servidor de banco de dados do site e as funções do sistema de sites remoto:** antes de instalar uma atualização do Configuration Manager, instale todas as atualizações críticas de cada sistema de sites aplicável. Se uma atualização instalada precisar de uma reinicialização, reinicie os computadores aplicáveis antes de iniciar a atualização.  

 **Desabilitar réplicas de banco de dados para pontos de gerenciamento em sites primários:** O Configuration Manager não pode atualizar com êxito um site primário que tenha uma réplica de banco de dados habilitada para pontos de gerenciamento. Desabilite a replicação de banco de dados antes de você:  

-   Criar um backup do banco de dados do site para testar a atualização do banco de dados.  

-   Instalar uma atualização para o Configuration Manager.  

Para saber mais, veja [Réplicas de banco de dados para pontos de gerenciamento no System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Reconfigure os pontos de atualização de software que usam NLBs:** O Configuration Manager não pode atualizar um site que usa um cluster de NLB (Balanceamento de Carga de Rede) para hospedar pontos de atualização de software.  Se você usar clusters NLB para pontos de atualização de software, use o Windows PowerShell para remover o cluster NLB.    

 Para obter mais informações, consulte [Planejar atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

 **Desabilite todas as tarefas de manutenção de site em cada site durante a instalação da atualização nesse site:** antes de instalar as atualizações, desabilite todas as tarefas de manutenção do site que possam ser executadas durante o tempo que o processo de atualização estiver ativo. Essas tarefas incluem, mas não estão limitadas a, o seguinte:  

-   Servidor do Site de Backup  

-   Excluir Operações Antigas do Cliente  

-   Excluir Dados Antigos de Descoberta  

Há possibilidade de falha na instalação da atualização quando uma tarefa de manutenção do banco de dados do site for executada durante o processo da instalação. Antes de desabilitar uma tarefa, registre o agendamento da tarefa para que você possa restaurar sua configuração depois que a atualização estiver instalada.  

 Para obter mais informações, consulte [Tarefas de manutenção do System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) e [Referência para tarefas de manutenção do System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md). 

**Interrompa temporariamente o software antivírus nos servidores do System Center Configuration Manager:** antes de atualizar um site, verifique se você interrompeu o software antivírus nos servidores do Configuration Manager. <!--SMS.503481--> 

 **Criar um backup do banco de dados do site no site de administração central e em sites primários:** antes de atualizar um site, faça backup do banco de dados do site para garantir um backup bem-sucedido a ser usado para recuperação de desastre.   

Para obter mais informações, consulte [Backup e recuperação para o System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  

 **Faça backup de um arquivo Configuration.mof personalizado:** se você usar um arquivo Configuration.mof personalizado para definir as classes de dados usadas com o inventário de hardware, crie um backup desse arquivo antes de atualizar o site. Após a atualização, restaure esse arquivo na versão 1602 do site. Ao atualizar um site, o arquivo atual será substituído pela versão original (padrão) do arquivo. Para saber mais sobre o uso desse arquivo, veja [Como estender o inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 **Teste a atualização do banco de dados em uma cópia do backup mais recente do banco de dados do site:** antes de atualizar um site de administração central ou um site primário do System Center Configuration Manager, teste o processo de atualização do banco de dados do site em uma cópia do banco de dados do site.  

-   Você deve testar o processo de atualização de banco de dados do site, pois ao atualizar um site, o banco de dados do site pode ser modificado.  

-   Embora o teste de atualização do banco de dados não seja necessário, ele pode identificar problemas na atualização antes que seu banco de dados de produção seja afetado.  

-   Uma atualização do banco de dados do site com falha pode deixar o banco de dados do site inoperante e pode requerer uma recuperação do site para restaurar a funcionalidade.  

-   Embora o banco de dados do site seja compartilhado entre sites em uma hierarquia, planeje testar o banco de dados em cada site aplicável antes de atualizar o site.  

-   Se você usar réplicas de banco de dados para pontos de gerenciamento em um site primário, desabilite a replicação antes de criar o backup do banco de dados do site.  

O Configuration Manager não dá suporte ao backup de sites secundários, nem ao teste de atualização de um banco de dados do site secundário.   
Não execute um teste da atualização do banco de dados no banco de dados do site de produção. Fazer isso atualiza o banco de dados do site e pode deixar seu site inoperável. Para obter mais informações, confira [Etapa 2: Testar a atualização do banco de dados antes de instalar uma atualização](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2) em **Antes de instalar uma atualização no console**.  

 **Planejar a criação do piloto do cliente:** Ao instalar uma atualização que atualiza o cliente, você pode testar essa nova atualização do cliente em pré-produção antes que ela seja implantada e atualize todos os clientes ativos.   

 Para aproveitar essa opção, antes de começar a instalação da atualização, você deve configurar o site para dar suporte às atualizações automáticas para pré-produção. Para obter mais informações, consulte [Atualizar clientes no System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md) e   
[Como testar atualizações do cliente em uma coleção de pré-produção no System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

 **Planeje usar janelas de manutenção para controlar quando os servidores do site instalam atualizações:** você pode usar as janelas de manutenção para definir um período de tempo no qual as atualizações do servidor do site podem ser instaladas. Isso pode ajudar a controlar quando os sites em sua hierarquia instalam a atualização.   

A partir da versão de atualização 1602, as janelas de manutenção passam a ser chamadas de *janelas de serviço*. Para obter mais informações, consulte [Service windows for site servers](/sccm/core/servers/manage/service-windows) (Períodos de serviço para servidores do site).  

 **Execute o verificador de pré-requisitos de instalação:**  antes de instalar a atualização 1602, você pode executar o verificador de pré-requisitos independentemente da instalação da atualização. Ao instalar a atualização no site, o Verificador de Pré-requisitos é executado novamente.  

Para saber mais, confira a **Etapa 3: Executar o verificador de pré-requisitos antes de instalar uma atualização** no tópico [Atualizações do System Center Configuration Manager](../../../core/servers/manage/updates.md).  

> [!IMPORTANT]  
>  Quando o verificador de pré-requisitos for executado como parte de uma instalação de atualização ou de modo independente, o processo atualizará alguns arquivos de origem do produto que são usados para tarefas de manutenção do site. Portanto, após executar o verificador de pré-requisitos, mas antes de instalar a atualização 1602, se você precisa executar uma tarefa de manutenção de site, execute **Setupwfe.exe** (Instalação do Configuration Manager) na pasta CD.Latest no servidor de sites.  

 **Atualizar os sites:** Agora você está pronto para iniciar a instalação da atualização para sua hierarquia. Recomendamos que você planeje a instalação da atualização fora do horário comercial normal de cada site, quando o processo de instalação da atualização e suas ações de reinstalação dos componentes do site e das funções do sistema de sites terão um efeito mínimo sobre as operações de seu negócio.

Para obter mais informações, consulte [Atualizações para o System Center Configuration Manager](../../../core/servers/manage/updates.md).  

## <a name="see-also"></a>Consulte também  
 [Atualizações para o System Center Configuration Manager](../../../core/servers/manage/updates.md)
