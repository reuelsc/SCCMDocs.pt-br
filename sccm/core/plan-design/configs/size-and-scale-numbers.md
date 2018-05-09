---
title: Tamanho e escala
titleSuffix: Configuration Manager
description: Determine o número de funções do sistema de sites e de sites necessários para dar suporte aos dispositivos no ambiente.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b995687e330fe4beca26da83ee29ddc504c38e3a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="size-and-scale-numbers-for-system-center-configuration-manager"></a>Números de tamanho e escala para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*



Cada implantação do Configuration Manager tem um número máximo de sites, funções do sistema de sites e dispositivos aos quais ela pode dar suporte. Esses números variam conforme a estrutura de hierarquia, quais tipos e números de sites são usados e as funções do sistema de sites implantadas. As informações deste artigo podem ajudá-lo a determinar o número de funções do sistema de sites e de sites necessários para dar suporte aos dispositivos que você pretende gerenciar.

Use as informações neste tópico em conjunto com as informações nos seguintes artigos:
-   [Hardware recomendado](../../../core/plan-design/configs/recommended-hardware.md)
-   [Sistemas operacionais com suporte para servidores de sistema de sites](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
-   [Sistemas operacionais com suporte para clientes e dispositivos](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)
-   [Pré-requisitos de sites e do sistema de sites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)


Esses números de suporte baseiam-se no uso do hardware recomendado para o Configuration Manager. Eles também se baseiam nas configurações padrão de todos os recursos disponíveis do Configuration Manager. Quando você não usa o hardware recomendado ou usa configurações personalizadas mais agressivas, o desempenho dos sistemas de sites pode ser prejudicado. Os sistemas de sites poderão não atender os níveis de suporte indicados. (Um exemplo de configurações de cliente mais agressivas é a execução do inventário de hardware ou software com mais frequência do que os padrões de uma vez a cada sete dias.)

##  <a name="bkmk_SiteSystemScale"></a> Tipos de site  

### <a name="central-administration-site"></a>Site de administração central  

-   Um site de administração central pode dar suporte a até 25 sites primários filho.  


### <a name="primary-site"></a>Site primário  

-   Cada site primário fornece suporte a até 250 sites secundários.  

-   O número de sites secundários por site primário se baseia em conexões de WAN (rede de longa distância) continuamente conectadas e confiáveis. Para os locais que têm menos de 500 clientes, considere um ponto de distribuição em vez de um site secundário.  

 Para obter mais informações sobre os números de clientes e os dispositivos para os quais um site primário pode dar suporte, consulte [Números de clientes para sites e hierarquias](#bkmk_clientnumbers).  


### <a name="secondary-site"></a>Site secundário  

-   Sites secundários não dão suporte a sites filhos.  



## <a name="bkmk_roles"></a> Site system roles    


### <a name="application-catalog-web-service-point"></a>Ponto de serviços Web do Catálogo de Aplicativos  

-   É possível instalar várias instâncias do ponto de serviços Web do catálogo de aplicativos em sites primários.  

    > [!TIP]  
    >  Como melhor prática, instale o ponto de sites da Web do catálogo de aplicativos e o ponto de serviços Web do catálogo de aplicativos juntos no mesmo sistema de sites quando eles fornecerem serviço aos clientes que estejam na intranet.  

    -   Para melhorar o desempenho, planeje o suporte a até 50.000 clientes por instância.  

    -   Cada instância desta função do sistema de sites dá suporte ao número máximo de clientes com suporte pela hierarquia.  


### <a name="application-catalog-website-point"></a>Ponto de sites da Web do Catálogo de Aplicativos  

-   É possível instalar várias instâncias do ponto de sites da Web do catálogo de aplicativos em sites primários.  

    > [!TIP]  
    >  Como melhor prática, instale o ponto de sites da Web do catálogo de aplicativos e o ponto de serviços Web do catálogo de aplicativos juntos no mesmo sistema de sites quando eles fornecerem serviço aos clientes que estejam na intranet.  

    -   Para melhorar o desempenho, planeje o suporte a até 50.000 clientes por instância.  

    -   Cada instância desta função do sistema de sites dá suporte ao número máximo de clientes com suporte pela hierarquia.  


### <a name="bkmk_cmg"></a> Gateway de gerenciamento de nuvem

- Instale várias instâncias do CMG (gateway de gerenciamento de nuvem) em sites primários ou no site de administração central.  

    > [!Tip]  
    > Em uma hierarquia, crie o CMG no site de administração central.  

    - Um CMG dá suporte a 16 instâncias de VM (máquina virtual) no serviço de nuvem do Azure.  

    - Cada instância de VM do CMG dá suporte a 6.000 conexões de cliente simultâneas. Quando o CMG está sob alta carga devido a ter mais do que o número de clientes compatíveis, ele ainda manipula as solicitações, mas pode haver atraso.  

Para obter mais informações, consulte [desempenho e escala](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#performance-and-scale) do CMG


### <a name="cloud-management-gateway-connection-point"></a>Ponto de conexão do gateway de gerenciamento de nuvem

- Instale várias instâncias do ponto de conexão do CMG em sites primários.  

- Um ponto de conexão do CMG pode dar suporte a um CMG com até quatro instâncias de VM. Se o CMG tiver mais de quatro instâncias de VM, adicione um segundo ponto de conexão do CMG para o balanceamento de carga. Um CMG com 16 instâncias de VM deve ser vinculado a quatro pontos de conexão do CMG.

Para obter mais informações, consulte [desempenho e escala](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#performance-and-scale) do CMG


### <a name="distribution-point"></a>Ponto de distribuição  

-   Pontos de distribuição por site:  

    -   Cada site primário e secundário dá suporte a até 250 pontos de distribuição.  

    -   Cada site primário e secundário dá suporte a até 2000 pontos de distribuição adicionais configurados como pontos de distribuição pull. **Por exemplo**, um único site primário dá suporte a 2250 pontos de distribuição quando 2000 deles são configurados como pontos de distribuição de pull.  

    -   Cada ponto de distribuição dá suporte a conexões de até 4.000 clientes.  

    -   Um ponto de distribuição pull atua como um cliente quando acessa o conteúdo de um ponto de distribuição de origem.  

-   Cada site primário dá suporte a um total combinado de até 5.000 pontos de distribuição. Este total inclui todos os pontos de distribuição no site primário e todos os pontos de distribuição que pertencem aos sites secundários filho do site primário.  

-   Cada ponto de distribuição dá suporte a um total combinado de até 10.000 pacotes e aplicativos.  

> [!WARNING]  
>  O número real de clientes aos quais um ponto de distribuição pode dar suporte depende da velocidade da rede e da configuração de hardware do servidor.  
>   
>  De maneira semelhante, o número de pontos de distribuição pull aos quais um ponto de distribuição de origem pode dar suporte depende da velocidade da rede e da configuração de hardware do ponto de distribuição de origem. Mas esse número também é afetado pela quantidade de conteúdo que você implantou. Esse efeito ocorre porque, ao contrário dos clientes que normalmente acessam o conteúdo em momentos diferentes durante a implantação, todos os pontos de distribuição pull solicitam o conteúdo ao mesmo tempo. Os pontos de distribuição pull podem solicitar todo o conteúdo disponível, não apenas o conteúdo aplicável a eles. Quando você coloca uma alta carga de processamento em um ponto de distribuição de origem, pode haver atrasos inesperados na distribuição do conteúdo para os pontos de distribuição de destino.  


### <a name="fallback-status-point"></a>Ponto de status de fallback  

-   Cada ponto de status de fallback pode dar suporte a até 100.000 clientes.  


### <a name="management-point"></a>Ponto de gerenciamento  

-   Cada site primário dá suporte a até 15 pontos de gerenciamento.  

    > [!TIP]  
    >  Não instale os pontos de gerenciamento em servidores que estão em um link lento partindo do servidor do site primário ou do servidor de banco de dados do site.  

-   Cada site secundário dá suporte a um único ponto de gerenciamento que deve ser instalado no servidor do site secundário.  

 Para obter informações sobre os números de clientes e os dispositivos compatíveis com um ponto de gerenciamento, consulte a seção [Pontos de gerenciamento](#bkmk_mp).  


### <a name="software-update-point"></a>Ponto de atualização de software  

-   Um ponto de atualização de software instalado no servidor do site pode dar suporte a até 25.000 clientes.   

-   Um ponto de atualização de software que é remoto do servidor do site pode dar suporte a até 150.000 clientes quando o computador remoto atende aos requisitos do WSUS (Windows Server Update Services) para dar suporte a esse número de clientes.  

-   Por padrão, o Configuration Manager não dá suporte à configuração de pontos de atualização de software como clusters de NLB (Balanceamento de Carga de Rede). No entanto, é possível usar o SDK do Configuration Manager para configurar até quatro pontos de atualização de software em um cluster de NLB.  



##  <a name="bkmk_clientnumbers"></a> Números de cliente para sites e hierarquias  
 Use as informações a seguir para determinar para quantos clientes e quais tipos de cliente, você pode dar suporte em um site ou em uma hierarquia.  


###  <a name="bkmk_cas"></a> Hierarquia com um site de administração central  
Um site de administração central oferece suporte a uma quantidade total de dispositivos que inclui até o número de dispositivos listados para os três grupos a seguir:  

-   700.000 desktops (computadores que executam Windows, Linux e UNIX). Consulte também, suporte para [dispositivos inseridos](#embedded).

-   25.000 dispositivos que executam Mac e Windows CE 7.0  

-   Um dos seguintes, dependendo de como sua implantação dá suporte ao MDM (gerenciamento de dispositivo móvel):  

    -   100.000 dispositivos que você gerencia usando o MDM local  

    -   300.000 dispositivos baseados em cluster  

 Por exemplo, em uma hierarquia, você pode dar suporte a 700.000 desktops, até 25.000 dispositivos Mac e Windows CE 7.0 e até 300.000 dispositivos baseados em nuvem ao integrar o Microsoft Intune. Essa hierarquia dá suporte a um total de 1.025.000 dispositivos. Se você der suporte a dispositivos gerenciados pelo MDM local, o total para essa hierarquia será de 825.000 dispositivos.  

> [!IMPORTANT]  
>  Em uma hierarquia na qual o site de administração central usa uma edição Standard do SQL Server, a hierarquia dá suporte a 50.000 dispositivos e desktops no máximo. Para dar suporte a mais de 50.000 dispositivos e desktops, é necessário usar uma edição Enterprise do SQL Server. Esse requisito se aplica somente a um site de administração central. Ele não se aplica a um site primário autônomo nem a um site primário filho. A edição do SQL Server usada para um site primário não limita sua capacidade de dar suporte ao número indicado de clientes.   


 A edição do SQL Server em uso em um site primário autônomo não limita a capacidade desse site a fim de dar suporte ao número especificado de clientes.  


###  <a name="bkmk_chipri"></a> Site primário filho  
Cada site primário filho em uma hierarquia com um site de administração central dá suporte ao seguinte número de clientes:  

-   150.000 clientes e dispositivos no total que não se limitam a um grupo ou tipo específico, contanto que o suporte não exceda o número com suporte para a hierarquia. Consulte também, suporte para [dispositivos inseridos](#embedded).

Por exemplo, um site primário dá suporte a 25.000 dispositivos Mac e Windows CE 7.0. Esse número é o limite de uma hierarquia. Em seguida, esse site primário pode dar suporte a mais 125.000 computadores desktop. O número total de dispositivos compatíveis com o site primário filho é o limite máximo compatível de 150.000.


###  <a name="bkmk_pri"></a> Site primário autônomo  
Um site primário autônomo oferece suporte à seguinte quantidade de dispositivos:  

-   175.000 clientes e dispositivos no total, não podendo exceder:  

    -   150.000 desktops (computadores que executam Windows, Linux e UNIX). Consulte também, suporte para [dispositivos inseridos](#embedded).

    -   25.000 dispositivos que executam Mac e Windows CE 7.0

    -   Um dos seguintes, dependendo de como sua implantação oferece suporte ao gerenciamento de dispositivos móveis:  

        -   50.000 dispositivos que você gerencia usando o MDM local  

        -   150.000 dispositivos baseados em nuvem  


Por exemplo, um site primário autônomo que dá suporte a 150.000 desktops e 10.000 Mac ou Windows CE 7.0 pode dar suporte a apenas 15.000 dispositivos adicionais. Esses dispositivos podem ser baseados em nuvem ou serem gerenciados usando o MDM local.  


### <a name="embedded"></a> Sites primários e dispositivos Windows Embedded
Os sites primários dão suporte aos dispositivos Windows Embedded que têm o FBWF (Filtros de Gravação Baseado em Arquivo) habilitado. Quando dispositivos inseridos não têm filtros de gravação habilitados, um site primário pode dar suporte a um número de dispositivos inseridos que chega até o número permitido de dispositivos para esse site. Do número total de dispositivos aos quais um site primário dá suporte, um máximo de 10.000 desses dispositivos pode ser Windows Embedded. Esses dispositivos precisam ser configurados para as exceções listadas na observação importante encontrada em [Planejando a implantação de cliente em dispositivos Windows Embedded](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices). Um site primário dá suporte a apenas 3.000 dispositivos Windows Embedded com EWF habilitado e que não estão configurados para as exceções.


###  <a name="bkmk_sec"></a> Sites secundários  
Os sites secundários dão suporte ao seguinte número de dispositivos:  

-   15.000 desktops (computadores que executam Windows, Linux e UNIX)  


###  <a name="bkmk_mp"></a> Pontos de gerenciamento  
Cada ponto de gerenciamento pode dar suporte à seguinte quantidade de dispositivos:  

-   25.000 clientes e dispositivos no total, não podendo exceder:  

    -   25.000 desktops (computadores que executam Windows, Linux e UNIX)  

    -   Uma das seguintes opções (não ambas):  

        -   10.000 dispositivos que são gerenciados usando o MDM local  

        -   10.000 dispositivos que executam clientes Mac e Windows CE 7.0
