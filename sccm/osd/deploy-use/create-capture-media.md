---
title: "Criar mídia de captura | Microsoft Docs"
description: "Use o Assistente para Criar Mídia da Sequência de Tarefas para criar mídia de captura no Configuration Manager, a fim de capturar uma imagem do sistema operacional de um computador de referência."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
caps.latest.revision: 11
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: f948c993099786432b76d1486bbb5eded4ec38eb


---
# <a name="create-capture-media-with-system-center-configuration-manager"></a>Criar mídia de captura com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A mídia de captura no Configuration Manager permite que você capture uma imagem do sistema operacional de um computador de referência. Use a mídia de captura para o cenário a seguir:  

-   [Criar uma sequência de tarefas para capturar um sistema operacional](create-a-task-sequence-to-capture-an-operating-system.md)  

##  <a name="a-namebkmkcreatecapturemediaa-how-to-create-capture-media"></a><a name="BKMK_CreateCaptureMedia"></a> Como criar mídia de captura  
 Use a mídia de captura para capturar uma imagem do sistema operacional de um computador de referência. A mídia de captura contém a imagem de inicialização que inicia o computador de referência e a sequência de tarefas que captura a imagem do sistema operacional.

Você cria a mídia de captura usando o Assistente para Criar Mídia de Sequência de Tarefas. Antes de executar o assistente, todas as condições a seguir devem ser atendidas:  

|Tarefa|Descrição|  
|----------|-----------------|  
|Imagem de inicialização|Considere o seguinte sobre a imagem de inicialização que você usará na sequência de tarefas para capturar o sistema operacional:<br /><br /> -   A arquitetura da imagem de inicialização deve ser apropriada para a arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode iniciar e executar uma imagem de inicialização x86 ou x64. No entanto, um computador de destino x86 pode iniciar e executar apenas uma imagem de inicialização x86.<br />-   Verifique se a imagem de inicialização contém os drivers de rede e armazenamento em massa necessários para provisionar o computador de destino.|  
|Distribuir todo o conteúdo associado à sequência de tarefas|Você deve distribuir todo o conteúdo exigido pela sequência de tarefas para pelo menos um ponto de distribuição. Isso inclui a imagem de inicialização, a imagem do sistema operacional e outros arquivos associados. O assistente reúne as informações do ponto de distribuição quando ele cria a mídia autônoma. Você deve ter direitos de acesso de **Leitura** à biblioteca de conteúdo no ponto de distribuição.  Para obter mais informações, consulte [Distribuir conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).|  
|Preparar a unidade USB removível|Para uma unidade USB removível:<br /><br /> Se você pretende usar uma unidade USB removível, a unidade USB deve ser conectada ao computador no qual o assistente é executado e a unidade USB deve ser detectável pelo Windows como um dispositivo de remoção. O assistente grava diretamente na unidade USB ao criar a mídia.|  
|Criar uma pasta de saída|Para um conjunto de CD/DVD:<br /><br /> Para executar o Assistente para Criar Mídia de Sequência de Tarefas para criar mídia para um conjunto de CD ou DVD, é preciso criar uma pasta para os arquivos de saída criados pelo assistente. A mídia criada para um conjunto de CD ou DVD é gravada como arquivos .iso diretamente na pasta.|  

 Use o procedimento a seguir para criar mídia de captura.  

#### <a name="to-create-capture-media"></a>Para criar mídia de captura  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Mídia de Sequência de Tarefas** para iniciar o Assistente para Criar Mídia de Sequência de Tarefas.  

4.  Na página **Selecionar o Tipo de Mídia** , selecione **Capturar mídia**e clique em **Próximo**.  

5.  Na página **Tipo de Mídia** , especifique se a mídia é uma unidade flash ou um conjunto de CD/DVD e clique em configurar o seguinte:  

    -   Se você selecionar a **Unidade flash USB**, especifique a unidade na qual deseja armazenar o conteúdo.  

    -   Caso selecione **Conjunto de CD/DVD**, especifique a capacidade da mídia, o nome e o caminho dos arquivos de saída. O assistente grava os arquivos de saída nesse local. Por exemplo: **\\\nomedoservidor\pasta\arquivodesaida.iso**  

         Se a capacidade da mídia for muito pequena para armazenar todo o conteúdo, vários arquivos são criados e você deve armazenar o conteúdo em vários CDs ou DVDs. Se várias mídias forem necessárias, o Configuration Manager adicionará um número de sequência ao nome de cada arquivo de saída criado. Além disso, se você implantar um aplicativo juntamente com o sistema operacional e o aplicativo não couber em uma única mídia, o Configuration Manager armazenará o aplicativo em várias mídias. Quando a mídia autônoma é executada, o Configuration Manager solicita ao usuário a próxima mídia, na qual o aplicativo está armazenado.  

        > [!IMPORTANT]  
        >  Se você selecionar uma imagem .iso existente, o Assistente de Mídia de Sequência de Tarefas excluirá essa imagem da unidade ou do compartilhamento assim que você prosseguir para a próxima página do assistente. A imagem existente será excluída mesmo se você cancelar o assistente.  

     Clique em **Avançar**.  

6.  Na página **Imagem de inicialização** , especifique as informações a seguir e clique em **Próximo**.  

    > [!IMPORTANT]  
    >  A arquitetura da imagem de inicialização que você especifica deve ser apropriada para a arquitetura do computador de referência. Por exemplo, um computador de referência x64 pode iniciar e executar uma imagem de inicialização x86 ou x64. No entanto, um computador de referência x86 pode iniciar e executar somente uma imagem de inicialização x86.  

    -   Na caixa **Imagem de inicialização** , especifique a imagem de inicialização para iniciar o computador de referência.  

    -   Na caixa **Ponto de distribuição** , especifique o ponto de distribuição onde a imagem de inicialização reside. O assistente recupera a imagem de inicialização do ponto de distribuição e a grava na mídia.  

        > [!NOTE]  
        >  É necessário ter direitos de acesso de leitura à biblioteca de conteúdo do ponto de distribuição.  

7.  Conclua o assistente.  



<!--HONumber=Dec16_HO3-->


