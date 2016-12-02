---
title: "Gerenciar largura de banda de rede para conteúdo | System Center Configuration Manager"
description: "Definir agendamento, limitação e pré-configuração de conteúdo para o System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e80d1151-91db-4a27-8411-a957297b67d0
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 92a08908f284abb02ce8000122b0839c474616d7


---

##  <a name="a-namebkmkplanningforthrottlingascheduling-and-throttling"></a><a name="BKMK_PlanningForThrottling"></a>Agendamento e limitação  
 Para ajudar a gerenciar a largura de banda de rede usada no processo de gerenciamento de conteúdo, você pode usar controles internos do Configuration Manager para agendamento e limitação ou usar conteúdo pré-teste.  

 Ao criar um pacote, altere o caminho de origem do conteúdo ou atualize o conteúdo no ponto de distribuição; os arquivos são copiados do caminho de origem para a biblioteca de conteúdo no servidor do site. Em seguida, o conteúdo é copiado da biblioteca de conteúdo no servidor do site para a biblioteca de conteúdo nos pontos de distribuição. Quando os arquivos de origem do conteúdo são atualizados e os arquivos de origem já foram distribuídos, o Configuration Manager recupera somente os arquivos novos ou atualizados e os envia ao ponto de distribuição. Controles de agendamento e limitação podem ser configurados para comunicação de site a site e para comunicação entre um servidor do site e um ponto de distribuição remoto. Quando a largura de banda de rede entre o servidor do site e o ponto de distribuição remoto está limitada mesmo depois de definir configurações de agendamento e limitação, você pode considerar pré-configurar o conteúdo no ponto de distribuição.  

 No Configuration Manager, você pode configurar um agendamento e definir configurações de limitação específicas ou pontos de distribuição remotos que determinam quando e como a distribuição do conteúdo é realizada. Cada ponto de distribuição remoto pode ter configurações diferentes que ajudam a tratar limitações de largura de banda de rede do servidor do site para o ponto de distribuição remoto. Os controles usados para agendamento e limitação para o ponto de distribuição remoto são semelhantes às configurações de um endereço de remetente padrão, mas, nesse caso, as configurações são utilizadas por um novo componente chamado Gerenciador de Transferência de Pacote. O Gerenciador de Transferência de Pacote distribui o conteúdo de um servidor do site, como um site primário ou secundário, para um ponto de distribuição instalado em um sistema de site. As configurações de limitação são definidas na guia **Limites de Taxa** e as configurações de agendamento são definidas na guia **Agendamento** para um ponto de distribuição que não está em um servidor do site. As configurações de hora são baseadas no fuso horário do site de envio, não do ponto de distribuição.  

> [!WARNING]  
>  As guias **Limites de Taxa** e **Agendamento** são exibidas somente nas propriedades de pontos de distribuição que não estão instalados em um servidor do site.  

Para obter mais informações sobre como definir configurações de agendamento e limitação para um ponto de distribuição remoto, consulte [Instalar e configurar pontos de distribuição para o System Center Configuration Manager](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).  

##  <a name="a-namebkmkprestagingcontentaprestaged-content"></a><a name="BKMK_PrestagingContent"></a>Conteúdo pré-teste  
 Você pode pré-testar conteúdo para adicionar os arquivos de conteúdo à biblioteca de conteúdo em um servidor do site ou ponto de distribuição antes de distribuir o conteúdo  

-   Uma vez que os arquivos de conteúdo já estão na biblioteca de conteúdo, eles não são transferidos pela rede ao distribuir o conteúdo  

-   Você pode pré-testar arquivos de conteúdo para aplicativos e pacotes  

No console do Configuration Manager, selecione o conteúdo que deseja pré-configurar e use o **Assistente para Criar Arquivo de Conteúdo de Pré-Teste** para criar um arquivo compactado de conteúdo de pré-teste, que contenha os arquivos e metadados associados para o conteúdo. Em seguida, você pode importar manualmente o conteúdo em um servidor do site ou ponto de distribuição.  

-   Quando você importa o arquivo de conteúdo de pré-teste em um servidor do site, os arquivos de conteúdo são adicionados à biblioteca de conteúdo no servidor do site, e em seguida registrados no banco de dados do servidor do site  

-   Quando você importa o arquivo de conteúdo de pré-teste em um ponto de distribuição, os arquivos de conteúdo são adicionados à biblioteca de conteúdo no ponto de distribuição, e uma mensagem de status é enviada ao servidor do site informando que o conteúdo está disponível no ponto de distribuição  

Opcionalmente, você pode configurar o ponto de distribuição como **pré-testado** para ajudar a gerenciar a distribuição de conteúdo. Então, ao distribuir conteúdo, você pode escolher se deseja:  

-   Sempre pré-testar o conteúdo no ponto de distribuição  

-   Pré-testar o conteúdo inicial para o pacote e então usar o processo de distribuição de conteúdo padrão quando houver atualizações para o conteúdo  

-   Sempre usar o processo de distribuição de conteúdo padrão para o conteúdo no pacote  

###  <a name="a-namebkmkdeterminetoprestagecontentadetermine-whether-to-prestage-content"></a><a name="BKMK_DetermineToPrestageContent"></a>Determinar se deseja pré-testar o conteúdo  
 Considere a pré-configuração do conteúdo para aplicativos e pacotes nos seguintes cenários:  

-   **Largura de banda de rede limitada do servidor do site ao ponto de distribuição**: quando o agendamento e a limitação não satisfazem suas preocupações sobre distribuição de conteúdo pela rede para um ponto de distribuição remoto, considere pré-configurar o conteúdo no ponto de distribuição. Cada ponto de distribuição tem a configuração **Habilitar este ponto de distribuição para conteúdo pré-configurado** que você pode definir nas propriedades do ponto de distribuição. Quando você habilita essa opção, o ponto de distribuição é identificado como um ponto de distribuição pré-configurado, e você pode escolher como gerenciar o conteúdo por pacote.  

     As configurações a seguir estão disponíveis nas propriedades de um aplicativo, pacote, pacote de driver, imagem de inicialização, instalador do sistema operacional e imagem, e permitem definir como a distribuição do conteúdo é gerenciada em pontos de distribuição remotos identificados como pré-configurados:  

    -   **Baixar conteúdo automaticamente quando pacotes forem atribuídos a pontos de distribuição**: use esta opção quando você tem pacotes menores em que as configurações de agendamento e limitação fornecem controle suficiente para distribuição do conteúdo.  

    -   **Baixar somente alterações ao conteúdo para o ponto de distribuição**: use essa opção quando você tiver um pacote inicial possivelmente grande, mas você esperar que futuras atualizações ao conteúdo no pacote sejam menores em geral. Por exemplo, você pode pré-testar um aplicativo como o Microsoft Office porque o tamanho inicial do pacote é maior que 700 MB e muito grande para ser enviado pela rede. No entanto, as atualizações de conteúdo nesse pacote podem ser inferiores a 10 MB e são aceitáveis para distribuição pela rede. Outro exemplo pode ser pacotes de driver em que o tamanho inicial do pacote é grande, mas adições de driver incrementais ao pacote podem ser pequenas.  

    -   **Copiar manualmente o conteúdo deste pacote para o ponto de distribuição**: use esta opção no caso de pacotes grandes, com conteúdo como um sistema operacional, e quando você nunca desejar usar a rede para distribuir o conteúdo para o ponto de distribuição. Ao selecionar essa opção, você deve pré-configurar o conteúdo no ponto de distribuição.  

    > [!WARNING]  
    >  As opções anteriores são aplicáveis por pacote e são usadas somente quando um ponto de distribuição é identificado como pré-configurado. Os pontos de distribuição que não foram identificados como pré-configurados ignoram essas configurações. Nesse caso, o conteúdo será sempre distribuído do servidor do site para os pontos de distribuição pela rede.  

-   **Restaurar a biblioteca de conteúdo em um servidor do site**: quando ocorre falha em um servidor do site, as informações sobre pacotes e aplicativos contidas na biblioteca de conteúdo são restauradas para o banco de dados do site como parte do processo de restauração, mas os arquivos dessa biblioteca não são restaurados como parte do processo. Se não tiver um backup do sistema de arquivos para restaurar a biblioteca de conteúdo, você poderá criar um arquivo de conteúdo pré-configurado de outro site que contenha os pacotes e aplicativos que você precisa ter e extrair o arquivo de conteúdo pré-configurado no servidor do site recuperado. Para obter mais informações sobre backup e recuperação do servidor do site, consulte [Backup e recuperação para o System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery)  



<!--HONumber=Nov16_HO1-->


