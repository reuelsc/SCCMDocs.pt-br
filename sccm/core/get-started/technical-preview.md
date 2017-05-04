---
title: Technical Preview do System Center Configuration Manager | Microsoft Docs
description: "Saiba mais sobre a versão do Technical Preview que permite a você testar novas funcionalidades e recursos no System Center Configuration Manager."
ms.custom: na
ms.date: 4/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 157
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: ae008c91a7387ba76f2bfac13f8feb489a0cc558
ms.openlocfilehash: 8ffaee12bd826e2f19653b215ee19423ea672433
ms.lasthandoff: 04/21/2017


---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Visualização técnica do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

**Bem-vindo ao System Center Configuration Manager Technical Preview**. Este tópico fornece detalhes sobre a versão de preview em evolução que introduz novas funcionalidades e recursos em que estamos trabalhando. Com cada versão de technical preview, são apresentados novos recursos que não estão incluídos no Branch Atual do System Center Configuration Manager assim que a versão do technical preview é disponibilizada. Esses recursos podem, eventualmente, ser incluídos em uma atualização da ramificação atual, mas antes de finalizarmos os recursos e os adicionarmos, queremos que você tenha a oportunidade de testá-los e fornecer comentários.  

 Como esta é uma technical preview, os detalhes e funcionalidades estão sujeitos a alterações.  

 Este tópico contém informações que se aplicam a todas as versões do Technical Preview e também lista cada nova funcionalidade (ou recurso) conjuntamente com a versão do Technical Preview na qual a funcionalidade aparece primeiro, como a versão 1701 de janeiro de 2017. Os detalhes desses recursos são descritos em tópicos separados dedicados a versão de preview.  

 Para obter informações sobre o que há de novo do branch atual do Configuration Manager, consulte [Novidades no System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Requisitos e limitações do Technical Preview  

> [!IMPORTANT]     
>  O Technical Preview é licenciado somente para uso em ambiente de laboratório.  A Microsoft não pode fornecer serviços de suporte e alguns recursos podem não estar disponíveis para o software na versão de preview. Além disso, o software na versão de preview pode padrões diferentes ou reduzidos de segurança, privacidade, acessibilidade, disponibilidade e confiabilidade em comparação com o software fornecido comercialmente.  

 Para a maioria dos pré-requisitos do produto, use as informações contidas em [Configurações com suporte para o System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). As seguintes exceções se aplicam às versões de Technical Preview:  

-   Cada instalação permanece ativa durante 90 dias antes de se tornar inativa.  

-   O inglês é o único idioma com suporte.  

-   Há suporte apenas para um site primário autônomo. Não há suporte para um site de administração central, para vários sites primários ou para sites secundários.  

-   Há suporte apenas para as seguintes versões do SQL Server:  

    -   SQL Server 2016 (sem Service Pack e posterior)
    -   SQL Server 2014 (sem Service Pack e posterior)
    -   SQL Server 2012 (sem Service Pack 2 ou posterior)


-   O site dá suporte a até 10 clientes, que devem executar um dos seguintes:  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 8  
      -   Windows 7  


-   Há suporte apenas para os seguintes sinalizadores de instalação (opções):  

    -   **/silent**  
    -   **/testdbupgrade**    


-   Por padrão, quando você usar a visualização técnica, o ponto de conexão de serviço será definido como o modo online quando é instalado e não dá suporte a uma alteração para o modo offline.

-   Quando aplicável, os requisitos ou limitações adicionais são incluídos com os detalhes de cada versão específica da Visualização Técnica  

-   Não há suporte para a migração de ou para esta compilação de visualização.  

-   Não há suporte para a atualização para esta compilação de visualização.  

-   Não há suporte para atualização para um build de produção (ramificação atual) deste build de preview. No entanto, quando as atualizações estão disponíveis para uma versão prévia, é possível localizá-las e instalá-las do nó **Atualizações e Manutenção** do console do Configuration Manager. Para obter um vídeo do processo de atualização no console, veja [Instalação dos pacotes de atualização do ConfigMgr](https://www.youtube.com/embed/KBd_EGFbUT8) no youtube.com.  

##  <a name="bkmk_install"></a> Instalar e atualizar a Visualização Técnica  
 O System Center Configuration Manager Technical Preview é diferente da versão atual do System Center Configuration Manager.  

 Para usar a technical preview, primeiro você deve instalar uma **versão de linha de base** do build da versão de technical preview. Depois de instalar uma versão de linha de base, use as **atualizações no console** para atualizar sua instalação para a versão de preview mais recente.     Normalmente, as novas versões da Technical Preview são disponibilizadas todos os meses.

Cada versão de visualização conta com suporte até que três versões sucessivas estejam disponíveis. Ou seja, quando a versão 1702 for liberada, a versão 1610 não terá mais suporte, mas as versões 1611, 1612 e 1701 permanecerão com suporte. Quando uma linha de base ficar sem suporte (como a versão 1610), ainda haverá suporte para instalar um novo site do Technical Preview até que uma nova versão de linha de base esteja disponível, desde que, depois, você atualize a instalação para uma versão com suporte. Durante a atualização, se você não vir a versão mais recente disponível no console, atualize para a versão mais recente oferecida e, em seguida, repita esse processo até que você possa instalar a versão mais atual da visualização técnica.

> [!TIP]  
>  Quando você instala uma atualização da visualização técnica, atualiza a instalação da visualização para essa nova versão de visualização técnica.    Uma instalação de visualização técnica nunca tem a opção de atualizar para uma instalação de ramificação atual nem receber atualizações de versão da ramificação atual.  

**Versões de linha de base ativas do Technical Preview:**  
É possível instalar uma versão de linha de base em até 1 ano após seu lançamento. No entanto, quando você instala um novo site de visualização técnica, é recomendável usar a versão de linha de base mais recente disponível.
-  **Technical Preview 1703** – O Configuration Manager Technical Preview 1703 está disponível como uma atualização no console para o Configuration Manager Technical Preview e como uma nova versão de linha de base no site do TechNet Evaluation Center.

-  **Technical Preview 1610** – O Configuration Manager Technical Preview 1610 estava disponível como uma atualização no console para o Configuration Manager Technical Preview e como uma nova versão de linha de base. Se você tiver a mídia para a instalação do 1610, é recomendável em vez disso baixar a versão 1703 e instalá-la.




##  <a name="BKMK_TPFeedback"></a> Enviando comentários  
 Adoraríamos receber seus comentários sobre nossas visualizações técnicas. Para enviar comentários sobre os recursos em cada visualização, clique no link de nosso formulário de comentários na página do [programa de comentários do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) no site do Microsoft Connect.  

 E se tiver sugestões sobre novos recursos que gostaria de ver, gostaríamos de saber também. Para enviar novas ideias e para votar nas ideias enviadas por outras pessoas, [visite nossa página de opinião do usuário](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Recursos fornecidos na visualização técnica  
 Veja a seguir os recursos fornecidos com cada versão de technical preview do Configuration Manager.  Recursos que estão disponíveis a partir de uma versão de technical preview permanecem disponíveis nas versões posteriores. De forma semelhante, os recursos que foram adicionados à Versão do System Center Configuration Manager (branch atual) permanecem disponíveis em versões de technical preview posteriores.  Clique no conteúdo relativo a cada versão de preview saber mais sobre uma funcionalidade específica.  

 |Funcionalidade |Versão do Technical Preview |Versão do Branch Atual|  
|----------------|---------------------|--------------------|
 |Configurar aplicativos do Android com as políticas de configuração de aplicativo  |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#configure-android-apps-with-app-configuration-policies)|![Não foi adicionado](media/Red_X.gif)|
 |O inventário de hardware coleta informações de Inicialização Segura |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#hardware-inventory-collects-secure-boot-information)|![Não foi adicionado](media/Red_X.gif)|
 |Adicionar sequências de tarefas filho a uma sequência de tarefas|[Tech Preview 1704](capabilities-in-technical-preview-1704.md#add-child-task-sequences-to-a-task-sequence)|![Não foi adicionado](media/Red_X.gif)|
 |Recarregue as imagens de inicialização com a versão atual do Windows PE |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#reload-boot-images-with-current-windows-pe-version)|![Não foi adicionado](media/Red_X.gif)|
 |Melhorias na implantação do sistema operacional|[Tech Preview 1704](capabilities-in-technical-preview-1704.md#improvements-to-operating-system-deployment)|![Não foi adicionado](media/Red_X.gif)|
 |Implantar aplicativos iOS adquiridos por volume em coleções de dispositivos|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#deploy-volume-purchased-ios-apps-to-device-collections)|[Versão 1702](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)|
 |Links diretos para aplicativos no Centro de Software|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#direct-links-to-applications-in-software-center)|![Não foi adicionado](media/Red_X.gif)
 |Certificados PFX para computadores cliente Windows do Configuration Manager|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#pfx-certificates-for-configuration-manager-windows-client-computers)|![Não foi adicionado](media/Red_X.gif)|
 |Assistente de Configuração de Serviços do Azure|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#configure-azure-services-wizard)|![Não foi adicionado](media/Red_X.gif)|
 |Converta BIOS em UEFI em uma sequência de tarefas de atualização do sistema operacional| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#convert-from-bios-to-uefi-during-an-in-place-upgrade) |[Versão 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)|
 |Grupos de sequências de tarefas recolhíveis| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#collapsible-task-sequence-groups) |![Não foi adicionado](media/Red_X.gif)|
 |Configurações do cliente para configurar o Windows Analytics para Preparação para Atualização | [Tech Preview 1703](capabilities-in-technical-preview-1703.md#client-settings-to-configure-windows-analytics-for-upgrade-readiness) |![Não foi adicionado](media/Red_X.gif)|
 |Novas configurações de conformidade para dispositivos iOS|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#new-compliance-settings-for-ios-devices)|[Versão 1702](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)|
 |Criar certificados PFX com suporte a S/MIME|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#create-pfx-certificates-with-s-mime-support)|[Versão 1702](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)|
 |Verificar se há arquivos executáveis antes de instalar um aplicativo|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#check-for-running-executable-files-before-installing-an-application)|[Versão 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Enviar comentários do console do Configuration Manager | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#send-feedback-from-the-configuration-manager-console)    |[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#send-feedback-from-the-configuration-managercconsole)  |
 |Alterações em Atualizações e Manutenção  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#changes-for-updates-and-servicing)  |[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#changes-for-updates-and-servicing) |
 |Aprimoramentos de cache de pares  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#peer-cache-improvements) |[Versão 1702](/sccm/core/plan-design/hierarchy/client-peer-cache)|
 |Usar o Azure Active Directory  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |![Não foi adicionado](media/Red_X.gif)|
 |Aprimoramentos na política de conformidade de dispositivo de acesso condicional | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#conditional-access-device-compliance-policy-improvements) |[Versão 1702](/sccm/mdm/deploy-use/create-compliance-policy)|
 |Alerta de versão do cliente de antimalware | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert) |[Versão 1702](/sccm/protect/deploy-use/endpoint-configure-alerts?branch=live#alert-for-outdated-malware-client)|
 |Avaliação de conformidade para atualizações do Windows Update for Business | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |![Não foi adicionado](media/Red_X.gif)|
 |Aprimoramentos nas configurações e mensagens de notificação do Centro de Software para sequências de tarefas de alto impacto|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert)|[Versão 1702](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)|
 |Suporte do Android for Work| [Tech Preview 1702](capabilities-in-technical-preview-1702.md#android-for-work-support) |[Versão 1702](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-for-work-enrollment)|
 |Aprimoramentos de grupos de limites para os pontos de atualização de software | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#boundary-groups-improvements-for-software-update-points)    |[Versão 1702](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)  |
 |O inventário de hardware coleta informações de UEFI | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#hardware-inventory-collects-uefi-information)|[Versão 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#hardware-inventory-collects-uefi-information) |
 |Melhorias na implantação do sistema operacional| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#improvements-to-operating-system-deployment)|[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment) |
 |Hospede as atualizações de software nos pontos de distribuição baseados em nuvem| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#host-software-updates-on-cloud-based-distribution-points)|![Não foi adicionado](media/Red_X.gif) |
 |Validar dados de atestado de integridade do dispositivo por meio de pontos de gerenciamento| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#validate-device-health-attestation-data-via-management-points)| [Versão 1702](/sccm/core/servers/manage/health-attestation) |
 |Conector do OMS para a nuvem Microsoft Azure Governamental |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#use-the-oms-connector-for-microsoft-azure-government-cloud) |[Versão 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig) |
 |As versões do Android e iOS não precisam mais ser direcionadas nos assistentes de criação |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |![Não foi adicionado](media/Red_X.gif) |
 |Acesso a dados do ponto de extremidade OData |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|![Não foi adicionado](media/Red_X.gif)|
 |Ponto de Serviço do Data Warehouse |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#the-data-warehouse-service-point)|[Versão 1702](/sccm/core/servers/manage/data-warehouse)|
 |Ferramenta de limpeza da biblioteca de conteúdo |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#content-library-cleanup-tool)|[Versão 1702](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) |
 |Melhorias da pesquisa no console |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#improvements-for-in-console-search)|[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-for-in-console-search)|
 |Impedir a instalação de um aplicativo se estiver executando um programa especificado|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#prevent-installation-of-an-application-if-a-specified-program-is-running)|[Versão 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Nova notificação do Windows Hello para Empresas para usuários finais|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#new-windows-hello-for-business-notification-for-end-users)|![Não foi adicionado](media/Red_X.gif)|
 |Suporte da Windows Store para Empresas no Configuration Manager|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#windows-store-for-business-support-in-configuration-manager)|![Não foi adicionado](media/Red_X.gif)|
 |Retornar à página anterior quando uma sequência de tarefas falhar|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#return-to-previous-page-when-a-task-sequence-fails)|[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment)|
 |Suporte dos arquivos de instalação expressa para atualizações do Windows 10|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#express-installation-files-support-for-windows-10-updates)|[Versão 1702](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates)|
 |Integração do Azure Active Directory|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#azure-active-directory-onboarding)|![Não foi adicionado](media/Red_X.gif)|
 |Alterar a configuração da autenticação multifator para registro de dispositivo|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#change-to-configuring-multi-factor-authentication-for-device-enrollment)|![Não foi adicionado](media/Red_X.gif)|
 |Conteúdo de cache prévio para sequências de tarefas e implantações |[Tech Preview 1611](capabilities-in-technical-preview-1611.md#pre-cache-content-for-available-deployments-and-task-sequences)|[Versão 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
 |Definições de configuração do Windows Defender|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#windows-defender-configuration-settings)|[Versão 1610](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |Solicitar sincronização de política no console do administrador|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#request-policy-sync-from-administrator-console)|[Versão 1610](/sccm/mdm/deploy-use/sync-intune-device)|
 |Suporte à função de segurança adicional para o nó de todos os dispositivos corporativos|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#additional-security-role-support)|[Versão 1610](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management#new-hybrid-features-in-november-2016)|
 |Acesso condicional para perfis de VPN do Windows 10|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#conditional-access-for-windows-10-vpn-profiles)|[Versão 1610](/sccm/protect/deploy-use/create-vpn-profiles#configure-the-authentication-method-for-the-vpn-profile)|
 |Filtrar por tamanho do conteúdo em regras de implantação automática|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|[Versão 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#filter-by-content-size-in-automatic-deployment-rules) |
 |Funcionalidade aprimorada para caixas de diálogo do software necessárias|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|[Versão 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Negar solicitações de aplicativos aprovadas anteriormente|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|[Versão 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Excluir clientes da atualização automática|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|[Versão 1610](/sccm/core/clients/manage/upgrade/exclude-clients-windows)|
 |Melhorias no Endpoint Protection|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|[Versão 1610](/sccm/protect/deploy-use/endpoint-antimalware-policies#cloud-protection-service)|
 |Aumento do número de dispositivos registrados|[Tech Preview 1609](/sccm/mdm/deploy-use/enable-platform-enrollment)|[Versão 1610](/sccm/mdm/deploy-use/enable-platform-enrollment)|
 |Configurações adicionais do Apple DEP|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|[Versão 1610](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)|
 |Aprimoramentos na integração da Windows Store para Empresas com o Configuration Manager|[Tech Preview 1609](capabilities-in-technical-preview-1609.md)|[Versão 1610](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |Novas configurações de conformidade para itens de configuração|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|[Versão 1610](/sccm/compliance/deploy-use/create-configuration-items)|
 |Integração com o Upgrade Analytics|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|[Versão 1610](/sccm/core/clients/manage/upgrade/upgrade-analytics)|
 |Tipos de conexão nativa para perfis híbridos de VPN do Windows 10|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![Não foi adicionado](media/Red_X.gif)|
 |Aprimoramentos para grupos de limites|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|[Versão 1610](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#BKMK_BoundaryGroups)|
 |Painel de gerenciamento de clientes do Office 365|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|[Versão 1610](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard)|
 |Implantar aplicativos do Office 365 em clientes|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#deploy-office-365-apps-to-clients)|[Versão 1702](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)|
 |Melhorias na conversão de BIOS para UEFI|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#BKMK_UEFIConversion)|[Versão 1610](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion)|
 |Gráficos de conformidade do Intune|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|[Versão 1610](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)|
 |Melhorias na etapa de sequência de tarefas Preparar o Cliente do ConfigMgr para Captura|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|[Versão 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)|
 |Melhorias ao Centro de Software|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|[Versão 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#general-improvements-to-software-center)|
 |Melhorias do Asset Intelligence|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|![Não foi adicionado](media/Red_X.gif)|
 |Tradução do teclado de controle remoto|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)|![Não foi adicionado](media/Red_X.gif)|
 |Melhorias na Política de atualização de edição do Windows 10|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|[Versão 1610](/sccm/compliance/deploy-use/upgrade-windows-version)|
 |Identidade visual personalizável para caixas de diálogo do Centro de Software|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-center-dialogs)|![Não foi adicionado](media/Red_X.gif)|  
 |Múltiplos pontos de gerenciamento para Gerenciamento de Dispositivo Móvel Local|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |Categorizar automaticamente dispositivos em coleções|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[Versão 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |Período de cortesia para imposição de implantações de atualizações de software e aplicativos obrigatórios|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|[Versão 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Uso do Configuration Manager como um instalador gerenciado com o Device Guard|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|![Não foi adicionado](media/Red_X.gif)|
 |Gateway de gerenciamento de nuvem (anteriormente conhecido como Serviço de Proxy de Nuvem)|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | [Versão 1610](/sccm/core/clients/manage/plan-cloud-management-gateway)|  
 |Gerenciamento do agente cliente do Office 365 no Configuration Manager|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#manage_o365) |[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#software-updates)|  
 |A variável de sequência de tarefas OSDPreserveDriveLetter foi preterida|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#osdpreservedriveletter) |[Versão 1606](/sccm/osd/understand/task-sequence-built-in-variables) |
 |Alterações no nó Atualizações e Manutenção|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#updatesandservicing)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#updates-and-servicing) |
 |VPN por aplicativo para dispositivos com Windows 10|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN)|[Versão 1606](/sccm/protect/deploy-use/create-vpn-profiles)|  
 |Melhorias na sequência de tarefas de Instalar Atualizações de Software|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_InstallSU)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |Melhorias na etapa de sequência de tarefas Preparar o Cliente do ConfigMgr para Captura |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PrepareConfigMgrClient)|[Versão 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) |
 |Período de cortesia para implantações de aplicativos obrigatórios |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Grace)|![Não foi adicionado](media/Red_X.gif)|  
 |Nova experiência para ações de dispositivo remoto |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Remote)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Aplicativos na Windows Store para Empresas |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_WSFB)|[Versão 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Melhorias gerais para aplicativos adquiridos por volume|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP2)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |EDP (Proteção de dados empresariais)|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Os usuários finais podem instalar aplicativos do Portal da Empresa |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|![Não foi adicionado](media/Red_X.gif)|  
 |Novas guias para Atualizações e Sistemas operacionais no Centro de Software|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_SW1)|[Versão 1606 ](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Realização de serviços em um grupo de servidores |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|[Versão 1606](/sccm/sum/deploy-use/service-a-server-group)|   
 |Suporte para o serviço Proteção Avançada contra Ameaças do Windows Defender |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ATP)|[Versão 1606](/sccm/protect/deploy-use/windows-defender-advanced-threat-protection)|  
 |Novas opções de reinício para clientes do Windows 10 após a instalação da atualização de software|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_RestartOptions)|[Versão 1606](/sccm/sum/plan-design/plan-for-software-updates#restart-options-for-Windows-10-clients-after-software-update-installation)|  
 |Atestado de integridade do dispositivo no local |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_DHA)|[Versão 1606](/sccm/core/servers/manage/health-attestation)|  
 |Pré-declarar dispositivos corporativos com número de série do iOS ou IMEI|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_IMEI)|[Versão 1606](/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id)|  
 |Gerenciar aplicativos adquiridos por volume da Windows Store para Empresas| [Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_WindowsVPP)|[Versão 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Melhorias no gerenciamento do Microsoft Passport for Work|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_PFW)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Opção para clientes alternarem para um novo ponto de atualização de software|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_switchsup)|[Versão 1606](/sccm/sum/plan-design/plan-for-software-updates#BKMK_ManuallySwitchSUPs)|  
 |Definições do cliente para gerenciar Configurações de Cache do Cliente e Cache de Mesmo Nível do cliente |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_peercache)|Configurações do cliente: [Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#administration)<br/>Cache de Pares: [Versão 1610](/sccm/core/plan-design/hierarchy/client-peer-cache)|  
 |Suporte ao Passport for Work como um KSP |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_passport)|[Versão 1606](/sccm/protect/deploy-use/create-certificate-profiles)|  
 |Atestado de integridade do dispositivo no local|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_onpremdha)|[Versão 1606](/sccm/core/servers/manage/health-attestation)|  
 |Configuração do SmartLock para dispositivos Android|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_Smart)|[Versão 1606](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference)|  
 <!--  TP 1603 Aged out of support and all features in Current Branch Builds:
 |Improvements to Software Center|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Improvements to remote control|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
-->
 Quando todos os recursos de uma versão de Technical Preview estão disponíveis na versão mínima com suporte do Branch Atual, os detalhes para essa versão de visualização são removidos desta tabela.


## <a name="see-also"></a>Consulte também  
[Novidades no System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Introduction to System Center Configuration Manager](../../core/understand/introduction.md)

