---
title: Interoperabilidade entre versões
titleSuffix: Configuration Manager
description: Saiba como evitar conflitos entre várias hierarquias do Configuration Manager na mesma rede.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 51243f8df55f2736cfb053f9e38cc7b6716b2158
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66354867"
---
# <a name="interoperability-between-different-versions-of-system-center-configuration-manager"></a>Interoperabilidade entre versões diferentes do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode instalar e operar várias hierarquias independentes do System Center Configuration Manager na mesma rede. No entanto, como as diferentes hierarquias do Configuration Manager não interoperam fora do processo de migração, cada hierarquia requer configurações para evitar conflitos entre elas. Além disso, você pode criar algumas configurações para ajudar os recursos que você gerencia a interagir com os sistemas de sites por meio da hierarquia correta.  

As seções a seguir fornecem informações sobre como usar versões diferentes do Configuration Manager na mesma rede:  

- [Interoperabilidade entre o System Center Configuration Manager e versões anteriores do produto](#BKMK_SupConfigInterop)  

- [Interoperabilidade do console do Configuration Manager](#BKMK_ConsoleInterop)  

- [Limitações do Configuration Manager em uma hierarquia de versão mista](#bkmk_mixed)  


## <a name="BKMK_SupConfigInterop"></a> Interoperabilidade entre o System Center Configuration Manager e versões anteriores do produto  

Os sites de versões diferentes não podem coexistir na mesma hierarquia do Configuration Manager. As únicas exceções ocorrem durante o processo dos seguintes cenários de atualização:

- Do System Center 2012 Configuration Manager para o System Center Configuration Manager
- De uma versão do System Center Configuration Manager para uma versão mais recente usando atualizações no console

Você pode implantar um site e uma hierarquia do System Center Configuration Manager lado a lado com um site ou uma hierarquia existente do System Center 2012 Configuration Manager. Planeje medidas para impedir que os clientes de uma das versões tentem ingressar no site da outra versão.

Por exemplo, se duas ou mais hierarquias do Configuration Manager tiverem [limites de sobreposição](/sccm/core/servers/deploy/configure/boundary-groups#overlapping-boundaries) que incluam os mesmos locais de rede, atribua cada novo cliente a um site específico em vez de usar a atribuição automática de site. Para obter mais informações, confira [Como atribuir clientes a um site](/sccm/core/clients/deploy/assign-clients-to-a-site).  

Além disso, não é possível instalar um cliente do System Center 2012 Configuration Manager em um computador que hospeda uma função do sistema de sites do System Center Configuration Manager. Da mesma maneira, não é possível instalar um cliente do System Center Configuration Manager em um computador que hospeda uma função do sistema de sites do System Center 2012 Configuration Manager.  

Não há suporte para os clientes e as conexões a seguir:  

- qualquer versão do cliente do computador do System Center 2012 Configuration Manager ou anterior  

- qualquer cliente de gerenciamento de dispositivo do System Center 2012 Configuration Manager ou anterior  

- Cliente de gerenciamento de dispositivo do Windows CE Platform Builder (qualquer versão)  

- Conexão VPN do System Center Mobile Device Manager  

### <a name="BKMK_SupConfigSiteAssignment"></a> Considerações sobre atribuição de site do cliente  

Os clientes do Configuration Manager podem ser atribuídos a apenas um único site primário. Não será possível prever a atribuição de site real de um cliente quando todas as seguintes condições forem verdadeiras:

- Você usa a atribuição automática de site para atribuir clientes a um site durante a instalação do cliente
- Mais de um grupo de limites inclui o mesmo limite
- Os grupos de limites têm vários sites atribuídos

Se os limites se sobrepuserem em várias hierarquias e sites do Configuration Manager, talvez os clientes não sejam atribuídos ao site esperado ou a nenhum site.  

Os clientes do System Center Configuration Manager verificam a versão, antes de concluírem a atribuição do site. Se os limites do site se sobrepuserem, não será possível atribuir clientes a um site com uma versão anterior. No entanto, os clientes anteriores do System Center 2012 Configuration Manager podem ser atribuídos incorretamente a um site posterior do System Center Configuration Manager.  

Para impedir que clientes sejam atribuídos acidentalmente ao site incorreto em caso de duas hierarquias terem limites de sobreposição, configure os parâmetros de instalação de cliente para atribuir clientes a um site específico.  

## <a name="bkmk_mixed"></a> Limitações do Configuration Manager em uma hierarquia de versão mista  

Quando você atualiza uma hierarquia do System Center Configuration Manager, algumas vezes sites diferentes têm versões diferentes. Por exemplo, primeiro atualize o site de administração central. Devido à janela de manutenção do site, você atualiza os sites primários apenas após uma data e hora posteriores.  

Quando sites diferentes em uma única hierarquia usam versões diferentes, algumas funcionalidades ficam indisponíveis. Este comportamento pode afetar a forma de gerenciar os objetos no console do Configuration Manager, bem como as funcionalidades que estão disponíveis para os clientes. Normalmente, as funcionalidades da versão mais recente do Configuration Manager não são acessíveis em sites ou para clientes que executam uma versão inferior do service pack.  

### <a name="network-access-account"></a>Conta de acesso à rede

Atualize o site de administração central do System Center Configuration Manager. Para exibir os detalhes da conta de acesso à rede, em um console do Configuration Manager que esteja conectado a esse site atualizado. O console não exibe os detalhes da conta em sites que ainda usam o System Center 2012 Configuration Manager.

Após atualizar o site primário para a mesma versão do site de administração central, os detalhes da conta ficam visíveis no console.

O mesmo comportamento se aplica quando você atualiza entre versões do System Center Configuration Manager.

### <a name="boot-images-for-os-deployment"></a>Imagens de inicialização para implantação de sistema operacional

#### <a name="when-upgrading-from-system-center-2012-configuration-manager-to-system-center-configuration-manager"></a>Ao atualizar do System Center 2012 Configuration Manager para o System Center Configuration Manager

Quando o site de nível superior de uma hierarquia é atualizado para o System Center Configuration Manager, ele atualiza automaticamente as imagens de inicialização padrão para usar o Windows ADK (Kit de Avaliação e Implantação do Windows) versão 10. Use essas imagens de inicialização somente para implantações em clientes nos sites do System Center Configuration Manager. Para obter mais informações, confira [Planejando a interoperabilidade da implantação do sistema operacional](/sccm/osd/plan-design/planning-for-operating-system-deployment-interoperability).

#### <a name="when-upgrading-between-system-center-configuration-manager-versions"></a>Ao atualizar entre versões do System Center Configuration Manager

desde que novas versões do Configuration Manager não atualizem a versão do Windows ADK em uso, não haverá nenhum efeito nas imagens de inicialização.

### <a name="new-task-sequence-steps"></a>Novas etapas da sequência de tarefas

Quando você cria uma sequência de tarefas com uma etapa introduzida em uma versão do Configuration Manager que não está disponível em uma versão anterior, podem ocorrer os seguintes problemas:

- Um erro ocorre quando você tenta editar a sequência de tarefas de um site que está executando uma versão anterior do Configuration Manager.

- A sequência de tarefas não é executada em um computador que executa uma versão anterior do cliente do Configuration Manager.

### <a name="client-to-down-level-management-point-communications"></a>Cliente para comunicação de ponto de gerenciamento de versão anterior

Um cliente do Configuration Manager que se comunica com um ponto de gerenciamento de um site que executa uma versão inferior à do cliente pode usar somente a funcionalidade para a qual a versão anterior do Configuration Manager dá suporte. Por exemplo, se você implantar o conteúdo de um site do System Center Configuration Manager que foi atualizado recentemente para um cliente que se comunica com um ponto de gerenciamento que ainda não foi atualizado para essa versão, esse cliente não poderá usar as novas funcionalidades da versão mais recente.

### <a name="package-and-task-sequence-deployments-to-legacy-clients"></a>Implantações de pacotes e sequência de tarefas em clientes herdados

<!-- SCCMDocs-pr issue #3493 -->

A partir da versão 1902, não é possível implantar um pacote ou uma sequência de tarefas em uma versão 5.7730 ou anterior do cliente. Para contornar essa limitação, atualize o cliente para uma versão posterior.


## <a name="BKMK_ConsoleInterop"></a> Interoperabilidade do console do Configuration Manager  

Esta seção contém informações sobre o uso do console do Configuration Manager em um ambiente com uma combinação de versões do Configuration Manager.  

### <a name="an-environment-with-both-system-center-2012-configuration-manager-and-system-center-configuration-manager"></a>Um ambiente com o System Center 2012 Configuration Manager e o System Center Configuration Manager

Para gerenciar um site do Configuration Manager, o console e o site ao qual ele se conecta devem executar a mesma versão do Configuration Manager. Por exemplo, não é possível usar um console do System Center 2012 Configuration Manager para gerenciar um site do System Center Configuration Manager, ou vice-versa.

Não há suporte para instalar o console do System Center 2012 Configuration Manager e o console do System Center Configuration Manager no mesmo computador.

### <a name="an-environment-with-multiple-versions-of-system-center-configuration-manager"></a>Um ambiente com várias versões do System Center Configuration Manager

O System Center Configuration Manager não dá suporte à instalação de mais de um único console do Configuration Manager em um computador. Para usar vários consoles específicos para diferentes versões do System Center Configuration Manager, instale os diferentes consoles em computadores separados.

Durante o processo de atualização dos sites em uma hierarquia, você pode conectar um console a um site que executa uma versão mais recente e exibir informações sobre outros sites nessa hierarquia. No entanto, essa configuração não é recomendada. É possível que as diferenças entre a versão do console e a versão do site do Configuration Manager resultem em problemas de dados. Alguns recursos que estão disponíveis na versão mais recente do produto não estarão disponíveis no console.

Não há suporte para gerenciar um site usando um console com uma versão que não corresponda à versão do site. Isso pode causar perda de dados, além de colocar seu site em risco. Por exemplo, não há suporte para usar um console da versão 1610 para gerenciar um site que execute a versão 1606.
