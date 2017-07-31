---
title: Tamanho e escala | Microsoft Docs
description: "Identifique o número de funções do sistema de sites e de sites que você precisará para dar suporte aos dispositivos em seu ambiente do System Center Configuration Manager."
ms.custom: na
ms.date: 07/24/2017
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
ms.translationtype: HT
ms.sourcegitcommit: 5945abb49fe06c59355805aa94b04d0d445ecbc3
ms.openlocfilehash: f539e2d282b56e56a9c58c773788325b27ea6b37
ms.contentlocale: pt-br
ms.lasthandoff: 07/24/2017

---
# <a name="size-and-scale-numbers-for-system-center-configuration-manager"></a>Números de tamanho e escala para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*



Cada implantação do System Center Configuration Manager tem um número máximo de sites, funções do sistema de sites e dispositivos aos quais ela pode dar suporte. Esses números variam conforme sua estrutura de hierarquia (os tipos e os números de sites usados) e as funções do sistema de sites implantados.  As informações nas seguintes áreas podem ajudar a identificar o número de funções de sites e do sistema de sites que será necessário para dar suporte aos dispositivos que você pretende gerenciar com o seu ambiente.

Use as informações neste tópico em conjunto com as informações nos seguintes artigos:
-   [Hardware recomendado](../../../core/plan-design/configs/recommended-hardware.md)
-   [Sistemas operacionais com suporte para servidores de sistema de sites](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
-   [Sistemas operacionais com suporte para clientes e dispositivos](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)
-   [Pré-requisitos de sites e do sistema de sites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)


Os números de suporte a seguir baseiam-se no uso do hardware recomendado para o Configuration Manager e as configurações padrão para todos os recursos disponíveis do Configuration Manager. Quando você não usar o hardware recomendado ou usar as configurações personalizadas de mais agressivas (como executar o inventário de hardware ou software com mais frequência do que os padrões de uma vez a cada sete dias), o desempenho dos sistemas de sites poderá ser degradado e poderão não atingir os níveis de suporte definidos.

##  <a name="bkmk_SiteSystemScale"></a> Tipos de site  
 **Site de administração central:**  

-   Um site de administração central pode dar suporte a até 25 sites primários filho.  

**Site primário:**  

-   Cada site primário fornece suporte a até 250 sites secundários.  

-   O número de sites secundários por site primário se baseia em conexões de WAN (rede de longa distância) continuamente conectadas e confiáveis. Para os locais que têm menos de 500 clientes, considere um ponto de distribuição em vez de um site secundário.  

 Para saber mais sobre os números de clientes e dispositivos com suporte em um site primário, consulte [Números de clientes para sites e hierarquias](#bkmk_clientnumbers) neste tópico.  

**Site secundário:**  

-   Sites secundários não dão suporte a sites filhos.  

-   Um site de administração central pode dar suporte a até 25 sites primários filho.  

**Ponto de sites da Web do Catálogo de Aplicativos:**  

-   É possível instalar várias instâncias do ponto de sites da Web do catálogo de aplicativos em sites primários.  

    > [!TIP]  
    >  Como melhor prática, instale o ponto de sites da Web do catálogo de aplicativos e o ponto de serviços Web do catálogo de aplicativos juntos no mesmo sistema de sites quando eles fornecerem serviço aos clientes que estejam na intranet.  

    -   Para melhorar o desempenho, planeje o suporte a até 50.000 clientes por instância.  

    -   Cada instância desta função do sistema de sites dá suporte ao número máximo de clientes com suporte pela hierarquia.  

## <a name="bkmk_roles"></a> Site system roles    

**Ponto de serviços Web do Catálogo de Aplicativos:**  

-   É possível instalar várias instâncias do ponto de serviços Web do catálogo de aplicativos em sites primários.  

    > [!TIP]  
    >  Como melhor prática, instale o ponto de sites da Web do catálogo de aplicativos e o ponto de serviços Web do catálogo de aplicativos juntos no mesmo sistema de sites quando eles fornecerem serviço aos clientes que estejam na intranet.  

    -   Para melhorar o desempenho, planeje o suporte a até 50.000 clientes por instância.  

    -   Cada instância desta função do sistema de sites dá suporte ao número máximo de clientes com suporte pela hierarquia.  

**Ponto de distribuição:**  

-   Pontos de distribuição por site:  

    -   Cada site primário e secundário dá suporte a até 250 pontos de distribuição.  

    -   Cada site primário e secundário dá suporte a até 2000 pontos de distribuição adicionais configurados como pontos de distribuição pull. **Por exemplo**, um único site primário dá suporte a 2250 pontos de distribuição quando 2000 deles são configurados como pontos de distribuição de pull.  

    -   Cada ponto de distribuição dá suporte a conexões de até 4.000 clientes.  

    -   Um ponto de distribuição pull atua como um cliente quando acessa o conteúdo de um ponto de distribuição de origem.  

-   Cada site primário dá suporte a um total combinado de até 5.000 pontos de distribuição. Este total inclui todos os pontos de distribuição no site primário e todos os pontos de distribuição que pertencem aos sites secundários filho do site primário.  

-   Cada ponto de distribuição dá suporte a um total combinado de até 10.000 pacotes e aplicativos.  

> [!WARNING]  
>  O número real de clientes aos quais um ponto de distribuição pode dar suporte depende da velocidade da rede e da configuração de hardware do computador do ponto de distribuição.  
>   
>  O número de pontos de distribuição pull aos quais um ponto de distribuição pode dar suporte depende de maneira semelhante da velocidade da rede e da configuração de hardware do computador do ponto de distribuição de origem. Mas esse número também é afetado pela quantidade de conteúdo que você implantou. Isso ocorre porque, diferentemente dos clientes que normalmente acessam o conteúdo em momentos diferentes durante implantação, todos os pontos de distribuição pull solicitam o conteúdo ao mesmo tempo e podem solicitar todo o conteúdo disponível, não apenas o conteúdo aplicável a ele, como faria um cliente. Quando uma carga de processamento excessiva for colocada em um ponto de distribuição de origem, poderá haver atrasos inesperados na distribuição do conteúdo para os pontos de distribuição esperados em seu ambiente.  


**Ponto de status de fallback:**  

-   Cada ponto de status de fallback pode dar suporte a até 100.000 clientes.  

**Ponto de gerenciamento:**  

-   Cada site primário dá suporte a até 15 pontos de gerenciamento.  

    > [!TIP]  
    >  Não instale os pontos de gerenciamento em servidores que estejam em um link lento partindo do servidor do site primário ou do servidor de banco de dados do site.  

-   Cada site secundário dá suporte a um único ponto de gerenciamento que deve ser instalado no servidor do site secundário.  

 Para saber mais sobre os números de clientes e dispositivos com suporte em um ponto de gerenciamento, consulte a seção [Pontos de gerenciamento](#bkmk_mp) neste tópico.  

**Ponto de atualização de software:**  

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

 Por exemplo, em uma hierarquia você pode dar suporte a 700.000 desktops, até 25.000 clientes Mac e Windows CE 7.0 e até 300.000 dispositivos baseados em nuvem quando integra o Microsoft Intune, somando 1.025.000 dispositivos. Se você der suporte a dispositivos gerenciados pelo MDM local, o total para a hierarquia será de 825.000 dispositivos.  

> [!IMPORTANT]  
>  Em uma hierarquia na qual o site de administração central usa uma edição Standard do SQL Server, a hierarquia dá suporte a 50.000 dispositivos e desktops no máximo. A edição do SQL Server em uso em um site primário autônomo não limita a capacidade desse site a fim de dar suporte ao número especificado de clientes.  


###  <a name="bkmk_chipri"></a> Site primário filho  
Cada site primário autônomo em uma hierarquia com um site de administração central oferece suporte ao seguinte:  

-   150.000 clientes e dispositivos no total que não se limitam a um grupo ou tipo específico, contanto que o suporte não exceda o número com suporte para a hierarquia. Consulte também, suporte para [dispositivos inseridos](#embedded).

Por exemplo, um site primário que dá suporte para até 25.000 computadores que executam Mac e Windows CE 7.0 (pois esse é o limite para uma hierarquia) pode dar suporte a 125.000 computadores desktop adicionais. Isso traz o número total de dispositivos com suporte até o limite máximo com suporte de 150.000 do site primário filho.

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
Os sites primários dão suporte aos dispositivos Windows Embedded que têm o FBWF (Filtros de Gravação Baseado em Arquivo) habilitado. Quando dispositivos inseridos não têm filtros de gravação habilitados, um site primário pode dar suporte a um número de dispositivos inseridos de até o número permitido de dispositivos para esse site. Do número total de dispositivos com suporte por um site primário, um máximo de 10.000 deles pode ser dispositivos Windows Embedded quando esses dispositivos são configurados para as exceções listadas na observação importante localizada em [Planejamento para implantação do cliente para dispositivos Windows Embedded](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices). Um site primário dá suporte a apenas 3.000 dispositivos Windows Embedded com EWF habilitado e que não estão configurados para as exceções.

###  <a name="bkmk_sec"></a> Sites secundários  
Sites secundários oferecem suporte ao seguinte:  

-   15.000 desktops (computadores que executam Windows, Linux e UNIX)  

###  <a name="bkmk_mp"></a> Pontos de gerenciamento  
Cada ponto de gerenciamento pode dar suporte à seguinte quantidade de dispositivos:  

-   25.000 clientes e dispositivos no total, não podendo exceder:  

    -   25.000 desktops (computadores que executam Windows, Linux e UNIX)  

    -   Uma das seguintes opções (não ambas):  

        -   10.000 dispositivos que são gerenciados usando o MDM local  

        -   10.000 dispositivos que executam clientes Mac e Windows CE 7.0

