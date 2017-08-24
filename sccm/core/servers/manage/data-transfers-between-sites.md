---
title: "Transferências de dados | Microsoft Docs"
description: "Saiba como o Configuration Manager move dados entre sites e como é possível gerenciar a transferência de dados pela rede."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
caps.latest.revision: "12"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: bf0fdc8d4b4a72760b2cfb91231378a17df01594
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="data-transfers-between-sites-in-system-center-configuration-manager"></a>Transferência de dados entre sites no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O System Center Configuration Manager usa a **replicação baseada em arquivo** e **replicação de banco de dados** para transferir diferentes tipos de informações entre sites. Saiba como o Configuration Manager move dados entre sites e como é possível gerenciar a transferência de dados pela rede.  


## <a name="bkmk_fileroute"></a> File-based replication  
O Configuration Manager usa a replicação baseada em arquivo para transferir dados baseados em arquivo entre sites em sua hierarquia. Esses dados incluem aplicativos e pacotes que você deseja implantar em pontos de distribuição em sites filho e os registros de dados de descoberta não processados que são transferidos para sites pai e, então, processados.  

A comunicação baseada em arquivo entre sites usa o protocolo **SMB** na porta TCP/IP 445. É possível especificar a limitação da largura de banda e o modo de pulso para controlar a quantidade de dados transferidos pela rede e é possível usar agendamentos para controlar quando enviar os dados pela rede.  

### <a name="bkmk_routes"></a> Rotas de replicação de arquivo  
As informações a seguir podem ajudar você a configurar e usar as rotas de replicação de arquivo.  

#### <a name="file-replication-route"></a>Rota de replicação de arquivo

Cada rota de replicação de arquivo identifica um site de destino para o qual os dados baseados em arquivo podem ser transferidos. Cada site dá suporte a uma rota de replicação de arquivo para um site de destino específico.  

Você pode alterar as seguintes configurações para rotas de replicação de arquivo:  

-  **Conta de replicação de arquivo**. Essa conta se conectar ao site de destino e grava dados no compartilhamento **SMS_Site** desse site. Os dados gravados nesse compartilhamento são processados pelo site de recebimento. Por padrão, quando um site é adicionado à hierarquia, o Configuration Manager atribui a conta do computador dos novos servidores do sistema de sites como os sites Conta de Replicação de Arquivo. Esta conta é adicionada ao grupo **SMS_SiteToSiteConnection_&lt;Sitecode\>** do site de destino, um grupo local no computador que concede acesso ao compartilhamento do SMS_Site. Você pode alterar essa conta para ser uma conta de usuário do Windows. Se você alterar a conta, certifique-se de adicionar a nova conta ao grupo **SMS_SiteToSiteConnection_&lt;Sitecode\>** do site de destino.  

    > [!NOTE]  
    >  Os sites secundários sempre usam a conta do computador do servidor do site secundário como a **Conta de Replicação de Arquivo**.  

-  **Agendamento**. Você pode configurar o agendamento para cada rota de replicação de arquivo para restringir o tipo de dado e a hora em que os dados podem ser transferidos para o site de destino.  
-  **Limites de taxa**. Você pode especificar os limites de taxa para cada rota de replicação de arquivo para controlar a largura de banda da rede usada quando o site transfere os dados ao site de destino:  

    -  Use o **Modo de pulso** para especificar o tamanho dos blocos de dados que são enviados ao site de destino. Você também pode especificar um retardo de tempo entre o envio de cada bloco de dados. Use essa opção quando você deve enviar dados através de uma conexão de rede com largura de banda bem baixa ao site de destino. Por exemplo, você pode ter restrições para enviar 1 KB de dados a cada cinco segundos, mas não 1 KB a cada três segundos, independentemente da velocidade do link ou seu uso em um determinado tempo.
    -  Use **Limitado às taxas de transferência máximas especificadas por hora** para que um site envie dados para o site de destino usando somente a porcentagem de tempo que você especificar. Ao usar essa opção, o Configuration Manager não identifica a largura de banda disponível da rede, mas, em vez disso, ele divide o tempo em que pode enviar dados em períodos de tempo. Os dados são enviados em um curto bloco de tempo, que é seguido por blocos de tempo quando os dados não são enviados. Por exemplo, se a taxa máxima está definida como **50%**, o Configuration Manager transmite dados por um período de tempo seguido de igual período quando nenhum dado é enviado. A quantidade de tamanho real de dados ou o tamanho do bloco de dados não é gerenciado. Em vez disso, somente a quantidade de tempo durante a qual os dados são enviados é gerenciada.  

        > [!CAUTION]  
        > Por padrão, um site pode usar até três **envios simultâneos** para transferir dados a um site de destino. Ao habilitar limites de taxa a uma rota de replicação de arquivo, os **envios simultâneos** para envio de dados para aquele site são limitados a um. Isso se aplica mesmo se o **Limite da largura de banda disponível (%)** está definido como **100%**. Por exemplo, se você usa as configurações padrão para o remetente, isso reduz a taxa de transferência para o site de destino para um terço da capacidade padrão.  

-  Você pode configurar uma rota de replicação de arquivo entre dois sites secundários para o conteúdo baseado em arquivo de rota entre esses sites.  

Para gerenciar uma rota de replicação de arquivo, no espaço de trabalho **Administração**, expanda o nó **Configuração da Hierarquia** e selecione **Replicação de Arquivo**.  

#### <a name="sender"></a>Remetente

Cada site tem um remetente. O remetente gerencia a conexão de rede de um site para um site de destino, e pode estabelecer conexões com vários sites ao mesmo tempo. Para conectar a um site, o remetente usa a rota de replicação de arquivos até o site para identificar a conta a ser usada para estabelecer a conexão de rede. O remetente também usa essa conta para gravar dados no compartilhamento SMS_Site do site de destino.  

Por padrão, o remetente grava dados em um site de destino, utilizando vários **envios simultâneos**, geralmente referidos como thread. Cada envio simultâneo, ou thread, pode transferir um objeto diferente com base em arquivo para o site de destino. Por padrão, quando o remetente começa a enviar um objeto, continua a gravar blocos de dados para esse objeto até que todo o objeto seja enviado. Depois que todos os dados do objeto foram enviados, um novo objeto pode começar a ser enviado nesse segmento.  

É possível alterar as seguintes configurações para um remetente:  

-  **Máximo de envios simultâneos**. Por padrão, cada site usa cinco envios simultâneos, com três disponíveis para uso quando são enviados dados para qualquer site de destino. Quando você aumenta esse número, pode aumentar a taxa de transferência de dados entre os sites, pois o Configuration Manager pode transferir mais arquivos ao mesmo tempo. O aumento desse número também aumenta a demanda de largura de banda de rede entre os sites.  

-  **Configurações de repetição**. Por padrão, cada site repete um problema de conexão duas vezes com um atraso de um minuto entre as tentativas de conexão. Você pode modificar o número de tentativas de conexão que o site faz e o tempo de espera entre as tentativas.  

Para gerenciar o remetente de um site, no espaço de trabalho **Administração**, expanda o nó **Configuração do Site**, selecione o nó **Sites** e selecione **Propriedades** para o site que deseja gerenciar. Selecione a guia **Remetente** para alterar as configurações de remetente.  

## <a name="bkmk_dbrep"></a> Database replication  
A replicação de banco de dados do Configuration Manager usa o SQL Server para transferir dados e mesclar as alterações feitas em um banco de dados do site com as informações armazenadas no banco de dados em outros sites na hierarquia. Observe o seguinte sobre a replicação de banco de dados:

-  Todos os sites compartilham as mesmas informações.  
-  Quando você instala um site em uma hierarquia, a replicação de banco de dados é estabelecida automaticamente entre o novo site e seu site pai designado.  
-  Quando termina a instalação do site, a replicação de banco de dados é iniciada automaticamente.  

Quando você adiciona um novo site a uma hierarquia, o Configuration Manager cria um banco de dados genérico no novo site. Em seguida, o site pai cria um instantâneo dos dados relevantes em seu banco de dados e, em seguida, transfere o instantâneo para o novo site com uma replicação baseada em arquivo. O novo site usa um BCP (Programa de Cópia em Massa) do SQL Server para carregar as informações em sua cópia local do banco de dados do Configuration Manager. Depois que o instantâneo é carregado, cada site realiza replicação de banco de dados com o outro site.  

Para replicar dados entre sites, o Configuration Manager usa seu próprio serviço de replicação de banco de dados. O serviço de replicação de banco de dados usa o controle de alterações do SQL Server para monitorar o banco de dados do site local quanto a alterações e, depois, replica essas alterações em outros sites, usando um SQL SSB (Server Service Broker). Por padrão, esse processo usa a porta TCP/IP 4022.  

O Configuration Manager agrupa os dados que replica pela replicação de banco de dados em grupos de replicação diferentes. Observe o seguinte sobre grupos de replicação:

-  Cada grupo de replicação tem uma agenda de replicação fixa, separada, que determina com que frequência as alterações de dados do grupo são replicadas em outros sites.  

     Por exemplo, uma alteração em uma configuração de administração baseada em função é replicada rapidamente em outros sites para assegurar que essas alterações sejam aplicadas o mais cedo possível. Enquanto isso, uma alteração de configuração de prioridade mais baixa, como uma solicitação para instalar um novo site secundário, é replicada com menos urgência. Pode levar vários minutos para que uma solicitação do novo site chegue ao site primário de destino.  

-   Você pode modificar as seguintes configurações da replicação de banco de dados:  

    -  **Links de replicação de banco de dados**. Controle quando o tráfego específico percorre a rede.  
    -  **Exibições distribuídas**. Altere as configurações para os links de replicação pelos quais as solicitações feitas em um site de administração central para os dados do site selecionado podem acessar os dados desse site diretamente do banco de dados no site primário filho.  
    -  **Agendas**. Especifique quando um link de replicação é usado e quando os diferentes tipos de dados do site são replicados.  
    -  **Resumo**. Altere as configurações de resumo de dados sobre o tráfico de rede que percorre os links de replicação. O resumo ocorre a cada 15 minutos, por padrão, e é usado em relatórios para replicação de banco de dados.  
    -  **Limites de replicação de banco de dados**. Defina quando os links são relatados como degradados ou com falha. Você também pode configurar quando o Configuration Manager emite alertas sobre links de replicação degradados ou com falha.  

O Configuration Manager classifica os dados replicados por replicação do banco de dados como **dados globais** ou **dados do site**. Quando a replicação do banco de dados ocorre, alterações em dados globais e dados do site são transferidas pelo link de replicação de banco de dados. Os dados globais podem replicar em um site pai ou filho. Os dados do site replicam apenas para um site pai. Um terceiro tipo de dados, dados locais, não são replicados em outros sites. Dados locais são informações não exigidas pelos outros sites. Observe o seguinte sobre os tipos de dados:  

-  **Dados globais**. Dados globais referem-se a objetos criados pelo administrador que são replicados em todos os sites, em toda a hierarquia, embora sites secundários recebam apenas um subconjunto dos dados globais, como dados de proxy global. Os dados globais incluem implantações e atualizações de software, definições de coleção e escopos de segurança de administração baseada em funções. Os administradores podem criar dados globais em sites de administração central e primários.  
-  **Dados do site**. Os dados de site referem-se a informações operacionais criadas pelos sites primários do Configuration Manager e pelos clientes que relatam aos sites primários. Os dados do site replicam para o site de administração central, mas não para outros sites primários. Os dados do site abrangem dados de inventário de hardware, mensagens de estado, alertas e resultados de coleções com base em consulta. Os dados de site são visíveis somente no site de administração central e no site primário do qual os dados são originários. Dados do site podem ser modificados apenas no site primário em que foram criados.  

     Todos os dados do site replicam para o site de administração central. O site de administração central executa a administração e relatórios para a hierarquia do site todo.  

As seções a seguir detalham as configurações que você pode alterar para gerenciar a replicação de banco de dados.  

### <a name="bkmk_Dblinks"></a> links de replicação de banco de dados  
Quando você instala um novo site em uma hierarquia, o Configuration Manager cria um link de replicação de banco de dados entre o site pai e o novo site. É criado um link único para conectar os dois sites.  

Você pode alterar as configurações para cada link de replicação de banco de dados para ajudá-lo a controlar a transferência de dados pelo link de replicação. Cada link de replicação oferece suporte a configurações separadas. Os controles de links de replicação de banco de dados incluem o seguinte:  

-  Parar a replicação de dados de sites selecionados por meio de um site primário para o site de administração central, portanto o site de administração central pode acessar esses dados diretamente do banco de dados do site primário.  
-  Agendar os dados de sites selecionados para transferir de um site primário filho para o site de administração central.
-  Definir as configurações que determinam quando um link de replicação de banco de dados tem um estado degradado ou com falha.
-  Especificar quando gerar alertas para um link de replicação com falha.
-  Especifique com que frequência o Configuration Manager resume dados sobre o tráfego de replicação que utiliza o link de replicação. Esses dados são usados em relatórios.

Para configurar um link de replicação de banco de dados, no console do Configuration Manager, no nó **Replicação de Banco de Dados**, edite as propriedades do link. Esse nó aparece no espaço de trabalho **Monitoramento** e no espaço de trabalho **Administração**, no nó **Configuração da Hierarquia**. Você pode editar um link de replicação do pai site ou do site filho do link de replicação.  

> [!TIP]  
> Você pode editar links de replicação de banco de dados no nó **Replicação do Banco de Dados** em qualquer um dos espaços de trabalho. No entanto, quando você usa o nó **Replicação do Banco de Dados** no espaço de trabalho **Monitoramento** também pode exibir o status de replicação de banco de dados dos links de replicação e acessar a ferramenta Replication Link Analyzer para ajudar a investigar problemas com a replicação.  

Para obter informações sobre como configurar os links de replicação, consulte [Controles de replicação de banco de dados do site](#BKMK_DBRepControls). Para obter mais informações sobre como monitorar a replicação, consulte a [Como monitorar o status de replicação e links de replicação de banco de dados](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) no tópico [Monitorar a infraestrutura de hierarquia e de replicação no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

Use as informações nas seções a seguir para ajudá-lo a planejar links de replicação de banco de dados.  

### <a name="bkmk_distviews"></a> exibições distribuídas  
Por meio das exibições distribuídas, as solicitações feitas em um site de administração central para acesso a dados de site selecionados acessam esses dados diretamente do banco de dados em um site primário filho. O acesso direto substitui a necessidade de replicar os dados do site por meio do site primário para o site de administração central. Como cada link de replicação é independente de outros links de replicação, você pode usar exibições distribuídas apenas nos links de replicação que escolher. Não é possível usar exibições distribuídas entre um site primário e um secundário.  

Exibições distribuídas podem fornecer os seguintes benefícios:  

-  Reduzir a carga de CPU para processar alterações de banco de dados no site da administração central e sites primários
-  Reduzir a quantidade de dados transferidos pela rede para o site de administração central
-  Melhorar o desempenho do SQL Server que hospeda o banco de dados de sites de administração central
-  Reduzir o espaço em disco usado pelo banco de dados no site da administração central

Considere o uso de exibições distribuídas quando um site primário está nas proximidades do site de administração central na rede e os dois sites estão sempre ativados e sempre conectados. Isso porque exibições distribuídas substituem a replicação dos dados selecionados entre os sites com conexões diretas entre os SQL Servers em cada local. Uma conexão direta acontece cada vez que uma solicitação de dados é feita no site da administração central. Geralmente, solicitações de dados que possam ser habilitadas para exibições distribuídas são feitas quando você executa relatórios ou consultas, visualiza informações no Gerenciador de Recursos e pela avaliação de coleções que incluem regras baseadas nos dados do site.  

Por padrão, as exibições distribuídas estão desligadas para cada link de replicação. Quando você ativa as exibições distribuídas de um link de replicação, seleciona os dados de site que não serão replicadas para o site de administração central por meio desse link. O site de administração central acessa esses dados diretamente do banco de dados do site primário filho que compartilha o link. Você pode configurar os seguintes tipos de dados do site para exibições distribuídas:  

-  Dados de inventário de hardware de clientes
-  Inventário e medição de software de dados de clientes
-  Mensagens de status de clientes, o site primário e todos os sites secundários

Operacionalmente, exibições distribuídas são invisíveis para um usuário administrativo que visualiza os dados no console do Configuration Manager ou em relatórios. Quando é feita uma solicitação de dados habilitados para exibições distribuídas, o SQL Server que hospeda o banco de dados do site de administração central acessa diretamente o SQL Server do site primário filho para recuperar as informações. Por exemplo, você usa um console do Configuration Manager no site de administração central para solicitar informações sobre o inventário de hardware por meio de dois sites, e apenas um site tem inventário de hardware habilitado para uma exibição distribuída. As informações de inventário para clientes daquele site que não estão configuradas para exibições distribuídas são recuperadas do banco de dados no site de administração central. As informações de inventário para clientes do site que estão configuradas para exibições distribuídas são acessadas por meio do banco de dados no site primário filho. Essas informações aparecem no console do Configuration Manager ou em um relatório sem identificar a origem.  

Enquanto um link de replicação tiver um tipo de dados habilitado para exibições distribuídas, o site primário filho não replicará os dados no site de administração central. Assim que você desliga as exibições distribuídas de um tipo de dados, o site primário filho retoma a replicação desses dados no site de administração central como parte da replicação de dados normal. No entanto, para que esses dados estejam disponíveis no site de administração central, os grupos de replicação que os têm devem reinicializar entre o site primário e o site de administração central. Da mesma forma, depois de desinstalar um site primário com visões distribuídas ativadas, o site de administração central deve completar a reinicialização dos seus dados para acessar dados habilitados para visões distribuídas no site de administração central.  

> [!IMPORTANT]  
> Quando você usa exibições distribuídas em qualquer link de replicação na hierarquia do site, deve desligar exibições distribuídas para todos os links de replicação para desinstalar qualquer site primário. Para obter mais informações, consulte [Uninstall a primary site that is configured with distributed views](../../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#BKMK_UninstallPrimaryDistViews).  

#### <a name="prerequisites-and-limitations-for-distributed-views"></a>Pré-requisitos e limitações para exibições distribuídas  

-  Você pode usar exibições distribuídas apenas nos links de replicação entre um site de administração central e um site primário.
- O site de administração central deve usar uma edição Enterprise do SQL Server. O site primário não tem esse requisito.
-  O site de administração central pode ter apenas uma instância do Provedor de SMS instalado, e essa instância deve ser instalada no servidor de banco de dados do site. Isso é necessário para dar suporte à autenticação Kerberos necessária para que o SQL Server no site de administração central possa acessar o SQL Server no site primário filho. Não há limitações de Provedor de SMS no site primário filho.
-  O site de administração central pode ter apenas um ponto do SQL Server Reporting Services instalado, e deve estar localizado no servidor de banco de dados do site. Isso é necessário para dar suporte à autenticação Kerberos necessária para habilitar o SQL Server no site de administração central para acessar o SQL Server no site primário filho.
-  O banco de dados do site não pode ser hospedado em um cluster do SQL Server.
-  O banco de dados do site não pode ser hospedado em um grupo de disponibilidade do AlwaysOn do SQL Server.
-  A conta de computador do servidor de banco de dados do site de administração central requer permissões de Leitura para o banco de dados do site primário.

> [!IMPORTANT]  
>  Visões e agendamentos distribuídos para quando os dados puderem ser replicados são configurações mutuamente exclusivas para um vínculo de replicação de banco de dados.  

### <a name="BKMK_schedules"></a> Agendar transferências de dados do site em links de replicação de banco de dados  
Para ajudá-lo a controlar a largura de banda de rede que é usada para replicar dados do site de um site primário filho para o seu site de administração central, você pode agendar o uso de um vínculo de replicação e especificar quando se dará a replicação dos diferentes tipos de dados do site. Você pode controlar quando o site primário replica as mensagens de status, inventário e dados de medição. Vínculos de replicação de banco de dados de sites secundários não oferecem suporte a agendamentos de dados do site. A transferência de dados globais não pode ser agendada.  

Quando você configurar um agendamento de vínculo de replicação de banco de dados, você pode restringir a transferência de dados do site selecionado do site primário para o site de administração central, e pode configurar diferentes horários para replicar diferentes tipos de dados do site.  

> [!IMPORTANT]  
> Visões e agendamentos distribuídos para quando os dados puderem ser replicados são configurações mutuamente exclusivas para um vínculo de replicação de banco de dados.  

### <a name="BKMK_SummarizeDBReplication"></a> Resumo do tráfego de replicação de banco de dados  
Periodicamente, cada site resume dados de tráfego de rede que percorrem links de replicação de banco de dados para o site. Os dados resumidos são usados em relatórios para replicação de banco de dados. Ambos os sites em um vínculo de replicação resumem o tráfego de rede que atravessa o vínculo de replicação. O resumo dos dados é executado pelo SQL Server que hospeda o banco de dados do site. Após os dados serem resumidos, as informações serão replicadas para outros sites como dados globais.  

Por padrão, o resumo ocorre a cada 15 minutos. Para modificar a frequência de resumo do tráfego de rede, nas propriedades do link de replicação de banco de dados, edite o **Intervalo de resumo**. A frequência do resumo afeta as informações exibidas nos relatórios sobre a replicação de banco de dados. Você pode escolher um intervalo de entre 5 minutos e 60 minutos. Quando você aumenta a frequência do resumo, aumenta a carga de processamento no SQL Server em cada site no vínculo de replicação.  

### <a name="BKMK_DBRepThresholds"></a> Limites de replicação de banco de dados  
Limites de replicação de banco de dados definem quando o status de um vínculo de replicação de banco de dados é informado degradado ou com falha. Por padrão, um link é definido para o status degradado quando qualquer grupo de replicação falha ao concluir a replicação para um período de 12 tentativas consecutivas. O link é definido para o status com falha quando algum grupo de replicação não consegue replicar após 24 tentativas consecutivas.  

É possível especificar valores personalizados para ajuste quando o Configuration Manager informa que um link de replicação está degradado ou com falha. O ajuste de quando o Configuration Manager relata cada status dos seus vínculos de replicação de banco de dados pode ajudar a monitorar com precisão a integridade da replicação de banco de dados por meio dos vínculos de replicação de banco de dados.  

Como é possível que um ou alguns grupos de replicação não repliquem enquanto outros grupos de replicação continuam a replicar com êxito, planeje examinar o status de replicação de um link de replicação quando ele informar pela primeira vez um status degradado. Se houver atrasos recorrentes para grupos de replicação específicos e esse atraso não apresentar problema, ou onde o link de rede entre os sites tiver baixa largura de banda disponível, considere modificar os valores de repetição para os status degradado ou com falha do link. Ao aumentar o número de tentativas antes que o link seja definido como degradado ou com falha, você pode eliminar falsos alertas para problemas conhecidos e acompanhar o status do link de forma mais precisa.  

Além disso, considere o intervalo de sincronização da replicação para cada grupo de replicação para entender com que frequência a replicação do grupo ocorre. Para exibir o **Intervalo de Sincronização** para grupos de replicação, no espaço de trabalho **Monitoramento**, no nó **Replicação de Banco de Dados**, selecione a guia **Detalhe da Replicação** de um link de replicação.  

Para obter mais informações sobre como monitorar a replicação de banco de dados, incluindo como exibir o status da replicação, consulte a [Como monitorar o status de replicação e links de replicação de banco de dados](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) no tópico [Monitorar a infraestrutura de hierarquia e de replicação no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

Para obter informações sobre como configurar os limites de replicação do banco de dados, consulte [Controles de replicação de banco de dados do site](#BKMK_DBRepControls).  

## <a name="BKMK_DBRepControls"></a> Controles de replicação de banco de dados do site  
Você pode alterar as configurações para cada banco de dados do site para ajudá-lo a controlar a largura de banda de rede usada para replicação de banco de dados. As configurações se aplicam somente ao banco de dados do site em que você definir as configurações. As configurações são sempre usadas quando o site replica quaisquer dados por replicação de banco de dados para qualquer outro site.  

Os itens a seguir são controles de replicação que você pode modificar para cada banco de dados de site:  

-  Alterar a porta SSB.  
-  Configurar o período de tempo de espera antes que as falhas de replicação acionem o site para reinicializar sua cópia de banco de dados do site.  
-  Configurar um banco de dados do site para compactar os dados que ele replica pela replicação de banco de dados. Os dados são compactados apenas para a transferência entre sites, e não para o armazenamento no banco de dados do site em qualquer um dos sites.  

Para alterar as configurações para os controles de replicação para um banco de dados de site, no console do Configuration Manager, no nó **Replicação de Banco de Dados**, edite as propriedades do banco de dados de site. Esse nó aparece no nó **Configuração da Hierarquia** , no espaço de trabalho **Administração** , e também é exibido no **Espaço de Trabalho de Monitoramento**. Para editar as propriedades do banco de dados do site, selecione o vínculo de replicação entre sites e depois abra **Propriedades de Banco de Dados Pai** ou **Propriedades de Banco de Dados Filho**.  

> [!TIP]  
> Você pode configurar controles de replicação de banco de dados no nó **Replicação do Banco de Dados** em qualquer um dos espaços de trabalho. No entanto, quando você usa o nó **Replicação do Banco de Dados** no espaço de trabalho **Monitoramento** você também pode exibir o status de replicação de banco de dados de um vínculo de replicação e acessar a ferramenta Replication Link Analyzer para ajudar a investigar problemas com a replicação.  
