---
title: Exemplos do MDT
titleSuffix: Microsoft Deployment Toolkit
description: 'Exemplos do Microsoft Deployment Toolkit. '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 2ff0100c-b7ef-4e09-8c96-fc1898390b6d
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 6b36da9f98749858829ab591571496532b26f290
ms.sourcegitcommit: 7198ec49d9ce68c6d55bfb9e2d537b5442a132cb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2018
ms.locfileid: "33915965"
---
# <a name="microsoft-deployment-toolkit-samples-guide"></a>Guia de exemplos do Microsoft Deployment Toolkit  
 Este guia faz parte do MDT (Microsoft® Deployment Toolkit) 2013 e orienta uma equipe de especialistas sobre a implantação de sistemas operacionais Windows e Microsoft Office. Especificamente, este guia foi projetado para fornecer parâmetros de configuração de exemplo para cenários de implantação específicos.  

> [!NOTE]
>  Neste documento, *Windows* aplica-se aos sistemas operacionais Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2, salvo indicação em contrário. O MDT não é compatível com versões do Windows baseadas no processador ARM. Da mesma forma, *MDT* se refere ao MDT 2013, salvo indicação em contrário.  

 **Para usar este guia**  

 Leia a lista de tópicos de cenário no Sumário.  

1.  Selecione o cenário que melhor representa as metas de implantação da sua organização.  

2.  Leia os parâmetros de configuração de exemplo para o cenário selecionado.  

3.  Use os parâmetros de configuração de exemplo como base para os do seu ambiente.  

4.  Personalize os parâmetros de configuração de exemplo para o seu ambiente.  

 Em muitos casos, mais de um cenário pode ser necessário para preencher os parâmetros de configuração para o ambiente.  

 Como este guia contém apenas definições de configuração de exemplo, ler os guias listados na tabela a seguir pode auxiliar ainda mais a personalizar as definições de configuração do ambiente.  

 |Guia|Este guia oferece assistência para ajudar a|  
 |-|-|  
 |*Guia de Início Rápido do Microsoft System Center 2012 R2 Configuration Manager* |Use o System Center 2012 R2 Configuration Manager para instalar o sistema operacional Windows 8.1 em um cenário de implantação de novo computador.|  
 |*Guia de Início Rápido para Instalação Lite Touch* |Instale o sistema operacional Windows 8.1 por meio de LTI (Instalação Lite Touch) usando a mídia inicializável em um cenário de implantação de novo computador.|  
 |*Guia de Início Rápido para a Instalação Controlada pelo Usuário* |Use o sistema operacional Windows 8.1 com a Instalação Controlada pelo Usuário e o System Center 2012 R2 Configuration Manager em um cenário de implantação de novo computador.|  
 |*Como usar o Microsoft Deployment Toolkit* |Personalize ainda mais os arquivos de configuração usados em implantações ZTI (Instalação Zero Touch) e LTI. Este guia também fornece diretrizes para configuração genérica e uma referência técnica para os parâmetros de configuração.|


## <a name="deploying-windows-8-applications-using-mdt"></a>Implantando aplicativos do Windows 8 usando MDT  
 O MDT pode implantar pacotes de aplicativos do Windows 8, que têm uma extensão de arquivo .appx. Esses pacotes de aplicativos são novidade no Windows 8. Para obter mais informações sobre esses aplicativos, consulte [Desenvolvimento de aplicativo da Windows Store.](http://msdn.microsoft.com/windows/apps)  

 Implante aplicativos do Windows 8 usando o MDT executando as seguintes etapas:  

-   Implante aplicativos do Windows 8 usando LTI conforme descrito em [Implantando aplicativos do Windows 8 usando LTI](#DeployWin8LTI).  

-   Implante aplicativos do Windows 8 usando UDI (Instalação Controlada pelo Usuário), conforme descrito em [Implantando aplicativos do Windows 8 usando UDI](#DeployWin8UDI).  

###  <a name="DeployWin8LTI"></a> Implantando aplicativos do Windows 8 usando LTI  
 É possível implantar aplicativos do Windows 8 usando LTI como qualquer outro aplicativo que inicia o processo de instalação de uma linha de comando. É possível adicionar aplicativos do Windows 8 para implantações LTI no nó Aplicativos do Deployment Workbench.  

 **Para implantar um aplicativo do Windows 8 usando LTI**  

1.  Crie uma pasta de rede compartilhada na qual armazenar o aplicativo.  

2.  Copie o aplicativo do Windows 8 para a pasta de rede compartilhada que você criou na etapa anterior.  

     Copie o arquivo .appx do aplicativo do Windows 8 e demais arquivos necessários, tal como um arquivo .cer que contém o certificado do aplicativo.  

3.  Crie um item de aplicativo LTI para o aplicativo do Windows 8 no nó Aplicativos do Deployment Workbench usando o Assistente do Novo Aplicativo.  

     Ao concluir o Assistente de Novo Aplicativo, na página do assistente **Detalhes do Comando**, na **Linha de comando**, digite **nome_do_arquivo_do_aplicativo** (em que *nome_do_arquivo_do_aplicativo* é o nome do aplicativo do Windows 8).  

     Para obter mais informações sobre como concluir o Assistente de Novo Aplicativo no Deployment Workbench, consulte as seções a seguir no documento do MDT, *Usando o Microsoft Deployment Toolkit*:  

    -   “Criar um novo aplicativo implantado do compartilhamento da implantação”  

    -   “Criar um novo aplicativo implantado de outra pasta de rede compartilhada”  

4.  Selecione o item de aplicativo LTI criado na etapa anterior em uma sequência de tarefas LTI.  

###  <a name="DeployWin8UDI"></a> Implantando aplicativos do Windows 8 usando UDI  
 É possível implantar aplicativos do Windows 8 usando UDI como qualquer outro aplicativo que inicia o processo de instalação de uma linha de comando. É possível adicionar aplicativos do Windows 8 a implantações UDI na página do assistente **ApplicationPage** no Designer do Assistente de UDI.  

> [!NOTE]
>  A implantação do Windows 8 e aplicativos do Windows 8 usando UDI requer o System Center 2012 R2 Configuration Manager.  

 **Para implantar um aplicativo do Windows 8 usando UDI**  

1.  Crie uma pasta de rede compartilhada na qual armazenar o aplicativo.  

     Esta pasta será a pasta de origem para o aplicativo do Configuration Manager que você criará posteriormente neste processo.  

2.  Copie o aplicativo do Windows 8 para a pasta de rede compartilhada que você criou na etapa anterior.  

     Copie o arquivo .appx do aplicativo do Windows 8 e demais arquivos necessários, tal como um arquivo .cer que contém o certificado do aplicativo.  

3.  Adicionar o aplicativo do Windows 8 como um aplicativo do Configuration Manager  

4.  Crie um item de aplicativo do Configuration Manager para o aplicativo do Windows 8 usando o Assistente para Criar Aplicativos no console do Configuration Manager.  

     Ao concluir o Assistente para Criar Aplicativos, crie um tipo de implantação para implantar o aplicativo do Windows 8 usando o Assistente para Criar Tipo de Implantação. No Assistente para Criar Tipo de Implantação, na página **Conteúdo**, em **Programa de instalação**, digite **nome_do_arquivo_do_aplicativo** (em que *nome_do_arquivo_do_aplicativo* é o nome do aplicativo do Windows 8).  

     Para obter mais informações sobre como concluir o Assistente para Criar Aplicativos no console do Configuration Manager, consulte as seções a seguir na Biblioteca de Documentação do System Center 2012 Configuration Manager, que vem incluída com o Configuration Manager:  

    -   [Como criar aplicativos no Configuration Manager](http://technet.microsoft.com/library/gg682159.aspx)  

    -   [Como criar tipos de implantação no Configuration Manager](http://technet.microsoft.com/library/gg682174.aspx#BKMK_Step3)  

    -   [Como gerenciar aplicativos e tipos de implantação no Configuration Manager](http://technet.microsoft.com/library/gg682031)  

5.  Verifique se o recurso UDA (afinidade de dispositivo de usuário) no Configuration Manager está configurado corretamente para dar suporte à afinidade entre usuários e dispositivos para implantação de aplicativo do Configuration Manager.  

     Para obter mais informações sobre como configurar o UDA para dar suporte à implantação de aplicativo do Configuration Manager, consulte [Como gerenciar afinidade de dispositivo de usuário no Configuration Manager](http://technet.microsoft.com/library/gg699365).  

6.  Implante o aplicativo criado na etapa 4 para os usuários de destino.  

     Para obter mais informações sobre como implantar um aplicativo, consulte [Como implantar aplicativos no Configuration Manager](http://technet.microsoft.com/library/gg682082).  

7.  Configure a página do assistente **ApplicationPage** para incluir o aplicativo do Configuration Manager criado na etapa 4 usando o Designer do Assistente de UDI.  

     Para obter mais informações sobre como configurar a página do assistente **ApplicationPage** usando o Designer do Assistente de UDI, consulte a seção "Etapa 5 a 11: personalizar o arquivo de configuração do Assistente de UDI para o computador de destino", no documento do MDT *Guia de início rápido para instalação controlada pelo usuário*.  

8.  Selecione o item de aplicativo UDI criado na etapa anterior em uma sequência de tarefas UDI.  

    > [!NOTE]
    >  O aplicativo do Windows 8 não é instalado pela sequência de tarefas, mas sim na primeira vez que o usuário faz logon no computador de destino (conforme definido pela configuração de UDA definida na etapa 5) usando o recurso de Instalador de Aplicativos Centrado no Usuário (AppInstall.exe) no UDI.  

     Para obter mais informações sobre o recurso do instalador de aplicativos centrado no usuário no UDI, consulte a seção “Referência do instalador de aplicativos centrado no usuário” no documento MDT *Referência do Toolkit*.  

## <a name="managing-mdt-using-windows-powershell"></a>Gerenciando o MDT usando o Windows PowerShell  
 É possível gerenciar compartilhamentos de implantação do MDT usando o Deployment Workbench e o Windows PowerShell. O MDT inclui um snap-in do Windows PowerShell™ —Microsoft.BDD.SnapIn— que precisa ser carregado antes de usar os recursos específicos do MDT no Windows PowerShell. O snap-in do MDT Windows PowerShell inclui:  

-   Um provedor do Windows PowerShell – MDTProvider – que fornece acesso ao conteúdo de um compartilhamento de implantação  

-   Cmdlets que fornecem a capacidade de administrar compartilhamentos de implantação do MDT  

 Gerencie compartilhamentos de implantação do MDT com o Windows PowerShell executando as seguintes etapas:  

-   Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [Carregando o snap-in do MDT Windows PowerShell](#LoadMDTSnapIn).  

-   Crie um compartilhamento de implantação usando o Windows PowerShell, conforme descrito em [Criando um compartilhamento de implantação usando o Windows PowerShell](#CreateDeployShare).  

-   Exiba as propriedades de compartilhamentos de implantação usando o Windows PowerShell, conforme descrito em [Exibindo as propriedades do compartilhamento de implantação usando o Windows PowerShell](#ViewDeployShareProp).  

-   Exiba a lista de compartilhamentos de implantação usando o Windows PowerShell, conforme descrito em [Exibindo a lista de compartilhamentos de implantação usando o Windows PowerShell](#ViewListDeployShare).  

-   Atualize um compartilhamento de implantação, que gera novas imagens de inicialização do Windows PE (Ambiente de Pré-Instalação do Windows), conforme descrito em [Atualizando uma implantação de compartilhamento usando o Windows PowerShell](#UpdateDeployShare).  

-   Atualize um compartilhamento de implantação vinculado, que replica o conteúdo de um compartilhamento de implantação para o compartilhamento de implantação vinculado, conforme descrito em [Atualizando um compartilhamento de implantação vinculado usando o Windows PowerShell](#UpdateLinkedDeployShare).  

-   Atualize a mídia de implantação, que replica o conteúdo de um compartilhamento de implantação para a mídia de implantação e, em seguida, gera novas imagens inicializáveis, conforme descrito em [Atualizando a mídia de implantação usando o Windows PowerShell](#UpdateDeployMedia).  

-   Gerencie itens em um compartilhamento de implantação (como sistemas operacionais, pacotes do sistema operacional, aplicativos e drivers de dispositivo), conforme descrito em [Gerenciando itens em um compartilhamento de implantação usando o Windows PowerShell](#ManageItemDeployShare).  

-   Automatize a população de itens em um compartilhamento de implantação (como sistemas operacionais, pacotes do sistema operacional, aplicativos e drivers de dispositivo), conforme descrito em [Automatizando a população de um compartilhamento de implantação](#AutomatePopulateDeployShare).  

-   Gerencie as pastas em um compartilhamento de implantação usando o Windows PowerShell, conforme descrito em [Gerenciando pastas do compartilhamento de implantação usando o Windows PowerShell](#ManageDeployShareFolder).  

###  <a name="LoadMDTSnapIn"></a> Carregando o snap-in do MDT Windows PowerShell  
 Os cmdlets do MDT são fornecidos em um snap-in do Windows PowerShell **Microsoft.BDD.SnapIn** que precisa ser carregado antes de usar os cmdlets do MDT. Carregue o snap-in do MDT Windows PowerShell usando um dos seguintes métodos:  

-   Carregue o snap-in do MDT Windows PowerShell usando o console dos Módulos do Windows PowerShell, conforme descrito em [Carregar o snap-in do MDT Windows PowerShell usando a tarefa Importar Módulos do Sistema](#LoadMDTSnapInImport).  

-   Carregue o snap-in do MDT Windows PowerShell usando o cmdlet **Add-PSSnapIn**, conforme descrito em [Carregar o snap-in do MDT Windows PowerShell usando o cmdlet Add-PSSnapIn](#LoadMDTSnapInCmdlet).  

####  <a name="LoadMDTSnapInImport"></a> Carregar o snap-in do MDT Windows PowerShell usando a tarefa Importar Módulos do Sistema  
 A tarefa Importar Módulos do Sistema inclui automaticamente todos os módulos e snap-ins do Windows PowerShell existentes nos módulos no diretório %Windir%\System32\WindowsPowerShell\1.0\Modules. O MDT automaticamente instala o snap-in do MDT Windows PowerShell **Microsoft.BDD.SnapIn** nessa pasta durante o processo de instalação do MDT.  

> [!NOTE]
>  A tarefa Importar Módulos do Sistema está disponível somente no Windows 7 e no Windows Server 2008 R2 quando o Windows PowerShell 3.0 não está instalado no computador. A partir do Windows PowerShell 3.0, os módulos são importados automaticamente na primeira vez que você usar um cmdlet no módulo.  

 Inicie um console do Windows PowerShell com a tarefa Importar Módulos do Sistema executando um dos procedimentos a seguir:  

-   Na barra de tarefas, clique com o botão direito do mouse no ícone **Windows PowerShell** e, em seguida, clique em **Importar Módulos do Sistema**.  

-   Clique em **Iniciar**, aponte para **Ferramentas Administrativas** e clique em **Módulos do Windows PowerShell**.  

 Para obter mais informações sobre como iniciar um console do Windows PowerShell com Importar Módulos do Sistema, consulte [Iniciando o Windows PowerShell com Importar Módulos do Sistema](http://msdn.microsoft.com/library/windows/desktop/hh847866.aspx).  

####  <a name="LoadMDTSnapInCmdlet"></a> Carregar o snap-in do MDT Windows PowerShell usando o cmdlet Add-PSSnapIn  
 É possível carregar o snap-in do MDT Windows PowerShell **Microsoft.BDD.PSSnapIn** de qualquer ambiente do Windows PowerShell usando o cmdlet [Add-PSSnapIn](http://technet.microsoft.com/library/hh849705.aspx), como mostrado no exemplo a seguir:  

```  
Add-PSSnapin -Name Microsoft.BDD.PSSnapIn  
```  

###  <a name="CreateDeployShare"></a> Criando um compartilhamento de implantação usando o Windows PowerShell  
 É possível criar compartilhamentos de implantação usando os cmdlets do MDT Windows PowerShell. A pasta raiz para o compartilhamento de implantação é criada e compartilhada usando os cmdlets padrão do Windows PowerShell e chamadas para comandos de classe WMI (Instrumentação de Gerenciamento do Windows). O compartilhamento de implantação é populado usando o provedor MDTProvider Windows PowerShell e o cmdlet [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx). A unidade do MDTProvider Windows PowerShell é mantida usando o cmdlet **Add-MDTPersistentDrive**.  

 **Para preparar um compartilhamento de implantação usando os cmdlets do MDT Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [Carregando o snap-in do MDT Windows PowerShell](#LoadMDTSnapIn).  

2.  Crie uma pasta que será a raiz do novo compartilhamento de implantação usando o cmdlet **New-Item**, como mostrado no exemplo a seguir e descrito em [Usando o cmdlet New-Item](http://technet.microsoft.com/library/ee176914.aspx):  

    ```  
    New-Item "C:\MDTDeploymentShare$" -Type directory  
    ```  

     O cmdlet exibe a criação bem-sucedida da pasta.  

3.  Compartilhe a pasta criada na etapa anterior usando a classe **WMI win32_share** como mostrado no exemplo a seguir:  

    ```  
    ([wmiclass]"win32_share").Create("C:\MDTDeploymentShare$", "MDTDeploymentShare$",0)  
    ```  

     A chamada para a classe **win32_share** retorna os resultados da chamada. Se o valor de **ReturnValue** é zero (0), a chamada foi bem-sucedida.  

4.  Especifique a nova pasta compartilhada como um compartilhamento de implantação usando o cmdlet [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx), como mostrado no exemplo a seguir:  

    ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "C:\MDTDeploymentShare$" -Description "MDT Deployment Share Created with Cmdlets" -NetworkPath "\\WDG-MDT-01\MDTDeploymentShare$" -Verbose  
    ```  

     O cmdlet automaticamente começa a criar o compartilhamento de implantação e a copiar as informações do modelo para o novo compartilhamento de implantação. Após a conclusão do processo de cópia, o cmdlet exibe as informações do novo compartilhamento de implantação.  

    > [!NOTE]
    >  O valor fornecido no parâmetro *Name* (DS002) precisa ser exclusivo e não pode ser o mesmo que um compartilhamento de implantação existente da unidade do Windows PowerShell.  

5.  Verifique se as pastas de compartilhamento de implantação apropriadas foram criadas usando o comando **dir**, como mostrado no exemplo a seguir:  

    ```  
    dir ds002:  
    ```  

     A lista de pastas padrão na raiz do compartilhamento de implantação é exibida.  

6.  Adicione o novo compartilhamento de implantação à lista de compartilhamentos de implantação MDT persistentes usando o cmdlet **Add-MDTPersistentDrive**, como mostrado no exemplo a seguir:  

    ```  
    $NewDS=Get-PSDrive "DS002"  
    Add-MDTPersistentDrive  -Name "DS002" -InputObject $NewDS Verbose  
    ```  

     Neste exemplo, a variável *$NewDS* é usada para passar o objeto de unidade do Windows PowerShell do novo compartilhamento de implantação para o cmdlet.  

     Outra opção seria combinar os cmdlets [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx) e **Add-MDTPersistentDrive adicionar**, conforme mostrado no exemplo a seguir:  

    ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "C:\MDTDeploymentShare$" -Description "MDT Deployment Share Created with Cmdlets" -NetworkPath "\\WDG-MDT-01\MDTDeploymentShare$" -Verbose | Add-MDTPersistentDrive -Verbose  
    ```  

     No exemplo anterior, o pipeline do Windows PowerShell fornece os parâmetros *Name* e *InputObject*.  

###  <a name="ViewDeployShareProp"></a> Exibindo as propriedades do compartilhamento de implantação usando o Windows PowerShell  
 Exiba as propriedades de compartilhamentos de implantação do MDT usando o cmdlet [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) e o provedor MDTProvider Windows PowerShell. Essas mesmas propriedades também podem ser vistas no Deployment Workbench.  

 **Para exibir as propriedades do compartilhamento de implantação usando cmdlets do MDT Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [Carregando o snap-in do MDT Windows PowerShell](#LoadMDTSnapIn).  

2.  Verifique se as implantações do MDT que compartilham unidades do Windows PowerShell foram restauradas usando o cmdlet **Restore-MDTPersistentDrive**, como mostrado no exemplo a seguir:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implantações do MDT que compartilham unidades do Windows PowerShell já tiverem sido restauradas, você receberá uma mensagem de aviso indicando que o cmdlet não pode restaurar a unidade.  

3.  Verifique se as implantações do MDT que compartilham unidades do Windows PowerShell foram restauradas corretamente usando o cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), da seguinte maneira:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista de unidades do Windows PowerShell fornecidas usando o MDTProvider é mostrada.  

4.  Exiba as propriedades do compartilhamento de implantação usando o cmdlet [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx), como mostrado no exemplo a seguir:  

    ```  
    Get-ItemProperty "DS002:"  
    ```  

     Neste exemplo, *DS002:* é o nome de uma unidade do Windows PowerShell retornada na etapa 3. O cmdlet retorna as propriedades para o compartilhamento de implantação.  

###  <a name="ViewListDeployShare"></a> Exibindo a lista de compartilhamentos de implantação usando o Windows PowerShell  
 Exiba a lista de compartilhamentos de implantação do MDT usando o cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) e o provedor MDTProvider Windows PowerShell. A mesma lista de compartilhamentos de implantação também pode ser exibida no Deployment Workbench.  

 **Para exibir uma lista de compartilhamentos de implantação usando os cmdlets do MDT Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [Carregando o snap-in do MDT Windows PowerShell](#LoadMDTSnapIn).  

2.  Verifique se as implantações do MDT que compartilham unidades do Windows PowerShell foram restauradas usando o cmdlet **Restore-MDTPersistentDrive**, como mostrado no exemplo a seguir:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implantações do MDT que compartilham unidades do Windows PowerShell já tiverem sido restauradas, você receberá uma mensagem de aviso indicando que o cmdlet não pode restaurar a unidade.  

3.  Exiba a lista de implantações do MDT que compartilham unidades do Windows PowerShell, uma para cada compartilhamento de implantação, usando o cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), da seguinte maneira:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista de unidades do Windows PowerShell fornecidas usando o MDTProvider é mostrada, uma para cada compartilhamento de implantação.  

###  <a name="UpdateDeployShare"></a> Atualizando um compartilhamento de implantação usando o Windows PowerShell  
 Atualize os compartilhamentos de implantação usando o cmdlet **Update-MDTDeploymentShare** e o provedor MDTProvider Windows PowerShell. Atualizar um compartilhamento de implantação cria imagens de inicialização do Windows PE (arquivos WIM e ISO [Organização Internacional de Normalização]) necessária para iniciar a implantação LTI. É possível efetuar o mesmo processo usando o Deployment Workbench, conforme descrito em “Atualizar um compartilhamento de implantação no Deployment Workbench”.  

 **Para atualizar um compartilhamento de implantação usando o Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [Carregando o snap-in do MDT Windows PowerShell](#LoadMDTSnapIn).  

2.  Verifique se as implantações do MDT que compartilham unidades do Windows PowerShell foram restauradas usando o cmdlet **Restore-MDTPersistentDrive**, como mostrado no exemplo a seguir:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implantações do MDT que compartilham unidades do Windows PowerShell já tiverem sido restauradas, você receberá uma mensagem de aviso indicando que o cmdlet não pode restaurar a unidade.  

3.  Verifique se as implantações do MDT que compartilham unidades do Windows PowerShell foram restauradas corretamente usando o cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), da seguinte maneira:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista de unidades do Windows PowerShell fornecidas usando o MDTProvider é mostrada.  

4.  Atualize o compartilhamento de implantação usando o cmdlet **Update-MDTDeploymentShare**, conforme mostrado no exemplo a seguir:  

    ```  
    Update-MDTDeploymentShare -Path "DS002:" -Force  
    ```  

     Neste exemplo, *DS002:* é o nome de uma unidade do Windows PowerShell retornada na etapa 3.  

    > [!NOTE]
    >  A atualização do compartilhamento de implantação pode levar muito tempo. O progresso do cmdlet é mostrado na parte superior do console do Windows PowerShell.  

     O cmdlet retornará sem saída se a atualização for bem-sucedida.  

###  <a name="UpdateLinkedDeployShare"></a> Atualizando um compartilhamento de implantação vinculado usando o Windows PowerShell  
 Atualize (replique) os compartilhamentos de implantação vinculados usando o cmdlet **Update-MDTLinkedDS** e o provedor MDTProvider Windows PowerShell. A atualização de um compartilhamento de implantação vinculado replica o conteúdo do compartilhamento de implantação original para o vinculado. É possível efetuar o mesmo processo usando o Deployment Workbench, conforme descrito em “Replicar compartilhamentos de implantação vinculados no Deployment Workbench”.  

 **Para atualizar um compartilhamento de implantação vinculado usando o Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [Carregando o snap-in do MDT Windows PowerShell](#LoadMDTSnapIn).  

2.  Verifique se as implantações do MDT que compartilham unidades do Windows PowerShell foram restauradas usando o cmdlet **Restore-MDTPersistentDrive**, como mostrado no exemplo a seguir:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implantações do MDT que compartilham unidades do Windows PowerShell já tiverem sido restauradas, você receberá uma mensagem de aviso indicando que o cmdlet não pode restaurar a unidade.  

3.  Verifique se as implantações do MDT que compartilham unidades do Windows PowerShell foram restauradas corretamente usando o cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), da seguinte maneira:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista de unidades do Windows PowerShell fornecidas usando o MDTProvider é mostrada.  

4.  Atualize o compartilhamento de implantação usando o cmdlet **Update-MDTDeploymentShare**, conforme mostrado no exemplo a seguir:  

    ```  
    Update-MDTLinkedDS -Path "DS002:\Linked Deployment Shares\LINKED002"  
    ```  

     Neste exemplo, *DS002:* é o nome de uma unidade do Windows PowerShell retornada na etapa 3.  

    > [!NOTE]
    >  A atualização do compartilhamento de implantação vinculado pode levar muito tempo. O progresso do cmdlet é mostrado na parte superior do console do Windows PowerShell.  

     O cmdlet retornará sem saída se a atualização for bem-sucedida.  

###  <a name="UpdateDeployMedia"></a> Atualizando a mídia de implantação usando o Windows PowerShell  
 Atualize (gere) a mídia de implantação usando o cmdlet **Update-MDTMedia** e o provedor MDTProvider Windows PowerShell. A atualização da mídia de implantação replica o conteúdo do compartilhamento de implantação original para o vinculado e, em seguida, gera os arquivos .iso e .wim. É possível efetuar o mesmo processo usando o Deployment Workbench, conforme descrito em “Gerar imagens de mídia no Deployment Workbench”.  

 Quando o cmdlet **Update-MDTMedia** termina, os seguintes arquivos são criados:  

-   Um arquivo .iso na pasta *pasta_de_mídia* (em que *pasta_de_mídia* é o nome da pasta que você especificou para a mídia)  

     Gerar o arquivo .iso é uma opção configurada da seguinte forma:  

    -   Marcando a caixa de seleção **Gerar uma imagem ISO inicializável Lite Touch** na guia **Geral** da caixa de diálogo **Propriedades de mídia** (desmarque essa caixa de seleção para reduzir o tempo necessário para gerar a mídia, a menos que seja necessário criar DVDs inicializáveis ou iniciar as máquinas virtuais [VMs] do arquivo .ISO.)  

    -   Definindo a mesma propriedade usando o cmdlet [Set-ItemProperty](http://technet.microsoft.com/library/hh849844)  

-   Arquivos WIM na pasta *pasta_de_mídia*\Content\Deploy\Boot (em que *pasta_de_mídia* é o nome da pasta que você especificou para a mídia)  

 **Para atualizar um compartilhamento de implantação vinculado usando o Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [Carregando o snap-in do MDT Windows PowerShell](#LoadMDTSnapIn).  

2.  Verifique se as implantações do MDT que compartilham unidades do Windows PowerShell foram restauradas usando o cmdlet **Restore-MDTPersistentDrive**, como mostrado no exemplo a seguir:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implantações do MDT que compartilham unidades do Windows PowerShell já tiverem sido restauradas, você receberá uma mensagem de aviso indicando que o cmdlet não pode restaurar a unidade.  

3.  Verifique se as implantações do MDT que compartilham unidades do Windows PowerShell foram restauradas corretamente usando o cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), da seguinte maneira:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista de unidades do Windows PowerShell fornecidas usando o MDTProvider é mostrada.  

4.  Atualize o compartilhamento de implantação usando o cmdlet **Update-MDTDeploymentShare**, conforme mostrado no exemplo a seguir:  

    ```  
    Update-MDTLinkedDS -Path "DS002:\Linked Deployment Shares\LINKED002"  
    ```  

     Neste exemplo, *DS002:* é o nome de uma unidade do Windows PowerShell retornada na etapa 3.  

    > [!NOTE]
    >  A atualização do compartilhamento de implantação vinculado pode levar muito tempo. O progresso do cmdlet é mostrado na parte superior do console do Windows PowerShell.  

     O cmdlet retornará sem saída se a atualização for bem-sucedida.  

###  <a name="ManageItemDeployShare"></a> Gerenciado itens em um compartilhamento de implantação usando o Windows PowerShell  
 Um compartilhamento de implantação contém itens que são usados para realizar implantações, como sistemas operacionais, aplicativos, drivers de dispositivo, pacotes do sistema operacional e sequências de tarefas. Esses itens podem ser gerenciados usando cmdlets do Windows PowerShell e aqueles fornecidos com o MDT.  

 Para obter mais informações sobre como manipular itens diretamente usando cmdlets do Windows PowerShell, consulte [Manipulando itens diretamente](http://technet.microsoft.com/library/dd315266.aspx). A estrutura de pastas de um compartilhamento de implantação também pode ser gerenciada usando o Windows PowerShell. Para obter mais informações, consulte [Gerenciando as pastas de compartilhamento de implantação usando o Windows PowerShell](#ManageDeployShareFolder).  

####  <a name="ImportItemDeployShare"></a> Importar um item em um compartilhamento de implantação  
 É possível importar todos os tipos de item, como sistemas operacionais, aplicativos ou drivers de dispositivo, usando os cmdlets do MDT. Para cada tipo de item, há um cmdlet específico do MDT. Se desejar importar vários itens para um compartilhamento de implantação usando o Windows PowerShell, consulte [Automatizando o rastreamento de um compartilhamento de implantação](#AutomatePopulateDeployShare).  

 A tabela a seguir lista os cmdlets do MDT Windows PowerShell usados para importar itens para um compartilhamento de implantação e fornece uma breve descrição de cada cmdlet. Exemplos de como usar cada cmdlet são fornecidos na seção que corresponde a cada cmdlet.  

 |**Cmdlet** | **Descrição** |  
 |-|-|  
 |**Import-MDTApplication** |Importa um aplicativo para um compartilhamento de implantação|  
 |**Import-MDTDriver** |Importa um ou mais drivers de dispositivo para um compartilhamento de implantação|  
 |**Import-MDTOperatingSystem** |Importa um ou mais sistemas operacionais para um compartilhamento de implantação|  
 |**Import-MDTPackage** |Importa um ou mais pacotes de sistema operacional para um compartilhamento de implantação|  
 |**Import-MDTTaskSequence** |Importa uma sequência de tarefas para um compartilhamento de implantação|  

####  <a name="ViewPropertyDeployShare"></a> Exibir as propriedades de um item em um compartilhamento de implantação  
 Cada item em um compartilhamento de implantação tem um conjunto diferente de propriedades. Exiba as propriedades de um item em um compartilhamento de implantação usando o cmdlet [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx). O cmdlet [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) usa o MDTProvider para exibir as propriedades para um item específico, da mesma forma que é possível ver as propriedades no Deployment Workbench.  

 Se você desejar exibir as propriedades de vários itens em um compartilhamento de implantação usando o Windows PowerShell, consulte [Automatizando o rastreamento de um compartilhamento de implantação](#AutomatePopulateDeployShare).  

 **Para exibir as propriedades de um item em um compartilhamento de implantação usando o Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [Carregando o snap-in do MDT Windows PowerShell](#LoadMDTSnapIn).  

2.  Verifique se as implantações do MDT que compartilham unidades do Windows PowerShell foram restauradas usando o cmdlet **Restore-MDTPersistentDrive**, como mostrado no exemplo a seguir:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implantações do MDT que compartilham unidades do Windows PowerShell já tiverem sido restauradas, você receberá uma mensagem de aviso indicando que o cmdlet não pode restaurar a unidade.  

3.  Verifique se as implantações do MDT que compartilham unidades do Windows PowerShell foram restauradas corretamente usando o cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), conforme mostrado no exemplo a seguir:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista de unidades do Windows PowerShell fornecidas usando o MDTProvider é mostrada.  

4.  Retornar uma lista de itens do tipo de item para o qual você deseja exibir as propriedades usando o cmdlet [Get-Item](http://technet.microsoft.com/library/hh849788), conforme mostrado no exemplo a seguir:  

    ```  
    Get-Item "DS001:\Operating Systems\*" | Format-List  
    ```  

     No exemplo anterior, é exibida uma lista de todos os sistemas operacionais no compartilhamento de implantação. A saída é redirecionada para o cmdlet **Format-List** para que os nomes longos dos sistemas operacionais possam ser vistos. Para obter mais informações sobre como usar o cmdlet **Format-List**, consulte [Usando o cmdlet Format-List](http://technet.microsoft.com/library/ee176830.aspx). O mesmo processo poderia ser usado para retornar a lista de outros tipos de itens, como drivers de dispositivo ou aplicativos.  

    > [!TIP]
    >  Também seria possível usar o comando **dir** para exibir a lista de sistemas operacionais em vez do cmdlet [Get-Item](http://technet.microsoft.com/library/hh849788).  

5.  Exiba as propriedades de um dos itens listados na etapa anterior usando o cmdlet [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx), como mostrado no exemplo a seguir:  

    ```  
    Get-ItemProperty -Path "DS002:\Operating Systems\Windows 8 in Windows 8 x64 install.wim"  
    ```  

     Neste exemplo, o valor do parâmetro *Path* é o caminho totalmente qualificado do Windows PowerShell para o item, incluindo o nome do arquivo que foi retornado na etapa anterior. Seria possível usar o mesmo processo para exibir as propriedades de outros tipos de itens, tal como drivers de dispositivo ou aplicativos.  

####  <a name="RemoveItemDeployShare"></a> Remover um item de um compartilhamento de implantação  
 Você pode remover um item de um compartilhamento de implantação usando o cmdlet [Remove-Item](http://technet.microsoft.com/library/hh849765). O cmdlet [Remove-Item](http://technet.microsoft.com/library/hh849765) usa o MDTProvider para remover um item específico, da mesma forma que um item é removido do Deployment Workbench. Se desejar remover vários itens de um compartilhamento de implantação usando o Windows PowerShell, consulte [Automatizando o rastreamento de um compartilhamento de implantação](#AutomatePopulateDeployShare).  

> [!NOTE]
>  Removendo um item utilizado por uma sequência de tarefas faz com que ela falhe. Verifique se um item não é referenciado por outros itens no compartilhamento de implantação antes de removê-lo. Depois que um item é removido, não é possível recuperá-lo.  

 **Para remover um item de um compartilhamento de implantação usando o Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [Carregando o snap-in do MDT Windows PowerShell](#LoadMDTSnapIn).  

2.  Verifique se as implantações do MDT que compartilham unidades do Windows PowerShell foram restauradas usando o cmdlet **Restore-MDTPersistentDrive**, como mostrado no exemplo a seguir.  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implantações do MDT que compartilham unidades do Windows PowerShell já tiverem sido restauradas, você receberá uma mensagem de aviso indicando que o cmdlet não pode restaurar a unidade.  

3.  Verifique se as implantações do MDT que compartilham unidades do Windows PowerShell foram restauradas corretamente usando o cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), conforme mostrado no exemplo a seguir:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista de unidades do Windows PowerShell fornecidas usando o MDTProvider é mostrada.  

4.  Retornar uma lista de itens do tipo de item para o qual você deseja exibir as propriedades usando o cmdlet [Get-Item](http://technet.microsoft.com/library/hh849788), conforme mostrado no exemplo a seguir:  

    ```  
    Get-Item "DS001:\Operating Systems\*" | Format-List  
    ```  

     No exemplo anterior, é exibida uma lista de todos os sistemas operacionais no compartilhamento de implantação. A saída é redirecionada para o cmdlet **Format-List** para que os nomes longos dos sistemas operacionais possam ser vistos. Para obter mais informações sobre como usar o cmdlet **Format-List**, consulte [Usando o cmdlet Format-List](http://technet.microsoft.com/library/ee176830.aspx). É possível usar o mesmo processo para retornar a lista de outros tipos de itens, como drivers de dispositivo ou aplicativos.  

    > [!TIP]
    >  Também seria possível usar o comando **dir** para exibir a lista de sistemas operacionais em vez do cmdlet [Get-Item](http://technet.microsoft.com/library/hh849788).  

5.  Remova um dos itens listados na etapa anterior usando o cmdlet [Remove-Item](http://technet.microsoft.com/library/hh849765), como mostrado no exemplo a seguir:  

    ```  
    Remove-Item -Path "DS002:\Operating Systems\Windows 8 in Windows 8 x64 install.wim"  
    ```  

     Neste exemplo, o valor do parâmetro *Path* é o caminho totalmente qualificado do Windows PowerShell para o item, incluindo o nome do arquivo que foi retornado na etapa anterior.  

     É possível usar o mesmo processo para remover outros tipos de itens, como drivers de dispositivo ou aplicativos.  

    > [!NOTE]
    >  Removendo um item utilizado por uma sequência de tarefas faz com que ela falhe. Verifique se um item não é referenciado por outros itens no compartilhamento de implantação antes de removê-lo.  

###  <a name="AutomatePopulateDeployShare"></a> Automatizando o rastreamento de um compartilhamento de implantação  
 Os cmdlets do MDT Windows PowerShell permitem gerenciar itens individuais. No entanto, usando os recursos de script do Windows PowerShell, é possível usar os cmdlets para automatizar o rastreamento de um compartilhamento de implantação.  

 Por exemplo, uma organização pode precisar implantar vários compartilhamentos de implantação para diferentes unidades de negócios ou fornecer serviços de implantação de sistema operacional para outras organizações. Em ambos os exemplos, as organizações precisam poder criar e popular os compartilhamentos de implantação que são configurados de forma consistente.  

 Um método para gerenciar vários itens seria usar um arquivo CSV (de valores separados por vírgula) contendo uma lista de todos os itens que você deseja gerenciar em um compartilhamento de implantação usando o cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx).  

 Veja a seguir um trecho de um script do Windows PowerShell para importar uma lista de aplicativos com base nas informações em um arquivo .csv usando os cmdlets [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx), [ForEach-Object](http://technet.microsoft.com/library/hh849731) e **Import-MDTApplication**:  

```  
$List=Import-CSV "C:\MDT\Import-MDT-Apps.csv"  
ForEach-Object ($App in $List) {  
Import-MDTApplication –path $App.ApplicationFolder -enable "True" –Name $App.DescriptiveName –ShortName $App.Shortname –Version $App.Version –Publisher $App.Publisher –Language $App.Language –CommandLine $App.CommandLine –WorkingDirectory $App.WorkingDirectory –ApplicationSourcePath $App.SourceFolder –DestinationFolder $App.DestinationFolder –Verbose  
}  
```  

 Neste exemplo, o arquivo C:\MDT\Import-MDT-Apps.csv contém um campo para cada variável necessária para importar um aplicativo. Para obter mais informações sobre como criar um arquivo .csv para ser usado com o cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx), consulte [Usando o cmdlet Import-Csv](http://technet.microsoft.com/library/ee176874.aspx).  

 Você pode usar esse mesmo método para importar sistemas operacionais, drivers de dispositivo e outros itens em um compartilhamento de implantação executando as seguintes etapas:  

1.  Crie um arquivo .csv para cada tipo de item de compartilhamento de implantação que você deseja popular.  

2.  Para obter mais informações sobre como criar um arquivo .csv para ser usado com o cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx), consulte [Usando o cmdlet Import-Csv](http://technet.microsoft.com/library/ee176874.aspx).  

3.  Crie um arquivo de script do Windows PowerShell que será usado para automatizar a população do compartilhamento de implantação.  

     Para obter mais informações sobre como criar um script do Windows PowerShell, consulte [Scripts com o Windows PowerShell](http://technet.microsoft.com/scriptcenter/powershell.aspx).  

4.  Crie a estrutura de pasta de pré-requisito necessária no compartilhamento de implantação antes de importar os itens de compartilhamento de implantação.  

     Para obter mais informações, consulte [Gerenciando as pastas de compartilhamento de implantação usando o Windows PowerShell](#ManageDeployShareFolder).  

5.  Adicione a linha de cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) a um dos arquivos .csv criados na etapa 1.  

     Para obter mais informações sobre o cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx), consulte [Usando o cmdlet Import-Csv](http://technet.microsoft.com/library/ee176874.aspx).  

6.  Crie um loop do cmdlet [ForEach-Object](http://technet.microsoft.com/library/hh849731) que processa cada item do arquivo .csv referenciado no cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) na etapa anterior.  

     Para obter mais informações sobre o cmdlet [ForEach-Object](http://technet.microsoft.com/library/hh849731), consulte [Usando o cmdlet ForEach-Object](http://technet.microsoft.com/library/ee176828).  

7.  Adicione o cmdlet MDT correspondente para importar os itens de compartilhamento de implantação dentro do loop do cmdlet [ForEach-Object](http://technet.microsoft.com/library/hh849731) criado na etapa anterior.  

     Para obter mais informações sobre os cmdlets do MDT usados para importar itens para um compartilhamento de implantação, consulte [Importar um item para um compartilhamento de implantação](#ImportItemDeployShare).  

###  <a name="ManageDeployShareFolder"></a> Gerenciando as pastas de compartilhamento de implantação usando o Windows PowerShell  
 É possível gerenciar pastas em um compartilhamento de implantação usando ferramentas de linha de comando, como o comando **mkdir**, ou usando cmdlets do Windows PowerShell, como o cmdlet [New-Item](http://technet.microsoft.com/library/hh849795) e o provedor MDTProvider Windows PowerShell. A mesma estrutura de pastas de compartilhamentos de implantação também pode ser vista e gerenciada no Deployment Workbench. Para obter mais informações sobre como manipular itens diretamente usando cmdlets do Windows PowerShell, consulte [Manipulando itens diretamente](http://technet.microsoft.com/library/dd315266.aspx).  

#### <a name="create-a-folder-in-a-deployment-share-using-windows-powershell"></a>Criar uma pasta em um compartilhamento de implantação usando o Windows PowerShell  
 **Para criar uma pasta em um compartilhamento de implantação usando o Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [Carregando o snap-in do MDT Windows PowerShell](#LoadMDTSnapIn).  

2.  Verifique se as implantações do MDT que compartilham unidades do Windows PowerShell foram restauradas usando o cmdlet **Restore-MDTPersistentDrive**, como mostrado no exemplo a seguir:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implantações do MDT que compartilham unidades do Windows PowerShell já tiverem sido restauradas, você receberá uma mensagem de aviso indicando que o cmdlet não pode restaurar a unidade.  

3.  Exiba a lista de implantações do MDT que compartilham unidades do Windows PowerShell, uma para cada compartilhamento de implantação, usando o cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), da seguinte maneira:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista de unidades do Windows PowerShell fornecidas usando o MDTProvider é mostrada, uma para cada compartilhamento de implantação  

4.  Crie uma pasta chamada *Windows_8* na pasta Operating Systems em um compartilhamento de implantação usando o comando **mkdir**, como mostrado no exemplo a seguir:  

    ```  
    mkdir "DS002:\Operating Systems\Windows_8"  
    ```  

     Neste exemplo, *DS002:* é o nome de uma unidade do Windows PowerShell retornada na etapa 3.  

5.  Verifique se a pasta foi criada corretamente digitando o seguinte comando:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     A pasta Windows_8 e demais pastas existentes na pasta Operating Systems são exibidas.  

6.  Crie uma pasta chamada *Windows_7* na pasta Operating Systems em um compartilhamento de implantação usando o cmdlet [New-Item](http://technet.microsoft.com/library/hh849795), como mostrado no exemplo a seguir e descrito em [Usando o cmdlet New-Item](http://technet.microsoft.com/library/ee176914.aspx):  

    ```  
    New-Item "DS002:\Operating Systems\Windows_7" -Type directory  
    ```  

     O cmdlet exibe a criação bem-sucedida da pasta.  

7.  Verifique se a pasta foi criada corretamente digitando o seguinte comando:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     A pasta Windows_7 e demais pastas existentes na pasta Operating Systems são exibidas.  

#### <a name="delete-a-folder-in-a-deployment-share-using-windows-powershell"></a>Excluir uma pasta em um compartilhamento de implantação usando o Windows PowerShell  
 **Para excluir uma pasta em um compartilhamento de implantação usando o Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [Carregando o snap-in do MDT Windows PowerShell](#LoadMDTSnapIn).  

2.  Verifique se as implantações do MDT que compartilham unidades do Windows PowerShell foram restauradas usando o cmdlet **Restore-MDTPersistentDrive**, como mostrado no exemplo a seguir:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implantações do MDT que compartilham unidades do Windows PowerShell já tiverem sido restauradas, você receberá uma mensagem de aviso indicando que o cmdlet não pode restaurar a unidade.  

3.  Exiba a lista de implantações do MDT que compartilham unidades do Windows PowerShell, uma para cada compartilhamento de implantação, usando o cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), da seguinte maneira:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista de unidades do Windows PowerShell fornecidas usando o MDTProvider é mostrada, uma para cada compartilhamento de implantação.  

4.  Exclua (remova) uma pasta chamada *Windows_8* na pasta Operating Systems em um compartilhamento de implantação usando o comando **mkdir**, como mostrado no exemplo a seguir:  

    ```  
    rmdir "DS002:\Operating Systems\Windows_8"  
    ```  

     Neste exemplo, *DS002:* é o nome de uma unidade do Windows PowerShell retornada na etapa 3.  

5.  Verifique se a pasta foi removida corretamente digitando o seguinte comando:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     A pasta Windows_8 não é mais exibida na lista de pastas da pasta Operating Systems  

6.  Exclua (remova) uma pasta chamada *Windows_7* na pasta Operating Systems em um compartilhamento de implantação usando o cmdlet [Remove-Item](http://technet.microsoft.com/library/hh849765), como mostrado no exemplo a seguir:  

    ```  
    Remove-Item "DS002:\Operating Systems\Windows_7"  
    ```  

     O cmdlet exibe a remoção bem-sucedida da pasta.  

7.  Verifique se a pasta foi criada corretamente digitando o seguinte comando:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     A pasta Windows_7 não é mais exibida na lista de pastas da pasta Operating Systems.  

#### <a name="rename-a-folder-in-a-deployment-share-using-windows-powershell"></a>Renomear uma pasta em um compartilhamento de implantação usando o Windows PowerShell  
 **Para renomear uma pasta em um compartilhamento de implantação usando o Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [Carregando o snap-in do MDT Windows PowerShell](#LoadMDTSnapIn).  

2.  Verifique se as implantações do MDT que compartilham unidades do Windows PowerShell foram restauradas usando o cmdlet **Restore-MDTPersistentDrive**, como mostrado no exemplo a seguir:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implantações do MDT que compartilham unidades do Windows PowerShell já tiverem sido restauradas, você receberá uma mensagem de aviso indicando que o cmdlet não pode restaurar a unidade.  

3.  Exiba a lista de implantações do MDT que compartilham unidades do Windows PowerShell, uma para cada compartilhamento de implantação, usando o cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) da seguinte maneira:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista de unidades do Windows PowerShell fornecidas usando o MDTProvider é mostrada, uma para cada compartilhamento de implantação.  

4.  Renomeie uma pasta chamada *Windows_8* para *Win_8* na pasta Operating Systems em um compartilhamento de implantação usando o comando **ren**, como mostrado no exemplo a seguir:  

    ```  
    ren "DS002:\Operating Systems\Windows_8" "Win_8"  
    ```  

     Neste exemplo, *DS002:* é o nome de uma unidade do Windows PowerShell retornada na etapa 3.  

5.  Verifique se a pasta foi removida corretamente digitando o seguinte comando:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     A pasta Windows_8 é renomeada para *Win_8*.  

6.  Renomeie uma pasta chamada *Windows_7* para *Win-7* na pasta Operating Systems em um compartilhamento de implantação usando o cmdlet [Rename-Item](http://technet.microsoft.com/library/hh849763), como mostrado no exemplo a seguir:  

    ```  
    Rename-Item "DS002:\Operating Systems\Windows_7" "Win_7"  
    ```  

     O cmdlet exibe a renomeação bem-sucedida da pasta.  

7.  Verifique se a pasta foi criada corretamente digitando o seguinte comando:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     A pasta Windows_7 é renomeada para *Win_7*.  

## <a name="automating-the-application-of-operating-system-service-packs-in-deployment-shares"></a>Automatizando a aplicação de service packs do sistema operacional em compartilhamentos de implantação  
 Service packs do sistema operacional são uma parte normal do ciclo de vida do software. Os sistemas operacionais existentes nos compartilhamentos de implantação precisam ser atualizados com esses service packs para ajudar a garantir que os computadores recém-implantados ou atualizados estejam em dia com as recomendações de segurança e parâmetros de configuração mais recentes.  

 Nos casos em que uma organização tem diversos compartilhamentos de implantação com vários sistemas operacionais em cada um deles, o processo para atualizar manualmente os sistemas operacionais em cada compartilhamento de implantação com os service packs pode ser demorado. Os métodos para automatizar a aplicação de service packs do sistema operacional em compartilhamentos de implantação incluem:  

-   Copiando o conteúdo de origem atualizado que já contém o service pack (por exemplo, mídia do Windows 7 com SP1) para a pasta no compartilhamento de implantação no qual reside o sistema operacional existente, conforme descrito em [Automatizando a aplicação de service packs do sistema operacional da mídia de origem atualizada](#AutomateAppFromUSM)  

-   Aplicando o service pack a um computador de referência e, em seguida, capturando uma imagem atualizada de um computador de referência, conforme descrito em [Automatizando a aplicação de service packs do sistema operacional usando um computador de referência e o Windows PowerShell](#AutomateAppUsingRef)  

###  <a name="AutomateAppFromUSM"></a> Automatizando a aplicação de service packs do sistema operacional em mídia de origem atualizada  
 É possível automatizar o processo de atualização de service packs do sistema operacional usando o Windows PowerShell quando há uma mídia de origem que inclui o service pack, tal como um DVD que tenha o Windows 7 com SP1 já integrado.  

 Para esse método, a mídia de origem do sistema operacional com o service pack é copiada sobre os arquivos de sistema operacional existentes sem o service pack no compartilhamento de implantação usando o Windows PowerShell.  

 **Para automatizar a aplicação de service packs do sistema operacional da mídia de origem de atualizações usando o Windows PowerShell**  

1.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [Carregando o snap-in do MDT Windows PowerShell](#LoadMDTSnapIn).  

2.  Verifique se as implantações do MDT que compartilham unidades do Windows PowerShell foram restauradas usando o cmdlet **Restore-MDTPersistentDrive**, como mostrado no exemplo a seguir:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implantações do MDT que compartilham unidades do Windows PowerShell já tiverem sido restauradas, você receberá uma mensagem de aviso indicando que o cmdlet não pode restaurar a unidade.  

3.  Exiba a lista de implantações do MDT que compartilham unidades do Windows PowerShell, uma para cada compartilhamento de implantação, usando o cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), conforme mostrado no exemplo a seguir:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista de unidades do Windows PowerShell fornecidas usando o MDTProvider é mostrada, uma para cada compartilhamento de implantação.  

4.  Remova a pasta para o sistema operacional existente do compartilhamento de implantação usando os cmdlets [Get-ChildItem](http://technet.microsoft.com/library/hh849800) e [Remove-Item](http://technet.microsoft.com/library/hh849765), conforme mostrado no exemplo a seguir:  

    ```  
    Get-ChildItem “DS002:\Operating Systems\Windows 7” –recurse | Remove-Item –recurse –force  
    ```  

     Neste exemplo, *DS002:* é o nome de uma unidade do Windows PowerShell retornada na etapa 3.  

5.  Copie o conteúdo dos arquivos de origem de sistema operacional que tem o service pack integrado usando o cmdlet [Copy-Item](http://technet.microsoft.com/library/hh849793), como mostrado no exemplo a seguir:  

    ```  
    Copy-Item "E:\*" -Destination "DS002:\Operating Systems\Windows 7"-Recurse -Force  
    ```  

     Neste exemplo, os arquivos de origem do sistema operacional estão na unidade E, e *DS002:* é o nome de uma unidade do Windows PowerShell retornada na etapa 3.  

6.  Atualize as mídias de implantação do MDT baseadas no compartilhamento de implantação usando o cmdlet **Update-MDTMedia**.  

 Para obter mais informações sobre como atualizar a mídia de implantação do MDT baseada no compartilhamento de implantação usando o cmdlet **Update-MDTMedia**, consulte [Atualizando a mídia de implantação usando o Windows PowerShell](#UpdateDeployMedia).  

###  <a name="AutomateAppUsingRef"></a> Automatizando a aplicação de service packs do sistema operacional usando um computador de referência e o Windows PowerShell  
 É possível automatizar o processo de atualização de service packs do sistema operacional usando o Windows PowerShell quando você tem apenas o service pack que ainda não está integrado com o sistema operacional, como o SP1 para Windows 7 que ainda não foi integrado a uma imagem do Windows 7.  

 Para esse método, implante o sistema operacional sem o service pack em um computador de referência. Em seguida, aplique o service pack no computador de referência. Em seguida, capture uma imagem de sistema operacional de um computador de referência. Por fim, copie o arquivo .wim capturado sobre o arquivo Install.wim no sistema operacional no compartilhamento de implantação usando o Windows PowerShell.  

 **Para automatizar a aplicação de service packs do sistema operacional da mídia de origem de atualizações usando o Windows PowerShell**  

1.  Implante o sistema operacional de destino em um computador de referência.  

     Para obter mais informações sobre como implantar um computador de referência, consulte os seguintes recursos no documento do MDT, *Usando o Microsoft Deployment Toolkit*:  

    -   “Preparando a implantação LTI ao computador de referência”  

    -   “Implantando e capturando uma imagem do computador de referência no LTI”  

2.  Instale o service pack desejado no computador de referência.  

     Para obter mais informações sobre como instalar o service pack, consulte a documentação que o acompanha.  

3.  Capture uma imagem do computador de referência criando e implantando uma sequência de tarefas baseada no modelo de sequência de tarefas **Sysprep e captura**.  

     Para obter mais informações sobre como criar uma sequência de tarefas baseada no modelo de sequência de tarefas **Sysprep e captura**, consulte “Criar uma nova sequência de tarefas no Deployment Workbench”.  

4.  Carregue o snap-in do MDT Windows PowerShell, conforme descrito em [Carregando o snap-in do MDT Windows PowerShell](#LoadMDTSnapIn).  

5.  Verifique se as implantações do MDT que compartilham unidades do Windows PowerShell foram restauradas usando o cmdlet **Restore-MDTPersistentDrive**, como mostrado no exemplo a seguir:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se as implantações do MDT que compartilham unidades do Windows PowerShell já tiverem sido restauradas, você receberá uma mensagem de aviso indicando que o cmdlet não pode restaurar a unidade.  

6.  Exiba a lista de implantações do MDT que compartilham unidades do Windows PowerShell, uma para cada compartilhamento de implantação, usando o cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), conforme mostrado no exemplo a seguir:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     A lista de unidades do Windows PowerShell fornecidas usando o MDTProvider é mostrada, uma para cada compartilhamento de implantação.  

7.  Copie o arquivo .wim capturado na etapa 3 sobre o arquivo Install.wim no sistema operacional no compartilhamento de implantação usando o cmdlet [Copy-Item](http://technet.microsoft.com/library/hh849793), como mostrado no exemplo a seguir:  

    ```  
    Copy-Item "DS002:\Captures\Win7SP1.wim" -Destination "DS002:\Operating Systems\Windows 7\sources\Install.wim" Force  
    ```  

     Neste exemplo, o arquivo de imagem do sistema operacional capturado (Win7SP1.wim) na pasta Capture no compartilhamento DS002: é o nome de uma unidade do Windows PowerShell retornado na etapa 6, e o sistema operacional Windows 7 existente é armazenado na pasta denominada *Windows 7*.  

8.  Atualize as mídias de implantação do MDT baseadas no compartilhamento de implantação usando o cmdlet **Update-MDTMedia**.  

     Para obter mais informações sobre como atualizar a mídia de implantação do MDT baseada no compartilhamento de implantação usando o cmdlet **Update-MDTMedia**, consulte [Atualizando a mídia de implantação usando o Windows PowerShell](#UpdateDeployMedia).  

## <a name="customizing-deployment-based-on-chassis-type"></a>Personalizando a implantação com base no tipo de chassi  
 É possível personalizar a implantação com base no tipo de chassi do computador. Os scripts criam variáveis locais que podem ser processadas no arquivo CustomSettings.ini. As variáveis locais `IsLaptop`, `IsDesktop` e `IsServer` indicam se o computador é um computador portátil, um computador desktop ou um servidor, respectivamente.  

> [!NOTE]
>  Em versões anteriores do Deployment Workbench, o sinalizador `IsServer` indicava que o sistema operacional existente era um sistema operacional de servidor (como o Windows Server 2003 Enterprise Edition). Este sinalizador foi renomeado para `IsServerOS`.  

 **Para implementar as variáveis locais no arquivo CustomSettings.ini**  

1.  Na seção `[Settings]`, linha `Priority`, adicione uma seção personalizada para personalizar a implantação com base no tipo de chassi (`ByChassisType` no exemplo a seguir, em que *Chassis* representa o tipo de computador).  

2.  Crie a seção personalizada que corresponde àquela definida na etapa 1 (`ByChassisType` no exemplo a seguir, em que *Chassi* representa o tipo de computador).  

3.  Definir uma subseção para cada tipo de chassi a ser detectado (`Subsection=Laptop-%IsLaptop%, Subsection=Desktop-%IsDesktop%, Subsection=Server-%IsServer%` no exemplo a seguir).  

4.  Crie uma subseção para cada estado `True` e `False` de cada subseção definida na etapa 3 (como `[Laptop-True], [Laptop-False], [Desktop-True], [Desktop-False]` no exemplo a seguir).  

5.  Em cada subseção `True` e `False`, adicione as configurações apropriadas com base no tipo de chassi.  

 **Listagem 1. Exemplo de personalização da implantação baseada no tipo de chassi no arquivo CustomSettings.ini**  

```  
[Settings]  

Priority=...,ByLaptopType,ByDesktopType,ByServerType  

[ByLaptopType]  
Subsection=Laptop-%IsLaptop%  

[ByDesktopType]  
Subsection=Desktop-%IsDesktop%  

[ByServerType]  
Subsection=Server-%IsServer%  
.  
.  
.  

[Laptop-True]  
.  
.  
.  

[Laptop-False]  
.  
.  
.  

[Desktop-True]  
.  
.  
.  

[Desktop-False]  
.  
.  
.  

[Server-True]  
.  
.  
.  

[Server-False]  
.  
.  
.  
```  

## <a name="deploying-applications-based-on-earlier-application-versions"></a>Implantando aplicativos baseados em versões anteriores do aplicativo  
 Geralmente, ao instalar um sistema operacional em um computador existente, os mesmos aplicativos instalados anteriormente no computador são instalados novamente. Faça isso usando scripts do MDT (em especial, ZTIGather.wsf) para consultar duas fontes separadas de informações:  

-   **Recurso de inventário de software do Configuration Manager.** Contém um registro para cada pacote de aplicativo – nesse caso, as listagens em Programas e Recursos no Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2 – instalado na última vez que o Configuration Manager fez inventário do computador.  

-   **Uma tabela de mapeamento.** Descreve qual pacote e programa precisam ser instalados para cada Registro (porque os registros de Programa e Recursos ou Adicionar ou Remover Programas não especificam exatamente qual pacote instalou o aplicativo, tornando impossível selecionar automaticamente o pacote com base apenas no inventário).  

 **Para efetuar uma instalação dinâmica de aplicativos específicos do computador**  

1.  Use a tabela no MDT DB para se conectar a pacotes específicos com os aplicativos listados no sistema operacional de destino.  

2.  Preencha a tabela com os dados que associam o pacote apropriado ao aplicativo listado em “Programas e Recursos” ou “Adicionar ou Remover Programas”.

     **Consulta SQL para popular a tabela**  

    ```  
    use [MDTDB]  
    go  
    INSERT INTO [PackageMapping] (ARPName, Packages) VALUES('Office12.0', 'XXX0000F:Install Office 2010 Professional Plus')  
    go  
    ```  

     A linha inserida se conecta a qualquer computador que tenha a entrada `Office12.0` com o pacote do Microsoft Office 2010 Professional Plus.  

     Isso significa que o Microsoft Office 2010 Professional Plus será instalado em qualquer computador que executa o sistema Microsoft Office 2007 (Office 12.0) no momento. Adicione as entradas semelhantes aos demais pacotes. Qualquer item para o qual nenhuma entrada é ignorada (nenhum pacote será instalado).  

3.  Crie um procedimento armazenado para simplificar a junção das informações na nova tabela com os dados de inventário.  

    ```  
    use [MDTDB]  
    go  

    if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[RetrievePackages]') and OBJECTPROPERTY(id, N'IsProcedure') = 1)  
    drop procedure [dbo].[RetrievePackages]  
    go  

    CREATE PROCEDURE [dbo].[RetrievePackages]  
    @MacAddress CHAR(17)  
    AS  

    SET NOCOUNT ON  

    /* Select and return all the appropriate records based on current inventory */  
    SELECT * FROM PackageMapping  
    WHERE ARPName IN  
    (  
      SELECT ProdID0 FROM CM_DB.dbo.v_GS_ADD_REMOVE_PROGRAMS a, CM_DB.dbo.v_GS_NETWORK_ADAPTER n  
      WHERE a.ResourceID = n.ResourceID AND  
      MACAddress0 = @MacAddress  
    )  
    go  
    ```  

     O procedimento armazenado no exemplo anterior pressupõe que o banco de dados do site primário central do Configuration Manager reside no computador em que o SQL Server é executado como o MDT DB. Se o banco de dados do site primário central residirem em um computador diferente, será necessário realizar as modificações apropriadas no procedimento armazenado. Além disso, o nome do banco de dados (`CM_DB`) precisa ser atualizado. Considere também conceder acesso de Leitura de contas adicionais à exibição **v_GS_ADD_REMOVE_PROGRAMS** no banco de dados do Configuration Manager.  

4.  Configure o arquivo CustomSettings.ini para consultar esta tabela de banco de dados especificando o nome de uma seção (`[DynamicPackages]` na lista **Prioridade**) que aponta para as informações do banco de dados.  

    ```  
    [Settings]  
    …  
    Priority=MacAddress, DefaultGateway, DynamicPackages, Default  
    …  
    ```  

5.  Crie uma seção `[DynamicPackages]` para especificar o nome de uma seção de banco de dados.  

    ```  
    [DynamicPackages]  
    SQLDefault=DB_DynamicPackages  
    ```  

6.  Crie uma seção de banco de dados para especificar as informações do banco de dados e os detalhes da consulta.  

    ```  
    [DB_DynamicPackages]  
    SQLServer=SERVER1  
    Database=MDTDB  
    StoredProcedure=RetrievePackages  
    Parameters=MacAddress  
    SQLShare=Logs  
    Instance=SQLEnterprise2005  
    Port=1433  
    Netlib=DBNMPNTW  
    ```  

     No exemplo anterior, o MDT DB denominado *MDTDB* no computador que executa a instância do SQL Server denominada *SERVER1* será consultado. O banco de dados contém um procedimento armazenado chamado `RetrievePackages` (criado na etapa 3).  

 Quando ZTIGather.wsf é executado, uma instrução `SELECT` da linguagem SQL é gerada automaticamente e o valor da chave personalizada **MakeModelQuery** é passado como um parâmetro para a consulta:  

 ```  
 EXECUTE RetrievePackages ?  
 ```  

 O valor real da chave personalizada **MACAddress** será substituído pelo “?” correspondente.  Essa consulta retorna um conjunto de registros com as linhas inseridas na etapa 2.  

 Um número variável de argumentos não pode ser passado para um procedimento armazenado. Como resultado, quando um computador tem mais de um endereço MAC, nem todos os endereços MAC podem ser transmitidos para o procedimento armazenado. Como alternativa, substitua o procedimento armazenado por um modo de exibição que permite consultar a exibição com uma instrução `SELECT` com uma cláusula `IN` para transmitir todos os valores de endereço MAC.  

 Baseado no cenário apresentado aqui, se o computador atual tem o valor `Office12.0` inserido na tabela (etapa 2), a linha um é retornada (`XXX0000F:Install Office 2010 Professional Plus`). Isso indica que o pacote XXX0000F:Install Office 2001 Professional Plus será instalado pelo processo ZTI durante a Fase de Restauração de Estado.  

## <a name="fully-automated-lti-deployment-scenario"></a>Cenário de implantação LTI totalmente automatizada  
 A principal finalidade do LTI é automatizar o processo de implantação o máximo possível. Embora o ZTI forneça automação de implantação completa usando os scripts do MDT e dos Serviços de Implantação do Windows, o LTI foi projetado para funcionar com menos requisitos de infraestrutura.  

 É possível automatizar o Assistente de Implantação do Windows usado no processo de implantação LTI para reduzir (ou eliminar) as páginas do assistente exibidas. Você pode ignorar todo o Assistente de Implantação do Windows especificando a propriedade **SkipWizard** em CustomSettings.ini. Para ignorar páginas individuais do assistente, use as seguintes propriedades:  

-   **SkipAdminPassword**  

-   **SkipApplications**  

-   **SkipBDDWelcome**  

-   **SkipBitLocker**  

-   **SkipBitLockerDetails**  

-   **SkipTaskSequence**  

-   **SkipCapture**  

-   **SkipComputerBackup**  

-   **SkipComputerName**  

-   **SkipDomainMembership**  

-   **SkipFinalSummary**  

-   **SkipLocaleSelection**  

-   **SkipPackageDisplay**  

-   **SkipProductKey**  

-   **SkipSummary**  

-   **SkipTimeZone**  

-   **SkipUserData**  

Para obter mais informações sobre essas propriedades individuais, consulte a propriedade correspondente no documento do MDT *Referência do Toolkit*.  

Para cada página do assistente ignorada, forneça os valores para as propriedades correspondentes que normalmente são coletadas por meio da página do assistente nos arquivos CustomSettings.ini e BootStrap.ini. Para obter mais informações sobre as propriedades que precisam ser configuradas nesses arquivos, consulte a seção “Fornecendo propriedades para páginas ignoradas do assistente de implantação” no documento do MDT *Referência do Toolkit*.  

## <a name="fully-automated-lti-deployment-for-a-refresh-computer-scenario"></a>Cenário de implantação LTI totalmente automatizada para atualização de computador  
 Veja a seguir como um arquivo CustomSettings.ini é usado para um cenário de Atualização de Computador para ignorar todas as páginas do Assistente de Implantação do Windows. Neste exemplo, as propriedades que serão fornecidas ao ignorar a página do assistente estão imediatamente sob a propriedade que ignora a página do assistente.  

```  
[Settings]  
Priority=Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac /lae  
SkipCapture=YES  
SkipAdminPassword=YES  
SkipProductKey=YES  

DeploymentType=REFRESH  

SkipDomainMembership=YES  
JoinDomain=DomainName  
DomainAdmin=Administrator  
DomainAdminDomain=DomainName  
DomainAdminPassword=a_secure_password  

SkipUserData=yes  
UserDataLocation=AUTO  
UDShare=\\Servername\Sharename\Directory  
UDDir=%ComputerName%  

SkipComputerBackup=YES  
ComputerBackuplocation=AUTO  
BackupShare=\\Servername\Backupsharename  
BackupDir=%ComputerName%  

SkipTaskSequence=YES  
TaskSequenceID=Enterprise  

SkipComputerName=YES  
OSDComputerName=%ComputerName%  

SkipPackageDisplay=YES  
LanguagePacks001={3af4e3ce-8122-41a2-9cf9-892145521660}  
LanguagePacks002={84fc70d4-db4b-40dc-a660-d546a50bf226}  

SkipLocaleSelection=YES  
UILanguage=en-US  
UserLocale=en-CA  
KeyboardLocale=0409:00000409  

SkipTimeZone=YES  
TimeZoneName=China Standard Time  

SkipApplications=YES  
Applications001={a26c6358-8db9-4615-90ff-d4511dc2feff}  
Applications002={7e9d10a0-42ef-4a0a-9ee2-90eb2f4e4b98}  
UserID=Administrator  
UserDomain=DomainName  
UserPassword=P@ssw0rd  

SkipBitLocker=YES  
SkipSummary=YES  
Powerusers001=DomainName\Username  
```  

## <a name="fully-automated-lti-deployment-for-a-new-computer-scenario"></a>Cenário de implantação LTI totalmente automatizada para um novo computador  
 Veja a seguir um exemplo de um arquivo CustomSettings.ini usado para um cenário de Novo Computador para ignorar todas as páginas do Assistente de Implantação do Windows. Neste exemplo, as propriedades que serão fornecidas ao ignorar a página do assistente estão imediatamente sob a propriedade que ignora a página do assistente.  

```  
[Settings]  
Priority=Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac /lae  

SkipCapture=YES  
ComputerBackupLocation=\\WDG-MDT-01\Backup$\  
BackupFile=MyCustomImage.wim  

SkipAdminPassword=YES  
SkipProductKey=YES  

SkipDomainMembership=YES  
JoinDomain=WOODGROVEBANK  
DomainAdmin=Administrator  
DomainAdminDomain=WOODGROVEBANK  
DomainAdminPassword=P@ssw0rd  

SkipUserData=Yes  
UserDataLocation=\\WDG-MDT-01\UserData$\Directory\usmtdata  

SkipTaskSequence=YES  
TaskSequenceID=Enterprise  

SkipComputerName=YES  
OSDComputerName=%SerialNumber%  

SkipPackageDisplay=YES  
LanguagePacks001={3af4e3ce-8122-41a2-9cf9-892145521660}  
LanguagePacks002={84fc70d4-db4b-40dc-a660-d546a50bf226}  

SkipLocaleSelection=YES  
UILanguage=en-US  
UserLocale=en-CA  
KeyboardLocale=0409:00000409  

SkipTimeZone=YES  
TimeZoneName=China Standard Time  

SkipApplications=YES  
Applications001={a26c6358-8db9-4615-90ff-d4511dc2feff}  
Applications002={7e9d10a0-42ef-4a0a-9ee2-90eb2f4e4b98}  

SkipBitLocker=YES  
SkipSummary=YES  
Powerusers001=WOODGROVEBANK\PilarA  
CaptureGroups=YES  
SLShare=\\WDG-MDT-01\UserData$\Logs  
Home_page=http://www.microsoft.com/NewComputer  
```  

## <a name="calling-web-services-in-mdt"></a>Chamando serviços Web no MDT  
 Nas versões anteriores do MDT, o processamento de regras recebia suporte por meio do CustomSettings.ini e dos bancos de dados, dos quais era possível recuperar valores do computador local, normalmente usando WMI, para tomar decisões sobre o que precisa ser feito em cada computador durante a implantação. Além disso, é possível fazer consultas SQL e chamadas de procedimento armazenado para recuperar informações adicionais de bancos de dados externos. Contudo, essa abordagem trazia certos desafios, especialmente na criação de conexões SQL seguras.  

 Para ajudar a resolver esse problema, o MDT oferece a capacidade de fazer chamadas de serviço Web com base em regras simples definidas em CustomSettings.ini. Essas solicitações de serviço Web não requerem nenhum contexto de segurança especial e podem usar qualquer porta TCP/IP necessária para simplificar as configurações de firewall.  

 Veja a seguir como configurar o CustomSettings.ini para chamar um serviço Web específico. Nesse cenário, o serviço Web é escolhido aleatoriamente de uma pesquisa na Internet. Ele usa um CEP como entrada e retorna a cidade, o estado, o código de área e o fuso horário (como uma letra) para o CEP especificado.  

```  
[Settings]  
Priority=Default, USZipService  
Properties=USZip, City, State, Zip, Area_Code, Time_Zones   
[Default]  
USZip=98052   
[USZipService]  
WebService=http://www.webservicex.net/uszip.asmx/GetInfoByZIP  
Parameters=USZip  
```  

 A execução deste código produz uma saída semelhante à seguinte:
```  
Added new custom property USZIP  
Added new custom property CITY  
Added new custom property STATE  
Added new custom property ZIP  
Added new custom property AREA_CODE  
Added new custom property TIME_ZONES  
Using from [Settings]: Rule Priority = DEFAULT, USZIPSERVICE  
------ Processing the [DEFAULT] section ------  
Property USZIP is now = 98052  
Using from [DEFAULT]: USZIP = 98052  
------ Processing the [USZIPSERVICE] section ------  
Using COMMAND LINE ARG: Ini file = CustomSettings.ini  
CHECKING the [USZIPSERVICE] section  
About to execute web service call to http://www.webservicex.net/uszip.asmx/GetInfoByZIP: USZip=98052  
Response from web service: 200 OK  
Successfully executed the web service.  
Property CITY is now = Redmond  
Obtained CITY value from web service:  CITY = Redmond  
Property STATE is now = WA  
Obtained STATE value from web service:  STATE = WA  
Property ZIP is now = 98052  
Obtained ZIP value from web service:  ZIP = 98052  
Property AREA_CODE is now = 425  
Obtained AREA_CODE value from web service:  AREA_CODE = 425  
------ Done processing CustomSettings.ini ------  
```  

 Há certas complicações menores que podem surgir ao executar um serviço Web:  

-   Não faça nada especial com os servidores proxy. Se houver um proxy anônimo, use-o, mas observe que autenticar proxies pode causar problemas. Na maioria dos casos, um serviço Web não será chamado.  

-   CustomSettings.ini ou ZTIGather.xml pesquisa propriedades definidas na marcação XML retornada como resultado da chamada de serviço Web (assim como ocorre com uma consulta de banco de dados ou outra regra). No entanto, a pesquisa XML diferencia maiúsculas de minúsculas. Felizmente, o serviço Web descrito aqui retorna todos os nomes de propriedade com letras maiúsculas, que é o esperado pelo ZTIGather.xml. É possível remapear as entradas minúsculas ou que contém maiúsculas e minúsculas para contornar esse problema.  

-   É recomendado usar uma solicitação `POST` para o serviço Web, por isso a chamada de serviço Web precisa ser capaz de dar suporte a um `POST`.  

## <a name="connecting-to-network-resources"></a>Conectando-se aos recursos da rede  
 Durante os processos de implantação de LTI e ZTI, pode ser necessário ter acesso a um recurso de rede em um servidor diferente daquele que hospeda o compartilhamento de implantação. É necessário estar autenticado no outro servidor para poder acessar as pastas ou serviços compartilhados dele. Por exemplo, você pode instalar um aplicativo de uma pasta compartilhada em um servidor diferente do servidor que hospeda o compartilhamento de implantação usado pelos scripts do MDT.  

> [!NOTE]
>  Para consultar bancos de dados do SQL Server hospedados em um servidor diferente daquele que hospeda o compartilhamento de implantação, consulte as propriedades **Database**, **DBID**, **DBPwd**, **Instance**, **NetLib**, **Order**, **Parameters**, **ParameterCondition**, **SQLServer**, **SQLShare** e **Table** no documento do MDT *Referência do Toolkit*.  

 Usando o script ZTIConnect.wsf, é possível conectar-se a outros servidores e acessar os recursos neles. A sintaxe do script ZTIConnect.wsf é a seguinte (em que *caminho_unc* é um caminho UNC para conectar ao servidor):  

```  
Cscript.exe “%SCRIPTROOT%\ZTIConnect.wsf” /uncpath:unc_path  
```  

 Na maioria dos casos, o script ZTIConnect.wsf é executado como uma tarefa do Sequenciador de Tarefas. Execute o script ZTIConnect.wsf antes das tarefas que requerem acesso a um servidor diferente daquele que hospeda o compartilhamento de implantação.  

 **Para adicionar o script ZTIConnect.wsf como uma tarefa à sequência de tarefas de um build**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação*/Task Sequences (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel de detalhes, clique em ***sequência_de_tarefas*** (em que *sequência_de_tarefas* é o nome da sequência de tarefas a ser modificada).  

4.  No painel Ações, clique em **Propriedades**.  

5.  Clique na guia Sequência de Tarefas, navegue até **grupo** (em que *grupo* é o grupo no qual executar o script ZTIConnec.wsf) e clique em **Adicionar**. Clique em **Geral** e, em seguida, em **Executar Linha de Comando**.  

    > [!NOTE]
    >  Adicione a tarefa antes de adicionar tarefas que exijam acesso a recursos no servidor de destino.  

6.  Conclua a guia **Propriedades** da nova tarefa usando as informações a seguir:

    |**Nesta caixa** |**Faça o seguinte** |  
    |-|-|  
    |**Nome** |Digite **Conectar a servidor** (em que servidor se refere ao nome do servidor ao qual você deseja se conectar).|  
    |**Descrição** |Digite o texto que explica por que a conexão precisa ser feita.|  
    |**Comando** |Digite **Cscript.exe “%SCRIPTROOT%\ZTIConnect.wsf” /uncpath:caminho_unc** (em que *caminho_unc* refere-se ao caminho UNC para uma pasta compartilhada no servidor).|  

7.  Conclua a guia **Opções** da nova tarefa usando as informações a seguir. Salvo especificação em contrário, aceite os valores padrão e clique em **OK**.  

    |**Nesta caixa** |**Faça o seguinte** |  
    |-|-|  
    |**Códigos de sucesso** |Digite **0 3010**. (O script de ZTIConnect.wsf retorna esses códigos após a conclusão bem-sucedida.)|  
    |**Caixa de listagem de condições** |Adicione as condições que podem ser necessárias. (Na maioria dos casos, esta tarefa não exige nenhuma condição.)|  

 Depois de adicionar a tarefa que executará o script ZTIConnect.wsf, as tarefas subsequentes poderão acessar os recursos de rede no servidor especificado na opção **/uncpath** do script ZTIConnect.wsf.  

## <a name="deploying-the-correct-device-drivers-to-computers-with-the-same-hardware-devices-but-different-make-and-model"></a>Implantando os drivers de dispositivo corretos em computadores com os mesmos dispositivos de hardware, mas com marca e modelo diferentes  
 Podem ocorrer variações nos nomes e números de modelo sem praticamente nenhuma diferença no conjunto de drivers. Essas variações nos nomes e números de modelo podem aumentar desnecessariamente o tempo gasto criando várias entradas de banco de dados para determinado modelo. O procedimento a seguir mostra como definir uma nova propriedade usando uma chamada de função de saída do usuário que retorna uma subcadeia de caracteres do número do modelo.  

 **Para criar aliases de modelo**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação* (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel Ações, clique em **Propriedades**.  

4.  Na caixa de diálogo **Propriedades**, clique na guia **Variáveis**.  

5.  Crie aliases para tipos de hardware nas seções Marca e Modelo do MDT DB. Trunque o tipo de modelo nos parênteses abertos “(” no nome do modelo. Por exemplo, *HP DL360 (G112)* se torna *HP DL360*.  

6.  Adicione a variável personalizada **ModelAlias** a cada seção.  

7.  Crie uma nova seção `[SetModel]`.  

8.  Adicione a seção `[SetModel]` às configurações de **Prioridade** na seção `[Settings]`.  

9. Adicione uma linha à seção `ModelAlias` para se referir a um script de saída do usuário que truncará o nome do modelo no “(”.  

10. Crie uma pesquisa de banco de dados **MMApplications** na qual **ModelAlias** é igual a **Modelo**.  

11. Crie um script de saída do usuário e coloque-o no mesmo diretório do arquivo CustomSettings.ini para truncar o nome do modelo.  

    O exemplo a seguir mostra um CustomSettings.ini e o script de saída do usuário, respectivamente.  

     **CustomSettings.ini**:  

    ```  
    [Settings]   
    Priority=SetModel, MMApplications, Default   
    Properties= ModelAlias   
    [SetModel]   
    ModelAlias=#SetModelAlias()#   
    Userexit=Userexit.vbs   
    [MMApplications]   
    SQLServer=Server1  
    Database=MDTDB   
    Netlib=DBNMPNTW   
    SQLShare=logs   
    Table= MakeModelSettings    
    Parameters=Make, ModelAlias   
    ModelAlias=Model   
    Order=Sequence  
    ```  

     **Script de saída do usuário**:  

    ```  
    Function UserExit(sType, sWhen, sDetail, bSkip)   
      UserExit = Success   
    End Function   

    Function SetModelAlias()   
      If Instr(oEnvironment.Item("Model"), "(") <> 0 Then   
        SetModelAlias = Left(oEnvironment.Item("Model"), _  
                          Instr(oEnvironment.Item("Model"), _  
                            "(") - 1)   
        oLogging.CreateEntry "USEREXIT – " & _  
          "ModelAlias has been set to " & SetModelAlias, _  
          LogTypeInfo  
      Else   
        SetModelAlias = oEnvironment.Item("Model")   
        oLogging.CreateEntry " USEREXIT - " & _  
          "ModelAlias has not been changed.", LogTypeInfo   
      End if   
    End Function  
    ```  

## <a name="configuring-conditional-task-sequence-steps"></a>Configurando etapas condicionais da sequência de tarefas  
 Em alguns cenários, considere a execução de uma etapa da sequência de tarefas condicionalmente com base em critérios definidos. Qualquer combinação dessas condições pode ser adicionada para determinar se a etapa de sequência de tarefas deve ser executada. Por exemplo, use o valor de uma variável da sequência de tarefas e o valor de uma configuração do Registro para determinar se uma etapa da sequência de tarefas deve ser executada.  

 Usando o MDT, execute uma sequência de tarefas condicionalmente baseada em:  

-   Uma ou mais instruções **IF**  

-   Uma variável de sequência de tarefas  

-   A versão do sistema operacional de destino  

-   Os resultados boolianos de uma consulta WMI  

-   Uma configuração do Registro  

-   O software instalado no computador de destino  

-   As propriedades de uma pasta  

-   As propriedades de um arquivo  

### <a name="configuring-a-conditional-task-sequence-step"></a>Configurando uma etapa condicional da sequência de tarefas  
 Etapas condicionais da sequência de tarefas são configuradas no Deployment Workbench, na guia **Opções** de uma etapa da sequência de tarefas. Você pode adicionar uma ou mais condições à etapa da sequência de tarefas para criar a condição apropriada para executar ou não a etapa.  

> [!NOTE]
>  Cada etapa condicional da sequência e tarefas precisa de pelo menos uma instrução **IF**.  

 **Para exibir a guia Opções de uma etapa da sequência de tarefas**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação*/Task Sequences (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel de detalhes, clique em **sequência_de_tarefas** (em que *sequência_de_tarefas* é o nome da sequência de tarefas a ser configurada).  

4.  No painel Ações, clique em **Propriedades**.  

5.  Na caixa de diálogo **Propriedades da** ***sequência_de_tarefas*** da guia **Sequência de Tarefas**, clique em ***etapa*** (em que *etapa* é o nome da etapa da sequência de tarefas a ser configurada) e, em seguida, clique na guia **Opções**.  

 Na guia **Opções** da etapa da sequência de tarefas, execute as seguintes ações:  

-   **Adicionar.** Clique nesse botão para adicionar uma condição à etapa da sequência de tarefas.  

-   **Remover.** Clique nesse botão para remover uma condição existente da etapa da sequência de tarefas.  

-   **Editar.** Clique nesse botão para modificar uma condição existente à etapa da sequência de tarefas.  

### <a name="if-statements-in-conditions"></a>Instruções IF em condições  
 Todas as condições da sequência de tarefas incluem uma ou mais instruções **IF**. Instruções **IF** são a base da criação de etapas da sequência de tarefa condicional. Uma condição de etapa de sequência de tarefas pode incluir apenas uma instrução **IF**, mas várias instruções **IF** podem ser aninhadas abaixo da instrução **IF** de nível superior para criar condições mais complexas.  

 Uma instrução **IF** pode ser baseada nas condições listadas na tabela a seguir, que são configuradas na caixa de diálogo **Propriedades da instrução IF**.  

 |**Condição** |**Selecione esta opção para executar o if da sequência de tarefas** |  
 |-|-|  
 |**Todas as condições** |Todas as condições abaixo desta instrução **IF** precisam ser verdadeiras.|  
 |**Qualquer condição** |Qualquer condição abaixo desta instrução **IF** é verdadeira.|  
 |**Nenhum** |Nenhuma condição abaixo desta instrução **IF** é verdadeira.|  

 Conclua a condição para executar a etapa da sequência de tarefas adicionando outros critérios para as condições (por exemplo, variáveis de sequência de tarefas ou valores em uma configuração do Registro).  

 **Para adicionar uma condição de instrução IF a uma etapa da sequência de tarefas**  

1.  Na guia **Opção de** ***step*** (em que *step* é o nome da etapa da sequência de tarefas a ser configurada), clique em **Adicionar** e em **Instrução If**.  

2.  Na caixa de diálogo **Propriedades da instrução IF**, clique em **condição** (em que *condição* é uma das condições listadas na tabela anterior) e, em seguida, clique em **OK**.  

### <a name="task-sequence-variables-in-conditions"></a>Variáveis de sequência de tarefas em condições  
 Use a condição **Variável de Sequência de Tarefas** para avaliar qualquer variável de sequência de tarefas criada por uma tarefa **Definir Variável de Sequência de Tarefas** ou por qualquer tarefa na sequência de tarefas. Por exemplo, imagine uma rede que contém computadores cliente com Windows XP que fazem parte de um domínio e alguns que estão em um grupo de trabalho. Sabendo que a política de domínio atual força todas as configurações de usuário a serem salvas na rede, as configurações de usuário podem precisar ser salvas apenas para computadores que não fazem parte do domínio, ou seja, os computadores que estão no grupo de trabalho. Nesse caso, adicione uma condição à tarefa **Capturar arquivos e configurações do usuário** destinada aos computadores no grupo de trabalho.  

 **Para adicionar uma condição baseada em uma variável de sequência de tarefas**  

1.  Na guia **Opções de** ***step*** (em que *step* é o nome da etapa da sequência de tarefas a ser configurada), clique em **Adicionar Condição** e em **Variável da Sequência de Tarefas**.  

2.  Na caixa de diálogo **Condição da variável da sequência de tarefas**, na caixa **Variável**, digite **OSDJoinType**.  

    > [!NOTE]
    >  Essa variável é definida como **0** para computadores que ingressaram em um domínio e como **1** para aqueles que estão em um grupo de trabalho.  

3.  Na caixa **Condição**, clique em **igual**.  

4.  Na caixa **Valor**, digite **1** e clique em **Avançar**.  

### <a name="operating-system-version-in-conditions"></a>Versão do sistema operacional em condições  
 Use a condição **Versão do Sistema Operacional** para verificar a versão do sistema operacional existente de um computador de destino ou cliente existente (durante a captura de uma imagem). Por exemplo, imagine uma rede que contém vários servidores que serão atualizados do Windows Server 2003 para o Windows Server 2008. As configurações de rede devem ser copiadas e aplicadas somente aos servidores que executam o Windows Server 2003. Todos os demais servidores terão as configurações de rede padrão que usa o Windows Server 2008.  

 **Para adicionar uma condição com base na versão do sistema operacional**  

1.  No Editor de Sequência de Tarefas, clique na tarefa **Capturar as configurações de rede**.  

2.  Clique em **Adicionar Condição** e, em seguida, na **Versão do Sistema Operacional**.  

3.  Na caixa **Arquitetura**, clique no servidor relevante. Neste exemplo, clique em **x86**.  

4.  Na caixa **Sistema operacional**, clique no sistema operacional e na versão para os quais uma condição será definida. Neste exemplo, clique em **x86 do Windows 2003**.  

5.  Na caixa **Condição**, clique na condição relevante e, em seguida, em **OK**.  

### <a name="file-properties-in-conditions"></a>Propriedades de arquivo em condições  
 Use a condição **Propriedades do Arquivo** para verificar a versão e/ou o carimbo de data/hora de dado arquivo para determinar se uma tarefa ou um grupo de tarefas deve ser executado ou não. Neste exemplo, o ambiente de produção contém uma imagem do Windows Server 2003 que é constantemente atualizada e usada para cada novo servidor adicionado à rede. Todos os computadores de servidor no ambiente executam um aplicativo personalizado que requer a API (interface de programação de aplicativo) versão 3.60.6815 do DAO (Objeto de Acesso Digital).  

 Todos os servidores existentes estão funcionando corretamente. No entanto, os novos servidores adicionados à rede com a imagem não poderão executar o aplicativo. Como a responsabilidade de manter e atualizar as imagens está a cargo de um grupo diferente, você decide se a sequência de tarefas de implantação é alterada para instalar a versão relevante do DAO caso a versão existente do DAO implantada com a imagem esteja incorreta.  

 **Para adicionar uma condição Propriedades do Arquivo a uma etapa da sequência de tarefas no Configuration Manager 2007 R3**  

1.  No Configuration Manager 2007 R3, crie um pacote para instalar o DAO 3.60.6815. Chame esse pacote *DAO* com um programa denominado *InstallDAO*. Para saber mais sobre a criação de pacotes, consulte [Como criar um pacote](http://technet.microsoft.com/library/bb693627.aspx).  

2.  Crie uma etapa **Instalar Software** para implantar o pacote DAO.  

3.  Clique na etapa da sequência de tarefas **Instalar Software** criada na etapa 2 e, em seguida, na guia **Opções**.  

4.  Clique em **Adicionar Condição**e, em seguida, em **Propriedades do Arquivo**.  

5.  Na caixa **Caminho**, digite **C:\Program Files\Microsoft Shared\DAO\dao360.dll**.  

6.  Marque a caixa de seleção **Verificar a versão** e clique em **não é igual a** para a condição.  

7.  Na caixa **Versão**, digite **3.60.6815**.  

8.  Nesse caso, desmarque a caixa de seleção **Verificar o carimbo de data/hora** e clique em **OK**.  

### <a name="folder-properties-in-conditions"></a>Propriedades de pasta em condições  
 Use a condição **Propriedades da Pasta** para verificar o carimbo de data/hora de certa pasta para determinar se uma tarefa ou um grupo de tarefas deve ser executado. Por exemplo, considere uma situação em que um aplicativo desenvolvido internamente foi atualizado para funcionar com o Windows 8. No entanto, nem todos os computadores na rede tem a versão mais recente do aplicativo instalado, sendo necessário executar um processo de conversão de dados antes de atualizar o aplicativo.  

 Se o carimbo de data/hora da pasta na qual o aplicativo está instalado é 31/12/2007 ou anterior, o computador de destino está executando a versão incompatível do aplicativo e o processo de conversão de dados deve ser executado no computador de destino. Condicionalmente, execute uma etapa de sequência de tarefas para efetuar o processo de conversão de dados em computadores que têm uma versão anterior do aplicativo.  

 **Para adicionar uma condição Propriedades de Pasta a uma etapa da sequência de tarefas**  

1.  No console do Configuration Manager ou no Deployment Workbench, no editor de sequência de tarefas, edite ***sequência_de_tarefas*** (em que *sequência_de_tarefas* refere-se à sequência de tarefas que você deseja editar).  

2.  Crie uma tarefa de **Linha de Comando** para executar o processo de conversão de dados.  

3.  Clique na tarefa criada na etapa 1.  

4.  Clique em **Adicionar Condição**e, em seguida, em **Propriedades da Pasta**.  

5.  Na caixa **Caminho**, digite o caminho da pasta que contém o aplicativo.  

6.  Marque a caixa de seleção **Verificar o carimbo de data/hora**.  

7.  Clique em **Menor ou igual a** para a condição.  

8.  Na caixa **Data**, clique em **31/12/2007**.  

9. Na caixa **Hora**, clique em **12:00:00 AM** e, em seguida, em **OK**.  

### <a name="registry-settings-in-conditions"></a>Configurações do Registro em condições  
 Use a condição **Configuração de Registro** para verificar a existência de chaves e valores do Registro e os dados correspondentes armazenados nos valores de Registro. Por exemplo, imagine um caso em que um aplicativo atualmente usado em um pequeno conjunto de computadores não pode ser executado no Windows 8 e uma implantação do Windows 8 está em vigor para atualizar os computadores que estão executando o Windows XP. Crie uma condição na primeira tarefa de uma sequência para verificar o Registro de uma entrada para o aplicativo incompatível e para interromper o processo de implantação para o computador em questão, se ele for encontrado.  

 **Para adicionar uma condição Configuração de Registro a uma etapa da sequência de tarefas**  

1.  No console do Configuration Manager ou no Deployment Workbench, no editor de sequência de tarefas, edite ***sequência_de_tarefas*** (em que *sequência_de_tarefas* refere-se à sequência de tarefas que implanta o Windows 8).  

2.  Clique na primeira tarefa na sequência e, em seguida, clique na guia **Opções**.  

3.  Clique em **Adicionar Condição**e, em seguida, em **Configuração de Registro**.  

4.  Na lista **Chave raiz**, clique em **HKEY_LOCAL_MACHINE**.  

5.  Na caixa **Chave**, digite **SOFTWARE\WOODGROVE**.  

6.  Clique em **não existe** para a condição. Nesse caso, a tarefa será executada e a sequência continuará somente se a chave não existir.  

7.  Opcionalmente, a condição poderá verificar a inexistência de um valor se o nome do valor for digitado na caixa **Nome do valor**.  

8.  Se uma condição diferente de **existe/não existe** foi usada, especifique um valor e o tipo de valor.  

9. Clique em **OK**.  

### <a name="wmi-queries-in-conditions"></a>Consultas WMI em condições  
 Use a condição **Consulta WMI** para executar qualquer consulta WMI. A condição será avaliada como True se a consulta retornar pelo menos um resultado. Por exemplo, imagine que uma equipe de implantação que precisa atualizar o sistema operacional de todos os servidores de determinado modelo – Dell 1950, por exemplo. Use uma consulta WMI para verificar o modelo de cada computador e continuar com a implantação somente se o modelo certo foi encontrado.  

 **Para adicionar uma condição Consulta WMI a uma etapa da sequência de tarefas**  

1.  No console do Configuration Manager ou no Deployment Workbench, no editor de sequência de tarefas, edite ***sequência_de_tarefas*** (em que *sequência_de_tarefas* refere-se à sequência de tarefas que atualizará os servidores).  

2.  Clique na primeira tarefa na sequência e, em seguida, clique na guia **Opções**.  

3.  Clique em **Adicionar Condição**e, em seguida, em **Consultar WMI**.  

4.  Na caixa **Namespace de WMI**, digite **root\cimv2**.  

5.  Na caixa **Consulta WQL**, digite **Select \* From Win32_ComputerSystem WHERE Model LIKE "%Dell%%1950%"**. Clique em **OK**.  

### <a name="installed-software-in-conditions"></a>Software instalado em condições  
 Use uma condição **Software Instalado** para verificar se certo software está instalado atualmente em um computador de destino. Apenas software instalado usando arquivos MSI (Microsoft Installer) pode ser avaliado usando essa condição. Por exemplo, imagine que você deseja atualizar o sistema operacional de todos os servidores, exceto os que executam o Microsoft SQL Server 2012.  

 **Para adicionar uma condição Software Instalado a uma etapa da sequência de tarefas**  

1.  No console do Configuration Manager ou no Deployment Workbench, no editor de sequência de tarefas, edite ***sequência_de_tarefas*** (em que *sequência_de_tarefas* refere-se à sequência de tarefas que atualizará os servidores).  

2.  Clique na primeira tarefa na sequência e, em seguida, clique na guia **Opções**.  

3.  Clique em **Adicionar Condição**e, em seguida, em **Software Instalado**.  

4.  Clique em **Procurar** e, em seguida, no arquivo MSI para o SQL Server 2012.  

5.  Marque a caixa de seleção **Corresponder a este produto específico** para especificar que somente computadores com SQL Server 2012, e nenhuma outra versão, são os computadores de destino que essa consulta deve detectar.  

6.  Clique em **OK**.  

### <a name="complex-conditions"></a>Condições Complexas  
 Várias condições podem ser agrupadas usando instruções **IF** para criar condições complexas. Por exemplo, imagine que determinada etapa deve ser executada apenas para computadores Contoso 1950 que executam o Windows Server 2003 ou o Windows Server 2008. Escrita como uma instrução **IF** programática, ela seria semelhante ao seguinte:  

```  
IF ((Computer Model IS “Contoso 1950”) AND (operating system=2003 OR operating system=2008))  
```  

 **Para adicionar uma condição complexa**  

1.  No console do Configuration Manager ou no Deployment Workbench, no editor de sequência de tarefas, edite ***sequência_de_tarefas*** (em que *sequência_de_tarefas* refere-se à sequência de tarefas que atualizará os servidores).  

2.  Clique na etapa da sequência de tarefas para a qual adicionar a condição e, em seguida, clique na guia **Opções**.  

3.  Clique em **Adicionar condição**, na **Instrução If** e depois em **Todas as condições**. Clique em **OK**.  

4.  Clique na instrução de condição, em **Adicionar condição** e, em seguida, em **Consulta WMI**.  

5.  Verifique se **root\cimv2** foi especificado como o namespace do WMI e, em seguida, na caixa **Consulta WQL**, digite **SELECT \* FROM Win32_ComputerSystem WHERE ComputerModel LIKE “%Contoso%1950%”**. Clique em **OK**.  

6.  Clique na instrução **IF** e depois clique em **Adicionar condição**. Clique na **Instrução If** e, em seguida, em **Qualquer condição**. Clique em **OK**.  

7.  Clique na segunda instrução **IF**. Clique em **Adicionar condição** e, em seguida, na **Versão do sistema operacional**.  

8.  Na caixa **Arquitetura**, clique na arquitetura para os servidores. Neste exemplo, clique em **x86**.  

9. Na caixa **Sistema operacional**, clique no sistema operacional e na versão. Neste exemplo, clique em **versão original x86 do Windows 2003**. Clique em **OK**.  

10. Clique na segunda instrução **IF**. Clique em **Adicionar condição** e, em seguida, na **Versão do sistema operacional**.  

11. Na caixa **Arquitetura**, clique na arquitetura para os servidores. Neste exemplo, clique em **x86**.  

12. Na caixa **Sistema operacional**, clique no sistema operacional e na versão. Neste exemplo, clique em **versão original x86 do Windows 2008**. Clique em **OK**.  

## <a name="creating-a-highly-scalable-lti-deployment-infrastructure"></a>Criando uma infraestrutura de implantação de LTI altamente escalonável  
 Nesse cenário, nenhuma distribuição de software eletrônico está disponível para ser aproveitado pela infraestrutura de implantação, por isso utilize o MDT para criar uma infraestrutura de implantação LTI totalmente automatizada. A infraestrutura LTI escalonável usa o SQL Server, os Serviços de Implantação do Windows e tecnologias do DFS-R (Replicação do Sistema de Arquivos Distribuído) do Windows Server 2003.  

 Dimensione a infraestrutura LTI da seguinte forma:  

-   Garantindo que a infraestrutura apropriada existe, conforme descrito em [Garantindo a existência da infraestrutura apropriada](#EnsureInfrastructure)  

-   Adicionando conteúdo ao MDT, conforme descrito em [Adicionando conteúdo ao MDT](#AddContent)  

-   Preparando os Serviços de Implantação do Windows, conforme descrito em [Preparando os Serviços de Implantação do Windows](#PrepareDeployment)  

-   Configurando o DFS-R, como descrito em [Configurando a replicação de Sistema de Arquivos Distribuído](#ConfigureFileReplication)  

-   Configurando a replicação do SQL Server, conforme descrito em [Preparando a replicação do SQL Server](#PrepareSQLReplication)  

-   Configurando a replicação do SQL Server, conforme descrito em [Configurando a replicação do SQL Server](#ConfigureSQLReplication)  

 Este cenário pressupõe que o MDT está configurado em um servidor de implantação mestre e que a configuração do MDT DB já foi concluída, conforme discutido no início deste documento.  

###  <a name="EnsureInfrastructure"></a> Garantindo a existência da infraestrutura apropriada  
 A infraestrutura de implantação LTI altamente escalonável usa uma topologia hub-spoke para replicação de conteúdo, portanto, designe primeiro um servidor de implantação no ambiente de produção que executará a função de servidor de implantação mestre.  Veja a seguir uma lista dos componentes necessários para o servidor de implantação mestre.  

 |**Componente obrigatório** |**Finalidade/comentário** |  
 |-|-|  
 |Windows Server 2003 R2|Obrigatório para dar suporte a DFS-R|  
 |MDT |Contém a cópia mestra do compartilhamento de implantação|  
 |SQL Server 2005|Precisa ser uma versão completa para permitir a replicação do MDT DB|  
 |DFS-R |Obrigatório para replicação do compartilhamento de implantação|  
 |Serviços de Implantação do Windows |Obrigatório para permitir que instalações de rede baseadas em PXE sejam iniciadas|  

 Após ter selecionado o servidor de implantação mestre, provisione servidores adicionais em cada site para dar suporte a implantações LTI.  Veja a seguir uma lista dos componentes necessários para o servidor de implantação filho.  

 |**Componente obrigatório** |**Finalidade/comentário** |  
 |-|-|  
 |Windows Server 2003 R2|Obrigatório para dar suporte a DFS-R|  
 |Microsoft SQL Server 2005 Express Edition |Recebe cópias replicadas do MDT DB|  
 |DFS-R |Obrigatório para replicação do compartilhamento de implantação|  
 |Serviços de Implantação do Windows |Obrigatório para permitir que instalações de rede baseadas em PXE sejam iniciadas|  

> [!NOTE]
>  Os Serviços de Implantação do Windows precisam ser instalados e configurados em cada servidor filho, mas não é necessário adicionar imagens de inicialização ou instalação.  

###  <a name="AddContent"></a> Adicionando conteúdo ao MDT  
 Popule o servidor de implantação mestre com o conteúdo usando o Deployment Workbench, e crie e popule o MDT DB, conforme descrito nas seções a seguir. Para obter informações sobre como popular o banco de dados com:  

-   Aplicativos, consulte a seção “Configurando aplicativos no Deployment Workbench”, no documento do MDT *Usando o Microsoft Deployment Toolkit*  

-   Sistemas operacionais, consulte a seção “Configurando sistemas operacionais no Deployment Workbench”, no documento do MDT *Usando o Microsoft Deployment Toolkit*  

-   Pacotes de sistemas operacionais, consulte a seção “Configurando pacotes no Deployment Workbench”, no documento do MDT *Usando o Microsoft Deployment Toolkit*  

-   Drivers de dispositivo, consulte a seção “Configurando drivers de dispositivo no Deployment Workbench”, no documento do MDT *Usando o Microsoft Deployment Toolkit*  

-   Sequências de tarefas, consulte a seção “Configurando sequências de tarefas no Deployment Workbench”, no documento do MDT *Usando o Microsoft Deployment Toolkit*  

> [!NOTE]
>  Verifique se o arquivo LiteTouchPE_x86.wim criado quando o compartilhamento de implantação é atualizado foi adicionado aos Serviços de Implantação do Windows.  

###  <a name="PrepareDeployment"></a> Preparando os Serviços de Implantação do Windows  
 Como o arquivo LiteTouchPE_x86.wim será replicado periodicamente por meio do grupo de replicação do DFS-R, o armazenamento de dados de configuração da inicialização precisa ser atualizado periodicamente para refletir o ambiente do Windows PE recém-replicado. Execute as etapas a seguir em cada um dos servidores de implantação.  

 **Para preparar os Serviços de Implantação do Windows**  

1.  Abra uma janela do Prompt de Comando.  

2.  Digite **WDSUtil/set-server/BCDRefreshPolicy/Enabled:yes/RefreshPeriod:60** e pressione ENTER.  

> [!NOTE]
>  No exemplo apresentado aqui, o período de atualização é definido como 60 minutos, no entanto, você pode configurar esse valor para ser replicado durante um período igual ao DFS-R.  

###  <a name="ConfigureFileReplication"></a> Configurando a Replicação do Sistema de Arquivos Distribuído  
 Ao dimensionar a arquitetura de implantação LTI, use o DFS-R como base para replicar o conteúdo do compartilhamento de implantação do MDT, do ambiente de inicialização Lite Touch do Windows PE e do servidor de implantação mestre para os servidores de implantação filho.  

> [!NOTE]
>  Verifique se o DFS-R está instalado antes de executar as etapas a seguir.  

 **Para configurar o DFS-R para replicar o conteúdo de implantação**  

1.  Abra o console de Gerenciamento de DFS.  

2.  No console de Gerenciamento de DFS, expanda Gerenciamento de DFS.  

3.  Clique com o botão direito do mouse em **Replicação** e, em seguida, clique em **Novo Grupo de Replicação**.  

4.  No Assistente de Novo Grupo de Replicação, na página **Tipo do Grupo de Replicação**, clique em **Novo Grupo de Replicação Multiuso**.  

5.  Clique em **Avançar**.  

6.  Na página **Nome e Domínio**, digite as seguintes informações:  

    -   Na caixa **Nome do grupo de replicação**, digite um nome para o grupo de replicação, por exemplo, **Grupo de replicação do MDT 2010**.  

    -   Na caixa **Descrição opcional do grupo de replicação**, digite uma descrição do grupo de replicação, por exemplo, **Grupo de replicação dos dados do MDT 2010**.  

    -   Verifique se a caixa **Domínio** contém o nome de domínio correto.  

7.  Clique em **Avançar**.  

8.  Na página **Membros do Grupo de Replicação**, realize estas etapas:  

    1.  Clique em **Adicionar**.  

    2.  Digite os nomes de todos os servidores que devem ser membros desse grupo de replicação – por exemplo, todos os servidores de implantação filho e o servidor de implantação mestre.  

    3.  Clique em **OK**.  

9. Clique em **Avançar**.  

10. Na página **Seleção de Topologia**, clique em **Hub e Spoke** e, em seguida, em **Avançar**.  

11. Na página **Membros do Hub**, clique no servidor de implantação mestre e, em seguida, em **Adicionar**.  

12. Clique em **Avançar**.  

13. Na página **Conexões de Hub e Spoke**, verifique se **Membro do Hub Obrigatório** está listado como o servidor de implantação mestre para todos os servidores de implantação filho.  

14. Clique em **Avançar**.  

15. Na página **Agendamento e largura de banda do grupo de replicação**, especifique uma agenda para replicar o conteúdo entre os servidores.  

16. Clique em **Avançar**.  

17. Na página **Membro Primário**, na caixa **Membro Primário**, clique no servidor de implantação mestre.  

18. Clique em **Avançar**.  

19. Na página **Pastas a serem replicadas**, clique em **Adicionar** e, em seguida, execute estas etapas:  

    1.  Na caixa **Caminho local da pasta a ser replicada**, clique em **Procurar** para ir para a pasta *X:\\*Deployment (em que *X* é a letra da unidade no servidor de implantação).  

    2.  Clique em **Usar nome baseado no caminho**.  

    3.  Clique em **OK**.  

    4.  Clique em **Adicionar**.  

    5.  Na caixa de diálogo **Adicionar pasta a ser replicada**, clique em **Procurar** para ir para a pasta *X:* \RemoteInstall\Boot.  

    6.  Clique em **Usar nome baseado no caminho**.  

20. Clique em **Avançar**.  

21. Na página **Caminho local de distribuição em outros membros**, execute estas etapas:  

    1.  Selecione todos os membros do grupo de distribuição e, em seguida, clique em **Editar**.  

    2.  Na caixa de diálogo **Editar caminho Local**, clique em **Habilitado**.  

    3.  Digite o caminho em que a pasta Deployment Share deve ser armazenada no servidor de implantação filho – por exemplo, ***X:\Deployment*** (em que *X* é a letra da unidade no servidor de implantação).  

    4.  Clique em **OK**.  

22. Clique em **Avançar**.  

23. Na página **Caminho local de inicialização em outros membros**, execute estas etapas:  

    1.  Selecione todos os membros do grupo de distribuição e, em seguida, clique em **Editar**.  

    2.  Na caixa de diálogo **Editar caminho Local**, clique em **Habilitado**.  

    3.  Digite o caminho em que a pasta Boot deve ser armazenada no servidor de implantação filho – por exemplo, ***X:\RemoteInstall\Boot*** (em que *X* é a letra da unidade no servidor de implantação).  

    4.  Clique em **OK**.  

24. Clique em **Avançar**.  

25. Na página **Configurações remotas e criar o grupo de replicação**, clique em **Criar** para concluir o Assistente de Novo Grupo de Replicação.  

26. Na página **Configuração**, clique em **Fechar** para fechar o assistente.  

> [!NOTE]
>  Verifique se o novo grupo de replicação agora está listado sob o nó Replicação.  

###  <a name="PrepareSQLReplication"></a> Preparando-se para a Replicação do SQL Server  
 Para que a replicação do SQL Server possa ser configurada, conclua as diversas etapas de pré-configuração para garantir que os servidores de implantação estejam devidamente configurados.  

 **Para se preparar para a replicação do SQL Server no servidor de implantação mestre**  

1.  Crie uma pasta para armazenar os instantâneos do banco de dados e, em seguida, configure-a como um compartilhamento.  

    > [!NOTE]
    >  Para obter mais informações sobre como proteger a pasta de instantâneos, consulte [Protegendo a pasta de instantâneos](http://msdn2.microsoft.com/library/ms151151.aspx).  

2.  Verifique se o serviço do SQL Server Browser está habilitado e definido como Automático.  

3.  Na caixa **Configuração da área de superfície do SQL Server**, clique em **Conexões locais e remotas**.  

 **Para se preparar para a replicação do SQL Server no servidor de implantação filho**  

1.  Na caixa **Configuração da área de superfície do SQL Server**, clique em **Conexões locais e remotas**.  

2.  Opcionalmente, crie um banco de dados vazio para hospedar o MDT DB replicado.  

> [!NOTE]
>  Este banco de dados precisa receber o mesmo nome que o MDT DB no servidor de implantação mestre. Por exemplo, se o MDT DB no servidor de implantação mestre for chamado de *MDTDB*, crie um banco de dados vazio chamado *MDTDB* no servidor de implantação filho.  

###  <a name="ConfigureSQLReplication"></a> Configurando a Replicação do SQL Server  
 Depois de configurar a replicação de arquivos e pastas necessárias para criar a infraestrutura de implantação, configure o SQL Server para replicar o MDT DB.  

> [!NOTE]
>  Também é possível manter apenas um único MDT DB central, no entanto, manter uma versão replicada do MDT DB proporciona maior controle sobre os dados transferidos por WAN (rede de longa distância).  

 O SQL Server 2005 usa um modelo de replicação semelhante a um modelo de distribuição de revista:  

1.  Uma *revista* é disponibilizada (publicada) por um *publicador*.  

2.  *Distribuidores* são usados para distribuir a publicação.  

3.  Os *Leitores* podem assinar uma publicação para que essa publicação seja entregue ao assinante periodicamente (uma *assinatura push*).  

 Essa terminologia é usada por meio dos assistentes de configuração e instalação de replicação do SQL Server.  

#### <a name="configure-a-sql-server-publisher"></a>Configurar um publicador do SQL Server  
 Para configurar o servidor de implantação mestre como um publicador do SQL Server, execute estas etapas:  

1.  Abra o SQL Server Management Studio.  

2.  Clique com o botão direito do mouse no nó **Replicação** e, em seguida, clique em **Configurar Distribuição**.  

3.  No Assistente para configurar distribuição, clique em **Avançar**.  

4.  Na página **Distribuidor**, clique em **atuará como seu próprio Distribuidor; o SQL Server criará um banco de dados e um log de distribuição** e, em seguida, em **Avançar**.  

5.  Na página **Pasta de Instantâneo**, na seção **Preparando para replicação do SQL Server**, digite o caminho UNC para a pasta de instantâneo criada.  

6.  Na página **Banco de Dados de Distribuição**, clique em **Avançar**.  

7.  Na página **Publicadores**, clique no servidor de implantação mestre para defini-lo como o distribuidor e, em seguida, clique em **Avançar**.  

8.  Na página **Ações do Assistente**, clique em **Configurar Distribuição** e, em seguida, em **Avançar**.  

9. Clique em **Concluir** e, em seguida, em **Fechar** quando o assistente estiver concluído.  

#### <a name="enable-the-mdt-db-for-replication"></a>Habilitar o MDT DB para Replicação  
 Para habilitar o MDT DB para replicação no servidor de implantação mestre, execute estas etapas:  

1.  No SQL Server Management Studio, clique com o botão direito do mouse no nó **Replicação** e, em seguida, clique em **Propriedades do Publicador**.  

2.  Na página **Propriedades do Publicador**, execute estas etapas:  

    1.  Clique em **Bancos de Dados Publicadores**.  

    2.  Clique no MDT DB e, em seguida, clique em **Transacional**.  

    3.  Clique em **OK**.  

 O MDT DB agora está configurado para replicação transacional e de instantâneo.  

#### <a name="create-a-publication-of-the-mdt-db"></a>Criar uma publicação do MDT DB  
 Para criar uma publicação do MDT DB que os servidores de implantação filho podem assinar, execute estas etapas:  

1.  No SQL Server Management Studio, expanda Replicação, clique com o botão direito do mouse em **Publicações Locais** e, em seguida, clique em **Nova Publicação**.  

2.  No Assistente para Nova Publicação, clique em **Avançar**.  

3.  Na página **Banco de Dados de Publicação**, clique em MDT DB e, em seguida, em **Avançar**.  

4.  Na página **Tipo de Publicação**, clique em **Publicação de instantâneo** e, em seguida, em **Avançar**.  

5.  Na página **Artigos**, selecione todas as **Tabelas, Procedimentos Armazenados** e **Exibições** e clique em **Avançar**.  

6.  Na página **Edições de Artigos**, clique em **Avançar**.  

7.  Na página **Filtrar Linhas da Tabela**, clique em **Avançar**.  

8.  Na página **Agente de Instantâneo**, execute estas etapas:  

    1.  Marque **Criar um instantâneo imediatamente e mantê-lo disponível para inicializar assinaturas**.  

    2.  Clique em **Agendar o Agente de Instantâneo para execução nos seguintes horários**.  

    3.  Clique em **Alterar**.  

    > [!NOTE]
    >  Especifique uma agenda que ocorrerá uma hora antes da replicação do banco de dados.  

9. Clique em **Avançar**.  

10. Na página **Segurança do Agente**, clique na conta que executará o agente de instantâneo e, em seguida, em **Avançar**.  

11. Na página **Ações do Assistente**, clique em **Configurar a publicação** e em **Avançar**.  

12. Na página **Concluir o Assistente**, na caixa **nome da publicação**, digite um nome descritivo para a publicação.  

13. Clique em **Concluir** para concluir o assistente e, em seguida, em **Fechar** quando o assistente tiver criado a publicação.  

    > [!NOTE]
    >  A publicação ficará visível abaixo do nó Publicações Locais no SQL Server Management Studio.  

#### <a name="subscribe-child-deployment-servers-to-the-published-mdt-db"></a>Faça com que os servidores de implantação filho assinem o MDT DB publicado  
 Agora que o MDT DB foi publicado, você pode adicionar servidores de implantação filho como assinantes a esta publicação, ou seja, eles receberão uma cópia do banco de dados regularmente, de forma que, durante uma implantação, os computadores cliente possam consultar um banco de dados local na rede em vez de pela WAN.  

 **Para fazer com que os servidores de implantação filho assinem a publicação do MDT DB**  

1.  No SQL Server Management Studio, acesse Replicação/Publicações Locais.  

2.  Clique com o botão direito do mouse na publicação criada na seção anterior e, em seguida, clique em **Novas Assinaturas**.  

3.  No Assistente de Novas Assinaturas, clique em **Avançar**.  

4.  Na página **Publicação**, clique na publicação criada na seção anterior.  

5.  Na página **Local do Agente de Distribuição**, clique em **Executar todos os agentes no SERVERNAME do distribuidor (assinaturas push)** e, em seguida, em **Avançar**.  

6.  Na página **Assinantes**, adicione cada um dos servidores de implantação filho executando as seguintes etapas:  

    1.  Clique em **Adicionar Assinante**e, em seguida, em **Adicionar Assinante ao SQL Server**.  

    2.  Adicione cada servidor de implantação filho.  

    3.  Para cada servidor de implantação filho adicionado, na caixa **Banco de dados de assinatura**, clique no MDT DB vazio nesse servidor de implantação filho.  

    > [!NOTE]
    >  Se o MDT DB ainda não foi criado, na caixa **Banco de Dados de Assinatura**, selecione a opção para criar um novo banco de dados.  

    > [!NOTE]
    >  Este banco de dados precisa receber o mesmo nome que o MDT DB no servidor de implantação mestre. Por exemplo, se o MDT DB no servidor de implantação mestre for chamado de *MDTDB*, crie um banco de dados vazio chamado *MDTDB* no servidor de implantação filho.  

7.  Clique em **Avançar**.  

8.  Na página **Segurança do Agente de Distribuição**, clique em **...** para abrir a caixa de diálogo **Segurança do Agente de Distribuição**.  

9. Digite os detalhes da conta a ser usado para o agente de distribuição e clique em **Avançar**.  

10. Na página **Agenda de Sincronização**, execute estas etapas:  

    1.  Na caixa **Agenda do Agente**, clique em **<Definir agendamento\>**.  

    2.  Especifique o agendamento que deve ser usado para replicar o banco de dados entre os servidores de implantação mestre e filho e, em seguida, clique em **Avançar**.  

11. Na página **Inicializar Assinatura**, clique em **Avançar**.  

12. Na página **Ações do Assistente**, clique em **Criar as assinaturas** e em **Avançar**.  

13. Clique em **Concluir** e, em seguida, em **Fechar** quando o assistente tiver sido concluído com êxito.  

 A replicação do SQL Server agora está configurada e o MDT DB será replicado do servidor de implantação mestre para todos os servidores de implantação filho inscritos nele periodicamente.  

#### <a name="configure-customsettingsini"></a>Configurar CustomSettings.ini  
 A infraestrutura de implantação LTI agora foi criada com êxito, e cada local conterá um servidor de implantação LTI com uma cópia replicada dos seguintes itens:  

-   O compartilhamento de implantação  

-   O MDT DB  

-   O ambiente LiteTouchPE_x86 do Windows PE que foi adicionado aos Serviços de Implantação do Windows  

 Agora, é possível configurar o arquivo CustomSettings.ini para o compartilhamento de implantação usar o conteúdo de implantação (banco de dados e compartilhamento de implantação) do seu servidor de implantação local, o servidor que fornece o ambiente LiteTouchPE_x86.wim por meio dos Serviços de Implantação do Windows.  

 Quando o arquivo LiteTouchPE_x86.wim é recebido dos Serviços de Implantação do Windows, uma chave do Registro é configurada com o nome do servidor de Serviços de Implantação do Windows que você está usando. O MDT captura este nome do servidor em uma variável (%WDSServer%) que pode ser usada para configurar o CustomSettings.ini.  

 **Sempre usar o servidor de implantação LTI local**  

> [!NOTE]
>  O procedimento a seguir pressupõe que o compartilhamento de implantação foi criado e definido como o compartilhamento Deployment$.  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação* (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel Ações, clique em **Propriedades**.  

4.  Clique na guia **Regras** e, em seguida, modifique o arquivo CustomSettings.ini para configurar as seguintes propriedades:  

    -   Para cada seção do SQL Server adicionada, configure **SQLServer** para usar o nome do servidor **%WDSServer%—** por exemplo, **SQLServer=%WDSServer%**.  

    -   Se **DeployRoot** for configurado, defina **DeployRoot** para usar a variável **%WDSServer%** – por exemplo, **DeployRoot=\\\\%WDSServer%\Deployment$**.  

5.  Clique em **Editar Bootstrap.ini**.  

6.  Configure o BootStrap.ini para usar a propriedade **%WDSServer%** adicionando ou alterando o valor **DeployRoot** para **DeployRoot=\\\\%WDSServer%\Deployment$**.  

7.  Clique em **Arquivo** e, em seguida, em **Salvar** para salvar as alterações no arquivo BootStrap.ini.  

8.  Clique em **OK**.  

     O compartilhamento de implantação e o ambiente LiteTouchPE_x86.wim do Windows PE precisam ser atualizados.  

9. No painel Ações, clique em **Atualizar Compartilhamento de Implantação**.  

     O Assistente de Atualização de Compartilhamento de Implantação é iniciado.  

10. Na página **Opções**, selecione as opções desejadas para atualizar o compartilhamento de implantação e clique em **Avançar**.  

11. Na página **Resumo**, verifique se os detalhes estão corretos e clique em **Avançar**.  

12. Na página **Confirmação**, clique em **Concluir**.  

 O exemplo a seguir ilustra o CustomSettings.ini depois de executar as etapas descritas nesta seção.  

 **CustomSettings.ini de exemplo configurado para infraestrutura de implantação LTI escalonável**  

```  
[Settings]  
Priority=CSettings,CPackages, CApps, CAdmins, CRoles, Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac  

[CSettings]  
SQLServer=%WDSServer%  
Instance=  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerSettings  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  

[CPackages]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerPackages  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
Order=Sequence  

[CApps]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerApplications  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
Order=Sequence  

[CAdmins]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerAdministrators  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  

[CRoles]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerRoles  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
```  

## <a name="selecting-a-local-mdt-server-when-multiple-servers-exist"></a>Selecionando um servidor MDT local quando existem vários servidores  
 Nesse cenário, vários servidores MDT estão sendo usados para dar suporte a um alto volume de implantações simultâneas e em vários sites. Quando uma implantação LTI é inicializada, o comportamento padrão é solicitar um caminho para o servidor MDT para conectar e acessar os arquivos necessários para iniciar o processo de implantação.  

 O Assistente de Implantação do Windows pode usar o arquivo LocalServer.xml para apresentar uma opção de servidores de implantação conhecidos para cada local.  

 Use o arquivo LocationServer.xml da seguinte forma:  

-   Entendendo a finalidade e uso do LocationServer.xml conforme descrito em [Entendendo o LocationServer.xml](#UnderstandingLocationServer)  

-   Criando o arquivo LocationServer.xml como descrito em [Criando o arquivo LocationServer.xml](#CreateLocationServer)  

-   Adicionando o arquivo LocationServer.xml ao diretório de arquivos extras, como descrito em “Adicionando o arquivo LocationServer.xml ao diretório Extra Files”  

-   Atualizando o arquivo BootStrap.ini, conforme descrito em [Atualizando o arquivo BootStrap.ini](#UpdateBootstrap)  

-   Atualizando o compartilhamento de implantação, conforme descrito em [Atualizando o compartilhamento de implantação](#UpdateDeploymentShare)  

 Este cenário pressupõe que o MDT está configurado em um servidor de implantação.  

###  <a name="UnderstandingLocationServer"></a> Entendendo o LocationServer.xml  
 Primeiro, é necessário entender como o MDT usa LocationServer.xml. Durante o LTI, os scripts do MDT leem e processam o arquivo BootStrap.ini para coletar informações iniciais sobre a implantação. Isso ocorre antes de estabelecer uma conexão com o servidor de implantação. Portanto, a propriedade **DeployRoot** normalmente é usada para especificar no arquivo BootStrap.ini o servidor de implantação com o qual uma conexão deve ser estabelecida.  

 Se o arquivo BootStrap.ini não contém uma propriedade **DeployRoot**, os scripts do MDT carregam uma página do assistente para solicitar ao usuário um caminho para o servidor de implantação. Ao inicializar a página do assistente **HTA (Aplicativo HTML)**, os scritps do MDT verificam a existência do arquivo LocationServer.xml e, se ele existir, usa LocationServer.xml para exibir os servidores de implantação disponíveis.  

#### <a name="understand-when-to-use-locationserverxml"></a>Entender quando usar o LocationServer.xml  
 O MDT oferece várias maneiras de determinar a qual servidor se conectar durante uma implantação LTI. Diferentes métodos para localizar o servidor de implantação são mais adequados para cenários diferentes, por isso, é importante entender quando usar o LocationServer.xml.  

 O MDT fornece vários métodos para descobrir automaticamente e usar o servidor de implantação mais apropriado. Esses métodos estão listados na tabela a seguir.

 |**Método** |**Detalhes** |  
 |-|-|  
 |**%WDSServer%** |Esse método é usado quando o servidor do MDT é coohospedado no servidor dos Serviços de Implantação do Windows.<br /><br /> Quando uma implantação LTI é iniciada dos Serviços de Implantação do Windows, uma variável de ambiente – %WDSServer% – é criada e populada com o nome do servidor dos Serviços de Implantação do Windows.<br /><br /> A variável **DeployRoot** pode usar essa variável para se conectar automaticamente a um compartilhamento de implantação no servidor dos Serviços de Implantação do Windows, como por exemplo:<br /><br /> **DeployRoot=\\\\%WDSServer%\Deployment$** |  
 |**Automação baseada na localização** |O MDT pode usar a automação baseada na localização no arquivo BootStrap.ini para determinar o servidor de implantação.<br /><br /> Use a propriedade **Gateway Padrão** para distinguir entre locais diferentes; para cada **Gateway Padrão**, é especificado um servidor diferente do MDT.<br /><br /> Para obter mais informações sobre como usar a automação baseada em local, consulte “Selecionando os métodos para aplicar os parâmetros de configuração”.|  

 Cada abordagem listada na tabela anterior oferece uma maneira de automatizar a seleção do servidor de implantação em um determinado local para certos cenários. Esses métodos destinam-se a cenários específicos como, por exemplo, quando o servidor do MDT é coospedado junto com os Serviços de Implantação do Windows.  

 Há outros cenários para os quais tais abordagens não são adequadas, por exemplo, se há vários servidores de implantação em determinado local ou a lógica de automação está indisponível (por exemplo, a rede não está segmentada o suficiente para permitir a determinação do local ou o servidor do MDT está separado dos Serviços de Implantação do Windows).  

 Nesses cenários, o arquivo LocationServer.xml fornece um modo flexível de apresentar essas informações no momento da implantação sem precisar conhecer os nomes do servidor e os nomes do compartilhamento de implantação.  

###  <a name="CreateLocationServer"></a> Criando o arquivo LocationServer.xml  
 Para apresentar uma lista de servidores de implantação disponíveis durante a implantação LTI, crie um arquivo LocationServer.xml que contém detalhes sobre cada servidor. Não há um arquivo LocationServer.xml padrão no MDT, portanto, crie um usando as diretrizes a seguir.  

#### <a name="create-a-locationserverxml-file-to-support-multiple-locations"></a>Criar um arquivo LocationServer.xml para dar suporte a vários locais  
 O método mais simples de criar e usar o LocationServer.xml é criar um arquivo LocationServer.xml e adicionar as entradas para cada servidor de implantação no ambiente (que pode estar no mesmo local ou em locais diferentes).  

 Construa o arquivo LocationServer.xml criando uma nova seção para cada servidor e, em seguida, adicionando as seguintes informações:  

-   Um identificador exclusivo  

-   Um nome de local usado para apresentar um nome de fácil identificação para esse local  

-   Um caminho UNC para o servidor do MDT para esse local  

 Veja a seguir como o arquivo LocationServer.xml é criado com cada uma dessas propriedades usando um arquivo LocationServer.xml de exemplo configurado para vários locais.  

 **Arquivo LocationServer.xml de exemplo para dar suporte a vários locais**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS01\Deployment$</UNCPath>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso NYC, New York, USA  
        </friendlyname>  
        <UNCPath>\\NYCDS01\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

 Usando esse formato, especifique as entradas de servidor diferente para cada local ou para situações em que há vários servidores em um único local, especificando uma entrada de servidor diferente para cada servidor nesse local, conforme mostrado no exemplo a seguir.   

 **Arquivo LocationServer.xml de exemplo para dar suporte a diversos servidores em vários locais**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ DS1, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS01\Deployment$</UNCPath>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso HQ DS2, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS02\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

#### <a name="create-a-locationserverxml-file-to-load-balance-multiple-servers-at-different-locations"></a>Crie um arquivo LocationServer.xml para balancear carga de vários servidores em diferentes locais  
 Usando o LocationServer.xml, especifique vários servidores por entrada de local e, em seguida, execute o balanceamento de carga básico para que quando um local for escolhido, o MDT selecione automaticamente um servidor de implantação na lista de servidores disponíveis. Para fornecer essa funcionalidade, o arquivo LocationServer.xml dá suporte à especificação de uma métrica de ponderação.  

 O exemplo a seguir ilustra um arquivo LocationServer.xml de exemplo configurado para vários servidores em diferentes locais.  

 **Arquivo LocationServer.xml de exemplo para diferentes locais**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ, Seattle, USA  
        </friendlyname>  
        <Server1>\\STLDS01\Deployment$</Server1>  
        <Server2>\\STLDS02\Deployment$</Server2>  
        <Server3>\\STLDS03\Deployment$</Server3>  
        <Server weight=”1”>\\STLDS01\Deployment$</Server>  
        <Server weight=”2”>\\STLDS02\Deployment$</Server>  
        <Server weight=”4”>\\STLDS03\Deployment$</Server>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso NYC, New York, USA  
        </friendlyname>  
        <UNCPath>\\NYCDS01\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

 Especifique a métrica de ponderação usando a marca <server weight\>, que o MDT usa no processo de seleção do servidor. A probabilidade de um servidor ser selecionado é calculada da seguinte forma:  

 **Peso do servidor/soma do peso de todos os servidores**  

 No exemplo anterior, os três servidores no Contoso HQ são listados como 1, 2 e 4. A probabilidade de um servidor com um peso 2 ser selecionado se torna 2 em 7. Portanto, para usar o sistema de ponderação, determine a capacidade dos servidores disponíveis em um local e de pondere cada servidor segundo a capacidade dele em relação a cada um dos demais.  

### <a name="adding-the-locationserverxml-file-to-the-extra-files-directory"></a>Adicionando o arquivo LocationServer.xml ao diretório de arquivos extras  
 Depois de criar o arquivo LocationServer.xml, adicione-o às imagens de inicialização LiteTouch_x86 e LiteTouch_x64 no Windows PE na pasta ***X:\\Deploy\Control***. Usando o Deployment Workbench, adicione outros arquivos e pastas a essas imagens do Windows PE especificando um diretório extra a ser adicionado nas propriedades de compartilhamento de implantação.  

 **Para adicionar o LocationServer.xml ao compartilhamento de implantação**  

1.  Crie uma pasta chamada *Extra Files* na pasta de compartilhamento de implantação raiz (por exemplo, D:\Production Deployment Share\Extra Files).  

2.  Crie uma estrutura de pastas na pasta Extra Files que reflete o local do Windows PE em que o arquivo adicional deve residir.  

     Por exemplo, o arquivo LocationServer.xml precisa residir na pasta \Deploy\Control no Windows PE, portanto, crie a mesma estrutura de pastas em Extra Files (por exemplo, D:\Production Deployment Share\Extra Files\Deploy\Control).  

3.  Copie LocationServer.xml para a pasta *compartilhamento_de_implantação*\Extra Files\Deploy\Control (em que *compartilhamento_de_implantação* refere-se ao caminho totalmente qualificado para a pasta raiz do compartilhamento de implantação).  

4.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

5.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação* (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

6.  No painel Ações, clique em **Propriedades**.  

7.  Na caixa de diálogo ***Propriedades do compartilhamento_de_implantação*** (em que compartilhamento_de_implantação é o nome do compartilhamento de implantação), execute estas etapas:  

    1.  Clique na guia **Configurações da plataforma do Windows PE** (em que *plataforma* é a arquitetura da imagem do Windows PE a ser configurada).  

    2.  Na seção **Personalizações do Windows PE**, na caixa **Diretório extra a ser adicionado**, digite ***caminho*** (em que *caminho* é caminho totalmente qualificado para a pasta Extra Files – por exemplo, D:\Production Deployment Share\Extra Files) e clique em **OK**.  

###  <a name="UpdateBootstrap"></a> Atualizando o arquivo BootStrap.ini  
 Ao criar um compartilhamento de implantação usando o Deployment Workbench, uma propriedade **DeployRoot** é automaticamente criada e populada no arquivo BootStrap.ini. Como o arquivo LocationServer.xml é usado para popular a propriedade **DeployRoot**, é necessário remover esse valor do arquivo BootStrap.ini.  

 **Para remover a propriedade DeployRoot de BootStrap.ini**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação* (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel Ações, clique em **Propriedades**.  

4.  Na caixa de diálogo ***Propriedades do compartilhamento_de_implantação*** (em que *compartilhamento_de_implantação* é o nome do compartilhamento de implantação), clique na guia **Regras** e, em seguida, em **Editar BootStrap.ini**.  

5.  Remova o valor **DeployRoot** (por exemplo, **DeployRoot=\\\Server\Deployment$**).  

6.  Clique em **Arquivo** e, em seguida, em **Salvar** para salvar as alterações no arquivo BootStrap.ini.  

7.  Clique em **OK** para enviar as alterações.  

###  <a name="UpdateDeploymentShare"></a> Atualizando o compartilhamento de implantação  
 O compartilhamento de implantação precisa ser atualizado em seguida para gerar um novo ambiente de inicialização do LiteTouch_x86 e LiteTouch_x64 que contém o arquivo LocationServer.xml e o arquivo BootStrap.ini atualizado.  

 **Para atualizar o compartilhamento de implantação**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação* (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel Ações, clique em **Atualizar Compartilhamento de Implantação**.  

     O Assistente de Atualização de Compartilhamento de Implantação é iniciado.  

4.  Na página **Opções**, selecione as opções desejadas para atualizar o compartilhamento de implantação e clique em **Avançar**.  

5.  Na página **Resumo**, verifique se os detalhes estão corretos e clique em **Avançar**.  

6.  Na página **Confirmação**, clique em **Concluir**.  

> [!NOTE]
>  Quando o processo de atualização estiver concluído, adicione os novos ambientes LiteTouch_x86 e LiteTouch_x64 do Windows PE de volta para os Serviços de Implantação do Windows ou grave-os em uma mídia de inicialização a ser usada durante a implantação.  

## <a name="replacing-an-existing-computer-with-a-new-computer-using-lite-touch-installation"></a>Substituindo um computador existente por um novo computador usando Lite Touch Installation  
 Você pode usar o MDT para implantar uma imagem para um novo computador que substituirá um computador existente na arquitetura da empresa. Essa situação poderá ocorrer ao fazer upgrade de um sistema operacional para outro (um novo sistema operacional poderia exigir novo hardware) ou se a organização precisar de computadores mais rápidos e modernos para os aplicativos existentes.  

 Ao substituir um computador existente por um novo computador, a Microsoft recomenda considerar todas as configurações que serão migradas de um computador para outro, como contas de usuário e dados de estado de usuário. Além disso, é importante criar uma solução de recuperação em caso de falha de migração.  

 Nessa implantação de exemplo, substitua o computador existente (WDG-EXIST-01) por um novo computador (WDG-NEW-02) no domínio CORP capturando dados de estado do usuário do WDG-EXIST-01 e salvando-os em um compartilhamento de rede. Em seguida, implante uma imagem existente no WDG-NEW-02 e restaure os dados de estado do usuário capturados para WDG-NEW-02. A implantação será executada de um servidor de implantação (WDG-MDT-01).  

 No MDT, use o modelo da Sequência de tarefas padrão de substituição de cliente para criar uma sequência de tarefas que executará todas as tarefas de implantação necessárias.  

 Esta demonstração pressupõe que:  

-   O MDT foi instalado no servidor de implantação (WDG MDT 01)  

-   O compartilhamento de implantação já foi criado e populado, incluindo imagens do sistema operacional, aplicativos e drivers de dispositivo  

-   Uma imagem de um computador de referência já foi capturada e será implantada no novo computador (WDG NEW 02)  

-   Uma pasta de rede compartilhada (UserStateCapture$) foi criada e compartilhada no servidor de implantação (WDG MDT 01) com as permissões de compartilhamento apropriadas  

 Um compartilhamento de implantação deve existir antes do início deste exemplo. Para obter mais informações sobre a criação de um compartilhamento de implantação, consulte a seção “Gerenciando compartilhamentos de implantação no Deployment Workbench”, no documento do MDT *Usando o Microsoft Deployment Toolkit*.  

### <a name="step-1-create-a-task-sequence-to-capture-the-user-state"></a>Etapa 1: criar uma sequência de tarefas para capturar o estado do usuário  
 Crie sequências de tarefas do MDT no nó Sequências de Tarefas no Deployment Workbench usando o Assistente de Nova Sequência de Tarefas. Para executar a primeira parte do cenário de implantação Substituir Computador (capturar o estado do usuário no computador existente), selecione o modelo da Sequência de tarefas padrão de substituição de cliente no Assistente de Nova Sequência de Tarefas.  

 **Para criar uma sequência de tarefas para capturar o estado do usuário no cenário de implantação Substituir Computador**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/ *compartilhamento_de_implantação*/Task Sequences (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel Ações, clique em **Nova sequência de tarefas**.  

     O Assistente de Nova Sequência de Tarefas é iniciado.  

4.  Conclua o Assistente de Nova Sequência de Tarefas usando as informações a seguir. Aceite os valores padrões, a menos que especificado de outra forma.  

    |**Nesta página do assistente** |**Faça o seguinte** |  
    |-|-|  
    |**Configurações Gerais** |1.  Em **ID da sequência de tarefas**, digite **VISTA_EXIST**.<br />2.  Em **Nome da sequência de tarefas**, digite **Executar cenário Substituir Computador em um computador existente**.<br />3.  Clique em **Avançar**.|  
    |**Selecionar Modelo** |Em **Os seguintes modelos de sequência de tarefas estão disponíveis**. **Selecione aquele que você deseja usar como ponto de partida**, escolha **Sequência de tarefas padrão de substituição de cliente** e, em seguida, clique em **Avançar**.|  
    |**Resumo** |Verifique se os detalhes de configuração estão corretos e clique em **Avançar**.|  
    |**Confirmação** |Clique em **Finalizar**.|  

 O Assistente de Nova Sequência de Tarefas é concluído e a sequência de tarefas **VISTA_EXIST** é adicionada à lista de sequências de tarefas.  

### <a name="step-2-create-a-task-sequence-to-deploy-operating-system-and-restore-the-user-state"></a>Etapa 2: criar uma sequência de tarefas para implantar o sistema operacional e restaurar o estado do usuário  
 Crie sequências de tarefas do MDT no nó Sequências de Tarefas no Deployment Workbench usando o Assistente de Nova Sequência de Tarefas. Para executar a segunda parte do cenário de implantação Substituir Computador (implantar o sistema operacional e, em seguida, restaurar o estado do usuário no computador existente), selecione o modelo da Sequência de tarefas padrão de substituição de cliente no Assistente de Nova Sequência de Tarefas.  

 **Para criar uma sequência de tarefas para implantar o estado do usuário no cenário de implantação Substituir Computador**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação*/Task Sequences (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel Ações, clique em **Nova sequência de tarefas**.  

     O Assistente de Nova Sequência de Tarefas é iniciado.  

4.  Conclua o Assistente de Nova Sequência de Tarefas usando as informações a seguir. Aceite os valores padrões, a menos que especificado de outra forma.  

    |**Nesta página do assistente**|**Faça o seguinte**|  
    |-|-|  
    |**Configurações Gerais**|1.  Em **ID da sequência de tarefas**, digite **VISTA_NEW**.<br />2.  Em **Nome da sequência de tarefas**, digite **Executar cenário Substituir Computador em um novo computador**.<br />3.  Clique em **Avançar**.|  
    |**Selecionar Modelo**|Em **Os seguintes modelos de sequência de tarefas estão disponíveis**. **Selecione aquele que você deseja usar como ponto de partida**, escolha **Sequência de tarefas padrão de cliente** e, em seguida, clique em **Avançar**.|  
    |**Selecionar o sistema operacional**|Em **As imagens de sistema operacional a seguir estão disponíveis para serem implantadas com esta sequência de tarefas**. Selecione uma opção para usar, escolha ***imagem_capturada_do_vista*** (em que *imagem_capturada_do_vista* é a imagem capturada do computador de referência adicionado ao nó Sistemas Operacionais no Deployment Workbench) e, em seguida, clique em *Avançar*.|  
    |**Especificar chave do produto (Product Key)**|Selecione **Não especificar uma chave do produto (Product Key) no momento** e, em seguida, clique em **Avançar**.|  
    |Configurações do sistema operacional|1.  Em **Nome Completo**, digite **Funcionário da Woodgrove**.<br />2.  Em **Organização**, digite **Woodgrove Bank**.<br />3.  Em **Página inicial do Internet Explorer**, digite **http://www.woodgrovebank.com**.<br />4.  Clique em **Avançar**.|  
    |**Senha do Administrador**|Em **Senha do Administrador** e **Confirme a Senha do Administrador**, digite **P@ssw0rd** e clique em **Concluir**.|  
    |**Confirmação**|Clique em **Finalizar**.|  

 O Assistente de Nova Sequência de Tarefas é concluído e a sequência de tarefas **VISTA_NEW** é adicionada à lista de sequências de tarefas.  

### <a name="step-3-customize-the-mdt-configuration-files"></a>Etapa 3: personalizar os arquivos de configuração do MDT  
 Quando a sequência de tarefas do MDT tiver sido criada, personalize os arquivos de configuração do MDT que fornecem os parâmetros de configuração para capturar as informações de estado do usuário. Especificamente, personalize o arquivo CustomSettings.ini, modificando-o nas propriedades do compartilhamento de implantação criado anteriormente no processo de implantação. Em uma etapa posterior, o compartilhamento de implantação será atualizado para garantir que o arquivo de configuração dele também esteja atualizado.  

 **Para personalizar os arquivos de configuração do MDT para capturar informações de estado do usuário**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação* (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel Ações, clique em **Propriedades**.  

     A caixa de diálogo **Propriedades** é exibida.  

4.  Na caixa de diálogo **Propriedades**, clique na guia **Variáveis**.  

5.  Na guia **Regras**, modifique o arquivo CustomSettings.ini para refletir as alterações necessárias, conforme mostrado no exemplo a seguir. Faça modificações adicionais conforme necessário para o ambiente.  

     **Arquivo CustomSettings.ini personalizado**  

    ```  
    [Settings]  
    Priority=Default  
    Properties=MyCustomProperty  

    [Default]  
    OSInstall=Y  

    UDShare=\\WDG-MDT-01\UserStateCapture$  
    UDDir=%OSDCOMPUTERNAME%  
    UserDataLocation=NETWORK  
    SkipCapture=NO  
    SkipAdminPassword=YES  
    SkipProductKey=YES  

    ```  

6.  Na caixa de diálogo **Propriedades**, clique em **OK**.  

7.  Feche todas as janelas abertas e caixas de diálogo.  

### <a name="step-4-configure-the-windows-pe-options-for-the-deployment-share"></a>Etapa 4: configurar as opções do Windows PE para o compartilhamento de implantação  
 Configure as opções do Windows PE para o compartilhamento de implantação no nó de Compartilhamentos da Implantação no Deployment Workbench.  

> [!NOTE]
>  Se os drivers de dispositivo para o computador existente (WDG-EXIST-01) e o novo computador (WDG-NEW-01) estão incluídos no Windows Vista, ignore esta etapa e prossiga para a etapa seguinte.  

 **Para configurar as opções do Windows PE para o compartilhamento de implantação**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação* (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel Ações, clique em **Propriedades**.  

     A caixa de diálogo **Propriedades** é exibida.  

4.  Na caixa de diálogo **Propriedades**, na guia **Componentes da *plataforma* do Windows PE** (em que *plataforma* é a arquitetura da imagem do Windows PE a ser configurada), em **Perfil de seleção**, selecione ***drivers_de_dispositivo*** (em que *drivers_de_dispositivo* refere-se ao nome do perfil de seleção do driver de dispositivo) e, em seguida, clique em **OK**.  

### <a name="step-5-update-the-deployment-share"></a>Etapa 5: atualizar o compartilhamento de implantação  
 Depois de configurar as opções do Windows PE para o compartilhamento de implantação, atualize o compartilhamento de implantação. A atualização do compartilhamento de implantação atualiza todos os arquivos de configuração do MDT e gera uma versão personalizada do Windows PE. A versão personalizada do Windows PE é usada para iniciar o computador de referência e o processo de implantação LTI.  

 **Para atualizar o compartilhamento de implantação no Deployment Workbench**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação* (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel Ações, clique em **Atualizar DeploymentShare**.  

     O Assistente de Atualização de Compartilhamento de Implantação é iniciado.  

4.  Na página **Opções**, selecione as opções desejadas para atualizar o compartilhamento de implantação e clique em **Avançar**.  

5.  Na página **Resumo**, verifique se os detalhes estão corretos e clique em **Avançar**.  

6.  Na página **Confirmação**, clique em **Concluir**.  

 O Deployment Workbench inicia a atualização do compartilhamento de implantação. O Deployment Workbench cria os arquivos de LiteTouchPE_x86.iso e LiteTouchPE_x86.wim (para computadores de destino de 32 bits) ou LiteTouchPE_x64.iso e LiteTouchPE_x64.wim (para computadores de destino de 64 bits) na pasta *compartilhamento_de_implantação*\Boot (em que *compartilhamento_de_implantação* é a pasta compartilhada usada como o compartilhamento de implantação).  

### <a name="step-6-create-the-lti-bootable-media"></a>Etapa 6: criar uma mídia inicializável LTI  
 Forneça um método para iniciar o computador com a versão personalizada do Windows PE criada quando o compartilhamento de implantação foi atualizado. O Deployment Workbench cria os arquivos de LiteTouchPE_x86.iso e LiteTouchPE_x86.wim (para computadores de destino de 32 bits) ou LiteTouchPE_x64.iso e LiteTouchPE_x64.wim (para computadores de destino de 64 bits) na pasta *compartilhamento_de_implantação*\Boot (em que *compartilhamento_de_implantação* é a pasta compartilhada usada como o compartilhamento de implantação). Crie mídia inicializável do LTI apropriada de uma dessas imagens.  

 **Para criar a mídia inicializável LTI**  

1.  No Windows Explorer, navegue para a pasta *compartilhamento_de_implantação*\Boot (em que *compartilhamento_de_implantação* refere-se à pasta compartilhada usada como o compartilhamento de implantação).  

2.  Baseado no tipo de computador usado para o computador existente (WDG-EXIST-01) e o novo computador (WDG-NEW-02), execute uma das seguintes tarefas:  

    -   Se o computador de referência for um computador físico, crie um CD ou DVD do arquivo ISO.  

    -   Se o computador de referência for uma VM, inicie-a diretamente do arquivo ISO ou de um CD ou DVD do arquivo ISO.  

### <a name="step-7-start-the-existing-computer-with-the-lti-bootable-media"></a>Etapa 7: iniciar o computador existente com a mídia inicializável LTI  
 Inicie o computador existente (WDG-EXIST-01) com a mídia inicializável LTI criada anteriormente no processo. Este CD inicializa o Windows PE no computador existente e começa o processo de implantação do MDT. No final do processo de implantação do MDT, as informações de migração de estado do usuário são armazenadas na pasta compartilhada UserStateCapture$.  

> [!NOTE]
>  Você também pode iniciar o processo do MDT inicializando o computador de destino dos Serviços de Implantação do Windows. Para obter mais informações, consulte a seção “Preparar os Serviços de Implantação do Windows” no documento do MDT *Usando o Microsoft Deployment Toolkit*.  

 **Para iniciar o computador existente com a mídia inicializável LTI**  

1.  Inicie o WDG-EXIST-01 com a mídia inicializável LTI criada anteriormente no processo.  

     O Windows PE é iniciado e, em seguida, o Assistente de Implantação do Windows.  

2.  Conclua o Assistente de Implantação do Windows usando as informações a seguir. Aceite os valores padrões, a menos que especificado de outra forma.  

    |**Nesta página do assistente**|**Faça o seguinte**|  
    |-|-|  
    |**Bem-vindo à Implantação**|Clique em **Executar o Assistente de Implantação para instalar um novo sistema operacional** e, em seguida, em **Avançar**.|  
    |**Especifique as credenciais para conectar-se aos compartilhamentos de rede.**|1.  Em **Nome de Usuário**, digite **Administrador**.<br />2.  Em **Senha**, digite **P@ssw0rd**.<br />3.  Em **Domínio**, digite **CORP**.<br />4.  Clique em **OK**.|  
    |**Selecione uma sequência de tarefas para executar neste computador.**|Clique em *Executar cenário de substituição de computador em um computador existente* e, em seguida, em **Avançar**.|  
    |**Especificar onde salvar seus dados e configurações**|Clique em **Avançar**.|  
    |**Especificar o local para salvar um backup completo do computador**|Clique em **Não fazer backup do computador existente** e, em seguida, clique em **Avançar**.|  
    |**Pronto para iniciar**|Clique em **Começar**.|  

     Caso ocorram erros ou avisos, consulte o documento do MDT *Referência de solução de problemas*.  

3.  Na caixa de diálogo **Resumo da Implantação**, clique em **Detalhes**.  

     Se ocorrerem erros ou avisos, examine-os e registre as informações de diagnóstico.  

4.  Na caixa de diálogo **Resumo da Implantação**, clique em **Concluir**.  

 As informações de migração de estado do usuário são capturadas e são armazenadas na pasta de rede compartilhada (UserStateCapture$) criada anteriormente no processo.  

### <a name="step-8-start-the-new-computer-with-the-lti-bootable-media"></a>Etapa 8: iniciar o novo computador com a mídia inicializável LTI  
 Inicie o novo computador (WDG-NEW-02) com a mídia inicializável LTI criada anteriormente no processo. Este CD inicia o Windows PE no computador de referência e inicializa o processo de implantação do MDT. No final do processo de implantação do MDT, o Windows Vista é implantado no novo computador e as informações de migração de estado do usuário são restauradas para o novo computador.  

> [!NOTE]
>  Você também pode iniciar o processo do MDT inicializando o computador de destino dos Serviços de Implantação do Windows. Para obter mais informações, consulte a seção “Preparar os Serviços de Implantação do Windows” no documento do MDT *Usando o Microsoft Deployment Toolkit*.  

 **Para iniciar o novo computador com a mídia inicializável LTI**  

1.  Inicie o WDG-NEW-02 com a mídia inicializável LTI criada anteriormente no processo.  

     O Windows PE é iniciado e, em seguida, o Assistente de Implantação do Windows.  

2.  Conclua o Assistente de Implantação do Windows usando as informações a seguir. Aceite os valores padrões, a menos que especificado de outra forma.  

    |**Nesta página do assistente**|**Faça o seguinte**|  
    |--|--|
    |**Bem-vindo à Implantação**|Clique em **Executar o Assistente de Implantação para instalar um novo sistema operacional** e, em seguida, em **Avançar**.|  
    |**Especifique as credenciais para conectar-se aos compartilhamentos de rede.**|1.  Em **Nome de Usuário**, digite **Administrador**.<br />2.  Em **Senha**, digite **P@ssw0rd**.<br />3.  Em **Domínio**, digite **CORP**.<br />4.  Clique em **OK**.|  
    |**Selecione uma sequência de tarefas para executar neste computador.**|Clique em **Executar cenário de substituição de computador em um novo computador** e, em seguida, em **Avançar**.|  
    |**Configurar o nome do computador**|Em **Nome do computador**, digite **WDG-NEW-02** e, em seguida, clique em **Avançar**.|  
    |**Ingressar o computador em um domínio ou grupo de trabalho**|Clique em **Avançar**.|  
    |**Especifique se os dados do usuário devem ser restaurados**|1.  Clique em **Especificar um local**.<br />2.  Em **Local**, digite **\\\WDG-MDT-01\UserStateCapture$\WDG-EXIST-01**.<br />3.  Clique em **Avançar**.|  
    |**Seleção de Localidade**|Clique em **Avançar**.|  
    |**Definir o fuso horário**|Clique em **Avançar**.|  
    |**Especificar se uma imagem deve ser capturada**|Clique em **Não capturar a imagem deste computador** e, em seguida, em **Avançar**.|  
    |**Especificar a configuração do BitLocker**|Clique em **Não habilitar o BitLocker para este computador** e, em seguida, em **Avançar**.|  
    |**Pronto para iniciar**|Clique em **Começar**.|  

     Caso ocorram erros ou avisos, consulte o documento do MDT *Referência de solução de problemas*.  

3.  Na caixa de diálogo **Resumo da Implantação**, clique em **Detalhes**.  

     Se ocorrerem erros ou avisos, examine-os e registre as informações de diagnóstico.  

4.  Na caixa de diálogo **Resumo da Implantação**, clique em **Concluir**.  

 O Windows Vista agora está instalado no novo computador e as informações de migração de estado do usuário capturadas também foram restauradas.  

## <a name="integrating-custom-deployment-code-into-mdt"></a>Integrando o código de implantação personalizado no MDT  
 É comum para uma equipe de implantação ter requisitos complexos e específicos para seu ambiente de destino que não são atendidos pelas ações de sequência de tarefas predefinidas do Deployment Workbench ou pelos arquivos de configuração padrão do MDT. Nesse caso, implemente código personalizado para atender às necessidades.  

 Integre o código de implantação personalizado ao MDT da seguinte forma:  

-   Escolhendo uma linguagem de script, conforme descrito em [Escolhendo a linguagem de script apropriada](#ChooseAppropLanguage)  

-   Aproveitando o ZTIUtility.vbs, conforme descrito em [Entendendo como aproveitar o ZTIUtility](#UnderstandLeverageZTI)  

-   Integrando o código de implantação personalizado, conforme descrito em [Integrar o código de implantação personalizado](#IntegrateCustomDeploy)  

 A seção a seguir pressupõe que o MDT está configurado em um servidor de implantação.  

###  <a name="ChooseAppropLanguage"></a> Escolhendo a linguagem de script apropriada  
 Embora qualquer código que pode ser executado no Windows ou no Windows PE possa ser chamado como uma instalação de aplicativo ou por meio de uma etapa da sequência de tarefas do MDT, a Microsoft recomenda usar scripts como arquivos .vbs ou .wsf.  

 A vantagem de usar arquivos .wsf é contar com registro em log interno, além de outras funções predefinidas já utilizadas pelos processos de ZTI e LTI. Essas funções estão disponíveis no script ZTIUtility distribuído com o MDT.  

 Quando referenciado de um script personalizado, o script ZTIUtility inicializa o ambiente e as classes de instalação do MDT. Essas classes estão disponíveis:  

-   **Logging**. Esta classe oferece a funcionalidade de registro em log usada por todos os scripts do MDT. Ela também cria um único arquivo de log para cada script executado durante a implantação e um arquivo de log consolidado de todos os scripts. Esses arquivos de log são criados em um formato projetado para ser lido pelo TRACE32; essa ferramenta está disponível no [System Center Configuration Manager 2007 Toolkit V2](https://www.microsoft.com/download/en/details.aspx?id=9257).  

-   **Environment**. Esta classe configura as variáveis de ambiente coletadas por meio do WMI e do processamento de regras do MDT, permitindo que elas sejam referenciadas diretamente do script. Isso permite que as propriedades de implantação sejam lidas, concedendo acesso a todas as informações de configuração usadas pelos processos do ZTI e LTI.  

-   **Utility**. Esta classe fornece utilitários gerais que são usados em scripts ZTI e LTI. A Microsoft recomenda que, sempre ao desenvolver código personalizado, essa classe deve ser examinada para ver se algum código pode ser simplesmente reutilizado. Informações adicionais sobre algumas das funcionalidades fornecidas nesta classe estão incluídas posteriormente nesta seção.  

-   **Database**. Esta classe executa funções como conectar aos bancos de dados e ler informações deles. Em geral, não é recomendado acessar a classe de banco de dados diretamente. Em vez disso, use o processamento de regra para executar pesquisas de banco de dados.  

-   **Strings**. Esta classe executa rotinas de processamento de cadeia de caracteres comuns, como a criação de uma lista de itens delimitada, exibindo um valor hexadecimal, cortando o espaço em branco de uma cadeia de caracteres, alinhando uma cadeia de caracteres à direita ou à esquerda, forçando um valor para o formato da cadeia de caracteres ou da matriz, gerando um GUID (identificador global exclusivo) aleatório e conversões de Base64.  

-   **FileHandling**. Esta classe executa funções como normalizar os caminhos e copiar, mover e excluir arquivos e pastas.  

-   **clsRegEx**. Esta classe executa funções de expressão regular.  

 No MDT, algumas alterações foram implementadas na arquitetura de script para tornar o cliente VBScript (Microsoft Visual Basic® Scripting Edition) mais robusto e confiável. Essas alterações incluem:  

-   Alterações significativas no ZTIUtility.vbs (a biblioteca de script principal), incluindo novas APIs e melhor tratamento de erro  

-   Uma nova aparência para a estrutura geral dos scripts ZTI_*xxx*.wsf  

 A estrutura geral de scripts do MDT também foi alterada. A maioria dos scripts do MDT agora são encapsulados em objetos **Class** do VBScript. A classe é inicializada e chamada com a função **RunNewInstance**.  

> [!NOTE]
>  A maioria dos scripts do MDT 2008 Atualização 1 funcionará no estado em que se encontra no MDT, mesmo com as alterações extensivas do ZTIUtility.vbs, visto que a maioria dos scripts do MDT inclui o ZTIUtility.vbs.  

###  <a name="UnderstandLeverageZTI"></a> Entendendo como aproveitar o ZTIUtility  
 O arquivo ZTIUtility.vbs contém classes de objeto que podem ser aproveitadas no seu código personalizado. Integre o código personalizado ao MDT usando a:  

-   Classe de registro em log definida no ZTIUtility.vbs, conforme descrito em [Usar a classe de registro em log ZTIUtility](#UseZTILogging)  

-   Classe de ambiente definida no ZTIUtility.vbs, conforme descrito em [Usar a classe de ambiente ZTIUtility](#UseZTIEnvironment)  

-   Classe de utilitário definida no ZTIUtility.vbs, conforme descrito em [Usar a classe de utilitário ZTIUtility](#UseZTIUtility)  

####  <a name="UseZTILogging"></a> Usar a classe de log ZTIUtility  
 A classe de registro em log ZTIUtiliy.vbs fornece um mecanismo simples para o código personalizado registrar em log as informações de status, avisos e erros da mesma maneira que outros scripts durante a implantação ZTI ou LTI. A padronização também garante que a caixa de diálogo **Resumo da Implantação LTI** informe corretamente o status de qualquer código personalizado que é executado.  

 Veja a seguir um exemplo de script de código personalizado que usa as funções **oLogging.CreateEntry** e **TestAndFail** para registra diferentes tipos de mensagens em log, dependendo dos resultados das diversas ações de script.  

 **Script de exemplo que utiliza registro em log do ZTIUtility: ZTI_Example.wsf**  

```  
<job id="ZTI_Example">  
<script language="VBScript" src="ZTIUtility.vbs"/>  
<script language="VBScript">  

' //*******************************************************  
' //  
' // Copyright (c) Microsoft Corporation.  All rights reserved  
' // Microsoft Deployment Toolkit Solution Accelerator  
' // File: ZTI_Example.wsf  
' //  
' // Purpose: Example of scripting with the  
' //          Microsoft Deployment Toolkit.  
' //  
' // Usage: cscript ZTI_Example.wsf [/debug:true]  
' //  
' //*******************************************************  

Option Explicit  
RunNewInstance  

'//--------------------------------------------------------  
'// Main Class  
'//--------------------------------------------------------  
Class ZTI_Example  

'//--------------------------------------------------------  
'// Main routine  
'//--------------------------------------------------------  

Function Main()  

  Dim iRetVal  
  Dim sScriptPath  

  iRetVal = SUCCESS  

  oLogging.CreateEntry "Begin example script…", _  
    LogTypeInfo  

  ' %ServerA% is a generic variable available within  
  ' every CustomSettings.ini file.  

  sScriptPath = "\\" & oEnvironment.Item("ServerA") & _  
    "\public\products\Applications\User\Technet\USEnglish"  

  ' Validate a connection to server, net connect with  
  ' credentials if necessary.  
  iRetVal = oUtility.ValidateConnection( sScriptPath )  
  TestAndFail iRetVal, 9991, "Validate Connection to [" & _  
    sScriptPath & "]"  

  'Run Setup Program  

  iRetVal = oUtility.RunWithHeartbeat( """" & _  
    sScriptPath & "\setup.exe"" /?" )  
  TestAndFail iRetVal, 9991, "RunWithHeartbeat [" & _  
    sScriptPath & "]"  

  'Perform any cleanup from installation process  

  oShell.RegWrite "HKLM\Software\Microsoft\SomeValue", _  
    "Done with Execution of XXX.", "REG_SZ"  

  Main = iRetVal  

End Function  

End Class  

</script>  
</job>  
```  

> [!NOTE]
>  Você poderá continuar usando scripts que chamam **ZTIProcess()** com **ProcessResults()**, se quiser. No entanto, certos recursos avançados de tratamento de erros não serão habilitados.  

####  <a name="UseZTIEnvironment"></a> Usar a classe de ambiente ZTIUtility  
 A classe de ambiente no ZTIUtiliy.vbs fornece acesso às propriedades do MTD, bem como a capacidade de atualizá-las. No exemplo anterior, **oEnvironment.Item("Memory")** é usado para recuperar a quantidade de RAM disponível, e também pode ser usado para recuperar o valor de qualquer uma das propriedades descritas no documento do MDT *Referência do Toolkit*.  

####  <a name="UseZTIUtility"></a> Usar a classe de utilitário ZTIUtility  
 O script ZTIUtility.vbs contém diversos utilitários frequentemente usados que qualquer script de implantação personalizada pode usar. Você pode adicionar esses utilitários a qualquer script da mesma forma que as classes **oLogging** e **oEnvironment**.  

A tabela a seguir detalha algumas funções úteis disponíveis, bem como sua saída. Para obter uma lista completa das funções disponíveis, consulte o arquivo ZTIUtility.vbs.  

|**Função**|**Saída**|  
|-|-|
|**oUtility.LocalRootPath**|Retorna o caminho da pasta raiz que está sendo usada pelo processo de implantação no computador de destino – por exemplo, C:\MININT|  
|**oUtility.BootDevice**|Retorna o dispositivo de inicialização do sistema – por exemplo, MULTI(0)DISK(0)RDISK(0)PARTITION(1)|  
|**oUtility.LogPath**|Retorna o caminho para a pasta de logs que está sendo usada durante a implantação – por exemplo, C:\MININT\SMSOSD\OSDLOGS|  
|**oUtility.StatePath**|Retorna o caminho do repositório de estado configurado no momento – por exemplo, C:\MININT\StateStore|  
|**oUtility.ScriptName**|Retorna o nome do script que chama a função – por exemplo, Z-RAMTest|  
|**oUtility.ScriptDir**|Retorna o caminho para o script que está chamando a função – por exemplo, \\\nome_do_servidor\Deployment$\Scripts|  
|**oUtility.ComputerName**|Determina o nome do computador que será usado durante o processo de build como, por exemplo, nome_do_computador|  
|**oUtility.ReadIni(file, section, item)**|Permite que o item especificado seja lido de um arquivo .ini|  
|**oUtility.WriteIni(file, section, item, value)**|Permite que o item especificado seja gravado em um arquivo .ini|  
|**oUtility.Sections(file)**|Lê as seções de um arquivo .ini e os armazena em um objeto de referência|  
|**oUtility.SectionContents(file, section)**|Lê o conteúdo do arquivo .ini especificado e os armazena em um objeto|  
|**oUtility.RunWithHeartbeat(sCmd)**|Quando o comando é executado, grava as informações de pulsação nos logs a cada 0,5 segundo|  
|**oUtility.FindFile**<br /><br /> **(sFilename,sFoundPath)**|Procura o arquivo especificado na pasta DeployRoot e subpastas padrão, incluindo Servicing, Tools, USMT, Templates, Scripts e Control|  
|**oUtility.findMappedDrive(sServerUNC)**|Verifica se uma unidade está mapeada para o caminho UNC especificado e retorna a letra da unidade|  
|**oUtility.ValidateConnection(sServerUNC)**|Verifica se há uma conexão com o servidor especificado e, caso não haja, tenta criá-la|  
|**MapNetworkDrive**<br /><br /> **(sShare, SDomID, sDomPwd)**|Mapeia uma letra da unidade para o caminho UNC especificado como o compartilhamento e retorna a letra da unidade usada, retornando um erro caso não seja bem-sucedido|  
|**VerifyPathExists(strPath)**|Verifica se o caminho especificado existe|  
|**oEnvironment.Substitute(sVal)**|Dada uma cadeia de caracteres, expande quaisquer variáveis ou funções da cadeia de caracteres em questão|  
|**oEnvironment.Item**<br /><br /> **(sName)**|Lê ou grava uma variável em um repositório persistente|  
|**oEnvironment.Exists**<br /><br /> **(sName)**|Realiza testes para verificar se a variável existe|  
|**oEnvironment.ListItem**<br /><br /> **(sName)**|Lê ou grava uma variável do tipo **matriz** em um repositório persistente|  
|**oLogging.ReportFailure**<br /><br /> **(sMessage, iError)**|Usada para executar uma saída estruturada se for detectado um erro irrecuperável|  
|**oLogging.CreateEvent**<br /><br /> **(iEventID, iType, sMessage, arrParms)**|Grava uma mensagem no arquivo de log e publica o evento em um servidor definido|  
|**oLogging.CreateEntry**<br /><br /> **(sLogMsg, iType)**|Grava uma mensagem no arquivo de log|  
|**TestAndFail(iRc, iError, sMessage)**|Sairá do script **iError** se **iRc** for falso ou falhar|  
|**TestAndLog(iRc , sMessage)**|Registrará um aviso somente se **iRc** for falso ou falhar|  

###  <a name="IntegrateCustomDeploy"></a> Integrando o código de implantação personalizado  
 O código de implantação personalizado pode ser integrado ao processo de MDT de várias maneiras, no entanto, independentemente do método usado, as duas regras a seguir devem ser atendidas:  

-   O nome do script de código de implantação personalizado sempre deve começar com a letra Z.  

-   O código de implantação personalizado deve ser colocado na pasta Scripts no compartilhamento de implantação – por exemplo, D:\Production Deployment Share\Scripts.  

 Os métodos usados com mais frequência para integrar o código personalizado que também garantem registro em log consistente são:  

-   Implantar o código como um aplicativo do MDT  

-   Iniciar o código como um comando da sequência de tarefas do MDT  

-   Iniciar o código como um script de saída do usuário  

#### <a name="deploy-custom-code-as-an-mdt-application"></a>Implantar código personalizado como um aplicativo do MDT  
 O código de implantação personalizado pode ser importado para o Deployment Workbench e gerenciado da mesma maneira que qualquer outro aplicativo.  

 **Para criar um novo aplicativo para executar código de implantação personalizada**  

1.  Copie o código de implantação personalizado para a pasta *compartilhamento_de_implantação*\Scripts (em que *compartilhamento_de_implantação* é o caminho totalmente qualificado para o compartilhamento de implantação).  

2.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

3.  Na árvore de console do Deployment Workbench, acesse Deployment Shares/*compartilhamento_de_implantação*/Applications (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

4.  No painel Ações, clique em **Novo Aplicativo**.  

     O Assistente de Novo Aplicativo é iniciado.  

5.  Conclua o Assistente de Novo Aplicativo usando as informações a seguir. Aceite os padrões, a menos que especificado de outra forma.  

    |**Nesta página do assistente**|**Faça o seguinte**|  
    |-|-|  
    |**Tipo de Aplicativo**|Clique em **Aplicativos sem arquivos de origem ou em outro lugar na rede** e, em seguida, clique em **Avançar**.|  
    |**Detalhes**|Conclua essa página com base nas informações do aplicativo e, em seguida, clique em **Avançar**.|  
    |**Detalhes do Comando**|1.  Na caixa **Linha de comando**, digite **cscript.exe %SCRIPTROOT%\custom_code** (em que *custom_code* é o nome do código personalizado que foi desenvolvido).<br />2.  Na caixa **Diretório de trabalho**, digite ***diretório_de_trabalho*** (em que “diretório_de_trabalho” é o nome do diretório de trabalho do código personalizado, que geralmente fica na mesma pasta especificada na caixa **Linha de comando**).<br />3.  Clique em **Avançar**.|  
    |**Resumo**|Verifique se os parâmetros de configuração estão corretos e clique em **Avançar**.|  
    |**Confirmação**|Clique em **Finalizar**.|  

 O aplicativo aparece no nó Aplicativos no Deployment Workbench.  

#### <a name="add-the-custom-code-as-a-task-sequence-step"></a>Adicionar o código personalizado como uma etapa de sequência de tarefas  
 O código de implantação personalizado pode ser chamado diretamente de qualquer ponto de uma sequência de tarefas, o que concede acesso às opções e regras usuais de sequência de tarefas.  

 **Para adicionar o código de implantação personalizado a uma sequência de tarefas existente**  

1.  Copie o código de implantação personalizado para a pasta *compartilhamento_de_implantação*\Scripts (em que *compartilhamento_de_implantação* é o caminho totalmente qualificado para o compartilhamento de implantação).  

2.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

3.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação/Task Sequences* (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

4.  No painel de detalhes, clique em ***sequência_de_tarefas*** (em que *sequência_de_tarefas* é o nome da sequência de tarefas que executa o código personalizado).  

5.  No painel Ações, clique em **Propriedades**.  

6.  Na caixa de diálogo ***Propriedades da sequência_de_tarefas***, clique na guia **Sequência de Tarefas**.  

7.  Na árvore de console, acesse *group* (em que *group* é o grupo para adicionar a etapa de sequência de tarefas).  

8.  Clique em **Adicionar**, **Geral** e, em seguida, em **Executar Linha de Comando**.  

9. Na árvore de console, clique em **Executar Linha de Comando** e, em seguida, clique na guia **Propriedades**.  

10. Na caixa **Nome**, digite ***name*** (em que *name* é um nome descritivo do código personalizado).  

11. Na guia **Propriedades** da caixa **Linha de comando**, digite ***linha_de_comando*** (em que *linha_de_comando* refere-se ao comando para executar o código personalizado, por exemplo, **cscript.exe %SCRIPTROOT%\CustomCode.vbs**).  

12. Na caixa **Iniciar em**, digite ***path*** (em que *path* refere-se ao caminho totalmente qualificado da pasta de trabalho do código personalizado que, geralmente, é o mesmo caminho especificado na caixa **Linha de comando**) e, em seguida, clique em **OK**.  

 A etapa de sequência de tarefas recém-criada é exibida na lista de etapas de sequência de tarefas.  

#### <a name="run-custom-code-as-a-user-exit-script"></a>Executar código personalizado como um script de saída do usuário  
 Também é possível executar o código personalizado como um script de saída do usuário do CustomSettings.ini usando a diretiva **UserExit**. Isso fornece um mecanismo para que as informações sejam passadas para o processo de validação de regras CustomSettings.ini e fornece uma atualização dinâmica das propriedades do MDT  

 Para obter mais informações sobre scripts de saída do usuário e a diretiva **UserExit**, consulte a seção “Scripts de saída do usuário no arquivo CustomSettings.ini” no documento do MDT *Usando o Microsoft Deployment Toolkit*.  

## <a name="installing-device-drivers-using-various-installation-methods"></a>Instalando drivers de dispositivo usando vários métodos de instalação  
 Nesse cenário, o MDT é usado para implantar um sistema operacional em diferentes tipos de hardware. Como parte do processo de implantação, identifique e instale os drivers de dispositivo para que cada tipo de hardware funcione corretamente. Há dois tipos principais de drivers de dispositivo; cada um deles precisa ser tratado de maneira diferente durante o processo de implantação:  

-   Drivers de dispositivo que contém um arquivo .inf que pode ser usado para importar o driver de dispositivo para o Deployment Workbench  

-   Drivers de dispositivo que são empacotadas como um aplicativo e que precisam ser instalados como um aplicativo  

 Usando o MDT, você pode manipular os dois tipos de drivers como parte de uma implantação de sistema operacional.  

 Instale os drivers de dispositivo da seguinte forma:  

-   Determinando os métodos para instalar cada driver de dispositivo, conforme descrito em [Determinar qual método usar para instalar um driver de dispositivo](#WhichMethodtoInstallDriver)  

-   Usando o método de drivers não incluídos, conforme descrito em [Instalar drivers de dispositivo usando o método de drivers não incluídos](#InstallOutofBoxDrivers)  

-   Instalando-os como aplicativos, conforme descrito em [Instalando drivers de dispositivo como aplicativos](#InstallDriversasApplications)  

 Este cenário pressupõe que o MDT está em execução em um servidor de implantação.  

###  <a name="WhichMethodtoInstallDriver"></a> Determinando o método a ser usado para instalar um driver de dispositivo  
 Fabricantes de hardware lançam drivers de dispositivo em uma das duas formas:  

-   Como um pacote que pode ser extraído e que contém arquivos .inf usados para importar o driver para o Deployment Workbench  

-   Como um aplicativo que precisa ser instalado usando processos de instalação de aplicativo tradicionais  

 Pacotes de driver de dispositivo que podem ser extraídos para acessar os arquivos .inf podem usar o processo de detecção e instalação automática de driver do MDT importando primeiro o driver para o nó Drivers não Incluídos no Deployment Workbench.  

 Pacotes de driver de dispositivo que não podem ser extraídos para isolar os arquivos .inf ou aqueles que não funcionam corretamente sem primeiro serem instalados usando um instalador de aplicativo como um arquivo .MSI ou Setup.exe podem usar o recurso de Instalação de Aplicativo do MDT e instalar o driver de dispositivo durante o processo de implantação, como ocorreria em qualquer aplicativo normal.  

###  <a name="InstallOutofBoxDrivers"></a> Instalando drivers de dispositivo usando o método de drivers não incluídos  
 Você pode importar pacotes de driver de dispositivo que incluem um arquivo .inf para o Deployment Workbench e instalá-los automaticamente como parte do processo de implantação. Para implementar esse tipo de implantação do driver de dispositivo, primeiro adicione o driver de dispositivo ao Deployment Workbench.  

 **Para adicionar o driver de dispositivo ao Deployment Workbench**  

1.  Baixe os drivers de dispositivo necessários para os tipos de hardware serem implantados e extraia o pacote de driver de dispositivo para um local temporário.  

2.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

3.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação*/Out-of-Box Drivers (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

4.  No painel Ações, clique em **Importar Drivers**.  

     O Assistente de Importação de Driver de Dispositivo é iniciado.  

5.  Na página **Especificar o Diretório**, na seção do diretório **Origem da unidade**, clique em **Procurar** para ir para a pasta que contém os novos drivers de dispositivo e, em seguida, clique em **Avançar**.  

    > [!NOTE]
    >  O Assistente de novo Driver de Dispositivo procurará todos os subdiretórios do diretório de origem do driver, portanto, se houver vários drivers a serem instalados, extraia-os para pastas no mesmo diretório raiz e defina o diretório de origem do driver como o diretório raiz que contém todas as pastas de origem do driver.  

6.  Na página **Resumo**, verifique se as configurações estão corretas e, em seguida, clique em **Avançar** para importar os drivers para o Deployment Workbench.  

7.  Na página **Confirmação**, clique em **Concluir**.  

 Se os drivers de dispositivo contêm drivers cruciais para inicialização, como drivers de armazenamento em massa ou de classe de rede, o compartilhamento de implantação precisará ser atualizado em seguida para gerar um novo ambiente de inicialização LiteTouch_x86 e LiteTouch_x64 contendo os novos drivers.  

 **Para adicionar drivers de dispositivo às imagens Lite Touch Windows PE**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação* (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel Ações, clique em **Atualizar Compartilhamento de Implantação**.  

     O Assistente de Atualização de Compartilhamento de Implantação é iniciado.  

4.  Na página **Opções**, selecione as opções desejadas para atualizar o compartilhamento de implantação e clique em **Avançar**.  

5.  Na página **Resumo**, verifique se os detalhes estão corretos e clique em **Avançar**.  

6.  Na página **Confirmação**, clique em **Concluir**.  

###  <a name="InstallDriversasApplications"></a> Instalando drivers de dispositivo como aplicativos  
 Drivers de dispositivo que são empacotados como aplicativos e que não podem ser extraídos para uma pasta que contém um arquivo .inf, além dos arquivos de driver, devem ser adicionados ao Deployment Workbench como um aplicativo de instalação durante o processo de implantação.  

 Aplicativos podem ser especificados como uma etapa de sequência de tarefas ou especificados em CustomSettings.ini, no entanto, os aplicativos de driver de dispositivo devem ser instalados somente quando a sequência de tarefas é executada em um computador com os dispositivos. Para garantir isso, execute a etapa da sequência de tarefas para implantar os aplicativos de driver de dispositivo relevantes como uma etapa condicional. Os critérios condicionais podem ser especificados para executar a etapa da sequência de tarefas usando consultas WMI para o dispositivo no computador de destino.  

#### <a name="add-the-device-driver-application-to-the-deployment-workbench"></a>Adicionar o aplicativo do driver de dispositivo ao Deployment Workbench  
 Cada aplicativo de driver de dispositivo precisa primeiro ser importado para o Deployment Workbench.  

> [!NOTE]
>  Configure se o aplicativo deve ficar visível durante a implantação na caixa de diálogo **Propriedades** de qualquer aplicativo marcando ou desmarcando a caixa de seleção **Ocultar este aplicativo no Assistente de Implantação**. Repita esse processo para cada aplicativo de driver de dispositivo usado durante a implantação.  

 **Para adicionar o aplicativo do driver de dispositivo ao Deployment Workbench**  

1.  Baixe o aplicativo de driver de dispositivo e salve-o em um local temporário.  

2.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

3.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação*/Applications (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

4.  No painel Ações, clique em **Novo Aplicativo**.  

     O Assistente de Novo Aplicativo é iniciado.  

5.  Na página **Tipo de Aplicativo**, clique em **Aplicativo com arquivos de origem** e, em seguida, clique em **Avançar**.  

6.  Na página **Detalhes**, digite os detalhes relevantes sobre o aplicativo e clique em **Avançar**.  

7.  Na página **Origem**, na seção **Diretório de origem**, clique em **Procurar** para ir para a pasta e clique no diretório que contém os arquivos de origem do driver de dispositivo. Clique em **OK**.  

8.  Clique em **Avançar**.  

9. Na página **Destino**, digite um nome para o diretório de destino e clique em **Avançar**.  

10. Na página **Detalhes do Comando**, na seção **Linha de comando**, digite o comando que permite a instalação silenciosa do aplicativo de driver de dispositivo.  

11. Na página **Resumo**, verifique se as configurações estão corretas e clique em **Avançar** para importar o aplicativo de driver de dispositivo para o Deployment Workbench.  

12. Na página **Confirmação**, clique em **Concluir**.  

 Depois que os aplicativos forem importados para o Deployment Workbench, adicione-os ao processo de implantação usando a lógica apropriada para garantir que o aplicativo seja instalado apenas se executado no hardware correto. Existem diferentes métodos para fazer isso:  

-   Especificar o aplicativo de driver de dispositivo como parte de uma sequência de tarefas de implantação.  

-   Especificar o aplicativo de driver de dispositivo em CustomSettings.ini.  

-   Especificar o aplicativo de driver de dispositivo no MDT DB.  

 Essa abordagem é descrita mais detalhadamente nas seções a seguir.  

####  <a name="SpecifyDeviceAppTask"></a> Especificar o aplicativo de driver de dispositivo como parte de uma sequência de tarefas  
 O primeiro método para adicionar um aplicativo de driver de dispositivo ao processo de implantação é usar uma sequência de tarefas para adicionar etapas para cada aplicativo de driver de dispositivo.  

 Há duas abordagens principais para gerenciar aplicativos de driver de dispositivo na sequência de tarefas:  

-   Crie um novo grupo de sequências de tarefas para cada modelo de hardware e, em seguida, adicione uma consulta para executar esse grupo de ações se o computador corresponder a um tipo de hardware específico.  

-   Crie um grupo de sequências de tarefas para aplicativos específicos de hardware e, em seguida, adicione consultas para cada ação da sequência de tarefas de maneira que cada etapa da sequência de tarefas seja avaliada em relação ao tipo de hardware e seja executada somente se uma correspondência for encontrada.  

 **Para criar um novo grupo de sequências de tarefas para cada tipo de hardware**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação*/Task Sequences (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel de detalhes, clique em ***sequência_de_tarefas*** (em que *sequência_de_tarefas* é a sequência de tarefas de implantação que será necessária para instalar o aplicativo do driver de dispositivo).  

4.  No painel Ações, clique em **Propriedades**.  

5.  Na caixa de diálogo ***Propriedades da sequência_de_tarefas***, na guia **Sequência de Tarefas**, no painel de detalhes, acesse State Restore/Windows Update (Instalação pré-aplicação).  

6.  Na guia **Sequência de Tarefas**, clique em **Adicionar** e, em seguida, em **Novo Grupo**.  

     Isso cria um novo grupo de sequências de tarefas na sequência de tarefas. Use esse novo grupo de sequências de tarefas para criar as etapas para instalar os aplicativos de driver de dispositivo específicos do hardware.  

7.  No painel de detalhes, clique em **Novo Grupo**.  

8.  Na guia **Propriedades**, na caixa **Nome**, digite ***nome_do_grupo*** (em que *nome_do_grupo* é o nome do grupo; por exemplo, *Aplicativos específicos de hardware – Dell Computer Corporation*).  

9. Na guia **Opções**, clique em **Adicionar** e, em seguida, em **Consultar WMI**.  

10. Na caixa de diálogo **Condição de WMI da sequência de tarefas**, digite os seguintes detalhes:  

    -   Na caixa **Namespace de WMI**, digite **root\cimv2**.  

    -   Na caixa **Consulta WQL**, digite uma consulta WQL usando a classe **Win32_ComputerSystem** para garantir que o aplicativo seja instalado apenas para um tipo específico de aplicativo – por exemplo:  

         **Select \* FROM Win32_ComputerSystem WHERE Model LIKE *%modelo_do_hardware%* AND Manufacturer LIKE *%fabricante_do_hardware%***  

         Neste exemplo, *modelo_do_hardware* refere-se ao nome do modelo de computador (como Latitude D620) e *fabricante_do_hardware* ao nome da marca do computador (como Dell Corporation).  

         O símbolo **%** é um caractere curinga incluído nos nomes para permitir que os administradores retornem qualquer fabricante ou modelo de computador contendo o valor especificado para ***modelo_do_hardware*** ou ***fabricante_do_hardware***.  

     Para obter mais informações sobre consultas WMI e WQL, consulte a seção “Adicionar consultas WMI a condições de etapa da sequência de tarefas” no documento do MDT *Usando o Microsoft Deployment Toolkit* e [Consultas com WQL](http://msdn.microsoft.com/library/aa392902.aspx).  

11. Clique em **OK** para enviar a consulta e, em seguida, em **OK** para enviar as alterações para a sequência de tarefas.  

> [!NOTE]
>  Este processo precisa ser repetido para cada tipo de hardware de cada aplicativo de driver de dispositivo a ser instalado.  

 Após a criação dos grupos da sequência de tarefas específicos de hardware, os aplicativos de driver de dispositivo poderão ser adicionados a cada grupo.  

 **Para adicionar aplicativos de driver de dispositivo a grupos de sequências de tarefas específicas de hardware**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação*/Task Sequences (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel de detalhes, clique em ***sequência_de_tarefas*** (em que *sequência_de_tarefas* é a sequência de tarefas de implantação que será necessária para instalar o aplicativo do driver de dispositivo).  

4.  No painel Ações, clique em **Propriedades**.  

5.  Na caixa de diálogo ***Propriedades da sequência_de_tarefas***, clique na guia **Sequência de Tarefas**.  

6.  No painel de detalhes, acesse State Restore/*grupo_específico_de_hardware* (em que *grupo_específico_de_hardware* refere-se ao nome do grupo específico de hardware em que a etapa da sequência de tarefas será adicionada para instalar o aplicativo de driver de dispositivo).  

7.  Na guia **Sequência de Tarefas**, clique em **Adicionar**, clique em **Geral** e em **Instalar Aplicativo**.  

     A etapa da sequência de tarefas **Instalar Aplicativo** é exibida no painel de detalhes.  

8.  No painel de detalhes, clique em **Instalar Aplicativo.**  

9. Na guia **Propriedades**, clique em **Instalar um único aplicativo** e, na lista **Aplicativo a ser instalado**, selecione ***aplicativo_de_hardware*** (em que *aplicativo_de_hardware* refere-se ao aplicativo para instalar o aplicativo específico do hardware).  

> [!NOTE]
>  É necessário repetir este processo para cada aplicativo de driver de dispositivo que precisa ser usado durante uma implantação.  

#### <a name="specify-the-device-driver-application-in-customsettingsini"></a>Especificar o aplicativo de driver de dispositivo em CustomSettings.ini  
 Quando uma implantação LTI ou ZTI começa, uma das primeiras ações a ser concluída é o processamento dos arquivos de controle BootStrap.ini e CustomSettings.ini. Ambos esses arquivos contêm regras que podem ser usadas para personalizar dinamicamente a implantação.  

 Devido à forma que o MDT processa o arquivo CustomSettings.ini, você poderá usá-lo para adicionar aplicativos dependendo de condições específicas. Essa lógica será usada para adicionar aplicativos específicos do driver de dispositivo durante a implantação com base em tipos específicos de hardware. Aplicativos são referenciados em CustomSettings.ini pelo GUID do aplicativo, localizado no arquivo Applications.xml no compartilhamento de implantação.  

 **Para localizar um GUID do aplicativo importado**  

1.  No compartilhamento de implantação do servidor de implantação, abra a pasta Control – por exemplo, D:\Production Deployment Share\Control.  

2.  Localize e abra o arquivo Applications.xml.  

3.  Localize o aplicativo necessário.  

4.  Localize o GUID do aplicativo, localizando a linha entre as marcas `<guid>` do aplicativo como, por exemplo, `<application guid={c303fa6e-3a4d-425e-8102-77db9310e4d0}>`.  

 Como parte do processo de inicialização, os processos do ZTI e do LTI coletam informações sobre o computador de execução. Como parte desse processo, as consultas WMI são executadas e os valores de marca e fabricante da classe **Win32_ComputerSystem** são populados como as variáveis **%Make%** e **%Model%**, respectivamente.  

 Esses valores podem ser usados durante o processamento do arquivo CustomSettings.ini para ler dinamicamente as seções do arquivo, dependendo da marca e modelo detectados.  O exemplo a seguir mostra um exemplo do arquivo CustomSettings.ini.  

 **CustomSettings.ini de exemplo configurado para uma instalação de aplicativo de hardware específico**  

```  
[Settings]  
Priority=Make, Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  

[Dell Computer Corporation]  
Subsection=Dell-%Model%  

[Dell-Latitude D620]  
MandatoryApplications001={1D7DF331-47B7-472C-87B3-442597EC2F7D}  

[Dell-Latitude D610]  
MandatoryApplications001={c303fa6e-3a4d-425e-8102-77db9310e4d0}  
```  

 Use as seguintes propriedades para especificar os aplicativos em CustomSettings.ini:  

-   **Applications**. Essa propriedade pode ser usada quando os administradores de implantação não quiserem apresentar um assistente de aplicativo como parte do processo de implantação, especificando **SkipApplications=YES** em CustomSettings.ini.  

-   **MandatoryApplications**. Essa propriedade poderá ser usada se os administradores de implantação desejarem apresentar o assistente de aplicativo durante a implantação para permitir que os engenheiros de implantação selecionem aplicativos adicionais a serem instalados durante a implantação.  

     Se o assistente de aplicativo for usado sem a propriedade **MandatoryApplications** (por exemplo, **SkipApplications=NO**), ele substituirá os aplicativos especificados pela propriedade **Applications**.  

     O exemplo anterior mostra como usar os valores de variáveis **%Make%** e **%Model%** para manipular dinamicamente a maneira como a lista de aplicativos é criada. Os valores para a marca e o modelo de cada tipo de hardware podem ser localizados usando um dos seguintes métodos:  

-   **A ferramenta Informações do Sistema**. Use o nó Resumo do Sistema nessa ferramenta para identificar o **Fabricante do Sistema** (marca) e **Modelo do Sistema** (modelo).  

-   **Windows PowerShell**. Use o cmdlet **Get-WMIObject –class Win32_ComputerSystem** para determinar a marca e o modelo do computador.  

-   **Linha de comando da Instrumentação de Gerenciamento do Windows**. Use **CSProduct Get Name, Vendor** para retornar o nome (modelo) e o fornecedor (marca) do computador.  

 **Para modificar CustomSettings.ini para adicionar lógica específica do hardware**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação* (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel Ações, clique em **Propriedades**.  

4.  Clique na guia **Regras**.  

5.  As informações digitadas nessa guia são armazenadas no arquivo CustomSettings.ini. Modifique as entradas do arquivo CustomSettings.ini para adicionar lógica para cada modelo de hardware que tem um aplicativo de driver de dispositivo específico, conforme descrito em [Especificar o aplicativo de driver de dispositivo como parte de uma sequência de tarefas](#SpecifyDeviceAppTask).  

6.  Clique em **OK** para enviar as alterações.  

7.  No painel de detalhes, clique em *compartilhamento_de_implantação* (em que *compartilhamento_de_implantação* é o nome do compartilhamento de implantação a ser configurado).  

8.  No painel Ações, clique em **Atualizar Compartilhamento de Implantação**.  

     O Assistente de Atualização de Compartilhamento de Implantação é iniciado.  

9. Na página **Opções**, selecione as opções desejadas para atualizar o compartilhamento de implantação e clique em **Avançar**.  

10. Na página **Resumo**, verifique se os detalhes estão corretos e clique em **Avançar**.  

11. Na página **Confirmação**, clique em **Concluir**.  

 Por padrão, todos os aplicativos disponíveis são exibidos no Assistente de Implantação do Windows durante a implantação de LTI. Como aplicativos de driver de dispositivo específicos são aplicáveis apenas a determinados tipos de hardware, talvez não seja uma boa ideia exibi-los o tempo todo. Ao definir o pacote de aplicativos específicos do driver de dispositivo em CustomSettings.ini, o aplicativo pode ficar oculto usando a opção **Ocultar o aplicativo no Assistente de Implantação** na configuração do aplicativo.  

 **Para ocultar um aplicativo no Assistente de Implantação**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação*/Applications (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel de detalhes, clique em ***aplicativo_de_driver_de_dispositivo*** (em que *aplicativo_de_driver_de_dispositivo* é o aplicativo a ser ocultado do Assistente de Implantação).  

4.  No painel Ações, clique em **Propriedades**.  

5.  Na guia **Geral**, marque a caixa de seleção **Ocultar o aplicativo no Assistente de Implantação**.  

6.  Clique em **Aplicar** e feche a caixa de diálogo **Propriedades**.  

#### <a name="specify-the-device-driver-application-in-the-mdt-db"></a>Especificar o aplicativo do driver de dispositivo no MDT DB  
 O MDT DB é uma versão de banco de dados do arquivo CustomSettings.ini e pode ser consultado no momento da implantação para obter informações a serem usadas durante a implantação. Para obter mais informações sobre como usar o MDT DB, consulte “Selecionando os métodos para aplicar os parâmetros de configuração”.  

 Ao consultar o MDT DB no momento da implantação, três métodos estão disponíveis para identificar o computador de destino:  

-   Procure o computador individual (usando o endereço MAC, a marca de ativo ou algo semelhante).  

-   Procure o local do computador (usando o gateway padrão).  

-   Procure a marca e o modelo do computador (usando consultas WMI de fabricante ou marca e modelo).  

 Para cada entrada de banco de dados criada, é possível especificar as propriedades de implantação, aplicativos, se os pacotes do Configuration Manager devem ser usados e os administradores. Ao criar as entradas de marca e modelo do banco de dados, você pode adicionar os aplicativos de driver de dispositivo de hardware específico necessários.  

 **Para criar entradas no MDT DB para permitir a instalação de aplicativos do driver de dispositivo**  

> [!NOTE]
>  Repita esse processo para cada marca e modelo de hardware que requer um aplicativo de driver de dispositivo.  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/**compartilhamento_de_implantação**/Advanced Configuration/Database/Make and Model (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel Ações, clique em **Novo**.  

4.  Na caixa de diálogo **Propriedades** da guia **Identidade**, na caixa **Marca**, digite ***nome_da_marca*** (em que *nome_da_marca* é um nome de fácil identificação associado ao fabricante do computador de destino).  

5.  Na caixa **Modelo**, digite ***nome_do_modelo*** (em que *nome_do_modelo* é um nome de fácil identificação associado ao modelo do computador de destino).  

6.  Na guia **Aplicativos**, adicione cada um dos aplicativos de driver de dispositivo necessários para o modelo de hardware.  

## <a name="initiating-mdt-using-windows-deployment-services"></a>Iniciando o MDT usando os Serviços de Implantação do Windows  
 O Windows Server 2008 usa os Serviços de Implantação do Windows como uma versão atualizada e reprojetada dos Serviços de Instalação Remota, a ferramenta de implantação padrão no Windows Server 2003 com SP2. Usando os Serviços de Implantação do Windows, é possível implantar sistemas operacionais Windows – particularmente, o Windows 7, o Windows Server 2008 ou sistemas operacionais posteriores – em uma rede usando a mídia de inicialização ou o adaptador de rede habilitado para PXE de um computador.  

 Antes de implantar Serviços de Implantação do Windows, determine qual das seguintes opções de integração melhor atende ao seu ambiente:  

-   Opção 1. Inicialize os computadores no PXE para iniciar o processo de LTI.  

-   Opção 2. Implante uma imagem do sistema operacional do repositório de imagens dos Serviços de Implantação do Windows.  

-   Opção 3. Use multicast com o MDT e a função de servidor dos Serviços de Implantação do Windows do Windows Server 2008.  

### <a name="option-1-boot-computers-in-pxe-to-initiate-the-lti-process"></a>Opção 1: inicializar os computadores no PXE para iniciar o processo de LTI  
 Ajude a minimizar o custo de gerenciar implantações de sistema operacional iniciando o processo de implantação do MDT usando os Serviços de Implantação do Windows junto com o protocolo DHCP. Isso elimina a necessidade de criar e entregar mídia inicializável para cada computador de destino.  

#### <a name="create-and-import-the-deployment-workbench-windows-pe-image-into-windows-deployment-services"></a>Criar e importar a imagem do Windows PE do Deployment Workbench para os Serviços de Implantação do Windows  
 Ao criar um novo compartilhamento de implantação do MDT ou modificar um compartilhamento de implantação do MDT existente, é possível criar uma imagem de inicialização do Windows PE personalizada. Quando o compartilhamento de implantação é atualizado, a imagem de inicialização do Windows PE é gerada automaticamente e atualizada com informações sobre o compartilhamento de implantação. Ela injetará os drivers ou componentes adicionais especificados durante a configuração de compartilhamento de implantação.  

 A imagem de inicialização do Windows PE é gerada como um arquivo de imagem ISO, que pode ser gravada em um CD ou DVD, e um arquivo WIM inicializável. É possível importar o arquivo WIM para os Serviços de Implantação do Windows, de forma que os computadores que podem ser inicializados no PXE possam baixar e executar a imagem de inicialização LTI do Windows PE em uma rede usada para inicializar uma instalação.  

 **Para criar uma imagem do Windows PE inicializável no Deployment Workbench**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação* (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel Ações, clique em **Propriedades**.  

     Na caixa de diálogo ***Propriedades do compartilhamento_de_implantação***, clique na guia **Configurações da *plataforma* do Windows PE** (em que plataforma é a arquitetura da imagem do Windows PE a ser configurada).  

4.  Na área **Configurações de imagem de inicialização do Lite Touch**, marque a caixa de seleção **Gerar uma imagem ISO do disco de RAM inicializável do Lite Touch**.  

5.  Clique na guia **Componentes da *plataforma* do Windows PE** (em que *plataforma* é a arquitetura da imagem do Windows PE a ser configurada).  

6.  Na seção **Injeção de Driver**, clique nos tipos de driver apropriados para serem incluídos.  

    > [!NOTE]
    >  Essa etapa não será necessária se o Windows PE já incluir os drivers de dispositivo necessários.  

7.  Na seção **Injeção de Driver**, na lista **Perfil de seleção**, escolha o perfil de seleção de driver apropriado.  

8.  Na caixa de diálogo **Propriedades**, clique em **OK**.  

    > [!NOTE]
    >  Essa etapa não será necessária se o Windows PE já incluir os drivers de dispositivo necessários.  

9. No painel de detalhes, clique em ***compartilhamento_de_implantação*** (em que *compartilhamento_de_implantação* é o nome do compartilhamento de implantação a ser configurado).  

10. No painel Ações, clique em **Atualizar Compartilhamento de Implantação**.  

     O Assistente de Atualização de Compartilhamento de Implantação é iniciado.  

11. Na página **Opções**, selecione as opções desejadas para atualizar o compartilhamento de implantação e clique em **Avançar**.  

12. Na página **Resumo**, verifique se os detalhes estão corretos e clique em **Avançar**.  

13. Na página **Confirmação**, clique em **Concluir**.  

     Quando esse processo for concluído, a pasta Boot no compartilhamento de implantação conterá diversas imagens de inicialização, como por exemplo:  

     D:\Production Deployment Share\Boot\LiteTouchPE_x64.iso  

     D:\Production Deployment Share\Boot\LiteTouchPE_x64.wim  

     D:\Production Deployment Share\Boot\LiteTouchPE_x86.iso  

     D:\Production Deployment Share\Boot\LiteTouchPE_x86.wim  

 Você pode gravar os arquivos ISO gerados diretamente em CD ou DVD ou usá-los para inicializar o processo de LTI em um novo hardware. Também é possível importar os arquivos WIM de inicialização para os Serviços de Implantação do Windows, para que os novos computadores possam inicializar o processo de implantação LTI sem precisar de mídia física.  

 **Para importar a imagem do Windows PE para os Serviços de Implantação do Windows**  

1.  Inicie o console dos Serviços de Implantação do Windows e, em seguida, conecte-se aos Serviços de Implantação do Windows.  

2.  Na árvore de console, clique com o botão direito do mouse em **Imagens de Inicialização**e, em seguida, clique em **Adicionar Imagem de Inicialização**.  

3.  Navegue até a imagem WIM a ser importada – por exemplo, D:\Production Deployment Share\Boot\LiteTouchPE_x86.wim.  

4.  O processo de importação lê automaticamente os metadados da imagem de inicialização, mas os valores **Nome da Imagem** e **Descrição da Imagem** também podem ser editados; o **Nome da Imagem** afeta as informações de opções de inicialização exibidas pelo Gerenciador de Inicialização do Windows quando o cliente é inicializado no PXE.  

5.  Quando a imagem de inicialização foi importada, qualquer computador que é inicializado no PXE e recebe uma resposta dos Serviços de Implantação do Windows poderá baixar a imagem de inicialização LTI e iniciar uma instalação LTI.  

 A instalação e configuração dos Serviços de Implantação do Windows não são abordadas neste guia. Para obter mais informações sobre os Serviços de Implantação do Windows, consulte o [Guia dos Serviços de Implantação do Windows](http://technet.microsoft.com/library/cc265612.aspx).  

#### <a name="use-windows-deployment-services-to-automatically-detect-the-deployment-server"></a>Usar os Serviços de Implantação do Windows para detectar automaticamente o servidor de implantação  
 Uma opção adicional está disponível ao usar os Serviços de Implantação do Windows para hospedar imagens de inicialização do MDT quando o compartilhamento de implantação do MDT está hospedado no mesmo servidor que os Serviços de Implantação do Windows.  

 Quando um cliente PXE carrega a imagem de inicialização do MDT, o nome do servidor dos Serviços de Implantação do Windows que hospeda a imagem de inicialização é capturado e colocado no **WDSServer** do MDTProperty. Dessa forma, você poderá fazer referência a esta propriedade no arquivo BootStrap.ini da imagem de inicialização e no arquivo CustomSettings.ini do compartilhamento de implantação da propriedade **DeployRoot**. Isso resulta em um cliente que é inicializado automaticamente dos Serviços de Implantação do Windows usando o compartilhamento de implantação hospedado no servidor dos Serviços de Implantação do Windows. Isso elimina a necessidade de especificar um nome do servidor em qualquer arquivo de configuração.  

 **Para definir o servidor local dos Serviços de Implantação do Windows como o servidor de implantação**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação*/Advanced Configuration/Database (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel Ações, clique em **Propriedades**.  

4.  Clique na guia **Regras**.  

     As informações digitadas nessa guia são armazenadas no arquivo CustomSettings.ini.  

5.  Configure a propriedade **DeployRoot** para usar a variável **%WDSServer%**, por exemplo **DeployRoot=\\\\%WDSServer%\Deployment$**.  

6.  Clique em **Editar Bootstrap.ini**.  

7.  Configure o BootStrap.ini para usar a propriedade **%WDSServer%** adicionando ou alterando o valor **DeployRoot** para **DeployRoot=\\\\%WDSServer%\Deployment$**.  

8.  No menu **Arquivo**, clique em **Salvar** para salvar as alterações no arquivo BootStrap.ini.  

9. Clique em **OK**.  

     O compartilhamento de implantação precisa ser atualizado.  

10. No painel de detalhes, clique em **compartilhamento_de_implantação** (em que *compartilhamento_de_implantação* é o nome do compartilhamento de implantação a ser configurado).  

11. No painel Ações, clique em **Atualizar Compartilhamento de Implantação**.  

     O Assistente de Atualização de Compartilhamento de Implantação é iniciado.  

12. Na página **Opções**, selecione as opções desejadas para atualizar o compartilhamento de implantação e clique em **Avançar**.  

13. Na página **Resumo**, verifique se os detalhes estão corretos e clique em **Avançar**.  

14. Na página **Confirmação**, clique em **Concluir**.  

15. Importe o WIM de inicialização atualizado para os Serviços de Implantação do Windows.  

### <a name="option-2-deploy-an-operating-system-image-from-the-windows-deployment-services-store"></a>Opção 2: implantar uma imagem do sistema operacional do repositório dos Serviços de Implantação do Windows  
 Se você já estiver usando os Serviços de Implantação do Windows para implantação de sistema operacional, estenda a funcionalidade do MDT configurando-o para fazer referência às imagens do sistema operacional dos Serviços de Implantação do Windows que já estão sendo utilizadas em vez de usar seu próprio repositório e para complementar implantações dos Serviços de Implantação do Windows com o gerenciamento de drivers, implantação de aplicativos, instalação da atualizações, processamento de regras e outras funcionalidades do MDT. Após o MDT fazer referência a uma imagem do sistema operacional dos Serviços de Implantação do Windows, trate-o como qualquer sistema operacional que tenha sido preparado para um compartilhamento de implantação do MDT.  

 **Para fazer referência a uma imagem do sistema operacional dos Serviços de Implantação do Windows**  

> [!NOTE]
>  As etapas a seguir exigem que pelo menos uma imagem de sistema operacional tenha sido previamente importada para o servidor dos Serviços de Implantação do Windows.  

1.  Atualize o MDT para poder acessar imagens dos Serviços de Implantação do Windows copiando os seguintes arquivos da pasta Sources da mídia do Windows para a pasta de fontes de mídia do Windows para a pasta C:\Program Files\Microsoft Deployment Toolkit\bin no servidor dos Serviços de Implantação do Windows:  

    -   Wdsclientapi.dll  

    -   Wdscsl.dll  

    -   Wdsimage.dll  

    -   Wdstptc.dll (só é aplicável ao copiar dos diretórios de origem do Windows Server 2008)  

    > [!NOTE]
    >  O diretório de origem do Windows que está sendo usado precisa corresponder à plataforma do sistema operacional em execução no computador no qual o MDT está instalado.  

2.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

3.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação*/Operating Systems (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

4.  No painel Ações, clique em **Importar Sistema Operacional**.  

     O Assistente de Novo Sistema Operacional é iniciado.  

5.  Na página **Tipo de sistema operacional**, clique em **Imagens dos Serviços de Implantação do Windows** e, em seguida, em **Avançar**.  

6.  Na página **Servidor WDS**, digite o nome do servidor dos Serviços de Implantação do Windows a ser referenciado – por exemplo, **WDSSvr001**— e, em seguida, clique em **Avançar**.  

7.  Na página **Resumo**, verifique se as definições estão corretas e clique em **Avançar**.  

8.  Na página **Confirmação**, clique em **Concluir**.  

     Todas as imagens disponíveis no servidor dos Serviços de Implantação do Windows agora estarão disponíveis para as sequências de tarefas do MDT.  

> [!NOTE]
>  A importação de imagens dos Serviços de Implantação do Windows não copia os arquivos de origem do servidor dos Serviços de Implantação do Windows para o compartilhamento de implantação. O MDT continua a usar os arquivos de origem de seu local original.  

### <a name="option-3-use-multicasting-with-mdt-and-the-windows-server-2008-windows-deployment-services-role"></a>Opção 3: usar multicast com o MDT e a função dos Serviços de Implantação do Windows do Windows Server 2008  
 Com o lançamento do Windows Server 2008, os Serviços de Implantação do Windows foram aprimorados para dar suporte à implantação de imagens usando transmissões multicast. O MDT também inclui atualizações para integrar multicast dos Serviços de Implantação do Windows ao MDT.  

 Além disso, uma Windows AIK (Kit de Instalação Automatizada) atualizada, a versão 1.1, inclui o Wdsmcast.exe. Isso permite ingressar nas sessões de multicast manualmente e permite que o cliente que inicia o Wdsmcast.exe copie arquivos de uma sessão multicast ativa.  

 O script LTIApply.wsf usa Wdsmcast.exe ao acessar os arquivos de origem do sistema operacional do compartilhamento de implantação. O LTIApply.wsf busca pelo Wdsmcast.exe no compartilhamento de implantação, seja na pasta *compartilhamento_de_implantação*\Tools\x86 ou na pasta *compartilhamento_de_implantação*\Tools\x64 (em que *compartilhamento_de_implantação* refere-se ao nome da pasta do sistema de arquivos que contém o compartilhamento de implantação), dependendo da versão Windows PE em execução.  

 Quando LTIApply.wsf for executado, ele sempre tentará acessar e baixar imagens WIM de um fluxo multicast existente, porém retornará a uma cópia de arquivo padrão se um fluxo multicast não existir.  

> [!NOTE]
>  Esse processo se aplica somente a arquivos de imagem WIM.  

 Os pré-requisitos do servidor de implantação para preparar a transmissão multicast do MDT são:  

-   O servidor de implantação precisa executar o Windows Server 2008 ou posterior  

-   A função dos Serviços de Implantação do Windows deve ser instalada no console do Gerenciamento de Servidor  

-   O Windows AIK 1.1 para Windows Server 2008 precisa estar instalado  

-   O MDT precisa estar instalado  

-   Como em qualquer implantação que utiliza o MDT, pelo menos uma imagem WIM do sistema operacional precisa ter sido importada, seja como um conjunto completo de arquivos de origem ou como uma imagem personalizada com arquivos de instalação  

> [!NOTE]
>  É importante usar a versão mais recente do Windows AIK para multicasting. A cópia do Windows PE incluída em versões anteriores do Windows AIK – por exemplo, o Windows AIK 1.0 – não é compatível com o download de um servidor multicast.  

 **Para configurar o MDT para multicasting de um compartilhamento de implantação existente**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação* (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação a ser configurado).  

3.  No painel Ações, clique em **Propriedades**.  

4.  Na guia **Geral**, marque a caixa de seleção **Habilitar multicast para este compartilhamento de implantação (requer os Serviços de Implantação do Windows do Windows Server 2008)**.  

5.  Clique em **OK**.  

6.  No painel Ações, clique em **Atualizar Compartilhamento de Implantação**.  

     O Assistente de Atualização de Compartilhamento de Implantação é iniciado.  

7.  Na página **Opções**, selecione as opções desejadas para atualizar o compartilhamento de implantação e clique em **Avançar**.  

8.  Na página **Resumo**, verifique se os detalhes estão corretos e clique em **Avançar**.  

9. Na página **Confirmação**, clique em **Concluir**.  

 O compartilhamento de implantação agora está configurado para transmissão multicast dos Serviços de Implantação do Windows.  

 Esse processo cria uma transmissão multicast automático dos Serviços de Implantação do Windows que usa diretamente o compartilhamento de implantação do MDT existente. O MDT não criar transmissões multicast agendadas. Observe também que imagens adicionais não são importadas para os Serviços de Implantação do Windows e que não é possível usar o multicast para imagens de inicialização, pois não é possível carregar o cliente do multicast depois que o Windows PE estiver em execução.  

 **Para verificar se a transmissão multicast foi gerada nos Serviços de Implantação do Windows**  

1.  Clique em **Iniciar**, aponte para **Ferramentas Administrativas** e clique em **Serviços de Implantação do Windows**.  

2.  Na árvore de console dos Serviços de Implantação do Windows, clique com o botão direito do mouse em **Servidores** e, em seguida, clique em **Adicionar Servidor**.  

3.  Na caixa de diálogo **Adicionar Servidores**, clique em **Computador local** e em **OK**.  

4.  Na árvore de console dos Serviços de Implantação do Windows, clique em **Servidores** e em ***nome_do_servidor*** (em que *nome_do_servidor* refere-se ao nome do computador que executa os Serviços de Implantação do Windows). Clique em **Transmissões multicast**.  

5.  No painel de detalhes, será listada uma nova transmissão de multicast automático para o compartilhamento de implantação – por exemplo, **BDD Share Deployment$**.  

6.  Verifique se o status da transmissão multicast automático **BDD Share Deployment$** está definida como **Ativa**.  

 Após a implantação de um computador, verifique se que o sistema operacional foi baixado de uma transmissão multicast examinando o arquivo BDD.log na pasta \Windows\Temp\DeploymentLogs.  

 Haverá duas entradas na pasta de logs, ambas a partir da **Transferência de multicast**; verifique-as para confirmar se a transferência foi bem-sucedida. Para obter mais informações sobre as transmissões multicast com o MDT e os Serviços de Implantação do Windows, consulte a seção “Habilitar os Serviços de Implantação do Windows para implantações LTI”, no documento do MDT *Usando o Microsoft Deployment Toolkit*.  

## <a name="performing-staged-deployments-using-mdt-oem-preload"></a>Executar implantações de teste usando o MDT (pré-carregamento de OEM)  
 Em muitas organizações, os computadores serão carregados com a imagem do sistema operacional antes da implantação para a rede de produção. Em alguns casos, o carregamento da imagem do sistema operacional é executado por uma equipe dentro da organização que é responsável pela criação de computadores em um ambiente de preparo. Em outros casos, o carregamento da imagem do sistema operacional é realizado pelo fornecedor de hardware do computador, também conhecido como um OEM (*fabricante de equipamento original*).  

> [!NOTE]
>  O processo de pré-carregamento de OEM tem suporte no MDT somente em implantações realizadas usando LTI. Para o Configuration Manager, use o recurso de mídia pré-configurada.  

### <a name="overview-of-the-oem-preload-process-in-mdt"></a>Visão geral do processo de pré-carregamento de OEM no MDT  
 O processo de pré-carregamento de OEM é dividido em três fases:  

-   **Fase 1**. Crie uma imagem de mídia do computador de referência para ser aplicada no ambiente de preparo.  

-   **Fase 2**. Aplica a imagem do computador de referência ao computador de destino em um ambiente de preparo.  

-   **Fase 3**. Conclua a implantação do computador de destino no ambiente de produção.  

 As fases 1 e 3 geralmente são realizadas pela organização de implantação. Dependendo do uso do processo de pré-carregamento de OEM na organização, a Fase 2 pode ser executada pela organização ou pelo fornecedor de hardware de computador dos computadores. Se a organização executar a Fase 2, o ambiente de preparo estará dentro da organização. Se um OEM executar a Fase 2, o ambiente de preparo estará no ambiente do OEM.  

#### <a name="overview-of-mdt-configuration-files-in-the-oem-preload-process"></a>Visão geral dos arquivos de configuração do MDT no processo de pré-carregamento de OEM  
 Arquivos de configuração do MDT separados (CustomSettings.ini e Bootstrap.ini) são usados pelas sequências de tarefas executadas durante as Fases 1 e 3 do processo de pré-carregamento de OEM. No entanto, ambos arquivos de configuração existem simultaneamente em estruturas de pasta diferentes.  

 Na primeira fase, os arquivos de configuração são usados durante a criação do computador de referência e armazenados na pasta específica para a sequência de tarefas usada nessa fase. Os arquivos de configuração usados na terceira e última fase do processo de pré-carregamento de OEM são armazenados na pasta específica para a sequência de tarefas usada nessa fase.  

 Ao fazer modificações nos arquivos de configuração, verifique se as alterações correspondem à sequência de tarefas apropriada em cada fase do processo de pré-carregamento de OEM.  

#### <a name="overview-of-mdt-log-files-in-the-oem-preload-process"></a>Visão geral dos arquivos de log do MDT no processo de pré-carregamento de OEM  
 Arquivos de log do MDT separados são gerados durante as Fases 1 e 3 do processo de pré-carregamento de OEM:  

-   Os arquivos de log do MDT para a Fase 1 são armazenados nas pastas C:\MININT e C:\SMSTSLog.  

-   Os arquivos de log do MDT para a Fase 3 são armazenados na pasta %WINDIR%\System32\CCM\Logs para implantações com base x86 ou na pasta %WINDIR%\SysWow64\CCM\Logs para implantações com base x64.  

 Use a pasta apropriada ao diagnosticar ou solucionar problemas de implantação relacionados ao MDT.  

### <a name="staged-deployments-using-lti"></a>Implantações de teste usando LTI  
 Para implantações LTI, execute o processo de pré-carregamento de OEM usando um tipo de compartilhamento de implantação de *Mídia removível (Mídia)*. Outros tipos de compartilhamento de implantação não são compatíveis com o processo de pré-carregamento do OEM.  

 Para executar o processo de pré-carregamento de OEM, crie uma sequência de tarefas baseada no modelo de sequência de tarefas Sequência de Tarefas OEM Litetouch, além das sequências de tarefas que serão usadas para implantar o sistema operacional de destino. Em seguida, crie um compartilhamento de implantação de *Mídia removível (Mídia)*, que criará um arquivo ISO do conteúdo do compartilhamento de implantação, especificamente o arquivo LiteTouchPE_x86.iso ou LiteTouchPE_x64.iso (dependendo da plataforma do processador do computador de destino). O processo de atualização de compartilhamento de implantação também cria uma estrutura de pastas que pode ser usada para criar mídia no formato UDF.  

#### <a name="lti-oem-preload-processphase-1-create-a-media-based-image"></a>Processo de pré-carregamento de OEM LTI – Fase 1: criar uma imagem de mídia  
 A organização de implantação realiza a primeira fase do processo de pré-carregamento de OEM. A entrega desta fase é uma imagem inicializável (como um arquivo ISO) ou mídia (como um DVD) que é enviado ao OEM ou ao ambiente de preparo dentro da organização de implantação. A maioria dessas etapas é executada no Deployment Workbench.  

 **Para criar uma imagem de mídia para entrega ao OEM ou ao ambiente de preparo dentro da organização de implantação**  

1.  Popule os seguintes nós no compartilhamento de implantação no Deployment Workbench:  

    -   Sistemas operacionais  

    -   Aplicativos  

    -   Pacotes  

    -   Drivers não incluídos  

     Para obter mais informações sobre como realizar esta etapa, consulte a seção “Gerenciar compartilhamentos de implantação do Deployment Workbench” no documento do MDT *Usando o Microsoft Deployment Toolkit*.  

2.  Crie uma nova sequência de tarefas com base no modelo de sequência de tarefas OEM Litetouch Task Sequence no Deployment Workbench.  

     Para obter mais informações sobre a realização desta etapa, consulte a seção “Configurando sequências de tarefas no Deployment Workbench”, no documento do MDT *Usando o Microsoft Deployment Toolkit*.  

3.  Crie um ou mais sequências de tarefas que serão usadas para implantar o sistema operacional de destino no computador de destino após a implantação no ambiente de produção.  

     Para obter mais informações sobre a realização desta etapa, consulte a seção “Configurando sequências de tarefas no Deployment Workbench”, no documento do MDT *Usando o Microsoft Deployment Toolkit*.  

4.  Crie um perfil de seleção que inclua aplicativos, sistemas operacionais, drivers, pacotes e sequências de tarefas necessários para a implantação de OEM.  

     Para obter mais informações sobre como realizar esta etapa, consulte a seção “Gerenciar perfis de seleção” no documento do MDT *Usando o Microsoft Deployment Toolkit*.  

5.  Crie a mídia de implantação.  

     Para obter mais informações sobre como realizar esta etapa, consulte a seção “Gerenciar a mídia de implantação LTI” no documento do MDT *Usando o Microsoft Deployment Toolkit*.  

6.  Atualize a mídia de implantação criada no Deployment Workbench na etapa anterior.  

     Quando você atualiza a mídia de implantação, o Deployment Workbench cria o arquivo LiteTouchMedia.iso. Para obter mais informações sobre como realizar esta etapa, consulte a seção “Gerenciar a mídia de implantação LTI” no documento do MDT *Usando o Microsoft Deployment Toolkit*.  

7.  Grave um DVD do arquivo LiteTouchMedia.iso criado na etapa anterior.  

    > [!NOTE]
    >  Se o arquivo ISO for entregue para o OEM ou para o ambiente de preparo da organização, essa etapa não será necessária.  

8.  Entregue o arquivo ISO ou o DVD ao OEM ou ao ambiente de preparo da organização.  

#### <a name="lti-oem-preload-processphase-2-apply-the-image-to-the-target-computer"></a>Processo de pré-carregamento de OEM LTI – Fase 2: aplicar a imagem ao computador de destino  
 A segunda fase do processo de pré-carregamento de OEM é executada pelo OEM ou pela equipe de implantação no ambiente de preparo da organização de implantação. Durante essa fase do processo, o arquivo .iso ou DVD criado na Fase 1 é aplicada aos computadores de destino. A entrega dessa fase é a imagem implantada nos computadores de destino para que eles estejam prontos para implantação no ambiente de produção.  

 **Para aplicar a imagem aos computadores de destino**  

1.  Inicie um computador de destino com a mídia criada na Fase 1.  

     O Windows PE é iniciado e, em seguida, o Assistente de Implantação do Windows.  

2.  No Assistente de Implantação do Windows, clique na sequência de tarefas **Sequência de tarefas de pré-instalação de OEM para ambiente de preparo**.  

     A sequência de tarefas será iniciada e o conteúdo da mídia inicializável será copiado para o disco rígido local do computador de destino.  

3.  Quando o Assistente de Implantação do Windows estiver concluído para a sequência de tarefas **Sequência de tarefas de pré-instalação de OEM para o ambiente de preparo**, o disco rígido estará pronto para iniciar o restante do processo de implantação executando o Assistente de Implantação do Windows para as outras sequências de tarefas que são usados para implantar o sistema operacional.  

     A sequência de tarefas **Sequência de tarefas de pré-instalação de OEM para o ambiente de preparo** é responsável por implantar a imagem no computador de destino e iniciar o processo LTI. O Assistente de Implantação do Windows será iniciado uma segunda vez para executar as sequências de tarefas usadas para implantar o sistema operacional no computador de destino.  

4.  Clone o conteúdo do primeiro disco rígido para o número necessário de computadores de destino no ambiente de preparo.  

5.  Os computadores de destino são entregues ao ambiente de produção para implantação.  

#### <a name="lti-oem-preload-processphase-3-complete-target-computer-deployment"></a>Processo de pré-carregamento de OEM LTI – Fase 3: concluir a implantação do computador de destino  
 A terceira e última fase do processo de pré-carregamento de OEM é executada no ambiente de produção da organização de implantação. Durante essa fase do processo, o computador de destino é iniciado e a imagem de uma mídia inicializável, colocada no disco rígido no ambiente de preparo durante a fase anterior, é iniciada.  

 **Para concluir a implantação do computador de destino no ambiente de produção**  

1.  Inicie o computador de destino.  

     O Windows PE é iniciado e, em seguida, o Assistente de Implantação do Windows.  

2.  Conclua o Assistente de Implantação do Windows usando as informações de configuração específicas para cada computador de destino.  

     Para obter mais informações sobre a conclusão desta etapa, consulte a seção “Executar o Assistente de Implantação”, no documento do MDT *Usando o Microsoft Deployment Toolkit*.  

 Quando essa fase estiver concluída, o computador de destino estará pronto para ser usado no ambiente de produção.  

## <a name="using-windows-powershell-to-perform-common-tasks"></a>Usando o Windows PowerShell para realizar tarefas comuns  
 As tarefas de administração do MDT no Deployment Workbench são realizadas por cmdlets subjacentes do Windows PowerShell, que podem ser usadas para automatizar tarefas administrativas, como aquelas indicadas nas seções a seguir.  

 Automatize a administração do MDT executando as seguintes etapas:  

-   Crie um novo compartilhamento de implantação, conforme descrito em [Criando um novo compartilhamento de implantação](#CreateNewDeployShare).  

-   Crie uma pasta em um compartilhamento de implantação, conforme descrito em [Criando uma pasta](#CreateFolder).  

-   Exclua uma pasta em um compartilhamento de implantação, conforme descrito em [Excluindo uma pasta](#DeleteFolder).  

-   Importe um driver de dispositivo para um compartilhamento de implantação, conforme descrito em [Importando um driver de dispositivo](#ImportDeviceDriver).  

-   Excluindo um driver de dispositivo em um compartilhamento de implantação, conforme descrito em [Excluindo um driver de dispositivo](#DeleteDeviceDriver).  

-   Importe um pacote de sistema operacional para um compartilhamento de implantação, conforme descrito em [Importando um pacote de sistema operacional](#ImportOpSysPackage).  

-   Excluindo um pacote do sistema operacional de um compartilhamento de implantação, conforme descrito em [Excluindo um pacote do sistema operacional](#DeleteOpSysPackage).  

-   Importe um sistema operacional para um compartilhamento de implantação, conforme descrito em [Importando um sistema operacional](#ImportOpSys).  

-   Excluindo um sistema operacional de um compartilhamento de implantação, conforme descrito em [Excluindo um sistema operacional](#DeleteOpSys).  

-   Crie um aplicativo em um compartilhamento de implantação, conforme descrito em [Criando um aplicativo](#CreateApplication).  

-   Exclua um aplicativo em um compartilhamento de implantação, conforme descrito em [Excluindo um aplicativo](#DeleteApplication).  

-   Crie uma sequência de tarefas em um compartilhamento de implantação, conforme descrito em [Criando uma sequência de tarefas](#CreateTaskSequence).  

-   Exclua uma sequência de tarefas de um compartilhamento de implantação, conforme descrito em [Excluindo uma sequência de tarefas](#DeleteTaskSequence).  

-   Crie um MDT DB, conforme descrito em [Criando um MDT DB](#CreateMDTDB).  

-   Crie um perfil de seleção, conforme descrito em [Criando um perfil de seleção](#CreateSelectProfile).  

-   Atualize o compartilhamento de implantação, conforme descrito em [Atualizando o compartilhamento de implantação](#UpdatingDeployShare).  

-   Crie um compartilhamento de implantação vinculado, conforme descrito em [Criando um compartilhamento de implantação vinculado](#CreateLinkedDeployShare).  

-   Atualize um compartilhamento de implantação vinculado, conforme descrito em [Atualizando um compartilhamento de implantação vinculado](#UpdatingLinkedDeployShare).  

-   Exclua um compartilhamento de implantação vinculado, conforme descrito em [Excluindo um compartilhamento de implantação vinculado](#DeleteLinkedDeployShare).  

-   Crie a mídia de implantação, conforme descrito em [Criando mídia](#CreateMedia).  

-   Gere a mídia de implantação, conforme descrito em [Gerando mídia](#GenerateMedia).  

-   Exclua uma mídia de implantação, conforme descrito em [Excluindo mídia](#DeleteMedia).  

###  <a name="CreateNewDeployShare"></a> Criando um novo compartilhamento de implantação  
 Os comandos do Windows PowerShell a seguir criam um novo compartilhamento de implantação em D:\Production Deployment Share chamado *Production$*. O novo compartilhamento de implantação será exibido no Deployment Workbench como produção.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "D:\Production Deployment Share" -Description "Production" -NetworkPath "\\Deployment_Server\Production$" -Verbose | add-MDTPersistentDrive -Verbose  
    ```  

###  <a name="CreateFolder"></a> Criando uma pasta  
 Os comandos do Windows PowerShell a seguir criam uma pasta do Adobe na árvore de console do Deployment Workbench em Deployment Workbench\/Deployment Shares\/Production\/Applications.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Applications" -enable "True" -Name "Adobe" -Comments "This folder contains Adobe software" -ItemType "folder" -Verbose remove-psdrive DS001 -Verbose  
    ```  

    > [!NOTE]
    >  Adicionar “`remove-psdrive`” ao script garante que o processo em segundo plano seja concluído antes de continuar.  

###  <a name="DeleteFolder"></a> Excluindo uma pasta  
 Os comandos do Windows PowerShell a seguir excluem a pasta Deployment Workbench\/Deployment Shares\/Production\/Applications\/Adobe.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Remove-item -path "DS002:\Applications\Adobe" -Verbose  
    ```  

> [!NOTE]
>  O script falhará se a pasta não estiver vazia.  

###  <a name="ImportDeviceDriver"></a> Importando um driver de dispositivo  
 Os comandos do Windows PowerShell a seguir importarão o driver de dispositivo do monitor Dell 2407 WFP para o compartilhamento de implantação de Produção.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtdriver -path "DS002:\Out-of-Box Drivers\Monitor" -SourcePath "D:\Drivers\Dell\2407 WFP" -Verbose  
    ```  

###  <a name="DeleteDeviceDriver"></a> Excluindo um driver de dispositivo  
 O comando do Windows PowerShell a seguir exclui o driver do monitor Dell 2407 WFP do compartilhamento de implantação de Produção.  

```  
Remove-item -path "DS002:\Out-of-Box Drivers\Dell Inc. Monitor 2407WFP.INF 1.0" -Verbose  
```  

###  <a name="ImportOpSysPackage"></a> Importando um pacote do sistema operacional  
 Os comandos do Windows PowerShell a seguir importam todos os pacotes do sistema operacional localizados em D:\\Updates\\Microsoft\\Vista. Esses pacotes do sistema operacional serão armazenados no compartilhamento de implantação de Produção, localizado em D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtpackage -path "DS002:\Packages" -SourcePath "D:\Updates\Microsoft\Vista" -Verbose  
    ```  

###  <a name="DeleteOpSysPackage"></a> Excluindo um pacote do sistema operacional  
 O comando do Windows PowerShell a seguir exclui o pacote do sistema operacional especificado do compartilhamento de implantação de Produção.  

```  
Remove-item -path "DS002:\Packages\Package_1_for_KB940105 neutral x86 6.0.1.0 KB940105" -Verbose  
```  

###  <a name="ImportOpSys"></a> Importando um sistema operacional  
 Os comandos do Windows PowerShell a seguir importam o sistema operacional Windows Vista localizado em D:\\Operating Systems\\Windows Vista x86. O sistema operacional será armazenado no compartilhamento de implantação de Produção, localizado em D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtoperatingsystem -path "DS002:\Operating Systems" -SourcePath "D:\Operating Systems\Windows Vista x86" -DestinationFolder "Windows Vista x86" -Verbose  
    ```  

###  <a name="DeleteOpSys"></a> Excluindo um sistema operacional  
 O comando do Windows PowerShell a seguir exclui o sistema operacional HOMEBASIC do Windows Vista do compartilhamento de implantação de Produção.  

```  
Remove-item -path "DS002:\Operating Systems\Windows Vista HOMEBASIC in Windows Vista x86 install.wim" -Verbose  
```  

###  <a name="CreateApplication"></a> Criando um aplicativo  
 Os comandos do Windows PowerShell a seguir criam o aplicativo Adobe Reader 9 usando arquivos de origem de D:\\Software\\Adobe\\Reader 9. O aplicativo será armazenado no compartilhamento de implantação de Produção, localizado em D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-MDTApplication -path "DS002:\Applications" -enable "True" -Name "Adobe Reader 9" -ShortName "Reader" -Version "9" -Publisher "Adobe" -Language "" -CommandLine "setup.exe" -WorkingDirectory ".\Applications\Adobe Reader 9" -ApplicationSourcePath "D:\Software\Adobe\Reader 9" -DestinationFolder "Adobe Reader 9" -Source ".\Applications\Adobe Reader 9" -Verbose  
    ```  

###  <a name="DeleteApplication"></a> Excluindo um aplicativo  
 O comando do Windows PowerShell a seguir exclui o aplicativo Adobe Reader 9 do compartilhamento de implantação de Produção.  

```  
Remove-item -path "DS002:\Applications\Adobe Reader 9" -Verbose  
```  

###  <a name="CreateTaskSequence"></a> Criando uma sequência de tarefas  
 Os comandos do Windows PowerShell a seguir criam a sequência de tarefas **Build de produção do Windows Vista** no compartilhamento de implantação de Produção, localizado em D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdttasksequence -path "DS002:\Task Sequences" -Name "Windows Vista Business Production Build" -Template "Client.xml" -Comments "Approved for use in the production environment.  This task sequence uses the Standard Client task sequence template" -ID "Vista_Ref" -Version "1.0" -OperatingSystemPath "DS002:\Operating Systems\Windows Vista BUSINESS in Windows Vista x86 install.wim" -FullName "Fabrikam User" -OrgName "Fabrikam" -HomePage "http://www.Fabrikam.com" -AdminPassword "secure_password" -Verbose  
    ```  

###  <a name="DeleteTaskSequence"></a> Excluindo uma sequência de tarefas  
 O comando do Windows PowerShell a seguir exclui a sequência de tarefas **Build de produção do Windows Vista** do compartilhamento de implantação de Produção.  

```  
Remove-item -path "DS002:\Task Sequences\Windows Vista Business Production Build" -force -Verbose  
```  

###  <a name="CreateMDTDB"></a> Criando um MDT DB  
 Os comandos do Windows PowerShell a seguir criam um novo MDT DB no servidor *deployment\_server* do compartilhamento de implantação de Produção. A conexão de banco de dados ocorrerá via TCP\/IP.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-MDTDatabase -path "DS002:" -SQLServer "DeploymentServer" -Netlib "DBMSSOCN" -Database "MDT2010" -SQLShare "DB_Connect" -Force -Verbose  
    ```  

###  <a name="CreateSelectProfile"></a> Criando um perfil de seleção  
 Os comandos do Windows PowerShell a seguir criam um novo perfil de seleção de Aplicativos.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Selection Profiles" -enable "True" -Name "Applications" -Comments "" -Definition "<SelectionProfile><Include path="Applications" /></SelectionProfile>" -ReadOnly "False" -Verbose  
    ```  

###  <a name="UpdatingDeployShare"></a> Atualizando um compartilhamento de implantação  
 Os comandos do Windows PowerShell a seguir atualizam um novo compartilhamento de implantação em D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  
    
-   ```
    Update\-MDTDeploymentShare \-path "DS002:" \-Verbose  
    ```
    
###  <a name="CreateLinkedDeployShare"></a> Criando um compartilhamento de implantação vinculado  
 Os comandos do Windows PowerShell a seguir criam um compartilhamento de implantação vinculado ao compartilhamento de implantação de Produção e reside no compartilhamento \\\\*remote\_server\_name*\\Deployment$. O perfil de seleção Tudo é usado para determinar qual conteúdo é replicado para o compartilhamento de implantação vinculado. O conteúdo do compartilhamento de implantação de Produção será mesclado com o conteúdo que já existe no compartilhamento \\\\*remote\_server\_name*\\Deployment$.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Linked Deployment Shares" -enable "True" -Name "LINKED001" -Comments "" -Root "\\RemoteServerName\Deployment$" -SelectionProfile "Everything" -Replace "False" -Verbose  
    ```  

###  <a name="UpdatingLinkedDeployShare"></a> Atualizando um compartilhamento de implantação vinculado  
 Os comandos do Windows PowerShell a seguir atualizam o compartilhamento de implantação LINKED001.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Replicate-MDTContent -path "DS002:\Linked Deployment Shares\LINKED001" -Verbose  
    ```  

###  <a name="DeleteLinkedDeployShare"></a> Excluindo um compartilhamento de implantação vinculado  
 Os comandos do Windows PowerShell a seguir excluem o compartilhamento de implantação LINKED001.  

-   Add\-PSSnapIn Microsoft.BDD.PSSnapIn  

-   ```  
    Remove-item -path "DS002:\Linked Deployment Shares\LINKED001" -Verbose  
    ```  

###  <a name="CreateMedia"></a> Criando mídia  
 Os comandos do Windows PowerShell a seguir criam uma pasta de origem que contém o conteúdo usado para criar uma mídia inicializável. O compartilhamento de implantação de Produção será usado como a origem. O perfil de seleção Tudo determina qual conteúdo é colocado na pasta de conteúdo de mídia. O arquivo LiteTouchMedia.iso será criado quando a mídia for gerada. A mídia será compatível com plataformas x86 e x64.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Media" -enable "True" -Name "MEDIA001" -Comments "some comment here" -Root "D:\Media" -SelectionProfile "Everything" -SupportX86 "True" -SupportX64 "True" -GenerateISO "True" -ISOName "LiteTouchMedia.iso" -Verbose  
    ```  

-   ```  
    New-PSDrive -Name "MEDIA001" -PSProvider "MDTProvider" -Root "D:\Media\Content" -Description "Embedded media deployment share" -Force -Verbose  
    ```  

###  <a name="GenerateMedia"></a> Gerando mídia  
 Os comandos do Windows PowerShell a seguir criam o arquivo LiteTouchMedia.iso em D:\\Media, que usará o conteúdo da pasta de origem de mídia MEDIA001.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Generate-MDTMedia -path "DS002:\Media\MEDIA001" -Verbose  
    ```  

###  <a name="DeleteMedia"></a> Excluindo mídia  
 O comando do Windows PowerShell a seguir exclui a mídia MEDIA001 do compartilhamento de implantação de Produção.  

```  
Remove-item -path "DS002:\Media\MEDIA001" -Verbos  
```  

## <a name="delaying-domain-join-to-avoid-application-of-group-policy-objects"></a>Atrasando o ingresso no domínio para evitar a aplicação de objetos de Política de Grupo  
 A Política de Grupo é uma tecnologia sofisticada e flexível que proporciona a capacidade de gerenciar com eficiência muitos computadores e objetos de usuário do AD DS (Active Directory Domain Services) por meio de um modelo um para muitos centralizado. As configurações da Política de Grupo são contidas em um GPO (objeto de Política de Grupo) e vinculadas a um ou mais contêineres de serviço do AD DS – sites, domínios e UOs (unidades organizacionais).  

 Algumas organizações têm configurações de Política de Grupo que são restritivas e podem causar problemas durante implantações de sistema operacional. Por exemplo, as configurações de Política de Grupo a seguir podem interromper um processo de logon automatizado:  

-   Restrições de logon automático  

-   Renomeando a conta de administrador  

-   Legendas e faixas legais  

-   Políticas de segurança restritivas (por exemplo, a política Segurança Especializada – Funcionalidade Limitada [SSLF])  

 Uma opção para resolver os problemas que pode causar um GPO durante a implantação é associar o computador no domínio o mais tarde possível no processo de implantação. Esse ingresso pode ser realizado usando uma etapa de sequência de tarefas personalizada que executa o script ZTIDomainJoin.wsf.  

 Para ingressar o computador de destino no domínio, o script de ZTIDomainJoin.wsf usa as propriedades **DomainAdmin**, **DomainAdminDomain**, **DomainAdminPassword**, **JoinDomain** e **MachineObjectOU**. Você pode declarar essas propriedades usando o Assistente de Implantação do Windows, as regras de compartilhamento de implantação, o MDT DB e regras de computador e coleção do Configuration Manager. A conta usada precisa ter os direitos necessários para criar e excluir objetos de computador no domínio.  

 Normalmente, o script ZTIConfigure.wsf atualiza o arquivo Unattend.xml ou Unattend.txt com os valores que especificam essas propriedades. Essas configurações são analisadas pelo programa de Instalação do Windows e o sistema tenta ingressar no domínio no início do processo de implantação. Isso aplica as configurações especificadas no GPOs de domínio ao computador de destino e pode causar falhas no processo de implantação.  

 Para atrasar intencionalmente o ingresso do computador de destino no domínio durante o processo de implantação, remova certos elementos do arquivo Unattend.xml. O script ZTIConfigure.wsf ignorará as propriedades de gravação no arquivo Unattend.xml se o elemento de propriedade associado estiver ausente do arquivo.  

> [!NOTE]
>  Esta solução alternativa de exemplo só é válida ao implantar os sistemas operacionais Windows 7, Windows Server 2008 ou Windows Server 2008 R2.  

 **Prepare o arquivo unattend.xml para que o computador de destino não tente ingressar no domínio durante a Instalação do Windows**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação* /Task Sequences/*sequência_de_tarefas* (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação e *sequência_de_tarefas* ao nome da sequência de tarefas a serem configurados).  

3.  No painel Ações, clique em **Propriedades**.  

4.  Na guia **Informações do sistema operacional**, clique em **Editar Unattend.xml**.  

     O Windows SIM (Gerenciador de Imagem de Sistema do Windows) é iniciado.  

5.  No painel **Arquivo de Resposta**, acesse **4 specialize/Identification/Credentials**. Clique com o botão direito do mouse em **Credenciais** e clique em **Excluir**.  

6.  Clique em **Sim**.  

7.  Salve o arquivo de resposta e, em seguida, saia do Windows SIM.  

8.  Clique em **OK** na caixa de diálogo **Propriedades** da sequência de tarefas.  

 Com os elementos `Credentials` ausentes do arquivo unattend.xml, o script ZTIConfigure.wsf não é capaz de popular as informações de ingresso no domínio no arquivo Unattend.xml, que impedirá que a Instalação do Windows tente ingressar no domínio.  

 **Para adicionar uma etapa da sequência de tarefas que ingressa o computador de destino no domínio**  

1.  Clique em **Iniciar** e aponte para **Todos os Programas**. Aponte para **Microsoft Deployment Toolkit** e clique em **Deployment Workbench**.  

2.  Na árvore de console do Deployment Workbench, acesse Deployment Workbench/Deployment Shares/*compartilhamento_de_implantação* /Task Sequences/*sequência_de_tarefas* (em que *compartilhamento_de_implantação* refere-se ao nome do compartilhamento de implantação e *sequência_de_tarefas* ao nome da sequência de tarefas a serem configurados).  

3.  No painel Ações, clique em **Propriedades**.  

4.  Na guia **Sequência de Tarefas**, acesse o nó Restauração de Estado e expanda-o.  

5.  Verifique se a etapa da sequência de tarefas **Recuperar do domínio** existe. Em caso afirmativo, vá para a etapa 9.  

6.  Na caixa de diálogo **Propriedades** da sequência de tarefas, clique em **Adicionar**, acesse **Configurações** e clique em **Recuperar do Domínio**.  

7.  Adicione a etapa da sequência de tarefas **Recuperar do domínio** ao editor de sequência de tarefas. Verifique se a etapa está no local desejado na sequência de tarefas.  

8.  Verifique se as configurações da etapa da sequência de tarefas **Recuperar do Domínio** estão devidamente definidas para atender às suas necessidades.  

9. Clique em **OK** na caixa de diálogo **Propriedades** da sequência de tarefas para salvá-la.
