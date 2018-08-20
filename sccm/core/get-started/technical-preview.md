---
title: Versões do Technical Preview
titleSuffix: Configuration Manager
description: Saiba mais sobre o branch de visualização técnica para fazer o test drive das novas funcionalidades e recursos no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b60ebcf0ce94dfdc25466b31c9a64d0d556e1ac6
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385381"
---
# <a name="technical-preview-for-configuration-manager"></a>Visualização técnica do Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo fornece detalhes sobre o branch de visualização técnica mensal do Configuration Manager. A visualização técnica introduz uma nova funcionalidade na qual a Microsoft tem trabalhado. Ele introduz novos recursos que ainda não estão incluídos no branch atual do Configuration Manager. Eventualmente, esses recursos poderão ser incluídos em uma atualização do branch atual. Antes de finalizarmos os recursos, queremos que você os experimente e dê sua opinião.  

Como esta versão é technical preview, os detalhes e funcionalidades estão sujeitos a alterações.  

Essas informações se aplicam a todas as versões do branch da visualização técnica do Configuration Manager. Este artigo lista cada novo recurso juntamente com a versão da visualização técnica na qual ele aparece pela primeira vez. Por exemplo, a versão **1806** de junho (06) de 2018 (18). Os artigos separados dedicados a cada detalhe da versão prévia detalham recursos individuais.  

Para saber mais sobre o que há de novo no *branch atual* do Configuration Manager, confira [Novidades nas versões incrementais do Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).



##  <a name="bkmk_reqs"></a> Requisitos e limitações  

> [!IMPORTANT]     
>  A visualização técnica é licenciada apenas para ser usada em um ambiente de laboratório. A Microsoft não pode fornecer serviços de suporte e alguns recursos podem não estar disponíveis para o software na versão prévia. Além disso, o software de versão prévia pode ter padrões diferentes ou reduzidos de segurança, privacidade, acessibilidade, disponibilidade e confiabilidade em comparação com o software fornecido comercialmente.  

Para a maioria dos pré-requisitos do produto, use as informações contidas nas [Configurações com suporte](/sccm/core/plan-design/configs/supported-configurations). As seguintes exceções se aplicam ao branch da visualização técnica:  

-   Cada instalação fica ativa por 90 dias antes de se tornar inativa.  

-   O inglês é o único idioma com suporte.  

-   Só há suporte para os seguintes parâmetros de linha de comando de configuração:  
    -   `/silent`  
    -   `/testdbupgrade`    

-   O ponto de conexão de serviço deve ser instalado no modo online. Ele não é compatível com o modo offline.  

-   Os artigos separados para cada versão específica do technical preview incluem requisitos ou limitações adicionais, conforme aplicável.

-   Os recursos a seguir não são compatíveis com o branch da visualização técnica:  

    - [Migração](/sccm/core/migration/migrate-data-between-hierarchies) de ou para esse o branch de visualização.  

    - [Faça upgrade](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) para esse o branch de visualização.  

    - [Recuperação de site](/sccm/core/servers/manage/recover-sites) na pasta cd.latest.  <!--507106-->

-   Não há suporte para atualização para o branch atual a partir deste o branch de visualização.  

    > [!Note]  
    > Quando as atualizações estão disponíveis para uma versão prévia, é possível localizá-las e instalá-las do nó **Atualizações e Manutenção** do console do Configuration Manager. Para obter um vídeo do processo de upgrade no console, confira [Instalação dos pacotes de atualização do Configuration Manager](https://www.youtube.com/embed/KBd_EGFbUT8) no youtube.com.  

-   Ele só é compatível com um site primário autônomo. Não há suporte para um site de administração central, para vários sites primários ou para sites secundários.  

O branch de visualização técnica do Configuration Manager é compatível com os seguintes produtos e tecnologias: 

-   Só há suporte para as seguintes versões do **SQL Server**:  

    -   SQL Server 2017 (com a atualização cumulativa 2 e posterior), do Configuration Manager versão 1710 em diante
    -   SQL Server 2016 (sem Service Pack e posterior)
    -   SQL Server 2014 (com Service Pack 1 e posterior)
    -   SQL Server 2012 (com Service Pack 3 ou posterior)  


-   O site dá suporte a até 10 clientes, que devem executar uma das seguintes versões do Windows:  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 7  

> [!Note]  
> A inclusão desses produtos nesse conteúdo não implica uma extensão de suporte para uma versão além do seu ciclo de vida de suporte. O Configuration Manager não oferece suporte a produtos além do ciclo de vida de suporte. Para mais informações, confira [Política de Ciclo de Vida da Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=208270).  



##  <a name="bkmk_install"></a> Instalar e atualizar  

O branch de visualização técnica do Configuration Manager para uso em laboratórios é diferente do branch atual do Configuration Manager para uso em produção.  

Primeiro, é necessário instalar uma versão de linha de base do branch da visualização técnica. Depois de instalar uma versão de linha de base, use as atualizações no console para atualizar sua instalação para a versão prévia mais recente. Normalmente, as novas versões da visualização técnica são disponibilizadas todos os meses.

A Microsoft oferece suporte a todas as versões da visualização técnica até que três versões sucessivas estejam disponíveis. Por exemplo, quando a versão 1708 foi liberada, a versão 1704 deixou de ter suporte. As versões 1705, 1706 e 1707 permaneceram com suporte. Quando uma linha de base fica sem suporte, ainda há suporte para a instalação um novo site da visualização técnica desde que você atualize imediatamente para uma versão com suporte. A linha de base mais antiga terá suporte até que uma nova versão de linha de base esteja disponível. Atualize para a versão mais recente disponível na linha de base e repita o processo de atualização até instalar a versão mais recente da visualização técnica.

> [!TIP]  
>  Quando você instala uma atualização do Technical Preview, atualiza a instalação da versão prévia para essa nova versão de Technical Preview. Uma instalação da visualização técnica nunca tem a opção de upgrade para uma instalação de branch atual. Ela também não recebe atualizações da versão de branch atual. 
> 
> Diversas vezes ao longo do ano, são disponibilizadas versões do branch da visualização técnica e do branch atual com o mesmo número de versão. Por exemplo, há um visualização técnica versão 1802 e um branch atual versão 1802. 


### <a name="active-baseline-versions"></a>Versões de linha de base ativas
   
Instale uma versão de linha de base em até um ano após seu lançamento. Quando você instala um novo site da visualização técnica, se mais de uma versão de linha de base estiver disponível no momento, use a versão de linha de base mais recente.

-  **Visualização técnica versão 1806**: a visualização técnica versão 1806 do Configuration Manager está disponível como uma atualização no console e como uma nova versão de linha de base. Baixe as versões de linha de base [no Centro de Avaliação do TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).



##  <a name="BKMK_TPFeedback"></a> Enviando comentários  

Adoramos ouvir seus comentários sobre os novos recursos da visualização técnica. Para obter mais informações, consulte [Comentários sobre o produto](/sccm/core/understand/find-help#product-feedback).

Caso tenha sugestões sobre novos recursos que gostaria de ver, gostaríamos de saber também. Para enviar novas ideias e para votar nas ideias enviadas por outras pessoas, [visite nossa página do UserVoice](https://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->



##  <a name="bkmk_tpCaps"></a> Recursos da versão mais recente  

Os seguintes recursos estão disponíveis com a visualização técnica mais recente do Configuration Manager versão: 

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1807"></a>Visualização técnica versão 1807

- [Hub da comunidade](capabilities-in-technical-preview-1807.md#bkmk_hub) <!--1357766-->
- [Especificar a unidade para manutenção offline de imagem do sistema operacional](capabilities-in-technical-preview-1807.md#bkmk_osd) <!--1358924-->
- [Atividade de sincronização de dispositivo cogerenciado com o Intune](capabilities-in-technical-preview-1807.md#bkmk_comgmt) <!--1358565-->
- [Reparar aplicativos](capabilities-in-technical-preview-1807.md#bkmk_app-repair) <!--1357866-->
- [Aprovar solicitações de aplicativo por email](capabilities-in-technical-preview-1807.md#bkmk_email-approve) <!--1321550-->
- [Melhoria na saída do script](capabilities-in-technical-preview-1807.md#bkmk_script) <!--1236459-->
- [Melhoria nas atualizações de software de terceiros](capabilities-in-technical-preview-1807.md#bkmk_3pupdate) <!--1358714-->


> [!Note]  
> Os recursos que estavam disponíveis em uma versão anterior da visualização técnica permanecem disponíveis em versões posteriores. De forma semelhante, os recursos que foram adicionadas ao branch atual do Configuration Manager permanecem disponíveis no branch da visualização técnica.   



## <a name="features-in-recent-supported-technical-previews"></a>Recursos em visualização técnicas recentes com suporte

Os recursos a seguir foram lançados com versões anteriores do branch da visualização técnica do Configuration Manager que ainda têm suporte: 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |Recurso |Versão da visualização técnica |Versão do branch atual|  
 |----------------|---------------------|--------------------|
 | Melhorias para implantações em fases <!--1358577,1358147,1358578--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_pod)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Suporte para novos formatos do pacote de aplicativo do Windows <!--1357427--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_msix)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhoria de segurança do cliente por push <!--1358204--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_client-push)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Insights de gerenciamento para manutenção proativa <!--1352184,et al--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_insights)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Carga de trabalho de aplicativos móveis de transição para dispositivos cogerenciados <!--1357892--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_comgmt)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Opções de grupo de limites para downloads de pares <!--1356193--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_bgoptions)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Suporte a catálogos personalizados de atualizações de software de terceiros <!--1358714--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhorias nos recursos de gerenciamento de nuvem <!--511980,515854--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_cloud)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Novo relatório de conformidade de atualizações de software <!--1357775--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_report)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Atualizações de software de terceiros <!--1352101--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#bkmk-3pupdate)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Definir as configurações do Windows Defender SmartScreen para o Microsoft Edge <!--1353701--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#configure-windows-defender-smartscreen-settings-for-microsoft-edge)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Sincronizar a política de MDM do Microsoft Intune para um dispositivo cogerenciado <!--1357377--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Fazer a transição da carga de trabalho do Office 365 para o Intune usando o cogerenciamento <!--1357841--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#transition-office-365-workload-to-intune-using-co-management)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Gerenciador de Conversão de Pacote <!--1357861--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#package-conversion-manager)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Implantar atualizações de software sem conteúdo <!--1357933--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#deploy-software-updates-without-content)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Integração da Ferramenta de Personalização do Office com o Instalador do Office 365 <!--1358149--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#office-customization-tool-integration-with-the-office-365-installer)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhorias no gateway de gerenciamento de nuvem <!--1358215,1358651,503899--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-cloud-management-gateway)   | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhorias nas comunicações seguras com o cliente <!--1358278,1358279--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-secure-client-communications)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhorias na infraestrutura do Centro de Software <!--1358309--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#software-center-infrastructure-improvements)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Provisionar pacotes de aplicativos do Windows para todos os usuários em um dispositivo <!--1358310--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#provision-windows-app-packages-for-all-users-on-a-device)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhorias no painel do Surface <!--1358654--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-the-surface-dashboard)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Revisão da unidade padrão do inventário de hardware <!--514442--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#hardware-inventory-default-unit-revision)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Criar uma implantação em fases com fases configuradas manualmente para uma sequência de tarefas <!--1358148--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Suporte de ponto de distribuição na nuvem para o Azure Resource Manager<!--1322209--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Executar ações com base em insights de gerenciamento <!--1357930--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#take-actions-based-on-management-insights)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Fazer a transição da carga de trabalho de configuração do dispositivo para o Intune usando o cogerenciamento <!--1357903--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#transition-device-configuration-workload-to-intune-using-co-management)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Habilitar os pontos de distribuição para usar o controle de congestionamento de rede <!--1358112--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#enable-distribution-points-to-use-network-congestion-control)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Painel de gerenciamento de nuvem <!--1358461--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#cloud-management-dashboard)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | CMPivot <!--1358456--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#cmpivot)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhorias nas comunicações seguras com o cliente <!--1356889,1358228,1358460--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#improved-secure-client-communications)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhorias para habilitar o suporte de atualização de software de terceiros <!--1357605--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhorias na sequência de tarefas de atualização in-loco do Windows 10 <!--1358500--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#improvements-to-windows-10-in-place-upgrade-task-sequence)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | CMTrace instalado com o cliente <!--1357971--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#cmtrace-installed-with-client)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhoria no console do Configuration Manager <!--1358202--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#improvement-to-the-configuration-manager-console)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhorias nos comentários do console <!--1357542--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#improvements-to-console-feedback)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhorias em pontos de distribuição habilitados para PXE <!--1357580--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#improvements-to-pxe-enabled-distribution-points)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhoria no inventário de hardware para grandes valores inteiros <!--1357880--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhoria na manutenção do WSUS <!--1357898--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#improvement-to-wsus-maintenance)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhoria no suporte para certificados CNG <!--1357314--> | [Visualização técnica 1805](capabilities-in-technical-preview-1805.md#improvement-to-support-for-cng-certificates)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Configurar uma biblioteca de conteúdo remoto para o servidor do site<!--1357525--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Enviar comentários do console do Configuration Manager <!--1357542--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#bkmk_feedback)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Centro de Suporte<!--1357489--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#support-center)  | ![Não foi adicionado](media/Red_X.gif) | 
 | Kit de ferramentas do Configuration Manager <!--1357145--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#configuration-manager-toolkit)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Desinstalar o aplicativo na revogação da aprovação <!--1357891--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#uninstall-application-on-approval-revocation)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Excluir contêineres do Active Directory da descoberta <!--1358143--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#exclude-active-directory-containers-from-discovery)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Especificar a visibilidade do link de site do Catálogo de Aplicativos no Centro de Software <!--1358214--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#specify-the-visibility-of-the-application-catalog-website-link-in-software-center)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Filtrar regras de implantação automática pela arquitetura de atualização de software <!--1322266--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#filter-automatic-deployment-rules-by-software-update-architecture)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Melhorias na implantação do sistema operacional <!--1358330,1358493--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#improvements-to-os-deployment) | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Os pontos de distribuição por pull são compatíveis com os pontos de distribuição de nuvem como origem <!--1321554--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#pull-distribution-points-support-cloud-distribution-points-as-source)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | O suporte parcial de download no cache de par de cliente para reduzir a utilização de WAN <!--1357346--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#partial-download-support-in-client-peer-cache-to-reduce-wan-utilization)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Janelas de manutenção no Centro de Software <!--1358131--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#maintenance-windows-in-software-center)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Guia personalizada para página da Web no Centro de Software <!--1358132--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#custom-tab-for-webpage-in-software-center)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Habilitar o suporte de atualização de software de terceiros em clientes <!--1357605--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Habilitar copiar/colar de detalhes do ativo das exibições de monitoramento <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-copypaste-of-asset-details-from-monitoring-views)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Extensões do SCAP <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#scap-extensions)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 
  

## <a name="features-in-previous-technical-previews"></a>Recursos em visualização técnicas anteriores

Os recursos a seguir foram lançados com versões anteriores do branch da visualização técnica do Configuration Manager. Esses recursos permanecem disponíveis em versões posteriores, mas ainda não estão disponíveis no branch atual. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

|Recurso |Versão do Technical Preview |  
|----------------|---------------------|
| Serviço de respondente PXE baseado no cliente <!-- 1357148 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
|Suporte de inicialização de rede PXE para IPv6 <!-- 1269793 --> |[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
|Usar o Azure Active Directory <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
|Avaliação de conformidade para atualizações do Windows Update para Empresas <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
|Acesso a dados do ponto de extremidade OData <!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
|Melhorias no Asset Intelligence <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
|Os usuários finais podem instalar aplicativos por meio do Portal da Empresa <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|

<!--Removed for 1806 CB:
 |Site server role high availability <!-- 1128774  |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 | Product lifecycle dashboard <!--1319632  | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) | 
 | Improvements to PXE-enabled distribution points <!-- 1357580  | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) | 
-->



## <a name="see-also"></a>Consulte também  

Para obter mais informações, consulte os seguintes artigos:  

- [Avaliar o Configuration Manager em um laboratório](/sccm/core/get-started/evaluate-with-lab-environment)
- [Novidades nas versões incrementais do Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Introdução ao Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]  
> Para saber mais sobre os recursos atuais de branch que exigem autorização para habilitação, confira [Recursos de pré-lançamento](/sccm/core/servers/manage/pre-release-features).  
> 
> Para saber mais sobre os recursos atuais de branch que precisam ser habilitados primeiro, confira [Habilitar recursos opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
