---
title: Funcionalidades no Technical Preview 1603 do Configuration Manager
description: "Saiba mais sobre os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1603."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f861b72-9f14-4d17-a512-4a79b660abe6
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.translationtype: Human Translation
ms.sourcegitcommit: 5d08d1f9ccd995d544c3c21c4af52ede73343077
ms.openlocfilehash: 1d3adcf3310d88b1266388aa03ae5ea03e23f2a5
ms.contentlocale: pt-br
ms.lasthandoff: 01/24/2017

---
# <a name="capabilities-in-technical-preview-1603-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1603 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1603. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview. Como alternativa, quando você usa o System Center Technical Preview 5, esta versão é instalada como uma versão de linha de base do System Center Configuration Manager Technical Preview. Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de um technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos em um technical preview.  

 **Problemas conhecidos nesse Technical Preview:**  

-   Essa versão inclui atualizações para recursos lançados anteriormente, mas não introduz novos recursos. Portanto, a página Recursos do Assistente de Atualização estará vazia se você tiver atualizado anteriormente para 1602 e se tiver habilitado todos os recursos incluídos nessa versão.  

-   Depois que o servidor do site é atualizado para a Technical Preview 1603, os clientes não poderão usar os recursos de controle remoto até que eles também sejam atualizados para a versão 1603.  

 **Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

##  <a name="BKMK_SC1603"></a> Melhorias no Centro de Software  

### <a name="new-tiled-view-for-apps"></a>Nova exibição lado a lado para aplicativos  
 Agora, os usuários finais podem escolher entre uma lista de aplicativos ou uma exibição lado a lado dos aplicativos na guia **Aplicativos** do Centro de Software.  

### <a name="select-multiple-updates-in-software-center"></a>Escolher várias atualizações no Centro de Software  
 Na guia **Atualizações** do Centro de Software, agora você pode escolher várias atualizações ou **Atualizar Tudo** para começar a instalação de várias atualizações simultaneamente.  

##  <a name="BKMK_RC1603"></a> Melhorias no controle remoto  

### <a name="limit-shared-clipboard-access-in-a-remote-control-session"></a>Limitar o acesso compartilhado à área de transferência em uma sessão de controle remoto  
 Agora você pode habilitar a nova configuração do cliente de ferramentas remotas **Solicitar ao usuário permissão para transferência de arquivo na área de transferência compartilhada** para limitar o acesso à área de transferência compartilhada em uma sessão de controle remoto.  

 Quando habilitada, o usuário final que está compartilhando uma sessão remota deverá conceder permissões ao visualizador da sessão para que este possa transferir arquivos da sessão para a máquina local por meio da área de transferência compartilhada.  

 Isso adiciona uma camada de proteção para o usuário final como anteriormente, caso o visualizador tenha recebido controle total do computador do usuário final; eles podiam usar a área de transferência compartilhada para transferir arquivos da sessão para o computador local de maneira que era totalmente transparente para o usuário final.  

##  <a name="BKMK_RamDiskTFTP"></a> Personalizar o tamanho do bloco e da janela do RamDisk TFTP nos pontos de distribuição habilitados para PXE  
 Na Technical Preview 1603, você pode personalizar o tamanho do bloco e da janela do RamDisk TFTP para pontos de distribuição habilitados para PXE. Se você tiver personalizado sua rede, isso poderá fazer com que o download da imagem de inicialização falhe com um erro de tempo limite devido ao tamanho muito grande do bloco ou da janela. A personalização do tamanho do bloco e da janela do RamDisk TFTP permite otimizar o tráfego TFTP ao usar o PXE para atender aos seus requisitos de rede específicos.   
Você precisará testar as configurações personalizadas no ambiente para determinar o que é mais eficiente.  

-   **Tamanho do bloco do TFTP**: o tamanho do bloco é o tamanho dos pacotes de dados que são enviados pelo servidor ao cliente que está baixando o arquivo (como discutido em RFC 2347). Um tamanho de bloco maior permite que o servidor envie menos pacotes, para que haja menos atrasos de viagem de ida e volta entre o servidor e o cliente. No entanto, um bloco de tamanho grande leva a pacotes fragmentados, com os quais a maioria das implementações do cliente PXE não é compatível.  

-   **Tamanho da janela do TFTP**: o TFTP exige um pacote ACK (de confirmação) para cada bloco de dados que é enviado. O servidor não enviará o próximo bloco na sequência enquanto não receber o pacote ACK do bloco anterior. As janelas do TFTP são um recurso nos Serviços de Implantação do Windows que permite definir quantos blocos de dados são necessários para preencher uma janela. O servidor envia os blocos de dados um após o outro até que a janela esteja preenchida; em seguida, o cliente envia um pacote ACK. Aumentar o tamanho da janela reduz o número de atrasos da viagem de ida e volta entre o cliente e o servidor, além de diminuir o tempo total que é necessário para baixar uma imagem de inicialização.  

### <a name="try-it-out"></a>Experimente!  
 Tente concluir as seguintes tarefas e depois use as informações dos comentários perto da parte superior deste tópico para nos contar como foi:  

-   Posso personalizar o tamanho da janela do RamDisk TFTP no ponto de distribuição habilitado para PXE.  

-   Posso personalizar o tamanho do bloco do RamDisk TFTP no ponto de distribuição habilitado para PXE.  

### <a name="to-modify-the-ramdisk-tftp-window-size"></a>Para modificar o tamanho da janela do RamDisk TFTP  

-   Adicione a seguinte chave do registro nos pontos de distribuição habilitados para PXE para personalizar o tamanho da janela do RamDisk TFTP:  

     **Local**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Nome: RamDiskTFTPWindowSize  

     **Tipo**: REG_DWORD  

     **Valor**: &lt;tamanho de janela personalizado\>  

 O valor padrão é 1 (um bloco de dados preenche a janela)  

### <a name="to-modify-the-ramdisk-tftp-block-size"></a>Para modificar o tamanho do bloco do RamDisk TFTP  

-   Adicione a seguinte chave do registro nos pontos de distribuição habilitados para PXE para personalizar o tamanho da janela do RamDisk TFTP:  

     **Local**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Nome: RamDiskTFTPBlockSize  

     **Tipo**: REG_DWORD  

     **Valor**: &lt;tamanho de bloco personalizado\>  

 O valor padrão é 4096 (4 k).  

