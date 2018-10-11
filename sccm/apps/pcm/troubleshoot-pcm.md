---
title: Solução de problemas do Gerenciador de Conversão de Pacotes
titleSuffix: Configuration Manager
description: Saiba como solucionar problemas com o Gerenciador de Conversão de Pacotes no Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cb616925-bb94-4b7c-a867-b3d95aef4d5e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fdcd31ec5a2fc5fbba12145115b46b2fbe8d4edd
ms.sourcegitcommit: 759098de944b8f7d5eedfc2bae2cb9a6ba15276f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43297166"
---
# <a name="troubleshoot-package-conversion-manager"></a>Solução de problemas do Gerenciador de Conversão de Pacotes

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

<!--1357861-->

Use as informações neste artigo para ajudar você a solucionar problemas ao usar o Gerenciador de Conversão de Pacotes.



## <a name="sms-provider"></a>Provedor de SMS

O Gerenciador de Conversão de Pacotes usa o Provedor de SMS. Para obter mais informações, veja [Planejar para o provedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).

Se o Provedor de SMS não está funcionando corretamente, o console do Configuration Manager, incluindo o Gerenciador de Conversão de Pacotes, não funcionará.



## <a name="package-readiness"></a>Preparação de pacote

Antes de converter um pacote em um aplicativo, analise o pacote usando a função **Analisar** do Gerenciador de Conversão de Pacotes. Após a análise, adicione a coluna **Preparação** ao nó **Pacotes** do console do Configuration Manager. A lista de pacotes exibe um dos seguintes estados de preparação do pacote analisado:

 - **Automática**: o pacote pode ser convertido diretamente com a função **Converter**.      

    > [!NOTE]  
    > Uma conversão automática não converte as consultas WQL em requisitos do aplicativo. Use o processo **Corrigir e Converter** para converter essas consultas.  

 - **Manual**: o pacote precisa de algumas adições ou alterações antes que você possa convertê-lo usando a função **Corrigir e Converter**.  

 - **Não Aplicável**: o pacote não é adequado para conversão. Corrija os problemas com o pacote ou continue a implantá-lo como um pacote.  

 - **Erro**: o pacote contém erros. Corrija esses erros manualmente antes de analisar e convertê-lo.  

O painel de detalhes do nó **Pacotes** no console do Configuration Manager mostra quaisquer problemas de preparação. Selecione um pacote e, depois, selecione a guia **Resumo** no painel de detalhes.



## <a name="log-files"></a>Arquivos de log

### <a name="enable-logging"></a>Habilitar o registro em log

Quando você habilita o registro em log para o Gerenciador de Conversão de Pacotes, ele registra todas as suas ações, exceções e erros. 

Para habilitar o registro em log nesse componente no Configuration Manager, modifique **Microsoft.ConfigurationManagement.exe.Config**. Por padrão, esse arquivo de configuração está localizado neste caminho:  
`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`  

Insira os seguintes elementos XML **switches** e **trace** no elemento **system.diagnostics** após o último elemento **fontes**:

``` XML
</sources>

    <switches>
      <add name="PcmLogging" value="3"/>
    </switches>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <add name="PcmTraceListener" type="Microsoft.ConfigurationManagement.UserCentric.Logging.RolloverLogTraceListener, Microsoft.ConfigurationManagement.UserCentric.Logging" initializeData="%UserProfile%\AppData\Local\Temp\PcmTrace.log"/>
      </listeners>
    </trace>

</system.diagnostics>
```

Este exemplo usa o arquivo **PCMTrace.log**. Este registro está no computador que executa o console do Configuration Manager neste caminho:  
`%UserProfile%\AppData\Local\Temp`

Para configurar o nível de detalhes, altere configuração de alternância de rastreamento **PcmLogging**. Defina esse valor como quatro níveis de detalhes, do menos detalhado (`1`) para o mais detalhado (`4`).


### <a name="smsprovlog"></a>SMSProv.log

Em algumas situações, as informações relevantes para a solução de problemas no processo de conversão de pacote estarão no arquivo do **SMSProv.log**. Esse arquivo captura informações do provedor de SMS do Configuration Manager.

Por padrão, esse arquivo de log está localizado no servidor do site do Configuration Manager no seguinte caminho:  
`C:\Program Files\Microsoft Configuration Manager\Logs`

Se você vir uma destas mensagens de erro, o arquivo **SMSProv.log** poderá conter informações de solução de problemas relevantes:

- `The SMS Provider reported an error`

- `Generic Failure`

Estas mensagens de erro geralmente indicam que ocorreu um erro no servidor do site e que as informações de erro não foram enviadas para o console do Gerenciador de Conversão de Pacote.

Saiba mais em [Referência técnica para mensagens de erro do Gerenciador de Conversão de Pacotes](/sccm/apps/pcm/error-messages).



## <a name="changing-package-attributes-after-analysis"></a>Alterando atributos de pacote após análise

Depois que um pacote for analisado e tiver um estado de preparação de **Automático** ou **Manual**, o processo de conversão poderá falhar se qualquer um dos atributos relevantes for alterado.

Por exemplo, você analisa um pacote e seu estado de preparação é **Automático**. Depois, você adiciona outro programa ao pacote. A conversão do pacote pode falhar.

Se você precisar fazer alterações a um pacote após a análise, execute novamente a análise antes da conversão. 



## <a name="see-also"></a>Consulte também

[Referência técnica para mensagens de erro do Gerenciador de Conversão de Pacotes](/sccm/apps/pcm/error-messages)