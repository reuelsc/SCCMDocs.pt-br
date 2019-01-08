---
title: Versões de visualização técnica
titleSuffix: Configuration Manager
description: Saiba mais sobre o branch de visualização técnica para fazer o test drive das novas funcionalidades e recursos no Configuration Manager.
ms.date: 12/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d2c1e93378711a19b10f9b67fcaad9973e53ee2e
ms.sourcegitcommit: d36e4c7082a5144e79035dd8847c8e741fa04667
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53444630"
---
# <a name="technical-preview-for-configuration-manager"></a>Visualização técnica para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

Este artigo fornece detalhes sobre o branch de visualização técnica mensal do Configuration Manager. A visualização técnica introduz uma nova funcionalidade na qual a Microsoft tem trabalhado. Ele introduz novos recursos que ainda não estão incluídos no branch atual do Configuration Manager. Eventualmente, esses recursos poderão ser incluídos em uma atualização do branch atual. Antes de finalizarmos os recursos, queremos que você os experimente e dê sua opinião.  

Como esta versão é technical preview, os detalhes e funcionalidades estão sujeitos a alterações.  

Essas informações se aplicam a todas as versões do branch da visualização técnica do Configuration Manager. Este artigo lista cada novo recurso juntamente com a versão da visualização técnica na qual ele aparece pela primeira vez. Por exemplo, a versão **1809** de setembro (09) de 2018 (18). Os artigos separados dedicados a cada detalhe da versão prévia detalham recursos individuais.  

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

-  **Technical Preview versão 1810.2**: O Configuration Manager Technical Preview versão 1810.2 está disponível como uma atualização no console e como uma nova versão de linha de base. Baixe as versões de linha de base do [Centro de Avaliação do TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).



##  <a name="BKMK_TPFeedback"></a> Enviando comentários  

Adoramos ouvir seus comentários sobre os novos recursos da visualização técnica. Para obter mais informações, consulte [Comentários sobre o produto](/sccm/core/understand/find-help#product-feedback).

Caso tenha sugestões sobre novos recursos que gostaria de ver, gostaríamos de saber também. Para enviar novas ideias e para votar nas ideias enviadas por outras pessoas, [visite nossa página do UserVoice](https://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->



##  <a name="bkmk_tpCaps"></a> Recursos da versão mais recente  

Os seguintes recursos estão disponíveis com a visualização técnica mais recente do Configuration Manager versão: 

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1812"></a>Technical Preview versão 1812

<!--capabilities-in-technical-preview-1812.md#bkmk_anchor-->

- [Melhorias para à etapa de sequência de tarefas de Executar Script do PowerShell](capabilities-in-technical-preview-1812.md#bkmk_posh) <!--3556028 fka 1359389-->  
- [Melhorias nas aprovações de aplicativo por email](capabilities-in-technical-preview-1812.md#bkmk_email) <!--3594063-->  
- [Configurar a afinidade de dispositivo de usuário no Centro de Software](capabilities-in-technical-preview-1812.md#bkmk_uda) <!--3485366-->  
- [Melhorias no console do Configuration Manager](capabilities-in-technical-preview-1812.md#bkmk_console) <!--3594151-->  
- [Baixar relatórios do Hub de Comunidade](capabilities-in-technical-preview-1812.md#bkmk_hub)<!--3555936-->  


> [!Note]  
> Os recursos que estavam disponíveis em uma versão anterior da visualização técnica permanecem disponíveis em versões posteriores. De forma semelhante, os recursos que foram adicionadas ao branch atual do Configuration Manager permanecem disponíveis no branch da visualização técnica.   



## <a name="features-in-recent-supported-technical-previews"></a>Recursos em visualização técnicas recentes com suporte

Os recursos a seguir foram lançados com versões anteriores do branch da visualização técnica do Configuration Manager que ainda têm suporte: 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 | Recurso | Versão da visualização técnica | Versão do branch atual |  
 |---------|---------------------------|------------------------|
 | Não carregar perfis do Windows PowerShell <!--1359239--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_noprofile) | ![Não foi adicionado](media/Red_X.gif) | 
 | Uma conexão do Intune não é mais necessária para o MDM local <!--1359124--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_opmdm) | ![Não foi adicionado](media/Red_X.gif) | 
 | Notificações do console do Configuration Manager <!--1318035--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_notify) | ![Não foi adicionado](media/Red_X.gif) | 
 | Melhorias na criação de mídia da sequência de tarefas <!--1359388--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_tsmedia) | ![Não foi adicionado](media/Red_X.gif) | 
 | Melhoria para à etapa de sequência de tarefas de Executar Script do PowerShell <!--1359389--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_posh) | ![Não foi adicionado](media/Red_X.gif) | 
 | Melhorias na avaliação de coleção <!--1358981--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_colleval) | Versão 1810 | 
 | Autenticação de administrador do Configuration Manager <!--1357013--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_auth) | Versão 1810 | 
 | Regra de insights de gerenciamento para a versão do cliente da origem do cache par <!--1358008--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_insights) | Versão 1810 | 
 | Melhorias na configuração de clientes baseados na Internet <!--1359181--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_cmg) | Versão 1810 | 
 | Converter aplicativos em MSIX <!--1359029--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_msix) | Versão 1810 | 
 | Melhoria à instalação do cliente <!--1358840--> | [Visualização técnica 1810](capabilities-in-technical-preview-1810.md#bkmk_ccmsetup) | Versão 1810 | 
 | Política de conformidade de aplicativo necessária para dispositivos cogerenciados <!--1358196--> | [Visualização técnica 1810](capabilities-in-technical-preview-1810.md#bkmk_app-compliance) | Versão 1810 | 
 | Melhoria ao painel de cogerenciamento <!--1358980--> | [Visualização técnica 1810](capabilities-in-technical-preview-1810.md#bkmk_comgmt-report) | Versão 1810 | 
 | Opções do novo grupo de limites <!--1358749--> | [Visualização técnica 1810](capabilities-in-technical-preview-1810.md#bkmk_bgoptions) | Versão 1810 | 
 | Sistema de sites no nó de cluster do Windows <!--1359132--> | [Visualização técnica 1810](capabilities-in-technical-preview-1810.md#bkmk_cluster) | Versão 1810 | 
 | Melhorias ao CMPivot <!--1359068--> | [Visualização técnica 1810](capabilities-in-technical-preview-1810.md#bkmk_cmpivot) | Versão 1810 | 
 | Melhorias nos scripts <!--1358239--> | [Visualização técnica 1810](capabilities-in-technical-preview-1810.md#bkmk_scripts) | Versão 1810 | 
 | Nova ação de notificação de cliente para ativação de dispositivo <!--1317364--> | [Visualização técnica 1810](capabilities-in-technical-preview-1810.md#bkmk_wakeup) | Versão 1810 | 
 | Suporte à sequência de tarefas para grupos de limites <!--1359025--> | [Visualização técnica 1810](capabilities-in-technical-preview-1810.md#bkmk_bgr-osd) | Versão 1810 | 
 | Painel de insights de gerenciamento <!--1357979--> | [Visualização técnica 1810](capabilities-in-technical-preview-1810.md#bkmk_insights) | Versão 1810 | 
 | Painel de documentação no console <!--1357546--> | [Visualização técnica 1810](capabilities-in-technical-preview-1810.md#bkmk_doc-dashboard) | ![Não foi adicionado](media/Red_X.gif) | 
 | Melhorias na manutenção do driver <!--1358270--> | [Visualização técnica 1810](capabilities-in-technical-preview-1810.md#bkmk_drivers) | Versão 1810 | 
 | Suporte à sequência de tarefas do Windows AutoPilot para dispositivos existentes <!--1358333--> | [Visualização técnica 1810](capabilities-in-technical-preview-1810.md#bkmk_autopilot) | Versão 1810 | 



## <a name="features-in-previous-technical-previews"></a>Recursos em visualização técnicas anteriores

Os recursos a seguir foram lançados com versões anteriores do branch da visualização técnica do Configuration Manager. Esses recursos permanecem disponíveis em versões posteriores, mas ainda não estão disponíveis no branch atual. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

| Recurso        | Versão da visualização técnica |  
|----------------|---------------------------|
| Hub de Comunidade <!--1357766--> | [Visualização técnica 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) | 
| Atividade de sincronização de dispositivo cogerenciados com o Intune <!--1358565--> | [Visualização técnica 1807](capabilities-in-technical-preview-1807.md#bkmk_comgmt) | 
| Serviço de respondente PXE baseado no cliente <!--1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| Suporte de inicialização de rede PXE para IPv6 <!--1269793--> |[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Usar o Azure Active Directory <!--1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Avaliação de conformidade para atualizações do Windows Update para Empresas <!--1235390--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
| Melhorias no Asset Intelligence <!--1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |
| Os usuários finais podem instalar aplicativos por meio do Portal da Empresa <!--1037233?--> | [Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End) |



## <a name="see-also"></a>Consulte também  

Para obter mais informações, consulte os seguintes artigos:  

- [Avaliar o Configuration Manager em um laboratório](/sccm/core/get-started/evaluate-with-lab-environment)
- [Novidades nas versões incrementais do Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Introdução ao Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]  
> Para saber mais sobre os recursos atuais de branch que exigem autorização para habilitação, confira [Recursos de pré-lançamento](/sccm/core/servers/manage/pre-release-features).  
> 
> Para saber mais sobre os recursos atuais de branch que precisam ser habilitados primeiro, confira [Habilitar recursos opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
