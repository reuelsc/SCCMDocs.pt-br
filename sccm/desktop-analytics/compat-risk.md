---
title: Risco de compatibilidade para aplicativos do Windows
titleSuffix: Configuration Manager
description: Saiba mais sobre os riscos de compatibilidade para aplicativos do Windows na área de trabalho de análise.
ms.date: 04/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: da0bde04e019fdf0fbb0a997be652860824270b1
ms.sourcegitcommit: 5ee9487c891c37916294bd34a10d04e398f111f7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59069391"
---
# <a name="compatibility-risk-for-windows-apps-in-desktop-analytics"></a>Risco de compatibilidade de aplicativos do Windows na área de trabalho de análise

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

As avaliações de atualização na análise do Windows foram genéricas, por exemplo: Necessária atenção ou correção disponível. Ele não fornece qualquer indicador visual sobre como priorizar aplicativos com problemas ou atualizar informações. Análise da área de trabalho substitui esse recurso com **riscos de compatibilidade**. Análise da área de trabalho mostra a avaliação de risco do aplicativo para aplicativos apenas na exibição de implantação para um cenário de pré-atualização. Ele categoriza os aplicativos com base em insights que Microsoft obtém das máquinas que está incluídas em um plano de implantação atual.

Análise da área de trabalho usa as seguintes categorias de risco de compatibilidade:

- **Baixa**: O serviço encontrado nenhum sinais para colocar em risco a esse aplicativo para um Windows atualizar. É provável que funcionam em SO de destino como-está.  

- **Médio**: Análise indica que o aplicativo pode portadores de deficiência funcionalidade, embora a correção é provavelmente possível.  

- **Alta**: O aplicativo é quase certo falhar durante ou após a atualização. Talvez seja necessário uma correção.  

- **Desconhecido**: O aplicativo não foi avaliado pelo analisador de integridade do aplicativo. Não há nenhuma outra informação, como *problemas conhecidos do MS* ou *pronto para o Windows*.  



## <a name="risk-assessment-engine"></a>Mecanismo de avaliação de risco

Há várias fontes que o analisador de integridade do aplicativo usa para gerar a classificação de risco.

![Diagrama de áreas de mecanismo de avaliação de risco de analisador de integridade do aplicativo](media/aha-risk-assessment-engine.png)


### <a name="ms-known-issues"></a>Problemas conhecidos do MS

O analisador de integridade do aplicativo examina o banco de dados de compatibilidade do Microsoft app para todos os problemas conhecidos. Ele usa esse banco de dados para determinar todos os blocos existentes compatibilidade de aplicativos publicamente disponíveis da Microsoft ou outros editores. Essa verificação só se aplica ao SO de destino para o plano de implantação selecionado.


### <a name="ready-for-windows"></a>Pronto para Windows

O repositório de dados pronto para o Windows verifica blocos de compatibilidade em um dispositivo. Ele correlaciona dados de outros clientes reporting aplicativos semelhantes. A Microsoft usa dados de outros dispositivos semelhantes em que esse aplicativo não relatado nenhum problema.


### <a name="app-health-analyzer-signals-for-compatibility-assessment"></a>Analisador de integridade do aplicativo sinaliza para avaliação de compatibilidade

Use o Kit de ferramentas do analisador de integridade do aplicativo para coletar sinais adicionais para compatibilidade de aplicativos. Para obter mais informações, consulte [analisador de integridade do aplicativo](/sccm/desktop-analytics/app-health-analyzer).

Os sinais a seguir estão disponíveis atualmente:

#### <a name="adopted-version-available"></a>Versão adotado disponível

Não há outra versão desse aplicativo que é altamente adotados por outros clientes. Esse sinal usa dados de pronto para Windows. Se houver qualquer bloqueadores de atualização com sua versão atual, considere implantar a versão alternativa em vez disso.

#### <a name="16-bit"></a>16-bit

Remova todos os componentes de 16 bits de aplicativos e substituir por equivalentes de 32 bits ou 64 bits. Para obter mais informações, consulte [a Vista do Windows e a história do desenvolvedor do Windows Server 2008: Manual de compatibilidade de aplicativos](https://msdn.microsoft.com/library/aa480152.aspx).

A outra opção é habilitar o NT NTVDM máquina DOS Virtual () para obter suporte no Windows 10.

#### <a name="requires-admin-privileges"></a>Exige privilégios de administrador

O aplicativo requer que o usuário tenha acesso administrativo ao dispositivo. Use um manifesto do aplicativo para esses aplicativos que exigem permissões de administrador. Para obter mais informações, consulte [criar e inserir um manifesto de aplicativo](https://msdn.microsoft.com/library/bb756929.aspx).
<!--Is this a better, more current link? https://docs.microsoft.com/windows/desktop/sbscs/application-manifests-->

Análise da área de trabalho recomenda o aplicativo para teste do piloto. Ele deve funcionar bem para piloto, mas você encontrará quaisquer regressões.

#### <a name="java-dependency"></a>Dependência de Java

Muitos aplicativos Java se baseiam em um instalado separadamente Java Runtime Environment (JRE). Enquanto as versões mais antigas do JRE podem continuar a trabalhar no Windows 10, o Oracle suporta apenas as versões mais recentes do JRE. Usar um JRE de sem suporte mais antigo pode ter vulnerabilidades de segurança. Verifique se seu aplicativo é executado em versões mais recentes do JRE.

#### <a name="not-dpi-aware"></a>Reconhecimento de DPI não

O aplicativo pode ter problemas de exibição com resoluções de tela avançada no Windows 10. Use um manifesto do aplicativo para evitar quaisquer problemas com altas resoluções DPI. Para obter mais informações, consulte [manifestos de aplicativo](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests).

Análise da área de trabalho recomenda o aplicativo para teste do piloto. Ele deve funcionar bem para piloto, mas você encontrará quaisquer regressões.

#### <a name="visual-basic-version-6-vb6"></a>Visual Basic versão 6 (VB6).

Análise da área de trabalho recomenda o aplicativo para teste do piloto. Aplicativos VB6 geralmente são compatíveis. Se o aplicativo regresses durante o piloto por causa de quaisquer dependências adicionais ou widgets, em seguida, você deve atualizar o aplicativo para o Visual Basic .NET

#### <a name="os-version-dependency"></a>Dependência de versão do sistema operacional

Considere redeveloping o aplicativo para usar a API de auxiliares de versão ou o aplicativo para Windows 10 de destino do manifesto.

Análise da área de trabalho recomenda o aplicativo para teste do piloto. Ele deve funcionar bem para piloto, mas você encontrará quaisquer regressões.

#### <a name="silverlight-framework"></a>Framework do Silverlight

A Microsoft recomenda que aplicativos não baseados em navegador não usam o Silverlight. A data de término do suporte para o Silverlight 5 é de 2021 de outubro.

Os navegadores da web mais atuais não suportam o Silverlight.

| Navegador | Suporte |
|---------|---------|
| Google Chrome  | Fim do suporte: Setembro de 2015 |
| Firefox | Fim do suporte: Março de 2017 |
| Microsoft Edge | Nenhum plug-in disponível |

Análise da área de trabalho recomenda o aplicativo para teste do piloto. Ele deve funcionar bem para piloto, mas você encontrará quaisquer regressões.

#### <a name="net-framework-1011"></a>.NET framework 1.0/1.1

O .NET framework versão 1.0 não tem suporte no Windows 10. Versão 1.1 não é compatível no Windows 10. Se o aplicativo for de um fornecedor de terceiros, contate o fornecedor para solicitar uma versão que está em conformidade com o Windows 10. Caso contrário, redevelop o aplicativo para usar uma versão compatível do .NET.

#### <a name="net-framework-2030"></a>.NET framework 2.0/3.0

.NET 2.0 e 3.5 estruturas têm suporte no Windows 10. Você talvez precise habilitar o recurso do Windows. Para obter mais informações, consulte [instalar o .NET Framework 3.5 no Windows 10](https://docs.microsoft.com/dotnet/framework/install/dotnet-35-windows-10).

#### <a name="ui-access"></a>Acesso de interface do usuário

Aplicativos com acesso de interface do usuário podem ignorar os níveis de controle de interface do usuário para conduzir a entrada para alto privilégio windows na área de trabalho. Use essa configuração somente para aplicativos de tecnologia assistencial de interface do usuário.

Se você não estiver usando recursos de acessibilidade em seu aplicativo, defina o sinalizador de acesso de interface do usuário no manifesto do aplicativo como false. Para obter mais informações, consulte [criar e inserir um manifesto de aplicativo](https://msdn.microsoft.com/library/bb756929.aspx).

#### <a name="driver-dependency"></a>Dependência de driver

O aplicativo depende de um driver. Análise da área de trabalho recomenda o aplicativo para teste do piloto. Ele deve funcionar bem para piloto, mas você encontrará quaisquer regressões. Se você tiver problemas, entre em contato com o publicador para solicitar uma versão que está em conformidade com o Windows 10.



## <a name="app-confidence-simulation-for-a-sample-population"></a>Simulação de confiança do aplicativo para uma população de exemplo

Os gráficos a seguir são de um estudo de caso do exemplo. Esses dados destaca o uso do analisador de integridade do aplicativo com análises de área de trabalho para adotar uma abordagem controlada por dados de validação do aplicativo. Essa abordagem pode ajudar a reduzir o tempo e esforço em testar seus aplicativos durante a atualização do Windows 10.

Esses dados mostram as métricas de confiança para 60 dispositivos com 899 aplicativos, incluindo aplicativos de linha de negócios.

![Antes e depois gráficos mostrando a confiança do aplicativo](media/aha-app-confidence-simulation.png)


## <a name="see-also"></a>Consulte também

O benefício de centro FastTrack para Windows 10 fornece acesso aos **aplicativo de área de trabalho garantir**. Esse benefício é um novo serviço projetado para resolver problemas com a compatibilidade de aplicativo do Office 365 ProPlus e Windows 10. Para obter mais informações, consulte [aplicativo de área de trabalho garantir](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
