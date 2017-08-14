---
title: "Monitorar clientes – Usar o Windows Analytics com o Configuration Manager | Microsoft Docs"
description: "O Windows Analytics é um conjunto de soluções executado no Operations Management Suite que permite a obtenção de informações valiosas sobre o estado atual de seu ambiente, aproveitando os dados telemétricos do Windows informados por dispositivos em seu ambiente."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
caps.latest.revision: 23
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: adabe8f475eb12dd44005ec07344e8565be20582
ms.contentlocale: pt-br
ms.lasthandoff: 07/29/2017

---

# <a name="use-windows-analytics-with-configuration-manager"></a>Usar o Windows Analytics com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O [Windows Analytics](https://www.microsoft.com/en-us/WindowsForBusiness/windows-analytics) é um conjunto de soluções executado no [Operations Management Suite](/azure/operations-management-suite/operations-management-suite-overview). As soluções permitem que você obtenha informações sobre o estado atual de seu ambiente. Os dispositivos em seu ambiente reportam dados telemétricos do Windows. Os dados podem ser acessados e analisados por meio de soluções no [Portal da Web do Operations Management Suite](https://mms.microsoft.com). No caso do [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics), os dados também podem ser disponibilizados diretamente no nó de monitoramento do console do Configuration Manager, conectando o Upgrade Readiness ao Configuration Manager.

Os dados telemétricos do Windows usados pelo Windows Analytics não são transferidos diretamente ao servidor de site do Configuration Manager. Computadores cliente enviam dados telemétricos do Windows para o serviço de telemetria. Em seguida, os dados relevantes são transferidos para soluções do Windows Analytics hospedadas em um dos espaços de trabalho de OMS da sua organização. O Configuration Manager pode então direcionar você aos dados relevantes no portal da Web com links no contexto ou dados de exibição direta que fazem parte das soluções que você conectou ao Configuration Manager. Também é possível consultar diretamente os dados no portal da Web do Operation Management Suite.

>[!Important]
>[Dados de diagnóstico e uso do Configuration Manager](../../plan-design/diagnostics/diagnostics-and-usage-data.md), reportados à Microsoft pelo servidor de site do Configuration Manager, são completamente separados do Windows Analytics e da telemetria do Windows.

## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Configurar clientes para reportar dados ao Windows Analytics

Para que os dispositivos cliente reportem os dados ao Windows Analytics, eles devem ser configurados com uma chave de ID Comercial associada ao espaço de trabalho do Operations Management Suite que hospeda os dados do Windows Analytics para a sua organização. Os dispositivos também devem ser configurados para reportar a telemetria em um nível de telemetria apropriado para a solução específica ou as soluções que você deseja usar. 

### <a name="configure-windows-analytics-client-settings"></a>Definir configurações de cliente de análise do Windows
Para configurar a análise do Windows, no console do Configuration Manager, escolha **Administração** > **Configurações do Cliente**, clique duas vezes em **Criar Configurações do Dispositivo Cliente Personalizado** e, em seguida, marque **Windows Analytics**.  

Depois de navegar até a guia de configurações do **Windows Analytics**, configure o seguinte:
  -  **ID comercial**  
A ID de chave comercial mapeia informações de dispositivos que você gerencia para o espaço de trabalho do OMS que hospeda os dados do Windows Analytics de sua organização. Se você já configurou uma ID comercial para uso com a Preparação para Atualização use essa ID. Se você ainda não tiver uma chave de ID comercial, veja [Gerar a chave de ID comercial]( https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key).

  -  **Nível de telemetria para dispositivos com Windows 10**   
Para saber mais sobre o que é coletado por cada nível de telemetria do Windows 10, veja [Configurar a telemetria do Windows em sua organização](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels).

  -  **Aceitar a coleta de dados comerciais em dispositivos com Windows 7, 8 e 8.1**   
Para obter informações sobre dados coletados desses sistemas operacionais quando você aceita, baixe o arquivo pdf [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields](https://go.microsoft.com/fwlink/?LinkID=822965) (Campos e eventos de telemetria de avaliação do Windows 7, Windows 8 e Windows 8.1) da Microsoft.

  -  **Configurar coleta de dados do Internet Explorer**  
Em dispositivos que executam o Windows 8.1 ou anteriores, a coleta de dados do Internet Explorer pode permitir que a Preparação para Atualização detecte incompatibilidades de aplicativos Web que poderiam impedir uma atualização tranquila para o Windows 10. A coleta de dados do Internet Explorer pode ser habilitada de acordo com a zona da internet. Para saber mais sobre as zonas de internet, veja [Sobre zonas de segurança de URL](https://msdn.microsoft.com/library/ms537183(v=vs.85).aspx).

## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Usar o Upgrade Readiness para identificar problemas de compatibilidade do Windows 10

O Upgrade Readiness (antigo Upgrade Analytics) permite que você analise a preparação e a compatibilidade do dispositivo com o Windows 10. Essa avaliação permite atualizações mais tranquilas. Após a conexão do Configuration Manager ao Upgrade Readiness, acesse os dados de compatibilidade de atualização do cliente diretamente no console do Configuration Manager. Você então poderá direcionar os aplicativos para atualização ou correção da lista de dispositivos.

Para obter mais informações e detalhes sobre como configurar e conectar-se ao Upgrade Readiness, confira [Upgrade Readiness](../../clients/manage/upgrade/upgrade-analytics.md).

## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Use o Windows Analytics para identificar lacunas em políticas de Proteção de Informações do Windows

Dispositivos com Windows 10 versão 1703 e posteriores configurados com uma política de WIP ([Proteção de Informações do Windows](https://docs.microsoft.com/en-us/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip)) reportam a telemetria em aplicativos que acessam dados corporativos em seu ambiente, mas que não contabilizados nas regras de aplicativo da política de WIP. Esses são aplicativos os quais os usuários em seu ambiente precisam que permaneçam produtivos, mas que estão com acesso bloqueado, portanto o conhecimento de que eles estão acessando dados corporativos pode ser útil na manutenção de suas políticas de Proteção de Informações do Windows no Configuration Manager. 

Esses dados de Proteção de Informações do Windows podem ser acessados usando essa [consulta do Operations Management Suite](https://go.microsoft.com/fwlink/?linkid=849952).
