---
title: 'Gerenciar imagens de inicialização '
titleSuffix: Configuration Manager
description: No Configuration Manager, saiba como gerenciar as imagens de inicialização do Windows PE usadas durante uma implantação de sistema operacional.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a2fe20896a781d7c897bd5a827d25a7b70390b7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="manage-boot-images-with-system-center-configuration-manager"></a>Gerenciar imagens de inicialização com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Uma imagem de inicialização no Configuration Manager é uma imagem do [WinPE](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-intro) (Windows PE) usada durante uma implantação de sistema operacional. As imagens de inicialização são usadas para iniciar um computador no WinPE. Esse sistema operacional mínimo contém componentes e serviços limitados. O Configuration Manager usa o WinPE para preparar o computador de destino para a instalação do Windows. Use as seções a seguir para gerenciar imagens de inicialização.

## <a name="BKMK_BootImageDefault"></a> Imagens de inicialização padrão
O Configuration Manager fornece duas imagens de inicialização padrão: uma para dar suporte a plataformas x86 e outra para dar suporte a plataformas x64. Essas imagens são armazenadas em: \\\\*servername*>\SMS_<*sitecode*>\osd\boot\\<*x64*> ou <*i386*>. As imagens de inicialização padrão são atualizadas ou geradas novamente dependendo da ação que você tomar.

Considere os seguintes comportamentos de uma das ações descritas para as imagens de inicialização padrão:
- Os objetos do driver de origem devem ser válidos. Esses objetos incluem os arquivos de origem do driver. Se os objetos não são válidos, o site não adiciona os drivers às imagens de inicialização.
- As imagens de inicialização que não são baseadas nas imagens de inicialização padrão, mesmo se usarem a mesma versão do Windows PE, não serão modificadas.
- Redistribua as imagens de inicialização modificadas para os pontos de distribuição.
- Recrie as mídias que usam as imagens de inicialização modificadas.
- Se não quiser que suas imagens de inicialização padrão/personalizadas sejam atualizadas automaticamente, não as armazene no local padrão.

> [!NOTE]
> A Ferramenta Log de Rastreamento do Configuration Manager (CMTrace) é adicionada a todas as imagens de inicialização na **Biblioteca de Software**. Quando estiver no Windows PE, inicie a ferramenta digitando **CMTrace** no prompt de comando. A partir da versão 1802, ao iniciar o cmtrace.exe no Windows PE, você não precisa mais escolher se deseja tornar este programa o visualizador padrão para arquivos de log.

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Use atualizações e manutenção para instalar a versão mais recente do Configuration Manager
A partir da versão 1702, quando você atualiza a versão do Windows ADK (Kit de Avaliação e Implantação) e, em seguida, usa as atualizações e o serviço para instalar a última versão do Configuration Manager, o site regenera as imagens de inicialização padrão. Essa atualização inclui a nova versão do WinPE no Windows ADK atualizado e a nova versão de cliente, drivers, personalizações do Configuration Manager. O site não modifica imagens de inicialização personalizadas.

Antes da versão 1702, o Configuration Manager atualiza a imagem de inicialização existente com os componentes cliente, os drivers e as personalizações, mas não usa a última versão do WinPE no Windows ADK. Modifique manualmente a imagem de inicialização para usar a nova versão do Windows ADK.

### <a name="upgrade-from-configuration-manager-2012-to-configuration-manager-current-branch-cb"></a>Atualização do Configuration Manager 2012 para o Configuration Manager Branch Atual (CB)
Ao atualizar do Configuration Manager 2012 para o CB do Configuration Manager usando o processo de instalação, o site regenera as imagens de inicialização padrão. Essa atualização inclui a nova versão do WinPE no Windows ADK atualizado e a nova versão do cliente do Configuration Manager. Todas as personalizações da imagem de inicialização permanecem inalteradas. O site não modifica imagens de inicialização personalizadas.

### <a name="update-distribution-points-with-the-boot-image"></a>Atualizar pontos de distribuição com a imagem de inicialização
Quando você usa a ação **Atualizar Pontos de Distribuição** no nó **Imagens de Inicialização** do console, o site atualiza a imagem de inicialização de destino com os componentes cliente, os drivers e as personalizações.    

A partir do Configuration Manager versão 1706, recarregue a imagem de inicialização com a última versão do WinPE no diretório de instalação do Windows ADK. A página **Geral** do Assistente de Atualização de Pontos de Distribuição fornece as seguintes informações: 
 - A versão do Windows ADK instalada no servidor do site
 - A versão do Windows ADK do WinPE na imagem de inicialização
 - A versão do cliente do Configuration Manager Use essas informações para ajudar a decidir se a imagem de inicialização será recarregada. O nó **Imagens de Inicialização** também inclui uma nova coluna para (**Versão do Cliente**). Use essa coluna para exibir rapidamente a versão do cliente do Configuration Manager em cada imagem de inicialização.    


##  <a name="BKMK_BootImageCustom"></a> Personalizar uma imagem de inicialização  
 Quando uma imagem de inicialização é baseada na versão do WinPE da versão do Windows ADK compatível, você pode personalizar ou [modificar uma imagem de inicialização](#BKMK_ModifyBootImages) no console. Quando um site é atualizado com uma nova versão e uma nova versão do Windows ADK é instalada, as imagens de inicialização personalizadas (não no local da imagem de inicialização padrão) não são atualizadas com a nova versão do Windows ADK. Quando isso acontece, não é possível personalizar as imagens de inicialização no console do Configuration Manager. No entanto, elas continuam funcionando como antes da atualização.  

 Quando uma imagem de inicialização é baseada em uma versão diferente do Windows ADK instalada em um site, é necessário personalizar as imagens de inicialização. Use outro método para personalizar essas imagens de inicialização, como usar a ferramenta de linha de comando DISM (Gerenciamento e Manutenção de Imagens de Implantação). O DISM faz parte do Windows ADK. Para obter mais informações, consulte [Customize boot images (Personalizar imagens de inicialização)](customize-boot-images.md).  

##  <a name="BKMK_AddBootImages"></a> Adicionar uma imagem de inicialização  

 Durante a instalação do site, o Configuration Manager adiciona automaticamente imagens de inicialização baseadas em uma versão do WinPE da versão do Windows ADK com suporte. Dependendo da versão do Configuration Manager, é possível adicionar imagens de inicialização baseadas em uma versão do WinPE diferente da versão com suporte do Windows ADK. Ocorre um erro quando você tenta adicionar uma imagem de inicialização que contém uma versão do WinPE não compatível. A seguinte lista contém as versões do Windows ADK e WinPE atualmente compatíveis: 

-   **Versão do Windows ADK**  

     Windows ADK para Windows 10  

-   **Versões do Windows PE para imagens de inicialização personalizáveis no console do Configuration Manager**  

     Windows PE 10  

-   **Versões do Windows PE com suporte para imagens de inicialização não personalizáveis no console do Configuration Manager**  

     Windows PE 3.1<sup>1</sup> e Windows PE 5  

     <sup>1</sup> Só será possível adicionar uma imagem de inicialização ao Configuration Manager quando ela se basear no Windows PE 3.1. Atualize o Windows AIK para Windows 7 (baseado no Windows PE 3.0) com o Suplemento Windows AIK para Windows 7 SP1 (baseado no Windows PE 3.1). Baixe o Suplemento Windows AIK para Windows 7 SP1 no [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  

     Por exemplo, use o console do Configuration Manager para personalizar imagens de inicialização baseadas no Windows PE 10 no Windows ADK para Windows 10. Para uma imagem de inicialização baseada no Windows PE 5, personalize-a em outro computador usando a versão do DISM no Windows ADK para Windows 8. Em seguida, adicione a imagem de inicialização personalizada ao console do Configuration Manager. Para obter mais informações, consulte [Customize boot images (Personalizar imagens de inicialização)](customize-boot-images.md).

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

 A imagem de inicialização agora estará listada no nó **Imagem de Inicialização** do console do Configuration Manager. Antes de usar a imagem de inicialização para implantar um sistema operacional, distribua-a para os pontos de distribuição. 

> [!NOTE]  
>  No nó **Imagem de Inicialização** do console, a coluna **Tamanho (KB)** exibe o tamanho descompactado de cada imagem de inicialização. Quando o site envia uma imagem de inicialização pela rede, ele envia uma cópia compactada. Normalmente, essa cópia é menor que o tamanho listado na coluna **Tamanho (KB)**.  

##  <a name="BKMK_DistributeBootImages"></a> Distribuir imagens de inicialização para um ponto de distribuição  
 As imagens de inicialização são distribuídas para os pontos de distribuição da mesma forma que outros conteúdos são distribuídos. Na maioria dos casos, você precisa distribuir a imagem de inicialização para pelo menos um ponto de distribuição antes de implantar um sistema operacional e antes de criar a mídia.   

> [!NOTE]  
> Para usar o PXE para implantar um sistema operacional, considere os seguintes pontos antes de distribuir a imagem de inicialização:  
> - Configure o ponto de distribuição para aceitar solicitações PXE.  
> - Distribua imagens de inicialização x86 e x64 habilitadas para PXE para, pelo menos, um ponto de distribuição habilitado para PXE.  
> - O Configuration Manager distribui as imagens de inicialização para a pasta **RemoteInstall** no ponto de distribuição habilitado para PXE.  
>   
> Para obter mais informações sobre como usar o PXE para implantar sistemas operacionais, consulte [Usar PXE para implantar o Windows na rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 Para ver as etapas da distribuição de uma imagem de inicialização, consulte [Distribute content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  

##  <a name="BKMK_ModifyBootImages"></a> Modificar uma imagem de inicialização  
 Você pode adicionar ou remover drivers de dispositivo da imagem ou editar as propriedades associadas à imagem de inicialização. Os drivers de dispositivo adicionados ou removidos podem incluir adaptadores de rede ou drivers de armazenamento em massa. Ao modificar imagens de inicialização, considere os seguintes fatores:  

-   Importe e habilite os drivers de dispositivo no catálogo de drivers de dispositivo antes de adicioná-los à imagem de inicialização.  

-   Quando você modifica uma imagem de inicialização, ela não altera os pacotes associados aos quais a imagem de inicialização faz referência.  

-   Depois de fazer alterações na imagem de inicialização, **atualize** a imagem de inicialização nos pontos de distribuição que já têm a imagem. Esse processo disponibiliza a versão mais atual da imagem de inicialização aos clientes. Para obter mais informações, consulte [Manage content you have distributed](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_manage).  

 Use o procedimento a seguir para modificar uma imagem de inicialização.  

#### <a name="to-modify-the-properties-of-a-boot-image"></a>Para modificar as propriedades de uma imagem de inicialização  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Imagens de Inicialização**.  

3.  Selecione a imagem de inicialização que deseja modificar.  

4.  Na guia **Início** , no grupo **Propriedades** , clique em **Propriedades** para abrir a caixa de diálogo **Propriedades** da imagem de inicialização.  

5.  Defina qualquer uma das configurações a seguir para alterar o comportamento da imagem de inicialização:  

    -   Na guia **Imagens** , caso tenha alterado as propriedades da imagem de inicialização usando uma ferramenta externa, clique em **Recarregar**.  

    -   Na guia **Drivers** , adicione os drivers de dispositivo do Windows necessários para inicializar o WinPE. Considere os seguintes pontos ao adicionar drivers de dispositivo:  

        -   Selecione **Ocultar drivers que não correspondem à arquitetura da imagem de inicialização** para exibir apenas os drivers para a arquitetura da imagem de inicialização. A arquitetura é baseada na arquitetura relatada no INF do fabricante.  

        -   Selecione **Ocultar drivers que não estão em uma classe de armazenamento ou de rede (para imagens de inicialização)** para exibir somente os drivers de armazenamento e de rede. Essa opção também oculta outros drivers que, geralmente, não são necessários para as imagens de inicialização, como drivers de vídeo ou de modem.  

        -   Selecione **Ocultar drivers que não são assinados digitalmente** para ocultar os drivers que não têm uma assinatura digital válida.  

        -   Como uma melhor prática, adicione somente drivers de rede e de armazenamento em massa à imagem de inicialização, a menos que haja requisitos para outros drivers no WinPE.  

        -   Como o WinPE já é fornecido com muitos drivers integrados, adicione somente os drivers de rede e de armazenamento em massa não fornecidos pelo WinPE.  

        -   Verifique se os drivers adicionados à imagem de inicialização correspondem à arquitetura da imagem de inicialização.  

        > [!NOTE]  
        >  É necessário importar os drivers de dispositivo para o catálogo de drivers antes de adicioná-los a uma imagem de inicialização. Para obter informações sobre como importar drivers de dispositivo, consulte [Gerenciar drivers](manage-drivers.md).  

    -   Na guia **Personalização** , selecione qualquer uma das seguintes configurações:  

        -   Marque a caixa de seleção **Habilitar Comando Prestart** para especificar um comando a ser executado antes de a sequência de tarefas ser executada. Ao habilitar essa opção, especifique também a linha de comando a ser usada para execução e os arquivos de suporte necessários para o comando.  

            > [!WARNING]  
            >  Adicione **cmd /c** ao início da linha de comando. Se você não especificar **cmd /c**, o comando não será fechado depois de ser executado. A implantação continuará aguardando a conclusão do comando e não iniciará outras ações ou outros comandos configurados.  

            > [!TIP]  
            >  Durante a criação da mídia de sequência de tarefas, o assistente grava a ID do pacote e a linha de comando prestart, incluindo o valor das variáveis de sequência de tarefas, no arquivo de log CreateTSMedia.log. O log está no computador que executa o console do Configuration Manager. Examine este arquivo de log para verificar o valor das variáveis da sequência de tarefas.  

        -   Defina as configurações de **Plano de Fundo do Windows PE** para especificar se deseja usar o plano de fundo padrão do WinPE ou um plano de fundo personalizado.  

        -   Selecione **Habilitar suporte de comandos (teste somente)** para abrir um prompt de comando usando a tecla **F8** enquanto a imagem de inicialização é implantada. Essa opção é útil para solucionar problemas ao testar a implantação. Não é recomendável usar essa configuração em uma implantação de produção.  

        -   Configure o espaço transitório do Windows PE, que é o armazenamento temporário (unidade de RAM) usado pelo WinPE. Por exemplo, quando um aplicativo é executado no WinPE e precisa gravar arquivos temporários, o WinPE redireciona os arquivos para o espaço transitório na memória para simular a presença de uma unidade de disco. Por padrão, o WinPE aloca 32 megabytes (MB) de memória gravável.  

    -   Na guia **Fonte de Dados** , atualize qualquer uma das seguintes configurações:  

        -   Para alterar o arquivo de origem da imagem de inicialização, defina o **Caminho da imagem** e o **Índice de imagens**.  

        -   Para criar um agendamento que indica quando o site atualiza a imagem de inicialização, selecione **Atualizar pontos de distribuição de acordo com um agendamento**.  

        -   Caso não deseje que o conteúdo desse pacote seja excluído do cache do cliente para liberar espaço para outros tipos de conteúdo, selecione **Persistir conteúdo no cache do cliente**.  

        -   Para especificar que o site somente distribui arquivos alterados quando ele atualiza o pacote de imagem de inicialização no ponto de distribuição, selecione **Habilitar a BDR** (replicação diferencial binária). Essa configuração minimiza o tráfego de rede entre sites. A BDR é especialmente útil quando o pacote de imagem de inicialização é grande e as alterações são relativamente pequenas.  

        -   Se você usar a imagem de inicialização em uma implantação habilitada para PXE, selecione **Implantar essa imagem de inicialização por meio do ponto de distribuição habilitado para PXE**.  

            > [!NOTE]  
            >  Para obter mais informações, consulte [Usar PXE para implantar o Windows na rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   Na guia **Acesso a Dados** , selecione qualquer uma das seguintes configurações:  

        -   Defina as **Configurações de compartilhamento de pacote** se desejar que os clientes instalem o conteúdo desse pacote a partir da rede.  

        -   Defina as **Configurações de atualização de pacote** para especificar como você deseja que o Configuration Manager desconecte os usuários do ponto de distribuição. O Configuration Manager poderá não conseguir atualizar a imagem de inicialização quando os usuários estiverem conectados ao ponto de distribuição.  

    -   Na guia **Configurações de Distribuição** , selecione qualquer uma das seguintes configurações:  

        -   Na lista **Prioridade de distribuição**, especifique o nível de prioridade. O Configuration Manager usa essa lista de prioridades quando o site distribui vários pacotes para o mesmo ponto de distribuição.  

        -   Caso deseje habilitar a distribuição de conteúdo sob demanda para pontos de distribuição preferenciais, selecione **Distribuir o conteúdo deste pacote para os pontos de distribuição preferenciais**. Quando você habilita essa configuração, se um cliente solicita o conteúdo do pacote e o conteúdo não está disponível em um dos pontos de distribuição preferenciais, o ponto de gerenciamento distribui o conteúdo para todos os pontos de distribuição preferenciais.  

        -   Para especificar como deseja que o site distribua a imagem de inicialização para os pontos de distribuição habilitados para o conteúdo pré-teste, defina as **Configurações do ponto de distribuição pré-teste**.  

            > [!NOTE]  
            >  Para obter mais informações sobre como distribuir conteúdo pré-configurado, consulte [Prestage content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  

    -   N guia **Locais de Conteúdo** , selecione o ponto de distribuição ou o grupo de pontos de distribuição e execute uma das ações a seguir:  

        -   Clique em **Redistribuir** para distribuir a imagem de inicialização para o ponto de distribuição selecionado ou para o grupo de pontos de distribuição novamente.  

        -   Clique em **Validar** para verificar a integridade do pacote de imagem de inicialização no ponto de distribuição ou grupo de pontos de distribuição selecionado.  

    -   Na guia **Componentes Opcionais**, especifique os componentes que serão adicionados ao Windows PE para uso com o Configuration Manager. Para obter mais informações sobre os componentes opcionais disponíveis, consulte [WinPE: Adicionar pacotes (Referência de Componentes Opcionais)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).  

    -   Na guia **Segurança** , selecione um usuário administrativo e altere as operações que eles executam.  

6.  Depois de configurar as propriedades, clique em **OK**.  

##  <a name="BKMK_BootImagePXE"></a> Configurar uma imagem de inicialização para ser implantada de um ponto de distribuição habilitado para PXE  
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

##  <a name="BKMK_BootImageLanguage"></a> Configurar vários idiomas para implantação de imagem de inicialização  
 As imagens de inicialização têm neutralidade de idioma. Essa funcionalidade permite que você use uma imagem de inicialização para exibir o texto da sequência de tarefas em vários idiomas enquanto usa o WinPE. Inclua o suporte de idioma apropriado por meio da guia **Componentes Opcionais** da imagem de inicialização. Em seguida, defina a variável de sequência de tarefas apropriada para indicar qual idioma exibir. O idioma do sistema operacional implantado não depende do idioma do WinPE. O idioma que o WinPE exibe para o usuário é determinado da seguinte maneira:  

-   Quando um usuário executa uma sequência de tarefas de um sistema operacional existente, o Configuration Manager utiliza automaticamente o idioma configurado para o usuário. Quando a sequência de tarefas é executada automaticamente como resultado de um prazo de implantação obrigatória, o Configuration Manager utiliza o idioma do sistema operacional.  

-   Para implantações de sistema operacional que usam PXE ou mídia, defina o valor da ID de idioma na variável **SMSTSLanguageFolder** como parte de um comando prestart. Quando o computador inicializar o WinPE, as mensagens serão exibidas no idioma especificado na variável. Se ocorrer um erro ao acessar o arquivo de recurso de idioma na pasta especificada ou se você não definir a variável, o WinPE exibirá as mensagens no idioma padrão.  

    > [!NOTE]  
    >  Quando a mídia estiver protegida por senha, o texto que solicita uma senha ao usuário será sempre exibido no idioma do WinPE.  

 Use o procedimento a seguir para definir o idioma do WinPE para implantações de sistema operacional iniciadas por PXE ou mídia.  

#### <a name="to-set-the-windows-pe-language-for-a-pxe-or-media-initiated-operating-system-deployment"></a>Para definir o idioma do Windows PE para uma implantação de sistema operacional iniciada por PXE ou mídia  

1.  Verifique se o arquivo de recurso de sequência de tarefas apropriado (tsres.dll) está na pasta de idioma correspondente no servidor do site antes de atualizar a imagem de inicialização. Por exemplo, o arquivo de recurso em inglês está no seguinte local: <*ConfigMgrInstallationFolder*>\OSD\bin\x64\00000409\tsres.dll.  

2.  Como parte do comando prestart, configure a variável de ambiente SMSTSLanguageFolder para a ID de idioma apropriada. A ID de idioma deve ser especificada usando decimal e não hexadecimal. Por exemplo, para definir a ID de idioma como inglês, especifique o valor decimal 1033, não o valor hexadecimal 00000409 do nome da pasta.  
