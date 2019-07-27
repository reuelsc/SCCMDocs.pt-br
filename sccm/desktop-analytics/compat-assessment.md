---
title: Avaliação de compatibilidade
titleSuffix: Configuration Manager
description: Saiba mais sobre a avaliação de compatibilidade para aplicativos e drivers do Windows no desktop Analytics.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: f6181f0e1a502d701ca7337641013a18b03251f9
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68535992"
---
# <a name="compatibility-assessment-in-desktop-analytics"></a>Avaliação de compatibilidade no desktop Analytics

> [!Note]  
> Essas informações se relacionam a um serviço de visualização que pode ser substancialmente modificado antes de ser lançada comercialmente. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

As avaliações de atualização no Windows Analytics eram genéricas, por exemplo: Atenção necessária ou correção disponível. Ele não fornece nenhum indicador visual sobre como priorizar aplicativos ou drivers com problemas ou informações de atualização. A análise de desktops substitui esse recurso por **risco de compatibilidade**. A análise de desktops mostra a avaliação de aplicativos somente no modo de exibição de implantação para um cenário anterior à atualização. Ele categoriza os aplicativos com base nas informações que a Microsoft obtém dos computadores incluídos em um plano de implantação atual.

A análise de desktops usa as seguintes categorias de avaliação de compatibilidade:

- **Baixa**: O serviço não encontrou sinais para colocar este aplicativo em risco para uma atualização do Windows. É provável que ele funcione no so de destino como está.  

- **Médio**: O Analytics indica que o aplicativo pode ter uma funcionalidade prejudicada, embora seja provável que a correção seja possível.  

- **Alta**: O aplicativo tem quase certeza de falha durante ou após a atualização. Ele pode precisar de uma correção.  

- **Desconhecido**: O aplicativo não foi avaliado. Não há outras informações, como *problemas conhecidos do MS* ou *prontos para o Windows*.  

Na lista de ativos de aplicativo ou de driver em um plano de implantação, você verá esse valor para cada ativo na coluna **risco de compatibilidade** .


## <a name="app-risk-assessment"></a>Avaliação de risco do aplicativo

![Diagrama de fontes de avaliação de risco do aplicativo](media/app-risk-assessment-sources.png)

Há várias fontes que a análise de desktop usa para gerar a classificação de avaliação para aplicativos:

- [Problemas conhecidos da Microsoft](#microsoft-known-issues)
- [Pronto para o catálogo do Windows](#ready-for-windows)
- [Informações avançadas](#advanced-insights)

Você pode encontrar a avaliação de cada fonte no aplicativo na análise de desktops. Na lista de ativos de aplicativo em um plano de implantação, selecione um aplicativo individual para abrir seu painel submenu de propriedades. Você verá um nível geral de recomendação e avaliação. A seção **fatores de risco de compatibilidade** mostra os detalhes dessas avaliações.


## <a name="microsoft-known-issues"></a>Problemas conhecidos da Microsoft

A análise de desktops examina o banco de dados do Microsoft App Compatibility em busca de problemas conhecidos. Ele usa esse banco de dados para determinar quaisquer blocos de compatibilidade existentes para aplicativos publicamente disponíveis da Microsoft ou de outros publicadores. Essa verificação só se aplica ao sistema operacional de destino para o plano de implantação selecionado.

Você verá os seguintes problemas no painel de propriedades do aplicativo como **problemas conhecidos do MS**:

### <a name="application-is-removed-during-upgrade"></a>O aplicativo é removido durante a atualização

O Windows detectou problemas de compatibilidade. O aplicativo não migrará para a nova versão do sistema operacional. Nenhuma ação é necessária para que a atualização continue.

### <a name="blocking-upgrade"></a>Atualização de bloqueio

O Windows detectou problemas de bloqueio e não pode remover o aplicativo durante a atualização. Ele pode não funcionar na nova versão do sistema operacional. Antes de atualizar, remova o aplicativo. Reinstale-o e teste-o na nova versão do sistema operacional.

### <a name="blocking-upgrade-but-can-be-reinstalled-after-upgrading"></a>Bloqueio de atualização, mas pode ser reinstalado após a atualização

O aplicativo é compatível com a nova versão do sistema operacional, mas não migra. Remova o aplicativo antes de atualizar o Windows. Reinstale-o na nova versão do sistema operacional.

### <a name="blocking-upgrade-update-application-to-newest-version"></a>Bloqueando a atualização, atualizando o aplicativo para a versão mais recente

A versão existente do aplicativo não é compatível com a nova versão do sistema operacional e não será migrada. Uma versão compatível do aplicativo está disponível. Atualize o aplicativo antes de atualizar.

### <a name="disk-encryption-blocking-upgrade"></a>Atualização de bloqueio de criptografia de disco

Os recursos de criptografia do aplicativo bloqueiam a atualização. Desabilite o recurso de criptografia antes de atualizar o Windows e habilitá-lo após a atualização.

### <a name="does-not-work-with-new-os-but-wont-block-upgrade"></a>Não funciona com o novo sistema operacional, mas não bloqueia a atualização

O aplicativo não é compatível com a nova versão do sistema operacional, mas não bloqueará a atualização. Nenhuma ação é necessária para que a atualização continue. Instale uma versão compatível do aplicativo na nova versão do sistema operacional.

### <a name="does-not-work-with-new-os-and-will-block-upgrade"></a>Não funciona com o novo sistema operacional e bloqueará a atualização

O aplicativo não é compatível com a nova versão do sistema operacional e bloqueará a atualização. Remova o aplicativo antes de atualizar. Uma versão compatível do aplicativo pode estar disponível.

### <a name="evaluate-application-on-new-os"></a>Avaliar o aplicativo no novo sistema operacional

O Windows migrará o aplicativo, mas detectou problemas que podem afetar o desempenho do aplicativo na nova versão do sistema operacional. Nenhuma ação é necessária para que a atualização continue. Teste o aplicativo na nova versão do sistema operacional.

### <a name="may-block-upgrade-test-application"></a>Pode bloquear a atualização, o aplicativo de teste

O Windows detectou problemas que podem interferir na atualização, mas precisam de mais investigações. Teste o comportamento do aplicativo durante a atualização. Se ele bloquear a atualização, remova-a antes de atualizar. Em seguida, reinstale-o e teste a nova versão do sistema operacional.

### <a name="multiple"></a>Vários

Vários problemas afetam o aplicativo. Selecione **consulta** para ver detalhes sobre os problemas detectados pelo Windows.

### <a name="reinstall-application-after-upgrading"></a>Reinstalar o aplicativo após a atualização

O aplicativo é compatível com a nova versão do sistema operacional, mas você precisa reinstalá-lo depois de atualizar o Windows. O processo de atualização remove o aplicativo. Nenhuma ação é necessária para que a atualização continue. Reinstale o aplicativo na nova versão do sistema operacional.


## <a name="ready-for-windows"></a>Pronto para o Windows

O catálogo [de aplicativos pronto para Windows](https://www.readyforwindows.com) correlaciona as seguintes fontes de dados:

- Dados de diagnóstico de outros clientes que relatam os mesmos aplicativos
- Verificações adicionais da Microsoft, como blocos de compatibilidade em um dispositivo

As categorias possíveis são:

- **Altamente adotado**: Pelo menos 100.000 dispositivos comerciais do Windows 10 instalaram este aplicativo.  

- **Adotado**: Pelo menos 10.000 dispositivos comerciais do Windows 10 instalaram este aplicativo.  

- **Dados**insuficientes: Poucos dispositivos comerciais do Windows 10 estão compartilhando informações para este aplicativo para a Microsoft categorizar sua adoção.

- **Contatar desenvolvedor**: Pode haver problemas de compatibilidade com esta versão do aplicativo. A Microsoft recomenda entrar em contato com o provedor de software para saber mais. Para obter mais informações, consulte [pronto para o Windows](https://www.readyforwindows.com/).  

- **Desconhecido**: Não há informações prontas para o Windows disponíveis para esta versão deste aplicativo. As informações podem estar disponíveis para outras versões do aplicativo em [pronto para o Windows](https://www.readyforwindows.com/).  

### <a name="support-statement"></a>Instrução de suporte

Se o provedor de software oferecer suporte a uma ou mais versões deste aplicativo no Windows 10, você verá essa instrução no painel de propriedades do aplicativo. Na seção fatores de risco de compatibilidade, examine a **instrução de suporte**.



## <a name="advanced-insights"></a>Informações avançadas

O desktop Analytics também pode detectar problemas usando as seguintes informações adicionais:

### <a name="adopted-version-available"></a>Versão adotada disponível

Há outra versão desse aplicativo que é altamente adotada por outros clientes. Esse sinal usa dados de prontos para o Windows. Se houver algum bloqueador de atualização com sua versão atual, considere implantar a versão alternativa.

### <a name="driver-dependency"></a>Dependência do driver

O aplicativo é dependente de um driver. A análise de desktops recomenda o aplicativo para teste piloto para descobrir qualquer regressão. Se você tiver problemas, entre em contato com o editor para solicitar uma versão compatível com o Windows 10.

### <a name="additional-insights"></a>Informações adicionais

<!-- 4021225 -->
Quando você atualiza o site Configuration Manager e os clientes para a versão 1906, os clientes também relatam essas informações adicionais:

> [!Important]  
> Para aproveitar ao máximo os novos recursos do Configuration Manager, depois de atualizar o site, atualize também os clientes para a versão mais recente. Esse cenário não funciona até que a versão do cliente também seja a mais recente.

#### <a name="16-bit-apps"></a>aplicativos de 16 bits

Remova todos os componentes de 16 bits de aplicativos e substitua pelos equivalentes de 32 bits ou 64 bits. Para obter mais informações, [consulte a história do desenvolvedor do Windows Vista e do Windows Server 2008: Manual](https://docs.microsoft.com/previous-versions/aa480152\(v=msdn.10\))de compatibilidade de aplicativos.

A outra opção é habilitar o NTVDM (computador virtual DOS) do NT para suporte no Windows 10.

#### <a name="requires-admin-privileges"></a>Requer privilégios de administrador

O aplicativo exige que o usuário tenha acesso administrativo ao dispositivo. Use um manifesto de aplicativo para esses aplicativos que exigem permissões de administrador. Para obter mais informações, consulte [criar e inserir um manifesto de aplicativo](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\)).

A análise de desktops recomenda o aplicativo para teste piloto para descobrir qualquer regressão.

#### <a name="java-dependency"></a>Dependência de Java

Muitos aplicativos Java dependem de um Java Runtime Environment instalado separadamente (JRE). Embora as versões mais antigas do JRE possam continuar a funcionar no Windows 10, a Oracle dá suporte apenas às versões mais recentes do JRE. O uso de um JRE sem suporte mais antigo pode ter vulnerabilidades de segurança. Verifique se o aplicativo é executado nas versões mais recentes do JRE.

#### <a name="not-dpi-aware"></a>Reconhecimento de não-DPI

O aplicativo pode ter problemas de exibição com resoluções de tela avançadas no Windows 10. Use um manifesto de aplicativo para evitar problemas com altas resoluções de DPI. Para obter mais informações, consulte manifestos do [aplicativo](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests).

A análise de desktops recomenda o aplicativo para teste piloto para descobrir qualquer regressão.

#### <a name="silverlight-framework"></a>Estrutura do Silverlight

A Microsoft recomenda que aplicativos não baseados em navegador não usem o Silverlight. A data de término do suporte para o Silverlight 5 é de outubro de 2021.

A maioria dos navegadores da Web atuais não oferece suporte ao Silverlight.

| Navegador | Suporte |
|---------|---------|
| Google Chrome | Fim do suporte: Setembro de 2015 |
| Firefox | Fim do suporte: Março de 2017 |
| Microsoft Edge | Nenhum plug-in disponível |

A análise de desktops recomenda o aplicativo para teste piloto para descobrir qualquer regressão.

#### <a name="net-framework-1011"></a>.NET Framework 1.0/1.1

A versão 1,0 do .NET Framework não tem suporte no Windows 10. A versão 1,1 não é compatível com o Windows 10. Se o aplicativo for de um Publicador de terceiros, entre em contato com o fornecedor para solicitar uma versão compatível com o Windows 10. Caso contrário, desenvolva o aplicativo para usar uma versão com suporte do .NET.

#### <a name="net-framework-2030"></a>.NET Framework 2.0/3.0

As estruturas do .NET 2,0 e 3,5 têm suporte no Windows 10. Talvez seja necessário habilitar o recurso do Windows. Para obter mais informações, consulte [instalar o .NET Framework 3,5 no Windows 10](https://docs.microsoft.com/dotnet/framework/install/dotnet-35-windows-10).

#### <a name="ui-access"></a>Acesso à interface do usuário

Os aplicativos com acesso à interface do usuário podem ignorar os níveis de controle da interface para direcionar a entrada para janelas de privilégio mais altas na área de trabalho. Use essa configuração somente para aplicativos de tecnologia assistencial de interface do usuário.

Se você não estiver usando recursos de acessibilidade em seu aplicativo, defina o sinalizador de acesso da interface do usuário no manifesto do aplicativo como false. Para obter mais informações, consulte [criar e inserir um manifesto de aplicativo](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\)).

A análise de desktops recomenda o aplicativo para teste piloto para descobrir qualquer regressão.


## <a name="driver-risk-assessment"></a>Avaliação de risco do driver

A análise de desktop também lista e grupos por disponibilidade todos os drivers que não migrarão para a versão do sistema operacional.

Você pode encontrar a avaliação no driver no desktop Analytics. Na lista de ativos de driver em um plano de implantação, selecione um driver individual para abrir seu painel submenu de propriedades. Você verá um nível geral de recomendação e avaliação. A seção **fatores de risco de compatibilidade** mostra os detalhes dessas avaliações.

| Disponibilidade do driver | Ação necessária? | O que significa | Diretrizes |
|---------------------|------------------|---------------|----------|
| Disponível na caixa | Não, somente para conscientização | A versão atualmente instalada de um aplicativo ou driver não migrará para a nova versão do sistema operacional. Uma versão compatível é instalada com a nova versão do sistema operacional. | Nenhuma ação é necessária para que a atualização continue. |
| Importar do Windows Update | Sim | A versão atualmente instalada de um driver não migrará para a nova versão do sistema operacional. Uma versão compatível está disponível em Windows Update. | Se o computador receber atualizações automaticamente do Windows Update, nenhuma ação será necessária. Caso contrário, importe um novo driver de Windows Update depois de atualizar o Windows. |
| Disponível na caixa e do Windows Update | Sim | A versão atualmente instalada de um driver não migrará para a nova versão do sistema operacional. Embora um novo driver seja instalado durante a atualização, uma versão mais recente está disponível em Windows Update. | Se o computador receber atualizações automaticamente do Windows Update, nenhuma ação será necessária. Caso contrário, importe um novo driver de Windows Update depois de atualizar o Windows. |
| Verificar com o fornecedor | Sim | O driver não migrará para a nova versão do so e a análise da área de trabalho não poderá localizar uma versão compatível. | Para uma solução, verifique com o fornecedor de hardware independente (IHV) que fabrica o driver ou o OEM (fabricante original do equipamento) que forneceu o dispositivo. |


## <a name="see-also"></a>Consulte também

O benefício do FastTrack Center para Windows 10 fornece acesso ao **aplicativo de área de trabalho garantir**. Esse benefício é um novo serviço projetado para resolver problemas com a compatibilidade de aplicativos com o Windows 10 e o Office 365 ProPlus. Para obter mais informações, consulte [Desktop App assure](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
