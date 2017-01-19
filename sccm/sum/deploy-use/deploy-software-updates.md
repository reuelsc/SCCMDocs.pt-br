---
title: "Implantar atualizações de software | Microsoft Docs"
description: "Escolha as atualizações de software no console do Configuration Manager para iniciar manualmente o processo de implantação ou implantar atualizações automaticamente."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
translationtype: Human Translation
ms.sourcegitcommit: e6cf8c799b5be2f7dbb6fadadddf702ec974ae45
ms.openlocfilehash: 70a0ad1da03a7ca88df206fec683ab1df2b531e1

---

#  <a name="a-namebkmksumdeploya-deploy-software-updates"></a><a name="BKMK_SUMDeploy"></a> Implantar atualizações de software  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A fase de implantação de atualização de software é o processo de implantação de atualizações de software. Independentemente de como você implanta atualizações de software, as atualizações normalmente são adicionados a um grupo de atualização de software, baixadas nos pontos de distribuição e o grupo de atualização é implantado para os clientes. Quando você cria a implantação, a política de atualização de software associada é enviada para computadores cliente, os arquivos do conteúdo de atualização de software são baixados de um ponto de distribuição para o cache local em computadores cliente e as atualizações de software estão disponíveis para instalação do cliente. Os clientes na Internet baixam conteúdo do Microsoft Update.  

> [!NOTE]  
>  É possível configurar um cliente na intranet para baixar atualizações de software do Microsoft Update caso um ponto de distribuição não esteja disponível.  

> [!NOTE]  
>  Ao contrário de outros tipos de implantação, as atualizações de software são todas baixadas para o cache do cliente independentemente da configuração do tamanho máximo do cache no cliente. Para obter mais informações sobre as configurações do cache do cliente, veja [Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

Se você configurar uma implantação de atualização de software necessária, as atualizações de software serão instaladas automaticamente no prazo agendado. Como alternativa, o usuário no computador cliente pode agendar ou iniciar a instalação da atualização de software antes do prazo. Após a tentativa de instalação, os computadores cliente enviam mensagens de estado de volta para o servidor do site para relatar se a instalação da atualização de software teve êxito. Para obter mais informações sobre implantações de atualização de software, veja [Software update deployment workflows](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows).  

Há dois cenários principais para implantar atualizações de software: implantação manual e implantação automática. Em geral, inicialmente você implantará manualmente atualizações de software para criar uma linha de base para seus computadores cliente; em seguida, você gerenciará atualizações de software em clientes usando a implantação automática.  

## <a name="a-namebkmkmanualdeploymenta-manually-deploy-software-updates"></a><a name="BKMK_ManualDeployment"></a> Implantar atualizações de software manualmente
Você pode selecionar as atualizações de software no console do Configuration Manager para iniciar manualmente o processo de implantação. Esse método de implantação é usado geralmente para ter os computadores cliente em dia com as atualizações de software necessárias antes de serem criadas regras de implantação automáticas que gerenciam as implantações de atualização de software mensalmente e continuamente e para implantar requisitos de atualização de software fora da banda. A lista seguinte fornece o fluxo de trabalho geral para implantação manual das atualizações de software:  

1. Filtro para atualizações de software que usam requisitos específicos. Por exemplo, você pode fornecer critérios que recuperam toda a segurança ou atualizações críticas de software que são necessárias em mais de 50 computadores cliente.  
2. Crie um grupo de atualização de software que contém as atualizações de software.  
3. Baixe o conteúdo das atualizações de software no grupo de atualização de software.  
4. Implante manualmente o grupo de atualização de software.

Para obter etapas detalhadas, consulte [Implantar manualmente as atualizações de software](manually-deploy-software-updates.md).

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



<!--HONumber=Dec16_HO3-->

