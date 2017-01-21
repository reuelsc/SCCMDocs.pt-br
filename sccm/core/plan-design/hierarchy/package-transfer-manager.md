---
title: "Gerenciador de Transferência de Pacote | Microsoft Docs"
description: "Entenda como Gerenciador de Transferência de Pacotes no System Center Configuration Manager transfere o conteúdo de um servidor do site para pontos de distribuição."
ms.custom: na
ms.date: 10/06/2016
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
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 6e61c56b9d1111287bf5a9f22832f6b1ca8146b7

---
# <a name="package-transfer-manager-in-system-center-configuration-manager"></a>Gerenciador de Transferência de Pacotes no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Em um site do System Center Configuration Manager, o Gerenciador de Transferência de Pacote é um componente do SMS_Executive que gerencia a transferência de conteúdo de um computador do servidor do site para pontos de distribuição remotos em um site. (Um ponto de distribuição remoto é um que não está localizado no computador servidor do site.) O Gerenciador de Transferência de Pacote não dá suporte a configurações realizadas pelo Administrador, mas a compreensão de como ele funciona pode ajudar a planejar a infraestrutura de gerenciamento de conteúdo e resolver problemas com a distribuição de conteúdo.


Quando você distribui conteúdo para um ou mais pontos de distribuição remotos em um site, o **Gerenciador de Distribuição** cria um trabalho de transferência de conteúdo e notifica o Gerenciador de Transferência de Pacote nos servidores dos sites primário e secundário a fim de que ele transfira o conteúdo para esses pontos de distribuição.

 O Gerenciador de Transferência de Pacote registra suas ações no arquivo **pkgxfermgr.log** no servidor do site. O arquivo de log é o único local em que você pode exibir as atividades desse gerenciador.  

> [!NOTE]  
>  Nas versões anteriores do Configuration Manager, o Gerenciador de Distribuição gerencia a transferência de conteúdo para um ponto de distribuição remoto. O Gerenciador de Distribuição também gerencia a transferência de conteúdo entre sites. Com o System Center Configuration Manager, o Gerenciador de Distribuição continua a gerenciar a transferência de conteúdo entre dois sites. No entanto, o Gerenciador de Transferência de Pacote permite que o Configuration Manager descarregue do Gerenciador de Distribuição as operações necessárias para transferir o conteúdo para um grande número de pontos de distribuição. Comparado às versões anteriores do produto, isso ajuda a aumentar o desempenho geral da implantação de conteúdo entre sites e nos pontos de distribuição de um site.  

 Para transferir conteúdo para um ponto de distribuição padrão, o Gerenciador de Transferência de Pacote utiliza o mesmo procedimento usado pelo Gerenciador de Distribuição nas versões anteriores do Configuration Manager. Ou seja, ele gerencia ativamente a transferência de arquivos para cada ponto de distribuição remoto. No entanto, para distribuir conteúdo para um ponto de distribuição de recepção, o Gerenciador de Transferência de Pacote notifica esse ponto de distribuição de que há um conteúdo disponível e, em seguida, encaminha o processo de transferência desse conteúdo a ele.  

As informações a seguir descrevem como o Gerenciador de Transferência de Pacote gerencia a transferência de conteúdo para os pontos de distribuição padrão e para pontos de distribuição configurados como de recepção:
1.  **O usuário administrativo implanta o conteúdo em um ou mais pontos de distribuição de um site**  

    -   **Ponto de distribuição padrão:** o Gerenciador de Distribuição cria um trabalho de transferência de conteúdo para esse conteúdo.  

    -   **Ponto de distribuição de recepção:** o Gerenciador de Distribuição cria um trabalho de transferência de conteúdo para esse conteúdo.  

2.  **O Gerenciador de Distribuição executa verificações preliminares**  

    -   **Ponto de distribuição padrão:** o Gerenciador de Distribuição executa uma verificação básica para confirmar se cada ponto de distribuição está pronto para receber o conteúdo. Após essa verificação, o Gerenciador de Distribuição notifica o Gerenciador de Transferência de Pacote para que ele inicie a transferência do conteúdo para o ponto de distribuição.  

    -   **Ponto de distribuição de recepção:** o Gerenciador de Distribuição inicia o Gerenciador de Transferência de Pacote que, por sua vez, notifica o ponto de distribuição de recepção de que há um novo trabalho de transferência de conteúdo para o ponto de distribuição. O Gerenciador de Distribuição não verifica o status dos pontos de distribuição remotos que são de recepção porque cada ponto de distribuição de recepção gerencia suas próprias transferências de conteúdo.  

3.  **O Gerenciador de Transferência de Pacote se prepara para transferir o conteúdo**  

    -   **Ponto de distribuição padrão:** o Gerenciador de Transferência de Pacote examina o repositório de conteúdo de instância única de cada ponto de distribuição remoto especificado, a fim de identificar todos os arquivos já existentes nesse ponto de distribuição. Em seguida, o Gerenciador de Transferência de Pacote colocará na fila para transferência apenas os arquivos que ainda não estão presentes.  

        > [!NOTE]  
        >  Quando a ação **Redistribuir** é usada para um conteúdo, o Gerenciador de Transferência de Pacote copia cada arquivo da distribuição para o ponto de distribuição, mesmo que os arquivos já estejam presentes no repositório de instância única do ponto de distribuição.  

    -   **Ponto de distribuição de recepção:** para cada ponto de distribuição de recepção na distribuição, o Gerenciador de Transferência de Pacote verifica os respectivos pontos de distribuição de origem para confirmar se o conteúdo está disponível:  

        -   Quando o conteúdo está disponível em pelo menos um ponto de distribuição de origem, o Gerenciador de Transferência de Pacote envia uma notificação a esse ponto de distribuição de recepção para que ele inicie o processo de transferência do conteúdo. A notificação inclui nome e tamanho de arquivos, atributos e valores de hash.  

        -   Quando o conteúdo ainda não está disponível, o Gerenciador de Transferência de Pacote não envia uma notificação para o ponto de distribuição. Em vez disso, ele repete a verificação a cada 20 minutos até que o conteúdo esteja disponível. Em seguida, quando o conteúdo está disponível, o Gerenciador de Transferência de Pacote envia a notificação para esse ponto de distribuição de recepção.  

        > [!NOTE]  
        >  Quando a ação **Redistribuir** é usada para um conteúdo, o ponto de distribuição de recepção copia cada arquivo da distribuição para o ponto de distribuição, mesmo que os arquivos já estejam presentes no repositório de instância única do ponto de distribuição de recepção.  

4.  **O conteúdo começa a ser transferido**  

    -   **Ponto de distribuição padrão:** o Gerenciador de Transferência de Pacote copia os arquivos para cada ponto de distribuição remoto. Durante a transferência para um ponto de distribuição padrão:  

        -   Por padrão, o Gerenciador de Transferência de Pacote pode processar simultaneamente três pacotes exclusivos e distribuí-los para cinco pontos de distribuição em paralelo. Esses pontos de distribuição são denominados **Configurações de distribuição simultânea** e são configurados na guia **Geral** das **Propriedades do Componente de Distribuição de Software** de cada site.  

        -   O Gerenciador de Transferência de Pacote usa as configurações de agendamento e largura de banda de rede de cada ponto de distribuição ao transferir conteúdo para esse ponto de distribuição. Essas configurações são definidas nas guias **Agendamento** e **Limites de Taxa** nas **Propriedades** de cada ponto de distribuição remoto. Para mais informações, consulte [Gerenciar conteúdo e infraestrutura de conteúdo do System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)  

    -   **Ponto de distribuição de recepção:** quando um ponto de distribuição de recepção recebe um arquivo de notificação, ele inicia o processo de transferência do conteúdo. O processo de transferência é executado de forma independente em cada ponto de distribuição de recepção:  

        -   O ponto de distribuição de recepção identifica os arquivos da distribuição de conteúdo ainda não existentes em seu repositório de instância única e prepara-se para baixar esse conteúdo de um de seus pontos de distribuição de origem.  

        -   Em seguida, o ponto de distribuição de recepção verifica cada um de seus pontos de distribuição de origem, por ordem, até localizar um com o conteúdo disponível. Quando identifica um ponto de distribuição de origem com o conteúdo, o ponto de distribuição de recepção inicia o download desse conteúdo.  

        > [!NOTE]  
        >  O ponto de distribuição de recepção utiliza o mesmo processo usado pelos clientes do Configuration Manager para baixar conteúdo. Para a transferência de conteúdo pelo ponto de distribuição de recepção, nem as configurações de transferência simultânea nem as opções de agendamento e limitação definidas para os pontos de distribuição padrão são usadas.  

5.  **A transferência do conteúdo é concluída**  

    -   **Ponto de distribuição padrão:** quando o Gerenciador de Transferência de Pacote conclui a transferência dos arquivos para cada ponto de distribuição remoto designado, ele verifica o hash do conteúdo no ponto de distribuição e notifica o Gerenciador de Distribuição que a distribuição foi concluída.  

    -   **Ponto de distribuição de recepção:** após baixar o conteúdo, o ponto de distribuição de recepção verifica o hash do conteúdo e envia uma mensagem de status para o ponto de gerenciamento de sites a fim de indicar que o processo foi concluído com êxito. No entanto, se após 60 minutos esse status não for recebido, o Gerenciador de Transferência de Pacote será ativado e verificará se o ponto de distribuição de recepção baixou o conteúdo. Se o download do conteúdo estiver em andamento, o Gerenciador de Transferência de Pacote ficará suspenso por 60 minutos antes de repetir essa verificação. Esse ciclo continua até que o ponto de distribuição de recepção conclua a transferência de conteúdo.  



<!--HONumber=Dec16_HO3-->


