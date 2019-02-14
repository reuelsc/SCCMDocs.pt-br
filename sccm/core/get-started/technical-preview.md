---
title: Versões de visualização técnica
titleSuffix: Configuration Manager
description: Saiba mais sobre o branch de visualização técnica para fazer o test drive das novas funcionalidades e recursos no Configuration Manager.
ms.date: 02/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 69fd77df25465910776eb413601efef5d87842aa
ms.sourcegitcommit: 4317bd20050f582a068d0a813e71c449d655e4b4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2019
ms.locfileid: "55971890"
---
# <a name="technical-preview-for-configuration-manager"></a>Visualização técnica para o Configuration Manager

*Aplica-se a: System Center Configuration Manager (Visualização Técnica)*

Este artigo fornece detalhes sobre o branch de visualização técnica mensal do Configuration Manager. A visualização técnica introduz uma nova funcionalidade na qual a Microsoft tem trabalhado. Ele introduz novos recursos que ainda não estão incluídos no branch atual do Configuration Manager. Eventualmente, esses recursos poderão ser incluídos em uma atualização do branch atual. Antes de finalizarmos os recursos, queremos que você os experimente e dê sua opinião.  

Como esta versão é de visualização técnica, os detalhes e funcionalidades estão sujeitos a alterações.  

Essas informações se aplicam a todas as versões do branch da visualização técnica do Configuration Manager. Este artigo lista cada novo recurso juntamente com a versão da visualização técnica na qual ele aparece pela primeira vez. Por exemplo, a versão **1901** de janeiro (01) de 2019 (19). Os artigos separados dedicados a cada detalhe da versão prévia detalham recursos individuais.  

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

-   Os artigos separados para cada versão específica da visualização técnica incluem requisitos ou limitações adicionais, conforme aplicável.

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

    -   SQL Server 2017 (com atualização cumulativa 2 ou posterior) 
    -   SQL Server 2016 (sem service pack ou posterior)
    -   SQL Server 2014 (com o service pack 1 ou posterior)
    -   SQL Server 2012 (com o service pack 3 ou posterior)  


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
>  Quando você instala uma atualização da Visualização Técnica, atualiza a instalação da versão prévia para essa nova versão da Visualização Técnica. Uma instalação da visualização técnica nunca tem a opção de upgrade para uma instalação de branch atual. Ela também não recebe atualizações da versão de branch atual. 
> 
> Diversas vezes ao longo do ano, são disponibilizadas versões do branch da visualização técnica e do branch atual com o mesmo número de versão. Por exemplo, há um visualização técnica versão 1802 e um branch atual versão 1802. 


### <a name="active-baseline-versions"></a>Versões de linha de base ativas
   
Instale uma versão de linha de base em até um ano após seu lançamento. Quando você instala um novo site da visualização técnica, se mais de uma versão de linha de base estiver disponível no momento, use a versão de linha de base mais recente.

-  **Visualização Técnica versão 1810.2**: A visualização técnica do Configuration Manager versão 1810.2 está disponível como uma atualização no console e como uma nova versão de linha de base. Baixe as versões de linha de base do [Centro de Avaliação do TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).



##  <a name="BKMK_TPFeedback"></a> Enviando comentários  

Adoramos ouvir seus comentários sobre os novos recursos da visualização técnica. Para obter mais informações, consulte [Comentários sobre o produto](/sccm/core/understand/find-help#product-feedback).

Caso tenha sugestões sobre novos recursos que gostaria de ver, gostaríamos de saber também. Para enviar novas ideias e para votar nas ideias enviadas por outras pessoas, [visite nossa página do UserVoice](https://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->



##  <a name="bkmk_tpCaps"></a> Recursos da versão mais recente  

Os seguintes recursos estão disponíveis com a visualização técnica mais recente do Configuration Manager versão: 

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1902"></a>Visualização Técnica versão 1902

<!-- - [title](/sccm/core/get-started/2019/technical-preview-1901#bkmk_anchor)<!--ID-->

- [Substituir as notificações do sistema por uma janela de diálogo](/sccm/core/get-started/2019/technical-preview-1902#bkmk_impact)<!--3555947-->
- [Status do andamento durante a sequência de tarefas de atualização in-loco](/sccm/core/get-started/2019/technical-preview-1902#bkmk_ipu)<!--3747129-->
- [Redirecionar pastas conhecidas do Windows para o OneDrive](/sccm/core/get-started/2019/technical-preview-1902#bkmk_odfb)<!--3556021-->
- [Visualizar a primeira tela somente durante o controle remoto](/sccm/core/get-started/2019/technical-preview-1902#bkmk_rcmulti)<!--3231732-->
- [Editar ou copiar os scripts do PowerShell](/sccm/core/get-started/2019/technical-preview-1902#bkmk_psedit)<!--3705507-->
- [Adicionar o gateway de gerenciamento de nuvem a grupos de limites](/sccm/core/get-started/2019/technical-preview-1902#bkmk_cmgbg)<!--3640932-->
- [Configurar os modos de exibição padrão no Centro de Software](/sccm/core/get-started/2019/technical-preview-1902#bkmk_swctr)<!--3612112-->
- [Melhorias no painel de integridade do cliente](/sccm/core/get-started/2019/technical-preview-1902#bkmk_health)<!--3599209-->



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
 | Painel de integridade do cliente <!--3599209--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_health) | ![Não foi adicionado](media/Red_X.gif) | 
 | Especificar a prioridade para as atualizações de recurso no serviço do Windows 10 <!--3734525--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_neo) | ![Não foi adicionado](media/Red_X.gif) | 
 | Monitoramento dedicado para implantações em fases <!--3555949--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_pod) | ![Não foi adicionado](media/Red_X.gif) | 
 | Executar o CMPivot do site de administração central <!--3610960--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_cmpivot) | ![Não foi adicionado](media/Red_X.gif) | 
 | Melhorias na etapa da sequência de tarefas Executar Script do PowerShell <!--3556028--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_posh) | ![Não foi adicionado](media/Red_X.gif) | 
 | Produtos do Office no painel de ciclo de vida <!--3556026--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_lifecycle) | ![Não foi adicionado](media/Red_X.gif) | 
 | Regras de insight de gerenciamento para coleções <!--3555752--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_micoll) | ![Não foi adicionado](media/Red_X.gif) | 
 | Pesquisar nas exibições de dispositivo usando o endereço MAC <!--3600878--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_mac) | ![Não foi adicionado](media/Red_X.gif) | 
 | Modo de manutenção do ponto de distribuição <!--3555754--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_dpmaint) | ![Não foi adicionado](media/Red_X.gif) | 
 | Serviço de imagens otimizadas <!--3555951--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_resetbase) | ![Não foi adicionado](media/Red_X.gif) | 
 | Importar um índice único de uma imagem do sistema operacional <!--3719699--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_index) | ![Não foi adicionado](media/Red_X.gif) | 
 | Usar o Azure Resource Manager para os serviços de nuvem <!--3605704--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_arm) | ![Não foi adicionado](media/Red_X.gif) | 
 | Confirmação de comentários do console <!--3556010--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_feedback) | ![Não foi adicionado](media/Red_X.gif) | 
 | Criar um laboratório de visualização técnica do Configuration Manager no Azure <!--3556017--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_azurevm) | ![Não foi adicionado](media/Red_X.gif) | 
 | Especificar uma porta personalizada para ativação de par <!--3605925--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_sleep) | ![Não foi adicionado](media/Red_X.gif) | 
 | Exibir consoles conectados recentemente <!--3699367--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_console) | ![Não foi adicionado](media/Red_X.gif) | 
 | Interromper o serviço de nuvem quando ele exceder o limite <!--3735092--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_cmg) | ![Não foi adicionado](media/Red_X.gif) | 
 | Tempo limite do modo de provisionamento de cliente <!--3197824--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_osdprov) | ![Não foi adicionado](media/Red_X.gif) | 
 | Melhorias na implantação do sistema operacional <!--3633146,3641475,3654172,3734270--> | [Visualização Técnica 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_osd) | ![Não foi adicionado](media/Red_X.gif) | 
 | Melhorias na etapa da sequência de tarefas Executar Script do PowerShell <!--3556028 fka 1359389--> | [Visualização Técnica 1812](capabilities-in-technical-preview-1812.md#bkmk_posh) | ![Não foi adicionado](media/Red_X.gif) | 
 | Melhorias nas aprovações de aplicativo por email <!--3594063--> | [Visualização Técnica 1812](capabilities-in-technical-preview-1812.md#bkmk_email) | ![Não foi adicionado](media/Red_X.gif) | 
 | Configurar a afinidade de dispositivo de usuário no Centro de Software <!--3485366--> | [Visualização Técnica 1812](capabilities-in-technical-preview-1812.md#bkmk_uda) | ![Não foi adicionado](media/Red_X.gif) | 
 | Melhorias no console do Configuration Manager <!--3594151--> | [Visualização Técnica 1812](capabilities-in-technical-preview-1812.md#bkmk_console) | ![Não foi adicionado](media/Red_X.gif) | 
 | Baixar os relatórios do Hub de Comunidade<!--3555936--> | [Visualização Técnica 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) | ![Não foi adicionado](media/Red_X.gif) | 
 | Não carregar perfis do Windows PowerShell <!--1359239--> | [Visualização Técnica 1811](capabilities-in-technical-preview-1811.md#bkmk_noprofile) | ![Não foi adicionado](media/Red_X.gif) | 
 | Uma conexão do Intune não é mais necessária para o MDM local <!--1359124--> | [Visualização Técnica 1811](capabilities-in-technical-preview-1811.md#bkmk_opmdm) | ![Não foi adicionado](media/Red_X.gif) | 
 | Notificações do console do Configuration Manager <!--1318035--> | [Visualização Técnica 1811](capabilities-in-technical-preview-1811.md#bkmk_notify) | ![Não foi adicionado](media/Red_X.gif) | 
 | Melhorias na criação de mídia da sequência de tarefas <!--1359388--> | [Visualização Técnica 1811](capabilities-in-technical-preview-1811.md#bkmk_tsmedia) | ![Não foi adicionado](media/Red_X.gif) | 
 | Melhoria para à etapa de sequência de tarefas de Executar Script do PowerShell <!--1359389--> | [Visualização Técnica 1811](capabilities-in-technical-preview-1811.md#bkmk_posh) | ![Não foi adicionado](media/Red_X.gif) | 



## <a name="features-in-previous-technical-previews"></a>Recursos em visualização técnicas anteriores

Os recursos a seguir foram lançados com versões anteriores do branch da visualização técnica do Configuration Manager. Esses recursos permanecem disponíveis em versões posteriores, mas ainda não estão disponíveis no branch atual. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

| Recurso        | Versão da visualização técnica |  
|----------------|---------------------------|
| Painel de documentação no console <!--1357546--> | [Visualização técnica 1810](capabilities-in-technical-preview-1810.md#bkmk_doc-dashboard) | 
| Hub de Comunidade <!--1357766--> | [Visualização técnica 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) | 
| Atividade de sincronização de dispositivo cogerenciados com o Intune <!--1358565--> | [Visualização técnica 1807](capabilities-in-technical-preview-1807.md#bkmk_comgmt) | 
| Serviço de respondente PXE baseado no cliente <!--1357148--> | [Visualização Técnica 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| Suporte de inicialização de rede PXE para IPv6 <!--1269793--> |[Visualização Técnica 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Usar o Azure Active Directory <!--1322145--> | [Visualização Técnica 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Avaliação de conformidade para atualizações do Windows Update para Empresas <!--1235390--> | [Visualização Técnica 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
| Melhorias no Asset Intelligence <!--1307390--> | [Visualização Técnica 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |
| Os usuários finais podem instalar aplicativos por meio do Portal da Empresa <!--1037233?--> | [Visualização Técnica 1605](capabilities-in-technical-preview-1605.md#BKMK_End) |



## <a name="see-also"></a>Consulte também  

Para obter mais informações, consulte os seguintes artigos:  

- [Avaliar o Configuration Manager em um laboratório](/sccm/core/get-started/evaluate-with-lab-environment)
- [Novidades nas versões incrementais do Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Introdução ao Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]  
> Para saber mais sobre os recursos atuais de branch que exigem autorização para habilitação, confira [Recursos de pré-lançamento](/sccm/core/servers/manage/pre-release-features).  
> 
> Para saber mais sobre os recursos atuais de branch que precisam ser habilitados primeiro, confira [Habilitar recursos opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
