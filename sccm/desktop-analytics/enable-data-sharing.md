---
title: Habilitar o compartilhamento de dados
titleSuffix: Configuration Manager
description: Um guia de referência para o compartilhamento de dados de diagnóstico com a análise de área de trabalho.
ms.date: 06/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: dbe161fd744343927f0b373775182eccfd58c1b6
ms.sourcegitcommit: a6a6507e01d819217208cfcea483ce9a2744583d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66748244"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Habilitar o compartilhamento de área de trabalho de análise de dados

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Para registrar dispositivos para análise de área de trabalho, eles precisam enviar dados de diagnóstico à Microsoft. Se seu ambiente usa um servidor proxy, use essas informações para ajudar a configurar o proxy.


## <a name="diagnostic-data-levels"></a>Níveis de dados de diagnóstico

![Diagrama de níveis de dados de diagnóstico para análise de área de trabalho](media/diagnostic-data-levels.png)

Quando você integra o Configuration Manager com a análise de área de trabalho, você também usá-lo para gerenciar o nível de dados de diagnóstico em dispositivos. Para obter a melhor experiência, use o Configuration Manager.

A funcionalidade básica da área de trabalho de análise funciona na **básica** nível de dados de diagnóstico. Você não obterá dados de uso ou a integridade de seus dispositivos atualizados sem habilitar a **avançado (limitado)** nível. A Microsoft recomenda que você habilite o **avançado (limitado)** nível de dados de diagnóstico. Para obter mais informações, consulte [Windows 10 aprimorada eventos de dados de diagnóstico e os campos usados pelo Windows Analytics](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)).

Para obter mais informações, consulte [privacidade de área de trabalho de análise](/sccm/desktop-analytics/privacy).

Os artigos a seguir também são bons recursos para melhor entender os níveis de dados de diagnóstico do Windows:

- [Windows 10 e o GDPR para tomadores de decisões](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configurar dados de diagnóstico do Windows em sua organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!Note]  
> O nível avançado (limitado), quando cada cliente faz a verificação completa inicial, ele envia aproximadamente de 2 MB de dados para a nuvem da Microsoft. O delta diário varia entre 400 250 KB por dia.
>
> A verificação diária de delta acontece às 3 horas (hora local do dispositivo). Alguns eventos são enviados na primeira vez disponível ao longo do dia. Esses tempos não são configuráveis.
>
> Para saber mais, veja [Configurar dados de diagnóstico do Windows em sua organização](https://aka.ms/enterprisetelemetry).  



## <a name="endpoints"></a>Pontos de extremidade

Para habilitar o compartilhamento de dados, configure o servidor de proxy para permitir que os pontos de extremidade a seguir:

> [!Important]  
> Por privacidade e integridade dos dados, o Windows verifica um certificado SSL da Microsoft ao se comunicar com os pontos de extremidade de dados de diagnóstico. Inspeção e interceptação de SSL não são possíveis. Para usar a análise de área de trabalho, exclua esses pontos de extremidade de inspeção de SSL.<!-- BUG 4647542 -->

| Ponto de extremidade  | Função  |
|-----------|-----------|
| `https://v10c.events.data.microsoft.com` | Experiência do usuário conectado e o ponto de extremidade de diagnóstico de componente. Usado por dispositivos que executam o Windows 10, versão 1703 ou posterior, com o 2018-09 cumulativo de atualização ou posterior instalado. |
| `https://v10.events.data.microsoft.com` | Experiência do usuário conectado e o ponto de extremidade de diagnóstico de componente. Usado por dispositivos que executam o Windows 10, versão 1803 ou posterior, _sem_ a atualização cumulativa de 2018-09 instalada. |
| `https://v10.vortex-win.data.microsoft.com` | Experiência do usuário conectado e o ponto de extremidade de diagnóstico de componente. Usado por dispositivos que executam o Windows 10, versão 1709 ou anterior. |
| `https://vortex-win.data.microsoft.com` | Experiência do usuário conectado e o ponto de extremidade de diagnóstico de componente. Usado pelos dispositivos que executam o Windows 7 e Windows 8.1 |
| `https://settings-win.data.microsoft.com` | Permite que a atualização de compatibilidade enviar dados à Microsoft. |
| `http://adl.windows.com` | Permite que a atualização de compatibilidade para receber os dados de compatibilidade mais recentes da Microsoft. |
| `https://watson.telemetry.microsoft.com` | Erro do Windows (WER) de emissão de relatórios. Necessário para monitorar a integridade da implantação no Windows 10, versão 1803 ou anterior. |
| `https://umwatsonc.events.data.microsoft.com` | Erro do Windows (WER) de emissão de relatórios. Necessário para relatórios de integridade do dispositivo no Windows 10, versão 1809 ou posterior. |
| `https://ceuswatcab01.blob.core.windows.net`<br> `https://ceuswatcab02.blob.core.windows.net`<br> `https://eaus2watcab01.blob.core.windows.net`<br> `https://eaus2watcab02.blob.core.windows.net`<br> `https://weus2watcab01.blob.core.windows.net`<br> `https://weus2watcab02.blob.core.windows.net` | Erro do Windows (WER) de emissão de relatórios. Necessário para monitorar a integridade da implantação no Windows 10, versão 1809 ou posterior. |
| `https://www.msftncsi.com` | Erro do Windows (WER) de emissão de relatórios. Necessário para a integridade do dispositivo verificar a conectividade. |
| `https://www.msftconnecttest.com` | Erro do Windows (WER) de emissão de relatórios. Necessário para a integridade do dispositivo verificar a conectividade. |
| `https://kmwatsonc.events.data.microsoft.com` | Análise online de pane. Necessário para relatórios de integridade do dispositivo no Windows 10, versão 1809 ou posterior. |
| `https://oca.telemetry.microsoft.com`  | Online Crash Analysis (OCA). Necessário para monitorar a integridade da implantação no Windows 10, versão 1803 ou anterior. |
| `https://login.live.com` | Deve para fornecer uma identidade de dispositivo mais confiável para a área de trabalho de análise. <br> <br>Para desabilitar o acesso à conta do usuário final Microsoft, use as configurações de política em vez de bloquear esse ponto de extremidade. Para obter mais informações, consulte [conta da Microsoft na empresa](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication). |
| `https://nexusrules.officeapps.live.com` | Para a funcionalidade futura <!-- Used to request dynamic diagnostic data events from Office clients. This data is useful for drill-down and diagnostics purposes in the Desktop Analytics portal --> |
| `https://nexus.officeapps.live.com` | Para a funcionalidade futura <!-- Used by Office clients to send diagnostic data events from Office 14, Office 15, and versions of Office 16 earlier than 16.0.8702. It's used to collect usage and reliability signals events for Desktop Analytics. --> |
| `https://office.pipe.aria.microsoft.com` | Para a funcionalidade futura <!-- Used by Office clients to send diagnostic data events from universal/modern Office apps, and Win32 Office 16 versions later than 16.0.8702. It's used to collect usage and reliability signals events for Desktop Analytics. --> |
| `https://graph.windows.net` | Usado para recuperar automaticamente as configurações como CommercialId ao anexar a sua hierarquia para análise de área de trabalho (na função de servidor do Configuration Manager somente). |
| `https://fef.msua06.manage.microsoft.com` | Usado para associações de coleção de dispositivo de sincronização, planos de implantação e status de preparação do dispositivo com a análise de área de trabalho (na função de servidor do Configuration Manager somente). |


## <a name="proxy-server-authentication"></a>Autenticação do servidor proxy

Certifique-se de que um proxy não impeça que os dados de diagnóstico devido a autenticação. Se sua organização usa a autenticação do servidor proxy para o tráfego de saída, use um ou mais das seguintes abordagens:

- **Bypass** (recomendado): Configure seus servidores proxy para não exigir autenticação de proxy para o tráfego para os pontos de extremidade de dados de diagnóstico. Essa opção é a solução mais abrangente. Ele funciona para todas as versões do Windows 10.  

- **Autenticação de proxy do usuário**: Configure dispositivos para usar o contexto do usuário conectado para autenticação de proxy. Esse método requer que os dispositivos que executam o Windows 10, versão 1703 ou posterior. Certifique-se de que os usuários têm permissão de proxy para acessar os pontos de extremidade de dados de diagnóstico. Essa opção exige que os dispositivos têm os usuários do console com permissões de proxy, portanto, você não pode usar esse método com dispositivos sem periféricos.  

- **Autenticação de proxy do dispositivo**:

    - Configure um servidor proxy de nível de sistema nos dispositivos.  
    - Configure esses dispositivos para usar a autenticação de proxy de saída com base no dispositivo.  
    - Configure servidores de proxy para permitir que as contas de computador acessar os pontos de extremidade de dados de diagnóstico.  
