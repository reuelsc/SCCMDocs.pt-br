---
title: Gerenciar implantações de alto risco
titleSuffix: Configuration Manager
description: Saiba como definir as configurações de site de verificação de implantação no Configuration Manager para avisar os administradores se eles criarem uma implantação de alto risco.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a2e2817f5f3bd48e4a84e2e507597126fa10f989
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53419217"
---
# <a name="settings-to-manage-high-risk-deployments-for-configuration-manager"></a>Configurações para gerenciar implantações de alto risco para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Com o Configuration Manager, você pode definir as configurações de site de verificação de implantação. Essas configurações avisam os administradores se eles criam uma implantação de sequência de tarefas de alto risco. Uma implantação de alto risco é:  

-   Uma implantação instalada automaticamente  

-   Tem o potencial de causar resultados indesejados  

Por exemplo, uma sequência de tarefas que tem uma finalidade **Obrigatória** e que implanta um sistema operacional é considerada de alto risco.  

Para reduzir o risco de uma implantação de alto risco indesejada, você pode definir os limites de tamanho dessas configurações de verificação de implantação:  

- **Limites de tamanho da coleção**: quando você criar uma implantação, oculte as coleções que incluem mais clientes do que o limite.  

  - **Tamanho padrão**: quando você criar uma implantação, essa configuração ocultará, por padrão, as coleções que incluírem mais clientes do que esse limite. Você ainda poderá ver essas coleções ao criar a implantação, mas elas ficarão ocultas por padrão. O valor padrão é **100**. Insira um valor de **0** para ignorar esta configuração.  

  - **Tamanho máximo**: quando você criar uma implantação, essa configuração sempre ocultará coleções com mais clientes que esse limite. O valor padrão é **0**, que ignora essa configuração. O valor **Tamanho máximo** deve ser maior que o valor **Tamanho padrão** .  

    Por exemplo, suponhamos que você defina **Tamanho padrão** como 100 e o **Tamanho máximo** como 1000. Quando você cria uma implantação de alto risco, a janela **Selecionar Coleção** exibe somente as coleções que incluem menos de 100 clientes. Se você desmarcar a configuração **Ocultar coleções com uma contagem de membros maior que a configuração mínima de tamanho do site**, a janela exibirá coleções que contenham menos de 1.000 clientes.  

- **Coleções com servidores do sistema de sites**: quando a coleção de destino incluir um computador com uma função do sistema de sites, bloqueie as implantações ou exija a verificação antes da criação da implantação. Quando uma implantação estiver bloqueada, selecione uma coleção diferente que atenda aos critérios de verificação de implantação para continuar a criar a implantação.  

> [!NOTE]  
>  As implantações de alto risco sempre estão limitadas às coleções personalizadas criadas e à coleção interna de **Computadores desconhecidos** . Ao criar uma implantação de alto risco, não é possível selecionar uma coleção interna como **Todos os Sistemas**.  

### <a name="configure-deployment-verification-for-a-site"></a>Configurar a verificação de implantação para um site  

1.  No console do Configuration Manager, vá para o workspace de **Administração**, expanda **Configuração do Site**, selecione **Sites** e, em seguida, selecione o site primário para configurar.  

2.  Clique em **Propriedades** na faixa de opções e, em seguida, mude para a guia **Verificação de Implantação**.  

3.  Depois de definir as configurações que você deseja usar, clique em **OK** para salvar a configuração.  


### <a name="see-also"></a>Consulte também  
 [Configurar sites e hierarquias](/sccm/core/servers/deploy/configure/configure-sites-and-hierarchies)
