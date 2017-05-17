---
title: "Gerenciador de Transferência de Pacote | Microsoft Docs"
description: "Entenda como Gerenciador de Transferência de Pacotes no System Center Configuration Manager transfere o conteúdo de um servidor do site para pontos de distribuição."
ms.custom: na
ms.date: 2/8/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3359f254-dd48-42b7-9eab-c92a3417e3fb
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 099345d59891841a336cbada896ec349751fecd3
ms.openlocfilehash: 54e54409a1792c7e28620a5e3cea3e8d8695c7d4
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017

---
# <a name="package-transfer-manager-in-system-center-configuration-manager"></a>Gerenciador de Transferência de Pacotes no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Em um site do System Center Configuration Manager, o Gerenciador de Transferência de Pacote é um componente do SMS_Executive que gerencia a transferência de conteúdo de um computador do servidor de sites para pontos de distribuição remotos em um site. (Um ponto de distribuição remoto é um que não está localizado no computador servidor do site.) O Gerenciador de Transferência de Pacote não dá suporte a configurações realizadas pelo administrador, mas a compreensão de como ele funciona pode ajudar a planejar a infraestrutura de gerenciamento de conteúdo. Também pode ajudar a resolver problemas com a distribuição de conteúdo.


Ao distribuir conteúdo a um ou mais pontos de distribuição remotos em um site, o **Gerenciador de distribuição** cria um trabalho de transferência de conteúdo. Em seguida, ele notifica o Gerenciador de Transferência de Pacote nos servidores de sites primário e secundário para transferir o conteúdo para os pontos de distribuição remotos.

 O Gerenciador de Transferência de Pacote registra suas ações no arquivo **pkgxfermgr.log** no servidor do site. O arquivo de log é o único local em que você pode exibir as atividades desse gerenciador.  

> [!NOTE]  
>  Nas versões anteriores do Configuration Manager, o Gerenciador de Distribuição gerencia a transferência de conteúdo para um ponto de distribuição remoto. O Gerenciador de Distribuição também gerencia a transferência de conteúdo entre sites. Com o System Center Configuration Manager, o Gerenciador de distribuição continua a gerenciar a transferência de conteúdo entre os dois sites. Entretanto, o Gerenciador de Transferência de Pacote agora gerencia a transferência de conteúdo para uma grande quantidade de pontos de distribuição. Isso ajuda a aumentar o desempenho geral da implantação de conteúdo entre sites e nos pontos de distribuição de um site.  

Para transferir conteúdo para um ponto de distribuição padrão, o Gerenciador de Transferência de Pacote utiliza o mesmo procedimento usado pelo Gerenciador de Distribuição nas versões anteriores do Configuration Manager. Ou seja, ele gerencia ativamente a transferência de arquivos para cada ponto de distribuição remoto. No entanto, para distribuir conteúdo para um ponto de distribuição de recepção, o Gerenciador de Transferência de Pacote notifica esse ponto de distribuição de que há conteúdo disponível. Em seguida, o ponto de distribuição de recepção assume o processo de transferência.  

As informações a seguir descrevem como o Gerenciador de Transferência de Pacote administra a transferência de conteúdo para os pontos de distribuição padrão e para pontos de distribuição de recepção:
1.  **O usuário administrativo implanta o conteúdo em um ou mais pontos de distribuição de um site.**  

    -   **Ponto de distribuição padrão:** o Gerenciador de Distribuição cria um trabalho de transferência de conteúdo para esse conteúdo.  

    -   **Ponto de distribuição de recepção:** o Gerenciador de Distribuição cria um trabalho de transferência de conteúdo para esse conteúdo.  

2.  **O Gerenciador de Distribuição executa verificações preliminares.**  

    -   **Ponto de distribuição padrão:** o Gerenciador de Distribuição executa uma verificação básica para confirmar se cada ponto de distribuição está pronto para receber o conteúdo. Após essa verificação, o Gerenciador de Distribuição notifica o Gerenciador de Transferência de Pacote para que ele inicie a transferência do conteúdo para o ponto de distribuição.  

    -   **Ponto de distribuição de recepção**: o Gerenciador de Distribuição inicia o Gerenciador de Transferência de Pacote, o qual, por sua vez, notifica o ponto de distribuição de recepção de que há um novo trabalho de transferência de conteúdo. O Gerenciador de Distribuição não verifica o status dos pontos de distribuição remotos que são de recepção, porque cada ponto de distribuição de recepção gerencia suas próprias transferências de conteúdo.  

3.  **O Gerenciador de Transferência de Pacote se prepara para transferir o conteúdo.**  

    -   **Ponto de distribuição padrão**: o Gerenciador de Transferência de Pacote examina o repositório de conteúdo de instância única de cada ponto de distribuição remoto especificado. A finalidade é identificar todos os arquivos que já estão no ponto de distribuição. Em seguida, o Gerenciador de Transferência de Pacote colocará na fila para transferência apenas os arquivos que ainda não estão presentes.  

        > [!NOTE]  
        >  Para copiar cada arquivo na distribuição para o ponto de distribuição, mesmo se os arquivos já estiverem presentes no repositório de instância única do ponto de distribuição, use a ação **Redistribuir** para o conteúdo.  

    -   **Ponto de distribuição de recepção**: para cada ponto de distribuição de recepção na distribuição, o Gerenciador de Transferência de Pacote verifica os respectivos pontos de distribuição de origem para confirmar se o conteúdo está disponível.  

        -   Quando o conteúdo está disponível, o Gerenciador de Transferência de Pacote envia a notificação para esse ponto de distribuição de recepção. A notificação direciona o ponto de distribuição para iniciar o processo de transferência do conteúdo. A notificação inclui nome e tamanho de arquivos, atributos e valores de hash.  

        -   Quando o conteúdo ainda não está disponível, o Gerenciador de Transferência de Pacote não envia uma notificação para o ponto de distribuição. Em vez disso, ele repete a verificação a cada 20 minutos até que o conteúdo esteja disponível. Em seguida, quando o conteúdo está disponível, o Gerenciador de Transferência de Pacote envia a notificação para esse ponto de distribuição de recepção.  

        > [!NOTE]  
        >  Para que o ponto de distribuição de recepção copie cada arquivo na distribuição para o ponto de distribuição, mesmo que os arquivos já estejam presentes no repositório de instância única do ponto de distribuição de recepção, use a ação **Redistribuir** para o conteúdo.  

4.  **O conteúdo começa a ser transferido.**  

    -   **Ponto de distribuição padrão:** o Gerenciador de Transferência de Pacote copia os arquivos para cada ponto de distribuição remoto. Durante a transferência para um ponto de distribuição padrão:  

        -   Por padrão, o Gerenciador de Transferência de Pacote pode processar simultaneamente três pacotes exclusivos e distribuí-los para cinco pontos de distribuição em paralelo. Coletivamente, eles são chamados de **Configurações de distribuição simultânea**. Para configurar a distribuição simultânea, nas **Propriedades do componente de distribuição de software** de cada site, vá para a guia **Geral**.  

        -   O Gerenciador de Transferência de Pacote usa as configurações de agendamento e largura de banda de rede de cada ponto de distribuição ao transferir conteúdo para esse ponto de distribuição. Para definir essas configurações, nas **Propriedades** de cada ponto de distribuição remoto, vá para as guias **Agendamento** e **Limites de taxa**. Para mais informações, consulte [Gerenciar conteúdo e infraestrutura de conteúdo do System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    -   **Ponto de distribuição de recepção:** quando um ponto de distribuição de recepção recebe um arquivo de notificação, ele inicia o processo de transferência do conteúdo. O processo de transferência é executado de forma independente em cada ponto de distribuição de recepção:  

        1.   O ponto de distribuição de recepção identifica os arquivos da distribuição de conteúdo ainda não existentes em seu repositório de instância única e prepara-se para baixar esse conteúdo de um de seus pontos de distribuição de origem.  

        2.   Em seguida, o ponto de distribuição de recepção verifica cada um de seus pontos de distribuição de origem, por ordem, até localizar um com o conteúdo disponível. Quando identifica um ponto de distribuição de origem com o conteúdo, o ponto de distribuição de recepção inicia o download desse conteúdo.  

        > [!NOTE]  
        >  O ponto de distribuição de recepção utiliza o mesmo processo usado pelos clientes do Configuration Manager para baixar conteúdo. Para a transferência de conteúdo pelo ponto de distribuição de recepção, as configurações de transferência simultânea não são usadas. As opções de agendamento e limitação que você configurar para pontos de distribuição padrão também não são usadas.  

5.  **A transferência do conteúdo é concluída.**  

    -   **Ponto de distribuição padrão**: quando o Gerenciador de Transferência de Pacote conclui a transferência dos arquivos para cada ponto de distribuição remoto designado, ele verifica o hash do conteúdo no ponto de distribuição. Em seguida, notifica o Gerenciador de Distribuição de que a distribuição foi concluída.  

    -   **Ponto de distribuição de recepção**: após baixar o conteúdo, o ponto de distribuição de recepção verifica o hash do conteúdo. Em seguida, ele envia uma mensagem de status para o ponto de gerenciamento de site para indicar êxito. Se, após 60 minutos esse status não for recebido, o Gerenciador de Transferência de Pacote é ativado novamente. Ele verifica com o ponto de distribuição de recepção para confirmar se o conteúdo foi baixado. Se o download do conteúdo estiver em andamento, o Gerenciador de Transferência de Pacote ficará suspenso por 60 minutos, até repetir essa verificação. Esse ciclo continua até que o ponto de distribuição de recepção conclua a transferência de conteúdo.  

