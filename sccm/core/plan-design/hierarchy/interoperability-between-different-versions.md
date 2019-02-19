---
title: Interoperabilidade entre versões
titleSuffix: Configuration Manager
description: Saiba como evitar conflitos entre várias hierarquias do System Center Configuration Manager na mesma rede.
ms.date: 1/30/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ccb7861b5264d649a8ff4b2340bf34eaaafe7970
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126973"
---
# <a name="interoperability-between-different-versions-of-system-center-configuration-manager"></a>Interoperabilidade entre versões diferentes do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode instalar e operar várias hierarquias independentes do System Center Configuration Manager na mesma rede. No entanto, como as diferentes hierarquias do Configuration Manager não interoperam fora do processo de migração, cada hierarquia requer configurações para evitar conflitos entre elas. Além disso, você pode criar algumas configurações para ajudar os recursos que você gerencia a interagir com os sistemas de sites por meio da hierarquia correta.  

As seções a seguir fornecem informações sobre como usar versões diferentes do Configuration Manager na mesma rede:  

-   [Interoperabilidade entre o System Center Configuration Manager e versões anteriores do produto](#BKMK_SupConfigInterop)  

-   [Interoperabilidade do console do Configuration Manager](#BKMK_ConsoleInterop)  

-   [Limitações do Configuration Manager em uma hierarquia de versão mista](#bkmk_mixed)  

##  <a name="BKMK_SupConfigInterop"></a> Interoperabilidade entre o System Center Configuration Manager e versões anteriores do produto  
Sites de diferentes versões não podem coexistir na mesma hierarquia, exceto durante o processo de atualização do System Center 2012 Configuration Manager para o System Center Configuration Manager ou de uma versão do System Center Configuration Manager para uma versão mais recente (usando atualizações no console).   

Como é possível implantar um site e uma e hierarquia do System Center Configuration Manager lado a lado com um site ou uma hierarquia existente do System Center 2012 Configuration Manager site ou hierarquia, planeje medidas que impeçam que clientes de uma dessas versões tentem ingressar em um site da outra versão.

Por exemplo, se duas ou mais hierarquias do Configuration Manager tiverem [limites de sobreposição](/sccm/core/servers/deploy/configure/boundary-groups#overlapping-boundaries) que incluam os mesmos locais de rede, atribua cada novo cliente a um site específico em vez de usar a atribuição automática de site. Para obter mais informações, confira [Como atribuir clientes a um site](/sccm/core/clients/deploy/assign-clients-to-a-site).  

Além disso, você não pode instalar um cliente do System Center 2012 Configuration Manager em um computador que hospeda uma função de sistema de sites do System Center Configuration Manager, nem instalar um cliente do System Center Configuration Manager em um computador que hospeda uma função de sistema de sites do System Center 2012 Configuration Manager.  

Da mesma forma, não há suporte para os clientes e as conexões a seguir:  

- qualquer versão do cliente do computador do System Center 2012 Configuration Manager ou anterior  

- qualquer cliente de gerenciamento de dispositivo do System Center 2012 Configuration Manager ou anterior  

- Cliente de gerenciamento de dispositivo do Windows CE Platform Builder (qualquer versão)  

- Conexão VPN do System Center Mobile Device Manager  

###  <a name="BKMK_SupConfigSiteAssignment"></a> Considerações sobre atribuição de site do cliente  
Os clientes do Configuration Manager podem ser atribuídos a apenas um único site primário. Quando a atribuição automática de site é usada para atribuir clientes a um site durante a instalação do cliente, mais de um grupo de limites inclui o mesmo limite e os grupos de limites têm diferentes locais atribuídos, não é possível prever a atribuição de site real de um cliente.  

Se os limites se sobrepuserem em várias hierarquias e sites do Configuration Manager, os clientes poderão não ser atribuídos ao site que você espera ou poderão não ser atribuídos a nenhum site.  

Os clientes do System Center Configuration Manager verificam a versão do site do Configuration Manager antes de concluírem a atribuição do site e não podem ser atribuídos a uma versão anterior quando e se os limites do site se sobrepuserem. No entanto, os clientes do System Center 2012 Configuration Manager podem ser atribuídos incorretamente a um site do System Center Configuration Manager.  

Para impedir que os clientes sejam atribuídos acidentalmente a um site errado quando duas hierarquias tiverem limites sobrepostos, configure os parâmetros de instalação de cliente do Configuration Manager para atribuir clientes a um site específico.  

##  <a name="bkmk_mixed"></a> Limitações do Configuration Manager em uma hierarquia de versão mista  
Quando você está no processo de atualizar um site do System Center Configuration Manager, algumas vezes sites diferentes terão versões diferentes. Por exemplo, você pode atualizar um site de administração central para uma nova versão, mas devido a janelas de manutenção do site, um ou mais sites primários podem não ser atualizados até que uma data e hora posterior.  

Quando sites diferentes em uma única hierarquia usam versões diferentes, parte da funcionalidade fica indisponível. Isso pode afetar a forma de gerenciar os objetos do Configuration Manager no console do Configuration Manager e quais funcionalidades estarão disponíveis para os clientes. Normalmente, as funcionalidades da versão do mais recente do Configuration Manager não são acessíveis em sites ou para clientes que executam uma versão de service pack inferior.  

### <a name="limitations-when-upgrading-configuration-manager"></a>Limitações ao atualizar o Configuration Manager  

|Objeto|Detalhes|  
|------------|-------------|  
|Conta de acesso à rede|**Ao atualizar do System Center 2012 Configuration Manager para o System Center Configuration Manager:** Quando você exibir os detalhes da conta de acesso à rede usando um console do Configuration Manager conectado a um site de administração central que tenha sido atualizado para o System Center Configuration Manager, o console não exibirá detalhes das contas configuradas em um site primário que execute o System Center 2012 Configuration Manager. Após o site primário ser atualizado para a mesma versão do site de administração central, os detalhes da conta ficam visíveis no console.<br /><br /> **Ao atualizar entre versões do System Center Configuration Manager:** Quando você exibir os detalhes da conta de acesso à rede usando um console do Configuration Manager conectado a um site de administração central que tenha sido atualizado para uma nova versão do System Center Configuration Manager, o console não exibirá detalhes das contas configuradas em um site primário que execute uma versão anterior. Após o site primário ser atualizado para a mesma versão do site de administração central, os detalhes da conta ficam visíveis no console.|  
|Imagens de inicialização para implantação de sistema operacional|**Ao atualizar do System Center 2012 Configuration Manager para o System Center Configuration Manager:**  Quando o site de nível superior de uma hierarquia é atualizado para o System Center Configuration Manager, as imagens de inicialização padrão são atualizadas automaticamente para imagens de inicialização com base no Windows ADK 10 (Kit de Avaliação e Implantação do Windows). Use essas imagens de inicialização somente para implantações em clientes nos sites do System Center Configuration Manager. Para obter mais informações, confira [Planejando a interoperabilidade da implantação do sistema operacional](/sccm/osd/plan-design/planning-for-operating-system-deployment-interoperability).<br /><br /> **Ao atualizar entre versões do System Center Configuration Manager:** desde que novas versões do Configuration Manager não atualizem a versão do Windows ADK em uso, não haverá nenhum efeito nas imagens de inicialização.|  
|Novas etapas da sequência de tarefas|Quando você cria uma sequência de tarefas com uma etapa introduzida em uma versão do Configuration Manager que não está disponível em uma versão anterior, podem ocorrer os seguintes problemas:<br /><br /> – um erro ocorre quando você tenta editar a sequência de tarefas de um site que está executando uma versão anterior do Configuration Manager.<br /><br /> – A sequência de tarefas não é executada em um computador que executa uma versão anterior do cliente do Configuration Manager.|  
|Cliente para comunicação de ponto de gerenciamento de versão anterior|Um cliente do Configuration Manager que se comunica com um ponto de gerenciamento de um site que executa uma versão inferior à do cliente pode usar somente a funcionalidade para a qual a versão anterior do Configuration Manager dá suporte. Por exemplo, se você implantar o conteúdo de um site do System Center Configuration Manager que foi atualizado recentemente para um cliente que se comunica com um ponto de gerenciamento que ainda não foi atualizado para essa versão, esse cliente não poderá usar as novas funcionalidades da versão mais recente.|  

##  <a name="BKMK_ConsoleInterop"></a> Interoperabilidade do console do Configuration Manager  
 A tabela a seguir contém informações sobre o uso do console do Configuration Manager em um ambiente com uma combinação de versões do Configuration Manager.  


| Ambiente de interoperabilidade | Mais informações |
|------------------------------|------------------|
| Um ambiente com o System Center 2012 Configuration Manager e o System Center Configuration Manager | Para gerenciar um site do Configuration Manager, o console e o site ao qual ele se conecta devem executar a mesma versão do Configuration Manager. Por exemplo, você não pode usar um console do System Center 2012 Configuration Manager para gerenciar um site do System Center Configuration Manager, ou vice-versa.<br /><br /> Não há suporte para instalar o console do System Center 2012 Configuration Manager e o console do System Center Configuration Manager no mesmo computador.|
| Um ambiente com várias versões do System Center Configuration Manager | O System Center Configuration Manager não dá suporte à instalação de mais de um único console do Configuration Manager em um computador. Para usar vários consoles específicos para diferentes versões do System Center Configuration Manager, instale os diferentes consoles em computadores separados.<br /><br /> Durante o processo de atualização dos sites em uma hierarquia, você pode conectar um console a um site que executa uma versão mais recente e exibir informações sobre outros sites nessa hierarquia. No entanto, essa configuração não é recomendada. É possível que as diferenças entre a versão do console e a versão do site do Configuration Manager resultem em problemas de dados. Alguns recursos que estão disponíveis na versão mais recente do produto não estarão disponíveis no console. <br /><br /> Não há suporte para gerenciar um site usando um console com uma versão que não corresponda à versão do site. Isso pode causar perda de dados, além de colocar seu site em risco. Por exemplo, não há suporte para usar um console da versão 1610 para gerenciar um site que execute a versão 1606. |

