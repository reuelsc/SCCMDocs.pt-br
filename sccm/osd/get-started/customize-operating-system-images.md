---
title: Personalizar imagens do sistema operacional | Microsoft Docs
description: "Use sequências de tarefas de captura e montagem, a configuração manual ou uma combinação de ambos para personalizar uma imagem do sistema operacional."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95033a9b-ff13-4b70-b1de-bcb25bcb6024
caps.latest.revision: 12
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: c183fbde6de29ccd7c78ae066d305f0e99e37bda


---
# <a name="customize-operating-system-images-with-system-center-configuration-manager"></a>Personalizar imagens do sistema operacional com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As imagens do sistema operacional no System Center Configuration Manager são arquivos WIM e representam uma coleção compactada de arquivos e pastas de referência necessários para instalar e configurar com êxito um sistema operacional em um computador. Uma imagem personalizada do sistema operacional é compilada e capturada de um computador de referência configurado com todos os arquivos do sistema operacional, os arquivos de suporte, as atualizações de software, as ferramentas e os outros aplicativos de software. A proporção de configuração manual do computador de referência fica a seu critério. É possível automatizar completamente a configuração do computador de referência usando uma sequência de tarefas de criação e captura, configurar manualmente certos aspectos do computador de referência e depois automatizar o restante usando sequências de tarefas, ou ainda configurar manualmente o computador de referência sem usar sequências de tarefas. Use as seções a seguir para personalizar um sistema operacional.

##  <a name="a-namebkmkpreparereferencecomputera-prepare-for-the--reference-computer"></a><a name="BKMK_PrepareReferenceComputer"></a> Preparar o computador de referência  
 Há várias coisas a ser consideradas antes de capturar uma imagem do sistema operacional de um computador de referência.  

###  <a name="a-namebkmkrefcomputerdecidea-decide-between-an-automated-or-manual-configuration"></a><a name="BKMK_RefComputerDecide"></a> Decidir entre uma configuração manual ou automatizada  
 Veja a seguir as vantagens e desvantagens de configurações automatizada e manual do computador de referência.  

#### <a name="automated-configuration"></a>Configuração automatizada  
 **Vantagens**  

-   A configuração pode ser completamente autônoma, o que elimina a necessidade da presença de um administrador ou usuário.  

-   É possível reutilizar a sequência de tarefas para repetir a configuração de computadores de referência adicionais com um alto nível de segurança.  

-   É possível modificar a sequência de tarefas para acomodar diferenças em computadores de referência sem precisar recriar a sequência de tarefas inteira.  

 **Desvantagens**  

-   A ação inicial de criar uma sequência de tarefas pode levar muito tempo para ser criada e testada.  

-   Se os requisitos do computador de referência mudarem significativamente, poderá demorar bastante até criar e testar a sequência de tarefas novamente.  

#### <a name="manual-configuration"></a>Configuração manual  
 **Vantagens**  

-   Não é preciso criar uma sequência de tarefas nem perder tempo para testar e solucionar os problemas da sequência de tarefas.  

-   É possível instalar diretamente dos CDs sem colocar todos os pacotes de software (incluindo o próprio Windows) em um pacote do Configuration Manager.  

 **Desvantagens**  

-   A precisão da configuração do computador de referência depende do administrador ou do usuário que configura o computador.  

-   Ainda é preciso verificar e testar se o computador de referência está configurado corretamente.  

-   Não é possível reutilizar o método de configuração.  

-   Exige que uma pessoa esteja ativamente envolvida em todo o processo.  

###  <a name="a-namebkmkrefcomputerconsiderationsa-considerations-for-the-reference-computer"></a><a name="BKMK_RefComputerConsiderations"></a> Considerações para o computador de referência  
 A lista a seguir relaciona os itens básicos que devem ser considerados ao se configurar um computador de referência.  

-   **Sistema operacional a implantar**  

     É preciso instalar o computador de referência com o sistema operacional que você pretende implantar nos computadores de destino. Para obter mais informações sobre os sistemas operacionais que podem ser implantados, consulte [Requisitos de infraestrutura para implantação do sistema operacional](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

-   **Service pack apropriado**  

     É preciso instalar o computador de referência com o sistema operacional que você pretende implantar nos computadores de destino.  

-   **Atualizações de software apropriadas**  

     Instale todos os aplicativos de software que deseja incluir na imagem do sistema operacional capturada do computador de referência. Também é possível instalar aplicativos de software ao implantar a imagem capturada do sistema operacional nos computadores de destino.  

-   **Associação a grupo de trabalho**  

     O computador de referência deve ser configurado como membro de um grupo de trabalho.  

-   **Sysprep**  

     A ferramenta de Preparação do Sistema (Sysprep) é uma tecnologia que pode ser usada com outras ferramentas de implantação para instalar sistemas operacionais Windows em um novo hardware. O Sysprep prepara um computador para a geração de imagens de disco ou entrega a um cliente, configurando-o para criar um novo SID (identificador de segurança do computador) quando ele for reiniciado. Além disso, o Sysprep limpa configurações e dados específicos do usuário e do computador que não devem ser copiados em um computador de destino.  

     É possível, com o uso do Sysprep, preparar o sistema manualmente no computador de referência executando o seguinte comando:  

     `Sysprep /quiet /generalize /reboot`  

     A opção /generalize instrui o Sysprep a remover dados específicos do sistema da instalação do Windows. Informações específicas do sistema incluem logs de eventos, SIDs (IDs de de segurança exclusivas) e outras informações exclusivas. Após as informações exclusivas do sistema serem removidas, o computador é reiniciado.  

     É possível automatizar a preparação do sistema usando a sequência de tarefas [Prepare Windows for Capture](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) ou a mídia de captura.  

    > [!IMPORTANT]  
    >  A etapa da sequência de tarefas [Prepare Windows for Capture](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) tenta redefinir a senha de administrador local no computador de referência para um valor em branco antes da execução da ferramenta Sysprep. Se a política de segurança local **A senha deve satisfazer a requisitos de complexidade** estiver habilitada, essa etapa da sequência de tarefas não conseguirá redefinir a senha de administrador. Nesse cenário, desabilite essa política antes de executar a sequência de tarefas.  

     Para obter mais informações sobre o Sysprep, consulte [Referência Técnica da Preparação do Sistema (Sysprep)](http://go.microsoft.com/fwlink/?LinkId=280286).  

-   **Ferramentas apropriadas e scripts necessários para atenuar problemas nos cenários de instalação**  

     Ferramentas apropriadas e scripts necessários para reduzir problemas de instalação  

-   **Personalização apropriada da área de trabalho, como papel de parede, identidade visual e perfil do usuário padrão**  

     É possível configurar o computador de referência com as propriedades de personalização de área de trabalho que você deseja incluir ao capturar a imagem do sistema operacional do computador de referência. As propriedades da área de trabalho incluem papel de parede, identidade visual organizacional e um perfil de usuário padrão.  

##  <a name="a-namebkmkmanuallybuildreferencea-manually-build-a-reference-computer"></a><a name="BKMK_ManuallyBuildReference"></a> Criar um computador de referência manualmente  
 Use o procedimento a seguir para criar manualmente um computador de referência.  

> [!NOTE]  
>  Quando cria manualmente o computador de referência, você pode capturar a imagem do sistema operacional usando mídia de captura. Para obter mais informações, consulte [Criar mídia de captura](../deploy-use/create-capture-media.md).  

#### <a name="to-manually-build-the-reference-computer"></a>Para criar o computador de referência manualmente  

1.  Identifique o computador a ser usado como computador de referência.  

2.  Configure o computador de referência com o sistema operacional apropriado e qualquer outro software necessário para criar a imagem do sistema operacional que deseja implantar.  

    > [!WARNING]  
    >  No mínimo, instale o sistema operacional e o service pack apropriado, drivers de suporte e atualizações de software necessárias.  

3.  Configure o computador de referência para ser membro de um grupo de trabalho.  

4.  Redefina a senha de administrador local no computador de referência de forma que o valor da senha fique em branco.  

5.  Execute o Sysprep usando o comando:  **sysprep /quiet /generalize /reboot**. A opção /generalize instrui o Sysprep a remover dados específicos do sistema da instalação do Windows. Informações específicas do sistema incluem logs de eventos, SIDs (IDs de de segurança exclusivas) e outras informações exclusivas. Após as informações exclusivas do sistema serem removidas, o computador é reiniciado.  

 Depois que o computador de referência estiver pronto, use uma sequência de tarefas para capturar a imagem do sistema operacional do computador de referência.  Para obter etapas detalhadas, veja [Capturar uma imagem do sistema operacional de um computador de referência existente](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_CaptureExistingRefComputer).  

##  <a name="a-namebkmkusetstobuildreferencea-use-a-task-sequence-to-build-a-reference-computer"></a><a name="BKMK_UseTSToBuildReference"></a> Use uma sequência de tarefas para criar um computador de referência  
 É possível automatizar o processo para criar um computador de referência usando uma sequência de tarefas para implantar o sistema operacional, drivers, aplicativos e assim por diante.  Use as etapas a seguir para compilar o computador de referência e capturar a imagem do sistema operacional do computador de referência.  

-   Use uma sequência de tarefas para compilar e capturar a imagem do sistema operacional do computador de referência.  Para obter etapas detalhadas, consulte [Use a task sequence to build and capture a reference computer](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_BuildCaptureTS).  



<!--HONumber=Dec16_HO3-->


