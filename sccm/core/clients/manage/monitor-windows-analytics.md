---
title: Monitorar os clientes com o Windows Analytics
titleSuffix: Configuration Manager
description: O Windows Analytics é um conjunto de soluções que permitem que você obtenha informações importantes sobre o estado atual de seu ambiente.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8405a212f9e4cd845ac7591767eb27e5425f404e
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893644"
---
# <a name="use-windows-analytics-with-configuration-manager"></a>Usar o Windows Analytics com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

O [Windows Analytics](https://docs.microsoft.com/windows/deployment/update/windows-analytics-overview) é um conjunto de soluções que permitem que você consiga informações sobre o estado atual de seu ambiente. Os dispositivos do Windows em seu ambiente reportam dados à Microsoft, que você pode acessar e analisar por meio dessas soluções. Por exemplo, conecte o [Upgrade Readiness](/sccm/core/clients/manage/upgrade-readiness) ao Configuration Manager para acessar diretamente os dados no espaço de trabalho **Monitoramento** do console do Configuration Manager.

Os dados usados pelo Windows Analytics não são transferidos diretamente ao servidor de site do Configuration Manager. Os computadores cliente enviam dados para o serviço de nuvem do Windows. Em seguida, esse serviço transfere os dados relevantes para soluções do Windows Analytics hospedadas em um dos espaços de trabalho de sua organização. Então, o Configuration Manager direciona você para os dados relevantes no portal da Web com links no contexto. Ele também pode diretamente exibir os dados que fazem parte das soluções que você conecta ao Configuration Manager.

> [!Important]  
> O Configuration Manager reporta dados de uso e diagnóstico para a Microsoft. Esses dados são separados dos dados do Windows Analytics. Para obter mais informações, consulte [Dados de diagnóstico e de uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  



## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Configurar clientes para reportar dados ao Windows Analytics

Para que os dispositivos de cliente relatem dados para o Windows Analytics, configure-os com uma *chave de ID comercial*. Essa chave é o espaço de trabalho do Azure Log Analytics que hospeda os dados do Windows Analytics. Além disso, configure os dispositivos para relatar dados em um nível apropriado para as soluções específicas que você deseja usar. 

### <a name="configure-windows-analytics-client-settings"></a>Definir configurações de cliente de análise do Windows
Para definir configurações do Windows Analytics: 
1. No console do Configuration Manager, vá até o espaço de trabalho **Administração** e selecione o nó **Configurações do Cliente**.  
2. Na faixa de opções, selecione **Criar Configurações Personalizadas do Cliente do Dispositivo**.  
3. Adicione o grupo **Windows Analytics** a essa política de configurações personalizadas do dispositivo cliente.  

Para saber mais sobre como criar configurações personalizadas do dispositivo do cliente, veja [Como definir as configurações do cliente](/sccm/core/clients/deploy/configure-client-settings).

Selecione a guia de configurações **Windows Analytics** e defina as seguintes configurações:  

#### <a name="manage-windows-telemetry-settings-with-configuration-manager"></a>Gerenciar as configurações de telemetria do Windows com o Configuration Manager
Defina essa configuração como **Sim** para definir configurações de dados de diagnóstico do Windows em clientes do Windows.   

#### <a name="commercial-id-key"></a>Chave da ID comercial
A ID de chave comercial mapeia informações de dispositivos que você gerencia para o espaço de trabalho do Log Analytics que hospeda os dados do Windows Analytics de sua organização. Se você já configurou uma ID comercial para uso com a Upgrade Readiness, use essa ID. Se você ainda não tiver uma chave de ID comercial, veja [Copiar a chave de ID comercial](https://docs.microsoft.com/windows/deployment/update/windows-analytics-get-started#copy-your-commercial-id-key).

#### <a name="windows-10-telemetry"></a>Telemetria do Windows 10
Para saber mais, veja [Configurar dados de diagnóstico do Windows em sua organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization##diagnostic-data-level).

> [!Note]  
> Também é possível definir o nível de coleta de dados do Windows 10 como **Avançado (Limitado)**. Essa configuração permite que você obtenha informações acionáveis sobre dispositivos em seu ambiente sem que os dispositivos relatem todos os dados no nível **Avançado** com Windows 10 versão 1709 ou posterior. O nível Avançado (Limitado) inclui métricas do nível Básico, bem como um subconjunto dos dados coletados do nível Avançado relevantes ao Windows Analytics.

#### <a name="windows-81-and-earlier-telemetry"></a>Telemetria do Windows 8.1 e anterior   
Para obter mais informações, consulte [Campos e eventos de telemetria do avaliador do Windows 7, Windows 8 e Windows 8.1](https://go.microsoft.com/fwlink/?LinkID=822965).

#### <a name="enable-windows-81-and-earlier-internet-explorer-data-collection"></a>Habilitar a coleta de dados do Windows 8.1 e do Internet Explorer anterior
Em dispositivos que executam o Windows 8.1 ou anterior, o Internet Explorer pode coletar dados sobre os aplicativos Web. Esses dados podem permitir que a Upgrade Readiness detecte incompatibilidades de aplicativos Web que poderiam impedir uma atualização tranquila para o Windows 10. Habilite a coleta de dados do Internet Explorer com base na zona da Internet. Para saber mais sobre as zonas de internet, veja [Sobre zonas de segurança de URL](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms537183\(v=vs.85\)).



## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Usar o Upgrade Readiness para identificar problemas de compatibilidade do Windows 10

O Upgrade Readiness permite que você analise a preparação e a compatibilidade do dispositivo com o Windows 10. Essa avaliação permite atualizações mais tranquilas. Após a conexão do Configuration Manager ao Upgrade Readiness, acesse esses dados de compatibilidade de upgrade do cliente diretamente no console do Configuration Manager. Em seguida, direcione dispositivos para upgrade ou correção na lista de dispositivos.

Para obter mais informações e detalhes sobre como configurar e conectar-se ao Upgrade Readiness, confira [Upgrade Readiness](/sccm/core/clients/manage/upgrade-readiness).



## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Use o Windows Analytics para identificar lacunas em políticas de Proteção de Informações do Windows

Você pode configurar o Windows 10 versão 1703 e os dispositivos posteriores com uma política de [Proteção de Informações do Windows](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP). Eles relatam dados de diagnóstico em aplicativos que acessam dados corporativos em seu ambiente, mas que não estão incluídos nas regras de aplicação da política. Os usuários podem precisar desses aplicativos para permanecerem produtivos, mas o WIP bloqueia o acesso dos usuários. Essas informações são úteis para manter suas políticas de Proteção de Informações do Windows no Configuration Manager. 

