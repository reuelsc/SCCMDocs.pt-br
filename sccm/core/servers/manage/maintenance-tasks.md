---
title: "Tarefas de manutenção | System Center Configuration Manager"
description: "Compreenda quais tarefas de manutenção executar para sites e hierarquias do Configuration Manager e quando executá-las."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ac47f1b88a89a42bb51b87b36147b731e37a5824


---
# <a name="maintenance-tasks-for-system-center-configuration-manager"></a>Tarefas de manutenção do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os sites e hierarquias do System Center Configuration Manager exigem manutenção e monitoramento regulares para prestar serviços de forma eficaz e contínua. A manutenção regular garante que o hardware, o software e o banco de dados do Configuration Manager continuem a funcionar de forma correta e eficiente. O desempenho otimizado reduz muito o risco de falha.  

 Para configurar Alertas e usar o Sistema de status para monitorar a integridade do Configuration Manager, consulte [Usar alertas e o sistema de status para o System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   [Tarefas de manutenção](#bkmk_MTs)  

##  <a name="a-namebkmkmtsa-maintenance-tasks"></a><a name="bkmk_MTs"></a> Tarefas de manutenção  
 A manutenção regular é importante para garantir operações de site corretas. Mantenha um log de manutenção para documentar as datas em que a manutenção foi realizada, por quem, e quaisquer comentários relacionados à manutenção da tarefa realizada.  

### <a name="when-to-perform-common-maintenance-tasks"></a>Quando realizar tarefas comuns de manutenção  
 Para manter seu site, considere realizar a manutenção regular em uma agenda diária, semanal e, para algumas tarefas, um agendamento mais periódico. A manutenção comum pode incluir tarefas internas de manutenção e outras tarefas, como manutenção da conta, para manter a conformidade com as políticas de sua empresa.  

 Use as informações a seguir como um guia para ajudá-lo a planejar quando executar tarefas de manutenção diferentes. Use essas listas como ponto de partida e adicione outras tarefas que você possa precisar.  

**Tarefas diárias**   
Veja abaixo as tarefas de manutenção que você pode considerar para serem executadas diariamente:  

-   Verificar se as tarefas de manutenção predefinidas que estão agendadas para execução diária estão sendo executadas com êxito.  

-   Verificar o status do banco de dados do Configuration Manager  

-   Verificar o status do servidor de site  

-   Verificar se há lista de pendências do arquivo nas caixas de entrada do sistema de sites do Configuration Manager  

-   Verificar o status dos sistemas de sites  

-   Verificar os logs de eventos do sistema operacional em sistemas de sites  

-   Verificar o log de erros do SQL Server no computador do banco de dados do site  

-   Verificar o desempenho do sistema  

-   Verificar alertas do Configuration Manager  

**Tarefas semanais**   
Veja abaixo as tarefas de manutenção que você pode considerar para serem executadas semanalmente:  

-   Verificar se as tarefas predefinidas de manutenção agendadas para execução semanal estão sendo executadas com êxito.  

-   Excluir arquivos desnecessários dos sistemas de sites  

-   Produzir e distribuir relatórios do usuário final, se necessário  

-   Fazer backup de logs de eventos de aplicativo, segurança e sistema e limpá-los  

-   Verificar o tamanho do banco de dados do site e verificar se há espaço em disco suficiente disponível no servidor do banco de dados do site para que o banco de dados possa aumentar  

-   Executar a manutenção do banco de dados do SQL Server no banco de dados do site conforme o plano de manutenção do SQL Server  

-   Verificar o espaço em disco disponível em todos os sistemas de sites  

-   Executar ferramentas de desfragmentação de disco em todos os sistemas de sites  

**Tarefas Periódicas**   
Algumas tarefas não precisam ser executadas durante a manutenção diária ou semanal, mas são importantes para garantir a integridade geral do site e manter os planos de segurança e recuperação de desastres atualizados. Eis as tarefas de manutenção que você pode considerar executar de forma mais periódica do que as tarefas diárias ou semanais:  

-   Alterar contas e senhas, se necessário, de acordo com o plano de segurança  

-   Examinar o plano de manutenção para verificar se as tarefas de manutenção estão agendadas corretamente e de forma eficaz, dependendo das definições do site  

-   Examinar o design de hierarquia do Configuration Manager de acordo com qualquer alteração necessária  

-   Verificar o desempenho da rede para garantir que não foram feitas alterações que afetam as operações do site  

-   Verificar se as configurações do Active Directory que afetam as operações do site não foram alteradas. Por exemplo, verificar se as sub-redes atribuídas a sites do Active Directory usadas ​​como limites para o site do Configuration Manager não foram alteradas  

-   Revisar seu plano de recuperação de desastres quanto a quaisquer alterações necessárias  

-   Executar uma recuperação local de acordo com o plano de recuperação de desastres em um laboratório de teste usando uma cópia do backup mais recente criada pela tarefa de manutenção Servidor do Site de Backup  

-   Verificar o hardware quanto a quaisquer erros ou atualizações de hardware disponíveis  

-   Verificar a integridade geral do site  

###  <a name="a-namebkmkusemtsa-maintain-the-operational-health-of-your-site-database"></a><a name="BKMK_UseMTs"></a> Manter a integridade operacional do banco de dados do site  
 Enquanto o site e a hierarquia do Configuration Manager executam as tarefas que você agenda e configura, os componentes do site adicionam dados continuamente ao banco de dados do Configuration Manager. À medida que o volume de dados aumenta, o desempenho do banco de dados e o espaço livre de armazenamento no banco de dados diminuem. Você pode configurar tarefas de manutenção do site para remover dados antigos que não precisa mais.  

 O Configuration Manager fornece tarefas de manutenção predefinidas que você pode usar para manter a integridade do banco de dados do Configuration Manager. Nem todas as tarefas de manutenção estão disponíveis em cada local. Por padrão, várias são habilitados, embora outras não, e todas suportam uma agenda que você pode configurar.  

 A maioria das tarefas de manutenção remove periodicamente dados desatualizados do banco de dados do Configuration Manager. A redução do tamanho do banco de dados pela remoção de dados desnecessários melhora o desempenho e a integridade do banco de dados, o que aumenta a eficácia do local e da hierarquia. Outras tarefas, como **Recompilar Índices**, ajudam a manter a eficiência do banco de dados, enquanto outras, como a tarefa **Servidor do Site de Backup** , ajudam você a se preparar para a recuperação de desastres.  

> [!IMPORTANT]  
>  Ao planejar a agenda de qualquer tarefa que exclui dados, considere o uso desses dados na hierarquia. Quando uma tarefa que exclui dados é executada em um site, a informação é removida do banco de dados do Configuration Manager e essa alteração é replicada em todos os sites na hierarquia. Isso pode afetar outras tarefas que dependem de dados. Por exemplo, no local da administração central, é possível configurar a Descoberta para ser executada uma vez por mês para identificar computadores não cliente e planejar a instalação do cliente do Configuration Manager nesses computadores duas semanas após sua descoberta. No entanto, em um site na hierarquia, um administrador configura a tarefa Excluir Dados Antigos de Descoberta para execução a cada sete dias, com um resultado que, sete dias após a descoberta de computadores não cliente, eles são excluídos do banco de dados do Configuration Manager. De volta no site de administração central, prepare-se para instalar por push o cliente do Configuration Manager nesses novos computadores no dia 10. No entanto, como a tarefa Excluir Dados Antigos de Descoberta foi executada recentemente e excluiu dados de sete dias ou mais, os computadores recém-descobertos não estão mais disponíveis no banco de dados.  

Depois de instalar um site do Configuration Manager, analise as tarefas de manutenção disponíveis e habilite aquelas de que suas operações precisam. Revise a agenda padrão de cada tarefa e, quando necessário, modifique a agenda para ajustar a tarefa de manutenção à sua hierarquia e ao seu ambiente. Embora o agendamento padrão de cada tarefa deva atender à maioria dos ambientes, monitore o desempenho de seus sites e do banco de dados e ajuste as tarefas para aumentar a eficiência de suas implantações. Planeje rever periodicamente o site e o desempenho do banco de dados e reconfigurar tarefas de manutenção e suas agendas para manter essa eficiência.  

#### <a name="configure-maintenance-tasks"></a>Configurar tarefas de manutenção  
 Cada site do Configuration Manager dá suporte a tarefas de manutenção que ajudam a manter a eficiência operacional do banco de dados do site. Por padrão, várias tarefas de manutenção estão habilitadas em cada site e agendamentos independentes oferecer suporte a todas as tarefas. Tarefas de manutenção são definidas individualmente para cada site e aplicam-se ao banco de dados nesse site; No entanto, algumas tarefas, como **Excluir dados antigos de descoberta**, afetam as informações disponíveis em todos os sites em uma hierarquia.  

 Somente as tarefas de manutenção que podem ser configuradas em um site são exibidas no console do Configuration Manager. Para obter uma lista completa de tarefas de manutenção por tipo de site, consulte [Referência para tarefas de manutenção do System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md)  

 Use o procedimento a seguir para ajudá-lo a definir as configurações comuns de tarefas de manutenção.  

###### <a name="to-configure-maintenance-tasks-for-configuration-manager"></a>Configurar tarefas de manutenção do Configuration Manager  

1.  No console do Configuration Manager, navegue até **Administração** > **Configuração de Site** >**Sites**.  

2.  Selecione o site que contém a tarefa de manutenção que você deseja configurar.  

3.  Sobre o **Home** guia o **configurações** clique em **manutenção do Site**, e, em seguida, selecione a tarefa de manutenção que você deseja configurar.  

    > [!TIP]  
    >  Somente as tarefas disponíveis no site selecionado são exibidas.  

4.  Para configurar a tarefa, clique em **Editar**, certifique-se de **habilitar esta tarefa** caixa de seleção está selecionada e configurar uma agenda para a execução da tarefa. Se a tarefa também exclui dados antigos, configure a idade dos dados que serão excluídos do banco de dados quando a tarefa é executada. Clique em **OK** para fechar a tarefa **propriedades**.  

    > [!NOTE]  
    >  Para **Excluir mensagens de Status antigos**, você configura a idade dos dados a serem excluídos quando você configura as regras de filtro de status.  

5.  Para habilitar ou desabilitar a tarefa sem editar as propriedades da tarefa, clique o **Habilitar** ou **Desabilitar** botão. O botão rótulo se altera dependendo da configuração atual da tarefa.  

6.  Quando tiver terminado de configurar as tarefas de manutenção, clique em **OK** para concluir o procedimento.



<!--HONumber=Nov16_HO1-->


