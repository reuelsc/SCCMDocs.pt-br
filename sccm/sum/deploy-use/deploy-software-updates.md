---
title: Implantar atualizações de software
titleSuffix: Configuration Manager
description: Escolha as atualizações de software no console do Configuration Manager para iniciar manualmente o processo de implantação ou implantar atualizações automaticamente.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 02/16/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: e6a825f0d4333dc551405e38db70f8417ee2b5ce
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
#  <a name="BKMK_SUMDeploy"></a> Implantar atualizações de software  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A fase de implantação de atualização de software é o processo de implantação de atualizações de software. Independentemente de como você implanta as atualizações de software, as atualizações são normalmente:
- Adicionadas a um grupo de atualização de software.
- Baixadas em pontos de distribuição.
- O grupo de atualização é implantado nos clientes. Depois de criar a implantação, uma política de atualização de software associada é enviada aos computadores cliente. Os arquivos de conteúdo da atualização de software são baixados de um ponto de distribuição para o cache local em computadores cliente. Assim, as atualizações de software ficam disponíveis para instalação pelo cliente. Os clientes na Internet baixam conteúdo do Microsoft Update.  

> [!NOTE]  
>  Se um ponto de distribuição não estiver disponível, você poderá configurar um cliente na intranet para baixar as atualizações de software do Microsoft Update.  

> [!NOTE]  
>  Ao contrário de outros tipos de implantação, as atualizações de software são baixadas no cache do cliente. Isso ocorre independentemente da configuração do tamanho máximo do cache no cliente. Para obter mais informações sobre as configurações do cache do cliente, veja [Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

Se você configurar uma implantação de atualização de software necessária, as atualizações de software serão instaladas automaticamente no prazo agendado. Como alternativa, o usuário no computador cliente pode agendar ou iniciar a instalação da atualização de software antes do prazo. Após a tentativa de instalação, os computadores cliente enviam mensagens de estado de volta para o servidor do site para relatar se a instalação da atualização de software teve êxito. Para obter mais informações sobre implantações de atualização de software, veja [Software update deployment workflows](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows).  

Há dois cenários principais para implantar atualizações de software: implantação manual e implantação automática. Em geral, inicialmente você implanta manualmente atualizações de software para criar uma linha de base para seus computadores cliente; em seguida, gerencia atualizações de software em clientes usando a implantação automática.  

## <a name="BKMK_ManualDeployment"></a> Implantar atualizações de software manualmente
Você pode selecionar as atualizações de software no console do Configuration Manager para iniciar manualmente o processo de implantação. Esse método de implantação é usado geralmente para ter os computadores cliente em dia com as atualizações de software necessárias antes de serem criadas regras de implantação automáticas que gerenciam as implantações de atualização de software mensalmente e continuamente e para implantar requisitos de atualização de software fora da banda. A lista seguinte fornece o fluxo de trabalho geral para implantação manual das atualizações de software:  

1. Filtro para atualizações de software que usam requisitos específicos. Por exemplo, você pode fornecer critérios que recuperam toda a segurança ou atualizações críticas de software que são necessárias em mais de 50 computadores cliente.  
2. Crie um grupo de atualização de software que contém as atualizações de software.  
3. Baixe o conteúdo das atualizações de software no grupo de atualização de software.  
4. Implante manualmente o grupo de atualização de software.

Para obter etapas detalhadas, consulte [Implantar manualmente as atualizações de software](manually-deploy-software-updates.md).

>[!NOTE]
>A partir do Configuration Manager versão 1706, as atualizações de cliente do Office 365 foram movidas para o nó **Gerenciamento de Clientes do Office 365** >**Atualizações do Office 365**. Isso não afetará a configuração de ADR, mas afetará a implantação manual de atualizações do Office 365. 

## <a name="automatically-deploy-software-updates"></a>Implantar atualizações de software automaticamente
A implantação automática de atualizações de software é configurada usando uma ADR (regra de implantação automática). Esse é um método comum de implantação de atualizações de software mensais (geralmente conhecido como “Patch Tuesday”) e para o gerenciamento de atualizações de definição. Quando a regra é executada, as atualizações de software são removidas do grupo de atualização de software (caso esteja usando um grupo de atualização existente), as atualizações de software que atendem aos critérios especificados (por exemplo, todas as atualizações de software de segurança lançadas no último mês) são adicionadas a um grupo de atualização de software, os arquivos de conteúdo das atualizações de software são baixados e copiados para os pontos de distribuição e as atualizações de software são implantadas em clientes na coleção de destino. A lista a seguir fornece o fluxo de trabalho geral para implantação automática das atualizações de software:  

1.  Crie uma ADR que especifica as configurações de implantação.
2.  As atualizações de software são adicionadas a um grupo de atualização de software.  
3.  O grupo de atualização de software é implantado nos computadores cliente na coleção de destino, se especificada.  

Você deve determinar qual estratégia de implantação usar no seu ambiente. Por exemplo, é possível criar a ADR e ter com alvo uma coleção de clientes de teste. Depois de verificar se as atualizações de software estão instaladas no grupo de teste, é possível adicionar uma nova implantação à regra ou alterar a coleção na implantação existente para uma coleção de destino que inclua um conjunto maior de clientes. Os objetos de atualização de software que são criados pelas ADRs são interativos.  

-   As atualizações de software implantadas usando uma ADR são automaticamente implantadas nos novos clientes adicionados à coleção de destino.  
-   Novas atualizações de software adicionadas a um grupo de atualização de software são automaticamente implantadas em clientes na coleção de destino.  
-   É possível habilitar ou desabilitar as implantações a qualquer momento para a ADR.  

Depois de criar uma ADR, é possível adicionar outras implantações à regra. Isso pode ajudá-lo a gerenciar a complexidade de implantar diferentes atualizações em diferentes coleções. Cada nova implantação tem a gama completa da funcionalidade e da experiência de monitoramento da implantação, e cada nova implantação que você adicionar:  

-   Usa o mesmo grupo e pacote de atualização que é criado quando o ADR é executado pela primeira vez  
-   Pode especificar uma coleção diferente  
-   Dá suporte a propriedades de implantação exclusivas, incluindo:  
   -   Tempo de ativação  
   -   Prazo  
   -   Mostrar ou ocultar a experiência do usuário final  
   -   Alertas separados para esta implantação  

Para obter etapas detalhadas, consulte [Implantar as atualizações de software automaticamente](automatically-deploy-software-updates.md)

<!-- ###  <a name="BKMK_ClientCache"></a> Client cache setting  
The Configuration Manager client downloads the content for required software updates to the local client cache soon after it receives the deployment. However, the client waits to download the content until after the **Software available time** setting for the deployment. The client does not download software updates in optional deployments (deployments that do not have a scheduled installation deadline) until the user manually starts the installation. When the configured deadline passes, the software updates client agent performs a scan to verify that the software update is still required, then the software updates client agent checks the local cache on the client computer to verify that the software update source file is still available, and then installs the software update. If the content was deleted from the client cache to make room for another deployment, the client downloads the software updates to the cache. Software updates are always downloaded to the client cache regardless of the configured maximum client cache size. For other deployments, such as applications or packages, the client only downloads content that is within the maximum cache size that you configure for the client. Cached content is not automatically deleted, but it remains in the cache for at least one day after the client used that content.  -->


 <!-- For more information about the deployment process, see [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).  -->
