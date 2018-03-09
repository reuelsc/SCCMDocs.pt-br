---
title: Technical Preview 1802 | Microsoft Docs
titleSuffix: Configuration Manager
description: "Saiba mais sobre os recursos disponíveis no Technical Preview versão 1802 do System Center Configuration Manager."
ms.custom: na
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4884a2d3-13ce-44e5-88c4-a66dc7ec6014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 162c47d867e78498650da685327c0fe296aa2eda
ms.sourcegitcommit: b1fa7be6a6fa5bb7c49e90c0e28a21ba8b41c842
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2018
---
# <a name="capabilities-in-technical-preview-1802-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1802 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo apresenta os recursos disponíveis no Technical Preview do System Center Configuration Manager, versão 1802. Você pode instalar esta versão para atualizar e adicionar novas funcionalidades ao seu site do Configuration Manager Technical Preview. 

Examine [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview) antes de instalar esta versão do technical preview. Este artigo familiariza você com os requisitos gerais e as limitações do uso de um technical preview, como atualizar entre versões e como fornecer comentários.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->
## <a name="known-issues-in-this-technical-preview"></a>Problemas conhecidos neste Technical Preview
-   **A atualização para uma versão prévia falha quando há um servidor do site no modo passivo**. Se você tiver um [servidor do site primário no modo passivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), deverá desinstalar o servidor do site no modo passivo antes de atualizar para esta nova versão de visualização. Você pode reinstalar o servidor de site no modo passivo após a conclusão da instalação pelo site.

  Para desinstalar o servidor do site no modo passivo:
  1. No console do Configuration Manager, acesse **Administração** > **Visão Geral** > **Configuração do Site** > **Servidores e Funções do Sistema de Sites** e, em seguida, selecione o servidor do site no modo passivo.
  2. No painel **Funções do Sistema de Sites**, clique com o botão direito do mouse na função **Servidor do Site** e, em seguida, escolha **Remover Função**.
  3. Clique com o botão direito no servidor do site de modo passivo e, em seguida, escolha **Excluir**.
  4. Após a desinstalação do servidor do site, no servidor do site primário ativo, reinicie o serviço **CONFIGURATION_MANAGER_UPDATE**.
<!--sms 489412-->


</br>

**Veja a seguir os novos recursos que você pode experimentar nesta versão.**  


## <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Transição da carga de trabalho do Endpoint Protection para o Intune usando o cogerenciamento    
<!-- 1357365 -->
Nesta versão, você pode agora transitar a carga de trabalho do Endpoint Protection a partir do Configuration Manager para o Intune depois de ativar o cogerenciamento. Para fazer a transição da carga de trabalho do Endpoint Protection, vá para a página de propriedades de cogerenciamento e mova a barra deslizante do Configuration Manager para **Piloto** ou **Todos**. Para obter detalhes, confira [Cogerenciamento para dispositivos com Windows 10](/sccm/core/clients/manage/co-management-overview).


 
## <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Configurar o Otimização de Entrega do Windows para usar os grupos de limites do Configuration Manager
<!-- 1324696 -->
Você usa os grupos de limites do Configuration Manager para definir e regular a distribuição de conteúdo em sua rede corporativa e para escritórios remotos. A [Otimização de Entrega do Windows](/windows/deployment/update/waas-delivery-optimization) é uma tecnologia ponto-a-ponto baseada na nuvem para compartilhar conteúdo entre dispositivos do Windows 10. A partir desta versão, configure a Otimização de Entrega para usar seus grupos de limites ao compartilhar conteúdos entre pares. Uma nova configuração de cliente aplica o identificador do grupo de limites como o identificador do grupo da Otimização de Entrega no cliente. Quando o cliente se comunica com o serviço de nuvem da Otimização de Entrega, ele usa esse identificador para localizar os pares com o conteúdo desejado. 

### <a name="prerequisites"></a>Pré-requisitos
- A Otimização de Entrega está disponível apenas em clientes do Windows 10

### <a name="try-it-out"></a>Experimente!
 Tente concluir as tarefas. Em seguida, envie **Comentários** da guia **Início** da faixa de opções, nos informando como isso funcionou.

1. No console do Configuration Manager, no espaço de trabalho **Administração**, nó **Configurações do Cliente** , crie uma política personalizada de configurações de dispositivos de cliente.
2. Selecione o novo grupo da **Otimização de Entrega**.
3. Habilite a configuração **Usar os grupos de limites do Configuration Manager para a ID do grupo da Otimização de Entrega**.

Para saber mais, confira a opção do modo de entrega **Grupo** nas [opções da Otimização de Entrega](/windows/deployment/update/waas-delivery-optimization#group-id).



## <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Sequência de tarefas de upgrade in-loco do Windows 10 por meio do gateway de gerenciamento de nuvem
<!-- 1357149 -->

A [sequência de tarefas de upgrade in-loco](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version) do Windows 10 agora oferece suporte à implantação de clientes baseados na Internet gerenciados por meio do [gateway de gerenciamento de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway). Essa habilidade permite que usuários remotos façam upgrade com mais facilidade para o Windows 10 sem precisar se conectar à rede corporativa. 

Certifique-se de que todo o conteúdo referenciado pela sequência de tarefas de upgrade in-loco seja distribuído para um [ponto de distribuição da nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point). Caso contrário, os dispositivos não podem executar a sequência da tarefas.

Ao implantar uma sequência de tarefas de upgrade, use as seguintes configurações:
- **Permitir que a sequência de tarefas seja executada para o cliente na Internet**, na guia Experiência do Usuário da implantação.
- **Baixar todo o conteúdo localmente antes de iniciar a sequência de tarefas**, na guia Pontos de Distribuição da implantação. Outras opções, como **Baixar conteúdo localmente quando necessário, executando a sequência de tarefas**, não funcionam neste cenário. O mecanismo de sequência de tarefas atualmente não consegue obter conteúdo de um ponto de distribuição da nuvem. O cliente do Configuration Manager deve baixar o conteúdo a partir do ponto de distribuição da nuvem antes de iniciar a sequência de tarefas.
- (*Opcional*) **Conteúdo pré-baixado para esta sequência de tarefas**, na guia Geral da implantação. Para saber mais, confira [Configurar o conteúdo de armazenamento prévio em cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Melhorias na sequência de tarefas de upgrade in-loco do Windows 10
<!-- 1357425 -->
O modelo de sequência de tarefas padrão para o upgrade in-loco do Windows 10 agora inclui grupos adicionais com ações recomendadas para adicionar antes e depois do processo de upgrade. Essas ações são comuns entre muitos clientes que atualizam com sucesso os dispositivos para o Windows 10. 

### <a name="new-groups-under-prepare-for-upgrade"></a>Novos grupos em **Preparar para o Upgrade**
- **Verificações da bateria**: adicione etapas neste grupo para verificar se o computador está usando bateria ou energia com fio. Esta ação requer um script personalizado ou um utilitário para executar esta verificação.
- **Verificações de rede/conexão com fio**: adicione etapas neste grupo para verificar se o computador está conectado a uma rede e não está usando uma conexão sem fio. Esta ação requer um script personalizado ou um utilitário para executar esta verificação.
- **Remover aplicativos incompatíveis**: adicione etapas neste grupo para remover quaisquer aplicativos incompatíveis com esta versão do Windows 10. O método para desinstalar um aplicativo varia. Se o aplicativo usar o Windows Installer, copie a linha de comando **Desinstalar programa** da guia **Programas** nas propriedades do tipo de implantação do Windows Installer do aplicativo. Em seguida, adicione uma etapa **Executar linha de comando** neste grupo com a linha de comando Desinstalar programa. Por exemplo: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **Remover drivers incompatíveis**: adicione etapas neste grupo para remover os drivers que são incompatíveis com esta versão do Windows 10.
- **Remover/suspender segurança de terceiros**: adicione etapas neste grupo para remover ou suspender programas de segurança de terceiros, como antivírus.
   - Se você estiver usando um programa de criptografia de disco de terceiros, forneça seu driver de criptografia à Instalação do Windows com a [opção de linha de comando](/windows-hardware/manufacture/desktop/windows-setup-command-line-options) **/ReflectDrivers**. Adicione uma etapa [Definir variável de sequência de tarefas](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) para a sequência de tarefas neste grupo. Defina a variável de sequência de tarefas como **OSDSetupAdditionalUpgradeOptions**. Defina o valor para **/ReflectDriver** com o caminho para o driver. Esta [variável de ação de sequências de tarefas](/sccm/osd/understand/task-sequence-action-variables#upgrade-operating-system) anexa a linha de comando da Instalação do Windows usada pela sequência de tarefas. Entre em contato com o fornecedor do software para obter qualquer orientação adicional sobre este processo.

### <a name="new-groups-under-post-processing"></a>Novos grupos em **Pós-processamento**
- **Aplicar drivers baseados em instalação**: adicione etapas neste grupo para instalar drivers baseados em instalação (.exe) de pacotes.
- **Instalar/habilitar a segurança de terceiros**: adicione etapas neste grupo para instalar ou habilitar programas de segurança de terceiros, como antivírus. 
- **Definir aplicativos e associações padrão do Windows**: adicione etapas neste grupo para definir aplicativos e associações de arquivos padrão do Windows. Primeiro prepare um computador de referência com suas associações de aplicativos desejadas. Em seguida, execute a seguinte linha de comando para exportar: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Adicione o arquivo XML a um pacote. Em seguida, adicione uma etapa [Executar linha de comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) neste grupo. Especifique o pacote que contém o arquivo XML e, em seguida, especifique a seguinte linha de comando: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Para saber mais, confira [Exportar ou importar associações de aplicativos padrão](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).
- **Aplicar personalizações**: adicione etapas a este grupo para aplicar as personalizações do menu Iniciar, como a organização de grupos de programas. Para saber mais, confira [Personalizar a Tela Inicial](/windows-hardware/manufacture/desktop/customize-the-start-screen).

### <a name="additional-recommendations"></a>Recomendações adicionais
- Examine a documentação do Windows para [Resolver erros de upgrade do Windows 10](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Este artigo também inclui informações detalhadas sobre o processo de upgrade.
- Na etapa padrão **Verificar a prontidão**, ative  **Verificar o espaço mínimo em disco (MB)**. Defina o valor para pelo menos **16384** (16 GB) para um pacote de upgrade do SO de 32 bits ou **20480** (20 GB) de 64 bits. 
- Use a [variável de sequência de tarefas interna](/sccm/osd/understand/task-sequence-built-in-variables) **SMSTSDownloadRetryCount** para repetir a política de download. Atualmente, por padrão, o cliente tenta novamente duas vezes; essa variável é definida como dois (2). Se seus clientes não estiverem conectados a uma conexão de rede corporativa com fio, tentativas adicionais ajudam o cliente a obter uma política. Usar esta variável não causa nenhum efeito colateral negativo, além de uma falha em atraso caso a política não possa ser baixada.<!-- 501016 --> Além disso, aumente a variável **SMSTSDownloadRetryDelay** dos 15 segundos padrão.
- Execute uma avaliação de compatibilidade em linha. 
   - Adicione uma segunda etapa **Atualizar sistema operacional** no início do grupo **Preparar para Upgrade**. Chame-o de *Avaliação de upgrade*. Especifique o mesmo pacote de upgrade e, em seguida, ative a opção para **Executar verificação de compatibilidade da Instalação do Windows sem iniciar o upgrade**. Habilite **Continuar em caso de erro** na guia Opções. 
   - Imediatamente após esta etapa *Avaliação do upgrade*, adicione uma etapa **Executar linha de comando**. Especifique a seguinte linha de comando:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>Na guia **Opções**, adicione as seguintes condições: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Este código de retorno é o equivalente decimal de MOSETUP_E_COMPAT_SCANONLY (0xC1900210), que é uma verificação de compatibilidade bem-sucedida sem problemas. Se a etapa *Avaliação do upgrade* for bem-sucedida e retornar esse código, esta etapa será ignorada. Caso contrário, se a etapa de avaliação retornar qualquer outro código de retorno, esta etapa falha na sequência de tarefas com o código de retorno da verificação de compatibilidade da Instalação do Windows.
   - Para saber mais, confira [Upgrade do sistema operacional](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS).
- Se você quiser mudar o dispositivo do BIOS para UEFI durante esta sequência de tarefas, veja [Converter de BIOS para UEFI durante um upgrade in-loco](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

Envie **Comentários** desde a aba **Página inicial** da faixa de opções se você tiver mais recomendações ou sugestões.



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Melhorias em pontos de distribuição habilitados para PXE
<!-- 1357580 -->
Para esclarecer o comportamento da [nova funcionalidade PXE](/sccm/core/get-started/capabilities-in-technical-preview-1706#pxe-network-boot-support-for-ipv6) introduzida pela primeira vez na versão de Technical Preview 1706, nós renomeamos a opção **Suporte IPv6**. Na guia **PXE** das propriedades do ponto de distribuição, verifique **Habilitar um respondente PXE sem o Serviço de Implantação do Windows**. 

Esta opção habilita um respondente PXE no ponto de distribuição, que não requer o Serviço de Implantação do Windows (WDS - Windows Deployment Services). Se você habilitar esta nova opção em um ponto de distribuição já habilitado para PXE, o Configuration Manager suspende o serviço WDS. Se você desativar esta nova opção, mas ainda **Ativar o suporte PXE para os clientes** , então o ponto de distribuição habilita o WDS novamente.

Como o WDS não é necessário, o ponto de distribuição habilitado para PXE pode ser um sistema operacional de cliente ou servidor, incluindo o Windows Server Core. Este novo serviço de respondente PXE continua a dar suporte ao IPv6 e também aumenta a flexibilidade dos pontos de distribuição habilitados para PXE em escritórios remotos.

> [!NOTE]
> Este serviço usa a mesma tecnologia fundamental que o [serviço de respondente PXE baseado no cliente](/sccm/core/get-started/capabilities-in-technical-preview-1712#client-based-pxe-responder-service) na versão de Technical Preview 1712. Esse recurso não requer a sobrecarga da função do ponto de distribuição.

### <a name="multicast"></a>Multicast
Para habilitar e configurar o multicast na guia **Multicast** das propriedades do ponto de distribuição, o ponto de distribuição deve usar o WDS. 
- Se você **Habilitar suporte a PXE para clientes**  e **Habilitar multicast para enviar dados a vários clientes simultaneamente**, então você não pode **Habilitar um respondente PXE sem o Serviço de Implantação do Windows**.
- Se você **Habilitar suporte a PXE para clientes** e **Habilitar um respondente PXE sem o Serviço de Implantação do Windows**, então você não pode **Habilitar multicast para enviar dados a vários clientes simultaneamente**



## <a name="deployment-templates-for-task-sequences"></a>Modelos de implantação para sequências de tarefas
<!-- 1357391 -->
O assistente de implantação para sequências de tarefas agora pode criar um modelo de implantação. O modelo de implantação pode ser salvo e aplicado a uma sequência de tarefas existente ou nova para criar uma implantação. 

### <a name="try-it-out"></a>Experimente!  
Tente concluir as tarefas. Em seguida, envie **Comentários** da guia **Início** da faixa de opções, nos informando como isso funcionou. 

 **Criar um modelo de implantação para uma nova implantação de sequência de tarefas** <br/> 
1. No espaço de trabalho **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Sequências de Tarefas**.
2. Clique com o botão direito do mouse em uma sequência de tarefas e selecione **Implantar**. 
3. Na guia **Geral**, observe que agora existe uma opção para **Selecionar modelo de implantação**. 
4. Continue por meio do **Assistente de implantação de software** selecionando as configurações de implantação para a sequência de tarefas. 
5. Quando você alcança a guia **Resumo** do **Assistente de implantação de software**, clique em **Salvar como modelo**.
6. Dê ao modelo um nome e selecione as configurações para salvar no modelo. 
7. Clique em **Salvar**. O modelo agora está disponível para uso na opção **Selecionar modelo de implantação**.



## <a name="product-lifecycle-dashboard"></a>Painel do Ciclo de Vida do Produto
<!--1319632-->
O novo [Painel do Ciclo de Vida do Produto](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard) mostra o estado da política do Ciclo de Vida do Produto Microsoft para produtos Microsoft instalados em dispositivos gerenciados com o Configuration Manager. O painel fornece informações sobre produtos da Microsoft em seu ambiente, estado de capacidade de suporte e datas de término do suporte. Você pode usar o painel para entender a disponibilidade de suporte para cada produto. 

Para acessar o Painel do Ciclo de Vida, no console do Configuration Manager, vá para **Ativos e conformidade** >**Asset Intelligence** >**Ciclo de vida do produto**



## <a name="improvements-to-reporting"></a>Melhorias em relatórios
<!--1357653-->
Como resultado de [seu feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/32434147-new-builtin-reports-about-windows-10-versions-and), adicionamos um novo relatório, **Detalhes de manutenção do Windows 10 para uma coleção específica**. Este relatório mostra a ID do recurso, o nome do NetBIOS, o nome do SO, o nome da versão do SO, a compilação, o branch do SO e o estado de manutenção para dispositivos do Windows 10. Para acessar o relatório, vá para **Monitoramento** >**Geração de relatórios** >**Relatório**  >**Sistemas operacionais** >**Detalhes de manutenção do Windows 10 para uma coleção específica**.



## <a name="improvements-to-software-center"></a>Melhorias ao Centro de Software
<!--1357592-->
Como resultado de [seu feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/13002684-software-center-show-only-available-software-hid), os aplicativos instalados agora podem ser ocultados no Centro de Software. Os aplicativos que já estão instalados não serão mais exibidos na guia Aplicativos quando esta opção estiver habilitada. 

### <a name="try-it-out"></a>Experimente!
Habilite a configuração **Ocultar aplicativos instalados no Centro de Software** nas configurações do cliente do Centro de Software. Observe o comportamento no Centro de Software quando o usuário final instalar um aplicativo.



## <a name="improvements-to-run-scripts"></a>Melhorias ao recurso Executar Scripts
<!--1236459-->
A função [Executar script](/sccm/apps/deploy-use/create-deploy-scripts) agora retorna a saída de script usando a formatação JSON. Este formato retorna consistentemente uma saída de script legível. Os scripts que falham ao executar podem não obter uma saída retornada. 



## <a name="boundary-group-fallback-for-management-points"></a>Fallback de grupo de limites para pontos de gerenciamento
<!-- 1324594 -->
A partir desta versão, você pode configurar relações de fallback para pontos de gerenciamento entre [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups). Esse comportamento proporciona maior controle para os pontos de gerenciamento que os clientes usam. Na guia **Relações** das propriedades do grupo de limites, existe uma nova coluna para o ponto de gerenciamento. Quando você adiciona um novo grupo de limites de fallback, o tempo de fallback para o ponto de gerenciamento é sempre zero (0). Esse comportamento é o mesmo para o **Comportamento padrão** no grupo de limites padrão do site.

Anteriormente, um problema comum ocorre quando você possui um ponto de gerenciamento protegido em uma rede segura. Os clientes da rede corporativa principal recebem políticas que incluem esse ponto de gerenciamento protegido, mesmo que não possam se comunicar com ele em um firewall. Para solucionar esse problema, use a opção **Nunca realizar fallback** para garantir que os clientes apenas retornem aos pontos de gerenciamento com os quais eles podem se comunicar.

Ao fazer upgrade do site para esta versão, o Configuration Manager adiciona todos os pontos de gerenciamento que não são direcionados para a Internet no grupo de limites padrão do site. Esse comportamento de upgrade garante que as versões mais antigas do cliente continuem a se comunicar com pontos de gerenciamento. Para aproveitar ao máximo esse recurso, mova seus pontos de gerenciamento para os grupos de limites desejados.

O fallback dos grupos de limites do ponto de gerenciamento não altera o comportamento durante a instalação do cliente (ccmsetup). Se a linha de comando não especificar o ponto de gerenciamento inicial usando o parâmetro /MP, o novo cliente recebe a lista completa de pontos de gerenciamento disponíveis. Para o processo inicial de inicialização, o cliente usa o primeiro ponto de gerenciamento que ele pode acessar. Uma vez que o cliente estiver registrado no site, ele recebe a lista de pontos de gerenciamento ordenada corretamente com esse novo comportamento. 

### <a name="prerequisites"></a>Pré-requisitos
- Habilitar os [pontos de gerenciamento preferenciais](/sccm/core/servers/deploy/configure/boundary-groups#preferred-management-points). No console do Configuration Manager, acesse o espaço de trabalho **Administração**. Expanda a **Configuração do site** e selecione **Sites**. Clique em **Configurações da hierarquia**  na faixa de opções. Na guia **Geral**, habilite **Os clientes preferem usar os pontos de gerenciamento especificados em grupos de limite**. 

### <a name="known-issues"></a>Problemas conhecidos
- Os processos de implantação de sistema operacional não estão conscientes dos grupos de limites.

### <a name="troubleshooting"></a>Solução de problemas
Novas entradas aparecem no **LocationServices.log**. O atributo **Localidade** identifica um dos seguintes estados:
- 0: Desconhecido
- 1: O ponto de gerenciamento especificado está apenas no grupo de limites padrão do site para o fallback
- 2: O ponto de gerenciamento especificado está em um grupo de limites remoto ou vizinho. Quando o ponto de gerenciamento está em um grupo vizinho ou em grupos de limites padrão do site, a localidade é 2.
- 3: O ponto de gerenciamento especificado está no grupo de limites local ou atual. Quando o ponto de gerenciamento está no grupo de limites atual, bem como em um grupo vizinho ou em um grupo de limites padrão do site, a localidade é 3. Se você não habilitar a configuração de pontos de gerenciamento preferenciais nas Configurações de Hierarquia, a localidade será sempre 3, independentemente do grupo de limites em que o ponto de gerenciamento esteja.

Os clientes usam os pontos de gerenciamento local primeiro (localidade 3), em seguida os remotos (localidade 2) e depois os fallbacks (localidade 1). 

Quando um cliente recebe cinco erros em dez minutos e não se comunica com um ponto de gerenciamento em seu grupo de limites atual, esse grupo tenta entrar em contato com um ponto de gerenciamento em um grupo vizinho ou em um grupo de limites padrão do site. Se o ponto de gerenciamento no atual grupo de limites voltar a ficar online mais tarde, o cliente retornará ao ponto de gerenciamento local no próximo ciclo de atualização. O ciclo de atualização é de 24 horas, ou quando o serviço do agente do Configuration Manager é reiniciado.



## <a name="improved-support-for-cng-certificates"></a>Suporte aprimorado para certificados CNG
<!-- 1357314 -->
O Configuration Manager (branch atual) versão 1710 Dá suporte a [Criptografia: certificados de próxima geração (CNG)](/sccm/core/plan-design/network/cng-certificates-overview). A versão 1710 limita o suporte a certificados de clientes em vários cenários. 

A partir desta versão de visualização técnica, use certificados de CNG para as seguintes funções de servidor habilitadas para HTTPS:
- Ponto de gerenciamento
- Ponto de distribuição
- Ponto de atualização de software

A lista de [cenários sem suporte](/sccm/core/plan-design/network/cng-certificates-overview#unsupported-scenarios) permanece a mesma.



## <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Suporte para gateway de gerenciamento de nuvem para o Azure Resource Manager
<!-- 1324735 -->
Ao criar uma instância do [gateway de gerenciamento de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway) (CMG), o assistente agora oferece a opção de criar uma **implantação do Azure Resource Manager**. O [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) é uma plataforma moderna para gerenciar todos os recursos da solução como uma única entidade, chamado [grupo de recursos](/azure/azure-resource-manager/resource-group-overview#resource-groups). Ao implantar o CMG com o Azure Resource Manager, o site usa o Azure Active Directory (Azure AD) para autenticar e criar os recursos necessários para a nuvem. Esta implantação modernizada não requer o certificado de gerenciamento do Azure clássico.  

O assistente do CMG ainda fornece a opção para uma **implantação de serviço clássico** usando um certificado de gerenciamento do Azure. Para simplificar a implantação e o gerenciamento de recursos, recomendamos usar o modelo de implantação do Azure Resource Manager para todas as novas instâncias do CMG. Se possível, reimplante as instâncias CMG existentes por meio do Resource Manager.

O Configuration Manager não migra as instâncias do CMG clássicas existentes para o modelo de implantação do Azure Resource Manager. Crie novas instâncias do CMG usando as implantações do Azure Resource Manager e, em seguida, remova instâncias clássicas do CMG. 

> [!IMPORTANT]
> Esse recurso não habilita o suporte para o Provedor de Serviços de Nuvem (CSP) do Azure. A implantação do CMG com o Azure Resource Manager continua a usar o serviço de nuvem clássico, ao qual o CSP não oferece suporte. Para saber mais, confira os [serviços do Azure disponíveis no CSP do Azure](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="prerequisites"></a>Pré-requisitos
- Integração com o [Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure). A descoberta do usuário do Azure AD não é necessária.
- Os mesmos [requisitos para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway#requirements-for-cloud-management-gateway), com exceção do certificado de gerenciamento do Azure.

### <a name="try-it-out"></a>Experimente!  
 Tente concluir as tarefas. Em seguida, envie **Comentários** da guia **Início** da faixa de opções, nos informando como isso funcionou.

1. No console do Configuration Manager, espaço de trabalho **Administração**, expanda os **Serviços de nuvem** e selecione o **Gateway de gerenciamento de nuvem**. Clique em **Criar gateway de gerenciamento de nuvem** na faixa de opções. 
2. Na página **Geral**, selecione **implantação do Azure Resource Manager** . Clique em **Entrar** para autenticar com uma conta de administrador de assinatura do Azure. O assistente automatiza os campos restantes das informações de assinatura do Azure AD armazenadas durante o pré-requisito de integração. Se você possui várias assinaturas, selecione a assinatura desejada para usar. Clique em **Avançar**.  
3. Na página **Configurações**, forneça o arquivo de certificado do servidor PKI como de costume. Este certificado define o nome do serviço CMG no Azure. Selecione a **Região** e, em seguida, selecione uma opção de grupo de recursos para **Criar novo** ou **Usar o existente**. Insira o novo nome do grupo de recursos ou selecione um grupo de recursos existente na lista suspensa. 
4. Conclua o assistente.

> [!NOTE] 
> Para o aplicativo de servidor do AD Azure selecionado, o Azure atribui a permissão **colaborador** de assinatura. 

Monitore o progresso da implantação do serviço com o **cloudmgr.log** no ponto de conexão do serviço.



## <a name="approve-application-requests-for-users-per-device"></a>Aprovar pedidos de aplicativos para usuários por dispositivo
<!-- 1357015 -->
Começando nesta versão, quando um usuário solicita um aplicativo que requer aprovação, o nome específico do dispositivo agora é parte da solicitação. Se o administrador aprova o pedido, o usuário só poderá instalar o aplicativo nesse dispositivo. O usuário deve enviar outro pedido para instalar o aplicativo em outro dispositivo. 

> [!NOTE]
> Esse recurso é opcional. Ao atualizar para esta versão, ative esse recurso no assistente de atualização. Alternativamente, habilite o recurso no console mais tarde. Para obter mais informações, consulte [Enable optional features from updates (Habilitar recursos opcionais de atualizações)](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).

### <a name="prerequisites"></a>Pré-requisitos
- Atualize o cliente do Configuration Manager para a versão mais recente
- Habilite a configuração do cliente **Usar o novo Centro de Software** no grupo [Agente de computador](/sccm/core/clients/deploy/about-client-settings#computer-agent)

### <a name="try-it-out"></a>Experimente!
 Tente concluir as tarefas. Em seguida, envie **Comentários** da guia **Início** da faixa de opções, nos informando como isso funcionou.

1. Implantar um aplicativo como disponível para uma coleção de usuários.
2. Na página **Configuração de implantação**, habilite a opção: **Um administrador deve aprovar uma solicitação para este aplicativo no dispositivo**.
3. Como usuário direcionado, use o Centro de Software para enviar uma solicitação para o aplicativo. 
4. Exiba **Solicitações de aprovação**, no **Gerenciamento de aplicativos**, no espaço de trabalho **Biblioteca de software** do console do Configuration Manager. Agora há uma coluna **Dispositivo** na lista para cada solicitação. Quando você toma ação no pedido, a caixa de diálogo Solicitação de Aplicativo também inclui o nome do dispositivo do qual o usuário enviou a solicitação.



## <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Use o Centro de Software para navegar e instalar aplicativos disponíveis para usuários em dispositivos ingressados no Azure AD
<!-- 1322613 -->
Se você implantar aplicativos como disponíveis para usuários, eles agora podem navegar e instalá-los por meio do Centro de Software nos dispositivos Azure Active Directory (Azure AD).  

### <a name="prerequisites"></a>Pré-requisitos
- Habilitar o HTTPS no ponto de gerenciamento
- Integrar o site com o [Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure)
- Implantar um aplicativo como disponível para uma coleção de usuários
- Distribuir qualquer conteúdo do aplicativo para um [ponto de distribuição na nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)
- Habilite a configuração do cliente **Usar o novo Centro de Software** no grupo [Agente de computador](/sccm/core/clients/deploy/about-client-settings#computer-agent)
- O cliente deve ser: 
   - Windows 10
   - Ingressado no Azure AD, também conhecido como ingressado no domínio de nuvem
- Para dar suporte a clientes baseados na Internet:
    - [Gateway de gerenciamento de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway) 
    - Habilite a configuração do cliente: **Habilitar solicitações da política de usuário de clientes da Internet** no grupo [Política do Cliente](/sccm/core/clients/deploy/about-client-settings#client-policy)
- Para oferecer suporte a clientes na rede corporativa:
    - Adicione o ponto de distribuição da nuvem a um grupo de limites usado pelos clientes
    - Os clientes devem ser capazes de resolver o nome de domínio totalmente qualificado (FQDN) do ponto de gerenciamento habilitado para HTTPS



## <a name="report-on-windows-autopilot-device-information"></a>Relatório sobre as informações do dispositivo do Windows AutoPilot
<!-- 1351442 -->
O Windows AutoPilot é uma solução para integração e configuração de novos dispositivos do Windows 10 de forma moderna. Para saber mais, confira uma [visão geral do Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). Um método de registro de dispositivos existentes com o Windows AutoPilot é fazer o upload de informações do dispositivo para a Microsoft Store para Empresas e Educação. Esta informação inclui o número de série do dispositivo, o identificador de produto do Windows e um identificador de hardware. Use o Configuration Manager para coletar e reportar as informações deste dispositivo. 

### <a name="prerequisites"></a>Pré-requisitos
- Esta informação do dispositivo aplica-se apenas a clientes no Windows 10, versão 1703 e posterior

### <a name="try-it-out"></a>Experimente!
 Tente concluir as tarefas. Em seguida, envie **Comentários** da guia **Início** da faixa de opções, nos informando como isso funcionou.

1. No console do Configuration Manager, espaço de trabalho **Monitoramento**, expanda o nó **Geração de relatórios**, expanda **Relatórios** e selecione o nó **Hardware - Geral**.
2. Execute o novo relatório, **Informações do dispositivo do Windows AutoPilot** e veja os resultados. 
3. No visor do relatório, clique no ícone **Exportar** e selecione a opção **CSV (delimitado por vírgulas)**.
4. Depois de salvar o arquivo, faça o upload dos dados para a Microsoft Store para Empresas e Educação. Para saber mais, confira [adicionar dispositivos na Microsoft Store para Empresas e Educação](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile). 



## <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Melhorias nas Políticas do Configuration Manager para o Windows Defender Exploit Guard
<!-- 1356220 -->
As configurações de políticas adicionais para os componentes Redução da superfície de ataque e Acesso controlado a pastas foram adicionadas no Configuration Manager para [Windows Defender Exploit Guard](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard).

**Novas configurações para acesso controlado à pasta**<br/>
Existem duas opções adicionais quando você configura o acesso controlado à pasta: **Bloquear apenas os setores de disco** e **Auditar apenas os setores de disco**. Essas duas configurações permitem que o acesso controlado à pasta seja ativado apenas para setores de inicialização e não habilita a proteção de pastas específicas ou de pastas protegidas padrão. 

**Novas configurações para a redução da superfície de ataque**
- Use a proteção avançada contra o ransomware.
- Bloqueie o roubo de credenciais do subsistema de autoridade de segurança local do Windows. 
- Bloqueie a execução de arquivos executáveis, a menos que eles atendam a uma prevalência, idade ou critérios de lista confiável. 
- Bloqueie processos não confiáveis e não assinados que sejam executados de USB.



## <a name="microsoft-edge-browser-policies"></a>Políticas do navegador Microsoft Edge
<!-- 1357310 -->
Para os clientes que utilizam o navegador web [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) nos clientes do Windows 10, agora você pode criar uma política de configurações de conformidade do Configuration Manager para configurar várias configurações do Microsoft Edge. Esta política atualmente inclui as seguintes configurações:
- **Definir o navegador Microsoft Edge como padrão** : configura a configuração do aplicativo padrão do Windows 10 para o navegador da Web para o Microsoft Edge
- **Permitir o menu suspenso na barra de endereços**: requer o Windows 10, versão 1703 ou posterior. Para saber mais, confira a [política de navegador AllowAddressBarDropdown ](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Permitir sincronizar favoritos entre navegadores da Microsoft** : requer o Windows 10, versão 1703 ou posterior. Para saber mais, confira a [política de navegador SyncFavoritesBetweenIEAndMicrosoftEdge](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Permitir limpar dados de navegação na saída**: requer o Windows 10, versão 1703 ou posterior. Para saber mais, confira a [política do navegador ClearBrowsingDataOnExit](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Permitir não rastrear cabeçalhos**: para obter mais informações, confira a [política do navegador AllowDoNotTrack](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Permitir preenchimento automático**: para obter mais informações, confira a [ política do navegador AllowAutofill](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Permitir cookies**: para obter mais informações, confira a [política do navegador AllowCookies](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).
- **Permitir o bloqueador de pop-up**: para obter mais informações, confira a [política do navegador AllowPopups](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Permitir sugestões de pesquisa na barra de endereços**: Para saber mais, confira a [política do navegador AllowSearchSuggestionsinAddressBar](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Permitir enviar o tráfego de Intranet para o Internet Explorer** : para obter mais informações, confira a [política do navegador SendIntranetTraffictoInternetExplorer](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Permitir o gerenciador de senhas**: para obter mais informações, confira a [política do navegador AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Permitir Ferramentas para desenvolvedores**: Para saber mais, confira a [política do navegador AllowDeveloperTools](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Permitir extensões**: para obter mais informações, confira a [política de navegador AllowExtensions](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).

### <a name="prerequisites"></a>Pré-requisitos
- Cliente do Windows 10 que está ingressado no Azure Active Directory. 

### <a name="known-issues"></a>Problemas conhecidos
- Os dispositivos ingressados no domínio local não podem aplicar esta política nesta versão. Esta questão também diz respeito a dispositivos ingressados no domínio híbrido.

### <a name="try-it-out"></a>Experimente!  
 Tente concluir as tarefas. Em seguida, envie **Comentários** da guia **Início** da faixa de opções, nos informando como isso funcionou.

**Criar a política**
1. No console do Configuration Manager, vá até o espaço de trabalho **Ativos e conformidade**. Expanda as **Configurações de conformidade** e selecione o novo nó **Perfis de navegador do Microsoft Edge**. Clique na opção da faixa de opções para **Criar a política do navegador do Microsoft Edge**.
2. Especifique um **Nome** para a política, digite opcionalmente a **Descrição** e clique em **Avançar**.
3. Na página **Configurações**, altere o valor para **Configurado** para que as configurações sejam incluídas nesta política e clique em **Avançar**.
4. Na página **Plataformas com suporte**, selecione as versões e arquiteturas do sistema operacional às quais esta política se aplica e clique em **Avançar**. 
5. Conclua o assistente.

**Implantar a política**
1. Selecione sua política e clique na opção da faixa de opções para **Implantar**.
2. Clique em **Procurar** para selecionar a coleção de usuário ou dispositivo para a qual implantar a política. 
3. Selecione as opções adicionais conforme necessário. Gerar alertas quando a política não for compatível. Defina o agendamento pelo qual o cliente avalia a conformidade do dispositivo com esta política.
4. Clique em **OK** para criar a implantação.

Como qualquer política de configurações de conformidade, o cliente soluciona as configurações no agendamento especificado. [Monitore e relate a conformidade do dispositivo](/sccm/compliance/deploy-use/monitor-compliance-settings) no console do Configuration Manager.



## <a name="report-for-default-browser-counts"></a>Relatório para as contagens padrão do navegador
<!-- 1357830 -->
Agora, há um novo relatório para mostrar a contagem de clientes com um navegador web específico como o padrão do Windows. 

### <a name="known-issues"></a>Problemas conhecidos
- Quando você abre o relatório pela primeira vez, ele só mostra a contagem e não o BrowserProgID. Para contornar esse problema, edite a consulta para o relatório para a seguinte sintaxe:  
    `select BrowserProgId00 as BrowserProgId, Count(*) as Count`  
    `from DEFAULT_BROWSER_DATA as dbd`  
    `group by BrowserProgId00`

### <a name="try-it-out"></a>Experimente!  
 Tente concluir as tarefas. Em seguida, envie **Comentários** da guia **Início** da faixa de opções, nos informando como isso funcionou.
1. No console **Configuration Manager**, espaço de trabalho **Monitoramento**, expanda a **Geração de relatórios**, expanda **Relatórios**, selecione **Software - Empresas e Produtos**.
2. Execute o relatório **Contagens do navegador padrão**.

Use a seguinte referência para BrowserProgIDs comuns:
- **AppXq0fevzme2pys62n3e0fbqa7peapykr8v**: Microsoft Edge
- **IE.HTTP**: Microsoft Internet Explorer
- **ChromeHTML**: Google Chrome
- **OperaStable**: software Opera
- **FirefoxURL-308046B0AF4A39CB**: Mozilla Firefox



## <a name="support-for-windows-10-arm64-devices"></a>Suporte para dispositivos Windows 10 ARM64
<!-- 1353704 -->
A partir desta versão, o cliente do Configuration Manager tem suporte nos dispositivos ARM64 do Windows 10. Os recursos existentes de gerenciamento de clientes devem funcionar com esses novos dispositivos. Por exemplo, inventário de hardware e software, atualizações de software e gerenciamento de aplicativos. A implantação de sistema operacional atualmente não tem suporte. 

## <a name="changes-to-phased-deployments"></a>Mudanças nas implantações em fases
<!-- 1357405 -->
As implantações em fases automatizam uma distribuição coordenada e sequenciada do software em várias coleções. Nesta versão de Technical Preview, o assistente de implantação em fases pode ser concluído para sequências de tarefas no console do administrador. Implantações também são criadas. No entanto, a segunda fase não começa automaticamente depois de satisfazer os critérios de sucesso da primeira fase. A segunda fase pode ser iniciada manualmente com uma declaração SQL.   

### <a name="try-it-out"></a>Experimente!  
  Tente concluir as tarefas. Em seguida, envie **Comentários** da guia **Início** da faixa de opções, nos informando como isso funcionou.
 
**Criar uma implantação em fases para uma sequência de tarefas** </br>
1. No espaço de trabalho **Biblioteca de Software**, expanda **Sistemas Operacionais** e selecione **Sequências de Tarefas**.
2. Clique com o botão direito do mouse em uma sequência de tarefas existente e selecione **Criar Implantação em Fases**. 
3. Na guia **Geral**, nomeie a implantação em fases e lhe dê uma descrição (opcional), em seguida, selecione **Criar automaticamente uma implantação de duas fases padrão**. 
4. Preencha os campos **Primeira coleção** e **Segunda coleção**. Selecione **Avançar**.
5. Na guia **Configurações**, escolha uma opção para cada uma das configurações de agendamento e selecione **Próximo** quando concluir. 
6. Na guia **Fases**, edite qualquer uma das fases se necessário e clique em **Próximo**.
7. Confirme suas seleções na guia **Resumo** e clique em **Próximo** para continuar.
8. Quando os critérios de sucesso para a primeira fase forem alcançados, siga as instruções para iniciar a segunda fase com uma declaração SQL.
 
**Inicie a segunda fase com uma declaração SQL**
1. Identifique o PhasedDeploymentID para a implantação que você criou com a seguinte consulta SQL:<br/> `Select * from PhasedDeployment`
2. Execute a seguinte declaração para iniciar a fase de produção:<br/> `UPDATE PhasedDeployment SET EvaluatePhasedDeployment = 1, Action = 3 WHERE PhasedDeploymentID = <Phased Deployment ID>`


## <a name="next-steps"></a>Próximas etapas
Para obter informações de como instalar ou atualizar o branch da technical preview, consulte [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
