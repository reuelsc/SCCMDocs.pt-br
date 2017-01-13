---
title: "Gerenciar imagens de inicialização | Microsoft Docs"
description: "No Configuration Manager, saiba como gerenciar as imagens de inicialização do Windows PE usadas durante uma implantação de sistema operacional."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
caps.latest.revision: 23
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: 8c41c39a7f984be2612ae882d3bc08d92278dba6


---
# <a name="manage-boot-images-with-system-center-configuration-manager"></a>Gerenciar imagens de inicialização com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Uma imagem de inicialização no Configuration Manager é uma imagem do [WinPE (Windows PE)](https://msdn.microsoft.com/library/windows/hardware/dn938389%28v=vs.85%29.aspx) usada durante uma implantação de sistema operacional. Imagens de inicialização são usadas para iniciar um computador no WinPE, que é um sistema operacional mínimo com componentes e serviços limitados que preparam o computador de destino para a instalação do Windows.  Use as seções a seguir para gerenciar imagens de inicialização.

##  <a name="a-namebkmkbootimagedefaulta-default-boot-images"></a><a name="BKMK_BootImageDefault"></a> Imagens de inicialização padrão  
 O Configuration Manager fornece duas imagens de inicialização padrão: uma para dar suporte a plataformas x86 e outra para dar suporte a plataformas x64. Essas imagens são armazenadas em: \\\\*nomedoservidor*>\SMS_<*códigodosite*>\osd\boot\\<*x64 ou i386*.  

 Quando você atualiza o Configuration Manager para uma nova versão, o Configuration Manager pode substituir as imagens de inicialização padrão e as imagens de inicialização personalizadas baseadas nas imagens de inicialização padrão, nesse local, pelos arquivos atualizados. As opções que podem ser configuradas nas imagens de inicialização padrão no site (como componentes opcionais) são transportadas quando as imagens de inicialização são atualizadas, inclusive drivers. Os objetos de driver de origem devem ser válidos, incluindo os arquivos de origem do driver, ou os drivers não serão adicionados às imagens de inicialização atualizada no site. Outras imagens de inicialização que não sejam baseadas em imagens de inicialização padrão, mesmo se baseadas na mesma versão do Windows ADK, não serão atualizadas. Após a atualização das imagens de inicialização, você precisará redistribuí-las aos pontos de distribuição. Qualquer mídia que use as imagens de inicialização precisará ser recriada. Se não quiser que suas imagens de inicialização padrão personalizadas sejam atualizadas automaticamente, você deverá armazená-las em um local diferente.  

 A ferramenta Log de Rastreamento do Configuration Manager é adicionada a todas as imagens de inicialização que você adiciona à **Biblioteca de Software**. Quando você estiver no WinPE, será possível iniciar a ferramenta Rastreamento de Log do Configuration Manager digitando **CMTrace** em um prompt de comando.  

##  <a name="a-namebkmkbootimagecustoma-customize-a-boot-image"></a><a name="BKMK_BootImageCustom"></a> Personalizar uma imagem de inicialização  
 É possível personalizar uma imagem de inicialização ou [Modificar uma imagem de inicialização](#BKMK_ModifyBootImages) no console do Configuration Manager quando ele é baseado em uma versão do Windows PE de uma versão do Windows ADK com suporte. Quando um site for atualizado com uma nova versão e uma nova versão do Windows ADK for instalada, as imagens de inicialização personalizadas (não no local da imagem de inicialização padrão) não serão atualizadas com a nova versão do Windows ADK. Quando isso acontecer, não será mais possível personalizar as imagens de inicialização no console do Configuration Manager. No entanto, elas continuarão funcionando como antes da atualização.  

 Quando uma imagem de inicialização é baseada em uma versão diferente do Windows ADK instalada em um site, você deverá personalizar as imagens de inicialização usando outro método, como usar a ferramenta de linha de comando DISM (Gerenciamento e Manutenção de Imagens de Implantação) que faz parte do Windows AIK e Windows ADK. Para obter mais informações, consulte [Customize boot images (Personalizar imagens de inicialização)](customize-boot-images.md).  

##  <a name="a-namebkmkaddbootimagesa-add-a-boot-image"></a><a name="BKMK_AddBootImages"></a> Adicionar uma imagem de inicialização  

 Durante a instalação do site, o Configuration Manager adiciona automaticamente imagens de inicialização baseadas em uma versão do WinPE da versão do Windows ADK com suporte. Dependendo da versão do Configuration Manager, é possível adicionar imagens de inicialização baseadas em uma versão do WinPE diferente da versão com suporte do Windows ADK.  Ocorre um erro quando você tenta adicionar uma imagem de inicialização que contém uma versão do WinPE sem suporte.  

 Veja a seguir a versão com suporte do Windows ADK, a versão do Windows PE na qual se baseia a imagem de inicialização que pode ser personalizada no console do Configuration Manager e as versões do Windows PE nas quais se baseia a imagem de inicialização que pode ser personalizada usando o DISM e, em seguida, adicione a imagem ao Configuration Manager.  

-   **Versão do Windows ADK**  

     Windows ADK para Windows 10  

-   **Versões do Windows PE para imagens de inicialização personalizáveis no console do Configuration Manager**  

     Windows PE 10  

-   **Versões do Windows PE com suporte para imagens de inicialização não personalizáveis no console do Configuration Manager**  

     Windows PE 3.1<sup>1</sup> e Windows PE 5  

     <sup>1</sup> Só será possível adicionar uma imagem de inicialização ao Configuration Manager quando ela se basear no Windows PE 3.1. Instale o Suplemento do Windows AIK para Windows 7 SP1 a fim de atualizar o Windows AIK para Windows 7 (baseado no Windows PE 3) com o Suplemento do Windows AIK para Windows 7 SP1 (baseado no Windows PE 3.1). Você pode baixar o Suplemento do Windows AIK para Windows 7 SP1 do [Centro de Download da Microsoft](http://www.microsoft.com/download/details.aspx?id=5188).  

     Por exemplo, quando você tiver o Configuration Manager, será possível personalizar as imagens de inicialização do Windows ADK para Windows 10 (baseado no Windows PE 10) no console do Configuration Manager. No entanto, embora haja suporte para imagens de inicialização baseadas no Windows PE 5, você deverá personalizá-las em outro computador e usar a versão do DISM instalada com o Windows ADK para Windows 8. Em seguida, é possível adicionar a imagem de inicialização ao console do Configuration Manager. Para obter mais informações sobre as etapas para personalizar uma imagem de inicialização (adicionar componentes e drivers opcionais), habilitar o suporte de comandos para a imagem de inicialização, adicionar a imagem de inicialização ao console do Configuration Manager e atualizar os pontos de distribuição com ela, consulte [Personalizar imagens de inicialização](customize-boot-images.md).

 Use o procedimento a seguir para adicionar manualmente uma imagem de inicialização.  

#### <a name="to-add-a-boot-image"></a>Para adicionar uma imagem de inicialização  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Imagens de Inicialização**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Adicionar Imagem de Inicialização** para o Assistente para Adicionar Imagem de Inicialização.  

4.  Na página **Fonte de Dados** , especifique as seguintes opções e clique em **Próximo**.  

    -   Na caixa **Caminho** , especifique o caminho para o arquivo WIM de imagem de inicialização.  

         O caminho especificado deve ser um caminho de rede válido no formato UNC. Por exemplo: \\\\<*nome do servidor*\\<*nome do compartilhamento*>\\<*nomedaimagemdeinicialização*>.wim.  

    -   Selecione a imagem de inicialização na lista suspensa **Imagem de Inicialização** . Se o arquivo WIM contiver várias imagens de inicialização, selecione a imagem adequada.  

5.  Na página **Geral**  , especifique as opções a seguir e clique em **Próximo**.  

    -   Na caixa **Nome** , especifique um nome exclusivo para a imagem de inicialização.  

    -   Na caixa **Versão** , especifique um número de versão para a imagem de inicialização.  

    -   Na caixa **Comentário** , faça uma breve descrição de como a imagem de inicialização é usada.  

6.  Conclua o assistente.  

 A imagem de inicialização agora estará listada no nó **Imagem de Inicialização** do console do Configuration Manager. No entanto, antes de usar a imagem de inicialização para implantar um sistema operacional, é necessário distribuir a imagem de inicialização para pontos de distribuição, grupos de pontos de distribuição ou para coleções associadas a grupos de pontos de distribuição.  

> [!NOTE]  
>  Ao selecionar o nó **Imagem de Inicialização** no console do Configuration Manager, a coluna **Tamanho (KB)** exibe o tamanho descompactado de cada imagem de inicialização. No entanto, quando o Configuration Manager envia a imagem de inicialização pela rede, ele envia uma cópia compactada da imagem, que normalmente é bem menor que o tamanho exibido na coluna **Tamanho (KB)**.  

##  <a name="a-namebkmkdistributebootimagesa-distribute-boot-images-to-a-distribution-point"></a><a name="BKMK_DistributeBootImages"></a> Distribuir imagens de inicialização para um ponto de distribuição  
 As imagens de inicialização são distribuídas para os pontos de distribuição da mesma forma que outros conteúdos são distribuídos. Na maioria dos casos, você precisa distribuir a imagem de inicialização para pelo menos um ponto de distribuição antes de implantar um sistema operacional e antes de criar a mídia.  

> [!NOTE]  
>  Para usar o PXE para implantar um sistema operacional, considere o seguinte antes de distribuir a imagem de inicialização:  
>   
>  -   O ponto de distribuição deve ser configurado para aceitar solicitações de PXE.  
> -   Você deve distribuir imagens de inicialização x86 e x64 habilitadas para PXE para pelo menos um ponto de distribuição habilitado para PXE.  
> -   O Configuration Manager distribui as imagens de inicialização para a pasta **RemoteInstall** no ponto de distribuição habilitado para PXE.  
>   
>  Para obter mais informações sobre como usar o PXE para implantar sistemas operacionais, consulte [Usar PXE para implantar o Windows na rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 Para ver as etapas da distribuição de uma imagem de inicialização, consulte [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content).  

##  <a name="a-namebkmkmodifybootimagesa-modify-a-boot-image"></a><a name="BKMK_ModifyBootImages"></a> Modificar uma imagem de inicialização  
 Você pode adicionar ou remover drivers de dispositivo da imagem ou editar as propriedades associadas à imagem de inicialização. Os drivers de dispositivo adicionados ou removidos podem incluir adaptadores de rede ou drivers de armazenamento em massa. Ao modificar imagens de inicialização, considere os seguintes fatores:  

-   Você deve importar e habilitar os drivers de dispositivo no catálogo de drivers do dispositivo antes de adicioná-los à imagem de inicialização.  

-   Quando você modifica uma imagem de inicialização, ela não altera os pacotes associados aos quais a imagem de inicialização faz referência.  

-   Após fazer alterações na imagem de inicialização, você deve **atualizar** a imagem de inicialização nos pontos de distribuição que já têm a imagem, de modo que a versão mais atual da imagem de inicialização esteja disponível. Para obter mais informações, consulte [Manage content you have distributed](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkmanagea-manage-the-content-you-have-distributed).  

 Use o procedimento a seguir para modificar uma imagem de inicialização.  

#### <a name="to-modify-the-properties-of-a-boot-image"></a>Para modificar as propriedades de uma imagem de inicialização  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Imagens de Inicialização**.  

3.  Selecione a imagem de inicialização que deseja modificar.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades** para abrir a caixa de diálogo **Propriedades** da imagem de inicialização.  

5.  Defina qualquer uma das configurações a seguir para alterar o comportamento da imagem de inicialização:  

    -   Na guia **Imagens** , caso tenha alterado as propriedades da imagem de inicialização usando uma ferramenta externa, clique em **Recarregar**.  

    -   Na guia **Drivers** , adicione os drivers de dispositivo do Windows necessários para inicializar o WinPE. Ao adicionar drivers de dispositivo, considere o seguinte:  

        -   Selecione **Ocultar drivers que não correspondem à arquitetura da imagem de inicialização** para exibir apenas os drivers para a arquitetura da imagem de inicialização. A arquitetura é baseada na arquitetura relatada no .INF do fabricante.  

        -   Selecione **Ocultar drivers que não estão em uma classe de armazen. ou de rede (para imagens de inic.)** para exibir somente os drivers de armazenamento e de rede e para ocultar outros drivers que geralmente não são necessários para as imagens de inicialização, como um driver de vídeo ou de modem.  

        -   Selecione **Ocultar drivers que não são assinados digitalmente** para ocultar drivers que não são assinados digitalmente.  

        -   Como uma prática recomendada, adicione somente drivers NIC e de armazenamento em massa à imagem de inicialização, a menos que haja requisitos para que outros drivers façam parte do WinPE.  

        -   Como o WinPE já é fornecido com muitos drivers integrados, adicione somente drivers NIC e de armazenamento em massa não fornecidos pelo WinPE.  

        -   Verifique se os drivers adicionados à imagem de inicialização correspondem à arquitetura da imagem de inicialização.  

        > [!NOTE]  
        >  É necessário importar os drivers de dispositivo para o catálogo de drivers antes de adicioná-los a uma imagem de inicialização. Para obter informações sobre como importar drivers de dispositivo, consulte [Gerenciar drivers](manage-drivers.md).  

    -   Na guia **Personalização** , selecione qualquer uma das seguintes configurações:  

        -   Marque a caixa de seleção **Habilitar Comando Prestart** para especificar um comando a ser executado antes de a sequência de tarefas ser executada. Quando os comando prestart são habilitados, é possível especificar a linha de comando que será executada, se serão necessários arquivos com suporte para executar o comando e o local de origem desses arquivos com suporte.  

            > [!WARNING]  
            >  É preciso adicionar **cmd /c** ao início da linha de comando. Se você não especificar **cmd /c**, o comando não será fechado depois que for executado. A implantação continuará aguardando o comando ser finalizado e não iniciará outros comandos e ações configurados.  

            > [!TIP]  
            >  Durante a criação de mídia de sequência de tarefas, a sequência de tarefas grava a ID do pacote e a linha de comando prestart, que inclui o valor de quaisquer variáveis de sequência de tarefas, no arquivo de log CreateTSMedia.log no computador que executa o console do Configuration Manager. Você poderá analisar esse arquivo de log para verificar o valor das variáveis de sequência de tarefas.  

        -   Defina as configurações de **Plano de Fundo do Windows PE** para especificar se deseja usar o plano de fundo padrão do WinPE ou um plano de fundo personalizado.  

        -   Selecione **Habilitar suporte de comandos (teste somente)** para abrir um prompt de comando usando a tecla **F8** enquanto a imagem de inicialização é implantada. Isso é útil para solucionar problemas ao testar a implantação. Não é recomendável usar essa configuração em uma implantação de produção.  

        -   Configure o espaço transitório do Windows PE, que é o armazenamento temporário (unidade de RAM) usado pelo WinPE. Por exemplo, quando um aplicativo é executado no WinPE e precisa gravar arquivos temporários, o WinPE redireciona os arquivos para o espaço transitório na memória para simular a presença de uma unidade de disco. Por padrão, o WinPE aloca 32 megabytes (MB) de memória gravável.  

    -   Na guia **Fonte de Dados** , atualize qualquer uma das seguintes configurações:  

        -   Configure **Caminho da imagem** e **Índice de imagem** para alterar o arquivo de origem da imagem de inicialização.  

        -   Selecione **Atualizar pontos de distribuição em um cronograma** para criar um agendamento de quando o pacote de imagem de inicialização é atualizado.  

        -   Selecione **Conteúdo persistente em cache de cliente** se não desejar que o conteúdo desse pacote seja excluído do cache do cliente após determinado tempo para liberar espaço.  

        -   Selecione **Habilitar replicação diferencial binária** para especificar que somente os arquivos alterados serão distribuídos quando a imagem de inicialização for atualizada no ponto de distribuição. Essa configuração minimiza o tráfego de rede entre sites, especialmente quando o pacote de imagem de inicialização é grande e as alterações são relativamente pequenas.  

        -   Escolha **Implantar esta imagem de inicialização do ponto de distribuição habilitado para PXE** se a imagem de inicialização for usada em uma implantação habilitada para PXE.  

            > [!NOTE]  
            >  Para obter mais informações, consulte [Usar PXE para implantar o Windows na rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   Na guia **Acesso a Dados** , selecione qualquer uma das seguintes configurações:  

        -   Defina as **Configurações de compartilhamento de pacote** se desejar que os clientes instalem o conteúdo desse pacote a partir da rede.  

        -   Defina as **Configurações de atualização de pacote** para especificar como você deseja que o Configuration Manager desconecte os usuários do ponto de distribuição. O Configuration Manager poderá não conseguir atualizar a imagem de inicialização quando os usuários estiverem conectados ao ponto de distribuição.  

    -   Na guia **Configurações de Distribuição** , selecione qualquer uma das seguintes configurações:  

        -   Na lista **Prioridade de distribuição**, especifique o nível de prioridade que você deseja que o Configuration Manager use quando vários pacotes forem distribuídos para o mesmo ponto de distribuição.  

        -   Selecione **Distribuir o conteúdo deste pacote para os pontos de distribuição preferenciais** se desejar habilitar a distribuição de conteúdo sob demanda para pontos de distribuição preferenciais. Quando essa configuração é habilitada, o ponto de gerenciamento distribui o conteúdo para todos os pontos de distribuição preferenciais quando um cliente solicita o conteúdo do pacote e o conteúdo está indisponível em qualquer um dos pontos de distribuição preferenciais.  

        -   Defina as **Configurações de ponto de distribuição em pré-teste** para especificar como deseja que a imagem de inicialização seja distribuída a pontos de distribuição habilitados para conteúdo em pré-teste.  

            > [!NOTE]  
            >  Para obter mais informações sobre como distribuir conteúdo pré-configurado, consulte [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkprestagea-use-prestaged-content).  

    -   N guia **Locais de Conteúdo** , selecione o ponto de distribuição ou o grupo de pontos de distribuição e execute uma das ações a seguir:  

        -   Clique em **Redistribuir** para distribuir a imagem de inicialização para o ponto de distribuição selecionado ou para o grupo de pontos de distribuição novamente.  

        -   Clique em **Validar** para verificar a integridade do pacote de imagem de inicialização no ponto de distribuição ou grupo de pontos de distribuição selecionado.  

    -   Na guia **Componentes Opcionais**, especifique os componentes que serão adicionados ao Windows PE para uso com o Configuration Manager. Para obter mais informações sobre os componentes opcionais disponíveis, consulte [WinPE: Adicionar pacotes (Referência de Componentes Opcionais)](https://msdn.microsoft.com/library/windows/hardware/dn938382\(v=vs.85\).aspx).  

    -   Na guia **Segurança** , selecione um usuário administrativo e altere as operações que eles executam.  

6.  Depois de configurar as propriedades, clique em **OK**.  

##  <a name="a-namebkmkbootimagepxea-configure-a-boot-image-to-deploy-from-a-pxe-enabled-distribution-point"></a><a name="BKMK_BootImagePXE"></a> Configurar uma imagem de inicialização para ser implantada de um ponto de distribuição habilitado para PXE  
 Antes que seja possível usar uma imagem de inicialização para uma implantação de sistema operacional do PXE, é necessário configurar a imagem de inicialização para ser implantada de um ponto de distribuição habilitado para PXE.  

#### <a name="to-configure-a-boot-image-to-deploy-from-a-pxe-enabled-distribution-point"></a>Para configurar uma imagem de inicialização para ser implantada de um ponto de distribuição habilitado para PXE  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Imagens de Inicialização**.  

3.  Selecione a imagem de inicialização que deseja modificar.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades** para abrir a caixa de diálogo **Propriedades** da imagem de inicialização.  

5.  Na guia **Fonte de Dados** , selecione **Implantar esta imagem de inicialização do ponto de distribuição habilitado para PXE**.  

    > [!NOTE]  
    >  Para obter mais informações, consulte [Usar PXE para implantar o Windows na rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

6.  Depois de configurar as propriedades, clique em **OK**.  

##  <a name="a-namebkmkbootimagelanguagea-configure-multiple-languages-for-boot-image-deployment"></a><a name="BKMK_BootImageLanguage"></a> Configurar vários idiomas para implantação de imagem de inicialização  
 As imagens de inicialização têm neutralidade de idioma. Isso permite que você use uma imagem de inicialização que exiba o texto de sequência de tarefas em diversos idiomas. No WinPE, no entanto, seria necessário incluir o suporte de idioma apropriado dos Componentes Opcionais do Windows PE e definir a variável de sequência de tarefas apropriada, para indicar qual idioma poderia ser exibido. O idioma do sistema operacional implantado é independente do idioma exibido no WinPE, em qualquer versão do Configuration Manager. O idioma que será exibido para o usuário é determinado como segue:  

-   Quando um usuário executa uma sequência de tarefas de um sistema operacional existente, o Configuration Manager utiliza automaticamente o idioma configurado para o usuário. Quando a sequência de tarefas é executada automaticamente como resultado de um prazo de implantação obrigatória, o Configuration Manager utiliza o idioma do sistema operacional.  

-   Para implantações de sistema operacional que utilizam PXE ou mídia, você pode configurar o valor de ID do idioma na variável SMSTSLanguageFolder como parte de um comando prestart. Quando o computador inicializar o WinPE, as mensagens serão exibidas no idioma especificado na variável. Se ocorrer um erro ao acessar o arquivo de recursos de idioma na pasta especificada, ou se você não tiver definido a variável, as mensagens serão exibidas no idioma do WinPE.  

    > [!NOTE]  
    >  Quando a mídia estiver protegida por senha, o texto que solicita uma senha ao usuário será sempre exibido no idioma do WinPE.  

 Use o procedimento a seguir para definir o idioma do WinPE para implantações de sistema operacional iniciadas por PXE ou mídia.  

#### <a name="to-set-the-windows-pe-language-for-a-pxe-or-media-initiated-operating-system-deployment"></a>Para definir o idioma do Windows PE para uma implantação de sistema operacional iniciada por PXE ou mídia  

1.  Verifique se o arquivo de recurso de sequência de tarefas apropriado (tsres.dll) está na pasta de idioma correspondente, no servidor do site, antes de atualizar a imagem de inicialização. Por exemplo, o arquivo de recurso em inglês está no seguinte local: <*ConfigMgrInstallationFolder*> \OSD\bin\x64\00000409\tsres.dll.  

2.  Como parte do comando prestart, configure a variável de ambiente SMSTSLanguageFolder para a ID de idioma apropriada. A ID de idioma deve ser especificada usando decimal e não hexadecimal. Por exemplo, para configurar o ID do idioma para inglês, especifique o valor decimal 1033 em vez do valor hexadecimal 00000409, usado para o nome da pasta.  



<!--HONumber=Dec16_HO3-->


