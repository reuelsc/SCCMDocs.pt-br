---
title: Configurar o status do cliente
titleSuffix: Configuration Manager
description: Selecione as configurações do status do cliente no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8f919e647ae252731d60a98e01485a01aae10698
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32343500"
---
# <a name="how-to-configure-client-status-in-system-center-configuration-manager"></a>Como configurar o status do cliente no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Para monitorar o status do cliente do System Center Configuration Manager e corrigir os problemas encontrados, configure seu site para especificar os parâmetros que são usados para marcar clientes como inativos e configurar opções para alertá-los se a sua atividade ficar abaixo do limite especificado. Você também pode desabilitar os computadores de consertar automaticamente os problemas que o status do cliente localizar.  

##  <a name="BKMK_1"></a> Para configurar o status do cliente  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , clique em **Status do Cliente**, na guia **Início** , no grupo **Status do Cliente** , clique em **Configurações de Status do Cliente**.  

3.  Na caixa de diálogo **Propriedades das Configurações de Status dos Clientes** , especifique os valores a seguir para determinar a atividade do cliente:  

    > [!NOTE]  
    >  Se nenhuma das configurações forem atendidas, o cliente será marcado como inativo.  

    -   **Solicitações da política do cliente nos seguintes dias:** Especifique o número de dias desde o dia em que um cliente solicitou a política. O valor padrão é **7** dias.  

    -   **Descoberta de pulsação durante os dias seguintes:** Especifique o número de dias desde o dia em que o computador cliente enviou um registro de descoberta de pulsação ao banco de dados do site. O valor padrão é **7** dias.  

    -   **Inventário de hardware durante os dias seguintes:** Especifique o número de dias desde o dia em que o computador cliente enviou um registro de inventário de hardware ao banco de dados do site. O valor padrão é **7** dias.  

    -   **Inventário de software durante os dias seguintes:** Especifique o número de dias desde o dia em que o computador cliente enviou um registro de inventário de software ao banco de dados do site. O valor padrão é **7** dias.  

    -   **Mensagens de status durante os seguintes dias:** Especifique o número de dias desde o dia em que o computador cliente enviou mensagens de status ao banco de dados do site. O valor padrão é **7** dias.  

4.  Na caixa de diálogo **Propriedades das Configurações de Status dos Clientes** , especifique o valor a seguir para determinar por quanto tempo o histórico de status do cliente deve ser mantido:  

    -   **Manter o histórico de status do cliente durante o seguinte número de dias:** Especifique por quanto tempo deseja que o histórico de status do cliente permaneça no banco de dados do site. O valor padrão é **31** dias.  

5.  Clique em **OK** para salvar as propriedades e fechar a caixa de diálogo **Propriedades das Configurações de Status dos Clientes** .  

##  <a name="BKMK_Schedule"></a> Para configurar o agendamento do status do cliente  

1.  No console do Configuration Manager, clique em **Monitoramento**.  

2.  No espaço de trabalho **Monitoramento** , clique em **Status do Cliente**, na guia **Início** , no grupo **Status do Cliente** , clique em **Agendar Atualização de Status do Cliente**.  

3.  Na caixa de diálogo **Agendar Atualização de Status do Cliente** , configure o intervalo no qual deseja que o status do cliente seja atualizado e então clique em OK.  

    > [!NOTE]  
    >  Quando você altera o agendamento das atualizações de status do cliente, a atualização não entrará em efeito até a próxima atualização de status do cliente agendada (do agendamento configurado anteriormente).  

##  <a name="BKMK_2"></a> Para configurar alertas de status do cliente  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade**.  

2.  No espaço de trabalho **Ativos e Conformidade** , clique em **Coleções de Dispositivos**.  

3.  Na lista **Coleções de Dispositivos** , selecione a coleção para a qual deseja configurar alertas e, então, na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

    > [!NOTE]  
    >  Você não pode configurar alertas para coleções de usuário.  

4.  Na guia **Alertas** da caixa de diálogo *&lt;***Propriedades* do \>nome da coleção*, clique em **Adicionar**.  

    > [!NOTE]  
    >  A guia **Alertas** torna-se visível somente se a função de segurança com a qual você está associado tiver permissões para alertas.  

5.  Na caixa de diálogo **Adicionar Novas Alertas da Coleção** , escolha os alertas que você deseja que sejam gerados quando os limites de status do cliente ficarem abaixo de um valor específico, então clique em **OK**.  

6.  Na lista **Condições** da guia **Alertas** , selecione cada alerta de status do cliente e então especifique as informações a seguir.  

    -   **Nome do Alerta** – Aceite o nome padrão ou insira um novo nome para o alerta.  

    -   **Severidade do Alerta** – Na lista suspensa, escolha o nível de alerta que será exibido no console do Configuration Manager.  

    -   **Gerar alerta** – Especifique o percentual de limite para o alerta.  

7.  Clique em **OK** para fechar a caixa de diálogo *&lt;***Propriedades* do \>nome da coleção*.  

##  <a name="BKMK_3"></a> Para excluir computadores de correção automática  

1.  Abra o editor do registro no computador cliente para o qual você deseja desabilitar a correção automática.  

    > [!WARNING]  
    >  Se você usar o Editor de Registro incorretamente, poderá causar sérios problemas e possivelmente precisará reinstalar o sistema operacional. A Microsoft não garante que você conseguirá resolver os problemas resultantes do uso incorreto do Editor do Registro. Use o Editor do Registro por sua conta e risco.  

2.  Navegue até **HKEY_LOCAL_MACHINE\Software\Microsoft\CCM\CcmEval\NotifyOnly**.  

3.  Digite um dos seguintes valores para essa chave do Registro:  

    -   **Verdadeiro** – O computador cliente não corrigirá automaticamente qualquer problema que for encontrado. No entanto, você ainda será alertado no espaço de trabalho de **Monitoramento** sobre quaisquer problemas com esse cliente.  

    -   **Falso** – O computador cliente corrigirá automaticamente os problemas quando forem localizados e você será alertado no espaço de trabalho de **Monitoramento**. Essa é a configuração padrão.  

4.  Feche o editor do Registro.  

 Você também pode instalar clientes usando a propriedade de instalação CCMSetup **NotifyOnly** para excluí-los da correção automática. Para obter mais informações sobre essa propriedade de instalação do cliente, consulte [Sobre as propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  
