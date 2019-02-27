---
title: Solucionar problemas do SCAP
titleSuffix: Configuration Manager
description: Saiba como solucionar problemas de extensões do SCAP para o Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 27261853-1641-4826-98c6-afbb73a1209d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 58a3c69e6206aa651e55f96286f98f64f748de70
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137129"
---
# <a name="troubleshoot-the-scap-extensions-for-configuration-manager"></a>Solucionar problemas de extensões do SCAP para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

As extensões do SCAP para o Configuration Manager são projetadas para trabalhar com os fluxos de dados do SCAP destinados à ferramenta validada pelo SCAP com a funcionalidade do ACS para dar suporte à USGCB. Normalmente, não há problemas com esses fluxos de dados do SCAP USGCB baixados do site do NIST.

Diagnostique e solucione problemas usando os seguintes métodos:  

- Verifique se os componentes do cliente de extensões do SCAP (scmdcm.msi) estão instalados em todos os computadores de destino.  

- Examine a saída do arquivo de log da ferramenta Microsoft.Sces.ScapToDcm.exe.  

- Examine os problemas e as soluções comuns ao usar extensões do SCAP.  

- Contate a Microsoft para fazer perguntas ou comentários sobre as extensões do SCAP.



## <a name="review-microsoftscesscaptodcmexe-log"></a>Examine o log Microsoft.Sces.ScapToDcm.exe

A ferramenta Microsoft.Sces.ScapToDcm.exe cria um arquivo de log nomeado personalizado quando você especifica o parâmetro `–log`. O arquivo de log contém informações sobre os resultados da execução da ferramenta Microsoft.Sces.ScapToDcm.exe. Por exemplo, ele inclui o número de itens no arquivo de entrada XCCDF/DataStream que foram removidos ou ignorados durante a execução da ferramenta Microsoft.Sces.ScapToDcm.exe.

A tabela a seguir lista algumas das informações que aparecem no arquivo de log e uma descrição de cada tipo de informação.

### <a name="information-found-in-the-microsoftscesscaptodcmexe-log-file"></a>Informações encontradas no arquivo de log Microsoft.Sces.ScapToDcm.exe

| Informações | Descrição |
| --- | --- |
| **Remover** | Um item pode ser removido porque o tipo de teste não é um tipo de teste com suporte. |
| **Ignorar** | A ID de definição do OVAL é uma plataforma inválida. </br> </br> A ID de definição do OVAL não é referenciada pelo arquivo de entrada do XCCDF/DataStream.</br> </br> A ID de teste do OVAL não é referenciada pelo arquivo de entrada do XCCDF/DataStream. </br> </br> A ID de perfil do XCCDF não contém nenhuma instruções `@select` igual a 1. </br> </br> A ID de perfil do XCCDF inclui um atributo abstrato que é true. </br> </br> A ID de perfil do XCCDF não contém uma regra de qualificação.|



## <a name="common-problems-and-solutions"></a>Problemas comuns e soluções

Aqui estão alguns problemas comuns e as soluções para ajudá-lo a solucionar problemas.

- O status **Erro** ou **Desconhecido** é exibido para uma linha de base e o Internet Explorer não consegue mostrar o relatório com êxito. O erro do navegador é "o relatório está vazio ou é inválido."  

     - Execute a linha de base novamente. Selecione a linha de base e clique em **Avaliar**. Em seguida, espere para monitorar o **Estado de Conformidade**/**Atualização da Última Avaliação**. Depois que a data da Última Avaliação for atualizada para a data/hora atual, o que significa que a avaliação foi concluída, selecione a linha de base e exiba o relatório novamente.  

     - Se o Internet Explorer ainda não puder exibir o relatório, isso poderá significar que a linha de base é muito grande. Gere novamente o conteúdo usando um tamanho de lote menor para criar linhas de base filho menores.  

     - Se esse problema acontecer nas linhas de base pai, tente implantar as linhas de base filho.  

- Eu criei GPOs (objetos de política de grupo) que incluem as configurações prescritas pelo USGCB. Eu os vinculei a UOs (unidades organizacionais) que contêm os computadores que executam o Windows 7. Os relatórios de conformidade indicam que algumas das configurações não estão configuradas corretamente.  

     - É possível que as permissões de política de grupo estejam incorretas ou que não tenham sido vinculadas à UO correta.  

     - É mais provável que as novas configurações ainda não tenham entrado em vigor. Por padrão, os clientes do Active Directory verificam se há atualizações na política de grupo a cada 90 minutos. Esse ciclo pode ser um dos motivos pelos quais as configurações parecem não ter sido aplicadas, mesmo que você tenha configurado as políticas corretamente.  

     - Muitas configurações do computador exigem uma reinicialização para que entrem em vigor. Por exemplo, a configuração de **Criptografia de sistema: usar algoritmos compatíveis com FIPS para criptografia, hash e assinatura** exige que você reinicie o computador antes que o Windows possa usar os algoritmos de criptografia especificados. Ignore o intervalo de atualização de política de grupo inserindo o seguinte comando em um prompt de comando com privilégios de administrador: `gpupdate /force`. Depois de concluída a atualização da Política de Grupo, reinicie o computador para garantir que todas as configurações tenham efeito. Para obter mais informações, confira [Uma descrição do utilitário de atualização de política de grupo](https://support.microsoft.com/help/298444).

- Estou tendo problemas ao fornecer a conexão de banco de dados com minhas informações organizacionais.  

     - Para obter mais informações de como configurar sua conexão de banco de dados, confira [Instalar e configurar o SCAP](/sccm/compliance/plan-design/scap/install-configure-scap).  
