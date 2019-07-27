---
title: Registrar dispositivos na análise de desktop
titleSuffix: Configuration Manager
description: Saiba como registrar dispositivos na análise de desktops.
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7099a31cc9766a3c9904c5ae1013eb1700181102
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68535964"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>Como registrar dispositivos no desktop Analytics

> [!Note]  
> Essas informações se relacionam a um serviço de visualização que pode ser substancialmente modificado antes de ser lançada comercialmente. A Microsoft não oferece garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Ao [conectar Configuration Manager](/sccm/desktop-analytics/connect-configmgr) ao desktop Analytics, você define as configurações para registrar dispositivos na análise de desktops. Você pode alterar essas configurações a qualquer momento. Verifique também se os dispositivos estão atualizados.



## <a name="update-devices"></a>Atualizar dispositivos

Há dois tipos de atualizações que você precisa aplicar para obter a melhor experiência com a análise de desktops:

- [Atualizações de compatibilidade](#bkmk_appraiser)  
- [Serviço de telemetria e experiências de usuário conectado](#bkmk_diagtrack)


### <a name="bkmk_appraiser"></a>Atualizações de compatibilidade

O componente de compatibilidade (avaliador) executa o diagnóstico no dispositivo Windows para avaliar seu status de compatibilidade com as versões mais recentes do Windows 10.

A Microsoft incrementa regularmente as atualizações para esse componente, mas o número de KB associado não é alterado. Certifique-se de que você sempre tenha a versão mais recente da atualização.

Reinicie os dispositivos depois de instalar as atualizações de compatibilidade pela primeira vez.

> [!Tip]  
> Use Configuration Manager para instalar automaticamente a versão mais recente dessas atualizações. Para mais informações, consulte [Implantar atualizações de software](/sccm/sum/deploy-use/deploy-software-updates).  

> [!Note]  
> Há uma atualização opcional relacionada, [KB 3150513](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=3150513). Esta atualização fornece configurações atualizadas e definições para atualizações de compatibilidade mais antigas. Para obter mais informações, consulte [atualização de definição de compatibilidade mais recente para Windows](https://support.microsoft.com/help/3150513).  

#### <a name="windows-10"></a>Windows 10

O Windows 10 inclui o componente de compatibilidade. Para obter a atualização de compatibilidade mais recente, instale a atualização cumulativa mais recente do Windows 10.

#### <a name="windows-81"></a>Windows 8.1

Baixe a atualização: [KB 2976978](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2976978) 

Executa o diagnóstico nos sistemas Windows 8.1 que participam da Programa de Aperfeiçoamento da Experiência do Usuário do Windows. Esses diagnósticos ajudam a determinar se você pode ter problemas de compatibilidade ao atualizar para o Windows 10.

Para obter mais informações, consulte [atualização de compatibilidade para manter o Windows atualizado em Windows 8.1](https://support.microsoft.com/help/2976978).

#### <a name="windows-7-with-service-pack-1"></a>Windows 7 com Service Pack 1

Baixe a atualização: [KB 2952664](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2952664) 

Executa o diagnóstico nos sistemas Windows 7 com Service Pack 1 (SP1) que participam do Windows Programa de Aperfeiçoamento da Experiência do Usuário. Esses diagnósticos ajudam a determinar se você pode ter problemas de compatibilidade ao atualizar para o Windows 10.

Para obter mais informações, consulte [atualização de compatibilidade para manter o Windows atualizado no Windows 7](https://support.microsoft.com/help/2952664).


### <a name="bkmk_diagtrack"></a>Serviço de telemetria e experiências de usuário conectado

Com os dados de diagnóstico do Windows habilitados, o serviço conectado de experiência do usuário e telemetria (DiagTrack) coleta dados do sistema, do aplicativo e do driver. A Microsoft analisa esses dados e os compartilha de volta para você por meio da análise de desktops.

Para obter a melhor experiência, instale as seguintes atualizações dependendo da versão do sistema operacional.

> [!Note]  
> Ao instalar essas atualizações, espere os seguintes comportamentos:
> 
> - Os dispositivos que você registra para o desktop Analytics aparecem no serviço em menos de uma hora  
> - Os dispositivos relatam rapidamente o status no recurso do Windows e atualizações de qualidade  
>
> Sem essas atualizações, esses processos podem levar mais de 48 horas para que um dispositivo relate para a análise de desktops.  


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

Instalar o acúmulo mensal de outubro de 2018, [KB4462926](https://support.microsoft.com/help/4462926)

#### <a name="windows-7"></a>Windows 7

Instalar o acúmulo mensal de outubro de 2018, [KB4462923](https://support.microsoft.com/help/4462923)



## <a name="device-enrollment"></a>Registro de dispositivo

O serviço de análise de área de trabalho não tem agentes para instalar. O registro de dispositivo requer a definição de configurações nos dispositivos que você deseja que ele monitore. Essas configurações controlam a qual instância da análise de desktop o dispositivo deve enviar seus dados e outras opções de configuração.

> [!Note]  
> Se você já estiver usando o Windows Analytics, use esse mesmo espaço de trabalho para análise de desktop. Você precisa registrar novamente os dispositivos no desktop Analytics que você registrou anteriormente no Windows Analytics.
>
> Você só pode ter um espaço de trabalho do desktop Analytics por locatário do Azure AD. Os dispositivos só podem enviar dados de diagnóstico para um espaço de trabalho.  

O Configuration Manager fornece uma experiência integrada para gerenciar e implantar essas configurações em clientes. Para obter a melhor experiência, use Configuration Manager.

Ao conectar Configuration Manager ao desktop Analytics, você define as configurações para registrar dispositivos. Para obter mais informações, consulte [como conectar Configuration Manager com o desktop Analytics](/sccm/desktop-analytics/connect-configmgr#bkmk_connect).

Para alterar essas configurações, use o seguinte procedimento:

1. No console do Configuration Manager, acesse o workspace **Administração**, expanda **Serviços de Nuvem** e selecione o nó **Serviços do Azure**. Selecione a conexão com o desktop Analytics e escolha **Propriedades** na faixa de opções.

2. Na página **dados de diagnóstico** , faça as alterações necessárias para as seguintes configurações:  

    - **ID comercial**: esse valor deve ser preenchido automaticamente com a ID da sua organização. Caso contrário, verifique se o servidor proxy está configurado para permitir todos os [pontos de extremidade](/sccm/desktop-analytics/enable-data-sharing#endpoints) necessários antes de continuar. Como alternativa, recupere sua ID comercial manualmente no [portal do desktop Analytics](/sccm/desktop-analytics/monitor-connection-health#bkmk_ViewCommercialID).   

    - **Nível de dados de diagnóstico do Windows 10**: Para obter mais informações, consulte [diagnóstico de níveis de dados](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

    - **Permitir nome do dispositivo em dados de diagnóstico**: Para obter mais informações, consulte [nome do dispositivo](#device-name).  

    Quando você faz alterações nessa página, a página **funcionalidade disponível** mostra uma visualização da funcionalidade de análise de desktop com as configurações de dados de diagnóstico selecionadas.  

3. Na página **conexão do desktop Analytics** , faça as alterações necessárias para as seguintes configurações:

    - **Nome de exibição**: O portal do desktop Analytics exibe essa Configuration Manager conexão usando esse nome.  

    - **Coleção de destino**: Essa coleção inclui todos os dispositivos que Configuration Manager configurados com a ID comercial e as configurações de dados de diagnóstico. É o conjunto completo de dispositivos que Configuration Manager se conecta ao serviço de análise de desktop.  

    - **Os dispositivos na coleção de destino usam um proxy autenticado pelo usuário para a comunicação de saída**: Por padrão, esse valor é **não**. Se necessário em seu ambiente, defina como **Sim**. Para obter mais informações, consulte [autenticação do servidor proxy](/sccm/desktop-analytics/enable-data-sharing#proxy-server-authentication).  

    - **Selecione coleções específicas para sincronizar com o desktop Analytics**: Selecione **Adicionar** para incluir coleções adicionais de sua hierarquia de **coleção de destino** . Essas coleções estão disponíveis no portal do desktop Analytics para agrupamento com planos de implantação. Certifique-se de incluir coleções de exclusão piloto e piloto.  <!-- 4097528 -->

        > [!Important] 
        > Essas coleções continuam a ser sincronizadas como suas alterações de associação. Por exemplo, seu plano de implantação usa uma coleção com uma regra de associação do Windows 7. À medida que os dispositivos são atualizados para o Windows 10 e Configuration Manager avalia a associação da coleção, os dispositivos saem da coleção e do plano de implantação.  


### <a name="windows-settings"></a>Configurações do Windows

Configuration Manager define as seguintes configurações do Windows no caminho `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`da política local:

| Política   | Valor  |
|----------|--------|
| **CommercialId** | Para que um dispositivo seja exibido no desktop Analytics, configure-o com a ID comercial da sua organização. |
| **AllowTelemetry**  | Defina `1` para **básico**, `2` para **avançado**ou `3` para dados de diagnóstico **completos** . A análise de desktops requer pelo menos dados básicos de diagnóstico. A Microsoft recomenda que você use o nível avançado (limitado) com a análise de desktop. Para saber mais, veja [Configurar dados de diagnóstico do Windows em sua organização](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | *Aplica-se ao Windows 10, versão 1709 e posterior*: Essa configuração se aplica somente quando a configuração AllowTelemetry `2`é. Ele limita os eventos de dados de diagnóstico aprimorados enviados à Microsoft apenas aos eventos necessários para a análise de desktops. Para obter mais informações, consulte [eventos e campos de dados de diagnóstico aprimorados do Windows 10, versão 1709 usados pelo Windows Analytics](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields).|
| **AllowDeviceNameInTelemetry** | *Aplica-se ao Windows 10, versão 1803 e posterior*: Uma aceitação separada é necessária para permitir que os dispositivos continuem a enviar o nome do dispositivo.<br> <br>Observação: O nome do dispositivo não é enviado para a Microsoft por padrão. Se você não enviar o nome do dispositivo, ele aparecerá na análise de desktop como "desconhecido". Esse comportamento pode dificultar a identificação e a avaliação de dispositivos. Para obter mais informações, consulte [nome do dispositivo](#device-name). |
| **CommercialDataOptIn** | *Aplica-se ao Windows 7 e Windows 8.1*: Um valor de `1` é necessário para a análise de desktop. Para obter mais informações, consulte [aceitação de dados comerciais no Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |

Exiba essas configurações no editor de diretiva de grupo no seguinte caminho: Configuração > do computador > **modelos administrativos** > **coleta de dados de** **componentes do Windows**e compilações de visualização.

> [!Important]  
> Na maioria das circunstâncias, use apenas Configuration Manager para definir essas configurações. Não aplique também essas configurações em objetos de diretiva de grupo de domínio. Para obter mais informações, consulte [resolução de conflitos](#conflict-resolution).<!-- SCCMDocs-pr 3120 -->

### <a name="device-name"></a>Nome do dispositivo

A partir do Windows 10, versão 1803, o nome do dispositivo não é mais coletado por padrão. A coleta do nome do dispositivo com os dados de diagnóstico requer uma aceitação separada. Sem o nome do dispositivo, é mais difícil identificar quais dispositivos exigem atenção ao avaliar uma atualização para uma nova versão do Windows.

Se você não enviar o nome do dispositivo, ele aparecerá na análise de desktop como "desconhecido".

![Lista de dispositivos do desktop Analytics mostrando nomes "desconhecidos"](media/unknown-device-name.png)

Há uma opção na Configuration Manager configurações do desktop Analytics para configurar essa opção: **Permitir nome do dispositivo em dados de diagnóstico**. Essa configuração de Configuration Manager controla a configuração da política do Windows, AllowDeviceNameInTelemetry.
 

### <a name="conflict-resolution"></a>Resolução de conflitos

Em geral, use coleções de Configuration Manager para direcionar as configurações de análise de desktop e o registro. Use a associação direta ou as consultas para incluir ou excluir dispositivos da coleção. Para obter mais informações, confira [Como criar coleções](/sccm/core/clients/manage/collections/create-collections).

Configuration Manager só definirá as configurações do Windows se um valor ainda não existir. Se você precisar definir configurações diferentes para um grupo exclusivo de dispositivos, poderá usar a [política de grupo](#windows-settings). As configurações direcionadas pela diretiva de grupo têm precedência sobre as configurações de Configuration Manager.

Se você direcionar clientes Configuration Manager com as configurações do Windows Analytics e do desktop Analytics, as configurações para análise de desktop têm precedência.

Ao configurar o nível de dados de diagnóstico, você define o limite superior para o dispositivo. Por padrão, no Windows 10, versão 1803 e posterior, os usuários podem optar por definir um nível mais baixo. Você pode controlar esse comportamento usando a configuração da política de grupo, **Configurar a configuração de aceitação de telemetria interface do usuário**. Para saber mais, veja [Configurar dados de diagnóstico do Windows em sua organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).



## <a name="next-steps"></a>Próximas etapas

Avance para o próximo artigo para criar planos de implantação na análise de desktops.
> [!div class="nextstepaction"]  
> [Criar planos de implantação](/sccm/desktop-analytics/create-deployment-plans)  
