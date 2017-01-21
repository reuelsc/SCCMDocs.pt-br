---
title: Tamanho e escala | Microsoft Docs
description: "Identifique o número de funções de sites e do sistema de sites que você precisará para dar suporte aos dispositivos em seu ambiente do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 453d934d693d58e98cf800988dff702400daaf95

---
# <a name="size-and-scale-numbers-for-system-center-configuration-manager"></a>Números de tamanho e escala para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*



Cada implantação do System Center Configuration Manager tem um número máximo de sites, funções do sistema de sites e dispositivos aos quais ela pode dar suporte. Esses números variam conforme sua estrutura de hierarquia (os tipos e o número de sites usados) e as funções do sistema de sites implantados.  As informações nos seguintes assuntos podem ajudar a identificar o número de funções de sites e do sistema de sites que será necessário para dar suporte aos dispositivos que você pretende gerenciar com o seu ambiente.

Use as informações neste tópico com as informações nos seguintes artigos:
-   [Hardware recomendado](../../../core/plan-design/configs/recommended-hardware.md)
-   [Sistemas operacionais com suporte para servidores de sistema de sites](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
-   [Sistemas operacionais com suporte para clientes e dispositivos](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)
-   [Pré-requisitos de sites e do sistema de sites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)

Os números com suporte neste artigo são baseados no uso de hardware recomendado para o Configuration Manager. Quando você não usa o hardware recomendado, o desempenho dos sistemas de sites pode ser prejudicado e talvez não atenda aos níveis de suporte indicados.

##  <a name="a-namebkmksitesystemscalea-site-types"></a><a name="bkmk_SiteSystemScale"></a> Tipos de site  
 **Site de administração central:**  

-   Um site de administração central pode dar suporte a até 25 sites primários filho.  

**Site primário:**  

-   Cada site primário fornece suporte a até 250 sites secundários.  

-   O número de sites secundários por site primário se baseia em conexões de WAN (rede de longa distância) continuamente conectadas e confiáveis. Para os locais que têm menos de 500 clientes, considere um ponto de distribuição em vez de um site secundário.  

 Para saber mais sobre os números de clientes e dispositivos com suporte em um site primário, consulte [Números de clientes para sites e hierarquias](#bkmk_clientnumbers) neste tópico.  

**Site secundário:**  

-   Sites secundários não oferecem suporte a sites filhos.  

-   Um site de administração central pode dar suporte a até 25 sites primários filho.  

**Ponto de sites da Web do Catálogo de Aplicativos:**  

-   É possível instalar várias instâncias do ponto de sites da Web do catálogo de aplicativos em sites primários.  

    > [!TIP]  
    >  Como melhor prática, instale o ponto de sites da Web do catálogo de aplicativos e o ponto de serviços Web do catálogo de aplicativos juntos no mesmo sistema de sites quando eles fornecerem serviço aos clientes que estejam na intranet.  

    -   Para melhorar o desempenho, planeje o suporte a até 50.000 clientes por instância.  

    -   Cada instância desta função do sistema de sites dá suporte ao número máximo de clientes com suporte pela hierarquia.  

## <a name="a-namebkmkrolesa-site-system-roles"></a><a name="bkmk_roles"></a> Site system roles    

**Ponto de serviços Web do Catálogo de Aplicativos:**  

-   É possível instalar várias instâncias do ponto de serviços Web do catálogo de aplicativos em sites primários.  

    > [!TIP]  
    >  Como melhor prática, instale o ponto de sites da Web do catálogo de aplicativos e o ponto de serviços Web do catálogo de aplicativos juntos no mesmo sistema de sites quando eles fornecerem serviço aos clientes que estejam na intranet.  

    -   Para melhorar o desempenho, planeje o suporte a até 50.000 clientes por instância.  

    -   Cada instância desta função do sistema de sites dá suporte ao número máximo de clientes com suporte pela hierarquia.  

**Ponto de Distribuição:**  

-   Pontos de distribuição por site:  

    -   Cada site primário e secundário dá suporte a até 250 pontos de distribuição.  

    -   Cada site primário e secundário dão suporte a até 2.000 pontos de distribuição adicionais configurados como pontos de distribuição de recepção. **Por exemplo**, um único site primário dá suporte a 2250 pontos de distribuição quando 2000 deles são configurados como pontos de distribuição de pull.  

    -   Cada ponto de distribuição dá suporte a conexões de até 4.000 clientes.  

    -   Um ponto de distribuição de recepção atua como um cliente quando acessa o conteúdo de um ponto de distribuição de origem.  

-   Cada site primário dá suporte a um total combinado de até 5.000 pontos de distribuição. Este total inclui todos os pontos de distribuição no site primário e todos os pontos de distribuição que pertencem aos sites secundários filho do site primário.  

-   Cada ponto de distribuição dá suporte a um total combinado de até 10.000 pacotes e aplicativos.  

> [!WARNING]  
>  O número real de clientes aos quais um ponto de distribuição pode dar suporte depende da velocidade da rede e da configuração de hardware do computador do ponto de distribuição.  
>   
>  O número de pontos de distribuição de recepção aos quais um ponto de distribuição de origem dá suporte depende da velocidade da configuração de rede e de hardware do computador do ponto de distribuição de origem, mas também é afetado pela quantidade de conteúdo implantado. Isso ocorre porque, diferentemente dos clientes que normalmente acessam o conteúdo em momentos diferentes durante uma janela de implantações, todo o ponto de distribuição de recepção solicita o conteúdo ao mesmo tempo e pode solicitar todo o conteúdo disponível e não apenas o conteúdo que se aplica a ele, como faria um cliente. Quando uma carga de processamento excessiva for colocada em um ponto de distribuição de origem, isso poderá causar atrasos inesperados na distribuição do conteúdo para os pontos de distribuição esperados em seu ambiente.  


**Ponto de status de fallback:**  

-   Cada ponto de status de fallback pode dar suporte a até 100.000 clientes.  

**Ponto de gerenciamento:**  

-   Cada site primário dá suporte a até 15 pontos de gerenciamento.  

    > [!TIP]  
    >  Não instale os pontos de gerenciamento em servidores que estejam em um link lento partindo do servidor do site primário ou do servidor de banco de dados do site.  

-   Cada site secundário dá suporte a um único ponto de gerenciamento que deve ser instalado no servidor do site secundário.  

 Para saber mais sobre os números de clientes e dispositivos com suporte em ponto de gerenciamento, consulte a seção [Pontos de gerenciamento](#bkmk_mp) neste tópico.  

**Ponto de atualização de software:**  

-   Um ponto de atualização de software instalado no servidor do site pode dar suporte a até 25.000 clientes.  

-   Um ponto de atualização de software que é remoto do servidor do site pode dar suporte a até 150.000 clientes quando o computador remoto atende aos requisitos do WSUS para dar suporte a esse número de clientes.  

-   Por padrão, o Configuration Manager não dá suporte à configuração de pontos de atualização de software como clusters de NLB. No entanto, é possível usar o SDK do Configuration Manager para configurar até quatro pontos de atualização de software em um cluster de NLB.  

##  <a name="a-namebkmkclientnumbersa-client-numbers-for-sites-and-hierarchies"></a><a name="bkmk_clientnumbers"></a> Números de cliente para sites e hierarquias  
 Use as informações a seguir para determinar para quantos clientes, e de quais tipos, você pode oferecer suporte em um site ou em uma hierarquia.  

###  <a name="a-namebkmkcasa-hierarchy-with-a-central-administration-site"></a><a name="bkmk_cas"></a> Hierarquia com um site de administração central  
Um site de administração central oferece suporte a uma quantidade total de dispositivos que inclui até o número de dispositivos listados para os três grupos a seguir:  

-   700.000 desktops (computadores que executam Windows, Linux e UNIX)  

-   25.000 dispositivos que executam Mac e Windows CE 7.0  

-   Um dos seguintes, dependendo de como sua implantação oferece suporte ao gerenciamento de dispositivos móveis:  

    -   100.000 dispositivos gerenciados com o MDM local  

    -   300.000 dispositivos baseados em cluster  

 Por exemplo, em uma hierarquia você pode dar suporte a 700.000 desktops, até 25.000 clientes Mac e Windows CE 7.0 e até 300.000 dispositivos baseados em nuvem quanto integra o Microsoft Intune, somando 1.025.000 dispositivos.  Se você oferecer suporte a dispositivos gerenciados pelo MDM local, o total para a hierarquia será de 825.000 dispositivos.  

> [!IMPORTANT]  
>  Em uma hierarquia na qual o site de administração central usa uma edição Standard do SQL Server, a hierarquia oferece suporte a 50.000 dispositivos e desktops no máximo. A edição do SQL Server em uso em um site primário autônomo não limita a capacidade desses sites a fim de oferecer suporte ao número especificado de clientes.  


###  <a name="a-namebkmkchipria-child-primary-site"></a><a name="bkmk_chipri"></a> Site primário filho  
Cada site primário autônomo em uma hierarquia com um site de administração central oferece suporte ao seguinte:  

-   150.000 clientes e dispositivos no total, sem limitar-se a um grupo ou tipo específico, contanto que o suporte não exceda o número com suporte para a hierarquia  

Por exemplo, um site primário que dá suporte a 25.000 computadores que executam o Mac e Windows CE 7.0 (pois este é o limite para uma hierarquia), pode dar suporte a um 125.000 computadores desktops adicionais, elevando o número total de dispositivos com suporte até limite máximo com suporte em sites primários filho de 150.000.

###  <a name="a-namebkmkpria-stand-alone-primary-site"></a><a name="bkmk_pri"></a> Site primário autônomo  
Um site primário autônomo oferece suporte à seguinte quantidade de dispositivos:  

-   175.000 clientes e dispositivos no total, não podendo exceder:  

    -   150.000 desktops (computadores que executam Windows, Linux e UNIX)  

    -   25.000 dispositivos que executam Mac e Windows CE 7.0  

    -   Um dos seguintes, dependendo de como sua implantação oferece suporte ao gerenciamento de dispositivos móveis:  

        -   50.000 dispositivos gerenciados por você com o MDM local  

        -   150.000 dispositivos baseados em nuvem  

Por exemplo, um site primário autônomo que oferece suporte a 150.000 desktops e 10.000 clientes Mac ou Windows CE 7.0 pode dar suporte a apenas um 15.000 dispositivos adicionais. Esses dispositivos podem ter base em nuvem ou serem gerenciados com o MDM local.  

###  <a name="a-namebkmkseca-secondary-sites"></a><a name="bkmk_sec"></a> Sites secundários  
Sites secundários oferecem suporte ao seguinte:  

-   15.000 desktops (computadores que executam Windows, Linux e UNIX)  

###  <a name="a-namebkmkmpa-management-points"></a><a name="bkmk_mp"></a> Pontos de gerenciamento  
Cada gerenciamento pode dar suporte a seguinte quantidade de dispositivos:  

-   25.000 clientes e dispositivos no total, não podendo exceder:  

    -   25.000 desktops (computadores que executam Windows, Linux e UNIX)  

    -   Uma das seguintes opções (não ambas):  

        -   10.000 dispositivos gerenciados usando o MDM local  

        -   10.000 dispositivos que executam Mac e Windows CE 7.0  



<!--HONumber=Dec16_HO3-->


