---
title: "Gerenciar implantações de alto risco | Microsoft Docs"
description: "Saiba como definir as configurações de site no System Center Configuration Manager para avisar os administradores se eles criaram uma implantação de alto risco."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 8b5564f39f07a67a3c9278379ed59ca415603d21


---
# <a name="settings-to-manage-high-risk-deployments-for-system-center-configuration-manager"></a>Configurações para gerenciar implantações de alto risco para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


Com o System Center Configuration Manager, você pode definir as configurações de site para avisar aos administradores que eles criaram uma implantação de sequência de tarefas de alto risco. Uma implantação de alto risco é:  

-   Uma implantação instalada automaticamente  

-   Tem o potencial de causar resultados indesejados  

 Por exemplo, uma sequência de tarefas que tem uma finalidade **Obrigatória** e que implanta um sistema operacional é considerada de alto risco.  

 Para reduzir o risco de uma implantação de alto risco indesejada, você pode definir os limites de tamanho dessas configurações de verificação de implantação:  

-   **Limites de tamanho da coleção**: ao criar uma implantação, oculte as coleções que contêm mais clientes que o número configurado.  

    -   **Tamanho padrão**: esta configuração oculta coleções, por padrão, com mais clientes do que o seu limite ao criar uma implantação. Você ainda poderá ver estas coleções ao criar a implantação, mas elas ficam ocultas por padrão. O valor padrão é 100. Insira um valor de 0 para ignorar esta configuração.  

    -   **Tamanho máximo**: essa configuração sempre oculta as coleções com mais clientes do que seu limite ao criar uma implantação. O valor padrão é 0, que ignora esta configuração. O valor **Tamanho máximo** deve ser maior que o valor **Tamanho padrão** .  

     Por exemplo, suponhamos que você defina **Tamanho padrão** como 100 e o **Tamanho máximo** como 1000. Ao criar uma implantação de alto risco, a janela **Selecionar coleção** exibirá somente as coleções que contêm menos de 100 clientes. Se você desmarcar a definição **Ocultar coleções com uma contagem de membro maior que a configuração mínima de tamanho do site**, a janela exibirá coleções que contêm menos de 1000 clientes.  

-   **Coleções com servidores do sistema de sites**: bloqueie as implantações ou exija a verificação antes de criar a implantação, quando a coleção de destino contiver um computador com uma função do sistema de sites. Quando uma implantação estiver bloqueada, você deve selecionar uma coleção diferente que atenda aos critérios de verificação da implantação.  

> [!NOTE]  
>  As implantações de alto risco sempre estão limitadas às coleções personalizadas criadas e à coleção interna de **Computadores desconhecidos** . Ao criar uma implantação de alto risco, não é possível selecionar uma coleção interna como **Todos os Sistemas**.  

### <a name="to-configure-deployment-verification-for-a-site"></a>Para configurar a verificação de implantação para um site  

1.  No console do Configuration Manager, clique em **Administração** >**Configuração do Site** > **Sites** e selecione o site primário para configurar.  

2.  Na guia **Início**, no grupo **Propriedades**, escolha **Propriedades** e a guia **Verificação de Implantação**.  

3.  Depois de definir as configurações que você deseja usar, escolha **OK** para salvar a configuração.  

### <a name="see-also"></a>Consulte também  
 [Configurar sites e hierarquias para o System Center Configuration Manager](../../core/servers/deploy/configure/configure-sites-and-hierarchies.md)



<!--HONumber=Dec16_HO3-->


