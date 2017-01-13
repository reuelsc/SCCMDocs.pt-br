---
title: "Transferências de dados | Microsoft Docs"
description: "Saiba como o Configuration Manager move dados entre sites e como é possível gerenciar a transferência de dados pela rede."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
caps.latest.revision: 12
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: e290a5491fbd43ddf3ca8f4cf6f122ac862103d1


---
# <a name="data-transfers-between-sites-in-system-center-configuration-manager"></a>Transferência de dados entre sites no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager usa a **replicação baseada em arquivo** e **replicação de banco de dados** para transferir diferentes tipos de informações entre sites.  Os seguintes assuntos deste tópico podem ajudá-lo a entender como o Configuration Manager move dados entre sites e como é possível gerenciar a transferência deles em sua rede.  


##  <a name="a-namebkmkfileroutea-file-based-replication"></a><a name="bkmk_fileroute"></a> File-based replication  
 O Configuration Manager usa a replicação baseada em arquivo para transferir dados baseados em arquivo entre sites em sua hierarquia. Esses dados incluem conteúdo tais como aplicativos e pacotes que você deseja implantar em pontos de distribuição em sites filho e os registros de dados de descoberta não processados que são transferidos para sites pai onde são processados.  

 A comunicação baseada em arquivo entre sites usa o protocolo **SMB** por meio da porta **TCP/IP 445**. É possível especificar as configurações que incluem a limitação da largura de banda e o modo de pulso para controlar a quantidade de dados transferidos pela rede, e agendamentos para controlar quando enviar os dados pela rede.  

###  <a name="a-namebkmkroutesa-file-replication-routes"></a><a name="bkmk_routes"></a> Rotas de replicação de arquivo  
 As informações a seguir podem ajudar você a configurar e usar as rotas de replicação de arquivo:  

 **Rota de replicação de arquivo** - Cada rota de replicação de arquivo identifica um site de destino para o qual os dados baseados em arquivo podem ser transferidos. Cada site oferece suporte a uma única rota de replicação de arquivo para um site de destino específico.  

 O Configuration Manager dá suporte às seguintes configurações para as rotas de replicação de arquivo:  

-   **Conta de Replicação de Arquivo**: esta conta é usada para conectar-se ao site de destino e para gravar dados no compartilhamento **SMS_SITE** desse site. Os dados gravados nesse compartilhamento são processados pelo site de recebimento. Por padrão, quando um site é adicionado à hierarquia, o Configuration Manager atribui a conta do computador dos novos servidores do sistema de site como os sites **Conta de Replicação de Arquivo**. Esta conta é adicionada ao grupo **SMS_SiteToSiteConnection_&lt;Códigodosite\>** do site de destino que é um grupo local no computador que concede acesso ao compartilhamento do **SMS_SITE**. Você pode alterar essa conta para ser uma conta de usuário do Windows. Se você alterar a conta, certifique-se de adicionar a nova conta ao grupo **SMS_SiteToSiteConnection_&lt;Códigodosite\>** do site de destino.  

    > [!NOTE]  
    >  Os sites secundários sempre usam a conta do computador do servidor do site secundário como a **Conta de Replicação de Arquivo**.  

-   **Agendamento**: você pode configurar o agendamento para cada rota de replicação de arquivo para restringir o tipo de dados e a hora quando os dados podem ser transferidos para o site de destino.  

-   **Limites de Taxa**: você pode configurar os limites de taxa para cada rota de replicação de arquivo para controlar a largura de banda da rede usada quando o site transfere os dados ao site de destino:  

    -   Use o **Modo de pulso** para especificar o tamanho dos blocos de dados que são enviados ao site de destino. Você também pode especificar um retardo de tempo entre o envio de cada bloco de dados. Use essa opção quando você deve enviar dados através de uma conexão de rede com largura de banda bem baixa ao site de destino. Por exemplo, você pode ter restrições para enviar 1 KB de dados a cada cinco segundos, mas não 1 KB a cada três segundos, independentemente da velocidade do link ou seu uso em um determinado tempo.  

    -   Use **Limitado às taxas de transferência máximas especificadas por hora** para que um site envie dados para o site de destino usando somente a porcentagem de tempo que você especificar. Ao usar essa opção, o Configuration Manager não identifica a largura de banda disponível da rede, mas, em vez disso, ele divide o tempo em que pode enviar dados em períodos de tempo. Os dados são enviados em um curto bloco de tempo, que é seguido por blocos de tempo quando os dados não são enviados. Por exemplo, se a taxa máxima está definida como **50%**, o Configuration Manager transmite dados por um período de tempo seguido de igual período quando nenhum dado é enviado. A quantidade de tamanho real de dados ou o tamanho do bloco de dados não é gerenciado. Em vez disso, somente a quantidade de tempo durante a qual os dados são enviados é gerenciada.  

        > [!CAUTION]  
        >  Por padrão, um site pode usar até três **envios simultâneos** para transferir dados a um site de destino. Ao habilitar limites de taxa a uma rota de replicação de arquivo, os **envios simultâneos** para envio de dados para aquele site são limitados a um. Isso se aplica mesmo se o **Limite da largura de banda disponível (%)** está definido como **100%**. Por exemplo, se você usa as configurações padrão para o remetente, isso reduz a taxa de transferência ao site de destino para um terço da capacidade padrão.  

-   Você pode configurar uma rota de replicação de arquivo entre dois sites secundários para o conteúdo baseado em arquivo de rota entre esses sites.  

Para gerenciar uma rota de replicação de arquivo, no espaço de trabalho **Administração** , expanda o nó **Configuração da Hierarquia** e selecione **Replicação de Arquivo**.  

**Remetente** - Cada site tem um remetente. O remetente gerencia a conexão de rede de um site para um site de destino, e pode estabelecer conexões com vários sites ao mesmo tempo. Para conectar a um site, o remetente usa a rota de replicação de arquivos até o site para identificar a conta a ser usada para estabelecer a conexão de rede. O remetente também usa essa conta para gravar dados no compartilhamento **SMS_SITE** do site de destino.  

 Por padrão, o remetente grava dados em um site de destino, utilizando vários **envios simultâneos**, geralmente referidos como thread. Cada envio simultâneo, ou thread, pode transferir um objeto diferente com base em arquivo para o site de destino. Por padrão, quando o remetente começa a enviar um objeto, continua a gravar blocos de dados para esse objeto até que todo o objeto seja enviado. Depois que todos os dados do objeto foram enviados, um novo objeto pode começar a ser enviado nesse segmento.  

 É possível definir as seguintes configurações para um remetente:  

-   **Máximo de envios simultâneos**: Por padrão, cada site é configurado para usar cinco **envios simultâneos**, com três disponíveis para uso quando são enviados dados para qualquer site de destino. Quando você aumenta esse número, pode aumentar a taxa de transferência de dados entre os sites, permitindo que o Configuration Manager transfira mais arquivos ao mesmo tempo. O aumento desse número também aumenta a demanda de largura de banda de rede entre os sites.  

-   **Configurações de repetição**: Por padrão, cada site é configurado para repetir um problema de conexão duas vezes com um atraso de um minuto entre as tentativas de conexão. Você pode modificar o número de tentativas de conexão que o site faz, e o tempo de espera entre as tentativas.  

Para gerenciar o remetente de um site, expanda o nó **Configuração do Site** no espaço de trabalho **Administração** , selecione o nó **Sites** e clique em **Propriedades** para o site que você quer gerenciar. Clique na guia **Remetente** para alterar a configuração do remetente.  

##  <a name="a-namebkmkdbrepa-database-replication"></a><a name="bkmk_dbrep"></a> Database replication  
A replicação de banco de dados do Configuration Manager usa o SQL Server para transferir dados e mesclar as alterações feitas em um banco de dados do site com as informações armazenadas no banco de dados em outros sites na hierarquia.  

-   Isso permite que todos os sites compartilhem as mesmas informações  

-   Quando você instala um site em uma hierarquia, a replicação de banco de dados configura automaticamente entre o novo site e seu site pai designado  

-   Quando termina a instalação do site, a replicação de banco de dados é iniciada automaticamente  

Quando você adiciona um novo site a uma hierarquia, o Configuration Manager cria um banco de dados genérico no novo site. Em seguida, o site pai cria um instantâneo dos dados relevantes em seu banco de dados e transfere esse instantâneo para o novo site com uma replicação baseada em arquivo. O novo site usa um BCP (programa de cópia em massa) do SQL Server para carregar as informações em sua cópia local do banco de dados do Configuration Manager. Depois que o instantâneo é carregado, cada site realiza replicação de banco de dados com o outro site.  

Para replicar dados entre sites, o Configuration Manager usa seu próprio serviço de replicação de banco de dados. O serviço de replicação de banco de dados usa o controle de alterações do SQL Server para monitorar o banco de dados do site local quanto a alterações e, depois, replica essas alterações em outros sites, usando um **SQL Server Service Broker**. Por padrão, esse processo usa a **porta TCP/IP 4022**.  

O Configuration Manager agrupa os dados que replica pela replicação de banco de dados em grupos de replicação diferentes.  

-   Cada grupo de replicação tem uma agenda de replicação fixa, separada, que determina com que frequência as alterações de dados do grupo são replicadas em outros sites.  

     Por exemplo, uma alteração de configuração em uma configuração de administração baseada em função é replicada rapidamente em outros sites para assegurar que essas alterações sejam aplicadas o mais cedo possível. Enquanto isso, uma alteração de configuração de menor prioridade, como uma solicitação para instalar um novo site secundário, replica com menos urgência e leva vários minutos para que a solicitação do novo site alcance o site primário de destino  

-   Você pode modificar as seguintes informações da replicação de banco de dados:  

    -   **links de replicação de banco de dados** permitem controlar quando um tráfego específico atravessa a rede.  

    -   As**exibições distribuídas** são configurações para links de replicação que permitem que as solicitações feitas em um site de administração central para dados de sites selecionados acessem esses dados diretamente do banco de dados em um site primário filho.  

    -   Os**agendamentos** permitem configurar quando um link de replicação é usado e especificar quando os diferentes tipos de dados do site são replicados.  

    -   O**resumo** dos dados sobre o tráfego de rede que atravessa os links de replicação ocorre a cada 15 minutos, por padrão, e é usado em relatórios de replicação de banco de dados.  

    -   Os**limites de replicação de banco de dados** definem quando os links são relatados como degradados ou com falha. Você também pode configurar quando o Configuration Manager emite alertas sobre links de replicação com status degradado ou com falha.  

O Configuration Manager classifica os dados replicados por replicação do banco de dados como dados globais ou do site. Quando a replicação do banco de dados ocorre, alterações em dados globais e dados do site são transferidas pelo link de replicação de banco de dados. Dados globais podem replicar para o site pai ou filho, e o site replica apenas para um site pai. Um terceiro tipo de dados, chamado de dados locais, não são replicados em outros sites. Dados locais incluem informações desnecessárias aos outros sites:  

-   **Dados globais**: Dados globais referem-se a objetos criados pelo administrador que são replicados em todos os sites, em toda a hierarquia, embora sites secundários recebam apenas um subconjunto dos dados globais, como dados de proxy global. Exemplos de dados globais incluem implantações e atualizações de software, definições de coleção e escopos de segurança de administração baseada em funções. Os administradores podem criar dados globais em sites de administração central e primários.  

-   **Dados de site**: os dados de site referem-se a informações operacionais criadas pelos sites primários do Configuration Manager e pelos clientes que relatam aos sites primários. Os dados do site replicam para o site de administração central, mas não para outros sites primários. Dados de inventário de hardware, mensagens de status, alertas e resultados de coleções baseadas em consulta são exemplos de dados do site. Os dados de site são visíveis somente no site de administração central e no site primário de onde os dados são originários. Dados do site podem ser modificados apenas no site primário em que foram criados.  

     Todos os dados do site replicam no site da administração central, por isso o site de administração central pode realizar administração e relatórios para toda a hierarquia.  

As seções a seguir detalham as configurações que você pode fazer para gerenciar a replicação de banco de dados  

###  <a name="a-namebkmkdblinksa-database-replication-links"></a><a name="bkmk_Dblinks"></a> links de replicação de banco de dados  
Quando você instala um novo site em uma hierarquia, o Configuration Manager cria um link de replicação de banco de dados entre os dois sites. É criado um link único para conectar o novo site ao site pai.  

Cada link de replicação de banco de dados dá suporte a configurações para ajudar a controlar a transferência de dados pelo link de replicação. Cada link de replicação oferece suporte a configurações separadas. Os controles de links de replicação de banco de dados incluem o seguinte:  

-   Usar visões distribuídas para parar a replicação de dados de sites selecionados por meio de um site primário para o site de administração central, e permitir que o site de administração central acesse diretamente esses dados por meio do banco de dados do site primário.  

-   Agendar quando os dados de sites selecionados são transferidos de um site primário filho para o site de administração central.  

-   Definir as configurações que determinam quando um link de replicação de banco de dados está em um estado degradado ou falhou.  

-   Configurar quando gerar alertas para um link de replicação com falha.  

-   Especifique com que frequência o Configuration Manager resume dados sobre o tráfego de replicação que utiliza o link de replicação. Esses dados são usados em relatórios.  

Para configurar um link de replicação de banco de dados, edite as propriedades do link no console do Configuration Manager no nó **Replicação de banco de dados**. Esse nó aparece no espaço de trabalho **Monitoramento** e sob o nó **Configuração da Hierarquia** no espaço de trabalho **Administração** . Você pode editar um link de replicação do pai site ou do site filho do link de replicação.  

> [!TIP]  
>  Você pode editar links de replicação de banco de dados no nó **Replicação do Banco de Dados** em qualquer um dos espaços de trabalho. No entanto, quando você usa o nó **Replicação do Banco de Dados** no espaço de trabalho **Monitoramento** também pode ver o status de replicação de banco de dados dos links de replicação e acessar a ferramenta Replication Link Analyzer para ajudar a investigar problemas com a replicação.  

Para obter informações sobre como configurar os links de replicação, consulte [Controles de replicação de banco de dados do site](#BKMK_DBRepControls). Para obter mais informações sobre como monitorar a replicação, consulte a seção [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) no tópico [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) .  

Use as informações nas seções a seguir para planejar links de replicação de banco de dados.  

###  <a name="a-namebkmkdistviewsa-distributed-views"></a><a name="bkmk_distviews"></a> exibições distribuídas  
Exibições distribuídas habilitam solicitações feitas em um site de administração central para dados de site selecionados, para acessar esses dados diretamente do banco de dados em um site primário filho. Esse acesso direto substitui a necessidade de replicar os dados do site por meio do site primário para o site de administração central. Como cada link de replicação é independente de outros links de replicação, você pode habilitar exibições distribuídas apenas nos links de replicação que escolher. Não há suporte para exibições distribuídas entre um site primário e um secundário.  

Exibições distribuídas podem fornecer os seguintes benefícios:  

-   Reduzir a carga de CPU para processar alterações de banco de dados no site da administração central e sites primários.  

-   Reduzir a quantidade de dados transferidos pela rede para o site de administração central.  

-   Melhorar o desempenho do SQL Server que hospeda o banco de dados de sites de administração central.  

-   Reduzir o espaço em disco usado pelo banco de dados no site da administração central.  

Considere o uso de exibições distribuídas quando um site primário está localizado nas proximidades da rede do site de administração central, e os dois sites estão sempre ativados e sempre conectados. Isso porque exibições distribuídas substituem a replicação dos dados selecionados entre os sites com conexões diretas entre os SQL Servers em cada local. Essa conexão direta acontece cada vez que uma solicitação de dados é feita no site da administração central. Geralmente, solicitações de dados que possam ser habilitados para exibições distribuídas são feitas quando você executa relatórios ou consultas, visualiza informações no Gerenciador de Recursos e pela avaliação de coleções que incluem regras baseadas nos dados do site.  

Por padrão, visões distribuídas estão desabilitadas para cada link de replicação. Quando você habilita exibições distribuídas para um link de replicação, seleciona os dados do site que não serão replicados no site de administração central por meio daquele link e habilita o site de administração central para acessar dados diretamente do banco de dados do site primário filho que compartilha o link. Você pode configurar os seguintes tipos de dados do site para exibições distribuídas:  

-   Dados de inventário de hardware de clientes  

-   Inventário e medição de software de dados de clientes  

-   Mensagens de status de clientes, o site primário e todos os sites secundários  

Operacionalmente, exibições distribuídas são invisíveis para um usuário administrativo que visualiza os dados no console do Configuration Manager ou em relatórios. Quando é feita uma solicitação de dados habilitados para exibições distribuídas, o SQL Server que hospeda o banco de dados do site de administração central acessa diretamente o SQL Server do site primário filho para recuperar as informações. Por exemplo, você usa um console do Configuration Manager no site de administração central para solicitar informações sobre o inventário de hardware por meio de dois sites, e apenas um site tem inventário de hardware habilitado para uma exibição distribuída. As informações de inventário para clientes daquele site que não estão configuradas para exibições distribuídas são recuperadas do banco de dados no site de administração central. As informações de inventário para clientes do site que não estão configuradas para exibições distribuídas são acessadas por meio do banco de dados no site primário filho. Essas informações aparecem no console ou relatório do Configuration Manager sem distinção da origem.  

Enquanto um link de replicação tiver um tipo de dados habilitado para exibições distribuídas, o site primário filho não replicará os dados no site de administração central. Assim que você desativa as exibições distribuídas de um tipo de dados, o site primário filho retoma a replicação desses dados no site de administração central como parte da replicação de dados normal. No entanto, para que esses dados estejam disponíveis no site de administração central, os grupos de replicação que os contêm devem reinicializar entre o site primário e o site de administração central. Da mesma forma, depois de desinstalar um site primário com visões distribuídas habilitadas, o site de administração central deve completar a reinicialização dos seus dados para acessar dados habilitados para visões distribuídas no site de administração central.  

> [!IMPORTANT]  
>  Quando você usa exibições distribuídas em qualquer link de replicação na hierarquia, deve desabilitar exibições distribuídas para todos os links de replicação para desinstalar qualquer site primário. Para obter mais informações, consulte [Uninstall a primary site that is configured with distributed views](../../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#BKMK_UninstallPrimaryDistViews).  

**Pré-requisitos e limitações para exibições distribuídas:**  

-   Exibições distribuídas têm suporte apenas no links de replicação entre um site de administração central e um site primário.  

-  O site de administração central deve usar uma edição Enterprise do SQL Server. O site primário não tem esse requisito.

-   O site de administração central pode ter apenas uma instância do Provedor de SMS instalado, e essa instância deve ser instalada no servidor de banco de dados do site. Isso é necessário para dar suporte à autenticação Kerberos necessária para habilitar o SQL Server no site de administração central para acessar o SQL Server no site primário filho. Não há limitações de Provedor de SMS no site primário filho.  

-   O site de administração central pode ter apenas um ponto do SQL Server Reporting Services instalado, e deve estar localizado no servidor de banco de dados do site. Isso é necessário para dar suporte à autenticação Kerberos necessária para habilitar o SQL Server no site de administração central para acessar o SQL Server no site primário filho.  

-   O banco de dados do site não pode ser hospedado em um cluster do SQL Server.  

-   O banco de dados do site não pode ser hospedado em um cluster AlwaysOn do SQL Server.  

-   A conta de computador do servidor de banco de dados do site de administração central requer permissões de **Read** para o banco de dados do site primário.  

> [!IMPORTANT]  
>  Visões e agendamentos distribuídos para quando os dados puderem ser replicados são configurações mutuamente exclusivas para um vínculo de replicação de banco de dados.  

###  <a name="a-namebkmkschedulesa-schedule-transfers-of-site-data-on-database-replication-links"></a><a name="BKMK_schedules"></a> Agendar transferências de dados do site em links de replicação de banco de dados  
Para ajudá-lo a controlar a largura de banda de rede que é usada para replicar dados do site de um site primário filho para o seu site de administração central, você pode agendar o uso de um vínculo de replicação e especificar quando se dará a replicação dos diferentes tipos de dados do site. Você pode controlar quando o site primário replica as mensagens de status, inventário e dados de medição. Vínculos de replicação de banco de dados de sites secundários não oferecem suporte a agendamentos de dados do site. A transferência de dados globais não pode ser agendada.  

Quando você configurar um agendamento de vínculo de replicação de banco de dados, você pode restringir a transferência de dados do site selecionado do site primário para o site de administração central, e pode configurar diferentes horários para replicar diferentes tipos de dados do site.  

> [!IMPORTANT]  
>  Visões e agendamentos distribuídos para quando os dados puderem ser replicados são configurações mutuamente exclusivas para um vínculo de replicação de banco de dados.  

###  <a name="a-namebkmksummarizedbreplicationa-summarization-of-database-replication-traffic"></a><a name="BKMK_SummarizeDBReplication"></a> Resumo do tráfego de replicação de banco de dados  
Periodicamente, cada site resume dados de tráfego de rede que atravessam links de replicação de banco de dados que incluem o site. Esses dados resumidos são usados em relatórios para replicação de banco de dados. Ambos os sites em um vínculo de replicação resumem o tráfego de rede que atravessa o vínculo de replicação. O resumo dos dados é executado pelo SQL Server que hospeda o banco de dados do site. Após o resumo dos dados, essas informações são replicadas para outros sites como dados globais.  

Por padrão, o resumo ocorre a cada 15 minutos. Você pode modificar a frequência de resumo do tráfego de rede editando o **Intervalo de Resumo** nas propriedades do vínculo de replicação de banco de dados. A frequência do resumo afeta as informações exibidas nos relatórios sobre a replicação de banco de dados. É possível modificar esse intervalo de 5 a 60 minutos. Quando você aumenta a frequência do resumo, aumenta a carga de processamento no SQL Server em cada site no vínculo de replicação.  

###  <a name="a-namebkmkdbrepthresholdsa-database-replication-thresholds"></a><a name="BKMK_DBRepThresholds"></a> limites de replicação de banco de dados  
Limites de replicação de banco de dados definem quando o status de um vínculo de replicação de banco de dados é informado degradado ou com falha. Por padrão, um link é definido degradado quando algum grupo de replicação falha ao concluir a replicação por um período de 12 tentativas consecutivas, e definido com falha quando algum grupo de replicação não consegue replicar após 24 tentativas consecutivas.  

É possível especificar valores personalizados para ajuste quando o Configuration Manager informa que um link de replicação está degradado ou com falha. O ajuste de quando o Configuration Manager relata cada status dos seus vínculos de replicação de banco de dados pode ajudar a monitorar com precisão a integridade da replicação de banco de dados por meio dos vínculos de replicação de banco de dados.  

Como é possível que um ou alguns grupos de replicação não repliquem enquanto outros continuam a replicar com sucesso, planeje a revisão do status de replicação de um vínculo de replicação quando ele informar pela primeira vez um status degradado. Se houver atrasos recorrentes para grupos de replicação específicos e esse atraso não apresentar problema, ou onde o link de rede entre os sites tiver baixa largura de banda disponível, considere modificar os valores de repetição para os status degradado ou com falha do link. Ao aumentar o número de tentativas antes que o link seja definido degradado ou com falha, você pode eliminar falsos alertas para problemas conhecidos, permitindo o acompanhamento mais preciso do status do link.  

Você também deve considerar o intervalo de sincronização da replicação para cada grupo de replicação, para entender com que frequência a replicação do grupo ocorre. Você pode ver o **Intervalo de Sincronização** para grupos de replicação na guia **Detalhe de Replicação** de um vínculo de replicação no nó **Replicação do Banco de Dados** no espaço de trabalho **Monitoramento** .  

Para obter mais informações sobre como monitorar a replicação de banco de dados, incluindo como exibir o status de replicação, consulte a seção [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) no tópico [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) .  

Para obter informações sobre como configurar os limites de replicação do banco de dados, consulte [Controles de replicação de banco de dados do site](#BKMK_DBRepControls).  

##  <a name="a-namebkmkdbrepcontrolsa-site-database-replication-controls"></a><a name="BKMK_DBRepControls"></a> Controles de replicação de banco de dados do site  
Cada banco de dados do site oferece suporte a configurações que podem auxiliar no controle da largura de banda de rede usada na replicação de banco de dados. Essas configurações aplicam-se somente ao banco de dados do site onde você define as configurações, e são sempre usadas quando o site replica quaisquer dados por replicação de banco de dados para qualquer outro site.  

Os controles de replicação para cada banco de dados do site incluem o seguinte:  

-   Alterar a porta que o Configuration Manager usa para o SQL Server Service Broker.  

-   Configurar o período de tempo de espera antes que as falhas de replicação acionem o site para reinicializar sua cópia de banco de dados do site.  

-   Configurar um banco de dados do site para compactar os dados que ele replica pela replicação de banco de dados. Os dados são compactados apenas para a transferência entre sites, e não para o armazenamento no banco de dados do site em qualquer um dos sites.  

Para configurar os controles de replicação para um banco de dados do site, é possível editar as propriedades do banco de dados do site no console do Configuration Manager do nó **Replicação de Banco de Dados**. Esse nó aparece no nó **Configuração da Hierarquia** , no espaço de trabalho **Administração** , e também é exibido no **Espaço de Trabalho de Monitoramento**. Para editar as propriedades do banco de dados do site, selecione o vínculo de replicação entre sites e depois abra **Propriedades de Banco de Dados Pai** ou **Propriedades de Banco de Dados Filho**.  

> [!TIP]  
>  Você pode configurar controles de replicação de banco de dados no nó **Replicação do Banco de Dados** em qualquer um dos espaços de trabalho. No entanto, quando você usa o nó **Replicação do Banco de Dados** no espaço de trabalho **Monitoramento** você também pode ver o status de replicação de banco de dados de um vínculo de replicação, e acessar a ferramenta Replication Link Analyzer para ajudar a investigar problemas com a replicação.  



<!--HONumber=Dec16_HO3-->


