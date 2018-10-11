---
title: Configurar a descoberta
titleSuffix: Configuration Manager
description: Configure métodos de descoberta para encontrar recursos para gerenciá-los na rede, no Active Directory e no Azure Active Directory.
ms.date: 08/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e232875aab086dea04261abc4d83df8d5d03e6c8
ms.sourcegitcommit: aca62bd3d267b1dbea46d4db6f32d797c5f6263c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/31/2018
ms.locfileid: "43347963"
---
# <a name="configure-discovery-methods-for-configuration-manager"></a>Configurar métodos de descoberta para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Configure métodos de descoberta para encontrar recursos para gerenciá-los na rede, no Active Directory e no Azure AD (Azure Active Directory). Primeiro habilite e, em seguida, configure cada método que desejar usar para pesquisar o ambiente. Desabilite também um método usando o mesmo procedimento usado para habilitá-lo. As únicas exceções a esse processo são a descoberta de pulsação e a descoberta de servidor:  

-   Por padrão, a **descoberta de pulsação** já está habilitada quando você instala um site primário do Configuration Manager. Ela é configurada para ser executada de acordo com um agendamento básico. Mantenha a descoberta de pulsação habilitada. Ela garante que os DDRs (registros dos dados de descoberta) dos dispositivos fiquem atualizados. Para saber mais sobre a Descoberta de Pulsação, consulte [Sobre a Descoberta de Pulsação](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutHeartbeat).  

-   A **descoberta de servidor** é um método de descoberta automática. Ela localiza os computadores utilizados como sistemas de sites. Você não pode configurar ou desabilitá-la.  

### <a name="enable-a-configurable-discovery-method"></a>Habilitar um método de descoberta configurável  
 > [!NOTE]  
 > As informações a seguir não se aplicam à descoberta de usuários do Azure AD. Em vez disso, consulte [Configurar a descoberta de usuários do Azure AD](#azureaadisc) mais adiante neste artigo.

1.  No console do Configuration Manager, acesse o espaço de trabalho **Administração**, expanda a **Configuração da Hierarquia** e, em seguida, selecione **Métodos de Descoberta**.  

2.  Selecione o método de descoberta para o site em que deseja habilitar a descoberta.  

3.  Na guia **Início** da faixa de opções, no grupo **Propriedades**, selecione **Propriedades**. Em seguida, na guia **Geral**, selecione a opção para **Habilitar &lt;método de descoberta\>**.  

     Se essa opção já estiver habilitada, você poderá desabilitar o método de descoberta desmarcando a caixa de seleção.  

4.  Selecione **OK** para salvar a configuração.  



##  <a name="BKMK_ConfigADForestDisc"></a> Configurar a Descoberta de Florestas do Active Directory  

Para concluir a configuração da Descoberta de Florestas do Active Directory, defina as configurações nos seguintes locais do console do Configuration Manager:  

- No nó **Métodos de Descoberta**:

    - Habilitar este método de descoberta.  

    - Definir um agendamento para a sondagem.  

    - Selecionar se a descoberta criará automaticamente os limites para os sites do Active Directory e as sub-redes que ela descobre.  

- No nó **Florestas do Active Directory**:

    - Adicionar florestas que você deseja descobrir.  

    - Habilitar a descoberta de sites do Active Directory e sub-redes na floresta.  

    - Definir as configurações que permitem aos sites do Configuration Manager publicar as informações do site na floresta.  

    - Atribuir uma conta a ser usada como a Conta de Floresta do Active Directory para cada floresta.  

Use os procedimentos a seguir para habilitar a descoberta de florestas do Active Directory e para configurar florestas individuais a serem usadas com a Descoberta de Florestas do Active Directory.  


### <a name="enable-active-directory-forest-discovery"></a>Habilitar a Descoberta de Florestas do Active Directory  

1.  No console do Configuration Manager, acesse o espaço de trabalho **Administração**, expanda a **Configuração da Hierarquia** e selecione o nó **Métodos de Descoberta**.  

2.  Selecione o método de descoberta de floretas do Active Directory para o site em que deseja configurar a descoberta.  

3.  Na guia **Início** da faixa de opções, no grupo **Propriedades**, selecione **Propriedades**.  

4.  Na guia **Geral**, marque a caixa de seleção para habilitar a descoberta. Ou você pode configurar a descoberta agora e voltar para habilitá-la posteriormente.  

5.  Especifique opções para criar limites de site para locais descobertos.  

6.  Especifique um agendamento para quando a descoberta for executada.  

7.  Selecione **OK** para salvar a configuração.  


### <a name="configure-a-forest-for-active-directory-forest-discovery"></a>Configurar uma floresta para Descoberta de Florestas do Active Directory  

1.  No espaço de trabalho **Administração**, expanda **Configuração da Hierarquia** e selecione o nó **Florestas do Active Directory**. Se uma descoberta de florestas do Active Directory tiver sido executada anteriormente, você verá cada floresta descoberta no painel de resultados. A floresta local e quaisquer florestas confiáveis são detectadas quando a descoberta de florestas do Active Directory é executada. Você só precisa adicionar manualmente florestas não confiáveis.  

    -   Para configurar uma floresta descoberta anteriormente, selecione-a no painel de resultados. Em seguida, na guia **Início** da faixa de opções, no grupo **Propriedades**, selecione **Propriedades** para abrir as propriedades da floresta. Continue na etapa 3.  

    -   Para configurar uma nova floresta que não esteja listada, na guia **Início** da faixa de opções, no grupo **Criar**, selecione **Adicionar Floresta**. Esta ação abre a caixa de diálogo **Adicionar Florestas**. Continue na etapa 3.  

2.  Na guia **Geral**, complete as configurações da floresta que você deseja descobrir e especifique a **Conta da Floresta do Active Directory**. Para saber mais sobre esta conta, confira [Contas](/sccm/core/plan-design/hierarchy/accounts#active-directory-forest-account).  

    > [!NOTE]  
    >  A descoberta de florestas do Active Directory requer uma conta global para descobrir e publicar em florestas não confiáveis. Se você não usar a conta de computador do servidor do site, selecione somente uma conta global.  

3.  Se você pretende permitir que os sites publiquem dados nessa floresta, na guia **Publicação** conclua as configurações para que seja possível fazer publicações nessa floresta.  

    > [!NOTE]  
    >  Se você permitir que sites publiquem em uma floresta, estenda o esquema do Active Directory dessa floresta para o Configuration Manager. A conta de floresta do Active Directory deve ter permissões de controle total ao contêiner do sistema nessa floresta.  

4.  Selecione **OK** para salvar a configuração.  



##  <a name="BKMK_ConfigADDiscGeneral"></a> Configurar a Descoberta do Active Directory para computadores, usuários ou grupos  

Para configurar a descoberta de computadores, usuários ou grupos, comece com estas etapas comuns:

1.  No console do Configuration Manager, acesse o espaço de trabalho **Administração**, expanda a **Configuração da Hierarquia** e selecione o nó **Métodos de Descoberta**.  

2.  Selecione o método para o site em que deseja configurar a descoberta.  

3.  Na guia **Início** da faixa de opções, no grupo **Propriedades**, selecione **Propriedades**.  

4.  Na guia **Geral**, marque a caixa de seleção para habilitar a descoberta. Ou você pode configurar a descoberta agora e voltar para habilitá-la posteriormente.  

Em seguida, use as informações nas seções a seguir para configurar os métodos de descoberta específicos:  

- [Descoberta de Grupos do Active Directory](#bkmk_config-adgd)  

- [Descoberta de Sistemas do Active Directory](#bkmk_config-adgd)  

- [Descoberta de Usuários do Active Directory](#bkmk_config-adud)  

> [!NOTE]  
>  As informações desta seção não se aplicam à descoberta de florestas do Active Directory.  

 Embora cada um desses métodos de descoberta seja independente dos outros, eles compartilham opções semelhantes. Para saber mais sobre essas opções de configuração, confira [Opções compartilhadas para descoberta de grupos, sistemas e usuários](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_shared).  

> [!WARNING]  
>  A sondagem do Active Directory por cada um desses métodos de descoberta pode gerar tráfego de rede significativo. Considere a possibilidade de agendar cada um dos métodos de descoberta para que eles sejam executados em um momento em que esse tráfego de rede não prejudique os usos corporativos da rede.  


### <a name="bkmk_config-adgd"></a> Configurar Descoberta de Grupos do Active Directory  

1. Na guia **Geral** da janela Propriedades de Descoberta de Grupo do Active Directory, selecione **Adicionar** para configurar um escopo de descoberta. Selecione **Grupos** ou **Local**. Em seguida, conclua as seguintes configurações na caixa de diálogo **Adicionar Grupos** ou **Adicionar Local do Active Directory**:  

    1.  Especifique um **nome** para esse escopo de descoberta.  

    2.  Especifique um **Domínio do Active Directory** ou **Local** para pesquisa:  

        -   Se você tiver escolhido **Grupos**, especifique um ou mais grupos do Active Directory a descobrir.  

        -   Se você tiver escolhido **Local**, especifique um contêiner do Active Directory como um local a descobrir. Você também pode habilitar uma pesquisa recursiva de contêineres filho do Active Directory para esse local.  

    3.  Especifique a **Conta de Descoberta de Grupos do Active Directory** que o site usa para pesquisar esse escopo de descoberta. Para saber mais, confira [Contas](/sccm/core/plan-design/hierarchy/accounts#active-directory-group-discovery-account).  

    4.  Selecione **OK** para salvar a configuração do escopo de descoberta.  

2.  Repita as etapas anteriores para cada escopo de descoberta adicional que desejar definir.  

3.  Na guia **Agendamento de Sondagem** , configure o agendamento de sondagem de descoberta completa e a descoberta de deltas.  

4.  Na guia **Opções**, defina configurações para filtrar ou excluir registros de computador obsoletos da descoberta. Configure também a descoberta da associação de grupos de distribuição.  

    > [!NOTE]  
    >  Por padrão, a descoberta de grupos do Active Directory descobre apenas a associação de grupos de segurança.  

5. Selecione **OK** para salvar a configuração.  


### <a name="bkmk_config-adsd"></a> Configurar a Descoberta de Sistemas do Active Directory  

1. Na guia **Geral** da janela Propriedades de Descoberta do Sistema do Active Directory, selecione o ícone **Novo** ![ícone Novo](media/Disc_new_Icon.gif) para especificar um novo contêiner do Active Directory. Na caixa de diálogo **Contêiner do Active Directory**, conclua as configurações a seguir:  

    1.  Digite ou procure um local para o **Caminho**. Esse valor é um caminho LDAP válido para um contêiner ou unidade organizacional (UO). O site consulta esse caminho em busca de recursos. Por exemplo, `LDAP://CN=Computers,DC=contoso,DC=com`  

    2.  Especifique opções que mudam o comportamento da pesquisa:  

        - **Descobrir objetos em grupos do Active Directory**: o site também analisa a associação de grupos nesse caminho.  

        - **Pesquisar recursivamente contêineres filho do Active Directory**: se você habilitar essa opção, o site pesquisará contêineres ou unidades organizacionais adicionais no caminho acima. Se você desabilitar essa opção, o site só procurará recursos no caminho específico.  

            A partir da versão 1806, selecione subcontêineres para excluir desta pesquisa recursiva. Esta opção ajuda a reduzir o número de objetos descobertos. Selecione **Adicionar** para escolher os contêineres no caminho acima. Na caixa de diálogo Selecionar Novo Contêiner, selecione um contêiner filho para exclusão. Selecione **OK** para fechar a caixa de diálogo Selecionar Novo Contêiner.<!--1358143-->

            > [!Tip]  
            > A lista de contêineres do Active Directory na janela Propriedades da Descoberta de Sistema do Active Directory inclui uma coluna **Tem exclusões**. Quando você seleciona contêineres para excluir, esse valor é **Sim**.  

    3.  Em cada local, especifique a conta a ser usada como a **Conta de descoberta do Active Directory**. Para saber mais, confira [Contas](/sccm/core/plan-design/hierarchy/accounts#active-directory-system-discovery-account).  

        > [!TIP]  
        >  Em cada local especificado, configure um conjunto de opções de descoberta e uma Conta de Descoberta exclusiva do Active Directory.  

    4.  Selecione **OK** para salvar a configuração do contêiner do Active Directory.  

2.  Na guia **Agendamento de Sondagem** , configure o agendamento de sondagem de descoberta completa e a descoberta de deltas.  

3.  Na guia **Atributos do Active Directory**, configure atributos adicionais do Active Directory para computadores que você deseja descobrir. Esta guia lista os atributos de objeto padrão.  

     > [!Tip]  
     > Por exemplo, sua organização usa o atributo **Descrição** na conta de computador no Active Directory. Selecione **Personalizar** e adicione `Description` como um atributo personalizado. Depois de executar esse método de descoberta, esse atributo é mostrado na guia Propriedades do dispositivo no console do Configuration Manager.<!--513948-->  

4.  Na guia **Opções**, defina configurações para filtrar ou excluir registros de computador obsoletos da descoberta.  

5. Selecione **OK** para salvar a configuração.  


### <a name="bkmk_config-adud"></a> Configurar a Descoberta de Usuários do Active Directory  

1.  Na guia **Geral** da janela Propriedades de Descoberta de Usuários do Active Directory, selecione o ícone **Novo** ![ícone Novo](media/Disc_new_Icon.gif) para especificar um novo contêiner do Active Directory. Na caixa de diálogo **Contêiner do Active Directory**, conclua as configurações a seguir:  

    1.  Especifique um ou mais locais para pesquisa.  

    2.  Em cada local, especifique opções que mudam o comportamento da pesquisa.  

    3.  Em cada local, especifique a conta a ser usada como a **Conta de descoberta do Active Directory**. Para saber mais, confira [Contas](/sccm/core/plan-design/hierarchy/accounts#active-directory-user-discovery-account).  

        > [!NOTE]  
        >  Em cada local especificado, configure um conjunto exclusivo de opções de descoberta e uma Conta de Descoberta exclusiva do Active Directory.  

    4.  Selecione **OK** para salvar a configuração do contêiner do Active Directory.  

6.  Na guia **Agendamento de Sondagem** , configure o agendamento de sondagem de descoberta completa e a descoberta de deltas.  

7.  Na guia **Atributos do Active Directory**, configure atributos adicionais do Active Directory para computadores que você deseja descobrir. Esta guia lista os atributos de objeto padrão.  

8.  Selecione **OK** para salvar a configuração.  



## <a name="azureaadisc"></a> Configurar a Descoberta de Usuário do Azure AD

A descoberta de usuários do Azure AD não é habilitada nem configurada da mesma maneira que outros métodos de descoberta. Configure-a ao carregar o site do Configuration Manager no Azure AD. Ao [Configurar os Serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para o **Gerenciamento de Nuvem**, habilite e configure também esse método de descoberta. 

Ao configurar o serviço do Azure **Gerenciamento de Nuvem**: 
- Na página **Descoberta** do assistente, selecione a opção para **Habilitar a Descoberta de Usuários do Azure Active Directory**. 
- Selecione **Configurações**. 
- Na caixa de diálogo Configurações da Descoberta de Usuários do Azure AD, configure um agendamento que indica quando ocorre a descoberta. Habilite também a descoberta de deltas, que verifica apenas as contas novas ou alteradas no Azure AD. 

Para obter mais informações, consulte [Descoberta de usuários do Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

 > [!Important]  
 > Antes de *importar* o aplicativo do Azure AD para o Configuration Manager, você precisa conceder a permissão de aplicativo para servidores para ler os dados do diretório do Azure AD. 
 >  - No [portal do Azure](https://portal.azure.com), acesse a folha **Azure Active Directory**. 
 >  - Selecione **Registros de aplicativo** e alterne para **Todos os aplicativos**, se necessário. 
 >  - Selecione o aplicativo para servidores do tipo *Aplicativo Web/API* e, em seguida, selecione **Configurações**. 
 >  - Selecione **Permissões necessárias** e, em seguida, selecione **Conceder permissões**.
 >  
 > Se você *criar* o aplicativo para servidores por meio do Configuration Manager, o Azure AD criará automaticamente as permissões com o aplicativo. Você ainda precisa dar o consentimento ao aplicativo no portal do Azure.

 > [!Note]  
 > Se o usuário tiver uma identidade federada ou sincronizada, use a [descoberta de usuários do Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser) do Configuration Manager, bem como a descoberta de usuários do Azure AD. Para obter mais informações sobre identidades híbridas, consulte [Definir uma estratégia de adoção de identidade híbrida](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->



##  <a name="BKMK_ConfigHBDisc"></a> Configurar a Descoberta de Pulsação  

O Configuration Manager habilita o método de descoberta de pulsação quando você instala um site primário. Se você quiser usar o agendamento padrão de sete em sete dias, não há mais nada a configurar. Caso contrário, você só precisa configurar a programação para a frequência com que os clientes enviam o registro de dados da Descoberta de Pulsação para um ponto de gerenciamento.  

> [!NOTE]  
>  Se você habilitar a instalação de push de cliente e a tarefa de manutenção de site para **Limpar Sinalizador de Instalação** ao mesmo tempo, defina o agendamento da descoberta de pulsação para ser menor do que o **Período de Redescoberta de Cliente** da tarefa de manutenção de site **Limpar Sinalizador de Instalação**. Para saber mais sobre tarefas de manutenção de site, confira [Tarefas de manutenção](/sccm/core/servers/manage/maintenance-tasks).  


### <a name="configure-the-heartbeat-discovery-schedule"></a>Configurar o agendamento de Descoberta de Pulsação  

1.  No console do Configuration Manager, acesse o espaço de trabalho **Administração**, expanda a **Configuração da Hierarquia** e selecione o nó **Métodos de Descoberta**.  

2.  Selecione o método **Descoberta de Pulsação** para o site em que deseja configurar a descoberta de pulsação.  

3.  Na guia **Início** da faixa de opções, no grupo **Propriedades**, selecione **Propriedades**.  

4.  Configure a frequência com que os clientes enviam registros de dados de descoberta de pulsação. Em seguida, selecione **OK** para salvar a configuração.  



<a name="BKMK_AboutConfigNetworkDisc"></a>

##  <a name="BKMK_ConfigNetworkDisc"></a> Configurar a Descoberta de Rede  

 Antes de configurar a descoberta de rede, entenda os seguintes tópicos:  

-   Níveis disponíveis de descoberta de rede  

-   Opções de descoberta de rede disponíveis  

-   Limitação de descoberta de rede na rede  

Para saber mais, consulte [Sobre a Descoberta de Rede](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutNetwork).  

As seções a seguir fornecem informações sobre configurações comuns de descoberta de rede. Você pode configurar uma ou mais dessas configurações para uso durante a execução da mesma descoberta. Se você usar várias configurações, planeje as interações que podem afetar os resultados da descoberta.  

Por exemplo, você descobre todos os dispositivos SNMP (Simple Network Management Protocol) que usam um nome de comunidade SNMP específico. Para a mesma execução de descoberta, você desabilita a descoberta em uma sub-rede específica. Quando a descoberta é executada, a descoberta de rede não descobre os dispositivos SNMP com o nome da comunidade especificado na sub-rede desabilitada.  


###  <a name="BKMK_DetermineNetTopology"></a> Determinar a topologia de rede  

 Você pode usar uma descoberta somente de topologia para mapear sua rede. Esse tipo de descoberta não descobre clientes potenciais. A Descoberta de Rede somente de topologia depende do SNMP.  

 Ao mapear a topologia de rede, configure o **Máximo de saltos** na guia **SNMP** na caixa de diálogo **Propriedades da Descoberta e Rede**. Apenas alguns saltos podem ajudar a controlar a largura de banda da rede usada quando a descoberta é executada. À medida que você descobre mais sobre a rede, aumenta o número de saltos para ter um entendimento melhor da topologia de rede.  

 Depois de entender sua topologia de rede, configure propriedades adicionais para a Descoberta de Rede. Essas propriedades ajudam a descobrir clientes em potencial e seus sistemas operacionais. Além disso, configure a Descoberta de Rede para limitar os segmentos de rede que ela pode pesquisar.  

 Para saber mais, confira [Como determinar sua topologia de rede](#bkmk_proc-top)


### <a name="network-discovery-search-options"></a>Opções de pesquisa de Descoberta de Rede

O Configuration Manager oferece suporte aos seguintes métodos para pesquisar na rede:
- [Limitar pesquisas usando sub-redes](#BKMK_LimitBySubnet)
- [Pesquisar um domínio específico](#BKMK_SearchByDomain)
- [Limitar pesquisas usando nomes de comunidades SNMP](#BKMK_LimitBySNMPname)
- [Pesquisar um servidor DHCP específico](#BKMK_SearchByDHCP)

####  <a name="BKMK_LimitBySubnet"></a> Limitar pesquisas usando sub-redes  

 Você pode configurar a Descoberta de Rede para pesquisar sub-redes específicas durante uma descoberta. Por padrão, a Descoberta de Rede pesquisa a sub-rede do servidor que executa a descoberta. Todas as sub-redes adicionais que você configurar e ativar aplicam-se somente às opções de pesquisa de SNMP e de DHCP. Quando a descoberta de rede pesquisa domínios, ela não é limitada pelas configurações de sub-redes.  

 Se você especificar uma ou mais sub-redes na guia **Sub-redes** na caixa de diálogo **Propriedades de Descoberta de Rede**, ele pesquisará somente as sub-redes que você marcar como **Habilitadas**.  

 Quando você desativa uma sub-rede, o site a exclui da descoberta e as seguintes condições se aplicam:  

-   As consultas baseadas em SNMP não são executadas na sub-rede.  

-   Os servidores DHCP não respondem com uma lista de recursos localizados na sub-rede.  

-   As consultas baseadas em domínio podem descobrir recursos que estão localizados na sub-rede.  


####  <a name="BKMK_SearchByDomain"></a> Pesquisar um domínio específico  

 Você pode configurar uma Descoberta de Rede para pesquisar um domínio específico ou um conjunto de domínios durante uma descoberta. Por padrão, a Descoberta de Rede pesquisa o domínio do servidor que executa a descoberta.  

 Se você especificar um ou mais domínios na guia **Domínios** na caixa de diálogo **Propriedades de Descoberta de Rede**, ele pesquisará somente nos domínios marcados como **Habilitados**.  

 Quando você desativa um domínio, o site o exclui da descoberta e as seguintes condições se aplicam:  

-   A Descoberta de Rede não consulta controladores de domínio nesse domínio.  

-   Ainda é possível executar consultas baseadas em SNMP em sub-redes no domínio.  

-   Os servidores DHCP ainda podem responder com uma lista de recursos localizados no domínio.  


#### <a name="BKMK_LimitBySNMPname"></a> Limitar pesquisas usando nomes de comunidades SNMP  

 Configure uma Descoberta de Rede para pesquisar uma comunidade SNMP específica ou um conjunto de comunidades durante uma descoberta. Por padrão, o método configura o nome da comunidade **pública**.  

 A Descoberta de Rede usa nomes de comunidades para obter acesso aos roteadores que são dispositivos SNMP. Um roteador pode fornecer à Descoberta de Rede informações sobre outros roteadores e sub-redes que estejam vinculados ao primeiro roteador.  

> [!NOTE]  
>  Os nomes de comunidades SNMP se parecem com senhas. A descoberta de rede pode obter informações somente de um dispositivo SNMP para o qual você especificou um nome da comunidade. Cada dispositivo SNMP pode ter seu próprio nome de comunidade, mas, geralmente, o mesmo nome de comunidade é compartilhado entre vários dispositivos. Além disso, a maioria dos dispositivos SNMP têm um nome de comunidade padrão de **pública**. Mas algumas organizações excluem o nome da comunidade **Pública** de seus dispositivos como uma precaução de segurança.  

 Se você incluir mais de uma comunidade SNMP na guia **SNMP** na caixa de diálogo **Propriedades de Descoberta de Rede**, ela as pesquisará na ordem em que são exibidas. Certifique-se de que os nomes usados ​​com mais frequência estejam no topo da lista. Essa configuração ajuda a minimizar o tráfego de rede que o site gera quando tenta entrar em contato com um dispositivo usando nomes diferentes.

> [!NOTE]  
>  Além de usar o nome da comunidade SNMP, você pode especificar o endereço IP ou o nome que pode ser resolvido de um dispositivo SNMP específico. Faça isso na guia **Dispositivos SNMP** da caixa de diálogo **Propriedades da Descoberta de Rede**.  


####  <a name="BKMK_SearchByDHCP"></a> Pesquisar um servidor DHCP específico  

 Você pode configurar a Descoberta de Rede para usar um servidor SNMP específico ou vários servidores para descobrir clientes DHCP durante uma descoberta.  

 A Descoberta de Rede pesquisa cada servidor DHCP especificado na guia **DHCP** na caixa de diálogo **Propriedades da Descoberta de Rede** . Se o servidor que está executando a descoberta conceder o seu endereço IP de um servidor DHCP, você poderá configurar a descoberta para pesquisar esse servidor DHCP. Habilite este comportamento com a opção para **Incluir o servidor DHCP que o servidor do site está configurado para usar**.  

> [!NOTE]  
>  Para configurar um servidor DHCP com êxito na Descoberta de Rede, o ambiente deve oferecer suporte a IPv4. Não é possível configurar a descoberta de rede para usar um servidor DHCP em um ambiente IPv6 nativo.  


###  <a name="BKMK_HowToConfigNetDisc"></a> Como configurar a Descoberta de Rede  

 Use os procedimentos a seguir para descobrir primeiro somente a topologia de rede e, em seguida, configurar a Descoberta de Rede para descobrir clientes potenciais usando uma ou mais das opções disponíveis da Descoberta de Rede.  

#### <a name="bkmk_proc-top"></a> Como determinar sua topologia de rede  

1.  No console do Configuration Manager, acesse o espaço de trabalho **Administração**, expanda a **Configuração da Hierarquia** e selecione o nó **Métodos de Descoberta**.  

2.  Selecione o método **Descoberta de Rede** para o site em que você deseja descobrir os recursos da rede.  

3.  Na guia **Início** da faixa de opções, no grupo **Propriedades**, selecione **Propriedades**.  

    -   Na guia **Geral**, selecione a opção para **Habilitar descoberta de rede**. Em seguida, selecione **Topologia** nas opções **Tipo de descoberta**.  

    -   Na guia **Sub-redes**, marque a opção **Pesquisar sub-redes locais**.  

        > [!TIP]  
        >  Se você conhece as sub-redes específicas que constituem sua rede, desmarque a caixa de seleção **Pesquisar sub-redes locais**. Em seguida, selecione o ícone **Novo** ![ícone Novo](media/Disc_new_Icon.gif) para adicionar as sub-redes específicas que deseja pesquisar. Para sub-redes grandes, geralmente, pesquise somente uma ou duas sub-redes por vez para minimizar o uso de largura de banda da rede.  

    -   Na guia **Domínios**, marque a opção para **Pesquisar domínios locais**.  

    -   Na guia **SNMP**, selecione uma opção na lista suspensa **Máximo de saltos**. Essa opção especifica quantos saltos de roteador a Descoberta de Rede pode realizar no mapeamento de sua topologia.  

        > [!TIP]  
        >  Ao mapear a topologia de rede pela primeira vez, configure poucos saltos do roteador para minimizar o uso de largura de banda de rede.  

4.  Na guia **Agendamento**, selecione o ícone **Novo** ![ícone Novo](media/Disc_new_Icon.gif) para definir um agendamento para executar a descoberta.  

    > [!NOTE]  
    >  Não é possível atribuir uma configuração de descoberta diferente para separar agendamentos de descoberta de rede. Cada vez que a Descoberta de Rede é executada, ela usa a configuração de descoberta atual.  

5.  Selecione **OK** para aceitar as configurações. A Descoberta de Rede é executada no horário agendado.  


#### <a name="bkmk_proc-config"></a> Como configurar a Descoberta de Rede  

1.  No console do Configuration Manager, acesse o espaço de trabalho **Administração**, expanda a **Configuração da Hierarquia** e selecione o nó **Métodos de Descoberta**.  

2.  Selecione o método **Descoberta de Rede** para o site em que você deseja descobrir os recursos da rede.  

3.  Na guia **Início** da faixa de opções, no grupo **Propriedades**, selecione **Propriedades**.  

4.  Na guia **Geral**, selecione a opção para **Habilitar descoberta de rede**.  

    - Selecione nas opções de **Tipo de descoberta** o tipo de descoberta que você deseja executar.  

    - Habilite a opção **Rede lenta** para o Configuration Manager para fazer ajustes automáticos em redes de baixa largura de banda.  

5.  Para configurar a descoberta para pesquisar sub-redes, mude para a guia **Sub-redes**. Em seguida, configure uma ou mais das seguintes opções:  

    -   Para executar a descoberta em sub-redes locais no computador que executa a descoberta, habilite a opção para **Pesquisar sub-redes locais**.  

    -   Para pesquisar uma sub-rede específica, ela deve estar listada em **Sub-redes a serem pesquisadas** e ter um valor de **Pesquisa** de **Habilitado**:  

        1.  Se a sub-rede não estiver listada, selecione o ícone **Novo** ![ícone Novo](media/Disc_new_Icon.gif). Na caixa de diálogo **Nova Atribuição de Sub-rede**, insira as informações da **Sub-rede** e da **Máscara** e selecione **OK**. Por padrão, uma nova sub-rede está habilitada para pesquisa.  

        2.  Para alterar o valor **Pesquisar** de uma sub-rede listada, selecione-a na lista. Em seguida, selecione o ícone **Alternar** para alternar o valor entre **Desabilitado** e **Habilitado**.  

6.  Para configurar a descoberta para pesquisar domínios, mude para a guia **Domínios**. Em seguida, configure uma ou mais das seguintes opções:  

    -   Para executar a descoberta no domínio do computador que executa a descoberta, habilite a opção para **Pesquisar domínio local**.  

    -   Para pesquisar um domínio específico, ele deve estar listado em **Domínios** e ter um valor de **Pesquisa** de **Habilitado**:  

        1.  Se o domínio não estiver listado, selecione o ícone **Novo** ![ícone Novo](media/Disc_new_Icon.gif). Na caixa de diálogo **Propriedades de Domínio**, insira as informações do **Domínio** e, em seguida, selecione **OK**. Por padrão, um novo domínio está habilitado para pesquisa.  

        2.  Para alterar o valor **Pesquisar** de um domínio listado, selecione-o na lista. Em seguida, selecione o ícone **Alternar** para alternar o valor entre **Desabilitado** e **Habilitado**.  

7.  Para configurar a descoberta para pesquisar nomes de comunidades de SNMP específicos para dispositivos SNMP, mude para a guia **SNMP**. Em seguida, configure uma ou mais das seguintes opções:  

    - Para adicionar um nome de comunidade SNMP à lista de **Nomes de Comunidades SNMP**, selecione o ícone **Novo** ![ícone Novo](media/Disc_new_Icon.gif). Na caixa de diálogo **Novo Nome de Comunidade SNMP**, especifique o **Nome** da comunidade SNMP e, em seguida, selecione **OK**.  

    - Para remover o nome de uma comunidade SNMP, selecione o nome da comunidade e selecione o ícone **Excluir** ![Ícone Excluir](media/Disc_delete_Icon.gif).  

    - Para ajustar a ordem de pesquisa dos nomes de comunidades SNMP, selecione um nome de comunidade na lista. Em seguida, selecione o ícone **Mover Item para Cima** ![Ícone Mover para Cima](media/Disc_moveUp_Icon.gif) ou o ícone **Mover Item para Baixo** ![Ícone Mover para Baixo](media/Disc_moveDown_Icon.gif). Quando a descoberta é executada, os nomes de comunidades são pesquisados em uma ordem de cima para baixo. 

    - Para configurar o número máximo de saltos do roteador para uso por pesquisas SNMP, selecione o número de saltos na lista suspensa **Máximo de saltos**.  

8. Para configurar um dispositivo SNMP, mude para a guia **Dispositivos SNMP**. Se o dispositivo não estiver listado, selecione o ícone **Novo** ![ícone Novo](media/Disc_new_Icon.gif). Na caixa de diálogo **Novo Dispositivo SNMP**, especifique o endereço IP ou o nome do dispositivo SNMP e selecione **OK**.  

    > [!NOTE]  
    >  Se você especificar o nome de um dispositivo, o Configuration Manager deverá ser capaz de resolver o nome NetBIOS de um endereço IP.  

9. Para configurar a descoberta para consultar servidores DHCP específicos, mude para a guia **DHCP**. Em seguida, configure uma ou mais das seguintes opções:  

    -   Para consultar o servidor DHCP no computador que executa a descoberta, habilite a opção para **Sempre usar o servidor DHCP do servidor do site**.  

        > [!NOTE]  
        >  Para usar essa opção, o servidor precisa conceder seu endereço IP de um servidor DHCP e não pode usar um endereço IP estático.  

    -   Para consultar um servidor DHCP específico, selecione o ícone **Novo** ![ícone Novo](media/Disc_new_Icon.gif). Na caixa de diálogo **Novo Servidor DHCP**, especifique o endereço IP ou o nome de servidor do servidor DHCP e selecione **OK**.  

        > [!NOTE]  
        >  Se você especificar o nome de um servidor, o Configuration Manager deverá ser capaz de resolver o nome NetBIOS de um endereço IP.  

10. Para configurar quando a descoberta é executada, mude para a guia **Agendamento**. Em seguida, selecione o ícone **Novo** ![ícone Novo](media/Disc_new_Icon.gif) para definir uma programação para a execução da Descoberta de Rede. Você pode configurar vários agendamentos e vários agendamentos sem recorrência.  

    > [!NOTE]  
    >  Se a guia **Agendamento** mostrar mais de um agendamento ao mesmo tempo, a Descoberta de Rede será executada para todos os agendamentos conforme estiverem configurados no horário indicado no agendamento. Esse comportamento também é verdadeiro para agendamentos recorrentes.  

11. Selecione **OK** para salvar suas configurações.  


###  <a name="BKMK_HowToVerifyNetDisc"></a> Como verificar se a Descoberta de Rede foi concluída  

 O tempo que a descoberta de rede precisa para ser concluída pode variar, dependendo de um ou mais dos seguintes fatores:  

-   O tamanho da rede  

-   A topologia da rede  

-   O número máximo de saltos que estão configurados para localizar roteadores na rede  

-   O tipo de descoberta que está sendo executado  

A descoberta de rede não cria mensagens para alertá-lo quando a descoberta foi concluída. Use o procedimento a seguir para verificar quando a descoberta foi concluída:  

1.  No console do Configuration Manager, acesse o espaço de trabalho **Monitoramento**. Expanda **Status do Sistema** e, em seguida, selecione o nó **Consultas de Mensagens de Status**.  

2.  Selecione a consulta **Todas as Mensagens de Status**.  

3.  Na guia **Início** da faixa de opções, no grupo **Consultas de Mensagens de Status**, selecione **Mostrar Mensagens**.  

4.  Na janela Todas as Mensagens de Status, selecione um valor na lista suspensa **Selecionar data e hora**, que inclui há quanto tempo a descoberta foi iniciada. Em seguida, selecione **OK** para abrir o **Visualizador de Mensagens de Status do Configuration Manager**.  

    > [!TIP]  
    >  Você também pode usar a opção **Especificar data e hora** para selecionar a data e a hora em que você executou a descoberta. Essa opção é útil quando a descoberta de rede foi executada em uma determinada data e você deseja recuperar mensagens somente dessa data.  

5.  Para validar a conclusão da descoberta de rede, procure uma mensagem de status com os seguintes detalhes:  

    -   ID da mensagem: **502**  

    -   Componente: **SMS_NETWORK_DISCOVERY**  

    -   Descrição: **Este componente parou**  

    Caso essa mensagem de status não esteja presente, a descoberta de rede ainda não foi concluída.  

7.  Para validar quando foi iniciada a descoberta de rede, procure a mensagem de status com os seguintes detalhes:  

    -   ID da mensagem: **500**  

    -   Componente: **SMS_NETWORK_DISCOVERY**  

    -   Descrição: **Este componente foi iniciado**  

    Essa informação verifica se a descoberta de rede foi iniciada. Caso essas informações não estejam presentes, reagende a descoberta de rede.  
