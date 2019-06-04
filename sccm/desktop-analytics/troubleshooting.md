---
title: Solução de problemas de análise da área de trabalho
titleSuffix: Configuration Manager
description: Detalhes técnicos para ajudá-lo a solucionar problemas com a análise de área de trabalho.
ms.date: 05/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: edb871cf9a12862f19109fe885bfb3a0e626f445
ms.sourcegitcommit: 65753c51fbf596f233fc75a5462ea4a44005c70b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/03/2019
ms.locfileid: "66463069"
---
# <a name="troubleshooting-desktop-analytics"></a>Solução de problemas de análise da área de trabalho

Use os detalhes neste artigo para ajudá-lo a solucionar problemas com a análise de área de trabalho integrado ao Configuration Manager.



## <a name="confirm-prerequisites"></a>Confirmar pré-requisitos

Muitos problemas comuns são causados por pré-requisitos ausentes. Primeiro, confirme as configurações a seguir:

- [Pré-requisitos](/sccm/desktop-analytics/overview#prerequisites)  

- [Atualizações de componentes do Windows](/sccm/desktop-analytics/enroll-devices#update-devices)  

- [Como habilitar o compartilhamento de dados](/sccm/desktop-analytics/enable-data-sharing), que abrange os seguintes tópicos:  

    - Pontos de extremidade de Internet para o qual os clientes precisam para se conectar  

    - Autenticação do servidor proxy  

    - Níveis de dados de diagnóstico  



## <a name="monitor-connection-health"></a>Monitorar a integridade de conexão

Use o **integridade de Conexão** painel no Configuration Manager para fazer uma busca detalhada em categorias por integridade do dispositivo. No console do Configuration Manager, vá para o **biblioteca de Software** espaço de trabalho, expanda o **área de trabalho de análise de manutenção** nó e selecione o **integridade de Conexão** Painel de controle.  

![Captura de tela do painel de integridade de Conexão do Configuration Manager](media/connection-health-dashboard.png)

Ao configurar a análise de área de trabalho pela primeira vez, esses gráficos não podem mostrar dados completos. Pode levar 2 a 3 dias para dispositivos ativos enviar dados de diagnóstico para o serviço de análise de área de trabalho, o serviço para processar os dados e, em seguida, sincronizar com seu site do Configuration Manager.<!-- 4098037 -->


### <a name="connection-details"></a>Detalhes de Conexão

<!-- 4412133 -->

Esse bloco mostra informações básicas, como o locatário conectado, nome e tempos de atualizações do serviço. O **dispositivos direcionados** valor é que todos os dispositivos na coleção de destino, menos os seguintes tipos de dispositivos:

- Descomissionado
- Obsoleto
- inativo
- não gerenciado

Para obter mais informações sobre esses estados de dispositivo, consulte [sobre o status do cliente](/sccm/core/clients/manage/monitor-clients#bkmk_about).

> [!Note]  
> Configuration Manager carrega para análise de área de trabalho todos os dispositivos na coleção de destino menos clientes encerrados e obsoletos.

### <a name="connected-devices"></a>Dispositivos conectados

Se você achar que alguns dispositivos não estiverem aparecendo na área de trabalho de análise, verifique primeiro o percentual de **dispositivos conectados**. Este gráfico representa o percentual de dispositivos usando a seguinte fórmula:

- Numerador: O **dispositivos direcionados** o valor a [os detalhes de Conexão](#connection-details) lado a lado
- Denominador: Todos os dispositivos no Configuration Manager menos dispositivos inativos e não gerenciados

Se for inferior a 100%, verifique se que os dispositivos têm suporte pela análise de área de trabalho. Para obter mais informações, veja [Pré-requisitos](/sccm/desktop-analytics/overview#prerequisites).


### <a name="connection-health-states"></a>Estados de integridade de Conexão

Em seguida examine os **integridade de Conexão** gráfico. Ele exibe o número de dispositivos nas seguintes categorias de integridade:  

- [Corretamente registrados](#properly-enrolled)  
- [Problemas de configuração](#configuration-issues)  
- [Cliente não instalado](#client-not-installed)  
- [Aguardando o registro](#waiting-for-enrollment)  
- [Pré-requisitos ausentes](#missing-prerequisites)  
- [Dados ausentes](#missing-data)  

Selecione o nome da categoria para remover ou adicioná-lo do gráfico. Essa ação ajuda a ampliar o gráfico para que você possa ver os tamanhos relativos dos segmentos menores.

#### <a name="properly-enrolled"></a>Corretamente registrados

O dispositivo tem os seguintes atributos:

- Um cliente versão 1810 ou posterior do Configuration Manager  
- Não há nenhum erro de configuração  
- Análise da área de trabalho recebeu os dados de diagnóstico completos deste dispositivo nos últimos 28 dias  
- Análise da área de trabalho tem um inventário completo de configuração do dispositivo e aplicativos instalados  

#### <a name="configuration-issues"></a>Problemas de configuração

Configuration Manager detecta um ou mais problemas com a configuração necessária para a área de trabalho de análise. Para obter mais informações, consulte a lista de [propriedades do dispositivo de área de trabalho de análise no Configuration Manager](#bkmk_config-issues).  

#### <a name="client-not-installed"></a>Cliente não instalado

O dispositivo é direcionado para a área de trabalho de análise, mas não é um cliente do Configuration Manager.

O cliente do Configuration Manager é necessário para configurar e gerenciar o dispositivo para a área de trabalho de análise. Confira mais informações em [Métodos de instalação do cliente](/sccm/core/clients/deploy/plan/client-installation-methods).  

#### <a name="waiting-for-enrollment"></a>Aguardando o registro

Análise da área de trabalho não tem dados de diagnóstico para este dispositivo. Esse problema pode ser porque o dispositivo recentemente foi adicionado à coleção de destino e ainda não enviou dados. Ele também pode significar o dispositivo não está se comunicando corretamente com o serviço e os dados de diagnóstico mais recente são a mais de 28 dias.

Verifique se que o dispositivo é capaz de se comunicar com o serviço. Para obter mais informações, consulte [pontos de extremidade](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

#### <a name="missing-prerequisites"></a>Pré-requisitos ausentes

O cliente do Configuration Manager não é de pelo menos a versão 1810 (5.0.8740).

Atualize o cliente para a versão mais recente. Considere habilitar a atualização automática do cliente para o site do Configuration Manager. Para obter mais informações, consulte [Atualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  

#### <a name="missing-data"></a>Dados ausentes

Análise da área de trabalho não é possível criar uma avaliação de compatibilidade. Ele não tem um conjunto de dados completo para a configuração do dispositivo (censo) ou (inventário) de aplicativos instalados.

Geralmente, esse problema é corrigido automaticamente quando o dispositivo tenta novamente. Se ele persistir, verifique se que o dispositivo é capaz de se comunicar com o serviço. Para obter mais informações, consulte [pontos de extremidade](/sccm/desktop-analytics/enable-data-sharing#endpoints).  


### <a name="device-list"></a>Lista de dispositivos

Para ver uma lista específica de dispositivos por status, inicie com o **integridade de Conexão** painel. Selecione um dos segmentos do **integridade de Conexão** lado a lado e fazer drill down até uma lista de dispositivos nessa categoria. Este modo de exibição personalizadas do dispositivo exibe as seguintes colunas de análise de área de trabalho por padrão:

- Configuração de ID comercial
- Atualização de compatibilidade mínimo
- Windows dados de diagnóstico opt-in
- Windows dados comerciais opt-in
- Conectividade de ponto de extremidade de diagnóstico do Windows

> [!Note]  
> Ignorar a coluna para **conectividade de ponto de extremidade de diagnóstico do Office**. Ele está reservado para a funcionalidade futura.

Essas colunas correspondem à chave [pré-requisitos](/sccm/desktop-analytics/overview#prerequisites) para dispositivos se comuniquem com a análise de área de trabalho.

![Lista de dispositivos de captura de tela de corretamente registrados](media/sccm-device-list-properly-enrolled.png)

Selecione um dispositivo para ver a lista completa de propriedades disponíveis no painel de detalhes. Você também pode adicionar qualquer uma dessas propriedades como colunas à lista de dispositivos.


### <a name="bkmk_config-issues"></a> Propriedades da área de trabalho do dispositivo do Analytics no Configuration Manager

As colunas a seguir estão disponíveis na lista de dispositivos:

- [Configuração de avaliador](#appraiser-configuration)  
- [Atualização de compatibilidade mínimo](#minimum-compatibility-update)  
- [Versão de avaliação](#appraiser-version)  
- [Última execução bem-sucedida de total de avaliador](#last-successful-full-run-of-appraiser)  
- [Coleta de dados de avaliador](#appraiser-data-collection)  
- [Última execução bem-sucedida de total de censo](#last-successful-full-run-of-census)  
- [Coleta de dados de censo](#census-data-collection)  
- [Conectividade de ponto de extremidade de diagnóstico do Windows](#windows-diagnostic-endpoint-connectivity)  
- [Verificar os dados de diagnóstico do usuário final](#check-end-user-diagnostic-data)  
- [Verificar o proxy de usuário](#check-user-proxy)  
- [Configuração de ID comercial](#commercial-id-configuration)  
- [Windows dados comerciais opt-in](#windows-commercial-data-opt-in)  
- [Verifique o nome do dispositivo em dados de diagnóstico](#check-device-name-in-diagnostic-data)  
- [Configuração do serviço DiagTrack](#diagtrack-service-configuration)  
- [Versão DiagTrack](#diagtrack-version)  
- [Recuperação de ID de SQM](#sqm-id-retrieval)  
- [Recuperação de identificador exclusivo do dispositivo](#unique-device-identifier-retrieval)  
- [Windows dados de diagnóstico opt-in](#windows-diagnostic-data-opt-in)  

> [!Note]  
> Ignorar as propriedades para **conectividade de ponto de extremidade de diagnóstico do Office** e **Office dados de diagnóstico opt-in**. Elas são reservadas para a funcionalidade futura.

#### <a name="appraiser-configuration"></a>Configuração de avaliador

<!--20,21-->
A ferramenta de avaliação é o componente de Windows que corresponde do [atualizações de compatibilidade](/sccm/desktop-analytics/enroll-devices#update-devices). Ele avalia os aplicativos e drivers do dispositivo para compatibilidade com a versão mais recente do Windows. 

Se essa verificação for bem-sucedida, o componente de avaliador está configurado corretamente no dispositivo.

Caso contrário, ela pode exibir um dos seguintes erros:

- Não é possível configurar a coleta de dados de compatibilidade de aplicativo de dispositivo (SetRequestAllAppraiserVersions). Verifique os logs para os detalhes da exceção  

- Não é possível configurar a coleta de dados de compatibilidade de aplicativo de dispositivo (SetRequestAllAppraiserVersions). Verifique os logs para os detalhes da exceção  

- Não é possível gravar o RequestAllAppraiserVersions chave do registro `HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser`. Verificar permissões  

Verifique as permissões na chave do registro. Certifique-se de que a conta sistema local pode acessar essa chave para o cliente do Configuration Manager definir.  

Para obter mais informações, examine M365AHandler.log no cliente.  

#### <a name="minimum-compatibility-update"></a>Atualização de compatibilidade mínimo

<!--18,19,32-->
A atualização de compatibilidade (appraiser.dll) não está instalado ou atualizado no dispositivo. Ele é mais antigo que o requisito mínimo para a área de trabalho de análise, 10.0.17763.

Instale a atualização de compatibilidade mais recente. Para obter mais informações, consulte [atualizações de compatibilidade](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser).

#### <a name="appraiser-version"></a>Versão de avaliação

Essa propriedade exibirá a versão atual do componente avaliador no dispositivo. Ele mostra a versão do arquivo no `%windir%\System32\appraiser.dll`, sem pontos decimais. Por exemplo, a versão do arquivo 10.0.17763 exibe como 10017763.

#### <a name="last-successful-full-run-of-appraiser"></a>Última execução bem-sucedida de total de avaliador

Essa propriedade exibirá a data e hora em que o dispositivo pela última vez foi executada com êxito a ferramenta de avaliação.

#### <a name="appraiser-data-collection"></a>Coleta de dados de avaliador

<!--Appraiser run status-->
<!--22,33-->
Essa propriedade mostra o resultado mais recente do Windows executando o componente do avaliador.

Se não for bem-sucedida, ela pode mostrar um dos seguintes erros:

- Não é possível coletar dados de compatibilidade de aplicativo (RunAppraiser). Verifique os logs para obter detalhes  

- Coleta de dados de compatibilidade do aplicativo (CompatTelRunner.exe) foi encerrado com um código de erro  

Para obter mais informações, examine M365AHandler.log no cliente.

Verificar o seguinte arquivo: `%windir%\System32\CompatTelRunner.exe`. Se ele não existir, reinstale o necessária [atualizações de compatibilidade](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser). Verifique se que nenhum outro componente do sistema é remover esse arquivo, como a diretiva de grupo ou um serviço de antimalware.

Se o arquivo M365Handler.log no cliente inclui um dos seguintes erros: `RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1`
`RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005`
`RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005`  

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

#### <a name="last-successful-full-run-of-census"></a>Última execução bem-sucedida de total de censo

Essa propriedade exibirá a data e hora em que o dispositivo pela última vez foi executada com êxito censo.

#### <a name="census-data-collection"></a>Coleta de dados de censo

<!-- Census run status -->
<!--51,52-->
Census é o componente do Windows que faz o inventário de dispositivo. Esses dados de inventário são usados para entender o dispositivo e sua configuração.

Essa propriedade mostra o resultado mais recente do Windows executando o componente de censo.

Se não for bem-sucedida, ela pode mostrar um dos seguintes erros:

- Não é possível coletar dados sobre o dispositivo e sua configuração (RunCensus). Verifique os logs para os detalhes da exceção  

- Dispositivo e a configuração dados ferramenta de coleta (devicecensus.exe) não encontrada  

Para obter mais informações, examine M365AHandler.log no cliente.

Verificar o seguinte arquivo: `%windir%\System32\DeviceCensus.exe`. Se ele não existir, reinstale o necessária [atualizações de compatibilidade](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser). Verifique se que nenhum outro componente do sistema é remover esse arquivo, como a diretiva de grupo ou um serviço de antimalware.

#### <a name="windows-diagnostic-endpoint-connectivity"></a>Conectividade de ponto de extremidade de diagnóstico do Windows

<!--12,15-->
Se essa verificação for bem-sucedida, o dispositivo é capaz de se conectar ao usuário conectado telemetria e experiência de ponto de extremidade (Vortex).

Caso contrário, ele pode mostrar um dos seguintes erros:  

- Não é possível conectar-se para o usuário conectado telemetria e experiência de ponto de extremidade (Vortex). Verifique suas configurações de rede/proxy  

- Não é possível verificar a conectividade com o usuário conectado telemetria e experiência de ponto de extremidade (CheckVortexConnectivity). Verifique os logs para os detalhes da exceção  

Dispositivos verificam a conectividade com uma solicitação GET para o ponto de extremidade a seguir com base na versão de sistema operacional:

| Versão do SO | Ponto de extremidade |
|------------|----------|
| Windows 10, versão 1803 ou posterior com a atualização cumulativa mais recente | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Atualizar do Windows 10, versão 1803 ou posterior sem 2018-09 ou posterior cumulativa | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10, versão 1709 ou anterior | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 ou Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

Verifique se que o dispositivo é capaz de se comunicar com o serviço. Essa verificação valida algumas, mas não todos os pontos de extremidade necessários. Para obter mais informações, consulte [pontos de extremidade](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

Para obter mais informações, examine M365AHandler.log no cliente.  

#### <a name="check-end-user-diagnostic-data"></a>Verificar os dados de diagnóstico do usuário final

<!--1004-->
Se essa verificação não for bem-sucedida, o usuário selecionou um menor dados de diagnóstico do Windows no dispositivo. Ele também pode ser causado por um objeto de diretiva de grupo conflitantes. Para obter mais informações, consulte [configurações do Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).

Dependendo das necessidades de negócios, você pode desabilitar a opção de usuário por meio da diretiva de grupo. Use a configuração para **interface do usuário de consentimento de configuração configurar telemetria**. Para saber mais, veja [Configurar dados de diagnóstico do Windows em sua organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).

#### <a name="check-user-proxy"></a>Verificar o proxy de usuário

<!--30,35-->
A configuração DisableEnterpriseAuthProxy é habilitada por padrão para o Windows 7. Para computadores Windows 8.1, o Configuration Manager define a configuração de DisableEnterpriseAuthProxy como 0 (não desativado).

Essa propriedade pode exibir os erros a seguir:

- O proxy de autenticação está habilitado. Defina DisableEnterpriseAuthProxy como 0 na `HKLM\Software\Policies\Microsoft\Windows\DataCollection`

- Não é possível verificar o status de proxy de autenticação. Verifique os logs para os detalhes da exceção

Para obter mais informações, examine M365AHandler.log no cliente.  

Verifique as permissões na chave do registro. Certifique-se de que a conta sistema local pode acessar essa chave para o cliente do Configuration Manager definir. Ele também pode ser causado por um objeto de diretiva de grupo conflitantes. Para obter mais informações, consulte [configurações do Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

#### <a name="commercial-id-configuration"></a>Configuração de ID comercial

<!--9, 11, 53-->
A Microsoft usa uma ID comercial exclusiva para mapear as informações de dispositivos para seu espaço de trabalho de análise de área de trabalho. Quando você integra o Configuration Manager com a análise de área de trabalho, ele consulta automaticamente o serviço para essa ID. Configuration Manager automaticamente deve aplicar essa ID para os clientes para que as configurações de análise de área de trabalho de destino.

Se essa verificação for bem-sucedida, em seguida, o dispositivo esteja devidamente configurado com uma ID comercial.

Caso contrário, ele pode mostrar um dos seguintes erros:

- Não é possível gravar o CommercialId chave do registro `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`. Verificar permissões  

- Não é possível atualizar o CommercialId na chave do registro `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`. Verifique os logs para os detalhes da exceção  

- Forneça o valor correto de CommercialId em `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`  

Para obter mais informações, examine M365AHandler.log no cliente.  

Verifique as permissões na chave do registro. Certifique-se de que a conta sistema local pode acessar essa chave para o cliente do Configuration Manager definir. Ele também pode ser causado por um objeto de diretiva de grupo conflitantes. Para obter mais informações, consulte [configurações do Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Há uma ID diferente para o dispositivo. Essa chave do registro é usada pela política de grupo. Ela terá precedência sobre a ID fornecida pelo Configuration Manager.  

Para exibir a ID comercial no portal de análise de área de trabalho, use o procedimento a seguir:

1. Acesse o portal de análise de área de trabalho e selecione **aos serviços conectados** no grupo de configurações globais.  

2. No **aos serviços conectados** painel, o **registrar dispositivos** painel é selecionado por padrão. No painel de dispositivos de registro, a seção de informações exibe sua chave de ID comercial.  

![Captura de tela da ID comercial no portal de análise de área de trabalho](media/commercial-id.png)

> [!Important]  
> Somente **obter a nova chave de ID** quando você não pode usar o atual. Se você regenerar a ID comercial, implante a nova ID para seus dispositivos. Esse processo pode resultar em perda de dados de diagnóstico durante a transição.  

#### <a name="windows-commercial-data-opt-in"></a>Windows dados comerciais opt-in

<!--64-->
Essa propriedade é específica para dispositivos que executam o Windows 7 ou Windows 8.1. Ele executa testes semelhantes como [Windows dados de diagnóstico opt-in](#windows-diagnostic-data-opt-in), exceto para o CommercialDataOptIn de valor.

#### <a name="check-device-name-in-diagnostic-data"></a>Verifique o nome do dispositivo em dados de diagnóstico

<!--56,58-->
Se essa verificação for bem-sucedida, o dispositivo está configurado corretamente para compartilhar o nome do dispositivo.

Caso contrário, ele pode mostrar um dos seguintes erros:

- Não é possível verificar o nome do dispositivo a serem enviados à Microsoft como parte dos dados de diagnóstico do Windows. Verifique os logs para os detalhes da exceção  

- Não é possível gravar AllowDeviceNameInTelemetry chave do registro `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`. Verificar permissões  

Para obter mais informações, examine M365AHandler.log no cliente.  

Verifique as permissões na chave do registro. Certifique-se de que a conta sistema local pode acessar essa chave para o cliente do Configuration Manager definir. Ele também pode ser causado por um objeto de diretiva de grupo conflitantes. Para obter mais informações, consulte [configurações do Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Certifique-se de que outro mecanismo de política, como a diretiva de grupo, não é desabilitar essa configuração.

#### <a name="diagtrack-service-configuration"></a>Configuração do serviço DiagTrack

<!--44,45,50-->
Se essa verificação for bem-sucedida, o componente DiagTrack está configurado corretamente no dispositivo. A versão mínima necessária pela análise de área de trabalho é 10010586 (10.0.10586).

Caso contrário, ela pode exibir um dos seguintes erros:

- Conectado a experiência do usuário e o componente de telemetria (diagtrack.dll) está desatualizado. Verificar os requisitos  

- Não é possível localizar o componente de telemetria (diagtrack.dll) e a experiência do usuário conectado. Verificar os requisitos  

- Habilitar e iniciar o serviço de telemetria e experiências do usuário conectado para enviar dados à Microsoft  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

Instale as atualizações mais recentes. Para obter mais informações, consulte [atualizações do dispositivo](/sccm/desktop-analytics/enroll-devices#update-devices).

Certifique-se de que o **experiências do usuário conectado e telemetria** serviço no dispositivo está em execução.

#### <a name="diagtrack-version"></a>Versão DiagTrack

Essa propriedade exibirá a versão atual do componente de experiência do usuário conectado e telemetria no dispositivo. Ele mostra a versão do arquivo no `%windir%\System32\diagtrack.dll`, sem pontos decimais. Por exemplo, a versão do arquivo 10.0.10586 exibe como 10010586.

#### <a name="sqm-id-retrieval"></a>Recuperação de ID de SQM

<!--38-->
Essa propriedade é principalmente para dispositivos Windows 7. Ele pode ser usado por versões mais recentes do sistema operacional como um identificador de fallback para o dispositivo.

Se não for bem-sucedido, ele pode ser exibido o seguinte erro:

- Não é possível recuperar o identificador de telemetria do dispositivo herdado (SQM ID)

Para obter mais informações, examine M365AHandler.log no cliente.  

Verifique se que você não tiver IDs duplicadas no seu ambiente. Por exemplo, se os dispositivos foram implantados com uma imagem do sistema operacional que não foi generalizada.

#### <a name="unique-device-identifier-retrieval"></a>Recuperação de identificador exclusivo do dispositivo

<!--54-->
Análise da área de trabalho usa o serviço de Account da Microsoft para uma identidade de dispositivo mais confiável.

Certifique-se a **conta de logon no Assistente do Microsoft** serviço não está desabilitado. O tipo de inicialização deve ser **Manual (início do gatilho)** .

Para desabilitar o acesso à conta do usuário final Microsoft, use as configurações de política em vez de bloquear esse ponto de extremidade. Para obter mais informações, consulte [conta da Microsoft na empresa](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication).

#### <a name="windows-diagnostic-data-opt-in"></a>Windows dados de diagnóstico opt-in

<!--8,40,55,62-->
Essa propriedade verifica se o Windows está configurado corretamente para permitir que os dados de diagnóstico. Ele verifica o valor de Allowtelemetry=0 nas chaves do registro a seguir:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Verifique as permissões nessas chaves do registro. Certifique-se de que a conta sistema local pode acessar essas chaves para o cliente do Configuration Manager definir. Ele também pode ser causado por um objeto de diretiva de grupo conflitantes. Para obter mais informações, consulte [configurações do Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Para obter mais informações, examine M365AHandler.log no cliente.  



## <a name="log-files"></a>Arquivos de log

Use os seguintes arquivos de log para ajudar a solucionar problemas com a análise de área de trabalho integrado ao Configuration Manager.


### <a name="service-connection-point"></a>Ponto de Conexão de Serviço

Os seguintes arquivos de log estão no ponto de conexão de serviço no seguinte diretório: `C:\Program Files\Configuration Manager\Logs\M365A`:

| Log | Descrição |
|---------|---------|
| **M365ADeploymentPlanWorker.log** | Informações sobre a sincronização de plano de implantação de área de trabalho de análise para o Gerenciador de configuração local do serviço de nuvem |
| **M365ADeviceHealthWorker.log** | Informações sobre a integridade do dispositivo carregar do Configuration Manager para a nuvem da Microsoft |
| **M365AUploadWorker.log** | Informações sobre a coleta e o dispositivo carregar do Configuration Manager para a nuvem da Microsoft |
| **SmsAdminUI.log** | Informações sobre a atividade do console do Configuration Manager, como configurar os serviços de nuvem do Azure  |


### <a name="configuration-manager-client"></a>Cliente do Configuration Manager

Os seguintes arquivos de log estão no cliente do Configuration Manager no seguinte diretório: `C:\Windows\CCM\logs`:

| Log | Descrição |
|---------|---------|
| **M365AHandler.log** | Informações sobre a política de configurações de área de trabalho de análise |


### <a name="enable-verbose-logging"></a>Habilitar o log detalhado

1. No ponto de conexão de serviço, vá para a seguinte chave do registro: `HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Defina as **LogLevel** valor `0`  
3. (Opcional) Execute o seguinte comando SQL no banco de dados do site:  

    ```SQL
    DELETE FROM M365AProperties WHERE Name = 'M365ATenantUpdateInfo_LastUpdateTime'
    ```

4. Reinicie o **SMS_EXECUTIVE** serviço no servidor do site



## <a name="bkmk_AzureADApps"></a> Aplicativos do Azure AD

Análise da área de trabalho adiciona os seguintes aplicativos ao AD do Azure:

- **Gerenciador de configuração de Microsserviço**: Conecta o Configuration Manager com a análise da área de trabalho. Este aplicativo não tem nenhum requisito de acesso.  

- **MALogAnalyticsReader**: Recupera grupos do OMS e os dispositivos criados no Log Analytics. Para obter mais informações, consulte [função de aplicativo MALogAnalyticsReader](#bkmk_MALogAnalyticsReader).  

Se você precisar provisionar esses aplicativos depois de concluir o conjunto de backup, vá para o **aos serviços conectados** painel. Selecione **configurar o acesso de usuários e aplicativos**e provisionar os aplicativos.  

- **Aplicativo do Azure AD para o Configuration Manager**. Se você precisar provisionar ou solucionar problemas de conexão depois de concluir o conjunto de backup, consulte [importação e criar aplicativos para o Configuration Manager](#create-and-import-app-for-configuration-manager). Este aplicativo requer **gravar dados de coleção do CM** e **ler dados de coleção do CM** no **Configuration Manager Service** API.  


### <a name="create-and-import-app-for-configuration-manager"></a>Criar e importar um aplicativo para o Configuration Manager

Se você não pode criar esse aplicativo do Azure AD no Assistente para configurar serviços do Azure no Configuration Manager, use as seguintes etapas para criar e importar o aplicativo para o Configuration Manager manualmente.

#### <a name="create-app-in-azure-ad"></a>Criar um aplicativo no Azure AD

1. Abra o [portal do Azure](http://portal.azure.com) como um usuário com permissões de administrador da empresa, acesse **Azure Active Directory**e selecione **registros do aplicativo**. Em seguida, selecione **novo registro de aplicativo**.  

2. No **criar** painel, defina as seguintes configurações:  

    - **Nome**: um nome exclusivo que identifica o aplicativo, por exemplo: `Desktop-Analytics-Connection`  

    - **Tipo de aplicativo**: **Aplicativo Web / API**  

    - **URL de logon**: esse valor não é usado pelo Configuration Manager, mas exigido pelo Azure AD. Insira uma URL exclusiva e é válida, por exemplo: `https://configmgrapp`  
  
   Selecione **Criar**.  

3. Selecione o aplicativo e observe os **ID do aplicativo**. Esse valor é um GUID que é usado para configurar a conexão do Configuration Manager.  

4. Selecione **as configurações** sobre o aplicativo e, em seguida, selecione **chaves**. No **senhas** , digite um **descrição da chave**, especifique uma expiração **duração**e, em seguida, selecione **salvar**. Cópia de **valor** da chave, que é usado para configurar a conexão do Configuration Manager.

    > [!Important]  
    > Isso é a única oportunidade para copiar o valor da chave. Se você não copiá-lo agora, você precisará criar outra chave.  
    >
    > Salve o valor da chave em um local seguro.  

5. No aplicativo **as configurações** painel, selecione **permissões necessárias**.  

    1. Sobre o **permissões necessárias** painel, selecione **Add**.  

    2. No **adicionar acesso à API** painel **selecionar uma API**.  

    3. Pesquise o **Microsserviço do Configuration Manager** API. Selecione-o e, em seguida, escolha **selecionar**.  

    4. Sobre o **habilitar acesso** painel, selecione ambas as permissões de aplicativo: **Gravar dados de coleção de CM** e **ler dados de coleção de CM**. Em seguida, escolha **selecionar**.  

    5. Sobre o **adicionar acesso à API** painel, selecione **feito**.  

6. Sobre o **permissões necessárias** página, selecione **conceder permissões**. Selecione **Sim**.  

7. Copie a ID de locatário do AD do Azure. Esse valor é um GUID que é usado para configurar a conexão do Configuration Manager. Selecione **Azure Active Directory** no menu principal e, em seguida, selecione **propriedades**. Cópia de **ID de diretório** valor.  

#### <a name="import-app-in-configuration-manager"></a>Importação de aplicativo no Configuration Manager

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Serviços do Azure**. Selecione **configurar serviços do Azure** na faixa de opções.  

2. Sobre o **serviços do Azure** página do Assistente de serviços do Azure, defina as seguintes configurações:  

    - Especifique um **Nome** para o objeto no Configuration Manager.  

    - Especifique uma **Descrição** opcional para ajudá-lo a identificar o serviço.  

    - Selecione **análise de área de trabalho** na lista de serviços disponíveis.  
  
   Selecione **Avançar**.  

3. Sobre o **aplicativo** , selecione apropriado **ambiente do Azure**. Em seguida, selecione **importação** para o aplicativo web. Defina as seguintes configurações na **importar aplicativos** janela:  

    - **Nome do locatário do Azure AD**: Esse nome é como ele é chamado no Configuration Manager  

    - **ID de locatário do Azure AD**: O **ID de diretório** você copiou do Azure AD  

    - **ID do cliente**: O **ID do aplicativo** você copiou do aplicativo Azure AD  

    - **Chave secreta**: A tecla **valor** você copiou do aplicativo Azure AD  

    - **Vencimento da Chave Secreta**: A mesma data de expiração da chave  

    - **URI da ID do aplicativo**: Essa configuração deve preencher automaticamente com o seguinte valor: `https://cmmicrosvc.manage.microsoft.com/`  
  
   Selecione **Verify**e, em seguida, selecione **Okey** para fechar a janela Importar aplicativos. Selecione **próxima** na página do aplicativo do Assistente de serviços do Azure.  

Para continuar o restante do assistente no **dados de diagnóstico** página, consulte [conectar ao serviço](/sccm/desktop-analytics/connect-configmgr#bkmk_connect).


### <a name="bkmk_MALogAnalyticsReader"></a> Função de aplicativo MALogAnalyticsReader

Quando você configurar a análise de área de trabalho, você aceita um consentimento em nome de sua organização. Esse consentimento é atribuir o aplicativo MALogAnalyticsReader a função de leitor do Log Analytics para o espaço de trabalho. Essa função de aplicativo é necessária pela análise de área de trabalho.

Se houver um problema com esse processo durante o conjunto de backup, use o seguinte processo para adicionar manualmente essa permissão:

1. Vá para o [portal do Azure](http://portal.azure.com)e selecione **todos os recursos**. Selecione o espaço de trabalho do tipo **do Log Analytics**.  

2. No menu do espaço de trabalho, selecione **controle de acesso (IAM)** , em seguida, selecione **Add**.  

3. No **adicionar permissões** painel, defina as seguintes configurações:  

    - **Função**: **Leitor do log Analytics**  

    - **Atribuir acesso a**: **Usuário, grupo ou aplicativo do Azure AD**  

    - **Selecione**: **MALogAnalyticsReader**  

4. Selecione **Salvar**.

O portal mostrará uma notificação de que ele adicionou a atribuição de função.


## <a name="data-latency"></a>Latência de dados

<!-- 3846531 -->
Dados no portal de análise de área de trabalho são atualizados diariamente. Esta atualização inclui alterações de dispositivo coletadas dos dados de diagnóstico e as alterações feitas na configuração. Por exemplo, quando você altera um ativo **decisão de atualização**, ele pode resultar em alterações para o estado de preparação de dispositivos com esse ativo instalado.

- **As alterações de administrador** geralmente são processadas pelo serviço de análise de área de trabalho dentro de nove horas. Por exemplo, se você fizer alterações às 11:00 PM UTC, o portal deve refletir essas alterações antes do UTC-08:00 AM no dia seguinte.

- **Alterações de dispositivo** detectado por UTC a meia-noite no horário local geralmente são incluídos na atualização diária. Normalmente é mais 23 horas de latência associada com o processamento das alterações de dispositivo em comparação com as alterações de administrador.

Se você não estiver vendo as alterações atualizadas dentro desses intervalos de tempo, aguarde a outra 24 horas para a próxima atualização diária. Se você vir a intervalos mais longos, verifique o painel de integridade do serviço. Se o serviço de relatórios como íntegros, entre em contato com o suporte da Microsoft.

Ao configurar a análise de área de trabalho pela primeira vez, os gráficos no Configuration Manager e o portal de análise de área de trabalho podem não mostrar dados completos. Pode levar 2 a 3 dias para dispositivos ativos enviar dados de diagnóstico para o serviço de análise de área de trabalho, o serviço para processar os dados e, em seguida, sincronizar com seu site do Configuration Manager.

Em uma hierarquia do Configuration Manager, ele pode levar 10 minutos para novas coleções aparecerá para planos de implantação. Os sites primários criarem as coleções, e o site de administração central sincroniza com análise de área de trabalho.<!-- 3896921 -->
