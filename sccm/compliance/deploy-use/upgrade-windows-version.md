---
title: "Atualizar dispositivos do Windows para uma versão diferente com o Configuration Manager | Microsoft Docs"
description: "Atualize automaticamente os dispositivos que executam o Windows 10 Desktop, Windows 10 Mobile ou Windows 10 Holographic para outra edição com o Configuration Manager."
ms.custom: na
ms.date: 04/18/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
caps.latest.revision: 8
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 4eee9731a4a27328c47c0d15931cab28cf520a18
ms.openlocfilehash: cfde0a43947013bbd3a1093688cee19fe309fd03
ms.lasthandoff: 04/18/2017


---

# <a name="upgrade-windows-devices-with-the-edition-upgrade-policy-in-system-center-configuration-manager"></a>Atualizar dispositivos Windows com a política de atualização de edição no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


A **Política de Atualização de Edição** do System Center Configuration Manager permite atualizar automaticamente os dispositivos que executem uma das seguintes versões do Windows 10 para uma edição diferente:

- Windows 10 Desktop
- Windows 10 Mobile
- Windows 10 Holographic

Há suporte para os seguintes caminhos de atualização:

- Do Windows 10 Pro para Windows 10 Enterprise
- Do Windows 10 Home para Windows 10 Education
- Do Windows 10 Mobile para Windows 10 Mobile Enterprise
- Do Windows 10 Holographic Pro para Windows 10 Holographic Enterprise

Os dispositivos devem ser registrados no Microsoft Intune ou executar o software cliente do Configuration Manager. Essa política não é compatível no momento com PCs gerenciados por MDM local.

## <a name="before-you-start"></a>Antes de começar  
 Antes de começar a atualizar os dispositivos para a versão mais recente, será necessário o seguinte:  

-   Uma chave do produto (Product Key) que é válida para instalar a nova versão do Windows em todos os dispositivos de que destino com a política (para sistemas operacionais de área de trabalho)  

-   Um arquivo de licença da Microsoft que contém as informações de licenciamento para instalar a nova versão do Windows em todos os dispositivos de destino com a política (para Windows Mobile 10 e Windows 10 Holographic).

- Para criar e implantar esse tipo de política, você deve recebido a atribuição da função de segurança de **Administrador Completo** do Configuration Manager.

## <a name="configure-the-edition-upgrade-policy"></a>Configurar a política de atualização de edição  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Atualização da Edição do Windows 10**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Política de Atualização de Edição**.  

4.  Clique em **Criar Política**.  

5.  Na página **Geral** do **Assistente de Criação de Política de Atualização de Edição**, especifique as seguintes informações:  

    -   **Nome** - Insira um nome para a política de atualização de edição.  

    -   **Descrição** (opcional) - opcionalmente, digite uma descrição para a política que ajuda a identificá-la no console do Intune.  

    -   **SKU para atualizar o dispositivo** - na lista suspensa, selecione a versão do Windows 10 Desktop, Windows 10 Holographic ou Windows 10 Mobile para a qual você deseja atualizar os dispositivos de destino.  

    -   **Informações de licença** - Selecione um destes:  

        -   **Chave do Produto (Product Key)** - Insira uma chave do produto (Product Key) válida do Windows 10 que será usada para atualizar os dispositivos que você visa que executam sistemas operacionais Windows 10 Desktop.  

            > [!NOTE]  
            >  Depois de criar uma política que contém uma chave do produto (Product Key), não é possível editar a chave do produto (Product Key) mais tarde. Isso ocorre porque a chave é obscurecida por motivos de segurança. Para alterar a chave do produto (Product Key), você deve reinserir a chave inteira.  

        -   **Arquivo de Licença** - Clique em **Procurar** para selecionar um arquivo de licença válida no formato XML que será usado para atualizar os dispositivos de destino que executam os sistemas operacionais Windows 10 Holographic e Windows 10 Mobile.  

6.  Conclua o assistente.  

A nova política é exibida no nó **Atualização de Edição do Windows 10** do espaço de trabalho **Ativos e Conformidade** .  

## <a name="deploy-the-edition-upgrade-policy"></a>Implantar a política de atualização de edição  

1.  No console do Configuration Manager, clique em **Ativos e Conformidade** > **Configurações de Conformidade** > **Atualização da Edição do Windows 10**.  

3.  Selecione a política de atualização de edição do Windows 10 que deseja implantar e, na guia **Início** , no grupo **Implantação** , clique em **Implantar**.  

4.  Na caixa de diálogo **Implantar a Atualização do Windows 10 Edition**, escolha a coleção a qual você deseja implantar a política e o agendamento pelo qual a política será avaliada e, em seguida, clique em **OK**. Para PCs gerenciados com o cliente do Configuration Manager, você deve implantar a política para uma coleção de dispositivos. Para computadores que são registrados com o Intune, você pode implantar a política a um usuário ou uma coleção de dispositivos. 

Você pode monitorar a implantação que acabou de ser criada no nó **Implantações** do espaço de trabalho **Monitoramento** .  

 Quando a política atinge um computador Windows definido como destino e é avaliada, ela será reiniciada dentro de duas horas para aplicar a atualização. Certifique-se de informar os usuários nos quais você implanta a política ou agende a política para ser executada fora do horário de trabalho dos usuários.

