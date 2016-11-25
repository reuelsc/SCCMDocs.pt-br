---
title: "Política de privacidade do System Center Configuration Manager – Biblioteca de Cmdlets do Configuration Manager"
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 88d11aaed4a0e6575cb859f5dfc3ac425bd2bf38


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

## <a name="update-check"></a>Verificação de atualização  
 **O que esse recurso faz:**   
a Biblioteca de Cmdlets do System Center Configuration Manager verifica automaticamente as atualizações da biblioteca em uma base diária e notifica você para baixar a biblioteca atualizada.  

 **Informações coletadas, processadas ou transmitidas:**   
a verificação de atualização da Biblioteca de Cmdlets baixa um pequeno arquivo de texto do Centro de Download da Microsoft para fazer uma verificação de versão.   Esse arquivo não é armazenado localmente.  A Biblioteca de Cmdlets não atualiza automaticamente o software.  

 **Uso das informações:**   
usamos essas informações para melhorar a qualidade, a segurança e a integridade dos produtos e serviços que oferecemos.  

 **Opção/controle:**   
a verificação de atualização é habilitada por padrão.  A Biblioteca de Cmdlets do System Center Configuration Manager inclui estes cmdlets para controlar a funcionalidade de notificação de atualização:  

-   O`Get-CMCmdletUpdateCheck` obtém a configuração do recurso de atualização e indica se a política de usuário está sendo substituída pela política do sistema.  

-   O`Send-CMCmdletUpdateCheck` permite que você execute uma verificação de atualização não programada. Uma verificação não agendada não considera as configurações de política.  

-   O`Set-CMCmdletUpdateCheck` define as configurações de verificação de atualização em uma base por usuário ou por sistema. Você deve estar executando como administrador para definir as configurações do sistema.  

 Você pode encontrar mais informações sobre como configurar a verificação de atualização na [documentação da Biblioteca de Cmdlets do System Center Configuration Manager](https://technet.microsoft.com/en-us/library/dn958404.aspx).  



<!--HONumber=Nov16_HO1-->


