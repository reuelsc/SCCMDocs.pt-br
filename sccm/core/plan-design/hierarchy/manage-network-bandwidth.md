---
title: Gerenciar largura de banda de rede para o conteúdo
titleSuffix: Configuration Manager
description: Defina o agendamento, a limitação e o pré-teste de conteúdo para o System Center Configuration Manager.
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e80d1151-91db-4a27-8411-a957297b67d0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2d8587c0640d831a723b9ff7c3a6402d47ee2405
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="manage-network-bandwidth-for-content"></a>Gerenciar largura de banda de rede para o conteúdo
Para ajudar a gerenciar a largura de banda de rede usada no processo de gerenciamento de conteúdo do System Center Configuration Manager, você pode usar controles internos para agendamento e limitação. Você também pode usar conteúdo pré-testado. As seções a seguir descrevem essas opções mais detalhadamente.

##  <a name="BKMK_PlanningForThrottling"></a>Agendamento e limitação  

 Ao criar um pacote, altere o caminho de origem do conteúdo ou atualize o conteúdo no ponto de distribuição; os arquivos são copiados do caminho de origem para a biblioteca de conteúdo no servidor do site. Em seguida, o conteúdo é copiado da biblioteca de conteúdo no servidor do site para a biblioteca de conteúdo nos pontos de distribuição. Quando os arquivos de origem do conteúdo são atualizados e os arquivos de origem já foram distribuídos, o Configuration Manager recupera somente os arquivos novos ou atualizados e os envia ao ponto de distribuição.

 Você pode usar controles de agendamento e limitação para comunicação de site a site e para comunicação entre um servidor de sites e um ponto de distribuição remoto. Se a largura de banda estiver limitada mesmo após configurar os controles de agendamento e limitação, considere pré-configurar o conteúdo no ponto de distribuição.  

 No Configuration Manager, você pode configurar um agendamento e definir configurações de limitação específicas em pontos de distribuição remotos que determinam quando e como a distribuição do conteúdo é realizada. Cada ponto de distribuição remoto pode ter configurações diferentes que ajudam a tratar limitações de largura de banda de rede do servidor do site para o ponto de distribuição remoto. Os controles de agendamento e limitação para pontos de distribuição remotos são semelhantes às configurações de um endereço de remetente padrão. Nesse caso, as configurações são usadas por um novo componente chamado Gerenciador de Transferência de Pacote.

 O Gerenciador de Transferência de Pacote distribui o conteúdo de um servidor do site, como um site primário ou secundário, para um ponto de distribuição instalado em um sistema de site. As configurações de limitação são definidas na guia **Limites de taxa** e as configurações de agendamento são definidas na guia **Agendamento** para um ponto de distribuição que não está em um servidor de sites. As configurações de hora são baseadas no fuso horário do site de envio, não do ponto de distribuição.  

> [!IMPORTANT]  
>  As guias **Limites de Taxa** e **Agendamento** são exibidas somente nas propriedades de pontos de distribuição que não estão instalados em um servidor do site.  

Para saber mais, veja [Instalar e configurar pontos de distribuição para o System Center Configuration Manager](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).  

##  <a name="BKMK_PrestagingContent"></a>Conteúdo pré-teste  
 Você pode pré-testar o conteúdo para adicionar os arquivos de conteúdo à biblioteca de conteúdo em um servidor de sites ou ponto de distribuição antes de distribuir o conteúdo. Como os arquivos de conteúdo já estão na biblioteca de conteúdo, eles não são transferidos pela rede durante a distribuição. Você pode pré-configurar arquivos de conteúdo para aplicativos e pacotes.  

No console do Configuration Manager, selecione o conteúdo que você deseja pré-testar e, em seguida, use o **Assistente para Criar Arquivo de Conteúdo de Pré-Teste**. Isso cria um arquivo de conteúdo compactado e pré-testado, que contém os arquivos, as metadados associados ao conteúdo. Em seguida, você pode importar manualmente o conteúdo em um servidor do site ou ponto de distribuição. Observe o seguinte:  

-   Quando você importa o arquivo de conteúdo de pré-teste em um servidor do site, os arquivos de conteúdo são adicionados à biblioteca de conteúdo no servidor do site, e em seguida registrados no banco de dados do servidor do site.  

-   Quando você importa o arquivo de conteúdo pré-testado no ponto de distribuição, os arquivos de conteúdo são adicionados à biblioteca de conteúdo no ponto de distribuição. Uma mensagem de status é enviada ao servidor de sites informando que o conteúdo está disponível no ponto de distribuição.  

Opcionalmente, você pode configurar o ponto de distribuição como **pré-testado** para ajudar a gerenciar a distribuição de conteúdo. Então, ao distribuir conteúdo, você pode escolher se deseja:  

-   Sempre pré-testar o conteúdo no ponto de distribuição.  

-   Pré-testar o conteúdo inicial para o pacote e, então, usar o processo de distribuição de conteúdo padrão quando houver atualizações para o conteúdo.  

-   Sempre usar o processo de distribuição de conteúdo padrão para o conteúdo no pacote.  

###  <a name="BKMK_DetermineToPrestageContent"></a>Determinar se deseja pré-testar o conteúdo  
 Considere a pré-configuração do conteúdo para aplicativos e pacotes nos seguintes cenários:  

-   **Para lidar com o problema de largura de banda de rede limitada do servidor de sites ao ponto de distribuição.** Se o agendamento e a limitação não são suficientes para atender às suas preocupações sobre largura de banda, considere pré-testar o conteúdo no ponto de distribuição. Cada ponto de distribuição tem a configuração **Habilitar este ponto de distribuição para conteúdo pré-configurado** que você pode definir nas propriedades do ponto de distribuição. Quando você habilita essa opção, o ponto de distribuição é identificado como um ponto de distribuição pré-configurado, e você pode escolher como gerenciar o conteúdo por pacote.  

    As seguintes configurações estão disponíveis nas propriedades de um aplicativo, pacote, pacote de driver, imagem de inicialização, instalador do sistema operacional e imagem. Essas configurações possibilitam escolher como a distribuição de conteúdo é gerenciada em pontos de distribuição remotos que são identificados como pré-testados:  

    -   **Baixar conteúdo automaticamente quando pacotes forem atribuídos a pontos de distribuição**: use esta opção quando tiver pacotes menores, e as configurações de agendamento e limitação fornecerem controle suficiente para distribuição do conteúdo.  

    -   **Baixar somente alterações de conteúdo para o ponto de distribuição**: use essa opção quando você espera que futuras atualizações ao conteúdo do pacote sejam menores em geral. Por exemplo, você pode pré-testar um aplicativo como o Microsoft Office, já que o tamanho inicial do pacote é maior que 700 MB e é muito grande para ser enviado pela rede. No entanto, as atualizações de conteúdo nesse pacote podem ser inferiores a 10 MB e são aceitáveis para distribuição pela rede. Outro exemplo pode ser pacotes de driver em que o tamanho inicial do pacote é grande, mas adições de driver incrementais ao pacote podem ser pequenas.  

    -   **Copiar manualmente o conteúdo deste pacote para o ponto de distribuição**: use esta opção no caso de pacotes grandes, com conteúdo como um sistema operacional, e quando você nunca desejar usar a rede para distribuir o conteúdo para o ponto de distribuição. Ao selecionar essa opção, você deve pré-configurar o conteúdo no ponto de distribuição.  

    > [!IMPORTANT]  
    >  As opções anteriores são aplicáveis por pacote e são usadas somente quando um ponto de distribuição é identificado como pré-testado. Os pontos de distribuição que não foram identificados como pré-configurados ignoram essas configurações. Nesse caso, o conteúdo será sempre distribuído do servidor do site para os pontos de distribuição pela rede.  

-   **Para restaurar a biblioteca de conteúdo em um servidor de sites.** quando ocorre falha em um servidor do site, as informações sobre pacotes e aplicativos contidas na biblioteca de conteúdo são restauradas para o banco de dados do site como parte do processo de restauração, mas os arquivos dessa biblioteca não são restaurados como parte do processo. Se você não tiver um backup do sistema de arquivos para restaurar a biblioteca de conteúdo, é possível criar um arquivo de conteúdo pré-testado de outro site que contenha os pacotes e aplicativos que você precisa ter. Você pode, então, extrair o arquivo de conteúdo pré-testado no servidor de sites recuperado. Para saber mais sobre backup e recuperação do servidor de sites, veja [Backup e recuperação para o System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).  
