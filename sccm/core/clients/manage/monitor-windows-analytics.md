---
title: Monitorar os clientes com o Windows Analytics
titleSuffix: Configuration Manager
description: O Windows Analytics é um conjunto de soluções executado no Operations Management Suite que permite a obtenção de informações valiosas sobre o estado atual de seu ambiente, aproveitando os dados telemétricos do Windows informados por dispositivos em seu ambiente.
ms.custom: na
ms.date: 01/02/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
caps.latest.revision: 23
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 15b1d07f35f774f3ec8f082a86c90ecb989a438e
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="use-windows-analytics-with-configuration-manager"></a>Usar o Windows Analytics com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O [Windows Analytics](https://www.microsoft.com/WindowsForBusiness/windows-analytics) é um conjunto de soluções executado no OMS [(Operations Management Suite)](/azure/operations-management-suite/operations-management-suite-overview). Essas soluções permitem que você obtenha informações sobre o estado atual de seu ambiente. Os dispositivos em seus dados de telemetria do Windows do relatório de ambiente podem ser acessados e analisados por meio de soluções no [Portal da Web do Operations Management Suite](https://mms.microsoft.com). Conectando o [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) ao Configuration Manager, você pode acessar diretamente os dados no nó **Monitoramento** do console do Configuration Manager.

Os dados telemétricos do Windows usados pelo Windows Analytics não são transferidos diretamente ao servidor de site do Configuration Manager. Computadores cliente enviam dados telemétricos do Windows para o serviço de telemetria do Windows. Em seguida, esse serviço transfere os dados relevantes para soluções do Windows Analytics hospedadas em um dos espaços de trabalho do OMS de sua organização. O Configuration Manager pode então direcioná-lo para os dados relevantes no portal da Web com links no contexto ou exibir diretamente dados que fazem parte das soluções que você conectou ao Configuration Manager. Também é possível consultar diretamente os dados no portal da Web do Operation Management Suite.

>[!Important]
>[Dados de diagnóstico e uso do Configuration Manager](../../plan-design/diagnostics/diagnostics-and-usage-data.md), relatados à Microsoft pelo servidor de site do Configuration Manager, são separados do Windows Analytics e da telemetria do Windows.

## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Configurar clientes para reportar dados ao Windows Analytics

Para que os dispositivos cliente relatem dados para o Windows Analytics, é necessário configurar dispositivos com uma chave de ID Comercial associada ao espaço de trabalho do OMS que hospeda os dados do Windows Analytics. Também é necessário configurar os dispositivos para relatar a telemetria em um nível de telemetria apropriado para as soluções específicas que você deseja usar. 

### <a name="configure-windows-analytics-client-settings"></a>Definir configurações de cliente de análise do Windows
Para configurar a análise do Windows, no console do Configuration Manager, escolha **Administração** > **Configurações do Cliente**, clique duas vezes em **Criar Configurações do Dispositivo Cliente Personalizado** e, em seguida, marque **Windows Analytics**.  

Depois de navegar para a guia de configurações **Windows Analytics**, defina as seguintes configurações:
  -  **Chave da ID comercial**  
A ID de chave comercial mapeia informações de dispositivos que você gerencia para o espaço de trabalho do OMS que hospeda os dados do Windows Analytics de sua organização. Se você já configurou uma ID comercial para uso com a Preparação para Atualização use essa ID. Se você ainda não tiver uma chave de ID comercial, veja [Gerar a chave de ID comercial]( https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key).

  -  **Nível de telemetria para dispositivos com Windows 10**   
Para obter mais informações sobre cada nível de telemetria do Windows 10, consulte [Configurar a telemetria do Windows em sua organização](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels).

   > [!Note]
   > Com a atualização 1710, você pode definir o nível de coleta de dados da telemetria do Windows 10 para **Avançado (Limitado)**. Essa configuração permite que você obtenha informações acionáveis sobre dispositivos em seu ambiente sem que os dispositivos reportem todos os dados no nível de telemetria **Avançado** com Windows 10 versão 1709 ou posterior. O nível de telemetria Avançado (Limitado) inclui métricas do nível Básico, bem como um subconjunto dos dados coletados do nível Avançado relevantes ao Windows Analytics.


  -  **Aceitar a coleta de dados comerciais em dispositivos com Windows 7, 8 e 8.1**   
Para obter mais informações, consulte [Campos e eventos de telemetria do avaliador do Windows 7, Windows 8 e Windows 8.1](https://go.microsoft.com/fwlink/?LinkID=822965).

  -  **Configurar coleta de dados do Internet Explorer**  
Em dispositivos que executam o Windows 8.1 ou anteriores, a coleta de dados do Internet Explorer pode permitir que a Preparação para Atualização detecte incompatibilidades de aplicativos Web que poderiam impedir uma atualização tranquila para o Windows 10. A coleta de dados do Internet Explorer pode ser habilitada de acordo com a zona da internet. Para saber mais sobre as zonas de internet, veja [Sobre zonas de segurança de URL](https://msdn.microsoft.com/library/ms537183(v=vs.85).aspx).

## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Usar o Upgrade Readiness para identificar problemas de compatibilidade do Windows 10

O Upgrade Readiness (antigo Upgrade Analytics) permite que você analise a preparação e a compatibilidade do dispositivo com o Windows 10. Essa avaliação permite atualizações mais tranquilas. Após a conexão do Configuration Manager ao Upgrade Readiness, acesse esses dados de compatibilidade de upgrade do cliente diretamente no console do Configuration Manager. Em seguida, direcione dispositivos para upgrade ou correção na lista de dispositivos.

Para obter mais informações e detalhes sobre como configurar e conectar-se ao Upgrade Readiness, confira [Upgrade Readiness](../../clients/manage/upgrade/upgrade-analytics.md).

## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Use o Windows Analytics para identificar lacunas em políticas de Proteção de Informações do Windows

Dispositivos Windows 10 versão 1703 e posteriores configurados com uma política do WIP ([Proteção de Informações do Windows](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip)) relatam a telemetria em aplicativos que acessam dados corporativos em seu ambiente, mas que as regras de aplicativo da política do WIP não incluem. Os usuários podem precisar desses aplicativos para permanecerem produtivos, mas o WIP bloqueia o acesso dos usuários. O conhecimento de que os usuários estão acessando dados corporativos é útil na manutenção de suas políticas da Proteção de Informações do Windows no Configuration Manager. 

Acesse esses dados da Proteção de Informações do Windows usando esta [consulta do Operations Management Suite](https://go.microsoft.com/fwlink/?linkid=849952).