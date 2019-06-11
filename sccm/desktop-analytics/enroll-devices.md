---
title: Registrar dispositivos de área de trabalho de análise
titleSuffix: Configuration Manager
description: Saiba como registrar dispositivos de área de trabalho de análise.
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 959061a764cff9f27defc4c0b0bf4eaa45b70afd
ms.sourcegitcommit: 725e1bf7d3250c2b7b7be9da01135517428be7a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822025"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>Como registrar dispositivos no Analytics de área de trabalho

> [!Note]  
> Essas informações se relaciona a um serviço de visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Quando você [conectar o Configuration Manager](/sccm/desktop-analytics/connect-configmgr) para análise de área de trabalho, você definir configurações para registrar dispositivos para análise de área de trabalho. Você pode alterar essas configurações a qualquer momento. Além disso, verifique se que os dispositivos estão atualizados.



## <a name="update-devices"></a>Atualizar dispositivos

Há dois tipos de atualizações que você precisa aplicar a melhor experiência com a área de trabalho de análise:

- [Atualizações de compatibilidade](#bkmk_appraiser)  
- [Serviço de telemetria e experiências do usuário conectado](#bkmk_diagtrack)


### <a name="bkmk_appraiser"></a> Atualizações de compatibilidade

O componente de compatibilidade (avaliador) executa o diagnóstico no dispositivo Windows para avaliar seus status de compatibilidade com as versões mais recentes do Windows 10.

Microsoft incrementa regularmente as atualizações para este componente, mas o número KB associado não muda. Certifique-se de que você sempre tenha a versão mais recente da atualização.

Reinicie dispositivos depois de instalar as atualizações de compatibilidade pela primeira vez.

> [!Tip]  
> Use o Configuration Manager para instalar automaticamente a versão mais recente dessas atualizações. Para mais informações, consulte [Implantar atualizações de software](/sccm/sum/deploy-use/deploy-software-updates).  

> [!Note]  
> Há uma atualização opcional relacionada [3150513 KB](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=3150513). Essa atualização fornece definições para as atualizações mais antigas de compatibilidade e configuração atualizada. Para obter mais informações, consulte [atualização de definição de compatibilidade mais recente do Windows](https://support.microsoft.com/help/3150513).  

#### <a name="windows-10"></a>Windows 10

O Windows 10 inclui o componente de compatibilidade. Para obter a atualização de compatibilidade mais recente, instale a atualização cumulativa mais recente do Windows 10.

#### <a name="windows-81"></a>Windows 8.1

Baixe a atualização: [KB 2976978](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2976978) 

Executa o diagnóstico nos sistemas Windows 8.1 que participam do programa de Aperfeiçoamento da experiência do cliente do Windows. Estes diagnósticos ajudam a determinar se você pode ter problemas de compatibilidade ao atualizar para o Windows 10.

Para obter mais informações, consulte [atualização de compatibilidade para manter-se atualizado no Windows 8.1 a Windows](https://support.microsoft.com/help/2976978).

#### <a name="windows-7-with-service-pack-1"></a>Windows 7 com Service Pack 1

Baixe a atualização: [KB 2952664](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2952664) 

Executa o diagnóstico na do Windows 7 com sistemas de Service Pack 1 (SP1) que participam do programa de Aperfeiçoamento da experiência do cliente do Windows. Estes diagnósticos ajudam a determinar se você pode ter problemas de compatibilidade ao atualizar para o Windows 10.

Para obter mais informações, consulte [atualização de compatibilidade para manter-se atualizado no Windows 7 o Windows](https://support.microsoft.com/help/2952664).


### <a name="bkmk_diagtrack"></a> Serviço de telemetria e experiências do usuário conectado

Com a dados de diagnóstico do Windows habilitados, o serviço de experiência do usuário conectado e telemetria (DiagTrack) coleta dados de sistema, o aplicativo e o driver. A Microsoft analisa esses dados e compartilhamentos de volta para você por meio da análise de área de trabalho.

Para obter a melhor experiência, instale as atualizações a seguir dependendo da versão do sistema operacional.

> [!Note]  
> Quando você instalar essas atualizações, esperar que os seguintes comportamentos:
> 
> - Dispositivos que você se registra para análise de área de trabalho aparecem no serviço em menos de uma hora  
> - Dispositivos rapidamente relatam o status de atualizações de recurso e qualidade do Windows  
>
> Sem essas atualizações, esses processos podem levar mais de 48 horas para um dispositivo relatar a análise de área de trabalho.  


#### <a name="windows-10"></a>Windows 10

Instale a atualização cumulativa mais recente do Windows 10.

<!-- 
- Windows 10 1809: Included in RTM build
- Windows 10 1803: [KB4458469](https://support.microsoft.com/help/4458469) (OS Build 17134.319)
- Windows 10 1709: [KB4457136](https://support.microsoft.com/help/4457136) (OS Build 16299.697)
- Windows 10 1703: [KB4457141](https://support.microsoft.com/help/4457141) (OS Build 15063.1358)
- Windows 10 1607: [KB4457127](https://support.microsoft.com/help/4457127) (OS Build 14393.2517)
 -->

#### <a name="windows-81"></a>Windows 8.1

Instale o pacote cumulativo mensal de outubro de 2018, [KB4462926](https://support.microsoft.com/help/4462926)

#### <a name="windows-7"></a>Windows 7

Instale o pacote cumulativo mensal de outubro de 2018, [KB4462923](https://support.microsoft.com/help/4462923)



## <a name="device-enrollment"></a>Registro de dispositivo

O serviço de análise de área de trabalho tem sem agentes para instalar. Registro de dispositivo requer a configuração de configurações nos dispositivos que você deseja monitorar. Essas configurações controlam a qual instância de área de trabalho de análise que o dispositivo deve enviar seus dados e outras opções de configuração.

> [!Note]  
> Se você já estiver usando o Windows Analytics, use o mesmo espaço de trabalho para análise de área de trabalho. Você precisará registrar novamente os dispositivos para análise de área de trabalho que você registrou anteriormente no Windows Analytics.
>
> Você pode ter apenas um espaço de trabalho de análise de área de trabalho por locatário do Azure AD. Dispositivos podem enviar somente dados de diagnóstico para um espaço de trabalho.  

Configuration Manager fornece uma experiência integrada para gerenciar e implantar essas configurações para os clientes. Para obter a melhor experiência, use o Configuration Manager.

Quando você conecta o Configuration Manager para análise de área de trabalho, você pode definir as configurações para registrar dispositivos. Para obter mais informações, consulte [como conectar o Configuration Manager com a área de trabalho de análise](/sccm/desktop-analytics/connect-configmgr#bkmk_connect).

Para alterar essas configurações, use o procedimento a seguir:

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Serviços do Azure**. Selecione a conexão de área de trabalho de análise e, em seguida, escolha **propriedades** na faixa de opções.

2. Sobre o **dados de diagnóstico** página, faça as alterações necessárias para as seguintes configurações:  

    - **ID comercial**: esse valor deve preencher automaticamente com a ID. da sua organização Se ele não abrir, certifique-se de seu servidor proxy está configurado para permitir todos os itens necessários [pontos de extremidade](/sccm/desktop-analytics/enable-data-sharing#endpoints) antes de continuar. Como alternativa, recuperar sua ID comercial manualmente a partir de [portal de análise de área de trabalho](/sccm/desktop-analytics/troubleshooting#bkmk_ViewCommercialID).   

    - **Nível de dados de diagnóstico do Windows 10**: Para obter mais informações, consulte [níveis de dados de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

    - **Permitir que o nome do dispositivo nos dados de diagnóstico**: Para obter mais informações, consulte [nome do dispositivo](#device-name).  

    Quando você faz alterações a esta página, o **funcionalidade disponível** página mostra uma visualização da funcionalidade de análise de área de trabalho com as configurações de dados de diagnóstico selecionado.  

3. Sobre o **Conexão de análise de área de trabalho** de página, faça as alterações necessárias para as seguintes configurações:

    - **Nome de exibição**: O portal de análise de área de trabalho exibe essa conexão do Configuration Manager usando esse nome.  

    - **Coleção de destino**: Esta coleção inclui todos os dispositivos que o Configuration Manager configura com sua ID comercial e as configurações de dados de diagnóstico. É o conjunto completo de dispositivos do Configuration Manager se conecta ao serviço de análise de área de trabalho.  

    - **Dispositivos na coleção de destino usam um proxy de usuário autenticado para comunicação de saída**: Por padrão, esse valor é **não**. Se for necessário em seu ambiente, definido como **Sim**. Para obter mais informações, consulte [autenticação do servidor Proxy](/sccm/desktop-analytics/enable-data-sharing#proxy-server-authentication).  

    - **Selecione as coleções específicas para sincronizar com a área de trabalho de análise**: Selecione **Add** incluir coleções adicionais de seus **coleção de destino** hierarquia. Essas coleções estão disponíveis no portal de análise de área de trabalho para o agrupamento com planos de implantação. Certifique-se de incluir coleções de exclusão do projeto-piloto e piloto.  <!-- 4097528 -->

        > [!Important] 
        > Essas coleções continuam a sincronização como suas alterações de associação. Por exemplo, o seu plano de implantação usa uma coleção com uma regra de associação do Windows 7. Como esses dispositivos de atualização para o Windows 10, e o Configuration Manager avalia a associação da coleção, esses dispositivos soltem fora a coleta e o plano de implantação.  


### <a name="windows-settings"></a>Configurações do Windows

O Configuration Manager define as seguintes configurações do Windows em `Microsoft\Windows\DataCollection`:

| Política   | Valor  |
|----------|--------|
| **CommercialId** | Para um dispositivo apareça na área de trabalho de análise que, configurá-lo com a ID comercial. sua organização |
| **AllowTelemetry**  | Definir `1` para **básicas**, `2` para **avançado**, ou `3` para **completo** dados de diagnóstico. Análise da área de trabalho requer dados de diagnóstico básicos de pelo menos. A Microsoft recomenda que você use o nível avançado (limitado) com a análise de área de trabalho. Para saber mais, veja [Configurar dados de diagnóstico do Windows em sua organização](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | *Aplica-se ao Windows 10, versão 1709 e posterior*: Essa configuração se aplica somente quando a configuração de Allowtelemetry=0 é `2`. Ele limita os eventos de dados de diagnóstico avançado enviados à Microsoft para apenas os eventos necessários pela análise de área de trabalho. Para obter mais informações, consulte [Windows 10, versão 1709 aprimorada eventos de dados de diagnóstico e os campos usados pelo Windows Analytics](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields).|
| **AllowDeviceNameInTelemetry** | *Aplica-se ao Windows 10, versão 1803 e posterior*: Um opt-in separado é necessário para permitir que dispositivos continuam a enviar o nome do dispositivo.<br> <br>Observação: Por padrão, o nome do dispositivo não será enviado à Microsoft. Se você não enviar o nome do dispositivo, ele aparece na área de trabalho de análise como "Desconhecido". Esse comportamento pode tornar difícil de identificar e avaliar os dispositivos. Para obter mais informações, consulte [nome do dispositivo](#device-name). |
| **CommercialDataOptIn** | *Aplica-se ao Windows 7 e Windows 8.1*: Um valor de `1` é necessária para análises de área de trabalho. Para obter mais informações, consulte [Opt-in dados comerciais no Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |

Exiba essas configurações no editor de diretiva de grupo no seguinte caminho: **Configuração do computador** > **modelos administrativos** > **componentes do Windows** > **dados coleta e a versão prévia Compilações**.

> [!Important]  
> Na maioria das circunstâncias, apenas use o Configuration Manager para definir essas configurações. Também não aplica essas configurações nos objetos de diretiva de grupo do domínio. Para obter mais informações, consulte [resolução de conflitos](#conflict-resolution).<!-- SCCMDocs-pr 3120 -->

### <a name="device-name"></a>Nome do dispositivo

Começando no Windows 10, versão 1803, o nome do dispositivo não é coletado por padrão. Coleta o nome do dispositivo com os dados de diagnóstico requer um opt-in separado. Sem o nome do dispositivo, é mais difícil para você identificar quais dispositivos requerem atenção ao avaliar uma atualização para uma nova versão do Windows.

Se você não enviar o nome do dispositivo, ele aparece na área de trabalho de análise como "Desconhecido".

![Lista de dispositivos de análise da área de trabalho mostrando os nomes "desconhecidos"](media/unknown-device-name.png)

Há uma opção nas configurações do Configuration Manager para análise de área de trabalho configurar essa opção: **Permitir que o nome do dispositivo nos dados de diagnóstico**. Essa configuração do Configuration Manager controla a configuração de política do Windows, AllowDeviceNameInTelemetry.
 

### <a name="conflict-resolution"></a>resolução de conflitos

Em geral, use coleções do Configuration Manager para registro e configurações de análise de área de trabalho de destino. Use associação direta ou consultas para incluir ou excluir dispositivos da coleção. Para obter mais informações, confira [Como criar coleções](/sccm/core/clients/manage/collections/create-collections).

Configuration Manager configura apenas as configurações do Windows, se um valor ainda não existir. Se você precisar definir configurações diferentes para um único grupo de dispositivos, você pode usar [política de grupo](#windows-settings). Configurações direcionadas pela política de grupo têm precedência sobre configurações do Configuration Manager.

Se você direcionar os clientes do Configuration Manager com as configurações do Windows Analytics e análise de área de trabalho, as configurações para análise de área de trabalho terão precedência.

Quando você configura o nível de dados de diagnóstico, você pode definir o limite superior para o dispositivo. Por padrão no Windows 10, versão 1803 e posterior, os usuários podem escolher definir um nível inferior. Você pode controlar esse comportamento usando a configuração de política de grupo **interface do usuário de consentimento de configuração configurar telemetria**. Para saber mais, veja [Configurar dados de diagnóstico do Windows em sua organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).



## <a name="next-steps"></a>Próximas etapas

Avance para o próximo artigo para criar planos de implantação na área de trabalho de análise.
> [!div class="nextstepaction"]  
> [Criar planos de implantação](/sccm/desktop-analytics/create-deployment-plans)  
