---
title: Métodos de descoberta
titleSuffix: Configuration Manager
description: Saiba mais sobre os métodos de descoberta disponíveis para encontrar dispositivos na rede, no Active Directory ou no Azure Active Directory.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ed931751-18f2-4230-a09e-a0a329fbfa1c
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 679f62bb38bab06c074c97e92ff7d3adcae80f1b
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65501440"
---
# <a name="about-discovery-methods-for-system-center-configuration-manager"></a>Sobre métodos de descoberta para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Os métodos de descoberta do Configuration Manager encontram diferentes dispositivos na rede, em dispositivos e usuários do Active Directory ou em usuários do Azure AD (Azure Active Directory). Para usar um método de descoberta de maneira eficiente, você deve compreender suas configurações disponíveis e limitações.  



##  <a name="bkmk_aboutForest"></a> Descoberta de Florestas do Active Directory  
 **Configurável:** Sim  

 **Habilitado por padrão:** Não  

 **Contas** que você pode usar para executar esse método:  

-   **Conta de descoberta de florestas do Active Directory** (definida pelo usuário)  

-   **Conta de computador** do servidor do site  

Ao contrário de outros métodos de descoberta do Active Directory, a descoberta de florestas do Active Directory não descobre recursos que você pode gerenciar. Em vez disso, esse método descobre os locais de rede configurados no Active Directory. Ele pode converter esses locais em limites para uso em toda a hierarquia.  

Quando esse método é executado, ele pesquisa a floresta local do Active Directory, cada floresta confiável e cada floresta adicional que você configurar no nó **Florestas do Active Directory** do console do Configuration Manager.  

Use a descoberta de florestas do Active Directory para:  

-   Descobrir as sub-redes e sites do Active Directory e, em seguida, criar limites do Configuration Manager com base nesses locais de rede.  

-   Identificar super-redes atribuídas a um site do Active Directory. Converter cada super-rede em um limite de intervalo de endereços IP.  

-   Publicar no AD DS (Active Directory Domain Services) em uma floresta quando a publicação nessa floresta está habilitada. A Conta da Floresta especificada do Active Directory deve ter permissões nessa floresta.  

Gerencie a descoberta de florestas do Active Directory no console do Configuration Manager. Acesse o workspace **Administração** e expanda **Configuração da Hierarquia**.   

-   **Métodos de Descoberta**: habilite a descoberta de florestas do Active Directory para ser executada no site de nível superior de sua hierarquia. Especifique também um agendamento simples para executar a descoberta. Configure-a para criar automaticamente limites nas sub-redes IP e sites do Active Directory descobertas por ela. A descoberta de florestas do Active Directory não pode ser executada em um site primário filho ou em um site secundário.  

-   **Florestas do Active Directory**: configure as florestas adicionais a serem descobertas, especifique cada Conta de Floresta do Active Directory e configure a publicação para cada floresta. Monitore o processo de descoberta. Adicione sub-redes IP e sites do Active Directory como limites do Configuration Manager e membros de grupos de limites.  

Para configurar a publicação de florestas do Active Directory para cada site em sua hierarquia, conecte o console do Configuration Manager ao site de nível superior da hierarquia. A guia **Publicando** na caixa de diálogo **Propriedades** de um site do Active Directory pode mostrar apenas o site atual e seus sites filho. Quando a publicação estiver habilitada para uma floresta e o esquema dessa floresta for estendido para o Configuration Manager, as seguintes informações serão publicadas em cada site que estiver habilitado para publicar nessa floresta do Active Directory:  

-    **SMS-Site-&lt;código do site>**

-   **SMS-MP-&lt;código do site>-&lt;nome do servidor do sistema de sites>**  

-   **SMS-SLP-&lt;código do site>-&lt;nome do servidor do sistema de sites>**  

-   **SMS-&lt;código do site>-&lt;sub-rede ou nome do site do Active Directory>**  

> [!NOTE]  
>  Sites secundários usam sempre a conta de computador do servidor do site secundário para publicar no Active Directory. Se desejar que sites secundários publiquem no Active Directory, verifique se o computador do servidor do site secundário tem permissões para publicar no Active Directory. Um site secundário não pode publicar dados em uma floresta não confiável.  

> [!CAUTION]  
>  Ao desmarcar a opção para publicar um site em uma floresta do Active Directory, todas as informações publicadas anteriormente nesse site, incluindo funções disponíveis do sistema de site, são removidas do Active Directory.  

As ações da descoberta de florestas do Active Directory são registradas nos logs a seguir:  

-   Todas as ações, exceto aquelas relacionadas à publicação, são registradas no arquivo **ADForestDisc.Log** na pasta **&lt;CaminhodeInstalação>\Logs** no servidor de sites.  

-   As ações de publicação da descoberta de florestas do Active Directory são registradas nos arquivos **hman.log** e **sitecomp.log** na pasta **&lt;CaminhodeInstalação>\Logs** no servidor de sites.  

Para obter mais informações sobre como configurar esse método de descoberta, consulte [Configurar métodos de descoberta](/sccm/core/servers/deploy/configure/configure-discovery-methods#BKMK_ConfigADForestDisc).  



##  <a name="bkmk_aboutGroup"></a> Descoberta de grupos do Active Directory  
**Configurável:** Sim  

**Habilitado por padrão:** Não  

**Contas** que você pode usar para executar esse método:  

-   **Conta de descoberta de grupos do Active Directory** (definida pelo usuário)  

-   **Conta de computador** do servidor do site  

> [!TIP]  
>  Além das informações nesta seção, confira [Recursos comuns da descoberta de grupos, sistemas e usuários do Active Directory](#bkmk_shared).  

Use esse método para pesquisar o Active Directory Domain Services a fim de identificar:  

-   Grupos de segurança locais, globais e universais.  

-   A associação de grupos.  

-   Informações limitadas sobre computadores e usuários associados a grupos, mesmo quando esses computadores e usuários não tiverem sido descobertos anteriormente por outro método de descoberta.  

Este método de descoberta tem como finalidade identificar grupos e as relações de grupos de membros de grupos. Por padrão, somente grupos de segurança são descobertos. Se você também deseja descobrir a associação de grupos de distribuição, precisa marcar a caixa de seleção da opção **Descobrir a associação de grupos de distribuição** na guia **Opção** da caixa de diálogo **Propriedades de descoberta de grupos do Active Directory**.  

A descoberta de grupos do Active Directory não dá suporte a atributos estendidos do Active Directory que podem ser identificados com a descoberta de sistemas ou a descoberta de usuários do Active Directory. Como esse método de descoberta não é otimizado para descobrir recursos de computadores e usuários, considere a possibilidade de executar esse método de descoberta depois de executar a descoberta de sistemas e a descoberta de usuários do Active Directory. Essa sugestão se deve ao fato de esse método criar um DDR (registro dos dados de descoberta) completo para os grupos, mas apenas um DDR limitado para os computadores e usuários que são membros de grupos.  

Você pode configurar os seguintes escopos de descoberta que controlam como esse método pesquisa informações:  

-   **Localização**: use um local, se você quiser pesquisar um ou mais contêineres do Active Directory. Essa opção de escopo dá suporte a uma pesquisa recursiva dos contêineres especificados do Active Directory. Esse processo pesquisa cada contêiner filho no contêiner especificado. Ele continua até que não sejam mais encontrados contêineres filho.  

-   **Grupos**: use grupos se desejar pesquisar um ou mais grupos específicos do Active Directory. Você pode configurar o **Domínio do Active Directory** para usar o domínio e a floresta padrão ou para limitar a pesquisa a um controlador de domínio específico. Além disso, você pode especificar um ou mais grupos para a pesquisa. Se você não especificar pelo menos um grupo, todos os grupos encontrados no local especificado do **Domínio do Active Directory** serão pesquisados.  

> [!CAUTION]  
>  Ao configurar um escopo de descoberta, selecione apenas os grupos a serem descobertos. Essa recomendação é feita porque a descoberta de grupos do Active Directory tenta descobrir cada membro de cada grupo no escopo da descoberta. A descoberta de grupos grandes pode exigir uso extensivo de largura de banda e recursos do Active Directory.  

> [!NOTE]  
>  Antes de criar coleções baseadas nos atributos estendidos do Active Directory, e para garantir resultados de descoberta precisos para computadores e usuários, execute a descoberta de sistemas ou a descoberta de usuários do Active Directory, dependendo do que deseja descobrir.  

As ações da descoberta de grupos do Active Directory são registradas no arquivo **adsgdis.log** e na pasta **&lt;InstallationPath\>\LOGS** no servidor do site.  

Para obter mais informações sobre como configurar esse método de descoberta, consulte [Configurar métodos de descoberta](/sccm/core/servers/deploy/configure/configure-discovery-methods#BKMK_ConfigADDiscGeneral).  



##  <a name="bkmk_aboutSystem"></a> Descoberta de sistemas do Active Directory  
**Configurável:** Sim  

**Habilitado por padrão:** Não  

**Contas** que você pode usar para executar esse método:  

-   **Conta de descoberta de sistemas do Active Directory** (definida pelo usuário)  

-   **Conta de computador** do servidor do site  

> [!TIP]  
>  Além das informações nesta seção, confira [Recursos comuns da descoberta de grupos, sistemas e usuários do Active Directory](#bkmk_shared).  

Use esse método de descoberta para pesquisar os locais do Active Directory Domain Services especificados para recursos do computador que podem ser usados para criar coleções e consultas. Você também pode instalar o cliente do Configuration Manager em um dispositivo descoberto usando a instalação do cliente por push.  

Por padrão, esse método descobre informações básicas sobre o computador, incluindo os seguintes atributos:  

-   Nome do computador  

-   Sistema operacional e versão  

-   Nome do contêiner do Active Directory  

-   Endereço IP  

-   Site do Active Directory  

-   Carimbo de data/hora do último logon  

Para criar com êxito um DDR para um computador, a descoberta de sistemas do Active Directory deve poder identificar a conta do computador e resolver com êxito o nome do computador para um endereço IP.  

Na caixa de diálogo **Propriedades da Descoberta de Sistemas do Active Directory** na guia **Atributos do Active Directory**, exiba a lista completa dos atributos de objeto padrão descobertos. Você também pode configurar o método para descobrir os atributos adicionais (estendidos).  

As ações da descoberta de sistemas do Active Directory são registradas no arquivo **adsysdis.log** e na pasta **&lt;InstallationPath\>\LOGS** no servidor do site.  

Para obter mais informações sobre como configurar esse método de descoberta, consulte [Configurar métodos de descoberta](/sccm/core/servers/deploy/configure/configure-discovery-methods#BKMK_ConfigADDiscGeneral).  



##  <a name="bkmk_aboutUser"></a> Descoberta de Usuário do Active Directory  
**Configurável:** Sim  

**Habilitado por padrão:** Não  

**Contas** que você pode usar para executar esse método:  

-   **Conta de descoberta de usuários do Active Directory** (definida pelo usuário)  

-   **Conta de computador** do servidor do site  

> [!TIP]  
>  Além das informações nesta seção, confira [Recursos comuns da descoberta de grupos, sistemas e usuários do Active Directory](#bkmk_shared).  

Use esse método de descoberta para pesquisar o Active Directory Domain Services a fim de identificar contas de usuário e atributos associados. Por padrão, esse método descobre informações básicas sobre a conta do usuário, incluindo os seguintes atributos:  

-   Nome de usuário  

-   Nome de usuário exclusivo (inclui o nome de domínio)  

-   Domain  

-   Nomes de contêineres do Active Directory  

Na caixa de diálogo **Propriedades da Descoberta de Usuários do Active Directory** na guia **Atributos do Active Directory**, exiba a lista padrão completa dos atributos de objeto descobertos. Você também pode configurar o método para descobrir os atributos adicionais (estendidos).

As ações da descoberta de usuários do Active Directory são registradas no arquivo **adusrdis.log** e na pasta **&lt;InstallationPath\>\LOGS** no servidor do site.  

Para obter mais informações sobre como configurar esse método de descoberta, consulte [Configurar métodos de descoberta](/sccm/core/servers/deploy/configure/configure-discovery-methods#BKMK_ConfigADDiscGeneral).  



## <a name="azureaddisc"></a> Descoberta de Usuários do Azure Active Directory
Use a descoberta de usuários do Azure AD (Azure Active Directory) para pesquisar sua assinatura do Azure AD em busca de usuários com uma identidade de nuvem moderna. A descoberta de usuários do Azure AD pode encontrar os seguintes atributos:  
-   objectId
-   displayName
-   mail
-   mailNickname
-   onPremisesSecurityIdentifier
-   userPrincipalName
-   AAD tenantID

Esse método dá suporte à sincronização completa e delta de atributos de usuário do Azure AD. Essas informações podem ser usadas junto com dados de descoberta coletados de outros métodos de descoberta.

As ações para a descoberta de usuários do Azure AD são registradas no arquivo **SMS_AZUREAD_DISCOVERY_AGENT.log** no servidor do site de nível superior da hierarquia.

Para configurar a descoberta de usuários do Azure AD, consulte [Configurar os Serviços do Azure](/sccm/core/servers/deploy/configure/Azure-services-wizard) para o Gerenciamento de Nuvem. Para saber mais sobre como configurar esse método de descoberta, confira [Configurar a Descoberta de Usuário do Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc).



##  <a name="bkmk_aboutHeartbeat"></a> Descoberta de pulsação  
**Configurável:** Sim  

**Habilitado por padrão:** Sim  

**Contas** que você pode usar para executar esse método:  

-   **Conta de computador** do servidor do site  

A descoberta de pulsação é diferente dos outros métodos de descoberta do Configuration Manager. Ela é habilitada por padrão e executada em cada cliente do computador (em vez de em um servidor de sites) para criar um DDR. Para clientes de dispositivos móveis, esse DDR é criado pelo ponto de gerenciamento que está sendo usado pelo cliente do dispositivo móvel. Para ajudar a manter o registro do banco de dados de clientes do Configuration Manager, não desabilite a descoberta de pulsação. Além de manter o registro de banco de dados, esse método pode forçar a descoberta de um computador como um novo registro de recurso. Ele também pode popular novamente o registro de banco de dados de um computador que foi excluído do banco de dados.  

A descoberta de pulsação é executada de acordo com um agendamento configurado para todos os clientes na hierarquia. O agendamento padrão para a descoberta de pulsação é definido como um intervalo de sete dias. Se você alterar o intervalo da descoberta de pulsação, garanta que ele seja executado com mais frequência do que a tarefa de manutenção do site **Excluir Dados Antigos de Descoberta**. Essa tarefa exclui os registros inativos do cliente do banco de dados do site. Você pode configurar a tarefa **Excluir Dados Antigos de Descoberta** somente para sites primários. 

Invoque também a descoberta de pulsação manualmente em um cliente específico. Execute o **Ciclo de Coleta de Dados de Descoberta** na guia **Ação** do painel de controle do cliente do Configuration Manager.  

Quando a Descoberta de Pulsação é executada, ela cria um DDR que contém as informações atuais do cliente. Em seguida, o cliente copia esse arquivo pequeno (aproximadamente 1 KB de tamanho) para um ponto de gerenciamento, para que ele possa ser processado por um site primário. O arquivo contém as seguintes informações:  

-   Local de rede  

-   Nome NetBIOS  

-   Versão do agente cliente  

-   Detalhes do status operacional  

A descoberta de pulsação é o único método de descoberta que fornece detalhes sobre o status de instalação do cliente. Isso é feito atualizando-se o atributo de cliente do recurso do sistema para definir um valor igual a **Sim**.  

> [!NOTE]  
>  Mesmo quando a descoberta de pulsação é desabilitada, os DDRs ainda são criados e enviados para clientes do dispositivo móvel ativo. Esse comportamento garante que a tarefa para **Excluir Dados Antigos de Descoberta** não afete os dispositivos móveis ativos. Quando a tarefa **Excluir Dados Antigos de Descoberta** exclui um registro de banco de dados de um dispositivo móvel, ela também revoga o certificado do dispositivo. Essa ação impede que o dispositivo móvel se conecte aos pontos de gerenciamento.  

As ações de descoberta de pulsação são registradas nos seguintes locais:  

-   Para clientes do computador, as ações da Descoberta de Pulsação são registradas no cliente no arquivo **InventoryAgent.log** na pasta *%Windir%\CCM\Logs*.  

-   Para clientes de dispositivos móveis, as ações da Descoberta de Pulsação são registradas no arquivo **DMPRP.log** na pasta *%Program Files%\CCM\Logs* do ponto de gerenciamento que o cliente do dispositivo móvel usa.  

Para obter mais informações sobre como configurar esse método de descoberta, consulte [Configurar métodos de descoberta](/sccm/core/servers/deploy/configure/configure-discovery-methods#BKMK_ConfigHBDisc).  



##  <a name="bkmk_aboutNetwork"></a> Descoberta de Rede  
**Configurável:** Sim  

**Habilitado por padrão:** Não  

**Contas** que você pode usar para executar esse método:  

-   **Conta de computador** do servidor do site  

Use esse método para descobrir a topologia da rede e para descobrir dispositivos na sua rede que têm um endereço IP. A descoberta de rede pesquisa os recursos habilitados para IP na rede consultando as seguintes entidades: 
- Servidores que executam uma implementação da Microsoft do DHCP
- Caches do ARP (Protocolo da resolução de endereço) em roteadores de rede
- dispositivos habilitados para SNMP
- Domínios do Active Directory  

Antes de poder usar a descoberta de rede, você deve especificar o *nível* de descoberta a ser executado. Além disso, é possível configurar um ou mais mecanismos de descoberta que permitem que a descoberta de rede consulte segmentos de rede ou dispositivos. Você também pode definir configurações que ajudam a controlar ações de descoberta na rede. Finalmente, você pode definir um ou mais agendamentos para quando a descoberta de rede é executada.  

Para esse método descobrir um recurso com êxito, a descoberta de rede deve identificar o endereço IP e a máscara de sub-rede do recurso. Os métodos a seguir são usados para identificar a máscara de sub-rede de um objeto:  

-   **Cache ARP do roteador:** A Descoberta de Rede consulta o cache ARP de um roteador para localizar informações de sub-rede. Normalmente, os dados do cache ARP de um roteador têm um curto período de vida. Portanto, quando a descoberta de rede consulta o cache ARP, este pode não conter mais as informações sobre o objeto solicitado.  

-   **DHCP:** A Descoberta de Rede consulta cada servidor DHCP especificado para descobrir os dispositivos para os quais o servidor DHCP forneceu concessão. A Descoberta de Rede oferece suporte somente a servidores DHCP que executam a implementação de DHCP da Microsoft.  

-   **Dispositivo SNMP:** a Descoberta de Rede pode consultar diretamente um dispositivo SNMP. Para a Descoberta de Rede consultar um dispositivo, o dispositivo deve ter um agente SNMP local instalado. Também configure a descoberta de rede para usar o nome da comunidade usado pelo agente SNMP.  

Quando a descoberta identifica um objeto de IP endereçável e pode determinar a máscara de sub-rede do objeto, ela cria um DDR para esse objeto. Como tipos diferentes de dispositivos se conectam à rede, a descoberta de rede descobre recursos que não dão suporte ao cliente do Configuration Manager. Por exemplo, dispositivos que podem ser detectados, mas não gerenciados incluem impressoras e roteadores.  

A descoberta de rede pode retornar vários atributos como parte do registro de descoberta criado. Esses atributos incluem:  

-   Nome NetBIOS  

-   Endereços IP  

-   Domínio de recurso  

-   Funções do sistema  

-   Nome da comunidade SNMP  

-   Endereços MAC  

A atividade da descoberta de rede é registrada no arquivo **Netdisc.log** na pasta *&lt;CaminhodeInstalação\>\Logs* no servidor de sites que executa a descoberta.  

 Para obter mais informações sobre como configurar esse método de descoberta, consulte [Configurar métodos de descoberta](/sccm/core/servers/deploy/configure/configure-discovery-methods#BKMK_ConfigNetworkDisc).  

> [!NOTE]  
>  Redes complexas e conexões de largura de banda baixa podem causar lentidão na execução da descoberta de rede e gerar tráfego de rede significativo. Como prática recomendada, execute a descoberta de rede somente quando os outros métodos de descoberta não conseguirem localizar os recursos que você deve descobrir. Por exemplo, use a descoberta de rede se você deve descobrir computadores do grupo de trabalho. Os computadores do grupo de trabalho não são descobertos por outros métodos de descoberta.  

###  <a name="BKMK_NetDiscLevels"></a> Níveis de descoberta de rede  
Ao configurar a descoberta de rede, especifique um dos três níveis de descoberta:  

|Nível de descoberta|Detalhes|  
|------------------------|-------------|  
|Topologia|Este nível descobre sub-redes e roteadores, mas não identifica uma máscara de sub-rede para objetos.|  
|Topologia e cliente|Além da topologia, este nível descobre clientes potenciais, como computadores, e recursos, como impressoras e roteadores. Esse nível de descoberta tenta identificar a máscara de sub-rede de objetos encontrados.|  
|Topologia, cliente e sistema operacional do cliente|Além da topologia e dos clientes potenciais, este nível tenta descobrir o nome e a versão do sistema operacional do computador. Esse nível usa o navegador do Windows e chamadas do sistema de rede do Windows.|  

 Com cada nível incremental, a descoberta de rede aumenta sua atividade e o uso de largura de banda de rede. Considere o tráfego de rede que pode ser gerado antes de habilitar todos os aspectos da descoberta de rede.  

 Por exemplo, ao usar a descoberta de rede pela primeira vez, você pode iniciar somente o nível de topologia para identificar sua infraestrutura de rede. Em seguida, reconfigure a descoberta de rede para descobrir objetos e os sistemas operacionais de seus dispositivos. Também é possível definir as configurações que limitam a descoberta de rede a um intervalo específico de segmentos de rede. Dessa forma, você descobre os objetos nos locais de rede necessários e evita o tráfego de rede desnecessário. Esse processo também permite a descoberta de objetos em roteadores de borda ou fora da rede.  

###  <a name="BKMK_NetDiscOptions"></a> Opções de descoberta de rede  
Para habilitar a descoberta de rede para pesquisar dispositivos endereçáveis por IP, configure uma ou mais dessas opções.  

> [!NOTE]  
>  A descoberta de rede é executada no contexto da conta de computador do servidor do site que executa a descoberta. Se a conta de computador não tiver permissões para um domínio não confiável, as configurações do servidor DHCP e do domínio poderão falhar na descoberta de recursos.  

#### <a name="dhcp"></a>DHCP  

Especifique cada servidor DHCP que você deseja que a descoberta de rede consulte. (A descoberta de rede dá suporte somente a servidores DHCP que executam a implementação de DHCP da Microsoft.)  

-   A descoberta de rede recupera as informações por meio de chamadas de procedimento remoto para o banco de dados no servidor DHCP.  

-   A descoberta de rede pode consultar servidores DHCP de 32 e 64 bits para obter uma lista de dispositivos que estão registrados com cada servidor.  

-   Para que a descoberta de rede consulte um servidor DHCP com êxito, a conta de computador do servidor que executa a descoberta deve ser um membro do grupo de usuários DHCP no servidor DHCP. Por exemplo, esse nível de acesso existe quando uma das seguintes afirmações é verdadeira:  

    -   O servidor DHCP especificado é o servidor DHCP do servidor que executa a descoberta.  

    -   O computador que executa a descoberta e o servidor DHCP estão no mesmo domínio.  

    -   Existe uma relação de confiança bidirecional entre o computador que executa a descoberta e o servidor DHCP.  

    -   O servidor do site é um membro do grupo Usuários DHCP.  

-   Quando a descoberta de rede enumera um servidor DHCP, ela nem sempre descobre endereços IP estáticos. A descoberta de rede não localiza endereços IP que fazem parte de um intervalo excluído de endereços IP no servidor DHCP. Também não descobre endereços IP reservados para atribuição manual.  

#### <a name="domains"></a>Domínios  

Especifique cada domínio que você deseja que a descoberta de rede consulte.  

-   A conta de computador do servidor do site que executa a descoberta deve ter permissões para ler os controladores de domínio em cada domínio específico.  

-   Para descobrir computadores no domínio local, é necessário habilitar o serviço Pesquisador de Computadores em, pelo menos, um computador. Esse computador deve estar na mesma sub-rede do servidor do site que executa a descoberta de rede.  

-   A descoberta de rede pode descobrir algum computador que você pode exibir do seu servidor do site ao procurar na rede.  

-   A descoberta de rede recupera o endereço IP. Ela então usa uma solicitação de eco do protocolo ICMP para executar ping de cada dispositivo encontrado. O comando **ping** ajuda a determinar quais computadores estão ativos no momento.  

#### <a name="snmp-devices"></a>Dispositivos SNMP  

Especifique cada dispositivo SNMP que você deseja que a descoberta de rede consulte.  

-   A descoberta de rede recupera o valor ipNetToMediaTable de algum dispositivo SNMP que responde à consulta. Esse valor retorna matrizes de endereços IP que são computadores cliente ou outros recursos, como impressoras, roteadores ou outros dispositivos de IP endereçável.  

-   Para consultar um dispositivo, você deve especificar o endereço IP ou nome NetBIOS do dispositivo.  

-   Configure a descoberta de rede para que ela use o nome da comunidade do dispositivo ou o dispositivo rejeitará a consulta baseada em SNMP.  


###  <a name="BKMK_LimitNetDisc"></a> Limitação da descoberta de rede  
Quando a descoberta de rede consulta um dispositivo SNMP na borda da rede, ela pode identificar informações sobre sub-redes e dispositivos SNMP que estão fora da rede imediata. Use as informações a seguir para limitar a descoberta de rede configurando os dispositivos SNMP com os quais a descoberta pode se comunicar e especificando os segmentos de rede a serem consultados.  

#### <a name="subnets"></a>Sub-redes  

Configure as sub-redes que a Descoberta de Rede consulta quando usa as opções SNMP e DHCP. Somente as sub-redes habilitadas são pesquisadas por essas duas opções.  

Por exemplo, uma solicitação DHCP pode retornar dispositivos de locais em toda a rede. Se você deseja descobrir somente dispositivos em determinada sub-rede, especifique e habilite essa sub-rede na guia **Sub-redes** da caixa de diálogo **Propriedades da Descoberta de Rede**. A especificação e habilitação de sub-redes limitam as operações futuras de descoberta de DHCP e SNMP para essas sub-redes.  

> [!NOTE]  
>  As configurações de sub-rede não limitam os objetos que a opção de descoberta **Domínios** descobre.  

#### <a name="snmp-community-names"></a>Nomes de comunidade SNMP  

Para permitir que a descoberta de rede consulte um dispositivo SNMP com êxito, configure a descoberta de rede com o nome da comunidade do dispositivo. Se a Descoberta de Rede não for configurada usando o nome de comunidade do dispositivo SNMP, o dispositivo rejeitará a consulta.  

#### <a name="maximum-hops"></a>Máximo de saltos  

Ao se configurar o número máximo de saltos do roteador, limita-se o número de segmentos de rede e roteadores que a Descoberta de Rede pode consultar usando SNMP.  

O número de saltos configurado limita o número de dispositivos adicionais e segmentos de rede que a Descoberta de Rede pode consultar.  

Por exemplo, uma descoberta somente de topologia com **0** (zero) salto de roteador descobre a sub-rede em que o servidor original reside. Também inclui os roteadores dessa sub-rede.  

O diagrama a seguir mostra o que a descoberta de rede somente de topologia encontra quando executada no Servidor 1 com 0 salto de roteador especificado: a sub-rede D e o Roteador 1.  

 ![Imagem de descoberta sem saltos do roteador](media/Disc-0.gif)  

 O seguinte diagrama mostra o que a descoberta de rede de topologia e cliente encontra quando executada no Servidor 1 com 0 salto de roteador especificado: a sub-rede D e o Roteador 1 e todos os clientes potenciais na sub-rede D.  

 ![Imagem de descoberta com um salto do roteador](media/Disc-1.gif)  

 Para ter uma ideia melhor de como saltos adicionais de roteador podem aumentar a quantidade de recursos de rede descobertos, considere a seguinte rede:  

 ![Imagem de descoberta com dois saltos do roteador](media/Disc-2.gif)  

 A execução de uma descoberta de rede somente de topologia no Servidor 1 com um salto de roteador descobre as seguintes entidades:  

-   Roteador 1 e sub-rede 10.1.10.0 (encontrados sem saltos)  

-   Sub-redes 10.1.20.0 e 10.1.30.0, sub-rede A e Roteador 2 (encontrados no primeiro salto)  

> [!WARNING]  
>  Cada aumento do número de saltos de roteador pode aumentar significativamente o número de recursos que podem ser descobertos e aumentar a largura de banda da rede que a Descoberta de Rede usa.  



##  <a name="bkmk_aboutServer"></a> Descoberta de Servidor  
**Configurável:** Não  

Além dos métodos de descoberta configuráveis pelo usuário, o Configuration Manager usa um processo chamado **Descoberta de Servidor** (SMS_WINNT_SERVER_DISCOVERY_AGENT). Esse método de descoberta cria registros de recursos para computadores que são sistemas de sites, como um computador configurado como ponto de gerenciamento.  



##  <a name="bkmk_shared"></a> Recursos comuns da descoberta de grupos, sistemas e usuários do Active Directory  
Esta seção fornece informações sobre os recursos que são comuns aos seguintes métodos de descoberta:  

-   Descoberta de grupos do Active Directory  

-   Descoberta de sistemas do Active Directory  

-   Descoberta de Usuário do Active Directory  

> [!NOTE]  
>  As informações nesta seção não se aplicam à descoberta de florestas do Active Directory.  

Esses três métodos de descoberta são semelhantes na configuração e na operação. Eles podem descobrir computadores, usuários e informações sobre associações de grupo de recursos armazenados no Active Directory Domain Services. O processo de descoberta é gerenciado por um agente de descoberta. O agente é executado no servidor do site em cada site em que a descoberta está configurada para ser executada. Você pode configurar cada um desses métodos de descoberta para pesquisar um ou mais locais do Active Directory como instâncias do local na floresta local ou em florestas remotas.  

Quando a descoberta pesquisa recursos em uma floresta não confiável, o agente de descoberta deve ser capaz de resolver o seguinte para ter êxito:  

-   Para descobrir um recurso de computador com a descoberta de sistemas do Active Directory, o agente de descoberta deve ser capaz de resolver o FQDN do recurso. Se ele não puder resolver o FQDN, ele tentará resolver o recurso pelo seu nome NetBIOS.  

-   Para descobrir um recurso do grupo ou do usuário com a descoberta de usuários do Active Directory ou a descoberta de grupos do Active Directory, o agente de descoberta deve ser capaz de resolver o FQDN do nome do controlador de domínio especificado para o local do Active Directory.  

Para cada local especificado, é possível configurar opções de pesquisa individuais, como habilitar uma pesquisa recursiva dos locais de contêineres filho do Active Directory. Também é possível configurar uma conta exclusiva para usar ao pesquisar esse local. Essa conta proporciona flexibilidade na configuração de um método de descoberta em um site para pesquisa de vários locais do Active Directory em várias florestas. Você não precisa configurar uma única conta que tem permissões em todos os locais.  

Quando cada um desses três métodos de descoberta é executado em um site específico, o servidor de sites do Configuration Manager entra em contato com o controlador de domínio mais próximo na floresta do Active Directory especificada para localizar recursos do Active Directory. O domínio e a floresta podem estar em qualquer modo compatível com o Active Directory. A conta atribuída a cada instância do local deve ter permissão de acesso de **Leitura** para os locais especificados do Active Directory.

A descoberta pesquisa os locais especificados por objetos e tenta coletar informações sobre eles. Um DDR é criado quando é possível identificar informações suficientes sobre um recurso. As informações necessárias variam de acordo com o método de descoberta usado.  

Se você configurar a execução do mesmo método de descoberta em sites do Configuration Manager diferentes para aproveitar a consulta de servidores locais do Active Directory, poderá configurar cada site com um conjunto exclusivo de opções de descoberta. Como os dados de descoberta são compartilhados com cada site na hierarquia, evite a sobreposição entre essas configurações para descobrir de forma eficiente cada recurso uma única vez.

Em ambientes menores, considere a possibilidade de executar cada método de descoberta em um único site na hierarquia. Essa configuração reduz a sobrecarga administrativa e o potencial de várias ações de descoberta para redescobrir os mesmos recursos. Ao minimizar a quantidade de sites que executa a descoberta, você reduz a largura de banda da rede geral utilizada pela descoberta. Também pode reduzir a quantidade total de DDRs criados e que devem ser processados pelos servidores do seu site.  

Muitas das configurações de método de descoberta são autoexplicativas. Use as seções a seguir para obter mais informações sobre as opções de descoberta que podem requerer informações adicionais antes de configurá-las.  

As opções a seguir estão disponíveis para uso com vários métodos de descoberta do Active Directory:  

-   [Descoberta de deltas](#bkmk_delta)  

-   [Filtrar registros obsoletos do computador por logon de domínio](#bkmk_stalelogon)  

-   [Filtrar registros obsoletos por senha do computador](#bkmk_stalepassword)  

-   [Pesquisar atributos personalizados do Active Directory](#bkmk_customAD)  


###  <a name="bkmk_delta"></a> Descoberta de deltas  
Disponível para:  

-   Descoberta de grupos do Active Directory  

-   Descoberta de sistemas do Active Directory  

-   Descoberta de Usuário do Active Directory  

A descoberta de deltas não é um método de descoberta independente, mas uma opção disponível para os métodos de descoberta aplicáveis. A descoberta de deltas pesquisa atributos específicos do Active Directory quanto às alterações que foram feitas desde o último ciclo de descoberta completo do método de descoberta aplicável. As alterações de atributo são enviadas ao banco de dados do Configuration Manager para atualizar o registro de descoberta do recurso.  

Por padrão, a descoberta de deltas é executada em um ciclo de cinco minutos. Esse agendamento é muito mais frequente do que o agendamento típico de um ciclo de descoberta completo. Esse ciclo frequente é possível porque a descoberta de deltas usa menos recursos de rede e servidor do site do que o ciclo de descoberta completo. Ao usar a descoberta de deltas, você pode reduzir a frequência do ciclo de descoberta completo para esse método de descoberta.  

As alterações a seguir são as mais comuns detectadas pela descoberta de deltas:  

-   Novos computadores ou usuários adicionados ao Active Directory  

-   Alterações nas informações básicas do computador e do usuário  

-   Novos computadores ou usuários que são adicionados a um grupo  

-   Computadores ou usuários que são removidos de um grupo  

-   Alterações em objetos do grupo de sistemas  

Embora a descoberta de deltas possa detectar novos recursos e alterações na associação do grupo, não pode detectar quando um recurso foi excluído do Active Directory. Os DDRs criados pela descoberta de deltas são processados de maneira semelhante aos DDRs criados por um ciclo de descoberta completo.  

Você configura a descoberta de deltas na guia **Agendamento de Sondagem** , nas propriedades de cada método de descoberta.  


###  <a name="bkmk_stalelogon"></a> Filtrar registros obsoletos do computador por logon de domínio  
Disponível para:  

-   Descoberta de grupos do Active Directory  

-   Descoberta de sistemas do Active Directory  

Configure a descoberta para excluir computadores com um registro de computador obsoleto. Essa exclusão baseia-se no último logon de domínio do computador. Quando essa opção estiver habilitada, a descoberta de sistemas do Active Directory avaliará cada computador que identificar. A descoberta de grupos do Active Directory avalia cada computador membro de um grupo descoberto.  

Para usar essa opção:  

-   Os computadores devem ser configurados para atualizar o atributo **lastLogonTimeStamp** no Active Directory Domain Services.  

-   O nível funcional de domínio do Active Directory deve ser definido para o Windows Server 2003 ou posterior.  

Ao definir o tempo após o último logon que você deseja usar para essa configuração, considere o intervalo de replicação entre controladores de domínio.  

Configure a filtragem na guia **Opção** nas caixas de diálogo **Propriedades de descoberta de sistemas do Active Directory** e **Propriedades de descoberta de grupos do Active Directory**. Escolha **Descobrir somente computadores que fizeram logon em um domínio em determinado período**.  

> [!WARNING]  
>  Ao configurar esse filtro e a opção **Filtrar registros obsoletos por senha do computador**, a descoberta exclui os computadores que atendem aos critérios de um dos filtros.  


###  <a name="bkmk_stalepassword"></a> Filtrar registros obsoletos por senha do computador  
Disponível para:  

-   Descoberta de grupos do Active Directory  

-   Descoberta de sistemas do Active Directory  

Configure a descoberta para excluir computadores com um registro de computador obsoleto. Essa exclusão baseia-se na última atualização de senha da conta de computador pelo computador. Quando essa opção estiver habilitada, a descoberta de sistemas do Active Directory avaliará cada computador que identificar. A descoberta de grupos do Active Directory avalia cada computador membro de um grupo descoberto.  

Para usar essa opção:  

-   Os computadores devem ser configurados para atualizar o atributo **pwdLastSet** no Active Directory Domain Services.  

Quando estiver configurando essa opção, considere o intervalo das atualizações nesse atributo. Considere também o intervalo de replicação entre controladores de domínio.  

Configure a filtragem na guia **Opção** nas caixas de diálogo **Propriedades de descoberta de sistemas do Active Directory** e **Propriedades de descoberta de grupos do Active Directory**. Escolha **Descobrir somente computadores que atualizaram suas senhas da conta de computador em determinado período**.  

> [!WARNING]  
>  Ao configurar esse filtro e a opção **Filtrar registros obsoletos por logon de domínio**, a descoberta exclui os computadores que atendem aos critérios de um dos filtros.  


###  <a name="bkmk_customAD"></a> Pesquisar atributos personalizados do Active Directory  
 Disponível para:  

-   Descoberta de sistemas do Active Directory  

-   Descoberta de Usuário do Active Directory  

Cada método de descoberta dá suporte a uma lista exclusiva de atributos do Active Directory que podem ser descobertos.  

Você pode exibir e configurar a lista de atributos personalizados na guia **Atributos do Active Directory** nas caixas de diálogo **Propriedades da descoberta de sistemas do Active Directory** e **Propriedades da descoberta de usuários do Active Directory**.  
