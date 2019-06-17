---
title: Avaliação de compatibilidade
titleSuffix: Configuration Manager
description: Saiba mais sobre a avaliação de compatibilidade para aplicativos do Windows e os drivers na área de trabalho de análise.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: bef2c11732177dfb842f0961dc2d5d5a69edd55e
ms.sourcegitcommit: d47d2f03482e48d343e2139a341e61022331e6c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67148093"
---
# <a name="compatibility-assessment-in-desktop-analytics"></a>Avaliação de compatibilidade na área de trabalho de análise

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

As avaliações de atualização na análise do Windows foram genéricas, por exemplo: Necessária atenção ou correção disponível. Ele não fornece qualquer indicador visual sobre como priorizar aplicativos ou drivers com problemas ou atualizar informações. Análise da área de trabalho substitui esse recurso com **riscos de compatibilidade**. Análise da área de trabalho mostra a avaliação para aplicativos apenas na exibição de implantação para um cenário de pré-atualização. Ele categoriza os aplicativos com base em insights que Microsoft obtém das máquinas que está incluídas em um plano de implantação atual.

Análise da área de trabalho usa as seguintes categorias de avaliação de compatibilidade:

- **Baixa**: O serviço encontrado nenhum sinais para colocar em risco a esse aplicativo para um Windows atualizar. É provável que funcionam em SO de destino como-está.  

- **Médio**: Análise indica que o aplicativo pode portadores de deficiência funcionalidade, embora a correção é provavelmente possível.  

- **Alta**: O aplicativo é quase certo falhar durante ou após a atualização. Talvez seja necessário uma correção.  

- **Desconhecido**: O aplicativo não foi avaliado. Não há nenhuma outra informação, como *problemas conhecidos do MS* ou *pronto para o Windows*.  

Na lista de ativos de aplicativo ou driver em um plano de implantação, você verá esse valor para cada ativo na **riscos de compatibilidade** coluna.


## <a name="app-risk-assessment"></a>Avaliação de risco do aplicativo

Há várias fontes que a análise de área de trabalho usa para gerar a classificação de avaliação de aplicativos:

- [Problemas conhecidos do Microsoft](#microsoft-known-issues)
- [Pronto para o catálogo do Windows](#ready-for-windows)
- [Insights avançados](#advanced-insights)

Você pode encontrar a avaliação para cada fonte no aplicativo na área de trabalho de análise. Na lista de ativos de aplicativo em um plano de implantação, selecione um aplicativo individual para abrir seu painel de submenu de propriedades. Você verá um nível geral de avaliação e recomendação. O **fatores de risco de compatibilidade** seção mostra os detalhes para essas avaliações.


## <a name="microsoft-known-issues"></a>Problemas conhecidos do Microsoft

Análise da área de trabalho examina o banco de dados de compatibilidade do Microsoft app para todos os problemas conhecidos. Ele usa esse banco de dados para determinar todos os blocos existentes compatibilidade de aplicativos publicamente disponíveis da Microsoft ou outros editores. Essa verificação só se aplica ao SO de destino para o plano de implantação selecionado.

Você verá os seguintes problemas no painel de propriedades do aplicativo, como **problemas conhecidos do MS**:

### <a name="application-is-removed-during-upgrade"></a>Aplicativo é removido durante a atualização

Windows detectou problemas de compatibilidade. O aplicativo não migrar para a nova versão do sistema operacional. Nenhuma ação é necessária para a atualização continuar.

### <a name="blocking-upgrade"></a>Bloqueio de atualização

Windows detectou problemas de bloqueio e não é possível remover o aplicativo durante a atualização. Ele pode não funcionar na nova versão do sistema operacional. Antes de atualizar, remova o aplicativo. Reinstale e testá-lo na nova versão do sistema operacional.

### <a name="blocking-upgrade-but-can-be-reinstalled-after-upgrading"></a>Bloqueio de atualização, mas poderá ser reinstalado após a atualização

O aplicativo é compatível com a nova versão do sistema operacional, mas não migrar. Remova o aplicativo antes de atualizar o Windows. Reinstale-o na nova versão do sistema operacional.

### <a name="blocking-upgrade-update-application-to-newest-version"></a>Bloqueio de atualização, atualize o aplicativo para a versão mais recente

A versão existente do aplicativo não é compatível com a nova versão do sistema operacional e não migrar. Uma versão compatível do aplicativo está disponível. Atualize o aplicativo antes de atualizar.

### <a name="disk-encryption-blocking-upgrade"></a>Atualização de bloqueio de criptografia de disco

Recursos de criptografia do aplicativo bloqueiam a atualização. Desabilite o recurso de criptografia antes de atualizar o Windows e habilitá-lo após a atualização.

### <a name="does-not-work-with-new-os-but-wont-block-upgrade"></a>Não funciona com o novo sistema operacional, mas não bloquearão a atualização

O aplicativo não é compatível com a nova versão do sistema operacional, mas não bloquearão a atualização. Nenhuma ação é necessária para a atualização continuar. Instale uma versão compatível do aplicativo na nova versão do sistema operacional.

### <a name="does-not-work-with-new-os-and-will-block-upgrade"></a>Não funciona com o novo sistema operacional e bloqueará a atualização

O aplicativo não é compatível com a nova versão do sistema operacional e bloqueará a atualização. Remova o aplicativo antes de atualizar. Uma versão compatível do aplicativo pode estar disponível.

### <a name="evaluate-application-on-new-os"></a>Avaliar o aplicativo no novo sistema operacional

Windows irá migrar o aplicativo, mas ele detectou problemas que podem afetar o desempenho do aplicativo na nova versão do sistema operacional. Nenhuma ação é necessária para a atualização continuar. Teste o aplicativo na nova versão do sistema operacional.

### <a name="may-block-upgrade-test-application"></a>Pode bloquear a atualização, teste o aplicativo

Windows detectou problemas que podem interferir com a atualização, mas precisam de mais investigação. Teste o comportamento do aplicativo durante a atualização. Se ele bloqueia a atualização, remova-o antes de atualizar. Em seguida, reinstalá-lo e teste na nova versão do sistema operacional.

### <a name="multiple"></a>Vários

Vários problemas afetam o aplicativo. Selecione **consulta** para ver detalhes sobre os problemas detectados pelo Windows.

### <a name="reinstall-application-after-upgrading"></a>Reinstale o aplicativo após a atualização

O aplicativo é compatível com a nova versão do sistema operacional, mas você precisará reinstalá-lo após a atualização do Windows. O processo de atualização remove o aplicativo. Nenhuma ação é necessária para a atualização continuar. Reinstale o aplicativo na nova versão do sistema operacional.


## <a name="ready-for-windows"></a>Pronto para Windows

O [pronto para o Windows](https://www.readyforwindows.com) catálogo de aplicativos se correlaciona as fontes de dados a seguir:

- Dados de diagnóstico de outros clientes que se reportam os mesmos aplicativos
- Verificações adicionais da Microsoft, como blocos de compatibilidade em um dispositivo

As categorias possíveis são:

- **Altamente adotados**: Pelo menos 100.000 dispositivos Windows 10 comerciais instalou esse aplicativo.  

- **Adotado**: Pelo menos de 10.000 dispositivos Windows 10 comerciais instalou esse aplicativo.  

- **Dados insuficientes**: Muito poucos dispositivos Windows 10 comerciais estão compartilhando informações para esse aplicativo para a Microsoft categorizar sua adoção.

- **Entre em contato com o desenvolvedor**: Pode haver problemas de compatibilidade com esta versão do aplicativo. A Microsoft recomenda a entrar em contato com o fornecedor de software para saber mais. Para obter mais informações, consulte [pronto para o Windows](https://www.readyforwindows.com/).  

- **Desconhecido**: Não há nenhuma informação de pronto para Windows disponíveis para esta versão do aplicativo. Informações podem estar disponíveis para outras versões do aplicativo no [pronto para o Windows](https://www.readyforwindows.com/).  

### <a name="support-statement"></a>Instrução de suporte

Se o provedor de software oferece suporte a uma ou mais versões do aplicativo no Windows 10, você verá essa instrução no painel de propriedades do aplicativo. Na seção de fatores de risco de compatibilidade, examine os **oferecem suporte a instrução**.



## <a name="advanced-insights"></a>Insights avançados

Análise de área de trabalho também pode detectar problemas usando as seguintes informações adicionais:

### <a name="adopted-version-available"></a>Versão adotado disponível

Não há outra versão desse aplicativo que é altamente adotados por outros clientes. Esse sinal usa dados de pronto para Windows. Se houver qualquer bloqueadores de atualização com sua versão atual, considere implantar a versão alternativa em vez disso.

### <a name="driver-dependency"></a>Dependência de driver

O aplicativo depende de um driver. Análise da área de trabalho recomenda o aplicativo para teste do piloto. Ele deve funcionar bem para piloto, mas você encontrará quaisquer regressões. Se você tiver problemas, entre em contato com o publicador para solicitar uma versão que está em conformidade com o Windows 10.



## <a name="driver-risk-assessment"></a>Avaliação de risco de driver

Análise da área de trabalho também lista e agrupa pela disponibilidade de todos os drivers não migram para a versão do sistema operacional.

Você pode encontrar a avaliação no driver na área de trabalho de análise. Na lista de ativos de driver em um plano de implantação, selecione um driver individual para abrir seu painel de submenu de propriedades. Você verá um nível geral de avaliação e recomendação. O **fatores de risco de compatibilidade** seção mostra os detalhes para essas avaliações.

| Disponibilidade de drivers | Ação necessária? | O que significa | Orientação |
|---------------------|------------------|---------------|----------|
| Na caixa disponível | Não, para que o reconhecimento somente | A versão atualmente instalada de um aplicativo ou driver não migrar para a nova versão do sistema operacional. Uma versão compatível é instalada com a nova versão do sistema operacional. | Nenhuma ação é necessária para a atualização continuar. |
| Importar do Windows Update | Sim | A versão atualmente instalada de um driver não migrar para a nova versão do sistema operacional. Uma versão compatível está disponível no Windows Update. | Se o computador recebe automaticamente as atualizações do Windows Update, nenhuma ação é necessária. Caso contrário, importe um novo driver do Windows Update após a atualização do Windows. |
| Na caixa disponível e do Windows Update | Sim | A versão atualmente instalada de um driver não migrar para a nova versão do sistema operacional. Embora um novo driver seja instalado durante a atualização, uma versão mais recente está disponível no Windows Update. | Se o computador recebe automaticamente as atualizações do Windows Update, nenhuma ação é necessária. Caso contrário, importe um novo driver do Windows Update após a atualização do Windows. |
| Entre em contato com o fornecedor | Sim | O driver não migrar para a nova versão do sistema operacional e análise de área de trabalho não é possível localizar uma versão compatível. | Para uma solução, verifique com o fornecedor independente de hardware (IHV) que fabrica o driver ou o fabricante original do equipamento (OEM) que forneceu o dispositivo. |


## <a name="see-also"></a>Consulte também

O benefício de centro FastTrack para Windows 10 fornece acesso aos **aplicativo de área de trabalho garantir**. Esse benefício é um novo serviço projetado para resolver problemas com a compatibilidade de aplicativo do Office 365 ProPlus e Windows 10. Para obter mais informações, consulte [aplicativo de área de trabalho garantir](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
