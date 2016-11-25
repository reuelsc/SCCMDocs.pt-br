---
title: "Exibir dados de diagnóstico | System Center Configuration Manager"
description: "Veja os dados de uso e de diagnóstico para confirmar se sua hierarquia do System Center Configuration Manager não contém nenhuma informação confidencial."
ms.custom: na
ms.date: 10/06/2016
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
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5d1382d4912d03fb38bfc2f07edfb361c0ac6139


---
# <a name="how-to-view-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Como exibir dados de diagnóstico e de dados do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Você pode exibir dados de uso e de diagnóstico da hierarquia do System Center Configuration Manager para verificar se nenhuma informação confidencial ou identificável foi incluída. Os dados de telemetria são resumidos e armazenados na tabela **TEL_TelemetryResults** do banco de dados do site e são formatados para ser úteis e eficientes de forma programática. Embora as opções a seguir forneçam uma exibição dos dados exatos enviados à Microsoft, elas não se destinam a ser usadas para outras finalidades, como análise de dados.  

O seguinte comando SQL pode ser usado para exibir o conteúdo desta tabela e mostra os dados exatos que são enviados (você também pode exportar esses dados para um arquivo de texto):  

-   **SELECT \* FROM TEL_TelemetryResults**  

> [!NOTE]  
>  Antes de instalar a versão 1602, a tabela que armazena os dados de telemetria é a **TelemetryResults**.  

Quando o ponto de conexão de serviço está no modo offline, você pode usar a ferramenta de conexão de serviço para exportar os dados de uso e de diagnóstico atuais para um arquivo CSV (valores separados por vírgula). Execute a ferramenta de conexão de serviço no ponto de conexão de serviço com o parâmetro **-Export**.  

##  <a name="a-namebkmkhashesa-one-way-hashes"></a><a name="bkmk_hashes"></a> Hashes unidirecionais  
Alguns dos dados que consistem em cadeias de caracteres alfanuméricos aleatórios. O Configuration Manager usa hashes unidirecionais que usam o algoritmo SHA-256 para garantir que não coletamos dados potencialmente confidenciais e, ao mesmo tempo, os deixa em um estado em que ainda podem ser usados para fins de correlação e comparação. Por exemplo, em vez de coletar os nomes de tabelas no banco de dados do site, um hash unidirecional é capturado para cada nome de tabela. Isso garante que quaisquer nomes de tabela personalizados criados por você ou por complementos de produtos de terceiros não sejam visíveis. Em seguida, podemos executar o mesmo hash unidirecional dos nomes de tabela SQL que são fornecidos por padrão no produto e fazer uma comparação para determinar o desvio de seu esquema de banco de dados em relação ao padrão do produto. Isso é usado para aperfeiçoar as atualizações que exigem alterações no esquema SQL.  

Ao exibir os dados brutos, um valor com hash comum aparecerá em cada linha de dados. Essa é a ID da hierarquia. Esse valor com hash é usado para garantir que os dados sejam correlacionados com a mesma hierarquia sem identificar o cliente ou a origem.  

#### <a name="to-see-how-the-one-way-hash-works"></a>Para ver como funciona o hash unidirecional  

1.  Obtenha a ID da hierarquia executando a seguinte instrução SQL no SQL Management Studio no banco de dados do Configuration Manager: **select [dbo].[fnGetHierarchyID](\)**  

2.  Em seguida, use o script do Windows PowerShell a seguir para executar o hash unidirecional do GUID obtido do banco de dados. Você pode comparar isso com a ID da hierarquia nos dados brutos para ver como podemos ocultar esses dados.  

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



<!--HONumber=Nov16_HO1-->


