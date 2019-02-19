---
title: Política de privacidade para biblioteca de cmdlets do Configuration Manager
description: Saiba mais sobre como a Microsoft coleta e usa dados relacionados à biblioteca de cmdlets do System Center Configuration Manager.
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 58b5a2eec6df6ecd6b96c18178cc116bc2b6965a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135663"
---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>Política de privacidade do System Center Configuration Manager – Biblioteca de Cmdlets do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

Esta política de privacidade abrange os recursos para a Biblioteca de Cmdlets do System Center Configuration Manager.  

## <a name="usage-data"></a>Dados de uso  

#### <a name="what-this-feature-does"></a>O que esse recurso faz   

A biblioteca de cmdlets do System Center Configuration Manager permite que você gerencie uma hierarquia do Configuration Manager usando cmdlets e scripts do Windows PowerShell. A biblioteca de cmdlets coleta informações sobre como usar os cmdlets na biblioteca para identificar tendências e padrões de uso. A biblioteca de cmdlets também coleta os tipos e números de erros recebidos ao usar os cmdlets.  

#### <a name="information-collected-processed-or-transmitted"></a>Informações coletadas, processadas ou transmitidas
   
os dados de uso coletados incluem como iniciar, parar e encerrar cmdlets, a execução de cmdlets preteridos e métricas de atividades para operações do provedor de SMS relacionadas aos cmdlets. Essas informações não são pessoalmente identificáveis. As informações de erro coletadas incluem erros retornados pelo cmdlets e detalhes de erros para erros de exceção. Alguns relatórios de detalhes de erro inadvertidamente podem incluir identificadores individuais, como um número de série para um dispositivo conectado ao computador. A biblioteca de cmdlets filtra e torna anônimas as informações nos relatórios de erro para remover identificadores individuais antes da transmissão à Microsoft.  

#### <a name="use-of-information"></a>Uso das informações
   
A Microsoft usa essas informações para melhorar a qualidade, a segurança e a integridade dos produtos e serviços que oferece.  

#### <a name="choicecontrol"></a>Opção/controle   

esse recurso de dados de uso é habilitado por padrão. A biblioteca de cmdlets do System Center Configuration Manager inclui duas chaves do Registro que controlam essa funcionalidade.  

 Para cancelar totalmente, defina esses dois valores de chave do Registro. Eles são para cada um dos provedores de ETW (Rastreamento de Eventos para Windows):  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (cancelamento de dados de uso para o provedor da unidade)  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (cancelamento de dados de uso para cmdlets)  

  Alterações nas configurações de dados de uso são específicas do computador em que foram feitas.  


## <a name="next-steps"></a>Próximas etapas

[Documentação da Biblioteca de Cmdlets do System Center Configuration Manager](https://docs.microsoft.com/powershell/sccm/configurationmanager/).   
