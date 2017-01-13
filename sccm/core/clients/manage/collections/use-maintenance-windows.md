---
title: "Usar janelas de manutenção | Microsoft Docs"
description: "Use coleções e janelas de manutenção para gerenciar com eficácia os clientes no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: e59953f41422ee8f79ca054b5ccaccf41bb4e7af


---
# <a name="how-to-use-maintenance-windows-in-system-center-configuration-manager"></a>Como usar as janelas de manutenção no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As janelas de manutenção n System Center Configuration Manager fornecem um meio pelo qual os usuários administrativos podem definir um período de tempo em que várias operações do Configuration Manager podem ser executadas nos membros de uma coleção de dispositivos. Você pode usar as janelas de manutenção para ajudar a assegurar que as alterações de configuração do cliente ocorram durante períodos que não afetem a produtividade da organização.  

 As seguintes operações do Configuration Manager dão suporte a janelas de manutenção:  

-   Implantações de software  

-   Implantações de atualização de software  

-   Implantação e avaliação das configurações de conformidade  

-   Implantações de sistema operacional  

-   Implantações de sequência de tarefas  

 As janelas de manutenção são configuradas para uma coleção com data de início, hora de início e término e um padrão de recorrência. Cada janela de manutenção deve ter uma duração de menos de 24 horas. Por padrão, as reinicializações do computador resultantes de uma implantação não são permitidas fora da janela de manutenção, mas é possível substituir o padrão nas configurações de cada implantação. As janelas de manutenção afetam somente o período em que o programa de implantação está em execução; os aplicativos configurados para ser baixados e executados localmente podem baixar conteúdo fora da janela de manutenção.  

 Quando um computador cliente é membro de uma coleção de dispositivos que contém uma janela de manutenção configurada, um programa de implantação somente é executado se o tempo máximo de execução permitido não ultrapassa a duração configurada para a janela de manutenção. Se o programa falhar na execução, um alerta será gerado e a implantação será executada novamente durante a próxima janela de manutenção agendada que tiver um horário disponível.  

## <a name="using-multiple-maintenance-windows"></a>Usando várias janelas de manutenção  
 Quando um computador cliente é um membro de várias coleções de dispositivos que configuraram janelas de manutenção, as seguintes regras se aplicam:  

-   Se as janelas de manutenção não se sobrepõem, elas são tratadas como duas janelas de manutenção independentes.  

-   Se as janelas de manutenção se sobrepõem, elas são tratadas como uma única janela de manutenção abrangendo o período de tempo coberto por ambas as janelas de manutenção. Por exemplo, se duas janelas de manutenção, cada uma com uma hora de duração se sobreporem por 30 minutos, a duração efetiva da janela de manutenção deverá ser de 90 minutos.  

 Quando um usuário inicia uma instalação do aplicativo no Centro de Software, o aplicativo é instalado imediatamente, independentemente de quaisquer janelas de manutenção configuradas.  

 Se uma implantação de aplicativo com a finalidade de **Obrigatória** atingir a data limite de instalação fora do horário comercial configurado pelo usuário no Centro de Software, o aplicativo será instalado.  

### <a name="how-to-configure-maintenance-windows"></a>Como configurar janelas de manutenção  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Coleções de Dispositivos**.  

3.  Na lista **Coleções de Dispositivos** , selecione a coleção para a qual você deseja configurar uma janela de manutenção.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Na guia **Janelas de Manutenção** da caixa de diálogo **Propriedades do &lt;nome da coleção\>**, clique no ícone **Novo**.  

    > [!NOTE]  
    >  Você não pode criar janelas de manutenção para a coleção **Todos os sistemas** .  

6.  Na caixa de diálogo **&lt;novo\> Agendamento**, especifique um nome, um agendamento e um padrão de recorrência para a janela de manutenção. Você também pode habilitar a opção para aplicar o agendamento somente a sequências de tarefas.  

7.  Na lista suspensa **Aplicar este agendamento a** , selecione se a janela de manutenção se aplica a todas as implantações, somente às atualizações de software ou apenas às sequências de tarefas.  

8.  Clique em **OK** para fechar a caixa de diálogo **&lt;novo\> Agendamento** e criar a nova janela de manutenção.  

9. Feche a caixa de diálogo **Propriedades de &lt;nome da coleção\>**.  



<!--HONumber=Dec16_HO3-->


