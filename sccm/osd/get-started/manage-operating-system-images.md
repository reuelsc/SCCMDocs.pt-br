---
title: Gerenciar imagens do sistema operacional | Microsoft Docs
description: "No Configuration Manager, saiba mais sobre os métodos que você pode usar para gerenciar imagens do sistema operacional que são armazenadas em arquivos do Windows Imaging (WIM)."
ms.custom: na
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
caps.latest.revision: 17
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 03722ff4f480cd26842e395fe1f7ec8359e2b33e
ms.openlocfilehash: 6953c3834ca303b949f22436010a87b3da9688dc


---
# <a name="manage-operating-system-images-with-system-center-configuration-manager"></a>Gerenciar imagens do sistema operacional com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As imagens do sistema operacional no Configuration Manager são armazenadas em arquivos de formato WIM (Windows Imaging) e representam uma coleção compactada de arquivos e pastas de referência necessários para instalar e configurar com êxito um sistema operacional em um computador. Para todos os cenários de implantação de sistema operacional, você deve selecionar uma imagem do sistema operacional.   Você pode usar a imagem do sistema operacional padrão ou compilar a imagem do sistema operacional de um computador de referência que você configura. Ao compilar o computador de referência, você pode adicionar arquivos do sistema operacional, drivers, arquivos de suporte, atualizações de software, ferramentas e outros aplicativos de software ao sistema operacional antes de capturá-lo para criar o arquivo de imagem. A seguir, veja informações sobre cada método.  

 **Imagem padrão**  

 A imagem padrão do sistema operacional (install.wim) é incluída com os arquivos de instalação do sistema operacional Windows. Essa imagem é uma imagem do sistema operacional básica que contém um conjunto padrão de drivers. Ao usar a imagem padrão do sistema operacional, você pode instalar aplicativos e fazer outras configurações depois de instalar o sistema operacional usando as etapas da sequência de tarefas.  A imagem padrão do sistema operacional está localizada em <*caminho de origem do sistema operacional*>\Sources\install.wim.  

-   **Vantagens**  

    -   O tamanho da imagem é menor do que uma imagem capturada.  

    -   A instalação de aplicativos e as configurações com etapas de sequências de tarefas são mais dinâmicas. Por exemplo, você pode alterar os aplicativos que serão instalados e as configurações da sequência de tarefas e não precisa recriar a imagem do sistema operacional.  

-   **Desvantagens**  

    -   A instalação do sistema operacional pode levar mais tempo porque a instalação do aplicativo e outras configurações ocorrem após a conclusão da instalação do sistema operacional.  

 **Imagem capturada**  

 Para criar uma imagem personalizada do sistema operacional, compile um computador de referência com o sistema operacional desejado, instale aplicativos, configure as configurações, etc. Em seguida, você pode capturar a imagem do sistema operacional do computador de referência para criar o arquivo WIM. É possível compilar o computador de referência manualmente ou usar uma sequência de tarefas para automatizar algumas ou todas as etapas de compilação.   
Para as etapas de criação de uma imagem personalizada do sistema operacional, consulte [Personalizar imagens do sistema operacional](customize-operating-system-images.md).  

-   **Vantagens**  

    -   A instalação pode ser mais rápida que usar a imagem padrão. Por exemplo, os aplicativos podem ser pré-instalados com a imagem capturada do sistema operacional e você não precisará instalar os aplicativos mais tarde usando as etapas da sequência de tarefas.  

-   **Desvantagens**  

    -   A instalação do sistema operacional pode levar mais tempo porque a instalação do aplicativo e outras configurações ocorrem após a conclusão da instalação do sistema operacional.  


##  <a name="a-namebkmkaddosimagesa-add-operating-system-images-to-configuration-manager"></a><a name="BKMK_AddOSImages"></a> Adicionar imagens do sistema operacional ao Configuration Manager  
 Antes de usar uma imagem do sistema operacional, você deve adicionar a imagem a um site do Configuration Manager. Use o procedimento a seguir para adicionar uma imagem do sistema operacional a um site.  

#### <a name="to-add-an-operating-system-image-to-a-site"></a>Para adicionar uma imagem do sistema operacional a um site  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Imagens do Sistema Operacional**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Adicionar Imagem do Sistema Operacional** para iniciar o Assistente para Adicionar Imagem do Sistema Operacional.  

4.  Na página de **Fonte de Dados** , especifique o caminho de rede para a imagem do sistema operacional. Por exemplo, especifique **\\\server\path\OS. WIM**.  

5.  Na página **Geral** , especifique as seguintes informações e clique em **Próximo**. Essa informação é útil para fins de identificação quando você adiciona várias imagens do sistema operacional no mesmo site.  

    -   **Nome**: especifique o nome da imagem. Por padrão, o nome da imagem é retirado do arquivo WIM.  

    -   **Versão**: especifique a versão da imagem.  

    -   **Comentário**: especifique uma breve descrição da imagem.  

6.  Conclua o assistente.  

 Você pode distribuir a imagem do sistema operacional para pontos de distribuição.  

##  <a name="a-namebkmkdistributebootimagesa-distribute-operating-system-images-to-distribution-points"></a><a name="BKMK_DistributeBootImages"></a> Distribuir imagens do sistema operacional para pontos de distribuição  
 Imagens do sistema operacional são distribuídas para os pontos de distribuição da mesma forma que outros conteúdos são distribuídos. Na maioria dos casos, você deve distribuir a imagem do sistema operacional para pelo menos um ponto de distribuição antes de implantar o sistema operacional. Para as etapas para distribuir uma imagem do sistema operacional, consulte [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content).  

##  <a name="a-namebkmkosimagesapplyupdatesa-apply-software-updates-to-an-operating-system-image"></a><a name="BKMK_OSImagesApplyUpdates"></a> Aplicar atualizações de software a uma imagem do sistema operacional  
 Periodicamente, são lançadas novas atualizações de software que se aplicam ao sistema operacional em sua imagem de sistema operacional. Antes de aplicar as atualizações de software a uma imagem, sua infraestrutura de atualizações de software deve estar em funcionamento, você deve ter sincronizado com êxito as atualizações de software e deve ter baixado as atualizações de software para a biblioteca de conteúdo no servidor do site. Para mais informações, consulte [Implantar atualizações de software](../../sum/deploy-use/deploy-software-updates.md).  

 Você pode aplicar as atualizações de software a uma imagem em um agendamento especificado. No agendamento que você especificar, o Configuration Manager aplica as atualizações de software que você selecionar na imagem do sistema operacional e, opcionalmente, distribui a imagem atualizada para os pontos de distribuição. As informações sobre a imagem do sistema operacional são armazenadas no banco de dados do site, incluindo as atualizações de software que foram aplicadas no momento da importação. As atualizações de software que foram aplicadas à imagem desde que ela foi inicialmente adicionada também são armazenadas no banco de dados do site. Ao iniciar o assistente para aplicar as atualizações de software à imagem do sistema operacional, o assistente recupera uma lista de atualizações de software aplicáveis que ainda não foram aplicadas à imagem para que você a selecione. O Configuration Manager copia as atualizações de software da biblioteca de conteúdo no servidor do site e aplica as atualizações de software à imagem do sistema operacional.  

 Use o procedimento a seguir para aplicar as atualizações de software a uma imagem do sistema operacional.  

#### <a name="to-apply-software-updates-to-an-operating-system-image"></a>Para aplicar atualizações de software a uma imagem do sistema operacional  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Imagens do Sistema Operacional**.  

3.  Selecione a imagem do sistema operacional a qual deseja aplicar atualizações de software.  

4.  Na guia **Início** , no grupo **Imagem do Sistema Operacional** , clique em **Agendar Atualizações** para iniciar o assistente.  

5.  Na página **Escolher Atualizações** , especifique as seguintes atualizações de software para aplicar à imagem do sistema operacional e clique em **Próximo**.  

6.  Na página **Definir Agendamento** , especifique as seguintes configurações e clique em **Próximo**.  

    1.  **Agendamento**: especifique o agendamento para quando as atualizações de software devem ser aplicadas à imagem do sistema operacional.  

    2.  **Continuar se houver erro**: selecione essa opção para continuar a aplicar as atualizações de software à imagem em caso de erro.  

    3.  **Distribuir a imagem para os pontos de distribuição**: selecione essa opção para atualizar a imagem do sistema operacional nos pontos de distribuição após as atualizações de software serem aplicadas.  

7.  Na página **Resumo** , verifique as seguintes informações e clique em **Próximo**.  

8.  Na página **Conclusão** , verifique se as atualizações de software foram aplicadas com êxito à imagem do sistema operacional.  

##  <a name="a-namebkmkosimagemulticasta-prepare-the-operating-system-image-for-multicast-deployments"></a><a name="BKMK_OSImageMulticast"></a> Preparar a imagem do sistema operacional para implantações multicast  
 Use implantações multicast para permitir que vários computadores baixem simultaneamente uma imagem do sistema operacional. A imagem é difundida via multicast para clientes pelo ponto de distribuição, em vez de o ponto de distribuição enviar uma cópia da imagem para cada cliente por uma conexão separada. Ao escolher o método de implantação de sistema operacional como [Usar o multicast para implantar o Windows pela rede](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md), é necessário configurar o pacote da imagem do sistema operacional para dar suporte a multicast antes de distribuir a imagem do sistema operacional para um ponto de distribuição habilitado para multicast. Use o procedimento a seguir para configurar as opções de multicast para um pacote de imagens do sistema operacional existente.  

#### <a name="to-modify-an-operating-system-image-package-to-use-multicast"></a>Para modificar um pacote de imagens do sistema operacional para usar multicast  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Imagens do Sistema Operacional**.  

3.  Selecione a imagem do sistema operacional que deseja distribuir para o ponto de distribuição habilitado para multicast.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Selecione a guia **Configurações de Distribuição** e configure as seguintes opções:  

    -   **Permitir que este pacote seja transferido via multicast (WinPE somente)**: é necessário selecionar essa opção para que o Configuration Manager implante simultaneamente as imagens do sistema operacional.  

    -   **Criptografar pacotes multicast**: especifique se a imagem é criptografada antes de ser enviada para o ponto de distribuição. Use essa opção se o pacote contiver informações confidenciais. Se a imagem não for criptografada, o conteúdo do pacote ficará visível em texto não criptografado na rede e poderá ser lido por um usuário não autorizado.  

    -   **Transferir este pacote somente via multicast**: especifique se deseja que o ponto de distribuição para implantar a imagem somente durante uma sessão de multicast.  

         Se a opção **Transferir este pacote somente via multicast**for selecionada, também será preciso especificar **Baixar conteúdo localmente quando necessário, executando a sequência de tarefas** como a opção de implantação da imagem do sistema operacional. É possível especificar as opções de implantação da imagem ao implantar a imagem do sistema operacional, ou você pode especificá-las mais tarde editando as propriedades da implantação. As opções de implantação estão na guia **Pontos de Distribuição** da página **Propriedades** do objeto de implantação.  

6.  Clique em **OK**.  



<!--HONumber=Dec16_HO2-->


