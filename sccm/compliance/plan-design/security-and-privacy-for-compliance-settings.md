---
title: "Segurança e privacidade de configurações de conformidade | Microsoft Docs"
description: "Saiba mais sobre as práticas recomendadas de segurança para as configurações de conformidade no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1c409244-6778-4970-a99c-d2508c9cf62b
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: e7dc554ffcd23978eed44819b525f6cc239b2135
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-compliance-settings-in-system-center-configuration-manager"></a>Segurança e privacidade de configurações de conformidade no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*


## <a name="security-best-practices-for-compliance-settings"></a>Práticas recomendadas de segurança para configurações de conformidade  

|Prática recomendada de segurança|Mais informações|  
|----------------------------|----------------------|  
|Não monitore os dados confidenciais.|Para ajudar a evitar a divulgação de informações, não defina itens de configuração para monitorar informações potencialmente confidenciais.|  
|Não configurar regras de conformidade que usam dados que podem ser modificados pelos usuários finais.|Se você criar uma regra de conformidade com base nos dados que os usuários podem modificar, como configurações de Registro para opções de configuração, os resultados de conformidade não serão confiáveis.|  
|Importe pacotes de configuração do Microsoft System Center e outros dados de configuração de fontes externas somente se tiverem uma assinatura digital válida de um fornecedor confiável.|Os dados de configuração publicados podem ser assinados digitalmente para que você possa verificar a fonte de publicação e assegurar que os dados não foram violados. Se a verificação da assinatura digital falhar, você será avisado e solicitado a continuar com a importação. Não importe dados não assinados se não puder verificar a origem e a integridade dos dados.|  
|Implementar controles de acesso para proteger computadores de referência.|Certifique-se de que, quando um usuário administrativo configurar um Registro ou definir uma configuração do sistema de arquivos acessando um computador de referência, o computador de referência não foi comprometido.|  
|Proteger o canal de comunicação, quando você navegar para um computador de referência.|Para prevenir a violação de dados durante a transferência pela rede, use o protocolo IPsec ou SMB entre o computador que executa o console do Configuration Manager e o computador de referência.|  
|Restrinja e monitore os usuários administrativos que recebem a função de segurança baseada em função do Gerenciador de Configurações de Conformidade.|Usuários administrativos que recebem a função de **Gerenciador de Configurações de Conformidade** podem implantar itens de configuração em todos os dispositivos e todos os usuários na hierarquia. Os itens de configuração podem ser muito eficientes e podem incluir, por exemplo, scripts e reconfiguração do Registro.|  

## <a name="privacy-information-for-compliance-settings"></a>Informações sobre privacidade para configurações de conformidade  
 Você pode usar as configurações de conformidade para avaliar se os dispositivos cliente são compatíveis com os itens de configuração implantados nas linhas de base de configuração. Algumas configurações podem ser corrigidas automaticamente se estiverem fora de conformidade. As informações de conformidade são enviadas para o servidor do site pelo ponto de gerenciamento e armazenadas no banco de dados do site. As informações são criptografadas quando os dispositivos as enviam para o ponto de gerenciamento, mas não são armazenadas em formato criptografado no banco de dados do site. As informações são retidas no banco de dados até que a tarefa de manutenção de site **Excluir Dados Antigos de Gerenciamento da Configuração** as exclua a cada 90 dias. Você pode configurar o intervalo de exclusão. As informações de conformidade não são enviadas à Microsoft.  

 Por padrão, os dispositivos não avaliam as configurações de conformidade. Além disso, você deve configurar os itens de configuração e as linhas de base de configuração e implantá-los em dispositivos.  
