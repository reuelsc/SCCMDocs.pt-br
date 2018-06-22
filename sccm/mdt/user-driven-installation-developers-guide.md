---
title: Instalação controlada pelo usuário
titleSuffix: Microsoft Deployment Toolkit
description: 'Guia para desenvolvedores para a instalação controlada pelo usuário do Microsoft Deployment Toolkit 2013. '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: a2b3a3a0-7b81-4191-b1f9-c618e59347c3
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 434178f100c32a4188ecf5283066f9332035f761
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2018
ms.locfileid: "27821080"
---
# <a name="user-driven-installation---developers-guide"></a>Instalação controlada pelo usuário – Guia para desenvolvedores
A UDI (Instalação controlada pelo usuário) ajuda a simplificar a implantação dos sistemas operacionais cliente do Windows®, como o Windows 8.1, em computadores que usam o recurso OSD (implantação de sistema operacional) no in Microsoft® System Center 2012 R2 Configuration Manager. A UDI faz parte do MDT (Microsoft Deployment Toolkit).  

## <a name="introduction"></a>Introdução  
 Normalmente, ao implantar sistemas operacionais que usam o recurso OSD, é necessário fornecer todas as informações necessárias para implantar o sistema operacional. As informações são configuradas nos arquivos de configuração ou em bancos de dados (como o arquivo CustomSettings.ini ou o DB MDT [banco de dados do MDT]). É necessário fornecer todas as configurações antes de iniciar a implantação.  

 A UDI oferece uma interface orientada por assistente que permite que você forneça informações de configuração imediatamente antes de executar a implantação. Esse comportamento permite criar sequências de tarefas OSD genéricas e, em seguida, fornecer informações específicas do computador no momento da implantação, que oferece maior flexibilidade no processo de implantação.  

### <a name="target-audience"></a>Público-alvo  
 Este guia foi escrito para desenvolvedores que criam páginas de assistente personalizadas para o Assistente de UDI e editores de página de assistente personalizadas para o Designer do Assistente de UDI. Este guia pressupõe que você já conheça o desenvolvimento de aplicativos do Windows usando:  

-   A C++, usada para criar páginas de assistente personalizadas  

-   O Microsoft .NET Framework, usado para criar editores de página de assistente personalizadas  

-   O WPF (Windows Presentation Foundation), usado para criar editores de página de assistente personalizadas  

-   Linguagens compatíveis com o WPF, como a C# ou a C++, ou o Microsoft Visual Basic® .NET, usadas para criar editores de página de assistente personalizadas  

### <a name="about-this-guide"></a>Sobre este guia  
 Este guia fornece as informações de referência necessárias para ajudar você a personalizar a UTI para sua organização. Este guia não discute tópicos administrativos ou operacionais, como a instalação do MDT (que inclui a UDI), configuração da UDI para implantar sistemas operacionais e aplicativos ou a realização de implantações usando o Assistente de UDI. Para obter mais informações sobre esses tópicos, consulte os tópicos de UDI *Usando o Microsoft Deployment Toolkit*, incluído com o MDT.  

## <a name="udi-development-overview"></a>Visão geral do desenvolvimento da UDI  
 O desenvolvimento da UDI permite que você expanda os recursos oferecidos pela UDI. Normalmente, o desenvolvimento da UDI é necessário quando você deseja coletar informações adicionais que o processo de implantação da UDI consome. Geralmente, essas informações adicionais são salvas como variáveis de sequência de tarefas que as etapas de sequência em uma sequência de tarefas da UDI no Configuration Manager leem.  

### <a name="udi-architecture"></a>Arquitetura da UDI  
 A meta de alto nível do desenvolvimento da UDI é criar páginas de assistente personalizadas que podem ser exibidas no Assistente de UDI. Ao criar páginas de assistente personalizadas, é possível expandir os recursos de UDI existentes para atender aos requisitos técnicos e comerciais da sua organização. Uma página de assistente personalizada coleta informações além das páginas de assistente oferecidas pela UDI ou no lugar delas.  

 A Figura 1 ilustra a relação entre o Designer de Assistente de UDI e o Assistente de UDI.  

 ![UDIDevelopersGuide1](media/UDIDevelopersGuide1.jpg "UDIDevelopersGuide1")  
Figura 1. Relação entre o Assistente de UDI e o Designer do Assistente de UDI  

 **Figura 1. Relação entre o Assistente de UDI e o Designer do Assistente de UDI**  

 Em um nível conceitual, o desenvolvimento da UDI inclui a criação de:  

-   **Páginas de assistente personalizadas**. As páginas de assistente são exibidas no Assistente de UDI e coletam as informações necessárias para concluir o processo de implantação. Crie páginas de assistente usando a C++ no Microsoft Visual Studio®. As páginas de assistente personalizadas são implementadas como DLLs que o Assistente de UDI lê. O SDK (Software Development Kit) da UDI inclui um exemplo de como criar páginas de assistente personalizadas.  

-   **Editores de páginas de assistente personalizadas**. Os editores de página de assistente são usados para configurar o comportamento de sua página de assistente personalizada. Os editores de página de assistente personalizada são implementados como DLLs que o Designer do Assistente de UDI lê. Os editores de página de assistente são criados usando:  

    -   [WPF](http://msdn.microsoft.com/library/ms754130.aspx) versão 4.0  

    -   [Microsoft Prism](http://compositewpf.codeplex.com/) versão 4.0  

    -   [Microsoft Unity Application Block](http://unity.codeplex.com/) (Unity) versão 2.1  

     O MDT inclui todos os assemblies necessários para criar um editor de página de assistente personalizada para uso no Designer do Assistente de UDI. O SDK da UDI inclui um exemplo de como criar editores de página de assistente personalizada.  

 Além disso, o Designer do Assistente de UDI consome arquivos de configuração do editor de página de assistente compatíveis. Crie os arquivos de configuração do editor de página de assistente como uma parte do processo para criação de suas páginas de assistente personalizadas e editores de página de assistente personalizada. O Designer do Assistente de UDI cria as informações XML necessárias no arquivo de configuração do Assistente de UDI e no arquivo .app correspondente.  

### <a name="preparing-the-udi-development-environment"></a>Preparando o Ambiente de desenvolvimento de UDI  
 Antes de começar a criar suas próprias páginas de assistente personalizado e editores de página de assistente, siga estas etapas para preparar o ambiente de desenvolvimento UDI:  

1.  Prepare os pré-requisitos do ambiente de desenvolvimento de UDI, conforme descrito em [Preparar os pré-requisitos do ambiente de desenvolvimento de UDI](#PrepareUDIDevelopmentEnvironmentPrerequisites).  

2.  Configure o ambiente de desenvolvimento de UDI conforme descrito em [Configurar o ambiente de desenvolvimento de UDI](#ConfigureUDIDevelopmentEnvironment).  

3.  Verifique se o ambiente de desenvolvimento de UDI foi configurado corretamente conforme descrito em [Verificar o ambiente de desenvolvimento de UDI](#VerifyUDIDeploymentEnvironment).  

####  <a name="PrepareUDIDevelopmentEnvironmentPrerequisites"></a> Preparar os pré-requisitos do ambiente de desenvolvimento de UDI  
 Para preparar os pré-requisitos do ambiente de desenvolvimento de UDI, siga estas etapas:  

1.  Prepare os pré-requisitos de hardware do ambiente de desenvolvimento de UDI conforme descrito em [Preparar os pré-requisitos de hardware do ambiente de desenvolvimento de UDI](#PrepareUDIDevelopmentEnvironmentHardwarePrerequisites).  

2.  Prepare os pré-requisitos de software do ambiente de desenvolvimento de UDI conforme descrito em [Preparar os pré-requisitos de software do ambiente de desenvolvimento de UDI](#PrepareUDIDevelopmentEnvironmentSoftwarePrerequisites).  

#####  <a name="PrepareUDIDevelopmentEnvironmentHardwarePrerequisites"></a> Preparar os pré-requisitos de hardware do ambiente de desenvolvimento de UDI  
 Os pré-requisitos de hardware do ambiente de desenvolvimento de UDI são os mesmos pré-requisitos de hardware da edição do Microsoft Visual Studio 2010 que você está usando. Para obter mais informações sobre esses requisitos, consulte os requisitos do sistema para cada edição em [Produtos do Visual Studio 2010](http://www.microsoft.com/visualstudio/products/2010-editions).  

#####  <a name="PrepareUDIDevelopmentEnvironmentSoftwarePrerequisites"></a> Preparar os pré-requisitos de software do ambiente de desenvolvimento de UDI  
 O ambiente de desenvolvimento de UDI tem os seguintes pré-requisitos de software:  

-   Qualquer sistema operacional Windows compatível com o Visual Studio 2010 (recomenda-se o Windows 7 ou o Windows Server® 2008 R2).  

     Será necessário um sistema operacional Windows compatível com a arquitetura do processador para o qual você deseja desenvolver. É possível realizar o desenvolvimento de UDI de 32 bits e de 64 bits usando um sistema operacional de 64 bits. Faça só um desenvolvimento de UDI de 32 bits em sistemas operacionais de 32 bits. Por esse motivo, você deverá usar um sistema operacional de 64 bits.  

    > [!NOTE]
    >  Não há suporte para versões IntelItanium (IA-64) de sistemas operacionais Windows para ambientes de desenvolvimento de UDI.  

     Para obter mais informações sobre os sistemas operacionais compatíveis com o Visual Studio 2010, consulte os requisitos do sistema para cada edição em [Produtos do Visual Studio 2010](http://www.microsoft.com/visualstudio/products/2010-editions).  

-   Microsoft .NET Framework versão 4.0 (exigido pelo Visual Studio 2010)  

-   Linguagem C++ (a linguagem usada na expansão das páginas do Assistente de UDI)  

-   Outras linguagens compatíveis com o WPF, como a C#, Visual Basic .NET ou C++/ Common Language Infrastructure, usadas para expandir os editores de página do assistente de Designer de UDI  

    > [!NOTE]
    >  O código-fonte de exemplo para os editores de página de assistente do Designer do Assistente de UDI é escrito em C#. Instala a linguagem C# se desejar usar o código-fonte de exemplo.  

####  <a name="ConfigureUDIDevelopmentEnvironment"></a> Configurar o Ambiente de desenvolvimento de UDI  
 Depois que os pré-requisitos do ambiente de desenvolvimento de UDI forem atendidos, siga estas etapas para configurar o ambiente de desenvolvimento de UDI:  

1.  Instale o Visual Studio 2010.  

     Certifique-se de instalar a linguagem C++ e qualquer outra linguagem compatível com o WPF.  

    > [!NOTE]
    >  O código-fonte de exemplo para as páginas do editor do Designer do Assistente de UDI é escrito em C#. Instala a linguagem C# se desejar usar o código-fonte de exemplo.  

     Para obter mais informações sobre a instalação do Visual Studio 2010, consulte [Instalando o Visual Studio](http://msdn.microsoft.com/library/e2h7fzkw.aspx).  

2.  Instale o MDT.  

     Para obter mais informações sobre como instalar o MDT, consulte a seção "Instalando ou atualizando para o MDT", no documento do MDT *Usando o Microsoft Deployment Toolkit*.  

3.  No Windows Explorer, crie *pasta_local* (em que *pasta_local* é qualquer pasta localizada em uma unidade local no computador de desenvolvimento).  

4.  Copie a pasta *pasta_de_instalação*\SDK para *pasta_local* (em que *pasta_de_instalação* é a pasta na qual você instalou o MDT, e *pasta_local* é qualquer pasta localizada em uma unidade local no computador de desenvolvimento).  

     Copie a pasta do SDK para outro local, porque o MDT está instalado na pasta Arquivos de Programas, que não pode ser gravada sem permissões elevadas. Copiar a pasta do SDK para outro local permite modificar os arquivos na pasta do SDK sem exigir permissões elevadas.  

5.  Copie a pasta *pasta_de_instalação*\Templates\Distribution\Tools para *pasta_local* (em que *pasta_de_instalação* é a pasta na qual você instalou o MDT e *pasta_local* é a pasta que você criou anteriormente no processo).  

6.  Renomeie a pasta *local_folder*\Tools para *local_folder*\OSDSetupWizard (em que *local_folder* é a pasta que você criou anteriormente no processo).  

     Quando concluído, a estrutura de pastas sob *local_folder* deverá ter a aparência da estrutura de pastas ilustrada na Figura 2 (em que *local_folder* é a pasta que você criou anteriormente no processo e é mostrada como *UDIDevelopment* na figura).  

     ![UDIDevelopersGuide2](media/UDIDevelopersGuide2.jpg "UDIDevelopersGuide2")  
Figura 2. Estrutura de pastas para o desenvolvimento da UDI  

     **Figura 2. Estrutura de pastas para o desenvolvimento da UDI**  

####  <a name="VerifyUDIDeploymentEnvironment"></a> Verificar o Ambiente de desenvolvimento de UDI  
 Quando o ambiente de desenvolvimento de UDI estiver configurado, verifique se o ambiente de desenvolvimento de UDI foi configurado corretamente garantindo que os projetos de exemplo foram criados corretamente no Visual Studio 2010.  

 Verifique se o ambiente de desenvolvimento de UDI foi configurado corretamente, determinando se:  

-   O projeto SamplePage foi criado corretamente, conforme descrito em [Verificar se o projeto SamplePage foi criado corretamente](#VerifySamplePageProjectBuildsCorrectly)  

-   O projeto SampleEditor foi criado corretamente, conforme descrito em [Verificar se o projeto SampleEditor foi criado corretamente](#VerifySampleEditorProjectBuildsCorrectly)  

#####  <a name="VerifySamplePageProjectBuildsCorrectly"></a> Verifique se o projeto SamplePage foi criado corretamente  
 O projeto SamplePage oferece um exemplo de como criar uma página de assistente personalizada para o Assistente de UDI. Para obter mais informações sobre o projeto SamplePage, consulte [Examinar a Solução do Visual Studio do SamplePage](#ReviewSamplePageVisualStudioSolution).  

 **Para verificar se o projeto SamplePage foi criado corretamente**  

1.  Inicie o Visual Studio 2010.  

2.  Abra o projeto SamplePage.  

     O projeto SamplePage reside na pasta *local_folder*\SDK\UDI\SamplePage (em que *local_folder* é a pasta que você criou anteriormente no processo).  

3.  No Visual Studio 2010, no Gerenciador de Soluções, clique com o botão direito do mouse no projeto SamplePage e, em seguida, clique em **Propriedades**.  

     A caixa de diálogo **Páginas de propriedades do SamplePage** é exibida.  

4.  Na caixa de diálogo **Páginas de propriedade do SamplePage**, acesse Propriedades da configuração/Depuração.  

5.  Nas propriedades de Depuração, em **Configuração**, selecione **Todas as configurações**.  

6.  Nas propriedades de Depuração, em **Comando**, digite **$(TargetDir)\OSDSetupWizard.exe.**  

7.  Nas propriedades de Depuração, em **Diretório de Trabalho**, digite **$(TargetDir)**.  

8.  Na caixa de diálogo **Páginas de propriedades do SamplePage**, acesse Propriedades da configuração/Eventos de build/Evento pós-build.  

9. Nas propriedades do Evento pós-build, em **Linha de comando**, digite o seguinte:  

    ```  
    copy /y "$(ProjectDir)..\..\..\..\OSDSetupWizard\x86\*.*" "$(TargetDir)"  
    xcopy /y /i "$(ProjectDir)..\..\..\..\OSDSetupWizard\x86\en-us" "$(TargetDir)en-us"  
    copy /y "$(ProjectDir)..\..\..\..\OSDSetupWizard\OSDResults\Images\UDI_Wizard_Banner.bmp" "$(ProjectDir)header.bmp"  
    copy /y "$(ProjectDir)Config.xml" "$(TargetDir)”  
    copy /y "$(ProjectDir)header.bmp" "$(TargetDir)header.bmp"  
    ```  

10. Na caixa de diálogo **Páginas de propriedades do SamplePage**, clique em **OK**.  

11. Salve o projeto.  

12. No menu **Depurar**, clique em **iniciar depuração**.  

     A caixa de diálogo **Microsoft Visual Studio** é exibida indicando que a origem está desatualizada e pergunta se você deseja criar o projeto.  

13. Na caixa de diálogo **Microsoft Visual Studio**, clique em **Sim**.  

     A caixa de diálogo **Nenhuma informação de depuração** é exibida informando que nenhuma informação de depuração está disponível para OSDSetupWizard.exe.  

14. Na caixa de diálogo **Nenhuma informação de depuração**, clique em **Sim**.  

     O Assistente de UDI é aberto com a página de assistente personalizada exibida.  

15. Verifique se é possível selecionar um valor em **Escolha seu local**.  

16. No formulário **Assistente com página de exemplo**, clique em **Cancelar**.  

     A caixa de diálogo **Cancelar assistente** é exibida.  

17. Na caixa de diálogo **Cancelar assistente**, clique em **Sim**.  

18. Feche o Visual Studio 2010.  

#####  <a name="VerifySampleEditorProjectBuildsCorrectly"></a> Verifique se o projeto SampleEditor foi criado corretamente  
 O projeto SampleEditor oferece um exemplo de como criar um editor de página de assistente personalizada para o Designer do Assistente de UDI. Para obter mais informações sobre o projeto SampleEditor, consulte [Examinar a Solução do Visual Studio do SamplePage](#ReviewSamplePageVisualStudioSolution).  

 **Para verificar se o projeto SampleEditor foi criado corretamente**  

1.  Inicie o Visual Studio 2010.  

2.  Abra o projeto SampleEditor.  

     O projeto SampleEditor reside na pasta *pasta_local*\SDK\UDI\SampleEditor (em que *pasta_local* é a pasta que você criou anteriormente no processo).  

3.  No Visual Studio 2010, no Gerenciador de Soluções, selecione o projeto SampleEditor.  

4.  No menu **Projeto**, clique em **Adicionar referência**.  

     A caixa de diálogo **Adicionar referência** é aberta.  

5.  Na caixa de diálogo **Adicionar referência**, clique na guia **Procurar**.  

6.  Na guia **Procurar**, acesse *pasta_de_instalação*\Bin (em que *pasta_de_instalação* é a pasta na qual você instalou o MDT). Selecione os arquivos a seguir e, em seguida, clique em **OK**:  

    -   Microsoft.Enterprise.UDIDesigner.Common.dll  

    -   Microsoft.Enterprise.UDIDesigner.DataService.dll  

    -   Microsoft.Enterprise.UDIDesigner.Infrastructure.dll  

    -   Microsoft.Practices.Prism.dll  

    -   Microsoft.Practices.ServiceLocation.dll  

    -   Microsoft.Practices.Unity.dll  

    -   RibbonControlsLibrary.dll  

    > [!NOTE]
    >  É possível selecionar vários arquivos na guia **Procurar** mantendo pressionada a tecla CTRL enquanto clica nos arquivos.  

7.  No Gerenciador de Soluções, acesse SampleEditor/Referências.  

8.  Verifique se nenhuma referência tem avisos ou erros.  

9. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto SampleEditor e, em seguida, clique em **Propriedades**.  

     A caixa de diálogo **Páginas de propriedades do SampleEditor** é exibida.  

10. Na caixa de diálogo **Páginas de propriedades do SampleEditor**, clique na guia **Depurar**.  

11. Na guia **Depurar**, clique em **Iniciar programa externo**.  

12. Em **Iniciar programa externo**, digite ***pasta_de_instalação\Bin\UDIDesigner.exe*** (em que *pasta_de_instalação* é a pasta na qual você instalou o MDT) e, em seguida, clique em **OK**.  

    > [!TIP]
    >  É possível clicar no botão de reticências (...) para navegar até a pasta e selecionar UDIDesigner.exe.  

13. No menu **Arquivo**, clique em **Salvar tudo**.  

14. Copie o arquivo *pasta_local*\SDK\SamplePage\SamplePage.dll.config para *pasta_de_instalação*\Bin\Config (em que *pasta_local* é a pasta que você criou no computador de desenvolvimento anteriormente no processo de configuração e *pasta_de_instalação* é a pasta na qual você instalou o MDT).  

15. No Visual Studio 2010, no menu **Depurar**, clique em **Iniciar depuração**.  

     O Designer do Assistente de UDI é iniciado.  

16. No Designer do Assistente de UDI, na Faixa de Opções, clique em **Abrir**.  

     A caixa de diálogo **Abrir** é exibida.  

17. Na caixa de diálogo **Abrir**, abra o arquivo *pasta_local*\SDK\SamplePage\SamplePage\Config.xml (em que *pasta_local* é a pasta que você criou no computador de desenvolvimento anteriormente no processo de configuração).  

     O arquivo Config.xml é aberto, e [StageGroup](#StageGroup) personalizado é exibido no painel de detalhes.  

18. No painel de detalhes, clique na guia **Configurar**.  

19. Examine as informações de configuração da caixa **Local**, incluindo o seguinte:  

    -   Botão **Desbloqueado**, com o qual você habilita ou desabilita a caixa **Local**  

    -   Caixa **Valor padrão**, na qual você insere um valor padrão a ser exibido na caixa **Local**  

    -   **Nome de exibição amigável visível na página de resumo**, na qual você insere a legenda para as informações exibidas na página **Resumo**  

    -   Caixa de listagem **Local**, que inclui uma lista de possíveis locais  

20. Feche o Designer do Assistente de UDI.  

21. Feche o Visual Studio 2010.  

## <a name="reviewing-the-udi-sdk-examples"></a>Examinando os exemplos de SDK da UDI  
 Antes de começar o desenvolvimento, examine os exemplos fornecidos no SDK da UDI. Use as informações neste guia e o código-fonte nos exemplos para ajudá-lo a criar suas próprias páginas de assistente personalizadas e os editores de página de UDI personalizada.  

 Percorra os exemplos de SDK da UDI examinando o:  

-   Conteúdo da pasta do SDK que você copiou anteriormente no processo de instalação, conforme descrito em [Examinar o conteúdo da pasta SDK](#ReviewContentsofSDKFolder)  

-   Exemplo de página de assistente de UDI personalizada, conforme descrito em [Examinar a Solução do Visual Studio de SamplePage](#ReviewSamplePageVisualStudioSolution)  

-   Exemplo de editor de página de assistente de UDI personalizada, conforme descrito em [Examinar a Solução do Visual Studio de SampleEditor](#ReviewSampleEditorVisualStudioSolution)  

###  <a name="ReviewContentsofSDKFolder"></a> Examinar o conteúdo da pasta do SDK  
 Durante a configuração do ambiente de desenvolvimento de UDI, você copiou a pasta do SDK da pasta na qual você instalou o MDT para outra pasta que você criou. A Tabela 1 lista as pastas imediatamente embaixo da pasta do SDK e oferece uma breve descrição de cada uma.  

### <a name="table-1-folders-in-the-udi-sdk"></a>Tabela 1. Pastas no SDK da UDI  

|**Pasta**|**Esta pasta contém**|  
|-|-|  
|Inclui|Arquivos de cabeçalho da C++ necessários para criar páginas de assistente personalizadas para o Assistente de UDI|  
|Bibliotecas|Arquivos de biblioteca C++ que serão vinculados à sua página personalizada; há versões de 32 bits e de 64 bits das bibliotecas de vínculo estático. **Observação:** as versões do Itanium das bibliotecas (IA-64) não estão disponíveis.|  
|SampleEditor|Um projeto do Visual Studio para criar um editor personalizado usado para editar a página do SamplePage no Designer do Assistente de UDI, escrito em C#|  
|SamplePage|Um projeto do Visual Studio para criar uma página de assistente de UDI personalizada, escrita em Visual C++|  

###  <a name="ReviewSamplePageVisualStudioSolution"></a> Examinar a Solução do Visual Studio do SamplePage  
 Antes de começar a criar suas páginas de assistente personalizado e editores de página de assistente, siga estas tarefas para preparar o ambiente de desenvolvimento UDI:  

-   Examine os estágios do ciclo de vida de uma página de assistente de UDI, conforme descrito em [Examinar o ciclo de vida da página de assistente](#ReviewWizardPageLifeCycle).  

-   Examine a solução do Visual Studio para o exemplo de SamplePage no SDK da UDI, conforme descrito em [Examinar o exemplo de SamplePage](#ReviewSamplePageExample).  

####  <a name="ReviewWizardPageLifeCycle"></a> Examinar o ciclo de vida da página de assistente  
 Uma página de assistente de UDI tem métodos que correspondem a cada estágio (ou fase) do ciclo de vida da página. Como parte da criação de sua página de assistente personalizada, é necessário substituir esses métodos pelo seu código. A tabela 2 lista os métodos que você precisará substituir e oferece uma breve descrição de cada um, incluindo quando usar o método no ciclo de vida da página de assistente.  

### <a name="table-2-methods-in-a-wizard-page-life-cycle"></a>Tabela 2. Métodos em um ciclo de vida da página de assistente  

|**Método**|**Descrição**|  
|-|-|  
|**OnWindowCreated**|Este método é chamado uma vez, após a criação da janela da página.<br /><br /> Para esse método, escreva o código que inicializa a página pela primeira vez e só precisa ser executada uma vez. Por exemplo, use esse método para inicializar campos ou para ler informações de configuração de elementos **Setter** no arquivo de configuração do Assistente de UDI.|  
|**OnWindowShown**|Esse método é chamado cada vez que a página é exibida (mostrada) no Assistente de UDI. Ele é chamado na primeira vez em que a página é exibida e cada vez que você navega até a página clicando em **Próximo** ou **Voltar** no assistente.<br /><br /> Para esse método, escreva um código que prepara a página para ser exibida – por exemplo, ler variáveis de memória, variáveis de sequência de tarefas ou variáveis de ambiente e, em seguida, atualizar a página com base em quaisquer alterações nessas variáveis.|  
|**OnCommonControlEvent**|Esse método poderá ser chamado sempre que a página de assistente for exibida e receberá uma mensagem WM_NOTIFY de um filho (normalmente, controles comuns).<br /><br /> Para esse método, escreva um código que manipule WM_NOTIFY com base na mensagem de notificação. Por exemplo, convém responder a eventos de um controle comum, como responder a eventos de um clique ou de dois cliques para um controle **TreeView**.|  
|**OnUnhandledEvent**|Esse método é chamado sempre que uma mensagem de janela sem tratamento ocorre para sua página de assistente. Esse método oferece a oportunidade de interceptar e manipular essas mensagens de janela sem tratamento.<br /><br /> Para esse método, escreva um código que manipule as mensagens de janela pertinentes para sua página de assistente. Normalmente, você não precisará substituir este método.|  
|**OnNextClicked**|Esse método é chamado quando você clica em **Próximo** no assistente.<br /><br /> Para esse método, escreva um código que execute as ações necessárias antes de passar para a próxima página do assistente – por exemplo, executar a validação que pode levar muito tempo. Se a validação falhar, será possível cancelar a solicitação **Próximo** e exibir uma mensagem.|  
|**OnWindowHidden**|Esse método é chamado cada vez que a página for ocultada quando a página de assistente anterior ou a próxima for mostrada.<br /><br /> Para esse método, escreva um código que execute quaisquer ações antes de a página ser ocultada, antes de outra página ser mostrada. Normalmente, você não precisará substituir este método.|  

####  <a name="ReviewSamplePageExample"></a> Examinar o exemplo de SamplePage  
 Examine o exemplo de SamplePage usando a lista a seguir, que representa a sequência de eventos durante o ciclo de vida da página de assistente do exemplo de SamplePage:  

1.  O Assistente de UDI, OSDSetupWizard.exe, lê as informações de configuração do arquivo de configuração do Assistente de UDI no exemplo (o arquivo Config.xml), conforme descrito em [Etapa 1: o Assistente de UDI (OSDSetupWizard.exe) lê o arquivo Config.xml](#UDIWizardReadstheConfigFile).  

2.  O Assistente de UDI carrega as DLLs necessárias para cada página de assistente listada no arquivo de configuração do Assistente de UDI, conforme descrito na [Etapa 2: o Assistente de UDI carrega a DLL para a página de assistente personalizada](#UDIWizardLoadstheDLLforCustomWizardPage).  

3.  O Assistente de UDI exibe a página de assistente personalizada e permite a interação de controles desejada, conforme descrito na [Etapa 3: o Assistente de UDI exibe a página de assistente personalizada](#UDIWizardDisplaysCustomWizardPage).  

4.  Quando a página de assistente personalizada tiver coletado as informações, execute quaisquer tarefas necessárias antes de clicar em **Avançar** para passar para o próximo assistente, conforme descrito na [Etapa 4: o botão Avançar é clicado na página de assistente personalizada](#TheNextButtonisClickedinCustomWizardPage).  

#####  <a name="UDIWizardReadstheConfigFile"></a> Etapa 1: o Assistente de UDI (OSDSetupWizard.exe) lê o arquivo Config.xml  
 Quando o Assistente de UDI (OSDSetupWizard.exe) é iniciado, ele lê, por padrão, o arquivo de configuração do Assistente de UDI, que é o arquivo UDIWizard_Config.xml – o arquivo de configuração principal para o Assistente de UDI.  

> [!NOTE]
>  O exemplo usa o arquivo Config.xml como arquivo de configuração. No MDT, o arquivo de configuração padrão é o arquivo UDIWizard_Config.xml, que reside na pasta Scripts no pacote de arquivos do MDT para configuração.  

 É possível substituir o arquivo de configuração padrão que o Assistente de UDI usa modificando a etapa de sequência de tarefas do Assistente de UDI para usar o parâmetro **/definition**. Para obter mais informações sobre como substituir o arquivo de configuração padrão que o Assistente de UDI usa, consulte "Substituir o arquivo de configuração que o Assistente de UDI usa".  

 Os elementos de nível superior no arquivo Config.xml são o  

-   Elemento [DLLs](#DLLs)  

-   Elemento [Style](#Style)  

-   Elemento [Pages](#Pages)  

-   Elemento [StageGroups](#StageGroups)  

 Para obter mais informações sobre o esquema do arquivo de configuração do Assistente de UDI e sobre cada um desses elementos, consulte [Referência de esquema do arquivo de configuração do Assistente de UDI](#UDIWizardConfigurationFileSchemaReference).  

 O Assistente de UDI examina o elemento **DLLs** procurando arquivos .dll a serem carregados. No exemplo, dois arquivos .dll são listados: SamplePage.dll e SharedPages.dll. Esses arquivos .dll devem residir na mesma pasta que OSDSetupWizard.exe – a pasta Tools\\*plataforma* (em que *plataforma* é x86 da versão de 32 bits ou x64 da versão de 64 bits).  

 O Assistente de UDI examina o elemento **Pages** procurando as páginas definidas. No exemplo, duas páginas são definidas: **Custom** e **SummaryPage**. O atributo **Type** do elemento **Page** é definido no arquivo PageClassIDs.h e define exclusivamente o tipo de sua página personalizada.  

 No exemplo, o tipo definido é **Microsoft.SamplePage.LocationPage**. Para sua página personalizada, substitua o seguinte para evitar eventuais conflitos com outras páginas que podem ser criadas no futuro:  

-   O nome da sua organização em vez de **Microsoft**.  

-   O nome do projeto no lugar de **SamplePage**.  

-   O nome da página de assistente personalizada em vez de **LocationPage**.  

#####  <a name="UDIWizardLoadstheDLLforCustomWizardPage"></a> Etapa 2: o Assistente de UDI carrega a DLL para a página de assistente personalizada  
 Quando o Assistente de UDI carrega sua DLL, ele chama a função **RegisterFactories**, que deve ser implementada em seu arquivo .dll. No exemplo, essa função é implementada no arquivo dllmain.ccp. Cada página de assistente criada deve implementar a função **RegisterFactories**.  

 A função **RegisterFactories** é usada para registrar a classe de fábrica de sua página de assistente com o Registro de fábrica da classe para o Assistente de UDI. *Fábricas de classe* são classes que podem criar uma instância de outra classe. A função **RegisterFactories** cria uma instância de uma classe de fábrica e passa essa classe para o Registro da fábrica de classes para o Assistente de UDI, que disponibiliza essa classe de fábrica para o assistente. O Assistente de UDI procura uma classe de fábrica registrada com uma ID que corresponde ao atributo **Type** do elemento **Page** da página de assistente personalizada.  

 No exemplo, a ID é definida como **ID_Location** no arquivo PageClassIds.h como **Microsoft.SamplePage.LocationPage**, que corresponde ao atributo **Type** do elemento **Page** no arquivo Config.xml. **ID_Location** é passado como um parâmetro na função **RegisterFactories** implementada no arquivo dllmain.ccp.  

 É possível criar uma função usando o modelo de função Register_*nome* template para simplificar a criação de uma nova instância de fábrica e registrar a instância recém-criada. O valor **nome** fornecido usando o modelo de função de registro deve implementar a interface **iClassFactory**. A [classe ClassFactoryImpl](#ClassFactoryImplClass) manipula a maioria dos detalhes para implementação de uma fábrica de classes.  

 Também é possível usar a função **RegisterFactories** para registrar tipos de tarefa e de validador. Para obter mais informações, consulte:  

-   [Criando tarefas de UDI personalizadas](#CreatingCustomUDITasks)  

-   [Criando validadores de UDI personalizados](#CreatingCustomUDIValidators)  

> [!NOTE]
>  O exemplo contém e registra apenas uma página de assistente personalizada. O exemplo não inclui tarefas ou validadores personalizados e, portanto, não registra nenhuma tarefa ou validador personalizado.  

#####  <a name="UDIWizardDisplaysCustomWizardPage"></a> Etapa 3: o Assistente de UDI exibe a página de assistente personalizada  
 A página de assistente personalizada no exemplo é definida no arquivo LocationPage.cpp. As páginas de assistente são derivadas de classes de modelo que fornecem grande parte da funcionalidade que uma página tem. Todas as páginas do assistente devem derivar da [Classe de modelo WizardPageImpl](#WizardPageImplTemplateClass), que implementa a [Interface IWizardPage](#IWizardPageInterface). Cada página de assistente pode implementar outras classes de modelo opcionais e as interfaces correspondentes com base nas necessidades da página.  

 A [Classe de modelo WizardPageImpl](#WizardPageImplTemplateClass) tem várias interfaces úteis que podem ajudá-lo a escrever páginas de assistente personalizadas. Implemente a [Classe de modelo WizardPageImpl](#WizardPageImplTemplateClass) como a classe base da sua página de assistente personalizada.  

 Para obter uma lista das:  

-   Classes de modelo disponíveis para páginas de assistente, consulte [Wizard Page Helper Classes](#WizardPageHelperClasses) (Classes auxiliares da página de Assistente)  

-   Interfaces disponíveis para as classes de modelo de página de assistente, consulte [Wizard Page Interfaces](#WizardPageInterfaces) (Interfaces de página de assistente)  

 A página de assistente personalizada no exemplo é derivada de [Classe de modelo WizardPageImpl](#WizardPageImplTemplateClass) e implementa a [Interface IWizardPage](#IWizardPageInterface). Além disso, a página de assistente personalizada implementa a interface **IFieldCallback**. Ambas são implementadas no arquivo LocationPage.cpp.  

 A página de assistente personalizada de exemplo substitui os seguintes métodos:  

-   **OnWindowCreated**. O método **OnWindowCreated** na página de assistente de exemplo chama os seguintes métodos:  

    -   [AddField](#AddField). Esse método relaciona o controle da caixa **IDC_COMBO_LOCATION** no recurso **IDD_LOCATION_PAGE** com o elemento [Data](#Data) nomeado **Location** no arquivo Config.xml.  

         Além do método **AddField**, é possível usar os métodos [AddRadioGroup](#AddRadioGroup) e [AddToGroup](#AddToGroup) para dar suporte a outros controles e comportamentos.  

        > [!NOTE]
        >  Chame o método [AddField](#AddField), [AddRadioGroup](#AddRadioGroup) ou [AddToGroup](#AddToGroup) antes de chamar o método [InitFields](#InitFields).  

    -   [InitFields](#InitFields). Use esse método para inicializar os campos (controles) que você adicionou ao formulário. O ponteiro da página é um parâmetro. No exemplo, o ponteiro **isso** é passado, que se refere à página atual.  

        > [!NOTE]
        >  Para dar suporte ao uso do ponteiro **isso**, é necessário implementar a interface **IFieldCallback** além das interfaces compatíveis com a [Classe de modelo WizardPageImpl](#WizardPageImplTemplateClass).  

         A interface **IFieldCallback** chama o método **SetFieldDefault**, usado para definir os valores padrão para controles que não sejam controles de caixa de texto e de caixa de seleção. No exemplo, o método **SetFieldDefault** define o índice inicial do controle de caixa de combinação com base no valor padrão especificado no elemento **Default** para o elemento [Field](#Field) no arquivo Config.xml.  

     O método **OnWindowCreated** configura o controlador de formulário usando a [interface IFormController](#IFormController-Interface). Para obter mais informações sobre como configurar o controlador de formulário, consulte [Setting up the Form](#SettingUptheForm) (Configurando o formulário).  

-   **InitLocations**. Esse método preenche a caixa de combinação da lista de locais no arquivo Config.xml. O elemento [Data](#Data) e os elementos filho [DataItem](#DataItem) do arquivo Confg.xml fornecem a lista de valores possíveis.  

-   **OnNextClicked**. Esse método executa as seguintes tarefas:  

    -   Atualiza a variável de sequência de tarefas **TSLocation** com o valor selecionado na caixa de combinação usando o método **SaveFields**  

    -   Adiciona informações que serão mostradas na página **Resumo** usando o método **SaveFields**  

#####  <a name="TheNextButtonisClickedinCustomWizardPage"></a> Etapa 4: o botão Avançar é clicado na página de assistente personalizada  
 Quando o usuário conclui os campos na página de assistente personalizada, ele clica em **Próximo**, que chama o método **OnNextClicked**. O método **OnNextClicked** executa quaisquer tarefas necessárias antes de prosseguir para a próxima página de assistente, como registrar alterações de configuração feitas na página de assistente personalizada.  

 Para a página de assistente personalizada de exemplo, a substituição do método **OnNextClicked** é implementada no arquivo LocationPage.ccp. No método **OnNextClicked** na página de assistente personalizada de exemplo, são chamados de métodos a seguir:  

1.  [InitSection](#InitSection). Esse método inicializa o cabeçalho (legenda de rótulo) dos dados de resumo exibidos na página **Resumo**. Normalmente, é possível definir esse valor usando a função **DisplayName()**. Os dados associados a essa legenda são salvos usando o método [SaveFields](#SaveFields).  

2.  [SaveFields](#SaveFields). Esse método salva valores de campo para variáveis de sequência de tarefas e para dados exibidos na página **Resumo**.  

###  <a name="ReviewSampleEditorVisualStudioSolution"></a> Examinar a Solução do Visual Studio do SampleEditor  
 Antes de começar a criar suas próprias páginas de assistente personalizado e editores de página de assistente, siga estas etapas para preparar o ambiente de desenvolvimento UDI:  

-   Examine a arquitetura do Designer do Assistente de UDI conforme descrito em [Examinar a arquitetura do Designer do Assistente de UDI](#ReviewUDIWizardDesignerArchitecture).  

-   Examine os componentes de uma página do Assistente de UDI que pode ser personalizada usando o arquivo de configuração do Assistente de UDI, conforme descrito em [Examinar componentes configuráveis de uma página do Assistente de UDI](#ReviewConfigurableComponentsofUDIWizardPage).  

-   Examine o exemplo de EditorPage fornecido no SDK da UDI, conforme descrito em [Examinar o exemplo de EditorPage](#ReviewEditorPageExample).  

####  <a name="ReviewUDIWizardDesignerArchitecture"></a> Examinar a arquitetura do Designer do Assistente de UDI  
 O Designer do Assistente de UDI foi implantado usando o WPF, Prism e Unity. O Designer de UDI é usado para editar o arquivo de configuração do Assistente de UDI (UDIWizard_Config.xml), que o Assistente de UDI (OSDSetupWizard.exe) lê em tempo de execução. O elemento [Pages](#Pages) no arquivo de configuração do Assistente de UDI contém uma lista de páginas que tem um elemento [Page](#Page) separado para cada página do assistente.  

 Quando você edita as configurações de uma página de assistente, o Designer do Assistente de UDI carrega o editor de página personalizada que corresponde ao tipo de página de assistente. Os editores de página de assistente personalizada são desenvolvidos como controles de usuário do WPF. As páginas do editor de página de assistente personalizada usam o padrão de design [MVVM](http://msdn.microsoft.com/magazine/dd419663.aspx) (Model–View–ViewModel) para o WPF.  

 O padrão de design MVVM ajuda a separar a interface do usuário (apresentação) dos dados que está sendo apresentados. Os dados são uma fachada sobre o elemento [Page](#Page) no arquivo de configuração do Assistente de UDI ( arquivo Config.xml no exemplo), acessando usando a propriedade [CurrentPage](#CurrentPage) da interface [IDataService](#IDataService).  

 O Designer do Assistente de UDI usa o **DependencyAttribute** para obter acesso à classe **DataService** com base na estrutura de injeção de dependência no Unity. Para obter mais informações sobre a estrutura de injeção de dependência no Unity, consulte [Inject Some Life into Your Applications—Getting to Know the Unity Application Block](http://msdn.microsoft.com/library/ff650806.aspx) (Injetar vida em seus aplicativos – Conhecendo o bloco de aplicativos do Unity).  

####  <a name="ReviewConfigurableComponentsofUDIWizardPage"></a> Examinar componentes configuráveis de uma página do Assistente de UDI  
 Ao criar sua página de assistente personalizada, algumas configurações podem ser definidas no código e não podem ser alteradas depois de você ter compilado a página. No entanto, para outras configurações, será necessário permitir que essas configurações sejam alteradas usando o Designer do Assistente de UDI.  

 Normalmente, as configurações que você deseja definir usando o Designer do Assistente de UDI são salvas no arquivo de configuração do Assistente de UDI (o arquivo Config.xml no exemplo). No entanto, também é possível criar seu próprio arquivo de configuração separado, se necessário. Um exemplo do uso de um arquivo de configuração separado é o arquivo UDIWizard_Config.xml.app, que a tarefa **Descoberta de aplicativo** e o tipo de página de assistente **ApplicationPage** usam.  

 A seguir, há uma lista das configurações comuns que você pode gerenciar usando o Designer do Assistente de UDI:  

-   **Field**. Os campos de uso permitem que os usuários forneçam uma entrada. Os campos aparecem como elementos [Field](#Field) no arquivo de configuração do Assistente de UDI (UDIWizard_Config.xml), que contém as configurações para cada campo. O editor da página de assistente correspondente precisa fornecer um método para editar as configurações de campo usando o [FieldElementControl](#FieldElementControl).  

-   **Propriedades**. Setters ajudam a criar propriedades para entidades na página, como páginas no elemento [Page](#Page), campos no elemento [Field](#Field) ou dados nos elementos [Data](#Data) ou [DataItem](#DataItem). Configure propriedades nos elementos [Setter](). Adicione um elemento [Setter]() separado para cada propriedade que você deseja definir. Edite as propriedades usando [SetterControl](#SetterControl) e configure outros elementos [Setter]() usando outros controles.  

-   **Dados**. Dados são usados para armazenar informações para uso pela página de assistente e por outros componentes. É possível definir dados para páginas ou para campos usando os elementos [Data](#Data) ou [DataItem](#DataItem). Os dados podem ser definidos em uma estrutura hierárquica ou simples por meio do uso adequado dos elementos [Data](#Data) ou [DataItem](#DataItem). O Config.xml no exemplo no SDK mostra como criar estruturas de dados simples.  

 O editor de página de assistente personalizada que você criar deverá ser capaz de gerenciar essas configurações.  

####  <a name="ReviewEditorPageExample"></a> Examinar o exemplo de EditorPage  
 O exemplo de EditorPage é usado para configurar as definições da página de assistente **SamplePage** no arquivo de configuração do Assistente de UDI. O exemplo de EditorPage tem os seguintes componentes principais:  

-   Interface do usuário para configurar as definições da caixa de combinação **Local**  

-   Interface do usuário para adicionar ou editar um local na lista de locais possíveis, mostrados na caixa de combinação **Local**  

-   Configurações lidas e salvas no arquivo de configuração do Assistente de UDI  

-   Código de suporte para os outros componentes  

 Examine o exemplo de EditorPage no Visual Studio seguindo estas etapas:  

1.  Examine como o editor de página de assistente **SampleEditor** é carregado e inicializado no Designer do Assistente de UDI, conforme descrito em [Examinar o carregamento e a inicialização do editor de página de assistente](#ReviewWizardPageEditorLoadingInitialization).  

2.  Examine a interface do usuário usada para editar a caixa de combinação **Local** nos arquivos LocationPageEditor.xaml e LocationPageEditor.xaml.cs, conforme descrito em [Examinar a interface do usuário usada para configurar a caixa de combinação Local](#ReviewUserInterfaceUsedtoConfigureLocationComboBox).  

3.  Examine a interface do usuário usada para adicionar ou editar locais à lista nos arquivos AddEditLocationView.xaml e AddEditLocationView.xaml.cs, conforme descrito em [Examinar a interface do usuário usada para modificar a lista de possíveis locais](#ReviewUserInterfaceUsedtoModifyListofPossibleLocations).  

4.  Examine o código usado para gerenciar informações de configuração salvas no arquivo de configuração do Assistente de UDI, conforme descrito em [Examinar o código usado para gerenciar informações de configuração](#ReviewCodeUsedtoManageConfigurationInformation).  

#####  <a name="ReviewWizardPageEditorLoadingInitialization"></a> Examinar o carregamento e a inicialização do editor de página de assistente  
 Os editores de página de assistente personalizada são carregados conforme necessário pelo Designer do Assistente de UDI. Os arquivos de configuração do Designer do Assistente de UDI são carregados quando o Designer do Assistente de UDI é iniciado. O Designer do Assistente de UDI examina a pasta *install_folder*\Bin\Config (em que *install_folder* é o nome da pasta na qual o MDT está instalado) para arquivos que têm uma extensão de arquivo .config.  

 Durante a configuração do ambiente de desenvolvimento de UDI, você copiou o arquivo SamplePage.dll.confg para a pasta *pasta_de_instalação*\Bin\Config. Quando você inicia o Designer do Assistente de UDI, o arquivo SamplePage.dll.confg é localizado e carregado.  

 O Designer do Assistente de UDI usa os seguintes atributos do elemento [Page](#Page) no arquivo SamplePage.dll.confg para carregar e inicializar o exemplo de EditorPage:  

-   **DesignerAssembly**. Este atributo determina o nome da DLL a ser carregada. Essa DLL precisa ser colocada na mesma pasta que o arquivo UDIDesigner.exe, que é a pasta *pasta_de_instalação*\Bin (em que *pasta_de_instalação* é o nome da pasta na qual o MDT está instalado).  

-   **DesignerType**. Esse atributo é o nome de tipo do Microsoft .NET da classe que contém o controle de usuário do WPF.  

-   **Tipo**. Use esse atributo para configurar o tipo de página da página de assistente personalizada, que o Assistente de UDI carrega. O Designer do Assistente de UDI usa esse atributo para localizar o elemento [Page](#Page) adequado no arquivo de configuração do Assistente de UDI.  

-   **Dll**. Use esse atributo para configurar o elemento [DLL](#DLL) no arquivo de configuração do Assistente de UDI, criado pelo Designer do Assistente de UDI.  

-   **Descrição**. Use esse atributo para fornecer informações sobre o editor de página de assistente. O valor deste atributo é mostrado na caixa de diálogo **Adicionar nova página** no Designer do Assistente UDI, usado para adicionar a página de assistente à "Biblioteca de páginas".  

-   **DisplayName**. Use esse atributo para fornecer o nome da página de assistente personalizada exibido no Designer do Assistente de UDI. O valor deste atributo é mostrado na caixa de diálogo **Adicionar nova página** no Designer do Assistente UDI, usado para adicionar a página de assistente à "Biblioteca de páginas".  

     No exemplo, o tipo da página de assistente personalizada **SamplePage** é **Microsoft.SamplePage.LocationPage**, salva no arquivo Config.xml. O arquivo Config.xml reside na pasta *pasta_local*\SDK\SamplePage\SamplePage (em que *pasta_local* é a pasta que você criou no computador de desenvolvimento anteriormente no processo de configuração).  

#####  <a name="ReviewUserInterfaceUsedtoConfigureLocationComboBox"></a> Examine a interface do usuário usada para configurar a caixa de combinação Local  
 Quando o editor de página de assistente é carregado e inicializado, o editor de página de assistente do SampleEditor é carregado quando uma página com um tipo de **Microsoft.SamplePage.LocationPage** é editada. A interface do usuário do editor de página é armazenada no arquivo LocationPageEditor.xaml.  

 Se você examinar a interface do usuário na guia **Design** e o código na guia **XAML**, será possível ver a relação entre a interface do usuário gráfica e os elementos e atributos na linguagem XAML.  

 Por exemplo, se você examinar o elemento **Controls:FieldElementControl** no XAML, será possível ver como isso se relaciona com o layout da interface do usuário correspondente. Use o elemento **Controls:FieldElementControl** para definir o controle [FieldElementControl](#FieldElementControl).  

 Os parâmetros **Binding** no arquivo XAML associam os campos no editor de página de exemplo com as informações no arquivo de configuração do Assistente de UDI. Por exemplo, o código a seguir vincula a caixa de texto **Valor padrão** ao elemento [Default](#Default) no arquivo de configuração do Assistente de UDI (Config.xml no exemplo):  

```  
<TextBox Text="{Binding FieldData.DefaultValue,  
 UpdateSourceTrigger=PropertyChanged,  
 Mode=TwoWay}"/>  
```  

 Para obter mais informações, consulte [How to: Make Data Available for Binding in XAML](http://msdn.microsoft.com/library/ms748857.aspx) (Como tornar dados disponíveis para associação no XAML).  

 Use o elemento **Views:CollectionTControl.ColumnCollectionView** no XAML para editar a lista de locais disponíveis no modo de exibição de grade. Use o controle [CollectionTControl](#CollectionTControl) para exibir o modo de exibição de grade e o associe ao elemento [Data](#Data) com o nome **Local** no arquivo de configuração de UDI.  

#####  <a name="ReviewUserInterfaceUsedtoModifyListofPossibleLocations"></a> Examinar a interface do usuário usada para modificar a lista de possíveis locais  
 A interface do usuário para modificar a lista de possíveis locais é composta por:  

-   Um menu contextual e os botões da Faixa de Opções que permitem adicionar, editar, remover ou alterar a ordem dos itens na lista de locais, conforme descrito em [Examinar o menu contextual e botões da Faixa de Opções para modificar a lista de locais](#ReviewContextSensitiveMenuandRibbonButtons)  

-   Uma caixa de diálogo iniciada quando você seleciona para adicionar ou editar um item na lista de locais, conforme descrito em [Examinar a caixa de diálogo para adicionar ou editar locais](#ReviewDialogBoxforAddingEditingLocations)  

######  <a name="ReviewContextSensitiveMenuandRibbonButtons"></a> Examinar o menu contextual e botões da Faixa de Opções para modificar a lista de locais  
 Quando você clica com o botão direito do mouse na caixa de listagem que contém a lista de locais, é exibido um menu contextual. A Faixa de Opções tem botões correspondentes que permitem executar as mesmas tarefas. O elemento de controle **Views:CollectionsTControl** no arquivo LocationPageEditor.xaml define os métodos chamados com base na ação executada e nas propriedades definidas como segue:  

-   **SelectedItem**. Essa propriedade associada a dados é ativada quando o usuário seleciona um item da lista. Essa propriedade está vinculada à propriedade **CurrentLocation** no modelo de exibição, localizado no arquivo LocationPageEditorViewModel.cs e usado pelo controle [CollectionTControl](#CollectionTControl) para passar o item selecionado quando você edita ou remove um item existente.  

-   **AddItemAction**. Esta ação é executada quando o usuário clica na opção **Adicionar Item** no menu contextual ou nos botões correspondentes na Faixa de Opções. Há uma associação de dados em uma propriedade no modelo de exibição que retorna o objeto **AddLocationAction**. Esse objeto é o método **AddLocationCallback**, localizado no arquivo LocationPageEditorViewModel.cs, e exibe a caixa de diálogo no arquivo AddEditLocationView.xaml.  

-   **EditItemAction**. Esta ação é executada quando o usuário clica na opção **Editar Item** no menu contextual. Há uma associação de dados em uma propriedade no modelo de exibição que retorna o objeto **EditLocationAction**. Esse objeto é o método **EditLocationCallback**, localizado no arquivo LocationPageEditorViewModel.cs, e exibe a caixa de diálogo no arquivo AddEditLocationView.xaml.  

-   **RemoveAction**. Esta ação é executada quando o usuário clica na opção **Remover Item** no menu contextual. Há uma associação de dados em uma propriedade no modelo de exibição que retorna o objeto **RemoveAction**. Esse objeto é o método **EditLocationCallback**, localizado no arquivo LocationPageEditorViewModel.cs, e mostra uma mensagem que confirma a exclusão do local.  

######  <a name="ReviewDialogBoxforAddingEditingLocations"></a> Examinar a caixa de diálogo para adicionar ou editar locais  
 Se você adicionar um novo local à lista de locais ou editar um local existente, será exibida uma mensagem que está no arquivo AddEditLocationView.xaml. A mensagem é exibida usando o método de janela [ShowDialogWindow](#ShowDialogWindow) no arquivo LocationPageEditorViewModel.cs.  

 A interface do usuário no arquivo AddEditLocationView.xaml é composta por:  

-   Um quadro de diálogo denominado **DialogFrame**, que inclui os seguintes elementos:  

    -   Um título, que você configura usando o atributo **DialogTitle** do quadro de diálogo  

    -   Um botão **OK**, que define o status de retorno quanto à propriedade **Aprovado** como **True** (O status de retorno é verificado no método **AddLocationCallback** no arquivo LocationPageEditorViewModel.cs para determinar se o usuário clicou em **OK**.)  

    -   Um botão **Cancelar**, que define o status de retorno quanto à propriedade **Aprovado** como **False** (O status de retorno é verificado no método **AddLocationCallback** no arquivo LocationPageEditorViewModel.cs para determinar se o usuário clicou em **Cancelar**.)  

-   Um elemento do WPF que contém:  

    -   Um rótulo, que você configura usando o atributo **Content**  

    -   Uma caixa de texto, associada ao elemento [Data](#Data) com o **Local** do nome no arquivo de configuração de UDI (o arquivo Config.xml no exemplo)  

######  <a name="ReviewCodeUsedtoManageConfigurationInformation"></a> Examinar o código usado para gerenciar informações de configuração  
 As informações de configuração para a sua página de assistente personalizada são armazenadas no arquivo de configuração do Assistente de UDI, que é o:  

-   Arquivo Config.xml no exemplo fornecido com o SDK da UDI (este arquivo contém apenas as configurações do exemplo).  

-   Arquivo UDIWizard_Config.xml fornecido com o MDT, armazenado na pasta *pasta_de_instalação*\Templates\Distribution\Scripts (em que *pasta_de_instalação* é a pasta na qual você instalou o MDT); esse arquivo contém as configurações de todas as páginas e estágios internos do assistente  

 No exemplo SampleEditor, a rotina **Locais** ajuda a gerenciar as informações de configuração e está localizada no arquivo LocationPageEditorViewModel.cs. A rotina **Locais** retorna uma lista dos locais do arquivo de configuração do Assistente de UDI. Especificamente, a lista retornada contém um item para cada elemento [DataItem](#DataItem) no arquivo de configuração do Assistente de UDI.  

## <a name="creating-custom-udi-wizard-pages"></a>Criando páginas de assistente de UDI personalizadas  
 O processo de alto nível para criar páginas de assistente de UDI personalizadas é o seguinte:  

1.  Faça uma cópia da solução SamplePage como ponto de partida.  

2.  Coloque os controles desejados (campos) no formulário.  

3.  Escreva o código para executar tarefas adequadas quando a página de assistente é carregada (substitui o método **OnWindowCreated**), incluindo as etapas a seguir:  

    1.  Inicialize o formulário.  

    2.  Leia variáveis de memória, variáveis de sequência de tarefas, variáveis de ambiente ou informações de arquivo XML (como propriedades **Setter**).  

4.  Escreva qualquer código para executar as tarefas adequadas quando página for mostrada (substitui o método **OnWindowShown**), incluindo as seguintes etapas:  

    1.  Habilite ou desabilite controles com base nas informações lidas quando a página foi carregada na etapa 3.  

    2.  Atualize os controles com base nas informações lidas quando a página foi carregada na etapa 3, como o rastreamento de controles com base nas informações lidas.  

5.  Escreva qualquer código para executar as tarefas adequadas enquanto o usuário interage com a página de assistente.  

6.  Escreva qualquer código para executar as tarefas adequadas quando o usuário clica em **Avançar** no Assistente de UDI (substitui o método **OnNextClicked**), incluindo as etapas a seguir:  

    1.  Atualize quaisquer variáveis de memória, variáveis de sequência de tarefas, variáveis de ambiente ou informações do arquivo XML.  

    2.  Atualize informações de página de resumo (se não foi executado pelos campos na página).  

7.  Crie a solução.  

     Certifique-se de que a versão da DLL criada é a mesma plataforma de processador que a instalação do MDT – especificamente, a plataforma de processador do Windows PE (Ambiente de Pré-Instalação do Windows). O Assistente de UDI pode ser executado:  

    -   **No sistema operacional existente no computador de destino**. É possível executar versões de 32 bits de sua página de assistente em sistemas operacionais Windows de 32 bits ou de 64 bits. No entanto, é possível executar apenas versões de 64 bits de sua página de assistente em sistemas operacionais Windows de 64 bits.  

    -   **Windows PE no computador de destino**. O Windows PE não é compatível com a execução de aplicativos de 32 bits em uma versão de 64 bits do Windows PE. Portanto, é necessário ter criado uma versão de sua página de assistente para cada arquitetura de processador do Windows PE que você planeja usar.  

8.  Copie a DLL da sua página de assistente personalizada para a pasta da plataforma *pasta_de_instalação*\Templates\Distribution\Tools\ (em que *pasta_de_instalação* é a pasta na qual você instalou o MDT e a *plataforma* é **x86** para a versão de 32 bits ou **x64** é para a versão de 64 bits).  

9. Conclua as etapas para criar o editor de página personalizada.  

## <a name="creating-custom-wizard-page-editors"></a>Criando editores de páginas de assistente personalizadas  
 O processo de alto nível para criar editores de páginas de assistente de UDI personalizadas é o seguinte:  

1.  Faça uma cópia da solução SampleEditor como ponto de partida.  

2.  Crie a interface do usuário do editor de página principal em um arquivo .xaml.  

3.  Adicione instâncias do controle [FieldElementControl](#FieldElementControl) conforme exigido pela página de assistente a ser configurada (se necessário).  

4.  Adicione instâncias do controle [SetterControl](#SetterControl) conforme exigido pela página de assistente a ser configurada (se necessário).  

5.  Adicione instâncias do controle [CollectionTControl](#CollectionTControl) conforme exigido pela página de assistente a ser configurada (se necessário).  

6.  Adicione a interface [IDataService](#IDataService).  

7.  Escreva o código adequado para atualizar o arquivo de configuração do Assistente de UDI com base nas configurações a serem definidas usando seu editor de páginas de assistente personalizadas.  

8.  Crie caixas de diálogo filho em um arquivo .xaml e chame-as do editor de páginas principal usando a interface [IMessageBoxService](#IMessageBoxService) conforme exigido pela página do assistente a ser configurado.  

9. Adicione as interfaces adequadas à Faixa de Opções do Designer do Assistente de UDI com base nos requisitos da página do assistente a ser configurado.  

10. Crie a solução.  

    > [!NOTE]
    >  Certifique-se de que a versão da DLL que você criar será a mesma plataforma de processador que a da instalação do MDT. Por exemplo, se você instalar a versão de 64 bits do MDT, crie uma versão de 64 bits do seu editor de página personalizada.  

11. Crie um arquivo de configuração do Designer do Assistente de UDI para carregar as DLLs necessárias e mapear o editor de página de assistente com a página de assistente correspondente (o arquivo SamplePage.dll.config no exemplo).  

     Para obter mais informações sobre os elementos necessários para realizar o mapeamento entre a página de assistente e o editor de página de assistente, consulte o elemento [DesignerMappings](#DesignerMappings), elementos filho e atributos correspondentes.  

12. Copie o arquivo de configuração do Designer de Assistente UDI criado na etapa anterior para a pasta *pasta_de_instalação*\Bin\Config (em que *pasta_de_instalação* é a pasta na qual você instalou a versão do MDT).  

13. Copie a DLL do seu editor de páginas de assistente personalizadas para a pasta *pasta_de_instalação*\Bin (em que *pasta_de_instalação* é a pasta na qual você instalou o MDT).  

##  <a name="CreatingCustomUDITasks"></a> Criando tarefas de UDI personalizadas  
 *Tarefas de UDI* são DLLs escritas em C++ que implementam a [interface ITask](#ITaskinterface). Registre a DLL com a biblioteca de tarefas do Designer do Assistente de UDI criando um arquivo de configuração do Designer do Assistente de UDI (arquivo .config) e colocando-o na pasta *pasta_de_instalação*\Bin\Config (em que *pasta_de_instalação* é a pasta na qual você instalou o MDT).  

> [!NOTE]
>  É possível criar uma DLL que contém páginas de assistente, tarefas e validadores dentro do mesmo arquivo .dll. Também é possível criar um único arquivo de configuração (.config) do Designer do Assistente de UDI que contenha as configurações da página de assistente, tarefas e validadores na DLL.  

 **Para criar tarefas de UDI personalizadas**  

1.  Escreva o código que implementa a [Interface ITask](#ITaskinterface) e os seguintes métodos:  

    -   [Init](#Init). Esse método é chamado para inicializar sua tarefa.  

    -   [Execute](#Execute). Esse método é chamado para executar sua tarefa.  

2.  Escreva o código que registra a fábrica de classes de tarefa personalizada com o Registro da fábrica.  

3.  Crie a solução para sua tarefa personalizada.  

    > [!NOTE]
    >  Certifique-se de que a versão da DLL que você criar será a mesma plataforma de processador que a da instalação do MDT. Por exemplo, se você instalar a versão de 64 bits do MDT, crie uma versão de 64 bits da tarefa UDI personalizada.  

4.  Crie um elemento [Task](#Task) no elemento [TaskLibrary](#TaskLibrary) no arquivo de configuração do Designer do Assistente de UDI semelhante ao trecho a seguir:  

    ```  
    <Task DLL="OSDRefreshWizard.dll" Description="Discovers supported applications for install." Type="Microsoft.OSDRefresh.AppDiscoveryTask" Name="Application Discovery">  
       <TaskItem Type="Setter" Name="Status Bitmap">  
          <Param Name="BitmapFilename"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Log File">  
          <Param Name="log"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Write Configuration File">  
          <Param Name="writecfg"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Read Configuration File">  
          <Param Name="readcfg"/>  
       </TaskItem>  
    </Task>  
    ```  

    > [!NOTE]
    >  Todos os elementos [Task](#Task) devem incluir o parâmetro **BitmapFilename**. Especifique todos os outros parâmetros como a tarefa requer. Por exemplo, no trecho anterior, o parâmetro **log** é usado para especificar um parâmetro para o local de um arquivo de log.  

5.  Copie o arquivo de configuração do Designer de Assistente UDI criado na etapa anterior para a pasta *pasta_de_instalação*\Bin\Config (em que *pasta_de_instalação* é a pasta na qual você instalou o MDT).  

6.  Copie a DLL da sua tarefa personalizada para a pasta da plataforma *pasta_de_instalação*\Templates\Distribution\Tools\ (em que *pasta_de_instalação* é a pasta na qual você instalou o MDT e a *plataforma* é **x86** para a versão de 32 bits ou **x64** é para a versão de 64 bits).  

##  <a name="CreatingCustomUDIValidators"></a> Criando validadores de UDI personalizados  
 *Validadores de UDI* são DLLs escritas em C++ que implementam a interface **IValidator**. Registre a DLL com a biblioteca de validadores do Designer do Assistente de UDI criando um arquivo de configuração do Designer do Assistente de UDI (arquivo .config) e colocando-o na pasta *pasta_de_instalação*\Bin\Config (em que *pasta_de_instalação* é a pasta na qual você instalou o MDT).  

 **Para criar validadores de UDI personalizados**  

1.  Escreva um código que crie uma subclasse da classe **BaseValidator** e implemente os métodos a seguir:  

    -   **Init(IControl \*pControl, IWizardPageContainer \*pContainer, IStringProperties \*pProperties)**. O controlador de formulário chama o membro **Init** para inicializar o validador. Esse método deve chamar o método **Init** para a classe **BaseValidator**. Normalmente, ele lê qualquer conjunto de propriedades para o validador do arquivo de configuração do Assistente de UDI. Por exemplo, o validador **InvalidCharactersValidator** recupera o valor da propriedade **InvalidChars** usando esse método.  

    -   **IsValid**. O controlador de formulário chama esse método para verificar se o controle contém um texto válido. A seguir há um exemplo do método **IsValid** para um validador que valida se o campo não está vazio:  

        ```  
        BOOL IsValid(LPBSTR pMessage)  
        {  
            __super::IsValid(pMessage);  

            _bstr_t text;  
            m_pText->GetText(text.GetAddress());  
            return (text.length() > 0);  
        }  
        ```  

    -   **Init(IControl \*pControl, mensagem LPCTSTR)**. O controlador de formulário chama esse membro para cada pressionamento de tecla e outros eventos para que o validador possa validar o conteúdo do controle e as mensagens atualizadas na parte inferior da página do assistente (ou limpá-los).  

     Normalmente, esses são os únicos métodos que você precisa substituir. No entanto, dependendo do validador, talvez seja necessário substituir outros métodos na subclasse da classe **BaseValidator** que você criar. Para obter mais informações sobre esses outros métodos, consulte a classe **BaseValidator**.  

2.  Escreva o código que registra a classe de tarefa personalizada com a fábrica do Registro.  

3.  Crie a solução para sua tarefa personalizada.  

    > [!NOTE]
    >  Certifique-se de que a versão da DLL que você criar será a mesma plataforma de processador que a da instalação do MDT. Por exemplo, se você instalar a versão de 64 bits do MDT, crie uma versão de 64 bits da tarefa UDI personalizada.  

4.  Crie um elemento [Validator](#Validator) no elemento **ValidatorLibrary** no arquivo de configuração do Designer do Assistente de UDI semelhante ao trecho a seguir:  

    ```  
    <Validator   
    <Validator DLL="" Description="Must follow a pre-defined pattern" Type="Microsoft.Wizard.Validation.RegEx" Name="NamedPattern">  
       <Param Description="Enter the message you want displayed when the text in this field doesn't match the pattern:" Name="Message" DisplayName="Message"/>  
       <Param Description="The name of a pre-defined regular expression pattern. Must be Username, ComputerName, or Workgroup" Name="NamedPattern" DisplayName="Named Pattern"/>  
    </Validator>  
    ```  

    > [!WARNING]
    >  Todos os elementos [Validator](#Validator) elementos devem incluir o parâmetro **Message**. Especifique todos os outros parâmetros conforme exigido pelo validador. Por exemplo, no trecho anterior, o parâmetro **NamedPattern** é usado para especificar um parâmetro para o nome de um padrão de expressão regular predefinido.  

5.  Copie o arquivo de configuração do Designer de Assistente UDI criado na etapa anterior para a pasta *pasta_de_instalação*\Bin\Config (em que *pasta_de_instalação* é a pasta na qual você instalou o MDT).  

6.  Copie a DLL da sua tarefa personalizada para a pasta da plataforma *pasta_de_instalação*\Templates\Distribution\Tools\ (em que *pasta_de_instalação* é a pasta na qual você instalou o MDT e a *plataforma* é **x86** para a versão de 32 bits ou **x64** é para a versão de 64 bits).  

## <a name="udi-wizard-reference"></a>Referência do Assistente de UDI  

### <a name="wizard-page-components"></a>Componentes da página do assistente  
 É possível usar qualquer um de vários componentes pré-criados para criar suas páginas personalizadas.  

#### <a name="creating-component-instances"></a>Criando instâncias de componente  
 O Assistente de UDI usa fábricas de classes para criar instâncias de objetos para você. Essas fábricas são registradas com um Registro de fábrica usando uma cadeia de caracteres como a chave para a fábrica. Por exemplo, o componente **WmiRepository** é identificado pela cadeia de caracteres "Microsoft.Wizard.WmiRepository," que está disponível no arquivo de cabeçalho IWmiRepository como **ID_WmiRepository**.  

 Supondo que você tenha escrito sua página como uma subclasse de **WizardPageImpl**, é possível criar uma nova instância de um **WmiRepoistory** como isto:  

```  
PWmiRepository pWmi;  
CreateInstance(Container(), ID_WmiRepository, &pWmi);  
```  

 **CreateInstance** é uma função de modelo fortemente tipada para criar novas instâncias de componentes. **PWmiRepository** é um ponteiro inteligente que manipula a contagem de referências para você.  

#### <a name="creatable-components"></a>Componentes criáveis  
 Há um conjunto de componentes que você pode registrar com o Registro. O primeiro conjunto de componentes sempre é registrado, porque o principal arquivo executável do Assistente de UDI o fornece. Os outros dois conjuntos de componentes são fornecidos nas DLLs "opcionais". Para esses componentes estarem disponíveis, a DLL deve estar listada na seção **DLLs** do arquivo XML .config. Seu código não precisa saber qual executável contém um componente específico.  

 A lista de IDs dos componentes (o nome do componente é o mesmo que a ID, mas sem a *ID_* inicial) registrada com o Registro de fábrica (definido em OSDSetupWizard) é mostrada na Tabela 3.  

### <a name="table-3-component-ids"></a>Tabela 3. IDs dos componentes  

|**ID**|**Descrição**|  
|-|-|  
|ID_ACPowerTask|(ITask, IWizardComponent) Uma tarefa de simulação que garante que seu computador não está sendo executado apenas com bateria|  
|ID_AppDiscoveryTask|(ITask, IWizardComponent) Uma tarefa especializada para detectar quais itens de software você instalou em seu computador|  
|**ID_BackgroundTask**|(**IBackgroundTask**, **IWizardComponent**) Pode ser usada para executar uma tarefa em outro thread|  
|**ID_CopyFilesTask**|(**ITask**, **IWizardComponent**) Uma tarefa para copiar um ou mais arquivos|  
|**ID_FormController**|(**IFormController**) Você provavelmente não precisará criar uma instância sozinho, uma vez que sua página recebe a própria instância|  
|**ID_InvalidCharactersValidator**|(**IValidator**) Garante que nenhum campo de texto contém caracteres de uma lista fornecida ao validador|  
|**ID_Logger**|(**ILogger**) Você provavelmente não precisará criar uma instância sozinho, uma vez que sua página recebe um ponteiro para a instância compartilhada|  
|**ID_NonEmptyValidator**|(**IValidator**) Um validador que garante que nenhum campo está vazio|  
|**ID_PasswordValidator**|(**IValidator**) Um validador que garante que dois campos não tenham o mesmo conteúdo|  
|**ID_Regex**|(**IRegEx**) Avalia expressões regulares, procurando correspondências|  
|**ID_RegExValidator**|(**IValidator**) Um validador valida em relação a uma expressão regular ou a um padrão conhecido|  
|**ID_SimpleStringProperties**|(**IStringProperties**, **ISimpleStringProperties**) Fornece uma maneira simples de enviar propriedades para tarefas sem usar XML|  
|**ID_ShellExecuteTask**|(**ITask**, **IWizardComponent**) Executa um programa externo|  
|**ID_SummaryBag**|(**ISummaryBag**) Disponível indiretamente de sua página por meio do método Form|  
|**ID_TaskManager**|(**ITaskManager**, **IBackgroundCallback**, **IWizardComponent**) Gerencia a execução de um conjunto de tarefas e da interface do usuário|  
|**ID_WmiRepository**|(**IWmiRepository**, **IWizardComponent**) Permite executar consultas WMI (Instrumentação de Gerenciamento do Windows)|  
|**ID_IXmlDocument**|(**IXmlDocument**) Fornece uma fachada para ler e gravar documentos XML|  

 A OSDRefreshWizard.dll definida, páginas compartilhadas e outros componentes de controle são mostrados na Tabela 4 e na Tabela 5.  

### <a name="table-4-directory-controls"></a>Tabela 4. Controles de diretório  

|**ID**|**Descrição**|  
|-|-|  
|**ID_Directory**|(**IDirectory**) Uma fachada para obter informações de diretório do sistema de arquivos|  

### <a name="table-5-defined-sharedpagesdll"></a>Tabela 5. Defined SharedPages.dll  

|**ID**|**Descrição**|  
|-|-|  
|**ID_ADHelper**|(**IADHelper**) Fornece uma fachada para um conjunto limitado de recursos no AD DS (Active Directory Domain Services®)|  
|**ID_CpuInfo**|(**ICpuInfo**) Determina se sua CPU é de 32 ou de 64 bits|  
|**ID_DomainJoinValidator**|(**IDomainJoinValidator**) Tem alguns métodos para verificar se um conjunto de credenciais tem permissão para ingressar em um domínio|  
|**ID_DriveList**|(**IDriveList**, **IBindableList**, **IWizardComponent**) Usa o WMI para obter uma lista de unidades em seu computador|  
|**ID_WiredNetworkTask**|(**ITask**) Uma tarefa que verifica se você está conectado à rede com um adaptador de rede cabeado (em vez de um sem fio)|  

#### <a name="control-components"></a>Componentes de controle  
 Você interage com os controles em sua página por meio da função de modelo **GetControlWrapper**, que fornece acesso a um dos tipos de componentes listados na Tabela 6.  

### <a name="table-6-components"></a>Tabela 6. Componentes  

|**Tipos de controle de caixa de diálogo**|**Descrição**|  
|-|-|  
|**CONTROL_CHECK_BOX**|(**ICheckBox**) Uma fachada para trabalhar com controles de caixa de seleção|  
|**CONTROL_COMBO_BOX**|(**IComboBox**) Uma fachada para controles de caixa de combinação|  
|**CONTROL_GENERIC**|(**IControl**) Permite trabalhar com a maioria dos tipos de controles para controlar o estado visível e de habilitação|  
|**CONTROL_LIST_VIEW**|(**IListView**) Uma fachada que fornece acesso aos recursos de um controle de exibição de lista|  
|**CONTROL_PROGRESS_BAR**|(**IProgressBar**) Uma fachada para trabalhar com a posição de um controle de barra de progresso|  
|**CONTROL_RADIO_BUTTON**|(**IRadioButton**) Uma fachada para trabalhar com controles de botão de opção|  
|**CONTROL_STATIC_TEXT**|(**IStaticText**) Uma fachada que oferece permissão de leitura/gravação para o texto de um controle, como um rótulo ou caixa de texto|  
|**CONTROL_TREE_VIEW**|(**ItreeView**) Uma fachada para trabalhar com um controle de exibição de árvore|  

#### <a name="image-list-component"></a>Componente de lista de imagens  
 Esse componente é uma fachada para um controle **ImageList** em sua página. Crie uma lista de imagens por meio da interface **IListView** ou **ITreeView**.  

#### <a name="formcontroller-component"></a>Componente FormController  
 O assistente cria esse componente para você e o passa para a página. Acesse-o na sua página usando o método **Form**, implementado pela classe base **WizardPageImpl**.  

#### <a name="invalidcharactervalidator-component"></a>Componente InvalidCharacterValidator  
 Este é um tipo de validador que pode ser incluído em uma página. A ID é **ID_InvalidCharactersValidator** (definida em IValidator.h), que tem um valor de texto de "Microsoft.Wizard.Validation.InvalidChars."  

 Esse validador procura uma única propriedade (um elemento **Setter** no arquivo .config) chamado **InvalidChars**, que é uma lista de caracteres que não são permitidos. Ele verifica os caracteres em uma caixa de texto; se o texto contiver caracteres desta lista, o componente relatará uma falha.  

#### <a name="nonemptyvalidator-component"></a>Componente NonEmptyValidator  
 Este é um tipo de validador que pode ser incluído em uma página. A ID é **ID_NonEmptyValidator** (definida em IValidator.h), que tem um valor de texto de "Microsoft.Wizard.Validation.NonEmpty."  

 Esse validador relatará uma falha se a caixa de texto (ou qualquer outro controle compatível com **IStaticText**) tiver um valor de cadeia de caracteres vazio.  

#### <a name="passwordvalidator-component"></a>Componente PasswordValidator  
 Este é um tipo de validador que pode ser incluído em uma página. A ID é **ID_PasswordValidator** (definida em IValidator.h), que tem um valor de texto de "Microsoft.Wizard.Validation.Password."  

 Esse validador funciona com dois controles de texto diferentes (controles compatíveis com **IStaticText**) e relatará falha se eles não contiverem os mesmos valores. Em outras palavras, haverá falha se as caixas de texto **Senha** e **Confirmar senha** não coincidirem.  

 Como esse validador requer dois controles, são necessárias mais etapas de configuração do que os outros validadores. A configuração pode ter esta aparência:  

```  
Form()->AddToGroup(IDC_EDIT_PASSWORD, IDC_EDIT_PASSWORD2);  
PValidator pValidator;  
Form()->AddValidator(IDC_EDIT_PASSWORD, ID_PasswordValidator, pMessage, &pValidator);  
PStaticText pPassword2;  
GetControlWrapper(View(), IDC_EDIT_PASSWORD2, CONTROL_STATIC_TEXT, &pPassword2);  
pValidator->SetProperty(0, pPassword2);  
```  

 Primeiro, defina o controle **Confirmar senha** como “filho” do controle **Senha**. Dessa forma, se o controlador de formulário desabilitar o controle **Senha**, ele também desabilitará o controle **Confirmar senha**. Em seguida, adicione um validador de senha ao formulário. Por fim, forneça uma interface ao validador de senha para o controle **Confirmar senha**.  

 Por causa do requisito de dois controles, é necessário usar um código para configurar esse validador, em vez do arquivo XML .config.  

#### <a name="regexvalidator-component"></a>Componente RegExValidator  
 Este é um tipo de validador que pode ser incluído em uma página. A ID é **ID_RegExValidator** (definida em IValidator.h), que tem um valor de texto de "Microsoft.Wizard.Validation.RegEx."  

 Esse validador compara o conteúdo de um controle de texto (compatível com **IStaticText**) com uma expressão regular e falhará se o texto não coincidir com a expressão regular.  

 Como alternativa, é possível usar esse validador com um padrão nomeado predefinido. Para usar uma expressão regular, o XML deverá conter uma propriedade setter chamada **Pattern**. Se desejar usar um padrão nomeado, use um setter chamado **NamedPattern** definido como um dos valores na Tabela 7.  

### <a name="table-7-named-pattern-setters"></a>Tabela 7. Setters do padrão nomeado  

|**Padrão**|**Descrição**|  
|-|-|  
|Nome de usuário|Verifica se o texto está no formato domínio\usuário ou user@domain|  
|ComputerName|O nome deve ter entre 1 e 15 caracteres e não pode incluir um conjunto de caracteres (como : e ?)|  
|Grupo de trabalho|O nome deve ter entre 1 e 15 caracteres e não pode conter um conjunto de caracteres (como =, + e ?)|  

#### <a name="factoryregistry-component"></a>Componente FactoryRegistry  
 Esse componente controla todos os serviços e fábricas de classes. Ele implementa a interface **IFactoryRegistry** e está disponível indiretamente por meio do método **Container** da sua página. Além disso, o Registro carrega DLLs de extensão. Depois que ele carregar uma DLL, o Registro procurará uma função exportada chamada **RegisterFactories**. É necessário implementar essa função e, nela, registrar as fábricas de classes de suas páginas, tarefas e validadores (e quaisquer outras fábricas de classes que você deseja registrar). Veja um exemplo do projeto:  

```  
extern "C" __declspec(dllexport) void RegisterFactories(IFactoryRegistry *factories)  
{  
Register<LocationPageFactory>(ID_LocationPage, factories);  
}  
```  

#### <a name="logger-component"></a>Componente Logger  
 Esse componente está disponível para sua página por meio do método **Logger** (implementado por **WizardPageImpl**). Use esse método para gravar entradas no arquivo de log. O conteúdo do arquivo de log é útil para diagnosticar problemas que os usuários podem ter ao executar o Assistente de UDI.  

#### <a name="propertybag-component"></a>Componente PropertyBag  
 O *recipiente de propriedades* é um contêiner para variáveis de memória. Ele está disponível na sua página usando **Contêiner()->Propriedades()**. As variáveis de memória são úteis para passar dados temporários entre páginas diferentes.  

#### <a name="tsvariablebag-and-tsrepository-components"></a>Componentes TSVariableBag e TSRepository  
 O componente **TSVariableBag** permite que você leia e grave variáveis de sequência de tarefas. Ele mantém os valores na memória até que o usuário clique em **Concluir** (por padrão). É possível acessar o recipiente **TSVariable** por meio do método **TSVariables** da página (implementado pela classe base **WizardPageImpl**). Esses componentes registram todas as leituras e gravações de variáveis de sequência de tarefas.  

#### <a name="wmirepository-component"></a>Componente WmiRepository  
 Esse componente oferece uma fachada para trabalhar com consultas WMI. É possível chamar a função auxiliar **CreateInstance** com **ID_WmiRepository** para obter uma instância desse componente, compatível com a interface **IWmiRepository**. Esse componente retorna registros de resultados por meio da interface **IWmiIterator**.  

###  <a name="WizardPageHelperClasses"></a> Classes auxiliares da página de assistente  
 É possível criar páginas de assistente de UDI personalizadas usando classes auxiliares internas fornecidas com o SDK da UDI. A Tabela 8 lista as classes auxiliares que você pode usar para criar páginas de assistente personalizadas.  

### <a name="table-8-helper-classes"></a>Tabela 8. Classes auxiliares  

|**Classe auxiliar**|**Descrição**|  
|-|-|  
|[Classe ClassFactoryImpl](#ClassFactoryImplClass)|Isso é uma classe base útil para a criação de uma fábrica de classes que você pode registrar com o Registro de fábrica.|  
|[Classe de modelo Interface](#InterfaceTemplateClass)|Use essa classe de modelo quando quiser criar um componente que implementa mais de uma interface.|  
|[Classe auxiliar Path](#PathHelperClass)|Essa classe fornece operações comuns de diretório/arquivo.|  
|[Classe de modelo Pointer](#PointerTemplateClass)|Essa classe fornece contagem de referências para gerenciamento de tempo de vida em componentes COM. É importante liberar interfaces quando as concluir. Essa classe de modelo manipula o tempo de vida automaticamente.|  
|[Classe PUnknown](#PUnkownClass)|Essa classe é um ponteiro inteligente especificamente para a interface IUnknown. Para todas as outras interfaces, use a classe de modelo Pointer.|  
|[Classe auxiliar StringUtil](#StringUtilHelperClass)|Essa classe oferece métodos auxiliares que tornam mais fácil trabalhar com cadeias de caracteres.|  
|[Classe de modelo SubInterface](#SubInterfaceTemplateClass)|Essa classe base torna mais fácil implementar um componente compatível com uma interface herdada de outra interface.|  
|[Classe de modelo UnknownImpl](#UnknownImplTemplateClass)|Essa classe manipula a maioria dos detalhes da criação de um componente COM.|  
|[Classe de modelo WizardComponent](#WizardComponentTemplateClass)|Essa classe base é usada para criar componentes que precisam acessar os serviços de assistente, como a criação e o registro em log de componentes.|  
|[Classe de modelo WizardPageImpl](#WizardPageImplTemplateClass)|Essa classe base deve ser usada como a classe base para todas as páginas de assistente personalizadas|  

####  <a name="ClassFactoryImplClass"></a> Classe ClassFactoryImpl  
 Isso é uma classe base útil para a criação de uma fábrica de classes que você pode registrar com o Registro de fábrica.  

 A seguir há um trecho do arquivo LocationPage.h no projeto de exemplo para definir a classe **ClassFactoryImpl**.  

```  
#pragma once  

#include "ClassFactoryImpl.h"  

class LocationPageFactory :public ClassFactoryImpl  
{  
protected:  
    IUnknown *CreateNewInstance();  
};  
```  

 A seguir, há um trecho do arquivo LocationPage.cpp na página de assistente de exemplo usada para definir a fábrica de classes da página.  

```  
IUnknown *LocationPageFactory::CreateNewInstance()  
{  
    return static_cast<IWizardPage *>(new LocationPage);  
}  
```  

####  <a name="InterfaceTemplateClass"></a> Classe de modelo Interface  
 Use essa classe de modelo quando desejar criar um componente que implemente mais de uma interface, por exemplo:  

```  
classLocationPage :public Interface<IFieldCallback, WizardPageImpl<IDD_LOCATION_PAGE>>  
```  

 Esse código cria uma cadeia de classe base compatível com **IFieldCalback** e com as interfaces compatíveis com **WizardPageImpl** (que é **IWizardPage**).  

####  <a name="PathHelperClass"></a> Classe auxiliar Path  
 Essa classe fornece operações comuns de diretório/arquivo:  

```  
static inline std::wstring GetModulePath(HINSTANCE hModule)  
```  

 Ela também retorna o caminho completo para o arquivo .exe ou .dll com o identificador de instância que você fornece a este método:  

```  
static inline std::wstring GetModuleFilename(HINSTANCE hModule)  
```  

 Essa classe retorna o caminho e o nome do arquivo completos do arquivo .exe e .dll com o identificador da instância fornecida a este método:  

```  
static inline std::wstring GetDirecotryName(LPCWSTR fullName)  
```  

 . . . ou apenas o caminho ao retirar o nome do arquivo:  

```  
static inline std::wstring GetFileName(LPCWSTR fullName)  
```  

 Dado um caminho com um nome de arquivo, a classe do auxiliar de caminho retorna apenas o nome do arquivo:  

```  
static inline std::wstring Combine(LPCWSTR path, LPCWSTR name)  
```  

 Por fim, a classe retorna uma nova cadeia de caracteres que é o caminho e o nome do arquivo combinados (ou outro caminho).  

####  <a name="PointerTemplateClass"></a> Classe de modelo Pointer  
 Essa classe é definida em Pointer.h. Como os componentes COM usam a contagem de referências para o gerenciamento de tempo de vida, é importante que você sempre libere interfaces quando as concluir. A Microsoft fornece uma classe de modelo que manipula o tempo de vida automaticamente. Por exemplo, se quiser um ponteiro inteligente para uma interface XML, você poderá escrever algo assim:  

```  
Pointer<IXMLDOMNode> pNewChild  
pXmlDom->CreateNode(NODE_ELEMENT, L"MyElement", L"", &pNewChild);  
```  

 A primeira linha define o ponteiro inteligente. A segunda linha mostra a recuperação de um ponteiro inteligente por meio de outra chamada. O operador **&** sempre liberará uma interface existente se contiver uma e retornará o endereço do ponteiro interno. Depois de recuperar um ponteiro como esse, a instância **Pointer** chamará **Release** para você quando a variável sair do escopo. A Microsoft recomenda que você use ponteiros inteligentes em vez de chamar **AddRef** e **Release** manualmente.  

 Além disso, a classe de ponteiro inteligente **Ponteiro** chama **QueryInterface** para recuperar outras instâncias para você. Por exemplo, quando o Registro de fábrica cria uma instância de um componente, ele tem um código como este:  

```  
PWizardComponent pComp = pUnknown;  
if (pComp != nullptr)  
    pComp->SetContainer(m_pContainer);  
```  

 A primeira linha chama **QueryInterface** nos bastidores para solicitar a interface **IWizardComponent**. O ponteiro inteligente resultante será igual a **nullptr** se o componente não for compatível com essa interface.  

####  <a name="PUnkownClass"></a> Classe PUnknown  
 Essa classe é um ponteiro inteligente especificamente para a interface **IUnknown**. Para todas as outras interfaces, use a classe de modelo **Pointer**.  

####  <a name="StringUtilHelperClass"></a> Classe auxiliar StringUtil  
 Essa classe é definida em Utilities.h e oferece métodos auxiliares que tornam mais fácil trabalhar com cadeias de caracteres:  

```  
static inline int CompareIgnore(LPCWSTR first, LPCWSTR second)  
```  

 Esse método compara duas cadeias de caracteres e, ao mesmo tempo, ignora maiúsculas e minúsculas (consulte a Tabela 9).  

### <a name="table-9-stringutil-helper-class"></a>Tabela 9. Classe auxiliar StringUtil  

|**Retorna**|**Descrição**|  
|-|-|  
|**0**|As cadeias de caracteres coincidem, ignorando maiúsculas e minúsculas|  
|**<0**|Primeiro < segundo|  
|**>0**|Primeiro > segundo|  

 Veja um exemplo:  

```  
static inline std::wstring Format(LPCWSTR input, int index, LPCWSTR value)  
static inline std::wstring Format(LPCWSTR input, int index, DWORD value)  
```  

 Esses métodos são um pouco parecidos com os métodos **Format** do Microsoft .NET no sentido em que são parâmetros na forma de **{0}**. No entanto, eles não realizam nenhuma formatação da entrada – apenas substituição:  

```  
static inline std::wstring Printf(std::wstring format, I val)  
static inline std::wstring Printf(std::wstring format, I val1, J val2)  
static inline std::wstring Printf(std::wstring format, I val1, J val2, K val3)  
static inline std::wstring Printf(std::wstring format, I val1, J val2, K val3, L val4)  
```  

 Esses são wrappers em torno de **StringCchPrintf** que retornam um **wstring**; assim, não é necessário alocar memória para cadeias de caracteres ou buffers.  

####  <a name="SubInterfaceTemplateClass"></a> Classe de modelo SubInterface  
 Essa classe base torna mais fácil implementar um componente compatível com uma interface herdada de outra interface. Por exemplo, a interface **ICheckBox** é herdada de **IControl**. É assim que essa classe é usada para definir o **CheckBoxWrapper**:  

```  
classCheckBoxWrapper :public SubInterface<IControl, UnknownImpl<ICheckBox> >  
```  

 A interface base é o primeiro parâmetro, enquanto a interface derivada é o segundo.  

####  <a name="UnknownImplTemplateClass"></a> Classe de modelo UnknownImpl  
 Essa classe é definida em UnknownImpl.h e manipula a maioria dos detalhes da criação de um componente COM. Veja um exemplo de como você usaria essa classe base:  

```  
classDirectory :public UnknownImpl<IDirectory>  
```  

 Esse código define uma classe compatível com a interface **IDirectory**.  

####  <a name="WizardComponentTemplateClass"></a> Classe de modelo WizardComponent  
 Essa classe é definida em IWizardComponent.h e é uma classe base útil para criar componentes que precisam acessar os serviços de assistente, como a criação e o registro em log de componentes.  

 Como um exemplo, é assim que o componente **CopyFilesTask** é definido:  

```  
classCopyFilesTask :public WizardComponent<ITask>  
{  
    ...  
```  

 O parâmetro dessa classe de modelo é a interface "principal" que você deseja usar para seu componente, que, no caso de tarefas, é **ITask**. Usar **WizardComponent** significa que o componente é compatível com a interface fornecida (**ITask** neste exemplo) e **IWizardComponent**.  

 Sempre que você usa o Registro de fábrica de classes para criar um novo componente, o Registro chama o método **IWizardComponent->SetContainer** do componente para fornecer acesso de componente aos serviços de assistente.  

####  <a name="WizardPageImplTemplateClass"></a> Classe de modelo WizardPageImpl  
 Use essa classe como a classe base para suas páginas personalizadas – por exemplo:  

```  
class LocationPage :public WizardPageImpl<IDD_LOCATION_PAGE>  
```  

 O parâmetro é a ID de recurso para seu modelo de caixa de diálogo.  

###  <a name="WizardPageInterfaces"></a> Interfaces da página de assistente  
 O Assistente de UDI usa interfaces para acessar os diferentes controles em sua página. Na página, use a função **GetControlWrapper** para recuperar um wrapper de controle. Veja um exemplo:  

```  
PStaticText pFormat;  
GetControlWrapper(View(), IDC_CHECK_PARTITION, CONTROL_STATIC_TEXT, &pFormat);  
```  

 Aqui, **PStaticText** é um ponteiro inteligente para a interface **IStaticText**. Os ponteiros inteligentes chamam automaticamente o método **Release()** COM quando eles saem do escopo ou quando você passa o endereço de uma variável (como **&pFormat**) para um método.  

#### <a name="iadhelper-interface"></a>Interface IADHelper  

```  
__interfaceIADHelper : IUnknown  
{  
    HRESULT Init(ILogger *pLogger);  
    HRESULT ValidLogon(LPCTSTR userName, LPCTSTR password, LPCTSTR domain);  
    HRESULT HasAccess(LPCTSTR username, LPCTSTR password, LPCTSTR domain, LPCTSTR computerName, LPCTSTR accountDomain);  
};  

```  

##### <a name="hresult-initilogger-plogger"></a>HRESULT Init(ILogger \*pLogger)  
 Inicialize esse componente, passando-o para o agente para que ele possa registrar informações.  

##### <a name="hresultvalidlogonlpctstr-username-lpctstr-password-lpctstr-domain"></a>HRESULTValidLogon(LPCTSTR userName, LPCTSTR password, LPCTSTR domain)  
 Esse método verifica se um conjunto de credenciais é válido, conforme mostrado na Tabela 10.  

### <a name="table-10-hresultvalidlogon"></a>Tabela 10. HResultValidLogon  

|**HResult**|**Descrição**|  
|-|-|  
|S_OK|As credenciais são válidas|  
|S_FALSE|As credenciais não são válidas|  
|E_FAIL|Não foi possível localizar o controlador de domínio; verifique os logs para obter detalhes|  

##### <a name="hresult-hasaccesslpctstr-username-lpctstr-password-lpctstr-domain-lpctstr-computername-lpctstr-accountdomain"></a>HRESULT HasAccess(LPCTSTR username, LPCTSTR password, LPCTSTR domain, LPCTSTR computerName, LPCTSTR accountDomain)  
 Esse método verifica se um conjunto de credenciais tem acesso de leitura/gravação para o objeto de computador no AD DS, conforme mostrado na Tabela 11.  

### <a name="table-11-hresult-hasaccess"></a>Tabela 11. HResult HasAccess  

|**HRESULT**|**Descrição**|  
|-|-|  
|S_OK|O usuário tem acesso|  
|E_FAIL|O usuário não tem acesso. Verifique o arquivo de log para obter informações adicionais.|  

#### <a name="ibackgroundtask-interface"></a>Interface IBackgroundTask  

```  
__interface IBackgroundTask : IUnknown  
{  
    HRESULT Init(ITask *pTask, int id, IBackgroundCallback *pCallback);  
    void Start(void);  
    BOOL Running(void);  
    HRESULT Wait(DWORD waitMilliseconds);  
    HRESULT Terminate(DWORD exitCode);  
    HRESULT GetExitCode(LPDWORD pCode, HRESULT *pHresult);  
    HRESULT Close(void);  
};  
```  

##### <a name="overview"></a>Visão geral  
 A página **Andamento** usa essa classe para executar tarefas em um thread separado. Também será possível usar essa classe sempre que você desejar executar operações em um thread separado. *Tarefas* são qualquer classe compatível com a interface **ITask**.  

 Essa interface é implementada pelo componente **ID_BackgroundTask** ("Microsoft.Wizard.BackgroundTask"), definido na interface IBackgroundTask.h.  

##### <a name="hresult-inititask-ptask-int-id-ibackgroundcallback-pcallback"></a>HRESULT Init(ITask \*pTask, int id, IBackgroundCallback \*pCallback)  
 Essa interface inicializa o componente, conforme mostrado na Tabela 12.  

### <a name="table-12-hresult-init"></a>Tabela 12. HRESULT Init  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**pTask**|O ponteiro para a classe que contém o código que você deseja executar em outro thread|  
|**Id**|Um número que você pode usar no método **Finished** de retorno de chamada para informar qual tarefa concluiu a execução; útil se você iniciar várias tarefas com o mesmo método de retorno de chamada|  
|**pCallback**|Uma classe que implementa o método **Finished**, chamado sempre que uma tarefa conclui a execução; a chamada para o método **Finished** estará no thread em segundo plano, não no thread da interface do usuário|  

##### <a name="void-startvoid"></a>void Start(void)  
 Esse método inicia a tarefa em um thread em segundo plano e retorna os elementos mostrados na Tabela 13.  

### <a name="table-13-return-background-thread"></a>Tabela 13. Retornar thread em segundo plano  

|**Retorna**|**Descrição**|  
|-|-|  
|**E_INVALIDARG**|A tarefa já está em execução, portanto, não é possível iniciá-la agora.|  
|**E_FAIL**|Houve um problema ao iniciar o thread.|  
|**S_OK**|O thread foi iniciado.|  

##### <a name="bool-running"></a>BOOL Running()  
 Esse método retornará TRUE se a tarefa em segundo plano estiver em execução no momento, e FALSE se não estiver em execução.  

##### <a name="hresult-waitdword-waitmilliseconds"></a>HRESULT Wait(DWORD waitMilliseconds)  
 Esse método aguarda até que a execução do thread seja interrompida ou até que o número de milissegundos tenha decorrido.  

##### <a name="hresult-terminatedword-exitcode"></a>HRESULT Terminate(DWORD exitCode)  
 Esse método elimina o thread que está sendo executado (consulte a Tabela 14 e a Tabela 15). Esse processo poderá demorar um curto período de tempo para ser concluído depois que esse método retornar.  

### <a name="table-14-hresult-terminate-exit-code"></a>Tabela 14. Código de saída para encerramento de HRESULT  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**exitCode**|O código de saída que será enviado ao método de retorno de chamada Finished, que também estará disponível no método **GetExitCode**.|  

### <a name="table-15-termination-codes"></a>Tabela 15. Códigos de encerramento  

|**Retorna**|**Descrição**|  
|-|-|  
|**E_FAIL**|Falha na chamada de encerramento.|  
|**S_OK**|A solicitação para encerrar o thread foi bem-sucedida.|  

##### <a name="hresult-getexitcodelpdword-pcode-hresult-phresult"></a>HRESULT GetExitCode(LPDWORD pCode, HRESULT \*pHresult)  
 Use esse método para obter os resultados da execução da tarefa no thread em segundo plano (consulte a Tabela 16).  

### <a name="table-16-result-codes"></a>Tabela 16. Código do resultado  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**pCode**|Ponteiro para um **DWORD** que será definido no retorno ou **nullptr** se o valor retornado não for necessário. Na saída, esse parâmetro será definido como **STILL_ACTIVE** se o thread estiver em execução, o código tiver sido retornado pelo método **Execute** da tarefa ou o valor tiver sido passado para o método **Terminate** se você tiver cancelado esse método.|  
|**pHresult**|Ponteiro para um **HRESULT** que será definido no retorno ou **nullptr** se o valor **HRESULT** não for necessário.|  

##### <a name="hresult-closevoid"></a>HRESULT Close(void)  
 Esse método libera o thread em segundo plano. Ele retornará **E_INVALIDARG** se o thread estiver em execução no momento e **S_OK**, caso contrário.  

#### <a name="icheckbox-interface"></a>Interface ICheckBox  

```  
__interface ICheckBox : IControl  
{  
    void Check(BOOL check);  
    BOOL IsButtonChecked();  
};  
```  

##### <a name="void-checkbool-check"></a>void Check(BOOL check)  
 Defina o estado de ativação da caixa de seleção. Quando o método for TRUE, a caixa de seleção estará selecionada; quando o método for FALSE, a caixa de seleção estará desmarcada.  

##### <a name="bool-isbuttonchecked"></a>BOOL IsButtonChecked()  
 Esse método relata o estado de ativação atual de uma caixa de seleção.  

#### <a name="icombobox-interface"></a>Interface IComboBox  

```  
__interface IComboBox : IControl  
{  
    HRESULT Bind([in] IBindableList *pList);  
    HRESULT Select(int index);  
    int Selected(void);  
    void Add([in] LPCTSTR caption);  
    HRESULT GetText([out, retval] LPBSTR pText);  
    void Clear();  
};  
```  

##### <a name="overview"></a>Visão geral  
 Esta interface é implementada pelo componente **CheckBoxWrapper**. Recupere uma instância desse componente usando a função auxiliar **GetControlWrapper** com o tipo **CONTROL_COMBO_BOX**.  

##### <a name="hresult-bindin-ibindablelist-plist"></a>HRESULT Bind([in] IBindableList \*pList)  
 Use esse método quando você tiver uma fonte de dados que implemente a interface **IBindableList**. A caixa de listagem inicializa o conteúdo com as legendas dessa lista.  

##### <a name="hresult-selectint-index"></a>HRESULT Select(int index)  
 Selecione o item na caixa de combinação no índice.  

##### <a name="int-selectedvoid"></a>int Selected(void)  
 Esse método retornará o índice do item selecionado ou **-1** se nada estiver selecionado.  

##### <a name="void-addin-lpctstr-caption"></a>void Add([in] LPCTSTR caption)  
 Adicione manualmente um item à caixa de combinação.  

##### <a name="hresult-gettextout-retval-lpbstr-ptext"></a>HRESULT GetText([out, retval] LPBSTR pText)  
 Recupere a cadeia de caracteres do item selecionado no momento na caixa de combinação.  

##### <a name="void-clear"></a>void Clear()  
 Remova todos os itens da caixa de combinação.  

#### <a name="icontrol-interface"></a>Interface IControl  

```  
__interface IControl : IUnknown  
{  
    HRESULT SetEnable(BOOL enable);  
    BOOL IsEnabled(void);  
    HRESULT SetVisible(BOOL visible);  
};  
```  

##### <a name="overview"></a>Visão geral  
 Esta interface é implementada pelo componente **ControlWrapper**. Recupere uma instância desse componente usando a função auxiliar **GetControlWrapper** com o tipo **CONTROL_GENERIC**.  

##### <a name="hresult-setenablebool-enable"></a>HRESULT SetEnable(BOOL enable)  
 Habilite ou desabilite o controle.  

##### <a name="bool-isenabledvoid"></a>BOOL IsEnabled(void)  
 Retornará TRUE se o controle estiver habilitado; caso contrário, FALSE.  

##### <a name="hresult-setvisiblebool-visible"></a>HRESULT SetVisible(BOOL visible)  
 Mostre ou oculte o controle.  

#### <a name="icpuinfo-interface"></a>Interface ICpuInfo  

```  
__interface ICpuInfo : IUnknown  
{  
    BOOL Is64Bit(void);  
};  
```  

##### <a name="overview"></a>Visão geral  
 Obtenha essa interface criando um novo componente **ID_CpuInfo**. O único método informa se a CPU tem 32 ou 64 bits. Observe que, se você tiver um sistema operacional de 32 bits em um computador de 64 bits, esse método retornará TRUE, porque ele está apenas informando a largura da CPU (não o sistema operacional).  

##### <a name="idirectory-interface"></a>Interface IDirectory  

```  
__interface IDirectory : IUnknown  
{  
    BOOL FileExists(LPCWSTR name);  
    BOOL FindFirst([in] LPCWSTR name);  
    HRESULT FoundName([out, retval] LPBSTR name);  
    DWORD FoundAttributes(void);  
    BOOL FindNext(void);  
    void FinishFind(void);  
};  
```  

###### <a name="overview"></a>Visão geral  
 O componente **Directory**, que você cria usando **ID_Directory**, fornece uma fachada para trabalhar com diretórios no sistema de arquivos.  

###### <a name="bool-fileexistslpcwstr-name"></a>BOOL FileExists(LPCWSTR name)  
 Esse método retornará TRUE se existir um arquivo com o nome fornecido.  

###### <a name="bool-findfirstin-lpcwstr-name"></a>BOOL FindFirst([in] LPCWSTR name)  
 Esse método localiza uma primeira correspondência para o nome fornecido. Ele dá suporte a caracteres curinga e retorna nomes de arquivo e de diretório. O método retornará TRUE se uma correspondência tiver sido encontrada; caso contrário, FALSE.  

###### <a name="hresult-foundnameout-retval-lpbstr-name"></a>HRESULT FoundName([out, retval] LPBSTR name)  
 Esse método recupera o nome do arquivo encontrado com uma chamada para **FindFirst** ou **FindNext**.  

###### <a name="dword-foundattributesvoid"></a>DWORD FoundAttributes(void)  
 Esse método retorna o atributo para o diretório ou arquivo encontrado mais recente. É possível usar o código da seguinte maneira para testar se ele é um diretório:  

```  
pDirectory->FoundAttributes() & FILE_ATTRIBUTE_DIRECTORY  
```  

###### <a name="bool-findnextvoid"></a>BOOL FindNext(void)  
 Encontre o próximo. Esse método retornará TRUE se outra correspondência tiver sido encontrada; caso contrário, FALSE.  

###### <a name="void-finishfindvoid"></a>void FinishFind(void)  
 Esse método libera recursos usados para a operação Localizar.  

#### <a name="idomainjoinvalidator-interface"></a>Interface IDomainJoinValidator  

```  
__interface IDomainJoinValidator : IUnknown  
{  
    HRESULT Init(ILogger *pLogger, IWizardPageContainer *pContainer, IStaticText *pUsername, IStaticText *pPassword, IStaticText *pComputerName);  
    HRESULT IsUsernameValid(LPCWSTR domainName);  
    BOOL CanModifyComputerAdEntry(LPCWSTR domainName);  
};  
```  

##### <a name="overview"></a>Visão geral  
 Obtenha uma instância dessa interface usando o valor **ID_DomainJoinValidator** para a função de modelo **CreateInstance**.  

##### <a name="hresult-initilogger-plogger-iwizardpagecontainer-pcontainer-istatictext-pusername-istatictext-ppassword-istatictext-pcomputername"></a>HRESULT Init(ILogger \*pLogger, IWizardPageContainer \*pContainer, IStaticText \*pUsername, IStaticText \*pPassword, IStaticText \*pComputerName)  
 Inicialize a instância, conforme mostrado na Tabela 17.  

### <a name="table-17-hresult-init---instance-initialization"></a>Tabela 17. HRESULT Init – Inicialização de instância  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**pLogger**|A instância do agente, que está disponível para sua página por meio do método **Logger** da página|  
|**pContainer**|Passa os resultados do método **Container** da sua página|  
|**pUsername**|A caixa de texto que contém o nome de usuário a ser validado|  
|**pPassword**|A caixa de texto que contém a senha a ser validada|  
|**PComputerName**|A caixa de texto que contém o nome do computador que eventualmente será ingressado no domínio|  

##### <a name="hresult-isusernamevalidlpcwstr-domainname"></a>HRESULT IsUsernameValid(LPCWSTR domainName)  
 Esse método usa o método **IADHelper->ValidLogon** para fazer o trabalho. Consulte esse método para obter detalhes.  

##### <a name="bool-canmodifycomputeradentrylpcwstr-domainname"></a>BOOL CanModifyComputerAdEntry(LPCWSTR domainName)  
 Verifique se o usuário tem direitos para modificar a entrada do computador. A maioria do trabalho é realizada por **IADHelper->HasAccess**. Se esse método retornar FALSE, verifique os detalhes no arquivo de log.  

#### <a name="idrivelist-interface"></a>Interface IDriveList  

```  
__interface IDriveList : IUnknown  
{  
    HRESULT Init(IWmiRepository *pWmi);  
    HRESULT SetWhereClause(LPCTSTR whereClause);  
    HRESULT SetMinimumDriveSize(__int64 size);  
    HRESULT Update(void);  
    HRESULT AddProperty(ENUM_DISK_QUERY_SECTION section, LPCTSTR propName, LPCTSTR propNameReturned);  

    size_t Count(void);  
    HRESULT GetProperty(size_t index, LPCTSTR propName,  LPVARIANT value);  
    HRESULT GetCaption(size_t index,  LPBSTR pCaption);  
}  
```  

##### <a name="hresult-initiwmirepository-pwmi"></a>HRESULT Init(IWmiRepository \*pWmi)  
 Chame esse método antes de chamar quaisquer outros métodos. Será necessário criar um novo **WmiRepository** antes de chamar esse método.  

##### <a name="hresult-setwhereclauselpctstr-whereclause"></a>HRESULT SetWhereClause(LPCTSTR whereClause)  
 Esse método permite adicionar texto que será exibido como uma cláusula "where" na consulta. Por exemplo, a linha a seguir retorna apenas unidades USB:  

```  
pDrives->SetWhereClause(L"WHERE InterfaceType='USB'");  
```  

##### <a name="hresult-setminimumdrivesizeint64-size"></a>HRESULT SetMinimumDriveSize(\__int64 size)  
 Defina o tamanho da unidade de minimização, em bytes, para unidades que serão retornadas da consulta.  

##### <a name="hresult-updatevoid"></a>HRESULT Update(void)  
 Execute o teste. A lista de unidades disponível após chamar esse método é classificada pela letra da unidade.  

##### <a name="hresult-addpropertyenumdiskquerysection-section-lpctstr-propname-lpctstr-propnamereturned"></a>HRESULT AddProperty(ENUM_DISK_QUERY_SECTION section, LPCTSTR propName, LPCTSTR propNameReturned)  
 Esse método adiciona os nomes de propriedades adicionais que você deseja tornar disponíveis nos resultados da consulta. Chame esse método antes de chamar **Update**. A Tabela 18 mostra três propriedades úteis.  

### <a name="table-18-hresult-addproperty-useful-properties"></a>Tabela 18. HRESULT AddProperty: propriedades úteis  

|**Seção**|**Propriedade**|**Descrição**|  
|-|-|-|  
|**DISKQUERY_LOGICALDISK**|**Tamanho**|O tamanho, em bytes, representado como uma cadeia de caracteres|  
|**DISKQUERY_DISKPARTITION**|**DiskIndex**|O número de disco como um inteiro, começando com 0|  
|**DISKQUERY_LOGICALDISK**|**VolumeName**|O rótulo do volume|  

##### <a name="sizet-countvoid"></a>size_t Count(void)  
 O número de registros retornados pela consulta. Chame **Update** antes de chamar esse método.  

##### <a name="hresult-getpropertysizet-index-lpctstr-propname--lpvariant-value"></a>HRESULT GetProperty(size_t index, LPCTSTR propName,  LPVARIANT value)  
 Esse método recupera o valor de uma propriedade dos resultados da consulta, conforme mostrado na Tabela 19.  

### <a name="table-19-hresult-getproperty"></a>Tabela 19. HRESULT GetProperty  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**Index**|Índice de base zero para o registro de resultados|  
|**propName**|Nome da propriedade, como "Tamanho"|  
|**Valor**|No retorno, esse parâmetro contém um valor variant da propriedade|  

##### <a name="hresult-getcaptionsizet-index--lpbstr-pcaption"></a>HRESULT GetCaption(size_t index,  LPBSTR pCaption)  
 Esse método recupera a legenda de um registro igual à propriedade **Caption**.  

#### <a name="iimagelist-interface"></a>Interface IImageList  

```  
__interface IImageList  
{  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    HImageList GetImageList(void);  
    int AddImage(HInstance hInstance, int resourceId);  
};  
```  

##### <a name="overview"></a>Visão geral  
 Esta interface é implementada pelo componente **ImageList**. Recupere uma instância desse componente da interface **IListView**.  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 Crie uma nova lista de imagens, que este componente gerencia. Chame esse método apenas uma vez.  

##### <a name="himagelist-getimagelistvoid"></a>HImageList GetImageList(void)  
 Esse método retorna o identificador da lista de imagens caso seja necessário executar outras operações na lista de imagens.  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HInstance hInstance, int resourceId)  
 Adicione uma nova imagem à lista de imagens de um recurso, conforme mostrado na Tabela 20.  

### <a name="table-20-hresult-iimagelist-interface"></a>Tabela 20. Interface HRESULT IImageList  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**hInstance**|Identificador de instância do módulo que contém o recurso de bitmap|  
|**resourceId**|A ID do recurso a ser carregada para a lista de imagens|  

#### <a name="ilistview-interface"></a>Interface IListView  

```  
__interface IListView : IControl  
{  
    int AddItem([in] LPCTSTR text);  
    int AddColumn(int width, [in] LPCTSTR text);  
    HRESULT SetSubItem(int index, int column, [in] LPCTSTR text);  
    int GetWidth(void);  
    void SetExtendedStyle(DWORD style);  
    int GetSelectedItem(void);  
    HRESULT SelectItem(int index);  
    BOOL IsItemChecked(int index);  
    int GetItemCount(void);  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    int AddImage(HINSTANCE hInstance, int resourceId);  
    HRESULT SetImage(int index, int imageIndex);  
    HRESULT Clear(void);  
};  
```  

##### <a name="overview"></a>Visão geral  
 Esta interface é implementada pelo componente **ControlWrapper**. Recupere uma instância desse componente usando a função auxiliar **GetControlWrapper** com o tipo **CONTROL_LIST_VIEW**.  

##### <a name="int-additemin-lpctstr-text"></a>int AddItem([in] LPCTSTR text)  
 Adicione uma nova linha à caixa de listagem. O método retorna o índice do item recém-adicionado.  

##### <a name="int-addcolumnint-width-in-lpctstr-text"></a>int AddColumn(int width, [in] LPCTSTR text)  
 Adicione uma nova coluna à exibição de lista.  

##### <a name="hresult-setsubitemint-index-int-column-in-lpctstr-text"></a>HRESULT SetSubItem(int index, int column, [in] LPCTSTR text)  
 Defina o texto em uma coluna diferente da primeira coluna da caixa de listagem, conforme mostrado na Tabela 21.  

### <a name="table-21-hresult-setsubitem"></a>Tabela 21. HRESULT SetSubItem  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**index**|O índice do item de lista que você deseja modificar|  
|**column**|O índice da coluna que você deseja atualizar; a primeira coluna é definida com **AddItem**, as colunas dois e as seguintes são definidas com esse método|  
|**text**|A cadeia de caracteres a ser mostrada na coluna|  

##### <a name="int-getwidthvoid"></a>int GetWidth(void)  
 Esse método retorna a largura de toda a caixa de texto.  

##### <a name="void-setextendedstyledword-style"></a>void SetExtendedStyle(DWORD style)  
 Esse método permite definir estilos estendidos na caixa de listagem, por exemplo:  

```  
m_pList->SetExtendedStyle(LVS_EX_FULLROWSELECT);  
```  

##### <a name="int-getselecteditemvoid"></a>int GetSelectedItem(void)  
 Esse método retorna o índice do item de exibição de lista selecionado no momento.  

##### <a name="hresult-selectitemint-index"></a>HRESULT SelectItem(int index)  
 Defina o item selecionado na lista como este índice.  

##### <a name="bool-isitemcheckedint-index"></a>BOOL IsItemChecked(int index)  
 Esse método retornará TRUE se um item na lista estiver selecionado. Esse método requer que você chame **SetExtendedStyle** para definir o estilo da caixa de seleção.  

##### <a name="int-getitemcountvoid"></a>int GetItemCount(void)  
 Esse método retorna o número de itens na exibição de lista.  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 Crie uma nova lista de imagens e anexe-a à exibição de lista.  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HINSTANCE hInstance, int resourceId)  
 Adicione uma imagem à lista de imagens da exibição de lista. É necessário chamar **CreateImageList** primeiro.  

##### <a name="hresult-setimageint-index-int-imageindex"></a>HRESULT SetImage(int index, int imageIndex)  
 Defina a imagem que será mostrada à esquerda para um item de exibição de lista específico.  

##### <a name="hresult-clearvoid"></a>HRESULT Clear(void)  
 Remova todos os itens da exibição de lista.  

#### <a name="iprogressbar-interface"></a>Interface IProgressBar  

```  
__interface IProgressBar : IControl  
{  
    HRESULT SetPercentage(int position);  
    int GetPercentage(void);  
};  
```  

##### <a name="overview"></a>Visão geral  
 Esta interface é implementada pelo componente **ProgressBarWrapper**. Recupere uma instância desse componente usando a função auxiliar **GetControlWrapper** com o tipo **CONTROL_PROGRESS_BAR**.  

##### <a name="hresult-setpercentageint-position"></a>HRESULT SetPercentage(int position)  
 Defina a posição da barra de progresso usando um número entre 0 e 100. Por padrão, as novas barras de progresso do Win32® têm um alcance máximo de 100.  

##### <a name="int-getpercentagevoid"></a>int GetPercentage(void)  
 Esse método retorna a posição atual da barra de progresso.  

#### <a name="iradiobutton-interface"></a>Interface IRadioButton  

```  
__interface IRadioButton : IControl  
{  
public:  
    void SetGroup(int firstId, int lastId);  
    void CheckRadio(int id);  
    BOOL IsButtonChecked(int id);  
    void EnableRadio(int id, BOOL enable);  
};  
```  

##### <a name="overview"></a>Visão geral  
 Essa interface é implementada pelo componente **RadioButtonWrapper**. Recupere uma instância desse componente usando a função auxiliar **GetControlWrapper** com o tipo **CONTROL_RADIO_BUTTON**.  

##### <a name="void-setgroupint-firstid-int-lastid"></a>void SetGroup(int firstId, int lastId)  
 Forneça o wrapper com o intervalo de botões de opção que devem ser tratados como um grupo. Chame esse método antes de chamar **CheckRadio**.  

##### <a name="void-checkradioint-id"></a>void CheckRadio(int id)  
 Defina o botão de opção específico para ser o único botão no grupo de botões de opção selecionados. Chame **SetGroup** antes de chamar esse método.  

##### <a name="bool-isbuttoncheckedint-id"></a>BOOL IsButtonChecked(int id)  
 Esse método retornará TRUE se o botão de opção estiver selecionado no momento; caso contrário, FALSE.  

##### <a name="void-enableradioint-id-bool-enable"></a>void EnableRadio(int id, BOOL enable)  
 Esse método habilita ou desabilita um botão de opção.  

#### <a name="istatictext-interface"></a>Interface IStaticText  

```  
__interface IStaticText : IControl  
{  
    HRESULT SetText([in] LPCTSTR pText);  
    HRESULT GetText([out, retval] LPBSTR pText);  
};  
```  

##### <a name="overview"></a>Visão geral  
 Essa interface é implementada pelo componente **StaticTextWrapper**. Recupere uma instância desse componente usando a função auxiliar **GetControlWrapper** com o tipo **CONTROL_STATIC_TEXT**.  

##### <a name="hresult-settextin-lpctstr-ptext"></a>HRESULT SetText([in] LPCTSTR pText)  
 Defina o texto do controle.  

##### <a name="hresult-gettextout-retval-lpbstr-ptext"></a>HRESULT GetText([out, retval] LPBSTR pText)  
 Esse método retorna o valor atual do texto do controle.  

####  <a name="ITaskinterface"></a> Interface ITask  

```  
__interface IControl : IUnknown  
{  
    HRESULT Init(IStringProperties *pProperties, ISettingsProperties *pTaskSettings);  
    HRESULT Execute(LPDWORD pReturnCode);  
};  
```  

 Implemente essa interface se desejar que seu componente esteja disponível como uma tarefa na página de simulação ou se desejar usar o componente **BackgroundTask** para realizar o trabalho em um thread em segundo plano.  

 Estes são os componentes que implementam a interface **ITask**:  

-   ID_ShellExecuteTask, L"Microsoft.Wizard.ShellExecuteTask"  

-   ID_CopyFilesTask, L"Microsoft.Wizard.CopyFilesTask"  

-   ID_ACPowerTask, L"Microsoft.OSDRefresh.ACPowerTask"  

-   ID_WiredNetworkTask, L"Microsoft.SharedPages.WiredNetworkTask"  

##### <a name="init"></a>Init  

```  
HRESULT Init(IStringProperties *pProperties, ISettingsProperties *pTaskSettings)  
```  

 Se você estiver escrevendo uma tarefa para a página de simulação, chame esse método para iniciá-la. O arquivo .config contém um XML que pode ter esta aparência:  

```  
<Task DisplayName="Check Windows Scripting Host" Type="Microsoft.Wizard.ShellExecuteTask">  
  <Setter Property="filename">%windir%\system32\cscript.exe</Setter>  
  <Setter Property="parameters">Preflight\OSDCheckWSH.vbs</Setter>  
  <Setter Property="BitmapFilename">images\WinScriptHost.bmp</Setter>  
  <ExitCodes>  
    <ExitCode State="Success" Type="0" Value="0" Text="" />  
    <ExitCode State="Error" Type="-1" Value="*" Text="Windows Scripting Host not installed." />  
  </ExitCodes>  
</Task>  
```  

 O parâmetro **pProperties** fornece acesso para aos três valores setter, enquanto o parâmetro **pTaskSettings** fornece acesso ao elemento **Task** e elementos filho. A maioria das tarefas só precisam ler dados do parâmetro **pProperties**.  

#####  <a name="Execute"></a> Execute  

```  
HRESULT Execute(LPDWORD pReturnCode)  
```  

 É aqui que você escreve o código que executa a tarefa. Esse método deverá retornar **S_OK** se não houver erros, e poderá retornar outro **HRESULT** se tiver ocorrido um erro durante a execução da tarefa. Valores diferentes de **S_OK** que esse método retorna serão correspondidos até elementos <Error\> na seção <ExitCodes\> se você estiver usando a página de simulação.  

 O parâmetro **pReturnCode** deve ser atualizado comum número que informa o estado da tarefa. Esses valores são correspondidos por páginas de simulação para elementos <ExitCode\>.  

#### <a name="itreeview-interface"></a>Interface ITreeView  

```  
__interface ITreeView : IControl  
{  
    void EnableCheckboxes(void);  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    int AddImage(HINSTANCE hInstance, int resourceId);  

    HTREEITEM AddItem(LPCTSTR text, HTREEITEM hParent = NULL);  
    void SetImage(HTREEITEM item, int image, int expandImage);  

    void Clear(void);  
    BOOL SetFirstVisible(HTREEITEM item);  
    BOOL SelectItem(HTREEITEM item);  
    void CheckItem(HTREEITEM item, UINT checkState);  
    HTREEITEM SelectedItem(void);  
    int SetItemHeight(SHORT height);  
    HRESULT EnableItem(HTREEITEM item, BOOL enable);  
    void Expand(HTREEITEM hItem, BOOL expand);  

    HTREEITEM GetChild(HTREEITEM hParent);  
    HTREEITEM GetParent(HTREEITEM hNode);  
    HTREEITEM GetNextItem(HTREEITEM hPrevious);  

    UINT IsChecked(HTREEITEM item);  
    BOOL IsEnabled(HTREEITEM item);  

    INT_PTR CommonControlEvent(WORD controlId, void* pInfo, BOOL *pCancel);  
    HRESULT SetEventHandler(ITreeViewEvent *pEventHandler);  

    void SetSelectedBackColor(COLORREF color);  
};  
```  

##### <a name="overview"></a>Visão geral  
 Esta interface é implementada pelo componente **TreeViewWrapper**. Recupere uma instância desse componente usando a função auxiliar **GetControlWrapper** com o tipo **CONTROL_TREE_VIEW**.  

##### <a name="void-enablecheckboxesvoid"></a>void EnableCheckboxes(void)  
 Esse método ativa caixas de seleção no controle de exibição de árvore definindo o estilo **TVS_CHECKBOXES**.  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 Adicione uma nova lista de imagens ao controle de exibição de árvore. O parâmetro **flags** é passado na chamada para a função **ImageList_Create** do Win32.  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HINSTANCE hInstance, int resourceId)  
 Adicione uma imagem à lista de imagens de um recurso (**resourceId**) no módulo com o identificador de instância **hInstance**.  

##### <a name="htreeitem-additemlpctstr-text-htreeitem-hparent--null"></a>HTREEITEM AddItem(LPCTSTR text, HTREEITEM hParent = NULL)  
 Adicione um nó ao modo de exibição de árvore. O novo nó será adicionado no nível superior se **hParent** for NULL. Caso contrário, forneça o identificador para o item pai ao qual você deseja que o novo item seja adicionado. Esse método retorna o identificador para o novo item.  

##### <a name="void-setimagehtreeitem-item-int-image-int-expandimage"></a>void SetImage(HTREEITEM item, int image, int expandImage)  
 Defina a imagem a ser usada para um item de modo de exibição de árvore. É possível definir a imagem normal e a expandida.  

##### <a name="void-clearvoid"></a>void Clear(void)  
 Remova todos os itens do modo de exibição de árvore.  

##### <a name="bool-setfirstvisiblehtreeitem-item"></a>BOOL SetFirstVisible(HTREEITEM item)  
 Certifique-se de que o item de modo de exibição de árvore está visível. O modo de exibição de árvore rolará se necessário para tornar este item visível.  

##### <a name="bool-selectitemhtreeitem-item"></a>BOOL SelectItem(HTREEITEM item)  
 Defina o item selecionado no momento como o item fornecido. É possível chamar **SetFirstVisible** depois disso para garantir que o item recém-selecionado está visível.  

##### <a name="void-checkitemhtreeitem-item-uint-checkstate"></a>void CheckItem(HTREEITEM item, UINT checkState)  
 Basicamente, esse método define a imagem que será mostrada para a caixa de seleção no modo de exibição de árvore. Essas imagens estão em um controle **ImageList** separado gerenciado pelo modo de exibição de árvore. Por padrão, esta lista de imagens contém três imagens, mostradas na Tabela 22.  

### <a name="table-22void-checkitem-image-list-default"></a>Tabela 22.void CheckItem Image List Default  

|**checkState**|**Descrição**|  
|-|-|  
|**0**|Em Branco|  
|**1**|Removido|  
|**2**|Selecionada|  

##### <a name="htreeitem-selecteditemvoid"></a>HTREEITEM SelectedItem(void)  
 Esse método retorna o identificador do item de modo de exibição de árvore selecionado no momento.  

##### <a name="int-setitemheightshort-height"></a>int SetItemHeight(SHORT height)  
 Esse método define a altura de todos os itens no controle de exibição de árvore em pixels. Ele retorna a altura anterior em pixels.  

##### <a name="hresult-enableitemhtreeitem-item-bool-enable"></a>HRESULT EnableItem(HTREEITEM item, BOOL enable)  
 Esse método habilita ou desabilita um único item na árvore. Desabilitar um item com filhos não desabilitará os filhos.  

##### <a name="void-expandhtreeitem-hitem-bool-expand"></a>void Expand(HTREEITEM hItem, BOOL expand)  
 Esse método expande ou recolhe um nó na árvore.  

##### <a name="htreeitem-getchildhtreeitem-hparent"></a>HTREEITEM GetChild(HTREEITEM hParent)  
 Esse método retornará o primeiro filho de um item de modo de exibição de árvore ou NULL se não houver nenhum filho.  

##### <a name="htreeitem-getparenthtreeitem-hnode"></a>HTREEITEM GetParent(HTREEITEM hNode)  
 Esse método retornará o identificador do pai de um nó no modo de exibição de árvore ou NULL se o nó estiver no nível superior.  

##### <a name="htreeitem-getnextitemhtreeitem-hprevious"></a>HTREEITEM GetNextItem(HTREEITEM hPrevious)  
 É possível chamar esse método com um identificador retornado por **GetChild** para iterar por meio de todos os filhos de um nó. Esse método retorna o próximo irmão na árvore que compartilha o mesmo pai.  

##### <a name="uint-ischeckedhtreeitem-item"></a>UINT IsChecked(HTREEITEM item)  
 Esse método retornará **0** se o nó do modo de exibição de árvore não estiver selecionado e **1** se estiver.  

##### <a name="bool-isenabledhtreeitem-item"></a>BOOL IsEnabled(HTREEITEM item)  
 Esse método retornará TRUE se o nó do modo de exibição de árvore estiver habilitado; caso contrário, FALSE.  

##### <a name="intptr-commoncontroleventword-controlid-void-pinfo-bool-pcancel"></a>INT_PTR CommonControlEvent(WORD controlId, void* pInfo, BOOL \*pCancel)  
 Esse método é apenas para uso interno.  

##### <a name="hresult-seteventhandleritreeviewevent-peventhandler"></a>HRESULT SetEventHandler(ITreeViewEvent \*pEventHandler)  
 Chame esse método se desejar receber uma notificação quando o item selecionado for alterado ou quando o usuário alterar o estado de ativação de um item de modo de exibição de árvore. É necessário implementar o **ITreeViewEvent** no seu componente para receber esses retornos de chamada.  

##### <a name="void-setselectedbackcolorcolorref-color"></a>void SetSelectedBackColor(COLORREF color)  
 Defina a cor da tela de fundo usada para o item selecionado.  

#### <a name="iwmiiteration-interface"></a>Interface IWmiIteration  

```  
__interface IWmiIterator : IUnknown  
{  
    HRESULT Next(void);  
    HRESULT GetProperty(LPCTSTR propertyName, [out] LPVARIANT pValue);  
};  
```  

##### <a name="overview"></a>Visão geral  
 Geralmente você usa essa interface com **IWmiRepository** ao trabalhar com chamadas WMI. A interface **IWmiIteration** permite que você itere nos valores retornados por uma consulta.  

##### <a name="hresult-nextvoid"></a>HRESULT Next(void)  
 Passe para o próximo item nos resultados da consulta, conforme mostrado na Tabela 23.  

### <a name="table-23-hresult-nextvoid-query-returns"></a>Tabela 23. Retornos de consulta HRESULT Next(void)  

|**HRRESULT**|**Descrição**|  
|-|-|  
|**S_OK**|Passado para o próximo resultado; é possível usar **GetProperty** para recuperar as propriedades desse resultado.|  
|**S_FALSE**|Não há mais itens na lista.|  
|**E_NOT_SET**|Não há nenhum resultado de pesquisa|  

##### <a name="hresult-getpropertylpctstr-propertyname-out-lpvariant-pvalue"></a>HRESULT GetProperty(LPCTSTR propertyName, [out] LPVARIANT pValue)  
 Esse método recupera o valor de uma propriedade do registro de resultado atual, conforme mostrado na Tabela 24 e na Tabela 25.  

### <a name="table-24-hresult-getproperty"></a>Tabela 24. HRESULT GetProperty  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**propertyName**|Nome da propriedade que você deseja recuperar|  
|**pValue**|Aponta para uma estrutura VARIANT que, no retorno, contém o valor da propriedade|  

### <a name="table-25-hresult-getproperty-result"></a>Tabela 25. HRESULT GetProperty Result  

|**HRESULT**|**Descrição**|  
|-|-|  
|**S_OK**|O valor da propriedade foi recuperado.|  
|**WBEM_E_NOT_FOUND**|Não há nenhuma propriedade com o nome.|  
|**E_NOT_VALID_STATE**|Não há nenhum registro atual.|  

> [!NOTE]
>  O método **GetProperty** pode retornar outros códigos de erro WMI diferente dos listados na Tabela 25. Os valores listados são os resultados comuns retornados.  

#### <a name="iwmirepository-interface"></a>Interface IWmiRepository  

```  
__interface IWmiRepository : IUnknown  
{  
    HRESULT SetNamespace(LPCWSTR namespaceName);  
    HRESULT ExecQuery(LPCWSTR query, [out] IWmiIterator **ppIterator);  
};  
```  

##### <a name="overview"></a>Visão geral  
 Essa interface é implementada pelo componente **WmiRepository** (**ID_WmiRepository**).  

##### <a name="hresult-setnamespacelpcwstr-namespacename"></a>HRESULT SetNamespace(LPCWSTR namespaceName)  
 Esse método define o namespace WMI que será usado para a consulta. Chame esse método antes de chamar **ExecQuery**. Se você não chamar esse método, o namespace será root\cimv2. Esse método sempre retorna **S_OK**.  

##### <a name="hresult-execquerylpcwstr-query-out-iwmiiterator-ppiterator"></a>HRESULT ExecQuery(LPCWSTR query, [out] IWmiIterator **ppIterator)  
 Execute uma consulta em relação ao namespace WMI definido com uma chamada para **SetNamespace**, conforme mostrado na Tabela 26 e na Tabela 27.  

### <a name="table-26-hresult-execquery"></a>Tabela 26. HRESULT ExecQuery  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**Query**|A cadeia de caracteres da consulta WMI que você deseja executar|  
|**ppIterator**|Passe um ponteiro para um ponteiro de interface, que, no retorno, será preenchido com uma interface, concedendo acesso aos resultados da consulta|  

### <a name="table-27-hresult-query-result"></a>Tabela 27. Resultado da consulta HRESULT  

|**HRESULT**|**Descrição**|  
|-|-|  
|**S_OK**|Êxito na consulta|  
|**Outros**|Se a consulta não foi bem-sucedida, retorna um **HRESULT** do WMI|  

#### <a name="iformcontroller-interface"></a>Interface IFormController  

```  
__interface IFormController : IUnknown  
{  
    Init(IWizardPageView *pView, IWizardPageContainer *pContainer);  
    SetPageInfo(ISettingsProperties *pPageInfo);  

    Validate(void);  

    AddToGroup(int groupControlId, int controlId);  
    UpdateCheckGroup(int groupControlId);  
    AddValidator(int controlId, IValidator *pValidator, IControl *pCOntrol = 0);  

    AddValidator(int controlId, LPCWSTR validatorId, LPCWSTR message, IValidator **ppValidator = nullptr);  
    DisableValidation(int controlId, BOOL disable);  

    AddField(LPCWSTR fieldName, int controlId, BOOL suppressLog, DialogControlTypes type);  
    AddRadioGroup(LPCWSTR groupName, int radioControlId);  
    EnableRadioGroup(LPCWSTR groupName, BOOL enable);  
    InitFields(IFieldCallback *pFieldCallback = nullptr);  
    SaveFields(IFieldCallback *pFieldCallback = nullptr);  
    BOOL IsFieldDisabled(int controlId);  

    InitSection(LPCWSTR key, LPCWSTR sectionCaption);  
    AddSummaryItem(LPCWSTR first, LPCWSTR second);  
    SuppressLogValue(LPCWSTR tsVariableName);  
    SaveText(int controlId, LPCWSTR tsVariableName, LPCWSTR summaryCaption);  
    LoadText(int controlId, LPCWSTR tsVariableName);  

    void ControlEvent(WORD eventId, WORD controlId);  
    BOOL IsValid(void);  
 };  
```  

##### <a name="overview"></a>Visão geral  
 Cada página do Assistente de UDI tem seu próprio controlador de formulário que implementa essa interface. Use esse controlador para conectar os dados do campo no arquivo XML .config aos controles em sua página. O controlador de formulário manipula muitos detalhes para você.  

#####  <a name="SettingUptheForm"></a> Configurando o formulário  
 Geralmente, configure o controlador de formulário no método **OnWindowCreated** da sua página. Fazer isso geralmente envolve chamar os métodos mostrados na Tabela 28.  

### <a name="table-28-onwindowcreated-method"></a>Tabela 28. OnWindowCreated Method  

|**Método**|**Descrição**|  
|-|-|  
|**Init**|Inicializa o controlador de formulário|  
|**AddField**|Oferece uma conexão entre um campo no arquivo XML .config que é um nome de cadeia de caracteres e um controle na caixa de diálogo da sua página que é uma ID|  
|**AddRadioGroup**|Usado para conectar um botão de opção a um grupo e a um controle em sua caixa de diálogo|  
|**AddToGroup**|Permite que você "defina como filho" controles habilitados ou desabilitados com seu pai ou com base nos quais o botão de opção está selecionado|  
|**InitFields**|Chamado depois de você ter chamado todos os métodos **Add** para configurar o formulário|  
|**Validate**|Executa a validação inicial|  

##### <a name="processing-form-events"></a>Processando eventos de formulário  
 Adicione a seguinte chamada ao seu método **OnControlEvent**:  

```  
Form()->ControlEvent(eventId, controlId);  
```  

 Essa chamada passa eventos para o controlador de formulário para ele poder processar eventos relacionados ao formulário.  

##### <a name="save-form-data"></a>Salvar dados de formulário  
 No método **OnNextClicked**, chame os métodos de formulário mostrados na Tabela 29.  

### <a name="table-29-onnextclicked-method"></a>Tabela 29. OnNextClicked Method  

|**Método**|**Descrição**|  
|-|-|  
|**InitSection**|Fornece o nome da seção que será mostrada na página **Resumo** desta página|  
|**SaveFields**|Salve os valores de campo para variáveis de sequência de tarefas e para a página **Resumo**|  

#####  <a name="Init"></a> Init  

```  
HRESULT Init(IWizardPageView *pView, IWizardPageContainer *pContainer)  
```  

 Você geralmente chama esse método próximo do início do método **OnWindowCreated** da sua página. O comando deve ter esta aparência:  

```  
Form()->Init(View(), Container());  
```  

##### <a name="setpageinfo"></a>SetPageInfo  

```  
HRESULT SetPageInfo(ISettingsProperties *pPageInfo)  
```  

 Esse método é chamado internamente, e você não deve chamá-lo por conta própria. Ele fornece o XML da página para o controlador de formulário.  

##### <a name="validate"></a>Validate  

```  
HRESULT Validate(void)  
```  

 Esse método executa todos os validadores anexados aos controles. Se um validador não for passado, o controlador de formulário exibirá uma mensagem de aviso e desabilitará o botão **Avançar**. Em seguida, interromperá o processamento dos validadores. Normalmente, só é necessário chamar esse método no final do seu método **OnWindowCreated**; ele sempre retorna **S_OK**.  

##### <a name="addtogroup"></a>AddToGroup  

```  
AddToGroup(int groupControlId, int controlId)  
```  

 Esse método adiciona um controle como um "filho" de uma caixa de seleção ou botão de opção, conforme mostrado na Tabela 30. Todos esses controles filho serão desabilitados quando o controle pai não estiver selecionado. O método sempre retorna **S_OK**.  

### <a name="table-30-addtogroup"></a>Tabela 30. AddToGroup  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**groupControlId**|A ID da caixa de seleção ou o botão de opção que controlará o estado de habilitação do controle filho|  
|**Controlld**|A ID do controle que você deseja adicionar como um filho|  

##### <a name="updatecheckgroup"></a>UpdateCheckGroup  

```  
HRESULT UpdateCheckGroup(int groupControlId)  
```  

 Esse método atualiza o status de habilitação ou desabilitação dos controles filho de um grupo com base no status do controle pai. Em geral, não é necessário chamar esse método por conta própria, porque o controlador de formulário o chama para você.  

##### <a name="addvalidator"></a>AddValidator  

```  
HRESULT AddValidator(int controlId, IValidator *pValidator, IControl *pControl = 0)  
```  

 Chame esse método apenas se você tiver um validador no qual deseja criar um código, em vez de fazer isso com o XML. Esse método sempre retorna **S_OK**.  

##### <a name="addvalidator"></a>AddValidator  

```  
HRESULT AddValidator(int controlId, LPCWSTR validatorId, LPCWSTR message, IValidator **ppValidator = nullptr)  
```  

 Chame esse método apenas se você tiver um validador no qual deseja criar um código, em vez de fazer isso com o XML.  

##### <a name="disablevalidation"></a>DisableValidation  

```  
HRESULT DisableValidation(int controlId, BOOL disable)  
```  

 Chame esse método para desabilitar explicitamente o validador para um controle ou para restaurar a validação normal, conforme mostrado na Tabela 31. Esse método é útil, por exemplo, quando você tem que habilitar/desabilitar regras para controles que não são abordados com a validação do formulário e você precisa desabilitar a validação para um controle. Em outras palavras, normalmente você não chamaria esse método. Esse método sempre retorna **S_OK**.  

### <a name="table-31-hresult-disablevalidation"></a>Tabela 31. HRESULT DisableValidation  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**controlId**|O controle para o qual você deseja habilitar ou desabilitar a validação|  
|**Desabilitar**|Definido como TRUE para desabilitar a validação e como FALSE para restaurar a validação normal|  

#####  <a name="AddField"></a> AddField  

```  
HRESULT AddField(LPCWSTR fieldName, int controlId, BOOL suppressLog, DialogControlTypes type)  
```  

 Adicione um mapeamento de controle entre o nome em um elemento **Field** do arquivo XML .config e a ID do controle na caixa de diálogo da sua página, conforme mostrado na Tabela 32. É necessário chamar esse método antes da chamada para **InitFields**, pois **InitFields** usa essas informações. Esse método sempre retorna **S_OK**.  

### <a name="table-32-hresult-addfield"></a>Tabela 32. HRESULT AddField  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**Fieldname**|Nome do campo como ele aparece no XML da sua página|  
|**controlId**|A ID do controle no modelo de caixa de diálogo da sua página|  
|**suppressLog**|Defina como TRUE se não desejar que os valores desse campo sejam gravados no arquivo de log; sempre defina esse parâmetro como TRUE para senha ou para campos PIN|  
|**Tipo**|O tipo de controle, que é um dos seguintes:<br /><br /> -   **CONTROL_STATIC_TEXT**<br />-   **CONTROL_COMBO_BOX**<br />-   **CONTROL_LIST_VIEW**<br />-   **CONTROL_PROGRESS_BAR**<br />-   **CONTROL_GENERIC**<br />-   **CONTROL_RADIO_BUTTON**<br />-   **CONTROL_CHECK_BOX**<br />-   **CONTROL_TREE_VIEW**|  

#####  <a name="AddRadioGroup"></a> AddRadioGroup  

```  
HRESULT AddRadioGroup(LPCWSTR groupName, int radioControlId)  
```  

 Esse método adiciona um controle a um grupo de botões de opção nomeados, conforme mostrado na Tabela 33. É necessário chamá-lo antes do método **InitFields**, porque esse método usa atributos no elemento **RadioGroup** para controlar as configurações de todos os controles de botão de opção no grupo. Grupos de botões de opção podem ser bloqueados, por exemplo, para que todos os botões de opção sejam desabilitados, mas os controles filho são habilitados ou desabilitados com base apenas em qual botão de opção está selecionado. Esse método sempre retorna **S_OK**.  

### <a name="table-33-hresult-addradiogroup"></a>Tabela 33. HRESULT AddRadioGroup  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**groupName**|Uma cadeia de caracteres que define um grupo de botões de opção nesta página|  
|**radioControlId**|A ID de um único botão de opção a ser adicionada a este grupo|  

##### <a name="enableradiogroup"></a>EnableRadioGroup  

```  
HRESULT EnableRadioGroup(LPCWSTR groupName, BOOL enable)  
```  

 Esse método permite habilitar ou desabilitar um grupo de botões de opção inteiro. Desabilitar um grupo de botões de opção desabilita todos os controles de botão de opção no grupo, assim como os filhos desses botões de opção que foram adicionados com **AddToGroup**. Consulte a Tabela 34 e a Tabela 35.  

### <a name="table-34-enableradiogroup"></a>Tabela 34. EnableRadioGroup  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**groupName**|Nome de um grupo de botões de opção que você já definiu com uma chamada para **AddRadioGroup**|  
|**Habilitar**|Defina como TRUE para habilitar o grupo de botões de opção e FALSE desabilitá-lo|  

### <a name="table-35-hresult-enableradiogroup"></a>Tabela 35. HRESULT EnableRadioGroup  

|**HRESULT**|**Descrição**|  
|-|-|  
|**S_OK**|Grupo habilitado ou desabilitado|  
|**E_INVALIDARG**|Não há nenhum grupo de botões de opção com o nome fornecido|  

#####  <a name="InitFields"></a> InitFields  

```  
HRESULT InitFields(IFieldCallback *pFieldCallback = nullptr)  
```  

 Antes de chamar esse método, chame **AddField** para cada campo que o XML pode controlar. Esse método sempre retorna **S_OK**.  

 O parâmetro **pFieldCallback** é opcional. Se você o fornecer, o controlador de formulário chamará **SetFieldDefault** para controles que não são **CONTROL_STATIC_TEXT** nem **CONTROL_CHECK_BOX**. Esse comportamento permite recuperar um valor padrão do XML e defini-lo no controle por conta própria.  

#####  <a name="SaveFields"></a> SaveFields  

```  
HRESULT SaveFields(IFieldCallback *pFieldCallback = nullptr)  
```  

 Esse método salva valores de campo para variáveis de sequência de tarefas e para os dados de resumo que serão mostrados na página **Resumo**. Fornecer um ponteiro em **pFieldCallback** permite manipular valores de salvamento para controles não compatíveis com **CONTROL_STATIC_TEXT**.  

##### <a name="isfielddisabled"></a>IsFieldDisabled  

```  
BOOL IsFieldDisabled(int controlId)  
```  

 Esse método permite que você determine se um campo foi desabilitado no XML.  

#####  <a name="InitSection"></a> InitSection  

```  
HRESULT InitSection(LPCWSTR key, LPCWSTR sectionCaption)  
```  

 Esse método inicializa os dados de resumo que serão mostrados na página **Resumo**, conforme mostrado na Tabela 36. Chame esse método em seu método **OnNextClicked** antes de chamar **SaveFields**. Esse método sempre retorna **S_OK**.  

### <a name="table-36-hresult-initsection"></a>Tabela 36. HRESULT InitSection  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**Key**|Esse parâmetro deve ser exclusivo para sua página. Ele é usado para garantir que cada página tem suas próprias informações de resumo.|  
|**sectionCaption**|O cabeçalho será mostrado na página **Summary** para as informações de resumo dessa página. Normalmente, use **DisplayName()** como o valor desse parâmetro.|  

##### <a name="addsummaryitem"></a>AddSummaryItem  

```  
HRESULT AddSummaryItem(LPCWSTR first, LPCWSTR second)  
```  

 Esse método permite adicionar itens de resumo à página **Resumo** acima e além desses itens definidos com o XML. Consulte a Tabela 37.  

### <a name="table-37-hresult-addsummaryitem"></a>Tabela 37. HRESULT AddSummaryItem  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**First**|A legenda do item de resumo, exibido no lado esquerdo|  
|**Second**|O valor que será mostrado no lado direito|  

##### <a name="suppresslogvalue"></a>SuppressLogValue  

```  
HRESULT SuppressLogValue(LPCWSTR tsVariableName)  
```  

 Chame esse método para as variáveis de sequência de tarefas para as quais você não deseja que os valores sejam gravados no arquivo de log. Chame esse método para variáveis de sequência de tarefas que armazenam senhas, PINs ou outros valores confidenciais que um usuário pode inserir.  

##### <a name="savetext"></a>SaveText  

```  
HRESULT SaveText(int controlId, LPCWSTR tsVariableName, LPCWSTR summaryCaption)  
```  

 Esse método salva o valor de um controle de texto em uma variável de sequência de tarefas e na seção de resumo. Normalmente, não será necessário chamar esse método por conta própria, porque o controlador de formulário faz isso para todos os campos. Consulte a Tabela 38.  

### <a name="table-38-hresult-savetext"></a>Tabela 38. HRESULT SaveText  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**controlId**|A ID da caixa de texto que contém o valor que você deseja salvar (ou qualquer outro controle que pode retornar texto)|  
|**tsVariableName**|Nome da variável de sequência de tarefas que você deseja modificar|  
|**summaryCaption**|A legenda na página **Resumo** para esse valor|  

##### <a name="loadtext"></a>LoadText  

```  
HRESULT LoadText(int controlId, LPCWSTR tsVariableName)  
```  

 Esse método lê o valor de uma variável de sequência de tarefas e define a caixa de texto como esse valor.  

##### <a name="controlevent"></a>ControlEvent  

```  
void ControlEvent(WORD eventId, WORD controlId)  
```  

 Chame esse método em seu método **OnControlEvent** para garantir que o controlador do formulário possa processar eventos de controle, que ele precisa fazer para funcionar corretamente. Os valores que você passa para esse método são os mesmos valores passados para o método **OnControlEvent**.  

##### <a name="isvalid"></a>IsValid  

```  
BOOL IsValid(void)  
```  

 Esse método retorna o status da validação mais recente do formulário. Se qualquer um dos validadores de controle relatou um erro, esse método retorna FALSE. Em outras palavras, ele retornará TRUE somente se todos os controles na página forem válidos.  

#### <a name="ivalidator-interface"></a>Interface IValidator  

```  
__interface IValidator : IUnknown  
{  
    HRESULT Init(IControl *pControl, LPCTSTR message);  
    HRESULT Init(IControl *pControl, IWizardPageContainer *pContainer, IStringProperties *pProperties);  
    BOOL, IsValid(LPBSTR pMessage);  
    HRESULT SetProperty(int propertyId, LPVARIANT pValue);  
    HRESULT SetProperty(int propertyId, IUnknown *pUnknown);  
    HRESULT SetProperty)(int propertyId, LPCTSTR pValue);  
};  
```  

##### <a name="overview"></a>Visão geral  
 *Validadores* são componentes que podem validar um único controle em sua página. A maneira mais fácil de implementar um validador é torná-lo uma subclasse da classe **BaseValidator**, definida no arquivo de cabeçalho BaseValidator.h.  

##### <a name="hresult-initicontrol-pcontrol-lpctstr-message"></a>HRESULT Init(IControl \*pControl, LPCTSTR message)  
 Se você criar um validador no código, será possível chamar esse método para inicializá-lo. Consulte a Tabela 39.  

### <a name="table-39-hresult-init"></a>Tabela 39. HRESULT Init  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**pControl**|O controle que seu validador deve validar|  
|**Message**|A mensagem a ser exibida na página se o controle não for válido|  

##### <a name="hresult-initicontrol-pcontrol-iwizardpagecontainer-pcontainer-istringproperties-pproperties"></a>HRESULT Init(IControl \*pControl, IWizardPageContainer \*pContainer, IStringProperties \*pProperties)  
 O controlador de formulário chama esse método para inicializar os validadores que ele cria com base no XML da página. Consulte a Tabela 40.  

### <a name="table-40-hresult-init-method"></a>Tabela 40. Método HRESULT Init  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**pControl**|O controle que seu validador deve validar|  
|**pContainer**|Caso seu validador precise de acesso ao agente ou precise criar outros componentes|  
|**pProperties**|Fornece acesso às propriedades (elementos setter) para o validador|  

##### <a name="bool-isvalidlpbstr-pmessage"></a>BOOL, IsValid(LPBSTR pMessage)  
 Esse método retornará TRUE se o controle for válido ou FALSE se o controle for inválido. No retorno, **pMessage** deve ser preenchido com um novo **BSTR** que contém a mensagem a ser exibida quando o controle não é válido.  

##### <a name="hresult-setpropertyint-propertyid-lpvariant-pvalue"></a>HRESULT SetProperty(int propertyId, LPVARIANT pValue)  
 Será possível implementar esse método se você precisar de valores extras que não são fornecidos no XML.  

##### <a name="hresult-setpropertyint-propertyid-iunknown-punknown"></a>HRESULT SetProperty(int propertyId, IUnknown \*pUnknown)  
 Será possível implementar esse método se você precisar de valores extras que não são fornecidos no XML.  

##### <a name="hresult-setpropertyint-propertyid-lpctstr-pvalue"></a>HRESULT SetProperty)(int propertyId, LPCTSTR pValue)  
 Será possível implementar esse método se você precisar de valores extras que não são fornecidos no XML.  

#### <a name="iregex-interface"></a>Interface IRegEx  

```  
__interface IRegEx : IUnknown  
{  
    BOOL MatchesRegex(LPCTSTR input, LPCTSTR regex);  
    HRESULT GetMatch(size_t index, LPBSTR pValue);  
};  
```  

 Esse método é implementado pelo componente **ID_Regex** (IRegex.h) e fornece suporte para processamento de expressão regular.  

##### <a name="bool-matchesregexlpctstr-input-lpctstr-regex"></a>BOOL MatchesRegex(LPCTSTR input, LPCTSTR regex)  
 Esse método executa a expressão regular com relação ao texto de entrada. Ele usa a função **regex_match** da biblioteca padrão C++ para fazer o trabalho real. O método retornará TRUE se houver correspondências; caso contrário, FALSE.  

##### <a name="hresult-getmatchsizet-index-lpbstr-pvalue"></a>HRESULT GetMatch(size_t index, LPBSTR pValue)  
 Esse método permite recuperar as correspondências da chamada **MatchesRegex** mais recente. Observe que não há nenhum processamento de erros nesse método, e ele retorna **S_OK** ou gera uma exceção.  

#### <a name="isummaryinfo-interface"></a>Interface ISummaryInfo  

```  
__interface ISummaryInfo : IUnknown  
{  
    size_t Count(void);  
    HRESULT Clear(void);  
    HRESULT AddInfo(LPCTSTR pFirst, LPCTSTR pSecond);  
    HRESULT GetInfo(size_t index, LPBSTR pFirst, LPBSTR pSecond);  
    HRESULT GetCaption(LPBSTR pCaption);  
    HRESULT SetCaption(LPCTSTR caption);  
};  
```  

 Você não deverá usar essa interface diretamente. Em vez disso, use **IFormController**.  

#### <a name="isummarybag"></a>ISummaryBag  

```  
__interface ISummaryBag : IUnknown  
{  
    size_t Count(void);  
    HRESULT GetInfoByIndex(size_t index, [out] ISummaryInfo **ppSummary);  
    HRESULT GetInfoByKey(LPCTSTR key, [out] ISummaryInfo **ppSummary);  
};  
```  

 Você não deverá usar essa interface diretamente. Em vez disso, use **IFormController**.  

#### <a name="itsvariablebag-interface"></a>Interface ITSVariableBag  

```  
__interface ITSVariableBag : IUnknown  
{  
    void GetValue([in] LPCTSTR variableName, [out] LPBSTR pValue);  
    void SetValue([in] LPCTSTR variableName, [in] LPCTSTR pValue);  
    void Clear(void);  
    HRESULT Remove([in] LPCTSTR variableName);  
    HRESULT SuppressLogValue([in] LPCTSTR variableName);  
    void Save(void);  
};  
```  

 Essa interface fornece acesso para as variáveis de sequência de tarefas. É possível acessar essa interface usando o método **TSVariables()** da sua página.  

##### <a name="void-getvaluein-lpctstr-variablename-out-lpbstr-pvalue"></a>void GetValue([in] LPCTSTR variableName, [out] LPBSTR pValue)  
 Esse método lê o valor de uma variável de sequência de tarefas.  

> [!NOTE]
>  Os valores são armazenados em cache depois da primeira leitura.  

##### <a name="void-setvaluein-lpctstr-variablename-in-lpctstr-pvalue"></a>void SetValue([in] LPCTSTR variableName, [in] LPCTSTR pValue)  
 Esse método define o valor de uma variável de sequência de tarefas. Esse valor é salvo na memória. Os valores de sequência de tarefas são escritos depois de você clicar em **Concluir** no Assistente de UDI.  

##### <a name="void-clearvoid"></a>void Clear(void)  
 Esse método remove todos os valores de sequência de tarefas que foram salvos na memória.  

##### <a name="hresult-removein-lpctstr-variablename"></a>HRESULT Remove([in] LPCTSTR variableName)  
 Esse método remove um valor específico da sequência de tarefas da memória. Na próxima vez em que você chamar **GetValue** com o mesmo nome de sequência de tarefas, o método tentará recuperá-lo da sequência de tarefas.  

##### <a name="hresult-suppresslogvaluein-lpctstr-variablename"></a>HRESULT SuppressLogValue([in] LPCTSTR variableName)  
 Sempre que as variáveis de sequência de tarefas forem gravadas, como quando você clica em **Concluir** no Assistente de UDI, os nomes e valores serão gravados no arquivo de log. Chame esse método para suprimir o registro em log de valores confidenciais, como senhas ou PINs, para uma variável de sequência de tarefas específica.  

##### <a name="void-savevoid"></a>void Save(void)  
 Esse método salva todos valores de sequência de tarefas que foram definidos com chamadas para **SetValue**.  

#### <a name="itsvariablerepository-interface"></a>Interface ITSVariableRepository  

```  
__interface ITSVariableRepository : IUnknown  
{  
    void GetValue([in] LPCTSTR variableName, BOOL logValue, [out] LPBSTR pValue);  
    void SetValue([in] LPCTSTR variableName, BOOL logValue, [in] LPCTSTR value);  
};  
```  

 Essa interface é para uso interno por **TSVariableBag** para leitura e gravação de variáveis de sequência de tarefas.  

#### <a name="iwizardfinish-interface"></a>Interface IWizardFinish  

```  
__interface IWizardFinish : IUnknown  
{  
    HRESULT Canceled(void);  
    HRESULT Finished(void);  
};  
```  

 Essa interface será útil em cenários avançados em que você desejar realizar processamento adicional quando clicar em **Concluir** ou **Cancelar** no Assistente de UDI. O Assistente de UDI contém uma tarefa **Concluir** que salva as variáveis de sequência de tarefas quando clica em **Concluir**. Se você cancelar o assistente, a tarefa somente definirá a variável de sequência de tarefas **OSDSetupWizCancelled** como TRUE e não salvará as alterações em nenhuma outra variável de sequência de tarefas.  

 Se você criar seu próprio componente de término, será necessário registrá-lo com um código como este:  

```  
Register<MyFinishTaskFactory>(ID_MyFinishTask, pRegistry);  

PWizardFinish pFinish;  
CreateInstance(pRegistry, ID_MyFinishTask, &pFinish);  

PWizardFinishService pService;  
GetService<IWizardFinishService>(pRegistry, &pService);  

pService->Register(pFinish);  
```  

#### <a name="ibindablelist-interface"></a>Interface IBindableList  

```  
__interface IBindableList : IUnknown  
{  
    size_t Count(void);  
    HRESULT GetCaption(size_t index, LPBSTR pCaption);  
};  
```  

 Implemente essa interface se você tiver um componente de fonte de dados que deseja associar a uma caixa de combinação chamando seu método **Bind**.  

##### <a name="sizet-countvoid"></a>size_t Count(void)  
 Esse método retorna o número de itens na lista.  

##### <a name="hresult-getcaptionsizet-index-lpbstr-pcaption"></a>HRESULT GetCaption(size_t index, LPBSTR pCaption)  
 Esse método retorna a legenda do item em um índice específico.  

#### <a name="idatanodes-interface"></a>Interfaces IDataNodes  

```  
__interface IDataNodes : IUnknown  
{  
    size_t Count();  
    HRESULT SetCaptionProperty(LPCTSTR captionProperty);  
    HRESULT GetProperty(size_t index, LPCTSTR propertyName, [out] LPBSTR propertyValue);  
    HRESULT GetNode(size_t index, [out] ISettingsProperties **ppNode);  
};  
```  

 Essa interface fornece acesso a dados hierárquicos que podem ser salvos em uma página. Obtenha essa interface por meio de métodos na interface **ISettingsProperties**, disponível para sua página por meio do método **Settings**.  

 Os dados no XML de uma página podem ter esta aparência  

```  
      <Data Name="Network">  
        <DataItem>  
          <Setter Property="DisplayName">Public</Setter>  
          <Setter Property="Share">\\servername\Share</Setter>  
        </DataItem>  
        <DataItem>  
          <Setter Property="DisplayName">Dev Team</Setter>  
          <Setter Property="Share">\\servername\DevShare</Setter>  
        </DataItem>  
      </Data>  
```  

 Chamar **Settings()->GetDataNode(L"Network", &pData)** oferece uma instância **IDataNodes** com dois itens de dados (cada um dos quais, por sua vez, tem duas propriedades).  

##### <a name="sizet-count"></a>size_t Count()  
 Esse método retorna o número de elementos **DataItem**.  

##### <a name="hresult-setcaptionpropertylpctstr-captionproperty"></a>HRESULT SetCaptionProperty(LPCTSTR captionProperty)  
 O componente compatível com essa interface também é compatível com **IBindableList**, que torna fácil preencher uma caixa de combinação usando dados do XML da página. Esse método controla qual propriedade (setter) em cada elemento **DataItem** será usada para essa associação. Por exemplo, seria possível chamar esse método com **DisplayName**, e ele usaria a propriedade setter para a associação de dados. A caixa de combinação poderia, então, conter **Público** e **Equipe de desenvolvimento** como itens.  

##### <a name="hresult-getpropertysizet-index-lpctstr-propertyname-out-lpbstr-propertyvalue"></a>HRESULT GetProperty(size_t index, LPCTSTR propertyName, [out] LPBSTR propertyValue)  
 Esse método obtém uma propriedade de um dos elementos **DataItem**. Consulte a Tabela 41 e a Tabela 42.  

### <a name="table-41-dataitem-getproperty"></a>Tabela 41. DataItem GetProperty  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**Index**|O valor de índice (que começa com 0) do **DataItem** para o qual você deseja recuperar um valor da propriedade|  
|**propertyName**|Nome da propriedade setter para a qual você deseja recuperar um valor|  
|**propertyValue**|No retorno, contém o valor de cadeia de caracteres de uma propriedade|  

### <a name="table-42-hresult-getproperty"></a>Tabela 42. HRESULT GetProperty  

|||  
|-|-|  
|**HRESULT**|**Descrição**|  
|**S_OK**|A propriedade foi recuperada.|  
|**E_INVALIDARG**|O índice ultrapassou o fim da matriz.|  

##### <a name="hresult-getnodesizet-index-out-isettingsproperties-ppnode"></a>HRESULT GetNode(size_t index, [out] ISettingsProperties **ppNode)  
 Esse método é semelhante a **GetProperty**, mas, em vez de retornar um valor de um **DataItem**, ele retorna o **DataItem** inteiro encapsulado em uma interface **ISettingsProperties**. Consulte a Tabela 43 e a Tabela 44.  

### <a name="table-43-hresult-getnode"></a>Tabela 43. HRESULT GetNode  

|**Parâmetro**|**Descrição**|  
|-|-|  
|Índice|O valor de índice (que começa com 0) do **DataItem** para o qual você deseja recuperar um valor da propriedade|  
|**ppNode**|Na saída, a interface **ISettingsProperties** que encapsula o nó **DataItem**|  

### <a name="table-44-hresult-getnode-results"></a>Tabela 44. Resultados de HRESULT GetNode  

|**HRESULT**|**Descrição**|  
|-|-|  
|**S_OK**|O nó foi recuperado.|  
|**E_INVALIDARG**|O índice ultrapassou o fim da matriz.|  

#### <a name="ifactoryregistry-interface"></a>Interface IFactoryRegistry  

```  
__interface IFactoryRegistry : IUnknown  
{  
    void Register(LPCTSTR type,  IClassFactory *pFactory);  
    HRESULT LoadAndRegister(LPCTSTR dllName, ILogger *pLogger);  
    BOOL Contains(LPCTSTR type);  
    HRESULT GetFactory(LPCTSTR type,  IClassFactory **ppFactory);  
    HRESULT CreateInstance(LPCTSTR type,  IUnknown **ppInstance);  
    HRESULT SetContainer(IWizardPageContainer *pContainer);  
    HRESULT RegisterService(REFGUID iid, IUnknown *pService);  
    HRESULT GetService(REFGUID iid,  IUnknown **ppService);  
};  
```  

##### <a name="overview"></a>Visão geral  
 Quando você cria uma página personalizada, é necessário, no mínimo, criar uma *fábrica de páginas*— uma classe que implementa **IClassFactory**. (É possível usar **ClassFactoryImpl** como uma classe base para sua fábrica).  

##### <a name="void-registerlpctstr-type--iclassfactory-pfactory"></a>void Register(LPCTSTR type,  IClassFactory \*pFactory)  
 Esse método registra uma fábrica de classes com o Registro. Consulte a Tabela 45.  

### <a name="table-45-iclassfactory-void-register"></a>Tabela 45. Registro IClassFactory void  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**Tipo**|Uma cadeia de caracteres que identifica a fábrica que você está registrando; geralmente, esse parâmetro deve ter o nome da usa empresa na cadeia de caracteres para garantir que ele seja exclusivo|  
|**pFactory**|Um ponteiro para sua instância de fábrica de classes|  

##### <a name="hresult-loadandregisterlpctstr-dllname-ilogger-plogger"></a>HRESULT LoadAndRegister(LPCTSTR dllName, ILogger \*pLogger)  
 Esse método é apenas para uso interno.  

##### <a name="bool-containslpctstr-type"></a>BOOL Contains(LPCTSTR type)  
 Esse método é geralmente para uso interno. Ele verifica se uma fábrica de classes foi registrada para um tipo.  

##### <a name="hresult-getfactorylpctstr-type--iclassfactory-ppfactory"></a>HRESULT GetFactory(LPCTSTR type,  IClassFactory **ppFactory)  
 Esse método permite recuperar a fábrica de classes. Normalmente, você chamaria **CreateInstance**. No entanto, se você criar um grande número do mesmo componente, será mais eficiente recuperar a fábrica e, em seguida, pedir para ela criar as instâncias para você.  

##### <a name="hresult-createinstancelpctstr-type--iunknown-ppinstance"></a>HRESULT CreateInstance(LPCTSTR type,  IUnknown **ppInstance)  
 Esse método cria uma instância de um componente, dado seu tipo. Use o método de modelo **CreateInstance**, que permite a criação de objetos fortemente tipados.  

##### <a name="hresult-setcontaineriwizardpagecontainer-pcontainer"></a>HRESULT SetContainer(IWizardPageContainer \*pContainer)  
 Esse método é apenas para uso interno.  

##### <a name="hresult-registerservicerefguid-iid-iunknown-pservice"></a>HRESULT RegisterService(REFGUID iid, IUnknown \*pService)  
 *Serviços* são instâncias individuais de um componente que podem ser usadas em vários lugares. É possível usar esse método para registrar um serviço em uma página e, em seguida, recuperar a mesma instância de outra página.  

##### <a name="hresult-getservicerefguid-iid--iunknown-ppservice"></a>HRESULT GetService(REFGUID iid,  IUnknown **ppService)  
 Esse método recupera um serviço registrado anteriormente com uma chamada para RegisterService.  

##### <a name="hresult-setlanguagelangid-languageid"></a>HRESULT SetLanguage(LANGID languageId)  
 Esse método define a linguagem do Assistente de UDI como o identificador de linguagem fornecido no parâmetro **languageId**.  

##### <a name="langid-getlanguage"></a>LANGID GetLanguage()  
 Esse método retorna o valor do identificador de linguagem fornecido com o parâmetro de linha de comando **/locale** para o Assistente de UDI. Esse método retorna um dos seguintes valores:  

-   O valor do identificador de linguagem fornecido com o parâmetro de linha de comando **/locale**  

-   0, se você não forneceu o parâmetro de linha de comando **/locale**  

#### <a name="ilogger-interface"></a>Interface ILogger  

```  
__interface ILogger : IUnknown  
{  
    HRESULT Init(LPCWSTR logFilename);  
    HRESULT MoveLog(LPCWSTR logFilename);  
    HRESULT LogBase(EMessageType messageType, LPCTSTR component, SYSTEMTIME eventTime, LPCTSTR message);  
    HRESULT Log(EMessageType messageType, LPCTSTR component, LPCTSTR message);  
    HRESULT Error(HRESULT error, LPCTSTR component, LPCTSTR message);  
    HRESULT Error2(HRESULT error, LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Normal(LPCTSTR component, LPCTSTR message);      
    HRESULT Normal2(LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Verbose(LPCTSTR component, LPCTSTR message);  
    HRESULT Verbose2(LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Debug(LPCWSTR component, LPCWSTR message);  
    HRESULT EnableDebug(BOOL debug);  
    HRESULT Close(void);  
    HRESULT GetLogFilename(LPBSTR pFilename);  
};  
```  

##### <a name="overview"></a>Visão geral  
 O Assistente de UDI registra informações em um arquivo de log, que ajuda a solucionar problemas encontrados no campo. É uma boa ideia para suas páginas registrarem informações. É possível obter um ponteiro para essa interface de dentro de sua página usando o método **Logger()** da página. As linhas no arquivo de log contêm um número de "nível" que representa mensagens de erro, normais, detalhadas ou de depuração.  

> [!NOTE]
>  As mensagens de depuração não são salvas no arquivo de log, a menos que o suporte à depuração esteja ativado. É possível ativar o suporte à depuração, adicionando a seguinte linha ao elemento **Style** no arquivo .config:  

```  
<Setter Property="debug">true</Setter>  
```  

##### <a name="init"></a>Init  

```  
HRESULT Init(LPCWSTR logFilename)  
```  

 Esse método é apenas para uso interno.  

##### <a name="movelog"></a>MoveLog  

```  
HRESULT MoveLog(LPCWSTR logFilename)  
```  

 Esse método é apenas para uso interno.  

##### <a name="logbase"></a>LogBase  

```  
HRESULT LogBase(EMessageType messageType, LPCTSTR component, SYSTEMTIME eventTime, LPCTSTR message)  
```  

 Esse método é apenas para uso interno.  

##### <a name="log"></a>Log  

```  
HRESULT Log(EMessageType messageType, LPCTSTR component, LPCTSTR message)  
```  

 Esse método é apenas para uso interno.  

##### <a name="error"></a>Erro  

```  
HRESULT Error(HRESULT error, LPCTSTR component, LPCTSTR message)  
```  

 Chame esse método para registrar informações sobre um erro. Consulte a Tabela 46.  

### <a name="table-46-hresult-error"></a>Tabela 46. Erro HRESULT  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**Erro**|O código de erro retornado por uma chamada (esse código será exibido na entrada de log como um número).|  
|**Componente**|Uma cadeia de caracteres que identifica a origem do erro, que geralmente é a página ou o componente que você escreveu|  
|**Message**|A mensagem que explica o que causou o erro|  

#####  <a name="Error2"></a> Error2  

```  
HRESULT Error2(HRESULT error, LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 Esse método é como o método **Error**, mas permite que você forneça uma mensagem de duas partes. A mensagem final terá "mensagem" e, em seguida, "mensagem2" no arquivo de saída. Isso é simplesmente um método de conveniência.  

##### <a name="normal"></a>Normal  

```  
HRESULT Normal(LPCTSTR component, LPCTSTR message)  
```  

 Esse método registra uma mensagem normal. Consulte a descrição do método [Error](#Error) para parâmetros.  

##### <a name="normal2"></a>Normal2  

```  
HRESULT Normal2(LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 Esse método registra uma mensagem normal. Consulte a descrição do método [Error2](#Error2) para parâmetros.  

##### <a name="verbose"></a>Detalhado  

```  
HRESULT Verbose(LPCTSTR component, LPCTSTR message)  
```  

 Esse método registra uma mensagem detalhada. Consulte a descrição do método [Error](#Error) para parâmetros.  

##### <a name="verbose2"></a>Verbose2  

```  
HRESULT Verbose2(LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 Esse método registra uma mensagem detalhada. Consulte a descrição do método [Error2](#Error2) para parâmetros.  

##### <a name="debug"></a>Depurar  

```  
HRESULT Debug(LPCWSTR component, LPCWSTR message)  
```  

 Esse método registra uma mensagem de depuração. Consulte a descrição do método [Error](#Error) para parâmetros. Mensagens de depuração não são salvas no arquivo, a menos que isso esteja habilitado. Consulte a seção Visão geral para obter detalhes.  

##### <a name="enabledebug"></a>EnableDebug  

```  
HRESULT EnableDebug(BOOL debug)  
```  

 Esse método é apenas para uso interno.  

##### <a name="close"></a>Fechar  

```  
HRESULT Close(void)  
```  

 Esse método é apenas para uso interno.  

##### <a name="getlogfilename"></a>GetLogFilename  

```  
HRESULT GetLogFilename(LPBSTR pFilename)  
```  

 Esse método recupera o nome do arquivo de log.  

#### <a name="iorientation-interface"></a>Interface IOrientation  

```  
__interface IOrientation : IUnknown  
{  
    void SetController(IWizardDialogController *pController);  
    int AddPage(LPCTSTR name);  
    void SelectPage(int index);  
};  
```  

 Essa interface é apenas para uso interno.  

#### <a name="isettings-interface"></a>Interface ISettings  

```  
__interface ISettings : IUnknown  
{  
    int NumDlls();  
    int NumPages();  

    HRESULT SetStage(LPCWSTR stageName);  
    HRESULT GetDllName(long index, __out LPBSTR pDllName);  
    HRESULT GetPageInfo(long index, __out ISettingsProperties **ppPageInfo);  
    HRESULT GetStyle(__out ISettingsProperties **ppStyleInfo);  
};  
```  

 Essa interface é apenas para uso interno.  

#### <a name="isettingsproperties-interface"></a>Interface ISettingsProperties  

```  
__interface ISettingsProperties : IUnknown  
{  
    HRESULT GetAttribute(LPCTSTR attributeName, __out LPBSTR attributeValue);  
    IStringProperties * Properties();  
   RESULT SelectNodes(LPCTSTR xPath, __out IXMLDOMNodeList **ppList);  
    HRESULT SelectSingleNode(LPCTSTR xPath, __out IXMLDOMNode **ppNode);  
    HRESULT GetDataNode(LPCTSTR name, __out ISettingsProperties **ppNode);  
    HRESULT GetDataNodes(__out IDataNodes **ppNodes);  
    HRESULT GetChildDataNodes(LPCTSTR childeName, __out IDataNodes **ppNodes);  
};  
```  

##### <a name="overview"></a>Visão geral  
 Essa interface fornece acesso aos dados da página. Para obter o nível superior de dados da página, use o método **Settings()** da página.  

##### <a name="hresult-getattributelpctstr-attributename--lpbstr-attributevalue"></a>HRESULT GetAttribute(LPCTSTR attributeName,  LPBSTR attributeValue)  
 Esse método permite recuperar os valores de atributos no nó principal, que é o nó **Página** quando você está usando o método **Settings()** da página.  

##### <a name="istringproperties--properties"></a>IStringProperties * Properties()  
 Esse método fornece acesso aos valores da propriedade setter no nó principal. Paga uma página, essas são as propriedades de nível superior.  

##### <a name="hresult-selectnodeslpctstr-xpath--ixmldomnodelist-pplist"></a>HRESULT SelectNodes(LPCTSTR xPath,  IXMLDOMNodeList **ppList)  
 Chame esse método se desejar obter diretamente uma lista de nós XML que usam uma expressão XPath. É melhor usar um dos outros métodos, se possível. Use esse método apenas se você não conseguir chegar aos nós de nenhuma outra maneira.  

##### <a name="hresult-selectsinglenodelpctstr-xpath--ixmldomnode-ppnode"></a>HRESULT SelectSingleNode(LPCTSTR xPath,  IXMLDOMNode **ppNode)  
 Chame esse método se desejar obter diretamente um único nó XML que usa uma expressão XPath. É melhor usar um dos outros métodos, se possível. Use esse método apenas se você não puder chegar a um nó de nenhuma outra maneira.  

##### <a name="hresult-getdatanodelpctstr-name--isettingsproperties-ppnode"></a>HRESULT GetDataNode(LPCTSTR name,  ISettingsProperties **ppNode)  
 Recupere um elemento **Data** com base no atributo **Name** desse elemento.  

##### <a name="hresult-getdatanodesidatanodes-ppnodes"></a>HRESULT GetDataNodes(IDataNodes **ppNodes)  
 Esse método recupera uma lista de elementos **DataItem** sob o nó atual. No nível da página, chame **GetDataNode** para recuperar uma interface **ISettingsProperty** para os dados. Em seguida, nessa instância, chame **GetDataNodes** para recuperar a lista de registros. Por exemplo, considerando este XML:  

```  
    <Page …>  
      <Data Name="Network">  
        <DataItem>  
          <Setter Property="DisplayName">Public</Setter>  
          <Setter Property="Share">\\servername\Share</Setter>  
        </DataItem>  
        <DataItem>  
          <Setter Property="DisplayName">Dev Team</Setter>  
          <Setter Property="Share">\\servername\DevShare</Setter>  
        </DataItem>  
      </Data>  

PSettingsProperties pData;  
Settings()->GetDataNode(L"Network", &pData);  
PDataNodes pNodes;  
pData->GetDataNodes(&pNodes);  
```  

##### <a name="hresult-getchilddatanodeslpctstr-childename--idatanodes-ppnodes"></a>HRESULT GetChildDataNodes(LPCTSTR childeName,  IDataNodes **ppNodes)  
 Esse método fornece uma maneira rápida de se chegar ao conjunto de nós **DataItem** em um nó **Dados** específico. Usando o XML do exemplo **GetDataNodes**, o código a seguir faz exatamente a mesma coisa que as quatro linhas de código no exemplo em **GetDataNodes**, mas com a verificação de erros:  

```  
ISimpleStringProperties Interface  
```  

#### <a name="isimplestringproperties-interface"></a>Interface ISimpleStringProperties  

```  
__interface ISimpleStringProperties : IStringProperties  
{  
void Add(LPCTSTR propertyName, LPCTSTR value);  
};  
```  

 Por si só, essa interface talvez não seja útil. No entanto, ela é implementada pelo componente **ID_SimpleStringProperties**, que também implementa a interface **IStringProperties**. É possível usar esse componente em casos em que é necessário passar um conjunto de propriedades para outro componente, como uma tarefa, mas você deseja adicionar valores programaticamente em vez de usar valores de XML. Veja um exemplo de como você usaria essa interface:  

```  
PSimpleStringProperties *pProperties;  
CreateInstance(Container(), ID_SimpleStringProperties, &pProperties);  
pProperties->Add(L"filename", L"%windir%\\system32\\cscript.exe");  
pTask->Init(pProperties, nullptr);  
IStringProperties  
__interface IStringProperties : IUnknown  
{  
    HRESULT Get(LPCTSTR propertyName, [out] LPBSTR pPropValue);  
};  
```  

 Essa interface oferece acesso simples a um conjunto de elementos setter oriundos do XML. Essa interface está disponível para as propriedades de uma página usando **Settings()->Properties()**.  

##### <a name="hresult-getlpctstr-propertyname-out-lpbstr-ppropvalue"></a>HRESULT Get(LPCTSTR propertyName, [out] LPBSTR pPropValue)  
 Esse método recupera um valor da propriedade único. Consulte a Tabela 47 e a Tabela 48.  

### <a name="table-47-ihresult-get-property-value"></a>Tabela 47. Valo da propriedade Get do IHRESULT  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**propertyName**|Nome da propriedade que você deseja ler|  
|**pPropValue**|Na saída, contém o valor da propriedade como uma cadeia de caracteres (esse valor será **nullptr** se não houver nenhuma propriedade).|  

### <a name="table-48-ihresult-get-property-value-results"></a>Tabela 48. Resultados do valor da propriedade Get de IHRESULT  

|||  
|-|-|  
|**HRESULT**|**Descrição**|  
|**S_OK**|O valor da propriedade é recuperado.|  
|**E_INVALIDARG**|Não há nenhuma propriedade com o nome fornecido.|  

#### <a name="itaskmanager-interface"></a>Interface ITaskManager  

```  
__interface ITaskManager : IUnknown  
{  
    HRESULT Init(IWizardPageView *pPageView, int idListView, int idMessage, int idRetryButton, ISettingsProperties *pPageInfo, ITaskManagerCallback *pCallback);  
    HRESULT SetFailMessage(LPCWSTR message);  

    HRESULT Start(void);  

    HRESULT GetTaskMessage(size_t index, LPBSTR message);  
    HRESULT GetResultType)(size_t index, LPBSTR type);  
    HRESULT GetProperty(size_t index, LPCTSTR propertyName, LPBSTR value);  
    int GetSelectedIndex(void);  
    HRESULT Wait(DWORD waitMilliseconds);  
    size_t FailedCount(void);  
    size_t WarningCount(void);  
    size_t SucceedCount(void);  
    size_t RunningCount(void);  

    void OnCommonControlEvent(WORD controlId, LPNMHDR pInfo);  
    void OnControlEvent(WORD eventId, WORD controlId);  
    void EnableButtons(BOOL enable);  
}  
```  

 Essa interface é implementada pelo componente **TaskManager** (**ID_TaskManager** em ITaskManager.h), que é o componente que executa tarefas na página de simulação. É possível usar a página de simulação diretamente, que é o que você faz na maior parte do tempo, ou criar sua própria, deixando esse componente fazer a maioria do trabalho.  

##### <a name="hresult-initiwizardpageview-ppageview-int-idlistview-int-idmessage-int-idretrybutton-isettingsproperties-ppageinfo-itaskmanagercallback-pcallback"></a>HRESULT Init(IWizardPageView \*pPageView, int idListView, int idMessage, int idRetryButton, ISettingsProperties \*pPageInfo, ITaskManagerCallback \*pCallback)  
 É necessário chamar esse método antes de chamar outro. Ele inicializa o componente **TaskManager**. Consulte a Tabela 49.  

### <a name="table-49-hresult-init"></a>Tabela 49. HRESULT Init  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**pPageView**|Fornece acesso à página que executará tarefas (essa página deve ter um conjunto específico de controles, que serão descritos nos próximos parâmetros).|  
|**idListView**|A ID de controle de um controle **ListView** que exibirá a lista de tarefas e o status dessas tarefas|  
|**idMessage**|A ID de controle de uma caixa de texto que será usada para exibir uma mensagem para a tarefa selecionada|  
|**idRetryButton**|A ID de controle de um botão que você pode clicar para executar as tarefas novamente|  
|**pPageInfo**|Um wrapper ao redor do XML da página (**TaskManager** carrega o conjunto de tarefas a serem executadas deste XML).|  
|**pCallback**|Pode ser nulo (se esse parâmetro não for nulo, **TaskManager** chamará o método **Started** quando ele iniciar uma tarefa e o método **Finished** para cada tarefa que concluir a execução).|  

##### <a name="hresult-setfailmessagelpcwstr-message"></a>HRESULT SetFailMessage(LPCWSTR message)  
 Esse método define a mensagem que será exibida se uma ou mais tarefas falharem.  

##### <a name="hresult-startvoid"></a>HRESULT Start(void)  
 Esse método inicia todas as tarefas. Cada tarefa é iniciada em um thread separado.  

##### <a name="hresult-gettaskmessagesizet-index-lpbstr-message"></a>HRESULT GetTaskMessage(size_t index, LPBSTR message)  
 Esse método é apenas para uso interno. Ele recupera a mensagem atual para uma tarefa com base em seu índice na lista de tarefas.  

##### <a name="hresult-getresulttypesizet-index-lpbstr-type"></a>HRESULT GetResultType)(size_t index, LPBSTR type)  
 Esse método recupera o "tipo" atual de uma tarefa. A Tabela 50 mostra os tipos disponíveis.  

### <a name="table-50-hresult-getresulttype"></a>Tabela 50. HRESULT GetResultType  

|**Tipo**|**Descrição**|  
|-|-|  
|**0**|Representa uma tarefa bem-sucedida|  
|**1**|Representa uma tarefa que retornou um aviso|  
|**-1**|Representa uma tarefa com falha|  

 O tipo é recuperado examinando o código de saída ou de erro da tarefa e localizando uma correspondência no elemento XML <ExitCodes\> da tarefa.  

##### <a name="hresult-getpropertysizet-index-lpctstr-propertyname-lpbstr-value"></a>HRESULT GetProperty(size_t index, LPCTSTR propertyName, LPBSTR value)  
 Esse método é usado pelas páginas de progresso e de simulação para recuperar a propriedade setter **BitmapFilename** para que ele possa exibir uma imagem ao lado da mensagem para a tarefa que você realça. Em outras palavras, é possível adicionar um setter personalizado ao XML da tarefa e, em seguida, recuperá-lo com esse método.  

##### <a name="int-getselectedindexvoid"></a>int GetSelectedIndex(void)  
 Esse método recupera o índice da tarefa selecionada no momento, o que é útil se você deseja recuperar informações adicionais sobre ela (consulte o método **GetProperty**) a serem exibidas para a tarefa selecionada. As páginas de progresso e de simulação usam esse método para exibir uma imagem da tarefa selecionada.  

##### <a name="hresult-waitdword-waitmilliseconds"></a>HRESULT Wait(DWORD waitMilliseconds)  
 Esse método ajuda principalmente com testes de unidade para o teste poder garantir que as tarefas sejam concluídas antes de o teste de unidade ser encerrado. Normalmente, você não chamaria esse método. Ele será retornado quando todas as tarefas terminarem de ser executadas ou quando tempo tiver decorrido.  

##### <a name="sizet-failedcountvoid"></a>size_t FailedCount(void)  
 Esse método retorna o número de tarefas marcadas como com falha no momento.  

##### <a name="sizet-warningcountvoid"></a>size_t WarningCount(void)  
 Esse método retorna o número de tarefas marcadas como aviso no momento.  

##### <a name="sizet-succeedcountvoid"></a>size_t SucceedCount(void)  
 Esse método retorna o número de tarefas marcadas como com êxito no momento.  

##### <a name="sizet-runningcountvoid"></a>size_t RunningCount(void)  
 Esse método retorna o número de tarefas em execução no momento.  

##### <a name="void-oncommoncontroleventword-controlid-lpnmhdr-pinfo"></a>void OnCommonControlEvent(WORD controlId, LPNMHDR pInfo)  
 Chame esse método de **OnCommonControlEvent** da sua página para que **TaskManager** possa processar os eventos necessários.  

##### <a name="void-oncontroleventword-eventid-word-controlid"></a>void OnControlEvent(WORD eventId, WORD controlId)  
 Chame esse método de **OnControlEvent** da sua página para que **TaskManager** possa processar os eventos necessários.  

##### <a name="void-enablebuttonsbool-enable"></a>void EnableButtons(BOOL enable)  
 Esse método é apenas para uso interno.  

#### <a name="iwizardcomponent-interface"></a>Interface IWizardComponent  

```  
__interface IWizardComponent : IUnknown  
{  
    HRESULT SetContainer(IWizardPageContainer *pContainer);  
};  
```  

##### <a name="overview"></a>Visão geral  
 Normalmente, você não implementará essa interface diretamente, mas, em vez disso, por meio da classe de modelo **WizardComponent**. Se seu componente implementar essa interface e você tiver registrado uma fábrica de classes com o Registro, seu componente receberá um ponteiro para a instância **IWizardPageContainer** quando ela for criada. Isso ajuda você, por exemplo, a acessar o Agente ou o Registro para criar outros componentes que talvez sejam necessários para seu componente.  

#### <a name="iwizarddialogcontroller-interface"></a>Interface IWizardDialogController  

```  
__interface IWizardDialogController : IUnknown  
{  
    void Initialize(ISettings *pSettings);  
    void InitPages(void);  
    void Start();  
    void Next();  
    void Finish();  
    void Previous();  
    int NumPages();  
    void Cancel();  

    HRESULT Focus(WizardButtons button);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage();  

    void ChangePage(size_t newIndex);  
    IUnknown *CurrentPage(void);  
    HRESULT GetCurrentTitle([out, retval] LPBSTR pDisplayName);  
};  
```  

 Essa interface é apenas para uso interno.  

#### <a name="iwizarddialogview-interface"></a>Interface IWizardDialogView  

```  
__interface IWizardDialogView : IUnknown  
{  
    HRESULT LoadBannerImage(LPCTSTR bannerFilename);  
    HRESULT LoadPage(LPCTSTR pageType, ISettingsProperties *pPageSettings, IWizardPageView **view);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    HRESULT Focus(WizardButtons button);  
    void EnableFinish(BOOL isFinish);  
    void Exit(int exitCode);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage(void);  
    void SetTitle(LPCTSTR title);  
    void SetPageTitle(LPCTSTR title);  
    int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType);  
    HWND GetHwnd(void);  
    void UpdateFocus(void);  
};  
```  

 Essa interface é apenas para uso interno.  

####  <a name="IWizardPageInterface"></a> Interface IWizardPage  

```  
__interface IWizardPage : IUnknown  
{  
    HRESULT SetPageSettings(ISettingsProperties *pPageSettings);  
    HINSTANCE GetInstanceHandle(void);  
    int GetDialogResourceId(void);  
    void WindowCreated(IWizardPageView *pView, IWizardPageContainer *pContainer);  
    void WindowShown(void);  
    void WindowHidden(void);  

    HRESULT NextClicked(void);  
    void ControlEvent(WORD eventId, WORD controlId);  
    void CommonControlEvent(WORD controlId, LPNMHDR pInfo, LPBOOL pCancel);  
    void UnhandledEvent(HWND hwnd, UINT message, WPARAM wParam, LPARAM lParam);  
};  
```  

##### <a name="overview"></a>Visão geral  
 Essa interface é implementada por **WizardPageImpl**; assim, normalmente não será necessário implementá-la por conta própria. O assistente chama todos esses métodos para você quando ele interage com suas páginas personalizadas.  

#### <a name="iwizardpagecontainer-interface"></a>Interface IWizardPageContainer  

```  
__interface IWizardPageContainer : IUnknown  
{  
    ILogger * Logger(void);  
    IPropertyBag * Properties(void);  
    HRESULT CreateInstance(LPCTSTR type, [out] IUnknown **ppInstance);  
    HRESULT GetService(REFIID iid, [out] IUnknown **ppInstance);  
    HRESULT ReplaceVariables(LPCTSTR source, [out] LPBSTR pDest);  
    HRESULT GotoPage(LPCTSTR pageName);  
    int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType);  
    BOOL InPreview(void);  
    HWND GetHwnd(void);  
};  
```  

##### <a name="overview"></a>Visão geral  
 Essa interface está disponível para sua página por meio do método **Container** (implementado por **WizardPageImpl**) e concede a você acesso a vários serviços do assistente.  

##### <a name="ilogger--loggervoid"></a>ILogger * Logger(void)  
 Use esse método para gravar mensagens no arquivo de log – por exemplo:  

```  
Logger()->Verbose(s_component, L"Message for log file");  
```  

##### <a name="ipropertybag--propertiesvoid"></a>IPropertyBag * Properties(void)  
 Esse método fornece acesso a variáveis de "memória", que são propriedades que estão na memória apenas enquanto o Assistente de UDI está em execução. Essas propriedades estão disponíveis para outras páginas no código ou no XML usando a sintaxe **$memoryVarName$**.  

##### <a name="hresult-createinstancelpctstr-type-out-iunknown-ppinstance"></a>HRESULT CreateInstance(LPCTSTR type, [out] IUnknown **ppInstance)  
 Esse método permite criar uma instância de qualquer componente que tenha sido registrado. No entanto, é melhor usar a função de modelo **CreateInstance**, porque ela é fortemente tipada.  

##### <a name="hresult-getservicerefiid-iid-out-iunknown-ppinstance"></a>HRESULT GetService(REFIID iid, [out] IUnknown **ppInstance)  
 Esse método permite recuperar um serviço que foi registrado. No entanto, é melhor chamar a função de modelo **GetService**, que é fortemente tipada (em vez de usar **IUnknown**).  

##### <a name="hresult-replacevariableslpctstr-source-out-lpbstr-pdest"></a>HRESULT ReplaceVariables(LPCTSTR source, [out] LPBSTR pDest)  
 Esse método lida com o trabalho com variáveis dentro dos valores de cadeia de caracteres. Ele é compatível com os formatos mostrados na Tabela 51 e na Tabela 52.  

### <a name="table-51-hresult-replacevariables"></a>Tabela 51. HRESULT ReplaceVariables  

|**Formato**|**Descrição**|  
|-|-|  
|**$Name$**|Substitui o valor de uma variável de memória por esse nome (se não houver variável de memória com o nome, o "token" será removido.)|  
|**%Name%**|Uma variável de sequência de tarefas ou uma variável de ambiente. A ordem é a seguinte:<br /><br /> 1.  Use o valor de uma variável de sequência de tarefas, se presente.<br />2.  Use o valor de uma variável de ambiente, se presente.<br />3.  Caso contrário, remova esse texto da cadeia de caracteres.|  

### <a name="table-52-hresult-parameter"></a>Tabela 52. Parâmetro HRESULT  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**Origem**|A cadeia de caracteres de entrada, que pode conter qualquer combinação das variáveis **$** e **%** ou nenhuma|  
|**pDest**|No retorno, contém uma nova cadeia de caracteres que tem todos os tokens substituídos de acordo com a Tabela 51|  

##### <a name="hresult-gotopagelpctstr-pagename"></a>HRESULT GotoPage(LPCTSTR pageName)  
 Esse método não foi totalmente testado. A ideia é que você possa alternar diretamente para uma página específica com base no nome da página, conforme definido no arquivo XML .config. Chamar esse método ignora **OnNextClicked** em sua página. Além disso, o comportamento desse método está sujeito a alterações. Portanto, use-o por sua conta e risco.  

##### <a name="int-showmessageboxlpctstr-message-lpctstr-lpcaption-uint-utype"></a>int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType)  
 Esse método exibe uma caixa de mensagem com o texto e a legenda fornecidos. O parâmetro **uType** é qualquer valor que você puder fornecer à função **MessageBox** do Win32.  

##### <a name="bool-inpreviewvoid"></a>BOOL InPreview(void)  
 Esse método retornará TRUE se você tiver iniciado o assistente no modo de "visualização" fornecendo a opção **/preview**. No modo de visualização, o botão **Avançar** nunca é desabilitado. Esse método permite ignorar o código no modo de visualização, por exemplo, que poderia causar problemas quando você não tem dados válidos na página.  

##### <a name="hwnd-gethwndvoid"></a>HWND GetHwnd(void)  
 Esse método retorna o **HWND** para a caixa de diálogo principal. Use esse método com cuidado. Em geral, a interface de programação de aplicativo do Assistente de UDI foi criada para você nunca trabalhar diretamente com os identificadores de janela.  

#### <a name="iwizardpageview-interface"></a>Interface IWizardPageView  

```  
__interface IWizardPageView : IUnknown  
{  
    HRESULT GetControlWrapper(int itemId, DialogControlTypes controlType, IUnknown **ppControl);  
    HWND GetHwnd(void);  
    HWND GetControl(int itemId);  
    HRESULT Show (void);  
    HRESULT Hide(void);  
    HRESULT Focus(int itemId);  
    IWizardPage * Page(void);  
    IFormController * Form(void);  

    HRESULT FocusWizardButton(WizardButtons button);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage(void);  
};  
```  

 Esta interface está disponível para o código em sua página por meio do método **View** (implementado por **WizardPageImpl**).  

##### <a name="hresult-getcontrolwrapperint-itemid-dialogcontroltypes-controltype-iunknown-ppcontrol"></a>HRESULT GetControlWrapper(int itemId, DialogControlTypes controlType, IUnknown \*ppControl)  
 O Assistente de UDI usa *wrappers*, que são realmente fachadas para interagir com os controles na sua página. Usar essas fachadas em vez dos controles reais torna muito mais fácil escrever testes para sua página, porque é possível fornecer fachadas fictícias em seus testes.  

 Em vez de usar esse método diretamente, é melhor usar o método de modelo **GetControlWrapper**, que é fortemente tipado, por exemplo:  

```  
PComboBox m_pLanguagePackCombo;  
GetControlWrapper(View(), IDC_MY_COMBO, CONTROL_COMBO_BOX, &m_pCombo);  
```  

##### <a name="hwnd-gethwndvoid"></a>HWND GetHwnd(void)  
 Esse método retorna o identificador de janela para sua página. Em geral, não deve ser necessário ter acesso a esse identificador de janela.  

##### <a name="hwnd-getcontrolint-itemid"></a>HWND GetControl(int itemId)  
 Se necessário, é possível chamar esse método para obter o identificador de janela para um controle em sua página. (É melhor chamar a função de modelo **GetControlWrapper**).  

##### <a name="hresult-show-void"></a>HRESULT Show (void)  
 Esse método é apenas para uso interno.  

##### <a name="hresult-hidevoid"></a>HRESULT Hide(void)  
 Esse método é apenas para uso interno.  

##### <a name="hresult-focusint-itemid"></a>HRESULT Focus(int itemId)  
 Defina o foco de entrada para um controle específico.  

##### <a name="iwizardpage--pagevoid"></a>IWizardPage * Page(void)  
 Esse método é apenas para uso interno.  

##### <a name="iformcontroller--formvoid"></a>IFormController * Form(void)  
 Esse método é apenas para uso interno.  

##### <a name="hresult-focuswizardbuttonwizardbuttons-button"></a>HRESULT FocusWizardButton(WizardButtons button)  
 Defina o foco como um dos botões do assistente. **WizardButtons** tem dois valores: **BackButton** e **NextButton**.  

##### <a name="hresult-setenablewizardbuttons-button-bool-enable"></a>HRESULT SetEnable(WizardButtons button, BOOL enable)  
 Solicite que um dos botões do assistente seja habilitado ou desabilitado. Talvez o botão não corresponda ao estado solicitado. Por exemplo, se você executar o Assistente de UDI com a opção **/preview**, os botões sempre serão habilitados. **WizardButtons** tem dois valores: **BackButton** e **NextButton**.  

##### <a name="void-showwarningmessagelpctstr-message"></a>void ShowWarningMessage(LPCTSTR message)  
 Esse método exibe uma mensagem de aviso na parte inferior da área de conteúdo da página. Essa mensagem poderá ser qualquer texto que você desejar.  

##### <a name="void-hidewarningmessagevoid"></a>void HideWarningMessage(void)  
 Oculte uma mensagem de aviso exibida com uma chamada para **ShowWarningMessage**.  

#### <a name="ixmldocument-interface"></a>Interface IXmlDocument  

```  
__interface IXmlDocument : IUnknown  
    HRESULT Load(LPCTSTR filename);  
    HRESULT LoadXml(LPCTSTR xml);  
    HRESULT Save(LPCWSTR filename);  
    HRESULT GetParseErrorMessage(LPBSTR pMessage);  
    HRESULT SelectNodes(LPCTSTR xpath, IXMLDOMNodeList **ppNodes);  
    HRESULT SelectSingleNode(LPCTSTR xpath, IXMLDOMNode **ppNode);  
    HRESULT AddSchema(LPCTSTR filename, LPCTSTR ns);  
    HRESULT AddAttribute(IXMLDOMNode *pNode, LPCWSTR name, LPCWSTR value);  
    HRESULT CreateNode(DOMNodeType type, LPCWSTR name, LPCWSTR ns, IXMLDOMNode **ppNode);  
};  
```  

##### <a name="overview"></a>Visão geral  
 Essa interface é implementada pelo componente **ID_IXmlDocument**, que é uma fachada criada para tornar mais fácil trabalhar com documentos XML em C++.  

##### <a name="hresult-loadlpctstr-filename"></a>HRESULT Load(LPCTSTR filename)  
 Esse método carrega um documento XML de um arquivo externo. Ele retornará **S_OK** se o arquivo tiver sido carregado sem erros ou **S_FALSE** se um erro tiver ocorrido. Quando há um erro, é possível obter a mensagem de erro chamando **GetParseErrorMessage**.  

##### <a name="hresult-loadxmllpctstr-xml"></a>HRESULT LoadXml(LPCTSTR xml)  
 Esse método carrega um documento XML de uma cadeia de caracteres, em vez de um arquivo externo. Diferentemente da origem da leitura do XML, o comportamento é o mesmo que o método **Load**.  

##### <a name="hresult-savelpcwstr-filename"></a>HRESULT Save(LPCWSTR filename)  
 Esse método salva o documento XML que está na memória para um arquivo externo.  

##### <a name="hresult-getparseerrormessagelpbstr-pmessage"></a>HRESULT GetParseErrorMessage(LPBSTR pMessage)  
 Esse método retornará uma nova cadeia de caracteres com a mensagem de erro do carregamento do documento XML, se houver. Ele sempre retorna **S_OK**.  

##### <a name="hresult-selectnodeslpctstr-xpath-ixmldomnodelist-ppnodes"></a>HRESULT SelectNodes(LPCTSTR xpath, IXMLDOMNodeList \**ppNodes)  
 Esse método permite que você use uma expressão XPath para recuperar uma coleção de nós do documento. Ele sempre retorna **S_OK**.  

##### <a name="hresult-selectsinglenodelpctstr-xpath-ixmldomnode-ppnode"></a>HRESULT SelectSingleNode(LPCTSTR xpath, IXMLDOMNode \**ppNode)  
 Esse método permite que você use uma expressão XPath para recuperar um nó do documento. Ele sempre retorna **S_OK**.  

##### <a name="hresult-addschemalpctstr-filename-lpctstr-ns"></a>HRESULT AddSchema(LPCTSTR filename, LPCTSTR ns)  
 Esse método adiciona o nome de um arquivo de esquema externo que será usado para validar o esquema do seu documento XML quando ele é carregado. O namespace fornecido é a cadeia de caracteres que você pode usar em consultas XPath, embora isso não tenha sido testado.  

##### <a name="hresult-addattributeixmldomnode-pnode-lpcwstr-name-lpcwstr-value"></a>HRESULT AddAttribute(IXMLDOMNode \*pNode, LPCWSTR name, LPCWSTR value)  
 Esse método adiciona um novo atributo a um nó existente no documento XML. Consulte a Tabela 53.  

### <a name="table-53-hresult-addattribute"></a>Tabela 53. HRESULT AddAttribute  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**pNode**|O nó ao qual você deseja adicionar um atributo|  
|**Nome**|Nome do novo atributo|  
|**Valor**|O valor do novo atributo|  

##### <a name="hresult-createnodedomnodetype-type-lpcwstr-name-lpcwstr-ns-ixmldomnode-ppnode"></a>HRESULT CreateNode(DOMNodeType type, LPCWSTR name, LPCWSTR ns, IXMLDOMNode \**ppNode)  
 Chame esse método para criar um nó:  

```  
Pointer<IXMLDOMNode> pNewChild  
pXmlDom->CreateNode(NODE_ELEMENT, L"MyElement", L"", &pNewChild);  
```  

 Quando você cria um nó, é possível adicioná-lo como um filho a outro nó chamando o método **appendChild** do pai.  

### <a name="helper-functions"></a>Funções auxiliares  

#### <a name="createinstance-template-function"></a>Função de modelo CreateInstance  

```  
HRESULT CreateInstance(IWizardPageContainer *pContainer, LPCTSTR type, I **ppObject)  
```  

 Essa função é definida em IWizardPageContainer.h e fornece um wrapper fortemente tipado sobre o método **IWizardPageContainer->CreateInstance** – por exemplo:  

```  
CreateInstance<IDirectory>(Container(), ID_Directory, &pDirectory);  
```  

 Esse código cria um componente **ID_Directory** para recuperar a interface **IDirectory** desse componente.  

#### <a name="getservice-template-function"></a>Função de modelo GetService  

```  
void GetService(IWizardPageContainer *pContainer, I **ppService)  
```  

 Essa função é definida em IWizardPageContainer.h e fornece um wrapper fortemente tipado sobre o método **IWizardPageContainer->GetService** – por exemplo:  

```  
GetService<ITSVariableBag>(Container(), &pTsBag);  
```  

 Essa função recupera o componente de sequência de tarefas, compatível com a interface **ITSVariableBag**. (Para **ITSVariableBag**, é possível usar o método TSVariables da classe **WizardPageImpl**).  

### <a name="udi-wizard-designer-configuration-file-schema-reference"></a>Referência de esquema de arquivo de configuração do Designer do Assistente de UDI  
 O arquivo é consumido pelo Designer do Assistente de UDI. Um arquivo separado é criado para cada arquivo .dll personalizado, que pode conter editores de página de assistente personalizada, tarefas personalizadas ou validadores personalizados. O arquivo deve terminar com *.config* e residir na pasta *pasta_de_instalação*\Bin\Config (em que *pasta_de_instalação* é a pasta na qual você instalou o MDT).  

  A Tabela 54 lista os elementos no arquivo de configuração do Designer do Assistente de UDI e suas descrições. O elemento **DesignerConfig** é o nó raiz dessa referência.  

### <a name="table-54-elements-in-the-udi-wizard-designer-configuration-file-and-their-descriptions"></a>Tabela 54. Elementos no arquivo de configuração do Designer do Assistente de UDI e suas descrições  

|**Nome do elemento**|**Descrição**|  
|-|-|  
|[DesignerConfig](#DesignerConfig)|Especifica a raiz de todos os outros elementos|  
|[DesignerMappings](#DesignerMappings)|Agrupa um conjunto de elementos [Page](#Page)|  
|[Página](#Page)|Especifica um editor de página de assistente a ser carregado no Designer do Assistente de UDI, usado para editar as configurações de uma página de assistente|  
|[Param](#Param)|Especifica um parâmetro passado para o elemento pai [Task](#Task) ou [Validator](#Validator) e corresponde a um elemento [Setter]() no arquivo de configuração do Assistente de UDI **Observação:** os atributos desse elemento serão diferentes se o pai for o elemento [Task](#Task) ou [Validator](#Validator).|  
|[Tarefa](#Task)|Especifica uma tarefa dentro da biblioteca de tarefas|  
|[TaskItem](#TaskItem)|Especifica um grupo de parâmetros passados para a tarefa|  
|[TaskLibrary](#TaskLibrary)|Agrupa um conjunto de elementos [Task](#Task)|  
|[Validator](#Validator)|Especifica um validador dentro da biblioteca de validadores|  
|[ValidatorLibrary](#ValidatorLibrary)|Agrupa um conjunto de elementos [Validator](#Validator)|  

####  <a name="DesignerConfig"></a> DesignerConfig  
 Este elemento especifica a raiz de todos os outros elementos.  

##### <a name="element-information"></a>Informações do elemento  
  A Tabela 55 fornece informações sobre o elemento [DesignerConfig](#DesignerConfig).  

### <a name="table-55-designerconfig-element-information"></a>Tabela 55. informações sobre o elemento DesignerConfig  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Um: esse elemento é obrigatório.|  
|Elementos pai|Nenhum|  
|Conteúdo|**DesignerMappings**, **TaskLibrary**, **ValidatorLibrary**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Esse elemento não tem atributos.  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  

```  
<DesignerConfig>  
   + <TaskLibrary>  
   + <ValidatorLibrary>  
   + <DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="DesignerMappings"></a> DesignerMappings  
 Esse elemento agrupa um conjunto de elementos [Page](#Page).  

##### <a name="element-information"></a>Informações do elemento  
  A Tabela 56 fornece informações sobre o elemento [DesignerMappings](#DesignerMappings).  

### <a name="table-56-designermappings-element-information"></a>Tabela 56. informações sobre o elemento DesignerMappings  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou uma dentro do elemento [DesignerConfig](#DesignerConfig) (esse elemento será opcional se não houver nenhuma página de assistente personalizada na DLL correspondente a esse arquivo de configuração do Designer do Assistente de UDI).|  
|Elementos pai|**DesignerConfig**|  
|Conteúdo|**Página**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Esse elemento não tem atributos.  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  

```  
<DesignerConfig>  
   + <TaskLibrary>  
   + <ValidatorLibrary>  
   - <DesignerMappings>  
        <Page DLL="SharedPages.dll"  
           Description="Used to display text that describes the current stagegroup"  
           Type="Microsoft.SharedPages.WelcomePage"  
           DisplayName="Welcome"   
           Image="Welcome_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.WelcomePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
        <Page DLL="OSDRefreshWizard.dll"  
           Description="Captures or restores user state data"  
           Type="Microsoft.OSDRefresh.UserStatePage"  
           DisplayName="User Data"  
           Image="UserState_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.UserStatePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
        <Page DLL="OSDRefreshWizard.dll"  
           Description="Allows selecting the image to install, target drive, and whether to format"  
           Type="Microsoft.OSDRefresh.VolumePage"  
           DisplayName="Volume"  
           Image="Volume_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.VolumePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
     </DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="Page"></a> Page  
 Esse elemento especifica um editor de página de assistente a ser carregado no Designer do Assistente de UDI, que, por sua vez, é usado para editar as configurações de uma página de assistente.  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 57 fornece informações sobre o elemento [Page](#Page).  

### <a name="table-57-page-element-information"></a>Tabela 57. informações sobre o elemento Page  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Uma ou mais para cada página de assistente definida no elemento [DesignerMappings](#DesignerMappings)|  
|Elementos pai|**DesignerMappings**|  
|Conteúdo|Qualquer conteúdo XML bem formado|  

##### <a name="element-attributes"></a>Atributos de elemento  
A Tabela 58 lista os atributos do elemento [Page](#Page) e uma descrição de cada um.  

### <a name="table-58-attributes-and-corresponding-values-for-the-page-element"></a>Tabela 58. Atributos e valores correspondentes do elemento Page  

|**Atributo**|**Descrição**|  
|-|-|  
|**Descrição**|Especifica o texto que fornece informações sobre o parâmetro, exibido no Designer do Assistente de UDI|  
|**DesignerAssembly**|Especifica o nome do arquivo .dll associado ao editor de página de assistente (o arquivo .dll deve existir na pasta *pasta_de_instalação*\Bin (em que *pasta_de_instalação* é a pasta na qual você instalou o MDT.)|  
|**DesignerType**|Especifica o nome do editor de página de assistente dentro do arquivo .dll especificado no atributo **DesignerAssembly** (esse é o tipo do Microsoft .NET do editor de página de assistente, com o namespace totalmente qualificado do Microsoft .NET).|  
|**DisplayName**|Especifica o nome amigável do editor de página, exibido no Designer do Assistente de UDI|  
|**DLL**|Especifica o nome do arquivo .dll associado à página de assistente (o arquivo .dll deve existir na pasta *pasta_de_instalação*\Templates\Distribution\Tools\\*plataforma* (em que *pasta_de_instalação* é a pasta na qual você instalou o MDT e a *plataforma* é **x86** para a versão de 32 bits ou **x64** é para a versão de 64 bits). **Observação:** certifique-se de que a arquitetura de processador de DLL corresponde à arquitetura de processador do MDT instalado. Por exemplo, se você instalou uma versão de 32 bits do MDT, use uma DLL de 32 bits para a página de assistente.|  
|**Image**|Especifica o nome de uma imagem da página que está no formato PNG. O arquivo .png deve existir na pasta *pasta_de_instalação*\Bin\Images (em que *pasta_de_instalação* é a pasta na qual você instalou o MDT.)|  
|**Tipo**|Especifica o editor de página de assistente e deve coincidir com o nome usado quando a página personalizada foi registrada|  

##### <a name="remarks"></a>Comentários  
 O Designer do Assistente de UDI usa o elemento [Page](#Page) como um modelo para criar o XML inicial para um novo assistente. O Designer do Assistente de UDI executa a validação de esquema para garantir que os elementos [Page](#Page) e os elementos filho tenham um formato válido. Esse elemento fornece um mapeamento entre o tipo de página do Assistente de UDI e as informações de que o Designer do Assistente de UDI precisa para editar e criar páginas desse tipo usando um editor de página personalizada.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="Param"></a> Param  
 Esse elemento especifica um parâmetro passado para o elemento pai [Task](#Task) ou [Validator](#Validator) e corresponde a um elemento [Setter]() no arquivo de configuração do Assistente de UDI.  

> [!NOTE]
>  Os atributos desse elemento serão diferentes se o pai for o elemento [Task](#Task) ou [Validator](#Validator).  

##### <a name="element-information"></a>Informações do elemento  
 A Tabela 59 fornece informações sobre o elemento [Param](#Param).  

### <a name="table-59-param-element-information"></a>Tabela 59. Informações sobre o elemento Param  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Uma ou mais para cada elemento pai [TaskItem](#TaskItem) ou [Validator](#Validator)|  
|Elementos pai|**TaskItem**, **Validator**|  
|Conteúdo|Qualquer conteúdo XML bem formado|  

##### <a name="element-attributes"></a>Atributos de elemento  
  A Tabela 60 lista os atributos do elemento [Param](#Param) e fornece uma descrição de cada um.  

### <a name="table-60-attributes-and-corresponding-values-for-the-param-element"></a>Tabela 60. Atributos e valores correspondentes do elemento Param  

|**Atributo**|**Descrição**|  
|-|-|  
|**Descrição**|Especifica o texto que fornece informações sobre o parâmetro, exibidas no Designer do Assistente de UDI **Observação:** esse atributo é válido apenas para o elemento [Validator](#Validator).|  
|**DisplayName**|Especifica o nome amigável do parâmetro de validador, exibido para a página do Assistente de UDI adequada no Designer do Assistente de UDI (esse nome é geralmente mais descritivo do que o atributo **Name**). **Observação:** esse atributo é válido somente para o elemento [Validator](#Validator).|  
|**Nome**|Especifica o nome do parâmetro passado para a tarefa ou validador, dependendo do elemento pai (Esse atributo se tornará o atributo **Property** em um elemento [Setter]() no arquivo de configuração do Assistente de UDI). **Observação:** esse parâmetro é usado para os elementos pai [TaskItem](#TaskItem) e [Validator](#Validator).|  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="Task"></a> Task  
 Esse elemento especifica uma tarefa dentro da biblioteca de tarefas.  

##### <a name="element-information"></a>Informações do elemento  
 A Tabela 61 fornece informações sobre o elemento [Task](#Task).  

### <a name="table-61-task-element-information"></a>Tabela 61. informações sobre o elemento Task  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Uma ou mais dentro do elemento [TaskLibrary](#TaskLibrary) (Esse elemento não será opcional se o elemento **TaskLibrary** for especificado).|  
|Elementos pai|**TaskLibrary**|  
|Conteúdo|**TaskItem**|  

##### <a name="element-attributes"></a>Atributos de elemento  
  A Tabela 62 lista os atributos do elemento [Task](#Task) e fornece uma descrição de cada um.  

### <a name="table-62-attributes-and-corresponding-values-for-the-task-element"></a>Tabela 62. Atributos e valores correspondentes do elemento Task  

|**Atributo**|**Descrição**|  
|-|-|  
|**Descrição**|Especifica o texto que fornece informações sobre a tarefa, exibido no Designer do Assistente de UDI|  
|**DLL**|Especifica o nome do arquivo .dll associado à tarefa (o arquivo .dll deve existir na *pasta_de_instalação*\Templates\Distribution\Tools\\*plataforma* (em que *pasta_de_instalação* é a pasta na qual você instalou o MDT e *plataforma* é **x86** para a versão de 32 bits ou **x64** para a versão de 64 bits).|  
|**Nome**|Especifica o nome da tarefa, exibido na página do Assistente de UDI adequada e no Designer do Assistente de UDI|  
|**Tipo**|Especifica o tipo de tarefa, registrado com o Registro de fábrica e usado para chamar uma tarefa específica dentro de um arquivo .dll|  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="TaskItem"></a> TaskItem  
 Esse elemento especifica um grupo de parâmetros passados para a tarefa.  

##### <a name="element-information"></a>Informações do elemento  
  A Tabela 63 fornece informações sobre o elemento [TaskItem](#TaskItem).  

### <a name="table-63-taskitem-element-information"></a>Tabela 63. Informações sobre elemento TaskItem  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Uma ou mais para cada elemento **Task**|  
|Elementos pai|**Tarefa**|  
|Conteúdo|**Param**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 A Tabela 64 lista os atributos do elemento [TaskItem](#TaskItem) e fornece uma descrição de cada um.  

### <a name="table-64-attribute-and-corresponding-values-for-the-taskitem-element"></a>Tabela 64. Atributos e valores correspondentes do elemento TaskItem  

|**Atributo**|**Descrição**|  
|-|-|  
|**Tipo**|Especifica o tipo de elemento que será criado no arquivo de configuração do Assistente de UDI. Um elemento XML será criado que corresponde ao valor deste atributo. Por exemplo, se o valor para esse atributo for [File](#File), um elemento **File** será criado no arquivo de configuração do Assistente de UDI.<br /><br /> No momento, os únicos valores compatíveis são:<br /><br /> -   **File**, que requer dois elementos filho [Param](#Param) (um elemento filho **Param** com o atributo **Name** definido como **Source** e outro elemento filho **Param** com o atributo **Name** definido como **Dest**)<br />-   [Setter](), que requer um elemento filho **Param**|  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="TaskLibrary"></a> TaskLibrary  
 Esse elemento agrupa um conjunto de elementos [Task](#Task).  

##### <a name="element-information"></a>Informações do elemento  
 A Tabela 65 fornece informações sobre o elemento [TaskLibrary](#TaskLibrary).  

### <a name="table-65-tasklibrary-element-information"></a>Tabela 65. Informações sobre o elemento TaskLibrary  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou uma dentro do elemento [DesignerConfig](#DesignerConfig) (esse elemento será opcional se não houver nenhuma tarefa personalizada na DLL correspondente a esse arquivo de configuração do Designer do Assistente de UDI).|  
|Elementos pai|**DesignerConfig**|  
|Conteúdo|**Tarefa**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Esse elemento não tem atributos.  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  

```  
<DesignerConfig>  
   - <TaskLibrary>  
        +<Task DLL="" Description="Executes a process with the given command line." Type="Microsoft.Wizard.ShellExecuteTask" Name="Shell Execute Task">  
        +<Task DLL="OSDRefreshWizard.dll" Description="Discovers supported applications for install." Type="Microsoft.OSDRefresh.AppDiscoveryTask" Name="Application Discovery">  
        +<Task DLL="SharedPages.dll" Description="Check to ensure a wired network connection is available." Type="Microsoft.SharedPages.WiredNetworkTask" Name="Wired Network Check">  
        +<Task DLL="OSDRefreshWizard.dll" Description="Check to ensure power source is AC (not battery)." Type="Microsoft.OSDRefresh.ACPowerTask" Name="AC Power Check">  
        +<Task DLL="" Description="Check to ensure power source is AC (not battery)." Type="Microsoft.Wizard.CopyFilesTask" Name="Copy Files Task">  
     </TaskLibrary>  
   + <ValidatorLibrary>  
   + <DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="Validator"></a> Validator  
 Esse elemento especifica um validador dentro da biblioteca de validadores.  

##### <a name="element-information"></a>Informações do elemento  
 A Tabela 66 fornece informações sobre o elemento [Validator](#Validator).  

### <a name="table-66-validator-element-information"></a>Tabela 66. informações sobre o elemento Validator  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou mais dentro de cada elemento [ValidatorLibrary](#ValidatorLibrary) (esse elemento é opcional).|  
|Elementos pai|**ValidatorLibrary**|  
|Conteúdo|**Param**|  

##### <a name="element-attributes"></a>Atributos de elemento  
A Tabela 67 lista os atributos do elemento [Validator](#Validator) e fornece uma descrição de cada um.  

### <a name="table-67-attributes-and-corresponding-values-for-the-validator-element"></a>Tabela 67. Atributos e valores correspondentes do elemento Validator  

|**Atributo**|**Descrição**|  
|-|-|  
|**Descrição**|Especifica o texto que fornece informações sobre o validador, exibido no Designer do Assistente de UDI|  
|**DisplayName**|Especifica o nome amigável do validador exibido no Designer do Assistente de UDI (esse nome é geralmente mais descritivo do que o atributo **Name**).|  
|**DLL**|Especifica o nome do arquivo .dll associado ao validador (o arquivo .dll deve existir na pasta *pasta_de_instalação*\Templates\Distribution\Tools\\*plataforma* (em que *pasta_de_instalação* é a pasta na qual você instalou o MDT e *plataforma* é **x86** para a versão de 32 bits ou **x64** para a versão de 64 bits).|  
|**Nome**|Especifica o nome do validador, exibido na página do Assistente de UDI adequada e no Designer do Assistente de UDI|  
|**Tipo**|Especifica o tipo de validador, registrado com o fator de Registro e usado para chamar um validador específico dentro de um arquivo .dll|  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="ValidatorLibrary"></a> ValidatorLibrary  
 Esse elemento agrupa um conjunto de elementos [Validator](#Validator).  

##### <a name="element-information"></a>Informações do elemento  
 A Tabela 68 fornece informações sobre o elemento [ValidatorLibrary](#ValidatorLibrary).  

### <a name="table-68-validatorlibrary-element-information"></a>Tabela 68. Informações sobre o elemento ValidatorLibrary  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou uma dentro do elemento [DesignerConfig](#DesignerConfig) (esse elemento será opcional se não houver nenhum validador personalizado na DLL correspondente a esse arquivo de configuração do Designer do Assistente de UDI).|  
|Elementos pai|**DesignerConfig**|  
|Conteúdo|**Validator**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Esse elemento não tem atributos.  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 <DesignerConfig\>   + <TaskLibrary\>   – <ValidatorLibrary\>        +<Validator DLL="" Description="Requer um texto em um campo" Type="Microsoft.Wizard.Validation.NonEmpty" Name="NonEmpty"\>        +<Validator DLL="" Description="Não permite que determinados caracteres estejam em um campo" Type="Microsoft.Wizard.Validation.InvalidChars" Name="InvalidChars"\>        +<Validator DLL="" Description="Deve seguir um padrão predefinido" Type="Microsoft.Wizard.Validation.RegEx" Name="NamedPattern"\>        +<Validator DLL="" Description="Exige que o conteúdo corresponda a uma expressão regular" Type="Microsoft.Wizard.Validation.RegEx" Name="RegEx"\>     </ValidatorLibrary\>   + <DesignerMappings\></DesignerConfig\>  

## <a name="udi-wizard-designer-reference"></a>Referência do Designer do Assistente de UDI  

### <a name="controls"></a>Controles  
 Os controles usados para criar editores de página de assistente personalizada para uso no Designer do Assistente de UDI são instâncias **UserControl** do WPF. A Tabela 69 lista os controles que você pode usar para criar editores de página de assistente personalizada.  

### <a name="table-69-controls-that-can-be-used-to-create-custom-wizard-page-editors"></a>Tabela 69. Controles que podem ser usados para criar editores de página de assistente personalizada  

|Controle|Descrição|  
|-|-|  
|[CollectionTControl](#CollectionTControl)|Este controle é usado para editar os dados armazenados no elemento [Data](#Data) dentro de um elemento [Page](#Page).|  
|[FieldElementControl](#FieldElementControl)|Esse controle é usado para editar um campo, que normalmente está vinculado a um controle TextBox na página .xaml.|  
|[SetterControl](#SetterControl)|Esse controle é usado para modificar o valor de um elemento [setter]() no arquivo de configuração do Assistente de UDI.|  

####  <a name="CollectionTControl"></a> CollectionTControl  
 Esse controle fornece vários recursos para edição de dados. A melhor maneira de aprender a usar esse controle é examinar o exemplo, que mostra como editar dados no elemento **Data** de uma página. Em particular, o exemplo mostra como adicionar, remover e editar itens nesse controle.  

####  <a name="FieldElementControl"></a> FieldElementControl  
 Use esse controle para editar um campo, que normalmente está vinculado a um controle **TextBox** na página .xaml.  

##### <a name="example"></a>Exemplo  
 O trecho a seguir de um arquivo .xaml ilustra o uso de **FieldElementControl** para configurar o valor padrão de um campo em uma página de assistente que usa um controle filho **TextBox**:  

```  
<Controls:FieldElementControl  
Width="450"  
Margin="0,5"  
FieldData="{Binding DataContext.Location, ElementName=ControlRoot}"  
HeaderText="Location Combo Box"  
InstructionText="Here you can configure the behavior of the location combo box."  
HideValidationTab="True">  

<TextBox Text="{Binding FieldData.DefaultValue,  
 UpdateSourceTrigger=PropertyChanged,  
 Mode=TwoWay}"/>  
</Controls:FieldElementControl>  
```  

##### <a name="properties"></a>Propriedades  

###### <a name="fielddata"></a>FieldData  
 A propriedade de cadeia de caracteres contém informações para conectar o **FieldElementControl** ao XML subjacente do campo. A conexão é feita com uma propriedade da interface do editor de página. O trecho a seguir de um arquivo .xaml ilustra o uso da propriedade **FieldData**:  

```  
FieldData="{Binding DataContext.Location, ElementName=ControlRoot}"  
```  

 Nesse trecho, a interface do editor de página é chamada **ControlRoot** e é especificada no parâmetro **ElementName**. A associação é executada para a propriedade **DataContext.Location** da interface do editor de página **ControlRoot**. **DataContext** é um modelo de exibição que aponta para o elemento [Page](#Page) dentro do arquivo de configuração do Assistente de UDI. **Local** é uma propriedade da exibição que retorna uma lista de possíveis locais e é definida por um elemento [Data](#Data) dentro do arquivo de configuração do Assistente de UDI. Cada local é definido por um elemento [DataItem](#DataItem) dentro do arquivo de configuração do Assistente de UDI.  

###### <a name="headertext"></a>HeaderText  
 Esta propriedade de cadeia de caracteres permite que você especifique um cabeçalho para o controle [FieldElementControl](#FieldElementControl). O cabeçalho funciona como um título para o controle e é formatado como texto laranja em negrito exibido imediatamente acima do controle.  

###### <a name="instructiontext"></a>InstructionText  
 Essa propriedade de cadeia de caracteres permite especificar um texto informativo para o controle [FieldElementControl](#FieldElementControl). Normalmente, o texto é usado para fornecer uma breve descrição do campo e explicar como a configuração do campo afeta a página de assistente correspondente.  

###### <a name="hideenablebutton"></a>HideEnableButton  
 Essa propriedade booliana permite controlar a visibilidade do botão que altera o estado entre **Desbloqueado** e **Bloqueado** (habilitado ou desabilitado). Se definido como:  

-   **True**, o botão não está visível  

-   **False**, o botão está visível (esse é o valor padrão).  

###### <a name="hidedefaulttab"></a>HideDefaultTab  
 Essa propriedade booliana permite controlar a visibilidade da seção que contém o controle usado para definir o valor padrão. Embora a propriedade se refira a uma guia, não há nenhuma guia no [FieldElementControl](#FieldElementControl), mas há uma seção que pode ser ocultada. Se definido como:  

-   **True**, a seção não está visível  

-   **False**, a seção está visível (esse é o valor padrão).  

###### <a name="hideborder"></a>HideBorder  
 Essa propriedade booliana permite controlar a visibilidade da borda ao redor do controle de campo. Se definido como:  

-   **True**, a borda não está visível  

-   **False**, a borda está visível (esse é o valor padrão).  

###### <a name="hideimage"></a>HideImage  
 Essa propriedade booliana permite controlar a visibilidade da imagem que a propriedade **FieldImageSource** configura. Se definido como:  

-   **True**, a imagem não está visível  

-   **False**, a imagem está visível (esse é o valor padrão).  

###### <a name="hidevalidationtab"></a>HideValidationTab  
 Essa propriedade booliana permite controlar a visibilidade da seção em que a lista de validadores é gerenciada. Embora a propriedade se refira a uma guia, não há nenhuma guia no [FieldElementControl](#FieldElementControl), mas há uma seção que pode ser ocultada. Se definido como:  

-   **True**, a seção não está visível  

-   **False**, a seção está visível (esse é o valor padrão).  

###### <a name="hidesummarytab"></a>HideSummaryTab  
 Essa propriedade booliana permite controlar a visibilidade da seção na qual você configura a legenda de resumo do campo. A legenda e o valor correspondente do campo são exibidos em um tipo de página de assistente **SummaryPage** em um fluxo de estágio. Embora a propriedade se refira a uma guia, não há nenhuma guia no [FieldElementControl](#FieldElementControl), mas há uma seção que pode ser ocultada. Se definido como:  

-   **True**, a seção não está visível  

-   **False**, a seção está visível (esse é o valor padrão).  

###### <a name="hidetasksequencetab"></a>HideTaskSequenceTab  
 Essa propriedade booliana permite controlar a visibilidade da seção na qual você configura a variável de sequência de tarefas que corresponde ao campo. Embora a propriedade se refira a uma guia, não há nenhuma guia no [FieldElementControl](#FieldElementControl), mas há uma seção que pode ser ocultada. Se definido como:  

-   **True**, a seção não está visível  

-   **False**, a seção está visível (esse é o valor padrão).  


####  <a name="SetterControl"></a> SetterControl  
 Use esse controle para modificar o valor de um elemento [Setter]() no arquivo de configuração do Assistente de UDI. Esse controle contém um controle filho usado para modificar o valor do elemento **setter**.  

##### <a name="example"></a>Exemplo  
 O trecho a seguir de um arquivo .xaml ilustra o uso do **SetterControl** para modificar um elemento [Setter]() nomeado **KeyLocationSetter** usando um controle filho **TextBox**.  

```  
<Controls:SetterControl Margin="5"  
        Width="450"  
        HeaderText="Title text"  
        SetterData="{Binding KeyLocationSetter}"   
        InstructionText="What this means…"  
        HorizontalAlignment="Left">  

    <TextBox  
                   Margin="0,3"  
                   Text="{Binding SetterData.SetterValue, Mode=TwoWay, UpdateSourceTrigger=PropertyChanged}"  
    />  

</Controls:SetterControl>  
```  

##### <a name="properties"></a>Propriedades  

###### <a name="setterdata"></a>SetterData  
 É necessário associar isso a uma propriedade da sua exibição ou modelo de exibição que se conecta ao setter. Fazer isso é semelhante à maneira como você se associaria a um campo, conforme descrito para **FieldElementControl**.  

###### <a name="headertext"></a>HeaderText  
 Essa propriedade permite definir o texto que será exibido no cabeçalho do controle. Pense nessa propriedade como um título para o controle; por padrão, ela é exibida como texto laranja em negrito.  

###### <a name="instructiontext"></a>InstructionText  
 Defina essa propriedade como o texto que você deseja que seja exibido embaixo do cabeçalho; normalmente, o texto de instrução que informa o usuário do seu editor personalizado quando e por que conviria modificar o comportamento do campo.  

### <a name="interfaces"></a>Interfaces  
A Tabela 70 lista as interfaces que você pode usar para criar editores de página de assistente personalizada.  

### <a name="table-70-interfaces-that-can-be-used-to-create-custom-wizard-page-editors"></a>Tabela 70. Interfaces que podem ser usadas para criar editores de página de assistente personalizada  

|**Interface**|**Descrição**|  
|-|-|  
|[IDataService](#IDataService)|Use esta interface para conectar campos aos elementos **Data** no arquivo de configuração do Assistente de UDI.|  
|[IMessageBoxService](#IMessageBoxService)|Essa interface fornece acesso aos métodos que podem ser usados para exibir caixas de mensagem.|  

####  <a name="IDataService"></a> IDataService  
 Essa interface contém várias propriedades e métodos, mas há apenas uma propriedade que você provavelmente precise. Essa propriedade é a única documentada aqui.  

 É possível usar a injeção de dependência para obter um ponteiro para essa interface usando um código como este em sua classe:  

```  
[Dependency]  
public IDataService DataService { get; set; }  
```  

##### <a name="properties"></a>Propriedades  
 A Tabela 71 lista as propriedades da interface **IDataService**.  

### <a name="table-71-properties-for-the-idataservice-interface"></a>Tabela 71. Propriedades da interface IDataService  

|**Interface**|**Descrição**|  
|-|-|  
|[CurrentPage](#CurrentPage)|Essa propriedade fornece acesso aos elementos XML, atributos e valores embaixo do contexto da página atual que está sendo editada no arquivo de configuração do Assistente de UDI|  

######  <a name="CurrentPage"></a> CurrentPage  

```  
XElement CurrentPage { get; set; }  
```  

 Essa propriedade oferece acesso ao XML para a página atual. Você nunca deve definir essa propriedade, mas sinta-se livre para modificar o XML da sua página. O editor de página de exemplo mostra exemplos de como modificar o XML. Use essa propriedade principalmente quando você tiver dados personalizados. Para obter campos e propriedades (setters), é possível usar controles predefinidos que cuidam de todos os detalhes.  

####  <a name="IMessageBoxService"></a> IMessageBoxService  
 Essa interface fornece acesso aos métodos que podem ser usados para exibir caixas de mensagem. Talvez você esteja se perguntando por que é necessária uma interface para exibir uma caixa de mensagem. A realidade é que ela não é necessária: a Microsoft usa essa interface com o código, porque ela auxilia a escrever testes automatizados para páginas de designer.  

 No entanto, usar esses métodos proporciona um benefício útil: as caixas de diálogo sempre têm o "proprietário" definido como o Assistente de UDI, que garante que a caixa de diálogo seja agrupada corretamente com a janela principal.  

 É possível usar a injeção de dependência para obter um ponteiro para essa interface usando um código como este em sua classe:  

```  
[Dependency]  
public IMessageBoxService MessageBoxes { get; set; }  
```  

##### <a name="methods"></a>Métodos  
 A Tabela 72 lista os métodos para a interface **IMessageBoxService**.  

### <a name="table-72-methods-for-the-imessageboxservice-interface"></a>Tabela 72. Métodos para a interface IMessageBoxService  

|**Método**|**Descrição**|  
|-|-|  
|[ShowMessageBox](#ShowMessageBox)|Esse método sobrecarregado é usado para exibir uma caixa de mensagem com os seguintes membros:<br /><br /> -   [ShowMessageBox(String message, String caption, MessageBoxImage icon)](#ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon)<br />-   [ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)](#ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon)<br />-   [ShowMessageBox(Exception exception)](#ShowMessageBox_Exception_exception)|  
|[ShowDialogWindow](#ShowDialogWindow)|Use esse método para criar uma caixa de diálogo.|  
|[ShowWizardWindow](#ShowWizardWindow)|Use esse método para exibir um editor personalizado dentro de uma caixa de diálogo que inclui os botões de navegação **Avançar** e **Voltar**.|  

######  <a name="ShowMessageBox"></a> ShowMessageBox  
 Esse método exibe uma caixa de mensagem que é um filho do editor de página do assistente personalizada. Esse membro está sobrecarregado: a Tabela 73 contém uma lista dos membros e uma breve descrição de cada um. Para obter informações completas sobre cada membro (incluindo sintaxe, uso e exemplos), consulte a seção que corresponde a cada membro.  

### <a name="table-73-overloaded-members-for-the-showmessagbox-method"></a>Tabela 73. Membros sobrecarregados para o método ShowMessagBox  

|Membro|Descrição|  
|-|-|  
|[ShowMessageBox(String message, String caption, MessageBoxImage icon)](#ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon)|Exibe uma caixa de mensagem com um ícone e um botão **OK**|  
|[ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)](#ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon)|Exibe uma caixa de mensagem com um ícone e diferentes combinações possíveis de botões|  
|[ShowMessageBox(Exception exception)](#ShowMessageBox_Exception_exception)|Exibe uma caixa de mensagem que fornece informações sobre uma exceção e tem um botão **OK**|  

######  <a name="ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon"></a> ShowMessageBox(mensagem da cadeia de caracteres, legenda da cadeia de caracteres, ícone MessageBoxImage)  

```  
void ShowMessageBox(String message, String caption, MessageBoxImage icon);  
```  

 Esse método exibe uma caixa de mensagem com um botão **OK**. Consulte a Tabela 74.  

### <a name="table-74-parameters-for-the-showmessageboxstring-message-string-caption-messageboximage-icon-method"></a>Tabela 74. Parâmetros para o método ShowMessageBox(mensagem String, legenda String, ícone MessageBoxImage) Method  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**message**|A mensagem a ser exibida na área de conteúdo da caixa de mensagem|  
|**caption**|O texto a ser mostrado na barra de título da caixa de diálogo|  
|**icon**|O tipo de ícone a ser mostrado na caia de mensagem|  

######  <a name="ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon"></a> ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)  

```  
MessageBoxResult ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon);  
```  

 Esse método exibe uma caixa de mensagem com o conjunto de botões que você deseja mostrar e relata em qual botão você clicou. Consulte a Tabela 75.  

### <a name="table-75-parameters-for-the-showmessageboxstring-message-string-caption-messageboxbutton-button-messageboximage-icon-method"></a>Tabela 75. Parâmetros para o método ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**message**|A mensagem a ser exibida na área de conteúdo da caixa de mensagem|  
|**caption**|O texto a ser mostrado na barra de título da caixa de diálogo|  
|**button**|Quais botões mostrar|  
|**icon**|O tipo de ícone a ser mostrado na caia de mensagem|  

######  <a name="ShowMessageBox_Exception_exception"></a> ShowMessageBox(Exception exception)  

```  
void ShowMessageBox(Exception exception);  
```  

 Esse método exibe uma caixa de mensagem que relata informações sobre uma exceção. Essa caixa de mensagem tem um único botão **OK**. Consulte a Tabela 76.  

### <a name="table-76-parameters-for-the-showmessageboxexception-exception-method"></a>Tabela 76. Parâmetros para o método ShowMessageBox(Exception exception)  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**exception**|A exceção que você deseja relatar (a caixa de diálogo usa **exception.Message** como o conteúdo).|  

######  <a name="ShowDialogWindow"></a> ShowDialogWindow  

```  
void ShowDialogWindow(Type viewType, DialogInteraction dialogPayload);  
```  

 Esse método cria uma nova caixa de diálogo, cujo conteúdo é o texto fornecido no parâmetro **viewType**. O Designer de UDI cria uma nova instância desse tipo e a encapsula em uma caixa de diálogo que tem os botões **OK** e **Cancelar**.  

 Passe dados para seu controle usando o parâmetro dialogPayload. A solução **SampleEditor** no diretório do SDK tem um exemplo de como usar essa funcionalidade.  

######  <a name="ShowWizardWindow"></a> ShowWizardWindow  

```  
void ShowWizardWindow(Type viewType, DialogInteraction dialogPayload);  
```  

 Esse método permite exibir um editor personalizado dentro de uma caixa de diálogo que inclui os botões de navegação **Avançar** e **Voltar**. A Microsoft não forneceu um exemplo de como usar esse método.  

###  <a name="UDIWizardConfigurationFileSchemaReference"></a> Referência de esquema de arquivo de configuração do Assistente de UDI  
 Esse arquivo é consumido pelo Assistente de UDI e configurado pelo Designer do Assistente de UDI. Esse arquivo é usado para configurar:  

-   As páginas de assistente exibidas no Assistente de UDI  

-   A sequência das páginas de assistente no Assistente de UDI  

-   As configurações dos campos em cada página de assistente  

-   Os StageGroups disponíveis no Designer do Assistente de UDI  

-   Os estágios disponíveis dentro de cada assistente de implantação no Designer do Assistente de UDI  

  A Tabela 77 lista os elementos no arquivo de configuração do Assistente de UDI e suas descrições. O elemento **Wizard** é o nó raiz dessa referência.  

### <a name="table-77-elements-in-the-udi-wizard-configuration-file-and-their-descriptions"></a>Tabela 77. Elementos no arquivo de configuração do Assistente de UDI e suas descrições  

|**Nome do elemento**|**Descrição**|  
|-|-|  
|[Data](#Data)|Agrupa os elementos individuais [DataItem](#DataItem) dentro de um elemento [Page](#Page) e é nomeado pelo atributo **Name**.|  
|[DataItem](#DataItem)|Agrupa os elementos individuais [Setter]() dentro de um elemento [Page](#Page). É possível criar dados hierárquicos incluindo um ou mais elementos [Data](#Data) dentro de um elemento [DataItem](#DataItem). Cada elemento **DataItem** representa um item individual. Por exemplo, uma lista de unidades disponíveis pode ter um **DataItem** para o nome de exibição e outro elemento **DataItem** para a letra da unidade correspondente.|  
|[Padrão](#Default)|Especifica um valor padrão para o campo especificado no elemento [Field](#Field) ou [RadioGroup](#RadioGroup). O padrão é definido como o valor agrupado por esse elemento.|  
|[DLL](#DLL)|Especifica uma DLL que deve ser carregada e referenciada pelo Assistente de UDI e pelo Designer do Assistente de UDI.|  
|[DLLs](#DLLs)|Agrupa os elementos individuais [DLL](#DLL).|  
|[Erro](#Error)|Especifica um possível código de erro que pode ser retornado por uma tarefa. O valor do código de erro é retornado pelo **HRESULT** da tarefa e interceptado por esse elemento para fornecer informações mais específicas sobre o erro.|  
|[ExitCode](#ExitCode)|Especifica um possível código de saída para uma tarefa. Os códigos de saída são códigos de retorno esperados pela tarefa. Crie um elemento **ExitCode** para cada código de saída possível. Caso contrário, é possível especificar um asterisco (\*) no atributo **Valor** para manipular códigos de retorno não listados em outros elementos **ExitCode**.|  
|[ExitCodes](#ExitCodes)|Agrupa um conjunto de elementos [ExitCode](#ExitCode) e [Error](#Error) para um elemento [Task](#Task) ou um elemento **Error**.|  
|[Field](#Field)|Especifica uma instância de um controle em um elemento [Page](#Page) usado para fornecer personalização com XML. Nem todos os controles permitem a personalização com XML – apenas controles que usam o elemento [Field](#Field).|  
|[Fields](#Fields)|Agrupa os elementos individuais [Field](#Field) dentro de um elemento [Page](#Page).|  
|[File](#File)|Especifica a origem e o destino de uma operação de cópia de arquivo usando o tipo de tarefa **Microsoft.Wizard.CopyFilesTask**. É possível incluir um elemento **File** separado para copiar mais de um arquivo em uma única tarefa.|  
|[Página](#Page)|Especifica uma instância de uma página e inclui todas as configurações da página.|  
|[PageRef](#PageRef)|Especifica uma referência a uma instância de uma página dentro de um [Stage](#Stage) dentro de um [StageGroup](#StageGroup).|  
|[Pages](#Pages)|Agrupa os elementos individuais [Page](#Page).|  
|[RadioGroup](#RadioGroup)|Especifica um grupo de botões de opção em um elemento [Field](#Field).|  
|[StageGroup](#StageGroup)|Especifica um grupo de um ou mais estágios.|  
|[StageGroups](#StageGroups)|Agrupa um conjunto de grupos de estágio dentro de um arquivo de configuração do Assistente de UDI.|  
|[Setter]()|Especifica uma configuração de propriedade de um valor para uma propriedade nomeada na propriedade **Property**.|  
|[Stage](#Stage)|Especifica um estágio dentro de um [StageGroup](#StageGroup) e contém um ou mais elementos [PageRef](#PageRef).|  
|[Style](#Style)|Agrupa os elementos individuais [setter]() que configuram a aparência do Assistente de UDI, incluindo o título mostrado na parte superior do assistente e a imagem da faixa mostrada no Assistente de UDI.|  
|[Tarefa](#Task)|Especifica uma tarefa que deve ser executada na página especificada no elemento pai [Page](#Page).|  
|[Tarefas](#Tasks)|Agrupa um conjunto de tarefas para um elemento [Page](#Page).|  
|[Validator](#Validator)|Especifica um validador para o controle de campo especificado no elemento pai [Field](#Field).|  
|[Wizard](#Wizard)|Especifica a raiz de todos os outros elementos.|  

####  <a name="Data"></a> Data  
 Esse elemento agrupa os elementos individuais [DataItem](#DataItem) dentro de um elemento [Page](#Page) e é nomeado pelo atributo **Name**.  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 78 fornece informações sobre o elemento [Data](#Data).  

### <a name="table-78-data-element-information"></a>Tabela 78. Informações sobre o elemento Data  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou mais dentro de cada elemento [Page](#Page) (Esse elemento é opcional.)|  
|Elementos pai|**Page**, **DataItem**|  
|Conteúdo|**DataItem**, **Setter**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 A Tabela 79 lista os atributos do elemento [Data](#Data) e fornece uma descrição de cada um.  

### <a name="table-79-attributes-and-corresponding-values-for-the-data-element"></a>Tabela 79. Atributos e valores correspondentes do elemento Data  

|**Atributo**|**Descrição**|  
|-|-|  
|**Nome**|Especifica o nome do elemento [Data](#Data)|  

##### <a name="remarks"></a>Comentários  
 O atributo **Name** permite que o código recupere um conjunto de dados específico.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="DataItem"></a> DataItem  
 Esse elemento agrupa os elementos individuais [Setter]() dentro de um elemento [Page](#Page). É possível criar dados hierárquicos incluindo um ou mais elementos [Data](#Data) dentro de um elemento [DataItem](#DataItem). Cada elemento **DataItem** representa um item individual. Por exemplo, uma lista de unidades disponíveis pode ter um **DataItem** para o nome de exibição e outro elemento **DataItem** para a letra da unidade correspondente.  

##### <a name="element-information"></a>Informações do elemento  
 A Tabela 80 fornece informações sobre o elemento [DataItem](#DataItem).  

### <a name="table-80-dataitem-element-information"></a>Tabela 80. Informações sobre o elemento DataItem  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou mais dentro de cada elemento [Data](#Data) (esse elemento é opcional).|  
|Elementos pai|**Data**|  
|Conteúdo|**Data**, **Setter**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Esse elemento não tem atributos.  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

#### <a name="default"></a>Padrão  
 Esse elemento especifica um valor padrão para o campo especificado no elemento [Field](#Field) ou [RadioGroup](#RadioGroup). O padrão é definido como o valor que esse elemento agrupa.  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 81 fornece informações sobre o elemento [Default](#Default).  

### <a name="table-81-default-element-information"></a>Tabela 81. Informações sobre o elemento Default  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências |Zero ou mais dentro de um elemento [Field](#Field) ou [RadioGroup](#RadioGroup) (esse elemento é opcional).|  
|Elementos pai|**Field**, **RadioGroup**|  
|Conteúdo|Pode ser qualquer conteúdo XML bem formado, mas normalmente é o texto padrão|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Esse elemento não tem atributos.  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 No exemplo a seguir, o padrão para o campo **TimeZone** é definido como "Hora Padrão do Pacífico":  

```  
<Field Name="TimeZone" Enabled="true" VarName="OSDTimeZone" Summary="Time Zone:">  
  <Default>Pacific Standard Time</Default>  
```  

####  <a name="DLL"></a> DLL  
 Esse elemento especifica uma DLL para o Assistente de UDI e para o Designer do Assistente de UDI carregarem e referenciarem.  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 82 fornece informações sobre o elemento [DLL](#DLL).  

### <a name="table-82-dll-element-information"></a>Tabela 82. Informações sobre o elemento DLL  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Uma ou mais dentro do elemento [DLLs](#DLLs)|  
|Elemento pai|**DLLs**|  
|Conteúdo|Nenhum conteúdo permitido para este elemento|  

##### <a name="element-attributes"></a>Atributos de elemento  
 A Tabela 83 lista os atributos do elemento [DLL](#DLL) e fornece uma descrição de cada um.  

### <a name="table-83-attributes-and-corresponding-values-for-the-dll-element"></a>Tabela 83. Atributos e valores correspondentes do elemento DLL  

|**Atributo**|**Descrição**|  
|-|-|  
|Name|Especifica o nome da DLL para o Assistente de UDI e o Designer do Assistente de UDI a ser referenciado|  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  

```  
<DLLs>  
  <DLL Name="OSDRefreshWizard.dll" />   
  <DLL Name="SharedPages.dll" />  
</DLLs>  
```  

####  <a name="DLLs"></a> DLLs  
 Esse elemento agrupa os elementos individuais [DLL](#DLL).  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 84 fornece informações sobre o elemento [DLLs](#DLLs).  

### <a name="table-84-dlls-element-information"></a>Tabela 84. Informações sobre o elemento DLLs  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Um|  
|Elementos pai|**Wizard**|  
|Conteúdo|**DLL**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Esse elemento não tem atributos.  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  

```  
<DLLs>  
   <DLL Name="OSDRefreshWizard.dll" />  
   <DLL Name="SharedPages.dll" />   
</DLLs>  
```  

####  <a name="Error"></a> Error  
 Esse elemento especifica um possível código de erro que uma tarefa pode retornar. O valor do código de erro é retornado e interceptado pelo **HRESULT** da tarefa para fornecer informações mais específicas sobre o erro.  

##### <a name="element-information"></a>Informações do elemento  
 A Tabela 85 fornece informações sobre o elemento [Error](#Error).  

### <a name="table-85-error-element-information"></a>Tabela 85. Informações sobre o elemento Error  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou mais dentro de cada elemento [ExitCode](#ExitCode) (Esse elemento é opcional.)|  
|Elementos pai|**ExitCodes**|  
|Conteúdo|Qualquer conteúdo XML bem formado|  

##### <a name="element-attributes"></a>Atributos de elemento  
 A Tabela 86 lista os atributos do elemento [Error](#Error) e fornece uma descrição de cada um.  

###  

|**Atributo**|**Descrição**|  
|-|-|  
|**Estado**|Especifica o estado de retorno de uma tarefa que encontrou um erro. Normalmente, o valor desse atributo é definido como Erro. Esse valor é exibido na coluna **Estado** na página de assistente no Assistente de UDI.|  
|**Text**|Especifica o texto descritivo sobre a condição de erro que a tarefa encontrou.|  
|**Tipo**|Especifica se esse elemento representa um erro, aviso ou êxito. O valor especificado em **Type** deve ser exclusivo dentro de um elemento [ExitCodes](#ExitCodes). Estes são os valores válidos para este elemento:<br /><br /> -   **0.** O elemento representa um êxito.<br />-   **1.** O elemento representa um aviso.<br />-   **-1.** O elemento representa um erro.|  
|**Valor**|Especifica o valor do código que a tarefa retornou como um valor numérico. Especificar o valor de um asterisco (*) indica o elemento padrão para códigos de retorno que não estão listados em outros elementos [Error](#Error).|  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="ExitCode"></a> ExitCode  
 Esse elemento especifica um possível código de saída para uma tarefa. Os códigos de saída são códigos de retorno esperados pela tarefa. Crie um elemento **ExitCode** para cada código de saída possível. Caso contrário, é possível especificar um asterisco (\*) no atributo **Valor** para manipular códigos de retorno não listados em outros elementos **ExitCode**.  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 87 fornece informações sobre o elemento [ExitCode](#ExitCode).  

### <a name="table-87-exitcode-element-information"></a>Tabela 87. Informações sobre o elemento ExitCode  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou mais dentro de cada elemento [ExitCodes](#ExitCodes) (Esse elemento é opcional.)|  
|Elementos pai|**ExitCodes**|  
|Conteúdo|Pelo menos um elemento [ExitCode](#ExitCode) e zero ou mais elementos [Error](#Error)|  

##### <a name="element-attributes"></a>Atributos de elemento  
A Tabela 88 lista os atributos do elemento [ExitCode](#ExitCode) e fornece uma descrição de cada um.  

### <a name="table-88-attributes-and-corresponding-values-for-the-exitcode-element"></a>Tabela 88. Atributos e valores correspondentes do elemento ExitCode  

|**Atributo**|Descrição|  
|-|-|  
|**Estado**|Especifica o estado de retorno de uma tarefa. O valor desse atributo é exibido na coluna **Estado** na página de assistente correspondente no Assistente de UDI. É possível usar quaisquer valores para esse atributo que sejam relevantes para sua tarefa. A seguir estão valores típicos usados para esse atributo:<br /><br /> – Êxito<br />– Aviso<br />– Erro|  
|**Text**|Especifica o texto descritivo sobre o código de existência da tarefa.|  
|**Tipo**|Especifica se esse elemento representa um erro, aviso ou êxito. O valor especificado no tipo deve ser exclusivo dentro de um elemento [ExitCodes](#ExitCodes). Estes são os valores válidos para este elemento:<br /><br /> -   **0.** O elemento representa um êxito.<br />-   **1.** O elemento representa um aviso.<br />-   **-1.** O elemento representa um erro.|  
|**Valor**|Especifica o valor do código que a tarefa retornou como um valor numérico. Especificar o valor de um asterisco (*) indica o elemento padrão para códigos de retorno que não estão listados em outros elementos [ExitCode](#ExitCode).|  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="ExitCodes"></a> ExitCodes  
 Esse elemento agrupa um conjunto de elementos [ExitCode](#ExitCode) e [Error](#Error) para um elemento [Task](#Task) ou um elemento **Error**.  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 89 fornece informações sobre o elemento [ExitCodes](#ExitCodes).  

### <a name="table-89-exitcodes-element-information"></a>Tabela 89. Informações sobre o elemento ExitCodes  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Uma dentro de cada elemento [Task](#Task)|  
|Elementos pai|**Tarefa**|  
|Conteúdo|**Error**, **ExitCode**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Esse elemento não tem atributos.  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="Field"></a> Field  
 Esse elemento especifica uma instância de um controle em um elemento [Page](#Page) usado para fornecer personalização com XML. Nem todos os controles permitem a personalização com XML – apenas controles que usam o elemento [Field](#Field).  

##### <a name="element-information"></a>Informações do elemento  
 A Tabela 90 fornece informações sobre o elemento [Field](#Field).  

### <a name="table-90-field-element-information"></a>Tabela 90. Informações sobre o elemento Field  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou mais dentro de cada elemento [Field](#Field) (esse elemento é opcional).|  
|Elementos pai|**Fields**|  
|Conteúdo|**Default**, **Validator**|  

##### <a name="element-attributes"></a>Atributos de elemento  
A Tabela 91 lista os atributos do elemento [Field](#Field) e fornece uma descrição de cada um.  

### <a name="table-91-attributes-and-corresponding-values-for-the-field-element"></a>Tabela 91. Atributos e valores correspondentes do elemento Field  

|**Atributo**|**Descrição**|  
|-|-|  
|**Enabled**|Especifica se o campo está habilitado para a entrada do usuário (o atributo pode ser definido como True ou False).|  
|**Nome**|Especifica o nome do campo|  
|**Resumo**|Especifica o texto descritivo exibido na página de assistente de **Resumo** para o valor definido por esse campo|  
|**VarName**|Especifica o nome da variável de sequência de tarefas lido ou configurado usando o campo no elemento pai [Field](#Field)|  

##### <a name="remarks"></a>Comentários  
 Esse elemento pode conter zero ou mais elementos [Default](#Default) e zero ou mais elementos [Validator](#Validator).  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="Fields"></a> Fields  
 Esse elemento agrupa os elementos individuais [Field](#Field) dentro de um elemento [Page](#Page).  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 92 fornece informações sobre o elemento [Fields](#Fields).  

### <a name="table-92-fields-element-information"></a>Tabela 92. Informações sobre o elemento Fields  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou mais dentro de cada elemento [Page](#Page) (Esse elemento é opcional.)|  
|Elementos pai|**Página**|  
|Conteúdo|**Field**, **RadioGroup**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Esse elemento não tem atributos.  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="File"></a> File  
 Esse elemento especifica a origem e o destino de uma operação de cópia de arquivo usando o tipo de tarefa **Microsoft.Wizard.CopyFilesTask**. É possível incluir um elemento [File](#File) separado para copiar mais de um arquivo em uma única tarefa.  

##### <a name="element-information"></a>Informações do elemento  
 A Tabela 93 fornece informações sobre o elemento [File](#File).  

### <a name="table-93-file-element-information"></a>Tabela 93. Informações sobre o elemento File  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Uma ou mais para cada tarefa que tem um tipo de tarefa de **Microsoft.Wizard.CopyFilesTask**|  
|Elementos pai|**Tarefa**|  
|Conteúdo|Nenhum|  

##### <a name="element-attributes"></a>Atributos de elemento  
 A Tabela 94 lista os atributos do elemento [File](#File) e fornece uma descrição de cada um.  

### <a name="table-94-attributes-and-corresponding-values-for-the-file-element"></a>Tabela 94. Atributos e valores correspondentes do elemento File  

|**Atributo**|**Descrição**|  
|-|-|  
|**Dest**|Especifica o caminho totalmente qualificado ou relativo para a pasta de destino para o arquivo especificado no atributo **Source**. As variáveis de ambiente são permitidas como uma parte do caminho.|  
|**Origem**|Especifica o caminho totalmente qualificado ou relativo para o arquivo de origem copiado pelo tipo de tarefa **Microsoft.Wizard.CopyFilesTask**. Esse atributo é compatível com caracteres curinga para que vários arquivos possam ser copiados usando um único elemento [File](#File). As variáveis de ambiente são permitidas como parte do caminho.|  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="PageElement"></a> Page  
 Esse elemento especifica uma instância de uma página e inclui todas as configurações da página.  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 95 fornece informações sobre o elemento [Page](#Page).  

### <a name="table-95-page-element-information"></a>Tabela 95. informações sobre o elemento Page  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Uma ou mais dentro de cada elemento [Pages](#Pages)|  
|Elementos pai|**Pages**|  
|Conteúdo|**Data**, **Fields**, **Setter**, **Tasks**|  

##### <a name="element-attributes"></a>Atributos de elemento  
A Tabela 96 lista os atributos do elemento [Page](#Page) e fornece uma descrição de cada um.  

### <a name="table-96-attributes-and-corresponding-values-for-the-page-element"></a>Tabela 96. Atributos e valores correspondentes do elemento Page  

|**Atributo**|**Descrição**|  
|-|-|  
|**DisplayName**|Especifica o nome amigável da página de assistente exibido no Designer do Assistente UDI. Esse nome é geralmente mais descritivo do que o atributo **Nome**.|  
|**Nome**|Especifica o nome da página de assistente exibido no Designer do Assistente de UDI.|  
|**Tipo**|Especifica o tipo de página de assistente que se relaciona diretamente a uma página de assistente específica dentro de uma DLL.|  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="PageRef"></a> PageRef  
 Esse elemento especifica uma referência a uma instância de uma página dentro de um [Stage](#Stage) dentro de um [StageGroup](#StageGroup).  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 97 fornece informações sobre o elemento [PageRef](#PageRef).  

### <a name="table-97-pageref-element-information"></a>Tabela 97. Informações sobre o elemento PageRef  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Uma ou mais dentro de um elemento [Stage](#Stage)|  
|Elementos pai|**Stage**|  
|Conteúdo|Nenhum|  

##### <a name="element-attributes"></a>Atributos de elemento  
A Tabela 98 lista o atributo do elemento [PageRef](#PageRef) e fornece uma descrição dele.  

### <a name="table-98-attributes-and-corresponding-values-for-the-pageref-element"></a>Tabela 98. Atributos e valores correspondentes do elemento PageRef  

|**Atributo**|**Descrição**|  
|-|-|  
|**Página**|Especifica a instância de uma página dentro de um [Stage](#Stage) dentro de um [StageGroup](#StageGroup). Defina esse valor como o atributo Name de um elemento [Page](#Page).|  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="Pages"></a> Pages  
 Esse elemento agrupa os elementos individuais [Page](#Page).  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 99 fornece informações sobre o elemento [Pages](#Pages).  

### <a name="table-99-pages-element-information"></a>Tabela 99. Informações sobre o elemento Pages  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Um|  
|Elementos pai|**Wizard**|  
|Conteúdo|**Página**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Esse elemento não tem atributos.  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  

```  
<Pages>  
   + <Page Name="WelcomePage" DisplayName="Welcome" Type="Microsoft.SharedPages.WelcomePage">  
   + <Page Name="ConfigScanPage" DisplayName="Deployment Readiness" Type="Microsoft.OSDRefresh.ConfigScanPage">  
   + <Page Name="ConfigScanBareMetal" DisplayName="Deployment Readiness" Type="Microsoft.OSDRefresh.ConfigScanPage">  
   + <Page Name="RebootPage" DisplayName="Reboot" Type="Microsoft.OSDRefresh.RebootPage">  
   + <Page Name="WelcomePageReplace" DisplayName="Welcome" Type="Microsoft.SharedPages.WelcomePage">  
   + <Page Name="VolumePage" DisplayName="Volume" Type="Microsoft.OSDRefresh.VolumePage">  
   + <Page Name="UserRestorePage" DisplayName="Select Target" Type="Microsoft.OSDRefresh.UserStatePage">  
   + <Page Name="ComputerPage" DisplayName="New Computer Details" Type="Microsoft.OSDRefresh.ComputerPage">  
   + <Page Name="AdminAccounts" DisplayName="Administrator Password" Type="Microsoft.SharedPages.AdminAccountsPage">  
   + <Page Name="UDAPage" DisplayName="User Device Affinity" Type="Microsoft.OSDRefresh.UDAPage">  
   + <Page Name="LanguagePage" DisplayName="Language" Type="Microsoft.OSDRefresh.LanguagePage">  
   + <Page Name="ApplicationPage" DisplayName="Install Programs" Type="Microsoft.OSDRefresh.ApplicationPage">  
     <Page Name="SummaryPage" DisplayName="Summary" Type="Microsoft.Shared.SummaryPage" />   
   + <Page Name="UserCapturePageOldPC" DisplayName="Select Target" Type="Microsoft.OSDRefresh.UserStatePage">  
   + <Page Name="ProgressPage" DisplayName="Capture Data" Type="Microsoft.OSDRefresh.ProgressPage">  
   + <Page Name="RebootAfterCapture" DisplayName="Reboot" Type="Microsoft.OSDRefresh.RebootPage">  
</Pages>  
```  

####  <a name="RadioGroup"></a> RadioGroup  
 Esse elemento especifica um grupo de botões de opção com um elemento [Field](#Field).  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 100 fornece informações sobre o elemento [RadioGroup](#RadioGroup).  

### <a name="table-100-radiogroup-element-information"></a>Tabela 100. Informações sobre o elemento RadioGroup  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou mais dentro de um elemento [Fields](#Fields) (esse elemento é opcional).|  
|Elementos pai|**Fields**|  
|Conteúdo|**Padrão**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 A Tabela 101 lista os atributos do elemento [RadioGroup](#RadioGroup) e fornece uma descrição de cada um.  

### <a name="table-101-attributes-and-corresponding-values-for-the-radiogroup-element"></a>Tabela 101. Atributos e valores correspondentes do elemento RadioGroup  

|**Atributo**|**Descrição**|  
|-|-|  
|**Locked**|Especifica se o grupo de botões de opção está habilitado para entrada de usuário. O atributo pode ser definido como:<br /><br /> -   **True**. Especifica que os botões de opção estão desabilitados, e os usuários não podem selecionar um botão de opção no grupo.<br />-   **False**. Especifica que os botões de opção estão habilitados, e os usuários podem selecionar um botão de opção no grupo.|  
|**Nome**|Especifica o nome do grupo de opção.|  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="StageGroup"></a> StageGroup  
 Esse elemento especifica um grupo de estágio de implantação.  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 102 fornece informações sobre o elemento [StageGroup](#StageGroup).  

### <a name="table-102-stagegroup-element-information"></a>Tabela 102. Informações sobre o elemento StageGroup  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Uma ou mais dentro de um elemento [StageGroups](#StageGroups)|  
|Elementos pai|**StageGroups**|  
|Conteúdo|**Stage**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 A Tabela 103 lista os atributos do elemento [StageGroup](#StageGroup) e uma descrição do atributo.  

### <a name="table-103-attributes-and-corresponding-values-for-the-stagegroup-element"></a>Tabela 103. Atributos e valores correspondentes do elemento StageGroup  

|**Atributo**|**Descrição**|  
|-|-|  
|**DisplayName**|Especifica o nome amigável do grupo de estágio exibido no Designer do Assistente de UDI. Esse nome é geralmente mais descritivo do que o atributo **Nome**.|  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="StageGroups"></a> StageGroups  
 Esse elemento agrupa um conjunto de grupos de estágio dentro de um arquivo de configuração do Assistente de UDI.  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 104 fornece informações sobre o elemento [StageGroups](#StageGroups).  

### <a name="table-104-stagegroups-element-information"></a>Tabela 104. Informações sobre o elemento StageGroups  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou uma dentro de um elemento [Wizard](#Wizard)|  
|Elementos pai|**Wizard**|  
|Conteúdo|**StageGroup**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Esse elemento não tem atributos.  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="Setter"></a> Setter  
 Esse elemento especifica uma configuração de propriedade para o valor de uma propriedade nomeado na propriedade **Property**.  

##### <a name="element-information"></a>Informações do elemento  
 A Tabela 105 fornece informações sobre o elemento [Setter]().  

### <a name="table-105-setter-element-information"></a>Tabela 105. Informações sobre o elemento Setter  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou mais dentro de cada elemento pai (esse elemento é opcional).|  
|Elementos pai|**Data**, **DataItem**, **Page**, **Style**, **Task**, **Validator**|  
|Conteúdo|Contém um valor de cadeia de caracteres no atributo **Property**|  

##### <a name="element-attributes"></a>Atributos de elemento  
A Tabela 106 lista o atributo do elemento [Setter]() e fornece uma descrição dele.  

### <a name="table-106-attributes-and-corresponding-values-for-the-setter-element"></a>Tabela 106. Atributos e valores correspondentes do elemento Setter  

|**Atributo**|**Descrição**|  
|-|-|  
|**Propriedade**|Especifica o nome da propriedade que está sendo definido. O nome da propriedade é definido como o valor que esse atributo delimita por colchetes.|  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

#### <a name="stage"></a>Estágio  
 Esse elemento especifica um [Stage](#Stage) dentro de um [StageGroup](#StageGroup) e contém um ou mais elementos [PageRef](#PageRef).  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 107 fornece informações sobre o elemento [Stage](#Stage).  

### <a name="table-107-stage-element-information"></a>Tabela 107. Informações sobre o elemento Stage  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Uma ou mais dentro de um elemento [StageGroup](#StageGroup)|  
|Elementos pai|**StageGroup**|  
|Conteúdo|**PageRef**|  

##### <a name="element-attributes"></a>Atributos de elemento  
A Tabela 108 lista os atributos do elemento [Stage](#Stage) e fornece uma descrição de cada um.  

### <a name="table-108-attributes-and-corresponding-values-for-the-stage-element"></a>Tabela 108. Atributos e valores correspondentes do elemento Stage  

|**Atributo**|**Descrição**|  
|-|-|  
|**DisplayName**|Especifica o nome amigável da página de assistente exibido no Designer do Assistente UDI. Esse nome é geralmente mais descritivo do que o atributo **Nome**.|  
|**Nome**|Especifica o nome do estágio. O valor desse elemento é usado ao iniciar o Assistente de UDI com o parâmetro de linha de comando **/stage: name**.|  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="Style"></a> Style  
 Esse elemento agrupa os elementos individuais [Setter]() que configuram a aparência do Assistente de UDI, incluindo o título mostrado na parte superior do assistente e a imagem da faixa mostrada no Assistente de UDI.  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 109 fornece informações sobre o elemento Style.  

### <a name="table-109-style-element-information"></a>Tabela 109. Informações sobre o elemento Style  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Um|  
|Elementos pai|**Wizard**|  
|Conteúdo|**Setter**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Esse elemento não tem atributos.  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  

```  
<Style>  
  <Setter Property="bannerFilename">UDI_Wizard_Banner.bmp</Setter>   
  <Setter Property="title">Operating System Deployment (OSD) Refresh Wizard</Setter>   
</Style>  
```  

####  <a name="TaskElement"></a> Task  
 Esse elemento especifica uma tarefa que deve ser executada na página especificada no elemento pai [Page](#Page).  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 110 fornece informações sobre o elemento [Task](#Task).  

### <a name="table-110-task-element-information"></a>Tabela 110. informações sobre o elemento Task  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Uma ou mais dentro de um elemento [Tasks](#Tasks)|  
|Elementos pai|**Tarefas**|  
|Conteúdo|**ExitCodes**, **File**, **Setter**|  

##### <a name="element-attributes"></a>Atributos de elemento  
A Tabela 111 lista os atributos do elemento [Task](#Task) e fornece uma descrição de cada um.  

### <a name="table-111-attributes-and-corresponding-values-for-the-task-element"></a>Tabela 111. Atributos e valores correspondentes do elemento Task  

|**Atributo**|**Descrição**|  
|-|-|  
|**DependsOn**|Especifica se a tarefa é dependente de outra tarefa. O valor desse atributo é definido como o atributo **Name** de outro elemento [Task](#Task). **Observação:** esse atributo não pode ser configurado usando o Designer do Assistente de UDI. No entanto, é possível adicionar manualmente esse atributo a um elemento [Task](#Task) modificando diretamente o arquivo .xml.|  
|**DisplayName**|Especifica o nome amigável da tarefa exibido no Designer do Assistente de UDI. Esse nome é geralmente mais descritivo do que o atributo **Nome**.|  
|**Nome**|Especifica o nome da tarefa. Esse nome deve ser exclusivo.|  
|Digite|Especifica o tipo de tarefa da tarefa a ser executada, definido na DLL que contém a tarefa.|  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="Tasks"></a> Tasks  
 Esse elemento agrupa um conjunto de tarefas para um elemento [Page](#Page).  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 112 fornece informações sobre o elemento [Tasks](#Tasks).  

### <a name="table-112-tasks-element-information"></a>Tabela 112. Informações sobre o elemento Tasks  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou uma dentro de cada elemento [Page](#Page) (esse elemento é opcional).|  
|Elementos pai|**Página**|  
|Conteúdo|**Tarefa**|  

##### <a name="element-attributes"></a>Atributos de elemento  
A Tabela 113 lista os atributos do elemento [Tasks](#Tasks) e fornece uma descrição de cada um.  

### <a name="table-113-attributes-and-corresponding-values-for-the-tasks-element"></a>Tabela 113. Atributos e valores correspondentes do elemento Tasks  

|**Atributo**|**Descrição**|  
|-|-|  
|**NameTitle**|Especifica a legenda exibida na parte superior da coluna que contém o nome das tarefas na página de assistente adequada.|  
|**StatusTitle**|Especifica a legenda exibida na parte superior da coluna que contém o status das tarefas na página de assistente adequada.|  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="ValidatorElement"></a> Validator  
 Esse elemento especifica um validador para o controle de campo especificado no elemento pai [Field](#Field).  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 114 fornece informações sobre o elemento [Validator](#Validator).  

### <a name="table-114-validator-element-information"></a>Tabela 114. informações sobre o elemento Validator  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou uma dentro de um elemento [Field](#Field)|  
|Elementos pai|**Field**|  
|Conteúdo|**Setter**|  

##### <a name="element-attributes"></a>Atributos de elemento  
A Tabela 115 lista o atributo do elemento [Validator](#Validator) e fornece uma descrição dele.  

### <a name="table-115-attributes-and-corresponding-values-for-the-validator-element"></a>Tabela 115. Atributos e valores correspondentes do elemento Validator  

|**Atributo**|**Descrição**|  
|-|-|  
|Digite|Especifica o tipo do validador, definido na DLL que contém o contém|  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  
 nenhuma.  

####  <a name="Wizard"></a> Wizard  
 Este elemento especifica a raiz de todos os outros elementos.  

##### <a name="element-information"></a>Informações do elemento  
A Tabela 116 fornece informações sobre o elemento [Wizard](#Wizard).  

### <a name="table-116-wizard-element-information"></a>Tabela 116. Informações sobre o elemento Wizard  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Um|  
|Elementos pai|Nenhum|  
|Conteúdo|**DLLs**, **Pages**, **StageGroups**, **Style**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Esse elemento não tem atributos.  

##### <a name="remarks"></a>Comentários  
 nenhuma.  

##### <a name="example"></a>Exemplo  

```  
<Wizard>  
   + <DLLs>  
   + <Style>  
   + <Pages>  
   + <StageGroups>  
</Wizard>  
```
