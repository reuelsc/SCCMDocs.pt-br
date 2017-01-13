---
title: Configurar a descoberta | Microsoft Docs
description: "Configure métodos de descoberta para serem executados em um site do Configuration Manager para encontrar recursos que você pode gerenciar usando sua infraestrutura de rede e o Active Directory."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 2fcc392ba700f871349200166fac715b73788c16

---
# <a name="configure-discovery-methods-for-system-center-configuration-manager"></a>Configurar métodos de descoberta para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Configure métodos de descoberta para serem executados em um site do System Center Configuration Manager para encontrar recursos que você pode gerenciar usando sua infraestrutura de rede e o Active Directory. É necessário que você habilite e configure cada método que quiser usar para pesquisar em seu ambiente. (Também é possível desabilitar um método usando o mesmo procedimento usado para habilitá-lo.)  As únicas exceções são a Descoberta de Pulsação e a Descoberta de Servidor:  

-   Por padrão, a Descoberta de Pulsação já está habilitada quando você instala um site primário do Configuration Manager, e está configurada para ser executada segundo um cronograma básico. Mantenha a Descoberta de Pulsação habilitada, pois esse método garante que os DDRs (registros de dados de descobertas) dos dispositivos fiquem atualizados. Para obter mais informações sobre a Descoberta de Pulsação, consulte [Sobre a Descoberta de Pulsação](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat)  

-   A Descoberta de Servidor é um método de descoberta automática que localiza os computadores que você utiliza como sistemas de sites, e não é um método que você possa configurar ou desabilitar.  

**Para habilitar qualquer método de descoberta configurável:**  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** e clique em **Métodos de Descoberta**.  

2.  Selecione o método de descoberta para o site em que deseja habilitar a descoberta.  

3.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades** e, na guia **Geral**, marque a caixa de seleção **Habilitar&lt;método de descoberta\>**.  

     Se essa caixa de seleção já estiver marcada, você poderá desabilitar o método de descoberta desmarcando-a.  

4.  Clique em **OK** para salvar a configuração.  


##  <a name="a-namebkmkconfigadforestdisca-configure-active-directory-forest-discovery"></a><a name="BKMK_ConfigADForestDisc"></a> Configurar a Descoberta de Florestas do Active Directory  
 Para concluir a configuração de descoberta de florestas do Active Directory, é necessário definir as configurações em dois locais:  

-   No nó **Métodos de Descoberta** , você pode habilitar esse método de descoberta, definir um agendamento de sondagem e selecionar se a descoberta criará automaticamente limites para os sites e sub-redes do Active Directory que ela descobrir.  

-   No nó **Florestas do Active Directory**, você pode adicionar as florestas que deseja descobrir, habilitar a descoberta de sites e sub-redes do Active Directory nessa floresta, definir configurações que habilitam sites do Configuration Manager a publicar suas informações na floresta e atribuir uma conta a ser usada como a Conta da Floresta do Active Directory para cada floresta.  

 Use os procedimentos a seguir para habilitar a descoberta de florestas do Active Directory e para configurar florestas individuais a serem usadas com a descoberta de florestas do Active Directory.  

#### <a name="to-enable-active-directory-forest-discovery"></a>Para habilitar a descoberta de florestas do Active Directory  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** e clique em **Métodos de Descoberta**.  

2.  Selecione o método de descoberta de floretas do Active Directory para o site em que deseja configurar a descoberta.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Na guia **Geral** , marque a caixa de seleção para habilitar a descoberta, ou configure a descoberta agora e retorne para habilitá-la posteriormente.  

5.  Especifique opções para criar limites de site para locais descobertos.  

6.  Especifique um agendamento para quando a descoberta for executada.  

7.  Quando você concluir a configuração da descoberta de florestas do Active Directory para esse site, clique em **OK** para salvar a configuração.  

#### <a name="to-configure-a-forest-for-active-directory-forest-discovery"></a>Para configurar uma floresta para descoberta de florestas do Active Directory  

1.  No espaço de trabalho de **Administração** , clique em **Florestas do Active Directory**. Se uma descoberta de florestas do Active Directory tiver sido executada anteriormente, você verá cada floresta descoberta no painel de resultados. A floresta local e quaisquer florestas confiáveis são detectadas quando a descoberta de florestas do Active Directory é executada. Somente as florestas não confiáveis devem ser adicionadas manualmente.  

    -   Para configurar uma floresta descoberta anteriormente, selecione-a no painel de resultados e na guia **Início** , no grupo **Propriedades** , clique em **Propriedades** para abrir as propriedades da floresta. Continue na etapa 3.  

    -   Para configurar uma nova floresta que não esteja listada: na guia **Início** , no grupo **Criar** , clique em **Adicionar Floresta** para abrir a caixa de diálogo **Adicionar Floresta** . Continue na etapa 3.  

2.  Na guia **Geral** , complete as configurações da floresta que você deseja descobrir e especifique a **Conta da Floresta do Active Directory**.  

    > [!NOTE]  
    >  A descoberta de florestas do Active Directory requer uma conta global para descobrir e publicar em florestas não confiáveis. Se você não usar a conta de computador do servidor do site, será possível selecionar somente uma conta global.  

3.  Se você pretende permitir que os sites publiquem dados nessa floresta, na guia **Publicação** conclua as configurações para que seja possível fazer publicações nessa floresta.  

    > [!NOTE]  
    >  Se você permitir que sites publiquem em uma floresta, será necessário estender o esquema do Active Directory dessa floresta para o Configuration Manager, e a Conta da Floresta do Active Directory deverá ter permissões de controle total no contêiner de Sistema dessa floresta.  

4.  Ao concluir a configuração da floresta a ser usada com a descoberta de florestas do Active Directory, clique em **OK** para salvá-la.  

##  <a name="a-namebkmkconfigaddiscgenerala-configure-active-directory-discovery-for-computers-users-or-groups"></a><a name="BKMK_ConfigADDiscGeneral"></a> Configurar a descoberta do Active Directory para computadores, usuários ou grupos  
 Use as informações das seções a seguir para configurar a descoberta de computadores, usuários ou grupos usando um dos seguintes métodos de descoberta:  

-   Descoberta de grupos do Active Directory  

-   Descoberta de sistemas do Active Directory  

-   Descoberta de Usuário do Active Directory  

> [!NOTE]  
>  As informações nesta seção não se aplicam à descoberta de florestas do Active Directory.  

 Embora cada um desses métodos de descoberta seja independente dos outros, eles compartilham opções semelhantes. Para obter mais informações sobre essas opções de configuração, consulte [Shared options for Group, System, and User discovery](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_shared) (Opções compartilhadas para a descoberta de grupo, sistema e usuário).  

> [!WARNING]  
>  A sondagem do Active Directory por cada um desses métodos de descoberta pode gerar tráfego de rede significativo. Considere agendar cada um dos métodos de descoberta para que eles sejam executados um de cada vez, quando esse tráfego de rede não afetar de forma adversa os usos corporativos da sua rede.  

#### <a name="to-configure-active-directory-group-discovery"></a>Para configurar a descoberta de grupos do Active Directory  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** e clique em **Métodos de Descoberta**.  

2.  Selecione o método **Descoberta de grupos do Active Directory** para o site em que deseja configurar a descoberta.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Na guia **Geral** , marque a caixa de seleção para habilitar a descoberta, ou configure a descoberta agora e retorne para habilitá-la posteriormente.  

5.  Clique em **Adicionar** para configurar um escopo de descoberta, selecione **Grupos** ou **Local**e conclua as configurações a seguir na caixa de diálogo **Adicionar Grupos**ou **Adicionar Local do Active Directory** :  

    1.  Especifique um **nome** para esse escopo de descoberta.  

    2.  Especifique um **Domínio do Active Directory** ou **Local** para pesquisa:  

        -   Se você tiver selecionado **Grupos**, especifique um ou mais grupos do Active Directory para descoberta.  

        -   Se você tiver selecionado **Local**, especifique um contêiner do Active Directory como um local a ser descoberto. Você também pode habilitar uma pesquisa recursiva de contêineres filho do Active Directory para esse local.  

    3.  Especifique a **Conta de descoberta de grupos do Active Directory** usada para pesquisar esse escopo de descoberta.  

    4.  Clique em **OK** para salvar a configuração do escopo de descoberta.  

6.  Repita a etapa 6 para cada escopo de descoberta adicional que desejar definir.  

7.  Na guia **Agendamento de Sondagem** , configure o agendamento de sondagem de descoberta completa e a descoberta de deltas.  

8.  Opcionalmente, na guia **Opção** , você pode configurar opções para filtrar, ou excluir, registros de computadores obsoletos da descoberta e para descobrir a associação dos grupos de distribuição.  

    > [!NOTE]  
    >  Por padrão, a descoberta de grupos do Active Directory descobre apenas a associação de grupos de segurança.  

9. Quando concluir a configuração da descoberta de grupos do Active Directory para esse site, clique em **OK** para salvá-la.  

#### <a name="to-configure-active-directory-system-discovery"></a>Para configurar a descoberta de sistemas do Active Directory  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** e clique em **Métodos de Descoberta**.  

2.  Selecione o método para o site em que deseja configurar a descoberta.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Na guia **Geral** , marque a caixa de seleção para habilitar a descoberta, ou configure a descoberta agora e retorne para habilitá-la posteriormente.  

5.  Clique no ícone **Novo** ![Ícone Novo](media/Disc_new_Icon.gif) para especificar um novo contêiner do Active Directory e, na caixa de diálogo **Contêiner do Active Directory**, conclua as seguintes configurações:  

    1.  Especifique um ou mais locais para pesquisa.  

    2.  Em cada local, especifique opções que modifiquem o comportamento da pesquisa.  

    3.  Em cada local, especifique a conta a ser usada como a **Conta de descoberta do Active Directory**.  

        > [!TIP]  
        >  Em cada local especificado, você pode configurar um conjunto de opções de descoberta e uma única conta de descoberta do Active Directory.  

    4.  Clique em **OK** para salvar a configuração do contêiner do Active Directory.  

6.  Na guia Agendamento de Sondagem, configure o agendamento de sondagem de descoberta completa e a descoberta de deltas.  

7.  Opcionalmente, na guia **Atributos do Active Directory** , você pode configurar atributos adicionais do Active Directory para computadores que você deseja descobrir. Os atributos de objeto padrão também são listados.  

8.  Opcionalmente, na guia **Opção** , você pode configurar opções para filtrar, ou excluir, registros de computadores obsoletos da descoberta.  

9. Quando concluir a configuração da Descoberta de Sistemas do Active Directory para esse site, clique em **OK** para salvá-la.  

#### <a name="to-configure-active-directory-user-discovery"></a>Para configurar a descoberta de usuários do Active Directory  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** e clique em **Métodos de Descoberta**.  

2.  Selecione o método **Descoberta de usuários do Active Directory** para o site em que deseja configurar a descoberta.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Na guia **Geral** , marque a caixa de seleção para habilitar a descoberta, ou configure a descoberta agora e retorne para habilitá-la posteriormente.  

5.  Clique no ícone **Novo** ![Ícone Novo](media/Disc_new_Icon.gif) para especificar um novo contêiner do Active Directory e, na caixa de diálogo **Contêiner do Active Directory**, conclua as seguintes configurações:  

    1.  Especifique um ou mais locais para pesquisa.  

    2.  Em cada local, especifique opções que modifiquem o comportamento da pesquisa.  

    3.  Em cada local, especifique a conta a ser usada como a **Conta de descoberta do Active Directory**.  

        > [!NOTE]  
        >  Em cada local especificado, você pode configurar um único conjunto de opções de descoberta e uma única conta de descoberta do Active Directory.  

    4.  Clique em **OK** para salvar a configuração do contêiner do Active Directory.  

6.  Na guia **Agendamento de Sondagem** , configure o agendamento de sondagem de descoberta completa e a descoberta de deltas.  

7.  Opcionalmente, na guia **Atributos do Active Directory** , você pode configurar atributos adicionais do Active Directory para computadores que você deseja descobrir. Os atributos de objeto padrão também são listados.  

8.  Quando concluir a configuração da Descoberta de Usuários do Active Directory para esse site, clique em **OK** para salvá-la.  

##  <a name="a-namebkmkconfighbdisca-configure-heartbeat-discovery"></a><a name="BKMK_ConfigHBDisc"></a> Configurar a Descoberta de Pulsação  
 Por padrão, a Descoberta de Pulsação é habilitada quando você instala um site primário do Configuration Manager. Consequentemente, você precisa configurar somente o cronograma da frequência com que os clientes enviam os DDRs (registro dos dados de descoberta) da descoberta de pulsação para um ponto de gerenciamento quando não quiser que eles usem o valor padrão de 7 dias.  

> [!NOTE]  
>  Se a instalação de push de cliente e a tarefa de manutenção de site para **Limpar Sinalizador de Instalação** forem habilitadas ao mesmo tempo, defina o agendamento da descoberta de pulsação para ser menor do que o **Período de Redescoberta de Cliente** da tarefa de manutenção de site **Limpar Sinalizador de Instalação** . Para obter mais informações sobre as tarefas de manutenção de sites, consulte [Tarefas de manutenção do System Center Configuration Manager](../../../../core/servers/manage/maintenance-tasks.md).  

#### <a name="to-configure-the-heartbeat-discovery-schedule"></a>Para configurar o agendamento de descoberta de pulsação  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** e clique em **Métodos de Descoberta**  

2.  Selecione **Descoberta de Pulsação** para o site em que deseja configurar a descoberta de pulsação.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Configure a frequência com que os clientes enviam DDRs de descoberta de pulsação e clique em **OK** para salvar a configuração.  

##  <a name="a-namebkmkconfignetworkdisca-configure-network-discovery"></a><a name="BKMK_ConfigNetworkDisc"></a> Configurar a Descoberta de Rede  
 Use as informações contidas nas seções a seguir para ajudá-lo a configurar a descoberta de rede.  

###  <a name="a-namebkmkaboutconfignetworkdisca-about-configuring-network-discovery"></a><a name="BKMK_AboutConfigNetworkDisc"></a> Sobre a configuração de Descoberta de Rede  
 Antes de configurar a descoberta de rede, é necessário saber o seguinte:  

-   Níveis disponíveis de descoberta de rede  

-   Opções de descoberta de rede disponíveis  

-   Limitação de descoberta de rede na rede  

Para obter mais informações, consulte a seção [Sobre a Descoberta de Rede](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutNetwork).  

 As seções a seguir fornecem informações sobre configurações comuns de descoberta de rede. Você pode configurar uma ou mais dessas configurações para uso durante a execução da mesma descoberta. Se você usar várias configurações, será necessário planejar as interações que possam afetar os resultados da descoberta.  

 Por exemplo, talvez você queira descobrir todos os dispositivos SNMP que usam um nome de comunidade SNMP específico. Além disso, para a execução da mesma descoberta, você poderá desabilitar a descoberta em uma sub-rede específica. Quando a descoberta for executada, a descoberta de rede não descobrirá dispositivos SNMP com o nome de comunidade especificado na sub-rede desabilitada.  

####  <a name="a-namebkmkdeterminenettopologya-determine-your-network-topology"></a><a name="BKMK_DetermineNetTopology"></a> Determinar a topologia de rede  
 Você pode usar uma descoberta somente de topologia para mapear sua rede. Esse tipo de descoberta não descobre clientes potenciais. A Descoberta de Rede somente de topologia depende do SNMP.  

 Ao mapear a topologia de rede, você deve configurar o **Máximo de saltos** na guia **SNMP** na caixa de diálogo **Propriedades da Descoberta e Rede** . Apenas alguns saltos podem ajudar a controlar a largura de banda de rede é usada quando a descoberta é executada. À medida que você descobre mais sobre a rede, pode aumentar o número de saltos para ter um entendimento melhor da topologia de rede.  

 Depois de entender a topologia de rede, você poderá configurar propriedades adicionais para que a Descoberta de Rede descubra clientes potenciais e seus sistemas operacionais enquanto você está usando configurações disponíveis para limitar os segmentos de rede que a Descoberta de Rede pode pesquisar.  

####  <a name="a-namebkmklimitbysubneta-limit-searches-by-using-subnets"></a><a name="BKMK_LimitBySubnet"></a> Limitar pesquisas usando sub-redes  
 Você pode configurar a Descoberta de Rede para pesquisar sub-redes específicas durante uma descoberta. Por padrão, a Descoberta de Rede pesquisa a sub-rede do servidor que executa a descoberta. Todas as sub-redes adicionais que você configurar e ativar aplicam-se somente às opções de pesquisa do SNMP (Simple Network Management Protocol) e do DHCP (Dynamic Host Configuration Protocol). Quando a Descoberta de Rede pesquisa domínios, ela não é limitada por configurações de sub-redes.  

 Se você especificar uma ou mais sub-redes na guia **Sub-redes** na caixa de diálogo **Propriedades da Descoberta de Rede** , somente as sub-redes marcadas como **Habilitadas** serão pesquisadas.  

 Quando você desabilita uma sub-rede, ela é excluída da descoberta e as seguintes condições são aplicáveis:  

-   Consultas baseadas em SNMP não são executadas na sub-rede  

-   Servidores DHCP não respondem com uma lista de recursos localizados na sub-rede  

-   Consultas baseadas em domínio podem descobrir recursos que estão localizados na sub-rede  

####  <a name="a-namebkmksearchbydomaina-search-a-specific-domain"></a><a name="BKMK_SearchByDomain"></a> Pesquisar um domínio específico  
 Você pode configurar uma Descoberta de Rede para pesquisar um domínio específico ou um conjunto de domínios durante uma descoberta. Por padrão, a Descoberta de Rede pesquisa o domínio do servidor que executa a descoberta.  

 Se você especificar um ou mais domínios na guia **Domínio** na caixa de diálogo **Propriedades da Descoberta de Rede** , somente os domínios marcados como **Habilitados** serão pesquisados.  

 Quando você desabilita um domínio, ele é excluído da descoberta e as seguintes condições são aplicáveis:  

-   A Descoberta de Rede não consulta controladores de domínio nesse domínio  

-   Ainda é possível executar consultas baseadas em SNMP em sub-redes no domínio  

-   Os servidores DHCP ainda podem responder com uma lista de recursos localizados no domínio  

####  <a name="a-namebkmklimitbysnmpnamea-limit-searches-by-using-snmp-community-names"></a><a name="BKMK_LimitBySNMPname"></a> Limitar pesquisas usando nomes de Comunidade SNMP  
 Configure uma Descoberta de Rede para pesquisar uma comunidade SNMP específica ou um conjunto de comunidades durante uma descoberta. Por padrão, o nome da comunidade de **pública** está configurado para uso.  

 A Descoberta de Rede usa nomes de comunidades para obter acesso aos roteadores que são dispositivos SNMP. Um roteador pode fornecer à Descoberta de Rede informações sobre outros roteadores e sub-redes que estejam vinculados ao primeiro roteador.  

> [!NOTE]  
>  Os nomes de comunidades SNMP se parecem com senhas. A Descoberta de Rede pode obter informações somente de um dispositivo SNMP para o qual você especificou um nome de comunidade. Cada dispositivo SNMP pode ter seu próprio nome de comunidade, mas, geralmente, o mesmo nome de comunidade é compartilhado entre vários dispositivos. Além disso, a maioria dos dispositivos SNMP têm um nome de comunidade padrão de **pública**. No entanto, algumas organizações excluem o nome da comunidade **pública** de seus dispositivos como uma precaução de segurança.  

 Se várias comunidades SNMP são exibidas na guia **SNMP** na caixa de diálogo **Propriedades da Descoberta de Rede** , a Descoberta de Rede pesquisa essas comunidades na ordem em que elas são exibidas. Para ajudar a minimizar o tráfego de rede gerado pelas tentativas de contatar um dispositivo usando nomes diferentes, verifique se os nomes usados com mais frequência estão no topo da lista.  

> [!NOTE]  
>  Além de usar o nome da Comunidade SNMP, você pode especificar o endereço IP ou o nome que pode ser resolvido de um dispositivo SNMP específico. Você pode configurar o endereço IP ou o nome que pode ser resolvido para um dispositivo específico na guia **Dispositivos SNMP** na caixa de diálogo **Propriedades da Descoberta de Rede** .  

####  <a name="a-namebkmksearchbydhcpa-search-a-specific-dhcp-server"></a><a name="BKMK_SearchByDHCP"></a> Pesquisar um servidor DHCP específico  
 Você pode configurar a Descoberta de Rede para usar um servidor SNMP específico ou vários servidores para descobrir clientes DHCP durante uma descoberta.  

 A Descoberta de Rede pesquisa cada servidor DHCP especificado na guia **DHCP** na caixa de diálogo **Propriedades da Descoberta de Rede** . Se o servidor que executa a descoberta conceder seu endereço IP de um servidor DHCP, você poderá configurar a descoberta para pesquisa esse servidor marcando a caixa de seleção **Incluir o servidor DHCP que o servidor do site está configurado para usar** .  

> [!NOTE]  
>  Para configurar um servidor DHCP com êxito na Descoberta de Rede, o ambiente deve oferecer suporte a IPv4. Não é possível configurar a Descoberta de Rede para usar um servidor DHCP em um ambiente IPv6 nativo.  

###  <a name="a-namebkmkhowtoconfignetdisca-how-to-configure-network-discovery"></a><a name="BKMK_HowToConfigNetDisc"></a> Como configurar a Descoberta de Rede  
 Use os procedimentos a seguir para descobrir primeiro somente a topologia de rede e, em seguida, configurar a Descoberta de Rede para descobrir clientes potenciais usando uma ou mais das opções disponíveis da Descoberta de Rede.  

##### <a name="to-determine-your-network-topology"></a>Para determinar a topologia de rede  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** e clique em **Métodos de Descoberta**  

2.  Selecione **Descoberta de Rede** para o site onde deseja executar a Descoberta de Rede.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

    -   Na guia **Geral** , marque a caixa de seleção **Habilitar descoberta de rede** e selecione **Topologia** nas opções **Tipo de descoberta** .  

    -   Na guia **Sub-redes** , marque a caixa de seleção **Pesquisar sub-redes locais** .  

        > [!TIP]  
        >  Caso conheça as sub-redes específicas que constituem sua rede, você pode desmarcar a caixa de seleção **Pesquisar sub-redes locais** e usar o ícone **Novo** ![Ícone Novo](media/Disc_new_Icon.gif) para adicionar as sub-redes específicas que deseja pesquisar. Para sub-redes grandes, geralmente é melhor pesquisar somente uma ou duas sub-redes por vez para minimizar o uso de largura de banda de rede.  

    -   Na guia **Domínios** , marque a caixa de seleção **Pesquisar domínios locais** .  

    -   Na guia **SNMP** , use a lista suspensa **Máximo de saltos** para especificar quantos saltos do roteador a Descoberta de Rede pode captar ao mapear sua topologia.  

        > [!TIP]  
        >  Ao mapear a topologia de rede pela primeira vez, configure poucos saltos do roteador para minimizar o uso de largura de banda de rede.  

4.  Na guia **Agendamento**, clique no ícone **Novo** ![Ícone Novo](media/Disc_new_Icon.gif) para definir um cronograma para executar a Descoberta de Rede.  

    > [!NOTE]  
    >  Não é possível atribuir uma configuração de descoberta diferente para separar agendamentos de Descoberta de Rede. Cada vez que a Descoberta de Rede é executada, ela usa a configuração de descoberta atual.  

5.  Clique em **OK** para aceitar as configurações. A Descoberta de Rede é executada no horário agendado.  

##### <a name="to-configure-network-discovery"></a>Para configurar a Descoberta de Rede  

1.  No console do Configuration Manager, clique em **Administração** > **Configuração da Hierarquia** e clique em **Métodos de Descoberta**  

2.  Selecione **Descoberta de Rede** para o site onde deseja executar a Descoberta de Rede.  

3.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Na guia **Geral** , marque a caixa de seleção **Habilitar descoberta de rede** e selecione o tipo de descoberta que deseja executar nas opções **Tipo de descoberta** .  

5.  Para configurar a descoberta para pesquisar sub-redes, clique na guia **Sub-redes** e, na guia **Sub-redes** , configure uma ou mais das seguinte opções:  

    -   Para executar a descoberta em sub-redes locais no computador que executa a descoberta, marque a caixa de seleção **Pesquisar sub-redes locais** .  

    -   Para pesquisar uma sub-rede específica, ela deve estar listada em **Sub-redes a serem pesquisadas**e ter um valor de **Pesquisa** de **Habilitado**:  

        1.  Se a sub-rede não estiver listada, clique no ícone **Novo** ![Ícone Novo](media/Disc_new_Icon.gif). Na caixa de diálogo **Nova Atribuição de Sub-rede** , insira as informações da **Sub-rede** e da **Máscara** e clique em **OK**. Por padrão, uma nova sub-rede está habilitada para pesquisa.  

        2.  Para alterar o valor de **Pesquisa** de uma sub-rede listada, selecione-a e clique no ícone **Ativar/Desativar** para alternar o valor entre **Desabilitado** e **Habilitado**.  

6.  Para configurar a descoberta para pesquisar domínios, clique na guia **Domínios** e, na guia **Domínios** , configure uma ou mais das seguinte opções:  

    -   Para executar a descoberta no domínio do computador que executa a descoberta, marque a caixa de seleção **Pesquisar domínio local** .  

    -   Para pesquisar um domínio específico, ele deve estar listado em **Domínios** e ter um valor de **Pesquisa** de **Habilitado**:  

        1.  Se o domínio não estiver listado, clique no ícone **Novo** ![Ícone Novo](media/Disc_new_Icon.gif) e, na caixa de diálogo **Propriedades do Domínio**, insira as informações do **Domínio** e clique em **OK**. Por padrão, um novo domínio está habilitado para pesquisa.  

        2.  Para alterar o valor de **Pesquisa** de um domínio listado, selecione-o e clique no ícone **Ativar/Desativar** para alternar o valor entre **Desabilitado** e **Habilitado**.  

7.  Para configurar a descoberta para pesquisar nomes específicos de comunidade SNMP, clique na guia **Domínios** e, na guia **SNMP** , configure uma ou mais das seguinte opções:  

    -   Para adicionar um nome de comunidade SNMP à lista de **Nomes de comunidades SNMP**, clique no ícone **Novo** ![Ícone Novo](media/Disc_new_Icon.gif) e, na caixa de diálogo **Nome da Nova Comunidade SNMP**, especifique o **Nome** da comunidade SNMP e clique em **OK**.  

    -   Para remover o nome de uma comunidade SNMP, selecione o nome da comunidade e clique no ícone **Excluir** ![Ícone Excluir](media/Disc_delete_Icon.gif).  

    -   Para ajustar a ordem de pesquisa de nomes de comunidades SNMP, selecione o nome da comunidade e clique no ícone **Mover Item para Cima** ![Ícone Mover para cima](media/Disc_moveUp_Icon.gif) ou no ícone **Mover Item para Baixo** ![Ícone Mover para baixo](media/Disc_moveDown_Icon.gif). Quando a descoberta é executada, os nomes de comunidades são pesquisados em uma ordem de cima para baixo.  

        > [!NOTE]  
        >  A Descoberta de Rede usa nomes de comunidades SNMP para obter acesso aos roteadores que são dispositivos SNMP. Um roteador pode informar à Descoberta de Rede sobre outros roteadores e sub-redes vinculados ao primeiro roteador.  

        -   Os nomes de comunidades SNMP se parecem com senhas.  

        -   A Descoberta de Rede pode obter informações somente de um dispositivo SNMP para o qual você especificou um nome de comunidade.  

        -   Cada dispositivo SNMP pode ter seu próprio nome de comunidade, mas, geralmente, o mesmo nome de comunidade é compartilhado entre vários dispositivos  

        -   A maioria dos dispositivos SNMP tem um nome de comunidade padrão **Pública** que pode ser usado se você não souber nenhum outro nome de comunidade. No entanto, algumas organizações excluem o nome da comunidade **Pública** de seus dispositivos como uma precaução de segurança.  

8.  Para configurar o número máximo de saltos do roteador para uso por pesquisas SNMP, clique na guia **SNMP** e, na guia **SNMP** , selecione o número de saltos na lista suspensa **Máximo de saltos** .  

9. Para configurar **Dispositivos SNMP**, clique na guia **Dispositivos SNMP** e, na guia **SNMP**, se o dispositivo não estiver listado, clique no ícone **Novo** ![Ícone Novo](media/Disc_new_Icon.gif). Na caixa de diálogo **Novo Dispositivo SNMP** , especifique o endereço IP ou o nome do dispositivo SNMP e clique em **OK**.  

    > [!NOTE]  
    >  Se você especificar o nome de um dispositivo, o Configuration Manager deverá ser capaz de resolver o nome NetBIOS de um endereço IP.  

10. Para configurar a descoberta para consultar servidores DHCP específicos para clientes SNMP, clique na guia **DHCP** e, na guia **DHCP** , configure uma ou mais das seguinte opções:  

    -   Para consultar o servidor DHCP no computador que está executando a descoberta, marque a caixa de seleção **Sempre usar o servidor DHCP do servidor do site** .  

        > [!NOTE]  
        >  Para usar esta opção, o servidor deve conceder seu endereço IP de um servidor DHCP e não pode usar um endereço IP estático.  

    -   Para consultar um servidor DHCP específico, clique no ícone **Novo** ![Ícone Novo](media/Disc_new_Icon.gif) e, na caixa de diálogo **Novo Servidor DHCP**, especifique o endereço IP ou o nome do servidor DHCP e clique em **OK**.  

        > [!NOTE]  
        >  Se você especificar o nome de um servidor, o Configuration Manager deverá ser capaz de resolver o nome NetBIOS de um endereço IP.  

11. Para configurar quando a descoberta é executada, clique na guia **Agendamento** e na guia **Agendamento**, clique no ícone **Novo** ![Ícone Novo](media/Disc_new_Icon.gif) para definir um cronograma segundo o qual executar a Descoberta de Rede.  

     Você pode configurar vários agendamentos para a Descoberta de Rede que inclui vários agendamentos recorrentes e vários agendamentos sem recorrência.  

    > [!NOTE]  
    >  Se vários agendamentos forem exibidos na guia **Agendamento** ao mesmo tempo, todos os agendamentos resultarão em uma execução da Descoberta de Rede, já que ela está configurada no período indicado no agendamento. Isso também é verdadeiro para agendamentos recorrentes.  

12. Clique em **OK** para salvar as configurações.  

###  <a name="a-namebkmkhowtoverifynetdisca-how-to-verify-that-network-discovery-has-finished"></a><a name="BKMK_HowToVerifyNetDisc"></a> Como verificar se a Descoberta de Rede foi concluída  
 O tempo de que a Descoberta de Rede precisa para ser concluída pode variar dependendo de uma série de fatores. Esses fatores podem incluir um ou mais destes itens:  

-   O tamanho da rede  

-   A topologia da rede  

-   O número máximo de saltos que estão configurados para localizar roteadores na rede  

-   O tipo de descoberta que está sendo executado  

Como a Descoberta de Rede não cria mensagens para alertar quando a descoberta está concluída, você pode usar o seguinte procedimento para verificar quando ela está concluída.  

##### <a name="to-verify-that-network-discovery-has-finished"></a>Para verificar se a Descoberta de Rede foi concluída  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , expanda **Status do Sistema**e clique em **Consultas de Mensagens de Status**.  

3.  Selecione **Todas as Mensagens de Status**.  

4.  Na guia **Início** , no grupo **Consultas de Mensagens de Status** , clique em **Mostrar Mensagens**.  

5.  Selecione a lista suspensa **Selecionar data e hora** e selecione um valor que inclui há quanto tempo a descoberta foi iniciada, e clique em **OK** para abrir o **Visualizador de Mensagens de Status do Configuration Manager**.  

    > [!TIP]  
    >  Você também pode usar a opção **Especificar data e hora** para selecionar a data e a hora em que você executou a descoberta. Essa opção é útil quando a descoberta de rede foi executada em uma determinada data e você deseja recuperar mensagens somente dessa data.  

6.  Para validar a conclusão da descoberta de rede, procure uma mensagem de status com os seguintes detalhes:  

    -   ID da mensagem: **502**  

    -   Componente: **SMS_NETWORK_DISCOVERY**  

    -   Descrição: **Este componente parou**  

    Caso essa mensagem de status não esteja presente, a descoberta de rede ainda não foi concluída.  

7.  Para validar quando foi iniciada a descoberta de rede, procure a mensagem de status com os seguintes detalhes:  

    -   ID da mensagem: **500**  

    -   Componente: **SMS_NETWORK_DISCOVERY**  

    -   Descrição: **Este componente foi iniciado**  

    Essa informação verifica se a descoberta de rede foi iniciada. Se essa informação não estiver presente, reagende a descoberta de rede.  



<!--HONumber=Dec16_HO3-->


