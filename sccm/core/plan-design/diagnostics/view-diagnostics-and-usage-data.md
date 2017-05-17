---
title: "Exibir dados de diagnóstico | Microsoft Docs"
description: "Veja os dados de uso e de diagnóstico para confirmar se sua hierarquia do System Center Configuration Manager não contém nenhuma informação confidencial."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 199096db7a23fb14db98b95e75246ed254848ab7
ms.openlocfilehash: 0932e2b2a4f3e13c35d6b7b0446083f1c233ce03
ms.contentlocale: pt-br
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-view-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Como exibir dados de diagnóstico e de dados do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode exibir dados de uso e de diagnóstico da hierarquia do System Center Configuration Manager para verificar se nenhuma informação confidencial ou identificável foi incluída. Os dados de telemetria são resumidos e armazenados na tabela **TEL_TelemetryResults** do banco de dados do site e são formatados para ser úteis e eficientes de forma programática. Embora as opções a seguir forneçam uma exibição dos dados exatos enviados à Microsoft, elas não se destinam a serem usadas para outras finalidades, como análise de dados.  

Use o comando SQL a seguir para exibir o conteúdo desta tabela e mostrar os dados exatos que são enviados. (Também é possível exportar esses dados para um arquivo de texto):  

-   **SELECT \* FROM TEL_TelemetryResults**  

> [!NOTE]  
>  Antes de instalar a versão 1602, a tabela que armazena os dados telemétricos é **TelemetryResults**.  

Quando o ponto de conexão de serviço está no modo offline, é possível usar a ferramenta de conexão de serviço para exportar os dados atuais de diagnóstico e de uso para um arquivo CSV (valores separados por vírgula). Execute a ferramenta de conexão de serviço no ponto de conexão de serviço usando o parâmetro **-Export**.  

##  <a name="bkmk_hashes"></a> Hashes unidirecionais  
Alguns dados consistem em cadeias de caracteres alfanuméricos aleatórios. O Configuration Manager usa o algoritmo SHA-256, que usa hashes unidirecionais, para garantir que não coletamos dados potencialmente confidenciais. O algoritmo mantém os dados em um estado no qual eles ainda podem ser usados para fins de correlação e comparação. Por exemplo, em vez de coletar os nomes de tabelas no banco de dados do site, um hash unidirecional é capturado para cada nome de tabela. Isso garante que os nomes de tabela personalizados criados ou os complementos de produtos de outros usuários não estão visíveis. Em seguida, podemos executar o mesmo hash unidirecional dos nomes de tabela SQL fornecidos por padrão no produto e comparar os resultados das duas consultas para determinar o desvio de seu esquema de banco de dados em relação ao padrão do produto. Isso é usado para aperfeiçoar as atualizações que exigem alterações no esquema SQL.  

Ao exibir os dados brutos, um valor com hash comum aparecerá em cada linha de dados. Essa é a ID da hierarquia. Esse valor com hash é usado para garantir que os dados são correlacionados com a mesma hierarquia sem identificar o cliente nem a origem.  

#### <a name="to-see-how-the-one-way-hash-works"></a>Para ver como funciona o hash unidirecional  

1.  Obtenha a ID da hierarquia executando a seguinte instrução SQL do SQL Management Studio no banco de dados do Configuration Manager: **select [dbo].[fnGetHierarchyID]\(\)**  

2.  Use o script do Windows PowerShell a seguir para executar o hash unidirecional do GUID obtido do banco de dados. Você pode comparar isso com a ID da hierarquia nos dados brutos para ver como podemos ocultar esses dados.  

    ```  
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)   
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)   
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()    
    # Hash the input   
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)              
    # Base64 encode the result for transport   
    $result = [Convert]::ToBase64String($hashedBytes)    
    return $result   
    ```  

