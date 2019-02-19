---
title: Como usar o plug-in de conversão
titleSuffix: Configuration Manager
description: Use o plug-in do Gerenciador de Conversão de Pacotes para personalizar os processos de análise e conversão.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 83cf156c-36de-483f-a9e6-2e06158f3b20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1d76b43a1918184fea9cc97bb3ed35a57a7c7ada
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126044"
---
# <a name="how-to-use-the-package-conversion-manager-plug-in"></a>Como usar o plug-in do Gerenciador de Conversão de Pacotes

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

<!--1357861-->

O plug-in Gerenciador de Conversão de Pacotes ajuda a personalizar os processos de análise e conversão. Para usar o plug-in do Gerenciador de Conversão de Pacotes, grave um arquivo executável ou de script que realize operações personalizadas. Em seguida, edite o arquivo de configuração, Microsoft.ConfigurationManagement.exe.config, para chamar o executável ou script. As linguagens mais comuns usadas para gravar o script são VBScript ou PowerShell.

O plug-in do Gerenciador de Conversão de Pacotes é executado uma vez para cada pacote. Se você analisar ou converter vários pacotes de uma vez, o plug-in do Gerenciador de Conversão de Pacotes será executado a cada vez.

> [!NOTE]  
> Para saber mais sobre os elementos do Gerenciador de Conversão de Pacotes no arquivo de configuração do Configuration Manager, confira [Referência técnica para o XML de configuração de plug-in do Gerenciador de Conversão de Pacotes](/sccm/apps/pcm/plugin-config-xml).



## <a name="default-process"></a>Processo padrão

Por padrão, o Gerenciador de Conversão de Pacotes realiza as seguintes ações:

1.  Leitura de um pacote do Configuration Manager.  

2.  Criação de um aplicativo do pacote e adicione atributos padrão.  

3.  Análise do aplicativo e determinação do status de preparação de um pacote.  

4.  Execute uma das ações a seguir, dependendo da operação do Gerenciador de Conversão de Pacotes:  

    - **Analisar**: exiba o estado de preparação do pacote no console do Configuration Manager.  

    - **Converter**: grave o aplicativo no banco de dados do Configuration Manager.  


## <a name="plug-in-based-process"></a>Processo baseado em plug-in 

Quando você usa o plug-in, o Gerenciador de Conversão de Pacotes realiza as seguintes ações:

1.  Leitura de um pacote do Configuration Manager.  

2.  Criação de um aplicativo do pacote e adicione atributos padrão.  

3.  Conversão do aplicativo para XML. Armazenamento do arquivo no disco.  

4.  Execução do script de plug-in para modificar o XML do aplicativo. Para saber mais, confira [Referência técnica para o XML de configuração de plug-in do Gerenciador de Conversão de Pacotes](/sccm/apps/pcm/plugin-config-xml).  

5.  Conversão do XML do aplicativo em um aplicativo do Configuration Manager.  

6.  Análise do aplicativo e determinação do status de preparação de um pacote.  

7.  Execute uma das seguintes ações, dependendo da operação do Gerenciador de Conversão de Pacotes:  

    - **Analisar**: exiba o estado de preparação do pacote no console do Configuration Manager.  

    - **Converter**: grave o aplicativo no banco de dados do Configuration Manager.  



## <a name="see-also"></a>Consulte também

[Referência técnica para o XML de configuração de plug-in do Gerenciador de Conversão de Pacotes](/sccm/apps/pcm/plugin-config-xml)
