---
title: Configurar o controle remoto
titleSuffix: Configuration Manager
description: Configure o controle remoto no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4e4d380319704eda608930ac938232513800b81a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>Configurando o controle remoto no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 Este procedimento descreve como definir as configurações padrão do cliente para o controle remoto. Essas configurações se aplicam a todos os computadores em sua hierarquia. Se quiser que essas configurações se apliquem somente a alguns computadores, atribua uma configuração personalizada do cliente de dispositivo que contém os computadores. Para obter mais informações, consulte [Como definir as configurações do cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md). 

Para usar a Assistência Remota ou a Área de Trabalho Remota, ela deve estar instalada e configurada no computador que executa o console do Configuration Manager. Para obter mais informações sobre como instalar e configurar a Assistência Remota ou a Área de Trabalho Remota, veja a documentação do Windows.  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>Para habilitar o controle remoto e definir as configurações do cliente  

1.  No console do Configuration Manager, escolha **Administração** > **Configurações do Cliente** > **Configurações do Cliente Padrão**.  

4.  Na guia **Início**, no grupo **Propriedades**, clique em **Propriedades**.  

5.  Na caixa de diálogo **Padrão**, escolha **Ferramentas Remotas**.  

6.  Configure o controle remoto e defina as configurações de cliente da Assistência Remota e da Área de Trabalho Remota. Para obter uma lista de configurações do cliente de ferramentas remotas que podem ser definidas, consulte [Ferramentas remotas](../../../../core/clients/deploy/about-client-settings.md#remote-tools).  

    Você pode alterar o nome da empresa que aparece na caixa de diálogo **Controle Remoto do ConfigMgr** configurando um valor para o **Nome da organização exibido no Centro de Software** nas configurações do cliente **Agente Computador** .  

 Os computadores cliente são definidos com essas configurações na próxima vez que baixarem a política do cliente. Para iniciar a recuperação de política para um cliente individual, veja [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

#### <a name="enable-keyboard-translation"></a>Habilitar a tradução do teclado

Por padrão, o Configuration Manager transmite a posição da chave do local do visualizador para o local do participante do compartilhamento. Isso pode apresentar um problema para configurações de teclado diferentes do visualizador para participante do compartilhamento. Por exemplo, um visualizador com um teclado em inglês digitaria um "A", mas o teclado francês do participante do compartilhamento forneceria um "Q". Agora você tem a opção de configurar o controle remoto para que o próprio caractere seja transmitido do teclado do visualizador para o participante do compartilhamento e para o que o visualizador pretenda digitar chegue ao participante do compartilhamento.

Para ativar a tradução do teclado, em **Controle Remoto do Configuration Manager**, escolha **Ação** e escolha **Habilitar Tradução do Teclado** para transmitir a posição da chave.

> [!NOTE]
>
> As chaves especiais, como ~!#@$% não serão convertidas corretamente.


## <a name="keyboard-shortcuts-for-the-remote-control-viewer"></a>Atalhos de teclado do visualizador de controle remoto

|Atalho de teclado|Descrição|  
|-----------------------|-----------------|  
|Alt+Page Up|Alterna entre programas em execução da esquerda para a direita.|  
|Alt+Page Down|Alterna entre programas em execução da direita para a esquerda.|  
|Alt+Insert|Percorre os programas em execução na ordem em que foram abertos.|  
|Alt+Home|Exibe o menu **Iniciar** .|  
|Ctrl+Alt+End|Exibe a caixa de diálogo de Segurança do Windows (Ctrl+Alt+Del).|  
|Alt+Delete|Exibe o menu do Windows.|  
|Ctrl+Alt+sinal de subtração (no teclado numérico)|Copia a janela ativa do computador local na Área de transferência do computador remoto.|  
|Ctrl+Alt+sinal de mais (no teclado numérico)|Copia toda a área da janela do computador local na Área de transferência do computador remoto.|  
