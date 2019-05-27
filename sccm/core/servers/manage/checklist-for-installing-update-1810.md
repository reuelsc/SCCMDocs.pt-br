---
title: Lista de verificação para 1810
titleSuffix: Configuration Manager
description: Conheça as ações a serem executadas antes de atualizar para o Configuration Manager versão 1810.
ms.date: 02/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b87ac054-9b37-4725-a3f3-2340cfb10bff
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c57042e6ea4db7b244b8617bbef99633d9026d1b
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65501120"
---
# <a name="checklist-for-installing-update-1810-for-configuration-manager"></a>Lista de verificação para instalar a atualização 1810 do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Ao usar o branch atual do Configuration Manager, é possível instalar a atualização no console da versão 1810 para atualizar a hierarquia de uma versão anterior. <!-- baseline only statement: (Because version 1802 is also available as [baseline media](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions), you can use the installation media to install the first site of a new hierarchy.)-->

Para obter a atualização da versão 1810, você precisa usar um ponto de conexão de serviço no site de nível superior da hierarquia. Essa função do sistema de sites pode estar no modo online ou offline. Depois que a hierarquia baixar o pacote de atualização da Microsoft, encontre-a no console. No workspace **Administração** e selecione o nó **Atualizações e Manutenção**.

-   Quando a atualização for listada como **Disponível**, ela estará pronta para ser instalada. Antes de instalar a versão 1810, examine as informações a seguir [sobre como instalar a atualização 1810](#about-installing-update-1810) e a [lista de verificação](#checklist) para saber quais configurações devem ser feitas antes do início da atualização.

-   Se a atualização for exibida como **Baixando** e não mudar, examine **hman.log** e **dmpdownloader.log** para verificar se há erros.

    -   O dmpdownloader.log pode indicar que o processo de dmpdownloader está aguardando um intervalo antes de verificar se há atualizações. Para reiniciar o download dos arquivos de redistribuição de atualizações, reinicie o serviço **SMS_Executive** no servidor do site.

    -   Outro problema de download comum ocorre quando as configurações do servidor proxy impedem downloads de http://silverlight.dlservice.microsoft.com, http://download.microsoft.com e/ou http://go.microsoft.com.

Para obter mais informações de como instalar atualizações, consulte [Atualizações e manutenção no console](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing).

Para obter mais informações sobre as versões do branch atual, veja [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#bkmk_Baselines).



## <a name="about-installing-update-1810"></a>Sobre a instalação da atualização 1810

#### <a name="sites"></a>Sites
Instale a atualização 1810 no site de nível superior da sua hierarquia. Inicie a instalação de seu site de administração central ou de seu site primário autônomo. Depois que a atualização for instalada no site de nível superior, os sites filho terão o seguinte comportamento de atualização:

-   Os sites filho primários iniciam automaticamente a atualização após a conclusão da instalação da atualização no site de administração central. Você pode usar períodos de serviço para controlar quando um site instala a atualização. Para obter mais informações, consulte [Service windows for site servers](/sccm/core/servers/manage/service-windows) (Períodos de serviço para servidores do site).

-   Atualize manualmente cada site secundário de dentro do console do Configuration Manager depois que o site pai primário concluir a instalação da atualização. Não há suporte para a atualização automática de servidores do site secundário.

#### <a name="site-system-roles"></a>Funções do sistema de site
Quando um servidor do site instalar a atualização, ele atualizará automaticamente todas as funções do sistema de sites. Essas funções estão no servidor do site ou instaladas em servidores remotos. Antes de instalar a atualização, verifique se cada servidor do sistema de sites atende aos pré-requisitos atuais para a nova versão de atualização.

#### <a name="configuration-manager-consoles"></a>Consoles do Configuration Manager   
Na primeira vez que você usar um console do Configuration Manager após a conclusão da atualização, será solicitado a atualizar esse console. Você também pode executar a instalação do Configuration Manager no computador que hospeda o console e escolher a opção para atualizar o console. Instale a atualização no console assim que possível. Para obter mais informações, veja [Instalar o console do Configuration Manager](/sccm/core/servers/deploy/install/install-consoles).

> [!IMPORTANT]  
> Quando você instala uma atualização no site de administração central, esteja ciente das seguintes limitações e atrasos existentes até que todos os sites primários filhos também concluam a instalação da atualização:    
> - **As atualizações do cliente** não são iniciadas. Isso inclui atualizações automáticas de clientes e clientes de pré-produção. Além disso, você não pode promover clientes de pré-produção para produção até que o último site conclua a instalação da atualização. Após o último site concluir a instalação da atualização, as atualizações do cliente serão iniciadas com base em suas opções de configuração.   
> - Os **novos recursos** que você habilita com a atualização não estão disponíveis. Isso é para impedir que a replicação de dados relacionada a esse recurso seja enviada a um site que ainda não instalou o suporte para esse recurso. Depois que todos os sites primários instalarem a atualização, o recurso estará disponível para uso.   
> - Os **links de replicação** entre o site de administração central e os sites primários filhos são exibidos como não atualizados. Isso é exibido no status de instalação do pacote de atualização como um status de Concluído com aviso para monitorar a inicialização de replicação. No nó Monitoramento do console, é exibido como *O link está sendo configurado*.


## <a name="checklist"></a>Lista de Verificação

#### <a name="all-sites-run-a-supported-version-of-configuration-manager"></a>Todos os sites executam uma versão com suporte do Configuration Manager  
Cada servidor do site na hierarquia deve executar a mesma versão do Configuration Manager para que você possa iniciar a instalação da atualização 1810. Para atualizar para a 1810, use a versão 1710, 1802 ou 1806.

#### <a name="review-the-status-of-your-product-licensing"></a>Examinar o status de licenciamento de produtos 
Você deve ter direitos de assinatura equivalentes para instalar essa atualização ou um contrato de SA (Software Assurance) ativo. Ao atualizar o site, a página **Licenciamento** apresentará a opção de confirmar a **Data de expiração do Software Assurance**.

Esse valor é opcional. Você pode especificar como um lembrete conveniente da data de validade de licença. Essa data é visível quando você instala as atualizações futuras. Você talvez tenha especificado esse valor anteriormente durante a configuração ou a instalação de uma atualização. Você também pode especificar esse valor no console do Configuration Manager. No workspace **Administração**, expanda **Configuração do Site** e selecione **Sites**. Clique em **Configurações da Hierarquia** na faixa de opções e mude para a guia **Licenciamento**.

Para obter mais informações, veja [Licenciamento e branches](/sccm/core/understand/learn-more-editions).

#### <a name="review-microsoft-net-versions"></a>Examinar as versões do Microsoft .NET 
Quando um site instala esta atualização, se o requisito mínimo do .NET Framework 4.5 não estiver instalado, o Configuration Manager instalará automaticamente o .NET Framework 4.5.2. Quando esse pré-requisito ainda não estiver instalado, o site será instalado em cada servidor que hospeda uma das seguintes funções do sistema de site:

-   Ponto de gerenciamento
-   Ponto de Conexão de Serviço
-   Ponto proxy do registro
-   Ponto de registro

Essa instalação pode colocar o servidor do sistema de sites em um estado de reinicialização pendente e relatar erros ao visualizador de status de componente do Configuration Manager. Além disso, os aplicativos .NET no servidor podem ter falhas aleatórias até que o servidor seja reinicializado.

Para obter mais informações, confira [Pré-requisitos do site e do sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

#### <a name="review-the-version-of-the-windows-adk-for-windows-10"></a>Examinar a versão do Windows ADK para Windows 10
A versão do ADK (Kit de Avaliação e Implantação) do Windows 10 deve ter suporte para o Configuration Manager versão 1810. Para obter mais informações sobre versões com suporte do Windows ADK, veja [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk). Se você precisar atualizar o Windows ADK, faça isso antes de começar a atualização do Configuration Manager. Essa ordem garante que as imagens de inicialização padrão sejam automaticamente atualizadas para a versão mais recente do Windows PE. Atualize manualmente todas as imagens de inicialização personalizadas após atualizar o site.

Caso você atualize o site antes de atualizar o Windows ADK, consulte [Atualizar pontos de distribuição com a imagem de inicialização](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image).

#### <a name="review-sql-server-native-client-version"></a>Revisar a versão do SQL Server Native Client
Deve ser instalada uma versão mínima do SQL Server 2012 Native Client que inclui suporte para o TLS 1.2. Para obter mais informações, confira a [Lista de verificações de pré-requisitos](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#sql-native-client).

#### <a name="review-the-site-and-hierarchy-status-for-unresolved-issues"></a>Examine o status do site e da hierarquia quanto a problemas não resolvidos 
Uma atualização de site pode falhar devido a problemas operacionais existentes. Antes de atualizar um site, resolva todos os problemas operacionais para os seguintes sistemas:  
- O servidor do site  
- O servidor de banco de dados do site  
- Funções do sistema de site remoto em outros servidores   

Para obter mais informações, confira [Usar alertas e o sistema de status](/sccm/core/servers/manage/use-alerts-and-the-status-system).

#### <a name="review-file-and-data-replication-between-sites"></a>Examinar a replicação de arquivo e dados entre sites   
Garanta que a replicação de arquivo e banco de dados entre sites esteja operacional e atualizada. Atrasos ou listas de pendências em qualquer um deles podem impedir uma atualização tranquila ou bem-sucedida. Para replicação de banco de dados, você pode usar o Replication Link Analyzer para ajudar na resolução de problemas antes de iniciar a atualização.

Para obter mais informações, veja [Sobre o Replication Link Analyzer](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA).

#### <a name="install-all-applicable-critical-windows-updates"></a>Instalar todas as atualizações do Windows críticas aplicáveis
Antes de instalar uma atualização para o Configuration Manager, instale quaisquer atualizações críticas do sistema operacional para cada sistema de sites aplicável. Esses servidores incluem o servidor do site, o servidor de banco de dados do site e funções do sistema de site remoto. Se uma atualização instalada precisar de uma reinicialização, reinicie os servidores aplicáveis antes de iniciar a atualização.

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Desabilite réplicas de banco de dados para pontos de gerenciamento em sites primários   
O Configuration Manager não pode atualizar com êxito um site primário que tenha uma réplica de banco de dados habilitada para pontos de gerenciamento. Antes de instalar uma atualização para o Configuration Manager, desabilite a replicação de banco de dados.

Para obter mais informações, consulte [Réplicas de banco de dados para pontos de gerenciamento](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).

#### <a name="set-sql-server-alwayson-availability-groups-to-manual-failover"></a>Definir grupos de disponibilidade AlwaysOn do SQL Server para failover manual   
Se você usar um grupo de disponibilidade, garanta que o grupo de disponibilidade esteja definido como failover manual antes de iniciar a instalação da atualização. Após a atualização do site, você pode restaurar o failover para que seja automático. Para saber mais, confira [SQL Server AlwaysOn para um banco de dados do site](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

#### <a name="disable-site-maintenance-tasks-at-each-site"></a>Desabilitar as tarefas de manutenção de site em cada site
Antes de instalar a atualização, desabilite todas as tarefas de manutenção do site que possam ser executadas durante o período em que o processo de atualização estiver ativo. Por exemplo, entre outros:

-   Servidor do Site de Backup
-   Excluir Operações Antigas do Cliente
-   Excluir Dados Antigos de Descoberta

Há possibilidade de falha na instalação da atualização quando uma tarefa de manutenção do banco de dados do site for executada durante o processo da instalação. Antes de desabilitar uma tarefa, registre o agendamento da tarefa para que você possa restaurá-la depois que a atualização estiver instalada.

Para obter mais informações, confira [Tarefas de manutenção](/sccm/core/servers/manage/maintenance-tasks) e [Referência para tarefas de manutenção](/sccm/core/servers/manage/reference-for-maintenance-tasks).

#### <a name="temporarily-stop-any-antivirus-software"></a>Interromper temporariamente qualquer software antivírus 
Antes de atualizar um site, interrompa o software antivírus nos servidores do Configuration Manager. <!--SMS.503481--> 

#### <a name="create-a-backup-of-the-site-database"></a>Criar um backup do banco de dados do site 
Antes de atualizar um site, faça o backup do banco de dados do site no site de administração central e nos sites primários. Esse backup garante que você tenha um backup bem-sucedido a ser usado para recuperação de desastre.

Para obter mais informações, confira [Backup e recuperação](/sccm/protect/understand/backup-and-recovery).

#### <a name="plan-for-client-piloting"></a>Planejar a criação do piloto do cliente   
Ao instalar uma atualização que atualiza o cliente, você pode testar essa nova atualização do cliente em pré-produção antes que ela seja implantada e atualize todos os clientes ativos. Para aproveitar essa opção, antes de começar a instalação da atualização, você deve configurar o site para dar suporte às atualizações automáticas para pré-produção.

Para obter mais informações, confira [Atualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients) e [Como testar atualizações do cliente em uma coleção de pré-produção](/sccm/core/clients/manage/upgrade/test-client-upgrades).

#### <a name="plan-to-use-service-windows"></a>Planejar o uso de janelas de serviço   
Para definir um período no qual as atualizações a um servidor do site podem ser instaladas, use as janelas de serviço. Isso pode ajudar a controlar quando os sites em sua hierarquia instalam a atualização. Para obter mais informações, confira [Períodos de serviço para servidores do site](/sccm/core/servers/manage/service-windows).

#### <a name="review-supported-extensions"></a>Examinar extensões com suporte
<!--SCCMdocs#587-->
Se você ampliar o Configuration Manager com outros produtos da Microsoft ou de parceiros da Microsoft, confirme se eles dão suporte à versão 1810. Solicite essas informações ao fornecedor do produto. Por exemplo, confira as [notas de versão](/sccm/mdt/release-notes) do Microsoft Deployment Toolkit.

#### <a name="run-the-setup-prerequisite-checker"></a>Executar o verificador de pré-requisitos de instalação   
Quando a atualização está listada no console como **Disponível**, você pode executar o verificador de pré-requisitos independentemente antes de instalar a atualização. (Ao instalar a atualização no site, o verificador de pré-requisitos é executado novamente).

Para executar uma verificação de pré-requisitos usando o console, acesse o workspace **Administração** e selecione **Atualizações e Manutenção**. Selecione o pacote de atualização **Configuration Manager 1810** e, em seguida, clique em **Executar verificação de pré-requisitos** na faixa de opções.

Para obter mais informações, veja a seção **Executar o verificador de pré-requisitos antes de instalar uma atualização** em [Antes de instalar uma atualização no console](/sccm/core/servers/manage/install-in-console-updates#bkmk_beforeinstall).

> [!IMPORTANT]  
> Quando o verificador de pré-requisitos é executado, o processo atualiza alguns arquivos de origem do produto usados para tarefas de manutenção do site. Portanto, após executar o verificador de pré-requisitos, mas antes de instalar a atualização, se você precisa executar uma tarefa de manutenção de site, execute **Setupwpf.exe**  (Instalação do Configuration Manager) na pasta CD.Latest no servidor de sites.

#### <a name="update-sites"></a>Atualizar sites   
Agora você está pronto para iniciar a instalação da atualização para a sua hierarquia. Para saber mais sobre como instalar a atualização, veja [Instalação de atualizações no console](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).

Você pode planejar a instalação da atualização fora do horário comercial normal. Determine quando o processo terá um efeito mínimo sobre as suas operações de negócios. Instalar a atualização e suas ações reinstala os componentes do site e as funções do sistema de sites.

Para mais obter informações, confira [Atualizações ao Configuration Manager](/sccm/core/servers/manage/updates).



## <a name="post-update-checklist"></a>Lista de verificação pós-atualização

Após as atualizações do site, use a lista de verificação a seguir para concluir tarefas comuns e configurações.


#### <a name="confirm-version-and-restart-if-necessary"></a>Confirme a versão e reinicie (se necessário)
Verifique se todos os servidores do site e todas as funções do sistema de sites foram atualizados para a versão 1810. No console, adicione a coluna **Versão** aos nós **Sites** e **Pontos de Distribuição** no workspace **Administração**. Quando necessário, uma função do sistema de sites será reinstalada automaticamente para ser atualizada para a nova versão. 

Considere reiniciar sistemas de site remoto que não são atualizados com êxito no início. Examine a infraestrutura do site e verifique se os servidores do site e os servidores do sistema de site remoto aplicáveis foram reinicializados com êxito. Normalmente, os servidores de site são reiniciados apenas quando o Configuration Manager instala o .NET como pré-requisito para uma função de sistema de sites.


#### <a name="confirm-site-to-site-replication-is-active"></a>Confirme se a replicação site a site está ativa
No console do Configuration Manager, vá para os locais a seguir para exibir o status e verificar se a replicação está ativa:  

-   Workspace de **Monitoramento**, nó **Hierarquia do Site**  

-   Workspace de **Monitoramento**, nó **Replicação de Banco de Dados**  

Para obter mais informações, consulte os seguintes artigos:  
- [Monitorar a infraestrutura de hierarquia e de replicação](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure)
- [Sobre o Replication Link Analyzer](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA)  


#### <a name="update-configuration-manager-consoles"></a>Atualizar consoles do Configuration Manager
Atualize todos os consoles remotos do Configuration Manager para a mesma versão. Você será solicitado a atualizar o console quando:  

-   Abra o console.  

-   Vá para um novo nó no console.  


#### <a name="reconfigure-database-replicas-for-management-points"></a>Reconfigurar réplicas de banco de dados para pontos de gerenciamento
Depois de atualizar um site primário, reconfigure a réplica de banco de dados para pontos de gerenciamento que você desinstalou antes de atualizar o site. Para obter mais informações, consulte [Réplicas de banco de dados para pontos de gerenciamento](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).  


#### <a name="reconfigure-any-disabled-maintenance-tasks"></a>Reconfigurar quaisquer tarefas de manutenção desabilitadas
Se você tiver desabilitado as [tarefas de manutenção](/sccm/core/servers/manage/maintenance-tasks) do banco de dados em um site antes de instalar a atualização, reconfigure-as. Use as mesmas configurações que estavam em vigor antes da atualização.  


#### <a name="update-clients"></a>Atualizar clientes
Atualize os clientes de acordo com o plano que você criou, principalmente se você configurou o piloto de cliente antes de instalar a atualização. Para obter mais informações, consulte [Como atualizar clientes em computadores Windows](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers).  


#### <a name="third-party-extensions"></a>Extensões de terceiros
Se você usar alguma extensão do Configuration Manager, atualize-a para a versão mais recente para dar suporte ao Configuration Manager versão 1810. 


#### <a name="update-custom-boot-images-and-media"></a>Atualizar imagens e mídia de inicialização personalizadas
<!--SCCMDocs issue 775-->

Use a ação **Atualizar pontos de distribuição** para qualquer imagem de inicialização usada, seja uma imagem de inicialização padrão ou personalizada. Essa ação garante que os clientes possam usar a versão mais recente. Mesmo se não houver uma nova versão do Windows ADK, os componentes do cliente do Configuration Manager poderão ser alterados com uma atualização. Se você não atualizar as imagens e a mídia de inicialização, as implantações de sequência de tarefas poderão falhar nos dispositivos. 

Quando você atualiza o site, o Configuration Manager atualiza automaticamente as imagens de inicialização *padrão*. Ele não distribui automaticamente o conteúdo atualizado para os pontos de distribuição. Use a ação **Atualizar pontos de distribuição** em imagens de inicialização específicas quando você estiver pronto para distribuir esse conteúdo em sua rede. 

Após atualizar o site, atualize manualmente todas as imagens de inicialização *personalizadas*. Essa ação atualiza a imagem de inicialização com os componentes cliente mais recentes e, se necessário, opcionalmente, a recarrega com a versão atual do Windows PE e redistribui o conteúdo para os pontos de distribuição. 

Para saber mais, confira [Atualizar pontos de distribuição com a imagem de inicialização](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image). 
