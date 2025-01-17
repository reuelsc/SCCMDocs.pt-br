---
title: Configurar alertas do Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba como configurar alertas do Endpoint Protection no System Center Configuration Manager.
ms.date: 03/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f504de3e-4caf-455c-80d7-a63f13f4c5d9
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ee1bf48298c3c21388267c4975d6d59383157593
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65494753"
---
#  <a name="configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Configurar alertas para o Endpoint Protection no Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 É possível configurar alertas do Endpoint Protection no Microsoft System Center Configuration Manager para notificar os usuários administrativos quando ocorrem eventos específicos, como uma infecção por malware, em sua hierarquia. As notificações são exibidas no painel do Endpoint Protection no console do Configuration Manager no nó **Alertas** do workspace **Monitoramento** ou podem ser enviadas por email para os usuários especificados.

 Use as seguintes etapas e os procedimentos complementares neste tópico para configurar alertas para o Endpoint Protection no Configuration Manager.

> [!IMPORTANT]
>  É necessário ter a permissão **Impor Segurança** para que as coleções configurem alertas do Endpoint Protection.

## <a name="steps-to-configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Etapas para configurar alertas para o Endpoint Protection no Configuration Manager

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.

2.  No workspace **Ativos e Conformidade**, clique em **Coleções de Dispositivos**.

3.  Na lista **Coleções de Dispositivos** , selecione a coleção para a qual deseja configurar alertas e, na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.

    > [!NOTE]
    >  Você não pode configurar alertas para coleções de usuário.

4.  Na guia **Alertas** da caixa de diálogo _<Nome da Coleção\>_ **Propriedades**, selecione **Exibir esta coleção no painel do Endpoint Protection** se você desejar exibir detalhes sobre operações antimalware para esta coleção no workspace **Monitoramento** do console do Configuration Manager.

    > [!NOTE]
    >  Essa opção não está disponível para a coleção **Todos os Sistemas** .

5.  Na guia **Alertas** da caixa de diálogo _<Nome da Coleção\>_ **Propriedades**, clique em **Adicionar**.

6.  Na caixa de diálogo **Adicionar Novos Alertas da Coleção**, na seção **Gerar um alerta quando estas condições se aplicarem**, selecione os alertas que você deseja que o Configuration Manager gere quando os eventos especificados do Endpoint Protection ocorrerem e clique em **OK**.

7.  Na lista **Condições** da guia **Alertas**, selecione cada alerta do Endpoint Protection e especifique as informações a seguir:

    -   **Nome do Alerta** – Aceite o nome padrão ou insira um novo nome para o alerta.

    -   **Severidade do Alerta** – na lista, selecione o nível de alerta a ser exibido no console do Configuration Manager.

8.  Dependendo do alerta selecionado, especifique as seguintes informações adicionais:

    -   **Detecção de malware** – este alerta será gerado se o malware for detectado em qualquer computador da coleção que você monitorar. O **Limite de detecção de malware** especifica os níveis de detecção de malware nos quais esse alerta é gerado:

        -   **Alto – Todas as detecções** – o alerta é gerado quando há um ou mais computadores na coleção especificada na qual qualquer malware é detectado, independentemente de qual ação o cliente do Endpoint Protection o cliente toma.

        -   **Médio – Detectado, ação pendente** – o alerta é gerado quando há um ou mais computadores na coleção especificada na qual o malware é detectado, e é necessário remover manualmente o malware.

        -   **Baixo – Detectado, continua ativo** – o alerta é gerado quando há um ou mais computadores na coleção especificada na qual o malware é detectado e ainda está ativo.

    -   **Ataque de malware** – Este alerta será gerado se um malware especificado for detectado em um percentual especificado de computadores na coleção monitorada.

        -   **Percentagem de computadores com malware detectado** – o alerta é gerado quando o percentual de computadores com malware detectado na coleção excede o percentual que você especifica. Especifique um percentual de **1** a **99**.

            > [!NOTE]
            >  O valor percentual é baseado no número de computadores na coleção, mas exclui os computadores que não têm um cliente do Configuration Manager instalado. Ele inclui computadores que ainda não têm o cliente do Endpoint Protection instalado.

    -   **Detecção de malware repetida** – este alerta será gerado se um malware específico for detectado mais de um número especificado de vezes em um número especificado de horas nos computadores da coleção que você monitorar. Especifique as seguintes informações para configurar este alerta:

        -   **Número de vezes que foi detectado malware:** - o alerta é gerado quando o mesmo malware é detectado em computadores na coleção mais vezes que o número de vezes especificado. Especifique um número de **2** a **32**.

        -   **Intervalo de detecção (horas):** especifique o intervalo de detecção (em horas) no qual o número de detecções de malware deve ocorrer. Especifique um número de **1** a **168**.

    -   **Detecção de Malware Múltipla** – Este alerta será gerado se mais de um número especificado de tipos de malware for detectado durante um número especificado de horas em computadores na coleção que você monitorar. Especifique as seguintes informações para configurar este alerta:

        -   **Número de tipos de malware detectado:** o alerta é gerado quando o número especificado de tipos diferentes de malware é detectado em computadores na coleção. Especifique um número de **2** a **32**.

        -   **Intervalo de detecção (horas):** especifique o intervalo de detecção, em horas, no qual o número de detecções de malware deve ocorrer. Especifique um número de **1** a **168**.

9. Clique em **OK** para fechar a caixa de diálogo _<Nome da Coleção\>_ **Propriedades**.  

## <a name="alert-for-outdated-malware-client"></a>Alerta de cliente de malware desatualizado

A partir do Configuration Manager versão 1702, você poderá configurar um alerta para garantir que os clientes do Endpoint Protection não estejam desatualizados. Em qualquer coleção de dispositivos, agora é possível adicionar colunas à lista dos seguintes atributos **Versão do cliente antimalware** e **Estado de implantação da proteção do Endpoint Protection**. Por exemplo, no console, navegue até **Ativos e Conformidade** > **Visão geral** > **Coleções de dispositivos** > **Todos os clientes de servidor e desktop**. Clique com o botão direito do mouse no cabeçalho da coluna e selecione as colunas a serem adicionadas. Para verificar se há um alerta, exiba **Alertas** no workspace **Monitoramento**. Se mais de 20% dos clientes gerenciados estiver executando uma versão expirada do software antimalware, o alerta de que o cliente antimalware está desatualizado será exibido. Esse alerta não aparece na guia **Monitoramento** > **Visão Geral**. Para atualizar clientes antimalware expirados, habilite as atualizações de software para clientes antimalware.

Para configurar o percentual em que o alerta é gerado, expanda **Monitoramento** > **Alertas** > **Todos os Alertas**, clique duas vezes em **Clientes antimalware desatualizados** e modifique a opção **Acionar alerta se o percentual de clientes gerenciados com uma versão desatualizada do cliente antimalware for de mais de**.

> [!div class="button"]
> [Próxima etapa >](endpoint-definition-updates.md)
> 
> [!div class="button"]
> [Voltar >](endpoint-protection-site-role.md)
