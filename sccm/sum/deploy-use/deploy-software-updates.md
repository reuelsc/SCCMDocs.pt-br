---
title: Implantar atualizações de software
titleSuffix: Configuration Manager
description: Saiba como implantar manual ou automaticamente as atualizações de software no console do Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: 80effa7ec3439925248e19dbf9d35efcf1694b8a
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53419352"
---
# <a name="deploy-software-updates"></a>Implantar atualizações de software  

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A fase de implantação de atualização de software é o processo de implantação de atualizações de software. Independentemente de como você implanta as atualizações de software, o site:
- Adiciona as atualizações a um grupo de atualização de software
- Distribui o conteúdo da atualização aos pontos de distribuição
- Implanta o grupo de atualização nos clientes  

Depois de criar a implantação, o site envia uma política de atualização de software associada para os clientes de destino. Os clientes baixam os arquivos de conteúdo de atualização de software de uma fonte de conteúdo para o cache local. Os clientes na Internet sempre baixam o conteúdo do serviço de nuvem do Microsoft Update. Assim, as atualizações de software ficam disponíveis para instalação pelo cliente.   

> [!Tip]  
>  Quando um ponto de distribuição não está disponível, os clientes da intranet também podem baixar as atualizações de software do Microsoft Update.  

> [!NOTE]  
>  Ao contrário de outros tipos de implantação, as atualizações de software são baixadas no cache do cliente. Isso ocorre independentemente da configuração do tamanho máximo do cache no cliente. Para obter mais informações sobre a configuração de cache do cliente, confira [Configurar o cache de cliente para clientes do Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_ClientCache).  

Se você configurar uma implantação de atualização de software necessária, as atualizações de software serão instaladas automaticamente no prazo agendado. Como alternativa, o usuário no computador cliente pode agendar ou iniciar a instalação da atualização de software antes do prazo. Após a tentativa de instalação, os computadores cliente enviam mensagens de estado de volta para o servidor do site para relatar se a instalação da atualização de software teve êxito. Para obter mais informações sobre implantações de atualização de software, veja [Software update deployment workflows](/sccm/sum/understand/software-updates-introduction#BKMK_DeploymentWorkflows).  

Há três cenários principais para implantar atualizações de software: 
- [Implantação manual](#BKMK_ManualDeployment)  
- [Implantação automática](#bkmk_auto)  
- [Implantação em fases](#bkmk_phased)  

Geralmente, você começa implantando as atualizações de software manualmente para criar uma linha de base para seus clientes e, em seguida, passa a gerenciar as atualizações de software nos clientes usando uma implantação automática ou em fases.  

> [!Note]  
> Você não pode usar uma regra de implantação automática com uma implantação em fases.



## <a name="BKMK_ManualDeployment"></a> Implantar atualizações de software manualmente
Selecione as atualizações de software no console do Configuration Manager e inicie manualmente o processo de implantação. Geralmente, esse método de implantação é usado para:  

- Atualizar clientes com as atualizações de software necessárias antes de criar regras de implantação automática que gerenciam implantações mensais  

- Implantar atualizações de software fora de banda  


A lista seguinte fornece o fluxo de trabalho geral para implantação manual das atualizações de software:  

1. Filtro para atualizações de software que usam requisitos específicos. Por exemplo, forneça critérios que recuperam todas as atualizações de software de segurança ou críticas necessárias para mais de 50 computadores cliente.  

2. Crie um grupo de atualização de software que contém as atualizações de software.  

3. Baixe o conteúdo das atualizações de software no grupo de atualização de software.  

4. Implante manualmente o grupo de atualização de software.  

Para obter mais informações e etapas detalhadas, confira [Implantar atualizações de software manualmente](manually-deploy-software-updates.md).

> [!Tip]  
> Ao implantar manualmente as atualizações do cliente do Office 365, encontre-as no nó **Atualizações do Office 365** em **Gerenciamento de clientes do Office 365** do workspace **Biblioteca de Software**.  



## <a name="bkmk_auto"></a> Implantar atualizações de software automaticamente

Configure implantação de atualizações automáticas de software usando uma ADR (regra de implantação automática). Esse método de implantação é comum de atualizações de software mensais (conhecidas como "Patch Tuesday") e para o gerenciamento de atualizações de definição. Você define os critérios de uma ADR para automatizar o processo de implantação. A lista a seguir fornece o fluxo de trabalho geral para implantação automática das atualizações de software:  

1.  Crie uma ADR que especifica as configurações de implantação.  

2.  O site adiciona as atualizações de software a um grupo de atualização de software.  

3.  O site implanta o grupo de atualização de software nos clientes na coleção de destino.  

Primeiro, determine sua estratégia de implantação de atualização automática de software. Por exemplo, crie a ADR para ser direcionada inicialmente a uma coleção de clientes de teste. Depois de verificar que o grupo de teste instalou as atualizações de software com sucesso, adicione uma nova implantação à regra. Você também pode alterar a coleção de destino na implantação existente para uma que inclua um conjunto maior de clientes. Ao decidir qual estratégia de usar, considere os seguintes comportamentos:  

- Você é capaz de modificar as propriedades dos objetos de atualização de software que a ADR cria.   

- A ADR implanta automaticamente as atualizações de software nos clientes quando você os adiciona à coleção de destino.  

- Quando você ou a ADR adiciona novas atualizações de software ao grupo de atualização de software, o site implanta-as automaticamente nos clientes na coleção de destino.  

- Habilite ou desabilite as implantações a qualquer momento para a ADR.  


Depois de criar uma ADR, adicione mais implantações à regra. Essa ação ajuda a gerenciar a complexidade da implantação de diferentes atualizações em diferentes coleções. Cada nova implantação tem a gama completa de funcionalidade e experiência de monitoramento da implantação.  

Cada nova implantação que você adicionar:  

- Usa o mesmo grupo e pacote de atualização que a ADR cria em sua primeira execução  
- Pode ser direcionada a uma coleção diferente  
- Dá suporte a propriedades de implantação exclusivas, incluindo:  
  -   Tempo de ativação  
  -   Prazo  
  -   Experiência do usuário  
  -   Alertas separados para cada implantação  


Para obter mais informações e etapas detalhadas, confira [Implantar atualizações de software automaticamente](automatically-deploy-software-updates.md)



## <a name="bkmk_phased"></a> Implantar atualizações de software em fases

<!--1358146--> Começando na versão 1810, crie implantações em fases das atualizações de software. As implantações em fases permitem que você coordene uma distribuição coordenada e sequenciada do software com base em grupos e critérios personalizáveis.

Saiba mais em [Criar implantações em fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).

