---
title: "Privacidade de segurança do Asset Intelligence | Microsoft Docs"
description: "Obtenha as informações de segurança e privacidade do Asset Intelligence no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d0c6f7a0-dcae-4e6d-aa28-35d464d97ff7
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: d577a16725c2b167d1ff9f77096018433a2fa580


---
# <a name="security-and-privacy-for-asset-intelligence-in-system-center-configuration-manager"></a>Segurança e privacidade do Asset Intelligence no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Este tópico contém as informações de segurança e privacidade do Asset Intelligence no System Center Configuration Manager.  

##  <a name="a-namebkmksecurityaia-security-best-practices-for-asset-intelligence"></a><a name="BKMK_Security_AI"></a> Práticas recomendadas de segurança para o Asset Intelligence  
 Use as práticas recomendadas a seguir ao usar o Asset Intelligence.  

|Prática recomendada de segurança|Mais informações|  
|----------------------------|----------------------|  
|Ao importar um arquivo de licença (arquivo de Licenciamento por Volume da Microsoft ou de Demonstrativo de Licença Geral), proteja o arquivo e o canal de comunicação.|Use as permissões do sistema de arquivos NTFS para garantir que somente usuários autorizados possam acessar os arquivos de licença e use a assinatura do protocolo SMB para garantir a integridade dos dados quando forem transferidos para o servidor do site durante o processo de importação.|  
|Use o princípio de menos permissões para importar os arquivos de licença.|Use a administração baseada em funções para conceder a permissão Gerenciar o Asset Intelligence para o usuário administrativo que importa os arquivos de licença. A função interna do Gerenciador de Ativos inclui essa permissão.|  

##  <a name="a-namebkmkprivacyhardwareinventorya-privacy-information-for-asset-intelligence"></a><a name="BKMK_Privacy_HardwareInventory"></a> Informações sobre privacidade do Asset Intelligence  
 O Asset Intelligence estende os recursos de inventário do Configuration Manager para fornecer um nível mais alto de visibilidade de ativos na empresa. A coleta de informações do Asset Intelligence não é habilitada automaticamente. Você pode modificar o tipo de informações coletadas habilitando as classes de relatório de inventário de hardware. Para mais informações, consulte [Configurando Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 As informações do Asset Intelligence são armazenadas no banco de dados do Configuration Manager da mesma maneira que as informações de inventário. Quando os clientes se conectam a pontos de gerenciamento usando HTTPS, os dados são sempre criptografados durante a transferência para o ponto de gerenciamento. Quando os clientes se conectam usando HTTP, é possível configurar a transferência de dados de inventário para ser assinada e criptografada. Dados de inventário não são armazenados em formato criptografado no banco de dados. As informações são mantidas no banco de dados até que a tarefa de manutenção do site **Excluir Histórico de Inventário Antigo** as exclua em intervalos de 90 dias. Você pode configurar o intervalo de exclusão.  

 O Asset Intelligence não envia informações sobre os usuários e os computadores ou o uso da licença para a Microsoft. Você pode optar por enviar solicitações ao System Center Online para categorização, o que significa que você pode marcar um ou mais títulos de software não categorizados e enviá-los para o System Center Online para pesquisa e categorização. Depois que um título de software é carregado, os pesquisadores da Microsoft identificam, categorizam e disponibilizam esse conhecimento para todos os clientes que usam o serviço online. É necessário estar ciente das implicações de privacidade do envio de informações ao System Center Online:  

-   O upload se aplica somente às informações de título de software genéricas (nome, fornecedor e assim por diante) que você escolher enviar para o System Center Online. As informações de inventário não são enviadas com um upload.  

-   O upload nunca ocorre automaticamente, e o sistema não foi projetado para a automatização dessa tarefa. Você deve selecionar e aprovar manualmente o carregamento de cada título de software.  

-   Uma caixa de diálogo mostra exatamente quais dados serão carregados, antes do início do processo de upload.  

-   As informações de licença não são enviadas à Microsoft. As informações de licença são armazenadas em uma área separada do banco de dados do Configuration Manager e não podem ser enviadas à Microsoft.  

-   Qualquer título de software carregado se torna público, o que significa que o conhecimento desse determinado aplicativo e sua categorização se tornam parte do catálogo do Asset Intelligence do System Center Online e, posteriormente, podem ser baixados para outros consumidores do catálogo.  

-   A origem do título de software não é registrada no catálogo do Asset Intelligence e não é disponibilizada para outros clientes. No entanto, ainda é necessário se certificar de que nenhum título de aplicativo que contém informações privadas é carregado.  

-   Os dados carregados não podem ser cancelados.  

 Antes de configurar a coleção de dados do Asset Intelligence e optar por enviar informações ao System Center Online, considere os requisitos de privacidade de sua organização.  



<!--HONumber=Dec16_HO3-->


