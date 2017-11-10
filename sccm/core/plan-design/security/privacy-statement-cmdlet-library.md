---
title: "Política de privacidade para biblioteca de cmdlets do Configuration Manager"
description: "Saiba mais sobre como a Microsoft coleta e usa dados relacionados à biblioteca de cmdlets do System Center Configuration Manager."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: e42193a810ec1206d083c1fd6e4c112be1c61a8d
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2017
---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>Política de privacidade do System Center Configuration Manager – Biblioteca de Cmdlets do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Esta política de privacidade abrange os recursos para a Biblioteca de Cmdlets do System Center Configuration Manager.  

## <a name="usage-data"></a>Dados de uso  
 **O que esse recurso faz:**   
A biblioteca de cmdlets do System Center Configuration Manager permite que você gerencie uma hierarquia do Configuration Manager usando cmdlets e scripts do Windows PowerShell. A biblioteca de cmdlets coleta informações sobre como usar os cmdlets na biblioteca para identificar tendências e padrões de uso. A biblioteca de cmdlets também coleta os tipos e números de erros encontrados ao usar os cmdlets.  

 **Informações coletadas, processadas ou transmitidas:**   
os dados de uso coletados incluem como iniciar, parar e encerrar cmdlets, a execução de cmdlets preteridos e métricas de atividades para operações do provedor de SMS (Systems Management Server) relacionadas aos cmdlets. Essas informações não são pessoalmente identificáveis.  As informações de erro coletadas incluem erros retornados pelo cmdlets e detalhes de erros para erros de exceção. Alguns relatórios de detalhes de erro inadvertidamente podem conter identificadores individuais, como um número de série para um dispositivo conectado ao computador. A biblioteca de cmdlets filtra e torna anônimas as informações nos relatórios de erro para remover identificadores individuais antes da transmissão à Microsoft.  

 **Uso das informações:**   
usamos essas informações para melhorar a qualidade, a segurança e a integridade dos produtos e serviços que oferecemos.  

 **Opção/controle:**   
esse recurso de dados de uso é habilitado por padrão. A biblioteca de cmdlets do System Center Configuration Manager inclui duas chaves do Registro que controlam essa funcionalidade.  

 Para cancelar totalmente, você precisa definir esses dois valores de chave do Registro, um para cada um dos provedores de Rastreamento de Eventos para Windows (ETW):  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (cancelamento de Dados de Uso para o provedor da unidade)  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (cancelamento de Dados de Uso para cmdlets)  

 Alterações nas configurações de Dados de Uso são específicas do computador em que foram feitas.  

 Para obter mais informações sobre como configurar os dados de uso (coleção), confira a [documentação da biblioteca de cmdlets do System Center Configuration Manager](https://technet.microsoft.com/en-us/library/dn958404.aspx).   
