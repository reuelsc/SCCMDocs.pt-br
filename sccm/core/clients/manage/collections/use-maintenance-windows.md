---
title: "Usar janelas de manutenção | Microsoft Docs"
description: "Use coleções e janelas de manutenção para gerenciar com eficácia os clientes no System Center Configuration Manager."
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 05c27c7aa36e0b4236867766dab36125c31467b3
ms.openlocfilehash: c0b4fcda6599ed91fe2393b97bdcec6cdfba9b7c


---
# <a name="how-to-use-maintenance-windows-in-system-center-configuration-manager"></a>Como usar as janelas de manutenção no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As janelas de manutenção permitem que você defina um período em que as operações do Configuration Manager podem ser executadas em uma coleção de dispositivos. É possível usar as janelas de manutenção para ajudar a assegurar que as alterações de configuração do cliente ocorrem durante períodos que não afetam a produtividade.  

 As seguintes operações dão suporte a janelas de manutenção:  

-   Implantações de software  

-   Implantações de atualização de software  

-   Implantação e avaliação das configurações de conformidade  

-   Implantações de sistema operacional  

-   Implantações de sequência de tarefas  

 Configure as janelas de manutenção com uma data de início, uma hora de início e término e um padrão de recorrência. A duração máxima de uma janela deve ser menor que 24 horas. Por padrão, as reinicializações do computador causadas por uma implantação não são permitidas fora de uma janela de manutenção, mas é possível substituir o padrão. As janelas de manutenção afetam somente o período em que o programa de implantação é executado; os aplicativos configurados para serem baixados e executados localmente podem baixar conteúdo fora da janela.  

 Quando um computador cliente é membro de uma coleção de dispositivos que contém uma janela de manutenção, um programa de implantação somente é executado se o tempo máximo de execução permitido não excede a duração configurada para a janela. Se o programa falhar na execução, um alerta será gerado e a implantação será executada novamente durante a próxima janela de manutenção agendada que tiver um horário disponível.  

## <a name="using-multiple-maintenance-windows"></a>Usando várias janelas de manutenção  
 Quando um computador cliente é membro de várias coleções de dispositivos que contêm janelas de manutenção, estas regras se aplicam:  

-   Se as janelas de manutenção não se sobrepõem, elas são tratadas como duas janelas de manutenção independentes.  

-   Se as janelas de manutenção se sobrepõem, elas são tratadas como uma única janela de manutenção abrangendo o período de tempo coberto por ambas as janelas de manutenção. Por exemplo, se duas janelas, cada uma com uma hora de duração, se sobreporem por 30 minutos, a duração efetiva da janela de manutenção deverá ser de 90 minutos.  

 Quando um usuário inicia uma instalação de aplicativo por meio do Centro de Software, o aplicativo é instalado imediatamente, independentemente das janelas de manutenção.  

 Se uma implantação de aplicativo com a finalidade de **Obrigatória** atingir a data limite de instalação fora do horário comercial configurado pelo usuário no Centro de Software, o aplicativo será instalado.  

### <a name="how-to-configure-maintenance-windows"></a>Como configurar janelas de manutenção  

1.  No console do Configuration Manager, escolha **Ativos e Conformidade**>  **Coleções de Dispositivos**.  

3.  Na lista **Coleções de Dispositivos**, selecione uma coleção. Você não pode criar janelas de manutenção para a coleção **Todos os sistemas** .  

4.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

5.  Na guia **Janelas de Manutenção** da caixa de diálogo **Propriedades do &lt;nome da coleção\>**, escolha o ícone **Novo**.  

6.  Conclua a caixa de diálogo **&lt;novo\> Agendamento**.  

7.  Faça uma seleção na lista suspensa **Aplicar este agendamento a**.  

8.  Escolha **OK** e feche a caixa de diálogo **Propriedades do &lt;nome da coleção\>**.  



<!--HONumber=Jan17_HO1-->


