---
title: Technical Preview do System Center Configuration Manager | Microsoft Docs
description: "Saiba mais sobre a versão do Technical Preview que permite a você testar novas funcionalidades e recursos no System Center Configuration Manager."
ms.custom: na
ms.date: 12/16/2016
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
ms.sourcegitcommit: 4b1b925a50d08d90e4e1250967e19c0bc5aac4d3
ms.openlocfilehash: faef3537eed740a6177f00991615c978659e06c7


---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Visualização técnica do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

**Bem-vindo ao System Center Configuration Manager Technical Preview**. Este tópico fornece detalhes sobre a versão de preview em evolução que introduz novas funcionalidades e recursos em que estamos trabalhando. Com cada versão de technical preview, são apresentados novos recursos que não estão incluídos no Branch Atual do System Center Configuration Manager assim que a versão do technical preview é disponibilizada. Esses recursos podem, eventualmente, ser incluídos em uma atualização da ramificação atual, mas antes de finalizarmos os recursos e os adicionarmos, queremos que você tenha a oportunidade de testá-los e fornecer comentários.  

 Como esta é uma technical preview, os detalhes e funcionalidades estão sujeitos a alterações.  

 Este tópico contém informações que se aplicam a todas as versões Technical Preview e também lista cada nova funcionalidade (ou recurso) em conjunto com a versão Technical Preview em que o recurso aparece primeiro, como a versão 1512 de dezembro de 2015. Os detalhes desses recursos são descritos em tópicos separados dedicados a versão de preview.  

 Para obter informações sobre o que há de novo do branch atual do Configuration Manager, consulte [Novidades no System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="a-namebkmkreqsa-requirements-and-limitations-for-the-technical-preview"></a><a name="bkmk_reqs"></a> Requisitos e limitações do Technical Preview  

> [!IMPORTANT]  
>  O Technical Preview é licenciado somente para uso em ambiente de laboratório.  A Microsoft não pode fornecer serviços de suporte e alguns recursos podem não estar disponíveis para o software na versão de preview. Além disso, o software na versão de preview pode padrões diferentes ou reduzidos de segurança, privacidade, acessibilidade, disponibilidade e confiabilidade em comparação com o software fornecido comercialmente.  

 Para a maioria dos pré-requisitos do produto, use as informações contidas em [Configurações com suporte para o System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). As seguintes exceções se aplicam às versões de Technical Preview:  

-   Cada instalação permanece ativa durante 90 dias antes de se tornar inativa.  

-   O inglês é o único idioma com suporte.  

-   Há suporte apenas para um site primário autônomo. Não há suporte para um site de administração central, para vários sites primários ou para sites secundários.  

-   Há suporte apenas para as seguintes versões do SQL Server:  

    -   SQL Server 2012 com atualização cumulativa 2 ou posterior  

    -   SQL Server 2014  

-   O site dá suporte a até 10 clientes, que devem executar um dos seguintes:  

    -   Windows 7  

    -   Windows 8  

    -   Windows 8.1  

    -   Windows 10  

-   Há suporte apenas para os seguintes sinalizadores de instalação (opções):  

    -   **/silent**  

    -   **/testdbupgrade**  

-   Quando aplicável, os requisitos ou limitações adicionais são incluídos com os detalhes de cada versão específica da Visualização Técnica  

-   Não há suporte para a migração de ou para esta compilação de visualização.  

-   Não há suporte para a atualização para esta compilação de visualização.  

-   Não há suporte para atualização para um build de produção (ramificação atual) deste build de preview. No entanto, quando as atualizações estão disponíveis para uma versão prévia, é possível localizá-las e instalá-las do nó **Atualizações e Manutenção** do console do Configuration Manager. Para obter um vídeo do processo de atualização no console, veja [Instalação dos pacotes de atualização do ConfigMgr](https://www.youtube.com/embed/KBd_EGFbUT8) no youtube.com.  

##  <a name="a-namebkmkinstalla-install-and-update-the-technical-preview"></a><a name="bkmk_install"></a> Instalar e atualizar a Visualização Técnica  
 O System Center Configuration Manager Technical Preview é diferente da versão atual do System Center Configuration Manager.  

 Para usar a technical preview, primeiro você deve instalar uma **versão de linha de base** do build da versão de technical preview. Depois de instalar uma versão de linha de base, use as **atualizações no console** para atualizar sua instalação para a versão de preview mais recente.     Normalmente, as novas versões da Technical Preview são disponibilizadas todos os meses.  

> [!TIP]  
>  Quando você instala uma atualização da visualização técnica, atualiza a instalação da visualização para essa nova versão de visualização técnica.    Uma instalação de visualização técnica nunca tem a opção de atualizar para uma instalação de ramificação atual nem receber atualizações de versão da ramificação atual.  

 **Versões de linha de base ativas do Technical Preview:**  
 É possível instalar uma versão de linha de base em até 1 ano após seu lançamento.

-   **Technical Preview 1610** – o Configuration Manager Technical Preview 1610 está disponível tanto como atualização no console para o Configuration Manager Technical Preview quanto como uma nova versão de linha de base no site do [Centro de Avaliação TechNet](https://www.microsoft.com/en-us/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

-   **Technical Preview 1603** como parte do **System Center Technical Preview 5** – o Configuration Manager Technical Preview 1603 está disponível como uma atualização no console para o Configuration Manager Technical Preview e como uma nova versão de linha de base incluída no System Center Technical Preview 5.    Somente a versão incluída no System Center Technical Preview 5 pode ser usada para uma instalação de linha de base.  

     Sobre a versão de linha de base do [Configuration Manager Technical Preview do System Center Technical Preview 5](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview):  

    -   Tanto a Instalação quanto o console do Configuration Manager listam a versão como o System Center Configuration Manager Technical Preview 1603.  

    -   Essa versão de linha de base funciona como o Configuration Manager Technical Preview 1603, incluindo suporte para atualizações no console.  


##  <a name="a-namebkmktpfeedbacka-providing-feedback"></a><a name="BKMK_TPFeedback"></a> Enviando comentários  
 Adoraríamos receber seus comentários sobre nossas visualizações técnicas. Para enviar comentários sobre os recursos em cada visualização, clique no link de nosso formulário de comentários na página do [programa de comentários do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) no site do Microsoft Connect.  

 E se tiver sugestões sobre novos recursos que gostaria de ver, gostaríamos de saber também. Para enviar novas ideias e para votar nas ideias enviadas por outras pessoas, [visite nossa página de opinião do usuário](http://configurationmanager.uservoice.com).  

##  <a name="a-namebdmktpknownissuesa-general-changes-introduced-in-technical-previews"></a><a name="bdmk_tpknownissues"></a> Alterações gerais introduzidas nas Technical Previews  

-   **Technical Preview 1603:**  

    -   Começando na Technical Preview 1603, você pode configurar implantações de atualizações de software para que os clientes executem uma verificação de conformidade de atualizações de software imediatamente depois que eles instalam atualizações de software e reiniciam. Isso permite que os clientes verifiquem atualizações de software adicionais que se tornam aplicáveis depois que eles são reiniciados e as instalem (e se tornem compatíveis) durante a mesma janela de manutenção.  

         Para configurar isso em uma implantação, na página **Experiência do Usuário** do Assistente para Implantar Atualizações de Software, escolha a opção **Se alguma atualização nessa implantação exigir uma reinicialização do sistema, executar o ciclo de avaliação da implantação de atualizações após a reinicialização**.  

    -   Começando na Technical Preview 1603, o comportamento da variável de sequência de tarefas SMSTSRebootDelay mudou. A variável SMSTSRebootDelay especifica quantos segundos aguardar antes de o computador ser reiniciado. O gerenciador da sequência de tarefas exibirá uma caixa de diálogo de notificação antes da reinicialização se essa variável não for definida como 0.  
        Quando você configura um valor para essa variável, esse valor será mantido até que você configure um novo valor. O atraso para todas as reinicializações subsequentes do computador terá o mesmo valor. No Configuration Manager versão 1602 e anteriores, a variável é redefinida para o valor padrão (30 segundos) depois que o computador é reiniciado.   Para obter mais informações, consulte [Task sequence built-in variables in System Center Configuration Manager](../../osd/understand/task-sequence-built-in-variables.md).

-   **Technical Preview 1602:** a partir da Technical Preview 1602, é possível fazer uma atualização in-loco do sistema operacional de um servidor do sistema de sites que executa o Windows 2008 Server R2 para o Windows 2012 Server R2.  Ao usar os procedimentos de atualização do Windows Server 2012 R2, não é necessário executar uma restauração do servidor do site do Configuration Manager após a atualização.  Para obter os procedimentos de atualização, veja [Opções de atualização para o Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx).  

    > [!WARNING]  
    >  Antes de atualizar para o Windows Server 2012 R2, **você deve desinstalar o WSUS 3.2** do servidor.  
    >   
    >  Para obter informações sobre esta etapa crítica, confira a seção Funcionalidade nova e alterada em [Visão geral do Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx) na documentação do Windows Server.  

-   **Technical Preview 1601:** por padrão, o ponto de conexão de serviço é definido como o modo online quando é instalado e não dá suporte a uma alteração para o modo offline.  





##  <a name="a-namebkmktpcapsa-capabilities-delivered-in-technical-previews"></a><a name="bkmk_tpCaps"></a> Recursos fornecidos na visualização técnica  
 Veja a seguir os recursos fornecidos com cada versão de technical preview do Configuration Manager.  Recursos que estão disponíveis a partir de uma versão de technical preview permanecem disponíveis nas versões posteriores. De forma semelhante, os recursos que foram adicionados à Versão do System Center Configuration Manager (branch atual) permanecem disponíveis em versões de technical preview posteriores.  Clique no conteúdo relativo a cada versão de preview saber mais sobre uma funcionalidade específica.  

 |Funcionalidade|Versão do Technical Preview|Versão do Branch Atual|  
 |----------------|---------------------|--------------------|
 |Acesso a dados do ponto de extremidade OData |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|![Não foi adicionado](media/Red_X.gif)|
 |Ponto de Serviço do Data Warehouse |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#the-data-warehouse-service-point)|![Não foi adicionado](media/Red_X.gif)|
 |Ferramenta de limpeza da biblioteca de conteúdo |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#content-library-cleanup-tool)|![Não foi adicionado](media/Red_X.gif)|
 |Melhorias da pesquisa no console |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#improvements-for-in-console-search)|![Não foi adicionado](media/Red_X.gif)|
 |Impedir a instalação de um aplicativo se estiver executando um programa especificado|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#prevent-installation-of-an-application-if-a-specified-program-is-running)|![Não foi adicionado](media/Red_X.gif)|
 |Nova notificação do Windows Hello para Empresas para usuários finais|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#new-windows-hello-for-business-notification-for-end-users)|![Não foi adicionado](media/Red_X.gif)|
 |Suporte da Windows Store para Empresas no Configuration Manager|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#windows-store-for-business-support-in-configuration-manager)|![Não foi adicionado](media/Red_X.gif)|
 |Retornar à página anterior quando uma sequência de tarefas falhar|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#return-to-previous-page-when-a-task-sequence-fails)|![Não foi adicionado](media/Red_X.gif)|
 |Suporte dos arquivos de instalação expressa para atualizações do Windows 10|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#express-installation-files-support-for-windows-10-updates)|![Não foi adicionado](media/Red_X.gif)|
 |Integração do Azure Active Directory|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#azure-active-directory-onboarding)|![Não foi adicionado](media/Red_X.gif)|
|Alterar a configuração da autenticação multifator para registro de dispositivo|[Tech Preview 1612](capabilities-in-technical-preview-1612.md#change-to-configuring-multi-factor-authentication-for-device-enrollment)|![Não foi adicionado](media/Red_X.gif)|
|Conteúdo de cache prévio para sequências de tarefas e implantações |[Tech Preview 1611](capabilities-in-technical-preview-1611.md#pre-cache-content-for-available-deployments-and-task-sequences)|![Não foi adicionado](media/Red_X.gif)|
 |Definições de configuração do Windows Defender|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#windows-defender-configuration-settings)|[Versão 1610](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |Solicitar sincronização de política no console do administrador|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#request-policy-sync-from-administrator-console)|[Versão 1610](/sccm/mdm/deploy-use/sync-intune-device)|
 |Suporte à função de segurança adicional para o nó de todos os dispositivos corporativos|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#additional-security-role-support)|[Versão 1610](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management#new-hybrid-features-in-november-2016)|
 |Acesso condicional para perfis de VPN do Windows 10|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#conditional-access-for-windows-10-vpn-profiles)|[Versão 1610](/sccm/protect/deploy-use/create-vpn-profiles#configure-the-authentication-method-for-the-vpn-profile)|
 |Filtrar por tamanho do conteúdo em regras de implantação automática|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|[Versão 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#filter-by-content-size-in-automatic-deployment-rules) |
 |Funcionalidade aprimorada para caixas de diálogo do software necessárias|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|[Versão 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Negar solicitações de aplicativos aprovadas anteriormente|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|[Versão 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Excluir clientes da atualização automática|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|[Versão 1610](/sccm/core/clients/manage/upgrade/exclude-clients-windows)|
 |Melhorias no Endpoint Protection|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|![Não foi adicionado](media/Red_X.gif)|
 |Aumento do número de dispositivos registrados|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#increased-number-of-enrolled-devices)|![Não foi adicionado](media/Red_X.gif)|
 |Configurações adicionais do Apple DEP|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|[Versão 1610](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)|
 |Aprimoramentos na integração da Windows Store para Empresas com o Configuration Manager|[Tech Preview 1609](capabilities-in-technical-preview-1609.md)|[Versão 1610](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |Novas configurações de conformidade para itens de configuração|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|[Versão 1610](/sccm/compliance/deploy-use/create-configuration-items)|
 |Integração com o Upgrade Analytics|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|[Versão 1610](/sccm/core/clients/manage/upgrade/upgrade-analytics)|
 |Tipos de conexão nativa para perfis híbridos de VPN do Windows 10|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![Não foi adicionado](media/Red_X.gif)|
 |Aprimoramentos para grupos de limites|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|[Versão 1610](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#BKMK_BoundaryGroups)|
 |Painel de gerenciamento de clientes do Office 365|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|[Versão 1610](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard)|
 |Implantar aplicativos do Office 365 em clientes|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#deploy-office-365-apps-to-clients)|![Não foi adicionado](media/Red_X.gif)|
 |Melhorias na conversão de BIOS para UEFI|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#BKMK_UEFIConversion)|[Versão 1610](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion)|
 |Gráficos de conformidade do Intune|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|[Versão 1610](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)|
 |Melhorias na etapa de sequência de tarefas Preparar o Cliente do ConfigMgr para Captura|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|[Versão 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)|
 |Melhorias ao Centro de Software|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|[1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#general-improvements-to-software-center)|
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
 |Melhorias ao Centro de Software|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Melhorias no controle remoto|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |Personalizar o tamanho do bloco e da janela do RamDisk TFTP nos pontos de distribuição habilitados para PXE|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |Melhorias ao gerenciamento de dispositivo móvel|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_MDM)|[Versão 1602](/sccm/mdm/deploy-use/manage-ios-activation-lock) |  
 |Melhorias no Centro de Software na versão 1602|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_SC1601)| [Versão 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#client-management)|  
 |Melhorias ao Serviço do Windows 10|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_Win10Servicing)|[Versão 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#operating-system-deployment) |  
 |Melhorias para a integração do Microsoft Intune|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_hybrid1)|[Versão 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#conditional-access)|  
 |Status online do cliente|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_clientStatus)|[Versão 1602](/sccm/core/clients/manage/monitor-clients)|
 |Aprimoramentos no gerenciamento de aplicativos|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_appmgmt1601)|[Versão 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#application-management)|  
 |Aprimoramentos para configurações de conformidade|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_compliance1601)|[Versão 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#compliance-settings)|  
 |Atestado de integridade do dispositivo|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_devicehealth)|[Versão 1602](/sccm/core/servers/manage/health-attestation))|
 |No console de monitoramento para os termos e condições|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_viewterms)|[Versão 1602](/sccm/mdm/deploy-use/terms-and-conditions)|  
 |Aprimoramentos nas configurações de política do Endpoint Protection|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_EPpolicy)|[Versão 1602](/sccm/protect/deploy-use/endpoint-antimalware-policies)|  
 |Integração com o Windows Update for Business no Windows 10|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_WUfB)|[Versão 1602](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)|  
 |Gerenciando a atualização do cliente do Office 365 ProPlus por meio do System Center Configuration Manager|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_Office365ProPlus)|[Versão 1602](/sccm/sum/deploy-use/manage-office-365-proplus-updates)|  
 |Suporte para o SQL Server AlwaysOn para bancos de dados altamente disponíveis|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_AlwasyOn)|[Versão 1602](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)|  
 |Atenda a um cluster de servidores|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_ClusterServerUpdates)|[Versão 1606](/sccm/sum/deploy-use/service-a-server-group)|  
## <a name="see-also"></a>Consulte também  
[Novidades no System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Introduction to System Center Configuration Manager](../../core/understand/introduction.md)



<!--HONumber=Dec16_HO3-->


