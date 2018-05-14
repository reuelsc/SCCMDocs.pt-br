---
title: Versões do Technical Preview
titleSuffix: Configuration Manager
description: Saiba mais sobre a versão do Technical Preview para fazer o test drive das novas funcionalidades do System Center Configuration Manager.
ms.date: 04/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6b39f5eec4209e176374dcbdffc11183625c4967
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Visualização técnica do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

**Bem-vindo ao System Center Configuration Manager Technical Preview**. Este artigo fornece detalhes sobre a versão de visualização em evolução que introduz novas funcionalidades e recursos nos quais estamos trabalhando. Cada versão do technical preview introduz novos recursos que não estão incluídos no branch atual do Configuration Manager no momento em que a versão do technical preview é disponibilizada. Esses recursos podem, eventualmente, ser incluídos em uma atualização da ramificação atual, mas antes de finalizarmos os recursos e os adicionarmos, queremos que você tenha a oportunidade de testá-los e fornecer comentários.  

 Como esta versão é technical preview, os detalhes e funcionalidades estão sujeitos a alterações.  

 Este artigo contém informações que se aplicam a todas as versões do Technical Preview. Também lista cada nova funcionalidade (ou recurso) junto com a versão Technical Preview na qual a funcionalidade aparece primeiro, como a versão 1804 de abril de 2018. Essas funcionalidades são detalhadas em tópicos separados, dedicados a cada versão de visualização.  

 Para obter informações sobre o que há de novo do branch atual do Configuration Manager, consulte [Novidades no System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Requisitos e limitações do Technical Preview  

> [!IMPORTANT]     
>  O Technical Preview é licenciado somente para uso em ambiente de laboratório.  A Microsoft não pode fornecer serviços de suporte e alguns recursos podem não estar disponíveis para o software na versão prévia. Além disso, o software de versão prévia pode ter padrões diferentes ou reduzidos de segurança, privacidade, acessibilidade, disponibilidade e confiabilidade em comparação com o software fornecido comercialmente.  

 Para a maioria dos pré-requisitos do produto, use as informações contidas em [Configurações com suporte para o System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). As seguintes exceções se aplicam às versões de Technical Preview:  

-   Cada instalação permanece ativa durante 90 dias antes de se tornar inativa.  

-   O inglês é o único idioma com suporte.


-   Há suporte apenas para os seguintes sinalizadores de instalação (opções):  

    -   **/silent**  
    -   **/testdbupgrade**    


-   Por padrão, quando você usa o technical preview, o ponto de conexão de serviço é instalado no modo online. Ele não dá suporte à alteração para o modo offline.

-   Os artigos separados para cada versão específica do technical preview incluem requisitos ou limitações adicionais, conforme aplicável.

-   Não há suporte para a migração de ou para esta compilação de visualização.  

-   Não há suporte para a atualização para esta compilação de visualização. 

-   Não há nenhum suporte para recuperação de site desde a pasta cd.latest.  <!--507106-->

-   Não há suporte para atualização para um build de produção (ramificação atual) deste build de preview. No entanto, quando as atualizações estão disponíveis para uma versão prévia, é possível localizá-las e instalá-las do nó **Atualizações e Manutenção** do console do Configuration Manager. Para obter um vídeo do processo de atualização no console, veja [Instalação dos pacotes de atualização do ConfigMgr](https://www.youtube.com/embed/KBd_EGFbUT8) no youtube.com.  
-   Há suporte apenas para um site primário autônomo. Não há suporte para um site de administração central, para vários sites primários ou para sites secundários.  

Há suporte para os seguintes produtos e tecnologias por esse branch do Configuration Manager. No entanto, sua inclusão neste conteúdo não implica uma extensão de suporte para um produto ou versão além do ciclo de vida de suporte individual desse produto. Os produtos além de seu ciclo de vida de suporte não têm suporte para uso com o Configuration Manager. Para obter mais informações sobre os Ciclos de vida de suporte da Microsoft, visite o site [Ciclo de Vida do Suporte da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) .  

-   Há suporte apenas para as seguintes versões do SQL Server:  

    -   SQL Server 2017 (com a atualização cumulativa 2 e posterior), do Configuration Manager versão 1710 em diante
    -   SQL Server 2016 (sem Service Pack e posterior)
    -   SQL Server 2014 (com Service Pack 1 e posterior)
    -   SQL Server 2012 (com Service Pack 3 ou posterior)


-   O site dá suporte a até 10 clientes, que devem executar uma das seguintes versões do Windows:  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 7  

##  <a name="bkmk_install"></a> Instalar e atualizar a Visualização Técnica  
 O System Center Configuration Manager Technical Preview é diferente da versão atual do System Center Configuration Manager.  

 Para usar o technical preview, primeiro é necessário instalar uma **versão de linha de base** do build do technical preview. Depois de instalar uma versão de linha de base, use as **atualizações no console** para atualizar sua instalação para a versão prévia mais recente. Normalmente, as novas versões da Technical Preview são disponibilizadas todos os meses.

Cada versão de visualização conta com suporte até que três versões sucessivas estejam disponíveis. Em outras palavras, quando a versão 1708 foi liberada, a versão 1704 deixou de ter suporte, mas as versões 1705 1706 e 1707 permaneceram com suporte. Quando uma linha de base fica sem suporte, ainda há suporte para a instalação um novo site do Technical Preview até que uma nova versão de linha de base esteja disponível, desde que, você atualize a instalação para uma versão com suporte posteriormente. Atualize para a última versão e, em seguida, repita esse processo até poder instalar a versão mais atual do technical preview.

> [!TIP]  
>  Quando você instala uma atualização do Technical Preview, atualiza a instalação da versão prévia para essa nova versão de Technical Preview. Uma instalação de Technical Preview nunca tem a opção de atualizar para uma instalação de ramificação atual nem receber atualizações de versão da ramificação atual.  

**Versões de linha de base ativas do Technical Preview:**
   
É possível instalar uma versão de linha de base em até um ano após seu lançamento. No entanto, quando você instala um novo site de visualização técnica, é recomendável usar a versão de linha de base mais recente disponível.
-  **Technical Preview 1804** – o Configuration Manager Technical Preview 1804 está disponível como uma atualização no console e como uma nova versão de linha de base. Baixe as versões de linha de base [no Centro de Avaliação do TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).


##  <a name="BKMK_TPFeedback"></a> Enviando comentários  
 Adoramos ouvir seus comentários sobre as funcionalidades de nossos technical previews. Para obter mais informações, consulte [Comentários sobre o produto](../understand/find-help.md#product-feedback).

Caso tenha sugestões sobre novos recursos que gostaria de ver, gostaríamos de saber também. Para enviar novas ideias e para votar nas ideias enviadas por outras pessoas, [visite nossa página de opinião do usuário](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Recursos fornecidos na visualização técnica mais recente  
Veja a seguir as funcionalidades fornecidas com a versão de technical preview mais recente do Configuration Manager.  Funcionalidades que estavam disponíveis em uma versão anterior do technical preview permanecem disponíveis em versões posteriores. De forma semelhante, as funcionalidades que foram adicionadas ao branch atual do Configuration Manager permanecem disponíveis em versões de technical preview.  Clique no conteúdo relativo a cada versão de preview saber mais sobre uma funcionalidade específica.  

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1804"></a>Technical Preview versão 1804
- [Configurar uma biblioteca de conteúdo remoto para o servidor do site](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server) <!--1357525--> 
- [Enviar comentários do console do Configuration Manager](capabilities-in-technical-preview-1804.md#bkmk_feedback) <!--1357542--> 
- [Centro de Suporte](capabilities-in-technical-preview-1804.md#support-center) <!--1357489--> 
- [Kit de ferramentas do Configuration Manager](capabilities-in-technical-preview-1804.md#configuration-manager-toolkit) <!--1357145--> 
- [Desinstalar o aplicativo na revogação da aprovação](capabilities-in-technical-preview-1804.md#uninstall-application-on-approval-revocation) <!--1357891--> 
- [Excluir contêineres do Active Directory da descoberta](capabilities-in-technical-preview-1804.md#exclude-active-directory-containers-from-discovery) <!--1358143--> 
- [Especificar a visibilidade do link de site do Catálogo de Aplicativos no Centro de Software](capabilities-in-technical-preview-1804.md#specify-the-visibility-of-the-application-catalog-website-link-in-software-center) <!--1358214--> 
- [Filtrar regras de implantação automática pela arquitetura de atualização de software](capabilities-in-technical-preview-1804.md#filter-automatic-deployment-rules-by-software-update-architecture) <!--1322266--> 
- [Melhorias na implantação do sistema operacional](capabilities-in-technical-preview-1804.md#improvements-to-os-deployment) <!--1358330,1358493--> 
- [Melhorias no console do Configuration Manager](capabilities-in-technical-preview-1804.md#improvements-to-the-configuration-manager-console) <!--510252--> 



## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>Funcionalidades fornecidas em technical previews recentes com suporte
Veja a seguir as funcionalidades fornecidas com versões anteriores da versão de technical preview do Configuration Manager ainda com suporte. 

<!-- This is the full list of new features in the past three TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |Funcionalidade |Versão do Technical Preview |Versão do Branch Atual|  
 |----------------|---------------------|--------------------|
 | Os pontos de distribuição por pull são compatíveis com os pontos de distribuição de nuvem como origem <!--1321554--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#pull-distribution-points-support-cloud-distribution-points-as-source)  | ![Não foi adicionado](media/Red_X.gif) | 
 | O suporte parcial de download no cache de par de cliente para reduzir a utilização de WAN <!--1357346--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#partial-download-support-in-client-peer-cache-to-reduce-wan-utilization)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Janelas de manutenção no Centro de Software <!--1358131--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#maintenance-windows-in-software-center)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Guia personalizada para página da Web no Centro de Software <!--1358132--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#custom-tab-for-webpage-in-software-center)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Habilitar o suporte de atualização de software de terceiros em clientes <!--1357605--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Habilitar copiar/colar de detalhes do ativo das exibições de monitoramento <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-copypaste-of-asset-details-from-monitoring-views)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Extensões do SCAP <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#scap-extensions)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Transição da carga de trabalho do Endpoint Protection para o Intune usando o cogerenciamento <!-- 1357365 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#transition-endpoint-protection-workload-to-intune-using-co-management) | [Versão 1802](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune) |  
 | Configurar o Otimização de Entrega do Windows para usar os grupos de limites do Configuration Manager <!-- 1324696 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups) | [Versão 1802](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization) |  
 | Sequência de tarefas de atualização in-loco do Windows 10 por meio do gateway de gerenciamento de nuvem <!-- 1357149 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway) | [Versão 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg) |  
 | Melhorias na sequência de tarefas de atualização in-loco do Windows 10 <!-- 1357425 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-windows-10-in-place-upgrade-task-sequence) | [Versão 1802](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system) |  
 | Melhorias em pontos de distribuição habilitados para PXE <!-- 1357580 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) | ![Não foi adicionado](media/Red_X.gif) | 
 | Modelos de implantação para sequências de tarefas <!-- 1357391 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#deployment-templates-for-task-sequences) | [Versão 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS) |  
 | Painel do ciclo de vida do produto <!--1319632 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) | ![Não foi adicionado](media/Red_X.gif) | 
 | Melhorias em relatórios <!--1357653 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-reporting) | [Versão 1802](/sccm/core/servers/manage/list-of-reports#operating-system) |  
 | Melhorias no Centro de Software <!--1357592 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-software-center) | [Versão 1802](/sccm/core/clients/deploy/about-client-settings#BKMK_HideInstalled) |  
 | Fallback de grupo de limites para pontos de gerenciamento <!-- 1324594 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#boundary-group-fallback-for-management-points) | [Versão 1802](/sccm/core/servers/deploy/configure/boundary-groups#management-points) |  
 | Suporte aprimorado para certificados CNG <!-- 1357314 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improved-support-for-cng-certificates) | [Versão 1802](/sccm/core/plan-design/network/cng-certificates-overview) |  
 | Suporte para gateway de gerenciamento de nuvem no Azure Resource Manager <!-- 1324735 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#cloud-management-gateway-support-for-azure-resource-manager) | [Versão 1802](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager) |  
 | Aprovar solicitações de aplicativo para usuários por dispositivo <!-- 1357015 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#approve-application-requests-for-users-per-device) | [Versão 1802](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings) |  
 | Usar o Centro de Software para navegar e instalar aplicativos disponíveis para os usuários em dispositivos ingressados no Azure AD <!-- 1322613 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices) | [Versão 1802](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices) |  
 | Relatório sobre as informações do dispositivo Windows AutoPilot <!-- 1351442 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#report-on-windows-autopilot-device-information) | [Versão 1802](/sccm/core/clients/manage/co-management-prepare#new-windows-10-devices) |  
 | Melhorias nas políticas do Configuration Manager para o Windows Defender Exploit Guard <!-- 1356220 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard) | [Versão 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |  
 | Políticas do navegador Microsoft Edge <!-- 1357310 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#microsoft-edge-browser-policies) | [Versão 1802](/sccm/compliance/deploy-use/browser-profiles) | 
 | Relatório para as contagens padrão do navegador <!-- 1357830 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#report-for-default-browser-counts) | [Versão 1802](/sccm/core/servers/manage/list-of-reports#software---companies-and-products) | 
 | Suporte para dispositivos Windows 10 ARM64 <!-- 1353704 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#support-for-windows-10-arm64-devices) | [Versão 1802](/sccm/core/plan-design/configs/support-for-windows-10) |  
 | Criar implantações em fases <!-- 1356837 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#create-phased-deployments) | [Versão 1802](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) |
 | Relatórios de cogerenciamento <!-- 1356648 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#co-management-reporting) | [Versão 1802](\sccm\core\clients\manage\client-management-dashboard) |
 | Melhorias ao agendamento de avaliação da regra de implantação automática <!-- 1357133 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-automatic-deployment-rule-evaluation-schedule) | [Versão 1802](/sccm/sum/deploy-use/automatically-deploy-software-updates#BKMK_CreateAutomaticDeploymentRule) |
 | Reatribuir ponto de distribuição <!-- 1306937 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#reassign-distribution-point) | [Versão 1802](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_reassign) |
 | Melhorias ao inventário de hardware <!-- 1357389 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-hardware-inventory) | [Versão 1802](/sccm/core/clients/manage/inventory/extend-hardware-inventory#BKMK_GreaterThan255) |
 | Melhorias às configurações do cliente para o Centro de Software do <!-- 1355146 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-client-settings-for-software-center) | [Versão 1802](/sccm/core/clients/deploy/about-client-settings#BKMK_HideUnapproved) |
 | Novas configurações para o Windows Defender Application Guard <!-- 1356256 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#new-settings-for-windows-defender-application-guard) | [Versão 1802](/sccm/protect/deploy-use/create-deploy-application-guard-policy#BKMK_HIS) |
 | Melhorias ao recurso Executar Scripts <!-- 1236459 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-run-scripts) | [Versão 1802](/sccm/apps/deploy-use/create-deploy-scripts) |
 
  

## <a name="capabilities-delivered-in-previous-technical-previews"></a>Recursos fornecidos em visualizações técnicas anteriores
Veja a seguir as funcionalidades específicas fornecidos com versões anteriores da versão de technical preview do Configuration Manager. Essas funcionalidades permanecem disponíveis em versões posteriores, mas ainda não estão disponíveis em uma versão de branch atual. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |Funcionalidade |Versão do Technical Preview |  
 |----------------|---------------------|
 | Serviço de respondente PXE baseado no cliente <!-- 1357148 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
 |Alta disponibilidade da função de servidor do site <!-- 1128774 --> |[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 |Suporte de inicialização de rede PXE para IPv6 <!-- 1269793 --> |[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
 |Usar o Azure Active Directory <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
 |Avaliação de conformidade para atualizações do Windows Update para Empresas <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
 |Acesso a dados do ponto de extremidade OData <!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
 |Melhorias no Asset Intelligence <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
 |Os usuários finais podem instalar aplicativos por meio do Portal da Empresa <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## <a name="see-also"></a>Consulte também  
[Novidades no System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Introduction to System Center Configuration Manager](../../core/understand/introduction.md)

> [!Tip]  
> Para saber mais sobre os recursos atuais de branch que exigem autorização para habilitação, confira [Recursos de pré-lançamento](/sccm/core/servers/manage/pre-release-features).  
> Para saber mais sobre os recursos atuais de branch que precisam ser habilitados primeiro, confira [Habilitar recursos opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  

