---
title: "Interoperabilidade entre versões"
titleSuffix: Configuration Manager
description: "Saiba como evitar conflitos entre várias hierarquias do System Center Configuration Manager na mesma rede."
ms.custom: na
ms.date: 1/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
caps.latest.revision: "8"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 66bfb130a27ed8e4b8b9d052a672ef7f72b56f59
ms.sourcegitcommit: ca9d15dfb1c9eb47ee27ea9b5b39c9f8cdcc0748
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2018
---
# <a name="interoperability-between-different-versions-of-system-center-configuration-manager"></a>Interoperabilidade entre versões diferentes do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode instalar e operar várias hierarquias independentes do System Center Configuration Manager na mesma rede. No entanto, como as diferentes hierarquias do Configuration Manager não interoperam fora do processo de migração, cada hierarquia necessita de configurações para impedir que haja conflitos entre elas. Além disso, você pode criar algumas configurações para ajudar os recursos que você gerencia a interagir com os sistemas de sites por meio da hierarquia correta.  

 As seções a seguir fornecem informações sobre como usar versões diferentes do Configuration Manager na mesma rede:  

-   [Interoperabilidade entre o System Center Configuration Manager e versões anteriores do produto](#BKMK_SupConfigInterop)  

-   [Interoperabilidade do console do Configuration Manager](#BKMK_ConsoleInterop)  

-   [Limitações do Configuration Manager em uma hierarquia de versão mista](#bkmk_mixed)  

##  <a name="BKMK_SupConfigInterop"></a> Interoperabilidade entre o System Center Configuration Manager e versões anteriores do produto  
 Sites de diferentes versões não podem coexistir na mesma hierarquia, exceto durante o processo de atualização do System Center 2012 Configuration Manager para o System Center Configuration Manager ou de uma versão do System Center Configuration Manager para uma versão mais recente (usando atualizações no console).   

 Uma vez que é possível implantar um site e uma hierarquia do System Center Configuration Manager lado a lado com um site ou uma hierarquia existente do System Center 2012 Configuration Manager, é recomendável planejar medidas que impeçam que os clientes de uma das versões tentem ingressar no site de outras versões.

Por exemplo, se duas ou mais hierarquias do Configuration Manager tiverem limites sobrepostos (consulte [limites sobrepostos](/sccm/core/servers/deploy/configure/boundary-groups#overlapping-boundaries)) que incluem os mesmos locais de rede, a prática recomendada será atribuir a cada novo cliente um site específico em vez de usar a atribuição de site automática. Para obter informações sobre a atribuição de site automática no System Center 2012 Configuration Manager, consulte [Como atribuir clientes a um site no System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

 Além disso, você não pode instalar um cliente do System Center 2012 Configuration Manager em um computador que hospeda uma função de sistema de sites do System Center Configuration Manager, nem instalar um cliente do System Center Configuration Manager em um computador que hospeda uma função de sistema de sites do System Center 2012 Configuration Manager.  

 De maneira semelhante, não há suporte para os seguintes clientes e para a conexão VPN (Rede Virtual Privada):  

-   qualquer versão do cliente do computador do System Center 2012 Configuration Manager ou anterior  

-   qualquer cliente de gerenciamento de dispositivo do System Center 2012 Configuration Manager ou anterior  

-   Cliente de gerenciamento de dispositivo do Windows CE Platform Builder (qualquer versão)  

-   Conexão VPN do System Center Mobile Device Manager  

###  <a name="BKMK_SupConfigSiteAssignment"></a> Considerações sobre atribuição de site do cliente  
 Os clientes do System Center Configuration Manager podem ser atribuídos apenas a um único site primário. A atribuição real do site de um cliente não pode ser prevista quando a atribuição automática de site é usada para atribuir clientes a um site durante a instalação do cliente, mais de um grupo de limites inclui o mesmo limite e os grupos de limites têm diferentes sites atribuídos.  

 Se os limites se sobrepuserem em várias hierarquias e sites do Configuration Manager, os clientes poderão não ser atribuídos ao site que você espera ou poderão não ser atribuídos a nenhum site.  

 Os clientes do System Center Configuration Manager verificam a versão do site do Configuration Manager antes de concluírem a atribuição do site e não podem ser atribuídos a uma versão anterior quando e se os limites do site se sobrepuserem. No entanto, os clientes do System Center 2012 Configuration Manager podem ser atribuídos incorretamente a um site do System Center Configuration Manager.  

 Para impedir que clientes sejam atribuídos acidentalmente a um site incorreto quando duas hierarquias tiverem limites sobrepostos, é recomendável configurar os parâmetros de instalação do cliente do Configuration Manager para atribuir clientes a um site específico.  

##  <a name="bkmk_mixed"></a> Limitações do Configuration Manager em uma hierarquia de versão mista  
 Quando você está no processo de atualizar um site do System Center Configuration Manager, algumas vezes sites diferentes terão versões diferentes. Por exemplo, você pode atualizar um site de administração central para uma nova versão, mas devido a janelas de manutenção do site, um ou mais sites primários podem não ser atualizados até que uma data e hora posterior.  

 Quando sites diferentes em uma única hierarquia usam versões diferentes, parte da funcionalidade fica indisponível. Isso pode afetar a forma de gerenciar os objetos do Configuration Manager no console do Configuration Manager e quais funcionalidades estarão disponíveis para os clientes. Normalmente, as funcionalidades da versão do mais recente do Configuration Manager não são acessíveis em sites ou para clientes que executam uma versão de service pack inferior.  

### <a name="limitations-when-upgrading--configuration-manager"></a>Limitações ao atualizar o Gerenciador de Configurações  

|Objeto|Detalhes|  
|------------|-------------|  
|Conta de acesso à rede|**Ao atualizar do System Center 2012 Configuration Manager para o System Center Configuration Manager:** quando você exibe os detalhes da conta de acesso à rede de um console do Configuration Manager conectado a um site de administração central atualizado para o System Center Configuration Manager, o console não exibe detalhes de contas configuradas em um site primário que executa o System Center 2012 Configuration Manager. Após o site primário ser atualizado para a mesma versão do site de administração central, os detalhes da conta ficam visíveis no console.<br /><br /> **Ao atualizar entre versões do System Center Configuration Manager:** quando você exibe os detalhes da conta de acesso à rede de um console do Configuration Manager conectado a um site de administração central atualizado para uma nova versão do System Center Configuration Manager, o console não exibe detalhes de contas configuradas em um site primário que executa uma versão anterior. Após o site primário ser atualizado para a mesma versão do site de administração central, os detalhes da conta ficam visíveis no console.|  
|Imagens de inicialização para implantação do sistema operacional|**Ao atualizar do System Center 2012 Configuration Manager para o System Center Configuration Manager:** quando o site de nível superior de uma hierarquia é atualizado para o System Center Configuration Manager, as imagens de inicialização padrão são atualizadas automaticamente para reiniciar as imagens com base no Kit de Avaliação e Implantação do Windows 10 (Windows ADK). Use essas imagens de inicialização somente para implantações em clientes nos sites do System Center Configuration Manager. Para obter mais informações, consulte [Planejando a interoperabilidade da implantação de sistema operacional no System Center Configuration Manager](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md).<br /><br /> **Ao atualizar entre versões do System Center Configuration Manager**: desde que as novas versões do cm6long não atualizem a versão do Windows ADK em uso, não há impacto sobre as imagens de inicialização.|  
|Novas etapas da sequência de tarefas|Quando você cria uma sequência de tarefas com uma etapa introduzida em uma versão do Configuration Manager que não está disponível em uma versão anterior, você pode encontrar os seguintes problemas:<br /><br /> – Ocorrerá um erro quando você tentar editar a sequência de tarefas de um site que executa uma versão anterior do Configuration Manager.<br /><br /> – A sequência de tarefas não é executada em um computador que executa uma versão anterior do cliente do Configuration Manager.|  
|Cliente para comunicação de ponto de gerenciamento de versão anterior|Um cliente do Configuration Manager que se comunica com um ponto de gerenciamento de um site que executa uma versão inferior à do cliente pode usar somente a funcionalidade para a qual a versão anterior do Configuration Manager dá suporte. Por exemplo, se você implantar conteúdo de um site do System Center Configuration Manager atualizado recentemente em um cliente que se comunica com um ponto de gerenciamento que ainda não foi atualizado para a mesma versão, esse cliente não poderá usar novas funcionalidades da versão mais recente.|  

##  <a name="BKMK_ConsoleInterop"></a> Interoperabilidade do console do Configuration Manager  
 A tabela a seguir contém informações sobre o uso do console do Configuration Manager em um ambiente com uma combinação de versões do Configuration Manager.  

|Ambiente de interoperabilidade|Mais informações|  
|----------------------------------|----------------------|  
|Um ambiente com o System Center 2012 Configuration Manager e o System Center Configuration Manager|Para gerenciar um site do Configuration Manager, o console e o site ao qual ele se conecta devem executar a mesma versão do Configuration Manager. Por exemplo, você não pode usar um console do System Center 2012 Configuration Manager para gerenciar um site do System Center Configuration Manager, ou vice-versa.<br /><br /> Não há suporte para instalar o console do System Center 2012 Configuration Manager e o console do System Center Configuration Manager no mesmo computador.|  
|Um ambiente com várias versões do System Center Configuration Manager|O System Center Configuration Manager não dá suporte à instalação de mais de um console único do Configuration Manager em um computador. Para usar vários consoles específicos de diferentes versões do System Center Configuration Manager, você precisa instalar os diferentes consoles em computadores separados.<br /><br /> Durante o processo de atualização dos sites em uma hierarquia, você pode conectar um console a um site que executa uma versão mais recente e exibir informações sobre outros sites nessa hierarquia. No entanto, essa configuração não é recomendada porque é possível que as diferenças entre a versão do console e a versão do site do Configuration Manager resultem em problemas de dados e alguns recursos que estão disponíveis na versão mais recente do produto não estarão disponíveis no console. <br /><br>Não há suporte para o gerenciamento de um site usando um console com uma versão que não coincide com a versão do site. Isso pode causar perda de dados, além de colocar seu site em risco. Por exemplo, não há suporte para o uso de um console da versão 1610 para gerenciar um site que executa a versão 1606. |
