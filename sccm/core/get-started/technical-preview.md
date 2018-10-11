---
title: Versões de visualização técnica
titleSuffix: Configuration Manager
description: Saiba mais sobre o branch de visualização técnica para fazer o test drive das novas funcionalidades e recursos no Configuration Manager.
ms.date: 09/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e49f39f2c9a052ef583b172c1ccad7b2963d300a
ms.sourcegitcommit: a7254f265098ae8e83b4fa1fac312e9cc3c4f897
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "44961068"
---
# <a name="technical-preview-for-configuration-manager"></a>Visualização técnica para o Configuration Manager

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

### <a name="technical-preview-version-1809"></a>Versão da visualização técnica 1809

- [Melhorias ao CMPivot](capabilities-in-technical-preview-1809.md#bkmk_cmpivot) <!--1359068-->
- [Melhoria ao painel do ciclo de vida](capabilities-in-technical-preview-1809.md#bkmk_lifecycle) <!--1358702-->
- [Melhoria ao data warehouse](capabilities-in-technical-preview-1809.md#bkmk_dataw) <!--1358870-->
- [Melhoria de janelas de manutenção para atualizações de software](capabilities-in-technical-preview-1809.md#bkmk_sum-mw) <!--vso2839307-->


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
 | Implantação em fases de atualizações de software <!--1358146--> | [Visualização técnica 1808](capabilities-in-technical-preview-1808.md#bkmk_pod) | ![Não foi adicionado](media/Red_X.gif) | 
 | Melhorias no reparo de aplicativos <!--1357866--> | [Visualização técnica 1808](capabilities-in-technical-preview-1808.md#bkmk_repair) | ![Não foi adicionado](media/Red_X.gif) | 
 | Hub de Comunidade <!--1357766--> | [Visualização técnica 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) | ![Não foi adicionado](media/Red_X.gif) | 
 | Especifique a unidade para manutenção offline da imagem do sistema operacional <!--1358924--> | [Visualização técnica 1807](capabilities-in-technical-preview-1807.md#bkmk_osd) | ![Não foi adicionado](media/Red_X.gif) | 
 | Atividade de sincronização de dispositivo cogerenciados com o Intune <!--1358565--> | [Visualização técnica 1807](capabilities-in-technical-preview-1807.md#bkmk_comgmt) | ![Não foi adicionado](media/Red_X.gif) | 
 | Reparar aplicativos <!--1357866--> | [Visualização técnica 1807](capabilities-in-technical-preview-1807.md#bkmk_app-repair) | ![Não foi adicionado](media/Red_X.gif) | 
 | Aprovar solicitações de aplicativo por email <!--1321550--> | [Visualização técnica 1807](capabilities-in-technical-preview-1807.md#bkmk_email-approve) | ![Não foi adicionado](media/Red_X.gif) | 
 | Melhoria na saída do script <!--1236459--> | [Visualização técnica 1807](capabilities-in-technical-preview-1807.md#bkmk_script) | ![Não foi adicionado](media/Red_X.gif) | 
 | Melhoria nas atualizações de software de terceiros <!--1358714--> | [Visualização técnica 1807](capabilities-in-technical-preview-1807.md#bkmk_3pupdate) | ![Não foi adicionado](media/Red_X.gif) | 
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



## <a name="features-in-previous-technical-previews"></a>Recursos em visualização técnicas anteriores

Os recursos a seguir foram lançados com versões anteriores do branch da visualização técnica do Configuration Manager. Esses recursos permanecem disponíveis em versões posteriores, mas ainda não estão disponíveis no branch atual. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

|Recurso |Versão do Technical Preview |  
|----------------|---------------------|
|Centro de Suporte<!--1357489--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#support-center)  | 
|Serviço de respondente PXE baseado no cliente <!-- 1357148 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
|Suporte de inicialização de rede PXE para IPv6 <!-- 1269793 --> |[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
|Usar o Azure Active Directory <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
|Avaliação de conformidade para atualizações do Windows Update para Empresas <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
|Acesso a dados do ponto de extremidade OData <!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
|Melhorias no Asset Intelligence <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
|Os usuários finais podem instalar aplicativos por meio do Portal da Empresa <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## <a name="see-also"></a>Consulte também  

Para obter mais informações, consulte os seguintes artigos:  

- [Avaliar o Configuration Manager em um laboratório](/sccm/core/get-started/evaluate-with-lab-environment)
- [Novidades nas versões incrementais do Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Introdução ao Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]  
> Para saber mais sobre os recursos atuais de branch que exigem autorização para habilitação, confira [Recursos de pré-lançamento](/sccm/core/servers/manage/pre-release-features).  
> 
> Para saber mais sobre os recursos atuais de branch que precisam ser habilitados primeiro, confira [Habilitar recursos opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
