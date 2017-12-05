---
title: "Versões do Technical Preview"
titleSuffix: Configuration Manager
description: "Saiba mais sobre a versão do Technical Preview que permite a você testar novas funcionalidades e recursos no System Center Configuration Manager."
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: nab
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: "157"
author: erikje
ms.author: erikje
manager: angrobe
ms.openlocfilehash: 209beadba5b575afbd7d00cc52deb7a790d41c38
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Visualização técnica do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

**Bem-vindo ao System Center Configuration Manager Technical Preview**. Este tópico fornece detalhes sobre a versão de preview em evolução que introduz novas funcionalidades e recursos em que estamos trabalhando. Com cada versão de technical preview, são apresentados novos recursos que não estão incluídos no Branch Atual do System Center Configuration Manager assim que a versão do technical preview é disponibilizada. Esses recursos podem, eventualmente, ser incluídos em uma atualização da ramificação atual, mas antes de finalizarmos os recursos e os adicionarmos, queremos que você tenha a oportunidade de testá-los e fornecer comentários.  

 Como esta é uma technical preview, os detalhes e funcionalidades estão sujeitos a alterações.  

 Este tópico contém informações que se aplicam a todas as versões do Technical Preview e também lista cada nova funcionalidade (ou recurso) em conjunto com a versão do Technical Preview na qual a funcionalidade aparece pela primeira vez, como a versão 1710 de outubro de 2017. Os detalhes desses recursos são descritos em tópicos separados dedicados a versão de preview.  

 Para obter informações sobre o que há de novo do branch atual do Configuration Manager, consulte [Novidades no System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Requisitos e limitações do Technical Preview  

> [!IMPORTANT]     
>  O Technical Preview é licenciado somente para uso em ambiente de laboratório.  A Microsoft não pode fornecer serviços de suporte e alguns recursos podem não estar disponíveis para o software na versão de preview. Além disso, o software na versão de preview pode padrões diferentes ou reduzidos de segurança, privacidade, acessibilidade, disponibilidade e confiabilidade em comparação com o software fornecido comercialmente.  

 Para a maioria dos pré-requisitos do produto, use as informações contidas em [Configurações com suporte para o System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). As seguintes exceções se aplicam às versões de Technical Preview:  

-   Cada instalação permanece ativa durante 90 dias antes de se tornar inativa.  

-   O inglês é o único idioma com suporte.


-   Há suporte apenas para os seguintes sinalizadores de instalação (opções):  

    -   **/silent**  
    -   **/testdbupgrade**    


-   Por padrão, quando você usar a visualização técnica, o ponto de conexão de serviço será definido como o modo online quando é instalado e não dá suporte a uma alteração para o modo offline.

-   Quando aplicável, os requisitos ou limitações adicionais são incluídos com os detalhes de cada versão específica da Visualização Técnica  

-   Não há suporte para a migração de ou para esta compilação de visualização.  

-   Não há suporte para a atualização para esta compilação de visualização.  

-   Não há suporte para atualização para um build de produção (ramificação atual) deste build de preview. No entanto, quando as atualizações estão disponíveis para uma versão prévia, é possível localizá-las e instalá-las do nó **Atualizações e Manutenção** do console do Configuration Manager. Para obter um vídeo do processo de atualização no console, veja [Instalação dos pacotes de atualização do ConfigMgr](https://www.youtube.com/embed/KBd_EGFbUT8) no youtube.com.  
-   Há suporte apenas para um site primário autônomo. Não há suporte para um site de administração central, para vários sites primários ou para sites secundários.  

Há suporte para os seguintes produtos e tecnologias por esse branch do Configuration Manager. No entanto, sua inclusão neste conteúdo não implica uma extensão de suporte para um produto ou versão além do ciclo de vida de suporte individual desse produto. Os produtos além de seu ciclo de vida de suporte não têm suporte para uso com o Configuration Manager. Para obter mais informações sobre os Ciclos de vida de suporte da Microsoft, visite o site [Ciclo de Vida do Suporte da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) .  

-   Há suporte apenas para as seguintes versões do SQL Server:  

    -   SQL Server 2016 (sem Service Pack e posterior)
    -   SQL Server 2014 (com Service Pack 1 e posterior)
    -   SQL Server 2012 (com Service Pack 3 ou posterior)


-   O site dá suporte a até 10 clientes, que devem executar um dos seguintes:  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 8  
      -   Windows 7  

##  <a name="bkmk_install"></a> Instalar e atualizar a Visualização Técnica  
 O System Center Configuration Manager Technical Preview é diferente da versão atual do System Center Configuration Manager.  

 Para usar a technical preview, primeiro você deve instalar uma **versão de linha de base** do build da versão de technical preview. Depois de instalar uma versão de linha de base, use as **atualizações no console** para atualizar sua instalação para a versão de preview mais recente. Normalmente, as novas versões da Technical Preview são disponibilizadas todos os meses.

Cada versão de visualização conta com suporte até que três versões sucessivas estejam disponíveis. Ou seja, quando a versão 1708 for liberada, a versão 1704 não terá mais suporte, mas as versões 1705, 1706 e 1707 permanecerão com suporte. Quando uma linha de base ficar sem suporte (como a versão 1703), ainda haverá suporte para instalar um novo site do Technical Preview até que uma nova versão de linha de base esteja disponível, desde que, depois, você atualize a instalação para uma versão com suporte. Durante a atualização, se você não vir a versão mais recente disponível no console, atualize para a versão mais recente oferecida e, em seguida, repita esse processo até que você possa instalar a versão mais atual da visualização técnica.

> [!TIP]  
>  Quando você instala uma atualização da visualização técnica, atualiza a instalação da visualização para essa nova versão de visualização técnica.    Uma instalação de visualização técnica nunca tem a opção de atualizar para uma instalação de ramificação atual nem receber atualizações de versão da ramificação atual.  

**Versões de linha de base ativas do Technical Preview:**  
É possível instalar uma versão de linha de base em até 1 ano após seu lançamento. No entanto, quando você instala um novo site de visualização técnica, é recomendável usar a versão de linha de base mais recente disponível.
-  **Technical Preview 1711** – o Configuration Manager Technical Preview 1711 está disponível como uma atualização no console para o Configuration Manager Technical Preview e como uma nova versão de linha de base [disponível no site do TechNet Evaluation Center](http://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).
-  **Technical Preview 1703** – o Configuration Manager Technical Preview 1703 estava disponível como uma atualização no console para o Configuration Manager Technical Preview e como uma nova versão de linha de base. Se você estiver instalando uma nova linha de base, será recomendável usar a versão 1711.


##  <a name="BKMK_TPFeedback"></a> Enviando comentários  
 Adoraríamos receber seus comentários sobre nossas visualizações técnicas. Para enviar comentários sobre os recursos em cada visualização, clique no link de nosso formulário de comentários na página do [programa de comentários do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) no site do Microsoft Connect.  

 E se tiver sugestões sobre novos recursos que gostaria de ver, gostaríamos de saber também. Para enviar novas ideias e para votar nas ideias enviadas por outras pessoas, [visite nossa página de opinião do usuário](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Recursos fornecidos na visualização técnica mais recente  
Veja a seguir os recursos fornecidos com cada versão de technical preview do Configuration Manager.  Recursos que estão disponíveis a partir de uma versão de technical preview permanecem disponíveis nas versões posteriores. De forma semelhante, os recursos que foram adicionados à Versão do System Center Configuration Manager (branch atual) permanecem disponíveis em versões de technical preview posteriores.  Clique no conteúdo relativo a cada versão de preview saber mais sobre uma funcionalidade específica.  

 |Funcionalidade |Versão do Technical Preview |Versão do Branch Atual|  
 |----------------|---------------------|--------------------|
 |Melhorias para executar a etapa de sequência de tarefas <!-- 1261338 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |![Não foi adicionado](media/Red_X.gif)    |
 |Permitir a interação do usuário ao instalar um aplicativo <!-- 1356976 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |![Não foi adicionado](media/Red_X.gif)    |
 |Novas políticas de conformidade para o Windows 10 <!-- 1356976 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md#new-compliance-policy-options-for-windows-10) |![Não foi adicionado](media/Red_X.gif)    |


## <a name="capabilities-delivered-in-previous-technical-previews"></a>Recursos fornecidos em visualizações técnicas anteriores
 Quando todos os recursos de uma versão de Visualização Técnica estão disponíveis na versão mínima com suporte do Branch Atual, os detalhes para essa versão de visualização são removidos da tabela a seguir.  

 |Funcionalidade |Versão do Technical Preview |Versão do Branch Atual|  
 |----------------|---------------------|--------------------|
 |Telemetria do Windows 10 para a Integridade do Dispositivo do Windows Analytics<!--1356148 --> | [Tech Preview 1710](capabilities-in-technical-preview-1710.md#limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health) |![Não foi adicionado](media/Red_X.gif)    |
 |Melhorias nos ícones do Centro de Software <!-- 1356194 --> | [Tech Preview 1710](capabilities-in-technical-preview-1710.md#software-center-no-longer-distorts-icons-larger-than-250x250) |![Não foi adicionado](media/Red_X.gif)    |
 |Verificar a conformidade no Centro de Software para dispositivos cogerenciados<!-- 1356374 -->|[Tech Preview 1710](capabilities-in-technical-preview-1710.md#check-compliance-from-software-center-for-co-managed-devices)|![Não foi adicionado](media/Red_X.gif)    |
 |Suporte limitado para certificados CNG<!-- 1356191 -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md#limited-support-for-cng-certificates)|![Não foi adicionado](media/Red_X.gif)    |
 |Suporte para Exploit Guard <!--1355468 --> | [Tech Preview 1710](capabilities-in-technical-preview-1710.md#support-for-exploit-guard) |[Versão 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)    |
 |Descrições aprimoradas para reinicializações pendentes do computador<!-- 1356283  -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md)|[Versão 1710](/sccm/core/clients/manage/manage-clients)    |
 |Alterações na política do Device Guard <!-- 1355092  -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md)|[Versão 1710](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)    |
 |Configurar e implantar políticas de Proteção de Aplicativos do Windows Defender <!-- 1351960  -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md)|[Versão 1710](/sccm/protect/deploy-use/create-deploy-application-guard-policy)    |
 |Melhorias na implantação de scripts do PowerShell do Configuration Manager <!-- 1236459 -->| [Tech Preview 1710](capabilities-in-technical-preview-1710.md#improvements-for-deploying-powershell-scripts-from-configuration-manager) | [Versão 1710](/sccm/apps/deploy-use/create-deploy-scripts)

## <a name="capabilities-delivered-in-previous-technical-previews"></a>Recursos fornecidos em visualizações técnicas anteriores
 Quando todos os recursos de uma versão de Visualização Técnica estão disponíveis na versão mínima com suporte do Branch Atual, os detalhes para essa versão de visualização são removidos da tabela a seguir.  

 |Funcionalidade |Versão do Technical Preview |Versão do Branch Atual|  
 |----------------|---------------------|--------------------|
 |Melhoria da experiência do perfil de VPN no Console do Configuration Manager <!-- 1313282 --> | [Tech Preview 1709](capabilities-in-technical-preview-1709.md) |![Não foi adicionado](media/Red_X.gif)    |
 |Cogerenciamento para dispositivos Windows 10|[Tech Preview 1709](capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices)|[Versão 1710](/sccm/core/clients/manage/co-management-overview.md)|
 |Melhorias para especificar parâmetros de script ao implantar scripts do PowerShell do Configuration Manager <!-- 1236459 -->|[Tech Preview 1708](capabilities-in-technical-preview-1708.md#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager)|[Versão 1710](/sccm/apps/deploy-use/create-deploy-scripts)|
 |Informações de gerenciamento  <!-- 1353967 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#management-insights)|![Não foi adicionado](media/Red_X.gif)|
 |Reinicie os computadores do console do Configuration Manager <!-- 1356283 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#restart-computers-from-the-configuration-manager-console)|[Versão 1710](/sccm/core/clients/manage/manage-clients) |
 |Personalização do Centro de Software<!-- 1351224 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#software-center-customization)|![Não foi adicionado](media/Red_X.gif)|
|Suporte do Cache Par do Cliente para arquivos de instalação expressa para Windows 10 e Office 365|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365)|[Versão 1706](/sccm/core/plan-design/hierarchy/client-peer-cache#requirements-and-considerations-for-peer-cache)|
 |Painel do Surface Device|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#surface-device-dashboard)|![Não foi adicionado](media/Red_X.gif)|
 |Configurar e implantar políticas de Proteção de Aplicativos do Windows Defender|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#configure-and-deploy-windows-defender-application-guard-policies)|[Versão 1710](/sccm/protect/deploy-use/create-deploy-application-guard-policy)|
 |Adicionar parâmetros ao implantar scripts do PowerShell do Configuration Manager|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager)|[Versão 1710](/sccm/apps/deploy-use/create-deploy-scripts)|
 |Novas configurações de política de gerenciamento de aplicativo móvel|[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#new-mobile-application-management-policy-settings)|[Versão 1710](/sccm/mdm/deploy-use/protect-apps-using-mam-policies#step-3-create-an-application-management-policy)|
 |Grupos de limites aprimorados para os pontos de atualização de software|[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#improved-boundary-groups-for-software-update-points)|[Versão 1706](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)|
 |Alta disponibilidade da função de servidor do site|[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |![Não foi adicionado](media/Red_X.gif)|
 |Incluir relação de confiança para arquivos e pastas específicos em uma política de Proteção do Dispositivo|[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#include-trust-for-specific-files-and-folders-in-a-device-guard-policy)|[Versão 1706](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|
 |Ocultar o progresso da sequência de tarefas|[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#hide-task-sequence-progress)|![Não foi adicionado](media/Red_X.gif)|
 |Especificar um local de conteúdo diferente para instalar e desinstalar o conteúdo|[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#specify-a-different-content-location-for-install-content-and-uninstall-content)|[Versão 1706](/sccm/core/get-started/capabilities-in-technical-preview-1706#hide-task-sequence-progress)|
 |Aprimoramentos na acessibilidade |[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#accessibility-improvements)|[Versão 1706](/sccm/core/understand/accessibility-features)|
 |Suporte do Assistente dos Serviços do Azure para o Upgrade Readiness |[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#changes-to-the-azure-services-wizard-to-support-upgrade-readiness)|[Versão 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |Novas configurações de cliente para serviços de nuvem|[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#new-client-settings-for-cloud-services)|[Versão 1706](/sccm/core/clients/deploy/deploy-clients-cmg-azure)|
 |Criar e executar scripts do PowerShell do console do Configuration Manager|[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console)|[Versão 1710](/sccm/apps/deploy-use/create-deploy-scripts)|
 |Suporte de inicialização de rede PXE para IPv6 |[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|![Não foi adicionado](media/Red_X.gif)|
 |Gerenciar atualizações de driver do Microsoft Surface |[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#manage-microsoft-surface-driver-updates)|[Versão 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#manage-microsoft-surface-driver-updates)|
 |Configurar as políticas de adiamento do Windows Update for Business |[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#configure-windows-update-for-business-deferral-policies)|[Versão 1706](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies)|
 |Restrições de registro de iOS|[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#android-and-ios-enrollment-restrictions)|[Versão 1706](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac#configure-enrollment-restrictions)|
 |Restrições de registro de Android|[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#android-and-ios-enrollment-restrictions)|[Versão 1706](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-enrollment)|
 |Política de gerenciamento de aplicativos do Android for Work para copiar e colar|[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#android-for-work-application-management-policy-for-copy-paste)|[Versão 1706](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client#android-for-work-configuration-item-settings-reference)|
 |Novas definições de item de configuração do Windows|[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#new-windows-configuration-item-settings)|[Versão 1706](/sccm/mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |Novas regras de política de conformidade do dispositivo|[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#new-device-compliance-policy-rules)|[Versão 1706](/sccm/mdm/deploy-use/create-compliance-policy)|
 |Avaliação do Atestado de Integridade do Dispositivo para políticas de conformidade para acesso condicional|[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#device-health-attestation-assessment-for-compliance-policies-for-conditional-access)|![Não foi adicionado](media/Red_X.gif)|
 |Suporte para autoridades de certificação Entrust|[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#support-for-entrust-certification-authorities)|[Versão 1706](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)|
 |Suporte do Cisco (IPSec) para perfis de VPN do macOS|[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#cisco-ipsec-support-for-macos-vpn-profiles)|[Versão 1706](/sccm/protect/deploy-use/vpn-profiles)|
 |Novos recursos do Azure AD e gerenciamento de nuvem|[Visualização Técnica 1705](capabilities-in-technical-preview-1705.md#new-capabilities-for-azure-ad-and-cloud-management)|[Versão 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#azure-ad-integration-with-configuration-manager)|
 |Configurar e implantar políticas de Proteção de Aplicativos do Windows Defender|[Visualização Técnica 1705](capabilities-in-technical-preview-1705.md#configure-and-deploy-windows-defender-application-guard-policies)|[Versão 1710](/sccm/protect/deploy-use/create-deploy-application-guard-policy)|
 |Ferramenta de redefinição de atualização  |[Visualização Técnica 1705](capabilities-in-technical-preview-1705.md#update-reset-tool)|[Versão 1706](/sccm/core/servers/manage/update-reset-tool)|
 |Suporte de console com alto DPI  |[Visualização Técnica 1705](capabilities-in-technical-preview-1705.md#high-dpi-console-support)|[Versão 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#high-dpi-console-support)|
 |Aprimoramentos de cache de pares  |[Visualização Técnica 1705](capabilities-in-technical-preview-1705.md#peer-cache-improvements) |[Versão 1706](/sccm/core/plan-design/hierarchy/client-peer-cache#requirements-and-considerations-for-peer-cache)|
 |Aprimoramentos para Grupos de Disponibilidade AlwaysOn do SQL Server |[Visualização Técnica 1705](capabilities-in-technical-preview-1705.md#improvements-for-sql-server-always-on-availability-groups) |[Versão 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#improvements-for-sql-server-always-on-availability-groups)|
 |Notificações de usuário aprimoradas para atualizações do Office 365|[Visualização Técnica 1705](capabilities-in-technical-preview-1705.md#improved-user-notifications-for-office-365-updates) |[Versão 1706](/sccm/sum/deploy-use/manage-office-365-proplus-updates#restart-behavior-and-client-notifications-for-office-365-updates)|
 |Use o Assistente para Serviços do Azure para configurar uma conexão para OMS|[Visualização Técnica 1705](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) |[Versão 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |Configurar aplicativos do Android com as políticas de configuração de aplicativo  |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#configure-android-apps-with-app-configuration-policies)|![Não foi adicionado](media/Red_X.gif)|
 |O inventário de hardware coleta informações de Inicialização Segura |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#hardware-inventory-collects-secure-boot-information)|[Versão 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#hardware-inventory-collects-secure-boot-information)|
 |Adicionar sequências de tarefas filho a uma sequência de tarefas|[Tech Preview 1704](capabilities-in-technical-preview-1704.md#add-child-task-sequences-to-a-task-sequence)|![Não foi adicionado](media/Red_X.gif)|
 |Recarregue as imagens de inicialização com a versão atual do Windows PE |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#reload-boot-images-with-current-windows-pe-version)|[Versão 1706](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image)|
 |Melhorias na implantação do sistema operacional...<!-- This item does not track to be added to the Current Branch. It is covered by various other incremental work. --> |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#improvements-to-operating-system-deployment)|![Não foi adicionado](media/Red_X.gif)|
 |Implantar aplicativos iOS adquiridos por volume em coleções de dispositivos|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#deploy-volume-purchased-ios-apps-to-device-collections)|[Versão 1702](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)|
 |Links diretos para aplicativos no Centro de Software|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#direct-links-to-applications-in-software-center)|[Versão 1706](/sccm/apps/deploy-use/share-applications)
 |Certificados PFX para computadores cliente Windows do Configuration Manager|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#pfx-certificates-for-configuration-manager-windows-client-computers)|[Versão 1706](/sccm/protect/deploy-use/create-certificate-profiles)|
 |Assistente de Configuração de Serviços do Azure|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#configure-azure-services-wizard)|[Versão 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |Converta BIOS em UEFI em uma sequência de tarefas de atualização do sistema operacional| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#convert-from-bios-to-uefi-during-an-in-place-upgrade) |[Versão 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)|
 |Grupos de sequências de tarefas recolhíveis| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#collapsible-task-sequence-groups) |[Versão 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#collapsible-task-sequence-groups)|
 |Configurações do cliente para configurar o Windows Analytics para Preparação para Atualização | [Tech Preview 1703](capabilities-in-technical-preview-1703.md#client-settings-to-configure-windows-analytics-for-upgrade-readiness) |[Versão 1706](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics)|
 |Novas configurações de conformidade para dispositivos iOS|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#new-compliance-settings-for-ios-devices)|[Versão 1702](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)|
 |Criar certificados PFX com suporte a S/MIME|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#create-pfx-certificates-with-s-mime-support)|[Versão 1706](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)|
 |Verificar se há arquivos executáveis antes de instalar um aplicativo|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#check-for-running-executable-files-before-installing-an-application)|[Versão 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Enviar comentários do console do Configuration Manager | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#send-feedback-from-the-configuration-manager-console)    |[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#send-feedback-from-the-configuration-managercconsole)  |
 |Alterações em Atualizações e Manutenção  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#changes-for-updates-and-servicing)  |[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#changes-for-updates-and-servicing) |
 |Aprimoramentos de cache de pares  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#peer-cache-improvements) |[Versão 1702](/sccm/core/plan-design/hierarchy/client-peer-cache)|
 |Usar o Azure Active Directory <!-- This item does not track to be added to the Current Branch. It is covered by various other incremental work. --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |![Não foi adicionado](media/Red_X.gif)|
 |Aprimoramentos na política de conformidade de dispositivo de acesso condicional | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#conditional-access-device-compliance-policy-improvements) |[Versão 1702](/sccm/mdm/deploy-use/create-compliance-policy)|
 |Alerta de versão do cliente de antimalware | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert) |[Versão 1702](/sccm/protect/deploy-use/endpoint-configure-alerts?branch=live#alert-for-outdated-malware-client)|
 |Avaliação de conformidade para atualizações do Windows Update for Business | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |![Não foi adicionado](media/Red_X.gif)|
 |Aprimoramentos nas configurações e mensagens de notificação do Centro de Software para sequências de tarefas de alto impacto|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert)|[Versão 1702](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)|
 |Suporte do Android for Work| [Tech Preview 1702](capabilities-in-technical-preview-1702.md#android-for-work-support) |[Versão 1702](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-for-work-enrollment)|
 |Aprimoramentos de grupos de limites para os pontos de atualização de software | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#boundary-groups-improvements-for-software-update-points)    |[Versão 1702](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)  |
 |O inventário de hardware coleta informações de UEFI | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#hardware-inventory-collects-uefi-information)|[Versão 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#hardware-inventory-collects-uefi-information) |
 |Melhorias na implantação de sistema operacional| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#improvements-to-operating-system-deployment)|[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment) |
 |Hospede as atualizações de software nos pontos de distribuição baseados em nuvem| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#host-software-updates-on-cloud-based-distribution-points)|[Versão 1702](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#plan-to-use-a-cloud-based-distribution-point) |
 |Validar dados de atestado de integridade do dispositivo por meio de pontos de gerenciamento| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#validate-device-health-attestation-data-via-management-points)| [Versão 1702](/sccm/core/servers/manage/health-attestation) |
 |Conector do OMS para a nuvem Microsoft Azure Governamental |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#use-the-oms-connector-for-microsoft-azure-government-cloud) |[Versão 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig) |
 |As versões do Android e iOS não precisam mais ser direcionadas nos assistentes de criação |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |
 |Acesso a dados do ponto de extremidade OData |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|![Não foi adicionado](media/Red_X.gif)|
 |Ponto de Serviço do Data Warehouse |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#the-data-warehouse-service-point)|[Versão 1702](/sccm/core/servers/manage/data-warehouse)|
 |Ferramenta de limpeza da biblioteca de conteúdo |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#content-library-cleanup-tool)|[Versão 1702](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) |
 |Melhorias da pesquisa no console |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#improvements-for-in-console-search)|[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-for-in-console-search)|
 |Impedir a instalação de um aplicativo se estiver executando um programa especificado|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#prevent-installation-of-an-application-if-a-specified-program-is-running)|[Versão 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Nova notificação do Windows Hello para Empresas para usuários finais|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#new-windows-hello-for-business-notification-for-end-users)|[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#new-windows-hello-for-business-notification-for-end-users)|
 |Suporte da Windows Store para Empresas no Configuration Manager|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#windows-store-for-business-support-in-configuration-manager)|[Versão 1702](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |Retornar à página anterior quando uma sequência de tarefas falhar|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#return-to-previous-page-when-a-task-sequence-fails)|[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment)|
 |Suporte dos arquivos de instalação expressa para atualizações do Windows 10|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#express-installation-files-support-for-windows-10-updates)|[Versão 1702](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates)|
 |Integração do Azure Active Directory|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#azure-active-directory-onboarding)|[Versão 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
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


 <!--  TP 1608 and earlier have aged out of support. Features from these previews are either in the minimum supported Current Branch version, or are not scheduled for inclusion.
 |Improvements to the Prepare ConfigMgr Client for Capture task sequence step|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|[Version 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)|
 |Improvements to Software Center|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|[Version 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#general-improvements-to-software-center)|
 |Improvements to Asset Intelligence|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|N/A|
 |Remote control keyboard translation|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)|[Version 1702](/sccm/core/clients/manage/remote-control/configuring-remote-control#enable-keyboard-translation)|
 |Improvements to the Windows 10 Edition Upgrade Policy|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|[Version 1610](/sccm/compliance/deploy-use/upgrade-windows-version)|
 |Customizable Branding for Software Center Dialogs|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-center-dialogs)|[Version 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#customizable-branding-for-software-center-dialogs)|  
 |Multiple device management points for On-premises Mobile Device Management|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |Automatically categorize devices into collections|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[Version 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |Enforcement grace period for required application and software update deployments|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|[Version 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Using Configuration Manager as a Managed Installer with Device Guard|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|[Version 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|
 |Cloud management gateway (formerly Cloud Proxy Service)|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | [Version 1610](/sccm/core/clients/manage/plan-cloud-management-gateway)|  
 |Manage the Office 365 client agent in Configuration Manager|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#manage_o365) |[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#software-updates)|  
 |The OSDPreserveDriveLetter task sequence variable has been deprecated|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#osdpreservedriveletter) |[Version 1606](/sccm/osd/understand/task-sequence-built-in-variables) |
 |Changes for the Updates and Servicing Node|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#updatesandservicing)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#updates-and-servicing) |
 |Per-app VPN for Windows 10 devices|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN)|[Version 1606](/sccm/protect/deploy-use/create-vpn-profiles)|  
 |Improvements to the Install software updates task sequence|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_InstallSU)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |Improvements to the Prepare ConfigMgr Client for Capture task sequence step |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PrepareConfigMgrClient)|[Version 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) |
 |Grace period for required application deployments |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Grace)|N/A|  
 |New experience for remote device actions |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Remote)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Windows Store for Business apps |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_WSFB)|[Version 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |General improvements for volume-purchased apps|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP2)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Enterprise Data Protection (EDP)|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |End users can install apps from the Company Portal |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|N/A|  
 |New tabs for Updates and Operating Systems in Software Center|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_SW1)|[Version 1606 ](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Service a server group |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|[Version 1606](/sccm/sum/deploy-use/service-a-server-group)|   
 |Support for Windows Defender Advanced Threat Protection service |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ATP)|[Version 1606](/sccm/protect/deploy-use/windows-defender-advanced-threat-protection)|  
 |New restart options for Windows 10 clients after software update installation|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_RestartOptions)|[Version 1606](/sccm/sum/plan-design/plan-for-software-updates#restart-options-for-Windows-10-clients-after-software-update-installation)|  
 |On-premises Device Health Attestation |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_DHA)|[Version 1606](/sccm/core/servers/manage/health-attestation)|  
 |Pre-declare corporate-owned devices with IMEI or iOS serial number|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_IMEI)|[Version 1606](/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id)|  
 |Manage volume-purchased apps from the Windows Store for Business| [Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_WindowsVPP)|[Version 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Improvements to Microsoft Passport for Work management|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_PFW)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Option for clients to switch to a new software update point|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_switchsup)|[Version 1606](/sccm/sum/plan-design/plan-for-software-updates#BKMK_ManuallySwitchSUPs)|  
 |Client settings to manage Client Cache Settings and client Peer Cache |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_peercache)|Client Settings: [Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#administration)<br/>Peer Cache: [Version 1610](/sccm/core/plan-design/hierarchy/client-peer-cache)|  
 |Support for Passport for Work as a KSP |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_passport)|[Version 1606](/sccm/protect/deploy-use/create-certificate-profiles)|  
 |On-premises Device Health Attestation|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_onpremdha)|[Version 1606](/sccm/core/servers/manage/health-attestation)|  
 |SmartLock setting for Android devices|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_Smart)|[Version 1606](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference)|  
 |Improvements to Software Center|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Improvements to remote control|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
-->



## <a name="see-also"></a>Consulte também  
[Novidades no System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Introduction to System Center Configuration Manager](../../core/understand/introduction.md)
