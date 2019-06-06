---
title: Interoperabilidade na implantação do sistema operacional
titleSuffix: Configuration Manager
description: Compreenda os problemas de interoperabilidade quando sites diferentes do System Center Configuration Manager em uma única hierarquia usam versões diferentes.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7d4f6275ede2a751acb8ca14d7b8b6ad307e78bd
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66355006"
---
# <a name="plan-for-os-deployment-interoperability"></a>Planejar a interoperabilidade na implantação do sistema operacional

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Quando sites diferentes do System Center Configuration Manager em uma única hierarquia usam versões diferentes, alguma funcionalidade do Configuration Manager não está disponível. Normalmente, a funcionalidade da versão mais recente do Configuration Manager não é acessível em sites ou por clientes que executam uma versão inferior. Para obter mais informações, consulte [Interoperabilidade entre versões diferentes do Configuration Manager](/sccm/core/plan-design/hierarchy/interoperability-between-different-versions).  


## <a name="objects"></a>Objetos

Considere os seguintes objetos quando for atualizar o site de nível superior na hierarquia e outros sites na hierarquia executarem o Configuration Manager com uma versão inferior:  

### <a name="client-installation-package"></a>Pacote de instalação do cliente  

- A origem do pacote de instalação do cliente padrão é atualizada automaticamente. Todos os pontos de distribuição na hierarquia são atualizados com o novo pacote de instalação do cliente. Esse comportamento ocorre mesmo nos pontos de distribuição em sites na hierarquia que são uma versão inferior.  

- Você não pode atribuir novos clientes de versão a sites que ainda não foram atualizados para a nova versão. A atribuição é bloqueada no ponto de gerenciamento.  

### <a name="boot-images"></a>Imagens de inicialização  

- Quando você atualiza o site de nível superior para a versão mais recente do Configuration Manager, ele atualiza automaticamente as imagens de iniciação padrão (x86 e x64). A atualização usa o Windows ADK para Windows 10, que inclui o Windows PE 10. Os arquivos associados às imagens de inicialização padrão são atualizados com a versão mais recente do Configuration Manager dos arquivos. O site não atualiza automaticamente imagens de inicialização personalizadas. Você precisa atualizar as imagens de inicialização personalizadas manualmente, o que inclui versões mais antigas do Windows PE.  

- Quando a hierarquia de sites contém sites com versões diferentes do Configuration Manager, evite o uso de mídia dinâmica. Em vez disso, use a mídia baseada em site para contatar um ponto de gerenciamento específico. Depois de atualizar todos os sites para a mesma versão do Configuration Manager, você pode usar a mídia dinâmica novamente.

- Verifique se as imagens de inicialização mais recentes do Configuration Manager incluem suas personalizações. Em seguida, atualize todos os pontos de distribuição de sites da nova versão com a versão mais recente das novas imagens de inicialização.  

### <a name="user-state-migration-tool-usmt"></a>USMT (Ferramenta de Migração do Usuário)  

Quando você atualiza o site de nível superior para a versão mais recente do Configuration Manager, ele atualiza automaticamente o pacote da USMT padrão para a versão mais recente. Ele não atualiza automaticamente nenhum pacote da USMT personalizado. Você precisa atualizar esses pacotes manualmente.  

### <a name="new-task-sequence-steps"></a>Novas etapas da sequência de tarefas  

Periodicamente, novas etapas da sequência de tarefas são introduzidas com novas versões do Configuration Manager. Ao implantar uma sequência de tarefas com uma nova etapa em clientes mais antigos, a etapa da sequência de tarefas falha. Antes de implantar uma sequência de tarefas com uma nova etapa, certifique-se de que os clientes na coleção de destino sejam atualizados para a nova versão.  

### <a name="os-deployment-media"></a>Mídia de implantação de sistema operacional  

Quando o site for atualizado para uma nova versão, atualize todas as mídias com o novo pacote de cliente do Configuration Manager. Esses tipos de mídia incluem inicializáveis, capturas, pré-configuradas e autônomas.

### <a name="third-party-extensions-to-os-deployment"></a>Extensões de terceiros para implantação de sistema operacional  

Quando você tiver extensões de terceiros para implantação de sistema operacional e tiver diferentes versões de sites ou de clientes do Configuration Manager poderá haver problemas com as extensões.  


## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>Versão mais recente de sites do Configuration Manager em uma hierarquia mista  

Ao atualizar um site para a versão mais recente do Configuration Manager, as sequências de tarefas que fazem referência ao pacote de instalação do cliente padrão começam a implantar automaticamente a versão mais recente do cliente do Configuration Manager.

As sequências de tarefas que fazem referência a um pacote de instalação do cliente personalizado continuam a implantar a versão do cliente que está contida no pacote personalizado. Os pacotes personalizados provavelmente incluem uma versão anterior do cliente do Configuration Manager. Para evitar falhas de implantação de sequência de tarefas, atualize todos os pacotes de instalação do cliente personalizado para a versão mais recente.

Quando você configura uma sequência de tarefas para usar um pacote de instalação do cliente personalizado, execute uma das seguintes ações:

- Atualizar a etapa de sequência de tarefas para usar a versão mais recente do Configuration Manager do pacote de instalação do cliente
- Atualizar o pacote personalizado para usar a origem de instalação de cliente mais recente do Configuration Manager

> [!IMPORTANT]  
> Não implante uma sequência de tarefas que faça referência ao pacote de instalação do cliente do Configuration Manager mais recente em clientes de um site do Configuration Manager mais antigo. Quando os clientes atribuídos a um site do Configuration Manager mais antigo são atualizados para a versão mais recente do cliente do Configuration Manager, o Configuration Manager bloqueia a atribuição ao site do Configuration Manager mais antigo. Esses clientes não são mais atribuídos a nenhum site. Até que você atribua manualmente o cliente para o site do Configuration Manager, ou reinstale a versão do Configuration Manager mais antiga do cliente no computador, esses clientes não serão gerenciados.


## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>Versões mais antigas do Configuration Manager em uma hierarquia mista  

Quando você atualizar seu site de administração central para a versão mais recente do Configuration Manager, verifique se as sequências de tarefas de implantação de sistema operacional implantadas não deixam esses clientes em um estado não gerenciado. Por exemplo, se você implantar em clientes atribuídos a um site do Configuration Manager mais antigo que ainda não foi atualizado para a versão mais recente do Configuration Manager.

Faça uma cópia de uma sequência de tarefas usada para implantar em clientes na versão mais recente do site do Configuration Manager. Em seguida, modifique-a para poder implantá-la em clientes em um site do Configuration Manager mais antigo. Configure a sequência de tarefas para fazer referência a um pacote de instalação do cliente personalizado que usa a origem de instalação do cliente mais antiga do Configuration Manager. Caso ainda não tenha um pacote de instalação do cliente personalizado que faça referência à origem de instalação do cliente mais antiga do Configuration Manager, crie um manualmente.  

> [!Important]  
> Começando na versão 1902, não é possível implantar um pacote ou uma sequência de tarefas em uma versão do cliente 5.7730 ou anterior. Para contornar essa limitação, atualize o cliente para uma versão posterior.<!-- SCCMDocs-pr issue #3493 -->
