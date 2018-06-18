---
title: Versões do Technical Preview
titleSuffix: Configuration Manager
description: Saiba mais sobre a versão do Technical Preview para fazer o test drive das novas funcionalidades do System Center Configuration Manager.
ms.date: 06/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b7372e0b894e93a5a8ec15e54bfeb09e18be6c32
ms.sourcegitcommit: 10a6e3444da631786e9b1729e79a5b728d54ca72
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34753987"
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Visualização técnica do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

**Bem-vindo ao System Center Configuration Manager Technical Preview**. Este artigo fornece detalhes sobre a versão de visualização em evolução que introduz novas funcionalidades e recursos nos quais estamos trabalhando. Cada versão do technical preview introduz novos recursos que não estão incluídos no branch atual do Configuration Manager no momento em que a versão do technical preview é disponibilizada. Esses recursos podem, eventualmente, ser incluídos em uma atualização da ramificação atual, mas antes de finalizarmos os recursos e os adicionarmos, queremos que você tenha a oportunidade de testá-los e fornecer comentários.  

 Como esta versão é technical preview, os detalhes e funcionalidades estão sujeitos a alterações.  

 Este artigo contém informações que se aplicam a todas as versões do Technical Preview. Ele também lista cada nova funcionalidade (ou recurso) juntamente com a visualização técnica em que a funcionalidade aparece pela primeira vez, como versão 1806 de junho de 2018. Essas funcionalidades são detalhadas em tópicos separados, dedicados a cada versão de visualização.  

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
-  **Visualização técnica 1806** – a visualização técnica 1806 do Configuration Manager está disponível como uma atualização no console e como uma nova versão de linha de base. Baixe as versões de linha de base [no Centro de Avaliação do TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).


##  <a name="BKMK_TPFeedback"></a> Enviando comentários  
 Adoramos ouvir seus comentários sobre as funcionalidades de nossos technical previews. Para obter mais informações, consulte [Comentários sobre o produto](../understand/find-help.md#product-feedback).

Caso tenha sugestões sobre novos recursos que gostaria de ver, gostaríamos de saber também. Para enviar novas ideias e para votar nas ideias enviadas por outras pessoas, [visite nossa página de opinião do usuário](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Recursos fornecidos na visualização técnica mais recente  
Veja a seguir as funcionalidades fornecidas com a versão de technical preview mais recente do Configuration Manager.  Funcionalidades que estavam disponíveis em uma versão anterior do technical preview permanecem disponíveis em versões posteriores. De forma semelhante, as funcionalidades que foram adicionadas ao branch atual do Configuration Manager permanecem disponíveis em versões de technical preview.  Clique no conteúdo relativo a cada versão de preview saber mais sobre uma funcionalidade específica.  

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1806"></a>Visualização técnica versão 1806
- [Atualizações de software de terceiros](capabilities-in-technical-preview-1806.md#bkmk-3pupdate) <!--1352101-->
- [Definir as configurações do Windows Defender SmartScreen para o Microsoft Edge](capabilities-in-technical-preview-1806.md#configure-windows-defender-smartscreen-settings-for-microsoft-edge) <!--1353701-->
- [Sincronizar a política de MDM do Microsoft Intune para um dispositivo cogerenciado](capabilities-in-technical-preview-1806.md#sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device) <!--1357377-->
- [Fazer a transição da carga de trabalho do Office 365 para o Intune usando o cogerenciamento](capabilities-in-technical-preview-1806.md#transition-office-365-workload-to-intune-using-co-management) <!--1357841-->
- [Gerenciador de Conversão de Pacote](capabilities-in-technical-preview-1806.md#package-conversion-manager) <!--1357861-->
- [Implantar atualizações de software sem conteúdo](capabilities-in-technical-preview-1806.md#deploy-software-updates-without-content) <!--1357933-->
- [Integração da Ferramenta de Personalização do Office com o Instalador do Office 365](capabilities-in-technical-preview-1806.md#office-customization-tool-integration-with-the-office-365-installer) <!--1358149-->
- [Melhorias no gateway de gerenciamento de nuvem](capabilities-in-technical-preview-1806.md#improvements-to-cloud-management-gateway) <!--1358215,1358651,503899--> 
- [Melhorias nas comunicações seguras com o cliente](capabilities-in-technical-preview-1806.md#improvements-to-secure-client-communications) <!--1358278,1358279-->
- [Melhorias na infraestrutura do Centro de Software](capabilities-in-technical-preview-1806.md#software-center-infrastructure-improvements) <!--1358309-->
- [Provisionar pacotes de aplicativos do Windows para todos os usuários em um dispositivo](capabilities-in-technical-preview-1806.md#provision-windows-app-packages-for-all-users-on-a-device) <!--1358310-->
- [Melhorias no painel do Surface](capabilities-in-technical-preview-1806.md#improvements-to-the-surface-dashboard) <!--1358654-->
- [Revisão da unidade padrão do inventário de hardware](capabilities-in-technical-preview-1806.md#hardware-inventory-default-unit-revision) <!--514442-->



## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>Funcionalidades fornecidas em technical previews recentes com suporte
Veja a seguir as funcionalidades fornecidas com versões anteriores da versão de technical preview do Configuration Manager ainda com suporte. 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |Funcionalidade |Versão do Technical Preview |Versão do Branch Atual|  
 |----------------|---------------------|--------------------|
 | Criar uma implantação em fases com fases configuradas manualmente para uma sequência de tarefas <!--1358148--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence)  | ![Não foi adicionado](media/Red_X.gif) |  
 | Suporte de ponto de distribuição na nuvem para o Azure Resource Manager<!--1322209--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)  | ![Não foi adicionado](media/Red_X.gif) |  
 | Executar ações com base em insights de gerenciamento <!--1357930--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#take-actions-based-on-management-insights)  | ![Não foi adicionado](media/Red_X.gif) |  
 | Fazer a transição da carga de trabalho de configuração do dispositivo para o Intune usando o cogerenciamento <!--1357903--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#transition-device-configuration-workload-to-intune-using-co-management)  | ![Não foi adicionado](media/Red_X.gif) |  
 | Habilitar os pontos de distribuição para usar o controle de congestionamento de rede <!--1358112--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#enable-distribution-points-to-use-network-congestion-control)  | ![Não foi adicionado](media/Red_X.gif) |  
 | Painel de gerenciamento de nuvem <!--1358461--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#cloud-management-dashboard)  | ![Não foi adicionado](media/Red_X.gif) |  
 | CMPivot <!--1358456--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#cmpivot)  | ![Não foi adicionado](media/Red_X.gif) |  
 | Melhorias nas comunicações seguras com o cliente <!--1356889,1358228,1358460--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#improved-secure-client-communications)  | ![Não foi adicionado](media/Red_X.gif) |  
 | Melhorias para habilitar o suporte de atualização de software de terceiros <!--1357605--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support)  | ![Não foi adicionado](media/Red_X.gif) |  
 | Melhorias na sequência de tarefas de atualização in-loco do Windows 10 <!--1358500--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#improvements-to-windows-10-in-place-upgrade-task-sequence)  | ![Não foi adicionado](media/Red_X.gif) |  
 | CMTrace instalado com o cliente <!--1357971--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#cmtrace-installed-with-client)  | ![Não foi adicionado](media/Red_X.gif) |  
 | Melhoria no console do Configuration Manager <!--1358202--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#improvement-to-the-configuration-manager-console)  | ![Não foi adicionado](media/Red_X.gif) |  
 | Melhorias nos comentários do console <!--1357542--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#improvements-to-console-feedback)  | ![Não foi adicionado](media/Red_X.gif) |  
 | Melhorias em pontos de distribuição habilitados para PXE <!--1357580--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#improvements-to-pxe-enabled-distribution-points)  | ![Não foi adicionado](media/Red_X.gif) |  
 | Melhoria no inventário de hardware para grandes valores inteiros <!--1357880--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values)  | ![Não foi adicionado](media/Red_X.gif) |  
 | Melhoria na manutenção do WSUS <!--1357898--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#improvement-to-wsus-maintenance)  | ![Não foi adicionado](media/Red_X.gif) |  
 | Melhoria no suporte para certificados CNG <!--1357314--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#improvement-to-support-for-cng-certificates)  | ![Não foi adicionado](media/Red_X.gif) |  
| Configurar uma biblioteca de conteúdo remoto para o servidor do site<!--1357525--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Enviar comentários do console do Configuration Manager <!--1357542--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#bkmk_feedback)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Centro de Suporte<!--1357489--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#support-center)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Kit de ferramentas do Configuration Manager <!--1357145--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#configuration-manager-toolkit)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Desinstalar o aplicativo na revogação da aprovação <!--1357891--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#uninstall-application-on-approval-revocation)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Excluir contêineres do Active Directory da descoberta <!--1358143--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#exclude-active-directory-containers-from-discovery)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Especificar a visibilidade do link de site do Catálogo de Aplicativos no Centro de Software <!--1358214--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#specify-the-visibility-of-the-application-catalog-website-link-in-software-center)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Filtrar regras de implantação automática pela arquitetura de atualização de software <!--1322266--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#filter-automatic-deployment-rules-by-software-update-architecture)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Melhorias na implantação do sistema operacional <!--1358330,1358493--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#improvements-to-os-deployment) | ![Não foi adicionado](media/Red_X.gif) | 
 | Os pontos de distribuição por pull são compatíveis com os pontos de distribuição de nuvem como origem <!--1321554--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#pull-distribution-points-support-cloud-distribution-points-as-source)  | ![Não foi adicionado](media/Red_X.gif) | 
 | O suporte parcial de download no cache de par de cliente para reduzir a utilização de WAN <!--1357346--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#partial-download-support-in-client-peer-cache-to-reduce-wan-utilization)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Janelas de manutenção no Centro de Software <!--1358131--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#maintenance-windows-in-software-center)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Guia personalizada para página da Web no Centro de Software <!--1358132--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#custom-tab-for-webpage-in-software-center)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Habilitar o suporte de atualização de software de terceiros em clientes <!--1357605--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Habilitar copiar/colar de detalhes do ativo das exibições de monitoramento <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-copypaste-of-asset-details-from-monitoring-views)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Extensões do SCAP <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#scap-extensions)  | ![Não foi adicionado](media/Red_X.gif) | 
 
  

## <a name="capabilities-delivered-in-previous-technical-previews"></a>Recursos fornecidos em visualizações técnicas anteriores
Veja a seguir as funcionalidades específicas fornecidos com versões anteriores da versão de technical preview do Configuration Manager. Essas funcionalidades permanecem disponíveis em versões posteriores, mas ainda não estão disponíveis em uma versão de branch atual. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |Funcionalidade |Versão do Technical Preview |  
 |----------------|---------------------|
 | Melhorias em pontos de distribuição habilitados para PXE <!-- 1357580 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) | 
 | Painel do ciclo de vida do produto <!--1319632 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) | 
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

