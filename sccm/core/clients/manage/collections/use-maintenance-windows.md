---
title: Usar janelas de manutenção
titleSuffix: Configuration Manager
description: Use coleções e janelas de manutenção para gerenciar com eficácia os clientes no System Center Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: cc4a984b15af66a5426d30f3fb4f0b68c794ba5f
ms.sourcegitcommit: 53f2380ac67025fb4a69fc1651edad15d98e0cdd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65673331"
---
# <a name="how-to-use-maintenance-windows-in-system-center-configuration-manager"></a>Como usar as janelas de manutenção no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As janelas de manutenção permitem que você defina um período em que as operações do Configuration Manager podem ser executadas em uma coleção de dispositivos. É possível usar janelas de manutenção para ajudar a assegurar que as alterações na configuração do cliente ocorram durante períodos que não afetam a produtividade. Começando com o Configuration Manager versão 1806, os usuários podem ver quando é a próxima janela de manutenção na guia **Status de instalação** no **Centro de Software**. <!--1358131-->

 As seguintes operações dão suporte a janelas de manutenção:  

- Implantações de software  

- Implantações de atualização de software  

- Implantação e avaliação das configurações de conformidade  

- Implantações de sistema operacional  

- Implantações de sequência de tarefas  

  Configure as janelas de manutenção com uma data de início, uma hora de início e término e um padrão de recorrência. A duração máxima de uma janela deve ser menor que 24 horas. Por padrão, as reinicializações do computador causadas por uma implantação não são permitidas fora de uma janela de manutenção, mas é possível substituir o padrão. As janelas de manutenção afetam somente o período em que o programa de implantação é executado; os aplicativos configurados para serem baixados e executados localmente podem baixar conteúdo fora da janela.  

  Quando um computador cliente é membro de uma coleção de dispositivos que contém uma janela de manutenção, um programa de implantação somente é executado quando o tempo máximo de execução permitido não excede a duração configurada para a janela. Se o programa falhar na execução, um alerta será gerado e a implantação será executada novamente durante a próxima janela de manutenção agendada que tiver um horário disponível.  

## <a name="using-multiple-maintenance-windows"></a>Usando várias janelas de manutenção  
 Quando um computador cliente é membro de várias coleções de dispositivos que contêm janelas de manutenção, estas regras se aplicam:  

- Quando as janelas de manutenção não se sobrepõem, elas são tratadas como duas janelas de manutenção independentes.  

- Quando as janelas de manutenção se sobrepõem, elas são tratadas como uma única janela de manutenção abrangendo o período de tempo coberto pelas duas janelas de manutenção. Por exemplo, se duas janelas, cada uma com uma hora de duração, se sobreporem por 30 minutos, a duração efetiva da janela de manutenção deverá ser de 90 minutos.  

  Quando um usuário inicia uma instalação de aplicativo por meio do Centro de Software, o aplicativo é instalado imediatamente, independentemente das janelas de manutenção.  

  Se uma implantação de aplicativo com a finalidade de **Obrigatória** atingir a data limite de instalação fora do horário comercial configurado pelo usuário no Centro de Software, o aplicativo será instalado. 

### <a name="how-to-configure-maintenance-windows"></a>Como configurar janelas de manutenção  

1.  No console do Configuration Manager, escolha **Ativos e Conformidade**>  **Coleções de Dispositivos**.  

3.  Na lista **Coleções de Dispositivos**, selecione uma coleção. Você não pode criar janelas de manutenção para a coleção **Todos os Sistemas**.  

4.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

5.  Na guia **Janelas de Manutenção** da caixa de diálogo **Propriedades do &lt;nome da coleção\>** , escolha o ícone **Novo**.  

6.  Conclua a caixa de diálogo **&lt;novo\> Agendamento**.  

7.  Faça uma seleção na lista suspensa **Aplicar este agendamento a**.  

8.  Escolha **OK** e feche a caixa de diálogo **Propriedades do &lt;nome da coleção\>** .  
 
## <a name="bkmk_powershell"></a> Uso do PowerShell

O PowerShell pode ser usado para configurar as janelas de manutenção.  Para obter mais informações, consulte:

* [Set-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmmaintenancewindow)
* [Get-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmmaintenancewindow)
* [New-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmmaintenancewindow)
* [Remove-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmmaintenancewindow)
