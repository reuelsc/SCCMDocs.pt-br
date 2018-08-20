---
title: Ferramenta de limpeza da biblioteca de conteúdo
titleSuffix: Configuration Manager
description: Use a ferramenta de limpeza da biblioteca de conteúdo para remover conteúdo órfão não associado a uma implantação do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e71b95642160d519f222a50a66bc8f636628d6e
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383516"
---
# <a name="content-library-cleanup-tool"></a>Ferramenta de limpeza da biblioteca de conteúdo

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Use a ferramenta de linha de comando de limpeza da biblioteca de conteúdo para remover conteúdo não está mais associado a nenhum pacote ou aplicativo em um ponto de distribuição. Esse tipo de conteúdo é chamado de *conteúdo órfão*. Essa ferramenta substitui as versões mais antigas de ferramentas semelhantes lançadas para produtos antigos do Configuration Manager.  

A ferramenta só afeta o conteúdo no ponto de distribuição que você especificar ao executá-la. A ferramenta não pode remover o conteúdo da biblioteca de conteúdo no servidor do site.

Encontre **ContentLibraryCleanup.exe** em `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` no servidor do site.



## <a name="requirements"></a>requisitos  

- Execute a ferramenta apenas em relação a um único ponto de distribuição por vez.  

- Execute-a diretamente no computador que hospeda o ponto de distribuição que receberá a limpeza ou remotamente de outro computador.  

- A conta de usuário que executa a ferramenta precisa ter permissões iguais às da função de segurança de **Administrador Completo** no Configuration Manager.  



## <a name="modes-of-operation"></a>Modos de operação

Execute a ferramenta nos dois modos a seguir: [Hipóteses](#what-if-mode) e [Exclusão](#delete-mode).

> [!Tip]  
> Comece com o modo *Hipóteses*. Quando estiver satisfeito com os resultados, execute a ferramenta no modo *Exclusão*.  


### <a name="what-if-mode"></a>Modo de Hipóteses   

Se você não especificar o parâmetro `/delete`, a ferramenta será executada no modo de hipóteses. Esse modo identifica o conteúdo que seria excluído do ponto de distribuição.

- Quando executada nesse modo, a ferramenta não exclui nenhum dado.  

- A ferramenta grava no arquivo de log as informações sobre o conteúdo que ela excluiria. Não há nenhuma solicitação de confirmação para cada possível exclusão.  


### <a name="delete-mode"></a>Modo de exclusão   

Quando você executa a ferramenta com o parâmetro `/delete`, ela é executada no modo de exclusão.

- Quando ela é executada nesse modo, o conteúdo órfão encontrado no ponto de distribuição especificado pode ser excluído da biblioteca de conteúdo do ponto de distribuição.  

- Antes de excluir cada arquivo, confirme que a ferramenta deve excluí-lo. Selecione **S** para Sim, **N** para não ou **Sim para tudo** para ignorar as próximas solicitações e excluir todo o conteúdo órfão.  


### <a name="log-file"></a>Arquivo de log

Independentemente do modo em que a ferramenta é executada, ela sempre cria um log automaticamente. Ele nomeia o arquivo de log com as seguintes informações: 
- O modo em que a ferramenta é executada  
- O nome do ponto de distribuição  
- A data e hora da operação  

Quando a ferramenta é concluída, ele abre automaticamente o arquivo de log no Windows. 

Por padrão, a ferramenta grava o arquivo de log na pasta temporária da conta de usuário que a executa. Esse local fica no computador em que você executa a ferramenta, que nem sempre é o destino da ferramenta. Use o parâmetro `/log` para redirecionar o arquivo de log para outro local, incluindo um compartilhamento de rede.



## <a name="run-the-tool"></a>Executar a ferramenta

Para executar a ferramenta: 

1. Abra um prompt de comando como administrador. Mude de diretório para a pasta que contém **ContentLibraryCleanup.exe**.  

2. Insira uma linha de comando que inclua os [parâmetros de linha de comando](#bkmk_params) necessários e os parâmetros opcionais que você deseja usar.



## <a name="bkmk_params"></a> Parâmetros de linha de comando  

Use esses parâmetros de linha de comando em qualquer ordem.   

### <a name="required-parameters"></a>Parâmetros necessários
|Parâmetro|Detalhes|
|---------|-------|
| `/dp <distribution point FQDN>`  | Especifique o FQDN (nome de domínio totalmente qualificado) do ponto de distribuição que deseja limpar. |
| `/ps <primary site FQDN>` | *Necessário* somente ao limpar o conteúdo de um ponto de distribuição em um site secundário. A ferramenta conecta-se ao site primário pai para executar consultas no provedor de SMS. Essas consultas permitem que a ferramenta determine qual conteúdo deve estar no ponto de distribuição. Em seguida, ela pode identificar o conteúdo órfão a ser removido. Essa conexão com o site primário pai precisa ser feita para os pontos de distribuição em um site secundário porque os detalhes necessários não estão disponíveis diretamente no site secundário.|
| `/sc <primary site code>`  | *Necessário* somente ao limpar o conteúdo de um ponto de distribuição em um site secundário. Especifique o código do site primário pai. |

#### <a name="example-scan-and-log-what-content-it-would-delete-what-if"></a>Exemplo: verificar e registrar qual conteúdo seria excluído (hipóteses)
`ContentLibraryCleanup.exe /dp server1.contoso.com`

#### <a name="example-scan-and-log-content-for-a-dp-at-a-secondary-site"></a>Exemplo: verificar e registrar o conteúdo de um DP em um site secundário
`ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com /sc ABC` 


### <a name="optional-parameters"></a>Parâmetros opcionais

|Parâmetro|Detalhes|
|---------|-------|
|`/delete`| Use esse parâmetro quando estiver pronto para excluir o conteúdo do ponto de distribuição. Um aviso é exibido antes da exclusão do conteúdo. </br></br> Quando você não usa esse parâmetro, a ferramenta registra os resultados de qual conteúdo seria excluído. Sem esse parâmetro, ela não exclui nenhum conteúdo do ponto de distribuição. |
| `/q` | Esse parâmetro executa a ferramenta no modo silencioso que suprime todos os avisos. Essas solicitações incluem quando ela exclui o conteúdo. Ela também não abre o arquivo de log automaticamente. |
| `/ps <primary site FQDN>` | Opcional somente ao limpar o conteúdo de um ponto de distribuição em um site primário. Especifique o FQDN do site primário ao qual o ponto de distribuição pertence. |
| `/sc <primary site code>` | Opcional somente ao limpar o conteúdo de um ponto de distribuição em um site primário. Especifique o código do site primário ao qual o ponto de distribuição pertence. |
| `/log <log file directory>` | Especifique o local onde a ferramenta grava o arquivo de log. Esse local pode ser uma unidade local ou um compartilhamento de rede.</br></br> Quando você não usa esse parâmetro, a ferramenta coloca o arquivo de log no diretório temporário do usuário no computador em que a ferramenta é executada.|

#### <a name="example-delete-content"></a>Exemplo: excluir conteúdo 
`ContentLibraryCleanup.exe /dp server1.contoso.com /delete`

#### <a name="example-delete-content-without-prompts"></a>Exemplo: excluir conteúdo sem avisos
`ContentLibraryCleanup.exe /q /dp server1.contoso.com /delete` 

#### <a name="example-log-to-local-drive"></a>Exemplo: registrar na unidade local
`ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop` 

#### <a name="example-log-to-network-share"></a>Exemplo: registrar no compartilhamento de rede
`ContentLibraryCleanup.exe /dp server1.contoso.com /log \\server\share`


### <a name="known-issue"></a>Problema conhecido

Quando algum pacote ou implantação falha ou está em andamento, a ferramenta pode retornar o seguinte erro: `System.InvalidOperationException: This content library cannot be cleaned up right now because package <packageID> is not fully installed.`

Não há nenhuma solução alternativa para esse problema. A ferramenta não consegue identificar com segurança os arquivos órfãos quando o conteúdo está em andamento ou não pôde ser implantado. A ferramenta não permitirá a limpeza do conteúdo até que você resolva esse problema.
