---
title: Definições de malware do Endpoint Protection do WSUS
titleSuffix: Configuration Manager
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
author: mestew
ms.author: mstewart
description: Saiba como configurar o Windows Server Updates Services para aprovação automática de atualizações de definição.
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f79fd876d19ecfae0872c97a8aabe60c121a90f2
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65494537"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-windows-server-update-services-wsus-for-configuration-manager"></a>Habilitar o download das definições de malware do Endpoint Protection do WSUS (Windows Server Update Services) para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Se você usa o WSUS para manter as definições antimalware atualizadas, pode configurá-lo para aprovação automática de atualizações de definições. Embora o uso das atualizações de software do Configuration Manager seja o método recomendado para manter as definições atualizadas, você também pode configurar o WSUS como um método para permitir que os usuários iniciem manualmente a definição atualizada. Use os procedimentos a seguir para configurar o WSUS como uma origem de atualização de definição.

## <a name="to-synchronize-endpoint-protection-definition-updates-in-configuration-manager-software-updates"></a>Para sincronizar as atualizações das definições do Endpoint Protection nas atualizações de software do Configuration Manager

1. No console do Configuration Manager, clique em **Administração**.

2. No workspace **Administração**, expanda **Configuração do Site** e clique em **Sites**.

3. Selecione o site que contém o ponto de atualização de software. No grupo **Configurações** , clique em **Configurar Componentes do Site**e clique em **Ponto de Atualização de Software**.

4. Na guia **Classificações** da caixa de diálogo **Propriedades do Componente de Ponto de Atualização de Software** , marque a caixa de seleção **Atualizações de Definições** .

5. Especifique os **Produtos** atualizados com o WSUS:

   -   Para Windows 8.1 e versões anteriores, na guia **Produtos** da caixa de diálogo **Propriedades do Componente de Ponto de Atualização de Software** , marque a caixa de seleção **Forefront Endpoint Protection 2010** .

   -   Para o Windows 10 e posteriores, na guia **Produtos** da caixa de diálogo **Propriedades do Componente de Ponto de Atualização de Software**, marque a caixa de seleção **Windows Defender**.

6. Clique em **OK** para fechar a caixa de diálogo **Propriedades do Componente de Ponto de Atualização de Software** .

   Use o procedimento a seguir para configurar as atualizações do Endpoint Protection quando o servidor do WSUS não estiver integrado ao seu ambiente do Configuration Manager.

## <a name="to-synchronize-endpoint-protection-definition-updates-in-standalone-wsus"></a>Para sincronizar as atualizações de definições do Endpoint Protection no WSUS autônomo

1.  No console de administração do WSUS, expanda **Computadores**, clique em **Opções**e clique em **Produtos e Classificações**.

2.  Especifique os **Produtos** atualizados com o WSUS:

    -   Para Windows 8.1 e versões anteriores, na guia **Produtos** da caixa de diálogo **Propriedades do Componente de Ponto de Atualização de Software** , marque a caixa de seleção **Forefront Endpoint Protection 2010** .

    -   Para o Windows 10 e posteriores, na guia **Produtos** da caixa de diálogo **Propriedades do Componente de Ponto de Atualização de Software**, marque a caixa de seleção **Windows Defender**.

3.  Na guia **Classificações** da caixa de diálogo **Produtos e Classificações** , marque as caixas de seleção **Atualizações de Definições** e **Atualizações** .

## <a name="approving-definition-updates"></a>Aprovando atualizações de definições
 As atualizações de definições do Endpoint Protection devem ser aprovadas e baixadas no servidor do WSUS antes de serem oferecidas a clientes que solicitam a lista de atualizações disponíveis. Os clientes se conectam ao servidor do WSUS para verificar se há atualizações aplicáveis e solicitam as atualizações de definições mais recentes aprovadas.

### <a name="to-approve-definitions-and-updates-in-wsus"></a>Para aprovar definições e atualizações no WSUS

1. No console de administração do WSUS, clique em **Atualizações**e clique em **Todas as Atualizações** ou a na classificação das atualizações que você deseja aprovar.

2. Na lista de atualizações, clique com o botão direito do mouse na atualização ou nas atualizações que deseja aprovar a instalação e clique em **Aprovar**.

3. Na caixa de diálogo **Aprovar Atualizações** , selecione o grupo de computadores para os quais você deseja aprovar as atualizações e clique em **Aprovadas para Instalação**.

   Além de aprovação manual, você também pode definir uma regra de aprovação automática para atualizações de definições e atualizações do Endpoint Protection. Isso configurará o WSUS para aprovar automaticamente as atualizações de definições do Endpoint Protection baixadas pelo WSUS.

### <a name="to-configure-an-automatic-approval-rule"></a>Para configurar uma regra de aprovação automática

1.  No console de administração do WSUS, clique em **Opções**e clique em **Aprovações Automáticas**.

2.  Na guia **Regras de Atualização** clique em **Nova Regra**.

3.  Na caixa de diálogo **Adicionar Regra** , em **Etapa 1: Selecionar propriedades**, marque a caixa de seleção **Quando uma atualização está em uma classificação específica** .

4.  Em **Etapa 2: Editar as propriedades**, clique em **qualquer classificação**.

5.  Desmarque todas as caixas de seleção, exceto **Atualizações de Definições**e clique em **OK**.

6.  Na caixa de diálogo **Adicionar Regra** , em **Etapa 1: Selecionar propriedades**, marque a caixa de seleção **Quando uma atualização está em um produto específico** .

7.  Em **Etapa 2: Editar as propriedades**, clique em **qualquer produto**.

8.  Desmarque todas as caixas de seleção, exceto **Forefront Endpoint Protection** para Windows 8.1 e versões anteriores ou **Windows Defender** para Windows 10 e versões posteriores e clique em **OK**.

9. Em **Etapa 3: Especificar um nome de**, digite um nome para a regra e clique em **OK**.

10. Na caixa de diálogo **Aprovações Automáticas** , marque a caixa de seleção para a regra recém-criada e clique em **Executar regra**.

> [!NOTE]
>  Para maximizar o desempenho nos seus computadores cliente e servidor do WSUS, recuse atualizações de definições antigas. Para realizar essa tarefa, você pode configurar a aprovação automática para revisões e recusa automática de atualizações expiradas. Para obter mais informações, consulte o [artigo 938947 da Base de Dados de Conhecimento Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=204078).
> 
> [!div class="button"]
> [Próxima etapa >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Voltar >](endpoint-configure-alerts.md)
