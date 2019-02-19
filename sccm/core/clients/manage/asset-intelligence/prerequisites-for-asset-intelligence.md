---
title: Pré-requisitos para o Asset Intelligence
titleSuffix: Configuration Manager
description: Conheça os pré-requisitos do Asset Intelligence no System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 23ab4f94-7bfe-436e-8a6a-029409a2730c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b47f2f06af45282349fec60ea9c7288a42c7e845
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124506"
---
# <a name="prerequisites-for-asset-intelligence-in-system-center-configuration-manager"></a>Pré-requisitos para o Asset Intelligence no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O Asset Intelligence no System Center Configuration Manager tem dependências externas e dependências dentro do produto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências externas ao Configuration Manager  
 A tabela a seguir fornece as dependências do Asset Intelligence que são externas ao Configuration Manager.  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Auditoria dos pré-requisitos de eventos de logon com êxito|Quatro relatórios do Asset Intelligence exibem informações coletadas dos logs de eventos de Segurança do Windows em computadores cliente. Se as configurações de log de eventos de Segurança não estiverem definidas para registrar todos os eventos de logon com Êxito, esses relatórios não conterão dados, mesmo que a classe apropriada de relatório de inventário de hardware esteja habilitada.<br /><br /> Os seguintes relatórios do Asset Intelligence dependem das informações coletadas de log de eventos de Segurança do Windows:<br /><br /> ‑   Hardware 03A ‑ Usuários primários do computador<br />‑   Hardware 03B ‑ Computadores de um usuário primário específico do console<br />‑   Hardware 04A ‑ Computadores compartilhados (multiusuário)<br />‑   Hardware 05A ‑ Usuários do console em um computador específico<br /><br /> Para habilitar o Agente Cliente de Inventário de Hardware para inventariar as informações necessárias para dar suporte a esses relatórios, primeiro você deve modificar as configurações de log de eventos de Segurança do Windows nos clientes para registrar todos os eventos de logon com Êxito e habilitar a classe de relatório de inventário de hardware **SMS_SystemConsoleUser** . Para obter mais informações sobre como modificar as configurações de log de eventos de Segurança para registrar todos os eventos de logon com Êxito, consulte [Habilitar auditoria dos eventos de logon com êxito](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableSuccessLogonEvents).|  

> [!NOTE]  
>  A classe de relatório de inventário de hardware **SMS_SystemConsoleUser** mantém dados de eventos de logon com êxito apenas para os 90 dias anteriores ao log de eventos de Segurança, independentemente do tamanho do log. Se o log de eventos de Segurança tiver menos de 90 dias de dados, o log inteiro será lido.  

## <a name="dependencies-internal-to-configuration-manager"></a>Dependências internas do Configuration Manager  
 A tabela a seguir fornece as dependências do Asset Intelligence que são internas ao Configuration Manager.  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Pré-requisitos do agente cliente|Os relatórios do Asset Intelligence dependem das informações do cliente obtidas por meio de relatórios de inventário de hardware e software do cliente. Para obter as informações necessárias para todos os relatórios do Asset Intelligence, os seguintes agentes cliente devem ser habilitados:<br /><br /> ‑   Agente Cliente de Inventário de Hardware<br />‑   Agente Cliente de Medição de Software|  
|Dependências do Agente Cliente de Inventário de Hardware|Para coletar dados de inventário necessários para alguns relatórios do Asset Intelligence, o Agente Cliente de Inventário de Hardware deve ser habilitado. Além disso, algumas classes de relatório de hardware das quais os relatórios do Asset Intelligence dependem devem ser habilitadas nos computadores do servidor do site primário.<br /><br /> Para obter informações sobre como habilitar o Agente Cliente de Inventário de Hardware, consulte [Como estender o inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).|  
|Dependências do Agente Cliente de Medição de Software|Um número de relatórios de software do Asset Intelligence depende do Agente Cliente de Medição de Software para os dados. Para obter informações sobre como habilitar o Agente Cliente de Medição de Software, consulte [Monitorar o uso de aplicativos com a medição de software no System Center Configuration Manager](../../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).<br /><br /> Os seguintes relatórios do Asset Intelligence dependem do Agente Cliente de Medição de Software para fornecer dados:<br /><br /> ‑   Software 07A ‑ Executáveis usados recentemente por número de computadores<br />‑   Software 07B ‑ Computadores que usaram recentemente um executável especificado<br />‑   Software 07C ‑ Executáveis usados recentemente em um computador específico<br />‑   Software 08A ‑ Executáveis usados recentemente por número de usuários<br />‑   Software 08B ‑ Usuários que usaram recentemente um executável especificado<br />‑   Software 08C ‑ Executáveis usados recentemente por um usuário especificado|  
|Pré-requisitos da classe de relatório de inventário de hardware do Asset Intelligence|Os relatórios do Asset Intelligence no Configuration Manager dependem de classes de relatório de inventário de hardware específicas. Até que as classes de relatório de inventário de hardware estejam habilitadas e os clientes tiverem relatado com base nessas classes, os relatórios do Asset Intelligence associados não conterão nenhum dado. Você pode habilitar as seguintes classes de inventário de hardware para dar suporte aos requisitos de relatório do Asset Intelligence:<br /><br /> -   SMS_SystemConsoleUsage<sup>1</sup><br />-   SMS_SystemConsoleUser<sup>1</sup><br />-   SMS_InstalledSoftware<br />-   SMS_AutoStartSoftware<br />-   SMS_BrowserHelperObject<br />-   Win32_USBDevice<br />-   SMS_InstalledExecutable<br />-   SMS_SoftwareShortcut<br />-   SoftwareLicensingService<br />-   SoftwareLicensingProduct<br />-   SMS_SoftwareTag<br /><br /> <sup>1</sup> Por padrão, as classes de relatório de inventário de hardware **SMS_SystemConsoleUsage** e **SMS_SystemConsoleUser** do Asset Intelligence estão habilitadas.<br /><br /> Você pode editar as classes de relatório de inventário de hardware do Asset Intelligence no console do Configuration Manager, no workspace **Ativos e Conformidade**, ao clicar no nó **Asset Intelligence**. Para mais informações, consulte a seção [Habilitar classes de relatório no inventário de hardware do Intelligence Hardware](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence) no tópico [Configurando o Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).|  
|Ponto do Reporting Services|A função do sistema de sites do ponto do Reporting Services deve estar instalada antes que os relatórios de atualizações de software possam ser exibidos. Para obter mais informações sobre como criar um ponto do Reporting Services, veja [Como configurar relatórios no Configuration Manager](http://go.microsoft.com/fwlink/p/?LinkId=232661).|  
