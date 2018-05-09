---
title: Technical Preview 1710 | Microsoft Docs
titleSuffix: Configuration Manager
description: Saiba mais sobre os recursos disponíveis na Technical Preview versão 1710 do System Center Configuration Manager.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f4706a58-1f11-4eab-b1eb-3d1a0da02d0f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 730d14c5985c088d964761bb83043f3a34924486
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="capabilities-in-technical-preview-1710-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1710 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos que estão disponíveis na Technical Preview do System Center Configuration Manager, versão 1710. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview. Antes de instalar esta versão da visualização técnica, veja [Visualização Técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos e limitações gerais de uso de uma visualização técnica, como atualizar entre versões e como fornecer comentários sobre os recursos em uma visualização técnica.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conhecidos nesse Technical Preview:**
-   **Suporte para Windows 10, versão 1709 (também conhecido como Atualização para Criadores de Outono)**.  A partir dessa versão do Windows, a mídia do Windows inclui várias edições. Ao configurar uma sequência de tarefas para usar um pacote de atualização do sistema operacional ou imagem do sistema operacional, selecione uma [edição com suporte para uso no Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).
-   **A atualização para uma versão prévia falha quando há um servidor do site no modo passivo**. Quando você executa uma versão prévia que tem um [servidor do site primário no modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), você deverá desinstalar o servidor do site de modo passivo para que seja possível atualizar seu site da versão prévia com êxito para essa nova versão prévia. Você pode reinstalar o servidor de site no modo passivo após a conclusão da instalação pelo site.

  Para desinstalar o servidor do site no modo passivo:
  1. No console, acesse **Administração** > **Visão geral** > **Configuração do Site** > **Servidores e Funções do Sistema de Sites** e selecione o servidor de site no modo passivo.
  2. No painel **Funções do Sistema de Site**, clique com o botão direito na função **Servidor do Site** e, em seguida, escolha **Remover Função**.
  3. Clique com o botão direito no servidor do site de modo passivo e, em seguida, escolha **Excluir**.
  4. Após a desinstalação do servidor do site, no servidor do site primário ativo, reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.

**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-deploying-powershell-scripts-from-configuration-manager"></a>Melhorias para a implantação de scripts do PowerShell do Configuration Manager
Com esta versão, agora há suporte dos scripts do PowerShell que você implanta para usar as seguintes melhorias: 
- **Escopos de Segurança**.  Agora, os scripts usam escopos de segurança para controlar a criação e a execução de scripts. Isso é feito por meio da atribuição de marcas que representam grupos de usuários. Para obter mais informações de como usar escopos de segurança, consulte [Configurar administração baseada em funções para o System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).
- **Monitoramento em tempo real**. Agora o monitoramento da execução de um script ocorre em tempo real, à medida que o script é executado.
- **Validação de parâmetro**. Cada parâmetro no script tem uma caixa de diálogo **Propriedades do Parâmetro do Script** para adicionar validação para esse parâmetro. Depois de adicionar a validação, ao inserir um valor para o parâmetro que não esteja de acordo com a sua validação, você receberá um erro.

A implantação de scripts do PowerShell foi introduzida no Technical Preview [Tech Preview 1706](/sccm/core/get-started/capabilities-in-technical-preview-1706#create-and-run-powershell-scripts-from-the-configuration-manager-console). Os aprimoramentos adicionais foram fornecidos com o [Tech Preview 1707](/sccm/core/get-started/capabilities-in-technical-preview-1707#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) e o [Tech Preview 1708](/sccm/core/get-started/capabilities-in-technical-preview-1708#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager).


### <a name="try-it-out"></a>Experimente!

Para testar o uso do recurso Executar Scripts, consulte [Criar e executar scripts](../../apps/deploy-use/create-deploy-scripts.md).



## <a name="limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Limitar telemetria avançada do Windows 10 para enviar apenas dados relevantes para a integridade do dispositivo do Windows Analytics
<!-- 1356148 -->

Com esta versão, agora é possível definir a coleta de dados de telemetria do Windows 10 como **Avançado (Limitado)**. Essa configuração permite que você obtenha informações acionáveis sobre dispositivos em seu ambiente sem que os dispositivos reportem todos os dados no nível de telemetria **Avançado** com Windows 10 versão 1709 ou posterior.

O nível de telemetria Avançado (Limitado) inclui métricas do nível básico, bem como um subconjunto dos dados coletados do nível **Avançado** relevantes ao Windows Analytics. Para saber mais sobre os níveis de telemetria, consulte [Níveis de telemetria](https://docs.microsoft.com/windows/configuration/configure-windows-telemetry-in-your-organization#telemetry-levels).

### <a name="try-it-out"></a>Experimente!
Para configurar a coleta de telemetria do Windows 10 em clientes, confira [Como definir as configurações de cliente](/sccm/core/clients/deploy/configure-client-settings). Abra a janela **Serviços de Nuvem** e defina a telemetria do Windows 10 como **Avançado**.


## <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>O Centro de Software não distorce mais os ícones maiores do que 250 x 250  
<!-- 1356194 -->

Com esta versão, o Centro de Software não distorcerá mais os ícones maiores do que 250 x 250. O Centro de Software fazia esses ícones parecerem desfocados. Agora, você pode definir um ícone com dimensões de pixel de até 512 x 512, e ele será exibido sem distorção.

### <a name="try-it-out"></a>Experimente!
Adicione um ícone para seu aplicativo no Centro de Software. Para experimentar confira [Criar aplicativos](/sccm/apps/deploy-use/create-applications).


## <a name="check-compliance-from-software-center-for-co-managed-devices"></a>Verificar a conformidade no Centro de Software para dispositivos cogerenciados
<!-- 1356374 -->
Nesta versão, os usuários podem usar o Centro de Software para verificar a conformidade de seus dispositivos Windows 10 cogerenciados, mesmo quando o acesso condicional for gerenciado pelo Intune. Para obter detalhes, confira [Cogerenciamento para dispositivos com Windows 10](./capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices).


## <a name="support-for-exploit-guard"></a>Suporte para Exploit Guard
Essa versão adiciona suporte para o Windows Defender Exploit Guard. Você pode configurar e implantar políticas que gerenciam todos os quatro componentes do Exploit Guard. Esses componentes incluem:
-   Redução da superfície de ataque
-   Acesso controlado à pasta
-   Proteção contra explorações
-   Proteção de rede

Os dados de conformidade da implantação do Exploit Guard estão disponíveis no console do Configuration Manager.

Para saber mais sobre o Exploit Guard e componentes e regras específicas, consulte [Windows Defender Exploit Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard) na biblioteca de documentação do Windows.

### <a name="prerequisites"></a>Pré-requisitos
Os dispositivos gerenciados devem executar a Atualização para Criadores de Outono do Windows 10 1709 ou posterior e atender aos requisitos a seguir, dependendo dos componentes e das regras configuradas:

|Componente do Exploit Guard |Pré-requisitos adicionais|
|------------------------|------------------------|
| Redução da superfície de ataque  | Os dispositivos devem ter a [proteção em tempo real do Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) habilitada.  |
| Acesso controlado à pasta  | Os dispositivos devem ter a [proteção em tempo real do Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) habilitada.   |
| Proteção contra explorações  | Nenhum  |
| Proteção de rede  |  Os dispositivos devem ter a [proteção em tempo real do Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) habilitada.  |

### <a name="create-an-exploit-guard-policy----1355468---"></a>Criar uma política do Exploit Guard<!--1355468 -->
1.  No console do Configuration Manager, acesse **Ativos e conformidade** > **Endpoint Protection** e, em seguida, clique em **Windows Defender Exploit Guard**.
2.  Na guia **Início**, no grupo **Criar**, clique em **Criar Política de Exploração**.
3.  Na página **Geral** do **Assistente para Criar Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.
4.  Em seguida, selecione os componentes do Exploit Guard que você quer gerenciar com essa política. Para cada componente que você selecionar, será possível configurar detalhes adicionais.
  - **Redução da Superfície de Ataque:** configure ameaça ao Office, ameaças de script e ameaças de email que você deseja bloquear ou auditar. Você também pode excluir arquivos ou pastas específicas nessa regra.
  - **Acesso controlado à pasta:** configure a auditoria ou bloqueio e, em seguida, adicione Aplicativos que podem ignorar essa política.  Você também pode especificar outras pastas que não estão protegidas por padrão.
  - **Proteção contra explorações:** especifique um arquivo XML que contém configurações para a redução de explorações de processos do sistema e de aplicativos. Você pode exportar essas configurações do aplicativo do Central de Segurança do Windows Defender em um dispositivo com Windows 10.
  - **Proteção de rede:** configure a proteção de rede para bloquear ou auditar o acesso aos domínios suspeitos.
5.  Conclua o assistente para criar a política, que, mais tarde, você poderá implantar em dispositivos.

### <a name="deploy-an-exploit-guard-policy"></a>Implantar uma política do Exploit Guard     
Depois de criar políticas do Exploit Guard, use o assistente para Implantar Política do Exploit Guard para implantá-las. Para fazer isso, abra console do Configuration Manager, acesse **Ativos e conformidade** > **Endpoint Protection** e, em seguida, clique em **Implantar Política do Exploit Guard**.

## <a name="limited-support-for-cng-certificates"></a>Suporte limitado para certificados CNG
<!-- 1356191 -->
A partir desta versão, você pode agora usar modelos de certificado [Cryptography API: Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) para os seguintes cenários:

- O registro de cliente e a comunicação com um ponto de gerenciamento HTTPS.   
- Distribuição e o aplicativo de implantação de software com um ponto de distribuição HTTPS.   
- Implantação de sistema operacional.  
- SDK de mensagens do cliente (com a atualização mais recente) e Proxy ISV.   
- Configuração do Gateway de Gerenciamento de Nuvem.  

Para usar os certificados CNG, sua CA (autoridade de certificação) precisa fornecer modelos de certificado de CNG para computadores de destino.  Os detalhes do modelo variam de acordo com o cenário. No entanto, as propriedades a seguir são obrigatórias:

- Guia **Compatibilidade**

    - **Autoridade de Certificação** deve ser Windows Server 2008 ou posterior. (Recomendamos o Windows Server 2012.)

    - **Destinatário de certificação** deve ser Windows Vista/Server 2008 ou posterior. (Recomendamos o Windows 8/Windows Server 2012.)

- Guia **Criptografia**

    - **Categoria de Provedor** devem ser **Provedor de armazenamento de chaves**.  (Obrigatório)

Para obter os melhores resultados, recomendamos a criação do Nome da Entidade a partir de informações do Active Directory.  Use o Nome DNS para o **Formato de nome de entidade** e inclua o nome DNS no nome alternativo da entidade.  Caso contrário, será necessário fornecer essas informações quando o dispositivo for registrado no perfil do certificado.


## <a name="improved-descriptions-for-pending-computer-restarts-----1356283---"></a>Descrições aprimoradas para reinicializações pendentes do computador<!--1356283 -->
Em [Technical preview 1708](/sccm/core/get-started/capabilities-in-technical-preview-1708#restart-computers-from-the-configuration-manager-console), adicionamos a capacidade de identificar os dispositivos que estão aguardando uma reinicialização de dentro do console do Configuration Manager.

A partir dessa technical preview, o console exibe detalhes adicionais que fornecem informações sobre o processo ou a ação que está solicitando a reinicialização.

## <a name="device-guard-policy-changes----1355092---"></a>Alterações na política do Device Guard <!-- 1355092 -->
Com o build Technical Preview 1710, as três alterações a seguir foram feitas em relação às políticas do Device Guard:

### <a name="device-guard-policies-renamed-to-windows-defender-application-control-policies"></a>Políticas do Device Guard renomeadas para políticas de Controle de Aplicativo do Windows Defender
Políticas do Device Guard que foram renomeadas para políticas de Controle de Aplicativo do Windows Defender. Então, por exemplo, o **Assistente para Criar política do Device Guard** foi nomeado para **Assistente para Criar política de controle de aplicativo do Windows Defender**.

### <a name="restart-is-not-required-to-apply-policies"></a>Não é necessário reinicializar para aplicar as políticas
A partir da Atualização para Criadores de Outono do Windows versão 1709, os dispositivos que usam a nova versão do Windows não exigem uma reinicialização para aplicar as políticas de Controle de aplicativo do Windows Defender.

A reinicialização é o padrão.

#### <a name="try-it-out"></a>Experimente!  

Se você quiser desativar reinicializações, execute estas etapas:

1.  Abra o assistente para **Criar política de controle de aplicativo do Windows Defender**.
2.  Na página **Geral**, desmarque a caixa de seleção **Impor uma reinicialização de dispositivos para que essa política possa ser aplicada a todos os processos**.
3.  Clique em **Avançar** até concluir o assistente.

Em versões mais antigas do Windows, ainda aplica-se uma reinicialização automática.

### <a name="automatically-run-software-trusted-by-the-intelligent-security-graph"></a>Executar automaticamente o software de confiança do Gráfico de Segurança Inteligente

Agora, os administradores têm a opção de permitir que dispositivos bloqueados executem software confiável com uma boa reputação, conforme determinado pelo Gráfico de Segurança Inteligente da Microsoft (ISG). O ISG é composto pelo Windows Defender SmartScreen e outros serviços da Microsoft.

Os dispositivos devem estar executando o Windows Defender SmartScreen para que o software seja confiável.

#### <a name="try-it-out"></a>Experimente!  

Para permitir que um dispositivo que está executando o Windows Defender SmartScreen execute um software confiável, execute estas etapas:

1.  Abra o **assistente para Criar política de controle de aplicativo do Windows Defender**.
2.  Na página **Inclusões**, marque a caixa de seleção para **Autorizar software de confiança do Gráfico de Segurança Inteligente**.
3.  Na caixa **Arquivos ou pasta confiáveis**, adicione os arquivos e pastas que você deseja tornar confiáveis.
4.  Clique em **Avançar** até concluir o assistente.

## <a name="configure-and-deploy-windows-defender-application-guard-policies----1351960---"></a>Configurar e implantar políticas de Proteção de Aplicativos do Windows Defender <!-- 1351960 -->

O [Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) é um novo recurso do Windows que ajuda a proteger os usuários através da abertura de sites não confiáveis em um contêiner isolado seguro que não esteja acessível por outras partes do sistema operacional. Nesse visualização técnica, adicionamos suporte para configurar esse recurso usando as configurações de conformidade do Configuration Manager que você configura e, em seguida, implanta em uma coleção. Este recurso será lançado na versão prévia para a versão de 64 bits da atualização do criador do Windows 10 (codinome: RS2). Para testar esse recurso agora, você deverá estar usando uma versão prévia desta atualização.

### <a name="before-you-start"></a>Antes de começar
Para criar e implantar as políticas do Windows Defender Application Guard, os dispositivos do Windows 10 nos quais você implantará a política deverão ser configurados com uma política de isolamento de rede. Para saber mais, veja a postagem no blog mencionado posteriormente. Esse recurso só funciona com versões atuais do Windows 10 Insider. Para testá-lo, os clientes deverão estar executando uma versão recente do Windows 10 Insider.

### <a name="try-it-out"></a>Experimente!

Para entender os conceitos básicos sobre o Windows Defender Application Guard, leia [a postagem no blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97).

Para criar uma política e procurar as configurações disponíveis:
1. No console do **Configuration Manager**, escolha **Ativos e Conformidade**.
2. No espaço de trabalho **Ativos e Conformidade**, escolha **Visão Geral** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. Na guia **Início**, no grupo **Criar**, clique em **Criar Política do Windows Defender Application Guard**.
4. Usando a postagem no blog como referência, você pode procurar e definir as configurações disponíveis para experimentar o recurso.
5. Nesta versão, adicionamos a nova página Definição de Rede ao assistente. Aqui, especifique a identidade corporativa e defina o limite da rede corporativa.

    > [!NOTE]
    > Os computadores Windows 10 armazenam apenas uma lista de isolamento de rede no cliente. Nesta versão, é possível criar dois tipos diferentes de listas de isolamento de rede (uma da Proteção de Informações do Windows e outra do Windows Defender Application Guard) e implantá-las no cliente. Se você implantar as duas políticas, essas listas de isolamento de rede deverão ser correspondentes. Se você implantar listas que não correspondem ao mesmo cliente, a implantação falhará.

    É possível localizar mais informações sobre como especificar definições de rede na [documentação da Proteção de Informações do Windows](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).

6. Quando tiver terminado, conclua o assistente e implante a política para um ou mais dispositivos Windows 10.

### <a name="further-reading"></a>Leitura adicional

Para saber mais sobre o Windows Defender Application Guard, veja [esta postagem no blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Além disso, para saber mais sobre o modo autônomo do Windows Defender Application Guard, veja [esta postagem no blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).

## <a name="next-steps"></a>Próximas etapas
Para obter informações de como instalar ou atualizar o branch da technical preview, consulte [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
