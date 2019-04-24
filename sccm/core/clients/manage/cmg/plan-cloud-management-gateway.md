---
title: Plano para o gateway de gerenciamento de nuvem
titleSuffix: Configuration Manager
description: Planeje e projete o CMG (gateway de gerenciamento de nuvem) para simplificar o gerenciamento de clientes baseados na Internet.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f9057a2126a548ebb8706e905b86edb702f0ff35
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59673676"
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Planejar o gateway de gerenciamento de nuvem no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*
 
<!--1101764-->
O CMG (gateway de gerenciamento de nuvem) fornece uma maneira simples de gerenciar clientes do Configuration Manager na Internet. Implantando o CMG como um serviço de nuvem no Microsoft Azure, você pode gerenciar clientes tradicionais que usam um perfil móvel na Internet sem infraestrutura adicional. Você também não precisa expor sua infraestrutura local para a Internet. 

> [!Tip]  
> Esse recurso foi introduzido na versão 1610 como um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1802, esse recurso deixa de ser um recurso de pré-lançamento.  


> [!Note]  
> O Configuration Manager não habilita esse recurso opcional por padrão. É necessário habilitar esse recurso antes de usá-lo. Para obter mais informações, consulte [Enable optional features from updates (Habilitar recursos opcionais de atualizações)](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Depois de estabelecer os pré-requisitos, a criação do CMG consiste nas três seguintes etapas no console do Configuration Manager:
1. Implantar o serviço de nuvem do CMG no Azure.
2. Adicionar a função do ponto de conexão do CMG. 
3. Configurar o site e as funções do site para o serviço. Depois de implantados e configurados, os clientes acessam diretamente as funções locais do site, independentemente de estarem na intranet ou na Internet.

Este artigo fornece o conhecimento básico para saber mais sobre o CMG, projetar como ele se ajusta ao ambiente e planejar a implementação. 



## <a name="scenarios"></a>Cenários 

Há vários cenários para os quais um CMG é útil. Os seguintes cenários são alguns dos mais comuns:  

- Gerenciar clientes tradicionais do Windows com a identidade ingressada no domínio do Active Directory. Esses clientes incluem Windows 7, Windows 8.1 e Windows 10. Ele usa certificados PKI para proteger o canal de comunicação. As atividades de gerenciamento incluem:  
    - Atualizações de software e proteção de ponto de extremidade
    - Inventário e status do cliente
    - Configurações de conformidade
    - Distribuição de software para o dispositivo
    - Sequência de tarefas de atualização in-loco do Windows 10 (a partir da versão 1802)

- Gerenciar clientes tradicionais do Windows 10 com a identidade moderna, ingressados em domínio de nuvem pura ou híbrida com o Azure AD (Azure Active Directory). Os clientes usam o Azure AD para autenticação, em vez de certificados PKI. O uso do Azure AD tem configuração e manutenção mais simples comparado aos sistemas de PKI mais complexos. As atividades de gerenciamento são as mesmas que no primeiro cenário, bem como:  
    - Distribuição de software para o usuário  

- Instalar o cliente do Configuration Manager em dispositivos Windows 10 pela Internet. O uso do Azure AD permite que o dispositivo se autentique no CMG para o registro de cliente e atribuição. Instale o cliente manualmente ou use outro método de distribuição de software, como o Microsoft Intune.  

- Novo provisionamento de dispositivos com cogerenciamento. O CMG não é necessário para o cogerenciamento. Ele ajuda a concluir um cenário de ponta a ponta para novos dispositivos que envolvem o Windows AutoPilot, Azure AD, Microsoft Intune e Configuration Manager.  

### <a name="specific-use-cases"></a>Casos de uso específicos
Entre esses cenários, os seguintes casos de uso de dispositivo específicos podem ser aplicáveis:

- Dispositivos móveis, como laptops  

- Dispositivos remotos/da filial são mais baratos e mais eficientes de serem gerenciados pela Internet em uma WAN ou por meio de uma VPN.  

- Fusões e aquisições, em que pode ser mais fácil ingressar dispositivos no Azure AD e gerenciá-los por meio de um CMG.  

> [!Important]
> Por padrão, todos os clientes recebem uma política para um CMG e começam a usá-la quando se tornam baseados na Internet. Dependendo do cenário e do caso de uso aplicáveis à sua organização, talvez você precise definir o escopo de uso do CMG. Para obter mais informações, consulte a configuração de cliente [Permitir que os clientes usem um gateway de gerenciamento de nuvem](/sccm/core/clients/deploy/about-client-settings#enable-clients-to-use-a-cloud-management-gateway).


## <a name="topology-design"></a>Design da topologia

### <a name="cmg-components"></a>Componentes do CMG
A implantação e a operação do CMG incluem os seguintes componentes:  

- O **serviço de nuvem do CMG** do Azure autentica e encaminha as solicitações de cliente do Configuration Manager para o ponto de conexão do CMG.  
 
- A função do sistema de sites do **ponto de conexão do CMG** permite uma conexão consistente e de alto desempenho da rede local com o serviço do CMG no Azure. Ele também publica configurações no CMG, incluindo informações de conexão e configurações de segurança. O ponto de conexão do CMG encaminha as solicitações de cliente do CMG para funções locais, de acordo com os mapeamentos de URL.

- A função do sistema de sites do [**ponto de conexão de serviço**](/sccm/core/servers/deploy/configure/about-the-service-connection-point) executa o componente do gerenciador de serviço de nuvem, que manipula todas as tarefas de implantação do CMG. Além disso, ele monitora e reporta informações de integridade e de registro em log do serviço do Azure AD. Verifique se o ponto de conexão do serviço está no [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes).  

- A função do sistema de sites do **ponto de gerenciamento** atende às solicitações do cliente de modo habitual.  

- A função do sistema de sites do **ponto de atualização de software** atende às solicitações do cliente de modo habitual.  

- Os **clientes baseados na Internet** se conectam ao CMG para acessar os componentes locais do Configuration Manager.

- O CMG usa um serviço Web **HTTPS baseado em certificado** para ajudar a proteger a comunicação de rede com clientes.  

- Os clientes baseados na Internet usam **certificados PKI ou o Azure AD** para identidade e autenticação.  

- Um [**ponto de distribuição na nuvem**](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) fornece conteúdo para clientes baseados na Internet, conforme necessário.  

    - Da versão 1806 em diante, um CMG pode também fornecer conteúdo aos clientes. Essa funcionalidade reduz os certificados necessários e o custo das VMs do Azure. Para obter mais informações, consulte [Modificar um CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg).<!--1358651-->  


### <a name="azure-resource-manager"></a>Azure Resource Manager
<!-- 1324735 -->
A partir da versão 1802, você pode criar o CMG usando uma **implantação do Azure Resource Manager**. O [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) é uma plataforma moderna para gerenciar todos os recursos da solução como uma única entidade, chamado [grupo de recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). Ao implantar o CMG com o Azure Resource Manager, o site usa o Azure Active Directory (Azure AD) para autenticar e criar os recursos necessários para a nuvem. Essa implantação modernizada não exige o certificado de gerenciamento do Azure clássico.  

> [!Note]  
> Essa funcionalidade não habilita o suporte para CSPs (Provedores de Serviços de Nuvem) do Azure. A implantação do CMG com o Azure Resource Manager continua usando o serviço de nuvem clássico, ao qual o CSP não dá suporte. Para saber mais, confira os [serviços do Azure disponíveis no CSP do Azure](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-available-services). 

O assistente do CMG ainda fornece a opção para uma **implantação de serviço clássico** usando um certificado de gerenciamento do Azure. Para simplificar a implantação e o gerenciamento de recursos, o uso do modelo de implantação do Azure Resource Manager é recomendado para todas as novas instâncias do CMG. Se possível, reimplante as instâncias CMG existentes por meio do Resource Manager. Para obter mais informações, consulte [Modificar um CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg).

> [!Important]  
> Da versão 1810, a implantação de serviço clássico no Azure é preterida para uso no Configuration Manager. Esta versão é a última a dar suporte à criação dessas implantações do Azure. Essa funcionalidade será removida na primeira versão do Configuration Manager lançada após 1º de julho de 2019. Mova seus pontos de distribuição do CMG e da nuvem para implantações do Azure Resource Manager antes dessa hora. <!--SCCMDocs-pr issue #2993-->  


### <a name="hierarchy-design"></a>Design de hierarquia

Crie o CMG no site de nível superior da hierarquia. Se esse for um site de administração central, crie pontos de conexão do CMG em sites primários filho. O componente de gerenciador de serviço de nuvem está localizado no ponto de conexão de serviço, que também está no site de administração central. Esse design pode compartilhar o serviço em sites primários diferentes, se necessário.

Você pode criar vários serviços do CMG no Azure e criar vários pontos de conexão do CMG. Vários pontos de conexão do CMG fornecem o balanceamento de carga do tráfego do cliente do CMG para as funções locais. Para reduzir a latência da rede, atribua o CMG associado à mesma região geográfica do site primário.

 > [!Note]  
 > Clientes baseados na Internet e o CMG não se enquadram em nenhum grupo de limites.

Outros fatores, como o número de clientes a serem gerenciados, também afetam o design do CMG. Para obter mais informações, consulte [Desempenho e escala](#performance-and-scale).

#### <a name="example-1-standalone-primary-site"></a>Exemplo 1: site primário autônomo

A Contoso tem um site primário autônomo em um datacenter local na sede de Nova York. 
- Eles criam um CMG na região Leste dos EUA do Azure para reduzir a latência da rede. 
- Eles também criam dois pontos de conexão do CMG, ambos vinculados ao único serviço do CMG.  

Como os clientes usam um perfil móvel na Internet, eles se comunicam com o CMG na região do Leste dos EUA do Azure. O CMG encaminha essa comunicação pelos dois pontos de conexão do CMG.

#### <a name="example-2-hierarchy-with-site-specific-cmg"></a>Exemplo 2: hierarquia com CMG específico ao site

A Fourth Coffee tem um site de administração central em um datacenter local na sede de Seattle. Um site primário está no mesmo datacenter e o outro site primário está em seu escritório principal na Europa em Paris. 
- No site de administração central, eles criam dois serviços do CMG:
     - Um CMG na região Oeste dos EUA do Azure.
     - Um CMG na região da Europa Ocidental do Azure.
- No site primário localizado em Seattle, eles criam um ponto de conexão do CMG vinculado ao CMG do Oeste dos EUA.
- No site primário localizado em Paris, eles criam um ponto de conexão do CMG vinculado ao CMG da Europa Ocidental.

Como os clientes localizados em Seattle usam um perfil móvel na Internet, eles se comunicam com o CMG na região do Oeste dos EUA do Azure. O CMG encaminha essa comunicação para o ponto de conexão do CMG localizado em Seattle.

Da mesma forma, como os clientes localizados em Paris usam um perfil móvel na Internet, eles se comunicam com o CMG na região da Europa Ocidental do Azure. O CMG encaminha essa comunicação para o ponto de conexão do CMG localizado em Paris. Quando os usuários de Paris viajam para a sede da empresa em Seattle, seus computadores continuam se comunicando com o CMG na região da Europa Ocidental do Azure. 

 > [!Note]  
 > A Fourth Coffee considerou a possibilidade de criar outro ponto de conexão do CMG no site primário localizado em Paris vinculado ao CMG do Oeste dos EUA. Os clientes de Paris usarão ambos os CMGs, seja qual for sua localização. Embora essa configuração ajude a balancear a carga do tráfego e forneça redundância de serviço, também poderá causar atrasos quando os clientes de Paris se comunicarem com o CMG localizado nos EUA. Os clientes do Configuration Manager não estão cientes de sua região geográfica atualmente e, portanto, não preferem um CMG geograficamente mais próximo. Os clientes usam aleatoriamente um CMG disponível.



## <a name="requirements"></a>requisitos

- Uma **assinatura do Azure** para hospedar o CMG.  

    - Um **administrador do Azure** precisa participar da criação inicial de alguns componentes, dependendo do design. Essa persona não precisa de permissões no Configuration Manager.  

- Pelo menos, um Windows Server local para hospedar o **ponto de conexão do CMG**. Você pode colocalizar essa função com outras funções do sistema de sites do Configuration Manager.  

- O **ponto de conexão de serviço** deve estar no [modo online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes).   

- Um [**certificado de autenticação de servidor**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_serverauth) para o CMG.  

- Se você estiver usando o método clássico de implantação do Azure, precisará usar um [**certificado de gerenciamento do Azure**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_azuremgmt).  

    > [!TIP]  
    > Do Configuration Manager versão 1802 em diante, a Microsoft recomenda o uso do modelo de implantação do **Azure Resource Manager**. Ele não exige esse certificado de gerenciamento. 
    > 
    > O método de implantação clássico foi preterido da versão 1810 em diante.   

- **Outros certificados** podem ser obrigatórios, dependendo do modelo de autenticação e da versão do sistema operacional cliente. Para obter mais informações, consulte [certificados do CMG](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).  

    - Na versão 1802, todos os [**pontos de gerenciamento habilitados para CMG para usar HTTPS**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps) devem ser configurados.  

    - Começando na versão 1806, ao usar a opção do site para **Usar certificados gerados pelo Configuration Manager para o sistema de sites HTTP**, o ponto de gerenciamento pode ser HTTP. Para obter mais informações, confira [HTTP aprimorado](/sccm/core/plan-design/hierarchy/enhanced-http).  


- A integração com o **Azure AD** é necessária para implantações do Azure Resource Manager. Isso também pode ser necessário para clientes do Windows 10. Para obter mais informações, consulte [Configurar serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard).  

- Os clientes devem usar **IPv4**.  



## <a name="specifications"></a>Especificações

- Todas as versões do Windows listadas em [Sistemas operacionais compatíveis com clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) são compatíveis com o CMG.  

- O CMG é compatível apenas com as funções de ponto de gerenciamento e ponto de atualização de software.  

- O CMG não dá suporte a clientes que se comunicam somente com endereços IPv6.<!--495606-->  

- Os pontos de atualização de software que usam um balanceador de carga de rede não funcionam com o CMG. <!--505311-->  

- Da versão 1802 em diante, as implantações do CMG que usam o Modelo de Recurso do Azure não permitem o suporte para CSPs (Provedores de Serviços de Nuvem) do Azure. A implantação do CMG com o Azure Resource Manager continua usando o serviço de nuvem clássico, ao qual o CSP não dá suporte. Para obter mais informações, consulte os [serviços do Azure disponíveis no Azure CSP](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-available-services)  


### <a name="support-for-configuration-manager-features"></a>Suporte para recursos do Configuration Manager
A seguinte tabela lista o suporte do CMG para recursos do Configuration Manager:


|Recurso  |Suporte  |
|---------|---------|
| Atualizações de software     | ![Com suporte](media/green_check.png) |
| Endpoint Protection     | ![Com suporte](media/green_check.png) |
| Inventário de hardware e software     | ![Com suporte](media/green_check.png) |
| Notificações e status do cliente     | ![Com suporte](media/green_check.png) |
| Executar scripts     | ![Com suporte](media/green_check.png) |
| Configurações de conformidade     | ![Com suporte](media/green_check.png) |
| Instalação do cliente<br>(com integração com o Azure AD)     | ![Com suporte](media/green_check.png)  (1706) |
| Distribuição de software (direcionada ao dispositivo)     | ![Com suporte](media/green_check.png) |
| Distribuição de software (direcionada ao usuário, obrigatória)<br>(com integração com o Azure AD)     | ![Com suporte](media/green_check.png)  (1710) |
| Distribuição de software (direcionada ao usuário, disponível)<br>([todos os requisitos](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices)) | ![Com suporte](media/green_check.png)  (1802) |
| Sequência de tarefas de atualização in-loco do Windows 10      | ![Com suporte](media/green_check.png)  (1802) |
| Sequências de tarefas que não estão usando imagens de inicialização e são implantadas com uma opção: **Baixar todo o conteúdo localmente antes de iniciar a sequência de tarefas**      | ![Com suporte](media/green_check.png)  (1802) |
| CMPivot     | ![Com suporte](media/green_check.png)  (1806) |
| Outros cenários de sequência de tarefas     | ![Sem suporte](media/Red_X.png) |
| Push de cliente     | ![Sem suporte](media/Red_X.png) |
| Atribuição automática de site     | ![Sem suporte](media/Red_X.png) |
| Catálogo de aplicativos     | ![Sem suporte](media/Red_X.png) |
| Solicitações de aprovação de software     | ![Sem suporte](media/Red_X.png) |
| Console do Configuration Manager     | ![Sem suporte](media/Red_X.png) |
| Ferramentas remotas     | ![Sem suporte](media/Red_X.png) |
| Site de relatórios     | ![Sem suporte](media/Red_X.png) |
| Wake on LAN     | ![Sem suporte](media/Red_X.png) |
| Clientes Mac, Linux e UNIX     | ![Sem suporte](media/Red_X.png) |
| Cache de pares     | ![Sem suporte](media/Red_X.png) |
| MDM local     | ![Sem suporte](media/Red_X.png) |


|Chave|
|--|
|![Com suporte](media/green_check.png) = há suporte para esse recurso no CMG em todas as versões compatíveis do Configuration Manager  |
|![Compatível](media/green_check.png) (*YYMM*) = há suporte para esse recurso no CMG a partir da versão *YYMM* do Configuration Manager  |
|![Sem suporte](media/Red_X.png) = esse recurso não é compatível com o CMG |



## <a name="cost"></a>Custo

>[!IMPORTANT]  
>As seguintes informações de custo são apenas uma estimativa. O ambiente pode ter outras variáveis que afetam o custo geral do uso do CMG.

O CMG usa os seguintes componentes do Azure, que incorrem em encargos para a conta de assinatura do Azure:

#### <a name="virtual-machine"></a>Máquina virtual

- O CMG usa os Serviços de Nuvem do Azure como PaaS (plataforma como serviço). Esse serviço usa VMs (máquinas virtuais) que incorrem em custos de computação.  

- No Configuration Manager versão 1706, o CMG usa uma VM A2 Standard.  

- A partir do Configuration Manager versão 1710, o CMG usa uma VM A2 V2 Standard.  

- Selecione quantas instâncias de VM dão suporte ao CMG. Uma é o padrão e 16 é o máximo. Esse número é definido durante a criação do CMG e pode ser alterado posteriormente para dimensionar o serviço, conforme necessário.

- Para obter mais informações sobre a quantidade de VMs para as quais você precisa dar suporte em seus clientes, consulte [Desempenho e escala](#performance-and-scale).

- Consulte a [Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/) para ajudar a determinar os possíveis custos.

    > [!NOTE]  
    > Os custos de máquina virtual variam de acordo com a região.

#### <a name="outbound-data-transfer"></a>Transferência de dados de saída

- Os encargos baseiam-se nos dados que fluem para fora do Azure (saída ou download). Os dados que fluem para o Azure são gratuitos (entrada ou upload). Os dados do CMG que fluem para fora do Azure incluem uma política para o cliente, as notificações do cliente e as respostas do cliente encaminhadas pelo CMG ao site. Essas respostas incluem relatórios de inventário, mensagens de status e status de conformidade.  

- Mesmo sem a comunicação dos clientes com um CMG, uma comunicação em segundo plano gera o tráfego de rede entre o CMG e o site local.  

- Exiba a **Transferência de dados de saída (GB)** no console do Configuration Manager. Para obter mais informações, consulte [Monitorar clientes no CMG](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway).  

- Consulte os [Detalhes de preços de largura de banda do Azure](https://azure.microsoft.com/pricing/details/bandwidth/) para ajudar a determinar os possíveis custos. O preço da transferência de dados é calculado por camadas. Quanto mais você utilizar, menos você paga por gigabyte.  

- *Apenas para fins de estimativa*, espere aproximadamente 100-300 MB por cliente/mês para clientes baseados na Internet. A estimativa mais baixa refere-se a uma configuração de cliente padrão. A estimativa mais alta refere-se a uma configuração de cliente mais agressiva. O uso real pode variar, dependendo de como as configurações do cliente são definidas.  

   > [!NOTE]  
   > A execução de outras ações, como a implantação de atualizações de software ou aplicativos, aumenta a quantidade de transferência de dados de saída do Azure.

#### <a name="content-storage"></a>Armazenamento de conteúdo

- Os clientes baseados na Internet recebem o conteúdo da atualização de software da Microsoft do Windows Update sem custo adicional. Não distribua pacotes de atualização com o conteúdo do Microsoft Update para um ponto de distribuição na nuvem; caso contrário, você poderá incorrer em custos de armazenamento e de saída de dados.  

- Para outros tipos de conteúdo necessários, como atualizações de aplicativos ou de software de terceiros, é necessário distribuí-los para um ponto de distribuição na nuvem. Atualmente, o CMG dá suporte apenas ao ponto de distribuição na nuvem para enviar conteúdo aos clientes.  

- Para obter mais informações, confira o custo de utilização de [pontos de distribuição na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_cost).  

- Da versão 1806 em diante, um CMG pode também fornecer conteúdo aos clientes. Essa funcionalidade reduz os certificados necessários e o custo das VMs do Azure. Para obter mais informações, consulte [Modificar um CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg).<!--1358651-->  


#### <a name="other-costs"></a>Outros custos

- Cada serviço de nuvem tem um endereço IP dinâmico. Cada CMG distinto usa um novo endereço IP dinâmico. A adição de outras VMs por CMG não aumenta esses endereços.  



## <a name="performance-and-scale"></a>Desempenho e escala

Para obter mais informações sobre a escala do CMG, consulte [Tamanho e números de escala](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg).

As seguintes recomendações podem ajudá-lo a melhorar o desempenho do CMG:

- Se possível, configure o CMG, o ponto de conexão do CMG e o servidor do site do Configuration Manager na mesma região da rede para reduzir a latência.  

- A conexão entre o cliente do Configuration Manager e o CMG não tem reconhecimento de região. A comunicação do cliente não é afetada pela latência/separação geográfica. Não é necessário implantar vários CMG para fins de proximidade geográfica. Implante o CMG no site de nível superior na sua hierarquia e adicione instâncias para aumentar a escala.

- Para alta disponibilidade do serviço, crie um CMG com, pelo menos, duas instâncias do CMG e dois pontos de conexão do CMG por site.  

- Dimensione o CMG para dar suporte a mais clientes adicionando mais instâncias de VM. O Azure Load Balancer controla as conexões de cliente com o serviço.  

- Crie mais pontos de conexão de CMG para distribuir a carga entre eles. O CMG distribui o tráfego para seus pontos de conexão do CMG de conexão de forma round-robin.  

- Quando o CMG está sob alta carga devido a ter mais do que o número de clientes compatíveis, ele ainda manipula as solicitações, mas pode haver atraso.  


> [!Note]  
> Embora o Configuration Manager não tenha nenhum limite rígido quanto ao número de clientes para um ponto de conexão do CMG, o Windows Server tem um intervalo máximo padrão de portas dinâmicas TCP de 16.384. Se um site do Configuration Manager gerencia mais de 16.384 clientes com um único ponto de conexão do CMG, é necessário aumentar o limite do Windows Server. Todos os clientes mantêm um canal para as notificações do cliente, que mantém uma porta aberta no ponto de conexão do CMG. Para obter mais informações sobre como usar o comando netsh para aumentar esse limite, consulte o [artigo 929851 do Suporte da Microsoft](https://support.microsoft.com/help/929851).



## <a name="ports-and-data-flow"></a>Portas e fluxo de dados

Você não precisa abrir nenhuma porta de entrada para a rede local. O ponto de conexão de serviço e o ponto de conexão do CMG iniciam toda a comunicação com o Azure e o CMG. Essas duas funções do sistema de sites precisam conseguir criar conexões de saída para a nuvem da Microsoft. O ponto de conexão de serviço implanta e monitora o serviço no Azure e, portanto, ele precisa estar no modo online. O ponto de conexão do CMG se conecta ao CMG para gerenciar a comunicação entre o CMG e as funções do sistema de sites locais.

O seguinte diagrama é um fluxo de dados básico e conceitual do CMG: ![Fluxo de dados do CMG](media/cmg-data-flow.png)
   1. O ponto de conexão de serviço se conecta ao Azure pela porta HTTPS 443. Ele se autentica usando o Azure AD ou o certificado de gerenciamento do Azure. O ponto de conexão de serviço implanta o CMG no Azure. O CMG cria o serviço de nuvem HTTPS usando o certificado de autenticação de servidor.  

   2. O ponto de conexão do CMG se conecta ao CMG no Azure por TCP-TLS ou HTTPS. Ele mantém a conexão aberta e cria o canal para a comunicação bidirecional futura.   

   3. O cliente se conecta ao CMG pela porta HTTPS 443. Ele se autentica usando o Azure AD ou o certificado de autenticação de cliente.  

   4. O CMG encaminha a comunicação do cliente pela conexão existente para o ponto de conexão do CMG local. Não é necessário abrir nenhuma porta de firewall de entrada.  

   5. O ponto de conexão do CMG encaminha a comunicação do cliente para o ponto de gerenciamento local e o ponto de atualização de software.  

### <a name="required-ports"></a>Portas obrigatórias
Esta tabela lista as portas de rede e os protocolos obrigatórios. O *Cliente* é o dispositivo que inicia a conexão, exigindo uma porta de saída. O *Servidor* é o dispositivo que aceita a conexão, exigindo uma porta de entrada. 

| Cliente  | Protocolo | Porta  | Servidor  | Descrição  |
|---------|---------|---------|---------|---------|
| Ponto de Conexão de Serviço     | HTTPS | 443        | Azure        | Implantação de CMG |
| Ponto de conexão de CMG     |  TCP-TLS | 10140-10155        | Serviço CMG        | Protocolo preferencial para criação do canal do CMG <sup>1</sup> |
| Ponto de conexão de CMG     | HTTPS | 443        | Serviço CMG       | Protocolo de fallback para criação do canal do CMG para apenas uma instância de VM<sup>2</sup> |
| Ponto de conexão de CMG     |  HTTPS   | 10124-10139     | Serviço CMG       | Protocolo de fallback para criação do canal do CMG para duas ou mais instâncias de VM<sup>3</sup> |
| Cliente     |  HTTPS | 443         | CMG        | Comunicação geral entre clientes |
| Ponto de conexão de CMG      | HTTPS ou HTTP | 443 ou 80         | Ponto de gerenciamento<br>(versão 1706 ou 1710) | Tráfego local; a porta depende da configuração do ponto de gerenciamento |
| Ponto de conexão de CMG      | HTTPS | 443      | Ponto de gerenciamento<br>(versão 1802) | O tráfego local deve ser HTTPS |
| Ponto de conexão de CMG      | HTTPS ou HTTP | 443 ou 80         | Ponto de atualização de software | Tráfego local; a porta depende da configuração do ponto de atualização de software |

<sup>1</sup> O ponto de conexão do CMG primeiro tenta estabelecer uma conexão TCP-TLS de longa vida com cada instância de VM do CMG. Ele se conecta à primeira instância de VM na porta 10140. A segunda instância de VM usa a porta 10141, até a 16ª na porta 10155. Uma conexão TCP-TLS tem o melhor desempenho, mas não dá suporte ao proxy da Internet. Se o ponto de conexão do CMG não puder se conectar por TCP-TLS, ele recorrerá ao HTTPS<sup>2</sup>.  

<sup>2</sup> Se o ponto de conexão do CMG não puder se conectar ao CMG por TCP-TLS<sup>1</sup>, ele se conectará ao balanceador de carga de rede do Azure por HTTPS 443 apenas para uma instância de VM.  

<sup>3</sup> Se houver duas ou mais instâncias de VM, o ponto de conexão do CMG usará o HTTPS 10124 para a primeira instância de VM, não o HTTPS 443. Ele se conectará à segunda instância de VM em HTTPS 10125, até a 16ª na porta HTTPS 10139.


### <a name="internet-access-requirements"></a>Requisitos de acesso à Internet

O sistema de sites do ponto de conexão do CMG é compatível com um proxy Web. Para obter mais informações sobre como configurar essa função para um proxy, consulte [Suporte do servidor proxy](/sccm/core/plan-design/network/proxy-server-support#to-set-up-the-proxy-server-for-a-site-system-server). O ponto de conexão do CMG exige conectividade com os seguintes pontos de extremidade:  

- Os pontos de extremidade específicos do Azure são diferentes conforme o ambiente, dependendo da configuração. O Configuration Manager armazena esses pontos de extremidade no banco de dados do site. Consulte a tabela **AzureEnvironments** no SQL Server para obter a lista de pontos de extremidade do Azure.  

- ServiceManagementEndpoint (https://management.core.windows.net/))  

- StorageEndpoint (core.windows.net)  

- Para a recuperação de token do Azure AD pelo cliente e console do Configuration Manager: ActiveDirectoryEndpoint (https://login.microsoftonline.com/)  

- Para a descoberta de usuários do Azure AD: Ponto de extremidade do AAD Graph (https://graph.windows.net/)  



## <a name="next-steps"></a>Próximas etapas

- [Certificados para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Segurança e privacidade para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Tamanho e números de escala do gateway de gerenciamento de nuvem](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
- [Perguntas frequentes sobre o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Configurar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
