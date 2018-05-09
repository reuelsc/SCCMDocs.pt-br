---
title: Solucionar problemas do SCAP
titleSuffix: Configuraton Manager
description: Importar as configurações de conformidade do SCAP como linhas de base de configuração e exportar os resultados
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 27261853-1641-4826-98c6-afbb73a1209d
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 05010d73916ac4c012c157a470ed98dce47fc747
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="troubleshoot-the-scap-extensions-for-microsoft-system-center-configuration-manager"></a>Solucionar problemas das Extensões do SCAP para o Microsoft System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

> [!Tip]  
> Esse recurso foi introduzido pela primeira vez na versão Technical Preview 1803 como um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features). Esta versão de pré-lançamento das extensões do SCAP pode ser instalada em todas as versões compatíveis no momento do branch atual do Configuration Manager e o LTSB 1606. O arquivo de instalação está localizado em cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi a partir da Technical Preview 1803. 

As Extensões do SCAP para o Microsoft System Center Configuration Manager foram desenvolvidas para funcionar com os fluxos de dados do SCAP destinados à ferramenta SCAP validada com a funcionalidade ACS para dar suporte à USGCB. Normalmente, você não teria problemas com esses fluxos de dados do SCAP do USGCB baixados do site do NIST.

No entanto, é possível diagnosticar e solucionar problemas que podem ser encontrados usando os seguintes métodos:

- Verifique se os componentes do cliente (scmdcm.msi) das Extensões do SCAP estão instalados em todos os computadores de destino.
- Examine a saída do arquivo de log da ferramenta Microsoft.Sces.ScapToDcm.exe.
- Examine os problemas comuns e as soluções ao usar as Extensões do SCAP.
- Entre em contato com a Microsoft em caso de dúvidas ou comentários sobre as Extensões do SCAP.



## <a name="review-microsoftscesscaptodcmexe-tool-log"></a>Examine o Log da ferramenta Microsoft.Sces.ScapToDcm.exe

A ferramenta Microsoft.Sces.ScapToDcm.exe cria um arquivo de log com um nome personalizado quando o parâmetro –log é especificado. O arquivo de log contém informações sobre os resultados da execução da ferramenta Microsoft.Sces.ScapToDcm.exe. Por exemplo, o arquivo de log contém o número de itens no arquivo de entrada do XCCDF/DataStream que foram descartados ou ignorados durante a execução da ferramenta Microsoft.Sces.ScapToDcm.exe.

A tabela a seguir lista algumas das informações que aparecem no arquivo de log e uma descrição de cada tipo de informação.

### <a name="description-of-information-found-in-microsoftscesscaptodcmexe-log-files"></a>Descrição de informações encontradas nos arquivos de log de Microsoft.Sces.ScapToDcm.exe

| Informações | Descrição |
| --- | --- |
| Soltar | Um item pode ser descartado, pois o tipo de teste não é um tipo de teste com suporte. |
| Skip |A ID de definição do OVAL é uma plataforma inválida. </br> </br> A ID de definição do OVAL não é referenciada no arquivo de entrada XCCDF/DataStream.</br> </br> A ID de teste do OVAL não é referenciada no arquivo de entrada XCCDF/DataStream. </br> </br> A ID de perfil do XCCDF não contém nenhuma instrução @select igual a 1. </br> </br> A ID de perfil do XCCDF inclui um atributo abstrato que é true. </br> </br> A ID de perfil do XCCDF não contém uma regra de qualificação.|

## <a name="common-problems-and-solutions"></a>Problemas comuns e soluções

A tabela a seguir lista alguns problemas comuns e soluções para ajudá-lo a solucionar problemas.

Tabela 1.6 problemas comuns e soluções

| Problema | Possível solução |
| --- | --- |
| Se você vir um status de **Erro** ou **Desconhecido** de uma linha de base e o IE não puder mostrar o relatório com êxito. O IE exibe a mensagem &quot;O relatório está vazio ou é inválido&quot; | Selecione a linha de base e clique em **Avaliar** para executar a linha de base novamente e aguarde para monitorar o **Estado de Conformidade**/**Atualização da Última Avaliação**. Após a atualização da data da Última Avaliação para a data/hora atual (isso significa que a avaliação foi concluída), selecione a linha de base e exiba o relatório novamente. Se o IE ainda não conseguir exibir o relatório, isso pode indicar que a linha de base é muito grande. Gere novamente o conteúdo usando um tamanho de lote menor para criar linhas de base filho menores. Se esse problema acontecer nas linhas de base pai, tente implantar as linhas de base filho. |
| Criei GPOs (objetos da Política de Grupo) que incluem as configurações prescritas do USGCB e vinculei-as às OUs (unidades organizacionais) que contêm computadores com Windows 7, mesmo que os relatórios de conformidade indiquem que algumas das configurações não estão configuradas corretamente. | É possível que as permissões da Política de Grupo estejam incorretas ou que elas não tenham sido vinculadas à UO correta. No entanto, é mais provável que as novas configurações ainda não tenham tido efeito. Por padrão, a Política de Grupo em computadores cliente que pertencem a um domínio do Active Directory verifica a atualização da Política de Grupo a cada 90 minutos. Este pode ser um dos motivos pelos quais as configurações não parecem ter sido aplicadas, mesmo que você tenha configurado as políticas corretamente. Outro fator a ser lembrado é que muitas configurações do computador exigem uma reinicialização para que tenham efeito. Por exemplo, a configuração chamada **Criptografia de sistema: usar algoritmos compatíveis com FIPS para criptografia, hash e assinatura** exige que você reinicie o computador antes que o Windows possa usar os algoritmos de criptografia especificados. Você pode ignorar o intervalo de atualização de Política de Grupo digitando o seguinte comando no prompt de comando com privilégios de administrador: gpupdate /force Após a atualização da Política de Grupo ser concluída, reinicie o computador para garantir que todas as configurações entrem em vigor. Para obter mais informações, consulte: [A descrição do utilitário de atualização de política de grupo](http://support.microsoft.com/kb/298444), Artigo 298444 da Base de Dados de Conhecimento. |
| Estou tendo problemas ao fornecer minhas informações organizacionais à conexão de banco de dados. | Para obter informações conceituais sobre como configurar as informações de conexão de banco de dados, veja o artigo [Instalar e configurar o SCAP](/sccm/compliance/plan-design/scap/install-configure-scap). 

## <a name="next-step"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Instalar e configurar as Extensões do SCAP](/sccm/compliance/plan-design/scap/install-configure-scap)