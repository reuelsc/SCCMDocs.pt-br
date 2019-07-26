---
title: Monitorar a integridade da conexão
titleSuffix: Configuration Manager
description: Detalhes sobre como monitorar a integridade da conexão e os Estados do dispositivo para análise de desktop no Configuration Manager.
ms.date: 06/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1f4e26f7-42f2-40c8-80cf-efd405349c6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3406c0fff57a1ecef24a045e3061417fc5fac46c
ms.sourcegitcommit: e0438c191df945305625ae91596c9417d16e8510
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68491649"
---
# <a name="monitor-connection-health"></a>Monitorar a integridade da conexão

Use o painel de **integridade da conexão** no Configuration Manager para analisar categorias por integridade do dispositivo. No console do Configuration Manager, vá para o espaço de trabalho **biblioteca de software** , expanda o nó **manutenção do desktop Analytics** e selecione o painel de **integridade da conexão** .  

![Captura de tela do painel de integridade da conexão Configuration Manager](media/connection-health-dashboard.png)

Quando você configura pela primeira vez a análise de desktops, esses gráficos podem não mostrar dados completos. Pode levar 2-3 dias para que os dispositivos ativos enviem dados de diagnóstico para o serviço de análise de desktop, o serviço para processar os dados e, em seguida, sincronizar com seu site do Configuration Manager.<!-- 4098037 -->


## <a name="connection-details"></a>Detalhes da conexão

Esse bloco exibe as seguintes informações básicas sobre a conexão de Configuration Manager para o desktop Analytics:

- **Nome do locatário**: O nome da conexão do desktop Analytics no nó de **Serviços do Azure**

- **Coleção de destino**: A mesma *coleção de destino* que você especificou ao conectar Configuration Manager ao desktop Analytics. Essa coleção inclui todos os dispositivos que Configuration Manager configurados com a ID comercial e as configurações de dados de diagnóstico. É o conjunto completo de dispositivos que Configuration Manager se conecta ao serviço de análise de desktop.

- **Dispositivos direcionados**: Todos os dispositivos na coleção de destino, menos os seguintes tipos de dispositivos:

    - Encerrado
    - Substituí
    - Inativo
    - Não gerenciados
    - Dispositivos executando versões LTSC (canal de manutenção em longo prazo) do Windows 10
    - Dispositivos que executam o Windows Server

    Para obter mais informações sobre esses Estados de dispositivo, consulte [sobre o status do cliente](/sccm/core/clients/manage/monitor-clients#bkmk_about).

    > [!Note]  
    > Configuration Manager carrega no desktop Analytics todos os dispositivos na coleção de destino menos clientes descomissionados e obsoletos.

- **Dispositivos qualificados para o da**: O número de dispositivos direcionados a menos dispositivos que não são elegíveis para análise de desktop. Por exemplo, os dispositivos na coleção de destino que executam o Windows Server ou o LTSC (canal de manutenção de longo prazo) do Windows 10.


## <a name="last-sync-details"></a>Detalhes da última sincronização

Esse bloco mostra quando Configuration Manager sincroniza com o serviço de nuvem do desktop Analytics e quantos dispositivos ele sincroniza.

- **Dispositivos sincronizados**: O número de dispositivos exclusivos que Configuration Manager enviados para a análise de desktops. O serviço inclui esses dispositivos no instantâneo visível no momento.

- **Última sincronização de serviço**: O mesmo que a hora da **última atualização** no portal do desktop Analytics.

- **Próxima sincronização de serviço**: Quando você pode esperar o próximo instantâneo diário no desktop Analytics.

> [!Note]  
> Nenhum desses valores é atualizado automaticamente quando você solicita um instantâneo sob demanda. Para obter mais informações, consulte [latência de dados](/sccm/desktop-analytics/troubleshooting#data-latency).

Se você considerar que alguns dispositivos não estão sendo mostrados na análise de desktops, verifique se os dispositivos têm suporte da análise de desktop. Para obter mais informações, veja [Pré-requisitos](/sccm/desktop-analytics/overview#prerequisites).


## <a name="connection-health"></a>Integridade da conexão

O gráfico de **integridade da conexão** exibe o número de dispositivos nos seguintes Estados de integridade:  

- [Registrado corretamente](#properly-enrolled): O dispositivo aparece no desktop Analytics com um inventário completo
- [Não é possível registrar](#unable-to-enroll): Há um problema de bloqueio que impede o registro do dispositivo
- [Alerta de configuração](#configuration-alert): O dispositivo não aparece na análise de desktops ou aparece com um inventário incompleto. Configuration Manager também identificou um problema com o registro do dispositivo.
- [Aguardando registro](#awaiting-enrollment): Configuration Manager configurou o dispositivo, mas ele ainda não aparece no desktop Analytics
- [Status pendente](#status-pending): Configuration Manager ainda está configurando este dispositivo ou não tem dados suficientes do dispositivo para determinar seu estado
- [Dados ausentes](#missing-data): Configuration Manager configurou o dispositivo, mas a análise de desktops tem apenas dados parciais

<!-- 
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
 -->

O número total de dispositivos neste gráfico deve ser o mesmo que o valor dos **dispositivos qualificados para** o no bloco detalhes da conexão.

Selecione a fatia no gráfico para fazer uma busca detalhada de uma lista de dispositivos com esse estado. Para obter mais informações, consulte [lista de dispositivos](#device-list).

Selecione o nome da categoria na legenda para removê-lo ou adicioná-lo do gráfico. Essa ação ajuda a aplicar zoom no gráfico para que você possa ver os tamanhos relativos de segmentos menores.

### <a name="properly-enrolled"></a>Registrado corretamente

O dispositivo tem os seguintes atributos:

- Um cliente Configuration Manager versão 1902 ou posterior  
- Não há erros de configuração  
- A análise de desktop recebeu dados de diagnóstico completos deste dispositivo nos últimos 28 dias  
- A análise de desktops tem um inventário completo da configuração do dispositivo e dos aplicativos instalados  

### <a name="unable-to-enroll"></a>Não é possível registrar

Configuration Manager detecta um ou mais problemas de bloqueio que impedem o registro do dispositivo. Para obter mais informações, consulte a lista de [Propriedades de dispositivo do desktop Analytics em Configuration Manager](#bkmk_config-issues).  

Por exemplo, o cliente Configuration Manager não tem pelo menos a versão 1902 (5.0.8790). Atualize o cliente para a versão mais recente. Considere habilitar a atualização automática do cliente para o site Configuration Manager. Para obter mais informações, consulte [Atualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  

### <a name="configuration-alert"></a>Alerta de configuração

O dispositivo não aparece na análise de desktops ou aparece com um inventário incompleto. Configuration Manager também identificou um problema com o registro do dispositivo. Para obter mais informações, consulte a lista de [Propriedades de dispositivo do desktop Analytics em Configuration Manager](#bkmk_config-issues).

Por exemplo, o dispositivo não tem conectividade com o serviço. Para obter mais informações, consulte [conectividade de ponto de extremidade de diagnóstico do Windows](#windows-diagnostic-endpoint-connectivity).

### <a name="awaiting-enrollment"></a>Aguardando registro

A análise de desktops não tem dados de diagnóstico para este dispositivo. Esse problema pode ser porque você adicionou recentemente o dispositivo à coleção de destino e ainda não enviou dados. Isso também pode significar que o dispositivo não está se comunicando corretamente com o serviço, e os dados de diagnóstico mais recentes têm mais de 28 dias.

Verifique se o dispositivo pode se comunicar com o serviço. Para obter mais informações, consulte [pontos de extremidade](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

### <a name="status-pending"></a>Status pendente

Configuration Manager ainda está configurando este dispositivo ou não tem dados suficientes do dispositivo para determinar seu estado.

### <a name="missing-data"></a>Dados ausentes

Configuration Manager configurou com êxito o dispositivo, mas o desktop Analytics não pode criar uma avaliação de compatibilidade. Ele não tem um conjunto de dados completo para a configuração do dispositivo (censo) ou aplicativos instalados (inventário).

Esse problema geralmente é corrigido automaticamente quando o dispositivo é repetido. Se ele persistir, verifique se o dispositivo pode se comunicar com o serviço. Para obter mais informações, consulte [pontos de extremidade](/sccm/desktop-analytics/enable-data-sharing#endpoints).  


## <a name="device-list"></a>Lista de dispositivos

Para ver uma lista específica de dispositivos por status, comece com o painel de **integridade da conexão** . Selecione um dos segmentos do bloco **integridade da conexão** e faça uma busca detalhada em uma lista de dispositivos nesse estado. Esta exibição de dispositivo Personalizada exibe as seguintes colunas do desktop Analytics por padrão:

- Configuração de ID comercial
- Atualização mínima de compatibilidade
- Aceitação de dados de diagnóstico do Windows
- Aceitação de dados comerciais do Windows
- Conectividade de ponto de extremidade de diagnóstico do Windows

> [!Note]  
> Ignore a coluna para **conectividade de ponto de extremidade de diagnóstico do Office**. Ele é reservado para funcionalidade futura.

Essas colunas correspondem aos [pré-requisitos](/sccm/desktop-analytics/overview#prerequisites) de chave para que os dispositivos se comuniquem com a análise de desktop.

![Captura de tela da lista de dispositivos registrados corretamente](media/sccm-device-list-properly-enrolled.png)

Selecione um dispositivo para ver a lista completa de propriedades disponíveis no painel de detalhes. Você também pode adicionar qualquer uma dessas propriedades como colunas à lista de dispositivos.


## <a name="bkmk_config-issues"></a>Propriedades do dispositivo

As seguintes propriedades de dispositivo de análise de desktop estão disponíveis como colunas na lista de dispositivos Configuration Manager:

- [Configuração do avaliador](#appraiser-configuration)  
- [Atualização mínima de compatibilidade](#minimum-compatibility-update)  
- [Versão do avaliador](#appraiser-version)  
- [Última execução completa bem-sucedida do avaliador](#last-successful-full-run-of-appraiser)  
- [Coleta de dados do avaliador](#appraiser-data-collection)  
- [Última execução completa bem-sucedida de censo](#last-successful-full-run-of-census)  
- [Coleta de dados censo](#census-data-collection)  
- [Conectividade de ponto de extremidade de diagnóstico do Windows](#windows-diagnostic-endpoint-connectivity)  
- [Verificar dados de diagnóstico do usuário final](#check-end-user-diagnostic-data)  
- [Verificar proxy do usuário](#check-user-proxy)  
- [Configuração de ID comercial](#commercial-id-configuration)  
- [Aceitação de dados comerciais do Windows](#windows-commercial-data-opt-in)  
- [Verificar o nome do dispositivo nos dados de diagnóstico](#check-device-name-in-diagnostic-data)  
- [Configuração do serviço DiagTrack](#diagtrack-service-configuration)  
- [Versão do DiagTrack](#diagtrack-version)  
- [Recuperação de ID de SQM](#sqm-id-retrieval)  
- [Recuperação de identificador de dispositivo exclusivo](#unique-device-identifier-retrieval)  
- [Aceitação de dados de diagnóstico do Windows](#windows-diagnostic-data-opt-in)  

> [!Note]  
> Ignore as propriedades de **conectividade de ponto de extremidade de diagnóstico do Office** e aceitação de dados de **diagnóstico do Office**. Eles estão reservados para funcionalidade futura.

O bloco de bloqueios de **registro e alertas de configuração mais frequentes** do painel de integridade da conexão exibe as propriedades que os dispositivos geralmente relatam como um problema.

### <a name="appraiser-configuration"></a>Configuração do avaliador

<!--20,21-->
Avaliador é o componente do Windows que corresponde às [atualizações de compatibilidade](/sccm/desktop-analytics/enroll-devices#update-devices). Ele avalia os aplicativos e drivers no dispositivo para compatibilidade com a versão mais recente do Windows. 

Se essa verificação for bem-sucedida, o componente avaliador será configurado corretamente no dispositivo.

Caso contrário, ele poderá exibir um dos seguintes erros:

- Não é possível configurar a coleta de dados de compatibilidade de aplicativos do dispositivo (SetRequestAllAppraiserVersions). Verifique os logs para obter os detalhes da exceção  

- Não é possível configurar a coleta de dados de compatibilidade de aplicativos do dispositivo (SetRequestAllAppraiserVersions). Verifique os logs para obter os detalhes da exceção  

- Não é possível gravar o RequestAllAppraiserVersions na `HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser`chave do registro. Verificar permissões  

Verifique as permissões nessa chave do registro. Verifique se a conta do sistema local pode acessar essa chave para que o Configuration Manager cliente seja definido.  

Para obter mais informações, examine M365AHandler. log no cliente.  

### <a name="minimum-compatibility-update"></a>Atualização mínima de compatibilidade

<!--18,19,32-->
A atualização de compatibilidade (avaliador. dll) não está instalada ou desatualizada no dispositivo. É mais antigo do que o requisito mínimo para a análise de desktops, 10.0.17763.

Instale a atualização de compatibilidade mais recente. Para obter mais informações, consulte [Compatibility updates](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser).

### <a name="appraiser-version"></a>Versão do avaliador

Essa propriedade exibe a versão atual do componente avaliador no dispositivo. Ele mostra a versão do arquivo `%windir%\System32\appraiser.dll`em, sem os pontos decimais. Por exemplo, File Version 10.0.17763 é exibido como 10017763.

### <a name="last-successful-full-run-of-appraiser"></a>Última execução completa bem-sucedida do avaliador

Essa propriedade exibe a data e a hora em que o dispositivo foi executado pela última vez com êxito.

### <a name="appraiser-data-collection"></a>Coleta de dados do avaliador

<!--Appraiser run status-->
<!--22,33-->
Essa propriedade mostra o resultado mais recente do Windows que está executando o componente avaliador.

Se não for bem-sucedido, ele poderá mostrar um dos seguintes erros:

- Não é possível coletar dados de compatibilidade de aplicativo (RunAppraiser). Verifique os logs para obter detalhes  

- A coleta de dados de compatibilidade do aplicativo (CompatTelRunner. exe) terminou com um código de erro  

Para obter mais informações, examine M365AHandler. log no cliente.

Verifique o seguinte arquivo: `%windir%\System32\CompatTelRunner.exe`. Se ele não existir, reinstale as [atualizações de compatibilidade](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser)necessárias. Verifique se nenhum outro componente do sistema está removendo esse arquivo, como a política de grupo ou um serviço antimalware.

Se o arquivo M365AHandler. log no cliente incluir um dos seguintes erros:
```
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005
```

Para ajudar a corrigir esses erros, execute os seguintes comandos em um console do Windows PowerShell com privilégios elevados no cliente afetado:

```PowerShell
# stop associated services
Stop-Service -Name diagtrack #Connected User Experiences and Telemetry
Stop-Service -Name pcasvc #Program Compatibility Assistant Service
Stop-Service -Name dps #Diagnostic Policy Service

# regenerate diagnostic data cache
Remove-Item -Path $Env:WinDir\appcompat\programs\amcache.hve
Remove-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name AmiHivePermissionsCorrect -Force

# set ASL logging level to output log files in %windir%\temp
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name LogFlags -Value 4 -PropertyType DWord -Force

# restart services
Start-Service -Name diagtrack
Start-Service -Name pcasvc
Start-Service -Name dps
```

### <a name="last-successful-full-run-of-census"></a>Última execução completa bem-sucedida de censo

Essa propriedade exibe a data e a hora em que o dispositivo foi executado pela última vez com êxito censo.

### <a name="census-data-collection"></a>Coleta de dados censo

<!-- Census run status -->
<!--51,52-->
Censo é o componente do Windows que inventaria o dispositivo. Esses dados de inventário são usados para entender o dispositivo e sua configuração.

Essa propriedade mostra o resultado mais recente do Windows que executa o componente censo.

Se não for bem-sucedido, ele poderá mostrar um dos seguintes erros:

- Não é possível coletar dados sobre o dispositivo e sua configuração (RunCensus). Verifique os logs para obter os detalhes da exceção  

- A ferramenta de coleta de dados de configuração e dispositivo (devicecensus. exe) não foi encontrada  

Para obter mais informações, examine M365AHandler. log no cliente.

Verifique o seguinte arquivo: `%windir%\System32\DeviceCensus.exe`. Se ele não existir, reinstale as [atualizações de compatibilidade](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser)necessárias. Verifique se nenhum outro componente do sistema está removendo esse arquivo, como a política de grupo ou um serviço antimalware.

### <a name="windows-diagnostic-endpoint-connectivity"></a>Conectividade de ponto de extremidade de diagnóstico do Windows

<!--12,15-->
Se essa verificação for bem-sucedida, o dispositivo poderá se conectar à experiência do usuário conectada e ao ponto de extremidade de telemetria (Vortex).

Caso contrário, ele pode mostrar um dos seguintes erros:  

- Não é possível se conectar à experiência do usuário conectada e ao ponto de extremidade de telemetria (Vortex). Verifique suas configurações de rede/proxy  

- Não é possível verificar a conectividade com a experiência do usuário conectado e o ponto de extremidade de telemetria (CheckVortexConnectivity). Verifique os logs para obter os detalhes da exceção  

Os dispositivos verificam a conectividade com uma solicitação GET para o seguinte ponto de extremidade com base na versão do sistema operacional:

| Versão do SO | Extremidade |
|------------|----------|
| Windows 10, versão 1803 ou posterior com a atualização cumulativa mais recente | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Windows 10, versão 1803 ou posterior sem a atualização cumulativa 2018-09 ou posterior | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10, versão 1709 ou anterior | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 ou Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

Verifique se o dispositivo pode se comunicar com o serviço. Essa verificação valida alguns, mas não todos os pontos de extremidade necessários. Para obter mais informações, consulte [pontos de extremidade](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

Para obter mais informações, examine M365AHandler. log no cliente.  

### <a name="check-end-user-diagnostic-data"></a>Verificar dados de diagnóstico do usuário final

<!--1004-->
Se essa verificação não for bem-sucedida, um usuário selecionou mais dados de diagnóstico do Windows no dispositivo. Ele também pode ser causado por um objeto de política de grupo conflitante. Para obter mais informações, consulte [configurações do Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).

Dependendo dos requisitos de negócios, você pode desabilitar a opção de usuário por meio da política de grupo. Use a configuração para **Configurar a interface de usuário de configuração de aceitação**de telemetria. Para saber mais, veja [Configurar dados de diagnóstico do Windows em sua organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).

### <a name="check-user-proxy"></a>Verificar proxy do usuário

<!--30,35-->
A configuração DisableEnterpriseAuthProxy é habilitada por padrão para o Windows 7. Para computadores Windows 8.1, Configuration Manager define a configuração DisableEnterpriseAuthProxy como 0 (não desabilitada).

Essa propriedade pode exibir os seguintes erros:

- O proxy de autenticação está habilitado. Definir DisableEnterpriseAuthProxy como 0 em`HKLM\Software\Policies\Microsoft\Windows\DataCollection`

- Não é possível verificar o status do proxy de autenticação. Verifique os logs para obter os detalhes da exceção

Para obter mais informações, examine M365AHandler. log no cliente.  

Verifique as permissões nessa chave do registro. Verifique se a conta do sistema local pode acessar essa chave para que o Configuration Manager cliente seja definido. Ele também pode ser causado por um objeto de política de grupo conflitante. Para obter mais informações, consulte [configurações do Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

### <a name="commercial-id-configuration"></a>Configuração de ID comercial

<!--9, 11, 53-->
A Microsoft usa uma ID comercial exclusiva para mapear informações de dispositivos para seu espaço de trabalho do desktop Analytics. Quando você integra Configuration Manager com o desktop Analytics, ele consulta automaticamente o serviço para essa ID. Configuration Manager deve aplicar automaticamente essa ID aos clientes para os quais você visa as configurações de análise da área de trabalho.

Se essa verificação for bem-sucedida, o dispositivo será configurado corretamente com uma ID comercial.

Caso contrário, ele pode mostrar um dos seguintes erros:

- Não é possível gravar o Comercialid na `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`chave do registro. Verificar permissões  

- Não é possível atualizar o Comercialid na `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`chave do registro. Verifique os logs para obter os detalhes da exceção  

- Forneça o valor comercial correto em`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`  

Para obter mais informações, examine M365AHandler. log no cliente.  

Verifique as permissões nessa chave do registro. Verifique se a conta do sistema local pode acessar essa chave para que o Configuration Manager cliente seja definido. Ele também pode ser causado por um objeto de política de grupo conflitante. Para obter mais informações, consulte [configurações do Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Há uma ID diferente para o dispositivo. Essa chave do registro é usada pela política de grupo. Ela tem precedência sobre a ID fornecida pelo Configuration Manager.  

<a name="bkmk_ViewCommercialID"></a>Para exibir a ID comercial no portal do desktop Analytics, use o seguinte procedimento:

1. Vá para o portal do desktop Analytics e selecione **Serviços conectados** no grupo configurações globais.  

2. No painel **Serviços conectados** , o painel **registrar dispositivos** é selecionado por padrão. No painel registrar dispositivos, a seção informações exibe sua chave de ID comercial.  

![Captura de tela da ID comercial no portal do desktop Analytics](media/commercial-id.png)

> [!Important]  
> Obtenha somente a **nova chave de ID** quando não puder usar a atual. Se você regenerar a ID comercial, [Registre novamente os dispositivos com a nova ID](/sccm/desktop-analytics/enroll-devices#device-enrollment). Esse processo pode resultar em perda de dados de diagnóstico durante a transição.  

### <a name="windows-commercial-data-opt-in"></a>Aceitação de dados comerciais do Windows

<!--64-->
Essa propriedade é específica para dispositivos que executam o Windows 7 ou Windows 8.1. Ele executa testes semelhantes como o [consentimento de dados de diagnóstico do Windows](#windows-diagnostic-data-opt-in), exceto para o valor CommercialDataOptIn.

### <a name="check-device-name-in-diagnostic-data"></a>Verificar o nome do dispositivo nos dados de diagnóstico

<!--56,58-->
Se essa verificação for bem-sucedida, o dispositivo será configurado corretamente para compartilhar o nome do dispositivo.

Caso contrário, ele pode mostrar um dos seguintes erros:

- Não é possível verificar o nome do dispositivo a ser enviado à Microsoft como parte dos dados de diagnóstico do Windows. Verifique os logs para obter os detalhes da exceção  

- Não é possível gravar AllowDeviceNameInTelemetry na `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`chave do registro. Verificar permissões  

Para obter mais informações, examine M365AHandler. log no cliente.  

Verifique as permissões nessa chave do registro. Verifique se a conta do sistema local pode acessar essa chave para que o Configuration Manager cliente seja definido. Ele também pode ser causado por um objeto de política de grupo conflitante. Para obter mais informações, consulte [configurações do Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Verifique se outro mecanismo de política, como a política de grupo, não está desabilitando essa configuração.

### <a name="diagtrack-service-configuration"></a>Configuração do serviço DiagTrack

<!--44,45,50-->
Se essa verificação for bem-sucedida, o componente DiagTrack será configurado corretamente no dispositivo. A versão mínima exigida pela análise de desktops é 10010586 (10.0.10586).

Caso contrário, ele poderá exibir um dos seguintes erros:

- O componente de experiência do usuário conectado e telemetria (diagtrack. dll) está desatualizado. Verificar requisitos  

- Não é possível localizar o componente de experiência do usuário conectado e telemetria (diagtrack. dll). Verificar requisitos  

- Habilitar e iniciar o serviço de experiências e telemetria de usuário conectado para enviar dados para a Microsoft  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

Instale as atualizações mais recentes. Para obter mais informações, consulte [atualizações de dispositivo](/sccm/desktop-analytics/enroll-devices#update-devices).

Verifique se o serviço de **experiência de usuário conectado e** de telemetria no dispositivo está em execução.

### <a name="diagtrack-version"></a>Versão do DiagTrack

Essa propriedade exibe a versão atual do componente de experiência do usuário conectado e telemetria no dispositivo. Ele mostra a versão do arquivo `%windir%\System32\diagtrack.dll`em, sem os pontos decimais. Por exemplo, File Version 10.0.10586 é exibido como 10010586.

### <a name="sqm-id-retrieval"></a>Recuperação de ID de SQM

<!--38-->
Essa propriedade é usada principalmente para dispositivos Windows 7. Ele pode ser usado por versões posteriores do sistema operacional como um identificador de fallback para o dispositivo.

Se não for bem-sucedido, ele poderá exibir o seguinte erro:

- Não é possível recuperar o identificador de telemetria do dispositivo herdado (ID do SQM)

Para obter mais informações, examine M365AHandler. log no cliente.  

Verifique se você não tem IDs duplicadas em seu ambiente. Por exemplo, se os dispositivos foram implantados com uma imagem do sistema operacional que não foi generalizada.

### <a name="unique-device-identifier-retrieval"></a>Recuperação de identificador de dispositivo exclusivo

<!--54-->
A análise de desktops usa o serviço de conta da Microsoft para uma identidade de dispositivo mais confiável.

Verifique se o serviço **Assistente de conexão de conta da Microsoft** não está desabilitado. O tipo de inicialização deve ser **manual (início do gatilho)** .

Para desabilitar o acesso conta Microsoft do usuário final, use as configurações de política em vez de bloquear esse ponto de extremidade. Para obter mais informações, consulte [a conta Microsoft na empresa](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication).

### <a name="windows-diagnostic-data-opt-in"></a>Aceitação de dados de diagnóstico do Windows

<!--8,40,55,62-->
Essa propriedade verifica se o Windows está configurado corretamente para permitir dados de diagnóstico. Ele verifica o valor de AllowTelemetry nas seguintes chaves do registro:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Verifique as permissões nessas chaves do registro. Verifique se a conta do sistema local pode acessar essas chaves para que o Configuration Manager Client seja definido. Ele também pode ser causado por um objeto de política de grupo conflitante. Para obter mais informações, consulte [configurações do Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Para obter mais informações, examine M365AHandler. log no cliente.  



## <a name="see-also"></a>Consulte também

[Solucionar problemas do Desktop Analytics](/sccm/desktop-analytics/troubleshooting)
