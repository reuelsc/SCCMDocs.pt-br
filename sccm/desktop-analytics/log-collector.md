---
title: Coletor de logs
titleSuffix: Configuration Manager
description: Use a ferramenta coletor de logs para ajudar a solucionar problemas do desktop Analytics
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 349b2a69-af46-481f-afb2-24d98774e852
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e99899ba9b12416e9549f88c7bc3b72fc09c6c28
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68537634"
---
# <a name="desktop-analytics-log-collector"></a>Coletor de logs do desktop Analytics

A partir do Configuration Manager versão 1906, use a ferramenta **DesktopAnalyticsLogsCollector. ps1** do diretório de instalação do Configuration Manager para ajudar a solucionar problemas de registro de dispositivo do desktop Analytics. Ele executa algumas etapas básicas de solução de problemas e coleta os logs relevantes em um único diretório de trabalho. Você pode compartilhar esse conteúdo com o suporte da Microsoft.


## <a name="prerequisites"></a>Pré-requisitos

- Um cliente de análise de desktop que executa o Windows 10, Windows 8.1 ou Windows 7 com Service Pack 1

- Execute o script no dispositivo como um usuário administrativo e **execute como administrador**.

    > [!Tip]
    > Você pode usar o recurso de **Scripts** Configuration Manager com essa ferramenta. Para obter mais informações, [consulte o exemplo 5: Implantar script por meio de **Scripts**](#bkmk_ex5)Configuration Manager.

- PowerShell versão 4,0 ou posterior
    - .NET Framework versão 4,6 ou posterior
    - Windows Management Framework versão 4,0 ou posterior

## <a name="usage"></a>Uso

Obtenha o script do conteúdo de instalação do Configuration Manager:`SMSSETUP\TOOLS\DesktopAnalyticsLogsCollector\DesktopAnalyticsLogsCollector.ps1`

```
DesktopAnalyticsLogsCollector.ps1
    [-LogPath] <String>
    [-LogMode] <Int16>
    [-CollectNetTrace] <Int16>
    [-CollectUTCTrace] <Int16>
```

## <a name="parameters"></a>Parâmetros

### `-LogPath`

Especifica um caminho local ou UNC para colocar o log e outros arquivos de saída.

**Valores**:

- Caminho local (comprimento máximo = 130), por exemplo:`c:\myfolder`

- Caminho UNC (comprimento máximo = 130), por exemplo:`\\myserver\myfolder`

**Tipo**: Cadeia de caracteres

**Posição**: 1

**Valor padrão**: `$Env:SystemDrive\M365AnalyticsLogs`(Quando esse parâmetro é nulo, vazio ou espaço em branco, o script cria a pasta M365AnalyticsLogs na unidade do sistema.)

### `-LogMode`

Especifica o nível detalhado dos logs.

**Valores**:

- `0`: Registrar mensagens de script somente na janela de comando do PowerShell.

- `1`: Registre mensagens de script em ambos os arquivos de log na pasta de saída e na janela de comando do PowerShell.

- `2`: Registre mensagens de script no arquivo de log somente na pasta de saída.

**Tipo**: Int16

**Posição**: 2

**Valor padrão**: `1`(Registrar mensagens de script no arquivo de log e na janela de comando do PowerShell.)

### `-CollectNetTrace`

Especifica se o script coleta o rastreamento de rede.

**Valores**:

- `0`: Não habilite o rastreamento de rede.

- `1`(qualquer valor inteiro diferente de zero): Habilite o rastreamento de rede e colete os resultados.

**Tipo**: Int16

**Posição**: 3

**Valor padrão**: `0`(Não habilite o rastreamento de rede)

### `-CollectUTCTrace`

Especifica se o script coleta o rastreamento UTC do Windows e executa o diagnóstico de conectividade.

**Valores**:

- `0`: Não habilite o rastreamento UTC ou execute o diagnóstico de conectividade.

- `1`(qualquer valor inteiro diferente de zero): Habilite o rastreamento UTC, execute diagnóstico de conectividade e colete os resultados.

**Tipo**: Int16

**Posição**: 4

**Valor padrão**: `0`(Não habilite o rastreamento UTC ou execute o diagnóstico de conectividade)


## <a name="output"></a>Saída

O script cria uma *pasta de trabalho* no caminho especificado. Por exemplo, **M365AnalyticsLogs_yy_MM_dd_HH_mm_ss**. Ele coloca todos os seus arquivos de saída nessa pasta de trabalho.

Se você habilitar o script para gravar em um *arquivo de log*, ele gerará um na pasta de trabalho. Por exemplo, **M365AnalyticsLogs_ yy_MM_dd_HH_mm_ss. txt**.

O script também gera outros *arquivos de diagnóstico* na pasta de trabalho. Por exemplo:

- `installedKBs.txt`: uma lista de atualizações do Windows instaladas no dispositivo
- `appcompat`: dados de compatibilidade de aplicativos
- `Reg*.txt`: uma série de arquivos com dados exportados do registro do Windows


## <a name="examples"></a>Exemplos

### <a name="bkmk_ex1"></a>Exemplo 1: Executar o script por meio da janela de comando do PowerShell com valores padrão

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1
```

### <a name="bkmk_ex2"></a>Exemplo 2: Executar o script por meio da janela de comando do PowerShell com parâmetros especificados

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogPath "c:\testABC" -LogMode 0 -CollectNetTrace 0 -CollectUTCTrace 0
```

### <a name="bkmk_ex3"></a>Exemplo 3: Executar o script por meio da janela de comando do PowerShell com os parâmetros especificados na posição

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 "c:\testABC" 2 0 0
```

### <a name="bkmk_ex4"></a>Exemplo 4: Executar o script por meio da janela de comando do PowerShell com o parâmetro e as mensagens detalhadas especificadas

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogMode 1 -Verbose
```

### <a name="bkmk_ex5"></a>Exemplo 5: Implantar script via **scripts** de Configuration Manager

Para saber mais, confira [Criar e executar scripts do PowerShell do console do Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).

DesktopAnalyticsLogsCollector. ps1 é assinado digitalmente pela Microsoft. Talvez seja necessário adicionar seu certificado de assinatura de código da Microsoft como um editor confiável no dispositivo de destino.

1. Abra as propriedades do script no Windows Explorer. Alterne para a guia **assinaturas digitais** e selecione **detalhes**.

1. Na guia **geral** , selecione **Exibir certificado**.

    > [!Note]
    > Para distribuir o certificado por meio de outros mecanismos, primeiro exporte o certificado para um arquivo. Vá para a guia **detalhes** e selecione **copiar para arquivo**.

1. Selecione **Instalar certificado**. Importe o certificado, colocando-o no repositório **editores confiáveis** .


## <a name="see-also"></a>Consulte também

- [Solucionar problemas do Desktop Analytics](/sccm/desktop-analytics/troubleshooting)

- [Criar e executar scripts do PowerShell do console do Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts)
