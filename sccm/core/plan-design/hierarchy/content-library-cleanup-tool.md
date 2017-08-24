---
title: "A ferramenta de limpeza da biblioteca de conteúdo | Microsoft Docs"
description: "Use a ferramenta de limpeza da biblioteca de conteúdo para remover conteúdo órfão não associado a uma implantação do System Center Configuration Manager."
ms.custom: na
ms.date: 4/7/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 76e6772bdd5cbd32d525e728f6ebc988b045da78
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="the-content-library-cleanup-tool-for-system-center-configuration-manager"></a>A ferramenta de limpeza da biblioteca de conteúdo no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

 A partir da versão 1702, você pode usar uma ferramenta de linha de comando (**ContentLibraryCleanup.exe**) para remover o conteúdo que não está mais associado a nenhum pacote ou aplicativo de um ponto de distribuição (conteúdo órfão). Essa ferramenta é chamada de ferramenta de limpeza da biblioteca de conteúdo e substitui as versões mais antigas de ferramentas semelhantes lançadas para os últimos produtos do Configuration Manager.  

A ferramenta só afeta o conteúdo no ponto de distribuição que você especificar ao executá-la. A ferramenta não pode remover o conteúdo da biblioteca de conteúdo no servidor do site.

Você poderá encontrar o **ContentLibraryCleanup.exe** na pasta *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* no servidor do site no site de administração central ou site primário.

## <a name="requirements"></a>Requisitos  
 A ferramenta só pode ser executada em um único ponto de distribuição por vez.  
 - Ela pode ser executada diretamente no computador que hospeda o ponto de distribuição que você quer limpar, ou remotamente de outro servidor.
 - A conta de usuário que executa a ferramenta diretamente deve ter permissões de administração baseada em funções equivalentes a um Administrador Completo na hierarquia do Configuration Manager. A ferramenta não funcionará quando a conta receber essas permissões como um membro de um grupo de segurança do Windows que contém as permissões de Administrador Completo.

## <a name="modes-of-operation"></a>Modos de operação
Você pode executar a ferramenta nos dois modos a seguir. Recomendamos que você execute a ferramenta no modo de *hipóteses (What-If)* para poder examinar os resultados antes de executar a ferramenta no *modo de exclusão*:
  1.    **Modo de hipóteses**:   
      Se você não especifica a opção **/delete**, a ferramenta é executada no modo de hipóteses e identifica o conteúdo que seria excluído do ponto de distribuição.
   - Quando executada nesse modo, a ferramenta não exclui os dados.
   - As informações sobre o conteúdo que seria excluído são gravadas no arquivo de log da ferramenta e você não precisará confirmar cada exclusão potencial.  
      </br>   

  2. **Modo de exclusão**:   
    quando você executa a ferramenta com a opção **/delete**, ela é executada no modo de exclusão.

     - Quando ela é executada nesse modo, o conteúdo órfão encontrado no ponto de distribuição especificado pode ser excluído da biblioteca de conteúdo do ponto de distribuição.
     -  Antes de excluir cada arquivo, você deverá confirmar se o arquivo deve ser excluído.  Você pode selecionar, **Y** para sim, **N** para não ou **Sim para todos** para ignorar as futuras solicitações e excluir todo o conteúdo órfão.  
     </br>

Quando a ferramenta é executada em um desses modos, ela cria automaticamente um log com um nome que inclui o modo no qual ela foi executada, o nome do ponto de distribuição, a data e a hora da operação. O arquivo de log é aberto automaticamente quando a ferramenta é concluída.

Por padrão, o arquivo de log é gravado na pasta temporária da conta de usuário que executa a ferramenta, no computador em que a ferramenta é executada. Você pode usar a opção **/log** para redirecionar o arquivo de log para outro local, incluindo um compartilhamento de rede.


## <a name="run-the-tool"></a>Executar a ferramenta
Para executar a ferramenta:
1. abra um prompt de comando administrativo para uma pasta que contém **ContentLibraryCleanup.exe**.  
2. Em seguida, insira uma linha de comando que inclui as opções de linha de comando necessárias e os comutadores opcionais que você deseja usar.

**Problema conhecido** Quando a ferramenta é executada, um erro semelhante ao seguinte pode ser retornado quando qualquer pacote ou implantação tiver falhado ou estiver em andamento:
-  *System.InvalidOperationException: esta biblioteca de conteúdo não pode ser limpa no momento porque o pacote <packageID> não está totalmente instalado.*

**Solução alternativa:** nenhuma. A ferramenta não é confiável para identificar arquivos órfãos quando o conteúdo está em andamento ou não pôde ser implantado. Portanto, a ferramenta não permitirá que você limpe conteúdo até que esse problema seja resolvido.

### <a name="command-line-switches"></a>Opções de linha de comando  
As opções de linha de comando a seguir podem ser usadas em qualquer ordem.   

|Alternar|Detalhes|
|---------|-------|
|**/delete**  |**Opcional** </br> Use essa opção quando você desejar excluir o conteúdo do ponto de distribuição. Você será perguntado antes do conteúdo ser efetivamente excluído. </br></br> Quando essa opção não for usada, a ferramenta registra os resultados de qual conteúdo seria excluído, mas não exclui conteúdo do ponto de distribuição. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**Opcional** </br> Essa opção executa a ferramenta no modo silencioso, o qual suprime todos os avisos (como os avisos para excluir conteúdo) e não abre automaticamente o arquivo de log. </br></br> Exemplo: ***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;FQDN do ponto de distribuição>**  | **Necessária** </br> Especifique o FQDN (nome de domínio totalmente qualificado) do ponto de distribuição que você deseja limpar. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/ps &lt;FQDN do site primário>**       | **Opcional** ao limpar o conteúdo de um ponto de distribuição em um site primário.</br>**Obrigatório** ao limpar o conteúdo de um ponto de distribuição em um site secundário. </br></br>A ferramenta se conecta ao site primário pai para executar consultas no SMS_Provider. Essas consultas permitem à ferramenta determinar qual conteúdo deve estar no ponto de distribuição, a fim de identificar o conteúdo órfão e removê-lo. Essa conexão ao site primário pai deve ser feita para pontos de distribuição em um site secundário, pois os detalhes necessários não estão disponíveis diretamente do site secundário.</br></br> Especifique o FQDN do site primário ao qual o ponto de distribuição pertence, ou do pai primário quando o ponto de distribuição estiver em um site secundário. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;código do site primário>**  | **Opcional** ao limpar o conteúdo de um ponto de distribuição em um site primário.</br>**Obrigatório** ao limpar o conteúdo de um ponto de distribuição em um site secundário. </br></br> Especifique o código do site primário ao qual o ponto de distribuição pertence, ou do site pai primário quando o ponto de distribuição estiver em um site secundário.</br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log <log file directory>**       |**Opcional** </br> Especifique o local onde a ferramenta grava o arquivo de log. Ele pode ser uma unidade local ou um compartilhamento de rede.</br></br> Quando essa opção não for usada, o arquivo de log será colocado na pasta temp do usuário, no computador em que a ferramenta é executada.</br></br> Exemplo de unidade local: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>Exemplo de compartilhamento de rede: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\&lt;share>\&lt;folder>***|
