---
title: "Comandos prestart para mídia de sequência de tarefas"
titleSuffix: Configuration Manager
description: "Crie um script para usar o comando prestart, distribuir o conteúdo associado a esse comando e configurar o comando prestart na mídia."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ccc9f652-2953-4c38-8a90-c799484105ca
caps.latest.revision: "6"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 3a1b39bb988d305c02d85ef168789d081637c084
ms.sourcegitcommit: 08f9854fb6c6d21e1e923b13e38a64d0bc2bc9a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/12/2017
---
# <a name="prestart-commands-for-task-sequence-media-in-system-center-configuration-manager"></a>Comandos prestart para mídia de sequência de tarefas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode criar um comando prestart no System Center Configuration Manager para usar com a mídia de inicialização, a mídia autônoma e a mídia pré-configurada. O comando prestart é um script ou executável que é executado antes da seleção da sequência de tarefas e pode interagir com o usuário no Windows PE. O comando prestart pode solicitar informações a um usuário e salvá-lo no ambiente da sequência de tarefas ou consultar uma variável da sequência de tarefas para obter informações. Quando o computador de destino se inicializa, a linha de comando é executada antes de a política ser baixada do ponto de gerenciamento. Use os procedimentos a seguir para criar um script para usar o comando prestart, distribuir o conteúdo associado a esse comando e configurar o comando prestart na mídia.  

## <a name="create-a-script-file-to-use-for-the-prestart-command"></a>Criar um arquivo de script a ser usado para o Comando Prestart  
 As variáveis de sequência de tarefas podem ser lidas e gravadas usando o objeto COM do Microsoft.SMS.TSEnvironment enquanto a sequência de tarefas está em execução. O exemplo a seguir ilustra um arquivo de script do Visual Basic que consulta a variável da sequência de tarefas _SMSTSLogPath para obter o local do log atual. O script também define uma variável personalizada.  

```  
dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")  
dim logPath  
' You can query the environment to get an existing variable.  
logPath = env("_SMSTSLogPath")  
' You can also set a variable in the OSD environment.  
env("MyCustomVariable") = "varname"  
```  

## <a name="create-a-package-for-the-script-file-and-distribute-the-content"></a>Criar um pacote para o arquivo de script e distribuir o conteúdo  
 Depois de criar o script ou executável para o comando prestart, você deverá criar uma origem do pacote para hospedar os arquivos do script ou executável, criar um pacote para os arquivos (nenhum programa necessário) e distribuir o conteúdo para um ponto de distribuição.  

 Para obter mais informações sobre a criação de pacotes, consulte [Pacotes e programas](../../apps/deploy-use/packages-and-programs.md).  

 Para obter mais informações sobre como distribuir conteúdo, consulte [Distribuir conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

## <a name="configure-the-prestart-command-in-media"></a>Configurar o comando prestart na mídia  
 Você pode configurar o comando prestart no Assistente para Criar Mídia de Sequência de Tarefas para mídia autônoma, mídia inicializável ou mídia em pré-teste. Para obter mais informações sobre os tipos de mídia, consulte [Criar mídia da sequência de tarefas](../deploy-use/create-task-sequence-media.md). Use o procedimento a seguir para criar um comando prestart na mídia.  

#### <a name="to-create-a-prestart-command-in-media"></a>Para criar um comando prestart na mídia  

1.  No console do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho **Biblioteca de Software** , expanda **Sistemas Operacionais**e clique em **Sequências de Tarefas**.  

3.  Na guia **Início** , no grupo **Criar** , clique em **Criar Mídia de Sequência de Tarefas** para iniciar o Assistente para Criar Mídia de Sequência de Tarefas.  

4.  Na página **Selecionar Tipo de Mídia** , selecione **Mídia autônoma**, **Mídia inicializável**ou **Mídia em pré-teste**e clique em **Próximo**.  

5.  Navegue até a página **Personalização** do assistente. Para obter mais informações sobre como configurar as outras páginas no assistente, consulte [Criar mídia da sequência de tarefas](../deploy-use/create-task-sequence-media.md).  

6.  Na página **Personalização** , especifique as informações a seguir e clique em **Próxima**.  

    -   Selecione **Habilitar comando prestart**.  

    -   Na caixa de texto **Linha de comando** , insira o script ou executável que você criou para o comando prestart.  

        > [!IMPORTANT]  
        >  Use **cmd /C <comando prestart\>** para especificar o comando prestart. Por exemplo, se você usou TSScript.vbs como o nome do script do comando prestart, você inseriria **cmd /C TSScript.vbs** na linha de comando. Em que **cmd /C** abre uma nova janela do interpretador de comandos do Windows e usa a variável de ambiente Path para encontrar o script ou executável do comando prestart. Você também pode especificar o caminho completo do comando prestart, mas a letra da unidade pode ser diferente em computadores com configurações de unidade diferentes.  

    -   Selecione **Incluir arquivos para o comando prestart**.  

    -   Clique em **Definir** para selecionar o pacote que está associado aos arquivos do comando prestart.  

    -   Clique em **Procurar** para selecionar o ponto de distribuição que hospeda o conteúdo para o comando prestart.  

7.  Conclua o assistente.  
