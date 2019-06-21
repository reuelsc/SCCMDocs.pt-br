---
title: Nova versão 1802
titleSuffix: Configuration Manager
description: Obtenha os detalhes sobre as alterações e as novas funcionalidades introduzidas na versão 1802 do Configuration Manager.
ms.date: 04/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5bd637b1-d7a1-411b-877a-c7aae9741173
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9d35558da6b25bba16b84c931b0254436ac3dd1e
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67285541"
---
# <a name="whats-new-in-version-1802-of-system-center-configuration-manager"></a>Novidades da versão 1802 do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Branch Atual)*

A atualização do 1802 para o branch atual do Configuration Manager está disponível como uma atualização no console. Aplique essa atualização em sites que executam a versão 1702, 1706 ou 1710. <!-- baseline only statement: -->Ao instalar um novo site, ela também está disponível como uma versão de linha de base.

Além de novos recursos, este lançamento inclui outras alterações, como correções de bugs. Para saber mais, veja [Resumo das alterações no Branch Atual do System Center Configuration Manager, versão 1802](https://support.microsoft.com/help/4101375).

As atualizações adicionais a seguir também já estão disponíveis neste lançamento:
- [Pacote cumulativo de atualizações para o branch atual do System Center Configuration Manager, versão 1802](https://support.microsoft.com/help/4163547)

> [!TIP]  
> Para instalar um novo site, você deve usar uma versão de linha de base do Configuration Manager.  
>
>  Saiba mais sobre:    
>   - [Instalação de novos sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Instalação de atualizações em sites](/sccm/core/servers/manage/updates)  
>   - [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#bkmk_Baselines)

As seções a seguir fornecem detalhes sobre as alterações e as novas funcionalidades introduzidas na versão 1802 do Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1802 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infraestrutura do site

### <a name="reassign-distribution-point"></a>Reatribuir ponto de distribuição
<!-- 1306937 -->
Muitos clientes têm grande infraestruturas do Configuration Manager e estão reduzindo sites primários ou secundários para simplificar os ambientes deles. Eles ainda precisam manter os pontos de distribuição de localizações de filiais para fornecer conteúdo para clientes gerenciados. Esses pontos de distribuição geralmente contêm vários terabytes de conteúdo ou mais. Distribuir esse conteúdo para esses servidores remotos custa muito em termos de largura de banda de rede e de tempo. Este recurso permite reatribuir um ponto de distribuição para outro site primário sem redistribuir o conteúdo. Esta ação atualiza a atribuição de sistema, persistindo todo o conteúdo no servidor. Para obter mais informações, consulte [Reatribuir um ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_reassign).

### <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Configurar o Otimização de Entrega do Windows para usar os grupos de limites do Configuration Manager
<!-- 1324696 -->
Você usa os grupos de limites do Configuration Manager para definir e regular a distribuição de conteúdo em sua rede corporativa e para escritórios remotos. A [Otimização de Entrega do Windows](/windows/deployment/update/waas-delivery-optimization) é uma tecnologia ponto-a-ponto baseada na nuvem para compartilhar conteúdo entre dispositivos do Windows 10. A partir desta versão, configure a Otimização de Entrega para usar seus grupos de limites ao compartilhar conteúdos entre pares. Uma nova configuração de cliente aplica o identificador do grupo de limites como o identificador do grupo da Otimização de Entrega no cliente. Quando o cliente se comunica com o serviço de nuvem da Otimização de Entrega, ele usa esse identificador para localizar os pares com o conteúdo desejado. Para mais informações, consulte [Conceitos fundamentais para o gerenciamento de conteúdo](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization).

### <a name="support-for-windows-10-arm64-devices"></a>Suporte para dispositivos Windows 10 ARM64
<!-- 1353704 -->
A partir desta versão, o cliente do Configuration Manager tem suporte nos dispositivos ARM64 do Windows 10. Os recursos existentes de gerenciamento de clientes devem funcionar com esses novos dispositivos. Por exemplo, inventário de hardware e software, atualizações de software e gerenciamento de aplicativos. A implantação de sistema operacional atualmente não tem suporte. 

### <a name="improved-support-for-cng-certificates"></a>Suporte aprimorado para certificados CNG
<!-- 1357314 -->
O Configuration Manager (branch atual) versão 1710 dá suporte a [Criptografia: CNG (Cryptography Next Generation)](/sccm/core/plan-design/network/cng-certificates-overview). A versão 1710 limita o suporte a certificados de clientes em vários cenários. 

A partir desta versão, use certificados do CNG para as seguintes funções de servidor habilitadas para HTTPS:
- Ponto de gerenciamento
- Ponto de distribuição
- Ponto de atualização de software
- Ponto de migração de estado  


### <a name="boundary-group-fallback-for-management-points"></a>Fallback de grupo de limites para pontos de gerenciamento
<!-- 1324594 -->
Configure relações de fallback para pontos de gerenciamento entre [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups). Esse comportamento proporciona maior controle para os pontos de gerenciamento que os clientes usam. Para obter mais informações, consulte [Configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups#management-points).


### <a name="cloud-distribution-point-site-affinity"></a>Afinidade do site do ponto de distribuição na nuvem
<!--503719-->
Esse recurso beneficia os clientes com uma hierarquia geograficamente dispersa de vários locais que usa pontos de distribuição na nuvem. Quando um cliente baseado na Internet pesquisava um tipo de conteúdo, anteriormente não havia nenhuma ordem na lista de pontos de distribuição na nuvem recebida pelo cliente. Esse comportamento pode resultar no recebimento de um tipo de conteúdo de pontos de distribuição na nuvem geograficamente distantes por clientes baseados na Internet. O download do conteúdo de um servidor distante desse tipo é geralmente mais lento do que o download de um servidor mais próximo.
 
Com a afinidade do site do ponto de distribuição na nuvem, um cliente baseado na Internet recebe uma lista ordenada. Essa lista prioriza os pontos de distribuição na nuvem no site atribuído do cliente. Esse comportamento permite que o administrador preserve sua intenção de design para downloads de conteúdo de recursos do site.
 

## <a name="management-insights"></a>Informações de gerenciamento
<!-- 1353967 -->
Os Insights de Gerenciamento do System Center Configuration Manager fornecem informações sobre o estado atual do ambiente. As informações baseiam-se na análise de dados do banco de dados do site. As informações ajudam você a melhor compreender seu ambiente e executar ações com base nas informações. Para obter detalhes, consulte [Insights de gerenciamento](/sccm/core/servers/manage/management-insights)

No Configuration Manager 1802, os seguintes insights estão disponíveis:
- Aplicativos:
    - Aplicativos sem implantações
- Serviços de nuvem: <!--1356412-->
    - Avaliar a prontidão do cogerenciamento 
    - Habilitar os dispositivos para serem híbridos e ingressados no Azure Active Directory
    - Modernizar a infraestrutura de identidade e acesso
    -  Atualizar os clientes para o Windows 10, versão 1709 ou acima 
- Coleções:
    - Coleções vazias
- Gerenciamento Simplificado:  <!--1355148-->
    - Versões de cliente desatualizadas  
- Centro de Software: 
    - Direcionar os usuários para o Centro de Software em vez de para o Catálogo de Aplicativos  
    - Usar a nova versão do Centro de Software 
- Windows 10: <!--1357421-->
    - Configurar a telemetria do Windows e a chave de ID comercial 
    - Conectar o Configuration Manager ao Upgrade Readiness 
   
<!-- ## Migration  -->



## <a name="client-management"></a>Gerenciamento de cliente

### <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Suporte para gateway de gerenciamento de nuvem para o Azure Resource Manager
<!-- 1324735 -->
Ao criar uma instância do [gateway de gerenciamento de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway) (CMG), o assistente agora oferece a opção de criar uma **implantação do Azure Resource Manager**. O [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) é uma plataforma moderna para gerenciar todos os recursos da solução como uma única entidade, chamado [grupo de recursos](/azure/azure-resource-manager/resource-group-overview#resource-groups). Ao implantar o CMG com o Azure Resource Manager, o site usa o Azure Active Directory (Azure AD) para autenticar e criar os recursos necessários para a nuvem. Essa implantação modernizada não exige o certificado de gerenciamento do Azure clássico. Para obter mais informações, consulte [Design da topologia do CMG](/sccm/core/clients/manage/plan-cloud-management-gateway#azure-resource-manager).

> [!IMPORTANT]
> Essa funcionalidade não habilita o suporte para CSPs (Provedores de Serviços de Nuvem) do Azure. A implantação do CMG com o Azure Resource Manager continua usando o serviço de nuvem clássico, ao qual o CSP não dá suporte. Para obter mais informações, consulte os [Serviços do Azure disponíveis no Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="improvements-to-cloud-management-gateway"></a>Melhorias no gateway de gerenciamento de nuvem  

- A partir desta versão, o **gateway de gerenciamento de nuvem** deixa de ser um recurso de pré-lançamento.  

- A documentação de recursos foi revisada e aprimorada. Para obter mais informações, consulte os seguintes artigos:
    - [Plano para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
    - [Tamanho e números de escala do gateway de gerenciamento de nuvem](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
    - [Segurança e privacidade para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
    - [Perguntas frequentes sobre o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
    - [Certificados para o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
    - [Configurar o gateway de gerenciamento de nuvem](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  


### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a>Configurar o inventário de hardware para coletar cadeias de caracteres maiores que 255 caracteres
<!-- 1357389 -->
Configure o tamanho de cadeias de caracteres para serem maiores que 255 caracteres nas propriedades de inventário de hardware. Essa alteração se aplica apenas às classes recém-adicionadas e às propriedades de inventário de hardware que não são chaves. Para obter detalhes, consulte o artigo [Estender o inventário de hardware](/sccm/core/clients/manage/inventory/extend-hardware-inventory#bkmk_GreaterThan255). 

 ### <a name="deprecation-announcement-for-linux-and-unix-client-support"></a>Comunicado de reprovação do suporte aos clientes Linux e Unix
 <!--510139-->
A Microsoft pretende preterir o suporte aos clientes Linux e UNIX no System Center Configuration Manager aproximadamente no prazo de um ano e, portanto, os clientes não serão incluídos na versão SCCM 1902 no início de 2019. A versão 1810 do Configuration Manager, no final de 2018, será a última versão para incluir os clientes Linux e UNIX e eles terão o suporte do ciclo de vida completo do Configuration Manager 1810. Após o Configuration Manager 1810, os clientes devem considerar o uso do Gerenciamento do Microsoft Azure para o gerenciamento de servidores Linux. As soluções do Azure têm amplo suporte para Linux que, na maioria dos casos, supera a funcionalidade do Configuration Manager, incluindo o gerenciamento de patches de ponta a ponta para o Linux.

### <a name="surface-device-dashboard"></a>Painel do dispositivo do Surface
<!--1355788-->
O painel do dispositivo do Surface fornece informações sobre os dispositivos do Surface encontrados no ambiente. No console, vá até **Monitoramento** > **Surface Devices**. Você pode exibir os itens:
- Percentual de Surfaces
- Percentual de modelos do Surface
- Cinco principais versões de firmware

Para obter detalhes, consulte o artigo [Painel do Surface](/sccm/core/clients/manage/surface-device-dashboard).

### <a name="change-in-the-configuration-manager-client-install"></a>Alteração na instalação do cliente do Configuration Manager
<!--1356195-->
A partir desta versão, o Silverlight deixa de ser instalado nos dispositivos cliente automaticamente. Para obter mais informações, consulte [Pré-requisitos de implantação de clientes em computadores Windows](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#bkmk_ExternalDependencies)

## <a name="co-management"></a>Cogerenciamento

### <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Transição da carga de trabalho do Endpoint Protection para o Intune usando o cogerenciamento
<!-- 1357365 -->
 A carga de trabalho do Endpoint Protection pode ser transferida para o Intune depois de habilitar o cogerenciamento. Para fazer a transição da carga de trabalho do Endpoint Protection, vá para a página de propriedades de cogerenciamento e mova a barra deslizante do Configuration Manager para **Piloto** ou **Todos**. Para saber mais sobre as cargas de trabalho, consulte [Cargas de trabalho de cogerenciamento](/sccm/comanage/workloads). Para obter mais informações sobre o cogerenciamento, consulte [Cogerenciamento para dispositivos Windows 10](/sccm/comanage/overview).
 
### <a name="co-management-dashboard-in-system-center-configuration-manager"></a>Painel de cogerenciamento no System Center Configuration Manager
<!--1356648-->
A partir desta versão, você pode exibir um painel com informações sobre o cogerenciamento. O painel ajuda você a analisar os computadores cogerenciados no ambiente. Os gráficos podem ajudar a identificar os dispositivos que podem precisar de atenção. Para obter detalhes, consulte o artigo [Painel de cogerenciamento](/sccm/comanage/how-to-monitor#co-management-dashboard). 


## <a name="compliance-settings"></a>Configurações de conformidade

### <a name="microsoft-edge-browser-policies"></a>Políticas do navegador Microsoft Edge
<!-- 1357310 -->
Para os clientes que utilizam o navegador da Web [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) em clientes Windows 10, crie uma política de configurações de conformidade do Configuration Manager para definir várias configurações do Microsoft Edge. Para obter mais informações, consulte [Criar o perfil do navegador Microsoft Edge](/sccm/compliance/deploy-use/browser-profiles). 



## <a name="application-management"></a>Gerenciamento de aplicativos

### <a name="allow-user-interaction-when-installing-an-application"></a>Permitir a interação do usuário ao instalar um aplicativo
<!-- 1356976 -->
Permita que um usuário final interaja com uma instalação de aplicativo durante a execução da sequência de tarefas. Por exemplo, execute um processo de instalação que solicite que o usuário final escolha entre várias opções. Alguns instaladores de aplicativos não podem silenciar os prompts de usuário ou o processo de instalação pode exigir valores de configuração específicos conhecidos apenas pelo usuário. Esse recurso permite que você manipule esses cenários de instalação. Para obter mais informações, consulte [Especificar as opções de experiência do usuário para o tipo de implantação](/sccm/apps/deploy-use/create-applications#bkmk_dt-ux).

### <a name="do-not-automatically-upgrade-superseded-applications"></a>Não fazer upgrade automaticamente de aplicativos substituídos
<!-- 1351266 -->
Configure uma implantação de aplicativo para não atualizar automaticamente qualquer versão substituída. Agora, ao criar a implantação na página **Configurações de Implantação** do **Assistente de Implantação de Software**, para uma finalidade de instalação **Disponível**, é possível habilitar ou desabilitar a opção **Fazer upgrade automático das versões substituídas deste aplicativo**. Para obter mais informações, consulte [Especificar as configurações de implantação](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy-settings).

### <a name="approve-application-requests-for-users-per-device"></a>Aprovar pedidos de aplicativos para usuários por dispositivo
<!-- 1357015 -->
Começando nesta versão, quando um usuário solicita um aplicativo que requer aprovação, o nome específico do dispositivo agora é parte da solicitação. Se o administrador aprova o pedido, o usuário só poderá instalar o aplicativo nesse dispositivo. O usuário deve enviar outro pedido para instalar o aplicativo em outro dispositivo. Para obter mais informações, consulte [Especificar as configurações de implantação](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy-settings).

 > [!Note]  
 > Esse é um recurso opcional. Para obter mais informações, consulte [Enable optional features from updates (Habilitar recursos opcionais de atualizações)](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  


### <a name="run-scripts-improvements"></a>Melhorias no recurso Executar scripts 
<!-- 1236459 -->
 A partir desta versão, **Executar Scripts** deixa de ser um recurso de pré-lançamento. A saída de script agora é retornada com a formatação JSON. Para saber mais, confira [Criar e executar scripts do PowerShell do console do Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).


## <a name="operating-system-deployment"></a>Implantação de sistema operacional

### <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Sequência de tarefas de upgrade in-loco do Windows 10 por meio do gateway de gerenciamento de nuvem
<!-- 1357149 -->
A [sequência de tarefas de upgrade in-loco](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version) do Windows 10 agora oferece suporte à implantação de clientes baseados na Internet gerenciados por meio do [gateway de gerenciamento de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway). Essa habilidade permite que usuários remotos façam upgrade com mais facilidade para o Windows 10 sem precisar se conectar à rede corporativa. Para obter mais informações, consulte [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence).

### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Melhorias na sequência de tarefas de upgrade in-loco do Windows 10
<!-- 1357425 -->
O modelo de sequência de tarefas padrão para o upgrade in-loco do Windows 10 agora inclui grupos adicionais com ações recomendadas para adicionar antes e depois do processo de upgrade. Essas ações são comuns entre muitos clientes que atualizam com sucesso os dispositivos para o Windows 10. Para obter mais informações, consulte [Criar uma sequência de tarefas para atualizar um sistema operacional](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-to-prepare-for-upgrade).

### <a name="improvements-to-operating-system-deployment"></a>Melhorias na implantação do sistema operacional
Esta versão inclui as seguintes melhorias na implantação de sistema operacional:
 - No Windows PE, ao iniciar cmtrace.exe, você não precisa mais escolher se deseja tornar este programa o visualizador padrão para arquivos de log. <!-- SMS 500897 -->
 - Adicione imagens de inicialização à etapa da sequência de tarefas [Baixar Conteúdo do Pacote](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent).
 - Melhorias na etapa [Executar a Sequência de Tarefas](/sccm/osd/understand/task-sequence-steps#child-task-sequence): <!-- 1261338 -->   
     - Suporte para todos os cenários de implantação de sistema operacional do Centro de Software, PXE e mídia.
     - Melhorias das ações do console, como copiar, importar, exportar e aviso durante a exclusão do objeto.
     - Suporte para o assistente para [Criar Arquivo de Conteúdo Pré-Teste](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent).
     - Integração com a verificação de implantação. Para obter mais informações, consulte [Implantações de alto risco de sequência de tarefas](/sccm/osd/deploy-use/deploy-a-task-sequence). 
     - A etapa Executar sequência de tarefas agora pode ser usada em vários níveis de sequências de tarefas, não apenas em um único relacionamento de pai-filho. Os relacionamentos de vários níveis aumentam a complexidade, portento, use com cuidado. Esses relacionamentos ainda estão marcados para referências circulares.
    
### <a name="deployment-templates-for-task-sequences"></a>Modelos de implantação para sequências de tarefas
<!-- 1357391 -->
O [assistente de implantação para sequências de tarefas](/sccm/osd/deploy-use/deploy-a-task-sequence) agora pode criar um modelo de implantação. O modelo de implantação pode ser salvo e aplicado a uma sequência de tarefas existente ou nova para criar uma implantação. 

### <a name="phased-deployments-for-task-sequences"></a>Implantações em fases para sequências de tarefas
<!--1356837-->
 As implantações em fases são um [recurso de pré-lançamento](/sccm/core/servers/manage/pre-release-features). As implantações em fases automatizam uma distribuição coordenada e sequenciada de uma sequência de tarefas em várias coleções. Você pode [criar implantações em fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) com o padrão de duas fases ou configurar várias fases manualmente. A implantação em fases de sequências de tarefas não dá suporte ao PXE e à mídia de instalação.




## <a name="software-center"></a>Centro de software

### <a name="install-multiple-applications-in-software-center"></a>Instalar vários aplicativos no Centro de Software
<!-- 1357126 -->
Se um usuário final ou um técnico da área de trabalho precisar instalar vários aplicativos em um dispositivo, o Centro de Software agora dará suporte à instalação de vários aplicativos selecionados. Esse comportamento permite que o usuário seja mais eficiente, não aguardando a conclusão de uma instalação antes do início da próxima. Para obter mais informações, consulte [Instalar vários aplicativos](/sccm/core/understand/software-center#install-multiple-applications) no novo guia do usuário do Centro de Software.

### <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Use o Centro de Software para navegar e instalar aplicativos disponíveis para usuários em dispositivos ingressados no Azure AD
<!-- 1322613 -->
Se você implantar aplicativos como disponíveis para usuários, eles agora podem navegar e instalá-los por meio do Centro de Software nos dispositivos Azure Active Directory (Azure AD). Para obter mais informações, consulte [Implantar aplicativos disponíveis para o usuário em dispositivos ingressados no Azure AD](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices).

### <a name="hide-installed-applications-in-software-center"></a>Ocultar os aplicativos instalados no Centro de Software
<!--1357592-->
Os aplicativos instalados agora podem ser ocultados no Centro de Software. Os aplicativos que já estão instalados não serão mais exibidos na guia Aplicativos quando essa opção estiver habilitada nas configurações do cliente. Essa opção é definida como o padrão quando você instala ou atualiza para o Configuration Manager 1802.  Os aplicativos instalados ainda ficam disponíveis para exame na guia de status da instalação. A seção [Ocultar os aplicativos instalados no Centro de Software](/sccm/core/clients/deploy/about-client-settings#bkmk_HideInstalled) traz mais detalhes.   

### <a name="hide-unapproved-applications-in-software-center"></a>Ocultar os aplicativos não aprovados no Centro de Software
 <!--1355146-->
Quando essa opção de configuração é habilitada, os aplicativos disponíveis para o usuário que exigem aprovação são ocultos no Centro de Software.  A seção [Ocultar os aplicativos não aprovados no Centro de Software](/sccm/core/clients/deploy/about-client-settings#bkmk_HideUnapproved) traz mais detalhes.  

### <a name="software-center-shows-user-additional-compliance-information"></a>O Centro de Software mostra mais informações de conformidade do usuário
<!-- 1235616 -->
 Ao usar o status do Atestado de Integridade do Dispositivo como uma regra de política de conformidade para o acesso condicional aos recursos da empresa, o Centro de Software agora mostra ao usuário a configuração do Atestado de Integridade do Dispositivo que não está em conformidade.


 ## <a name="software-updates"></a>Atualizações de software 

### <a name="schedule-automatic-deployment-rule-evaluation-to-be-offset-from-a-base-day"></a>Agende a avaliação da regra de implantação automática para o deslocamento de um dia base. 
<!--1357133-->
As regras de implantação automática podem ser agendadas para avaliar o deslocamento de um dia base. Ou seja, se o patch de terça-feira, na verdade, cair na quarta-feira para você, o agendamento de avaliação poderá ser definido para a segunda terça-feira do deslocamento do mês por um dia. Para obter detalhes, consulte [Implantar as atualizações de software automaticamente](/sccm/sum/deploy-use/automatically-deploy-software-updates#BKMK_CreateAutomaticDeploymentRule). 



## <a name="reporting"></a>Relatórios

### <a name="report-for-default-browser-counts"></a>Relatório para as contagens padrão do navegador
<!-- 1357830 -->
Agora, há um novo relatório para mostrar a contagem de clientes com um navegador web específico como o padrão do Windows. Consulte o relatório **Contagens do navegador padrão** no grupo de relatórios **Software – empresas e produtos**. Para obter mais informações, consulte a [Lista de relatórios](/sccm/core/servers/manage/list-of-reports#software---companies-and-products).

### <a name="report-on-windows-autopilot-device-information"></a>Relatório sobre as informações do dispositivo do Windows Autopilot
<!-- 1351442 -->
O Windows Autopilot é uma solução para integração e configuração de novos dispositivos Windows 10 de forma moderna. Para saber mais, consulte uma [Visão geral do Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). Um método de registro de dispositivos existentes com o Windows Autopilot é carregar as informações do dispositivo para a Microsoft Store para Empresas e Educação. Esta informação inclui o número de série do dispositivo, o identificador de produto do Windows e um identificador de hardware. Use o Configuration Manager para coletar e relatar essas informações de dispositivo com o novo relatório, **Informações de dispositivo do Windows Autopilot**, no nó de relatórios **Hardware – Geral**. Para saber mais, consulte [Como preparar dispositivos baseados na Internet para cogerenciamento](/sccm/comanage/how-to-prepare-win10#windows-autopilot) ao se preparar para o cogerenciamento.

### <a name="report-on-windows-10-servicing-details-for-a-specific-collection"></a>Relatar os detalhes do Serviço do Windows 10 para uma coleção específica
<!--1357653-->
O relatório **Detalhes do Serviço do Windows 10 para uma coleção específica** exibe informações gerais sobre o serviço do Windows 10 para uma coleção específica. Este relatório mostra a ID do recurso, o nome do NetBIOS, o nome do SO, o nome da versão do SO, a compilação, o branch do SO e o estado de manutenção para dispositivos do Windows 10. Para obter mais informações, consulte a [Lista de relatórios](/sccm/core/servers/manage/list-of-reports#operating-system)



<!-- ## Inventory  -->



<!-- ## Mobile device management -->



 ## <a name="protect-devices"></a>Proteger dispositivos

### <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Melhorias nas Políticas do Configuration Manager para o Windows Defender Exploit Guard
<!-- 1356220 -->
As configurações de políticas adicionais para os componentes [Redução da Superfície de Ataque](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy#bkmk_ASR) e [Acesso controlado a pastas](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy#bkmk_CFA) foram adicionadas ao Configuration Manager para o [Windows Defender Exploit Guard](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard).

### <a name="new-host-interaction-settings-for-windows-defender-application-guard"></a>Novas configurações de interação de host para o Windows Defender Application Guard
<!-- 1356256 -->
Para dispositivos Windows 10 versão 1709 e posteriores, há duas novas configurações de interação de host para o [Windows Defender Application Guard](/sccm/protect/deploy-use/create-deploy-application-guard-policy#bkmk_HIS): 
- O acesso ao processador de gráficos virtuais do host pode ser concedido a sites. 
- Arquivos baixados dentro do contêiner podem ser persistentes no host. 




## <a name="configuration-manager-console"></a>Console do Configuration Manager

### <a name="improvements-to-the-configuration-manager-console"></a>Melhorias no console do Configuration Manager 
Esta versão inclui as melhorias a seguir no console do Configuration Manager.
- As listas de dispositivos em Ativos e Conformidade, Dispositivos agora exibem o usuário primário por padrão. Essa coluna é exibida apenas no nó Dispositivos. O último usuário conectado também pode ser adicionado como uma coluna opcional.<!-- 1357280 --> Habilite as configurações do cliente [Afinidade de usuário e dispositivo](/sccm/core/clients/deploy/about-client-settings#user-and-device-affinity) no site para associar um usuário primário a um dispositivo.
- Se uma coleção for membro de outra coleção e for renomeada, o novo nome será atualizado de acordo com as regras de associação.<!--1357282--> 
- Ao usar o controle remoto em um cliente com vários monitores em um ajuste de DPI diferente, o cursor do mouse agora faz o mapeamento correto entre eles. <!--433170-->
- O [painel de Gerenciamento de Clientes do Office 365](/sccm/sum/deploy-use/office-365-dashboard) exibe uma lista de dispositivos relevantes quando seções de gráfico são selecionadas. <!--1357281 --> 



## <a name="next-steps"></a>Próximas etapas
Quando estiver pronto para instalar esta versão, consulte [Atualizações para o Configuration Manager](/sccm/core/servers/manage/updates).
