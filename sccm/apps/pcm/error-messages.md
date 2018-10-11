---
title: Mensagens de erro
titleSuffix: Configuration Manager
description: Saiba mais sobre as mensagens de erro do Gerenciador de Conversão de Pacotes.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0d3cf6e1-b295-4b05-821d-e9f57c74ca14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 62c4453cc383fa14eebf6e66c2582b878aaebae2
ms.sourcegitcommit: 759098de944b8f7d5eedfc2bae2cb9a6ba15276f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43297201"
---
# <a name="technical-reference-for-package-conversion-manager-error-messages"></a>Referência técnica para mensagens de erro do Gerenciador de Conversão de Pacotes

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

<!--1357861-->

Este artigo descreve as mensagens de erro exibidas pelo Gerenciador de Conversão de Pacotes. Ele também inclui as possíveis causas do erro e métodos para corrigi-lo. O Gerenciador de Conversão de Pacotes registra mensagens de erro no **PCMTrace.log**. Para saber mais, incluindo como controlar o nível de detalhes, confira [Arquivos de log](/sccm/apps/pcm/troubleshoot-pcm#log-files).


#### <a name="application-creation-failed-with-the-following-exception"></a>Falha na criação do aplicativo com a seguinte exceção

Ocorreu a exceção especificada durante o envio do objeto de aplicativo para o servidor do Gerenciador de Conversão de Pacote.

Verifique suas permissões no Configuration Manager, valide a conectividade e tente novamente. Se essas ações não resolverem o problema, examine o arquivo **PCMtrace.log** (nível de detalhes 4) e **SMSProv.log**.


#### <a name="conversion-error--applies-to-a-package-transform-status"></a>Erro de conversão – APLICA-SE A UM STATUS DE TRANSFORMAÇÃO DE PACOTE

Ocorreu uma exceção geral durante a conversão do pacote. Examine o arquivo de log **PCMtrace.log** (nível de detalhes 4).

Verifique as permissões de usuário para o compartilhamento de rede (fonte de dados do pacote), valide sua conectividade e tente novamente. Se essas ações não resolverem o problema, examine o arquivo **PCMtrace.log** (nível de detalhes 4).


#### <a name="did-not-find-a-converted-package-and-its-resultant-application-in-the-workflow-outputs"></a>Não foi possível encontrar um pacote convertido e seu aplicativo resultante nas saídas de fluxo de trabalho
O aplicativo (pacote/programa convertido) foi excluído.

Modificar o pacote/programa dependente para garantir a existência de pacote/programa dependente.


#### <a name="objects-were-not-created-successfully"></a>Os objetos não foram criados com êxito
Há várias causas possíveis.

Verifique suas permissões no Configuration Manager, valide a conectividade e tente novamente. Se essas ações não resolverem o problema, examine o arquivo **PCMtrace.log** (nível de detalhes 4) e o arquivo **SMSProv.log**.


#### <a name="please-close-the-wizard-and-resolve-any-issues-with-the-selected-package-see-pcmtracelog-for-more-details"></a>Feche o assistente e resolva todos os problemas com o pacote selecionado. Saiba mais em PCMtrace.Log
Há várias causas possíveis.

Verifique suas permissões no Configuration Manager, valide a conectividade e tente novamente. Se essas ações não resolverem o problema, examine o arquivo **PCMtrace.log** (nível de detalhes 4) e o arquivo **SMSProv.log**.


#### <a name="some-deployment-types-are-missing-detection-methods-all-deployment-types-must-have-detection-methods"></a>Alguns Tipos de implantação não contêm Métodos de detecção. Todos os Tipos de Implantação devem ter Métodos de Detecção
Os métodos de detecção estão ausentes do programa.

Adicione um ou mais métodos de detecção durante o processo **Corrigir e Converter**.


#### <a name="there-was-an-error-preparing-the-package-for-conversion"></a>Ocorreu um erro ao preparar o pacote para conversão
Há várias causas possíveis.

Verifique suas permissões no Configuration Manager, valide a conectividade e tente novamente. Se essas ações não resolverem o problema, examine o arquivo **PCMtrace.log** (nível de detalhes 4) e o arquivo **SMSProv.log**.


