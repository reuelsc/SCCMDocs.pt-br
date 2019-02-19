---
title: XML do plug-in de configuração
titleSuffix: Configuration Manager
description: Referência técnica para elementos XML do plug-in do Gerenciador de Conversão de Pacotes.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 940cc075-4066-44d5-972a-927c0b0a1143
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: dffa07009c253401c2ef15bdd2d3b37722deb450
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126262"
---
# <a name="technical-reference-for-the-package-conversion-manager-plug-in-configuration-xml"></a>Referência técnica para o XML de configuração de plug-in do Gerenciador de Conversão de Pacotes

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

<!--1357861-->

Este tópico descreve os elementos XML no arquivo de configuração (Microsoft.ConfigurationManagement.exe.config) que controlam a operação do plug-in do Gerenciador de Conversão de Pacotes. Para saber mais sobre como usar esse plug-in, confira [Como usar o plug-in do Gerenciador de Conversão de Pacotes](/sccm/apps/pcm/how-to-use-plug-in).



## <a name="xml-configuration-elements"></a>Elementos de configuração de XML

A tabela a seguir descreve os elementos XML no arquivo de configuração do Configuration Manager relacionados ao plug-in Gerenciador de Conversão de Pacotes.

|Elemento  |Digite  |Descrição  |
|---------|---------|---------|
|**PcmPlugIn**|Cadeia de caracteres|O nome do script ou do executável a ser usado como o plug-in do Gerenciador de Conversão de Pacotes.|
|**PcmPlugInTimeoutMilliseconds**|Inteiro|A quantidade máxima de tempo, em milissegundos, para aguardar até que o script ou o executável de plug-in do Gerenciador de Conversão de Pacotes conclua o processamento de um pacote.|
|**PcmPluginExitCode**|Inteiro|O código de saída esperado do processo de plug-in. Este valor indica êxito. Todos os outros códigos são considerados um erro.|
|**ForceRequirementsExtraction**|Booliano|Permita que a conversão automática use os requisitos de coleção associados a um pacote. Isso deve ser apenas definido como True ao trabalhar com um plug-in do Gerenciador de Conversão de Pacotes que foi projetado para tomar decisões sobre quais requisitos serão usados.|



## <a name="sample-configuration-xml"></a>XML de configuração de exemplo

Esta seção fornece um exemplo dos elementos XML de configuração do Gerenciador de Conversão de Pacotes, no arquivo de configuração do Gerenciador de Conversão de Pacotes, **Microsoft.ConfigurationManagement.exe.config**. Por padrão, esse arquivo está neste caminho:  
`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

No exemplo, os elementos relacionados ao Gerenciador de Conversão de Pacotes estão dentro do elemento a seguir: `Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings`

``` XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
...
    </Microsoft.ConfigurationManagement.AdminConsole.Properties.Settings>
    <Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
      <setting name="DecisionVerbosity" serializeAs="String">
        <value>2</value>
      </setting>
      <setting name="PcmPlugIn" serializeAs="String">
        <value>pcmplugin.vbs</value>
      </setting>
      <setting name="PcmPlugInTimeoutMilliseconds" serializeAs="String">
        <value>10000</value>
      </setting>
      <setting name="PcmPluginExitCode" serializeAs="String">
        <value>0</value>
      </setting>
      <setting name="ForceRequirementsExtraction" serializeAs="String">
        <value>True</value >
      </setting>
    </Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
  </applicationSettings>
...
```

