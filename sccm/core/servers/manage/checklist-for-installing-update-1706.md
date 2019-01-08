---
title: Lista de verificação para 1706
titleSuffix: Configuration Manager
description: Conheça as ações a serem executadas antes de atualizar para o System Center Configuration Manager versão 1706.
ms.date: 12/19/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7def067e-845c-4db3-9d56-fa1dcf2fd7c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c6d544b0bdc087a8d78bb677ed519711131c5a0d
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53414830"
---
# <a name="checklist-for-installing-update-1706-for-system-center-configuration-manager"></a>Lista de verificação para instalar a atualização 1706 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Ao usar a ramificação atual do System Center Configuration Manager, você pode instalar a atualização no console da versão 1706 para atualizar sua hierarquia da versão anterior.

Para obter a atualização da versão 1706, você deve usar uma função do sistema de sites do ponto de conexão de serviço no site de nível superior da hierarquia. Isso pode ser no modo online ou offline. Depois que a hierarquia baixar o pacote de atualização da Microsoft, você o encontrará no console em **Administração &gt; Visão Geral &gt; Serviços de Nuvem &gt; Atualizações e Manutenção**.

-   Quando a atualização for listada como **Disponível**, ela estará pronta para ser instalada. Antes de instalar a versão 1706, examine as seguintes informações [sobre a instalação da atualização 1706](#about-installing-update-1706) e a [lista de verificação](#checklist) para saber quais configurações devem ser feitas antes de iniciar a atualização.

-   Se a atualização for exibida como **Baixando** e não mudar, examine o **hman.log** e o **dmpdownloader.log** para verificar se há erros.

    -   Se o dmpdownloader.log indica que o processo de dmpdownloader está no estado de suspensão e esperando um intervalo para verificar se há atualizações, você pode reiniciar o serviço **SMS_Executive** no servidor do site para reiniciar o download dos arquivos de redistribuição da atualização.

    -   Outro problema de download comum ocorre quando as configurações do servidor proxy impedem downloads de <http://silverlight.dlservice.microsoft.com> e <http://download.microsoft.com>.

Para obter mais informações de como instalar atualizações, consulte [Atualizações e manutenção no console](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing).

Para obter informações sobre as versões do Branch Atual, consulte [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#bkmk_Baselines) em [Atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="about-installing-update-1706"></a>Sobre como instalar a atualização 1706

**Sites:**  
Instale a atualização 1706 no site de nível superior da hierarquia. Isso significa que você inicia a instalação no site de administração central, se tiver um, ou no site primário autônomo. Depois que a atualização for instalada no site de camada superior, os sites filho terão o seguinte comportamento de atualização:

-   Os sites filho primários iniciam automaticamente a atualização após a conclusão da instalação da atualização no site de administração central. Você pode usar períodos de serviço para controlar quando um site instala a atualização. Para obter mais informações, consulte [Service windows for site servers](/sccm/core/servers/manage/service-windows) (Períodos de serviço para servidores do site).

-   Você deve atualizar cada site secundário manualmente de dentro do console do Configuration Manager depois que a instalação da atualização estiver concluída no site pai primário. Não há suporte para atualização automática de servidores do site secundário.

**Funções do sistema de sites:**  
Quando um servidor do site instala a atualização, as funções de sistema de sites instaladas no computador do servidor do site e as instaladas em computadores remotos são atualizadas automaticamente. Antes de instalar a atualização, verifique se cada servidor do sistema de sites atende aos pré-requisitos para operação com a nova versão de atualização.

**Consoles do Configuration Manager:**   
Na primeira vez que você usar um console do Configuration Manager após a conclusão da atualização, será solicitada a atualização desse console. Para isso, você deve executar a instalação do Configuration Manager no computador que hospeda o console e escolher a opção para atualizar o console. É recomendável não postergar a instalação da atualização no console.

> [!IMPORTANT]  
> Quando você instala uma atualização no site de administração central, esteja ciente das seguintes limitações e atrasos existentes até que todos os sites primários filhos também concluam a instalação da atualização:    
> - **As atualizações do cliente** não são iniciadas. Isso inclui atualizações automáticas de clientes e clientes de pré-produção. Além disso, você não pode promover clientes de pré-produção para produção até que o último site conclua a instalação da atualização. Após o último site concluir a instalação da atualização, as atualizações do cliente serão iniciadas com base em suas opções de configuração.   
> - Os **novos recursos** que você habilita com a atualização não estão disponíveis. Isso é para impedir que a replicação de dados relacionada a esse recurso seja enviada a um site que ainda não instalou o suporte para esse recurso. Depois que todos os sites primários instalarem a atualização, o recurso estará disponível para uso.   
> - Os **links de replicação** entre o site de administração central e os sites primários filhos são exibidos como não atualizados. Isso é exibido no status de instalação do pacote de atualização como um status de Concluído com aviso para monitorar a inicialização de replicação. No nó Monitoramento do console, é exibido como *O link está sendo configurado*.


## <a name="checklist"></a>Lista de Verificação

**Verifique se todos os sites executam uma versão do System Center Configuration Manager que fornece suporte à atualização até o 1706:**   
Cada servidor do site na hierarquia deve executar a mesma versão do System Center Configuration Manager para que você possa iniciar a instalação da atualização 1706. Para atualizar para a 1706, você deverá usar a versão 1606, 1610 ou 1702.

**Examine o status do seu Software Assurance ou de seus direitos de assinatura equivalentes:**   
Você precisa ter um contrato de SA (Software Assurance) ativo para instalar a atualização 1706. Ao instalar essa atualização, a guia **Licenciamento** apresentará a opção para confirmar a **data de expiração do Software Assurance**.

Esse é um valor opcional que você pode especificar como um lembrete conveniente da data de expiração da sua licença. Essa data é visível quando você instala as atualizações futuras. É possível que você já tenha especificado esse valor anteriormente durante a configuração ou instalação de uma atualização, ou na guia **Licenciamento** das **Configurações da Hierarquia** dentro do console do Configuration Manager.

Para mais informações, consulte [Licenciamento e branches do System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

**Examine as versões do Microsoft .NET instaladas nos servidores do sistema de sites:**  quando um site instala essa atualização, o Configuration Manager instala automaticamente o .NET Framework 4.5.2 em cada computador que hospeda uma das seguintes funções do sistema de sites quando o .NET Framework 4.5 ou posterior ainda não está instalado:

-   Ponto proxy do registro
-   Ponto de registro
-   Ponto de gerenciamento
-   Ponto de Conexão de Serviço

Essa instalação pode colocar o servidor do sistema de sites em um estado de reinicialização pendente e relatar erros ao visualizador de status de componente do Configuration Manager. Além disso, os aplicativos .NET no servidor podem ter falhas aleatórias até que o servidor seja reinicializado.

Para obter mais informações, confira [Pré-requisitos do site e do sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

**Reveja a versão do ADK (Kit de Avaliação e Implantação) do Windows para o Windows 10** O Windows 10 ADK deve ser da versão 1703 ou posterior. (Para obter mais informações sobre versões com suporte do Windows ADK, consulte [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).) Se você precisar atualizar o Windows ADK, faça isso antes de começar a atualização do Configuration Manager. Isso garante que as imagens de inicialização padrão serão automaticamente atualizadas para a versão mais recente do Windows PE. (As imagens de inicialização personalizada devem ser atualizadas manualmente.)

Se você atualizar o site antes de atualizar o Windows ADK, consulte [Atualizar pontos de distribuição com a imagem de inicialização](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image) para encontrar melhorias para esse processo no Configuration Manager versão 1706.

**Examine o status do site e da hierarquia e verifique se não existem problemas não resolvidos:**  Antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, do servidor de banco de dados do site e das funções do sistema de site que estão instalados em computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.

Para obter mais informações, confira [Usar alertas e o sistema de status do System Center Configuration Manager](/sccm/core/servers/manage/use-alerts-and-the-status-system).

**Examine a replicação de arquivo e dados entre sites:**   
Verifique se a replicação de arquivo e banco de dados entre sites está operacional e atualizada. Atrasos ou listas de pendências em qualquer um deles podem impedir uma atualização tranquila ou bem-sucedida.
Para replicação de banco de dados, você pode usar o Replication Link Analyzer para ajudar na resolução de problemas antes de iniciar a atualização.

Para obter mais informações, confira [Sobre o Replication Link Analyzer](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA) no tópico [Monitorar a infraestrutura de hierarquia e de replicação no System Center Configuration Manager](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure) .

**Instale todas as atualizações críticas aplicáveis para sistemas operacionais em computadores que hospedam o site, o servidor de banco de dados do site e as funções do sistema de sites remoto:**  antes de instalar uma atualização do Configuration Manager, instale todas as atualizações críticas de cada sistema de sites aplicável. Se uma atualização instalada precisar de uma reinicialização, reinicie os computadores aplicáveis antes de iniciar a atualização.

**Desabilitar réplicas de banco de dados para pontos de gerenciamento em sites primários:**   
O Configuration Manager não pode atualizar com êxito um site primário que tenha uma réplica de banco de dados habilitada para pontos de gerenciamento. Desabilite a replicação de banco de dados antes de instalar uma atualização para o Configuration Manager.

Para obter mais informações, consulte [Réplicas de banco de dados para pontos de gerenciamento no System Center Configuration Manager](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).

**Definir Grupos de Disponibilidade AlwaysOn do SQL Server para failover manual:**   
Se você usar um grupo de disponibilidade, verifique se o grupo de disponibilidade está definido como failover manual antes de iniciar a instalação da atualização. Após a atualização do site, você pode restaurar o failover para que ele seja automático. Para obter mais informações, confira [AlwaysOn do SQL Server para um banco de dados do site](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

**Reconfigure os pontos de atualização de software que usam NLBs:**   
O Configuration Manager não pode atualizar um site que usa um cluster de NLB (balanceamento de carga de rede) para hospedar pontos de atualização de software.

Se você usar clusters NLB para pontos de atualização de software, use o Windows PowerShell para remover o cluster NLB.
Para obter mais informações, confira [Planejar atualizações de software no System Center Configuration Manager](/sccm/sum/plan-design/plan-for-software-updates).

**Desabilite todas as tarefas de manutenção do site em cada site durante a instalação da atualização nesse site:**   
Antes de instalar a atualização, desabilite todas as tarefas de manutenção do site que possam ser executadas durante o período em que o processo de atualização estiver ativo. Isso inclui, mas não está limitado ao seguinte:

-   Servidor do Site de Backup
-   Excluir Operações Antigas do Cliente
-   Excluir Dados Antigos de Descoberta

Há possibilidade de falha na instalação da atualização quando uma tarefa de manutenção do banco de dados do site for executada durante o processo da instalação. Antes de desabilitar uma tarefa, registre o agendamento da tarefa para que você possa restaurá-la depois que a atualização estiver instalada.

Para obter mais informações, confira [Tarefas de manutenção do System Center Configuration Manager](/sccm/core/servers/manage/maintenance-tasks) e [Referência das tarefas de manutenção do System Center Configuration Manager](/sccm/core/servers/manage/reference-for-maintenance-tasks).

**Interrompa temporariamente o software antivírus nos servidores do System Center Configuration Manager:** antes de atualizar um site, verifique se você interrompeu o software antivírus nos servidores do Configuration Manager. <!--SMS.503481--> 

**Crie um backup do banco de dados do site no site de administração central e nos sites primários:**  antes de atualizar um site, faça backup do banco de dados do site para garantir um backup bem-sucedido a ser usado para recuperação de desastre.

Para obter mais informações, confira [Backup e recuperação do System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

**Planeje o cliente piloto:**   
Ao instalar uma atualização que atualiza o cliente, você pode testar essa nova atualização do cliente em pré-produção antes que ela seja implantada e atualize todos os clientes ativos.

Para aproveitar essa opção, antes de começar a instalação da atualização, você deve configurar o site para dar suporte às atualizações automáticas para pré-produção.

Para saber mais, confira [Atualizar clientes no System Center Configuration Manager](/sccm/core/clients/manage/upgrade/upgrade-clients) e [Como testar atualizações do cliente em uma coleção de pré-produção no System Center Configuration Manager](/sccm/core/clients/manage/upgrade/test-client-upgrades).

**Planeje usar períodos de serviço para controlar quando os servidores do site instalam atualizações:**   
Use períodos de serviço para definir um período durante o qual as atualizações de um servidor de sites possam ser instaladas.

Isso pode ajudar a controlar quando os sites em sua hierarquia instalam a atualização. Para obter mais informações, confira [Períodos de serviço para servidores do site](/sccm/core/servers/manage/service-windows).

**Execute o verificador de pré-requisitos de instalação:**   
Quando a atualização está listada no console como **Disponível**, você pode executar o verificador de pré-requisitos independentemente antes de instalar a atualização. (Ao instalar a atualização no site, o verificador de pré-requisitos é executado novamente).

Para executar um verificador de pré-requisitos a partir do console, vá para **Administração > Visão geral > Serviços de Nuvem > Atualizações e Manutenção.** Em seguida, clique com botão direito do mouse em **Pacote de atualização do Configuration Manager 1706** e escolha **Executar verificação de pré-requisitos**.

Para saber mais sobre como iniciar e monitorar a verificação de pré-requisitos, confira **Etapa 3: Executar o verificador de pré-requisitos antes de instalar uma atualização** no tópico [Instalar atualizações no console do System Center Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).

> [!IMPORTANT]  
> Quando o verificador de pré-requisitos for executado como parte de uma instalação de atualização ou de modo independente, o processo atualizará alguns arquivos de origem do produto que são usados para tarefas de manutenção do site. Portanto, após executar o verificador de pré-requisitos, mas antes de instalar a atualização, se você precisa executar uma tarefa de manutenção de site, execute **Setupwpf.exe**  (Instalação do Configuration Manager) na pasta CD.Latest no servidor de sites.

**Sites de atualização:**   
Agora você está pronto para iniciar a instalação da atualização para sua hierarquia. Para saber mais sobre como instalar a atualização, veja [Instalação de atualizações no console.](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates)

Recomendamos que você planeje a instalação da atualização fora do horário comercial normal de cada site, quando o processo de instalação da atualização e suas ações de reinstalação dos componentes do site e das funções do sistema de sites terão um efeito mínimo sobre as operações de seu negócio.

Para obter mais informações, confira [Atualizações do System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="post-update-checklist"></a>Lista de verificação pós-atualização
Examine as seguintes ações a serem executadas depois que a instalação da atualização tiver sido concluída.
1. Verifique se a replicação de site a site está ativa. No console, exiba **Monitoramento** > **Hierarquia do Site** e **Monitoramento** > **Replicação de Banco de Dados** para obter indicações de problemas ou confirmação de que os links de replicação estão ativos.
2. Verifique se cada servidor do site e a função do sistema de site foram atualizados para a versão 1706. No console, você pode adicionar a coluna opcional **Versão** para a exibição de alguns nós incluindo **Sites** e **Pontos de Distribuição**.

   Quando necessário, uma função de sistema de site será reinstalada automaticamente para ser atualizada para a nova versão. Reinicie os sistemas de site remoto que não foram atualizados com êxito.
3. Reconfigure as réplicas de banco de dados para pontos de gerenciamento em sites primários que você desabilitou antes de iniciar a atualização.
4. Reconfigure as tarefas de manutenção de banco de dados que foram desabilitadas antes de iniciar a atualização.
5. Se você configurou o piloto de cliente antes de instalar a atualização, atualize os clientes de acordo com o plano que você criou.

## <a name="known-issues"></a>Problemas conhecidos 
Depois de atualizar para a versão 1706, cada vez que o SMS_Executive inicia, a seguinte mensagem de status de aviso é criada pelo SMS_CERTIFICATE_MANAGER:
-    Microsoft SQL Server reported SQL message 515, severity 16: [23000][515][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot insert the value NULL into column 'RowVersion', table 'CM_GF1.dbo.AAD_SecretChange_Notify'; column does not allow nulls. INSERT fails.

Essa mensagem pode ser ignorada.  Ela ocorre quando não há serviços de nuvem configurados para uso antes de atualizar para a versão 1706. Esse problema será resolvido em uma versão futura.
