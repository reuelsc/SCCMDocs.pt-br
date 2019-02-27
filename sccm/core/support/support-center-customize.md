---
title: Personalizar o Centro de Suporte
titleSuffix: Configuration Manager
description: Personalizar o arquivo de configuração do Centro de Suporte.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a6f7f6b7-9ef3-4ffa-a3cf-d877ac55983b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b100daf91b8bb7c5d4dd5f041c57e7dc9dac390e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156773"
---
# <a name="customize-support-center"></a>Personalizar o Centro de Suporte

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A ferramenta [Centro de Suporte](/sccm/core/support/support-center) inclui um arquivo de configuração que você pode personalizar. Por padrão, quando você instala o Centro de Suporte, esse arquivo está no seguinte caminho: `C:\Program Files (x86)\Configuration Manager Support Center\ConfigMgrSupportCenter.exe.config`. O arquivo de configuração muda o comportamento do programa:

  - [Personalizar a coleta de dados](#bkmk_datacoll): edite os conjuntos de chaves do Registro e os namespaces do WMI que ele inclui durante a coleta de dados  

  - [Personalizar grupos de log](#bkmk_loggroups): defina novos grupos de arquivos de log usando expressões regulares. Também adicione outros arquivos de log a grupos de log.  

  - [Coletar arquivos de log adicionais usando caracteres curinga:](#bkmk_wildcards): use pesquisas curinga para coletar arquivos de log adicionais  

Para fazer essas alterações, você precisa ter permissões administrativas locais no cliente no qual instalou o Centro de Suporte. Faça essas personalizações usando um editor de texto ou XML, como o Bloco de Notas ou o Visual Studio.

> [!Important]  
> O arquivo de configuração do Centro de Suporte é um arquivo de formato XML. É essencial para a operação do Centro de Suporte. Modificar esse arquivo só é recomendado para usuários que estão familiarizados com XML e expressões regulares.  

Antes de personalizar o arquivo de configuração do Centro de Suporte, salve um backup do original. Esse backup permitirá que você recupere a funcionalidade do Centro de Suporte original se cometer erros ao editar o arquivo. Se você não criar um backup e o Centro de Suporte não funcionar corretamente depois de modificar o arquivo de configuração, reinstale o Centro de Suporte. Você também pode copiar um arquivo de configuração de outra instalação do Centro de Suporte.



## <a name="bkmk_datacoll"></a> Personalizar a coleta de dados

Para personalizar a coleta de dados no cliente, modifique o arquivo de configuração do Centro de Suporte usando elementos XML contidos no elemento `<dataCollectorSettings>`.


### <a name="wmi-data-collection"></a>Coleta de dados do WMI

O elemento `<CcmWmiDataCollector>` contém um elemento `<collectionScopes>`. Use esse elemento para alterar os namespaces do WMI do qual o Centro de Suporte coleta dados. Ele também inclui um elemento `<ignoreScopes>`. Use esse elemento para filtrar a coleta de dados de partes de namespaces definidos no elemento `<collectionScopes>`.  
    
#### <a name="example"></a>Exemplo
O arquivo de configuração padrão coleta dados do namespace `root\ccm`. Ele inclui esse caminho em um elemento `<add/>` no `<collectionScopes>`. 

Ele também ignora tudo sob os caminhos `\cimodels`, `\invagt`, `\events` e `\policy` para este namespace. Ele inclui esses caminhos em elementos `<add/>` contidos no `<ignoreScopes>`.

```XML
<CcmWmiDataCollector>
  <collectionScopes>
    <!-- Collect these namespaces (ignoring the sub-scopes in the ignoreScopes block) -->
    <add key="root\ccm"/>
    <add key="root\cimv2\sms"/>
  </collectionScopes>
  <ignoreScopes>
    <!-- Collecting these namespaces is known to be problematic/unnecessary -->
    <add key="root\ccm\cimodels"/>
    <add key="root\ccm\invagt"/>
    <add key="root\ccm\events"/>
    <!-- Do not collect policy, there's already a separate policy collector.-->
    <add key="root\ccm\policy"/>
  </ignoreScopes>
</CcmWmiDataCollector>
```


### <a name="registry-data-collection"></a>Coleta de dados do Registro

O elemento `<RegistryDataCollector>` contém um elemento `<registryKeys>`. Use esse elemento para alterar as chaves e as subchaves de Registro que esse Centro de Suporte coleta no caminho `HKEY_LOCAL_MACHINE`. O Centro de Suporte não dá suporte à coleta de dados de Registro de outros caminhos de Registro raiz.

#### <a name="example"></a>Exemplo
Para coletar chaves do Registro para os programas clássicos instalados no dispositivo, adicione o seguinte elemento `<add/>` no elemento `<registryKeys>`: `<add key="software\\microsoft\\windows\\currentversion\\uninstall"/>`

```XML
<RegistryDataCollector>
  <registryKeys>
    <!-- Registry keys (and all subkeys) to collect -->
    <add key="software\\microsoft\\ccm"/>
    <add key="software\\microsoft\\sms"/>
    <add key="software\\microsoft\\ccmsetup"/>
    <add key="software\\microsoft\\windows\\currentversion\\uninstall"/>
  </registryKeys>
</RegistryDataCollector>
```



## <a name="bkmk_loggroups"></a> Personalizar grupos de arquivos de log

Para personalizar que arquivos de log o Centro de Suporte coleta e como ele os representa na lista **Grupos de log**, use elementos no elemento `<logGroups>`. Quando você iniciar o Centro de suporte, ele examinará esta seção do arquivo de configuração. Ele então criará um grupo na lista **Grupos de log** para cada valor de atributo de chave exclusivo encontrado nos elementos `<add/>` contidos no elemento `<logGroups>`.

  - **Grupo de logs de componente**: o elemento `<componentLogGroup>` usa um atributo de chave para definir o nome do grupo de log exibido na lista. Ele também usa um atributo de valor que contém uma regex (expressão regular). Ele usa essa regex para coletar um conjunto de arquivos de log relacionados.  

  - **Grupo de log estático:** o elemento `<staticLogGroup>` usa um atributo de chave para definir o nome do grupo de log exibido na lista. Ele também usa um atributo de valor que define um nome de arquivo de log.  

Se o mesmo valor de atributo de chave for usado em um elemento `<add/>` dentro dos elementos `<componentLogGroup>` e do elemento `<staticLogGroup>`, o Centro de Suporte criará um único grupo. Esse grupo inclui os arquivos de log definidos por ambos os elementos que usam a mesma chave.

#### <a name="example"></a>Exemplo
```XML
<logGroups>
  <componentLogGroup>
    <add key="Application Management" value="^(app.*|ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|execmgr.*|UserAffinity.*|.*Handler$|.*Provider$)"/>
    <add key="Client Registration" value="^(clientregistration|locationservices|ccmmessaging|ccmexec)"/>
    <add key="Inventory" value="^(ccmmessaging|inventoryagent|mtrmgr|swmtrreportgen|virtualapp|mtr.*|filesystemfile)"/>
    <add key="Policy" value="^(ccmmessaging|policyagent_.*|policyevaluator_.*)"/>
    <add key="Software Updates" value="^(ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|update.*|wuahandler|xmlstore|scanagent)"/>
    <add key="Software Distribution" value="^(datatransferservice|execmgr.*|contenttransfermanager|locationservices|contentaccess|filebits)"/>
    <add key="Desired Configuration Management" value="^(ci.*|dcm.*)"/>
    <add key="Operating System Deployment" value="^(ts.*)"/>
  </componentLogGroup>
  <staticLogGroup>
    <add key="Application Management" value="ccmsdkprovider.log"/>
    <add key="Desired Configuration Management" value="ccmsdkprovider.log"/>
    <add key="Software Updates" value="ccmsdkprovider.log"/>
  </staticLogGroup>
</logGroups>
```



## <a name="bkmk_wildcards"></a> Coletando arquivos de log adicionais usando caracteres curinga

Para coletar arquivos de log adicionais, use curingas no caminho do arquivo ou no nome de arquivo. Esses caracteres curinga incluem variáveis de ambiente de todo o sistema, como `%WINDIR%`, mas excluem variáveis de ambiente no escopo do usuário, como `%USERPROFILE%`. Para coletar arquivos de log adicionais usando essa pesquisa de arquivo de log não-recursivo, use um elemento `<add/>` dentro do elemento `<additionalLogFiles>`. 

Estes exemplos mostram como o Centro de Suporte usa esse recurso no arquivo de configuração padrão.

#### <a name="example-1-collect-all-windows-update-log-files-in-the-windows-directory"></a>Exemplo 1: coletar todos os arquivos de log do Windows Update no diretório do Windows
O elemento a seguir coleta qualquer arquivo chamado `WindowsUpdate.log` encontrado no diretório do Windows: 

`<add key="%WINDIR%\WindowsUpdate.log" />`

#### <a name="example-2-collect-all-log-files-in-the-windows-logs-directory"></a>Exemplo 2: coletar todos os arquivos de log no diretório de Logs do Windows
O seguinte elemento coleta qualquer arquivo que termine em `.log` localizado no diretório de logs do Windows: 

`<add key="%WINDIR%\logs\*.log" />`

#### <a name="full-example-xml"></a>XML de exemplo completo
```XML
<CcmLogDataCollector>
  <additionalLogFiles>
    <!-- Collect these additional log files. Can pass in a wildcard for the filename. System variables are also supported. -->
    <!--
    <add key="%WINDIR%\WindowsUpdate.log" />
    <add key="%WINDIR%\logs\*.log" />
    -->
  </additionalLogFiles>
</CcmLogDataCollector>
```
