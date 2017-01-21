---
title: "Política de privacidade do System Center Configuration Manager – Biblioteca de cmdlets do Configuration Manager | Microsoft Docs"
description: "Saiba mais sobre como a Microsoft coleta e usa dados relacionados à biblioteca de cmdlets do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 767d0594eb871462df038997ea3b7e29615e05f7
ms.openlocfilehash: 10d8e8948d66a6b9b74e16a02cfbfc4ced66596c


---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>Política de privacidade do System Center Configuration Manager – Biblioteca de Cmdlets do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Esta política de privacidade abrange os recursos para a Biblioteca de Cmdlets do System Center Configuration Manager.  

## <a name="usage-data"></a>Dados de uso  
 **O que esse recurso faz:**   
A Biblioteca de Cmdlets do System Center Configuration Manager permite que você gerencie uma hierarquia do Configuration Manager usando cmdlets e scripts do Windows PowerShell. A Biblioteca de Cmdlets coleta informações sobre como usar os cmdlets incluídos na biblioteca para identificar tendências e padrões de uso.  A Biblioteca de Cmdlets também coleta os tipos e números de erros encontrados durante o uso dos cmdlets.  

 **Informações coletadas, processadas ou transmitidas:**   
os dados de uso coletados incluem como iniciar, parar e encerrar cmdlets; a execução de cmdlets preteridos e métricas de atividades para operações do provedor de SMS relacionadas aos cmdlets. Essas informações não são pessoalmente identificáveis.  As informações de erro coletadas incluem erros retornados pelo cmdlets e detalhes de erros para erros de exceção. Alguns relatórios de detalhes de erro inadvertidamente podem conter identificadores individuais, como um número de série para um dispositivo conectado ao computador. A Biblioteca de Cmdlets filtra e torna anônimas as informações contidas nos relatórios de erro para remover quaisquer identificadores individuais antes da transmissão à Microsoft.  

 **Uso das informações:**   
usamos essas informações para melhorar a qualidade, a segurança e a integridade dos produtos e serviços que oferecemos.  

 **Opção/controle:**   
esse recurso de dados de uso é habilitado por padrão. A Biblioteca de Cmdlets do System Center Configuration Manager inclui duas chaves do Registro para controlar essa funcionalidade.  

 Para cancelar totalmente, você precisa definir esses dois valores de chave do Registro, um para cada um dos provedores de Rastreamento de Eventos para Windows (ETW):  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (cancelamento de Dados de Uso para o provedor da unidade)  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (cancelamento de Dados de Uso para cmdlets)  

 Alterações nas configurações de Dados de Uso são específicas do computador em que foram feitas.  

 Para obter mais informações sobre como configurar os Dados de Uso (coleção), veja a [documentação da Biblioteca de Cmdlets do System Center Configuration Manager](https://technet.microsoft.com/en-us/library/dn958404.aspx).   



<!--HONumber=Dec16_HO3-->


