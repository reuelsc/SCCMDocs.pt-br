---
title: Gerenciar imagens de inicialização
titleSuffix: Configuration Manager
description: No Configuration Manager, saiba como gerenciar as imagens de inicialização do Windows PE usadas durante uma implantação de SO.
ms.date: 02/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ddc856b3c1615045aadba60c4616223349a7b61d
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68340412"
---
# <a name="manage-boot-images-with-configuration-manager"></a>Gerenciar imagens de inicialização com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Uma imagem de inicialização no Configuration Manager é uma imagem do [Windows PE](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-intro) (WinPE) usada durante uma implantação de SO. As imagens de inicialização são usadas para iniciar um computador no WinPE. Esse SO mínimo contém componentes e serviços limitados. O Configuration Manager usa o WinPE para preparar o computador de destino para a instalação do Windows. 



## <a name="BKMK_BootImageDefault"></a> Imagens de inicialização padrão

O Configuration Manager fornece duas imagens de inicialização padrão: uma para dar suporte a plataformas x86 e outra para dar suporte a plataformas x64. Essas imagens são armazenadas nas pastas *x64* ou *i386* no seguinte compartilhamento no servidor do site: `\\<SiteServerName>\SMS_<sitecode>\osd\boot\`. As imagens de inicialização padrão são atualizadas ou geradas novamente dependendo da ação que você tomar.

Considere os seguintes comportamentos de uma das ações descritas para as imagens de inicialização padrão:

- Os objetos do driver de origem devem ser válidos. Esses objetos incluem os arquivos de origem do driver. Se os objetos não são válidos, o site não adiciona os drivers às imagens de inicialização.  

- As imagens de inicialização que não são baseadas nas imagens de inicialização padrão, mesmo se usarem a mesma versão do Windows PE, não serão modificadas.  

- Redistribua as imagens de inicialização modificadas para os pontos de distribuição.  

- Recrie as mídias que usam as imagens de inicialização modificadas.  

- Se não quiser que suas imagens de inicialização padrão/personalizadas sejam atualizadas automaticamente, não as armazene no local padrão.  

> [!NOTE]
> A ferramenta log do Configuration Manager (**CMTrace**) é adicionada a todas as imagens de inicialização na **Biblioteca de Software**. Quando estiver no Windows PE, inicie a ferramenta digitando `cmtrace` no prompt de comando. 
> 
> A partir da versão 1802, ao iniciar o CMTrace no Windows PE, você não precisa mais escolher se deseja tornar este programa o visualizador padrão para arquivos de log.


### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Use atualizações e manutenção para instalar a versão mais recente do Configuration Manager

Quando você atualiza a versão do Windows ADK (Kit de Avaliação e Implantação) e, em seguida, usa as atualizações e o serviço para instalar a última versão do Configuration Manager, o site regenera as imagens de inicialização padrão. Essa atualização inclui a nova versão do WinPE no Windows ADK atualizado e a nova versão de cliente, drivers, personalizações do Configuration Manager. O site não modifica imagens de inicialização personalizadas.


### <a name="upgrade-from-configuration-manager-2012-to-current-branch"></a>Atualização do Configuration Manager 2012 para o branch atual

Quando você atualiza o Configuration Manager 2012 para o branch atual, o site gera novamente as imagens de inicialização padrão. Essa atualização inclui a nova versão do WinPE no Windows ADK atualizado e a nova versão do cliente do Configuration Manager. Todas as personalizações da imagem de inicialização permanecem inalteradas. O site não modifica imagens de inicialização personalizadas.


### <a name="update-distribution-points-with-the-boot-image"></a>Atualizar pontos de distribuição com a imagem de inicialização

Quando você usa a ação **Atualizar Pontos de Distribuição** no nó **Imagens de Inicialização** do console, o site atualiza a imagem de inicialização de destino com os componentes cliente, os drivers e as personalizações.    

Você pode recarregar a imagem de inicialização com a versão mais recente do WinPE no diretório de instalação do Windows ADK. A página **Geral** do Assistente de Atualização de Pontos de Distribuição fornece as seguintes informações: 
- A versão atual do Windows ADK instalada no servidor do site
- A versão atual do cliente de produção
- A versão do Windows ADK do WinPE na imagem de inicialização
- A versão do cliente do Configuration Manager na imagem de inicialização

Se as versões na imagem de inicialização estiverem desatualizadas, use a opção para **Recarregar essa imagem de inicialização com a versão atual do Windows PE no Windows ADK**. 

> [!Important]  
> Esta ação está disponível para imagens de inicialização padrão e personalizadas. Durante esse processo para recarregar a imagem de inicialização, o site não mantém qualquer personalização manual feita fora do Configuration Manager. Essas personalizações incluem extensões de terceiros. Essa opção recria a imagem de inicialização usando a versão mais recente do WinPE e a versão mais recente do cliente. Somente as configurações especificadas nas propriedades da imagem de inicialização são reaplicadas. <!--SCCMDocs issue #1283-->

O nó **Imagens de Inicialização** também inclui uma nova coluna para (**Versão do Cliente**). Use essa coluna para exibir rapidamente a versão do cliente do Configuration Manager em cada imagem de inicialização.    



##  <a name="BKMK_BootImageCustom"></a> Personalizar uma imagem de inicialização  

Quando uma imagem de inicialização é baseada na versão do WinPE da versão do Windows ADK compatível, você pode personalizar ou [modificar uma imagem de inicialização](#BKMK_ModifyBootImages) no console. Quando você atualiza um site e instala uma nova versão do Windows ADK, as imagens de inicialização personalizadas não são atualizadas com a nova versão do Windows ADK. Quando isso acontece, não é possível personalizar as imagens de inicialização no console do Configuration Manager. No entanto, elas continuam funcionando como antes da atualização.  

Quando uma imagem de inicialização é baseada em uma versão diferente do Windows ADK instalada em um site, é necessário personalizar as imagens de inicialização. Use outro método para personalizar essas imagens de inicialização, como usar a ferramenta de linha de comando DISM (Gerenciamento e Manutenção de Imagens de Implantação). O DISM faz parte do Windows ADK. Para obter mais informações, consulte [Customize boot images (Personalizar imagens de inicialização)](customize-boot-images.md).  



##  <a name="BKMK_AddBootImages"></a> Adicionar uma imagem de inicialização  

Durante a instalação do site, o Configuration Manager adiciona automaticamente imagens de inicialização baseadas em uma versão do WinPE da versão do Windows ADK com suporte. Dependendo da versão do Configuration Manager, você pode adicionar imagens de inicialização baseadas em uma versão do WinPE diferente da versão com suporte do Windows ADK. Ocorre um erro quando você tenta adicionar uma imagem de inicialização que contém uma versão do WinPE não compatível. A seguinte lista contém as versões do Windows ADK e WinPE atualmente compatíveis: 


|  |  |
|---------|---------|
| Versão do Windows ADK | Windows ADK para Windows 10 |
| Versões do Windows PE para imagens de inicialização personalizáveis no console do Configuration Manager | Windows PE 10 |
| Versões do Windows PE com suporte para imagens de inicialização *não personalizáveis* no console do Configuration Manager | - Windows PE 3.1<sup>[Observação 1](#bkmk_note1)</sup> <br> - Windows PE 5 |

Por exemplo, use o console do Configuration Manager para personalizar imagens de inicialização baseadas no Windows PE 10 no Windows ADK para Windows 10. Para uma imagem de inicialização baseada no Windows PE 5, personalize-a em outro computador usando a versão do DISM no Windows ADK para Windows 8. Em seguida, adicione a imagem de inicialização personalizada ao console do Configuration Manager. Para obter mais informações, consulte os seguintes artigos:
- [Personalizar imagens de inicialização](/sccm/osd/get-started/customize-boot-images)
- [Suporte para Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk)
- [Plataformas com suporte DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms)

#### <a name="bkmk_note1"></a> Observação 1: suporte para Windows PE 3.1

Adicione uma imagem de inicialização ao Configuration Manager somente com base no Windows PE *versão 3.1*. Atualize o Windows AIK para Windows 7 (baseado no Windows PE 3.0) com o Suplemento Windows AIK para Windows 7 SP1 (baseado no Windows PE 3.1). Baixe o Suplemento Windows AIK para Windows 7 SP1 no [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  


#### <a name="process-to-add-a-boot-image"></a>Adicionar uma imagem de inicialização  

1. No console do Configuration Manager, acesse o espaço de trabalho **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione o nó **Imagens de Inicialização**.  

2. Na guia **Início** da faixa de opções, no grupo **Criar**, selecione **Adicionar Imagem de Inicialização**. Essa ação inicia o Assistente para Adicionar Imagem de Inicialização.  

3. Na página **Fonte de Dados**, especifique as seguintes opções:  

    - Na caixa **Caminho** , especifique o caminho para o arquivo WIM de imagem de inicialização. O caminho especificado deve ser um caminho de rede válido no formato UNC. Por exemplo: `\\ServerName\ShareName\BootImageName.wim`

    - Selecione a imagem de inicialização na lista suspensa **Imagem de Inicialização** . Se o arquivo WIM contiver várias imagens de inicialização, selecione a imagem adequada.  

4. Na página **Geral**, especifique as opções a seguir:  

    - Na caixa **Nome** , especifique um nome exclusivo para a imagem de inicialização.  

    - Na caixa **Versão** , especifique um número de versão para a imagem de inicialização.  

    - Na caixa **Comentário**, faça uma breve descrição de como a imagem de inicialização é usada.  

5. Conclua o assistente.  

A imagem de inicialização agora estará listada no nó **Imagem de Inicialização**. Antes de usar a imagem de inicialização para implantar um SO, distribua-a para os pontos de distribuição. 

> [!Tip]  
> No nó **Imagem de Inicialização** do console, a coluna **Tamanho (KB)** exibe o tamanho descompactado de cada imagem de inicialização. Quando o site envia uma imagem de inicialização pela rede, ele envia uma cópia compactada. Normalmente, essa cópia é menor que o tamanho listado na coluna **Tamanho (KB)** .  



##  <a name="BKMK_DistributeBootImages"></a> Distribuir imagens de inicialização  

As imagens de inicialização são distribuídas para os pontos de distribuição da mesma forma que outros conteúdos são distribuídos. Antes de implantar um SO ou criar mídia, distribua a imagem de inicialização para pelo menos um ponto de distribuição.   

Para saber mais sobre como distribuir uma imagem de inicialização, confira [Distribuir Conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  

Para usar o PXE para implantar um SO, considere os seguintes pontos antes de distribuir a imagem de inicialização:  
- Configure o ponto de distribuição para aceitar solicitações PXE.  
- Distribua imagens de inicialização x86 e x64 habilitadas para PXE para, pelo menos, um ponto de distribuição habilitado para PXE.  
- O Configuration Manager distribui as imagens de inicialização para a pasta **RemoteInstall** no ponto de distribuição habilitado para PXE.  
  
Para obter mais informações sobre como usar o PXE para implantar sistemas operacionais, consulte [Usar PXE para implantar o Windows na rede](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).  



##  <a name="BKMK_ModifyBootImages"></a> Modificar uma imagem de inicialização  

Adicione ou remova drivers de dispositivo à imagem ou edite as propriedades da imagem de inicialização. Os drivers adicionados ou removidos podem incluir drivers de rede ou armazenamento. Ao modificar imagens de inicialização, considere os seguintes fatores:  

- Antes de adicionar drivers à imagem de inicialização, importe-os e habilite-os no catálogo de drivers de dispositivos.  

- Quando você modifica uma imagem de inicialização, ela não altera os pacotes associados aos quais a imagem de inicialização faz referência.  

- Depois de fazer alterações na imagem de inicialização, **atualize** a imagem de inicialização nos pontos de distribuição que já têm a imagem. Esse processo disponibiliza a versão mais atual da imagem de inicialização aos clientes. Para saber mais, confira [Gerenciar o conteúdo que você distribuiu](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_manage).  


### <a name="process-to-modify-the-properties-of-a-boot-image"></a>Modificar as propriedades de uma imagem de inicialização  

1. No console do Configuration Manager, acesse o espaço de trabalho **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione o nó **Imagens de Inicialização**.  

2. Selecione a imagem de inicialização que deseja modificar.  

3. Na guia **Início** da faixa de opções, no grupo **Propriedades**, selecione **Propriedades**.  

4. Defina qualquer uma das configurações a seguir para alterar o comportamento da imagem de inicialização:  

#### <a name="images"></a>Imagens
Na guia **Imagens**, se você alterar as propriedades da imagem de inicialização usando uma ferramenta externa, clique em **Recarregar**.  

#### <a name="drivers"></a>Drivers
Na guia **Drivers** , adicione os drivers de dispositivo do Windows necessários para inicializar o WinPE. Considere os seguintes pontos ao adicionar drivers de dispositivo:  

- Verifique se os drivers adicionados à imagem de inicialização correspondem à arquitetura da imagem de inicialização.  

- Para exibir apenas os drivers para a arquitetura da imagem de inicialização, selecione **Ocultar drivers que não correspondem à arquitetura da imagem de inicialização**. A arquitetura do driver é baseada na arquitetura relatada no INF do fabricante.  

- O WinPE já vem com muitos drivers. Adicione apenas drivers de rede e armazenamento que não estão incluídos no WinPE.  

- Adicione somente drivers de rede e de armazenamento à imagem de inicialização, a menos que haja requisitos para outros drivers no WinPE.  

- Para exibir somente os drivers de armazenamento e de rede, selecione **Ocultar drivers que não estão em uma classe de armazenamento ou de rede (para imagens de inicialização)** . Essa opção também oculta outros drivers que, geralmente, não são necessários para as imagens de inicialização, como drivers de vídeo ou de modem.  

- Para ocultar os drivers que não têm uma assinatura digital válida, selecione **Ocultar drivers que não são assinados digitalmente**.  

> [!NOTE]  
> Importe os drivers de dispositivo para o catálogo de drivers antes de adicioná-los a uma imagem de inicialização. Para obter informações sobre como importar drivers de dispositivo, consulte [Gerenciar drivers](manage-drivers.md).  

#### <a name="customization"></a>Personalização
Na guia **Personalização** , selecione qualquer uma das seguintes configurações:  

- Selecione a opção **Habilitar Comando Prestart** para especificar um comando a ser executado antes da execução da sequência de tarefas. Ao habilitar essa opção, especifique também a linha de comando a ser usada para execução e os arquivos de suporte necessários para o comando.  

    > [!WARNING]  
    > Adicione **cmd /c** ao início da linha de comando. Se você não especificar **cmd /c**, o comando não será fechado depois de ser executado. A implantação continuará aguardando a conclusão do comando e não iniciará outras ações ou outros comandos configurados.  

    > [!TIP]  
    > Durante a criação da mídia de sequência de tarefas, o assistente grava a ID do pacote e a linha de comando prestart no arquivo de log CreateTSMedia.log. Essas informações incluem o valor de quaisquer variáveis da sequência de tarefas. O log está no computador que executa o console do Configuration Manager. Examine este arquivo de log para verificar os valores das variáveis da sequência de tarefas.  

- Defina as configurações de **Plano de Fundo do Windows PE** para especificar se deseja usar o plano de fundo padrão do WinPE ou um plano de fundo personalizado.  

- Selecione **Habilitar suporte de comandos (teste somente)** para abrir um prompt de comando usando a tecla **F8** enquanto a imagem de inicialização é implantada. Essa opção é útil para solucionar problemas ao testar a implantação. Usar essa configuração em uma implantação de produção não é aconselhável devido a questões de segurança.  

- Configure o espaço transitório do Windows PE, que é o armazenamento temporário (unidade de RAM) usado pelo WinPE. Por exemplo, quando um aplicativo é executado no WinPE e precisa gravar arquivos temporários, o WinPE redireciona os arquivos para o espaço transitório na memória para simular a presença de uma unidade de disco. Por padrão, esse valor é de 512 MB para dispositivos com mais de 1 GB de RAM, caso contrário, o padrão é 32 MB.  

#### <a name="optional-components"></a>Componentes Opcionais
Na guia **Componentes Opcionais**, especifique os componentes que serão adicionados ao Windows PE para uso com o Configuration Manager. Para obter mais informações sobre os componentes opcionais disponíveis, consulte [WinPE: Adicionar pacotes (Referência de Componentes Opcionais)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).  

Os seguintes componentes são exigidos pelo Configuration Manager e sempre adicionados às imagens de inicialização:
- Script (WinPE-Scripting)
- Inicialização (WinPE-SecureStartup)
- Rede (WinPE-WDS-Tools)
- Script (WinPE-WMI)

A lista **Componentes** mostra itens adicionais que são adicionados a esta imagem de inicialização. Para adicionar mais componentes, selecione o asterisco dourado. Para remover um componente, selecione-o na lista e, em seguida, selecione o X vermelho. 

Os seguintes componentes são comumente usados pelos clientes:
- Microsoft .NET (WinPE-NetFX): esse componente é um pré-requisito para o PowerShell. É um dos maiores componentes opcionais.  
- Windows PowerShell (WinPE-PowerShell): este componente requer o .NET e adiciona suporte limitado ao PowerShell. Se você executar scripts personalizados do PowerShell durante a fase do WinPE da sequência de tarefas, adicione esse componente. Há outros componentes que podem ser necessários para outros cmdlets do PowerShell.   
- HTML (WinPE-HTA): se você executar aplicativos HTML personalizados durante a fase do WinPE da sequência de tarefas, adicione esse componente. 

Para saber mais sobre como adicionar idiomas, confira [Configurar vários idiomas](#BKMK_BootImageLanguage). 

#### <a name="data-source"></a>fonte de dados
Na guia **Fonte de Dados** , atualize qualquer uma das seguintes configurações:  

- Para alterar o arquivo de origem da imagem de inicialização, defina o **Caminho da imagem** e o **Índice de imagens**.  

- Para criar um agendamento que indica quando o site atualiza a imagem de inicialização, selecione **Atualizar pontos de distribuição de acordo com um agendamento**.  

- Caso não deseje que o conteúdo desse pacote seja excluído do cache do cliente para liberar espaço para outros tipos de conteúdo, selecione **Persistir conteúdo no cache do cliente**.  

- Para especificar que o site somente distribui arquivos alterados quando ele atualiza o pacote de imagem de inicialização no ponto de distribuição, selecione **Habilitar a BDR** (replicação diferencial binária). Essa configuração minimiza o tráfego de rede entre sites. A BDR é especialmente útil quando o pacote de imagem de inicialização é grande e as alterações são relativamente pequenas.  

- Se você usar a imagem de inicialização em uma implantação habilitada para PXE, selecione **Implantar essa imagem de inicialização por meio do ponto de distribuição habilitado para PXE**. Para obter mais informações, consulte [Usar PXE para implantar o Windows na rede](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).  

#### <a name="data-access"></a>Acesso a Dados
Na guia **Acesso a Dados**, você pode definir as configurações de compartilhamento de pacote. Se necessário em seu ambiente, defina a opção para **Copiar o conteúdo deste pacote para um compartilhamento de pacote nos pontos de distribuição**. Em seguida, você tem a opção adicional para **Usar um nome personalizado para o compartilhamento de pacote** e especificar o **Nome do Compartilhamento** personalizado. O espaço em disco adicional é necessário nos pontos de distribuição quando você habilita esta opção. Ela se aplica a todos os pontos de distribuição que recebem essa imagem de inicialização. 

#### <a name="distribution-settings"></a>Configurações de Distribuição
Na guia **Configurações de Distribuição** , selecione qualquer uma das seguintes configurações:  

- Na lista **Prioridade de distribuição**, especifique o nível de prioridade. O Configuration Manager usa essa lista de prioridades quando o site distribui vários pacotes para o mesmo ponto de distribuição.  

- Caso queira habilitar a distribuição de conteúdo sob demanda para pontos de distribuição preferenciais, selecione **Habilitar para distribuição sob demanda**. Quando você habilita essa configuração, se um cliente solicitar o conteúdo do pacote e o conteúdo não estiver disponível em nenhum ponto de distribuição, o ponto de gerenciamento distribuirá o conteúdo. Para obter mais informações, confira [Distribuição de conteúdo sob demanda](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#on-demand-content-distribution).  

- Para especificar como deseja que o site distribua a imagem de inicialização para os pontos de distribuição habilitados para o conteúdo pré-teste, defina as **Configurações do ponto de distribuição pré-teste**. Para obter mais informações sobre como distribuir conteúdo pré-configurado, consulte [Prestage content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  

#### <a name="content-locations"></a>Locais de Conteúdo
Na guia **Locais de Conteúdo**, selecione o ponto de distribuição ou o grupo de pontos de distribuição e use as seguintes ações:  

- **Validar**: verifique a integridade do pacote de imagem de inicialização no ponto de distribuição ou grupo de pontos de distribuição selecionado.  

- **Redistribuir**: distribua a imagem de inicialização para o ponto de distribuição selecionado ou para o grupo de pontos de distribuição novamente.  

- **Remover**: exclua a imagem de inicialização do ponto de distribuição ou grupo de pontos de distribuição selecionado.  

#### <a name="security"></a>Segurança
Na guia **Segurança**, visualize os usuários administrativos que têm permissões para esse objeto.



## <a name="BKMK_BootImagePXE"></a> Configurar uma imagem de inicialização para o PXE  

Antes que seja possível usar uma imagem de inicialização para uma implantação baseada no PXE, é necessário configurar a imagem de inicialização para ser implantada de um ponto de distribuição habilitado para PXE.  

1. No console do Configuration Manager, acesse o espaço de trabalho **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione o nó **Imagens de Inicialização**.  

2. Selecione a imagem de inicialização que deseja modificar.  

3. Na guia **Início** da faixa de opções, no grupo **Propriedades**, selecione **Propriedades**.  

4. Na guia **Fonte de Dados** , selecione **Implantar esta imagem de inicialização do ponto de distribuição habilitado para PXE**. Para obter mais informações, consulte [Usar PXE para implantar o Windows na rede](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).  



## <a name="BKMK_BootImageLanguage"></a> Configurar vários idiomas

As imagens de inicialização têm neutralidade de idioma. Essa funcionalidade permite que você use uma imagem de inicialização para exibir o texto da sequência de tarefas em vários idiomas enquanto usa o WinPE. Inclua o suporte de idioma apropriado por meio da guia **Componentes Opcionais** da imagem de inicialização. Em seguida, defina a variável de sequência de tarefas apropriada para indicar qual idioma exibir. O idioma do SO implantado não depende do idioma do WinPE. O idioma que o WinPE exibe para o usuário é determinado da seguinte maneira:  

- Quando um usuário executa uma sequência de tarefas de um SO existente, o Configuration Manager utiliza automaticamente o idioma configurado para o usuário. Quando a sequência de tarefas é executada automaticamente como resultado de um prazo de implantação obrigatória, o Configuration Manager utiliza o idioma do SO.  

- Para implantações de SO que usam PXE ou mídia, defina o valor da ID de idioma na variável **SMSTSLanguageFolder** como parte de um comando prestart. Quando o computador inicializar o WinPE, as mensagens serão exibidas no idioma especificado na variável. Se ocorrer um erro ao acessar o arquivo de recurso de idioma na pasta especificada ou se você não definir a variável, o WinPE exibirá as mensagens no idioma padrão.  

    > [!NOTE]  
    > Quando você protege a mídia com uma senha, o texto que solicita uma senha ao usuário será sempre exibido no idioma do WinPE.  

Use o procedimento a seguir para definir o idioma do WinPE para implantações de SO iniciadas por PXE ou mídia.  

#### <a name="process-to-set-the-windows-pe-language-for-a-pxe-or-media-initiated-os-deployment"></a>Definir o idioma do Windows PE para uma implantação de SO iniciada por PXE ou mídia  

1. Antes de atualizar a imagem de inicialização, verifique se o arquivo de recurso de sequência de tarefas apropriado (tsres.dll) está na pasta de idioma correspondente no servidor do site. O arquivo de recursos para o inglês, por exemplo, está no seguinte local: `<ConfigMgrInstallationFolder>\OSD\bin\x64\00000409\tsres.dll`  

2. Como parte do comando prestart, configure a variável de ambiente **SMSTSLanguageFolder** para a ID de idioma apropriada. A ID de idioma deve ser especificada usando o formato decimal e não hexadecimal. Por exemplo, para definir a ID de idioma como inglês, especifique o valor decimal **1033**, não o valor hexadecimal 00000409 do nome da pasta.  
