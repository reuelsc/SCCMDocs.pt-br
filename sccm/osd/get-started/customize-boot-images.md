---
title: "Personalizar imagens de inicialização | Microsoft Docs"
description: "Aprenda várias maneiras de usar o Configuration Manager ou a ferramenta de linha de comando DISM (Gerenciamento e Manutenção de Imagens de Implantação ) para personalizar uma imagem de inicialização."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9cbfc406-d009-446d-8fee-4938de48c919
caps.latest.revision: 15
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: 9312ad976986f97293d294c12161f78e5d6fee1e


---
# <a name="customize-boot-images-with-system-center-configuration-manager"></a>Personalizar imagens de inicialização com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Cada versão do Configuration Manager dá suporte a uma versão específica do Windows ADK (Kit de Avaliação e Implantação do Windows). Você pode manter ou personalizar imagens de inicialização no console do Configuration Manager quando elas se baseiam em uma versão do Windows PE da versão com suporte no Windows ADK. Para personalizar outras imagens de inicialização, será necessário usar outro método, como a ferramenta de linha de comando Gerenciamento e Manutenção de Imagens de Implantação que faz parte do Windows AIK e do Windows ADK.  

 Veja a seguir a versão com suporte do Windows ADK, a versão do Windows PE na qual se baseia a imagem de inicialização que pode ser personalizada no console do Configuration Manager e as versões do Windows PE nas quais se baseia a imagem de inicialização que pode ser personalizada usando o DISM e, em seguida, adicione a imagem ao Configuration Manager.  

-   **Versão do Windows ADK**  

     Windows ADK para Windows 10  

-   **Versões do Windows PE para imagens de inicialização personalizáveis no console do Configuration Manager**  

     Windows PE 10  

-   **Versões do Windows PE com suporte para imagens de inicialização não personalizáveis no console do Configuration Manager**  

     Windows PE 3.1<sup>1</sup> e Windows PE 5  

     <sup>1</sup> Só será possível adicionar uma imagem de inicialização ao Configuration Manager quando ela se basear no Windows PE 3.1. Instale o Suplemento do Windows AIK para Windows 7 SP1 a fim de atualizar o Windows AIK para Windows 7 (baseado no Windows PE 3) com o Suplemento do Windows AIK para Windows 7 SP1 (baseado no Windows PE 3.1). Você pode baixar o Suplemento do Windows AIK para Windows 7 SP1 do [Centro de Download da Microsoft](http://www.microsoft.com/download/details.aspx?id=5188).  

     Por exemplo, quando você tiver o Configuration Manager, será possível personalizar as imagens de inicialização do Windows ADK para Windows 10 (baseado no Windows PE 10) no console do Configuration Manager. No entanto, embora haja suporte para imagens de inicialização baseadas no Windows PE 5, você deverá personalizá-las em outro computador e usar a versão do DISM instalada com o Windows ADK para Windows 8. Em seguida, é possível adicionar a imagem de inicialização ao console do Configuration Manager.  

 Os procedimentos deste tópico demonstram como adicionar os componentes opcionais exigidos pelo Configuration Manager à imagem de inicialização usando os seguintes pacotes do Windows PE:  

-   **WinPE-WMI**: Adiciona o suporte para a WMI (Instrumentação de Gerenciamento do Windows).  

-   **WinPE-Scripting**: Adiciona o suporte para o WSH (Windows Script Host).  

-   **WinPE-WDS-Tools**: Instala as ferramentas dos Serviços de Implantação do Windows.  

 Existem outros pacotes do Windows PE disponíveis para você adicionar. Os recursos a seguir fornecem mais informações sobre os componentes opcionais que você pode adicionar à imagem de inicialização.  

-   Para o Windows PE 5, consulte [WinPE: Adicionar pacotes (Referência de Componentes Opcionais)](https://msdn.microsoft.com/library/windows/hardware/dn938382\(v=vs.85\).aspx)  

-   Para Windows PE 3.1, consulte o tópico [Adicionar um pacote a uma imagem do Windows PE](http://technet.microsoft.com/library/dd799312\(v=WS.10\).aspx) biblioteca de documentação do TechNet do Windows 7.  

> [!NOTE]
>Ao inicializar no WinPE de uma imagem de inicialização personalizada que inclui ferramentas que você adicionou, é possível abrir um prompt de comando do WinPE e digitar o nome do arquivo da ferramenta para executá-la. O local dessas ferramentas é adicionado automaticamente à variável caminho. O prompt de comando somente poderá ser adicionado se a configuração **Habilitar suporte de comandos (somente teste)** for selecionada na guia **Personalização** nas propriedades da imagem de inicialização.

## <a name="customize-a-boot-image-that-uses-windows-pe-5"></a>Personalizar uma imagem de inicialização que usa o Windows PE 5  
 Para personalizar uma imagem de inicialização que usa o Windows PE 5, você deve instalar o Windows ADK e usar a ferramenta de linha de comando DISM para montar a imagem, adicionar componentes e drivers opcionais e confirmar as alterações feitas na imagem. Use o procedimento a seguir para personalizar a imagem de inicialização.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-5"></a>Para personalizar uma imagem de inicialização que usa o Windows PE 5  

1.  Instale o Windows ADK em um computador que não tenha outra versão do Windows AIK ou do Windows ADK, nem nenhum componente do Configuration Manager instalados.  

2.  Baixe o Windows ADK para Windows 8.1 do [Centro de Download da Microsoft](http://www.microsoft.com/download/details.aspx?id=39982)  

3.  Copie a imagem de inicialização (wimpe.wim) da pasta de instalação do Windows ADK (por exemplo, <*Caminho de instalação*>\Windows Kits\\<*versão*>\Assessment and Deployment Kit\Windows Preinstallation Environment\\<*x86 ou amd64*>\\<*localidade*>) em uma pasta de destino no computador em que você deseja personalizar a imagem de inicialização. Esse procedimento usa C:\WinPEWAIK como o nome da pasta de destino.  

4.  Use o DISM para montar a imagem de inicialização em uma pasta local do Windows PE. Por exemplo, digite a seguinte linha de comando:  

     **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

     Onde C:\WinPEWAIK é a pasta que contém a imagem de inicialização e C:\WinPEMount é a pasta montada.  

    > [!NOTE]
    >  Para obter mais informações sobre o DISM, consulte o tópico [DISM - Referência técnica do Gerenciamento e Manutenção de Imagens de Implantação](http://technet.microsoft.com/library/hh824821.aspx) na biblioteca de documentação técnica do TechNet do Windows 8.1 e do Windows 8.

5.  Após montar a imagem de inicialização, use o DISM para adicionar componentes opcionais a ela. No Windows PE 5, os componentes opcionais de 64 bits estão localizados em <*Caminho instalação*>\Kits do Windows\8.1\Kit de Avaliação e Implantação\Ambiente de Pré-Instalação do Windows\amd64\WinPE_OCs.  

    > [!NOTE]
    >  Esse procedimento usa o seguinte local para os componentes opcionais: C:\Arquivos de Programas (x86)\Kits do Windows\8.1\Kit de Avaliação e Implantação\Ambiente de Pré-instalação do Windows\amd64\WinPE_OCs. O caminho usado poderá ser diferente dependendo da versão e das opções de instalação selecionadas para o Windows ADK.  

     Digite o seguinte para instalar os componentes opcionais:  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wmi.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-scripting.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wds-tools.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-SecureStartup.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Arquivos de Programas (x86)\Kits do Windows\8.1\Kit de Avaliação e Implantação\Ambiente de Pré-Instalação do Windows\amd64\WinPE_OCs\\** *<localidade\>* **\WinPE-SecureStartup_** *<localidade\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Arquivos de Programas (x86)\Kits do Windows\8.1\Kit de Avaliação e Implantação\Ambiente de Pré-Instalação do Windows\amd64\WinPE_OCs\\** *<localidade\>* **\WinPE-WMI_** *<localidade\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Arquivos de Programas (x86)\Kits do Windows\8.1\Kit de Avaliação e Implantação\Ambiente de Pré-Instalação do Windows\amd64\WinPE_OCs\\** *<localidade\>* **\WinPE-Scripting** *<localidade\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Arquivos de Programas (x86)\Kits do Windows\8.1\Kit de Avaliação e Implantação\Ambiente de Pré-Instalação do Windows\amd64\WinPE_OCs\\** *<localidade\>* **\WinPE-WDS-Tools_** *<localidade\>* **.cab"**  

     Em que C:\WinPEMount é a pasta montada e localidade é a localidade dos componentes. Por exemplo, para a localidade **en-us** , você digitaria:  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-SecureStartup_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WMI_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-Scripting_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WDS-Tools_en-us.cab"**  

    > [!TIP]
    >  Para obter mais informações sobre os componentes opcionais que você pode adicionar à imagem de inicialização, consulte o tópico [Referência de Componentes Opcionais do Windows PE](http://technet.microsoft.com/library/hh824926.aspx) na biblioteca de documentação do TechNet do Windows 8.1 e do Windows 8.  

6.  Use o DISM para adicionar drivers específicos à imagem de inicialização, quando necessário. Digite o seguinte para adicionar drivers à imagem de inicialização:  

     **dism.exe /image:C:\WinPEMount /add-driver /driver:&lt;** *caminho para o arquivo .inf do driver* **>**  

     Onde C:\WinPEMount é a pasta montada.  

7.  Digite o seguinte para desmontar o arquivo de imagem de inicialização e confirmar as alterações.  

     **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

     Onde C:\WinPEMount é a pasta montada.  

8.  Adicione a imagem de inicialização atualizada ao Configuration Manager a fim de disponibilizá-la para uso nas sequências de tarefas. Use as etapas a seguir para importar a imagem de inicialização atualizada:  

    1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

    2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Imagens de Inicialização**.  

    3.  Na guia **Início** , no grupo **Criar** , clique em **Adicionar Imagem de Inicialização** para o Assistente para Adicionar Imagem de Inicialização.  

    4.  Na página **Fonte de Dados** , especifique as seguintes opções e clique em **Próximo**.  

        -   Na caixa **Caminho** , especifique o caminho para o arquivo de imagem de inicialização atualizado. O caminho especificado deve ser um caminho de rede válido no formato UNC. Por exemplo: **\\\\<***nomedoservidor***>\\<***compartilhamento WinPEWAIK***>\winpe.wim**.  

        -   Selecione a imagem de inicialização na lista suspensa **Imagem de Inicialização** . Se o arquivo WIM contiver várias imagens de inicialização, cada imagem será listada.  

    5.  Na página **Geral** , especifique as seguintes opções e clique em **Próximo**.  

        -   Na caixa **Nome** , especifique um nome exclusivo para a imagem de inicialização.  

        -   Na caixa **Versão** , especifique um número de versão para a imagem de inicialização.  

        -   Na caixa **Comentário** , faça uma breve descrição de como a imagem de inicialização é usada.  

    6.  Conclua o assistente.  

9. Você pode habilitar um shell de comando na imagem de inicialização para fins de depuração e solução de problemas no Windows PE. Use as etapas a seguir para habilitar o shell de comando.  

    1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

    2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Imagens de Inicialização**.  

    3.  Localize a nova imagem de inicialização na lista e identifique a ID do pacote da imagem. Esse ID pode ser encontrado na coluna **ID da Imagem** correspondente à imagem de inicialização.  

    4.  Em um prompt de comando, digite **wbemtest** para abrir o Testador de instrumentação de gerenciamento do Windows.  

    5.  Digite **\\\\<***Computador do Provedor de SMS***>\root\sms\site_<***códigodosite***>** em **Namespace** e clique em **Conectar**.  

    6.  Clique em **Abrir Instância**, digite **sms_bootimagepackage.packageID="<packageID\>"** e clique em **OK**. Para packageID, insira o valor identificado na etapa 3.  

    7.  Clique em **Atualizar Objeto**e, em seguida, clique em **EnableLabShell** no painel **Propriedades** .  

    8.  Clique em **Editar propriedade**, altere o valor para **TRUE**e clique em **Salvar propriedade**.  

    9. Clique em **Salvar objeto**e saia do Testador de instrumentação de gerenciamento do Windows.  

10. Você deve distribuir a imagem de inicialização para pontos de distribuição, grupos de pontos de distribuição ou coleções associadas a grupos de pontos de distribuição antes de usá-la em uma sequência de tarefas. Use as etapas a seguir para distribuir a imagem de inicialização.  

    1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

    2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Imagens de Inicialização**.  

    3.  Clique na imagem de inicialização identificada na etapa 3.  

    4.  Na guia **Início** , no grupo **Implantação** , clique em **Atualizar Pontos de Distribuição**.  

## <a name="customize-a-boot-image-that-uses-windows-pe-31"></a>Personalizar uma imagem de inicialização que usa o Windows PE 3.1  
 Para personalizar uma imagem de inicialização que usa o WinPE 3.1, você deve instalar o Windows AIK, instalar o suplemento do Windows AIK para Windows 7 SP1 e usar a ferramenta de linha de comando DISM para montar a imagem, adicionar os componentes e drivers opcionais e confirmar as alterações na imagem de inicialização. Use o procedimento a seguir para personalizar a imagem de inicialização.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-31"></a>Para personalizar uma imagem de inicialização que usa o Windows PE 3.1  

1.  Instale o Windows AIK em um computador que não tenha outra versão do Windows AIK ou do Windows ADK, nem nenhum componente do Configuration Manager instalados. Baixe o Windows AIK do [Centro de Download da Microsoft](http://www.microsoft.com/download/details.aspx?id=5753).  

2.  Instale o Suplemento do Windows AIK para Windows 7 com SP1 no computador descrito na etapa 1. Baixe o Suplemento do Windows AIK para Windows 7 SP1 do [Centro de Download da Microsoft](http://www.microsoft.com/download/details.aspx?id=5188).  

3.  Copie a imagem de inicialização (wimpe.wim) da pasta de instalação do Windows AIK (por exemplo, <*Caminho de instalação*>\Windows AIK\Tools\PETools\amd64\\) em uma pasta no computador em que você personalizará a imagem de inicialização. Esse procedimento usa C:\WinPEWAIK como o nome da pasta.  

4.  Use o DISM para montar a imagem de inicialização em uma pasta local do Windows PE. Por exemplo, digite a seguinte linha de comando:  

     **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

     Onde C:\WinPEWAIK é a pasta que contém a imagem de inicialização e C:\WinPEMount é a pasta montada.  

    > [!NOTE]
    >  Para obter mais informações sobre o DISM, consulte o tópico [Referência técnica do Gerenciamento e Manutenção de Imagens de Implantação](http://technet.microsoft.com/library/dd744256\(v=ws.10\).aspx) na biblioteca de documentação do TechNet do Windows 7.  

5.  Após montar a imagem de inicialização, use o DISM para adicionar componentes opcionais a ela. No Windows PE 3.1, por exemplo, os componentes opcionais estão localizados em <*Caminho de instalação*>\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\.  

    > [!NOTE]
    >  Esse procedimento usa o seguinte local para os componentes opcionais: C:\Arquivos de Programas\Windows AIK\Tools\PETools\amd64\WinPE_FPs. O caminho que você usará poderá ser diferente dependendo da versão e das opções de instalação selecionadas para o Windows AIK.  

     Digite o seguinte para instalar os componentes opcionais:  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wmi.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-scripting.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wds-tools.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Arquivos de Programas\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<localidade\>* **\winpe-wmi_** *<localidade\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Arquivos de Programas\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<localidade\>* **\winpe-scripting_** *<localidade\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Arquivos de Programas\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<localidade\>* **\winpe-wds-tools_** *<localidade\>* **.cab"**  

     Em que C:\WinPEMount é a pasta montada e localidade é a localidade dos componentes. Por exemplo, para a localidade **en-us** , você digitaria:  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wmi_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-scripting_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wds-tools_en-us.cab"**  

    > [!TIP]
    >  Para obter mais informações sobre os diferentes pacotes que podem ser adicionados à imagem de inicialização, consulte o tópico [Adicionar um pacote a uma imagem do Windows PE](http://technet.microsoft.com/library/dd799312\(v=WS.10\).aspx) na biblioteca de documentação do TechNet do Windows 7.  

6.  Use o DISM para adicionar drivers específicos à imagem de inicialização, quando necessário. Digite o seguinte para adicionar drivers à imagem de inicialização, se necessário:  

     **dism.exe /image:C:\WinPEMount /add-driver /driver:&lt;** *caminho para o arquivo .inf do driver* **>**  

     Onde C:\WinPEMount é a pasta montada.  

7.  Digite o seguinte para desmontar o arquivo de imagem de inicialização e confirmar as alterações.  

     **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

     Onde C:\WinPEMount é a pasta montada.  

8.  Adicione a imagem de inicialização atualizada ao Configuration Manager a fim de disponibilizá-la para uso nas sequências de tarefas. Use as etapas a seguir para importar a imagem de inicialização atualizada:  

    1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

    2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Imagens de Inicialização**.  

    3.  Na guia **Início** , no grupo **Criar** , clique em **Adicionar Imagem de Inicialização** para o Assistente para Adicionar Imagem de Inicialização.  

    4.  Na página **Fonte de Dados** , especifique as seguintes opções e clique em **Próximo**.  

        -   Na caixa **Caminho** , especifique o caminho para o arquivo de imagem de inicialização atualizado. O caminho especificado deve ser um caminho de rede válido no formato UNC. Por exemplo: **\\\\<***nomedoservidor***>\\<***compartilhamento WinPEWAIK***>\winpe.wim**.  

        -   Selecione a imagem de inicialização na lista suspensa **Imagem de Inicialização** . Se o arquivo WIM contiver várias imagens de inicialização, cada imagem será listada.  

    5.  Na página **Geral** , especifique as seguintes opções e clique em **Próximo**.  

        -   Na caixa **Nome** , especifique um nome exclusivo para a imagem de inicialização.  

        -   Na caixa **Versão** , especifique um número de versão para a imagem de inicialização.  

        -   Na caixa **Comentário** , faça uma breve descrição de como a imagem de inicialização é usada.  

    6.  Conclua o assistente.  

9. Você pode habilitar um shell de comando na imagem de inicialização para fins de depuração e solução de problemas no Windows PE. Use as etapas a seguir para habilitar o shell de comando.  

    1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

    2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Imagens de Inicialização**.  

    3.  Localize a nova imagem de inicialização na lista e identifique a ID do pacote da imagem. Esse ID pode ser encontrado na coluna **ID da Imagem** correspondente à imagem de inicialização.  

    4.  Em um prompt de comando, digite **wbemtest** para abrir o Testador de instrumentação de gerenciamento do Windows.  

    5.  Digite **\\\\<***Computador do Provedor de SMS***>\root\sms\site_<***códigodosite***>** em **Namespace** e clique em **Conectar**.  

    6.  Clique em **Abrir Instância**, digite **sms_bootimagepackage.packageID="<packageID\>"** e clique em **OK**. Para packageID, insira o valor identificado na etapa 3.  

    7.  Clique em **Atualizar Objeto**e, em seguida, clique em **EnableLabShell** no painel **Propriedades** .  

    8.  Clique em **Editar propriedade**, altere o valor para **TRUE**e clique em **Salvar propriedade**.  

    9. Clique em **Salvar objeto**e saia do Testador de instrumentação de gerenciamento do Windows.  

10. Você deve distribuir a imagem de inicialização para pontos de distribuição, grupos de pontos de distribuição ou coleções associadas a grupos de pontos de distribuição antes de usá-la em uma sequência de tarefas. Use as etapas a seguir para distribuir a imagem de inicialização.  

    1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

    2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Imagens de Inicialização**.  

    3.  Clique na imagem de inicialização identificada na etapa 3.  

    4.  Na guia **Início** , no grupo **Implantação** , clique em **Atualizar Pontos de Distribuição**.  



<!--HONumber=Dec16_HO3-->


