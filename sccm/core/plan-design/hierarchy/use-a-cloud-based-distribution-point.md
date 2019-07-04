---
title: Ponto de distribuição na nuvem
titleSuffix: Configuration Manager
description: Planeje e projete a distribuição de conteúdo de software por meio do Microsoft Azure com pontos de distribuição na nuvem no Configuration Manager.
ms.date: 06/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fe6544e020f819f1ed18592ce811f2992a5603eb
ms.sourcegitcommit: 86968fc2f129e404ff8e08f91a05fa17b5c47527
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2019
ms.locfileid: "67251497"
---
# <a name="use-a-cloud-distribution-point-in-configuration-manager"></a>Usar um ponto de distribuição na nuvem no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

> [!Important]  
> A implementação para o compartilhamento de conteúdo do Azure foi alterada. Use um gateway de gerenciamento de nuvem habilitado para conteúdo ativando a opção **Permitir que o CMG funcione como um ponto de distribuição de nuvem e forneça conteúdo do armazenamento do Azure**. Para obter mais informações, consulte [Modificar um CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg).
>
> Você não poderá criar um ponto de distribuição de nuvem tradicional no futuro. Para saber mais, consulte [Recursos removidos e preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).

Um ponto de distribuição na nuvem é um ponto de distribuição do Configuration Manager hospedado como uma PaaS (plataforma como serviço) no Microsoft Azure. Esse serviço dá suporte aos seguintes cenários:  

- Fornecer conteúdo de software a clientes baseados na Internet sem infraestrutura local adicional  

- Habilitar seu sistema de distribuição de conteúdo para a nuvem  

- Reduzir a necessidade de pontos de distribuição tradicionais  

Este artigo ajuda você a saber mais sobre o ponto de distribuição na nuvem, planejar o uso e projetar sua implementação. Ele inclui as seguintes seções:

- [Recursos e benefícios](#bkmk_features)
- [Design da topologia](#bkmk_topology)
- [Requirements](#bkmk_requirements)
- [Especificações](#bkmk_spec)
- [Custo](#bkmk_cost)
- [Desempenho e escala](#bkmk_perf)
- [Portas e fluxo de dados](#bkmk_dataflow)
- [Certificados](#bkmk_certs)
- [Perguntas frequentes](#bkmk_faq)


## <a name="bkmk_features"></a> Recursos e benefícios

### <a name="features"></a>Recursos

O ponto de distribuição na nuvem dá suporte a vários recursos que também são oferecidos pelos pontos de distribuição locais:  

- Gerencie pontos de distribuição na nuvem individualmente ou como membros de grupos de pontos de distribuição  

- Usar um ponto de distribuição na nuvem como local de conteúdo de fallback  

- Dá suporte para clientes tanto baseados na Internet quanto na intranet  

### <a name="benefits"></a>Benefícios

O ponto de distribuição na nuvem oferece os seguintes benefícios adicionais:  

- O site criptografa o conteúdo antes de enviá-la para o ponto de distribuição na nuvem no Azure.  

- Para atender às demandas inconstantes de solicitações de conteúdo por clientes, dimensione manualmente o serviço de nuvem no Azure. Essa ação não exige que você instale e provisione pontos de distribuição adicionais no Configuration Manager.  

- Dá suporte ao download de conteúdo de clientes configurados para outras tecnologias de conteúdo, como Windows BranchCache e provedores de conteúdo alternativo.  

- Da versão 1806 em diante, use pontos de distribuição na nuvem como locais de origem para os pontos de distribuição por pull.  


## <a name="bkmk_topology"></a> Design da topologia

A implantação e a operação de ponto de distribuição na nuvem inclui os seguintes componentes:  

- Um **serviço de nuvem** no Azure. O site distribui conteúdo para esse serviço, que o armazena no armazenamento em nuvem do Azure. O ponto de gerenciamento fornece aos clientes esse local de conteúdo na lista de fontes disponíveis conforme apropriado.  

- Uma função do sistema de sites do **ponto de gerenciamento** atende às solicitações do cliente de modo habitual.  

    - Clientes locais normalmente usam um ponto de gerenciamento local.  

    - Clientes baseados na Internet usam um [Gateway de Gerenciamento de Nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) ou um [ponto de gerenciamento baseado na Internet](/sccm/core/clients/manage/plan-internet-based-client-management).  

- O ponto de distribuição na nuvem usa um serviço Web **HTTPS baseado em certificado** para ajudar a proteger a comunicação de rede com clientes. Os clientes devem confiar nesse certificado.  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!--1322209-->
Da versão 1806 em diante, crie um ponto de distribuição na nuvem usando uma **implantação do Azure Resource Manager**. O [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) é uma plataforma moderna para gerenciar todos os recursos da solução como uma única entidade, chamado [grupo de recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). Ao implantar o ponto de distribuição na nuvem com o Azure Resource Manager, o site usa o Azure Active Directory (Azure AD) para autenticar e criar os recursos necessários para a nuvem. Essa implantação modernizada não exige o certificado de gerenciamento do Azure clássico.  

> [!Note]  
> Esse recurso não habilita o suporte para CSPs (Provedores de Serviços de Nuvem) do Azure. A implantação do ponto de distribuição na nuvem com o Azure Resource Manager continua a usar o serviço de nuvem clássico, ao qual o CSP não oferece suporte. Para saber mais, confira os [serviços do Azure disponíveis no CSP do Azure](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

A partir do Configuration Manager versão 1902, o Azure Resource Manager é o único mecanismo de implantação para novas instâncias do ponto de distribuição de nuvem. As implantações existentes continuam a funcionar.<!-- 3605704 -->

No Configuration Manager versão 1810 e anterior, o assistente do ponto de distribuição na nuvem ainda fornece a opção para uma **implantação de serviço clássico** usando um certificado de gerenciamento do Azure. Para simplificar a implantação e o gerenciamento de recursos, use o modelo de implantação do Azure Resource Manager para todos os pontos de distribuição na nuvem. Se possível, reimplante os pontos de distribuição na nuvem existentes por meio do Gerenciador de Recursos.

> [!Important]  
> Da versão 1810, a implantação de serviço clássico no Azure é preterida para uso no Configuration Manager. Esta versão é a última a dar suporte à criação dessas implantações do Azure. Essa funcionalidade será removida na primeira versão do Configuration Manager lançada após 1º de julho de 2019. Mova seus pontos de distribuição do CMG e da nuvem para implantações do Azure Resource Manager antes dessa hora. <!--SCCMDocs-pr issue #2993-->  

O Configuration Manager não migra os pontos de distribuição na nuvem clássicos existentes para o Modelo de implantação do Azure Resource Manager. Crie novos pontos de distribuição de nuvem usando implantações do Azure Resource Manager e remova os pontos de distribuição de nuvem clássicos.

### <a name="hierarchy-design"></a>Design de hierarquia

O local em que você cria o ponto de distribuição na nuvem depende de quais clientes precisam acessar o conteúdo. Da versão 1806 em diante, há três tipos de pontos de distribuição na nuvem:  

- Implantação do Azure Resource Manager: crie esse tipo em um site primário ou no site de administração central.  

- Implantação do serviço clássico: crie esse tipo somente em um site primário.  

- O Gateway de Gerenciamento de Nuvem também pode fornecer conteúdo aos clientes. Essa funcionalidade reduz os certificados necessários e o custo das VMs do Azure. Para obter mais informações, consulte [Planejar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).<!--1358651-->  

Para determinar se é necessário incluir os pontos de distribuição na nuvem em grupos de limites, considere os seguintes comportamentos:  

- Clientes baseados na Internet não confiam em grupos de limites. Eles usam apenas pontos de distribuição voltados para a Internet ou pontos de distribuição na nuvem. Se você estiver usando apenas os pontos de distribuição na nuvem para atender a esses tipos de clientes, não precisará incluí-los em grupos de limites.  

- Se você quiser que os clientes em sua rede interna usem um ponto de distribuição na nuvem, ele precisará estar no mesmo grupo de limite que os clientes. Os clientes priorizam os pontos de distribuição na nuvem por último na lista de fontes de conteúdo, porque há um custo associado a baixar conteúdo do Azure. Portanto, um ponto de distribuição na nuvem normalmente é usado como uma origem de fallback para clientes baseados na intranet. Se você quiser um design primeiro na nuvem, crie os grupos de limites para atender a esse requisito de negócios. Para obter mais informações, consulte [Configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).  

Mesmo que você instale pontos de distribuição na nuvem em regiões específicas do Azure, os clientes não estarão cientes das regiões do Azure. Eles selecionam aleatoriamente um ponto de distribuição na nuvem. Se você instalar pontos de distribuição na nuvem em várias regiões e um cliente receber mais de um na lista local de conteúdo, o cliente não poderá usar um ponto de distribuição na nuvem da mesma região do Azure.  

### <a name="backup-and-recovery"></a>Backup e descoberta  

Quando você usa um ponto de distribuição na nuvem em sua hierarquia, use as seguintes informações para ajudá-lo a planejar-se para backup e recuperação:  

- Quando você usa a tarefa de manutenção **Servidor do Site de Backup**, o Configuration Manager inclui automaticamente as configurações do ponto de distribuição na nuvem.  

- Faça o backup e salve uma cópia do certificado de autenticação de servidor. Se você usar a implantação de serviço clássico no Azure, também faça backup e salve uma cópia do certificado de gerenciamento do Azure. Quando você restaurar o site primário do Configuration Manager para um servidor diferente, deve reimportar os certificados.  


## <a name="bkmk_requirements"></a> Requisitos

- Você precisa de uma **assinatura do Azure** para hospedar o serviço.  

    - Um **administrador do Azure** precisa participar da criação inicial de alguns componentes, dependendo do design. Essa persona não precisa de permissões no Configuration Manager.  

- O servidor do site exige **acesso à Internet** para implantar e gerenciar o serviço de nuvem.  

- Ao usar o método de implantação do **Azure Resource Manager**, integre o Configuration Manager ao [Azure AD](/sccm/core/servers/deploy/configure/azure-services-wizard) para **Gerenciamento de Nuvem**. A *descoberta de usuário* do Azure AD não é necessária.  

- Um **certificado de autenticação de servidor**. Para obter mais informações, consulte a seção [Certificados](#bkmk_certs) abaixo.  

    - Para reduzir a complexidade, use um provedor de certificado público para o certificado de autenticação de servidor. Ao fazer isso, você também precisa de um **alias de DNS CNAME** para clientes resolverem o nome do serviço de nuvem.  

- No Configuration Manager versão 1810 e anterior, se você estiver usando o método clássico de implantação do Azure, precisará usar um **certificado de gerenciamento do Azure**. Para obter mais informações, consulte a seção [Certificados](#bkmk_certs) abaixo.  

    > [!TIP]  
    > Do Configuration Manager versão 1806 em diante, use o Modelo de implantação do **Azure Resource Manager**. Ele não exige esse certificado de gerenciamento.  
    >
    > O método de implantação clássico foi preterido da versão 1810 em diante.  

- Defina a configuração do cliente, **Permitir acesso aos pontos de distribuição na nuvem**, como **Sim** no grupo **Serviços de Nuvem**. Por padrão, esse valor é definido como **Não**.  

- Os dispositivos de cliente requerem **conectividade com a Internet** e devem usar **IPv4**.  


## <a name="bkmk_spec"></a> Especificações

- O ponto de distribuição na nuvem dá suporte a todas as versões do Windows listadas em [Sistemas operacionais compatíveis para clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).  

- Um administrador distribui os seguintes tipos de conteúdo de software com suporte:  
  - Aplicativos
  - Pacotes
  - Pacotes de atualização do sistema operacional
  - Atualizações de software de terceiros  

    > [!Important]  
    > Embora o console do Configuration Manager não bloqueie a distribuição de atualizações de software da Microsoft para um ponto de distribuição na nuvem, você está pagando os custos do Azure para armazenar o conteúdo que os clientes não usam. Clientes baseados na Internet sempre obtêm conteúdo de atualização de software da Microsoft do serviço de nuvem do Microsoft Update. Não distribua as atualizações de software da Microsoft para um ponto de distribuição na nuvem.  

- Da versão 1806 em diante, configure um ponto de distribuição por pull para usar um ponto de distribuição na nuvem como origem. Para saber mais, veja [Sobre pontos de distribuição de origem](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point#about-source-distribution-points).<!--1321554-->  

### <a name="deployment-settings"></a>Configurações da implantação

- Quando você implanta uma sequência de tarefas com a opção de **Baixar conteúdo localmente quando necessário executando uma sequência de tarefas**, o ponto de gerenciamento não inclui um ponto de distribuição na nuvem como local de conteúdo. Implante a sequência de tarefas com a opção de **Baixar todo o conteúdo localmente antes de iniciar a sequência de tarefas** para os clientes usarem um ponto de distribuição na nuvem.  

- Um ponto de distribuição na nuvem não dá suporte a implantações de pacote com a opção de **Executar programa do ponto de distribuição**. Use a opção de implantação para **Baixar conteúdo do ponto de distribuição e executar localmente**.  

### <a name="limitations"></a>Limitações  

- Você não pode usar um ponto de distribuição na nuvem para PXE ou implantações habilitadas para multicast.  

- Um ponto de distribuição na nuvem não dá suporte a aplicativos de streaming do App-V.  

- Não é possível [pré-configurar conteúdo](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent) em um ponto de distribuição na nuvem. O gerente de distribuição do site primário que gerencia o ponto de distribuição na nuvem transfere todo o conteúdo.  

- Não é possível configurar um ponto de distribuição na nuvem como um ponto de distribuição por pull.  


## <a name="bkmk_cost"></a> Custo

<!--501018-->
> [!IMPORTANT]  
> As seguintes informações de custo são apenas uma estimativa. Seu ambiente pode ter outras variáveis que afetam o custo geral do uso de um ponto de distribuição na nuvem.  

O Configuration Manager inclui as seguintes opções para ajudar a controlar os custos e monitorar o acesso a dados:  

- Controle e monitore a quantidade de conteúdo armazenado em um serviço de nuvem. Para obter mais informações, veja [Monitorar pontos de distribuição na nuvem](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure#bkmk_monitor).  

- Configure o Configuration Manager para alertá-lo quando os limites para downloads do cliente atingirem ou excederem o limite mensal. Para obter mais informações, veja [Alertas de limite de transferência de dados](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure#bkmk_alerts).

- Para ajudar a reduzir o número de transferências de dados de pontos de distribuição na nuvem por clientes, use uma das seguinte tecnologias de cache de par:  
  - Cache par do Configuration Manager
  - Windows BranchCache
  - Otimização de Entrega do Windows 10  

    Para mais informações, consulte [Conceitos fundamentais para o gerenciamento de conteúdo](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).  

### <a name="components"></a>Componentes

Um ponto de distribuição na nuvem usa os seguintes componentes do Azure, que incorrem em encargos para a conta de assinatura do Azure:  

> [!Tip]  
> Da versão 1806 em diante, o Gateway de Gerenciamento de Nuvem também pode veicular conteúdo aos clientes. Essa funcionalidade reduz o custo consolidando as VMs do Azure. Para obter mais informações, veja [Custo para Gateway de Gerenciamento de Nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#cost).  

#### <a name="virtual-machine"></a>Máquina virtual

- O ponto de distribuição na nuvem usa a PaaS (plataforma como serviço) dos Serviços de Nuvem do Azure. Esse serviço usa VMs (máquinas virtuais) que incorrem em custos de computação.  

- Cada serviço de ponto de distribuição na nuvem usa duas VMs A0 padrão.  

- Consulte a [Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/) para ajudar a determinar os possíveis custos.

    > [!NOTE]  
    > Os custos de máquina virtual variam de acordo com a região.

#### <a name="outbound-data-transfer"></a>Transferência de dados de saída

- Quaisquer fluxos de dados para o Azure são gratuitos (entrada ou upload). Distribuição de conteúdo do site para o ponto de distribuição na nuvem que está carregando para o Azure.  

- Os encargos baseiam-se nos dados que fluem para fora do Azure (saída ou download). Fluxos de dados do ponto de distribuição na nuvem fora do Azure consistem em conteúdo de software que os clientes baixam.  

- Para obter mais informações, veja [Monitorar pontos de distribuição na nuvem](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure#bkmk_monitor).  

- Consulte os [Detalhes de preços de largura de banda do Azure](https://azure.microsoft.com/pricing/details/bandwidth/) para ajudar a determinar os possíveis custos. O preço da transferência de dados é calculado por camadas. Quanto mais você utilizar, menos você paga por gigabyte.  

#### <a name="content-storage"></a>Armazenamento de conteúdo

- Clientes baseados na Internet obtêm conteúdo de atualização de software Microsoft do serviço de nuvem do Microsoft Update sem custo adicional. Não distribua pacotes de implantação de atualização de software com atualizações de software da Microsoft para um ponto de distribuição na nuvem. Caso contrário, você incorrerá em custos de armazenamento de dados para conteúdo que os clientes nunca usarão.  

- Pontos de distribuição em nuvem usam o seguinte Armazenamento de Blobs padrão dependendo do modelo de implantação:  

    - Uma implantação do Azure Resource Manager usa o LRS (armazenamento localmente redundante) do Azure. Essa alteração reduz o custo da conta de armazenamento. A implantação clássica não estava usando os recursos adicionais do GRS. Para saber mais, veja [Armazenamento com redundância local](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs).  

    - Uma implantação clássica com o Configuration Manager versão 1810 ou anterior usa o armazenamento do Azure com redundância geográfica (GRS). Para obter mais informações, veja [Armazenamento com redundância geográfica](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs).  

#### <a name="other-costs"></a>Outros custos

- Cada serviço de nuvem tem um endereço IP dinâmico. Cada ponto de distribuição na nuvem distinto usa um novo endereço IP dinâmico. A adição de outras VMs por serviço de nuvem não aumenta esses endereços.  


## <a name="bkmk_dataflow"></a> Portas e fluxo de dados

Há dois fluxos de dados primários para o ponto de distribuição na nuvem:  

- O servidor do site se conecta ao Azure para configurar o serviço de ponto de distribuição na nuvem  

- Um cliente se conecta ao ponto de distribuição na nuvem para baixar conteúdo  

### <a name="site-server-to-azure"></a>Servidor do site para o Azure

Você não precisa abrir nenhuma porta de entrada para a rede local. O servidor do site inicia todas as comunicações com o Azure e o ponto de distribuição na nuvem para implantar, atualizar e gerenciar o serviço de nuvem. O servidor do site precisa criar conexões de saída para a nuvem da Microsoft. Essa ação equivale a instalar a função do sistema de site do ponto de distribuição em um site específico.  

### <a name="client-to-cloud-distribution-point"></a>Ponto de distribuição do cliente para a nuvem

Você não precisa abrir nenhuma porta de entrada para a rede local. Clientes baseados na Internet comunicam-se diretamente com o serviço do Azure. Clientes que usam um ponto de distribuição na nuvem em sua rede interna precisam se conectar à nuvem da Microsoft.

Para obter mais informações sobre a prioridade de localização de conteúdo e quando clientes baseados na intranet usam um ponto de distribuição na nuvem, veja [Prioridade da fonte de conteúdo](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#content-source-priority).

Quando um cliente usa um ponto de distribuição na nuvem como local de conteúdo:  

1. O ponto de gerenciamento dá ao cliente um token de acesso, juntamente com a lista de fontes de conteúdo. Esse token é válido por 24 horas e dá ao cliente acesso ao ponto de distribuição na nuvem.  

2. O ponto de gerenciamento responde à solicitação de local do cliente com o **FQDN do Serviço** do ponto de distribuição na nuvem. Essa propriedade é igual ao nome comum do certificado de autenticação de servidor.  

    Se você estiver usando seu nome de domínio, por exemplo, WallaceFalls.contoso.com, o cliente primeiro tentará resolver esse FQDN. É necessário um alias de CNAME no DNS voltado para a Internet do seu domínio para clientes resolverem o nome de serviço do Azure, por exemplo: WallaceFalls.cloudapp.net.  

3. Em seguida, o cliente resolve o nome do serviço do Azure, por exemplo, WallaceFalls.cloudapp.net, para um endereço IP válido. Essa resposta deve ser tratada pelo DNS do Azure.  

4. O cliente conecta-se ao ponto de distribuição na nuvem. O Azure faz o balanceia a carga da conexão para uma das instâncias da VM. O cliente autentica-se usando o token de acesso.  

5. O ponto de distribuição na nuvem autentica o token de acesso do cliente e, em seguida, dá ao cliente o local exato do conteúdo no armazenamento do Azure.  

6. Se o cliente confiar no certificado de autenticação de servidor do ponto de distribuição na nuvem, ele se conectará ao armazenamento do Azure para baixar o conteúdo.


## <a name="bkmk_perf"></a> Desempenho e escala

<!--494872-->

Como com qualquer design de ponto de distribuição, considere os seguintes fatores:  

- Número de conexões de cliente simultâneas
- O tamanho do conteúdo que os clientes baixam
- O tempo permitido para atender às suas necessidades de negócios

Dependendo do seu [design de topologia](#bkmk_topology), se os clientes tiverem a opção de mais de um ponto de distribuição na nuvem para qualquer conteúdo em questão, eles naturalmente usarão esses serviços de nuvem de modo aleatório. Se você distribuir apenas uma determinada parte do conteúdo para um ponto de distribuição na nuvem único, e um grande número de clientes tentar baixar esse conteúdo ao mesmo tempo, essa atividade imporá uma carga maior àquele ponto de distribuição na nuvem único. Adicionar um ponto de distribuição na nuvem extra também inclui um serviço de armazenamento do Azure separado. Para obter mais informações sobre como o cliente se comunica com os componentes do ponto de distribuição na nuvem e baixa conteúdo, veja [Portas e fluxo de dados](#bkmk_dataflow).  

O ponto de distribuição na nuvem usa duas VMs do Azure como o front-end para o armazenamento do Azure. Essa implantação padrão atende à maioria das necessidades do cliente. Em algumas circunstâncias extremas, com um grande número de conexões de cliente simultâneas (por exemplo, 150 mil clientes), a capacidade de processamento das VMs do Azure não consegue acompanhar as solicitações do cliente. Você não pode redimensionar as VMs do Azure usadas para o ponto de distribuição na nuvem. Embora você não possa configurar o número de instâncias de VM para o ponto de distribuição na nuvem no Configuration Manager, se necessário, reconfigure o serviço de nuvem no portal do Azure. Adicione mais instâncias de VM manualmente ou configure r o serviço para dimensionar automaticamente.

> [!Important]  
> Quando você atualiza o Configuration Manager, o site reimplanta o serviço de nuvem. Se você reconfigurar manualmente o serviço de nuvem no portal do Azure, o número de instâncias será redefinido para o padrão de dois.  

O serviço de armazenamento do Azure dá suporte a 500 solicitações por segundo para um único arquivo. Teste de desempenho de um ponto de distribuição na nuvem única deu suporte para a distribuição de um único arquivo de 100 MB para 50 mil clientes em 24 horas.<!--512106-->  


## <a name="bkmk_certs"></a> Certificados  

Dependendo do design do ponto de distribuição na nuvem, você precisa de um ou mais certificados digitais.  

### <a name="general-information"></a>Informações gerais

<!--SCCMDocs issue #779-->
Certificados para pontos de distribuição na nuvem têm suporte para as seguintes configurações:  

- Comprimento de chave de 4096 bits

- Certificados da Versão 3. Para obter mais informações, consulte [Visão geral dos certificados CNG](/sccm/core/plan-design/network/cng-certificates-overview).  

- Iniciando na versão 1802, quando você configura o Windows com a seguinte política: **Criptografia do sistema: use algoritmos em conformidade com FIPS para criptografia, hash e assinatura**  

- Da versão 1802 em diante, suporte para TLS 1.2. Para obter mais informações, veja [Referência técnica para controles de criptografia](/sccm/core/plan-design/security/cryptographic-controls-technical-reference#about-ssl-vulnerabilities).  

### <a name="server-authentication-certificate"></a>Certificado de autenticação de servidor

*Esse certificado é obrigatório para todas as implantações de ponto de distribuição na nuvem.*

Para obter mais informações, veja [Certificado de autenticação de servidor do CMG](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_serverauth) e as subseções a seguir, conforme necessário:  

- Certificado raiz confiável do CMG para clientes
- Certificado de autenticação de servidor emitido por um provedor público
- Certificado de autenticação de servidor emitido pelo PKI corporativo

O ponto de distribuição na nuvem usa esse tipo de certificado da mesma forma que o Gateway de Gerenciamento de Nuvem. Os clientes também precisam confiar nesse certificado. Para reduzir a complexidade, a Microsoft recomenda o uso de um certificado emitido por um provedor público.

A menos que você use um certificado curinga, não reutilize o mesmo certificado. Cada instância do ponto de distribuição na nuvem e o Gateway de Gerenciamento de Nuvem requer um certificado de autenticação de servidor exclusivo.

Para obter mais informações sobre como criar esse certificado de uma PKI, veja [Implantar o certificado de serviço para pontos de distribuição na nuvem](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012).  

### <a name="azure-management-certificate"></a>Certificado de gerenciamento do Azure

*Esse certificado é obrigatório para implantações de serviço clássico. Não é necessário para implantações do Azure Resource Manager.*

> [!Important]  
> Do Configuration Manager versão 1806 em diante, use o Modelo de implantação do **Azure Resource Manager**. Ele não exige esse certificado de gerenciamento.  
>
> O método de implantação clássico foi preterido da versão 1810 em diante.  
>
> A partir do Configuration Manager versão 1902, o Azure Resource Manager é o único mecanismo de implantação para novas instâncias do ponto de distribuição de nuvem. Esse certificado não é necessário no Configuration Manager versão 1902 ou posterior.<!-- 3605704 -->

Se você estiver usando o método clássico de implantação do Azure com o Configuration Manager versão 1810 ou anterior, precisará usar um **certificado de gerenciamento do Azure**. Para obter mais informações, veja a seção [Certificado de gerenciamento do Azure](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_azuremgmt) do artigo de certificados de Gateway de Gerenciamento de Nuvem. O servidor do site do Configuration Manager usa esse certificado para autenticar com o Azure para criar e gerenciar a implantação clássica.  

Para reduzir a complexidade, use o mesmo certificado de gerenciamento do Azure para todas as implantações clássicas de pontos de distribuição na nuvem e gateways de gerenciamento em nuvem em todas as assinaturas do Azure e todos os sites do Configuration Manager.


## <a name="bkmk_faq"></a> Perguntas frequentes

### <a name="does-a-client-need-a-certificate-to-download-content-from-a-cloud-distribution-point"></a>Um cliente precisa de um certificado para baixar o conteúdo de um ponto de distribuição na nuvem?

Um certificado de autenticação de cliente não é necessário. O cliente precisa confiar no certificado de autenticação de servidor usado pelo ponto de distribuição na nuvem. Se esse certificado for emitido por um provedor de certificado público, a maioria dos dispositivos do Windows já incluirá certificados raiz confiáveis para esses provedores. Se você emitir um certificado de autenticação de servidor da PKI da sua organização, os clientes precisarão confiar nos certificados de emissão em toda a cadeia. Esta cadeia inclui a autoridade de certificação raiz e qualquer autoridade de certificação intermediária. Dependendo do design de PKI, esse certificado poderá introduzir complexidade adicional à implantação do ponto de distribuição na nuvem. Para evitar essa complexidade, a Microsoft recomenda o uso de um provedor de certificado público em que os clientes já confiam.  

### <a name="can-my-on-premises-clients-use-a-cloud-distribution-point"></a>Meus clientes locais podem usar um ponto de distribuição na nuvem?

Sim. Se você quiser que os clientes em sua rede interna usem um ponto de distribuição na nuvem, ele precisará estar no mesmo grupo de limite que os clientes. Os clientes priorizam os pontos de distribuição na nuvem por último na lista de fontes de conteúdo, porque há um custo associado a baixar conteúdo do Azure. Assim, um ponto de distribuição na nuvem normalmente é usado como uma origem de fallback para clientes baseados na intranet. Se você quiser um design primeiro na nuvem, crie os grupos de limites adequadamente. Para obter mais informações, consulte [Configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).  

### <a name="do-i-need-azure-expressroute"></a>O Azure ExpressRoute é necessário?

O [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) possibilita que você estenda a rede local para a nuvem da Microsoft. O ExpressRoute, ou outras conexões de rede virtual desse tipo, não é necessário para o ponto de distribuição na nuvem do Configuration Manager.  

Se a sua organização usar o ExpressRoute, isole a assinatura do Azure para o ponto de distribuição na nuvem da assinatura que usa o ExpressRoute. Essa configuração garante que o ponto de distribuição na nuvem não seja conectado acidentalmente dessa maneira.  

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>É necessário manter as máquinas virtuais do Azure?

Nenhuma manutenção é necessária. O design do ponto de distribuição na nuvem usa a PaaS (plataforma como serviço) do Azure. Usando a assinatura fornecida, o Configuration Manager cria as VMs, o armazenamento e a rede necessários. O Azure protege e atualiza a máquinas virtuais. Essas VMs não fazem parte do ambiente local, como é o caso do IaaS (infraestrutura como serviço). O ponto de distribuição na nuvem é uma PaaS que estende seu ambiente do Configuration Manager para a nuvem. Para obter mais informações, veja [Vantagens de segurança de um modelo de serviço de nuvem PaaS](https://docs.microsoft.com/azure/security/security-paas-deployments#security-advantages-of-a-paas-cloud-service-model).  

### <a name="does-the-cloud-distribution-point-use-azure-cdn"></a>O ponto de distribuição na nuvem usa a CDN do Azure?

A CDN (Rede de Distribuição de Conteúdo) do Azure é uma solução global para fornecer rapidamente conteúdo de alta largura de banda armazenando em cache o conteúdo em nós estrategicamente posicionados no mundo inteiro. Para obter mais informações, veja [O que é a CDN do Azure?](https://docs.microsoft.com/azure/cdn/cdn-overview).

O ponto de distribuição na nuvem do Configuration Manager atualmente não dá suporte para a CDN do Azure.


## <a name="next-steps"></a>Próximas etapas

[Instalar pontos de distribuição na nuvem](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure)
