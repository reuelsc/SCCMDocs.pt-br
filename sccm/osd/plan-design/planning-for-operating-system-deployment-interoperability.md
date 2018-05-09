---
title: Planejando a interoperabilidade da implantação do sistema operacional
titleSuffix: Configuration Manager
description: Compreenda os problemas de interoperabilidade quando sites diferentes do System Center Configuration Manager em uma única hierarquia usam versões diferentes.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4faaae2d261837043b8b6ec208dd8b53b2a97b15
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="planning-for-operating-system-deployment-interoperability-in-system-center-configuration-manager"></a>Planejando a interoperabilidade da implantação de sistema operacional no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Quando sites diferentes do System Center Configuration Manager em uma única hierarquia usam versões diferentes, alguma funcionalidade do Configuration Manager não está disponível. Normalmente, a funcionalidade da versão do mais recente do Configuration Manager não é acessível em sites ou por clientes que executam uma versão inferior. Para obter mais informações, consulte [Interoperability between different versions of System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

 Considere o seguinte quando for atualizar o site de nível superior na hierarquia e outros sites na hierarquia executarem o Configuration Manager com uma versão inferior:  

-   Pacote de instalação do cliente  

    -   A origem do pacote de instalação do cliente padrão é atualizada automaticamente e todos os pontos de distribuição na hierarquia são atualizados com o novo pacote de instalação do cliente, mesmo nos pontos de distribuição em sites na hierarquia que têm uma versão inferior.  

    -   Não é possível atribuir clientes que executam a nova versão a sites que ainda não foram atualizados para a nova versão. A atribuição é bloqueada no ponto de gerenciamento.  

-   Imagens de inicialização  

    -   Quando você atualiza o site de nível superior para a versão mais recente do Configuration Manager, as imagens de inicialização padrão (x86 e x64) são atualizadas automaticamente para as imagens de inicialização baseadas no Windows ADK para o Windows 10, que usam o Windows PE 10. Os arquivos associados às imagens de inicialização padrão são atualizados com a versão mais recente do Configuration Manager dos arquivos. Imagens de inicialização personalizadas não são atualizadas automaticamente. Você precisará atualizar as imagens de inicialização personalizadas manualmente, o que inclui versões mais antigas do Windows PE.  

    -   Evite o uso de mídia dinâmica quando a hierarquia de sites contém sites com versões diferentes do Configuration Manager. Em vez disso, use mídia baseada em site para contatar um ponto de gerenciamento específico até que todos os sites sejam atualizados para a mesma versão do Configuration Manager.  

    -   Verifique se as imagens de inicialização mais recentes do Configuration Manager contêm a personalização desejada e, em seguida, atualize todos os pontos de distribuição nos sites com a versão mais recente do Configuration Manager com as novas imagens de inicialização.  

-   USMT (Ferramenta de Migração do Usuário)  

    -   Quando você atualiza o site de nível superior para a versão mais recente do Configuration Manager, o pacote da padrão da USMT é atualizado automaticamente para a versão mais recente. Pacotes da USMT personalizados não são atualizados automaticamente. Você precisará atualizar manualmente esses pacotes.  

-   Novas etapas da sequência de tarefas  

    -   Periodicamente, novas etapas da sequência de tarefas são introduzidas com novas versões do Configuration Manager. Ao implantar uma sequência de tarefas com uma nova etapa em clientes mais antigos, a etapa da sequência de tarefas falhará. Antes de implantar uma sequência de tarefas com uma nova etapa, certifique-se de que os clientes na coleção de destino sejam atualizados para a nova versão.  

-   Mídia de implantação do sistema operacional  

    -   Toda a mídia (inicializável, de captura, de pré-teste e autônoma) deve ser atualizada com o novo pacote de cliente do Configuration Manager quando o site for atualizado para uma nova versão.  

-   Extensões de terceiros para implantação de sistema operacional  

    -   Quando você tiver extensões de terceiros para implantação de sistema operacional e tiver diferentes versões de sites ou de clientes do Configuration Manager, em uma hierarquia mista, poderá haver problemas com as extensões.  

 Enquanto estiver atualizando de forma ativa os sites na hierarquia, use as seções a seguir para ajudar nas implantações de sistema operacional.  

## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>Versão mais recente de sites do Configuration Manager em uma hierarquia mista  
 Ao atualizar um site para a versão mais recente do Configuration Manager, as sequências de tarefas que fazem referência ao pacote de instalação do cliente padrão começarão a implantar automaticamente a versão mais recente do cliente do Configuration Manager. As sequências de tarefas que fazem referência a um pacote de instalação do cliente personalizado continuarão implantando a versão do cliente contida no pacote personalizado (provavelmente, uma versão anterior do cliente do Configuration Manager), e é necessário atualizá-las para evitar falhas na implantação da sequência de tarefas. Quando há uma sequência de tarefas configurada para usar um pacote de instalação do cliente personalizado, é necessário atualizar a etapa da sequência de tarefas para usar a versão mais recente do Configuration Manager do pacote de instalação do cliente ou atualizar o pacote personalizado para usar a origem de instalação do cliente mais recente do Configuration Manager.  

> [!IMPORTANT]  
>  Não implante uma sequência de tarefas que faça referência ao pacote de instalação do cliente do Configuration Manager mais recente em clientes de um site do Configuration Manager mais antigo. Quando os clientes atribuídos a um site do Configuration Manager mais antigo são atualizados para a versão mais recente do cliente do Configuration Manager, o Configuration Manager bloqueia a atribuição ao site do Configuration Manager mais antigo. Portanto, o cliente não é mais atribuído a nenhum site e não será gerenciado até que você o atribua manualmente ao site mais recente do Configuration Manager ou que a versão mais antiga do Configuration Manager do cliente seja reinstalada no computador.  

## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>Versões mais antigas do Configuration Manager em uma hierarquia mista  
 Depois de atualizar o site de administração central para a versão mais recente do Configuration Manager, é necessário executar a etapa a seguir para garantir que as sequências de tarefas da implantação de sistema operacional implantadas em clientes atribuídos a um site mais antigo do Configuration Manager (ainda não atualizados para a versão mais recente do Configuration Manager) não deixem esses clientes sem gerenciamento.  

-   Crie uma sequência de tarefas que será usada para implantar em clientes somente em um site do Configuration Manager. Provavelmente, você fará uma cópia de uma sequência de tarefas que será usada para implantar em clientes na versão mais recente do site do Configuration Manager e depois modificará a sequência de tarefas para que seja possível implantá-la em clientes de um site do Configuration Manager mais antigo. Em seguida, configure a sequência de tarefas para fazer referência a um pacote de instalação do cliente personalizado que usa a origem de instalação do cliente mais antiga do Configuration Manager. Caso ainda não tenha um pacote de instalação do cliente personalizado que faça referência à origem de instalação do cliente mais antiga do Configuration Manager, será necessário criar um manualmente.  
