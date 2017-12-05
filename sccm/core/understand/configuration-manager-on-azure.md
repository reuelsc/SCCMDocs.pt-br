---
title: Configuration Manager no Azure
description: "Informações sobre o uso do Configuration Manager em um ambiente do Azure."
ms.custom: na
ms.date: 03/27/2017
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: article
ms.assetid: d24257d8-8136-47f4-8e0d-34021356dc37
caps.latest.revision: "2"
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: c21ebf6e608655504664fe7fa6a1bdc3f96850eb
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="configuration-manager-on-azure---frequently-asked-questions"></a>Configuration Manager no Azure – Perguntas frequentes
*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As perguntas e respostas a seguir podem ajudá-lo a entender quando usar e como configurar o Configuration Manager no Microsoft Azure.

## <a name="general-questions"></a>Perguntas gerais
### <a name="my-company-is-trying-to-move-as-many-physical-servers-as-possible-to-microsoft-azure-can-i-move-configuration-manager-servers-to-azure"></a>Minha empresa está tentando mover o máximo possível de servidores físicos para o Microsoft Azure, posso mover servidores do Configuration Manager para o Azure?
Certamente, esse é um cenário com suporte.  Confira [Support for Virtualization Environments for System Center Configuration Manager](/sccm/core/plan-design/configs/support-for-virtualization-environments) (Suporte para ambientes de virtualização do System Center Configuration Manager).

### <a name="great-my-environment-requires-multiple-sites-should-all-child-primary-sites-be-in-azure-with-the-central-administration-site-or-on-premises-what-about-secondary-sites"></a>Ótimo! Meu ambiente requer vários sites. Todos os sites primários filho devem estar no Azure com o site de administração central ou devem estar locais? E os sites secundários?
As comunicações site a site (com base em arquivo e replicação de banco de dados) se beneficiam da proximidade de estar hospedado no Azure. No entanto, todo o tráfego relacionado ao cliente seria remoto dos servidores do site e dos sistemas de sites. Se você usa uma conexão de rede rápida e confiável entre o Azure e sua intranet com um plano de dados ilimitado, hospedar toda a sua infraestrutura no Azure é uma opção.

No entanto, se você usar um plano de dados limitado e a largura de banda disponível ou o custo for uma preocupação ou a conexão de rede entre o Azure e sua intranet não for rápida ou puder não ser confiável, considere colocar sites específicos (e sistemas de sites) localmente e use os controles de largura de banda integrados no Configuration Manager.

### <a name="is-having-configuration-manager-in-azure-a-saas-scenario-software-as-a-service"></a>Ter o Configuration Manager no Azure é um cenário de SaaS (Software como Serviço)?
Não, é um IaaS (Infraestrutura como Serviço) porque você hospeda os servidores da infraestrutura do Configuration Manager em máquinas virtuais do Azure.

### <a name="what-areas-should-i-pay-attention-to-when-considering-a-move-of-my-configuration-manager-infrastructure-to-azure"></a>A quais áreas devo prestar atenção ao considerar uma mudança da minha infraestrutura do Configuration Manager para o Azure?
Boa pergunta, aqui estão as áreas que são mais importantes ao tomar essa decisão, cada uma é explorada em uma seção separada deste tópico:
1.  Rede
2.  Disponibilidade
3.  Desempenho
4.  Custo
5.  Experiência do usuário

## <a name="networking"></a>Rede
### <a name="what-about-networking-requirements-should-i-use-expressroute-or-an-azure-vpn-gateway"></a>E quanto aos requisitos de rede, devo usar o ExpressRoute ou um Gateway de VPN do Azure?
A rede é uma decisão muito importante. As velocidades de rede e latência podem afetar a funcionalidade entre o servidor do site e sistemas de sites remotos e qualquer comunicação de cliente para os sistemas de sites. Nossa recomendação é usar o ExpressRoute. Mas não há nenhuma limitação do Configuration Manager para parar de usar o Gateway de VPN do Azure. Você deve examinar cuidadosamente suas necessidades (desempenho, aplicação de patches, distribuição de software, implantação do sistema operacional) dessa infraestrutura e então tomar sua decisão. Alguns pontos a serem considerados para cada solução incluem:

 - **ExpressRoute** (recomendado)
  - Extensão natural para seu datacenter (pode unir vários datacenters)
  - Conexões privadas entre datacenters do Azure e sua infraestrutura
  - Não passe pela Internet pública
  - Oferece confiabilidade, velocidades rápidas, latência mais baixa, segurança alta
  - Oferece opções de planos de dados ilimitados e velocidades de até 10 Gbps
 - **Gateway de VPN**
  - VPNs site a site/ponto a site
  - O tráfego passa pela Internet pública
  - Usa o protocolo IPsec e o protocolo IKE

### <a name="expressroute-has-many-different-options-like-unlimited-vs-metered-different-speed-options-and-premium-add-on-which-should-i-choose"></a>O ExpressRoute tem muitas opções diferentes, como ilimitada vs. limitado, diferentes opções de velocidade e complemento premium. Qual devo escolher?
As opções selecionadas dependem do cenário que você está implementando e quantos dados você pretende distribuir. A transferência de dados do Configuration Manager pode ser controlada entre servidores do site e pontos de distribuição, mas a comunicação de servidor do site para servidor do site não pode ser controlada.   Quando você usa um plano de dados limitado, colocar sites (e sistemas de sites) específicos localmente e usar [controles de largura de banda internos do Configuration Manager](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management) pode ajudar a controlar o custo do uso do Azure.

### <a name="what-about-installation-requirements-like-active-directory-domains-do-i-still-need-to-join-my-site-servers-to-an-active-directory-domain"></a>E quanto aos requisitos de instalação como os domínios do Active Directory? Ainda preciso adicionar meus servidores do site a um domínio do Active Directory?
Sim. Quando você muda para o Azure, as [configurações com suporte](/sccm/core/plan-design/configs/supported-configurations) permanecem as mesmos, incluindo os requisitos do Active Directory para a instalação do Configuration Manager.

### <a name="i-understand-the-need-to-join-my-site-servers-to-an-active-directory-domain-but-can-i-use-azure-active-directory"></a>Eu entendo a necessidade de adicionar meus servidores do site a um domínio do Active Directory, mas posso usar o Azure Active Directory?
Não, não há suporte para o Azure Active Directory no momento. Seus servidores de site ainda devem ser membros de um [domínio do Windows Active Directory](/sccm/core/plan-design/configs/support-for-active-directory-domains).



## <a name="availability"></a>Disponibilidade
### <a name="one-of-the-reasons-i-am-moving-infrastructure-to-azure-is-the-promise-of-high-availability-can-i-take-advantage-of-high-availability-options-like-azure-vm-availability-sets-for-vms-that-i-will-use-for-configuration-manager"></a>Um dos motivos pelos quais estou mudando a infraestrutura para o Azure é a promessa de alta disponibilidade. Posso aproveitar as opções de alta disponibilidade como os conjuntos de disponibilidade de VM do Azure para VMs que usarei para o Configuration Manager?
Sim. Os conjuntos de disponibilidade de VM do Azure podem ser usados para funções redundantes do sistema de sites como pontos de distribuição ou pontos de gerenciamento.

Você também pode usá-los para os servidores do site do Configuration Manager. Por exemplo, os sites de administração central e os sites primários podem estar todos no mesmo conjunto de disponibilidade, o que pode ajudá-lo a garantir que eles não sejam reinicializados ao mesmo tempo.

### <a name="how-can-i-make-my-database-highly-available-can-i-use-azure-sql-database-or-do-i-have-to-use-microsoft-sql-server-in-a-vm"></a>Como torno meu banco de dados altamente disponível? Posso usar o Banco de Dados SQL do Azure? Ou preciso usar o Microsoft SQL Server em uma VM?
Você precisa usar o Microsoft SQL Server em uma VM. No momento, o Configuration Manager não dá suporte ao SQL Server do Azure. Mas você pode usar funcionalidades como Grupos de Disponibilidade AlwaysOn para seu SQL Server. Os [Grupos de Disponibilidade AlwaysOn](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database) são recomendados e têm suporte oficialmente a partir da versão 1602 do Configuration Manager.

### <a name="can-i-use-azure-load-balancers-with-site-system-roles-like-management-points--or-software-update-points"></a>Posso usar os balanceadores de carga do Azure com funções do sistema de sites como pontos de gerenciamento ou pontos de atualização de software?
Embora o Configuration Manager não seja testado com os balanceadores de carga do Azure, se a funcionalidade for transparente para o aplicativo, ele não deverá ter nenhum efeito adverso em operações normais.


## <a name="performance"></a>Desempenho
### <a name="what-factors-affect-performance-in-this-scenario"></a>Quais fatores afetam o desempenho nesse cenário?
O [tipo e o tamanho da VM do Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs), os discos da VM do Azure (é recomendado o Armazenamento Premium, especialmente para o SQL Server), a latência de rede e a velocidade são as áreas mais importantes.

### <a name="so-tell-me-more-about-azure-virtual-machines-what-size-vms-should-i-use"></a>Então, quero saber mais sobre as máquinas virtuais do Azure. Devo usar VMs de qual tamanho?
Em geral, o poder de computação (CPU e memória) precisa atender ao [hardware recomendado para o System Center Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware). Mas há algumas diferenças entre o hardware do computador regular e VMs do Azure, especialmente quando se trata dos discos que essas VMs usam.  O tamanho das VMs usadas depende do tamanho do seu ambiente, mas aqui estão algumas recomendações:
- Para implantações de produção de qualquer tamanho significativo, recomendamos VMs do Azure de classe “**S**”. Isso ocorre porque eles podem aproveitar os discos do Armazenamento Premium.  As VMs que não são da classe “S” usam o armazenamento de blobs e, em geral, não atenderão aos requisitos de desempenho necessários para a experiência de produção aceitável.
- Devem ser usados vários discos de Armazenamento Premium para uma escala maior e devem ser distribuídos no console de Gerenciamento de Disco do Windows para IOPS máximo.  
- É recomendável usar discos premium melhores ou vários discos premium durante a implantação de site inicial (como P30 em vez de P20 e 2xP30 em vez de 1xP30). Então, se seu site posteriormente precisar aumentar de tamanho de VM devido à carga adicional, você poderá aproveitar o CPU e a memória adicionais que o tamanho de VM maior fornece. Você também já terá discos instalados que podem aproveitar a taxa de transferência de IOPS adicional que o tamanho de VM maior permite.



As tabelas a seguir listam as contagens de disco iniciais sugeridas para utilizar em sites de administração central e primários para instalações de vários tamanhos:

**Banco de dados de site colocalizado** – site de administração central ou primário com o banco de dados do site no servidor do site:

| Clientes de desktop    |Tamanho de VM recomendado|Discos recomendados|
|--------------------|-------------------|-----------------|
|**Até 25 mil**       |   DS4_V2          |2xP30 (distribuído)  |
|**25 mil a 50 mil**      |   DS13_V2         |2xP30 (distribuído)  |
|**50 mil a 100 mil**     |   DS14_V2         |3xP30 (distribuído)  |


**Banco de dados de site remoto** – site de administração central ou primário com o banco de dados do site em um servidor remoto:

| Clientes de desktop    |Tamanho de VM recomendado|Discos recomendados |
|--------------------|-------------------|------------------|
|**Até 25 mil**       | Servidor do site: F4S </br>Servidor de banco de dados: DS12_V2 | Servidor do site: 1xP30 </br>Servidor de banco de dados: 2xP30 (distribuído)  |
|**25 mil a 50 mil**      | Servidor do site: F4S </br>Servidor de banco de dados: DS13_V2 | Servidor do site: 1xP30 </br>Servidor de banco de dados: 2xP30 (distribuído)   |
|**50 mil a 100 mil**     | Servidor do site: F8S </br>Servidor de banco de dados: DS14_V2 | Servidor de site: 2xP30 (distribuído)   </br>Servidor de banco de dados: 3xP30 (distribuído)   |

Veja a seguir um exemplo de configuração para clientes de 50 a 100 mil em discos DS14_V2 com 3xP30 em um volume distribuído com volumes lógicos separados para os arquivos de instalação e de banco de dados do Configuration Manager: ![VM)disks](media/vm_disks.png)  



## <a name="user-experience"></a>Experiência do usuário
### <a name="you-mention-that-user-experience-is-one-of-the-main-areas-of-importance-why-is-that"></a>Você mencionou que a experiência do usuário é uma das principais áreas de importância, por quê?
As decisões tomadas para rede, desempenho, disponibilidade e onde colocar seus servidores do site do Configuration Manager podem afetar os usuários diretamente. Acreditamos que uma mudança para o Azure deve ser transparente para os usuários para que eles não enfrentem uma alteração em suas interações diárias com o Configuration Manager.

### <a name="ok-i-get-it-i-plan-to-install-a-single-stand-alone-primary-site-on-an-azure-virtual-machine-and-i-want-to-make-sure-my-costs-are-low-should-i-place-remote-site-systems-like-management-points-distribution-points-and-software-update-points-on-azure-virtual-machines-as-well-or-on-premises"></a>OK, entendi. Planejo instalar um único site primário autônomo em uma máquina virtual do Azure e quero me certificar de que meu os custos são baixos. Deve colocar os sistemas de sites (remotos) (como pontos de gerenciamento, pontos de distribuição e pontos de atualização de software) em máquinas virtuais do Azure também ou localmente?
Exceto para a comunicação entre o servidor do site e um ponto de distribuição, essas comunicações servidor para servidor em um site podem ocorrer a qualquer momento e não usar mecanismos para controlar o uso da largura de banda da rede. Como você não pode controlar a comunicação entre sistemas de sites, todos os custos associados a essas comunicações devem ser considerados.

As velocidades e a latência de rede são outros fatores a serem considerados também. Redes lentas ou não confiáveis podem afetar a funcionalidade entre o servidor do site e sistemas de sites remotos, como também qualquer comunicação do cliente com os sistemas de sites. O número de clientes que usam um sistema de sites específico, bem como os recursos usados ativamente, também deve ser considerado.
Em geral, você pode aproveitar a diretriz normal uma vez que ela é relacionada aos sistemas de sites e links WAN como um ponto de partida. Em condições ideais, a taxa de transferência de rede selecionada e recebida entre o Azure e sua intranet será consistente com uma WAN bem conectada com uma rede rápida.

### <a name="what-about-content-distribution-and-content-management-should-standard-distribution-points-be-in-azure-or-on-premises-and-should-i-use-branchcache-or-pull-distribution-points-on-premises-or-should-i-make-exclusive-use-of-cloud-distribution-points"></a>E a distribuição de conteúdo e o gerenciamento de conteúdo? Os pontos de distribuição padrão devem estar no Azure ou locais e devo usar BranchCache ou pontos de distribuição por pull localmente? Ou devo fazer uso exclusivo de Pontos de Distribuição na Nuvem?
A abordagem de gerenciamento de conteúdo é muito semelhante à dos servidores do site e dos sistemas de sites.
- Se você usa uma conexão de rede rápida e confiável entre o Azure e sua intranet com um plano de dados ilimitado, hospedar os pontos de distribuição padrão no Azure pode ser uma opção.
-  Se você usa um plano de dados limitado e o custo da largura de banda é uma preocupação ou se a conexão de rede entre o Azure e sua intranet não é rápida ou pode não ser confiável, considere outras abordagens. Elas incluem a localização de pontos de distribuição por pull ou padrão localmente, bem como usando o BranchCache. O uso de pontos de distribuição baseados em nuvem também é uma opção, mas existem alguns limites sobre os tipos de conteúdo com suporte (por exemplo, não há suporte para pacotes de atualizações de software).

> [!NOTE]
>  Se o suporte a PXE for necessário, use pontos de distribuição locais (padrão ou pull) para responder às solicitações de inicialização. [No momento, não há suporte para o WDS ser executado em VMs do Azure](https://technet.microsoft.com/library/hh831764(v=ws.11).aspx).


### <a name="while-i-am-ok-with-the-limitations-of-cloud-based-distribution-points-i-dont-want-to-put-my-management-point-into-a-dmz-even-though-that-is-needed-to-support-my-internet-based-clients-do-i-have-any-other-options"></a>Embora eu esteja OK com as limitações dos pontos de distribuição baseados em nuvem, não quero colocar meu ponto de gerenciamento em um DMZ, mesmo que isso seja necessário para dar suporte aos meus clientes baseados na Internet. Tenho alguma outra opção?
Sim. Com o Configuration Manager versão 1610, apresentamos o [Gateway de gerenciamento de nuvem](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) como um recurso de pré-lançamento. (Esse recurso apareceu pela primeira vez na Technical Preview versão 1606 como o [Serviço de Proxy de Nuvem](/sccm/core/get-started/capabilities-in-technical-preview-1606#a-namecloudproxyacloud-proxy-service-for-managing-clients-on-the-internet).)

O **Gateway de Gerenciamento de Nuvem** fornece uma maneira simples de gerenciar clientes do Configuration Manager na Internet. O serviço, que é implantado no Microsoft Azure e requer uma assinatura do Azure, conecta-se à sua infraestrutura do Configuration Manager local usando uma nova função chamada ponto de conexão do gateway de gerenciamento de nuvem. Depois de implantado e configurado, os clientes podem acessar funções do sistema de sites do Configuration Manager locais independentemente de se eles estão conectados à rede privada interna ou na Internet.

Você pode começar a usar o gateway de gerenciamento de nuvem em seu ambiente e nos fornecer comentários para melhorá-lo. Para obter mais informações sobre os recursos de pré-lançamento, consulte [Usar recursos de pré-lançamento de atualizações](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkprereleasea-use-pre-release-features-from-updates).

### <a name="i-also-heard-that-you-have-another-new-feature-called-peer-cache-introduced-as-a-pre-release-feature-in-version-1610-is-that-different-than-branchcache-which-one-should-i-choose"></a>Também ouvi que você tem outro novo recurso chamado Cache de Sistema Par introduzido com um recurso de pré-lançamento na versão 1610. Isso é diferente do BranchCache? Qual devo escolher?
Sim, totalmente diferente. O [Cache de Sistema Par](/sccm/core/plan-design/hierarchy/client-peer-cache) é uma tecnologia do Configuration Manager totalmente nativa, em que o BranchCache é um recurso do Windows. Ambos podem ser úteis para você. O BranchCache usa uma difusão para localizar o conteúdo necessário, enquanto o Cache de Sistema Par usa configurações de grupo de limite e fluxo de trabalho de distribuição regulares do Configuration Manager.

Você pode configurar qualquer cliente como uma origem de Cache de Sistema Par. Então, quando os pontos de gerenciamento fornecem aos clientes informações sobre os locais de fonte de conteúdo, eles fornecem detalhes sobre os pontos de distribuição e quaisquer origens de Cache de Sistema Par que contenham o conteúdo de que o cliente precisa.


## <a name="cost"></a>Custo
### <a name="ok-tell-me-a-bit-about-the-cost-will-this-be-a-cost-effective-solution-for-me"></a>OK, quero saber um pouco sobre o custo. Essa será uma solução econômica para mim?
Difícil dizer, uma vez que cada ambiente é diferente. O melhor a se fazer é determinar o custo do seu ambiente usando a calculadora de preços do Microsoft Azure:  https://azure.microsoft.com/pricing/calculator/

## <a name="additional-resources"></a>Recursos adicionais
**Conceitos básicos:** http://azure.microsoft.com/documentation/articles/fundamentals-introduction-to-azure/

**Tipos de computadores das VMs do Azure:**
 - Tamanhos de computadores do Azure: https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs/  
 - Preços de VM: http://azure.microsoft.com/pricing/details/virtual-machines/  
 - Preços de armazenamento: http://azure.microsoft.com/pricing/details/storage/

**Considerações sobre desempenho de disco:**    
 - Introdução de Disco Premium:  http://azure.microsoft.com/blog/2014/12/11/introducing-premium-storage-high-performance-storage-for-azure-virtual-machine-workloads/  
 - Mais informações sobre o Disco Premium: http://azure.microsoft.com/documentation/articles/storage-premium-storage-preview-portal/   
 - Coleção prática de gráficos para as metas de desempenho e tamanhos máximos para o armazenamento: https://azure.microsoft.com/documentation/articles/storage-scalability-targets/  
 - Outra introdução, mais alguns dados interessantes supergeeks sobre como o Armazenamento Premium funciona nos bastidores:  http://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2/

**Disponibilidade:**
 - SLA do tempo de ativação de IaaS do Azure: https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/  
 - Conjuntos de disponibilidade explicados: https://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability/

**Conectividade:**
 - ExpressRoute vs. VPN do Azure: http://azure.microsoft.com/blog/2014/06/10/expressroute-or-virtual-network-vpn-whats-right-for-me/
 - Preços do ExpressRoute: http://azure.microsoft.com/pricing/details/expressroute/
 - Mais informações sobre o ExpressRoute: http://azure.microsoft.com/documentation/articles/expressroute-introduction/

 
